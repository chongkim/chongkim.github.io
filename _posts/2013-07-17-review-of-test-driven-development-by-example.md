---
layout: post
title: Review of "Test-Driven Development By Example"
date: 2013-07-17 23:00:47
categories: update programming
---
The book is written in three parts

  * Part I: Money Example
  * Part II: The xUnit Example
  * Part III: Patterns for Test-Driven Development

The Money Example takes a simple problem of implementing other currencies into
a system that takes dollars.  It would make for a interesting kata and it's
something that should be seen, rather than read.  The idea follows the pattern

1. Quickly add a test.
2. Run all tests and see the new one fail.
3. Make a little change.
4. Run all tests and see them all succeed.
5. Refactor to remove duplication.

The problem is that it doesn't show you the errors, so it feels less like the
implementation is driven by the test.  It still feels like there is a lot of
planning ahead of time to get the test to pass.  For example, it implements
supporting code before it writes the code under test.  I would like to have
seen errors such as "class not defined" and "method not defined", etc...  When
you fix those problems, you get closer to a design, thus making it feel
"test-driven".  Much of the book is a description of what he's doing, it would
be better if I was watching a screencast with a voiceover explaining as he was
going along.

Another problem with this book is that since there is so many changes to the
code, you have a hard time knowing what is th current state of the code.  You
see snippets of the new code, so you have to go back to see what has changed.
A book is probably not the right format for this exposition.

The xUnit was very confusing.  I had a hard time following this section even
when I was writing code along with it.  The project he chose was to implement a
testing framework while using TDD.  It was difficult to know whether the method
he was writing was part of the test or was the subject of the test.  He had a
class called `WasRun`, which had a flag to see if the test was run, but it also
kept flags to see if things were set up.  The class name added to the
confusion. It wasn't clear which method `WasRun` was tracking. 

When I finished reading the xUnit section, I didn't leave it knowing any more
than the Money section.  I do have experience with TDD and I felt that the book
is a bit dated.  Reading `assertEquals(0, foo())` reminded me of times long
past where today I would see it as `foo().should == 0`.  If I had an array, I
would need to say `assertArrayEquals(expected, actual)` whereas `actual.should
== expected` reads better.  Using the "should" method makes it clear which is
the expected and which is the actual.  If I had said `assertEquals(x,y)`, it
isn't clear which is the expected and which is the actual.  You would have to
know the API to understand.  Getting it wrong can lead to misleading error
messages.  The "should" method allows many kinds of matchers such as
`foo().should be_nil`, `foo().should be_true`, `foo().should include([1,2,3])`,
and lets you define your own.

The third part of the book contained some useful information.  It mentions
Pluggable Object.  The idea being that if you have code that looks like

```java
public void mouseDown() {
  selected = findFigure()
  if (selected != null)
    select(selected);
}
public void mouseMove() {
  if (selected != null)
    move(selected);
  else
    moveSelectionRectangle();
}
public void mouseUp() {
  if (select != null)
    selectAll();
}
```

You can make it look like this:

```java
public void mouseDown() {
  selected = findFigure();
  if (selected != null)
    mode = SingleSelection(selected)
  else
    mode = MultipleSelection()
}
public void mouseMove() {
  mode.mouseMove();
}
public void mouseUp() {
  mode.mouseUp();
}
```

The point being that after the initial setup, the logic is simplified by
calling the appropriate method on the object and let the object handle the
event instead of having the logic in the event handler.  The code looks cleaner
because event code does not have magical `if` conditions making the programmer
wonder why there is a special case.  Moving the code around is much easier too
because you don't have to worry about bugs because you forgot to add that
special case.

A lot of the other patterns seems like common sense.  I've read "The RSpec
Book", which mentions BDD and TDD.  It does a better job of explaining the TDD
methodologies.  The TDD book was published in 2003.  I suppose at the time, it
was fresh and innovative, but after having spent some time with TDD as well as
tools more suitable for it (rather than xUnit), the book has shown its age.

