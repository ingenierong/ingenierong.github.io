---
layout: post
title: Manejo de Redmine
author: Juanma Gomez  < jmgomez@iaa.es >
categories: Project Manager Redmine Git RaspberryPi
bibliografia: 

---

## Introducción
[Redmine](http://www.redmine.org) es una herramienta para la gestión de proyectos, que con sus diversas funcionalidades permite a los usuarios de diferentes proyectos realizar el seguimiento y organización de los mismos. Además es posible optimizar su funcionamiento agregando funcionalidades. Incluye un sistema de seguimiento de incidentes con seguimiento de errores. Otras herramientas que incluye son calendario de actividades, diagramas de Gantt para la representación visual de la línea del tiempo de los proyectos, wiki, foro, visor del repositorio de control de versiones, RSS, control de flujo de trabajo basado en roles, integración con correo electrónico, entre otras opciones.

Está escrito usando el framework Ruby on Rails. Es software libre y de código abierto, disponible bajo la Licencia Pública General de GNU v2.

Ya hablamos de como instalarla en ....

## Manejo de Redmine
Redmine es una aplicación web, y por lo tanto para acceder a la misma debemos hacerlo desde nuestro navegador. Entramos en Firefox y accedemos a la direccion http://10.9.0.104/redmine


Las credenciales por defecto de Redmine son:
user: admin
password: admin

Cuando accedamos lo primero que nos exigira hacer la aplicaciones, es cambiar la contraseña de administrador.

En la parte superior de la aplicacion se encuentra el menu de navegación, que incluye varias pestañas Inicio, Mi Pagina, Proyectos, Administracion. Hacemos click en Administración...

![Menu Administración clicado, con las categorias a la vista](rpi3-redmine-intro_uso-001.png)

Dentro de este menu, se encuentran la categorias/herramientas con las que manejamos Redmine. Nuestro primer paso, es crear un Usuario para dejar de movernos por la web con la contraseña de administrado.

Hacemos click, en Usuarios.

![Menu Usuarios, dentro de Administracion. Muestra una lista de los usuarios, con una caja para filtrar la saldia, y un enlace para crear un nuevo usuario](rpi3-redmine-intro_uso-001.png)

Hacemos click sobre __Nuevo usuario__, en la parte superior derecha de la ficha de Usuarios.
