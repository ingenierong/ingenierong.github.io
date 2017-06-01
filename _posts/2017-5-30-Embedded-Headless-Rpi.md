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




[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/




