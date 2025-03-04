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
