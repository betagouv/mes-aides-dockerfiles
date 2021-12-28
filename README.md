This repository is used to build Docker images for testing [Mes Aides](https://github.com/betagouv/mes-aides-ui) on CircleCI.

Basically, it creates Docker images with Node, Python & Cypress prerequisites.

The images are deployed on [Github Container Registry](https://github.com/betagouv/mes-aides-dockerfiles/pkgs/container/mes-aides-dockerfiles)

How it works
------------

Each folder `node{$NODE_VERSION}-python{$PYTHON_VERSION}` contains a `Dockerfile`.

On Github Container Registry, [each built version](https://github.com/betagouv/mes-aides-dockerfiles/pkgs/container/mes-aides-dockerfiles/versions) is available.

Each folder should have a corresponding image with an appropriate tag.

Generating a new Dockerfile
---------------------------

### 1. Create a new folder named after the tag you want to build

```
mkdir node8-python3.7
```

### 2. Generate a `Dockerfile` in this folder

```
export FOLDER=node8-python3.7-cy LINUX_VERSION=buster NODE_VERSION=8.16.1 PYTHON_VERSION=3.7.3 && mkdir --parents $FOLDER && bin/generate.sh > $FOLDER/Dockerfile
```

### 3. Push your changes

```
git add .
git commit -m 'Add a new Dockerfile for Node 8 & Python 3.7.'
git push
```

Building & pushing Docker images
--------------------------------

In order for the Docker image to be available for the CI, you will need to build the image on your machine, and push it manually to Github Container Registry.

### 1. Login on Docker

It will ask for your Github credentials. You can skip this step if you are already authenticated.

```
docker login ghcr.io --username <github-token>
```

### 2. Build the Docker image (may take a while)

```
TAG=node8-python3.7; docker build --no-cache -t ghcr.io/betagouv/mes-aides-dockerfiles:$TAG -f $TAG/Dockerfile .
```

### 3. Push the image to Github Container Registry

```
docker push ghcr.io/betagouv/mes-aides-dockerfiles:node8-python3.7
```
