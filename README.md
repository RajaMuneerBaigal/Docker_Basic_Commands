# Docker_Basic_Commands

## Some important Docker Concepts/Terminalogies 

## Difference between Image and Container
- Image is an artifact that can be moved across different containers. Image has layers and it can be stored in a private or public repository.All the artifacts inside a docker hub are images. We have several versions of different images which we can used as our application dependencies rely upon.

- Container is actually a running environment for an image. Container has environment configurations, applications images and file systems all in one place.A container has a port binded to it which makes it possible to talk to an application running inside of a container

## Difference between Virtual Machine and Docker

- Both are virtualization technologies. Virtual machine utilizes both the layers of Operation system(kernel and applications)  while docker only runs on application layer of a Host OS.


=========================================================================

## Some Basic Docker Commands

### docker pull <imagename> or docker pull <imagename>:version 
  to pull a docker image from a repository to our local environment (dockerhub/codecommit)

### docker run <imagename> or docker run <imagename>:version
  to pull and run a docker image or to pull and run a specific version of docker image

### docker start <container_id>
  to start a container with specific id

### docker stop <container_id>
  to stop a container with specific id

### docker run -d <imagename> 
  to run a docker container in deattached mode so if we want to use terminal again i.e it actually runs in background in deattached mode

### docker run -p6000:6001 <imagename>
  to bind a local host(laptop) port to a docker container port. Here we are running a docker image with specific image name
  and making it run on specific 6000 port on our local host.6000 is our laptop port while 6001 is container port.

### docker ps
  to show list of currenlty running containers in our local system

### docker ps -a 
  lists all the docker containers running or not running

### docker images
  list all the images on our local system

=========================================================================

## Docker commands for troubleshooting

 ### docker logs <containerid> or docker logs <containername>
   shows logs of the container for trouble shooting. if any container is facing some issues we can use logs 
   to detect.

 ### docker run -d -p6001:6000 --name new_name imagename
   this renames a previous image with old name to new name and creates a new container image.
 
 ### docker exec -it <image_id> /bin/bash
   to get inside the container and execute terminal

==========================================================================
 
## Commands to remove Docker Containers and Images

### Note: To remove a container we need to first stop container then we can remove it. We can remove an image only if we stopped a container and deleted a container.

 ### docker rm <container_id>
   to remove a container with a specific container id

 ### docker rmi <container_id/image_name>
   to remove an image from our local system


==================================================================================================================================
