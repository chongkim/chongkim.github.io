---
layout: post
title: Blog 
date: 2013-05-18 00:29:19
categories: update programming
---
I pushed out two changes to my blog site.  It now handles exceptions if you
have a bad fenced block code.  For example if I tag a snippet of code to be
````lisp`, it will break since it doesn't know about lisp.  Previously, the
site would just show an ugly error page.  Now it will put "block cannot be
interpreted" as the text inside the fenced block code.

The second change was I added pagination.  The problem was that I had too many
entries and it took a long time before I get a response if I hit the first time
in the morning.  I limited the entries to 5 per page.  Now things are as zippy
as before.
