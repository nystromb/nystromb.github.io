---
layout: post
title:  "Functional vs Imperative Programming"
date:  January 21th, 2016
blog: true
---

Recently I have been introduced to the crazy world of the functional programming by learning Clojure. Speaking as someone who has mainly a Java background, I naturally like to write programs in an Object Oriented way, by creating mutable objects with classes. However, once I began writing programs in Clojure, this imperative way of thinking has pretty much gone completely out the window.

In Object Oriented programming languages, you will have classes that have data fields, and you will modify that data fields using methods that the classes define. Functional languages work a little different, by the fact that they generally avoid containing immutable data and operate by performing mathematical transformations on data. This means that you don't really make variable assignments to data or have `while` or `for` loops like you would in an imperative style language. This makes functional languages good for concurrent systems.

Learning to think in a "functional" way might take some getting used to, but after spending some time learning Clojure, I'm starting to force myself to approach problems a little differently. In the functional paradigm everything is essentially a ...function, and every expression has a return value. For example, if you write a function that adds up all the numbers up to a given number n in both an imperative and a functional program, you'll notice some interesting differences.

    (defn add-up-to [n]
      (reduce + (range n)))

    user=> (add-up-to 3)
    3

To do the same thing in Java, you would do something like this:

    public int addUpTo(int num) {
      int sum = 0;

      for (int i = 0; i < num; i++) {
        sum += i;
      }

      return sum;
    }

    System.out.println(addUpTo(3))
    => 3

You'll notice that in the Java example, you must set the variables `sum` and `i` in order to loop through the given number. On the other hand, in the Clojure example, you'll see that it is short and seemingly simple, but I'll explain a bit of whats happening there anyway. First you'll probably notice all the parentheses, but this just basically says in what order things are evaluated in. In this function, you pass in a number, and based on that it returns the sum of every number up to that number. In order to do this, it uses 3 functions: `range`, `reduce`, and `+`. First it will get a list of ranges from in, like so:

    user=> (range 3)
    (0 1 2)

Then it will use a reduce function, which takes two parameters, a function and a collection. So I pass it the `+` function and a range of values `(0 1 2)` and uses the `+` on each of those numbers and returns the result of applying + to every number in the list.

This is a pretty basic example, but the example highlights some of the main differences of both of these programming paradigms. In one example, you don't save any data, just input -> transform -> output, while the other was longer and had stored some variables. It's long debated whether one is better than the other, but I think they have their specific applications, and you should use the right tool for the job. However, one of the best things about the beauty of Clojure is that it allows for Java interop. That means the Clojure can actually use Java classes to perform functions. This makes for a extremely powerful functional language.
