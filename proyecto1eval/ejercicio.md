# Proyecto 1º Evaluación

## En este archivo realizaremos todas las actividades del primer proyecto de esta primera evaluación. Iremos apartado por apartado explicando y mostrando con capturas de pantalla cómo lo realizo.


### 1. Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python
Para la instalación de apache abriremos un terminal de Ubuntu *(Ctrl+Alt+T)* y actualizaremos el sistema con el siguiente comando utilizando **"apt"**. Siempre utilizaremos **"sudo"** de aquí en adelante al necesitar de permisos de administrador.
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

### Instala y configura wordpress [ayuda](https://www.hostinger.es/tutoriales/instalar-wordpress-ubuntu)
Para instalar Wordpress primero debemos de tener instalado PHP y MySQL. Como ya tenemos php instalado en nuestra máquina, comenzaremos con la instalación de MySQL. Debemos de tener una base de datos MySQL antes de instalar Wordpress, por lo que ejecutaremos el comando **"apt"** seguido de los siguientes parámetros:
```ubuntu
$ sudo apt install mysql-server -y
```
Una vez instalado,  reiniciaremos nuestro servidor Apache2 con **"systemctl"** y abriremos el terminal de MySQL con el comando **"mysql"**:
```ubuntu
# sudo systemctl restart apache2
$ sudo mysql
```
Crearemos nuestra base de datos para wordpress usando la siguiente orden: 
```mysql
mysql> CREATE DATABASE WordPress;
```
Ahora crearemos un usuario para trabajar con la base de datos:
```mysql
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'contrasena';
```
Y por último asignaremos los permisos al usuario para poder ejecutar cualquier orden SQL, recargaremos la base de datos y saldremos:
```mysql
GRANT ALL PRIVILEGES ON wordpress.* TO 'wp_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
Este es el resultado de todos los comandos anteriores: [órdenes sql](imagenes/mysql_wordpress.png)

Activaremos el módulo rewrite con el comando **"a2enmod"**, el paquete **"wget"** y unzip para comenzar con la instalación de WordPress:
```ubuntu
$ sudo a2enmod rewrite
$ sudo apt install wget
$ sudo apt install unzip
```
**Ahora podemos comenzar con la instalación de WordPress.** Primero descargaremos el archivo comprimido de WordPress usando el comando **"wget"** seguido de la dirección web:
```ubuntu
$ sudo wget https://wordpress.org/latest.zip
```
Una vez descargado, lo moveremos con el comando **"mv"** al directorio donde queramos alojar WordPress, que en nuestro caso es /var/www/centro_intranet. Una vez movido lo descomprimiremos con el comando **"unzip"**
```ubuntu
$ sudo mv latest.zip /var/www/centro_intranet
$ cd /var/www/html
$ sudo unzip latest.zip
```
Ahora moveremos todo lo que se encuentra en la carpeta wordpress al directorio actual con el comando **"mv -r"**. Después de esto eliminaremos el archivo *index.html* con el comando **"rm -rf"**:
```ubuntu
$ sudo mv -f wordpress/* ./
$ sudo rm -rf index.html
```
Por último, modificaremos el usuario, grupo y permisos de la carpeta */var/www/centro_intranet* con el comando **"chown"** y **"chmod"** de la siguiente manera. También reiniciaremos el servidor apache2 con **"systemctl"**:
```ubuntu
$ sudo chown -R www-data:www-data /var/www/centro_intranet
$ sudo chmod -R 755 /var/www/centro_intranet
$ sudo systemctl restart apache2
```
Ahora ingresaremos en el dominio de centros.intranet y podremos ver la primera pantalla de configuración de WordPress: [captura de inicio en WordPress](imagenes/wordpress_idiomas.png)

Seleccionaremos nuestro idioma y continuaremos. WordPress nos informará de los datos que nos pedirá a continuación para continuar con la configuración, que son sobre la base de datos que creamos anteriormente. Continuamos.

