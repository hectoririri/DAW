# Actividad 1. Instalación de Docker en Ubuntu
Para la instalación de Docker en Ubuntu seguiré el siguiente [tutorial](https://www.tecmint.com/install-docker-and-run-docker-containers-in-ubuntu/).
Primero eliminaremos las versiones anteriores de Docker que se encuentren en nuestra máquina. Aunque sepamos que no lo hemos instalado podemos ejecutarlo sin problemas:
```ubuntu
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```
![image](https://github.com/user-attachments/assets/dc2f710e-7a3a-4916-826a-ce2e5465685c)
Podemos ver como no ha encontrado ninguna instalación de docker. Ahora actualizaremos nuestra máquina ubuntu e instalaremos Docker con los siguientes comandos:
```ubuntu
$ sudo apt-get update
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
![image](https://github.com/user-attachments/assets/12e07f33-5ced-48dc-bc04-69be9d60c40f)

Ahora instalaremos la última versión de Docker CE con el siguiente comando:
```ubuntu
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
![image](https://github.com/user-attachments/assets/6aa05ffd-cf4c-4139-b5fd-22c16e2db3af)

Una vez hayamos instalado el servicio, este se ejecutará automáticamente al instalarse y cada vez que iniciemos el sistema. Para comprobar el estado del servicio ejecutaremos el siguiente comando:
```ubuntu
$ sudo systemctl status docker 
```
![image](https://github.com/user-attachments/assets/b0e3d0e8-20e7-4f6b-8ee8-1699aee271e9)

Con esto hemos instalado correctamente nuestro Docker en Ubuntu.

# Actividad 2. 
## Lleva a cabo la práctica descrita en el primer artículo
### Ejecuta la imagen "hello-world"
Para ejecutar la imagen usaremos el comando **docker**, que es con el que iremos trabajando de aquí en adelante.
```ubuntu
$ sudo docker run hello-world
```
Podemos ver que en el mensaje nos indica que la instalación se ha ejecutado correctamente.
![image](https://github.com/user-attachments/assets/f69f5bf0-ca35-4c66-b001-25ff4285beb1)

### Muestra las imágenes Docker instaladas
Para mostrar las imágenes instaladas de nuestro Docker ejecutaremos el siguiente comando:
```ubuntu
$ sudo docker images
```
![image](https://github.com/user-attachments/assets/77c2630d-db92-44d6-bc49-eb2cd3bd4ed7)

### Muestra los contenedores Docker
Para mostrar los contenedores de nuestro Docker, utilizaremos el comando con el argumento **"-a"** para ver todos los contenedores (incluso los contenedores parados o cancelados).
```ubuntu
$ sudo docker ps -a
```
![image](https://github.com/user-attachments/assets/432010e5-2c42-4225-882e-fcfec62b8deb)

## Lleva a cabo la práctica descrita en el segundo artículo
### Edita el fichero Dockerfile
Para crear el fichero primero tenemos que bajarnos el codigo de la aplicación con la que vamos a trabajar el Dockerfile. Para ello clonaremos el repositorio con el que trabajaremos de la siguiente manera:
```ubuntu
$ sudo git clone https://github.com/docker/getting-started-app.git
$ ls getting-started-app/
```
![image](https://github.com/user-attachments/assets/f4b06518-752f-4af9-aa28-aeb8bf1214f9)
Ahora crearemos el fichero Dockerfile dentro de la carpeta clonada con el comando `nano` e introduciendo lo siguiente en este archivo:
```ubuntu
$ cd getting-started-app
$ sudo nano Dockerfile

# syntax=docker/dockerfile:1
FROM node:lts-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```
1/2![image](https://github.com/user-attachments/assets/975459d3-b9c8-48de-9d97-22cd754bd224)
2/2![image](https://github.com/user-attachments/assets/7f102d74-c1b6-45e5-a282-38124ddd8565)
Si obtenemos este resultado hemos seguido los pasos correctamente.

### Construye el contenedor
Ahora construiremos el contenedor ejecutando el siguiente comando. Este utiliza el fichero Dockfile que creamos anteriormente para copiar las instrucciones que escribimos en él en nuestra nueva aplicación:
```ubuntu
$ sudo docker build -t getting-started .
```
![image](https://github.com/user-attachments/assets/eb18699d-7790-4685-bcf9-3345ba6390c4)

### Ejecútalo
Para ejecutar nuestro contenedor usaremos el comando `docker run` con los siguientes parámetros. Esto nos permitirá ejecutar el contenedor y devolvernos de vuelta a la terminal:
```ubuntu
$ sudo docker run -d -p 127.0.0.1:3000:3000 getting-started
```
Podemos ver cómo hemos ejecutado el comando correctamente al igual que nuestro contenedor ahora está corriendo en la dirección `127.0.0.1:3000:`
![imagen](https://github.com/user-attachments/assets/b73726e4-7569-4f71-9711-97274b3c3e3c)

Para acceder a nuestro contenedor accederemos a nuestra instancia EC2 de AWS desde el navegador, entrando por el puerto 3000 estaremos accediendo al contenedor:


### Create una cuenta en hub.docker.com
### Publícalo



