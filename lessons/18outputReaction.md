---
title: Reaction output
---

Exercise: An outputter for reactions
====================================

An outputter for reactions
--------------------------

We would like to be able to write an output method for our Reaction class, so that we can write:

``` cpp
std::cout << myreaction << std::endl;
```

which can be very useful when debugging!

We'll need to add a declaration to the header file:

``` cpp
std::ostream & operator<<(std::ostream &s, const reactor::Reaction& reaction);
```

and in the implementation file, we'll need to write something to appropriately print each reactant, each product, and the rate.

We'll also need a new test.

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v1.9...v2.0) is [`v2.0`](https://github.com/UCL/rsd-cppcourse-example/tree/v2.0)
