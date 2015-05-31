#Use method references with Streams

When the body of a lambda expression is used to execute a method, like in this example:
````java
List<String> l = new ArrayList<>();
l.stream().forEach(s -> System.out.println(s));
````
We can substitue the lambda expression with a method reference like this:
````java
List<String> l = new ArrayList<>();
l.stream().forEach(System.out::println);
````
Notice how **::** is used to call the method and that no parameters are passed, since the compiler infers them along with their type.

There are four types of method references (assuming a class named Person with a `getName()` method and a variable named p of that type):

|Type|Example|
|----|---------|
|Reference to a static method|`Math::square`|
|Reference to a constructor	|`Integer::new`|
|Reference to an instance method of an arbitrary object of a particular type	|`Person::getName`|
|Reference to an instance method of a particular object	|`p::getName`|

Here's a comparison between a lambda expression and the equivalent method expression:

|Lambda Expression|Method Reference|
|----|---------|
|`n -> Math.square(n)`|`Math::square`|
|`i -> new Integer(i)`	|`Integer::new`|
|`p -> p.getName()`	|`Person::getName`|
|`p -> p.getName()`	|`p::getName`|
