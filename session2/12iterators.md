Iterators
=========

Looping over arrays
-------------------

We've seen how to access elements of arrays, but now we want to loop over all the elements of the reactants array to calculate the reaction flux,
which, according to the law of mass action, is the product of the reaction rate and all of the reactant concentrations.

##For loops

The C and C++ for loop, which we need to use, is very complicated.

It is written like this:

``` cpp
for (start_expression; test_expression; increment_expression ){
	// do this code many times
}
```

The first statement is used to set up the loop. The loop runs until the middle expression is no longer true.
The final statement can be used to do anything, but is conventionally used to modify the loop's control variable: the variable used in the completion test.

A trivial sum
-------------

For example, for a trivial sum:

``` cpp
int triangle=0;
for (int i=0; i<10; i++){ // i++ is C++ abbreviation for i=i+1;
	triangle+=i; // C++ abbreviation for triangle = triangle + i;
}
EXPECT_EQ(45,triangle);
// EXPECT_EQ(10,i) would not compile, because i is not in scope.
```

Note that if you use the initialiser statement to both declare and initialise the control variable, it is only defined for the duration of the for loop.
We say that the for loop defines a "scope".

More complicated for loops
--------------------------

``` cpp

int first_factorial_over_1000=1;
int multiplier; // Declared here due so that can see it outside the for loop.
for (multiplier=1; first_factorial_over_1000<1000 ; 
			first_factorial_over_1000*=multiplier){ // x*=y is an
			                                        // abbreviation for x=x*y
	multiplier+=1;
}
EXPECT_EQ(7, multiplier);
EXPECT_EQ(5040, first_factorial_over_1000);
```


##Old-style loops over vectors

We could, of course, loop over a C++ vector like this:

``` cpp
std::vector<int> threes(5,3);
int sum=0;
for (unsigned int i=0; i<threes.size(); i++){
	sum+=threes[i];
}
EXPECT_EQ(15,sum);
```

But C++ provides a more formal way, an "iterator".

##C++ Iterators


An "iterator" is a way of indirectly refering to the current element of a container. When we apply the "add one" `x++` operator to an iterator,
it advances to point at the next element of a container. (This is called "operator overloading": we can make the standard operators do something
unusual when applied to a custom class -- more on this later.)

##Obtaining iterators

We can obtain an iterator to the start of a container with `container.begin()` and to the element *after* the last one with `container.end()`,
so that `container.end()--` is an iterator pointing to the last element.

##Looping with iterators

So, the preferred way to iterate over a C++ container is:

``` cpp
int new_sum=0;
for (std::vector<int>::iterator element=threes.begin(); 
								element!=threes.end(); 
								element++){
	new_sum+=*element;
}
EXPECT_EQ(15,new_sum);
```

Note that we use an asterix operator `*`, to obtain the thing the iterator *points to*, the value itself.

Note that the type of an operator is based on the type of the container, so that a `vector<Reaction>::iterator` is different from a `list<double>::iterator`.

##C++ is Complex!

This a pretty clear example of the sometimes over-complicated nature of C++, but that's the language you've chosen to learn!

Note that in C++11, which, again, we're not using, this is much easier, we can write:

``` cpp
for (auto element : threes) {
	new_sum+=element;
}
EXPECT_EQ(15,new_sum);
```

