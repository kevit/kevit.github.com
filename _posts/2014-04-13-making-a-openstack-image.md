---
layout: post
title: "Making an openstack image"
published: false
description: ""
category: 
tags: []
---


making an images for openstack: different ways

virt-builder centos-6 \
    --run-command 'rpm -ivh
http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm'
\
    --update \
    --install cloud-utils,cloud-init 



debian way
build-openstack-debian-image -m -r wheezy 

packer
