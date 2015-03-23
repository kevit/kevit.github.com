---
layout: post
title: "Linux to ASA VPN"
description: ""
category: 
tags: []
---

## Cisco ASA 5505

ip cisco 188.164.255.47
ip linux box 206.54.167.110
internal net 10.1.15.0/24

access-list 100 extended permit ip host 206.54.167.110 any

crypto ipsec transform-set myset esp-3des esp-sha-hmac
!--- Define the transform set for Phase 2.
crypto map outside_map 20 match address 100
!--- Define which traffic can be sent to the IPsec peer.
crypto map outside_map 20 set peer 206.54.167.110
!--- Sets the IPsec peer.
crypto map outside_map 20 set transform-set myset
!--- Sets the IPsec transform set "myset"
!--- to be used with the crypto map entry "outside_map"
crypto map outside_map interface outside
!--- Crypto map applied to the outside interface of the ASA


crypto isakmp enable outside
crypto isakmp policy 10
 authentication pre-share
 encryption 3des
 hash sha
 group 2
 lifetime 86400

tunnel-group 206.54.167.110 type ipsec-l2l
tunnel-group 206.54.167.110 ipsec-attributes
  ipsec_onevpn pre-shared-key key
!


## Linux Side

```bash
apt-get install openswan ntp ike-scan ipsec-tools
```

#####
#####
config setup

        listen=100.120.5.40
        plutodebug=all
        klipsdebug=all
        plutoopts="--perpeerlog"

        nat_traversal=yes
        virtual_private=%v4:10.1.15.0/24,%v4:10.1.16.0/24,%v4:100.120.5.0/24
        oe=off #opportunistic encryption is off
        protostack=netkey #use netkey over klips(old version)
        plutostderrlog=/tmp/pluto.log

conn L2L-IPSEC
        auto=start #automatically start if detected
        type=tunnel #tunnel mode/not transport

        ###THIS SIDE###
  left=206.54.167.110
#        leftsubnet=10.1.15.0/24
#        leftsourceip=10.1.15.1 # this is needed so Openswan knows what IP to source from when packets originate on this side of the tunnel.
  leftsourceip=100.120.5.40
        ###PEER SIDE###
        right=188.164.255.47
        rightsubnet=10.1.16.0/24

        #phase 1 encryption-integrity-DiffieHellman
        keyexchange=ike
        ike=3des-md5-modp1024,aes256-sha1-modp1024
        ikelifetime=86400s
        authby=secret #use presharedkey
        rekey=yes  #should we rekey when key lifetime is about to expire

        #phase 2 encryption-pfsgroup
        phase2=esp #esp for encryption | ah for authentication only
        phase2alg=3des-md5;modp1024
        pfs=no
        forceencaps=yes

###Linux debug

/etc/ipsec.conf
# klipsdebug=all
# plutodebug=all

tcpdump port 500
tail -f /var/log/syslog /tmp/pluto.log


ipsec whack --listen
ipsec auto --add connect1
ipsec look
ipsec verif
ipsec auto --up L2L-IPSEC

022 "L2L-IPSEC": We cannot identify ourselves with either end of this connection
you have no interfaces on your linux box and left=


### Cisco Debug
capture capin interface outside match ip host 206.54.167.110 any
show cap capin
clear cap capin

clear config access-list 100

more system:running-config | inc pre-shared-key
pre-shared-key key






debug crypto isakmp 127
debug crypto ipsec 127


vpnsetup site-to-site steps

sh crypto isakmp sa
sh crypto ipsec sa
sh vpn-sessiondb l2l
sh vpn-sessiondb detail l2l
sh parser dump all | include debug vpn 



sh conn all

===
Feb 16 13:36:40 [IKEv1]: IP = 206.54.167.110, No crypto map bound to interface... dropping pkt

crypto ipsec transform-set SITESET esp-3des esp-sha-hmac
crypto map site2site 10 set transform-set SITESET
crypto map site2site interface outside

===
[IKEv1 DEBUG]: Group = 206.54.167.110, IP = 206.54.167.110, All SA proposals found unacceptable
tripple check your settings! i had des in linux, but 3des on cisco

