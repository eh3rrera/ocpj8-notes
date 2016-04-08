#Use enumerated types including methods, and constructors in an enum type
Enumerated types (or enums) are classes that can be used to define a set of constants. They are type-safe, meaning that you cannot assign anything else other than the predefined constants to an enum variable.

Here's an example:
````java
public enum Colors {
    RED,
    BLUE,
    BLACK
}
````
You can refer to the constants in the enum like this:
````java
Colors color = Colors.BLUE;
````
Enums extend from `java.lang.Enum` implicitly, so they cannot extend another class. But they can implement an interface and override any method like a normal class.

You can specify values of enum constants at the creation time, but you need to define a constructor for this and, optionally, a method to get these values, for example:
````java
public enum Colors {
    RED("#ff0000"),
    BLUE("#3366cc"),
    BLACK("#000000");
    
    private String hexValue;

    private Colors(String hexValue) {
      this.hexValue = hexValue;
    }
    
    public String getHexValue() {
      return value;
    }
}
````
And the method is used like this:
````java
String value = Colors.BLUE.getHexValue();
````
If an enum contains attributes and methods, their definition  must always come after the list of constants in the enum and the list of constants must be terminated by a semicolon.

The constructor of an enum must be private, any other access modifier will result in compilation error. For this reason, you cannot create an instance of an enum by using the *new* operator.

Enums can be used in if statements in this way:
````java
Colors color = Colors.BLUE;

if( color == Colors.RED) {
  /** Do something */
} else if( color == Colors.BLUE) {
  /** Do something */
} else if( color == Colors.BLACK) {
  /** Do something */
}
````
And in switch statements like this:
````java
Colors color = Colors.BLUE;

switch (color) {
    case RED: /** Do something */; break;
    case BLUE: /** Do something */; break;
    case BLACK: /** Do something */; break;
}
````
You can also get all the possible values of an enum type by calling the static `values()` method:
````java
for (Colors c : Colors.values()) {
    System.out.println(c);
}
````
The order of the values is exactly the same in which they were defined.
