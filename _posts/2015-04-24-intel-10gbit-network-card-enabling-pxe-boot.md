---
layout: post
title: "Intel 10Gbit network card enabling PXE boot"
description: "Intel X540-AT2 card boot settings"
category: 
published: true
tags: [linux, intel, nic, 10gbit, X540-AT2]
---

Usually people asking me, what kind of task I am handson everydays. Today was a normal day.


##Problem

No pxe boot from 10Gbit Intel Nic

##Reconnaissance

```bash
lspci -nn
8086:1528
```

```bash
root@server:~# ethtool -i eth4
driver: ixgbe
version: 3.6.7-k
firmware-version: 0x80000389
```


Download bootutil from [Intel site](https://downloadcenter.intel.com/download/19186/Intel-Ethernet-Connections-Boot-Utility-Preboot-images-and-EFI-Drivers)

##Run flascher

```bash
cd /tmp; tar xvzf Preboot.tar.gz; cd /tmp/APPS/BootUtil/Linux_x64; chmod 755 ./bootutil64e; ./bootutil64e -BOOTENABLE=PXE -ALL
```

