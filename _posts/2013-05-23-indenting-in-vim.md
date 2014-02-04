---
layout: post
title: Indenting in Vim
date: 2013-05-23 21:37:04
categories: programming
---
Just discovered that `=` in vim's normal mode is to indent properly.  In insert
mode you can do do `ctrl-f`.

This comes in handy if you're doing clojure.  Just go the the beginning of the
sexp (usually the parenthesis) and do `=%` and it will auto-indent that whole
expression.  `==` will just do the current line.
