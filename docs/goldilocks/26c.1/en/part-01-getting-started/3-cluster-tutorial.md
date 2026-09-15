<a id="7f3a7970b24e7f8a"></a>

# 3. Cluster Tutorial

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/7f3a7970b24e7f8a)  
> Tag: `26c.1_0_tag`

[← 2. Tutorial](2-tutorial.md) · [Table of contents](../README.md) · [4. What's New →](4-what-s-new.md)

<a id="3d868a53dc624056"></a>
## Managing GOLDILOCKS Cluster System

This chapter provides basic information on configuring and managing a cluster system using multiple GOLDILOCKS databases. It covers only the aspects specific to the cluster system or that distinguish it from a standalone database. Therefore, it is a prerequisite to read the standalone database tutorial before this chapter.

<a id="39a856d068b2dfc4"></a>
### Overview

GOLDILOCKS can be used by configuring a standalone database as described in the previous chapter. Alternatively, users can bind multiple databases into a single cluster and select a suitable solution for data distribution. In other words, users can customize the distribution of large data across multiple servers when using the GOLDILOCKS cluster system. This approach ensures high availability and enhances throughput through parallel processing.

The GOLDILOCKS cluster system consists of one or more cluster groups, and each cluster group consists one or more cluster members. It does not require an additional application server or a meta server. Applications operate by connecting to cluster members that act as data servers. Cluster members within the same cluster group maintain identical data replication (replicas).

When creating the database for each node, users should decide whether to use GOLDILOCKS as a standalone system or as a cluster system. If using a cluster system, users must add cluster-related options when creating the database on each node.

<a id="f2f12d8d2f043757"></a>
### Property Settings

Properties for building a cluster system are specified in the $GOLDILOCKS_DATA/conf/goldilocks.property.conf file on each server, similar to the configuration for a standalone database. Main properties for TBS (tablespace), LOG and CONTROL FILE can be set in the same way as for a standalone system, even when using a cluster system. However, when configuring multiple databases on a single server for a cluster system, ensure that the paths and ports for each file do not overlap among cluster members.

The following describes the main property items for configuring a cluster system.

**Main property items**

<a id="dc1a5ee8cbfabce6"></a>
| Property | Description | Default value |
| --- | --- | --- |
| SYSTEM_TABLESPACE_DIR | It is the directory path for installing the following system TBS. * DICTIONARY_TBS * MEM_DATA_TBS * MEM_UNDO_TBS * MEM_TEMP_TBS * MEM_TRANS_TBS | ‘&lt;GOLDILOCKS_DATA&gt;/db’ |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | It is the size of the dictionary tablespace. | 256M |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | It is the size of the data tablespace. | 200M |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | It is the size of the undo tablespace. | 32M |
| LOG_DIR | It is the default log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/wal’ |
| SYSTEM_LOGGER_DIR | It is the system log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/trc’ |
| CONTROL_FILE_COUNT | It is the number of control files. | 2 |
| CONTROL_FILE_0 | It specifies the path of the first control file. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl' |
| CONTROL_FILE_1 | It specifies the path of the second control file. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_1.ctl' |
| LOCAL_CLUSTER_MEMBER | It is the name of the cluster member used by the local server in the cluster system. | ‘G1N1’ |
| LOCAL_CLUSTER_MEMBER_HOST | It is the host name of the local server. | '127.0.0.1' |
| LOCAL_CLUSTER_MEMBER_PORT | It is the TCP listen port used by the local server for communication in the cluster system. | 10101 |

The name of each cluster member and its host-port combination must be unique within the cluster system. To omit the above property settings, provide this information using the *--member, --host and --port* options when creating the database with gcreatedb. The member information specified through properties or gcreatedb options is stored and managed in the *$GOLDILOCKS_DATA/wal/location.ctl* file.

To modify the properties, update the text property file (*$GOLDILOCKS_DATA/conf/goldilocks.properties.conf*), or define a new variable in a form of *GOLDILOCKS_&lt;property_name&gt;* in an environment variable. The property file takes precedence over the environment variable.

<a id="80c07a53af63f5f0"></a>
### Background Process

The GOLDILOCKS cluster system includes a background process (gmaster) that manages instances for each member node. Each node's gmaster consists of multiple internal system threads. While most of these threads are the same as those in a standalone system, the following system threads are added to manage the cluster system.

The following threads are executed only when starting a database configured in cluster mode.

- Cluster recover thread: It recovers global transactions in the cluster system.
- Failover thread: It manages failover by reselecting offiline and coordinator members when an error occurs on a specific node or within the network in the cluster system.

The following two processes are additionally initiated when using GOLDILOCKS in a cluster system:

- cdispatcher: It transmits and receives cluster packets and manages sessions.
- cserver: It performs operations for modifying and querying the database to which the member node belongs.

The GOLDILOCKS cluster system requires complex cluster protocol communication among member nodes. The cluster dispatcher (cdispatcher) is responsible for efficiently managing network communication contexts and packet distribution. Additionally, it continuously monitors the validity of cluster sessions through heartbeat signals.

In a cluster system, when an SQL query executed on a specific node (the driver node) needs to store data on a remote member node or query data stored on that node according to the sharding policy of the target table, a process is required on each member node to handle these requests and return the results. The process that performs this role is cserver.

<a id="b670575fbfc73364"></a>
### Client Process

Users can use both the client server (C/S) model and direct access (D/A) model in a cluster system, just as in a standalone system. However, since each member node in the cluster system has its own listener, the client program must be aware of the listen port for each cluster member it intends to connect to in advance (in C/S mode). Users can process various transactions by accessing any node in the cluster system similar to how they would with a standalone database.

Other aspects, such as signal handling, connection cleanup, and the release of shared resources, are handled in the same way in both standalone and cluster systems.

<a id="fe913d5712b2abfe"></a>
### Memory Structure of an Instance

The GOLDILOCKS cluster system is designed to integrate multiple shared-nothing databases into a unified management unit, functioning as a single cluster system. Each member node in the cluster operates with memory in a manner similar to that of a standalone system. The amount of memory used by each member node is determined by properties set in its own configuration. The static area contains instance basic information for database management, including session details, statements, transactions, redo log buffers, dictionary caches, and other operational data much like a standalone system. Additionally, information for managing cluster sessions, such as information for the locations and cluster session data are stored.

The tablespace area is composed of page frames and a Page Control Header (PCH). Each page frame holds the contents of a specific tablespace, while the PCH manages and controls these page frames.

The application process memory contains instance memories attached when connecting, the ODBC environment shared within the process unit, various ODBC handles, and a heap memory area containing other information such as bind information.

<a id="c4ead4f42111c434"></a>
### Starting and Shutting Down the Cluster System

To start the GOLDILOCKS system, create an instance on each member node beforehand (gcreatedb), and then register the cluster group and cluster members. Later, a user can start or shut down the system using sysdba role through gsql and gsqlnet.

In the C/S model's dedicated mode, if you want to start or shut down the GOLDILOCKS cluster system, meaning if you intend to use gsqlnet, the [listener](../part-06-utility-manual/43-glsnr.md#cfdd4261bac8bef9) must be running.

The GOLDILOCKS cluster system can not be started or shut down in the C/S model's shared mode.

```
% gsql --as sysdba

Enter user-name: sys
Enter password: 

Connected to an idle instance.

gSQL>
```

The GOLDILOCKS cluster system has the following startup phases: the OPEN phase, which is subdivided into LOCAL OPEN and GLOBAL OPEN, unlike in a standalone system.

- NOMOUNT
    - It launches gmaster, a demon responsible for managing the GOLDILOCKS instance.
- MOUNT
    - It reads properties and the control file for recovery purposes, using the $GOLDILOCKS_DATA environment variable.
- LOCAL OPEN
    - It involves loading tablespace content from data files, performing recovery using redo log files, recovering in-doubt global transactions, rebuilding no-logging indexes, and creating dictionary caches.
- OPEN (GLOBAL OPEN)
    - It connects cluster sessions for each cluster member, arranges the shard map, selects both a global manager (global coordinator) and a group manager (group coordinator), then waits for user access to the service.

To start or shut down the GOLDILOCKS cluster system, the cluster system environment must be configured by performing the following preliminary steps. If the member name, host address, port number are uniquely specified when creating each member database using gcreatedb, the property setting process for each node can be omitted.

- Setting properties: Update the property files to be used on each member node. 
- Creating the database: Create the database on each member node using gcreatedb.
- Creating the cluster group and adding members: Create a group and add members by configuring the cluster system.
- Starting the listener: Ensure the listener on each node is started beforehand to use gsqlnet.

Use the following syntaxes to create a cluster group or a member:

- [ALTER CLUSTER GROUP name ADD MEMBER](../part-03-sql-manual/18-sql-references-a-b.md#587d989b6ad2040a)
- [CREATE CLUSTER GROUP](../part-03-sql-manual/19-sql-references-c-g.md#6ad165b04482545a)

- Creating the database: It is performed on each node.

```
% gcreatedb --cluster --db_name='goldilocks' --member='g1n1' \
    --host='192.168.0.11' --port 10110
% gcreatedb --cluster --db_name='goldilocks' --member='g1n2' \
    --host='192.168.0.12' --port 10120
```

- Creating a cluster group and a member: It is performed on a single node. The startup phase of the cluster member to be created or added must be GLOBAL OPEN.

```
gSQL> create cluster group g1 cluster member g1n1 
        host '192.168.0.11' port 10110;
gSQL> alter cluster group g1 add cluster member g1n2 
        host '192.168.0.12' port 10120;
```

If the configuration of the GOLDILOCKS cluster system is completed as described above, the entire cluster system can be started or shut down using the following two methods:

- Accessing each member node to start or shut down nodes one by one
    - Use the `\`startup and `\`shutdown commands.
- Starting or shutting down all member nodes at once from a single node 
    - Connect through gsqlnet, and then use the `\`cstartup and `\`cshutdown commands.

The following is an example of starting up the cluster system by accessing each member node according to the first method described above. The `\`startup command is used to directly enter the LOCAL OPEN phase without intermediate phases, but it can also be performed in three separate phases: `\`startup nomount, alter system mount database, and alter system open local database.

Start up to LOCAL OPEN phase on each node using `\`startup, and then access a single node and proceed up to GLOBAL OPEN phase.

- Start up to LOCAL OPEN: This is performed on each member node.

```
% gsql sys gliese --as sysdba
  gSQL> \startup
  Startup success.
```

- Start up to OPEN: This is performed on a single node.

```
% gsql sys gliese --as sysdba
  gSQL> alter system open global database;
  System altered.
```

When the number of nodes in the cluster system is large, using the first method described above to perform the startup can be burdensome for the operator. This is because, after the cluster system is shut down and restarted, the LOCAL OPEN process must be performed on each member node individually. For operational convenience, you can use the following simpler method to start up all members at once.

- Start up to GLOBAL OPEN: This is performed on a single node.

```
% gsqlnet sys gliese --as sysdba
gSQL> \cstartup
Startup success.
```


> 
> - The `\`cstartup and `\`cshutdown commands can be performed only in gsqlnet, and are not supported in gsql. Additionally, the listener must be started on every member node beforehand. 
> 
> 
> 
> - To build a GOLDILOCKS cluster system with multiple members on a single physical node, ensure that the home directory, member name, and cluster port information are unique for each database created.
> 

When the GOLDILOCKS system is shut down, gmaster, the management daemon process, terminates on each member node, preventing any further connections or database operations.

> ABORT is the only shutdown mode available when terminating a single node in the GOLDILOCKS cluster system. The ABORT mode immediately terminates gmaster regardless of the state of connected sessions and unloads the instance.

If the `\`shutdown command is executed using gsql as follows, only the connected member node is terminated.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown abort

Shutdown success

gSQL>
```

To terminate all members of the cluster system at once, use the `\`cshutdown command in gsqlnet as follows. The normal option can be omitted.

```
% gsqlnet sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \cshutdown normal

Shutdown success

gSQL>
```

> Using the abort option with the `\`cshutdown command forcibly terminates the entire member node. Consequently, some member nodes might fail to rejoin the cluster system when restarting with `\`cstartup. While failed nodes can be rejoined through the following join commands and rebalance process, it is recommended to use `\`cshutdown normal for a safer termination method.

To terminate and restart a member node or several member nodes in the cluster system, follow the process below. The following describes how to restart only the G1N2 node among the cluster member nodes then make it rejoin the cluster system.

```
% gsql sys gliese --as sysdba --dsn=g1n2

Connected to GOLDILOCKS Database.

gSQL> \shutdown abort

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

System altered.
```

To restart a member node and make it rejoin cluster system, a rebalancing operation for any altered tables may be required if the corresponding node was terminated while a transaction was in progress. If the rebalancing operation is not performed, transactions on the driver node may fail to alter the table if the rebalancing has not been completed.

A rebalancing operation is a process that synchronizes the data distribution policy and property information of tables among member nodes and redistributes the table data across each member node according to the data distribution policy.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown abort

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

ERR-42000(16405): some tables in the database need to be rebalanced
System altered.

gSQL> alter database rebalance;

Database altered.
```

<a id="925da0f781d13faf"></a>
## Installing GOLDILOCKS and Creating Database

Installing and creating a member database to be included in the GOLDILOCKS cluster system is nearly identical to the process used for standalone systems. This chapter describes only the unique features and methods for installing and creating databases in a cluster system, as compared to a standalone system.

<a id="59127184d8c36264"></a>
### Configuring GOLDILOCKS Package

The package used to configure the GOLDILOCKS cluster system is the same as that used for standalone databases. However, the scripts for building the dictionary and performance views are divided into separate scripts for standalone systems and cluster systems. Therefore, users must select the appropriate script to build the necessary information after creating the database.

The script for standalone database is located under the *$GOLDILOCKS_HOME/admin/standalone *directory, while the script for cluster systems is located under the* $GOLDILOCKS_HOME/admin/cluster *directory.

**admin/ standalone directory**

<a id="61dbe5b83f4d3fee"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| DictionarySchema.sql | It is the dictionary schema creation script. |
| InformationSchema.sql | It is the information schema creation script. |
| PerformanceViewSchema.sql | It is the PerformanceView schema creation script. |

**admin/ cluster directory**

<a id="4e3c1e6a4cfb749c"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| DictionarySchema.sql | It is the dictionary schema creation script. |
| InformationSchema.sql | It is the information schema creation script. |
| PerformanceViewSchema.sql | It is the PerformanceView schema creation script. |

**admin/ packages directory**

<a id="98a2ccd26789dec4"></a>
| File name | Server | Client | Description |
| --- | --- | --- | --- |
| DBMS_LOCK.sql | O | X | DBMS_LOCK package creation script |
| DBMS_OUTPUT.sql | O | X | DBMS_OUTPUT package creation script |
| DBMS_SQL.sql | O | X | DBMS_SQL package creation script |
| DBMS_STANDARD.sql | O | X | DBMS_STANDARD package creation script |

<a id="e10fbf95877c7ce1"></a>
### Installing GOLDILOCKS Software

The GOLDILOCKS software must be installed on every member node in the cluster system, following the same installation method as for standalone systems. The methods for setting and checking kernel parameters and environment variables are also the same as those for standalone systems. Refer to the corresponding tutorial for these procedures.

In this case, the property settings for each cluster member node, including the database name, database version, character set, and time zone, must be identical to properly configure the cluster system.

<a id="6cb830edff293504"></a>
### Creating Database

Use the gcreatedb utility to create a database on each member node, configuring the cluster system as if it were a standalone system.

The following options for gcreatedb are used only when creating a cluster database. Other options are the same as those used for standalone systems.

**Execution arguments for gcreatedb**

<a id="b27b0674ab7b554d"></a>
| Argument | Description |
| --- | --- |
| --cluster | It specifies that the database being created is a cluster database. If this argument is omitted, a standalone database will be created. |
| --member | It specifies the member name of the local database to be used in the cluster system. If this argument is omitted, it will use the value set in the LOCAL_CLUSTER_MEMBER property. |
| --host | It defines the IP address of the local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | It specifies the TCP listen port of the local member for communication between cluster system members. If it is omitted, it will use the value set in the LOCAL_CLUSTER_MEMBER_PORT property. |

The following is an example of creating a database to be used in a cluster system:

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

<a id="a48e953dd9e9c801"></a>
### Building Dictionary Schema Information

Like in a standalone system, the dictionary schema information must be built to use the cluster system properly. If the following schema is not built, the catalog API (e.g. the SQLTables() function) of ODBC and JDBC, which retrieves object structure information, may malfunctions and fail to interoperate with third-party tools. In conclusion, it is essential to build the schema after creating the database.

It is recommended to build the schema in the cluster system after completing the creation of a cluster group and its members. It is because GOLDILOCKS automatically creates the schema on every member node when running the creation script by connecting to a member node, after the cluster system configuration is complete.

- DICTIONARY_SCHEMA: It consists of tables and views that query object information such as DBA_*, ALL_*, USER_*.
- INFORMATION_SCHEMA: It consists of tables and views included in the SQL standard INFORMATION_SCHEMA.
- PERFORMANCE_VIEW_SCHEMA: It consists of views that query system information by combining data from fixed tables.

The following describes how to build the schema using the script for the cluster system. Perform the operation by accessing a single member node during the GLOBAL OPEN phase, as described above.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

Various structural information of the cluster system can be viewed using the schema information built above. The difference from a standalone system is that a user can extract information from only the desired node by specifying the group and member names after the object when querying.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N1               PLAN_CACHE_TOTAL_SIZE   17844952
G2N2               PLAN_CACHE_TOTAL_SIZE   16796288
G2N1               PLAN_CACHE_TOTAL_SIZE   16796288
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288
G3N1               PLAN_CACHE_TOTAL_SIZE   16796288
G3N2               PLAN_CACHE_TOTAL_SIZE   16796288

6 rows selected.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat@g1n2
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288

1 row selected.

gSQL> select origin_member_name, stat_name, stat_value
    2   from gv$system_mem_stat@g1
    3  where stat_name = 'PLAN_CACHE_TOTAL_SIZE';

ORIGIN_MEMBER_NAME STAT_NAME             STAT_VALUE
------------------ --------------------- ----------
G1N1               PLAN_CACHE_TOTAL_SIZE   17844952
G1N2               PLAN_CACHE_TOTAL_SIZE   16796288

2 row selected.
```

The following describes how to create a package to use a built-in package.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="f2791da5eafd203b"></a>
## Managing Schema Object

A schema object is a logical structure created by a user. The GOLDILOCKS cluster system supports schema objects such as tables, indexes and global sequences. This chapter describes the features of each schema object in the cluster system compared to a standalone system and also explains how to manage them efficiently.

<a id="55f3218018bcbc51"></a>
### Managing Table

A user can specify one of the following four sharding strategies as an option when creating a table in the GOLDILOCKS cluster system. The sharding strategy determines how table data is distributed and stored across each cluster group in the system. This option is available only in the cluster system and cannot be used when the database is created in standalone mode.

- Cloned strategy
    - It equally copies the entire table data.
- Hash sharding strategy
    - It distributes table data based on the hash value of the sharding key.
- Range sharding strategy
    - It distributes table data based on the range value of the sharding key.
- List sharding strategy
    - It distributes table data based on a list values for the sharding key.

For more information about creating tables, refer to [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#47f3ce328094503e) and [Cluster Table and Shard](../part-03-sql-manual/14-cluster-objects.md#e56d5d1087eefb48).

When the sharding strategy option is omitted, it is defined by the [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#b42b1ed9a19b2182) property. The default value of DEFAULT_SHARDING is 0, and which creates a cloned table.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

If a table is created by a user without specifying a sharding strategy, as described above, the GOLDILOCKS cluster system internally creates the table using the following syntax:

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
)
    CLONED
    AT CLUSTER WIDE
;
```

> For tables with Hash, Range, or List sharding, the following constraints must be observed when creating constraints:   
> - The PRIMARY KEY and UNIQUE constraints must include the sharding key.

<a id="ac7718ce7683e0a5"></a>
#### Cloned Strategy

It does not distribute the table data based on specific conditions; instead, it copies all the data. The data can be copied to all nodes in the cluster system or to a specific cluster group. In other words, it arranges clones across the cluster members of the defined cluster group.

- AT CLUSTER WIDE 
    - It arranges clones across all cluster members in all cluster groups within the cluster system.
    - When adding a cluster group or cluster member, a user can rearranges clones using the [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#f207258645781242) statement. 
- AT CLUSTER GROUP group_list 
    - It arranges clones across all cluster members within the defined cluster group.
    - When adding a cluster member to a defined cluster group, a user can rearranges clones using the [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#f207258645781242) statement. 
    - Adding a cluster group does not affect the rearrangement of clones.

When the option is omitted, the default value is automatically set to *AT CLUSTER WIDE*.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
) 
CLONED 
AT CLUSTER WIDE;
```

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
) 
CLONED 
AT CLUSTER GROUP G1, G2;
```

<a id="2b4cf1bf599707f2"></a>
#### Hash Sharding Strategy

It distributes the table data based on the hash value of a column defined as the sharding key.

To use the hash sharding strategy, the sharing key must be defined complying with the following conditions:

- Up to 32 columns can be listed.
- Duplicated columns can not be used.
- Columns of type LONG VARCHAR or LONG VARBINARY can not be used.

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id);
```

When hash sharding-related options are omitted as described above, the GOLDILOCKS system interprets it as follows:

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

Table rows are distributed to one of 24 shards based on the hash value of the id column, and 24 shards are evenly distributed across the entire cluster system. For more information, refer to [Cluster Table and Shard](../part-03-sql-manual/14-cluster-objects.md#e56d5d1087eefb48).

<a id="f15be6eb1e2561e8"></a>
#### Range Sharding Strategy

It distributes the table data based on the range value of the column defined as the sharding key. The shards are classified according to each range value and can be arranged either by defining a specific group or as CLUSTER WIDE.

The following is the syntax of defining six range shards based on the range value of the sharding key column and creating a table that distributes them as CLUSTER WIDE. If a cluster group is created after the table has been created, the rearrangement of shards to include the created group can be performed using the REBALANCE feature.

- Create a range sharded table.
- Arrange six shards across the existing cluster groups (g1, g2, g3).

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    AT CLUSTER WIDE
    SHARD s1 VALUES LESS THAN ( 200000 ),
    SHARD s2 VALUES LESS THAN ( 400000 ),
    SHARD s3 VALUES LESS THAN ( 500000 ),
    SHARD s4 VALUES LESS THAN ( 600000 ),
    SHARD s5 VALUES LESS THAN ( 800000 ),
    SHARD s6 VALUES LESS THAN ( MAXVALUE )
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Rearrange the range shards.
- Rearrange the six shards across the cluster groups (g1, g2, g3, g4), including the newly added group.

```
ALTER TABLE t1 REBALANCE;
```

The following syntax defines range shards based on the range of the sharding key column values, specifically arranged within defined cluster groups. In other words, shard s1, with a range value smaller than 200,000, is allocated to cluster group g1; shard s2 is allocated to g2; and shard s3 is allocated to g3. Shards arranged in this manner cannot be rearranged using the REBALANCE feature, even if a cluster group is added later, in a table created with predefined cluster groups.

- Create a range sharded table.
- Allocate each range shard to the defined cluster groups.

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    SHARD s1 VALUES LESS THAN ( 200000 )   AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( 400000 )   AT CLUSTER GROUP g2,
    SHARD s3 VALUES LESS THAN ( 500000 )   AT CLUSTER GROUP g3,
    SHARD s4 VALUES LESS THAN ( 600000 )   AT CLUSTER GROUP g2,
    SHARD s5 VALUES LESS THAN ( 800000 )   AT CLUSTER GROUP g3,
    SHARD s6 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g1
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Rearrange the range shards.
- The shard is not allocated to the newly created cluster group (g4).

```
ALTER TABLE t1 REBALANCE;
```

The following conditions must be considered when specifying the range sharding key.

- Up to 32 columns can be listed.
- Duplicated column can not be used.
- Columns of type LONG VARCHAR or LONG VARBINARY can not be used.

<a id="f61c2804ed2bd7bc"></a>
#### List Sharding Strategy

It distributes the table data based on the list value of the column defined as the sharding key. Like as with the range sharding strategy, each shard can be arranged either by defining a specific group or as CLUSTER WIDE.

The following are the conditions for defining the shard key in the list sharding strategy.

- Only a single column can be used.
- Columns of type LONG VARCHAR or LONG VARBINARY can not be used.

The following is a syntax of creating a table where the generated list shards are arranged as CLUSTER WIDE. To rearrange the shards to include any additional cluster groups created after the table is created, use the REBALANCE feature.

- Create a list sharded table.
- Arrange the five shards across the existing cluster groups (g1, g2, g3).

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    AT CLUSTER WIDE
    SHARD s1 VALUES IN ( 'SEOUL' ),
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ),
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' ),
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' ),
    SHARD s5 VALUES IN ( DEFAULT )
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Rearrange the list shards.
- Rearrange the five shards across the cluster groups (g1, g2, g3, g4), including the newly created group (g4).

```
ALTER TABLE city REBALANCE;
```

The following syntax defines list shards based on the list values of the sharding key column value, arranged specifically within defined cluster groups. Shards can not be rearranged using the REBALANCE feature, even if a new cluster group is created.

- Create a list sharded table.
- Allocate each list shard to the defined cluster groups.

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    SHARD s1 VALUES IN ( 'SEOUL' )                   AT CLUSTER GROUP g1,
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ) AT CLUSTER GROUP g2,
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' )      AT CLUSTER GROUP g3,
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' )         AT CLUSTER GROUP g2,
    SHARD s5 VALUES IN ( DEFAULT )                   AT CLUSTER GROUP g1
;
```

- Create a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Rearrange the list shards.
- The shard is not allocated to the newly created cluster group (g4).

```
ALTER TABLE city REBALANCE;
```

<a id="7376d77dd9f21db2"></a>
### Managing Index

<a id="1aeb5ae206fa809c"></a>
#### Global Secondary Index

In a cluster system, multiple member nodes exist, and table records are stored either in partitions or duplicated based on the sharding strategy. In a standalone system, uniqueness of a record is guaranteed by storing a unique value (Row Identifier: RID) in the database. However, in a cluster system, each node may have duplicated values, so uniqueness can not be guaranteed across the entire cluster.

Therefore, ensuring the uniqueness of a record in a cluster system is essential. This is why a global RID (GRID) is introduced. The GRID value of a record remains unchanged even when the record is updated, thereby guaranteeing the uniqueness of a specific record across the cluster system.

A global secondary index is a B-tree index that consists of keys to quickly search for the GRID values of records in a cluster system.

A user can choose whether to create a global secondary index using the following properties when creating a table. The user also can delete or recreate the global secondary index after the table has been created. Only one global secondary index can be created per table.  
For more information, refer to [DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION](../part-02-administration-manual/10-server-property.md#f521d98b5f13c26a).

A global secondary index is necessary to perform non-deterministic queries on a table. If a global secondary index does not exist for the table, the non-deterministic query will fail as follows.

```
gSQL> DELETE FROM T1 LIMIT 1;

ERR-42000(16423): does not support non-deterministic DML in the cluster system : global secondary index expected
```

To check if a global secondary index has been created for a table, query the USER_GSI_PLACE dictionary, or use the ALL_GSI_PLACE and DBA_GSI_PLACE dictionaries.

```
gSQL> CREATE TABLE T1( I1 INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT * 
    2   FROM USER_GSI_PLACE@LOCAL
    3  WHERE TABLE_NAME = 'T1';

TABLE_SCHEMA TABLE_NAME GROUP_ID GROUP_NAME MEMBER_ID MEMBER_NAME MEMBER_OFFLINE
------------ ---------- -------- ---------- --------- ----------- --------------
BLOCKS
------
PUBLIC       T1                1 G1                 1 G1N1        FALSE         
    64
PUBLIC       T1                1 G1                 2 G1N2        FALSE         
  null

2 rows selected.

gSQL> DROP TABLE T1;

Table dropped.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT * 
    2   FROM USER_GSI_PLACE@LOCAL
    3  WHERE TABLE_NAME = 'T1';

no rows selected.
```

<a id="3c6868a388280a2f"></a>
### Global Sequence

The GOLDILOCKS cluster system provides a global sequence object, an extension of the existing sequence, allowing multiple member nodes to share and use a set of sequence values according to user-defined conditions. In other words, a global sequence object is automatically created when a user creates a sequence in the cluster system. The sequence values within a specific range are allocated and used when calling NEXTVAL on each member node. The following syntax for creating and using the global sequence is the same as for sequences in standalone systems.

```
gSQL> CREATE SEQUENCE global_user_seq START WITH 1000 INCREMENT BY 1 NOCACHE NOCYCLE; 

Sequence created.

gSQL> SELECT global_user_seq.NEXTVAL FROM dual;

NEXTVAL
-------
      1

1 row selected.

gSQL> DROP SEQUENCE global_user_seq;

Sequence dropped.
```

Like as sequences in standalone systems, the global sequence object allows you to define a cache size as a creation option. This means that several sequence values are acquired from the global sequence object and loaded into the local cache. The following describes the local cache status of each member node and the return values when calling NEXTVAL, with the global sequence object created with a cache size set to 5.

```
gSQL> CREATE SEQUENCE seq START WITH 1 CACHE 5; 

Sequence created.
```

<a id="961832890f3a6a78"></a>
<table class="table column_count_5"><caption> </caption><thead><tr><th class="to_center to_middle" rowspan="2"><div>Member name</div></th><th class="to_center to_middle" rowspan="2"><div>NEXTVAL result</div></th><th class="to_center" colspan="2"><div>The number of remaining 
sequence values in the local cache</div></th><th class="to_center to_middle" rowspan="2"><div>Description</div></th></tr><tr><th class="to_center"><div>G1N1</div></th><th class="to_center"><div>G1N2</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 1 ~ 5)</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>6</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 6 ~ 10)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>7</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>8</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>9</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>10</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>11</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 11 ~ 15)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>12</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>5</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>16</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 16 ~ 20)</div></td></tr></tbody></table>

