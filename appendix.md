# Appendix

## More ways to ignore files

In addition to the project's `.gitignore` file, there are two other ways to
ignore files. You can specify patterns to ignore in the project's `excludes`
file, or you can make a **global** `.gitignore`.

## `excludes` file

The excludes file is actually within the git repository's configuration files.
You can find it at `.git/info/excludes`. Since changes you make to this file are
made directly to the repository itself not in the project's root directory, you
do not need to commit it, but it stays with your local repository and is not
pushed to a remote.

You might use the `excludes` file to ignore files that are in your project's
folder but are just plain irrelevant to the repository, and save `.gitignore`
for "junk" files that are generated in the process of developing your project
(e.g., `__pycache__` or `*.[oa]`).

A good rule of thumb is that if you think it could apply to someone else too,
put it in the `.gitignore`. Otherwise, put it in the `excludes`.

## Global `.gitignore`

If there are patterns that you find yourself adding to a `.gitignore`/`excludes`
all the time, you might want to make a global `.gitignore` file. You can specify
the path to this file in your `~/.gitconfig`, and then git will ignore the patterns
for every project.

A reasonable place to put the file would be `~/.gitignore-global` or
`~/.gitexclude-global`. The file name doesn't actually matter, since you'll be
telling git where to look for it anyway.

You can tell git what file to use by running:

```sh
git config --global core.excludesfile="~/.gitignore-global"
```

replacing `~/.gitignore-global` with the actual file path.

Then any patterns you add to that file will be ignored by all git repositories
on your computer.
