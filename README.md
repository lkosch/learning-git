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

Tells you what branch you are on. Gives a general overview of untracked files, files that haven't been staged, and files that are staged and ready for commit. Files can show up in the Changes to be commited and the Changes not staged for commit if the file has been modified since the last time it was staged. This can also be used to show unmerged files if there has been a merge conflict.

```
git status
```

## git diff [Documentation](http://git-scm.com/docs/git-diff "Git Diff Documentation")

This shows you changes to files that have not yet been staged. If all your changes have been staged this will show no output. You can add `--cached` or in versions Git 1.6.1 and later you can add `--staged`. Adding this compares your staged changes to your last commit. Adding `--check` will inform you of possible whitespace errors that you may wish to correct. To show only the work a branch has introduced since its common ancestor with another branch you can do `[branch]...[topic-branch]`, so something like `master...[branch-from-master]`

```
git diff
git diff --staged
git diff --check
git diff [branch]...[topic-branch]
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

To open an interactive shell displaying staged and unstaged changes as well as commands use `-i` or `--interactive`. This can be used to stage certain files or parts of files into seperate commits. `-p` or `--patch` can also be used for adding parts of files. [git add -i](http://git-scm.com/book/en/Git-Tools-Interactive-Staging "-i Quick Guide")

```
git add -i
git add -p
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

If you want to change the commit message or forgot to stage a file to the last commit, `--amend`. If you made no changes since the commit, it will just open up the editor and let you overwrite the commit message. This changes the SHA-1 of the commit, like a small rebase, so you shouldn't use this if you have already pushed the commit to a remote.

```
// Example from Git docs

$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

## git push [Documentation](http://git-scm.com/docs/git-push "Git Push Documentation")

To send changes to the remote is where `git push` comes in. This only works if you have write access and if no one has pushed before you. If someone has pushed before you then your push will be rejected. You will have to pull down their work and merge it into yours before you can push to the remote. To push tags to remote servers you can run `git push [remote-name] [tag-name]` or to push all tags that aren't already on the remote server you can do `--tags` instead. To delete a remote branch use `git push [remote-name] :[branch]`, this kind of says "Take nothing on my side and make it be [remote-branch]"

```
git push [remote-name] [local-branch]:[remote-branch]
git push [remote-name] [branch-name]
git push [remote-name] [tag-name]
git push [remote-name] --tags
git push [remote-name] :[remote-branch]

Example of pushing to the master branch of your origin server (git clone sets this up for you automatically)
git push origin master
```

## git log [Documentation](http://git-scm.com/docs/git-log "Git Log Documentation")

This pulls up the existing commit history for the current repository from newest to oldest. Adding `-p` will show the diff for each commit. Adding `--word-diff` after `-p` will take out the added and removed lines and shows changes inline instead. `--stat` will give a short summary of stats for each commit. `--graph` will show an ASCII graph of your branch and merge history on the left side. Using `--not` will not show commits for a branch that are also in another branch. Using `--pretty` with `oneline`, `short`, `full`, or `fuller` will display the output differently with more or less information. `--pretty` can also be passed `format:"Make up a format here."` to display whatever you want. Options for `format` and other options for `git log` can be found in the documentation, there are quite a few.

```
git log -p -3
git log -p --word-diff
git log --stat
git log [branch] --not [another-branch]
git log --pretty=format:"%h - %an, %ar : %s"
git log -3 --pretty=oneline --graph
```

There are also options to limit and filter `git log`. Adding `-(n)` will pull the last `(n)` commits only where `(n)` is some number. `--since`, `--after` to limit the commits to those made after the specified date. `--until`, `--before` to limit the commits to those made before the specified date. Plus many more in the Git docs.

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

If you want to overwrite a modified file with say a last commited version you can use `git checkout`. Any uncommited changes will be lost forever you use this command. This overwrites the file with the one you are checking out. If misused you could lose data that you can not recover. Using this with a branch name switches HEAD to point to that branch and work from that branches last commit. Adding `-b` will create a new branch with the given name and switch to that branch. `git checkout -b [localbranch] [remotename]/[remotebranch]` will track a remote branch and you can name `[localbranch]` something different than the `[remotebranch]`. We can use `--track` to track a branch fetched from a remote and use the same name which is shorthand for `git checkout -b [branch] [remotename]/[branch]`.

```
git checkout -- README.md
git checkout [branch]
git checkout -b [branch]
git checkout -b [localbranch] [remotename]/[remotebranch]
git checkout --track [remotename]/[remotebranch]
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

