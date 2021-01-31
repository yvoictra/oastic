---
title: 'Cómo añadir alias a tu Linux'
date: Sat, 24 Oct 2020 09:43:16 +0000
draft: false
tags: ['alias', 'aliases', 'bash', 'Linux', 'Ubuntu', 'personalizar']
categories: ['Linux', 'Ubuntu', 'Personalización']
aliases: ['/es/how-to-add-alias-to-your-linux']
---

Utilizando un sistema operativo Linux, hay un alto nivel de personalización, dependiendo de tus preferencias o necesidades.

Una cosa importante es crear alias de los comandos más comunes para optimizar el tiempo que utilizas. En micaso, adoro utilizar ".." en lugar de "cd .." o "update" para actualizar todas las actualizaciones pendientes del software de Ubuntu.

Aquí os pongo mi lista de alias, no es grande pero es lo que yo utilizo mayormente en los servidores que tengo con Linux.

Para instalarlos, lo primero que tienes que hacer es editar el fichero `~/.bash_alises`así:

    root@rhea:~# vi ~/.bash_aliases

E insertar estas líneas:

```
alias l="ls -lh --color"
alias rm="rm -i"
alias ..="cd .."
alias ...="cd ../.."
alias update='sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade'
alias clean='sudo apt-get autoclean && sudo apt-get autoremove && sudo apt-get clean'
```

Ahora puedes actualizar los alias usados en tu sesión actual:

```
root@rhea:~# source ~/.bash_aliases
root|rhea:~$
```

Y desde ese momento, ya puedes utilizarlos.
