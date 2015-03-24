---
title: How to work with USB-Serial in OSx
date: Sat Oct 27 17:32:40 +0800 2012
published: true
description: "WHC341 and PL2303 hardware in OSX"
layout: post
category: 
tags: [osx, hardware, sysadmin]
---

## WCH341 based hardware
Unfortunately, no tty device presented, only userspace hardware.
You can download application from [here](http://www.staarcom.com/software/WCH341-Terminal/WCH341-Terminal.zip)


## PL2303 based hardware

Firstly download a kext from [link](http://www.xbsd.nl/pub/osx-pl2303.kext.tgz) and put to the /System/Library/Extensions
Then load kext and rebuild cache

```bash
cd /System/Library/Extensions
kextload ./osx-pl2303.kext
kextcache -system-cache
```

Then you can use your adapter from CLI

```bash
sudo cu -l /dev/tty.PL2303-000012FD
```

* [WCH341 source](http://www.staarcom.com/software/WCH341-Terminal/index.html)
* [PL2303 source](http://xbsd.nl/2011/07/pl2303-serial-usb-on-osx-lion.html)
* [Originally found WCH341 software here](http://menelkir.itroll.org/2013/08/wch341-usb-serial-converter-for-osx.html)
