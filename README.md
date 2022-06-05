# Non-access Modifiers

## Learning Goals

- Explain the different non-access modifiers in Java
- Use non-access modifiers

## Introduction

Non-access modifiers apply to classes, methods, variables and constructors and
indicate their desired behavior to the compiler.

Here is the list of non-access modifiers that are in scope for this discussion:

1. `static` - static methods and variables are also called "class" variables or
   methods because they do not require an instance of the class to be used
2. `final` - final classes, methods or variables mean that they cannot be
   modified, which manifest itself different for classes, methods and variables

## Static

A `static` variable is a variable that belongs to the class where it's defined
and does not require an instance of the class to be created in order to be used.
This also means that all instances of the class will share the same actual value
for this particular variable.

Let's consider a `Student` class where we want to create a field that is a text
version of the type of user a student is. In this example, all students have a
user type of "Student", so it would not make sense to initialize a variable with
that value every time we create a new instance of the `Student` class. In this
case, we make the `userType` field `static` and share it across all student
instances:

```java
public class Student {
    public static String userType = "Student";

    // ...
}
```

This class variable, as static variable are known, can now be accessed via the
class without having an instance of it:

`System.out.println("Students' user type is: " + Student.userType);`

The same field can also be accessed through an instance of the class:

```java
Student raj = new Student("Raj", "Singh");
Student eva = new Student("Eva", "Dupont");
eva.userType = "Special Student";

System.out.println("Students' user type is: " + Student.userType);
System.out.println("Eva's user type is: " + Student.userType);
System.out.println("Raj' user type is: " + Student.userType);
```

The problem with the code above is that all students now have a type of "Special
Student", because the `userType` variable is static and therefore shared across
all instances of the `Student` class, as you can see from the code's output:

```
Students' user type is: Special Student
Eva's user type is: Special Student
Raj' user type is: Special Student
```

There are two ways to deal with this problem, one that we're familiar with and
one that introduces a new concept.

We could make the `userType` field in the `Student` class `private` so that it
can no longer be modified from outside the class. This would work for the code
above, but does not completely solve the problem, because methods inside the
`Student` class could still modify the value for the `userType` field, in which
case it would be modified for all instances of that class.

Another way to address this problem is to make the variable `final`, which we
will examine in the next session.

The `static` modifier can also be applied to methods and classes. For methods,
it means they can be accessed without needing an instance of that class, just
like variables. We have been using the `main()` method for all our classes we
need to run from the command line - that method is always `static` because the
JVM needs to be able to call it without being able to initialize our class,
since it doesn't know anything about the values that might be required to
properly create an instance.

Only inner classes can be `static`, which means they don't need to be
instantiated to be used, and it also means they can only access the `static`
members of their outer class.

## Final

A `final` variable is a variable with a value that cannot be changed once it's
been initialized. It is often used in conjunction with the `static` modifier to
handle "constants".

In our `Student` example, we could make the `userType` variable `public`, but
also make it `final` so that it cannot be modified by anyone, either outside of
the `Student` class or even within methods of the `Student` class itself:

```java
public class Student {
    public static final String userType = "Student";

    // ...
}
```

Now we can access the `userType` variable in the `Student` class without needing
to instantiate an instance of it, but we cannot modify its value from anywhere,
which means it's a constant value that we can rely on.
