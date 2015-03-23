---
layout: post
title: "How to make Debian LiveCD"
published: false
description: ""
category: 
tags: []
---
Creating Debian LiveCD with SerialConsole boot:
http://svend.ciffer.net/tech/livesc/
https://help.ubuntu.com/community/SerialConsoleHowto


# Uncomment to disable graphical terminal (grub-pc only)
GRUB_TERMINAL=serial
GRUB_SERIAL_COMMAND="serial --speed=115200 --unit=0 --word=8 --parity=no
--stop=1"

apt-get install  git-core live-helper
git clone http://git.ciffer.net/svend/live-sc.git
cd live-sc
lh config

replace in bootstrap file mirror to archive.debian.org

#security
http:// archive.debian.org/debian-security/debian

lh build
