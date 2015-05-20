---
layout: post
title: "Building Solaris 11 image for OpenStack"
published: true
description: "Important points of your Solaris 11 image building for OpenStack"
category: 
tags: [solaris, openstack]
---


## Image propeties
Solaris 11 using IDE-bus and Intel e1000 network card. You should use glance with right keys

```bash
glance image-create --name sole1000 --disk-format=qcow2 --container-format=bare --is-public=false --property hw_disk_bus=ide --property hw_vif_model=e1000 < /srv/clientimages/solaris11-k3.qcow2
```
 
## APIC problem

March 2015 Solaris have a troube with booting on x2apic-enabled systems. You should edit your nova-compute settings to run with appropriate flags

```bash
cat /etc/nova/nova-compute.conf
[DEFAULT]
libvirt_cpu_mode=custom
libvirt_cpu_model=Westmere
libvirt_type=kvm
compute_driver=libvirt.LibvirtDriver
```

## Debug

One of most important things to debug - prevent system reboot after kernel or system crash.
grub: adding -k

```bash
kernel$ /platform/i86pc/multiboot -B console=ttyb,$ZFS-BOOTFS -k
```


