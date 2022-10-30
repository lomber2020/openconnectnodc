Setup OpenConnect Server on Ubuntu
OS : Ubuntu 22.04 64.bit
_______________________________

1) Install Docker:

sudo apt update

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

apt-cache policy docker-ce

sudo apt install docker-ce

sudo systemctl status docker

_______________________________

2) Install OpenConnect Container On Server

>>> Build docker image:
docker build -t ocserv https://github.com/lomber2020/openconnectnodc.git

>>> Run docker container:
docker run --name ocserv --privileged -p 80:443 -p 80:443/udp -d ocserv


.:::Commands:::.

>>> Add user:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd test

>>> Show all users and hashed password
docker exec -ti ocserv cat /etc/ocserv/ocpasswd

>>> Change user password:
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd test

>>> Delete user
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -d test

>>> Lock user
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -l test

>>> Unlock user
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -u test



special tnx to iw4p♥
