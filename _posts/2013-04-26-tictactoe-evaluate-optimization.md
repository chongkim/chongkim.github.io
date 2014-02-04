---
layout: post
title: Tic Tac Toe evaluate optimization
date: 2013-04-26 10:15:00
categories: update programming
---
Tic Tac Toe evaluate optimization	I had a thought that I can do a better job of
evaluating the position in my Tic Tac Toe game.  For each unevaluated position,
I go through all the rows, columns and diagonals and check for` xxx` or `ooo`.
I realized I can do something clever by only evaluating on a move.  I only need
to check the row of the last move and the column.  I only check the major and
minor diagonals if the last move lies on the diagonal.  The change doubled the
speed.

I still needed to keep the original code so I can evaluate the initial position
since there is no last move.
