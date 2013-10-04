Inline Definitions
==================

##Introduction

In our [interface declaration](https://github.com/UCL/rsd-cppcourse-example/blob/v1.2/reactor/src/Species.h) for the new Species methods, we've put the implmentation of the methods right in with the definition:

``` cpp
void SetConcentration(double new_concentration) {
	concentration=new_concentration;
} // Set concentration
```

Normally, we would put the declaration in the header file:

``` cpp
void SetConcentration(double new_concentration);
```

and the implementation in the .cpp file:

``` cpp
void Species::SetConcentration(double new_concentration) {
	concentration=new_concentration;
}
```

However, sometimes, for brevity, we choose to do the implementation and the declaration in one go.

Why Inline?
-----------

One reason for this can be speed: jumps into functions in an implementation file are harder for the compiler to optimise.
However, I would recommend against this: unless your code is really absolutely performance critical, you should design your
code to be as easy to read as possible. Usually, separation of interface and implementation leads to more readable code: users
of your classes don't need to know how they work inside.

However, for really simple brief functions, such as getters and setters, it can be more convenient just to implement them in the header file.
This is a judgement call, a matter of your personal programming aesthetics.
