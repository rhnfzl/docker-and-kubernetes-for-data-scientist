# Basics

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
1. Delete stopped container using the `docker rm <container name>` command.
2. Confirm container is not listed when we do a `docker ps -a`.

## E: Shell into container
1. Override the default container launch command by passing in parameters when we create a container using [`docker run`](https://docs.docker.com/engine/reference/commandline/run).

# Essentials

1. Change  a directory on your local machine.

```cd 01-hello-world```

2. Create a python file that prints "Hello World" and save it as `hello_world.py`
```python hello_world.py```

3. In the same folder, create a `Dockerfile` (filename `Dockerfile`) with the following contents:

```Dockerfile
# Dockerfile

# Use latest Python runtime as base image
FROM python:3.6.5-alpine3.7

# Set the working directory to /app and copy current dir
WORKDIR /app
COPY . /app

# Run hello_world.py when the container launches
CMD ["python", "hello_world.py"]
```

4. Use `docker build -t hello-world .` to build an image from a `Dockerfile` located in the current directory with the tag, `hello-world`.

5. Create a new container using `docker run hello-world`. You should see a `Hello World` message printed to the console.

6. Look at all stopped containers using `docker ps -a`. Note the `container-name` or `container-id` of the image.

7. Restart the image using `docker start -ia [container-name OR container-id]`. `Hello World` will be printed to the console once again.

8. Delete the container:

```docker rm [container-name OR container-id]```

9. Delete the image:

```docker rmi [image-name (Repository) OR image-id]```

10. Confirm image has been deleted using `docker images`




