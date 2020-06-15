---
title: Automate Docker build with GitHub Actions
teaching: 1
exercises: 1
questions:
- "How do I build and publish a new release of my application?"
objectives:
- "Build a Docker image and push it to DockerHub if the tests pass."
- "Only build and push when a new release is published,."
keypoints:
- "Use the official GitHub Action from Docker."
- "Set sensible informations, such as passwords, in GitHub Secrets."
---

If the tests pass without failing you might want to build a Docker image for your application, and publish it to [DockerHub](https://hub.docker.com/). This will enable anyone to easily reuse your applications without the need to install dependencies.

> ## Build and push Docker image
>
> *  Find the "Build and push Docker images" action on the [GitHub Marketplace](https://github.com/marketplace?type=actions): [https://github.com/marketplace](https://github.com/marketplace)
> *  Use the action to automatically build and push a Docker image if the tests pass. Do the build in a new job named `build`. Use the **Example usage** section in the action readme.
> *  You can safely store your DockerHub username and password using secrets. 
>    *  Go to the ⚙️ **Settings** tab of your GitHub repository
>    *  Go to **Secrets** in the left navbar. 
>    *  Create 2 secrets that will be used by the GitHub Actions workflow: `DOCKER_USERNAME` and `DOCKER_PASSWORD` 🔒
>
> > Once a secret has been defined no one (not even you) can read it, you can still override it though.
>
> > ## Solution
> > ~~~YAML
> > name: Test and publish to DockerHub
> > on:
> >   push:
> >     branches: [ master ]
> > jobs:
> >   test:
> >     [...]
> >   
> >   build:
> >     if: startsWith(github.event.ref, 'refs/tags')
> >     needs: test
> >     runs-on: ubuntu-latest
> > 
> >     steps:
> >     - uses: docker/build-push-action@v1
> >       with:
> >         username: ${{ secrets.DOCKER_USERNAME }}
> >         password: ${{ secrets.DOCKER_PASSWORD }}
> >         repository: myorg/myrepository
> >         tag_with_ref: true
> >         push: ${{ startsWith(github.ref, 'refs/tags/') }}
> > ~~~
> > {: .output}
> {: .solution}
>
> {: .challenge}


> ## Push only when release
>
> *  Add a condition to only push to DockerHub when a release is pushed (a.k.a. creating a tag)
> *  2 solutions are available for this case: using a `if` condition in the GitHub workflow (recommended), or use a parameter provided by the "Build and push Docker images" action.
>
> > ## Solution
> > ~~~YAML
> > name: Test and publish to DockerHub
> > on:
> >   push:
> >     branches: [ master ]
> > jobs:
> >   test:
> >     [...]
> >   
> >   build:
> >     if: startsWith(github.event.ref, 'refs/tags')
> >     needs: test
> >     runs-on: ubuntu-latest
> > 
> >     steps:
> >     - uses: docker/build-push-action@v1
> >       with:
> >         username: ${{ secrets.DOCKER_USERNAME }}
> >         password: ${{ secrets.DOCKER_PASSWORD }}
> >         repository: myorg/myrepository
> >         tag_with_ref: true
> > ~~~
> > {: .output}
> > {: .solution}
>
>
> {: .challenge}

