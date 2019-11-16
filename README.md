This repository is used to build Docker images for testing [Mes Aides](https://github.com/betagouv/mes-aides-ui) on CircleCI.

Basically, it creates Docker images with Node & Python.

The images are deployed on [Docker Hub](https://hub.docker.com/r/betagouv/mes-aides-docker)

How it works
------------

Each folder `node{$NODE_VERSION}-python{$PYTHON_VERSION}` contains a `Dockerfile`.

On Docker Hub, [Automated Builds](https://docs.docker.com/docker-hub/builds/) are configured.

Each folder is configured to build the corresponding tag.

![Automated Builds](https://raw.githubusercontent.com/betagouv/mes-aides-dockerfiles/master/images/automated-builds.png "Automated Builds")

Generating a new Dockerfile
---------------------------

1. Create a new folder named after the tag you want to build

```
mkdir node8-python3.7
```

2. Generate a `Dockerfile` in this folder

```
FOLDER=node8-python3.7-cy LINUX_VERSION=buster NODE_VERSION=8.16.1 PYTHON_VERSION=3.7.3; mkdir $FOLDER && bin/generate.sh > $FOLDER/Dockerfile
```

3. Push your changes

```
git add .
git commit -m 'Add a new Dockerfile for Node 8 & Python 3.7.'
git push
```

Building & pushing Docker images manually
-----------------------------------------

You may want to build the Docker image on your machine, and push it manually to Docker Hub.

1. Login on Docker

It will ask for your Docker hub credentials. You can skip this step if you are already authenticated.

```
docker login --username=<username>
```

2. Build the Docker image (may take a while)

```
TAG=node8-python3.7; docker build --no-cache -t betagouv/mes-aides-docker:$TAG -f $TAG/Dockerfile .
```

3. Push the image to Docker Hub

```
docker push betagouv/mes-aides-docker:node8-python3.7
```
