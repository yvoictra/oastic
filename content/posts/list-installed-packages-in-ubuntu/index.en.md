---
title: 'List installed packages in Ubuntu'
date: Mon, 30 Jul 2018 22:55:23 +0000
draft: false
tags: ['Linux', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/list-installed-packages-in-ubuntu']
---

In some situations we need to know which packages we have installed in a Debian or Ubuntu system. In that case, we can use the tool [dpkg](https://en.wikipedia.org/wiki/Dpkg), which will give us the information we need. 

Next command will give us the current packages installed with different states:
```
dpkg --get-selections
```

The states we can have are:

*   **install**: The package is selected for installation.
*   **hold**: A package marked to be on hold is not handled by dpkg, unless forced to do that with option --force-hold.
*   **deinstall**: The package is selected for deinstallation (i.e. we want to remove all files, except configuration files).
*   **purge**: The package is selected to be purged (i.e. we want to remove everything from system directories, even configuration files).

If we want to filter packages, we can combine **dpkg** tool with **grep** tool. Here an example to filter the packages related with _nginx_:
```
$ dpkg --get-selections | grep nginx
libnginx-mod-http-geoip                         install
libnginx-mod-http-image-filter                  install
libnginx-mod-http-lua                           install
libnginx-mod-http-ndk                           install
libnginx-mod-http-xslt-filter                   install
libnginx-mod-mail                               install
libnginx-mod-stream                             install
nginx                                           install
nginx-common                                    install
nginx-core                                      install
python3-certbot-nginx                           install
```
Also, you could export the result of the command to a file:
```
$ dpkg --get-selections > ~/packages.txt
```
