Develop code that uses primitive versions of functional interfaces
Due to the way generics are implemented, parameters of the functional interfaces (for example, *Predicate<T>*) can be bound only to reference types (like *String*, objects, etc).

If you want to use primitive types with these functional interfaces, Java use a mechanism called autoboxing to automatically convert a primitive to its corresponding wrapper type (for example, int to *Integer*) and viceversa.

But since boxed values use more memory, this comes with a performance cost. For this reason, Java provides specialized versions of the functional interfaces in order to avoid autoboxing operations when the inputs or outputs are primitives.

For example, instead of using
````java
Predicate<Integer> p = i -> i > 10;
````
You can use
````java
IntPredicate p = i -> i > 10;
````

In general, the names of functional interfaces that have a primitive version for the input parameter are preceded by the primitive type, like *IntPredicate*.
The *Function* interface also has variants for the output parameter like *ToIntFunction<T>*.

Here's a summary of the primitive version of functional interfaces with a link to their javadoc:

**Predicate<T>**  
[IntPredicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntPredicate.html). Predicate of one int-valued argument.  
[LongPredicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongPredicate.html). Predicate of one long-valued argument.  
[DoublePredicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoublePredicate.html). Predicate of one double-valued argument.

**Consumer<T>**  
[IntConsumer](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntConsumer.html). Operation that accepts a single int-valued argument and returns no result.  
[LongConsumer](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongConsumer.html). Operation that accepts a single long-valued argument and returns no result.  
[DoubleConsumer](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoubleConsumer.html). Operation that accepts a single double-valued argument and returns no result.

**Function<T, R>**  
[IntFunction<R>](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntFunction.html). Function that accepts an int-valued argument and produces a result.  
[IntToDoubleFunction](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntToDoubleFunction.html). Function that accepts an int-valued argument and produces a double-valued result.  
[IntToLongFunction](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntToLongFunction.html). Function that accepts an int-valued argument and produces a long-valued result.  
[LongFunction<R>](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongFunction.html). Function that accepts a long-valued argument and produces a result.  
[LongToDoubleFunction](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongToDoubleFunction.html). Function that accepts a long-valued argument and produces a double-valued result.  
[LongToIntFunction](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongToIntFunction.html). Function that accepts a long-valued argument and produces an int-valued result.  
[DoubleFunction<R>](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoubleFunction.html). Function that accepts a double-valued argument and produces a result.  
[ToIntFunction<T>](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToIntFunction.html). Function that produces an int-valued result.  
[ToDoubleFunction<T>](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToDoubleFunction.html). Function that produces a double-valued result.  
[ToLongFunction<T>](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToLongFunction.html). Function that produces a long-valued result.

**Supplier<T>**  
[BooleanSupplier](https://docs.oracle.com/javase/8/docs/api/java/util/function/BooleanSupplier.html). Supplier of boolean-valued results.  
[IntSupplier](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntSupplier.html). Supplier of int-valued results.  
[LongSupplier](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongSupplier.html). Supplier of long-valued results.  
[DoubleSupplier](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoubleSupplier.html). Supplier of double-valued results.

**UnaryOperator<T>**  
[IntUnaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntUnaryOperator.html). Function operation on a single int-valued operand that produces an int-valued result.  
[LongUnaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongUnaryOperator.html). Function operation on a single long-valued operand that produces a long-valued result.  
[DoubleUnaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoubleUnaryOperator.html). Function operation on a single double-valued operand that produces a double-valued result.
