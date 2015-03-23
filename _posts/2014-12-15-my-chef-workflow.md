---
layout: post
title: "My chef workflow"
published: false
description: ""
category: 
tags: []
---

## How i working with Chef

chef gem install meez

meez --cookbook-path localdev --copyright kevit -I apachev2 -m simarg@gmail.com localdev


* Initializing Cookbook
** Creating cookbook imagebuilder
** Creating README for cookbook: imagebuilder
** Creating CHANGELOG for cookbook: imagebuilder
** Creating metadata for cookbook: imagebuilder
Rewriting metadata.rb
Rewriting recipes/default.rb
* Initializing Berkshelf
create  imagebuilder/imagebuilder/Berksfile
create  imagebuilder/imagebuilder/Thorfile
create  imagebuilder/imagebuilder/chefignore
create  imagebuilder/imagebuilder/.gitignore
create  imagebuilder/imagebuilder/Gemfile
* Initializing Vagrantfile
Creating imagebuilder/imagebuilderimagebuilder/Vagrantfile from template
* Initializing Knife
adding chef gem to Gemfile
* Initializing Rakefile
Creating imagebuilder/imagebuilder/Rakefilee from template
adding rake gem to Gemfile
* Initializing Rubocop
Creatingting imagebuilder/imagebuilder/.rubocop.yml from template
adding rubocop gem to Gemfile
* Initializing Food Critic
adding foodcritic gem to Gemfile
* Initializing Chef Spec
Creating imagebuilder/imagebuildergebuilder/test/unit/spec/spec_helper.rb from template
Creating imagebuildergebuilderilder/imagebuilder/test/unit/spec/default_spec.rb from template
adding chefspec gem to Gemfile
* Initializing Server Spec
Creating imagebuilder/imagebuilderilder/test/integration/default/serverspec/spec_helper.rb from template
Creating imagebuilder/imagebuilder/test/integration/default/serverspec/default_spec.default_specrb from template
* Initializing Test Kitchen
create  .kitchen.yml
append  Rakefile
append  Thorfile
exist  test/integration/default
append  .gitignore
append  .gitignore
append  Gemfile
append  Gemfile
You must run `bundle install' to fetch any new gems.
Creating imagebuilder/imagebuilder/.kitchenen.yml from template
* Initializing Guard
Creating imagebuilder/imagebuilderuilder/Guardfile from template
adding guard gem to Gemfile
adding guard-rubocop gem to Gemfile
adding guard-foodcritic gem to Gemfile
* Initializing Drone
Creating imagebuilder/imagebuilder/.drone.yml from template
* Initializing Docker
Creating imagebuilder/imagebuilder/Dockerfile fromm template
Cookbook imagebuilder created successfully
Next steps...
$ cd imagebuilder/imagebuilder
$ export USE_SYSTEM_GECODE=1
$ chef exec rake prepare
$ chef exec rake test
