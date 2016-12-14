# Working with remotes

One great thing about git is easy to host your repositories on a **remote server**
(online). This makes it easy for you to access it from anywhere, as well as for
others to collaborate while keeping track of who made what changes.

[Github](https://github.com) and [Bitbucket](https://bitbucket.com) are two 
major sites that host git repositories. This tutorial will mostly talk about 
Github, but the process is more or less the same for any remote.

## Adding a remote

In order to host your repository on a remote server, you first need to set up a
repository on that server. On Github, you would click the "+" button in the 
upper right, and select "New repository." Name it whatever you want, select
"public" or "private" as you see fit, and ignore the options to initialize with
a README or license; those don't apply when you already have a repository that
you are going to push out.

Once it is created, it will bring you to a page that lists several URLs. Copy
the HTTPS one. For the sake of example, let's say it's `https://github.com/example/example-repo.git`.

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

So now your git repository knows of a remote server, located at `https://github.com/example/example-repo.git`,
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

* Initialize a repo on the remote (e.g., Github or Bitbucket)
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

* Just edit already-tracked files
* `git commit -am "My commit message."`
* `git push`



