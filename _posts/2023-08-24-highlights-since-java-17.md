---
layout: post
title:  "Highlights of new features between Java 18 and 21"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## All changes
Before we start with the highlights: in case you want to learn more or have a complete view of all changes, just head to the [Open JDK website](https://openjdk.java.net/projects/jdk/).

## Java 18
UTF-8 by default, code snippets allowed in Javadoc, a bundled http server and deprecation of finalizers (try-catch-finally) in favor of try with resources. Not very exciting.

### Simple Web Server
```bash
$ jwebserver -p 9000
```

```java
var server = SimpleFileServer.createFileServer(
    new InetSocketAddress(8080), 
    Path.of("/some/path"), 
    OutputLevel.VERBOSE);
server.start
```

## Java 19
No real features introduced, mainly previews.

## Java 20
No real features introduced, mainly previews (again).

## Java 21 (LTS)
This is where stuff gets released - not a ton, but a few nice additions!

### Sequenced collections
A new interface called `SequencedCollection<E>` that represents collections with a specific sequence of elements, for traversal in reverse order and similar.

### Pattern matching for Records (JEP 440)
In the same way that instanceof type inference was introduced in Java 16, the same is now available for Records.

### Pattern matching for switch (JEP 441)
You can now use a more compact switch syntax, add cases for nulls and even simple logic to select cases. 

```java
static String typing(Object obj) {
    return switch (obj) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case Double d  -> String.format("double %f", d);
        case String s  -> String.format("String %s", s);
        default        -> obj.toString();
    };
}
```
```java
static void logic(String s) {
    switch (s) {
        case null         -> System.out.println("Oops");
        case "Foo", "Bar" -> System.out.println("Great");
        case String s when s.length() == 1 -> System.out.println("One");
        default           -> System.out.println("Ok");
    }
}
```

### Virtual threads (JEP 444)
Lightweight threads (like goroutines etc.) in Java, to enable using a threading model that scales with web server requests and similar.

```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    IntStream.range(0, 10_000).forEach(i -> {
        executor.submit(() -> {
            Thread.sleep(Duration.ofSeconds(1));
            return i;
        });
    });
}  // executor.close() is called implicitly, and waits
```

### Key Encapsulation Mechanism (JEP 452)
For cryptographical purposes, securing symmetrical keys.