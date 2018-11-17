# docker-commands-cheatsheet
Cheat sheet  commands used when working with Docker 

### To desplay all images found on your local machine
`docker images`

### To start a container from am images (e.g from a busybox images and run a command in the container)

`docker run <images>:<tag> <any command you wish to execute in that container when it is stated>`

Example: `docker run busybox:1.29 echo "Hello World!"`

### To go into the container in an interactive mode

`docker run -i -t <image-name or image-id> ` OR  `docker run -it <image-name or image-id> `

