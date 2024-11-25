## Ejercicio 2

# Crea un script que añada un nombre de dominio y una ip al fichero hosts. Debemos comprobar que no existe dicho dominio en el fichero hosts

Volveremos a ir a la carpeta de **"mis_scripts"** para crear este segundo script. Volveremos a ejecutar el comando **"touch"** seguido del nombre de nuestro nuevo script, que será ***script2.sh***.
```ubuntu
sudo touch script2.sh
```
Ahora modificaremos los permisos del script, como hicimos anteriormente, con **"chmod"** seguido de los permisos "755".
```ubuntu
sudo chmod 755 script2.sh
```
Abriremos el script con el editor de texto **"nano"** y escribiremos el siguiente código:
```ubuntu
sudo nano script2.sh
```
[Imagen código script2.sh](/tema1/imagenes/script2.png)
Al guardar con Ctrl+O y Enter, lo ejecutaremos de diferentes maneras para comprobar que el código funciona correctamente:
```ubuntu
sudo ./script2.sh ip dominio
```
[Imagen pruebas script2.sh](/tema1/imagenes/script2ejecutado.png)
Podemos ver que las condiciones del script funcionan correctamente y no deja añadir un dominio si ya existe, y lo añade si no existe.
