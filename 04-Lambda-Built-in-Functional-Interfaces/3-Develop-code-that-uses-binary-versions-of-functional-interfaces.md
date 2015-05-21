#Develop code that uses binary versions of functional interfaces

The following functional interfaces:
* Predicate<T>
* Consumer<T>
* Function<T,R>
* UnaryOperator<T>

Represent an operation that takes one arguments. There are versions of these interfaces that take two arguments called the binary versions. They have the same semantics, the only difference is the number of arguments. Note there is no binary version of *Supplier*. This is due to the fact that a *Supplier* takes no arguments.

