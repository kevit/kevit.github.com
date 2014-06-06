---
title: Apache2 module compilation
date: Fri Jun 01 17:32:40 +0800 2009
published: true
layout: post
categories: apache
---

If you have a source for Apache module, assembling process is quite easy:

{% highlight sh %}
apxs -c mod_authnz_external.c
apxs -i -a mod_authnz_external.la
{% endhighlight %}
