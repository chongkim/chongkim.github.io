---
layout: post
title: autoreload gem
date: 2013-07-10 17:39:58
categories: programming
---
I'm writing an http server and I make small modifications to the code, such as
displaying certain items.  The problem is that I have to stop the server and
run it each time.  This can get quite annoying if you need to do this serveral
times when you're tweaking something.

You can get around this problem by using the `autoreload` gem.

```ruby
require "autoreload"
autoreload(interval: 2) do
  require "./myserver"
end

myserver = MyServer.new
myserver.start
```

`myserver.rb`:

```ruby
class MyServer
  def foo
    1
  end
  def start
    loop do
      puts foo
      sleep 2
    end
  end
end
```

When you run this, you'll see 1's being printed.  Keep the code running and
modify `myserver.rb` so that `foo` returns `2`.  The running code will now
display 2 instead of 1.

This is a great time saver.  If you do anything that causes an exception, the
running program will terminate.
