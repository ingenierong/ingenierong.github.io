---
layout: post
title: Sistemas Empotrados II
---

#Instalación Sistema Operativo Raspbian (Linux)

Una vez que tengamos nuestra _Raspberry Pi 3_, es hora de echarla a andar. Existe una distribución linux, especifica para nuestra Raspberry, [**Raspbian**][raspbian_web].  

Raspbian es el sistema operativo oficial de la Fundación Raspberry Pi. Raspbian incluye por defecto, aplicaciones para educacion, programacion y uso general. Entre ellas, podemos encontrar Python, Scratch, Sonic Pi, Java, Mathematica y algunos otros.

La imagen de Raspbian esta contenida en un fichero ZIP de aproximadamente 4 GB, lo que significa que necesitaremos un tarjeta microSD de mas de 4 GB para poder grabarlo.

Para descargar la imagen o bien accedemos a la web de [Raspbian][raspbian_web] y descargamos la imagen o bien la descargamos empleando el comando `wget https://downloads.raspberrypi.org/raspbian_latest`.

Esta imagen que hemos descargado esta comprimida con ZIP, por lo que tenemos que descomprimirla para poder grabarla en nuestra SD `unzip raspbian_latest.zip`.

Ahora, ya tenemos acceso a los datos de la imagen. Una imagen es un fichero con extension `.img` que almacena los datos binarios de un fichero de bloques. Ahora que sabemos que es, vamos a estudiar que contiene nuestra imagen de _Raspbian_. En nuesta shell preferida, vamos a listar la [tabla de particiones](https://es.wikipedia.org/wiki/Tabla_de_particiones):

```shell
~]$ fdisk -l $(pwd)/2017-03-02-raspbian-jessie.img

Disco /mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img: 4,1 GiB, 4393533440 bytes, 8581120 sectores
Unidades: sectores de 1 * 512 = 512 bytes
*Tamaño de sector* (lógico/físico): 512 bytes / 512 bytes
Tamaño de E/S (mínimo/óptimo): 512 bytes / 512 bytes
Tipo de etiqueta de disco: dos
Identificador del disco: 0x432b3940

Disposit.                                                    Inicio Comienzo   Final Sectores Tamaño Id Tipo
/mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img1            8192  137215   129024    63M  c W95 FA
/mnt/Datos/Workspace/rpi/Iso/2017-03-02-raspbian-jessie.img2          137216 8581119  8443904     4G 83 Linux
```
Observamos que nuestra imagen tiene 2 particiones: 
1. 2017-03-02-raspbian-jessie.img1 Esta partición es la de arranque
2. 2017-03-02-raspbian-jessie.img2 Esta partición es la de root.

La partion de arranque debe ser obligatoriamente de tipo FAT.
En cuanto a la partición de rot, almacena el sistema de archivos de nuestra distribución linux. En ella se encuentran las aplicaciones de usuario, las librerias y los drivers para controlar los dispositivos de nuestro sistema.

Vamos a echarles un vistazo. Vamos a montar nuestra partición, de root. Para ello calculamos el offset donde se encuentra en el fichero `137216*512 Bytes/sector=70254592`.

```shell
~]$ sudo mkdir jessie
~]$ sudo mount -o loop,offset=70254592 2017-03-02-raspbian-jessie.img jessie
~]$ sudo mkdir -p jessie/boot
~]$ sudo mount -o loop,offset=41943042017-03-02-raspbian-jessie.img jessie/boot
```
Ahora el sistema de archivos de nuestra imagen raspbian es accesible para nosotros y vamos a cambiar algunas configuración segun nos interesen.
En primer lugar editaremos el fichero dhcpd.conf, podemos fijar la IP de nuestro sistema, de forma que al arrancar tome una IP estatica.

```shell
~]$ sudo nano jessie/etc/dhcpcd.conf
interface eth0
static ip_address=192.168.1.139/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8
```

A partir de 2016, las imágenes de Raspbian, el servicio ssh viene por defecto
desactivado. Dadas las limitaciones de material disponible, para poder trabajar con
nuestro sistema empotrado vamos a activar el servicio ssh. La documentación indica que debemos crear un fichero llamado ssh en la partición boot.

```shell
~]$ touch jessie/boot/ssh
```

Finalmente, activaremos el uso de la consola UART para poder acceder directamente a nuestro sistema en caso de que no funcione el acceso a traves de la red. 

```shell
~]$ sudo nano jessie/boot/config.txt
# Add enable_uart=1 to the file config.txt
```

UART transmit and receive pins are on GPIO 14 and GPIO 15 respectively, which are pins 8 and 10 on the GPIO header.

```shell
~]$ sudo umount jessie/boot
~]$ sudo umount jessie
```

## Grabación de la tarjeta microSD
Insertamos nuestra tarjeta microSD en nuestro Lector/Grabador de Tarjeta, y buscamos en nuestro sistema el dispositivo que le ha sido asignado.


```shell
~]$ su -
~]$ mount 
~]$ umount /dev/sdc*
~]$ dd if=2017-03-02-raspbian-jessie.img | pv -tpreb | dd of=/dev/sdc bs=128M
~]$ sync
```

Ahora insertamos la microSD en la Raspbery pi 3 y la encendemos. A cabo de unos segundos, estara lista. Si hacemos ssh a nuestra pi ```~]$ ѕѕh pi@[rasberrypi_ip_address]``` tendremos acceso a la misma.



[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/




