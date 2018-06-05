---
layout: post
title: Sistemas empotrados I
author: Juanma Gomez  < jmgomez@iaa.es >
categories: Teoria Embebidos RaspberryPi
---

## Introducción
Un **sistema embebido** es una combinación de hardware y software diseñado para un tipo de _aplicación especifica_, cuyo software por lo general enfrenta a una tarea de _tiempo real_. Al tratarse de sistemas de proposito especifico, en la mayoria de las ocasiones, todos los componentes se encuentran incluidos en la placa base y no suelen permitir ampliaciones de hardware. 

![Image Ejemplos de sistemas empotrados, lavadoras, microondas, controles de acceso, televisiones](images/Embedded-System-and-Its-Real-Time-Applications-Image-3.jpg)

Por lo general, un sistema embebido incluye un pequeño procesador con una memoria acorde al mismo. La comunicacion es un aspecto fundamental de los mismos, suelen incluir puertos de comunicaciones que soportan los protocolos mas comunes, 1Wire, I2C, SPI, CAN, UART. Al igual, que las comunicaciones se suelen incluir modulos de control, generalmente PWM y Timers para manejar actuadores (motores, reles, leds, etc).

Puesto que se suelen fabricar miles o cientos de miles el costo es un factor de gran importarcia.

Hasta no hace mucho, no era habitual, que los fabricantes dieran un gran soporte. El empleo de arquitecturas exoticas, alejaba a estos sistemas de los metodos estandars de desarrollo. De echo, no es extraño que el software de los sistemas empotrados sea programado en Ensamblador. Sin embargo, en la actualidad los fabricantes de procesadores tratan de aproximarse lo maximo posible al estandard, creando forks de GGC o LLVM y para proporcionar una toolchain decente.

En resumen, podemos decir que entre las principales caracteristicas de los sistema empotrados podemos destacar:
* Diseñados a medida.
* Costes muy ajustados.
* Recursos limitados.
 * Cantidad de memoria.
 * Potencia de cálculo.
 * Perifericos disponibles.
 * Puertos de E/S.

## Tendencias en los sistemas empotrados
El incremento en la capacidad de integracion en la fabricacion de Circuitos Integrados, origino un movimiento de los fabricantes hacia la inclusion de mas componentes dentro del mismo circuitos integrado. De esta forma se consegue reducir costes y construir sistemas mas reducidos.

Este movimiento se ha llevado al extremo, ahora practicamente todo el sistema esta integrado dentro del mismo chip. Dentro del mismo chip se incluye el microprocesador, la memoria, los controladores de las interfaces, timers y pwms conformando un *system on chip* (SoC).

Dependiendo de la tirada es posible que el costo de fabricar un SoC no sea abarcable y entonces se suele recurrir a System in Package (SIP). En la que varias chips comparten encapsulado.

![Image of ARM System-on-chip Block Diagram]({{ site.baseurl }}/images/500px-ARMSoCBlockDiagram.svg.png)

La mayoría de SoC son desarrollados a partir de módulos de hardware básicos previamente probados para la construcción de diversos elementos más complejos junto con los controladores de software que proporcionan las instrucciones para su manejo. Estos elementos constitutivos suelen estar interconectados mediante el empleo de buses.

## Raspberry Pi

![Raspberry Pi3 Board]({{ site.baseurl }}/images/board_rpi3.jpg)


Raspberry Pi es un pequeño computador del tamañano de una tarjeta de crédito, el cual podemos conectar fácilmente a una televisión vía HDMI. Además, podemos utilizarla, con un teclado y un ratón. Tiene conexión a Internet y unos pines GPIO (General Purpose Input/Output), para que podamos interactuar con nuestra placa con sensores, botones, o lo que queramos. 

![Raspberry pi 3 BlockDiagram Curso pag 22](rpi3_blk_diagram.jpg)

Los sistemas Raspberry Pi 3 estan basados en el SOC BCM2837. Este SoC del fabricante Broadcom incluye una CPU con juego de instrucciones de 64bit de la familia ARMv8. Se trata de un procesador es Quad Core, o sea, de cuatro núcleos y de tipo Cortex-A53 con una velocidad de 1.2GHz, dispone de 32kB de memoria caché de nivel 1 y 512kB de caché de nivel 2. Por otro lado, el SoC incluye una GPU con dual core VideoCore IV a 400MHz y que soporta OpenGL ES 2.0.

El ARM Cortex-A53 es un procesador de altas prestaciones y alta eficiciencia energetica. Permite dos modos de ejecucion, AArch32 y AArch64, con lo que puede ejecutar tanto aplicaciones de 32 como de 64 bits.
[Ampliar Cortex-A53](https://developer.arm.com/products/processors/cortex-a/cortex-a53)


### Instalar Raspbian
El sistema Raspberry Pi 3, incluye una interfaz microSD desde la cual el sistema es capaz de arrancar el Sistema Operativo. Muchos de los sistema empotrados (de cierta potencia), disponibles en el mercado estan soportados por el SO **Linux**. 

La fundación Raspberry nos proporciona una distribucion del SO Linux precompilada y lista para ser instalada en nuestra Raspberry. Nos proporcionan un fichero de imagen, que debemos descargar y grabar en una tarjeta microSD. Esta tarjeta micro SD una vez insertada en el zocalo para tarjetas micro SD, __J9__, permitira arrancar nuestro Raspbian.

A continuacion vamos a poner en practica esto. Necesitaremos el siguiente material:
* __Tarjeta micro SD__ de al menos 4 GB.
* __Herramientas descompresion__ como PeaZIP, 7Zip.
* __Herramientas grabacion micro SD__ como Image Write Tool, Rufus o el clasico dd.
* __Lector de tarjetas micro SD__ y si es necesario el adaptador de micro SD a SD.

En primer lugar vamos a descargar la imagen de Raspbian de la web de raspberry y descomprimirla:

{% highlight bash %}
`~]$ wget -O rasbian_lite_latest.zip`

`~]$ unzip raspbian_lite_latest.zip`
{% endhighlight %}  

Insertamos nuestra tarjeta micro SD en el lector y mostramos los dispositivos de bloques del sistema para localizar nuestra micro SD.

`~]$ lsblk`

# Objetivos

* Manejar  herramientas de desarrollo para construir sistemas embebidos.
* Configurar un sistema embebido basado en micropocesador.



>“The most important factor for me is that the device must be supported in upstream Linux (preferably stable, but mainline will do) and U-Boot”
>Juan M. Gómez

> “Dive into the hardware from a linux and you will have the key to to rule them all”
> Juan P. Cobos


Next : Instalación del sistema operativo.

[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/


