<a id="20b6970d176ab8e0"></a>

# 42. tablediff

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/20b6970d176ab8e0)  
> Tag: `22c.1_10_tag`

[← 41. gdump](41-gdump.md) · [Table of contents](../README.md) · [43. gsyncher →](43-gsyncher.md)

<a id="9e4bbbe73f12a365"></a>
## Overview of tablediff

<a id="65fe77b8465db94d"></a>
### Background

The GOLDILOCKS system operator should prepare for the unexpected failure of GOLDILOCKS synchronization of two tables using the tools such as cyclone or LogMirror. An unexpected failure of synchronization refers that a particular row exists only in one table or the column values of rows to be synchronized are different from each other. Cyclone and LogMirror do not notify a user whether synchronization is failed. It is required to verify the synchronization of the table and to perform synchronization, if necessary, at non-operation time.

<a id="483d822db7e5ab17"></a>
### Features

tablediff is a tool comparing two tables of GOLDILOCKS which was synchronized by using CDC in a row unit. It reports when a particular row exists only in a table or values are different each other, then performs synchronization. The configuration file for controlling various operations is input, and the log files to report the unsynchronized rows and the synchronization results are output.

The constraints are that the schemas of two tables should be same and each of them should have the primary key. It is not recommended to perform the tool for table of the currently executing transaction because the table can be updated in real time. However, it does not matter for the currently executing querying (SELECT statement). This tool is available only for the GOLDILOCKS tables.

This tool has two executing commands, which are TableDiff and TableSync.

<a id="7543d3eefcd2703f"></a>
#### TableDiff

```
java sunje.goldilocks.tool.diff.TableDiff [configure file]
```

TableDiff program verifies whether two tables are unsynchronized, and it may output the information(binary file) to perform synchronization for unsynchronized rows immediately or at a later time according to an option. The immediate synchronization can be operated for multiple threads.

<a id="71453ba4a65f1fe8"></a>
#### TableSync

```
java sunje.goldilocks.tool.diff.TableSync [configure file]
```

Tablesync program performs synchronization by using the sync information which was previously left by TableDiff. (Row comparison is not performed.) A simultaneous execution can be performed by driving multi threads.

> Unsynchronized rows of two tables to which the configure file is not applied are stored in a bin file left by TableDiff. TableSync uses this bin file to forcibly synchronize two tables.

<a id="81ce88f4bb2c1522"></a>
### Characteristics

This tool is a java application and it is provided in a jar file form, so Java(1.6) is required to execute the tool. Also, goldilocks6.jar is required because GOLDILOCKS JDBC driver is used. It can be remotely performed because it is connected to GOLDILOCKS by using TCP/ IP, and it is performed at much faster rate than using JDBC, ODBC with the proprietary protocol.

The row comparison and synchronization can be simultaneously performed with multi threads. For multithreading of the row comparison, equal dividing of the range of the key in the table should be manually performed. When the user splits the key range into ten ranges (The user can specify it in the configuration file), then ten threads compare the tables. On the other hand, the synchronization operation is performed by threads of as many as it is specified.

<a id="0ba6587b9b1805d9"></a>
### File Configuration

tablediff program consists of a single file called as $GOLDILOCKS_HOME/bin/tablediff.jar. $GOLDILOCKS_HOME/lib/goldilocks6.jar file is also required for execution. Also, the configuration file is required as an input argument, and refer to the sample file, $GOLDILOCKS_HOME/conf/tablediff.conf.

<a id="d7a2edd752c3082d"></a>
## Usage

<a id="27d85e0612d3497b"></a>
### Command Usage

Java (JRE 1.6 or JDK1.6) is required because tablediff is a java program. For this, tablediff.jar and goldilocks6.jar files should be included in CLASSPATH, or they should be specified with -classpath option of java. tablediff is executed as follows.

```
export CLASSPATH=$CLASSPATH:$GOLDILOCKS_HOME/bin/tablediff.jar:$GOLDILOCKS_HOME/lib/goldilocks6.jar
java sunje.goldilocks.tool.diff.TableDiff [configure file]
```

Or

```
java -classpath $GOLDILOCKS_HOME/bin/tablediff.jar:$GOLDILOCKS_HOME/lib/goldilocks6.jar sunje.goldilocks.tool.diff.TableDiff [configure file]
```

The result of executing TableDiff for the simple sample table is as follows.

