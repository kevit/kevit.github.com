---
layout: post
title: "How to install KVS in Ubuntu 14.04"
published: false
description: ""
category:
tags: [php, ubuntu]
---

```bash
add-apt-repository ppa:jon-severinsson/ffmpeg
apt-get update
apt-get install ffmpeg libavcodec-extra-54

add-apt-repository ppa:kedazo/ioncube-loader 
apt-get update
apt-get install php5 
apt-get install ioncube-loader php5-mysql  php5-gd mysql-server
php5-curl php5-cli php-xml-parser php5-imagick php5-memcache
a2enmod rewrite;  php5enmod ioncube-loader; service apache2 restart
```

```bash
 [ionCube Loader] The Loader must appear as the first entry in the
change /etc/php/apache2/php.ini according requirements (first line will
be a zend_extension=/usr/lib/ioncube/ioncube_loader_lin_5.5.so
```


```bash
Failed loading /usr/lib/ioncube/ioncube_loader_lin_5.5.so:
/usr/lib/ioncube/ioncube_loader_lin_5.5.so: cannot open shared object
file: No such file or directory
```

you should download ioncube_loaders_lin_x86-64.tar.gz and untar to /usr/lib/ioncube


