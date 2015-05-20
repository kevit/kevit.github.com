---
layout: post
title: "Adding Junos 10.4 image into Openstack"
description: "Now our OpenStack got a Junos: there is a short explanation"
category: 
published: false
tags: []
---

##Preparation
You should find a JunOS Vmware image and convert them into QCOW2

```bash
qemu-img convert JunOS-10.4.vmdk -O qcow juniper.qcow2
```

Load your image into OpenStack using right hardware flag settings

```bash
glance image-create --name junos --disk-format=qcow2 --container-format=bare --is-public=false --property hw_disk_bus=ide --property hw_vif_model=e1000 < juniper.qcow2
```

[Building your own Olive](http://brezular.com/2012/08/04/how-to-run-junos-installed-on-qemu-on-virtualbox-part1-introduction/)
