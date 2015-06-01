#Test invariants by using assertions

Assertions are statements that you can use to test your assumptions about the code during development. If the assertion turns out to be false, then an AssertionError is thrown. You can use assertions in two forms:
````java
private method(int i) {
  assert i > 0;
  //or
  assert i > 0 : "Parameter i must be a positive value"
  
  // Do something now that we know i is greater than 0
}
````
In the first form, the assert expression must evaluate to a boolean value. The other version adds a second
expression separated from the first boolean expression by a colon. This expression would be used when the assertion is false in addition to throwing AssertionError. This second expression must resolve to a value, otherwise, a compile-time error is generated.

To enable assertions, you have to compile the code with the assertion enabled. Then, when running the program, assertions have to be enabled again.

Assertions were added to Java since version 1.4, so before that version, you can use assert as an identifier. This is important because in Java 7, assertions are compiled by default, but you can override this behavior at the command line:
````
javac -source 1.3 Test.java
````
The command above will issue warnings when  the word assert is used as an identifier, but the code will compile and execute. But if you use any of the following commands:
````
javac -source 1.4 Test.java
javac -source 1.5 Test.java
javac -source 5 Test.java
javac -source 1.6 Test.java
javac -source 6 Test.java
javac -source 1.7 Test.java
javac -source 7 Test.java
javac Test.java
````
The compilation will fail if assert is used as an identifier.

So compilation is the first step to use assertions. But to execute the assertion checks, you have to enable them with:
````
java -ea com.example.Test
````
or
````
java -enableassertions com.example.Test
````

The default behavior is to run the code with assertions disabled, but the commands to explicitly disabling assertions are:
````
java -da com.example.Test
````
or
````
java -disableassertions com.example.Test
````
However, this command is useful in the case you want to enable assertions for some classes or packages only, for example:
````
java -ea -da:com.example.PrintUtil com.example.Test
````
To disable assertions only for the com.example.Test class. Or:
````
java -ea -da:com.example.util... com.example.Test
````
To disable assertions for the com.example.util package and all of its subpackages.

But no all uses of assertions are considered appropriate. Here are the rules:
* Don't use assertions to validate arguments to a public method
* Use assertions to validate arguments to a private method
* Don't use assertions to validate command-line arguments
* Use assertions, even in public methods, to check for cases that are never supposed to happen
* Don't use assert expressions that can cause side effects. For example:

  ````java
  private void m(List<Integer> l) {
    assert checkSize(l);
  }
  private boolean checkSize(List<Integer> l) {
    l.add(10);
    return l.size() > 3;
  }
  ````
