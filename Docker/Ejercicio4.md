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


### Ejemplo 3: Despliegue de la aplicación Guestbook [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo3/guestbook.md)

