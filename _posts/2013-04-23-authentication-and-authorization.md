---
layout: post
title: Authentication and Authorization with Devise and CanCan
date: 2013-04-23 23:59:00
categories: programming
---
Spent the day setting up authentication with devise and authorization with
CanCan for this blog website. Devise allows you to register on the website and
get email confirmation.  I had some of the issues with heroku.

* Turned out that it does not automatically run the `rake db:migrate` for you.
  I suppose if you want to have this set up, you need to create a `Procfile`
  with some additional commands to run.  Since the migration only needs to be
  run once, I don't think it's necessary to do this.  I just need to run
  `heroku run rake db:migrate` after the deploy and before I hit the website.
* Heroku takes a few minutes for it to send out email.  Since I'm using the
  free version, I have to live with this.
* I get an error message if I have assets.  Heroku will throw a bunch of error
  messages when you deploy and it's not very clear what it's doing.  After
  googling on the web, I determined that it's because of precompiling assets.
  Initially I thought it was because of incompatible ruby versions (1.9.2 vs
  1.9.3).  The solution was to
  1. set `config.assets.initialize_on_precompile = false` in
  config/application.rb
  2. precompile the assets yourself using `bundle exec rake assets:precompile
  3. check it into git
  4. push to heroku.

CanCan is an authorization tool.  It assigns certain permissions to Models for
CRUD (create, read, update, destroy) operations.  You can assign other
permissions as well but those are the conventional ones.  It's written by Ryan
Bates of Railscast fame.  Was fairly simple to set up.

* Used the same code as the example
* Added an is_admin field to the `User` model (needed migration)
* Added `admin?` method on `User`
* Modified the view to put conditionals around certain links.  For example, in
  blog_entries/index.html.erb

{% highlight erb %}
<% if can? :read, BlogEntry %>
  <%= link_to 'Show', blog_entry %>
<% end %>
<% if can? :update, BlogEntry %>
  <%= link_to 'Edit', edit_blog_entry_path(blog_entry) %>
<% end %>
<% if can? :destroy, BlogEntry %>
  <%= link_to 'Destroy', blog_entry, method: :delete, data: { confirm: 'Are you sure?' } %>
<% end %>
{% endhighlight %}

I prettied up the blog entry listing by rearranging some HTML structure.  I
wanted to add multimarkdown so I don't have to use html while writing the blog.
I tried out BlueCloth but didn't like it because it was just using markdown.
I'm using RedCloth right now, but I'm not too happy because the support for
multimarkdown is limited.  I'm looking for something more full featured so that
I can describe source code and it will display it using github style.  There is
a potential gem called rpeg-multimarkdown.  I'll try that out.  If that doesn't
work, I may have to write my own.

Went to the Microcontroller's meetup in Pinellas Park Library.  Bruce was
showing his web interface that simplifies sending controls to various parts of
the robot.  You specify the code in Python.  It's a shame that Ruby is not used
more with microcontroller programming.  It's a shame that is' not used for
Geospatial Analysis (standard language being Python).  It's a shame that it's
not used for scientific calculations (Python again is used along with Fortran,
C/C++ -- for example look at CUDA, a toolkit that uses parallel processing and
fast matrix operations from your GPU).  It's no wonder that Python has IPython,
a scientific notebook, although IPython can interface with Ruby (among other
languages).

My next steps are to

* look into Bootstrap to make the site look pretty,
* try out rpeg-multimarkdown,
* look for a better way to enter and edit my blog entry.  I want to be able to
  add images along with the text,
* start looking into tic-tac-toe again
* read objective-c
