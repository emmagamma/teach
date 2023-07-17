##### Before continuing, make sure you've gone through the steps in the previous guide:

---

> [Setup your Environment](README.md)

---

# Info and Background, working with Bash

In the previous guide, we set up WSL for windows, meaning we can just use bash for all systems going forward rather than doing things in powershell separately.

Something worth noting about using bash, is that most of the time if a command is successful it won't generate any output at all. This may be a little confusing at first, but there are often other commands available to check on the results and verify that things worked as expected if you really need to. Generally speaking though, if there's an error it will be very obvious when the command terminates and spits out a bunch of text about what went wrong.

Another thing to think about is that, often times typing commands slightly wrong could have very bad unintended consequences depending on what you're trying to do. As a rule of thumb I always sort of pause for a moment before pressing enter to actually run a command, I'll just scan it and verify that everything was typed correctly. You'll speed up as you get more familiar, but there's absolutely nothing wrong with taking your time and making 100% sure it's correct.

## bash configuration

When you open a new terminal window, it should log in as your user and run your `~/.bash_profile` file which can contain bash code to configure your sessions. In addition each time you open a new tab it starts a new session logged in as your user, and will run your `~/.bashrc` which is very similar to your bash profile in that it can contain arbitrary bash code and further configures the same environment.

If you're using Zsh and Oh My Zsh, then your `~/.zshrc` and `~/.zprofile` files will also re-run in a similar fashion.

After making changes to these files, we can run any of the following commands to have that specific config file refresh in the current session instead of requiring us to open a new tab:

```bash
source ~/.bash_profile
source ~/.bashrc
source ~/.zprofile
source ~/.zshrc
```

<br />

## file system and folder structures

I've used the path `~/` several times now, so let's talk about what that means in bash. We'll come back to expand on what this means after filling in some related details, but for now I'll just mention that `~/` points to the home directory or home folder. 

Regardless of which OS you're using, your file system is a type of tree structure, this means that one thing contains other things and those things can contain **more** other things and so on. You've seen plenty of tree structures before, including trees themselves. But think this:

```
     G
   /   \
  A     I
 / \   / \
L   Y  R  F
      / \  \
     L   D  T
```

...representing the shared structure of the words: Gal, Gay, Girl, Gird, and Gift.

Except in a file system, we have folders rather than just letters and those folders can contain files and other folders.
Intuitively I think most of us know this but it helps to be explicit about things.
Every file system, like every tree structure, has a root node or in the case of a folder structure a root folder.

<br />

## change directory

We can navigate to the root, the topmost level, where everything else about your system is contained, by running the following command:

```bash
cd /
```

`cd` is short for change directory, and it should be followed by whitespace and then a path

`/` is the path in this instance, and is just the convention in bash to point to the root folder, similarly to how `~/` is a convention to point to the home folder for the currently logged in user.

For most versions/distros of linux, the absolute path from the root directory to your home folder would be:

`/home/WhateverYourUsernameIs/`

However on macOS, it'll be:

`/Users/YourUsername/`

But in either case you can just use:

`~/`

to point to your home folder.

---
> **NOTE about paths**

> the first `/` on the left is our root folder, however the trailing forward slash on the right `/` is just denoting that `WhateverYourUsernameIs` is a folder not a file, and it's optional. So `/Users/YourUsername` and `/home/WhateverYourUsernameIs` would also be valid paths.

---

so to go to our home folder you'd use:

```bash
cd ~/
```

We can also just run `cd` with no path provided, and it will take you to your home directory by default.

```bash
cd
```

to go up one level to the containing directory, we can use `../`

```bash
cd ../
```

<br />

## listing out the contents of the current directory

the `ls` command, short for list, lets us see all the files and folders at our current location in the folder structure:

```bash
# gives you a list of file names and folder names
ls

# list everything, and give me more info about each file
ls -al

# the flag -a means list everything including hidden files and dotfiles (files beginning with .)
# the flag -l short for "long format", meaning it shows other information beyond just file names
# such as read/write/execute permissions, owners and groups, file size, and more

# provide a path to list out all the files and folders contained there
ls /etc/

# or show metadata and hidden files at a given path
ls -al /etc/

```

<br />

## make a new directory

We can create a new directory with the `mkdir` command, short for "make directory",
passing it a name for our folder afterwards, like so:

```bash
# will create a folder named `Code` in whichever folder you're currently in
mkdir Code

# equivalent to above, ./ is the convention for relative paths starting from the current directory
mkdir ./Code

# perhaps more reliable, we know that no matter where we've cd'd into
# this will create the `Code` directory, directly under our home folder
mkdir ~/Code
```

I highly recommend keeping a folder to contain all your git repos in one place, but you can call it whatever you like.

Now let's cd into our Code dir, and create another directory inside of it for your first project.

```bash
# go into the Code folder
cd Code

# make a new folder
mkdir BabysFirstProject

# go into our new folder
cd BabysFirstProject
```

or instead you could do it in just two commands:

```bash
# make the new folder inside the Code folder
mkdir ~/Code/BabysFirstProject

# go into the new folder
cd ~/Code/BabysFirstProject
```

<br />

## other useful commands:

A list of all default commands in bash on linux can be seen here: https://ss64.com/bash/

Or go to the main site and click on your OS to see a list of commands available to you: https://ss64.com/

We'll highlight a few here and provide usage examples...

---

`man` : short for "Manual", prints out detailed documentation for a given command.

```bash
# yo dawg, did u know you can man the man command to see the manual page for the manual pages? lol
man man

# show manual page for whoami
man whoami
# WHOAMI(1)                                          General Commands Manual                                         WHOAMI(1)
# NAME
#      whoami – display effective user id
# SYNOPSIS
#      whoami
# DESCRIPTION
#      The whoami utility has been obsoleted by the id(1) utility, and is equivalent to “id -un”.  The command “id -p” is
#      suggested for normal interactive use.
#      The whoami utility displays your effective user ID as a name.
# EXIT STATUS
#      The whoami utility exits 0 on success, and >0 if an error occurs.
# SEE ALSO
#      id(1)
```


