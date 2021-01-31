---
title: 'Crear un nuevo usuario en Ubuntu desde la línea de comandos'
date: Wed, 01 Apr 2020 21:54:34 +0000
draft: false
tags: ['Linux', 'password', 'contraseña', 'Ubuntu', 'usuario']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/create-a-new-user-in-ubuntu-from-terminal']
---

Para crear un usuario nuevo en una distribución de Linx Ubuntu desde la terminal, debes de usar el siguiente comando.

    sudo adduser username

Tras esto, el sistema the preguntará algunos parámetros incluida la **contraseña**.

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

Y ya está creado correctamente.