## git branch [Documentation](http://git-scm.com/docs/git-branch "Git Branch Documentation")

`git branch` by itself will produce a list of branches. Adding `-v` will show the last commit for each branch. Using `--merged` and `--no-merged` shows the branches that have been merged or not merged into the current checked out branch. `git branch` will make a new branch starting at the commit that HEAD is pointing to with whatever name you pass to it. This does not switch HEAD to point at the new branch though, use `git checkout [branch]` to change where HEAD is pointing. Adding `-b` to `git checkout [branch]` will create a new branch with the given name and switch to that branch. Adding `-d` to `git branch [name]` will delete a branch.

```
git branch
git branch -v
git branch --merged
git branch [name]
git checkout -b [branch]
git branch -d [name]
```

## git merge [Documentation](http://git-scm.com/docs/git-merge "Git Merge Documentation"), [Branching and Merging Explained](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging "Merge Explained")

This will merge the branch you name with the branch you are currently checked out to, so whatever branch that HEAD is pointing to. If you see "Fast forward" after running the merge then the branch you merged in was directly upstream and Git will just move the pointer forward to the new commit. If the commit on the branch isn't a direct ancestorof the branch it's merging into then Git does a three-way merge using the common ancestor of the two branches, the snapshot to merge into, and the snapshot to merge in. This creates a new snapshot and a new commit that points to this snapshot which is called a merge commit and it has more than one parent.

```
git merge [branch]
```

## git rebase [Documentation](http://git-scm.com/docs/git-rebase "Git Rebase Documentation"), [Rebasing Explained](http://git-scm.com/book/en/Git-Branching-Rebasing "Rebasing Explained")

