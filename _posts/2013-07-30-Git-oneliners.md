---
title: Git oneliners
published: true
date: Fri Jul 30 17:32:40 +0800 2013
layout: post
categories: git
---

###How to check fatal: CRLF would be replaced by LF

```bash
	git config --global core.autocrlf false  
	git config --global core.safecrlf false
```

###How to get remote url

```bash
	git remote show origin
```
###How to add ignoring

```bash
	git config --global core.excludesfile ~/.gitignore_global
```

###How to add excludes

```bash
	vim .git/info/exclude
```

###How to fix git error no refs
No refs in common and none specified; doing nothing.
Perhaps you should specify a branch such as 'master'.

how to fix:

```bash
  git push origin master
```

###how to debug ssh git repo 
```bash
ssh -vT git@git
```

###git new feature workflow

```bash
git clone git@git:cookbooks/swift.git
git branch feature/swift_undelete
git checkout feature/swift_undelete
vim proxy-server.conf.erb
git add proxy-server.conf.erb
git commit -m 'adding swift_undelete middleware'
git push -u origin feature/swift_undelete###
```
### Using a git submodules

```bash
git clone 
git subtree add --prefix images/docker-backup https://github.com/kevit/docker-backup master --squash
```

[More on Atlassian](http://blogs.atlassian.com/2013/05/alternatives-to-git-submodule-git-subtree/)



