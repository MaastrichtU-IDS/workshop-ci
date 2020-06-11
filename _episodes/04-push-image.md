---
title: Push a Docker image to DockerHub
teaching: 1
exercises: 1
questions:
- "How do I share my Docker Images with my colleagues?"
objectives:
- "Understand how Docker images are shared and reused."
- "Know how to push images to a Docker repository."
keypoints:
- "Sharing Docker images saves time recreating work and environments"
---

When a Docker image is created, it is at first stored locally. To share images with others, Docker *Repositories* can be hosted on dockerhub. After *pushing* an image, others will be able to *pull* from the same repository. Note that with a free organization plan *all* docker repositories are public.
Images are stored by supplying a *repository id* and a *tag*. If no *tag* is supplied, the image will default to the *latest* tag. *latest* does not have any special meaning, but the convention is to use this tag for the latest version of the image. In a build process for example, you may decide to tag the image twice; once with a specific version number and once with latest to overwrite the current latest image.

> ## Push Docker image to dockerhub
>
> *   [Sign up for a Docker ID](https://hub.docker.com/signup)
> * Ask an administrator (t.hendriks@maastrichtuniversity.nl for example) to be added to the IDS organization developers team on dockerhub.
> * Under the **Repositories** tab, select the *umids* organization and **Create Repository**.
![Creating a Docker Repository]({{ page.root }}/fig/template-selection.png)
> * Provide a Repository name (**name should be equal to the repository id of your created image**) and description while leaving the other values on their defaults. Create the repository.
> * In a terminal, use ```bash docker login``` to login to your docker account.
> * Use ```bash docker push umids/REPOSITORY_NAME:TAG_NAME``` to push your image to dockerhub.
> * Check your repository on [dockerhub](https://hub.docker.com) to see your hosted image.
{: .challenge}

{% include links.md %}