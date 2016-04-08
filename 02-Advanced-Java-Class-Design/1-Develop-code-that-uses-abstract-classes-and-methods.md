#Develop code that uses abstract classes and methods

An abstract class is a class that is declared `abstract`. Abstract classes cannot be instantiated, only subclassed.
````java
abstract class Animal {
  public void eat() {}
}
````

An abstract method is a method that is declared without an implementation, like this:
````java
public abstract void method(int arg);
````
If a class includes an abstract method, it has to be declared abstract. When an abstract class is subclassed, if the subclass doesn't provide an implementation for the inherited abstract methods, it has to be declared abstract as well.
````java
abstract class Animal {
  public void eat() {
   /** Do something */
  }
  public abstract makeSound();
}
class Dog extends Animal {
  public makeSound() {
    System.out.println("Bark");
  }
}
````

If an abstract class has static members, you can use them with a class reference (`AbstractClass.staticMethod()`) as you would with any other class.

Abstract classes are similar to interfaces. However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all fields are automatically public, static, and final, and all methods that you declare or define are public. In addition, you can extend only one class, whether or not it is abstract, whereas you can implement any number of interfaces.

Use abstract classes when:
* You want to share code among several closely related classes.
* You expect that classes that extend your abstract class have many common methods or fields, or require access modifiers other than public (such as protected and private).
* You want to declare non-static or non-final fields. This enables you to define methods that can access and modify the state of the object to which they belong.

Use interfaces when:
* You expect that unrelated classes would implement your interface. For example, the interfaces *Comparable* and *Cloneable* are implemented by many unrelated classes.
* You want to specify the behavior of a particular data type, but not concerned about who implements its behavior.
* You want to take advantage of multiple inheritance of type.
