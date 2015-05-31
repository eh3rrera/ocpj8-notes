#Create inner classes including static inner class, local class, nested class, and anonymous inner class
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
* Nested static classes don't need a reference of their outer class (the enclosing class)
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
* Nested  classes need a reference of their outer class
* Static and non-static members of the outer class are accessible in a nested  class
* If the nested class is used inside the class that defines it, the keyword this can be used to create an instance of the nested class (for example `OuterClass.NestedClass nc = this.new NestedClass();`)

There's also a concept named shadowing. If a declaration of a type (such as a member variable or a parameter name) in a particular scope (such as an inner class or a method definition) has the same name as another declaration in the enclosing scope, then the declaration shadows the declaration of the enclosing scope, for example:
````java
public class Test {
    public int x = 10;

    class Inner {
        public int x = 1;
        void m(int x) {
            System.out.println("x = " + x);
            System.out.println("this.x = " + this.x);
            System.out.println("Test.this.x = " + Test.this.x);
        }
    }

    public static void main(String... args) {
        Test t = new Test();
        Test.Inner i = t.new Ineer();
        i.m(5);
    }
}
````
This example defines three variables named x, the member variable of the class Test, the member variable of the inner class Inner, and the parameter in the method m. The variable x defined as a parameter of the method shadows the variable of the inner class. So, when you use the variable x in the method m, it refers to the method parameter. To refer to the member variable of the inner class Inner, use the keyword this to represent the enclosing scope. To refer to member variables that enclose larger scopes, use the class name to which they belong. The output of the example is:
````
x = 5
this.x = 1
Test.this.x = 10
````

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
