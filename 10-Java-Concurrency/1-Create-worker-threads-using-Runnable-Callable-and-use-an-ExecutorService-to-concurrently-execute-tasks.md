#Create worker threads using Runnable, Callable and use an ExecutorService to concurrently execute tasks

###Runnable
We can create a thread by passing an implementation of [Runnable](http://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html) to a Thread constructor. There are three ways to do it:
````java
class Task implements Runnable {
  @Override
  public void run() {
      System.out.println("Running");
  }
}

public class Test {
  public static void main(String args[]) {
    Runnable r = new Task();
    Thread thread = new Thread(r);
    thread.start();
  }
}

````
Or with an anonymous class:
````java
public class Test {
  public static void main(String args[]) {
    Runnable r = new Runnable() {
      @Override
      public void run() {
          System.out.println("Running");
      }
    };
    Thread thread = new Thread(r);
    thread.start();
  }
}
````
Or with a lambda expression:
````java
public class Test {
  public static void main(String args[]) {
    Runnable r = () -> System.out.println("Running");
    Thread thread = new Thread(r);
    thread.start();
  }
}
````

###Callable
The [Callable](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html) interface is similar to Runnable, they're both designed to be executed by another thread, a Runnable however, does not return a result and cannot throw a checked exception. We can create a Callable in three ways:
````java
class Task implements Callable<Integer> {
  @Override
  public Integer call() {
      int n = 0;
      for(int i = 0; i < 100; i++) { n += i; }
      return n;
  }
}

public class Test {
  public static void main(String args[]) {
    ExecutorService executor = Executors.newSingleThreadExecutor();
    Callable c = new Task();
    Future<Long> future = executor.submit(c);
    try {
        Long result = future.get(); //waits for the thread to complete
        System.out.println(result);
    } catch (ExecutionException e) {
        e.printStackTrace();
    }
    executor.shutdown();
  }
}

````
Or with an anonymous class:
````java
public class Test {
  public static void main(String args[]) {
    ExecutorService executor = Executors.newSingleThreadExecutor();
    Callable c = new Callable<Integer>() {
      public Integer call() {
          int n = 0;
          for(int i = 0; i < 100; i++) { n += i; }
          return n;
      }
    };
    Future<Long> future = executor.submit(c);
    try {
        Long result = future.get(); //waits for the thread to complete
        System.out.println(result);
    } catch (ExecutionException e) {
        e.printStackTrace();
    }
    executor.shutdown();
  }
}
````
Or with a lambda expression:
````java
public class Test {
  public static void main(String args[]) {
    ExecutorService executor = Executors.newSingleThreadExecutor();
    Callable c = () -> {
          int n = 0;
          for(int i = 0; i < 100; i++) { n += i; }
          return n;
      };
    Future<Long> future = executor.submit(c);
    try {
        Long result = future.get(); //waits for the thread to complete
        System.out.println(result);
    } catch (ExecutionException e) {
        e.printStackTrace();
    }
    executor.shutdown();
  }
}
````

###ExecutorService
The [ExecutorService](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html) interface represents a mechanism that executes tasks in the background. 

You can use the [Executors](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html) factory class to create ExecutorService implementations. Some examples are:
````java
// Creates an Executor that uses a single worker thread operating off an unbounded queue.
ExecutorService es1 = Executors.newSingleThreadExecutor();
// Creates a thread pool that reuses a fixed number of threads operating off a shared unbounded queue.
ExecutorService es2 = Executors.newFixedThreadPool(10);
// Creates a thread pool that can schedule commands to run after a given delay, or to execute periodically.
ExecutorService es3 = Executors.newScheduledThreadPool(10);
````
There are a few methods to execute task with an ExecutorService:
####execute(Runnable)
The execute method takes a Runnable, and executes it asynchronously:
````java
executorService.execute(new Runnable() {
    public void run() {
        System.out.println("A task");
    }
});
executorService.shutdown();
````

####submit(Runnable)
This method takes a Runnable, but returns a Future object. This object returns null when the Runnable has finished executing:
````java
Future future = executorService.submit(new Runnable() {
    public void run() {
        System.out.println("A task");
    }
});
future.get(); //Blocks until the Runnable has finished
executorService.shutdown();
````

####submit(Callable)
This version of the method takes a Callable, and returns a Future object with a result when it has finished executing:
````java
Future future = executorService.submit(new Callable<String>() {
    public String call() {
        return "A callable";
    }
});
System.out.println(future.get()); //Blocks until the Callable has finished
executorService.shutdown();
````

####invokeAny(Collection<? extends Callable<T>>)
This method executes the given tasks returning the result of one that has completed successfully. You have no guarantee about which of the Callable's results you'll get, just one of the ones that finish. When one of the tasks complete or throws an exception, the rest are cancelled. For example:
````java
List<Callable<String>> callables = new ArrayList<Callable<String>>();
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 1";
    }
});
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 2";
    }
});
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 3";
    }
});
String result = executorService.invokeAny(callables);
System.out.println(result);
executorService.shutdown();
````
Sometimes it will print "Callable 1", sometimes "Callable 2", and other times "Callable 3".

####invokeAll(Collection<? extends Callable<T>>)
This method executes the given tasks, returning a list of Futures holding their status and results when all complete. `Future.isDone()` is true for each element of the returned list. A completed task could have terminated either normally or by throwing an exception:
````java
List<Callable<String>> callables = new ArrayList<Callable<String>>();
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 1";
    }
});
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 2";
    }
});
callables.add(new Callable<String>() {
    public String call() {
        return "Callable 3";
    }
});
List<Future<String>> futures = executorService.invokeAll(callables);
for(Future<String> f : futures){
    System.out.println(f.get());
}
executorService.shutdown();
````

When you are done using the ExecutorService you should shut it down, so the threads do not keep running. To terminate the threads inside the ExecutorService you call its `shutdown()` method. The ExecutorService will not shut down immediately, but it will no longer accept new tasks, and once all threads have finished current tasks, the ExecutorService shuts down. If you want to shut down the ExecutorService immediately, you can call the `shutdownNow()` method. This will attempt to stop all executing tasks right away, and skips all non-processed tasks.
