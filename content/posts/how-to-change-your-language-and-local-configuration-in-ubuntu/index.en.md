---
title: 'How to change your language and local configuration in Ubuntu'
date: Wed, 01 Apr 2020 19:32:37 +0000
draft: false
tags: ['keyboard', 'language', 'Linux', 'locales', 'timezone', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/how-to-change-your-language-and-local-configuration-in-ubuntu.md']
---

Connect with SSH to your machine and execute next command

    sudo dpkg-reconfigure locales

After this, you will see a list of languages and countries. You have to select with _space bar_ the language and country you need. In my case, as I live in Spain, I have selected **es\_ES.UTF-8**. It is recommended to choose UTF-8 version.

Finally, Ubuntu will ask you to select the default language to use in the operating system.

After that, you should configure the language in the keyboard with this command:

    sudo dpkg-reconfigure keyboard-configuration

Now, we will configure the timezone

    sudo dpkg-reconfigure tzdata

I have select the country (Europe) and the city (Madrid) where I live, so the timezone has been updated.

Finally it is recommended to reboot the system to apply the changes.

    sudo reboot
