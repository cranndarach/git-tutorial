# 4. Working with remotes

One great thing about git is easy to host your repositories on a **remote server** (online). This makes it easy for you to access it from anywhere, as well as
for others to collaborate while keeping track of who made what changes.

This tutorial will mostly talk about [GitHub](https://github.com), a major site that hosts git repositories, but the process is more or less the same for any
remote.

## Side note: Setting up SSH

Because working with a remote repository involves transferring data via the Internet, you should consider setting up SSH, which is safer and actually easier to
use than the default HTTPS. You can find instructions in [z1-setting-up-ssh.md](z1-setting-up-ssh.md).

## Adding a remote

In order to push your repository to a remote server, you first need to initialize a repository on that server. On GitHub, you would click the "+" button in the
upper right, and select "New repository." Name it whatever you want, select "public" or "private" as you see fit, and ignore the options to initialize with a
README or license; those don't apply when you already have a repository that you are going to push out.

Once it is created, it will bring you to a page that lists several URLs. Copy the SSH one if you have SSH set up, or the HTTPS one otherwise. For the sake of
example, let's say it's `https://github.com/example/example-repo.git`.

Now go over to your terminal and enter:

```sh
git remote add origin https://github.com/example/example-repo.git
```

To break that down: `git` is what tells it that you're doing a git command. `remote` says that you are going to be telling it to do something with a remote
server. `add` says that specifically, you are *adding* a remote. `origin` is the name of the new remote that you are adding. You get to pick the name—it could
really be anything, but "origin" is the convention. And then the URL tells it where to point when fetching or pushing changes to origin.

So now your git repository knows of a remote server, located at `https://github.com/example/example-repo.git`, and knows that that's what you're referring to
when you talk about "origin."

## Pushing to a remote

Now, you'll want to update the new remote repository so that it mirrors your local repository. This is called `push`ing.

The first time you push, enter:

```sh
git push -u origin master
```

`master` is the name of the **branch** that you are on. Branching will be covered in the next step, but in short, it allows you to copy the repo at a certain
point so that you can make changes in one branch but not another. By default, the main branch in a repository is called "master".

The `-u` option means "set upstream," meaning that it tells git to set up the current branch to track any changes on its remote counterpart, and vice versa.
This pairs your local branch `master` with the remote branch `origin/master` so that for future pushes, you can just run `git push` by itself without any extra
arguments. But nothing bad will happen if you still run `git push [-u] origin master` each time.

### Integrating this into your workflow

Keep in mind that `commit`ting and `push`ing are **two separate steps.** You cannot `push` changes that are not `commit`ted, and `commit`ting by itself does
not `push`.

## Workflow so far

Let's take a break to review the git flow so far. Note that the order is mostly only locally-dependent (you have to stage before or during the `commit`, not
after), but not so much globally-dependent (you can add a remote server whenever you want, as long as it is before you `push`).

### Initialize a repository

* `git init`

### Add a remote

* Initialize a repo on the remote (e.g., GitHub)
* Register it with your local repository: `git remote add origin git@github.com:example/example-repo.git`

### Make your first commits and pushes

* Create some files
* Stage them: `git add [relevant files]`
* Commit the changes: `git commit -m "Initial commit."`
* Update the remote: `git push -u origin master`

### Let the workflow flow!

* Create and/or edit some files
* `git add [relevant files]`
* `git commit -m "My commit message."`
* `git push`

or

* Edit already-tracked files
* `git commit -am "My commit message."`
* `git push`

## Pulling from a remote

When you are collaborating with others on one repository, or working across multiple computers, there will likely be times when the remote contains work that
is not in your local repository. Just like you `push` changes from your local repository to the remote, you can `pull` changes from the remote to your local
repository.

If your current branch is already tracking a remote branch (such as if you have already run a `git push -u origin master` once), then all you need to do is
run:

```git
git pull
```

If you have not set up your branch to track one on the remote, it's just a couple more terms:

```git
git pull origin master
```

But after that first run, you can do `git pull` from then on.

## Cloning a repository

Sometimes, you might be retrieving a repository that you do not have on your local machine. You *could* run through all the steps of making a blank repo on
your computer, adding the remote, and pulling from the remote. But you can also use `git clone` to do all that in one command.

So, to clone a repository, first find the URL of the remote repository. On GitHub, you can find that by clicking the green "Clone or download" button on a
repository's main page, and copying the HTTPS URL (or SSH if you have it set up).

Then go to your terminal and `cd` into a folder where you want the new repository to be—it will clone into its own subfolder.

Then run `git clone URL` (replacing "URL" with the actual URL).

Now `cd` into the project's folder. It will already have the remote set up as "origin", so no need to add it again. Now you can just pick up the workflow
like normal.

Up next: [05-branching-forking-merging.md](05-branching-forking-merging.md)
