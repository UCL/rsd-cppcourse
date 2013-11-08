Putting it all together
=======================

The problem, solved
-------------------

We're now ready to put all this together, all we need to do is write a main function to:

``` cpp
int main(int argc, char **argv){
	// Send the command line arguments to a command line parser
	// Open the filename supplied as an input stream;
	std::fstream system_file("filename_here",std::ios_base::in);
	// Create a solver with the file stream for input and stdout for output
	// call Solve on the solver.
}
```

Note we've provided an example solution file at [test/example.txt](github address)

As you work, you can invoke our program on the command line with:
``` bash
./reactor ../test/example.txt 1.5 100 0
```

The [scaffold](https://github.com/UCL/rsd-cppcourse-example/compare/v3.8...v3.9) for you to work on is [`v3.9`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.9/reactor/)

The [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v3.9...v4.0) is [`v4.0`](https://github.com/UCL/rsd-cppcourse-example/blob/v4.0/reactor/)

Calling the program
-------------------

We should now be able to plot a graph:

``` bash
./reactor ../test/example.txt 1.5 100 0 > results
gnuplot
plot 'results' u 1:2 w lp
```

Hooray!
