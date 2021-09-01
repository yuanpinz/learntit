# Docker

## Resources

### Books

- Docker in Practice
- Practical Docker with Python

## Notes

### Jargon around Docker

#### Layers

 A layer is created when a base image  is changed. Example:

```bash
FROM ubuntu
Run mkdir /tmp/logs			# added a layer for creating /tmp/logs
RUN apt-get install vim		# added a layer that installs vim
RUN apt-get install htop	# added a layer that installs htop
```

- When Docker builds the image, each layer is stacked on the next and  merged into a single layer using the union filesystem
- When Docker scans a base image, it scans for the IDs of all the layers  that constitute the image.

#### Docker Image

- Docker image is a **read-only template** that forms the foundation of your  application
- A Docker image starts with a base image like Ubuntu. On top  of this image, we can add build our application stack adding the packages  as and when required.
- Docker images are created using a series of commands, known as  instructions, in the Dockerfile.

#### Docker Container

- The main difference  between a Docker image and a container is the presence of *a thin read/ write layer* known as the **container layer**.
- when the container is  stopped/killed, the container layer is not saved
- Stateful applications and those requiring persistent data were  initially not recommended as containerized applications

#### Bind Mounts and Volumes

- volumes and bind mounts: stored in the host filesystem
- tmpfs volumes: stored in the host system’s memory  only

#### Docker Registry

A Docker Registry is a place  where you can store Docker images so that they can be used as the basis  Chapter 2 Docker 101 19 for an application stack

#### Dockerfile

A Dockerfile is a set of instructions that tells Docker how to build an image.  A typical Dockerfile is made up of the following: 

- A **FROM** instruction that tells Docker what the *base  image* is 
- An **ENV** instruction to pass an *environment variable* 
- A **RUN** instruction to run some *shell commands* (for  example, install-dependent programs not available in  the base image) 
- A **CMD** or an **ENTRYPOINT** instruction that tells Docker  which *executable* to run when a container is started

#### Docker Engine

Docker Engine is a client-server  application that provides the platform, the runtime, and the tooling for  building and managing Docker images, Docker containers, and more

##### Docker Daemon

The Docker daemon is a service that runs in the  background of the host computer and handles the  heavy lifting of most of the Docker commands

##### Docker CLI

Docker CLI is the primary way that you will interact with Docker. Docker  CLI exposes a set of commands that you can provide. The Docker CLI  forwards the request to Docker daemon, which then performs the  necessary work

```bash
docker build
docker pull
docker run
docker exec
docker help <command>
```

##### Docker API

This  is particularly useful if there’s a need to create or manage containers from  within applications.

#### Docker Compose

Docker Compose is a tool for defining and running multi-container  applications.

The most common use case for Docker Compose is to run applications  and their dependent services (such as databases and caching providers)  in the same simple, streamlined manner as running a single container  application.

#### Docker Machine

Docker Machine allows you to  create Docker hosts on local as well remote systems, including on cloud  platforms like Amazon Web Services, DigitalOcean, and Microsoft Azure

### Hands-on Docker
