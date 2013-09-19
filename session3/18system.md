A reaction system
=================

A reaction system is a system of several reactions.

Use everything you have learned to create a new ReactionSystem class, with all new boilerplate code, and a new test file.

This should have a container of reactions, and containers of species, with ways of adding new species, and adding new reactions.

It should have a method which when called:

* Resets the rate of change of each species to zero.
* Asks each reaction to contribute to the rate of change of all it's participating species.

It should have a method which when called return a vector of the rates of change of all species, and another which returns a vector of the concentrations of all species.

It should have another method which when called with a container of concentrations, sets the concentration of each species.

Each of these methods should have good tests.