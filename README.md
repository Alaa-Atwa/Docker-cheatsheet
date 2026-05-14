# Docker Cheatsheet

## Table of Contents
- [Login to a registry](#login-to-a-registry)
- [Handling images (pull/push/search)](#handling-images-pullpushsearch)
- [Handling containers](#handling-containers)
- [Handling images (build/remove)](#handling-images-buildremove)
- [Docker networking](#docker-networking)
- [Docker compose](#docker-compose)

---

## Login to a registry

#### Login
```bash
docker login
```

#### Logout
```bash
docker logout
```

> You need to create a registry account (e.g., Docker Hub)

---

## Handling images (pull/push/search)

#### Search for an image
```bash
docker search redis
```

#### Search with filters
```bash
docker search --filter stars=3 --no-trunc redis
```

#### Pull official images
```bash
docker pull redis
```

#### Pull user images
```bash
docker pull username/image
docker pull alaaatwa/ssh-machine
```

#### Push image to registry
```bash
docker push name/image
docker push alaaatwa/ssh-machine
```

---

## Handling containers

#### Create a container (without starting)
```bash
docker container create -it --name alpine-machine alpine
```

#### Start a container
```bash
docker start alpine-machine
```

#### Create and start a container
```bash
docker run -it --name alpine-machine alpine
```

#### Run with interactive shell
```bash
docker run -it --name alpine-machine alpine /bin/bash
```

#### Stop container
```bash
docker stop alpine-machine
```

#### Show running containers
```bash
docker ps
```

#### Show all containers
```bash
docker ps -a
```

#### Rename a container
```bash
docker container rename alpine-machine myalpine
```

#### Remove a container
```bash
docker rm alpine-machine
```

#### Force remove a running container
```bash
docker rm -f alpine-machine
```

#### Show resource usage
```bash
docker stats
docker stats alpine-machine
```

#### Update container resources
```bash
docker container update --cpus 2 --memory 512M alpine-machine
```

#### Update restart policy
```bash
docker container update --restart always alpine-machine
```

#### Execute command inside running container
```bash
docker exec -it alpine-machine /bin/bash
```

#### Restart container
```bash
docker restart alpine-machine
```

#### Pause and unpause container
```bash
docker pause alpine-machine
docker unpause alpine-machine
```

#### Wait for container to stop
```bash
docker container wait alpine-machine
```

#### Kill container
```bash
docker container kill alpine-machine
```

#### Show logs
```bash
docker logs alpine-machine
docker logs -f alpine-machine
```

#### Inspect container
```bash
docker inspect alpine-machine
```

#### Show container ports
```bash
docker container port alpine-machine
```

#### Show running processes in container
```bash
docker container top alpine-machine
```

#### Remove container with volumes
```bash
docker rm -v nginx-container
```

#### Remove all containers
```bash
docker rm -f $(docker ps -aq)
```

---

## Handling images (build/remove)

#### List images
```bash
docker images
```

#### Build image from Dockerfile
```bash
docker build -t <image-name> .
```

#### Build using a different Dockerfile
```bash
docker build -t <image-name> -f anotherDockerfile .
```

#### Remove image
```bash
docker rmi alpine
```

#### Force remove image
```bash
docker rmi -f alpine
```

#### Show image history
```bash
docker image history alpine-image
```

#### Save image to archive
```bash
docker image save alpine > alpine.tar
```

#### Create image from container
```bash
docker commit alpine-machine
```

#### Add author when committing
```bash
docker commit -a alaaatwa alpine-machine
```

#### Tag image
```bash
docker tag alpine-machine alaaatwa/alpine-machine
```

#### Push image
```bash
docker push alaaatwa/alpine-machine
```

#### Remove dangling images
```bash
docker rmi $(docker images -qf dangling=true)
```

#### Remove all images
```bash
docker rmi -f $(docker images -aq)
```

#### Remove unused images
```bash
docker image prune -a
```

#### Remove unused resources
```bash
docker system prune -f
```

#### Remove everything unused
```bash
docker system prune -a
```

#### Cleanup with filter
```bash
docker system prune --filter "until=24h"
```

---

## Docker networking

#### Create a bridge network
```bash
docker network create mynet
```

#### List networks
```bash
docker network ls
```

#### Run containers in a network
```bash
docker run -d --name app --network mynet nginx
docker run -d --name db --network mynet mysql
```

#### Run container with no network
```bash
docker run --network none nginx
```

#### Expose container port
```bash
docker run -d -p 8080:80 nginx
```

#### Inspect network
```bash
docker inspect mynet
```

#### Connect and disconnect containers
```bash
docker network connect mynet alpine-machine
docker network disconnect mynet alpine-machine
```

#### Create network with subnet
```bash
docker network create --subnet 192.168.1.0/24 mynet
```

#### Create network with specific driver
```bash
docker network create -d overlay mynet
```

#### Remove network
```bash
docker network rm mynet
```

---

## Docker compose

#### Start services
```bash
docker compose up -d
```

#### Use a specific compose file
```bash
docker compose -f docker-compose.yml up
```

#### Validate configuration
```bash
docker compose config
```

#### List services and volumes
```bash
docker compose config --services
docker compose config --volumes
```

#### Stop and remove with volumes
```bash
docker compose down -v
```

#### Show logs
```bash
docker compose logs
```

#### Show running services
```bash
docker compose ps
```

#### Execute command in service
```bash
docker compose exec app sh
```

#### Build without cache
```bash
docker compose build --no-cache
```

#### Restart services
```bash
docker compose restart
```

#### Show processes
```bash
docker compose top
```

#### Execute shell in service
```bash
docker compose exec web bash
```

#### Scale services
```bash
docker compose up --scale web=3
```

#### Remove images
```bash
docker compose down --rmi all
```
