---
layout: page
title: All posts
tagline: 
---

<ul class="posts" itemscope="" itemtype="http://schema.org/Blog">
  {% for post in site.posts %}
    <li itemprop="blogPost" itemscope="" itemtype="http://schema.org/BlogPosting"><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}" itemprop="url">{{ post.title }}</a>
    <meta itemprop="name" content="{{ post.title }}" />
    <meta itemprop="keywords" content="{{ post.tags | join: ',' }}" />
    <meta itemprop="description" content="{{ post.description }}" />
    </li>
  {% endfor %}
</ul>



