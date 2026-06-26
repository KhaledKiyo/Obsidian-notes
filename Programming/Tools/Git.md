#programing #devtools
## setup

download git

```bash
sudo pacman -S git
```

check git version

```bash
git --version
```

set default git branch to main

```bash
git config --global init.defaultBranch main
```

---

## create a new repository

```bash
git init
```

---

## check out a repository

```bash
# local
git clone /path/to/repository
# remote server
git clone username@host:/path/to/repository
```

---

## workflow

your local repository consists of three "trees" maintained by git. the first one is your `Working Directory` which holds the actual files. the second one is the `Index` which acts as a staging area and finally the `HEAD` which points to the last commit you've made.

```
Working Dir --(add)--> Index (Stage) --(commit)--> HEAD
```

---

## add & commit

to add a single file

```bash
git add <filename>
```

to add all files including dot-files

```bash
git add .
```

to add all files but ignore dot-files

```bash
git add *
```

to add only modified and deleted tracked files (ignores new untracked files)

```bash
git add -u
```

to commit

```bash
git commit -m "commit message"
```

---

## pushing changes

after committing, your changes are in `HEAD` but not yet on the remote. to push them:

```bash
git push origin <branch>
```

if you created a new local repo and haven't linked it to a remote yet, connect it first:

```bash
git remote add origin <server>
```

then push for the first time:

```bash
git push -u origin main
```

the `-u` flag sets `origin main` as the default upstream, so after this you can just type `git push` with no arguments.

---

## branching

branches are used to develop features isolated from each other. `main` is the default branch when you create a repository. use other branches for development and merge them back to `main` when done.

create a new branch and switch to it

```bash
git checkout -b <branch name>
```

switch to an existing branch

```bash
git checkout <branch name>
```

delete a branch

```bash
git branch -d <branch name>
```

push a branch so others can use it

```bash
git push origin <branch name>
```

---

## update & merge

pull the latest changes from remote into your current branch

```bash
git pull
```

merge another branch into your current branch

```bash
git merge <branch>
```

git tries to auto-merge, but if there are conflicts you have to resolve them manually in the files, then mark them as resolved:

```bash
git add <filename>
```

preview differences between two branches before merging

```bash
git diff <source_branch> <target_branch>
```

---

## tagging

create a tag for a release (e.g. version 1.0.0), using the first 10 characters of a commit id

```bash
git tag 1.0.0 <commit id>
```

get commit ids from the log (see below)

---

## log

view commit history

```bash
git log
```

filter by author

```bash
git log --author=<name>
```

one commit per line

```bash
git log --pretty=oneline
```

visual branch tree

```bash
git log --graph --oneline --decorate --all
```

see which files changed

```bash
git log --name-status
```

---

## replace local changes

discard changes in a file and restore it to the last commit

```bash
git checkout -- <filename>
```

> this only affects the working directory. staged changes and new files are kept.

drop everything and reset to the latest remote state

```bash
git fetch origin
git reset --hard origin/main
```

> ⚠️ this deletes all local changes and commits that aren't on remote. no undo.

---

## useful

colorful git output

```bash
git config color.ui true
```

interactive staging (lets you pick which parts of a file to stage)

```bash
git add -i
```
