---
layout: post
title: Poltergeist For Rails Javascript testing
date: 2013-05-27 01:18:28
categories: programming
---
Since `capybara-webkit` is broken for JRuby. I installed the `poltergeist` gem.
It uses PhantomJS so I needed to install that too.

{% highlight bash %}
$ brew install phantomjs
{% endhighlight %}

I modified my `features/support/env.rb` file by adding the following at the end.

{% highlight ruby %}
require 'capybara/poltergeist'
Capybara.javascript_driver = :poltergeist
{% endhighlight %}

WooHoo!  It works.  Now I can work on the Tic Tac Toe program again.

