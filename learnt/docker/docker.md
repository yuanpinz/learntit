# Docker

## Resources

**Online resources**: [Docker Docs](https://docs.docker.com/)

**Books**: Docker in Practice, Practical Docker with Python

## Notes

### Docker Architecture

![docker architecture](imgs/architecture.svg)

Docker uses a **client-server** architecture. The **Docker daemon** `dockerd` listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. The **Docker client** `docker`  sends these commands to `dockerd`. A **Docker registry** stores *Docker images*.

An **image** is a read-only template with instructions for creating a Docker *container*. A **container** is a runnable instance of an image.

### Manage data in Docker

![](imgs/types-of-mounts.png)

**Volumes** are stored in a part of the host filesystem which is *managed by Docker* (`/var/lib/docker/volumes/` on Linux). **Bind mounts** may be stored *anywhere* on the host system. **tmpfs mounts** are stored in the host system’s memory only, and are never written to the host system’s filesystem.

### Docker Run

[Doc](https://docs.docker.com/engine/reference/commandline/run/)

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

The `docker run` command first `creates` a **writeable container layer over the specified image**, and then `starts` it using the specified command. A stopped container can be **restarted with all its previous changes** intact using `docker start`. See `docker ps -a` to view a **list of all containers**.

| Name, shorthand        | Default | Description                                        |
| ---------------------- | ------- | -------------------------------------------------- |
| `--interactive` , `-i` |         | Keep STDIN open even if not attached               |
| `--tty` , `-t`         |         | Allocate a pseudo-TTY                              |
| `--name`               |         | Assign a name to the container                     |
| `--privileged`         |         | Give extended privileges to this container         |
| `--workdir` , `-w`     |         | Working directory inside the container             |
| `--mount`              |         | Attach a filesystem mount to the container         |
| `--publish` , `-p`     |         | Publish a container's port(s) to the host          |
| `--detach` , `-d`      |         | Run container in background and print container ID |

#### Examples

**Assign name and allocate pseudo-TTY (--name, -it)**

```bash
docker run --name test -it debian
```

**Full container capabilities (--privileged)**

```bash
docker run -t -i --privileged ubuntu bash
```

**Set working directory (-w)**

```bash
docker  run -w /path/to/dir/ -i -t  ubuntu pwd
```

**Mount tmpfs (--tmpfs)**

```bash
docker run -d --tmpfs /run:rw,noexec,nosuid,size=65536k my_image
```

**Mount volume (-v, --read-only)**

```bash
docker  run  -v `pwd`:`pwd` -w `pwd` -i -t  ubuntu pwd
```

**Add bind mounts or volumes using the --mount flag**

```bash
docker run --read-only --mount type=volume,target=/icanwrite busybox touch /icanwrite/here
```

```bash
docker run -t -i --mount type=bind,src=/data,dst=/data busybox sh
```

**Publish or expose port (-p, --expose)**

This binds port `8080` of the container to TCP port `80` on `127.0.0.1` of the host machine. Note that ports which are not bound to the host (i.e., `-p 80:80` instead of `-p 127.0.0.1:80:80`) will be accessible from the outside.

```bash
docker run -p 127.0.0.1:80:8080/tcp ubuntu bash
```

This exposes port `80` of the container without publishing the port to the host system’s interfaces.

```bash
docker run --expose 80 ubuntu bash
```

### Docker Commit

[Doc](https://docs.docker.com/engine/reference/commandline/commit/)

```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

#### Options

| Name, shorthand    | Default | Description                                                |
| ------------------ | ------- | ---------------------------------------------------------- |
| `--author` , `-a`  |         | Author (e.g., "John Hannibal Smith <hannibal@a-team.com>") |
| `--change` , `-c`  |         | Apply Dockerfile instruction to the created image          |
| `--message` , `-m` |         | Commit message                                             |
| `--pause` , `-p`   | `true`  | Pause container during commit                              |

#### Examples

**Commit a container**

```bash
docker ps
docker commit c3f279d17e0a  svendowideit/testimage:version3
docker images
```

**Commit a container with new `CMD` and `EXPOSE` instructions**

```bash
docker ps
docker commit --change='CMD ["apachectl", "-DFOREGROUND"]' -c "EXPOSE 80" c3f279d17e0a  svendowideit/testimage:version4
docker run -d svendowideit/testimage:version4
docker ps
```

### Dockerfile

[Reference](https://docs.docker.com/engine/reference/builder/), [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

#### Docker Build

The [docker build](https://docs.docker.com/engine/reference/commandline/build/) command builds an image from a `Dockerfile` and a *context*. The build’s context is the set of files at a specified location `PATH` or `URL`.

#### Dockerfile Format

```dockerfile
# Comment
INSTRUCTION arguments
```

A `Dockerfile` **must begin with a `FROM` instruction**. This may be after [parser directives](https://docs.docker.com/engine/reference/builder/#parser-directives), [comments](https://docs.docker.com/engine/reference/builder/#format), and globally scoped [ARGs](https://docs.docker.com/engine/reference/builder/#arg).  

#### `.dockerignore` file

Here is an example `.dockerignore` file:

```gitignore
# comment
*/temp*
*/*/temp*
temp?
```

| Rule        | Behavior                                                     |
| :---------- | :----------------------------------------------------------- |
| `# comment` | Ignored.                                                     |
| `*/temp*`   | Exclude files and directories whose names start with `temp` in any immediate subdirectory of the root. For example, the plain file `/somedir/temporary.txt` is excluded, as is the directory `/somedir/temp`. |
| `*/*/temp*` | Exclude files and directories starting with `temp` from any subdirectory that is two levels below the root. For example, `/somedir/subdir/temporary.txt` is excluded. |
| `temp?`     | Exclude files and directories in the root directory whose names are a one-character extension of `temp`. For example, `/tempa` and `/tempb` are excluded. |

#### FROM

```dockerfile
FROM [--platform=<platform>] <image> [AS <name>]
```

Or

```dockerfile
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```

Or

```dockerfile
FROM [--platform=<platform>] <image>[@<digest>] [AS <name>]
```

`ARG` is the only instruction that may precede `FROM` in the `Dockerfile`. An `ARG` declared before a `FROM` is outside of a build stage, so it can’t be used in any instruction after a `FROM`. To use the default value of an `ARG` declared before the first `FROM` use an `ARG` instruction without a value inside of a build stage.

`FROM` can appear multiple times within a single `Dockerfile` to create multiple images or use one build stage as a dependency for another. 

Example:

```dockerfile
ARG  CODE_VERSION=latest
FROM base:${CODE_VERSION}
CMD  /code/run-app

FROM extras:${CODE_VERSION}
CMD  /code/run-extras
```





## Practical Docker with Python Notes

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

