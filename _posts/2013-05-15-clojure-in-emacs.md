---
layout: post
title: Clojure in Emacs
date: 2013-05-15 22:34:02
categories: update programming
---
It was quite confusing to set up clojure for emacs.  Setting up clojure-mode
itself was quite easy.  Assuming you have the latest emacs with package
manager, you can look for clojure-mode.  Make sure the package manager is set
up by putting this in your `.emacs` or `.emacs.d/init.el` file.

```cl
(require 'package)
(add-to-list 'package-archives
             '("marmalade" . "http://marmalade-repo.org/packages/") t)
(package-initialize)
```

Then do

* `M-x package-list-packages`
* Choose `clojure-mode` by typing `i` when you're on that line
* Type `x` to execute the install

You should now have clojure mode.  You can test this out by opening a `.clj`
file and see that it says it's in clojure-mode.

Now I want to connect this to a REPL.  If you google search for this, you'll
see mentions of swank and SLIME.  If you go to the [github
page](https://github.com/technomancy/swank-clojure), you'll see it mention that
the project has been deprecated.  It is now replaced by
[nREPL](https://github.com/kingtim/nrepl.el).

Install nREPL by going through the package manager and choose `nrepl` (yes, you
could've done this at the same time you installed clojure-mode).