In the table above, the sequence values are allocated twice each to G1N1 and G1N2 (a total of four times) from the global sequence object. Since the cache option is set to 5 when creating the sequence, five sequence values are allocated from the global sequence object to each member node. These five sequence values are stored in the local cache of each member node and are returned one by one whenever NEXTVAL is called.

- G1N1
    - The values of five sequences (1~5) are allocated from the global sequence object when calling the first NEXTVAL.
    - A single sequence is returned as a result of NEXTVAL, and the values of other four sequences are loaded into its own local cache.
    - NEXTVAL called later returns in turn the values of the sequences loaded in the local cache.
- G1N2
    - The values of sequences (6~10) which follows the sequences allocated on G1N1 are allocated when calling the first NEXTVAL.
    - 6 is returned as a result of NEXTVAL, and the values of the other four sequences (7~10) are loaded into its own local cache.
    - NEXTVAL called later returns the sequence values loaded in the local cache.
    - When the local cache is exhausted, values of other five sequences (11~15) are allocated again from the global sequence object. 
- G1N1
    - When the local cache is exhausted, the values of five sequences (16~20) following the sequences allocated last on G1N2 are allocated.

Sequences as large as the CACHE size are allocated to all member nodes when NEXTVAL has never been called on a node or when all allocated values on that node are exhausted. Therefore, to ensure quick acquisition of sequence values, it is important to set an appropriate cache size when creating a sequence. This helps prevent frequent allocation, which can be costly due to network communication overhead associated with fetching sequences from the global sequence object, unlike in a standalone database.

