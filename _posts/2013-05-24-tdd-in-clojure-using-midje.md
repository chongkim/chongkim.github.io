---
layout: post
title: TDD in Clojure Using Midje
date: 2013-05-24 19:21:44
categories: update programming
---
I just discovered midje, a testing library for clojure.  Clojure already comes
with `clojure.test` and it looks something like this:

```clj
(ns tic-tac-toe.core-test
  (:require [clojure.test :refer :all]
            [tic-tac-toe.core :refer :all]))

(deftest init-position-test
  (let [position (init-position)
        ply (:ply position)]
    (testing "initialize a board."
      (is (= (:board position) '[- - -, - - -, - - -])))
    (testing "make sure it is x's turn"
      (is (= (:turn position) 'x)))))
```

An error looks like this

```bash
euler:tic-tac-toe.clj ckim$ lein test

lein test tic-tac-toe.core-test

lein test :only tic-tac-toe.core-test/position-string-test

FAIL in (position-string-test) (core_test.clj:15)
display of position
expected: (= (position-str (init-position)) "   |   |   \\n-----------\\n   |   |   \\n-----------\\n   |   |   ")
  actual: (not (= " 0 | 1 | 2 \\n-----------\\n 3 | 4 | 5 \\n-----------\\n 6 | 7 | 8 " "   |   |   \\n-----------\\n   |   |   \\n-----------\\n   |   |   "))

Ran 8 tests containing 22 assertions.
1 failures, 0 errors.
Tests failed.
```

If you fix the problem it, will look like this:

```bash
euler:tic-tac-toe.clj ckim$ lein test

lein test tic-tac-toe.core-test

Ran 8 tests containing 22 assertions.
0 failures, 0 errors.
```

With midje, it looks like

```clj
(ns ttt.midje
  (:use [midje.sweet]))

(fact (+ 2 2) => 5)
(fact (+ 2 2) => odd?)
```

Error output looks like

```bash
euler:ttt ckim$ lein midje

FAIL at (midje.clj:4)
    Expected: 5
      Actual: 4

FAIL at (midje.clj:5)
Actual result did not agree with the checking function.
        Actual result: 4
    Checking function: odd?
```

If you correct it, it looks like

```bash
euler:ttt ckim$ lein midje
All checks (2) succeeded.
```

To get midje set up, you need to add this to `~/.lein/profiles.clj`

```clj
{:user {:plugins [[lein-midje "3.0.0"]]}}
```

Add this to `project.clj` in your project root directory

```clj
  :profiles  {:dev  {:dependencies  [[midje "1.5.0"]]}}
```

Then you run the following to fetch the necessary files.

```bash
$ lein deps
```

Once you have it set up, you can modify the file located in
`test/<app>/midje.clj` directory (`test/ttt/midje.clj`).

To get stubbing, you pass `(provided <function-call> => <result>)`.  For
example, assume `foo` calls `bar`, you can define:

```clj
(fact
  (foo) => 'hello
  (provided (bar) => 'hello))

```
