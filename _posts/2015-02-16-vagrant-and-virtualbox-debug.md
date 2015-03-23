---
layout: post
title: "Vagrant and Virtualbox debug"
published: false
description: ""
category: 
tags: []
---


sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian precise contrib" >> /etc/apt/sources.list.d/virtualbox.list'
apt-get update
apt-get install virtualbox-4.3

<?php echo $this->privateMessagesLink ?>


export VBOX_LOG=main.e.l.f+gui.e.l.f
export VBOX_LOG_FLAGS="time tid thread"
export VBOX_LOG_DEST=dir=/tmp/virtualbox.log
kitchen converge -l debug

