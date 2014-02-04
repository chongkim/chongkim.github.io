---
layout: post
title: Spork Broken For Cucumber On JRuby
date: 2013-06-05 23:52:15
categories: update programming
---
Spork was almost running on JRuby, but it's completely broken.  I ran my
experiment where I created a new MRI rails application called `foo`.  I
modified the Gemfile to include

```ruby
 group :test do
  gem 'spork-rails'
  gem 'cucumber', '1.2.5'
  gem 'cucumber-rails', :require => false
  gem 'guard'
  gem 'guard-spork'
  gem 'guard-cucumber'
  gem 'database_cleaner'
end
```

I run `bundle install`.

I set up cucumber with `rails g cucumber:install`.

I set up spork with `spork cucumber -b`.  I modify the
`features/support/env.rb` file.

I set up guard with:

```bash
guard init cucumber
guard init spork
```

I edit the `Guardfile` so that cucumber runs with `:cli => '--drb'`.

I create some dummy feature files and I run `guard`.  This works perfectly on
MRI Ruby, but JRuby acts really flaky.  First thing you notice is the error
message:

<pre>
16:02:45 - INFO - Running all features
SocketError: bind: name or service not known
        bind at org/jruby/ext/socket/RubyUDPSocket.java:160
  initialize at /Users/ckim/.rvm/rubies/jruby-1.7.1/lib/ruby/1.9/rinda/ring.rb:35
      (root) at ring_server.rb:7
</pre>

Second thing you notice is that the color is gone *if* it runs your features.
Sometimes it decides not to run it.

If you run `cucumber` on the command line it complains that there is no DRb

<pre>
euler:jfoo ckim$ cucumber --drb
Using the default profile...
file:/Users/ckim/.rvm/rubies/jruby-1.7.1/lib/jruby.jar!/jruby/java/java_package_module_template.rb:11 warning: `eval' should not be aliased
WARNING: No DRb server is running. Running features locally:
</pre>

But you can see that it connected from looking at the spork output log.

I did the same thing using MRI Ruby and everything worked.  No problems at all.
I'm beginning to hate JRuby even though there's nothing with with JRuby itself.
The gem support really sucks.

I tested RSpec and that seems to work fine on JRuby so I'll need to convert my
test over.