```
gSQL> create table tab1 ( c1 integer primary key, c2 char(10) );
gSQL> create table tab2 ( c1 integer primary key, c2 char(10) );
gSQL> insert into tab1 values ( 1, 'HELLO');
gSQL> insert into tab2 values ( 1, 'HELLO');
gSQL> insert into tab1 values ( 2, 'WORLD');
gSQL> insert into tab2 values ( 2, 'world');
gSQL> insert into tab1 values ( 3, 'good');
gSQL> insert into tab2 values ( 4, 'good');
gSQL> commit;


shell> java sunje.goldilocks.tool.diff.TableDiff tablediff.conf
Total 4 rows processed
  > row diff            : 1, update target(success/failure): 1/0
  > key diff source only: 1, insert into target(success/failure): 1/0
  > key diff target only: 1, delete from target(success/failure): 1/0
TableDiff completed
elapsed time = 0.229 sec
```

- The contents of tablediff.conf

```
SOURCE_URL      = jdbc:goldilocks://127.0.0.1:22581/test
SOURCE_USER     = TEST
SOURCE_PASSWORD = test
SOURCE_SCHEMA   = PUBLIC
SOURCE_TABLE    = TAB1

TARGET_URL      = jdbc:goldilocks://127.0.0.1:22581/test
TARGET_USER     = TEST
TARGET_PASSWORD = test
TARGET_SCHEMA   = PUBLIC
TARGET_TABLE    = TAB2

OPERATION       = SYNC
TARGET_INSERT = ON
TARGET_UPDATE = ON
TARGET_DELETE = ON
SOURCE_INSERT = OFF
```

<a id="3e756c7f0734d655"></a>
### Property Option

This chapter describes the available property options in the configuration file of tablediff.

<a id="8ae4623f76e77e7b"></a>
#### Property Options for SOURCE, TARGET Tables

These property options should necessarily be specified and they define the source and target tables. The source and target refer to table to be compared each.

- SOURCE_URL: It is JDBC connection URL of GOLDILOCKS in which the source table exists.
- SOURCE_USER: It is the user account of GOLDILOCKS in which the source table exists.
- SOURCE_PASSWORD: It is the password of GOLDILOCKS in which the source table exists.
- SOURCE_SCHEMA: It is the schema of source table. 
- SOURCE_TABLE: It is the name of source table.
- TARGET_URL: It is JDBC connection URL of GOLDILOCKS in which the target table exists.
- TARGET_USER: It is the user account of GOLDILOCKS in which the target table exists.
- TARGET_PASSWORD: It is the password of GOLDILOCKS in which the target table exists.
- TARGET_SCHEMA: It is the schema of target table.
- TARGET_TABLE: It is the name of target table.

The following is an example.

```
SOURCE_URL      = jdbc:goldilocks://192.168.0.100:22581/test
SOURCE_USER     = TEST
SOURCE_PASSWORD = test
SOURCE_SCHEMA   = PUBLIC
SOURCE_TABLE    = T1

TARGET_URL      = jdbc:goldilocks://192.168.0.101:22581/test
TARGET_USER     = TEST
TARGET_PASSWORD = test
TARGET_SCHEMA   = PUBLIC
TARGET_TABLE    = T2
```

<a id="af524968b5dac882"></a>
#### Operation

It determines the operations of TableDiff. The DIFF property verifies only the synchronization integrity and reports it, but the SYNC property verifies the integrity and simultaneously performs synchronization.

The integrity result file (whose file name is specified as DIFF_BIN_ FILE property) is generated when operating with DIFF and it is used to execute TableSync.

<a id="5806645bb5ba16a3"></a>
#### Synchronization Policy

Four properties are used for controlling the synchronization policy and all of them have the value of either ON or OFF.

- TARGET_INSERT: If the key in the source does not exist in the target, it inserts the key into the target.
- TARGET_UPDATE: If the value of the column which is not a key is different, it updates the target row. 
- TARGET_DELETE: If the key does not exist in the source but exists in the target, it deletes the target row. 
- SOURCE_INSERT: If the key does not exist in the source but exists in the target, it inserts that row into the source.

> Both TARGET_DELETE and SOURCE_INSERT are not allowed to be ON together.

<a id="405aa50d7e522e93"></a>
#### EXCLUDED_COLUMNS

It specifies the columns to be excluded from the comparison. The comma (,) is used as a delimiter and the column name should be specified. The key columns can not be excluded.

<a id="b219410f358ffb15"></a>
#### WHERE_CLAUSE

