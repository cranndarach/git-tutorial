# Branching, forking, and merging

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
page (below the upper toolbar). 
