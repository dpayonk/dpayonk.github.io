---
layout: page
title: "My notes with Java coming from .Net"
date: 2013-06-05 14:01
comments: true
sharing: true
footer: true
---
In the last 18 months or so, I've made the transition from .Net to Ruby.
For my more professional/enterprise projects, I've settled on JRuby, a flavor
of Ruby that runs on the JVM.  It offers access to the plethora of libraries
created over the years and the enterprise acceptance of the JVM.  Not to
mention, the speed rocks once you get over the startup of the JVM.

Here are the notes I've compiled over the last year about Java as it related
to my work in JRuby.

###System Level Access
It is not as easy to access and manipulate system objects using Java.

###Memory Settings
Memory settings can matter, especially with Ruby and Application servers.
Here are the ones I found to be most helpful for performance and memory consumption

+ -Xms1024m -Xmx1024m (Sets min and max memory to 1024 megabytes or 1GB)
+ -client -XX:+TieredCompilation -XX:TieredStopAtLevel=1
+ -Djruby.compile.mode=OFF
+ -Djava.awt.headless=true
+ -J-server -J-noverify -J-XX:+UseParallelOldGC
+ -J-XX:+TieredCompilation -J-XX:TieredStopAtLevel=1 -J-XX:CICompilerCount=3
+ -XX:CICompilerCount=31
+ -server -noverify
+ -XX:+UseParallelGC
+ -XX:PermSize=512m -XX:MaxPermSize=512m
+ -XX:+UseCompressedOops'

###Debugging Tools

####jvisualvm
Replaced jconsole and jps and installed add ins for garbage collection visualization.
Garbage collection visualization was awesome in helping me track down memory leaks
as I was profiling the application

###Deploying with JBoss
The JBoss application server that runs Java code is the basis for Torquebox,
maybe the most popular JRuby application server.


