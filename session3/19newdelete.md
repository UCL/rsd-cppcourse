New and Delete
==============

The Heap and the Stack
----------------------

When I declare a variable inside a function or method like this:

```C++
void somefunction()
{
	int x=5;
	// do stuff with x;
}
```

as soon as the function is deleted, the variable ceases to exist, and the memory associated with it is cleaned up.

Variables declared like this are variables "on the stack". They can be called from the function they are created in.
If they are passed as references to functions called from that function, then it's fine, they'll still exist:

```C++
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

But they are cleaned up, and the associated memory freed, when the creating function exits. This means that if I try to return a
reference, pointer, or iterator to a stack variable, the reference will become invalid, and crashes can occur:

```C++
std::string * makemeastring(){
	std::string result("Hello");
	return &result;
}

std::cout << *makemeastring() << std::endl; \\ NO! This might crash!
```

If I want to make something to which I can return a reference, a stack variable will not do. I need a way of creating variables which
will hang around until I specifically tell them to be deleted. The place where such variables exist is called the "heap".

New
---

I can make a heap variable like this:

```C++
std::string * makemeastring(){
	std::string * heapstring=new std::string("Hello");
	return *heapstring;
}

std::cout << *makemeastring() << std::endl; \\ Bad, memory leak!
```

Which will work, but will cause a "memory leak". Each time I call this, space for the new string is created on the heap.
But it is never cleaned up. So a program like:

```C++
for (int i=0;i<1000000;i++){
	makemeastring();
}
```

will eventually crash due to lack of memory.

Delete
------

So when we use `new`, we should use `delete` as well, so as to make sure we clean up after ourselves.

``` C++
std::string * makemeastring(){
	std::string * heapstring=new std::string("Hello");
	return *heapstring;
}

std::string * mystring=makemeastring();
std::cout << *mystring << std::endl;
delete mystring;
```

We pass a pointer to `delete`, specifying the heap variable to be cleaned up.

Destructors
-----------

Functions, like the example above, which create an object on the heap and return it, are sometimes called "factory methods". The danger here is that you might forget to `delete`
the returned pointer.

Where we can, it is good practice to keep all heap variables managed as part of the implementation internals of one class. To facilitate this, C++ provides a tool called "destructors"
to make it easy for objects to clean up their heap data when it is their turn to be cleaned up. The descructor method is called whenever the object is cleaned up,
either through an explicit delete call or at the end of a scope when an object is allocated on the stack.

A destructor method is often used to free memory allocated during a constructor. The name of the destructor is the same as the name of the destructor, preceded by a tilde `~`:

``` C++
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

The heap variable memory is managed inside the class: a pointer to it is given out, but client classes never have to worry about deleting it. Indeed, the program will crash if they do: if you try to delete a variable twice, the program will crash. (This is where C++11 shared_ptrs start to look seriously cool.)

Let's move on to the next [exercise](20system.md)