---
layout: post
title: "Baking an openstack image"
published: false
description: "There a list of different ways how to make Openstack images"
category: 
tags: [openstack]
---


##Centos/RHEL

```bash
virt-builder centos-6 \
    --run-command 'rpm -ivh
http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm'
\
    --update \
    --install cloud-utils,cloud-init 
```



##Debian/Ubuntu

```bash
build-openstack-debian-image -m -r wheezy 
```

##Triple-O way

```bash
apt-get install uuid-runtime
git clone https://github.com/openstack/diskimage-builder

DIB_RELEASE=trusty ./bin/disk-image-create -u -a amd64 ubuntu vm base cloud-init-nocloud -o /tmp/image.qcow2
```



##Packer

Packer is a most universal way to prepare an image

```bash
packer
```

