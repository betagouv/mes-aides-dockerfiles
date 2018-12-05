This repository is used to build Docker images for testing Mes Aides on CircleCI.

Basically, it creates Docker images with Node & Python.

The images are deployed on [Docker Hub](https://hub.docker.com/r/betagouv/mes-aides-docker)

Building Docker images manually
-------------------------------

For example, to build a Docker image with Node 8 & Python 3.6:

```
docker build --no-cache -t betagouv/mes-aides-docker:<tag> -f node8-python3.6/Dockerfile .
```
