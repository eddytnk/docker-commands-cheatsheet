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

### To run a command in a running container

`docker exec -it <container-id> <specify the command to run>`

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

Dockerfile is a text file that contains all the instructions users provide to assemble a docker image. Each instruction will create a new layer to the image. 

A Dockerfile must not have any extension and must be name `Dockerfile`

### How to write instruction in the Dockerfile

The first instruction must be a specification of the base image e.g 


```
FROM debian:jessie

```

The next instruction must be the RUN command to execute when building the image is started


```
FROM debian:jessie
RUN apt-get update
RUN apt-get install -y git
```
### Building the docker image with docker build command

Save your Dockerfile and open the terminal to the directory of the Dockerfile.

specify the docker build command

`docker build -t <repository-name>:<tag> <path-to-Dockerfile>`

Example `docker build -t eddytnk/debian:1.00 .`  

`dot (.)` because I am in the current directory of my Dockerfile 


## More on dockerFile
You can specify one RUN command with multiple instruction

```
FROM debian:jessie
RUN apt-get update && apt-get install -y \
    git \
    python\
    vim 
```
### CMD Instruction 

You can specify the CMD instruction using a Dockerfile. CMD Instruction is the instruction that runs when the container is started. If you don't specify the CMD instruction in the Dockerfile, docker will use the default command defined in the based image.

For debian:jessie, the default command is bash.

Remember, the CMD instruction does NOT run when building the image, it only runs when the container starts up.

Example:

```
FROM debian:jessie
RUN apt-get update && apt-get install -y \
    git \
    python\
    vim 
CMD ["echo", "Hello Word!"]
```

### COPY Instruction

The COPY instruction copies new files and directory from the  build context and add them to the file system of the container.

```
FROM debian:jessie
RUN apt-get update && apt-get install -y \
    git \
    python\
    vim 
COPY myfile.txt /src/myfile.txt
```

The example Dockerfile will copy `myfile.txt` into `/src/myfile.txt` after the container is started

### ADD Instruction

Simillar to COPY instruction but ADD allows you to download a file from the internet and copy to the conatiner when it is started.

ADD can automatically unpack compressed file


## How to push images to Docker Hub (Docker Registry)

if you wish to change your image repository name and tag name

`docker tag <image-id> <new-image-name>:<tag>`

Remember to use `docker images` to get your image-id.

To push your image to docker hub your first need to login to docker hub using:

`docker login --username=<docker-hub-id> ` then provide your password.

then you do:
`docker push <repository-name>:<tag>`

Example: `docker push eddytnk/debian:1.00`