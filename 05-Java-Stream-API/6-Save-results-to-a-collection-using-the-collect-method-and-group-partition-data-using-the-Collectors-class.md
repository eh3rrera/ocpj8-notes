#Save results to a collection using the collect method and group/partition data using the Collectors class
Streams have the following method:
````java
collect(Collector<? super T,A,R> collector)
````
This method performs a mutable reduction operation on the elements of this stream using a {Collector}(https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collector.html).

A mutable reduction operation accumulates (or collects) input elements into a mutable result container, such as a Collection or StringBuilder, as it processes the elements in the stream.

A collect operation requires three functions: 
* A supplier function to construct new instances of the result container
* An accumulator function to incorporate an input element into a result container
* A combining function to merge the contents of one result container into another.

In fact, streams also have the following method that takes the above functions to create our own collect operations:
````java
collect(Supplier<R> supplier, BiConsumer<R,? super T> accumulator, BiConsumer<R,R> combiner)
````
For example, traditionally, to collect the elements of a list into another list, we could do:
````java
List<String> word = new ArrayList<>();;
List<String> letters = new ArrayList<>();
letters.add("H");
letters.add("e");
letters.add("l");
letters.add("l");
letters.add("o");
for (String s : letters) {
   word.add(s.toUpperCase());
}
````
Now with the collect method:
````java
List<String> letters = new ArrayList<>();
letters.add("H");
letters.add("e");
letters.add("l");
letters.add("l");
letters.add("o");
List<String> word = letters.stream().collect(() -> new ArrayList<>(),
                                    (c, s) -> c.add(s.toUpperCase()),
                                    (c1, c2) -> c1.addAll(c2));
````

However, there's a class, [Collectors](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html), which implements many useful reduction operations. So using Collectors, the code becomes simpler:
````java
List<String> letters = new ArrayList<>();
letters.add("H");
letters.add("e");
letters.add("l");
letters.add("l");
letters.add("o");
List<String> word = letters.stream().map(s -> s.toUpperCase()).collect(Collectors.toList());
````

Other implementations of Collectors are:
````java
// Accumulate into a TreeSet
Set<String> set = letters.stream()
                          .map(s -> s.toUpperCase())
                          .collect(Collectors.toCollection(TreeSet::new));

// Convert elements to strings and concatenate them, separated by commas
String joined = letters.stream()
                      .map(s -> s.toUpperCase())
                      .collect(Collectors.joining(", "));

// Compute sum of all letters
int total = letters.stream()
                      .collect(Collectors.summingInt(s.length())));

// Group by starting letter
Map<String, List<String>> grouped = letters.stream()
                                    .collect(Collectors.groupingBy(s.substring(0,1)));

// Partition letters into uppercase and lowercase
Map<Boolean, List<String>> upperLower = letters.stream()
                                    .collect(Collectors.partitioningBy(s -> Character.isUpperCase(s.codePointAt(0))));

````
The last method, partitionBy, takes a predicate that returns `Map<Boolean, List <String>>` where the key is a boolean and the results are based on the behavior of the predicate. So its output is:
````
{false=["e","l","l","o"], true=[H]}
````
