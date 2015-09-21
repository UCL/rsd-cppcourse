---
title: Main Program
---

The main program
================

##Introduction

Have a look at the [reactor.cpp](https://github.com/UCL/rsd-cppcourse-example/blob/master/reactor/reactor.cpp)
file in your editor. You will see comments which explain some of what this file does.

##Including libraries or other source files.

In C++ there is a powerful *standard library*: we include things from the standard library with angle brackets:

``` cpp
#include <iostream>
```

We include our own local other code with quotes:

``` cpp
#include "Species.h"
```

##The main function

Every program must have one, called main.

In C++, you declare a function like this:

``` cpp
returntype functionname(argumenttype1 argument1, argumenttype2 argument2)
{
	functionbody;
}
```

If you are of a computer-science type mindset, you might now be wanting to see the above syntax rule written
in a more formal way. Unfortunately for you, this is not that kind of course.

The arguments to the main function are special: they are how the command line arguments get into the program.

##Types

C++ is a *strongly typed* language.
There are types like `int` for an integer, and `char` for a letter. Unlike most other languages you probably know,
you have to explicitly tell the compiler what kind of thing each variable is, and which kind of thing each
function returns. You do this by liberally sprinkling the names of types throughout your code.

##Declaring types

When we create a new variable, we have to specify it's type, and you can't just use a variable without doing so.

Hence the line

``` cpp
reactor::Species calcium("Ca");
```

The syntax here is:

``` cpp
nameoftype variablename(initialisation_arguments);
```

##Homemade types: Classes

Note that the type here *Species* is a type we've invented for ourselves. From the other languages you know,
you may be more familiar with types like string, integer, or boolean. C++ has those too, but in C++,
we spend most of our time working with types we define ourselves: **classes**.

##Initialisers

The intialisation arguments can be optional, depending on the type of thing you're declaring, and there
are a few different styles to choose from, so you can write:

``` cpp
int five(5); // Create an integer variable called five, intialised to 5.

int six; // Create an integer variable called six, don't initialise.
six=6; // Set it to six.

int seven = 7; // Create an integer variable called seven, put 7 in it.

```

to declare integer variables.

##Semicolons

In C++, every line has to end with a semicolon. This is because in C++, the amount of spaces, new lines, tabs and so on
have no meaning. You can arrange your code within the file completely as you like, breaking up lines freely.
A "line" of code is something that ends at a semicolon.


##Braces

Sections of code, such as the innards of functions, or sections controlled by `if` or `for` statements
are shown with braces {}.

``` cpp
if (do_this_code) {
	// Only do this code if do_this_code is true
}
```

## Coding conventions

Again, there are no rules at all as to how your braces are laid out.

You can write

``` cpp
int
main( int argc, char**
         argv) {
std::cout
<< "Hello world" << std::endl
; }
```

Instead of:

``` cpp
int main( int argc, char** argv)
{
    std::cout << "Hello world" << std::endl;
}
```

if you really want to.

But **don't** because one is much easier to read!
