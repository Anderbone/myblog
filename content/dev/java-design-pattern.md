+++ 
date = "2023-11-14"
title = "Most common design patterns in Java"
tags = ["java"]
toc = true
+++

## [Stragety](https://refactoring.guru/design-patterns/strategy/java/example)

The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

 **Strategy** is a behavioral design pattern that turns a set of behaviors into objects and makes them interchangeable inside original context object.

Has-A can be better than Is-A.

![](https://i.imgur.com/z9ZYSVG.png)

Java 8 brought the support of lambda functions, which can serve as simpler alternatives to the Strategy pattern.

Here some examples of Strategy in core Java libraries:

    java.util.Comparator#compare() called from Collections#sort().

    javax.servlet.http.HttpServlet: service() method, plus all of the doXXX() methods that accept HttpServletRequest and HttpServletResponse objects as arguments.

    javax.servlet.Filter#doFilter()

Identification: Strategy pattern can be recognized by a method that lets a nested object do the actual work, as well as a setter that allows replacing that object with a different one.

Examples:

![](https://i.imgur.com/hl47XRv.png)

![](https://i.imgur.com/mPb70Xo.png)


## [Factory method](https://refactoring.guru/design-patterns/factory-method/java/example)

Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

![](https://i.imgur.com/gSaQvID.png)

The pattern is present in core Java libraries:

    java.util.Calendar#getInstance()
    java.util.ResourceBundle#getBundle()
    java.text.NumberFormat#getInstance()
    java.nio.charset.Charset#forName()
    java.net.URLStreamHandlerFactory#createURLStreamHandler(String) (Returns different singleton objects, depending on a protocol)
    java.util.EnumSet#of()
    javax.xml.bind.JAXBContext#createMarshaller() and other similar methods.

Identification: Factory methods can be recognized by creation methods that construct objects from concrete classes. While concrete classes are used during the object creation, the return type of the factory methods is usually declared as either an abstract class or an interface.

Examples:

![](https://i.imgur.com/Jnb8cp7.png)

![](https://i.imgur.com/01YGHIb.png)
Note: render() in Dialog could better be named as renderDialog() or renderWindow(), as it has nothing to do with the render() in Button class.