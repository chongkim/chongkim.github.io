---
layout: post
title: An Elegant Negamax With Alpha-Beta Pruning in Clojure
date: 2013-05-29 08:59:13
categories: update programming
---
I've been reading up on [Negamax with Alpha-Beta
Pruning](http://en.wikipedia.org/wiki/Negamax) and I need to write the
following pseudocode in Clojure.

```js
function negamax(node, depth, alpha, beta, color)
    if node is a terminal node or depth = 0
        return color * the heuristic value of node
    else
        foreach child of node
            val := -negamax(child, depth - 1, -beta, -alpha, -color)
            if val >= beta
                return val
            if val > alpha
                alpha := val
        return alpha
```

At first I was struggling because I needed to figure out a way to modify a
variable and then break a loop.  The code was starting to get ugly and I knew I
was on the wrong course.  I realized I need to write it the way someone who
knows clojure would code it.  I thought, "What function has short circuiting?"
and I came up with `take-while`.  That returns a list, but the pseudocode was
just returning a number.  I started thinking about what the assignment was
doing and realized that it was just an artifact of the imperative language as
it was trying to find the max value of it's children.  This meant that once I
have the list, I just need to find the max and I'm done.  The resulting clojure
code looks like this.

```clj
(defn negamax [node alpha beta color]
  (let [node-value (evaluate-leaf node)]
    (if node-value
      (* color node-value)
      (->> node
           (find-children)
           (map #(- (negamax % (- beta) (- alpha) (- color))))
           (take-while #(< % beta))
           (cons alpha)
           (apply max)))))
```

Let's step through the code.

`evaluate-leaf` returns a value for the current node.  If there is a
`node-value`, that means it's a leaf-node (or terminal node if you use the
terminology of the pseudocode) and we can return a value.

In the else clause

* We start with the current node,
* then we get all its children ending up with a list of child nodes.
* We map the negamax function on each of the child nodes in the list.  At this
  point you may ask, "Doesn't this defeat the purpose of alpha-beta pruning
  because you're not cutting off the calculation when you find it necessary?".
  The answer is that `map` returns a lazy sequence, so the elements are not
  executing the recursion yet.
* The `take-while` will fetch each element as long as the condition holds.
  This is when the lazy sequence is realized (i.e. actually gets executed).
  When this is done, you'll end up with a list of values.
* `(cons alpha)` adds the alpha value that was passed in because in the
  pseudocode, we needed to have an initial value when calculating the max.
* We `apply` the `max` function on this list and we're done.

**Note** The return value needs to have the sign set by the color in the initial call, i.e.

```clj
(* color (negamax node alpha beta color))
```

**Note** The flaw in this code is that it is not updating the alpha after
checking each child.  It does get set when the cousins are calculated.  This
means I will need to write a new function that combines the `map` and
`take-while`.

Just for the record, the clojure code ended up being one line less than the
pseudocode.

As a side note, we see `->>`.  That is just a macro to reduce embedded
parentheses.  For example, these two statements are identical.

```clj
(->> x (foo 1 2) (bar 3 4))

(bar 3 4 (foo 1 2 x))
```

There is also `->` that works the same way but puts the previous form at the
beginning instead of the end of the argument list.  So in this case, these two
statements are equivalent.

```clj
(-> x (foo 1 2) (bar 3 4))

(bar (foo x 1 2) 3 4)
```

Back to the code.