===
Group = 206.54.167.110, IP = 206.54.167.110, Session is being torn down. Reason: crypto map policy not found

crypto map site2site 10 set peer 206.54.167.110

Feb 16 14:13:46 [IKEv1]: Group = 206.54.167.110, IP = 206.54.167.110, Rejecting IPSec tunnel: no matching crypto map entry for remote proxy 100.120.5.0/255.255.255.0/0/0 local proxy 10.0.16.0/255.255.255.0/0/0 on interface outside

access-list L2LACL extended permit ip any any
access-list TUNNEL extended permit 
crypto map site2site 10 match address TUNNEL

100.120.5.0/255.255.255.0/0/0 local proxy 10.0.16.0/255.255.255.0/0/0 on interface outside

 L2LACL

 access-list TUNNEL extended permit ip host 188.164.255.47 host 206.54.167.110
 access-list TUNNEL extended permit ip 100.120.5.0 255.255.255.0 10.0.16.0 255.255.255.0
 access-list TUNNEL extended permit ip 10.0.16.0 255.255.255.0 100.120.5.0 255.255.255.0

 10.1.16.0/24 - vpn client network


 webvpn
 enable outside
 svc image disk0:/anyconnect-win-2.5.2014-k9.pkg 1
 svc enable



 crypto key generate rsa label sslvpnkey
 crypto ca trustpoint localtrust
 enrollment self
 fqdn sslvpn.mycompany.com
 subject-name CN=sslvpn.mycompany.com
 keypair sslvpnkey
 crypto ca enroll localtrust noconfirm
 ssl trust-point localtrust outside

 ip local pool SSLClientPool 10.1.16.2-10.1.16.100 mask 255.255.255.0
 group-policy SSLCLient internal
 group-policy SSLCLient attributes
 vpn-tunnel-protocol svc
 default-domain value mysite.com
 address-pools value SSLClientPool
 sysopt connection permit-vpn


 tunnel-group SSLClient type remote-access
 tunnel-group SSLClient general-attributes
 default-group-policy SSLCLient
 tunnel-group SSLClient webvpn-attributes
 group-alias MY_RA enable
 webvpn
 tunnel-group-list enable



 ##Avoid default gateway
 access-list ROUTES standard permit 10.0.16.0 255.255.0.0
 access-list ROUTES standard permit 100.120.5.0 255.255.0.0

 group-policy SSLCLient attributes
  split-tunnel-policy tunnelspecified
   split-tunnel-network-list value ROUTES



   sh vpn-sessiondb l2l






   packet-tracer input outside tcp 78.140.151.7 59401 188.18864.255.47 80 detailed




важное%

$ ethtool --offload  eth0  rx off  tx off
$ ethtool -K eth0 gso off


mtu inside 1400
mtu outside 1400

### Important to push traffic between anyconnect and site2site interface (not really far way, but)
same-security-traffic permit inter-interface
same-security-traffic permit intra-interface




### Links
http://thejimmahknows.com/site-to-site-ipsec-vpn-using-openswan-and-cisco-asa-9-13/
https://doc.pfsense.org/index.php/IPsec_Troubleshooting
http://www.cisco.com/c/en/us/support/docs/security/asa-5500-x-series-next-generation-firewalls/118097-configure-asa-00.html
http://itsecworks.com/2013/09/18/cisco-asa-troubleshooting-commands/
http://www.firewall.cx/cisco-technical-knowledgebase/cisco-routers/904-cisco-router-anyconnect-webvpn.html
http://www.cisco.com/c/en/us/support/docs/security/asa-5500-x-series-next-generation-firewalls/113574-tg-asa-ipsec-ike-debugs-main-00.html
http://www.cisco.com/c/en/us/support/docs/security/asa-5500-x-series-next-generation-firewalls/81824-common-ipsec-trouble.html
http://xgu.ru/wiki/Cisco_ASA/Site-to-Site_VPN
http://xgu.ru/wiki/Cisco_ASA
Anyconnect
http://www.techrepublic.com/blog/data-center/eight-easy-steps-to-cisco-asa-remote-access-setup/
http://www.cisco.com/c/en/us/td/docs/security/asa/asa80/configuration/guide/conf_gd/cert_cfg.html#wp1042284
