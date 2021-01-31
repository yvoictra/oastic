---
title: 'Cómo activar SUDO en Ubuntu para un usuario'
date: Sat, 18 Apr 2020 11:23:49 +0000
draft: false
tags: ['Linux', 'root', 'sudo', 'Ubuntu', 'usuario']
categories: ['Ubuntu' , 'Linux']
aliases: ['/es/how-to-activate-sudo-in-ubuntu-for-a-user']
cover:
    image: "/img/create-sudo-user-on-ubuntu.webp"
    alt: "Sudo Ubuntu"
    caption: "Sudo Ubuntu"
---

El comando **sudo** permite a los usuarios a ejecutar programas con los privilegios de seguridad de otro usuario, por defecto, del usuario **root**.

Lo primero, [el usuario debe de ser creado](/es/posts/create-a-new-user-in-ubuntu-from-terminal/) en el sistema si no existe aún.

En sistemas **Ubuntu**, por defecto los miembros del **grupo sudo** tienen permiso para acceder al comando sudo.

Una vez el usuario está creado, desde el usuario root o desde un usuario con acceso al comando sudo, tienes que ejecutar este comando para añadir al usuario al grupo sudo.

    sudo usermod -a -G sudo username

Tras esto, el usuario tendrá acceso al comando sudo.

Para revisar si está funcionado, logéate en una sesión con el nuevo usuario:

    su - username

y ejecuta este comando:

    sudo whoami

La salida debe de ser "root", así que se confirma que el acceso se ha dado de forma satisfactoria.
