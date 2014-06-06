---
title: Ansible in MacosX
published: true
date: Fri Jul 29 17:32:40 +0800 2013
layout: post
categories: ansible osx
---

##Preparation
Ansible is a quite powerful tool for bootstrapping.

	#!sh
	#prepare a dependencies
	sudo easy_install jinja2
	sudo easy_install PyYAML
	sudo easy_install paramiko
	#doing a checkout
	git clone git://github.com/ansible/ansible.git
	cd ./ansible
	#setting a env
	source ./hacking/env-setup
	cd ~
	touch .ansible_hosts
	#exporting a needed envs
	export ANSIBLE_HOSTS=~/.ansible_hosts
	export ANSIBLE_TRANSPORT=ssh
	echo echo “192.168.0.62”
	echo “example.org” > ~/ansible_hosts
	ansible all -m ping

##Or if you needed a Ubuntu
Just use a package from	https://launchpad.net/~rquillo/+archive/ansible

##Debug

	#!sh
	line 65, in <module>\r\n    import simplejson as json\r\nImportError: No module named simplejson

Just check a https://github.com/ansible/ansible/issues/1245#issuecomment-9202113

##Oneliners

How to define your host file ( in case you have multiple host files otherwise use the ANSIBLE_HOSTS environment variable).

	#!sh
	ansible-playbook -i hosts infrastructure.yml

How to run only certain tags for all playbooks

	#!sh
	ansible-playbook -i hosts infractructure.yml --tags backup

How to run a specific playbook

	#!sh
	ansible-playbook -i hosts webservers.yml

How to run a specific group

	#!sh
	ansible-playbook -i hosts infrastructure.yml --limit webservers

How limit the number of hosts for group ( first 10 )

	#!sh
	ansible-playbook -i hosts infrastructure.yml --limit webservers[0-10]



## Ansible Redhat trouble
 ansible monitoring -i 8to_servers.ansible -m ping
monitoring | FAILED >> {
    "failed": true,
    "msg": "Error: ansible requires a json module, none found!",
    "parsed": false
}

Ansible requires python-simplejson being installed on EL boxes < 6. This
is how modules can pass information back and forth (roughly).

You can bootstrap all your EL 5 boxes with this command:

ansible rhe5box.com -i my-serverlist -u root -m raw -a "yum install -y python-simplejson"

## Ansible playbooks
http://www.it-hure.de/2013/07/thank-you-seth-vidal-my-first-ansible-playbook/
https://github.com/pjan/the-ansibles
https://github.com/francisbesset/ansible-playbooks
http://habrahabr.ru/company/selectel/blog/196620/
https://github.com/ansible/ansible/tree/devel/plugins/inventory
https://github.com/ansible/ansible-examples
https://github.com/al3x/sovereign/blob/master/README.textile personal
cloud
http://habrahabr.ru/post/195048/

## bacula Ansible
https://twitter.com/brodul/status/375010718753378304

https://groups.google.com/forum/#!msg/ansible-project/vgc2bFQgzmE/0SDKwCniPjgJ
http://www.ansibleworks.com/docs/playbooks_roles.html#id7
