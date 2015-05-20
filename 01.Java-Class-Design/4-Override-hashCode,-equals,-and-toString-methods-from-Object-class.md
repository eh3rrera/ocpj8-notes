#Override hashCode, equals, and toString methods from Object class

###equals
From [javadoc](http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals-java.lang.Object-):

`public boolean equals(Object obj)`
Indicates whether some other object is "equal to" this one.  
The equals method implements an equivalence relation on non-null object references:
* It is reflexive: for any non-null reference value x, x.equals(x) should return true.
* It is symmetric: for any non-null reference values x and y, x.equals(y) should return true if and only if y.equals(x) returns true.
* It is transitive: for any non-null reference values x, y, and z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) should return true.
* It is consistent: for any non-null reference values x and y, multiple invocations of x.equals(y) consistently return true or consistently return false, provided no information used in equals comparisons on the objects is modified.
* For any non-null reference value x, x.equals(null) should return false.
* The equals method for class Object implements the most discriminating possible equivalence relation on objects; that is, for any non-null reference values x and y, this method returns true if and only if x and y refer to the same object (x == y has the value true).

It is generally necessary to override the `hashCode` method whenever this method is overridden, so as to maintain the general contract for the `hashCode` method, which states that equal objects must have equal hash codes.

###hashCode
From [javadoc](http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#hashCode--):

`public int hashCode()`
Returns a hash code value for the object. This method is supported for the benefit of hash tables such as those provided by `HashMap`.
The general contract of hashCode is:
* Whenever it is invoked on the same object more than once during an execution of a Java application, the `hashCode` method must consistently return the same integer, provided no information used in equals comparisons on the object is modified. This integer need not remain consistent from one execution of an application to another execution of the same application.
* If two objects are equal according to the equals(Object) method, then calling the `hashCode` method on each of the two objects must produce the same integer result.
* It is not required that if two objects are unequal according to the equals(java.lang.Object) method, then calling the `hashCode` method on each of the two objects must produce distinct integer results. However, the programmer should be aware that producing distinct integer results for unequal objects may improve the performance of hash tables.
* As much as is reasonably practical, the hashCode method defined by class `Object` does return distinct integers for distinct objects. (This is typically implemented by converting the internal address of the object into an integer, but this implementation technique is not required by Java.)

The relation between the two methods is:

Whenever `a.equals(b`), then `a.hashCode()` must be same as `b.hashCode()`.

###toString
From [javadoc](http://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#toString--):

`public String toString()`
Returns a string representation of the object. In general, the `toString` method returns a string that "textually represents" this object. The result should be a concise but informative representation that is easy for a person to read. It is recommended that all subclasses override this method.
The `toString` method for class `Object` returns a string consisting of the name of the class of which the object is an instance, the at-sign character `@', and the unsigned hexadecimal representation of the hash code of the object. In other words, this method returns a string equal to the value of:

 `getClass().getName() + '@' + Integer.toHexString(hashCode())`
 
  
  
 The following is an example of an implementation for these methods:
 ````java
 public class Person {
   private final String lastName;
   private final String firstName;
   private final boolean female;
   
   @Override
   public boolean equals(Object obj)
   {
      if (obj == null)
      {
         return false;
      }
      if (getClass() != obj.getClass())
      {
         return false;
      }
      final Person other = (Person) obj;
      if ((this.lastName == null) ? (other.lastName != null) : !this.lastName.equals(other.lastName))
      {
         return false;
      }
      if ((this.firstName == null) ? (other.firstName != null) : !this.firstName.equals(other.firstName))
      {
         return false;
      }
      if (this.female != other.female)
      {
         return false;
      }
      return true;
   }
   
   @Override
   public int hashCode()
   {
      int hash = 3;
      hash = 19 * hash + (this.lastName != null ? this.lastName.hashCode() : 0);
      hash = 19 * hash + (this.firstName != null ? this.firstName.hashCode() : 0);
      hash = 19 * hash + (this.female ? 1 : 0);
      return hash;
   }

   @Override
   public String toString()
   {
      return  "Person{" + "lastName=" + lastName + ", firstName=" + firstName
            + ", female=" + female +  '}';
   }
 }
 ````