Rebasing makes for a cleaner, linear history rather than just merging does. As taken from the link below, "It works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn". Then you do a fast foward merge. You can also rebase a branch that was branched from a branch without replaying the 1st branch and just replaying the commits from the branch from the 1st branch by using `--onto`. [More Interesting Rebases](http://git-scm.com/book/en/Git-Branching-Rebasing#More-Interesting-Rebases "More Interesting Rebases") will take you to a better explanation of this. **Do not rebase commits that you have pushed to a public repository.** If you do it can cause much confusion plus make your rebase irrelevant if someone pulled the original commits down and merged them then merge your rebased commits, when they push they will be pushing both sets of commits.

```
Start of process

git checkout [topicbranch]
git rebase [basebranch]
git checkout [basebranch]
git merge [topicbranch]

End of process

or

Start of process

git rebase [basebranch] [topicbranch]
git checkout [basebranch]
git merge [topicbranch]

End of process

Then you can do this to delete [topicbranch] to leave a nice clean and linear history.
git branch -d [topicbranch]
```

You can also run an interactive rebase using `-i` to rebase multiple commits and passing how far back you want to go. This will rewrite every commit in the range you select so remember not to do this to any commits you have already pushed. Then when your editor opens you can change pick to edit for any commit you actually want to edit. When you save and exit the editor Git will rewind back to the last commit and then you can using `--amend` to change the commit and `--continue` to cycle through the rest of the rebase. This can also be used to remove or reorder commits in the commmit range. Besides "pick" and "edit" there is also a "squash" option that can be used to make multiple commits become a single commit. Using "edit" will also allow you to split a commit into multiple commits by using `git reset HEAD^` and then staging and commiting files however you want, then just `git rebase --continue` to continue. [Multiple Commit Rebasing](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages "Multiple Commit Rebasing")

```
git rebase -i [commit-range]
```

## git cherry-pick [Documentation](http://git-scm.com/docs/git-cherry-pick "Git Cherry-Pick Documentation")

You can pick a single commit to apply to the branch you are currently one by using `git cherry-pick`. This will take the changes in this commit and apply them to the branch making a new commit with a new date.

```
git cherry-pick [SHA-1 value of commit]
```

## git archive [Documentation](http://git-scm.com/docs/git-archive "Git Archive Documentation")

`git archive` can archive your lastest snapshot into tar or zip, this way you can share a new release of the project with people who don't have Git.

```
Shows turning the master branch into a **tar** archive using `git describe` and `--prefix` to make the name.
git archive master --prefix='project/' | gzip > `git describe master`.tar.gz

Shows turning the master branch into a **zip** archive using `git describe` and `--prefix` to make the name.
git archive master --prefix='project/' --format=zip > `git describe master`.zip
```

## git shortlog [Documentation](http://git-scm.com/docs/git-shortlog "Git Shortlog Documentation")

`git shortlog` summarizes `git log` into something that can be used for things like release announcments.

```
git shortlog

This example shows getting a shortlog since the version you decide on the master branch.
git shortlog --no-merges master --not v1.0.1
```

## git stash [Documentation](http://git-scm.com/docs/git-stash "Git Stash Documentation")

Using `git stash` will throw your current changes into a stash and give you a clean working directory. Adding `list` will print out a list of stashes that are stored. Using `apply` will apply the most recent stash. If you want to apply an older stash you can add the name of the stash to `apply`. To restage files that were staged when stashed use `--index`. When you `apply` a stash it continues to be on the stack, to remove a stash you can use `drop`. `pop` will apply the stash and then immediately drop it from the stack. Using `branch` will make a new branch with the commit you were on when you did the stash, applies the stash, and then drops the stash if it was all successful.

```
git stash
git stash list
git stash apply
git stash apply [stash-name]
git stash --index
git stash drop [stash-name]
git stash pop [stash-name]
git stash branch [branch-name] [stash-name]
```

## git blame [Documentation](http://git-scm.com/docs/git-blame "Git Blame Documentation")

`git blame` allows you to see when each line of a file was lasted and by whom. `-L` lets you limit the lines it shows to a certain range. `-C` will tell you where the code came from orginally, like if it was copied from a file that was already in Git.

```
git blame [file-name]
git blame -C -L [N1,N2] [file-name]
```

## git bisect [Documentation](http://git-scm.com/docs/git-bisect "Git Bisect Documentation")

`git bisect` can be used when you aren't sure what commit a bug was introduced in. `start` will start the bisect, then `bad` will say the current commit is broke. `good` is for the last commit you know the code worked or didn't have the bug in it. Git will figure out the number of commits between the two and will checkout the commit in the middle of the two so you can test it. If the issue isn't in this commit you can use `git bisect good` to continue to the halfway point between the commit you are on the bad commit. Say on this commit you find that it is broken, use `git bisect bad`. When Git figures out which commit is the broken one it will show commit information and the files modified. When finished, use `git bisect reset` to move the HEAD back to where it was before you started the bisect or else things will get wierd.

```
git bisect start
git bisect bad
git bisect good [last-known-good-commit]
git bisect good
git bisect reset
```

If you have a test script that "will exit 0 if the project is good or non-0 if the project is bad" then this can be automated. `[bad-commit]` can be HEAD. This will run the `[test-file]` on each checked out commit until it finds the first broken one.

```
git bisect start [bad-commit] [good-commit]
git bisect run [test-file]
```

## git submodule [Documentation](http://git-scm.com/docs/git-submodule "Git Submodule Documentation"), [Submodule Explained](http://git-scm.com/book/en/Git-Tools-Submodules "Submodule Explained")

Sometimes you want to use external projects inside your project. With `git submodule` you can clone an external project into your project and now you can use Git to keep track of any changes you add to this subdirectory but also be able to merge upstream changes from the actual project. The `.gitmodules` is the file that stores the information for these subdirectories and is versioned like `.gitignore`. When cloning a project with submodules, after you clone the project you have to go into the submodule's directory and run `git submodule init` and `git submodule update`. 

```
git submodule add [URL] [submodule-name]
git submodule init
git submodule update
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

git config --global alias.stash-unapply '!git stash show -p | git apply -R'
```
