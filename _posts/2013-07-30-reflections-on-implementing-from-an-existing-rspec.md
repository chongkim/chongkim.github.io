---
layout: post
title: Reflections on Implementing From An Existing RSpec
date: 2013-07-30 23:29:37
categories: update programming
---
I've been writing RSpec code first and implementing the actual code.  I go back
and forth until the program is done.  I had a thought.  What would it be like
if I took someone else's RSpec and started implementing it.  I wanted something
small, so I asked a co-worker if I could take her rspec and see what I come up
with.  I wanted to write a minimal program that will pass her test.

Before getting started, I turned off the RSpec config to run in random
ordering.  This way I can work on one spec at a time in order.  Usually tests
are built up as you go down the file, so this should make it easier to
implement.

```ruby
RSpec.configure do |config|
  config.treat_symbols_as_metadata_keys_with_true_values = true
  config.run_all_when_everything_filtered = true
  config.filter_run :focus
  # config.order = 'random'
end
```

After getting set up with my development environment, I started to run the
RSpec using Guard.  The first set of errors were all about non-existent files.
I created empty files, bringing me to the next set of errors.  I wrote the
empty classes and empty methods.  I just followed mechanically from one error
to the next.

When there was a non-matching expectation, I looked at how the test was set up
to get a clue about what the method was supposed to do.  If it was expecting a
list, I gave it an empty list.  If there was an expectation that a method was
called, I made sure it's included within the code.  This was probably the
hardest part -- to reverse engineer the logic based on the expectations.

When I finally got it to pass, I ran the main ruby code.  It gave errors about
missing `require` files.  This was because the RSpec had required all the files
in the lib directory as part of the configuration.  It's always a good idea to
require only the list of files within RSpec that you'd expect the main code to
require.  If you include all the lib files, as in this case, then you may find
missing required files when you run the main code.

After I put in all the missing requires. I started getting `nil` errors.  This
was because tests didn't check for all necessary instance variables after the
initialization.

The next error was "wrong number or parameters".  How could this be?  It passed
all the tests.  How was it possible that RSpec did not catch this.  I started
digging through the code and found that it was due to use of doubles.  Doubles
supply dummy code to make the testing easier.  In this case, it was used more
than necessary because it skipped over this erroneous code.

I stopped making corrections because there must be something wrong with the
tests if I get all these errors were happening after having passed the tests.

This was a good learning experience for me.  From an existing RSpec file, I was
able to make it pass from looking at the specs.  In this way RSpec really is
self documenting.  It would've been nice if I had it working at the end.

