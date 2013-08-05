Why C++?
========

This course assumes you already know how to program for science in some other language.

This might be Python, MATLAB, Perl, Ruby. C or FORTRAN.

Compared to these, C++ is a difficult, cumbersome, and confusing language. 

It contains many many different ways to do the same thing, makes some really questionable language design choices,
and is verbose. There is a bewildering choice of compiler vendors and versions, and support for
getting hold of and using third-party libraries is much worse.

There is no great choice of language for scientific programming. Python, Perl, and MATLAB are too slow, C and FORTRAN are insufficiently flexible and expressive, and C++ is just too darn complicated and hard. Of these unpleasant choices, however, we believe C++ is the best choice if both performance and expressiveness are important to your work.

C++ from Python, MATLAB, Perl, or Ruby.
---------------------------------------

Compare this fragment of python:

``` python
numbers=[1,2,3]

for value in numbers:
	print value
```

to this C++:

``` C++
std::vector<int> numbers;
numbers.push_back(1);
numbers.push_back(2);
numbers.push_back(3);

for (std::vector<int>::iterator value=numbers.start();value++;value!=numbers.end()){
	std::cout << *value << std::endl;
}
```

It is clear that using C++ where a simpler language would do, is going to make life difficult for you.

However, compared to these languages, C++ can be a **lot faster to run**. C++, like C and FORTRAN, is a compiled language,
where the code you type is not run directly, but translated into machine code before being run.

This speed is the main reason to try using a compiled language. However, even this is not the final story: good use of
non-compiled languages can produce code that is nearly as fast, and bad use of C++ can produce code which is slow.
Some modern languages with "just in time" compilation like Java and Julia can sometimes be nearly as fast as FORTRAN.

Because it's easy to write very slow code with non-compiled languages, parallel programs for high-performance computing,
for running on supercomputers, are often written in compiled languages, and the tools for accessing parallelism (like OpenMP and MPI)
are better in these languages.

So, if you want code that runs really fast, especially on state of the art supercomputers, then you might want to use C++, C, or FORTRAN.

C++ from C or FORTRAN
---------------------

If you're used to programming Python or Perl, C++ makes available some of the features you'll have grown to expect: containers like
associative arrays (hashes) and lists, exceptions, stream-based IO, and, of course, object orientation. Support for these, and for good programming
practices like testing, is much stronger than in FORTRAN or C.

In C++, I can do things like

``` c++
Moments::InertiaTensor(protein_database["amylase"].GetCoordinateArray());
```

which is, in my view, easier to read than the equivalent might be in FORTRAN or C, and almost as pretty as it would be in Python.

But, because C++ is much more complicated, it is harder for the compiler to produce really efficient machine code, so C++ programs tend to be a bit slower
than FORTRAN code. You can view C++ as a half-way-house in terms of flexibility and expressiveness between Python and FORTRAN.

Note that C is a subset of C++, so if you want to, you can use as much or as little C++ as you like: you can write as if you were writing a C program, but just use C++'s list
container, or just use stream-based IO. This style (writing C, but targeting a C++ compiler) might be a good place to start.

Are you sure you want to learn C++?
-----------------------------------

C++ is:

* Faster than Python, Perl, MATLAB, Mathematica or Ruby.
* More expressive and flexible than FORTRAN or C.

But C++ is:

* Complicated, error-prone, and difficult to learn.
* Usually slower than C or FORTRAN.
* More verbose and less expressive than Python, Perl, MATLAB, Mathematica or Ruby.
* Cumbersome to get running, with a bewildering choice of compilers and variants.

There's a new C++ variant, C++11, which is better than the old version, but this isn't supported yet, so you'll need to decide
whether to use these new features, which make C++ easier to learn and use, but mean your code will run in less places.

Our view is that despite these problems, C++ is a good choice for future scientific programmers to learn as a *second* scientific programming language: 
it introduces object orientation and dynamic data structures if you're coming from C or FORTRAN, 
and pointers and strict typing if you're coming from Python or MATLAB. 
If you're an aspiring computational scientist, you'll need to get to grips with all these concepts
eventually, so C++ is a good learning exercise. Once you've learned C++ as your second language, 
you'll have the vocabulary and concepts you need to learn many other languages.

Of the available choices, we recommend C++ as the best choice only if both performance and
expressiveness are important to your work. If you don't care about speed, use Python.
If you don't care about expressiveness, use FORTRAN.