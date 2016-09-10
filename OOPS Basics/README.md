# Object Oriented Programming

Referring to [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/concepts/object.html)

Advantages
* Modularity and code reuse
* better code maintenance
* Closely simulates real world events

## Object

Consists of state and behavior. It is an instance of a class. State of an object can be changed using the methods exposed by it.  
e.g. Man  
    *State* - Color, Name, Height, Weight, Age
    *behavior* - Eats, Runs, Talks, Works

## Class

Logical entity which is a collection of Objects.
Blueprint of an object.
It is also a type in Java.

## Inheritance

Classes can inherit commonly used state and behavior from other classes using **Inheritance**.  
In Java, a class can extend only one superclass.

*Advantages* - Code reusability and runtime polymorphism

e.g.  
*Superclass* - Car  
*Subclass* - Sedan, SportsCar, Suv, Electric

## Encapsulation

Encapsulation is the mechanism to wrap state/data and methods/behavior/actions into a single unit. This unit is called as class in Java.  
It is also an information-hiding mechanism. An object can hide data and methods using access specifiers thereby only exposing the desired ones.  

e.g. The fields/variables of a class can be declared as private. These can be modified and accessed only using the public getter and setter methods.

## Abstraction

Abstraction is hiding the implementation details from the user and exposing only the functionality to the user. Java provides abstraction using abstract classes and interfaces.

e.g. The car example. ;-) The user just needs to know how to drive a car instead of wondering about how the car engine works.

## Polymorphism

Polymorphism is performing one task in different ways. This generally arises from inheritance where we have an 'Is-a' relationship between classes.

e.g. Consider a superclass A with a method printDetails(). Now, classes B, C and D extend the superclass A. Each of these subclasses has a method printDetails() but with a different implementation.
```java
class A {
  public void printDetails() {
    System.out.println("A");
  }
}

class B extends A {
  public void printDetails() {
    System.out.println("B");
  }
}

class C extends A {
  public void printDetails() {
    System.out.println("C");
  }
}

class D extends A {
  public void printDetails() {
    System.out.println("D");
  }
}
```
Now, we define a test class to show polymorphic behavior.
```java
public class Test {
  public static void main (String [] args) {
    //creating references of type A
    A referenceA1, referenceA2, referenceA3, referenceA4;
    referenceA1 = new A();
    referenceA2 = new B();
    referenceA3 = new C();
    referenceA4 = new D();

    referenceA1.printDetails();
    referenceA2.printDetails();
    referenceA3.printDetails();
    referenceA4.printDetails();
  }
}  
```
Output:  

    A
    B
    C
    D

From [Tutorials Point](http://www.tutorialspoint.com/java/java_polymorphism.htm) -
*Polymorphism is the ability of an object to take on many forms. In Java, all Java objects are polymorphic since any object will pass the IS-A test for their own type and for the class Object.*

**Method Overloading and Method Overriding**

Note - Two methods have the same signature if they have the same name and argument types.  

Method Overloading - Methods within the same class with different signatures. Overloaded methods are differentiated by the number and the type of the arguments passed into the method. The *return type* is not considered a part of this differentiation.

[Method Overriding](https://docs.oracle.com/javase/tutorial/java/IandI/override.html) - Overriding is possible because of the ability of a reference variable to refer to any object of its declared type or any subtype of its declared type. A reference variable can be declared as a class or interface type.  
*It is a compile-time error if an instance method overrides a static method.* Also, the access modifier of an overriding or hiding method must provide at least as much access as the overridden or hidden method.
**Return types** - In overriding the return types must match if they are void or of primitive type. If they are of reference type then there must be a parent-child/Is-a relation.
**Throws** - The overriding method must not throw more checked exceptions than the overridden or hidden method. Also, the overriding method must throw the same or supertype exception for every checked exception thrown by the overridden method.  
Read more about Overriding [here](http://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html#jls-8.4.8)

Sample Question from above link-  
```java
class Super {
    static String greeting() { return "Goodnight"; }
    String name() { return "Richard"; }
}
class Sub extends Super {
    static String greeting() { return "Hello"; }
    String name() { return "Dick"; }
}
class Test {
    public static void main(String[] args) {
        Super s = new Sub();
        System.out.println(s.greeting() + ", " + s.name());
    }
}
```

Output-

    Goodnight, Dick  
Logic- Remember, static methods have nothing to do with objects. So, type of the reference (in this case *Super*) is used to invoke static methods.

* Static / Compile-Time / Early Binding - This is method overloading

* Dynamic / Runtime / Late Binding- This is method overriding

Virtual method invocation

From [Java docs](http://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html) -
Hiding Fields - If the class declares a field with a certain name, then the declaration of that field is said to hide any and all accessible declarations of fields with the same name in superclasses, and superinterfaces of the class.

A hidden field can be accessed by using a qualified name if it is static, or by using a field access expression that contains the keyword super or a cast to a superclass type.  

[Overriding private method](http://stackoverflow.com/questions/11976446/can-a-private-method-in-super-class-be-overriden-in-the-sub-class) - Cannot be done as it is not visible .
```java
class Base {
	private void func() {
		System.out.println("In base func method");
	};

	public void func2() {
		System.out.println("func2");
		func();
	}
}

class Derived extends Base {
	//@Override - Un-commenting this annotation gives compile time error
	public void func() { // Is this an overriding method?
		System.out.println("In Derived Class func method");
	}
}

class Learning {
	public static void main(String[] args) {
		Derived D = new Derived();
		D.func2();
	}
}
```
*Also, a subclass instance method cannot override a supercalss static method*

## Interface

Interfaces are like contracts between the class and the outside world. It is a collection of methods with no Implementation.

e.g. class ACMEBicycle **implements** Bicycle {

The interface itself can have any desired access specifier but the interface body follows a certain set of rules.

The interface body can contain abstract methods, default methods, and static methods.  
All methods in an interface are **implicitly** public, so you can omit the public modifier (even for default methods).  
*So, a class implementing an interface has to implement all the methods of the interface with the public access specifier.*  
All constant values defined in an interface are implicitly **public, static, and final.** Once again, you can omit these modifiers  
Also, from [Java docs](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html) - *Methods in an interface that are not declared as default or static (so an interface can have static and default methods) are implicitly abstract, so the abstract modifier is not used with interface methods. (It can be used, but it is unnecessary.)*

* In Java , an interface can have static and default methods which are not abstract. These methods also become public because of interface property. refer [Java docs](https://docs.oracle.com/javase/tutorial/java/IandI/defaultmethods.html)
* Also, remember the **differences between interfaces and abstract class**. From [java docs](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)- "Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation. However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all fields are automatically public, static, and final, and all methods that you declare or define (as default methods) are public. In addition, you can extend only one class, whether or not it is abstract, whereas you can implement any number of interfaces." The following list is from [Javatpoint](http://www.javatpoint.com/difference-between-abstract-class-and-interface)

Abstract | Interface
-------- | ---------
Abstract class can have abstract and non-abstract methods. | Interface can have only abstract methods.
Abstract class doesn't support multiple inheritance. | Interface supports multiple inheritance.
Abstract class can have final, non-final, static and non-static variables. | Interface has only static and final variables.
Abstract class can have static methods, main method and constructor. | Interface can't have static methods, main method or constructor.
Abstract class can provide the implementation of interface. | Interface can't provide the implementation of abstract class.
The abstract keyword is used to declare abstract class. | The interface keyword is used to declare interface.

## Package

Package is similar to a folder in an Operating System. It provides a namespace to organize related classes and interfaces.

## Composition
* #### Is-a
* #### Has-a
