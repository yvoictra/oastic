---
title: 'Customize our Linux terminal with screenFetch (Ubuntu, Debian, CentOS, Linux Mint...)'
date: Thu, 04 Jan 2018 17:28:34 +0000
draft: false
tags: ['CentOS', 'customize', 'Debian', 'Linux', 'screenfetch', 'terminal', 'Ubuntu']
categories: ['Linux', 'Ubuntu', 'Customization']
aliases: ['/customize-our-linux-terminal-with-screenfetch-ubuntu-debian-centos-linux-mint']
---

**screenFetch** is a software for GNU/Linx which shows information related to our Hardware and our Operating System, including the logo of the Linux Distro it is being used. This is the info screenFetch shows:

*   User Name
*   Host Name
*   OS with Code Name
*   Installed Kernel Info
*   System Uptime
*   List of Installed Packages
*   bash Shell Version
*   System Resolution
*   DE (Desktop Environment)
*   WM (Window Manager)
*   WM Theme
*   GTK Theme
*   Icon Theme
*   Font
*   CPU
*   RAM Usage

Here some examples: 

![](./images/screenfetch_debian.webp) 

![](./images/screenfetch_centos.webp) 

## Install screenFetch in any Linux Distro

screeenFetch can be used in a lot of GNU/Linux distros, and mostly all of them have this software in their software repositories. To install it, you have to open the terminal and use this: **Debian / Ubuntu / Linux Mint...**

```
sudo apt update
sudo apt install screenfetch
```

### CentOS

    sudo curl -o /usr/local/bin/screenfetch https://raw.githubusercontent.com/KittyKatt/screenFetch/master/screenfetch-dev && sudo chmod +x /usr/local/bin/screenfetch

### Suse / OpenSuse

    sudo zypper install screenfetch

### Arch Linux

    sudo pacman -S screenfetch

### Fedora

    sudo dnf install screenfetch

### FreeBSD

    sudo pkg install screenfetch

## Add screenFetch on User Login

To add screenFetch on User Login, you should edit the `/etc/bash.bashrc` file, and add the following line to the bottom:

    if [ -f /usr/bin/screenfetch ]; then screenfetch; fi

It is also possible to configure the output of this software.

#### To strip all color from output:

    screenfetch -N

#### Do not display ASCII distribution logo:

    screenfetch -n

#### To display only the ASCII distribution logo:

    screenfetch -L
