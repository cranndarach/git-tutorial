# 3. Working with remotes

One great thing about git is easy to host your repositories on a **remote server**
(online). This makes it easy for you to access it from anywhere, as well as for
others to collaborate while keeping track of who made what changes.

[GitHub](https://github.com) and [Bitbucket](https://bitbucket.com) are two 
major sites that host git repositories. This tutorial will mostly talk about 
GitHub, but the process is more or less the same for any remote.

## Setting up SSH

This is an optional step, but it has two significant benefits. 

1. It is more secure than the default of using a password (SSH stands for
"secure shell"!).
2. It is actually way easier to use than the default once you have it set up,
because you don't have to enter a password each time you interact with the remote.

(Note: You can find more complete info on SSH with GitHub
[here](https://help.github.com/articles/connecting-to-github-with-ssh/). That
is where most of this info is coming from.)

### Generate an SSH key

An **SSH Key** is a large random number used for encrypting an decrypting
messages. It also sort of serves as your identity on the Internet, in that
services will use it to verify whether a message actually came from you. It
sounds kind of complicated, but don't worry—your computer handles most of it.
You just need to set it up.

First, make sure you don't already have a key. In your terminal, enter:

```sh
ls -al ~/.ssh
```

If it comes up empty, then you're good to create a new key. If there is something
there, e.g., `id_rsa` and `id_rsa.pub`, then you can skip to the next step.

If you're creating a key, enter the following into your terminal: (replace the
email address with your actual email address)

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

That means, "Hey program called ssh-keygen, make a key using the standard (RSA)
encryption type, make it 4096 bytes, and use my email address as a way to make
it personal."

It will prompt you for a bit more information. You can probably just hit enter
through the questions, because the defaults are typically fine, unless you have
a particular preference to do otherwise.

Importantly, this generated two files. One is called `id_rsa`, and the other is
called `id_rsa.pub`. The .pub file is called a **public key.** It is what you
give to whoever/whatever is going to be decrypting your messages. The one without
an extension is called a **private key.** You *do not* want to give that key to any web
site. It is the one you use to encrypt your messages, and then they can only be
decrypted with your corresponding public key. You can think of a public key as
being like your driver's license, in that you give it to someone to show that
you are who you say you are. And then I guess the private key in this analogy
would be something like a clone of yourself. So if you give someone else a clone
of you, that clone can go around telling people it's you pretty convincingly.

Weird dystopic scifi analogies aside, once the key is generated, enter the
following lines:

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### Adding the key to GitHub

Now you need to tell GitHub what your public key is so that it can verify your
identity when you send it commits.

First you need to copy your public key. In your terminal, try:

```sh
xclip -sel clip < ~/.ssh/id_rsa.pub
```

If that returns an error that xclip is not installed, you can just use `cat`:

```sh
cat id_rsa.pub
```

to print it to the screen, and then copy it normally (highlight and right-click
\> copy or Ctrl/Cmd+Shift+C)

Then go to GitHub, and on the top right, click on the arrow next to your icon,
and then click "Settings."

On the left bar, click "SSH and GPG keys."

On the top-ish right (green button), click "New SSH key."

Add a title that will help you identify which computer it's from.

And then paste the key in the box, and hit "Add SSH key."

You should be good!

## Adding a remote

In order to host your repository on a remote server, you first need to set up a
repository on that server. On GitHub, you would click the "+" button in the 
upper right, and select "New repository." Name it whatever you want, select
"public" or "private" as you see fit, and ignore the options to initialize with
a README or license; those don't apply when you already have a repository that
you are going to push out.

Once it is created, it will bring you to a page that lists several URLs. Copy
the SSH one. For the sake of example, let's say it's `git@github.com:example/example-repo.git`.
(They'll all follow the same pattern of `git@github.com:USERNAME/REPOSITORY.git`.)

Now go over to your terminal and enter:

```sh
git remote add origin https://github.com/example/example-repo.git
```

Let's break that down. `git` is what tells it that you're doing a git command.
`remote` says that you are going to be telling it to do something with a remote
server. `add` says that specifically, you are *adding* a remote. `origin` is
the name of the new remote that you are adding. You get to pick the name—it 
could really be anything. "origin" is just the convention. And then the URL 
tells it where to point when fetching or pushing changes on origin.

So now your git repository knows of a remote server, located at `git@github.com:example/example-repo.git`,
and knows that that's what you're referring to when you talk about "origin."

## Pushing to a remote

Now, you'll want to get your repository onto the remote. This is called `push`ing.

The first time you push, you will want to use 

```sh
git push -u origin master
```

`master` is the name of the **branch** that you are on. Branching will be 
covered later, but in short, it allows you to copy the repo at a certain point 
so that you can make changes in one branch but not another. By default, the main
branch in a repository is called *master*.

The `-u` option tells it to set up the current branch to track any changes on
its remote counterpart, and vice versa. It essentially pairs your local branch
`master` with the remote branch `origin/master`. That way, for future pushes, 
you can just run `git push` by itself without any extra arguments. But nothing 
bad will happen if you still run `git push [-u] origin master` each time.

### Integrating this into your workflow

Keep in mind that `commit`ting and `push`ing are two separate steps. You cannot
`push` changes that are not `commit`ted, and simply `commit`ting does not `push`.
In that way, you can also save up a bunch of commits and push them in one batch,
but typically you would probably just push after each commit.

## Review so far

Let's take a break to review the steps so far. Note that the order is mostly 
only locally-dependent (you have to stage before or during the `commit`, not 
after), but not so much globally-dependent (you can add a remote server whenever 
you want, as long as it is before you `push`). 

### Initialize a repository

* `git init`

### Add a remote

* Initialize a repo on the remote (e.g., GitHub or Bitbucket)
* `git remote add origin https://github.com/example/example-repo.git`

### Make your first commits and pushes

* Create some files
* `git add [relevant files]`
* `git commit -m "Initial commit."`
* `git push -u origin master`

### Let the workflow flow! (or, `while project != complete`)

* Create and/or edit some files
* `git add [relevant files]`
* `git commit -m "My commit message."`
* `git push`

or

* Edit already-tracked files
* `git commit -am "My commit message."`
* `git push`


## Pulling from a remote

When you are collaborating with others on one repository, or working across 
multiple computers, there will likely be times when the remote contains work 
that is not in your local repository. If your current branch is already tracking
a remote branch (such as if you have already run a `git push -u origin master` 
once), then all you need to do to retrieve these changes is run:

```git
git pull
```

If you have not set up your branch to track one on the remote, it's just a couple
more terms:

```git
git pull origin master
```

But after that first run, you can do `git pull` from then on.

## Cloning a repository

Sometimes, you might be retrieving a repository that you do not have on your
local machine. You could run through all the steps of making a blank repo on 
your computer, adding the remote, and pulling from the remote. But this is all
accomplished in one command: `git clone [URL]`.

So, to clone a repository, first go to your terminal and `cd` into a folder 
where you want the new repository to be—it will clone into its own subfolder, so 
if you have folder called "Projects" or something, that would be suitable. 

Then find the URL of the remote repository. On GitHub, you can find that by 
clicking the green "Clone or download" button on a repository's main page, and
copying the HTTPS URL. 

Then, in your terminal, run `git clone https://github.com/example/example-repo.git`

Now `cd` into the project's folder. (While it is cloning, it will say something
like "cloning into example-repo/", so then you can do `cd example-repo`.) This
will already have the remote set up as "origin", so no need to add it again. Now
you can just pick up the workflow like normal.

### That's all for remotes

Next, try 04_branching-forking-merging.md
