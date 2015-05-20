#Implement inheritance including visibility modifiers and composition

###Inheritance
With inheritance, you created classes based on the other classes so they can get the attributes and methods from the base class to reuse them and even redefine them.

The keyword `extends` is used to make a new class that derives from an existing class. The base class is called the superclass and the new class is called the subclass.

Let's begin for example with this class:
````java
public class Animal {
  public void eat() { /* Do something */ }
}
````
A subclass can be:
````java
public class Dog extends Animal {
}
````
By inheriting from *Animal*, the *Dog* class automatically gets the method `eat()`. We can add a method to the class:
````java
public class Dog extends Animal {
  public void bark() { /* Do something */ }
}
````
So now *Dog* has two methods, `eat()` that is inherited from *Dog* and `bark()` that is specific to the *Dog* class. *Animal* still has one method, inheritance only works from the superclasses to the subclasses.

Not everything can be inherited, and this depends directly from the used visibility modifiers.

When a subclass extends a superclass in Java, all protected and public attributes and methods of the superclass are inherited by the subclass. Attributes and methods with default (package) access modifiers can be accessed by subclasses only if the subclass is located in the same package as the superclass. Private attributes and methods of the superclass are not inherited.

| Modifier | Inherited |
| :----------------: |:------------:|
| public | Yes |
| protected | Yes |
| default | Only for subclasses in the same package |
| private | No |

When you create a subclass, the methods in the subclass cannot have less accessible access modifiers assigned to them than they had in the superclass. For instance, if a method in the superclass is public then it must be public in the subclass too.

In Java, a class is only allowed to inherit from a single superclass (singular inheritance). In some programming languages, like C++, it is possible for a subclass to inherit from multiple superclasses (multiple inheritance).

###Composition
You do composition by having an instance of another class as a field of your class instead of extending.

When to use which?
* If there is an IS-A relation, inheritance is likely to be preferred.
* If there is a HAS-A relationship, composition is preferred.

For example:
````java
class Toy {} 

class Animal{} 

// Cat is an Animal, so Cat class extends Animal class.
class Cat extends Animal { 
 // Cat has a Toy, so Cat has an instance of Toy as its member.
 private Toy toy; 
}
````

Favoring composition over inheritance is a popular object oriented design principle that helps to create flexible and maintainable code. For example, composition facilitates testing. If one class is composed of another class, you can easily create a mock object representing the composed class.
