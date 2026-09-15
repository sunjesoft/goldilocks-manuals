<a id="73eefc2a9135ca20"></a>

# 2. Tutorial

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/73eefc2a9135ca20)  
> Tag: `20c.1_30_tag`

[← 1. Preface](1-preface.md) · [Table of contents](../README.md) · [3. Cluster Tutorial →](3-cluster-tutorial.md)

<a id="1ebcf1221492ab6c"></a>
## Managing GOLDILOCKS Instance

This chapter describes the basic knowledge of managing the GOLDILOCKS instance.

<a id="473d9e56f05dac56"></a>
### Overview

GOLDILOCKS database system consists of database and instance. Database is a collection of various files which are necessary for driving database such as dictionary data on memory, user data, data file for dictionary data and user data, online redo files.

Database instance consists of two parts. One is the memory portions containing the run-time information for operating GOLDILOCKS database, and the other is the background process which is used to operate and manage it. Each database instance is identified as shared memory key value and "GOLDILOCKS _DATA" environment variable value, both are used to configure shared memory.

<a id="b029958fbce063f4"></a>
### Property Setting

GOLDILOCKS properties are listed in *$GOLDILOCKS _DATA/conf/goldilocks.properties.conf* file. A user may install GOLDILOCKS using the basic properties. This chapter describes the main properties such as TBS (Tablespace), LOG, CONTROL FILE.

The followings describe main property items of when installing GOLDILOCKS.

**Main property items**

<a id="a16f05ff2bbc9878"></a>
| Property | Description | Default value |
| --- | --- | --- |
| SYSTEM_TABLESPACE_DIR | It is the directory path of installing the following system TBS. * DICTIONARY_TBS * MEM_DATA_TBS * MEM_UNDO_TBS * MEM_TEMP_TBS * MEM_TRANS_TBS | ‘&lt;GOLDILOCKS_DATA&gt;/db’ |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | It is the dictionary tablespace size. | 128M |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | It is the memory data tablespace size. | 200M |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | It is the disk data tablespace size. | 200M |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | It is the undo tablespace size. | 32M |
| LOG_DIR | It is the default log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/wal’ |
| SYSTEM_LOGGER_DIR | It is the system log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/trc’ |
| CONTROL_FILE_COUNT | It is the number of control files. | 2 |
| CONTROL_FILE_0 | It is the first control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl' |
| CONTROL_FILE_1 | It is the second control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_1.ctl' |
| BUFFER_CACHE_SIZE | It is the size of the buffer cache which is used to cache the table and the index page created in the disk tablespace. | 64M |


> 
> - DICTIONARY_TBS: It is the tablespace which stores dictionary tables of GOLDILOCKS.
> 
> 
> 
> - MEM_DATA_TBS: It is the memory tablespace in which the user table/index is generated.
> 
> 
> 
> - DISK_DATA_TBS: It is the disk tablespace in which the user table/index is generated.
> 
> 
> 
> - MEM_UNDO_TBS: It is the tablespace which contains the undo (rollback) information of the transaction.
> 
> 
> 
> - MEM_TRANS_TBS (Cluster only): It is the tablespace used for the global transaction recovery in cluster system. The size is automatically calculated based on the transaction table size and the number of cluster node.
> 

A user can change the text property file ($GOLDILOCKS_DATA/conf/goldilocks.properties.conf), or define a new variable in the form of GOLDILOCKS_&lt;property_name&gt; to change the database settings or instance settings. In the priority, the property file takes precedence over the environment variable.

<a id="193e8f099bd63442"></a>
### Background Process

GOLDILOCKS has a background process (gmaster) for managing instance. gmaster consists of multiple system thread internally, and the contents are as follows.

**System threads**

<a id="fa0fd597189371e4"></a>
| Thread | Description |
| --- | --- |
| Main thread | It starts or ends gmaster process. |
| Log archiving thread | It copies the previous redo log file to a specified location when switching online redo file, and stores it. |
| Ager thread | It cleans up the resources being used by dropped schema objects. |
| Page flusher thread | It distributes the task to the IO slave and controls them in order to store the dirty pages of in-memory into the disk at checkpoint. |
| Log flusher thread | It periodically collects the log records accumulated in the redo log buffer, and then stores them into online redo log file at run-time. |
| Checkpoint thread | It downloads the in-memory's changes to the data file on the disk and the online redo log file when switching redo log file. |
| Cleanup thread | It cleans up resources used by abnormally terminated clients, and then rolls back the transactions. |
| IO slave thread | It performs all disk IO related to data file such as checkpoint and data file loading. |
| Checkpoint list flush thread | It flushes pages linked to the buffer checkpoint list to the disk tablespace. |
| Buffer replace flush thread | It flushes pages linked to the buffer flush list to the disk tablespace. |
| Process monitor thread | It monitors after executing the processes such as balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver), then reexecutes when abnormal termination is detected. |
| Cluster Recover Thread (Cluster only) | It recovers a global transaction in cluster system. |
| Failover Thread (Cluster only) | It deals with the failover through reselecting offiline and coordinator for the members when an error occurs on a specific node or in a network in cluster system. |

<a id="8f43d4541b907f6f"></a>
### Client Process

<a id="5ff04573b0ca40a3"></a>
#### Client/ Server Model

The Client/ Server (C/S) model application is connected to listener (glsnr) which is waiting for access request. Then it creates a new database service process (gserver), in dedicated mode, and it handles user's request by using TCP communication. All these operations are carried out through inter process communication, so any signal generated in the application process does not affect on the state of the database. Moreover, cleanup thread regularly checks and returns all the resources used by abnormally terminated application.

<a id="8efb6bf5c14d07e8"></a>
#### Direct Access Model

GOLDILOCKS supports a direct access (D/A) model as well as Client/ Server (C/S) model. All applications using D/A model are linked to the server library supported by GOLDILOCKS, and then directly access database and instance. Therefore, no other special service process exists but only the application processes does exist.

When D/A model application process is interrupted abnormally by the signal generated during operation, all resources in use will be cleaned up by the signal handler function which the library set during connection. The function cleans up the resources according to the two following steps.

1. The signal handler marks an abnormal termination on the session object and terminates the process. 
2. The cleanup thread of gmaster return resources to the database in the same way as C/S model after a certain period of time.

Application processes directly access the database area in D/A model. Therefore, comply with the following precautions.

- When the D/A model application process is terminated by a fatal signal such as SEGV, the signal handler which was registered by the library at connection to the database should stop using shared resources. If a specific signal handler should be installed in the application it should be declared before connecting to the database.
- When forcibly shut down the application process, do not use SIGKILL (kill-9) because the process can not detect the generation of the signal. A user should use SIGTERM, SIGQUIT or SIGUSR2.

<a id="bcde684b0aca51af"></a>
### Memory Architecture of Instance

The memory size used by the database instance is determined by the relevant properties in the property file. Shared memory used by instance can be divided into static area and tablespace area. Static area includes basic information about public instance, each session, statement, transaction, redo log buffer, dictionary cache and several other operation. Tablespace area includes page frame of each tablespace and Page Control Header (PCH) for controlling them.

The application process memory includes instance memory attached at connection. Additionally, it includes process basis sharing ODBC environment, several ODBC handles, heap memory area with bind information.

<a id="06b187dc7d2a72f8"></a>
### Startup and Shutdown Instance

To startup the GOLDILOCKS instance, set the SHARED_MEMORY_STATIC_KEY property differently from other instances. After that, a user can startup the GOLDILOCKS instance by using gsql. Execute it to take sysdba role as follows.

