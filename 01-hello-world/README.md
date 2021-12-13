# Hello World Example

## A: Pull Image from Docker Hub

1. Start by pulling an image from DockerHub to our local machine using the [`docker pull`](https://docs.docker.com/engine/reference/commandline/pull/) command.

```docker pull python:3.6.5-alpine3.7```

2. Take a look at all images on the system using [`docker images`](https://docs.docker.com/engine/reference/commandline/images/) command.

## B: Create Container

> We can create containers from an image.

1. Look at the [Dockerfile](https://github.com/docker-library/python/blob/b99b66406ebe728fb4da64548066ad0be6582e08/3.6/alpine3.7/Dockerfile) for the image pulled, it will run `python3` when a container is created.

```docker run -it python:3.6.5-alpine3.7```

2. Use `Ctrl + P + Q` to detach from the container and return to your prompt.

## C: Stop Container

> Detaching from the container means it is still running in the background.

1. Look at all running container using the [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps) command. Use `docker ps -a` to view all stopped containers.

2. Use [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) with your container name to stop the container.

```docker stop <container name>```

3. Confirm container has stopped using `docker ps -a`.

## D: Delete Container

1. Delete stopped container using the `docker rm <container name>` command:

2. Confirm container is not listed when we do a `docker ps -a`.

## E: Shell into container

1. Override the default container launch command by passing in parameters when we create a container using [`docker run`](https://docs.docker.com/engine/reference/commandline/run)






