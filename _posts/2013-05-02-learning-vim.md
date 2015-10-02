---
layout: post
title: Learning Vim
date: 2013-05-02 09:36:00
categories: programming
---
I knew vi from way back.  I've used it time to time, but I thought it was time
to get serious and start using vim for real.  I decided to use vim for a week
as my sole editor.  After Googling around the web, I realized I should start
from the beginning and typed:

{% highlight bash %}
$ vimtutor
{% endhighlight %}

I discovered `ctrl-d`.  In command mode (when you hit the `:`), `ctrl-d` will
list all the available commands.  You can start typing a few letters of the
command and press `ctrl-d` again and see them filtered.  You can also do this
with filenames when you do `:e`.

Learned about the `it` (inner tag) selection and in the process found out about
the other object object selections.  I see a lot of speed up potential to my
editing with these.  Do a `:h object-select`

I also learned that there is a user manual if you do `:h user-manual`.  You can
get there with tab completion by doing `:h user<tab>`.

Googling around, I found visual block mode via `ctrl-v`, which allows you to do
column editing.  It is built into vim.  Don't know how I missed this one.

Probably for the nth time, I got onto tpope's github site for some vim script.
I realized I should just go through his whole repository and look for stuff
than to google for random scripts.  Notably, `vim-surround`looks useful.

I got [snipMate](https://github.com/garbas/vim-snipmate) installed.  One
annoying problem I encountered was that the indentation is done with `<tab>`s.
Found that I just needed to add this to my .vimrc:

{% highlight vim %}
set expandtab
set ts=2
{% endhighlight %}


`set expandtab` will automatically convert tabs to spaces.  `set ts=2` sets the
tab stops to be 2.  The effect of these two options will put two spaces instead
of `<tab>`.

Probably the most useful command I discovered is `:map`.  It will show you the
key mapping.  Here is a sample output

{% highlight vim %}
n  <D-E>         :RerunSpec<CR>
n  <D-L>         :RunSpecLine<CR>
n  <D-R>         :RunSpec<CR>
x  S             <Plug>VSurround
n  \\\\u           <Plug>CommentaryUndo
n  \\\\\\           <Plug>CommentaryLine
n  \\\\            <Plug>Commentary
x  \\\\            <Plug>Commentary
n  cs            <Plug>Csurround
n  ds            <Plug>Dsurround
n  gx            <Plug>NetrwBrowseX
x  gS            <Plug>VgSurround
{% endhighlight %}

The first column looks like the mode.  `n` is normal.  I believe `x` might be
some extension.

Discovered that `ctrl-x ctrl-n` does word completion in insert mode.

