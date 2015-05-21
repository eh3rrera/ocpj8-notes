#Create and use ArrayList, TreeSet, TreeMap, and ArrayDeque objects
###ArrayList
ArrayList is an implementation of the List interface that internally uses an Array to store the elements. This implementation is not synchronized.

Each ArrayList instance has a capacity. The capacity is the size of the array used to store the elements in the list. It is always at least as large as the list size. As elements are added to an ArrayList, its capacity grows automatically.

Here's the [javadoc](http://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html) and an example:
````java
public class Test {
  public static void main(String[] args) {
  	List<Integer> l = new ArrayList<>();
  
  	// Add elements
  	l.add(1);
  	l.add(2);
  	l.add(3);
  
  	// Get size.
  	int count = l.size();
  
  	// Get an element with the zero-based index.
  	Integer i = l.get(0);
  }
}
````

###TreeSet
TreeSet is an implementation of the Set interface that uses a tree for storage, which makes access time very fast. The elements are ordered using their natural ordering, or by a Comparator provided at set creation time, depending on which constructor is used. This implementation is not synchronized.

Here's the [javadoc](http://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) and an example:
````java
public class Test {
  public static void main(String[] args) {
  	Set<Integer> ts = new TreeSet<>();
  
  	// Add elements
  	ts.add(2);
  	ts.add(1);
  	ts.add(3);
  
  	// Get size.
  	System.out.println(ts); // Prints [1,2,3]
  }
}
````

###TreeMap
TreeMap is an implementation of the Map interface that uses a tree for storage key/value pairs, which makes access time very fast. The elements are ordered using the natural ordering or their keys, or by a Comparator provided at map creation time, depending on which constructor is used. This implementation is not synchronized.

Here's the [javadoc](http://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) and an example:
````java
public class Test {
  public static void main(String[] args) {
  	  Map<String, Integer> tm = new TreeMap<>();
      // Put elements to the map
      tm.put("A", 10);
      tm.put("C", 40);
      tm.put("B", 20);
      
	    // Get a set of the entries
      Set<Entry<String, Integer>> set = tm.entrySet();
      // Get an iterator
      Iterator<Entry<String, Integer>> i = set.iterator();
      // Display elements
      while(i.hasNext()) {
         Entry<String, Integer> me = i.next();
         System.out.print(me.getKey() + ": ");
         System.out.println(me.getValue());
      }
      
      // Get an element
      Integer i = tm.get("C"));
  }
}
````

###ArrayDeque
ArrayDeque is an implementation of the Deque interface.  Array deques have no capacity restrictions; they grow as necessary to support usage. They are not thread-safe. Null elements are prohibited. This class and its iterator implement all of the optional methods of the Collection and Iterator interfaces. Elements are stored in the order (first or last) in which they are inserted.

Here's the [javadoc](http://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html) and an example:
````java
public class Test {
  public static void main(String[] args) {
  	Deque<Integer> d = new ArrayDeque();
  
  	//Add elements
  	d.add(1); //add element at tail
    d.addFirst(2); //add element at head
    d.addLast (3); //add element at tail
    
    //Get elements
    Integer firstElement1 = d.element(); //peek at the element at the head without taking the element out of the queue (throws exception is the queue is empty)
    Integer firstElement2 = d.peek(); //peek at the element at the head without taking the element out of the queue (returns null is the queue is empty)
    Integer firstElement3 = d.getFirst();//get first element (throws exception is the queue is empty)
    Integer firstElement4 = d.peekFirst();//get first element (returns null is the queue is empty)
    Integer lastElement1  = d.getLast();//get last element (throws exception is the queue is empty)
    Integer lastElement2  = d.peekLast();//get last element (returns null is the queue is empty)
    
    //Remove elements
    Integer element1 = d.remove(); //retrieves and removes the head of the queue
    Integer element2 = d.removeFirst(); //retrieves and removes the first element of the queue
    Integer element3  = d.removeLast(); //retrieves and removes the last element of the queue
  }
}
````
