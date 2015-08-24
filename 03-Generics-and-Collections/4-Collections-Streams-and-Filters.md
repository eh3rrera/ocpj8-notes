#Collections Streams and Filters
A stream represents a sequence of elements. It supports different kind of operations to perform computations upon those elements.

In Java 8, collections have methods that return a stream, for example, *List* and *Set* support the new methods `stream()` and  `parallelStream()` to either create a sequential or a parallel stream.

But we don't have to create collections in order to work with streams:
````java
Stream.of("a1", "a2", "a3")
    .forEach(System.out::println);
````
`Stream.of()` will create a stream from object references.

Besides regular object streams, Java 8 brings special kinds of streams for working with the primitive data types, sucha as *IntStream*, *LongStream* and *DoubleStream*.

*IntStreams* for example, can replace the regular for loop using `IntStream.range()`:
````java
IntStream.range(1, 10)
    .forEach(System.out::println);
````
Streams cannot be reused. As soon as you call any terminal operation the stream is closed. Terminal operations return either a void or non-stream result, like the `forEach()` method. To overcome this limitation, we have to create a new stream chain for every terminal operation we want to execute.

Before Java 8, we used for loops or iterators to iterate through the collections and filter them. In Java 8, stream operations have methods like foreach, map, filter, etc. which internally iterates through the elements.
For example:
````java
List<String> names = newArrayList<>();
for(Employee e : employees) {
  if(e.getName().startsWith("C")) {
    names.add(e.getName());
  }
}
````
Now, the line below is doing exactly the same thing but using stream and a filter:
````java
List<String> names = employees.stream().filter(e -> e.getName().startsWith("A")).collect(Collectors.toList());
````
