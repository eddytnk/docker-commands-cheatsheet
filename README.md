# docker-commands-cheatsheet
Cheat sheet  commands used when working with Docker 

### To desplay all images found on your local machine
`docker images`

### To start a container from an images (e.g from a busybox images and run a command in the container)

`docker run <image>:<tag> <any command you wish to execute in that container when it is stated>`

Example: `docker run busybox:1.29 echo "Hello World!"`

### To start a container from an images (e.g from a busybox images and run a command in the container) in the Background (detached mode)

`docker run -d <image>:<tag> <any command you wish to execute in that container when it is stated>`

### To show all runing containers
`docker ps`

### To show all containers that has previously run
`docker ps -a `

### To go into the container in an interactive mode

`docker run -i -t <image-name or image-id> ` OR  `docker run -it <image-name or image-id> `


### To start and remove the container when it finished run

`docker run --rm <image>:<tag> <any command you wish to execute in that container when it is stated>`

### To inspect a runnung container in detached mode 

Recall that when you runa container in detached mode by specifying `-d` the terminal returns to us the running container's id. To inspect this container:

`docker inspect <container-id>`

This inspection gives us information about the container like IP address, MAC address, image id, log path, status etc

### To run an image like Tomcat and expose it to the host in another port

Recall that tomcat image runs by default in port 8080 in the container. to expose tomcat to the hosting OS in port 8888 we used:

`docker run -it -p <host-port>:<conatiner-port> tomcat:9.0` 

Example: `docker run -it -p 8888:8080 tomcat:9.0` 

After running the above command, go to your browser and run `http://host-ip-address:8888` it should take you to the tomcat server runing in your docker container

### To see the logs of a running container

`docker logs <container-id>`

### To check the full set of image layers that make up an image

`docker history <image>:<tag>`


## How to create a custom docker image using docker commit

In this section, 
1. We will pull and run the debian image from docker repository (docker hub) 
2. We will install git into the the runing container. 
3. Finally we will package/commit this container into a new docker image. 

The idea of the have debain image with git installed.

Let's get started

We will pull and run the debian image from docker 

`docker run -it debian:jessie`

We will install git into the the runing container. In the interactive mode install git using:

`apt-get update && apt-get install -y git`

Finally we will package/commit this container into a new docker image. 

`docker commit <container-id> <repository-name>:<tag>`

Remember to get `container-id` use `docker ps -a` and select the container id of the debain conatiner 

The `repository-name` is the username of the docker registry/new-image-name e.g `eddytnk/debian`

You can now start a container based on this new image. 
Example: `docker run -it eddytnk/debian:1.00`


## How to create a custom docker image using Dockerfile



