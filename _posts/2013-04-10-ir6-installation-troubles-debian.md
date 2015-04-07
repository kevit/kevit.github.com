---
layout: post
title: "How to fix some kind of installation troubles SAS/IR6 in Debian"
published: true
description: "IR6 controller debugging in Debian"
category: 
tags: [ir6, debian]
---

## Different kind of installation troubles

Put in GRUB

```bash
rootdelay=60
```

## So big partition

1. create a grubbios
2. create a 200Mb boot

## Readonly isw raid:

```bash
dmraid --stop
[root@localhost ~]# dmraid -r -E /dev/sdc Do you really want to erase
“pdc” ondisk metadata on /dev/sdc ? [y/n] :y
```

or 

```bash
mdadm –zero-superblock /dev/sdx
http://retsepts.blogspot.sg/2012/02/mdadm.html
```


## If GRUB install failed:

```
replace a /dev/mapper to appropriate /dev/mapper/isw_cchibbaeag_Volume0
```
