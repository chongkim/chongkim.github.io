---
layout: post
title: Fixed my first bug in TicTacToe
date: 2013-04-27 23:00:00
categories: update programming
---
Somehow as I played my TicTacToe game, I noticed it was not unbeatable.  It was
unbeatable but somewhere along the way, I must've introduced a bug.  It was
passing my RSpec so I knew I had to dig deeper.

The problem happened during one of my optimization phase where I was memoizing
`@symmetries`.  This variable lived inside my ComputerPlayer class.  The
ComputerPlayer is looking for the best move.  In order to limit the amount of
search it needs to do, it finds all the symmetries of the current position,
then it removes any moves that are symmetrical, ie redundant.  The symmetry is
calculated and memoized until another move is made.  This was all fine and good
when the code was living inside the Board class.  When I moved it out into the
newly created ComputerPlayer, this was where it all went wrong.  The problem
happens when it's the HumanPlayer's turn.  When the code was living inside
Board, `@symmetries` was reset when either the HumanPlayer or the
ComputerPlayer moved.  Now that it's inside ComputerPlayer, it only got reset
when the computer moved.

The solution was to remove the memoized `@symmetries` and have it calculate it
every time.  It wasn't such a bad thing because the calculation was not done
that many times.  I came to this through the process of elimination.  Since the
`@symmetries` was only known to ComputerPlayer, I can't reset this when the
HumanPlayer moved or from anywhere outside of ComputerPlayer.  The
ComputerPlayer has no way of knowing if anyone has moved.  For instance, I can
call the symmetries method, modify the position of the board outside of
ComputerPlayer, and the call the symmetries method again.  I would expect
ComputerPlayer to find the symmetries for the updated position.

If the symmetries method took a long time and memoizing it was necessary, there
is a way to do it without explicitly resetting the memoized variable from
outside.  I could have a listener to the move method from Board.  So if anyone
tried to move pieces on the board, I could go through the list of listeners and
invoke any hooks.  This is a good general way to fix the problem.  I thought it
was overkill.  I may do this in the future if I think it's necessary -- i.e. if
I make extended version of the TicTacToe program.

This bug lead me to thinking about my TDD process.  How did this bug get
introduced and yet pass the RSpec tests?  This passed because there was a
missing test.  In this case, I wrote a failing test after finding the bug and
fixed it but could I have foreseen this problem and written the test before?
It is difficult to say because I am not going to write a test for every
possible move and even if I had written a test, there was no guarantee that the
bug was going to trigger that branch of the tree of possible moves.

I came out of this with two lessons.  One was to be very careful of memoized variables because refactoring can change the logic since it is dependent on state.  The second was that I should not memoize variables that are dependent on an outside object (the board, in my case) since those are subject to change state.  If you do, then you need to set up a listener so that you know when it has changed state.
