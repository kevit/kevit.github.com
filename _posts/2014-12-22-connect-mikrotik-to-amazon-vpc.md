---
layout: post
title: "Connect Mikrotik to Amazon VPC"
description: ""
category: 
tags: [mikrotik, amazon, ipsec, bgp]
---

##Target

I would like to connect my home office with mirkotik router to amazon cloud

##Presettings
https://eu-west-1.console.aws.amazon.com/vpc/home?region=eu-west-1#vpns

You should download file with vpn settings ( for other vendors ). Inside the
file you will find ip's for your tunnels and bgp peers

##Configure mikrotik router
```bash
/ip address add address= 78.140.190.216/28 interface=ether1
/ip route add gateway=78.140.190.209


/ip address add address= 169.254.254.58/30 interface=ether1
/ip address add address= 169.254.254.62/30 interface=ether1


/ip ipsec policy add src-address=0.0.0.0/0 src-port=any dst-address=172.31.0.0/16 dst-port=any protocol=all action=encrypt level=require ipsec-protocols=esp tunnel=yes sa-src-address=78.140.190.216 sa-dst-address=176.32.107.246 proposal=default priority=0 

/ip ipsec policy add src-address=169.254.254.58/32 src-port=any dst-address=169.254.254.57/32 dst-port=any protocol=all action=encrypt level=require ipsec-protocols=esp tunnel=yes sa-src-address=78.140.190.216 sa-dst-address=176.32.107.246 proposal=default priority=0 

/ip ipsec policy add src-address=169.254.254.62/32 src-port=any dst-address=169.254.254.61/32 dst-port=any protocol=all action=encrypt level=require ipsec-protocols=esp tunnel=yes sa-src-address=78.140.190.216 sa-dst-address=176.32.107.244 proposal=default priority=0 

/ip ipsec policy add src-address=169.254.254.57/32 src-port=any dst-address=169.254.254.58/32 dst-port=any protocol=all action=encrypt level=require ipsec-protocols=esp tunnel=yes sa-src-address=176.32.107.246 sa-dst-address=78.140.190.216 proposal=default priority=0 

/ip ipsec policy add src-address=169.254.254.61/32 src-port=any dst-address=169.254.254.62/32 dst-port=any protocol=all action=encrypt level=require ipsec-protocols=esp tunnel=yes sa-src-address=176.32.107.244 sa-dst-address=78.140.190.216 proposal=default priority=0


/ip ipsec peer add address=176.32.107.244/32 local-address=78.140.190.216 passive=no port=500 auth-method=pre-shared-key secret="ENs0jsTtItxeQRoLMozf4xK8IMteyi_d" generate-policy=no exchange-mode=main send-initial-contact=yes nat-traversal=no proposal-check=obey hash-algorithm=sha1 enc-algorithm=aes-128 dh-group=modp1024 lifetime=8h lifebytes=0 dpd-interval=10s dpd-maximum-failures=3 

/ip ipsec peer add address=176.32.107.246/32 local-address="78.140.190.216" passive=no port=500 auth-method=pre-shared-key secret="cUNDGzkWu3n0zsN_CQieRPerO0K9DS7B" generate-policy=no exchange-mode=main send-initial-contact=yes nat-traversal=no proposal-check=obey hash-algorithm=sha1 enc-algorithm=aes-128 dh-group=modp1024 lifetime=8h lifebytes=0 dpd-interval=10s dpd-maximum-failures=3


/ip firewall filter add chain=input action=accept protocol=ipsec-esp src-address=176.32.107.246 dst-address=78.140.190.216 in-interface=ether1

/ip firewall filter add chain=input action=accept protocol=udp src-address=176.32.107.246 dst-address=78.140.190.216 in-interface=ether1 src-port=500 dst-port=500 

/ip firewall filter add chain=input action=accept protocol=ipsec-esp src-address=176.32.107.244 dst-address=78.140.190.216 in-interface=ether1
/ip firewall filter add chain=input action=accept protocol=udp src-address=176.32.107.244 dst-address=78.140.190.216 in-interface=ether1 src-port=500 dst-port=500

/ip firewall filter add chain=input action=accept protocol=tcp src-address=169.254.254.57 dst-address=169.254.254.58 dst-port=179 

/ip firewall filter add chain=input action=accept protocol=tcp src-address=169.254.254.61 dst-address=169.254.254.62 dst-port=179

/ip firewall filter add chain=forward action=accept src-address=172.31.0.0/16 in-interface=ether1


/routing bgp instance add name="vgw-1" as=65000 router-id=169.254.254.58 redistribute-connected=no redistribute-static=yes redistribute-rip=no redistribute-ospf=no redistribute-other-bgp=no out-filter="" client-to-client-reflection=no ignore-as-path-len=no routing-table="" 

/routing bgp instance add name="vgw-2" as=65000 router-id=169.254.254.62 redistribute-connected=no redistribute-static=yes redistribute-rip=no redistribute-ospf=no redistribute-other-bgp=no out-filter="" client-to-client-reflection=no ignore-as-path-len=no routing-table=""

/routing bgp peer add name="awsvpc1" instance=vgw-1 remote-address=169.254.254.57 remote-as=9059 tcp-md5-key="" nexthop-choice=default multihop=no route-reflect=yes hold-time=30s ttl=default in-filter="" out-filter="" address-families=ip update-source=169.254.249.30 default-originate=never remove-private-as=no as-override=no passive=no use-bfd=no 

/routing bgp peer add name="awsvpc2" instance=vgw-2 remote-address=169.254.254.61 remote-as=9059 tcp-md5-key="" nexthop-choice=default multihop=no route-reflect=yes hold-time=30s ttl=default in-filter="" out-filter="" address-families=ip update-source=169.254.249.26 default-originate=never remove-private-as=no as-override=no passive=no use-bfd=no
```



[Source](http://forum.mikrotik.com/viewtopic.php?f=2&t=87844)
[Initial setup](http://wiki.mikrotik.com/wiki/Manual:First_time_startup)


