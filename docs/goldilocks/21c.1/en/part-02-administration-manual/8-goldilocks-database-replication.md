<a id="abf71cb0fe7b510f"></a>

# 8. GOLDILOCKS Database Replication

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/abf71cb0fe7b510f)  
> Tag: `21c.1_35_tag`

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<a id="ec671186576fc735"></a>
## Overview

This chapter describes CYCLONE, LOGMIRROR and CYFILE.

GOLDILOCKS supports two types of replication, and they are CYCLONE and LOGMIRROR. CYCLONE replicates transactions using CDC, and LOGMIRROR replicates redo log files in the source database.

CYFILE uses CDC method to store/ record the transaction which was applied to the original database in Comma-Separated Values (CSV) format file.

**Replication tool**

<a id="834e9255b69242eb"></a>
| Tool | Replication target | Description |
| --- | --- | --- |
| CYCLONE | Transaction | It uses CDC method, and replicates the transaction reflected in master, then reflect it to slave. |
| LOGMIRROR | Redo log file | It identically replicates redo file in master database to slave. |
| CYFILE | Transaction | It uses CDC method to store/ record the transaction in CSV format file. |

- CYCLONE
    - It uses Change Data Capture (CDC) method to analyze and treat redo log files of the source database, then applies them to a remote database.
    - It supports only asynchronous (async) method because it analyzes contents stored in database's redo log file.
- LOGMIRROR
    - It replicates redo log files stored in the source database to a remote database.
    - It is used to avoid the data loss of CYCLONE which is executed in async method.
- CYFILE
    - It analyzes the redo log file of the database in CDC method, and stores it in CSV format data file. 
    - A user can perform the replication by using the corresponding file or perform ETL according to the purpose of the development.

<a id="38de4803e2a8c69b"></a>
## Operating Method

<a id="13d753da8279b639"></a>
### CYCLONE

For more information about general operating method and option, refer to [CYCLONE](../part-07-replication/50-cyclone.md#8113a087fe0f915a).

<a id="f56976411ab1ead6"></a>
#### Adding and Deleting Nodes

CYCLONE is performed in a group unit, and it is as same as the replication nodes. Add a group when adding nodes, drop a group when deleting nodes.

<a id="970743ddd7aaf649"></a>
##### Examples of Adding Nodes

- Record the group 2 to be added in master configuration file.
    - Set a unique port per each group.
    - The default master configuration file is $GOLDILOCKS_DATA/conf/cyclone.master.conf.

    - The following is an example of group 1 node in operation.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102
    CAPTURE_TABLE =
    (
        testTable1,
        testTable2
    )
}
```

    - The following is an example of group 2 node to be added.

```
GROUP_NAME = Group2
{
    PORT = 21103
    CAPTURE_TABLE =
    (
        testTable5,
        testTable6
    )
}
```

- Record the group 2 to be added in slave configuration file.
    - The port of group 2 should be as same as the port added to the existing master.
    - The default slave configuration file is $GOLDILOCKS_DATA/conf/cyclone.slave.conf.

    - The following is an example of group 1 node in operation.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102    
    APPLY_TABLE = 
    (
        testTable1 To testTable3,
        testTable2 To testTable4
    )
}
```

    - The following is an example of group 2 node to be added.

```
GROUP_NAME = Group2
{
    PORT = 21103    
    APPLY_TABLE = 
    (
        testTable5 To testTable7,
        testTable6 To testTable8
    )
}
```

- Execute and check the added group 2 node in the master device as follows.

```
prompt> cyclone --master --start --group Group2
[GROUP2] Startup done as Master.

prompt> cyclone --master --status
======================================
|       CYCLONE STATUS - MASTER      |
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

- Execute and check the added group 2 node in the slave device as follows.

```
prompt> cyclone --slave --start --group Group2
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="770c9f02664555e2"></a>
##### Examples of Deleting Nodes

- Terminate the group 2 node to be deleted in the slave device as follows.

