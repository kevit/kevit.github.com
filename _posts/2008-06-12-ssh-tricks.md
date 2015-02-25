---
layout: post
title: "ssh tricks"
description: ""
category: 
tags: [ssh]
---

###stop key auth
ssh -o "PubkeyAuthentication no" username@hostname

###How to debug ssh forwarding
ssh-add -l
