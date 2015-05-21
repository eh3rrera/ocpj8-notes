#Create and use a generic class
Generics introduce the concept of type variable. Type variable are delimited by angle brackets and follow the class (or the interface) name:
````java
class Test<T> {
  void m(T arg) { /** Do something with the argument of type T */ }
}
````
Type variables are really parameters that provide information to the compiler so it can check types. In the example above, class *Test* works with an object of type T, the same types that takes method *m*. Here's how we will use it:
````java
Test<String> t1 = new T<>();
t1.m("a");

Test<Integer> t2 = new T<>();
t2.m(1);
````
Notice that the generic parameter on the right is optional, it can be infered by the compiler using the reference declaration.

So generics are a mechanism for type checking, for example, when we create an instance of *List<String>*:
````java
List<String> l = new ArrayList<String>();
l.add("a");
l.add("b");
````
If we tried to put some other type of object different than *String*, the compiler would raise an error:
````java
l.add(1); //Compile-time error
````
To get a value from the collection:
````java
String s = l.get(0);
````
To iterate the collection:
````java
for(String s : l) {
    System.out.println(s);
}
````
Now consider this object hierarchy:
````java
public class Animal { }
public class Dog extends Animal { }
public class Cat extends Animal { }
````

There are three generic wildcard operators:
````java
List<?>           l1 = new ArrayList<>();
List<? extends Animal> l2 = new ArrayList<>();
List<? super   Animal> l3 = new ArrayList<>();
````
The unknown wildcard (`List<?>`) means the list is typed to an unknown type, so the list could hold any type. Since we don't know the type of the *List*, you can't add elements to the collection, you can only read from the collection and treat the objects as *Object* instances:
````java
List<?> l = new ArrayList<>();
for(Object o : l){
      System.out.println(o);
}
````
The extends wildcard (`List<? extends Animal>`) means the list can hold objects that are instances of *Animal*, or subclasses of *Animal* (e.g. *Dog* and *Cat*). Again, you cannot insert elements into the list, because you don't know the exact type of the list. But you can get the elements from the collection because you can safely say that its elements are of instances or subclasses of *Animal*:
````java
List<? extends Animal> l = new ArrayList<>();
for(Animal a : l){
      System.out.println(a);
}
````
The super wildcard  (`List<? super Animal>`) means the list is typed to either the *Animal* class, or a superclass of *Animal*. This time, you can insert elements into the list because you know that the list is typed to either *Animal* or a superclass of *Animal*, so it is safe to insert instances of *Animal* or subclasses of *Animal* (like *Dog or *Cat*) because they are an *Animal*:
````java
List<? super Animal> l = new ArrayList<>();
l.add(new Animal());
l.add(new Dog());
l.add(new Cat());
````
However, to get elements from the list, you must cast the result to *Object*, since the elements could be of any type that is either an *Animal* or a superclass, but it is not possible to know exactly which. The only thing you know for sure, is that any class is a subclass of *Object*:
````java
List<? super Animal> l = new ArrayList<>();
for(Object o : l){
      System.out.println(o);
}
````
