#Describe the interfaces that make up the core of the JDBC API including the Driver, Connection, Statement, and ResultSet interfaces and their relationship to provider implementations

[Driver](https://docs.oracle.com/javase/8/docs/api/java/sql/Driver.html).  Provides the API for registering and connecting drivers based on JDBC (every driver class must implement it). Generally used only by the DriverManager class

[DriverManager](https://docs.oracle.com/javase/8/docs/api/java/sql/DriverManager.html). To makes a connection with a driver.

[Connection](https://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html). Provides methods for creating statements and managing connections with a data source and their properties.

[Statement](https://docs.oracle.com/javase/8/docs/api/java/sql/Statement.html). Object used for executing a static SQL statement and returning the results it produces.

[ResultSet](https://docs.oracle.com/javase/8/docs/api/java/sql/ResultSet.html). Object used for retrieving and updating the results of a query.

To use the JDBC API with a particular DBMS, you need a JDBC driver to establish the communication between Java and the database. JDBC drivers are divided into four types:

Type 1: JDBC-ODBC (Open Database Connectivity) Bridge  
Type 2: Native-API, partly Java driver  
Type 3: Network-protocol, all-Java driver  
Type 4: Native-protocol, all-Java driver

All JDBC drivers implement four JDBC interfaces: 
* Driver
* Connection
* Statement
* ResultSet.

The DriverManager class tracks the loaded JDBC drivers and creates the database connections. Before JDBC 4.0, the Driver class was loaded with this code:
````java
Class.forName("com.jw.client.JWDriver");
````
From JDBC 4.0 this is done automatically. This registers the driver with the DriverManager. This way, when a program creates a database connection with the `DriverManager.getConnection()` method, the DriverManager, in turn, calls the `Driver.connect()` method. Every JDBC driver must implement the java.sql.Driver interface. So, the JDBC driver's `connect()` method checks whether the driver URL is correct, and then, returns the Connection within its `connect()` method.
