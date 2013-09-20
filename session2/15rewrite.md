Exercise: Rewriting Reaction To Use Pointers
============================================

Using pointers
--------------

So, our next exercise is to rewrite the Reaction class to use vector<Species *> not vector<Species>.

We'll need to change our loop-over reactants in calculating the flux, ensure we `push_back` pointers onto the `vector`s.
We'll need a new test to ensure that we really are referring to the original species, something like:

``` cpp
EXPECT_EQ(something.GetReactants()[0], &calcium);
```

Our solution is tagged as `v1.8`
