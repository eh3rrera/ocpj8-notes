#Implement polymorphism

With inheritance, you can take advantage of polymorphism. Polymorphism is based on the fact that you can use a variable of a superclass type to hold a reference to an object whose class is any of its subclasses, for example:
````java
Animal animal = new Dog();
````

This way, polymorphism allows the program to act differently based on the object performing the action. For example:
````java
class Animal {
  public void eat() {
    System.out.println("Animal Food");
  }
}
class Dog extends Animal {
  public void eat() {
    System.out.println("Dog Food");
  }
}
class Cat extends Animal {
  public void eat() {
    System.out.println("Cat Food");
  }
}
public class Test {
  public static void main(String args[]) {
    Animal a = new Dog();
    System.out.println(a.eat());
    a = new Cat();
    System.out.println(a.eat());
  }
}
````
The first `System.out.println(a.eat());` will print *Dog Food* since in that moment, the *a* reference is holding a *Dog* object. In the second call, it will print *Cat Food*, since now the reference holds a *Cat* object.

So polymorphism can help make code easier to change. If you have a fragment of code that uses a variable of a superclass type, such as *Animal*, you could later create a brand new subclass with another behavior, such as *Spider*, polymorphism will ensure that *Spider*'s implementation of *Animal*'s method gets executed and the fragment will work without change. 
