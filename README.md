# Jenkins custom Docker image with docker

This is a customization of the official Jenkins Docker image with Docker installed.

## Usage
The idea behind this custom image is to have Jenkins access the Docker host server through the `/var/run/docker.sock` file.

First, here is how to start the image properly, exposing the correct ports and setting the correct volumes:

```shell
docker run -v <home_folder>:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 -p 50000:50000 <jenkins custom image name>:<tag>
```

Because we use the same Docker server (the one from the host) we need to match the id of the `docker` group from the host to the one inside the custom image. Look into your `/etc/group` file for the `docker` group id:

    docker:x:789:user1,user2

For your convenince, there is a build argument defined for the `docker` group, called `DOCKER_GROUP_ID`. When you build the image, set the correct value using `--build-arg DOCKER_GROUP_ID=<your group id>`

In order to build the image, navigate to `jenkins-docker` folder and run

```shell
docker build --build-arg DOCKER_GROUP_ID=789 . -t jenkins-docker:stable
```

## Starting via docker-compose

For your convenience, there is also a docker-compose yaml file included in the project.
After you build the `jenkins-docker:stable` image locally, just run docker compose using:

    docker-compose up

