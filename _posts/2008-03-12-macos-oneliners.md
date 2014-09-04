---
layout: post
title: "Useful MacOS cli commands"
description: ""
category: 
tags: []
---

## All kext not from Apple
kextstat | grep -v com.apple

## How to find URL for downloaded file
xattr -l com.apple.metadata:kMDItemWhereFroms file.zip

## How to list all USB devices
system_profiler SPUSBDataType
