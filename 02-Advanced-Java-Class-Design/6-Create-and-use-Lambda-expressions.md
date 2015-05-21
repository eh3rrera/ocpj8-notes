#Create and use Lambda expressions
Think about an interface with one method, like the one used to create threads:
````java
public interface Runnable() {
  public void run();
}
````
You can use an anonymous class to implement that interface:
````java
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("run");
    }
}).start();
````
Lambda expressions can be used in cases like this, where you have what is called a functional interface, an interface with just one method declared in it.

A lambda expression has the following syntax:
````
parameter -> expression body
````
* The type declaration is optional.  Compiler can inference the same from value of the parameter.
* Parenthesis around the parameter are optional. The parenthesis are required only for multiple parameters.
* Curly braces in the expression body are optional. - The braces are required only if the expression body contains more than one statement.
* A return keyword in the expression body is optional. The compiler automatically returns a value if the expression body has a single expression to return the value. 

Here are some examples of Lambda expressions.
````java
(int a, int b) -> {  return a * b; }
() -> System.out.println("Hi");
String s -> { System.out.println(s); }
(a) -> a
() -> return 100;
````

Using a lambda expression, a thread can be started in this way:
````java
new Thread(
    () -> System.out.println("run");
).start();
````
In this case, the lambda expression replaces the method `run()`. Since this method has no parameters, the parentheses have no content in between. That is to signal that the lambda takes no parameters. Also, with lambda expressions, the type can be inferred from the surrounding code, so there is no need to reference the *Runnable* interface.

Lambda expressions are objects. You can assign a lambda expression to a variable and pass it around like this:
````java
Runnable r = () -> System.out.println("run");
new Thread(r).start();
````

So lambda expressions only work with one-method interfaces (called functional interfaces). There's even an annotation to make the compiler check if an interface has more than one method:
````java
@FunctionalInterface
public interface FuncInterface { //Generates a compile-time error
    public void doSomething();
    public void doMoreSomething();
}
````

Here's another example of the use of a lambda expression:
````java
@FunctionalInterface
interface MathFunction {
    public void operation(int a, int b);
}

public class Test {
   public static void main(String args[]) {
      MathFunction multiply = (a, b) -> a * b;
      MathFunction divide = (a, b) -> a / b;

      System.out.println("4 * 2 = " + multiply.operation(4, 2));	   
      System.out.println("4 / 2 = " + divide.operation(4, 2));  
   }
}
````
In summary, lambda expressions are basically used to define an implementation of a functional interface instead of using an anonymous class.
