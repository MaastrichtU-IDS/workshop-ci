---
title: Automate the publication of your package using GitHub Actions
teaching: 1
exercises: 1
questions:
- "What do I need to think about when creating a new repository on GitHub?"
objectives:
- "Know how to setup a GitHub repository according to IDS standards."
- "Understand the benifits of templates and how they differ from forking/cloning."
- "Understand how to allow the different levels of access to your repository."
keypoints:
- "Use template provided by GitHub."
- "Set PyPI credentials in GitHub Secrets."
- "Add a version badge to display the latest version available on PyPI in your README."
---

The best way to make your application FAIR (Findable Accessible Interoperable and Reusable) is to publish it as a package in a popular repository. In the case of Python packages, the reference repository is [PyPI](https://pypi.org/) (pronounce Pie-Pea-Eye).

You just need to register providing a valid email address and a username, then the project will be automatically created and you will be set as its owner if the chosen project name has not already been taken.

> ## Automatically publish to PyPI
>
> *   Add a new job named `publish`. Similarly to the build Docker job, this job will be triggered only if a release/tag is pushed.
> *   Use the template **Publish Python Package** provided by GitHub in your repository **Actions** tab (which uses `twine`).
>*   Define `PYPI_USERNAME` and `PYPI_PASSWORD` Secrets 🙈
> 
> > ## Solution
> > ```YAML
> >   publish:
> >     if: startsWith(github.event.ref, 'refs/tags')
> >     needs: test
> >     runs-on: ubuntu-latest
> > 
> >     steps:
> >     - uses: actions/checkout@v2
> >     - name: Set up Python
> >       uses: actions/setup-python@v2
> >       with:
> >         python-version: '3.x'
> >     - name: Install dependencies
> >       run: |
> >         python -m pip install --upgrade pip
> >         pip install setuptools wheel twine
> >     - name: Build and publish to PyPI
> >       if: startsWith(github.event.ref, 'refs/tags')
> >       env:
> >         TWINE_USERNAME: ${{ secrets.PYPI_USERNAME }}
> >         TWINE_PASSWORD: ${{ secrets.PYPI_PASSWORD }}
> >       run: |
> >         python setup.py sdist bdist_wheel
> >         twine upload dist/*
> > ```
> {: .solution}
> 
{: .challenge}

> ## Publish a new release
>
> *  Publish a new release to trigger the newly created publish job and publish the first version of your package! 🏷️
>
{: .challenge}

> ## Add version badge
>
> *   Add a badge getting the latest version from PyPI to your project `README.md`
>
> ```markdown
> ![Version](https://img.shields.io/pypi/v/my-package)
> ```
>
{: .challenge}