# Docker for [fast.ai](http://course.fast.ai) Course 1
A Jupyter environment for fast.ai's Deep Learning MOOC at http://course.fast.ai.

Runs a Jupyter notebook on port 7777 with the default password '123'.

Uses CPUs by default and NVIDIA GPUs when run with [nvidia-docker](https://github.com/NVIDIA/nvidia-docker).

The container comes with:
* All notebooks from https://github.com/fastai/courses/tree/master/deeplearning1/nbs
* Python 2.7 (the default Python version used in the course)
* Conda
* Theano
* Keras
* PIL
* Jupyter
* bcolz
* kaggle-cli
* ...all other libraries needed for the course.

## Usage

#### CPU Only
```bash
docker run -it -p 7777:7777 nsharmarijal/pdl
```

#### With GPU
```bash
nvidia-docker run -it -p 7777:7777 nsharmarijal/pdl
```

## Data management
Docker containers are designed to be ephemeral, so if you need persistent data for Kaggle competitions you should download it on your local machine and [mount the directory as a host volume](https://docs.docker.com/engine/tutorials/dockervolumes/#/mount-a-host-directory-as-a-data-volume) when you run the container.

For example, if your data directory is at `/Users/yourname/data`, start your container with this command:

```bash
docker run -it -p 7777:7777 -v /Users/yourname/data:/home/docker/data nsharmarijal/pdl
```

Your local data directory will now be visible in the container at `/home/docker/data`.

## Installing packages
All packages should ideally be part of the Dockerfile. If something is missing, please open an issue or submit a PR to update the Dockerfile. If you need to install something as a workaround, follow the steps below:
1. Get a shell into the running container with `docker exec -it <container_name> /bin/bash`
2. `sudo apt-get update && sudo apt-get install package_name`
