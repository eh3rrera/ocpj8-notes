#Use java.util.Comparator and java.lang.Comparable interfaces
`compareTo(obj)` is from the [Comparable](http://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) interface and is called on one object, to compare it to another object, so the object to be compared has to implement this interface.
````java
String s = "hello";
int result = s.compareTo("world");
````
`compare(obj1, obj2)` is from the [Comparator](http://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html) interface and is called on some object to compare two other objects, so an utility class has to implement this interface to be used somewhere else.
````java
Comparator<String> comp = new MyComparator<>();
int result = comp.compare("hello", "world");
````

Java classes that have a natural ordering implement the *Comparable* interface (like *String*, *Integer*, *BigInteger*, etc).

The *Comparator* interface is tipically used for sorting data structures such as *TreeMap* and *TreeSet* or to be passed to a sort method (such as `Collections.sort` or `Arrays.sort`).

Both methods return:
0 if the objects are equal (this have to be consistent with the equals() method)
-1 if the first object (or the object making the comparison) is "less" than the other object
1 if the first object (or the object making the comparison) is "greater" than the other object

Here's and example:
````java
class Person implements Comparable<Person> {
	private int age;
	private String name;
 
	public Person(int age, String name) {
		this.age = age;
		this.name = name;
	}
 
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
 
	@Override
	public int compareTo(Person p) {
		if (this.getAge() > p.getAge())
			return 1;
		else if (this.getAge() < p.getAge())
			return -1;
		else
			return 0;
	}
}

class AgeComparator implements Comparator<Person> {
	@Override
	public int compare(Person p1, Person p2) {
		int age1 = p1.getAge();
		int age2 = p2.getAge();
 
		if (age1 > age2) {
			return 1;
		} else if (age1 < age2) {
			return -1;
		} else {
			return 0;
		}
	}
}

public class Test {
	public static void main(String[] args) {
		Pesron p1 = new HDTV(60, "James");
		Person p2 = new HDTV(55, "Bryan");
 
		if (p1.compareTo(p2) > 0) {
			System.out.println(p1.getName() + " is older.");
		} else {
			System.out.println(p2.getName() + " is older.");
		}
		
		//Sorted by age
		List<Person> l = new ArrayList<>();
		l.add(p1);
		l.add(p2);
 
		Collections.sort(l, new AgeComparator());
		for (Person p : l)
		  System.out.println(p.getName());
	}
}
````

Output:
````
James is older
Bryan
James
````
