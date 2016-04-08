#Filter a collection by using lambda expressions

The way to filter collections is through the use of a [Predicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html), which is basically something that returns a boolean value.

*Predicate* is a functional interface, which means that wherever an implementation of this interface is expected, we can pass a lambda expression.

For example, consider a list of objects of this class:
````java
class Person {
	private int age;
	private String name;
 
	public int getAge() {
		return age;
	}
 
	public void setAge(int age) {
		this.age = age
	}
 
	public String getName() {
		return name;
	}
 
	public void setName(String name) {
		this.name = name;
	}
}
````
To filter the list, first we need to convert it to a stream and then pass a lambda expression that returns a boolean value to its `filter()` method:
````java
List filterd = l.stream().filter(p -> p.getAge() > 20).collect(Collectors.toList());
````

But what if we want to use multiple conditions to filter the list? The *Predicate* interface has some methods to join conditions:
````java
Predicate<Person> nameNotNull = p -> p.getName() != null;
Predicate<Person> ageAbove20 = p -> p.getAge() > 20;

Predicate<Person> multipleConditions = nameNotNull.and(ageAbove20);
List filterd = l.stream().filter(multipleConditions).collect(Collectors.toList());
````
