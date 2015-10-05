---
layout: post
title: Fireplace and Vim 
date: 2013-05-18 00:35:58
categories: programming
---
I finally figured out what was wrong with my fireplace setup.  Fireplace is a
vim plugin that allows you to interact with the Clojure REPL.  My problem was
that I need to put a namespace at the top, so if had a file foo.clj, I need to
put `(ns tic-tac-toe.foo)` (tic-tac-toe is the app I'm working on).  Everything
is working as advertised.

Now I just need to figure out how I want to have my setup so I can be most
efficient.
