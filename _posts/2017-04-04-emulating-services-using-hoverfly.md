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

<img src="/images/hoverfly_simulate.png" alt="Capture sequence">

### When to use a service virtualization tool

A stub is a minimal implementation that works as a stateful substitute, often with hard-coded values. A mock is more like an empty interface that verifies behaviour, with data set up manually for each test. Mocks are typically used for cases where the behaviour is more complex, but both of them work perfectly well in most cases for removing dependencies.

When you are dealing with many service interactions in a test, as can be the case with microservices, setting up the data manually for each test can be tough. Recording the interactions and replaying them becomes a good option, and service virtualization does that for you.

If you have external service dependencies that are unstable, you can emulate them using an external service rather than changing your own system. 

Injecting faults, latency and similar becomes more realistic when used through an external system instead of modifying your system. 

You can use service virtualization as a tactical approach to working with services that don't exist yet, or to extend services.

### Getting started with HoverFly

[The tutorials of the HoverFly documentation](https://docs.hoverfly.io/en/latest/pages/tutorials/tutorials.html) are quite good, and provide excellent examples of most use cases. I'd suggest starting with reading up on the [key concepts](https://docs.hoverfly.io/en/latest/pages/keyconcepts/keyconcepts.html), then following the tutorials for: 

* Capturing and exporting data
* Simulating and importing data
* Request matching 

Another interesting service you can use, besides [jsontest](http://time.jsontest.com/) that they refer to in the documentation, is [httpbin](http://httpbin.org/). It's really a collection of simple but useful services that responds with the e.g. exact GET-request it received, or the originating IP, or some sample XML or JSON. Quite nifty.

**Note:** Both the product itself and the documentation is updated very frequently at this point though, so stay tuned!

### A few gotchas

_Raw recorded data only gets you so far_. Timestamps, ids and similar that are unique for each request must be excluded from the request matching manually. Also, simulating requests to the same URL that generate different responses tends to be tricky. So far, your best option seems to be using the DSL and/or different recordings for each test case. I suspect this may be a future focus area.

The hoverctl wrapper works well most of the time, but I've managed to generate recordings that couldn't be imported again, that fail silently. Same thing when using a load testing tool that I suspect crashed the underlying process. It's usually visible in the logs though, but you have to look for it.

The Java tools don't seem to print the contents of the HoverFly logs in the output, only status messages. Therefore, request misses can be hard to detect. Controlling a remote, already running HoverFly instance in Java has also proven difficult using the built in classes - the most stable way seems to be using the REST API directly.

### Some similar tools worth mentioning

* [Wiremock](http://wiremock.org/) - Another service virtualization tool.
* [MockRestServiceServer](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/web/client/MockRestServiceServer.html) - A Spring Mock Service Template
