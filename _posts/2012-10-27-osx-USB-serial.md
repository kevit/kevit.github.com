---
title: How to work with ATEN UC232A in Macos 10.7
date: Sat Oct 27 17:32:40 +0800 2009
published: true
layout: post
categories: osx hardware sysadmin
---

## WCH341 based hardware
Unfortunately, no tty device presented, only userspace hardware

http://menelkir.itroll.org/2013/08/wch341-usb-serial-converter-for-osx.html
http://www.staarcom.com/software/WCH341-Terminal/index.html

## PL2303 based hardware
http://xbsd.nl/2011/07/pl2303-serial-usb-on-osx-lion.html

Then 
sudo cu -l /dev/tty.PL2303-000012FD
