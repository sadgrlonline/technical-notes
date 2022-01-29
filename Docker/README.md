# Docker

```shell
# check available containers (& see container ids)
docker ps -a

# re-compose 
docker-compose up -d

# enter a running docker container
docker exec -u 0 -it [imageID] /bin/bash

# kill all docker containers
docker kill $(docker ps -q)

# remove all docker containers
docker rm $(docker ps -a -q)

# commit change from running container
sudo docker commit [imageID] image-name

# reload nginx from within a running container
docker container exec [imageID] nginx -s reload

```