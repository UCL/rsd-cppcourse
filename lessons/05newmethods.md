---
title: Adding methods
---


Exercise: Adding new methods to Species
=======================================

##Introduction

So, we're trying to build up a program which can simulate mass-action chemical kinetics.

##Concentration

We're going to want our Species class to be able to have a concentration.

So the first exercise you will face will be to add a new data field (member variable) to Species to hold a concentration.

Think about which of the following types would be best to hold a concentration: `double, int, float, std::string`.

You'll want to add accessor methods: a getter method, like we had for the name, and, because we want the concentration to change, a setter method.

You'll want to add one or more new tests to SpeciesTest.cpp which check your new functionality is working.

Don't forget, as you make reasonable-sized changes to your code, to commit to version control.

##Comparing with my answers

Once you've finished, we can compare your work to my answers, and if you like, you can get hold of my own version and get rid of your own with a bit of git magic:

``` Bash
git checkout v1.1 .
```

This will be the case after all the exercises, we'll let you know the git tag (above [`1.1`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.1)) which solves each exercise.

Here is the comparison of what changed: [from v1.0 to v1.1](https://github.com/UCL/rsd-cppcourse-example/compare/v1.0...v1.1)

##Rate of Change

There's another piece of information we're going to want to add to Species: a knowledge of the rate of change of the species.

Obviously we'll want a getter method and a new member variable again.

However, in this case, instead of a setter method, you should add a method to contribute a certain amount to the rate of change, adding or subtracting to the rate.
Later, we'll call this as we work out the rate of each reaction.

We'll also want a reset method to zero the reaction rate, so we can start a new adding-up of the fluxes from each reaction at a different time step.

And we'll want some more tests: for example, I have a test called `CanContributeToSpeciesRateOfChange`.

##Comparing with my answers

My solution here is tag [`v1.2`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.2)

Have a look at the [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.1...v1.2)
