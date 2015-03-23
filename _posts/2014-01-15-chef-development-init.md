---
layout: post
title: "How to start new chef project"
published: false
description: ""
category: 
tags: []
---



rvm use 1.9.3@cloud --create
gem update --system

vagrant init

#ls
Berksfile Gemfile

gem install bundler
bundle install

git init chef-gemserver
knife cookbook create chef-gemserver -o .
cd chef-gemserver
berks install
kitchen init

serverspec-init

## Serverspecs asserts examples

it 'adds the Opscode package signing key' do
    opscode_key = shell_out("apt-key list")
    assert opscode_key.stdout.include?("Opscode Packages
<packages@opscode.com>")
  end

it 'creates the correct pinning preferences for chef' do
    chef_policy = shell_out("apt-cache policy chef")
    assert chef_policy.stdout.include?("Package pin: 10.16.2-1")
  end
