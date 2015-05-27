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
* [LinkedBlockingDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingDeque.html). An optionally-bounded blocking deque based on linked nodes.  
* [LinkedBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingQueue.html). An optionally-bounded blocking queue based on linked nodes. This queue orders elements FIFO (first-in-first-out).  
* [LinkedTransferQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedTransferQueue.html). An unbounded TransferQueue based on linked nodes. This queue orders elements FIFO (first-in-first-out) with respect to any given producer.  
* [PriorityBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/PriorityBlockingQueue.html). An unbounded blocking queue that uses the same ordering rules as class [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) and supplies blocking retrieval operations.  
* [SynchronousQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/SynchronousQueue.html). A blocking queue in which each insert operation must wait for a corresponding remove operation by another thread, and vice versa. A synchronous queue does not have any internal capacity, not even a capacity of one. You cannot peek at a synchronous queue because an element is only present when you try to remove it; you cannot insert an element (using any method) unless another thread is trying to remove it; you cannot iterate as there is nothing to iterate.

Here's an example using ArrayBlockingQueue:
````java
class Producer implements Runnable {
    private BlockingQueue queue = null;
    public Producer(BlockingQueue queue) {
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
    private BlockingQueue queue = null;
    public Consumer(BlockingQueue queue) {
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
        BlockingQueue queue = new ArrayBlockingQueue(1024);
        Producer producer = new Producer(queue);
        Consumer consumer = new Consumer(queue);

        new Thread(producer).start();
        new Thread(consumer).start();
        Thread.sleep(4000);
    }
}
````
###ConcurrentMap
