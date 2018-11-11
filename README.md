# Design_Patterns_Samples
Implementation of DESIGN PATTERNS in Java


# Design Patterns

History:
  Christopher Alexander was the first person who invented all the above Design Patterns in 1977.
  But later the Gang of Four - Design patterns, elements of reusable object-oriented software book was written by a group of four persons named as Erich Gamma, Richard Helm, Ralph Johnson and John Vlissides in 1995.
  That's why all the 23 Design Patterns are known as Gang of Four (GoF) Design Patterns.

"A software design pattern is a general reusable solution to a commonly occurring problem within a given context in software design" 
--- Wikipedia

Design patterns, as name suggest, are solutions for most commonly (and frequently) occurred problems while designing a software. These patterns are mostly “evolved” rather than “discovered”. A lot of learning, by lots of professional, have been summarized into these design patterns. None of these patterns force you anything in regard to implementation; they are just guidelines to solve a particular problem – in a particular way – in particular contexts. Code implementation is your responsibility.

# Advantage of design pattern:
They are reusable in multiple projects.
They provide the solutions that help to define the system architecture.
They capture the software engineering experiences.
They provide transparency to the design of an application.
They are well-proved and testified solutions since they have been built upon the knowledge and experience of expert software developers.
Design patterns don?t guarantee an absolute solution to a problem. They provide clarity to the system architecture and the possibility of building a better system.

# Types of patterns
1. Creational Design Patterns
2. Structural Design Patterns
3. Behavioral Design Patterns

# Creational Design Patterns
Creational patterns often used in place of direct instantiation with constructors. They make the creation process more adaptable and dynamic. In particular, they can provide a great deal of flexibility about which objects are created, how those objects are created, and how they are initialized.

# Structural Design Patterns
These design patterns show you how to glue different pieces of a system together in a flexible and extensible fashion. Structural patterns help you guarantee that when one of the parts changes, the entire structure does not need to change.

# Behavioral Design Patterns
A behavioral pattern abstracts an action you want to take from the object or class that takes the action. By changing the object or class, you can change the algorithm used, the objects affected, or the behavior, while still retaining the same basic interface for client classes.


## Creational Design Patterns
Default way of creating object is- new ClassName(parms...);

# Singleton
When an application wants to have one and only one instance of any class per JVM, in all possible scenarios without any exceptional condition.Singleton pattern restricts the instantiation of a class and ensures that only one instance of the class exists in the Java virtual machine. The singleton class must provide a global access point to get the instance of the class. Singleton pattern is used for logging, driver objects, caching and thread pool. Singleton design pattern is also used in other design patterns like Abstract Factory, Builder, Prototype, Facade etc.

## How to create Singleton:
To implement Singleton pattern, there are really many approaches but all of them have following common concepts:
  A private constructor to avoid instantiation of the class,
  A private static variable from the same class that's the only instance of the class.
  public static method that returns the instance of the class, this is the global access point for the outer world to get the instance of the class.

## Examples:
In-built Examples:
  java.lang.Runtime.getRuntime(): This method gives Runtime class that has only one instance in a JVM.
  java.lang.System.getSecurityManager(): This method returns a SecurityManager for the current platform. java.awt.Desktop.getDesktop()

Custom Examples
  Connection Pool class
  Persistence Manager class


## Advantages

## Disadvantages


# Builder
This is an alternative way to construct complex objects and should be used only when you want to build different immutable objects using same object building process.

## Examples:
In-built JDK Implementation:
  All implementations of java.lang.Appendable are infact good example of use of Builder pattern in java. e.g.
  java.lang.StringBuilder#append() [Unsynchronized class]
  java.lang.StringBuffer#append() [Synchronized class]
  java.nio.ByteBuffer#put() (also on CharBuffer, ShortBuffer, IntBuffer, LongBuffer, FloatBuffer and DoubleBuffer)


Custom Examples

## Advantages
Undoubtedly, the number of lines of code increase at least to double in builder pattern, but the effort pays off in terms of design flexibility and much more readable code. The parameters to the constructor are reduced and are provided in highly readable method calls.
Builder pattern also helps minimizing the number of parameters in constructor and thus there is no need to pass in null for optional parameters to the constructor.
Another advantage is that Object is always instantiated in a complete state rather than sitting in an incomplete state until the developer calls (if ever calls) the appropriate “setter” method to set additional fields.

And I finally I can build immutable objects without much complex logic in object building process.

## Disadvantages
The client code is more verbose.


# Prototype
A prototype is a template of any object before the actual object is constructed. In java also, it holds the same meaning. Prototype design pattern is used in scenarios where application needs to create a number of instances of a class, which has almost same state or differs very little.

In this design pattern, an instance of actual object (i.e. prototype) is created on starting, and thereafter whenever a new instance is required, this prototype is cloned to have another instance. The main advantage of this pattern is to have minimal instance creation process which is much costly than cloning process.
Lets understand this pattern using an example. I am creating an entertainment application that will require instances of Movie, Album and Show classes very frequently. I do not want to create their instances everytime as it is costly. So, I will create their prototype instances, and everytime when i will need a new instance, I will just clone the prototype.

## Examples:
In-built Examples:

Custom Examples

## Advantages

## Disadvantages


# Factory
This is most suitable where there is some complex object creation steps are involved. To ensure that these steps are centralized and not exposed to composing classes, factory pattern should be used. We may not always know what kind of objects we want to create in advance.
Some objects can be created only at execution time after a user requests so.

Examples when you may use a factory method:

A user may click on a certain button that creates an object.
A user may create several new documents of different types.
If a user starts a webbrowser, the browser does not know in advance how many tabs (where every tab is an object) will be opened.

## Examples:
In-built Examples:

Custom Examples

## Advantages

## Disadvantages

# Abstract factory
Whenever you need another level of abstraction over a group of factories, you should consider using abstract factory pattern.

## Examples:
In-built Examples:

Custom Examples

## Advantages

## Disadvantages

************** WORK IN PROGRES ****************
















References:
1. https://howtodoinjava.com/gang-of-four-java-design-patterns/
2. https://github.com/sdmg15/Java-design-patterns
3. https://www.javatpoint.com/design-patterns-in-java
