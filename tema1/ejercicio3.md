## Ejercicio 3

# 

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
Ejecutaremos el script de diferentes maneras para comprobar que el código funciona correctamente:
[Imagen código script3.sh](/tema1/imagenes/script3.png)
```ubuntu
sudo ./script3.sh 
```
[Imagen pruebas script3.sh](/tema1/imagenes/script3ejecutado.png)


Podemos ver que las condiciones del script funcionan correctamente y no deja añadir un dominio si ya existe, y lo añade si no existe.
