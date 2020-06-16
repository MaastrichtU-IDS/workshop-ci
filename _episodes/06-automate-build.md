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

You can add a job to your GitHub Action workflow which will automatically build the Docker image and push it to [DockerHub](https://hub.docker.com/) if the tests pass.

> ## Build and push Docker image
>
> *  Find the **Build and push Docker images** action on the [GitHub Marketplace](https://github.com/marketplace?type=actions): [https://github.com/marketplace](https://github.com/marketplace)
> *  Use the action to automatically build and push a Docker image with tag `latest` if the tests pass. Do the build in a new job named `build`. Use the **Example usage** section in the action readme.
> *  You can safely store your DockerHub username and password using secrets. 
>    *  Go to the ⚙️ **Settings** tab of your GitHub repository
>    *  Go to **Secrets** in the left navbar. 
>    *  Create 2 secrets that will be used by the GitHub Actions workflow: `DOCKER_USERNAME` and `DOCKER_PASSWORD` 🔒
>
> Once a secret has been defined no one (not even you) can read it 🙈, you can still override it though.
>
> > ## Solution
> > {% raw %}
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
> >     needs: test
> >     runs-on: ubuntu-latest
> >    
> >  steps:
> >        - uses: docker/build-push-action@v1
> >       with:
> >         username: ${{ secrets.DOCKER_USERNAME }}
> >         password: ${{ secrets.DOCKER_PASSWORD }}
> >         repository: myorg/my-repository
> >         tags: latest
> > ~~~
> > {% endraw %}
> > 
> {: .solution}
> 
{: .challenge}

It is recommended to avoid rebuilding and publishing a new image at every new push to master. We will now set the build and push job to only be triggered if a new release is created on GitHub (a.k.a tag 🏷️)

> ## Build and push image only when release
>
> *  Add a condition to only push to DockerHub when a release is pushed
> * Use the GitHub tag to tag the DockerHub image
> *  2 solutions are available for this case: 
>    *  using a `if` condition in the GitHub workflow (recommended)
>    *  use a parameter provided by the "Build and push Docker images" action.
>
{: .challenge}

> ## Solution
> {% raw %}
> ```YAML
> name: Test and publish to DockerHub
> on:
>   push:
>     branches: [ master ]
> jobs:
>   test:
>     [...]
>   
>   build:
>     if: startsWith(github.event.ref, 'refs/tags')
>     needs: test
>     runs-on: ubuntu-latest
> 
>     steps:
>     - uses: docker/build-push-action@v1
>       with:
>         username: ${{ secrets.DOCKER_USERNAME }}
>         password: ${{ secrets.DOCKER_PASSWORD }}
>         repository: myorg/my-repository
>         tag_with_ref: true
> ```
> {% endraw %}
{: .solution}