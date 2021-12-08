# Docker and Kubernetes for data scientist

---

## DOCKER

> What Docker does?
	>> It standardises the Einvironment
	>> Build once and deploy it anywhere
	>> Isolation using virtualization where resources are shared
	>> Portbility helps to switch to different einvironment

WSGI : Web Server Gateway Interface

DockerHUb has Images

> Difference Between Container and Image
	>> Container is a running environment for Image
	>> Container provides the application image, port binding, virtual file system
	
	
### Docker Commands

* ```docker pull <image name>``` : To pull the docker image
* ```docker images``` : To see the docker images```
* ```docker ps``` : list which dockers are running and obtain the container id
* ```docker run <image name>``` : To run the image as well as can be used for first time to download and run
* ```docker run <image name>:<version number>``` : pull and start a image with specific version number
* ```docker run -d <image name>``` : start a container in detach mode
* ```docker stop <contianer id>``` : to stop the specific container
* ```docker start <contianer id>```: to start the container with the same contianer id
* ```docker ps -a``` : lists which docker is running and not running, so stopped docker can be restarted from the contaoner id from here

> *Concept: * Container Port vs Host Port : 
	>> Multiple container can run on a host (laptop/pc). 
	>> Host has certain ports available that can be opened for certain applications.
	>> Conflict would arise when same port is used by two different conatiners.
	>> So it is essential to create binding between the host and the container with different port number such that it should be able comunicate with the application without any interferance.
	>> Host will know how to redrect to the conatiner when host binding is applied
	
* ```docker run -p<self defined port number for host>:<container port> <image name>``` : to bind the host port to container port ```docker ps -a``` could be used to see the port information.





	



