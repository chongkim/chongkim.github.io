---
layout: post
title: Executing Shell Scripts
date: 2015-10-01 15:34:25
categories: programming
---
Let's say you just created the following file:

{% highlight bash %}
# file hello.sh
echo 'hello'
{% endhighlight %}

If you want to run it, you can try running it:

{% highlight bash %}
$ hello.sh
bash: ./hello.sh: Permission denied
{% endhighlight %}

Let's take a look at the permissions.

{% highlight bash %}
$ ls -l hello.sh
-rw-r--r--  1 ckim  staff  11 Oct  1 15:58 hello.sh
{% endhighlight %}

There is no `x` (executable) for the permissions, only `r` (read) and `w` write.
