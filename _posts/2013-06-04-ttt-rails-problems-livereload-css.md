---
layout: post
title: TTT Rails Problems - Livereload, CSS
date: 2013-06-04 14:05:18
categories: programming
---
One thing I hate about JRuby is that you keep encountering broken gems.
Livereload is one of those.  I have guard running and installed livereload for
guard and the browser.  It looked like it should work because I saw the guard
message that the browser had connected.  As soon as I make a change, it breaks.
Of course the next step is to set up a dummy MRI ruby instance and set up
livereload again to see if it's a problem with my setup.  I do that and it
works fine.  No problems.  I made sure I did the exact same steps in JRuby,
even uninstalling and reinstalling gems.  It still didn't work.  After an hour
or so, determined that the gem is broken.  I tried to see if there were other
gems, perhaps a jruby version.  I found one on Github, but it too was broken.
I wasted a lot of time on this.  This is one major drawback to using JRuby.

Another problem I had today was with CSS.  Let's say you had

```html
<!DOCTYPE html>
<html>
  <style type="text/css" media="all">
    #whole {
      width: 100%;
      height: 100%;
      background-color: red;
    }
  </style>
<body>
  <div id="whole"></div>
</body>
</html>
```

You'd expect to see a flood of red on your screen.  Instead you see nothing.
If you take away the <code>&lt;!DOCTYPE html&gt;</code>, then it works.  If you
keep the doctype, you can also get it to work by setting the `html` and `body`
sizes.

```html
<!DOCTYPE html>
<html>
  <style type="text/css" media="all">
    html, body {
      width: 100%;
      height: 100%;
    }
    #whole {
      width: 100%;
      height: 100%;
      background-color: red;
    }
  </style>
<body>
  <div id="whole"></div>
</body>
</html>
```

Seems like <code>&lt;!DOCTYPE html&gt;</code> defines the `body` and `html` to
have height zero until there is content.  This one issue took a while to figure
out because I kept stripping my HTML down until it was basically nothing.

One good thing was I got my project going along.  I incorporated Alejandra's
images and the background for the website.  I accidentally deleted the files
she had created for me, but I remembered that I had Time Machine and went back
and fetched it.  It was the first time I used Time Machine.  Now it has become
part of my tool set.
