---
layout: post
title: "Making a Vagrant test enviroment for chef development"
description: ""
category: 
tags: []
---

rvm use 1.9.2@chef --create
sudo gem install bundler
sudo bundle install

vagrant plugin install vagrant-managed-servers
vagrant box add dummy
https://github.com/tknerr/vagrant-managed-servers/raw/master/dummy.box
--provider=managed

vagrant plugin install vagrant-omnibus
vagrant plugin install vagrant-berkshelf --plugin-version '>= 2.0.1'

kitchen init
(knife solo init .)???

http://stackoverflow.com/questions/1519006/git-how-to-create-remote-branch

http://stackoverflow.com/questions/22531452/chef-workflow-for-new-cookbooks
http://leopard.in.ua/2013/01/04/chef-solo-getting-started-part-1/
http://leopard.in.ua/2013/02/17/chef-server-getting-started-part-1/
http://leopard.in.ua/2013/12/01/chef-and-tdd/





##Vagrant tricks
#vagrant inline provision
# install some base packages
  config.vm.provision :shell, :inline => "sudo aptitude -y install
build-essential"

#Shared folders
The apt cache solution is working with a share folder between my laptop,
and it’s also affected by a dsl change in vagrant :
1
config.vm.share_folder "v-cache", "/var/cache/apt/archives/", cache_dir 
is now called synced folder :
1
config.vm.synced_folder cache_dir, '/var/cache/apt/archives/', id:
'v-cache', owner: 'vagrant', group: 'www-data'
