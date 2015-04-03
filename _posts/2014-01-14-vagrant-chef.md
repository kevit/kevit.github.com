---
layout: post
title: "Making a Vagrant test enviroment for chef development"
published: true
description: ""
category: 
tags: [chef, osx]
---


##Initial settings

```bash
rvm use 1.9.3@chef --create
sudo gem install bundler
sudo bundle install
```

## Using your hardware servers from vagrant

```bash
vagrant plugin install vagrant-managed-servers
vagrant box add dummy
https://github.com/tknerr/vagrant-managed-servers/raw/master/dummy.box
--provider=managed
```

## Install necessary plugins

```bash
vagrant plugin install vagrant-omnibus
vagrant plugin install vagrant-berkshelf --plugin-version '>= 2.0.1'
```


* [Git remote](http://stackoverflow.com/questions/1519006/git-how-to-create-remote-branch)
* [Example of workflow](http://stackoverflow.com/questions/22531452/chef-workflow-for-new-cookbooks)
* [Test Driven Development for Chef](http://leopard.in.ua/2013/12/01/chef-and-tdd/)





##Some Vagrant tricks

###Vagrant inline provision

```
  config.vm.provision :shell, :inline => "sudo aptitude -y install build-essential"
```

###Shared folders

```
config.vm.synced_folder cache_dir, '/var/cache/apt/archives/', id: 'v-cache', owner: 'vagrant', group: 'www-data'
```
