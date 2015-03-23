---
layout: post
title: "Introduction to IPv6"
description: ""
category: 
tags: [ipv6]
---

##

###Concepts
ARP -> NDP (NS/NA)
DHCP -> autooconfigure
ICMP -> ICMPv6

###Addresation
Link-local
Такой адрес всегда начинается с FE80, ну а последние 64 бита — это мак-адрес с FFFE, вставленными посередине, плюс один бит инвертирует
EUI-64
Global unicast

###Configure network
ICMPv6 133 request / 134 advertisement
DHCPv6

###Looking around
ip -6 neighbor show, а в Windows среде это можно сделать командой netsh interface ipv6 show neighbors.

###Scanning
alive6 from THC-IPV6
alive6 -p eth0 2001:67c:238::0-ffff::0-2
Alive: 2001:db8:238:1::2 [ICMP echo-reply]
Alive: 2001:db8:238:3::1 [ICMP echo-reply]

 ipv6_neighbor, так и отдельные скрипты ipv6_surface_analyzer
