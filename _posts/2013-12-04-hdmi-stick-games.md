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


apt-get install build-essential



sudo apt-get install android-tools-adb
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="2207", MODE="0666", GROUP="plugdev"' > "/etc/udev/rules.d/51-android.rules" 
udevadm control --reload-rules

Log in with your normal    unix user, and edit ~/.android/adb_usb.ini,
add 0x2207 at the end of the file
As user, restart the adb server with "adb kill-server; adb
start-server"

As user, you should be able to list your device with "adb devices"

adb shell

```bash
#cat /proc/cpuinfo
Processor: ARMv7 Processor rev 0 (v7l)
BogoMIPS: 1631.46
Features: swp half thumb fastmult vfp edsp neon vfpv3 
CPU implementer: 0x41
CPU architecture: 7
CPU variant: 0x3
CPU part: 0xc09
CPU revision: 0

Hardware: RK2928board
Revision: 0000
Serial: 0000000000000000
```

```bash
root@android:/data # lsmod
wlan 652931 0 - Live 0x00000000
vpu_service 11919 0 - Live 0x00000000
mali 101258 2 - Live 0x00000000
ump 26232 5 mali, Live 0x00000000
```

```bash
cat /proc/version                                         
Linux version 3.0.36+ (lynn@lynn-GA-78LMT-S2P) (gcc version 4.6.x-google 20120106 (prerelease) (GCC) ) #1 PREEMPT Wed Oct 9 17:11:20 CST 2013
```

http://www.rockchipfirmware.com/developer-tools
http://stackoverflow.com/questions/14460656/android-debug-bridge-adb-device-no-permissions


Then:
disassemble squashfs
install dropbear


http://forum.xda-developers.com/showthread.php?t=2339152


TODO: WTF YOU MEAN GPS??111
