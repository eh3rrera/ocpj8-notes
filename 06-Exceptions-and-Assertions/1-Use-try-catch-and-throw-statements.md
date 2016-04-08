#Use try-catch and throw statements
A try block is used to enclose code that might throw an exception and it can be followed by one or many catch block. 

A catch block is used to handle an exception. It defines the type of the exception and a reference. For example:
````java
try {  
// Code that may throw an exception  
} catch(Exception e){
 // Do something with the exception using reference e
} 
````

If exception is not handled, the Java Virtual Machine provides a default exception handler that performs the following tasks:

1. Prints out exception description.
2. Prints the stack trace (Hierarchy of methods where the exception occurred).
3. Causes the program to terminate.

But if an exception is handled by in a try-catch block, the normal flow of the application is maintained and rest of the code is executed.

If you want to manually throw an exception, use the throw keyword:
````java
public class Test {  
   public static boolean validateName(String name) {
      boolean valid = true;
      try {
        if(name != null) {
         throw new Exception("The name is not valid");
        }
      } catch(Exception e) {
        valid = false;
      }
      
      return valid;
   }  
   public static void main(String args[]) {  
      if(validateName(null)) {
        System.out.println("Valid Name");
      } else {
        System.out.println("Invalid Name");
      }
  }  
} 
````
The output is:
````
Invalid name
````
