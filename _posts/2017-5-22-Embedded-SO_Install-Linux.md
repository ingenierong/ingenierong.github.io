---
layout: post
title: Instalación Sistema Operativo Raspbian (Linux)
---

## Introducción

Una vez que tengamos nuestra _Raspberry Pi 3_, es hora de echarla a andar. Existe una distribución linux, especifica para nuestra Raspberry, [**Raspbian**][raspbian_web].  

Raspbian es el sistema operativo oficial de la Fundación Raspberry Pi. Raspbian incluye por defecto, aplicaciones para educacion, programacion y uso general. Entre ellas, podemos encontrar Python, Scratch, Sonic Pi, Java, Mathermatica y algunos otros.

La imagen de Raspbian esta contenida en un fichero ZIP de aproximadamente 4 GB, lo que significa que necesitaremos un tarjeta microSD de mas de 4 GB para poder grabarlo.

Para descargar la imagen o bien accedemos a la web de [Raspbian][raspbian_web] y descargamos la imagen o bien la descargamos empleando el comando `wget https://downloads.raspberrypi.org/raspbian_latest`.

Esta imagen que hemos descargado esta comprimida con ZIP, por lo que tenemos que descomprimirla para poder grabarla en nuestra SD `unzip raspbian_latest.zip`.


```shell
~]$ fdisk -l $(pwd)/2017-03-02-raspbian-jessie.img

Disco /mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img: 4,1 GiB, 4393533440 bytes, 8581120 sectores
Unidades: sectores de 1 * 512 = 512 bytes
Tamaño de sector (lógico/físico): 512 bytes / 512 bytes
Tamaño de E/S (mínimo/óptimo): 512 bytes / 512 bytes
Tipo de etiqueta de disco: dos
Identificador del disco: 0x432b3940

Disposit.                                                    Inicio Comienzo   Final Sectores Tamaño Id Tipo
/mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img1            8192  137215   129024    63M  c W95 FA
/mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img2          137216 8581119  8443904     4G 83 Linux
```

## Introducción



[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/



