---
layout: post
title:  "Thoughts on unit testing"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## The power of a name
What should this code do? That's a question that helps us focus on what's important, the very reason for the codes existance. Shouldn't the answer to that question be among the most important documentation we have? The first thing that comes to mind might be how to make the code communicate its intent by design. With that said though, shouldn't your tests describe it in an even more easily understandable, short and consise way? How do you write tests that communicate intent?

## Test names should document the behavior
A trick I learned from [Sandro Mancuso](https://twitter.com/sandromancuso) a while ago is to make the names of both the test class and the test methods a readable specification of the behavior. Say the behavior out loud! What _should_ this code do? For instance: a client repository _should_ return all connected clients? Why not use exactly that as the test name?

```java
AClientRepositoryShould.return_all_connected_clients()
```

If the test fails, it's obvious what both the test and the code is supposed to do, and that hopefully makes it trivial to find the cause of the failure. If the test ever evolved into testing more things or started to clutter up, the name would communicate the original intent and reveal the clutter.

## The test code should reflect the test name
Working with "Arrange, Act, Assert" is great, but me and Sandro would also ask you to consider doing it in reverse - start with what should be the result. Should the code return something? Should it throw an exception? Send a request to another service? Then work your way upwards to how the code should be called and what data is required to do that. The beauty of this approach is that the focus of the test should end up on a single output, and that should also be the name of your test. You keep your tests short, clear and hopefully readable.

Fluent assertions with e.g. [AssertJ](https://github.com/assertj/assertj-core) work wonders in making your expectations more readable. Take this verification of what elements are present in a list as an example:

```java
assertThat(clients).containsExactlyInAnyOrderElementsOf(expectedClients);
```

Another trick is to try to leave out details that aren't important for the test. Breaking out objects to reusable constants based on their properties (e.g. `AN_INVALID_USER`) can help redability a lot, as opposed to repeating the creation or hiding it in cryptic helper methods.

Personally, I also like to focus on the result and ignoring how the code gets there as best I can. Prefer using real code whenever the logic is simple enough to warrant it, and work with all types of [test doubles](https://martinfowler.com/bliki/TestDouble.html), not just strict mocks. You will have more resilient code that doesn't break as easily when you are refactoring, and with less setup in your tests they will also be shorter and more readable.

## Describe the behavior before writing the code
Last, but not least - the best way I know of creating tests that clearly communicate intent is to describe the behavior before writing the code, and that is exactly what you should be doing with [TDD](https://www.agilealliance.org/glossary/tdd/). 

Start by figuring out how you'd like the code to behave and describe that in the clearest way you can in a test. Then implement the code after that clear structure. Refactor as needed, both tests and code. That usually makes both the tests and the code more readable. Use a simple TODO list or similar to keep track of tests you might want to write next. If you need more inspiration, maybe let [zombies](http://blog.wingman-sw.com/tdd-guided-by-zombies) guide you?