---
title: 'How to resolve LAN hostnames with Ubuntu'
date: Sun, 19 Apr 2020 14:35:52 +0000
draft: false
tags: ['avahi', 'files', 'hostnames', 'LAN', 'Linux', 'mdns4', 'mdns4_minimal', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/how-to-resolve-lan-hostnames-with-ubuntu']
---

By default, Ubuntu desktop installation will provide DNS resolving configured, however in Ubuntu server installation **avahi-daemon** (or mdnsresponder) is needed to be installed to provide local LAN DNS resolution.

In my case, i found the error "_Temporary failure in name resolution_" when I tried to resolve a machine of my LAN from Ubuntu.

```
yvoictra@zoar:~$ ping erie.local  
ping: erie.local: Temporary failure in name resolution
```

To solve this issue, there is no need to install a DNS server in the LAN. We can use the **mDNS** (Multicast Domain Name System) protocol. This protocol is used to resolve host names in a small network (LAN). The **mDNS** service can be contacted using UDP queries over port 5353. The mDNS protocol is published as RFC6762 and implemented by the **Apple Bonjour** and **avahi-daemon** services.

```
$ sudo apt-get install libnss-mdns
```

There is a specific search order order according to which it is performed. This order is set in the `/etc/nsswitch.conf` configuration file.

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

In this file, what we are interested in the line of "_hosts_". The column _files_ means the use of the `/etc/hosts` file, and the _dns_ means use of the Domain Name Service. If “_files_” are located before “_dns_”, this means that the system will first try to find the domain in `/etc/hosts`, and only then by DNS. This is default configuration.

Hostnames are stored in `/etc/hostname`, the system first looks there and if is is not found there, looks the file `/etc/hosts`.

After installing **libnss-mdns**, the line in `/etc/nsswitch.conf` should be like this:

```
hosts:         files mdns4_minimal [NOTFOUND=return] dns mdns4
```

So, now, before using the DNS server, will try to resolv `.local` domains.

After this, now I can resolv my LAN machines:

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

And that's all.
