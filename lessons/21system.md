---
title: Factory Class
---

A factory class
===============

The reaction system can create species
--------------------------------------

We should upgrade our reaction system class so that it can create and own species, not just store pointers to them.

When a new species is to be created, you should pass the necessary data into the system, not the species itself.

You can get rid of the method allowing a reaction system to store pointers to species.

The species should be created on the heap and appended to the container. A pointer or reference to the newly created species should be returned
so the calling class can use the species. Thus, the ReactionSystem acts
as a factory for Species.

Hint: Example client code.
--------------------------

Client code should look something like:

``` cpp
ReactionSystem myReactionSystem;

Species * h= myReactionSystem.NewSpecies("H")),
Species * o= myReactionSystem.NewSpecies("O")),
Species * w= myReactionSystem.NewSpecies("Water")),
```

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.3...v2.4) is [`v2.4`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.4/reactor/src/ReactionSystem.h)

The reaction system can create reactions
----------------------------------------

Similarly, it should be possible to create a new, empty reaction, with the reaction allocated on the heap, and a pointer to the new reaction returned,
so that species can be added to its reactants and products.

Once you're done, client code should look like this:

``` cpp
Reaction * r1= myReactionSystem.NewReaction(9.0);
Species * h= myReactionSystem.NewSpecies("H")),
Species * o= myReactionSystem.NewSpecies("O")),
Species * w= myReactionSystem.NewSpecies("Water")),
r1.AddReactant(h);
r1.AddReactant(h); // Include Hydrogen twice for stoichiometry
r1.AddReactant(o);
r1.AddProduct(w);
```

Don't forget to add tests.
The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.4...v2.5) is [`v2.5`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.5/reactor/src/ReactionSystem.h)

Keeping memory clean
------------------

Add a destructor, which `deletes` the allocated memory.

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.5...v2.6) is [`v2.6`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.6/reactor/src/ReactionSystem.h)
