<a id="d1174d6cbc66ce69"></a>

# 32. JDBC

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/d1174d6cbc66ce69)  
> Tag: `21c.1_35_tag`

[← 31. ODBC](31-odbc.md) · [Table of contents](../README.md) · [33. Embedded SQL →](33-embedded-sql.md)

<a id="49907babfb60ab57"></a>
## Overview of GOLDILOCKS JDBC Driver

<a id="9165707183207a1b"></a>
### Concepts of GOLDILOCKS JDBC Driver

GOLDILOCKS provides GOLDILOCKS JDBC driver (excluding some features) which complies with standard JDBC 4.0 based on TCP/IP connection. The user can use various transaction features and data query features by using GOLDILOCKS JDBC driver and connecting to GOLDILOCKS in Java program. GOLDILOCKS JDBC driver is written and built based on JDK 1.6. Therefore, it supports JDBC 4.0 features. The driver can be used by adding $GOLDILOCKS_HOME/lib/goldilocks6.jar file to the class path.

The number after goldilocks refers to the JDK version. For more information, refer to [Supporting Versions](#5fb122abc3f8f46e).

GOLDILOCKS JDBC complies with most of JDBC standard specifications, and it also supports non-standard API methods and classes to provide some unique features. For more information about non-standard methods, refer to each class API of [JDBC API References](#0290b5f7e2462758) or [Using Other Data Types](#ffdc3b15ea1df333).

<a id="7ee8fbe9009cce44"></a>
### Characteristics

- **• Type-4 JDBC Driver:** 

GOLDILOCKS JDBC is a JDBC Type-4 type which is implemented only with pure Java. A user can use a JDBC driver only with jar file without any additional libraries. Also, it is faster and reliable than JDBC-ODBC Bridge type, and it has better portability than Type-2 using Native API.

- **• JDBC Standard Compliance:** 

GOLDILOCKS JDBC can recycle most of other existing JDBC programs without changing because it complies with the JDBC standard. The connection, various statements and ResultSet features can be used without modifying. However, the connection URL and property name, the name of driver class to be loaded should be changed to suit GOLDILOCKS. And the non-standard features and types are usable with the separate classes and methods API.

- **• Supporting Various Java Versions:** 

GOLDILOCKS JDBC driver supports three files such as goldilocks8.jar, goldilocks7.jar, goldilocks6.jar, so that a user can select and use the file appropriate for user's Java run-time environment. Because each jar file was built based on JDK 1.8, JDK 1.7, JDK 1.6, it complies with each JDBC 4.2, JDBC 4.1, JDBC 4.0 specifications.

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

Various logging features are provided to monitor the usual JDBC API calls and network usage as well as the problem. If the logging-related features are specified in the connection URL, a user can leave a the content log to the console or files. Four types of logging exist, which are logging for JDBC method call recording, logging for protocol sending and receiving, logging for the SQL statement used, logging for global connection usage.

- **• Connection Failover:** 

Connection failover is supported on JDBC driver level to continuously use an existing connection by automatically reconnecting to the previously registered alternate server when the connection with the execution GOLDILOCKS server fails or is disconnected. A user can use connection failover feature as an existing JDBC program without any exception handling in preparation for the broken connection.

- **• Connectivity between server and direct attach:** 

Other than TCP/IP based connection, it can be connected with direct attach method interworking with a process as same as the server. Like as ODBC connection supports direct attach method and Client/ Server method, GOLDILOCKS JDBC driver also provides both methods. JDBC program connected with direct attach does not communicate with TCP/IP, but it can use the server features in jvm by directly interworking with the server process. The perfomance is doubled or more than the JDBC program connected with TCP/ IP.

<a id="5fb122abc3f8f46e"></a>
### Supporting Versions

<a id="26461c702beac67e"></a>
#### GOLDILOCKS JDBC versions

GOLDILOCKS JDBC version information can be viewed when executing goldilocks6.jar file as follows.

```
shell>java -jar goldilocks6.jar

 GOLDILOCKS JDBC Driver 1.1 Procotol-2.5.2, JDBC4.0 compiled with JDK1.6
```

The examples above describe that current GOLDILOCKS JDBC driver version is 1.1, and the protocol version is 2.5.2, and JDBC standard version is 4.0 and it is built in JDK 1.6. The driver version is displayed apart from GOLDILOCKS product version, and it goes up whenever the function is strengthened. For more information about JDBC driver version, refer to [getDriverMajorVersion](#984bcce26afb55f6), [getDriverMinorVersion](#620c1d93d9c48e4e), [getDriverVersion](#53a22acb285785d4) of DatabaseMetaData.

Protocol version determines compatibility with the server, and the driver can interwork with the server if the version is equal to or lower than the server protocol version. The server supports all clients API of the lower protocol version.

goldilocks6.jar complies with JDBC 4.0 standard and it was built in JDK 1.6. goldilocks7.jar complies with JDBC 4.1 standard and it was built in JDK 1.7. goldilocks8.jar complies with JDBC 4.2 standard and it was built in JDK 1.8. Therefore, if the user's java environment is higher than JDK 1.8, use goldilocks8.jar. However, when using Java JDK 1.9 or higher, goldilocks8.jar can be used but API or classes of JDBC 4.3 can not be used.

<a id="2a5ac8c97ef9b86b"></a>
### Examples

<a id="39e438bc6fd15be3"></a>
#### Setting Class Path

CLASSPATH should be set to use GOLDILOCKS JDBC driver.

```
export CLASSPATH=.:$GOLDILOCKS_HOME/lib/goldilocks6.jar
```

Or, add a suitable jar file for the user's Java execution environment to the path.

<a id="ed6a704fd0db7bdd"></a>
#### Loading Driver Class

The driver class can be loaded as follows.

```
Class.forName("sunje.goldilocks.jdbc.GoldilocksDriver");
```

The example above is the conventional method of using JDBC, and it is the method of dynamically loading the driver class and registering in DriverManager and getting the connection. Nowadays, the way to get the connection through DataSource is used more. For more information, refer to the corresponding class in [JDBC API References](#0290b5f7e2462758).

<a id="bec1576b76d80a37"></a>
#### Getting Connection

The following code is used to get the connection.

```
Connection con = DriverManager.getConnection(
    "jdbc:goldilocks://127.0.0.1:22581/test", "TEST", "test");
```

The connection URL should be started with "jdbc:goldilocks:" to use GOLDILOCKS JDBC. The next is the IP address and port number of the server and "/test" which is the final part of URL is the DB name. The current GOLDILOCKS does not specifically check the DB name because it does not support multi DB. A user connected URL may be obtained again through DatabaseMetaData.getURL().

It connects in Direct Attach (D/A) mode when setting IP to 0.0.0.0, and a port to 0. Or, the connecting protocol, *da*, can be used instead of ip:port. In other words, both of the following two URL enables connecting in DA mode.

```
"jdbc:goldilocks://0.0.0.0:0/test"
"jdbc:goldilocks:da/test"
```

Username and password should respectively use the account and password for DB.

<a id="5d2b35e7f2b5e6ca"></a>
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

<a id="f1042294f81f7dd0"></a>
## Feature Specification

<a id="3a6a0e51fa65e3b3"></a>
### Connection

<a id="526e4110e12b0f38"></a>
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

The host name, IPv4 and IPv6 are available for IP address, and port_no refers to the port number set. db_name is not used for the current connection so it can have any name. However, it can not be omitted. The following is an example of URL.

```
String url_string = "jdbc:goldilocks://localhost:22581/test";
```

```
String url_string = "jdbc:goldilocks://127.0.0.1:22581/test";
```

```
String url_string = "jdbc:goldilocks://[::1]:22581/test";
```

IP "0.0.0.0" and port 0 are used as a special address for D/A connection. For more information about D/A mode, refer to [Direct Attach Mode Connection](#8429ee4c8080d90d).

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

The property list which can be used for the connection is known through getPropertyInfo() method of GoldilocksDriver. For more information, refer to [Connection property](#00de0770e9a7490d).

The login timeout of the connection object which is created by DriverManager and the logger uses the value registered in DriverManager. The logger is used by all JDBC interfaces generated from the connection object. Each connection object is not allowed to have an individual logger.

<a id="d6e0e9d7af0bdbac"></a>
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

Then, various connection information should use setter method which is not DataSource standard API.For more information, refer to [DataSource](#4d253460259583ae).

When using DriverManager, the login timeout and the logger should be globally set. However, when using DataSource, the login timeout and the logger can be individually set.

```
ds.setLoginTimeout(10);
ds.setLogWriter(out);
```

<a id="cbef462e53fe514e"></a>
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

<a id="4a69930ca736a612"></a>
#### Connection Property

**Connection property**

<a id="00de0770e9a7490d"></a>
| Name | Mandatory/ optional | Valid value | Description |
| --- | --- | --- | --- |
| alternate_servers | Optional | IP:PORT[,IP:PORT]+ | It is the list of alternate servers for failover. It is delimited by comma (,). |
| alternate_locators | Optional | IP:PORT[,IP:PORT]+ | It is the list of alternate of glocator. |
| batch_count | Optional | Any integer | It is the number of the batch jobs which can be processed in a single protocol transmission and reception. The default value is 1,000. If the value is too small, too much frequent network communication causes poor performance of the batch processing. If the value is too large, the server memory is increased because the session stacks the execution results. |
| connection_retry_count | Optional | Any integer | It stores the number of retrials to connect. The default value is 0, then it does not retry to connect. |
| connection_retry_delay | Optional | Any integer | It stores the delay before the connection retrial in seconds when trying to connect again. The default value is 3. |
| date_format | Optional | Any string | It is the character format which is used to interconvert between date and string inside the driver. |
| da_buffer_size | Optional | Any integer | It sets the size of a buffer which sends and receives data when fetching and binding while connected in direct attach mode. The default value is 100000. |
| decoding_replacement | Optional | Any string | It is the character replacing a byte value which can not be decoded when decoding a byte array into a string. The default value is ?. |
| failover_granularity | Optional | {"0", "1", "2"} | It determines whether failover is successful. non-atomic(0), atomic(1), 2 are not yet supported. When an error occurs for the existing prepared statements in the prepare process during failover, if it is 0, then it proceeds the failover, and if it is 1, it determines that the failover fails. The default value is 0. |
| failover_type | Optional | {"connection", "session"} | It determines the failover types.  * Connection: Failover is used only when connecting to server.  * Session: Failover is used when connecting to server as well as communicating with the server like execution.  The default value is session. |
| format_grammar | Optional | {"db", "java"} | It determines whether the property string such as date_format is the GOLDILOCKS syntax or the syntax used in SimpleDateFormat of java. The default value is db. |
| global_connection_log | Optional | boolean | It determines whether to perform the global connection logging. The default value is false. |
| global_logger | Optional | {"console"} | It specifies the logging target.  Currently only console is available. Only the first specified one is valid. |
| home_dir | Optional | Any string | It specifies a home directory of a cluster server. The default value is null. |
| include_synonyms | Optional | boolean | It sets whether to include the synonym object in DatabaseMetaData.getColumns(). The default value is false. |
| keep_alive | Optional | boolean | It determines whether to set the keep_alive as the socket property of the connection. Using the property, the connection remains by periodically sending and receiving ack inside TCP socket. LAN cable error detection can forcibly cut off the connection. The default value is false. |
| locality_aware_transaction | Optional | boolean | It determines whether to use GLOBAL CONNECTION. If it is set to true, then it uses GLOBAL CONNECTION. The default value is false. |
| locality_group_policy | Optional | {"0", "1", "2"} | It determines how to select a group if neither of groups are available, or two or more groups are available when using GLOBAL CONNECTION. * 0: It randomly selects the group. * 1: It sequentially selects groups which exist in LOCALITY_GROUP_PATH setting. If neither of groups in LOCALITY_GROUP_PATH are not available, it randomly selects the group. * 2: It sequentially selects groups. It always selects groups in an order of they are connected to the driver. |
| locality_group_path | Optional | Group name list | It defines the list of selected groups when the available group is not a single one when using GLOBAL CONNECTION. Each group is distinguished with comma (,). e.g. G1,G2,G3 |
| locality_member_policy | Optional | {"0","1","2","3","4"} | It determines how to select a member in the selected group when using GLOBAL CONNECTION. * 0: DML : MASTER / SELECT : MASTER * 1: DML : ANY / SELECT : ANY * 2: DML : MASTER / SELECT : ANY * 3: DML : MASTER / SELECT : SLAVE * 4: It sequentially selects members which exist in LOCALITY_MEMBER_PATH setting. If neither of members in LOCALITY_MEMBER_PATH are not available, it uses the MASTER in the selected group. |
| locality_member_path | Optional | Member name list | It defines the list of members to be used in the selected group when using GLOBAL CONNECTION. Each member is distinguished with comma (,). e.g. G1N1,G2N1,G3N1,G1N2,G2N2,G3N2 |
| locality_on_demand | Optional | boolean | It accesses to a specific member in need when using GLOBAL CONNECTION. The default value is false. * false: It accesses to all members from the beginning. * true: It accesses to a specific member when it is required. |
| locator_connection_timeout | Optional | Any integer | It is the time of waiting for receiving a packet from glocator. |
| locator_file | Optional | Any string | It is a location file. |
| locator_host | Optional | IP address | It is host address of glocator. |
| locator_port | Optional | Port no | It is port of glocator. |
| locator_service | Optional | Any string | It is the service name to obtain the server connection information. |
| login_timeout | Optional | Any integer | It sets the timeout duration (second) of the socket when connecting to the server. The default value is 0, and it indefinitely waits. |
| lzeros | Optional | Any integer | When a numeric is expressed as a string and the number of zeros following the decimal point exceeds this value, it is expressed in exponent notation. The default value is 15. |
| new_password | Optional | Any string | It can change the account password by using old_password property together. |
| old_password | Optional | Any string | It can change the account password by using new_password property together. |
| packet_compression_threshold | Optional | Any integer | It compresses the communication data to be sent to the server when the data size is bigger than packet_compression_threshold. The property range is 32 ~ 2113929216. |
| password | Mandatory | Any string | It is user account password. |
| prefer_ipv6 | Optional | boolean | It sets whether IPv6 takes precedence over other IP addresses on the host name. The default value is false. |
| program | Optional | Any string | It is program description. |
| protocol_log | Optional | boolean | It determines whether to log sending and receiving a protocol. The default value is false. |
| query_log | Optional | boolean | It determines whether to log a query.  The default value is false. |
| role | Optional | {"", "SYSDBA", "ADMIN"} | It specifies the account role. The default value is "". |
| session_type | Optional | {"1", "2", "3"} or {"dedicate", "shared", "default"} | It is one of dedicated/ shared/ default. (It is selected by DB when it is set to default.) |
| statement_pool_on | Optional | boolean | It enables the statement pool. The default value is false. |
| statement_pool_size | Optional | Any integer | It sets the size of the statement pool. |
| time_format | Optional | Any string | It is the character format which is used to interconvert between time and string inside the driver. |
| tcp_nodelay | Optional | boolean | It sets TCP_NODELAY(Nagle's Algorithm) property on the socket of the connection. The default value is true. |
| timestamp_format | Optional | Any string | It is the character format which is used to interconvert between timestamp and string inside the driver. |
| time_with_time_zone_format | Optional | Any string | It is the character format which is used to interconvert between time with timezone and string inside the driver. |
| timestamp_with_time_zone_format | Optional | Any string | It is the character format which is used to interconvert between timestamp with timezone and string inside the driver. |
| trace_log | Optional | boolean | It determines whether to log the trace. The default value is false. |
| tzeros | Optional | Any integer | When a numeric is expressed as a string and the number of zeros in digit goes beyond this value, it is expressed in exponent notation. The default value is 15. |
| user | Mandatory | Any string | It is user account name. |
| use_global_session | Optional | boolean | It is whether to use GLOBAL SESSION. The default value is false. |
| use_targettype | Optional | {"0", "1", "2"} | It is the information which is to be received together when receiving a column type through communication. * 0: none * 1: name * 2: all |


> 
> - locator_file is applied prior to locator_host and locator_port. For more information about locator_file, refer to [Location File](../part-06-utility-manual/48-gloctl.md#5a93eeebc4b5377a).
> - locator_service property enables the access to the server belonging to locator_service. For more information, refer to [glocator](../part-06-utility-manual/46-glocator.md#5c6d9f818741f0f3) and [gloctl](../part-06-utility-manual/48-gloctl.md#a4f051a64cd67b11).
> 

<a id="bd58cf1eebeb8059"></a>
### Data Manipulation

<a id="3121798063179e0c"></a>
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

<a id="2c22a18e148248b0"></a>
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

In the sample above, lines 1 ~ 2 binds java.sql.Timestamp object. The binding type (It is GOLDILOCKS type of the data when the data is sent to the server) is TIMESTAMP. For more information about the binding type which is determined by the various setter methods, refer to the corresponding API of [PreparedStatement](#197da4e8d4db3bd2).

Line 3 binds a reader object, and it is bound as LONG VARCHAR type internally.

Line 4 binds the object of Java object type, and explicitly notifies that the type is LONG VARCHAR. For more information about GOLDILOCKS type which is mapped to the type of Types, refer to [SQL types → GOLDILOCKS types](#e2eaca60f3630d26).

Line 5 literally binds the Java object type, and it is bound to the corresponding GOLDILOCKS data type according to the class type. For more information about mapping between class types and GOLDILOCKS data types, refer to [Java objects -> GOLDILOCKS types](#694f851c65f23d77).

<a id="4cc47dc5c83bbf57"></a>
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

<a id="ceb2396da6898b9d"></a>
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

<a id="8a2f9134818fb247"></a>
### Data Retrieval

<a id="c49c9c1ceb708f7b"></a>
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

The contents of the column can be obtained through various getter methods in the ResultSet after retrieving the data in the table. The data in the table is sent to JDBC drivers in the original form of GOLDILOCKS data type, and it is converted to an appropriate Java data type according to the types of getter methods called by a user and it is transmitted to the user. For more information about type conversion mapping of GOLDILOCKS data type and getter method, refer to [Whether supporting getter method for GOLDILOCKS type - 1 ](#3ad95d69b475c64d).

If GOLDILOCKS data type can not be converted to the type of getter, it throws SQLException.

<a id="c41c460605699631"></a>
#### Closing ResultSet

The ResultSet which is used up can release the resources through close(). Even if a user does not explicitly call close(), the followings bring the result as same as when calling close() of ResultSet.

- When superordinate statement is closed
- When superordinate connection is closed
- When executeQuery() of Statement is called again
- When an error occurs during fetching

The two ResultSets which are created from a single statement can not be remained simultaneously in the third case above. Only the ResultSet object which is created by the last executeQuery() is valid.

<a id="f7d29efe92e5073a"></a>
#### Fetch Size

JDBC can specify the number of rows fetched at once from the server through setFetchSize(int rows) of Statement. The default value of the ResultSet property of GOLDILOCKS is 0. 0 automatically determines the number of rows fetched by the server. For forward only, it is the maximum number of rows fetched in a communication packet. For scrollable, it is fixed to 100. If the value is too large, the amount of memory used by JDBC ResultSet becomes large. If the value is too small, the communication is frequently executed.

The value is mainly used in a scrollable ResultSet because it is not sensitive even when it is scroll sensitive while moving within the row cache of ResultSet. If the value is set too large, the latest information about the changes of rows can not be known.

<a id="6896263db3bc3d89"></a>
#### Field Size Limit

JDBC may limit the maximum length of the column through setMaxFieldSize(int size) of statement. The maximum length can be limited for the types of CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, and LONG VARBINARY. The data bigger than the length is truncated. The default value is 0, and the maximum length is not limited in this case.

This property is ignored for other types such as INTEGER, DATE, etc..

<a id="fafd2b1319424f7c"></a>
### ResultSet Scroll

<a id="7103685b2a16875c"></a>
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

<a id="57df9c2c6589c8d0"></a>
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

<a id="e1e75759adfbb386"></a>
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

<a id="ffdc3b15ea1df333"></a>
### Using Other Data Types

<a id="3af4967cb3826613"></a>
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

For more information about createIntervalXXX method, refer to [GoldilocksInterval](#d4511de4af40986a). Likewise, GoldilocksInterval is created and it is bound via setObject. Or, a type is explicitly specified as follows.

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

The data of GoldilocksInterval type can be retrieved via getObject() of ResultSet. GoldilocksInterval class provides getter like getYear(), getHour(), etc. that return various time data. For more information about getter API, refer to [GoldilocksInterval](#d4511de4af40986a).

<a id="990c7d77d9bacbe2"></a>
#### Time with Time Zone and Timestamp with Time Zone Types

Concerning time, GOLDILOCKS provides not only SQL standard types such as Date, Time, Timestamp but also Time with time zone and Timestamp with time zone types.

```
CREATE TABLE SAMPLE_TABLE ( C1 TIME WITH TIME ZONE,
                            C2 TIMESTAMP WITH TIME ZONE );
```

GOLDILOCKS JDBC provides setTimeTimeZone(int colIndex, Time time, Calendar timezone) method and setTimestampTimeZone(int colIndex, Timestamp time, Calendar timezone) method in GoldilocksPreparedStatement class to insert the data of Time with time zone and Timestamp with time zone types. For more information about specifications refer to [setTimeTimeZone](#40180ea95c43ba0f) and [setTimestampTimeZone](#1d891c28bb8fb893).

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

<a id="1fb0a997a5de3855"></a>
### Logging

<a id="c436d90add721716"></a>
#### Logging Types

When developing a project by using JDBC, it is helpful in many ways for JDBC driver to leave various logs. GOLDILOCKS provides the facility to log the useful information even during operation, as well as the project development.  
There are three types of log, which are trace log, protocol log and query log.

Trace log leaves information every time when JDBC API is called. It can be known which JDBC API is called. Protocol log shows the situation to send and receive communication packets between JDBC driver and GOLDILOCKS server. Query log records the SQL statement to be executed, when PreparedStatement or Statement is executed.

<a id="903f74f03de32a66"></a>
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

The connection properties which can be used in GOLDILOCKS are defined in [Connection property](#00de0770e9a7490d).

Sometimes it is difficult to call setLogWriter() of DriverManager. When using the middleware, the code like that can not be added. For such a case, GOLDILOCKS JDBC provides a global property called global_logger. Other general properties are limited to a single connection, but this property is global. In other words, if the property is set, it does not have to call DriverManager.setLogWriter ().

```
String url = "jdbc:goldilocks://localhost:22581/test?" +            
             "global_logger=console&trace_log=on&query_log=on";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

global_logger property is applied only once initially, and it is ignored if log writer is already set in DriverManager. Only the current console is applicable as the property value. Other value does not cause any operation.

<a id="6d288fa857f4280d"></a>
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

<a id="8a0d6fc839863652"></a>
### Viewing Plan Text

<a id="895ede2933cc53b3"></a>
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

<a id="5a91ba2f0827d1da"></a>
#### Option Types

GOLDILOCKS provides the following four properties about the plan text generation.

- EXPLAIN_PLAN_OPTION_OFF: It does not generate the plan text as the default value of the property related to the plan text of statement.
- EXPLAIN_PLAN_OPTION_ON: It generates the plan text when executing or fetching. 
- EXPLAIN_PLAN_OPTION_ON_VERBOSE: It generates more detailed plan text such as execution time when executing or fetching. 
- EXPLAIN_PLAN_OPTION_ONLY: It generates the plan text like as EXPLAIN_PLAN_OPTION_ON when executing or fetching but it is not actually executed.

These properties are set by using GoldilocksStatement.setExplainPlanOption(int) method, and the property which is set once is continuously maintained. A constant value of the property is defined in GoldilocksStatement.

> The plan text for non-SELECT DML statements or other SQL statements is generated at run-time, but the plan text for the SELECT statements is generated when the SELECT statement is fetched and the cursor is positioned at the end in the server. The plan text should be obtained after all rows are traversed with ResultSet for the SELECT statement. The plan text can be obtained when there are few rows in a table because the cursor can traverse until the end in the server without fetching all rows.

<a id="c288b3c87ae9ee54"></a>
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

<a id="711854d4dff3f642"></a>
#### failover_type

The property is used to select the failover type. In the example above, the failover at 1 is the connection failover and the failover at 2 is the session failover. If the property value is *connection*, only the connection failover is used, and if it is *session*, both of the connection failover and session failover can be used. The default value is *session*.

<a id="88678462f2690356"></a>
#### failover_granularity

When failover occurs, the prepare operation is performed after the PreparedStatement objects which are generated from the current connection object are connected to the alternative server. If the prepare operation fails in the alternative server (An error may occur due to the different server environment.), the property is used to determine whether to consider the failover failed or to ignore the prepare error. The property value is either 0 or 1. If the property value is 0, the prepare error is ignored and the failover continuously proceeds. If the property value is 1, the failover is failed. The default value is 0. If the value is 0 and the prepare operation is failed, PreparedStatement object can not continue to be used and the user should directly create the PreparedStatement object again.

<a id="8429ee4c8080d90d"></a>
### Connecting in Direct Attach Mode

Since JDBC 1.1, Goldilocks provides the connection in direct attach mode (D/A mode) besides the existing connection in Client/ Server mode (C/S mode) based on TCP/ IP. Like as ODBC D/A connection mode, this is operated directly interworking with the server process. so the server module interworks within a single process (in a process same as jvm). Therefore, the remote host can not connect in D/A mode.

D/A mode is designed to utilize the merit of an in-memory DB GOLDILOCKS, which is a fast processing. TCP/ IP based connection offsets the fast processing of GOLDILOCKS by expensive cost, so an alternative method is required when a fast processing is required. Though it is restricted to be operated within the host which is same as the host of GOLDILOCKS server, this D/A mode connection is a good solution.

JDBC program connecting in D/A mode can directly call the server feature by loading GOLDILOCKS jni library when DB connection is created first within jvm. A server module can be directly called through native interface in jvm without network cost, it enables faster processing than the existing C/S mode.

<a id="a4917946e1aed421"></a>
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

<a id="2fcb2fa1a4a3e176"></a>
#### Features of D/A Connection

GOLDILOCKS server module can be directly called in jvm when connecting in D/A mode. It is called through JNI (Java Native Interface) between JDBC program and GOLDILOCKS server module. It uses the server module with minimum call cost considering that it is expensive to call JNI, so it is faster double than the JDBC based on existing TCP/ IP.

When using the connection based on the existing TCP/ IP, it uses only goldilocks6.jar file. However, when using the connection based on D/A mode, it uses libgoldilocksjni.so file and libgoldilocksas.so file in $GOLDILOCKS_HOME/lib by dynamically loading them. Therefore, an error occurs when connecting if those two library files do not exist. However, the location of the library files need not to be separately specified when operating java program. Because it searches for those two library files and loads them as long as it is in the directory as same as the directory of goldilocks6.jar file.

<a id="f5641bf90d15a3a9"></a>
### Global Connection

It support the global connection feature. When using the global connection, an application selects a node appropriate for a query process and performs it in the cluster environment.

<a id="00e94363ecd4ec8a"></a>
#### Settings

locator_file or locator_host, locator_port should be set together with locality_aware_transaction property value to use the global connection. use_global_session property value should be set to 1 to use the global connection.

```
Properties prop = new Properties();
prop.put("locality_aware_transaction", "1");
prop.put("locator_file", "/home/goldilocks/.location.ini");
prop.put("user", "TEST");
prop.put("password", test");
Connection con = DriverManager.getConnection(url, prop);
```

```
String url = "jdbc:goldilocks://192.168.0.1:22581/test?" +            
             "locality_aware_transaction=1&locator_host=192.168.0.2&locator_port=42581";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

<a id="dcae2950a32e7998"></a>
#### Procedure

1. Connect to the database.

After connecting to the server input by a user and receiving the information of the cluster system, the cluster system information is built through the locator file or glocator, then it connects to all nodes in the cluster system.

2. Execute the statement.

If the cluster system information is not built, then the cluster system information is built through the locator file or glocator, then it connects to all nodes in the cluster system.

When connecting to a new server by adding a node to the cluster, then it creates all statements of another node on the node, and is ready to execute SQL.

The statement class does not have the information about the sharding key, so the node is selected according to locality_group_policy or locality_member_policy property and the statement is executed.

If PreparedStatement or CallableStatement class does not have the information about the sharding key, then it builds the information about the sharding key of the SQL from an arbitrary server. If the information about the sharding key is built, then an appropriate node is selected by using the information about the sharding key or locality_group_policy, locality_member_policy, and the query is executed.

If an error occurs on the selected node, then it selects an appropriate node again except for that node, and executes the query.

If the sharding information is updated after executing the statement, then the built sharding key information is dropped.

If the cluster system information is updated by adding/ dropping the cluster node after executing the statement, then the built cluster system information is dropped.

3. Receive ResultSet data.

It receives the data from the node where SQL was executed.

4. Close ResultSet.

It closes a cursor on the node where SQL was executed.

5. Close the statement.

It releases the statement from all connected node.

6. Close the database.

It releases connection to all nodes.

<a id="4a51fffa164f32b5"></a>
#### Exception Handling for High Availability

When using GLOBAL CONNECTION, if an error occurs on the selected node during the operation, then it is operated as follows according to the transaction occurrence and SELECT progress.

- When a transaction did not occur

If an error occurs on the selected node when a transaction did not occur, then it selects another node within JDBC and executes the query. Though an error occurred on the selected node, the query was normally executed on another node, so it does not transfer an error to a user.

- When a transaction occurred or SELECT is in progress

If an error occurs on the selected node when a transaction occurred or ResultSet.next() is in progress, then JDBC can not proceeds the current operation any more so it transfers 21047(Retry the transactional operations again). If 21047 error occurs, then a user should perform the transaction or SELECT again.

```
PreparedStatement pstmt = con.prepareStatement("INSERT INTO T1 VALUES (?)");

boolean retry;

do
{
    retry = false;

    try
    {
        pstmt.setInt(1, 1);
        pstmt.executeUpdate();
    }
    catch (SQLException e)
    {
        if (e.getErrorCode() == 21047)
        {
            retry = true;
        }
        else
        {
            throw e;
        }       
    }
} while (retry == true);
```

```
PreparedStatement pstmt = con.prepareStatement("SELECT * FROM T1 WHERE C1 = ?");

boolean retry;

do
{
    retry = false;

    try
    {
        pstmt.setInt(1, 1);
        ResultSet rs = pstmt.executeQuery();
        while (rs.next())
        {
            ...
        }
        rs.close();
    }
    catch (SQLException e)
    {
        if (e.getErrorCode() == 21047)
        {
            retry = true;
        }
        else
        {
            throw e;
        }       
    }
} while (retry == true);
```

- When committing or rolling back a transaction

If an error occurs on the selected node when committing a transaction, then JDBC checks whether the transaction has been committed before the error occurred through another node. Though an error occurred on the selected node, if the transaction was normally committed, then it does not transfer an error. Also, if an error occurred on the selected node when a transaction has not been committed, then it transfers 21047(Retry the transactional operations again) error. If 21047error occurs, then a user should perform the transaction again.

If an error occurs on the selected node when rolling back a transaction, then JDBC does not transfer an error. It is because the transaction already has been rolled back due to the node error.

```
con.setAutoCommit(false);

PreparedStatement pstmt = con.prepareStatement("INSERT INTO T1 VALUES (?)");

boolean retry;

do
{
    retry = false;

    try
    {
        pstmt.setInt(1, 1);
        pstmt.executeUpdate();
        con.commit();
    }
    catch (SQLException e)
    {
        if (e.getErrorCode() == 21047)
        {
            retry = true;
        }
        else
        {
            throw e;
        }       
    }
} while (retry == true);
```

<a id="d09870c8ca6ded58"></a>
#### Constraints

- Use only PreparedStatement and CallableStatement class to select a node appropriate for SQL.

The statement class does not have the information required to select the node appropriate for the query, so the node is selected according to locality_group_policy or locality_member_policy property.

- Use Connection.commit(). Connection.rollback() to commit or rollback a transaction.

If committing or rolling back with SQL statement when using GLOBAL CONNECTION, then the status change of the transaction is not detected. It is mandatory to use Connection.commit(). Connection.rollback() to commit or rollback the transaction.

- Global session feature does not support Data Definition Language (DDL) among SQL statements.

<a id="143a16e29d609458"></a>
### Statement Pooling

GOLDILOCKS supports the statement pooling feature. Statement pooling improves the performance by pooling statements which are repeatedly used such as a repetitive statement and a repeatedly called method. The interface for the statement pooling is defined in JDBC 3.0.

An application pools the statement related to a specific connection by using the statement pool. Each connection object has its own pool. GoldilocksConnection includes a method which enables the statement pool. If the statement pool is used, then the statement object is pooled when the close method is called.

<a id="409049ad0de5c9c2"></a>
#### Description

If the statement pool is enabled and the close method of the statement object is called, then GOLDILOCKS JDBC driver automatically pools the statement, PreparedStatement and CallableStatement. PreparedStatement and CallableStatement objects perform pooling by using SQL string as a key value. JDBC driver automatically compares/ retrieves PreparedStatement or CallableStatement when creating them.

It is compared based on the following basis.

- SQL strings should be same.
- The statement types should be same.
- The result set properties should be same.

SQL string of the statement object is subject to change, so SQL string is not used for the pooling, but JDBC driver automatically processes it.

If the matching statement is retrieved while searching in the pool, then it is returned, and if it is not found, then a new statement is created. The statement, the cursor and the status are pooled in both cases if the close method of the object is called. However, the statement becomes closed. Create the statement whose SQL string, the statement type and the result set property are same to use the closed statement again.

If pooled PreparedStatement and CallableStatement objects are retrieved, then the status and the data information are automatically initialized again, and reset to the default value. When the statement pool is full, then it is dropped from the pool by LRU algorithm. Statements stored in the statement pool can be cleared when the close method of the connection object is called.

<a id="176bed7ee613ed64"></a>
#### Usage

<a id="f3a4a4193e391820"></a>
##### Enabling Statement Pool

STATEMENT_POOL_ON and STATEMENT_POOL_SIZE properties should be set to use the statement pool of the connection object. Even when STATEMENT_POOL_ON property is enabled, the default value of STATEMENT_POOL_SIZE is 0, so use the figure bigger than 0.

The statement pool feature is enabled by adding STATEMENT_POOL_ON and STATEMENT_POOL_SIZE properties to the properties object. The statement pool feature is also enabled through GoldilocksDataSource API and GoldilocksConnection API.

<a id="28e5ecc1934c0a1c"></a>
###### **Enabling through GoldilocksDataSource**

If GoldilocksDataSource class is used, then all connection objects gets statement pools with the identical STATEMENT_POOL_SIZE.

- Call setStatementPoolOn(true) method.
- Call setStatementPoolsize method.

```
GoldilocksDataSource sDataSource = new GoldilocksDataSource();

sDataSource.setStatementPoolOn( true );
sDataSource.setStatementPoolSize( 10 );
```

The property setting values can be viewed as follows.

```
System.out.println("Statement Pool on:" + sDataSource.getStatementPoolOn());
System.out.println("Statement Pool size:" + sDataSource.getStatementPoolSize());
```

<a id="c7d65448bcad8270"></a>
###### **Enabling through GoldilocksConnection**

If GoldilocksConnection class is used, then the statement pool is enabled aside from other objects.

- Call setStatementPoolOn(true) method.
- Call setStatementpoolSize method.

```
GoldilocksConnection sCon = sDataSource.getConnection();

sCon.setStatementPoolOn( true );
sCon.setStatementPoolSize( 10 );
```

The property setting values can be viewed as follows.

```
System.out.println("Statement Pool on:" + sCon.getStatementPoolOn());
System.out.println("Statement Pool size:" + sCon.getStatementPoolSize());
```

<a id="a6a2d718c5b35a71"></a>
##### Disabling Statement Pool

Enabled statement pool can be disabled. If switching the enabled status to the disabled status, then statements stored in the statement pool are dropped and closed.

Disabling by using setStatementPoolOn method

```
sCon.setStatementPoolOn(false);
```

Disabling by using setStatementPoolSize method

```
sCon.setStatementPoolSize(0);
```

<a id="44e461aff53fbe81"></a>
##### Creating Statement

The method to created the statement, PreparedStatement, and CallableStatement while the statement pool is enabled is as same as the general creating method.

The following is a code to create the new statement object.

```
PreparedStatement sPstmt = sCon.prepareStatement( "INSERT INTO EMP VALUES ( ?, ? )" );
```

<a id="0b07e3619552ebee"></a>
##### Disabling Specific Statement

If the statement pool is enabled, then GOLDILOCKS JDBC driver automatically pools all statements. Using setPoolable method excludes a specific statement from the pooling.

The following is an example of checking whether it is pooled by using isPoolable method and setPoolable method.

```
PreparedStatement sPstmt = sCon.prepareStatement( "SELECT 1 FROM DUAL" );
System.out.println( "Is poolable: " + sPstmt.isPoolable() );
sPstmt.setPoolable( false );
System.out.println( "Is poolable: " + sPstmt.isPoolable() );
```

<a id="0290b5f7e2462758"></a>
## JDBC API References

<a id="f1e91413b625a755"></a>
### Array

The class is not implemented.

<a id="aa60a5b4c77c8ef0"></a>
#### free

```
void free() throws SQLException
```

<a id="aa1b8401809ad613"></a>
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

<a id="8d61a80f4378aa48"></a>
#### getBaseType

```
int getBaseType() throws SQLException
```

<a id="13b20bb1bc2f399e"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="5e8c878f8afa92fe"></a>
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

<a id="0843d9dcc6136065"></a>
### Blob

<a id="fb56d834c330e5d2"></a>
#### free

```
void free() throws SQLException
```

- Operation: It frees the sources owned by this object.
- Exception: It does not occur.

<a id="5bce478f7bf7716a"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

- Operation: It returns the blob object value in InputStream type.
- Exception: If the blob is freed, it throws SQLException.

```
InputStream getBinaryStream(long pos, long length) throws SQLException
```

- Operation: It returns InputStream type which includes the blob object value as big as the length from the byte defined as pos.
- Exception: When the blob is freed, if pos is smaller than 1 or bigger than the byte length of the blob object, or if pos + length is bigger than the byte length of blob object, then it throws SQLException.

<a id="186dd159359c6e39"></a>
#### getBytes

```
byte[] getBytes(long pos, int length) throws SQLException
```

- Operation: It returns byte array which includes the blob object value as big as the length from the byte defined as pos.
- Exception: When the blob is freed, if pos is smaller than 1 or if the length is smaller than 0, then it throws SQLException.

<a id="b86fbf0504137700"></a>
#### length

```
long length() throws SQLException
```

- Operation: It returns the byte length of the blob object.
- Exception: If the blob is freed, it throws SQLException.

<a id="0daed203f76df10d"></a>
#### position

```
long position(byte[] pattern, long start) throws SQLException
```

- Operation: It returns the location of the byte from which the byte array pattern starts defined in the blob object value. pattern search starts from the location of start. If the pattern is not found in the blob object then -1 is returned.
- Exception: When the blob is freed, if start is smaller than 1, then it throws SQLException.

```
long position(Blob pattern, long start) throws SQLException
```

- Operation: It returns the location of the byte from which the blob object pattern starts defined in the blob object value. pattern search starts from the location of start. If the pattern is not found in the blob object then -1 is returned.
- Exception: When the blob is freed, if start is smaller than 1, then it throws SQLException.

<a id="6ff11a498874af14"></a>
#### setBinaryStream

```
OutputStream setBinaryStream(long pos) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="0ef94e9575bbfdcc"></a>
#### setBytes

```
int setBytes(long pos, byte[] bytes) throws SQLException
```

- Operation: It records the byte array bytes from the given pos location in the blob object value, and returns the length of the recorded bytes. If the value exists in pos location, then the byte array is overwritten. If it reaches to the end of the blob value while recording byte array, then the length of the blob value is extended so that it can include the additional bytes. 
- Exception: When the blob is freed, if pos is smaller than 1, then it throws SQLException.

```
int setBytes(long pos, byte[] bytes, int offset, int len) throws SQLException
```

- Operation: It records the blob object value from pos location as long as the len length from offset location of the given byte array bytes, and returns the length of the recorded bytes. If the value exists in pos location, then the byte array is overwritten. If it reaches to the end of the blob value while recording byte array, then the length of the blob value is extended so that it can include the additional bytes. 
- Exception: When the blob is freed, if pos is smaller than 1 or offset is smaller than 0 or offset + len is bigger than bytes length, then it throws SQLException.

<a id="cc218fe8b67038de"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

- Operation: It truncates the length of the blob object into the given len length. 
- Exception: When the blob is freed, if len is smaller than 0, then it throws SQLException.

<a id="3e73467a821afdba"></a>
### CallableStatement

<a id="c54a1d8922cf804c"></a>
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

<a id="5a798a6813ac508d"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in BigDecimal type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
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

<a id="d169d56fe470957b"></a>
#### getBlob

```
Blob getBlob(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in blob type.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Blob getBlob(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ca95c0398176bcbb"></a>
#### getBoolean

```
boolean getBoolean(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in boolean type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
boolean getBoolean(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="1adb7f753d6830d7"></a>
#### getByte

```
byte getByte(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in byte type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
byte getByte(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="b1a81b3fab3bb09f"></a>
#### getBytes

```
byte[] getBytes(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in byte[] type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
byte[] getBytes(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="89e79490341713eb"></a>
#### getCharacterStream

```
Reader getCharacterStream(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in reader type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Reader getCharacterStream(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="477f7ae8bf350f54"></a>
#### getClob

```
Clob getClob(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in clob type.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Clob getClob(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="2d1e5cad15cd94e8"></a>
#### getDate

```
Date getDate(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in date type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses local time zone and locale when creating a date object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Date getDate(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in date type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses time zone and locale of cal when creating a date object.
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

<a id="ed55460b33f63aa1"></a>
#### getDouble

```
double getDouble(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in double type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
double getDouble(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="66a5460ffc6d9777"></a>
#### getFloat

```
float getFloat(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in float type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
float getFloat(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="9086efe43a1431f2"></a>
#### getInt

```
int getInt(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in int type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
int getInt(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="346223884936b90e"></a>
#### getLong

```
long getLong(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in long type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
long getLong(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="23b969cca7543fa0"></a>
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

<a id="b21cd1efcf40a741"></a>
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

<a id="fefd9601c10f8d6b"></a>
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

<a id="90f05aead4bbff94"></a>
#### getObject

```
Object getObject(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in Java object type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
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

<a id="ad1cd8c8e3958aae"></a>
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

<a id="59db2700ee4e6a2e"></a>
#### getRowId

```
RowId getRowId(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in rowid type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
RowId getRowId(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="8253ef6b75b1b8a8"></a>
#### getShort

```
short getShort(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in short type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
short getShort(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a60cc02e9b4d51fd"></a>
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

<a id="ef7a50848a632ef0"></a>
#### getString

```
String getString(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in string type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
String getString(String parameterName) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="9a1f9e790f15e765"></a>
#### getTime

```
Time getTime(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in time type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses local time zone when creating a time object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Time getTime(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in time type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses time zone of cal when creating a time object.
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

<a id="6784f9d715110aeb"></a>
#### getTimestamp

```
Timestamp getTimestamp(int parameterIndex) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in timestamp type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses local time zone when creating a timestamp object.
- Exception: If the parameterIndex is invalid, database is not accessible, or CallableStatement is already closed, then it throws SQLException.

```
Timestamp getTimestamp(int parameterIndex, Calendar cal) throws SQLException
```

- Operation: It obtains column data at parameterIndex-th position in timestamp type. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d). It uses time zone of cal when creating a timestamp object.
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

<a id="496867842cb2f205"></a>
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

<a id="ed77b2a28754d4de"></a>
#### registerOutParameter

```
void registerOutParameter(int parameterIndex, int sqlType) throws SQLException
```

- Operation: It registers out parameters positioned in parameterIndex as sqlType. All out parameters should be registered before executing the stored procedure. JDBC type of out parameter specified as sqlType determines Java type which is used in a get method to read parameter parameter value. For more information about whether it supports GOLDILOCKS types, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
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

<a id="add8c94cdc9fce7d"></a>
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

<a id="c806a8f2e7b47072"></a>
#### setBigDecimal

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="d01a0dc929ebb59c"></a>
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

<a id="400f24b2c3706ddb"></a>
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

<a id="c56f856fbf3c2e95"></a>
#### setBoolean

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ca193edbec3b7f15"></a>
#### setByte

```
void setByte(String parameterName, byte x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="d3be56692af2ebdc"></a>
#### setBytes

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="edefb208e1d9930b"></a>
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

<a id="e75f2406925c2503"></a>
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

<a id="85c803445417ca30"></a>
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

<a id="7d487b3869530892"></a>
#### setDouble

```
void setDouble(String parameterName, double x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a0b628f52d69c6f5"></a>
#### setFloat

```
void setFloat(String parameterName, float x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a029c7a9ff0aed30"></a>
#### setInt

```
void setInt(String parameterName, int x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e462ff576f79c4d2"></a>
#### setLong

```
void setLong(String parameterName, long x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ea9737ead0c14776"></a>
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

<a id="170d58d3e8c70a63"></a>
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

<a id="ea752b310771c093"></a>
#### setNString

```
void setNString(String parameterName, String value) throws SQLException
```

- Operation: It does not support NChar.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="204d2abe3194a1e8"></a>
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

<a id="d79a3e1433369ddd"></a>
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

<a id="bad34056a0cbdfed"></a>
#### setRowId

```
void setRowId(String parameterName, RowId x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="2389c53c37abbae1"></a>
#### setShort

```
void setShort(String parameterName, short x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="2215ddd9bef70511"></a>
#### setSQLXML

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

- Operation: It does not support SQLXML type.
- Exception: It always returns SQLFeatureNotSupportedException.

<a id="3258077e0c7da43c"></a>
#### setString

```
void setString(String parameterName, String x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="4a2f50da74a6ecb9"></a>
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

<a id="4736e03bb7039fa9"></a>
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

<a id="c77b199b414a6984"></a>
#### setURL

```
void setURL(String parameterName, URL val) throws SQLException
```

- Operation: It does not support URL type.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e32d9503f9863876"></a>
#### wasNull

```
boolean wasNull()
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="a98e75f88fa63634"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="930be4d71fdcc49b"></a>
#### unwrap

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="0e11a9b92118d745"></a>
### Clob

<a id="03604f8a1492e4d8"></a>
#### free

```
void free() throws SQLException
```

- Operation: It frees the sources owned by this object.
- Exception: It does not occur.

<a id="0c4f74b1f01852d8"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

- Operation: It returns the clob object value in InputStream type.
- Exception: If the clob is freed, it throws SQLException.

<a id="8bddf8677abb1d2c"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

- Operation: It returns the clob object value in reader type.
- Exception: If the clob is freed, it throws SQLException.

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

- Operation: It returns the clob object value in reader type as big as the length from the location defined as pos.
- Exception: When the blob is freed, if pos is smaller than 1 or if length is smaller than 1, or if pos + len is equal to or bigger than the length of clob object, then it throws SQLException.

<a id="b42abe56f9b695dc"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

- Operation: It returns the string which includes the clob object value as big as the length from the length defined as pos.
- Exception: When the clob is freed, if pos is smaller than 1 or if length is smaller than 0, then it throws SQLException.

<a id="b831178cf73e9db2"></a>
#### length

```
long length() throws SQLException
```

- Operation: It returns the data length of the clob object.
- Exception: If the clob object is freed, it throws SQLException.

<a id="f53108907ed6f2e1"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

- Operation: It returns the location from which the clob object searchstr starts defined in the clob object value. searchstr search starts from the location of start. If searchstr is not found in the clob object then -1 is returned.
- Exception: When the clob is freed, if start is smaller than 1, then it throws SQLException.

```
long position(String searchstr, long start) throws SQLException
```

- Operation: It returns the location from which the string object searchstr starts defined in the clob object value. searchstr search starts from the location of start. If searchstr is not found in the clob object then -1 is returned.
- Exception: When the clob is freed, if start is smaller than 1, then it throws SQLException.

<a id="e538a7a379c83f63"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="9036e624155802bb"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="d673cf40a57faf10"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

- Operation: It records str from the given pos location in the clob object value, and returns the recorded length. If the value exists in pos location, then it is overwritten. If it reaches to the end of the clob value while recording the string type, then the length of the clob value is extended so that it can include the additional bytes. 
- Exception: When the clob is freed, if pos is smaller than 1, then it throws SQLException.

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

- Operation: It records the clob object value from pos location as long as the len length from offset location of the given string object str, and returns the recorded length. If the value exists in pos location, then the value is overwritten. If it reaches to the end of the clob value while recording the string type, then the length of the clob value is extended so that it can include the additional bytes. 
- Exception: When the clob is freed, if pos is smaller than 1 or if it is bigger than offset + len, then it throws SQLException.

<a id="adf38a5d6d0a0d08"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

- Operation: It truncates the length of the clob object into the given len length. 
- Exception: When the clob is freed, if len is smaller than 0 or if the clob size is smaller than len, then it throws SQLException.

<a id="5dd987c06edb0cba"></a>
### CommonDataSource

<a id="984ed4d9340b6e20"></a>
#### getLoginTimeout

```
int getLoginTimeout() throws SQLException
```

- Operation: It returns the login timeout setting value. Login timeout is used as a timeout value when performing socket connection to the server. If the value is not set, 0 is returned. 0 means infinite standby.
- Exception: It does not occur.

<a id="71d0c3a92d4f19f7"></a>
#### getLogWriter

```
PrintWriter getLogWriter() throws SQLException
```

- Operation: It returns the log writer which is set in the DataSource. If it is not set, null is returned. Log writer refers to PrintWriter to write various trace logs. For more information about logging, refer to [Logging](#1fb0a997a5de3855).
- Exception: It does not occur.

<a id="2689f6cced1a9c9f"></a>
#### setLoginTimeout

```
void setLoginTimeout(int seconds) throws SQLException
```

- Operation: It sets the login timeout value. Login timeout is used as a timeout value when performing socket connection to the server. 0 means infinite standby.
- Exception: It does not occur.

<a id="88a932562f498b46"></a>
#### setLogWriter

```
void setLogWriter(PrintWriter out) throws SQLException
```

- Operation: It sets the log writer in DataSource. If the value is not set, the default value is null. Log writer refers to PrintWriter to write various trace logs. If the value is set, trace log, query log, and protocol log are written according to the options, and connection object which is created from DataSource and all objects which are created from connection object such as Statement, ResultSet, perform logging. Trace log, query log, protocol log options can be specified in the connection url or property. For more information about logging, refer to [Logging](#1fb0a997a5de3855).
- Exception: It does not occur.

<a id="17fc1124b460dc7c"></a>
#### setDataSourceName

```
void setDataSourceName(String aDataSourceName)
```

- Operation: It sets the data source name. It is not the mandatory information required for the connection. It is the information charged separately to distinguish objects.
- Exception: It does not occur.

<a id="21f8e67477fa2ce4"></a>
#### setServerName

```
void setServerName(String aServerName)
```

- Operation: It sets the server name, which is the connection URL. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="cbf017b992cece24"></a>
#### setDatabaseName

```
void setDatabaseName(String aDBName)
```

- Operation: It sets the database name. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="5335894b91204e87"></a>
#### setNetworkProtocol

```
void setNetworkProtocol(String aProtocol)
```

- Operation: It is the network protocol information. It is not the mandatory information required for the connection.
- Exception: It does not occur.

<a id="e8d0b3293963a4d9"></a>
#### setUser

```
void setUser(String aUser)
```

- Operation: It sets the connection account name. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="d225929140985400"></a>
#### setPassword

```
void setPassword(String aPassword)
```

- Operation: It sets the connection account password. It is the mandatory information required for the connection.
- Exception: It does not occur.

<a id="1f89975e07103619"></a>
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

<a id="ab7a9dfa79687320"></a>
#### setRoleName

```
void setRoleName(String aRoleName)
```

- Operation: It specifies the role of when connecting to server. It is not mandatory information required for the connection, but it is the connection related information. One of "", "ADMIN", "SYSDBA" is specified.
- Exception: It does not occur.

<a id="4f31f8aca4a54ee1"></a>
#### setDescription

```
void setDescription(String aDescription)
```

- Operation: It sets the description about the data source. It is not used for the connection.
- Exception: It does not occur.

<a id="e8af9c7ab6bf32e1"></a>
#### setConnectionProperties

```
void setConnectionProperties(Properties aProps)
```

- Operation: It defines the properties which can be used in various connections.
- Exception: It does not occur.

<a id="e20bf836d11d186a"></a>
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

<a id="1b4711b0d1d46350"></a>
#### setLogTarget

```
void setLogTarget(String aTarget)
```

- Operation: If setLogWriter can not be called, the log writer is set by this method. Currently, it is supported only when aTarget is "console", other values are ignored. If it is set to "console", all loggings below the connection object which is generated from the DataSource are output to the console.
- Exception: It does not occur.

<a id="6465c0e297e369a4"></a>
#### setTraceLog

```
void setTraceLog(String aMode)
```

- Operation: It sets the trace log. If aMode is *on*, the trace logging is on.
- Exception: It does not occur.

<a id="9c1f76d4e961a329"></a>
#### setQueryLog

```
void setQueryLog(String aMode)
```

- Operation: It sets the query log. If aMode is *on*, the query logging is on.
- Exception: It does not occur.

<a id="3eaadcc9036a9456"></a>
#### setProtocolLog

```
void setProtocolLog(String aMode)
```

- Operation: It sets the protocol log. If aMode is *on*, the protocol logging is on.
- Exception: It does not occur.

<a id="abcf14ed8a505e94"></a>
### Connection

<a id="7e78119336eb3187"></a>
#### clearWarnings

```
void clearWarnings() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It clears the warning object(s) owned by the current connection object.
- Exception: It does not occur.

<a id="18f70330871159ca"></a>
#### close

```
void close() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It breaks the connection with GOLDILOCKS not to use anymore the current connection and closes all statement objects created from the object. If already closed, any operation is not performed.
- Exception: It may happen when an error occurs from the server or it does not respond.

<a id="2d6d7f92f1900fb1"></a>
#### commit

```
void commit() throws SQLException
```

- Operation: For non-auto commit mode, the commit is executed for the current connection.
- Exception: If it is already closed or is on the auto-commit mode, it throws SQLException.

<a id="39ee5f9aa74c438d"></a>
#### createArrayOf

```
Array createArrayOf(String typeName, Object[] elements) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="e22ce19408aadfd9"></a>
#### createBlob

```
Blob createBlob() throws SQLException
```

- Operation: It creates the object which implemented the blob interface. The first returned object does not have a data. The data can be added to the blob object by using setBytes method of the blob interface.
- Exception: If it is already closed, it throws SQLException.

<a id="dbf80c1dc4da5f88"></a>
#### createClob

```
Clob createClob() throws SQLException
```

- Operation: It creates the object which implemented the clob interface. The first returned object does not have a data. The data can be added to the clob object by using setString method of the clob interface.
- Exception: If it is already closed, it throws SQLException.

<a id="2281fd1b1c9a1d5f"></a>
#### createNClob

```
NClob createNClob() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="b1b39fe24effda76"></a>
#### createSQLXML

```
SQLXML createSQLXML() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6087157e1366807c"></a>
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

<a id="990cd92c9c5c04be"></a>
#### createStruct

```
Struct createStruct(String typeName, Object[] attributes) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="8f105104fdc083e6"></a>
#### getAutoCommit

```
boolean getAutoCommit() throws SQLException
```

- Operation: It returns the current auto commit mode. If setAutoCommit() has not been called, it returns true.
- Exception: It does not occur.

<a id="74522a5a3e855512"></a>
#### getCatalog

```
String getCatalog() throws SQLException
```

- Operation: It gets the current catalog name of the database.
- Exception: If an error occurs from the server or it does not respond, then it throws SQLException.

<a id="5541e66df9237fff"></a>
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

<a id="879bb7cbf21ad0c2"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- Operation: It returns the default holdability value of statements created by this object. The default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="f51dc990a446b94a"></a>
#### getMetaData

```
DatabaseMetaData getMetaData() throws SQLException
```

- Operation: It gets a DatabaseMetaData object which can be queried for metadata information from this object. It always returns the same object.
- Exception: If it is already closed, it throws SQLException.

<a id="59039e203360ee8f"></a>
#### getNetworkTimeout

```
int getNetworkTimeout() throws SQLException
```

- Operation: It returns the current network timeout (millisecond). 0 means no limit.
- Exception: If it is already closed, it throws SQLException.
- Since: 1.7

<a id="50552303966448a3"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

- Operation: It gets the transaction isolation level which is set on the current session (connection). The default value which is set on the server is Connection.TRANSACTION_READ_COMMITTED.
- Exception: If an error occurs from the server, it throws SQLException.

<a id="245a6efbc699e056"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="aa73575cb2106bc3"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns a warning which the server responds to connection object until now. If a warning does not exist or clearWarnings() is already performed, it returns null.
- Exception: It does not occur.

<a id="4570f3f60fbb101d"></a>
#### isClosed

```
boolean isClosed() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It queries whether close() is successfully called. If close() is successfully performed, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

> This method does not inform a user whether the connection to a physical server is broken. Even if the actual connection is broken it returns true when close () has never been called.

<a id="b1b849b699aac159"></a>
#### isReadOnly

```
boolean isReadOnly() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: If the session(connection) is read only mode, it returns true. Otherwise, it returns false. The default value is false. Communication with the server occurs.
- Exception: If an error occurs from the server or it does not respond, it throws SQLException.

<a id="7cac016cff638de6"></a>
#### isValid

```
boolean isValid(int timeout) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: If isClosed() returns true or the heart beat query is sent to the server and response is not successfully received, it returns false. Otherwise, it returns true.
- Exception: It does not occur.

<a id="911ffeff9bc2958c"></a>
#### nativeSQL

```
String nativeSQL(String sql) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- Operation: It returns the native SQL recognized by the server for the given user SQL statement. GOLDILOCKS always return the value as same as given by the user because the server recognizes the user's SQL statement literally.
- Exception: It does not occur.

<a id="b8bf307b5879e955"></a>
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

<a id="24bd2c5d7485b7f3"></a>
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

<a id="cbd81d2407081232"></a>
#### releaseSavepoint

```
void releaseSavepoint(Savepoint savepoint) throws SQLException
```

- Operation: It removes the savepoint from the server. It also removes all savepoints after this savepoint.
- Exception: If it is already closed or the savepoint object was already released or it is not the GOLDILOCKS savepoint object, it throws SQLException.

<a id="5a4b957c03838a4c"></a>
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

<a id="7f02d61690a7ccef"></a>
#### setAutoCommit

```
void setAutoCommit(boolean autoCommit) throws SQLException
```

- Operation: It changes the auto commit mode for the current connection. If the performed transaction exists and the non auto commit mode is changed to the auto commit, it performs commit.
- Exception: It is as same as the exception which may occur during the commit process.

<a id="39c8b565df0e0c6a"></a>
#### setCatalog

```
void setCatalog(String catalog) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="ce9e23d41bf4ade6"></a>
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

<a id="edb152b0b299bfc8"></a>
#### setHoldability

```
void setHoldability(int holdability) throws SQLException
```

- Operation: It sets the ResultSet holdability which is generated by the statement generated from this object. If the method is not called, the default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="5535278f0d76b616"></a>
#### setNetworkTimeout

```
void setNetworkTimeout(Executor executor, int milliseconds) throws SQLException
```

- Operation: It sets the maximum time to wait for the connection or the object created from the connection to respond after a request to the database. If it can not get a response, then it is returned together with SQLException and the connection object is closed.
- Exception: If it is already closed, or an executor is null, or the millisecond is smaller than 0, then it throws SQLException. If a security manager exists and the corresponding checkPermission method rejects the setNetworkTimeout call, then it throws SecurityException.
- Since: 1.7

<a id="4a37d9fc79bc77d4"></a>
#### setReadOnly

```
void setReadOnly(boolean readOnly) throws SQLException
```

- Operation: It sets the read only property of the current session (connection). The default value is false.
- Exception: If it is already closed or an error is returned from the server, it throws SQLException.

<a id="cb3e54d41402f079"></a>
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

<a id="18d4b07e51518b9f"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

- Operation: It changes the transaction isolation for the current session (connection). The supported value is Connection.TRANSACTION_READ_COMMITED, Connection.TRANSACTION_READ_UNCOMMITTED, and Connection.TRANSACTION_SERIALIZABLE. Connection.READ_UNCOMMITTED is set to Connection.TRANSACTION_READ_COMMITED, and Connection.TRANSACTION_REPEATABLE_READ is set to Connection.TRANSACTION_SERIALIZABLE.
- Exception: If it is already closed or the level has the wrong value, it throws SQLException.

<a id="c4764b26a9a1634e"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="d68342c5952abf95"></a>
#### isWrapperFor

```
void isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether this object is a class which implements the iface interface. If it is, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper but it only queries only whether the given argument class type is implemented because GOLDILOCKS connection object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="0cf8126b1dd57f99"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS connection is not the wrapper of any other class. It returns itself after casting it to the corresponding type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of this object (if this object returns the unimplemented type), it throws SQLException.

<a id="4825ff55999ad94d"></a>
### ConnectionPoolDataSource

<a id="7259a328349a1070"></a>
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

<a id="eb5ecd17ae70cad8"></a>
### DatabaseMetaData

<a id="70241a4cd5cddd36"></a>
#### allProceduresAreCallable

```
boolean allProceduresAreCallable() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="66e1ab34c3a3f7b2"></a>
#### allTablesAreSelectable

```
boolean allTablesAreSelectable() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="2b368fb769c88d5f"></a>
#### autoCommitFailureClosesAllResultSets

```
boolean autoCommitFailureClosesAllResultSets() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="acfb72225930f730"></a>
#### dataDefinitionCausesTransactionCommit

```
boolean dataDefinitionCausesTransactionCommit() throws SQLException
```

- Operation: It always returns false because it does not automatically commit DDL statements at run-time.
- Exception: It does not occur.

<a id="42088b93b17c3839"></a>
#### dataDefinitionIgnoredInTransactions

```
boolean dataDefinitionIgnoredInTransactions() throws SQLException
```

- Operation: It always returns false, because DDL statements are included in a transaction.
- Exception: It does not occur.

<a id="37a4ac7339efc680"></a>
#### deletesAreDetected

```
boolean deletesAreDetected(int type) throws SQLException
```

- Operation: If type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="da1edaa1957cca28"></a>
#### doesMaxRowSizeIncludeBlobs

```
boolean doesMaxRowSizeIncludeBlobs() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="a1e1a73d59c28560"></a>
#### getAttributes

```
ResultSet getAttributes(String catalog, String schemaPattern, String typeNamePattern, String attributeNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="ef3d7d77ee5cbeff"></a>
#### getBestRowIdentifier

```
ResultSet getBestRowIdentifier(String catalog, String schema, String table, int scope, boolean nullable) throws SQLException
```

- Operation: It returns a ResultSet including one row consisting with rowid information because the rowid type is supported for all tables. If the table does not exist, it returns an empty ResultSet.
- Exception: If the table is null or an error is returned from the server, it throws SQLException.

<a id="3c62ef9a9f0ec38e"></a>
#### getCatalogs

```
ResultSet getCatalogs() throws SQLException
```

- Operation: It returns a ResultSet which has the catalog name in a column.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d9ad890158dc058d"></a>
#### getCatalogSeparator

```
String getCatalogSeparator() throws SQLException
```

- Operation: It returns a catalog separator character.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="b5712bfc99b79ee3"></a>
#### getCatalogTerm

```
String getCatalogTerm() throws SQLException
```

- Operation: It returns a catalog term character.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="1c66b75b3e669f41"></a>
#### getClientInfoProperties

```
ResultSet getClientInfoProperties() throws SQLException
```

- Operation: It returns a ResultSet including client information.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="366b5c460945b8f1"></a>
#### getColumnPrivileges

```
ResultSet getColumnPrivileges(String catalog, String schema, String table, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including column privilege information of the column in the table. If the table or the column corresponding to the column name pattern does not exist, it returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="95be0f423d8d028d"></a>
#### getColumns

```
ResultSet getColumns(String catalog, String schemaPattern, String tableNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including all column information of the table. If the table or the column corresponding to the column name pattern does not exist, it returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a882d6a99aee216c"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns the connection object which created the DatabaseMetaData object.
- Exception: It does not occur.

<a id="eaef7ebaa2a892a6"></a>
#### getCrossReference

```
ResultSet getCrossReference(String parentCatalog, String parentSchema, String parentTable, String foreignCatalog, String foreignSchema, String foreignTable) throws SQLException
```

- Operation: It returns a ResultSet including information of the foreign keys which refers to the given parent table in the given foreign key table. If reference relationship does not exist, it returns an empty ResultSet.
- Exception: If the foreign table or parent table is null or an error is returned from the server, it throws SQLException.

<a id="2c8ccbaf07649e2d"></a>
#### getDatabaseMajorVersion

```
int getDatabaseMajorVersion() throws SQLException
```

- Operation: It returns the major version of the product.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3de069bc5947aee0"></a>
#### getDatabaseMinorVersion

```
int getDatabaseMinorVersion() throws SQLException
```

- Operation: It returns the minor version of the product.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="233b50d58b498981"></a>
#### getDatabaseProductName

```
String getDatabaseProductName() throws SQLException
```

- Operation: It returns the product name.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="eb281142c2d9f854"></a>
#### getDatabaseProductVersion

```
String getDatabaseProductVersion() throws SQLException
```

- Operation: It returns the product version.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="6f937be38ff3f57f"></a>
#### getDefaultTransactionIsolation

```
int getDefaultTransactionIsolation() throws SQLException
```

- Operation: It returns the default transaction isolation. The default value which is set on the server is Connection.TRANSACTION_READ_COMMITTED.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="984bcce26afb55f6"></a>
#### getDriverMajorVersion

```
int getDriverMajorVersion() throws SQLException
```

- Operation: It returns the major version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="620c1d93d9c48e4e"></a>
#### getDriverMinorVersion

```
int getDriverMinorVersion() throws SQLException
```

- Operation: It returns the minor version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="c532f5171f7d55c6"></a>
#### getDriverName

```
String getDriverName() throws SQLException
```

- Operation: It returns "GOLDILOCKS JDBC Driver".
- Exception: It does not occur.

<a id="53a22acb285785d4"></a>
#### getDriverVersion

```
String getDriverVersion() throws SQLException
```

- Operation: It returns GOLDILOCKS JDBC driver version string. It includes the protocol version.
- Exception: It does not occur.

<a id="b781b196d6a2a380"></a>
#### getExportedKeys

```
ResultSet getExportedKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including foreign key information referring to the column in the given table.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="c6d83f97dd7a7421"></a>
#### getExtraNameCharacters

```
String getExtraNameCharacters() throws SQLException
```

- Operation: It returns "-$".
- Exception: It does not occur.

<a id="bdb38b1399f0a231"></a>
#### getFunctionColumns

```
ResultSet getFunctionColumns(String catalog, String schemaPattern, String functionNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a459f519022d303e"></a>
#### getFunctions

```
ResultSet getFunctions(String catalog, String schemaPattern, String functionNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="1717d948d0190982"></a>
#### getIdentifierQuoteString

```
String getIdentifierQuoteString() throws SQLException
```

- Operation: It returns an identifier quote character. The value that is set on the server is ".
- Exception: If an error is returned from the server, it throws SQLException.

<a id="af164a688d6e8b84"></a>
#### getImportedKeys

```
ResultSet getImportedKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including parent key information to which the foreign key column in the given table refers.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a413b836c390480b"></a>
#### getIndexInfo

```
ResultSet getIndexInfo(String catalog, String schema, String table, boolean unique, boolean approximate) throws SQLException
```

- Operation: It returns a ResultSet including index information of the given table. If unique is true, only unique index information is displayed. The approximate argument is ignored.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="985e8f5e2f77fea4"></a>
#### getJDBCMajorVersion

```
int getJDBCMajorVersion() throws SQLException
```

- Operation: It returns JDBC major version of GOLDILOCKS JDBC driver. It can vary depending on the jar file in use.
- Exception: It does not occur.

<a id="290d38c93d712870"></a>
#### getJDBCMinorVersion

```
int getJDBCMinorVersion() throws SQLException
```

- Operation: It returns JDBC minor version of GOLDILOCKS JDBC driver. It can vary depending on the jar file in use.
- Exception: It does not occur.

<a id="a4124789c0cdba5d"></a>
#### getMaxBinaryLiteralLength

```
int getMaxBinaryLiteralLength() throws SQLException
```

- Operation: It gets the maximum binary length from the server. 0 refers that the maximum length is infinite. 
- Exception: If an error is returned from the server, it throws SQLException.

<a id="53f5cd80d1d1dede"></a>
#### getMaxCatalogNameLength

```
int getMaxCatalogNameLength() throws SQLException
```

- Operation: It gets the maximum length of the catalog name from the server. 0 refers that the maximum length is infinite. 
- Exception: If an error is returned from the server, it throws SQLException.

<a id="f24ccc8271965832"></a>
#### getMaxCharLiteralLength

```
int getMaxCharLiteralLength() throws SQLException
```

- Operation: It gets the maximum literal length from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2f542258500258fe"></a>
#### getMaxColumnNameLength

```
int getMaxColumnNameLength() throws SQLException
```

- Operation: It gets the maximum length of the column name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="b8d41dbe2c83393d"></a>
#### getMaxColumnsInGroupBy

```
int getMaxColumnsInGroupBy() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in *group by* clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="35aa87899783e81a"></a>
#### getMaxColumnsInIndex

```
int getMaxColumnsInIndex() throws SQLException
```

- Operation: It gets the maximum number of columns available to use as the index from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d7c6d1662afb4f20"></a>
#### getMaxColumnsInOrderBy

```
int getMaxColumnsInOrderBy() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in *order by* clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="c57cf9d39ef9adfd"></a>
#### getMaxColumnsInSelect

```
int getMaxColumnsInSelect() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in select target clause from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d67791139bc38bb2"></a>
#### getMaxColumnsInTable

```
int getMaxColumnsInTable() throws SQLException
```

- Operation: It gets the maximum number of columns available to use in the table from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3325e11cb398dbfa"></a>
#### getMaxConnections

```
int getMaxConnections() throws SQLException
```

- Operation: It gets the maximum number of connection to the server from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="8c5311835351c1b6"></a>
#### getMaxCursorNameLength

```
int getMaxCursorNameLength() throws SQLException
```

- Operation: It gets the maximum length of the cursor name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="2da88d5aaeccdcf2"></a>
#### getMaxIndexLength

```
int getMaxIndexLength() throws SQLException
```

- Operation: It gets the maximum size for a single index key from the server.
- Exception: If an error is returned from the server, it throws SQLException.

> The JDBC specification defines that the available maximum size of a single index is returned in bytes, but its value is meaningless, because index size does not have limit. It operates in this way for it to have the same meaning as ODBC.

<a id="d489a0645ffba5de"></a>
#### getMaxProcedureNameLength

```
int getMaxProcedureNameLength() throws SQLException
```

- Operation: It gets the maximum length of the procedure name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="52ef1e81e4436534"></a>
#### getMaxRowSize

```
int getMaxRowSize() throws SQLException
```

- Operation: It gets the maximum number of rows in a table from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d9aeff42e381823c"></a>
#### getMaxSchemaNameLength

```
int getMaxSchemaNameLength() throws SQLException
```

- Operation: It gets the maximum length of the schema name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0d029a3c7bb8d42c"></a>
#### getMaxStatementLength

```
int getMaxStatementLength() throws SQLException
```

- Operation: It gets the maximum string length of an SQL statement from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="01de80075456a60b"></a>
#### getMaxStatements

```
int getMaxStatements() throws SQLException
```

- Operation: It gets the maximum number of statements which can be open at once from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="9e9d13b3feda5cdc"></a>
#### getMaxTableNameLength

```
int getMaxTableNameLength() throws SQLException
```

- Operation: It gets the maximum string length of the table name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="075d6dcbdf2f9ffb"></a>
#### getMaxTablesInSelect

```
int getMaxTablesInSelect() throws SQLException
```

- Operation: It gets the maximum number of tables which can be used in the select statement from the server. 0 refers that the maximum number is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="dc469f428f41b633"></a>
#### getMaxUserNameLength

```
int getMaxUserNameLength() throws SQLException
```

- Operation: It gets the maximum string length of the user name from the server. 0 refers that the maximum length is infinite.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="cfb5509fdb0464ca"></a>
#### getNumericFunctions

```
String getNumericFunctions() throws SQLException
```

- Operation: It gets a list of numeric-related functions corresponding to SQL standard from the server. Each function name is distinguished by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a9dded42fdfd8622"></a>
#### getPrimaryKeys

```
ResultSet getPrimaryKeys(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns a ResultSet including all primary keys in a given table.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="21caab6c7255c943"></a>
#### getProcedureColumns

```
ResultSet getProcedureColumns(String catalog, String schemaPattern, String procedureNamePattern, String columnNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including column information corresponding to the given name pattern for a given procedure.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="20dc23b0cfd676a6"></a>
#### getProcedures

```
ResultSet getProcedures(String catalog, String schemaPattern, String procedureNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including procedure information of a given name pattern.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="93b1400981f0fc36"></a>
#### getProcedureTerm

```
String getProcedureTerm() throws SQLException
```

- Operation: It gets the keyword which refers to the procedure from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="de0c01641ac28a85"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- Operation: It returns the default holdability property of ResultSet. It is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: It does not occur.

<a id="07f823c9a7646b21"></a>
#### getRowIdLifetime

```
RowIdLifetime getRowIdLifetime() throws SQLException
```

- Operation: It always returns RowIdLifetime.ROWID_VALID_FOREVER.
- Exception: It does not occur.

<a id="4e9924e96241cf3e"></a>
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

<a id="b4561ba460ed106a"></a>
#### getSchemaTerm

```
String getSchemaTerm() throws SQLException
```

- Operation: It gets the keyword which refers to the schema from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="283c8a8ee16d726f"></a>
#### getSearchStringEscape

```
String getSearchStringEscape() throws SQLException
```

- Operation: It returns the escape characters used in *like* clause as a string.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="80050de47ee070d4"></a>
#### getSQLKeywords

```
String getSQLKeywords() throws SQLException
```

- Operation: It returns the keywords which can not be used in SQL statement, separated by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="fc461d010982dbda"></a>
#### getSQLStateType

```
int getSQLStateType() throws SQLException
```

- Operation: It always returns DatabaseMetaData.sqlStateSQL99.
- Exception: It does not occur.

<a id="e8d58205e0a67f6d"></a>
#### getStringFunctions

```
String getStringFunctions() throws SQLException
```

- Operation: It gets a list of functions which handle the strings and corresponds to SQL standard. Each function name is distinguished by comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0daee45ce08d66fc"></a>
#### getSuperTables

```
ResultSet getSuperTables(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="be3b58283ac9b421"></a>
#### getSuperTypes

```
ResultSet getSuperTypes(String catalog, String schemaPattern, String typeNamePattern) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="5429d1f1ae5ba2be"></a>
#### getSystemFunctions

```
String getSystemFunctions() throws SQLException
```

- Operation: It gets a list of system functions corresponding to SQL standard. Each function name is separated by the comma (,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="b7d7a60723e56ee7"></a>
#### getTablePrivileges

```
ResultSet getTablePrivileges(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- Operation: It returns a ResultSet including privilege information of all tables which satisfy the condition.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="88ff2260ca5f933f"></a>
#### getTables

```
ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types) throws SQLException
```

- Operation: It returns a ResultSet including information of all tables which satisfy the condition.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="4cb90033259014b7"></a>
#### getTableTypes

```
ResultSet getTableTypes() throws SQLException
```

- Operation: It returns a ResultSet containing information of all table types.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="9e2a6eaeb5bebc09"></a>
#### getTimeDateFunctions

```
String getTimeDateFunctions() throws SQLException
```

- Operation: It gets functions which are related to time and date and corresponds to SQL standard. Each function name is separated by the comma(,).
- Exception: If an error is returned from the server, it throws SQLException.

<a id="e9d8b165be6fa025"></a>
#### getTypeInfo

```
ResultSet getTypeInfo() throws SQLException
```

- Operation: It returns a ResultSet including information of the data type.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="a6346bbe7e0a58cb"></a>
#### getUDTs

```
ResultSet getUDTs(String catalog, String schemaPattern, String typeNamePattern, int[] types) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="59b03601c5dd21a9"></a>
#### getURL

```
String getURL() throws SQLException
```

- Operation: It returns the URL used to connect to the server.
- Exception: It does not occur.

<a id="600906ed6bd07cbb"></a>
#### getUserName

```
String getUserName() throws SQLException
```

- Operation: It returns the current user name which maintains a session.
- Exception: If an error is returned from the server, it throws SQLException.

> A user name may be different from the user name used to connect firstly because the user can be changed during a session.

<a id="a52f803c0f4e715a"></a>
#### getVersionColumns

```
ResultSet getVersionColumns(String catalog, String schema, String table) throws SQLException
```

- Operation: It returns an empty ResultSet.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="ed8235ecf07217ee"></a>
#### insertsAreDetected

```
boolean insertsAreDetected(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="79b750c4238fc9b4"></a>
#### isCatalogAtStart

```
boolean isCatalogAtStart() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="e6181e80f390c4e2"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

- Operation: It gets the information whether the current connection is the read only mode from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="886e26d6b84188da"></a>
#### locatorsUpdateCopy

```
boolean locatorsUpdateCopy() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="8cafc7f982ac7cb3"></a>
#### nullPlusNonNullIsNull

```
boolean nullPlusNonNullIsNull() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="c40cba1d9943b917"></a>
#### nullsAreSortedAtEnd

```
boolean nullsAreSortedAtEnd() throws SQLException
```

- Operation: It always returns false. It does not separately sort null.
- Exception: It does not occur.

<a id="e11548a1e41526bf"></a>
#### nullsAreSortedAtStart

```
boolean nullsAreSortedAtStart() throws SQLException
```

- Operation: It always returns false. It does not separately sort null.
- Exception: It does not occur.

<a id="4e524b19d4267ffe"></a>
#### nullsAreSortedHigh

```
boolean nullsAreSortedHigh() throws SQLException
```

- Operation: It always returns true. Null is positioned at last by default.
- Exception: It does not occur.

<a id="3dedfe718aa0a1e3"></a>
#### nullsAreSortedLow

```
boolean nullsAreSortedLow() throws SQLException
```

- Operation: It always returns false. Null is positioned at last by default.
- Exception: It does not occur.

<a id="b2bcc7512ba72df5"></a>
#### othersDeletesAreVisible

```
boolean othersDeletesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="e6ed8d134de8d926"></a>
#### othersInsertsAreVisible

```
boolean othersInsertsAreVisible(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="1a0703674c871ef7"></a>
#### othersUpdatesAreVisible

```
boolean othersUpdatesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="234a065dff211b47"></a>
#### ownDeletesAreVisible

```
boolean ownDeletesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="e03f087d8d7a4dd5"></a>
#### ownInsertsAreVisible

```
boolean ownInsertsAreVisible(int type) throws SQLException
```

- Operation: It always returns false regardless of the type.
- Exception: It does not occur.

<a id="fdab3a1bd612c4e1"></a>
#### ownUpdatesAreVisible

```
boolean ownUpdatesAreVisible(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="2704e89963a0a0dc"></a>
#### storesLowerCaseIdentifiers

```
boolean storesLowerCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="b2937f5737ca8cb2"></a>
#### storesLowerCaseQuotedIdentifiers

```
boolean storesLowerCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="999712bb5072e9fd"></a>
#### storesMixedCaseIdentifiers

```
boolean storesMixedCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="6a12d7094ec62d16"></a>
#### storesMixedCaseQuotedIdentifiers

```
boolean storesMixedCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="1a1cd0acc17acbc6"></a>
#### storesUpperCaseIdentifiers

```
boolean storesUpperCaseIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="c7cee66857aa8e4d"></a>
#### storesUpperCaseQuotedIdentifiers

```
boolean storesUpperCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="276f085c264ae213"></a>
#### supportsAlterTableWithAddColumn

```
boolean supportsAlterTableWithAddColumn() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="c19d1856a8a9619b"></a>
#### supportsAlterTableWithDropColumn

```
boolean supportsAlterTableWithDropColumn() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="42eec261a86afebd"></a>
#### supportsANSI92EntryLevelSQL

```
boolean supportsANSI92EntryLevelSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="fe6e381563e07cd1"></a>
#### supportsANSI92FullSQL

```
boolean supportsANSI92FullSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="cd62ac5d09e698b8"></a>
#### supportsANSI92IntermediateSQL

```
boolean supportsANSI92IntermediateSQL() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="d8b27e824b4d3a73"></a>
#### supportsBatchUpdates

```
boolean supportsBatchUpdates() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="7c893dd216c9fdc0"></a>
#### supportsCatalogsInDataManipulation

```
boolean supportsCatalogsInDataManipulation() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="2fdba7a6ce87a863"></a>
#### supportsCatalogsInIndexDefinitions

```
boolean supportsCatalogsInIndexDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="3303d109ebef6afa"></a>
#### supportsCatalogsInPrivilegeDefinitions

```
boolean supportsCatalogsInPrivilegeDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="7fd7b572e8a32bd1"></a>
#### supportsCatalogsInProcedureCalls

```
boolean supportsCatalogsInProcedureCalls() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="a38443b342e329ab"></a>
#### supportsCatalogsInTableDefinitions

```
boolean supportsCatalogsInTableDefinitions() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="238354d311571c9b"></a>
#### supportsColumnAliasing

```
boolean supportsColumnAliasing() throws SQLException
```

- Operation: It gets information whether to support the column aliasing from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="e42cda2c5e68e19d"></a>
#### supportsConvert

```
boolean supportsConvert() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="739e6082e7e0f521"></a>
#### supportsConvert

```
boolean supportsConvert(int fromType, int toType) throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="4d32aeb97311eb58"></a>
#### supportsCoreSQLGrammar

```
boolean supportsCoreSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="04adbab62c5c8355"></a>
#### supportsCorrelatedSubqueries

boolean supportsCorrelatedSubqueries() throws SQLException

- Operation: It always returns true.
- Exception: It does not occur.

<a id="7a8a364bb81be13c"></a>
#### supportsDataDefinitionAndDataManipulationTransactions

```
boolean supportsDataDefinitionAndDataManipulationTransactions() throws SQLException
```

- Operation: It always returns true. It can perform DML and DDL with a single transaction.
- Exception: It does not occur.

<a id="096f1bc972d672f7"></a>
#### supportsDataManipulationTransactionsOnly

```
boolean supportsDataManipulationTransactionsOnly() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="d3fd0897f22184c9"></a>
#### supportsDifferentTableCorrelationNames

```
boolean supportsDifferentTableCorrelationNames() throws SQLException
```

- Operation: It gets information whether the table correlation name should be different from the table name from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="3e0b2072ff240a30"></a>
#### supportsExpressionsInOrderBy

```
boolean supportsExpressionsInOrderBy() throws SQLException
```

- Operation: It gets information whether the calculation can be used in *order by* clause from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="16b89826185d6b3c"></a>
#### supportsExtendedSQLGrammar

```
boolean supportsExtendedSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="57c200b51dad25d7"></a>
#### supportsFullOuterJoins

```
boolean supportsFullOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="868dde7316d27efc"></a>
#### supportsGetGeneratedKeys

```
boolean supportsGetGeneratedKeys() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="be1c3a41998d5c84"></a>
#### supportsGroupBy

```
boolean supportsGroupBy() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="7a8db098c72deab4"></a>
#### supportsGroupByBeyondSelect

```
boolean supportsGroupByBeyondSelect() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="738e5d3ee89ad478"></a>
#### supportsGroupByUnrelated

```
boolean supportsGroupByUnrelated() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="d4241c73f8b2666d"></a>
#### supportsIntegrityEnhancementFacility

```
boolean supportsIntegrityEnhancementFacility() throws SQLException
```

- Operation: It gets information whether to support SQL integrity enhancing feature from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="793addecf88cb5e3"></a>
#### supportsLikeEscapeClause

```
boolean supportsLikeEscapeClause() throws SQLException
```

- Operation: It gets information whether to support escape clause in like statement from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="f562cc263d975c24"></a>
#### supportsLimitedOuterJoins

```
boolean supportsLimitedOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="81a647b9f16ea99d"></a>
#### supportsMinimumSQLGrammar

```
boolean supportsMinimumSQLGrammar() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="68014077c60af67e"></a>
#### supportsMixedCaseIdentifiers

```
boolean supportsMixedCaseIdentifiers() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="c874a6aa25a61ee2"></a>
#### supportsMixedCaseQuotedIdentifiers

```
boolean supportsMixedCaseQuotedIdentifiers() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="7c1032f432ddd030"></a>
#### supportsMultipleOpenResults

```
boolean supportsMultipleOpenResults() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="7275e0b468789ad0"></a>
#### supportsMultipleResultSets

```
boolean supportsMultipleResultSets() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="d4776562085cad55"></a>
#### supportsMultipleTransactions

```
boolean supportsMultipleTransactions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="07a8b6674d665a75"></a>
#### supportsNamedParameters

```
boolean supportsNamedParameters() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="2e0a2a0da9f69055"></a>
#### supportsNonNullableColumns

```
boolean supportsNonNullableColumns() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="83a9289f13e3253d"></a>
#### supportsOpenCursorsAcrossCommit

```
boolean supportsOpenCursorsAcrossCommit() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="c959ae749b8e4c46"></a>
#### supportsOpenCursorsAcrossRollback

```
boolean supportsOpenCursorsAcrossRollback() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="50190f222c100699"></a>
#### supportsOpenStatementsAcrossCommit

```
boolean supportsOpenStatementsAcrossCommit() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="2abe7970ea933edd"></a>
#### supportsOpenStatementsAcrossRollback

```
boolean supportsOpenStatementsAcrossRollback() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="1c9cf376a47b2058"></a>
#### supportsOrderByUnrelated

```
boolean supportsOrderByUnrelated() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="012a0f081b0116b8"></a>
#### supportsOuterJoins

```
boolean supportsOuterJoins() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="6a1f8dc17fdb8665"></a>
#### supportsPositionedDelete

```
boolean supportsPositionedDelete() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="00a76160d04fa5f6"></a>
#### supportsPositionedUpdate

```
boolean supportsPositionedUpdate() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="c4a13c55b5e8982c"></a>
#### supportsResultSetConcurrency

```
boolean supportsResultSetConcurrency(int type, int concurrency) throws SQLException
```

- Operation: It returns true for all ResultSet types and all concurrency. It returns false for the invalid arguments.
- Exception: It does not occur.

<a id="921661f2453d6720"></a>
#### supportsResultSetHoldability

```
boolean supportsResultSetHoldability(int holdability) throws SQLException
```

- Operation: If the holdability is ResultSet.CLOSE_CURSORS_AT_COMMIT or ResultSet.HOLD_CURSORS_OVER_COMMIT, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="09f68ccdb43c4779"></a>
#### supportsResultSetType

```
boolean supportsResultSetType(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_FORWARD_ONLY, ResultSet.TYPE_SCROLL_INSENSITIVE or ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="3711ee88370235ab"></a>
#### supportsSavepoints

```
boolean supportsSavepoints() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5f4d5050fb3178f0"></a>
#### supportsSchemasInDataManipulation

```
boolean supportsSchemasInDataManipulation() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="a687f10821b11f66"></a>
#### supportsSchemasInIndexDefinitions

```
boolean supportsSchemasInIndexDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="04326e8d4969b85d"></a>
#### supportsSchemasInPrivilegeDefinitions

```
boolean supportsSchemasInPrivilegeDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="0b0a7d930940d785"></a>
#### supportsSchemasInProcedureCalls

```
boolean supportsSchemasInProcedureCalls() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="9b8d7d6364e6ec12"></a>
#### supportsSchemasInTableDefinitions

```
boolean supportsSchemasInTableDefinitions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="c08af0ba09ecc668"></a>
#### supportsSelectForUpdate

```
boolean supportsSelectForUpdate() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="ded74fffd8d4c31b"></a>
#### supportsStatementPooling

```
boolean supportsStatementPooling() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="66b4079553f229d5"></a>
#### supportsStoredFunctionsUsingCallSyntax

```
boolean supportsStoredFunctionsUsingCallSyntax() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="4fa391ca22fb1177"></a>
#### supportsStoredProcedures

```
boolean supportsStoredProcedures() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="7d4180ca45e37ca1"></a>
#### supportsSubqueriesInComparisons

```
boolean supportsSubqueriesInComparisons() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="5e16cf6992d8d473"></a>
#### supportsSubqueriesInExists

```
boolean supportsSubqueriesInExists() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="a41cf3620fc09653"></a>
#### supportsSubqueriesInIns

```
boolean supportsSubqueriesInIns() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="571e6503f482fc45"></a>
#### supportsSubqueriesInQuantifieds

```
boolean supportsSubqueriesInQuantifieds() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="320febd8d692c597"></a>
#### supportsTableCorrelationNames

```
boolean supportsTableCorrelationNames() throws SQLException
```

- Operation: It gets information whether to support the table correlation name from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="43518ab307940558"></a>
#### supportsTransactionIsolationLevel

```
boolean supportsTransactionIsolationLevel(int level) throws SQLException
```

- Operation: It gets information whether to support the transaction isolation level from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="d37c4306f516421c"></a>
#### supportsTransactions

```
boolean supportsTransactions() throws SQLException
```

- Operation: It always returns true.
- Exception: It does not occur.

<a id="ccaa1c1e6618f14b"></a>
#### supportsUnion

```
boolean supportsUnion() throws SQLException
```

- Operation: It gets information whether to support the union operation from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="0de09dd0230f4cea"></a>
#### supportsUnionAll

```
boolean supportsUnionAll() throws SQLException
```

- Operation: It gets information whether to support the union all operation from the server.
- Exception: If an error is returned from the server, it throws SQLException.

<a id="fbaafb2717a59a8a"></a>
#### updatesAreDetected

```
boolean updatesAreDetected(int type) throws SQLException
```

- Operation: If the type is ResultSet.TYPE_SCROLL_SENSITIVE, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="928a1c55223f5a21"></a>
#### usesLocalFilePerTable

```
boolean usesLocalFilePerTable() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="ab66fbe4f7fa6bfd"></a>
#### usesLocalFiles

```
boolean usesLocalFiles() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="4d253460259583ae"></a>
### DataSource

<a id="3ce8096ef1ed1f03"></a>
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

<a id="fc8ffb91b6bf1f1a"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: This class is not implemented as the wrapper of any other class. If the object is an instance of iface, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="1f323d60bf5863cd"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It returns *this* because this class is not implemented as the wrapper of any other class.
- Exception: If the object is not an instance of iface, it throws SQLException.

<a id="b60dcb240a2b63f7"></a>
### Driver

<a id="ad16ac7525928290"></a>
#### acceptsURL

```
boolean acceptsURL(String url) throws SQLException
```

- Operation: If the url is not null and it starts with "jdbc:goldilocks:", it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="a60fb6234b593b24"></a>
#### connect

```
Connection connect(String url, Properties info) throws SQLException
```

- Operation: It creates and returns a new connection object. The url should include the server address, DB name and port.
- Exception: If the url is invalid or the connection from the server fails, it throws SQLException.

<a id="45b609b868931284"></a>
#### getMajorVersion

```
int getMajorVersion() throws SQLException
```

- Operation: It returns the major version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="4533291387d6d43f"></a>
#### getMinorVersion

```
int getMinorVersion() throws SQLException
```

- Operation: It returns the minor version of GOLDILOCKS JDBC driver.
- Exception: It does not occur.

<a id="e26ef5eb07b1a141"></a>
#### getPropertyInfo

```
DriverPropertyInfo[] getPropertyInfo(String url, Properties info) throws SQLException
```

- Operation: It gets the list of available property when GOLDILOCKS JDBC driver is connected.
- Exception: It does not occur.

<a id="ff766bd9977e115b"></a>
#### jdbcCompliant

```
boolean jdbcCompliant() throws SQLException
```

- Operation: It always returns false.
- Exception: It does not occur.

<a id="f229a67ac9732f98"></a>
### NClob

This class is not implemented.

<a id="f8f589f9d58c85a6"></a>
#### free

```
void free() throws SQLException
```

<a id="224fb8825d01d521"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

<a id="6be4d6a600a57085"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

<a id="f574ad49f7f14abc"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

<a id="c16e6b10343ef3c6"></a>
#### length

```
long length() throws SQLException
```

<a id="f670bca8bd83fffb"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

```
long position(String searchstr, long start) throws SQLException
```

<a id="1844ed134997ef45"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

<a id="fb482e03c679114f"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

<a id="c0ed76d4c899d8b7"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

<a id="2d3273bbc651599d"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="c9f9039706c32f42"></a>
### ParameterMetaData

ParameterMetaData object is returned by PreparedStatement.getParameterMetaData(). The parameterMetaData of the GOLDILOCKS JDBC does not use the actual DB information but it is based on the basic type varchar for other information (such as type, etc.) except for in/out. It is because in/out is the only information got from the server on the parameter after prepared. For example, if it is prepared with the query statement which is "Select * from t1 where a =?", the parameter type used in the condition clause is not determined. The server generally assumes it a varchar type.

<a id="e92baa338b846914"></a>
#### getParameterClassName

```
String getParameterClassName(int param) throws SQLException
```

- Operation: It returns java.lang.String. The parameter type is regarded as varchar.
- Exception: If the param value exceeds the range of the number of parameters, it throws SQLException.

<a id="d9e84a716bd9d89f"></a>
#### getParameterCount

```
int getParameterCount() throws SQLException
```

- Operation: It returns the number of parameters. It is also the number of ? used in the query statement.
- Exception: It does not occur.

<a id="ede88f3cf1aab965"></a>
#### getParameterMode

```
int getParameterMode(int param) throws SQLException
```

- Operation: It returns the in/out mode of the param-th parameter. It returns one of ParameterMetaData.parameterModeIn, ParameterMetaData.parameterModeInOut, ParameterMetaData.parameterModeOut, or ParameterMetaData.parameterModeUnknown. The case of returning parameterModeUnknown value does not exist until now.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="23cf97f2c61b9d20"></a>
#### getParameterType

```
int getParameterType(int param) throws SQLException
```

- Operation: It returns Types.VARCHAR for all parameters.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="4371777b86f6ae57"></a>
#### getParameterTypeName

```
String getParameterTypeName(int param) throws SQLException
```

- Operation: It returns "VARCHAR" for all parameters.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="39abed891d51ad95"></a>
#### getPrecision

```
int getPrecision(int param) throws SQLException
```

- Operation: It returns 4000 for all parameters. The parameter is regarded as varchar(4000) by default.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="b7c7615a2fa5e986"></a>
#### getScale

```
int getScale(int param) throws SQLException
```

- Operation: It returns 0 for all parameters. The parameter is regarded as varchar(4000) by default.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="029cccfefc377d86"></a>
#### isNullable

```
int isNullable(int param) throws SQLException
```

- Operation: It always returns ParameterMetaData.parameterNullableUnknown.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="a02a94f8fa5a63b3"></a>
#### isSigned

```
boolean isSigned(int param) throws SQLException
```

- Operation: It always returns false.
- Exception: If the param value exceeds range of the number of parameters, it throws SQLException.

<a id="034516ff2c63c890"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It enquires if it the object is an instance of iface. If so, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="858c053e87b50a72"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: If the object is an instance of iface, it casts this object to iface type and returns it.
- Exception: If the object is not an instance of iface, it throws SQLException.

<a id="9a6888831b46d40b"></a>
### PooledConnection

<a id="a9a958d64c4a3448"></a>
#### addConnectionEventListener

```
void addConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- Operation: It registers the ConnectionEventListener object. After then, if close() of the connection object (logical connection) which is returned from PooledConnection is called or the actual connection is broken, ConnectionEvent is generated to the registered listeners.
- Exception: It does not occur.

<a id="ab9e316a680a828e"></a>
#### addStatementEventListener

```
void addStatementEventListener(StatementEventListener listener) throws SQLException
```

- Operation: It does not perform any operation. GOLDILOCKS JDBC driver does not implement the method. Statement pooling feature is performed by the external middleware.
- Exception: It does not occur.

<a id="5d393c681f806cae"></a>
#### close

```
void close() throws SQLException
```

- Operation: It calls close() of the physical connection that the object has.
- Exception: It may occur in close() of physical connection.

<a id="45cd862b355c3e40"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns logical connection owned by the object.
- Exception: It does not occur.

<a id="8293c6dca0a5b1e8"></a>
#### removeConnectionEventListener

```
void removeConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- Operation: It removes the registered ConnectionEventListener. After then, ConnectionEvent is not transferred to this listener.
- Exception: It does not occur.

<a id="ac6a860db7bde4f5"></a>
#### removeStatementEventListener

```
void removeStatementEventListener(StatementEventListener listener) throws SQLException
```

- Operation: It does not perform any operation.
- Exception: It does not occur.

<a id="197da4e8d4db3bd2"></a>
### PreparedStatement

<a id="749f6e23a9af86fc"></a>
#### addBatch

```
void addBatch() throws SQLException
```

- Operation: It registers the currently bound data as batch job. If any of this batch job is registered, an error occurs when performing execute (), executeUpdate (), executeQuery () execution. If any one is not bound for the parameter, an error occurs. After addBatch if another addBatch is performed again at the state without binding with the method of setXXX () type, it registers the batch job as the previously bound value.
- Exception: If a parameter which has never been bound exists, it throws an exception.

<a id="9dc87833942d2e60"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

- Operation: It removes all of currently bound data and information. But if at least one batch job is registered, operation is not performed.
- Exception: It does not occur.

<a id="75c006ecb6e5c15b"></a>
#### execute

```
boolean execute() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter. If the executed statement is the select statement, it returns true and gets a ResultSet from the object. Otherwise, it returns false.
- Exception: If the batch job is registered, the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="9ece10894e42c6e7"></a>
#### executeQuery

```
ResultSet executeQuery() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter and fetches, then creates and returns a ResultSet object.
- Exception: If the batch job is registered or the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="a2bec8c4f32edd90"></a>
#### executeUpdate

```
int executeUpdate() throws SQLException
```

- Operation: It executes the prepared statement based on the bound data to the current parameter. It returns the number of updated records. If updated record with DDL statements does not exist, it returns 0.
- Exception: If the batch job is registered or the statement is not a select statement or the bound parameters are insufficient or an error occurs on the server when executing, it throws an exception.

<a id="48b84e1871631f78"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- Operation: It gets ResultSetMetaData object. If the prepared statement is not the select statement (It is the statement which does not return ResultSet), it returns an empty ResultSetMetaData. The method can be called before executing.
- Exception: If an error occurs on the server, it throws an exception.

<a id="7bad7acf8b3fc2e2"></a>
#### getParameterMetaData

```
ParameterMetaData getParameterMetaData() throws SQLException
```

- Operation: It gets the ParameterMetaData object. It can be called before executing. However, all parameters are assumed to be varchar(4000) because information about the exact parameter type is not known to the server.
- Exception: If an error occurs on the server, it throws an exception.

<a id="afa506f8450184a4"></a>
#### setArray

```
void setArray(int parameterIndex, Array x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="80b987c591ba10b2"></a>
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

- Operation: It binds the InputStream object to the parameter index as LONG VARCHAR type. It does not execute the encoding operation because the input data is a binary form. It does not consider the character set and and assumes it as ascii data. If English data is inserted or the server client character set environment is identical, this method is faster than setCharacterStream or setString when inserting the data as varchar.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setAsciiStream(int parameterIndex, InputStream x, long length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARCHAR type. It does not execute the encoding operation because the input data is a binary form. It does not consider the character set and assumes it as ascii data. If English data is inserted or the server client character set environment is identical, this method is faster than setCharacterStream or setString when inserting the data as varchar.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="9a98a26b46743bba"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

- Operation: It binds the BigDecimal object to the parameter index as NUMBER type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="8167cf465edeb002"></a>
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

<a id="cef8b6fb8a9d9a9c"></a>
#### setBlob

```
void setBlob(int parameterIndex, Blob x) throws SQLException
```

- Operation: It binds the blob object to the parameter index as LONG VARBINARY type.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

```
void setBlob(int parameterIndex, InputStream inputStream) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARBINARY type.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

```
void setBlob(int parameterIndex, InputStream inputStream, long length) throws SQLException
```

- Operation: It binds the InputStream object to the parameter index as LONG VARBINARY type. The number of characters included in InputStream is as many as the length.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

<a id="dfe33641a5d66340"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

- Operation: It binds the data x to the parameter index as BOOLEAN type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="dcfe60376d8e767e"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_SMALLINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="74fb95108cf05991"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

- Operation: It binds the data x to the parameter index as VARBINARY or LONG VARBINARY type. If the length of x is equal to or smaller than 4000, it is bound as VARBINARY, and if it is bigger than 4000, it is bound as LONG VARBINARY type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="35a2be5d41fba3b1"></a>
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

<a id="8b00ac86feb7cb0a"></a>
#### setClob

```
void setClob(int parameterIndex, Clob x) throws SQLException
```

- Operation: It binds the clob object to the parameter index as LONG VARCHAR type.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

```
void setClob(int parameterIndex, Reader reader) throws SQLException
```

- Operation: It binds the reader object to the parameter index as LONG VARCHAR type.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

```
void setClob(int parameterIndex, Reader reader, long length) throws SQLException
```

- Operation: It binds the reader object to the parameter index as LONG VARCHAR type. The number of characters included in reader is as many as the length.
- Exception: If parameterIndex is smaller than 0 or it is bigger than the number of parameters, it throws SQLException.

<a id="717dbe18c2cc0059"></a>
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

<a id="9b157d4fad0959ce"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_DOUBLE type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="335dff71c670fd7a"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_REAL type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="e14ed89cb7a10c10"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_INTEGER type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="10ae85cf816dbfeb"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_BIGINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="cbf41022d6060560"></a>
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

<a id="80a9edfb43e308b1"></a>
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

<a id="9a984682c0f228d3"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="97843f71c7125deb"></a>
#### setNull

```
void setNull(int parameterIndex, int sqlType) throws SQLException
```

- Operation: It binds null to the parameter index as GOLDILOCKS type corresponding to sqlType. For more information about GOLDILOCKS type mapped to sqlType, refer to [SQL types → GOLDILOCKS types](#e2eaca60f3630d26).
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

```
void setNull(int parameterIndex, int sqlType, String typeName) throws SQLException
```

- Operation: It binds null to the parameter index as GOLDILOCKS type corresponding to sqlType type. For more information about GOLDILOCKS type mapped to sqlType, refer to [SQL types → GOLDILOCKS types](#e2eaca60f3630d26). The third argument, typeName, is ignored because REF or the user type is not supported.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="a4535ff378608ee8"></a>
#### setObject

```
void setObject(int parameterIndex, Object x) throws SQLException
```

- Operation: It binds the data x to the parameter index as the mapped GOLDILOCKS type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

**Java objects → GOLDILOCKS types**

<a id="694f851c65f23d77"></a>
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

- Operation: It binds the data x to the parameter index as GOLDILOCKS type corresponding to targetSqlType. For more information about GOLDILOCKS type mapped to targetSqlType, refer to [SQL types → GOLDILOCKS types](#e2eaca60f3630d26).
- Exception: It occurs if parameterIndex is smaller than 0 or it is greater than the number of parameters.

```
void setObject(int parameterIndex, Object x, int targetSqlType, int scaleOrLength) throws SQLException
```

- Operation: It binds the data x to the parameter index as GOLDILOCKS type corresponding to targetSqlType. For more information about GOLDILOCKS type mapped to targetSqlType, refer to [SQL types → GOLDILOCKS types](#e2eaca60f3630d26). If x is InputStream or Reader then scaleOrLength indicates the data length. For other types this value is ignored.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="0737cb98830f7ff0"></a>
#### setRef

```
void setRef(int parameterIndex, Ref x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="95c6c917a2cb8b50"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

- Operation: It binds the data x to the parameter index as ROWID type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="53e7aa0c05ec5909"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

- Operation: It binds the data x to the parameter index as NATIVE_SMALLINT type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="b032c18352b5e68b"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="05bd8a179ed285d8"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

- Operation: It binds the data x to the parameter index as VARCHAR or LONG VARCHAR type. If the length of x is equal to or smaller than 4000, it is bound as VARCHAR, and if it is bigger than 4000, it is bound as LONG VARCHAR type.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

<a id="dea9992539afc93b"></a>
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

<a id="1b285198e3371ce3"></a>
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

<a id="94f87da9f976137c"></a>
#### setUnicodeStream

```
void setUnicodeStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- Operation: It is not implemented. (It is a deprecated method.)
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="48b95714361dbc66"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

- Operation: It is not implemented.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="15db9001f4f21c02"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether this object is the class implementing the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS PreparedStatement object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="ca27d6ea7df4118e"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself even when it is unwrapped because GOLDILOCKS PreparedStatement is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not this object type (The type which is not implemented by this object is given), it throws SQLException.

<a id="ebffdd0d2536e154"></a>
#### executeBatchAtomic

```
boolean executeBatchAtomic() throws SQLException
```

- Operation: It is identical to executeBatch(), but it is atomically executed. The batch job is either entirely succeeded or failed. It is performed faster than executeBatch(). If the executed statement is the select statement, it returns true, otherwise, it returns false.
- Exception: If batch job is not registered or an error occurs on the server, it throws SQLException.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).executeBatchAtomic();

<a id="40180ea95c43ba0f"></a>
#### setTimeTimeZone

```
void setTimeTimeZone(int parameterIndex, Time x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIME WITH TIME ZONE type. Time x is regarded as timezone of cal. Timezone information for DB column refers to timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, aTime, aCalendar);

<a id="1d891c28bb8fb893"></a>
#### setTimestampTimeZone

```
void setTimestampTimeZone(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

- Operation: It binds the data x to the parameter index as TIMESTAMP WITH TIME ZONE type. Timestamp x is regarded as timezone of cal. Timezone information for DB column refers to timezone of cal.
- Exception: It occurs if parameterIndex is smaller than 0 or it is bigger than the number of parameters.

> It is GOLDILOCKS JDBC-specific feature, and PreparedStatement object can be used after it is casted as GoldilocksPreparedStatement.  
> e.g. ((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(1, aTimestamp, aCalendar);

<a id="f7fa3ac631a209ca"></a>
### Ref

The class is not implemented.

<a id="ca355851c3ee8a1f"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="6025ef67a7317dd9"></a>
#### getObject

```
Object getObject() throws SQLException
```

```
Object getObject(Map<String,Class<?>> map) throws SQLException
```

<a id="7f12c3bec4e0f0a5"></a>
#### setObject

```
void setObject(Object value) throws SQLException
```

<a id="82f05937c395b5b3"></a>
### ResultSet

<a id="0f306d45dcf7253c"></a>
#### absolute

```
boolean absolute(int row) throws SQLException
```

- Operation: The fetched row cursor position is at the row-th. The first row is 1. 0 points to the previous first row. If it is a negative number, it points to the last row. -1 points to the last row, and -2 points to the second row from the last row. If the cursor can be positioned within the fetched row cache, only the position information is changed within the cache. If it is not within the cache, it is fetched from the server again. If the row exceeds the range, the cursor is positioned before first or after last, and it returns false. Otherwise, the cursor is positioned at the corresponding row and it returns true.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

> If it is not in the cache, it should be fetched again. If the row is behind the current position, the number of rows(n) from row position are fetched from the server in favor of next(). If the row is prior to the current position, the number of n rows from the position(row-n+1) are fetched from the server in favor of previous().

<a id="fda69ee3fac8d143"></a>
#### afterLast

```
void afterLast() throws SQLException
```

- Operation: The row cursor is positioned at *after last*. If the row cache is the last row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the last row set (The total number of rows-n + 1 to n rows, n is the number of rows fetched from the server), then positions the cursor at *after last*.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="36f2093ddb42b8f7"></a>
#### beforeFirst

```
void beforeFirst() throws SQLException
```

- Operation: The row cursor is positioned at *before first*. If the row cache is the first row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the first row set (1 to n rows, n is the number of rows fetched from the server), then positions the cursor at *before first*.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="dc460fb4119cb848"></a>
#### cancelRowUpdates

```
void cancelRowUpdates() throws SQLException
```

- Operation: Cursor update feature has not been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="9e3c9967a9013774"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- Operation: It clears all SQLWarning objects which is owned by ResultSet object.
- Exception: It does not occur.

<a id="3f773dbba8a5ed99"></a>
#### close

```
void close() throws SQLException
```

- Operation: If the cursor is open on the server, it closes the cursor (If the cursor is already closed on the server, this operation is not performed. Namely, the protocol is not transferred.), and the current state of the ResultSet object is changed to be closed. If it is already closed, then any operation is not performed.
- Exception: If an error occurs on the server, it throws SQLException.

<a id="6ae1979e2d9b0978"></a>
#### deleteRow

```
void deleteRow() throws SQLException
```

- Operation: Cursor update feature is not implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="d3760761b3f9ec5c"></a>
#### findColumn

```
int findColumn(String columnLabel) throws SQLException
```

- Operation: It returns the index of the column name. The index of the first column is 1.
- Exception: If it is already closed or the column name is not found, it throws SQLException.

<a id="36cd4ff9ae0eee17"></a>
#### first

```
boolean first() throws SQLException
```

- Operation: It positions the row cursor at the first (the first row). If the row cache is the first row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, it fetches the first row set (1 to n rows, n is the number of rows fetched from the server), then positions the cursor at the first. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="4f4b4c9a175e035a"></a>
#### getArray

```
Array getArray(int columnIndex) throws SQLException
```

- Operation: Array type is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Array getArray(String columnLabel) throws SQLException
```

- Operation: Array type is not supported. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d).
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="036dbfe7845d2169"></a>
#### getAsciiStream

```
InputStream getAsciiStream(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as InputStream type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to InputStream, it throws SQLException.

```
InputStream getAsciiStream(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as InputStream type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to InputStream, it throws SQLException.

<a id="45519f63792ef216"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as BigDecimal type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to BigDecimal, it throws SQLException.

```
BigDecimal getBigDecimal(int columnIndex, int scale) throws SQLException
```

- Operation: This is a deprecated method. It operates in the same way as getBigDecimal(int columnIndex). The scale is ignored.
- Exception: For more information, refer to [getBigDecimal](#5a798a6813ac508d)(int columnIndex).

```
BigDecimal getBigDecimal(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as BigDecimal type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to BigDecimal, it throws SQLException.

```
BigDecimal getBigDecimal(String columnLabel, int scale) throws SQLException
```

- Operation: This is a deprecated method. It operates in the same way as getBigDecimal(String columnLabel). The scale is ignored.
- Exception: For more information, refer to [getBigDecimal](#5a798a6813ac508d)(String columnLabel).

<a id="a9ed484d5bb7c6b0"></a>
#### getBinaryStream

```
InputStream getBinaryStream(int columnIndex) throws SQLException
```

- Operation: It is as same as [getAsciiStream](#036dbfe7845d2169)(int columnIndex).
- Exception: For more information, refer to [getAsciiStream](#036dbfe7845d2169)(int columnIndex).

```
InputStream getBinaryStream(String columnLabel) throws SQLException
```

- Operation: It is as same as [getAsciiStream](#036dbfe7845d2169)(String columnLabel).
- Exception: For more information, refer to [getAsciiStream](#036dbfe7845d2169)(String columnLabel).

<a id="5f69bf2e45f95c09"></a>
#### getBlob

```
Blob getBlob(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as blob type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for GOLDILOCKS type - 1](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to blob, it throws SQLException.

```
Blob getBlob(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as blob type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for GOLDILOCKS type - 1](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to blob, it throws SQLException.

<a id="05633e664652df6d"></a>
#### getBoolean

```
boolean getBoolean(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as Boolean type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to Boolean, it throws SQLException.

```
boolean getBoolean(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as Boolean type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to Boolean, it throws SQLException.

<a id="3285acccda3b1bb8"></a>
#### getByte

```
byte getByte(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as byte type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to byte, it throws SQLException.

```
byte getByte(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as byte type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to byte, it throws SQLException.

<a id="9b3b223bf593aec6"></a>
#### getBytes

```
byte[] getBytes(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as byte[] type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

> If getBytes is performed for all GOLDILOCKS data types, it gets the binary form stored in DB.

```
byte[] getBytes(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as byte[] type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

> If getBytes is performed for all GOLDILOCKS data types, it gets the binary form stored in DB.

<a id="5a70524d9fd8b037"></a>
#### getCharacterStream

```
Reader getCharacterStream(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as reader type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to reader, it throws SQLException.

```
Reader getCharacterStream(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as reader type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) .
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to reader, it throws SQLException.

<a id="4f51edc1e317b821"></a>
#### getClob

```
Clob getClob(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as clob type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for GOLDILOCKS type - 1](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to clob, it throws SQLException.

```
Clob getClob(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as clob type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for GOLDILOCKS type - 1](#3ad95d69b475c64d).
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to clob, it throws SQLException.

<a id="12117b9871a14573"></a>
#### getConcurrency

```
int getConcurrency() throws SQLException
```

- Operation: It returns concurrency of the current ResultSet object. It supports only ResultSet.CONCUR_READ_ONLY currently.
- Exception: It does not occur.

<a id="a3f3fe3a5a6962aa"></a>
#### getCursorName

```
String getCursorName() throws SQLException
```

- Operation: It gets the cursor name of the server pointed by the ResultSet. The communication with the server occurs.
- Exception: If ResultSet is already closed or an error occurs on the server, it throws SQLException.

<a id="0196fd31214f9fee"></a>
#### getDate

```
Date getDate(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the date object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to date, it throws SQLException.

```
Date getDate(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the date object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to date, it throws SQLException.

```
Date getDate(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the date object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to date, it throws SQLException.

```
Date getDate(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as date type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the date object, the local timezone of cal is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to date, it throws SQLException.

<a id="3a7a187859b1c81d"></a>
#### getDouble

```
double getDouble(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as double type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to double, it throws SQLException.

```
double getDouble(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as double type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to double, it throws SQLException.

<a id="5d7dac86523e4bca"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- Operation: It always returns ResultSet.FETCH_FORWARD. The backward fetch is not supported.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="19c8d8b921bd30be"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- Operation: It gets the number of rows fetched from the server at once. If it is 0, it calculates the maximum number of rows included in a communication packet per transmission. The default value is 0.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="879add09160af9a8"></a>
#### getFloat

```
float getFloat(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as float type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to float, it throws SQLException.

```
float getFloat(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as float type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to float, it throws SQLException.

<a id="5411d35b822b06cb"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- Operation: It returns the holdability of the current ResultSet. It is the value determined when the ResultSet object is created, and it can not be changed in the meantime. The default value is ResultSet.HOLD_CURSOR_OVER_COMMIT.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="4f74ce57b1b81dc8"></a>
#### getInt

```
int getInt(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as int type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to int, it throws SQLException.

```
int getInt(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as int type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to int, it throws SQLException.

<a id="efe469266daa4ed0"></a>
#### getLong

```
long getLong(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as long type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to long, it throws SQLException.

```
long getLong(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as long type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to long, it throws SQLException.

<a id="23703cf348d9a79e"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- Operation: It creates and returns the ResultSetMetaData object getting detailed information on the column.
- Exception: If ResultSet is already closed or an error occurs while detailed information on the column is fetched from the server, it throws SQLException.

<a id="334b3c6866083022"></a>
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

<a id="5595efac8b5af193"></a>
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

<a id="175257cf9c9dba2e"></a>
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

<a id="6ccae17250def39e"></a>
#### getObject

```
Object getObject(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as the most appropriate Java object type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

```
Object getObject(int columnIndex, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

```
Object getObject(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as the most appropriate Java object type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

```
Object getObject(String columnLabel, Map<String,Class<?>> map) throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6f1c91a83713ac36"></a>
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

<a id="5cf51e716da890e2"></a>
#### getRow

```
int getRow() throws SQLException
```

- Operation: It returns the cursor position of the current ResultSet object. The first row is 1. If it is *before first*, it returns 0.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="8b85d1a80d36a87c"></a>
#### getRowId

```
RowId getRowId(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as Rowld type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to Rowld, it throws SQLException.

```
RowId getRowId(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as Rowld type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to Rowld, it throws SQLException.

<a id="d176e3a2e564f3ba"></a>
#### getShort

```
short getShort(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as short type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to short, it throws SQLException.

```
short getShort(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as short type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for SUNDB Type - 1 ](#3ad95d69b475c64d) . 
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to short, it throws SQLException.

<a id="53a8b7f1241efc19"></a>
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

<a id="ef25ab8f14fc807d"></a>
#### getStatement

```
Statement getStatement() throws SQLException
```

- Operation: It returns the statement object which created the ResultSet object.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="cf59af54f4ad7445"></a>
#### getString

```
String getString(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as string type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . If getString() is performed for BINARY, VARBINARY, LONG VARBINARY, the string of hex code is returned.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range, it throws SQLException.

```
String getString(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as string. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . If getString() is performed for BINARY, VARBINARY, LONG VARBINARY, it returns the string of hex code.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist, it throws SQLException.

<a id="09332ca0adc926fe"></a>
#### getTime

```
Time getTime(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the time object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to time, it throws SQLException.

```
Time getTime(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the time object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to time, it throws SQLException.

```
Time getTime(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the time object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to time, it throws SQLException.

```
Time getTime(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as time type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the time object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to time, it throws SQLException.

<a id="39217022ae2894d5"></a>
#### getTimestamp

```
Timestamp getTimestamp(int columnIndex) throws SQLException
```

- Operation: It gets the columnIndex-th column data as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the timestamp object, local timezone is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(int columnIndex, Calendar cal) throws SQLException
```

- Operation: It gets the columnIndex-th column data as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the timestamp object, local timezone of cal is used.
- Exception: If ResultSet is already closed or the columnIndex exceeds the range or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(String columnLabel) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the timestamp object, the local timezone is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to timestamp, it throws SQLException.

```
Timestamp getTimestamp(String columnLabel, Calendar cal) throws SQLException
```

- Operation: It gets the column data whose name is columnLabel as timestamp type. For more information about GOLDILOCKS type-specific support, refer to [Whether supporting getter method for Goldilocks Type - 1 ](#3ad95d69b475c64d) . When creating the timestamp object, the local timezone of cal is used.
- Exception: If ResultSet is already closed or the corresponding columnLabel does not exist or the type can not be converted to timestamp, it throws SQLException.

<a id="349b7a8c1bac3e57"></a>
#### getType

```
int getType() throws SQLException
```

- Operation: It returns the current ResultSet type. It returns one of ResultSet.TYPE_FORWARD_ONLY, ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.TYPE_SCROLL_SENSITIVE.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="129ad305143c41d7"></a>
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

<a id="1f5f1f9f514196c0"></a>
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

<a id="7c15f7d4a340ec64"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns a list of SQLWarning accumulated on the object so far. If it gets a warning from the server, it creates SQLWarning. If clearWarning is not performed, it continues to be accumulated. If a warning does not occur, null is returned.
- Exception: It does not occur.

<a id="f2feac7b1e8ca4fd"></a>
#### insertRow

```
void insertRow() throws SQLException
```

- Operation: Cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="06d83820acca000c"></a>
#### isAfterLast

```
boolean isAfterLast() throws SQLException
```

- Operation: It queries whether the current cursor position is at *after last*. If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="b0e707c7cd827ba0"></a>
#### isBeforeFirst

```
boolean isBeforeFirst() throws SQLException
```

- Operation: It queries whether the current cursor position is at *before first*. If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="53d652f06f94ded4"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- Operation: It queries whether the current ResultSet is closed. If closed, it returns true. Otherwise, it returns false. Even if the user does not call the close, ResultSet can be closed by closing the cursor of the server. It is when, for example, the statement which created the ResultSet is closed, or the transaction is committed when the holdability is ResultSet.CLOSE_CURSOR_AT_COMMIT mode, or an error occurs from the server during fetching.
- Exception: It does not occur.

<a id="6d4e70ff9d4c828a"></a>
#### isFirst

```
boolean isFirst() throws SQLException
```

- Operation: It queries whether the current cursor position is at first (the first row). If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="e0bfd257651f6b86"></a>
#### isLast

```
boolean isLast() throws SQLException
```

- Operation: It queries whether the current cursor position is at last (the last row). If so, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed, it throws SQLException.

<a id="d0398f32b1ac875f"></a>
#### last

```
boolean last() throws SQLException
```

- Operation: The row cursor is positioned at last (the last row). If the row cache is the last row set (It is a part of the entire result set), only the cursor position is changed. Otherwise, the row cursor is positioned at last after the last row set is fetched (row from last-n+1 to the last row, n is the number of rows fetched from the server). If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="b4526c47feebfecf"></a>
#### moveToCurrentRow

```
void moveToCurrentRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="f72d7d662132103b"></a>
#### moveToInsertRow

```
void moveToInsertRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="d5597fda3d791f71"></a>
#### next

```
boolean next() throws SQLException
```

- Operation: The row cursor is positioned at the next to the current row. If the current row is the last row of the row cache, the next row cache is fetched from the server. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or an error occurs from the server when fetching, it throws an exception.

<a id="a3f5483b59b31d40"></a>
#### previous

```
boolean previous() throws SQLException
```

- Operation: The row cursor is positioned at the row before the current position. If the current row is the first row of the row cache, the previous row cache(n rows from x-n to x-1, x is the current row index) is fetched from the server. If the row exists, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server during fetching, it throws an exception.

<a id="31810626624a7960"></a>
#### refreshRow

```
void refreshRow() throws SQLException
```

- Operation: If ResultSet type is ResultSet.SCROLL_SENSITIVE, the current row cache is fetched from the server. If any row is changed (by the same transaction or other transactions), it is reflected. If ResultSet type is ResultSet.Scroll_INSENSITIVE, any operation is not performed.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server during fetching, it throws an exception.

<a id="14b383e3338b860c"></a>
#### relative

```
boolean relative(int rows) throws SQLException
```

- Operation: It moves the row cursor from the current cursor position to the position apart as many as the number of rows. If it can be moved within the current row cache, only the cursor position is changed. Otherwise, the cursor is moved after the row cache is fetched from the server. If the position to be moved is backward from the current position (next direction), the row cache is fetched from rows to rows+n-1 (in favor of next). If the position to be moved is forward from the current position(previous direction), the row cache is fetched from rows-n+1 to rows (in favor of previous).
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY or an error occurs from the server when fetching, it throws an exception.

<a id="6b88619505954542"></a>
#### rowDeleted

```
boolean rowDeleted() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is deleted (by the same transaction or other transactions). If deleted, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="69c7ec55e47ec0c7"></a>
#### rowInserted

```
boolean rowInserted() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is inserted (by the same transaction or other transactions). If inserted, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="462def9c21548805"></a>
#### rowUpdated

```
boolean rowUpdated() throws SQLException
```

- Operation: It queries whether the row of the current cursor position is updated (by the same transaction or other transactions). If updated, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the ResultSet type is ResultSet.TYPE_FORWARD_ONLY, it throws an exception.

<a id="eba8c9c5ce4fd023"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- Operation: The backward fetch is not supported by the server. Therefore, only ResultSet.FETCH_FORWARD is available. SQLWarning occurs if other values are inserted.
- Exception: If ResultSet is already closed or the argument does not have the defined value, it throws an exception.

<a id="1bd33a74e7c9d423"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- Operation: It specifies the number of rows fetched from the server at once. 0 refers that the server determines it. If it is 0, it refers to the number of rows of which a communication packet can include at once for the forward only cursor. It is specified as 100 for the scrollable cursor.
- Exception: If ResultSet is already closed, it throws an exception.

<a id="0f3d9fc3f210ef7b"></a>
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

<a id="2a351df03eae3589"></a>
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

<a id="b230095fcbe0f6b6"></a>
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

<a id="09be3ed922f2480b"></a>
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

<a id="aebdd13533004201"></a>
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

<a id="3ab0a1ff1bc6524c"></a>
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

<a id="367e14c6c75d45fb"></a>
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

<a id="c9e6a958e9c24a03"></a>
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

<a id="0248d1332bfc6ebd"></a>
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

<a id="5bfeafb319d54c04"></a>
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

<a id="8d99443479147769"></a>
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

<a id="8b07e46fe142da53"></a>
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

<a id="8733b98c36dc996b"></a>
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

<a id="220021138a9ca2ec"></a>
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

<a id="7f91d30f133f4fb0"></a>
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

<a id="73d516f52f371871"></a>
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

<a id="a3f0bc97c6dbf768"></a>
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

<a id="8134987013e3e89f"></a>
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

<a id="ab9bae19176e0973"></a>
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

<a id="d8749b276ecfc478"></a>
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

<a id="431a2e6b05040a53"></a>
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

<a id="d946593e82be53da"></a>
#### updateRow

```
void updateRow() throws SQLException
```

- Operation: The cursor update feature has not yet been implemented. If ResultSet concurrency is ResultSet.CONCUR_READ_ONLY, it throws SQLException. If it is ResultSet.CONCUR_UPDATABLE, it throws SQLFeatureNotSupportedException.
- Exception: If it is already closed, it throws SQLException. Otherwise, refer to the operation.

<a id="b3f89c6d2250446b"></a>
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

<a id="3c20bbf88bae8617"></a>
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

<a id="378cc1da54a3d540"></a>
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

<a id="1c289e20e54bb180"></a>
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

<a id="ccd29cd7e38b8f53"></a>
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

<a id="29d46f60d185e548"></a>
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

<a id="ead6096ebfe01bf6"></a>
#### wasNull

```
boolean wasNull() throws SQLException
```

- Operation: It queries whether the column value which was read last is NULL. If it is NULL, it returns true. Otherwise, it returns false.
- Exception: If ResultSet is already closed or the column value never has been read, it throws SQLException.

<a id="487d3717483c521d"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It queries whether this object is the class which implemented the iface interface. If it so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS ResultSet object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="294ee756007a2538"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- Operation: It eventually returns itself even when it is unwrapped because GOLDILOCKS ResultSet is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, then the method throws an exception.
- Exception: If iface is not this object type (when this object type is not implemented.), it throws SQLException.

<a id="d1a19b07fe01c919"></a>
### ResultSetMetaData

<a id="3a01237166cf9cbd"></a>
#### getCatalogName

```
String getCatalogName(int column) throws SQLException
```

- Operation: It returns the catalog name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="119e67e8c3a86387"></a>
#### getColumnClassName

```
String getColumnClassName(int column) throws SQLException
```

- Operation: It returns the name of Java class which is the most appropriate to the column type. It is specified such as java.math.BigDecimal, and it refers to getName() method in Java. For binary type, it refer to byte[].class.getName(), so it can be specified such as '[B'.
- Exception: If the column value is wrong, it throws SQLException.

<a id="7f4b111f123b168b"></a>
#### getColumnCount

```
int getColumnCount() throws SQLException
```

- Operation: It returns the number of columns that the ResultSet has.
- Exception: It does not occur.

<a id="d58a5a8d649cec40"></a>
#### getColumnDisplaySize

```
int getColumnDisplaySize(int column) throws SQLException
```

- Operation: It returns the maximum width when the column value is displayed.
- Exception: If the column value is wrong, it throws SQLException.

<a id="b731b7d06a587544"></a>
#### getColumnLabel

```
String getColumnLabel(int column) throws SQLException
```

- Operation: It gets the label of the column. For example, the label is "C1 + 1" and the name is "" for the query statement such as "select C1 + 1 from t1".
- Exception: If the column value is wrong, it throws SQLException.

<a id="5ded935a6c55c653"></a>
#### getColumnName

```
String getColumnName(int column) throws SQLException
```

- Operation: It returns the alias name of the column. The original column name, not the alias name is defined to be returned in JDBC specification. However, it is recommended to use the alias name because some view names are meaningless or complicated. For example, both the name and label are "C2" for the query statement such as "select C1 as C2 from t1". For more information about the case of when name and label are different, refer to [getColumnLabel](#b731b7d06a587544).
- Exception: If the column value is wrong, it throws SQLException.

<a id="12c0157583dc592a"></a>
#### getColumnType

```
int getColumnType(int column) throws SQLException
```

- Operation: It returns the type of the column. The return value is defined in types. Types.OTHERS is returned for GOLDILOCKS interval family types. The constant values of the corresponding types are returned for the other types.
- Exception: If the column value is wrong, it throws SQLException.

<a id="11099956016cee1b"></a>
#### getColumnTypeName

```
String getColumnTypeName(int column) throws SQLException
```

- Operation: It returns GOLDILOCKS column type name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="cfa64852626ae095"></a>
#### getPrecision

```
int getPrecision(int column) throws SQLException
```

- Operation: It returns the precision of the column. It returns 0 for the type without any precision.
- Exception: If the column value is wrong, it throws SQLException.

<a id="768ce8b6630ac5ff"></a>
#### getScale

```
int getScale(int column) throws SQLException
```

- Operation: It returns the scale of the column. It returns 0 for the type without any scale.
- Exception: If the column value is wrong, it throws SQLException.

<a id="7dfabaa6e7671994"></a>
#### getSchemaName

```
String getSchemaName(int column) throws SQLException
```

- Operation: It returns the schema name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="b980ebf823df99d5"></a>
#### getTableName

```
String getTableName(int column) throws SQLException
```

- Operation: It returns the table name of the column.
- Exception: If the column value is wrong, it throws SQLException.

<a id="5ae1b631a3eb307a"></a>
#### isAutoIncrement

```
boolean isAutoIncrement(int column) throws SQLException
```

- Operation: It returns whether it is the column which is automatically given the unique value. If so, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="c2623535dbbd15e5"></a>
#### isCaseSensitive

```
boolean isCaseSensitive(int column) throws SQLException
```

- Operation: It returns whether the column is case sensitive. If it is case sensitive, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="895833c552f435ad"></a>
#### isCurrency

```
boolean isCurrency(int column) throws SQLException
```

- Operation: It always returns false because the currency of the column can not be determined by the server.
- Exception: If the column value is wrong, it throws SQLException.

<a id="0f33f61c89c8861e"></a>
#### isDefinitelyWritable

```
boolean isDefinitelyWritable(int column) throws SQLException
```

- Operation: It returns whether the column is updatable. GOLDILOCKS does not support the definitely writable. It always returns the value as same as isUpdatable().
- Exception: If the column value is wrong, it throws SQLException.

<a id="f09ce95672d64197"></a>
#### isNullable

```
int isNullable(int column) throws SQLException
```

- Operation: It returns whether the column has nullable. It returns either columnNullable or columnNoNulls.
- Exception: If the column value is wrong, it throws SQLException.

<a id="6c7b6b1377eb314e"></a>
#### isReadOnly

```
boolean isReadOnly(int column) throws SQLException
```

- Operation: It returns whether the column is read only. It always returns the opposite value of isUpdatable().
- Exception: If the column value is wrong, it throws SQLException.

<a id="dad857238b984153"></a>
#### isSearchable

```
boolean isSearchable(int column) throws SQLException
```

- Operation: It returns whether the column can be used in the conditional clause. It always returns true because all target columns in GOLDILOCKS can be used in the conditional clause.
- Exception: If the column value is wrong, it throws SQLException.

<a id="3b6d468099ac7f39"></a>
#### isSigned

```
boolean isSigned(int column) throws SQLException
```

- Operation: It returns whether the column has a sign. If it has a sign, it returns true. Otherwise, it returns false.
- Exception: If the column value is wrong, it throws SQLException.

<a id="a5e0807143bc7436"></a>
#### isWritable

```
boolean isWritable(int column) throws SQLException
```

- Operation: It returns whether the column is updatable.
- Exception: If the column value is wrong, it throws SQLException.

<a id="49b5f7303f38dd1f"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- Operation: It queries whether the object is a class implementing the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper and it queries only whether the given argument class type is implemented because GOLDILOCKS ResultSetMetaData object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="5a40a0b3a281c998"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS ResultSetMetaData is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of the object (if this object returns the unimplemented type), it throws SQLException.

<a id="f8ace88e5209854d"></a>
### RowId

<a id="0c616e609b6a677d"></a>
#### equals

```
boolean equals(Object obj) throws SQLException
```

- Operation: If RowId of this object is as same as RowId of obj, it returns true. Otherwise, it returns false.
- Exception: It does not occur.

<a id="7abef4ce20714504"></a>
#### getBytes

```
byte[] getBytes() throws SQLException
```

- Operation: It returns the byte array value of RowId.
- Exception: It does not occur.

<a id="3497e9e1bb4c625c"></a>
#### hashCode

```
int hashCode() throws SQLException
```

- Operation: It returns the hash code value.
- Exception: It does not occur.

<a id="5517adb274130b88"></a>
#### toString

```
String toString() throws SQLException
```

- Operation: It returns a base-64 string of RowId value.
- Exception: It does not occur.

<a id="9c775101b74f5e0f"></a>
### RowSet

The class is not implemented

<a id="d26446f014adfd98"></a>
#### addRowSetListener

```
void addRowSetListener(RowSetListener listener) throws SQLException
```

<a id="4295e1a57e253ddb"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

<a id="4fa9ccde8ef80b1c"></a>
#### execute

```
void execute() throws SQLException
```

<a id="83bfd330204a956d"></a>
#### getCommand

```
String getCommand() throws SQLException
```

<a id="8e46e8132360700c"></a>
#### getDataSourceName

```
String getDataSourceName() throws SQLException
```

<a id="06325dd4cd83dd14"></a>
#### getEscapeProcessing

```
boolean getEscapeProcessing() throws SQLException
```

<a id="72b0e2f76e3542bb"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

<a id="c96f4cca42d2d05b"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

<a id="22ddf0b0d237c543"></a>
#### getPassword

```
String getPassword() throws SQLException
```

<a id="274ea1a93bfb3874"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

<a id="32b1f3b557d3bd2a"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

<a id="398b34fc99f9b6dc"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

<a id="5ecb79a96fe07e72"></a>
#### getUrl

```
String getUrl() throws SQLException
```

<a id="ac011674e457672f"></a>
#### getUsername

```
String getUsername() throws SQLException
```

<a id="4061ce65aa142d35"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

<a id="1fd778a20574908b"></a>
#### removeRowSetListener

```
void removeRowSetListener(RowSetListener listener) throws SQLException
```

<a id="b8604a46e740a2aa"></a>
#### setArray

```
void setArray(int i, Array x) throws SQLException
```

<a id="389fa8947ae6d33d"></a>
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

<a id="df40aed0389a48a7"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

<a id="b7533e9aef0cba3b"></a>
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

<a id="2c5c89306de08110"></a>
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

<a id="d9ed2a123040b16b"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

<a id="14ec6a6051e26a06"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

```
void setByte(String parameterName, byte x) throws SQLException
```

<a id="88aeb3827fec4df3"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

<a id="3a92728e195c0d74"></a>
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

<a id="eab583f7163abe0f"></a>
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

<a id="8e5a7e1fd560a3a9"></a>
#### setCommand

```
void setCommand(String cmd) throws SQLException
```

<a id="f3e9e7cf1f72f1cc"></a>
#### setConcurrency

```
void setConcurrency(int concurrency) throws SQLException
```

<a id="4215235f6051212b"></a>
#### setDataSourceName

```
void setDataSourceName(String name) throws SQLException
```

<a id="a923b3435306b04a"></a>
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

<a id="0be998c062605ec3"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

```
void setDouble(String parameterName, double x) throws SQLException
```

<a id="3627ca3b52e7e368"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

<a id="a4cfd1afe28db811"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

```
void setFloat(String parameterName, float x) throws SQLException
```

<a id="52ed34547fd1c1d3"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

```
void setInt(String parameterName, int x) throws SQLException
```

<a id="ee1477cd5e8e5051"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

```
void setLong(String parameterName, long x) throws SQLException
```

<a id="ccf77e15c61ac392"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

<a id="93788f091850d6a2"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

<a id="b1a915a30159ace9"></a>
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

<a id="c8fae024d8b0b78e"></a>
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

<a id="7902abeee6b0ca58"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

```
void setNString(String parameterName, String value) throws SQLException
```

<a id="8d8e7a15fa207782"></a>
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

<a id="64f5f5e9504d9387"></a>
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

<a id="c43f6cb09657ca38"></a>
#### setPassword

```
void setPassword(String password) throws SQLException
```

<a id="c0f72e845161a95d"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

<a id="7e928be2e1429eda"></a>
#### setReadOnly

```
void setReadOnly(boolean value) throws SQLException
```

<a id="73c0cd06430803e6"></a>
#### setRef

```
void setRef(int i, Ref x) throws SQLException
```

<a id="7fb40882bae53c84"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

```
void setRowId(String parameterName, RowId x) throws SQLException
```

<a id="6707dca648f54d81"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

```
void setShort(String parameterName, short x) throws SQLException
```

<a id="114ef80ddc244451"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

<a id="2c8d715fbf05a0ef"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

```
void setString(String parameterName, String x) throws SQLException
```

<a id="d98612ee3aa0cdbb"></a>
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

<a id="18a847df33e123bb"></a>
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

<a id="b497652d098a744d"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

<a id="b095c89e7a0be333"></a>
#### setType

```
void setType(int type) throws SQLException
```

<a id="ce0624889072fa03"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

<a id="80afce308f3cedb1"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

<a id="c0015701a6d6ce56"></a>
#### setUrl

```
void setUrl(String url) throws SQLException
```

<a id="2098e61848fa14b2"></a>
#### setUsername

```
void setUsername(String name) throws SQLException
```

<a id="d822fe28c43b486a"></a>
### RowSetMetaData

The class is not implemented

<a id="a71a629ac890f4bb"></a>
#### setAutoIncrement

```
void setAutoIncrement(int columnIndex, boolean property) throws SQLException
```

<a id="968511776ce441a3"></a>
#### setCaseSensitive

```
void setCaseSensitive(int columnIndex, boolean property) throws SQLException
```

<a id="bd56c6c8bfb96ec5"></a>
#### setCatalogName

```
void setCatalogName(int columnIndex, String catalogName) throws SQLException
```

<a id="66cd47d9bcd322c3"></a>
#### setColumnCount

```
void setColumnCount(int columnCount) throws SQLException
```

<a id="7207b25338aac9fc"></a>
#### setColumnDisplaySize

```
void setColumnDisplaySize(int columnIndex, int size) throws SQLException
```

<a id="a1402486e9a4d64f"></a>
#### setColumnLabel

```
void setColumnLabel(int columnIndex, String label) throws SQLException
```

<a id="738151135e45ffde"></a>
#### setColumnName

```
void setColumnName(int columnIndex, String columnName) throws SQLException
```

<a id="b5959879d2ce8e4e"></a>
#### setColumnType

```
void setColumnType(int columnIndex, int SQLType) throws SQLException
```

<a id="08d5dca5ebf3456a"></a>
#### setColumnTypeName

```
void setColumnTypeName(int columnIndex, String typeName) throws SQLException
```

<a id="ff20d60d6d5bfa01"></a>
#### setCurrency

```
void setCurrency(int columnIndex, boolean property) throws SQLException
```

<a id="db749f4cffafa90b"></a>
#### setNullable

```
void setNullable(int columnIndex, int property) throws SQLException
```

<a id="4a440e7126052173"></a>
#### setPrecision

```
void setPrecision(int columnIndex, int precision) throws SQLException
```

<a id="35974c05201ce167"></a>
#### setScale

```
void setScale(int columnIndex, int scale) throws SQLException
```

<a id="2ec89419e0938f56"></a>
#### setSchemaName

```
void setSchemaName(int columnIndex, String schemaName) throws SQLException
```

<a id="4f67e81bb821fb6e"></a>
#### setSearchable

```
void setSearchable(int columnIndex, boolean property) throws SQLException
```

<a id="7218b1a5aa38aacb"></a>
#### setSigned

```
void setSigned(int columnIndex, boolean property) throws SQLException
```

<a id="85ec9f1f16aa3677"></a>
#### setTableName

```
void setTableName(int columnIndex, String tableName) throws SQLException
```

<a id="3723161e30917469"></a>
### Savepoint

<a id="0e60f3155b25987a"></a>
#### getSavepointId

```
int getSavepointId() throws SQLException
```

- Operation: It returns the id value which is automatically assigned.
- Exception: It throws SQLException because it does not have an ID if the savepoint object is created by giving its name.

<a id="8e70a7c3040cad27"></a>
#### getSavepointName

```
String getSavepointName() throws SQLException
```

- Operation: It returns the name specified at the time of when a savepoint object is created.
- Exception: If the savepoint created with an automatic id value, it throws SQLException.

<a id="49eef60a4ed5a875"></a>
### SQLData

The class is not implemented.

<a id="0907d3fe8bcdc355"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="1100e256cc94fee2"></a>
#### readSQL

```
void readSQL(SQLInput stream, String typeName) throws SQLException
```

<a id="5b2aa415ba4fd9aa"></a>
#### writeSQL

```
void writeSQL(SQLOutput stream) throws SQLException
```

<a id="c3e425382f7c5cb1"></a>
### SQLXML

The class is not implemented.

<a id="1d4197aeee9c74a3"></a>
#### free

```
void free() throws SQLException
```

<a id="b6919669b63ece05"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

<a id="c820fb422a0840ba"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

<a id="83725109db833cb5"></a>
#### getSource

```
<T extends Source> T getSource(Class<T> sourceClass) throws SQLException
```

<a id="9d22a719ad12f0a7"></a>
#### getString

```
String getString() throws SQLException
```

<a id="5e735d68b7cb69e6"></a>
#### setBinaryStream

```
OutputStream setBinaryStream() throws SQLException
```

<a id="f6e314de86ecfc8b"></a>
#### setCharacterStream

```
Writer setCharacterStream() throws SQLException
```

<a id="d0ba1357391a69a7"></a>
#### setResult

```
<T extends Result> T setResult(Class<T> resultClass) throws SQLException
```

<a id="266ae80d88bc8360"></a>
#### setString

```
void setString(String value) throws SQLException
```

<a id="0da1c46ef437b04a"></a>
### Statement

<a id="594a2e36732c406c"></a>
#### addBatch

```
void addBatch(String sql) throws SQLException
```

- Operation: The SQL statement is added to the batch job.
- Exception: It does not occur.

<a id="5a936820ce6a881d"></a>
#### cancel

```
void cancel() throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="19eaad9df9969e04"></a>
#### clearBatch

```
void clearBatch() throws SQLException
```

- Operation: It clears all registered batch jobs. If registered batch job does not exist, any operation is not performed.
- Exception: It does not occur.

<a id="1ab3c1a9f67d5b51"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- Operation: It clears all SQLWarning objects which is owned by the statement object.
- Exception: It does not occur.

<a id="e6fe3810b2e27bda"></a>
#### close

```
void close() throws SQLException
```

- Operation: The current statement object is closed, and it is released if the statement related information assigned to the server exists. If the ResultSet created by the object exists, it is closed. The object is removed from the connection object which created the statement object.
- Exception: If an error occurs when statement information is released from the server, it throws an exception.

<a id="52f283cdcf92774f"></a>
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

<a id="e63844777523b1b4"></a>
#### executeBatch

```
int[] executeBatch() throws SQLException
```

- Operation: It executes the registered batch job in turn. The communication with the server occurs per each batch job. It returns the array of the number of rows in which the update reflected after executing each batch job.
- Exception: If the statement is already closed or any batch job is not registered or an error occurs when executing from the server, it throws an exception.

> It does not have definite advantage over the normal execute() because the batch jobs are not transmitted and executed at once. Use a batch execution of the PreparedStatement for fast processing.

<a id="ef25ce5981bed2fb"></a>
#### executeQuery

```
ResultSet executeQuery(String sql) throws SQLException
```

- Operation: It executes the given SQL statement and gets part of results and creates the ResultSet.
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is not the select statement, it throws an exception.

> Its operation is a bit different from execute(). The communicate with the server occurs twice if getResultSet() is performed for the same SQL statement after performing execute(). The execution command is performed when performing execute(), and the fetch related command is performed when performing getResultSet(). On the other hand, executeQuery() assumes that the SQL statement is the select statement, and it executes all with a single communication until fetch.

<a id="d39897b60e544c96"></a>
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
- Exception: If the statement is already closed or the batch job is registered or an error occurs when executing on the server or the SQL statement is the select statement, it throws an exception. If autoGeneratedKeys is not Statement.NO_GENERATED_KEYS, it throws SQLFeatureNotSupportedException

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

<a id="6415b12066b89faa"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- Operation: It returns the connection object which created the object. If statement object is created with logical connection via the PooledConnection, the user gets the logical connection, not the physical connection via the method.
- Exception: If the statement is already closed, it throws an exception.

<a id="3c10894797036ffa"></a>
#### getExplainPlan

```
String getExplainPlan() throws SQLException
```

- Operation: It is non-standard method, and it is the unique method of GoldilocksStatement. It gets the generated plan text. It should set for generating the plan text via setExplainPlanOption to use the method. For more information about the detailed usage, refer to [Viewing Plan Text](#8a0d6fc839863652).
- Exception: If the statement is already closed or an error occurs on the server, it throws an exception.

<a id="206418891a14242c"></a>
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

<a id="c8f9df856b5bc11a"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- Operation: It always returns ResultSet.FETCH_FORWARD.
- Exception: If the statement is already closed, it throws an exception.

<a id="eec9d67151db9379"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- Operation: It returns the default fetch size of ResultSet which is got from the statement object. The default value is 0, and 0 refers that the server determines the number of fetched rows. For more information, refer to [getFetchSize](#19c8d8b921bd30be) of ResultSet.
- Exception: If the statement is already closed, it throws an exception.

<a id="e17e723828737966"></a>
#### getGeneratedKeys

```
ResultSet getGeneratedKeys() throws SQLException
```

- Operation: It is not supported.
- Exception: It always throws SQLFeatureNotSupportedException.

<a id="6112fdc0e3e414b4"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

- Operation: It returns the max field size. The value limits the maximum length of the column. If the column value is bigger than this length when fetching, the rest of the data is truncated. The default value is 0, and 0 refers that the maximum length is infinite.
- Exception: If the statement is already closed, it throws an exception.

<a id="d749b7d51df04a65"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

- Operation: It returns the max rows. The max rows refer to the maximum number of rows of ResultSet which is got from the statement. The rows more than the maximum number of rows are ignored. The default value is 0, and 0 means infinity.
- Exception: If the statement is already closed, it throws an exception.

<a id="c6b98bf9050ede99"></a>
#### getMoreResults

```
boolean getMoreResults() throws SQLException
```

- Operation: It always returns false because a user can only have a single ResultSet per one execution, currently. The current ResultSet is closed.
- Exception: If the statement is already closed, it throws an exception.

```
boolean getMoreResults(int current) throws SQLException
```

<a id="4ab922e20f7e9e7c"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

- Operation: It gets the value of the query timeout. The value is the timeout value which the sever applies at execution. The execution is canceled and the user gets the error related to timeout if the execution time exceeds the time. The unit is seconds and it applies the default value of the session if the user does not specifically set it. The default value of the session is 0 if it is not set with the property, and it refers to the infinite wait.
- Exception: If the statement is already closed, it throws an exception.

<a id="2212ef8a1e7dafed"></a>
#### getResultSet

```
ResultSet getResultSet() throws SQLException
```

- Operation: It performs the fetch for the currently execution, and it gets part of fetched results, and creates and returns the ResultSet. JDBC specification defines to call this method once per the execution, but it is implemented to return the same object for several calls of the method.
- Exception: If the statement is already closed, it throws an exception. If an error occurs on the server when fetching, it throws an exception.

<a id="e383cc8b9f65d637"></a>
#### getResultSetConcurrency

```
int getResultSetConcurrency() throws SQLException
```

- Operation: It returns the ResultSet concurrency. The value determines the concurrency of ResultSet generated from the object. The default value is ResultSet.CONCUR_READ_ONLY. The updatable cursor is not yet supported.
- Exception: If the statement is already closed, it throws an exception.

<a id="597bfebe797d3717"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- Operation: It returns the ResultSet holdability. The value determines the holdability of ResultSet generated from the object. The default value is ResultSet.HOLD_CURSORS_OVER_COMMIT.
- Exception: If the statement is already closed, it throws an exception.

<a id="1eff836c3bee57f4"></a>
#### getResultSetType

```
int getResultSetType() throws SQLException
```

- Operation: It returns the ResultSet type. The value determines the type of ResultSet generated from the object. The default value is ResultSet.TYPE_FORWARD_ONLY.
- Exception: If the statement is already closed, it throws an exception.

<a id="6b3acef92ce89d0e"></a>
#### getUpdateCount

```
int getUpdateCount() throws SQLException
```

- Operation: It returns the number of rows in which the update for the last execution is reflected. If the last executed SQL statement is not UPDATE statement nor is INSERT statement, it returns -1.
- Exception: It does not occur.

<a id="6992593e66fd935e"></a>
#### getUpdateRowCount

```
long getUpdateRowCount() throws SQLException
```

- Operation: It is as same as getUpdateCount, but the returned type is long. It is non-standard method, and the type casting to GoldilocksStatement should be performed to use it.
- Exception: It does not occur.

<a id="9cd3421b2f234828"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- Operation: It returns SQLWarning accumulated on the object. If it does not exist, it returns null.
- Exception: It does not occur.

<a id="caba758a87935c68"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- Operation: It returns whether the statement is closed. If it is closed, it returns true. Otherwise, it returns false. It can be closed not only by the explicit call of close() but also by the server or the connection object.
- Exception: It does not occur.

<a id="b4be7be74e5503bb"></a>
#### isPoolable

```
boolean isPoolable() throws SQLException
```

- Operation: It returns whether the statement pooling is allowed for this object.
- Exception: It does not occur.

<a id="06f0d4bc38cf7add"></a>
#### setCursorName

```
void setCursorName(String name) throws SQLException
```

- Operation: It sets a name for the cursor created by the currently executed statement.
- Exception: If an error occurs on the server when setting the cursor name, it throws an exception.

<a id="a6be58f5aeee22c1"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

- Operation: JDBC can not ban the feature because the escape processing of the SQL statement is performed in the server parser. Any operation is not performed.
- Exception: If the statement is already closed, it throws an exception.

<a id="998512bc6548e5a3"></a>
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

<a id="916bef7fca18e5e7"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- Operation: It sets the fetch direction. If the direction is not ResultSet.FETCH_FORWARD, it throws an exception because GOLDILOCKS supports only the forward fetch.
- Exception: If the statement is already closed or the direction is not FETCH_FORWARD, it throws an exception.

<a id="5ed498ca484245fe"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- Operation: It sets the default fetch size of ResultSet which is got from the statement object. The default value is 0, and 0 refers that the server determines the number of fetched rows. For more information, refer to [setFetchSize](#1bd33a74e7c9d423) of ResultSet.
- Exception: If the statement is already closed, it throws an exception.

<a id="12a1b17c868f574c"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

- Operation: It sets the max field size. The value limits the maximum length of the column. If the column value is bigger than this length when fetching, the rest of the data is truncated. The default value is 0, 0 refers that the maximum length is infinity. It is valid for CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, LONG VARBINARY types.
- Exception: If the statement is already closed, it throws an exception.

<a id="738b69656d5b5b92"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

- Operation: It sets the max rows. The max rows refers to the maximum number of rows of ResultSet which is got from the statement. The rows more than the maximum number of rows are ignored. The default is 0, and 0 means infinity.
- Exception: If the statement is already closed, it throws an exception.

<a id="1f4d068ee439e58f"></a>
#### setPoolable

```
void setPoolable(boolean poolable) throws SQLException
```

- Operation: It sets whether to pool the statement.
- Exception: It does not occur.

<a id="8ab86b82e3974310"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

- Operation: It sets the value of query timeout. The value is the timeout value which the sever applies at the execution, and the execution is canceled and the user gets the error related to timeout if the execution time exceeds the time. The unit is seconds and it applies the default value of the session if the user idoes not specifically set it. The default value of the session is 0 if it is not set with the property, and 0 refers to the infinite wait.
- Exception: If the statement is already closed, it throws an exception.

<a id="2ec1f4ffc12b334e"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- Operation: It queries whether the object is a class which implements the iface interface. If so, it returns true. Otherwise, it returns false. It does not determine the presence of the wrapper but it only queries only whether the given argument class type is implemented because GOLDILOCKS statement object is not the wrapper of any other class.
- Exception: It does not occur.

<a id="94a1c7aea4df98b4"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- Operation: It eventually returns itself, even when it is unwrapped because GOLDILOCKS statement is not the wrapper of any other class. It returns after casting to that type. If iface is an argument of isWrapperFor() method and false is returned, the method throws an exception.
- Exception: If iface is not the type of the object (when this object returns the unimplemented type), it throws SQLException.

<a id="6710c6267f20e37d"></a>
### Struct

The class is not implemented.

<a id="6ee6b8c9a3342306"></a>
#### getAttributes

```
Object[] getAttributes() throws SQLException
```

<a id="f7f5e8bd1c2922f7"></a>
#### getAttributes

```
Object[] getAttributes(Map<String,Class<?>> map) throws SQLException
```

<a id="13c276481a405bd0"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="7981c8d07a8b8fec"></a>
### XAConnection

<a id="37c60e44f0a3c75e"></a>
#### getXAResource

```
XAResource getXAResource() throws SQLException
```

- Operation: It returns XAResource object which can perform XA command. When the method is called for several times, the same result is continuously returned.
- Exception: It does not occur.

<a id="54d227ea8c66d9aa"></a>
### XADataSource

<a id="0253910e4a389977"></a>
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

<a id="5c51830a20f8fed1"></a>
### XAResource

<a id="3a3fdffeb4d20359"></a>
#### commit

```
void commit(Xid xid, boolean onePhase) throws XAException
```

- Operation: It performs the XA commit command for the global transaction xid. If onePhase is set to true, one phase commit is performed.
- Exception: If the execution result error occurs, it throws XAException.

<a id="8ac481bcd17192b1"></a>
#### end

```
void end(Xid xid, int flags) throws XAException
```

- Operation: It performs the XA end command for the global transaction xid. The flags may be one of TMSUCCESS, TMFAIL, or TMSUSPEND.
- Exception: If the execution result error occurs, it throws XAException.

<a id="500dbac955bb3d4b"></a>
#### forget

```
void forget(Xid xid) throws XAException
```

- Operation: It performs the XA forget command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="c7e494b6517daddb"></a>
#### getTransactionTimeout

```
int getTransactionTimeout() throws XAException
```

- Operation: GOLDILOCKS does not support the transaction timeout. It always return 0.
- Exception: It does not occur.

<a id="1d301263144335b7"></a>
#### isSameRM

```
boolean isSameRM(XAResource xares) throws XAException
```

- Operation: It has the unique rmid when XAResource object is created. Whether it is the same XAResource object is determined with this rmid.
- Exception: It does not occur.

<a id="6312065daf4b73fb"></a>
#### prepare

```
int prepare(Xid xid) throws XAException
```

- Operation: It performs the XA prepare command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="c4618c3b0ca4a717"></a>
#### recover

```
Xid[] recover(int flag) throws XAException
```

- Operation: It performs XA recover command with the given flag, and the array of the prepared transaction branches is returned. The flag may be one of TMSTARTRSCAN, TMENDRSCAN, TMNOFLAGS.
- Exception: If the execution result error occurs, it throws XAException.

<a id="5fb8602d76238bb5"></a>
#### rollback

```
void rollback(Xid xid) throws XAException
```

- Operation: It performs the XA rollback command for the global transaction xid.
- Exception: If the execution result error occurs, it throws XAException.

<a id="8fb530aa047275a5"></a>
#### setTransactionTimeout

```
boolean setTransactionTimeout(int seconds) throws XAException
```

- Operation: GOLDILOCKS does not support the transaction timeout. Any operation is not performed.
- Exception: It does not occur.

<a id="9590c824b2b23a03"></a>
#### start

```
void start(Xid xid, int flags) throws XAException
```

- Operation: It starts the global transaction with the given flag. The flag may be one of TMNOFLAGS, TMJOIN, TMRESUME.
- Exception: If the execution result error occurs, it throws XAException.

<a id="d4511de4af40986a"></a>
### GoldilocksInterval

To give value to a column of GOLDILOCKS by using a GoldilocksInterval object, refer to [Using Other Data Types](#ffdc3b15ea1df333).

<a id="f4d671068894fdc6"></a>
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

<a id="e4a9f1fcc906c310"></a>
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

<a id="062962745692b92b"></a>
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

<a id="26819fea86d721fa"></a>
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

<a id="828f2cc94ac5f482"></a>
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

<a id="de197dc850c6a981"></a>
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

<a id="afe2efd4fa4dc774"></a>
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

<a id="88fca715b01369f3"></a>
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

<a id="1bb9426b9cf5882d"></a>
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

<a id="14ddc4037c1c1a6b"></a>
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

<a id="6097f81c5e3eb7ec"></a>
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

<a id="3734a0ad02043660"></a>
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

<a id="4c7e52b4aaa771b0"></a>
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

<a id="38d9b565ae5d3b5c"></a>
#### getSign

```
public int getSign()
```

- Operation: If the time is a positive number, 1 is returned. If the time is a negative number, -1 is returned.
- Exception: It does not occur.

<a id="e1a77665611e6def"></a>
#### getYear

```
public int getYear()
```

- Operation: It returns the year value. Whether the interval object is a negative number is not returned through getYear().
- Exception: It does not occur.

<a id="18c2999e3f69199b"></a>
#### getMonth

```
public int getMonth()
```

- Operation: It returns the month value. Whether the interval object is a negative number is not returned through getMonth().
- Exception: It does not occur.

<a id="d95993ed6b10effe"></a>
#### getAccumulatedMonth

```
public int getAccumulatedMonth()
```

- Operation: It converts the value of year and month to the value of month, and returns the result.
- Exception: It does not occur.

<a id="2949877928dcd3f3"></a>
#### getDay

```
public int getDay()
```

- Operation: It returns the day value. Whether the interval object is a negative number is not returned through getDay().
- Exception: It does not occur.

<a id="c61c67c3c808e3ae"></a>
#### getHour

```
public int getHour()
```

- Operation: It returns the hour value. Whether the interval object is a negative number is not returned through getHour().
- Exception: It does not occur.

<a id="a10c2d9900835d93"></a>
#### getAccumulatedHour

```
public int getAccumulatedHour()
```

- Operation: It converts the value of day and hour to the value of hour, and returns the result.
- Exception: It does not occur.

<a id="d928b05175f1fad4"></a>
#### getMinute

```
public int getMinute()
```

- Operation: It returns the minute value. Whether the interval object is a negative number is not returned through getMinute().
- Exception: It does not occur.

<a id="13df6a669152994c"></a>
#### getAccumulatedMinute

```
public int getAccumulatedMinute()
```

- Operation: It converts the value of day, hour and minute to the value of minute, and returns the result.
- Exception: It does not occur.

<a id="85ca3b3d83fc5416"></a>
#### getSecond

```
public int getSecond()
```

- Operation: It returns the second value. Whether the interval object is a negative number is not returned through getSecond().
- Exception: It does not occur.

<a id="5e2f58a0215bcea8"></a>
#### getAccumulatedSecond

```
public int getAccumulatedSecond()
```

- Operation: It converts the value of day, hour, minute and second to the value of second, and returns the result.
- Exception: It does not occur.

<a id="e2541f594a1917cc"></a>
#### getMicroSecond

```
public int getMicroSecond()
```

- Operation: It returns the microsecond value. Whether the interval object is a negative number is not returned through getMicroSecond().
- Exception: It does not occur.

<a id="e3331dbd6ef4fbdd"></a>
#### getAccumulatedMicroSecond

```
public long getAccumulatedMicroSecond()
```

- Operation: It converts the value of day, hour, minute, second and microsecond to the value of microsecond, and returns the result.
- Exception: It does not occur.

<a id="ed0b45ca1cf8db48"></a>
#### getTypeName

```
public String getTypeName()
```

- Operation: The type name is returned.
- Exception: It does not occur.

<a id="264f55d5c9136d9f"></a>
#### getSqlType

```
public int getSqlType()
```

- Operation: The type of this object is returned as the type constant defined in GoldilocksTypes.
- Exception: It does not occur.

<a id="7660647cd14362be"></a>
#### toString

```
public String toString()
```

- Operation: The interval value which is indicated by this object is returned as a string value.
- Exception: It does not occur.

<a id="5189514530c88154"></a>
### GOLDILOCKS Type

<a id="a53190b1370f2463"></a>
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

These constants are used as like the constants of java.sql.Types. In other words, they are used when specifying the types in setObject of PreparedStatement or the types in getObject of ResultSet. These types are separately provided by GoldilocksTypes because they are not defined in the JDBC standard.

<a id="55781271b90c5d33"></a>
### Type Conversion

The following tables describe how to convert types.

**SQL types → GOLDILOCKS types**

<a id="e2eaca60f3630d26"></a>
| SQL type | GOLDILOCKS type |
| --- | --- |
| Types.BIGINT | NATIVE_BIGINT |
| Types.BINARY | BINARY(2000) |
| Types.BIT | BOOLEAN |
| Types.BOOLEAN | BOOLEAN |
| Types.BLOB | LONG VARBINARY |
| Types.CHAR | CHAR(2000) |
| Types.CLOB | LONG VARCHAR |
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

<a id="3ad95d69b475c64d"></a>
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
| getClob | O | O | O | O | O |
| getBlob | raw data | raw data | raw data | raw data | raw data |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Short | Integer | Long | Float | Double |
| getRowId | X | X | X | X | X |

**Whether supporting getter method for GOLDILOCKS Type - 2**

<a id="dec1725736a270e7"></a>
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
| getClob | "TRUE" or "FALSE" | O | O | O | O |
| getBlob | raw data | raw data | raw data | raw data | raw data |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Boolean | BigDecimal | String | byte[] | RowId |
| getRowId | X | X | X | X | O |

**Whether supporting getter method for GOLDILOCKS Type - 3**

<a id="78094da0e28f70bf"></a>
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
| getClob | O | O | O | O |
| getBlob | raw data | raw data | raw data | raw data |
| getArray | X | X | X | X |
| getRef | X | X | X | X |
| getURL | X | X | X | X |
| getObject | Date | Time | Timestamp | GoldilocksInterval |
| getRowId | X | X | X | X |

---

[← 31. ODBC](31-odbc.md) · [Table of contents](../README.md) · [33. Embedded SQL →](33-embedded-sql.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
