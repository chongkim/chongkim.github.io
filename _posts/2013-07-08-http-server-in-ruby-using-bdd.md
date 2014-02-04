---
layout: post
title: HTTP Server In Ruby Using BDD
date: 2013-07-08 18:31:52
categories: update programming
---
I wrote a rudimentary HTTP server and practiced writing it for the past few
days.  I used Screenflow to record and replayed it in fast motion so I can see
what I was doing.  Going through it several times, you make a lot of mistakes
and see pretty much every variation of errors you would encounter for that
project.  I learned a lot and kept my code to the bare minimum.  You can see
the code on [github](https://github.com/chongkim/httpd-ruby-bdd)

It uses Cucumber to set up the expected behavior.  Then I jump into RSpec to
start implementing the guts.  When all the RSpec tests pass, I check on
Cucumber again to see if I was able to accomplish my goal.  The server only
handles one request, but you can keep modifying it to make it more robust and
add more features.

<iframe width="560" height="315" src="//www.youtube.com/embed/OsrV5MOBkUI?rel=0" frameborder="0" allowfullscreen></iframe>
