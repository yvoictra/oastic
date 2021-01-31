---
title: 'Cambiar el hostname en Ubuntu Linux'
date: Mon, 14 Jan 2019 22:22:13 +0000
draft: false
aliases: ['/es/change-hostname-in-ubuntu-linux']
tags: ['bash', 'hostname', 'hostnamectl', 'Linux', 'Ubuntu', 'vi']
categories: ['Linux', 'Ubuntu']
---

Cuando instalamos por primera vez un nuevo sistema operativo una de las primeras consultas en el proceso de instalación es definir el **hostname**.

Para cambiar el hostname de un sistema Ubuntu Linux, puedes seguir diferentes procedimientos.

## Editar los ficheros de configuración y reiniciando

Edita el fichero `/etc/hostname` utilizando el editor **vi**. Modificar el viejo nombre por el nuevo.

    $ sudo vi /etc/hostname

Edita el fichero `/etc/hosts` y reemplaza cualquier ocurrencia del viejo nombre por el nuevo nombre.

    $ sudo vi /etc/hosts

Reinicia el sistema para que los cambios surtan efecto.

    $ sudo reboot

## Cambiando el hostname sin reiniciar el sistema

Como en el procedimiento anterior, es necesario editar algunos ficheros, pero también podemos utilizar la herramienta **hostname** para definir el nuevo hostname sin reiniciar.

```
$ sudo vi /etc/hostname  
$ sudo vi /etc/hosts  
$ sudo hostname new-server-name 
```

## Cambiando el hostname con **hostnamectl**

Éste es el método más sencillo, pero no valido para todas las versiones de Ubuntu. Sólo funciona desde Ubuntu 16.04 y posteriores.

```
$ hostnamectl  
$ sudo hostnamectl set-hostname new-server-name  
$ hostnamectl
```
