---
title: Testing
---


Testing
=======

##Automated Tests

When we program, we want to know that our code works as expected.

Newer programmers tend to do this in an ad-hoc fashion, working with a main program that they thing should work, and
inspecting the output to check things are OK.

A better way, however, is to write *automated tests*, small pieces of
code which verify each subroutine or class does what is expected. We write many such small tests, and keep running them
whenever we make a change.

That way, we can be sure that our new changes haven't broken old functionality.

##The Species Test File

Look at the file [test/SpeciesTest.cpp](https://github.com/UCL/rsd-cppcourse-example/blob/master/reactor/test/SpeciesTest.cpp):

``` cpp
// Test that the system has a name as expected.
TEST(SpeciesTest, SpeciesHasAName) { // First argument is test group
									 // second is test name
  Species mySpecies("SomeName"); // Create a species with a specified name
  EXPECT_EQ("SomeName", mySpecies.GetName()); // Assert that the name
  											  // should be as expected
}
```

Here we define an *expectation*: something which should be true, in this case, that the system name should be as defined.

##Running the Tests

You can run this test with

``` bash
ctest
```

and should see:

> ```
> Running tests...
> Test project /Users/jamespjh/devel/rsdt/
>     rsd-cppcourse-example/reactor/build
>     Start 1: SpeciesTest
> 1/1 Test #1: SpeciesTest .......   Passed    0.02 sec
>
> 100% tests passed, 0 tests failed out of 1
>
> Total Test time (real) =   0.02 sec
> ```

##Analysing failing tests

try modifying the test so it should fail:
``` Diff
- Species mySpecies("SomeName");
+ Species mySpecies("SomeOtherName");
```

``` bash
make
ctest
```

(Note that we needed to recompile with make.)

> ```
> Running tests...
> Test project /Users/jamespjh/devel/
         rsdt/rsd-cppcourse-example/reactor/build
>    Start 1: SpeciesTest
> 1/1 Test #1: SpeciesTest ........***Failed    0.01 sec
>
> 0% tests passed, 1 tests failed out of 1
>
> Total Test time (real) =   0.02 sec
>
> The following tests FAILED:
>           1 - SpeciesTest (Failed)
> Errors while running CTest
> make: *** [test] Error 8
> ```

``` bash
ctest --output-on-failure
```

> ```
> /Users/jamespjh/devel/rsdt/rsd-cppcourse-example/reactor/test/SpeciesTest.cpp:7: Failure
> Value of: mySpecies.GetName()
>  Actual: "SomeOtherName"
> Expected: "SomeName"
> ```

Note the difference between the *expected* and *actual* values.

Put your code back right again. (`git checkout SpeciesTest.cpp`)

##Adding new tests

Note that in future, as we code, we will add new tests for our new functionality.

We'll need to tell CMake to build them, with an appropriate new line in `testing/CMakeLists.txt`, which currently has:

``` CMake
cxx_test(SpeciesTest SpeciesTest.cpp reactor_library)
#specify a new test, and which files it depends on.
```
