---
layout: post
title: "How to fix ZlibInStream crash VNC"
description: ""
category: 
tags: [VNC, linux]
---


I was really annoyed by crashed VNC. I use vnc often since I build new images for cloud almost everyday
Chicken of the vnc not working properly and I migrate to linux xvnc4viewer. It works much better, but still crashed
I tried to debug little bit and found a trouble


was crashed with main:        ZlibInStream: inflate failed
ssh linux 'xvnc4viewer -FullColor 88.85.71.5:47'
