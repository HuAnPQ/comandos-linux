# Instalacion de Nginx
# https://www.nanotutoriales.com/instalacion-de-nginx
sudo apt-get update
sudo apt-get install nginx

# Configuracion
sudo nano /etc/nginx/nginx.conf

# Descomentar
server_tokens off

# Restart Nginx
sudo services nginx restart

## Check your Web Serve
systemctl status nginx

### https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-in-ubuntu-16-04
## Comandos de Nginx Process
sudo systemctl stop nginx
sudo systemctl start nginx
# Para recargar sin perder conexiones
sudo systemctl reload nginx
# Para no cargar Nginx al arrancar el sistema
sudo systemctl disable nginx
sudo systemctl enable nginx

## MySql
sudo apt-get install mysql-server
mysqladmin -uroot -pmysupersecretpassword proc
mysql_secure_installation
# /usr/bin/mysqladmin -u root password 'MySql++26'
# select user();
# SHOW VARIABLES WHERE Variable_name = 'port';
# Cmabiar contrasena de root
# alter user 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Mysql++26';

## Php
sudo apt-get install php-fpm php-mysql
# Para mejorar la seguridad de php-fpm
sudo nano /etc/php/7.0/fpm/php.ini
cgi.fix_pathinfo=0
# Necesario para que funcione php en nginx
sudo nano /etc/php/7.2/fpm/pool.d/www.conf
# en este archivo cambiar la linea 
# de abajo por la siguiente
;listen = 127.0.0.1:9000
listen = /var/run/php/php7.2-fpm.sock

# Luego de lo de arriba restart
sudo systemctl restart php7.2-fpm

# Verificar si esta en la ruta el archivo sock
ll /var/run/php
# Reiniciar fpm y nginx si no aparece
service php7.2-fpm restart
service nginx restart

# Configuracion de Nginx
sudo nano /etc/nginx/sites-available/default
# Para validar los cambios en el archivo de arriba
sudo nginx -t




