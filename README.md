# Docker for Data Scientist

## DOCKER

> What Docker does? <br />
>> * It standardises the Einvironment. <br />
>> * Build once and deploy it anywhere. <br />
>> * Isolation using virtualization where resources are shared. <br />
>> * Portbility helps to switch to different environments. <br />

<!-- This is commented out.
WSGI : Web Server Gateway Interface
DockerHUb has Images -->

* Docker container images can be downloaed from [DockerHub](https://hub.docker.com/). It is a public [registry](https://docs.docker.com/registry/) where you can find and download Docker images.

> Difference Between Container and Image
>> * Container is a running environment for Image. <br />
>> * Container provides the application image, port binding, virtual file system. <br />
>> * Docker images are read-only templates used to build containers and Containers are deployed instances created from those templates. <br />
>> * Running Instance of an Image is called Container. <br />

### Resource Used

* [Docker Tutorial for Beginners](https://youtu.be/3c-iBn73dDE)
* [Docker for Data Science](https://youtu.be/jbb1dbFaovg) and the [GitHub Repo](https://github.com/docker-for-data-science/docker-for-data-science-tutorial)


Docker File -build-> Dokcer Image -run-> Container
						|		|
						Push	Pull
						|		|
						Docker Registry
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
	* ```VOLUME``` /mounted_dir : mount point for external volumes, although need -v flag to connect
	* ```EXPOSE``` 8888 : Make port 8888 available to outside world, again need -p flag to connect
		
> [Best Practices of Dockerfile](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
		
#### Configuring Dockerfile at Runtime

* ENTRYPOINT : configures container to run as executable
* CMD : provides default for executing container
	* CMD and ENTRYPOINT interation
* Two forms:
	* Shell ```CMD python hello-world.py```
	* Exec (preferred) ```CMD ["python", "hello-world.py"]```
	
* [Example Hello World Dockerfile](/01-hello-world/Dockerfile)

#### Docker Commands

##### --Lifecycle--

###### For Containers

* ```docker create```
* ```docker rename```
* ```docker run ``` : To run the image as well as can be used for first time to download and run, It has multiple [options](https://docs.docker.com/engine/reference/commandline/run/#options)
	* ```docker run :``` : pull and start a image with specific version number
	* ```docker run -d <image name>``` : starts a container in detach mode which lets to use the terminal again
	* ```docker run -d -p<host port>:<docker port> --name <coustom docker name> <image name>``` : to run the docker with specific name
	* ```docker run -v /full/local/path:/mounted_dir``` : "host path : container path" adding volume to the container
* ```docker rm```
* ```docker update```

###### For Images

* ```docker images``` : to see the docker images
* ```docker import```
* ```docker build```
	* ```docker build -t hello-world:0.0.1 .``` : to build the images from the docker file, -t tags the image, "hello-world:0.0.1" tag name and version and "." sets the current directory.
* ```docker commit```
* ```docker rmi <image id>``` : to remove docker image
* ```docker load```
* ```docker save```

##### --Info--

###### For Containers
* ```docker ps``` : list which containers are running and obtain the container id
* ```docker ps -a``` : lists which docker is running and not running, so stopped docker can be restarted from the container id from here
* ```docker logs``` 
* ```docker inspect``` 
* ```docker events``` 
* ```docker portdocker top``` 
* ```docker stats``` 
* ```docker diff``` 

###### For Images

* ```docker history```
* ```docker tag```

##### --Misc (Containers)--

* ```docker cp```
* ```docker export```
* ```docker exec```

##### --Start/Stop (Containers)--
* ```docker stop <container name/ container id>``` : to stop the specific container
* ```docker start <container name/ container id>```: to start the container with the same container id
* ```docker start -ia <container name/ container id>``` : -i to make standard interacive -a to connect standard out and error
* ```docker restart```
* ```docker pause```
* ```docker unpause```
* ```docker wait```
* ```docker kill```
* ```docker attach```

Difference between the docker run and docker start is, docker run lets to start the new instance of the conatainer whereas the docker start lets to re-start the stopped container.

##### --Registry (Images)--
* ```docker pull <image name>``` : to pull the docker image e.g : ```docker pull python:3.6.5-alpine3.7```
* ```docker push```
* ```docker login```
* ```docker logout```
* ```docker search```


* [Options] : command line argurments
	* -d : Detached, i.e. the container would run in the background
	* -a : Attach to STDOUT/STDERR
	* -i : Running the image InteractiveLY (keeps STDIN open)
	* -t : To run bash inside the docker container created
	* -p : Connect/publish the container ports to host.
	* -v : adding data volume to the container
	* --name [NAME] : set the container name
	
* [COMMAND]
	* Can pass in parameter or ```bin/```

#### Docker Host
> *Concept: * Container Port vs Host Port : <br />
>> * Multiple containers can run on a host (laptop/pc).??<br />
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

#### Docker Container Lifecycle

> Conception
* ```BUILD``` an image from a Dockerfile
> Birth
* ```RUN``` (create+start) a container
> Reporoduction
* ```COMMIT``` (persist) a container to a new image
* RUN a new container from an image
> Sleep
* ```KILL``` a running contaoner
> Wake
* ```START``` a stopped container
> Death
* ```RM``` (delete) a stopped container
> Extinction
* ```RMI``` a container image (delete image)

#### Docker Projects 

* Simulation of [Proactive-BPM-Adaptation-via-Online-Reinforcement-Learning](https://github.com/rhnfzl/simulation-proactive-bpm-adaptation) was performed using docker image provided by the author of the paper.


## Addtional Resources

[Docker Labs](https://github.com/docker/labs) and [also this](https://notes.hamel.dev/docs/docker/Docker-In-Action.html) <br />
[How Docker Can Help You Become A More Effective Data Scientist](https://towardsdatascience.com/how-docker-can-help-you-become-a-more-effective-data-scientist-7fc048ef91d5) <br />
[A Step Towards Reproducible Data Science : Docker for Data Science Workflows](https://www.analyticsvidhya.com/blog/2017/11/reproducible-data-science-docker-for-data-science/) <br />
[Docker Deep Dive](https://www.pluralsight.com/courses/docker-deep-dive-update?aid=7010a000002BWqGAAW&promo=&utm_source=non_branded&utm_medium=digital_paid_search_google&utm_campaign=EMEA_Dynamic&utm_content=&gclid=Cj0KCQiA5OuNBhCRARIsACgaiqX-TqDP6FX1ez8QxMiBOUZ9QmXEdtH9gHT9Lq8zDHvki3ZfGDAsm-AaAh1lEALw_wcB) <br />
[Docker for Data Science ??? A Step by Step Guide](https://dagshub.com/blog/setting-up-data-science-workspace-with-docker/) <br />
[Docker for data science](https://medium.com/analytics-vidhya/docker-for-data-science-442299c5203c) <br />


 




	



