---
layout: post
title: "How to add rule in iptables at the first place"
published: true
description: "Useful way to adding iptables rules"
category: 
tags: [iptables, linux]
---

```bash
iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT
```
