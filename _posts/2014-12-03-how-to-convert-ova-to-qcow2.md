---
layout: post
title: "How to convert OVA to QCOW2 format"
published: false
description: ""
category: 
tags: [openstack , ova , qcow2 , vmware]
---

Firstly, unarchie files from container

```bash
$ tar -xvf csr1000v.ova
csr1000v-universalk9.03.12.01.S.154-2.S1-std.ovf
csr1000v-universalk9.03.12.01.S.154-2.S1-std.mf
csr1000v_harddisk.vmdk
bdeo.sh
README-OVF.txt
README-BDEO.txt
csr1000v-universalk9.03.12.01.S.154-2.S1-std.iso
```

Check what is inside

```bash
$ file *
bdeo.sh:                                          Bourne-Again shell script, ASCII text executable
csr1000v_harddisk.vmdk:                           VMware4 disk image
csr1000v.ova:                                     POSIX tar archive (GNU)
csr1000v-universalk9.03.12.01.S.154-2.S1-std.iso: # ISO 9660 CD-ROM filesystem data 'CDROM                           ' (bootable)
csr1000v-universalk9.03.12.01.S.154-2.S1-std.mf:  ASCII text
csr1000v-universalk9.03.12.01.S.154-2.S1-std.ovf: XML  document text
README-BDEO.txt:                                  ASCII text
README-OVF.txt:                                   ASCII text
```

Convert vmdk to qcow2 file

```bash
qemu-img convert -O qcow2 csr1000v_harddisk.vmdk csr1000v_harddisk.qcow2
```


