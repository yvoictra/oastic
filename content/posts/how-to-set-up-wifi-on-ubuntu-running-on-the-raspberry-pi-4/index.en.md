---
title: 'How to set up WIFI on Ubuntu running on the Raspberry Pi 4'
date: Thu, 02 Apr 2020 21:18:31 +0000
draft: false
tags: ['ifconfig', 'Linux', 'Raspberry', 'Ubuntu', 'WIFI', 'Wireless']
categories: ['Linux', 'Ubuntu', 'Raspberry']
aliases: ['/how-to-set-up-wifi-on-ubuntu-running-on-the-raspberry-pi-4']
---

First step is to check the status of the interfaces. For this, we will use the _net-tools_ package.

    sudo apt install net-tools

Then, we can see the interfaces status

    ifconfig -a

In my case, I have this status of my interface wlan0:

```
ubuntu@ubuntu:~$ ifconfig -a wlan0
wlan0: flags=4098<BROADCAST,MULTICAST> mtu 1500
        ether dc:a6:32:6c:xx:xx txqueuelen 1000 (Ethernet)
        RX packets 0 bytes 0 (0.0 B)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 0 bytes 0 (0.0 B)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

```

In the flags only there are 2 _(BROADCAST,MULTICAST)_, but there is no "UP" flag.

In order to configure the WIFI network, I recommend to use the program **netplan**, available from Ubuntu 18.04. It doesn't require any additional installation, it comes with the base system.

For the wireless configuration, you may follow the example:

    /usr/share/doc/netplan/examples/wireless.yaml

so next step is to copy the file in the directory `/etc/netplan/`

    sudo cp /usr/share/doc/netplan/examples/wireless.yaml /etc/netplan/

Then, edit the new file created and change the values. Probably you want to enable dhcp configuration and remove static parts. In my case, the file looks like this:

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

Last step is to execute the netplan

    sudo netplan try

As an alternative, you could modify the existing file `/etc/netplan/50-cloud-init.yaml` which is created by default. In this file you could add the WIFI configuration.

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

Last step is to execute the netplan

    sudo netplan try

After this, your WIFI should be established. You could check it with ifconfig tool:

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

And now the flags UP and RUNNING are set.
