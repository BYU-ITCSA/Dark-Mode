# Source Control

Steven Palica

## What is source control?

Acording to [Amazon](https://aws.amazon.com/devops/source-control/)
>Source control (or version control) is the practice of tracking and managing changes to code. Source control management (SCM) systems provide a running history of code development and help to resolve conflicts when merging contributions from multiple sources.

### Why is source control important?
Have you ever needed to make a change to a file, but wanted to keep a previous version? Have you ever worked on a group project where everyone needed to be able to work on it both at the same time *and* individually? Have you ever needed to keep track of multiple versions of a document? Have you ever needed to keep track of who edited a document?

If you answered *yes* to any of those questions, you are not alone. In fact, these were many of the same issues early programmers ran into when developing software. Source control applications meet many of these needs. One of the main ones used in the industry is Git.

## What is Git?

According to [Git](https://git-scm.com/)
>Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. 

Git allows you to create a *repository* (also called a *repo*) to store files. Anyone with access may *clone* the repository to create a local copy of the files. A *branch* is used to keep changes from adversely affecting each other. While working on a branch, you may need to *commit* then *push* any changes you make to the repository. Anyone else working on the project can *pull* the repository to see your changes. Once changes have been tested, you may *merge* the branch with another to put it into production.

### What is a Repository?
A repository is a selection of files that you want to track. Generally, these files contain source code and documentation, but they can contain any files. While not required, it is useful to use a service like GitHub (a company owned by Microsoft) to store a copy of the repository on the internet. This allows anyone with an internet connection to access the repository.

### What is cloning?
When you first need to work on the files in a repository, they exist within the repository, but you don't have a copy of the files on your computer. To download a copy, clone the repository. This downloads a copy of the files to your computer, but also downloads information about the repository in a folder named `.git`. This folder contains things like the branch name and where the remote repository is located. 

### What is a branch?
A branch 

### What is a commit?

### What is a push?
### What is a pull?
### What is merge?
### What is fetch?
### What is a pull request?
### What is the difference between a private and a public repository?

### What is .gitignore?


## Common problems

### Setting username and email
Before you are able to commit any changes, you need to set your name and email. This can be done with the following commands:

~~~
git config --global user.name "<Your name>"
git config --global user.email <Your email address>
~~~
For example, if your name were Cosmo Cougar, you might use:
~~~
git config --global user.name "Cosmo Cougar"
git config --global user.email cosmo.cougar@example.com
~~~

## Fun facts

Git was originally invented by Linus Torvalds, the guy who invented and still maintains the Linux kernel.

## Additional resources
