Scaffold Code
=============

All languages have an unfortunate tendency to something called "boiler plate" code: 
code that you have to type in to make a bare-minimum program. Some have more, and some have less.

In the repository that you checked out in preparing for the course, we have given you basic boiler plate or "scaffold"
code, so you do not have to type it from scratch.

In this first session, we're going to work slowly through the contents of this 'boiler plate' code, and see
what we can learn about C++ from it. Don't worry about not understanding everything in the
scaffold files at first, some of it is very complicated. But eventually, it should all make sense.

Repository Layout
-----------------

Type:

``` Bash
cd reactor
ls
```

1. There is a folder called "src" which will contain all of the actual code for the project we are going to write
2. There is a folder called "test" which will contain all of the tests for our project.
3. There is a folder called "build" which will contain the executable program we will run.

It is important, when starting any project, to set up a good structure for your code: 
to keep the different bits of the code separate.

Executables, source files, and build tools
------------------------------------------

Type:

``` Bash
cd build
cmake ..
make
ls
./reactor
```

C++ is a **compiled language** : you cannot just 'run' the source code: you must tell the computer to *build*
the source code into an *executable* which you run. 

Many bugs in your program will show up when you try to do this: the 
*compiler* cannot compile buggy code. There's a lot of subtlety to the build process: *compiling* and *linking*.

Fortunately, we do not have to get to grips with all this now. For this course, we'll be using **CMake** a *build tool*
which hides a lot of the complexity of the compiling and linking process. Our instructions on how to
build the program are described in the file CMakeLists.txt, which we will look at later.


The main program
----------------

Have a look at the reactor.cpp file in your editor. You will see comments which explain some of what this file does.

###There are lines which "include" libraries or other source files.

In C++ there is a powerful *standard library*: we include things from the standard library with angle brackets:

``` c++
#include <iostream>
```

We include our own local other code with quotes:

``` c++
#include "ReactionSystem.h"
```

###There is a main function

Every program must have one, called main.

In C++, you declare a function like this:

``` c++
returntype functionname(argumenttype1 argument1, argumenttype2 argument2... )
{
functionbody;
}
```

If you are of a computer-science type mindset, you might now be wanting to see the above syntax rule written 
in a more formal way. Unfortunately for you, this is not that kind of course.

The arguments to the main function are special: they are how the command line arguments get into the program.

###There are **types** everywhere

C++ is a *strongly typed* language. This will be a major part of what we learn this session. 
There are types like *int* for an integer, and *char* for a letter. Unlike most other languages you probably know, 
you have to explicitly tell the compiler what kind of thing each variable is, and which kind of thing each
function returns. You do this by liberally sprinkling the names of types throughout your code.

When we create a new variable, we have to specify it's type, and you can't just use a variable without doing so.

Hence the line

``` c++
ReactionSystem my_simple_reaction_system("Simple reaction system");
```

The syntax here is:

``` c++
nameoftype variablename(initialisation-arguments);
```

The intialisation arguments can be optional, depending on the type of thing you're declaring, and there
are a few different styles to choose from, so you can write:

``` c++
int five(5); // Create an integer variable called five, intialised to 5.

int six; // Create an integer variable called six, don't initialise.
six=6; // Set it to six.

int seven = 7; // Create an integer variable called seven, put 7 in it.

```

to declare an integer variables.

###There are plenty of semicolons and braces

In C++, every line has to end with a semicolon. This is because in C++, the amount of spaces, new lines, tabs and so on
have no meaning. You can arrange your code within the file completely as you like, breaking up lines freely.
A "line" of code is something that ends at a semicolon. Sections of code, such as the innards of functions,
are shown with braces {}. Again, there are no rules at all as to how your braces are laid out.

You can write

``` C++
int
main( int argc, char**
         argv) {
std::cout
<< "Hello world" << std::endl
; }
```

Instead of:

``` C++
int main( int argc, char** argv) 
{
    std::cout << "Hello world" << std::endl; 
}
```

if you really want to. (But don't because one is much easier to read! We always end lines at the end of a line,
and we always indent four spaces whenever we go inside a brace block, as a *coding convention*, not because we
have to.)

The reaction system header file
-------------------------------

Have a look in your editor at src/ReactionSystem.h

First of all, this file has a file extension ".h".

C++ and C source files come in two flavours: header files and non-header files.

We use .h files to describe the **interfaces** to things, and .cpp files to actually define what they do.

So we can describe, in src/ReactionSystem.h, that our user-defined type, or *class*, called ReactionSystem,
exists, and that it has a *member function* called GetName():

``` c++
class ReactionSystem // A "class" is a user defined type with built-in functions
{   
  std::string GetName(); // declare a member function takes no arguments, and returns a string.
};
```

because we've done this, when we have our reaction system, we can ask it for it's name:

``` c++
my_simple_reaction_system.GetName();
```

note the dot operator is used to get access to the method of the reaction system.

This, the defining of user-defined types which contain their own custom built-in functions, defines the
basics of "object" based programming. Such a user-defined type is called a class. We will talk more about the basics
of classes later in the session.

The reaction system test file
-----------------------------

When we program, we want to know that our code works as expected.

Newer programmers tend to do this in an ad-hoc fashion, working with a main program that they thing should work, and
inspecting the output to check things are OK. A better way, however, is to write *automated tests*, small pieces of
code which verify each subroutine or class does what is expected. We write many such small tests, and keep running them
whenever we make a change. That way, we can be sure that our new changes haven't broken old functionality.

Look at the file test/ReactionSystemTest.cpp:

``` c++
// Test that the system has a name as expected.
TEST(ReactionSystemTest, SystemHasAName) { // First argument is test group, second is test name
  ReactionSystem mySystem("SomeName"); // Create a reaction system with a specified name
  EXPECT_EQ("SomeName", mySystem.GetName()); // Assert that the name should be as expected
}
```

Here we define an *expectation*: something which should be true, in this case, that the system name should be as defined.

You can run this test with

``` bash
ctest
```

and should see:

> Running tests...
> Test project /Users/jamespjh/devel/rsdt/rsd-cppcourse-example/reactor/build
>     Start 1: ReactionSystemTest
> 1/1 Test #1: ReactionSystemTest ...............   Passed    0.02 sec
> 
> 100% tests passed, 0 tests failed out of 1
> 
> Total Test time (real) =   0.02 sec

try modifying the test so it should fail:
``` Diff
- ReactionSystem mySystem("SomeName");
+ ReactionSystem mySystem("SomeOtherName");
```

``` bash
make
ctest
```

(Note that we needed to recompile with make, before rerunning the tests.)

> Running tests...
> Test project /Users/jamespjh/devel/rsdt/rsd-cppcourse-example/reactor/build
>    Start 1: ReactionSystemTest
> 1/1 Test #1: ReactionSystemTest ...............***Failed    0.01 sec
>
> 0% tests passed, 1 tests failed out of 1
> 
> Total Test time (real) =   0.02 sec
>
> The following tests FAILED:
>           1 - ReactionSystemTest (Failed)
> Errors while running CTest
> make: *** [test] Error 8

``` bash
ctest --output-on-failure
```

> /Users/jamespjh/devel/rsdt/rsd-cppcourse-example/reactor/test/ReactionSystemTest.cpp:7: Failure
> Value of: mySystem.GetName()
>  Actual: "SomeOtherName"
> Expected: "SomeName"

Note the difference between the *expected* and *actual* values.

Put your code back right again. (Use version control if you know how, or just edit it back.)

Note that in future, as we code, we will add new tests for our new functionality.
