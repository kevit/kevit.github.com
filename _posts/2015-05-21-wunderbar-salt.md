---
layout: post
title: "Wunderbar Salt"
description: "Short No U introduction into Salt"
category: 
published: true
tags: [salt, devops]
---

##Inroduction

There is a my first steps in Salt. I would like to use this framework next few years. Let's start!
For any operations by ssh yours ssh key should be loaded into ssh-agent


##Saltfile

```bash
salt-ssh:
 config_dir: etc
 max_prox: 30
 wipe_ssh: true
```

##etc/master content

```bash
file_roots:
 base:
  - salt/
  - formulas/owncloud-formula
  - formulas/openvpn-formula

root_dir: ./

pillar_roots:
 base:
  - pillar/
```

##etc/roster content

```bash
saltmaster:
 host: 192.0.2.1
 user: user
 sudo: True
```

##Debug
* salt-ssh could not be run because it could not generate keys
You should check your master content, especially root_dir

* How to debug using your pillar or not?

```bash
salt-ssh '*' pillar.items
salt-ssh '*' pillar.get owncloud
```

Moreover, you can refresh pillar or append pillars from cli

```bash
salt-ssh '*' saltutil.refresh_pillar
salt-ssh '*' state.highstate pillar='{"owncloud": {"owncloudpass": "password"}}'
```

* Check your salt version (useful for asking help)

```bash
salt --versions-report
```
