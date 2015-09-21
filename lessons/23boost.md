---
title:  The Boost library
---


Boost
=====

Boost
-----

[Boost](http://www.boost.org/) is a massive set of extra libraries for C++.

It contains all kinds of useful functionality: it's hard to write C++ code without wanting to use it!

Telling CMake about boost
-----------------------

You were asked to follow the [instructions][Installing Boost] to install Boost. Do so now if you haven't already.

We now need to tell CMake to look for and use Boost:

``` cpp
set(Boost_ADDITIONAL_VERSIONS 1.53.0 1.54.0 1.53 1.54)
find_package(Boost 1.53.0 )
if(Boost_FOUND)
	include_directories(${Boost_INCLUDE_DIRS})
endif()
```

Using boost
-----------

Once CMake knows about Boost, we can use Boost libraries with:

``` cpp
#include <boost/whatever.hpp> // e.g.:
#include <boost/numeric/odeint.hpp> // Include ODE solver library
					// just to check our build system found it
```

There is a tag for [updating](https://github.com/UCL/rsd-cppcourse-example/compare/v2.9...v3.0) the CMake system to use boost: [`v3.0`](https://github.com/UCL/rsd-cppcourse-example/blob/v2.9/reactor/src)
