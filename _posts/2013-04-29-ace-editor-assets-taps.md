---
layout: post
title: Ace Editor, Assets, taps
date: 2013-04-29 15:54:00
categories: update programming
---
Just added the Ace editor into my blog.  It was quite an ordeal getting the
content passed from the editor into the textarea so it can be processed by
Rails.  The trick was to set up javascript to copy the data from the textarea to
the editor and then pass it back from the editor to the textarea on submit.

Finally determined that I have to precompile my assets before pushing out to
heroku blog site.  I have a little bit of texture for the background.  Now that
it is able to access the CSS and javascript, I can start doing something useful
with it.

I installed a gem called `taps`.  It allows you to easily import and export the
database.  Once installed, you type `heroku db:pull`.  You can also do `heroku
db:push`.  I have my production and development databases synched up.

Funny thing happened today.  In the morning, the person entering the room has to
greet everyone else.  I went around and bumped fists and shook hands.  When I
got to Megan, I didn't recognize her because she changed her hair.  It was
darker and in a different style.  I went to her and introduced myself causing
the room to burst out laughing.
