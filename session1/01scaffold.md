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

