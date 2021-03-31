---
layout: post
title:  "Thoughts on unit testing"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## The power of a name
What should this code do? That's a question that helps us focus on what's important, the very reason for the codes existance. Shouldn't the answer to that question be among the most important documentation we have? The first thing that comes to your mind might be how to make the code communicate its intent by design, but shouldn't your tests describe it in an even more easily understandable, short and consise way? How do you write tests that communicate intent?

## Test names should document the behavior
A trick I learned from [Sandro Mancuso](https://twitter.com/sandromancuso) a while ago is to make the names of both the test class and the test methods a readable specification of the behavior. What _should_ this code do? A currency converter should... ACurrencyConverterShould. _What_ should this code do? Return amount according to conversion rate... return_amount_according_to_conversion_rate(). Together, they create a very readable sentence, a living documentation of what the code should do:

```java
ACurrencyConverterShould.return_amount_according_to_conversion_rate()
```

If the test fails, it's obvious what both the test and the code is supposed to do, and that hopefully makes it trivial to find the cause of the failure. If the test ever evolved into testing more things or starting to clutter up, the name would communicate the original intent and reveal the clutter.

## The test code should reflect the test name
Working with the well known "Arrange, Act, Assert" is great, but me and Sandro would also ask you to consider starting from the back. Start with what should be the result. Should the code return something? Should it throw an exception? Send a request to another service? Then work your way upwards to how the code should be called and what data is required to do that. The beauty of this approach is that the focus of the test should end up on a single output, and that should also be the name of your test. You keep your tests short, clear and hopefully readable.

I also think fluent assertions with e.g. [AssertJ](https://github.com/assertj/assertj-core) make your expectations more readable. Take a verification of what elements are present in a list:

```java
assertThat(result).containsExactly(expectedElements);
```

Also try to leave out other details that aren't important for the test. Breaking out objects as constant that are reused based on their properties (AN_INVALID_USER) instead of repeating the creation or hiding it in cryptic helper methods.

Focus on the result you want and ignore how the code gets there as best you can. Prefer using real code whenever possible and work with all types of test doubles, not just mocks. You will have more resilient code that doesn't break as easily when you are refactoring, and with less setup in your tests they will also be shorter and more readable.

## Describe the behavior before writing the code
Last, but not least - the best way I know of creating tests that clearly communicate intent is to describe the behavior before writing the code, and that is exactly what you should be doing with TDD. Start by figuring out how you'd like the code to behave and describe that in the clearest way you can in a test. Then implement the code after that clear structure. That usually makes both the tests and the code more readable.