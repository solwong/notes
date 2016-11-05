<!-- # Doker - Continuous Integration -->

## Continuous Integration

**1. Source and system dependency commit**

The Operations Engineer should test the new environment system and stored it into Dockerfile file and tag a new version to the docker-compose.yml file, which are all in the home directory of project. Then these new Docker file will be released with new source together.

**2. Rebuild Docker Images automatically**

So, after new version has been committed, the Webholk can effect that the Docker Hub will rebuild the images with new system dependency and source.

**3. Up a new Docker Container**

While the new version released, engineers could pull the new source of repo, then the `docker-compose up` will check the docker-compose.yml file, when the tag changed, it will down pull the new images, which rebuild automatically by Docker Hub.

At last, although the system dependency changed, the engineers should do nothing but get a new environment, and the environment is consistent with others.


## Advanced

### Why use Docker for deploy?

#### What is Docker

> Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries – anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

To get more, please go to [https://www.docker.com/]

#### Docker help us

- **Eliminate the differences in a variety of environments.** Whatever system you are using, Windows, Linux or macOS, Docker will give you a consistent environment like the VM does, but more lightweight than VM.

- **Reduce the dependency and damage of system components.** Docker divides your complex project into some service([Docker Compose Service]), there Service run in a sandbox like a green software, even a complex WEB service.

- **Continuous integration through the cooperation of Docker Hub and GitHub or Bitbucket.**

### When need rebuild Docker Image

#### Production environment

In production environment, the Docker Images need to be update when system dependency and source changed. It sounds terrible, but if you know the principle of Docker Images, it won't make you feel bad, And the principle of container tell us this is more appropriate in your production environment.

#### Development environment

When you using a Docker environment for development, it is also cool that you can get the problem earlier because of the consistent environment.

But you just need rebuild Docker Images when the system dependency changed by the help of Docker Volume. And just one engineer should do it(rebuild), than other engineers could update the images through a command `docker pull ...`, because the system dependency are all stored by the Dockerfile file.




[https://www.docker.com/]: https://www.docker.com/
[Docker Compose Service]: https://docs.docker.com/compose/overview/
