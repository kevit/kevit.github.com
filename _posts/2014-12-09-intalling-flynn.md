---
layout: post
title: "Installing Flynn"
description: ""
category: 
tags: [docker , heroku , flynn , hosting]
---

##Preparations

```bash
modprobe aufs
```

## Flynn installation

```bash
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv BC79739C507A9B53BB1B0E7D820A5489998D827B
echo deb https://dl.flynn.io/ubuntu flynn main | sudo tee /etc/apt/sources.list.d/flynn.list
apt-get update
apt-get install flynn-host
```

## Flynn running

```bash
flynn-host download /etc/flynn/version.json
```

Getting a new token https://discovery.etcd.io/new

env ETCD_DISCOVERY=https://discovery.etcd.io/25de9fc57a803d514489b26651de0cf8
start flynn-host
status start flynn-host
CLUSTER_DOMAIN=demo.188.42.225.11.xip.io flynn-host bootstrap /etc/flynn/bootstrap-manifest.json


## Flynn using
flynn cluster add -g demo.188.42.225.11.xip.io:2222 -p KcJ62BmkUluWC/THC8s6gVQhaWLPry/fN9edRMuzDhA= default https://controller.demo.188.42.225.11.xip.io 83d5502e1ca7c51dd94955bc0136fbcb
$ ssh-keygen -t dsa
$ flynn key add
$ sudo apt-get install git
$ git clone https://github.com/flynn/nodejs-flynn-example.git
$ cd nodejs-flynn-example;  flynn create example
$ git push flynn master


## Flynn debug



https://flynn.io/docs/using-flynn
