<a id="d89a03bd68c9ab76"></a>

# 8. GOLDILOCKS Database Replication

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/d89a03bd68c9ab76)  
> Tag: `26c.1_0_tag`

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<a id="1edbc48b7e65b9e4"></a>
## Overview

This chapter describes CYCLONE, LOGMIRROR and CYFILE.

GOLDILOCKS supports two types of replication, and they are CYCLONE and LOGMIRROR. CYCLONE replicates transactions using CDC, and LOGMIRROR replicates redo log files from the source database.

CYFILE employs the CDC method to store or record transactions applied to the original database in Comma-Separated Values (CSV) format file.

**Replication tool**

<a id="0b40645c103f751e"></a>
| Tool | Replication target | Description |
| --- | --- | --- |
| CYCLONE | Transaction | It uses the CDC method to replicate transactions reflected in the master, and then applies them to the slave. |
| LOGMIRROR | Redo log file | It replicates the redo log files from the master database to the slave identically. |
| CYFILE | Transaction | It uses the CDC method to store or record transactions in a CSV format file. |

- CYCLONE
    - It uses the Change Data Capture (CDC) method to analyze and process the redo log files of the source database, and then applies them to a remote database.
    - It only supports the asynchronous (async) method, as it analyzes the contents stored in the database's redo log file.
- LOGMIRROR
    - It replicates the redo log files stored in the source database to a remote database.
    - It is used to prevent data loss for CYCLONE, which operates in asynchronous mode.
- CYFILE
    - It analyzes the database's redo log file using the CDC method and stores the data in a CSV format file. 
    - A user can perform replication using the corresponding file or carry out ETL based on the development's purpose.

<a id="87c284b7b8b22690"></a>
## Operating Method

<a id="1b6cf86b3ac9008a"></a>
### CYCLONE

