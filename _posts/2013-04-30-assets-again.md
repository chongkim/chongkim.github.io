---
layout: post
title: Assets again
date: 2013-04-30 10:05:00
categories: programming
---
Yesterday, I thought I figured out what I needed to do in order to get assets
working on heroku.  Today, I modified the CSS in `app/assets/css` and pushed it
out to heroku without running `bundle exec rake assets:precompile`.  It worked
anyway.  I saw from the output

```
...
-----> Preparing app for Rails asset pipeline
       Running: rake assets:precompile
       Asset precompilation completed (25.81s)
...
```

The difference was that in this push, I deleted all the files in
`public/assets` and committed those deletes.  I suspect that Rails sees that
the directory is empty and runs the `rake assets:precompile`.  This is good
news.  This means I don't need to precompile and check in those compiled
assets.  That's less files to keep track of and one step less in the deploy
process.

The site is starting to look prettier.  Still a lot more work to do before it
starts looking like something people would want to visit.
