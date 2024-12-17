## Ejercicio AWS

# Crear instancia en AWS
Para crear una instancia en AWS iniciaremos sesión en este y seguiremos la siguiente ruta para llegar al laboratorio:

[Imagen ruta a seguir para entrar en el laboratorio](/tema1/imagenes/aws_ruta_laboratorio.png)

Una vez lleguemos aquí tendremos que iniciarlo para poder acceder a nuestro menú y lanzar nuestras instancias. Para lanzarlo pulsaremos sobre **"Start Lab"**, y una vez el icono de la izquierda cambie a verde haremos click sobre este para acceder al menú y las instancias:

[Imagen lanzar el laboratorio](/tema1/imagenes/aws_iniciando_laboratorio.png)

Al haber hecho click sobre el icono de AWS, volveremos a seguir la siguiente ruta para llegar al apartado de instancias y poder lanzar una:

[Imagen ruta a seguir para entrar en las instancias](/tema1/imagenes/aws_ruta_instancias.png)

Estando en el apartado de instancias, lanzaremos una pulsando sobre **"Lanzar instancias"** y configuraremos nuestra instancia en el siguiente apartado:

[Imagen lanzando una instancia](/tema1/imagenes/aws_lanzando_instancia.png)

La configuración de la instancia es la siguiente: (cambié el tamaño de almacenamiento a 8gb y el tipo de instancia a t2.medium porque no tenía permisos para usarlo)

+ [Imagen configuración de instancia 1](/tema1/imagenes/aws_configuracion_instancia1.png)

+ [Imagen configuración de instancia 2](/tema1/imagenes/aws_configuracion_instancia2.png)

+ [Imagen configuración de instancia 3](/tema1/imagenes/aws_configuracion_instancia3.png)

Una vez finalice la instancia, veremos la siguiente pantalla de confirmación:

[Imagen confirmación de instancia](/tema1/imagenes/aws_confirmacion_instancia.png)

Volveremos al apartado de las instancias para seleccionar la que creamos y conectarnos a ella. Una vez seleccionada marcando un checkbox pulsaremos sobre **"Conectar"**:

[Imagen cómo conectarse, la ruta, a una instancia](/tema1/imagenes/aws_como_conectar.png)

Nos saltará una nueva ventana donde configuraremos la forma en la que queramos conectarnos y lo haremos desde el navegador de la siguiente manera:

[Imagen conectándose a una instancia](/tema1/imagenes/aws_conectandose_instancia.png)

Una vez nos conectemos, veremos que saltará una nueva ventana en la que veremos un simulador de la terminal de linux de nuestra instancia. Desde aquí realizaremos las siguientes actividades:

[Imagen conectado a instancia desde navegador](/tema1/imagenes/aws_conectado_instancia.png)


# Activar la autenticación con MySql
Damos por hecho que Apache2 está instalado en nuestra instancia, ya que se explicó en el otro proyectó. Primero instalaremos MySQL con el siguiente comando:
```ubuntu
$ sudo apt install mysql-server
```
Y ahora instalaremos el módulo de autenticación de MySQL para Apache2:
```ubuntu
$ sudo apt-get install libaprutil1-dbd-mysql
```
Activaremos ahora sí el módulo de autenticación MySQL usando **"a2enmod"**:
```ubuntu
$ sudo a2enmod dbd
$ sudo a2enmod authn_dbd
```
[Imagen activando los modulos](/tema1/imagenes/aws_activando_modulos.png)


Una vez habilitado los modulos, configuraremos el archivo de configuración de Apache2 (el del sitio web que usaremos) para declarar la configuración de autenticación con MySQL. Para esto lo indicaremos en el archivo de configuración **"/etc/apache2/sites-available/000-default.conf"** (en este caso) y usando el comando **"nano"** introduciendo lo siguiente:
```ubuntu
$ sudo nano /etc/apache2/sites-available/000-default.conf
```
[Imagen archivo configuración Apache2 autenticación MySQL](/tema1/imagenes/aws_apache_autenticación_MySQL.png)

Por último, reiniciaremos el servidor de Apache2 con **"systemctl"**
```ubuntu
$ sudo systemctl restart apache2
```


# Crear un certificado autofirmado y activar el módulo SSL
Primero instalaremos la librería criptográfica de **"openssl"**, que es la que usaremos para crear nuestro certificado:
```ubuntu
$ sudo apt install openssl
```

Ahora crearemos una carpeta en la que almacenaremos nuestro certificado autofirmado para organizarlo mejor. En esta carpeta crearemos nuestro certificado que durará 365 días, con el sistema criptográfico rsa:2048 y demás parámetros que tendremos que rellenar mientras generamos la clave:
```ubuntu
$ sudo mkdir /etc/apache2/ssl
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```
[Imagen creación de certificado autofirmado](/tema1/imagenes/aws_apache_creacion_certificado_autofirmado.png)

Después de crear nuestro certificado, habilitaremos el módulo y sitio de SSL:
```ubuntu
$ sudo a2enmod ssl
$ sudo a2ensite default-ssl
```

Ahora configuraremos el archivo de configuración de Apache2 para habilitar el funcionamiento de SSL. Para esto añadiremos lo siguiente:
```ubuntu
$ sudo nano /etc/apache2/sites-available/000-default.conf
```
[Imagen archivo configuración Apache2 certificado autofirmado](/tema1/imagenes/aws_apache_certificado_autofirmado.png)

Por último, reiniciaremos el servidor de Apache2 con el comando **"systemctl"**:
```ubuntu
$ sudo systemctl restart apache2
```

