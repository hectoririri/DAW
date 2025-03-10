# Actividad 3. 
## Descarga la imagen de ubuntu, hello-world y nginx
Para descargar las imágenes usaremos el comando `docker pull`. Indicando el nombre de la imagen que queremos como parámetro nos descargará la imagen:
```ubuntu
$ sudo docker pull ubuntu
$ sudo docker pull hello-world
$ sudo docker pull nginx
```
![image](https://github.com/user-attachments/assets/d7c430c5-8967-4bd6-ae80-bea8e85d57e6)
Podemos ver en los distintos mensajes que se ha descargado correctamente.

## Muestra un listado de todas la imágenes
Con el comando `docker images ls` podremos mostrar todas las imágenes que tengamos descargadas en nuestro equipo:
![image](https://github.com/user-attachments/assets/1b8f94c9-b998-41b1-89a6-431deecb54fa)

## Ejecuta un contenedor hello-world y dale nombre “myhello1”
Para ejecutar un contenedor ejecutaremos el comando `docker run` para ejecutar el contenedor y el parámetro `--name` para dar el nombre del contenedor al que llamamos al que queramos:
```ubuntu
$ sudo docker run --name myhello1 hello-world
```
![image](https://github.com/user-attachments/assets/93a12851-5708-4750-a0a2-1252754d4a28)

## Ejecuta un contenedor hello-world y dale nombre “myhello2”
Repetiremos el ejercicio anterior cambiando la propiedad `--name`:
```ubuntu
$ sudo docker run --name myhello2 hello-world
```
![image](https://github.com/user-attachments/assets/f6a768a9-a99b-4515-bb91-e4602a99404c)

## Ejecuta un contenedor hello-world y dale nombre “myhello3”
Repetiremos el ejercicio anterior cambiando la propiedad `--name`:
```ubuntu
$ sudo docker run --name myhello3 hello-world
```
![image](https://github.com/user-attachments/assets/f6b2f1ea-48f1-44f7-8895-af01a999b260)

## Muestra los contenedores que se están ejecutando

![image](https://github.com/user-attachments/assets/566e7255-74bf-4668-b33c-e26e6d7d3e7a)


## Para el contenedor "myhello1”
## Para el contenedor "myhello2”
## Borra el contenedor “myhello1”
## Muestra los contenedores que se están ejecutando.
## Borra todos los contenedores
