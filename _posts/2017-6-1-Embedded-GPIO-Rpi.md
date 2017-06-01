---
layout: post
title: Sistemas Empotrados (Part IV)
---

##Manejo de las interfaces electricas de Raspberry Pi 3

Además de las interfaces mas habituales, USB, Ethernet y HDMI, la Raspberry Pi 3 dispone de interfaces para conectarse a una amplia variedad de dispositios electronicos.
* Digital outputs: turn lights, motors, or other devices on or off
* Digital inputs: read an on or off state from a button, switch, or other sensor
* Communication with chips or modules using low-level protocols: SPI, I²C, or serial UART.

Estas conexiones se realizan empleando los pines de conexion GPIO, que estan disponibles en el conector J8.

![Conector GPIO_J8](https://ingenierong.github.io/images/Rpi3_Hw_J8.png)

Estas conexiones no son "plug and play" y deben realizarse con cuidad, para no dañar el dispositivo.  

*Las interfaces GPIO funcionan a 3.3 V y no incluyen ninguna protección de sobrevoltaje.* La idea detras de estas interfaces es permitir desarrollar a los intersados tarjetas externas que se conecten a este conector. Estas tarjetas son conocidas como *HAT*s (_Hardware Attached on Top_). Una [HAT](https://www.raspberrypi.org/blog/introducing-raspberry-pi-hats/) es Y ofrecen ampliaciones de la funcionalidad de la Raspberry Pi.


Raspberry Pi supports the special autoconfiguration system that allows automatic GPIO setup and driver setup. The automatic configuration is achieved using 2 dedicated pins (ID_SD and ID_SC) on the 40W B+ GPIO header that are reserved for an I2C EEPROM. The EEPROM holds the board manufacturer information, GPIO setup and a thing called a ‘device tree‘ fragment – basically a description of the attached hardware that allows Linux to automatically load the required drivers.


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



[elinux_LowLevelPer]: http://elinux.org/RPi_Low-level_peripherals
[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/




