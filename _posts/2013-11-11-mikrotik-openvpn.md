---
title: "Mikrotik OpenVPN"
date: Mon Nov 11 13:50:53 +0800 2013
layout: post
published: true
tags: mikrotik openvpn network 
---


/ip pool add name=openvpn-pool ranges=172.28.1.10-172.28.1.20
/interface bridge add name=vpn-bridge

/ppp profile add change-tcp-mss=default comment="" bridge=vpn-bridge
local-address=172.28.1.1 name="openvpn-profile" only-one=default
remote-address=openvpn-pool use-compression=default
use-encryption=required use-vj-compression=default 
/ppp secret add caller-id="" comment="" disabled=no limit-bytes-in=0
limit-bytes-out=0 name="kevit" password="kevit" routes="" service=any
profile="openvpn-profile"
/ppp secret add caller-id="" comment="" disabled=no limit-bytes-in=0
limit-bytes-out=0 name="andy" password="yPKBzFQnYhTf5" routes=""
service=any profile="openvpn-profile"
/certificate import file=openvpn-server.crt
/certificate import file-name=openvpn-server.key
/interface ovpn-server server set auth=sha1,md5 certificate=cert1
cipher=blowfish128,aes128,aes192,aes256 default-profile=openvpn-profile
enabled=yes keepalive-timeout=disabled max-mtu=1500 mode=ethernet
netmask=24 port=1194 require-client-certificate=no
/interface ovpn-server add name=ovpn-server user=kevit
/ip firewall filter add action=accept chain=input comment="OpenVPN"
disabled=no dst-port=1194 protocol=tcp
/interface bridge port add interface=VLAN100 bridge=vpn-bridge

