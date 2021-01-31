---
title: 'Solve issue "client intended to send too large body" in Nginx'
date: Tue, 01 Sep 2020 13:55:38 +0000
draft: false
tags: ['error', 'Linux', 'nginx', 'server', 'Ubuntu', 'upload', 'web', 'wordpress']
categories: ['Linux', 'Ubuntu']
aliases: ['/solve-issue-client-intended-to-send-too-large-body-in-nginx']
---

I have faced an issue in a web server using **Nginx** while trying to upload a file using wordpress.

In the nginx error log I saw the error "Client intended to send too large body" in this entry:

```
$ tail -f /var/log/nginx/*error*.log
2020/09/01 14:31:04 [error] 884#884: *126565 client intended to send too large body: 1195619 bytes, client: 55.173.250.46, server: test.com, request: "POST /wp-json/wp/v2/media?_locale=user HTTP/2.0", host: "test.com", referrer: "https://test.com/wp-admin/post.php?post=2460&action=edit"
```

This limitation is defined in the Nginx web server, so I have to changed the configuration of the server:

```
$ sudo vi /etc/nginx/nginx.conf
```

Then you have to add or modify the next configuration in the `http{}` section.

```
client_max_body_size 250M;
```

Next step is to check the configuration of Nginx is OK:

```
$ nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

And finally, restart the server:

```
$ sudo systemctl reload nginx
$
```

It's done. Now you shouldn't see this error while uploading files under 250Mb.
