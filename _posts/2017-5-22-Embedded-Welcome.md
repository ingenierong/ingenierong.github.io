---
layout: post
title: Sistemas empotrados I
---


A lo largo de estos post, vamos a adquirir una visión general de como funcionan los _sistemas embebidos_. Entre los principales objetivos de este mini-curso, pretendemos alcanzar los siguientes objetivos:  
* Conocer las caracteristicas básuicas de los sistemas embebidos para instrumentación.
* Conocer las nuevas tendencias de desarrollo en el dominio de los _system-on-chip_ (SOC).
* Manejar  herramientas de desarrollo para construir sistemas embebidos.
* Configurar un sistema embebido basado en micropocesador.
* Conocer y manipulas los entornos de programación C y Python.
* Usar las capacidades de comunicación más habituales de un sistema embebido.
* Crear conexiones con elementos electrónicos como leds, relés, sensores, etc.
* Controlar los puertos de entrada y salida digitales de un sistema embebido.
* Controlar los puertos de entrada y salida digitales de un sistema embebido.
* Diseñar y adaptar un sistema embebido para instrumetación científica.  

Para alcanzar estos objetivos, vamos a planificar un conjunto de prácticas en las que mediante ejemplos aprenderemos a manejar los sitemas embebidos.

## Prácticas
* Conexión y configuración de un sistema empotrado Raspberry Pi 3.
* Instalación y oncfiguración de servicios básicos: red, FTP, servidor web, base datos, etc.
* Conexión de actuadores y sensores mediante los puertos digitales.
* Uso de buses de comunicación I2C, SPI y UART.

>“The most important factor for me is that the device must be supported in upstream Linux (preferably stable, but mainline will do) and U-Boot”
>Juan M. Gómez

> “Dive into the hardware from a linux and you will have the key to to rule them all”
> Juan P. Cobos

## Introducción
Un **sistema embebido** es una combinación de hardware y software diseñado para un tipo de aplicación especifica.  
Entre sus principales caracteristicas estos sistemas tienen: 
* Diseñados a medida.
* Costes muy ajustados. 
* Recursos limitados
 * Cantidad de memoria.
 * Potencia de cálculo.
 * Perifericos disponibles.
 * Puertos de E/S.

Resulta complicado acotar estrictamente donde terminan los microprocesadores y donde comienzan los sistema empotrados. Algunos ejemplos de sistemas empotrados son:

![Raspberry Pi3 Board](https://ingenierong.github.io/images/board_rpi3.jpg)


![Arduino Board](https://ingenierong.github.io/images/board_arduino.jpg)


## Instalación del sistema operativo.

[raspbian_web]: https://www.raspberrypi.org/downloads/raspbian/


