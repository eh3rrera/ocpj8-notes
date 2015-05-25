#Use BufferedReader, BufferedWriter, File, FileReader, FileWriter, FileInputStream, FileOutputStream, ObjectOutputStream, ObjectInputStream, and PrintWriter in the java.io package.

[File](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)
This class is a representation of a file or a directory pathnames. Its instaces are immutable, that is, once created, the abstract pathname represented by the object will never change.

You can create an instance this way:
´´´´java
File file = new File("c:\\file.txt");
´´´´
Or:
´´´´java
File file = new File("/usr/file.txt");
´´´´
Once you have created a File object you can do a lot of things:
´´´´java
// Check if the corresponding file actually exists
boolean fileExists = file.exists();

//

´´´´
