# Docker

## Resources

### Books

- Docker in Practice
- Practical Docker with Python

## Notes

- [Jargon around Docker](#jargon-around-docker)
- [Docker Basics](#docker-basics)
- [Dockerfile](#dockerfile)
- [Docker Volumes](#docker-volumes)
- [Docker Networks](#docker-networks)
- [Docker Compose](#docker-compose)

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

### Docker Basics

#### List of commands

- general command
  - [docker info](#hello-world)
  - [docker pull](#pull-an-image)
  - [docker run](#run-an-image)
- Containers
  - [list containers](#list-containers)
  - [stop/kill containers](#stopkill-a-container)
  - [remove containers](Remove containers)
- Images
  - [docker image ls](#remove-images)
  - [docker image inspect](#hello-world)
  - [remove images](#remove-images)

#### Hello world

```bash
# print docker info
docker info
# run hello world
docker run --rm hello-world
# list images
docker image ls
# see more info of the hello-world image, jq is required
docker image inspect hello-world
docker image inspect hello-world | jq .[].Config.Env
docker image inspect hello-world | jq .[].Config.Cmd
docker image inspect hello-world | jq .[].RootFS.Layers
```

#### Working with a Real-World Docker Image

##### Pull an image

```bash
docker pull nginx						# pull the latest version nginx
docker pull nginx:1.12-alpine-perl		# pull a older version with tag
docker login <host>:<port>				# login to private registry
docker pull <host>:<port>/<image>  		# pull from private registry
```

##### Run an image

```bash
docker run -p 8080:80 nginx	# -p <host machine port>:<container exposed port> flag publish the exposed port from container to host
```

Check the nginx server at another terminal

```bash
# check localhost
curl http://localhost:8080
# check container port
docker image inspect nginx | jq .[].Config.ExposedPorts
```

##### List containers

```bash
docker ps		# list running containers
docker ps -a 	# list all containers
```

Results:

```bash
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
371d946f9aed   nginx     "/docker-entrypoint.…"   43 seconds ago   Up 42 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   ecstatic_moser
```

Note that we can use ```-n <name>``` to provide a name when starting a container.

##### Stop/Kill a container

```bash
docker stop <container-id>	# stop a container
docker kill <container-id>	# force stop and kill the container
```

##### Remove containers

```bash
docker rm <container-id>
```

##### Remove images

Check image id

```bash
docker image ls		# list all images
```

Results

```bash
REPOSITORY        TAG                             IMAGE ID       CREATED         SIZE
nginx             latest                          dd34e67e3371   2 weeks ago     133MB
nginx             1.12-alpine-perl                b6a456f1d7ae   3 years ago     57.7MB
```

Remove images

```bash
docker rmi <image-id>
```

Note that docker refuses to remove an image that is referred by another container

### Dockerfile

#### Build Context

```bash
docker build https://github.com/sathyabhat/sample-repo
git#mybranch												# or git#mytag
```

#### Dockerignore

The ignore list provided by ```.dockerignore```

```shell
# This is a .dockerignore file
*/temp*
.DS_Store
.git
```

#### Dockerfile Instructions

##### FROM

Tells the Docker which Image to build from.

Every valid Dockerfile must start with ```FROM```

```bash
FROM <image>[:<tag>] [AS <name>]
FROM <image>[@digest] [AS <name>]
```

##### WORKDIR

Works like ```cd``` in ```bash```, but ```WORKDIR``` is set as ```/``` by default.

Sets the current working directory for ```RUN```, ```CMD```, ```ENTRYPOINT```, ```COPY``` and ```ADD```.

```WORKDIR``` can be set multiple times in a Dockerfile and, if a relative directory succeeds a previous ```WORKDIR``` instruction, it will be relative to the previously set working directory.

```bash
WORKDIR <dir>
```

Notice that we did not set any absolute working directory in the Dockerfile. The relative directories were appended to the default.

##### ADD & COPY





##### RUN

Execute any commands in a new layer on top of the current image and create a new layer that is available for the next steps

```bash
RUN <command>										# the shell form
RUN ["executable", "parameter 1", " parameter 2"]	# the exec form
```





##### CMD & ENTRYPOINT





##### ENV

Sets the environment variables to the image.

The environment variables set are **persisted** through the container runtime. They can be viewed using `docker inspect`.

```bash
ENV <key> <value>		# the entire string after <key> will be considered the value
ENV <key>=<value> ...
```

The environment variables defined for a container can be **changed** when running a container by 

 ````bash
 docker run -e <key>=<value> <image>
 ````

##### [VOLUME](#docker-volumes)

Tells Docker to create a directory on the host and mount it to a path specified in the instruction.

```bash
VOLUME <dir>
```

##### EXPOSE

Tells Docker that the container listens for the specified network ports at runtime. If it’s not specified, Docker assumes the protocol to be TCP

```bash
EXPOSE <port> [<port>/<protocol>]
```

For example

```bash
# expose port 53 on TCP and UDP
EXPOSE 53/tcp
EXPOSE 53/udp
```

##### LABEL

Adds metadata to an image as a key/value pair.

```bash
LABEL <key1>=<value1> <key2>=<value2> ...
```

- Key

  - keys should begin and end with lowercase letters
  - keys only allow `[a-z0-9]`, periods `.`, hyphens `-`. Consecutive hyphens or periods are not allowed
  - Authors of **third-party tools** should prefix each key with reverse DNS notaion of a domain owned by them. For example, `com.sathyasays.my-image`
  - Reserved by Docker: `com.docker.*`, `io.docker.*`, `org.dockerporject.*`

- Value

  Label values can contain any data type that can be represented as string, including `JSON`, `XML`, ```YAML```, and `CSV`.

#### Dockerfiles Guidelines

- Containers should be ephemeral

  we should be able stop, destroy, and restart the container at any point with minimal setup and
  configuration to the container.

- Keep the build context minimal

  This can be done by using the `.dockerignore` file effectively.

- Use multi-stage builds

- Skip unwanted packages

- Minimize the number of layers

  As of Docker 1.10 and above, only `RUN`, `COPY`, and `ADD` instructions create layers.

#### Multi-Stage Builds (ver. 17.05+)

Especially useful for building images of applications that require some additional build-time dependencies but are not needed during runtime.

With multi-stage builds, a single Dockerfile can be leveraged for build and deploy images—the build images can contain the build tools required for generating the binary or the artifact and in the second stage, the artifact can be copied to the runtime image, thereby reducing considerably the size of the runtime image.

### Docker Volumes



### Docker Networks

### Docker Compose

