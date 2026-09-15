<a id="2b0e37cc31de37b6"></a>

# 26. JDBC

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/2b0e37cc31de37b6)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 25. ODBC](25-odbc.md) · [Table of contents](../README.md) · [27. Embedded SQL →](27-embedded-sql.md)

<a id="0694f41d68754f94"></a>
## Overview of GOLDILOCKS JDBC Driver

<a id="5457d6c753b9fcbf"></a>
### Concepts of GOLDILOCKS JDBC Driver

GOLDILOCKS provides GOLDILOCKS JDBC driver (excluding some features) which complies with standard JDBC 4.0 based on TCP/IP connection. The user can use various transaction features and data query features by using GOLDILOCKS JDBC driver and connecting to GOLDILOCKS in Java program. GOLDILOCKS JDBC driver is written and built based on JDK 1.6. Therefore, it supports JDBC 4.0 features. The driver can be used by adding $GOLDILOCKS_HOME/lib/goldilocks6.jar file to the class path.

For a user who uses the lower versions of Java (JDK 1.4, JDK 1.5), goldilocks4 and goldilocks5.jar which are the implementation of JDBC 3.0 are also supported. The number after goldilocks refers to the JDK version. For more information, refer to [Supporting Versions](#073c654f95c9e375).

GOLDILOCKS JDBC complies with most of JDBC standard specifications, and it also supports non-standard API methods and classes to provide some unique features. For more information about non-standard methods, refer to each class API of [JDBC API References](#fbfef9bc90db5ce9) or [Using Other Data Types](#eb039cd34b72969b).

<a id="1e116aea23df0a14"></a>
### Characteristics

- **• Type-4 JDBC Driver:** 

GOLDILOCKS JDBC is a JDBC Type-4 type which is implemented only with pure Java. A user can use a JDBC driver only with jar file without any additional libraries. Also, it is faster and reliable than JDBC-ODBC Bridge type, and it has better portability than Type-2 using Native API.

- **• JDBC Standard Compliance:** 

GOLDILOCKS JDBC can recycle most of other existing JDBC programs without changing because it complies with the JDBC standard. The connection, various statements and ResultSet features can be used without modifying. However, the connection URL and property name, the name of driver class to be loaded should be changed to suit GOLDILOCKS. And the non-standard features and types are usable with the separate classes and methods API.

- **• Supporting Various Java Versions:** 

GOLDILOCKS JDBC driver supports four files such as goldilocks7.jar, goldilocks6.jar, goldilocks5.jar, goldilocks4.jar, so that a user can select and use the file appropriate for user's Java run-time environment. Because each jar file was built based on JDK 1.7, JDK 1.6, JDK 1.5, JDK 1.4, it complies with each JDBC 4.1, JDBC 4.0, JDBC 3.0, JDBC 3.0 specifications.

- **• Flexible Version Compatibility with the Server:** 

Refer to the protocol version for the compatibility with the server and the JDBC driver. If the protocol version of server is higher than that of the JDBC driver, it can be connected.

- **• API Support for Connection Pooling:** 

JDBC connection object is a resource which is expensive to generate. Therefore, the JDBC standard define a pooling system for it, and ConnectionPoolDataSource and PooledConnection are its interfaces. GOLDILOCKS JDBC implements these interfaces and provides the pooling facility in third party middleware products.

- **• Supporting XA API:** 

A user can perform the global transaction work by implementing XA interface which is the global transaction standard. And a user can perform the various XA features complying with a standard by using XAResource which is JDBC interface.

- **• GOLDILOCKS-specific Data Type:** 

GOLDILOCKS uses the data types which are not provided by the JDBC standard. For example, they are Interval related type, the type with time zone information such as Timestamp with time zone, etc. The driver provides a way to obtain or insert these types to DB.

- **• Server-based Powerful Cursor Scroll Feature:** 

Other JDBC drivers cache the row set in the driver for ResultSet scroll, so uses excessively memory of a client application program. For example, if the cursor is open by scroll insensitive and the rows are patched up to the last, all rows are cached in the driver, and the entire table resides in the client memory. It causes the out of memory error and the excessive use of client memory resource.

However, GOLDILOCKS supports the cursor scroll feature within the server, and clients may have lightweight, fast and reliable performance.

- **• Efficient Use of Resources:** 

Because GOLDILOCKS minimizes the memory which maintains the row information compared to other JDBC drivers and it does not use Java objects as possible. It can avoid the excessive garbage collection, and perform fast and reliable table scanning with less memory.

- **• Accurate and Extensive Metadata:** 

Because DatabaseMetaData interface of JDBC standard is faithfully and accurately implemented, it is easy to be linked with various DB tools. In addition, the usability is increased by retrieving DB meta information through various system views.

- **• Powerful Logging:** 

Various logging features are provided to monitor the usual JDBC API calls and network usage as well as the problem. If the logging-related features are specified in the connection URL, a user can leave a the content log to the console or files. Three types of logging exist, which are logging for JDBC method call recording, logging for protocol sending and receiving, logging for the SQL statement used.

- **• Connection Failover:** 

Connection failover is supported on JDBC driver level to continuously use an existing connection by automatically reconnecting to the previously registered alternate server when the connection with the execution GOLDILOCKS server fails or is disconnected. A user can use connection failover feature as an existing JDBC program without any exception handling in preparation for the broken connection.

- **• Connectivity between server and direct attach:** 

Other than TCP/IP based connection, it can be connected with direct attach method interworking with a process as same as the server. Like as ODBC connection supports direct attach method and Client/ Server method, GOLDILOCKS JDBC driver also provides both methods. JDBC program connected with direct attach does not communicate with TCP/IP, but it can use the server features in jvm by directly interworking with the server process. The perfomance is doubled or more than the JDBC program connected with TCP/ IP.

<a id="073c654f95c9e375"></a>
### Supporting Versions

<a id="b569b353563a80b3"></a>
#### GOLDILOCKS JDBC versions

GOLDILOCKS JDBC version information can be viewed when executing goldilocks6.jar file as follows.

```
shell>java -jar goldilocks6.jar

GOLDILOCKS JDBC Driver 1.0 Procotol-1.3.1, JDBC4.0 compiled with JDK1.6
```

The examples above describe that current GOLDILOCKS JDBC Driver version is 1.0, and the protocol version is 1.3.1, and JDBC standard version is 4.0 and it is built in JDK 1.6. The driver version is displayed apart from GOLDILOCKS product version, and it goes up whenever the function is strengthened. For more information about JDBC driver version, refer to [getDriverMajorVersion](#7e4553b6f98cebe5), [getDriverMinorVersion](#0e5b7adae127eced), [getDriverVersion](#cc7abfabf7d439fc) of DatabaseMetaData.

Protocol version determines compatibility with the server, and the driver can interwork with the server if the protocol version is equal to or lower than the server protocol version. The server supports all clients API of the lower protocol version.

goldilocks6.jar was built in JDK 1.6 which complies with JDBC 4.0 standard. Therefore, if the user's java environment is higher than JDK 1.6, goldilocks6.jar is used. However, if Java JDK 1.7 or higher is used, goldilocks6.jar can be used but API or classes of JDBC 5.0 can not be used.

goldilocks5.jar or goldilocks4.jar should be used if Java of JDK 1.5 or 1.4 environment is used. Both of them comply with JDBC 3.0 standard.

<a id="67b0e68f73cae943"></a>
### Examples

<a id="77d5aae7e631a9ec"></a>
#### Setting Class Path

CLASSPATH should be set to use GOLDILOCKS JDBC driver.

```
export CLASSPATH=.:$GOLDILOCKS_HOME/lib/goldilocks6.jar
```

Or, add a suitable jar file for the user's Java execution environment to the path.

<a id="120e2a0ce498c438"></a>
#### Loading Driver Class

The driver class can be loaded as follows.

```
Class.forName("sunje.goldilocks.jdbc.GoldilocksDriver");
```

The example above is the conventional method of using JDBC, and it is the method of dynamically loading the driver class and registering in DriverManager and getting the connection. Nowadays, the way to get the connection through DataSource is used more. For more information, refer to the corresponding class in [JDBC API References](#fbfef9bc90db5ce9).

<a id="da646fdd3b6c3149"></a>
#### Getting Connection

The following code is used to get the connection.

```
Connection con = DriverManager.getConnection(
    "jdbc:goldilocks://127.0.0.1:22581/test", "TEST", "test");
```

The connection URL should be started with "jdbc:goldilocks:" to use GOLDILOCKS JDBC. The next is the IP address and port number of the server and "/test" which is the final part of URL is the DB name. The current GOLDILOCKS does not specifically check the DB name because it does not support multi DB. A user connected URL may be obtained again through DatabaseMetaData.getURL().

It connects in Direct Attach (D/A) mode when setting IP to 0.0.0.0, and a port to 0. Or, the connecting protocol, *da*, can be used instead of ip:port. In other words, both of the following two URL enables connecting in D/A mode.

```
"jdbc:goldilocks://0.0.0.0:0/test"
"jdbc:goldilocks:da/test"
```

Username and password should respectively use the account and password for DB.

<a id="520ebeaa2f8dab8d"></a>
#### Using Statement and ResultSet

Statement and ResultSet are used in the same way as other JDBC programs.

```
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT NAME, ADDRESS FROM EMP");
while (rs.next())
{
    System.out.println("name = " + rs.getString(1));
    System.out.println("address = " + rs.getString(2));
}
rs.close();
stmt.close();
```

<a id="bb4910bcac6fcb73"></a>
## Feature Specification

<a id="ccb513891b9a0c3e"></a>
### Connection

<a id="de1209185463f2cf"></a>
#### Connection Using DriverManager

The traditional way to get a connection is to use DriverManager.

```
Connection con = DriverManager.getConnection(url_string, user_name, password);
```

url_string has the following three types.

```
jdbc:goldilocks://[ip address]:[port_no]/[db_name]
```

```
jdbc:goldilocks:da/[db_name]
```

```
jdbc:goldilocks:locator//[ip address]:[port_no][, [ip address]:[port_no] ]*/[db_name]
```

Both of IPv4, IPv6 are available for IP address, and port_no refers to the port number set. db_name is not used for the current connection so it can have any name. However, it can not be omitted. The following is an example of URL.

```
String url_string = "jdbc:goldilocks://127.0.0.1:22581/test";
```

IP "0.0.0.0" and port 0 are used as a special address for D/A connection. For more information about D/A mode, refer to [Direct Attach Mode Connection](#100f752d5a6283ae).

user_name and password refer to GOLDILOCKS account.

The following method is used for various property settings except for the getConnection() method above.

```
Properties prop = new Properties();
prop.setProperty("user", user_name);
prop.setProperty("password", password);
Connection con = DriverManager.getConnection(url_string, prop);
```

A locator keyword can be added to  url_string to obtain the server connection information from glocator instead of using the connection property. In this case, ip address and port_no is considered as the connection information of glocator.   
The following is an example of using the locator keyword to the connection statement.

```
String url_string = "jdbc:goldilocks:locator//127.0.0.1:42581,127.0.0.1:42582/test?locator_service=S1";
```

The first connection information (127.0.0.1:42581) is the connection information of glocator, and the latter connection information is processed as ALTERNATE_LOCATORS property such as 127.0.0.1:42582.

The following is the property setting which has the meaning as same as the url_string above.

```
String url_strng = "jdbc:goldilocks://0.0.0.0:0/test";
Properties prop = new Properties();
prop.setProperty("locator_host", "127.0.0.1");
prop.setProperty("locator_port", "42581");
prop.setProperty("alternate_locators", "127.0.0.1:42582");
prop.setProperty("locator_service", "S1");
Connection con = DriverManager.getConnection(url_string, prop);
```

The property list which can be used for the connection is known through getPropertyInfo() method of GoldilocksDriver. For more information, refer to [Connection property](#8a0535fad0cd8b1a).

The login timeout of the connection object which is created by DriverManager and the logger uses the value registered in DriverManager. The logger is used by all JDBC interfaces generated from the connection object. Each connection object is not allowed to have an individual logger.

<a id="fef942fab85f88b0"></a>
#### Connection Using DataSource

The JDBC standard recommends to use DataSource rather than the previous DriverManager. It is because DataSource is a single interface to access any data source, and it can individually set the values related to the various data sources, and may remotely send a DataSource object literally.

A connection object can be obtained through DataSource as follows.

```
import sunje.goldilocks.jdbc.GoldilocksDataSource;

GoldilocksDataSource ds = new GoldilocksDataSource();
ds.setServerName("127.0.0.1");
ds.setPortNumber(22581);
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
Connection con = ds.getConnection();
```

GoldilocksDataSource classes should be used to create a DataSource object.  

Then, various connection information should use setter method which is not DataSource standard API.For more information, refer to [DataSource](#87a203b40470f35b).

When using DriverManager, the login timeout and the logger should be globally set. However, when using DataSource, the login timeout and the logger can be individually set.

```
ds.setLoginTimeout(10);
ds.setLogWriter(out);
```

<a id="a85c5c0ed7f642d9"></a>
#### Interworking with Middleware

It is necessary to know the name of the class which implements XADataSource, ConnectionPoolDataSource interface to interwork with middleware such as Weblogic, JBoss, etc. GOLDILOCKS provides GoldilocksXADataSource, GoldilocksConnectionPoolDataSource for sunje.goldilocks.jdbc package. Both classes offer the various setter methods such as GoldilocksDataSource.

```
import sunje.goldilocks.jdbc.GoldilocksXADataSource;

GoldilocksXADataSource ds = new GoldilocksXADataSource();
ds.setServerName("127.0.0.1");
ds.setPortNumber(22581);
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
XAConnection con = ds.getXAConnection();
```

<a id="0342fbea344af6ed"></a>
#### Connection Property

**Connection property**

<a id="8a0535fad0cd8b1a"></a>
| Name | Mandatory/ optional | Valid value | Description |
| --- | --- | --- | --- |
| alternate_servers | Optional | IP:PORT[,IP:PORT]+ | It is the list of alternate servers for failover. It is delimited by comma (,). |
| batch_count | Optional | Any integer | It is the number of the batch jobs which can be processed in a single protocol transmission and reception. The default value is 1,000. If the value is too small, too much frequent network communication causes poor performance of the batch processing. If the value is too large, the server memory is increased because the session stacks the execution results. |
| connection_retry_count | Optional | Any integer | It stores the number of retrials to connect. The default value is 0, then it does not retry to connect. |
| connection_retry_delay | Optional | Any integer | It stores the delay before the connection retrial in seconds when trying to connect again. The default value is 3. |
| date_format | Optional | Any string | It is the character format which is used to interconvert between date and string inside the driver. |
| da_buffer_size | Optional | Any integer | It sets the size of a buffer which sends and receives data when fetching and binding while connected in direct attach mode. The default value is 100000. |
| decoding_replacement | Optional | Any string | It is the character replacing a byte value which can not be decoded when decoding a byte array into a string. The default value is ?. |
| failover_granularity | Optional | {"0", "1", "2"} | It determines whether failover is successful. non-atomic(0), atomic(1), 2 are not yet supported. When an error occurs for the existing prepared statements in the prepare process during failover, if it is 0, then it proceeds the failover, and if it is 1, it determines that the failover fails. The default value is 0. |
| failover_type | Optional | {"connection", "session"} | It determines the failover types.  * Connection: Failover is used only when connecting to server.  * Session: Failover is used when connecting to server as well as communicating with the server like execution.  The default value is session. |
| format_grammar | Optional | {"db", "java"} | It determines whether the property string such as date_format is the GOLDILOCKS syntax or the syntax used in SimpleDateFormat of java. The default value is db. |
| global_logger | Optional | {"console"} | It specifies the logging target.  Currently only console is available. Only the first specified one is valid. |
| home_dir | Optional | Any string | It specifies a home directory of a cluster server. The default value is null. |
| keep_alive | Optional | {"on", any} | It determines whether to set the keep_alive as the socket property of the connection. Using the property, the connection remains by periodically sending and receiving ack inside TCP socket. LAN cable error detection can forcibly cut off the connection. |
| locator_connection_timeout | Optional | Any integer | It is the time of waiting for receiving a packet from glocator. |
| locator_file | Optional | Any string | It is a location file. |
| locator_host | Optional | IP address | It is host address of glocator. |
| locator_port | Optional | Port no | It is port of glocator. |
| locator_service | Optional | Any string | It is the service name to obtain the server connection information. |
| lzeros | Optional | Any integer | When a numeric is expressed as a string and the number of zeros following the decimal point exceeds this value, it is expressed in exponent notation. The default value is 15. |
| new_password | Optional | Any string | It can change the account password by using old_password property together. |
| old_password | Optional | Any string | It can change the account password by using new_password property together. |
| packet_compression_threshold | Optional | Any integer | It compresses the communication data to be sent to the server when the data size is bigger than packet_compression_threshold. The property range is 32 ~ 2113929216. |
| password | Mandatory | Any string | It is user account password. |
| program | Optional | Any string | It is program description. |
| protocol_log | Optional | {"on", any} | It determines whether to log sending and receiving a protocol. The default value is "" (not). |
| query_log | Optional | {"on", any} | It determines whether to log a query.  The default value is "" (not). |
| role | Optional | {"", "SYSDBA", "ADMIN"} | It specifies the account role. The default value is "". |
| session_type | Optional | {"1", "2", "3"} or {"dedicate", "shared", "default"} | It is one of dedicated/ shared/ default. (It is selected by DB when it is set to default.) |
| time_format | Optional | Any string | It is the character format which is used to interconvert between time and string inside the driver. |
| timestamp_format | Optional | Any string | It is the character format which is used to interconvert between timestamp and string inside the driver. |
| timetz_format | Optional | Any string | It is the character format which is used to interconvert between time with timezone and string inside the driver. |
| timestamptz_format | Optional | Any string | It is the character format which is used to interconvert between timestamp with timezone and string inside the driver. |
| trace_log | Optional | {"on", any} | It determines whether to log the trace. The default value is "" (not). |
| tzeros | Optional | Any integer | When a numeric is expressed as a string and the number of zeros in digit goes beyond this value, it is expressed in exponent notation. The default value is 15. |
| user | Mandatory | Any string | It is user account name. |
| use_targettype | Optional | {"0", "1", "2"} | It is the information which is to be received together when receiving a column type through communication. * 0: none * 1: name * 2: all |


> 
> - locator_file is applied prior to locator_host and locator_port. For more information about locator_file, refer to [Location File](../part-06-utility-manual/42-gloctl.md#533f3f1f47ce5bf5).
> - locator_service property enables the access to the server belonging to locator_service. For more information, refer to [glocator](../part-06-utility-manual/40-glocator.md#806ed1d0a43526e5) and [gloctl](../part-06-utility-manual/42-gloctl.md#58c6a5230940f6f1).
> 

<a id="b5733fe1c4072232"></a>
### Data Manipulation

<a id="5d3b44c9142bdc44"></a>
#### Data Manipulation Using Statement

Various SQL statements can be executed by using statement objects. Statement object can be obtained from the connection object as follows.

```
Connection con = DriverManager.getConnection(...);
Statement stmt = con.createStatement();
```

Various DML or DDL statements can be executed by using the execute method of the created statement object, and the executeUpdate method.

```
stmt.executeUpdate("create table emp ( id varchar(20), name varchar(30), age integer )");
stmt.executeUpdate("insert into emp values ('1234560000', 'Yuna', 24)");
int updated = stmt.executeUpdate("delete from emp where age > " + age);
```

The difference between execute and executeUpdate methods is only the return values. The execute method indicates whether the executed SQL statement returns ResultSet. The executeUpdate method returns the number of updated rows. The execute method can be used for both of DML and SELECT statements, but it throws SQLException if the executeUpdate method is used for SELECT statement.

> Direct-execution refers to execution of SQL statement by using statement. It is the method of performing the prepare operation(parsing, validation, optimization) and execution for the SQL statement at a time. On the other hand, prepare-execution refers to the method of preparing the operation, then repeating the execution. Direct-execution repeatedly performs prepare and execution operation every time it is performed, so prepare-execution is more efficient when repeatedly performing the SQL statement.

<a id="18c80b6d8b888e8b"></a>
#### Data Manipulation Using PreparedStatement

The JDBC standard provides PreparedStatement interface which can use a parameter for data manipulation, and it enables a user to run it more efficiently. In addition, PreparedStatement quickly perform the repeated operation of the SQL statement because performs the prepare operation for the SQL statement only once.

```
Connection con = DriverManager.getConnection(...);
PreparedStatement pstmt = con.prepareStatement(
  "insert into emp values (?, ?, ?)");
pstmt.setString(1, "55544123000");
pstmt.setString(2, "Gildong");
pstmt.setInt(3, 32);
pstmt.executeUpdate();
pstmt.setString(1, "1357924680");
pstmt.setString(2, "Dooli");
pstmt.setInt(3, 41);
pstmt.executeUpdate();
```

After preparing the SQL statement as shown in the lines 2-3, the data is bound and performed. PreparedStatement which is prepared once, can bind and execute repeatedly.

If the binding is omitted and execute() is performed, the previously bound values are used.

```
pstmt.setString(1, "333555777000");
pstmt.setString(2, "Kang");
pstmt.setInt(3, 55);
pstmt.executeUpdate();
pstmt.setString(1, "245778884440");
pstmt.executeUpdate();
```

When the value is not bound to the second, third parameters as shown in line 6 but immediately executed, the value, "Kang" and 55, which was previously bound, is used. If the previously bound value does not exist, it throws SQLException.

All bound values are deleted by using clearParameters().

```
pstmt.setString(1, "333555777000");
pstmt.setString(2, "Kang");
pstmt.setInt(3, 55);
pstmt.executeUpdate();
pstmt.clearParameters();
pstmt.setString(1, "245778884440");
pstmt.executeUpdate();
```

After deleting parameters in line 5, if the value is bound only to the first parameter and executed (line 7), then it throws SQLException.

The main reason to use PreparedStatement is because it can bind the data of various types. It is inconvenient to handle the data of the type such as binary or timestamp because the value can be expressed only in the character string when using Statement. Therefore, it is more convenient to bind all types by using PreparedStatement.

```
pstmt.setTimestamp(1,
  new Timestamp(Calendar.getInstance().getTimeInMillis()));
pstmt.setCharacterStream(2, new StringReader(BIG_STRING));
pstmt.setObject(3, someObj, Types.LONGVARCHAR);
pstmt.setObject(4, otherObj);
```

In the sample above, lines 1 ~ 2 binds java.sql.Timestamp object. The binding type (It is GOLDILOCKS type of the data when the data is sent to the server) is TIMESTAMP. For more information about the binding type which is determined by the various setter methods, refer to the corresponding API of [PreparedStatement](#5c8b89a602285a79).

Line 3 binds a reader object, and it is bound as LONG VARCHAR type internally.

Line 4 binds the object of Java object type, and explicitly notifies that the type is LONG VARCHAR. For more information about GOLDILOCKS type which is mapped to the type of Types, refer to [SQL types → GOLDILOCKS types](#cb02001a30776570).

Line 5 literally binds the Java object type, and it is bound to the corresponding GOLDILOCKS data type according to the class type. For more information about mapping between class types and GOLDILOCKS data types, refer to [Java objects -> GOLDILOCKS types](#28bad6cc9ea16d01).

<a id="1026dfe05e98a9ce"></a>
#### Batch Execution Using Statement

The different SQL statements can be executed as the batch job by using addBatch() and executeBatch() of Statement.

```
stmt.addBatch("insert into emp values ("12345", "Jake", 22)");
stmt.addBatch("insert into salary values ("12345", 5000)");
stmt.addBatch("update members set total_count=total_count+1 where age=22");
stmt.executeBatch();
```

Likewise, different SQL statements may be performed through a single executeBatch () method. However, this does not mean that the method call executes three statements in the server, gathers the results, sends the results to the JDBC driver with a single protocol. Internally, three times of protocol transmission, execution in the server and result transmission are performed. In other words, it does not have a big performance advantage.

After performing executeBatch, all registered jobs are deleted.

Even if an error occurs during execution, all registered jobs are performed until it is completed. Whether an error occurs or not can be known by the value of the returned int [] type. In other words, if int [] has EXECUTE_FAILED value, it means that the job is failed.

<a id="b70f98e799b50bcb"></a>
#### Batch Execution Using PreparedStatement

More powerful batch operation can be performed by using addBatch() and executeBatch() methods of PreparedStatement.

```
PreparedStatement pstmt = con.prepareStatement("insert into emp values (?, ?, ?)");
pstmt.setString(1, "12345000");
pstmt.setString(2, "John");
pstmt.setInt(3, 33);
pstmt.addBatch();

pstmt.setString(1, "222333555");
pstmt.setString(2, "Henry");
pstmt.setInt(3, 24);
pstmt.addBatch();
int[] inserted = pstmt.executeBatch();
```

The example above is a process of inserting two rows. The values configuring the two rows are bound through addBatch (), and then if executeBatch () is called, the bound value and the protocol for execution are sent to the server and executed. It is more efficient than the batch execution of Statement and the performance is faster because communication occurs only when executeBatch() is called.

The new value should be bound to execute executeBatch() again because the bound values are deleted after executing executeBatch(). clearBatch() does not be to be explicitly called to delete the registered job after execution.

Even if an error occurs during execution, all registered jobs are performed until it is completed. Whether an error occurs or not can be known by the value of the returned int [] type. In other words, if int [] has EXECUTE_FAILED value, it means that the job is failed.

GOLDILOCKS JDBC provides a separate method which is executeBatchAtomic() in addition to executeBatch(). executeBatch () performs the execution as many as the number of the registered jobs in the server, but the response time is fast because executeBatchAtomic() performs the execution at once with the registered job (the bound values). However, if any one fails, everything fails as it can be seen from the name which is atomic. Therefore, the return type is not int[], but int.

```
...
int inserted = ((GoldilocksPreparedStatement)pstmt).executeBatchAtomic();
```

<a id="5b1793d4c396b3da"></a>
### Data Retrieval

<a id="8780b49fe810d49d"></a>
#### Getting Column Values

The data can be retrieved through ResultSet object which is obtained by executeQuery () of the Statement or PreparedStatement.

```
...
ResultSet rs = pstmt.executeQuery();
while(rs.next())
{
    String id = rs.getString(1);
    String name = rs.getString(2);
    int age = rs.getInt(3);
    ...
}
```

The contents of the column can be obtained through various getter methods in the ResultSet after retrieving the data in the table. The data in the table is sent to JDBC drivers in the original form of GOLDILOCKS data type, and it is converted to an appropriate Java data type according to the types of getter methods called by a user and it is transmitted to the user. For more information about type conversion mapping of GOLDILOCKS data type and getter method, refer to [Whether supporting getter method for GOLDILOCKS type - 1 ](#fa62c08a45390115).

If GOLDILOCKS data type can not be converted to the type of getter, it throws SQLException.

<a id="369b1fc1ec54f019"></a>
#### Closing ResultSet

The ResultSet which is used up can release the resources through close(). Even if a user does not explicitly call close(), the followings bring the result as same as when calling close() of ResultSet.

- When superordinate statement is closed
- When superordinate connection is closed
- When executeQuery() of Statement is called again
- When an error occurs during fetching

The two ResultSets which are created from a single statement can not be remained simultaneously in the third case above. Only the ResultSet object which is created by the last executeQuery() is valid.

<a id="4e623b52d20bac84"></a>
#### Fetch Size

JDBC can specify the number of rows fetched at once from the server through setFetchSize(int rows) of Statement. The default value of the ResultSet property of GOLDILOCKS is 0. 0 automatically determines the number of rows fetched by the server. For forward only, it is the maximum number of rows fetched in a communication packet. For scrollable, it is fixed to 100. If the value is too large, the amount of memory used by JDBC ResultSet becomes large. If the value is too small, the communication is frequently executed.

The value is mainly used in a scrollable ResultSet because it is not sensitive even when it is scroll sensitive while moving within the row cache of ResultSet. If the value is set too large, the latest information about the changes of rows can not be known.

<a id="8a9ba81cc3e3fa73"></a>
#### Field Size Limit

JDBC may limit the maximum length of the column through setMaxFieldSize(int size) of statement. The maximum length can be limited for the types of CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, and LONG VARBINARY. The data bigger than the length is truncated. The default value is 0, and the maximum length is not limited in this case.

This property is ignored for other types such as INTEGER, DATE, etc..

<a id="5bcd2720037f626a"></a>
### ResultSet Scroll

<a id="aff298c28a388a39"></a>
#### Getting Scrollable ResultSet

There are two kinds of scrollable ResultSet, which are scroll sensitive and scroll insensitive. Scroll sensitive is the cursor type which can view the values changed by the transaction itself or other transaction while traversing the ResultSet, but scroll insensitive is not. GOLDILOCKS server supports both of the scroll types, and those facilities can be used by JDBC.

```
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,
                                     ResultSet.CONCUR_READ_ONLY);
ResultSet rs = stmt.executeQuery("select id, name, age from emp");
```

If the ResultSet type is TYPE_SCROLL_INSENSITIVE when creating statement as line 1, ResultSet which is created from the statement object is scroll sensitive cursor. However, the current GOLDILOCKS does not support the updatable ResultSet.

The type should be set to TYPE_SCROLL_INSENSITIVE to obtain scroll insensitive ResultSet. The default value is TYPE_FORWARD_ONLY.

However, even it is a scroll sensitive ResultSet, a user can not know the latest value or whether it is changed, when moving within the row cache of ResultSet. The row should be fetched again from the server to find out the latest value or whether it is changed.

<a id="dc899a3a8f660a56"></a>
#### Scrolling

JDBC API provides the following methods to scroll the cursor.

```
public boolean next() throws SQLException;
public boolean previous() throws SQLException;
public boolean first() throws SQLException;
public boolean last() throws SQLException;
public boolean absolute(int rows) throws SQLException;
public boolean relative(int rows) throws SQLException;
public void beforeFirst() throws SQLException;
public void afterLast() throws SQLException;
```

next() is the method which can be used for forward only or scrollable ResultSet, and it sets the cursor position to the next row. If the row can be read at the moved position, it is true. Otherwise, it is false. Other methods can be used only for scrollable ResultSet.

previous() moves the cursor to the previous row, first() moves the cursor to the first row, last() moves the cursor to the last row, absolute() moves the cursor to the absolute position and relative() moves the cursor to the relative position from the current position. beforeFirst() moves the cursor to before the first row. afterLast()moves the cursor to after the last row.

```
rs.afterLast();
while (rs.previous())
{
    String id = rs.getString(1);
    String name = rs.getString(2);
    int age = rs.getInt(3);
    ...
}
```

The code above will query backwards from the last row to the first row.

The current cursor position can be known by the following method.

```
public int getRow() throws SQLException;
```

<a id="2f40e3ee2d8c5803"></a>
#### Scrolling Principle

The ResultSet scroll is easy to use, but it may cause poor performance without knowing internal operating principles. Scrolling is performed in result cache within ResultSet of JDBC driver, but it is performed on the server in case when the range exceeds the cache, so the communication may occur. Therefore, it should be used carefully to prevent the poor performance.

The internal default value of the fetch size of scrollable ResultSet is 100 (the external default value is 0 and it can be changed through setFetchSize() method). It means that the number of rows that are fetched to JDBC driver at once are 100. The row cache of ResultSet consists of 100 rows, and the cursor position of ResultSet should be changed if the row position to be moved is in the cache. However, if it is not in the cache, the row at the position where to be moved should be got from the server. At this time, it is necessary to know how to get the row set including the row to be moved.

For example, if the ResultSet has rows from 1 to 100 and the current cursor position is at 100, calling next () will fetch rows 101 through 200 from the server because the next row does not exist in the cache. On the other hand, the rows from 101 to 200 are in ResultSet cache, and it is not appropriate to fetch rows from 100 to 199 from the server by calling previous() if the current cursor position is 101 row. When this approach is used, row should be fetched from the server whenever previous() is called. However, GOLDILOCKS fetches the rowset which includes the corresponding last row from the server when it is required to fetch the row from the server due to calling previous () to prevent this inefficiency. For example, when it is necessary to fetch row of the number 100 by calling previous(), GOLDILOCKS fetches the rows from 1 to 100. Then it is fetched in favor of previous ().

The rule is generalized as follows.

- If the position to be moved is after the current position, 100 rows (the fetch size) after that position are fetched. 
- If the position to be moved is before the current position, 100 rows before that position are fetched.
- When moved with first(), the first 100 rows are fetched. 
- When moved with last(), the last 100 rows are fetched.

When moved backward, the fetch is performed in favor of next(). When moved forward, the fetch is performed in favor of previous(). This is also applied to absolute () and relative ().

<a id="eb039cd34b72969b"></a>
### Using Other Data Types

<a id="af0516c215b02a61"></a>
#### Interval Type

GOLDILOCKS supports the following 13 types related to interval.

- interval year
- interval month
- interval year to month
- interval day
- interval hour
- interval minute
- interval second
- interval minute to second
- interval hour to minute
- interval hour to second
- interval day to hour
- interval day to minute
- interval day to second

sunje.goldilocks.jdbc.GoldilocksInterval object is created and the insert operation is executed by setObject() of PreparedStatement to insert the interval data into a table using JDBC.

GoldilocksInterval object can be created by using createIntervalXXX which is the static method of GoldilocksInterval.

```
import sunje.goldilocks.jdbc.GoldilocksInterval;

...
GoldilocksInterval interval = GoldilocksInterval.createIntervalDayToSecond(2, 6, "2 08:23:54.560843");
PreparedStatement pstmt = con.prepareStatement("insert into interval_table values (?,?)");
pstmt.setString(1, someId);
pstmt.setObject(2, interval);
pstmt.executeUpdate();
```

For more information about createIntervalXXX method, refer to [GoldilocksInterval](#17d473bca9c2891a). Likewise, GoldilocksInterval is created and it is bound via setObject. Or, a type is explicitly specified as follows.

```
import sunje.goldilocks.jdbc.GoldilocksTypes;
...
pstmt.setObject(2, interval, GoldilocksTypes.INTERVAL_DAY_TO_SECOND);
```

The data may be inserted by using a character string without GoldilocksInterval object.

```
pstmt.setObject(2, "2 08:23:54.560843", GoldilocksTypes.INTERVAL_DAY_TO_SECOND);
```

In this case, a GoldilocksInterval object is created within JDBC driver and bound to a host variable. Or it may be bound as a string by using setString() method.

```
pstmt.setString(2, "2 08:23:54.560843");
```

The string is literally sent to the server when using this method, and the string is converted to Interval day to second type and inserted in the server.

getObject() or getString() of ResultSet queries the Interval type from the DB.

```
import sunje.goldilocks.jdbc.GoldilocksInterval;

ResultSet rs = stmt.executeQuery("select interval_value from some_table");
while (rs.next())
{
    GoldilocksInterval interval = (GoldilocksInterval)rs.getObject(1);
    System.out.println("type = " + interval.getTypeName() + 
                       ", value = " + interval.toString());
}
```

The data of GoldilocksInterval type can be retrieved via getObject() of ResultSet. GoldilocksInterval class provides getter like getYear(), getHour(), etc. that return various time data. For more information about getter API, refer to [GoldilocksInterval](#17d473bca9c2891a).

<a id="610e68f0d9ce58b6"></a>
#### Time with Time Zone and Timestamp with Time Zone Types

Concerning time, GOLDILOCKS provides not only SQL standard types such as Date, Time, Timestamp but also Time with time zone and Timestamp with time zone types.

```
CREATE TABLE SAMPLE_TABLE ( C1 TIME WITH TIME ZONE,
                            C2 TIMESTAMP WITH TIME ZONE );
```

GOLDILOCKS JDBC provides setTimeTimeZone(int colIndex, Time time, Calendar timezone) method and setTimestampTimeZone(int colIndex, Timestamp time, Calendar timezone) method in GoldilocksPreparedStatement class to insert the data of Time with time zone and Timestamp with time zone types. For more information about specifications refer to [setTimeTimeZone](#3a06db3c0697d934) and [setTimestampTimeZone](#09a2c8b2b2ef5867).

The data can be inserted via existing setTime() and setTimestamp() methods, but the time zone value of the column is unconditionally set to the local time zone of Java execution environment. Therefore, setTimeTimeZone() or setTimestampTimeZone should be used to insert various time zone information.

Time, Timestamp data can be inserted with the given time zone value via setTimeTimeZone and setTimestampTimeZone.

```
import sunje.goldilocks.jdbc.GoldilocksPreparedStatement;

PreparedStatement pstmt = con.prepareStatement(
    "INSERT INTO SAMPLE_TABLE VALUES (?,?,?,?)");
Calendar now = Calendar.getInstance();
Calendar usNow = Calendar.getInstance(TimeZone.getTimeZone("GMT-8"));

Time t = new Time(now.getTimeInMillis());
Timestamp ts = new Timestamp(now.getTimeInMillis());

pstmt.setTime(1, t);
pstmt.setTimestamp(2, ts);
pstmt.executeUpdate();

((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, t, now);
((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(2, ts, now);
pstmt.executeUpdate();

((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, t, usNow);
((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(2, ts, usNow);
pstmt.executeUpdate();
```

Line 11, 12 binds the column to time type and timestamp type. Each value of t and ts is sent to the server and the default time zone value is inserted to DB column in the server.

On the other hand, line 15, 16 binds the column to time with time zone type and timestamp with time zone type, and is sent to the server together with time zone information. As a result, if the time zone settings of a server and a client are same, the rows which are inserted by lines 11~13 and 15~17 are same.

Line 19, 20 inserts time zone information of GMT-8 time zone.

There are two ways to query data, which are time with time zone and timestamp with time zone. One is the way to get data as char from the server, and the other is the way to get data of the corresponding type by JDBC and to obtain as time or as timestamp object.

```
ResultSet rs = stmt.executeQuery("select c1, cast(c1 as char(33)), c2, cast(c2 as char(33)) from sample_table");
while (rs.next())
{
    System.out.println("c1 = " + rs.getTime(1).toString());
    System.out.println("c1 as char = " + rs.getString(2));

    System.out.println("c2 = " + rs.getTimestamp(3).toString());
    System.out.println("c2 as char = " + rs.getString(4));
}
```

When executing the code above, the results are as follows.

```
c1 = 12:35:26
c1 as char = 12:35:26.052000 +09:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-27 12:35:26.052000 +09:00
c1 = 12:35:26
c1 as char = 12:35:26.052000 +09:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-27 12:35:26.052000 +09:00
c1 = 12:35:26
c1 as char = 19:35:26.052000 -08:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-26 19:35:26.052000 -08:00
```

<a id="3e28fb7c42dbecab"></a>
### Logging

<a id="02d275a1fdd8307c"></a>
#### Logging Types

When developing a project by using JDBC, it is helpful in many ways for JDBC driver to leave various logs. GOLDILOCKS provides the facility to log the useful information even during operation, as well as the project development.   
There are three types of log, which are trace log, protocol log and query log.

Trace log leaves information every time when JDBC API is called. It can be known which JDBC API is called. Protocol log shows the situation to send and receive communication packets between JDBC driver and GOLDILOCKS server. Query log records the SQL statement to be executed, when PreparedStatement or Statement is executed.

<a id="6cca652488f61d36"></a>
#### Logging by Using DriverManager

First, the logging is left by using DriverManager. The logging media can be determined by using setLogWriter() method in DriverManager, and the type of logging to be left can be specified in connection url.

```
DriverManager.setLogWriter(new PrintWriter(System.out));
String url = "jdbc:goldilocks://localhost:22581/test?trace_log=on&query_log=on";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

Line 1 defines the logging media. All logging is output to the console. Line 2 defines the connection url, and the property can be defined after ? character. It means to using trace_log, query_log.

Likewise, these properties can be specified in URL, or they can be defined with properties object.

```
Properties prop = new Properties();
prop.put("trace_log", "on");
prop.put("query_log", "on");
prop.put("protocol_log", "on");
prop.put("user", "TEST");
prop.put("password", test");
Connection con = DriverManager.getConnection(url, prop);
```

The connection properties which can be used in GOLDILOCKS are defined in [Connection property](#8a0535fad0cd8b1a).

Sometimes it is difficult to call setLogWriter() of DriverManager. When using the middleware, the code like that can not be added. For such a case, GOLDILOCKS JDBC provides a global property called global_logger. Other general properties are limited to a single connection, but this property is global. In other words, if the property is set, it does not have to call DriverManager.setLogWriter ().

```
String url = "jdbc:goldilocks://localhost:22581/test?" +            
             "global_logger=console&trace_log=on&query_log=on";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

global_logger property is applied only once initially, and it is ignored if log writer is already set in DriverManager. Only the current console is applicable as the property value. Other value does not cause any operation.

<a id="9bdb3de4f3c94117"></a>
#### Logging by Using DataSource

Unlike DriverManager, DataSource can set the log writer by each object. If the log writer is set for a DataSource object, all connections which are generated from the DataSource are logged by the log writer. The following describes how to set the logging in the DataSource.

```
import sunje.goldilocks.jdbc.GoldilocksDataSource;
...
GoldilocksDataSource ds = new sunje.goldilocks.jdbc.GoldilocksDataSource();
ds.setServerName("localhost");
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
ds.setPortNumber(22581);
ds.setLogTarget("console");
ds.setTraceLog("on");
ds.setQueryLog("on");
ds.setProtocolLog("on");
Connection con = ds.getConnection();
```

Likewise, the logging feature is set by using setLogTarget(), setTraceLog(), setQueryLog() and setProtocolLog() methods. setLogWriter() of DataSource can be called instead of setLogTarget(). When using the middleware, the method such as setLogWriter() can not be directly called, so it should be controlled with the property. In this case, if logTarget, traceLog, queryLog and protocolLog properties are defined, the middleware automatically calls the methods.

<a id="f6c886676bd9a407"></a>
### Viewing Plan Text

<a id="fc169e2ddf75bdc1"></a>
#### Usage

The plan text can be obtained by using GOLDILOCKS JDBC like as the plan text of the executed statement is obtained by using GOLDILOCKS ODBC. It can be configured to generate a plan text by using non-standard API method in GoldilocksStatement class, or obtain the plan text which is already generated.

```
Connection con = ...
GoldilocksStatement stmt = (GoldilocksStatement)con.createStatement();
stmt.setExplainPlanOption(GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON);
ResultSet rs = stmt.executeQuery("select * from t1");
System.out.println(stmt.getExplainPlan());
```

For example, when querying a simple table, the plan text is output as follows.

```
< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                |            |
|    1  |    TABLE ACCESS ("T1")                           |          0 |
==========================================================================
     1  -  READ COLUMNS : A
```

<a id="20e79f498b71923f"></a>
#### Option Types

GOLDILOCKS provides the following four properties about the plan text generation.

- EXPLAIN_PLAN_OPTION_OFF: It does not generate the plan text as the default value of the property related to the plan text of statement.
- EXPLAIN_PLAN_OPTION_ON: It generates the plan text when executing or fetching. 
- EXPLAIN_PLAN_OPTION_ON_VERBOSE: It generates more detailed plan text such as execution time when executing or fetching. 
- EXPLAIN_PLAN_OPTION_ONLY: It generates the plan text like as EXPLAIN_PLAN_OPTION_ON when executing or fetching but it is not actually executed.

These properties are set by using GoldilocksStatement.setExplainPlanOption(int) method, and the property which is set once is continuously maintained. A constant value of the property is defined in GoldilocksStatement.

> The plan text for non-SELECT DML statements or other SQL statements is generated at run-time, but the plan text for the SELECT statements is generated when the SELECT statement is fetched and the cursor is positioned at the end in the server. The plan text should be obtained after all rows are traversed with ResultSet for the SELECT statement. The plan text can be obtained when there are few rows in a table because the cursor can traverse until the end in the server without fetching all rows.

<a id="a3abfd326fee706d"></a>
### Connection Failover

GOLDILOCKS supports the connection failover of the client level (JDBC, ODBC). The application which accesses with client/ server mode by using the JDBC or ODBC to GOLDILOCKS, may perform connection to the alternative server automatically when the connection fails or disconnected. This allows a user to use high availability applications which utilize multiple servers. In particular, when a user registers the main server URL and the alternative server URL through the connection property under interworking web server environment, it can safely use the connection object obtained from the connection pool without worrying about the interruption. Failover is performed entirely automatically inside the driver and the user does not need to worry about the reconnection logics.

alternate_servers property should be given to use failover. IP and port of the alternative server are given for this property, and it may indicate the multiple alternative servers by using the comma (,).

```
Class.forName("sunje.goldilocks.jdbc.GoldilocksDriver");

String url = "jdbc:goldilocks://192.168.0.101:22581/test";
Property prop = new Properties();
prop.setProperty("user", "TEST");
prop.setProperty("password", "test");
prop.setProperty("alternate_servers", "192.168.0.201:22581");
Connection con = DriverManager.getConnection(url, prop);  ❶
Statement stmt = con.createStatement();
stmt.executeUpdate("insert into time_tab values (sysdate)");  ❷
...
```

For example, if 1 fails to connect to the main server (192.168.0.101), it will automatically connect to an alternative server (192.168.0.201) and returns a connection object. Any error is not returned to the user. If it can not communicate with the server because the connection is broken at 2 during executeUpdate() or before then, it automatically connects to the alternative server inside the driver and continues to use the existing connection object and returns SQLException. Users can continue to use the existing connection object after processing SQLException.

Whether failover or not can be viewed through getWarnings() of connection object.

A failover feature of GOLDILOCKS JDBC is that a user can continue to use statement object or PreparedStatement object created from connection object. (ResultSet can not continue to be used.)

In particular, a user can continue to use the object because PreparedStatements perform the prepare operations internally again in the alternative server if a failover occurs.

```
Connection con = DriverManager.getConnection(url, prop);
PreparedStatement pstmt = 
    con.prepareStatement("insert into t1 values (?,?)");
...
try
{
    pstmt.setInt(1, 100);
    pstmt.setString(2, "John");
    pstmt.executeUpdate();
}
catch (SQLException sException)
{
    if (sException.getErrorCode() == 21012)
    {
```

- Failover occurs due to the communication link failure error.
- A user can continue to use the pstmt object.

```
pstmt.executeUpdate(); 
    }
    else
    {
        ...
    }
}
```

GOLDILOCKS JDBC driver provides some properties related to failover. These can help a user to decide the failover type, connection order and simple policy used for failover.

<a id="24fa6c84a6c24378"></a>
#### failover_type

The property is used to select the failover type. In the example above, the failover at 1 is the connection failover and the failover at 2 is the session failover. If the property value is *connection*, only the connection failover is used, and if it is *session*, both of the connection failover and session failover can be used. The default value is *session*.

<a id="61c8f93423d7adc1"></a>
#### failover_granularity

When failover occurs, the prepare operation is performed after the PreparedStatement objects which are generated from the current connection object are connected to the alternative server. If the prepare operation fails in the alternative server (An error may occur due to the different server environment.), the property is used to determine whether to consider the failover failed or to ignore the prepare error. The property value is either 0 or 1. If the property value is 0, the prepare error is ignored and the failover continuously proceeds. If the property value is 1, the failover is failed. The default value is 0. If the value is 0 and the prepare operation is failed, PreparedStatement object can not continue to be used and the user should directly create the PreparedStatement object again.

<a id="100f752d5a6283ae"></a>
### Connecting in Direct Attach Mode

Since JDBC 1.1, Goldilocks provides the connection in direct attach mode (D/A mode) besides the existing connection in Client/ Server mode (C/S mode) based on TCP/ IP. Like as ODBC D/A connection mode, this is operated directly interworking with the server process. so the server module interworks within a single process (in a process same as jvm). Therefore, the remote host can not connect in D/A mode.

D/A mode is designed to utilize the merit of an in-memory DB GOLDILOCKS, which is a fast processing. TCP/ IP based connection offsets the fast processing of GOLDILOCKS by expensive cost, so an alternative method is required when a fast processing is required. Though it is restricted to be operated within the host which is same as the host of GOLDILOCKS server, this D/A mode connection is a good solution.

JDBC program connecting in D/A mode can directly call the server feature by loading GOLDILOCKS jni library when DB connection is created first within jvm. A server module can be directly called through native interface in jvm without network cost, it enables faster processing than the existing C/S mode.

<a id="d3e9f993caeaa16e"></a>
#### Connecting Method

Use *0.0.0.0:0* instead of existing ip:port in the connection URL to connect in D/A mode. The existing URL can be literaly used and using a special ip:port address (0.0.0.0:0) can minimize changing exisiting applications. Or, use a special protocol (*da*) to connect in D/A mode.

```
Connection con =
 DriverManager.getConnection("jdbc:goldilocks://0.0.0.0:0/test","TEST","test");
```

or,

```
Connection con =
 DriverManager.getConnection("jdbc:goldilocks:da/test", "TEST", "test");
```

<a id="cc056002461c496a"></a>
#### Features of D/A Connection

GOLDILOCKS server module can be directly called in jvm when connecting in D/A mode. It is called through JNI (Java Native Interface) between JDBC program and GOLDILOCKS server module. It uses the server module with minimum call cost considering that it is expensive to call JNI, so it is faster double than the JDBC based on existing TCP/ IP.

When using the connection based on the existing TCP/ IP, it uses only goldilocks6.jar file. However, when using the connection based on D/A mode, it uses libgoldilocksjni.so file and libgoldilocksas.so file in $GOLDILOCKS_HOME/lib by dynamically loading them. Therefore, an error occurs when connecting if those two library files do not exist. However, the location of the library files need not to be separately specified when operating java program. Because it searches for those two library files and loads them as long as it is in the directory as same as the directory of goldilocks6.jar file.

<a id="fbfef9bc90db5ce9"></a>
## JDBC API References

<a id="786b1a1a62137716"></a>
### Array

The class is not implemented.

<a id="6dc236aca5be5ea9"></a>
#### free

```
void free() throws SQLException
```

<a id="1cd94aa26e6157d2"></a>
#### getArray

```
Object getArray() throws SQLException
```

```
Object getArray(Map<String,Class<?>> map) throws SQLException
```

```
Object getArray(long index, int count) throws SQLException
```

```
Object getArray(long index, int count, Map<String,Class<?>> map) throws SQLException
```

<a id="45f2141e7b6f6cc6"></a>
#### getBaseType

```
int getBaseType() throws SQLException
```

<a id="93bf66d549b912ce"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="2435f33881008a6c"></a>
#### getResultSet

```
ResultSet getResultSet() throws SQLException
```

```
ResultSet getResultSet(Map<String,Class<?>> map) throws SQLException
```

```
ResultSet getResultSet(long index, int count) throws SQLException
```

```
ResultSet getResultSet(long index, int count, Map<String,Class<?>> map) throws SQLException
```

<a id="a18010506181a3b7"></a>
### Blob

The class is not implemented.

<a id="99939130e1820881"></a>
#### free

```
void free() throws SQLException
```

<a id="60f5a66c77885035"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

```
InputStream getBinaryStream(long pos, long length) throws SQLException
```

<a id="903686fd71fb0ddf"></a>
#### getBytes

```
byte[] getBytes(long pos, int length) throws SQLException
```

<a id="ba6fc99cf9b8bc0e"></a>
#### length

```
long length() throws SQLException
```

<a id="0b6d62b2a50c8b61"></a>
#### position

```
long position(byte[] pattern, long start) throws SQLException
```

```
long position(Blob pattern, long start) throws SQLException
```

<a id="7555bc25a8aa19bc"></a>
#### setBinaryStream

```
OutputStream setBinaryStream(long pos) throws SQLException
```

<a id="2f3d0f46ea7e8f73"></a>
#### setBytes

```
int setBytes(long pos, byte[] bytes) throws SQLException
```

```
int setBytes(long pos, byte[] bytes, int offset, int len) throws SQLException
```

<a id="dcba0cebb2e66272"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="bf058abff091a181"></a>
### CallableStatement

<a id="a6ed3b8cb26d0edf"></a>
#### getArray

```
Array getArray(int parameterIndex) throws SQLException
```

- Operation: It does not support an array type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
Array getArray(String parameterName) throws SQLException
```

- Operation: It does not support an array type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="f00e09e6b1a66cd1"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in BigDecimal type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
BigDecimal getBigDecimal(int parameterIndex, int scale) throws SQLException
```

- Operation: It is not implemented. (It is a deprecated method.)
- Exception: It always throws SQLFeatureNotSupportedException.

```
BigDecimal getBigDecimal(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="645a60e8dcfa96cb"></a>
#### getBlob

```
Blob getBlob(int parameterIndex) throws SQLException
```

- Operation: It does not support blob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
Blob getBlob(String parameterName) throws SQLException
```

- Operation: It does not support blob type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="108b85f93d3fe89b"></a>
#### getBoolean

```
boolean getBoolean(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in boolean type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
boolean getBoolean(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a5ea706195dfcf1c"></a>
#### getByte

```
byte getByte(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in byte type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
byte getByte(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="9580af0621b986e8"></a>
#### getBytes

```
byte[] getBytes(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in byte[] type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
byte[] getBytes(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="614fc80c8eb6e6f2"></a>
#### getCharacterStream

```
Reader getCharacterStream(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in reader type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Reader getCharacterStream(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="8f35f0bf77e5695e"></a>
#### getClob

```
Clob getClob(int parameterIndex) throws SQLException
```

- Operation: It does not support clob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
Clob getClob(String parameterName) throws SQLException
```

- Operation: It does not support clob type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="624e8db9a4a8c47c"></a>
#### getDate

```
Date getDate(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in date type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses local time zone and locale when creating a date object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Date getDate(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in date type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses time zone and locale of cal when creating a date object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Date getDate(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Date getDate(String parameterName, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="12f5bdd9c65c8b7b"></a>
#### getDouble

```
double getDouble(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in double type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
double getDouble(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="7892309732af9fb6"></a>
#### getFloat

```
float getFloat(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in float type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
float getFloat(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="955d712bdecc79db"></a>
#### getInt

```
int getInt(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in int type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
int getInt(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6503c3e41a5f8230"></a>
#### getLong

```
long getLong(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in long type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
long getLong(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="aee48d3dadec541f"></a>
#### getNCharacterStream

```
Reader getNCharacterStream(int parameterIndex) throws SQLException
```

- Operation: Currently, it does not support NCHAR-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Reader getNCharacterStream(String parameterName) throws SQLException
```

- Operation: Currently, it does not support NCHAR-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e1a72a5fb9c9940f"></a>
#### getNClob

```
NClob getNClob(int parameterIndex) throws SQLException
```

- Operation: Currently, it does not support NClob-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

```
NClob getNClob(String parameterName) throws SQLException
```

- Operation: Currently, it does not support NClob-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="48d581aece833080"></a>
#### getNString

```
String getNString(int parameterIndex) throws SQLException
```

- Operation: Currently, it does not support NCHAR-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

```
String getNString(String parameterName) throws SQLException
```

- Operation: Currently, it does not support NCHAR-family type.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="35168d5f29648948"></a>
#### getObject

```
Object getObject(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in Java object type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Object getObject(int parameterIndex, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Object getObject(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Object getObject(String parameterName, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="8bfa1a30b1af17cc"></a>
#### getRef

```
Ref getRef(int parameterIndex) throws SQLException
```

- Operation: It does not support ref type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
Ref getRef(String parameterName) throws SQLException
```

- Operation: It does not support ref type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="65d31306d05051c4"></a>
#### getRowId

```
RowId getRowId(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in rowid type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
RowId getRowId(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a3e8c9ebb732653a"></a>
#### getShort

```
short getShort(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in short type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
short getShort(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="9d5ab0958e41310f"></a>
#### getSQLXML

```
SQLXML getSQLXML(int parameterIndex) throws SQLException
```

- Operation: It does not support SQLXML type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
SQLXML getSQLXML(String parameterName) throws SQLException
```

- Operation: It does not support SQLXML type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="67aabd1197a5b573"></a>
#### getString

```
String getString(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in string type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
String getString(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="f153bd8971405b71"></a>
#### getTime

```
Time getTime(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in time type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses local time zone when creating a time object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Time getTime(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in time type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses time zone of cal when creating a time object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Time getTime(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Time getTime(String parameterName, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ae81df8db186caa2"></a>
#### getTimestamp

```
Timestamp getTimestamp(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in timestamp type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses local time zone when creating a timestamp object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Timestamp getTimestamp(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in timestamp type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115). It uses time zone of cal when creating a timestamp object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Timestamp getTimestamp(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Timestamp getTimestamp(String parameterName, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="b9627adf188807f0"></a>
#### getURL

```
URL getURL(int parameterIndex) throws SQLException
```

- Operation: It does not support URL type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
URL getURL(String parameterName) throws SQLException
```

- Operation: It does not support URL type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="bc90a8c3a0e77eb7"></a>
#### registerOutParameter

```
void registerOutParameter(int parameterIndex, int sqlType) throws SQLException
```

- Operation: It registers out parameters positioned in parameterIndex as sqlType. All out parameters should be registered before executing the stored procedure. JDBC type of out parameter specified as sqlType determines Java type which is used in a get method to read parameter parameter value. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLFeatureNotSupprtedException.

```
void registerOutParameter(int parameterIndex, int sqlType, int scale) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void registerOutParameter(int parameterIndex, int sqlType, String typeName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void registerOutParameter(String parameterName, int sqlType) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void registerOutParameter(String parameterName, int sqlType, int scale) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void registerOutParameter(String parameterName, int sqlType, String typeName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e96cbc6d4b8de55e"></a>
#### setAsciiStream

```
void setAsciiStream(String parameterName, InputStream x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setAsciiStream(String parameterName, InputStream x, int length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setAsciiStream(String parameterName, InputStream x, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="1877346c1b2f83ea"></a>
#### setBigDecimal

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="1b9f714ddc967b58"></a>
#### setBinaryStream

```
void setBinaryStream(String parameterName, InputStream x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setBinaryStream(String parameterName, InputStream x, int length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setBinaryStream(String parameterName, InputStream x, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="67b849ef35f9d88d"></a>
#### setBlob

```
void setBlob(String parameterName, Blob x) throws SQLException
```

- Operation: It does not support blob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
void setBlob(String parameterName, InputStream inputStream) throws SQLException
```

- Operation: It does not support blob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
void setBlob(String parameterName, InputStream inputStream, long length) throws SQLException
```

- Operation: It does not support blob type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="7e75a5643cce707d"></a>
#### setBoolean

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="da44c72d07aa6352"></a>
#### setByte

```
void setByte(String parameterName, byte x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="cbaf1dad56f11452"></a>
#### setBytes

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="996daf2ac202ef13"></a>
#### setCharacterStream

```
void setCharacterStream(String parameterName, Reader reader) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setCharacterStream(String parameterName, Reader reader, int length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setCharacterStream(String parameterName, Reader reader, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="c70b8372523147e2"></a>
#### setClob

```
void setClob(String parameterName, Clob x) throws SQLException
```

- Operation: It does not support clob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
void setClob(String parameterName, Reader reader) throws SQLException
```

- Operation: It does not support clob type.
- Exception: It always returns SQLFeatureNotSupportedException.

```
void setClob(String parameterName, Reader reader, long length) throws SQLException
```

- Operation: It does not support clob type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="cc662f510cc5344e"></a>
#### setDate

```
void setDate(String parameterName, Date x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setDate(String parameterName, Date x, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="1aa4887eb64b7b0f"></a>
#### setDouble

```
void setDouble(String parameterName, double x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="cbf6e443608cc4be"></a>
#### setFloat

```
void setFloat(String parameterName, float x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="2206e38971988086"></a>
#### setInt

```
void setInt(String parameterName, int x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="20fca33090a0e5b7"></a>
#### setLong

```
void setLong(String parameterName, long x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="413e71f4449f4ce3"></a>
#### setNCharacterStream

```
void setNCharacterStream(String parameterName, Reader value) throws SQLException
```

- Operation: It does not support NChar.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNCharacterStream(String parameterName, Reader value, long length) throws SQLException
```

- Operation: It does not support NChar.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="d692c60faf461ee9"></a>
#### setNClob

```
void setNClob(String parameterName, NClob value) throws SQLException
```

- Operation: It does not support NClob.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNClob(String parameterName, Reader reader) throws SQLException
```

- Operation: It does not support NClob.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNClob(String parameterName, Reader reader, long length) throws SQLException
```

- Operation: It does not support NClob.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="b97cc7b5433c42c2"></a>
#### setNString

```
void setNString(String parameterName, String value) throws SQLException
```

- Operation: It does not support NChar.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ac8ec02c2fd5d934"></a>
#### setNull

```
void setNull(String parameterName, int sqlType) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNull(String parameterName, int sqlType, String typeName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="45d39ed7c0ebb924"></a>
#### setObject

```
void setObject(String parameterName, Object x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setObject(String parameterName, Object x, int targetSqlType) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setObject(String parameterName, Object x, int targetSqlType, int scale) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e00c137a1b50fe2a"></a>
#### setRowId

```
void setRowId(String parameterName, RowId x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="b521163831a87a93"></a>
#### setShort

```
void setShort(String parameterName, short x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="23bfb5324c36b8df"></a>
#### setSQLXML

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

- Operation: It does not support SQLXML type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="0a58136999a8a96e"></a>
#### setString

```
void setString(String parameterName, String x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="8c4bdf6fda68d27c"></a>
#### setTime

```
void setTime(String parameterName, Time x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setTime(String parameterName, Time x, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="60e7ddf29931f540"></a>
#### setTimestamp

```
void setTimestamp(String parameterName, Timestamp x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setTimestamp(String parameterName, Timestamp x, Calendar cal) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="517b10c2329c0093"></a>
#### setURL

```
void setURL(String parameterName, URL val) throws SQLException
```

- Operation: It does not support URL type.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="29f6b28dc361e540"></a>
#### wasNull

```
boolean wasNull()
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="02c119a896636528"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="0533676e77455bf9"></a>
#### unwrap

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="93f1efccda4edecc"></a>
### Clob

The class is not implemented.

<a id="4870a3cecc408086"></a>
#### free

```
void free() throws SQLException
```

<a id="f11b27e13f2430a7"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

<a id="2610ae5e3d5efc45"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

<a id="951b3573117d9847"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

<a id="f4a88982ec1ef60c"></a>
#### length

```
long length() throws SQLException
```

<a id="a0ed6d25deb49fb5"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

```
long position(String searchstr, long start) throws SQLException
```

<a id="945ea730cae18664"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

<a id="042ec63f9ffcf6b6"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

<a id="305d49dc131e5e34"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

<a id="2d862429af3bf69f"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="62dbb79b27e48f83"></a>
### CommonDataSource

<a id="2d054f33646097fb"></a>
#### getLoginTimeout

```
int getLoginTimeout() throws SQLException
```

- Operation: It returns the login timeout setting value. Login timeout is used as a timeout value when performing socket connection to the server. If the value is not set, 0 is returned. 0 means infinite standby.
- Exception: It does not occur.

<a id="5510836ca655bf5a"></a>
#### getLogWriter

```
PrintWriter getLogWriter() throws SQLException
```

- Operation: It returns the log writer which is set in the DataSource. If it is not set, null is returned. Log writer refers to PrintWriter to write various trace logs. For more information about logging, refer to [Logging](#3e28fb7c42dbecab).
- Exception: It does not occur.

<a id="f661ae660ef7bbf0"></a>
#### setLoginTimeout

```
void setLoginTimeout(int seconds) throws SQLException
```

- Operation: It sets the login timeout value. Login timeout is used as a timeout value when performing socket connection to the server. 0 means infinite standby.
- Exception: It does not occur.

<a id="dbdbb6279a252031"></a>
#### setLogWriter

```
void setLogWriter(PrintWriter out) throws SQLException
```

- Operation: It sets the log writer in DataSource. If the value is not set, the default value is null. Log writer refers to PrintWriter to write various trace logs. If the value is set, trace log, query log, and protocol log are written according to the options, and connection object which is created from DataSource and all objects which are created from connection object such as Statement, ResultSet, perform logging. Trace log, query log, protocol log options can be specified in the connection url or property. For more information about logging, refer to [Logging](#3e28fb7c42dbecab).
- Exception: It does not occur.

<a id="d026ba7ff7cc0312"></a>
#### setDataSourceName

```
void setDataSourceName(String aDataSourceName)
```

- Operation: It sets the data source name. It is not the mandatory information required for the connection. It is the information charged separately to distinguish objects.
- Exception: It does not occur.

<a id="f0fafd16d4a6f7c5"></a>
#### setServerName

```
void setServerName(String aServerName)
```

- Operation: It sets the server name, which is the connection URL. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="b4b49e21622481f6"></a>
#### setDatabaseName

```
void setDatabaseName(String aDBName)
```

- Operation: It sets the database name. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="9a2dddca5b4c5177"></a>
#### setNetworkProtocol

```
void setNetworkProtocol(String aProtocol)
```

- Operation: It is the network protocol information. It is not the mandatory information required for the connection.
- Exception: It does not occur.

<a id="5e06a868b9e5a7b8"></a>
#### setUser

```
void setUser(String aUser)
```

- Operation: It sets the connection account name. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="3dc66ef04c4a0512"></a>
#### setPassword

```
void setPassword(String aPassword)
```

- Operation: It sets the connection account password. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="a05ade9cb66fb051"></a>
#### setPortNumber

```
void setPortNumber(int aPort)
```

- Operation: It sets the port number used when connecting to the server. It is the mandatory information required for the connection.
- Exception: It does not occur.

```
void setPortNumber(String aPort)
```

- Operation: It sets the port number used when connecting to the server. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="50bb9a76bab1ad5b"></a>
#### setRoleName

```
void setRoleName(String aRoleName)
```

- Operation: It specifies the role of when connecting to server. It is not mandatory information required for the connection, but it is the connection related information. One of "", "ADMIN", "SYSDBA" is specified.
- Exception: It does not occur.

<a id="88491feff5e70c84"></a>
#### setDescription

```
void setDescription(String aDescription)
```

- Operation: It sets the description about the data source. It is not used for the connection.
- Exception: It does not occur.

<a id="6c08e8c7035c5a50"></a>
#### setConnectionProperties

```
void setConnectionProperties(Properties aProps)
```

- Operation: It defines the properties which can be used in various connections.
- Exception: It does not occur.

<a id="09f8193719da099b"></a>
#### setURL

```
void setURL(String aURL) throws SQLException
```

- Operation: It specifies the serverName, portNumber, and database Name in URL form. It has URL as same as the URL of when connecting via DriverManager.
- Exception: If it is the wrong format, it throws SQLException.

```
void setUrl(String aUrl) throws SQLException
```

It is as same as setURL (String aURL).

<a id="a947d8aea03236b6"></a>
#### setLogTarget

```
void setLogTarget(String aTarget)
```

- Operation: If setLogWriter can not be called, the log writer is set by this method. Currently, it is supported only when aTarget is "console", other values are ignored. If it is set to "console", all loggings below the connection object which is generated from the DataSource are output to the console.
- Exception: It does not occur.

<a id="2c6ed251a466fee4"></a>
#### setTraceLog

```
void setTraceLog(String aMode)
```

- Operation: It sets the trace log. If aMode is *on*, the trace logging is on.
- Exception: It does not occur.

<a id="4923789d9da88e0b"></a>
#### setQueryLog

```
void setQueryLog(String aMode)
```

- Operation: It sets the query log. If aMode is *on*, the query logging is on.
- Exception: It does not occur.

<a id="fb8a5d367cb92cd7"></a>
#### setProtocolLog

```
void setProtocolLog(String aMode)
```

- Operation: It sets the protocol log. If aMode is *on*, the protocol logging is on.
- Exception: It does not occur.

<a id="cfac8507df01b067"></a>
### Connection

<a id="55833530b628a64f"></a>
#### clearWarnings

```
void clearWarnings() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It clears the warning object(s) owned by the current connection object.
- Exception: It does not occur.

<a id="7e27e9aabca86cf0"></a>
#### close

```
void close() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It breaks the connection with GOLDILOCKS not to use anymore the current connection and closes all statement objects created from the object. If already closed, any operation is not performed.
- Exception: It may happen when an error occurs from the server or it does not respond.

<a id="43e6a75de725826e"></a>
#### commit

```
void commit() throws SQLException
```

- Operation: For non-auto commit mode, the commit is executed for the current connection.
- Exception: If it is already closed or is on the auto-commit mode, it throws SQLException.

<a id="8ad0a86c7dd24889"></a>
#### createArrayOf

```
Array createArrayOf(String typeName, Object[] elements) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ecfe3f5f0c4f2b14"></a>
#### createBlob

```
Blob createBlob() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="740b9fe335b32778"></a>
#### createClob

```
Clob createClob() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="eb302ae64abedc8b"></a>
#### createNClob

```
NClob createNClob() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="3a3dcd428630bd85"></a>
#### createSQLXML

```
SQLXML createSQLXML() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6c901e4fdc3ec791"></a>
#### createStatement

```
Statement createStatement() throws SQLException
```

- Operation: It creates statement object. The ResultSet type created by the statement is ResultSet.TYPE_FORWARD_ONLY, and concurrency is ResultSet.CONCUR_READ_ONLY, and holdability is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed, it throws SQLException.

```
Statement createStatement(int resultSetType, int resultSetConcurrency) throws SQLException
```

- Operation: It creates statement object which creates ResultSet including the user defined resultset type and resultset concurrency. The holdability of ResultSet which are generated from the statement object is as same as the holdability of the connection type. The default holdability of connection is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed, it throws SQLException.

```
Statement createStatement(int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- Operation: It creates a statement object which creates ResultSet including the user defined resultset type, resultset concurrency and holdability.
- Exception: If it is already closed, it throws SQLException.

<a id="8235f79788f3259e"></a>
#### createStruct

```
Struct createStruct(String typeName, Object[] attributes) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="be2e27edff0fb1d9"></a>
#### getAutoCommit

```
boolean getAutoCommit() throws SQLException
```

- Operation: It returns the current auto commit mode. If setAutoCommit() has not been called, it returns true.
- Exception: It does not occur.

<a id="f6329e53c753fa92"></a>
#### getCatalog

```
String getCatalog() throws SQLException
```

- Operation: It gets the current catalog name of the database.
- Exception: If an error occurs from the server or it does not respond, then it throws SQLException.

<a id="7c81c28d0633b4da"></a>
#### getClientInfo

```
Properties getClientInfo() throws SQLException
```

- Operation: It returns client information set by the user. If setting information does not exist, It returns null.
- Exception: It does not occur.

```
String getClientInfo(String name) throws SQLException
```

- Operation: It returns specific client information set by the user. If the corresponding information does not exist, it returns null.
- Exception: It does not occur.

<a id="2556902e631a914e"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- Operation: It returns the default holdability value of statements created by this object. The default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="92fc4419f9403696"></a>
#### getMetaData

```
DatabaseMetaData getMetaData() throws SQLException
```

- Operation: It gets a DatabaseMetaData object which can be queried for metadata information from this object. It always returns the same object.
- Exception: If it is already closed, it throws SQLException.

<a id="1ca23cbeb01cbb7f"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

- Operation: It gets the transaction isolation level which is set on the current session (connection). The default value which is set on the server is Connection.TRANSACTION_READ_COMMITTED.
- Exception: If an error occurs from the server, it throws SQLException.

<a id="7c2fbfd7f1a9d26a"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="c9e375f81b2d4ae4"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns a warning which the server responds to connection object until now. If a warning does not exist or clearWarnings() is already performed, it returns null.
- Exception: It does not occur.

<a id="2227c9b8e72b095b"></a>
#### isClosed

```
boolean isClosed() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It queries whether close() is successfully called. If close() is successfully performed, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

> This method does not inform a user whether the connection to a physical server is broken. Even if the actual connection is broken it returns true when close () has never been called.

<a id="b89a8cec230f3310"></a>
#### isReadOnly

```
boolean isReadOnly() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: If the session(connection) is read only mode, it returns true. Otherwise, it returns false. The default value is false. Communication with the server occurs.
- Exception: If an error occurs from the server or it does not respond, it throws SQLException.

<a id="ceb8d3956a8e9294"></a>
#### isValid

```
boolean isValid(int timeout) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: If isClosed() returns true or the heart beat query is sent to the server and response is not successfully received, it returns false. Otherwise, it returns true.
- Exception: It does not occur.

<a id="d24bded34ca9d9fe"></a>
#### nativeSQL

```
String nativeSQL(String sql) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It returns the native SQL recognized by the server for the given user SQL statement. GOLDILOCKS always return the value as same as given by the user because the server recognizes the user's SQL statement literally.
- Exception: It does not occur.

<a id="30c0dc3ac0b2e76f"></a>
#### prepareCall

```
CallableStatement prepareCall(String sql) throws SQLException
```

- Operation: It returns CallableStatement object for calling stored procedures. ResultSet type created from this CallableStatement is ResultSet.TYPE_FORWARD_ONLY, the concurrency is ResultSet.CONCUR_READ_ONLY, and the holdability is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed or the SQL statement is wrong, then it throws SQLException.

```
CallableStatement prepareCall(String sql, int resultSetType, int resultSetConcurrency) throws SQLException
```

- Operation: It creates CallableStatement object which creates ResultSet with the resultset type and the resultset concurrency specified by the user. The holdability of ResultSet created from this CallableStatement is as same as that of the connection. The default holdability value of the connection is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed or the SQL statement is wrong, then it throws SQLException.

```
CallableStatement prepareCall(String sql, int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- Operation: It creates CallableStatement object which creates ResultSet with the resultset type, the resultset concurrency and the holdability specified by the user. 
- Exception: If it is already closed or the SQL statement is wrong, then it throws SQLException.

<a id="f62d3edff153f440"></a>
#### prepareStatement

```
PreparedStatement prepareStatement(String sql) throws SQLException
```

- Operation: It sends the SQL statement to the server and prepares (parsing, validation, optimization), and it returns the PreparedStatement object which controls the prepared statement to the user. The type of ResultSet generated by the PreparedStatement is ResultSet.TYPE_FORWARD_ONLY, and concurrency is ResultSet. CONCUR_READ_ONLY, and holdability is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed or the SQL statement is wrong, it throws SQLException.

```
PreparedStatement prepareStatement(String sql, int autoGeneratedKeys) throws SQLException
```

- Operation: If autoGeneratedKeys is Statement.NO_GENERATED_KEYS, it operates in the same way as prepareStatement(String sql) method. Otherwise, it throws an exception.
- Exception: If it is already closed, the SQL statement is wrong or autoGeneratedKeys value is neither Statement.NO_GENERATED_KEYS nor Statement.RETURN_GENERATED_KEYS, then it throws SQLException. If autoGeneratedKeys is Statement.RETURN_GENERATED_KEYS, it throws SQLFeatureNotSupportedException.

```
PreparedStatement prepareStatement(String sql, int[] columnIndexes) throws SQLException
```

- Operation: If columnIndexes is null, it operates in the same way as the prepareStatement(String sql) method. Otherwise, it throws an exception.
- Exception: If it is already closed or the SQL statement is wrong, it throws SQLException. If columnIndexes is not null, it throws SQLFeatureNotSupportedException.

```
PreparedStatement prepareStatement(String sql, int resultSetType, int resultSetConcurrency) throws SQLException
```

- Operation: It sends the SQL statement to the server and prepares (parsing, validation, optimization). It returns the PreparedStatement object which controls the prepared statement to the user. It creates the PreparedStatement object generating ResultSet which includes the user defined result set type and result set concurrency. The holdability of ResultSet which is generated by PreparedStatement is as same as the holdability of connection. The default holdability value of connection is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If it is already closed or the SQL statement is wrong, it throws SQLException.

```
PreparedStatement prepareStatement(String sql, int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- Operation: It sends the SQL statement to the server and prepares (parsing, validation, optimization). It returns the PreparedStatement object which controls the prepared statement to the user. It creates the PreparedStatement object generating ResultSet which includes the user defined result set type and result set concurrency and holdability.
- Exception: If it is already closed or the SQL statement is wrong, it throws SQLException.

```
PreparedStatement prepareStatement(String sql, String[] columnNames) throws SQLException
```

- Operation: If columnNames is null, it operates in the same way as prepareStatement(String sql) method. Otherwise, it throws an exception.
- Exception: If it is already closed or the SQL statement is wrong, it throws SQLException. If columnNames is not null, it throws SQLFeatureNotSupportedException.

<a id="1e731f17e2909684"></a>
#### releaseSavepoint

```
void releaseSavepoint(Savepoint savepoint) throws SQLException
```

- Operation: It removes the savepoint from the server. It also removes all savepoints after this savepoint.
- Exception: If it is already closed or the savepoint object was already released or it is not the GOLDILOCKS savepoint object, it throws SQLException.

<a id="fa142e1eb6e7981a"></a>
#### rollback

```
void rollback() throws SQLException
```

- Operation: If it is non auto commit mode, it rolls back the current transaction.
- Exception: If it is already closed or it is the auto commit mode or an error is returned from the server, it throws SQLException.

```
void rollback(Savepoint savepoint) throws SQLException
```

- Operation: If it is non auto commit mode, it performs partial rollback to the savepoint for the current transaction.
- Exception: If it is already closed or it is the auto commit mode or an error is returned from the server or the savepoint is not valid, it throws SQLException.

<a id="3129d82db95e053b"></a>
#### setAutoCommit

```
void setAutoCommit(boolean autoCommit) throws SQLException
```

- Operation: It changes the auto commit mode for the current connection. If the performed transaction exists and the non auto commit mode is changed to the auto commit, it performs commit.
- Exception: It is as same as the exception which may occur during the commit process.

<a id="fcb1cf0af8b395c0"></a>
#### setCatalog

```
void setCatalog(String catalog) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="4cab1e6ed8b00a61"></a>
#### setClientInfo

```
void setClientInfo(Properties properties) throws SQLException
```

- Operation: It sets the user defined client information. Existing client information is eliminated. It does not affect the server.
- Exception: It does not occur.

```
void setClientInfo(String name, String value) throws SQLException
```

- Operation: It adds the user defined client information. Existing client information is retained.
- Exception: It does not occur.

<a id="8d818107a7524d99"></a>
#### setHoldability

```
void setHoldability(int holdability) throws SQLException
```

- Operation: It sets the ResultSet holdability which is generated by the statement generated from this object. If the method is not called, the default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="15c588b3877705a2"></a>
#### setReadOnly

```
void setReadOnly(boolean readOnly) throws SQLException
```

- Operation: It sets the read only property of the current session (connection). The default value is false.
- Exception: If it is already closed or an error is returned from the server, it throws SQLException.

<a id="b7a43b737b617181"></a>
#### setSavepoint

```
Savepoint setSavepoint() throws SQLException
```

- Operation: If it is the non auto commit mode, it sets the savepoint for the current transaction. The savepoint name is internally determined.
- Exception: If it is already closed or it is the auto commit mode or an error is returned from the server, it throws SQLException.

```
Savepoint setSavepoint(String name) throws SQLException
```

- Operation: If it is the non auto commit mode, it sets the savepoint whose name is specfied by the user for the current transaction.
- Exception: If it is already closed or it is the auto commit mode or an error is returned from the server, it throws SQLException.

<a id="7cabf9940501b5fc"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

- Operation: It changes the transaction isolation for the current session (connection). The supported value is Connection.TRANSACTION_READ_COMMITED, Connection.TRANSACTION_READ_UNCOMMITTED, and Connection.TRANSACTION_SERIALIZABLE. Connection.READ_UNCOMMITTED is set to Connection.TRANSACTION_READ_COMMITED, and Connection.TRANSACTION_REPEATABLE_READ is set to Connection.TRANSACTION_SERIALIZABLE.
- Exception: If it is already closed or the level has the wrong value, it throws SQLException.

<a id="c44aa0d919590007"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a344404a73fb3bb8"></a>
#### isWrapperFor

```
void isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether this object is a class which implements the iface interface. If it is, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper but it only queries only whether the given argument class type is implemented because GOLDILOCKS connection object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="ca6082f9abfd438d"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS connection is not the wrapper of any other class. It returns itself after casting it to the corresponding type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of this object (if this object returns the unimplemented type), it throws SQLException.

<a id="b7850322b68c4022"></a>
### ConnectionPoolDataSource

<a id="971cea08c8878f29"></a>
#### getPooledConnection

```
PooledConnection getPooledConnection() throws SQLException
```

- Operation: It creates the PooledConnection object. Various connection information, such as user name, password, connection URL should be set through the setter method in advance.
- Exception: If the connection fails, it throws SQLException.

```
PooledConnection getPooledConnection(String user, String password) throws SQLException
```

- Operation: It creates the PooledConnection object. Username and password shall comply with the argument. Other connection information should be set to the setter method in advance.
- Exception: If the connection fails, it throws SQLException.

<a id="d843475e86d83fdc"></a>
### DatabaseMetaData

<a id="1d569a57eddbee69"></a>
#### allProceduresAreCallable

```
boolean allProceduresAreCallable() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="b762a42f02c5f424"></a>
#### allTablesAreSelectable

```
boolean allTablesAreSelectable() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="6818fb0a9d265719"></a>
#### autoCommitFailureClosesAllResultSets

```
boolean autoCommitFailureClosesAllResultSets() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="27f28cc507aba7f1"></a>
#### dataDefinitionCausesTransactionCommit

```
boolean dataDefinitionCausesTransactionCommit() throws SQLException
```

- Operation: It always returns false because it does not automatically commit DDL statements at run-time.
- Exception: It does not occur.

<a id="ddc21556eb60efed"></a>
#### dataDefinitionIgnoredInTransactions

```
boolean dataDefinitionIgnoredInTransactions() throws SQLException
```

- Operation: It always returns false, because DDL statements are included in a transaction.
- Exception: It does not occur.

<a id="9e86cd21868cfa29"></a>
#### deletesAreDetected

```
boolean deletesAreDetected(int type) throws SQLException
```

- Operation: If type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="51f72fafdf932be2"></a>
#### doesMaxRowSizeIncludeBlobs

```
boolean doesMaxRowSizeIncludeBlobs() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="aef7e20f81c40f83"></a>
#### getAttributes

```
ResultSet getAttributes(String catalog, String schemaPattern, String typeNamePattern, String attributeNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="621d26833680f651"></a>
#### getBestRowIdentifier

```
ResultSet getBestRowIdentifier(String catalog, String schema, String table, int scope, boolean nullable) throws SQLException
```

- Operation: It returns a ResultSet including one row consisting with rowid information because the rowid type is supported for all tables. If the table does not exist, it returns an empty ResultSet.
- Exception: If the table is null or an error is returned from the server, it throws SQLException.

<a id="4074ff1ebb77815a"></a>
#### getCatalogs

```
ResultSet getCatalogs() throws SQLException
```

- Operation: It returns a ResultSet which has the catalog name in a column.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="7a49953988fd46ae"></a>
#### getCatalogSeparator

```
String getCatalogSeparator() throws SQLException
```

- Operation: It returns a catalog separator character.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="4515124c87e4dbec"></a>
#### getCatalogTerm

```
String getCatalogTerm() throws SQLException
```

- Operation: It returns a catalog term character.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2c63caa2690e6da3"></a>
#### getClientInfoProperties

```
ResultSet getClientInfoProperties() throws SQLException
```

- Operation: It returns a ResultSet including client information.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0a69a8bdfb080a3c"></a>
#### getColumnPrivileges

```
ResultSet getColumnPrivileges(String catalog, String schema, String table, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including column privilege information of the column in the table. If the table or the column corresponding to the column name pattern does not exist, it returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d68a567c9e2e0d71"></a>
#### getColumns

```
ResultSet getColumns(String catalog, String schemaPattern, String tableNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including all column information of the table. If the table or the column corresponding to the column name pattern does not exist, it returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="09d18369a528bbe7"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns the connection object which created the DatabaseMetaData object.
- Exception: It does not occur.

<a id="3d0717d39ee03dda"></a>
#### getCrossReference

```
ResultSet getCrossReference(String parentCatalog, String parentSchema, String parentTable, String foreignCatalog, String foreignSchema, String foreignTable) throws SQLException
```

- Operation: It returns a ResultSet including information of the foreign keys which refers to the given parent table in the given foreign key table. If reference relationship does not exist, it returns an empty ResultSet.
- Exception: If the foreign table or parent table is null or an error is returned from the server, it throws SQLException.

<a id="42a728fede7821a3"></a>
#### getDatabaseMajorVersion

```
int getDatabaseMajorVersion() throws SQLException
```

- Operation: It returns the major version of the product.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="e5583806a221c13e"></a>
#### getDatabaseMinorVersion

```
int getDatabaseMinorVersion() throws SQLException
```

- Operation: It returns the minor version of the product.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="f4a57134f833b36c"></a>
#### getDatabaseProductName

```
String getDatabaseProductName() throws SQLException
```

- Operation: It returns the product name.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="54fad147191742ac"></a>
#### getDatabaseProductVersion

```
String getDatabaseProductVersion() throws SQLException
```

- Operation: It returns the product version.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d97020eedbf6644b"></a>
#### getDefaultTransactionIsolation

```
int getDefaultTransactionIsolation() throws SQLException
```

- Operation: It returns the default transaction isolation. The default value which is set on the server is Connection.TRANSACTION_READ_COMMITTED.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="7e4553b6f98cebe5"></a>
#### getDriverMajorVersion

```
int getDriverMajorVersion() throws SQLException
```

- Operation: It returns the major version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="0e5b7adae127eced"></a>
#### getDriverMinorVersion

```
int getDriverMinorVersion() throws SQLException
```

- Operation: It returns the minor version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="4f7857487fc2d175"></a>
#### getDriverName

```
String getDriverName() throws SQLException
```

- Operation: It returns "GOLDILOCKS JDBC Driver".
- Exception: It does not occur.

<a id="cc7abfabf7d439fc"></a>
#### getDriverVersion

```
String getDriverVersion() throws SQLException
```

- Operation: It returns GOLDILOCKS JDBC driver version string. It includes the protocol version.
- Exception: It does not occur.

<a id="be2427b341c1f3c8"></a>
#### getExportedKeys

```
ResultSet getExportedKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including foreign key information referring to the column in the given table.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="f11ca987f234714d"></a>
#### getExtraNameCharacters

```
String getExtraNameCharacters() throws SQLException
```

- Operation: It returns "-$".
- Exception: It does not occur.

<a id="aca65da6c2f6a189"></a>
#### getFunctionColumns

```
ResultSet getFunctionColumns(String catalog, String schemaPattern, String functionNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="8af7607cf6407cd7"></a>
#### getFunctions

```
ResultSet getFunctions(String catalog, String schemaPattern, String functionNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="165f7bb7246b641f"></a>
#### getIdentifierQuoteString

```
String getIdentifierQuoteString() throws SQLException
```

- Operation: It returns an identifier quote character. The value that is set on the server is ".
- Exception: If an error is returned from the server, it throws SQLException.

<a id="5c2bf9825c2eb08a"></a>
#### getImportedKeys

```
ResultSet getImportedKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including parent key information to which the foreign key column in the given table refers.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="46e352163c612da6"></a>
#### getIndexInfo

```
ResultSet getIndexInfo(String catalog, String schema, String table, boolean unique, boolean approximate) throws SQLException
```

- Operation: It returns a ResultSet including index information of the given table. If unique is true, only unique index information is displayed. The approximate argument is ignored.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2d615a4148e54de4"></a>
#### getJDBCMajorVersion

```
int getJDBCMajorVersion() throws SQLException
```

- Operation: It returns JDBC major version of GOLDILOCKS JDBC driver. It can vary depending on the jar file in use.
- Exception: It does not occur.

<a id="06243c93a4524da0"></a>
#### getJDBCMinorVersion

```
int getJDBCMinorVersion() throws SQLException
```

- Operation: It returns JDBC minor version of GOLDILOCKS JDBC driver. It can vary depending on the jar file in use.
- Exception: It does not occur.

<a id="f1f9b0b5d1120abd"></a>
#### getMaxBinaryLiteralLength

```
int getMaxBinaryLiteralLength() throws SQLException
```

- Operation: It gets the maximum binary length from the server. 0 refers that the maximum length is infinite. 
- Exception: If an error is returned from the server, it throws SQLException.

<a id="eaffd65cb26ff15b"></a>
#### getMaxCatalogNameLength

```
int getMaxCatalogNameLength() throws SQLException
```

- Operation: It gets the maximum length of the catalog name from the server. 0 refers that the maximum length is infinite. 
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2018bb46fa15299b"></a>
#### getMaxCharLiteralLength

```
int getMaxCharLiteralLength() throws SQLException
```

- Operation: It gets the maximum literal length from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="12315af0ad350d21"></a>
#### getMaxColumnNameLength

```
int getMaxColumnNameLength() throws SQLException
```

- Operation: It gets the maximum length of the column name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="b3690866bc229120"></a>
#### getMaxColumnsInGroupBy

```
int getMaxColumnsInGroupBy() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in *group by* clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="4a207806fa2065b7"></a>
#### getMaxColumnsInIndex

```
int getMaxColumnsInIndex() throws SQLException
```

- Operation: It gets the maximum number of columns available to use as the index from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3d2a53dd859627b5"></a>
#### getMaxColumnsInOrderBy

```
int getMaxColumnsInOrderBy() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in *order by* clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="8ea1123e90e21bcb"></a>
#### getMaxColumnsInSelect

```
int getMaxColumnsInSelect() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in select target clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="4749e02cf7d5e2d8"></a>
#### getMaxColumnsInTable

```
int getMaxColumnsInTable() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in the table from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2237cebd1fa8a97e"></a>
#### getMaxConnections

```
int getMaxConnections() throws SQLException
```

- Operation: It gets the maximum number of connection to the server from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="96414ed63402e3b5"></a>
#### getMaxCursorNameLength

```
int getMaxCursorNameLength() throws SQLException
```

- Operation: It gets the maximum length of the cursor name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3b5147917378f131"></a>
#### getMaxIndexLength

```
int getMaxIndexLength() throws SQLException
```

- Operation: It gets the maximum size for a single index key from the server.
- Exception: If an error is returned from the server, it throws SQLException.

> The JDBC specification defines that the available maximum size of a single index is returned in bytes, but its value is meaningless, because index size does not have limit. It operates in this way for it to have the same meaning as ODBC.

<a id="f4773e6d1edfbe00"></a>
#### getMaxProcedureNameLength

```
int getMaxProcedureNameLength() throws SQLException
```

- Operation: It gets the maximum length of the procedure name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="ea438c28a18f2b15"></a>
#### getMaxRowSize

```
int getMaxRowSize() throws SQLException
```

- Operation: It gets the maximum number of rows in a table from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="5a69d60dc6298037"></a>
#### getMaxSchemaNameLength

```
int getMaxSchemaNameLength() throws SQLException
```

- Operation: It gets the maximum length of the schema name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2db091d90d6efd3b"></a>
#### getMaxStatementLength

```
int getMaxStatementLength() throws SQLException
```

- Operation: It gets the maximum string length of an SQL statement from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="962bd72cb4aec07a"></a>
#### getMaxStatements

```
int getMaxStatements() throws SQLException
```

- Operation: It gets the maximum number of statements which can be open at once from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="322297bd7d535d82"></a>
#### getMaxTableNameLength

```
int getMaxTableNameLength() throws SQLException
```

- Operation: It gets the maximum string length of the table name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="1cdda01637bd2605"></a>
#### getMaxTablesInSelect

```
int getMaxTablesInSelect() throws SQLException
```

- Operation: It gets the maximum number of tables which can be used in the select statement from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="ec4aa6d88fd0baf0"></a>
#### getMaxUserNameLength

```
int getMaxUserNameLength() throws SQLException
```

- Operation: It gets the maximum string length of the user name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="fce403e975c0d137"></a>
#### getNumericFunctions

```
String getNumericFunctions() throws SQLException
```

- Operation: It gets a list of numeric-related functions corresponding to SQL standard from the server. Each function name is distinguished by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="e8f51860e9da305c"></a>
#### getPrimaryKeys

```
ResultSet getPrimaryKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including all primary keys in a given table.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="714c0c11b5183d13"></a>
#### getProcedureColumns

```
ResultSet getProcedureColumns(String catalog, String schemaPattern, String procedureNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including column information corresponding to the given name pattern for a given procedure.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="f20702268a5161a8"></a>
#### getProcedures

```
ResultSet getProcedures(String catalog, String schemaPattern, String procedureNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including procedure information of a given name pattern.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="6d02bf82c7cbc622"></a>
#### getProcedureTerm

```
String getProcedureTerm() throws SQLException
```

- Operation: It gets the keyword which refers to the procedure from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="33f3facb06eba761"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- Operation: It returns the default holdability property of ResultSet. It is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="aad1bdcbf4e5fcef"></a>
#### getRowIdLifetime

```
RowIdLifetime getRowIdLifetime() throws SQLException
```

- Operation: It always returns RowIdLifetime.ROWID_VALID_FOREVER.
- Exception: It does not occur.

<a id="ceedc463b61367be"></a>
#### getSchemas

```
ResultSet getSchemas() throws SQLException
```

- Operation: It returns a ResultSet including information about all schemas in the server.
- Exception: If an error is returned from the server, it throws SQLException.

```
ResultSet getSchemas(String catalog, String schemaPattern) throws SQLException
```

- Operation: It returns a ResultSet including information for all schemas which meet the pattern of a given schema name. The catalog is ignored.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="37899b1a6c92971f"></a>
#### getSchemaTerm

```
String getSchemaTerm() throws SQLException
```

- Operation: It gets the keyword which refers to the schema from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="60f7021ef0154ab3"></a>
#### getSearchStringEscape

```
String getSearchStringEscape() throws SQLException
```

- Operation: It returns the escape characters used in *like* clause as a string.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0dad3dc3446d25fa"></a>
#### getSQLKeywords

```
String getSQLKeywords() throws SQLException
```

- Operation: It returns the keywords which can not be used in SQL statement, separated by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="4141633f8dbfe246"></a>
#### getSQLStateType

```
int getSQLStateType() throws SQLException
```

- Operation: It always returns DatabaseMetaData.sqlStateSQL99.
- Exception: It does not occur.

<a id="f8a3067eaada92e1"></a>
#### getStringFunctions

```
String getStringFunctions() throws SQLException
```

- Operation: It gets a list of functions which handle the strings and corresponds to SQL standard. Each function name is distinguished by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="eb001246f7e9b208"></a>
#### getSuperTables

```
ResultSet getSuperTables(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="de28d518d427d0d5"></a>
#### getSuperTypes

```
ResultSet getSuperTypes(String catalog, String schemaPattern, String typeNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="274efb107b0eddb2"></a>
#### getSystemFunctions

```
String getSystemFunctions() throws SQLException
```

- Operation: It gets a list of system functions corresponding to SQL standard. Each function name is separated by the comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a28b235ea1a65072"></a>
#### getTablePrivileges

```
ResultSet getTablePrivileges(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including privilege information of all tables which satisfy the condition.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="9bb398144beada6e"></a>
#### getTables

```
ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types) throws SQLException
```

- Operation: It returns a ResultSet including information of all tables which satisfy the condition.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="dd73e4d0cddfa28a"></a>
#### getTableTypes

```
ResultSet getTableTypes() throws SQLException
```

- Operation: It returns a ResultSet containing information of all table types.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="27ec13aa921f3427"></a>
#### getTimeDateFunctions

```
String getTimeDateFunctions() throws SQLException
```

- Operation: It gets functions which are related to time and date and corresponds to SQL standard. Each function name is separated by the comma(,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="b6e03b7980e2419d"></a>
#### getTypeInfo

```
ResultSet getTypeInfo() throws SQLException
```

- Operation: It returns a ResultSet including information of the data type.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="da7793d29498487c"></a>
#### getUDTs

```
ResultSet getUDTs(String catalog, String schemaPattern, String typeNamePattern, int[] types) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="fafc2d45856d5b06"></a>
#### getURL

```
String getURL() throws SQLException
```

- Operation: It returns the URL used to connect to the server.
- Exception: It does not occur.

<a id="bbf5db73e550a51b"></a>
#### getUserName

```
String getUserName() throws SQLException
```

- Operation: It returns the current user name which maintains a session.
- Exception: If an error is returned from the server, it throws SQLException.

> A user name may be different from the user name used to connect firstly because the user can be changed during a session.

<a id="852f41c2535c5346"></a>
#### getVersionColumns

```
ResultSet getVersionColumns(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="1cd82581befcdb0b"></a>
#### insertsAreDetected

```
boolean insertsAreDetected(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="7a7271170160bc92"></a>
#### isCatalogAtStart

```
boolean isCatalogAtStart() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="7c685f52c875dac2"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

- Operation: It gets the information whether the current connection is the read only mode from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="5490c1d314bf88b7"></a>
#### locatorsUpdateCopy

```
boolean locatorsUpdateCopy() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="463bdc203f995aec"></a>
#### nullPlusNonNullIsNull

```
boolean nullPlusNonNullIsNull() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="2b071a56b7d51916"></a>
#### nullsAreSortedAtEnd

```
boolean nullsAreSortedAtEnd() throws SQLException
```

- Operation: It always returns false. It does not separately sort null.
- Exception: It does not occur.

<a id="3aa1ac078dd24449"></a>
#### nullsAreSortedAtStart

```
boolean nullsAreSortedAtStart() throws SQLException
```

- Operation: It always returns false. It does not separately sort null.
- Exception: It does not occur.

<a id="29ee22a43b5cdebf"></a>
#### nullsAreSortedHigh

```
boolean nullsAreSortedHigh() throws SQLException
```

- Operation: It always returns true. Null is positioned at last by default.
- Exception: It does not occur.

<a id="35218a36eafc106f"></a>
#### nullsAreSortedLow

```
boolean nullsAreSortedLow() throws SQLException
```

- Operation: It always returns false. Null is positioned at last by default.
- Exception: It does not occur.

<a id="7792d46ee479eb5b"></a>
#### othersDeletesAreVisible

```
boolean othersDeletesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="a787d2762dd078ad"></a>
#### othersInsertsAreVisible

```
boolean othersInsertsAreVisible(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="4a133b5e7a356573"></a>
#### othersUpdatesAreVisible

```
boolean othersUpdatesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="64005044e99cc94f"></a>
#### ownDeletesAreVisible

```
boolean ownDeletesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="926fa19f28d830e4"></a>
#### ownInsertsAreVisible

```
boolean ownInsertsAreVisible(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="4c9344c414cf4fb0"></a>
#### ownUpdatesAreVisible

```
boolean ownUpdatesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="b69fce71fa19d336"></a>
#### storesLowerCaseIdentifiers

```
boolean storesLowerCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="32941c15c8fd635e"></a>
#### storesLowerCaseQuotedIdentifiers

```
boolean storesLowerCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="f25de5f221e8e95b"></a>
#### storesMixedCaseIdentifiers

```
boolean storesMixedCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="b007742c7dd9ea59"></a>
#### storesMixedCaseQuotedIdentifiers

```
boolean storesMixedCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5a704fcb1b9cc5ea"></a>
#### storesUpperCaseIdentifiers

```
boolean storesUpperCaseIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5569142091e3a162"></a>
#### storesUpperCaseQuotedIdentifiers

```
boolean storesUpperCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="47149a98c85ca671"></a>
#### supportsAlterTableWithAddColumn

```
boolean supportsAlterTableWithAddColumn() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="39754b0ec3da6a8d"></a>
#### supportsAlterTableWithDropColumn

```
boolean supportsAlterTableWithDropColumn() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="2f8a547a029017fc"></a>
#### supportsANSI92EntryLevelSQL

```
boolean supportsANSI92EntryLevelSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="3d6d2366418c6c2d"></a>
#### supportsANSI92FullSQL

```
boolean supportsANSI92FullSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="b6ec786e380209eb"></a>
#### supportsANSI92IntermediateSQL

```
boolean supportsANSI92IntermediateSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="bb05299228775a36"></a>
#### supportsBatchUpdates

```
boolean supportsBatchUpdates() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="55eb3b8f1b650d23"></a>
#### supportsCatalogsInDataManipulation

```
boolean supportsCatalogsInDataManipulation() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="e78331034577d119"></a>
#### supportsCatalogsInIndexDefinitions

```
boolean supportsCatalogsInIndexDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="039f71d97d46778d"></a>
#### supportsCatalogsInPrivilegeDefinitions

```
boolean supportsCatalogsInPrivilegeDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="0f6459d21d031efa"></a>
#### supportsCatalogsInProcedureCalls

```
boolean supportsCatalogsInProcedureCalls() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="e442f8208d94f6f5"></a>
#### supportsCatalogsInTableDefinitions

```
boolean supportsCatalogsInTableDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="d9ddcf659cb971db"></a>
#### supportsColumnAliasing

```
boolean supportsColumnAliasing() throws SQLException
```

- Operation: It gets information whether to support the column aliasing from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d3af98b8f659d64b"></a>
#### supportsConvert

```
boolean supportsConvert() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="c319c9503cad109d"></a>
#### supportsConvert

```
boolean supportsConvert(int fromType, int toType) throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="ac449b6da269e352"></a>
#### supportsCoreSQLGrammar

```
boolean supportsCoreSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5027214550cfe40c"></a>
#### supportsCorrelatedSubqueries

boolean supportsCorrelatedSubqueries() throws SQLException

- Operation: It always returns true.
- Exception: It does not occur.

<a id="ac167948bc6bfb82"></a>
#### supportsDataDefinitionAndDataManipulationTransactions

```
boolean supportsDataDefinitionAndDataManipulationTransactions() throws SQLException
```

- Operation: It always returns true. It can perform DML and DDL with a single transaction.
- Exception: It does not occur.

<a id="1f8406418c4f9e35"></a>
#### supportsDataManipulationTransactionsOnly

```
boolean supportsDataManipulationTransactionsOnly() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="274ffc2b7e6d1614"></a>
#### supportsDifferentTableCorrelationNames

```
boolean supportsDifferentTableCorrelationNames() throws SQLException
```

- Operation: It gets information whether the table correlation name should be different from the table name from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="7b58b3f0e7d039a6"></a>
#### supportsExpressionsInOrderBy

```
boolean supportsExpressionsInOrderBy() throws SQLException
```

- Operation: It gets information whether the calculation can be used in *order by* clause from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="24788bcd73470dc4"></a>
#### supportsExtendedSQLGrammar

```
boolean supportsExtendedSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5b88a1c58282ace6"></a>
#### supportsFullOuterJoins

```
boolean supportsFullOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="1168acab6c421ea5"></a>
#### supportsGetGeneratedKeys

```
boolean supportsGetGeneratedKeys() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="f8b829108f665b89"></a>
#### supportsGroupBy

```
boolean supportsGroupBy() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="e4b0c42101cd2dbd"></a>
#### supportsGroupByBeyondSelect

```
boolean supportsGroupByBeyondSelect() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="a43f49f847ebbaaa"></a>
#### supportsGroupByUnrelated

```
boolean supportsGroupByUnrelated() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="d019ac0a563676e5"></a>
#### supportsIntegrityEnhancementFacility

```
boolean supportsIntegrityEnhancementFacility() throws SQLException
```

- Operation: It gets information whether to support SQL integrity enhancing feature from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="20a981587aa6811f"></a>
#### supportsLikeEscapeClause

```
boolean supportsLikeEscapeClause() throws SQLException
```

- Operation: It gets information whether to support escape clause in like statement from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3e692b61551bbb6c"></a>
#### supportsLimitedOuterJoins

```
boolean supportsLimitedOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="0b3f0a2543d9e82d"></a>
#### supportsMinimumSQLGrammar

```
boolean supportsMinimumSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="925adcff7939aa67"></a>
#### supportsMixedCaseIdentifiers

```
boolean supportsMixedCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="166982bd0807c880"></a>
#### supportsMixedCaseQuotedIdentifiers

```
boolean supportsMixedCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="968c7f5981aa7318"></a>
#### supportsMultipleOpenResults

```
boolean supportsMultipleOpenResults() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="9eb6c80140468872"></a>
#### supportsMultipleResultSets

```
boolean supportsMultipleResultSets() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="628f259af0cb221a"></a>
#### supportsMultipleTransactions

```
boolean supportsMultipleTransactions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="1cd07f636c1e809c"></a>
#### supportsNamedParameters

```
boolean supportsNamedParameters() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="3e0d1d13460aafc1"></a>
#### supportsNonNullableColumns

```
boolean supportsNonNullableColumns() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="4ee6fc6e03a162b8"></a>
#### supportsOpenCursorsAcrossCommit

```
boolean supportsOpenCursorsAcrossCommit() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="f8a4c4e87adbaf6c"></a>
#### supportsOpenCursorsAcrossRollback

```
boolean supportsOpenCursorsAcrossRollback() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="3195872214a568f2"></a>
#### supportsOpenStatementsAcrossCommit

```
boolean supportsOpenStatementsAcrossCommit() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="79d6eba78eff50ae"></a>
#### supportsOpenStatementsAcrossRollback

```
boolean supportsOpenStatementsAcrossRollback() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="e15666e10fa7676c"></a>
#### supportsOrderByUnrelated

```
boolean supportsOrderByUnrelated() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="1e607b63b679ae2b"></a>
#### supportsOuterJoins

```
boolean supportsOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="53e92f537979d1cd"></a>
#### supportsPositionedDelete

```
boolean supportsPositionedDelete() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="841d385dac7257be"></a>
#### supportsPositionedUpdate

```
boolean supportsPositionedUpdate() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="dc7c05471e1dc11f"></a>
#### supportsResultSetConcurrency

```
boolean supportsResultSetConcurrency(int type, int concurrency) throws SQLException
```

- Operation: It returns true for all ResultSet types and all concurrency. It returns false for the invalid arguments.
- Exception: It does not occur.

<a id="21811e588c8020a4"></a>
#### supportsResultSetHoldability

```
boolean supportsResultSetHoldability(int holdability) throws SQLException
```

- Operation: If the holdability is ResultSet.CLOSE_CURSORS_AT_COMMIT or ResultSet.HOLD_CURSORS_OVER_COMMIT, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="f2ea2abf59165f13"></a>
#### supportsResultSetType

```
boolean supportsResultSetType(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_FORWARD_ONLY, ResultSet.TYPE_SCROLL_INSENSITIVE or ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="0162edd8b4cd0425"></a>
#### supportsSavepoints

```
boolean supportsSavepoints() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="997b097e69ad4fba"></a>
#### supportsSchemasInDataManipulation

```
boolean supportsSchemasInDataManipulation() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="6cdb347154b2d21f"></a>
#### supportsSchemasInIndexDefinitions

```
boolean supportsSchemasInIndexDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="0bdba1fe46c38c1e"></a>
#### supportsSchemasInPrivilegeDefinitions

```
boolean supportsSchemasInPrivilegeDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="dc295454b4ce4d0a"></a>
#### supportsSchemasInProcedureCalls

```
boolean supportsSchemasInProcedureCalls() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="d564b01ef492c4ac"></a>
#### supportsSchemasInTableDefinitions

```
boolean supportsSchemasInTableDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="0837cf2f0070cc04"></a>
#### supportsSelectForUpdate

```
boolean supportsSelectForUpdate() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="d2234b605ab3ff38"></a>
#### supportsStatementPooling

```
boolean supportsStatementPooling() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="8ec6b1c64ff54081"></a>
#### supportsStoredFunctionsUsingCallSyntax

```
boolean supportsStoredFunctionsUsingCallSyntax() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="1fa284d0ee39971d"></a>
#### supportsStoredProcedures

```
boolean supportsStoredProcedures() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="0f570ada6203a04c"></a>
#### supportsSubqueriesInComparisons

```
boolean supportsSubqueriesInComparisons() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="9ea122e6cb61d84d"></a>
#### supportsSubqueriesInExists

```
boolean supportsSubqueriesInExists() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="4a820ed287089cd0"></a>
#### supportsSubqueriesInIns

```
boolean supportsSubqueriesInIns() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="23c6446359d9b7a7"></a>
#### supportsSubqueriesInQuantifieds

```
boolean supportsSubqueriesInQuantifieds() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="91d0171139903f4d"></a>
#### supportsTableCorrelationNames

```
boolean supportsTableCorrelationNames() throws SQLException
```

- Operation: It gets information whether to support the table correlation name from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0a5cce12facfec27"></a>
#### supportsTransactionIsolationLevel

```
boolean supportsTransactionIsolationLevel(int level) throws SQLException
```

- Operation: It gets information whether to support the transaction isolation level from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="7fcb486a934f6ee9"></a>
#### supportsTransactions

```
boolean supportsTransactions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="18049dc704a1e8c1"></a>
#### supportsUnion

```
boolean supportsUnion() throws SQLException
```

- Operation: It gets information whether to support the union operation from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="7cc589cdbbb15b31"></a>
#### supportsUnionAll

```
boolean supportsUnionAll() throws SQLException
```

- Operation: It gets information whether to support the union all operation from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="8a99fdd49b89659e"></a>
#### updatesAreDetected

```
boolean updatesAreDetected(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="a3bdfe1995ca1e19"></a>
#### usesLocalFilePerTable

```
boolean usesLocalFilePerTable() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="b32128ab1995c54f"></a>
#### usesLocalFiles

```
boolean usesLocalFiles() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="87a203b40470f35b"></a>
### DataSource

<a id="cb7f3cf976500846"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It opens and returns a new connection object. The information required for connection should be set through a separate non-standard method in advance.
- Exception: If the connection to the server fails, it throws SQLException.

```
Connection getConnection(String username, String password) throws SQLException
```

- Operation: It opens and returns a new connection object with the username and password. Other information required for the connection should be set through a separate non-standard method in advance.
- Exception: If the connection to the server fails, it throws SQLException.

<a id="950e23ad4d29abb0"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: This class is not implemented as the wrapper of any other class. If the object is an instance of iface, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="da4ee9cc1ae51a21"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It *returns* this because this class is not implemented as the wrapper of any other class.
- Exception: If the object is not an instance of iface, it throws SQLException.

<a id="16e541b0b569c2ce"></a>
### Driver

<a id="d523826b7857e63d"></a>
#### acceptsURL

```
boolean acceptsURL(String url) throws SQLException
```

- Operation: If the url is not null and it starts with "jdbc:goldilocks:", it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="8153c95461b6168b"></a>
#### connect

```
Connection connect(String url, Properties info) throws SQLException
```

- Operation: It creates and returns a new connection object. The url should include the server address, DB name and port.
- Exception: If the url is invalid or the connection from the server fails, it throws SQLException.

<a id="fabbd46ba6fe5ab9"></a>
#### getMajorVersion

```
int getMajorVersion() throws SQLException
```

- Operation: It returns the major version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="0940bcd968c62c06"></a>
#### getMinorVersion

```
int getMinorVersion() throws SQLException
```

- Operation: It returns the minor version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="73d88319e93f3361"></a>
#### getPropertyInfo

```
DriverPropertyInfo[] getPropertyInfo(String url, Properties info) throws SQLException
```

- Operation: It gets the list of available property when GOLDILOCKS JDBC driver is connected.
- Exception: It does not occur.

<a id="1c0f28a9fccb0dd7"></a>
#### jdbcCompliant

```
boolean jdbcCompliant() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="8ab83e8e37c83c4c"></a>
### NClob

This class is not implemented.

<a id="377000ce6c11aacc"></a>
#### free

```
void free() throws SQLException
```

<a id="2c1d8d8d3eef0a3b"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

<a id="1cc0dd5681d4a734"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

<a id="3ebaeb32b4843996"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

<a id="2ab6c423a8b1a8dc"></a>
#### length

```
long length() throws SQLException
```

<a id="8b19a6e615d11803"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

```
long position(String searchstr, long start) throws SQLException
```

<a id="2f7956a2968665df"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

<a id="675a07f177556e8b"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

<a id="e13a343239b45c52"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

<a id="8e2af4e71d68ffc0"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="7ec61749a62e0549"></a>
### ParameterMetaData

ParameterMetaData object is returned by PreparedStatement.getParameterMetaData(). The parameterMetaData of the GOLDILOCKS JDBC does not use the actual DB information but it is based on the basic type varchar for other information (such as type, etc.) except for in/out. It is because in/out is the only information got from the server on the parameter after prepared. For example, if it is prepared with the query statement which is "Select * from t1 where a =?", the parameter type used in the condition clause is not determined. The server generally assumes it a varchar type.

<a id="1e71f2128ab8a459"></a>
#### getParameterClassName

```
String getParameterClassName(int param) throws SQLException
```

- Operation: It returns java.lang.String. The parameter type is regarded as varchar.
- Exception: If the param value exceeds the range of the number of parameters, it throws SQLException.

<a id="228516989eb4c8cb"></a>
#### getParameterCount

```
int getParameterCount() throws SQLException
```

- Operation: It returns the number of parameters. It is also the number of ? used in the query statement.
- Exception: It does not occur.

<a id="5a52b30b9ce45517"></a>
#### getParameterMode

```
int getParameterMode(int param) throws SQLException
```

- Operation: It returns the in/out mode of the param-th parameter. It returns one of ParameterMetaData.parameterModeIn, ParameterMetaData.parameterModeInOut, ParameterMetaData.parameterModeOut, or ParameterMetaData.parameterModeUnknown. The case of returning parameterModeUnknown value does not exist until now.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="0bdb61ac7cdad221"></a>
#### getParameterType

```
int getParameterType(int param) throws SQLException
```

- Operation: It returns Types.VARCHAR for all parameters.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="88b3c0ab84e08a12"></a>
#### getParameterTypeName

```
String getParameterTypeName(int param) throws SQLException
```

- Operation: It returns "VARCHAR" for all parameters.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="3e78a5955b5377cc"></a>
#### getPrecision

```
int getPrecision(int param) throws SQLException
```

- Operation: It returns 4000 for all parameters. The parameter is regarded as varchar(4000) by default.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="f2ea845ed9f8c98c"></a>
#### getScale

```
int getScale(int param) throws SQLException
```

- Operation: It returns 0 for all parameters. The parameter is regarded as varchar(4000) by default.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="5b6d91b5f51d08b0"></a>
#### isNullable

```
int isNullable(int param) throws SQLException
```

- Operation: It always returns ParameterMetaData.parameterNullableUnknown.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="14b1b507392b4892"></a>
#### isSigned

```
boolean isSigned(int param) throws SQLException
```

- Operation: It always returns false.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="140b67f33ea260d1"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It enquires if it the object is an instance of iface. If so, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="a233938a9f3feea0"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: If the object is an instance of iface, it casts this object to iface type and returns it.
- Exception: If the object is not an instance of iface, it throws SQLException.

<a id="bd4ac62c48286f0d"></a>
### PooledConnection

<a id="7e621039bee20f93"></a>
#### addConnectionEventListener

```
void addConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- Operation: It registers the ConnectionEventListener object. After then, if close() of the connection object (logical connection) which is returned from PooledConnection is called or the actual connection is broken, ConnectionEvent is generated to the registered listeners.
- Exception: It does not occur.

<a id="bedb3acafe86e45e"></a>
#### addStatementEventListener

```
void addStatementEventListener(StatementEventListener listener) throws SQLException
```

- Operation: It does not perform any operation. GOLDILOCKS JDBC driver does not implement the method. Statement pooling feature is performed by the external middleware.
- Exception: It does not occur.

<a id="cac4f5256207426b"></a>
#### close

```
void close() throws SQLException
```

- Operation: It calls close() of the physical connection that the object has.
- Exception: It may occur in close() of physical connection.

<a id="33e32c2d64300bd4"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns logical connection owned by the object.
- Exception: It does not occur.

<a id="49b12212a5f16f71"></a>
#### removeConnectionEventListener

```
void removeConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- Operation: It removes the registered ConnectionEventListener. After then, ConnectionEvent is not transferred to this listener.
- Exception: It does not occur.

<a id="8812172a1e1f62b9"></a>
#### removeStatementEventListener

```
void removeStatementEventListener(StatementEventListener listener) throws SQLException
```

- Operation: It does not perform any operation.
- Exception: It does not occur.

<a id="5c8b89a602285a79"></a>
### PreparedStatement

<a id="2a6a4efbf8a9a3e3"></a>
#### addBatch

```
void addBatch() throws SQLException
```

- Operation: It registers the currently bound data as batch job. If any of this batch job is registered, an error occurs when performing execute (), executeUpdate (), executeQuery () execution. If any one is not bound for the parameter, an error occurs. After addBatch if another addBatch is performed again at the state without binding with the method of setXXX () type, it registers the batch job as the previously bound value.
- Exception: If a parameter which has never been bound exists, it throws an exception.

<a id="f38f49a0878111dd"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

- Operation: It removes all of currently bound data and information. But if at least one batch job is registered, operation is not performed.
- Exception: It does not occur.

<a id="b9fdcc0c95e63352"></a>
#### execute

```
boolean execute() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter. If the executed statement is the select statement, it returns true and gets a ResultSet from the object. Otherwise, it returns false.
- Exception: If the batch job is registered, the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="e4ff218deff856f6"></a>
#### executeQuery

```
ResultSet executeQuery() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter and fetches, then creates and returns a ResultSet object.
- Exception: If the batch job is registered or the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="ae9a90c302481a1e"></a>
#### executeUpdate

```
int executeUpdate() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter. It returns the number of updated records. If updated record with DDL statements does not exist, it returns 0.
- Exception: If the batch job is registered or the statement is not a select statement or the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="83e877ec4da6c7ad"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- Operation: It gets ResultSetMetaData object. If the prepared statement is not the select statement (It is the statement which does not return ResultSet), it returns an empty ResultSetMetaData. The method can be called before executing.
- Exception: If an error occurs on the server, it throws an exception.

<a id="d5d5d1fe2b968c63"></a>
#### getParameterMetaData

```
ParameterMetaData getParameterMetaData() throws SQLException
```

- Operation: It gets the ParameterMetaData object. It can be called before executing. However, all parameters are assumed to be varchar(4000) because information about the exact parameter type is not known to the server.
- Exception: If an error occurs on the server, it throws an exception.

<a id="6f6db93518a95fe5"></a>
#### setArray

```
void setArray(int parameterIndex, Array x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="efd4d70953933599"></a>
#### setAsciiStream

```
void setAsciiStream(int parameterIndex, InputStream x) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARCHAR type. It does not execute the encoding operation because the input data is a binary form. It does not consider the character set and assumes it as ascii data.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

> The cost of conversion to VARCHAR occurs in the server because it is bound to LONG VARCHAR. If the length can be known, it is recommended to use void setAsciiStream(int parameterIndex, InputStream x, int length).

```
void setAsciiStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARCHAR type. It does not execute the encoding operation because the input data is a binary form. It does not consider the character set and and assumes it as ascii data. If English data is inserted or the server client character set environment is identical, this method is faster than setCharacterStream or setString when inserting the string as varchar.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setAsciiStream(int parameterIndex, InputStream x, long length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARCHAR type. It does not execute the encoding operation because the input data is a binary form. It does not consider the character set and assumes it as ascii data. If English data is inserted or the server client character set environment is identical, this method is faster than setCharacterStream or setString when inserting the string as varchar.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="e68930e51a08b605"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

- Operation: It binds the BigDecimal object to the parameter index as NUMBER type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="754d578a0ef6df0d"></a>
#### setBinaryStream

```
void setBinaryStream(int parameterIndex, InputStream x) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARBINARY type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setBinaryStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARBINARY type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setBinaryStream(int parameterIndex, InputStream x, long length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARBINARY type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="afce2bcf5f4423d6"></a>
#### setBlob

```
void setBlob(int parameterIndex, Blob x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setBlob(int parameterIndex, InputStream inputStream) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setBlob(int parameterIndex, InputStream inputStream, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="acbd82f7c3043e63"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

- Operation: It binds the data x to the parameter index as BOOLEAN type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="217621e364ad7c57"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_SMALLINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="52312fc036a0df72"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

- Operation: It binds the data x to the parameter index as VARBINARY or LONG VARBINARY type. If the length of x is equal to or smaller than 4000, it is bound as VARBINARY, and if it is bigger than 4000, it is bound as LONG VARBINARY type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="0c00fa316bb73d1a"></a>
#### setCharacterStream

```
void setCharacterStream(int parameterIndex, Reader reader) throws SQLException
```

- Operation: It binds the reader object to the parameter index as LONG VARCHAR type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setCharacterStream(int parameterIndex, Reader reader, int length) throws SQLException
```

- Operation: It binds the reader object to the parameter index as LONG VARCHAR type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setCharacterStream(int parameterIndex, Reader reader, long length) throws SQLException
```

- Operation: It binds the reader object to the parameter index as LONG VARCHAR type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="0e3396510b44ed0d"></a>
#### setClob

```
void setClob(int parameterIndex, Clob x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setClob(int parameterIndex, Reader reader) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setClob(int parameterIndex, Reader reader, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a3f4aa774769ee4e"></a>
#### setDate

```
void setDate(int parameterIndex, Date x) throws SQLException
```

- Operation: It binds the data x to the parameter index as DATE type. It is equivalent to calling setDate(parameterIndex, x, Calendar.getInstance()). The local timezone is applied.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setDate(int parameterIndex, Date x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as DATE type. Date x is regarded as timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="6861604c267fb535"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_DOUBLE type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="ae8f42e1577d34af"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_REAL type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="f6a9e9b2ac42cd4e"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_INTEGER type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="0dfa57d85dfed9c5"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_BIGINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="8f958ecabf639797"></a>
#### setNCharacterStream

```
void setNCharacterStream(int parameterIndex, Reader value) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNCharacterStream(int parameterIndex, Reader value, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="583309b24ecd3906"></a>
#### setNClob

```
void setNClob(int parameterIndex, NClob value) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNClob(int parameterIndex, Reader reader) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
void setNClob(int parameterIndex, Reader reader, long length) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="765739b23a98c6f5"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="967ca6d62b7d0f2a"></a>
#### setNull

```
void setNull(int parameterIndex, int sqlType) throws SQLException
```

- Operation: It binds null to the parameter index as GOLDILOCKS type corresponding to sqlType. For more information about GOLDILOCKS type mapped to sqlType, refer to [SQL types → GOLDILOCKS types](#cb02001a30776570).
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setNull(int parameterIndex, int sqlType, String typeName) throws SQLException
```

- Operation: It binds null to the parameter index as GOLDILOCKS type corresponding to sqlType type. For more information about GOLDILOCKS type mapped to sqlType, refer to [SQL types → GOLDILOCKS types](#cb02001a30776570). The third argument, typeName, is ignored because REF or the user type is not supported.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="390226ef17994eaa"></a>
#### setObject

```
void setObject(int parameterIndex, Object x) throws SQLException
```

- Operation: It binds the data x to the parameter index as the mapped GOLDILOCKS type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

**Java objects → GOLDILOCKS types**

<a id="28bad6cc9ea16d01"></a>
| Java class | GOLDILOCKS type |
| --- | --- |
| null | VARCHAR |
| Boolean | BOOLEAN |
| Byte | NATIVE_SMALLINT |
| Short | NATIVE_SMALLINT |
| Integer | NATIVE_INTEGER |
| Long | NATIVE_BIGINT |
| Float | NATIVE_REAL |
| Double | NATIVE_DOUBLE |
| BigInteger | NATIVE_BIGINT |
| BigDecimal | NUMBER |
| String | VARCHAR or LONG VARCHAR |
| byte[] | VARBINARY or LONG VARBINARY |
| Date | DATE |
| Time | TIME |
| Timestamp | TIMESTAMP |
| Blob | N/A |
| Clob | N/A |
| InputStream | LONG VARBINARY |
| Reader | LONG VARCHAR |
| GoldilocksInterval | Corresponding INTERVAL type |
| RowId | ROWID |
| Others | N/A |

```
void setObject(int parameterIndex, Object x, int targetSqlType) throws SQLException
```

- Operation: It binds the data x to the parameter index as GOLDILOCKS type corresponding to targetSqlType. For more information about GOLDILOCKS type mapped to targetSqlType, refer to [SQL types → GOLDILOCKS types](#cb02001a30776570).
- Exception: It occurs if parameterIndex is smaller than 0 or it is greater than the number of parameters.

```
void setObject(int parameterIndex, Object x, int targetSqlType, int scaleOrLength) throws SQLException
```

- Operation: It binds the data x to the parameter index as GOLDILOCKS type corresponding to targetSqlType. For more information about GOLDILOCKS type mapped to targetSqlType, refer to [SQL types → GOLDILOCKS types](#cb02001a30776570). If x is InputStream or Reader then scaleOrLength indicates the data length. For other types this value is ignored.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="501390e32a61e104"></a>
#### setRef

```
void setRef(int parameterIndex, Ref x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="18b713fce38d6dce"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

- Operation: It binds the data x to the parameter index as ROWID type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="62d4063a0b69894f"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_SMALLINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="c9e9c58e5e29f263"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="16f4b564fa913f17"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

- Operation: It binds the data x to the parameter index as VARCHAR or LONG VARCHAR type. If the length of x is equal to or smaller than 4000, it is bound as VARCHAR, and if it is bigger than 4000, it is bound as LONG VARCHAR type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="d1dde41346199230"></a>
#### setTime

```
void setTime(int parameterIndex, Time x) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIME type. It is equivalent to calling setTime(parameterIndex, x, Calendar.getInstance()). The local timezone is applied.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setTime(int parameterIndex, Time x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIME type. Time x is regarded as timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="19e5252c1e4802b5"></a>
#### setTimestamp

```
void setTimestamp(int parameterIndex, Timestamp x) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIME type. It is equivalent to calling setTimestamp(parameterIndex, x, Calendar.getInstance()). The local timezone is applied.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setTimestamp(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIMESTAMP type. Timestamp x is regarded as timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="0249985de73d2a6b"></a>
#### setUnicodeStream

```
void setUnicodeStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- Operation: It is not implemented. (It is a deprecated method.)
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="f7596d68279f2920"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="93c9987dfe551d5d"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether this object is the class implementing the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS PreparedStatement object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="6e6f79a5123e29a7"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself even when it is unwrapped because GOLDILOCKS PreparedStatement is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not this object type (The type which is not implemented by this object is given), it throws SQLException.

<a id="247573ec3c378648"></a>
#### executeBatchAtomic

```
boolean executeBatchAtomic() throws SQLException
```

- Operation: It is identical to executeBatch(), but it is atomically executed. The batch job is either entirely succeeded or failed. It is performed faster than executeBatch(). If the executed statement is the select statement, it returns true, otherwise, it returns false.
- Exception: If batch job is not registered or an error occurs on the server, it throws SQLException.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).executeBatchAtomic();

<a id="3a06db3c0697d934"></a>
#### setTimeTimeZone

```
void setTimeTimeZone(int parameterIndex, Time x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIME WITH TIME ZONE type. Time x is regarded as timezone of cal. Timezone information for DB column refers to timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, aTime, aCalendar);

<a id="09a2c8b2b2ef5867"></a>
#### setTimestampTimeZone

```
void setTimestampTimeZone(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIMESTAMP WITH TIME ZONE type. Timestamp x is regarded as timezone of cal. Timezone information for DB column refers to timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(1, aTimestamp, aCalendar);

<a id="11fdd3707358e2cd"></a>
### Ref

The class is not implemented.

<a id="8fbe710cb431c143"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="a876fcca4927e65b"></a>
#### getObject

```
Object getObject() throws SQLException
```

```
Object getObject(Map<String,Class<?>> map) throws SQLException
```

<a id="13bc9613aa080e4c"></a>
#### setObject

```
void setObject(Object value) throws SQLException
```

<a id="40bec4ae3afea26c"></a>
### ResultSet

<a id="705cb51907a2bb91"></a>
#### absolute

```
boolean absolute(int row) throws SQLException
```

- Operation: The fetched row cursor position is at the row-th. The first row is 1. 0 points to the previous first row. If it is a negative number, it points to the last row. -1 points to the last row, and -2 points to the second row from the last row. If the cursor can be positioned within the fetched row cache, only the position information is changed within the cache. If it is not within the cache, it is fetched from the server again. If the row exceeds the range, the cursor is positioned before first or after last, and it returns false. Otherwise, the cursor is positioned at the corresponding row and it returns true.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

> If it is not in the cache, it should be fetched again. If the row is behind the current position, the number of rows(n) from row position are fetched from the server in favor of next(). If the row is prior to the current position, the number of n rows from the position(row-n+1) are fetched from the server in favor of previous().

<a id="ec4b109b494db56f"></a>
#### afterLast

```
void afterLast() throws SQLException
```

- Operation: The row cursor is positioned at *after last*. If the row cache is the last row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the last row set (The total number of rows-n + 1 to n rows, n is the number of rows fetched from the server), then positions the cursor at *after last*.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="ed1bfa97b64c7515"></a>
#### beforeFirst

```
void beforeFirst() throws SQLException
```

- Operation: The row cursor is positioned at *before first*. If the row cache is the first row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the first row set (1 to n rows, n is the number of rows fetched from the server), then positions the cursor at *before first*.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="b03951f3657df52c"></a>
#### cancelRowUpdates

```
void cancelRowUpdates() throws SQLException
```

- Operation: Cursor update feature has not been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="25ddc27d2ad0e9c3"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- Operation: It clears all SQLWarning objects which is owned by ResultSet object.
- Exception: It does not occur.

<a id="51698eecee9334c1"></a>
#### close

```
void close() throws SQLException
```

- Operation: If the cursor is open on the server, it closes the cursor (If the cursor is already closed on the server, this operation is not performed. Namely, the protocol is not transferred.), and the current state of the ResultSet object is changed to be closed. If it is already closed, then any operation is not performed.
- Exception: If an error occurs on the server, it throws SQLException.

<a id="d49d9f636675fba7"></a>
#### deleteRow

```
void deleteRow() throws SQLException
```

- Operation: Cursor update feature is not implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="84809cdd6d40a37d"></a>
#### findColumn

```
int findColumn(String columnLabel) throws SQLException
```

- Operation: It returns the index of the column name. The index of the first column is 1.
- Exception: If it is already closed or the column name is not found, it throws SQLException.

<a id="88cf24228c4c94a6"></a>
#### first

```
boolean first() throws SQLException
```

- Operation: It positions the row cursor at the first (the first row). If the row cache is the first row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the first row set (1 to n rows, n is the number of rows fetched from the server), then positions the cursor at the first. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="ef78ac553b3c9c1d"></a>
#### getArray

```
Array getArray(int columnIndex) throws SQLException
```

- Operation: Array type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Array getArray(String columnLabel) throws SQLException
```

- Operation: Array type is not supported. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115).
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e3d1142c27d64674"></a>
#### getAsciiStream

```
InputStream getAsciiStream(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as InputStream type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to InputStream, it throws SQLException.

```
InputStream getAsciiStream(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as InputStream type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to InputStream, it throws SQLException.

<a id="8bdaeec389a31ef5"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as BigDecimal type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115).
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to BigDecimal, it throws SQLException.

```
BigDecimal getBigDecimal(int columnIndex, int scale) throws SQLException
```

- Operation: This is a deprecated method. It operates in the same way as getBigDecimal(int columnIndex). The scale is ignored.
- Exception: For more information, refer to [getBigDecimal](#f00e09e6b1a66cd1)(int columnIndex).

```
BigDecimal getBigDecimal(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as BigDecimal type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115).
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to BigDecimal, it throws SQLException.

```
BigDecimal getBigDecimal(String columnLabel, int scale) throws SQLException
```

- Operation: This is a deprecated method. It operates in the same way as getBigDecimal(String columnLabel). The scale is ignored.
- Exception: For more information, refer to [getBigDecimal](#f00e09e6b1a66cd1)(String columnLabel).

<a id="11248b8ae08cd8fd"></a>
#### getBinaryStream

```
InputStream getBinaryStream(int columnIndex) throws SQLException
```

- Operation: It is as same as [getAsciiStream](#e3d1142c27d64674)(int columnIndex).
- Exception: For more information, refer to [getAsciiStream](#e3d1142c27d64674)(int columnIndex).

```
InputStream getBinaryStream(String columnLabel) throws SQLException
```

- Operation: It is as same as [getAsciiStream](#e3d1142c27d64674)(String columnLabel).
- Exception: For more information, refer to [getAsciiStream](#e3d1142c27d64674)(String columnLabel).

<a id="608e6e7a0720fab8"></a>
#### getBlob

```
Blob getBlob(int columnIndex) throws SQLException
```

- Operation: It does not support blob type currently.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Blob getBlob(String columnLabel) throws SQLException
```

- Operation: It does not support blob type currently.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6cfc3d17dcab6f87"></a>
#### getBoolean

```
boolean getBoolean(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as Boolean type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to Boolean, it throws SQLException.

```
boolean getBoolean(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as Boolean type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to Boolean, it throws SQLException.

<a id="a4bf0f2ce1a1130b"></a>
#### getByte

```
byte getByte(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as byte type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to byte, it throws SQLException.

```
byte getByte(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as byte type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to byte, it throws SQLException.

<a id="dc0ca000cd563576"></a>
#### getBytes

```
byte[] getBytes(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as byte[] type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

> If getBytes is performed for all GOLDILOCKS data types, it gets the binary form stored in DB.

```
byte[] getBytes(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as byte[] type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

> If getBytes is performed for all GOLDILOCKS data types, it gets the binary form stored in DB.

<a id="f87e44ce7d568cec"></a>
#### getCharacterStream

```
Reader getCharacterStream(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as reader type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to reader, it throws SQLException.

```
Reader getCharacterStream(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as reader type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to reader, it throws SQLException.

<a id="58f27f9ee4fef3da"></a>
#### getClob

```
Clob getClob(int columnIndex) throws SQLException
```

- Operation: It does not support clob type currently.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Clob getClob(String columnLabel) throws SQLException
```

- Operation: It does not support clob type currently.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="52a8e196c8addad8"></a>
#### getConcurrency

```
int getConcurrency() throws SQLException
```

- Operation: It returns concurrency of the current ResultSet object. It supports only ResultSet.CONCUR_READ_ONLY currently.
- Exception: It does not occur.

<a id="a239bc95a9d69b0a"></a>
#### getCursorName

```
String getCursorName() throws SQLException
```

- Operation: It gets the cursor name of the server pointed by the ResultSet. The communication with the server occurs.
- Exception: If ResultSet is already closed or an error occurs on the server, it throws SQLException.

<a id="9ac231cdd10284c2"></a>
#### getDate

```
Date getDate(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the date object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to date, it throws SQLException.

```
Date getDate(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the date object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to date, it throws SQLException.

```
Date getDate(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the date object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to date, it throws SQLException.

```
Date getDate(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the date object, the local timezone of cal is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to date, it throws SQLException.

<a id="0f119bb4605dc92b"></a>
#### getDouble

```
double getDouble(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as double type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to double, it throws SQLException.

```
double getDouble(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as double type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to double, it throws SQLException.

<a id="238ae5f7b8abb15c"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- Operation: It always returns ResultSet.FETCH_FORWARD. The backward fetch is not supported.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="95193f04fb40fcfa"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- Operation: It gets the number of rows fetched from the server at once. If it is 0, it calculates the maximum number of rows included in a communication packet per transmission. The default value is 0.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="8833d5db82bb8f8c"></a>
#### getFloat

```
float getFloat(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as float type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to float, it throws SQLException.

```
float getFloat(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as float type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to float, it throws SQLException.

<a id="761c14f110c7561c"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- Operation: It returns the holdability of the current ResultSet. It is the value determined when the ResultSet object is created, and it can not be changed in the meantime. The default value is ResultSet.HOLD_CURSOR_OVER_COMMIT.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="9c16b8090c4326bb"></a>
#### getInt

```
int getInt(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as int type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to int, it throws SQLException.

```
int getInt(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as int type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to int, it throws SQLException.

<a id="41a22757a2febf39"></a>
#### getLong

```
long getLong(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as long type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to long, it throws SQLException.

```
long getLong(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as long type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to long, it throws SQLException.

<a id="3fc64210d7921523"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- Operation: It creates and returns the ResultSetMetaData object getting detailed information on the column.
- Exception: If ResultSet is already closed or an error occurs while detailed information on the column is fetched from the server, it throws SQLException.

<a id="ec02377c9cb0ec71"></a>
#### getNCharacterStream

```
Reader getNCharacterStream(int columnIndex) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Reader getNCharacterStream(String columnLabel) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="5578305e3ab78bee"></a>
#### getNClob

```
NClob getNClob(int columnIndex) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

```
NClob getNClob(String columnLabel) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="938d8fa043c04ace"></a>
#### getNString

```
String getNString(int columnIndex) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

```
String getNString(String columnLabel) throws SQLException
```

- Operation: NCHAR family types are not supported currently.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e290a939ae085970"></a>
#### getObject

```
Object getObject(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as the most appropriate Java object type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

```
Object getObject(int columnIndex, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Object getObject(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as the most appropriate Java object type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

```
Object getObject(String columnLabel, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="eda40050766944b8"></a>
#### getRef

```
Ref getRef(int columnIndex) throws SQLException
```

- Operation: REF type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Ref getRef(String columnLabel) throws SQLException
```

- Operation: REF type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="79757146252ad18b"></a>
#### getRow

```
int getRow() throws SQLException
```

- Operation: It returns the cursor position of the current ResultSet object. The first row is 1. If it is *before first*, it returns 0.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="821cef40075fd3f3"></a>
#### getRowId

```
RowId getRowId(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as Rowld type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to Rowld, it throws SQLException.

```
RowId getRowId(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as Rowld type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to Rowld, it throws SQLException.

<a id="ff15deda9937ffea"></a>
#### getShort

```
short getShort(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as short type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to short, it throws SQLException.

```
short getShort(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as short type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#fa62c08a45390115) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to short, it throws SQLException.

<a id="31a3123e753182a4"></a>
#### getSQLXML

```
SQLXML getSQLXML(int columnIndex) throws SQLException
```

- Operation: SQLXML type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
SQLXML getSQLXML(String columnLabel) throws SQLException
```

- Operation: SQLXML type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="fadb19949a032d04"></a>
#### getStatement

```
Statement getStatement() throws SQLException
```

- Operation: It returns the statement object which created the ResultSet object.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="b39b410976e70dfc"></a>
#### getString

```
String getString(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as string type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . If getString() is performed for BINARY, VARBINARY, LONG VARBINARY, the string of hex code is returned.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

```
String getString(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as string. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . If getString() is performed for BINARY, VARBINARY, LONG VARBINARY, it returns the string of hex code.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

<a id="e163d7e4276c7588"></a>
#### getTime

```
Time getTime(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the time object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to time, it throws SQLException.

```
Time getTime(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the time object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to time, it throws SQLException.

```
Time getTime(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the time object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to time, it throws SQLException.

```
Time getTime(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the time object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to time, it throws SQLException.

<a id="79710414d62459ac"></a>
#### getTimestamp

```
Timestamp getTimestamp(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the timestamp object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the timestamp object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the timestamp object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#fa62c08a45390115) . When creating the timestamp object, the local timezone of cal is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to timestamp, it throws SQLException.

<a id="312c086a11f44a80"></a>
#### getType

```
int getType() throws SQLException
```

- Operation: It returns the current ResultSet type. It returns one of ResultSet.TYPE_FORWARD_ONLY, ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.TYPE_SCROLL_SENSITIVE.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="6b60b7f32b7ec8c8"></a>
#### getUnicodeStream

```
InputStream getUnicodeStream(int columnIndex) throws SQLException
```

- Operation: It is a deprecated method. It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

```
InputStream getUnicodeStream(String columnLabel) throws SQLException
```

- Operation: It is a deprecated method. It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="71d4f74cbcdbec8e"></a>
#### getURL

```
URL getURL(int columnIndex) throws SQLException
```

- Operation: URL type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
URL getURL(String columnLabel) throws SQLException
```

- Operation: URL type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="261a89d2eb2bdabc"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns a list of SQLWarning accumulated on the object so far. If it gets a warning from the server, it creates SQLWarning. If clearWarning is not performed, it continues to be accumulated. If a warning does not occur, null is returned.
- Exception: It does not occur.

<a id="5fc619b92e968911"></a>
#### insertRow

```
void insertRow() throws SQLException
```

- Operation: Cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="3e624263f2cf4be3"></a>
#### isAfterLast

```
boolean isAfterLast() throws SQLException
```

- Operation: It queries whether the current cursor position is at *after last*. If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="fcf3ddccf22cca67"></a>
#### isBeforeFirst

```
boolean isBeforeFirst() throws SQLException
```

- Operation: It queries whether the current cursor position is at *before first*. If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="5f76dc2ffad40c81"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- Operation: It queries whether the current ResultSet is closed. If closed, it returns true. Otherwise, it returns false. Even if the user does not call the close, ResultSet can be closed by closing the cursor of the server. It is when, for example, the statement which created the ResultSet is closed, or the transaction is committed when the holdability is ResultSet.CLOSE_CURSOR_AT_COMMIT mode, or an error occurs from the server during fetching.
- Exception: It does not occur.

<a id="e0bbd86b562bf8fb"></a>
#### isFirst

```
boolean isFirst() throws SQLException
```

- Operation: It queries whether the current cursor position is at first (the first row). If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="b89dc53f74d1299c"></a>
#### isLast

```
boolean isLast() throws SQLException
```

- Operation: It queries whether the current cursor position is at last (the last row). If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="6986001134623bde"></a>
#### last

```
boolean last() throws SQLException
```

- Operation: The row cursor is positioned at last (the last row). If the row cache is the last row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, the row cursor is positioned at last after the last row set is fetched (row from last-n+1 to the last row, n is the number of rows fetched from the server). If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="ce6b27b963abdb12"></a>
#### moveToCurrentRow

```
void moveToCurrentRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="b5f63a0087784008"></a>
#### moveToInsertRow

```
void moveToInsertRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="e1d086b8ceb87d31"></a>
#### next

```
boolean next() throws SQLException
```

- Operation: The row cursor is positioned at the next to the current row. If the current row is the last row of the row cache, the next row cache is fetched from the server. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or an error occurs from the server when fetching, it throws an exception.

<a id="003b584ce08afac0"></a>
#### previous

```
boolean previous() throws SQLException
```

- Operation: The row cursor is positioned at the row before the current position. If the current row is the first row of the row cache, the previous row cache(n rows from x-n to x-1, x is the current row index) is fetched from the server. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server during fetching, it throws an exception.

<a id="0df2fb2c7acb5071"></a>
#### refreshRow

```
void refreshRow() throws SQLException
```

- Operation: If ResultSet type is ResultSet.SCROLL_SENSITIVE, the current row cache is fetched from the server. If any row is changed (by the same transaction or other transactions), it is reflected. If ResultSet type is ResultSet.Scroll_INSENSITIVE, any operation is not performed.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server during fetching, it throws an exception.

<a id="b7138da48509811d"></a>
#### relative

```
boolean relative(int rows) throws SQLException
```

- Operation: It moves the row cursor from the current cursor position to the position apart as many as the number of rows. If it can be moved within the current row cache, only the cursor position is changed. Otherwise, the cursor is moved after the row cache is fetched from the server. If the position to be moved is backward from the current position (next direction), the row cache is fetched from rows to rows+n-1 (in favor of next). If the position to be moved is forward from the current position(previous direction), the row cache is fetched from rows-n+1 to rows (in favor of previous).
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="7a4587e5a6e1d7b9"></a>
#### rowDeleted

```
boolean rowDeleted() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is deleted (by the same transaction or other transactions). If deleted, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="8408c162c55eb261"></a>
#### rowInserted

```
boolean rowInserted() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is inserted (by the same transaction or other transactions). If inserted, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="a6acdd2290af3d2e"></a>
#### rowUpdated

```
boolean rowUpdated() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is updated (by the same transaction or other transactions). If updated, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="ba76048f8f11f45a"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- Operation: The backward fetch is not supported by the server. Therefore, only ResultSet.FETCH_FORWARD is available. SQLWarning occurs if other values are inserted.
- Exception: If ResultSet is already closed or the argument does not have the defined value, it throws an exception.

<a id="0c61a2d262f43960"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- Operation: It specifies the number of rows fetched from the server at once. 0 refers that the server determines it. If it is 0, it refers to the number of rows of which a communication packet can include at once for the forward only cursor. It is specified as 100 for the scrollable cursor.
- Exception: If ResultSet is already closed, it throws an exception.

<a id="68ad725561c9304e"></a>
#### updateArray

```
void updateArray(int columnIndex, Array x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateArray(String columnLabel, Array x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="eb8e2f4b4ba51055"></a>
#### updateAsciiStream

```
void updateAsciiStream(int columnIndex, InputStream x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateAsciiStream(int columnIndex, InputStream x, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateAsciiStream(int columnIndex, InputStream x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateAsciiStream(String columnLabel, InputStream x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateAsciiStream(String columnLabel, InputStream x, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateAsciiStream(String columnLabel, InputStream x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="b0eefdffdf756a20"></a>
#### updateBigDecimal

```
void updateBigDecimal(int columnIndex, BigDecimal x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBigDecimal(String columnLabel, BigDecimal x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="8545e87a245cde4c"></a>
#### updateBinaryStream

```
void updateBinaryStream(int columnIndex, InputStream x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBinaryStream(int columnIndex, InputStream x, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBinaryStream(int columnIndex, InputStream x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBinaryStream(String columnLabel, InputStream x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBinaryStream(String columnLabel, InputStream x, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBinaryStream(String columnLabel, InputStream x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="867ab831d075a48a"></a>
#### updateBlob

```
void updateBlob(int columnIndex, Blob x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBlob(int columnIndex, InputStream inputStream) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBlob(int columnIndex, InputStream inputStream, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBlob(String columnLabel, Blob x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBlob(String columnLabel, InputStream inputStream) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBlob(String columnLabel, InputStream inputStream, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="862d67b5dfb7ccdd"></a>
#### updateBoolean

```
void updateBoolean(int columnIndex, boolean x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBoolean(String columnLabel, boolean x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="515a5409790329b1"></a>
#### updateByte

```
void updateByte(int columnIndex, byte x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateByte(String columnLabel, byte x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="c68913a2ee226d0b"></a>
#### updateBytes

```
void updateBytes(int columnIndex, byte[] x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateBytes(String columnLabel, byte[] x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="851e42ef583ffb28"></a>
#### updateCharacterStream

```
void updateCharacterStream(int columnIndex, Reader x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateCharacterStream(int columnIndex, Reader x, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateCharacterStream(int columnIndex, Reader x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateCharacterStream(String columnLabel, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateCharacterStream(String columnLabel, Reader reader, int length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateCharacterStream(String columnLabel, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="0f2bd0247b228cef"></a>
#### updateClob

```
void updateClob(int columnIndex, Clob x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateClob(int columnIndex, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateClob(int columnIndex, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateClob(String columnLabel, Clob x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateClob(String columnLabel, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateClob(String columnLabel, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="ccabf10497efba30"></a>
#### updateDate

```
void updateDate(int columnIndex, Date x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateDate(String columnLabel, Date x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="a48802f9633128a4"></a>
#### updateDouble

```
void updateDouble(int columnIndex, double x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateDouble(String columnLabel, double x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="100ce4f8e8a35056"></a>
#### updateFloat

```
void updateFloat(int columnIndex, float x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateFloat(String columnLabel, float x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="19b8d206b724076f"></a>
#### updateInt

```
void updateInt(int columnIndex, int x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateInt(String columnLabel, int x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="c3c39732670850ba"></a>
#### updateLong

```
void updateLong(int columnIndex, long x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateLong(String columnLabel, long x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="cb6ab3ef183548cd"></a>
#### updateNCharacterStream

```
void updateNCharacterStream(int columnIndex, Reader x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNCharacterStream(int columnIndex, Reader x, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNCharacterStream(String columnLabel, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNCharacterStream(String columnLabel, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="facb46a732576a04"></a>
#### updateNClob

```
void updateNClob(int columnIndex, NClob nClob) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNClob(int columnIndex, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNClob(int columnIndex, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNClob(String columnLabel, NClob nClob) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNClob(String columnLabel, Reader reader) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNClob(String columnLabel, Reader reader, long length) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="01f93af318afa18b"></a>
#### updateNString

```
void updateNString(int columnIndex, String nString) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNString(String columnLabel, String nString) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="b97e3ab35a085001"></a>
#### updateNull

```
void updateNull(int columnIndex) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateNull(String columnLabel) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="1b8681808a441d24"></a>
#### updateObject

```
void updateObject(int columnIndex, Object x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateObject(int columnIndex, Object x, int scaleOrLength) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateObject(String columnLabel, Object x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateObject(String columnLabel, Object x, int scaleOrLength) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="4b54d48613b61fd1"></a>
#### updateRef

```
void updateRef(int columnIndex, Ref x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateRef(String columnLabel, Ref x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="6e45322c0919f43d"></a>
#### updateRow

```
void updateRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="36c84a20487a0c94"></a>
#### updateRowId

```
void updateRowId(int columnIndex, RowId x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateRowId(String columnLabel, RowId x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="010f55fa61c22cfb"></a>
#### updateShort

```
void updateShort(int columnIndex, short x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateShort(String columnLabel, short x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="a8d9f318159b8f02"></a>
#### updateSQLXML

```
void updateSQLXML(int columnIndex, SQLXML xmlObject) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateSQLXML(String columnLabel, SQLXML xmlObject) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="0954820ae7475791"></a>
#### updateString

```
void updateString(int columnIndex, String x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateString(String columnLabel, String x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="62b0812a59939e76"></a>
#### updateTime

```
void updateTime(int columnIndex, Time x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateTime(String columnLabel, Time x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="31641968065d77c9"></a>
#### updateTimestamp

```
void updateTimestamp(int columnIndex, Timestamp x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

```
void updateTimestamp(String columnLabel, Timestamp x) throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="3689d1e15b7ac49a"></a>
#### wasNull

```
boolean wasNull() throws SQLException
```

- Operation: It queries whether the column value which was read last is NULL. If it is NULL, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the column value never has been read, it throws SQLException.

<a id="b4ac84eaff97a1c3"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It queries whether this object is the class which implemented the iface interface. If it so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS ResultSet object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="e501b5d530f4e3e8"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- Operation: It eventually returns itself even when it is unwrapped because GOLDILOCKS ResultSet is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, then the method throws an exception.
- Exception: If iface is not this object type (when this object type is not implemented.), it throws SQLException.

<a id="1f62bceaa67ba985"></a>
### ResultSetMetaData

<a id="3ae98e97bdb3a513"></a>
#### getCatalogName

```
String getCatalogName(int column) throws SQLException
```

- Operation: It returns the catalog name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="971d35310b7822c3"></a>
#### getColumnClassName

```
String getColumnClassName(int column) throws SQLException
```

- Operation: It returns the name of Java class which is the most appropriate to the column type. It is specified such as java.math.BigDecimal, and it refers to getName() method in Java. For binary type, it refer to byte[].class.getName(), so it can be specified such as '[B'.
- Exception: If the column value is wrong, it throws SQLException.

<a id="b76a9ee6cd4f773d"></a>
#### getColumnCount

```
int getColumnCount() throws SQLException
```

- Operation: It returns the number of columns that the ResultSet has.
- Exception: It does not occur.

<a id="d5d29256fea21a33"></a>
#### getColumnDisplaySize

```
int getColumnDisplaySize(int column) throws SQLException
```

- Operation: It returns the maximum width when the column value is displayed.
- Exception: If the column value is wrong, it throws SQLException.

<a id="588809e1185ac9f6"></a>
#### getColumnLabel

```
String getColumnLabel(int column) throws SQLException
```

- Operation: It gets the label of the column. For example, the label is "C1 + 1" and the name is "" for the query statement such as "select C1 + 1 from t1".
- Exception: If the column value is wrong, it throws SQLException.

<a id="84716d89be3e1b98"></a>
#### getColumnName

```
String getColumnName(int column) throws SQLException
```

- Operation: It returns the alias name of the column. The original column name, not the alias name is defined to be returned in JDBC specification. However, it is recommended to use the alias name because some view names are meaningless or complicated. For example, both the name and label are "C2" for the query statement such as "select C1 as C2 from t1". For more information about the case of when name and label are different, refer to [getColumnLabel](#588809e1185ac9f6).
- Exception: If the column value is wrong, it throws SQLException.

<a id="20e952ce44aa206c"></a>
#### getColumnType

```
int getColumnType(int column) throws SQLException
```

- Operation: It returns the type of the column. The return value is defined in types. Types.OTHERS is returned for GOLDILOCKS interval family types. The constant values of the corresponding types are returned for the other types.
- Exception: If the column value is wrong, it throws SQLException.

<a id="0853d8cc86f5904a"></a>
#### getColumnTypeName

```
String getColumnTypeName(int column) throws SQLException
```

- Operation: It returns GOLDILOCKS column type name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="43a46fc41ea84284"></a>
#### getPrecision

```
int getPrecision(int column) throws SQLException
```

- Operation: It returns the precision of the column. It returns 0 for the type without any precision.
- Exception: If the column value is wrong, it throws SQLException.

<a id="a02f6f27f1eb3550"></a>
#### getScale

```
int getScale(int column) throws SQLException
```

- Operation: It returns the scale of the column. It returns 0 for the type without any scale.
- Exception: If the column value is wrong, it throws SQLException.

<a id="7a22669903f9bf4d"></a>
#### getSchemaName

```
String getSchemaName(int column) throws SQLException
```

- Operation: It returns the schema name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="0f5c3922a53a1b13"></a>
#### getTableName

```
String getTableName(int column) throws SQLException
```

- Operation: It returns the table name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="e81b953b555eadd7"></a>
#### isAutoIncrement

```
boolean isAutoIncrement(int column) throws SQLException
```

- Operation: It returns whether it is the column which is automatically given the unique value. If so, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="c929f44a2eef2f43"></a>
#### isCaseSensitive

```
boolean isCaseSensitive(int column) throws SQLException
```

- Operation: It returns whether the column is case sensitive. If it is case sensitive, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="59c453249978843b"></a>
#### isCurrency

```
boolean isCurrency(int column) throws SQLException
```

- Operation: It always returns false because the currency of the column can not be determined by the server.
- Exception: If the column value is wrong, it throws SQLException.

<a id="2df38db9eb0d0909"></a>
#### isDefinitelyWritable

```
boolean isDefinitelyWritable(int column) throws SQLException
```

- Operation: It returns whether the column is updatable. GOLDILOCKS does not support the definitely writable. It always returns the value as same as isUpdatable().
- Exception: If the column value is wrong, it throws SQLException.

<a id="458bd70ff2c99d1c"></a>
#### isNullable

```
int isNullable(int column) throws SQLException
```

- Operation: It returns whether the column has nullable. It returns either columnNullable or columnNoNulls.
- Exception: If the column value is wrong, it throws SQLException.

<a id="9f72293aba626e2c"></a>
#### isReadOnly

```
boolean isReadOnly(int column) throws SQLException
```

- Operation: It returns whether the column is read only. It always returns the opposite value of isUpdatable().
- Exception: If the column value is wrong, it throws SQLException.

<a id="ffbc5d0d656c5f50"></a>
#### isSearchable

```
boolean isSearchable(int column) throws SQLException
```

- Operation: It returns whether the column can be used in the conditional clause. It always returns true because all target columns in GOLDILOCKS can be used in the conditional clause.
- Exception: If the column value is wrong, it throws SQLException.

<a id="474f34a982d75d8e"></a>
#### isSigned

```
boolean isSigned(int column) throws SQLException
```

- Operation: It returns whether the column has a sign. If it has a sign, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="118ea774bd20740e"></a>
#### isWritable

```
boolean isWritable(int column) throws SQLException
```

- Operation: It returns whether the column is updatable.
- Exception: If the column value is wrong, it throws SQLException.

<a id="c129d16eb73c0dcf"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It queries whether the object is a class implementing the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS ResultSetMetaData object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="71589838d80376d9"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS ResultSetMetaData is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of the object (if this object returns the unimplemented type), it throws SQLException.

<a id="2a789a1a74f664bc"></a>
### RowId

<a id="5148c21e51abdb3d"></a>
#### equals

```
boolean equals(Object obj) throws SQLException
```

- Operation: If RowId of this object is as same as RowId of obj, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="504b9cbf28e93695"></a>
#### getBytes

```
byte[] getBytes() throws SQLException
```

- Operation: It returns the byte array value of RowId.
- Exception: It does not occur.

<a id="8eb0714987e2c544"></a>
#### hashCode

```
int hashCode() throws SQLException
```

- Operation: It returns the hash code value.
- Exception: It does not occur.

<a id="406b7dd6c4272257"></a>
#### toString

```
String toString() throws SQLException
```

- Operation: It returns a base-64 string of RowId value.
- Exception: It does not occur.

<a id="766c30e4d4475d9a"></a>
### RowSet

The class is not implemented

<a id="22a02ca3ab43a2a4"></a>
#### addRowSetListener

```
void addRowSetListener(RowSetListener listener) throws SQLException
```

<a id="4b29bfbb58f07cd2"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

<a id="30bdc237edd60431"></a>
#### execute

```
void execute() throws SQLException
```

<a id="2d344b111ab1ec2f"></a>
#### getCommand

```
String getCommand() throws SQLException
```

<a id="d20c90b16947f17a"></a>
#### getDataSourceName

```
String getDataSourceName() throws SQLException
```

<a id="20d3ffd5ba2477fb"></a>
#### getEscapeProcessing

```
boolean getEscapeProcessing() throws SQLException
```

<a id="5108bd6a5437be40"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

<a id="9468d3d98c65a338"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

<a id="d97634bbf60d415d"></a>
#### getPassword

```
String getPassword() throws SQLException
```

<a id="4db8005afb3f7604"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

<a id="144d9b0a8094c6b0"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

<a id="38f40e9b99e7bc6d"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

<a id="cb6e17f71f936216"></a>
#### getUrl

```
String getUrl() throws SQLException
```

<a id="46bb5610753ffebc"></a>
#### getUsername

```
String getUsername() throws SQLException
```

<a id="7418d389a69d49c8"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

<a id="91551f74314952c2"></a>
#### removeRowSetListener

```
void removeRowSetListener(RowSetListener listener) throws SQLException
```

<a id="28cd5dd27a841bbc"></a>
#### setArray

```
void setArray(int i, Array x) throws SQLException
```

<a id="f12ec61725bcaa0e"></a>
#### setAsciiStream

```
void setAsciiStream(int parameterIndex, InputStream x) throws SQLException
```

```
void setAsciiStream(int parameterIndex, InputStream x, int length) throws SQLException
```

```
void setAsciiStream(String parameterName, InputStream x) throws SQLException
```

```
void setAsciiStream(String parameterName, InputStream x, int length) throws SQLException
```

<a id="a926aca28e628818"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

<a id="23280604e25bd104"></a>
#### setBinaryStream

```
void setBinaryStream(int parameterIndex, InputStream x) throws SQLException
```

```
void setBinaryStream(int parameterIndex, InputStream x, int length) throws SQLException
```

```
void setBinaryStream(String parameterName, InputStream x) throws SQLException
```

```
void setBinaryStream(String parameterName, InputStream x, int length) throws SQLException
```

<a id="8a777dcdec2a444d"></a>
#### setBlob

```
void setBlob(int i, Blob x) throws SQLException
```

```
void setBlob(int parameterIndex, InputStream inputStream) throws SQLException
```

```
void setBlob(int parameterIndex, InputStream inputStream, long length) throws SQLException
```

```
void setBlob(String parameterName, Blob x) throws SQLException
```

```
void setBlob(String parameterName, InputStream inputStream) throws SQLException
```

```
void setBlob(String parameterName, InputStream inputStream, long length) throws SQLException
```

<a id="105fb80e04e0609f"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

<a id="90de6ff493e07c2d"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

```
void setByte(String parameterName, byte x) throws SQLException
```

<a id="7657e05bdbb58020"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

<a id="b2f11ab8256b4a92"></a>
#### setCharacterStream

```
void setCharacterStream(int parameterIndex, Reader reader) throws SQLException
```

```
void setCharacterStream(int parameterIndex, Reader reader, int length) throws SQLException
```

```
void setCharacterStream(String parameterName, Reader reader) throws SQLException
```

```
void setCharacterStream(String parameterName, Reader reader, int length) throws SQLException
```

<a id="ae32b1730cf24b32"></a>
#### setClob

```
void setClob(int i, Clob x) throws SQLException
```

```
void setClob(int parameterIndex, Reader reader) throws SQLException
```

```
void setClob(int parameterIndex, Reader reader, long length) throws SQLException
```

```
void setClob(String parameterName, Clob x) throws SQLException
```

```
void setClob(String parameterName, Reader reader) throws SQLException
```

```
void setClob(String parameterName, Reader reader, long length) throws SQLException
```

<a id="bf31c066e393327b"></a>
#### setCommand

```
void setCommand(String cmd) throws SQLException
```

<a id="906d843bb7bcd74b"></a>
#### setConcurrency

```
void setConcurrency(int concurrency) throws SQLException
```

<a id="cc22f6b15850e510"></a>
#### setDataSourceName

```
void setDataSourceName(String name) throws SQLException
```

<a id="2c784b67c08c9f89"></a>
#### setDate

```
void setDate(int parameterIndex, Date x) throws SQLException
```

```
void setDate(int parameterIndex, Date x, Calendar cal) throws SQLException
```

```
void setDate(String parameterName, Date x) throws SQLException
```

```
void setDate(String parameterName, Date x, Calendar cal) throws SQLException
```

<a id="110b10a4d77f205a"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

```
void setDouble(String parameterName, double x) throws SQLException
```

<a id="440826efa04973e4"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

<a id="6205978b38322457"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

```
void setFloat(String parameterName, float x) throws SQLException
```

<a id="48b2e8b163f67743"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

```
void setInt(String parameterName, int x) throws SQLException
```

<a id="6bdb8049f05f7e6b"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

```
void setLong(String parameterName, long x) throws SQLException
```

<a id="325b95092347d71c"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

<a id="9d6b157ebd96066e"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

<a id="a0a5a4d0021110f5"></a>
#### setNCharacterStream

```
void setNCharacterStream(int parameterIndex, Reader value) throws SQLException
```

```
void setNCharacterStream(int parameterIndex, Reader value, long length) throws SQLException
```

```
void setNCharacterStream(String parameterName, Reader value) throws SQLException
```

```
void setNCharacterStream(String parameterName, Reader value, long length) throws SQLException
```

<a id="75770d4914be473f"></a>
#### setNClob

```
void setNClob(int parameterIndex, NClob value) throws SQLException
```

```
void setNClob(int parameterIndex, Reader reader) throws SQLException
```

```
void setNClob(int parameterIndex, Reader reader, long length) throws SQLException
```

```
void setNClob(String parameterName, NClob value) throws SQLException
```

```
void setNClob(String parameterName, Reader reader) throws SQLException
```

```
void setNClob(String parameterName, Reader reader, long length) throws SQLException
```

<a id="9e1ece5d0f091931"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

```
void setNString(String parameterName, String value) throws SQLException
```

<a id="9f62cb98126879fc"></a>
#### setNull

```
void setNull(int parameterIndex, int sqlType) throws SQLException
```

```
void setNull(int paramIndex, int sqlType, String typeName) throws SQLException
```

```
void setNull(String parameterName, int sqlType) throws SQLException
```

```
void setNull(String parameterName, int sqlType, String typeName) throws SQLException
```

<a id="ff72b8f53b51225b"></a>
#### setObject

```
void setObject(int parameterIndex, Object x) throws SQLException
```

```
void setObject(int parameterIndex, Object x, int targetSqlType) throws SQLException
```

```
void setObject(int parameterIndex, Object x, int targetSqlType, int scaleOrLength) throws SQLException
```

```
void setObject(String parameterName, Object x) throws SQLException
```

```
void setObject(String parameterName, Object x, int targetSqlType) throws SQLException
```

```
void setObject(String parameterName, Object x, int targetSqlType, int scale) throws SQLException
```

<a id="00cebbb1c13f4164"></a>
#### setPassword

```
void setPassword(String password) throws SQLException
```

<a id="ae1f5f3d7ebc5aa0"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

<a id="353d6371dc14553a"></a>
#### setReadOnly

```
void setReadOnly(boolean value) throws SQLException
```

<a id="3856d4e97292c2e0"></a>
#### setRef

```
void setRef(int i, Ref x) throws SQLException
```

<a id="4de37561b905fd32"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

```
void setRowId(String parameterName, RowId x) throws SQLException
```

<a id="5e6acab0ddfa7c76"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

```
void setShort(String parameterName, short x) throws SQLException
```

<a id="3d6147c1985b0a88"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

<a id="05e3c5668c188251"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

```
void setString(String parameterName, String x) throws SQLException
```

<a id="94471fb2e3758a84"></a>
#### setTime

```
void setTime(int parameterIndex, Time x) throws SQLException
```

```
void setTime(int parameterIndex, Time x, Calendar cal) throws SQLException
```

```
void setTime(String parameterName, Time x) throws SQLException
```

```
void setTime(String parameterName, Time x, Calendar cal) throws SQLException
```

<a id="7a82c65043fb7cc0"></a>
#### setTimestamp

```
void setTimestamp(int parameterIndex, Timestamp x) throws SQLException
```

```
void setTimestamp(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

```
void setTimestamp(String parameterName, Timestamp x) throws SQLException
```

```
void setTimestamp(String parameterName, Timestamp x, Calendar cal) throws SQLException
```

<a id="c30add7ff4dada9c"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

<a id="bdbd2cd786d52d86"></a>
#### setType

```
void setType(int type) throws SQLException
```

<a id="0baa3d0afcf950ec"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

<a id="358124baa75a83f0"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

<a id="1ddc689d309cc133"></a>
#### setUrl

```
void setUrl(String url) throws SQLException
```

<a id="631b0db659a3c35e"></a>
#### setUsername

```
void setUsername(String name) throws SQLException
```

<a id="0ad44f2330683de4"></a>
### RowSetMetaData

The class is not implemented

<a id="698a66e95c8403fa"></a>
#### setAutoIncrement

```
void setAutoIncrement(int columnIndex, boolean property) throws SQLException
```

<a id="02158fab172761e4"></a>
#### setCaseSensitive

```
void setCaseSensitive(int columnIndex, boolean property) throws SQLException
```

<a id="a83b65e675da916e"></a>
#### setCatalogName

```
void setCatalogName(int columnIndex, String catalogName) throws SQLException
```

<a id="8b80d902529ead9b"></a>
#### setColumnCount

```
void setColumnCount(int columnCount) throws SQLException
```

<a id="291dcf3ba3596754"></a>
#### setColumnDisplaySize

```
void setColumnDisplaySize(int columnIndex, int size) throws SQLException
```

<a id="24956eb08d9a778e"></a>
#### setColumnLabel

```
void setColumnLabel(int columnIndex, String label) throws SQLException
```

<a id="75cf049903403892"></a>
#### setColumnName

```
void setColumnName(int columnIndex, String columnName) throws SQLException
```

<a id="9344ddaeebc9b507"></a>
#### setColumnType

```
void setColumnType(int columnIndex, int SQLType) throws SQLException
```

<a id="287010303b209075"></a>
#### setColumnTypeName

```
void setColumnTypeName(int columnIndex, String typeName) throws SQLException
```

<a id="7befea8d48451e52"></a>
#### setCurrency

```
void setCurrency(int columnIndex, boolean property) throws SQLException
```

<a id="fb6250110c0273af"></a>
#### setNullable

```
void setNullable(int columnIndex, int property) throws SQLException
```

<a id="750fe254816c3fca"></a>
#### setPrecision

```
void setPrecision(int columnIndex, int precision) throws SQLException
```

<a id="6549395693525aff"></a>
#### setScale

```
void setScale(int columnIndex, int scale) throws SQLException
```

<a id="7e4f234fea97069b"></a>
#### setSchemaName

```
void setSchemaName(int columnIndex, String schemaName) throws SQLException
```

<a id="c48861710af5c266"></a>
#### setSearchable

```
void setSearchable(int columnIndex, boolean property) throws SQLException
```

<a id="ae946696694f304a"></a>
#### setSigned

```
void setSigned(int columnIndex, boolean property) throws SQLException
```

<a id="6db4c1d050e4adfe"></a>
#### setTableName

```
void setTableName(int columnIndex, String tableName) throws SQLException
```

<a id="5067f6e97f2f9ad5"></a>
### Savepoint

<a id="0d5a1566e4b4873a"></a>
#### getSavepointId

```
int getSavepointId() throws SQLException
```

- Operation: It returns the id value which is automatically assigned.
- Exception: It throws SQLException because it does not have an ID if the savepoint object is created by giving its name.

<a id="79cadadb7c791983"></a>
#### getSavepointName

```
String getSavepointName() throws SQLException
```

- Operation: It returns the name specified at the time of when a savepoint object is created.
- Exception: If the savepoint created with an automatic id value, it throws SQLException.

<a id="fa081439d6d4196a"></a>
### SQLData

The class is not implemented.

<a id="50742ffed1f33410"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="73f2cec85f1a4b9b"></a>
#### readSQL

```
void readSQL(SQLInput stream, String typeName) throws SQLException
```

<a id="7379845213b5b19b"></a>
#### writeSQL

```
void writeSQL(SQLOutput stream) throws SQLException
```

<a id="a9dff1f3403b7ca0"></a>
### SQLXML

The class is not implemented.

<a id="7632cf435185fbe7"></a>
#### free

```
void free() throws SQLException
```

<a id="174cbe96a1146171"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

<a id="3a6b151bad8132dc"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

<a id="d1b03db7b92b7e41"></a>
#### getSource

```
<T extends Source> T getSource(Class<T> sourceClass) throws SQLException
```

<a id="5f2c50174dede87d"></a>
#### getString

```
String getString() throws SQLException
```

<a id="ba12a8562b1d77a2"></a>
#### setBinaryStream

```
OutputStream setBinaryStream() throws SQLException
```

<a id="6e851436fe0369ae"></a>
#### setCharacterStream

```
Writer setCharacterStream() throws SQLException
```

<a id="1b7366c5ffb81393"></a>
#### setResult

```
<T extends Result> T setResult(Class<T> resultClass) throws SQLException
```

<a id="1cba709dfc32bb2c"></a>
#### setString

```
void setString(String value) throws SQLException
```

<a id="bf8149029a1480d0"></a>
### Statement

<a id="f5cbab74f599e9b6"></a>
#### addBatch

```
void addBatch(String sql) throws SQLException
```

- Operation: The SQL statement is added to the batch job.
- Exception: It does not occur.

<a id="c9e4f18856eab6ce"></a>
#### cancel

```
void cancel() throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="da88db93703a7b2a"></a>
#### clearBatch

```
void clearBatch() throws SQLException
```

- Operation: It clears all registered batch jobs. If registered batch job does not exist, any operation is not performed.
- Exception: It does not occur.

<a id="d5d08e77cdc8d254"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- Operation: It clears all SQLWarning objects which is owned by the statement object.
- Exception: It does not occur.

<a id="2b7435d61ef37090"></a>
#### close

```
void close() throws SQLException
```

- Operation: The current statement object is closed, and it is released if the statement related information assigned to the server exists. If the ResultSet created by the object exists, it is closed. The object is removed from the connection object which created the statement object.
- Exception: If an error occurs when statement information is released from the server, it throws an exception.

<a id="ca8835be55334ec5"></a>
#### execute

```
boolean execute(String sql) throws SQLException
```

- Operation: It executes the SQL statement. If the executed SQL statement has the ResultSet, it returns true. Otherwise, it returns false.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing from the server, it throws an exception.

```
boolean execute(String sql, int autoGeneratedKeys) throws SQLException
```

- Operation: It executes the SQL statement. If the executed SQL statement has the ResultSet, it returns true. Otherwise, it returns false. Auto key generation is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing from the server, it throws an exception. If autoGeneratedKeys is not Statement.NO_GENERATED_KEYS, it throws SQLFeatureNotSupportedException.

```
boolean execute(String sql, int[] columnIndexes) throws SQLException
```

- Operation: It executes the SQL statement. If the executed SQL statement has the ResultSet, it returns true. Otherwise, it returns false. Auto key generation is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing from the server, it throws an exception. If the columnIndexes are not null, it throws SQLFeatureNotSupportedException.

```
boolean execute(String sql, String[] columnNames) throws SQLException
```

- Operation: It executes the SQL statement. If the executed SQL statement has the ResultSet, it returns true. Otherwise, it returns false. Auto key generation is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing from the server, it throws an exception. If the columnNames are not null, it throws SQLFeatureNotSupportedException.

<a id="acbf9c4828a4e618"></a>
#### executeBatch

```
int[] executeBatch() throws SQLException
```

- Operation: It executes the registered batch job in turn. The communication with the server occurs per each batch job. It returns the array of the number of rows in which the update reflected after executing each batch job.
- Exception: If the statement is already closed or any batch job is not registered or an error occurs when executing from the server, it throws an exception.

> It does not have definite advantage over the normal execute() because the batch jobs are not transmitted and executed at once. Use a batch execution of the PreparedStatement for fast processing.

<a id="455576890e834170"></a>
#### executeQuery

```
ResultSet executeQuery(String sql) throws SQLException
```

- Operation: It executes the given SQL statement and gets part of results and creates the ResultSet.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is not the select statement, it throws an exception.

> Its operation is a bit different from execute(). The communicate with the server occurs twice if getResultSet() is performed for the same SQL statement after performing execute(). The execution command is performed when performing execute(), and the fetch related command is performed when performing getResultSet(). On the other hand, executeQuery() assumes that the SQL statement is the select statement, and it executes all with a single communication until fetch.

<a id="3d2042a3f085c173"></a>
#### executeUpdate

```
int executeUpdate(String sql) throws SQLException
```

- Operation: It executes the SQL statement. It returns the number of rows updated by the execution.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is the select statement, it throws an exception.

```
int executeUpdate(String sql, int autoGeneratedKeys) throws SQLException
```

- Operation: It executes the SQL statement. It returns the number of rows updated by the execution. The auto key generation feature is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is the select statement, it throws an exception. If autoGeneratedKeys is not Statement.NO_GENERATED_KEYS, it throws SQLFeatureNotSupportedException.

```
int executeUpdate(String sql, int[] columnIndexes) throws SQLException
```

- Operation: It executes the SQL statement. It returns the number of rows updated by the execution. The auto key generation feature is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is the select statement, it throws an exception. If the columnIndexes are not null, it throws SQLFeatureNotSupportedException.

```
int executeUpdate(String sql, String[] columnNames) throws SQLException
```

- Operation: It executes the SQL statement. It returns the number of rows updated by the execution. The auto key generation feature is not supported.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing from the server or the SQL statement is the select statement, it throws an exception. If the columnNames are not null, it throws SQLFeatureNotSupportedException.

<a id="f7fa7dac5b0cb6fa"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns the connection object which created the object. If statement object is created with logical connection via the PooledConnection, the user gets the logical connection, not the physical connection via the method.
- Exception: If the statement is already closed, it throws an exception.

<a id="f85585168bf821da"></a>
#### getExplainPlan

```
String getExplainPlan() throws SQLException
```

- Operation: It is non-standard method, and it is the unique method of GoldilocksStatement. It gets the generated plan text. It should set for generating the plan text via setExplainPlanOption to use the method. For more information about the detailed usage, refer to [Viewing Plan Text](#f6c886676bd9a407).
- Exception: If the statement is already closed or an error occurs on the server, it throws an exception.

<a id="0d54475cdd60c21b"></a>
#### getExplainPlanOption

```
int getExplainPlanOption() throws SQLException
```

- Operation: It is non-standard method, and it is the unique method of GoldilocksStatement. It gets the option for the generating the plan text which is currently set. The return value is one of the followings and the default value is GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON_VERBOSE
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ONLY
- Exception: It does not occur.

<a id="10d414c6b2a20997"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- Operation: It always returns ResultSet.FETCH_FORWARD.
- Exception: If the statement is already closed, it throws an exception.

<a id="a813c489e4e29012"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- Operation: It returns the default fetch size of ResultSet which is got from the statement object. The default value is 0, and 0 refers that the server determines the number of fetched rows. For more information, refer to [getFetchSize](#95193f04fb40fcfa) of ResultSet.
- Exception: If the statement is already closed, it throws an exception.

<a id="1a75b6f3093086bb"></a>
#### getGeneratedKeys

```
ResultSet getGeneratedKeys() throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e40a84081597c351"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

- Operation: It returns the max field size. The value limits the maximum length of the column. If the column value is bigger than this length when fetching, the rest of the data is truncated. The default value is 0, and 0 refers that the maximum length is infinite.
- Exception: If the statement is already closed, it throws an exception.

<a id="441c7fca4c176e6d"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

- Operation: It returns the max rows. The max rows refer to the maximum number of rows of ResultSet which is got from the statement. The rows more than the maximum number of rows are ignored. The default value is 0, and 0 means infinity.
- Exception: If the statement is already closed, it throws an exception.

<a id="f6ef0d92a4a86c16"></a>
#### getMoreResults

```
boolean getMoreResults() throws SQLException
```

- Operation: It always returns false because a user can only have a single ResultSet per one execution, currently. The current ResultSet is closed.
- Exception: If the statement is already closed, it throws an exception.

```
boolean getMoreResults(int current) throws SQLException
```

<a id="3ad7218b347439fa"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

- Operation: It gets the value of the query timeout. The value is the timeout value which the sever applies at execution. The execution is canceled and the user gets the error related to timeout if the execution time exceeds the time. The unit is seconds and it applies the default value of the session if the user does not specifically set it. The default value of the session is 0 if it is not set with the property, and it refers to the infinite wait.
- Exception: If the statement is already closed, it throws an exception.

<a id="aeecbdd0d4691204"></a>
#### getResultSet

```
ResultSet getResultSet() throws SQLException
```

- Operation: It performs the fetch for the currently execution, and it gets part of fetched results, and creates and returns the ResultSet. JDBC specification defines to call this method once per the execution, but it is implemented to return the same object for several calls of the method.
- Exception: If the statement is already closed, it throws an exception. If an error occurs on the server when fetching, it throws an exception.

<a id="efe5204fed5bd7d5"></a>
#### getResultSetConcurrency

```
int getResultSetConcurrency() throws SQLException
```

- Operation: It returns the ResultSet concurrency. The value determines the concurrency of ResultSet generated from the object. The default value is ResultSet.CONCUR_READ_ONLY. The updatable cursor is not yet supported.
- Exception: If the statement is already closed, it throws an exception.

<a id="c73cd913a7c66c4b"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- Operation: It returns the ResultSet holdability. The value determines the holdability of ResultSet generated from the object. The default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If the statement is already closed, it throws an exception.

<a id="1c575c09ca59adb4"></a>
#### getResultSetType

```
int getResultSetType() throws SQLException
```

- Operation: It returns the ResultSet type. The value determines the type of ResultSet generated from the object. The default value is ResultSet.TYPE_FORWARD_ONLY.
- Exception: If the statement is already closed, it throws an exception.

<a id="d4ac56d78bb61e1d"></a>
#### getUpdateCount

```
int getUpdateCount() throws SQLException
```

- Operation: It returns the number of rows in which the update for the last execution is reflected. If the last executed SQL statement is not UPDATE statement nor is INSERT statement, it returns -1.
- Exception: It does not occur.

<a id="c283d0b4b8919d74"></a>
#### getUpdateRowCount

```
long getUpdateRowCount() throws SQLException
```

- Operation: It is as same as getUpdateCount, but the returned type is long. It is non-standard method, and the type casting to GoldilocksStatement should be performed to use it.
- Exception: It does not occur.

<a id="69c2dcd616e51fe4"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns SQLWarning accumulated on the object. If it does not exist, it returns null.
- Exception: It does not occur.

<a id="b05f00709c4ee8b8"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- Operation: It returns whether the statement is closed. If it is closed, it returns true. Otherwise, it returns false. It can be closed not only by the explicit call of close() but also by the server or the connection object.
- Exception: It does not occur.

<a id="d2accbcb9bbe46fd"></a>
#### isPoolable

```
boolean isPoolable() throws SQLException
```

- Operation: Statement pooling is not supported. It always returns false.
- Exception: It does not occur.

<a id="13f425202f69196f"></a>
#### setCursorName

```
void setCursorName(String name) throws SQLException
```

- Operation: It sets a name for the cursor created by the currently executed statement.
- Exception: If an error occurs on the server when setting the cursor name, it throws an exception.

<a id="e512fcff8e64e147"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

- Operation: JDBC can not ban the feature because the escape processing of the SQL statement is performed in the server parser. Any operation is not performed.
- Exception: If the statement is already closed, it throws an exception.

<a id="38aa543775960002"></a>
#### setExplainPlanOption

```
void setExplainPlanOption(int option) throws SQLException
```

- Operation: It is non standard method, but it is the GoldilocksStatement unique method. It specifies the plan text generation options. The option should be set to one of the followings, and each meaning is as follows.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF: The plan text is not generated.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON: The plan text is generated when executing.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON_VERBOSE: Detailed plan text is generated when executing.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ONLY: The plan text is generated when executing, but the actual execution is not performed.
- Exception: When setting a value other than four values above, it throws an exception.

<a id="7b23cdc7272123d0"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- Operation: It sets the fetch direction. If the direction is not ResultSet.FETCH_FORWARD, it throws an exception because GOLDILOCKS supports only the forward fetch.
- Exception: If the statement is already closed or the direction is not FETCH_FORWARD, it throws an exception.

<a id="cc091779e0443738"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- Operation: It sets the default fetch size of ResultSet which is got from the statement object. The default value is 0, and 0 refers that the server determines the number of fetched rows. For more information, refer to [setFetchSize](#0c61a2d262f43960) of ResultSet.
- Exception: If the statement is already closed, it throws an exception.

<a id="e37eac53e8a93065"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

- Operation: It sets the max field size. The value limits the maximum length of the column. If the column value is bigger than this length when fetching, the rest of the data is truncated. The default value is 0, 0 refers that the maximum length is infinity. It is valid for CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, LONG VARBINARY types.
- Exception: If the statement is already closed, it throws an exception.

<a id="c958e77937eca0e7"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

- Operation: It sets the max rows. The max rows refers to the maximum number of rows of ResultSet which is got from the statement. The rows more than the maximum number of rows are ignored. The default is 0, and 0 means infinity.
- Exception: If the statement is already closed, it throws an exception.

<a id="5e6f18d03fec9d9f"></a>
#### setPoolable

```
void setPoolable(boolean poolable) throws SQLException
```

- Operation: Statement pooling is not supported. Any operation is not performed.
- Exception: It does not occur.

<a id="889c63e3b0d2f8e5"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

- Operation: It sets the value of query timeout. The value is the timeout value which the sever applies at the execution, and the execution is canceled and the user gets the error related to timeout if the execution time exceeds the time. The unit is seconds and it applies the default value of the session if the user idoes not specifically set it. The default value of the session is 0 if it is not set with the property, and 0 refers to the infinite wait.
- Exception: If the statement is already closed, it throws an exception.

<a id="14b84d0ffd9e59e4"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether the object is a class which implements the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper but it only queries only whether the given argument class type is implemented because GOLDILOCKS statement object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="760e032bff82b422"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS statement is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of the object (when this object returns the unimplemented type), it throws SQLException.

<a id="348ff4c92407a51d"></a>
### Struct

The class is not implemented.

<a id="70851ba373c42dfb"></a>
#### getAttributes

```
Object[] getAttributes() throws SQLException
```

<a id="6b5e31cf7d5bb2b7"></a>
#### getAttributes

```
Object[] getAttributes(Map<String,Class<?>> map) throws SQLException
```

<a id="a8cc22eb3e0568f3"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="0300d26f9ce00f53"></a>
### XAConnection

<a id="02fab622ad45b4d5"></a>
#### getXAResource

```
XAResource getXAResource() throws SQLException
```

- Operation: It returns XAResource object which can perform XA command. When the method is called for several times, the same result is continuously returned.
- Exception: It does not occur.

<a id="f40c065c030427ff"></a>
### XADataSource

<a id="a5792cb1a3da435d"></a>
#### getXAConnection

```
XAConnection getXAConnection() throws SQLException
```

- Operation: It creates XAConnection object and returns it. The information required for the connection should be set as the separate non-standard methods in advance.
- Exception: When connection to the server is failed, it throws SQLException.

```
XAConnection getXAConnection(String user, String password) throws SQLException
```

- Operation: It opens and returns a new XAConnection object with the username and password. Other information required for the connection should be set as the separate non-standard methods in advance.
- Exception: When connection to the server is failed, it throws SQLException.

<a id="593d9cafa29d8c6e"></a>
### XAResource

<a id="a91e7fefdd7b36ca"></a>
#### commit

```
void commit(Xid xid, boolean onePhase) throws XAException
```

- Operation: It performs the XA commit command for the global transaction xid. If onePhase is set to true, one phase commit is performed.
- Exception: If the execution result error occurs, it throws XAException.

<a id="9d392574642eca84"></a>
#### end

```
void end(Xid xid, int flags) throws XAException
```

- Operation: It performs the XA end command for the global transaction xid. The flags may be one of TMSUCCESS, TMFAIL, or TMSUSPEND.
- Exception: If the execution result error occurs, it throws XAException.

<a id="5d845a849b006481"></a>
#### forget

```
void forget(Xid xid) throws XAException
```

- Operation: It performs the XA forget command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="1da0fdd61dbf296f"></a>
#### getTransactionTimeout

```
int getTransactionTimeout() throws XAException
```

- Operation: GOLDILOCKS does not support the transaction timeout. It always return 0.
- Exception: It does not occur.

<a id="0647d838b525dd70"></a>
#### isSameRM

```
boolean isSameRM(XAResource xares) throws XAException
```

- Operation: It has the unique rmid when XAResource object is created. Whether it is the same XAResource object is determined with this rmid.
- Exception: It does not occur.

<a id="4f09d9518828e9d8"></a>
#### prepare

```
int prepare(Xid xid) throws XAException
```

- Operation: It performs the XA prepare command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="58d749875cf8eb1c"></a>
#### recover

```
Xid[] recover(int flag) throws XAException
```

- Operation: It performs XA recover command with the given flag, and the array of the prepared transaction branches is returned. The flag may be one of TMSTARTRSCAN, TMENDRSCAN, TMNOFLAGS.
- Exception: If the execution result error occurs, it throws XAException.

<a id="0c90582855e52444"></a>
#### rollback

```
void rollback(Xid xid) throws XAException
```

- Operation: It performs the XA rollback command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="d0742a4bd0b10463"></a>
#### setTransactionTimeout

```
boolean setTransactionTimeout(int seconds) throws XAException
```

- Operation: GOLDILOCKS does not support the transaction timeout. Any operation is not performed.
- Exception: It does not occur.

<a id="19cb03bd1735d9cf"></a>
#### start

```
void start(Xid xid, int flags) throws XAException
```

- Operation: It starts the global transaction with the given flag. The flag may be one of TMNOFLAGS, TMJOIN, TMRESUME.
- Exception: If the execution result error occurs, it throws XAException.

<a id="17d473bca9c2891a"></a>
### GoldilocksInterval

To give value to a column of GOLDILOCKS by using a GoldilocksInterval object, refer to [Using Other Data Types](#eb039cd34b72969b).

<a id="b85ac9ad29f4856c"></a>
#### createIntervalYear

```
public static GoldilocksInterval createIntervalYear(int yearPrecision, boolean sign, int year) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given year value. The yearPrecision refers to the number of digits which the year can have. The value of year should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given year value exceeds yearPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalYear(int yearPrecision, String year) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given year value. The yearPrecision refers to the number of digits which the year can have. The value of year should be an integer equal to or bigger than 0.
- Exception: If the given year value exceeds yearPrecision, an error occurs.

<a id="8c6750743d5c20e9"></a>
#### createIntervalMonth

```
public static GoldilocksInterval createIntervalMonth(int monthPrecision, boolean sign, int month) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given month value. The monthPrecision refers to the number of digits which the month can have. The value of month should be an integer equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given month value exceeds monthPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalMonth(int monthPrecision, String month) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given month value. The monthPrecision refers to the number of digits which the month can have. The value of month should be an integer equal to or bigger than 0.
- Exception: If the given month value exceeds monthPrecision, an error occurs.

<a id="7b09b038644ac5f7"></a>
#### createIntervalYearToMonth

```
public static GoldilocksInterval createIntervalYearToMonth(int yearPrecision, boolean sign, int year, int month) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given year, month value. The yearPrecision refers to the number of digits which the year can have. The value of year, month should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given year value exceeds yearPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalYearToMonth(int yearPrecision, String yearToMonth) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given yearToMonth value. The yearPrecision refers to the number of digits which the year can have. yearToMonth should satisfy "yy-mm" pattern.
- Exception: If the given year value exceeds yearPrecision, an error occurs.

<a id="61317535144f89cd"></a>
#### createIntervalDay

```
public static GoldilocksInterval createIntervalDay(int dayPrecision, boolean sign, int day) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day value. The dayPrecision refers to the number of digits which the day can have. The value of day should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given day value exceeds dayPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalDay(int dayPrecision, String day) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day value. The dayPrecision refers to the number of digits which the day can have. The value of day should be an integer equal to or bigger than 0.
- Exception: If the given day value exceeds dayPrecision, an error occurs.

<a id="af6b98ae7bcb4aa5"></a>
#### createIntervalHour

```
public static GoldilocksInterval createIntervalHour(int hourPrecision, boolean sign, int hour) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hour value. The hourPrecision refers to the number of digits which the hour can have. The value of hour should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given hour value exceeds hourPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalHour(int hourPrecision, String hour) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hour value. The hourPrecision refers to the number of digits which the hour can have. The value of hour should be an integer equal to or bigger than 0.
- Exception: If the given hour value exceeds hourPrecision, an error occurs.

<a id="2652d86fcda2d42b"></a>
#### createIntervalMinute

```
public static GoldilocksInterval createIntervalMinute(int minutePrecision, boolean sign, int minute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given minute value. The minutePrecision refers to the number of digits which the minute can have. The value of minute should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given minute value exceeds minutePrecision, an error occurs.

```
public static GoldilocksInterval createIntervalMinute(int minutePrecision, String minute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given minute value. The minutePrecision refers to the number of digits which the minute can have. The value of minute should be an integer equal to or bigger than 0.
- Exception: If the given minute value exceeds minutePrecision, an error occurs.

<a id="edad58b9ff97d6fb"></a>
#### createIntervalSecond

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, boolean sign, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given second value. The secondPrecision refers to the number of digits of second, and the fractionalPrecision refers to the number of digits of microsecond. The value of second and microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the given second value exceeds secondPrecision or the given microSecond value exceeds fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute, second, microsecond value. The secondPrecision refers to the number of digits of second when day, hour, minute, second is converted to second. The fractionalPrecision refers to the number of digits of microsecond. The value of day, hour, minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the converted second value exceeds the secondPrecision or the microSecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, String second) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given second string. The secondPrecision refers to the number of digits of second. The fractionalPrecision refers to the number of digits of microsecond. The second string should be one of "dd hh:mm:ss.ffffff" or "dd hh:mm:ss", "dd hh:mm", "dd hh", "hh:mm", "ss.ffffff", "ss" patterns.
- Exception: If the converted second value exceeds the secondPrecision or the microSecond value exceeds the fractionalPrecision, an error occurs. If the string does not conform to the prescribed format, an error occurs.

<a id="224bc2e823541a48"></a>
#### createIntervalDayToHour

```
public static GoldilocksInterval createIntervalDayToHour(int dayPrecision, boolean sign, int day, int hour) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour value. The dayPrecision refers to the number of digits of day. The value of day, hour should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the day value exceeds dayPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalDayToHour(int dayPrecision, String dayToHour) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given dayToHour string. The dayPrecision refers to the number of digits of day. dayToHour should satisfy "dd hh" format. Or, if its format is "dd hh:mm:ss", all should be 0 except for dd, hh.
- Exception: If the day value exceeds dayPrecision or the given string does not satisfy the format, an error occurs.

<a id="667e9284dbcb7778"></a>
#### createIntervalDayToMinute

```
public static GoldilocksInterval createIntervalDayToMinute(int dayPrecision, boolean sign, int day, int hour, int minute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute value. The dayPrecision refers to the number of digits of day. The value of day, hour, minute should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the day value exceeds dayPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalDayToMinute(int dayPrecision, String dayToMinute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given dayToMinute string. The dayPrecision refers to the number of digits of day. dayToMinute should satisfy "dd hh:mm" format. Or, if its format is "dd hh:mm:ss", all should be 0 except for dd, hh, mm.
- Exception: If the day value exceeds dayPrecision or the given string does not satisfy the format, an error occurs.

<a id="21bd0136fb425d25"></a>
#### createIntervalDayToSecond

```
public static GoldilocksInterval createIntervalDayToSecond(int dayPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute, second, microsecond value. The dayPrecision refers to the number of digits of day. The fractionalPrecision refers to the number of digits of microsecond. The value of day, hour, minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the day value exceeds dayPrecision or the microsecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalDayToSecond(int dayPrecision, String dayToSecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given dayToSecond string. The dayPrecision refers to the number of digits of day. The fractionalPrecision refers to the number of digits of microsecond. dayToSecond should satisfy one of "dd hh:mm:ss.ffffff", "dd hh:mm:ss", "hh:mm:ss", "hh:mm" formats.
- Exception: If the day value or the converted day value exceeds dayPrecision or the microsecond value exceeds the fractionalPrecision or the given string does not satisfy the format, an error occurs.

<a id="9d8160ea3afd5ef3"></a>
#### createIntervalHourToMinute

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, boolean sign, int hour, int minute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hour, minute value. The hourPrecision refers to the number of digits of hour. The value of hour, minute should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the hour value exceeds hourPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, boolean sign, int day, int hour, int minute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute value. The hourPrecision refers to the number of digits of hour. The value of day, hour, minute should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the hour value or the converted hour value exceeds hourPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, String hourToMinute) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hourToMinute string. The hourPrecision refers to the number of digits of hour. hourToMinute must satisfy "hh:mm" format. The value of ss or ffffff should be 0 for other formats.
- Exception: If the hour value or the converted hour value exceeds hourPrecision, an error occurs. If the given string does not satisfy the format, an error occurs.

<a id="9fdabf75c1a9bdbb"></a>
#### createIntervalHourToSecond

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, boolean sign, int hour, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hour, minute, second, microsecond value. The hourPrecision refers to the number of digits of hour. The fractionalPrecision refers to the number of digits of microsecond. The value of hour, minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the hour value exceeds hourPrecision or the microsecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute, second, microsecond value. The hourPrecision refers to the number of digits of hour. The fractionalPrecision refers to the number of digits of microsecond. The value of day, hour, minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the hour value or the converted hour value exceeds hourPrecision or the microsecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, String hourToSecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given hourToSecond string. The hourPrecision refers to the number of digits of hour. The fractionalPrecision refers to the number of digits of microsecond. hourToSecond should satisfy "hh:mm:ss.ffffff", "hh:mm:ss", or "hh:mm" format. If dd is included, the value of converted hour should not exceed hourPrecision.
- Exception: If the hour value or the converted hour value exceeds hourPrecision or the microsecond value exceeds the fractionalPrecision, or the given string does not satisfy the format, an error occurs.

<a id="b4c337a62213583e"></a>
#### createIntervalMinuteToSecond

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, boolean sign, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given minute, second, microsecond value. The minutePrecision refers to the number of digits of minute. The fractionalPrecision refers to the number of digits of microsecond. The value of minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the minute value exceeds the minutePrecision or the microsecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given day, hour, minute, second, microsecond value. The minutePrecision refers to the number of digits of minute. The fractionalPrecision refers to the number of digits of microsecond. The value of day, hour, minute, second, microsecond should be equal to or bigger than 0. If the time is a positive number, sign is true. If it is a negative number, sign is false.
- Exception: If the minute value or the converted minute value exceeds minutePrecision or the microsecond value exceeds the fractionalPrecision, an error occurs.

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, String minuteToSecond) throws SQLException
```

- Operation: It creates GoldilocksInterval object with the given minuteToSecond string. The minutePrecision refers to the number of digits of minute. The fractionalPrecision refers to the number of digits of microsecond. minuteToSecond should satisfy "mm:ss.ffffff" or "mm:ss" format. If dd or hh is included, the value of the converted minute should not exceed minutePrecision.
- Exception: If the minute value or the converted minute value exceeds the minutePrecision or the microsecond value exceeds the fractionalPrecision or the given string does not satisfy the format, an error occurs.

<a id="83d56aed91d9e82d"></a>
#### getSign

```
public int getSign()
```

- Operation: If the time is a positive number, 1 is returned. If the time is a negative number, -1 is returned.
- Exception: It does not occur.

<a id="e6a9a5d37f6efb64"></a>
#### getYear

```
public int getYear()
```

- Operation: It returns the year value. Whether the interval object is a negative number is not returned through getYear().
- Exception: It does not occur.

<a id="fd2cfd39d42d0cf8"></a>
#### getMonth

```
public int getMonth()
```

- Operation: It returns the month value. Whether the interval object is a negative number is not returned through getMonth().
- Exception: It does not occur.

<a id="c8261144a05a4f1a"></a>
#### getAccumulatedMonth

```
public int getAccumulatedMonth()
```

- Operation: It converts the value of year and month to the value of month, and returns the result.
- Exception: It does not occur.

<a id="8f520278792bce36"></a>
#### getDay

```
public int getDay()
```

- Operation: It returns the day value. Whether the interval object is a negative number is not returned through getDay().
- Exception: It does not occur.

<a id="9650c17b60281c19"></a>
#### getHour

```
public int getHour()
```

- Operation: It returns the hour value. Whether the interval object is a negative number is not returned through getHour().
- Exception: It does not occur.

<a id="e1316f98a94d6866"></a>
#### getAccumulatedHour

```
public int getAccumulatedHour()
```

- Operation: It converts the value of day and hour to the value of hour, and returns the result.
- Exception: It does not occur.

<a id="e4e1fb8d172a54b5"></a>
#### getMinute

```
public int getMinute()
```

- Operation: It returns the minute value. Whether the interval object is a negative number is not returned through getMinute().
- Exception: It does not occur.

<a id="0750cc0e772ef0e2"></a>
#### getAccumulatedMinute

```
public int getAccumulatedMinute()
```

- Operation: It converts the value of day, hour and minute to the value of minute, and returns the result.
- Exception: It does not occur.

<a id="d7d44a87700f68e6"></a>
#### getSecond

```
public int getSecond()
```

- Operation: It returns the second value. Whether the interval object is a negative number is not returned through getSecond().
- Exception: It does not occur.

<a id="25d38f0929a3ba66"></a>
#### getAccumulatedSecond

```
public int getAccumulatedSecond()
```

- Operation: It converts the value of day, hour, minute and second to the value of second, and returns the result.
- Exception: It does not occur.

<a id="79513ccb74988469"></a>
#### getMicroSecond

```
public int getMicroSecond()
```

- Operation: It returns the microsecond value. Whether the interval object is a negative number is not returned through getMicroSecond().
- Exception: It does not occur.

<a id="620299376e227e49"></a>
#### getAccumulatedMicroSecond

```
public long getAccumulatedMicroSecond()
```

- Operation: It converts the value of day, hour, minute, second and microsecond to the value of microsecond, and returns the result.
- Exception: It does not occur.

<a id="04469735818e83f9"></a>
#### getTypeName

```
public String getTypeName()
```

- Operation: The type name is returned.
- Exception: It does not occur.

<a id="5518c56d842586ec"></a>
#### getSqlType

```
public int getSqlType()
```

- Operation: The type of this object is returned as the type constant defined in GoldilocksTypes.
- Exception: It does not occur.

<a id="6c26495a670d98fc"></a>
#### toString

```
public String toString()
```

- Operation: The interval value which is indicated by this object is returned as a string value.
- Exception: It does not occur.

<a id="68c2eeb8a25bab2e"></a>
### GOLDILOCKS Type

<a id="28c07deb75c4243c"></a>
#### Constant Definition

```
public static final int INTERVAL_YEAR;
public static final int INTERVAL_MONTH;
public static final int INTERVAL_DAY;
public static final int INTERVAL_HOUR;
public static final int INTERVAL_MINUTE;
public static final int INTERVAL_SECOND;
public static final int INTERVAL_YEAR_TO_MONTH;
public static final int INTERVAL_DAY_TO_HOUR;
public static final int INTERVAL_DAY_TO_MINUTE;
public static final int INTERVAL_DAY_TO_SECOND;
public static final int INTERVAL_HOUR_TO_MINUTE;
public static final int INTERVAL_HOUR_TO_SECOND;
public static final int INTERVAL_MINUTE_TO_SECOND;
public static final int TIME_WITH_TIME_ZONE;
public static final int TIMESTAMP_WITH_TIME_ZONE;
```

These constants are used like as the constants of java.sql.Types. In other words, they are used when specifying the types in setObject of PreparedStatement or the types in getObject of ResultSet. These types are separately provided by GoldilocksTypes because they are not defined in the JDBC standard.

<a id="d731cb3fcbb0bdbe"></a>
### Type Conversion

The following tables describe how to convert types.

**SQL types → GOLDILOCKS types**

<a id="cb02001a30776570"></a>
| SQL type | GOLDILOCKS type |
| --- | --- |
| Types.BIGINT | NATIVE_BIGINT |
| Types.BINARY | BINARY(2000) |
| Types.BIT | BOOLEAN |
| Types.BOOLEAN | BOOLEAN |
| Types.BLOB | N/A |
| Types.CHAR | CHAR(2000) |
| Types.CLOB | N/A |
| Types.DATE | DATE |
| Types.DECIMAL | DECIMAL |
| Types.DOUBLE | NATIVE_DOUBLE |
| Types.FLOAT | FLOAT |
| Types.NUMERIC | NUMBER |
| Types.INTEGER | NATIVE_INTEGER |
| Types.LONGVARBINARY | LONG VARBINARY |
| Types.LONGVARCHAR | LONG VARCHAR |
| Types.REAL | NATIVE_REAL |
| Types.ROWID | ROWID |
| Types.SMALLINT | NATIVE_SMALLINT |
| Types.TIME | TIME |
| Types.TIMESTAMP | TIMESTAMP |
| Types.VARBINARY | VARBINARY(4000) |
| Types.VARCHAR | VARCHAR(4000) |
| GoldilocksTypes.INTERVAL_YEAR | INTERVAL YEAR |
| GoldilocksTypes.INTERVAL_MONTH | INTERVAL MONTH |
| GoldilocksTypes.INTERVAL_YEAR_TO_MONTH | INTERVAL YEAR TO MONTH |
| GoldilocksTypes.INTERVAL_DAY | INTERVAL DAY |
| GoldilocksTypes.INTERVAL_HOUR | INTERVAL HOUR |
| GoldilocksTypes.INTERVAL_MINUTE | INTERVAL MINUTE |
| GoldilocksTypes.INTERVAL_SECOND | INTERVAL SECOND |
| GoldilocksTypes.INTERVAL_DAY_TO_HOUR | INTERVAL DAY TO HOUR |
| GoldilocksTypes.INTERVAL_DAY_TO_MINUTE | INTERVAL DAY TO MINUTE |
| GoldilocksTypes.INTERVAL_DAY_TO_SECOND | INTERVAL DAY TO SECOND |
| GoldilocksTypes.INTERVAL_HOUR_TO_MINUTE | INTERVAL HOUR TO MINUTE |
| GoldilocksTypes.INTERVAL_HOUR_TO_SECOND | INTERVAL HOUR TO SECOND |
| GoldilocksTypes.INTERVAL_MINUTE_TO_SECOND | INTERVAL MINUTE TO SECOND |
| Types.OTHER | N/A |
| Types.ARRAY | N/A |
| Types.DATALINK | N/A |
| Types.DISTINCT | N/A |
| Types.NCHAR | N/A |
| Types.NCLOB | N/A |
| Types.NVARCHAR | N/A |
| Types.JAVA_OBJECT | N/A |
| Types.REF | N/A |
| Types.SQLXML | N/A |
| Types.STRUCT | N/A |

**Whether supporting getter method for GOLDILOCKS type - 1**

<a id="fa62c08a45390115"></a>
|  | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| getByte | O | O | O | O | O |
| getShort | O | O | O | O | O |
| getInt | O | O | O | O | O |
| getLong | O | O | O | O | O |
| getFloat | O | O | O | O | O |
| getDouble | O | O | O | O | O |
| getBigDecimal | O | O | O | O | O |
| getBoolean | Avaliable only for 0,1 | Avaliable only for 0,1 | Avaliable only for 0,1 | Avaliable only for 0,1 | Avaliable only for 0,1 |
| getString | O | O | O | O | O |
| getBytes | raw data | raw data | raw data | raw data | raw data |
| getDate | X | X | X | X | X |
| getTime | X | X | X | X | X |
| getTimestamp | X | X | X | X | X |
| getAsciiStream | raw data | raw data | raw data | raw data | raw data |
| getBinaryStream | raw data | raw data | raw data | raw data | raw data |
| getCharacterStream | X | X | X | X | X |
| getClob | X | X | X | X | X |
| getBlob | X | X | X | X | X |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Short | Integer | Long | Float | Double |
| getRowId | X | X | X | X | X |

**Whether supporting getter method for GOLDILOCKS Type - 2**

<a id="75b32d4b17e2fc78"></a>
|  | BOOLEAN | FLOAT/ NUMBER | CHAR/ VARCHAR/ LONG VARCHAR | BINARY/ VARBINARY/LONG VARBINARY | ROWID |
| --- | --- | --- | --- | --- | --- |
| getByte | 0 or 1 | O | Available only for numeric | X | X |
| getShort | 0 or 1 | O | Available only for numeric | X | X |
| getInt | 0 or 1 | O | Available only for numeric | X | X |
| getLong | 0 or 1 | O | Available only for numeric | X | X |
| getFloat | 0 or 1 | O | Available only for numeric | X | X |
| getDouble | 0 or 1 | O | Available only for numeric | X | X |
| getBigDecimal | 0 or 1 | O | Available only for numeric | X | X |
| getBoolean | O | Available only for 0,1 | Available only for "t", "f", "true", "false", "y", "n", "yes", "no", "on", "off", "1", "0" (case-insensitive) | X | X |
| getString | "TRUE" or "FALSE" | O | O | O | O |
| getBytes | raw data | raw data | raw data | O | raw data |
| getDate | X | X | Available only for date format | X | X |
| getTime | X | X | Available only for time format | X | X |
| getTimestamp | X | X | Available only for timestamp format | X | X |
| getAsciiStream | raw data | raw data | raw data | O | raw data |
| getBinaryStream | raw data | raw data | raw data | O | raw data |
| getCharacterStream | X | X | O | X | X |
| getClob | X | X | X | X | X |
| getBlob | X | X | X | X | X |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Boolean | BigDecimal | String | byte[] | RowId |
| getRowId | X | X | X | X | O |

**Whether supporting getter method for GOLDILOCKS Type - 3**

<a id="86f96925735092de"></a>
|  | DATE | TIME/ TIME WITH TIME ZONE | TIMESTAMP/ TIMESTAMP WITH TIME ZONE | INTERVAL |
| --- | --- | --- | --- | --- |
| getByte | X | X | X | Available only for a single item type |
| getShort | X | X | X | Available only for a single item type |
| getInt | X | X | X | Available only for a single item type |
| getLong | X | X | X | Available only for a single item type |
| getFloat | X | X | X | Available only for a single item type |
| getDouble | X | X | X | Available only for a single item type |
| getBigDecimal | X | X | X | Available only for a single item type |
| getBoolean | X | X | X | X |
| getString | O | O | O | O |
| getBytes | raw data | raw data | raw data | raw data |
| getDate | O | O | O | X |
| getTime | O | O | O | X |
| getTimestamp | O | O | O | X |
| getAsciiStream | raw data | raw data | raw data | raw data |
| getBinaryStream | raw data | raw data | raw data | raw data |
| getCharacterStream | X | X | X | X |
| getClob | X | X | X | X |
| getBlob | X | X | X | X |
| getArray | X | X | X | X |
| getRef | X | X | X | X |
| getURL | X | X | X | X |
| getObject | Date | Time | Timestamp | GoldilocksInterval |
| getRowId | X | X | X | X |

---

[← 25. ODBC](25-odbc.md) · [Table of contents](../README.md) · [27. Embedded SQL →](27-embedded-sql.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
