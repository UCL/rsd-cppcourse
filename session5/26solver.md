Exercise: Building A Solver
===========================

Exercise: Building A Solver
---------------------------

So far, we've only created an integration test to prove we can solve ODEs.

We need to move this into a proper class, bringing together the code we wrote to
allow reaction systems to set and get concentrations, with the reaction system
parser we wrote.

As a syntax exercise, we've written most of this class, and some tests.
All you have to do is replace pseudocode with the right calls to make the tests pass.

Solution
--------

The [scaffold](https://github.com/UCL/rsd-cppcourse-example/compare/v3.4...v3.5) for you to work on is [`v3.5`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.5/reactor/)

Note we're trying to make a space-separated
output of the results of the solution, suitable for plotting with gnuplot.

The [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v3.5...v3.6) is [`v3.6`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.6/reactor/)

An obscure line in Solver::Solve
--------------------------------

There's a line we gave you in Solver::Solve:

``` cpp
return boost::numeric::odeint::integrate(boost::ref(*this), 
	initial_concentrations, 
	start_time, end_time, initial_step, 
	boost::bind(&Solver::observe_integration,this,_1,_2));
}
```

With two interesting Boost featuers, `bind` and `ref`.

These are beyond the scope of the course, but we have to use them to make the integration neat,
so you can read the following slides if you're curious about functional programming in C++.

Boost::Bind
-----------

We have spoken previously of the way in which `integrate` expects two functions to be passed to it,
one of which, the last argument, is an integration observer, for printing out to a stream the proceedings
of the numerical method.

In the IntegrationTest, we declared a bare function, not a method of any class. 
(So that it can be called without a . or ->)
```
int add(int a, int b)
{
	return a+b;
}
ASSERT_EQ(5, add(2, 3));
```

Here, we'd like to pass a function which is not a bare function, as in the `IntegrationTest`, but a 
*method* of `Solver`. 

But what do I call it from?
---------------------------

But if we just pass the method to the integrator, 
it won't know how to get to the Solver object to call it on.

``` cpp
\\ Inside the integrator
?.observe_integration(time);
```

Binding arguments ahead of time
-------------------------------

We can use boost::bind to create a new function, which specifies some of the arguments to another function ahead of time:
``` cpp
add_four=boost::bind(add,_1,4);
ASSERT_EQ(11,add_four(7));
```

In the case of using bind with a member function, the first argument is assumed to be a pointer to the object to call
with (using . or ->), so

``` cpp
boost::bind(&Solver::observe_integration,this,_1,_2));
```

will yield a function whose first argument is the concentrations, second is time, and which is a freestanding function not
a method. Note that `this` is a C++ keyword meaning "a pointer to the current object".

Boost::Ref
----------

Our other obscure problem is that inside the integrator, it makes copies of the system argument, the first one passed to
it, implementing `operator()`. In our case, we'd like that to be the solver itself.

However, when it makes a copy, the copy gets a copy of the same pointer to the same `ReactionSystem`. And when the copy
gets `delete`d, it deletes that system, in the `Solver` destructor. So each copy will try to delete the same
reaction system, and you can't delete the same thing more than once. So the program crashes.

Adding a wrapper-wrapper-wrapper
--------------------------------

We could get around this by adding another layer of indirection, with a:

``` cpp
class SolverWrapper{
	Solver & solver;
	SolverWrapper(Solver & solver):solver(solver){};
	operator() (whatever...) {solver(same whatever...)}
}
```

But `boost::ref` implements exactly this tedium for us:

```cpp
boost::ref(*this)
```