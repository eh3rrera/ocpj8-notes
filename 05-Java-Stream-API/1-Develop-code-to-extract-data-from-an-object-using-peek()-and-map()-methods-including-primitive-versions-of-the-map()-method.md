#Develop code to extract data from an object using peek() and map() methods including primitive versions of the map() method
###peek()
````java
Stream<T> peek(Consumer<? super T> action)
````
Peek is an intermediate operation that returns a stream consisting of the elements of the original stream, and performing the provided action on each element.

According to the [API](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#peek-java.util.function.Consumer-), This method exists mainly to support debugging, where you want to see the elements as they flow past a certain point in a pipeline:
````java
Stream.of("the", "good", "bad", "ugly")
   .filter(e -> e.length() > 3)
   .peek(e -> System.out.println("Filtered value: " + e))
   .map(String::toUpperCase)
   .peek(e -> System.out.println("Mapped value: " + e))
   .collect(Collectors.toList());
````

###map()
````java
<R> Stream<R> map(Function<? super T,? extends R> mapper)
````
Map is an intermediate operation that returns a stream consisting of the results of applying the given function to the elements of this stream. Since we're talking about a *Function*, it's possible to convert the items in the stream to other objects. In other words, for each item you create a new object based on that item.

For example, to convert all strings in the stream to uppercase:
````java
Stream.of("a", "b", "c", "d").map(s -> s.toUpperCase()).forEach(s -> System.out.print(s));
````

Just like a *Function*, map() include primitive versions:
````java
IntStream mapToInt(ToIntFunction<? super T> mapper)
LongStream mapToLong(ToLongFunction<? super T> mapper)
DoubleStream mapToDouble(ToDoubleFunction<? super T> mapper)
````
These methods can be used when you want a stream of these primitive types. For example, consider a stream of elements of this type:
````java
class Employee {
  private int id;
  private String name;
  public int getId() {
    return id;
  }
  public String getName() {
    return name;
  }
  public void setId(int id) {
    this.id = id;
  }
  public void setName(String name) {
    this.name = name;
  }
}
````
We can extract the employee ids directly to a stream of `int` in this way:
````java
List<Integer> employeeIds = employees.stream().mapToInt(e -> e.getId()).collect(Collectors.toList());
````
This works because `getInt()` returns an `int`, the type expected by `mapToInt()`.
