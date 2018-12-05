This repository is used to build Docker images for testing Mes Aides on CircleCI.

Basically, it creates Docker images with Node & Python.

Building Docker images manually
-------------------------------

For example, to build a Docker image with Node 8 & Python 3.6:

```
docker build --no-cache -t betagouv/mes-aides-docker:<tag> -f node8-python3.6/Dockerfile .
```
