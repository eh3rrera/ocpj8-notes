#Use  the built-in interfaces included in the java.util.function package such as Predicate, Consumer, Function, and Supplier
###Predicate
A predicate is a statement that may be true or false depending on the values of its variables. It can be thought of as a function that returns a value that is either true or false.

In java 8, a *Predicate* is a functional interface that can be used anywhere you need to evaluate a boolean condition. Since it's a functional interface, you can pass a lambda expressions wherever a *Predicate* is expected.

See the [API](https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html) to know the methods of this interface.

Here's an example. First we see how the interface with an anonymous class:
````java
Predicate<String> isALongWord = new Predicate<String>() {
    @Override
    public boolean test(String t) {
        return t.length() > 10;
    }
};
String s = "successfully"
boolean result = isALongWord.test(s);
````
And now with a lambda expression:
````java
Predicate<String> isALongWord = t -> t.length() > 10;
String s = "successfully"
boolean result = isALongWord.test(s);
````
Predicates are also used to filter collections, for example:
````java
public class Test {
  public static void main(String[] args) {
    List<String> l = new ArrayList<>();
    l.add("successfully");
    l.add("easy");
    l.add("fortune");
    List<String> filtered = l.stream().filter( s -> s.length() > 5 ).collect(Collectors.<String>toList());
    System.out.println(filtered);
  }
}
````
Here, the filter method expects a *Predicate*, so we can pass a lambda expression to simplify things, so the output of the example is:
````
["successfully", "fortune"]
````

###Consumer
This functional interface represents an operation that accepts a single input argument and returns no result. The real outcome is the side-effects it produces. Since it's a functional interface, you can pass a lambda expressions wherever a *Consumer* is expected.

See the [API](https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html) to know the methods of this interface.

Here's an example:
````java
class Product {
  private double price = 0.0;
  
  public void setPrice(double price) {
    this.price = price;
  }
  
  public void printPrice() {
    System.out.println(price);
  }
}

public class Test {
  public static void main(String[] args) {
    Consumer<Product> updatePrice = p -> p.setPrice(5.9);
    Product p = new Product();
    updatePrice.accept(p);
    p.printPrice();
  }
}
````
Basically, what *Consumer* does is executing the assigned lambda expression. The side-effect here, it's the updating of the product's price, so the output is:
````
5.9
````

###Function
This functional interface a function that accepts one argument and produces a result. One use for example, it's  to convert or transform from one object to another. Since it's a functional interface, you can pass a lambda expressions wherever a *Function* is expected.

See the [API](https://docs.oracle.com/javase/8/docs/api/java/util/function/Function.html) to know the methods of this interface.

Here's an example:
````java
public class Test {
  public static void main(String[] args) {
    int n = 5;
    modifyTheValue(n, val-> val + 10);
    modifyTheValue(n, val-> val * 100);
  }
  
  static void modifyValue(int v, Function<Integer, Integer> function){
    int result = function.apply(v);
    System.out.println(newValue);
  }
  
}
````
The input parameter type and the return type of the method can either be same or different. In this case, they are the same type and the program just execute the functions represented by the lambda expression, an addition and a multiplication, so the output is:
````
15
500
````

###Supplier
