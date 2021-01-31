---
title: 'Cómo cambiar el idioma y la configuración local en Ubuntu'
date: Wed, 01 Apr 2020 19:32:37 +0000
draft: false
tags: ['teclado', 'idioma', 'Linux', 'locales', 'timezone', 'Ubuntu']
categories: ['Linux', 'Ubuntu']
aliases: ['/es/how-to-change-your-language-and-local-configuration-in-ubuntu.md']
---

Conecta vía SSH a tu máquina y ejecuta el siguiente comando

    sudo dpkg-reconfigure locales

Tras esto, veras un listado de idiomas y países. Tienes que seleccionar con _la barra espaciadora_ el idioma y el país que necesites. En mi caso, como vivo en España, he seleccionado **es\_ES.UTF-8**. Es recomendable seleccionar la versión UTF-8.

Finalmente, Ubuntu te preguntará el idioma por defecto del sistema operativo.

Tras esto, debes de configurar el idioma en el teclado con este comando:

    sudo dpkg-reconfigure keyboard-configuration

Ahora, configuraremos la zona horaria

    sudo dpkg-reconfigure tzdata

Yo he seleccionado el país (Europa) y la ciudad (Madrid) donde vivo, así que la zona horaria ha sido actualizada.

Finalmente es recomendable reiniciar el sistema para aplicar los cambios.

    sudo reboot
