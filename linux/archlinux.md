---
layout: default
title: Archlinux
parent: Linux
---

# Archlinux

archlinux is a Linux distribution based on the Linux kernel and other open-source software.

## Installation

### Partitioning

Show current partitions:

```shell
~# fdisk -l
```

Format your desired partition:

```shell
~# mkfs.ext4 /dev/sda1
```

### Installing Base System

Mount your partition and start the installation:

```shell
~# mount /dev/sda1 /mnt
~# pacstrap /mnt base base-devel
```

Generate fstab:

```shell
~# genfstab -U /mnt >> /mnt/etc/fstab
~# cat /mnt/etc/fstab
```

Change root into the new system:

```shell
~# arch-chroot /mnt /bin/bash
```

### Setting Up Users

Set root password:

```shell
~# passwd
```

Create a new user:

```shell
~# useradd -m -g users -G wheel,storage,power -s /bin/bash lsong
~# passwd lsong
```

### Basic System Configuration

Synchronize and update repositories:

```shell
~# pacman -Syu
```

Install sudo:

```shell
~# pacman -S sudo
```

### Bootloader Installation

Install and configure Grub:

```shell
~# pacman -S grub os-prober
~# grub-install /dev/sda
~# grub-mkconfig -o /boot/grub/grub.cfg
```

When ready, exit and reboot:

```shell
~# exit
~# umount -R /mnt
~# reboot
```

## GUI Installation

### X Window System

Install basic X server components:

```shell
~# pacman -S xorg-server xorg-xinit
```

Or, install the full Xorg group:

```shell
~# pacman -S xorg xorg-xinit
```

Start the X server (this will start to a blank screen):

```shell
~$ startx
```

### Graphics Driver Installation

Identify your graphics card:

```shell
~$ lspci | grep VGA
```

Install the appropriate driver, e.g., for Intel:

```shell
~# pacman -S xf86-video-intel
```

For other graphic cards, refer to: [ArchWiki Xorg Driver Installation](https://wiki.archlinux.org/index.php/Xorg#Driver_installation)

### Desktop Environments

+ [LightDM](linux/lightdm)

### Window Managers

**XFCE**:

```shell
~# pacman -S xfce4 xfce4-goodies
~$ startxfce4
```

**i3**:

```shell
~# pacman -S i3-wm i3status i3lock
```

[bspwm](bspwm):

```shell
~# pacman -S bspwm
```

### Supplementary Tools and Utilities

From status bars to launchers and languages, choose what suits you:

Status Bars: `i3status`, `Polybar`

Launchers: `rofi`, `dmenu`

Golang:

```shell
~# pacman -S go
~# ln -sf /usr/lib/go /usr/local/go
```

AUR Helper - Yay:

```shell
~# pacman -S --needed git base-devel
~$ git clone https://aur.archlinux.org/yay.git
~$ cd yay
~$ makepkg -si
```

Audio:

```shell
~# pacman -S alsa-utils pulseaudio
```

Network:

```shell
~# pacman -S networkmanager network-manager-applet xfce4-notifyd
```

Fonts:

```shell
~# pacman -S noto-fonts-cjk
```

---