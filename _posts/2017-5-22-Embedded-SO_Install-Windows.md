---
layout: post
title: Sistemas Empotrados II
---

##Instalación Sistema Operativo Raspbian (Windows)

Una vez que tengamos nuestra _Raspberry Pi 3_, es hora de echarla a andar. Existe una distribución linux, especifica para nuestra Raspberry, [**Raspbian**][raspbian_web].  

Raspbian es el sistema operativo oficial de la Fundación Raspberry Pi. Raspbian incluye por defecto, aplicaciones para educacion, programacion y uso general. Entre ellas, podemos encontrar Python, Scratch, Sonic Pi, Java, Mathematica y algunos otros.

La imagen de Raspbian esta contenida en un fichero ZIP de aproximadamente 4 GB, lo que significa que necesitaremos un tarjeta microSD de mas de 4 GB para poder grabarlo.

Para descargar la imagen o bien accedemos a la web de [Raspbian][raspbian_web] y descargamos la imagen o bien la descargamos empleando el comando `wget https://downloads.raspberrypi.org/raspbian_latest`.

Esta imagen que hemos descargado esta comprimida con ZIP, para ello empleamos nuestra herramienta preferida de descompresion. Hacemos click con el boton derecho sobre el dichero descargado y seleccionamos `Extraer Aqui`.

Ahora, ya tenemos acceso a los datos de la imagen. Una imagen es un fichero con extension `.img` que almacena los datos binarios de un fichero de bloques. Ahora que sabemos que es, vamos a estudiar que contiene nuestra imagen de _Raspbian_.

Para grabar la imagen en nuestra tarjeta microSD tenemos que emplear un software, W32DiskImage o alternativamente se puede emplear Etcher SD. Lo descargamos y ejecutamos:

```
Win32DiskImager
https://sourceforge.net/projects/win32diskimager/files/latest/download

Etcher SD for Windows 10
https://resin-production-downloads.s3.amazonaws.com/etcher/1.0.0/Etcher-1.0.0-win32-x64.zip

Etcher SD for OS X
https://resin-production-downloads.s3.amazonaws.com/etcher/1.0.0/Etcher-1.0.0-darwin-x64.dmg

```

Una vez grabada nuestra microSD tendremos disponible una imagen lista para ejecutar en nuestra Raspberry Pi 3.

La imagen descargada incluye 2 particiones:
1. 2017-03-02-raspbian-jessie.img1 Esta partición es la de arranque
2. 2017-03-02-raspbian-jessie.img2 Esta partición es la de root.

La partion de arranque debe ser obligatoriamente de tipo FAT. Cuando insertamos nuestra microSD en el PC Windows, esta es la única particion que se reconoce.

En cuanto a la partición de root, almacena el sistema de archivos de nuestra distribución linux. En ella se encuentran las aplicaciones de usuario, las librerias y los drivers para controlar los dispositivos de nuestro sistema.

A partir de 2016, las imágenes de Raspbian, el servicio ssh viene por defecto desactivado. Dadas las limitaciones de material disponible, para poder trabajar con nuestro sistema empotrado vamos a activar el servicio ssh. La documentación indica que debemos crear un fichero llamado ssh en la partición boot.

```
Entramos con el Explorador de ficheros, en la microSD y Boton derecho y en el submenu Nuevo fichero de texto. Le ponemos el nombre ssh. Precaución el fichero tendra extension .txt por defecto, debemos cambiarla.
```

Finalmente, activaremos el uso de la consola UART para poder acceder directamente a nuestro sistema en caso de que no funcione el acceso a traves de la red. 

```
Doble clock en config.txt y añadimos al final:
enable_uart=1

```

UART transmit and receive pins are on GPIO 14 and GPIO 15 respectively, which are pins 8 and 10 on the GPIO header.


Ahora insertamos la microSD en la Raspbery pi 3 y la encendemos. A cabo de unos segundos, estara lista. Si hacemos ssh a nuestra pi ```~]$ ѕѕh pi@[rasberrypi_ip_address]``` tendremos acceso a la misma.



[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/


Next: Conectar con nuestra Raspberry Pi 3


