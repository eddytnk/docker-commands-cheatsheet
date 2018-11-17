# docker-commands-cheatsheet
Cheat sheet  commands used when working with Docker 

### To desplay all images found on your local machine
`docker images`

### To start a container from an images (e.g from a busybox images and run a command in the container)

`docker run <image>:<tag> <any command you wish to execute in that container when it is stated>`

Example: `docker run busybox:1.29 echo "Hello World!"`

### To start a container from an images (e.g from a busybox images and run a command in the container) in the Background

`docker run -d <image>:<tag> <any command you wish to execute in that container when it is stated>`

### To show all runing containers
`docker ps`

### To show all containers that has previously run
`docker ps -a `

### To go into the container in an interactive mode

`docker run -i -t <image-name or image-id> ` OR  `docker run -it <image-name or image-id> `


### To start and remove the container when it finished run

`docker run --rm <image>:<tag> <any command you wish to execute in that container when it is stated>`
