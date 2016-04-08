#Use Files class to check, read, delete, copy, move, manage metadata of a file or directory

The class [Files](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html) contains static methods that operate on files and directories.

###Check files
The `Files.exists()` method checks if a given Path exists in the file system, for example
````java
Path path = Paths.get("data/logging.properties");
boolean exists = Files.exists(path, new LinkOption[]{ LinkOption.NOFOLLOW_LINKS});
````
The LinkOption parameter is used to indicate how symbolic links are handled if the file is a symbolic link. By default, symbolic links are followed. If the option NOFOLLOW_LINKS is present as in the example, then symbolic links are not followed.

There's also:
````java
static boolean	notExists(Path path, LinkOption... options)
````
That tests whether the file located by this path does not exist.

###Read files
The methods for reading a file are:
````java
public static byte[] readAllBytes(Path path) throws IOException
````
Reads all the bytes from a file.

````java
public static List<String> readAllLines(Path path,  Charset cs) throws IOException
````
Read all lines from a file. Bytes from the file are decoded into characters using the specified charset.

````java
public static List<String> readAllLines(Path path)  throws IOException
````
Read all lines from a file. Bytes from the file are decoded into characters using the UTF-8 charset.

All methods ensure that the file is closed when all bytes have been read or an I/O error, or other runtime exception, is thrown. Also, they are not designed for reading large files. Here's an example
````java
Path path = Paths.get("file.txt");
try {
    List<String> lines = Files.readAllLines(path);
} catch (IOException e) {
    // something failed
    e.printStackTrace();
}
````

###Delete files
The `Files.delete()` method can delete a file or directory. Here's an example:
````java
Path path = Paths.get("file.txt");
try {
    Files.delete(path);
} catch (IOException e) {
    // deleting failed
    e.printStackTrace();
}
````
This method will only delete a directory if it is empty.

###Copy files
The `Files.copy()` method copies a file from one path to another. If the destination file already exists, a `java.nio.file.FileAlreadyExistsException` is thrown:
````java
Path source  = Paths.get("file.txt");
Path target = Paths.get("file-copy.txt");

try {
    Files.copy(source, destination);
} catch(FileAlreadyExistsException fae) {
    fae.printStackTrace();
} catch (IOException e) {
    // something else went wrong
    e.printStackTrace();
}
````
If you want to overwrite an existing file use this line:
````java
Files.copy(source, destination, StandardCopyOption.REPLACE_EXISTING);
````

###Move files
`Files.move()` moves a file. Moving a file is the same as renaming it, but moving an both move it to a different directory and change its name in the same operation. If the destination file already exists, a `java.nio.file.FileAlreadyExistsException` is thrown:
````java
Path source  = Paths.get("file.txt");
Path target = Paths.get("file-moved.txt");

try {
    Files.move(source, destination);
} catch(FileAlreadyExistsException fae) {
    fae.printStackTrace();
} catch (IOException e) {
    // something else went wrong
    e.printStackTrace();
}
````
If you want to overwrite an existing file use this line:
````java
Files.move(source, destination, StandardCopyOption.REPLACE_EXISTING);
````

###Manage metadata
The following methods can be used to extract information about the file or directory:
````java
public static boolean isDirectory(Path path, LinkOption... options)
````
Tests whether a file is a directory.

-----

````java
public static boolean isExecutable(Path path)
````
Tests whether a file is executable.

-----

````java
public static boolean isHidden(Path path)
````
Tells whether or not a file is considered hidden.

-----

````java
public static boolean isReadable(Path path)
````
Tests whether a file is readable.

-----

````java
public static boolean isWritable(Path path)
````
Tests whether a file is writable.

-----

````java
public static long size(Path path)
````
Returns the size of a file (in bytes).

-----

````java
public static A <A extends BasicFileAttributes> readAttributes(Path path, Class<A> type, LinkOption... options)
````
Reads a file's attributes as a bulk operation. The type parameter is the type of the attributes and this method returns an instance of that type if supported. The implementations are:
* [BasicFileAttribute](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/BasicFileAttributes.html)
* [PosixFileAttributes](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/PosixFileAttributes.html)
* [DosFileAttributes](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/DosFileAttributes.html)

The options array may be used to indicate how symbolic links are handled. By default, symbolic links are followed.

For example:
````java
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class, LinkOption.NOFOLLOW_LINKS);
````

-----

````java
public static Map<String,Object> readAttributes(Path path, String attributes, LinkOption... options)
````
Reads a set of file attributes as a bulk operation. The attributes parameter identifies the attributes to be read and takes the form:
````
[view-name:]attribute-list
````
Where `view-name` is the name of a [FileAttributeView](https://docs.oracle.com/javase/8/docs/api/java/nio/file/attribute/FileAttributeView.html) that identifies a set of file attributes. If not specified, it defaults to "basic". Some possible values are:  
`"*"` - Read all basic-file-attributes.  
`"lastModifiedTime,lastAccessTime"` - Reads the last modified time  and last access time basic attributes.  
`"posix:*"` - Read all POSIX-file-attributes.  
`"posix:permissions,owner"` - Reads the POSX file permissions and owner.

The options parameter may be used to indicate how symbolic links are handled. By default, symbolic links are followed.

-----

````java
public static Object getAttribute(Path path, String attribute, LinkOption... options)throws IOException
````
Reads the value of a file attribute. The attribute parameter identifies the attribute to be read and takes the form:
````
[view-name:]attribute-name
````
The options parameter may be used to indicate how symbolic links are handled. By default, symbolic links are followed.

For example:
````java
int size = (Integer)Files.getAttribute(path, "basic:size");
````

-----

````java
public static Path setAttribute(Path path, String attribute,  Object value,  LinkOption... options)
````
Sets the value of a file attribute. The attribute parameter identifies the attribute to be set and takes the form:
````
[view-name:]attribute-name
````
The options parameter may be used to indicate how symbolic links are handled. By default, symbolic links are followed.

For example:
````java
Files.setAttribute(path, "dos:hidden", false);
````
