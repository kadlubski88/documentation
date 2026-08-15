# ARCH
## Installation
### Set keyboard layout and font
List available layout:
~~~
localectl list-keymaps
~~~
Set keyboard layout:
~~~
loadkeys <layout>
~~~
> NOTE: Use `de-latin1` for german keyboard
> NOTE: Default layout is `us`

### Verify boot mode
Get UEFI bitness:
~~~
cat /sys/firmware/efi/fw_platform_size
~~~
It should be `64`

### Connect to internet
List the network interfaces:
~~~
ip link
~~~
Set WLAN:
~~~
iwctl
~~~
|Action|Command|Comment|
|-|-|-|
|List the wlan devices|`device list`|It should be wlan0|
|Initiate scan|`station <device name> scan`|No Output|
|List available networks|`station <device name> get-networks`|Get Network name and security|
|Connect to network|`station <device name> connect <network name> <security>`|Shows passphrase prompt|
|Verify connection|`station <device name> show`||
|exit iwctl|`quit`||
> NOTE: Internet test:
>   ~~~
>   ping ping.archlinux.org
>   ~~~

### Time synchronization
Verify if time is sychronized:
~~~
timedatectl
~~~

### Partition disks
identify disks and block devices:
~~~
lsblk
~~~
Or
~~~
fdisk -l
~~~
Partitioning:
~~~
fdisk /dev/<disk>
~~~
|Action|Command|Comments|
|-|-|-|
|Print partition table|`p`||
|Delete a partition|`d`||
|Add new partition|`n`|`+1G` to make it 1GiB|
|Write table and exit|`w`||
|Quit without saving changes|`q`||

> Recommended layout:
> 1. Boot 1GiB
> 2. Swap 4GiB 
> 3. Root At least 32GiB

> NOTE: Boot and SWAP partitions can be reused from another Linux system.

### Format partitions
For Boot:
~~~
mkfs.fat -F 32 /dev/<boot partition>
~~~
> NOTE: Only if not existing

For Swap:
~~~
mkswap /dev/<swap partition>
~~~
For Root:
~~~
mkfs.ext4 /dev/<root partition>
~~~
> Note: Use `parted -l` to verify the formats

### Mount file systems
For Root:
~~~
mount /dev/<root partition> /mnt
~~~
For Boot:
~~~
mount --mkdir /dev/<root partition> /mnt/boot
~~~
For Swap:
~~~
swapon /dev/<swap partition>
~~~

### Select mirrors
Mirror servers are defined in `/etc/pacman.d/mirrirlist`. The higher a mirror is placed in the list, the more priority it is given.
Worldwide mirrors should be enough.
> NOTE: This file will be copied in the new system.

### Install essential packages
Create the new root file system and install the minimum packages.
~~~
pacstrap -K /mnt base linux linux-firmware iwd vim
~~~
> NOTE: `iwd` is for wifi (iwctl)

### Generate fstab file
Make mounting persistent:
~~~
genfstab -U /mnt >> /mnt/etc/fstab
~~~

### Enter new system
Chroot in the new system:
~~~
arch-chroot -S /mnt
~~~

### Time
Set time zone:
~~~
ln -sf /usr/share/zoneinfo/<area>/<location> /etc/localtime
~~~
Generate `etc/adjtime`:
~~~
hwclock --systohc
~~~

### Localization
Choose locales to be used:
~~~
vim /etc/locale.gen
~~~
> NOTE: Uncomment the needed entry. For example: `en_GB.UTF-8 UTF-8`

Generate locales:
~~~
locale-gen
~~~
Create `locale.conf` and add language:
~~~
echo "LANG=en_GB.UTF-8 > /etc/locale.conf
~~~

### Set keyboard layout
Create `/etc/vconsole.conf` and add keymap:
~~~
echo "KEYMAP=us" > /etc/locale.conf
~~~
> NOTE: Use `de-latin1` for german keyboard.

### Hostname
Set host name in `/etc/hostname`:
~~~
echo "<host name>" > /etc/hostname
~~~

### Initramfs
Generate initramfs:
~~~
mkinitcpio -P
~~~

### Root password
Set password for root:
~~~
passwd
~~~

### GRUB
Install grub package:
~~~
pacman -S grub efibootmgr
~~~
install grub:
~~~
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
~~~
Generate grub config:
~~~
grub-mkconfig -o /boot/grub/grub.cfg
~~~

### Reboot
Exit chroot:
~~~
exit
~~~
Unmount the partitions:
~~~
umount -R /mnt
~~~
Reboot:
~~~
reboot now
~~~
> NOTE: Remove installation medium

## Post installation
### Set Wifi
Enable and start iwd service:
~~~
systemctl enable --now iwd
~~~
Configure iwd:
~~~
vim /etc/iwd/main.conf
~~~
to add the following:
~~~
[General]
EnableNetworkConfiguration=true
~~~
Restart iwd service:
~~~
systemctl restart iwd
~~~
Set the wifi with `iwctl` like in the installation phase.

Enable and start systemd-resolved service
~~~
systemctl enable --now systemd-resolved
~~~
Set resolv configuration
~~~
ln -sf /run/systemd/resolv/stub-resolv.conf /etc/resolv.conf
~~~

### User
Install sudo:
~~~
pacman -S sudo
~~~
Add a user:
~~~
useradd -m -s /bin/bash <user name>
~~~
Set password for user:
~~~
passwd <user name>
~~~
Add user to sudoers:
~~~
EDITOR=vim visudo
~~~
To add after `root ALL=(ALL:ALL) ALL`:
~~~
<user name> ALL=(ALL:ALL) ALL
~~~
Login as the new user
~~~
logout
~~~

### Hyprland
Install hyprland and the most important packages:
~~~
sudo pacman -S hyprland kitty ttf-jetbrains-mono-nerd qt5-wayland qt6-wayland
~~~
Start hyprland:
~~~
start-hyprland
~~~