---

`pwd` : short for "Print (full path to the) Working Directory" and will give you the absolute path from root to wherever you currently are.

```bash
# just show the path of the current working directory that we're cd'd into
pwd 

# should give you an absolute path even if you use a relative path, like:
pwd ./some/relative/path
# /home/username/some/relative/path
```

---

`touch` : create a file.

```bash
touch fileNameGoesHere.whatever
```

---

`cat` : short for "Concatenate", print (display) the content of files

```bash
# list contents of one file
cat ~/.zshrc

# list contents of multiple files
cat <file-path-one> <file-path-two> <file-path-three>

# list contents of all text files
cat *.txt

# list contents of all files named thing, regardless of file extension
cat thing.*
```

---

`cp` : short for "Copy", give it two file paths separated by whitepsace to copy a file from the first path to the second path

```bash
# if the second path is just a directory, you can leave out the file name and it will default to the same file name
cp fileNameGoesHere.whatever ~/Documents/

# equivalent to above, but more verbose as we include the file name explicitly
cp ./fileNameGoesHere.whatever ~/Documents/fileNameGoesHere.whatever

# copy the contents of the file to a new file with a different name
cp ./fileNameGoesHere.whatever ~/Documents/copyButChangeFile.name

# use the -R flag to copy the entire contents of a folder to a new location
cp -R <path-to-folder> <new-folder-path>
```

---

`mv` : short for "Move", similar to copy except it removes the original file.

```bash
mv fileNameGoesHere.whatever ~/Documents/

# equivalent to above, but more verbose as we include the file name explicitly
mv ./fileNameGoesHere.whatever ~/Documents/fileNameGoesHere.whatever

# move the file to a new location under a different filename, and remove the original
mv ./fileNameGoesHere.whatever ~/Documents/copyButChangeFile.name

# use the wildcard `*` to copy everything within that folder recursively to the new location
mv /some/path/* /some/newpath

# use the -i flag to have it ask before overwriting anything
mv -i /some/path/* /some/newpath
```

---

`rm` : short for "Remove", deletes files and folders. BE VEWY CAWEFUW!!

```bash
# for our example just to be safe let's create an empty file to delete
touch things.stuff

rm things.stuff

# now let's create en empty directory and try deleting it
mkdir emptyDir

# when we try to delete a directory, we should get an error
rm emptyDir

# you just need to provide the flag -r to make it recursive
rm -r emptyDir

# but be very vareful, let's say you gave it the path ~/ it would delete your entire home directory
# with all your files, apps, and everything else. or worse yet if you tried to rm / with the -r flag
# it would delete your entire computer, and deletion is a very fast operation so even if you cancel
# by using Ctrl + C (generally how to quit a command line program)
# it'll still most likely have done too much damage to recover without reinstalling your entire OS

# even more dangerous is the -f flag combined with -r
rm -rf vewyVewyDangerous

# -f means force, so it doesn't stop and trigger a confirmation step for protected files
# it will just auto-agree to everything and keep deleting everything contained at the path you provided
```

---

`whoami` : lets you know which user you're logged in as.

```bash
whoami
```

---

`chown` : short for "Change Owner", changes the owner of a file

```bash
chown username:groupname file-path.etc

# or without the group is fine too, if you just want to change the owner
chown username file-path.etc

# to view the owner and group info use ls -l
ls -l file-path.etc
# -rw-r--r--  1 emma  staff  8342 Apr 20 06:09 file-path.etc

# assuming `file-path.etc` exists, you should get output similar to the line above
# in which, `emma` is the user and `staff` is the group
```

---

`chmod` : short for "Change Mode", changes the file permissions to whatever you specify

> More details about chmod, and a super handy permissions calculator: https://ss64.com/bash/chmod.html

```bash
# Allow everyone to read, write, and execute file
chmod 777 file-path

# Only allow the owner to read, write, and execute but don't let anyone else access the file at all
chmod 700 file-path

# Allow everyone to read the file
chmod a+r file-path

# add read and write for the user (owner) and the group, but not others
chmod ug+rw file-path

# deny execute permissions to everyone
chmod a-x file-path

# recursively set read and write permissions for everyone
# on the entire contents of this folder and the folder itself
chmod -R a+rw folder-path
```

---

`passwd` : set the password for the specified user, or the currently logged in user if none is provided.

```bash
# make sure we're signed in as the correct user
whoami

# calling passwd by itself will let you reset the password for the currently logged in user
passwd

# set the root password, or provide another username to set that user's password
passwd root
```

---

`su` : "Switch User", lets you attempt to log in as another user.

```bash
# login as root
su root

# you'll be asked for the password of the user you specify

# if I were root and wanted to go back to my main user, emmagamma, I'd do this
su emmagamma
```

---

`sudo` : stands for "Super User Do", however it does not actually switch users permanently like `su` does, but rather only for a single command. So it's prepended before another command to give you elevated privileges. It lets anyone who's in the wheel group act *as if* they're root by providing their user's password. By default your user should already be in the wheel group on most distros, so sudo should work already for your user.

```bash
# one common example (not on macOS) would be using apt-get to install packages
sudo apt-get install somePackage

# without sudo it won't have the permissions required to make changes to your file system.

# this is how you would start a new bash shell with root privileges
sudo bash

# sometimes sudo may be required to delete certain files
sudo rm passwordProtected.txt
```

---

> Next Up: [Lets dive into creating a website!](MAKEAWEBSITE.md)

---
