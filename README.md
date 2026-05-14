## Docker cheatsheet 

### Login to a registery
```bash
# you need to create a registery account ex. dockerhub
docker login 
docker logout

```

### Handling images 
```bash 
# search for image
docker search redis

# search with a filter 
docker search --filter stars=3 --no-trunc redis

# pull known images 
docker pull redis   

# pull user images 
docker pull username/image
docker pull alaaatwa/ssh-machine  

# push image to your registery 
docker push name/image 
docker push alaaatwa/ssh-machine 

```

### Handling Containers 
```bash 
# create a container [ but don't start it]
docker container create -it --name alpine-machine alpine 

# start a container 
docker start alpine-machine 

# docker run == create + start the container 
docker run -it --name alpine-machine alpine 
# -it == interactive shell 

# seletc the interactive shell 
docker run -it --name alpine-machine alpine /bin/bash 

# stop container 
docker stop alpine-machine 

# show running containers 
docker ps 

# show running containers including stopped 
docker ps -a 

# rename a container 
docker container rename alpine-machine myalpine 

# remove a container 
docker rm alpine-machine 

# force remove a running container 
docker rm -f alpine-machine 

# show resource usage of running containers 
docker stats 
docker stats alpine-machine 

# update a container 
# limiting the cpu and memory usage.
docker container update --cpus 2 --memory 512M 

# update the restart policy 
docker container update --restart always nginx

# interact with a running container (you can use sh instead)
docker exec -it alpine-machine /bin/bash 

# restart a container 
docker restart alpine-machine

# pause or unpause a container 
docker pause alpine-machine 
docker unpause alpine-machine 

# wait for a container to stop
docker cotainer wait alpine-machine 

# killing a container (for unresponsive containers)
docker container kill alpine-machine 

# show container logs (-f for live logs)
docker logs alpine-machine 
docker logs alpine-machine -f 

# inspect a container (useful command for any resource)
docker inspect alpine-machine 

# show used ports by container 
docker container port alpine-machine 

# show running processes (resources) by a container 
docker container top alpine-machine 

# removing a container with its volume 
docker rm -v nginx 

# remove all stopped containers 
docker container prune 

# remove all containers including running 
docker rm -f $(docker ps -aq)


```

### Handling Images 
```bash 
# list images 
docker images 

# build image from a Dockerfile (in the current directory)
docker build -t <image-name> .  

# build image with a different file 
docker build -t <image-name> -f anotherDockerfile .

# remove image 
docker rmi alpine

# force remove image (if containers still using it)
docker rmi -f alpine 

# show image history 
docker image history alpine-image 

# archive an image 
docker image save alpine > alpine.tar 

# building image from a container 
docker commit alpine-machine 

# building with author 
docker commit -a alaaatwa alpine-machine 

# tag image 
docker tag alpine-machine alaaatwa/alpine-machine 

# push image (configure your registery first with docker login)
docker push alaaatwa/alpine-machine 

# remove dangling images 
docker rmi $(docker images -qf dangling=true)

# remove all images 
docker rmi -f $(docker images -aq)

# remove all unused images without the risk of force "deletion"
docker image prune -a 

# remove all unused resources (images, containers, networks, and volumes)
docker system prune -f

# clean all 
docker system prune -a 

# clean with a filter 
docker system prune --filter "until=24h"

```

### Docker Networking 
```bash 

# create a custom bridge network (most common)
docker network create mynet 

# list networks 
docker network ls 

# connect containers to your network 
docker run -d --name app --network mynet nginx 
docker run -d --name db --network mynet mysql

# create isolated containers using "none" network
docker run --network none nginx 

# expose a container to your machine 
docker run -d -p 8080:80 nginx 

# inspect a network 
docker inspect mynet 

# connect / disconnect containers 
docker network connect mynet alpine-machine 
docker network disconnect mynet alpine-machine 

# docker-compose 
# docker compose creates a default network automatically for its services.

# creating a custom network with a custom subnet 
docker network create --subnet 192.168.1.0/24 mynet 

# creating a network with a different type (overlay,..)
docker network create -d overlay mynet 

# remove a network 
docker network rm mynet 


```
### docker compose 
```bash 

# up 
docker compose up -d 

# compose from a different file 
docker compose -f docker-compose.yml up 

# edit configs
docker compose config 

# list services or volumes 
docker compose config --services 
docker compose config --volumes 

# down with removing volume 
docker compose down  -v 

# show lgos 
docker compose logs 

# show running services 
docker compose ps 

# execute shell 
docker compose exec app sh 

# rebuild without cache 
docker compose build --no-cache 

# restart services
docker compose restart 

# show running processes 
docker compose top 

# execute a shell inside the service.
docker compose exec web bash 

# scale compose 
docker compose up --scale web=3  

# remove images 
docker compose down --rmi all

```
