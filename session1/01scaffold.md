Obtaining the Scaffold Code
=================================

All languages have an unfortunate tendency to something called "boiler plate" code: 
code that you have to type in to make a bare-minimum program. Some have more, and some have less.

We have prepared basic boiler plate or "scaffold"
code, so you do not have to type it from scratch. You should obtain this code from GitHub.

To do this, first, go to https://github.com/UCL/rsd-cppcourse-example and hit the *fork* button top right, to make a copy of the code into your own account
on GitHub. You should make sure you are logged in to your own GitHub account. If you don't have one, sign up.

Now, you should clone your repository. Find an appropriate place to work on your computer, with something similar to

``` Bash
cd my_development_folder
git clone git@github.com:myusername/rsd-cppcourse-example.git
cd rsd-cppcourse-example
```

replacing *myusername* with your GitHub user name.

If this proceeds without error, you're almost good to go. But you should make sure you have a copy of our reference trainer answers.

``` Bash
git checkout -b answers origin/answers
ls # Wow, you can see all the answers!
git checkout master
```

In this first session, we're going to work slowly through the contents of this 'boiler plate' code, and see
what we can learn about C++ from it. Don't worry about not understanding everything in the
scaffold files at first, some of it is very complicated. But eventually, it should all make sense.

Later, we'll show you how to copy work from the answers branch into your own work, so that you can catch up if you get stuck.

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

C++ is a **compiled language** : you cannot just 'run' the source code: you must tell the computer to *build*
the source code into an *executable* which you run. Many bugs in your program will show up when you try to do this: the 
*compiler* cannot compile buggy code. There's a lot of subtlety to the build process: *compiling* and *linking*. We will not go
into the messy details of this in this course.

Most C++ courses start with directly using the compiler to compile a hello world file:

``` C++
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

However, this is misleading: directly using the compiler without a build tool will eventually become too difficult and cause a mess.
Therefore, we are starting you off with a working scaffold, using the build tool **CMake** which hides a lot of the complexity of the compiling and linking process. 
Our instructions on how to build the program are described in the file CMakeLists.txt, which we will look at later.

Type:

``` Bash
cd build
cmake ..
make
ls
./reactor
```


The CMakeLists.txt build tool files
-----------------------------------

Let's have a brief look at the top-level CMakeLists.txt file, which tells CMake how to build our program.

There's a lot of tedious stuff here, defining our executable, linking to lower level CMakeLists.txt files which
define our tests and libraries, and downloading the Google C++ Testing framework from the internet.

If we look at the lower level `reactor/CMakeLists.txt` file we can see this line:

``` CMake
add_library(reactor_library Species.cpp)
```

which specifies the source files which go into our library. If we want to add other files,
we will need to tell CMake:

``` CMake
add_library(reactor_library ReactionSystem.cpp Reaction.cpp Species.cpp)
```

Continue to the [next section](02mainprogram.md)
