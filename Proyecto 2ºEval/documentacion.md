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
5/7![imagen](https://github.com/user-attachments/assets/be212f57-0b02-43f0-8f7b-a91f6f070c7a)
6/7![imagen](https://github.com/user-attachments/assets/b3b1639a-00a3-4ea6-b7a3-9526fe177363)
7/7![imagen](https://github.com/user-attachments/assets/9eec5e38-d978-4df2-88b7-fc6464817806)

Hemos metido la base de datos en los mismos grupos de seguridad en los que se encuentra nuestra instancia EC2, por lo tanto no tenemos que configurar el grupo de seguridad de nuestra instancia RDS para que pueda conectarse a la instancia EC2.

Ahoras








paquete linux para conectar con efs -> apt-get install nfs-common


