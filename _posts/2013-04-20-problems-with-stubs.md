---
layout: post
title: Problems with stubs
date: 2013-04-20 12:15:00
categories: update programming
---
Found a glaringly bad problem with my rspec.  Since the computer takes a long
time to think, I stubbed the move selection.  This was okay because I have
other tests to make sure that the move selection works properly.  The problem
happens after I refactor.  Some methods were moved around.  My rspec passed but
when I ran my program, it threw an 'undefined local variable or method'
exception.  My stubs allowed the rspec to pass.  This makes the optimization
even more important so can get rid of my stubs.
