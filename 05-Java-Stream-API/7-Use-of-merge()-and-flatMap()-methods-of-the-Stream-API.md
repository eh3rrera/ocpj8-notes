#Use of merge() and flatMap() methods of the Stream API
````java
<R> Stream<R> flatMap(Function<? super T,? extends Stream<? extends R>> mapper)
````
This method returns a stream consisting of the results of replacing each element of the original stream with the content of the stream produced by the provided function (if the function returns null, an empty stream is used, instead).

This method is commonly used in one to many relationships to flatten all the elements into a new stream.

For example, consider the following classes:
````java
class Student {
  private int id;
  private String name;
  public int getId() {
    return id;
  }
  public String getName() {
    return name;
  }
  public void setId(int id) {
    this.id = id;
  }
  public void setName(String name) {
    this.name = name;
  }
}
class Course {
  private List<Student> students;
  private String name;
  public List<Student> getStudents() {
    return students;
  }
  public String getName() {
    return name;
  }
  public void setStudents(List<Student> students) {
    this.students = students;
  }
  public void setName(String name) {
    this.name = name;
  }
}
````
Assuming there's a list of courses and each course has a list of students that take that course, if we want to aggregate the names of all students taking a course into one stream, the following code will do it:
````java
List<String> students = courses.stream()
                .flatMap(course -> course.getStudents().stream()) //Get the students of each course
                .map(student -> student.getName()) //Now that we have a stream with all the students, we extract their name
                .collect(Collectors.toList());
````

There are other examples in the [javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#flatMap-java.util.function.Function-) of the method.
