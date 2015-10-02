---
layout: post
title: Vim Fluency, Tmux Panes and iTerm
date: 2013-05-06 17:44:33
categories: programming
---
Learned some more vim and tmux over the weekend.

## Vim

* Learned about folding in vim -- `zf<motion>` to fold, `zo` to open a fold.  `:help folding` will give more info.
* `:NERDtree` allows me to navigate much easier.
* ControlP bound to `ctrl-p` allows me to use Textmate style file find.
* Since I have `set mouse=a` in my `.vimrc`, copy and paste to the system
  clipboard no longer works the same.  I can select with my mouse while holding
  down the `opt` button and that will bring my regular copy back.  However,
  this is not as useful since I have numbers in the gutter.  Instead, I have
  `ctrl-c` bound to `:w !pbcopy<Cr><Cr>`.

I'm able to use vim more fluently now.

## iTerm

I turned off iTerm Preference *General* > *Window* > *Use Lion-style Fullscreen
windows* because there is a delay due to the swiping animation when it has to
switch desktop spaces.  With it turned off, it's real zippy.

## tmux

Learned that you can detach a pane via `<prefix> !` (prefix is `ctrl-b` but I
bound it to `ctrl-a` because I find the screen binding more convenient -- ie
closer).  The following is my `~/.tmux.conf`.

{% highlight bash %}
# Set screen-like shortcuts  (also to avoid Ctrl-b for vi users)
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mode-mouse on
unbind C-b
set -g prefix C-a
unbind ^a
bind-key ^a  last-window            # C-a C-a: quick switch to last-viewed window
bind-key ^i  select-pane -t :.+     # C-a C-i: cycle between panes in window
bind-key A   command-prompt "rename-window '%%'"
bind-key '"' choose-window
bind-key k   confirm-before -p "kill-pane #W? (y/n)" kill-pane
bind-key K   confirm-before -p "kill-window #W? (y/n)" kill-window
bind-key S   split-window
bind-key a   send-key 'C-a'
{% endhighlight %}

The first three lines allow my mouse and tmux to interact as you'd expect from
a GUI interface.  The rest is just rebinding to be more like the unix `screen`
command -- something I'm more familiar with.
