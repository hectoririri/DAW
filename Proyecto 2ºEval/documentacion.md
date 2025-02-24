# 1º Creación de VPC

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



paquete linux para conectar con efs -> apt-get install nfs-common


