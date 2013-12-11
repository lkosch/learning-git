# .gitconfig --global for Windows

A copy of my --global .gitconfig file for Windows. For a backup and also so I can use it between PCs.


```
[user]
	name = [name]
	email = [email]
[core]
  editor = 'c:/program files/sublime text 2/sublime_text.exe' -w
  whitespace=fix,-indent-with-non-tab,trailing-space,cr-at-eol,space-before-tab
  autocrlf = true
[color]
  ui = auto
[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green
[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red bold
  new = green bold
  whitespace = red reverse
[color "status"]
  added = green
  changed = yellow
  untracked = cyan
[web]
	browser = chrome
[alias]
	last = log -1 HEAD
	unstage = reset HEAD --
	ls = ls-files
	ign = ls-files -o -i --exclude-standard
	lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
	lol = log --graph --decorate --pretty=oneline --abbrev-commit
	hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
	type = cat-file -t
	dump = cat-file -p
  stash-unapply = !git stash show -p | git apply -R
[branch]
	autosetupmerge = true
[imap]
  folder = "[Gmail]/Drafts"
  host = imaps://imap.gmail.com
  user = user@gmail.com
  pass = p4ssw0rd
  port = 993
  sslverify = false

```
