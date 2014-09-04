---
layout: post
title: "how to use old LTS kernel in Ubuntu"
description: ""
category: 
tags: []
---

You can tell dpkg/apt to hold a package at a specific version:

>aptitude hold linux-image-generic
>aptitude hold linux-image-3.2.0-23-generic


That should stop updates from changing your kernel.

Here is a cite from Ubuntu documentation:

12.04 The UDS-Q decision is that we will provide the kernels from 12.10,
13.04, 13.10, and 14.04 in 12.04. We propose the following meta
packages:
* linux-image-<flavour> - this existing meta package will always point to
the GA 3.2 kernel 
* linux-image-hwe-<flavor> -> rolling release meta package. It will point
to thehe hardware enablement kernel package. 
* linux-hwe-<flavor> -> rolling release meta package. It will point to
the hardware enablement kernel and headers packages. 
* linux-image-current-<flavor> - always points to the the most recently
released kernel, e.g., 12.10, 13.04, etc. 
* linux-current-<flavor> - always points to the the most recently
released kernel and headers, e.g., 12.10, 13.04, etc.


{% highlight sh %}
dpkg -l 'linux-*' | sed '/^ii/!d;/'"$(uname -r | sed
"s/\(.*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^
]*\).*/\1/;/[0-9]/!d' | xargs sudo apt-get purge
{% endhighlight %}

{% highlight sh %}
apt-get install linux-image-3.2.0-64-virtual
aptitude hold linux-image-3.2.0-64-virtual
apt-get remove linux-image-3.11.0-15-generic
apt-get remove linux-image-3.11.0-23-generic
{% endhighlight %}

Based on:
[1](http://askubuntu.com/questions/341893/what-is-the-best-way-to-upgrade-the-kernel-in-12-04-3)
[2](http://markmcb.com/2013/02/04/cleanup-unused-linux-kernels-in-ubuntu/)
[3](https://wiki.ubuntu.com/Kernel/Release/Rolling)
