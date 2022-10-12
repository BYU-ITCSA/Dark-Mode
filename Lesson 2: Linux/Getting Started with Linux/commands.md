# Commands
While it is possible to use a desktop environment to have a GUI in Linux, most servers don't have this, and it can be much faster to use a command line to perform tasks. This command line environment is refered to as a **terminal**. Terminals get their name from the old days of computing where an organization would own one large computer, and many people accessed it at the same time by each using their own keyboard and monitor to interface with the computer. In a terminal, you will generally have a prompt. While this may vary by machine, it is often set to `<username>@<hostname or IP address>:<working directory>$`. 

For example, the prompt may look like this:
    cosmo@192.168.1.10:/bin/bash$

In this case, you are logged in as the user with username 'cosmo' on a machine with IP address '192.168.1.10' with a current working directory of '/bin/bash'.


## Navigating the filesystem

A few notes on the Linux filesystem:

Similar to Windows and MacOS, there Linux has files and directories. A directory is just a folder which can contain other files and direcotires. A file is just a chunk of data.

In Linux, everything is a file. This includes things like disks, USB devices, SSH sessions, etc. There is a root directory called '/'. All other files are arranged hierarchically under this root. Each directory has two special files, one being '.' which is a reference to the current directory, and one called '..' which is a reference to the parent directory. All directories are seperated by a '/' in a file path. For example, you will have a directory called 
    /etc/passwd

When using a CLI, your session has a working directory associated with it. By default, it will be
    /home/<current username>
when a session is first started, but you will likely change it as you work.


## Filepaths
When referring to a file, you can either reference it by where it is in relation to the root directory (an absolute reference) or by its location to the current working directory (a releative reference).

### Absolute Filepaths
An aboslute reference always starts with a '/' and a reletive reference will start with another character. For example, if your working directory was `/var/www/` and you wanted to refer to a file called `index.html`, you could use the absolute reference `/var/www/index.html`.

### Relative Filepaths
Alternatively, you could use a relative reference `index.html` which will imply the `/var/www/` at the beginning because that is your working diretory. Alternatively, you could use `./index.html`, `../www/index.html`, or `../../var/www/index.html` which make use of `.` and `..` to refer to the current directory, the parent directory, and the parent directory of the parent directory respectively.

### pwd
pwd stands for '**p**rint **w**orking **d**irectory'. Running this command will print the current working directory to the terminal. For example, if you have just logged in as a user called 'cosmo', it will look something like this:

    cosmo@localhost:~$**pwd**
    /home/cosmo/
    cosmo@localhost:~$

### ls
ls is short for **l**i**s**t', and will print a list of all files and directories in the directory referenced. If no directory is referenced, it will default to the working directory. For example:

    cosmo@localhost:~$**ls**
    my_diary.txt    cool_things.txt notes.txt
    cosmo@localhost:~$

Common arguments:

ls <filepath>: This will list the files located in the directory located at the filepath specified.

Common flags:

-l
The `-l` flag will print all of the file permissions as well as the owner of the file or directory for each item contained in the directory

-a
The `-a` flag will print *all* files in the directory including hidden files (files that start with a `.` are hidden by default).

### cd
The `cd` command stands for '**c**change **d**irectory'. It is used by giving it a path to a directory.  It will change your current working directory to the one specified. For example:

    cosmo@localhost:/var/www$**cd ..**
    cosmo@localhost:/var$

## Viewing/editing files

### touch
The `touch` command will create a file with the specified name. It is used like this:

    cosmo@localhost:~$**ls**
    file.txt    new_file.txt
    cosmo@localhost:~$**rm new_file.txt**
    cosmo@localhost:~$**ls**
    file.txt

