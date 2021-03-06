---
layout: page
title: Install Arch Linux as a guest VM on Parallels 14
date: 2019-07-12
---

## TL;DR

To install Arch Linux with working Parallels Tools without making any code changes to the tools, before starting the
installation process with pacman, change the installation source in `mirrorlist` to an archive url that still uses a v4
kernel package. Then when running a full system update with `pacman` ensure all kernel packages are excluded from the
update.

After the Arch Linux process completes, follow the Parallels KB article on installing Parallels Tools on Arch Linux and
everything should work OK.

## Introduction

As of 12th July 2019 it is not possible to get Parallels Tools working with Linux Kernel v5. As Arch
Linux is a rolling-release distro that is always trying to install the latest versions of packages, including the kernel
, this can make it difficult to get Arch Linux to work on Parallels 14.

I recently spent some time trying to get around this and managed to get it working by install a version of Arch Linux
with a 4.x version of the linux kernel and then specifically excluding updates to this when doing a system update with
`pacman`.

Since I did this, I noticed that others on the Parallels forum have found ways to change the parallels tools source to
make it work with v5 of the kernel while we still wait for official support from Parallels.

If you do not want to go through these steps for any reason, then the way I describe below can be used as an alternative
.

## Preparation

There are many guides and YouTube videos going into great depth the steps required to install Arch Linux. Most of these
will be equally applicable to this guide barring a few key points which I will mention. For reference, here are the
guides I found the most helpful:

