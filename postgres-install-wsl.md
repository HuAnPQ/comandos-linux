# Comandos usados en ubuntu desde WSL_2

sudo apt-get update 

sudo apt-get install postgresql postgresql-contrib 

service postgresql status 

## Iniciar: 
sudo service postgresql start 

## Entrar 
sudo su - postgres

psql 

## Cambiar contraseña del usuario postgres: 
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';" 

https://tableplus.com/blog/2018/10/how-to-start-stop-restart-postgresql-server.html
