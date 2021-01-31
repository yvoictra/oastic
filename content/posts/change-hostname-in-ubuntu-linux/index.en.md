---
title: 'Change hostname in Ubuntu Linux'
date: Mon, 14 Jan 2019 22:22:13 +0000
draft: false
aliases: ['/change-hostname-in-ubuntu-linux']
tags: ['bash', 'hostname', 'hostnamectl', 'Linux', 'Ubuntu', 'vi']
categories: ['Linux', 'Ubuntu']
---

When we first install a new Operating System one of the typical request of the installation process is to set the **hostname**.

To change the hostname in Ubuntu Linux system, you can follow different procedures.

## Editing system configuration files

Edit the file `/etc/hostname` using the vi editor. Modify the old name and set the new one.

    $ sudo vi /etc/hostname

Edit the file `/etc/hosts` and replace any ocurrence of the old name with the new one.

    $ sudo vi /etc/hosts

Reboot the system to make the changes to take effect.

    $ sudo reboot

## Changing the hostname without reboot the system

As in the previous method, it is also needed to edit some files, but also to use the **hostname** command to set the new hostname without reboot.

```
$ sudo vi /etc/hostname  
$ sudo vi /etc/hosts  
$ sudo hostname new-server-name 
```

## Changing the hostname with **hostnamectl**

This is the easiest method, but not valid for all Ubuntu releases. It only works from Ubuntu 16.04 and above.

```
$ hostnamectl  
$ sudo hostnamectl set-hostname new-server-name  
$ hostnamectl
```
