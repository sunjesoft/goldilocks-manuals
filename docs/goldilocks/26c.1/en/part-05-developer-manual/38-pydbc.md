<a id="68c7082c3f84e6f6"></a>

# 38. PyDBC

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/68c7082c3f84e6f6)  
> Tag: `26c.1_0_tag`

[← 37. PDO](37-pdo.md) · [Table of contents](../README.md) · [39. aiogoldilocks →](39-aiogoldilocks.md)

<a id="52b2b527e3527c3c"></a>
## GOLDILOCKS PyDBC

<a id="0e46af515a0f01df"></a>
### Overview

PyDBC programs Python accessing GOLDILOCKS database by using API which complies with [Python Database API Specification v2.0(PEP 249)](https://www.python.org/dev/peps/pep-0249/).

PyDBC requires the Python standard library, and the internal operation which connects to and operate GOLDILOCKS database requires ODBC library because it calls ODBC API. PyDBC uses gdlcs in ODBC library *$GOLDILOCKS_HOME/lib* by default, and the user can modify it by updating *setup.py*.

The internal operation of PyDBC uses ODBC driver, so it is the same as [Overview of ODBC Components](34-odbc.md#6454d2401b9429d0). There are an architecture of which an application links to the driver manager, and an architecture of which an application links to GOLDILOCKS ODBC driver library.

<a id="1c22d970b52284f1"></a>
### Driver Version

The version of the GOLDILOCKS PyDBC driver is managed in accordance with the GOLDILOCKS product release version. All PyDBC libraries included in the same product release use the same driver version, although their file formats may differ depending on the Python version or operating system.

The installed PyDBC driver version can be checked using the version attribute of the pygoldilocks module.

```
shell>python
>>> import pygoldilocks
>>> print( pygoldilocks.version )
X.Y.Z (The output X.Y.Z indicates the version of the PyDBC driver installed in the current Python environment.)
```

The PyDBC driver version is different from the version of the Python Database API specification. PyDBC complies with Python Database API Specification v2.0 (PEP 249). The version number 2.0 refers to the version of the API specification that PyDBC implements, not the version of the PyDBC driver.

It is recommended to use the PyDBC driver included in the GOLDILOCKS client package provided with the GOLDILOCKS server. If a different PyDBC release version must be used, verify its compatibility with the target server version before use.

PyDBC libraries are provided for specific Python versions and operating system environments. Install the library that matches the following:

- Python major and minor versions
- Operating system and CPU architecture
- Bitness of Python and the GOLDILOCKS client library (32-bit or 64-bit)

<a id="2b8933dcf02a2a49"></a>
### Installing

PyDBC is provided as a Python C extension module and is installed by building the source included in the GOLDILOCKS client package. Internally, PyDBC uses the GOLDILOCKS ODBC library, gdlcs.

<a id="caef7051a0752f76"></a>
#### Supported Environments

PyDBC does not officially support the HP-UX, AIX, or macOS platforms.

PyDBC supports the following Python versions:

- Python 2.4 or later
- Python 3.4 or later

Python 2 is a deprecated version that is no longer maintained by the Python community. PyDBC supports Python 2.4 through 2.7 for compatibility with existing Python 2 applications.

Because PyDBC is a Python C extension module, the major and minor versions of the Python interpreter used to build PyDBC must match those of the Python interpreter used to run it.

<a id="bef821dc50bc570a"></a>
#### Prerequisites

Before installing PyDBC, ensure that the following requirements are met:

- The GOLDILOCKS client package is installed.
- The GOLDILOCKS_HOME environment variable is set to the GOLDILOCKS client installation directory.
- The goldilocks.h header file exists in $GOLDILOCKS_HOME/include.
- The gdlcs client library exists in $GOLDILOCKS_HOME/lib.
- A C compiler compatible with the target Python version is installed.
- The development headers for the target Python version are installed.
- Python and the GOLDILOCKS client library use the same architecture.

<a id="ee13121f7cdf246a"></a>
#### Installing on Linux

To build PyDBC on Linux, a C compiler and the development headers for the target Python version are required.

First, set the GOLDILOCKS_HOME environment variable.

```
shell> export GOLDILOCKS_HOME=/path/to/goldilocks
```

If necessary, configure the library search path so that the gdlcs shared library can be found at runtime.

```
shell> export LD_LIBRARY_PATH=$GOLDILOCKS_HOME/lib:$LD_LIBRARY_PATH
```

<a id="e0fe3d84277484f3"></a>
##### Python 2

Navigate to the Python 2 source directory and install PyDBC.

```
shell> cd $GOLDILOCKS_HOME/app_dev/pygoldilocks/ver2
shell> python setup.py install
```

If multiple versions of Python 2 are installed, specify the target Python executable when installing.

```
shell> python2.7 setup.py install
```

For Python 2.4 through 2.7, installation must be performed using a version of setuptools or distutils that is compatible with the target Python version.

<a id="f9abda95d2050263"></a>
##### Python 3

Navigate to the Python 3 source directory and install PyDBC using pip.

```
shell> cd $GOLDILOCKS_HOME/app_dev/pygoldilocks/ver3
shell> python3 -m pip install .
```

If multiple versions of Python 3 are installed, specify the target Python executable when installing.

```
shell> python3.13 -m pip install .
```

It is recommended to install PyDBC in a Python virtual environment rather than directly into the system Python installation. Installing with administrator privileges, such as by using sudo python setup.py install, is also not recommended.

<a id="6d4696507da16183"></a>
#### Installing on Windows

To build PyDBC on Windows, a Microsoft C/C++ compiler compatible with the target Python version is required. In addition, Python, the C/C++ compiler, and the GOLDILOCKS client library must use the same architecture.

The following compilers are supported for Python 2:

- Python 2.4 ~ 2.5: Microsoft Visual Studio 2003.NET
- Python 2.6 ~ 2.7: Microsoft Visual C++ 2008

For Python 3, use the Microsoft C/C++ Build Tools compatible with the target Python version.   
For more information, refer to [https://wiki.python.org/moin/WindowsCompilers](https://wiki.python.org/moin/WindowsCompilers).

Set the GOLDILOCKS_HOME environment variable from the command prompt.

```
C:\> set GOLDILOCKS_HOME=C:\goldilocks
```

<a id="c9bc040172a1f614"></a>
##### Python 2

```
C:\> cd %GOLDILOCKS_HOME%\app_dev\pygoldilocks\ver2
C:\> python setup.py install
```

<a id="40d2905e279b2bae"></a>
##### Python 3

```
C:\> cd %GOLDILOCKS_HOME%\app_dev\pygoldilocks\ver3
C:\> python -m pip install .
```

<a id="be610e948216fda7"></a>
#### Verifying the Installation

After the installation is complete, run the following command to verify that the pygoldilocks module can be loaded successfully.

```
shell> python -c "import pygoldilocks; print(pygoldilocks.version)"
26.1.0
```

If the version is displayed, PyDBC has been installed successfully in the current Python environment.

If an error indicating that the pygoldilocks module cannot be found occurs, verify that the same Python interpreter was used for both the installation and the verification.

If an error indicating that the gdlcs library cannot be found occurs, check the following:

- The GOLDILOCKS_HOME environment variable
- The installation path of the GOLDILOCKS client library
- The operating system's shared library search path
- Whether Python and the GOLDILOCKS client library use the same architecture

<a id="71b7d00168962dbe"></a>
### Examples

<a id="816309b00021eb2d"></a>
#### Obtaining Connection Class

PyDBC implicitly calls ODBC library. Therefore, [the data source](34-odbc.md#c0bc1af6b9e0ca88) should be configured to obtain the connection.

- Obtain the connection as follows.

```
import pygoldilocks
cnxn = pygoldilocks.connect( 'DSN=GOLDILOCKS;UID=test;PWD=test' )
```

Call connect which is an internal function of pygoldilocks, a module of PyDBC, to obtain the connection.

> [Data Source](34-odbc.md#c0bc1af6b9e0ca88) should be configured in advance to use DSN.

If CHARSET is not set in DSN, then ODBC library sets it to Console Character Set. PyDBC implicitly performs the basic encoding for the character set used by ODBC. If the character set used in GOLDILOCKS server is different from that in ODBC library, then the data conversion occurs and it degrades the performance. For example, CP949 is used as a basic character set in Windows. If nothing is set, PyDBC implicitly uses CP949(UHC) when encoding, and ODBC library also uses UHC when processing the character set.

The following are how to alter the character set of the client.

- Alter CHARSET property in [Data Source Configuration](34-odbc.md#c0bc1af6b9e0ca88).
- Add CHARSET property to the connection string. 
- Use attrs_before keyword in connect method of pygoldilocks module.

All of the three methods above alter the connection property of ODBC, SQL_ATTR_CHARACTER_SET, and set the encoding of PyDBC library as well.

<a id="c5a24bde5525a382"></a>
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

<a id="e30c4d91ce6f9eb5"></a>
#### EXPLAIN PLAIN Retrieval

A cursor attribute can be configured to generate an execution plan as part of SQL execution. When the execution plan feature is enabled, the execution plan for the SQL statement can be retrieved through the cursor attribute after SQL execution is complete.

As shown below, execute the SQL statement using the standard `cursor.execute()` method, and retrieve the execution plan separately through the cursor attribute function.

```
import pygoldilocks


conn = pygoldilocks.connect("DSN=GOLDILOCKS;UID=test;PWD=test;")
cur = conn.cursor()
try:
    cur.setattr( pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_OPTION,
        pygoldilocks.SQL_EXPLAIN_PLAN_ON )
<code>    cur.execute("select * from t1 where i1 = ?", 1)
    plan = cur.getattr(pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_TEXT)
    print(plan)</code>
finally:
    try:
        cur.setattr( pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_OPTION,
            pygoldilocks.SQL_EXPLAIN_PLAN_OFF )
    finally:
        cur.close()
        conn.close()
```

The SQL execution plan is displayed as follows.

```
$ python test.py

< Execution Plan >
=====================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                       ROWS |
-----------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                          1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                          1 |
|    2  |      TABLE ACCESS ("T1")                                     |                          1 |
=====================================================================================================

     1  -  TARGET : T1.I1
     2  -  READ COLUMN : T1.I1
             PHYSICAL FILTER : T1.I1 = ?
```

<a id="7b78e3d20d4a35f8"></a>
## API Reference

<a id="21b2d09e259d79b2"></a>
### pygoldilocks Module

pygoldilocks object complies with [Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/).  
For more information, refer to [Python DB API module](https://www.python.org/dev/peps/pep-0249/#module-interface).

<a id="da0b182152b8e19f"></a>
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

<a id="7203c784cb3c2ff9"></a>
#### connect

It newly connects to the database.

```
connect( [connection_str], **kwargs )
```

It inputs the ODBC connect string and keywords. The keywords are as follows.

<a id="cd0ec4a04ae701dd"></a>
| Keyword | Description | Default value |
| --- | --- | --- |
| connection_str | It is an optional positional string argument. An error occurs if more than one value is specified or if a value other than a string is specified. | - |
| autocommit | It specifies whether to auto commit. If it is false, connection.commit should be called to reflect it in the database. | False |
| readonly | If it is true, the connection is set to readonly. | False |
| timeout | It specifies the timeout value for the connection. It is set using the SQL_ATTR_LOGIN_TIMEOUT attribute. | - |
| attrs_before | It specifies attributes that must be set before establishing the connection. A value of dictionary type must be specified. | - |
| user, password | It converts the values to the GOLDILOCKS connection keywords uid and pwd, respectively. | - |
| Other keywords | It converts the value to a string and adds it to the connection string in the format of key=value;. | - |

The connect() function creates a new connection using a single GOLDILOCKS connection string, keyword arguments, or a combination of both.

The following is an example of passing connection attributes using a single string.

```
cnxn = pygoldilocks.connect("dsn=GOLDILOCKS;host=127.0.0.1;port=22581;uid=test;pwd=test" )
```

The following is an example of passing connection attributes using a combination of a string and keyword arguments.

```
cnxn = pygoldilocks.connect("dsn=GOLDILOCKS",user="test",password="test",autocommit=True)
```

The following is an example of passing connection attributes using keyword arguments.

```
cnxn = pygoldilocks.connect( dsn="GOLDILOCKS", port=22581, user="test", autocommit=True )
```

PyDBC handles autocommit, readonly, timeout, and attrs_before directly; these options are not added to the connection string.

- attrs_before
    - It specifies options to be set before establishing the connection. These options are set by using [SQLSetConnectAttr](34-odbc.md#a2ddb5cc3c0b2f7e). The attributes and values must be specified as a dictionary. For more information about the available attributes, refer to [ODBC Attributes](34-odbc.md#9593e227b0df79f0).

```
cnxn =  pygoldilocks.connect( "DSN=GOLDILOCKS", attrs_before={ pygoldilocks.SQL_ATTR_MAX_ROWS : 1000 })
```

<a id="45505b00cf2e1066"></a>
#### Date

```
>>> print pygoldilocks.Date(1984,11,23),  type(pygoldilocks.Date(1984,11,23))
1984-11-23 <type 'datetime.date'>
```

It creates a date object corresponding to the given value.

<a id="308657585c94a5d5"></a>
#### Time

```
>>> print pygoldilocks.Time(11,23,23), type(pygoldilocks.Time(11,23,23))
11:23:23 <type 'datetime.time'>
```

It creates a time object corresponding to the given value.

<a id="f37db2afadef5a09"></a>
#### Timestamp

```
>>> print pygoldilocks.Timestamp(1984,11,23,11,23,23), type(pygoldilocks.Timestamp(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

It creates a datetime.datetime object corresponding to the given value.

<a id="5f905bbc5432d8be"></a>
#### DATETIME

```
>>> print pygoldilocks.DATETIME(1984,11,23,11,23,23), type(pygoldilocks.DATETIME(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

It creates a datetime.datetime object corresponding to the given value. It is the same as [Timestamp](#f37db2afadef5a09).

<a id="01076a5378123ac8"></a>
#### Binary

```
>>> print pygoldilocks.Binary('binary'), type(pygoldilocks.Binary('binary'))
binary <type 'bytearray'>
```

It creates a bytearray object corresponding to the given value. It is the same as [BINARY](#05f8b849a3556553).

<a id="05f8b849a3556553"></a>
#### BINARY

```
>>> print pygoldilocks.BINARY('binary'), type(pygoldilocks.BINARY('binary'))
binary <type 'bytearray'>
```

It creates a bytearray object corresponding to the given value.

<a id="965e6507e2b658da"></a>
#### STRING

```
>>> print pygoldilocks.STRING('str'), type(pygoldilocks.STRING('str'))
str <type 'str'>
```

It creates an str object corresponding to the given value.

<a id="9ef0d7a2ca0f1141"></a>
#### NUMBER

```
>>> print pygoldilocks.NUMBER(100.001), type(pygoldilocks.NUMBER(100.001))
100.001 <type 'float'>
```

It creates a float object corresponding to the given value.

<a id="f2e34f69dfa27b66"></a>
#### ROWID

```
>>> print pygoldilocks.ROWID('AA'), type(pygoldilocks.ROWID('AA'))
AA <type 'str'>
```

It is used to describe the row ID column of the database, and returns an str object.

<a id="2fa58a8e7ff57146"></a>
#### TimeFromTicks

```
>>> pygoldilocks.TimeFromTicks(10)
datetime.time(9, 0, 10)
```

It returns a datetime.time object which is set as an argument value.

<a id="d42f350a28895ffe"></a>
#### DateFromTicks

```
>>> pygoldilocks.DateFromTicks(360000)
datetime.date(1970, 1, 5)
```

It returns a datetime.date object which is set as an argument value.

<a id="3a91c5b417f72876"></a>
#### TimestampFromTicks

```
>>> pygoldilocks.TimestampFromTicks(360000)
datetime.datetime(1970, 1, 5, 13, 0)
```

It returns a datetime.datetime object which is set as an argument value.

<a id="c93049d0ec572ac3"></a>
#### setDecimalSeparator

It sets the decimal point delimiter in NUMERIC type obtained from the database. The default value uses a period (.).

<a id="4890b8e2cdedda07"></a>
#### getDecimalSeparator

It obtains the set decimal point delimiter in NUMERIC type.

<a id="67ed0362f95c0824"></a>
### Connection

It is an object managing the connection with the database, and it is created with connect() function of pygoldilocks module.

<a id="e4eb5d3cc2b90a21"></a>
#### Properties

<a id="39e553fa04612b32"></a>
##### Python 2/3

- autocommit
    - It sets the autocommit mode of the connection.

- searchescape
    - It is the pattern escape character returned by ODBC's SQLGetInfo(SQL_SEARCH_PATTERN_ESCAPE).

- timeout
    - It sets the default query timeout for a new cursor. 
    - It sets the SQL_ATTR_QUERY_TIMEOUT attribute using the SQLSetConnectAttr function.

- maxwrite
    - It specifies the size in bytes used as the threshold for determining whether character and binary parameters are bound directly or sent using SQLPutData. 
    - If the value is 0, the default threshold based on the driver and data type is used. A user-defined value must be 255 or greater.
    - This value only changes the input transfer method; it does not truncate values or limit the size of fetch results.

<a id="4d74798f3f852227"></a>
##### Python 3

- closed
    - It is true if the connection handle is closed and false if it is available for use.

- messages
    - It is a list of DB-API warnings generated during connection operations. Each item is in the format (Warning, warning instance). 
    - Connection methods clear the existing list before starting a new operation, so it must be checked immediately after the operation.

<a id="638b140fd449e1c1"></a>
#### Function

<a id="73516f8e0911d876"></a>
##### Python 2/3

- cursor()
    - It returns a new cursor object.

- commit()
    - It commits the executed SQL statement.

- rollback()
    - It rolls back the executed SQL statement.

- close()
    - It closes the connection. If the autocommit is false, then the SQL statement which was not committed is rolled back.

- getinfo( info )
    - It can obtain the connection properties by using SQLGetInfo function of ODBC. For more information, refer to [SQLGetInfo](34-odbc.md#c2dcfe03f0659b13).

```
dsn_name = cnxn.getinfo( pygoldilocks.SQL_DATA_SOURCE_NAME )
```

- execute( sql, [*params] )
    - It creates a new cursor object, and executes execute function of this object, then returns a cursor object.

```
cursor = cnxn.execute( "SELECT COUNT(*) FROM EMP" )
```

For more information, refer to Cursor.execute() function. This function is not part of the Python DB-API 2.0 standard but is provided for convenience. Whenever this function is called, a cursor object is allocated, so it is not recommended to use it when it is required to execute one or more SQL statements.

- set_attr( attr_id, value )
    - The connection properties can be set by executing SQLSetConnectAttr function. 
    - The following is an example of controlling the transaction isolation level of the database by using set_attr function.

```
connection.set_attr( pygoldilocks.SQL_ATTR_TXN_ISOLATION, pygoldilocks.SQL_TXN_SERIALIZABLE )
```

- __enter__, __exit__
    - It is a special method that is automatically called by a with connection statement rather than a general method called directly by the user. When autocommit is disabled, it performs a commit on normal completion and a rollback if an exception occurs. The exception is propagated to the caller as is, and the connection remains open.

<a id="49f916be5f811408"></a>
##### Python 3

- character_set_name()
    - It returns the name of the GOLDILOCKS character set used by the current connection as a string.

<a id="95537ea85bd8c402"></a>
###### **Output Converter**

Output converters are registered per connection and are applied to all cursors created from that connection. Registering a converter for the same SQL type again replaces the existing converter. The registration state is determined when execute creates the result set, and any subsequent registry changes are applied from the next execute call.

An output converter receives raw bytes before the database character set is automatically converted to a Python string. Therefore, the codec used by the converter must match the actual character encoding used by the connection.

- get_output_converter( sqltype )
    - It returns the output converter callable registered for the specified SQL type. It returns None if no converter is registered.

- add_output_converter(sqltype, func)
    - It registers a callable that converts the result of the specified SQL type. The callable receives raw bytes or None for SQL NULL as the input value, and the returned value is used as the value of the fetched row.

- remove_output_converter(sqltype)
    - It removes the converter registered for the specified SQL type. It completes without an error even if no converter is registered.

- clear_output_converters()
    - It removes all output converters registered for the connection.

The following is an example of an SQL_VARCHAR type converter receiving raw bytes or None corresponding to SQL NULL for a UTF-8 connection.

```
def uppercase_varchar(raw_value):
    if raw_value is None:
        return None
    return raw_value.decode("utf-8").upper()

cnxn.add_output_converter(
    pygoldilocks.SQL_VARCHAR,
    uppercase_varchar,
)

try:
    registered_converter = cnxn.get_output_converter(
        pygoldilocks.SQL_VARCHAR
    )
    assert registered_converter is uppercase_varchar

    cursor.execute(
        "select cast('alpha' as varchar(20)) "
        "from fixed_table_schema.dual"
    )
    assert cursor.fetchone()[0] == "ALPHA"
finally:
    # Removing an unregistered converter does not raise an error.
    cnxn.remove_output_converter(
        pygoldilocks.SQL_VARCHAR
    )

assert (
    cnxn.get_output_converter(pygoldilocks.SQL_VARCHAR)
    is None
)

# The following removes all registered converters.
cnxn.clear_output_converters()

# The removal takes effect from the next execute() call.
cursor.execute(
    "select cast('alpha' as varchar(20)) "
    "from fixed_table_schema.dual"
)
assert cursor.fetchone()[0] == "alpha"
```

- setencoding( encoding, ctype=SQL_CHAR )
    - It sets the Python codec used to encode SQL text and string parameters into bytes. Only SQL_CHAR can be specified for ctype, and wide character types are not supported.

```
cnxn.setencoding("cp949", ctype=pygoldilocks.SQL_CHAR)
```

- setdecoding( sqltype, encoding, ctype=SQL_CHAR )
    - It sets the codec used to decode character result data into Python strings. Only SQL_CHAR can be specified for sqltype, and wide character types are not supported.

```
cnxn.setdecoding( sqltype=pygoldilocks.SQL_CHAR, encoding="cp949", ctype=pygoldilocks.SQL_CHAR )
```


> 
> - The settings configured by setencoding() and setdecoding() apply to the corresponding connection and remain in effect until the same function is called again or the connection object is destroyed. They are not automatically reset when executing SQL, committing, rolling back, or closing a cursor.
> - A reset API that restores the automatically detected codec and an API that retrieves the name of the currently configured codec are not provided. 
> - character_set_name() returns the database character set name, not the name of the Python codec configured last. 
> - SQL_VARCHAR and SQL_LONGVARCHAR are supported as SQL column/parameter types, but cannot be used as the ctype argument of setencoding() and setdecoding().
> 

<a id="dea7bcb0f7cd7cf0"></a>
### Cursor

Generally, a cursor object refers to a database cursor used to manage fetch operations. A database cursor is mapped to an ODBC statement handle (HSTMT). Each cursor created from the same connection uses a separate statement handle, and its position in the result set is managed independently. Therefore, the fetch position of one cursor does not affect other cursors.  
However, transactions are managed at the connection level. Therefore, changes made through one cursor and the result of a commit or rollback on that connection also apply to other cursors created from the same connection.

<a id="b1413e42ef5cb1cc"></a>
#### Properties

<a id="f09ff4988a1449ea"></a>
##### Python 2/3

<a id="6075c8e6ae3c14fb"></a>
###### **description**

It is the read-only property, and it includes the contents for each column which was returned by SELECT statement executed last with tuple type. Each tuple includes the following.

1. Column name (or alias)
2. Type code
3. Display size
4. Internal size
5. Precision
6. Scale
7. Nullable

When SELECT statement is not called, then the description is None.

<a id="bcec22414cb89f5a"></a>
###### **rowcount**

It is the number of rows affected by the last DML statement or executemany(). If the exact value cannot be determined or the statement is a SELECT statement, it is set to -1. If the values from multiple executions can be accurately summed, it returns the summed value.

<a id="acc08f59317786d5"></a>
###### **arraysize**

It is the number of rows which can be fetched per one time by using [fetchmany( [size = cursor.arraysize] )](#76c392a2ec8cc4bd) function. The default value 1.

<a id="a9489c2db0b22813"></a>
###### **connection**

It is the read-only property, and it indicates the connection object which created the corresponding cursor object.

<a id="418d1bd53c47f5f7"></a>
###### **fast_executemany**

If it is set to true, then makes the parameters in array and executes them at once when executing [executemany( sql, [*params] )](#acac11fb5494ad2f) function. If it is set to false, it separately executes each parameter.

<a id="84561791d0c4d1f5"></a>
###### **timeout**

It sets the query timeout of the cursor in seconds. A value of 0 indicates no timeout. It uses the connection.timeout value as the default value when created, and an independent value can be set for each cursor afterward.

<a id="2c2e84792ee64d3d"></a>
##### Python 3

<a id="5426ba8d37acd5f6"></a>
###### **closed**

It is True if the cursor itself or its parent connection is closed.

<a id="f487ab99e17ba717"></a>
###### **messages**

It is a list of cursor warnings, and each item is in the format (Warning, warning_instance).  
Performing a new non-fetch operation clears the existing list. In contrast, fetch operations retain existing items and may add warnings.

<a id="52c9e63cd071dea3"></a>
#### Function

<a id="411ce0ce7ceb43b2"></a>
##### execute( sql, [*params] )

It executes SQL statement through SQLPrepare and SQLExecute functions, then returns a cursor which called this function.   
The parameter option can be used as follows.

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", x, y )
```

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", (x, y) )
```

<a id="acac11fb5494ad2f"></a>
##### executemany( sql, [*params] )

It executes the SQL statement for each parameter and returns the cursor object that called this method. The params parameter must be a sequence of parameter sets or an iterator or generator that returns parameter sets in sequence.

```
params = [ ( 1, 'A' ), ( 2, 'B' ) ]
cursor.executemany("INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", params)
```

SQL statement is executed twice in the example above. In other words, it is separately executed for  ( 1, 'A' ) and ( 2, 'B') each. The operation of executemany depends on whether fast_executemany of a cursor object is set to true or false.

The example above is the same as follows.

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

<a id="e97e9702e8408bc7"></a>
##### fetchone()

It returns the next row of the query. If the next data does not exist, it is None.

<a id="e4cf64e2138b8fa4"></a>
##### fetchall()

It returns all rows left in the query. Be cautious when using it because it reads all rows to the memory.

<a id="ef9eb37af0207d66"></a>
##### fetchval()

It returns the value of the first column of the next row in the query result. It returns None if there is no next row.

<a id="76c392a2ec8cc4bd"></a>
##### fetchmany( [size = cursor.arraysize] )

It returns rows which were left as many as size or cursor.arraysize. The next fetch returns an empty list. The default value of cursor.arraysize is 1.

<a id="b6dd60911bbd1142"></a>
##### commit()

It commits SQL statement. It is a function executed by a connection object which created a cursor object, and it is applied to all cursor which were created in the same connection object. It is the same as commit of the connection object.

<a id="a0d0c36fc1dbf603"></a>
##### rollback()

It rolls back SQL statement. It is a function executed by a connection object which created a cursor object, and it is applied to all cursor which were created in the same connection object. It is the same as rollback of the connection object.

<a id="448f1d4819f0399b"></a>
##### skip( count )

It passes through the record through SQLFetchScroll and SQL_FETCH_NEXT as many times as it is set in count.

<a id="da9d11843d97cf52"></a>
##### nextset()

It moves to the next result set and returns true if a next result set exists. It returns None if no more result sets are available.

<a id="4a78fd63d831a4a2"></a>
##### close()

It closes a cursor object.

<a id="67235566cc7f0919"></a>
##### setinputsizes( sizes )

It specifies the type and size metadata to use for binding input parameters when executing SQL. Each item in sizes corresponds to the parameter marker (?) in the SQL statement in order. This method does not return a value.

A sequence, iterator, or generator can be passed to sizes. A passed iterator or generator is converted to a sequence only once when the method is called. The converted settings are used for subsequent executions of the same cursor until a different value is set or setinputsizes(None) is called.

The size specified by setinputsizes() is not an option for truncating or padding data to the specified length. Specifying a size smaller than the string or binary data may cause an error during binding or execution; the data is not truncated or partially stored. Specifying a size larger than the data does not modify the original data. Specifying a smaller column size for a fixed-size integer does not truncate the integer value.

The following is an example of setting the column sizes of three input parameters to 10, 100, and 1000, respectively.

```
cursor.setinputsizes((10, 100, 1000))

cursor.execute(
      "insert into sample(code, name, description) values(?, ?, ?)",
      "A01",
      "Goldilocks",
      "Database description",
  )
```

If the number of specified settings is smaller than the number of SQL parameters, the remaining parameters are detected automatically during execution. To specify only a specific position, use None for the preceding positions.

The following is an example of automatically detecting the first and third parameters and specifying only the size of the second parameter.

```
cursor.setinputsizes((None, 100, None))

cursor.execute(
    "insert into sample(id, name, amount) values(?, ?, ?)",
    1,
    "Goldilocks",
    12500,
)
```

The following is an example of removing all stored settings.

```
cursor.setinputsizes(None)
```

When settings are applied temporarily, using try/finally is recommended to ensure that they are reset regardless of whether an exception occurs.

```
try:
    cursor.setinputsizes((10, 100))
    cursor.execute(
        "insert into sample(code, name) values(?, ?)",
        "A01",
        "Goldilocks",
    )
finally:
    cursor.setinputsizes(None)
```

<a id="07a9cce0f76b60af"></a>
###### **Python 2**

In Python 2, a column size can be specified for each item in sizes using a non-negative int or long type.

<a id="452f3b961d77dc8b"></a>
###### **Python 3**

In Python 3, one of the following formats can be used for each input parameter.

- None: Keeps the automatically detected SQL type, column size, and decimal digits.
- A non-negative integer: Keeps the automatically detected SQL type and changes only the column size.
- A supported Python type object: Uses the SQL type corresponding to the specified Python type.
- (sql_type, column_size, decimal_digits): Specifies the SQL type, column size, precision, decimal digits, or scale. Specify None for items to retain the automatically detected value.

The supported Python type objects are as follows.

- str: SQL_VARCHAR
- float: SQL_DOUBLE
- bytes, bytearray: SQL_VARBINARY
- datetime.date: SQL_TYPE_DATE
- datetime.time: SQL_TYPE_TIME
- datetime.datetime: SQL_TYPE_TIMESTAMP

setinputsizes() automatically converts some Python type objects to the corresponding SQL types. Type objects of int, bool, and decimal.Decimal do not support this automatic conversion. To use these types, specify the appropriate SQL type constant as the first item in the tuple descriptor.

The following is an example of binding parameters by setting the first parameter to SQL_INTEGER and the second parameter to NUMERIC(12, 3) metadata.

```
from decimal import Decimal

cursor.setinputsizes(
    (
        # Only the SQL_INTEGER type is specified and the remaining metadata is automatically detected.
        (pygoldilocks.SQL_INTEGER, None, None),
        # The precision and scale of NUMERIC(12, 3) are specified.
        (pygoldilocks.SQL_NUMERIC, 12, 3),
    )
)

try:
    cursor.execute(
        "insert into sample(id, amount) values(?, ?)",
        1,
        Decimal("12345.678"),)
finally:
    cursor.setinputsizes(None)
```

The following is an example of using Python type objects directly.

```
from datetime import date, datetime, time

cursor.setinputsizes((str, float, bytes, bytearray, date, time, datetime))
```

The following is an example of replacing the Python type objects in the previous example with SQL type constants. Listing SQL type constants directly is interpreted as specifying column sizes and does not have the same effect.

```
cursor.setinputsizes( (
    (pygoldilocks.SQL_VARCHAR, None, None), # str
    (pygoldilocks.SQL_DOUBLE, None, None), # float
    (pygoldilocks.SQL_VARBINARY, None, None), # bytes
    (pygoldilocks.SQL_VARBINARY, None, None), # bytearray
    (pygoldilocks.SQL_TYPE_DATE, None, None),
    (pygoldilocks.SQL_TYPE_TIME, None, None),
    (pygoldilocks.SQL_TYPE_TIMESTAMP, None, None), ) )
```

<a id="af51c1f4b2772459"></a>
##### setoutputsize( size, column=None )

<a id="70a82d53b11ce9cd"></a>
###### **Python 2**

It stores the setting in the cursor and applies it to the LONG variable OUT parameter buffer size for callproc(). column is the 1-based index of the OUT parameter. Specify None to clear the stored global or index-specific setting. This API is not intended to limit the fetch size of a normal SELECT statement.

```
try:
    # Sets the buffer size of the second LONG VARCHAR OUT parameter for callproc()
    cursor.setoutputsize(4096, 2)
    values = cursor.callproc("PROC_WITH_LONG_OUT", ("", ""))
finally:
    cursor.setoutputsize(None)
```

<a id="6e387844632f400e"></a>
###### **Python 3**

It is a DB-API compatibility no-op that validates the arguments but does not affect the output size or data values.

<a id="cdd9203be3cb6ebb"></a>
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

<a id="e870a8ba1016aca9"></a>
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

result = cursor.callfunc( 'FUNC1', ( 1,  4) )
```

<a id="dbe0e792d9573bb2"></a>
##### tables( table=None, catalog=None, schema=None, tableType=None )

It returns the table information of the database which satisfies the given condition. The character  '_' and '%' are translated as a wild card. Each row has the following column information. For more information, refer to [SQLTables](34-odbc.md#2cf8935e0f8b9592).

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

<a id="3792ac1d710b318c"></a>
##### columns( table=None, catalog=None, schema=None, column=None )

It returns metadata for columns that match the specified conditions using the [SQLColumns](34-odbc.md#5b9b1c9408d2bb3a) function. Each row contains the following column information.

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

<a id="801c7a698cdf45b0"></a>
##### procedureColumns( procedure=None, catalog=None, schema=None )

It obtains metadata for the procedure return value, result columns, and IN, OUT, and INOUT parameters using the [SQLProcedureColumns](34-odbc.md#c915e2c5e3d2e0ca) function.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. column_name
5. column_type
6. data_type
7. type_name
8. column_size
9. buffer_length
10. decimal_digits
11. num_prec_radix
12. nullable
13. remarks
14. column_def
15. sql_data_type
16. sql_datetime_sub
17. char_octet_length
18. ordinal_position
19. is_nullable

<a id="adf6c976ca2b9bf7"></a>
##### statistics( table, catalog=None, schema=None, unique=False, quick=True )

It obtains the information about the specified table through [SQLStatistics](34-odbc.md#a42e1bfe518c9b4c) function.  
If unique is true, it returns an unique index, and if it is false, it returns all indexes.  
If quick is true, CARDINALITY and PAGES are returned only when it is instantly available, otherwise, NULL is returned to the corresponding column.

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

<a id="95355e54b8d03a56"></a>
##### rowIdColumns( table, catalog=None, schema=None, nullable=True )

It returns the result set of columns which uniquely identifies a row by executing [SQLSpecialColumns](34-odbc.md#3c60153be4224bf6) with SQL_BEST_ROWID. Each row includes the following column information.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, or SQL_SCOPE_SESSION
2. column_name
3. data_type: SQL type constant of ODBC
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO or SQL_PC_PSEUDO

<a id="3690cb50ee3781f7"></a>
##### rowVerColumns( table, catalog=None, schema=None, nullable=True )

It returns the result set of columns which are automatically updated when a row is updated by executing [SQLSpecialColumns](34-odbc.md#3c60153be4224bf6) with SQL_ROWVER. Each row includes the following column information.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, or SQL_SCOPE_SESSION
2. column_name
3. data_type: SQL type constant of ODBC
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO, or SQL_PC_PSEUDO

<a id="41cebce27fdf6787"></a>
##### primaryKeys( table, catalog=None, schema=None )

It returns the result set of columns which configures major keys of a table by executing [SQLPrimaryKeys](34-odbc.md#5c3f0cca4017b7ac) function. Each row includes the following column information.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. key_seq
6. pk_name

<a id="c0a150a5fc2ec5d3"></a>
##### foreignKeys( table=None, catalog=None, schema=None, foreignTable=None, foreignCatalog=None, foreignSchema=None )

It creates the result set of column names of a specified table, or the result set of column names which are foreign keys of another table referring to the basic key of the specified table, by executing [SQLForeignKeys](34-odbc.md#ae36d1b78e59cf29) function. Each row includes the following column information.

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

<a id="e5186771202e24a2"></a>
##### procedures( procedure=None, catalog=None, schema=None )

It creates the result set of the information about the procedure by executing [SQLProcedures](34-odbc.md#0f681141eecc3ecf). Each row includes the following column information.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. num_input_params
5. num_output_params
6. num_result_sets
7. remarks
8. procedure_type

<a id="d93b90c38d30c223"></a>
##### getTypeInfo( sqlType=None )

It creates the result set of the information about the specified data type or about all data types which are supported by GOLDILOCKS ODBC, by executing [SQLGetTypeInfo](34-odbc.md#776d96ea02e7ea6d) function. Each row includes the following column information.

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

<a id="45cf3a88f7ab1c3f"></a>
##### getattr( attr )

Executes the [SQLGetStmtAttr](34-odbc.md#f080b6285d3f422e) function and returns the specified statement attribute information. The return value type depends on the statement attribute.

<a id="9fcd451beaad05c9"></a>
##### setattr( attr, attr_value )

Executes the [SQLSetStmtAttr](34-odbc.md#36bfe523796f6177) function and sets attr_value for the specified statement attribute.

<a id="d46d313b823b173d"></a>
##### cancel()

It requests cancellation of the statement currently being executed by the cursor.

cancel() only requests cancellation. The actual cancellation result may be reported as an exception depending on the diagnostic information returned by the CLI. After cancellation, whether the cursor can be reused must be determined by the application after completing exception handling.

```
import threading

def cancel_running_statement():
    cursor.cancel()

timer = threading.Timer(1.0, cancel_running_statement)
timer.start()
try:
    cursor.execute("CALL DBMS_LOCK.SLEEP(10)")
finally:
    timer.cancel()
```

<a id="4949e0983be7e1b5"></a>
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

<a id="0a85e774c7243207"></a>
#### Properties

- cursor_description

It is the copy of property description of a cursor object which created the corresponding row. For more information, refer to [Cursor.description](#b1413e42ef5cb1cc).

<a id="4a77c08e2afc1255"></a>
## Exception

Python exceptions occur by pygoldilocks when GOLDILOCKS ODBC detects an error. The exception classes are as follows, which are the same as [Python DB API](https://www.python.org/dev/peps/pep-0249/#exceptions).

```
Exception
├── Warning
└── Error
    ├── InterfaceError
    └── DatabaseError
        ├── DataError
        ├── OperationalError
        ├── IntegrityError
        ├── InternalError
        ├── ProgrammingError
        └── NotSupportedError
```

If an error occurs, generally, the exception is processed based on SQLSTATE value provided by the database.

<a id="945d259c94333d07"></a>
| SQLSTATE | Exception |
| --- | --- |
| 01002 | OperationalError |
| 08001, 08003, 08004, 08007, 08S01 | OperationalError |
| 0A000 | NotSupportedError |
| 28000 | InterfaceError |
| 40002 | IntegrityError |
| 22*** | DataError |
| 23*** | IntegrityError |
| 24***, 25***, 42*** | ProgrammingError |
| HY001, HY014, HYT00, HYT01 | OperationalError |
| IM001, IM002, IM003 | InterfaceError |

<a id="a28ec86b7db41e41"></a>
## Data Type

<a id="b2cb2394afb1fa54"></a>
### Transferring Python Parameter to GOLDILOCKS

The data is converted as follows when transferring Python parameter to GOLDILOCKS ODBC.

**Python 3**

<a id="77aad275ac4fc58e"></a>
| Python datatype | Description | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | The encoding to use as the writing codec for the connection | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytes, bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | boolean | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.time | time with time zone | SQL_TYPE_TIME_WITH_TIMEZONE |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| datetime.datetime | timestamp with time zone | SQL_TYPE_TIMESTAMP_WITH_TIMEZONE |
| int | integer | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

**Python 2**

<a id="6138b00303408288"></a>
| Python datatype | Description | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | byte string | SQL_VARCHAR or SQL_LONGVARCHAR |
| unicode | Converted to the connection's character encoding | SQL_VARCHAR or SQL_LONGVARCHAR |
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

<a id="59b8351c5459858c"></a>
### SQL Value Received from GOLDILOCKS

The data is converted as follows when transferring the data of GOLDILOCKS database to Python.

**Python 3**

<a id="8b42ebe3114e223a"></a>
| ODBC datatype | Description | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | str |
| SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | int |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.datetime |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | datetime.time |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | datetime.datetime |
| SQL_C_INTERVAL_*** | interval | str |
| SQL_ROWID | rowid | str |

**Python 2**

<a id="72a2be5a4469664f"></a>
| ODBC datatype | Description | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytearray |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.datetime |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |
| SQL_ROWID | rowid | text |

The text of Python data type is converted to unicode in Python 3. It is converted to the unicode or a string according to the character set of the database in Python 2.

**Python 2 text**

<a id="97a55cab531793ce"></a>
| DB character set | Python type |
| --- | --- |
| UTF-8 | str |
| SQL_ASCII | str |
| UHC | unicode |
| GB18030 | unicode |

---

[← 37. PDO](37-pdo.md) · [Table of contents](../README.md) · [39. aiogoldilocks →](39-aiogoldilocks.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
