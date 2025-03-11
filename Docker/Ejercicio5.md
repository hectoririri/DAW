# Ejercicio 5
## Lleva a cabo al menos tres de los ejemplos mostrados en el módulo cuatro “Docker-compose” y documentalo en tu repositorio incluyendo capturas de pantalla.
### Ejemplo 1:
Primero crearemos una carpeta donde almacenaremos nuestro **docker-composer.yaml** llamada


### Ejemplo 2: Despliegue de la aplicación guestbook [enlace](https://github.com/josedom24/curso_docker_ies/blob/main/modulo4/guestbook.md):
Para este ejemplo repetiremos el anterior creando así el directorio **guestbook-hector** donde almacenaremos nuestro **docker-composer.yaml**. 
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

Con esto habremos terminado.

### Ejemplo 3:

