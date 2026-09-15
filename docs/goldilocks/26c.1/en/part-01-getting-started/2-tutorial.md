<a id="b2083bd710b9d708"></a>

# 2. Tutorial

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/b2083bd710b9d708)  
> Tag: `26c.1_0_tag`

[← 1. Preface](1-preface.md) · [Table of contents](../README.md) · [3. Cluster Tutorial →](3-cluster-tutorial.md)

<a id="c97fc44a77eb7890"></a>
## Managing GOLDILOCKS Instance

This chapter describes the basic knowledge required for managing a GOLDILOCKS instance.

<a id="d441e6c5531664cb"></a>
### Overview

The GOLDILOCKS database system consists of a database and an instance. The database is a collection of various files necessary for operating the database, including dictionary data in memory, user data, data files for dictionary data and user data, and online redo files.

A database instance consists of two parts. one is the memory portions that contain runtime information for operating the GOLDILOCKS database, and the other is the background processes used to operate and manage it. Each database instance is identified by the shared memory key value and the "GOLDILOCKS_DATA" environment variable, both of which are used to configure shared memory.

<a id="36e14f857c36fcc8"></a>
### Property Setting

GOLDILOCKS properties are listed in *$GOLDILOCKS _DATA/conf/goldilocks.properties.conf* file. A user may install GOLDILOCKS using the basic properties provided. This chapter describes the main properties, including TBS (Tablespace), LOG and CONTROL FILE.

The following sections describe the main property items involved in installing GOLDILOCKS.

**Main property items**

<a id="ff21af4582bc7ffc"></a>
| Property | Description | Default value |
| --- | --- | --- |
| SYSTEM_TABLESPACE_DIR | It is the directory path for installing the following system TBS. * DICTIONARY_TBS * MEM_DATA_TBS * MEM_UNDO_TBS * MEM_TEMP_TBS * MEM_TRANS_TBS | ‘&lt;GOLDILOCKS_DATA&gt;/db’ |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | It is the dictionary tablespace size. | 128 M |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | It is the memory data tablespace size. | 200 M |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | It is the disk data tablespace size. | 200 M |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | It is the undo tablespace size. | 32 M |
| LOG_DIR | It is the default log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/wal’ |
| SYSTEM_LOGGER_DIR | It is the system log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/trc’ |
| CONTROL_FILE_COUNT | It is the number of control files. | 2 |
| CONTROL_FILE_0 | It is the first control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl' |
| CONTROL_FILE_1 | It is the second control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_1.ctl' |
| BUFFER_CACHE_SIZE | It is the size of the buffer cache used to cache table and index pages created in the disk tablespace. | 64 M |


> 
> - DICTIONARY_TBS: It is the tablespace that stores the dictionary tables of GOLDILOCKS.
> - MEM_DATA_TBS: It is the memory tablespace where user tables/ indexes are generated.
> - DISK_DATA_TBS: It is the disk tablespace where user tables/ indexes are generated.
> - MEM_UNDO_TBS: It is the tablespace that contains the undo (rollback) information for transactions.
> - MEM_TRANS_TBS (Cluster only): It is the tablespace used for global transaction recovery in a cluster system. Its size is automatically calculated based on the transaction table size and the number of cluster nodes.
> 

A user can modify the text property file ($GOLDILOCKS_DATA/conf/goldilocks.properties.conf), or define a new variable in the form of GOLDILOCKS_&lt;property_name&gt; to change the database or instance settings. In terms of priority, the property file takes precedence over the environment variable.

<a id="8b77b9e497b7cedb"></a>
### Background Process

GOLDILOCKS includes a background process (gmaster) for managing instance. The gmaster process consists of multiple internal system threads, described as follows.

**System threads**

<a id="025292aaf0433f1c"></a>
| Thread | Description |
| --- | --- |
| Main thread | It starts or ends gmaster process. |
| Log archiving thread | It copies the previous redo log file to a specified location when switching online redo file, and stores it. |
| Ager thread | It cleans up resources used by dropped schema objects. |
| Page flusher thread | During a checkpoint, it distributes tasks to the IO slaves to store dirty pages on disk and controls them. |
| Log flusher thread | It periodically collects the log records accumulated in the redo log buffer to the online redo log file during run-time. |
| Checkpoint thread | It downloads dirty pages to the data file on disk and online redo log file when switching the redo log file. |
| Cleanup thread | It cleans up resources used by abnormally terminated clients, and rolls back transactions. |
| IO slave thread | It performs all disk IO related to data files such as checkpoint and data file loading. |
| Process monitor thread | It monitors after executing the processes such as balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver), then reexecutes when abnormal termination is detected. |
| Cluster Recover Thread (Cluster only) | It recovers global transactions in the cluster system. |
| Failover Thread (Cluster only) | It handles failovers by reselecting offiline and coordinator for the members when an error occurs on a specific node or in a network within the cluster system. |

<a id="e1e2ee441ec5c849"></a>
### Client Process

<a id="7449ac24eea36b29"></a>
#### Client/ Server Model

Applications using the Client/Server (C/S) model connects to a listener (glsnr) that is waiting for access requests. Then, it creates a new database service process (gserver), in dedicated mode to handle the user's request by using TCP communication. All operations are carried out through inter process communication, ensuring that any signals generated in the application process does not affect on the state of the database. Moreover, cleanup thread regularly checks and returns all the resources used by abnormally terminated application.

<a id="2b3d9c0e0efeffd0"></a>
#### Direct Access Model

GOLDILOCKS supports a Direct Access (D/A) model as well as a Client/Server (C/S) model. In the D/A model, applications are linked to the server library provided by GOLDILOCKS and directly access the database and instance. Therefore, there are no additional service processes, only the application processes exist.

When a D/A model application process is interrupted abnormally by a signal generated during operation, all resources in use will be cleaned up by the signal handler function set by the library during connection. The function cleans up the resources according to the following two steps.

1. The signal handler marks the session object as having terminated abnormally and then terminates the process.
2. The cleanup thread of gmaster returns resources to the database in a manner similar to the C/S model after a certain period of time.

In the D/A model, application processes access the database area directly. Therefore, adhere to the following precautions.

- When the D/A model application process is terminated by a fatal signal, such as SEGV, the signal handler registered by the library at the time of database connection should cease using shared resources. If a custom signal handler needs to be installed, it should be declared before connecting to the database.
- When forcibly shutting down the application process, avoid using SIGKILL (kill -9), as the process can not detect this signal. Instead, use SIGTERM, SIGQUIT, or SIGUSR2.

<a id="2959e8d4325e1811"></a>
### Memory Architecture of Instance

The memory size utilized by the database instance is determined by the relevant properties specified in the property file. The shared memory used by the instance can be divided into two main areas: the static area and the tablespace area. The static area includes fundamental information about the public instance, as well as details related to each session, statement, transaction, redo log buffer, dictionary cache, and several other operations. The tablespace area consists of the page frames for each tablespace and the Page Control Header (PCH), which manages the page frames.

The application process memory includes instance memory attached at connection. Additionally, it includes the process-based shared ODBC environment, several ODBC handles, and a heap memory area with bind information.

<a id="7909baa054d6dd22"></a>
### Startup and Shutdown of the Instance

To start up the GOLDILOCKS instance, set the SHARED_MEMORY_STATIC_KEY property differently from other instances. After that, you can start up the GOLDILOCKS instance by using gsql. Execute the following command to assume the SYSDBA role.

