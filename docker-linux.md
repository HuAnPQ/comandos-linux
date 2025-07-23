# Prerequisitos

## Instalar los paquetes necesarios

sudo apt update

sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2

## Configurar el repositorio para instalar docker

source /etc/os-release

curl -fsSL https://download.docker.com/linux/${ID}/gpg | sudo apt-key add -

echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list

echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu jammy stable" | sudo tee /etc/apt/sources.list.d/docker.list

sudo apt update

# Instalar Docker

sudo apt install docker-ce docker-ce-cli containerd.io

## Agregar nuestro usuario al grupo Docker

sudo usermod -aG docker $USER

## Configurar Dockerd

DOCKER_DIR=/mnt/wsl/shared-docker

mkdir -pm o=,ug=rwx "$DOCKER_DIR"

sudo chgrp docker "$DOCKER_DIR"

sudo mkdir /etc/docker

sudo vim /etc/docker/daemon.json

{
"hosts": ["unix:///mnt/wsl/shared-docker/docker.sock"]
}