### rm
The `rm` command will remove a file (it doesn't work with directories unless certain flags are used). It is used like this:
    cosmo@localhost:~$**ls**
    file.txt    new_file.txt

Common Flags:
-r or --recursive
The -r flag will delete all files and folders in a directory by going into each subdirectory recursively. 

-f or --force
The -f flag is used with the -r flag. When the -r flag is used, it asks the user whether they would like to delete each file. The -f flag supresses those prompts and just deletes them.

>#### ⛔ **WARNING:** Be extremely careful where you run a `rm -rf <directory>` command. While it is extremely useful in some situations, it will instantly start deleting files. There are memes about running `sudo rm -rf /`. This will delete every file on the computer. Most distributions require an additional flag to do this, but you should not count on that.

### rmdir
The rmdir command is similar to rm, but can only remove empty directories instead of files. If you get an error that the directory is not empty, but it looks like it is, check for hidden files with `ls -a <directory>`

### cat
Cat is short for con**cat**enate, and will print the contents of a file to the terminal. You can give it multiple arguments, and it will print the entire contents of each file one after the other. For example,

    cosmo@localhost:~$**cat my_diary.txt cool_things.txt**
    Dear diary, today I learned how to use Linux!
    Cougars
    Cookies and Cream Milk
    Cougar tails
    cosmo@localhost:~$


### head

Head will print the top few rows of a file. This is especially useful if you want to check the top few lines of a file such as a title of a document. You can give it multiple file names if you want to look at the top few lines of multiple files.

Common flags:

-n <number> or --lines <number>
The -n flag will print the first <number> lines of the file instead of 10, which is the default.

### tail
Tail is similar to head, except it prints the *bottom* few lines of a file.

Common flags:
-n <number> or --lines <number>
The -n flag will print the first <number> lines of the file instead of 10, which is the default.

-f or --follow
The -f flag will *follow* the file, meaning that it will print the last few lines of the file, but will keep running and print any additional lines that get appended to the file. This is *extremely* useful for watching logs. For example, you may follow a logfile of a webserver to watch for specific types of events.

### Grep

Grep stands for **g**lobal **r**egular **e**xpression **p**rint. It will take an input, filter it with a regular expression, then print it to the output. It is used to help filter through files to find information you are looking for. Check the section on the '|' operator for examples on usage.

### nano
Nano is a command line text editor included with many distributions. It is used `nano <name of file>`. By default, it will open a file if it exists, and will create a file with that name if it doesn't. To exit, you need to press ctrl+x. If you have any unsaved changes, you will be asked if you'd like to save them, then the name of the file you would like to use (automatically filled if you specified a filename). 

>#### ⚠️ **Note**
>If you accidentally use ctrl+c or ctrl+z while using nano, see the section below on what those commands do.

### vi/vim
Vi and Vim are text editors that are included with most Linux Distributions. They are famously a little tricky to exit. This is because vim has several modes of operation, and you can't exit from all of them. There are a lot of customization options you can use to make vim an extremely powerful editor.

Normal Mode
You can enter Normal mode by pressing the esc key. In this mode, you can move the cursor around to browse a file and modify only single characters.

Insert Mode
To enter insert mode press 'i'. This will allow you to insert characters as you would expect. To exit this mode, press esc.

Command Mode
To enter command mode, press ':'. There are a lot of commands that you can run to help edit files. To quit vim, press :q (for **q**uit) and hit enter. To save your changes, do :wq (for **w**rite and **q**uit) instead. To discard changes, type :q!.

## Running Applications
Applications are generally stored in one of a few places, one of which is `/bin/bash`. In this directory, you will find executables that run programs when you type their name on the terminal. For example, there are files for pwd, cd, and ls. When you type anythint into the terminal, it looks in these locations to see if there is an executable application with that name. If one is found, it will run that application with any specified arguments and flags.

### stdin, stdout, and stderr
Each running application in Linux has three data streams: stdin, stdout, and stderr with stdin standing for **st**an**d**ard **in**put, stdout standing for **st**an**d**ard **out**put, and stderr standing for **st**an**d**ard **err**or. Each one can be thought of as a stream of characters or bytes. By default, stdin prompts the user for input (though there is not always an indication that the user needs to input anything) and stdout prints text out to the terminal. stderr also prints to the terminal, but it is normally used only when an application encounters an error. Depending on your terminal software, other visual cues (such as a different font color) may be used when printing things from stderr. If you have written code that reads input from a terminal, you are reading from stdin, and if you have printed things to the terminal, you are writing to stdout. If an exception is thrown, that is generally printed to stderr.

### Arguments
When running a command, you are able to add optional settings that get passed to the program. These settings are used by the program, and will change how it executes. The example above with `ls` are an example. Often, there are two options for arguments, a long option which is more verbose but clear and a short option that is shorter but less clear. For example `ls -a` does the same thing as `ls --all`. The short option is generally a single letter, and can be combined with a single dash or left seperate. For example `tar -xvf archive.tar.gz` is the same as `tar -x -v -f archive.tar.gz`. Note that arguments must be seperated by spaces. The short option is often refered to as a flag, though the terms argument, flag, and option can all be used to refer to the long or short version.

### Return Values
All applications have a return code. If the program finishes and exits without any errors, code '0' should be used. If any other exit code is used, you will generally get a message in stderr. If you've ever wondered why c++ has the main function declared as an int (which returns an int) it is because that function is will return the return code for the whole application.

>#### ⚠️ **Note**
>When attempting to execute a file in the current directory that has the same name as another command, you need to specify that you want to run that version. You can do this by using the full filepath. For example, you could run an executable called `python3` in the current directory using `./python3 <arguments>`


## Piping
One of the most powerful features of Unix which Linux inherited is the command pipeline. On a most basic level, it allows you to change the source of stdin and the destination of stdout. One common usage of this is to redirect the stdout of one application to the stdin of another application. This allows you to combine small programs that each do one small thing to make a pipeline to process data. There are a few operators you can use.

### > and >>
The `>` operator will redirect stdout of application on the left of the '>' to a file instead of printing it to a terminal. It will *overwrite* the current contents of the file (this will also delete the file if you try to process a file then write it with the same filename. This is because redirection will truncate the file *before* the application runs).

The `>>` operator works similarly, but will instead *append* the data to the end of the file.

### |

The pipe character `|`, also called a vertical bar. It is used to redirect the stdout of one application into the stdin of another application. This allows a lot of fun things. One common one is looking through files for specific things. For example, in a CTF competition, you may be looking for a flag in a format `not_a_real_ctf{<flag>} where you don't know what <flag> is supposed to be in a file called `findme.txt` which has thousands of lines of gibberish. You could find the flag by using `cat` to print the contents of the file, but using a | to send it in to `grep` to filter the output with a regular expression (regular expressions are complicated, so for now, just pretend it is filtering based on a literal string). This would look something like this:

    cosmo@localhost:~$**cat findme.txt**
    Never gonna give you up
    Never gonna let you down
    Never gonna run around and desert you
    ... (output truncated)
    cosmo@localhost:~$**cat findme.txt | grep not_a_real_ctf{**
    not_a_real_ctf{this_is_a_flag}
    cosmo@localhost:~$

### &
The `&` operator will run the command to its right in the background, and immediately exit with code 0. This allows you to run a command in the background with `<command> &` which lets you use your terminal while it executes. You can also run mutliple commands with `<command1> & <command2>` where command1 runs in the background, and command2 runs at the same time in the terminal.

### &&
The `&&` operator is completely different from the `&` operator. When you run `<command1> && <command2>`, command1 will execute, then if it returns with status code 0, command2 will run. If command1 returns a non-zero exit code, command2 will never run. This is useful when you have a few commands which depend on earlier ones to complete such as `sudo apt update -y && sudo apt upgrade -y`. One fun example of a good use of it is `cd some_dir && rm *`

### ||
The `||` operator is similar to `&&` except the second command will only run if the first one returns a non-zero status code.

### <
The `<` operator allows you to read stdin from a file instead of from the terminal. For example, if you wanted to run a program with specific inputs every time, you may put them in a file, then read them like `python3 my_application.py < test_inputs.txt`.

### Other operators
There are other operators that can be useful, but they are generally less common than the ones listed here.

## Permissions

## Switching Users

### who

### whoami

### su

### sudo

## Installing Software

## Misc

### * and .

### Ctrl + c

### Ctrl + z

