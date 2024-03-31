---
layout: post
title:  "Configuración de Virtual Hosts en Apache"
date:   2023-03-06 23:07:15 -0600
tags: [Apache, Virtual hosts]
menu: /blog
post_category: Web Development
---
Cuando se trata de alojar múltiples sitios web en un solo servidor, el uso de Virtual Hosts es una solución excelente. Con esta tecnología de alojamiento, los propietarios de sitios web pueden alojar múltiples sitios en una única partición virtual dentro del servidor físico, en lugar de tener un servidor físico dedicado para cada sitio web.
<!--more-->

Cada partición virtual cuenta con su propio nombre de dominio, configuraciones y archivos de contenido, lo que permite que los sitios web se ejecuten como si estuvieran en servidores dedicados individuales. Esto significa que cada sitio web puede tener su propio conjunto de configuraciones personalizadas, como preferencias de servidor, opciones de seguridad y otros ajustes específicos, sin interferir con los demás sitios alojados en el mismo servidor físico. 


## Cómo crear un Virtual Host con Apache en Ubuntu

En este tutorial, crearemos 2 virtual hosts en un mismo servidor haciendo uso de Apache.


### 1. Actualizar repositorios

Primero, nos aseguraremos de tener actualizados nuestros repositorios y sistema operativo. Escribiremos en nuestra terminal:

```
sudo apt update
sudo apt upgrade -y
```

### 2. Instalaremos nuestro servidor web Apache.

```
sudo apt install apache2 -y
```

Reiniciaremos el servidor y validaremos su estatus.

```
sudo systemctl restart apache2
sudo systemctl status apache2
```

### 3. Crear los sitios web

Crearemos 2 directorios donde estarán hospedados nuestros sitios y cambiaremos la propiedad, para que no sea necesario usar el usuario root para modificarlos. Además, daremos permisos de lectura al directorio web de nuestro Apache.

```
sudo mkdir -p /var/www/site1/public_html
sudo mkdir -p /var/www/site2/public_html

sudo chown -R $USER:$USER /var/www/site1/public_html
sudo chown -R $USER:$USER /var/www/site2/public_html

sudo chmod -R 755 /var/www
```

Dentro de cada uno de los directorios creados, agregaremos un archivo index.html para diferenciar en cuál de ellos estamos utilizando.

```
cat >> /var/www/site1/public_html/index.html
cat >> /var/www/site2/public_html/index.html
```

En el archivo index.html de site1 escribiremos

```
Website 1
```

En el archivo index.html de site2 escribiremos

```
Website 2
```
*Otras opciones para crear el archivo son mediante los comandos touch o echo, o el editor de tu preferencia*

### 4. Añadir los hosts a la lista de DNS local

Modificaremos el archivo hosts, el cual nos permite resolver localmente consultas DNS. Esto será útil para probar la configuración de nuestros sitios una vez creados los virtual hosts.

Editaremos el archivo /etc/hosts para agregar las siguientes líneas:

```
127.0.0.1 www.site1.com
127.0.0.1 www.site2.com
```

### 5. Configurar los virtual hosts

El directorio /etc/apache2/sites-available contiene las configuraciones de virtual hosts en Apache. Si deseamos crear nuevos hosts, podemos editar ese archivo u optar por modificar una copia del archivo *000-default.conf*, el cual contiene la configuración por defecto de virtual host.

Podemos crear las copias mediante los comandos:

```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/site1.conf
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/site2.conf
```

Modificaremos los archivos de la siguiente forma:

site1.conf:

```
<VirtualHost *:80>
    ServerAdmin admin@host1.com
    ServerName site1
    ServerAlias www.site1.com
    DocumentRoot /var/www/site1/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
</VirtualHost>
```
site2.conf:

```
<VirtualHost *:80>
    ServerAdmin admin@host1.com
    ServerName site2
    ServerAlias www.site2.com
    DocumentRoot /var/www/site2/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
</VirtualHost>
```

### 6. Habilitar las configuraciones

Ahora procederemos a habilitar las configuraciones creadas mediante los comandos:

```
sudo a2ensite site1.conf
sudo a2ensite site2.conf
```

Antes de reiniciar el servidor, es recomendable validar que no haya errores que podrían dejarlo fuera de servicio aun si es momentáneamente. Utilizaremos el siguiente comando para validar la sintaxis:

```
sudo apachectl configtest
```

### 7. Reiniciar el servidor

En caso de que no haya errores de sintaxis, procederemos a reiniciar el servidor y aplicar los cambios.

```
sudo systemctl reload apache2
```

### 8. Probar la configuración

Podemos comprobar que la configuración es la correcta mediante el comando curl o accediendo a través del navegador.

```
curl www.site1.com
```

Verificaremos que el servidor nos entregará contenido diferente dependiendo de la URL solicitada.