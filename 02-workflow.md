# 2. Workflow

Now that you've made your first commit, you'll want to get into the habit of staging and committing changes as you go.

## Staging more changes

Whether the file is brand new, or already being tracked but just modified, you can add it to the staging area with `git add [file]` (without the
brackets). You can also list as many files as you want here, separated by spaces, and you can use glob patterns. So something like this would be valid:

```sh
git add file1.txt file2.txt data/*.csv
```

Remember that you can always see what is staged by running `git status`.

Anything that you do not add to the stage will not be included in the commit. So, if you have files that you don't want tracked (see "Ignoring files," up
next), or if you've made changes that you think don't really fit with the theme of your current commit, you can just not stage them.

On the flip side, if you forget to stage a file, it won't be included in your commit, so double check the `status` before you make a commit just to be safe.

## More commits

You should make a commit every time you are *about to* change something big, and again afterward. That way, if you make a mistake, you can just roll back in
time and pretend it never happened.

## Skipping the staging (or, staging at the commit)

Sometimes, even most of the time, you might not need to do too much with staging. You might be only working on existing files rather than adding new ones, and
committing all changes to tracked files at every commit. In these situations, it is possible to skip the `git add` parts. Instead, run your `commit` with the
option `-a` for "all."

You can combine single-letter options, as long as any with a parameter are last. That means, this:

```sh
git commit -a -m "My commit message."
```

is the same as

```sh
git commit -am "My commit message."
```

## Commit messages

Commit messages are short (72 characters max), imperative ("Update an important thing." instead of "Update**d** an important thing."), and end with a period.
It is important to be as descriptive as possible in your commit message, especially when collaborating or working on an open source project (even if it's your
own open source project).

If you cannot fit all of the necessary information in your commit message, you can use the extended version. To write an extended commit message, make your
commit without the `-m "Message"` option. That is, just run `git commit` or `git commit -a`. This will open a text editor for you to enter your message.

On the first line, write your brief summary, but end it with "..." For example, "Add cool_function() to my_script.py..."

Then skip a line.

Then, begin your extended message. Here, you can be as detailed as you need to be about the changes that you made. You don't have to use the imperative. Try to
cover the rationale for the changes, as well as the outcome (Was it successful? Is it a work in progress?).

When you're done, save it and exit. This will take you back to the command line and finish the commit.

**Note:** In GitKraken, you can write an extended message in the bigger box under the main commit message box.


Coming up: [Ignoring Files](03-ignoring-files.md).
