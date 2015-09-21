---
title: Memory Management with New and Delete
---


New and Delete
==============

##Nowhere for a Species to live

So that we are always referring to the same instance of each Species, we're now always using pointers in our vectors.

This is fine in our tests: we actually instantiate the Species in the fixture class.

But in the real code, we need somewhere for the Species and Reactions to actually be **owned** by.

##The Stack

When I declare a variable inside a function or method like this:

``` cpp
void somefunction()
{
	int x=5;
	// do stuff with x;
}
```

as soon as the function is deleted, the variable ceases to exist, and the memory associated with it is cleaned up.

Variables declared like this are variables "on the stack". They can be called from the function they are created in.

## The stack and called functions

If they are passed as references to functions called from that function, then it's fine, they'll still exist:

``` cpp
void someotherfunction(int & input)
{
	std::cout << input << std::endl;
}

void somefunction()
{
	int x=5;
	someotherfunction(x);
}
```

## The stack and calling functions

But they are cleaned up, and the associated memory freed, when the creating function exits. This means that if I try to return a
reference, pointer, or iterator to a stack variable, the reference will become invalid, and crashes can occur:

``` cpp
std::string * makemeastring(){
	std::string result("Hello");
	return &result;
}

std::cout << *makemeastring() << std::endl; \\ NO! This might crash!
```

## The Heap

If I want to make something to which I can return a reference, a stack variable will not do.

I need a way of creating variables which will hang around until I specifically tell them to be deleted.

The place where such variables exist is called the "heap".

##New

I can make a heap variable like this:

``` cpp
std::string * makemeastring(){
	std::string * heapstring=new std::string("Hello");
	return *heapstring;
}

std::cout << *makemeastring() << std::endl;
```

## Memory leaks

The example we just saw will work, but will cause a "memory leak".

Each time I call this, space for the new string is created on the heap.

But it is never cleaned up. So a program like:

``` cpp
for (int i=0;i<1000000;i++){
	makemeastring();
}
```

will eventually crash due to lack of memory.

##Delete

So when we use `new`, we should use `delete` as well, so as to make sure we clean up after ourselves.

``` cpp
std::string * makemeastring(){
	std::string * heapstring=new std::string("Hello");
	return *heapstring;
}

std::string * mystring=makemeastring();
std::cout << *mystring << std::endl;
delete mystring;
```

We pass a pointer to `delete`, specifying the heap variable to be cleaned up.

## Ownership

So, we can use a pointer in two ways:

1. A "strong reference" : to a variable which we have created, and have a responsibility to delete
2. A "weak reference" : to a variable someone else has created.

## Factories


Classes which create an object on the heap and return it, are sometimes called "factories".

The danger here is that you might forget to `delete`
the returned pointer.

We need to think about who "owns" the memory: who has the responsibility to delete it.

Where we can, it is good practice to keep all heap variables managed as part of the implementation internals of one class.

##Destructors

To facilitate good cleanup of heap memory, C++ provides a tool called "destructors".

The descructor method is called whenever the object is cleaned up, either through an explicit delete call or at the end of a scope when an object is allocated on the stack.

We use the destructor to clean up "daughter" objects which the class created on the heap during it's lifetime.

## Destructor Syntax

The name of the destructor is the same as the name of the constructor, preceded by a tilde `~`:

``` cpp
class Myclass {
	double * heapdouble;

	Myclass(){
		heapdouble = new double;
	}

	double * GetMyData() {return heapdouble;}

	~Myclass(){
		delete heapdouble;
	}
}
```

The heap variable memory is managed inside the class: a pointer to it is given out, but client classes never have to worry about deleting it. Indeed, the program will crash if they do: if you try to delete a variable twice, the program will crash.
