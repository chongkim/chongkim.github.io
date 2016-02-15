---
layout: post
title: Gem problems with openssl
date: 2016-02-15 14:24:00
categories: programming
---

I did a `bundle install` on a Rails project and got a bunch of errors dealing
with openssl when it tries to compile. Towards the end of the message, we see:

{% highlight text %}
#warning use "ruby/io.h" instead of "rubyio.h"
 ^
mini_ssl.c:4:10: fatal error: 'openssl/bio.h' file not found
#include <openssl/bio.h>
         ^
1 warning and 1 error generated.
make: *** [mini_ssl.o] Error 1

make failed, exit code 2
{% endhighlight %}

The solution is to

{% highlight sh %}
$ brew install openssl
$ brew link --force openssl
{% endhighlight %}

Even if you have openssl installed, make sure to run the link command otherwise
bundler won't see it.
