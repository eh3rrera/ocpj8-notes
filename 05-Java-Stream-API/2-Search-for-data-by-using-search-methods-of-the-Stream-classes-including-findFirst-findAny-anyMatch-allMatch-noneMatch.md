#Search for data by using search methods of the Stream classes including findFirst, findAny, anyMatch, allMatch, noneMatch
We hava two types of methods in the Stream API to search for data:
* findXXX methods. Take no arguments and return an Optional object with the result, or an empty Optional if nothing is found.
* XXXMatch methods. Take a Predicate and return a boolean if an element in the stream returns true by applying the Predicate.

The methods are:

`Optional<T>	findAny()`
This is a short-circuiting terminal operation that returns an Optional representing some element of the stream. This doesn't guarantee to return the first element of a sorted stream.

`Optional<T>	findAny()`
This is a short-circuiting terminal operation that returns the first element of the stream. If the stream has no order, then any element may be returned.

`boolean anyMatch(Predicate<? super T> predicate)`
This is a short-circuiting terminal operation that returns whether any elements of this stream match the provided predicate.  If the stream is empty then false is returned and the predicate is not evaluated.

`boolean allMatch(Predicate<? super T> predicate)`
This is a short-circuiting terminal operation that returns whether all elements of this stream match the provided predicate.  If the stream is empty then true is returned and the predicate is not evaluated.

`boolean noneMatch(Predicate<? super T> predicate)`
This is a short-circuiting terminal operation that returns whether no elements of this stream match the provided predicate.  If the stream is empty then true is returned and the predicate is not evaluated.

A short-circuiting terminal operation basically means that there's no need to process the entire stream to return a result. As soon as an element that fits the predicate is found or that a result can be inferred, the result is return.

Here's an example:
````java
Optional<Integer> first = Stream.of(1, 10, 5, 3, 13, 20).filter(i -> i % 2 == 0).findFirst(); //returns 2
Optional<Integer> any = Stream.of(1, 10, 5, 3, 13, 20).filter(i -> i % 2 == 0).findFirst(); //can return 2
boolean any2 = Stream.of(1, 10, 5, 3, 13, 20).anyMatch(i -> i % 3 == 0); //returns true
boolean all = Stream.of(1, 10, 5, 3, 13, 20).allMatch(i -> i % 2 == 0); //returns false
boolean none = Stream.of(1, 10, 5, 3, 13, 20).noneMatch(i -> i % 6 == 0); //returns true
````
