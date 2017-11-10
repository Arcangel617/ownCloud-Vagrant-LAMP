# Instalación de ownCloud utilizando Vagrant, Ubuntu 16.04 (xenial), Apache, PHP7 y MySQL  
Ésta guía está basada en el siguiente [tutorial](https://hipertextual.com/archivo/2014/10/owncloud/) el cual lo adapté de acuerdo a mis necesidades.
> Nota: Se asume que [Vagrant](https://www.vagrantup.com/) ya está instalado en el sistema host. 
#### Requerimientos
- Vagrant
- Git

### Clonar el repositorio
```
$ git clone https://github.com/Arcangel617/ownCloud-Vagrant-LAMP.git
```
### Inicializamos nuestra máquina virtual
```
$ cd ownCloud-Vagrant-LAMP && vagrant up
```
Una vez que nuestra máquina esté corriendo accedemos a ella de la mediante ssh de la siguiente forma:
```
$ vagrant ssh
```
Si todo fue bien veremos algo como esto:
```
Welcome to Ubuntu 16.04.3 LTS (GNU/Linux 4.4.0-98-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


Last login: Fri Nov 10 06:23:02 2017 from 10.0.2.2
ubuntu@ubuntu-xenial:~$ 
```
### Instalar LAMP stack
Una vez que hayamos accedido procedemos a instalar los siguientes paquetes 
```
$ sudo apt-get install language-pack-es
```
```
$ sudo apt-get install lamp-server^
```
> Nota: recordar agregar el ^ al final
```
$ sudo mysql_secure_installation 
```
#### Instalación de paquetes adicionales para PHP
```
$ sudo apt-get install php7.0-gd php-xml-parser php7.0-intl smbclient curl libcurl3 php7.0-curl php7.0-mbstring php7.0-zip 
```
#### Configuración de apache
Habilitamos los siguientes módulos de apache:
```
$ sudo a2enmod rewrite
$ sudo a2enmod headers
```
Ahora debemos editar una línea del archivo apache2.conf
```
$ sudo nano /etc/apache2/apache2.conf 
```
Guardamos los cambios y reiniciamos el servicio
```
$ sudo service apache2 restart
```

#### Instalación de ownCloud
Al momento de realizar este tutorial la última versión de ownCloud es la 10.0.3. Si se quiere utilizar dicha versión basta con descargarla de la siguiente forma:
```
$ wget https://download.owncloud.org/community/owncloud-10.0.3.tar.bz2
```
De lo contrario si se quiere utilizar la última versión, debemos descargarla de la siguiente forma:
```
$ wget https://download.owncloud.org/community/owncloud-latest.tar.bz2
```
Descomprimimos el archivo descargado:
```
$ tar -xjf owncloud-10.0.3.tar.bz2 
```
> Si hemos descargado la última versión,el archivo será el siguiente : owncloud-latest.tar.bz2 

Movemos el directorio que se ha generado a /var/www/html
```
$ sudo mv owncloud /var/www/html/
```
y nos trasladamos a dicho directorio
```
$ cd /var/www/html/
```
Una vez allí le otorgamos los siguientes permisos:
```
$ sudo chown -R www-data:www-data owncloud/
```
#### Configurar la base da datos
```
$ mysql -u root -p
```