#Develop code that declares, implements and/or extends interfaces and use the atOverride annotation
###Interfaces
An interface is like an abstract class, except that it cannot contain an implementation of the methods, only their signature (return type, name, parameters and exceptions).

An interface is declared using the interface keyword. Just like classes, an interface can be declared public or with package scope (no access modifier).
````java
public interface Vehicle {
    public String serie = "XXX";
    public void start();
}
````
The variables declared in an interface are public, static and final by default. The methods are public and abstract by default.

Before you can use an interface, it must be implemented by some class:
````java
public class Truck implements Vehicle {
    public void start() {
        System.out.println("Starting truck...");
    }
}
````
A class that implements an interface must implement all the methods declared in the interface. The only exception are default methods. Java 8 introduces this feature, that provides the flexibility to allow an interface to define an implementation which will be used as default in the situation where a class fails to provide an implementation for that method.

This is made by adding the keyword `default` before the method's access modifier and adding the implementation inside interface:
````java
interface Vehicle {
    default public void start() {
        System.out.println("Default start");
    }
}

class Car implements Vehicle {
    // valid in Java 8
}
````java

Once a class implements an interface, an instance of that class can be assigned to a reference of the interface type:
````java
Vehicle truck = new Truck();
````

A class can implement multiple interfaces. In that case, the class must implement all the methods declared in all the interfaces implemented:
````java
interface Run {
    public void run();
}
interface Sleep {
    public void sleep();
}
public class Man
    implements Run, Sleep {

    public void run() {
        System.out.println("run");
    }

    public void sleep() {
        System.out.println("sleep");
    }
}
````
An interface cannot extend from another class or implement another interface. It can only extend another interface(s):
````java
interface Run {
    public void run();
}
interface Sleep {
    public void sleep();
}
interface Behavior extends Run, Sleep {
}

public class Man
    implements Behavior {

    public void run() {
        System.out.println("run");
    }

    public void sleep() {
        System.out.println("sleep");
    }
}
````
If a class implements *Behavior*, it has to implement all methods defined in both *Run* and *Sleep* interfaces.

###atOverride Annotation
Whe you use the `@Override` annotation, the compiler checks to make sure you're actually overriding a method. For example, if you misspell the method name or not match the parameters correctly, you will be warned that you're not actually overriding a method of the superclass.  

The most common use case for `@Override` is with *Object* methods:
````java
public class Test {
  @Override
  public String toString() {
    /** Do something */
  }
  @Override
  public boolean equals(Object) {
    /** Do something */
  }
  @Override
  public int hashCode() {
    /** Do something */
  }
}
````
