---
title: 'Cómo resolver nombres de hosts en una LAN con Ubuntu'
date: Sun, 19 Apr 2020 14:35:52 +0000
draft: false
tags: ['avahi', 'ficheros', 'hostnames', 'LAN', 'Linux', 'mdns4', 'mdns4_minimal', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/how-to-resolve-lan-hostnames-with-ubuntu']
---

Por defecto, la instalación Ubuntu desktop nos proporcionará la resolución de DNS configurada, sin embargo, en la instalación de Ubuntu Server **avahi-daemon** (o mdnsresponder) es necesario que sea instalado para proporcionar resolución DNS de la LAN local.

En mi caso, encontré el error "_Temporary failure in name resolution_" cuando intentaba resolver una máquina en mi LAN desde Ubuntu.

```
yvoictra@zoar:~$ ping erie.local  
ping: erie.local: Temporary failure in name resolution
```

Para solucionar este problema, no es necesario instalar un servidor de DNS en la red LAN. Podemos utilizar el protocolo **mDNS** (Multicast Domain Name System). Este protocolo se utiliza para resolver nombres de hosts en una pequeña red local (LAN). El servicio **mDNS** puede ser contactado usando consultas UDP sobre sobre el puerto 5353. El protocolo mDNS está publicado en la RFC6762 e implementado por los servicios **Apple Bonjour** y **avahi-daemon**.


    $ sudo apt-get install libnss-mdns

Hay un orden de búsqueda específico acorde a cómo se ejecuta. Este orden se define en el fichero de configuración `/etc/nsswitch.conf`.

```
yvoictra@zoar:~$ cat /etc/nsswitch.conf
# /etc/nsswitch.conf
#
# Example configuration of GNU Name Service Switch functionality.
# If you have the `glibc-doc-reference' and `info' packages installed, try:
# `info libc "Name Service Switch"' for information about this file.

passwd:         files systemd
group:          files systemd
shadow:         files
gshadow:        files

hosts:          files dns
networks:       files

protocols:      db files
services:       db files
ethers:         db files
rpc:            db files

netgroup:       nis
```

En este fichero, en lo que estamos interesados en la línea con "_hosts_". La columna _files_ significa el uso del fichero `/etc/hosts`, y el término _dns_ significa el uso del Servicio Domain Name. Si el término “_files_” esta localizado antes del término “_dns_”, esto signnifica que el sistema intentara primero encontrar un dominio en el fichero `/etc/hosts`, y sólo entonces lo intentará buscar en un DNS. Ésta es la configuración por defecto.

Los hostnames están guardados en el fichero `/etc/hostname`, el sistema primero mira en ese fichero, y si no lo encuentra ahí, mira en el fichero `/etc/hosts`.

Tras la instalación de **libnss-mdns**, la línea del fichero `/etc/nsswitch.conf` debería de ser así:

    hosts:         files mdns4_minimal [NOTFOUND=return] dns mdns4

Así que ahora, antes de utilizar el servidor de DNS, intentará resolver los dominios `.local`.

Tras esto, ahora puedo resolver mis máquinas de la LAN:

```
yvoictra@zoar:~$ ping erie.local
PING erie.local (192.168.1.211) 56(84) bytes of data.
64 bytes from 192.168.1.211 (192.168.1.211): icmp_seq=1 ttl=64 time=4.66 ms
64 bytes from 192.168.1.211 (192.168.1.211): icmp_seq=2 ttl=64 time=2.68 ms
64 bytes from 192.168.1.211 (192.168.1.211): icmp_seq=3 ttl=64 time=2.31 ms
64 bytes from 192.168.1.211 (192.168.1.211): icmp_seq=4 ttl=64 time=2.56 ms
^C
--- erie.local ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 2.307/3.051/4.659/0.937 ms
yvoictra@zoar:~$ 
```

Y esto es todo.
