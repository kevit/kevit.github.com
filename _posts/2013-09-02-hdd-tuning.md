---
title: "HDD tuning example"
date: Mon Sep 02 15:56:12 +0800 2013
layout: post
published: true
categories: hardware sysadmin 
---

Simple primer


>echo 60 > /proc/sys/vm/dirty_ratio
>echo 20 > /proc/sys/vm/dirty_background_ratio

>echo deadline > /sys/block/sda/queue/scheduler
>echo 2048 > /sys/block/sda/queue/nr_requests
>blockdev --setra 8192 /dev/sda
>echo 256 > /sys/block/sda/queue/iosched/fifo_batch
