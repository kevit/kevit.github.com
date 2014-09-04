---
layout: post
title: "How to debug brew receipt setup"
description: ""
category: 
tags: []
---

## brew debugging:
Error: You must brew link pkg-config' before lftp can be installed
brew link --overwrite --dry-run pkg-config
brew link --overwrite xz

## another debugging example
$zsh: command not found: nmap
$brew install nmap
Warning: nmap-6.40 already installed, it's just not linked
$brew link nmap
Linking /usr/local/Cellar/nmap/6.40... Warning: Could not link nmap.
Unlinking...
$brew link --overwrite nmap
