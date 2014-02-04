---
layout: post
title: Autotest In Python
date: 2013-07-16 01:38:11
categories: update programming
---
In Python, there is a testing framework called `nose` and it's fairly easy to
use.

<pre>
$ pip install nose
</pre>

Create a file and create a function with a name starting with `test` (for
example `test`, `testFoo`, `test_foo`)

**myfile.py**

```python
def test():
  x = 1
  assert x == 2
```

This test should fail.  Run it

<pre>
$ nosetests myfile.py
F
======================================================================
FAIL: myfile.test
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/usr/local/lib/python2.7/site-packages/nose/case.py", line 197, in runTest
    self.test(*self.arg)
  File "/Users/ckim/lang/python/myfile.py", line 3, in test
    assert x == 2
AssertionError

----------------------------------------------------------------------
Ran 1 test in 0.002s

FAILED (failures=1)
</pre>

A passing test looks like this:

```bash
$ nosetests myfile.py
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

There is another package called `sniffer`

<pre>
$ pip install sniffer
</pre>

Depending on your operating system, you'll want to download one of these file
system checkers (otherwise it will poll your file system, which would be
slower):

* Linux: pyinotify
* Windows: pywin32
* Mac: MacFSEvents

By default sniffer will run a nose test, but it can be configured to run any
other framework or run some custom code.  Here's how to run it with nose

<pre>
$ sniffer -x myfile.py
</pre>

Whenever you change your code, the test will run and you can see the results
immediately.  The `-x` argument is passed to the testing framework (in this
case `nose`).

If you want to read more, you can go to [the github
repository](https://github.com/jeffh/sniffer) and read the README.rst

