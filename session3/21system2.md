
Adding science to the reaction system
=====================================

We're going to add all the rest of the methods we need to use the reaction system as a set of ordinary differential equations.

Add a method which when called:

* Resets the rate of change of each species to zero.
* Asks each reaction to contribute to the rate of change of all it's participating species.

Add a method which when called return a vector of the rates of change of all species, and another which returns a vector of the concentrations of all species.

Add another method which when called with a container of concentrations, sets the concentration of each species.

Each of these methods should have good tests.

Our solution is v2.2

Now we need to actually solve the system of ODEs. We'll use an [external library](22boost.md) to do this.