---
layout: post
title: Tic Tac Toe Rails In JRuby
date: 2013-06-25 16:54:00
categories: programming
---
I've been working on my JRuby implementation of the Tic Tac Toe Rails program
with a Clojure back-end.  It's been taking me a lot longer than I expected and
it's partially due to using JRuby.  The problem with JRuby is that a lot of
gems don't work.  Sometimes it installs but it's only after using it that you
notice some features seem to be broken (Spork with Cucumber/RSpec, Email with
Devise) or it just doesn't install at all.  On top of that, the startup time is
a bit slower since it has to start the JVM.  It makes developing on it very
painful.

The other reason why it was taking longer was because I thought the hard part
was the Clojure back-end that runs the TTT engine.  That turned out to be the
easy part.  The interface gave me some challenges.  I used CoffeeScript.  The
language is pretty simple.  I ran into silly little errors such as

{% highlight js %}
setTimeout(myfunc, 500)  // runs fine

setTimeout(-> myfunc, 500)  // does not work
setTimeout(-> myfunc(), 500)  // this is what it should be

// this is what it would look like in javascript
setTimeout(function() {
    myfunc();
}, 500)
{% endhighlight %}

Since the first two lines look very similar so my eye didn't catch it until
much later.

I have CSS and HTML issues (I still don't know why my page is more than a
screenful when everything fits on the page).  It didn't start off that way.  It
looked perfect when I made the TTT game but when I added more pages to it so I
can add a login screen and a game request, things shifted around a bit and now
it needs to be revisited.  I need to finish up the rest of the features so
that'll have to wait.

I'm almost done with this project.  I have email requests being sent out.  I
need to re-use my TTT interface so it can play a move and email back to the
opponent.  I have thought about re-implementing this in MRI Ruby and forking
off a process to run the clojure back-end but it's too late.  I'm 90% of the
way there and I just want to finish this off as soon as possible.
