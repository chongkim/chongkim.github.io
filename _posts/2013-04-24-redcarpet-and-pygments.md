---
layout: post
title: Redcarpet and Pygments
date: 2013-04-24 14:59:00
categories: programming
---
Decided on Redcarpet over RedCloth and BlueCloth.  Redcarpet has a lot more
flexibility in that it allows you to modify post processing of certain areas.
I was interested in fenced code blocks.  This is where you want to specify
blocks of code delimited by <code>```</code>.  I want to add syntax highlighting, which is
where pyments come in.

To set up Redcarpet.

1. `gem install redcarpet`
2. Edit apps/helpers/application_helper.rb

{% highlight ruby %}
module ApplicationHelper
  def markdown
    @markdown ||= Redcarpet::Markdown.new(Redcarpet::Render::HTML, :fenced_code_blocks => true)
  end
end
{% endhighlight %}

3. Use it in the view

{% highlight ruby %}
<%= raw(markdown.render(content)) %>
{% endhighlight %}

To set up pygments

1. `gem install pygments.rb`
2. Modify apps/helpers/application_helper.rb

{% highlight ruby %}
class HTMLwithPygments < Redcarpet::Render::HTML
  def block_code(code, language)
    Pygments.highlight(code, :lexer => language)
  end
end

module ApplicationHelper
  def markdown
    @markdown ||= Redcarpet::Markdown.new(HTMLwithPygments, fenced_code_blocks: true)
  end
end
{% endhighlight %}

I didn't have too much trouble getting this installed.  It was hard to detect
that this was working because it doesn't specify the css files so the processed
text didn't show colors.  I installed py33-pygments (`sudo port install
py33-pygments`) so I can run `pygmentize-3.3`.  Here's the command that
generated my css files:

{% highlight ruby %}
$ pygmentize-3.3 -S default -f html > style.css
{% endhighlight %}

To get a list of styles you can do:

{% highlight bash %}
$ pygmentize-3.3 -L styles
Pygments version 1.6, (c) 2006-2013 by Georg Brandl.

Styles:
`~~~~~~~
* autumn:
    A colorful style, inspired by the terminal highlighting style.
* monokai:
    This style mimics the Monokai color scheme.
* rrt:
    Minimalistic "rrt" theme, based on Zap and Emacs defaults.
...
{% endhighlight %}

My site is still not ready for prime time.  Need to look into bootstrap to add
good looking css.  Found out that Github uses pygments so it would be nice to
have my code look like Github's.