A user should run [listener](../part-06-utility-manual/36-glsnr.md#0fd87486f960aa01) before startup or shutdown the GOLDILOCKS instance in dedicated mode of C/S model.  
A user can not startup or shutdown the GOLDILOCKS instance in shared mode of C/S model.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

Startup phrase in the GOLDILOCKS instance has several phases as follows.

- NOMOUNT
    - It starts up gmaster process which is a managing daemon of the GOLDILOCKS instance.
- MOUNT
    - It loads properties and recovery control file by using $GOLDILOCKS _DATA environment variable.
- OPEN
    - After loading the tablespace contents from data file, it recovers by using redo log, rebuilds no-logging indexes, creates dictionary cache, and then waits for the user's service connection.

A user can start up the GOLDILOCKS instance by using gsql as follows.

```
gSQL> ＼startup nomount
Startup success

gSQL> alter system mount database;
System altered.

gSQL> alter system open database;
System altered.
```

To directly enter into OPEN phase, do as follows.

```
gSQL> ＼startup open
Startup success
```

If GOLDILOCKS instance is shut down, gmaster (the daemon process for management) would be terminated. Then, connection and database operation is no longer possible.

There are four ways to shutdown the GOLDILOCKS instance as follows.

- NORMAL
    - After blocking the access of a new session and waiting until the end of all connected sessions, a user perform a checkpoint and shuts down the instance. 
- TRANSACTIONAL
    - After blocking the start of a new transaction and waiting until the end of all running transactions, a user performs a checkpoint and shuts down the instance. 
- IMMEDIATE
    - After blocking the execution of a new unit operation (Connection unit with GOLDILOCKS database. e.g. FETCH or EXECUTE, etc.) and waiting until the end of all unit operations, a user rolls back all transactions, performs a checkpoint and shuts down the instance. 
- ABORT
    - Regardless of any connected session's status, a user terminates gmaster and shuts down the instance.

To shutdown an instance, use gsql with sysdba role and perform `\shutdown`, as follows.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL>
```

<a id="e78fcddd92b9e1cf"></a>
### Start and End of Listener

A user should run the listener to provide the service in the client/ server environment.

A user can start the listener as follows.

```
% glsnr --start
 
Listener is started successfully.

%
```

A user can end the listener as follows.

```
% glsnr --stop
 
Listener is stopped.

%
```

For more information about listener control, refer to [glsnr](../part-06-utility-manual/36-glsnr.md#0fd87486f960aa01).  
For more information about how to start or end cluster system refer to [Start and End of Cluster System](3-cluster-tutorial.md#9040f21ba0ec1244).

<a id="dd9ff2ae6810b9b5"></a>
## Installing GOLDILOCKS and Creating Database

This chapter describes how to install the GOLDILOCKS software and create a database.

<a id="8f3311fa9a5529b8"></a>
### Overview

GOLDILOCKS  software is a compressed file with the name such as *goldilocks-&lt;version_no&gt;-&lt;os_type&gt;-&lt;cpu_type&gt;.tar.gz*. After decompressing the file, software binaries, various samples, fundamental database directory structures are created at the corresponding location, and then installation is completed. After the installation, the directory is created, and the directory is named after the package.  Then directories whose names are *goldilocks_home* and *goldilocks_data* are created under it.

- goldilocks_home directory
    - Binary home of GOLDILOCKS product
    - Defined as GOLDILOCKS _HOME environment variable
    - Operation binaries, libraries for the client, header files, licenses, etc. are located.
- goldilocks_data directory
    - Home of the user database (instance) which GOLDILOCKS creates.
    - Defined as GOLDILOCKS _DATA environment variable
    - A default location which has data files, log files, property files

After that, use a utility called gcreatedb in *$GOLDILOCKS_HOME/bin* directory to create a database in *$GOLDILOCKS _DATA* directory.

<a id="315136b586adae89"></a>
### Release Platform

GOLDILOCKS is available in the following release platform.

<a id="fec0e4faecf8ffe5"></a>
<table class="table column_count_5"><caption>Release platform</caption><thead><tr><th class="to_center to_middle"><div>Platform</div></th><th class="to_center to_middle"><div>Platform name</div></th><th class="to_center to_middle"><div>OS</div></th><th class="to_center to_middle"><div>CPU</div></th><th class="to_center to_middle"><div>Remarks</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="4"><div>Server 
platform</div></td><td class="to_middle"><div>linux-x86_64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_64</div></td><td class="to_middle"><div>>= linux kernel 2.6
>= glibc 2.1<small>[1]</small>
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>linux-powerpc-64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>powerpc</div></td><td class="to_middle"><div>&gt;= linux kernel 2.6
>= glibc 2.1<small>[1]</small>
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>hpux11.31-itanium-64</div></td><td class="to_middle"><div>HP-UX 11.31</div></td><td class="to_middle"><div>itanium</div></td><td class="to_middle"><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>aix7-powerpc-64</div></td><td class="to_middle"><div>AIX 6.1</div></td><td class="to_middle"><div>powerpc</div></td><td class="to_middle"><div>&gt;= java 1.6
<= java 1.8</div></td></tr><tr><td class="to_left to_middle" rowspan="8"><div>Client 
platform</div></td><td class="to_middle"><div>linux-x86_64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_64</div></td><td class="to_middle"><div>>= linux kernel 2.6
>= glibc 2.1<small>[1]</small>
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>linux-x86_32</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>x86_32</div></td><td class="to_middle"><div>&gt;= Linux kernel 2.6
>= glibc 2.1<small>[1]</small>
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>hpux11.31-itanium-64</div></td><td class="to_middle"><div>HP-UX 11.31</div></td><td class="to_middle"><div>itanium</div></td><td class="to_middle"><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>hpux11.31-itanium-32</div></td><td class="to_middle"><div>HP-UX 11.31</div></td><td class="to_middle"><div>itanium</div></td><td class="to_middle"><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>aix7-powerpc-64</div></td><td class="to_middle"><div>AIX 7.2</div></td><td class="to_middle"><div>powerpc</div></td><td class="to_middle"><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>linux-powerpc-64</div></td><td class="to_middle"><div>linux</div></td><td class="to_middle"><div>powerpc</div></td><td class="to_middle"><div>&gt;= Linux kernel 2.6
>= glibc 2.1<small>[1]</small>
>= gcc 4.1.2
>= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>windows-x86-64</div></td><td class="to_middle"><div>Windows</div></td><td class="to_middle"><div>PENTINUM x86</div></td><td><div>&gt;= java 1.6
&lt;= java 1.8</div></td></tr><tr><td class="to_middle"><div>windows-x86-32</div></td><td class="to_middle"><div>Windows</div></td><td class="to_middle"><div>PENTINUM x86</div></td><td><div>&gt;= java 1.6
<= java 1.8</div></td></tr></tbody></table>

<small>[1]</small>The user should install libnsl separately in CentOS 8, RHEL 8 or higher.

<a id="8d6574a1e95fca23"></a>
### System Requirements

Check the following requirements before installing GOLDILOCKS.

- At least 2 G should be secured at the physical memory and disk space.
- A sufficient amount of paging (swap) area is required.
- The correct package version which fits into the platform to be installed is required.

<a id="8e6e9e25f1cfd781"></a>
### GOLDILOCKS Package Configuration

This chapter describes the directory configuration when installing GOLDILOCKS.

<a id="110fafddaa312eef"></a>
#### Package Directory Configuration

**Parent directory configuration**

<a id="c657b52ef1dcf389"></a>
| Directory | Server | Client | Description |
| --- | --- | --- | --- |
| GOLDILOCKS_HOME | O | O | Binaries and libraries are installed, overwriting-enabled group when updating |
| GOLDILOCKS_DATA | O | X | The data storing path, overwriting-unabled group |

<a id="c5160a3f877f916b"></a>
<table class="table column_count_3"><caption>Package directory configuration</caption><thead><tr><th class="to_center to_middle"><div>Parent directory</div></th><th class="to_center to_middle"><div>Package directory</div></th><th class="to_center to_middle"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="9"><div>GOLDILOCKS_HOME</div></td><td class="to_middle"><div>admin</div></td><td class="to_middle"><div>Required schema script to create database</div></td></tr><tr><td class="to_middle"><div>bin</div></td><td class="to_middle"><div>Execution files</div></td></tr><tr><td class="to_middle"><div>lib</div></td><td class="to_middle"><div>Library files</div></td></tr><tr><td class="to_middle"><div>include</div></td><td class="to_middle"><div>Header files such as ODBC, XA, Embedded SQL, etc.</div></td></tr><tr><td class="to_middle"><div>license</div></td><td class="to_middle"><div>License files</div></td></tr><tr><td class="to_middle"><div>sample</div></td><td class="to_middle"><div>Sample files</div></td></tr><tr><td class="to_middle"><div>msg</div></td><td class="to_middle"><div>Error message files</div></td></tr><tr><td class="to_middle"><div>script</div></td><td class="to_middle"><div>Script file for ease of use (It will be supported in future)</div></td></tr><tr><td class="to_middle"><div>app_dev</div></td><td class="to_middle"><div>Application development</div></td></tr><tr><td class="to_middle" rowspan="7"><div>GOLDILOCKS_DATA</div></td><td class="to_middle"><div>conf</div></td><td class="to_middle"><div>Configuration files</div></td></tr><tr><td class="to_middle"><div>db</div></td><td class="to_middle"><div>Database files</div></td></tr><tr><td class="to_middle"><div>wal</div></td><td class="to_middle"><div>Log files, control files</div></td></tr><tr><td class="to_middle"><div>archive_log</div></td><td class="to_middle"><div>Archive log files</div></td></tr><tr><td class="to_middle"><div>backup</div></td><td class="to_middle"><div>Back up files</div></td></tr><tr><td class="to_middle"><div>trc</div></td><td class="to_middle"><div>Trace log files, warning message files</div></td></tr><tr><td class="to_middle"><div>journal</div></td><td class="to_middle"><div>Journal file used at cluster rebalance</div></td></tr></tbody></table>

<a id="a31441693b090937"></a>
#### Package File List

The followings are description of files in a directory, and whether it is included in server package or client package.

**admin/ standalone directory**

<a id="0ef20404af19e9d8"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | Read me |
| DictionarySchema.sql | O | X | Dictionary schema creating script |
| InformationSchema.sql | O | X | Information schema creating script |
| PerformanceViewSchema.sql | O | X | Performanceview schema creating script |

**admin/ cluster directory**

<a id="8f47c6c170e70c7d"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | read me |
| DictionarySchema.sql | O | X | Dictionary schema creating script |
| InformationSchema.sql | O | X | Information schema creating script |
| PerformanceViewSchema.sql | O | X | Performanceview schema creating script |

The script created in admin/standalone directory is used when using GOLDILOCKS in standalone. On the other hand, the script created in admin/cluster directory is used when using GOLDILOCKS by configuring cluster system.

**bin directory (Unix)**

<a id="f63e4f305bf31c01"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| gmaster | O | X | GOLDILOCKS master |
| gcreatedb | O | X | Database creating tool |
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

**bin directory (Windows client)**

<a id="a2688a6f3d9c4c8b"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | X | O | read me |
| gloadernet.exe | X | O | Import/export tool for C/S |
| gpec.exe | X | O | Embedded SQL precompiler |
| gsqlnet.exe | X | O | Interactive SQL tool for C/S |
| gloctl.exe | X | O | - |

**lib directory (Unix)**

<a id="f712ba5c81b0ee65"></a>
| File name | Server | Client  (64 bit) | Client  (32 bit) | Description |
| --- | --- | --- | --- | --- |
| README | O | O | O | Read me |
| libstib.so | O | X | X | Shared library for infiniband |
| libgoldilocks.a | O | X | X | D/A and C/S-inclusive static library for ODBC |
| libgoldilocksa.a | O | X | X | D/A-only static library for ODBC |
| libgoldilocksas.so | O | X | X | D/A-only shared library for ODBC |
| libgoldilocksc.a | O | O | O | C/S-only static library for ODBC |
| libgoldilockscs-ul32.so | O | O | X | 64 bit-C/S-only shared library for ODBC (SQLLEN = 4 byte) |
| libgoldilockscs-ul64.so | O | O | X | 64 bit-C/S-only shared library for ODBC (SQLLEN = 8 byte) |
| libgoldilockscs.so | X | X | O | 32 bit-C/S-only shared library for ODBC |
| libgoldilockscvtGB18030_32.so | X | X | O | 32 bit GB18030 character set conversion library |
| libgoldilockscvtGB18030_64.so | O | O | X | 64 bit GB18030 character set conversion library |
| libgoldilockscvtUHC_32.so | X | X | O | 32 bit UHC character set conversion library |
| libgoldilockscvtUHC_64.so | O | O | X | 64 bit UHC character set conversion library |
| libgoldilocksesql.a | O | O | O | Static library for embedded SQL |
| libgoldilocksesqls.so | O | O | O | Shared library for embedded SQL |
| libgoldilockss.so | O | X | X | D/A and C/S-inclusive shared library for ODBC |
| goldilocks6.jar | O | O | O | C/S-only JDBC library (java 1.6) |
| goldilocks7.jar | O | O | O | C/S-only JDBC library (java 1.7) |
| goldilocks8.jar | O | O | O | C/S-only JDBC library (java 1.8) |
| libgoldilocksjni.so | O | X | X | D/A-only JDBC shared library |
| libgoldilocksjnigc.so | O | O | O | JDBC shared library for global connection |

**lib directory (Windows client)**

<a id="0087d94850a71905"></a>
| File name | Server | Client   (64 bit) | Client  (32 bit) | Description |
| --- | --- | --- | --- | --- |
| goldilocksc.lib | X | O | O | C/S-only static library for ODBC |
| goldilockscs.dll | X | X | O | 32 bit-C/S-only shared library for ODBC |
| goldilockscs-ul64.dll | X | O | X | 64 bit-C/S-only shared library for ODBC (SQLLEN = 8byte) |
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

**include directory (Unix)**

<a id="22001151eed229f2"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| sql.h | O | O | ODBC header file |
| sqlca.h | O | O | ODBC header file |
| sqlext.h | O | O | ODBC header file |
| sqltypes.h | O | O | ODBC header file |
| sqlucode.h | O | O | ODBC header file |
| goldilocks.h | O | O | Header file for GOLDILOCKS ODBC application development |
| goldilockstypes.h | O | O | GOLDILOCKS ODBC data type specification file |
| xa.h | O | O | Standard XA header file |
| goldilocksxa.h | O | O | GOLDILOCKS XA header file |
| goldilocksesql.h | O | O | Embedded SQL header file |

**include directory (Windows client)**

<a id="15c1afbac9fb1caa"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | X | O | Read me |
| goldilocks.h | X | O | Header file for GOLDILOCKS ODBC application development |
| goldilockstypes.h | X | O | GOLDILOCKS ODBC data type specification file |
| goldilocksxa.h | X | O | GOLDILOCKS XA header file |
| goldilocksesql.h | X | O | Embedded SQL header file |
| sqlca.h | X | O | ODBC header file |

**license directory**

<a id="0855c60b6b087174"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | X | Read me |

**msg directory**

<a id="90d2537d2623bc44"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| README | O | O | Read me |
| goldilocks_error.msg | O | O | Error message file |

**conf directory**

<a id="72fbbf1884e651f7"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| goldilocks.property.conf | Database operation property text file |
| goldilocks.listener.conf | Listener property file |
| goldilocks.invited.conf | Client management file for database connection invited |
| goldilocks.excluded.conf | Client management file for database connection excluded |
| goldilocks.gagent.conf | gagent-only configuration file |
| tablediff.conf | Tablediff configuration file |
| cyclone.master.conf | Cyclone master only file |
| cyclone.slave.conf | Cyclone slave only file |
| logmirror.master.conf | LogMirror master only file |
| logmirror.slave.conf | LogMirror slave only File |
| odbc.ini | Template for ODBC configuration |
| gsql.ini | Template for gsql configuration |
| glogin.sql | Execution statement list when driving gsql |

**db directory**

<a id="17dc1e5e4b228611"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**wal directory**

<a id="8051b907d2cef9a6"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**archive_log directory**

<a id="3ee7995b4ab7399b"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**backup directory**

<a id="746f8e589151b113"></a>
| File name | Description |
| --- | --- |
| README | Read me |

**trc directory**

<a id="1c8112f3a222c2f1"></a>
| File name | Description |
| --- | --- |
| README | Read me |

<a id="7a0ed63aca3dcd72"></a>
### Installing GOLDILOCKS Software

This chapter describes the operating system and the environment setting before installing GOLDILOCKS.

<a id="d6b1589a502c765e"></a>
#### Kernel Parameters

<a id="703d993b37671a98"></a>
##### Shared Memory

Shared memory is a type of Inter Process Communication (IPC). It is a memory which is used for sharing data in multiple programs. GOLDILOCKS uses shared memory with user programs using gsql, gloader, ODBC for Client/ Server (C/S) environment. Because all tablespaces for operation are created in shared memory, the precise parameter setting is required.

The followings are parameters and the recommended values required for the shared memory which is used to install GOLDILOCKS.

**Kernal properties for shared memory**

<a id="1bd00294de42f56b"></a>
| Parameter  name | Description | Recommended  value | Remarks |
| --- | --- | --- | --- |
| shmmax | The maximum size of single shared memory segment | The value should be bigger than the size of the biggest datafile. | The value should be set bigger than the size of the biggest datafile belonging to the desired tablespace. |
| shmmni | The maximum number of shared memory segment available in system | The value should be bigger than the value of which the number of all datafile + 1. | The value should be set bigger than the value of which the number of all datafile + 1 (shared memory segment for SSA). |
| shmall | The total sum of all shared memory segment  (The number of pages) | The value should bebigger than the total sum of tablespace configuration. | It is the total sum of pages in shared memory available in system. Generally, it is used for 8 GB or bigger shared memory. If the total sum of tablespaces in GOLDILOCKS is 32 GB, shmall should be set bigger than it. |

The following is an example of setting shmall when the total size of tablespaces is 32 GB.

```
kernel.shmmax = 34359738368
kernel.shmmni=4096
kernel.shmall = 8388609
```

• It is assumed that the shmmax is 32 GB and PAGE_SIZE is 4096 bytes.

```
8388609 = (34359738368 / 4096) + 1
```

• In this case, the value of shmall should be bigger than 8388609.

<a id="308105d22ee7d3fd"></a>
##### Semaphore

Semaphore is a kind of IPC, like as shared memory, and it is a technology to control multiple processes' behavior using the resources from the operating system. Depending on semaphore setting, multiple processes can simultaneously refer to a relevant resource, and when any process is in use, the other process may wait until it stops using the resource.

GOLDILOCKS uses semaphore to control the access sequence to the shared memory. For example, if multiple GOLDILOCKS client programs request a change to the same data, it should be controlled properly. The semaphore parameter value should be set to an appropriate value according to semaphore operation of GOLDILOCKS. A general Linux value is recommended.

The followings are recommended semaphore values to install GOLDILOCKS.

**Recommended kernel parameter value for semaphore**

<a id="9728e6d30cab182c"></a>
| Kernel parameter | Description | Recommended  value |
| --- | --- | --- |
| semmsl | The number of semaphores per single semaphore set | 250 |
| semmni | The number of semaphore sets | 128 |
| semmns | The total sum of semaphore sets  (semmni * semmsl) | 32000 |
| semopm | The maximum number of semaphores per system call | 100 |

In Linux based system such as Redhat, Ubuntu, if a user creating IPC resource logs out the session list managed by systemd, then the corresponding IPC resource is automatically deleted. Therefore, the system should be set as follows to prevent deleting the semaphore. (kernel 3.0.0 and higher)

```
# cp -i /etc/systemd/logind.conf /etc/systemd/logind.conf_prev

# cat /etc/systemd/logind.conf
[Login]
#NAutoVTs=6
#ReserveVT=6
...
RemoveIPC=no
```

- Modify it, then execute it.

```
# systemctl restart systemd-logind
```

<a id="2d367bb813f584f7"></a>
##### Network

The backlog means the sockets' queue length waiting to be accepted during the TCP socket listen. Set glsnr's backlog in GOLDILOCKS as glsnr config file's BACKLOG. If the backlog's maximum value in system is bigger than somaxconn, then it sets to somaxconn. In this case, somaxconn should be extended.

GOLDILOCKS uses Unix Domain Socket (UDS) queue when it operates in C/S shared mode. The queue length is set to max_dgram_qlen. If the value is small when clients access the network simultaneously, then it leads to bottleneck state of communication among glsnr, gbalancer and gdispatcher.

The followings are recommended network values to install GOLDILOCKS.

**Recommended kernel parameter value for network**

<a id="d69a482c4e648629"></a>
| Kernel parameter | Description | Recommended  value |
| --- | --- | --- |
| somaxconn | The maximum value of listen backlog | 1024 |
| max_dgram_qlen | Unix domain socket queue size | 256 |

<a id="81030eaee35eec97"></a>
##### Applying Parameters

For a one-time execution, a user can do as follows. (It is required to reapply when the user restarts the system).

```
[SHELL]> echo   34359738368   >  /proc/sys/kernel/shmmax
[SHELL]> echo   8388608 >   /proc/sys/kernel/shmall
[SHELL]> echo   4096   >  /proc/sys/kernel/shmmni
[SHELL]> echo   250 32000 100 128  /proc/sys/kernel/sem
[SHELL]> echo   1024   >  /proc/sys/net/core/somaxconn
[SHELL]> echo   256   >  /proc/sys/net/unix/max_dgram_qlen
```

If a user wants to apply it automatically even when the user restarts the system, the user can do as follows in /etc/sysctl.conf.

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

Use the following command to apply the changes given above.

```
[SHELL]> sysctl  -p
```

<a id="07c800bd18f95537"></a>
##### Checking Parameters

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

<a id="f19d5b1ca9c74718"></a>
#### Decompressing GOLDILOCKS

GOLDILOCKS package is supplied in a compressed form. The basic installation completes by decompression.

The followings are simple examples of how to install the GOLDILOCKS package.

```
##  $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/

[SHELL]> gzip –d goldilocks-mercury.2.1.0-linux-x86_64.tar.gz

[SHELL]> tar -xvf goldilocks-server-mercury.2.1.0-linux-x86_64.tar
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlext.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/goldilocks.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlca.h
…
```

When the decompression completes, a user can change the directory name &lt;package_file_name&gt; on the user's taste, and accordingly the user should change the environment variables of $GOLDILOCKS _HOME and $GOLDILOCKS _DATA.

For more information about directory created by decompression, refer to [GOLDILOCKS Package Configuration](#8e6e9e25f1cfd781)

<a id="74fd79068a5cb24b"></a>
#### Setting Enviromment Variables

After decompression of GOLDILOCKS package, bin and lib path will be created under $GOLDILOCKS _HOME directory. Then as given below, a user should add bin and lib path under PATH and LD__LIBRARY_PATH to execute GOLDILOCKS software and develop applications. (When developing GOLDILOCKS client application, a user should always insert $GOLDILOCKS_HOME/include to include file directory of compile option.)

```
export PATH=$GOLDILOCKS _HOME/bin:$PATH
export LD_LIBRARY_PATH=$GOLDILOCKS _HOME/lib:$LD_LIBRARY_PATH
```

Environment variables are required to use GOLDILOCKS. A user should set them prior to installation because some variables are referenced to even during installation.

**OS environment variables for GOLDILOCKS installation**

<a id="bbd8b8f5428b05c7"></a>
<table><thead><tr><th align="center">Environment<br>variables</th><th align="center" valign="middle">Description</th><th align="center" valign="middle">Remarks</th></tr></thead><tbody><tr><td valign="middle">GOLDILOCKS_HOME</td><td valign="middle">Directory path to install GOLDILOCKS binaries</td><td valign="middle">This variable is referenced during GOLDILOCKS operation, and the directory to install GOLDILOCKS should be set as an environment variable in advance.</td></tr><tr><td valign="middle">GOLDILOCKS_DATA</td><td valign="middle">The location to create GOLDILOCKS database instance</td><td valign="middle">This variable is referenced during GOLDILOCKS database creation and operation.</td></tr><tr><td valign="middle">PATH</td><td valign="middle">Directory path of GOLDILOCKS executable file</td><td valign="middle">This variable should be set to execute various GOLDILOCKS binaries without an absolute path.</td></tr><tr><td valign="middle">LANG</td><td valign="middle">Character set of terminal</td><td valign="middle"><ul><li>If the character set is different from the original character set which is created during GOLDILOCKS database creation, characters (Except alphabets, numbers and special characters) may not be displayed properly. Or the string related functions may not be executed correctly.</li><li>A user should set locale corresponding to GB18030, SQL_ASCII, UHC, UTF8.</li><li>e.g. export LANG=ko_KR.utf8</li></ul></td></tr></tbody></table>

```
##  $GOLDILOCKS_HOME=/home/GOLDILOCKS/goldilocks-mercury.2.1.0-linux-x86_64/

[SHELL]> gzip –d goldilocks-mercury.2.1.0-linux-x86_64.tar.gz

[SHELL]> tar -xvf goldilocks-server-mercury.2.1.0-linux-x86_64.tar
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlext.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/goldilocks.h
goldilocks-server-mercury.2.1.0-linux-x86_64/goldilocks_home/include/sqlca.h
…
```

<a id="1cd22c7bc1353b6d"></a>
#### Deleting Database

Delete datafile, control file, redo log file and archive log file (when using the archive log file) should be deleted when deleting the existing database to recreate the GOLDILOCKS DATABASE.

The following is an example of deleting GOLDILOCKS DATABASE.

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

The location of the data file and archive file may vary depending on the settings by a user.

<a id="dc7a2025ed3eb36b"></a>
#### Deletion

GOLDILOCKS package is not provided in compressed file format, so a specific deletion rule is not required. Delete the installed directory after terminating DATABASE.

The following is an example of deleting GOLDILOCKS package.

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

<a id="3cee40d7d7510538"></a>
### Creating Database

Create database after the completion of property creation. A user can create database by using $GOLDILOCKS_HOME/bin/gcreatedb. The followings are how to use the gcreatedb commands.

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
    --home           home directory
    --member         local member name
    --host           host address
    --port           host port
    --silent         suppresses the display of the result message
    --help           print help message

examples:

    gcreatedb --db_name="goldilocks" --db_comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --char_length_units="OCTETS" --silent
```

*$GOLDILOCKS_HOME/conf/goldilocks.properties.conf* is referenced when creating database. Then, tablespace files are created in *SYSTEM_TABLESPACE_DIR* path in *goldilocks.properties.conf* with the value of ****_TABLESPACE_SIZE*.

--cluster option should be specified when creating the database which is to participate in cluster system.

The followings are execution arguments of gcreatedb.

**Execution arguments of gcreatedb**

<a id="2c193c3a37696151"></a>
| Argument | Description |
| --- | --- |
| --cluster | It is the database to be used in cluster system. If it is omitted, standalone database is created. |
| --db_name | It is the database name. If it is omitted, it is set as goldilocks. |
| --db_comment | It is the database description. If it is omitted, it is set as goldilocks database. |
| --timezone | It is the timezone. If it is omitted, it is set as TIMEZONE property. |
| --character_set | It is the database character set. GOLDILOCKS supports four types of character sets. * GB18030: Simplified Chinese * SQL_ASCII: Character set supporting ASCII  * UHC: Unified Hangul Code  * UTF8: Unicode Transformation Format – 8  If it is omitted, it is set as CHARACTER_SET property. |
| --char_length_units | It is the unit of character length. * OCTETS: It identifies 1 byte as 1 character * CHARACTERS: It identifies 1 character (n byte) as 1 character. If it is omitted, it is set as CHAR_LENGTH_UNITS property. |
| --home | It is the database home directory. It searches for a property file, and is referenced to as a location of creating and storing various DB files. If it is omitted, it uses the value set in GOLDILOCKS_DATA environment variable. |
| --member | It is the member name local database to be used in cluster system. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER property. |
| --host | It is the IP address of local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | It is the TCP listen port of local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_PORT property. |
| --silent | It hides display messages. |
| --help | It displays help messages. |

A user should consider the followings when creating database.

- Setting kernel parameter shared memory 
    - If the size specified in shared memory setting is smaller than the size described in $GOLDILOCKS _HOME/conf/goldilocks.properties.conf, a user can not create the database.
- Tablespace size
    - Tablespace files are created when the database is created, and the tablespace is used after being allocated to the memory as big as the tablespace size when driving GOLDILOCKS. Therefore, it uses memory even when the actual user data does not exist in the data tablespace. Therefore, a user should create database with the sufficient memory considering the actually available memory as well as shared memory on GOLDILOCKS startup machine when writing goldilocks.properties.conf.
- Whether to use cluster system
    - It should be specified that whether the database will participatte as a member of cluster system when creating the database. In other words, --cluster option should be omitted when executing gcreatedb using the database as standalone, but --cluster option should be specified when using the database as cluster system.

When database is created successfully, a user can check the following tablespace file in the path described in SYSTEM_TABLESPACE_DIR of goldilocks.properties.conf.

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

The following is an example of creating database to be used in cluster system.

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

<a id="1d2740362a45da29"></a>
### Building Dictionary Schema Information

Create the following schema to get the system and object information.

> A user should build the following schema after database creation. Otherwise, there is a possibility of malfunction in Catalog API of ODBC, JDBC for obtaining the object's structure information (for example, SQLTables() function). If so, it will not interlock with third party tools.

- DICTIONARY_SCHEMA: It consists of views and tables to get object information such as DBA_*, ALL_*, USER_* .
- INFORMATION_SCHEMA: It consists of views and tables included in the SQL standard INFORMATION_SCHEMA. 
- PERFORMANCE_VIEW_SCHEMA: It consists of views to get system information by combining the fixed tables' information.

Views and tables included in each schemas provides convenience to get system information.

After driving GOLDILOCKS instance on OPEN phase, a user should execute the sql files as follows. It should be done at least once after the first database creation.

> The scripts to build dictionary schema information are divided into the script for standalone system and the script for cluster system. Therefore, a user should use the appropriate script for the purpose to build the information.

The following describes how to build the information by using the script for standalone database.

```
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/InformationSchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/PerformanceViewSchema.sql
```

The following describes how to build the information by using the script for cluster system.

```
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
% gsql --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

<a id="53c2e5fb6f571dd2"></a>
## Managing Database Memory Structure

This chapter describes the database components which compose GOLDILOCKS instance.

<a id="fb730424088b447a"></a>
### Database Memory Structure

GOLDILOCKS database is divided into memory area and disk area. Memory area is a collection of tablespace consisting of one or more shared memories. Owe to its in-memory database, GOLDILOCKS database never goes down to the disk by replace operation.

Disk area consists of data files, control file, property file, online redo log files. Data file exists one per shared memory of each tablespace, and control file contains instance configuration information. property file stores instance environment settings, and online redo log file is used to recover database.

<a id="cd111c8658410500"></a>
#### Control File

Control file records the physically stored information on the disk of database, and determines the status of database by firstly reading at the beginning of Instance startup. The control file records the following information.

- Instance state at the time of the previous checkpoint
- Transaction durability mode (CDS/TDS) at the time of the previous startup
- Online redo log file information
- Data file information of each tablespace

<a id="51a7c29006e4a576"></a>
#### Online Redo Log File

Online redo log files store all changes made to the database by transactions in instances. It is used to recover unwritten changes on the data file when restarting instance after database's abnormal termination. Four online redo log files are generated by default in the size specified in LOG_FILE_SIZE property when creating database. A user can add more if the user need. The redo log files are reused in circulation manner.

Checkpoint are generated when online redo log file switches to the next file, and then some dirty pages move down to an appropriate data file. If the checkpoint operation is delayed and the updated page does not move down (ACTIVE state), all transactions will be suspended until checkpoint completion. Therefore, creating a suitable size online redo log file according to the application's characteristic is helpful to improve the database system performance.

<a id="2ecfd9776c675b4c"></a>
#### Undo Segment

Undo segments records images in advance of changing operation to use when transactions partially or totally rollback. A single undo segment is assigned to a single transaction during update operation. Undo segments are stored in MEM_UNDO_TBS tablespace. It is recommended to secure enough undo tablespace, in preparation for multiple update transactions or a single transaction with large amount of update operation (bulk delete).

<a id="42fa10f7acdc7020"></a>
#### Data File

Data file includes the contents of tables/indexes stored in tablespace.

Data file consists of the followings.

- Page
    - The minimum unit of database I/O. The current size is 8 Kbytes.
- Extent
    - A certain number of continuous pages' collection. The minimum unit of which the segment is allocated space from the tablespace.
    - Extent size of each tablespace could be different. 
- Segment
    - A specific type of data structure's collection. A segment consists of extent sets.

Exceptionally, a temporary tablespace, such as MEM_TEMP_TBS tablespace, does not execute redo logging, nor does data file create.

<a id="70eac93ea5ec2ea0"></a>
#### Tablespace

Database is divided into tablespaces which is a logical structure containing tables and indexes. GOLDILOCKS tablespace is classified into the memory tablespace and the disk tablespace. In the memory tablespace, a separate disk I/O does not occur when the shared memory is created per each data file in the tablespace and accesses to the page. However, in the disk tablespace, the buffer cache of the system is used to access the page. The information about the tablespace existing in the current database can be output by retrieving V$TABLESPACE table.

GOLDILOCKS supports the following tablespaces by default.

<a id="6e1db8c474866680"></a>
<table class="table column_count_3"><caption>Tablespaces of GOLDILOCKS </caption><thead><tr><th class="to_center"><div>Owner</div></th><th class="to_center"><div>Name</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="6"><div>SYSTEM</div></td><td class="to_middle"><div>DICTIONARY_TBS</div></td><td class="to_middle"><div>Default dictionary tables are stored in this tabespace to operate database.</div></td></tr><tr><td class="to_middle"><div>MEM_UNDO_TBS</div></td><td class="to_middle"><div>Undo segments and transaction information are stored in this table space.</div></td></tr><tr><td class="to_middle"><div>MEM_DATA_TBS</div></td><td class="to_middle"><div>If a user does not specify a tablespace when creating schema object, the data table is stored in this tablespace by default.</div></td></tr><tr><td class="to_middle"><div>DISK_DATA_TBS</div></td><td class="to_middle"><div>It is the disk tablespace which the user uses by default.</div></td></tr><tr><td class="to_middle"><div>MEM_TEMP_TBS</div></td><td class="to_middle"><div>Indexes which does not specified tablespace name, and temporary tables which are used by queries are created in the tablespace. Indexes are rebuilt when restarting instance because logging does not occur.</div></td></tr><tr><td class="to_middle"><div>MEM_TRANS_TBS</div></td><td class="to_middle"><div>It is used to recover global transaction in cluster system. It is created only when it is configured as cluster system.</div></td></tr><tr><td class="to_middle"><div>USER</div></td><td class="to_middle"><div>User-defined</div></td><td class="to_middle"><div>User defines this tablespace to collect specific tables to a specific tablespace and manage them.</div></td></tr></tbody></table>

<a id="ba310e6e619d3166"></a>
##### Tablespace Types

There are five types of tablespace as follows.

- DICT
    - Tablespace type for storing dictionary tables and indexes. 
- DATA
    - Tablespace type for storing general schema objects such as tables and indexes.
    - It becomes the subject of redo logging and page flushing. 
- UNDO
    - Tablespace type for storing undo segments.
    - It becomes the subject of redo logging and page flushing. 
- TEMPORARY
    - Tablespace type for storing the temporary tables and no-logging indexes which are created during SELECT query.
    - It is not the subject of redo logging and page flushing.
- TRANSACTION (Cluster only)
    - Tablespace type which is used to recover global transaction in cluster system

<a id="3b79d653c871376b"></a>
### Checking Information of Database Storage Structure

This chapter describes a method to check the information about multiple database storage structure which are mentioned above.

<a id="2f85b3e39517ed92"></a>
#### Control File Information

Use gdump utility to check the contents because control file is stored in binary format.

```
[SHELL]> gdump CONTROL control_0.ctl
```

<a id="5bb21befb197200e"></a>
#### Online Redo Log File Information

Retrieve the control file by using gdump tool, then the name and current state of each online redo file will be displayed.

<a id="bfa21f6a2f15e0ac"></a>
#### Data File Information

Retrieve the control file by using gdump tool, then the data files in each tablespaces and its states will be displayed. Also, viewing the V$DATAFILE table, their current states will be displayed.

<a id="945008772d898c23"></a>
#### Tablespace Information

Retrieve the control file by using gdump tool, then the name and state of each tablespace in the current database will be displayed. Also, a user can enquire the V$TABLESPACE table by using SQL.

<a id="bde9c3a8bdbd8022"></a>
#### Property Information

Open the text file $GOLDILOCKS_Data/conf/goldilocks.properties.conf, then the property information will be displayed. When working online, retrieve V$PROPERTY table, then the information about currently applied property values will be displayed.

<a id="cbb2d9c66a9f71cd"></a>
### General Operation of Data Storage

A tablespace stores data, and its operation is as follows.

<a id="41cdc9e6e1b0ff2e"></a>
#### Creating Tablespace

The memory and the disk USER DATA tablespaces are created as follows.

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

TEMPORARY tablespace does not include data file, so it is created as follows.

```
gSQL> CREATE TEMPORARY TABLESPACE TEST_TEMP_TBS MEMORY 'TEST_TEMP_TBS' SIZE 10M;

Tablespace created.
```

<a id="6af0e9891209becb"></a>
#### Retrieving Tablespace Usage State

A tablespaces space is allocated or deallocated in the unit of one extent consisting of one or more consecutive pages. A user can retrieve the size of one extent (BYTE) in a specific tablespace as follows.

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

Seeing the result above, the empty space in TEST_TBS is 38 * 262144 = 9437184 Byte.

<a id="dfdf7da0c783f815"></a>
#### Altering Tablespace

A user can alter the tablespaces by using Add/Remove Data File (Memory in case of temporary tablespaces), and Online/Offline.

<a id="f4fee8b67248d9c1"></a>
##### Add/ Drop Data File (or Memory)

If a user wants to add spaces to tablespaces while operating the database, the DATA tablespaces allocate the additional space by using the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TBS ADD DATAFILE 'TEST_TBS2.dbf' SIZE 10M;

Tablespace altered.
```

TEMPORARY tablespace adds spaces as follows. Unlike DATA tablespace, a name should be given, and the name should be a unique memory name in database.

```
gSQL> ALTER TABLESPACE TEST_TEMP_TBS ADD MEMORY 'TEST_TEMP_TBS2' SIZE 10M;

Tablespace altered.
```

A user can drop the space in DATA tablespace by using the following syntax. However, if any part of the area is used, the user can not drop it.

```
gSQL> ALTER TABLESPACE TEST_TBS DROP DATAFILE 'TEST_TBS2.dbf';

Tablespace altered.
```

Similarly, a user can withdraw the space in TEMPORARY tablespace by using the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TEMP_TBS DROP MEMORY 'TEST_TEMP_TBS2';

Tablespace altered.
```

<a id="3f17de3f0a64c722"></a>
##### Offline Tablespace

Switch the tablespace to offline mode if a user wants to move the location of data file in the tablespace. Use the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE;

Tablespace altered.
```

A user can switch the tablespace to online mode again by using the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TBS ONLINE;

Tablespace altered.
```

<a id="229c50f030aae795"></a>
##### Altering Automatic Data File Expand Property in Disk Tablespace

The data file in the disk tablespace is created in the initial size, and it is automatically extended to the maximum size when it is needed. The automatic expand property can be on or off as follows. The automatic expand size and the maximum size of the data file can be altered when altering the automatic expand property.

```
gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND ON;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND OFF;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'TEST_DISK_TBS.dbf' AUTOEXTEND ON NEXT 10M MAXSIZE 20M;

Database altered.
```

<a id="a34981a1558eca98"></a>
#### Rename

Rename the tablespace by using the following syntax.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME TO TEST_TBS2;

Tablespace altered.
```

Switch the tablespace to offiline mode, if a user wants to change the location of data file in the tablespace. Then, move the data file by using OS command, rename it by using ALTER TABLESPACE statement, then switch the tablespace to online state.

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE;

Tablespace altered.

gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf';

ERR-42000(16164): file does not exist : 
ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf'
                                                                         *
ERROR at line 1:
```

- The following procedure describes how to rename the file by using OS command.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'TEST_TBS.dbf' TO 'TEST_TBS_1.dbf';

Tablespace altered.

gSQL> ALTER TABLESPACE TEST_TBS ONLINE;

Tablespace altered.
```

<a id="472cc46f1faf3b40"></a>
#### Dropping Tablespace

Drop an unnecessary tablespace by using the following syntax. The statement after INCLUDING is optional, but if the statement is given then it will delete all the content (schema object) and data file in the tablespaces.

```
gSQL> DROP TABLESPACE TEST_TBS INCLUDING CONTENTS AND DATAFILES;

Tablespace dropped.
```

<a id="3ab42b6d1f98aeaa"></a>
### Store Mode

GOLDILOCKS uses the store mode as an instance unit to maximize performance under certain circumstance. Store mode defines which part of ACID property to give up to improve the operation performance in the transaction.

GOLDILOCKS supports two types of store modes.

- Transactional Data Store (TDS) mode
    - TDS mode is default store mode of GOLDILOCKS database.
    - Transactional Data Store (TDS) mode is general DBMS store mode. In this mode, all transactions in the instance write both undo log and redo log. Therefore, a user can rollback the transactions and recover using data file and online redo log file even when an instance is terminated abnormally, because periodical checkpoint are performed.
- Concurrent Data Store (CDS) mode
    - All running transactions in the instance write undo logs, but do not write redo logs. Therefore, the transactions can deal with all run-time errors, and can rollback. But if an instance is terminated abnormally or terminated using shutdown abort statement, all updated data would be lost. (It does not provide recover facility). It is because checkpoint action does not occur. CDS Mode controls concurrency among transactions, so it ensures normal operations of transactions even when different transactions access the same object at the same time. 
    - CDC Mode is mainly used in run-time information oriented database in which query/update operations are frequently performed but does not require durability such as cache server.

Store mode is set through the property setting when a user starts up the instance. Transactions can not be executed in different store modes. The user should carefully set the store mode when the user starts up the instance because the user can not change the instance in online mode.

<a id="5a3b227e5d8cc5e3"></a>
## Managing Schema Object

<a id="9abd2ab827c0771d"></a>
### Schema Object

Schema object is a set of logical structure created by a user. GOLDILOCKS supports the following schema objects, which are table, index, synonym, view, sequence, constraint and stored procedure.

<a id="06771717f24c34a1"></a>
### Schema Object Management Privileges

Currently, GOLDILOCKS supports user and his privilege. Therefore, not all the users share all the created objects, so the privilege should be given to a user.

<a id="2054ed860be536ea"></a>
### Managing Table

This chapter describes table overview, methods of retrieving the table information, creating/ altering table and loading/ dropping data.

<a id="5f576afbfe808b3b"></a>
#### Table

A table is the most basic unit of storage containing user data. A table consists of columns and rows.

<a id="f1b1beeac048a84c"></a>
##### Table Type

Currently, GOLDILOCKS supports general heap table whose data saving order is irrelevant to sort order of a particular column. However, GOLDILOCKS does not support clustered table, partitioned table.

- It supports basic heap table only.
- It supports primary key/unique/not null constraint. 
- It supports the datatypes as follows.
    - BOOLEAN 		
    - SMALLINT, 		INTEGER, BIGINT, REAL, DOUBLE, NUERMIC, FLOAT 		
    - CHAR (MAX 		2000), VARCHAR (MAX 4000), BINARY, VARBINARY, LONG VARCHAR, LONG VARBINARY
    - DATE, 		TIME, TIMESTAMP, INTERVAL (It supports WITH/WITHOUT 		TIMEZONE of TIME/TIMESTAMP.) 		
    - It does not support BLOB type.
- The number of columns, indexes and constraints are not limited.
- A user can retrieve the entire table information using a query *SELECT * FROM TABLES;*.

If a huge number of rows are stored in a particular table, and then the table size becomes big, even bulk delete operation does not return the table's empty space to the tablespace. But TRUNCATE operation can return all existing space to the tablespace.

Table data can be stored and retrieved being distributed to multiple nodes according to the user's desiring distribution policy when using GOLDILOCKS configuring it as cluster system. For more information, refer to [Managing Table](3-cluster-tutorial.md#443225ad6837c4f9)

<a id="68acc2d64ca9c912"></a>
### Managing Index

This chapter describes index overview and creating/deleting index.

<a id="320ef111ab959d00"></a>
#### Overview

Index is a subsidiary schema object which is linked to tables. A user can easily find the location of specifically conditioned row using the index. A user can also retrieve the row's column value if the column is the key column of the index.

GOLDILOCKS can create as many indexes in need to tables. However, too many indexes burden the execution of inserting/ changing/ deleting operation of the table, then it may lower the performance.

Primary key or unique constraint automatically creates an index on that column.

<a id="5fe9aeacb85ab09b"></a>
#### Index Property

- It supports B-link tree form index.
    - GOLDILOCKS provides B-link tree form index by default. 
- The size of a single index node is 8 Kbytes. 	
- The maximum number of key columns is 32, and the maximum key length is 2000 bytes. 	
- It supports unique index. 
- It supports Ascending/Descending, 	NULLS FIRST and NULLS LAST.
    - A user can define whether to sort index key columns in ascending order (ASC) or in descending (DESC) order.
    - A user can define whether to list NULL value of the index key column at first (NULLS 		FIRST) or at last (NULLS 		LAST).
- A user can retrieve the whole index information by using the query *SELECT * FROM INDEXES;*.
- A user can calculate the index size in the similar way of calculating table because index is implemented by segment in the same way of implementing table.

<a id="1bc2a8e03aafb953"></a>
### Sequence

Sequence is a schema object which generates a unique number.

A user can generate the sequence as follows.

```
gSQL> CREATE SEQUENCE customers_seq START WITH 1000 INCREMENT BY 1 NOCACHE NOCYCLE; 

Sequence created.
```

A user can use the sequence by using NEXTVAL.

```
gSQL> SELECT customers_seq.NEXTVAL FROM dual;
```

A user can drop the sequence as follows.

```
gSQL> DROP SEQUENCE customers_seq;
```

Global sequence object is automatically created when user creates sequence by using GOLDILOCKS configuring cluster system. This object manages the global pool of the sequence value which is used being shared by all member nodes in cluster system. Each member node is allocated the sequence value as many as specified from the global object when calling NEXTVAL and uses them.  
For more information, refer to [Global Sequence](3-cluster-tutorial.md#02d28b306c5135b1).

<a id="d05171dfc3157773"></a>
## Managing User

<a id="87ec521e61dc1235"></a>
### Creating User

Only the SYS user and the user with the CREATE USER ON DATABASE privilege can create a user for GOLDILOCKS database. The CREATE SESSION ON DATABASE privilege is required to connect to the newly created user.

The followings are the syntax to create a user.

```
<user definition> ::=
    CREATE USER user_identifier IDENTIFIED BY password
    [ DEFAULT TABLESPACE tablespace_name ]
    [ TEMPORARY TABLESPACE tablespace_name ]
```

The followings are the syntax rules and parameters to create a user.

- user_identifier 	
    - It is a username to be created.
    - The username and the role name should be unique.
    - The length of a user_identifier should be smaller than 128 bytes. 	
- password 	
    - The password is stored encrypted. 	
    - The length of a password should be smaller than 128 bytes. 
    - Password is case-sensitive.
- DEFAULT 	TABLESPACE tablespace_name 	
    - It specifies the default tablespace which stores the objects such as tables, indexes (LOGGING) created by a user which is to be created.
    - If DEFAULT 		TABLESPACE clause is omitted, it specifies as the default 		data tablespace (MEM_DATA_TBS) which is defined when creating DATABASE (&lt;database 		definition&gt;).
- TEMPORARY 	TABLESPACE tablespace_name 	
    - It specifies the TABLESPACE to store user-created temporary tables, index (NO LOGGING), and query processing-generated intermediate results.
    - If TEMPORARY 	TABLESPACE clause is omitted, it is specified as the default temporary tablespace (MEM_TEMP_TBS) which is defined when creating DATABASE (&lt;database 		definition&gt;).
- INDEX TABLESPACE tablespace_name
    - It specifies the default tablespaces to store an index object created by a user to be created.
    - If INDEX TABLESPACE clause is omitted, the default value is INDEX TABLESPACE NULL.

<a id="429f604c83b34975"></a>
### Dropping User

It drops the created user of GOLDILOCKS database. An access privilege and user range for dropping user are as same as those for creating user.

The following is the syntax to drop a user.

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

The followings are the syntax rules and parameters for dropping a user.

- IF 	EXISTS 	
    - Even when the user does not exist, an error does not occur.
- user_identifier 	
    - It is a database username to be dropped.
    - A user can not drop a user, such as SYS, which is automatically generated when the database is created.
    - It does not drop objects, such as tablespace, which is not the owner but created by user_identifier.
- drop 	behavior 	
    - If drop 	behavior is omitted, the default value is RESTRICT.

<a id="d36a0cb42da0e715"></a>
### Altering User

It alters the definition of the GOLDILOCKS database user. ALTER USER privilege is required for an ordinary user. However, if a user is the user_identifier user, then the user can alter the definition without the privilege.

The followings are the syntax to alter the user definition.

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

The followings are the syntax rule and parameters for altering user.

- user_identifier 	
    - It is a username to be altered.
- &lt;alter 	password&gt; 	
    - It alters user password.
    - IDENTIFIED 		BY new_password 		
        - It changes the current password, and the new password is stored encrypted.
        - The length of a password should be smaller than 128 bytes. 
        - Password is case-sensitive. 
    - REPLACE 		old_password 		
        - If a user have ALTER 			USER ON DATABASE privilege, the user can omit it.
        - If a user do not have ALTER 			USER ON DATABASE privilege, the user can not omit it.
        - The user and user_identifier should be same.
- &lt;alter profile&gt;
    - It alters the profile for password management policies.
    - PROFILE profile_name
        - It allocates profile_name created by a user.
    - PROFILE DEFAULT
        - It allocates "DEFAULT" which is the default profile.
    - PROFILE NULL
        - It does not allocate the profile.
- &lt;password expire&gt;
    - It expires the user password.
- &lt;account lock&gt;
    - ACCOUNT LOCK
        - It locks the user account.
    - ACCOUNT UNLOCK
        - It unlocks the account lock.
- &lt;alter 	default tablespace&gt; 	
    - It alters user's default tablespace. 	
    - tablespace_name should be data tablespace.
- &lt;alter 	temporary tablespace&gt; 	
    - It alters user's temporary tablespace. 
    - tablespace_name should be temporary 		tablespace.
- &lt;alter index tablespace&gt;
    - It alters the index tablespace of a user.
    - It assigns INDEX TABLESPACE tablespace_name
        - When assigning the data tablespace, it becomes the LOGGING index.
        - When assigning the temporary tablespace, it becomes the NOLOGGING index.
    - INDEX TABLESPACE NULL
        - It does not assign the index tablespace.

<a id="657379d50591d35c"></a>
## GOLDILOCKS Property

GOLDILOCKS property is classified as the property which is applied when creating database and the property which can be updated at online/offline. A user can change the tablespace path and the redo log file only at MOUNT phase of startup.

<a id="c579e5584c2ab337"></a>
### Properties When Creating Database

**Properties when creating database**

<a id="fbef6541aec3dda4"></a>
| Name | Description |
| --- | --- |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | Initial size of dictionary tablespace |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | Initial size of system data tablespace |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | Initial size of system undo tablespace |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | Initial size of system temporary tablespace |
| LOG_BLOCK_SIZE | Block size of redo log file |
| LOG_FILE_SIZE | Initial size of redo log file |
| LOG_GROUP_COUNT | The number of redo log files |
| CHARACTER_SET | Character set |
| TIMEZONE | Time zone |
| CHAR_LENGTH_UNITS | Character length unit |

<a id="27740daa9944686c"></a>
### Properties When Driving Database

There are more than 100 properties in GOLDILOCKS database. The followings are frequently used properties among them.

**Frequently used properties when driving database**

<a id="59ecaeb10bb4f5d7"></a>
| Name | Description |
| --- | --- |
| SHARED_MEMORY_STATIC_KEY | Key value to create the shared memory |
| SHARED_MEMORY_STATIC_SIZE | Size of the shared memory |
| DATA_STORE_MODE | Storage mode of GOLDILOCKS instance |
| LOG_BUFFER_SIZE | Log buffer size |
| LOG_DIR | Directory path of redo log |
| PRIVATE_STATIC_AREA_SIZE | Static area size per session |
| CLIENT_MAX_COUNT | The maximum number of accessible session |
| PROCESS_MAX_COUNT | The maximum number of process |
| NET_BUFFER_SIZE | Network buffer size per session |

<a id="be318bb300eff7aa"></a>
## GOLDILOCKS Utility

<a id="4808a9494c602c5c"></a>
### gcreatedb

The gcreatedb utility initializes GOLDILOCKS database and gets ready for the service. The gcreatedb generates data files and log files in the GOLDILOCKS_DATA environment variable location according to given properties. The following is a syntax.

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
    --home           home directory
    --member         local member name
    --host           host address
    --port           host port
    --silent         suppresses the display of the result message
    --help           print help message

examples:

    gcreatedb --db_name="goldilocks" --db_comment="goldilocks database" --timezone="+09:00" --character_set="UTF8" --char_length_units="OCTETS" --silent
```

Tablespace files are created in *SYSTEM_TABLESPACE_DIR* of goldilocks.properties.conf as each value of ***_TABLESPACE_SIZE by referring to $GOLDILOCKS_HOME/conf/goldilocks.properties.conf when creating the database.

The followings are execution arguments of gcreatedb command.

**Execution arguments of gcreatedb**

<a id="35158567559e0121"></a>
| Argument | Description |
| --- | --- |
| --cluster | It is the database to be used in cluster system. If it is omitted, standalone database is created. |
| --db_name | It is the database name. If it is omitted, it is set as *goldilocks*. |
| --db_comment | It is the database description. If it is omitted, it is set as *goldilocks database*. |
| --timezone | It is the timezone. If it is omitted, it is set as TIMEZONE property. |
| --character_set | It is the database character set. GOLDILOCKS supports four types of character sets. * GB18030: Simplified Chinese * SQL_ASCII: Character set supporting ASCII  * UHC: Unified Hangul Code  * UTF8: Unicode Transformation Format – 8  If it is omitted, it is set as CHARACTER_SET property. |
| --char_length_units | It is the unit of character length. * OCTETS: It identifies 1 byte as 1 character. * CHARACTERS: It identifies 1 character (n byte) as 1 character. If it is omitted, it is set as CHAR_LENGTH_UNITS property. |
| --home | It is the database home directory. It searches for a property file, and is referenced to as a location of creating and storing various DB files. If it is omitted, it uses the value set in GOLDILOCKS_DATA environment variable. |
| --member | It is the member name of local database to be used in cluster system. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER property. |
| --host | It is the IP address of local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | It is the TCP listen port of local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_PORT property. |
| --silent | It hides display messages. |
| --help | It displays help messages. |

<a id="c15b15641dade1df"></a>
### gsql (GOLDILOCKS Interactive SQL Tool)

gsql is an interactive command line utility to execute SQL statements for managing GOLDILOCKS database. DBA creates initial table schema by using gsql, or checks the current database state.

The following is the gsql syntax.

```
[SHELL]> gsql <userid> <passwd>

gSQL> CREATE TABLE T1 ( COL1 INTEGER );

create success

gSQL> \q

[SHELL]>
```

<a id="8f8ec089e4b81d59"></a>
### gloader (GOLDILOCKS Data Upload/download Tool)

The gloader utility downloads existing data in database to a file in text format, or it uploads an existing data in text format to a new database. The text data file format of gloader is Comma-Separated Value (CSV).

The following is how to use gloader.

```
gloader [export|import] userid/passwd control='control_file_name' \
data='data_file_name' log='log_file_name' bad='bad_file_name'
```

**Arguments of gloader**

<a id="770ce026993b2a0a"></a>
| Argument | Description |
| --- | --- |
| export 	\| import | It declares whether to download the contents of existing table to data_file_name, or to upload existing data in data_file_name to a specified table in control_file_name. |
| userid | It specifies user ID. |
| passwd | It specifies the password of the userid. |
| control | It specifies the file path in which detailed settings are written during export/import operation. |
| data | It specifies target 	data file to export, or data file to import. |
| log | It specifies log file path in which the progress and the elapsed time of import/export operation. |
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
