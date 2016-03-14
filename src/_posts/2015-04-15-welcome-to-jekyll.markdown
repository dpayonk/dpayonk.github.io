---
layout: post
title:  "Welcome to Jekyll!"
date:   2015-04-15 15:29:59
categories: jekyll 
image: "/assets/bannerLogo.png"
---

I decided to spend some time spring cleaning my different web properties.  It
turns out that Octopress is in a state of flux between 2.0 being in the graveyard
and 3.0 being incomplete, that I decided to move this blog to Jekyll.

I had to do three things to complete my transition.

1) Copy over the entries.  I could have used an importer, but copying directories
worked just fine.

2) Create plugins for the missing features which included discus, google analytics, and deployment

So far, the process went smoothly.  I'm very happy with my continued use of
a static site generator for my blog content and it made the migration process very easy.



Here's to hoping a new blog and a new year bring about a renewed spirit of writing.

{% highlight ruby %}
def welcome(name)
  puts "Hi #{name}, my name is Dennis.  Welcome to my new blog."
end
welcome('You')
#=> prints 'Hi You, my name is Dennis.  Welcome to my new blog.'
{% endhighlight %}
