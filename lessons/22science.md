---
title: Completing the model
---

Adding science to the reaction system
=====================================

Adding science to the reaction system
-------------------------------------

We're going to add all the rest of the methods we need to use the reaction system as a set of ordinary differential equations.

Looping over reactions
----------------------

Add a method which when called:

* Resets the rate of change of each species to zero.
* Asks each reaction to contribute to the rate of change of all its participating species.
* Returns the resulting vector of rates of change

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.6...v2.7) is [`v2.7`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.7/reactor/src/ReactionSystem.h)

Accessing all the concentrations in one go
-------------------------------------------

Add a method which when called returns a vector of the concentrations of all species.

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.7...v2.8) is [`v2.8`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.8/reactor/src/ReactionSystem.h)

Changing all the concentrations in one go
-----------------------------------------

Add another method which when called with a container of concentrations, sets the concentration of each species.

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v2.8...v2.9) is [`v2.9`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.9/reactor/src/ReactionSystem.h)
