---
layout: post
title: "Ssh tricks"
published: true
description: ""
category: 
tags: [ssh]
---

###Prevent key auth
```bash
ssh -o "PubkeyAuthentication no" username@hostname
```

###How to debug ssh forwarding
```bash
ssh-add -l
```

###How to avoid host key checking
```bash
ssh -o StrictHostKeyChecking=no cloud-user@188.42.225.33
```
