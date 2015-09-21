---
title: Fixtures
---


Fixtures
========

##Introduction

We often end up writing tests with common parts, which set up our example object for investigation.

We use the term "fixture" to refer to a standard set of inputs used for tests. This could be a whole scientific problem or a small set of values.

In the GoogleTest C++ testing framework, we can declare fixtures as classes, and access them in our tests as objects.

##Testing Reaction with Fixtures

Using a fixture, our [ReactionTest](https://github.com/UCL/rsd-cppcourse-example/blob/v1.4/reactor/test/ReactionTest.cpp) code looks like:


``` cpp
class ReactionTest: public ::testing::Test {
protected:
	Reaction myReaction;
	ReactionTest():
		myReaction(5.0)
	{
	};
};

TEST_F(ReactionTest, ReactionHasRate) { // First argument is test
										// fixture, second is test name
  EXPECT_EQ(5.0, myReaction.GetRate()); // Assert that the reaction
  										// rate should be as expected
}
```

Where we use `TEST_F` instead of `TEST` to introduce a test which uses a fixture. Note that in the expectation,
we reference the member variable myReaction created in the fixture.
