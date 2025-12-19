# Docker - Images-Containers

# Images vs Containers

https://youtu.be/pg19Z8LL06w

# Docker images / containers


# See a list of docker images/containers

## Images

Active images
```cmd
docker images
docker image ls
docker images -a
```

* https://devconnected.com/how-to-list-docker-images/
## Containers

Show active containers
```cmd
sudo docker ps
```

Show all containers
```cmd
sudo docker ps -a
sudo docker ps -all
```


* https://spacelift.io/blog/docker-list-containers



# Remove docker images/containers

## Images


```cmd
docker rmi image hello-world
docker image rm -f hello-world
```

* https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes
## Containers

**Active containers**
```cmd
docker rm ID_or_Name ID_or_Name
```

https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

**Remove all stopped containers**
```cmd
docker container prune
```


# Docker images

## Build an image out of a Dockerfile

Current directory

```cmd
sudo docker build -t my_image .
```

other
```cmd
sudo docker build -t my-app:1.0
sudo docker build -t my-app:version1 .
```


## Reference
* https://youtu.be/WmcdMiyqfZs?t=720



# Docker containers

## Create a Docker container from Dockerfiles

Build the image from a dockerfile
```cmd
sudo docker build -t <image-name> .
```


Docker compose
 * Dockerfile
```cmd
sudo docker compose up --build
sudo docker run -p 8888:8000 <image-name>
```



## Run a image as container
```cmd
sudo docker run hello-world
```


## Run a image as container with terminal
```cmd
sudo docker run -it hello-world
```

## Stop/ start container
```cmd
sudo docker container stop hello-world
sudo docker container start hello-world
```


# REFERENCES

## YouTube

* Docker Crash Course for Absolute Beginners: https://youtu.be/pg19Z8LL06w
	* Docker Crash Course for Absolute Beginners NEW: https://youtu.be/pg19Z8LL06w
* Docker Tutorial for Beginners -FULL COURSE in 3 Hours -: https://youtu.be/3c-iBn73dDE
* What is Docker in 5 minutes: https://youtu.be/_dfLOzuIg2o
* 100+ Docker Concepts you Need to Know: https://youtu.be/rIrNIzy6U_g
* Docker With Django Tutorial | How To Dockerize A Django Application (Beginners Guide): https://youtu.be/BoM-7VMdo7s
* Docker for Robotics Pt 1 - What and Why?? https://youtu.be/XcJzOYe3E6M?list=PLunhqkrRNRhaqt0UfFxxC_oj7jscss2qe