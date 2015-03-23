---
layout: post
title: "How to make Python Debian package"
published: false
description: ""
category: 
tags: []
---

##Building packages
Firstly, you need python's stdeb module:

> apt-get install python-stdeb

Then in source directory generate a deb-package:

> python setup.py --command-packages=stdeb.command bdist_deb

And finally install package in system:

> dpkg -i deb_dist/python-nginxcachecleaner_*_all.deb
