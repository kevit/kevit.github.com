---
layout: post
title: "How to make Debian LiveCD"
published: true
description: "Steps to make Debian LiveCD"
category: 
tags: [debian]
---
#Creating Debian LiveCD with SerialConsole boot


## Uncomment to disable graphical terminal (grub-pc only)

```bash
GRUB_TERMINAL=serial
GRUB_SERIAL_COMMAND="serial --speed=115200 --unit=0 --word=8 --parity=no --stop=1"
```

##Prepare building environment

```bash
apt-get install  git-core live-helper
git clone http://git.ciffer.net/svend/live-sc.git
cd live-sc
lh config
```

Be sure that you replaced file mirror to archive.debian.org

##Build image

```bash
lh build
```


##Links
[1](http://svend.ciffer.net/tech/livesc/)
[2](https://help.ubuntu.com/community/SerialConsoleHowto)
