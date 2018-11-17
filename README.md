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


