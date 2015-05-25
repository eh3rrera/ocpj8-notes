#Read and write data from the console

###Console object
Access to the console depends upon the underlying platform and also upon the way in which the java program is invoked. If it's started from the command line without redirecting the standard input and output streams then its console will exist. If it's stated for example by a background job scheduler or an IDE, it's most likely that it will be no access to the console.

If there's a console,  it will be available with the `System.console()` method. If it's not available, an invocation of that method will return null.

Reading a line of text from the console:
````java
Console console = null;
String s = null;
try
{
   console = System.console();
   if (console != null)
   {
      s = console.readLine();
      System.out.println(s);
   }
} catch (Exception ex)
{
   ex.printStackTrace();
}
````
For reading a password or other secure data,`readPassword()` or `readPassword(String, Object...)` (that provides a formatted prompt) and manually zero the returned character array after processing to minimize the lifetime of sensitive data in memory:
````java
Console console = null;
char[] passwd = null;
try
{
   console = System.console();
   if (console != null)
   {
      if((passwd = cons.readPassword("[%s]", "Password:")) != null) {
        java.util.Arrays.fill(passwd, ' ');
      }
   }
} catch (Exception ex)
{
   ex.printStackTrace();
}
````
For writing, we have two equivalent methods that accept a [format string](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html#syntax):
````java
Console console = System.console();
if (console != null)
{
  console.format("[%s]", "Hi");
  console.printf("[%s]", "Hi again");
  console.format("Or just hi");
}
````

###Standard Streams
Java supports three standard streams: Standard Input, accessed through `System.in`; Standard Output, accessed through `System.out`; and Standard Error, accessed through `System.err`. These objects are defined automatically and do not need to be opened.

To read using streams:
````java
try {
   BufferedReader bufferRead = new BufferedReader(new InputStreamReader(System.in));
   String s = bufferRead.readLine();
    
   System.out.println(s);
}
catch(IOException ex)
{
  ex.printStackTrace();
}
 ````
 To write, standard output and standard error are both for output and they are defined as PrintStream objects:
 ````java
System.out.println("Hi");
System.out.print("Hi again\n");
 ````
 
