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

After the installation, the `/usr/local` directory was owned by `root`. I
changed the ownership to me but this didn't fix the problem because later
`/usr/local/bin` and `/usr/local/share` reverted back to being owned by root. I
followed the instructions based on this [El Capitan and Homebrew] and it works now.

<ol>
  <li> Reboot machine in recovery mode (press &#8984;R on reboot)</li>
  <li> Open up a terminal (Click on <b>Utilities</b> menu and choose <b>Terminal</b>)</li>
  <li> Type <code>csrutil disable</code></li>
  <li> Reboot machine and log in as usual</li>
  <li> In the terminal type</li>
{% highlight bash %}
$ sudo chflags norestricted /usr/local
$ sudo chown -R $(whoami):admin /usr/local
{% endhighlight %}
  <li> Reboot back to recovery mode</li>
  <li> Type <code>csrutil enable</code> in terminal</li>
  <li>Reboot back to to OS X</li>
</ol>

[El Capitan and Homebrew]: https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/El_Capitan_and_Homebrew.md
