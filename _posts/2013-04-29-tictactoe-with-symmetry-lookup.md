---
layout: post
title: 4x4 TicTacToe with Symmetry Lookup
date: 2013-04-29 09:24:00
categories: update programming
---
Last night I finally finished a working version of the 4x4 TicTacToe program.
I had to add the symmetry lookup because it took too long for me to actually
see how it plays.  Symmetry lookup takes the current position of the board and
makes the 8 transformations

* rotate 0
* rotate 90
* rotate 180
* rotate 270
* flip horizontal
* flip vertical
* flip on major diagonal
* flip on minor diagonal

and looks up the deep evaluation values.  Deep evaluation is evaluation of the
position looking at all following moves whereas the evaluation looks only at
the current position (i.e. it is the base case for the recursive deep
evaluation).

This did speed it up and I was able to play after waiting about half an hour
for the first move.  The game itself if not very interesting.  It's much too
easy to tie because the burden of getting four in a row is easy to thwart by
even the novice of players.

I think this is enough for now.  I need to look into other aspects of this
project, mainly getting an objective-c version.
