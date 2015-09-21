---
title: Boost ODEint
---

Solving the ODEs
================

Boost ODEint
------------

Boost can solve ODEs like this:

```cpp
boost::numeric::odeint::integrate(rhs_function, concentrations ,
	start_time, end_time, time_step, observe_integration);
```

Here, `rhs_function` must be something that can be called with `operator()`, a function or a class with an overloaded method.

The function is passed to the integrator to determine the rates given the current values.

Similarly, `observe_integration` is something that should be called every timestep to
print or store the result of each step.

An example wrapper class
------------------------

```cpp
class WrapReactionSystemForODEINT
{
public:
	ReactionSystem &system;
	WrapReactionSystemForODEINT(ReactionSystem & system):
		system(system)
	{
	}
	void operator() ( const std::vector<double> &x ,
					  std::vector<double> &dxdt,
					  const double time)
    {
        system.GetRatesGivenConcentrations(x,dxdt);
    }
};
```

An example Observer
-------------------

```cpp
void observe_integration(const std::vector<double> &concentrations,
	const double time)
{
	std::cout << time << ": [" << std::flush;
	for (unsigned int i=0; i<concentrations.size();i++){
		std::cout << concentrations[i] <<  ", " << std::flush;
	}
	std::cout << "]" << std::endl;
}
```

Exercise: A solver test
-----------------------

For now, we're just going to write a standalone test, to prove that we can use Boost to solve a reaction system

Make a new test file, called `IntegrationTest.cpp`.

Add a fixture which sets up a simple reaction, a decay of one species into another:

$A \overset{k}{\rightarrow} B$

Add a test which checks the final concentrations of the species are as expected:

$[A] = A_0 e^{-kt}$

$[B] = A_0 (1-e^{-kt})$

The tag for this [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v3.0...v3.1) is [`v3.1`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.1/reactor/test/IntegrationTest.cpp)

Hint: Using the wrapper class
-----------------------

Copy in my wrapper class from the previous slide, and call it like this:

``` cpp
	WrapReactionSystemForODEINT wrapper(simple_decay_system);
	int step_count=boost::numeric::odeint::integrate(wrapper, concentrations,
		 0.0, 1.5, 0.1, observe_integration);
```
