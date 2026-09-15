<a id="162838622a7b72ea"></a>

# 6. Structure and Storage Structure of GOLDILOCKS Database

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/162838622a7b72ea)  
> Tag: `26c.1_0_tag`

[← 5. Basic Management of GOLDILOCKS Database](5-basic-management-of-goldilocks-database.md) · [Table of contents](../README.md) · [7. Backup and Recovery of GOLDILOCKS Database →](7-backup-and-recovery-of-goldilocks-database.md)

<a id="efda9fc851899fb4"></a>
## Managing Control File

To use the GOLDILOCKS database, a database instance must be created, which also involves creating a control file. When the GOLDILOCKS multilevel startup process transitions from the NOMOUNT phase to the MOUNT phase, the information recorded in the control file is used to determine details such as the absolute paths and sizes of the files to be used by the database. The control file is a binary file that stores the following database information.

<a id="bedd8013879a57f7"></a>
### Control File Contents

**GOLDILOCKS database system information**

<a id="bd343eda51e8dc67"></a>
| Item | Description |
| --- | --- |
| Data store mode | It is the storage mode set when the database starts up, such as TDS or CDS. |
| Server state | It is the state of the database instance. (NONE, RECOVERED, RECOVERING, SERVICE, SHUTDOWN) |
| Last checkpoint lsn | It is the LSN of the most recent checkpoint executed in the database. |
| On Disk Lsn | The minimum LSN that contains the logs required for database recovery. |

**Log information**

<a id="701ce6b99ca92594"></a>
| Item | Description |
| --- | --- |
| Checkpoint lid, lsn | It is the log information (LSN, log position) of the most recent checkpoint executed in the database. |
| Last inactivated log file sequence | It is the sequence number of the log file that was most recently changed to inactive. |
| Archivelog mode | It is the archivelog mode currently in operation for the database. |
| Creation time | It is the timestamp when the database was created. |

The database information includes details about the database’s operation, information on all in-use tablespaces, and data. The operational information stored in the control file includes the following.

**Database information**

<a id="a1ca81cee6d73bda"></a>
| Item | Description |
| --- | --- |
| Transaction table size | It is the maximum number of transaction tables currently in use by the database. |
| Undo relation count | It is the number of undo relations currently in use by the database. |
| Tablespace count | It is the number of tablespaces that have been created and are in use in the database. |
| New tablespace id | It is the ID for the tablespace that will be created next. |

Tablespace information stored in the control file includes the following.

**Tablespace information**

<a id="dda9f570b183f487"></a>
| Item | Description |
| --- | --- |
| Tablespace id | It is a unique ID for the tablespace. |
| Attributes | It is the characteristics of the tablespace, including the storage device (memory, disk), persistence (temporary, persistent), and tablespace usage (dictionary, undo, data, temporary). |
| Page count in extent | It is the number of pages in each extent. |
| State | It is the current status of the tablespace. (CREATING, CREATED, DROPPING, DROPPED, AGING) |
| Relation id | It is the relation ID used to store pending operations for the tablespace. |
| New data file id | It is the ID assigned to a new data file added to the tablespace. |
| Is logging | It is the logging mode of the tablespace. (LOGGING, NOLOGGING) |
| Is online | It is the online status of the tablespace. (ONLINE, OFFLINE) |
| Data file count | It is the number of data files currently in use by the tablespace. |
| Offline lsn | It is the last LSN required for recovery if needed, to transition an offline tablespace back to online. |
| Offline state | It is the status of an offline tablespace. (CONSISTENT, INCONSISTENT)  A CONSISTENT offline tablespace does not require recovery when brought back online, as it was taken offline only after ensuring that the most recent data in memory was written to disk. In contrast, an INCONSISTENT offline tablespace requires recovery using the log to bring it back online. |

Data file information stored in the control file includes the following.

**Data file information**

<a id="1fa8dd6ed07f94b3"></a>
| Item | Description |
| --- | --- |
| Name | It is the name of the data file, including the absolute path where data is stored. |
| State | It is the status of the data file. (CREATING, CREATED, DROPPING, DROPPED, AGING) |
| Data file id | It is a unique ID for the data file within a tablespace. |
| Auto extend | It indicates whether the data file is set to automatically extend when it becomes full. |
| Size | It is the current size of the data file. |
| Next size | It is the size by which the data file will be extended when it is full. |
| Max size | It is the maximum size to which the data file can be extended. |
| Timestamp | It is the time when the data file was created. |
| Checkpoint lsn, lid | It is the checkpoint log information for the last checkpoint performed on the data file. (LSN, log position) |
| Creation lsn, lid | It is the checkpoint log information from the time when the data file was created. (LSN, log position) |

