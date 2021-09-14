# Docker for Data Scientist

## Why Docker?(Or why not Anaconda?)

Before starting with Docker, you should know there are some other options to build your machine learning (ML) developing environment such as [Anaconda](https://www.anaconda.com/) or [pyenv](https://github.com/pyenv/pyenv). Anaconda is a better choice if you‘re totally new to ML because it's easier to start with. However, there are some reason that bordered me which drove me to switch to Docker:

- Anaconda didn't have China mirror site. Installing new package could be painful because of the download speed.
- Although Anaconda is theoretically functional of sharing environment to others, practically it's quite difficult to do that. 
- Anaconda could take a lot of disk space if you're using multiple virtual environments, even if they're just slightly different.

With Docker, all these problems solved. Docker have multiple China mirror site. It's easy to share environment with Dockerhub or Dockerfile. Docker takes much fewer disk space by its layer mechanism.

## Using Docker just like Anaconda

Before we start, I assume you already install [Docker](https://docs.docker.com/engine/install/) and [NVIDIA Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html). [VSCode](https://code.visualstudio.com/) is also recommended as your IDE. Make sure platform requirements are satisfied before you install. 

> ### Platform Requirements
>
> The list of prerequisites for running NVIDIA Container Toolkit is described below:
>
> 1. GNU/Linux x86_64 with kernel version > 3.10
> 2. Docker >= 19.03 (recommended, but some distributions may include older versions of Docker. The minimum supported version is 1.12)
> 3. NVIDIA GPU with Architecture >= Kepler (or compute capability 3.0)
> 4. [NVIDIA Linux drivers](http://www.nvidia.com/object/unix.html) >= 418.81.07 (Note that older driver releases or branches are unsupported.)

Run this simple test to **verify NVIDIA Docker is correctly installed**.

```bash
$ sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
```

This should result in a console output shown below:

```shell
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.51.06    Driver Version: 450.51.06    CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   34C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

Some terminology should be clarified. `Image` is like an **Object or Class** in Python, `Container` is an **instance** of Image. We don't use `Image` directly. When we use the `Docker run <image>` command, we specify a container, every change we make is made on the container.

Let's start now.

### Step 1: Pull an Image

Choose a base image to start with, use the following command to download the image.

```bash
docker pull <image>:<tag>
```

There are many choices on [Dockerhub](https://hub.docker.com/). You can download a basic linux image with CUDA and CUDNN installed, such as [nvidia/cuda](https://hub.docker.com/r/nvidia/cuda), and install your own python packages. Official deep learning images such as [pytorch/pytorch](https://hub.docker.com/r/pytorch/pytorch) and [tensorflow/tensorflow](https://hub.docker.com/r/tensorflow/tensorflow) are also provided. It's also a good idea to start with a Jupyter Notebook Image such as [jupyter/scipy-notebook](https://hub.docker.com/r/jupyter/scipy-notebook) or [jupyter/tensorflow-notebook](https://hub.docker.com/r/jupyter/tensorflow-notebook).

### Step 2: Run a Container

#### Interactively

#### Run in background

#### Expose a port to Use Jupyter Notebook

#### Where do I put my data and results?

### Step 3: Commit a Container to a New Image

### Step 4: What if I Want to Add Volumes or Expose New Ports to an Existing Container?

### Step 5: Use VSCode as Your Editor

[Connect to remote Docker over SSH](https://code.visualstudio.com/docs/containers/ssh)









## A Simple Dockerfile Template For Data Scientist