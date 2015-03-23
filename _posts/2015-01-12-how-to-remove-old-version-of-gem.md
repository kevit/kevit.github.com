---
layout: post
title: "How to remove old version of gem"
published: false
description: ""
category: 
tags: [ruby, osx, chefdk]
---

###Problem

```bash
meez --cookbook-path localdev --copyright kevit -I apachev2 -m simarg@gmail.com localdev
/opt/chefdk/embedded/lib/ruby/site_ruby/2.1.0/rubygems/specification.rb:2087:in `check_version_conflict': can't activate json-1.7.7, already activated json-1.8.1 (Gem::LoadError)
```

```bash
gem list | grep json
json (1.8.1, 1.7.7)
```

```bash
gem cleanup json
Cleaning up installed gems...
Clean Up Complete
```

```bash
gem list | grep json
json (1.8.1, 1.7.7)
```

```bash
gem uninstall json --version '<1.8.1'
ERROR:  While executing gem ... (Gem::InstallError)
    json is not installed in GEM_HOME, try:
    gem uninstall -i /opt/chefdk/chefdkembedded/lib/ruby/gems/2.1.0 json
```

```bash
sudo gem uninstall -i /opt/chefdk/embedded/lib/ruby/gems/2.1.0 json --version '<1.8.1'
Password:

You have requested to uninstall the gem:
json-1.7.7

chef-11.6.2 depends on json (<= 1.7.7, >= 1.4.4)
hitimes-11.2.2 depends on json (~> 1.7.7, development)
hitimes-1.2.1 depends on json (~> 1.7.7, development)
If you remove this gem, these dependencies will not be met.
Continue with Uninstall? [yN]  y
Successfully uninstalled json-1.7.7
```
