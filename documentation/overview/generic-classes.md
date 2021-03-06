---
layout: page
title: Generic Classes
tutorial: scala-tour
num: 17
tutorial-next: variances
tutorial-previous: sequence-comprehensions
---

Scala has built-in support for classes parameterized with types. Such generic classes are particularly useful for the development of collection classes.
Here is an example which demonstrates this:

    class Stack[T] {
      var elems: List[T] = Nil
      def push(x: T) { elems = x :: elems }
      def top: T = elems.head
      def pop() { elems = elems.tail }
    }

Class `Stack` models imperative (mutable) stacks of an arbitrary element type `T`. The type parameters enforces that only legal elements (that are of type `T`) are pushed onto the stack. Similarly, with type parameters we can express that method `top` will only yield elements of the given type.

Here are some usage examples:

    object GenericsTest extends App {
      val stack = new Stack[Int]
      stack.push(1)
      stack.push('a')
      println(stack.top)
      stack.pop()
      println(stack.top)
    }

The output of this program will be:

    97
    1

_Note: subtyping of generic types is *invariant*. This means that if we have a stack of characters of type `Stack[Char]` then it cannot be used as an integer stack of type `Stack[Int]`. This would be unsound because it would enable us to enter true integers into the character stack. To conclude, `Stack[T]` is only a subtype of `Stack[S]` if and only if `S = T`. Since this can be quite restrictive, Scala offers [variance annotations](variance) to control the subtyping behavior of generic types._
