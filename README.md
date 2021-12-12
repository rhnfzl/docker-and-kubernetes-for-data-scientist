# Docker and Kubernetes for data scientist

---

## DOCKER

> What Docker does? <br />
>> * It standardises the Einvironment. <br />
>> * Build once and deploy it anywhere. <br />
>> * Isolation using virtualization where resources are shared. <br />
>> * Portbility helps to switch to different environments. <br />

<!-- This is commented out.
WSGI : Web Server Gateway Interface
DockerHUb has Images -->

* Docker container images can be downloaed from [DockerHub](https://hub.docker.com/)

> Difference Between Container and Image
>> * Container is a running environment for Image. <br />
>> * Container provides the application image, port binding, virtual file system. <br />
>> * Docker images are read-only templates used to build containers and Containers are deployed instances created from those templates. <br />

### Resource Used

* [Docker Tutorial for Beginners](https://youtu.be/3c-iBn73dDE)
* [Docker for Data Science](https://youtu.be/jbb1dbFaovg)

---

### Dockerfile

* File containing all commands used to assemble image
* Automated build
* Stucture of Dockerfile Commands
	* ```FROM``` : sets base image
	* ```LABEL``` : add metadata to image
		* MAINTAINER is depreciated
		* LABEL maintainer="Rehan <rehanfazal@live.com>" 
	* ```COPY``` : copies files / directories into image
		* .dockerignore
	* ```ENV``` : sets environment variables
	* ```WORKDIR``` : sets working directory
	* ```RUN``` : executes shell commands in a new layer
		* ```RUN pip install jupyter``` <br />
		```RUN pip install pandas``` : 2 layers
		* ```RUN install jupyter && \``` <br />
		```RUN install pandas``` : 1 layer (best practice)
		
> [Best Practices of Dockerfile](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
		
#### Configuring Dockerfile at Runtime

* ENTRYPOINT : configures container to run as executable
* CMD : provides default for executing container
	* CMD and ENTRYPOINT interation
* Two forms:
	* Shell ```CMD python hello-world.py```
	* Exec (preferred) ```CMD ["python", "hello-world.py"]
	
<!-- ##### Example Hello World Dockerfile -->

#### Docker Commands

* ```docker pull <image name>``` : to pull the docker image e.g : ```docker pull python:3.6.5-alpine3.7```
* ```docker images``` : to see the docker images
* ```docker rmi <image id>``` : to remove docker image
* ```docker ps``` : list which dockers are running and obtain the container id
* ```docker run ``` : To run the image as well as can be used for first time to download and run
* ```docker run :``` : pull and start a image with specific version number
* ```docker run -d <image name>``` : starts a container in detach mode which lets to use the terminal again
* ```docker run -d -p<host port>:<docker port> --name <coustom docker name> <image name>``` : to run the docker with specific name
* ```docker stop <container name/ container id>``` : to stop the specific container
* ```docker start <container name/ container id>```: to start the container with the same container id
* ```docker start -ia <container name/ container id>``` : -i to make standard interacive -a to connect standard out and error
* ```docker ps -a``` : lists which docker is running and not running, so stopped docker can be restarted from the container id from here

* [Options]
	* -d : Detached (runs in background)
	* -a : Attach to STDOUT/STDERR
	* -i : Interactive (keeps STDIN open)
	* -t : Allocates pseudo-TTY
	* --name [NAME] : set the container name
	
* [COMMAND]
	* Can pass in parameter or ```bin/

Difference between the docker run and docker start is, docker run lets to start the new instance of the conatainer whereas the docker start lets to re-start the stopped container.

#### Docker Host
> *Concept: * Container Port vs Host Port : <br />
>> * Multiple containers can run on a host (laptop/pc). <br />
>> * Host has certain ports available that can be opened for certain applications. <br />
>> * Conflict would arise when the same port is used by two different containers. <br />
>> * So it is essential to create a binding between the host and the container with different port numbers such that it should be able to communicate with the application without any interference. <br />
>> * Host will know how to redirect to the container when host binding is applied. <br />
	
* ```docker run -p<self defined port number for host>:<container port> <image name>``` : to bind the host port to container port ```docker ps -a``` could be used to see the port information.

#### Debugging Docker

* ```docker logs <container id>``` or ```docker logs <docker name>```: to see the logs for the docker
* ```docker exec -it <container id> /bin/bash``` : to open the interactive command inside the container can also be used to export the data out from the container, exit out pf container by using ```exit``` command, see the einvironmental variables using ```env```.

* ```docker network ls``` : to see the docker network
* ```docker network create <network name>``` : to create network

#### Docker Compose

A structured way to store docker comments in ```.yaml``` file. Docker Compose take cares of creating a common Network.

#### Docker Projects 

* Simulation of [Proactive-BPM-Adaptation-via-Online-Reinforcement-Learning](https://github.com/rhnfzl/simulation-proactive-bpm-adaptation) was performed using docker image provided by the author of the paper.




 




	



