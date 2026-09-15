<a id="0a41649a645e0dbf"></a>

# 5. Basic Management of GOLDILOCKS Database

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/0a41649a645e0dbf)  
> Tag: `21c.1_35_tag`

[← 4. What's New](../part-01-getting-started/4-what-s-new.md) · [Table of contents](../README.md) · [6. Structure and Storage Structure of GOLDILOCKS Database →](6-structure-and-storage-structure-of-goldilocks-database.md)

<a id="c77b6bc6410a915e"></a>
## Creating and Configuring GOLDILOCKS Database

<a id="44076ce0b8a1ccd7"></a>
### Creating Database

Create database using gcreatedb which is included in GOLDILOCKS package. Before creating database, the followings should be considered.

**Considerations when creating database**

<a id="4b1386a9554f30a8"></a>
<table><thead><tr><th align="center" valign="middle">Considerations</th><th align="center" valign="middle">For more information, refer to</th></tr></thead><tbody><tr><td valign="middle">Consider the space size of tables and indexes to be used in database.</td><td><ul><li><a href="6-structure-and-storage-structure-of-goldilocks-database.md#501186da0fdd0a54">Structure and Storage Structure of GOLDILOCKS Database</a></li></ul></td></tr><tr><td valign="middle">Consider the location to create database files. It is because the database performance will be improved by properly distributing the files and dispersing the disk IO. For example, a user can allocate redo log file to a separate disk or stripe it, and then disperse data file into a number of disks, to execute a parallel disk IO operation.</td><td align="left" valign="middle"><ul><li><a href="6-structure-and-storage-structure-of-goldilocks-database.md#df42badd98d33e64">Managing Redo Log File</a></li></ul></td></tr><tr><td valign="middle">Be aware of each property's concepts and its operation which are set in server property file, then constantly manage them.</td><td valign="middle"><ul><li><a href="#5f32ccd2bddca241">Specifying Initial Property</a></li><li><a href="#c5c699ae15e3466e">Managing Initial Property Using GOLDILOCKS Configuration File</a></li><li><a href="10-server-property.md#5d474603dd66e8e7">Server Property</a></li></ul></td></tr></tbody></table>

In addition to the above considerations, refer to [Creating Database](../part-01-getting-started/2-tutorial.md#251bcd234a0219bd) in [Getting Started](../part-01-getting-started/1-preface.md#12bf538e54e9cbc7) for more options to be considered when creating database.

A user should set environment variables to use GOLDILOCKS, and the variables are $GOLDILOCKS_HOME and $GOLDILOCKS_DATA. The property file, *goldilock.properties.conf*, for creating and managing GOLDILOCKS database is in *$GOLDILOCKS_DATA/conf*.

- GOLDILOCKS_HOME: Binaries which are included in GOLDILOCKS package are installed here, and it can be overwritten during software version upgrading (The license backup is required.)
- GOLDILOCKS_DATA: Log file, data file, control file which are used by GOLDILOCKS database are installed here, and it can not be overwritten.

<a id="5f32ccd2bddca241"></a>
### Specifying Initial Property

A user can use properties to control the information for operation and management in GOLDILOCKS.

<a id="a8df4247235be170"></a>
#### Initial Property

Set the properties of when creating or starting the database as follows.

1. Setting system environment variable
    1. Change it by typing in the command window in which GOLDILOCKS is installed and database is created or operated.
    2. It is necessary to add the prefix before the property name, and the prefix is *GOLDILOCKS_*.

- The following is an example of changing SHARED_MEMORY_STATIC_SIZE to 100M.

```
export GOLDILOCKS_SHARED_MEMORY_STATIC_SIZE=100M
```

2. Property file: The prefix is not required, so change it directly in the property file.

- The following is an example of changing SHARED_MEMORY_STATIC_SIZE to 200M.
- Shared memory static size (100 M ~ 32 G)

```
SHARED_MEMORY_STATIC_SIZE = 200M
```

> If the same property is set to system environment variable and property file, then the value of the property file will be applied. For example, if SHARED_MEMORY_STATIC_SIZE is set to 100 M as the system environment variable, and SHARED_MEMORY_STATIC_SIZE is set to 200 M as the property file, then SHARED_MEMORY_STATIC_SIZE will be applied to 200 M when operating database.

<a id="c5c699ae15e3466e"></a>
### Managing Initial Property Using GOLDILOCKS Configuration File

Property file is in *$GOLDILOCKS_DATA/conf*, and is divided into two according to the file format.

- Text property file 
    - File name: goldilocks.properties.conf
    - It is "property name = value" format file, and a user can directly edit it. 
    - If a binary property file exists, it does not read text property file.

- Binary property file 
    - It is created by the system, and a user can not edit it directly.
    - File name: goldilocks.properties.binary
    - Use gdump tool to retrieve the binary file's contents.

> If a text property file and a binary property file exist together, it reads the binary property file only. The text property file is not processed. This binary property file is managed by user SQL (ALTER SYSTEM SET), and can be edited using SQL only.   
>   
> For information, refer to [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#8524798b9d7f6a03), [ALTER SYSTEM RESET property_name](../part-03-sql-manual/18-sql-references-a-b.md#8c8b1bcebb15cd54).

- Editing text property file
    - Use "PROPERTY_NAME = VALUE" format.
    - Use '#' for annotation.
    - Property has one of the following three data types.
        - Character data type: Use a single quote (') to set the character value. Use *&lt;GOLDILOCKS_DATA&gt;* if the character value includes $GOLDILOCKS_DATA link.
        - Numeric data type: Do not use calculation for numeric data. For example, LOG_BUFFER_SIZE=1024 * 1024 is not allowed to use. Its size is selectable accordingly such as K (kilobyte), M (megabyte), G (gigabyte), T (terabyte), and P (petabyte)
        - Boolean data type: Allowed to use ON/OFF, ENABLE/DISABLE, 1/0 and TRUE/FALSE, YES/NO.

<a id="f4cc9e00c2eb1ce9"></a>
## Starting up and Shutting down GOLDILOCKS Instance

This chapter describes starting up and shutting down of GOLDILOCKS instance.

<a id="4dff841c56142b8e"></a>
### Starting up Instance

GOLDILOCKS instance can be started only by a user with SYSDBA privilege.   
GOLDILOCKS instance can be started by using Direct Attach (D/A) method and dedicated method of Client/Server (C/S). However, it can not be started by using shared method of C/S.

<a id="9b804f5fb2033c1a"></a>
#### Multi-level Startup

GOLDILOCKS has multi-level startup procedure. Multi-level startup procedure enables to change the database's state by the intervention of administrator in each phase.

The phases are idle, nomount, mount, open, and each phase has the following features.

<a id="64963fc094796fce"></a>
##### Idle Phase

The idle phase is a state in which an instance is not started up.

If connecting to gsql when an instance is not started, then it will be connected to idle instance as follows. In this phase, any sever command can not be executed except for `\`startup.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> select * from dual;

ERR-08003(40044): connection does not exist 

gSQL>
```

- Administrator operations in idle phase
    - Adjusting the property required to start up the instance 
    - Transition to nomount using `\startup` in gsql

- Operation in an instance at the nomount transition
    - Starting up gmaster which is a daemon managing GOLDILOCKS instance
    - Starting up timer thread and cleanup thread in gmaster
    - Allocating and initializing Shared memory Static Area (SSA).

**Applied properties at the transition to nomount**

<a id="aaa9715bdd03a460"></a>
| Property name | Description |
| --- | --- |
| CLIENT_MAX_COUNT | Maximum number of connectable sessions |
| CONTROL_FILE_0 ~ 7 | Path of control file |
| CONTROL_FILE_COUNT | The number of valid path among the path of control file |
| DATA_STORE_MODE | Store mode of GOLDILOCKS instance |
| PLAN_CACHE_SIZE | Maximum size of shared memory for plan cache |
| PROCESS_MAX_COUNT | Maximum number of connectable process |
| SHARED_MEMORY_ADDRESS | Address of shared memory |
| SHARED_MEMORY_STATIC_NAME | Name of shared memory |
| SHARED_MEMORY_STATIC_KEY | Key value for creating shared memory |
| SHARED_MEMORY_STATIC_SIZE | Size of shared memory to be created |
| SYSTEM_LOGGER_DIR | Path of system logger |

Properties can not be changed in idle phase. An administrator changes the properties as follows.

To use an environment variable, then set GOLDILOCKS_[property_name] to a desired value and transit it to nomount. Then, the properties will be applied.

```
% export GOLDILOCKS_CLIENT_MAX_COUNT=1000
```

To use 'SCOPE = FILE', record the property value to be changed in the file. The recorded property will be applied at nomount transition.

```
gSQL> alter system set client_max_count = 1000 scope = file;

System altered.

gSQL> \shutdown 

Shutdown success

gSQL> \startup    

Startup success

gSQL>
```

<a id="9c4e90f278784d61"></a>
##### Nomount Phase

The nomount phase is a state in which it is not mounted to database, and only the gmaster process has been started. A gmaster is a daemon which manages GOLDILOCKS instance.

The following describes how to transit idle phase to nomount phase.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup nomount

Startup success

gSQL>
```

- Administrator operations in nomount phase
    - Adjusting nomount property
    - For more information, refer to [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#54011886eee6d8dd), [ALTER DATABASE RESTORE](../part-03-sql-manual/18-sql-references-a-b.md#85fee9c048422d86).

- Operation in an instance at the mount transition
    - Loading the control file to database
    - Preparing for database recovery
    - Starting up threads in gmaster such as checkpoint, log flusher, page flusher, IO slave, archive log

**Updatable properties in nomount phase**

<a id="50139cfd92155524"></a>
| Property name | Description |
| --- | --- |
| DATABASE_ACCESS_MODE | Database access mode (READ ONLY, READ WRITE) |
| LOG_BUFFER_SIZE | Redo log buffer size |
| PARALLEL_LOAD_FACTOR | The number of threads for parallel operations after loading database |
| PARALLEL_IO_FACTOR | The number of parallel threads for loading database |
| PARALLEL_IO_GROUP_1 ~ 16 | Datafile group at parallel loading |
| PENDING_LOG_BUFFER_COUNT | The number of delayed log buffers |
| TRANSACTION_TABLE_SIZE | Transaction table size |
| UNDO_RELATION_COUNT | The number of undo relations |

<a id="ab3cfd018c4dc704"></a>
##### Mount Phase

The mount phase is a state in which it is mounted to database, and the database recognizes the control file. All sections in the control file is controllable in this phase.

The following describes how to transit nomount phase to mount phase.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup nomount

Startup success

gSQL> alter system mount database;

System altered.

gSQL>
```

- Administrator operations in mount phase
    - Adjusting mount properties
    - [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#54011886eee6d8dd)
    - [ALTER DATABASE ADD LOGFILE](../part-03-sql-manual/18-sql-references-a-b.md#e61d8380d28bd181)
    - [ALTER DATABASE DROP LOGFILE](../part-03-sql-manual/18-sql-references-a-b.md#8d6a8c5cd906742d)
    - [ALTER DATABASE RENAME LOGFILE](../part-03-sql-manual/18-sql-references-a-b.md#ea9453261d58be3a)
    - [ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }](../part-03-sql-manual/18-sql-references-a-b.md#ba215547bc1143dc)
    - [ALTER DATABASE DELETE BACKUP](../part-03-sql-manual/18-sql-references-a-b.md#e90cdf82964500a1)
    - [ALTER DATABASE REGISTER](../part-03-sql-manual/18-sql-references-a-b.md#f1c48ce65f4ddd31)
    - [ALTER DATABASE RECOVER](../part-03-sql-manual/18-sql-references-a-b.md#3fa18e0049bd27dd)
    - [ALTER DATABASE RESTORE](../part-03-sql-manual/18-sql-references-a-b.md#85fee9c048422d86)
    - [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#9478b0e9e0d1d5e2)
    - [ALTER SYSTEM RESET property_name](../part-03-sql-manual/18-sql-references-a-b.md#8c8b1bcebb15cd54)
    - [ALTER SYSTEM SWITCH LOGFILE](../part-03-sql-manual/18-sql-references-a-b.md#cad24f3df58ddc03)
    - [ALTER SYSTEM [KILL | DISCONNECT] SESSION](../part-03-sql-manual/18-sql-references-a-b.md#38e96a269836e35e)
    - [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](../part-03-sql-manual/18-sql-references-a-b.md#e6c60d7941ea0eca)
    - [ALTER TABLESPACE name RENAME DATAFILE](../part-03-sql-manual/18-sql-references-a-b.md#c37c6f99c21bcc51)
    - [ALTER TABLESPACE name [ONLINE|OFFLINE]](../part-03-sql-manual/18-sql-references-a-b.md#03c54bf99c431d45)

- Operation in an instance at the open transition
    - Loading all data file used in an instance to shared memory
    - Performing instance recovery
    - Creating NOLOGGING index
    - Deleting objects or files which are not deleted by ager thread
    - Creating cache for dictionary objects
    - If "SHARED_SESSION" property is set to *YES*, process monitor thread in gmaster will be started up.
    - Process monitor thread executes balancer process, dispatcher process, shared-server process.

**Updatable property in mount**

<a id="6282b4087d83a11f"></a>
| Property name | Description |
| --- | --- |
| ARCHIVELOG_FILE | Prefix name of archive file |
| IN_DOUBT_DECISION | Decision about in-doubt transaction |
| LOCK_HASH_TABLE_SIZE | Hash table size of lock administrator |
| LOG_MIRROR_MODE | Log mirroring mode |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | Shared memory size for log mirroring |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | Whether to perform supplemental logging at the database-level |

<a id="c7951eb876f57660"></a>
##### Open Phase

The open phase is a state in which all the data file is loaded to memory, and it is ready for service. All operations are allowed in this phase.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup mount

Startup success

gSQL> alter system open database;

System altered.

gSQL>
```

The database access mode is selectable at the transition to open phase. The database access modes are divided into READ_ONLY mode and READ_WRITE mode. The READ_ONLY mode can only read data in database, but READ_WRITE mode can both read and write the data.

To open database in READ_ONLY mode, the previous database should be normally shut down. If the access mode is omitted, it refers to the DATABASE_ACCESS_MODE property value when opening database.

```
gSQL> \shutdown abort

Shutdown success

gSQL> \startup mount

Startup success

gSQL> alter system open database read only;

ERR-42000(14038): unable to recover database in READ ONLY mode

gSQL> alter system open database read write;

System altered.

...

gSQL> \shutdown normal

Shutdown success

gSQL> \startup mount

Startup success

gSQL> alter system open database read only;

System altered.
```

<a id="0abb5ccd51604597"></a>
#### Diagnosis

It is possible to execute several phases at a same time using a single command(`\startup`) when starting up instance. If a certain phase fails, the administrator should figure out in which phase the failure occurs. Check using to which phase the instance has come using V$INSTANCE. Then the administrator can continue operations of startup instance from the subsequent phase.

The following is an example of starting up instance to open phase after `\`startup failure.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

ERR-42000(14051): media recovery required - 'TEST_TBS'

gSQL> select INSTANCE_STATUS from v$instance;

INSTANCE_STATUS
---------------
MOUNTED           

1 row selected.

...

gSQL> alter system open database;

System altered.
```

<a id="cab772fc27e93807"></a>
### Shutting down Instance

GOLDILOCKS instance can be terminated only by a user with SYSDBA privilege. It is not allowed to create new session during shutdown.

GOLDILOCKS instance can be shut down by Direct Attach (D/A) method and dedicated method of Client/Server (C/S), but it can not be shut down by shared method of C/S.

There are four types of instance shutdown mode, and they are shutdown normal, shutdown transactional, shutdown immediate and shutdown abort.

<a id="7d359347be08c460"></a>
#### Shutdown Normal

The shutdown normal is set by default if a particular mode is not specified when shutting down. Use this type if a user wants to shut down an instance normally.

```
gSQL> \shutdown normal

Shutdown success

gSQL>
```

The followings describe the characteristics of shutdown normal.

- New session is not allowed.
- New transactions and statements are allowed in session which already have been connected. 
- Waiting for all the sessions which are connected to the instance to be shut down.
- It does not execute instance recovery process when starting up the instance.

<a id="2f6e000a6d5b613f"></a>
#### Shutdown Transactional

Use this type to shut down the currently proceeding transactions normally even when the session is forcibly shut down.

```
gSQL> \shutdown transactional

Shutdown success

gSQL>
```

The followings describe the characteristics of shutdown transactional.

- Neither new session nor is new transaction allowed.
- New statements are allowed in ongoing transaction.
- Waiting for the ongoing transactions to be shut down.
- The session will be automatically terminated after the ongoing transactions is terminated.
- It does not execute instance recovery process when starting up the instance.

<a id="50d0f69d1fdd54ea"></a>
#### Shutdown Immediate

Use this type to terminate the instance when a user can not terminate current transactions.

```
gSQL> \shutdown immediate

Shutdown success

gSQL>
```

The followings describe the characteristics of shutdown immediate.

- Neither new session nor is new transaction allowed.
- Forcibly shut down ongoing sessions and transactions.
- Waiting until the background thread of the system to be completed.
- It does not execute instance recovery process when starting up the instance.

<a id="30512ee9c395c8ba"></a>
#### Shutdown Abort

Use this type when a user judged the instance is in an abnormal state.

```
gSQL> \shutdown abort

Shutdown success

gSQL>
```

The followings describe the characteristics of shutdown abort.

- Neither new session nor is new transaction allowed.
- Forcibly shut down ongoing sessions and transactions.
- Instantly shut down the background thread of the system.
- It executes instance recovery process when starting up the instance.

<a id="6d42c7fbee0a65ca"></a>
## Managing Process

This chapter describes the background processes of GOLDILOCKS instance.

<a id="9a682e8e416dfbfe"></a>
### Master Process

Master process performs the asynchronous operation for database performance and monitoring. It consists of many threads.

The master process' executable file name is gmaster.

<a id="23093fa48b8533e7"></a>
#### Checkpoint Thread

Checkpoint thread executes asynchronous checkpoint events which occur in the log flushing thread. The checkpoint event occurs whenever redo log file is switched.

Checkpoint event is executed asynchronously regardless of a user, and its log is recorded in system.trc as follows.

```
[2014-09-11 14:04:34.704465 THREAD(14497,140178383427328)] [INFORMATION]
[CHECKPOINT] begin

...

[2014-09-11 14:04:34.743933 THREAD(14497,140178383427328)] [INFORMATION]
[CHECKPOINT] save control file

[2014-09-11 14:04:34.759521 THREAD(14497,140178383427328)] [INFORMATION]
[CHECKPOINT] end
```

<a id="99f365e5ffa7deb6"></a>
#### Log Flushing Thread

User transactions record redo log in log buffer, and it is periodically recorded in log file by log flushing thread.

Log switching occurs when redo log is recorded to the end of the log file, then it will be recorded in the next redo log file. When the log switching occurs, checkpoint event is transferred to a checkpoint thread.

If reusable log file does not exist when the log file is switched, all queries except for the read-only queries will wait until the reusable log file is created.

The message remains as follows in system.trc when logging is blocked.

```
...

[2014-09-11 14:31:44.315871 THREAD(19102,139674683647744)] [INFORMATION]
[LOG FLUSHER] disable logging - blocked lfsn(1)

...
```

<a id="6a23973a3d6447b5"></a>
#### Log Archiving Thread

The log archiving thread asynchronously archives redo log file. This thread is executed only when database is operated in ARCHIVELOG mode.

Log archiving is a part of checkpoint process, and it is executed by log archiving event in which the checkpoint thread occurred.

The message remains as follows in system.trc when redo_0_0.log is archived to archive_0.log.

```
[2014-09-11 14:13:32.515996 THREAD(16913,140631135463168)] [INFORMATION]
[ARCHIVELOG BEGIN] LOG(/home/test/work/product/Gliese/home/wal/redo_0_0.log(0)) => ARCHIVE(/home/test/work/product/Gliese/home/archive_log/archive_0.log)

[2014-09-11 14:13:33.145850 THREAD(16913,140631135463168)] [INFORMATION]
[ARCHIVELOG END] (/home/test/work/product/Gliese/home/archive_log/archive_0.log) : SUCCESS

...
```

<a id="518121b8423cdceb"></a>
#### Ager Thread

Ager thread physically drops the logically dropped database objects.

DROP TABLE statement executes only logical drop operation to maintain statement level consistency in GOLDILOCKS. Therefore, the statement which was invoked before DROP TABLE can explore the records of dropped table even when DROP TABLE is executed.

The message remains as follows in system.trc when table and tablespaces are physically dropped.

```
[2014-09-11 14:13:37.966788 THREAD(16925,139892990408448)] [INFORMATION]
[AGER] aging table - object scn(4561), object view scn(4562), type(0), physical id(25043954302976)

...

[2014-09-11 14:13:37.966917 THREAD(16925,139892990408448)] [INFORMATION]
[AGER] aging tablespace - object scn(4561), object view scn(4564), tablespace id(61)
```

<a id="b9c0d7cbf484e0b7"></a>
#### Timer Thread

Timer thread asynchronously sets time to the system to reduce the time measuring cost of user transactions, and the user transactions read the time set in the system.  
The time precision is set according to [TIMER_INTERVAL](10-server-property.md#e3fb26d21297b93a), and the default value is 10 ms.

The followings describe the case of using the time set in the timer thread. The time error occurs as much as TIMER_INTERVAL value. For example, if TIMER_INTERVAL is 10 ms, then the time error is also 10 ms.

- Time out: QUERY_TIMEOUT, IDLE_TIMEOUT, DDL_LOCK_TIMEOUT, ...
- Message record time written in trace log
- Startup time of login statement or transaction
- Time recorded in transaction commit redo log

<a id="0a660d122f366b6d"></a>
#### Page Flusher & IO Slave Threads

It applies the updated data pages to the disk when a checkpoint occurs. The updated information is stored in multiple data files in a tablespace. For that, the page flusher thread distributes operations to IO slave threads per each tablespace and data files and manages them. Then the IO slave threads record the updated pages in the data file in parallel.

If tables and index pages stored in the disk tablespace are updated by caching them to the buffer, they are linked to the checkpoint list, and the pages updated for the reuse in the buffer cache are linked to the buffer replace list. I/O slave threads reflect the pages in IO checkpoint list and the pages in the buffer replace list on the disk at the checkpoint or regularly.

Storing the updated pages as many as possible at a time improves performance. The number of written pages at each time follow the properties in [MAXIMUM_FLUSH_PAGE_COUNT](10-server-property.md#9ffb198d8cb15d1c).

After the updated pages are written to the data file, the message remains in system.trc is as follows.

```
[2014-09-11 14:13:38.329162 THREAD(16925,139893221086976)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 0, datafile : 0 )

[2014-09-11 14:13:38.552161 THREAD(16925,139893221086976)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 1, datafile : 0 )

[2014-09-11 14:13:38.587510 THREAD(16925,139893221086976)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 2, datafile : 0 )

[2014-09-11 14:13:38.587831 THREAD(16925,139893221086976)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 62, datafile : 0 )

[2014-09-11 14:13:38.620239 THREAD(16925,139893221086976)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 63, datafile : 0 )
```

<a id="5481e64188420d2f"></a>
#### Cleanup Thread

Cleanup thread cleans up the system resource asynchronously, and performs the following operations.

- It cleans up normally terminated session. GOLDILOCKS processes termination of a user session logically, and uses cleanup thread for physical termination of a session. 
- It cleans up abnormally terminated session. If the session is using transactions, then they will be rolled back.
- It checks the time-out of snapshot statements. If a session exceeds the time-out, it is forced to be terminated.

When cleaning up the abnormally terminated session, a message remains in system.trc as follows.

```
[2014-09-12 10:34:38.387349 THREAD(23003,140722556352256)] [WARNING]
[CLEANUP] cleaning session - env(19), session(20), transaction(FFFFFFFFFFFFFFFF), program(gsql), pid(23209), thread(140080441665280)

[2014-09-12 10:34:38.387515 THREAD(23003,140722556352256)] [WARNING]
[CLEANUP] cleaning up 1 sessions
```

If a snapshot statement exceeds the time-out, a message remains in system.trc as follows.

```
[2014-09-12 10:49:21.842179 THREAD(3972,139706316711680)] [WARNING]
[CLEANUP] long statement timeout - pid(8029), thread(140053960505088), program(gsql), statement start time(2014-09-12 10:48:49.963471)
```

If abnormally terminated session is terminated by 'kill-9' signal during changing shared memory when exclusive latch is acquired, it is no longer possible to operate the database. In this situation, a message remains in system.trc as follows, and the instance should be terminated using *SHUTDOWN ABORT*.

```
[2014-09-12 11:12:58.809249 THREAD(15313,140671386121984)] [WARNING]
[CLEANUP] failed to cleaning session - server restart required
...... dead session in critical section - env(3), session(4), transaction(47001E0004), pid(15296), thread(140178075756288)
```

<a id="69c8d73dbfbb9a89"></a>
#### Process Monitor Thread

The process monitor thread executes processes, and monitors them.

- It is executed only when "SHARED_SESSION" property is set to *YES*.
- It executes load-balancer (gbalancer), dispatcher(gdispatcher), shared-server(gserver), and re-executes them when they are abnormally terminated.
- It does not monitor listener (glsnr) process.

<a id="cc7c81fae9d10aec"></a>
#### Cluster Recover Thread

When starting up a node on a cluster system environment, if the node phases up to the mount phase, then the cluster recover thread is created. If there is an in-doubt transaction, the cluster recover thread communicates with the cluster recover thread on the remote node, and recovers the in-doubt transaction.

If there is an in-doubt transaction, the cluster recover thread communicates with the cluster recover thread on the remote node, and figures out the status of the in-doubt transaction. If the remote node is restarted and it is not recovered yet, then it transfers a message requesting the preferential completion of recovery and recovers the in-doubt transaction status after the recovery is completed.

The in-doubt transaction statuses figured out through the remote node are NONE, PREPARE, COMMIT, and ROLLBACK. If the cluster recover thread received the response such as COMMIT, ROLLBACK from at least one remote node, then it performs COMMIT or ROLLBACK. If the cluster recover thread received the response such as NONE, PREPARE from all remote nodes, then it performs ROLLBACK because COMMIT or ROLLBACK never has been performed on any cluster node.

The in-doubt transaction recovery using the cluster recover thread leaves the following messages in system.trc.

```
[2018-11-22 16:52:00.466805 INSTANCE(G3N2) THREAD(7828,140557371479808)] [WARNING]
[CLUSTER RECOVER] begin recovery

[2018-11-22 16:52:00.467221 INSTANCE(G3N2) THREAD(7828,140557371479808)] [WARNING]
[CLUSTER RECOVER] commit in-doubt transaction - commit scn(999.0.439), global transaction id(1.29294650), local transaction id(4)

[2018-11-22 16:52:00.468253 INSTANCE(G3N2) THREAD(7828,140557371479808)] [WARNING]
[CLUSTER RECOVER] rollback in-doubt transaction - commit scn(1000.439), global transaction id(4.34406459), local transaction id(59)

[2018-11-22 16:52:00.469198 INSTANCE(G3N2) THREAD(7828,140557371479808)] [WARNING]
[CLUSTER RECOVER] commit in-doubt transaction - commit scn(1001.0.439), global transaction id(5.35127356), local transaction id(60)
```

<a id="57a7c9c31a33d527"></a>
#### Failover Thread

When starting up a node on a cluster system environment, if the node phases up to the LOCAL OPEN phase, then the cluster failover thread is created. Cluster failover thread performs the failover for the error node by reselecting a coordinator or offlining when an error occurs on a specific node or the network in the cluster system.

In a situation requiring the failover, a normal node which acquired a failover lock among other normal nodes communicates with failover threads of other nodes, then performs the failover.

The failover performed by the failover thread leaves the following messages in system.trc.

```
[2018-11-22 15:27:34.619208 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION]
[FAILOVER] begin - failover member(5)

[2018-11-22 15:27:34.619418 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION]
[FAILOVER] acquire failover lock - driver(0), target(5), driver seq(1)

[2018-11-22 15:27:34.619692 INSTANCE(G1N1) THREAD(20183,140317097449216)] [INFORMATION]
[CDISPATCHER-S2] disconnect member - target member(5)

[2018-11-22 15:27:34.619893 INSTANCE(G1N1) THREAD(20183,140317097449216)] [INFORMATION]
[CDISPATCHER-S2] finalize sender socket - member(5)

[2018-11-22 15:27:34.621860 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION]
[FAILOVER] acquire failover lock

...

[2018-11-22 15:27:38.726436 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION][FAILOVER] member(5) has failovered

[2018-11-22 15:27:38.728624 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION]
[FAILOVER] release failover lock - driver(-1), target(5), driver seq(1)

[2018-11-22 15:27:38.728786 INSTANCE(G1N1) THREAD(20140,140219957368576)] [WARNING]
reset remote session map - member(5)

[2018-11-22 15:27:38.729679 INSTANCE(G1N1) THREAD(20140,140219957368576)] [INFORMATION]
[FAILOVER] finished
```

<a id="1d5edbc357ac6a20"></a>
#### Buffer Checkpoint Flusher, Buffer Replace Flusher

The table and index pages stored in disk table spaces are cached in a buffer and linked to a checkpoint list as changes are made. The buffer checkpoint flusher reflects pages linked to the checkpoint list to the corresponding data file. The buffer checkpoint flusher is performed when a checkpoint event occurs, or is periodically performed after sleeping for the period set in the [BUFFER_FLUSHING_INTERVAL](10-server-property.md#8184f2dfdfb9d6be) property. The number of buffer checkpoint flushers is determined by [BUFFER_CHECKPOINT_LIST_COUNT](10-server-property.md#24c97c83343d7d0b) property.

If the requested page does not exist in the buffer cache, then it fills the buffer cache by reading pages from the data file. When looking for the available space in the buffer caches, then it links the updated pages which are not currently used to the buffer replace list. Then, the buffer replace flusher reflects the pages linked to the buffer replace list to the corresponding data file. The buffer replace flusher wakes up by the event when an available space does not exist because the buffer is full, or is periodically performed after sleeping for the period set in the [BUFFER_FLUSHING_INTERVAL](10-server-property.md#8184f2dfdfb9d6be) property. The number of buffer replace flushers is determined by [BUFFER_FLUSH_THREADS](10-server-property.md#d044842eeb9da9d5) property.

<a id="c7609cab5b762e33"></a>
### Listener Process

Listener process enables remote access through the network in a client/server environment. Listener process waits for a client connection using [LISTEN_PORT](../part-06-utility-manual/38-glsnr.md#d59ec8937579bc6b). If connected in dedicated mode, new gserver starts, and connects a client. If connected in shared mode, it selects underloaded dispatcher (gdispatcher) using load-balancer (gbalancer), and connects a client.

gserver is a kind of operation server, and it executes a client request.

If LISTEN_PORT is already in use, the following error occurs.

```
% glsnr --start

ERR-HY000(11077): given address is already in use
```

Listener process operates independently from the instance. In other words, listener process can start up and shut down regardless of instance start up anytime.

<a id="f4a7ba4e43b3cf2b"></a>
## Managing Memory

<a id="5e02926687602146"></a>
### GOLDILOCKS Memory Architecture

GOLDILOCKS uses SSA which is a memory shared by all sessions in the system, a shared memory for database pages, and PSA (heap memory) which each session uses independently.

<a id="8cbb3b68083dd18c"></a>
![Shared memory](../assets/images/077303dea8fc6b6e.png)

<a id="e817f2288347d8dd"></a>
### Managing SSA

Shared Static Area (SSA) is a memory area to store information which is shared by the system's all sessions.

A new process should use the same physical address for using SSA. It is because the position of all information referenced by SSA uses the physical address.

The physical starting address of SSA is determined by [SHARED_MEMORY_STATIC_KEY](10-server-property.md#8c758b0eb012e6c8) and [SESSION_FATAL_BEHAVIOR](10-server-property.md#abff02de68596df4). The following error occurs when another program is already using shared memory key assigned by the same SHARED_MEMORY_STATIC_KEY, and the memory assigned by SHARED_MEMORY_ADDRESS.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

ERR-HY000(11029): shared memory segment exists 

gSQL>
```

SSA stores main information, and they are log buffer, dictionary cache, plan cache, session pool, lock pool, and transaction pool.

SSA size is determined by [SHARED_MEMORY_STATIC_SIZE](10-server-property.md#21a645ba81300a01). The system automatically manages memories used in session/lock/transaction pool and dictionary cache, and a user can not arbitrarily manage them. However, a user can arbitrarily manage the usage of log buffer and plan cache.

If the default value of log buffer and plan cache are increased, SHARED_MEMORY_STATIC_SIZE should be increased accordingly. Otherwise, the following error occurs.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

ERR-HY000(13010): Insufficient static area

gSQL>
```

<a id="91a31a8059b10150"></a>
### Managing PSA

Private Static Area (PSA) is a heap memory area, and it is used independently by each session. [PRIVATE_STATIC_AREA_SIZE](10-server-property.md#697022ef0dc019e2) determines the maximum size of PSA.

An initial size is allocated to PSA when a session is created. If additional memory is required in the session, PSA can be allocated up to its maximum size. The following error occurs when it exceeds the maximum size.

```
ERR-HY000(13011): Unable to extend memory: [MAX: 104857600, TOTAL: 102764408, ALLOC: 2097240] DESC: private static area
```

<a id="f3c9d1890dc8b780"></a>
## Monitoring

Database monitoring is needed not only to detect and prevent the problem which can be an issue in the future, but also to find a way to improve database management. For monitoring, GOLDILOCKS database provides text file type trace log and several performance views.

<a id="6021029967c1a402"></a>
### Monitoring with Trace File

From when the instance starts up until it terminates, GOLDILOCKS database provides the system log which records the overall system error, warning, information. In addition, it provides XA transaction log, trace log such as DDL log, and SQL Trace Log. For more information, refer to [SQL Trace Log](../part-03-sql-manual/15-sql-tuning.md#2e4e615384b6c596).

<a id="a7d058302c31f58b"></a>
#### Managing Trace Log File

GOLDILOCKS database's trace log file consists of system.trc file and xa.trc file. The system.trc file records system log and DDL log, and xa.trc file records XA transaction log. Trace log file is created in directory set in SYSTEM_LOGGER_DIR property. Therefore, it is generally created in trc directory below the directory specified in GOLDILOCKS_DATA environment variable. The trace log file's size is 10 Mbytes. If its space is insufficient, the existing trace log file with unique file extension is preserved, and the new trace log file is created.

Listener trace log file is created as *listener.trc* in trc directory below the directory specified by GOLDILOCKS_DATA environment variable. The log file size is 10 Mbytes. If the space is insufficient, the existing log file with unique file extension is preserved, and the new trace log file is created.

Except for system log, XA transaction log and DDL log can ON/OFF the monitoring. Set the TRACE_DDL property value to 0 to turn off the DDL log, or set it to 1 to turn on the DDL log. XA log is set in the same way using the TRACE_XA property.

<a id="cf95ed29a5a10e3d"></a>
#### System Log

The errors, warnings, and information which occurred in database instance from when master process starts up until it terminates are recorded in the system log.

<a id="a2cd21ba8c9a8d2a"></a>
##### System Log Format

System log is recorded in the following format.

```
['log record data and time' THREAD('process Id', 'thread handle')] ['log level']
['log prefix'] 'log body'
```

- 'log record date and time' is the date and time of the recorded log.
- THREAD('process Id', 'thread handle') is the information of log process id and thread handle.
- 'log prefix' is the entity or feature which created the log, and 'log body' is the detailed information.
- 'Log level' is the level of log recorded in system log, and its value is FATAL, ABORT, WARNING, INFO. 'log level' has the properties as follows.

**Log level properties**

<a id="2bd7da621b794304"></a>
| Log level | Description | Processing |
| --- | --- | --- |
| FATAL | The state which master or client process is shut down abnormally. | The client should be reconnected in case of client process FATAL, and the database instance should be shut down and restarted in case of system FATAL.  Backup the data file, control file, redo log file, system log file and contact the manufacturer. |
| ABORT | The state to continue service after rollback. | It is the normal state for system operation. Execute it again after eliminating the rollback cause. |
| WARNING | Operational warnings | The abnormal state of database instance. there is no operational problem but cause analysis is needed. |
| INFO | Operational information | - |

For example, the following system log recorded the operational information at 17:30:55 on September 11 in 2014 by process id 21395 (The thread handle is 139982731163392). Log prefix is 'STARTUP-SM' and was executing the storage manager when the master process of GOLDILOCKS database started up. It means that the transition to NO-MOUNT phase had been done during multilevel startup.

```
[2014-09-11 17:30:55.758164 THREAD(21395,139982731163392)] [INFORMATION]
[STARTUP-SM] NO-MOUNT PHASE
```

<a id="a5fa55353f2df0d6"></a>
##### Operational Information of GOLDILOCKS Database

It is the log for creating database instance, multilevel startup and shutdown, loading data file, recovering restart and media. It records the necessary information for the operation of the master process from when master process starts up until it terminates.

- GOLDILOCKS instance creation log

The system log records the following information when database instance is created. It creates the control file after the transition to NO-MOUNT phase to create database.

```
=================================================
 Startup GOLDILOCKS
 TIME    : 2014-09-03 14:43:17.321020
=================================================


[2014-09-03 14:43:17.321134 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] NO-MOUNT PHASE

[2014-09-03 14:43:17.321658 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] DATA_STORE_MODE(2)

[2014-09-03 14:43:17.335809 THREAD(14979,140542517491456)] [INFORMATION]
.... copy control file from '/goldilocks_data/wal/control_0.ctl' to '/goldilocks_data/wal/control_1.ctl'
```

Then, it moves to transition to OPEN phase, and creates the system tablespace.

```
[2014-09-03 14:43:17.401356 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] MOUNT PHASE

[2014-09-03 14:43:19.319769 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] PRE-OPEN PHASE

[2014-09-03 14:43:19.320494 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] RECOVER TABLESPACE AND DATAFILE STATE

[2014-09-03 14:43:19.326269 THREAD(14979,140542517491456)] [INFORMATION]
[STARTUP-SM] OPEN PHASE

[2014-09-03 14:43:21.005536 THREAD(14979,140542517491456)] [INFORMATION]
[TABLESPACE] Create Tablespace(0)

[2014-09-03 14:43:21.005593 THREAD(14979,140542517491456)] [INFORMATION]
[TABLESPACE] Create Tablespace(1)

...
```

After creating the system tablespace, it executes checkpoint, and terminates the database instance.

```
[2014-09-03 14:43:21.788129 THREAD(14979,140542517491456)] [INFORMATION]
[CHECKPOINT] begin - checkpoint lid(0,10128,13), checkpoint lsn(10512), oldest lsn(10512)

[2014-09-03 14:43:21.788188 THREAD(14979,140542517491456)] [INFORMATION]
[CHECKPOINT] body - checkpoint lid(-1,0,0), checkpoint lsn(-1), active transaction count(0)

[2014-09-03 14:43:21.788203 THREAD(14979,140542517491456)] [INFORMATION]
[CHECKPOINT] end - checkpoint lid(0,10128,77), checkpoint lsn(10513)

[2014-09-03 14:43:21.788214 THREAD(14979,140542517491456)] [INFORMATION]
[CHECKPOINT] flush redo log

[2014-09-03 14:43:21.949589 THREAD(14979,140542517491456)] [INFORMATION]
[CHECKPOINT] save control file

[2014-09-03 14:43:21.957563 THREAD(14979,140542517491456)] [INFORMATION]
[SHUTDOWN-SM] CLOSE

[2014-09-03 14:43:21.957595 THREAD(14979,140542517491456)] [INFORMATION]
[SHUTDOWN-SM] POST CLOSE

[2014-09-03 14:43:21.992521 THREAD(14979,140542517491456)] [INFORMATION]
[SHUTDOWN-SM] DISMOUNT

[2014-09-03 14:43:21.992557 THREAD(14979,140542517491456)] [INFORMATION]
[SHUTDOWN-SM] INIT
```

- GOLDILOCKS instance startup log

Master process records logs such as multilevel startup of database instance, loading data file, restart recovery, media recovery. After the transition to MOUNT phase, the data file is loaded.

```
=================================================
 Startup GOLDILOCKS
 TIME    : 2014-09-03 14:43:22.162601
=================================================


[2014-09-03 14:43:22.162765 THREAD(14982,140025756808960)] [INFORMATION]
[STARTUP-SM] NO-MOUNT PHASE

[2014-09-03 14:43:22.163389 THREAD(14982,140025756808960)] [INFORMATION]
[STARTUP-SM] DATA_STORE_MODE(2)

[2014-09-03 14:43:22.429311 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] MOUNT PHASE

[2014-09-03 14:43:22.559395 THREAD(14983,140025756808960)] [INFORMATION]
[EVENT] system startup : SUCCESS

[2014-09-03 14:43:22.568526 THREAD(14981,139649517561600)] [INFORMATION]
[STARTUP] MOUNT PHASE

[2014-09-03 14:43:22.571200 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] LOAD DATAFILES

[2014-09-03 14:43:22.571241 THREAD(14983,140025756808960)] [INFORMATION]
.... datafile '/goldilocks_data/db/system_dict.dbf' assigned to PARALLEL_IO_GROUP_1

...

[2014-09-03 14:43:22.571562 THREAD(14983,140025280841472)] [INFORMATION]
.... LOAD DATAFILE(/goldilocks_data/db/system_dict.dbf)

...
```

After loading data file to the memory, it executes the recovery.

```
[2014-09-03 14:43:23.537256 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] REFINE TABLESPACE AND DATAFILE

[2014-09-03 14:43:23.631974 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART REDO] begin

[2014-09-03 14:43:23.634374 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART REOD] read checkpoint log - checkpoint log id(0,10128,13), oldest lsn(10512), system scn(7)

[2014-09-03 14:43:23.756293 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART REDO] ready to redo - start lid(0,10128,13), lsn(10512)

...

[2014-09-03 14:43:24.090755 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART REDO] end - restart lsn(10514), restart scn(7)

[2014-09-03 14:43:24.091551 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART UNDO] begin

[2014-09-03 14:43:24.091598 THREAD(14983,140025756808960)] [INFORMATION]
[RESTART UNDO] end
```

After recovery, it executes checkpoint, reflects the recovery result to disk data file. Then, it creates index, moves to the transition to OPEN phase.

```
[2014-09-03 14:43:24.111878 THREAD(14983,140025633163008)] [INFORMATION]
[CHECKPOINT] begin

...

[2014-09-03 14:43:24.129995 THREAD(14983,140025633163008)] [INFORMATION]
[CHECKPOINT] save control file

[2014-09-03 14:43:24.135864 THREAD(14983,140025633163008)] [INFORMATION]
[CHECKPOINT] end

[2014-09-03 14:43:24.144525 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] PRE-OPEN PHASE

[2014-09-03 14:43:24.202782 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] RECOVER TABLESPACE AND DATAFILE STATE

[2014-09-03 14:43:24.210158 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] REFINE RELATIONS

[2014-09-03 14:43:24.210304 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] REBUILD INDEXES

[2014-09-03 14:43:24.210375 THREAD(14983,140025756808960)] [INFORMATION]
[STARTUP-SM] OPEN PHASE

[2014-09-03 14:43:24.332064 THREAD(14983,140025756808960)] [INFORMATION]
[EVENT] system startup : SUCCESS

[2014-09-03 14:43:24.340843 THREAD(14981,139649517561600)] [INFORMATION]
[STARTUP] OPEN PHASE
```

- GOLDILOCKS instance termination log

When it shuts down database instance, it reflects all data file to the disk, executes checkpoint, then terminates the master process.

```
[2014-09-03 14:48:03.467293 THREAD(15416,139855812097792)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 0, datafile : 0 )

...

[2014-09-03 14:48:03.748958 THREAD(15416,139855908558592)] [INFORMATION]
[PAGE FLUSHER] flushed lsn(137496), flushed page count(9216)]

[2014-09-03 14:48:03.761055 THREAD(15416,139856376227584)] [INFORMATION]
[CHECKPOINT] begin

...

[2014-09-03 14:48:03.780011 THREAD(15416,139856376227584)] [INFORMATION]
[CHECKPOINT] save control file

[2014-09-03 14:48:03.786387 THREAD(15416,139856376227584)] [INFORMATION]
[CHECKPOINT] end

[2014-09-03 14:48:03.791251 THREAD(15416,139856430274304)] [INFORMATION]
[SHUTDOWN-SM] CLOSE

[2014-09-03 14:48:03.791383 THREAD(15416,139856430274304)] [INFORMATION]
[SHUTDOWN-SM] POST CLOSE

[2014-09-03 14:48:03.824445 THREAD(15416,139856430274304)] [INFORMATION]
[SHUTDOWN-SM] DISMOUNT

[2014-09-03 14:48:03.824518 THREAD(15416,139856430274304)] [INFORMATION]
[EVENT] system shutdown : SUCCESS

[2014-09-03 14:48:04.267130 THREAD(15416,139856430274304)] [INFORMATION]
[SHUTDOWN-SM] INIT
```

If `\shutdown` `abort` forcibly stopped the server, neither checkpoint, nor is normal server shutdown executed.

```
[2014-09-03 14:51:45.353154 THREAD(8989,139949509089024)] [INFORMATION]
[SHUTDOWN] skip CLOSE phase

[2014-09-03 14:51:45.678461 THREAD(8989,139949509089024)] [INFORMATION]
[SHUTDOWN] skip DISMOUNT phase

[2014-09-03 14:51:45.678696 THREAD(8989,139949509089024)] [INFORMATION]
[EVENT] system shutdown : SUCCESS

[2014-09-03 14:51:45.678928 THREAD(8989,139949509089024)] [INFORMATION]
[SHUTDOWN-SM] INIT
```

- The logs of master process checkpoint, log flusher, log archiving, ager, parallel IO, cleanup thread during database operation

A checkpoint reflects to disk all data files which are updated only in memory and not written to the disk yet at checkpoint time. If it uses the parallel IO, it executes parallel IO in data file units. One unit of checkpoint log is from '[CHECKPOINT] begin' to '[CHECKPOINT] end'.

[IO SLAVE] is a log which is recorded by IO thread dedicated to parallel IO. '[IO SLAVE] flush data file (tablespace: 0, datafile: 0)' log is recorded after the data file (whose datafile id is '0' and whose tablespace id is 0) is reflected to the disk. These data file flush logs are repeatedly recorded as many as the number of data file at checkpoint time.

'[PAGE FLUSHER] flushed lsn(139039), flushed page count(9216)]' means that the reflected minimum Lsn in the disk is 139039, and reflected pages are 9216. The last log Lsn archives redo log files which are smaller than 139039. They record checkpoint log and control file, then stores them in the disk.

If a database is large its checkpoint time will be longer. Check if the datafile is continuously being recorded by tracking [IO SLAVE] logs. And if disk IO does not operate and stops, then check if log archiving is in progress. If the space is insufficient , then spare the space and ensure the log archiving proceed normally.

If checkpoint fails '[CHECKPOINT] CHECKPOINT was failed' log will be recorded. The checkpoint can be specially omitted at checkpoint time due to the log file switch, where '[CHECKPOINT] CHECKPOINT was skipped' log might be recorded.

```
[2014-09-12 15:54:59.654427 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] begin

[2014-09-12 15:54:59.654798 THREAD(13780,140493029623552)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 0, datafile : 0 )

[2014-09-12 15:54:59.835173 THREAD(13780,140493029623552)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 1, datafile : 0 )

[2014-09-12 15:54:59.893991 THREAD(13780,140493029623552)] [INFORMATION]
[IO SLAVE] flush datafile ( tablespace : 2, datafile : 0 )

[2014-09-12 15:54:59.926753 THREAD(13780,140493050603264)] [INFORMATION]
[PAGE FLUSHER] flushed lsn(138895), flushed page count(9216)]

[2014-09-12 15:54:59.926989 THREAD(13780,140492777965312)] [INFORMATION]
[ARCHIVING] stable lsn(139039)

[2014-09-12 15:54:59.933780 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] begin - checkpoint lid(0,55527,13), checkpoint lsn(139040), oldest lsn(139040)

[2014-09-12 15:54:59.933825 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] body - checkpoint lid(0,55527,77), checkpoint lsn(139041), active transaction count(1)

[2014-09-12 15:54:59.933844 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] end - checkpoint lid(0,55527,155), checkpoint lsn(139042)

[2014-09-12 15:54:59.933859 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] flush redo log

[2014-09-12 15:54:59.936154 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] save control file

[2014-09-12 15:54:59.942850 THREAD(13780,140493515450112)] [INFORMATION]
[CHECKPOINT] end
```

Log flusher records the system log when the log buffer stops flushing to disk, and when it restarts the stopped flusher. If the next log group is not reusable log file, the logging stops until it becomes reusable. The following describes an example when the logging is stopped because the redo log file of which sequence number is 34 has not been archived.

```
[2014-09-12 16:01:57.514303 THREAD(13780,140573333325568)] [INFORMATION]
[LOG FLUSHER] disable logging - blocked lfsn(34)
```

If the logging stops, then the transaction stops, so an immediate action is needed. When checkpoint is executed and archiving is done, the logging will restarts.

```
[2014-09-12 16:01:58.079236 THREAD(13780,140380267869952)] [INFORMATION]
[ARCHIVING] enable logging - blocked lfsn(34), inactivated lfsn(34)
```

Log archiving thread archives the redo log file of ACTIVE state, and it records the system log. One unit is from '[ARCHIVING] stable lsn(...)' to '[ARCHIVING] inactivate group ...'. If database is operated in archive log mode, the redo file archiving log(from'[ARCHIVELOG BEGIN] ...' to '[ARCHIVELOG END] ...') is recorded.

```
[2014-09-02 17:41:56.762950 THREAD(20800,140129584793344)] [INFORMATION]
[ARCHIVING] stable lsn(144143)

[2014-09-02 17:41:56.763549 THREAD(20800,140129584793344)] [INFORMATION]
[ARCHIVELOG BEGIN] LOG(/goldilocks_data/wal/redo_0_0.log(8)) => ARCHIVE(/goldilocks_data/archive_log/archive_8.log)

[2014-09-02 17:41:57.385936 THREAD(20800,140129584793344)] [INFORMATION]
[ARCHIVELOG END] (/goldilocks_data/archive_log/archive_8.log) : SUCCESS

[2014-09-02 17:41:57.385987 THREAD(20800,140129584793344)] [INFORMATION]
[ARCHIVING] inactivate group #0(8)
```

If the log *'Archiving was failed - ...'* outputs after the log *'[ARCHIVELOG BEGIN] ...'* ,, then log archiving is failed. This failure should be immediately resolved in order that the service will be enabled by reusing the redo log file in active state.

The table whose ager is dropped and the aging information for the tablespace will be recorded as follows. When dropping the table, the table lock is also deleted, and the table scn information, scn which is able to aging at aging time and the aging information of table lock will be recorded. If a table has an index, it will be deleted when dropping the table.

```
[2014-09-03 12:13:56.539971 THREAD(5225,139821699815168)] [INFORMATION]
[AGER] aging index - object scn(224), type(0), physical id(22634477649920)

[2014-09-03 12:13:56.540388 THREAD(5225,139821699815168)] [INFORMATION]
[AGER] aging table - object scn(224), object view scn(225), type(0), physical id(22630182682624)

[2014-09-03 12:13:56.540491 THREAD(5225,139821699815168)] [INFORMATION]
[AGER] aging lock item - object scn(226), agable stmt scn(228), physical id(22630182682624)
```

When deleting a tablespace, tablespace scn, aging available scn at aging time and dropped tablespace id are recorded.

```
[2014-09-03 12:13:56.540553 THREAD(5225,139821699815168)] [INFORMATION]
[AGER] aging tablespace - object scn(224), object view scn(227), tablespace id(5)
```

The cleanup thread records the information about abnormally terminated session as follows. Even when a user session is abnormally terminated, the resources of the session is cleaned up, so the database instance or other users continue to operate.

```
[2014-09-03 13:43:02.220139 THREAD(7768,140298504156928)] [WARNING]
[CLEANUP] snipe at zombie session - pid(7766), thread(139967223228160), program(gsql)

[2014-09-03 13:43:02.220211 THREAD(7768,140298504156928)] [WARNING]
[CLEANUP] cleaning session - env(3), session(4), transaction(FFFFFFFFFFFFFFFF), program(gsql), pid(7766), thread(139967223228160)
[2014-09-03 13:43:02.220270 THREAD(7768,140298504156928)] [WARNING]
[CLEANUP] cleaning up 1 sessions
```

- Log of creating, dropping, altering tablespace by a user

The system log records the operations of creating, deleting, updating of a user tablespace. Tablespace related to DDL is recorded by default, regardless of TRACE_DDL ON/OFF. DDL failure will not be recorded in the system log. Therefore, a user should operate the system by setting TRACE_DDL to *ON *in order to figure out more details about DDL log and the causes of its failure.

```
[2014-09-15 10:26:41.649909 THREAD(24881,140468897289984)] [INFORMATION]
[TABLESPACE] Create Tablespace(7)

[2014-09-15 10:26:55.966385 THREAD(24881,140468897289984)] [INFORMATION]
[DATAFILE] add datafile(/home/zkyungoh/work/product/Gliese/home/db/TEST1.dbf)

[2014-09-15 10:27:11.325897 THREAD(24881,140468897289984)] [INFORMATION]
[DATAFILE] Drop Datafile(/home/zkyungoh/work/product/Gliese/home/db/TEST1.dbf)

...

[2014-09-15 10:32:00.669550 THREAD(24881,140468897289984)] [INFORMATION]
[TABLESPACE] drop tablespace ( 7 )
```

- System internal error and index creation failure log

An internal error occurs when GOLDILOCKS database system error occurs but the exact cause of the failure can not be defined. If an internal error occurs, the SQL statement which raised the error is rolled back. The service is continuously available because the error does not affect the system nor does other sessions.

By the way, if the error raising SQL statement is executed again, it could be failed for the same reason, or the cause of failure could disappear and the operation could succeed. Therefore, a user should not change the database at the point of failure, but should request cause analysis to find the cause.

The index creation fails if the same key index on a table exists when creating UNIQUE index. Even though the index creation fails, it does not affect the index tables which are already created. Therefore, it does not affect the service.

```
[2014-09-15 11:26:59.640345 THREAD(7819,140737354012416)] [INFORMATION]
Index creation failed ( physical id : 22638772617216, error code : 14016 )
```

<a id="1fe4edeca457580e"></a>
#### XA Log

It records the success or failure log of start, close, end, rollback, prepare, commit, recover, forget operations of XA transaction interface for processing distributed transactions. GOLDILOCKS database does not record XA trace log by default. TRACE_XA should be set to *ON* to record the XA trace log as follows. For more information, refer to [XA API References](../part-05-developer-manual/31-odbc.md#f9b6eaee23b0166d).

```
gSQL> alter system set trace_xa = yes;

System altered.
```

XA trace log is recorded in 'xa.trc' as follows. At first, executed XA interface is recorded, and then the status (*complete* or *failed*) is recorded. The information such as session id and transaction id is also recorded. If it fails, the error code defined in [XA API References](../part-05-developer-manual/31-odbc.md#f9b6eaee23b0166d) is recorded.

```
[2014-09-15 11:45:19.599018 THREAD(7966,139931504572160)] [INFORMATION]
xa_start() complete - session(4), xid(0.3231.00), flags(0)

[2014-09-15 11:45:19.599360 THREAD(7966,139931504572160)] [INFORMATION]
xa_end() complete - session(4), xid(0.3231.00), flags(4000000)

[2014-09-15 11:45:19.599418 THREAD(7966,139931504572160)] [INFORMATION]
xa_prepare() complete - session(4), xid(0.3231.00), flags(0)

[2014-09-15 11:45:22.864563 THREAD(7966,139931504572160)] [INFORMATION]
xa_recover() complete - session(4), xid(), flags(1000000)

[2014-09-15 11:45:22.864829 THREAD(7966,139931504572160)] [INFORMATION]
xa_commit() complete - session(4), xid(0.3231.00), flags(0)

[2014-09-15 11:45:22.864887 THREAD(7966,139931504572160)] [INFORMATION]
xa_rollback() complete - session(4), xid(0.3232.00), flags(0)

[2014-09-15 11:45:22.885951 THREAD(7966,139931504572160)] [INFORMATION]
xa_forget() complete - session(4), xid(0.3230.00), flags(0)

[2014-09-15 11:45:22.886017 THREAD(7966,139931504572160)] [INFORMATION]
xa_forget() failed - session(4), xid(0.3231.00), flags(0), xa_error(-4)
```

<a id="2dc9f97e55e5615f"></a>
#### DDL Log

For all DDL (creating, dropping, altering) generated in GOLDILOCKS database, the DDL generating sessions, overall SQL statements, status of success or failure are added in system log. In GOLDILOCKS database, DDL log is not recorded by default. TRACE_DDL should be set to *ON* as follows to record DDL trace log.

```
gSQL> alter system set trace_ddl = yes;

System altered.
```

The followings describe an example of which DDL log is recorded when a tablespace is created using the DDL.

```
gSQL> CREATE TABLESPACE TEST_TBS1 
DATAFILE 'TEST_TBS1_01.dbf' SIZE 10M, 
                      'TEST_TBS1_02.dbf' SIZE 10M, 
                      'TEST_TBS1_03.dbf' SIZE 10M;

Tablespace created.
```

```
[2014-09-15 12:26:29.209210 THREAD(8149,140267442067200)] [INFORMATION]
[SESSION:11][DDL success] CREATE TABLESPACE TEST_TBS1 
DATAFILE 'TEST_TBS1_01.dbf' SIZE 10M, 
                      'TEST_TBS1_02.dbf' SIZE 10M, 
                      'TEST_TBS1_03.dbf' SIZE 10M

[2014-09-15 12:26:29.209277 THREAD(8149,140267442067200)] [INFORMATION]
[SESSION:11][COMMIT with DDL]
```

If DDL statement fails, 'DDL failure' is recorded as follows.

```
gSQL> ALTER TABLESPACE TEST_TBS1 ADD DATAFILE 'TEST_TBS1_04.dbf' SIZE 10M;

ERR-42000(16130): file is already exist - '/home/zkyungoh/work/product/Gliese/home/db/TEST_TBS1_04.dbf' : 
ALTER TABLESPACE TEST_TBS1 ADD DATAFILE 'TEST_TBS1_04.dbf' SIZE 10M
                                        *
ERROR at line 1:
```

```
[2014-09-15 12:45:08.598789 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][DDL failure] ALTER TABLESPACE TEST_TBS1 ADD DATAFILE 'TEST_TBS1_01.dbf' SIZE 10M
```

DDL log for table or index DDL statement is recorded in the same way. After creating a table or an index, the committed DDL log is as follows.

```
gSQL> CREATE TABLE T1 ( I1 NATIVE_INTEGER ) TABLESPACE TEST_TBS1;

Table created.

gSQL> CREATE INDEX T1X ON T1 ( I1 );

Index created.

gSQL> COMMIT;

Commit complete.
```

```
[2014-09-15 12:40:37.887952 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][DDL success] CREATE TABLE T1 ( I1 NATIVE_INTEGER ) TABLESPACE TEST_TBS1

[2014-09-15 12:40:47.451806 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][DDL success] CREATE INDEX T1X ON T1 ( I1 )

[2014-09-15 12:40:51.017975 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][COMMIT with DDL]
```

The following is a rollback DDL log after creating a table or an index.

```
[2014-09-15 12:42:27.367722 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][DDL success] CREATE TABLE T1 ( I1 NATIVE_INTEGER ) TABLESPACE TEST_TBS1

[2014-09-15 12:42:31.317436 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][DDL success] CREATE INDEX T1X ON T1 ( I1 )

[2014-09-15 12:42:34.601738 THREAD(8115,140191085913856)] [INFORMATION]
[SESSION:4][ROLLBACK with DDL]
```

<a id="4332245622032651"></a>
#### Trace Log Replication

Replication trace log is recorded in a separate file when using GOLDILOCKS' replication tool such as CYCLONE and LOGMIRROR. For more information about replication trace log, refer to [operating CYCLONE](../part-07-replication/50-cyclone.md#a57e2f11f120138c) in CYCLONE chapter and [operating](../part-07-replication/51-logmirror.md#9159683d94848fd7) in LOGMIRROR chapter.

<a id="4d95796659103f30"></a>
#### Listener Log

The errors and information which occurs from the startup of listener process until the end of the process are recorded in the listener log.

<a id="c26f61398ec1936d"></a>
##### Listener Log Format

The listener log is recorded in the following format.

```
['log recorded date and time' THREAD('process id', 'thread handle')]
['log prefix'] 'log body'
```

- 'log record date and time' is the date and time of the recorded log.
- THREAD ('process Id', 'thread handle') is the information of log process id and thread handle.
- 'log prefix' is the entity or feature which created the log, and 'log body' is the detailed information.

<a id="5e9057d6c0cf0db1"></a>
### Monitoring Performance Using View

Concurrency control for multi-user is needed because database is accessed or updated by multiple users at the same time. The concurrency should be provided for system data and shared resources as well as explicit data by SQL statements. GOLDILOCKS controls the concurrency using latch.

The concurrency control using lock can cause a deadlock when same data is updated by multiple different transactions. The concurrency control using latch (supported by GOLDILOCKS) can cause a deadlock, too. It is because the deadlock affects the performance, so a view is provided to handle the latch when a deadlock occurs.

The transactions generating the deadlock will be found when using V$LOCK_WAIT. Then, the administrator should monitor them, and unlock the deadlock. For more information about V$LOCK_WAIT, refer to [V$LOCK_WAIT](9-database-information.md#862c0534c4840926). For more information for monitoring latch item causing the deadlock, refer to [V$LATCH](9-database-information.md#d8c13ece3dd9ed4e).

---

[← 4. What's New](../part-01-getting-started/4-what-s-new.md) · [Table of contents](../README.md) · [6. Structure and Storage Structure of GOLDILOCKS Database →](6-structure-and-storage-structure-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
