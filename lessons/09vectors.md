---
title: Vectors
---


Vectors
=======

Vectors
-------

To do this, we need some way for the reaction to keep a list of all the reactants and products it has. So we'll need some kind of array.

In C++, a `vector` works like this:

``` cpp
#include <vector> //Include the vector part of the standard library
std::vector<double> an_array(5); // argument here is the size,
							     // type in angle brackets.
EXPECT_EQ(5,an_array.size()); // Use size() to get the size of an array.

an_array[0]=2.5; // elements are indexed from zero ; here the last one is 4.
EXPECT_EQ(an_array[0],2.5);

std::vector<std::string> another_array(3,"hello"); // Second argument is
												   // the initial value
EXPECT_EQ("hello",another_array[2]);

std::vector<int> array3; // No arguments, initially empty
array3.push_back(1); // Can add to array at the end.
array3.push_back(2); // This can be slow-ish.
EXPECT_EQ(2,array3.size());
EXPECT_EQ(2,array3[1]);
```

Vectors as types
----------------

A vector is a proper type, and can be referenced like any other type.
Note that a `vector<int>` is a different type from a `vector<Species>`,
you can't set one from the other.

We call a type like this which is based on
another type a "template". We call a template type which is designed to store several other objects
a "container".

Other C++ standard library containers include `set`, `list`, and `map`.

Initialising vectors
--------------------

In order to initialise a vector with values, we have to add each value manually:

``` cpp
std::vector<int> array;
array.push_back(1);
array.push_back(2);
array.push_back(3);
```

However, if you have C++11, the latest version of C++, which in this course we're not assuming you do, you can write:

``` cpp
std::vector<int> x {1,2,3};
```
