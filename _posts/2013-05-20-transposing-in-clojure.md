---
layout: post
title: Transposing in Clojure
date: 2013-05-20 18:22:48
categories: programming
---
Let's say you have `[[0 1 2] [3 4 5] [6 7 8]]` and you want to transpose that
to `[[0 3 5] [1 4 7] [2 5 8]]`.  There is a simple idiom that takes care of
that.

{% highlight clj %}
(apply mapv vector [[0 1 2] [3 4 5] [6 7 8]])
{% endhighlight %}

Let's break this down.  Our end goal is to get something like

{% highlight clj %}
(vector
  (vector 0 3 6)
  (vector 1 4 7)
  (vector 2 5 8))
{% endhighlight %}

You can get this by grouping each of the columns into a vector and mapping over
them

{% highlight clj %}
(mapv vector [0 1 2] [3 4 5] [6 7 8])
{% endhighlight %}

The only problem is that our input is a vector of vectors.  Using `apply`, it
will splat the vector (i.e. embed, or flatten, them into the call), so you end
up with the three vectors.

