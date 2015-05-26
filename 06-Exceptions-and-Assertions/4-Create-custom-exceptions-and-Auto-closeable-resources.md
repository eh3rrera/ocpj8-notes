#Create custom exceptions and Auto-closeable resources
###Custom exceptions
We can create our own exceptions by extending the [java.lang.Exception](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html) class. For example:
````java
class MyException extends Exception {
  public MyException(String message) {
    super(message);
  }
}
public class Test {
  public static void main(String args[]) {
    try{
            throw new MyException("My exception...");
        } catch(MyException e){
            e.printStackTrace();
        }
  }
}
````
You can also extend from [RuntimeException](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html), to make your exception unchecked (so it doesn't have to be catched if you don't want to).

###Auto-closeable resources
You can implement the [java.lang.AutoCloseable](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) or [java.lang.Closeable](https://docs.oracle.com/javase/8/docs/api/java/io/Closeable.html) interfaces in your own classes and use them with a try-with-resources block. However, the close method of the *Closeable* interface throws exceptions of type *IOException* while the close method of the *AutoCloseable* interface throws exceptions of type Exception. So it's better to implement *AutoCloseable*, since you can override this behavior and throw other exceptions or no exception at all.

*AutoClosable* only has one method called close():
````java
public interface AutoClosable {
    public void close() throws Exception;
}
````
So an implementation would look like this:
````java
public class MyAutoClosable implements AutoCloseable {
    public void someMethod() {
       System.out.println("Doing something");
    }

    @Override
    public void close() throws Exception {
        System.out.println("Closed!");
    }
}
````
And this is how you'd use it:
````java
try(MyAutoClosable ac = new MyAutoClosable()){
    ac.someMethod();
}
````
The output:
````
Doing something
Closed!
````
