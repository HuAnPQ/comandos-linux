# Obtener la Ip 
ip addr show wlp2s0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
192.168.0.104

# Obtener la Ip Publica
curl -4 icanhazip.com
200.25.142.106

sudo su -
