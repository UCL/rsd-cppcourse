Adding a new class
==================

We're going to add the class for the reaction.

So far, we don't want it to *do* anything, just to exist and be able to be instantiated.

To complete this exercise, you're going to have to copy Species boiler plate code, changing file, class, variable and method names as appropriate.

This exercise is tedious -- if you use an IDE such as Microsoft Visual C++ or Eclipse, that will be easier, but for this course we're doing without.

You'll need to create interface and implementation files for Reaction. You'll need a new test file, and you'll need to add to the relevant CMakeLists.txt files to tell the compiler
to compile these files.

The git tag for our solution to this exercise is v1.3.

Adding a Reaction Rate to the class
===================================

The class is going to need the ability to store a reaction rate, with a getter access method and ability to set the rate in the constructor. Add this with new tests.

The git tag for our solution to this exercise is v1.4.

Finally, have a look at some [new coding points](08fixtures.md) introduced in our solution for this exercise.