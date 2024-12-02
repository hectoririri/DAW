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

[Foto de la estructura de carpetas en /var/www/](/proyecto1eval/imagenes/apache2_estructura_carpetas.png)

Ahora crearemos un fichero de onfiguración para cada dominio en el que le indicaremos su ruta de carpeta, nombre de dominio, etc... Para esto, iremos a la carpeta **"/etc/apache2/sites-avaliable"**.
En esta carpeta se encuentran los ficheros de configuración para cada dominio que tengamos en nuestro Apache2. Copiaremos el que hay por defecto y lo modificaremos para cada dominio:

```ubuntu
$ cd /etc/apache2/sites-avaliable
$ sudo cp 000-default.conf centro_intranet.conf
$ sudo cp 000-default.conf departamentos_centro_intranet.conf
```

Una vez copiado, modificaremos cada fichero de configuración en respecto al dominio al que queramos hacer referencia. Primero configuraremos el de centro_intranet, por lo tanto ejecutaremos el comando **"nano"** seguido del fichero para editarlo.
Para guardar haremos Ctrl+O y Enter. Para salir Ctrl+X:

```ubuntu
$ sudo nano centro_intranet.conf
```
Ahora modificaremos el fichero de la siguiente manera y haremos lo mismo para el fichero de departamentos_centro_intranet:

[Foto de configuración de centro_intranet.conf](/proyecto1eval/imagenes/apache2_centro_intranet.conf.png)

[Foto de configuración de departamentos_centro_intranet.conf](/proyecto1eval/imagenes/apache2_departamentos_centro_intranet.conf.png)

+ *"ServerName"* -> Nombre del dominio
+ *"ServerAdmin"* -> Correo del administrador del dominio
+ *"DocumentRoot"* -> Recursos que el dominio accederá, como su index.html, imagenes, etc...

Ahora que los ficheros de configuración están listos, los habilitaremos para Apache2 utilizando el comando **"a2ensite"** para habilitar el sitio web.
Al usarlo hacemos referencia al fichero de configuración del sitio web, por lo que lo ejecutaremos con ambos ficheros:
```ubuntu
$ sudo a2ensite centro_intranet.conf
$ sudo a2ensite departamentos_centro_intranet.conf
```
Una vez habilitados ambos ficheros, reiniciaremos el servicio de Apache2 para que los cambios que hicimos surjan efecto. Ejecutaremos el comando **"systemctl reload"** y a continuación **"systemctl status"** para comprobar el estado de Apache2:
```ubuntu
$ sudo systemctl reload apache2
$ sudo systemctl status apache2
```
Al comprobar que el servidor está activo, añadiremos ambos dominios al fichero **"hosts"** de nuestro Ubuntu para poder acceder a los dominios, ya que estos no son públicos tenemos que especificar en qué máquina se encuentra.
Como se encuentra en nuestra propia máquina, indicaremos nuestra IP y los nombres de los dominios. Nuestra IP la conseguiremos ejecutando el comando **"ip a"** y recogiendo la IP que se encuentre en el apartado "inet" de la siguiente manera:
```ubuntu
$ ip a
```
[Foto de mi ip](/proyecto1eval/imagenes/apache2_ip.png)

Ahora que tenemos nuestra IP, ejecutaremos el comando **"nano"** en el archivo *"/etc/hosts"* para indicar a esta IP los dominios a los que queremos acceder:
```ubuntu
$ sudo nano /etc/hosts
```
[Foto de archivo hosts](/proyecto1eval/imagenes/apache2_hosts.png)

Una vez guardado *(Ctrl+O y Enter)* podremos ir a nuestro navegador e introducir el dominio para comprobar que funciona correctamente. Introduciremos **"http://centro.intranet"** y **"http://departamentos.centro.intranet"**:
[Foto de dominios funcionando](/proyecto1eval/imagenes/apache2_dominios_funcionando.png)

### Activar los módulos necesarios para ejecutar php y acceder a mysql
Para activar los módulos, volveremos a ejecutar el comando **"a2enmod"** seguido del módulo que queramos activar, en nuestro caso, php:
```ubuntu
$ sudo a2enmod php
```

En caso de que al ejecutarlo nos indique el módulo no existe, lo instalaremos ejecutando el comando **"apt"** con los siguientes parámetros. De esta manera, también estaremos instalando la extensión para acceder a mysql:
```ubuntu
$ sudo apt update
$ sudo apt install php libapache2-mod-php php-mysql
```
+ *"php-mysql"* permite a PHP comunicarse con MySQL.

Una vez instalado php y sus extensiones, reiniciaremos nuestro servidor Apache2 con **"systemctl"**:
```ubuntu
# sudo systemctl restart apache2
```

### Instala y configura wordpress
Para instalar Wordpress primero debemos de tener instalado PHP y MySQL. Como ya tenemos php instalado en nuestra máquina, comenzaremos con la instalación de MySQL. Debemos de tener una base de datos MySQL antes de instalar Wordpress, por lo que ejecutaremos el comando **"apt"** seguido de los siguientes parámetros:
```ubuntu
$ sudo apt install mysql-server -y
```

Una ve instalado, abriremos el terminal de MySQL con el comando **"mysql"**:
```ubuntu
$ sudo mysql
```


### Activar el módulo “wsgi” para permitir la ejecución de aplicaciones Python
Para activar el módulo "wsgi" ejecutaremos el comando **"a2enmod"** seguido del nombre del módulo. Antes actualizaremos el sistema:
```ubuntu
$ sudo apt update ; sudo apt upgrade
$ sudo a2enmod wsgi
```
Ahora reiniciaremos Apache2 para confirmar que el módulo se ha habilitado correctamente ejecutando también el status del servidor Apache2:
```ubuntu
$ sudo systemctl reload apache2
$ sudo systemctl status apache2
```
En caso de que no lo tengamos instalado, podremos hacerlo ejecutando el comando **"apt install"** seguido de la libreria específica:
```ubuntu
$ sudo apt install libapache2-mod-wsgi-py3
```

### Crea y despliega una pequeña aplicación python para comprobar que funciona correctamente.


### Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación


### Instala y configura awstat.


### Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.

