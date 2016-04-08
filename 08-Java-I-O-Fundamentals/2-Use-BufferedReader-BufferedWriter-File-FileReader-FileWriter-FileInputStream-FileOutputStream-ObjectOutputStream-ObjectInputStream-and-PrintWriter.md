#Use BufferedReader, BufferedWriter, File, FileReader, FileWriter, FileInputStream, FileOutputStream, ObjectOutputStream, ObjectInputStream, and PrintWriter in the java.io package.

[File](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)

This class is a representation of a file or a directory pathnames. Its instances are immutable, that is, once created, the abstract pathname represented by the object will never change.

You can create an instance this way:
````java
File file = new File("c:\\file.txt");
````
Or:
````java
File file = new File("/usr/file.txt");
````
Once you have created a File object you can do a lot of things:
````java
// Check if the corresponding file or directory actually exists
boolean fileExists = file.exists();

// Create a single directory if it does not already exist
boolean directoryCreated = file.mkdir();

// Read the length of the file in bytes
long length = file.length();

// Rename or move a file or directory:
boolean renameSuccessful = file.renameTo(new File("c:\\new-file.txt"));

// Delete the file or directory
success = file.delete();

// Check if the File object points to a directory
boolean isDirectory = file.isDirectory();

// Check if the file/directory is hidden
boolean isHidden = file.isHidden();

// Get a list (an array) of all the names of the files/directories in a directory
String[] fileNames = file.list();

// Get a list of all files/directories in a directory as instances of File
File[]   files = file.listFiles();

````