```
prompt> cyclone --slave --stop --group Group2
stop done.

prompt> cyclone --slave --status
======================================
CYCLONE STATUS - SLAVE
======================================
GROUP1 Running...
--------------------------------------
```

- Terminate the group 2 node to be deleted in the master device as follows.

```
prompt> cyclone --master --stop --group Group2
stop done.

prompt> cyclone --master --status
======================================
CYCLONE STATUS - MASTER
======================================
GROUP1 Running...
--------------------------------------
```

- Drop the group 2 node to be deleted from the master configuration file.
    - The default master configuration file is $GOLDILOCKS_DATA/conf/cyclone.master.conf.

    - The following is an example of group 1 node in operation.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102
    CAPTURE_TABLE =
    (
        testTable1,
        testTable2
    )
}
```

    - The following is an example of deleting group 2 node.

<pre><code><del>GROUP_NAME = Group2
{
    PORT = 21103
    CAPTURE_TABLE =
    (
        testTable5,
        testTable6
    )
}</del></code></pre>

- Drop the group 2 node to be deleted from the slave configuration file as follows.
    - The default slave configuration file is $GOLDILOCKS_DATA/conf/cyclone.slave.conf.

    - The following is an example of group 1 node in operation.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102    
    APPLY_TABLE = 
    (
        testTable1 To testTable3,
        testTable2 To testTable4
    )
}
```

    - The following is an example of deleting group 2 node.

<pre><code><del>GROUP_NAME = Group2
{
    PORT = 21103    
    APPLY_TABLE = 
    (
        testTable5 To testTable7,
        testTable6 To testTable8
    )
}</del></code></pre>

<a id="1e7eac3ebff04f66"></a>
#### Initializing Replication

Initializing replication is executed when existing replication nodes or a group's table gives up execution due to DDL operation. A specific node or entire node can be initialized.

The initializing replication is performed by restarting replication being operated in slave using --reset option.  
On the other hand, master does not require any operation.

<a id="382a7a7f9a8527e4"></a>
##### Examples of Initializing Replication on a Specific Node

- Terminate the group 2 node to be initialized in the slave device as follows.

```
prompt> cyclone --slave --stop --group Group2
stop done.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
--------------------------------------
```

- Restart group 2 node in slave device using --reset option.
    - Master device does not require any operation.
    - Replication restarts from the current point.

```
prompt> cyclone --slave --start --reset --group Group2
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="96ef30504bc36bf4"></a>
##### Examples of Initializing Replication of All Nodes

- Terminate all CYCLONE in operation in the slave device as follows.

```
prompt> cyclone --stop --slave
```

- Restart CYCLONE in slave device using --reset option.
    - Master device does not require any operation.
    - Replication starts from the current point.

```
prompt> cyclone --slave --start --reset
[GROUP1] Startup done as Slave.
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="3c8205c940d04d93"></a>
### LOGMIRROR

