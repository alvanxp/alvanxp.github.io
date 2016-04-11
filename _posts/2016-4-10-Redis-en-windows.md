---
tags:
  - redis
layout: post
title: 'Redis en Windows'
category: Cache
comments: true
---

Alguna vez necesitaste instalar redis en windows? En este blog te mostrare como instalar una vm de Ubuntu con redis (400 Mb +) usando un gestor de entornos (Vagrant) 

### Herramientas usadas:
- **[Chocolatey:](https://chocolatey.org/)** Gestor de packetes para windows
- **[Vagrant:](https://www.vagrantup.com/)**  Software para crear y configurar entornos de desarrollo virtuales 
- **VirtualBox:** Visor de maquinas virtuales

### Prerequisitos

- Tener instalado Git

## Instalacion

1. **Instalación de Chocolatey:**
Abrir cmd en modo admin y correr el siguientes lineas

```dosbatch
c:\> @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

2. **Instalación de Vagrant**
En la consola cmd escribir el siguiente  comando:

```dosbatch	
choco install vagrant
```

<img src="{{ site.url }}/assets/content/redis-vagrant/vagrant-install.png" alt="vagrant">

3. **Instalacion de Virtual Box**
Escribir el siguiente comando en la consola cmd:

```dosbatch
choco install virtualbox
```	

>Ahora se puede ver en el menu inicio virtualbox recientemente instalado:

4. Crear un directorio (c:\vagrant)

-	Nos situamos en el directorio : Cd c:\vagrant
	
-	Ahora descargamos una VM con ubuntu preconfigurada, ejecute el siguiente comando en la consola:

```dosbatch
vagrant init hashicorp/precise32
```	

## Configuración 

Ahora descargaremos la VM y iniciaremos la configuración:

Escribimos el comando  para iniciarla:

```dosbatch
vagrant up
```
Ahora entraremos remotamente  usando SSH:

```dosbatch
vagrant ssh
```	

Actualizar los packetes de ubuntu:

```sh
$ sudo apt-get update
```	
Instalacion de Redis Server

```sh
$ sudo apt-get install redis-server
```		

## Configuración de Redis Server

Abrir el archivo de configuracion de Redis con el siguiente comando:

```sh	
$ sudo nano /etc/redis/redis.conf
```	
- Para hacer accesible desde fuera necesita dejar comentada la línea referente al bind de la siguiente manera:

```sh
    #bind 127.0.0.1
```		
- Establecer el siguiente valor :

```sh	
	tcp-keepalive 60
```			
**Ctrl + O** para Guardar y **Ctrl + x** para salir del editor

Reiniciar redis con el siguiente query:

```sh
$ sudo service redis-server restart
```

Test Redis:

Entrar al cliente redis:

```sh	
$ redis-cli
```

Agregar un item:

```sh	
set name "Alvaro Carpio"
```

También podemos instalar una herramienta visual para tener un mayor manejos de los datos , **Redis Desktop Manager**

Para instalar correr el siguiente comando en una consola cmd dentro de windows:

```sh
$ choco install redis-desktop-manager
```	
Luego de instalado, abrir Redis Desktop Manager y agregar una nueva conexión de la siguiente manera:


	
Ahora podemos ver los datos ingresados previamente  en la consola: 


	



