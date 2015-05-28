#Use java.util.concurrent collections and classes including CyclicBarrier and CopyOnWriteArrayList
###BlockingQueue
The [BlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) interface represents a thread-safe queue. Generally, a thread produce objects, while another thread consume them.

A BlockingQueue has four forms of methods:

| | Throws Exception |	Special Value |	Blocks |	Times Out |
|----|--------|-----------|----------|-------|
|Insert |` add(o)` | `offer(o)` | `put(o)` | o`ffer(o, timeout, timeunit)`|
|Remove | `remove(o)` | `poll()` | `take()` | `poll(timeout, timeunit)`|
|Examine | `element()`| `peek()` |  |  |

**Throws Exception**: If the attempted operation is not possible immediately, an exception is thrown.  
**Special Value**: If the attempted operation is not possible immediately, a special value is returned (often true / false).  
**Blocks**: If the attempted operation is not possible immedidately, the method call blocks until it is.  
**Times Out**: If the attempted operation is not possible immedidately, the method call blocks until it is, but waits no longer than the given timeout.

It is not possible to insert null into a BlockingQueue. If you try to insert null, the BlockingQueue will throw a NullPointerException.

The implementations of the BlockingQueue are:
* [ArrayBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ArrayBlockingQueue.html). A bounded blocking queue backed by an array. This queue orders elements FIFO (first-in-first-out). The head of the queue is that element that has been on the queue the longest time. The tail of the queue is that element that has been on the queue the shortest time. New elements are inserted at the tail of the queue, and the queue retrieval operations obtain elements at the head of the queue.  
* [DelayQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/DelayQueue.html). An unbounded blocking queue of Delayed elements, in which an element can only be taken when its delay has expired. 
* [LinkedBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingQueue.html). An optionally-bounded blocking queue based on linked nodes. This queue orders elements FIFO (first-in-first-out).  
* [LinkedTransferQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedTransferQueue.html). An unbounded TransferQueue based on linked nodes. This queue orders elements FIFO (first-in-first-out) with respect to any given producer.  
* [PriorityBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/PriorityBlockingQueue.html). An unbounded blocking queue that uses the same ordering rules as class [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) and supplies blocking retrieval operations.  
* [SynchronousQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/SynchronousQueue.html). A blocking queue in which each insert operation must wait for a corresponding remove operation by another thread, and vice versa. A synchronous queue does not have any internal capacity, not even a capacity of one. You cannot peek at a synchronous queue because an element is only present when you try to remove it; you cannot insert an element (using any method) unless another thread is trying to remove it; you cannot iterate as there is nothing to iterate.

Here's an example using ArrayBlockingQueue:
````java
class Producer implements Runnable {
    private BlockingQueue<String> queue = null;
    public Producer(BlockingQueue<String> queue) {
        this.queue = queue;
    }
    public void run() {
        try {
            // The sleeps calls will cause the Consumer to block while waiting for objects in the queue.
            queue.put("1");
            Thread.sleep(1000);
            queue.put("2");
            Thread.sleep(1000);
            queue.put("3");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

class Consumer implements Runnable {
    private BlockingQueue<String> queue = null;
    public Consumer(BlockingQueue<String> queue) {
        this.queue = queue;
    }
    public void run() {
        try {
            System.out.println(queue.take());
            System.out.println(queue.take());
            System.out.println(queue.take());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class Test {
    public static void main(String[] args) throws Exception {
        BlockingQueue<String> queue = new ArrayBlockingQueue<>(1024);
        Producer producer = new Producer(queue);
        Consumer consumer = new Consumer(queue);

        new Thread(producer).start();
        new Thread(consumer).start();
        Thread.sleep(4000);
    }
}
````

###Blocking Deque



###ConcurrentMap
The [ConcurrentMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) interface represents a Map that can handle concurrent access.

The implementations of the ConcurrentMap are:
* (ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html). A hash table supporting full concurrency of retrievals and high expected concurrency for updates. 

Since it extends form Map, it has the same methods as a normal map and some others for concurrent access:
````java
ConcurrentMap<String, String> concurrentMap = new ConcurrentHashMap<>();
concurrentMap.put("key", "value");
Object value = concurrentMap.get("key");

// Puts a new value into the map only if no value exists for the given key
String val = map.putIfAbsent("key2", "value2");

// Returns the value for the given key. If doesn't exist, the passed default value is returned
value = map.getOrDefault("hi", "or not");
````
However, Java 8 adds new methods that support functional programming.

The method `forEach()` accepts a BiConsumer lambda expression with both the key and value of the map passed as parameters. It replaces for-each loops:
````java
concurrentMap.forEach((key, value) -> System.out.println(key + "=" + value));
````

The method `replaceAll()` accepts a BiFunction lambda expression. The function is called with the key and the value of each map entry returning a new value to be assigned for the current key:
````java
concurrentMap.replaceAll((key, value) -> value.toUpperCase());
````

To transform a single entry, use `compute()`. The method accepts both the key to be computed and a bi-function. There are two variations, `computeIfAbsent()` and `computeIfPresent()`, that work only if the key is absent or present respectively:
````java
concurrentMap.compute("key", (key, value) -> value.toUpperCase());
````
The method `merge()` can be used to unify a new value with an existing value in the map. It accepts a key, the new value to be merged into the existing entry and a bi-function to specify the merging behavior of both values:
````java
concurrentMap.merge("key", "newVal", (oldVal, newVal) -> oldVal + " merged with " + newVal);
System.out.println(concurrentMap.get("key")); // It prints "value merged with newVal"
````


###ConcurrentNavigableMap
* [ConcurrentSkipListMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html)