For more information about general operation method and options, refer to [LOGMIRROR](../part-07-replication/51-logmirror.md#d8f0287925f9d4d4).

<a id="0ed2f3441e78b8ae"></a>
#### Retrieving LOGMIRROR State

GOLDILOCKS includes the response waiting procedure of LOGMIRROR when GOLDILOCKS interworks with LOGMIRROR. If LOGMIRROR is waiting for response, GOLDILOCKS is also waiting in a blocked state. This state can be retrieved in v$system_stat.

```
gSQL> SELECT * FROM V$SYSTEM_STAT WHERE STAT_NAME='LOG_MIRROR_SYNC_STATE';

STAT_NAME             STAT_VALUE COMMENTS                                     
--------------------- ------ ---------------------------------------------
LOG_MIRROR_SYNC_STATE      0 logmirror sync state( 0 : sync, 1 : blocked )


1 row selected.
```

If STAT_VALUE is 0, it is not a standby state but an ordinary state. If STAT_VALUE is 1, it is a blocked state waiting for a response. To restart GOLDILOCKS service while LOGMIRROR is waiting for a response, LOGMIRROR service can be stopped by modifying LOG_MIRROR_TIMEOUT as follows.

```
gSQL> ALTER SYSTEM SET LOG_MIRROR_TIMEOUT = 20;

System altered.
```

<a id="f1595b70d08a46b1"></a>
#### Initializing Replication

Initializing replication of LOGMIRROR should be done manually. This is to prevent data dropping or the unrecoverable situation driven by the user's incorrect option usage.

> Control files and redo log files are stored in LOGMIRROR slave. The required information for the operation is stored and updated in the control files.

<a id="fb846d9b22b40661"></a>
##### Examples of Initializing Replication

- Terminate LOGMIRROR in operation in the slave device as follows.

```
prompt> logmirror --slave --stop 
stop done.
```

- Terminate LOGMIRROR in operation in the master device as follows.

```
prompt> logmirror --master --stop 
stop done.
```

- Drop the replicated control files and redo log files from the slave device.
    - For more information about the path, refer to 'LOG_PATH' option described in the slave configuration file.
    - The default LOGMIRROR slave configuration file is $GOLDILOCKS_DATA/conf/logmirror.slave.conf.

<a id="fdb37cb5d817f1ea"></a>
### CYFILE

For more information about how to operate and its options, refer to [CYFILE](../part-07-replication/52-cyfile.md#5448c3ff47773041).

<a id="c9451f5353a180f8"></a>
#### Starting, Stopping and Status Checking of cyfile

<a id="d17433800ffc26ec"></a>
##### Example

- Start cyfile from the current moment by using the default configuration file.

```
prompt> cyfile --start --reset all
Startup done.
```

- Stop cyfile.

```
prompt> cyfile --stop
Stop done.
```

- CYFILE is operated in groups and the data file is created in groups.

```
prompt> cyfile --status
cyfile --status
======================================
|          CYFILE STATUS             |
======================================
 GROUP1 Running...
======================================
```

<a id="c350f6faf29c7f16"></a>
## Trace Log

The followings are detailed information about the trace log.

<a id="155e01d74140d01e"></a>
<table class="table column_count_3"><caption>Trace log</caption><thead><tr><th class="to_center"><div>Name</div></th><th class="to_center"><div>Category</div></th><th class="to_center"><div>File name</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="2"><div>CYCLONE</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>cyclone_master_GROUP_NAME.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>cyclone_slave_GROUP_NAME.trc</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>LOGMIRROR</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>LogMirror_master.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>LogMirror_slave.trc</div></td></tr><tr><td><div>CYFILE</div></td><td class="to_center"><div>-</div></td><td><div>cyfile_GROUP_NAME.trc</div></td></tr></tbody></table>

<a id="ee4799fdd8451177"></a>
### Troubleshooting of CYCLONE

The followings are error messages and troubleshooting of CYCLONE.

**Troubleshooting of CYCLONE**

<a id="9bb2adc830b33aa1"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is normally running. |
| table does not exist | Check the table name described in the configuration file. |
| schema does not exist | Check the schema name described in the configuration file. |
| previously added. Maybe duplicated | Check if a table is duplicated in the configuration file. |
| table must have a primary key | Ensure that a table in the configuration file has the primary key. |
| internal error occurred. | Check the error details. |
| table must set supplemental log | Ensure that supplemental logging is executed in GOLDILOCKS. |
| group XXX is already running | Check if the corresponding group is already running. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that GOLDILOCKS_DATA environment variable is set. |
| log file reused or invalid. restart cyclone with '--reset' option | This error occurs when the redo log file is reused or archived redo log file does not exist. In this case, initialize CYCLONE and restart it. |
| fail to analyze flow | This error occurs when analyzing an abnormal redo log file. Ensure that the release version between master and slave are same. |
| Communication link failure | Check the network state. Restart CYCLONE. |
| Master disconnect abnormally | Check the network state. Restart CYCLONE. |
| Protocol error occurred | Check the error details. |
| Already slave connected | Check if the slave is already running. |
| Invalid group name | Check the specified group name at the startup/termination. The group name should be same as described in the configuration file. |
| Invalid capture information | This error occurs when the existing operating information is abnormal. In this case, initialize CYCLONE and restart it. |
| Redo log file read timeout | Ensure that the archived redo log files normally exist. |
| Invalid archive log file | The archived redo log file is not normal. In this case, initialize CYCLONE and restart it. |
| Fail to write file | Check the available space in the disk, and restart CYCLONE. |
| Invalid Meta File | This error occurs when the meta files which are managed by CYCLONE are corrupted. In this case, initialize CYCLONE and restart it. |
| Redo log file does not exist | Ensure that GOLDILOCKS which is operated as master is normally running. |
| [APPLIER-INSERT] XXX | INSERT is failed due to XXX. |
| [APPLIER-DELETE] XXX | DELETE is failed due to XXX. |
| [APPLIER-UPDATE] XXX | UPDATE is failed due to XXX. |

<a id="40dd00003e243c21"></a>
### Troubleshooting of LOGMIRROR

The followings are error messages and troubleshooting of LOGMIRROR.

**Troubleshooting of LOGMIRROR**

<a id="cb44b560c798a4cc"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is normally running. |
| Invalid Protocol value | Check the error details. |
| file does not exist | Ensure that the corresponding file normally exists. |
| invalid Control file | The control file is corrupted. Initialize and restart LOGMIRROR. |
| Communication link failure | Check the network state. Restart LOGMIRROR. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that GOLDILOCKS_DATA environment variable is set. |
| There is no Shared Memory Area for LogMirror | Ensure that LOG_MIRROR_MODE property is normally set to 'enabled' in properties of GOLDILOCKS which is operated as master. |
| Master disconnect abnormally | Check the network state. Restart LOGMIRROR. |
| Invalid Log File | Ensure that the corresponding file normally exists. |
| Connection Information does not exist | Ensure that GOLDILOCKS connecting information in configuration files is normal. |
| Archive Log File does not exist | Ensure that ARCHIVELOG_MODE in GOLDILOCKS which is operated as master is normally set. |

<a id="9f9099d7a16236d5"></a>
### Troubleshooting of CYFILE

The followings are error messages and troubleshooting of CYFILE.

<a id="be413e8260e19423"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is normally running. |
| table does not exist | Check the table name described in the configuration file. |
| schema does not exist | Check the schema name described in the configuration file. |
| previously added. Maybe duplicated | Check if a table is duplicated in the configuration file. |
| table must have a primary key | Ensure that a table in the configuration file has the primary key. |
| internal error occurred. | Check the error details. |
| table must set supplemental log | Ensure that supplemental logging is executed in GOLDILOCKS. |
| group XXX is already running | Check if the corresponding group is already running. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that GOLDILOCKS_DATA environment variable is set. |
| log file reused or invalid. restart cyfile with '--reset' option | This error occurs when the redo log file is reused or archived redo log file does not exist. In this case, initialize cyfile and restart it. |
| fail to analyze flow | This error occurs when analyzing an abnormal redo log file. Ensure that the release version between master and slave are same. |
| Invalid group name | Check the specified group name at the startup/termination. The group name should be same as described in the configuration file. |
| Invalid capture information | This error occurs when the existing operating information is abnormal. In this case, initialize cyfile and restart it. |
| Redo log file read timeout | Ensure that the archived redo log files normally exist. |
| Invalid archive log file | The archived redo log file is not normal. In this case, initialize cyfile and restart it. |
| Fail to write file | Check the available space in the disk, and restart cyfile. |
| Invalid Meta File | This error occurs when the meta files which are managed by cyfile are corrupted. In this case, initialize cyfile and restart it. |
| Redo log file does not exist | Ensure that GOLDILOCKS is normally running. |
| Control has broken(CRC Error) | The control file of cyfile is damaged. Retry it by using the mirror file. |

---

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
