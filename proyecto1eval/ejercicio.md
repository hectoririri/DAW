# Proyecto 1º Evaluación

## En este archivo realizaremos todas las actividades del primer proyecto de esta primera evaluación. Iremos apartado por apartado explicando y mostrando con capturas de pantalla cómo lo realizo.


### 1. Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python
Para la instalación de apache abriremos un terminal de Ubuntu *(Ctrl+T)* y actualizaremos el sistema con el siguiente comando utilizando **"apt"**. Siempre utilizaremos **"sudo"** de aquí en adelante al necesitar de permisos de administrador.
```ubuntu
$ sudo apt update ; sudo apt upgrade
```
Cuando nos pregunte "¿Desea continuar? [Y/n], escribiendo **"y"** y pulsando Intro confirmaremos la actualización de nuestro sistema. Una vez terminada la actualización, volveremos a usar el comando **"apt"** para instalar Apache2:
```ubuntu
$ sudo apt install apache2
```

[Foto de la instalación](/proyecto1eval/imagenes/apache2_instalacion.png)

Una vez terminada la instalación, podremos comprobar si se hizo correctamente ejecutando los siguientes comandos para visualizar la versión de Apache2 y el status en el que se encuentra:
```ubuntu
$ apache -v
$ sudo systemctl status apache2
```
[Foto de la comprobación de la instalación](/proyecto1eval/imagenes/apache2_comprobacion_instalacion.png)

Ahora pondremos en marcha los dos dominios que nos pide el apartado. Para ello crearemos una carpeta para cada dominio en el que, más adelante, almacenaremos el contenido que queramos mostrar en estos.
Para ello, de momento, crearemos un index.html para cada dominio indicando el nombre de este. Crearemos las carpetas con el comando **"mkdir"** en la ruta de **"/var/www"**, que es donde se aloja el contenido de cada dominio en Apache2:
```ubuntu
$ sudo mkdir /var/www/centro_intranet
$ sudo mkdir /var/www/departamentos_centro_intranet
```
En estas carpetas, utilizaremos el comando **"cat"** para crear y escribir directamente el fichero index.html que se encontrará en cada carpeta. Al terminar de escribir pulsamos Ctrl+D para salir:
```ubuntu
$ sudo cat > /var/www/centro_intranet/index.html
Soy la página de centro.intranet
$ sudo cat > /var/www/departamentos_centro_intranet/index.html
Soy la página de departamentos.centro.intranet
```
Este es el resultado final de nuestra estructura de carpetas con los index.html correspondientes para cada carpeta:
[Foto de la estructura de carpetas en /var/www/](/proyecto1eval/imagenes/apache2_estructura_carpetaspng.png)

Ahora crearemos un fichero de onfiguración para cada dominio en el que le indicaremos su ruta de carpeta, nombre de dominio, etc... Para esto, iremos a la carpeta **"/etc/apache2/sites-avaliables"**.
En esta carpeta se encuentran los ficheros de configuración para cada dominio que tengamos en nuestro Apache2. Copiaremos el que hay por defecto y lo modificaremos para cada dominio:
### Activar los módulos necesarios para ejecutar php y acceder a mysql
```ubuntu
$ cd /etc/apache2/sites-avaliables
$ sudo cp 000-default.conf centro_intranet.conf
$ sudo cp 000-default.conf departamentos_centro_intranet.conf
```

Una vez copiado, modificaremos cada fichero de configuración en respecto al dominio al que queramos hacer referencia. Primero configuraremos el de centro_intranet, por lo tanto ejecutaremos el comando **"nano"** seguido del fichero para editarlo:
### Instala y configura wordpress
```ubuntu
$ sudo nano centro_intranet.conf
```
Ahora modificaremos el fichero de la siguiente manera y haremos lo mismo para el fichero de departamentos_centro_intranet:
[Foto de configuración de centro_intranet.conf](/proyecto1eval/imagenes/apache2_centro_intranet.conf.png)

[Foto de configuración de departamentos_centro_intranet.conf](/proyecto1eval/imagenes/apache2_departamentos_centro_intranet.conf.png)


### Activar el módulo “wsgi” para permitir la ejecución de aplicaciones Python


### Crea y despliega una pequeña aplicación python para comprobar que funciona correctamente.


### Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación


### Instala y configura awstat.


### Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.

