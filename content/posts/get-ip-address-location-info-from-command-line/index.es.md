---
title: 'Obtener la localización de una dirección IP desde la línea de comandos'
date: Sat, 05 Sep 2020 09:39:33 +0000
draft: false
tags: ['Dirección', 'IP', 'Linux', 'Ubuntu', 'localización']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/get-ip-address-location-info-from-command-line']
cover:
    image: "/img/ipinfo.io.webp"
    alt: "IPInfo.io Home"
    caption: "IPInfo.io Home"
---

**La línea de comandos de Linux es una gran herramienta**. Hoy me gustaría compartir un método para obtener la informción geográfica de una IP con un comando, utilizando cURL y la herramienta de [ipinfo.io](https://ipinfo.io).

Es tan sencillo como usar este comando:

    $ curl ipinfo.io/<IP Address>

Aquí tienes un ejemplo:

![Curl ipinfo](./images/curl_ipinfo.webp)

Obtendrás estos parámetros:

*   IP
*   Ciudad
*   Región
*   País
*   Loc (Coordenadas)
*   Org
*   Código Postal
*   Zona Horaria

Y esto es todo. Si quieres tener más información sobre una dirección IP, podría visitar la web de [ipinfo.io](https://ipinfo.io), y obtendrás más información y herramientas.
