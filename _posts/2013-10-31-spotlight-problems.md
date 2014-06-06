---
title: "Spotlight problems"
date: Thu Oct 31 17:27:39 +0800 2013
layout: post
published: true
categories: osx
---

## Spotlight go nuts and eating 100% CPU. Not a trouble, really


  #!sh
  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist

## Another useful comands



  #!sh
  mdutil -i off /
  mdutil -i on /
  mdutil -E /
