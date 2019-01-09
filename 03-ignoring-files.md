# 3. Ignoring files

Sometimes you will have files that you do not want to track. They might be logs, output from programs, or contain sensitive information. It is a little
annoying to have these files show up when you run `git status`, and it can clutter up the visual space and make you miss important files that you *did* mean to
commit. Fortunately, there are two main ways to tell git not to track certain files: `.gitignore` and `.git/info/exclude`.

Any file name that you add to either of those files will be ignored in `git status` output and will not be committed.

## .gitignore

First, let's make a file to ignore. In a text editor, create a file called something like `ignore-me.txt`, and have it say something like "This is some
sensitive data that should not end up in a repository!" (If you're feeling fancy, run `echo "This is some sensitive data that should not end up in a
repository!" > ignore-me.txt` instead.)

Now run `git status`. Since we haven't told git to ignore that file yet, you should see it listed. Now let's change that.

In a text editor, create a file called `.gitignore` — the "." is important!

Write `ignore-me.txt` in it. You can add as many files as you want, as well as regular expressions (e.g., `*.log`), each on its own line. When you're done,
save and exit.

Now run `git status` again. You shouldn't see `ignore-me.txt` listed anymore, but you should see `.gitignore`. It is customary to commit `.gitignore` to your
repository so that in the future, you or others won't have to re-write it.

`.gitignore` works just like any other file in terms of git workflow. When you change it, you will want to stage and commit it.
