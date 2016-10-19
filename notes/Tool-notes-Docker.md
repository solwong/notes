# Common use
```shell
docker attach $containerName
docker port $containerName
docker run -it
```

# Client and Server
## Server
```shell
sudo docker run -d redis
sudo docker inspect -f '{{.NetworkSettings.IPAddress}}' $imageID # Fet the Server IP
```

## Client
```shell
sudo docker run -it ubuntu /bin/bash

sudo apt-get install redis-server

rediscli -h $clientIP
```

# Network
## Modify the Docker Network
```shell
ifconfig
sudo ifconfig docker0 192.168.200.1 netmask 255.255.255.0
sudo service docker restart
```
## Set connect between container
### Allow all
```shell
docker run -it --name cct1 ubuntu
docker run -it --name cct2 ubuntu

docker attach cct1
docker run -it --name cct3 --link=cct1:webtest ubuntu

```
### Forbidden all
```shell
docker run ... --icc=false
```
```shell
# Modify the etc file
vi /etc/default/docker

DOCKER_OPTS = '--icc=false'
sudo service docker restart
```

### Permit some
```shell
--icc=false --iptables=true --link
```

##  Connection between host and docker
```shell
sudo iptables -L -n
sudo iptables -I DOCKER -s 10.211.55.3 -d 172.17.0.7 -p TCP --dport 80 -j DROP
```
