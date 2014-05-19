Why C++?
========

Prerequisite languages
----------------------

This course assumes you already know how to program for science in some other language.

This might be Python, MATLAB, Perl, Ruby, Java, C or Fortran.

What's wrong with C++?
----------------------

Compared to these, C++ is a difficult, cumbersome, and confusing language. 

It contains many many different ways to do the same thing, makes some really questionable language design choices,
and is verbose. There is a bewildering choice of compiler vendors and versions, and support for
getting hold of and using third-party libraries is much worse.

No Good Choice
--------------

There is no great choice of language for scientific programming. Python, Perl, and MATLAB are too slow, C and Fortran are insufficiently flexible and expressive, and C++ is just too darn complicated and hard. Of these unpleasant choices, however, we believe C++ is the best choice if both performance and expressiveness are important to your work.

C++ from Python, MATLAB, Perl, or Ruby: The Bad
-----------------------------------------------

Compare this fragment of python:

``` python
numbers=[1,2,3]

for value in numbers:
	print value
```

to this C++:

``` cpp
std::vector<int> numbers;
numbers.push_back(1);
numbers.push_back(2);
numbers.push_back(3);

for (std::vector<int>::iterator value=numbers.start(); 
	 value != numbers.end(); ++value){
	 std::cout << *value << std::endl;
}
```

It is clear that using C++ where a simpler language would do, is going to make life difficult for you.

C++ from Python, MATLAB, Perl, or Ruby: The Good
------------------------------------------------

However, compared to these languages, C++ can be a **lot faster to run**. 

C++, like C and Fortran, is a compiled language,
where the code you type is not run directly, but translated into machine code before being run.

Compiled is not necessarily faster
----------------------------------

This speed is the main reason to try using a compiled language. However, even this is not the final story: good use of
non-compiled languages can produce code that is nearly as fast, and bad use of C++ can produce code which is slow.
Some modern languages with "just in time" compilation like Java and Julia can sometimes be nearly as fast as Fortran.

Compiled languages for high-performance
----------------------------------------

Because it's easy to write very slow code with non-compiled languages, parallel programs for high-performance computing,
for running on supercomputers, are often written in compiled languages, and the tools for accessing parallelism (like OpenMP and MPI)
are better in these languages.

So, if you want code that runs really fast, especially on state of the art supercomputers, then you might want to use C++, C, or Fortran.

C++11
-----

There's a new version of C++, C++11, which is better than the old version. The above fragment can be written in C++11 as:

This C++03:

``` cpp
std::vector<int> numbers;
numbers.push_back(1);
numbers.push_back(2);
numbers.push_back(3);

for (std::vector<int>::iterator value=numbers.start(); 
	 value != numbers.end(); ++value){
	 std::cout << *value << std::endl;
}
```

is this in C++11:

``` cpp
std::vector<int> numbers{ 1, 2, 3};

for (auto value : numbers) std::cout << value << std::endl;
```

No C++11 in this course
-----------------------

but this isn't supported everywhere yet, so you'll need to decide
whether to use these new features, which make C++ easier to learn and use, but mean your code will run in less places. In this course, 
we teach the old-style C++, but will occasionally mention the C++11 versions for future awareness.

C++ from C or Fortran: The Good
-------------------------------

If you're used to programming Python or Perl, C++, unlike C or Fortran, makes available some of the features you'll have grown to expect: 

* associative arrays (hashes)
* linked lists
* exceptions
* stream-based IO,
* object orientation. 

Support for these, and for good programming practices like testing, is much stronger in C++ than in Fortran or C.

C++ can be fairly readable
--------------------------

In C++, I can do things like

``` cpp
Moments::InertiaTensor(protein_database["amylase"].GetCoordinateArray());
```

which is, in my view, easier to read than the equivalent might be in Fortran or C, and almost as pretty as it would be in Python.

C++ from C or Fortran: The Bad
------------------------------

Because C++ is much more complicated, it is harder for the compiler to produce really efficient machine code, so C++ programs tend on average to be a bit slower
than Fortran code. 

It is possible to craft C++ which is just as fast as C or Fortran, but naively used, C++ can often be slower. 

As always, it is a good idea to profile your code before attempting optimisation.

C is C++
--------

C is a subset of C++, so if you want to, you can use as much or as little C++ as you like: you can write as if you were writing a C program, but just use C++'s list
container, or just use stream-based IO. 

This style (writing C, but targeting a C++ compiler) might be a good place to start.

Are you sure you want to learn C++?
-----------------------------------

C++ is:

* Faster than Python, Perl, MATLAB, Mathematica or Ruby.
* More expressive and flexible than Fortran or C.


But C++ is:

* Complicated, error-prone, and difficult to learn.
* Harder than C or Fortran to make really fast.
* More verbose and less expressive than Python, Perl, MATLAB, Mathematica or Ruby.
* Tough to get running, with hard-to-install libraries and cumbersome build tools.

So, why C++?
------------

Our view is that despite these problems, C++ is a good choice for future scientific programmers to learn as a *second* scientific programming language: 

* It introduces object orientation and dynamic data structures if you're coming from C or Fortran, 
* It introduces pointers, memory management, and strict typing if you're coming from Python or MATLAB. 

If you're an aspiring computational scientist, you'll need to get to grips with all these concepts
eventually, so C++ is a good learning exercise. Once you've learned C++ as your second language, 
you'll have the vocabulary and concepts you need to learn many other languages.

Conclusion
----------

Of the available choices, we recommend C++ as the best choice only if both performance and
expressiveness are important to your work. If you don't care about speed, use Python.
If you don't care about expressiveness, use Fortran.
