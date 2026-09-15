<a id="e8e225cb7017a437"></a>

# 8. GOLDILOCKS Database Replication

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/e8e225cb7017a437)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<a id="6aca1f9df341e6ba"></a>
## Overview

This chapter describes CYCLONE and LOGMIRROR.

GOLDILOCKS supports two types of replication, and they are CYCLONE and LOGMIRROR. CYCLONE replicates transactions using CDC, and LOGMIRROR replicates redo log files in the source database.

**Replication tool**

<a id="87b02e2fc5af978e"></a>
| Tool | Replication target | Description |
| --- | --- | --- |
| CYCLONE | Transaction | It uses CDC method, and replicates the transaction reflected in master, then reflect it to slave. |
| LOGMIRROR | Redo log file | It identically replicates redo file in master database to slave. |

- CYCLONE
    - It uses Change Data Capture (CDC) method to analyze and treat redo log files of the source database, then applies them to a remote database.
    - It supports only asynchronous (async) method because it analyzes contents stored in database's redo log file.
- LOGMIRROR
    - It replicates redo log files stored in the source database to a remote database.
    - It is used to avoid the data loss of CYCLONE which is executed in async method.

<a id="b95854d7603c3f5e"></a>
## Operating Method

<a id="bdffb7a7fa2339b3"></a>
### CYCLONE

For more information about general operating method and option, refer to [CYCLONE](../part-07-replication/44-cyclone.md#3e588d1e894bf1d0).

<a id="de9f2a4ca9e6602d"></a>
#### Adding and Deleting Nodes

CYCLONE is performed in a group unit, and it is as same as the replication nodes. Add a group when adding nodes, drop a group when deleting nodes.

<a id="551dfa1822321ea3"></a>
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

<a id="1dfc8427febb28ea"></a>
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

<a id="beeb84ba87f38ab1"></a>
#### Initializing Replication

Initializing replication is executed when existing replication nodes or a group's table gives up execution due to DDL operation. A specific node or entire node can be initialized.

The initializing replication is performed by restarting replication being operated in slave using --reset option.  
On the other hand, master does not require any operation.

<a id="4b69e31b538162b1"></a>
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

<a id="012fdf5152d86502"></a>
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

<a id="488600f5b7621baf"></a>
### LOGMIRROR

For more information about general operation method and options, refer to [LOGMIRROR](../part-07-replication/45-logmirror.md#825637a16fcab368).

<a id="1472c32a9872d3b5"></a>
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

<a id="fe970bc4a211122f"></a>
#### Initializing Replication

Initializing replication of LOGMIRROR should be done manually. This is to prevent data dropping or the unrecoverable situation driven by the user's incorrect option usage.

> Control files and redo log files are stored in LOGMIRROR slave. The required information for the operation is stored and updated in the control files.

<a id="6cae33d05f05bad4"></a>
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

<a id="8e6fcd5f2ae16747"></a>
## Trace Log

The followings are detailed information about the trace log.

<a id="303e7cc3e09b4b27"></a>
<table class="table column_count_3"><caption>Trace log</caption><thead><tr><th class="to_center"><div>Name
</div></th><th class="to_center"><div>Category
</div></th><th class="to_center"><div>File name
</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="2"><div>CYCLONE</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>cyclone_master_GROUP_NAME.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>cyclone_slave_GROUP_NAME.trc</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>LOGMIRROR</div></td><td class="to_left"><div>Master</div></td><td class="to_left"><div>LogMirror_master.trc</div></td></tr><tr><td class="to_left"><div>Slave</div></td><td class="to_left"><div>LogMirror_slave.trc</div></td></tr></tbody></table>

<a id="167dc9cef09772bb"></a>
### Troubleshooting of CYCLONE

The followings are error messages and troubleshooting of CYCLONE.

**Troubleshooting of CYCLONE**

<a id="6f39453e943b65e3"></a>
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

<a id="b729d2d126748f0f"></a>
### Troubleshooting of LOGMIRROR

The followings are error messages and troubleshooting of LOGMIRROR.

**Troubleshooting of LOGMIRROR**

<a id="d1265f32955c8a65"></a>
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

---

[← 7. Backup and Recovery of GOLDILOCKS Database](7-backup-and-recovery-of-goldilocks-database.md) · [Table of contents](../README.md) · [9. Database Information →](9-database-information.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
