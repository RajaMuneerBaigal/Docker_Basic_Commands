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
  - to pull a docker image from a repository to our local environment (dockerhub/codecommit)

### docker run "imagename" or docker run "imagename":version
  - to pull and run a docker image or to pull and run a specific version of docker image

### docker start "container_id"
  - to start a container with specific id. this can only be run when a container was stopped and we want to run the container again.

### docker stop "container_id"
  - to stop a container with specific id

### docker run -d "imagename" 
  - to run a docker container in deattached mode so if we want to use terminal again i.e it actually runs in background in deattached mode

### docker run -p6000:6001 "imagename"
  - to bind a local host(laptop) port to a docker container port. Here we are running a docker image with specific image name
  and making it run on specific 6000 port on our local host.6000 is our laptop port while 6001 is container port.

### docker ps
  - to show list of currenlty running containers in our local system

### docker ps -a 
  - lists all the docker containers running or not running

### docker images
  - list all the images on our local system

=========================================================================

## Docker commands for troubleshooting

 ### docker logs "containerid" or docker logs "containername"
   - shows logs of the container for trouble shooting. if any container is facing some issues we can use logs 
     to detect.

 ### docker run -d -p6001:6000 --name new_name imagename
   - this runs a container with a name given which then can be used to inpsect logs.
 
 ### docker exec -it <image_id> /bin/bash
   - to get inside the container and execute terminal

==========================================================================
 
## Commands to remove Docker Containers and Images

- Note: To remove a container we need to first stop container then we can remove it. We can remove an image only if we stopped a container and deleted a container.

 ### docker rm <container_id>
   - to remove a container with a specific container id

 ### docker rmi <container_id/image_name>
   - to remove an image from our local system

  ==============================================================================
  
  ## Commands to stop all containers at once and restart them 
  - docker kill $(docker ps -q)
  - docker restart $(docker ps -a -q)
  

  ==============================================================================
  
  ## Commands to delete all volumes, containers and images
  - docker container prune
  - docker volume prune
  - docker network prune
  - docker image prune

  ==============================================================================
  
  ## Commands to list all volumes, containers and images
  - docker volume ls
  - docker network ls
  - docker image ls
  - docker container ls
   
  ## Docker Secret
   ==============================================================================
   - docker secret create  "name" -            : to create a secret. here name is any name .i.e dbpass etc and minus at the enter is used to input secret
   - docker secret create "filename" myfile    : to create a secret using file.i.e in myfile I can save my secret and create a filename with secret insid
   - docker secret ls                          : to list all secrets
   - docker secret rm  -id-                    : to remove secrets
   - docker secret inspect                     : to inspect a secret
  
  ### NOTE: the secret created needs to be associated with a service in docker swarm while creating a service with --secret "name"  flag otherwise it won't be accessbile to any service without properly associating.
  e.g docker service create --secret dbpass alpine ping 8.8.8.8
  
  The secrets will be stored inside the container at the location /run/secrets/secretname
  To create a database service such as mysql with our secret will be as follows:
  docker service create  --secret dbpass -e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/dbpass mysql
  
  ## Docker Swarm
   ==============================================================================
   A Docker Swarm is a group of either physical or virtual machines that are running the Docker application and that have been configured to join  together   in a cluster. A cluster is a group of nodes joined together to perform a task. Nodes are actually virtual machines connected together using docker api.
  There is a concept of manager and worker node in docker swarm. Manager node assigns tasks to nodes inside the cluster and sometimes itslef also performs some tasks.The activities of the cluster are controlled by a swarm manager, and machines that have joined the cluster are referred to as nodes.
  Docker Swarm has two types of services: replicated and global.
  ![image](https://user-images.githubusercontent.com/105891199/205648617-77e3182f-3876-466b-96aa-62fc2a688d39.png)
  ![image](https://user-images.githubusercontent.com/105891199/205650359-e90013db-f1dc-4621-ab79-4de4476cb0a0.png)

  One of the key benefits associated with the operation of a docker swarm is the high level of availability offered for applications.
  Some other key   features of docker swarm are:
  1- Load balancing
  2- Decentraliztion
  3- Security
  4- high availability
  5- low downtime
  ### Docker architecture
  ![image](https://user-images.githubusercontent.com/105891199/205650880-557dac9c-f1a7-4713-a0b0-13c6d938b30f.png)

  ### How Docker Swarm Work
  ![image](https://user-images.githubusercontent.com/105891199/205651248-057b24cc-c0e5-4a56-92f9-1877bddec41c.png)
  ![image](https://user-images.githubusercontent.com/105891199/205651562-c91d9dad-cbf6-41bb-a6c0-034fa4a3afe6.png)


   ==============================================================================
   ## Docker Swarm commands 
  ### The commands to be run on manager node are as follows:
  -  docker swarm init --advertise-addr -ip-                : this will create the current machine as manager node in docker swarm cluster
  -  docker swarm init                                      : same as above
  -  docker info | head -50                                 : to check the status of docker swarm if initialized or not.
  -  docker node ls                                         : to list down all docker nodes
  -  docker swarm join --token -token-                      : to join a worker node to cluster 
  -  docker swarm join-token worker/manager                 : to get the token after missing it. this will give token for joining nodes as manager or wrk
  -  docker node rm -f -node-name-                          : to remove a node from cluster or swarm
  -  docker node inspect -node-name-                        : to inspect a node just like container inspect
  -  docker node promote -node1- -node2-                    : to promote a node to manager node
  -  docker node demote -node1- -node2-                     : to demote a node to worker node
  -  watch docker container ls                              : list all containers after one seconds
  -  docker service create -imageName-                      : will create a service on all nodes inside the cluster
  -  docker service inspect -service-id-                    : to inspect a service with service id
  -  docker service inspect --pretty -service-name-         : to inspect service in a more readable way
  -  docker service logs <service-id>                       : to find the logs of the service created
  -  docker service rm -service-name-                       : to remove a service
  -  docker service scale -name/id-=5
  -  docker service ps -service-name-                       : to list a service with its name
  -  docker node update --availability drain -node-name-    : it will not allocate services to that node specified
  -  docker node upate --availability active -node-name-    : it will active the node again and tasks will be assigned to it
  -  docker node update --label-add="ssd=true" -node-name-  : this will add a label to our node to which we can add tasks or services. e.g ssd node
  ### Some important flags regarding creating services in docker swarm
   -  --name -service-name-                                 : flag used to give name to a service
   -  --mode global                                         : flag used to create service in every node including manager
   -  --replicas -number-                                   : how many replicas of current service you want to run in cluster or docker swarm.  
   -  -p  8080:80                                           : to expose a port
   -  --constraint="node.role==manager"                     : this will create all the services in manager mode
   -  --constraint="node.role==worker"                      : this will create all the services in worker node
   -  --constraint="node.label.ssd==true"                   : this will create all the services in a node with label ssd and ssd=true
  ### The commands to be run on worker nodes are as follows:
  - docker swarm leave  --force                   : if a node wants to leave a cluster it can use this command but its status will be shown as down.
  
   ==============================================================================
   ## Docker Stack
   With docker compose we have a yaml file which is used to create services but the issue with docker compose is that when we write docker compose up it creates services only on the machine on which the command is run. for multiple machines we have to do it manually which is not an efficient way. With docker stack we can deploy services to all nodes in a cluster using a single command.Though it uses the same docker compose file
  
 - docker stack deploy -c docker-compose.yml "stackname"
 - docker stack --help   to find more options for docker stack
