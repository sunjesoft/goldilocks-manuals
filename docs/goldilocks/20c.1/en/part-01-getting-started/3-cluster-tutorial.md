<a id="8de1791c0b9103de"></a>

# 3. Cluster Tutorial

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/8de1791c0b9103de)  
> Tag: `20c.1_30_tag`

[← 2. Tutorial](2-tutorial.md) · [Table of contents](../README.md) · [4. What's New →](4-what-s-new.md)

<a id="a9d6de7669607fd5"></a>
## Managing GOLDILOCKS Cluster System

This chapter describes the basic information for configuring and managing the cluster system by using multiple GOLDILOCKS databases. Only the parts added to the cluster system or distinguishing the cluster system comparing to the standalone database are described in this chapter, so it is prerequisite to read the standalone database tutorial before read this chapter.

<a id="7076d4320aa40424"></a>
### Overview

GOLDILOCKS can be used by configuring a standalone database as described in the previous chapter. Or, a user can also bind multiple databases into a single cluster, then select an appropriate solution for data distribution. In other words, a user can customize how to distribute massive data to multiple servers when using GOLDILOCKS cluster system. This guarantees high availability and improves the throughput due to the parallel processing.

GOLDILOCKS cluster system consists of one or more cluster groups, and a cluster group consists of one or more cluster members. It does not require an extra application server or a meta server. Applications are operated accessing to cluster members corresponding to the data server. Cluster members belonging to the same cluster group keeps the same data replication.

A user should determine whether to use GOLDILOCKS database as standalone system or as cluster system, when creating database of each node. To use it as cluster system, a user should add options related to cluster when creating database of each node.

<a id="e160f0d2cf84015b"></a>
### Property Setting

Properties to build cluster system are described in *$GOLDILOCKS_DATA/conf/goldilocks.property.conf* file of each server as like when using standalone database. Main properties for TBS (tablespace), LOG, CONTROL FILE can be set as same as setting in standalone system even when using cluster system. However, there should not be the same path or port of files among cluster members when creating multiple databases to configure cluster system in a single server.

The followings describe main property items of when configuring cluster system.

**Main property items**

<a id="da86a35d0c0f23a0"></a>
| Property | Description | Default value |
| --- | --- | --- |
| SYSTEM_TABLESPACE_DIR | It is the directory path of installing the following system TBS. * DICTIONARY_TBS * MEM_DATA_TBS * MEM_UNDO_TBS * MEM_TEMP_TBS * MEM_TRANS_TBS | ‘&lt;GOLDILOCKS_DATA&gt;/db’ |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | It is the dictionary tablespace size. | 256M |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | It is the data tablespace size. | 200M |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | It is the undo tablespace size. | 32M |
| LOG_DIR | It is the default log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/wal’ |
| SYSTEM_LOGGER_DIR | It is the system log directory path. | ‘&lt;GOLDILOCKS_DATA&gt;/trc’ |
| CONTROL_FILE_COUNT | It is the number of control files. | 2 |
| CONTROL_FILE_0 | It is the first control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl' |
| CONTROL_FILE_1 | It is the second control file path. | '&lt;GOLDILOCKS_DATA&gt;/wal/control_1.ctl' |
| LOCAL_CLUSTER_MEMBER | It is the name of cluster member of which local server uses in cluster system. | ‘G1N1’ |
| LOCAL_CLUSTER_MEMBER_HOST | It is the host name of local server. | '127.0.0.1' |
| LOCAL_CLUSTER_MEMBER_PORT | It is TCP listen port of which local server uses for the communication in cluster system. | 10101 |

The name of cluster member and host-port combination should be unique in cluster system. To omit the property setting above, provide information by using *--member, --host, --port* options when creating database using gcreatedb. The member information provided by property or gcreatedb option is stored and managed in *$GOLDILOCKS_DATA/wal/location.ctl* file.

To modify the properties, update the text property file (*$GOLDILOCKS_DATA/conf/goldilocks.properties.conf*), or define a new variable in a form of *GOLDILOCKS_&lt;property_name&gt;* in an environment variable. The property file is prior to the environment variable.

<a id="5904dcae4a23ee9a"></a>
### Background Process

GOLDILOCKS cluster system has the background process (gmaster) to manage instances per each member node. gmaster of each node consists of multiple system threads internally. Most of them are as same as those in standalone system, but the following system threads are added to manage cluster system.

The following threads are performed only when starting the database created as cluster mode.

- Cluster recover thread: It recovers global transaction in cluster system.
- Failover thread: It deals with the failover through reselecting offiline and coordinator for the members when an error occurs on a specific node or in a network in cluster system.

Two following processes are additionally driven when using GOLDILOCKS as cluster system.

- cdispatcher: It transmit/receive cluster packet and manages sessions.
- cserver: It performs operation of modifying and querying for the database to which the member node belongs.

GOLDILOCKS cluster system requires complex cluster protocol communication among member nodes, and cluster dispatcher (cdispatcher) is a process to efficiently perform the management of network communication context and packet distribution mechanism. In addition, it performs monitoring continuously the validity of cluster session through heartbeat.

In cluster system, SQL performing in a specific node (driver node) needs to store data on the remote member node by referring to the sharding strategy of the target table or enquires the data stored in the corresponding node. In this case, a process is required to process this request and return the result in each member node, and that process is cserver.

<a id="dfd9a9f94ad28a54"></a>
### Client Process

A user can use both client server (C/S) model and direct access (D/A) model in cluster system as like standalone system. However, each member node of cluster system has its own listener, so the client program should know the listen port of the cluster member to access beforehand (in C/S mode). A user can process various transactions when accessing to any node of cluster system as like standalone database.

Signal handling, cleanup for connection, releasing shared resources in cluster system are processes as same as those in standalone system.

<a id="051e44cb317f4433"></a>
### Memory Structure of Instance

GOLDILOCKS cluster system is used to bind multiple shared-nothing databases to a management unit which is a single cluster system. Therefore, a method of using memory of cluster member nodes is similar to that of standalone. The memory size of which each member node uses are determined by properties set in its own property. Static area contains instance basic information for database management, information for each session, statement, transaction, redo log buffer, dictionary cache, and other operational information as like standalone system. Additionally, information for management of cluster session such as information for location and cluster session are also stored.

Tablespace area consists of page frames and page control header (PCH). The page frame contains the contents of each tablespace and PCH controls those page frames.

The application process memory contains instance memories attached when connecting, ODBC environment shared in process unit, various ODBC handles and heap memory area containing other information such as bind information.

<a id="9040f21ba0ec1244"></a>
### Start and End of Cluster System

To start GOLDILOCKS system, create instance on each member node beforehand (gcreatedb), and then register cluster group and cluster member. Later, a user can start or end the system by using sysdba role through gsql and gsqlnet.

[listener](../part-06-utility-manual/36-glsnr.md#0fd87486f960aa01) should be in operation if a user wants to start or end GOLDILOCKS cluster system in dedicated mode of C/S model(to use gsqlnet).

GOLDILOCKS cluster system can not be started or ended in the shared mode of C/S model.

```
% gsql --as sysdba

Enter user-name: sys
Enter password: 

Connected to an idle instance.

gSQL>
```

GOLDILOCKS cluster system has the following startup phases. OPEN phase is subdivided into LOCAL OPEN and GLOBAL OPEN unlike the standalone system.

- NOMOUNT
    - It launches gmaster which is a demon to manage GOLDILOCKS instance.
- MOUNT
    - It reads properties, and the control file for the recovery by using $GOLDILOCKS_DATA environment variable.
- LOCAL OPEN
    - It loads tablespace content from data files, then performs recovery by using the redo log files, and recovers in-doubt global transaction, newly build no-logging indexes, and creates dictionary caches.
- OPEN (GLOBAL OPEN)
    - It connects cluster sessions of each cluster member, arranges shard map, selects a global manager ( global coordinator) and a group manager (group coordinator), then waits for the user to access the service.

To start or end the GOLDILOCKS cluster system the cluster system environment should be configured performing the following preliminary works. If the member name, host address, port number are uniquely given when creating each member database by using gcreatedb, the property setting process for each node can be omitted.

- Setting property: Update property files to be used on each member node. 
- Creating database: Create the database through gcreatedb on each member node.
- Creating cluster group and adding a member: Create a group and a member configuring cluster system.
- Driving listener: The listner on each node should be driven beforehand to use gsqlnet.

Use the following syntaxes to create a cluster group or a member.

- [ALTER CLUSTER GROUP name ADD MEMBER](../part-03-sql-manual/18-sql-references.md#619c417c530cdf9a)
- [CREATE CLUSTER GROUP](../part-03-sql-manual/18-sql-references.md#77c1869df568145d)

• Creating database: It is performed on each node.

```
% gcreatedb --cluster --db_name='goldilocks' --member='g1n1' \
    --host='192.168.0.11' --port 10110
% gcreatedb --cluster --db_name='goldilocks' --member='g1n2' \
    --host='192.168.0.12' --port 10120
```

• Creating a cluster group and a member: It is performed on a single node. The startup phase of the cluster member to be created or added should be GLOBAL OPEN.

```
gSQL> create cluster group g1 cluster member g1n1 
        host '192.168.0.11' port 10110;
gSQL> alter cluster group g1 add cluster member g1n2 
        host '192.168.0.12' port 10120;
```

If the configuration of GOLDILOCKS cluster system is completed as above, the entire cluster system can be started or ended by using the following two methods.

- Accessing to each member node to start or end nodes one by one
    - Use `\`startup and `\`shutdown commands.
- Start or end the entire member node at once in a single member node 
    - Connect through gsqlnet, and then use `\`cstartup and `\`cshutdown commands.

The following describes the first method above which is how to access each member node then drive cluster system. `\`startup command is used to directly enter into LOCAL OPEN phase without the intermediate phase. This can be operated being subdividing into three phases, which are `\`startup nomount, alter system mount database, and alter system open local database.

Drive up to LOCAL OPEN phase on each node through `\`startup, and then access a single node and drive up to GLOBAL OPEN phase.

• Startup up to LOCAL OPEN: It is performed on each member node.

```
% gsql sys gliese --as sysdba
  gSQL> \startup
  Startup success.
```

• Startup up to OPEN: It is performed on a single node.

```
% gsql sys gliese --as sysdba
  gSQL> alter system open global database;
  System altered.
```

Starting up with the first method can be a burden to an operator if many nodes are included in cluster system. It is because the entire process from end of cluster system to LOCAL OPEN should be performed everytime on every member node. The following is a simple method to startup the entire member for the ease of operation.

• Startup to GLOBAL OPEN: It is performed on a single node.

```
% gsqlnet sys gliese --as sysdba
gSQL> \cstartup
Startup success.
```


> 
> - `\`cstartup and `\`cshutdown commands can be performed only in gsqlnet, and it is not supported in gsql. Also, listener should be driven beforehand on every member node to be driven. 
> 
> 
> 
> - To build GOLDILOCKS cluster system containing multiple members on a single physical node, home directory name, member name and the cluster port information should not be duplicated when creating each database.
> 

When GOLDILOCKS system ends, gmaster, the management daemon process, ends on each member node, so it does not allow any more connection or other database operations.

The followings are two ending modes of GOLDILOCKS cluster system.

- NORMAL: It blocks an access of a new session, waits for the termination of all sessions, performs checkpoint, then unloads the instance.
- ABORT: It immediately terminates gmaster regardless of the state of connected sessions, and unloads the instance.

If `\`shutdown command is performed by using gsql as follows, only the connected member node is terminated.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL>
```

To terminate the entire member belonging to cluster system at once, use `\`cshutdown command of gsqlnet as follows. The normal option can be omitted.

```
% gsqlnet sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \cshutdown normal

Shutdown success

gSQL>
```

> Using abort option when performing `\`cshutdown, it terminates the entire member node by force. Therefore, some member nodes may fail to join cluster system when restarting it by using `\`cstartup. Although the failed nodes can join through the following join commands and rebalance process, it is recommended to terminate it by using `\`cshutdown normal which is a safe method.

To terminate and start a member node or some member nodes belonging to cluster system, follow the process below. The following describes how to restart only the G1N2 node among cluster member nodes then make it join cluster system.

```
% gsql sys gliese --as sysdba --dsn=g1n2

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

System altered.
```

To restart a member node and make it rejoin cluster system, rebalancing operation for the altered table may be required if the corresponding node is terminated when a transaction occurs. It the rebalancing operation is not performed, the transaction performing on a driver node may fail to alter the table on which the rebalaning is not performed.

A rebalancing operation is a process which synchronizes data distribution policy and property information of table among member nodes, and dividedly stores table data again in each member nodes according to the data distribution policy.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown normal

Shutdown success

gSQL> \startup

Startup success

gSQL> alter system join database;

ERR-42000(16405): some tables in the database need to be rebalanced
System altered.

gSQL> alter database rebalance;

Database altered.
```

<a id="707ffd85109eb5be"></a>
## Installing GOLDILOCKS and Creating Database

Installing and creating member database which is to be included in GOLDILOCKS cluster system is almost as same as those in standalone system. This chapter describes only the unique feature and method used for installing and creating database of cluster system comparing to standalone system.

<a id="08eb2f1a046ebe06"></a>
### Configuring GOLDILOCKS Package

The package used to configure GOLDILOCKS cluster system is as same as those of standalone database. However, the scripts to build dictionary and performance view are divided into the script for standalone system and the script for cluster system. Therefore, a user should use the appropriate script for the purpose to build the information after creating the database.

The script for standalone database is located below the *$GOLDILOCKS_HOME/admin/standalone *directory and the script for cluster system is located below the* $GOLDILOCKS_HOME/admin/cluster *directory.

**admin/ standalone directory**

<a id="0aea90fffda41aaf"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| DictionarySchema.sql | It is the dictionary schema creation script. |
| InformationSchema.sql | It is the information schema creation script. |
| PerformanceViewSchema.sql | It is the PerformanceView schema creation script. |

**admin/ cluster directory**

<a id="de4966a9e00ad198"></a>
| File name | Description |
| --- | --- |
| README | Read me |
| DictionarySchema.sql | It is the dictionary schema creation script. |
| InformationSchema.sql | It is the information schema creation script. |
| PerformanceViewSchema.sql | It is the PerformanceView schema creation script. |

<a id="69233704dc90136a"></a>
### Installing GOLDILOCKS Software

GOLDILOCKS software should be installed on every member node belonging to cluster system, and the installing method is as same as that of standalone system. The method for setting and checking kernel parameter, setting environment variable are as same as those of standalone system, so refer to the corresponding tutorial.

In this case, be cautious that setting properties for each cluster member node, database name, database version, character set, time zone should be same for the normal operation of cluster system.

<a id="c6e91d30ea5feffb"></a>
### Creating Database

Use gcreatedb utility to create database on each member node configuring cluster system as like standalone system.

The following options of gcreatedb are used only when creating cluster database. Other options are as same as standalone system.

**Execution arguments of gcreatedb**

<a id="a66b90e2350da1e6"></a>
| Argument | Description |
| --- | --- |
| --cluster | It represents that it is cluster database. When it is omitted, standalone database is created. |
| --member | The member name of local database to be used in cluster system. When it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER property. |
| --host | IP address of local member to be used for communication between cluster system members. If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_HOST property. |
| --port | TCP listen port of local member to be used for communication between cluster system members If it is omitted, it uses the value set in LOCAL_CLUSTER_MEMBER_PORT property. |

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

<a id="cb696f50972f2efe"></a>
### Building Dictionary Schema Information

To normally use cluster system, the dictionary schema information should be built as like standalone system. If the following schema is not built, the catalog API (e.g. SQLTables() function) of ODBC, JDBC obtaining object's structure information malfunctions, then it can not interwork with the third party tools. In conclusion, it should be built after creating database.

It is recommended to build schema in cluster system after completing the operation of creating a cluster group and a member. It is because GOLDILOCKS automatically creates schema on every member node when performing creation script by connecting to a member node after completing cluster system configuration.

- DICTIONARY_SCHEMA: It consists of tables and views inquiring object information such as DBA_*, ALL_*, USER_*.
- INFORMATION_SCHEMA: It consists of tables and views included in the SQL standard INFORMATION_SCHEMA.
- PERFORMANCE_VIEW_SCHEMA: It consists of views inquiring system information combining information of fixed tables.

The followings describe how to build schema by using the script for cluster system. Perform the operation by accessing to a single member node in GLOBAL OPEN phase as described above.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

Various structure information can be viewed by using the schema information built above. What is different from standalone system is that a user can extract only the desired node information by giving group name and member node after the object when inquiring the information.

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

<a id="c1efbbc8c5732d9d"></a>
## Managing Schema Object

The schema object is a logical structure created by a user. GOLDILOCKS cluster system supports the schema objects such as table, index and global sequence. This chapter describes features of each schema object in cluster system comparing to standalone system. How to efficiently manage them is also described.

<a id="443225ad6837c4f9"></a>
### Managing Table

A user can specifies one of four following sharding strategies as an option when creating a table in GOLDILOCKS cluster system. Sharding strategy is how to distribute and store table data to each cluster group in cluster system. This option can be specified only in cluster system, and it can not be used when database is created as standalone.

- Cloned strategy
    - It equally copies entire table data.
- Hash sharding strategy
    - It distributes table data based on the hash value of sharding key.
- Range sharding strategy
    - It distributes table data based on the range value of sharding key.
- List sharding strategy
    - It distributes table data based on the list value of sharding key.

For more information about creating table, refer to [CREATE TABLE](../part-03-sql-manual/18-sql-references.md#ddfa46214a0f4901) and [Cluster Table and Shard](../part-03-sql-manual/14-cluster-objects.md#65a46771a314ec47).

When omitting the sharding strategy option, it is defined by [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#94ad7bb7c7a05563) property. The default value of DEFAULT_SHARDING is 0, and it creates cloned table.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

If a table is created without giving the sharding strategy by as user as above, then GOLDILOCKS cluster system internally creates a table by using the following syntax.

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

> Hash/Range/List sharded table should comply with the followings when creating constraints.   
> - PRIMARY KEY, UNIQUE constraint should include the sharding key.

<a id="caf4d357c5bc524f"></a>
#### Cloned Strategy

It does not distribute the table data based on a specific condition, but it copies all data. The target of copying data can be all nodes in cluster system, or it can be a specific cluster group. In other words, it arranges clones in cluster members of a defined cluster group.

- AT CLUSTER WIDE 
    - It arranges clones in all cluster members of all cluster group in cluster system.
    - When adding a cluster group or cluster member, a user can rearranges clones by using [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references.md#2daa906aac739ab1) statement. 
- AT CLUSTER GROUP group_list 
    - It arranges clones in all cluster members of a defines cluster group.
    - When adding a cluster member to a defined cluster group, a user can rearranges clones by using [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references.md#2daa906aac739ab1) statement. 
    - Adding cluster group does not affect the rearrangement of clones.

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

<a id="64ba0433e0906e20"></a>
#### Hash Sharding Strategy

It distributes the table data based on the hash value of a column defined as a sharding key.

To use hash sharding strategy, sharing key should be defined complying with the following conditions.

- Up to 32 columns can be listed.
- The duplicated column can not be used.
- The column of LONG VARCHAR or LONG VARBINARY type can not be used.

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id);
```

When hash sharding related options are omitted as above, GOLDILOCKS system interprets it as follows.

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

Table rows are distributes to one of 24 shards based on hash value of id column, and 24 shards are equally arranged over the entire cluster system. For more information, refer to [Cluster Table and Shard](../part-03-sql-manual/14-cluster-objects.md#65a46771a314ec47).

<a id="053f31b02b8675d8"></a>
#### Range Sharding Strategy

It distributes the table data based on the range value of the column defined as a sharding key. The shards are classified based on each range value, and they can be arranged by defining a specific group, or arranged as CLUSTER WIDE.

The following is a syntax of defining six range shards based on the range value of the sharding key column, and creating a table to distribute them as CLUSTER WIDE. If a cluster group is created after creating a table, the rearrangement of shard containing the created group can be performed by using REBALANCE feature.

- Create a range sharded table.
- Arrange six shards in existing cluster groups (g1, g2, g3).

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

- Rearrange the range shard.
- Rearrange six shards in cluster groups (g1, g2, g3, g4) in which the added group is included.

```
ALTER TABLE t1 REBALANCE;
```

The following is a syntax of defining range shards, which are defined based on the range of sharding key column value, only to be arranged in a specific cluster group. In other words, the shard s1 whose range value is smaller than 200000 is allocated in cluster group g1, s2 is allocated in cluster group g2, and shard s3 is allocated in g3. Like as shards can not be rearranged by using REBALANCE feature even when a cluster group is added later in a table created by defining cluster group.

- Create a range sharded table.
- Allocate each range shards to defined cluster groups.

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

- Rearrange the range shard.
- A shard is not allocated to the newly created cluster group (g4).

```
ALTER TABLE t1 REBALANCE;
```

The following conditions should be considered to specify the range sharding key.

- Up to 32 columns can be listed.
- The duplicated column can not be used.
- The column of LONG VARCHAR or LONG VARBINARY type can not be used.

<a id="c0ad498362231e62"></a>
#### List Sharding Strategy

It distributes the table data based on the list value of the column defined as a sharding key. Like as the range sharding strategy, each shard can be arranged by defining a specific group, or arranged as CLUSTER WIDE.

The followings are conditions to define the shard key in list sharding strategy.

- Only a single column can be used.
- The column of LONG VARCHAR or LONG VARBINARY type can not be used.

The following is a syntax of creating a table of which created list shards are arranged as CLUSTER WIDE. Use REBALANCE feature to rearrange shards including a cluster group created after creating a table.

- Create a list sharded table.
- Arrange five shards in existing cluster groups (g1, g2, g3).

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

- Rearrange the list shard.
- Rearrange five shards in cluster groups (g1, g2, g3, g4) in which the created group is included.

```
ALTER TABLE city REBALANCE;
```

The following is a syntax of defining list shards, which are defined based on the list value of sharding key column value, only to be arranged in a specific cluster group. Shards can not be rearranged by using REBALANCE feature even when a cluster group is created.

- Create a list sharded table.
- Allocate each range shards to defined cluster groups.

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

- Rearrange the list shard.
- A shard is not allocated to the newly created cluster group (g4).

```
ALTER TABLE city REBALANCE;
```

<a id="993cdb4744970ae4"></a>
### Managing Index

<a id="415f519024fbccae"></a>
#### Global Secondary Index

In cluster system, multiple member nodes exist, and table records are dividedly stored or duplicated based on the shard strategy. Standalone system guarantees the uniqueness of a record by storing unique value (Row Identifier: RID) in the database when the record is stored. However, in cluster system, each node can have the duplicated value, so the uniqueness can not be guaranteed.

Therefore, it is required to guarantee the uniqueness of a record in cluster system. This is a reason why global RID(GRID) is added. The GRID value of a record is not updated even when the record is updated, then it guarantees the uniqueness of a specific record in cluster system.

Global secondary index is a B-tree index which consists of keys to search the GRID value of the records quickly in cluster system.

A user can select whether to create global secondary index through the following properties when creating a table. The user also can delete or recreate the global secondary index after table creation is completed. Only one global secondary index can be created per table.  
For more information, refer to [DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION](../part-02-administration-manual/10-server-property.md#ad829fbb24a70f70).

A global secondary index is necessary to perform the non-deterministic query for a table. If a global secondary index does not exist in a table, then a non-deterministic query fails as follows.

```
gSQL> DELETE FROM T1 LIMIT 1;

ERR-42000(16423): does not support non-deterministic DML in the cluster system : global secondary index expected
```

Enquire USER_GSI_PLACE DICTIONARY, or use ALL_GSI_PLACE and DBA_GSI_PLACE dictionary to check if the global secondary index of a table is created.

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

<a id="02d28b306c5135b1"></a>
### Global Sequence

GOLDILOCKS cluster system provides global sequence object which are an expansion of the existing sequence for multiple member nodes to share and use the set of sequence value fitting into user defined conditions. In other words, the global sequence object is internally and automatically created when a user creates a sequence in cluster system, then the sequence values in a specific range are allocated and used when calling NEXTVAL on each member node. The following is a syntax of creating and using the global sequence, which are as same as those of sequence in standalone.

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

Like as the sequence used in standalone, the global sequence object can define a cache size as a creating option, and this means acquiring several sequence value from the global sequence object and loading at local cache. The followings are local cache status of each member node and return values of when calling NEXTVAL, this is when creating the global sequence object by setting cache size to 5.

```
gSQL> CREATE SEQUENCE seq START WITH 1 CACHE 5; 

Sequence created.
```

<a id="de99156187049389"></a>
<table class="table column_count_5"><caption> </caption><thead><tr><th class="to_center to_middle" rowspan="2"><div>Member name</div></th><th class="to_center to_middle" rowspan="2"><div>NEXTVAL result</div></th><th class="to_center" colspan="2"><div>The number of remaining 
local cache sequence</div></th><th class="to_center to_middle" rowspan="2"><div>Description</div></th></tr><tr><th class="to_center"><div>G1N1</div></th><th class="to_center"><div>G1N2</div></th></tr></thead><tbody><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 1 ~ 5)</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>6</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 6 ~ 10)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>7</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>8</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>2</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>9</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>10</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>11</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 11 ~ 15)</div></td></tr><tr><td class="to_left to_middle"><div>G1N2</div></td><td class="to_center to_middle"><div>12</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>1</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>5</div></td><td class="to_center to_middle"><div>0</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Local Cache</div></td></tr><tr><td class="to_left to_middle"><div>G1N1</div></td><td class="to_center to_middle"><div>16</div></td><td class="to_center to_middle"><div>4</div></td><td class="to_center to_middle"><div>3</div></td><td class="to_left to_middle"><div>From Global Object
(Alloc 16 ~ 20)</div></td></tr></tbody></table>

In the table above, the sequence values are allocated to G1N1 and G1N2 two times each (four times in total) from the global sequence object. The cache option value is set to 5 when creating a sequence, so five sequence values are allocated each from the global object. Those five sequences allocated to a member node is stored in its own local cache, then it is returned one by one whenever calling NEXTVAL.

- G1N1
    - The values of five sequences (1~5) are allocated from the global sequence object when calling the first NEXTVAL.
    - A single sequence is returned as a result of NEXTVAL and the values of other four sequences are loaded in its own local cache.
    - NEXTVAL called later returns in turn the values of the sequences loaded in the local cache.
- G1N2
    - The values of sequences (6~10) which are after the sequences allocated on G1N1 are allocated when calling the first NEXTVAL.
    - 6 is returned as a result of NEXTVAL, and the values of other four sequences (7~10) are loaded in its own local cache.
    - NEXTVAL called later returns the sequence values loaded in the local cache.
    - Local cache is run out, so values of other five sequences (11~15) are allocated again from the global sequence object. 
- G1N1
    - Local cache is run out, so the values of five sequences (16~20) after the sequences allocated last on G1N2 are allocated.

The sequence as big as the CACHE size are allocated to all member nodes when NEXTVAL has never been called on its own node or when all allocated nodes are run out. Therefore, if a system needs to acquire the sequence value quickly, it is required to set the appropriate cache size when creating a sequence to prevent too much frequent allocation. It is because, unlike standalone database, allocating sequence from the global sequence object is accompanied by the network communication cost.

The sequence values loaded in local cache can not be reused when database restarts due to a system error or operational work. The sequence values are allocated again from the global sequence object when calling NEXTVAL for the first time since the restart. Therefore, the CACHE size allocated when creating the sequence also means the range value of sequence which is possible to be lost when an error occurs, so the size should be set appropriately considering not only the corresponding feature but also loss range.

The result value of calling NEXTVAL from a specific node may not be sequential in cluster system. In the example above, the return value is not sequential when G1N1 node calls NEXTVAL. After the first allocated value(1~5) is run out, 16~20 is allocated second, so 16 is returned to a user as the next sequence value of 5. It is because a single global sequence pool is allocated competitively to multiple nodes.

The followings are features and constraints of global sequence object, comparing to the sequence for existing standalone database.

- The sign can not be modified by using INCREMENT BY option in ALTER SEQUENCE statement. (The size can be modified.)
- The duplicated value among member nodes can be returned depending on the pool size of entire sequence when using CYCLE option. Therefore, create the sequence pool big enough, considering INCREMENT BY, CACHE SIZE, and the number of cluster member nodes when CYCLE option is in need. 
- The return value from a specific node may not be sequential even when an error does not occur. Of course, if only one member node calls NEXTVAL, then sequential sequence value is obtained.
- The CACHE SIZE is 1 for NOCACHE, so the additional sequence values are not loaded in local cache. In this case, only one sequence is allocated from the global sequence object whenever calling NEXTVAL, and it increases the network cost and degrades the performance. 
- Creating, updating and deleting sequences are operated as AUTO COMMIT.
- All sequence values loaded in local cache of all nodes are reset when the size of CACHE and INCREMENT are updated by ALTER statement. In other words, a new sequence set should be allocated from the global sequence object when calling NEXTVAL afterwards.

<a id="d398d817183b7bb3"></a>
## GOLDILOCKS Property

The followings are main properties used in GOLDILOCKS cluster system.

**Main properties of GOLDILOCKS**

<a id="c6605ec56084927d"></a>
| Name | Description |
| --- | --- |
| LOCAL_CLUSTER_MEMBER | Member name |
| LOCAL_CLUSTER_MEMBER_HOST | Host address for connecting to cluster session |
| LOCAL_CLUSTER_MEMBER_PORT | Port for connecting to cluster session |
| CDISPATCHER_THREADS | The number of cluster dispatcher threads |
| CSERVERS | The number of cluster server process |
| CLUSTER_DATA_SYNC_SERVERS | The number of cluster server process to synchronize replica data |

Each property has the following two alterable scopes in GOLDILOCKS cluster system.

- LOCAL: It can alter property values not only for entire member but also for a specific member only.
- GLOBAL: It can not alter the property value only for a specific member, but it should alter the property value for all members.

For example, PRIVATE_STATIC_AREA_SIZE properties can be altered up to the LOCAL range (IS_GLOBAL column = FALSE) as follows, so the property value can be altered by using *alter system set* statement not only for entire member but also for a specific member only. If AT clause is not added to after *alter system set* statement, the altered properties are applied to all members of cluster system.

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

However, DDL_AUTOCOMMIT can be altered up to GLOBAL as follows. Therefore, an error occurs when specifying a member by using AT clause in *alter system set* statement.

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
