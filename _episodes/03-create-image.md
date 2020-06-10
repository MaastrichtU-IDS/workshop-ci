---
title: Create a container image with Docker
teaching: 1
exercises: 1
questions:
- "What are the advantages of using Docker?"
- "How do I use Docker to package my application?"
objectives:
- "Understand the usecases of Docker."
- "Know how to run Docker containers locally."
- "Understand why Docker container orchestration is useful."
keypoints:
- "Docker solves 'it only runs on my laptop' issues."
- "Docker images can be reused to share container blueprints."
---
`
## Introduction
Docker is the foundation of most modern CI/CD solutions. Your application can be added to a Docker *container* which acts as a kind of super-lightweight virtual machine. Any further build steps can then be performed inside this *container*. For more in-depth information on Docker see [this workshop](https://github.com/MaastrichtU-IDS/docker-workshop).

## Creating a Docker image
A Docker *image* is a blueprint for the container you want to create. Images can stored locally or on any Docker *repository* such as *DockerHub*. Images can then be *pulled* by different actors to run code in the exact same environment. In order to use the *image*, the actor creates a *container* from the image, which is an instantiation of the image. In order to create a Docker image, a *Dockerfile* is used to provide build instructions for the image (Check the [d2s documentation](https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-from-dockerhub#define-a-dockerfile)) for more information. The following instructions for example set environment variables for the build process and the eventual container:

```dockerfile
#ARG variables are only used during the building process. They will not be available in the container. ```
#ENV sets an environment variable in the container.
ARG APP_NAME=ci_workshop
ENV APP_NAME=${APP_NAME}
ARG HOME="/app"
ENV HOME=${HOME}
#The binary folder is added to the path variable, so that any command in it can be run without specifying the path.
ENV PATH $PATH:${HOME}/${APP_NAME}/bin

#Sets the working directory to the folder mentioned. All further commands will be run from here.
WORKDIR ${HOME}
```

By using *ADD*, files can be copied from your machine into the image.

```dockerfile
#ADD adds everything in the folder mentioned first to the path in the container specified as the second parameter.
ADD requirements.txt requirements.txt
ADD . ${HOME}/${APP_NAME}
```

Instructions can be run from your image to perform any manner of task.

```dockerfile
#RUN runs a command in the Docker container.
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
RUN pip install -e ${HOME}/${APP_NAME}
```

> ## Create a Docker Image
> * In the root of your repository, create a file named *Dockerfile* (with no extension).
> * Start your Image from an existing image with Python already included by adding ```dockerfile FROM python:3```to your *Dockerfile*.
> * Add the first code snippet above to your *Dockerfile* to setup the image environment. 
> * Add the second code snippet above to your *Dockerfile* to add contents from your repository to the image.
> * Add the third code snippet above to your *Dockerfile* to install your Python modules in the image.
> * Create your image by running ```bash docker build . -t ci-workshop```.
> * Confirm the creation of your image with ```bash docker image ls```.
> * Add the build instructions to the README.md.
{: .challenge}

## Running a Docker Container

When want to run a container based on your image (or someone elses) it needs to be created and then run. 
```bash

```
Creates the container
```bash
```
Creates the container just as the create command, and afterwards runs it. It then performs the specified command inside the container.

> ## Configure repository permissions
>
> *   first step 
>
{: .challenge}

## Orchestrating Containers

One of the strengths of using Docker containers is using containers created by others and combining them with your own containers. For example, for most applications rather than manually installing a database and multiple applications you can simply pull and run a couple of containers created by the third party. 
There are a large number of solutions of varying complexity to handle things such as container networking and configuration. At IDS, for simple solutions Docker Compose is used. For more complex and/or production ready solutions IDS hosts an Openshift cluster, which leverages kubernetes.

> ## Create and run a simple docker-compose file
>
> *   first step 
>
{: .challenge}

{% include links.md %}
