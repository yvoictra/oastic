---
title: 'Create a new user in Ubuntu from terminal'
date: Wed, 01 Apr 2020 21:54:34 +0000
draft: false
tags: ['Linux', 'password', 'Ubuntu', 'user']
categories: ['Linux', 'Ubuntu']
aliases: ['/create-a-new-user-in-ubuntu-from-terminal']
---

In order to create a new user in a Linux Ubuntu distribution from terminal, you have to use this command.

    sudo adduser username

After this, the system will ask you some parameters included the **password**.

```
[23:43:24] ubuntu|zoar:~$ sudo adduser yvoictra
Adding user `yvoictra' ... Adding new group`yvoictra' (1001) …
Adding new user `yvoictra' (1001) with group`yvoictra' …
Creating home directory `/home/yvoictra' ... Copying files from`/etc/skel' …
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for yvoictra
Enter the new value, or press ENTER for the default
Full Name []: Yvoictra
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n] y
[23:46:40] ubuntu|zoar:~$
```

And it's sucessfully created.
