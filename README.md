# Git Commands Reference

[Git Documentation](http://git-scm.com/docs "Git Documentation")

My own notes while taking the journey of learning Git. Makes reading through all of this a little more fun. =)

## git help [Documentation](http://git-scm.com/docs/git-help "Git Help Documentation")


Git command to help with commands and such in the command line.

```
git help [something]
git [something] --help
```

## git config [Documentation](http://git-scm.com/docs/git-config "Git Config Documentation")

There are three levels of git config files: (/etc/gitconfig) `--system` refers to all users on the system and all their repositories, (~/.gitconfig) `--global` is specific to one user, (.git/config) `git config` by itself refers to the config file in the current repository. Anything in both the `--system` and `--global` configs will use the `--global` configs settings. Anything in the .git/config will override the setting in the other two configs. Like in CSS when an inline style overrides a style in a linked .css file.

```
git config --system
git config --global
git config
```

Commits will use the `user.name` and `user.email` information in these configs. You can also set the text editor Git opens to for things like your commit messages with `core.editor`. `merge.tool` allows you to set the diff tool to resolve merge conflicts. `web.broswer` for default broswer. `--list` will list out all settings so far.
```
git config --global user.name "Some Name"
git config --global user.email "somename@whatever.com"
git config --global core.editor [editor or the path for the editor]
git config --global web.browser firefox
git config --list
```

## git init [Documentation](http://git-scm.com/docs/git-init "Git Init Documentation")

Create a new local repository.

```
git init   
```

## git clone [Documentation](http://git-scm.com/docs/git-clone "Git Clone Documentation")

Copy an existing repository, [name] is optional, will name local repository this instead.

```
git clone [url] [name]
```

## git status [Documentation](http://git-scm.com/docs/git-status "Git Status Documentation")

Tells you what branch you are on. Gives a general overview of untracked files, files that haven't been staged, and files that are staged and ready for commit. Files can show up in the Changes to be commited and the Changes not staged for commit if the file has been modified since the last time it was staged.

```
git status
```

## git diff [Documentation](http://git-scm.com/docs/git-diff "Git Diff Documentation")

This shows you changes to files that have not yet been staged. If all your changes have been staged this will show no output.

```
git diff
```

You can add `--cached` or in versions Git 1.6.1 and later you can add `--staged`. Adding this compares your staged changes to your last commit.

```
git diff --staged
```


## git add [Documentation](http://git-scm.com/docs/git-add "Git Add Documentation")

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

## git rm [Documentation](http://git-scm.com/docs/git-rm "Git rm Documentation")

This stops tracking a file and removes the file from the working directory so it doesn't show as an untracked file. If you remove the file from the working directory then run git rm on it, the file will be staged to be deleted.

```
git rm [filename]
```

Add `-f` to force a removal of a file. If a file was modified, then added but not commited it would have to be force removed. This is to avoid accidently losing data.

```
git rm -f [filename]
```

Add `--cached` to remove a file from staging and to stop tracking the file but leaves it in the working directory on the hard drive.

```
git rm --cached [filename]
```

You can pass files, directories, and file glob patterns to `git rm`. The example below would remove all files that are .md extension from the notes/ directory. For Windows, omit the backslash (\\).

```
git rm notes/\*.md
```

## git mv [Documentation](http://git-scm.com/docs/git-mv "Git mv Documentation")

This is the shorthand for renaming a file using Git. Run this and Git will stage the rename for you.

```
git mv [old_file_name] [new_file_name]
```

This is what Git does for you when you run git mv. It renames the file, `git rm [old_file_name]`, then `git add [new_file_name]`. Saves you from writing three lines to just one.

```
mv 	[old_file_name] [new_file_name]
git rm [old_file_name]
git add [new_file_name]
```

## git commit [Documentation](http://git-scm.com/docs/git-commit "Git Commit Documentation")

Records the staged changes to the local repository. This will launch the text editor that was configured in the `git config core.editor` command with comments of the latest git status command in it. Add your message under the comments or just delete them and it will be saved and commited after the editor is closed.

```
git commit
```
Adding `-v` will put the diff of your changes in the editor as well.

```
git commit -v
```

Adding `-m ""` will allow you to do an inline message and skip opening up the editor. Will instantly commit when this command runs.

```
git commit -m "Whatever you want the commit message to be goes here."
```

You can skip staging by adding `-a` to the commit. This will stage every file that is being tracked into the commit for you. By using `-a` and `-m` you can do quicker commits.

```
git commit -a -m "This is my commit message."
```

After the commit was successful it will show the branch commited to, the SHA-1 id, how many files were changed, and stats on the lines added and removed.

## git push [Documentation](http://git-scm.com/docs/git-push "Git Push Documentation")

## git log [Documentation](http://git-scm.com/docs/git-log "Git Log Documentation")

This pulls up the existing commit history for the current repository from newest to oldest.

```
git log
```
