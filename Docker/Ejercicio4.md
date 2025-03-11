# Ejercicio 4
## Lleva a cabo al menos tres de los ejemplos mostrados en el módulo tres “Almacenamiento y redes Docker” y documentalo en tu repositorio incluyendo capturas de pantalla.
### Ejemplo 1: Despliegue de la aplicación Temperaturas [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo3/temperaturas.md)
Esta aplicación de temperaturas está dividida en dos partes: **Frontend y Backend.** Por esto, primero configuraremos una red para contectar ambos contenedores. Para ello ejecutaremos el siguiente comando:
```ubuntu
$ docker network create red_temperaturas
```
Ahora ejecutaremos ambos contenedores, frontend y backend:
```ubuntu
$ docker run -d --name temperaturas-backend --network red_temperaturas iesgn/temperaturas_backend
$ docker run -d -p 80:3000 --name temperaturas-frontend --network red_temperaturas iesgn/temperaturas_frontend
```
El resultado debe ser el siguiente:
![imagen](https://github.com/user-attachments/assets/85c65ea1-5f29-49fc-a606-ed7f33a1bdda)

Con esto, ahora accederemos a nuestra dirección IP, es decir, al localhost en nuestro navegador para comprobar si los contenedores se están ejecutando y comunicando correctamente:
![imagen](https://github.com/user-attachments/assets/9cb98043-a502-4384-8f8b-1dc6421b935e)
*(he ejecutado el ejercicio en una máquina virtual ya que con AWS no me permitía acceder a la aplicación)*

### Ejemplo 2: Despliegue de tomcat + nginx [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo3/tomcat.md)
Volveremos a crear una red para que los contenedores puedan comunicarse entre sí. Para ello ejecutaremos el comando `docker network` con los siguientes parámetros:
```ubuntu
$ docker network create red_tomcat
```
![imagen](https://github.com/user-attachments/assets/4d29c610-d5c8-4eaa-bec7-d0e83a860c36)

Ahora vamos a crear un contenedor con la imagen de **tomcat**. Primero crearemos una carpeta donde guardaremos los siguientes archivos que nos encontraremos en el siguiente repositorio y que son necesarios para la configuración:
```ubuntu
$ mkdir tomcat
Guardamos los ficheros del repositorio aquí
$ ls tomcat
```
![imagen](https://github.com/user-attachments/assets/55edaa31-def4-4e1b-a84e-9b64b0f62354)

Ahora crearemos el contenedor conectado a nuestra red:
```ubuntu
$ docker run -d --name aplicacionjava \
                --network red_tomcat \
                -v /home/vagrant/tomcat/sample.war:/usr/local/tomcat/webapps/sample.war:ro \
                tomcat:9.0
```
![imagen](https://github.com/user-attachments/assets/352ec8af-b693-40fa-b66a-80f120b4da90)

Ahora desplegaremos el nginx como proxy inverso. Para ello crearemos el siguiente contenedor nginx:
```ubuntu
$ docker run -d --name proxy \
                -p 80:80 \
                --network red_tomcat \
                -v /home/hector/tomcat/default.conf:/etc/nginx/conf.d/default.conf:ro \
                nginx
```
![imagen](https://github.com/user-attachments/assets/fafeeff7-bfd9-49dc-8de4-ab7a48e6a88b)

Ahora accederemos a nuestra dirección para comprobar el funcionamiento de la aplicación:
![imagen](https://github.com/user-attachments/assets/f5fd716f-16fc-4f26-8f14-6660ac38ab63)

### Ejemplo 3: Despliegue de la aplicación Guestbook [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo3/guestbook.md)
La aplicación de Guestbook también utiliza dos contenedores que tienen que comunicarse entre sí, por lo que primero crearemos una red donde meteremos ambos contenedores:
```ubuntu
$ docker network create red_guestbook
```

Ahora crearemos ambos contenedores dentro de esta red:
```ubuntu
$ docker run -d --name redis --network red_guestbook -v /opt/redis:/data redis redis-server --appendonly yes
$ docker run -d -p 80:5000 --name guestbook --network red_guestbook iesgn/guestbook
```

Ahora nos iremos a nuestro navegador y accederemos a nuestra dirección usando localhost:

