# 2. Workflow

Now that you've made your first commit, you'll want to get into the habit of 
staging and committing changes as you go.

## Staging more changes

Whether the file is brand new, or already being tracked but just modified, you
can add it to the staging area with `git add [filename].[ext]` (without the 
brackets). You can also list as many files as you want here, separated by 
spaces, and you can use regular expressions. So something like this would be
valid:

```sh
git add file1.txt file2.txt data/*.csv
```

Remember that you can always see what is staged by running `git status`.

You don't have to add everything to the staging area if you don't want to 
commit its changes. So, if you have files that you don't want tracked (see 
"Ignoring files" below), or if you've made changes that you think don't really 
fit with the theme of your current commit, you can just not stage them, and 
then they won't be included in your commit.

On the flip side, if you forget to stage a file, it won't be included in your 
commit, so double check the `status` before you make a commit just to be safe.

## More commits

You should make a commit every time you are *about to* change something big,
and again afterward. That way, if you mess something up, you can just roll back
in time and pretend it never happened. 

## Skipping the staging (or, staging at the commit)

Sometimes, even most of the time, you might not need to do too much with staging. 
You might be only working on existing files rather than adding new ones, and 
committing all changes to tracked files at every commit. In these situations, 
it is possible to skip the `git add` parts. Instead, run your `commit` with the
option `-a` for "all." You can combine single-letter options, as long as any with a 
parameter are last. That means, this:

```sh
git commit -a -m "My commit message."
```

is the same as 

```sh
git commit -am "My commit message."
```

## Commit messages

Commit messages are generally short (~120 characters max), imperative ("Update
README.md." instead of "Update**d** README.md."), and end with a period. It is 
important to be as descriptive as possible in your commit message. This is 
especially important when collaborating or working on an open source project.
If you cannot fit all of the necessary information in your commit message, 
you can use the extended version.

To write an extended commit message, make your commit without the `-m "Message"`
option. That is, just run `git commit` or `git commit -a`. This will open a 
text editor for you to enter your message.

On the first line, write your brief summary, but end it with "..." For example,
"Make important changes to my_script.py..."

Then skip a line.

Then, begin your extended message. Here, you can be as detailed as you need to
be about the changes that you made. You don't have to use the imperative. Try 
to cover the rationale for the changes, as well as the outcome (Was it 
successful? Is it a work in progress?). 

When you're done, save it and exit. This will take you back to the command line
and finish the commit. 

## Ignoring files

Sometimes you will have files that you do not want to track. They might be logs,
output from programs, or contain sensitive information. It is a little annoying
to have these files show up when you run `git status`, and it can clutter up
the visual space and make you miss important files that you *did* mean to 
commit. Fortunately, `.gitignore` exists.

First, let's make a file to ignore. In a text editor, create a file called 
something like `ignore-me.txt`, and have it say something like "This is some 
sensitive data that should not end up in a repository!" (If you're feeling 
fancy, run `echo "This is some sensitive data that should not end up in a 
repository!" > ignore-me.txt` instead.)

Now run `git status`. You'll see that file listed. Let's change that.

In a text editor, create a file called `.gitignore` — the "." is important!

Write `ignore-me.txt` in it. You can add as many files as you want, as well as
regular expressions (e.g., `*.log`), separated by new lines. When you're done, 
save and exit.

Now run `git status` again. You shouldn't see `ignore-me.txt` listed anymore, 
but you should see `.gitignore`. It is customary to commit `.gitignore` to your
repository so that in the future, you or others won't have to re-write it. 

`.gitignore` works just like any other file in terms of git workflow. When you
change it, you will want to stage and commit it.
