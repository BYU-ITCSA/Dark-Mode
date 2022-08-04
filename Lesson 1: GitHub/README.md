# Source Control

Steven Palica

---

## What is source control?

Acording to [Amazon](https://aws.amazon.com/devops/source-control/)
>Source control (or version control) is the practice of tracking and managing changes to code. Source control management (SCM) systems provide a running history of code development and help to resolve conflicts when merging contributions from multiple sources.

### Why is source control important?
Have you ever needed to make a change to a file, but wanted to keep a previous version? Have you ever worked on a group project where everyone needed to be able to work on it both at the same time *and* individually? Have you ever needed to keep track of multiple versions of a document? Have you ever needed to keep track of who edited a document?

If you answered *yes* to any of those questions, you are not alone. In fact, these were many of the same issues early programmers ran into when developing software. Source control applications meet many of these needs. One of the main ones used in the industry is Git.

## What is Git?

According to [Git](https://git-scm.com/)
>Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. 

Git allows you to create a *repository* (also called a *repo*) to store files. Anyone with access may *clone* the repository to create a local copy of the files. A *branch* is used to keep changes from adversely affecting each other. While working on a branch, you may need to *commit* then *push* any changes you make to the *remote*. Anyone else working on the project can *pull* the repository to see your changes. Once changes have been tested, you may *merge* the branch with another to put it into production.

### What is a Repository?
A repository is a selection of files that you want to track. Generally, these files contain source code and documentation, but they can contain any files. While not required, it is useful to use a service like GitHub (a company owned by Microsoft) to store a copy of the repository on the internet. This allows anyone with an internet connection to access the repository.

### What is cloning?
When you first need to work on the files in a repository, they exist within the repository, but you don't have a copy of the files on your computer. To download a copy, clone the repository. This downloads a copy of the files to your computer, but also downloads information about the repository in a folder named `.git`. This folder contains things like the branch name and where the remote repository is located. You can clone a repository with

~~~
git clone <url to repository>
~~~

For example, you can download a copy of this repository using

~~~
git clone https://github.com/BYU-ITCSA/Dark-Mode.git
~~~

### What is a branch?
A branch is a divergence from the main line of code so changes can be made without affecting the main line. When a repository is created on GitHub, it automatically creates a branch called `main`. You can create additional branches using the command

>#### ⚠️ **Note**
>In older documentation and repositories, the `main` branch may be referred to as `master`. The industry is tending toward replacing the terms `master` and `slave`. They generally get replaced with `main` or `primary` and `secondary`.

~~~
git branch <new branch name>
~~~

This will create a branch based on the current commit you have locally on your computer.

You can switch to a different branch that already exists using

~~~
git checkout <existing branch name>
~~~

You can create a new branch *and* switch to it using

~~~
git checkout -b <new branch name>
~~~

You can delete an existing branch using 

~~~
git branch -d <existing branch name>
~~~

Once you are done working in a branch and need to move your code into the `main` branch, you will need to do a merge (see below).

### What is a commit?

A commit is a state of the repository at a specific place in time. For changes to a file to be included in a commit, you must add it to the commit using the `git add` command like this

~~~
git add <filename to add>
~~~

>#### ⚠️ **Note**
>The `git add` command will add the *current* version of the file to the commit. If you change the file again after adding it, you will need to add it again

For files to be included in the next commit, the changes must be staged first. The `git add` command will automatically stage the current version of the file. It is not required to stage all of the changes you have made. 

You can have a `.gitignore` file to automatically ignore specific files (or types of file). It supports a simplified regular expression, and can use wildcards. This is useful for libraries that will be downloaded on the production system when the code is deployed, such as the `node_modules` directory in a NodeJS application or for test data that you don't want copied to production.

A commit message is *required* when making a commit.

>#### ⚠️ **Note**
>If your application has credentials stored (such as a database password or API key), make sure to have them in a seperate file from your code (like a `.env` file). This way, you can put that file in `.gitignore` so you don't accidentally push credentials somewhere they can be accessed publicly. There ***have*** been data breaches caused by this. See note below if you accidentally do this.

It is also possible to unstage a staged file using

~~~
git restore --staged <file to unstage>
~~~

You can unmodify a file (revert it to its state from the previous commit) using

~~~
git restore <file to restore>
~~~

This will discard any changes, and is useful for recovering to a previously working version of that file.

>#### ⛔ **WARNING:** using the `git restore` command will remove ***all*** changes to the file in the local filesystem and overwrite the file with the last committed version.

### What is merge?

When you have made an update to your repository, you may want to combine the new changes you have made with another branch of code (for example, to update an application in production). To do this, after committing all of your changes, switch to the branch you want to copy the code into

~~~
git checkout <name of branch>
~~~

Then, to merge the changes from the other branch, run

~~~
git merge <name of other branch>
~~~

As long as you haven't made changes to the same part of code in both branches, this is all you should need to do. If you *did* make changes to both branches, you will need to resolve the conflict since Git doesn't know which changes should be used. 

If this is the case, you will get a message like this

~~~
Auto-merging <file with conflicts>
CONFLICT (content): Merge conflict in <file with conflicts>
Automatic merge failed; fix conflicts and then commit the result.
~~~

You can use the git mergetool with

~~~
git mergetool
~~~

Once merge conflicts are fixed, you need to use `git add` to add the file again, then `git commit` to finish the merge.

---

## What is a remote?
Remotes are where Git starts to really shine. All of the previous commands and tools can be used on a single workstation to great effect. A remote allows much better collaboration on a repository.

When you clone a repository, it automatically adds a `remote origin` for it. When you run any of the following commands, it interacts with all remotes (for large or complex projects, there can be more than one)

### What is a push?
When you have a commit that you like, and would like to upload it to a central server (such as GitHub), run

~~~
git push
~~~

This will upload all commits to all branches to the remote(s). In many DevOps jobs, there are hooks on the remote that will take other actions when this occurs.

### What is a pull?
A pull will copy any changes from the remote to your local computer. If you have local changes on your computer that haven't been pushed to the remote, and the remote has changed since you last pulled, see the below section on this issue.

### What is fetch?
Fetch is used to check for updates to the remote. It is similar to a pull, but only pulls the list of changes, not the files themselves.

---

## Additional Items
Here are some additional things you can do with Git or GitHub (remember, Git is the software, GitHub is a specific online service that allows you to store repositories on the internet using Git).

### What is a pull request?
A pull request is when a repository pulls changes from another source. For example, if you use an open source tool, and want to add functionallity to it, you can clone the repository, make the changes, then submit a pull request. Your code should then be reviewed, then your changes will be pulled into that repository for others to use.

### What is the difference between a private and a public repository?
A public repository is open for everyone to see without authentication. Open source software will often be available in a public repository. 

A private repository is only visible to people who are authenticated and autorized to view that repository.

On both public and private repositories, read and write permissions are seperate. Only those who are given write permission can push to the repository (at least on the remote).

>#### ⛔ **WARNING:** Most professors ask you not to store code in public repositories. If you do work for class, use a private repository unless you have permission to post it publicly.

### CI/CD Pipelines
Continuous intergration/ continous development practices often employ *pipelines*. These are common, and allow automated processes to occur when you push code. You may have a staging branch where you push code you want to put into production. The code may automatically be deployed to a test environment, run a suite of software tests to check stability, then automatically push to production if it passes all of the tests. This can drastically improve development speed, something which is important in commercial development.

---

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

### Accidentally commiting credentials or API keys to a repository

Due to the nature of Git, any committed changes will be stored indefinitely, even if you delete them in a later commit. This can be a massive security problem if not resolved.

If you haven't committed the changes yet, you should be fine to edit any files as needed before commiting.

If you have commited the changes, but have not yet pushed them anywhere, use

~~~
git commit --amend
~~~

This command will replace the previous commit with any changes you have made. Remove any sensitive data, and run this command.

If you have already pushed changes to a remote, you should ***always*** consider this information compromised. Revoke any access keys, and reset any passwords immediately. This should remove any access that could be gained using the sensitive data. After this is complete, add any files with sensitive data in them to `.gitignore`. Ideally, you should have a seperate file for credentials that is not tracked in your source control. 

If you really must remove the old key, the easiest way may be to create a new repository with `.gitignore` set up correctly, copy your code to the new repository, then delete the old repository.

If you don't want to do this, there are tools to remove a file from the complete Git history. See [this link](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) for more info.


### I cannot clone a private repository by authenticating with my username and password

If you use only the command line, you are normally prompted for your username and password to push to or pull from your remote. If you are using GitHub, they have changed their process. You will need to create a personal access token on their web portal, then use that as the password while authenticating. Documentation for creating a token can be found [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). 

### I don't want to type in my username and access token every time I want to interact with my remote

Great news! You can have Git cache your credentials! 

Just use 
~~~
git config --global user.name "<your git remote username>"
git config --global user.password "<your git remote password OR personal access token>"
~~~

This will cache your credentials for five minutes. To permenantly store them, use 

~~~
git config --global credential.helper store
~~~

then authenticate once.

>#### ⛔ **WARNING:** This method stores credentials in plain text. If you are using personal access tokens, there is no way to retrieve them after they are first created anyway. If you were already going to save it for future use, this may not be an issue. If in doubt, use the first option.

### I have local changes, and cannot pull from a remote

I highly recommend checking out [this](https://happygitwithr.com/pull-tricky.html) site. Depending on what your local changes are, and whether or not they are already commited can make a fairly big difference. This site covers most cases.

## Fun facts

Git was invented by Linus Torvalds, the guy who invented and still maintains the Linux kernel.

Linus (jokingly) says that since Linux was named after him, he continued the trend with Git. (A self burn. Those are rare.)

## Additional resources

[Linus Torvalds speaks about Git at Google](https://www.youtube.com/watch?v=4XpnKHJAok8)