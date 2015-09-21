---
title: Refactoring to Pointers
---


Exercise: Rewriting Reaction To Use Pointers
============================================

Using pointers
--------------

So, our next exercise is to rewrite the Reaction class to use `vector<Species *>` not `vector<Species>`.

We'll need to change our loop-over reactants in calculating the flux, ensure we `push_back` pointers onto the `vector`s.
We'll need a new test to ensure that we really are referring to the original species, something like:

``` cpp
EXPECT_EQ(something.GetReactants()[0], &calcium);
```

Our solution for this exercise is tagged as [`v1.8`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.8)

Have a look at my [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.7...v1.8)
