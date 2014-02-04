---
layout: post
title: Initial Blog
date: 2013-04-20 08:00:00
categories: update programming
---
The is the start of my blog. I'm writing this in an HTML static file even
though it's a Ruby on Rails app. Eventually I'll get this set up so that it's
stored in a database and acts like a real app. For now, it's just plain old
HTML.

I'll be starting as an apprentice at 8th Light on May 6th (a couple of weeks
from now), but I'll be coming in next week to prepare. I think it's going to be
an interesting experience. I've already submitted my tic-tac-toe program and
had it reviewed by Micah (CTO). He made a really good suggestion to make a
Player class. I incorporated it into my code yesterday and the main code looks
a lot better. The next phase for my tic-tac-toe program is to extend it so that
it can also work on a 4x4 grid and/or a 3x3x3 grid. My solution is general
enough so I don't have to rewrite the whole thing. I'll probably need to make a
few minor tweaks and a 4x4 should not be too far off. My only concern is that
it's a bit slow on the start up. If you let the computer go first on the 3x3,
it takes about 10 seconds before it makes a move. I've already brought the time
down due to some optimizations:

* Symmetry detection: If it sees that two moves are symmetrical, then filter
  out the second one since it's redundant.
* Data structure: Initially the board was set up as a string. The problem is
  when you access a particular cell like `data[3]`, instead of returning a
  character like C, it's returns a substring. In Ruby 1.8.7, it used to return
  an ascii value of the character stored in that location, but in Ruby 1.9.3,
  it returns a substring. This means every time I access a cell, it has to
  create a substring. You can imagine how slow this would be in your code. I
  changed it so that board is now an array of strings. This avoids any string
  allocation and I can leave the rest of my code unchanged since accessing a
  `data[3]` works the same in either representations.
* I think it's still too slow. My guess is that it's because of the recursion.
  I've heard that python's interpreter deliberately did not implement tail
  recursion optimization so that it can make the debugging processing easier.
  That made me look into Ruby and found that it too does not optimize on tail
  recursion. That means for my program, it has to create a call stack for each
  recursive step. This can get quite expensive. It's equivalent to the string
  problem I mentioned earlier -- i.e. allocating unnecessary blocks of memory.
  I'll have to see what ruby-prof has to say about this, although I wouldn't be
  too surprised if it doesn't mention this at all since it might be too low
  level and not actually part of the program per se. One way around all this
  optimization is to put the recomputed moves into some form of persistent
  storage. I'd probably use this as a last resort after I finish any other
  optimizations.

My next feature is to make it run on a 4x4 grid. I'll start this after I unroll
the recursion.
