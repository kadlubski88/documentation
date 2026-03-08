# LFS

## Partitioning
- fdisk
- partition table: gpt
- 1GB EFI System (boot)
- 4GB Linux swap
- 26GB linux filesystem (root)

## Make file system
- "mkfs.ext4" for root
- "mkfs.fat -F 32" for boot
- "mkswap" for swap

## Environment
~~~
export LFS=/mnt/lfs
umask 022
~~~

## Mounting new partition
~~~
mkdir -vp $LFS
mount -v -t ext4 /dev/sdb3 $LFS
mkdir -vp $LFS/boot/efi
mount -v -t fat /dev/sdb1 $LFS/boot/efi
/sbin/swapon -v /dev/sdb2
~~~

## Sources
~~~
mkdir -v $LFS/sources
cd $LFS/sources
~~~
wget list of sources
wget list of md5sums
wget sources
~~~
wget --input-file=wget-list-systemd --continue --directory-prefix=$LFS/sources
md5sum -c md5sums
~~~

## LFS file system
~~~
mkdir -pv $LFS/{etc,var} $LFS/usr/{bin,lib,sbin}

for i in bin lib sbin; do
  ln -sv usr/$i $LFS/$i
done

mkdir -pv $LFS/lib64
~~~
> /usr/lib64 should never exists

## LFS user
~~~
groupadd lfs
useradd -s /bin/bash -g lfs -m -k /dev/null lfs
passwd lfs
chown -v lfs $LFS/{usr{,/*},var,etc,tools}
chown -v lfs $LFS/lib64

su - lfs
~~~

## Setup environment for lfs user
for login shell
~~~
cat > ~/.bash_profile << "EOF"
exec env -i HOME=$HOME TERM=$TERM PS1='\u:\w\$ ' /bin/bash
EOF
~~~

for non-login shell
~~~
cat > ~/.bashrc << "EOF"
set +h
umask 022
LFS=/mnt/lfs
LC_ALL=POSIX
LFS_TGT=$(uname -m)-lfs-linux-gnu
PATH=/usr/bin
if [ ! -L /bin ]; then PATH=/bin:$PATH; fi
PATH=$LFS/tools/bin:$PATH
CONFIG_SITE=$LFS/usr/share/config.site
export LFS LC_ALL LFS_TGT PATH CONFIG_SITE
EOF
~~~

set parallel make
~~~
cat >> ~/.bashrc << "EOF"
export MAKEFLAGS=-j$(nproc)
EOF
~~~

resource environment
~~~ 
source ~/.bash_profile
~~~

## Build
- all sources and patches are in /mnt/lfs/sources/
- cd /mnt/lfs/sources
- tar -xvf \<package.tar.xz>
- cd \<package>
- follow instruction for compiling
- cd /mnt/lfs/sources
- rm -rf \<extracted package>

### Typical compiling workflow
1. 
    ~~~
    ./configure --prefix=/usr --host=$LFS_TGT --build=$(build-aux/config.guess)
    ~~~
2. 
    ~~~
    make
    ~~~
3. 
    ~~~
    make DESTDIR=$LFS install
    ~~~

### Compiling cross-toolchain
|package|pass|comments|
|-|-|-|
|binutils|1|linker, assembler, tools for handlings object files|
|gcc|1|GNU compiler collection (C, C++)|
|linux api header|-|expose kernels'api for use by Glibc|
|glibc|-|main C library|
|libstdc++|-|standard C++ library using gcc(not buildable before because glibc is needed)|

### Cross compiling temporary tools
|package|pass|comments|
|-|-|-|
|m4|-|macro processor|
|ncurses|-|terminal independent handling of character screens|
|bash|-|bourne again shell| 
|coreutils|-|basic utility programms needed by every OS|
|diffutils|-|show differences between files or directories|
|file|-|determine the type of a given file or files|
|findutils|-|find files and xargs|
|gawk|-|manipulating text files|
|grep|-|searching through the contents of files|
|gzip|-|compressing and decompressing files|
|make|-|generation of executable and other non-source files|
|patch|-|modify or create file by applying a patch created by diff|
|sed|-|stream editor|
|tar|-|tar archives creation and manipulation|
|xz|-|compressing and decompressing files|
|binutils|2|linker, assembler, tools for handlings object files|
|gcc|2|GNU compiler collection (C, C++)|
