Exercise: An outputter for reactions
------------------------------------

We would like to be able to write an output method for our Reaction class, so that we can write:

``` cpp
std::cout << myreaction << std::endl;
```

which can be very useful when debugging!

We'll need to add a declaration to the header file:

``` cpp
std::ostream & operator<<(std::ostream &s, const reactor::ReactionSystem& system);
```

and in the implementation file, we'll need to write something to appropriately print each reactant, each product, and the rate.

We'll also need a new test.

You'll find our solution tagged as v2.0.

