Streams
-------

We've seen that we can output data to the terminal with code like:

``` cpp
std::cout << "A species was created called '" << calcium.GetName() << "'" << std::endl;
```

Now, `std::cout` is a stream. A stream is anything which can absorb output like this. It might be a file:

``` cpp
#include <fstream>
std::fstream my_file("filename",std::ios_base::out);
my_file << "Write to the file" << std::endl;
my_file.close();

std::fstream input_file("filename",std::ios_base::in);
std::string first_word;
input_file >> first_word;
EXPECT_EQ("Write",first_word);
```

Or a stringstream, which is a string we can write to like a stream:

``` cpp
std::ostringstream output_buffer;
int x=3;
output_buffer << "Write " << x << " to the buffer" << std::endl;
EXPECT_EQ("Write 3 to the buffer\n",output_buffer.str());
```

We can write a method which accepts *any* kind of output stream, and writes to whatever kind of stream it is:
``` cpp
void output(std::ostream &output){
	output << "Some content" << std::flush;
}

output(std::cout);
output(my_file2);
output(output_buffer);
```

This is our first enounter with the advanced idea of "inheritance". The idea is that each specified type of stream is also a
"derived type" of a "base type" of stream.

Operator Overloading
--------------------

We've also encountered operator overloading again: the `<<` operator is normally used to mean a bitwise-multiply-by-two:

``` cpp
x=5;
EXPECT_EQ(40,x<<3);
```

but when used with streams, `<<` means output, and `>>` means input.

It's easy to define an operator overloading for your type: simply declare a function with a name like `operator+` or `operator--`, which conforms to the appropriate set of arguments and outputs. (Called a "function signature").

The signature one for `operator<<` is:

``` cpp
left_hand_type & operator<<(left_hand_type &, const right_hand_type&);
```

the compiler will work out the left and right hand types in use, and call the operator as appropriate.

