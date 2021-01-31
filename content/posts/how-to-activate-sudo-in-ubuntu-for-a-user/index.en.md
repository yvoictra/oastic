---
title: 'How to activate SUDO in Ubuntu for a user'
date: Sat, 18 Apr 2020 11:23:49 +0000
draft: false
tags: ['Linux', 'root', 'sudo', 'Ubuntu', 'user']
categories: ['Ubuntu' , 'Linux']
aliases: ['/how-to-activate-sudo-in-ubuntu-for-a-user']
cover:
    image: "/img/create-sudo-user-on-ubuntu.webp"
    alt: "Sudo Ubuntu"
    caption: "Sudo Ubuntu"
---

The **sudo** command allows users to run programs with the security privileges of another user, by default, the **root** user.

First if all, [the user should be created](/posts/create-a-new-user-in-ubuntu-from-terminal/) in the system if it doesn't exists yet.

On **Ubuntu** systems, by default members of the **group sudo** are granted to sudo command access.

Once the user is created, from root user, or a user with sudo access, you have to execute this command to add the user to sudo group.

    sudo usermod -a -G sudo username

After this, the user will have access to sudo command.

To check if it is working, log in the session of the new user:

    su - username

and execute the command:

    sudo whoami

The output should be "root", so you confirm the access has been granted successfully.
