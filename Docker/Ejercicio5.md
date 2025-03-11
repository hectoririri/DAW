# Ejercicio 5
## Lleva a cabo al menos tres de los ejemplos mostrados en el módulo cuatro “Docker-compose” y documentalo en tu repositorio incluyendo capturas de pantalla.
### Ejemplo 1: Despliegue de la aplicación guestbook [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo4/guestbook.md):
Para este ejemplo repetiremos el anterior creando así el directorio **guestbook-hector** donde almacenaremos nuestro **docker-compose.yaml**. 
```
$ mkdir guestbook-hector
```
Dentro de este crearemos el archivo con el comando `nano` pegando el siguiente contenido:
```ubuntu
$ nano docker-compose.yaml
```
```json
version: '3.1'
services:
  app:
    container_name: guestbook
    image: iesgn/guestbook
    restart: always
    environment:
      REDIS_SERVER: redis
    ports:
      - 8080:5000
  db:
    container_name: redis
    image: redis
    restart: always
    command: redis-server --appendonly yes
    volumes:
      - redis:/data
volumes:
  redis:
```
![imagen](https://github.com/user-attachments/assets/a041e80b-0bac-4678-b200-afc7936e6b2a)

Para crear el escenario usando este fichero, nos moveremos dentro de la carpeta y ejecutaremos el comando `docker compose` con los siguientes parámetros para que utilice el fichero que creamos en el paso anterior:
```ubuntu
$ cd guestbook-hector
$ docker compose -f docker-compose.yaml up -d
```
![imagen](https://github.com/user-attachments/assets/79166436-0903-41e5-9b77-e19de3356df5)

Con esto habremos terminado el primer ejemplo.

### Ejemplo 2: Despliegue de la aplicación Temperaturas [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo4/temperaturas.md):
Repetiremos los mismos pasos que en el ejemplo anterior. Primero crearemos el directorio para el ejemplo:
```
$ mkdir temperatura-hector
$ nano temperatura-hector/docker-compose.yaml
```
Ahora el fichero **docker-compose.yaml** con el siguiente contenido:
```json
version: '3.1'
services:
  frontend:
    container_name: temperaturas-frontend
    image: iesgn/temperaturas_frontend
    restart: always
    ports:
      - 8081:3000
    environment:
      TEMP_SERVER: temperaturas-backend:5000
    depends_on:
      - backend
  backend:
    container_name: temperaturas-backend
    image: iesgn/temperaturas_backend
    restart: always
```
![imagen](https://github.com/user-attachments/assets/ea32852d-1b74-4f3c-80e7-c020c0fb5d6f)

Y ahora crearemos el escenario con el comando `docker compose`:
```ubuntu
$ cd temperatura-hector
$ docker compose -f docker-compose.yaml up -d
```
![imagen](https://github.com/user-attachments/assets/4290868a-d212-418b-8dd3-ab16219d45e8)

Con esto habremos terminado el segundo ejemplo.

### Ejemplo 3 Despliegue de tomcat + nginx [enlace]:
Repetiremos los mismos pasos que en el ejemplo anterior. Esta vez nos moveremos al directorio ya creado con los ficheros de configuración para el **tomcat y nginx**. Aquí crearemos el fichero **docker-compose.yaml**
```
$ cd tomcat
$ nano docker-compose.yaml
```
En el fichero pegaremos el siguiente contenido:
```json
version: '3.1'
services:
  aplicacionjava:
    container_name: tomcat
    image: tomcat:9.0
    restart: always
    volumes:
      - ./sample.war:/usr/local/tomcat/webapps/sample.war:ro
  proxy:
    container_name: nginx
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./default.conf:/etc/nginx/conf.d/default.conf:ro
```
![imagen](https://github.com/user-attachments/assets/c79b4f8d-e2d7-4d12-ade8-6e013b92b916)

Ahora ejecutaremos el comando para crear el escenario usando `docker compose -f docker-compose.yaml up -d`:
```ubuntu
$ docker compose -f docker-compose.yaml up -d
```
![imagen](https://github.com/user-attachments/assets/f787ab45-e81a-494f-b198-d155583579e4)
