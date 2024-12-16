## Ejercicio AWS

# Activar la autenticación con MySql
Primero instalaremos MySQL con el siguiente comando:
```ubuntu
sudo apt install mysql-server
```
Y ahora instalaremos el módulo de autenticación de MySQL para Apache2:
```ubuntu
sudo apt install libapache2-mod-auth-mysql
```
Activaremos ahora sí el módulo de autenticación MySQL usando **"a2enmod"**:
```ubuntu
sudo a2enmod auth_mysql
```

Una vez habilitado, configuraremos el archivo de configuración de Apache2 para declarar la configuración de autenticación con MySQL. Para esto lo indicaremos en el archivo de configuración **"/etc/apache2/sites-available/000-default.conf"** usando el comando **"nano"** e introduciendo lo siguiente:
```ubuntu
sudo nano install /etc/apache2/sites-available/000-default.conf
```
[Imagen archivo configuración Apache2 autenticación MySQL](/tema1/imagenes/apache_autenticación_MySQL.png)
<Directory /var/www/html>
    AuthType Basic
    AuthName "Restricted Content"
    AuthBasicProvider mysql
    AuthMySQLHost localhost
    AuthMySQLUser your_mysql_user
    AuthMySQLPassword your_mysql_password
    AuthMySQLDB your_database
    AuthMySQLUserTable your_user_table
    AuthMySQLNameField username
    AuthMySQLPasswordField password
    Require valid-user
</Directory>

Por último, reiniciaremos el servidor de Apache2 con **"systemctl"**
```ubuntu
sudo systemctl restart apache2
```


# Crear un certificado autofirmado y activar el módulo SSL
Primero crearemos una carpeta en la que almacenaremos nuestro certificado autofirmado para organizarlo

```ubuntu
sudo mkdir /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```
