---
title: 'Solucionar el problema "client intended to send too large body" en Nginx'
date: Tue, 01 Sep 2020 13:55:38 +0000
draft: false
tags: ['error', 'Linux', 'Nginx', 'servidor', 'Ubuntu', 'subir', 'web', 'wordpress']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/solve-issue-client-intended-to-send-too-large-body-in-nginx']
---

He encontrado un error en un servidor web utilizando **Nginx** mientras trataba de subir un fichero usando wordpress.

En el log de errores de Nginx he visto el error "Client intended to send too large body" en esta entrada:

```
$ tail -f /var/log/nginx/*error*.log
2020/09/01 14:31:04 [error] 884#884: *126565 client intended to send too large body: 1195619 bytes, client: 55.173.250.46, server: test.com, request: "POST /wp-json/wp/v2/media?_locale=user HTTP/2.0", host: "test.com", referrer: "https://test.com/wp-admin/post.php?post=2460&action=edit"
```

Esto es una limitación definida en el servidor web de Nginx, así que he cambiado la configuración del servidor:

    $ sudo vi /etc/nginx/nginx.conf

Entonces tienes que añadir o modificar la siguiente configuración en la sección `http{}`.

    client_max_body_size 250M;

El siguiente paso es comprobar que la configuración de Nginx es correcta:

```
$ nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Y finalmente, reinicia el servidor:

```
$ sudo systemctl reload nginx
$
```

Y ya estaria listo. Ahora no deberias de volver a este error mientras subas ficheros inferiores a 250Mb.
