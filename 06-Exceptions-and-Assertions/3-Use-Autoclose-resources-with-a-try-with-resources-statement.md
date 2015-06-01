#Use Autoclose resources with a try-with-resources statement

Normally, a finally block is used to ensure that a resource is closed whether the try statement completes normally or not. For example:
````java
BufferedReader br = new BufferedReader(new FileReader(path));
try {
    return br.readLine();
} catch(IOException e) {
    e.printStackTrace();
} finally {
    if (br != null) br.close();
}
```` 

However, Java 7 introduced the try-with-resources statement, which ensures that each resource is closed at the end of the statement. Any object that implements `java.lang.AutoCloseable`, which includes all objects which implement `java.io.Closeable`, can be used as a resource. The above example can be rewritten with a try-with-resources statement like this:
````java
try (BufferedReader br = new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
````

But there's a subtle difference between these two try blocks. If the methods `readLine()` and `close()` both throw exceptions, then the method in the first example throws the exception thrown from the finally block (from `close()`) and the exception thrown from the try block (from `readLine()`) is suppressed. In contrast, in the try-with-resources example, if exceptions are thrown from both the try block (from `readLine()`) and the try-with-resources statement (from `close()`), then the exception from the try block is thrown and the exception thrown from the try-with-resources block is suppressed. You can retrieve these suppressed exceptions by calling the `Throwable.getSuppressed()` method from the exception thrown by the try block.

The [Closeable](https://docs.oracle.com/javase/8/docs/api/java/io/Closeable.html) interface extends the [AutoCloseable](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) interface. The `close()` method of the Closeable interface throws exceptions of type IOException while the close method of the AutoCloseable interface throws exceptions of type Exception.

You may declare more than one resources in a try-with-resources statement, separated by a semicolon. When the try block   terminates, either normally or because of an exception, the `close()` methods of the resources are automatically called in the opposite order of their creation. For example:
````java
// At the end, br2 is closed before br1.
try (BufferedReader br1 = new BufferedReader(new FileReader(path1)); 
      BufferedReader br2 = new BufferedReader(new FileReader(path2))) {
        String l1 =  br1.readLine();
        String l2 =  br2.readLine();
    }
````

An important note, in a try-with-resources statement, any catch or finally blocks are run after the resources declared have been closed.
