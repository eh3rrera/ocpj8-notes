#Use Stream API with NIO.2

In Java 8, the class [Files](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html) adds methods that allow us to use streams with files. 

###List
````java
public static Stream<Path> list(Path dir)
````
Streams all the elements of a given directory. This method is not recursive. For example:
````java
try (Stream<Path> stream = Files.list(Paths.get("c:\\data"))) {
    stream.map(String::valueOf)
        .filter(path -> path.endsWith(".txt"))
        .forEach(System.out::println);
}
````
The example maps each path to its string representation, filter the results (only files ending in .txt) and print them. Streams implement AutoCloseable, so the try-with-resources block should be used to ensure that the stream's close method is invoked after the stream operations are completed.

###Find and Walk
````java
public static Stream<Path> find(Path start, int maxDepth,  BiPredicate<Path,BasicFileAttributes> matcher, FileVisitOption... options)
````
Search for files starting at the given Path that represents the root of the file tree with the maximum number of directory levels to search given by the parameter maxDepth. For each file encountered, the given BiPredicate is invoked and the file is only included in the returned Stream if the BiPredicate returns true. For example:
````java
try (Stream<Path> stream = Files.find(Paths.get("c:\\data"), 3, 
                                        (path, attr) -> String.valueOf(path).endsWith(".txt"))) {
    stream.map(String::valueOf).forEach(System.out::println);
}
````
The example searches for all txt files and print their path and name.

````java
public static Stream<Path> walk(Path start, int maxDepth,  FileVisitOption... options)
public static Stream<Path> walk(Path start, FileVisitOption... options) // This visits all levels of the directory tree.
````
We can do the same thing but using the walk method and a stream filter:
````java
try (Stream<Path> stream = Files.walk(Paths.get("c:\\data"), 3)) {
    stream.map(String::valueOf).
          filter(path -> path.endsWith(".txt")).
          forEach(System.out::println);
}
````
However, the find method is more efficient for these cases.

###Read lines and BufferedReader
````java
public static Stream<String>	lines(Path path, Charset cs)
public static Stream<String>	lines(Path path) // Uses the UTF-8 charset.
````
This method reads all lines from a file into a stream. For example:
````java
try (Stream<String> stream = Files.lines(Paths.get("c:\\data\\file.txt"))) {
    stream.map(String::toLowerCase).forEach(System.out::println);
}
````

[BufferedReader](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html) also supports stream with its lines method:
````java
try (BufferedReader reader = Files.newBufferedReader(Paths.get("c:\\data\files.txt"))) {
    reader.lines().map(String::toLowerCase).forEach(System.out::println);
}
````