For more information about general operational methods and options, refer to [CYCLONE](../part-07-replication/55-cyclone.md#c0dd6c17daab1472).

<a id="81ceaa96cceaf95c"></a>
#### Adding and Deleting Nodes

CYCLONE operates in group units, similar to the replication nodes. When adding nodes, a group must be added, and when deleting nodes, a group must be dropped.

<a id="6ef348c9487013fc"></a>
##### Examples of Adding Nodes

- Record the group 2 to be added in the master configuration file.
    - Set a unique port for each group.
    - The default master configuration file is $GOLDILOCKS_DATA/conf/cyclone.master.conf.

    - The following is an example of a group 1 node in operation.

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

    - The following is an example of a group 2 node to be added.

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

- Record the group 2 to be added in the slave configuration file.
    - The port for group 2 must be the same as the port added to the existing master.
    - The default slave configuration file is $GOLDILOCKS_DATA/conf/cyclone.slave.conf.

    - The following is an example of a group 1 node in operation.

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

    - The following is an example of a group 2 node to be added.

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

- Execute and verify the added group 2 node on the master device.

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

- Execute and verify the added group 2 node on the slave device.

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

<a id="c2e894a895d5f823"></a>
##### Examples of Deleting Nodes

- Terminate the group 2 node to be deleted on the slave device as follows.

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

- Terminate the group 2 node to be deleted on the master device as follows.

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

    - The following is an example of a group 1 node in operation.

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

    - The following is an example of how to delete the group 2 node.

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

    - The following is an example of a group 1 node in operation.

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

    - The following is an example of how to delete the group 2 node.

<pre><code><del>GROUP_NAME = Group2
{
    PORT = 21103    
    APPLY_TABLE = 
    (
        testTable5 To testTable7,
        testTable6 To testTable8
    )
}</del></code></pre>

<a id="567b3a43610f29bf"></a>
#### Initializing Replication

Initializing replication is executed when existing replication nodes or a group's table gives up execution due to a DDL operation. Either a specific node or all nodes can be initialized.

The initializing replication is performed by restarting the replication running on the slave using the --reset option.  
On the other hand, no action is required on the master.

<a id="d2ac2dd4c98e83a4"></a>
##### Examples of Initializing Replication on a Specific Node

- Terminate the group 2 node to be initialized on the slave device as follows.

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

- Restart the group 2 node on the slave device using the --reset option.
    - No action is required on the master device.
    - Replication will restart from the current point.

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

<a id="0adcf855098079ab"></a>
##### Examples of Initializing Replication for All Nodes

- Terminate all CYCLONE operations running on the slave device.

```
prompt> cyclone --stop --slave
```

- Restart CYCLONE on the slave device using the --reset option.
    - No action is required on the master device.
    - Replication will resume from the current point.

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

<a id="bc4f225c6d7c7261"></a>
### LOGMIRROR

For more information about general operational methods and options, refer to [LOGMIRROR](../part-07-replication/56-logmirror.md#68ef4cdd96f98d3e).

<a id="37e7306a36222db0"></a>
#### Retrieving LOGMIRROR State

When interworking with LOGMIRROR, GOLDILOCKS includes the response waiting process of LOGMIRROR. If LOGMIRROR is waiting for a response, GOLDILOCKS will also be in a blocked state, waiting. This state can be checked in v$system_stat.

```
gSQL> SELECT * FROM V$SYSTEM_STAT WHERE STAT_NAME='LOG_MIRROR_SYNC_STATE';

STAT_NAME             STAT_VALUE COMMENTS                                     
--------------------- ------ ---------------------------------------------
LOG_MIRROR_SYNC_STATE      0 logmirror sync state( 0 : sync, 1 : blocked )


1 row selected.
```

If STAT_VALUE is 0, it indicates an ordinary state rather than a standby state. If STAT_VALUE is 1, it indicates a blocked state waiting for a response. To restart the GOLDILOCKS service while LOGMIRROR is waiting for a response, the LOGMIRROR service can be stopped by modifying LOG_MIRROR_TIMEOUT as follows.

```
gSQL> ALTER SYSTEM SET LOG_MIRROR_TIMEOUT = 20;

System altered.
```

<a id="f1938ee507a06a27"></a>
#### Initializing Replication

Initializing the replication of LOGMIRROR must be done manually to prevent data loss or an unrecoverable situation caused by incorrect user options.

> Control files and redo log files are stored on the LOGMIRROR slave. The necessary information for operation is stored and updated in these control files.

<a id="8b0186e5ec0b9f9b"></a>
##### Examples of Initializing Replication

- Terminate LOGMIRROR in operation on the slave device as follows.

```
prompt> logmirror --slave --stop 
stop done.
```

- Terminate LOGMIRROR in operation on the master device as follows.

```
prompt> logmirror --master --stop 
stop done.
```

- Drop the replicated control files and redo log files from the slave device.
    - For more information about the path, refer to the 'LOG_PATH' option described in the slave configuration file.
    - The default LOGMIRROR slave configuration file: $GOLDILOCKS_DATA/conf/logmirror.slave.conf.

<a id="d9d9cdbff356f4c9"></a>
### CYFILE

For more information about general operational methods and options, refer to [CYFILE](../part-07-replication/57-cyfile.md#e9848afe20792281).

<a id="c2c3de7c7d17eb6d"></a>
#### Starting, Stopping, and Checking the Status of Cyfile

<a id="ffd368ab608e924c"></a>
##### Example

- Start cyfile from the current point using the default configuration file.

```
prompt> cyfile --start --reset all
Startup done.
```

- Stop cyfile.

```
prompt> cyfile --stop
Stop done.
```

- CYFILE operates in groups, and the data files are created in groups.

```
prompt> cyfile --status
cyfile --status
======================================
|          CYFILE STATUS             |
======================================
 GROUP1 Running...
======================================
```

<a id="cd2f409c705f2128"></a>
## Trace Log

The following provides detailed information about the trace log.

<a id="605dc9c24ce7e0ed"></a>
<table class="table column_count_3"><caption>Trace log</caption><thead><tr><th class="to_center"><div>Name</div></th><th class="to_center"><div>Category</div></th><th class="to_center"><div>File name</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="2"><div>CYCLONE</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>cyclone_master_GROUP_NAME.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>cyclone_slave_GROUP_NAME.trc</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>LOGMIRROR</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>LogMirror_master.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>LogMirror_slave.trc</div></td></tr><tr><td><div>CYFILE</div></td><td class="to_center"><div>-</div></td><td><div>cyfile_GROUP_NAME.trc</div></td></tr></tbody></table>

<a id="ac20cf143b39651b"></a>
### Troubleshooting for CYCLONE

The following are error messages and troubleshooting for CYCLONE.

**Troubleshooting for CYCLONE**

<a id="f011a73b79456fc0"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is running normally. |
| table does not exist | Check the table name specified in the configuration file. |
| schema does not exist | Check the schema name specified in the configuration file. |
| previously added. Maybe duplicated | Check if a table is duplicated in the configuration file. |
| table must have a primary key | Ensure that a table in the configuration file has a primary key. |
| internal error occurred. | Check the error details. |
| table must set supplemental log | Ensure that supplemental logging is enabled in GOLDILOCKS. |
| group XXX is already running | Check if the corresponding group is already running. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that the GOLDILOCKS_DATA environment variable is set. |
| log file reused or invalid. restart cyclone with '--reset' option | This error occurs when the redo log file is reused or the archived redo log file does not exist. In this case, initialize CYCLONE and restart it. |
| fail to analyze flow | This error occurs when analyzing an abnormal redo log file. Ensure that the release versions between the master and slave are the same. |
| Communication link failure | Check the network status. Restart CYCLONE. |
| Master disconnect abnormally | Check the network status. Restart CYCLONE. |
| Protocol error occurred | Check the error details. |
| Already slave connected | Check if the slave is already running. |
| Invalid group name | Check the specified group name at the startup and termination. The group name must be the same as described in the configuration file. |
| Invalid capture information | This error occurs when the existing operational information is abnormal. In this case, initialize CYCLONE and restart it. |
| Redo log file read timeout | Ensure that the archived redo log files exist normally. |
| Invalid archive log file | The archived redo log file is not functioning normally. In this case, initialize CYCLONE and restart it. |
| Fail to write file | Check the available disk space, and then restart CYCLONE. |
| Invalid Meta File | This error occurs when the meta files managed by CYCLONE are corrupted. In this case, initialize CYCLONE and restart it. |
| Redo log file does not exist | Ensure that GOLDILOCKS, operating as master, is running normally. |
| [APPLIER-INSERT] XXX | INSERT failed due to XXX. |
| [APPLIER-DELETE] XXX | DELETE failed due to XXX. |
| [APPLIER-UPDATE] XXX | UPDATE failed due to XXX. |

<a id="740ea77938d89ea6"></a>
### Troubleshooting for LOGMIRROR

The following are error messages and troubleshooting for LOGMIRROR.

**Troubleshooting for LOGMIRROR**

<a id="8549c4f69b36fccf"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is running normally. |
| Invalid Protocol value | Check the error details. |
| file does not exist | Ensure that the corresponding file exists normally. |
| invalid Control file | The control file is corrupted. Initialize and restart LOGMIRROR. |
| Communication link failure | Check the network status. Restart LOGMIRROR. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that GOLDILOCKS_DATA environment variable is set. |
| There is no Shared Memory Area for LogMirror | Ensure that the LOG_MIRROR_MODE property is set to 'enabled' in the properties of GOLDILOCKS, which is operating as the master. |
| Master disconnect abnormally | Check the network status. Restart LOGMIRROR. |
| Invalid Log File | Ensure that the corresponding file exists normally. |
| Connection Information does not exist | Ensure that the connection information for GOLDILOCKS in the configuration files is correct. |
| Archive Log File does not exist | Ensure that the ARCHIVELOG_MODE in GOLDILOCKS, operating as the master, is set correctly. |

<a id="b95410a226c4d8a5"></a>
### Troubleshooting for CYFILE

The following are error messages and troubleshooting for CYFILE.

**Troubleshooting for CYFILE**

<a id="b9338b4ca3071737"></a>
| Error message | Solution |
| --- | --- |
| Service is not available | Ensure that GOLDILOCKS is running normally. |
| table does not exist | Check the table name specified in the configuration file. |
| schema does not exist | Check the schema name specified in the configuration file. |
| previously added. Maybe duplicated | Check if a table is duplicated in the configuration file. |
| table must have a primary key | Ensure that a table in the configuration file has a primary key. |
| internal error occurred. | Check the error details. |
| table must set supplemental log | Ensure that supplemental logging is enabled in GOLDILOCKS. |
| group XXX is already running | Check if the corresponding group is already running. |
| GOLDILOCKS_DATA system environment is invalid | Ensure that the GOLDILOCKS_DATA environment variable is set. |
| log file reused or invalid. restart cyfile with '--reset' option | This error occurs when the redo log file is reused or archived redo log file does not exist. In this case, initialize cyfile and restart it. |
| fail to analyze flow | This error occurs when analyzing an abnormal redo log file. Ensure that the release versions between the master and the slave are the same. |
| Invalid group name | Check the specified group name at the startup and termination. The group name must be the same as described in the configuration file. |
| Invalid capture information | This error occurs when the existing operational information is abnormal. In this case, initialize cyfile and restart it. |
| Redo log file read timeout | Ensure that the archived redo log files exist normally. |
| Invalid archive log file | The archived redo log file is not functioning normally. In this case, initialize cyfile and restart it. |
| Fail to write file | Check the available disk space, and then restart cyfile. |
| Invalid Meta File | This error occurs when the meta files managed by cyfile are corrupted. In this case, initialize cyfile and restart it. |
| Redo log file does not exist | Ensure that GOLDILOCKS is running normally. |
| Control has broken(CRC Error) | The control file of cyfile is damaged. Retry using the mirror file. |

---

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
