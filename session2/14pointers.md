Pointers
========

## Why we need pointers

We have a problem. 

Our `vector<Species>` in the reaction class is actually taking a *COPY* of each species we define:

``` cpp
	emptyReaction.AddReactant(calcium);
	EXPECT_EQ(emptyReaction.GetReactants()[0].GetName(),"Ca");

	emptyReaction.GetReactants()[0].SetConcentration(19.0);
	EXPECT_EQ(19.0,emptyReaction.GetReactants()[0].GetConcentration());
	EXPECT_EQ(19.0,calcium.GetConcentration()); // FAIL!
```

(I removed some "const" declarations temporarily to demonstrate this, so that I could call SetConcentration() on the result of GetReactants(). )

This will be a big problem when we have multiple reactions: we need all the reactions involving Calcium to refer to the same *Calcium*!

## Storing references

So, we're going to need to ensure that our `vector` stores not Species themselves, but references to species defined elsewhere.

Unfortunately, we can't just solve this by writing `vector<Species &> reactants;`

This is because dangling references are not allowed: a container must be able to be initialised with default values, as in `vector<int> x(5);`.

But a `vector<int &>x(5)` wouldn't know what to refer to!

## Pointers to the rescue!

Instead, we can use the *pointer*, an older way of achieving this indirection, borrowed from C. Just as we declare a reference to an int with a type of

``` cpp
int &x=something();
``` 

so we declare a pointer to an int with 

```cpp
int *x;
```

## Pointers are dangerous

With a reference, we know the reference always refers to something, but with a pointer, it can point to an unspecified location. 

If we try to use a pointer which
points to something invalid, our program will crash at runtime. 

It is easy this way to write programs that crash, and this isn't detected by the compiler. 

(In C++11, we can avoid these nasty problems by using `std::shared_ptr` and `std::weak_ptr`.)

## Pointer syntax

Just as with iterators, we use an asterix operator to obtain the thing pointed to. To obtain a pointer to something we already have, we use an ampersand, a confusing overuse
of one symbol!

``` cpp
	double x=5;

	double *my_ptr; // This pointer points nowhere : not safe to use yet.
	my_ptr=&x; // Make it point to x;

	*my_ptr=6;

	EXPECT_EQ(6,*my_ptr); // obviously OK
	EXPECT_EQ(6,x); // Oh, by modifying the pointer, we changed x!
```

## Pointer syntax 2

``` cpp
	double y=7;

	my_ptr=&y; // We can change what it points to!
	EXPECT_EQ(7,*my_ptr);

	*my_ptr=8; // Change the value of the thing pointed to
	EXPECT_EQ(8,*my_ptr);
	EXPECT_EQ(8,y);
	EXPECT_EQ(6,x); // the thing the pointer *used* to point to is unchanged.

	std::cout << my_ptr << " " << *my_ptr << std::endl; // Outputs .

	double *new_ptr=&x;

	//EXPECT_EQ(new_ptr,my_ptr); // Two pointers compare equal if they 
								 // point to the same thing. 
								 // These two don't so this test would fail.
	new_ptr=&y;
	EXPECT_EQ(new_ptr,my_ptr); // OK
```

## Reference syntax revisited

``` cpp
	double x=5;
	double &x_ref=x; // You *have* to define what a reference refers to
	double y=7;

	x_ref=y; // The reference is *still* referring to x. We can't move the 
			 // reference to refer to something else!
	EXPECT_EQ(7,x_ref);
	EXPECT_EQ(7,x); // By modifying the reference, we changed x.

	x_ref=8;
	EXPECT_EQ(8,x_ref);
	EXPECT_EQ(8,x); // By modifying the reference, we changed x.
	EXPECT_EQ(7,y); // y is unchanged.

```

##There's more than one way to do it.

So, we've now seen three ways of referring indirectly to something, references, pointers, and iterators. C++ frustratingly contains many different ways to do the same thing. This is sometimes called TMTWWTDI, pronounced "tim-toady".

##Calling methods of pointers

If we have a reference to, or an iterator to, an object with methdos we can call, we might think we would have to write:

``` cpp
(*my_ptr).CallMethod();
```

But there is a syntactic sugar for this:

``` cpp
my_ptr->CallMethod();
```

This "arrow operator" means dereference-then-call.

If we have a double pointer, or a pointer to an iterator, or an iterator to a pointer, we still need the annoying brackets:

``` cpp
Species **double_pointer;
Species *pointer;
Species calcium;
pointer=&calcium;
double_pointer=&pointer;
pointer->SetConcentration(11.0);
EXPECT_EQ(2.0, (*double_pointer)->GetConcentration()); 
		// Sadly, not double_pointer->->GetConcentration();
```


