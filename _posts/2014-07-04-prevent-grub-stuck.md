---
layout: post
title: "How to prevent grub stucking in boot menu Ubuntu 12.04"
published: false
description: ""
category: 
tags: []
---

{% highlight sh %}
if grep '^GRUB_RECORDFAIL_TIMEOUT='   /etc/default/grub ; then
   echo GOOD: /etc/default/grub
else
   echo FIXING: /etc/default/grub
   perl -pi.bak -e \
      's/^(GRUB_TIMEOUT=.*\n)/${1}GRUB_RECORDFAIL_TIMEOUT=2\n/' \
      /etc/default/grub
   update-grub
fi
{% endhighlight %}

[Based on](http://serverfault.com/questions/243343/headless-ubuntu-server-machine-sometimes-stuck-at-grub-menu)
