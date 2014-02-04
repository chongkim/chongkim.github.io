---
layout: post
title: Ruby Debugging
date: 2013-07-24 17:39:55
categories: update programming
---
To start debugging in ruby 1.9, you need the gem `debugger` (see [github
repository](https://github.com/cldwalker/debugger))

**Gemfile**

```ruby
source "https://rubygems.org"

gem "debugger"
```

**yourcode.rb**

```ruby
require "debugger"

def my_function
  debugger    # <== place debug point by putting this in your code
  x = 1
end
```

You can also do it in one shot:

```ruby
def my_function
  require "debugger"; debugger
  x = 1
end
```

Because the breakpoint is in your code, you can put logic around it

```ruby
def my_function
  debugger if foo == 3 && !bar
  x = 1
end
```

You should put `debugger` before the desired breakpoint because it will stop on
the next statement after a call to `debugger`.  If you put it at the end of
function, you may end up in a different file, wherever the stack frame happen
to be after the function returns.

You run your code the same way as you did before, the difference is that you'll
be placed into a interactive ruby debugger.

People have injected `pry` into their code to put an interactive shell so they
can look around (This is done by `require "pry"` and calling `binding.pry` in
the code).  `pry` is powerful and it can be used for some types of debugging,
but it's not a debugger.  You are not able to step through your code.  Within
`debugger`, have access to the ruby interpreter so you have most of the
functionality you need.  So if you used `pry` in the past, you should try out
`debugger`.

Once you're inside the debugger, you can type "help" or just "h".

```bash
(rdb:1) h
ruby-debug help v1.6.1
Type 'help <command-name>' for help on a specific command

Available commands:
backtrace  delete   enable  help  list    ps       save    start   undisplay
break      disable  eval    info  method  putl     set     step    up
catch      display  exit    irb   next    quit     show    thread  var
condition  down     finish  jump  p       reload   skip    tmate   where
continue   edit     frame   kill  pp      restart  source  trace
```

You can also type "h set" to see options available

```bash
(rdb:1) h set
Modifies parts of the ruby-debug environment. Boolean values take
on, off, 1 or 0.
You can see these environment settings with the "show" command.

--
List of set subcommands:
--
set annotate -- Set annotation level
set args -- Set argument list to give program being debugged when it is started
set autoeval -- Evaluate every unrecognized command
set autolist -- Execute 'list' command on every breakpoint
set autoirb -- Invoke IRB on every stop
set autoreload -- Reload source code when changed
set basename -- Report file basename only showing file names
set callstyle -- Set how you want call parameters displayed
set debuggertesting -- Used when testing the debugger
set forcestep -- Make sure 'next/step' commands always move to a new line
set fullpath -- Display full file names in frames
set history -- Generic command for setting command history parameters
set linetrace+ -- Set line execution tracing to show different lines
set linetrace -- Set line execution tracing
set listsize -- Set number of source lines to list by default
set trace -- Display stack trace when 'eval' raises exception
set width -- Number of characters the debugger thinks are in a line
```

You can put these commands into a `.rdebugrc` file.  You can also require ruby
files so it'll load automatically when the debugger is run.  I always have
"autolist" set so I can see the code listing while I am stepping through the
code.  You should also set autoeval so you can type ruby code (e.g. "a = 2")
rather than typing "eval" (e.g. "eval a = 2") or using "p" to print the value.

Some useful commands

* n : to go to the next statement
* s : to step into the statement
* c : continue
* fin : to finish the method and stop at the next stack trace
* p <expr>: print out result of ruby expression
* pp <expr>: pretty print result of ruby expression.  It prints list and hashes
  in a more readable format
* bt : a backtrace to tell you where you are (you can also use "where")

You can exit by typing "exit", "q", or press Ctrl-d.

When you're debugging something complicated, it's a good idea to put some print
statements to see what your program is doing, but you may not want to have to
clean it up every time.  I solve this by creating a `Logger` class that takes a
`debug` method.  It will only print if the debug flag is set.  This is
especially useful when you're dealing with multiple threads or when you're not
sure where to put the breakpoint.

I think you should try `debugger` out.  It's worth learning.

