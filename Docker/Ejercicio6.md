# Ejercicio 6
## Lleva a cabo al menos tres de los ejemplos mostrados en el módulo 5 “Creación de imágenes Docker” y documentalo en tu repositorio incluyendo capturas de pantalla.
### Ejemplo 1: Construcción de imágenes con una una aplicación Python [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo5/ejemplo3.md)
Para este ejemplo, primero crearemos nuestro **Dockerfile** y el directorio donde monstaremos la imagen. Ejecutaremos los siguientes comandos:
```ubuntu
$ sudo mkdir app
$ sudo nano Dockerfile

Pegamos el siguiente contenido
# syntax=docker/dockerfile:1
FROM debian:12
RUN apt-get update && apt-get install -y python3-pip  && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/share/app
COPY app .
RUN pip3 install --no-cache-dir --break-system-packages -r requirements.txt
EXPOSE 3000
CMD python3 app.py
```
![image](https://github.com/user-attachments/assets/466ef2b6-336a-4e26-8b87-a6ea07beaff9)

Ahora crearemos el siguiente archivo de texto para poder instalar pip3:
```
$ sudo nano requirements.txt
pegamos lo siguiente:
certifi==2020.12.5
chardet==4.0.0
click==7.1.2
Flask==1.1.2
idna==2.10
itsdangerous==1.1.0
Jinja2==2.11.3
MarkupSafe==1.1.1
requests==2.25.1
urllib3==1.26.3
Werkzeug==1.0.1
```
![image](https://github.com/user-attachments/assets/fc1f48b0-209a-415a-8f89-f8a7fd4d03fe)


Ahora crearemos la imagen usando el comando `docker build` con los siguientes parámetros:
```ubuntu
$ docker build -t josedom24/ejemplo3:v1 .
```
![image](https://github.com/user-attachments/assets/ddea0357-129a-4e4c-88b3-d106910c212d)

Por último, mostraremos las imágenes que tenemos disponibles en nuestro equipo `(docker images)`, a lo que encontraremos esta. La ejecutaremos con `docker run` y los siguientes parámetros:
```ubuntu
$ docker images | grep ejemplo3
$ docker run -d -p 80:3000 --name ejemplo2 josedom24/ejemplo3:v1
```
![image](https://github.com/user-attachments/assets/15c69965-b149-4c37-956c-b96892282be4)

### Ejemplo 2: Construcción de imágenes con una una aplicación PHP [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo5/ejemplo2.md)
Para este ejemplo seguiremos los mismos pasos que en el anterior. Primero crearemos la carpeta y nuestro fichero **Dockerfile**:
```ubuntu
$ sudo mkdir app
$ sudo nano Dockerfile

Pegamos lo siguiente:
# syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 libapache2-mod-php php && apt-get clean && rm -rf /var/lib/apt/lists/* && rm /var/www/html/index.html
COPY app /var/www/html/
EXPOSE 80
CMD apache2ctl -D FOREGROUND
```
![image](https://github.com/user-attachments/assets/641af839-746c-46fd-b05c-a902a25c7000)

Ahora creamos la imagen con el comando `docker build`:
```ubuntu
$ docker build -t josedom24/ejemplo2:v1 .
```
![image](https://github.com/user-attachments/assets/d5bfda8a-a7d8-4467-884f-04e8328f5740)

Buscaremos nuestra imagen en las que tenemos en nuestro dispositivo con `docker images`:
```ubuntu
$ docker images | grep ejemplo2
$ sudo docker run -d -p 80:80 --name ejemplo3 josedom24/ejemplo2:v1
```
![image](https://github.com/user-attachments/assets/24a4f732-44c7-4ca3-bf78-badd79d1a92b)


### Ejemplo 3: Construcción de imágenes con una página estática [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo5/ejemplo1.md)
Repetiremos los ejemplos anteriores. Esta vez crearemos un directorio donde almacenaremos una página web .html además de nuestro fichero **Dockerfile**:
```ubuntu
$ mkdir public_html
$ sudo nano public_html/index.html
```
```html
pegamos lo siguiente
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pagina web HNG</title>
</head>
<body>
    <h1>Muestra de que la página web funciona</h1>
</body>
</html>
```
Y ahora crearemos el fichero **Dockerfile**:
```ubuntu
$ nano Dockerfile
pegamos lo siguiente
# syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/html/
COPY public_html .
EXPOSE 80
CMD apache2ctl -D FOREGROUND
```
![image](https://github.com/user-attachments/assets/f3853ff6-ea55-41c5-ad4f-dcb147717272)

Creamos la imagen con `docker build` y comprobamos que se ha creado con `docker images`:
```ubuntu
$ docker build -t josedom24/ejemplo1:v1 .
$ docker images | grep ejemplo1
```
![image](https://github.com/user-attachments/assets/6a0c5bb9-c641-4447-8249-2e9319b71b56)

Ahora crearemos el contenedor con `docker run`:
```ubuntu
$ docker run -d -p 80:80 --name ejemplo1 josedom24/ejemplo1:v1
```
![image](https://github.com/user-attachments/assets/82f9184b-f7e2-42a5-9cfb-b028d743951e)



