# Ejercicio 1. 

## Crea un script que añada un puerto de escucha en el fichero de configuración de Apache. El puerto se recibirá como parámetro en la llamada y se comprobará que no esté ya presente en el fichero de configuración.

Primero nos moveremos a la ruta donde se encuentra la configuración de Apache utilizando el comando **"cd"** con la ruta **"/etc/apache2"**.
```ubuntu
cd /etc/apache2
```
Aquí crearemos una carpeta llamada **"mis_scripts"** donde guardaremos todos los scripts que crearemos a lo largo del ejercicio.
Con el comando **"mkdir"** crearemos nuestra carpeta en la ubicación actual:
```ubuntu
sudo mkdir mis_scripts
```
Ahora crearemos nuestro archivo .sh para ejecutar nuestro script con el comando **"touch"**.
Lo ejecutaremos seguido del nombre del fichero que vamos a crear, el cual será **"script1.sh"**:
```ubuntu
sudo touch script1.sh
```
Tenemos que habilitar unos permisos para los scripts de Ubuntu y que así puedan ejecutarse, por lo que ejecutaremos el comando **"chmod"** seguido de sus respectivos parámetros.
Estos serán **"755"** para que el propietario y otros puedan ejecutarlo. Añadimos el nombre del fichero como segundo parámetro para que modifique este:
```ubuntu
sudo chmod 755 script1.sh
```
Listaremos la carpeta actual para confirmar la creación del fichero script y sus permisos correspondientes con **"ls -l"**.
Este es el resultado del script con los permisos modificados -->

[Imagen permisos script1.sh](/tema1/imagenes/script1ls.png)

Para editar nuestro script debemos de ejecutar el comando **"nano"** seguido del nombre del script para editarlo. Nano es un editor de texto que Ubuntu trae por defecto:
```ubuntu
sudo nano script1.sh
```
Escribiremos el siguiente script y lo guardamos pulsando Ctrl+O y Enter:

[Imagen código de script1.sh](/tema1/imagenes/script1.png)

Ahora ejecutaremos el script utilizando **"./"** antes de escribir el nombre del script en el terminal, para así ejecutarlo. Probaremos ejecutándolo sin argumentos, con uno correcto y otro incorrecto para comprobar que se ejecuta correctamente:

[Imagen ejecutando y probando script1.sh](/tema1/imagenes/script1ejecutado.png)

De esta manera, nuestro script está funcionando correctamente.
