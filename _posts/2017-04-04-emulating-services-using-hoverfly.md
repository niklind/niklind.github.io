---
layout: post
title:  "Emulating services using HoverFly"
---

### Contents

* Table of Contents
{:toc}

### What is HoverFly?

[HoverFly](https://hoverfly.io/) is a [service virtualization](https://en.wikipedia.org/wiki/Service_virtualization) tool that can emulate other services by recording requests and responses and then playing them back. It's set as a [proxy](https://en.wikipedia.org/wiki/Proxy_server) between your system under test and the services you want to emulate. 

That way you can test your system without using any real services, which increases the reliability of the tests. 

![Capture sequence](/images/hoverfly_simulate.png)

### When to use it

A service virtualization tool is often used as a complement or replacement for a mock or a stub. In my personal opinion, mocks work best when there are complex interactions with a few services and stubs are effective when there are simple interactions with a small amount of services. 

Service virtualization tools are the most useful when there are many services to interact with because of the recording capabilities. This can be the case with systems based on microservices, and mostly for the types of tests that exercise larger portions of the system such as [compontent tests](https://martinfowler.com/bliki/ComponentTest.html) and [end-to-end tests](https://martinfowler.com/bliki/BroadStackTest.html).

Emulating a flaky or unstable dependent service by injecting faults, latency and similar becomes more realistic when used through an external service instead of modifying your own system. 

You can also use service virtualization as a tactical approach to working with services that don't exist yet, or to extend existing services with new functionality before it's available.

### Getting started

[The tutorials of the HoverFly documentation](https://docs.hoverfly.io/en/latest/pages/tutorials/tutorials.html) are quite good, and provide excellent examples of most use cases. I'd suggest starting with reading up on the [key concepts](https://docs.hoverfly.io/en/latest/pages/keyconcepts/keyconcepts.html), then following the tutorials for: 

* Capturing and exporting data
* Simulating and importing data
* Request matching 

Another interesting service you can use, besides [jsontest](http://time.jsontest.com/) that they refer to in the documentation, is [httpbin](http://httpbin.org/). It's really a collection of simple but useful services that responds with the e.g. exact GET-request it received, or the originating IP, or some sample XML or JSON. Quite nifty.

**Note:** Both the product itself and the documentation is updated very frequently at this point though, so stay tuned! At the time this article was published, the version was 0.11. 

### A few gotchas

_Raw recorded data only gets you so far_. Timestamps, ids and similar that are unique for each request must be excluded from the request matching manually. Also, simulating requests to a URL that generates different responses based on some state tends to be tricky. So far, your best option seems to be using the DSL to modify the responses and/or using different recordings for each test case. I suspect this may be a future focus area.

The hoverctl wrapper works well most of the time, but I've managed to generate recordings that couldn't be imported again, that fail silently and have to be looked for in the logs. Same thing when using a load testing tool that I suspect crashed the underlying process.

The Java tools don't seem to print the contents of the HoverFly logs in the output, only status messages. Therefore, e.g. request misses can be hard to detect. Controlling a remote, already running HoverFly instance in Java has also proven unreliable at times using the built in classes - the most stable way seems to be using the REST API directly.

### Alternatives

* [Wiremock](http://wiremock.org/) - Another service virtualization tool.
* [MockRestServiceServer](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/web/client/MockRestServiceServer.html) - A Spring Mock Service Template
