---
layout: post
title: "Adding OSX Mavericks into Openstack"
description: "My findings about OSX in Mavericks"
category: 
published: true
tags: [osx, openstack]
---

## Disclamer

Unfortunately, no direct way to run OSX in cloud founded.


##How to build

### Prepare a disk

### Prepare a iso

### Prepare running environment

You need qemu 2.3, chimera bootloader and secret code from your retail Mac SMC

```bash
qemu-system-x86_64 -enable-kvm -m 2048 -cpu core2duo  -machine q35 -smp 4,cores=2  -usb -device usb-kbd -device usb-mouse \
-device isa-applesmc,osk="string_from_smc"  -kernel chimera_4.1_boot  -smbios type=2  -device ide-drive,bus=ide.2,drive=MacHDD \
-drive id=MacHDD,if=none,file=./mac.img.qcow2  -netdev user,id=hub0port0  -device e1000-82545em,netdev=hub0port0,id=mac_vnet0 \
-device ide-drive,bus=ide.0,drive=MacDVD  -drive id=MacDVD,if=none,snapshot=on,file=./Yosemite.iso \
-monitor stdio -vnc :1
```


##How to run


```bash
qemu-system-x86_64 -enable-kvm -m 2048 -cpu core2duo  -machine q35 -smp 4,cores=2  -usb -device usb-kbd -device usb-mouse \ 
-device isa-applesmc,osk="string_from_smc"  -kernel chimera_4.1_boot  -smbios type=2  -device ide-drive,bus=ide.2,drive=MacHDD \
-drive id=MacHDD,if=none,file=./mac.img.qcow2  -netdev user,id=hub0port0  -device e1000-82545em,netdev=hub0port0,id=mac_vnet0  -monitor stdio -vnc :1
```



## Links

[Andrei Ostanin initial post](http://blog.ostanin.org/2014/02/11/playing-with-mac-os-x-on-kvm/)
[Gabriel L. Somlo work](http://www.contrib.andrew.cmu.edu/~somlo/OSXKVM/)
[kernelpanik page based on Andrei post](http://kernelpanik.net/running-mac-osx-yosemite-on-kvm/)
[Some chameleon and VirtIO information](http://blog.definedcode.com/osx-qemu-kvm)

