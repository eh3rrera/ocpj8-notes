#Iterate using forEach methods of Streams and List

In Java 8, collections that implement *Iterable* (such as *List* and *Set*) now have a `forEach()` method. This method takes as a parameter a functional interface, therefore, the parameter can be a lambda expression:
````java
List<String> l = new ArrayList<>();

l.add("A");
l.add("B");
l.add("C");
l.add("D");

l.forEach(i -> System.out.println(i));
````
Using Stream's `forEach()` method is almost the same:
````java
List<String> l = new ArrayList<>();

l.add("A");
l.add("B");
l.add("C");
l.add("D");

l.stream().forEach(i -> System.out.println(i));
````

The advantage of using a stream is that we can perform operations on the elements of the collection before the iteration.
