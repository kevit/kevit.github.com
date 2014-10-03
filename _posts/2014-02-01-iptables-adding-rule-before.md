---
layout: post
title: "How to add rule in iptables before anything else"
description: ""
category: 
tags: []
---

{% highlight sh %}
iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT
{% endhighlight %}
