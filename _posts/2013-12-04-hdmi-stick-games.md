---
title: "HDMI stick games"
date: Wed Dec 04 20:38:48 +0800 2013
layout: post
published: true
tags: hardware linux android 
---

## Prelude
I got a nice HDMI stick. Unfortunately, software not work properly. I
should fix this!

## Connect to linux

```
Feb 23 17:06:10 dreamplug-debian kernel: [4658785.948540] scsi 5:0:0:0:
Direct-Access     rockchip _usb                  PQ: 0 ANSI: 2
Feb 23 17:06:10 dreamplug-debian kernel: [4658785.961103] sd 5:0:0:0:
Attached scsi generic sg3 type 0
Feb 23 17:06:10 dreamplug-debian kernel: [4658785.970768] sd 5:0:0:0:
[sdf] Attached SCSI removable disk
Feb 23 17:06:10 dreamplug-debian kernel: [4658785.984043] scsi 5:0:0:1:
Direct-Access     rockchip _usb                  PQ: 0 ANSI: 2
Feb 23 17:06:10 dreamplug-debian kernel: [4658786.010852] sd 5:0:0:1:
Attached scsi generic sg4 type 0
Feb 23 17:06:11 dreamplug-debian kernel: [4658786.018900] sd 5:0:0:1:
[sdg] Attached SCSI removable disk
```

```
$ lsusb
Bus 002 Device 023: ID 2207:0010
```
That is nice, new stealth usb device onboard. Just look trough using
goole and USB id. What we got?

http://linux-rockchip.info/mw/index.php?title=Main_Page
http://linux-rockchip.info/mw/index.php?title=ADB_shell_with_RK3066

## Hardware

It is a single chip computer based on ARM Cortex A9. Pretty interesting
to have a full-hd PC for 20 bucks, do you mind?

CPU: RK2928 ARMv7-A ARM Cortex-A9
GPU: Mali-400 MP (330 MHz)
RAM: DDR3, DDR3L RAM support

## Rooting

sudo apt-get install android-tools-adb
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="2207", MODE="0666", GROUP="plugdev"' > "/etc/udev/rules.d/51-android.rules" 
udevadm control --reload-rules

Log in with your normal    unix user, and edit ~/.android/adb_usb.ini,
add 0x2207 at the end of the file
As user, restart the adb server with "adb kill-server; adb
start-server"
•adbAs user, you should be able to list your device with "adb devices"

http://www.rockchipfirmware.com/developer-tools
http://stackoverflow.com/questions/14460656/android-debug-bridge-adb-device-no-permissions


Then:
disassemble squashfs
install dropbear


http://forum.xda-developers.com/showthread.php?t=2339152


TODO: WTF YOU MEAN GPS??111
