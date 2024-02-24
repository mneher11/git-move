# git-move
git-move solves a problem that has been bugging me for a long time: switching between branches
without having to first stash all uncommited changes and then checkout the other branch.

## Installation
To install git-move, just download the script into a directory on your system that is included in
your `PATH` and make sure its executable bit is set. Git automatically detects all executables named
`git-<command>` and makes them available as a separate command, `git <command>`. This is inspired by
[this blogpost](https://mikebarkas.dev/git-alias-bash-functions-with-arguments/) by Mike Barkas.

## Usage
git move works similar to other git commands. For a detailed description of its various flags and
options, run:
```bash
git move -h
```
The usual use-case would be just to call git-move with the branch you want to move to, like so:
```bash
# On branch main
git move develop
```
git-move then automatically stashes your uncommited changes and checks out the destination branch.
When you want to move back to the previous branch, just call:
```bash
# On branch develop
git move main
```
which will automatically pop the stash associated with the `main` branch after checking it out.

If you want to move to a new branch, just add the `-b` flag to your command like so:
```bash
git move -b new_branch
```

## How it works
git-move keeps track of the current uncommited changes of each branch and applies them upon
revisiting the branch. It does so by maintaining a metadata file inside the `.git` directory called
`gitmove`.
