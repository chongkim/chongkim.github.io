---
layout: post
title: Ruby Java Clojure Integration
date: 2013-05-22 21:55:11
categories: programming
---
I have Ruby, Java and Clojure set up in my rails app.  I'm using JRuby and I'm
able to load the jar file created from Clojure.  Here's what I did.

{% highlight bash %}
$ rvm install jruby
$ rvm use jruby
$ brew install clojure
$ brew install leiningen
$ lein new default ttt  # this will also create function foo in ttt/core.clj
$ lein uberjar   # this will create a standalone jar file in directory "target"
{% endhighlight %}

Then you edit the `Gemfile` to include

{% highlight ruby %}
gem "jrclj"
{% endhighlight %}

Create a file `a.rb` with the following sample code

{% highlight ruby %}
#!/usr/bin/env ruby

require 'java'

Dir["#{File.dirname(__FILE__)}/ttt/target/*.jar"].each do |jar|
  require jar
end

require 'jrclj'

clj = JRClj.new "ttt.core"
clj.foo "chong"
{% endhighlight %}

Execute the code and you should see

{% highlight bash %}
chong Hello, World!
{% endhighlight %}

I have everything I need to create the Rails Tic Tac Toe.
