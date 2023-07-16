##### Before continuing, make sure you've gone through the steps in the previous guide:

---

> [Setup your Environment](README.md)

---

# Info and Background, working with Bash

In the previous guide, we set up WSL for windows, meaning we can just use bash for all systems going forward rather than doing things in powershell separately.

## bash configuration

When you open a new terminal window, it should log in as your user and run your `~/.bash_profile` file which can contain bash code to configure your sessions. In addition each time you open a new tab it starts a new session logged in as your user, and will run your `~/.bashrc` which is very similar to your bash profile in that it can contain arbitrary bash code and further configures the same environment.

If you're using Zsh and Oh My Zsh, then your `~/.zshrc` file will also re-run each time you start a new session.

After making changes to these files, we can run any of the following commands to have that specific config file refresh in the current session instead of requiring us to open a new tab:

```bash
source ~/.bash_profile
source ~/.bashrc
source ~/.zshrc
```

---

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

---

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

---

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

---

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
cd Code

mkdir BabysFirstProject
```



