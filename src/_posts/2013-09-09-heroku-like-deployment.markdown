---
layout: post
title: "Heroku like deployment"
date: 2013-09-09 18:10
comments: true
categories: 
---

[How I found out Bundler knew where my gems were](http://stackoverflow.com/questions/9771172/rbenv-surviving-without-gemsets)
```
~/.bundle/config is an internal implementation detail of Bundler. We use it to remember flags passed to install, like --path vendor/bundle. You shouldn't edit it yourself because unsupported things could happen if you do that. :) The triple dash is because it's stored as a YAML file. I specifically suggested --skip-bundle so that the failing autorun of bundle install would be skipped. I believe it fails because of how these commands bootstrap the rails gem. – indirect Mar 21 '12 at 17:00
```
