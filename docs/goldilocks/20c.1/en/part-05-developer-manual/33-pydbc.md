<a id="fb576ef1f9d217df"></a>

# 33. PyDBC

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/fb576ef1f9d217df)  
> Tag: `20c.1_30_tag`

[← 32. PDO](32-pdo.md) · [Table of contents](../README.md) · [34. Hibernate →](34-hibernate.md)

<a id="490bcb62696d8e1d"></a>
## GOLDILOCKS PyDBC

<a id="c0826b7711030866"></a>
### Overview

PyDBC programs Python accessing GOLDILOCKS database by using API which complies with [Python Database API Specification v2.0(PEP 249)](https://www.python.org/dev/peps/pep-0249/).

PyDBC requires the Python standard library, and the internal operation which connects to and operate GOLDILOCKS database requires ODBC library because it calls ODBC API. PyDBC uses gdlcs in ODBC library *$GOLDILOCKS_HOME/lib* by default, and the user can modify it by updating *setup.py*.

The internal operation of PyDBC uses ODBC driver, so it is as same as [Overview of ODBC Components](29-odbc.md#d337e9a65f3e454c). There are an architecture of which an application links to the driver manager, and an architecture of which an application links to GOLDILOCKS ODBC driver library.

<a id="a19a4b1ab65f5efe"></a>
### Version

The information of GOLDILOCKS PyDBC version can be viewed by executing *pygoldilocks.so* file as follows.

```
shell>python
>>> import pygoldilocks
>>> print pygoldilocks.version
3.2.0
```

The current version of GOLDILOCKS PyDBC driver is 3.2.0 according to GOLDILOCKS version, and this driver complies with the standard Python database API 2.0. PyDBC driver supports Python 2.7, 3.4, 3.5, 3.6 versions, and PyDBC driver library should be installed according to each Python version.

<a id="7315907ef454d6da"></a>
### Installation

The source should be built to install PyDBC. PyDBC links gdlcs library in GOLDILOCKS_HOME/lib and it includes *goldilocks.h* header file in GOLDILOCKS_HOME/include, so the environment variable GOLDILOCKS_HOME should be set in an appropriate position.

When installing PyDBC, the bit of Python should be as same as that of GOLDILOCKS library. Therefore, if GOLDILOCKS is built in 32 bit, then PyDBC should be installed by using Python 32 bit.

<a id="c832bff111861bfd"></a>
#### Installation on Linux

Linux requires the gcc compiler, and it is built as follows.

```
shell> sudo python setup.py install
```

> It does not support HP-UX nor AIX platform.

<a id="dbfec13c18617823"></a>
#### Installation on Windows

It is built on Windows as follows.

```
shell> python setup.py install
```

An appropriate Microsoft Visual C++ compiler according to python version is required to compile PyDBC  
For more information, refer to [https://wiki.python.org/moin/WindowsCompilers](https://wiki.python.org/moin/WindowsCompilers).

- Visual Studio 2003.NET compiler is required to build Python version 2.4 or 2.5, and there is not a freeware for this version.
- Visual C++ 2008 compiler is required to build Python version 2.6, 2.7, 3.0, 3.2, and the freeware for this version is Visual C++ 2008 Express.
- Visual C++ 2010 compiler is required to build Python version 3.3, 3.4, and the freeware for this version is Visual C++ 2010 Express.
- Visual C++ 2014 or VC 2017 compiler is required to build Python version 3.5, 3.6.
- Visual C++ 2017 compiler is required to build Python version 3.7.

<a id="6cef8eb7e334adc3"></a>
### Examples

<a id="e2996dec2349b93a"></a>
#### Obtaining Connection Class

PyDBC implicitly calls ODBC library. Therefore, [the data source](29-odbc.md#bd6b4a774ef02591) should be configured to obtain the connection.

- Obtain the connection as follows.

```
import pygoldilocks
cnxn = pygoldilocks.connect( 'DSN=GOLDILOCKS;UID=test;PWD=test' )
```

Call connect which is an internal function of pygoldilocks, a module of PyDBC, to obtain the connection.

> [Data Source](29-odbc.md#bd6b4a774ef02591) should be built in advance to use DSN.

If CHARSET is not set in DSN, then ODBC library sets it to Console Character Set. PyDBC implicitly performs the basic encoding for the character set used by ODBC. If the character set used in GOLDILOCKS server is different from that in ODBC library, then the data conversion occurs and it degrades the performance. For example, CP949 is used as a basic character set in Windows. If nothing is set, PyDBC implicitly uses CP949(UHC) when encoding, and ODBC library also uses UHC when processing the character set.

The followings are how to alter the character set of the client.

- Alter CHARSET property in [Data Source Configuration](29-odbc.md#bd6b4a774ef02591).
- Add CHARSET property to the connection string. 
- Use attrs_before keyword in connect method of pygoldilocks module.

All of the three methods above alter the connection property of ODBC, SQL_ATTR_CHARACTER_SET, and set the encoding of PyDBC library as well.

<a id="53d62cea7bb55b8c"></a>
#### Using Cursor and Row Class

A cursor and a row class can be used as follows.

```
cursor = cnxn.cursor()
cursor.execute( "SELECT NAME, ADDRESS FROM EMP" )

rows = cursor.fetchall()

for row in rows:
    print row.A, row.B

cursor.close()
cnxn.close()
```

<a id="bb09f1df2e6b29a5"></a>
## API Reference

<a id="9a1890e92ac3a5d7"></a>
### pygoldilocks Module

pygoldilocks object complies with [Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/).  
For more information, refer to [Python DB API module](https://www.python.org/dev/peps/pep-0249/#module-interface).

<a id="eada53ac9521a859"></a>
#### Properties

- version
    - The version of pygoldilocks module follows that of GOLDILOCKS database. The version is a string in a form of major.minor.patch.

- apilevel
    - It indicates DB API level 2.0, and the value is "2.0" character string constant.

- lowercase
    - It controls whether to convert the column name from the row object of the result value to lowercase. The default value is false. It is useful when the case of database column does not conform.

- threadsafety
    - It is constant 1, and it does not share the connection even when threads share the module.

- paramstyle
    - It indicates a parameter and the value is the character string constant "qmark" which means a question mark.

<a id="01db3009707b27dc"></a>
#### connect

It newly connects to the database.

```
connect( *connectionstring, **kwargs )
```

It inputs the ODBC connect string and keywords. The keywords are as follows.

<a id="125b6240b5eb6ddb"></a>
| Keyword | Description | Default value |
| --- | --- | --- |
| attrs_before | It sets properties which should be set before the connection. It receives the value in dictionary type. | - |
| autocommit | It sets whether to auto commit. If it is false, connection.commit should be called to reflect it in the database. | False |
| readonly | If it is true, the connection is set to readonly. | False |
| timeout | It sets the timeout for the connection. SQL_ATTR_LOGIN_TIMEOUT is set. | - |

- attrs_before
    - It sets options which is to be set before the connection. These options are set by using [SQLSetConnectAttr](29-odbc.md#98a6503b22b3e1f1). It receives the properties and values in dictionary type. For more information about configuration, refer to [ODBC attributes](29-odbc.md#ef242bc360494269).

```
cnxn =  pygoldilocks.connect( "DSN=GOLDILOCKS", attr_before={ pygoldilocks.SQL_ATTR_MAX_ROWS : 1000 })
```

<a id="34e61ec1b84981f5"></a>
#### Date

```
>>> print pygoldilocks.Date(1984,11,23),  type(pygoldilocks.Date(1984,11,23))
1984-11-23 <type 'datetime.date'>
```

It creates a date object corresponding to the given value.

<a id="25c17d9f565ffd43"></a>
#### Time

```
>>> print pygoldilocks.Time(11,23,23), type(pygoldilocks.Time(11,23,23))
11:23:23 <type 'datetime.time'>
```

It creates a time object corresponding to the given value.

<a id="4b273684a53929df"></a>
#### Timestamp

```
>>> print pygoldilocks.Timestamp(1984,11,23,11,23,23), type(pygoldilocks.Timestamp(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

It creates a datetime object corresponding to the given value.

<a id="74f6dc0d971e6177"></a>
#### DATETIME

```
>>> print pygoldilocks.DATETIME(1984,11,23,11,23,23), type(pygoldilocks.DATETIME(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

It creates a datetime object corresponding to the given value. It is as same as [Timestamp](#4b273684a53929df).

<a id="1546b5064858b2d1"></a>
#### Binary

```
>>> print pygoldilocks.Binary('binary'), type(pygoldilocks.Binary('binary'))
binary <type 'bytearray'>
```

It creates a bytearray object corresponding to the given value. It is as same as [BINARY](#f8ace02f54ea2673).

<a id="f8ace02f54ea2673"></a>
#### BINARY

```
>>> print pygoldilocks.BINARY('binary'), type(pygoldilocks.BINARY('binary'))
binary <type 'bytearray'>
```

It creates a bytearray object corresponding to the given value.

<a id="fcbf5be83435cca7"></a>
#### STRING

```
>>> print pygoldilocks.STRING('str'), type(pygoldilocks.STRING('str'))
str <type 'str'>
```

It creates an str object corresponding to the given value.

<a id="b9d46c15814df87e"></a>
#### NUMBER

```
>>> print pygoldilocks.NUMBER(100.001), type(pygoldilocks.NUMBER(100.001))
100.001 <type 'float'>
```

It creates a float object corresponding to the given value.

<a id="6790374b59f57097"></a>
#### ROWID

```
>>> print pygoldilocks.ROWID('AA'), type(pygoldilocks.ROWID('AA'))
AA <type 'str'>
```

It is used to describe the row ID column of the database, and returns an str object.

<a id="3f4a66783a858b75"></a>
#### TimeFromTicks

```
>>> print pygoldilocks.TimeFromTicks( 10 )
09:00:10
```

It returns a datetime.time object which is set as an argument value.

<a id="39a345218c3f0e1a"></a>
#### DateFromTicks

```
>>> print pygoldilocks.DateFromTicks( 360000 )
1970-01-05
```

It returns a datetime.date object which is set as an argument value.

<a id="6b328eba9782f54e"></a>
#### TimestampFromTicks

```
>>> print pygoldilocks.DateFromTicks( 360000 )
1970-01-05
```

It returns a datetime.timestamp object which is set as an argument value.

<a id="bd06d6eafc637512"></a>
#### setDecimalSeparator

It sets the decimal point delimiter in NUMERIC type obtained from the database. The default value uses a period (.).

<a id="4698fd178428000d"></a>
#### getDecimalSeparator

It obtains the set decimal point delimiter in NUMERIC type.

<a id="4b1b64b9309307bc"></a>
### Connection

It is an object managing the connection with the database, and it is created with connect() function of pygoldilocks module.

<a id="40231110c4328aa9"></a>
#### Properties

- autocommit
    - It can set the autocommit mode of the connection.

- searchescape
    - It obtains an escape character of ODBC. pygoldilocks uses '/'.

- timeout
    - It sets SQL_ATTR_QUERY_TIMEOUT by using SQLSetConnectAttr function.

<a id="0a52bc5c7c29fee9"></a>
#### Functions

- cursor()
    - It returns a new cursor object.

- commit()
    - It commits the executed SQL statement.

- rollback()
    - It rolls back the executed SQL statement.

- close()
    - It closes the connection. If the autocommit is false, then the SQL statement which was not committed is rolled back.

- getinfo( info )
    - It can obtain the connection properties by using SQLGetInfo function of ODBC. For more information, refer to [SQLGetInfo](29-odbc.md#db49de4dc2a5539f).

```
dns_name = cnxn.getinfo( pygoldilocks.SQL_DATA_SOURCE_NAME )
```

- execute( sql, [*params] )
    - It creates a new cursor object, and executes execute function of this object, then returns a cursor object.

```
cursor = cnxn.execute( "SELECT COUNT(*) FROM EMP" )
```

For more information, refer to Cursor.execute() function. This function does not exist in Python API, but it is provided for the convenience. Whenever this function is called, a cursor object is allocated, so it is not recommended to use it when it is required to execute one or more SQL statements.

- set_attr( attr_id, value )
    - The connection properties can be set by executing SQLSetConnectAttr function. 
    - The following is an example of controlling the transaction isolation level of the database by using set_attr function.

```
connection.set_attr( pygoldilocks.SQL_ATTR_TXN_ISOLATION, pygoldilocks.SQL_TXN_SERIALIZABLE )
```

<a id="e18046c47dfd79a8"></a>
### Cursor

Generally, a cursor object means the database cursor which is used to manage the fetch operation. The database cursor is mapped to ODBC statement handle (HSTMT). The cursor objects which is created by the same connection are not separated. In other words, all updates executed by a cursor to the database are also applied to other cursors.

> Cursor does not manage the database transaction, but the connection commits or rolls back the transaction.

<a id="074d3f449927513b"></a>
#### Properties

<a id="43c49a36780c2538"></a>
##### Description

It is the read-only property, and it includes the contents for each column which was returned by SELECT statement executed last with tuple type. Each tuple includes the followings.

1. Column name (or alias)
2. Type code
3. Display size
4. Internal size
5. Precision
6. Scale
7. Nullable

When SELECT statement is not called, then the description is none.

<a id="e29be188d3ccac1e"></a>
##### rowcount

It is the number of rows which were updated by SQL statement which was executed last.

<a id="f41b90a0443e0d1c"></a>
##### arraysize

It is the number of rows which can be fetched per one time by using [fetchmany( [size = cursor.arraysize] )](#094ed007d5fe89bf) function. The default value 1.

<a id="5b72b28578e14780"></a>
##### connection

It is the read-only property, and it indicates the connection object which created the corresponding cursor object.

<a id="b35c485cdef9d5fb"></a>
##### fast_executemany

If it is set to true, then makes the parameters in array and executes them at once when executing [executemany( sql, [*params] )](#878276028153c736) function. If it is set to false, it separately executes each parameter.

<a id="a5a1d920e7d7e1ce"></a>
#### Function

<a id="a01c405407ab4432"></a>
##### execute( sql, [*params] )

It executes SQL statement through SQLPrepare and SQLExecute functions, then returns a cursor which called this function.   
The parameter option can be used as follows.

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", x, y )
```

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", (x, y) )
```

<a id="878276028153c736"></a>
##### executemany( sql, [*params] )

It executes SQL statement for each parameter and returns *none*. Parameter *params* should be a sequence type of a sequence or a sequence generator.

```
params = [ ( 1, 'A' ), ( 2, 'B' ) ]
cursor.executemany("INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", params)
```

SQL statement is executed twice in the example above. In other words, it is separately executed for  ( 1, 'A' ) and ( 2, 'B') each. The operation of executemany depends on whether fast_executemany of a cursor object is set to true or false.

The example above is as same as follows.

```
params = [ ( 1, 'A' ), ( 2, 'B' ) ]
for p in params:
    cursor.execute( "INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", p )
```

If fast_executemany is set to true, executemany processes the operation with only a single execute. For that, data in the same index location in items of parameter *params* should be the same data type.

```
params = [ ( 1, 'A' ), ( '2', 'B' ) ]
cursor.executemany("INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", params)
```

In the example above, the data type of the first item among two items of parameter params is different. Likewise, the data type on the same index location between items are different, then executemany does not process SQL statement at once, but separately processes it.

If the autocommit of a connection object is true, then SQL statement is processed being splited and each SQL statement is separately committed. If an error occurs while sequentailly processing records, then only some records are committed to the database and the operation is completed leaving some records are not committed. Therefore, it is recommended to set autocommit to false to check if all records are committed to the database when using executemany().

<a id="06d3008fd87617d3"></a>
##### fetchone()

It returns the next row of the query. If the next data does not exist, it is *none*.

<a id="6f6ee4bcf2c5fab9"></a>
##### fetchall()

It returns all rows left in the query. Be cautious when using it because it reads all rows to the memory.

<a id="094ed007d5fe89bf"></a>
##### fetchmany( [size = cursor.arraysize] )

It returns rows which were left as many as size or cursor.arraysize. The next data returns an empty sequence data. The default value of cursor.arraysize is 1.

<a id="d7ceca007794fbdd"></a>
##### commit()

It commits SQL statement. It is a function executed by a connection object which created a cursor object, and it is applied to all cursor which were created in the same connection object. It is as same as commit of the connection object.

<a id="868b2e5d60304bed"></a>
##### rollback()

It rolls back SQL statement. It is a function executed by a connection object which created a cursor object, and it is applied to all cursor which were created in the same connection object. It is as same as rollback of the connection object.

<a id="238905756feb8434"></a>
##### skip( count )

It passes through the record through SQLFetchScroll and SQL_FETCH_NEXT as many times as it is set in count.

<a id="ee751df242b85841"></a>
##### nextset()

It returns false because GOLDILOCKS ODBC does not support SQLMoreResults.

<a id="dc9edbf8a504c24d"></a>
##### close()

It closes a cursor object.

<a id="9b5499113165f50b"></a>
##### setinputsizes( size_list )

It is an optional function, and receives sequence type as a parameter. It sets INPUT parameter size of SQLBindParameter.

<a id="315bc8326f0f3bc2"></a>
##### setoutputsize( size )

It is an optional function, and is used for a purpose which is different from that of DB API, and it allocates the buffer size of OUTPUT parameter.

<a id="8571210874a39669"></a>
##### callproc( procname [, params] )

It calls the storage procedure corresponding to procname. The parameter should be a sequence type, and it includes the output parameter. However, data located in the output parameter when inputting is meaningless. callproc function updates data corresponding to INOUT, OUT of the input parameter data, and returns it in sequence type.

```
create_proc = """CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 OUT CHAR(10) )
IS 
  V1 CHAR(10);
BEGIN
  SELECT T1.I1
    INTO V1
    FROM T1
    WHERE T1.I1 >= A1 AND T1.I1 <= A1;
  A2 := V1;
END;\
"""

cursor.execute( create_proc )

result = cursor.callproc( 'PROC1', ( 1, 0 ) )
```

<a id="e6644ae596d633fc"></a>
##### callfunc( funcname [, params] )

It calls a function corresponding to funcname. callfunc() returns the function data.

```
create_func = """
CREATE OR REPLACE FUNCTION FUNC1( A1 INTEGER, A2 INTEGER )
  RETURN INTEGER
  IS
    V1 INTEGER;
  BEGIN

    SELECT COUNT(*)
      INTO V1
      FROM T1
      WHERE T1.I1 >= A1 AND T1.I1 <= A2;

    RETURN V1;
  END;\
"""

cursor.execute( create_func )
cursor.commit()

result = cussr.callfunc( 'FUNC1', ( 1,  4) )
```

<a id="e5650d1205016fae"></a>
##### tables( table=None, catalog=None, schema=None, tableType=None )

It returns the table information of the database which satisfies the given condition. The character  '_' and '%' are translated as a wild card. Each row has the following column information. For more information, refer to [SQLTables](29-odbc.md#358f11958076274d).

1. table_cat: It is the name of the catalog.
2. table_schem: It is the name of the schema.
3. table_name: It is the name of the table.
4. table_type: 'TABLE', 'VIEW', 'SYSTEM TABLE', 'GLOBAL TEMPORARY', 'LOCAL TEMPORARY', 'IMMUTABLE TABLE', 'ALIAS', 'SYNONYM' or a specific type name can be a table type. 
5. remarks: It is a description of a table.

```
print cursor.tables( table= 'TEST' ).fetchone()

#print table name
for row in cursor.tables():
 print row.table_name
```

> If a parameter is empty, information of all table of which a user has a privilege is returned.

<a id="b16e6011a51cd481"></a>
##### columns( table=None, catalog=None, schema=None, tableType=None )

It obtains the column information of the specified table through [SQLColumns](29-odbc.md#daadb0282be38696) function. Each row includes the following column information.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. data_type
6. type_name
7. column_size
8. buffer_length
9. decimal_digits
10. num_prec_radix
11. nullable
12. remarks
13. column_def
14. sql_data_type
15. sql_datetime_sub
16. char_octet_length
17. ordinal_position
18. is_nullable: SQL_NULLABLE, SQL_NO_NULLS or SQL_NULLS_UNKNOWN.

```
#print column name of table TEST
for r in cursor.columns( table = 'TEST' ):
    print r.column_name
```

<a id="b3d451e696a32002"></a>
##### statistics( table, catalog=None, schema=None, unique=False, quick=True )

It obtains the information about the specified table through [SQLStatistics](29-odbc.md#4f8552719ad32620) function.  
If unique is true, it returns an unique index, and if it is false, it returns all indexes.  
If quick is true, CARDINALYTIY and PAGES are returned only when it is instantly available, otherwise, NULL is returned to the corresponding column.

1. table_cat
2. table_schem
3. table_name
4. non_unique
5. index_qualifier
6. index_name
7. type
8. ordinal_position
9. column_name
10. asc_or_desc
11. cardinality
12. pages
13. filter_condition

> A wildcard character is not allowed.

<a id="e903c4ea00d63c3f"></a>
##### rowIdColumns( table, catalog=None, schema=None, nullable=True )

It returns the result set of columns which uniquely identifies a row by executing [SQLSpecialColumns](29-odbc.md#65ad5d5f831006ba) with SQL_BEST_ROWID. Each row includes the following column information.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, or SQL_SCOPE_SESSION
2. column_name
3. data_type: SQL type constant of ODBC
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO or SQL_PC_PSEUDO

<a id="02bcc1e9c22509d9"></a>
##### rowVerColumns( table, catalog=None, schema=None, nullable=True )

It returns the result set of columns which are automatically updated when a row is updated by executing [SQLSpecialColumns](29-odbc.md#65ad5d5f831006ba) with SQL_ROWVER. Each row includes the following column information.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, or SQL_SCOPE_SESSION
2. column_name
3. data_type: SQL type constant of ODBC
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO, or SQL_PC_PSEUDO

<a id="bd310945f6870047"></a>
##### primaryKeys( table, catalog=None, schema=None )

It returns the result set of columns which configures major keys of a table by executing [SQLPrimaryKeys](29-odbc.md#a6257df6d70933bb) function. Each row includes the following column information.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. key_seq
6. pk_name

<a id="8ef703cbd6c77466"></a>
##### foreignKeys( table=None, catalog=None, schema=None, foreignTable=None, foreignCatalog=None, foreignSchema=None )

It creates the result set of column names of a specified table, or the result set of column names which are foreign keys of another table referring to the basic key of the specified table, by executing [SQLForeignKeys](29-odbc.md#4a43ff90f1499844) function. Each row includes the following column information.

1. pktable_cat
2. pktable_schem
3. pktable_name
4. pkcolumn_name
5. fktable_cat
6. fktable_schem
7. fktable_name
8. fkcolumn_name
9. key_seq
10. update_rule
11. delete_rule
12. fk_name
13. pk_name
14. deferrability

<a id="753fcc4ef0c4530f"></a>
##### procedures( procedure=None, catalog=None, schema=None )

It creates the result set of the information about the procedure by executing [SQLProcedures](29-odbc.md#6cc21c4a767fc99b). Each row includes the following column information.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. num_input_params
5. num_output_params
6. num_result_sets
7. remarks
8. procedure_type

<a id="53f7b86a269d87db"></a>
##### getTypeInfo( sqlType=None )

It creates the result set of the information about the specified data type or about all data types which are supported by GOLDILOCKS ODBC, by executing [SQLGetTypeInfo](29-odbc.md#d6bf633fc15ec040) function. Each row includes the following column information.

1. type_name
2. data_type
3. column_size
4. literal_prefix
5. literal_suffix
6. create_params
7. nullable
8. case_sensitive
9. searchable
10. unsigned_attribute
11. fixed_prec_scale
12. auto_unique_value
13. local_type_name
14. minimum_scale
15. maximum_scale
16. sql_data_type
17. sql_datetime_sub
18. num_prec_radix
19. interval_precision

<a id="60e130279ed8389d"></a>
### Row

A row object is returned with fetch function of a cursor object. It is processed as a tuple type as described in DB API.

```
row = cursor.fetchone()
for column in row:
    print column
```

The following features are added to pygoldilocks.

- It can access the data by using a column name. 
- It can access the value of cursor.description through a row even after a cursor object is closed.
- It can update the value of a row.

Accessing to a row by using a column name is not only convenient but it also improves the readability. However, if a column name includes Python reserved name or a whitespace, then it be accessed only through row.__getattribute__().

```
cursor.execute( "select c1 from test")
print cursor.description
row = cursor.fetchone()
print row.C1
```

```
(('C1', <type 'str'>, 10, 10, 10, 0, True),)
test
```

> Basically, the identifier of GOLDILOCKS database is uppercase. However, sometimes it is required to be specified in lowercase, so be cautious of using uppercase or lowercase when accessing to a row by using a column name.

<a id="4708704bef195851"></a>
#### Properties

- cursor_description

It is the copy of property description of a cursor object which created the corresponding row. For more information, refer to [Cursor.description](#074d3f449927513b).

<a id="ba9f3815c1d4ea1e"></a>
## Exception

Python exceptions occur by pygoldilocks when GOLDILOCKS ODBC detects an error. The exception classes are as follows, which are as same as [Python DB API](https://www.python.org/dev/peps/pep-0249/#exceptions).

- Error
    - DatabaseError
        - DataError
        - OperationalError
        - IntegrityError
        - InternalError
        - ProgrammingError
        - NotSupportedError

If an error occurs, generally, the exception is processed based on SQLSTATE value provided by the database.

<a id="c03fd88561586541"></a>
| SQLSTATE | Exception |
| --- | --- |
| 0A000 | NotSupportedError |
| 01002 | OperationalError |
| 08001 | OperationalError |
| 08003 | OperationalError |
| 08004 | OperationalError |
| 08007 | OperationalError |
| 08S01 | OperationalError |
| 28000 | InterfaceError |
| 40002 | IntegrityError |
| 22*** | DataError |
| 23*** | IntegrityError |
| 24*** | ProgrammingError |
| 25*** | ProgrammingError |
| 42*** | ProgrammingError |

<a id="fa1913decf705fcf"></a>
## Data Type

<a id="d5d9afa63bb6bde7"></a>
### Transferring Python Parameter to GOLDILOCKS

The data is converted as follows when transferring Python parameter to GOLDILOCKS ODBC.

**Python 3**

<a id="dfe67508de057336"></a>
| Python datatype | Description | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | UTF-8 | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytes, bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | bit | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| int | integer | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

**Python 2**

<a id="0f027dcdec50f9ef"></a>
| Python datatype | Description | ODBC datatype |
| --- | --- | --- |
| None |  | SQL_VARCHAR |
| str | UTF-8 | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| buffer | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | bit | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| int | integer | 32 bit: SQL_INTEGER, 64 bit: SQL_BIGINT |
| long | bigint | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

<a id="53b64e9212ab86cb"></a>
### SQL Value Received from GOLDILOCKS

The data is converted as follows when transferring the data of GOLDILOCKS database to Python.

**Python 3**

<a id="1842eb12e183f503"></a>
| ODBC datatype | Description | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY_SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.timestamp |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |

**Python 2**

<a id="2858ace8cdac6506"></a>
| ODBC datatype | Description | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY_SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.timestamp |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |

The text of Python data type is converted to unicode in Python 3. It is converted to the unicode or a string according to the character set of the database in Python 2.

**Python 2 text**

<a id="271a41cc1a843c2f"></a>
| DB character set | Python type |
| --- | --- |
| UTF-8 | str |
| SQL_ASCII | str |
| UHC | unicode |
| GB18030 | unicode |

---

[← 32. PDO](32-pdo.md) · [Table of contents](../README.md) · [34. Hibernate →](34-hibernate.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
