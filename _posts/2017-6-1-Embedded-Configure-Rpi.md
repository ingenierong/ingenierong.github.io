---
layout: post
title: Sistemas Empotrados II
---

##Configurar nuestra Raspberry Pi 3

*Raspi-config* es una herramienta de configuración grafica, basada en n-curses. Esta herramienta se puede ejecutar en una shell, por lo que podremos lanzarla desde nuestra consola SSH. 

```shell
#sudo raspi-config
```

Su aspecto es algo asi:

![Vista de Raspi-config](https://ingenierong.github.io/images/raspi-config_mainMenu.png)

Para movernos por los distintos items y submenus, empleamos las fechas arriba y abajo, y para entrar en un submenu pulsamos intro cuando estemos sobre él.


Entre los menus disponibles tenemos:
* Change User Password, cambia el password del usuario.
* Hostname, cambia el nombre de Host del dispositivo.
* Localisation Options, para configurar opcionesy adecuarlas a nuestro idioma. Languaje de los menus, idioma del teclado, etc.
* Interface option, permite activar y configurar las distintas interfaces disponibles en el sistema.
* Advanced options,
* Update
* About...




[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/




