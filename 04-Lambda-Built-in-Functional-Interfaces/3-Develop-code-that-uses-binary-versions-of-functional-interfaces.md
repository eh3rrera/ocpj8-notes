#Develop code that uses binary versions of functional interfaces

The following functional interfaces:
* Predicate&lt;T&gt;
* Consumer&lt;T&gt;
* Function&lt;T,R&gt;
* UnaryOperator&lt;T&gt;

Represent an operation that takes one argument. But there are versions of these interfaces that take two arguments called. These are the binary versions. They have the same semantics, the only difference is the number of arguments. Note there is no binary version of *Supplier*. This is due to the fact that a *Supplier* takes no arguments.

Here's a summary of the binary versions of the functional interfaces along with their primitive versions and a link to their javadoc:

**BiPredicate&lt;L, R&gt;**  
(No primitive versions)

**BiConsumer&lt;T, U&gt;**  
[ObjIntConsumer&lt;T&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ObjIntConsumer.html). Operation that accepts an Object-valued and an int-valued argument and returns no result.  
[ObjLongConsumer&lt;T&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ObjLongConsumer.html). Operation that accepts an Object-valued and a long-valued argument and returns no result.  
[ObjDoubleConsumer&lt;T&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ObjDoubleConsumer.html). Operation that accepts an Object-valued and a double-valued argument and returns no result.

**BiFunction&lt;T, U, R&gt;**  
[ToIntBiFunction&lt;T, U&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToIntBiFunction.html). Function that accepts two arguments and produces an int-valued result.  
[ToLongBiFunction&lt;T, U&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToLongBiFunction.html). Function that accepts two arguments and produces a long-valued result.  
[ToDoubleBiFunction&lt;T, U&gt;](https://docs.oracle.com/javase/8/docs/api/java/util/function/ToDoubleBiFunction.html). Function that accepts two arguments and produces a double-valued result.

**BinaryOperator&lt;T&gt;**
[IntBinaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/IntBinaryOperator.html). Function operation upon two int-valued operands and producing an int-valued result.
[LongBinaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/LongBinaryOperator.html). Function operation upon two long-valued operands and producing a long-valued result.
[DoubleBinaryOperator](https://docs.oracle.com/javase/8/docs/api/java/util/function/DoubleBinaryOperator.html). Function operation upon two double-valued operands and producing a double-valued result.
