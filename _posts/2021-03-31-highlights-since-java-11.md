---
layout: post
title:  "Highlights since Java 11"
---

## Contents
{: .no_toc}

* Table of Contents
{:toc}

## All changes
Before we start with the highlights: in case you want to learn more or have a complete view of all changes, just head to the [Open JDK website](https://openjdk.java.net/projects/jdk/).

## Java 12
Not very interesting as a whole, but there are a few things to note at least. 

### String indentation and transforms
```java
"text".indent(2); // adds two spaces
"text".indent(-2); // removes two spaces

String transformed = "text".transform(value ->
      new StringBuilder(value).reverse().toString()
);
```
### Files.mismatch
```java
long diff = Files.mismatch(fileA, fileB); 
// -1 means no diff, otherwise returns the first byte that differs
```
### Collectors.teeing
```java
double mean = Stream.of(1, 2, 3, 4, 5)
      .collect(Collectors.teeing(
             Collectors.summingDouble(i -> i), 
             Collectors.counting(), 
             (sum, count) -> sum / count)); // fork then join stream
```
### Compact number formatting
```java
NumberFormat likesShort = 
      NumberFormat.getCompactNumberInstance(
           new Locale("en", "US"), 
           NumberFormat.Style.SHORT);
likesShort.setMaximumFractionDigits(2);
likesShort.format(2592); // "2.59K"
```

## Java 13
### Nothing of interest really..
Just a bunch of previews, garbage collection and under the hood improvements.

## Java 14
Compact switch cases is a nice addition, and JFR monitoring of live applications is niche, but useful.

### Switch Expressions (JEP 361)
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
};
```

### Java Flight Recorder Event Streaming (JEP 349)
Monitoring of code running live, e.g. in production, with low overhead

## Java 15
Text blocks are nice, and sealed classes can be useful for library applications.

### Text Blocks (JEP 378)
```java
String html = """
              <html>
                  <body>
                      <p>Hello, world</p>
                  </body>
              </html>
              """;
```

### Sealed Classes (JEP 360)
```java
public abstract sealed class Person permits Employee, Manager {} 
// only allows Employee and Manager as sub-classes. 
// Also works for interfaces

public final class Employee extends Person {}
public non-sealed class Manager extends Person {}
```

### New garbage collection features (JEP 377 and JEP 379)
ZGC and Shenandoah are no longer experimental, although G1 is still the default.

## Java 16
Records are finally here! Pattern matching is a nice addition, although in itself not a huge improvement. Better NullPointerExceptions are also long overdue as the default!

### Pattern Matching for instanceof (JEP 394)
```java
if (obj instanceof String) {
    obj.getBytes() // Use obj as String without casting
}
```

### Records (JEP 395)
```java
record Point(int x, int y) {
  Point {
    if (x != y)  // implicit constructor parameters
      throw new IllegalArgumentException("..."));
    }
}

Point a = new Point(1,1);
a.x();
a.toString();
a.equals();
```

### Helpful NullPointerExceptions (JEP 358)
```java
int[] arr = null;
arr[0] = 1;

java.lang.NullPointerException: 
    Cannot store to int array because "arr" is null
```

### Packaging Tool (JEP 392)
Create native install packages (msi, deb, rpm etc.) using the JDK.

### Warnings for Value-Based Classes (JEP 390)
```java
Integer a = new Integer(0); // Warning! 
// Should use Integer.valueOf(0) or auto-boxing with 0
```