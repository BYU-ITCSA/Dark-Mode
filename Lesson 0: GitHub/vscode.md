# Source Control in Visual Studio Code

## Introdution
While some developers want to flex by saying they only code using Vim, Emacs, Nano, or some other command line text editor, this way of thinking can be extremely wasteful. When using an IDE (integrated development environment), many quality of life features are built in, or can be added. After all, the people who created the IDE want a good experience writing code too!

One IDE that has gained a lot of popularity in the last several years is Visual Studio Code. This tutorial acts as an extension of the Git tutorial and shows how to use the source control built into VSCode.

## Installation
Out of the box, VSCode has Git support, though Git does need to be installed on your computer for this to work. You can check if Git is installed by running the command

~~~
git --version
~~~

## Local Usage
There are many features within the VSCode for managing repositories locally. This image will be referenced for locations of interface elements

![Sidebar](vscode.png)

### Area 1
On the image, area 1 (left edge) is the source control tab (hotkey ctrl+shift+G). This will open area 2.

### Area 2

>#### ⚠️ **Note**
> If you have a single file or a folder open that doesn't have a .git folder in it, VSCode will not see your repository. Instead, this area will have options to open a folder with a repository, clone a repository, create a repository, or publish the folder to GitHub.

Area 2 (top left, away from the edge) has several elements. Above it are a few quick buttons
* View as tree/View as list - changes the view of the files to show them as a flat list, or in their file structure
* Commit - Commits the code. If you do not have a commit message, it will open a file detailing the changes in this commit. You should enter a message in this file.
* Create pull request - this allows you to request someone to pull your changes into their version of the repository.
* Refresh - checks for additional changes to the repository
* More actions - has a list of additional repository options such as cloning a repository, pushing, pulling, branching, etc.

To simply commit your changes locally, type a message into the message box at the top of area 2 and click the Commit button. You can use the dropdown on the button to instead commit then push, or to commit then sync.

### Area 3 
Area 3 (left edge of the code window) is a series of colored bars. The color denotes any changes to this file since it was last committed. The colors may change depending on the theme you are using. They can denote lines that have been added, modified, or removed. In the example, only line 1 was included in the previous commit, and the rest of the lines have been added to the file.

### Area 4
Area 4 (bottom left corner) is the most useful if you are planning on storing your code on a remote such as GitHub. The left button allows you to change branches. The center button allows you to sync (sync will run a pull, then a push). The lefthand number next to the down arrow indicates how many commits will be pulled from the remote. The righthand number next to the up arrow indicates how many commits will be pushed to the remote. The numbers to the right of that indicate errors and warnings in your code, and are not part of the source control features.

## Recommended Usage
In my experience, the easiest way to use these features are to do the following:
1. Create a new repository in GitHub
2. Go to the source control tab and select the option to clone a repository. 
3. When the prompt appears at the top of the screen, select the option to clone from GitHub. If you are cloning from GitHub, you may need to take a few extra steps to sign in to your account. If you are already signed in, you should be able to search all of your repositories.
4. Save the repository somewhere you can find it. 

>#### ⛔ **WARNING:** ***Really*** weird stuff happens if you save a repository inside another repository. I **HIGHLY** recommend against doing this.

5. When you finish a feature or are done writing code for a while, commit all your changes, and push them to GitHub. If you are working in a group in a single branch, you may want to coordinate when you push to the remote to not introduce errors. If you are the only one pushing to that repository, you should be fine to commit and push whenever you want.

## A Few Notes
When you first use VSCode, you may be prompted to stage changes before commiting them. You can set it to automatically stage and commit. This will save a few clicks every time you commit, and there isn't really any harm in doing this.

You may also be prompted to periodically run a fetch. This is also fine. A fetch will not pull any code, it will only inform you of changes to the the remote. You can then pull them if you want.