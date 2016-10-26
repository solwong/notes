## Install
```shell
## Docker Engine
curl -sSL https://get.docker.com/ | sh
docker --version

## Not sudo
sudo usermod -aG docker pine
newgrp $docker

## Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## Problem

`ERROR: for service-controller  Cannot start service service-controller: invalid header field value "oci runtime error: container_linux.go:247: starting container process caused \"exec: \\\"./startServiceBroker.sh\\\": permission denied\"\n"
ERROR: Encountered errors while bringing up the project`

This is caused by error environment like the shell file is not found.

## `docker-compose up` and `docker-compose restart`

`docker-compose up`: Create a Docker Container and start it, if there is someone running, stop and remove before create a new.
`docker-compose restart`: Restart a new Docker Container, this cannot be effective when a Docker Container config Changed.

## Usage

## Common use
```shell
docker attach $containerName
docker port $containerName
docker run -it

## Stop all container
docker stop $(docker ps -q)
## Remove all container
docker rm $(docker ps -aq)
```

## Docker Compose
```shell
## Edit the docker-compose.yml file
docker-compose build
docker-compose up
```

## Key-map
* `CTR + P, CTR + Q`: Change but not exit

## Client and Server
### Server
```shell
sudo docker run -d redis
sudo docker inspect -f '{{.NetworkSettings.IPAddress}}' $imageID ## Fet the Server IP
```

### Client
```shell
sudo docker run -it ubuntu /bin/bash

sudo apt-get install redis-server

rediscli -h $clientIP
```

## Network
### Modify the Docker Network
```shell
ifconfig
sudo ifconfig docker0 192.168.200.1 netmask 255.255.255.0
sudo service docker restart
```
### Set connect between container
#### Allow all
```shell
docker run -it --name cct1 ubuntu
docker run -it --name cct2 ubuntu

docker attach cct1
docker run -it --name cct3 --link=cct1:webtest ubuntu

```
#### Forbidden all
```shell
docker run ... --icc=false
```
```shell
## Modify the etc file
vi /etc/default/docker

DOCKER_OPTS = '--icc=false'
sudo service docker restart
```

#### Permit some
```shell
--icc=false --iptables=true --link
```

###  Connection between host and docker
```shell
sudo iptables -L -n
sudo iptables -I DOCKER -s 10.211.55.3 -d 172.17.0.7 -p TCP --dport 80 -j DROP
```
