# Non-access Modifiers

## Learning Goals

- Explain the different non-access modifiers in Java
- Use non-access modifiers

## Introduction

In the previous lesson, we learned about **access modifiers**. We've seen
other types of keywords used other than the access modifier keywords though.
For example:

`public static void main(Stringp[] args`

In this lesson we will focus on the next keyword `static` and what that means.

## What are Non-Access Modifiers?

Non-access modifiers apply to classes, methods, variables and constructors and
indicate their desired behavior to the compiler.

Here is the list of non-access modifiers that are in scope for this discussion:

1. `static` - static methods and variables are also called "class" variables or
   methods because they do not require an instance of the class to be used.
2. `final` - final classes, methods or variables mean that they cannot be
   modified, which manifest itself different for classes, methods and variables.

## Static

A `static` member of a class (i.e. a variable or a method) is a member that can be
accessed directly on the class without needing an instance of that class to be created.
This is usually the case when we describe something about the class that will
be true for all instances of that class.

In Java, any class that we want to be able to run from the command line needs to have a
`public` (i.e. fully accessible)`static` (i.e. accessible through the class, without an object)
method called `main` because the JVM needs to be able to call it without an object since it
doesn't know anything about the values that might be required to properly create an instance.

In our previous `Bicycle` class, we could have a variable `numWheels` that represents the
number of wheels that a bicycle has. We could say it's `static` because all our bikes will
always have exactly two wheels. Here is the `Bicycle` class with the `numWheels`
variable added:

```java
public class Bicycle {
    String color; 
    int height;
    static int numWheels; 
} 
```

We can now access this static variable via the class without having and instance of it:

```java
public static void main(String[] args) {
    int wheels = Bicycle.numWheels;
    System.out.println(wheels);
}
```

The same field can also be accessed through an instance of the class:

```java
Bicycle johnsBike = new Bicycle();
Bicycle clariesBike = new Bicycle();
clairesBike.numWheels = 1;
System.out.println(Bicycle.numWheels);
```

The problem with the code above is that all bicycles now have only one wheel instead of
two because the `numWheels` variable is static and therefore shared across all instances
of the `Bicycle` class. The following would be the output from the print statement:

```java
1
```

There are two ways to deal with this problem, one that we're familiar with and
one that introduces a new concept.

1. We could make the `numWheels` field in the `Bicycle` class `private` so that it
can no longer be modified from outside the class. This would work for the code above;
however, it does not completely solve the problem because the methods inside the
`Bicycle` class could still modify the value for the `numWheels` field, in which case
it would be modified for all instances of that class.
2. Another way we could address this problem is to make the variable `final`. Let's
look at that keyword next!

## Final

A `final` variable is a variable with a value that cannot be changed once it's
been initialized. It is often used in conjunction with the `static` modifier to
handle "constants".

In our `Bicycle` example, we could make the `numWheels` variable `public`, but
also make it `final` so that it cannot be modified by anyone, either outside of
the `Bicycle` class or even within the `Bicycle` class itself:

```java 
public class Bicycle {
    String color; 
    int height;
    public static final int NUM_WHEELS; 
} 
```

Note that when constants are defined, in Java, we usually depict constants with a
variable name in all capital letters and underscores for separation of words.

We can now access the `NUM_WHEELS` variable in the `Bicycle` class without needing
to instantiate an instance of it, but we cannot modify its value from anywhere,
which means it's a constant value that we can rely on.
