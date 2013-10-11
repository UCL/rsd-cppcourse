References
==========

Reference syntax
----------------

We already looked very briefly at references in the first session.

Consider the following code fragment, which should help to explain the role of references!

``` cpp
	double x=5;

	double &x_ref=x; // You *have* to define what a 
					 // reference refers to when it is made
	//double & illegal_ref; // Dangling references are forbidden.

	x_ref=6;

	EXPECT_EQ(6,x_ref); // obviously OK
	EXPECT_EQ(6,x); // Oh, by modifying the reference, we changed x!

	const double &const_x_ref=x; // It would be illegal to say const_x_ref=7
```

Avoiding large copies
---------------------

This can be used to speed things up. We're now starting to return quite big objects from our methods:
we just returned a list of Species. By default, the vector of Species returned will be a *copy* of the vector stored in the reaction object. It would be more efficient
to return the list itself. 

So, we should instead return a reference to the list: we can just add an ampersand to the return type.

References and const
--------------------

However, this would cause a const-ness violation: the returned reference could be used to modify the species, so the GetReactants() method would not be `const`.

Thus, we should make sure it is a "const reference". 

A const reference, like `const double &`, is a type that means "this is a reference to a double", and cannot be used to modify the double.

Exercise: returning vectors as references
-----------------------------------------

As an exercise, you should now modify your code to ensure that if you return vectors, you do so with a const reference.

Our solution for this exercise is tagged as [`v1.6`](https://github.com/UCL/rsd-cppcourse-example/tree/v1.6)

Have a look at my [changes](https://github.com/UCL/rsd-cppcourse-example/compare/v1.5...v1.6)
