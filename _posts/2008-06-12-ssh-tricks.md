---
layout: post
title: "ssh tricks"
published: false
description: ""
category: 
tags: [ssh]
---

###stop key auth
ssh -o "PubkeyAuthentication no" username@hostname

###How to debug ssh forwarding
ssh-add -l

###How to avoid host key checking
ssh -o StrictHostKeyChecking=no cloud-user@188.42.225.33
