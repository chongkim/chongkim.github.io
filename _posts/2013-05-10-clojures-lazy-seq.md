---
layout: post
title: Clojure's lazy-seq
date: 2013-05-10 18:28:49
categories: programming
---
I'm reading through Programming Clojure and was struck by one of their examples
on lazy-seq.  They didn't go into detail because they will be going more in
detail on lazy evaluation on a future chapter.  The started to analyze the
code:

```clj
(def primes
  (concat
   [2 3 5 7]
   (lazy-seq
    (let [primes-from
          (fn primes-from [n [f & r]]
            (if (some #(zero? (rem n %))
                      (take-while #(<= (* % %) n) primes))
              (recur (+ n f) r)
              (lazy-seq (cons n (primes-from (+ n f) r)))))
          wheel (cycle [2 4 2 4 6 2 6 4 2 4 6 6 2 6  4  2
                        6 4 6 8 4 2 4 2 4 8 6 4 6 2  4  6
                        2 6 6 4 2 4 6 2 6 4 2 4 2 10 2 10])]
      (primes-from 11 wheel)))))
```

A few things of note:

* This is not a function definition.  This is binding `primes` to a list which
  is lazy evaluated.
* The function `primes-from` is named twice.  Once for the `let` to get local
  scoping and as the name argument for `fn` so that this function has a name.
  The name is required in this case because it is called recursively.
* The `if` condition checks to see if _n_ is divisible by any of the previous
  subset of primes.  It is not necessary to check the complete previously
  generated primes because mathematically only numbers \\\\( \\sqrt{n} \\\\) is
  a possible divisors of \\\\(n\\\\).
* In `take-while` in the `if` conditional, it is necessary to find a value to
  test that is included in the previous cached values of `primes`.  For
  instance, if you had

```clj
(take-while #(< % n) primes)
```

This would never end (infinite recursion) because let's say _n_ = 8. `primes`
would return `[2 3 5 7]`, which are all less than 8 so it will try to fetch the
next prime number from `primes`, which is exactly what it was trying to do in
the first place.  Thus it gets caught in an infinite recursion.  You need the
test to have a failure point (ie where it evaluates to false) within the
precomputed list.  So in the original code `(take-while #(< (* % %) n) primes`,
3 does the trick since `(< 9 n)` (_n_=8 in this case) stops the `take-while`
from continuing.

* `(recur (+ n f) r)` is allowed to be used instead of a normal recursive call
  because it is the last line of executable code of the function `primes-from`.
  `recur` works just like a recursive call without building a new stack -- for
  efficiency.
* The `recur` in the `if` clause don't have `lazy-seq`because we haven't found
  a prime and we want it to keep searching.
* The else clause needs a `lazy-seq` because it found the next prime and wants
  to have that value available and we do not want to have the recursive call to
  `prime-from` executed here but at the time when it gets evaluated.  In effect
  it is putting a marker here to say what it needs to execute when it the
  evaluator sees it.
* The recursive call in the else clause cannot use `recur` because there is
  code that needs to be executed after `prime-from` returns with it's value.
* The following code could be written another way from

```clj
(lazy-seq (cons n (primes-from (+ n f) r)))
```

to

```clj
(cons n (lazy-seq (primes-from (+ n f) r)))
```

* Seems like `lazy-seq` needs to have a recursive call in the body otherwise it
  throws an exception.
* The `wheel` is just a set of increments used to find the next number to test
  for a prime.  Since we know that 2, 3, 5, 7 are prime, we can skip multiples
  of these.  Once you get the list of offsets, they cycle.
