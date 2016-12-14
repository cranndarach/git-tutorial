# Glossary of git commands

### `git init`

Initializes a blank repository.  
Do this from a project's main folder or **root directory**.

### `git status`

Check out what changes have or have not been staged for committing.

### `git add [files]`

Stage files to commit.

### `git commit -m "My commit message."`

Commit your staged changes.

### `git commit -am "My commit message."`

Commit all tracked changes, regardless of whether they have been staged.

### `git remote add [name] [URL]`

Add a remote repository located at [URL], called [name].

### `git push -u origin master`

Push the branch "master" to the remote "origin", and set "origin/master" to 
track the local "master".

### `git push`

Push to the default location (probably `origin/branch-name`).

### `git pull`

Pull changes from the remote tracked branch to the current branch.

### `git clone [URL]`

Copy the repository located at [URL] here.

### `git branch`

List the branches on the current repository.

### `git branch branch-name`

Create a new branch called `branch-name`.

### `git checkout branch-name`

Switch to the branch `branch-name`.

### `git checkout -B branch-name`

Create a branch called `branch-name` and switch to it.

### `git merge [from] [to]`

Update branch `to` with the changes found on branch `from`.
