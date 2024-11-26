# Proyecto 1º Evaluación

## En este archivo realizaremos todas las actividades del primer proyecto de esta primera evaluación. Iremos apartado por apartado explicando y mostrando con capturas de pantalla cómo lo realizo.


### Instalación del servidor web apache. Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python
Para la instalación de apache abriremos un terminal de Ubuntu *(Ctrl+T)* y actualizaremos el sistema con el siguiente comando utilizando **"apt"**. Siempre utilizaremos **"sudo"** de aquí en adelante al necesitar de permisos de administrador.
```ubuntu
sudo apt update ; sudo apt upgrade
```
Cuando nos pregunte "¿Desea continuar? [Y/n], escribiendo **"y"** y pulsando Intro confirmaremos la actualización de nuestro sistema. Una vez terminada la actualización, volveremos a usar el comando **"apt"** para instalar Apache2:
```ubuntu
sudo apt install apache2
```

[Foto de la instalación](/proyecto/imagenes/apache2_instalacion.png)

### Activar los módulos necesarios para ejecutar php y acceder a mysql


### Instala y configura wordpress


### Activar el módulo “wsgi” para permitir la ejecución de aplicaciones Python


### Crea y despliega una pequeña aplicación python para comprobar que funciona correctamente.


### Adicionalmente protegeremos el acceso a la aplicación python mediante autenticación


### Instala y configura awstat.


### Instala un segundo servidor de tu elección (nginx, lighttpd) bajo el dominio “servidor2.centro.intranet”. Debes configurarlo para que sirva en el puerto 8080 y haz los cambios necesarios para ejecutar php. Instala phpmyadmin.

