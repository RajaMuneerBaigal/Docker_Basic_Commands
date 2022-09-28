# Docker_Basic_Commands

## Some important Docker Concepts/Terminalogies 

## Difference between Image and Container
### Image is an artifact that can be moved across different containers. Image has layers and it can be stored in a private or public repository.All the artifacts inside a docker hub are images. We have several versions of different images which we can used as our application dependencies rely upon.

### Container is actually a running environment for an image. Container has environment configurations, applications images and file systems all in one place.A container has a port binded to it which makes it possible to talk to an application running inside of a container

## Difference between Virtual Machine and Docker

### Both are virtualization technologies. Virtual machine utilizes both the layers of Operation system(kernel and applications)  while docker only runs on application layer of a Host OS.
