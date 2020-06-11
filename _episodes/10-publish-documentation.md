---
title: Complete and publish the documentation
teaching: 1
exercises: 1
questions:
- "How can I publish documentation for my application?"
objectives:
- "Know how to setup a GitHub repository according to IDS standards."
- "Understand the benifits of templates and how they differ from forking/cloning."
- "Understand how to allow the different levels of access to your repository."
keypoints:
- "No one wants to read your dirty code to understand how to run your application, not even yourself in 2 months."
- "So please publish a short, but exhaustive documentation about how to deploy and use your application."
---

Depending on the size of your application and your use-case you can choose between various options. All the options proposed here are using the Markdown format (the format used by the `README.md`)

> ## Create a simple README.md
>
> *   Complete it with relevant informations you want the user of your application to see first (install, usage, etc)
>
{: .challenge}

> ## Transform your README.md in a simple GitHub Page
>
> *   Choose the best template to display your documentation. We recommend Cayman (clear and wide main page), XXX (generates outline using `## Title 2` and `### Title 3`)
>
{: .challenge}

> ## Create a GitHub Wiki for more details
>
> *   Create an install page
> *   Create a "How to cite" page
> *   Add sidebar and footer
>
{: .challenge}

> ## Create a Gitter chat room
>
> [Gitter](https://gitter.im/) is a service from GitLab which allows to easily create and use public and private chatrooms linked to GitHub repositories. Users can easily connect using their GitHub or GitLab account.
>
> * Login to Gitter using your GitHub account
> * Access the workshop Gitter chat room (**TODO?**)
> * Post a message
> * Check an issue in the activity sidebar
>
{: .challenge}

## Automated and embedded Python documentation with MkDocs

[MkDocs](https://www.mkdocs.org/) is a library to generate and maintain documentation for your Python project.

The generated documentation goes to `docs/`

* You can use [pydoc-markdown](https://pypi.org/project/pydoc-markdown/#description) to generate markdown documentation from your Python source code.
* And add manually written documentation

## Complete documentation website using Docusaurus

For large project you might want to build a complete documentation website with a fancy landing page and dozens of documentations pages written in markdown and ordered in categories.

We recommend to use [Docusaurus](https://docusaurus.io/) from facebook Open Source. Docusaurus is built with React and allows you to deploy a documentation website based on markdown file. Pages, like the landing or help page, can be more customized using simplified JavaScript/React templates.

Docusaurus provides scripts to easily deploy your website to GitHub or GitLab Pages, or using Docker. 

Get started in a few minutes at https://github.com/facebook/docusaurus
