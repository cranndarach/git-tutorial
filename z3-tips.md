# Z3. Tips

## More Git tools

* [hub](https://hub.github.com/): Adds some commands specifically for working with repositories on GitHub (e.g., `git create` and `git fork`), and makes some existing commands easier (e.g., `git clone user/repository`)
* [tig](https://github.com/jonas/tig): text-mode interface for git (and git spelled backwards).
* Most editors have a git interface (e.g., git-plus for Atom, and vim-fugitive for vim).

## Aliases

Some git commands are long and annoying to type. Luckily, programmers hate typing more than 3 characters per task, give or take, so aliases exist. Aliases are user-defined abbreviations for commands.

To define an alias, add the line `alias abc="original command"` (where "abc" is the new alias, and "original command" is the full original command) to your shell configuration file (probably `~/.bashrc` or `~/.bash_profile`). Then be sure to reload the file (e.g., `source ~/.bashrc`) to apply the aliases.

Here are the git aliases I use, in case they might make your life easier too.

```sh
alias gs="git status"
alias gadd="git add"
alias gc="git commit -m"
alias gca="git commit -am"
alias gpl="git pull"
alias gp="git push"
alias gpu="git push -u"
alias gpi="git push -u"
alias gsub="git submodule add"
alias gco="git checkout"
alias gcob="git checkout -B"
alias gbr="git branch"
```

The `commit` aliases expect the message afterward, like `gc "My commit message."`
