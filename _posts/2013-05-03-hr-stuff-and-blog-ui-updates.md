---
layout: post
title: HR Stuff and Blog UI 
date: 2013-05-03 19:16:40
categories: update programming
---
HR Stuff and Blog UI Updates	Spent most of the day getting my paperwork done
for 8th Light.  I will be starting as a resident apprentice on Monday 5/6.

I went home and slept until 11pm.  When I awoke, I decided I was going to work
on the Blog's UI a bit.

Data Migration
--------------
I created a new field called `published_at` that combined what `date` and
`time` did.  The difficult part was that I also wanted to combine the data.  I
know how to do it in SQL, but I wanted to find a Rails way.  Here's the final
result:

{% highlight ruby %}
class CreatePublishAt < ActiveRecord::Migration
  def up
    add_column :blog_entries, :published_at, :datetime
    BlogEntry.update_all "published_at = date + time"
    remove_column :blog_entries, :date
    remove_column :blog_entries, :time
  end

  def down
    add_column :blog_entries, :time, :time
    add_column :blog_entries, :date, :date
    BlogEntries.update_all "date = published_at::date, time = published_at::time"
    remove_column :blog_entries, :published_at
  end
end
{% endhighlight %}

**NOTE**: `published_at::date` converts `published_at` to a `date` type,
likewise for `::time`.

The alternative way to update `published_at` was to do something like this.

{% highlight ruby %}
# don't do this
BlogEntry.all.each do |entry|
  entry.published_at = DateTime.new(entry.date.year, entry.date.month, entry.date, day, entry.time.hour, entry.time.min, entry.time.sec)
end
{% endhighlight %}

It's a bad habit to iterate through each object because this would generate a
sql command for each row.  By using `update_all`, there is one sql command so
this would scale for large datasets.

Ace Editor
---------
I've been annoyed by the 80 column print margin that shows up on the editor
when entering a new blog entry.  After a lot of googling and trial and error, I
came upon this winning workflow.

1. In Chrome, go to the webpage that contains the editor.
2. Open up Javascript Console by `cmd-opt-J`
3. type `editor.set`

You should see that the console will try to complete the method.  If you scroll
through, you'll see something promising `setShowPrintMargin`.  So if you call 

{% highlight js %}
editor.setShowPrintMargin(false);
{% endhighlight %}

you'll see the print margin disappear.

Datepicker
----------
I went to the [JQueryUI website](http://jqueryui.com/) and added the CDN
(Content Delivery Network) to the header.  You can find the links at the bottom
of the page.  CDN are links that host the resource (Javascript or CSS) so you
don't have to have your own copy on your site.  It can make your site faster
because since it's a central resource, it can be cached across multiple
websites that use the CDN links.

I added a little javascript to get it working.

{% highlight html %}
  <script>
    $(function() {
      $("#blog_entry_published_date").datepicker({ dateFormat: "yy-mm-dd"});
    });
  </script>
{% endhighlight %}

I ran into a problem in the beginning because the example code on JQueryUI used
this format: `datepicker("option", "dateFormat", "yy-mm-dd")` but I wasn't able
to get it to work.
