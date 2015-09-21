---
title: Adding up the reaction rates
---

Exercise: Contributing to the species fluxes
============================================

Contributing to the species fluxes
----------------------------------

A reaction needs to be able to add it's flux to the rate-of-change of species: positive for products and negative for reactants.

Write a method in the Reaction class which iterates over all reactants and products, contributing to the fluxes appropriately, and
add some new tests to ensure it works.

Our solution for this exercise is tagged as [`v1.9`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.9)

Have a look at my [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.8...v1.9)

In the next session, we'll start to use some external libraries, so please install the C++ *boost* library before next time,
following the [instructions](99appendices/03install_boost.html).
