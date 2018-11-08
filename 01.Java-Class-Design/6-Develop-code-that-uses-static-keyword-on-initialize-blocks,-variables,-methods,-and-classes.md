# Develop code that uses static keyword on initialize blocks, variables, methods, and classes

A static member belongs to the class rather than to an instance of the class.

### Static Initialize Blocks
A static block is used to initialize a static variable or execute some initialize code since the block is executed at the time of the class loading, before any constructors or methods.
````java
class Block {  
  static {  
    System.out.println("static block executed"); 
  }
  
  Block() {
    System.out.println("constructor executed"); 
  }
  
  public static void main(String args[]) {
    new Block();
    System.out.println("main method executed"); 
  }
} 
````
The output is:
````
static block executed
constructor executed
main method executed
````
Static blocks are executed in the order they are defined.

### Statics Variables
A static variable is used to refer a common property of all objects or instances (something that is not unique for each object)  of a class. It's initialized at the time of class loading.
````java
public class Man {
  String name;
  static String gender = "M";
  
  Man(String name) {
    this.name = name;
  }
  
  void display() {
    System.out.println(name+" "+gender);
  }  
  
  public static void main(String args[]) {
    Man m1 = new Man("Bob");
    Man m2 = new Man("Richard");
    
    m1.display();
    m2.display();
  }
}
````
The output is:
````
Bob M
Richard M
````

### Static Method
A static method also belongs to the class rather than object of a class and can be invoked without the need for creating an instance of a class. The only restrictions are:
1. A static method can only access another static  member.
2. `this` and `super` cannot be used in a static method.
````java
public class Square {  
  static int calculate(int x) {  
    return x * x;  
  }  
  
  public static void main(String args[]) {  
    int result = Square.calculate(9);  
    System.out.println(result);  
  }  
} 
````

### Static Classes
We can define a class within another class. Such a class is called a nested class. We can't make a top level class static. Only nested classes can be static.

````java
class OuterClass {
   // Static nested class
   public static class NestedStaticClass {
       public void print() { 
         System.out.println("Message from nested static class"); 
       }
    }
} 

public class Test {
    public static void main(String args[]) {
       // create instance of nested Static class
       OuterClass.NestedStaticClass sc = new OuterClass.NestedStaticClass();

       // call non static method of nested static class
       sc.print();
    }
}
````

The characteristics of a static nested class are:
* Nested static classes don't need a reference to their outer class (the enclosing class)
* Only static members of the outer class are accessible in a nested static class
