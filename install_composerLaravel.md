# Comandos para instalar composer

## Previo

> php --ini
> sudo apt-get install php7.2-zip

# Sacado de este sitio https://tecadmin.net/install-laravel-framework-on-ubuntu/

~~~console
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
sudo chmod +x /usr/local/bin/composer
~~~~

# Verificar instalacion de composer
> composer -V


## Para ver el archivo de los $PATH
> sudo nano /etc/environment
> echo $PATH


## Para instalar laravel/installer
# download installer
> composer global require "laravel/installer=~1.1"

# para anadir mas alias 
> nano ~/.bashrc

# add
## Eg => alias laravel='~/.composer/vendor/bin/laravel'
> alias laravel='~/.config/composer/vendor/bin/laravel'

## Mas recomendado es esta opcion
> export PATH="~/.config/composer/vendor/bin:$PATH"

## Importante luego ejecutar el comando siguiente
> source ~/.bashrc

# Probar en una nueva terminar si funciona el comando laravel
> laravel

# going to html dir to create project there
> cd /var/www/html/

# install project in blog dir.
> laravel new blog



