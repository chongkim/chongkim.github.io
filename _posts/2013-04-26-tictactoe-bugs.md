---
layout: post
title: Tic Tac Toe bugs and RSpec during memoized position optimization
date: 2013-04-26 10:24:00
categories: update programming
---
Tic Tac Toe bugs and RSpec during memoized position optimization	I discovered
a bug in my Tic Tac Toe program that was not detected by the RSpec.  I'm trying
to wrap my head around this problem because I wonder if I did anything wrong
when I was developing my RSpec.  The bug happens when I am playing a game where
I let the computer win.  On the turn where the computer should pick out the
winning move, it misses it completely.  I'm not sure when it was introduced but
I suspect that it was when I added the evaluate-on-move optimization.

I had just finished my memoized position optimization where the program
remembers the evaluation of each positions so it doesn't have to recalculate it
if it encounters it again.  Initially I thought the bug was introduced during
this optimization, but I went back to my previously committed code, the
evaluate-on-move optimization, and saw that it was happening there too.  I
remember when I was initially writing my code before any optimization,  I was
able to let the computer win.  I look at my test suite and saw that I do not
have a test that allows the computer to win.  The main reason for this was
because my understanding of RSpec was not good enough to implement the test the
way I wanted to.  I googled around a bit and I think I have enough info to
implement it.  There will be another blog entry when I have this all figured
out.
