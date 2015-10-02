---
layout: post
title: Memoize In Clojure
date: 2013-05-30 00:29:32
categories: programming
---
Let's say you have a function that calls itself and repeatedly calculates
previous results.  For instance,

{% highlight clj %}
(defn fib [n]
  (println "fib" n)
  (cond (= n 0) 1
        (= n 1) 1
        :else (+ (fib (- n 2)) (fib (- n 1)))))

(fib 4)
{% endhighlight %}

gives this output.

{% highlight bash %}
fib 4
fib 2
fib 0
fib 1
fib 3
fib 1
fib 2
fib 0
fib 1
{% endhighlight %}

To cache the results, you need to use clojure's `memoize` function.

{% highlight clj %}
(def fib (memoize (fn [n]
                    (println "fib" n)
                    (cond (= n 0) 1
                          (= n 1) 1
                          :else (+ (fib (- n 2)) (fib (- n 1)))))))

(fib 4)
{% endhighlight %}

Now the output looks like this:

{% highlight bash %}
fib 4
fib 2
fib 0
fib 1
fib 3
{% endhighlight %}

In the previous example, `fib 1` was called three times.  This example only
executed it once and then cached the result so it didn't have to compute it
again.
