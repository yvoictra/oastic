---
title: 'Cómo configurar la WIFI en Ubuntu sobre una Raspberry Pi 4'
date: Thu, 02 Apr 2020 21:18:31 +0000
draft: false
tags: ['ifconfig', 'Linux', 'Raspberry', 'Ubuntu', 'WIFI', 'Wireless']
categories: ['Linux', 'Ubuntu', 'Raspberry']
aliases: ['/es/how-to-set-up-wifi-on-ubuntu-running-on-the-raspberry-pi-4']
---

El primer paso es revisar el estado del interfaz. Para ello, usaremos el paquete _net-tools_.

    sudo apt install net-tools

Tras esto, podemos ver el estado del interfaz

    ifconfig -a

En mi caso, éste es el estado de mi interfaz wlan0:

```
ubuntu@ubuntu:~$ ifconfig -a wlan0
wlan0: flags=4098<BROADCAST,MULTICAST> mtu 1500
        ether dc:a6:32:6c:xx:xx txqueuelen 1000 (Ethernet)
        RX packets 0 bytes 0 (0.0 B)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 0 bytes 0 (0.0 B)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

```

En los flags del ineterfaz solo hay 2 _(BROADCAST,MULTICAST)_, pero no está el flag "UP".

Para configrar la red WIFI, yo recomiendo utilizar el programa **netplan**, disponible desde Ubuntu 18.04. No necesita ninguna instalación adicional, viene de serie con el sistema.

Para la configuración del wireless, debes de seguir el siguiente ejemplo:

    /usr/share/doc/netplan/examples/wireless.yaml

el siguiente paso es copiar el fichero en el directorio `/etc/netplan/`

    sudo cp /usr/share/doc/netplan/examples/wireless.yaml /etc/netplan/

Entonces, edita el nuevo fichero creado y cambia los valores. Probablemente quieras activar la configuración de dhcp y eliminar la parte estática. En mi caso, el fichero tiene esta pinta:

```
network:
  version: 2
  renderer: networkd
  wifis:
    wlan0:
      dhcp4: yes
      dhcp6: no
      access-points:
        "<your network ESSID>":
          password: "<your WIFI Password>"
```

El último paso es ejecutar netplan

    sudo netplan try

Como alternativa, podrías modificar el fichero existente `/etc/netplan/50-cloud-init.yaml` que está creado por defecto. En este fichero podrías añadir la configuración de WIFI.

```
network:
    version: 2
    ethernets:
        eth0:
            dhcp4: true
            optional: true
    wifis:
        wlan0:
            dhcp4: true
            dhcp6: false
            access-points:
                    "<your network ESSID>":
                     password: "<your WIFI Password>"
```

El último paso es ejecutar netplan

    sudo netplan try

Tras esto, tu WIFI debería de estar establecida. Podrías comprobarlo con la herramienta ifconfig:

```
ubuntu@ubuntu:~$ ifconfig -a wlan0
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.220  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::dea6:32ff:fe6c:xxxx  prefixlen 64  scopeid 0x20
        ether dc:a6:32:6c:xx:xx  txqueuelen 1000  (Ethernet)
        RX packets 5047  bytes 936652 (936.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 78  bytes 9491 (9.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Y ahora, los flags UP y RUNNING están activados.
