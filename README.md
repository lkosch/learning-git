# Git Commands Reference

[Git Documentation](http://git-scm.com/docs "Git Documentation")
[Git Immersion](http://gitimmersion.com/index.html "Git Tutorial") is a great easy Git tutorial to get started with Git.
[My Git Aliases](https://github.com/lkosch/learning-git/master/README.md#my-git-aliases-documentation "My Git Aliases") to keep track of my own aliases.

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

This can also be used to make aliases. Using `alias.[name]` you can either set up short hand for existing command or make new commands that you want.

```
git config --global alias.unstage 'reset HEAD --'
This makes git unstage fileA the same as git reset HEAD fileA

git config --global alias.last 'log -1 HEAD'
This makes git last the same as git log -1 HEAD
```

## git init [Documentation](http://git-scm.com/docs/git-init "Git Init Documentation")

Create a new local repository.

```
git init   
```

## git clone [Documentation](http://git-scm.com/docs/git-clone "Git Clone Documentation")

Copy an existing repository, [name] is optional, will name local repository this instead. `git clone` will set up a server remote named origin with a branch named master that automatically tracks the remote branch.

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

This is the shorthand that can be used to move a file in Git. This is also the shorthand for renaming a file using Git. Run this and Git will stage the rename for you.

```
git mv [file] [path]
git mv [old_file_name] [new_file_name]
```

This is what Git does for you when you run git mv. It renames the file, `git rm [old_file_name]`, then `git add [new_file_name]`. Saves you from writing three lines to just one.

```
mv 	[old_file_name] [new_file_name]
git rm [old_file_name]
git add [new_file_name]
```

## git commit [Documentation](http://git-scm.com/docs/git-commit "Git Commit Documentation")

Records the staged changes to the local repository. This will launch the text editor that was configured in the `git config core.editor` command with comments of the latest git status command in it. Add your message under the comments or just delete them and it will be saved and commited after the editor is closed. Adding `-v` will put the diff of your changes in the editor as well. Adding `-m ""` will allow you to do an inline message and skip opening up the editor. Will instantly commit when this command runs.

```
git commit
git commit -v
git commit -m "Whatever you want the commit message to be goes here."
```

You can skip staging by adding `-a` to the commit. This will stage every file that is being tracked into the commit for you. By using `-a` and `-m` you can do quicker commits. After the commit was successful it will show the branch commited to, the SHA-1 id, how many files were changed, and stats on the lines added and removed.

```
git commit -a -m "This is my commit message."
```

If you want to change the commit message or forgot to stage a file to the last commit, `--amend`. If you made no changes since the commit, it will just open up the editor and let you overwrite the commit message. 

```
// Example from Git docs

$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

## git push [Documentation](http://git-scm.com/docs/git-push "Git Push Documentation")

To send changes to the remote is where `git push` comes in. This only works if you have write access and if no one has pushed before you. If someone has pushed before you then your push will be rejected. You will have to pull down their work and merge it into yours before you can push to the remote. To push tags to remote servers you can run `git push [remote-name] [tagname]` or to push all tags that aren't already on the remote server you can do `--tags` instead.

```
git push [remote-name] [branch-name]
git push [remote-name] [tagname]
git push [remote-name] --tags

Example of pushing to the master branch of your origin server (git clone sets this up for you automatically)
git push origin master
```

## git log [Documentation](http://git-scm.com/docs/git-log "Git Log Documentation")

This pulls up the existing commit history for the current repository from newest to oldest. Adding `-p` will show the diff for each commit. Adding `--word-diff` after `-p` will take out the added and removed lines and shows changes inline instead. `--stat` will give a short summary of stats for each commit. `--graph` will show an ASCII graph of your branch and merge history on the left side. Using `--pretty` with `oneline`, `short`, `full`, or `fuller` will display the output differently with more or less information. `--pretty` can also be passed `format:"Make up a format here."` to display whatever you want. Options for `format` and other options for `git log` can be found in the documentation, there are quite a few.

```
git log -p -3
git log -p --word-diff
git log --stat
git log --pretty=format:"%h - %an, %ar : %s"
git log -3 --pretty=oneline --graph
```

There are also options to limit and filter `git log`. Adding `-(n)` will pull the last `(n)` commits only where `(n)` is some number. `--since`, `--before` to limit the commits to those made after the specified date. `--until`, `--before` to limit the commits to those made before the specified date. Plus many more in the Git docs.

```
git log --pretty=format:"%h - %an, %ar : %s" --author=lkosch --since="2013-11-01" --before="2013-12-01"
```

Running `gitk` opens a GUI that is a visual `git log`.

```
gitk
```

## git reset [Documentation](http://git-scm.com/docs/git-reset "Git Reset Documentation")

To unstage a file use `git reset HEAD [file]`. Using `git reset --hard [hash/tag]` will reset the branch to the given commit and the `--hard` is so that the working directory is updated to be consistent with the new branch head. Using this wont erase the other commits and can be seen with the `git log --all` command and referenced to by their tags or hashes.

```
git reset HEAD README.md
git reset --hard [hash/tag]
```

## git checkout [Documentation](http://git-scm.com/docs/git-checkout "Git Checkout Documentation")

If you want to overwrite a modified file with say a last commited version you can use `git checkout`. Any uncommited changes will be lost forever you use this command. This overwrites the file with the one you are checking out. If misused you could lose data that you can not recover.

```
git checkout -- README.md
```

## git remote [Documentation](http://git-scm.com/docs/git-remote "Git Remote Documentation")

`git remote` will show a list of shortnames for each remote you've specified. Adding `-v` will show the URL that Git stored. `git remote add` allows you to add a new remote Git repository with a shortname. Adding `show` will display information about a specific remote. Will show branches and where `git pull` and `git push` will go for branches. Using `git remote rename` changes the shorthand for a remotes. This also changes remote branch names too, `[old-name]/master` to `[new-name]/master`. To remove a remote just use `git remote rm`.

```
git remote -v
git remote add [shortname] [url]
git remote show [remote-name]
git remote rename [old-name] [new-name]
git remote rm [remote-name]
```

## git fetch [Documentation](http://git-scm.com/docs/git-fetch "Git Fetch Documentation")

Using `git fetch` will grab any new data from the remote since you cloned or last fetched. This does not automatically merge that data though.

```
git fetch [remote-name]
```

## git pull [Documentation](http://git-scm.com/docs/git-pull "Git Pull Documentation")

If a branch is set up to track a remote branch then using `git pull` will grab any new data from the remote since you cloned or last fetched and try to merge this data with your current branch.

```
git pull [remote-name]
```

## git tag [Documentation](http://git-scm.com/docs/git-tag "Git Tag Documentation")

Running `git tag` will list available tags. This can be used to search for tags with a pattern. Create annotated tages (recommended) by adding `-a`. You can also throw `-m` to add a message to the tag. If you don't then Git will open up your editor to create a message with. Can use `git show` to see tag data with the commit data the tag was used on. Can also sign tags with GPG if you have a private key by using `-s`. To verify a signed tag with GPG, use `-v`. You must have the signer's public key in your keyring for this to work. You can add tags later if you forget by adding the checksum (or part of it) to the end of the command. To push tags to remote servers you can run `git push [remote-name] [tagname]` or to push all tags that aren't already on the remote server you can do `--tags` instead. To delete a tag locally use `-d`. To delete a tag after it has been pushed `git push --delete origin [tagname]`.

```
git tag
git tag -l 'v1.4.2.*'
git tag -a v0.1 -m 'Alpha Version 0.1 or whatever message you want in here.'
git show v0.1
git tag -v [tag-name]
git tag -a v0.1 -m 'Alpha Version 0.1 or whatever message you want in here.' [checksum]
git push [remote-name] [tagname]
git push [remote-name] --tags
git tag -d [tagname]
git push --delete origin [tagname]
```

You can also create a lightweight tag. This is just the commit checksum stored in a file, it saves no other information and for this reason is somewhat not recommended. A `git show` will only show the commit data since there is no tag data. To create a lightweight tag just don't apply `-a`, `-s`, or `-m`.

```
git tag v0.1
```

## git show [Documentation](http://git-scm.com/docs/git-show "Git Show Documentation")

`git show` can be used to see tag data with the commit data the tag was used on.

```
git show v0.1
```

## git revert

`git revert` can be used to undo a commit. If your on the HEAD you can just use HEAD as the argument to undo the last commit. You can revert any commit using that commits hash. You can edit the commit messaged or use `--no-edit` to skip that and the revert as well as the original commit will be be shown in `git log`.

```
git revert HEAD --no-edit
git revert [hash]
```

## My Git Aliases [Quick Explanation of Aliases](http://git-scm.com/book/en/Git-Basics-Tips-and-Tricks "Quick Explanation of Aliases")

List of Git aliases that I use.

```
git config --global alias.unstage 'reset HEAD --'
This makes git unstage fileA the same as git reset HEAD fileA.

git config --global alias.last 'log -1 HEAD'
This makes git last the same as git log -1 HEAD.

git config --global alias.ls 'ls-files'
Displays a list of files if they have at least been staged.

git config --global alias.ign 'ls-files -o -i --exclude-standard'
Displays a list of ignored files.

git config --global alias.lol 'log --graph --decorate --pretty=oneline --abbrev-commit'
git config --global alias.lola 'log --graph --decorate --pretty=oneline --abbrev-commit --all'
git config --global alias.hist 'log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short'

git config --global alias.type 'cat-file -t'
git config --global alias.dump 'cat-file -p'
```