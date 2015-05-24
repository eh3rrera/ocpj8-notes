An inner class is a class declared inside another class.
 
###Static Inner Class
A inner class declared with the static keyword becomes a static inner class, for example:
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
    public static void main(String args[]){
       // create instance of nested Static class
       OuterClass.NestedStaticClass sc = new OuterClass.NestedStaticClass();

       // call non static method of nested static class
       sc.print();
    }
}
````

The rules of a static nested class are:
* Nested static clases don't need a reference of their outer class (the enclosing class)
* Only static members of the outer class are accessible in a nested static class

###Local Inner Class
A class created inside a method or a block is called local inner class. If you want to use a local inner class, you must instantiate it inside the method or block.
````java
public class LocalClass{  
 private int n = 5;
 
 void result(){  
   // Local inner class
   class Cube {  
     int calc() {
        return n*n*n;
     }  
   }
  
   Cube c = new Cube();  
   System.out.println(c.calc());  
 }  
 
 public static void main(String args[]) {  
    LocalClass lc = new LocalClass();  
    lc.result();  
 }  
}  
````
The rules of a local inner class are:
* Local inner class cannot be invoked from outside the method.
* Since java 8, it's possible to access the non-final local variables in a local inner class.

###Nested class
A nested class or member inner class is a non-static class that is created inside a class but outside a method.
 ````java
class OuterClass {
   // Nested class
   public static class NestedClass {
       public void print() { 
         System.out.println("Message from nested class"); 
       }
    }
} 

public class Test {
    public static void main(String args[]){
       // create instance of outer class
       OuterClass oc = new OuterClass();
       // create instance of nested Static class
       OuterClass.NestedClass nc = oc.new NestedClass();

       // call non static method of nested static class
       sc.print();
    }
}
````

The rules of a nested class are:
* Nested  clases need a reference of their outer class
* Static and non-static members of the outer class are accessible in a nested  class
* If the nested class is used inside the class that defines it, the keyword this can be used to create an instance of the nested class (for example `OuterClass.NestedClass nc = this.new NestedClass();`)

###Anonymous Inner Class
Anonymous Inner classes are classes without name (but not without type) used to override a method of class or interface. They can'y have constructors.
````java
interface Animal {  
  void eat();  
}  
public class Test {  
  public static void main(String args[]){  
    Animal a = new Animal(){  
      public void eat() { System.out.println("eat"); }  
    };  
    a.eat();  
  }  
} 
````

The code:
````java
    Animal a = new Animal() { //This is the only case where you can use the keyword 'new' with an interface
      public void eat() { System.out.println("eat"); }  
    }; 
````
Represents:
* A class that is created but have its name decided by the compiler
* The class implements the *Animal* interface and provides the implementation of the *eat* method.
* An object is created and referred by the *a* variable of *Animal* type.

The rules to access variables in anonymous classes are:
* An anonymous class has access to the members of its enclosing class.
* An anonymous class cannot access local variables in its enclosing scope that are not declared as final or effectively final.
* Like a nested class, a declaration of a variable in an anonymous class shadows any other declarations in the enclosing scope that have the same name. 
