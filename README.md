# Arch Linux Sugar Desktop Environment Setup Guide

```bash
### Prerequisites
### Ensure you have a stable internet connection and the latest Arch Linux ISO installed on your system.  <br>


### System Update
`pacman -Syu`  <br>


### Partitioning and Mounting
### Use fdisk or cfdisk to create and format partitions:
### Example Commands:  <br>


### View available disks
`fdisk -l`  <br>


### Partition a disk (replace /dev/sdX with your disk name)
`fdisk /dev/sdX`  <br>


### Format the partitions
`mkfs.ext4 /dev/sdX1`
`mkfs.fat -F 32 /dev/sdX2`  <br>


### Mount the filesystem
`mount /dev/sdX1 /mnt`
`mkdir /mnt/boot`
`mount /dev/sdX2 /mnt/boot`  <br>


### Install Essential Packages
`pacstrap /mnt base linux linux-firmware`  <br>


### System Configuration
### Generate fstab:
`genfstab -U /mnt >> /mnt/etc/fstab`  <br>


### Chroot into Installed System
`arch-chroot /mnt`  <br>


### Set Time Zone
`ln -sf /usr/share/zoneinfo/Region/City /etc/localtime`
`hwclock --systohc`  <br>


### Locale Configuration
### Uncomment your locale in /etc/locale.gen (e.g., en_US.UTF-8 UTF-8)
`nano /etc/locale.gen`
`locale-gen`
`echo "LANG=en_US.UTF-8" > /etc/locale.conf`  <br>


### Set Hostname
`echo "myhostname" > /etc/hostname`  <br>


### Network Configuration
`pacman -S networkmanager`
`systemctl enable NetworkManager`  <br>


# Setting Up Sugar Desktop Environment (DE)
### Install Sugar desktop environment and its packages
`pacman -S sugar sugar-fructose sugar-runner`  <br>


### Start Sugar Manually (Optional)
### To start Sugar manually, create an .xinitrc file:
`echo "exec sugar" > ~/.xinitrc`
`startx`  <br>


# Install Bootloader
### Install GRUB bootloader
`pacman -S grub efibootmgr`  <br>


### Install GRUB to the EFI directory (adjust /dev/sdX):
`grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`
`grub-mkconfig -o /boot/grub/grub.cfg`  <br>


### Finalize Installation
### Exit chroot:
`exit`  <br>


### Unmount Partitions
`umount -R /mnt`  <br>


### Reboot System
`reboot`  <br>


# Troubleshooting
### Mirrorlist Errors:
### If no mirrors are found, update the mirror list:
`reflector --country 'YourCountry' --latest 5 --sort rate --save /etc/pacman.d/mirrorlist`  <br>


### Replace 'YourCountry' with your actual country name for optimal speed.  <br>


### X Server Issues:
### If startx fails, ensure the X server is installed:
`pacman -S xorg-server xorg-xinit`  <br>

