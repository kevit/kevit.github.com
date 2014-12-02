---
layout: post
title: "How to debug Git ssh access"
description: ""
category: 
tags: [git, ssh]
---

#### How to regenerate public key using old private key
```bash
ssh-keygen -y -f private.key
```

#### How to check connect to the git repository using ssh
```bash
 ssh -vT git@git.pagodabox.com
```
