---
layout: post
title: On To Clojure Tic-Tac-Toe
date: 2013-05-16 18:57:20
categories: programming
---
I've started writing my Clojure version of Tic-Tac-Toe.  I was trying to get
fireplace.vim working but it'll have to wait.  I started writing simple tests
and I'm working on a good way to modify state.  I could use `ref` but then I
have to wrap a bunch of code in `dosync`.  I might use `atom` and `swap!`.
Once I figure this out, the rest of the code should write itself.

My second priority is to read through all of `user_*.txt` docs from vim.
Eventually learning vimscript so I can see what the plugins are doing so I
don't have to google around for hours.
