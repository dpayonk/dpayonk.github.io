---
layout: page
title: "My Vagrant Notes"
date: 2013-08-28 16:50
comments: true
sharing: true
footer: true
---
##Versions
Vagrant 1.X versions differ significantly enough for what we were doing.  It
starts off as simple difference in semantics, but the functions end up
changing enough to make sure to go through the effort of installing it
instead of using "gem install vagrant"

```
   Vagrant.configure('2') do |env|
   ...
   end
```
vs
```
   Vagrant::Config.run do |config|
    ...
   end
```

+ When using Vagrant with AWS and CentOS/Redhat, make sure to put this line in your script
to enable requiretty in sudoers (do stuff without a terminal session)
```
aws.user_data = "#!/bin/sh\nsed -i -e '/requiretty/ d' /etc/sudoers\n"
```