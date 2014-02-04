---
layout: post
title: Object Scope Bindings
date: 2013-05-06 07:59:59
categories: update programming
---
Some time ago, I saw a ruby code that looked something like

```ruby
obj.some_method do
  foo "something"
end
```

where foo was some method of `obj`.  I could see that inside of the block the
scoping rules were respect to the `obj`.  I wondered for a long time how this
was done so I decided to figure it out.  It turns out that it's just a simple
use of `instance_eval`.  You can implement it as such:

```ruby
class A
  def foo arg
    puts arg
  end

  def some_method &block
    instance_eval(&block)
  end
end

obj = A.new
obj.some_method do
  foo "something"
end

#=> "something"
```

You can see something like this from RSpec or rake.
