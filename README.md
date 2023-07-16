# Intro

This guide assumes you know pretty much nothing about programming and seeks to take you through everything you'll need to get started with javaScript, HTML, and CSS as well as a number of other tangential tools and technologies that are widely used by professional software engineers. If you follow along, by the end you should have everything you need to start your first project and kick it's freakin ass.

# Getting your environment set up

### on Windows:

First you'll basically want to set up a linux environment, since that's now built into the windows operating system.
It's called Windows Subsystem for Linux, and to install it, simply open powershell and run:

```powershell
wsl --install
```

By default this will allow you act as if you're running Ubuntu, so you can follow any command line tutorial for something in Ubuntu and it should work fine. For more information about WSL check out [microsoft's WSL docs](https://learn.microsoft.com/en-us/windows/wsl/install).

### on macOS:

Already good to go, we should have a bash shell by default.

However, there are things such as [iTerm 2](https://iterm2.com), [Zsh + Oh My Zsh](https://sourabhbajaj.com/mac-setup/iTerm/zsh.html), and of course [homebrew](https://brew.sh) if you don't already have that installed, which can make the terminal experience a lot nicer as well as improving your package management experience.

```bash
# you need the xcode command line tools before installing homebrew, may take a while
sudo xcode-select --install

# install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

# add homebrew to your $PATH
# and set it in your bash profile so that it runs every time you start a new command line session
echo 'PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

# optionally, verify that brew is installed and working correctly
brew doctor

# install iTerm 2
brew install --cask iterm2

# install zsh
brew install zsh

# install oh my zsh (this part should be the same on linux and mac, but brew is not available on linux)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# the installation script above *should set zsh to your default shell rather than bash
# however you can do so manually like this
chsh -s $(which zsh)
```

### on Linux:

You can find alternatives for iTerm on linux, but Zsh and Oh My Zsh should both still work on most distros.

For Ubuntu or any other OS with `apt` available, it would just be:

```bash
# first let's just make sure apt and apt-get are up-to-date
sudo apt update && sudo apt-get update

# install zsh
sudo apt install zsh

# check if curl is already installed or not
curl --version

# if you see output similar to
# `zsh: command not found: curl`
# rather than a version and other info, then we need to install it

# install curl
sudo apt install curl

# install oh my zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# the installation script above *should set zsh to your default shell rather than bash
# however you can do so manually like this
chsh -s $(which zsh)
```

More details about installing [Zsh](https://www.tecmint.com/install-zsh-in-ubuntu/).

More details about installing [Oh My Zsh](https://www.tecmint.com/install-oh-my-zsh-in-ubuntu/).


# Getting Git

Git is an absolutely crucial tool for any software engineer. there are alternatives but for the most part git is the defacto way to manage your code base and track changes over time non-destructively. Meaning when you delete a file or delete lines from a file, you can always just revert to a previous `commit` (a revision, or like, the latest edition) to get all the data back.

### install git on macOS: 

```bash
brew install git
```

### install git on ubuntu/windows:

```bash
sudo apt-get install git-all
```

For more info about installing git you can also refer to [this guide](https://github.com/git-guides/install-git).

#### Then we should be able to verify (for any OS) that git was installed correctly, with

```bash
git version
```

### Configuring git further:

As mentioned in these docs/articles:

- [Customizing Git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration): in depth but a bit dense.
- [Git Config](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config): not as in depth but covers the important parts well and provides clear simple examples.

We will want to update the git config user, with name and email, however we'll want this to match our github profile.
So let's first [create a github account](https://github.com/signup).

Git is the actual version control system, so it's a command line tool that lets you track your changes as you go.

Github is a website built around git, that provides a copy of your code that lives in the cloud, so even if all your code was deleted from your machine you can easily pull the latest version back down. It also let's you easily collaborate with others, set up teams, private repos, and rules around how contributions from others are handled, and control other settings. Like whether those changes require certain individuals to approve before being accepted, or what.

<a href="https://preview.redd.it/iyiauvgxxhf51.jpg?auto=webp&s=3c19af625ca24b1897aa6ad0edcc1310e62da83b" target="_blank">
  <img alt="Git is to Github as Porn is to Pornhub" title="Git is to Github as Porn is to Pornhub" src="https://preview.redd.it/iyiauvgxxhf51.jpg?auto=webp&s=3c19af625ca24b1897aa6ad0edcc1310e62da83b" width="400" />
</a>

There **are** alternatives to github such as bitbucket or gitlab but they've both had catastrophic failures in the past where they lost tons of user's code. So in general everybody uses Github. However, even just using git by itself it already has the ability to host your code in the cloud. You would just create a server using something like AWS, Digital Ocean, Linode, or whatever else... and then set that server up as a git remote. But don't worry about that just yet, just somemthing that's good to be aware of for now, that you don't *need* a github alternative and can just use git by itself if you like.

Okay, so anyway now that you have your github account set up, you'll wanna use the same email you used to sign up for github with and run this command, AFTER replacing `your@email.com` with your **actual** email address:

```bash
git config --global user.email "your@email.com"
```

Then you'll want user.name to match whatever you're using on github as your display name:

```bash
git config --global user.name "Your Display Name"
```

Doing these two things above will help github properly attribute your changes to you, and if you don't set it up to match github then you may notice some activity missing from your github profile, aka fewer little green squares.

# Setting Up your Github SSH keys

Don't worry if you're unsure what an SSH key is, we'll cover it in more depth later, but for now just know that properly configured SSH keys are more secure than passwords, and this will be how we authenticate with github so that we can push changes up to our repositories hosted there.

Luckily github provides some really thorough guides, so just follow each of these steps, in order:

1. [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
2. [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
3. [Testing your SSH connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)

Now all the git/github setup and configuration should be done, and you're ready to start creating new repos and submitting changes!

# Creating your first git repository

You can either create a repo just locally on your machine, by going to a new directory and using the command:

```bash
# this assumes you're already inside the folder you want to use
git init

# you can also pass the name of the folder you want it to create and initialize
git init MyNewProject
```

Or you can <a href="https://docs.github.com/en/get-started/quickstart/create-a-repo" target="_blank">create a repo on github</a> first and then pull it down to start making changes.

Cheat Sheet with a buncha handy commands: <a href="https://training.github.com/downloads/github-git-cheat-sheet/" target="_blank">github git cheat sheet</a>
