---
layout: post
title: CoffeeScript
date: 2013-06-11 13:02:23
categories: update programming
---
I've always wanted to try CoffeeScript ever since I saw it on Railscast.  I
finally got my chance.  Luckily it comes built-in for Rails 3, but I didn't
know how it worked.  At first I thought I needed to compile and downloaded the
coffee compiler.  It turned out to be useful to have.  Rails does not give good
error messages if there is a problem in the coffee script, so I run it through
the compiler and it'll give me a better idea of what's going on.

**Installing CoffeeScript**.  CoffeeScript is a Node.js module.  Node.js is a
javascript interpreter you can use outside of the browser.  To install using
Homebrew use

<pre>
$ brew install node
$ sudo npm install -g coffee-script
</pre>

and put this in your `~/.bashrc` file

```bash
PATH="/usr/local/share/npm/bin/:$PATH"
```

You can use the `coffee` command to compile your coffeescript.

**Don't neeed guard**.  I installed `guard-coffeescript` but I found I didn't
need it.  You don't need to compile it because Rails will automatically do it
for you using the asset pipeline.

**The language**.  Coffeescript is somewhat like python in that indents matter.
`if` `then` does not need an end.  You don't need curly braces or semicolons.
Sometimes you don't need parentheses. Functions are defined using `->`.  So far
these are simple translations that make your code smaller.  You get power when
you find out about the `for` loop.  If you go to [the coffeescript
website](http://coffeescript.org), they have a really great overview of the
language with lots of examples.  You can even use the coffeescript interpreter
directly from the browser.  I found that useful when I'm developing some tricky
coffeescript.  You can immediately see any errors as you type then.

It's a bit frustrating when you make some modifications to your code and it
either just doesn't work or you get an incomprehensible error.  You end up
looking at the resulting javascript for clues.  The trouble is worth it because
some of the powers of the `for` loop and parameter handling (you can have
default args).

All in all, it's worth looking into.  Probably the best way to use it is by
converting an existing javascript code and cleaning it up.
