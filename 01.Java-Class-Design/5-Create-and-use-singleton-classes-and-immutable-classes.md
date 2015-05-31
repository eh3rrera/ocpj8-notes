#Create and use singleton classes and immutable classes
###Singleton
Singleton is a design pattern that provides a way for a class to create only one object from that class. 

The key for a Singleton class is to make the constructor private, have a static instance of itself and a method to access it:
````java
public class Singleton {
  //Create an object
   private static final Singleton instance = new Singleton();

   //Make the constructor private so that this class cannot be instantiated
   private Singleton(){}

   //Get the only object available
   public static Singleton getInstance(){
      return instance;
   }
}
````
The line `private static final Singleton instance = new Singleton();` is only executed when the class Singleton is actually used. This guaranteed the instantiation to be thread safe. To use the singleton class:
````java
Singleton s = Singleton.getInstance();
````

The other ways to build a Singleton class are:

**Using an Enum**
````java
public enum Singleton{
    INSTANCE;
}
````
**Locking /Lazy loading with Double checked Locking**
````java
public class Singleton{
     private static volatile Singleton instance;

     private Singleton(){}

     public static Singleton getInstance(){
         if(instance == null){
            synchronized(Singleton.class){
                //double checking Singleton instance
                if(instance == null){
                    instance = new Singleton();
                }
            }
         }
         return instance;
     }
}
````

###Immutable objects
Immutable objects are simply objects whose state (data) cannot change after construction, for examples the String class. They are useful in concurrent applications, since they cannot change state, they cannot be corrupted by threads.

There are several ways for creating immutable objects:
* Don't provide "setter" methods — methods that modify fields or objects referred to by fields.
* Make all fields final and private.
* Don't allow subclasses to override methods. The simplest way to do this is to declare the class as final.
* Make the class a Singleton
* If the instance fields include references to mutable objects, don't allow those objects to be changed:
    * Don't provide methods that modify the mutable objects.
    * Don't share references to the mutable objects. Never store references to external, mutable objects passed to the constructor; if necessary, create copies, and store references to the copies. Similarly, create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.
