---
layout: post
title: ".Net to Ruby (and Nix)"
date: 2012-06-30 22:43
comments: true
categories:
published: true
---

It's official.  I've migrated out of the .Net space and into the wonderful
world of *Nix based development.  It's been a pleasure, a struggle, and thousands
of googles later, I'm finally writing an article about it.  I've been meaning
to write this article for over a year, but I never quite knew when I would feel
comfortable that I knew enough to comment.  So before, I forget all of the good
things about .Net development...

## Software (Mac vs Windows and etc)
Sans an OS discussion, the most important aspect of moving is getting used to and
understanding software installation.  It's fair to say that installing software
in the Mac feels and is different.  First, the /Applications directory and its
associated /Applications/App.app 's are just directories like C:\Program Files\
and its contents can be traversed inside a bash shell.  It's not really necessary
in everyday life, but it helpful to know there is an equivalent.

Startup programs and scheduled tasks are done in a more configuration oriented way.
I think Windows has done this better save for headless execution.  Scheduled Tasks
can be accomplished via cron which is *totally* not as good as windows task scheduler.
Unix certainly has a more fleixble syntax and if I were continuously scheduling tasks,
I would think differently about the *features*, but that's not a task I do that often.
For any task I don't do that often, I tend to prefer straightforward option provided
by a GUI (usually via an IDE).  That goes for startup programs as well.

Separating Mac and Linux might be good for startup programs, but both are not that great.
In Nix, startup programs can be configured using tools like upstart and loading them via
scripts in /etc/init.d folder.  In the Mac, an XML configuration file called .plist is used.
This configuration is difficult to read and you really don't need it all that often.
I tend to Google as needed.

As a developer, there are always several additional tools not needed to ordinary users.  I'll use
a separate post to recommend them, but at this point Homebrew and MacPorts are
standard options, and almost everyone moves to homebrew eventually.

## (Integrated) Development Environment

The single most missed software for me is the SQL Management Studio IDE.  I've replaced
Visual Studio with JetBrains and Rubymine, and while not as feature rich, it offers
the only important feature (intellisense).  I view the lack of features as a feature other
than that.

But SQL Management Studio is the Tesla of Database management applications.
I've settled on the Postgres DBMS solution and while there are certainly better
tools for MySQL, none of them compare to SQL Management Studio.  So, get ready to feel
like it's Sql Management Studio 2000 once you make the switch.

What Nix development lacks in IDE, it makes up for with collections
of command line tools that can be automatically scripted to create very
productive workflows.  While the BASH language looks atrocious, I'd still
recommend someone take the time to write a few tools in it because it can
be so powerful down the road.  BASH tools are the modern day equivalent
of "There's an app for that."