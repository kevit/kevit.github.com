---
title: "OSX and VeeWee"
date: Thu Nov 14 14:50:38 +0800 2013
layout: post
published: true
tags: osx vagrant rvm veewee
---

## Preparation

## RVM part
I use a $http://www.stewgleadow.com/blog/2011/12/10/installing-rvm-on-os-x-lion/ instruction to run RVM

bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
rvm install 1.9.2


## Veewee part
cd Projects
git clone https://github.com/jedi4ever/veewee.git; cd veewee
zsh --login
rvm use 1.9.2@veewee --create 
bundle install
bundle exec veewee

## Usage

bundle exec veewee vbox templates | grep -i ubuntu
bundle exec veewee vbox define 'mybuntubox' 'ubuntu-12.10-server-amd64'
bundle exec veewee vbox build 'mybuntubox'

## Doing a export to vagrant box
bundle exec veewee vbox export 'myubuntubox'

## Doing a import to vagrant
vagrant box add 'myubuntubox' 'myubuntubox.box'

#running a new enviroment
vagrant init 'myubuntubox'
vagrant up
vagrant ssh

## Interesting source
https://github.com/timsutton/osx-vm-templates

