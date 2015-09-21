---
title: Parsing configuration files
---

Parsing files
=============

The other 80/20 rule
--------------------

Much of the time, scientific programming effort is focused on the core numerical routine of the simulation or analysis.

Yet most of the code usually deals with other things:

* Loading in the data
* Setting up memory structures
* Saving results
* Checking for validity
* Reporting on progress


**Mistakes here can ruin your results just as much as a mistake in the "scientific kernel".**

Exercise for the day
----------------------

In this lesson, you will be working in small groups to define a file format for your
system. You will have to work to:

* Define your file format
* Write your parser code

The file format you choose is up to you.

We have defined a test scaffold, and a basic parser class for you to fill in.
There's no need to write the boiler-plate yourself this time.

The tag for the [scaffold](https://github.com/UCL/rsd-cppcourse-example/compare/e541d01...v3.2) is [`v3.2`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.2/reactor/)

The next few slides will introduce some concepts you'll want to use in completing this task.

Working with the provided tests
-------------------------------

We have provided a bunch of tests, which are, in tag , failing. Your task in the exercises today will be to implement three methods:

``` cpp
ReactionSystemParser::NewOrFind();
ReactionSystemParser::ParseLine();
ReactionSystemParser::FromStream();
```

until the tests pass.

Recovering previously defined species
-------------------------------------

A key design decision you will face is whether to

* Separately define the list of species, perhaps at the beginning of the file, or...
* Sefine each species the first time is encountered in the list of reactions.

Either way, you will want to ensure that you can recover the single unique species created for a given name of species.

New Or Find
-----------

The scaffold we have provided assumes that you will create a method called `NewOrFind` with the job of:

* If a species with a given name already exists, you will need to return it.
* If a species with a given name doesn't already exist, you will need to create it.

In order to do this, you will need a data structure called a `map`.

Maps
----

A map is an associative array. It works like an array, except the "key" you use to look up an entry is not a number, as in:

``` cpp
#include <vector>
std::vector<double> my_array;
...
double x = my_array[5];
```

but can be (almost) any type:

``` cpp
#include <map>
std::map<std::string, double> my_map;
...
double x = my_map["banana"];
```

The computer science as to how this can be implemented, and still be fast, is [really very interesting](http://en.wikipedia.org/wiki/Hash_table), but is beyond the scope of this course.

Inserting into a map
--------------------

To add to a map, you can just do:

```cpp
my_map["some_key"]=4.3;
ASSERT_EQ(4.3, my_map["some_key"]);
```

this will overwrite any previous content.

Finding out if a map has an entry
---------------------------------

Doing `some_map[some_key]` by itself will *not* return an error or an empty value. It'll just happily return the default value for the type and return:

``` cpp
std::map<std::string,std::string> empty_map;
ASSERT_EQ("", empty_map["apple"]);
```

To investigate a map without changing it, you need to use `find`. This returns an *iterator* to the found object, or `map::end()` if one is missing:

``` cpp
std::map<std::string,double> my_map;
ASSERT_EQ(my_map.end(), my_map.find("orange"));
empty_map["orange"]=4.3;
ASSERT_EQ(4.3, my_map.find("orange")->second);
ASSERT_EQ("orange", my_map.find("orange")->first);
```

Using a hash for the parser
---------------------------

You should implement the NewOrFind method to pass the provided tests, using a map. It is up to you to work out the correct type for the map.

A reminder on streams
---------------------

Eventually, we will hook this code up to actually read from real files. However, we're going to be writing tests for this code using `std::stringstream`:

``` cpp
std::istringstream buffer(
	"Some example\n"
	"File content\n"
	"Over three lines\n"
	);
```

It's up to you once you've defined your file format, to fill in the example text for your file format. You might find the ability to turn a string into a stream useful in your
solution.

The example system
------------------

The test expectations assume this system is the one used in the examples:

$A+B \overset{2.0}{\rightarrow} C+D$

$C  \overset{3.0}{\rightarrow} E+F$

$A \overset{5.0}{\rightarrow} C$

You should fill in the text for your chosen file format appropriately.

This system defines 6 species.


Reading from a stream
---------------------

We already saw that we can read from a stream by words, separated by spaces, with `>>`

``` cpp
std::string first_word;
input_stream >> first_word;
EXPECT_EQ("Write",first_word);
```

You might want to use this tool to read from a stream: you can read into other types, such as a `double` or a `char`. If you use this approach, you might find a [reference](http://www.cplusplus.com/doc/tutorial/basic_io/) useful.

Continuing until a stream is empty
----------------------------------

We want to keep absorbing from a stream until it is empty. Once the stream is empty, or otherwise not available for new input, then `stream.good()` returns `false`.

So we can loop, and keep getting lines from a file, with:

``` cpp
while (source.good())
{
	std::string line;
	std::getline(source,line);
}
```

Where `source` is some stream.

Breaking from Loops
-------------------

You might need, in your solution, needing to exit early from a loop:

``` cpp
while (true){
	// Continue comes to here
	...
	if (condition_for_skipping_this_cycle) continue;
	...
	if (condition_for_stopping) break;
	...
}
// Break comes to here.
```

This works in `for` loops as well.

Manipulating strings
--------------------

You might find yourself, if you use `getline`, wanting to manipulate strings.

Boost provides some [helpful functions](http://www.boost.org/doc/libs/1_54_0/doc/html/string_algo/usage.html). First, to remove whitespace:

``` cpp
#include <boost/algorithm/string/trim.hpp>
std::string content=" Hello \n";
boost::trim(content)
EXPECT_EQ("Hello",content);
```

And to split up a string:
``` cpp
#include <boost/algorithm/string.hpp>
std::string content2=" Apple, Pear, Orange";
std::vector<std::string> broken;
boost::split(broken,content2,boost::is_any_of(","));
EXPECT_EQ(" Pear",broken[1]);
```

Turning strings into numbers
----------------------------

Without Boost, reliably turning a string into a number involves using stream IO:

``` cpp
string content3="1.5";
std::istringstream buffer(content3);
double x;
buffer >> x;
ASSERT_EQ(x,1.5);
```

Boost provides a `lexical cast` to do this more prettily:
``` cpp
#include <boost/lexical_cast.hpp>
double a=boost::lexical_cast<double>(content3);
ASSERT_EQ(a,1.5);
```

Error handling
--------------

All these examples assume the file we're parsing is just how we want it.
A file which deviates from our file format will crash or hang the program.
A real program would have to manage this properly, and handle any problems graciously.
This is beyond the scope of this course.

Using References to return multiple things
------------------------------------------

When we `return` something from a function in C++, we can only return one thing.

In the ParseReaction method, we want to return the list of products, the list of
reactants, and a rate.

When things are passed by reference, changes made in a function happen to the
supplied variables.

So we can return two values from a function like this:

``` cpp
void myfunction(double & out1, double & out2){...};
double return_one;
double return_two;
myfunction(return_one, return two);
```

Start the exercise
------------------

I recommend you implement NewOrFind to pass the associated tests first.

Then, tackle ParseReaction. This should return the list of strings names for reactants
and products that need to be passed to the `Reaction` constructor.

You have two choices for ParseReaction: you might want to implement it being supplied a stream, or being supplied a string. In our example, we offer the change to the test
you might want to use for either solution.

Then, implement FromStream to call ParseReaction and put it all together.

My Solutions
------------

I have two solutions.

The [first](https://github.com/UCL/rsd-cppcourse-example/compare/v3.2...v3.3) uses a stringstream to parse the reaction line. The tag is [`v3.3`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.3/reactor/)

The [second](https://github.com/UCL/rsd-cppcourse-example/compare/v3.3...v3.4) uses boost string manipulation to parse the reaction line. The tag is [`v3.4`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.4/reactor/)
