#Sort a collection using Stream API

To sort a collection using the method `sorted()` from the Stream API, you need a Comparator (there's a version of sorted that takes no arguments that returns a stream with its elements sorted according to natural order).

Comparator is a functional interface, so you can create a comparator in the form of a lambda expression.  For example:
````java
Comparator<String> byLength = (s1, s2) -> Integer.compare( s1.length(), s2.length());

Stream.of("hello","good bye", "black", "white", "good", "bad")
          .sorted(byLength)
          .forEach(s -> System.out.println(s)); 
````
The output:
````
bad
good
hello
black
white
good bye
````

If you want to compare using multiple criteria, in Java 8 there's a new method to make this easily,  `Comparator.thenComparing()`:
````java
Comparator<String> byLength = (s1, s2) -> Integer.compare( s1.length(), s2.length());
Comparator<String> byLetters = (s1, s2) -> s1.compareTo(s2);

Stream.of("hello","good bye", "black", "white", "good", "bad")
          .sorted(byLength.thenComparing(byLetters))
          .forEach(s -> System.out.println(s)); 
````
The output:
````
bad
good
black
hello
white
good bye
````
