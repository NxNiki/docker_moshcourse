# Notes of the online course on docker

## Section 1

### What is docker?
Docker is a platform for building, running, and shipping applications in a consistent manner.

Problems in development:
One or more files missing
Software version mismatch
Different configuration setting


Docker download and run dependencies in a container, which is an isolated environment that allows multiple applications use different versions of some software side by side.

  `docker-compose up`
  
Docker can also easily remove the dependencies associated with an application when it is not in use.

  `docker-compose down --rmi all`


### Container: An isolated environment for running an application.
  Allow running multiple apps in isolation
  Lightweight
  Use the OS of the host
  Start quickly
  Need fewer hardware resources (no need to assign CPU cores or memory space)

### Virtual machine: an abstraction of a machine (physical hardware). Use hypervisor to create and manage virtual machines.

### Docker architecture:

Client: client talks to the server using RESTful API

Server: also called docker-engine, sits in the background and takes care of building and running Docker containers.

The container is technically a special process that runs on the computer. All containers share the kernel of the host.


### install docker:
Check if docker is installed:

  `docker version`


### development workflow:
Dockerize an application:
Dockerfile: a plain text file that includes instructions that docker uses to package an application into an image. This image contains everything the application needs to run.

Image:
  A cut-down OS
  A runtime environment (eg. Node)
  Application files.
  Third-party libraries
  Environment variables

Docker starts a container using an image. A container is a special process that has its own file system, which is provided by the image. Instead of launching an application and running it inside a typical process, we tell docker to run it inside a container.

Beauty of Docker:
An image can be pushed to a Docker registry (Docker Hub), then it can be put on any machines running docker. We can pack an application with an image and run it anywhere.


Create Dockerfile:
FROM node:alpine # base image that is officially published on docker hub.
COPY . /app # copy all the files in the current directory into the app directory into that image. (app is created automatically)
CMD node /app/app.js
or
WORKDIR /app
CMD node app.js

Package up our application, run in terminal:

`docker build -t (tag to identify the image) hello-docker . (specify where to find Dockerfile eg. in current directory)`

list the docker images:
  `docker images`
  `docker image ls`

Run image:
  `docker run hello-docker`

We can push this image to docker hub so that it can be pulled on any computer. Search for play with docker and enjoy!

  `docker pull codewithmosh/hello-docker`
  `docker images`
  `docker run codewithmosh/hello-docker`

  
