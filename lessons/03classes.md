---
title: Your first Class
---


An introduction to simple classes
=================================

##Introduction

Here we'll look in more detail at defining a user-defined type, or Class.
We'll see that we need to specify two things: how other sections of the code will interact with the class, which we call the *interface*,
and the internals of how the class works, which we call the *implementation*.

##Header files

Have a look in your editor at [src/Species.h](https://github.com/UCL/rsd-cppcourse-example/blob/master/reactor/src/Species.h)

First of all, this file has a file extension ".h".

C++ and C source files come in two flavours: header files and non-header files.

We use .h files to describe the **interfaces** to things, what they are capable of, and .cpp files to actually define how they do it, the **implementation**.

##The species header file

So we can describe, in src/Species.h, that our user-defined type, or *class*, called Species,
exists, and that it has a *member function* called GetName():

``` cpp
class Species // A "class" is a user defined type with built-in functions
{   
  std::string GetName(); // declare a member function that
                         //takes no arguments, and returns a string.
};
```

Here, `std::string` refers to the string type, which is not a part of the C++ language itself, but is part of the
standard library. `std::` is used to refer to things from the standard library.

Calling a method
----------------

Because we've done this, when we have our reaction system, we can ask it for it's name:

``` cpp
calcium.GetName();
```

note the dot operator is used to get access to the method of the reaction system. We refer to functions which are part of a
class's abilities like this as *member functions* or *methods*.

Object-based programming
------------------------

Defining of user-defined types which contain their own custom built-in methods, defines the
basics of "object" based programming. It is the user-defined type which is called a class. Any particular *instance*
of the class is refered to as an *object*.

Constructors
------------

We note also that we define a function called the same as the name of the class:

``` cpp
Species(std::string input_name);
```

This describes a special function called a *constructor* which is used by the
language for making new Species. We invoked
it in the main function when we said:

``` cpp
Species calcium("Ca");
```

Member variables
----------------

We also define that the class has a member *variable* as well as member functions, to store the name:

``` cpp
class Species
{   
private:
  std::string name;
}
```

Privacy
-------

In principle, we could access this directly with a dot in outer code:

``` cpp
std::cout << calcium.name << std::endl;
// Instead of:
std::cout << calcium.GetName() << std::endl;
```

however, we might in future change the way the name of a system is stored, so it is traditional good practice
never to directly access member variables. We *enforce* that the user of our class doesn't try this with `private`.

If we try this, we get an error message on compiling with `make`:

> ```
> /Users/jamespjh/devel/rsdt/
>     rsd-cppcourse-example/reactor/reactor.cpp:15:126:
> error: 'name' is a private member of 'Species'
> ```

##Name collisions

When you are working with other people's code, it can be very very annoying if they have a class called Solver or some other common name,
and so do you. Your code is working fine, you bring in their library, and suddenly there's a bug because you're both using something with the same name.

##Namespaces

To get around this problem C++ allows `namespaces`. Something in a namespace must be referenced with the name preceding it like we saw in the main program:

``` cpp
reactor::Species myspecies;
```

We can surround a section of code with a namespace declaration, as we do in Species.h:

``` cpp
namespace reactor
{
  class Species
  {
  	...
  }
}
```

Everything declared inside the namespace declaration becomes part of the namespace, and it is not necessary to explitly reference it with a `namespace::` declaration.

Importing namespaces
--------------------

Finally, as in our [test files](https://github.com/UCL/rsd-cppcourse-example/blob/master/reactor/test/SpeciesTest.cpp),
you can simply import everything from a namespace into another one, including the default global namespace:

``` cpp
	using namespace reactor;
```

In `std::string` we're referencing `string` from the `std` namespace.

Some programmers just import the `std` namespace with

``` cpp
  using namespace std;
```

I recommend against that practice: in general it's better to spend a few extra characters for more clarity. There is a saying for this "explicit is better than implicit."

##Accessors

We can now look at the implementation of these methods in [`species.cpp`](https://github.com/UCL/rsd-cppcourse-example/blob/master/reactor/src/Species.cpp):

``` cpp
std::string reactor::Species::GetName()
{
	return name;
}
```

which obviously just returns the current stored value. What is the point of this?
We've gone to all that trouble to hide the data as `private` and now we're just writing a function which returns that value.
This is considered best practice because the way we store the name might change: for example, we might have short and long names.
We would like to change the internals of the class more often than we change the interface, so we use *accessor methods* like these.

Defining Constructors
---------------------

Now, the constructor could be defined as:

``` cpp
reactor::Species::Species(std::string input_name)
{
        name = input_name;
}
```

in fact we do something different:

``` cpp
reactor::Species::Species(std::string input_name)
         : name(input_name)
{
}
```

which means **exactly** the same thing: it's so common for constructors just to boringly pass on arguments like this,
that the language designers created a shortcut, called an initialiser-list. (We call this "syntactic sugar"!)

Constructor name overlap
------------------------

Where no confusion can occur, if using an initialiser-list, the standard even allows constructor arguments and member data to have the same name, so we could have written:

``` cpp
reactor::Species::Species(std::string name)
         : name(name)
{
}
```

##Double-definition danger

If we accidentally include two classes which both include the same class, we can get confused because the header definition will be included twice.
To get around this problem, we use something called a "once guard".

##Macros

The C++ compiler recognises something called "macros": an old-fashioned way of defining symbols like this:

``` cpp
#define PI 3.141 // Macro: not recommended
const double pi=3.141 // Better, use C++ const
```

We won't use macros in this course, except for one thing: to avoid double-compilation of headers.

##Conditional compilation

We can use a `#ifdef` or `#ifndef` statement to produces "conditional compilation", where code is only compiled if a given macro has not been defined:

``` cpp
#ifndef FOO
// only do this code if the macro FOO has not been defined
#endif
```

##Once guards

With the definition of the macro inside the conditional block, we get a piece of code which is guaranteed to be compiled only once per "compilation unit":

``` cpp
#ifndef ONCE_FILE_NAME
#define ONCE_FILE_NAME
// Code here safe from multiple compilation
#endif // ONCE_FILE_NAME
```

##Qualified Types

Our example files contain types like:

``` cpp
const std::string &
```

What in the world is this all about?

##Why be const-correct?

We like to specify at in our code which variables should be changed by a function, and which will not.

That way, the compiler will complain if we try to change
a variable which we should not, which will help prevent us from creating bugs.

In addition, knowing which methods can and cannot change variables can help
the compiler create much more efficient machine code.

##Const variables

Therefore, whenever we declare a variable which we guarantee will not change, we can specify `const` as part of the type:

``` cpp
const int x=1;
const double y=2.3;
const Species somespecies=GetSpecies();
```

That means that in this function, the variable will not be changed.

##Const methods

We can also say that a whole *method* doesn't change any of the variables
of the class, by writing `const` *after* the name of the method:

``` cpp
bool TellMeAboutTheObject() const;
```

##An early look at references

When we create a method, by default, the variables will be copied into new memory spaces for the new subroutine.
Compilers are quite good at realising when this is unnecessary, but we can make this specific by writing an & as the last symbol of the type:

``` cpp
double &reference_to_x=x;
```

This means that the new
variable is really just a reference to another one.

We will look at this much more in next week's session.
