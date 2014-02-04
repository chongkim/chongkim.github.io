---
layout: post
title: Homebrew And MySQL
date: 2013-05-08 18:11:42
categories: programming
---
I've been using MacPorts and I needed to install clojure.  The one on MacPorts
is old and Gavin Stark told me I should use Homebrew and get rid of MacPorts
because it's not up to date on a lot of stuff and suggested I start with a
pristine `/usr/local` directory.  So I blew away my MacPorts directory `/opt`
and `/usr/local` and used installed `mysql` and `postgresql`.  The only tricky
part was that my MySQL Preference Pane is expecting to see `/usr/local/mysql`.
I just symlinked that to current version of mysql

```bash
sudo ln -s /usr/local/Cellar/mysql/5.6.10 /usr/local/mysql
```

and everything is back to normal.  This may be a problem if I upgrade in the
future.  I may fix this by removing the symlink and make it into a real
directory and symlinking the individual bin commands from
`/usr/local/mysql/bin` to `/usr/local/mysql/bin`
