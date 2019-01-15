# Z3. Tips

## More Git tools

* [hub](https://hub.github.com/): Adds some commands specifically for working with repositories on GitHub (e.g., `git create` and `git fork`), and makes some existing commands easier (e.g., `git clone user/repository`)
* [tig](https://github.com/jonas/tig): text-mode interface for git (and git spelled backwards).
* Most editors have a git interface (e.g., git-plus for Atom, and vim-fugitive for vim).

## Aliases

Some git commands are long and annoying to type. Luckily, programmers hate typing more than 3 characters per task, give or take, so aliases exist. Aliases are user-defined abbreviations for commands.

To define an alias, add the line `alias abc="original command"` (where "abc" is the new alias, and "original command" is the full original command) to your shell configuration file (probably `~/.bashrc` or `~/.bash_profile`).
