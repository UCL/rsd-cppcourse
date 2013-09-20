Scaffold Code
=============

Boiler-Plate
------------

All languages have an unfortunate tendency to something called "boiler plate" code: 
code that you have to type in to make a bare-minimum program. Some have more, and some have less.

We have prepared basic boiler plate or "scaffold"
code, so you do not have to type it from scratch. 

You should have obtained this code during the introduction.

## Session objectives

In this first session, we're going to work slowly through the contents of this 'boiler plate' code, and see
what we can learn about C++ from it. 

Don't worry about not understanding everything in the
scaffold files at first, some of it is very complicated. But eventually, it should all make sense.

##Repository Layout

``` Bash
cd reactor
ls
```

* There is a folder called `src` which will contain all of the actual code for the project we are going to write
* There is a folder called `test` which will contain all of the tests for our project.
* There is a folder called `build` which will contain the executable program we will run.

It is important, when starting any project, to set up a good structure for your code: 
to keep the different bits of the code separate.

##Executables, source files, and build tools

C++ is a **compiled language** : you cannot just 'run' the source code: you must tell the computer to *build*
the source code into an *executable* which you run. 

Many bugs in your program will show up when you try to do this: the 
*compiler* cannot compile buggy code. 

There's a lot of subtlety to the build process: *compiling* and *linking*. We will not go
into the messy details of this in this course.

## Hello world

Most C++ courses start with directly using the compiler to compile a hello world file:

``` cpp
#include <iostream>
int main(int argc, char** argv){
	std::cout << "Hello world!" << std::endl;
}
```
``` Bash
g++ hello_world.cpp
./a.out
  #Hello World!
```

## Goodbye, cruel world.

However, this is misleading: directly using the compiler without a build tool will eventually become too difficult and cause a mess.

## Using CMake

Therefore, we are starting you off with a working scaffold, using the build tool **CMake** which hides a lot of the complexity of the compiling and linking process.

Our instructions on how to build the program are described in the file CMakeLists.txt, which we will look at later.

## Building with CMake

Type:

``` Bash
cd build
cmake ..
make
ls
./reactor
```

##The CMakeLists.txt build tool files

In the scaffold code, have a brief look at the top-level CMakeLists.txt file, which tells CMake how to build our program.

There's a lot of tedious stuff here, defining our executable, linking to lower level CMakeLists.txt files which
define our tests and libraries, and downloading the Google C++ Testing framework from the internet.

##Defining a library with CMake

If we look at the lower level `reactor/CMakeLists.txt` file we can see this line:

``` CMake
add_library(reactor_library Species.cpp)
```

which specifies the source files which go into our library. If we want to add other files,
we will need to tell CMake:

``` CMake
add_library(reactor_library ReactionSystem.cpp Reaction.cpp Species.cpp)
```