Before starting up or shutting down the GOLDILOCKS instance in dedicated mode of the C/S model, ensure that the [listener](../part-06-utility-manual/43-glsnr.md#b1c92cc0b4612d13) is running. Note that you cannot start up or shut down the GOLDILOCKS instance in shared mode of the C/S model.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

Startup phrase in the GOLDILOCKS instance has several phases as follows.

- NOMOUNT
    - It starts up gmaster process, which is the managing daemon of the GOLDILOCKS instance.
- MOUNT
    - It loads properties and the recovery control file using the $GOLDILOCKS _DATA environment variable.
- OPEN
    - After loading the tablespace contents from data files, it performs recovery using redo logs, rebuilds no-logging indexes, creates the dictionary cache, and then waits for user service connections.

To start up the GOLDILOCKS instance, use the following gsql command.

```
gSQL> ＼startup nomount
Startup success

gSQL> alter system mount database;
System altered.

gSQL> alter system open database;
System altered.
```

To directly enter into the OPEN phase, do as follows.

```
gSQL> ＼startup open
Startup success
```

If the GOLDILOCKS instance is shut down, the gmaster (the management daemon process) will be terminated. As a result, connections and database operations will no longer be possible.

There are four ways to shut down the GOLDILOCKS instance, as follows.

- NORMAL
    - After blocking access for new sessions and waiting for all connected sessions to end, a user performs a checkpoint and then shuts down the instance. 
- TRANSACTIONAL
    - After blocking the start of new transactions and waiting for all running transactions to complete, a user performs a checkpoint and then shuts down the instance. 
- IMMEDIATE
    - After blocking the execution of new unit operations (e.g., FETCH or EXECUTE, which are connection units with the GOLDILOCKS database) and waiting for all ongoing unit operations to complete, a user rolls back all transactions, performs a checkpoint, and then shuts down the instance. 
- ABORT
    - Regardless of the status of connected sessions, a user terminates the gmaster process and shuts down the instance.

To shutdown an instance, use gsql with the sysdba role and perform the `\shutdown` command as follows.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL>
```

<a id="a06ee4b5a12f1199"></a>
### Start and End of Listener

A user should run the listener to provide service in the client/ server environment.

A user can start the listener as follows.

```
% glsnr --start
 
Listener is started successfully.

%
```

A user can stop the listener as follows.

```
% glsnr --stop
 
Listener is stopped.

%
```

For more information about listener control, refer to [glsnr](../part-06-utility-manual/43-glsnr.md#cfdd4261bac8bef9).  
For more information about how to start or end the cluster system, refer to [Start and End of Cluster System](3-cluster-tutorial.md#c4ead4f42111c434).

<a id="9d1d445ae52786d4"></a>
## Installing GOLDILOCKS and Creating a Database

This chapter describes how to install the GOLDILOCKS software and create a database.

<a id="814a084f9a630d79"></a>
### Overview

GOLDILOCKS  software comes as a compressed file named *goldilocks-&lt;version_no&gt;-&lt;os_type&gt;-&lt;cpu_type&gt;.tar.gz*. After decompressing the file, the software binaries, various samples and fundamental database directory structures are created at the specified location, completing the installation. Following the installation, a directory named after the package is created.  Within this directory, two additional directories are created, which are *goldilocks_home* and *goldilocks_data* are created under it.

- goldilocks_home directory
    - Binary home of GOLDILOCKS product
    - Defined as GOLDILOCKS_HOME environment variable
    - Operation binaries, libraries for the client, header files, licenses, etc. are located.
- goldilocks_data directory
    - Home of the user database (instance) which GOLDILOCKS creates.
    - Defined as GOLDILOCKS _DATA environment variable
    - A default location which has data files, log files, property files

After that, use the utility called gcreatedb in *$GOLDILOCKS_HOME/bin* directory to create a database in the *$GOLDILOCKS _DATA* directory.

<a id="7742f8fe048f39ac"></a>
### Release Platform

GOLDILOCKS is available on the following release platforms.

<a id="7bd6ed542b87c194"></a>
<table class="table column_count_5"><caption>Release platform</caption><thead><tr><th class="to_center to_middle"><div>Platform</div></th><th class="to_center to_middle"><div>Platform name</div></th><th class="to_center to_middle"><div>OS</div></th><th class="to_center to_middle"><div>CPU</div></th><th class="to_center to_middle"><div>Remarks</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>Server 
platform</div></td><td class="to_middle"><div>linux-x86_64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_64</div></td><td class="to_middle"><div>>= linux kernel 2.6
>= glibc 2.1
>= gcc 4.1.2
>= java 1.6
<= java 1.8</div></td></tr><tr><td class="to_left to_middle" rowspan="4"><div>Client 
platform</div></td><td class="to_middle"><div>linux-x86_64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_64</div></td><td class="to_middle"><div>>= linux kernel 2.6
>= glibc 2.1
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>linux-x86_32</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_32</div></td><td class="to_middle"><div>&gt;= Linux kernel 2.6
>= glibc 2.1
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>windows-x86-64</div></td><td class="to_middle"><div>Windows</div></td><td class="to_middle"><div>PENTINUM x86</div></td><td><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>windows-x86-32</div></td><td class="to_middle"><div>Windows</div></td><td class="to_middle"><div>PENTINUM x86</div></td><td><div>&gt;= java 1.6
<= java 1.8</div></td></tr></tbody></table>

<a id="a7f9f91bf91b791b"></a>
### System Requirements

Before installing GOLDILOCKS, ensure that the following requirements are met.

- At least 2 GB of physical memory and disk space must be available.
- A sufficient amount of paging (swap) space is also required.
- Additionally, the correct package version that matches the platform to be installed must be used.

<a id="5cfdbd1e7f60bfe5"></a>
### GOLDILOCKS Package Configuration

This chapter describes the directory configuration required for installing GOLDILOCKS.

<a id="a7aef527b211a76c"></a>
#### Package Directory Configuration

**Parent directory configuration**

<a id="a4fb424a26db1f54"></a>
| Directory | Server | Client | Description |
| --- | --- | --- | --- |
| GOLDILOCKS_HOME | O | O | Binaries and libraries are installed, overwriting-enabled group when updating |
| GOLDILOCKS_DATA | O | X | The data storing path, overwriting-unabled group |

<a id="933040c121d26238"></a>
<table class="table column_count_3"><caption>Package directory configuration</caption><thead><tr><th class="to_center to_middle"><div>Parent directory</div></th><th class="to_center to_middle"><div>Package directory</div></th><th class="to_center to_middle"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="9"><div>GOLDILOCKS_HOME</div></td><td class="to_middle"><div>admin</div></td><td class="to_middle"><div>Required schema script to create the database</div></td></tr><tr><td class="to_middle"><div>bin</div></td><td class="to_middle"><div>Execution files</div></td></tr><tr><td class="to_middle"><div>lib</div></td><td class="to_middle"><div>Library files</div></td></tr><tr><td class="to_middle"><div>include</div></td><td class="to_middle"><div>Header files such as ODBC, XA, Embedded SQL, etc.</div></td></tr><tr><td class="to_middle"><div>license</div></td><td class="to_middle"><div>License files</div></td></tr><tr><td class="to_middle"><div>sample</div></td><td class="to_middle"><div>Sample files</div></td></tr><tr><td class="to_middle"><div>msg</div></td><td class="to_middle"><div>Error message files</div></td></tr><tr><td class="to_middle"><div>script</div></td><td class="to_middle"><div>Script file for ease of use (Planned for future support.)</div></td></tr><tr><td class="to_middle"><div>app_dev</div></td><td class="to_middle"><div>Application development</div></td></tr><tr><td class="to_middle" rowspan="9"><div>GOLDILOCKS_DATA</div></td><td class="to_middle"><div>conf</div></td><td class="to_middle"><div>Configuration files</div></td></tr><tr><td class="to_middle"><div>db</div></td><td class="to_middle"><div>Database files</div></td></tr><tr><td class="to_middle"><div>wal</div></td><td class="to_middle"><div>Log files, control files</div></td></tr><tr><td class="to_middle"><div>archive_log</div></td><td class="to_middle"><div>Archive log files</div></td></tr><tr><td class="to_middle"><div>backup</div></td><td class="to_middle"><div>Back up files</div></td></tr><tr><td><div>extlib</div></td><td><div>External library file</div></td></tr><tr><td class="to_middle"><div>trc</div></td><td class="to_middle"><div>Trace log files, warning message files</div></td></tr><tr><td><div>certs</div></td><td><div>Server-side SSL/TLS file</div></td></tr><tr><td class="to_middle"><div>journal</div></td><td class="to_middle"><div>Journal file used at cluster rebalance</div></td></tr></tbody></table>

<a id="83e15839c6c87263"></a>
#### Package File List

The following is a description of the files in a directory and their inclusion in the server or client package.

**admin/ standalone directory**

<a id="bdaf4bc068e04399"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | Read me |
| DictionarySchema.sql | O | X | Dictionary schema creation script |
| InformationSchema.sql | O | X | Information schema creation script |
| PerformanceViewSchema.sql | O | X | Performanceview schema creation script |

**admin/ cluster directory**

<a id="d204c2f49dc79c7c"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | read me |
| DictionarySchema.sql | O | X | Dictionary schema creation script |
| InformationSchema.sql | O | X | Information schema creation script |
| PerformanceViewSchema.sql | O | X | Performanceview schema creation script |

**admin/ packages directory**

<a id="aaded1c62d9bbcf7"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| DBMS_LOCK.sql | O | X | DBMS_LOCK package creation script |
| DBMS_OUTPUT.sql | O | X | DBMS_OUTPUT package creation script |
| DBMS_SQL.sql | O | X | DBMS_SQL package creation script |
| DBMS_STANDARD.sql | O | X | DBMS_STANDARD package creation script |

The script created in the admin/standalone directory is used when running GOLDILOCKS in standalone. Conversely, the script created in the admin/cluster directory is used when using GOLDILOCKS by configuring cluster system.

**bin directory (Unix)**

<a id="b487d6044a734ce4"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| gmaster | O | X | GOLDILOCKS master |
| gcreatedb | O | X | Database creation tool |
| glsnr | O | X | Listener control tool |
| gbalancer | O | X | Loads balancer for C/S shared |
| gdispatcher | O | X | Manages multiple connections for C/S shared |
| gserver | O | X | Instance manager for C/S |
| gsql | O | X | Interactive SQL tool |
| gsqlnet | O | O | Interactive SQL tool for C/S |
| gpec | O | O | Embedded SQL precompiler |
| logmirror | O | X | Redo log replication tool |
| cyclone | O | X | CDC replication tool |
| gloader | O | X | Import/ export tool |
| gloadernet | O | O | Import/ export tool for C/S |
| cymon | O | X | CDC monitoring Tool |
| gdump | O | X | Control/ log/ data/ binary property file viewer |
| gsyncher | O | X | Synchronization utility for shared memory log and disk log files |
| tablediff.jar | O | X | Table comparison tool |
| cdispatcher | O | X | Manages cluster connections and distributes protocols in cluster system |
| cserver | O | X | Instance manager for cluster system |
| gtrclogger | O | X | Trace log manager for cluster system |
| gmon | O | X | Process monitoring tool |
| galocator | O | X | Location management tool |
| gagent | O | X | Location provider tool |
| gloctl | O | O | Interactive location editing tool |
| gextproc | O | X | External C procedure tool |
| cyfile | O | X | CDC exporting file tool |

**bin directory (Windows client)**

<a id="26e1b817355bdc86"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | X | O | read me |
| gloadernet.exe | X | O | Import/export tool for C/S |
| gpec.exe | X | O | Embedded SQL precompiler |
| gsqlnet.exe | X | O | Interactive SQL tool for C/S |
| gloctl.exe | X | O | - |

**lib directory (Unix)**

<a id="9dd370c6f955e295"></a>
| File name | Server | Client  (64 bit) | Client  (32 bit) | Description |
| --- | --- | --- | --- | --- |
| README | O | O | O | Read me |
| libstib.so | O | X | X | Shared library for infiniband |
| libgoldilocks.a | O | X | X | Static library for ODBC, including D/A and C/S |
| libgoldilocksa.a | O | X | X | D/A-specific static library for ODBC |
| libgoldilocksas.so | O | X | X | D/A-specific shared library for ODBC |
| libgoldilocksc.a | O | O | O | C/S-specific static library for ODBC |
| libgoldilockscs-ul32.so | O | O | X | 64-bit C/S-specific shared library for ODBC (SQLLEN = 4 bytes) |
| libgoldilockscs-ul64.so | O | O | X | 64 bit-C/S-specific shared library for ODBC (SQLLEN = 8 byte) |
| libgoldilockscs.so | X | X | O | 32 bit-C/S-specific shared library for ODBC |
| libgoldilockscvtGB18030_32.so | X | X | O | 32 bit GB18030 character set conversion library |
| libgoldilockscvtGB18030_64.so | O | O | X | 64 bit GB18030 character set conversion library |
| libgoldilockscvtUHC_32.so | X | X | O | 32 bit UHC character set conversion library |
| libgoldilockscvtUHC_64.so | O | O | X | 64 bit UHC character set conversion library |
| libgoldilocksesql.a | O | O | O | Static library for embedded SQL |
| libgoldilocksesqls.so | O | O | O | Shared library for embedded SQL |
| libgoldilockss.so | O | X | X | Shared library for ODBC, including D/A and C/S |
| goldilocks6.jar | O | O | O | C/S-specific JDBC library (java 1.6) |
| goldilocks7.jar | O | O | O | C/S-specific JDBC library (java 1.7) |
| goldilocks8.jar | O | O | O | C/S-specific JDBC library (java 1.8) |
| libgoldilocksjni.so | O | X | X | D/A-specific JDBC shared library |
| libgoldilocksjnigc.so | O | O | O | JDBC shared library for global connection |
| libgdlc.a | O | O | O | C/S-specific static library for ODBC |
| libgdlcs.so | O | O | O | C/S-specific shared library for ODBC |

**lib directory (Windows client)**

<a id="a16ca5d436585f82"></a>
| File name | Server | Client   (64 bit) | Client  (32 bit) | Description |
| --- | --- | --- | --- | --- |
| goldilocksc.lib | X | O | O | C/S-specific static library for ODBC |
| goldilockscs.dll | X | X | O | 32 bit-C/S-specific shared library for ODBC |
| goldilockscs-ul64.dll | X | O | X | 64 bit-C/S-specific shared library for ODBC (SQLLEN = 8byte) |
| goldilockssetup32.dll | X | X | O | 32 bit setup library for ODBC |
| goldilockssetup64.dll | X | O | X | 64 bit setup library for ODBC |
| goldilocksesql.lib | X | O | O | Static library for embedded SQL |
| goldilocksesqls.dll | X | O | O | Shared library for embedded SQL |
| goldilockscvtGB18030_32.dll | X | X | O | 32 bit GB18030 character set conversion library |
| goldilockscvtGB18030_64.dll | X | O | X | 64 bit GB18030 character set conversion library |
| goldilockscvtUHC_32.dll | X | X | O | 32 bit UHC character set conversion library |
| goldilockscvtUHC_64.dll | X | O | X | 64 bit UHC18030 character set conversion library |
| goldilocks6.jar | X | O | O | C/S-only JDBC library (for java 1.6) |
| goldilocks7.jar | X | O | O | C/S-only JDBC library (for java 1.7) |
| goldilocks8.jar | X | O | O | C/S-only JDBC library (for java 1.8) |
| gdlc.lib | X | O | O | C/S-only static library for ODBC |
| gdlcs.lib | X | O | O | C/S-only shared library for ODBC |
| gdlcs.dll | X | O | O | C/S-only shared library for ODBC |
| README | X | O | O | read me |
| goldilocksjnigc.dll | X | O | O | GOLDILOCKS application development library (JDBC D/A mode) |

**include directory (Unix)**

<a id="9395e018cd291930"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| sql.h | O | O | ODBC header file |
| sqlca.h | O | O | ODBC header file |
| sqlda.h | O | O | Embedded SQL header file for SQLDA |
| sqlext.h | O | O | ODBC header file |
| sqltypes.h | O | O | ODBC header file |
| sqlucode.h | O | O | ODBC header file |
| goldilocks.h | O | O | Header file for GOLDILOCKS ODBC application development |
| goldilockstypes.h | O | O | GOLDILOCKS ODBC data type specification file |
| xa.h | O | O | Standard XA header file |
| goldilocksxa.h | O | O | GOLDILOCKS XA header file |
| goldilocksesql.h | O | O | Embedded SQL header file |

**include directory (Windows client)**

<a id="a5acf50396b43c6e"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | X | O | Read me |
| goldilocks.h | X | O | Header file for GOLDILOCKS ODBC application development |
| goldilockstypes.h | X | O | GOLDILOCKS ODBC data type specification file |
| goldilocksxa.h | X | O | GOLDILOCKS XA header file |
| goldilocksesql.h | X | O | Embedded SQL header file |
| sqlda.h | X | O | Embedded SQL header file for SQLDA |
| sqlca.h | X | O | ODBC header file |

**license directory**

<a id="7ca9d4cbbbe1a4e0"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | Read me |

**msg directory**

<a id="76a862cb01009fbb"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| goldilocks_error.msg | O | O | Error message file |

**conf directory**

<a id="383fcca9e906bd76"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| goldilocks.property.conf | Database operation property text files |
| goldilocks.listener.conf | Listener property file |
| goldilocks.invited.conf | Client management file for database connection allowed. |
| goldilocks.excluded.conf | Client management file for database connection denied. |
| goldilocks.gagent.conf | gagent-specific configuration file |
| tablediff.conf | Tablediff configuration file |
| cyclone.master.conf | Cyclone master-specific default file |
| cyclone.slave.conf | Cyclone slave-specific default file |
| logmirror.master.conf | LogMirror master-specific default file |
| logmirror.slave.conf | LogMirror slave-specific default file |
| odbc.ini | Template for ODBC configuration |
| gsql.ini | Template for gsql configuration |
| glogin.sql | Execution statement list when driving gsql |
| goldilocks.glocator.conf | gLocator-only configuration file |
| cyfile.conf | cyfile-only configuration file |

**db directory**

<a id="77abe94eba25e001"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**wal directory**

<a id="a5ba613fb1d07f33"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**archive_log directory**

<a id="3eba4c756d02ab1a"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**backup directory**

<a id="2bad93e4c0cad4c9"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**trc directory**

<a id="e5023fb64beb0f61"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**app_dev directory**

<a id="f220e02453d6cb62"></a>
| File name | Description |
| --- | --- |
| README | read me |

**sample directory**

<a id="93d8a3acf6fd377b"></a>
| File name | Description |
| --- | --- |
| README | read me |

**script directory**

<a id="830ec3e5602b7385"></a>
| File name | Description |
| --- | --- |
| README | read me |

**certs directory**

<a id="9039bc5388c0295d"></a>
| File name | Description |
| --- | --- |
| README | read me |

**extlib directory**

<a id="1be1daad89ed339c"></a>
| File name | Description |
| --- | --- |
| README | read me |
| .lockfile |  |

**journal directory**

<a id="04f8120ab884a7ab"></a>
| File name | Description |
| --- | --- |
| README | read me |

The CDC package includes the following files.

**CDC Package**

<a id="ef734f7044e0553d"></a>
| Path | File name | Description |
| --- | --- | --- |
| bin | cyclone | CDC replication tool |
| bin | cymon | CDC monitoring tool |
| conf | cyclone.master.conf | Default configuration file for the Cyclone master |
| conf | cyclone.slave.conf | Default configuration file for the Cyclone slave |

<a id="3f2b4f172cc714b2"></a>
### Installing GOLDILOCKS Software

This chapter describes the operating system requirements and environment settings needed before installing GOLDILOCKS.

<a id="26bd59e15faf7306"></a>
#### Kernel Parameters

<a id="95e79431633bb282"></a>
##### Shared Memory

Shared memory is a type of Inter-Process Communication (IPC) used for sharing data among multiple programs. GOLDILOCKS utilizes shared memory with user programs through gsql, gloader, and ODBC in a Client/Server (C/S) environment. Since all tablespaces for operations are created in shared memory, precise value settings are required.

The following are the parameters and recommended values required for the shared memory used to install GOLDILOCKS.

**Kernal properties for shared memory**

<a id="017b0a3ca47c0acd"></a>
| Parameter  name | Description | Recommended  value | Remarks |
| --- | --- | --- | --- |
| shmmax | The maximum size of a single shared memory segment | The value must be larger than the size of the largest datafile. | Set this value to be larger than the size of the largest datafile belonging to the desired tablespace. |
| shmmni | The maximum number of shared memory segments available in the system | The value must be greater than the number of datafiles plus one. | Set this value to be greater than the number of datafiles plus one (shared memory segment for SSA). |
| shmall | The total sum of all shared memory segments (number of pages) | The value must be greater than the total sum of the tablespace configuration. | This represents the total number of pages available in shared memory in the system. Typically, this parameter applies to systems with 8 GB or more of shared memory. If the total sum of tablespaces in GOLDILOCKS is 32 GB, shmall must be set to a value greater than this. |

The following is an example of how to set shmall when the total size of tablespaces is 32 GB.

```
kernel.shmmax = 34359738368
kernel.shmmni=4096
kernel.shmall = 8388609
```

- Assume that the shmmax is 32 GB and PAGE_SIZE is 4096 bytes.

```
8388609 = (34359738368 / 4096) + 1
```

- In this case, the value of shmall must be greater than 8388609.

<a id="8383a17e6394689c"></a>
##### Semaphore

A semaphore is a type of IPC, similar to shared memory, and is a technology to control multiple processes' behavior using the resources provided by the operating system. Depending on the semaphore settings, multiple processes can refer to a relevant resource simultaneously, while any process using the resource will cause other processes to wait until it is available.

GOLDILOCKS uses semaphore to control the access sequence to the shared memory. For example, if multiple GOLDILOCKS client programs request a change to the same data, it should be controlled properly. The semaphore parameter value should be set to an appropriate value according to semaphore operation of GOLDILOCKS. A general Linux value is recommended.

The following are the recommended semaphore values for installing GOLDILOCKS.

**Recommended kernel parameter values for semaphore**

<a id="1443d8475f182588"></a>
| Kernel parameter | Description | Recommended  value |
| --- | --- | --- |
| semmsl | The number of semaphores per single semaphore set | 250 |
| semmni | The number of semaphore sets | 128 |
| semmns | The total sum of semaphore sets  (semmni * semmsl) | 32000 |
| semopm | The maximum number of semaphores per system call | 100 |

In Linux-based systems such as Redhat or Ubuntu, if a user who created IPC resource logs out from the session list is managed by systemd, the corresponding IPC resources are automatically deleted. Therefore, the system must be set as follows to prevent the deletion of semaphores. (for kernel 3.0.0 and higher)

```
# cp -i /etc/systemd/logind.conf /etc/systemd/logind.conf_prev

# cat /etc/systemd/logind.conf
[Login]
#NAutoVTs=6
#ReserveVT=6
...
RemoveIPC=no
```

- Execute after the modifications.

```
# systemctl restart systemd-logind
```

<a id="5377ff4e368ef034"></a>
##### Network

The backlog refers to the queue length of sockets waiting to be accepted during the TCP socket listen process. Set the glsnr's backlog in GOLDILOCKS to the value specified in the glsnr configuration file under BACKLOG. If the system's maximum backlog value exceeds somaxconn, then set it to somaxconn. In such cases, increasing the somaxconn value.

GOLDILOCKS uses a Unix Domain Socket (UDS) queue when operating in C/S shared mode. The queue length is set to max_dgram_qlen. If this value is too small while clients are accessing the network simultaneously, it can cause a communication bottleneck among glsnr, gbalancer and gdispatcher.

The following are the recommended network values for installing GOLDILOCKS.

**Recommended kernel parameter value for network**

<a id="7411bd079d2b98b0"></a>
| Kernel parameter | Description | Recommended  value |
| --- | --- | --- |
| somaxconn | The maximum value of the listen backlog | 1024 |
| max_dgram_qlen | Unix domain socket queue size | 256 |

<a id="6dbf6c9bc6135145"></a>
##### Applying Parameters

For a one-time execution, a user can proceed as follows. (It is necessary to reapply the settings when the system is restarted.)

```
[SHELL]> echo   34359738368   >  /proc/sys/kernel/shmmax
[SHELL]> echo   8388608 >   /proc/sys/kernel/shmall
[SHELL]> echo   4096   >  /proc/sys/kernel/shmmni
[SHELL]> echo   250 32000 100 128  /proc/sys/kernel/sem
[SHELL]> echo   1024   >  /proc/sys/net/core/somaxconn
[SHELL]> echo   256   >  /proc/sys/net/unix/max_dgram_qlen
```

If a user wants to apply the settings automatically even after a system restart, the user can proceed as follows in /etc/sysctl.conf.

```
# shared memory
kernel.shmmax = 34359738368
kernel.shmall = 8388608
kernel.shmmni = 4096

# semaphore
kernel.sem = 250 32000 100 128

# network
net.core.somaxconn = 1024
net.unix.max_dgram_qlen = 256
```

Use the following command to apply the described changes.

```
[SHELL]> sysctl  -p
```

<a id="255d60e82b05ff4a"></a>
##### Verifying Parameters

The described parameters can be checked by using the following commands.

```
[SHELL]> ipcs -l

------ Shared Memory Limits --------
max number of segments = 4096
max seg size (kbytes) = 33554432
max total shared memory (kbytes) = 33554432
min seg size (bytes) = 1

------ Semaphore Limits --------
max number of arrays = 128
max semaphores per array = 250
max semaphores system wide = 32000
max ops per semop call = 100
semaphore max value = 32767
```

<a id="888d4e67b35e5fb8"></a>
#### Decompressing GOLDILOCKS

The GOLDILOCKS package is supplied in a compressed form. The basic installation is completed by decompressing it.

The following are simple examples of how to install the GOLDILOCKS package.

```
##  $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/

[SHELL]> gzip –d goldilocks-mercury.2.1.0-linux-x86_64.tar.gz

[SHELL]> tar -xvf goldilocks-server-mercury.2.1.0-linux-x86_64.tar
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlext.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/goldilocks.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlca.h
…
```

When the decompression is complete, the user can rename the directory &lt;package_file_name&gt; as desired. Consequently, the user must update the environment variables $GOLDILOCKS _HOME and $GOLDILOCKS _DATA accordingly.

For more information about directory created after decompression, refer to [GOLDILOCKS Package Configuration](#5cfdbd1e7f60bfe5)

<a id="ff9bdf7c9255d9f9"></a>
#### Setting Enviromment Variables

After decompressing the GOLDILOCKS package, to run the GOLDILOCKS software and develop applications, add the bin and lib directories, created under the $GOLDILOCKS_HOME directory, to the PATH and LD_LIBRARY_PATH environment variables as follows. (When developing GOLDILOCKS client application, a user should always insert $GOLDILOCKS_HOME/include to include file directory of compile option.)

If a shared library exists to call external library functions, the directory set in the EXTLIB_DIR property must be added to LD_LIBRARY_PATH to include it in the search path so that the library can be searched.

```
export PATH=$GOLDILOCKS_HOME/bin:$PATH
export LD_LIBRARY_PATH=$GOLDILOCKS_HOME/lib:$GOLDILOCKS_DATA/extlib:$LD_LIBRARY_PATH
```

Environment variables are required to use GOLDILOCKS. The user must set them before installation, as some variables are referenced even during the installation process.

**OS environment variables referenced during GOLDILOCKS installation**

<a id="47d63679b2c2c197"></a>
<table><thead><tr><th align="center">Environment<br>variables</th><th align="center" valign="middle">Description</th><th align="center" valign="middle">Remarks</th></tr></thead><tbody><tr><td valign="middle">GOLDILOCKS_HOME</td><td valign="middle">Directory path to install GOLDILOCKS binaries</td><td valign="middle">This variable is referenced during GOLDILOCKS operation. The directory where GOLDILOCKS will be installed must be set as an environment variable in advance.</td></tr><tr><td valign="middle">GOLDILOCKS_DATA</td><td valign="middle">The location for creating the GOLDILOCKS database instance</td><td valign="middle">This variable is referenced during both GOLDILOCKS database creation and operation.</td></tr><tr><td valign="middle">PATH</td><td valign="middle">Directory path for GOLDILOCKS executable file</td><td valign="middle">This variable must be set to execute various GOLDILOCKS binaries without specifying the absolute path.</td></tr><tr><td valign="middle">LANG</td><td valign="middle">Character set for the terminal</td><td valign="middle"><ul><li>If the character set differs from the one specified during the creation of the GOLDILOCKS database, characters (except for letters, numbers and special characters) may not display correctly, or string-related functions may not execute properly.</li><li>The user must set the locale to one corresponding to GB18030, SQL_ASCII, UHC or UTF8.</li><li>e.g. export LANG=ko_KR.utf8</li></ul></td></tr></tbody></table>

```
##  $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/

[SHELL]> gzip –d goldilocks-mercury.2.1.0-linux-x86_64.tar.gz

[SHELL]> tar -xvf goldilocks-server-mercury.2.1.0-linux-x86_64.tar
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlext.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/goldilocks.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlca.h
…
```

<a id="47f4adaba4e26922"></a>
#### Deleting Database

When deleting an existing GOLDILOCKS DATABASE to recreate it, the datafile, control file, redo log file, and archive log file (if using archive logs) must be deleted.

The following is an example of how to delete a GOLDILOCKS DATABASE.

```
## $GOLDILOCKS_BASE=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
## $GOLDILOCKS_DATA=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_data/
## $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_home/
[SHELL]> rm -rf $GOLDILOCKS_DATA/db/*.dbf
[SHELL]> rm -rf $GOLDILOCKS_DATA/wal/*.ctl
[SHELL]> rm -rf $GOLDILOCKS_DATA/wal/*.log
[SHELL]> rm -rf $GOLDILOCKS_DATA/archive_log/*.log
```

The location of the data files and archive files may vary depending on user settings.

<a id="678ad7299d809038"></a>
#### Deleting

The GOLDILOCKS package is provided in a compressed file format, so a specific deletion rule is not required. To remove the package, delete the installed directory after terminating the DATABASE.

The following is an example of how to delete the GOLDILOCKS package.

```
## $GOLDILOCKS_BASE=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
## $GOLDILOCKS_DATA=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_data/
## $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_home/
[SHELL]> rm -rf $GOLDILOCKS_DATA
[SHELL]> rm -rf $GOLDILOCKS_HOME
[SHELL]> rm -rf $GOLDILOCKS_BASE



## ~/.bash_profile
$GOLDILOCKS_BASE=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/ ❶ Delete
$GOLDILOCKS_DATA=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_data/ ❷ Delete
$GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/
					goldilocks_home/ ❸ Delete
```

<a id="531376da5fc853cc"></a>
### Creating Database

Create the database after the completing the property creation. A user can create the database using the $GOLDILOCKS_HOME/bin/gcreatedb command. The following are instructions on how to use the gcreatedb commands.

```
[SHELL]> gcreatedb --help
Usage 

    gcreatedb [options]

Options:

    --cluster        cluster system (if not specified, stand-alone system)
    --db_name        database name
    --db_comment     database comment
    --timezone       timezone ( {+/-}{TZH:TZM} )
    --character_set  character set
                       SQL_ASCII
                       UTF8
                       UHC
                       GB18030
    --char_length_units  char length units
                          OCTETS
                          CHARACTERS
    --member         local cluster member name
    --host           cluster ip address or host name
    --port           cluster port number
    --silent         suppresses the display of the result message
    --help           print help message

examples:

    gcreatedb --db_name="goldilocks" --db_comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --char_length_units="OCTETS" --silent
```

The file $GOLDILOCKS_HOME/conf/goldilocks.properties.conf is referenced when creating the database. Tablespace files are created in the SYSTEM_TABLESPACE_DIR path specified in goldilocks.properties.conf with the value of ***_TABLESPACE_SIZE.

The --cluster option must be specified when creating a database that will participate in a cluster system.

The following are the execution arguments for gcreatedb.

**Execution arguments for gcreatedb**

<a id="836a29d5984bb3b7"></a>
| Argument | Description |
| --- | --- |
| --cluster | It is the database that will be used in a cluster system. If omitted, a standalone database is created. |
| --db_name | It is the database name. If omitted, the default name is goldilocks. |
| --db_comment | It is a description for the database. If omitted, the default description is goldilocks database. |
| --timezone | It is the timezone. If omitted, it defaults to the TIMEZONE property. |
| --character_set | It is the character set for the database. GOLDILOCKS supports the following character sets. * GB18030: Simplified Chinese * SQL_ASCII: ASCII character set  * UHC: Unified Hangul Code  * UTF8: Unicode Transformation Format – 8  If omitted, it defaults to the CHARACTER_SET property. |
| --char_length_units | It is the unit of character length. * OCTETS: 1 byte is counted as 1 character. * CHARACTERS: 1 character (n bytes) is counted as 1 character. If omitted, it defaults to the CHAR_LENGTH_UNITS property. |
| --member | It is the member name of the local database to be used in the cluster system. If omitted, it uses the value set in the LOCAL_CLUSTER_MEMBER property. |
| --host | It is the hostname or IP address of the local member for communication between cluster system members. If a host name is provided, the first IPv4 address of the system is used.  If omitted, it defaults to the value in the LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | It is the TCP listen port of the local member for communication between cluster system members. If omitted, it defaults to the value in the LOCAL_CLUSTER_MEMBER_PORT property. |
| --silent | It hides display messages. |
| --help | It displays help messages. |

A user must consider the following when creating a database.

- Setting kernel parameter shared memory 
    - If the size specified in the shared memory setting is smaller than the size described in $GOLDILOCKS _HOME/conf/goldilocks.properties.conf, you can not create the database.
- Tablespace size
    - When creating a database, the tablespace files created will be allocated and used in memory according to their size when GOLDILOCKS is started. Therefore, memory is used even if there is not actual user data in the data tablespace. Therefore, when writing goldilocks.properties.conf, you should consider not only the shared memory but also the available memory on the machine where GOLDILOCKS will be started to ensure that there is sufficient memory for the database.
- Cluster System Usage
    - You must specify whether the database will participate as a member of a cluster system during database creation. Specifically, the --cluster option must be omitted when executing gcreatedb using the database as standalone, but you must include the --cluster option when using the database as a cluster system.

When the database is created successfully, you can check the following tablespace files in the path described in SYSTEM_TABLESPACE_DIR of goldilocks.properties.conf.

```
[SHELL]> gcreatedb
Database created

[SHELL]> gcreatedb --db_name="TEST_DB"                   \
                   --db_commnet="test database comment"  \
                   --timezone="+09:00"                   \
                   --character_set="UHC"                 \
                   --char_length_units="OCTETS"
Database created

[SHELL]> ls $GOLDILOCKS_DATA/db
system_data.dbf  system_dict.dbf  system_undo.dbf
```

The following is an example of creating a database for use in a cluster system.

```
[SHELL]> gcreatedb --cluster
Database created

[SHELL]> gcreatedb --cluster --member=G1N1
Database created

[SHELL]> gcreatedb --cluster --member=G1N1 --host=127.0.0.1 --port 10101
Database created

[SHELL]> gcreatedb --cluster                         \
                   --db_name="TEST_DB"               \
                   --home=$GOLDILOCKS_DATA           \
                   --host=127.0.0.1                  \
                   --port=10101                      \
                   --db_comment="g1n1 db comment"    \
                   --timezone="+09:00"               \
                   --character_set="UHC"             \
                   --char_length_units="OCTETS"
Database created

[SHELL]> ls $GOLDILOCKS_DATA/db
system_data.dbf  system_dict.dbf  system_trans.dbf system_undo.dbf
```

<a id="9852a239ed3a4b96"></a>
### Building Dictionary Schema Information

Create the following schema to retrieve system and object information.

> After creating the database, the user must build the following schema. Failing to do so may cause malfunctions in the Catalog API of ODBC and JDBC when retrieving the object's structure information (e.g., the SQLTables() function). As a result, it may not integrate properly with third-party tools.

- DICTIONARY_SCHEMA: This schema consists of views and tables that provide object information, including those prefixed with DBA_, ALL_, and USER_*.
- INFORMATION_SCHEMA: This schema consists of views and tables that are part of the SQL standard INFORMATION_SCHEMA.
- PERFORMANCE_VIEW_SCHEMA: This schema comprises views that aggregate system information by combining data from fixed tables.

Views and tables included in each schema provide convenience for obtaining system information.

After starting the GOLDILOCKS instance in the OPEN phase, the user must execute the following SQL files. This step must be performed at least once after the initial database creation.

> The scripts to build dictionary schema information are categorized into two types: one for standalone systems and one for cluster systems. Therefore, users must select and execute the appropriate script based on their system type to build the information correctly.

The following describes how to build the dictionary schema information using the script for a standalone database.

```
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/InformationSchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/PerformanceViewSchema.sql
```

The following describes how to build the dictionary schema information using the script for a cluster system.

```
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

The following describes how to create a package to use a built-in package.

```
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="3cedead5d21d92cb"></a>
## Managing Database Memory Structure

This chapter describes the database components that compose a GOLDILOCKS instance.

<a id="6b6b95717b4f92c2"></a>
### Database Memory Structure

The GOLDILOCKS database is primarily divided into memory and disk areas. The memory area consists of a collection of tablespaces, each made up of one or more shared memory segments, and it does not involve writing to disk during replacement operations.

The disk area consists of data files, control files, property files, and online redo log files. Each data file corresponds to a shared memory segment of a tablespace. The control file contains instance configuration information, while the property file stores instance environment settings. The online redo log files are used for database recovery.

<a id="0f4190c51d815e1c"></a>
#### Control File

The control file records information about the physical storage of the database on disk and determines the database's status by being read first at the beginning of instance startup. The control file includes the following information:

- Instance state at the time of the previous checkpoint
- Transaction durability mode (CDS/TDS) at the time of the previous startup
- Online redo log file information
- Data file information for each tablespace

<a id="2e515bd5044626f3"></a>
#### Online Redo Log File

Online redo log files record all changes made to the database by transactions in instances. They are used to recover any unwritten changes to the data files when restarting an instance after an abnormal database termination. By default, four online redo log files are generated with the size specified by the LOG_FILE_SIZE property during database creation. Users can add more log files if needed. The redo log files are reused in a circular manner.

Checkpoints are created when the online redo log file switches to the next file, causing some dirty pages to be written to the appropriate data files. If the checkpoint operation is delayed and updated pages are not written (remaining in the ACTIVE state), all transactions will be suspended until the checkpoint is completed. Therefore, configuring an appropriately sized online redo log file based on the application's characteristics can help improve database system performance.

<a id="fdaf00cd9ae7c980"></a>
#### Undo Segment

Undo segments record images of data before a change operation, allowing transactions to be rolled back partially or fully. Each undo segment is assigned to a single transaction during update operations. Undo segments are stored in the MEM_UNDO_TBS tablespace. It is recommended to allocate sufficient undo tablespace to accommodate multiple update transactions or a single transaction involving a large number of updates (e.g., bulk deletes).

<a id="66f4165ea87ff48e"></a>
#### Data File

A data file contains the contents of tables and indexes stored within a tablespace.

A data file consists of the following:

- Page
    - The smallest unit of database I/O operations, with a current size of 8 kilobytes (KB).
- Extent
    - A collection of a certain number of contiguous pages. It is the smallest unit of space allocation for a segment within a tablespace.
    - The extent size can vary between tablespaces. 
- Segment
    - A collection of a specific type of data structure. A segment consists of a set of extents.

Exceptionally, a temporary tablespace, such as the MEM_TEMP_TBS tablespace, does not perform redo logging, nor does it create data files.

<a id="0ea795a97369b0b1"></a>
#### Tablespace

A database is divided into tablespaces, which are logical structures containing tables and indexes. GOLDILOCKS tablespaces are classified into memory tablespaces and disk tablespaces. In a memory tablespace, shared memory is created for each data file, so there is no separate disk I/O when accessing pages. In contrast, a disk tablespace uses the system’s buffer cache to access pages. Information about the tablespaces currently present in the database can be retrieved by querying the V$TABLESPACE view.

GOLDILOCKS supports the following tablespaces by default.

<a id="54d12f99154f78d7"></a>
<table class="table column_count_3"><caption>Tablespaces of GOLDILOCKS </caption><thead><tr><th class="to_center"><div>Owner</div></th><th class="to_center"><div>Name</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="6"><div>SYSTEM</div></td><td class="to_middle"><div>DICTIONARY_TBS</div></td><td class="to_middle"><div>Default dictionary tables are stored in this tabespace for database operation.</div></td></tr><tr><td class="to_middle"><div>MEM_UNDO_TBS</div></td><td class="to_middle"><div>Undo segments and transaction information are stored in this tablespace.</div></td></tr><tr><td class="to_middle"><div>MEM_DATA_TBS</div></td><td class="to_middle"><div>If a user does not specify a tablespace when creating schema objects, the data tables are stored in this tablespace by default.</div></td></tr><tr><td class="to_middle"><div>DISK_DATA_TBS</div></td><td class="to_middle"><div>It is the default disk tablespace used by the user.</div></td></tr><tr><td class="to_middle"><div>MEM_TEMP_TBS</div></td><td class="to_middle"><div>Indexes that do not have a specified tablespace name and temporary tables used by queries are created in this tablespace. Indexes are rebuilt when the instance is restarted because logging does not occur.</div></td></tr><tr><td class="to_middle"><div>MEM_TRANS_TBS</div></td><td class="to_middle"><div>It is used to recover global transaction in a cluster system. This tablespace is created only if the system is configured as a cluster.</div></td></tr><tr><td class="to_middle"><div>USER</div></td><td class="to_middle"><div>User-defined</div></td><td class="to_middle"><div>It is created and used when a user wants to organize and manage tables for specific purposes within a tablespace.</div></td></tr></tbody></table>

<a id="ccdc646be9bb2fc5"></a>
##### Tablespace Type

There are five types of tablespaces as follows.

- DICT
    - Tablespace type for storing dictionary tables and indexes
- DATA
    - Tablespace type for storing general schema objects, such as tables and indexes
    - This tablespace is subject to redo logging and page flushing. 
- UNDO
    - Tablespace type for storing undo segments
    - This tablespace is also subject to redo logging and page flushing. 
- TEMPORARY
    - Tablespace type for storing temporary tables and no-logging indexes created during SELECT queries
    - This tablespace is not subject to redo logging and page flushing.
- TRANSACTION (Cluster only)
    - Tablespace type used to recover global transaction in a cluster system

<a id="1f6b166672889a72"></a>
### Checking Database Storage Structure Information

This chapter describes the method for checking information about the various database storage structures mentioned above.

<a id="334ea7ab35f1dc26"></a>
#### Control File Information

Use the gdump utility to check the contents, as control file is stored in binary format.

```
[SHELL]> gdump CONTROL control_0.ctl
```

<a id="e18724076ec128b5"></a>
#### Online Redo Log File Information

Retrieve the control file by using gdump tool, then the name and current state of each online redo file will be displayed.

<a id="9fa39aaef883283e"></a>
#### Data File Information

Use the gdump tool to retrieve the control file, which will display the data files in each tablespace and their states. Additionally, you can view the V$DATAFILE table to see their current states.

<a id="f43bdb890c433856"></a>
#### Tablespace Information

Use the gdump tool to retrieve the control file, which will display the name and state of each tablespace in the current database. Additionally, you can also query the V$TABLESPACE table using SQL.

<a id="3778e070212e5986"></a>
#### Property Information

Open the text file $GOLDILOCKS_Data/conf/goldilocks.properties.conf to view the property information. For online operations, retrieve the V$PROPERTY and V$DB_PROPERTY tables to display the currently applied property values.

<a id="393a18009e71800b"></a>
### General Operation of Data Storage

A tablespace stores data, and its operations are as follows:

<a id="18949043e8220991"></a>
#### Creating Tablespace

Memory and disk USER DATA tablespaces can be created using the following commands:

```
gSQL> CREATE TABLESPACE TEST_TBS DATAFILE 'TEST_TBS.dbf' SIZE 10M;

Tablespace created.

gSQL> CREATE MEMORY TABLESPACE TEST_TBS DATAFILE 'TEST_MEM_TBS.dbf' SIZE 10M;

Tablespace created.

gSQL> CREATE DISK TABLESPACE TEST_TBS DATAFILE 'TEST_DISK_TBS.dbf' SIZE 10M;

Tablespace altered.

gSQL> CREATE DISK TABLESPACE DISK_TBS DATAFILE 'TEST_DISK_TBS.dbf' SIZE 10M AUTOEXTEND OFF;

Tablespace altered.
```

The TEMPORARY tablespace does not include a data file, so it is created as follows:

```
gSQL> CREATE TEMPORARY TABLESPACE TEST_TEMP_TBS MEMORY 'TEST_TEMP_TBS' SIZE 10M;

Tablespace created.
```

<a id="6eca74b573e384c5"></a>
#### Retrieving Tablespace Usage Status

Space in a tablespace is allocated or deallocated in units of one extent, which consists of one or more consecutive pages. To retrieve the size of one extent (in bytes) for a specific tablespace, use the following method:

```
gSQL> SELECT EXTENT_SIZE FROM V$TABLESPACE WHERE TBS_NAME = 'TEST_TBS';

EXTENT_SIZE
-----------
     262144

1 row selected.
```

A user can view the state of all extents in tablespaces by using D$TABLESPACE_EXTENT table. When an extent is in use, the STATE column is 'U'. When an extent is in free state, the STATE column is 'F'. Therefore, the remaining size of space in the current tablespace (the number of extents) can be calculated as follows.

```
gSQL> SELECT COUNT(*) FROM D$TABLESPACE_EXTENT('TEST_TBS') WHERE STATE = 'F';

COUNT(*)
--------
      38

1 row selected.
```

Based on the result above, the empty space in TEST_TBS is calculated as 38×262,144=9,437,18438 \times 262,144 = 9,437,18438×262,144=9,437,184 bytes.

<a id="4b0b54aaa7fc3a61"></a>
#### Altering Tablespace

A user can alter tablespaces by using Add/Remove Data File (or Memory for temporary tablespaces), and Online/Offline.

<a id="a578899ee62aa983"></a>
##### Add/ Drop Data File (or Memory)

If a user wants to add space to tablespaces while the database is operating, the DATA tablespaces can allocate additional space using the following syntax:

```
gSQL> ALTER TABLESPACE TEST_TBS ADD DATAFILE 'TEST_TBS2.dbf' SIZE 10M;

Tablespace altered.
```

The TEMPORARY tablespace adds space as follows. Unlike the DATA tablespace, a name must be specified, and it should be a unique memory name within the database.

```
gSQL> ALTER TABLESPACE TEST_TEMP_TBS ADD MEMORY 'TEST_TEMP_TBS2' SIZE 10M;

Tablespace altered.
```

A user can drop space in the DATA tablespace using the following syntax. However, if any part of the space is used, it can not be dropped.

```
gSQL> ALTER TABLESPACE TEST_TBS DROP DATAFILE 'TEST_TBS2.dbf';

Tablespace altered.
```

Similarly, a user can withdraw space from the TEMPORARY tablespace using the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TEMP_TBS DROP MEMORY 'TEST_TEMP_TBS2';

Tablespace altered.
```

<a id="c10fc282dc4a6783"></a>
##### Offline Tablespace

Switch the tablespace to offline mode if you want to move the location of a data file within the tablespace. Use the following syntax:

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE;

Tablespace altered.
```

A user can switch the tablespace back to online mode using the following syntax:

```
gSQL> ALTER TABLESPACE TEST_TBS ONLINE;

Tablespace altered.
```

<a id="8e29a9dd001252e8"></a>
##### Altering Automatic Data File Expand Property in Disk Tablespace

The data file in a disk tablespace is created with a initial size, and automatically extends to its maximum size as needed. The automatic expansion feature can be enabled or disabled (on/off) as follows. When altering the automatic expansion property, you can also modify the automatic expansion size and the maximum size of the data file.

```
gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND ON;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND OFF;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND ON NEXT 10M MAXSIZE 20M;

Database altered.
```

<a id="507d5297e4e5fad6"></a>
#### Rename

Rename the tablespace using the following syntax:

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME TO TEST_TBS2;

Tablespace altered.
```

Switch the tablespace to offiline mode if you want to change the location of the data file in the tablespace. Then, move the data file using an OS command, rename the datafile of the tablespace using the ALTER TABLESPACE statement, and finally switch the tablespace back to online mode.

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE;

Tablespace altered.

gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf';

ERR-42000(16164): file does not exist : 
ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf'
                                                                         *
ERROR at line 1:
```

- The following procedure describes how to rename a file using an OS command:

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf';

Tablespace altered.

gSQL> ALTER TABLESPACE TEST_TBS ONLINE;

Tablespace altered.
```

<a id="91e29f94a9cc88e6"></a>
#### Dropping Tablespace

Drop an unnecessary tablespace using the following syntax. The statement after INCLUDING is optional. If the statement is given, it will delete all content (schema objects) and data files within the tablespace.

```
gSQL> DROP TABLESPACE TEST_TBS INCLUDING CONTENTS AND DATAFILES;

Tablespace dropped.
```

<a id="a5b62d046efc4189"></a>
### Store Mode

GOLDILOCKS uses the store mode as an instance unit to maximize performance under certain circumstances. Store mode defines which aspect of the ACID properties can be sacrificed to improve transaction performance.

GOLDILOCKS supports two types of store modes.

- Transactional Data Store (TDS) mode
    - TDS mode is the default store mode for the GOLDILOCKS database.
    - Transactional Data Store (TDS) mode is a standard DBMS store mode. In this mode, all transactions in the instance write both undo logs and redo logs. As a result, users can roll back transactions and recover data using the data file and online redo log file, even if the instance terminates abnormally, due to periodic checkpoints.
- Concurrent Data Store (CDS) mode
    - In CDS mode, all running transactions in the instance write undo logs but do not write redo logs. This allows transactions to handle run-time errors and roll back if necessary. However, if an instance is terminated abnormally or terminated using the shutdown abort statement, all updated data will be lost. (The mode does not provide recover facilities). CDS mode controls concurrency among transactions ensuring normal operations of transactions even when different transactions access the same object simultaneously. 
    - CDC mode is primarily used in runtime information-oriented databases, such as cache server, where frequent query/update occur but durability is not a requirement.

The store mode is configured through property settings when the instance is started. Transactions can not be executed across different store modes. Therefore, users must carefully select the store mode during instance startup, as it cannot be changed while the instance is running in online mode.

<a id="de102a44de8df561"></a>
## Managing Schema Object

<a id="58453eb9d1174220"></a>
### Schema Object

A schema object is a set of logical structures created by a user. GOLDILOCKS supports the following schema objects: table, index, synonym, view, sequence, constraint, stored procedure, stored function, package, library, and trigger.

<a id="c3559464848b029f"></a>
### Schema Object Management Privileges

Currently, GOLDILOCKS supports user accounts and their associated privileges. Therefore, not all created objects are shared with all users, and privileges must be granted to allow sharing.

<a id="e08d4ab91fbfdfe9"></a>
### Managing Table

This chapter covers an overview of tables, methods for retrieving table information, procedures for creating, altering tables and loading/ dropping data.

<a id="ccc93d258590d8fd"></a>
#### Table

A table is the fundamental unit of storage for user data. It is composed of columns and rows.

<a id="db412edd0e490f55"></a>
##### Table Type

Currently, GOLDILOCKS supports general heap tables, where the order of data storage is not related to the sort order of any particular column. However, GOLDILOCKS does not support clustered tables or partitioned tables.

- It supports only basic heap tables.
- It supports primary key/unique/not null constraints. 
- It supports the following data types:
    - BOOLEAN 		
    - SMALLINT, 		INTEGER, BIGINT, REAL, DOUBLE, NUERMIC, FLOAT 		
    - CHAR (MAX 		2000), VARCHAR (MAX 4000), BINARY, VARBINARY, LONG VARCHAR, LONG VARBINARY
    - DATE, 		TIME, TIMESTAMP, INTERVAL (It supports WITH/WITHOUT 		TIMEZONE of TIME/TIMESTAMP.) 		
    - It does not support the BLOB type.
- There is no limit on the number of columns, indexes, or constraints.
- A user can retrieve the entire table information using the query: SELECT * FROM TABLES;.

If a large number of rows are stored in a particular table, resulting in a big table size, even a bulk delete operation may not return the table's empty space to the tablespace. However, TRUNCATE operation can return all the existing space to the tablespace.

Table data can be stored and retrieved across multiple nodes according to the user's desired distribution policy when GOLDILOCKS is configured it as a cluster system. For more information, refer to [Managing Table](3-cluster-tutorial.md#55f3218018bcbc51)

<a id="bc7e338877af4ea7"></a>
### Managing Index

This chapter covers an overview of indexes and procedures for creating and deleting them.

<a id="6e98d017a62ec49d"></a>
#### Overview

An index is a subsidiary schema object linked to tables. It allows users to quickly locate rows that meet specific conditions. Additionally, if the column is a key column of the index, users can directly retrieve the values from that column.

GOLDILOCKS allows the creation of multiple indexes on tables as needed. However, having too many indexes can burden the execution of insert, update, and delete operations, potentially reducing performance.

A primary key or unique constraint automatically creates an index on the associated column.

<a id="6e7c35cba72a16f2"></a>
#### Index Property

- It supports B-link tree index.
    - GOLDILOCKS provides B-link tree index by default. 
- The size of a single index node is 8 KB. 	
- The maximum number of key columns is 32, and the maximum key length is 2000 bytes. 	
- Unique indexes are supported.. 
- Sorting options include Ascending/Descending, NULLS FIRST, and NULLS LAST.
    - Users can define whether to sort index key columns in ascending order (ASC) or descending (DESC) order.
    - Users can define whether to list NULL values of the index key column first (NULLS 		FIRST) or last (NULLS 		LAST).
- Users can retrieve the entire index information by using the query: *SELECT * FROM INDEXES;*.
- The index size can be calculated similarly to a table because an index is implemented as a segment in the same way a table is.

<a id="17cc443e4650ad2e"></a>
### Sequence

A sequence is a schema object that generates unique numbers.

A user can create a sequence as follows:

```
gSQL> CREATE SEQUENCE customers_seq START WITH 1000 INCREMENT BY 1 NOCACHE NOCYCLE; 

Sequence created.
```

A user can use the sequence by utilizing NEXTVAL.

```
gSQL> SELECT customers_seq.NEXTVAL FROM dual;
```

A user can drop the sequence as follows:

```
gSQL> DROP SEQUENCE customers_seq;
```

When a user creates a sequence in GOLDILOCKS configured a cluster system, a global sequence object is automatically created. This object manages the global pool of sequence values, which are shared among all member nodes in the cluster. Each member node is allocated a specified number of sequence values from the global object when calling NEXTVAL and uses them accordingly.  
For more information, refer to [Global Sequence](3-cluster-tutorial.md#3c6868a388280a2f).

<a id="c0bf8be7787797f7"></a>
## Managing User

<a id="3650fa6728c76be3"></a>
### Creating User

Only the SYS user and users with the CREATE USER ON DATABASE privilege can create users for the GOLDILOCKS database. The CREATE SESSION ON DATABASE privilege is required to connect using the newly created user.

The following is the syntax to create a user:

```
<user definition> ::=
    CREATE USER user_identifier IDENTIFIED BY password
    [ DEFAULT TABLESPACE tablespace_name ]
    [ TEMPORARY TABLESPACE tablespace_name ]
```

The following are the syntax rules and parameters for creating a user:

- user_identifier 	
    - It specifies the username to be created.
    - Both the username and the role name must be unique.
    - The length of a user_identifier must be less than 128 bytes.
- password 	
    - The password is stored in an encrypted form. 	
    - The length of the password must be less than 128 bytes. 
    - Passwords are case-sensitive.
- DEFAULT 	TABLESPACE tablespace_name 	
    - It specifies the default tablespace where objects created by the user being created, such as tables and indexes (with logging), will be stored.
    - If the DEFAULT 		TABLESPACE clause is omitted, it defaults to the data tablespace (MEM_DATA_TBS) defined when creating the DATABASE (&lt;database 		definition&gt;).
- TEMPORARY 	TABLESPACE tablespace_name 	
    - It specifies the TABLESPACE for storing user-created temporary tables, indexes (NO LOGGING), and intermediate results generated by queries.
    - If the TEMPORARY 	TABLESPACE clause is omitted, it defaults to the temporary tablespace (MEM_TEMP_TBS) defined when creating the DATABASE (&lt;database 		definition&gt;).
- INDEX TABLESPACE tablespace_name
    - It specifies the default tablespace for storing index objects created by the user being created.
    - If the INDEX TABLESPACE clause is omitted, the default value is INDEX TABLESPACE NULL.

<a id="fceed8225bc02649"></a>
### Dropping User

It drops a user from the GOLDILOCKS database. The access privileges and user range required to drop a user are the same as those required to create a user.

The following is the syntax for dropping a user:

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

The following are the syntax rules and parameters for dropping a user.

- IF 	EXISTS 	
    - Even if the user does not exist, an error does not occur.
- user_identifier 	
    - It is the database username to be dropped.
    - Users cannot drop certain built-in users, such as SYS, which are automatically created when the database is created.
    - It does not drop objects, such as tablespaces, that were created by user_identifier but are not owned by them.
- drop behavior
    - If drop 	behavior is omitted, the default value is RESTRICT.

<a id="becaa84965d7f7f3"></a>
### Altering User

It alters the definition of a GOLDILOCKS database user. The ALTER USER privilege is required for ordinary users. However, if the user is the user_identifier user, they can alter their own definition without needing this privilege.

The following is the syntax for altering the user definition:

```
<alter user statement> ::=
      ALTER USER user_identifier <alter user action>
    | ALTER USER PUBLIC <alter schema path>
    ;

<alter user action> ::=
      <alter password>
    | <alter profile>
    | <alter default tablespace>
    | <alter temporary tablespace>
    | <alter index tablespace>
    | <alter schema path>

<alter password> ::=
    IDENTIFIED BY new_password [ REPLACE old_password ]

<alter profile> ::=
    PROFILE { profile_name | DEFAULT | NULL }

<password expire> ::=
    PASSWORD EXPIRE

<account lock> ::=
    ACCOUNT { LOCK | UNLOCK }

<alter default tablespace> ::=
    DEFAULT TABLESPACE tablespace_name

<alter temporary tablespace> ::=
    TEMPORARY TABLESPACE tablespace_name

<alter index tablespace> ::=
    INDEX TABLESPACE { tablespace_name | NULL }

<alter schema path> ::=
    SCHEMA PATH ( { schema_name | CURRENT PATH } [, ...] )
```

The following are the syntax rules and parameters for altering a user:

- user_identifier 	
    - It is the username to be altered.
- &lt;alter 	password&gt; 	
    - It alters the user's password.
    - IDENTIFIED 		BY new_password 		
        - It changes the current password, storing the new password in an encrypted form.
        - The length of the password must be less than 128 bytes. 
        - Passwords are case-sensitive. 
    - REPLACE 		old_password 		
        - If a user has the ALTER 			USER ON DATABASE privilege, they can omit this clause.
        - If a user does not have the ALTER 			USER ON DATABASE privilege, they can not omit this clause.
        - The user must match the user_identifier.
- &lt;alter profile&gt;
    - It alters the profile for password management policies.
    - PROFILE profile_name
        - It assigns the profile_name created by a user.
    - PROFILE DEFAULT
        - It assigns the "DEFAULT", which is the default profile.
    - PROFILE NULL
        - It does not assign a profile.
- &lt;password expire&gt;
    - It sets the user's password to expire.
- &lt;account lock&gt;
    - ACCOUNT LOCK
        - It locks the user account.
    - ACCOUNT UNLOCK
        - It unlocks the account.
- &lt;alter 	default tablespace&gt; 	
    - It alters the user's default tablespace. 	
    - tablespace_name must be a data tablespace.
- &lt;alter 	temporary tablespace&gt; 	
    - It alters the user's temporary tablespace. 
    - tablespace_name must be a temporary 		tablespace.
- &lt;alter index tablespace&gt;
    - It alters the index tablespace for the user.
    - It assigns INDEX TABLESPACE tablespace_name
        - If assigned a data tablespace, it becomes a LOGGING index.
        - If assigned a temporary tablespace, it becomes a NOLOGGING index.
    - INDEX TABLESPACE NULL
        - It does not assign an index tablespace.

<a id="2fd9a294aa745e4f"></a>
## GOLDILOCKS Property

GOLDILOCKS properties are classified into those applied during database creation and those that can be updated while the database is online or offline. A user can change the tablespace path and redo log file only during the MOUNT phase of startup.

<a id="105f03e6ec249cee"></a>
### Properties Applied During Database Creation

**Properties applied during database creation**

<a id="e2bbd5ea179fbeab"></a>
| Name | Description |
| --- | --- |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | Initial size of the dictionary tablespace |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | Initial size of the system data tablespace |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | Initial size of the system undo tablespace |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | Initial size of the system temporary tablespace |
| LOG_BLOCK_SIZE | Block size for the redo log file |
| LOG_FILE_SIZE | Initial size of the redo log file |
| LOG_GROUP_COUNT | The number of redo log files |
| CHARACTER_SET | Character set |
| TIMEZONE | Time zone |
| CHAR_LENGTH_UNITS | Character length unit |

<a id="67a7712f477bc172"></a>
### Properties Applied During Database Startup

There are over 100 properties in the GOLDILOCKS database. The following are some of the most frequently used properties:

**Properties applied during database startup**

<a id="a2059558c929650a"></a>
| Name | Description |
| --- | --- |
| SHARED_MEMORY_STATIC_KEY | Key value to create the shared memory |
| SHARED_MEMORY_STATIC_SIZE | Size of the shared memory |
| DATA_STORE_MODE | Storage mode for the GOLDILOCKS instance |
| LOG_BUFFER_SIZE | Size of the log buffer |
| LOG_DIR | Directory path for redo logs |
| PRIVATE_STATIC_AREA_SIZE | Size of the static area allocated per session |
| CLIENT_MAX_COUNT | The maximum number of accessible sessions |
| PROCESS_MAX_COUNT | The maximum number of processes |
| NET_BUFFER_SIZE | Network buffer size allocated per session |

<a id="60ecd09e6da41674"></a>
## GOLDILOCKS Utility

<a id="b3de67da49a24b93"></a>
### gcreatedb

The gcreatedb utility initializes the GOLDILOCKS database and prepares it for the service. It generates data files and log files in the location specified by the GOLDILOCKS_DATA environment variable, based on the provided properties. The following is the syntax:

```
[SHELL]> gcreatedb --help
Usage 

    gcreatedb [options]

Options:

    --cluster                 cluster system (if not specified, stand-alone system)
    --db_name                 database name
    --db_comment              database comment
    --timezone                timezone ( {+/-}{TZH:TZM} )
    --character_set           character set
                                SQL_ASCII
                                UTF8
                                UHC
                                GB18030
    --char_length_units       char length units
                                OCTETS
                                CHARACTERS
    --member                  local cluster member name
    --host                    cluster ip address or host name
    --port                    cluster port number
    --silent                  suppresses the display of the result message
    --help                    print help message

examples:

    gcreatedb --db_name="goldilocks" --db_comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --char_length_units="OCTETS" --silent
```

When creating the database, tablespace files are generated in the *SYSTEM_TABLESPACE_DIR* path specified in *goldilocks.properties.conf*, with each file sized according to the ****_TABLESPACE_SIZE* values referenced from *$GOLDILOCKS_HOME/conf/goldilocks.properties.conf*.

The following are the execution arguments for the gcreatedb command:

**Execution arguments for gcreatedb**

<a id="acb4edcd0665a1f7"></a>
| Argument | Description |
| --- | --- |
| --cluster | It is the database to be used in a cluster system. If omitted, a standalone database is created. |
| --db_name | It is the database name. If omitted, it is set as goldilocks. |
| --db_comment | It is the database description. If omitted, it defaults to goldilocks database. |
| --timezone | It is the timezone. If omitted, the default is the TIMEZONE property. |
| --character_set | It is the database character set. GOLDILOCKS supports four character sets: * GB18030: Simplified Chinese * SQL_ASCII: Character set supporting ASCII  * UHC: Unified Hangul Code  * UTF8: Unicode Transformation Format – 8  If omitted, it defaults to the CHARACTER_SET property. |
| --char_length_units | It is the unit of character length: * OCTETS: 1 byte is counted as 1 character. * CHARACTERS: 1 character (n bytes) is counted as 1 character. If it is omitted, it defaults to the CHAR_LENGTH_UNITS property. |
| --home | It is the database home directory. This directory is used to locate the property file and serves as the location for creating and storing various database files. If it is omitted, it defaults to the value set in the GOLDILOCKS_DATA environment variable. |
| --member | It is the member name of the local database to be used in the cluster system. If omitted, it defaults to the value set in the LOCAL_CLUSTER_MEMBER property. |
| --host | It is the host name or the IP address of local member to be used for communication between cluster system members. If the host name is used, then it uses the first IPv4 address of the system. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | It is the TCP listen port of the local member to be used for communication between cluster system members. If it is omitted, it defaults to the value set in the LOCAL_CLUSTER_MEMBER_PORT property. |
| --silent | It suppresses display messages. |
| --help | It suppresses help messages. |

<a id="0cd14be365d9daef"></a>
### gsql (GOLDILOCKS Interactive SQL Tool)

gsql is an interactive command line utility used for executing SQL statements to manage the GOLDILOCKS database. It allows database administrators (DBAs) to create initial table schemas and check the current state of the database.

The following is the gsql syntax.

```
[SHELL]> gsql <userid> <passwd>

gSQL> CREATE TABLE T1 ( COL1 INTEGER );

create success

gSQL> \q

[SHELL]>
```

<a id="ce750531424c00a2"></a>
### gloader (GOLDILOCKS Data Upload/download Tool)

The gloader utility is used to download existing data from a database into a text file, or it uploads an existing data in text format to a new database. The text data file format of gloader is Comma-Separated Value (CSV).

The following is how to use gloader.

```
gloader [export|import] userid/passwd control='control_file_name' \
data='data_file_name' log='log_file_name' bad='bad_file_name'
```

**gloader sample arguments**

<a id="663eac058ea544a0"></a>
| Argument | Description |
| --- | --- |
| export 	\| import | gloader declares whether to download the contents of an existing table to data_file_name, or to upload the existing data in data_file_name to a table specified in control_file_name. |
| userid | It specifies the user ID. |
| passwd | It specifies the password associated with the userid. |
| control | It specifies the file path where detailed settings for the export or import operation are recorded. |
| data | It specifies the target data file for export, or the data file for import. |
| log | It specifies the log file path where the progress and elapsed time of import/export operation will be recorded. |
| bad | It specifies bad file path which records data records failed in insertion at importing due to various errors. |

The following is an example of a control file.

```
TABLE  TEST_TBL
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
```

---

[← 1. Preface](1-preface.md) · [Table of contents](../README.md) · [3. Cluster Tutorial →](3-cluster-tutorial.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
