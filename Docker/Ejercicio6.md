# Ejercicio 6
## Lleva a cabo al menos tres de los ejemplos mostrados en el módulo 5 “Creación de imágenes Docker” y documentalo en tu repositorio incluyendo capturas de pantalla.
### Ejemplo 1: Construcción de imágenes con una una aplicación Python [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo5/ejemplo3.md)
Para este ejemplo, primero crearemos nuestro dockerfile y el directorio donde monstaremos la imagen. Ejecutaremos los siguientes comandos:
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

### Ejemplo 2:  [enlace]()

