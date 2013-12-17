C-Style Arrays and Strings
==========================

C-Style Arrays and Strings
--------------------------

The C++ main function:

```cpp
int main(int argc, char** argv){}
```

passes in the command line arguments in C-Style, that is,
using the constructs for arrays and strings provided in C,
not C++.

C is C++
--------

All of C is part of C++. Any C program is also a C++ program.
Thus, in reading other people's C++ programmes, you will
need to be able to read C programs, since people often drop into using
C-style arrays and strings in C++. Libraries often expect them too.

Pointer Arithmetic
------------------

When you add a number to a pointer, it points to the next thing along in memory, 
counting along that many bytes as the size of whatever the type that is pointed to takes.

``` cpp
std::vector<int> x;
x.push_back(5);
x.push_back(11);
x.push_back(17);
int_pointer=&x[0]
ASSERT_EQ(5,*int_pointer);
ASSERT_EQ(17,*(int_pointer+2));
```

Arrays in C
-----------

This is how arrays work in C.

C provides a square bracket operator as syntactic sugar for pointer arithmetic, and for
allocating blocks of memory for such arrays:

``` c
int array_pointer[3]={5,11,17};
ASSERT_EQ(5,array_pointer[0]);
ASSERT_EQ(17,array_pointer[2]);
```

C also provides matrices in the same way:

``` c
int matrix[3][3];
...
middle = matrix[1][1];
```

C-Style Strings
---------------

The C++ `std::string` knows how many characters it has:
``` cpp
std::string message("Hello World");
ASSERT_EQ(11,message.size());
```

The C-style string does not. It is simply a C-style array of characters,
with a special constructor syntax, and a zero byte after the last character.
``` c
char * c_message = "Hello World";
ASSERT_EQ(c[10]='d');
ASSERT_EQ(c[11]=0); // Not '0'!
```
This is called a null-terminated string. 

When you print it out, the printer knows to stop when it finds the termination marker.

Converting Between String Styles
--------------------------------

You can get a C-style string from a C++ string:

``` cpp
ASSERT_EQ(c_message,message.c_str());
```

and construct a C++ string from a C string
``` cpp
ASSERT_EQ(message,std::string(c_message));
```

Understanding main()
--------------------

We can now understand the C and C++ `main` function:

``` cpp
int main(int argumnet_count, char **array_of_c_strings) {
	return 0;
}
```

