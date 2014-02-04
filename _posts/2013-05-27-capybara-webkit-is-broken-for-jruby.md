---
layout: post
title: Capybara-webkit Is Broken for JRuby
date: 2013-05-27 00:37:01
categories: programming
---
I've been having a hard time trying to get `capybara-webkit` (version 1.0.0)
working on my rails app using cucumber using JRuby.  When I run `cucumber`, I
see this error

```bash
  @javascript
  Scenario:
    Given I visit the home page
      undefined method `[]' for nil:NilClass (NoMethodError)
      ./features/step_definitions/ttt_steps.rb:2:in `/^I visit the home page$/'
      features/ttt.feature:5:in `Given I visit the home page'
    Then I should have selector "#ttt"
    And I should see content "Who do you want to play first"
```

I suspected it might have something to do with the jruby version, so I created
a new Rails app using the MRI ruby and it worked perfectly.  I also tried using
RSpec instead of Cucumber, and it had the same problem.

Since I can't rely on capybara-webkit on jruby, I'll have to look into selenium
to test the javascript.

JRuby is nowhere close to the maturity of MRI Ruby.  The usual gems like
`debugger` or `looksee` is not able to be installed.  My experience with
`capybara-webkit` showed me that even if I managed to get it to install, there
is no guarantee that it would work.  It's tempting to scrap JRuby and go back
to MRI, but I'm not sure how I would handle Clojure.  I could make the Clojure
code run as a server but I think that defeats the learning experience of trying
to get it integrated.