Ahora introduciremos el nombre de la base de datos, el usuario y contraseña que creamos anteriormente. Una vez introducido pulsaremos sobre **"Enviar"**:
[captura de información base de datos en WordPress](imagenes/wordpress_base_de_datos.png)

Nos confirmará que WordPress ha establecido una conexión con nuestra base de datos y ahora podremos terminar con la instalación. Pulsaremos sobre **"Realizar la instalación"**.
Ahora tendremos que rellenar la información básica del título del sitio web, usuario y contraseña, correo electrónico, etc...:
[captura de información básica WordPress](imagenes/wordpress_informacion_basica.png)

Podremos ver en la siguiente pantalla de confirmación que nuestro WordPress ha sido instalado correctamente. Ahora iniciaremos sesión y accederemos a nuestro WordPress:
[captura de confirmación WordPress](imagenes/wordpress_confirmacion.png)
[captura de menu inicio WordPress](imagenes/wordpress_menu.png)

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
Primero crearemos el fichero *.py* que usaremos para crear nuestra aplicación y ejecutarla más adelante. Utilizaremos el comando **"nano"** directamente:
```ubuntu
$ sudo nano /var/www/html/wsgy.py
```

[aplicacion en python](imagenes/python_aplicacion.png)

A continuación, damos los permisos adecuados al archivo *wsgi.py* con el comando **"chown"** y **"chmod"**:
```ubuntu
$ sudo chown www-data:www-data /var/www/html/wsgy.py
$ sudo chmod 755 /var/www/html/wsgy.py
```

Ahora configuraremos el archivo de configuración de este 

[captura de configuración dominio python](imagenes/python_dominio.png)








### Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación



### Instala y configura awstat.
Primero descargaremos los paquetes necesarios para instalar awstat:
```ubuntu
$ sudo apt-get install awstats libgeo-ipfree-perl libnet-ip-perl -y
```
Una vez descargado, copiaremos la plantilla con el comando **"cp"** que encontramos en la ruta */etc/awstats/awstats.conf* y la pegamos en /etc/awstats/departamentos_centro_intranet.conf. El nombre del fichero que copiamos será el nombre de nuestro dominio, en nuestro caso, departamentos.centro.intranet:
```ubuntu
$ sudo cp /etc/awstats/awstats.conf /etc/awstats/departamentos_centro_intranet.conf
```
Ahora editaremos este fichero de configuración que hemos copiado con el comando **"nano"** y escribiremos lo siguiente:
```ubuntu
$ sudo nano /etc/awstats/departamentos_centro_intranet.conf
```

[captura de configuración](imagenes/awstat_configuracion_dominio.png)

Al configurar este archivo lo copiaremos con **"cp"** en la misma carpeta pero con *"www."* al principio del archivo ya que AWstats distingue el www:
```ubuntu
$ cp /etc/awstats/$DOMINIO.conf /etc/awstats/www.$DOMINIO.conf
```
A continuación, configuraremos el archivo de configuración de apache2 *(/etc/apache2/apache2.conf)* con el comando **"nano"** para poder acceder a la página de AWstats:
```ubuntu
Alias /awstatsclasses "/usr/share/awstats/lib/"
Alias /awstats-icon/ "/usr/share/awstats/icon/"
Alias /awstatscss "/usr/share/doc/awstats/examples/css"
ScriptAlias /statistics/ /usr/lib/cgi-bin/
Redirect /awstats /statistics/awstats.pl
Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
```

[captura de fichero de configuración apache2.conf](imagenes/awstats_apache2_conf.png)

Por último, habilitaremos el módulo **"cgi"** y reiniciaremos nuestro servidor Apache2 con **"systemctl"** e ingresaremos en la siguiente ruta de nuestro dominio para acceder al AWstats de nuestro dominio:
```ubuntu
$ sudo a2enmod cgi
$ sudo systemctl restart apache2
```

[captura de awstats en dominio departamentos.centro.intranet](imagenes/awstats_funcionando.png)






### Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.

