# Obtener la Ip 
> ip addr show wlp2s0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

Print =  192.168.0.104

# Obtener la Ip Publica
curl -4 icanhazip.com
200.25.142.106

sudo su -

## Mostrar dispositivos de red y su configuración.
> ifconfig ip addr show // ip link show

## Activar una interfaz de red.
> ifconfig eth0 up ip link set eth0 up

## Desactivar una interfaz de red.
> ifconfig eth0 down ip link set eth0 down

## Establecer una dirección IP a una interfaz.
> ifconfig eth0 192.168.1.1 ip address add 192.168.1.1 dev eth0

## Añadir una interfaz virtual.
> ifconfig eth0:1 10.0.0.1/8 ip addr add 10.0.0.1/8 dev eth0 label eth0:1
