Git Commands Reference
----------------------

Just a list of Git commands for reference.

git init
========

Create a new local repository.

```
git init   
```

git clone
=========

Copy an existing repository, [name] is optional, will name local repository this instead.

```
git clone [url] [name]
```

git status
==========

Tells you what branch you are on. Gives a general overview of untracked files, files that haven't been staged, and files that are staged and ready for commit. Files can show up in the Changes to be commited and the Changes not staged for commit if the file has been modified since the last time it was staged.

```
git status
```

git diff
========

This shows you changes to files that have not yet been staged. If all your changes have been staged this will show no output.

```
git diff
```

You can add --cached or in versions Git 1.6.1 and later you can add --staged. Adding this compares your staged changes to your last commit.

```
git diff --staged
```


git add 
=======

Stages the specified file.

```
git add [filename]
```

Stages new and modified, without deleted.

```
git add .  
```

Stages modified and deleted, without new.  

```
git add -u .
```

Stages All.

```
git add -A .     
```

git commit
==========


