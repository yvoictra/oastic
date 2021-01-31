---
title: 'Listar paquetes instalados en Ubuntu'
date: Mon, 30 Jul 2018 22:55:23 +0000
draft: false
tags: ['Linux', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/list-installed-packages-in-ubuntu']
---

En algunas situaciones necesitamos saber qué paquetes tenemos instalados en nuestro sistema Debian o Ubuntu. En este caso, utilizamos la herramienta [dpkg](https://en.wikipedia.org/wiki/Dpkg), que nos dará la información que necesitamos.

El siguiente comando nos dara el estado actual de paquetes instalados con sus diferentes estados:
```
dpkg --get-selections
```

Los estados que podemos tener son los siguientes:

*   **install**: The package is selected for installation.
*   **hold**: A package marked to be on hold is not handled by dpkg, unless forced to do that with option --force-hold.
*   **deinstall**: The package is selected for deinstallation (i.e. we want to remove all files, except configuration files).
*   **purge**: The package is selected to be purged (i.e. we want to remove everything from system directories, even configuration files).

Si queremos filtrar los paquetes, podemos combinar la herramienta **dpkg** con la herramienta **grep**. Aquí tienes un ejemplo de cómo filtrar los paquetes relacionados con _nginx_:
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
Además, podría exportar el resultado con un comando a un fichero:
```
$ dpkg --get-selections > ~/packages.txt
