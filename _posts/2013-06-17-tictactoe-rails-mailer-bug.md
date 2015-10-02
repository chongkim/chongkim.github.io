---
layout: post
title: TicTacToe Rails Mailer Bug
date: 2013-06-17 22:07:06
categories: programming
---
I had a bug in my TTT Rails app.  When I try to send out email, I get

<pre>
NameError: ActionMailer is not missing constant Base!
  load_missing_constant at /Users/ckim/.rvm/gems/jruby-1.7.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:494
          const_missing at /Users/ckim/.rvm/gems/jruby-1.7.1/gems/activesupport-3.2.13/lib/active_support/dependencies.rb:192
.
.
.
</pre>

It turns out that at one point I created a mailer called `mail`.

{% highlight bash %}
# don't do this

$ rails g mailer mail
{% endhighlight %}

Once I deleted that file (`app/mailers/mail.rb`), my email starting working
again.
