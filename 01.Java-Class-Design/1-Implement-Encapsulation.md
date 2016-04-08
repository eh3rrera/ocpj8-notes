# Implement encapsulation

Encapsulation means keeping the internal workings of your code safe from other programs that use it, allowing only what you choose to be accessed. This makes the code that uses the encapsulated code much simpler and easier to maintain since much of the complexity of the latter is hidden.

The main benefit of encapsulation is that it protects a class from being used in a way that it wasn't meant to be. By controlling the way the code is used, it can only ever do what you want it to do. 

For example, if we set variables like this:
````java
car.model = 2015;
````
We can't prevent something invalid like this:
````java
car.model = 2343242;
````
To implement encapsulation, we set up the class so only its methods can refer to its instance variables. External code will access these private instance variables only through public get/set methods. This is a convention used in reusable components called JavaBeans. The rules are:
* Instance variables are *private*
* Getter methods begin with *get* if the property is not a *boolean*, otherwise, they begin with *is*
* Setter methods begin with *set*
* The method name starts with get/is/set followed by the name of the instance variable with its first letter in uppercase

So if we have a class like the following:
````java
public class Car {
  int model;
  String name;
  String color;
}
````
The encapsulated version would look like this:
````java
public class Car {
  private int model;
  private String name;
  private String color;
  
  public int getModel() {
    return model;
  }
  public String getName() {
    return name;
  }
  public String getColor() {
    return color;
  }
  public void setModel(int model) {
    this.model = model;
  }
  public void setName(int name) {
    this.name = name;
  }
  public void setColor(int color) {
    this.color = color;
  }
}
````
Notice the use of `this` in the setter methods. The parameter name can be anything, but if it's the same as the instance variable's name, `this` (that references the instance) must be used to differentiate between them.

Of course, just like that, in the surface this code does the same as the non-encapsulated version, but by using a method instead of getting/setting the instance variable directly, we can add something like a validation without breaking the external code:
````java
public void setModel(int model) {
  if(model >= 2000 && model <= 2015) {
    this.model = model;
  } else {
    this.model = 2000;
  }
}
````
Now, if we set an invalid value:
````java
car.setModel(2343242);
````
We'll get a default and valid value that will protect the class from being used in a way it wasn't meant to be.

Encapsulation can also be used with constructors and methods of a class. The key thing is to restrict the access to any member of the class that can break things when something changes or that doesn't want to be exposed.