The sequence values loaded in the local cache cannot be reused if the database restarts due to a system error or operational maintenance. When NEXTVAL is called for the first time after a restart, new sequence values are allocated from the global sequence object. Consequently, the CACHE size set when creating the sequence also represents the range of sequence values that could potentially be lost in the event of an error. Therefore, the cache size should be set appropriately, taking into account both the feature's requirements and the potential loss range.

The result value of calling NEXTVAL from a specific node may not be sequential in a cluster system. In the example above, when the G1N1 node calls NEXTVAL, the returned values are not sequential. After the initial allocated range (1~5) is exhausted, the next allocated range (16–20) is used, so 16 is returned to a user as the next sequence value after 5. This occurs because a single global sequence pool is allocated competitively among multiple nodes.

The following are the features and constraints of the global sequence object, compared to sequences in existing standalone databases.

- The sign can not be modified using the INCREMENT BY option in the ALTER SEQUENCE statement (though the size can be modified).
- When using the CYCLE option, duplicated values among member nodes may be returned depending on the pool size of the entire sequence. Therefore, create a sufficiently large sequence pool by considering INCREMENT BY, CACHE SIZE, and the number of cluster member nodes when the CYCLE option is required.
- The return values from a specific node may not be sequential even in the absence of errors. However, if only one member node calls NEXTVAL, sequential sequence values will be obtained.
- For NOCACHE, the CACHE SIZE is set to 1, meaning no additional sequence values are loaded into the local cache. In this case, only one sequence value is allocated from the global sequence object with each NEXTVAL call, increasing network cost and degrading performance.
- Creating, updating and deleting sequences operate with AUTO COMMIT.
- All sequence values loaded into the local cache of all nodes are reset when the size of CACHE or INCREMENT is updated by the ALTER statement. In other words, a new sequence set must be allocated from the global sequence object for subsequent NEXTVAL calls.

