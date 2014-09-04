---
title: Git oneliners
published: true
date: Fri Jul 30 17:32:40 +0800 2013
layout: post
categories: git
---

###How to check fatal: CRLF would be replaced by LF

	#!sh
	git config --global core.autocrlf false  
	git config --global core.safecrlf false


###How to get remote url

	#!sh
	git remote show origin

###How to add ignoring

	#!sh
	git config --global core.excludesfile ~/.gitignore_global

###How to add excludes

	#!sh
	vim .git/info/exclude

###How to fix git error no refs
No refs in common and none specified; doing nothing.
Perhaps you should specify a branch such as 'master'.

how to fix:
  #!sh  

  git push origin master

###how to debug ssh git repo 
ssh -vT git@git

###git new feature workflow

git clone git@git:cookbooks/swift.git
git branch feature/swift_undelete
git checkout feature/swift_undelete
vim proxy-server.conf.erb
git add proxy-server.conf.erb
git commit -m 'adding swift_undelete middleware'
git push -u origin feature/swift_undelete###

