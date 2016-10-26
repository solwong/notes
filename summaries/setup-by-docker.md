<!-- # Setup by Doker -->

## Quickly start

### 1. Clone our project

If you use the command tool, like:
```shell
git clone https://github.com/CloudEDA/AuroraPlatform.git
# ...wait...
cd AuroraPlatform
```

### 2. Do some configuration

Copy the the there files end of .env.sample, then, modify the three environment files (those are end of .env) according to your own computer.
```shell
cp  .env.sample   .env
cp  aurora-ws.env.sample   aurora-ws.env
cp  service-controller.env.sample   service-controller.env
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
sudo curl -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
If your `docker --version` and `docker-compose --version` commands both run well, themes the thing went well!

### 4. Run our APP

```shell
# Ensure you are in the project directory (AuroraPlatform).
docker-compose up
# ...wait...
```
Wait for it, until the the commands stop changing, open you browser, go to the address: `http://localhost:3000/`

If you see an error about Rails APP, don't be afraid, this show you are succeed in step.

This error occur when your are first run the database container. To solve it, you should do:
```shell
docker-compose run aurora-ws rake db:create
docker-compose run aurora-ws rake db:migrate
```
Then, every thing will be completed, **congratulations**!

These are some common commands:

```shell
docker-compose up       # Create and start containers
docker-compose start    # Start services
docker-compose stop     # Stop services
docker-compose restart  # Restart services
docker-compose down     # Stop and remove containers, networks, images, and volumes
docker-compose ps       # List containers
```

### \* Some skill

* You want to run our app in the background? You can add `-d` parameter:

```shell
# Shop your running APP
# ...wait...
docker-compose up -d
```

Then you can tracking APP by:

```shell
docker-compose logs -f
```

* You want to restart some part of our APP? Try to attach some service name when using up, start, stop etc.:

```shell
# Restart the ServiceController and DB (MySQL) module
docker-compose restart service-controller db
```

Until now, there are four services in total:

1. **aurora-ws**: The Rails APP, serve the WEB Service.

2. **service-controller**: The Circuit Simulation service, mainly powerd by Java.

3. **db**: We use the MySQL5.7 to serve our data storage.

4. **cache**: We use the Redis3.2 to serve our data cache.

## Advanced

* [Doker and Continuous Integration]

[Docker Home]: (https://www.docker.com/products/docke)
[Doker and Continuous Integration]: https://github.com/CloudEDA/AuroraPlatform/wiki/Doker-and-Continuous-Integration
