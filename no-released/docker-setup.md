<!-- # Docker - Getting started -->

## Quickly start

### 1. Clone our project

#### Have no our projecct.

If you use the command tool, like:
```shell
git clone -b pine_docker https://github.com/CloudEDA/AuroraPlatform.git
# ...wait...
cd AuroraPlatform
```

#### Have already our projecct.

```shell
cd AuroraPlatform
git fetch origin pine_docker
git checkout pine_docker
```

### 2. Do some configuration

Copy the these files end of .env.sample, then, modify the effective environment files (those are end of .env) according to your own computer.

```shell
cp  .env.sample   .env
cp  docker.env.sample   docker.env
# Then do some changes to these new files.
# ...
```

### 3. Install Docker

If you use a Windows or macOS, you may goto [Docker Home], and install it by steps.

If you use a Linux, do follow below:

```shell
curl -sSL https://get.docker.com/ | sh
# Not sudo
sudo usermod -aG docker $USER
newgrp docker
# Docker Compose
sudo -i
# Input your sudo password
curl -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
logout
docker --version && docker-compose --version
```

If your `docker --version` and `docker-compose --version` commands both run well, themes the thing went well!

Also, if you pull images slowly in China, you can speed it by [configuring Docker Mirrors].

### 4. Up you APP

```shell
# Ensure you are in the project directory (AuroraPlatform).
docker-compose up
# ...wait...
```
Wait for it, until the the commands stop changing, open you browser, go to the address: `http://localhost:3000/`

If you see an error about Rails APP, don't be afraid, this show you are succeed in step.

This error occur when your are first run the database container. To solve it, you should reopen a terminal and do these:

```shell
docker-compose run app rake db:setup
```

Then, every thing will be completed, **congratulations**!

These are some common commands:

```shell
docker-compose ps       # List all Services
docker-compose up       # Create and start containers
docker-compose start    # Start Services
docker-compose stop     # Stop Services
docker-compose restart  # Restart Services
docker-compose down     # Stop and remove containers, networks, images, and volumes
```

## Some skill

### Docker data

- Do you want to know the data of these Services on docker? Please see the tmp folder of our project. And also, you can set your own path on .env file.

### Running in background

- You want to run our app in the background? You can add `-d` parameter:

```shell
# Shop your running APP
# ...wait...
docker-compose up -d
```

Then you can tracking APP by:

```shell
docker-compose logs -f
```

### Control some part of Services

- You want to control some part of our APP? Try to attach some service name when using up, start, stop etc.:

```shell
# Restart the ServiceController and DB (MySQL) service
docker-compose restart circuit db
# Stop the web and db service
docker-compose stop web db
```

Until now, there are seven Services in total:

1. **web**: The Rails APP, serve the WEB Service.

2. **db**: We use the MySQL5.7 to serve our data storage.

3. **cache**: We use the Redis3.2 to serve our data cache.

4. **queue**: We use the Sidekiq to serve our queue server.

5. **service-broker**: The Broker service, mainly powerd by Java.

6. **trans-layout**: The Trans-layout service, mainly powerd by Java.

7. **trans-schematic**: The Trans-schematic service, mainly powerd by Java.

8. **svc-verification**: The Verification service, mainly powerd by Java.

## Advanced

- [Doker - Continuous Integration]


[Docker Home]: https://www.docker.com/products/docker

[Doker - Continuous Integration]: https://github.com/CloudEDA/AuroraPlatform/wiki/%5BDoker%5D--Continuous-Integration

[configuring Docker Mirrors]: http://www.daocloud.io/mirror.html
