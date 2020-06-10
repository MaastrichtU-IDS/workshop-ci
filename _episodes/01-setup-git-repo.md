---
title: Setup Git repository
teaching: 1
exercises: 1
questions:
- "What do I need to think about when creating a new repository on GitHub?"
objectives:
- "Know how to setup a GitHub repository according to IDS standards."
- "Understand the benifits of templates and how they differ from forking/cloning."
- "Understand how to allow the different levels of access to your repository."
keypoints:
- "When creating a GitHub repository keep permissions in mind."
- "Templates are a quick way to scaffold your application."
---

Setting up a GIT repository should always be the first step for any software related project. For the many advantages of using GIT check !!here!!. While there are many options for hosting your repository, the default choice at IDS is GitHub. Some of the advantages of using GitHub are features like free processing power, free artifact hosting, a large community and having all IDS repositories searchable under the same organisation. 
When first setting up a GitHub repository, there are a number of things to consider:
- Is there a template I can use to save time setting everything up?
- Who will have permissions to read/write/administrate this repository?
- Do I have SSH keys configured?

Create and setup GitHub repository: setup SSH key, create repo from template, manage access of the created repository, give maintainer access of the created project to ids-developers team)

## GitHub templates

GitHub templates are a quick way to start your application with the scaffolding already in place. This can save a lot of time as you don't have to worry about setting everything up. This could also be achieved by forking a repository. However forking is meant more for collaborating on the original repository. In the case of using a template you will not include the entire commit history of the original project for example. It's a fresh start as if you had simply copy pasted the code into a fresh repository. At IDS we have a number of templates ready to use for Python, Java and React websites.

> ## Create a repository from template
>
> * In [GitHub](https://GitHub.com), Use the **+** icon to create a new repository. 
> * Choose the MaastrichtU-IDS/workshop-ci-template from the repository template dropdown.
> * Select MaastrichtU-IDS as the owner of the repository.
> * Add a name and description to your repository and leave the access on *private*. 
{: .challenge}

## Repository permissions

GitHub diffferentiates between 5 different types of access:
- **Read** - for users who only need to view or discuss the code.
- **Triage** - Allows users to do minor administrative tasks such as modifying issues and requesting reviews.
- **Write** - Allows users to push code to the repository and setup GitHub actions.
- **Maintain** - Allows users to do more potentially destructive things such as pushing to protected branches. 
- **Admin** - Allows users to do anything, such as deleting or transferring the repository.

Check [here](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/repository-permission-levels-for-an-organization) for a detailed overview. To save time, GitHub allows organizations to create teams of usersfor which permissions can be handled in one go. 

> ## Configure repository permissions
> *   Under *settings* for your repository, go to **Manage access**.
> *   Click **Invite teams or people**.
> *   Add the MaastrichtU-IDS/developers team and provide them with *Write* access.
> *   Add the MaastrichtU-IDS/admins team and provide them with *Admin* access.
{: .challenge}

SSH keys provide an easy way to access your GitHub repositories without having supplying your username and password every time. This is done by generating a *keypair*, publishing the public key on GitHub and storing the private key locally on your machine.

> ## Clone repository using SSH
>
> * Follow the [instructions](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to generate a keypair for your operating system.
> * Follow the [instructions](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account) to upload the public key to GitHub.
> * In your repository, click **Clone or Download** and make sure *Clone with SSH* is selected. 
> * Copy the url to your clipboard and in a terminal perform ```git clone URL``` in the path of your choice. The name will be set to the repository name by default.
{: .challenge}

{% include links.md %}