<a id="5c646df32aaf29aa"></a>
## GOLDILOCKS Property

The following are the main properties used in the GOLDILOCKS cluster system.

**Main properties of GOLDILOCKS**

<a id="978584829374cb49"></a>
| Name | Description |
| --- | --- |
| LOCAL_CLUSTER_MEMBER | Member name |
| LOCAL_CLUSTER_MEMBER_HOST | Host address for connecting to the cluster session |
| LOCAL_CLUSTER_MEMBER_PORT | Port for connecting to the cluster session |
| CDISPATCHER_THREADS | The number of cluster dispatcher threads |
| CSERVERS | The number of cluster server process |
| CLUSTER_DATA_SYNC_SERVERS | The number of cluster server processes dedicated to synchronizing replica data. |

Each property in the GOLDILOCKS cluster system has the following two alterable scopes:

- LOCAL: It can alter property values for either the all members or a specific member only.
- GLOBAL: It alters the property value for all members in the cluster system, and cannot be used to change the value for a specific member only.

For example, the PRIVATE_STATIC_AREA_SIZE property can be altered within the LOCAL scope (IS_GLOBAL column = FALSE) as follows. This means the property value can be modified using the alter system set statement for either the all members or a specific member only. If the AT clause is not included after the alter system set statement, the altered properties will apply to all members of the cluster system.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    

