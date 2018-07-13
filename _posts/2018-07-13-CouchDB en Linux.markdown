---
layout: post
title: Instalación de CouchDB en Linux
date: 2018-07-13 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: js-1.png # Add image post (optional)
tags: [Js, Conference] # add tag
---

La instalación de CouchDB 2.0.0 en un equipo con sistema operativo Mac OS X, se puede realizar de tres formas:
* Instalación de CouchDB como una aplicación nativa
* Instalación de CouchDB con Homebrew (Todavía en construcción)
* Instalación desde el código fuente

El siguiente procedimiento describe la instalación CouchDB 2.0.0 desde el código fuente, en un equipo con sistema operativo Ubuntu 16.04.

## Instalación de dependencias

Se debe tener instalado las siguientes dependencias.
* build-essential
* pkg-config
* erlang
* libicu-dev
* libmozjs185-dev
* libcurl4-openssl-dev

Utilice el siguiente comando para realizar la instalación de las dependencias.

```bash
$ sudo apt-get --no-install-recommends -y install \
    build-essential pkg-config erlang \
    libicu-dev libmozjs185-dev libcurl4-openssl-dev
```

## Descargar código fuente de CouchDB
Una vez que se han instalado las dependencias necesarias, el siguiente paso es descargar el [código fuente de CouchDB](http://couchdb.apache.org/#download).

Descomprimir en algún directorio el archivo descargado (.tar.gz), que contiene el código fuente de CouchDB. Para descomprimir por línea de comandos, utilice:

## Instalación
Para empezar con el proceso de instalación, se debe acceder a la carpeta descomprimida desde un terminal y ejecutar el comando. 

```bash
$ ./configure
```

Si se ejecuta correctamente se mostrará el siguiente mensaje. 

```bash
You have configured Apache CouchDB, time to relax.
Luego ejecutar el siguiente comando.
```

Para compilar CouchDB debes ejecutar:

```bash
$ make release
```

Si se ejecuta correctamente, se debería mostrar el siguiente mensaje.

```bash
$ ... done
You can now copy the rel/couchdb directory anywhere on your system.
Start CouchDB with ./bin/couchdb from within that directory.
```


## Registro de usuario y seguridad
En este paso se debe crear un usuario especial para administrar CouchDB. En Ubuntu se puede crear un usuario utilizando la siguiente línea de comandos.

```bash
$ adduser --system \
        --shell /bin/bash \
        --group --gecos \
        "couchdbadmin" couchdb
```

En Ubuntu cuando se añade un nuevo usuario no se crea automáticamente un directorio principal para ese usuario, por ello se debe crear una carpeta llamada CouchDB en /home/CouchDB, y es allí donde se debe copiar la liberación de CouchDB construida.


Para copiar la liberación de CouchDB construida al directorio del nuevo usuario ejecute:

```bash
$ cp -R /path/to/CouchDB/rel/CouchDB /home/CouchDB
```

Cambie la propiedad de los directorios CouchDB ejecutando:

```bash
$ chown -R CouchDB:CouchDB /home/CouchDB
```

Cambie los permisos de los directorios CouchDB ejecutando:
```bash
$ find /home/CouchDB -type d -exec chmod 777 {} \;
```

Para cambiar los permisos de los archivos .ini

```bash
$ chmod 0644 /home/CouchDB/etc/*
```
