---
layout: post
title: "How to validate your OpenSSL keys"
published: false
description: ""
category: 
tags: []
---

#HOW to check your ssl/openvpn keys
openssl x509 -noout -modulus -in kevit.crt | openssl md5
openssl rsa -noout -modulus -in server.key | openssl md5
openssl req -noout -modulus -in server.csr | openssl md5

all MD5 will be the same
