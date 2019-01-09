# 1. ~~Getting~~ Gitting Started

>Initialize a repository and make your first commit.

## Setup

This tutorial mostly covers git for command line, with some notes about GitKraken (a graphical tool for git) and GitHub.

If you want to follow along with the tutorial, you should first do the following:

* Install git. You can [find it here](https://git-scm.com/downloads).
  * On Windows, make sure to include the command-line tools and enable support for MinTTY.
* Sign up for an account on [GitHub.com](https://github.com) (optional, but recommended).
* Install [GitKraken](https://gitkraken.com) (optional, but recommended).
* Create a folder somewhere on your computer to use as your "project folder" for this tutorial.

## Opening the project folder

Git repositories are stored in a folder named `.git/` within your project's main folder or **root directory**. To start a repository, you will need to open
your project's root directory from a terminal.

### OSX & Linux

On Mac, you can find the application called "Terminal" in your Applications folder. On Linux, it varies, but you can probably find it by pressing `Ctrl-Alt-T`
or searching your applications menu for "Terminal."

When you have the terminal open, **change directories** into the project's root. To do this, type `cd path/to/project/directory`, replacing
`path/to/project/directory` with the actual path to the directory. Hint: Your terminal most likely opens to a directory called `~`, also known as the **home
directory**, which contains folders like `Documents` and `Desktop`. You can type `ls` to see what is in a folder at any time. You can also type the first few
characters (to the point where the name is unique, e.g., "Doc") and hit the tab key to complete it. You may also be able to drag-and-drop the name of the
folder from the file explorer (e.g., Finder or Nautilus).

### Windows

Open the project folder in your file explorer (Windows+E or "My Computer"). Right click, and select "Git Bash here."

## Initializing a repository

Now that you are in the project's root directory, you can initialize a git repository. To do this enter into the command line:

```sh
git init
```

Tada! You have now initialized a blank git repository.

## Stage some files

A git repository tracks and records changes to files. When you have a file in your directory that you want to keep track of, you will need to **add** it to the
**staging area** and **commit** it to the repository. 

First, let's make a file to stage. In a text editor, create a file in your project's root called `something-important.txt` (or whatever you want to call it).
Write something in it, like "This is some important information that I want to keep track of." Then save it. 

Now, in your terminal, enter:

```sh
git status
```

You should see `something-important.txt` under "Untracked files." In order for git to keep track of it, you'll need to **stage** it. Enter:

```sh
git add something-important.txt
```

Now check the status again:

```sh
git status
```

You should see your file under "Changes to be committed." That means that git has made a note of the current state of your file. If you make any more changes
to it that you want to commit, you'll need to `add` it again. You can stage as many files as you want prior to a commit. 

## Making your initial commit

A **commit** is sort of like an entry in a log. You have gathered up all of your relevant changes, staged them, and now you are ready to create a snapshot of
their current state before moving on. When you make a commit, you will write a brief **commit message** about what you changed. Then, at any point in the
future, you can come back to that commit, see what was different between before and after the commit, and see what you said about it.

So let's make the first commit now. To make a commit, you run the command `git commit` with the **option** `-m` followed by your commit message in quotes. By
convention, the message on your first commit to a repository is usually "Initial commit."

```sh
git commit -m "Initial commit."
```

Congratulations! You've just made your first commit to a repository. See [02_workflow.md](02_workflow.md) for the next steps.
