#Develop code that uses the Optional class

The [java.util.Optional<T>](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) class acts as a container which may or may not contain a non-null value. 

The main methods of the class are:
* `isPresent()` that returns true if it contains a non-null value, false otherwise.
* `get()` that returns the non-null value if it contains a non-null value, and throws a NoSuchElementException otherwise. To avoid the exception, before getting the value you must check if the Optional object contains a non-null value.
* `ifPresent(Consumer<? super T> action)` takes a Consumer to perform some operation on the value contained in the Optional. If the Optional is empty or null, it does not perform anything.

OptionalInt, OptionalLong, and OptionalDouble deal with optional primitive values.
* `getAsInt()` method from OptionalInt class returns int value.
* `getAsLong()` method from OptionalLong class return long value.
* `getAsDouble()` method from OptionalDouble class return double value.

Some stream operations (like `map()`, `max()`, `min()`, etc.)  return optional values with nothing inside if the stream is empty. For example:
````java
OptionalInt min = Stream.of(10, 20, 30, 40).filter(n -> n > 50).min();
if (min.isPresent()) {
  System.out.println(min.getAsInt());
} else {
  System.out.println("No value");
}
````
Or if we don't need to print the "No value" message:
````java
OptionalInt min = Stream.of(10, 20, 30, 40).filter(n -> n > 50).min();
min.isPresent(n -> System.out.println(n));
````

Besides `get()`, we have three other methods to obtain values from an Optional:
* `T orElse(T defaultValue)` Returns the value contained in the Optional. If empty, it returns the specified defaultValue.
* `T orElseGet(Supplier<? extends T> defaultSupplier)` Returns the value contained in the Optional. If empty, it returns the value returned from the specified defaultSupplier.
* `<X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier) throws X extends Throwable` Returns the value contained in the Optional. If empty, it throws the exception returned from the specified exceptionSupplier.
For example:
````java
Stream.of(10, 20, 30, 40).filter(n -> n > 50).min().orElse(0);
Stream.of(10, 20, 30, 40).filter(n -> n > 50).min().orElseGet(() -> logAndReturnDefault());
Stream.of(10, 20, 30, 40).filter(n -> n > 50).min().orElseThrow(Exception::new);
````

If we are not using streams and we need to create an Optional, there are three methods we can use:
* `<T> Optional<T> empty()` Returns an empty Optional.
* `<T> Optional<T> of(T value)` Returns an Optional containing the specified value  If the value is null, it throws a NullPointerException.
* `<T> Optional<T> ofNullable(T value)` Returns an Optional containing the specified value if the value is non-null. If the specified value is null, it returns an empty Optional.

For example:
````java
Optional<String> empty  = Optional.empty();
Optional<String> string = Optional.of("Hello");
Optional<String> empty2  = Optional.ofNullable(null);
````