It stores information about each incremental backup performed in the database. The GOLDILOCKS database supports incremental backups for both the database and individual tablespaces. This incremental backup information is recorded in the control file as follows.

**Incremental backup information**

<a id="661e27b5250e088d"></a>
| Item | Description |
| --- | --- |
| Backup lsn, lid | It is the checkpoint log information from the last checkpoint executed at the start of the backup. (LSN, log position) |
| Begin time | It is the start time of the incremental backup. |
| Completion time | It is the completion time of the incremental backup. |
| Tablespace id | It is the unique tablespace ID for which the incremental backup was performed. If an incremental backup was executed for a tablespace, its tablespace ID is recorded. If no backup was performed for a tablespace, the maximum tablespace ID (65535) is recorded instead. |
| Level | It is the level of the incremental backup that was executed. |
| Object type | It is the target of the incremental backup. (database, control file, tablespace) |
| Backup file name | It is the name of the incremental backup file. |
| Backup option | It is the option used for the incremental backup. (cumulative, differential) |

<a id="d8d1c8abbbcaf199"></a>
### Multiplexing Control File

The control file stores the physical structure of the GOLDILOCKS database and information on data consistency. If the control file becomes corrupted or is accidentally deleted, the database cannot operate.

Therefore, the GOLDILOCKS database recommends creating at least two control files and storing them on physically separate disks. GOLDILOCKS supports multiplexing up to 8 control files. To add control files when creating a database, specify the number of multiplexing control files and their paths in the property file. To add control files during database operation, increase the control file multiplexing property value and add the paths of the new control files.

<a id="fc42c5e086144596"></a>
### Restoring Corrupted Control File

If a control file is corrupted due to an abnormal database termination, the corrupted control file is restored using one of the intact control files from the multiplexed set, and then the database is restarted.