* [Arch Wiki Installation guide](https://wiki.archlinux.org/index.php/Installation_guide)
* [Parallels KB article - Installing Arch Linux OS in Parallels Desktop](https://kb.parallels.com/en/124124)
* [YouTube: Full Arch Linux Install (Savage Edition!) by Luke Smith](https://youtu.be/4PBqpX0_UOc)

### Download latest Arch Linux install ISO

Even though the trick to get this working is to use an older kernel, it should be possible to use as up to date ISO
image as possible. The important part later

Download this and create a new VM image in Parallels using it as normal (select More Linux, Other Linux for the OS type).

> I normally customise the settings at this point and give a bit more CPU / Memory and ensure any unneeded integrations
> have been turned off or disabled like application and cloud drive sharing etc.

## Pre-checks and initial setup

As stated, there are many in depth guides on installing Arch Linux so I'm going to fly through the steps and commands _I_
use. YMMV if you follow along exactly.

Boot the ISO image in your new Parallels VM image, once booted:

Check you have networking by pinging archlinux.org `ping archlinux.org`

Load keyboard layout if non-US: `loadkeys uk`

Use NTP: `timedatectl set-ntp true`

## Configure Partitions

This is based on a standard 64 GB partition create by Parallels

Confirm disk id (should be `/dev/sda`: `fdisk -l`

`fdisk /dev/sda` to start partitionig the disk

### Boot Partition

```
n
p
1
[Enter for default]
+256M
```

### Swap Partition

```
n
p
2
[Enter for default]
+8G
```

### Programs / OS Partition

```
n
p
3
[Enter for default]
+32G
```


### Home Partition

```
n
p
4
[Enter for default]
[Enter for default]
```

> You may want to play with these sizes if you want a bigger program partition vs home etc or just use a bigger disk image

`w` to write partition table

## Create Filesystems

```
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda3
mkfs.ext4 /dev/sda4

mkswap /dev/sda2
swapon /dev/sda2
```

## Mount partitions

```
mount /dev/sda3 /mnt

mkdir /mnt/boot
mkdir /mnt/home

mount /dev/sda1 /mnt/boot
mount /dev/sda4 /mnt/home
```

## Update mirror list with archive version

**Now comes the important part** we need to update the mirrorlist file so it points to an archive with the 4.x kernel:

> I am using vim editor commands below, substitute with editor of your choice e.g. nano

```
cd /etc/pacman.d
cp mirrorlist mirrorlist.bak
vim mirrorlist
dG
I
Server=https://archive.archlinux.org/repos/2019/03/05/$repo/os/$arch
[Esc]
SHIFT-Z-Z

cd ~

pacstrap /mnt base base-devel (optional packages e.g. vim)
```

## Generate fstab

`genfstab -U /mnt >> /mnt/etc/fstab`

## Finalise and enable persistent

```
arch-chroot /mnt
pacman -S networkmanager
systemctl enable NetworkManager
```

## Make bootable

```
pacman -S grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

## Set password

`passwd`

## Set locale and timezone

`vim /etc/locale.gen` and uncomment as many locales as you need e.g. en_GB.UTF-8, en_GB.ISO-8859-1.
`locale-gen`

`vim /etc/locale.conf` (will createa a file)
add lang e.g. `LANG=en_GB.UTF-8`

find your timezone in `/usr/share/zoneinfo` then create a symlink e.g. `ln -sf /usr/share/zoneinfo/Europe/London /etc/localtime`

## Set a hostname and reboot

`vim /etc/hostname`

```
exit
umount -R /mnt
reboot
```

> At this point, if you can login successfully after the reboot using root and the password you set with passwd,
> shutdown the image and crate a snapshot or copy the disk image just in case you need to go back.

## Add user and assign sudo

login as root

```
useradd -m -g wheel [username]
passwd [username]
```

`visudo`, find and uncomment `%wheel ALL=(ALL) ALL` and save and close the file.

As as a best practice, log out out of the root account and log back in as the user just created. Of course most commands
will now need to be run with `sudo`.

## Install xorg packages

> You can swap xfce4 with a desktop environment of your choice such as gnome.

(when prompted, choose option 1: `libglvnd`)

```
sudo pacman -S xorg-server xorg-xinit xorg-apps mesa-libgl xterm
sudo pacman -S xf86-video-vesa
```

### XFCE 4

```
sudo pacman -S xfce4 xfce4-goodies sddm
sudo systemctl enable sddm.service
```

### GNOME

```
sudo pacman -S gnome
sudo systemctl enable gdm.service

```

> the parallels guide says to include xorg-server-utils but this has changed to xorg-apps

Now restart and login to the desktop environment.

> This may not be needed but is worth adding just to be sure: When the Grub menu appears, press `e` then find the the
linux line, go to the end and add `iomem=relaxed` and press `F10` to continue booting.

## Install parallels tools

Enter the following command into the terminal:

```
sudo ln -sf /usr/lib/systemd/scripts/ /etc/init.d
export def_sysconfdir=/etc/init.d
sudo touch /etc/X11/xorg.conf
sudo pacman -S base-devel python2 linux-headers
sudo ln -sf /usr/bin/python2 /usr/local/bin/python
sudo touch /usr/lib/systemd/system/parallels-tools.service
```

Add the following e.g. `sudo vim /usr/lib/systemd/system/parallels-tools.service`

```
[Unit]
Description=Parallels Tools
[Service]
Type=oneshot
ExecStart=/usr/lib/systemd/scripts/prltoolsd start
ExecStop=/usr/lib/systemd/scripts/prltoolsd stop
RemainAfterExit=yes
[Install]
WantedBy=multi-user.target
```

Now mount Parallels Tools image from Parallels Actions menu (Install Parallels Tools...).

You may find some desktop environments automatically mount to `/run/media/[username]/Parallels Tools`, but if not,
you can mount manually and run as follows:

```
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
sudo ./install
```

Choose, Next and Next again and once installed **don't** reboot just yet, instead exit and type:

```
sudo systemctl enable parallels-tools.service
sudo rm /usr/local/bin/python
reboot
```

## Switch back to latest mirrors and upgrade all packages except kernel

`sudo vim /etc/pacman.d/mirrorlist`

comment out the archive mirror and paste a real mirror from https://www.archlinux.org/mirrorlist/ e.g.
`Server=http://mirrors.manchester.m247.com/arch-linux/$repo/os/$arch`

> There is also a tool on archlinux.org that will generate a complete list of mirrors, or just those matching a given
criteria

Resync the package sources and update all packages except kernel and headers:

```
sudo pacman -Syy
sudo pacman -Syu --ignore linux,linux-headers,linux-lts,linux-lts-headers,linux-api-headers
```

> It should be possible to add the ignore packages to /etc/pacman.conf so you don't have to keep remembering to add the
switches, but unfortunately I have not been able to get this:
sudo vim /etc/pacman.conf
IgnorePkg linux,linux-headers,linux-lts,linux-lts-headers,linux-api-headers

