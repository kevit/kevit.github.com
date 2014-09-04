---
layout: post
title: "How to increase entropy"
description: ""
category: 
tags: []
---

Funny topic, really?


> Not enough random bytes available.  Please do some other work to give
the OS a chance to collect more entropy! (Need 284 more bytes)

{% highlight sh %}
watch -n 1 cat /proc/sys/kernel/random/entropy_avail
{% endhighlight %}

How to fix: increasing entropy!
> apt-get install haveged

