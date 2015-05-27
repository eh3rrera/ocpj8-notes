#Identify potential threading problems among deadlock, starvation, livelock, and race conditions

###Deadlock
Deadlock describes a situation where two or more threads are blocked forever, waiting for each other. Example:
````java
public class TestThread {
   public static Object lock1 = new Object();
   public static Object lock2 = new Object();
   
   public static void main(String args[]) {
   
      Thread t1 = new Thread(new Task1());
      Thread t2 = new Thread(new Task2);
      t1.start();
      t2.start();
   }
   
   private static class Task1 implements Runnable {
      public void run() {
         synchronized (lock1) {
            System.out.println("Task 1: Holding lock 1...");
            try {
              Thread.sleep(10);
            }
            catch (InterruptedException e) {}
            System.out.println("Task 1: Waiting for lock 2...");
            synchronized (lock2) {
               System.out.println("Task 1: Holding lock 1 & 2...");
            }
         }
      }
   }
   
   private static class Task2 implements Runnable {
      public void run() {
         synchronized (lock2) {
            System.out.println("Task 2: Holding lock 2...");
            try {
              Thread.sleep(10);
            }
            catch (InterruptedException e) {}
            System.out.println("Task 2: Waiting for lock 1...");
            synchronized (lock1) {
               System.out.println("Task 2: Holding lock 1 & 2...");
            }
         }
      }
   } 
}
````

###Starvation
Lock starvation occurs when a thread, having lesser priority than other ones, is constantly waiting for a lock, never able to take it because other thread(s) with higher priority are constanly acquiring the lock.

###Livelock
A LiveLock is like a deadlock in the sense that two (or more) threads are blocking each others. But with the livelock, each thread is waiting "actively", trying to resolve the problem on its own. A live lock occurs when the combination of these processes's efforts to resolve the problem makes it impossible for them to ever terminate. For example, if two threads detect a deadlock, and try to "step aside" for each other, without care they will end up being stuck in a loop always "stepping aside" and never managing to move forwards.

###Race conditions
A race condition is the situation where two threads compete for the same resource and they try to change it at the same time, doing it in a way that causes unexpected results.. The problem happens when for example, one thread checks if the value is X, then do something that depends on that value and another thread does something to the value in between the check and the do.
