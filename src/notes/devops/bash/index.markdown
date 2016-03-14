---
layout: page
title: "My notes on Shell programming/administration"
date: 2013-06-05 14:34
comments: true
sharing: true
footer: true
---
Having moved from [.Net to Ruby](/dotnettoruby), I also moved from Windows to Unix/Mac OS X.
I had plenty of familiarity with Unix and Mac and felt comfortable on
the command line, but I also learned some important points along the
way to using it professionally.  I hope these help.

##Bash Startup
+ .bashrc is run on NON interactive sessions
+ .bash_profile is run on interactive sessions

##Linux
+ /etc/.bashrc is the all systems location on redhat
+ /etc/.bash_profile is on all systems for red hat and reads from /etc/profile.d/*

Permissions
+ You need the execute permission (x) on directories to cd into them

##SSH Helpfuls
+ Remote to local -> ssh -i key.pem  root@remote:/full/path/directory /local/dir/file.txt
+ Local to Remote -> ssh -i key.pem file.txt root@remote:/full/path/directory
+ Machine To Machine -> scp -i key.pem  user@rh1.edu:/remote/directory/foobar.txt your_username@rh2.edu:/another/remote/directory/

##System Monitoring
+ Kill a process no matter what -> kill -9 3486
+ Disk Usage -> du -hs /opt/apps/xsell_dashboard

+ Kill all commands matching grep
```
ps -ef | grep postgresql | grep -v grep | awk '{print $2}' | xargs kill -9
```

##System Start up
Init
+ chkconfig --add service_name

##User Admin

###Create new user
1. useradd -g primary_group_name dpayonk
2. passwd username

##Others
+ openssl passwd -1 "plaintext"
+ cat ~/.ssh/id_rsa.pub | ssh username@server.com 'cat >> .ssh/authorized_keys'

##Tools
+ rpm -Uvh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
+ wget http://prdownloads.sourceforge.net/webadmin/webmin-1.620-1.noarch.rpm
