---
layout: page
title: "sidekiq"
date: 2013-09-06 20:59
comments: true
sharing: true
footer: true
---

##Whoops

When we initially started load testing the Sidekiq stuff, I didn't realize
that the 25 scheduled workers (default) would take up all my 
database connections and not pool them.  In case you have some unintended
database connection problems, just make sure to take a look.


