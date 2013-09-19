A reaction system
=================

A reaction system is a system of several reactions.

Create a new ReactionSystem class, with all new boilerplate code, and a new test file.

This should have a container of reactions, and containers of species, with ways of adding new species, and adding new reactions.

When a new species is to be created, you should pass the necessary data into the system, not the species itself.
The species should be created on the heap and appended to the container. A pointer or reference to the newly created species should be returned
so the calling class can use the species. It should be cleaned up in a destructor method for the ReactionSystem. Thus, the ReactionSystem acts
as a factory for Species.

Similarly, it should be possible to create a new, empty reaction, with the reaction allocated on the heap, and a pointer to the new reaction returned,
so that species can be added to it's reactants and products.

Client code should look something like:

```C++
ReactionSystem myReactionSystem;

Reaction * r1= myReactionSystem.NewReaction(9.0);
Species * h= myReactionSystem.NewSpecies("H")),
Species * o= myReactionSystem.NewSpecies("O")),
Species * w= myReactionSystem.NewSpecies("Water")),

r1.AddReactant(h);
r1.AddReactant(h); // Include Hydrogen twice for stoichiometry
r1.AddReactant(o);
r1.AddProduct(w);
```

You should of course add appropriate new tests to check this machinery is working.

Our solution is v2.1

Now it's time to finish off the science, and tell the system how to [add up the rates](21system2.md)