---
layout: post
title: Learning Bootstrap, LiveReload, vim, etc.
date: 2013-05-01 09:55:00
categories: update programming
---
Yesterday, I looked for documentation for Bootstrap but that wasn't necessary.
The documentation was on the [site](http://twitter.github.io/bootstrap/)
itself.  I was looking for a link that says "Documentation" but if you click on
the links at the top (Get Started, Scaffolding, Base CSS, Components,
Javascript, Customize), you get everything you need.  I read through the whole
thing and now I'm ready to work on my site with a fair degree of confidence.
It makes it really convenient to start up any website.  The documentation was
awesome.  It tells you everything you need without any fluff.

Playing around with Bootstrap, I had to install LiveReload so I can see the
changes right away.  I have guard running to keep things up to date.

I decided to try to use vim exclusively for a week.  I learned how to use
multiple cursors
([vim-multiple-cursors](https://github.com/terryma/vim-multiple-cursors) in
vim.  The problem is that it doesn't create multiple cursors for the next line,
which makes it difficult to column editing.  If you type `ctrl-n`, it will
highlight the word, and subsequent `ctrl-n` will bring you to the next word
creating a new cursor in the process.  I guess I'll have to look for another
vim package to do column editing.

I discovered Vim Adventure from the Python Meetup on Monday.  It's a web based
game that helps you learn vim.  You move the character using the vim key
strokes (`hjkl`) and learn new things as you progress through the game.  I
haven't had time to play with it much.  I'll try to find some time to play with
it this week.

Played Dominion during lunch.  It's an interesting game.  I find it interesting
that someone can make a card game and make it interesting.  The only card game
I know of are ones played with regular playing cards like poker or blackjack.
In Dominion, you start off with ten coins and victory point cards.  You shuffle
your deck and select five.  You buy cards that is in the common pool, such as
other coins, victory points, or action cards.  The action cards allow you to do
special things and the instructions are written on the card.  You win by
collecting the most victory points.  The victory points are useless during play
because they don't actually do anything so it just take up space in your hand.
The game ends when the 6-point victory card pile is depleted or when the other
three victor card piles are depleted.

During the day, I had some thoughts about my tic-tac-toe program.  I figured
that my symmetry lookup, that is looking for symmetrical patterns of the
current board, is taking too long so I came up with an idea.  Instead of
keeping track of the current board and calculating the symmetrical positions to
look up, I store eight copies of the current board in different symmetrical
states because updating a board is a lot quicker than creating a new board each
time.

I'm reading "Ruby on Rails 3 Tutorial".  Even though I know a lot of the
material, there is still a lot of new information, much of it ancillary to Ruby
on Rails itself.  I'm about a quarter of the way through.  I'm going to see if
I can finish this by tomorrow.  I want to get started on the next phase of my
learning, which is to learn objective-c and Mac OS X programming.

