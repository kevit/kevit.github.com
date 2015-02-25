---
title: Centos oneliners
published: true
date: Fri Jul 30 17:32:40 +0800 2013
layout: post
categories: centos
---

##How to disable SELinux

```bash
echo 0 >/selinux/enforce; sed -ri 's/SELINUX=enforcing/SELINUX=disabled/' /etc/sysconfig/selinux
```

remove graphic boot in centos
```
sed -i "s/rhgb quiet//g" /boot/grub/grub.conf
```
