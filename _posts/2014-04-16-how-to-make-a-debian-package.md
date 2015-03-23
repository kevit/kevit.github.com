---
layout: post
title: "How to make Debian package based on MBSE BBS "
published: false
description: ""
category: 
tags: []
---

make debian package

sudo apt-get install build-essential autoconf automake autotools-dev
dh-make debhelper devscripts fakeroot xutils lintian pbuilder

wget mbsebbs-1.0.1.tar.bz2
tar xvjf mbsebbs-1.0.1.tar.bz2; cd mbsebbs-1.0.1
dh_make -e simarg@gmail.com -f ../mbsebbs-1.0.1.tar.bz2

vim debian/control

dpkg-depcheck -d ./configure


http://www.webupd8.org/2010/01/how-to-create-deb-package-ubuntu-debian.html
http://www.debian.org/doc/manuals/maint-guide/build.en.html
