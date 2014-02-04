---
layout: post
title: Macbook Pro Hangs On Startup -- Fixed
date: 2013-05-17 08:24:38
categories: update programming
---
Today, I was using my laptop as normal.  I closed the laptop and went home.
When I opened my laptop, I noticed my machine was completely stalled.  Computer
gave no response when I tried to do anything (pressing keys, moving mouse).  I
turned it off and restarted it.  I hear the bell when the laptop starts up,
then it completely freezes again showing only the gray background and an apple
logo.  No spinner, no mouse, not responsive.

The fix takes about two hours.  Follow these steps: (Note: You may need to be
connected to the Internet.  I was connected via Ethernet cable when I did this.)

1. Turn off the laptop.
2. Turn on the laptop and wait for the tone the laptop makes when it starts up.
3. Immediately press `command-R`. The laptop will boot up in Recovery Mode.
4. When it prompts you with a menu, choose to re-install the operating system.
5. You wait.  The laptop will take about two hours to re-install the OS.  It
   will reboot itself (perhaps twice).  When it is all done, you will see a
   login prompt.
6. You'll need to reinstall Xcode command tools.  Open Xcode
7. Go to the menu item *Xcode* > *Open Developer Tools* > *More Developer
   Tools...*
8. This will open up a webpage.  Download the Command Line Tools
9. Open the dmg file and install.

At this point, your OS has been fixed... at least for now.  We haven't actually
fixed the original problem so it may happen again, but probably not for a long
time.  This problem happened to me twice in 6 months on my Macbook Pro Retina
15".

