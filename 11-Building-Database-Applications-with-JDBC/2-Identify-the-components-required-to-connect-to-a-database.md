#Identify the components required to connect to a database using the DriverManager class including the JDBC URL
When working with JDBC, the first thing you need to do is to establish a connection with a data source (like a DBMS). One way to this is to use the class [DriverManager](https://docs.oracle.com/javase/8/docs/api/java/sql/DriverManager.html).

DriverManager connects an application to a data source by using a database URL. When this class first attempts to establish a connection, it automatically loads any JDBC 4.0 drivers found within the class path.

A database URL varies depending on the DBMS used. For example, for MySQL it looks like this:
````
jdbc:mysql://localhost:3306/data
````
Where localhost is the name of the server that is hosting the database, 3306 is the port number and data is the name of the database.

In previous versions of JDBC, to get a connection, you first had to initialize the JDBC driver by calling the method `Class.forName()`. Since JDBC 4.0, drivers that are found in your class path are automatically loaded. 

To connect to a data source using DriverManager, we need to get a [Connection](https://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html) object with something like the following snippet:
````java
Properties props = new Properties();
props.put("user", userName);
props.put("password", password);

Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/data");
````
