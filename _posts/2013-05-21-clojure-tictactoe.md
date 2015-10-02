---
layout: post
title: Clojure Tic-Tac-Toe
date: 2013-05-21 18:28:45
categories: programming
---
I finally completed my tic-tac-toe program in Clojure.  I learned enough about
Clojure to be comfortable with it the next time I need to write something.  I
also have a good development environment in vim.  That is probably more
important since you really need to be fluent in your environment to be able to
focus on learning the language.

I learned a new trick in vim paredit mode.  If I want to auto-indent an sexp, I
normally have to do `Jr<Cr>` (i.e. join the line, replace the space delimiter
with a carriage return so vim can do the auto-indent).  But that means I have
to do it for each line, which gets tedious really fast.  The new way is to wrap
the expression in parenthesis and then promote the inner sexp and voila!  The
sexp is auto-indented.  Instructions:

1. Go to the beginning of the sexp in normal mode.
2. `,W`.  This will wrap it in parentheses
3. Go to the beginning of the inner sexp.
4. `,I`.  This will promote it, i.e. remove the outer parentheses (the one you
   had just added).

Here's a list of Clojure functions I found useful:

{% highlight clj %}
(keep-indexed #(vector %1 %2) '(a b c)) ; => ([0 a] [1 b] [2 c])

(some #{1 2} '(1 2 3))  ; => 1
(some #{1 2} '(0 3 4))  ; => nil

(apply mapv vector '[[0 1] [2 3]]) ; => [[0 2] [1 3]]

(when (= 1 1) (+ 1 2))  ; same as (if (= 1 1) (+ 1 2) nil)

(read-line) ; reads a line from stdin

(flush) ; flushes stdout buffer

; tries to convert "123", throws exception on parsing error
; catch will handle the exception.
(try
  (Integer. "123")
  (catch NumberFormatException e
    false))

; you can throw an exception and catch it somewhere in you call heirarchy
(throw (Throwable. "my message"))
{% endhighlight %}
