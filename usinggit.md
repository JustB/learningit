# Setting up your repository

```
git config --global user.name “Bilbo Baggins”
git config --global user.email “bilbo@shirerocks.com”
```

This will create a new ~/.gitconfig file that will look like this:

```
$ cat ~/.gitconfig
[user]
    name = Bilbo Baggins
    email = bilbo@shirerocks.com
```

# Getting a Git repository

## New repository

```
git init
```

This will create a .git directory in your current working directory that is entirely empty.

If you have existing files you want to add to your new repository, type:

```
git add .
git commit -m ‘my first commit’
```

## Cloning a repository

```
git clone git://github.com/justb/test_repo.git
```

If you want to put it in a different directory than the name of the project, you can specify that on the command line,
too.

```
git clone git://github.com/justb/test_repo.git myotherfolder
```

# Workflow

We can add patterns into the `.gitignore` file to tell Git that we don’t want it to track them. Example:

```
tmp/*
log/*
config/database.yml
config/environments/production.rb
```

A good way to find out what you’re about to commit (that is, what is in your index) is to use the status command.

```
$ git status
# On branch master
# Changed but not updated:
# (use “git add <file>...” to update what will be committed)
#
# modified: README
# modified: Rakefile
# modified: lib/simplegit.rb
#

no changes added to commit (use “git add” and/or “git commit -a”)
```

You could commit only the Rakefile:

```
git add Rakefile
git commit -m "Add new task"
```
![git commit and git add](img/gitaddcommit.png)

If we want to commit all our changes, we can use this shorthand:

```
$ git commit -a -m ‘committing all changes’
```
![git commit -a](img/gitcommita.png)

## Removing

For removing files from your tree, you can simply run:

```
git rm <filename>
```

## Moving files

Renaming a file or moving a directory in Git is simple, using the `git mv` command:

```
$ git mv foo bar
```

## Unstaging Changes

If you want to start over with this process, it’s easy: just use `git reset`

```
$ git reset
Unstaged changes after reset:
M file1.php
M file2.java
```

# Undoing

## Changing the last commit

The most common correction to make is to the previous commit: you run `git commit`, and then realize you made a mistake:

```
$ git commit --amend
```

Git will present you with the previous commit message to edit if you like. You can also use this command to add other
files to the commit (before pushing it to the remote).

## Discarding the last commit

Suppose you make a commit, but then decide that you weren’t ready to do that. You want to _uncommit_. Just do:

```
$ git reset HEAD~
Unstaged changes after reset:
...
```
## Discarding any number of consecutive commits

```
$ git reset HEAD~3
Unstaged changes after reset:
...
```

## Undoing a commit

Suppose you want to undo the effect of an earlier commit, and make a new commit undoing the earlier commit’s changes.

```
$ git revert 9c6a1fad
```

This will compute the diff between that commit and the previous one, reverse it, and then attempt to apply that to
your working tree.

# Showing objects

The git show command is really useful for presenting any of the objects in a very human readable format.

```
git show branchname|SHA|tag|tree
```

# Diff

Git has a great diff utility built in that can give you statistics or a patch file given any combination of tree
objects, working directory and index.

```
justb:~/GitCourse  (master *)
⇒ git diff
diff --git a/usinggit.md b/usinggit.md
index f4d4eeb..28c451e 100644
--- a/usinggit.md
+++ b/usinggit.md
@@ -99,7 +99,13 @@ git rm <filename>
 The git show command is really useful for presenting any of the objects in a very human readable format.
+
+# Diff

+Git has a great diff utility built in that can give you statistics or a patch file given any combination of tree
+objects, working directory and index.
```

We can have a more compact view:

```
justb:~/GitCourse  (master *)
⇒ git diff --numstat
25      0       usinggit.md
```

# Branching

## Switching branches

Let’s say we’re working on our project and we want to add a new function to our library, so we’ll make a new branch
called `new-func` and switch to it. There are two ways we can do this

```
$ git branch newfunc; git checkout newfunc
```

```
$ git checkout -b newfunc
```

Now, to check which branch we are on, we just type `git branch`:

```
$ git branch
master
* newfunc
```

To check the differences between two branches:

```
$ git diff --stat master newfunc
```

## Merging

We can merge our branch:

```
$ git merge newfunc
```

And then get rid of it:

```
$ git branch -d newfunc
Deleted branch newfunc.
```

## Aborting a merge

If you start a merge and then want to cancel it — perhaps you weren’t expecting so many conflicts and you don’t have
time to deal with them now — just use:

```
git merge --abort .
```
