# 5. Branching, forking, and merging

## Branching

Branching is a somewhat more advanced feature of git, but it is extremely useful. Branching allows you to duplicate a repository at one point in history, and
make changes in one copy that are not reflected in another. This adds a layer of security and makes it easier to try things without worrying about breaking
your project.

To list the branches that currently exist in your repository, run:

```git
git branch
```

Right now, you will probably see something like

```
*master
```

That means that "master" is the only branch, and the "\*" means it is the one you are currently on.

But what if you wanted to make a new branch? Let's call it "dev" for "development". One way you could do this is to run

```git
git branch dev
```

Now, if you run `git branch` again, you'll see something like

```
dev
*master
```

Okay, so you made the branch dev, but you're still on master. That means any changes you make will still be made on master, not dev. To switch over to dev, run

```git
git checkout dev
```

There is actually a slightly faster way. People used `git branch [new-branch] && git checkout [new-branch]` enough that it got shortened into one command:

```git
git checkout -B dev
```

meaning, "Switch to a new branch called 'dev'."

If you run `git branch` now, it should output:

```
*dev
master
```

Now, any changes that you make will be kept to the branch dev, and master will be unchanged.

When you want to switch back over to master, just use `git checkout master`.

You can have as many branches as you want, and they can branch off of whatever other branch you want them to.

Remember that when you are pushing out a new branch, just using `git push` won't work. You'll need to use `git push -u origin branch-name`.

## Merging

When you want to incorporate changes from one branch into another, you can do a `merge`.

First, make sure you don't have any conflicts. A conflict happens when files on both branches have changed in the same place, and git doesn't know which one
you want to keep. (If you do end up with a merge conflict, I would recommend using a GUI tool like GitKraken to help you resolve it.)

To merge, fist checkout to the receiving branch (e.g., `git checkout master`). Then run `git merge source`, replacing `source` with the name of the branch
containing the changes. This will merge changes from `source` into your current branch.

## Forking

Forking is sort of like branching an entire project.

Normally, forking is something you do on a remote site, like GitHub (which will again be used for the examples). If someone else has a project that you want to
either contribute to, or just have a copy of to make some changes for yourself, you would fork it using the "Fork" button at the upper right of a repository's
page (below the upper toolbar). This will make a copy of the repository on your account.

Then you can go to the fork on your account and clone it to your computer like you normally would (find the URL with the "Clone or download" button, then run
`git clone URL`).

By default, your fork on GitHub will be set as "origin." If you want to pull in changes from the original repository, you can add it as another remote. The
convention is to call it "upstream."


```git
git remote add upstream URL
```

When you want to pull from upstream, run

```git
git pull upstream/master
```

## Pull requests

If you've made changes to a fork that you would like the maintainer of the upstream repository to consider incorporating into their project, you can submit a
**pull request** on that repository's page. If the maintainer likes your changes, they will merge them with (or, "pull them into") their repository. This is
primarily how open source development works.

## That's all!

Congratulations! That is just about all you need to know to use git.

One last note: There is no need to memorize all of these commands. You might end up memorizing them from using them a lot, but in the meantime, that's what
things like `git [command] --help` are for. You can also see glossary.md for a list of the commands covered in this tutorial.
