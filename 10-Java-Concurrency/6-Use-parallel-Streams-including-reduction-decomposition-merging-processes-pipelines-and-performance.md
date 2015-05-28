#Use parallel Streams including reduction, decomposition, merging processes, pipelines and performance.

You can execute streams in parallel so Java partitions the stream into multiple substreams. Aggregate operations iterate over and process these substreams in parallel and then combine the results. It's important that the operations are stateless and can be executed in an arbitrary order.

A stream is not parallel by default. To make a parallel stream, invoke the method `Collection.parallelStream` (if you're working with a collection) or `BaseStream.parallel`:
````java
List l = new ArrayList();
l.parallelStream().forEach(System.out:println);
// Or
Stream.of("1", "2", "3").parallel().forEach(System.out:println);
````
Parallel streams use a common ForkJoinPool available via the `ForkJoinPool.commonPool()` method. The size of the thread-pool depends on the amount of available physical CPU cores:
````java
ForkJoinPool commonPool = ForkJoinPool.commonPool();
System.out.println(commonPool.getParallelism()); 
````
The value can be modified by setting the following JVM parameter to a non-negative integer:
````java
-Djava.util.concurrent.ForkJoinPool.common.parallelism=4
````

###Reduction
A reduction operation combines all elements into a single result, such as finding the sum or maximum of a set of numbers, or accumulating elements into a list. So in addtion to `reduce()`, `collect()`, `sum()`, `max()`, or `count()` are also reduction operations.

The `reduce()` method has the following versions:
````java
Optional<T>	reduce(BinaryOperator<T> accumulator)
````
Performs a reduction on the elements of this stream, using an associative accumulation function, and returns an Optional describing the reduced value, if any.
````java
T	reduce(T identity, BinaryOperator<T> accumulator)
````
Performs a reduction on the elements of this stream, using the provided identity value and an associative accumulation function, and returns the reduced value.
````java
<U> U	reduce(U identity, BiFunction<U,? super T,U> accumulator, BinaryOperator<U> combiner)
````
Performs a reduction on the elements of this stream, using the provided identity, accumulation and combining functions.

A reduce operation is parallelizable as long as the function(s) used to process the elements are associative and stateless. For example:
````java
int sum = numbers.parallelStream().reduce(0, (x,y) -> x+y);
````
Can be parallelized with no modification:
````java
int sum = numbers.parallelStream().reduce(0, (x,y) -> x+y);
````
Reduction can operate on subsets of the data in parallel, and then combine the intermediate results to get the final answer.

A reduce operation on elements of type <T> yielding a result of type <U> requires three parameters:
````java
 <U> U reduce(U identity,
              BiFunction<U, ? super T, U> accumulator,
              BinaryOperator<U> combiner);
````
Here, the identity element is both an initial seed value for the reduction and a default result if there are no input elements. The accumulator function takes a partial result and the next element, and produces a new partial result. The combiner function combines two partial results to produce a new partial (or the final) result. Example:
````java
int sum = numbers.parallelStream()
                  .reduce(0, 
                    (sum, x) -> sum + x,
                    (x, y) -> x + y);
````
