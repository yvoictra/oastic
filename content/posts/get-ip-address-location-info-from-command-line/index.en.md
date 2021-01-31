---
title: 'Get IP address location info from command line'
date: Sat, 05 Sep 2020 09:39:33 +0000
draft: false
tags: ['Address', 'IP', 'Linux', 'Ubuntu', 'localization']
categories: ['Linux', 'Ubuntu']
aliases: ['/get-ip-address-location-info-from-command-line']
cover:
    image: "/img/ipinfo.io.webp"
    alt: "IPInfo.io Home"
    caption: "IPInfo.io Home"
---

**The Linux command line is a great tool**. Today I'll like to share a method to get Geographical IP information with one command, using curl and the tool of [ipinfo.io](https://ipinfo.io).

It is as easy to use this command:

    $ curl ipinfo.io/<IP Address>

Here you have an example:

![Curl ipinfo](./images/curl_ipinfo.webp)

You will have these parameters:

*   IP
*   City
*   Region
*   Country
*   Loc (Coordinates)
*   Org
*   Postal
*   Timezone

And that's all. If you want more information about an IP address, you could visit the website of [ipinfo.io](https://ipinfo.io), and you'll get some more information and tools.
