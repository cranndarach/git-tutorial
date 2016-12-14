# 4. Branching, forking, and merging

## Branching

A somewhat more advanced feature of git, but still very important, is branching.
Branching allows you to duplicate a repository at one point in history, and
make changes in one copy that are not reflected in another. This adds a layer of
security and makes it easier to mess around without worrying about breaking your
project.

First, you may want to see all of the branches that are currently in your repo.
To do this, run

```git
git branch
```

You will probably see something like

```
*master
```

That means that "master" is the only branch, and the "\*" means it is the one
you are currently on.

But what if you wanted to make a new branch? Let's call it "dev" for 
"development". One way you could do this is to run

```git
git branch dev
```

Now, check your list of branches again

```git
git branch
```

you'll see something like

```
dev
*master
```

Okay, so you made the branch dev, but you're still on master. That means any 
changes you make will still be made on master, not dev. To switch over to dev,
run 

```git
git checkout dev
```

now you should see something like

```
Switched to branch `dev`
```

Whereas most git commands make sense in come way, I honestly don't know why
`checkout` is so named. But anyway...

There is actually a slightly faster way. People used `git branch [new-branch] &&
git checkout [new-branch]` enough that it got shortened into one command:

```git
git checkout -B dev
```

meaning, "Switch over to the new branch 'dev'." (Replace "dev" with whatever 
you want the new branch to be called.)

Now, any changes that you make will be kept to the branch dev, and master will
be unchanged. 

When you want to switch back over to master, just use `git checkout master`.

You can have as many branches as you want, and they can branch off of whatever 
other branch you want them to.

Remember that when you are pushing out a new branch, just using `git push` won't
work. You'll need to use `git push -u origin [branch-name]`.

## Forking

Forking is kind of like if `git branch` and `git clone` had a baby. It's sort
of branching an entire project.

Normally, forking is something you do on a remote site, like Github (which will
again be used for the examples). If someone else has a project that you want to
either contribute to, or just have a copy of to make some changes for yourself, 
you would fork it using the "Fork" button at the upper right of a repository's
page (below the upper toolbar). This will make a copy of the repository on your
account.

Then, go to the fork on your account and clone it to your computer like normal 
(find the URL with the "Clone or download" button, then run `git clone URL`).

Now, one of the first things you'll want to do is make a new branch for your 
changes. This makes it easy to keep track of which changes are yours and which
changes are from the maintainer.

You'll want to give the branch a descriptive name. For example, let's say you
forked the repo to suggest a new color scheme for the user interface. Run

```git
git checkout -B color-scheme
```

The next thing to think about is the remote. By default, your fork on Github is 
"origin." This makes it easy to push your changes to your fork. But you will 
probably also want to pull changes in from the "original" one, commonly called
"upstream." So go grab the URL from the upstream repo, and run

```git
git remote add upstream URL
```

Now, when you want to pull from upstream, run

```git
git pull upstream/master color-scheme
```

(to be perfectly honest, I am not 100% sure about this one... I will update it 
if it turns out to be wrong.)

## Merging

Hopefully, changes you make to one branch will eventually be stable enough for 
you to incorporate them into the main project. To do this, you'll `merge` the
development branch with master.

First, make sure you don't have any conflicts, where files on both branches have
changed, and git doesn't know which one to keep.

Once you've made sure of that, just run `git merge [from] [to]`, only replace
`[from]` with the name of the branch containing the changes, and replace `[to]` 
with the name of the branch receiving the changes. So that would be something
like:

```git
git merge dev master
```

## Pull requests

When you've made changes to a fork that you would like the maintainer of the
upstream repository to consider incorporating into their project, you can submit
a **pull request** on that repository's page. If the maintainer likes your 
changes, they will merge them with (or, "pull them into") their repository. This
is primarily how open source development works.

## That's all!

Congratulations! That is just about all you need to know to use git. 

One last note: There is no need to memorize all of these commands. You might end
up memorizing them from using them a lot, but in the meantime, that's what things
like `git [command] --help` are for. You can also see glossary.md for a list of
the commands covered in this tutorial.
