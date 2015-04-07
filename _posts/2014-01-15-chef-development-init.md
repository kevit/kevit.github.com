---
layout: post
title: "How to start new chef project in OSX"
published: true
description: "Using meez to Chef development"
category: 
tags: [chef, osx]
---


##Initial Ruby preparation

```bash
rvm use 1.9.3@cloud --create
gem update --system
```


I use [meez](https://github.com/paulczar/meez) for initial cookbook infrastructure



## Serverspecs asserts examples

```ruby
it 'adds the Opscode package signing key' do
    opscode_key = shell_out("apt-key list")
    assert opscode_key.stdout.include?("Opscode Packages
<packages@opscode.com>")
  end

it 'creates the correct pinning preferences for chef' do
    chef_policy = shell_out("apt-cache policy chef")
    assert chef_policy.stdout.include?("Package pin: 10.16.2-1")
  end
```
