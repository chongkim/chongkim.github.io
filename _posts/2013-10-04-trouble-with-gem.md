---
layout: post
title: Trouble With Gem
date: 2013-10-04 08:49:25
categories: update programming
---
I've been getting this error when I try to install a gem:

```bash
ERROR:  Could not find a valid gem 'pry' (>= 0), here is why:
          Unable to download data from https://rubygems.org/ - SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://s3.amazonaws.com/production.s3.rubygems.org/latest_specs.4.8.gz)
```

My solution was to reinstall my ruby instances via:

```bash
$ rvm list   # to get the list of ruby versions

$ rvm reinstall 2.0.0 --with-openssl-dir=$rvm_path/usr
```