[FileReader](https://docs.oracle.com/javase/8/docs/api/java/io/FileReader.html)  
and  
[FileWriter](https://docs.oracle.com/javase/8/docs/api/java/io/FileWriter.html)

FileReader and FileWriter are character based, they are intended for reading and writing text. 

Here's an example code snippet for FileReader:
````java
Reader reader = new FileReader("c:\\file.txt");
int data = reader.read();
while(data != -1){
    char dataChar = (char) data;
    data = reader.read();
}
reader.close();
````
Here's an example code snippet for FileWriter:
````java
Writer writer = new FileWriter("c:\\file.txt");
writer.write("Hello World Writer");
writer.close();
````
FileReader extends from InputStreamReader, so it can work with an InputStream. At the same time, FileWriter extends from OutputStreamReader, so it can work with an OutputStream.

[FileInputStream](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)

FileInputStream reads the contents of a file as a stream of bytes. It's a subclass of InputStream. It can be created either with a String or a File object that represent a path. Here's an example:
````java
InputStream input = new FileInputStream("c:\\text.txt");
int byteData = input.read();
while(byteData != -1) {
  byteData = input.read();
}
input.close();
````
There's another version of `read()` that reads up to the length of an array of bytes of data from the input stream into that array:
````java
InputStream fis = new FileInputStream("c:\\text.txt");
byte[] data = new byte[1024];
int bytesRead = fis.read(data);
while(bytesRead != -1) {
  bytesRead = fis.read(data);
}
fis.close();
````

[FileOutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)

FileOutputStream writes the contents of a file as a stream of bytes. It's a subclass of OutputStream. It can be created either with a String or a File object that represent a path.

When you create a FileOutputStream representing a file that already exists, you can decide if you want to overwrite or to append to the existing file. It depends on the constructor you choose:
````java
OutputStream fos1 = new FileOutputStream("c:\\text.txt"); //overwrites file
OutputStream fos2 = new FileOutputStream("c:\\text.txt", true); //appends to file
OutputStream fos3 = new FileOutputStream("c:\\text.txt", false); //overwrites file
````

When you write to a FileOutputStream, the data may get cached internally in memory and written to disk at a later time. If you want to make sure that all data is written to disk without having to close the FileOutputStream, you can call its `flush()` method.

````java
OutputStream output = null;
try {
  output = new FileOutputStream("c:\\text.txt");

  while(moreData()) {
    int data = getData();
    output.write(data);
  }
} finally {
    if(output != null) {
        output.close();
    }
}
````
The other versions of the `write()` method are:
`write(byte[] bytes)`. It writes all the bytes in the byte array to the OutputStream.
`write(byte[] bytes, int offset, int length)`. It writes to the OutputStream length number of bytes starting from an offset of the byte array.

[BufferedReader](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)

BufferedReader provides buffering to a character-input stream. Rather than read one byte at a time, BufferedReader reads a larger block at a time. 
To add buffering to an InputStream just wrap it in a BufferedInputStream:
````java
Reader r = new BufferedReader(new FileReader("c:\\file.txt"));
````
The BufferedReader creates a byte array internally and fills it by calling the `read()` or `readLine()` methods on the underlying Reader. You can set the buffer size to use internally, for example to 1024 bytes, like this:
````java
Reader r = new BufferedReader(new FileReader("c:\\file.txt"), 1024);
````

[BufferedWriter](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)

BufferedWriter provides buffering to a character-output stream. To add buffering to a Writer just wrap it in a BufferedWriter:
````java
BufferedWriter input = new BufferedWriter(new FileWriter("c:\\file.txt"));
````
To set the size of the buffer, provide it as a constructor parameter like this:
````java
BufferedWriter input = new BufferedWriter(new FileWriter("c:\\file.txt"), 1024);
````
Without buffering, each invocation of a `write()` or `newLine()` method would cause characters to be converted into bytes and written immediately to the file, which can be very inefficient.

[ObjectInputStream](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectInputStream.html)

ObjectInputStream allows you to read serialized objects (their class must implement java.io.Serializable) from an InputStream instead of only bytes. You wrap an InputStream in an ObjectInputStream like this:
````java
class Test implements java.io.Serializable {}
...
ObjectInputStream input = new ObjectInputStream(new FileInputStream("obj.data"));
Test object = (Test) input.readObject();
input.close();   
````

[ObjectOutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/ObjectOutputStream.html)

ObjectOutputStream allows you to write serialized objects (their class must implement java.io.Serializable) from an OutputStream instead of only bytes. You wrap an OutputStream in an ObjectOutputStream like this:
````java
class Test implements java.io.Serializable {}
...
ObjectOutputStream output = new ObjectOutputStream(new FileOutputStream("obj.data"));
Test object = new Test();
output.writeObject(object);
output.close();  
````

[PrintWriter](https://docs.oracle.com/javase/8/docs/api/java/io/PrinterWriter.html) 

PrintWriter class allows you to write formatted data or data from primitive types instead of bytes to an underlying Writer. Here's an example:
````java
PrintWriter writer = new PrintWriter(new FileWriter("c:\\file.txt") );
writer.print(true);
writer.print(1);
writer.print(1.23);

// printf and format methods do the same
writer.printf("%s", "Hi");
writer.format("%s", "Hi");

writer.close();
````

The constructors of PrintWriter are:

`PrintWriter(File file)`  
Creates a new PrintWriter, without automatic line flushing, with the specified file.

`PrintWriter(File file, String csn)`  
Creates a new PrintWriter, without automatic line flushing, with the specified file and charset.

`PrintWriter(OutputStream out)`  `  
Creates a new PrintWriter, without automatic line flushing, from an existing OutputStream.

`PrintWriter(OutputStream out, boolean autoFlush)`  
Creates a new PrintWriter from an existing OutputStream.

`PrintWriter(String fileName)`  
Creates a new PrintWriter, without automatic line flushing, with the specified file name.

`PrintWriter(String fileName, String csn)`  
Creates a new PrintWriter, without automatic line flushing, with the specified file name and charset.

`PrintWriter(Writer out)`  
Creates a new PrintWriter, without automatic line flushing.

`PrintWriter(Writer out, boolean autoFlush)`  
Creates a new PrintWriter.
