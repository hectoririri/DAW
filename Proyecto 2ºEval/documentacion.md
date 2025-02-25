![imagen](https://github.com/user-attachments/assets/94866744-11e8-4c14-ad4a-fb7480539280)# 1º Creación de VPC

Primero tenemos que crear la estructura de nuestra red, donde incluiremos las diferentes instancias y servidores EFS y RDS. Nuestra VPC constará de 4 subredes; 2 públicas y 2 privadas. 
Para crearlas entraremos a nuestro labotario de AWS y buscaremos la opción **"VPC"** en el buscador e ingresaremos en el siguiente resultado:
![image](https://github.com/user-attachments/assets/f0504f7e-aaa4-483d-8d68-dbcf7abf6ec2)

Ahora entraremos en el apartado de **"Sus VPC"** para crear el nuestro propio. Para ello pulsaremos sobre **"Crear VPC"**
![image](https://github.com/user-attachments/assets/e24f599c-cf5c-43f4-8d8e-92eff47a801f)

Una vez aquí, ingresaremos los siguientes datos para crear nuestra VPC:

1/1![image](https://github.com/user-attachments/assets/f71e20d0-10ed-4821-8693-44f6818f83ed)
1/2![image](https://github.com/user-attachments/assets/c1d6efcd-211f-48b1-95d4-9f5c020f5261)

Ahora podremos ver la pantalla de confirmación de la creación del VPC. Podemos verla si entramos en **"Ver VPC"**:
![image](https://github.com/user-attachments/assets/7b6101b8-b42b-48b5-bf59-927f2c46fa9a)

# 2º Creación de EC2

Ahora crearmos nuestra instancia donde alojaremos nuestro servidor Apache 2 y Wordpress. Para ello escribiremos en el buscador **"EC2"** e ingresaremos en el siguiente resultado:

![image](https://github.com/user-attachments/assets/074562b3-5452-4b92-8335-18ccb3dbbbab)

Para lanzar una instancia, primero entraremos en el apartado de estas para visualizarlas y crearlas. Entraremos **"Instancias"** para lanzar una pulsando sobre **"Lanzar instancias"**:

![image](https://github.com/user-attachments/assets/a3c39190-d49c-4c6a-bb12-761c933a1caa)

Ahora introduciremos los siguientes datos a la hora de crear nuestra EC2 para así poder conectarnos a esta, incluirla en nuestra VPC, etc...

1/5![image](https://github.com/user-attachments/assets/a5bc3563-7a1e-446a-875f-a41da454c583)

2/5![image](https://github.com/user-attachments/assets/2615911e-2057-48bc-94b2-9f12944c58a9)

3/5![image](https://github.com/user-attachments/assets/85981ba0-109d-400d-8769-1df5d4585000)

4/5![image](https://github.com/user-attachments/assets/97f430c1-3408-4f78-9f92-fbd5d466c0d3)

5/5![image](https://github.com/user-attachments/assets/76fdad14-6d4a-41c0-aabc-d86aae6aadb4)

Una vez pulsado sobre **"Lanzar instancia"** podremos ver el proceso de creación de nuestra EC2 y la confirmación de esta. Para visualizarla pulsaremos sobre **"Ver todas las instancias"**

![image](https://github.com/user-attachments/assets/df8f4fd5-9c26-4126-8c31-2f177908b4fe)

Una vez aquí, marcaremos el checkbox de nuestra EC2 para conectarnos a ella pulsando después sobre **"Conectar"**:
![imagen](https://github.com/user-attachments/assets/febf1479-6589-420d-8d05-0885d1347e28)

Aquí seleccionaremos la manera en la que nos conectaremos a nuestra instancia EC2. Elegiremos la conexión por navegador y el nombre de usuario por defecto, que es ubuntu, y pulsaremos sobre **"Contectar"**:
![imagen](https://github.com/user-attachments/assets/965fcb24-54c4-4093-8d98-f3d60e67636f)

Se nos abrirá una pestaña nueva donde tendremos la terminal de nuestra instancia. Aquí procederemos con la instalación de PHP y Apache.
![imagen](https://github.com/user-attachments/assets/4536bf98-1782-4f91-9a38-3efaf4b01d7d)

# 3º Instalación Apache y PHP


Para instalar nuestro servidor Apache, primero actualizaremos nuestro sistema y ejecutaremos los siguientes comandos para la instalación y comprobación de que esta misma se realizó con éxito:
```ubuntu
$ sudo apt update ; sudo apt upgrade
$ sudo install apache2
$ sudo apache2 -v
```
1/2![imagen](https://github.com/user-attachments/assets/93018a27-4bcc-4b76-b24b-417354db894b)
2/2![imagen](https://github.com/user-attachments/assets/1c5ba51d-6efc-49fd-9216-bff16538b055)

Una vez la instalación se haya completado, ejecutaremos el siguiente comando para levantar el servidor y el posterior que hará que Apache se inicie cada vez que se arranca la instancia
```ubuntu
$ sudo systemctl start apache2
$ sudo systemctl enable apache2
```
![imagen](https://github.com/user-attachments/assets/5f4ac9ec-055b-42b9-98e6-1946fee2a0fc)
![imagen](https://github.com/user-attachments/assets/d68cd65d-d290-4c76-ad1a-22e6ede68ad7)


Para acceder a este desde internet, debemos de escribir en nuestro navegador la dirección IP pública. Esta la encontraremos en la información de nuestra instancia EC2:
1/2![imagen](https://github.com/user-attachments/assets/2989e20c-d723-47a9-ab7e-f2dd84b635d6)
2/2![imagen](https://github.com/user-attachments/assets/8659a2a6-00fb-4338-9dde-4b1787dae3d8)

## PHP
Para la instalación de PHP, primero debemos comprobar que el paquete amazon-linux-extras ya está instalado en nuestro servidor con el siguiente comando. En mi caso ya lo está:
```ubuntu
$ sudo apt -y update && sudo apt upgrade
```
![imagen](https://github.com/user-attachments/assets/3e9f7692-f76c-415d-933f-d5e2ae8a8210)

Ahora instalaremos PHP mediante un módulo de Apache2. El comando que ejecutaremos para instalar la versión más reciente será el siguiente:
```ubuntu
sudo apt install php libapache2-mod-php php-cli
```
Podemos ver como los paquetes que vamos a instalar de PHP se refieren a la versión 8.3:
![imagen](https://github.com/user-attachments/assets/0bb37a0a-f2b7-4e23-9ef4-b3cac19e7c78)

Para confirmar la instalación de este ejecutaremos el siguiente comando:
```ubuntu
$ php -v
```
![imagen](https://github.com/user-attachments/assets/2f3eabf7-3400-4814-a8ff-52fa788db645)

Ahora instalaremos MySQL como módulo de apache, por lo tanto ejecutaremos el siguiente comando:
```ubuntu
$ sudo apt install php-mysql
```
![imagen](https://github.com/user-attachments/assets/9b91b0cd-22a7-4f2c-b307-5d2fc2ce321a)

Una vez terminada la instalación, reiniciaremos el servidor de Apache y comprobaremos su funcionamiento con los siguientes comandos:
```ubuntu
$ sudo systemctl restart apache2
$ sudo systemctl status apache2
```
![imagen](https://github.com/user-attachments/assets/e23ac01c-1810-41f8-811b-dd394f28e63c)

Con esto habremos terminado la configuración de Apache y PHP en nuestra instancia EC2.

# 4º Creación de la base de datos

Ahora nos moveremos al apartado de AWS e introduciremos en el buscador **"RDS"** y entraremos en el siguiente resultado:
![imagen](https://github.com/user-attachments/assets/7bdcccf9-2f0f-4fa6-a04c-3a4603749e28)

Una vez aquí, nos moveremos a la sección de **"Bases de datos"** y pulsaremos sobre **"Crear base de datos"**
![imagen](https://github.com/user-attachments/assets/287288b6-b7f8-4a34-aa60-8dbacc380df4)

Ahora configuraremos la base de dato de la siguiente manera:
1/7![imagen](https://github.com/user-attachments/assets/502bf3e6-243c-456e-881f-31b1fae1c831)
2/7![imagen](https://github.com/user-attachments/assets/172ccca7-132c-4701-b325-6cf4ae4e1017)
3/7![imagen](https://github.com/user-attachments/assets/aa0a9edc-fa85-4216-88fc-c06ea37b7ab0)
4/7![imagen](https://github.com/user-attachments/assets/9ae17bb4-5904-4a09-8442-b78c9c9de4b7)
5/7![imagen](https://github.com/user-attachments/assets/5c6c4d28-b36d-421c-9a68-722cdb59b8c7)
6/7![imagen](https://github.com/user-attachments/assets/b3b1639a-00a3-4ea6-b7a3-9526fe177363)
7/7![imagen](https://github.com/user-attachments/assets/9eec5e38-d978-4df2-88b7-fc6464817806)

Ahora debemos de configurar los grupos de seguridad para que podamos conectarnos a la base de datos desde la instancia EC2. Para ello, usaremos el asistente que se encargará de establecer los permisos necesarios en los grupos de seguridad entre ambas máquinas. Marcaremos el checkbox seleccionando nuestra base de datos y pulsaremos sobre **"Acciones"** -> **"Configurar la conexión de EC2"**:
![imagen](https://github.com/user-attachments/assets/874204cf-7e77-4229-9aae-77afdfe41cfb)

En la nueva ventana, seleccionaremos nuestra instancia EC2 Apache que configuramos anteriormente:
![imagen](https://github.com/user-attachments/assets/8e0818dc-01dd-4ca6-b996-93b1103da360)

Confirmaremos la conexión entre ambas máquinas pulsando sobre **"Configurar"**:
![imagen](https://github.com/user-attachments/assets/b1ed3d99-b472-438c-9143-94124bc107bd)

Podemos entrar en la configuración de nuestra base de datos y anotar el punto de enlace de esta que usaremos más adelante a la hora de configurar wordpress:
![imagen](https://github.com/user-attachments/assets/2a27b70b-96f7-480f-acce-4e7445db3ed0)

Ya hemos terminado de configurar nuestra base de datos.

# 5º Elastic File System (EFS)
Ahora vamos a crear el sistema de almacenamiento externo que vamos a conectar con la instancia, y más tarde configuraremos para que se conecte en Wordpress también. Para crearlo, debemos de ir al buscador de AWS y escribir **"EFS"** y entrar en el siguiente resultado:
![imagen](https://github.com/user-attachments/assets/adacf487-36a6-42a8-95c6-90d59724edf1)

Una vez hayamos entrado, pulsaremos sobre **"Crear un sistema de archivos"** para comenzar con la creación de nuestro EFS:
![imagen](https://github.com/user-attachments/assets/f87ef306-17f2-4299-961d-a926217fd514)

Ahora asignaremos un nombre a este y la VPC en la que se podrán conectar nuestras instancias, en este caso, la que creamos el principio:
![imagen](https://github.com/user-attachments/assets/a0af3d60-3d52-4e99-b8a9-a13e0b417fc4)

Ya creado, entraremos en la configuración de nuestro EFS *haciendo click en su nombre* y confirmaremos que se ha montado en las subredes correspondientes de nuestro VPC:
![imagen](https://github.com/user-attachments/assets/14131e6a-6296-427b-9c19-a73462e845df)

Ahora permitiremos la entrada de conexión de nuestra instancia EC2 añadiendo el grupo de seguridad de este a la instanacia EFS. Para ello pulsaremos sobre **"Administrar"** en la pantalla anterior. Una vez aquí, añadiremos en ambas zonas de disponibilidad el grupo de seguridad al que pertence la instancia EC2. En la información de nuestra EC2 aparece de la siguiente manera:
![imagen](https://github.com/user-attachments/assets/62cf64c8-a149-4cd5-9592-64ea1174bbef)

Añadiremos el grupo de seguridad en la instancia EFS de la siguiente manera:
![imagen](https://github.com/user-attachments/assets/9ed9063d-3ad0-43d9-b612-5faa6a6c1d38)

Ahora incluiremos la conexión EFS en las reglas del grupo de seguridad en el que se encuentra la instancia EC2. Así las conexiones a la EFS podrán realizarse. Para ello nos iremos al menú de VPC y en concreto al apartado de **"Grupos de seguridad"**. Aquí buscaremos el grupo de seguridad que añadimos en la EFS para modificarlo en el buscador y entraremos a este: 
![imagen](https://github.com/user-attachments/assets/d574e270-3f61-4d6e-9198-7dd41d6af039)

Aquí editaremos las reglas de entrada para permitir la procediente desde una conexión EFS. Entraremos en en **"Editar reglas de entrada"**:
![imagen](https://github.com/user-attachments/assets/5b703c0d-bebe-4ca9-8fd6-758f2590b556)

Aquí añadiremos una nueva regla que permita las entradas tipo **"EFS"** desde cualquier IP. Pulsaremos sobra **"Guardar reglas"**:
![imagen](https://github.com/user-attachments/assets/69d22add-bce4-4b10-8a90-f91b268f2dd2)


Ahora vincularemos la instancia EC2 con la instancia EFS. Para ello, iremos a la instancia EFS y entraremos en los detalles de esta haciendo click sobre su nombre. 
![imagen](https://github.com/user-attachments/assets/2389cbd9-041b-4fc7-9eda-6a87515d6f9e)

Una vez en los detalles de esta, pulsaremos sobre **"Asociar"** y copiaremos el la siguiente línea:
![imagen](https://github.com/user-attachments/assets/66ecf464-c21a-4fb2-b71d-5375a985bcfc)

Una vez copiada al línea, nos moveremos a la terminal de nuestra instancia EC2. Aquí instalaremos el siguiente paquete antes de hacer la conexión:
```ubuntu
$ apt-get install nfs-common
```
![imagen](https://github.com/user-attachments/assets/94d33319-0d9c-47a2-918d-e3acee65da7d)

Crearemos la carpeta en la que almacenaremos los archivos que se encuentren en la EFS, para ello ejecutaremos el siguiente comando:
```ubuntu
$ mkdir miefs
```
Ahora pegaremos el comando que copiamos anteriormente para conectar la instancia EC2 con la EFS cambiando la carpeta final por la que hemos creado:
![imagen](https://github.com/user-attachments/assets/35d4d36a-ffa0-4a55-800a-9f2f6f552eff)

Podemos ver que ya se ha montado correctamente al no saltar ningún error al ejecutar el comando. Hemos terminado con la configuración de la EFS.

# 6º Instalación Wordpress
Ahora procederemos con la instalación de Wordpress. Nos moveremos al directorio */var/www/html* para descargar el archivo comprimido de Wordpress y descomprimirlo en el mismo sitio. Ejecutaremos los siguientes comandos:
```ubuntu
$ cd /var/www/html
$ sudo wget http://wordpress.org/latest.tar.gz
$ sudo tar -xf latest.tar.gz
```
Una vez ejecutado los comandos, el directorio debería de quedar tal que así:
![imagen](https://github.com/user-attachments/assets/4061375b-c8c7-481a-bea5-8ee27efb9e02)

A continuación crearemos un usuario y contraseña para Wordpress. Para ello primero descargaremos el cliente de mysql para poder conectarnos. Ejectuaremos el siguiente comando:
```ubuntu
$ apt install default-mysql-client
```
![imagen](https://github.com/user-attachments/assets/8624d8c8-6058-497a-b472-71e0b3efea18)

Nos iremos al menú de RDS para copiar el punto de enlace y conectarnos a la base de datos ERS que creamos anteriormente. Aquí buscaremos nuestra base de datos y nos iremos al siguiente apartado para copiar lo siguiente:
![imagen](https://github.com/user-attachments/assets/f7a1291d-50ab-49a5-a292-5be4ccec8dee)

Ahora volveremos a nuestra instancia EC2 para ejecutar el siguiente comando donde pegaremos el punto de enlace de nuestra base de datos y así conectarnos a ella:
```ubuntu
$ mysql -u admin -h dbmiwordpress.cux0zbzopjym.us-east-1.rds.amazonaws.com -p
```

A continuación ejecutaremos las siguientes líneas de MySQL para crear nuestra base de datos Wordpress:
```mysql
mysql> CREATE DATABASE miwordpress; 
mysql> CREATE USER 'hnungar584'@'%' IDENTIFIED BY 'Gvuubw56'; 
mysql> GRANT ALL PRIVILEGES ON wordpress.* TO 'hnungar584'@'%'; 
mysql> FLUSH PRIVILEGES;
```

Si hemos hecho todo bien hasta ahora. el resultado debería de ser el siguiente:
![image](https://github.com/user-attachments/assets/777ba012-4a88-43d6-ac9c-8218bff693ed)



