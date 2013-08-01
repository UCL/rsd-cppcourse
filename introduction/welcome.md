Intensive C++ for Research
==========================

Welcome to the first of the new UCL Research IT training courses: ``Intensive C++ for Research''.

What this course is and is not.
------------------------

This course is not:

* An introduction to programming: you are assumed to be already able to program in some language.
* A comprehensive introduction to C++ syntax: we will introduce the language ad-hoc as we progress.
* A gentle course: the course is intensive, and assumes a highly intelligent trainee with the willingness to commit time to the learning process.
* A software engineering course: while we will touch on some aspects of good software engineering practice, this will not be the focus.

This course is:

* Primarily intended for quantitative scientists: the focus and examples will emphasise numerical aspects.
* Interactive: by following the examples, you will have constructed for yourself a working C++ program capable of real science.
* Short: a good student should be able to work through all the material in around 25 hours.
* Selective: we will touch on only a tiny fraction of what C++ offers.

Prerequisites
-------------

In order to follow this course, you should at minimum already know:

* How to program in some language, (such as Basic, Python, Ruby, MATLAB, or FORTRAN) including:
  * Variables including arrays or vectors
  * For and while loops
  * If statements and case switches
  * Functions and/or procedures
* How to edit program files in a text editor
* How to create and delete files and folders (directories) using a unix command line.

In the [syntax appendix](../appendices/syntax.md) we give simple look-up translations to find the C++ syntax
in terms of the language you already know. You should use this as we go along, in order to answer questions such as

> I know that in Python, I make an array with [1,2,3], but how do I write that in C++?

In addition, it will make the course easier for you if you
also already have experience of the following, though we will introduce 
the basics of these during this course, so these are not an absolute prerequisite:

* Version control (in git, mercurial, or subversion)
* Unit testing
* Build tools (such as make, scons or cmake)

In order to meet these prerequisites, you could attend a [Software Carpentry](http://softwarecarpentry.org) course, 
which are offered regularly around the world.

How to follow the course
------------------------

First, follow the instructions listed in [preparing for the course](../appendices/preparation.md).

The course is divided into five sessions, each of which will be one afternoon's training when delivered in person.
These can be followed on line, without a hands-on-trainer. If you run into any problems, 
please [raise an issue in the GitHub repository](https://github.com/UCL/rsd-cppcourse/issues) or email us at rc-softdev@ucl.ac.uk.

In each section, code you should be adding into your example will be shown like this:

*filename.cpp*:

``` c++
std::cout << "Hello world" << std::endl;
```

You should have the code you are working on open in your editor of choice, and be ready to edit it.

Occasionally we will show changes you should make to a file like this:

*filename.cpp*:

``` Diff
+Line to be added
Unchanged line
-Line to be taken away
```

We will show commands you should type in your command line like this:

*Type:*

``` Bash
cd build
cmake ..
make
```

You should have a terminal open and ready for this, and should be ``standing'' in the directory where you have
obtained the starting course materials, as explained in [preparing for the course](../appendices/preparation.md).

So, you should now be ready to go to the [first section](../session1/) of the first chapter, and begin
