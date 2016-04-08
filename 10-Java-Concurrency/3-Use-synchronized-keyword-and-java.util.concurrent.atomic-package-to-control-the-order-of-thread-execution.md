#Use synchronized keyword and java.util.concurrent.atomic package to control the order of thread execution
###synchronized
You have to be careful when multiple threads access shared variables, since it can result in a race condition. For example, in a method like this:
````java
int n = 0;

void m() {
    this.n = this.n + 1;
}
````
The increment of variable n is vulnerable to concurrency. We can use the synchronized keyword to fix this. We can, for example, synchronize the method:
````java
int n = 0;

synchronized void m() {
    this.n = this.n + 1;
}
````
Or just a block of code:
````java
int n = 0;

void m() {
  synchronized (this) {
    this.n = this.n + 1;
  }
}
````
Internally, Java uses a so monitor or lock to manage synchronization. This monitor is bound to an object. For synchronized instance methods, the lock is on the instance of the corresponding object. For static methods, it's the class. For synchronized blocks, the object can be specified (the example use this to refer to the instance the method belongs to). Only the thread that acquires the lock has access to the method (or block).

###java.util.concurrent.atomic
[java.concurrent.atomic](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html) contains classes to perform atomic operations. With an atomic operation, you can safely perform the operation in parallel on multiple threads without using the synchronized keyword or locks.

We have for example:
* AtomicBoolean, AtomicInteger, AtomicLong, and AtomicReference<V> to update a value of the corresponding type (or object reference) atomically.
* AtomicIntegerArray, AtomicLongArray, and AtomicReferenceArray<E> to update the elements of the corresponding array type (or object reference) atomically.
* DoubleAdder and LongAdder, where one or more variables together maintain an initially zero sum of the corresponding type.
* DoubleAccumulator and LongAccumulator, where one or more variables together maintain a running value of the corresponding type updated using a supplied binary operator.

The synchronized example above can be changed to use an AtomicInteger in this way:
````java
AtomicInteger n = new AtomicInteger(); // creates an AtomicInteger with the initial value 0.

void m() {
    n.incrementAndGet();
}
````
Here are some common operations for the atomic classes:
````java
AtomicInteger ai = new AtomicInteger(10);
int val = ai.get(); // Get the value
ai.set(15); // Set the value

int expectedValue = 15;
int newValue      = 20;
// If the value of ai equals expectedValue, ai is set to newValue
ai.compareAndSet(expectedValue, newValue);

ai = new AtomicInteger(10);
val = ai.getAndAdd(10); // val contains 10 but ai contains 20
val = ai.addAndGet(10); // val and ai contain 30

val = ai.getAndDecrement(); // val contains 30 but ai contains 29
val = ai.decrementAndGet(); // val and ai contain 28

val = ai.getAndIncrement(); // val contains 28 but ai contains 29
val = ai.incrementAndGet(); // val and ai contain 30
````
The methods `updateAndGet()` and `getAndUpdate()` accept a lambda expression in order to perform a function (an IntUnaryOperator in the case of AtomicInteger) upon the value, for example:
````java
AtomicInteger ai = new AtomicInteger(10);
ai.updateAndGet(i -> i * 5); // ai contains 50
````
The methods `accumulateAndGet()` and `getAndAccumulate()` accept a lambda expression of type IntBinaryOperator (in the case of AtomicInteger) that updates the current value with the results of applying the given function to the current and given values. The function is applied with the current value as its first argument, and the given value as the second argument. For example:
````java
AtomicInteger ai = new AtomicInteger(10);
atomicInt.accumulateAndGet(5, (a, b) -> a + b) // ai contains 15
````
In the case of LongAdder and DoubleAdder, they can be used to consecutively add values to a number. For example:
````java
ExecutorService executor = Executors.newFixedThreadPool(3);
LongAdder la = new LongAdder();
IntStream.range(0, 1000)
    .forEach(i -> executor.submit(la::increment)); //Adds one to la, 1000 times
System.out.println(la.sum());   // la contains 1000
````
This class provides the methods `add(long)` (adds the given value) and `increment()` (add one) and is thread-safe. But instead of just summing up a single result, this class maintains a set of variables internally to reduce contention over threads. The result can be retrieved by calling `sum()` or `sumThenReset()` (gets the value and reset the sum to zero). This class is prefered over the atomic classes when updates from multiple threads are more common than reads. 

LongAccumulator and DoubleAccumulator are a more generalized version of the previous classes. Here's an example:
````java
LongAccumulator acc = new LongAccumulator((a, b) -> a + b , 1L);
ExecutorService executor = Executors.newFixedThreadPool(2);
IntStream.range(0, 5)
    .forEach(i -> executor.submit(() -> acc.accumulate(i)));
System.out.println(acc.getThenReset()); //acc contains 15
````
In the example, a LongAccumulator is created with the function `a + b` and an initial value of one. With every call to accumulate(i), both the current result and the value i are passed as parameters to the lambda expression. A LongAccumulator also maintains a set of variables internally to reduce contention over threads. The result can be retrieved by calling `get()` or `getThenReset()` (gets the value and reset the variables to zero).
