---
title: Course content
---

How to follow the Course
=========================

First, follow the provided [installation instructions](99appendices).

The course is offered occasionally as a hands-on course with an experienced research programmer as trainer.
It can also be followed on line, without a hands-on-trainer. If you run into any problems,
please [raise an issue in the GitHub repository](https://github.com/UCL/rsd-cppcourse/issues) or email us at rc-softdev@ucl.ac.uk.

Example Code
------------

Sometimes, we will show code directly in these notes.

Code you should be adding into your example will be shown like this:

``` cpp
std::cout << "Hello world" << std::endl;
// A comment
```

You should have the code you are working on open in your editor of choice, and be ready to edit it.

Showing differences
-------------------

Occasionally we will show changes you should make to a file like this:

``` Diff
+Line to be added
Unchanged line
-Line to be taken away
```

Showing command line commands
-----------------------------

We will show commands you should type in your command line like this:

``` Bash
cd build # A comment
cmake ..
make
```

Terminal output
---------------

We will show output which is expected from the terminal like this:

> ```
> Your program has worked.
> Well done.
> ```

Online example code for the course
-------------------------------

We have prepared a standard solution for our example problem, and
a scaffold for you to build your solution on.

The code for our solution, as we gradually build it up, is all online on [GitHub](https://github.com/UCL/rsd-cppcourse-example).

We will regularly link to a piece of our [finished code](https://github.com/UCL/rsd-cppcourse-example/tree/develop),
to a particular [version of it](https://github.com/UCL/rsd-cppcourse-example/tree/7e64eaf60e76980577049708fe00c9dfb3e9bb8b),
or to the [changes](https://github.com/UCL/rsd-cppcourse-example/commit/2bb59360f1744a8bc6f325288e91e260184a8c1e) we made in a particular piece of work.

As with local links in these course notes, links to changes show removed lines in red, and added lines in green.

The example problem
-------------------

In this course, we're going to build a complete program capable of simulating mass-action chemical kinetics.
We will define a file parser which loads files which specify several reactions, containing a variety of species.
We will implement code which calculates the rates of these reactions given their concentrations, according to the usual
mass-action rules. (Where the rate of the reaction is proportional to the concentrations of the reactants.)
We will use a library to numerically solve the resulting ordinary differential equations, and we will produce output
which can be plotted to show a graph of the concentrations as it proceeds.

The example problem: ecology edition
------------------------------------

If you're not a chemist, this is exactly the same mathematics which is often used to describe the variation of populations of competing species,
or many other kinds of problem. We've chosen this example because it's relevant to many different areas of research.



Fork the code on GitHub
-----------------------

As well as looking at our solutions online, you can grab your own copy.

This will allow you, if you fall behind in the exercises, to jump forward and build your next solution on top of our solution to the
previous exercise.

To do this, first, go to  [http://github.com/UCL/rsd-cppcourse-example] and hit the *fork* button top right, to make a copy of the code into your own account
on GitHub.

You should make sure you are logged in to your own GitHub account.
If you don't have one, [sign up](http://github.com).

Clone the repository
--------------------

Find an appropriate place to work on your computer, with something similar to

``` Bash
cd my_development_folder
git clone git@github.com:myusername/rsd-cppcourse-example.git
cd rsd-cppcourse-example
```

replacing *myusername* with your GitHub user name.

## The reference answers

If this proceeds without error, you're almost good to go. But you should make sure you have a copy of our reference trainer answers.

``` Bash
git checkout -b develop origin/develop
ls # Wow, you can see all the answers!
git checkout master
```

Using version control
---------------------

Note that at various points in the development of the example, we have tagged in our answers a version of the code which is our version of the code at that state.

If your own code is all committed, you can check out a version of our code, with:

``` Bash
git checkout v1.0 # or v2.3 or whatever tag
```

You can abandon your own current work, and revert to our version, by typing:

``` Bash
git reset --hard v1.0
```

If you are more experienced with version control, you
could even use these tags to merge our version into your own, resolving conflicts as appropriate:

``` Bash
git merge v1.4
```

These notes
-----------

The notes in
this document are not intended to be a comprehensive textbook. They are the tutor's notes for delivery of the course,
and are provided to trainees as an aide memoir. This is a practical course, and the purpose is to give trainees a
feel for the use of the language. You will want to supplement this treatment with a good textbook
or [online tutorial](http://www.cplusplus.com/doc/tutorial/).
