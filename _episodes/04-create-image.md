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
A Docker *image* is a blueprint for the container you want to create. Images can stored locally or on any Docker *repository* such as *DockerHub*. Images can then be *pulled* by different actors to run code in the exact same environment. In order to use the *image*, the actor creates a *container* from the image, which is an instantiation of the image.

In order to create a Docker image, a *Dockerfile* is used to provide build instructions for the image (Check the [d2s documentation](https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-from-dockerhub#define-a-dockerfile) for more information). One such instruction for example is adding environment variables to your container.

```dockerfile
#ARG variables are only used during the building process. They will not be available in the container. ```
#ENV sets an environment variable in the container.
ARG APP_NAME=ci_workshop
ENV APP_NAME=${APP_NAME}
ARG HOME="/app"
ENV HOME=${HOME}
```

Ofcourse we also need some way to add our application to the container. By using *ADD*, files can be copied from your machine into the image. There are some conventions to keep in mind when doing this. The app itself should be copied to the /app directory in a subfolder with its name. Data for the app should be added to .. FIXME: fix / add more conventions?
Configuration should be by *mounted* using a *volume*. A *volume* is shared between the host machine and the container, so that when the configuration is changed on the host it takes effect in the container. For more information on volumes, see [here](https://d2s.semanticscience.org/docs/guide-docker) and [here](https://docs.docker.com/storage/volumes/). For now we will not be using any configuration.

```dockerfile
#The binary folder is added to the path variable, so that any command in it can be run without specifying the path.
ENV PATH $PATH:${HOME}/${APP_NAME}/bin

#Sets the working directory to the folder mentioned. All further commands will be run from this path.
WORKDIR ${HOME}

#ADD adds everything in the folder mentioned first to the path in the container specified as the second parameter.
ADD requirements.txt requirements.txt
ADD . ${HOME}/${APP_NAME}
```

Lastly we need some way to run commands in our container. This is done by using **RUN**. For a Python container, we can use this to install some dependencies and the module itself.

```dockerfile
#RUN runs a command in the Docker container.
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
RUN pip install -e ${HOME}/${APP_NAME}
```
FIXME: add some comments on good practices for order of dockerfile contents.

> ## Create a Docker Image
> * In the root of your repository, open *Dockerfile*.
> * Start your Image from an existing image with Python already included by adding ```dockerfile FROM python:3```to your *Dockerfile*.
> * Add the first code snippet above to your *Dockerfile* to setup the image environment. 
> * Add the second code snippet above to your *Dockerfile* to add contents from your repository to the image.
> * Add the third code snippet above to your *Dockerfile* to install your Python modules in the image.
> * Create your image by running ```docker build . -t ci-workshop```.
> * Confirm the creation of your image with ```docker image ls```.
> * Add the build instructions to the README.md.
{: .challenge}

## Running a Docker Container

After the image is created we can create a container from it and run a command inside it. While ```docker create [OPTIONS] IMAGE [COMMAND] [ARG...]``` creates the container, we can also use ```docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]``` to create the container just as the create command, and afterwards runs it. It then performs the specified command inside the container.

> ## Run a Docker Container
>
> *   Create and run your application inside a container based on the image created earlier.
>
{: .challenge}

## Orchestrating Containers

One of the strengths of using Docker containers is using containers created by others and combining them with your own containers. For example, for most applications rather than manually installing a database and multiple applications you can simply pull and run a couple of containers created by the third party. In such cases (or ofcourse when you've created many images yourself) the need arises to configure for multiple images at a time, and 'link' them by having them share networks and expose ports.
There are a large number of solutions of varying complexity to handle things such as container networking and configuration. At IDS, for simple solutions [Docker Compose](https://docs.docker.com/compose/) is used. For more complex and/or production ready solutions IDS hosts an [Openshift](https://www.openshift.com/learn/what-is-openshift) cluster, which leverages [kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/). We will explore these concepts in later workshops. 

> ## Update the README.md
>
> *  Add the docker commands to the README.md
>
{: .challenge}

{% include links.md %}
