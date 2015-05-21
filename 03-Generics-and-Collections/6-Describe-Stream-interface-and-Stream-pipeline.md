#Describe Stream interface and Stream pipeline

A stream is a sequence of elements supporting sequential and parallel aggregate operations.  A stream is not a data structure that stores elements. Instead, it just carries values from a source through a pipeline. Here's the [javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html).

A stream pipeline is just a sequence of aggregate operations. A stream pipeline consists of:
* A stream source, like a collection
* Intermediate operations that transform the stream and produce a new stream, like `filter()` and
* A terminal operation that either produces a result or calls the `forEach()` method. 

An example of a pipeline that consists of the aggregate operations filter and count:
````java
long count = words.stream()
                  .filter(w -> w.endsWith("ly"))
                  .count();
````
