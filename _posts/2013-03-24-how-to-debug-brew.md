---
layout: post
title: "How to debug brew receipt setup"
published: true
description: "Dark side of brewery in OSX"
category: 
tags: [osx]
---

## brew debugging:
Error: You must brew link pkg-config' before lftp can be installed

```bash
brew link --overwrite --dry-run pkg-config
brew link --overwrite xz
```


## another debugging example

```bash
$brew install nmap
Warning: nmap-6.40 already installed, it's just not linked
$brew link nmap
Linking /usr/local/Cellar/nmap/6.40... Warning: Could not link nmap.
Unlinking...
$brew link --overwrite nmap
```
