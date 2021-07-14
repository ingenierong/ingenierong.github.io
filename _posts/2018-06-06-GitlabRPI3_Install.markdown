---
layout: post
title: Servidor Git con Gilab
author: Juanma Gomez  < jmgomez@iaa.es >
categories: Project Manager Redmine Git RaspberryPi
bibliografia:  https://about.gitlab.com/installation/#raspberry-pi-2 https://pimylifeup.com/raspberry-pi-gitlab/

---

## Introducción
For those who don’t know what is GitHub, GitHub is a web service based on the software Git (which is a versioning software written by Linus Torvald, creator of Linux). Git allows you to store the history of your software code base and easily control versioning. GitHub host all those Git repositories and also provides many other features like bug tracking, milestone creation and also the creation of Wiki for your project.



##Instalación

En primer lugar instalamos el software necesario para nuestro  servidor de git.
{% highlight bash %}
sudo apt-get install curl openssh-server ca-certificates postfix apt-transport-https
{% endhighligh %}

La instalación de postfix puede configurar el paquete para trabajar como un sitio internet site, para poder enviar notificaciones via email desde nuestro servidor.

![Menu de instalacion Postfix Configuracion, tipo de sitio internet site] (rpi3_gitlab_install_001.png)

En segundo lugar, nos pide que le indiquemos el nombre de dominio desde el que se enviaran las notificaciones via email. Este email se usar en las notificaciones, el emisor del correo sera @loqueleindiquemos.com

Ya estamos listos para instalar nuestro software, vamos descargamos la clave publica GPG de GITLab de forma que podamos acualizar nuestro paquete gitlab-ce de forma sencilla empleando nuestro gestor de paquetes.

{% highlight bash %}
curl https://packages.gitlab.com/gpg.key | sudo apt-key add -
{% endhighlight %}

Realizamos la instalación de los paquetes necesarios para el funcionamiento del servidor de gitlab. Tenemos que descargar el script de instalación y lanzarlo.

{% highlight bash %} 
sudo curl -sS https://packages.gitlab.com/install/repositories/gitlab/raspberry-pi2/script.deb.sh | sudo bash
{% endhighlight %}

NOTA:
Hemos comprobado que la version de raspbian es para strech y tenemos instalada jessie, asi que editamos manualmente y cambiamos de strecht a jessie en el fichero gitlab_raspbery-pi2.
sudo nano /etc/apt/sources.list.d/gitlab_raspberry-pi2.list 
sudo apt-get update
sudo apt-cache search gitlab-ce
gitlab-ce - GitLab Community Edition (including NGINX, Postgres, Redis

Finalmente, instalamos el paquete de gitlab-ce.
{% highlight bash %} 
sudo apt-get install gitlab-ce
{% endhighlight %}

![Instaalcion con exito. Muestra un Banner de gitlab en ASCII ] (rpi3_gitlab_install_002.png)

## Configuración
The final command that needs to be run to finalize the installation of GITLab is the one shown below, this command configures and sets up all the settings for GITLab and installs all the required databases.

$ sudo gitlab-ctl reconfigure

Aqui morimos!!
