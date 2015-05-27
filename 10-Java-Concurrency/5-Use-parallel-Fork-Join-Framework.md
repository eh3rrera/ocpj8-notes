#Use parallel Fork/Join Framework

The Fork/Join Framework is designed for work that can be broken down into smaller tasks, with its results combined to produce the final result. One important concept is that ideally no worker thread is idle, idle workers steal the work from those workers who are busy, this is known as *work-stealing*.

It follows this algorithm:
````
if (problem is small)
	directly solve problem
else {
	split problem into independent parts
	fork new subtasks to solve each part
	join all subtasks
	compose result from subresults
}
````
The core classes of the Fork-Join framework are ForkJoinPool and ForkJoinTask.

####ForkJoinPool
[ForkJoinPool](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html) is an implementation of ExecutorService that employs the work-stealing algorithm. It can be created like this:
````java
ForkJoinPool pool = new ForkJoinPool(int); //creates a ForkJoinPool with the indicated parallelism level (number of initial threads in the pool)
ForkJoinPool pool = new ForkJoinPool(); //equivalent to new ForkJoinPool(Runtime.availableProcessors())
````
There are different ways of submitting a task to the ForkJoinPool:
````java
void execute(ForkJoinTask<?> task)
````
Arranges for (asynchronous) execution of the given task.
````java
void execute(Runnable task)
````
Executes the given command at some time in the future.
````java
<T> T invoke(ForkJoinTask<T> task)
````
Performs the given task, returning its result upon completion.
````java
<T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks)
````
Executes the given tasks, returning a list of Futures holding their status and results when all complete.
````java
<T> ForkJoinTask<T>	submit(Callable<T> task)
````
Submits a value-returning task for execution and returns a Future representing the pending results of the task.
````java
<T> ForkJoinTask<T>	submit(ForkJoinTask<T> task)
````
Submits a ForkJoinTask for execution.
````java
ForkJoinTask<?> submit(Runnable task)
````
Submits a Runnable task for execution and returns a Future representing that task.
````java
<T> ForkJoinTask<T>	submit(Runnable task, T result)
````
Submits a Runnable task for execution and returns a Future representing that task.

####ForkJoinTask
[ForkJoinTask](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinTask.html) is an abstract class for creating tasks that run within a ForkJoinPool. [RecursiveAction](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveAction.html) and [RecursiveTask](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/RecursiveTask.html) are its subclasses. The only difference between these two classes is that the RecursiveAction does not return a value while RecursiveTask does.

The main methods of ForkJoinTask are:
* The `fork()` method allows a ForkJoinTask to be planned for asynchronous execution. A new task can be created with this method.
* The join() method allows a ForkJoinTask to wait for the completion of another one.

In this example,  the program finds the minimum number from a large array:
````java
public class MinimumTaskFinder extends RecursiveTask<Integer> {

  private static final int SEQUENTIAL_THRESHOLD = 5;

  private final int[] data;
  private final int start;
  private final int end;

  public MinimumTaskFinder(int[] data, int start, int end) {
    this.data = data;
    this.start = start;
    this.end = end;
  }

  public MinimumTaskFinder(int[] data) {
    this(data, 0, data.length);
  }

  @Override
  protected Integer compute() {
    final int length = end - start;
    if (length < SEQUENTIAL_THRESHOLD) {
      return computeDirectly();
    }
    final int split = length / 2;
    final MinimumTaskFinder left = new MinimumTaskFinder(data, start, start + split);
    left.fork();
    final MinimumTaskFinder right = new MinimumTaskFinder(data, start + split, end);
    return Math.min(right.compute(), left.join());
  }

  private Integer computeDirectly() {
    int min = Integer.MAX_VALUE;
    for (int i = start; i < end; i++) {
      if (data[i] < min) {
        min = data[i];
      }
    }
    return min;
  }

  public static void main(String[] args) {
    int[] data = new int[10000];
    Random random = new Random();
    for (int i = 0; i < data.length; i++) {
      data[i] = random.nextInt(1000);
    }

    ForkJoinPool pool = new ForkJoinPool();
    MinimumTaskFinder task = new MinimumTaskFinder(data);
    System.out.println(pool.invoke(task));
  }
}
````
If the size of the array is less than a threshold, then find the minimum directly by iterating over the array. Otherwise, since the problem can be broken into chunks, split the array into two halves, recurse on each half and wait for them to complete (join). Once the value is reduced to the threshold, the tasks are not further divided for parallelism. Finally, once we have the result of each half, we can find the minimum of the two and return it. 
