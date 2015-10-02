---
layout: post
title: Ruby Data Handling Between Threads
date: 2013-07-06 22:41:30
categories: programming
---
Let's say that I want to have two threads.  The main thread is waiting for the
worker thread to do a computation, which is expected to take some time.

{% highlight ruby %}
  x = nil
  Thread.new { sleep 1; x = 100; }
  sleep 100 while x.nil?
  puts "x = #{x}"
{% endhighlight %}

This code is not efficient because the `x` will be set in 1 second but the
while loop checks every 100 seconds, so if the thread has not completed by the
time it gets to the check, it'll have to wait the whole 100 seconds

Using `Thread#wakeup`
---------------------
A better method to let another thread know that the data is ready is by using
the `wakeup` instance method for Thread.

{% highlight ruby %}
  x = nil
  Thread.new { sleep 1; x = 100; Thread.main.wakeup() }
  sleep 100 while x.nil?
  puts "x = #{x}"
{% endhighlight %}

Now when the data is ready, the worker thread can notify the main thread
immediately.  We can even have the main thread just stop completely and wait
until the data is ready instead of polling the variable to see if it was set.
This is useful if the check is expensive.

{% highlight ruby %}
  x = nil
  Thread.new { sleep 1; x = 100; Thread.main.wakeup() }
  Thread.stop
  puts "x = #{x}"
{% endhighlight %}

A problem with this method is that the notification is happening at the thread
level.  If you have multiple variables you want to check, you have to handle it
yourself.  You also have the complication of what happens when the `wakeup` is
called but the main thread is not in the waiting state.

**NOTE**:  If you call `Thread.stop`, make sure that there is not another
thread calling `join` on that thread.  You will get a `deadlock detected
(fatal)`.

Using `ConditionVariable`
-------------------------

`ConditionVariable` works with `Mutex`.

{% highlight ruby %}
  require 'thread'
  x = nil
  m = Mutex.new
  cond = ConditionVariable.new
  Thread.new { m.synchronize { sleep 1; x = 100; cond.signal } }
  m.synchronize do
    cond.wait(m)
    puts "x = #{x}"
  end
{% endhighlight %}

The `cond.wait(m)` has an optional argument if you want a timeout, e.g.
`cond.wait(m, 100)`.

This code is not that much different.  Don't be fooled by `synchronize` because
you could also create mutexes in the `Thread` example.  Also it's quite
annoying since you have to keep track of two variables (`Mutex` and
`ConditionVariable` instances `m` and `cond`).  However, in the following code,
you can get around that by using `MonitorMixin`.

{% highlight ruby %}
  require 'monitor'
  x = nil
  x.extend(MonitorMixin)
  change_cond = x.new_cond
  Thread.new do
    sleep 1
    x.synchronize do
      x = 100
      change_cond.signal
    end
  end
  x.synchronize do
    change_cond.wait_while { x.nil? }
    puts "x = #{x}"
  end
{% endhighlight %}

Instead of `change_cond.wait_while { x.nil? }`, you can use
`change_cond.wait(100)` if you want to wait a specific amount of time.

Queue
-----
Probably the best way is to use `Queue`.

{% highlight ruby %}
  require 'thread'
  x = nil
  q = Queue.new
  Thread.new { sleep 1; q.push(100) }
  x = q.pop
  puts "x = #{x}"
{% endhighlight %}

If the queue is empty when you call `pop`, it will wait until something is
pushed into the queue.  There are many aliases for the methods `push` and `pop`

{% highlight ruby %}
  # these do the same thing as push
  q.push 100
  q.enq 100
  q << 100

  # These are the same as pop
  q.pop
  q.deq
  q.shift
{% endhighlight %}

`Queue` does not have a method that takes a timeout, but you can get around
that by using `Timeout::timeout`.

{% highlight ruby %}
  require 'thread'
  require 'timeout'
  x = nil
  q = Queue.new
  Thread.new { sleep 5; q.push 100 }
  begin
    Timeout::timeout(1) do
      x = q.pop
    end
    puts "x = #{x}"
  rescue
    puts "timed out"
  end
{% endhighlight %}

`Timeout::timeout` will raise a `Timeout::Error` exception if the block does
not complete within the timeout, so you'd need to handle it with a rescue.

In general, I'll probably use the `Queue` in my future code since it reads
better.

