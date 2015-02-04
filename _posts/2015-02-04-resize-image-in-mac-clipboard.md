---
layout: post
title: Resize Image In Mac Clipboard
date: 2015-02-04 15:04:18
categories: programming
---
At work, I had to grab a screen shot and paste it into an email.
I've done this many times befoe using Mail. I do &#8984;&#8679;&#8963;4
to put it into my clipboard (or pasteboard) and do a &#8984;v on Apple's Mail,
but at my new company we're using Outlook. Because I'm using a Retina Macbook Pro, pasting it into Outlook shows the image at twice the size.

![Picture of pasting from clipboard to outlook showing double size image](/img/2015-02-04-screenshot-paste-email.png)

I couldn't find any option in Outlook to resize the image, so I
started Googling around for solutions.  What I needed was a way to
resize the image conveniently in my clipboard. I know I could have
put it into a file, use GIMP to scale it down, import the picture
from Outlook, but that's way too many steps for something that
was once simple. I found three programs that I had to gather from the web

* [http://www.alecjacobson.com/weblog/?p=3816](http://www.alecjacobson.com/weblog/?p=3816)
* [https://github.com/jcsalterego/pngpaste](https://github.com/jcsalterego/pngpaste)
* [http://apple.stackexchange.com/questions/105185/how-can-i-stop-my-retina-display-from-taking-2x-sized-screenshots](http://apple.stackexchange.com/questions/105185/how-can-i-stop-my-retina-display-from-taking-2x-sized-screenshots)

I pieced them together into one git repository called [pbresize](https://github.com/chongkim/pbresize). Once you install it, you can just type:

```bash
$ pbresize
```

to resize the image in your clipboard, and you're free to paste it anywhere.
