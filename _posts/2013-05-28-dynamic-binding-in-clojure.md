---
layout: post
title: Dynamic Binding in Clojure
date: 2013-05-28 23:21:13
categories: update programming
---
Clojure has a `binding` method that allows you to stub out a method.  According
to the `(cdoc binding)`, one example is:

```clj
(defn mymax [x y]
  (min x y))

(defn find-max [x y]
  (max x y))

(binding [max mymax]
  (find-max 10 20))  ;; => 10
```

Unfortunately this doesn't work anymore.  When you run it, you'll get this
error:

```clj
user=> (binding [max mymax] (find-max 10 20))
IllegalStateException Can't dynamically bind non-dynamic var: clojure.core/max  clojure.lang.Var.pushThreadBindings (Var.java:353)
```

The only way to fix it is by defining the method as dynamic.

```clj
(defn ^:dynamic foo []
  (println "hello"))
```

I'm able to do this for my own code, but I haven't figured out how to alter the
meta data for an existing function, such as the `max` used in the example
above. 


-----------
Comment: you can do this for existing functions using `with-redefs`
