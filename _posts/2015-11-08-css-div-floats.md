---
layout: post
title: CSS div floats
date: 2015-11-08 13:15:00
categories: programming
---

One problem with putting `div` floating inside a container (such as another `div`) is that the containing `div` does not handle the size very well and it ends up collapsing.

Let's say you have the following HTML:
{% highlight html %}
<div class="container">
  <div class="float"> float 1 </div>
  <div class="float"> float 2 </div>
  <div class="float"> float 3 </div>
</div>
{% endhighlight %}

and the following CSS:
{% highlight css %}
.container {
  border: 1px solid green;
}
.float {
  border: 1px solid red;
  width: 50px;
  float: left;
}
{% endhighlight %}

<style>
.container {
  border: 1px solid green;
}
.float {
  border: 1px solid red;
  width: 50px;
  float: left;
}
</style>

You'll end up with with a collapsed container (in green).

<div class="container">
  <div class="float"> float 1 </div>
  <div class="float"> float 2 </div>
  <div class="float"> float 3 </div>
</div>
<div style="clear: both"></div><br/>

If add `overflow: auto;` to the container, then it will prevent it from collapsing:

{% highlight css %}
.container {
  border: 1px solid green;
  overflow: auto;
}
{% endhighlight %}


<div class="demo">
  <div class="container" style="overflow: auto">
    <div class="float"> float 1 </div>
    <div class="float"> float 2 </div>
    <div class="float"> float 3 </div>
  </div>
</div>
