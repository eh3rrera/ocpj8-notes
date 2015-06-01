#Use Path interface to operate on file and directory paths

The [Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html) interface defines an object that represents the path to a file or a directory. 

A Path object has a root component and a hierarchical sequence of names separated by backslashes (in Windows) or slashes (Unix/Linux). The root component identifies the file system being used, for example, a drive letter. The names represent the directories needed to navigate to the target file or directory. The last name in the sequence represents the name of the target file or directory.

To create a Path object you can use the the get method of the Paths class like this:
````java
Path p1 = Paths.get("c:\\file.txt"); // using an absolute path
Path p2 = Paths.get("c:\\data", "examples\\file.txt"); // using a relative path to construct the path c:\data\examples\file.txt
````

When working with relative paths you can use:
* **.** to refer to the current directory
* **..** to refer to the parent directory

For example:
````java
Path p1 = Paths.get("c:\\data\\.\\file.txt"); // refers to c:\data\file.txt
Path p2 = Paths.get("c:\\data\\examples\\..\\file.txt"); // refers to c:\data\file.txt
````

The `normalize()` method of the Path interface can normalize a path, meaning that it removes all the **.** and **..** in the path and resolves to the real path it refers to. 

You can convert a relative path to an absolute path like this:
````java
Path p1 = Paths.get("file.txt");
Path p2 = p1.toAbsolutePath(); // refers for example to c:\data\file.txt
````

You can convert a Path to a File and a File to a Path like this:
````java
File f = Paths.get("file.txt").toFile();
Path p = new File("file.txt").toPath();
````

Path stores the name elements as a sequence. The highest element is located at index 0. The following code snippet shows some methods to get information about the path:
````java
Path path = Paths.get("c:\\users\\admin\\file.txt"); 
Path path = path.getFileName(); // returns file.txt
Path path = path.getName(0); // returns users
int count = path.getNameCount(); // returns 3 (users, admin and file.txt)
Path path = path.subpath(0, 2); // returns users/admin
Path path = path.getParent(); // returns /users/admin
Path path = path.getRoot(); // returns c:\ (if we were in a unix filesystem, it would return /)
````
