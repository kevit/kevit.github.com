---
layout: post
title: "Useful glance commands"
published: false
description: ""
category: 
tags: [glance, openstack]
---

#change an image name
glance image-modify --name "WindowsXP" 1776205d-beee-4eef-8b0f-c8b3298f1936

#share image
glance member-create 1776205d-beee-4eef-8b0f-c8b3298f1936 7e913b8e8edd4e35b94e68e532e32174

#change hardware properties
glance image-update --property hw_disk_bus=ide --property hw_vif_model=virtio 1776205d-beee-4eef-8b0f-c8b3298f1936

