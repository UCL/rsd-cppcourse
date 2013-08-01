Scaffold Code
=============

All languages have an unfortunate tendency to something called "boiler plate" code: 
code that you have to type in to make a bare-minimum program. Some have more, and some have less.

In the repository that you checked out in preparing for the course, we have given you basic boiler plate or "scaffold"
code, so you do not have to type it from scratch.

It would be very boring and confusing to explain every detail of the scaffold now, but there are a few things worth noting:

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
*compiler* cannot compile buggy code. There's a lot of subtlety to the build process: *compiling* and *linking* code
which, to be expert in C++, you will eventually need to understand. To see the full horror of this, try typing:

``` Bash
c++ --help
```

Fortunately, we do not have to get to grips with all this now. For this course, we'll be using **CMake** a *build tool*
which hides a lot of the complexity of the compiling and linking process. In your editor, have a look at the 
CMakeLists.txt file in the repository. You will see comments which explain some of what this file does.


The main program
----------------

Have a look at the src/main.cpp file in your editor. You will see comments which explain some of what this file does.

###There is a line which "includes" a library.

In C++ there is a powerful *standard library*: we include things from the standard library with angle brackets:

``` c++
#include <iostream>
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

The arguments to the main function are special: they are how the command line arguments get into the program.

###There are **types** everywhere

C++ is a *strongly typed* language. This will be a major part of what we learn this session. 
There are types like *int* for an integer, and *char* for a letter. Unlike most other languages you probably know, 
you have to explicitly tell the compiler what kind of thing each variable is, and which kind of thing each
function returns. You do this by liberally sprinkling the names of types throughout your code.

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

if you really want to. (But don't because one is much easier to read!)



