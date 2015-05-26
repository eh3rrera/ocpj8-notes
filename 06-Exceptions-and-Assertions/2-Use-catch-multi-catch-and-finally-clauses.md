#Use catch, multi-catch, and finally clauses
###Catch and multi-catch
If you're handling multiple exceptions, the catch blocks must be ordered from most specific to most general, for example, the catch for IndexOutOfBoundsException must come before catch for Exception, otherwise, a compile-time error is generated:
````java
try {  
  int arr[] = new int[5];  
  arr[10] = 20;  
}  
catch(ArrayIndexOutOfBoundsException e) {
  e.printStackTrace();
}  
catch(ArithmeticException, e) {
  e.printStackTrace();
}  
````

The problem with this example is that it contains duplicate code in each of the catch blocks. For this situation, since Java 7, we can use a multi-catch block:
````java
try {  
  int arr[] = new int[5];  
  arr[10] = 20;  
  int r = arr[10]/10;
}  
catch(ArrayIndexOutOfBoundsException|ArithmeticException, ex) {
  ex.printStackTrace();
}  
````
The multi-catch clause specifies the types of exceptions that the block can handle, and each exception type is separated with a vertical bar (|). In this case, the catch parameter is implicitly final. So in the example, the catch parameter ex is final and therefore you cannot assign any values to it within the catch block.

A restriction when using the multi-catch clause is that you can use related exceptions (subclasses) in the same clause because it is redundat, the exception would already be caught by an alternative. For example, the following is invalid, since ArrayIndexOutOfBoundsException is a subclass of Exception:
````java
try {  
  int arr[] = new int[5];  
  arr[10] = 20;  
  int r = arr[10]/10;
}  
catch(ArrayIndexOutOfBoundsException|Exception, ex) { // compile-time error
  ex.printStackTrace();
} 
````

###Finally
A finally block is always executed whether exception is handled or not. It's an optional block, and if there's one, it goes after a try or catch block. This means the following blocks are both valid:
````java
try {
  // code that might throw an exception 
} catch(Exception e) {
  // handle exception
} finally {
  // code that it's executed no matter what
}

try {
  // code that might throw an exception 
} finally {
  // code that it's executed no matter what
}
````

So for each try block there can be zero or more catch blocks, but only one finally block.

The only situation where a finally block will not be executed, it's if the program exits abruptly (either by calling `System.exit()` or by a fatal error that causes the process to abort). Finally gets called even in the following case, before the method returns:
````java
void m() {
  try {  
      throws Exception();  
  }  
  catch (Exception e) {   
      return failure;  
  }  
  finally {  
      System.out.println("Of course this is printed");
  }
}
````
