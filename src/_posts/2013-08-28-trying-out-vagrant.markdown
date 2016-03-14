---
layout: post
title: "Trying out Vagrant"
date: 2013-08-28 16:57
comments: true
categories: ["devops","sys admin"]
published: true
---

We've been starting to use Vagrant to document and provision our environments
for a few weeks now and I thought it's time to share some of the learnings
we've made over that time period.

### Vagrant versions are different
Vagrant 1.X versions differ significantly enough for what we were doing.  It
starts off as simple difference in semantics.

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

But it ends up changing significantly enough that I had to rewrite
most of my provisioning code by the time we got to trying it with AWS
(which was the whole driver in the first place).  Make sure to go
through the effort of installing it instead of using "gem install vagrant"

### Vagrant and the Cloud
Like I mentioned before, the key feature for starting to look at Vagrant was
the integration of the cloud providers so that I can provision machines in the cloud
instead of just in my Virtualbox world.  This sounded swell, but caused
some angst while trying to understand what goes on behind the scenes.

Turns out, to log in and configure chef, Vagrant AWS uses rsync.  Well, for
most of the Linux instances we used, that just wasn't working because
of the security of our boxes.  To fix this, we had to actually go through
some of the pull requests for Vagrant and understand a little more about
AWS provisioning.  The first was that sudo wouldn't work how we hoped it would.
I tried a little script before chef started running to "sed" it out, but
that wasn't full proof.  A colleague of mine then pointed out a [pull request](https://github.com/mitchellh/vagrant-aws/pull/26)
that helped.  Turns out the Amazon User Data that I never had used in the past
could be used to create a little start up script.  Wish there would have been
a tooltip there.  I'm always disappointed by the AWS interface and that's
just one of many failings I'm used to.  No worries Amazon, keep on spending
your efforts on the actual infrastructure, I'll figure the rest out.

That's it for now, but you might want to check out my [Vagrant](/devops/vagrant) notes
later if you're nodding your head as you're reading this.