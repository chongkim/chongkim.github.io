---
layout: post
title: Vim Ctags Gem Trick
date: 2015-02-05 15:59:53
categories: programming
---
In vim, you can use &#8963;] to go to the function definition if
you've set up ctags, but I've had a problem with gems because they
weren't located in the same project directory.

One way to get this working is by setting your path so it knows where is your gem.


File: .vimrc

{% highlight vim %}
set path+=/Users/ckim/.rvm/gems/ruby-2.1.5/gems/nokogiri-1.6.6.2/lib/
{% endhighlight %}

But this means you'd have to do it for every gem and that's a lot of maintaining.

Chris Lamb showed me a simpler solution: just include your gems in
your project directory and run the ctags as you'd normally do.

{% highlight bash %}
$ bundle install --path .bundle
$ ctags -R .
{% endhighlight %}
Now I'm able to jump into the gem's source code as easily as the
rest of my code in my project.

