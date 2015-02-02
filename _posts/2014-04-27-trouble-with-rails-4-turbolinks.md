---
layout: post
title: Trouble With Rails 4 - Turbolinks
date: 2014-04-27 10:49:25
categories: programming
---

I ran into a problem with my Rails 4 server.  My `$(document).ready()` was not
being called.  After digging around a bit I found it was because of turbolinks.
Turbolinks makes your webpage load faster because it updates the head and
body when you click on a link, so it doesn't have to reprocess the javascript.
The problem is that the `onload` for the document is not triggered, which means
that this breaks jQuery's `$(document).ready()`.

The easiest solution is to use jquery.turbolinks

Gemfile:

```ruby
gem 'jquery-turbolinks'
```

app/assets/javascripts/application.js:

```javascript
//= require jquery
//= require jquery.turbolink
//= require jquery_ujs
//= require turbolinks
//= require_tree .
```

This update the jQuery so that `$(document).ready()` will also register to
turbolink's `page:load` event.  Now everything should be working normally.
