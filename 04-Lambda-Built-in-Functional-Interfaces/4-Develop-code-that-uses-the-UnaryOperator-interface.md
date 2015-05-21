#Develop code that uses the UnaryOperator interface
*UnaryOperator* is a functional interface that receives a value of a certain type and returns a value of the same type. This is a specialization of the *Function* interface for the case where the operand and result are of the same type (in fact *UnaryOperator* extends from *Function*).

Here's the [javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/function/UnaryOperator.html).

And here's an example:
````java
public class Test {
  public static void main(String[] args) {

  	UnaryOperator<Integer> unary = v -> v * 10;
	  // This means the same as the UnaryOperator above.
  	Function<Integer, Integer> function = v -> v * 10;
  
  	System.out.println(unary.apply(10));
  	System.out.println(function.apply(10));
  }
}
````
The output:
````
100
100
````

The UnaryOperator can also be applied to a collection like this:
````java
public class Program {
  public static void main(String[] args) {
  	List<Integer> list = new ArrayList<>();
  	list.add(1);
  	list.add(2);
  	list.add(3);
  	list.replaceAll(i -> i * 10);
  	// ... Display the results.
  	System.out.println(list);
  }
}
````
The output:
````
[10, 20, 30]
````
