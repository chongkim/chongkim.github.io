---
layout: post
title: Poltergeist For Rails Javascript testing
date: 2013-05-27 01:18:28
categories: update programming
---
Since `capybara-webkit` is broken for JRuby. I installed the `poltergeist` gem.
It uses PhantomJS so I needed to install that too.

```bash
$ brew install phantomjs
```

I modified my `features/support/env.rb` file by adding the following at the end.

```ruby
require 'capybara/poltergeist'
Capybara.javascript_driver = :poltergeist
```

WooHoo!  It works.  Now I can work on the Tic Tac Toe program again.

