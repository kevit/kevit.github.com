---
layout: post
title: "Managing your JBOD on LSI"
description: "Some CLI magic for your storage server based on LSI controller"
category: 
published: true
tags: [linux]
---

##Firmware update on LSI 9207

```bash
./sas2flash -listall
./sas2flash -b 9207-8e.rom -c 0
./sas2flash -f 9207-8e.bin -c 0
./sas2flash -listall
```

##Check number of disks

```bash
lsscsi | grep dev| wc -l
```

##Getting partition UUIDS

```bash
IFS=$'\n'; for i in ` ls -l /dev/disk/by-uuid/ | grep -v total | awk '{print $9, $11}' | sed 's|../../||' `; do P=`echo ${i} | awk '{print $2}'`; echo -n "${i} "; fdisk -s /dev/${P}; done | sort -k3n,3 -k2
```

##Getting all HDD serial numbers 

```bash
sas2ircu 0 DISPLAY|grep "Serial No" > /tmp/file ; sas2ircu 1 DISPLAY|grep "Serial No" >> /tmp/file; cat /tmp/file |grep -v x
```

##Reattach disk by SCSI id

```bash
echo 'scsi remove-single-device X X X X' > /proc/scsi/scsi && echo 'scsi add-single-device X X X X' > /proc/scsi/scsi
```

## Flashing LED for onsite support

```bash
wget https://raw.githubusercontent.com/amarao/sdled/master/encled; chmod a+x encled; ./encled
```

## Go deeper

```bash
apt-get install sg3-utils
```

Firstly, looking for the enclosures

```bash
sg_map -i |grep LSI
/dev/sg26  LSILOGIC  SASX36 A.1        7017
/dev/sg51  LSI CORP  SAS2X36           0717
/dev/sg73  LSI CORP  SAS2X36           0717
```

Then looking for the information pages

```bash
sg_ses -p 0 /dev/sg73
LSI CORP  SAS2X36           0717
Supported diagnostic pages:
Supported Diagnostic Pages [sdp] [0x0]
Configuration (SES) [cf] [0x1]
Enclosure Status/Control (SES) [ec,es] [0x2]
Element Descriptor (SES) [ed] [0x7]
Additional Element Status (SES-2) [aes] [0xa]
Download Microcode (SES-2) [dm] [0xe]
```


We are interesting in Status and Control page (SES)

```
Enclosure Status/Control (SES) [ec,es] [0x2]
```

Mapping slot to SAS address

```bash
sg_ses -p 0xa /dev/sg73 |grep -E 'slot|  SAS address' |sed 'N;s/\n//' | awk '{print $3, " ", $NF}'

```

## Links

* [sg_ses](http://sg.danny.cz/sg/sg_ses.html)
* [Explained sg_ses manual](http://matrix207.github.io/2013/06/20/use-sg_ses/)