It sets the conditions for comparing rows in the table. For example, the condition, WHERE_CLAUSE = SALARY> = 1000000, refers that the integrity is verified only for the rows having the values of their column salary equal to or bigger than 1,000,000.

<a id="11db20bbae42356e"></a>
#### DISPLAY_ROW_UNIT

TableDiff program displays the progress status of table comparison, and it outputs to the console the number of rows processed each time whenever it processes a certain number of rows. The property sets the number of rows to be output. the default value is 100,000, and it can be omitted.

<a id="4e99b4309a88f702"></a>
#### SYNC_OUT_FILE

It specifies the name of the file in which the synchronization result is to be recorded. If not specified, the result is recorded in tablesync.log. If multiple synchronized threads exist, a number is added at the end of the file name.

<a id="e99e7cfb608c96aa"></a>
#### DIFF_OUT_FILE

It specifies the name of the file in which the row mismatch result is to be recorded. If not specified, the result is recorded in tablesync.log. This file is in a text form which is human-readable.

<a id="b09a8d43397c6932"></a>
#### DIFF_BIN_FILE

If the operation property is set to DIFF, TableDiff records the synchronization information in a file with a name specified by this property. This file is used as an input argument by TableSync.

<a id="432a72cb4d8af9b0"></a>
#### PROPAGATE_REDO_LOG

It determines whether to propagate the row synchronization log to another replicated server. The default value is OFF.

<a id="14e5b20ffe282767"></a>
#### LOGGING_ON_SUCCESS

It sets whether to record logs even when DML(INSERT, UPDATE, DELETE) used for the row synchronization is successful. The default value is OFF. If it is OFF, then the synchronization performance becomes poor. If DML is failed, the logging information is recorded regardless of this property.

<a id="08048e2332188cea"></a>
#### LOGGING_ON_DIFF

It sets whether to record logs when the mismatch occurs during comparing the row integrity. The default value is OFF.

<a id="a4134234c629a3f3"></a>
#### JOB_QUEUE_SIZE

The row synchronization is performed by the operating thread. The threads perform the synchronization by getting the operation from the JOB QUEUE one by one. The main thread of TableDiff or TableSync inserts the operation to JOB QUEUE. JOB QUEUE becomes full if the thread slowly performs synchronization.   
JOB_QUEUE_SIZE property sets the size of JOB QUEUE. If this value is big, JOB QUEUE never becomes full but it wastes a lot of memory. The default value is 100, and 100 is big enough to use without filling of the queue.  
The property is recommended not to change unless it is needed.

<a id="498e2aef92338a9b"></a>
#### JOB_THREAD

It sets the number of threads for synchronization. If not set, the default value is 1. If there are multiple rows to be synchronized, the value should be set considering the number of CPU. The bigger the value, the faster the synchronization is performed.

<a id="f9281ae212c405c5"></a>
#### JOB_UNIT_SIZE

The synchronization is performed in batch as much as the size specified by the property. The default value is 100.

<a id="d8628648ed7645c8"></a>
#### DISPLAY_CALL_STACK

It sets whether to display call stack when an error occurs. The default value is OFF.

<a id="ca7e1a985a7b3eef"></a>
#### Replication Settings for Table Comparison

The row comparison of TableDiff is performed by a single thread by default. But multiple threads can perform comparisons by specifying the condition clause. The property name is PARTITION_RANGE[n], and if the range for N properties is set such as the WHERE clause, n threads perform the comparison each.

For example, the following properties are specified for each of 12 threads to perform the comparison when the table includes the monthly data.

```
PARTITION_RANGE1 = MONTH=1
PARTITION_RANGE2 = MONTH=2
PARTITION_RANGE3 = MONTH=3
PARTITION_RANGE4 = MONTH=4
PARTITION_RANGE5 = MONTH=5
PARTITION_RANGE6 = MONTH=6
PARTITION_RANGE7 = MONTH=7
PARTITION_RANGE8 = MONTH=8
PARTITION_RANGE9 = MONTH=9
PARTITION_RANGE10 = MONTH=10
PARTITION_RANGE11 = MONTH=11
PARTITION_RANGE12 = MONTH=12
```

All conditions should be disjointed, and the union of all conditions should be as same as the total set. Also, the column used in the condition should the front part of the primary key. (It means that the specified condition should be able to use the primary index.)  
This property is applied only to TableDiff, and TableSync ignores this property.

---

[← 41. gdump](41-gdump.md) · [Table of contents](../README.md) · [43. gsyncher →](43-gsyncher.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
