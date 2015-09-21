---
title: Command Line arguments
---


Exercise: Creating a Command Line Parser
========================================

Creating a command line parser
------------------------------

When someone, in the shell, writes

``` bash
reactor mysystem.txt 17 10 50 100
```

We want it to load the file mysystem.txt to describe the reactions, solve from t=0 to t=17,
and use 10 50 and 100 as the initial concentrations for the species.

So, we've written a scaffold with tests for a command line parser class, which needs to take the
`int argc, char **argv` inputs, and have methods to give back the filename, the initial concentrations,
and the final time.

The [scaffold](https://github.com/UCL/rsd-cppcourse-example/compare/v3.6...v3.7) for you to work on is [`v3.7`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.7/reactor/)

The [solution](https://github.com/UCL/rsd-cppcourse-example/compare/v3.7...v3.8) is [`v3.8`](https://github.com/UCL/rsd-cppcourse-example/blob/v3.8/reactor/)
