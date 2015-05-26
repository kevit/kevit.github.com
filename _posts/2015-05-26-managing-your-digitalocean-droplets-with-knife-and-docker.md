---
layout: post
title: "Managing your DigitalOcean droplets with Knife and Docker"
description: "How to manage your cloud using Docker"
category: 
published: true
tags: [docker, knife, chef]
---

## Preparation in OSx

```bash
brew install boot2docker
boot2docker init
boot2docker up
```

## Prepare your Dockerfile

There is a quite forward

```
FROM ubuntu:15.04
MAINTAINER kevit
RUN apt-get update && apt-get install -y \
    wget
RUN wget https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.6.0-1_amd64.deb
RUN dpkg -i chefdk_0.6.0-1_amd64.deb
ENV PATH="/opt/chefdk/bin:/root/.chefdk/gem/ruby/2.1.0/bin:/opt/chefdk/embedded/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
ENV GEM_ROOT="/opt/chefdk/embedded/lib/ruby/gems/2.1.0"
ENV GEM_HOME="/root/.chefdk/gem/ruby/2.1.0"
ENV GEM_PATH="/root/.chefdk/gem/ruby/2.1.0:/opt/chefdk/embedded/lib/ruby/gems/2.1.0"
RUN gem install knife-digital_ocean
ENTRYPOINT ["knife"]
```

##Building image and running knife

```bash
docker build -t digital-ocean .
docker run -t -v ~/.chef/knife.rb:/root/.chef/knife.rb:ro -i digital-ocean digital_ocean -VV account info
```

All parameters for knife you can find in documentation for the knife module


## Debug:

error in run: Failed to initialize machine "boot2docker-vm": exit status 1

```bash
rm -rfi ~/VirtualBox\ VMs/boot2docker-vm/
```

docker ps
FATA[0000] Error response from daemon: client and server don't have same version (client : 1.17, server: 1.16)

```bash
boot2docker upgrade
```


You can clone my [git](https://github.com/kevit/knife-digital_ocean) repo with Dockerfile and updated readme

## Links
* [boot2docker debug](http://stackoverflow.com/questions/26572112/running-boot2docker-error-in-run-failed-to-get-machine-boot2docker-vm-mac)
* [ways to copy files into docker container](http://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container)
