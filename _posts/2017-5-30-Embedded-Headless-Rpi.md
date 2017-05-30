---
layout: post
title: Sistemas Empotrados II
---

##Headless Raspberry Pi 3 (Linux)

Para realizar esta practica es necesario que tengamos nuestra _Raspberry Pi 3_ encendida, conectada una red local y con una imagen de [**Raspbian**][raspbian_web] ejecutandose. Es necesario, que la Red local cuente con un [servidor DHCP](https://es.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol), que puede ser por ejemplo el mismo router que tenemos en casa y que usamos para conectarnos a Internet.  

En nuestra practica anterior, grabamos la imagen de Raspbian y creamos un fichero con nombre ssh, para que al arrancar Raspbian activara el [servicio SSH](https://es.wikipedia.org/wiki/Secure_Shell).

La imagen de Raspbian incluye por defecto al usuario `pi`, cuyo password es `rapsberry`. 

En primer lugar, debemos localizar nuestra Raspberry Pi 3 dentro nuestra red local. En nuestro, caso no sera necesario ya que cada una de las Rasbperry Pi tienen fijada una IP estatica desde nuestro servidor DHCP.En otro caso empleariamos cualquiera de los métodos para enumerar nuestra red, desde acceder a la información del servidor DHCP de nuestro router y ver la IP que ha asignado a nuestra Raspberry, hasta analizar todas las IPs que esten en nuestro rango empleando nmap.

```shell
~]$ nmap -sP 192.168.10.1/24
```

##Clientes SSH
Existen varias opciones a la hora de conectarnos a un dispositivo empleando el servicio SSH. En el caso de plataformas windows, es necesario descargar el programa [Putty] (https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). Para el caso de sistemas Linux y OS X emplearemos el cliente que trae por defecto.

La conexion se realiza mediante el comando  `ssh pi@IP_RASPBERRY`, esto nos proporciona una shell Linux en nuestro sistema empotrado. Al conectar, nos pedira la contraseña del usuario `pi` que es `raspberry`.

```shell
#]~ ssh 
usage: ssh [-1246AaCfgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
           [-D [bind_address:]port] [-E log_file] [-e escape_char]
           [-F configfile] [-I pkcs11] [-i identity_file]
           [-L [bind_address:]port:host:hostport] [-l login_name] [-m mac_spec]
           [-O ctl_cmd] [-o option] [-p port]
           [-Q cipher | cipher-auth | mac | kex | key]
           [-R [bind_address:]port:host:hostport] [-S ctl_path] [-W host:port]
           [-w local_tun[:remote_tun]] [user@]hostname [command]
```
Este es el mensaje de uso de ssh. A nosotros por ahora solo nos interesa la parte final, `ssh user@hotsname`. Si observamos el comando que hemos usado para conectarnos, pi seria el usuario y IP_RASPBERRY seria el hosname del dispositivo.

```shell
#]~ ssh  pi@192.168.10.149

```


Una vez conectados, vamos a actualizar nuestro sistema, firmware, software y paquetes, empleando el gestor de paquetes de raspbian.

```shell
# sudo apt-get update
# sudo apt-get upgrade -y
# sudo rpi-update
# sudo reboot


```

(https://es.wikipedia.org/wiki/Tabla_de_particiones):

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
En cuanto a la partición de root, almacena el sistema de archivos de nuestra distribución linux. En ella se encuentran las aplicaciones de usuario, las librerias y los drivers para controlar los dispositivos de nuestro sistema.

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




