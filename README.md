# Notes of the online course on docker

## Section 1

###What is docker?
Docker is a platform for building, running, and shipping applications in a consistent manner.

Problems in development:
One or more files missing
Software version mismatch
Different configuration setting


Docker download and run dependencies in a container, which is an isolated environment that allows multiple applications use different versions of some software side by side.
  `docker-compose up`
  
Docker can also easily remove the dependencies associated with an application when it is not in use.
  `docker-compose down --rmi all`


###Container: An isolated environment for running an application.
  Allow running multiple apps in isolation
  Lightweight
  Use the OS of the host
  Start quickly
  Need fewer hardware resources (no need to assign CPU cores or memory space)

###Virtual machine: an abstraction of a machine (physical hardware). Use hypervisor to create and manage virtual machines.

#### Docker architecture:

Client: client talks to server using RESTful API

Server: also called docker-engine, sits in the background and takes care of building and running Docker containers.

The container is technically a special process that runs on the computer. All containers share the kernel of the host.


### install docker:
check if docker is installed:
  docker version




