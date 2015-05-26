#Submit queries and read results from the database including creating statements, returning result sets, iterating through the results, and properly closing result sets, statements, and connections

To process a SQL statement with JDBC you have to:

1. Establishing a connection.
2. Create a statement.
3. Execute the query.
4. Process the ResultSet object.
5. Close the connection.

In code, it looks like this:
````java
String sql = "SELECT id, name FROM users WHERE id = ?";
List<User> users = new ArrayList<>();
try (Connection con = DriverManager.getConnection("jdbc:mysql://localhost/test?user=admin&password=admin12345");
     PreparedStatement ps = con.prepareStatement(sql);) {
    ps.setInt(1, 1001);
    try (ResultSet rs = ps.executeQuery();) {
        while(rs.next()) {
            users.add(new User(rs.getInt("id"), rs.getString("name")));
        }
    }
} catch (SQLException e) {
    e.printStackTrace();
}
````

First, a connection with a MySQL database is established.

With a Connection object, you create a Statement object. There are three different kinds of statements:
* [Statement](https://docs.oracle.com/javase/8/docs/api/java/sql/Statement.html). Used to implement simple SQL statements with no parameters.
* [PreparedStatement](https://docs.oracle.com/javase/8/docs/api/java/sql/PreparedStatement.html). Used for precompiling SQL statements that might contain input parameters. It extends Statement.
* [CallableStatement](https://docs.oracle.com/javase/8/docs/api/java/sql/CallableStatement.html). Used to execute stored procedures that may contain both input and output parameters. It extends PreparedStatement.

To execute a query, call an execute method from Statement such as:
* `execute()`. Returns true if the first object that the query returns is a ResultSet object. Use this method if the query could return one or more ResultSet objects. Retrieve the ResultSet objects returned from the query by repeatedly calling Statement.getResultSet.
* `executeQuery()`. Returns one ResultSet object.
* `executeUpdate()`. Returns an integer representing the number of rows affected by the SQL statement. Use this method if you are using INSERT, DELETE, or UPDATE SQL statements.

With a ResultSet objecto, you can access the data. It acts like a cursor, pointing  to one row of data and positioned before the first row at the begginning. Then you call for example, the method `next()` to move the cursor forward by one rowand you can get the data with getter methods that either take the column index (the first column is 1) or the column name. There are getter methods for a lot of types, for example:
````java
int getInt(int columnIndex);
int getInt(String columnName);

long getLong(int columnIndex);
long getLong(String columnName);

String getString(int columnIndex);
String getString(String columnName);

BigDecimal getBigDecimal(int columnIndex);
BigDecimal getBigDecimal(String columnName);
````

When you are finished,, call the method `Statement.close()` to immediately release the resources it's using. When you call this method, its ResultSet objects are also closed. If you're not going to need the connection anymore, you should also close the connection with `Connection.close()`. You can use a try-with-resources statement to automatically close Connection, Statement, and ResultSet objects, regardless of whether an SQLException has been thrown. Or you can close them manually in the finally block like this:
````java
try {
  Connection con = ...
  Statement stmt = ...
  // Do something with stmt
} catch(Exception e) {
  e.printStackTrace();
} finally {
    if (stmt != null) { stmt.close(); }
    if (con != null) { con.close(); }
}
````
