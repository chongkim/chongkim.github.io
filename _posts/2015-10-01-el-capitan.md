---
layout: post
title: El Capitan Installing Problem
date: 2015-10-01 14:52
categories: programming
---
I ran into a problem when I downloaded El Capitan from the App Store. It started
downloading and I switched tasks to do other things in the meantime. When I
checked back with the App Store, it said "An error has occurred" next to "Downloaded".

I didn't know what to do at this point so I Googled around a bit and found a
solution. I need to look in my `Applications` folder for the install file.
Double click it to run it and everything went fine from there.

After the installation, the `/usr/local` directory was owned by `root` so I had to do

{% highlight bash %}
$ chown -R ckim:staff /usr/local
{% endhighlight %}