2 rows selected.

gSQL> alter system set private_static_area_size = 200000000 at g1n2;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 104857600      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 200000000      FALSE    

2 rows selected.

gSQL> alter system set private_static_area_size = 300000000;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'PRIVATE_STATIC_AREA_SIZE';

ORIGIN_MEMBER_NAME PROPERTY_NAME            PROPERTY_VALUE IS_GLOBAL
------------------ ------------------------ -------------- ---------
G1N1               PRIVATE_STATIC_AREA_SIZE 300000000      FALSE    
G1N2               PRIVATE_STATIC_AREA_SIZE 300000000      FALSE    

2 rows selected.
```

However, the DDL_AUTOCOMMIT property can only be altered within the GLOBAL scope as follows. Therefore, specifying a member using the AT clause in the ALTER SYSTEM SET statement will result in an error.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'DDL_AUTOCOMMIT';

ORIGIN_MEMBER_NAME PROPERTY_NAME  PROPERTY_VALUE IS_GLOBAL
------------------ -------------- -------------- ---------
G1N1               DDL_AUTOCOMMIT NO             TRUE     
G1N2               DDL_AUTOCOMMIT NO             TRUE     

2 rows selected.

gSQL> alter system set ddl_autocommit = false at g1n2;

ERR-42000(16398): the domain of property does not match with domain 'G1N2' : 
alter system set ddl_autocommit = false at g1n2
                                           *
ERROR at line 1:

gSQL> alter system set ddl_autocommit = false;

System altered.

gSQL> select origin_member_name, property_name, property_value, is_global
    2   from gv$property
    3  where property_name = 'DDL_AUTOCOMMIT';

ORIGIN_MEMBER_NAME PROPERTY_NAME  PROPERTY_VALUE IS_GLOBAL
------------------ -------------- -------------- ---------
G1N1               DDL_AUTOCOMMIT NO             TRUE     
G1N2               DDL_AUTOCOMMIT NO             TRUE     

2 rows selected.
```

---

[← 2. Tutorial](2-tutorial.md) · [Table of contents](../README.md) · [4. What's New →](4-what-s-new.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