If all multiplexed control files are corrupted, the backup control file is restored. An incomplete media recovery is then performed using archive redo log files and redo log files, followed by a restart of the database. For more information about performing incomplete recovery with the backup control file, refer to [When all multiplexed control files are corrupted](7-backup-and-recovery-of-goldilocks-database.md#9b4e88574fce46ba) in the recovery examples.

<a id="35e1dd1e522e894c"></a>
### Control File Information

A user can use the performance view V$CONTROLFILE to query information about the location and name of the control file. The following is an example of how to retrieve the control file names using V$CONTROLFILE.

```
gSQL> SELECT CONTROLFILE_NAME FROM V$CONTROLFILE;

CONTROLFILE_NAME                                         
---------------------------------------------------------
/goldilocks_data/wal/control_0.ctl
/goldilocks_data/wal/control_1.ctl

2 rows selected.
```

A user can retrieve accurate information from the control file using [gdump](../part-06-utility-manual/46-gdump.md#e9ec9dbb7f8caa83), the dump tool provided by GOLDILOCKS.

<a id="2659b5d5c8f0ac63"></a>
## Managing Redo Log File

GOLDILOCKS uses redo log files to ensure database persistency. In other words, if the GOLDILOCKS database is abnormally terminated for any reason, it can be restored to its state prior to shutdown using the redo log files and data files.

To achieve this, the GOLDILOCKS database uses the Write Ahead Logging (WAL) policy to log all database update operations.

The updated data from an update operation is not recorded directly in the data file; instead, the log for the update operation is recorded in the redo log file. This approach is more efficient in terms of database performance. Recording each update operation directly in the data file would require random access and could lead to excessive disk I/O due to multiple updates to the same file. In contrast, the update log is smaller than the updated data and is continuously appended to the end of the log file, which allows for more efficient disk I/O.

Additionally, the GOLDILOCKS database uses a log buffer in shared memory to record update logs and then writes the log buffer to the log file in batches, resulting in more efficient disk I/O.

<a id="972c373e3dcef665"></a>
### Redo Log File Structure

The redo log buffer and log files in GOLDILOCKS have a circular structure. A predefined number of log files are created to record logs, and when one log file becomes full, the system uses the next log file. Once all log files are used, the previously used log files are reused. The log files consist of a circular structure with a single log group containing multiple members, and GOLDILOCKS performs logging using a minimum of four log groups.

<a id="2bd7b889197da4e4"></a>
![GOLDILOCKS redo log file, log buffer structure](../assets/images/bdbc97d91608b3cf.png)

<a id="cba1a157e2cabf64"></a>
### Redo Log Group and Its Member

The GOLDILOCKS database uses log groups and members to record logs to the disk log file during database operation. Each redo log file is a member of a log group, and a log group consists of several log members. Having multiple members in a log group ensures high availability, as other log members can be used if a particular disk fails or if a particular log member becomes corrupted.

The system uses a circular log group structure, recording logs to one log group at a time. When that log group becomes full, the system moves to the next log group. The transition of the system from the current log group to the next one is referred to as log switching.

The number of log groups and members, as well as their positions, are set by properties during database creation. They can also be modified using ADD or DROP statements while the database is in operation.

<a id="03e1103349561db9"></a>
#### Log Group State

A log group is initialized to the UNUSED state when created and changes to CURRENT, ACTIVE, or INACTIVE states during operation as managed by the system.

**GOLDILOCKS log group state**

<a id="cb14aaece5fb0607"></a>
| Log group state | Description |
| --- | --- |
| UNUSED | The log group has not been used since its creation. |
| CURRENT | The log group is currently in use by the system. |
| ACTIVE | The log group is not yet ready to be reused after the CURRENT log group has been switched. |
| INACTIVE | The ACTIVE state log group is now ready to be reused. |

An ACTIVE log group can not be reused in the system, but it can be reused once it is changed to INACTIVE by the archive log thread. The archive log thread is triggered by an event that occurs before the checkpoint is completed, and it changes ACTIVE log groups to INACTIVE. To do this, the log archiving thread first archives the log file in the ACTIVE log group, and then changes its status to INACTIVE if the system is operating in ARCHIVELOG mode. If the system is operating in NOARCHIVELOG mode, the ACTIVE log group becomes immediately reusable once its status is changed to INACTIVE.

<a id="ef0708963150c5f4"></a>
#### Adding Log Group and Log Member

<a id="d6c2b58f5ba199ad"></a>
##### Adding Log Group

Adding a log group is allowed only during the mount phase of the GOLDILOCKS database multilevel startup. The new log group is added next to the CURRENT log group that is currently being used.  
The following is an example to add a new log group with the file name 'abc.log', and a file size of 20 Mbytes to group ID 10.

```
ALTER DATABASE ADD LOGFILE GROUP 10 ('abc.log') SIZE 20M;
```

<a id="f9c696c4ade01880"></a>
##### Adding Log Member

A new log member can be added to enhance the stability of a log group in use. This can be done during the mount phase of the GOLDILOCKS database multilevel startup, similar to the process for adding a log group. The following is an example to add a log file named 'test log' to group ID 10. The log file size is not specified because all log members within a log group have the same size.

```
ALTER DATABASE ADD LOGFILE MEMBER 'test.log' TO GROUP 10;
```

<a id="664425f873f8a00d"></a>
#### Altering Log Member Name

The position and file name of a log member in use can be altered by executing the RENAME command during the mount phase. RENAME is executed when a log member's disk has physically failed or when the log member needs to be transferred to another disk for performance reasons.  
The following is an example to RENAME the log file from '/disk1/goldilocks_data/wal/redo_0_0.log' to '/disk2/goldilocks_data/wal/redo_0_0.log'.

```
ALTER DATABASE RENAME LOGFILE '/disk1/GOLDILOCKS_data/wal/redo_0_0.log' TO '/disk2/GOLDILOCKS_data/wal/redo_0_0.log';
```

<a id="de5f69fb292d752a"></a>
#### Dropping Log Group or Log Member

A log member or log group in use can be dropped during the mount phase if a user wants to reduce log groups or log members or if a log file's disk has failed.  
The following is an example to drop all members of log group ID 10.

```
ALTER DATABASE DROP LOGFILE GROUP 10;
```

Dropping a log member is only allowed when at least two members exist in the log group.  
The following is an example to drop the log member '/disk1/goldilocks_data/wal/redo_0_0.log'.

```
ALTER DATABASE DROP LOGFILE MEMBER '/disk1/GOLDILOCKS_data/wal/redo_0_0.log';
```

<a id="6b0d08290be77845"></a>
### Restoring Corrupted Redo Log File

If the system fails and the redo log files become corrupted, restart recovery will fail, and the system can not be operated. However, if there are normal log members present in the corrupted log group, you can recover the system by copying the log file from a normal log member to replace the corrupted log files. This allows restart recovery and system operation to proceed.

At this time, the log file that contains the log recorded at the ON_DISK_LSN in [V$CONTROLFILE](9-database-information.md#a50c1cf27fd41808) of the control file must exist in order to complete the recovery. If the log file does not exist, the recovery cannot be completed and the database can only be restarted after performing [incomplete recovery](7-backup-and-recovery-of-goldilocks-database.md#a7a4cbac95de9e6c).

If all log files in a log group are corrupted or if there is only one log member, the system can be restarted by performing incomplete media recovery. The incomplete media recovery is limited to normal log files.  
For more information about incomplete media recovery, refer to [Incomplete Recovery](7-backup-and-recovery-of-goldilocks-database.md#a7a4cbac95de9e6c).

<a id="cfc9d66c67548ce5"></a>
### Redo Log File Information

A user can query the V$LOGFILE view, which is a performance view to retrieve the location and name of the redo log files. When querying V$LOGFILE, information such as the log file name, its log group ID, its state, and the file size is retrieved as follows.

```
gSQL> SELECT FILE_NAME, GROUP_ID, GROUP_STATE, FILE_SIZE FROM V$LOGFILE;

FILE_NAME                          GROUP_ID GROUP_STATE FILE_SIZE
---------------------------------- -------- ----------- ---------
/disk1/goldilocks_data/wal/redo_0_0.log        0 INACTIVE    104857600
/disk1/goldilocks_data/wal/redo_1_0.log        1 CURRENT     104857600
/disk1/goldilocks_data/wal/redo_2_0.log        2 UNUSED      104857600
/disk1/goldilocks_data/wal/redo_3_0.log        3 UNUSED      104857600

4 rows selected.
```

<a id="774a4d55bc79a330"></a>
## Managing Archive Redo Log File

GOLDILOCKS redo log files reuse log groups that have been used, employing a *circular* log group structure. Therefore, for media recovery using backups, the database must be operated in archive log mode. In this mode, completed redo log files are copied to archive redo log files.  
For more information about the archive log mode in the GOLDILOCKS database, refer to [ARCHIVELOG Mode](7-backup-and-recovery-of-goldilocks-database.md#f25383eaa57ab850).

<a id="d7cdd67b3f591f73"></a>
### Creating Archive Redo Log File

The redo log file is copied to the archive redo log file directory by the log archiving thread, which is a system thread in the GOLDILOCKS database. The log archiving thread is activated by the checkpoint thread during a checkpoint, and it archives the appropriate redo log files.

The archive redo log file is created in the directory specified by the ARCHIVELOG_DIR_ 1 property. The name of the archive redo log file is composed of a prefix set by the ARCHIVELOG_FILE property and a sequence number corresponding to each redo log file.

<a id="3b91035465b1f665"></a>
### Maintaining and Dropping Archive Redo Log File

Media recovery using backups can fail if archive redo log files are arbitrarily dropped, just as with redo log files. Therefore, archive redo log files must be preserved along with backup files. When backup files are no longer needed, the corresponding archive redo log files required for media recovery using the backup can also be dropped.

A backup involves copying the data file that was downloaded to disk by the most recent checkpoint. Therefore, to recover media using a backup, you need the archive log files starting from the oldest LSN and later. A checkpoint occurs whenever a redo log file is switched, so one or more checkpoint logs are present in every log file except for the redo log file in the CURRENT state.

The following describes how to obtain the archive redo log files required for media recovery using a backup file:

1. Retrieve the checkpoint LSN recorded in the file header of the backup data files.
2. Identify the archive redo log files and locate the file that includes the checkpoint LSN.
3. The archive redo log files required for media recovery using the backup start from just before the archive redo log file identified in step 2.

Dump the control file and get the checkpoint LSN to get the archive redo log file needed for incremental backup. Subsequent process is the same as the entire backup process.

If backup files are no longer needed, the corresponding archive redo log files required for media recovery using those backups can also be deleted.

<a id="ff5309d1fa814d79"></a>
### Multiplexing Archive Redo Log File Directory

If an archive redo log file is moved from the directory specified by ARCHIVELOG_DIR_1 to another directory or media for preservation, media recovery may fail because the system will not be able to locate the required archive redo log file.

In this case, you can either move the relocated archive redo log file back to the directory specified by ARCHIVELOG_DIR_1 to proceed, or configure additional directories for the archive redo log files by setting ARCHIVELOG_DIR_2 through ARCHIVELOG_DIR_10. Ensure that READABLE_ARCHIVELOG_DIR_COUNT is set to the number of directories used (ARCHIVELOG_DIR_2 through ARCHIVELOG_DIR_10) to properly support media recovery.

<a id="88359ab2b5772eac"></a>
## Managing Tablespace

All data used by the database is stored in physical disk files, with the database's logical structure employed for efficient data management and performance. GOLDILOCKS efficiently manages disk space using logical structures such as tablespaces, segments, extents, and pages.

A tablespace can include multiple data files, and each tablespace can be set to online or offline to support high data availability. Additionally, distributing the disks that store data files enhances I/O performance and reduces contention for physical disk I/O.

<a id="ce91e2dfc308e200"></a>
### Tablespace Type

In GOLDILOCKS, tablespaces are categorized into SYSTEM tablespaces and non-SYSTEM tablespaces. The SYSTEM tablespace is created during database creation and is used and managed exclusively by the GOLDILOCKS system. Non-SYSTEM tablespaces, on the other hand, are created and utilized by users.

<a id="cbb718b7918d4bea"></a>
#### SYSTEM Tablespace

The SYSTEM tablespace is created when the GOLDILOCKS database is initialized and is essential for database operation. It includes the dictionary tablespace, undo tablespace, and system temporary tablespace.

<a id="5a738c92dc4ec792"></a>
#### Non-SYSTEM Tablespace

Non-SYSTEM tablespaces are used to store tables and indexes for data storage, and users can create or delete these tablespaces as needed.

<a id="8681d52d5d1969b6"></a>
### Managing Tablespace and Data File

<a id="8f6d07dd47ad7f3c"></a>
#### Managing Tablespace

<a id="843cc7f4d6019de3"></a>
##### Managing Tablespace State

The GOLDILOCKS database tablespace can be in either an online or offline state. An offline tablespace is not accessible. A user can set the tablespace to offline arbitrarily, or the system sets an abnormal tablespace to offline. However, the system tablespace must not be set to offline.

- Offline tablespace

The GOLDILOCKS database flushes all data files in the tablespace to disk before the tablespace is set to offline. Since flushing the data files requires all related logs to be flushed to disk as well, there is no need for special recovery when the tablespace later transitions back to online. However, any DDL operations that occurred while the tablespace was offline are applied when the tablespace state is changed to online.

A tablespace can be set to offline immediately using the IMMEDIATE mode, without flushing the data files. In this case, the tablespace state will be changed to online only after performing media recovery when the tablespace is set back to online.

**Tablespace offline option**

<a id="48808454f6ff667e"></a>
| Option | Description | Media recovery when setting  the tablespace to online |
| --- | --- | --- |
| NORMAL | Flushing all data file-related logs in the tablespace to disk, and then set the tablespace to offline | Media recovery is not required. |
| IMMEDIATE | Setting a tablespace to offline immediately | Media recovery is required. |

GOLDILOCKS can set a tablespace to offline during the mount phase. To do this, the service must be normally terminated, or the server must be operated in ARCHIVELOG mode. This method provides high availability by excluding unrecoverable tablespaces during database startup.

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE;
 
Tablespace altered.
 
gSQL> ALTER TABLESPACE TEST_TBS ONLINE;
 
Tablespace altered.
```

```
gSQL> ALTER TABLESPACE TEST_TBS OFFLINE IMMEDIATE;
 
Tablespace altered.
 
gSQL> ALTER TABLESPACE TEST_TBS ONLINE;
 
ERR-42000(14051): media recovery required - 'TEST_TBS'
 
gSQL> ALTER DATABASE RECOVER TABLESPACE TEST_TBS;
 
Database altered.
 
gSQL> ALTER TABLESPACE TEST_TBS ONLINE;
 
Tablespace altered.
```

<a id="ec620f0cbc7c5959"></a>
##### Attributes of Tablespace

The following are attributes of a tablespace in the GOLDILOCKS database. PERSISTENT or TEMPORARY indicates whether the persistence of the tablespace is ensured. DATA or UNDO specifies the type of tablespace and the kind of data it stores.

<a id="8124b75704f27b01"></a>
<table class="table column_count_3"><caption>Tablespace attribute of GOLDILOCKS database</caption><thead><tr><th class="to_center" colspan="2"><div>Attribute</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Persistence</div></td><td class="to_left to_middle"><div>PERSISTENT</div></td><td class="to_middle"><div>It supports the persistence of data stored in a tablespace. (A recovery is required.)</div></td></tr><tr><td class="to_middle"><div>TEMPORARY</div></td><td class="to_middle"><div>It does not support the persistence of data stored in a tablespace.</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Type of stored data</div></td><td class="to_middle"><div>DATA</div></td><td class="to_middle"><div>It stores the user-input data.</div></td></tr><tr><td class="to_middle"><div>UNDO</div></td><td class="to_middle"><div>It stores data required for MVCC of the database.</div></td></tr><tr><td class="to_middle"><div>DICT</div></td><td class="to_middle"><div>It stores dictionary information for database operations.</div></td></tr><tr><td class="to_middle"><div>TEMPORARY</div></td><td class="to_middle"><div>It stores data for SQL processing.</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Type of stored media</div></td><td class="to_middle"><div>DISK</div></td><td class="to_middle"><div>Pages of the disk tablespace must be read from the disk data file using the buffer cache. If the pages are cached, they will be accessible in the buffer cache.</div></td></tr><tr><td class="to_middle"><div>MEMORY</div></td><td class="to_middle"><div>When creating a tablespace, exclusive shared memory is allocated with a size equal to that of the data file. This allows for instant access to the desired page in memory.</div></td></tr></tbody></table>

<a id="35c0472a3359fb49"></a>
##### Managing Tablespace

- Creating user tablespace

It creates a new user tablespace. The name of the tablespace used in the database instance must be unique when creating the tablespace. A tablespace can contain up to 1024 data files. In a memory tablespace, each data file can store up to 30 Gbyte, while in a disk tablespace, the data file can store as much data as the physical disk allows. The database can create up to 65,535 tablespaces, including the system tablespace.

The name of each data file, including its absolute path, must be unique. Use the 'REUSE' option to reuse an existing data file that is not currently in use by the database. The extent size of a tablespace can be selected from 64 Kbyte, 128 Kbyte, 256 Kbyte, 512 Kbyte, or 1 Mbyte, with the default extent size being 256 Kbyte.

```
gSQL> CREATE TABLESPACE TEST_TBS DATAFILE
     '/goldilocks1/db/TEST_TBS1.dbf' SIZE 20M,
     '/goldilocks2/db/TEST_TBS2.dbf' SIZE 50M,
     '/goldilocks3/db/TEST_TBS3.dbf' SIZE 100M REUSE;

Tablespace created.
```

The following is an example of creating a disk tablespace.

```
gSQL> CREATE DISK TABLESPACE TEST_TBS DATAFILE
     '/goldilocks1/db/TEST_DISK_TBS1.dbf' AUTOEXTEND OFF MAXSIZE 20M,
     '/goldilocks2/db/TEST_DISK_TBS2.dbf' AUTOEXTEND ON NEXT 20M MAXSIZE UNLIMITED REUSE;

Tablespace created.
```

When creating a tablespace, you can set its state to ONLINE or OFFLINE, and also specify the LOGGING or NOLOGGING property.

- Dropping tablespace

A tablespace and its data files can be dropped when they are no longer needed. Unused tablespaces should be dropped to avoid wasting resources. This is because once a tablespace is created, the added disk data files and memory allocations are created and remain in use.

```
gSQL> DROP TABLESPACE TEST_TBS;

Tablespace dropped.
```

Dropping a tablespace does not, by default, drop the table indexes in use. Therefore, the *INCLUDING CONTENTS* option must be used together when dropping a tablespace that contains tables or indexes in use.

```
gSQL> DROP TABLESPACE TEST_TBS;

ERR-42000(16148): tablespace not empty, use INCLUDING CONTENTS option : 
drop tablespace TEST_TBS
                *
ERROR at line 1:

gSQL> DROP TABLESPACE TEST_TBS INCLUDING CONTENTS;

Tablespace dropped.
```

Use the *AND DATAFILES* option to also drop the data files added to the tablespace.

```
gSQL> DROP TABLESPACE TEST_TBS INCLUDING CONTENTS AND DATAFILES;

Tablespace dropped.
```

- Altering tablespace size

To alter the size of a tablespace, you can add data files to or drop data files from the tablespace. Add new data files to the tablespace when additional storage space is needed during database operations. Conversely, drop unused data files from the tablespace to avoid wasting space.

```
gSQL> ALTER TABLESPACE TEST_TBS ADD DATAFILE 'TEST_TBS2.dbf' SIZE 20M;

Tablespace altered.

gSQL> ALTER TABLESPACE TEST_TBS DROP DATAFILE 'TEST_TBS2.dbf;

Tablespace altered.
```

A data file can only be dropped from a tablespace if it has never been used since its creation. Once a data file has been used, it cannot be dropped, even if all the data has been removed.

```
ALTER TABLESPACE TEST_TBS DROP DATAFILE 'TEST_TBS2.dbf';

ERR-42000(14044): datafile not empty
```

- Managing temporary tablespace

A temporary tablespace does not store data files, but allocates memory of a specified size. Create a temporary tablespace as follows.

```
gSQL> CREATE TEMPORARY TABLESPACE TEST_TBS MEMORY 'TEST_TEMP_TBS' SIZE 10M EXTSIZE 256K;

Tablespace created.
```

Add memory to the temporary tablespace as follows.

```
gSQL> ALTER TABLESPACE TEST_TBS ADD MEMORY 'TEST_TBS2' SIZE 10M;

Tablespace altered.
```

Drop unused memory from the temporary tablespace as follows.

```
gSQL> ALTER TABLESPACE TEST_TBS DROP MEMORY 'TEST_TBS2';

Tablespace altered.
```

Drop the temporary tablespace as follows.

```
gSQL> DROP TABLESPACE TEST_TBS INCLUDING CONTENTS AND DATAFILES;

Tablespace dropped.
```

<a id="34aa1844cd25556a"></a>
##### Transferring Data File

The data file storage path stored in the database must be modified when altering the datafile's storage disk or directory.

The following is an example to describe how to modify the path when transferring the datafile '/goldilocks1/db/TEST_TBS1.dbf' in tablespace TEST_TBS to '/goldilocks4/db/TEST_TBS1.dbf'.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE
    '/goldilocks1/db/TEST_TBS1.dbf' TO '/goldilocks4/db/TEST_TBS1.dbf';

Tablespace altered.
```

<a id="d3d87684c641b3db"></a>
#### Tablespace Information

For more information about the tablespaces created in the database, refer to [V$TABLESPACE](9-database-information.md#6a44f779a7259a10).

```
gSQL> \DESC V$TABLESPACE

COLUMN_NAME   TYPE                   IS_NULLABLE
------------- ---------------------- -----------
TBS_NAME      CHARACTER VARYING(128) FALSE      
TBS_ID        NUMBER                 FALSE      
TBS_ATTR      CHARACTER VARYING(128) FALSE      
IS_LOGGING    BOOLEAN                FALSE      
IS_ONLINE     BOOLEAN                FALSE      
OFFLINE_STATE CHARACTER VARYING(32)  FALSE      
EXTENT_SIZE   NUMBER                 FALSE      
PAGE_SIZE     NUMBER                 FALSE
```

<a id="534aeb00e2b7507a"></a>
## Managing Data File

<a id="d2a9057ae53dee90"></a>
### Data File Matching

A data file can become corrupted due to disk failure, database defects, or human error. If a corrupted data file is used in the database, it can lead to serious problems.

The GOLDILOCKS database ensures data file integrity by using a checksum for each page of the data file. The page checksum is generated using LSN and CRC value, and is stored on each page. Users can set the page checksum type using the value in [PAGE_CHECKSUM_TYPE](10-server-property.md#45271d23b2ad2617), with LSN being the default value.

The page checksum is verified when loading the data file into memory at database startup. If an error occurs with the checksum value, the database service can not start.

The following is an example to describe a database startup failure when the datafile TEST_TBS.dbf in the user-created tablespace TEST_TBS does not match.

```
gSQL> \STARTUP MOUNT

Startup success

gSQL> ALTER SYSTEM OPEN DATABASE;

ERR-HY000(14094): datafile recovery required - datafile(/goldilocks/db/TEST_TBS.dbf) of tablespace(TEST_TBS) corrupted
```

If the data file does not match, set the tablespace containing the data file to *OFFLINE*, or recover the data file to restart the database.

The following describes how to start up the database after setting the tablespace to *OFFLINE*.

```
gSQL> \STARTUP MOUNT

Startup success

gSQL> ALTER SYSTEM OPEN DATABASE;

ERR-HY000(14094): datafile recovery required - datafile(/goldilocks/db/TEST_TBS.dbf) of tablespace(TEST_TBS) corrupted

gSQL> ALTER TABLESPACE TEST_TBS OFFLINE IMMEDIATE;

Tablespace altered.

gSQL> ALTER SYSTEM OPEN DATABASE;

System altered.
```

A full backup or incremental backup of the data file must exist when recovering the data file. The following describes how to recover the data file when a backup is available.

```
gSQL> \STARTUP MOUNT

Startup success

gSQL> ALTER SYSTEM OPEN DATABASE;

ERR-HY000(14094): datafile recovery required - datafile(/goldilocks/db/TEST_TBS.dbf) of tablespace(TEST_TBS) corrupted

gSQL> ALTER DATABASE RECOVER DATAFILE 'TEST_TBS.dbf' CORRUPTION;

Database altered.

gSQL> ALTER SYSTEM OPEN DATABASE;

System altered.
```

<a id="b0e165cb30d5ba88"></a>
### Data File Information

For more information about the data files being used in the database, refer to [V$DATAFILE](9-database-information.md#62f407c3ba7f72da).

```
gSQL> \DESC V$DATAFILE

COLUMN_NAME    TYPE                           IS_NULLABLE
-------------- ------------------------------ -----------
TBS_NAME       CHARACTER VARYING(128)         FALSE      
DATAFILE_NAME  CHARACTER VARYING(1024)        FALSE      
CHECKPOINT_LSN NUMBER                         FALSE      
CREATION_TIME  TIMESTAMP(6) WITHOUT TIME ZONE FALSE      
FILE_SIZE      NUMBER                         FALSE
```

<a id="325c77f9c005172a"></a>
## Buffer Cache

<a id="2768c5890b046153"></a>
### Structure of GOLDILOCKS Buffer Cache

It caches pages required from the disk data file to access index pages and tables stored in the disk tablespace into the buffer. GOLDILOCKS allocates the buffer cache based on the size set in the [BUFFER_CACHE_SIZE](10-server-property.md#42a6f9bb91593e38) property and retrieves requested pages from the page cached in the buffer cache using a hash table sized according to the [BUFFER_HASH_BUCKETS](10-server-property.md#e16f49d6d65cd213) property. The touch count is incremented each time a page is accessed. If there is no available space in the buffer cache, the LRU strategy is employed, which replaces the page with the smallest touch count value.

<a id="dc1039ec68402f6a"></a>
![Structure of GOLDILOCKS buffer cache](../assets/images/25623285c0d7abe3.png)

<a id="831efcc3592e1214"></a>
### Buffer Cache List

The following lists are used for the buffer cache in GOLDILOCKS:

**Buffer cache list**

<a id="08744eb8948c87e9"></a>
| List | Description | Property |
| --- | --- | --- |
| Buffer free list | It is a list of buffer frames that are immediately available. | BUFFER_FREE_LIST_COUNT |
| Buffer LRU list | It is a list used to retrieve pages that are reusable, based on the touch count. | BUFFER_LRU_LIST_COUNT |
| Buffer flush list | It is a list of buffer frames used to reflect updated pages from the buffer LRU list to the data file for reuse. | PARALLEL_IO_FACTOR |
| Buffer checkpoint list | It is a list of updated page frames that must be flushed to the data file during a checkpoint. | CHECKPOINT_LIST_COUNT_PER_IO_GROUP |

Page frames that have not been used since system startup are linked to the buffer free list, while used page frames are linked to the buffer LRU list. Page frames that are updated in the buffer cache are linked to the buffer checkpoint list, but they are not dropped from the buffer LRU list.

When all page frames in the buffer free list are used and there is no available page frame to cache a new page, the system looks for an available page frame by retrieving from the buffer LRU list. At this point, any page frames that have been updated but are not in use are moved to the buffer flush list.

A page frame cannot be redundantly linked to the buffer free, LRU, or flush lists, except for the buffer checkpoint list. In other words, a page frame in the buffer free list cannot simultaneously be in the buffer LRU or flush lists, and a page frame in the buffer LRU list cannot exist in the buffer free or flush lists.

The buffer LRU list is divided into hot/ cold areas. If the touch count of a page frame in the cold area meets or exceeds the specified value ([BUFFER_HOT_REGION_CRITERIA](10-server-property.md#5efa1717c0b99abc)), it is transferred to the hot area. The touch count of page frames in the buffer LRU list increases with each access. If all page frames belong to the hot area, no page frame is available for replacement. Therefore, the size of the hot area is limited by the [BUFFER_HOT_REGION_PERCENT](10-server-property.md#c6fa75007e908adc) property value.

<a id="db1388c38d43b4b0"></a>
### Page Frame Status

All page frames in the buffer cache have the following statuses.

**Buffer frame status**

<a id="93bb600e394c0377"></a>
| Status | Description | Page frame access |
| --- | --- | --- |
| FREE | It is a page frame that is not currently in use. | Inaccessible |
| PREPARED | It is allocated for page caching but has not been fully read from the disk. | Inaccessible |
| CLEAN | The page has been cached in the buffer cache but the page frame has never been updated. | Accessible |
| DIRTY | The page has been cached in the buffer cache, and the page frame has been updated. | Accessible |
| FLUSHING | The page has been cached in the buffer cache, the page frame has been updated, and it is being flushed to the disk data file. | Accessible |
| INCONSISTENT | The page frame status is abnormal in the buffer cache. | Inaccessible |

---

[← 5. Basic Management of GOLDILOCKS Database](5-basic-management-of-goldilocks-database.md) · [Table of contents](../README.md) · [7. Backup and Recovery of GOLDILOCKS Database →](7-backup-and-recovery-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
