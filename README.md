Notes of the online course on docker

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

Docker starts a container using an image. A container is a special process with its own file system, provided by the image. Instead of launching and running an application inside a typical process, we tell docker to run it inside a container.

The beauty of Docker:
An image can be pushed to a Docker registry (Docker Hub), then put on any machines running Docker. We can pack an application with an image and run it anywhere.


Create Dockerfile:
```
FROM node:alpine # base image that is officially published on docker hub.
COPY . /app # copy all the files in the current directory into the app directory into that image. (app is created automatically)
CMD node /app/app.js
or
WORKDIR /app
CMD node app.js
```

Package up our application, and run it in terminal:

`docker build -t (tag to identify the image) hello-docker . (specify where to find Dockerfile eg. in current directory)`

list the docker images:
  `docker images`
  `docker image ls`

Run image:
  `docker run hello-docker`

We can push this image to the docker hub to pull it on any computer. Search for play with Docker and enjoy!


  `docker pull codewithmosh/hello-docker`
  `docker images`
  `docker run codewithmosh/hello-docker`


## Section 3:

- Creating Docker files
- Versioning images
- Sharing images
- Saving and loading images
- Reducing the image size
- Speeding up builds

### Docker file instructions:

```
FROM node:14.16.0-alpine3.13 # specifying the base image, find images on docker hub
```

Build image:
`docker build -t react-app .` 
`-t: tagging the image
`.`: tell docker where to find the docker file

`docker run -it react app
This will lead us to a node environment where we can write javascript code. Press Ctrl+C to exit.

`docker run -t react-app sh`
This starts the shell so we can check the files in the container.


Copy application files into the image:
```
FROM node:14.16.0-alpine3.13
COPY package*.json /app # docker automatically creates the directory if it does not exist.
```

```
FROM node:14.16.0-alpine3.13
WORKDIR /app # setting the working directory.
COPY . . # This will copy files to the working directory.
# COPY ["hello word.txt", "."] # This is useful when we have spaces in the file name.
# ADD HTTP://.../file.json .  # ADD has two additional features compared to COPY, we can add files from a URL, it will automatically uncompress the file
# ADD file.zip .
```


Excluding files and directories:
- build is faster
- avoid transferring too many files to the docker engine.

