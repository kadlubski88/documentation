# Linux parallel installation
How to install different Linux distros from an existing distro (Ubuntu)
## General
1. Install arch installation scripts for simplicity
   ~~~bash
    sudo apt install arch-install-scripts
    ~~~
2. Create root partition
    ~~~bash
    sudo fdisk /dev/sdX
    # n -> +32GB
    # w
    ~~~
3. Format the partition to ext4
    ~~~bash
    sudo mkfs.etx4 /dev/sdXN
    ~~~
4. Mount the new root partition to
    ~~~bash
    sudo mount /dev/sdXN /mnt
    ~~~
## Debian minimal
1. Install debootstrap
    ~~~bash
    sudo apt install debootstrap
    ~~~
2. Get debian keyrings
    ~~~bash
    sudo apt install debian-archive-keyring
    ~~~
3. Install a Debian bootstrap to the new root partiotion
    ~~~bash
    sudo debootstrap stable /mnt http://deb.debian.org/debian
    ~~~
4. Generate a fstab for the new OS
    ~~~bash
    genfstab -U /mnt | sudo tee /mnt/etc/fstab
    ~~~
    > NOTE: It will also automaticaly add the swap if already existing.
5. Chroot to the new root
    ~~~bash
    sudo arch-chroot /mnt
    ~~~
6. Source the default profile
    ~~~bash
    source /etc/profile
    ~~~
7. Install the kernel
    ~~~bash
    apt update
    apt install linux-image-amd64
    ~~~
8. Install vim and locales
    ~~~bash
    apt install vim locales
    ~~~
9. Choose locale package
    ~~~bash 
    vim /etc/locale.gen
    # uncomment needed locale (e.g. en_US.UTF-8 UTF-8)
    ~~~
10. Generate locale
    ~~~bash
    locale-gen
    ~~~
11. Set local time
    ~~~bash
    # e.g. Berlin
    ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
    ~~~
12. Set hostname
    ~~~bash
    echo"<new_hostname>" > /etc/hostname
    ~~~
13. Set root password
    ~~~bash
    passwd
    ~~~
14. [optional] Set keyboard configuration
    ~~~bash
    apt install keyboard-configuration
    setupcon
    ~~~
15. [optional] Install console configuration tool
    ~~~bash
    apt install console-setup
    ~~~ 
16. [optional] Install dbus
    Needed for localctl, timedatectl,...
    ~~~bash
    apt install dbus
    ~~~
17. Exit chroot
    ~~~bash
    exit
    ~~~
18. Configure grub
    ~~~bash
    sudo nano /etc/default/grub
    # uncomment GRUB_DISABLE_OS_PROBER=false
    # set GRUB_TIMEOUT=10
    ~~~
19. Update grub
    ~~~bash
    sudo grub-mkconfig -o /boot/grub/grub.cfg
    ~~~
20. Reboot
## Arch