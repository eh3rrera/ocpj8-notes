#Develop code that uses Stream data methods and calculation methods
###Data methods
````Optional<T>	max(Comparator<? super T> comparator)````
Terminal operation that returns the maximum element of this stream according to the provided Comparator wrapped in an Optional object, or an empty Optional if the stream is empty.

````Optional<T>	min(Comparator<? super T> comparator)````
Terminal operation that returns the minimum element of this stream according to the provided Comparator wrapped in an Optional object, or an empty Optional if the stream is empty.

````long	count()````
Terminal operation that returns the count of elements in this stream.

Comparator is a functional interface, so you can create a comparator in the form of a lambda expression. For example:
`````java
Comparator<String> byLength = (s1, s2) -> Integer.compare( s1.length(), s2.length());
Optional<String> max = Stream.of("hello","good bye", "black", "white", "good", "bad")
        .max(byLength); //returns "good bye"
Optional<String> min = Stream.of("hello","good bye", "black", "white", "good", "bad")
        .min(byLength); //returns "bad"
long count = Stream.of("hello","good bye", "black", "white", "good", "bad")
        .count(); //returns 6
````

###Calculation methods
Calculation methods only work with the primitive versions of Stream: IntStream, LongStream, and DoubleStream. For example, for IntStream the methods are:

`int sum()`
Terminal operation that returns the sum of elements in the stream.

`OptionalInt min()`
Terminal operation that returns an OptionalInt describing the minimum element of the stream, or an empty optional if this stream is empty.

`OptionalInt max()`
Terminal operation that returns an OptionalInt describing the minimum element of the stream, or an empty optional if this stream is empty.

`OptionalDouble average()`
Terminal operation that returns an OptionalDouble describing the arithmetic mean of elements of the stream, or an empty optional if this stream is empty.

Except for `average()` that always returns an OptionalDouble, the other methods return a long and OptionalLong for LongStream, and a dobule and OptionalDouble for DoubleStream.

Here's an example:
````java
OptionalInt max = IntStream.of(1, 34, 667, 3, 32, 23).max(); // max() returns 667

OptionalInt min = IntStream.of(1, 34, 667, 3, 32, 23).min(); // min() returns 1

OptionalDouble average = IntStream.of(1, 34, 667, 3, 32, 23).average(); // returns 126.66

int sum = IntStream.of(1, 34, 667, 3, 32, 23).sum(); // returns 760
````
