---
layout: post
title: "Useful MacOS cli commands"
published: true
description: ""
category: 
tags: [osx, cli]
---

## List all kext not from Apple
```bash
kextstat | grep -v com.apple
```

## How to find URL for downloaded file
```bash
xattr -l com.apple.metadata:kMDItemWhereFroms file.zip
```

## How to list all USB devices
```bash
system_profiler SPUSBDataType
```

## How to get sha1 checksum for the file
```bash
sha1sum file
```
