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



