## Ejercicio 3

# Crea un script que nos permita crear una página web con un título, una cabecera y un mensaje

Volveremos a ingresar a la carpeta de **"mis_scripts"** y crearemos nuestro último script. Ejecutaremos el comando **"touch"** seguido de ***script3.sh***.
```ubuntu
sudo touch script3.sh
```
Ahora modificaremos los permisos del script con **"chmod"** y los establecemos a 755.
```ubuntu
sudo chmod 755 script3.sh
```
Editaremos el código del script con el editor de texto **"nano"** y escribiremos el siguiente código. Guardamos con Ctrl+O y Enter.
```ubuntu
sudo nano script3.sh
```
[Imagen código script3.sh](/tema1/imagenes/script3.png)

Ejecutaremos el script de diferentes maneras para comprobar que el código funciona correctamente:
```ubuntu
sudo ./script3.sh 
```
[Imagen pruebas script3.sh](/tema1/imagenes/script3ejecutado.png)

Ahora, el código genera una página html con los argumentos que el usuario le pase al ejecutar el **"script3.sh"**. Aquí podemos ver una visualización de la página web:
[Imagen página web script3.sh](/tema1/imagenes/script3html.png)

Documentación a parte de la moodle para el comando cat ODF: https://blog.pachahosting.com/como-escribir-texto-en-un-archivo-usando-el-comando-linux-cat/
