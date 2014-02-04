---
layout: post
title: Gap in Coverage
date: 2013-04-22 23:59:00
categories: programming
---
Jury duty at Hillsborough County Courthouse. Was achy from playing tennis on
two days ago.  Wasn't selected.  Was able to get some work done while waiting.

I was able to refactor the code so that `ComputerPlayer` contains all the logic
of calculating the best move.  `Board` is just a functional board with the
responsibility of setting up the board and moving the pieces.

I use code coverage with simplecov.  This was after I discovered that my rspec
passed but threw an exception because of untested code.  This was the second
time (see 4/20/2013 post). It was untested due to aggressive use of stubs.  I
added those stubs because the tests were taking too long for certain
calculations.  I figured it was okay to stub those methods since it was being
tested elsewhere.  The problem happens when you refactor and methods aren't
where they're supposed to be.  The code coverage detected the gap. I also
removed all stubs except for `puts`, `print`, `gets`.

As soon as I got home I fell asleep right away.  It was really difficult to sit
still on a hard bench while my body is aching.  I just wanted to lie down the
whole time.  When I woke up, I tried out rspec-prof but I didn't find it
useful.  The output intermingled RSpec and the TicTacToe code and I couldn't
make sense out of it.
