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

Note that at various points in the development of the example, we have tagged in the version control repository you
checked out while preparing for the course, a version of the code which is our version of the code at that state.

You can abandon your own current work, and revert to our version, by typing:

``` Bash
git reset --hard <tag name>
```

Where *tag name* represents the version you want to switch to. If you are more experienced with version control, you
could even use these tags to merge our version into your own, resolving conflicts as appropriate.

The example problem
-------------------

In this course, we're going to build a complete program capable of simulating mass-action chemical kinetics.
We will define a file parser which loads files which specify several reactions, containing a variety of species.
We will implement code which calculates the rates of these reactions given their concentrations, according to the usual
mass-action rules. (Where the rate of the reaction is proportional to the concentrations of the reactants.)
We will use a library to numerically solve the resulting ordinary differential equations, and we will produce output
which can be plotted to show a graph of the concentrations as it proceeds.

If you're not a chemist, this is exactly the same mathematics which is often used to describe the variation of populations of competing species,
or many other kinds of problem. We've chosen this example because it's relevant to many different areas of research.

Let's start
-----------

So, you should now be ready to go to the [first section](../session1/) of the first chapter, and begin. The notes in
this document are not intended to be a comprehensive textbook. They are the tutor's notes for delivery of the course,
and are provided to trainees as an aide memoir. This is a practical course, and the purpose is to give trainees a
feel for the use of the language. You will want to supplement this treatment with a good textbook 
or [online tutorial](http://www.cplusplus.com/doc/tutorial/).
