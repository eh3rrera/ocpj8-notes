#Create worker threads using Runnable, Callable and use an ExecutorService to concurrently execute tasks

###Runnable
We can create a thread by passing an implementation of Runnable to a Thread constructor. There are three ways to do it:
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
The Callable interface is similar to Runnable, they're both designed to be executed by another thread, a Runnable however, does not return a result and cannot throw a checked exception. We can create a Callable in three ways:
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
    ExecutorService executor = Executors.newFixedThreadPool(10);
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
    ExecutorService executor = Executors.newFixedThreadPool(10);
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
    ExecutorService executor = Executors.newFixedThreadPool(10);
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
