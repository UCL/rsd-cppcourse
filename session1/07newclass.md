Exercise: The reaction rate class
=================================

## Adding the new class

We're going to add the class to model reactions.

So far, we don't want it to *do* anything, just to exist and be able to be instantiated.

To complete this exercise, you're going to have to copy Species boiler plate code, changing file, class, variable and method names as appropriate.

This exercise is tedious -- if you use an IDE such as Microsoft Visual C++ or Eclipse, that will be easier, but for this course we're doing without.

You'll need to create interface and implementation files for Reaction. You'll need a new test file, and you'll need to add to the relevant CMakeLists.txt files to tell the compiler
to compile these files.

## Comparing with my answers

The git tag for our solution to this exercise is [`v1.3`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.3)

Have a look at my [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.2...v1.3)

## Adding a Reaction Rate to the class

The class is going to need the ability to store a reaction rate, with a getter access method and ability to set the rate in the constructor. Add this with new tests.

The git tag for our solution to this exercise is [`v1.4`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.4).

Have a look at my [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.3...f1494eb)
