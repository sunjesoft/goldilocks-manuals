<a id="3ae338b18fe83e54"></a>

# 10. Server Property

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/3ae338b18fe83e54)  
> Tag: `26c.1_0_tag`

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="7578401839846138"></a>
## Server Property Information

For more information about SQL syntax to change properties, refer to the following.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#ca16f1acaf4c1a9b)
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#a7df2194f3a8476a)

For more information about property types, refer to the following.

- [V$PROPERTY](9-database-information.md#3bbd715bcc26bde5): It displays the list of properties that can be altered while the system is operating or during a restart.
- [V$SPROPERTY](9-database-information.md#8d1cc08113922f30): It represents either the property set by reading the binary file or the list of properties stored in the binary file. 
- [V$DB_PROPERTY](9-database-information.md#5dce0d3509d51946): It is a read-only property list that can only be altered when creating the database and can not be altered afterward.

The following describes the basic information items about properties in this manual.

**Basic Information item of property**

<a id="d59fca61a5e9e699"></a>
| Item | Description |
| --- | --- |
| Name | Property name |
| Summary | Short description of the property |
| Data type | Data type of the property value |
| Applicable phase | A startup phase that can be updated using ALTER SYSTEM or ALTER SESSION * NONE: The applicable phase does not exist. (If it can be updated but the applicable phase is NONE, use the *SCOPE = FILE* option.) |
| Updatable | Whether property is updatable or not * If the property value is TRUE, it is updatable.  * If the property value is FALSE, only read-only access is allowed. |
| ALTER SESSION | Whether the property is updatable using [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#a7df2194f3a8476a) |
| ALTER SYSTEM | Whether the property is updatable using [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#ca16f1acaf4c1a9b) * IMMEDIATE: The updated value is immediately reflected in all sessions after execution. * DEFERRED: The updated value is reflected only in sessions that connect after execution. However, it will not affect already connected sessions. * FALSE: The updated value is not reflected in the session during execution. However, the updated value will be reflected after a restart, (Properties are updatable only using the *SCOPE=FILE* option.) * NONE: The property is not updatable. |
| MIN | If the data type is BIGINT, it represents the minimum value of the property. If the data type is VARCHAR, the minimum value of the property is N/A. |
| MAX | If the data type is BIGINT, it represents the maximum value of the property. If the data type is VARCHAR, the maximum value of the property is N/A. |
| Default value | Default value of the property |

<a id="838bba16ab8e16b6"></a>
## Property Alias Information

The information about the property alias can be viewed through [V$PROPERTY_ALIAS](9-database-information.md#646bbdf99cd7a3c0).

The basic information about the property alias provided in this manual is as follows.

<a id="3f569e92536a6a94"></a>
| Item | Description |
| --- | --- |
| Original name | It is the original name of the property. |
| ALIAS | It is the name of the property alias. |

For more information about the property alias list, refer to [Property Alias](../part-01-getting-started/4-what-s-new.md#578e12425e1987b4).

<a id="14eb98fb03731e6f"></a>
### CDISPATCHER_THREADS

It is an alias for [CDISPATCHER_LOCKABLE_THREADS](#fdfb51d52a773c11).

<a id="755972f052be5140"></a>
### CLUSTER_COMMIT_SLAVES

It is an alias for [CLUSTER_COMMIT_SLAVE_CSERVERS](#a9417dd71332949a).

<a id="72d2344515d6a037"></a>
### CLUSTER_SERVER_RESPONSE_ QUEUE_SIZE

It is an alias for [CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE](#4479a9182623b5ec).

<a id="86311c00710ce5e3"></a>
### CSERVER

It is an alias for [CLUSTER_LOCKABLE_CSERVERS](#9020e957dde68206).

<a id="8804bb71f889adf0"></a>
### INCREMENTAL_CHECKPOINT_CRITERIA

It is an alias for [BUFFER_DIRTY_PAGE_LIMIT](#5c88ba27554a8c6b).

<a id="9764aad05cec29a3"></a>
### INDEX_LOGGING_THROTTLING

It is an alias for [REDO_LOGGING_THROTTLING](#fc97a492acbd2b65).

<a id="a5e77ba13d37ebb8"></a>
### INST_TABLE_BLOCK_SIZE

It is an alias for [INST_TABLE_PAGE_SIZE](#b88cb19b3df8ec64).

<a id="e20f14532c59b0ff"></a>
### LOCKLESS_CSERVERS

It is an alias for [CLUSTER_LOCKLESS_CSERVERS](#3fe09fe1c9a0e8eb).

<a id="41f664f7c9f0ea59"></a>
### MAXIMUM_JOURNAL_REPLAY_COUNT

It is an alias for ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT.

<a id="6739454e6e90ac05"></a>
### MEMORY_MERGE_RUN_COUNT

It is an alias for [INDEX_MERGE_RUN_COUNT](#589f961b7faeb58f).

<a id="cc6fadf79326ccf9"></a>
### MEMORY_SORT_RUN_SIZE

It is an alias for [INDEX_SORT_RUN_SIZE](#b49e5c4915accfc6).

<a id="d1f0ca9e9460368a"></a>
### ONLINE_JOURNAL_REPLAY_THRESHOLD

This is an alias for [ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD](#6d34d4485d097e76).

<a id="2a27486980a4c5d5"></a>
### REBALANCE_BLOCK_READ_COUNT

This is an alias for [ONLINE_DDL_BLOCK_READ_COUNT](#01c6d9aec58015c6).

<a id="ff73df2a9aab0ece"></a>
### REBALANCE_SHARD_DIVISOR

This is an alias for [ONLINE_DDL_SCAN_PARTITION](#10db0f046d22a3e2).

<a id="45361fa02b6376bd"></a>
### SYSTEM_LOGGER_DIR

It is an alias for [TRACE_SYSTEM_DIR](#03a6bc4279f688d4).

<a id="08e3490fe158fb81"></a>
## ADMIN_SESSION_POOL_INIT_SIZE

<a id="53b725c3f139f55e"></a>
### Basic Information

<a id="af57eccfd3b0cc9c"></a>
| Item | Description |
| --- | --- |
| Name | ADMIN_SESSION_POOL_INIT_SIZE |
| Summary | initial memory size for admin session pool |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1099511627776 (1T) |
| Default value | 10485760 (10M) |

<a id="d75633fc391431b6"></a>
### Description

It sets the initial memory size for the admin session pool.

<a id="1180f146b146ac2c"></a>
## ADMIN_SESSION_POOL_NEXT_SIZE

<a id="f0d7f492ba6d2d62"></a>
### Basic Information

<a id="e71af81ef945fa87"></a>
| Item | Description |
| --- | --- |
| Name | ADMIN_SESSION_POOL_NEXT_SIZE |
| Summary | memory size to be expanded in admin session pool |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 1048576 (1M) |

<a id="be6d452aaa1d634c"></a>
### Description

It sets how much to extend the memory size in the session pool when expanding the admin session pool space.   
This setting is valid only when ADMIN_SESSION_POOL_INIT_SIZE is greater than 0.

<a id="6d1a131faafd3dd0"></a>
## AGING_INTERVAL

<a id="7f08e32e7b6be9b9"></a>
### Basic Information

**Basic Information of AGING_INTERVAL**

<a id="b8a7b69b0d39af11"></a>
| Item | Description |
| --- | --- |
| Name | AGING_INTERVAL |
| Summary | aging interval time(ms) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| Default value | 10 |

<a id="903188be6d2ffba2"></a>
### Description

It sets the idle time (in seconds) when an ager thread that deletes previous version data in an MVCC-based database has no jobs to process.

<a id="f172c22d22687c8a"></a>
## AGING_PLAN_INTERVAL

<a id="942e96e2781dea6a"></a>
### Basic Information

**Basic Information of AGING_PLAN_INTERVAL**

<a id="1053a86e95dd7fd9"></a>
| Item | Description |
| --- | --- |
| Name | AGING_PLAN_INTERVAL |
| Summary | aging plan interval time(s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 31536000 |
| Default value | 3 |

<a id="ad034115d2d4e3ae"></a>
### Description

The SQL plan that is older than AGING_PLAN_INTERVAL becomes the aging target.

<a id="5d1bcc692e3875ff"></a>
## ARCHIVE_LOG_THROTTLING

<a id="404dc4670aa51690"></a>
### Basic Information

<a id="4e0baae952a96afb"></a>
| Item | Description |
| --- | --- |
| Name | ARCHIVE_LOG_THROTTLING |
| Summary | I/O throttling threshold for redo log archiving |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 |
| Default value | 0 |

<a id="2c00d9af2a2543c3"></a>
### Description

This property is used to control disk I/O performance during redo log archiving.   
It causes the process to sleep each time the amount of data copied to the destination file exceeds the specified property value.

<a id="06ffb701c965428b"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="a1b125328bc654f3"></a>
### Basic Information

**Basic Information of ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10**

<a id="911ce0a55b868fbf"></a>
| Item | Description |
| --- | --- |
| Name | ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10 |
| Summary | archive log directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE(ARCHIVELOG_DIR_1), TRUE(ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10) |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/archive_log |

<a id="f5d7cd9de97d6de7"></a>
### Description

It specifies the archiving directory for the GOLDILOCKS database's online redo log files. It also indicates where to read archive redo log files during media recovery. The online redo log file creates archive redo log files only in ARCHIVELOG_DIR_1.

ARCHIVELOG_DIR_1 can only be set at the system level, while ARCHIVELOG_DIR_2 to ARCHIVELOG_DIR_10 can be set at the session level.

<a id="7022a5c8a8d20924"></a>
## ARCHIVELOG_FILE

<a id="6d0ba34476791898"></a>
### Basic Information

**Basic Information of ARCHIVELOG_FILE**

<a id="24baa5872f5751cc"></a>
| Item | Description |
| --- | --- |
| Name | ARCHIVELOG_FILE |
| Summary | default archive log file |
| Data type | VARCHAR |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | archive |

<a id="e172db4c0275014f"></a>
### Description

It sets the prefix of the targeted file name stored in the archive directory when archiving the online redo logfile. The archive logfile's name consists of the prefix defined in ARCHIVELOG_FILE, followed by '_', the file sequence and the file extension 'log'. For example, the online logfile with a sequence number of 0 is archived as 'archive_0.log'.

<a id="77dbfbbfacf55659"></a>
## ARCHIVELOG_MODE

<a id="8e79daa2dd010f21"></a>
### Basic Information

**Basic Information of ARCHIVELOG_MODE**

<a id="bbc3c5179f798e0b"></a>
| Item | Description |
| --- | --- |
| Name | ARCHIVELOG_MODE |
| Summary | archive log mode(0:disable, 1:enable) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="39a13840737b74c9"></a>
### Description

The property is applied during database creation. The archivelog mode can be set to one of the following values.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

It does not affect the archive log mode during operation after the database is created. The archive log mode can be modified using the command ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG} during the MOUNT phase.

<a id="5f1c1192895e8d41"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="e7a34569592fab7e"></a>
### Basic Information

**Basic Information of BACKUP_DIR_1 ~ BACKUP_DIR_10**

<a id="8d59c19f0a9b2388"></a>
| Item | Description |
| --- | --- |
| Name | BACKUP_DIR_1 ~ BACKUP_DIR_10 |
| Summary | backup directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE(BACKUP_DIR_1), TRUE(BACKUP_DIR_2 ~ BACKUP_DIR_10) |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/backup |

<a id="4bdfe97bd1f3fc48"></a>
### Description

A backup file is created when an incremental backup is performed, and the directory for reading the backup file is set for restoring files using the incremental backup. Incremental backups are created only in the directory specified by BACKUP_DIR_1.

BACKUP_DIR_1 can only be set for the system, while BACKUP_DIR_2 to BACKUP_DIR_10 can be set for the session.

<a id="d15f655b49f8124e"></a>
## BLOCK_READ_COUNT

<a id="ec20ee8f2c14f673"></a>
### Basic Information

**Basic Information of BLOCK_READ_COUNT**

<a id="ff0abbc6a66904aa"></a>
| Item | Description |
| --- | --- |
| Name | BLOCK_READ_COUNT |
| Summary | value count for a block read |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| Default value | 20 |

<a id="fee79d38db4aa0fc"></a>
### Description

The SQL operation executes by reading rows in units defined by BLOCK_READ_COUNT, which represents a bundle of rows. BLOCK_READ_COUNT specifies the number of rows to be processed at a time during execution. It serves as the basic unit in the pipelining process of execution nodes used in SQL query processing.

If the value of BLOCK_READ_COUNT is large, processing performance improves, but it consumes more memory resources. A value between 10 and 100 is recommended. If the value exceeds 100, resource usage increases proportionately, but the performance improvement does not scale proportionately

<a id="7976cb05a3889bcc"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="ab2da819e97d947f"></a>
### Basic Information

<a id="fbf557a14f4fdd49"></a>
| Item | Description |
| --- | --- |
| Name | BROADCAST_INDEX_REBUILD_PROTOCOL |
| Summary | broadcast index rebuild protocol |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="13fdb17d4b1ca5bd"></a>
### Description

It determines whether to rebuild indexes simultaneously on multiple members when performing index reconstruction in a clustered environment.

<a id="07a4aea8a6776250"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="84c0a7e23b4cf0a0"></a>
### Basic Information

<a id="3e71d401a0ee8462"></a>
| Item | Description |
| --- | --- |
| Name | BROADCAST_REBALANCE_PROTOCOL |
| Summary | broadcast rebalance protocol |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="248651caf291a2d1"></a>
### Description

It determines whether to simultaneously process protocols that can be handled by multiple members during table rebalancing in a clustered environment.

<a id="42a6f9bb91593e38"></a>
## BUFFER_CACHE_SIZE

<a id="fa48c36797c0e626"></a>
### Basic Information

<a id="833c9e461a9041c0"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_CACHE_SIZE |
| Summary | buffer cache size ( byte ) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 MB |
| MAX | 1 TB |
| Default value | 64 MB |

<a id="7539b562ab311d69"></a>
### Description

It sets the size of the buffer that caches pages in the disk tablespace.

<a id="f9e7c75e6ce5e74c"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

> It has not been supported since version 21c.1.

<a id="c8262670d52d1b28"></a>
### Basic Information

<a id="c0500bbdbe499359"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_CHECKPOINT_LIST_COUNT |
| Summary | number of buffer checkpoint lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 36 |
| Default value | 1 |

<a id="cd8e5fd46288d17b"></a>
### Description

It is linked to the checklist when pages in the disk tablespace cached in the buffer are updated. Each checkpoint list flushes the updated pages associated with it to disk using its own flush thread. The parameter BUFFER_CHECKPOINT_LIST_COUNT sets both the number of checkpoint lists and the number of flush threads.

<a id="5c88ba27554a8c6b"></a>
## BUFFER_DIRTY_PAGE_LIMIT

<a id="4a5a0fe3d7c0ae5a"></a>
### Basic Information

<a id="12a5bd42cef83265"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_DIRTY_PAGE_LIMIT |
| Summary | a limit on the number of dirty pages in the buffer cache |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 134217728 |
| Default value | 0 |

<a id="2f6aa8c3a43ec3e2"></a>
### Description

Pages updated in the system buffer cache are written to disk at each checkpoint. If the buffer cache size is large and there are many updated pages, the checkpoint process can take a long time, affecting service performance. GOLDILOCKS performs incremental checkpoints, applying updated pages to disk when the number of modified pages exceeds a specified threshold. The parameter BUFFER_DIRTY_PAGE_LIMIT sets the criteria for initiating the incremental checkpoint.

For example, if this value is set to 1000 and the number of updated pages in the system is less than 1000, the updated pages will not be written to disk. However, if the number of updated pages is 1000 or more, the pages in the buffer will be applied to the disk.

The default value is 0, which indicates infinity. In this case, incremental checkpoints are not performed, even if all cached pages in the buffer are updated.

Set the appropriate values for BUFFER_DIRTY_PAGE_LIMIT and [INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA](#208b2579f8a70601), taking into account the restart recovery time and its impact on service performance.

<a id="dc517f173dca26e6"></a>
### ALIAS

<a id="e6b4b8488c864034"></a>
| Item | Description |
| --- | --- |
| Original name | BUFFER_DIRTY_PAGE_LIMIT |
| ALIAS | INCREMENTAL_CHECKPOINT_CRITERIA |

<a id="54d171222ffcdfe4"></a>
## BUFFER_FLUSH_THREADS

> It has not been supported since version 21c.1.

<a id="ef0e435d3f3a4ec8"></a>
### Basic Information

<a id="7be88fc9648a52d4"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_FLUSH_THREADS |
| Summary | number of buffer flush threads |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 36 |
| Default value | 1 |

<a id="c5c68f6bbedd8967"></a>
### Description

To reuse the bch that has cached updated pages in the lru list, it connects to the flush list and requests a flush from the buffer flusher. In this case, BUFFER_FLUSH_THREADS sets the number of buffer flushers and flush lists to be used in the database.

<a id="1b01f3a3b0c82701"></a>
## BUFFER_FLUSHING_INTERVAL

> It has not been supported since version 21c.1.

<a id="1f610bd8c898b0e3"></a>
### Basic Information

<a id="5bd005ee4cee20a8"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_FLUSHING_INTERVAL |
| Summary | buffer flushing interval time (sec) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 86400 (1 day) |
| Default value | 3 |

<a id="81a00c8982e84c1c"></a>
### Description

It sets the idle time (in seconds) for the buffer flusher when there are no jobs to process for flushing updated disk tablespace pages to disk.

<a id="428d06a5aecd8efd"></a>
## BUFFER_FREE_LIST_COUNT

<a id="54524214c9b123d5"></a>
### Basic Information

<a id="c9f9931cefef595c"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_FREE_LIST_COUNT |
| Summary | number of buffer free lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 64 |
| Default value | 16 |

<a id="56037d787a1a19c8"></a>
### Description

It sets the number of buffer free lists that connect to the bch entries available for immediate use in the buffer cache.

<a id="e16f49d6d65cd213"></a>
## BUFFER_HASH_BUCKETS

<a id="4d103e5530fa5ff6"></a>
### Basic Information

<a id="fffe1dae21de2269"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_HASH_BUCKETS |
| Summary | number of buffer hash buckets |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1073741824 |
| Default value | 0 |

<a id="48dd366b0b34f563"></a>
### Description

It sets the number of hash buckets for the disk tablespace pages cached in the buffer. This value can range from 0 to 1,073,741,824, with 0 indicating that the number of hash buckets is calculated based on the number of pages that can be cached in the buffer according to BUFFER_CACHE_SIZE. If the buffer size is smaller than the specified value, the number of hash buckets will be adjusted to match the buffer size.

<a id="5efa1717c0b99abc"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="532aa93151cb4f3d"></a>
### Basic Information

<a id="2adc18178ece9b25"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_HOT_REGION_CRITERIA |
| Summary | threshold touch count of hot region in the buffer lru list |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 100 |
| Default value | 2 |

<a id="4091ff8d9c777c9f"></a>
### Description

It sets the touch count to transfer pages from the cold region to the hot region in the buffer LRU list.

<a id="c6fa75007e908adc"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="c0fe58efc2a47f40"></a>
### Basic Information

<a id="cfd59d11af29d1eb"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_HOT_REGION_PERCENT |
| Summary | the percentage of hot region in the buffer lru list |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 80 |
| Default value | 50 |

<a id="1e75f5aaa30ab364"></a>
### Description

It sets the proportion (percentage) of hot region pages relative to the total number of pages in the buffer LRU list.

<a id="689479763f022f45"></a>
## BUFFER_LRU_LIST_COUNT

<a id="5b1f521b0a9fd69e"></a>
### Basic Information

<a id="17ad72a18af3f8d7"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_LRU_LIST_COUNT |
| Summary | number of buffer LRU lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 64 |
| Default value | 16 |

<a id="9b7c585b7d286319"></a>
### Description

It sets the number of LRU lists used to select a victim from the pages in use when there are no free buffers available for caching disk tablespace pages.

<a id="d2822bb6ed31f752"></a>
## BUFFER_LRU_SCAN_PERCENT

<a id="45c2ccc4d2ff43c1"></a>
### Basic Information

<a id="bc5985c36c3ef538"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_LRU_SCAN_PERCENT |
| Summary | the percentage of buffers to inspect when looking for free |
| Data type | NO MOUNT or above |
| Applicable phase | TRUE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10 |
| MAX | 100 |
| Default value | 40 |

<a id="636b29de38a0c7fd"></a>
### Description

If no free buffer is currently available in the system, it searches the lru list for a reusable buffer to cache the disk tablespace page. BUFFER_LRU_SCAN_PERCENT specifies the percentage of buffer pages defined in [BUFFER_CACHE_SIZE](#42a6f9bb91593e38), which determines the number of pages to check in the lru list to find a reusable buffer.

<a id="c2eacf16a5019755"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="5e24c9ed277bc7e5"></a>
### Basic Information

<a id="b0e8c655ed5bb503"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_MULTIPAGE_READ_COUNT |
| Summary | maximum number of pages read in one I/O operation during a full scan |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 128 |
| Default value | 32 |

<a id="9289eb7274e0c665"></a>
### Description

It sets the maximum number of pages to be used for a single disk I/O operation when performing a full scan of the disk table.

<a id="dd8c6dd0a411e1be"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="485360f10365a6db"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="a4ccc8d82967335f"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_PREFETCH_PAGE_COUNT |
| Summary | the maximum number of pages to be prefetched to the buffer per I/O operation |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 128 |
| Default value | 4 |

<a id="bde17005b4afd6f3"></a>
### Description

It sets the maximum number of nearby pages to be prefetched per disk I/O when accessing a page in the disk tablespace that is not present in the buffer.

<a id="0de67ba114808601"></a>
## BULK_IO_PAGE_COUNT

<a id="f92eccef5e943732"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="b8cd87424d67fee2"></a>
| Item | Description |
| --- | --- |
| Name | BULK_IO_PAGE_COUNT |
| Summary | page count for bulk IO operation |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 128 |
| MAX | 131072 |
| Default value | 3840 |

<a id="9e4c4e45d5c2f248"></a>
### Description

It is used when an I/O READ of the data file occurs during server restart, or when an I/O WRITE takes place while creating a data file.

Heap memory is allocated to a size of BULK_IO_PAGE_COUNT * 8192 when the server restarts or a data file is created. If the session's PRIVATE_STATIC_AREA_SIZE is smaller than the allocated heap memory size, an insufficient memory error may occur. In this case, you should extend PRIVATE_STATIC_AREA_SIZE.

<a id="1014a49724e1ea25"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="2b8506ea73a77a01"></a>
### Basic Information

**Basic Information of CDISPATCHER_HOT_POLICY_INTERVAL**

<a id="05c4388821dca027"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_HOT_POLICY_INTERVAL |
| Summary | cdispatcher dequeue interval for busy waiting ( micro second ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000 (1day) |
| Default value | 0 |

<a id="5d38165fd00ec3f3"></a>
### Description

It represents the duration of busy waiting during dequeue operations in the cdispatcher, measured in microseconds. A larger value increases CPU usage but reduces user response time (latency). The default value is 0, which means busy waiting is not allowed.

<a id="fdfb51d52a773c11"></a>
## CDISPATCHER_LOCKABLE_THREADS

<a id="62636ca9bab8ef76"></a>
### Basic Information

<a id="088bb008dcdd9268"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_LOCKABLE_THREADS |
| Summary | cdispatcher lockable sender, receiver thread count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 30 |
| Default value | 1 |

<a id="18f967d221d2cfde"></a>
### Description

It sets the number of cdispatcher threads for lockble data senders and receivers. The number of cdispatcher threads for lockless data senders and receivers is configured using [CDISPATCHER_LOCKLESS_THREADS](#c0dd3946921b40ff).

<a id="0871938663b20f8b"></a>
### ALIAS

<a id="becc059755c934e0"></a>
| Item | Description |
| --- | --- |
| Original name | CDISPATCHER_LOCKABLE_THREADS |
| ALIAS | CDISPATCHER_THREADS |

<a id="c0dd3946921b40ff"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="09b48c4438947900"></a>
### Basic Information

<a id="7caf3cf7ef5a57e4"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_LOCKLESS_THREADS |
| Summary | cdispatcher lockless sender, receiver thread count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 30 |
| Default value | 1 |

<a id="bdf3a3047daccffe"></a>
### Description

It sets the number of cdispatcher threads for lockless data senders and receivers. The number of cdispatcher threads for lockable data senders and receivers is configured using [CDISPATCHER_LOCKABLE_THREADS](#fdfb51d52a773c11).

<a id="029d4d35701be01f"></a>
## CDISPATCHER_MAX_PACKET_BUFFER_SIZE

<a id="73ed4b67fd37b95b"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="cfedbe61d3a2d19f"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_MAX_PACKET_BUFFER_SIZE |
| Summary | maximum packet buffer size for cdipatcher sender and receiver threads |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| Default value | 1 Giga |

<a id="562d71370787e8a3"></a>
### Description

It sets the maximum size of the buffer where the cdispatcher's data sender and receiver store the sent/ received packets.

<a id="f51bf5f79932e5cb"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="8faf3a5fd6b73bf6"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="29c0ddce5048b56d"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_SOCKET_BUFFER_SIZE |
| Summary | cdispatcher socket buffer(sender, receiver) size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 64 |
| MAX | 100 Mega |
| Default value | 32768 |

<a id="f8105204894a5d3c"></a>
### Description

It refers to the socket buffer size (sender and receiver) of the cdispatcher.

<a id="15afebf99e9aea8c"></a>
## CDISPATCHER_SYNC_THREADS

<a id="6ce6421b34d96bfc"></a>
### Basic Information

**Basic Information of CDISPATCHER_SYNC_THREADS**

<a id="bd45ce489159228e"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_SYNC_THREADS |
| Summary | cdispatcher sync thread count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 30 |
| Default value | 1 |

<a id="e2546e6d75bd1964"></a>
### Description

It refers to the thread count for cdispatcher sync.

<a id="677b530eacc70cb1"></a>
## CHANGE_TRACKING

<a id="2e2d54b532507bca"></a>
### Basic Information

<a id="ddce71591832ba9d"></a>
| Item | Description |
| --- | --- |
| Name | CHANGE_TRACKING |
| Summary | enable change tracking for incremental backup |
| Data type | BOOLEAN |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="0a6576ff4a70b32d"></a>
### Description

It determines whether to track the updated pages for performing incremental backups of the disk tablespace.

- NO: disable change tracking
- YES: enable change tracking

*change tracking* can be enabled using the command ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING during the mount phase or above, but only when the database is operating in archivelog mode.

<a id="9179ff071f077bde"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="f2eda73985d247e7"></a>
### Basic Information

<a id="75caf68052ca2d16"></a>
| Item | Description |
| --- | --- |
| Name | CHANGE_TRACKING_EXTENT_SIZE |
| Summary | number of pages to track changed of incremental backup |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 32 |
| MAX | 512 |
| Default value | 32 |

<a id="09770a48733fe46c"></a>
### Description

It sets the number of pages to be displayed with a single dirty flag during change tracking. For example, if set to 32, one dirty flag is used for every 32 pages; if set to 128, one dirty flag is used for every 128 pages.

<a id="18b22dba09497e21"></a>
## CHANGE_TRACKING_FILE

<a id="2caae4396c64c7d0"></a>
### Basic Information

<a id="e80d0d702b0cfe54"></a>
| Item | Description |
| --- | --- |
| Name | CHANGE_TRACKING_FILE |
| Summary | default change tracking file |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/backup/gl_change_tracking_file.ctf |

<a id="e1115673af6dc60a"></a>
### Description

It sets the file directory and filename for storing change tracking data.

<a id="b06a0825ab72d342"></a>
## CHAR_LENGTH_UNITS

<a id="34e725afa9db5288"></a>
### Basic Information

**Basic Information of CHAR_LENGTH_UNITS**

<a id="e6ea3a893ce1b473"></a>
| Item | Description |
| --- | --- |
| Name | CHAR_LENGTH_UNITS |
| Summary | char length units |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | OCTETS |

<a id="0073a908382a10e0"></a>
### Description

It is the value of the char length units used when defining string columns such as CHAR, VARCHAR, particularly when the char length unit is omitted as follows.

```
CREATE TABLE t1 
(
   id   CHAR( 10 OCTETS ),          
   name VARCHAR( 128 CHARACTERS ),  
   addr VARCHAR( 128 )    
);
```

- id CHAR( 10 OCTETS ) means 10 bytes.
- name VARCHAR( 128 CHARACTERS ) means 128 characters.
- addr VARCHAR( 128 ) indicates that this value is referenced when the char length unit is omitted.

When the database is created, the property is set to either OCTETS or CHARACTERS. OCTETS refers to the number of bytes, while CHARACTERS refers to the number of characters.

> The SQL standard defines CHARACTERS as the default value. Other DBMSs define the default value of the char length unit as follows. 
> 
> - Oracle and DB2 define OCTETS as the default value. 
> - MS-SQL, MySQL and PostgreSQL define CHARACTERS as the default value.
> 

<a id="e0299b8677bc1e4e"></a>
## CHARACTER_SET

<a id="92105e47cad35fed"></a>
### Basic Information

**Basic Information of CHARACTER_SET**

<a id="75fd9a7dd5c99f2d"></a>
| Item | Description |
| --- | --- |
| Name | CHARACTER_SET |
| Summary | character set |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | UTF8 |

<a id="2a37e0a3bb99c236"></a>
### Description

It is a character set for the database that is applied when the database is created.  
The property is set to one of the following values.

**Character set**

<a id="235f5cd437ef5489"></a>
| Character set | Description |
| --- | --- |
| SQL_ASCII | ASCII standards |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standards |

<a id="d32d0fd51a62eab3"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="a11e37ad713e2fc2"></a>
### Basic Information

**Basic Information of CHECK_DEDICATE_CONNECTION_INTERVAL**

<a id="9a04e6c9528926d0"></a>
| Item | Description |
| --- | --- |
| Name | CHECK_DEDICATE_CONNECTION_INTERVAL |
| Summary | check dedicate socket |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000 |
| Default value | 1000 |

<a id="3dde8ec67e03ff31"></a>
### Description

It is the interval for checking when the client forcibly disconnects in a C/S dedicated environment. The dedicated server (gserver) monitors the socket and terminates it if the connection is lost. The default value is 1,000 milliseconds (1 second).

<a id="c8b6575984364db6"></a>
## CHECKPOINT_LIST_COUNT_PER_IO_GROUP

<a id="0bc5281b13e6c404"></a>
### Basic Information

<a id="878435c7ea248d07"></a>
| Item | Description |
| --- | --- |
| Name | CHECKPOINT_LIST_COUNT_PER_IO_GROUP |
| Summary | number of checkpoint lists per each io group |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 8192 |
| Default value | 0 |

<a id="4c8af5812adc1c00"></a>
### Description

It sets the number of checkpoint lists to be processed by each IO slave, determined by the [PARALLEL_IO_FACTOR](#250c145fdbcbb2a5). This value specifies the optimal number for efficiently handling concurrency when connecting updated pages to the checkpoint lists. The default value is 0, meaning that each IO slave creates as many checkpoint lists as there are CPU cores and processes them accordingly.

<a id="8b3693c33e39689d"></a>
## CLIENT_MAX_COUNT

<a id="79c94a7c5c6794e7"></a>
### Basic Information

**Basic Information of CLIENT_MAX_COUNT**

<a id="11494e299daa310f"></a>
| Item | Description |
| --- | --- |
| Name | CLIENT_MAX_COUNT |
| Summary | maximum session count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 12 |
| MAX | 65535 |
| Default value | 128 |

<a id="9c234c178eb0bdea"></a>
### Description

It sets the maximum number of sessions allowed to connect.

<a id="39c96e1a3a35ced2"></a>
## CLIENT_NUMA_POLICY

<a id="ec57098ec1eaf7a0"></a>
### Basic Information

**Basic Information of CLIENT_NUMA_POLICY**

<a id="17e135e60af5a79c"></a>
| Item | Description |
| --- | --- |
| Name | CLIENT_NUMA_POLICY |
| Summary | client numa policy( 0: by modualar, 1: by statistics , 2: by manunal ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="670754954c5479f5"></a>
### Description

It determines the policy for distributing client processes across NUMA nodes. This property is activated when the NUMA setting is turned on.

- 0: It determines the NUMA node to connect to by modularizing the session ID.
- 1: It prioritizes connections to the least connected NUMA node based on statistical information.
- 2: C/S client is determined by the TCP_CLIENT_NUMA_NODE property, while D/A client is determined by the DA_CLIENT_ NUMA_NODE property.

<a id="80dac4861bc36c1b"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="82d2eab8cae20139"></a>
### Basic Information

**Basic Information of CLOSE_PSM_CHILD_STMTS**

<a id="f21bbc3817bb735a"></a>
| Item | Description |
| --- | --- |
| Name | CLOSE_PSM_CHILD_STMTS |
| Summary | close child statements of PSM at the end of each execution |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="a3c095eecb1d25ef"></a>
### Description

It closes the child statement of the PSM at the end of each execution.

<a id="466e3feff66040fc"></a>
## CLUSTER_ASYNC_COMMIT

<a id="9ad759c18d60f32e"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="ba3c10f3014a1190"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_ASYNC_COMMIT |
| Summary | enable asynchronous commit in cluster system |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="66206114c39abe77"></a>
### Description

It determines whether to internally process the commit protocol in async mode within a cluster system.

> If this property is set to on, it asynchronously commits for each node, which may lead to temporary inconsistencies among nodes. Conversely, if it is set to 'off,' it synchronizes with each commit, potentially reducing performance. Therefore, it is essential to determine the appropriate setting based on your specific needs.

<a id="4c9378dcdb77ed56"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="79dfbfd0ab6f2fec"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_SIZE**

<a id="008f0b410fc883c7"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_CM_BUFFER_SIZE |
| Summary | communication buffer size for cluster |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| Default value | 10 Mega |

<a id="3afb9a2831a6f333"></a>
### Description

It is the communication buffer size for the cluster.

<a id="6c15dc92597e0eda"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="a86362d746e11a7b"></a>
### Basic Information

**Basic Information of CLUSTER_CM_READ_BUFFER_SIZE**

<a id="adf61eeae9951507"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_CM_READ_BUFFER_SIZE |
| Summary | communication read block size |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8192 |
| MAX | 10485,760 |
| Default value | 65536 |

<a id="136981b50012d798"></a>
### Description

It is the size of the communication read block.

<a id="a9417dd71332949a"></a>
## CLUSTER_COMMIT_SLAVE_CSERVERS

<a id="09e780d894838fce"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_SLAVES**

<a id="b3f294db21425e19"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_COMMIT_SLAVE_CSERVERS |
| Summary | number of commit slave cservers |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 8 |
| Default value | 0 |

<a id="9a20151b543af12e"></a>
### Description

It is the number of commit slaves.

<a id="6f4ab0a64d3fe6d3"></a>
### ALIAS

<a id="4a535e405c840e6a"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_COMMIT_SLAVE_CSERVERS |
| ALIAS | CLUSTER_COMMIT_SLAVES |

<a id="bae655a4ed821cbd"></a>
## CLUSTER_CONNECTION

<a id="cba2e103817ea861"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION**

<a id="c71403cb9e900226"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_CONNECTION |
| Summary | connection mode for cluster ( socket:0, rdma:1 ) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0: socket |

<a id="fcdd4938809e55f0"></a>
### Description

It is the connection mode for the cluster. ( socket:0, rdma:1 )

<a id="0e6e1eb0cbed5739"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="1089fb11d707808c"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION_TIMEOUT_SEC**

<a id="bacfb0681904e5e8"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_CONNECTION_TIMEOUT_SEC |
| Summary | connection timeout for cluster |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400 |
| Default value | 10 |

<a id="31593f934f101ec6"></a>
### Description

It is the connection timeout used for the initial connection between cluster members.

<a id="f97ce65172368fdd"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="945f4e606713bdef"></a>
### Basic Information

**Basic Information of CLUSTER_DATA_SYNC_SERVERS**

<a id="46c2e10fa8b011c7"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_DATA_SYNC_SERVERS |
| Summary | count of data synchronization server |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 128 |
| Default value | 3 |

<a id="4e0a25882838b878"></a>
### Description

It is the count of data synchronization servers.

<a id="b263f4e6880f8f13"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="595842ab23f8c00f"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_IN_QUEUE_SIZE**

<a id="005f70716387aa99"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_DISPATCHER_IN_QUEUE_SIZE |
| Summary | in-queue size for cluster dispatcher |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1024 |
| MAX | 32768 |
| Default value | 1024 |

<a id="0ab681f7c9bd0127"></a>
### Description

It is the in-queue size for the cluster dispatcher.

<a id="2bf2bc5d6fc95df5"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="491661009ee91780"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_NUMA_STREAM_MAP**

<a id="42ea6118faca4cfc"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_DISPATCHER_NUMA_STREAM_MAP |
| Summary | numa stream map for cluster dispatcher |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | 'x' : no binding |

<a id="634ed60a5c98b555"></a>
### Description

It determines the NUMA node to which the cluster dispatcher will connect. This property is activated when the NUMA setting is enabled.

The following is an example of three dispatchers. It connects stream 0 to NUMA node 0, stream 1 to NUMA node 1, and stream 2 to NUMA node 2.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="c3db604202392c82"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="c55d7aff5d2dba71"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_OUT_QUEUE_SIZE**

<a id="42c6841767afe86c"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_DISPATCHER_OUT_QUEUE_SIZE |
| Summary | out-queue size for cluster dispatcher |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1024 |
| MAX | 32768 |
| Default value | 1024 |

<a id="a7a272d90751214a"></a>
### Description

It is the out-queue size for the cluster dispatcher.

<a id="86f4bb660db7ff71"></a>
## CLUSTER_FETCH_ORDER

<a id="f38af56ed6ba4245"></a>
### Basic Information

<a id="73e6fdbf5c1901a3"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_FETCH_ORDER |
| Summary | fetch order in cluster |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="4058dbf62ac0f295"></a>
### Description

It configures the fetch priority of the cluster puller.

If the value is 0, data is fetched from the node—either local or remote—that becomes available first.  
If the value is 1, data is fetched from the local node first, followed by the remote node.  
If the value is 2, data is fetched from the remote node first, followed by the local node.

<a id="4479a9182623b5ec"></a>
## CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE

<a id="fff5b76078319aac"></a>
### Basic Information

<a id="d6396034c7ccc934"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| Summary | response queue size for cluster server |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 30 |
| MAX | 32768 |
| Default value | 30 |

<a id="dfc985c1ec13a9a1"></a>
### Description

It sets the maximum queue size for receiving responses from the remote server.

<a id="5796492fa83243a8"></a>
### ALIAS

<a id="294f76cb774cf3cc"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| ALIAS | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |

<a id="2a90ec9a4176ed4a"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="48965b371d5877db"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_INTERVAL**

<a id="c4ac103c3c257971"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_HEARTBEAT_INTERVAL |
| Summary | interval seconds for health checking of cluster |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400 |
| Default value | 3 |

<a id="02f961efc8e7bef2"></a>
### Description

It is the interval in seconds for health checking of the cluster. A value of 0 means it is disabled.

<a id="563e601ff125903e"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="d5a0e54a4feb1bcf"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_RETRY_COUNT**

<a id="8264df911217240d"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_HEARTBEAT_RETRY_COUNT |
| Summary | retry count for health checking of cluster |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 65536 |
| Default value | 5 |

<a id="b32b9f5db165a5e1"></a>
### Description

It is the retry count for health checking of the cluster.

<a id="0f35f925409ec4d5"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="bfde680a10da3a01"></a>
### Basic Information

**Basic Information of CLUSTER_IGNORE_INACTIVE_MEMBER**

<a id="3f8b57603fb77f0f"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_IGNORE_INACTIVE_MEMBER |
| Summary | ignore in-active member for cluster |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="d1444a0af97855d4"></a>
### Description

It ignores in-active members of the cluster.

<a id="c7c5bd3f4c93fb81"></a>
## CLUSTER_KEEPALIVE_IDLE_TIME

<a id="edf418489f6f8e79"></a>
### Basic Information

<a id="83bdf006a3abce69"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_KEEPALIVE_IDLE_TIME |
| Summary | The number of seconds a cluster connection needs to be idle |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 16383 |
| Default value | 0 |

<a id="acc99b276f11c302"></a>
### Description

It is the idle time, defined as the duration without sending or receiving TCP packets between a cluster session and a cdispatcher, before a keep alive packet is sent. In other words, if TCP packets are not exchanged during the duration set in CLUSTER_KEEPALIVE_IDLE_TIME, the keep alive mechanism is activated on the cdispatcher side to detect a dead connection.

The default value is 0, which disables the keep-alive feature.

<a id="9020e957dde68206"></a>
## CLUSTER_LOCKABLE_CSERVERS

<a id="94704960769cf957"></a>
### Basic Information

<a id="6e2825b9b2ba34f3"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_LOCKABLE_CSERVERS |
| Summary | number of lockable cserver processes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 5 |

<a id="8bda71fd8c3431cb"></a>
### Description

It sets the number of cluster server processes that perform operations requiring a lock. The number of cluster server processes for operations that do not require a lock is set using [CLUSTER_LOCKLESS_CSERVERS](#3fe09fe1c9a0e8eb).

<a id="3994152a48ce3830"></a>
### ALIAS

<a id="a6d534bf0ef298c3"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_LOCKABLE_CSERVERS |
| ALIAS | CSERVERS |

<a id="3fe09fe1c9a0e8eb"></a>
## CLUSTER_LOCKLESS_CSERVERS

<a id="7960e6b201340f30"></a>
### Basic Information

<a id="6d192d8b736029ca"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_LOCKLESS_CSERVERS |
| Summary | number of lockless cserver processes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 5 |

<a id="8dbca1adf4cb1b11"></a>
### Description

It sets the number of cluster server processes that perform operations without acquiring a lock. The number of cluster server processes for operations that acquires a lock is set using [CLUSTER_LOCKABLE_CSERVERS](#9020e957dde68206) property.

<a id="ade85dccf2282d40"></a>
### ALIAS

<a id="4d0780cb551f164e"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_LOCKLESS_CSERVERS |
| ALIAS | LOCKLESS_CSERVERS |

<a id="9d62ee0963fa5dda"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="300ff0991c990ac2"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PACKET_SIZE**

<a id="52c54aaaf072a50c"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_MAX_PACKET_SIZE |
| Summary | maximum packet size for cluster session |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| Default value | 100 Mega |

<a id="5f0e4883b941def8"></a>
### Description

It sets the maximum packet size that the remote protocol can transfer at one time. If the column size to be remotely transferred exceeds this property size, then the property size must be increased to accommodate the column size.

<a id="7d1824dde4b9f6b0"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="586d4dec2cda3cfe"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PAYLOAD_SIZE**

<a id="c02e3b2e3b5d40f4"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_MAX_PAYLOAD_SIZE |
| Summary | maximum packet payload size for cluster session (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 524288 |
| MAX | 33554432 |
| Default value | 524288 |

<a id="eb645a059cd2a833"></a>
### Description

The cluster packet that is remotely transferred may be delivered in segments, and this property sets the maximum size of data that can be stored in a single segment.

<a id="0ad6b326122d8425"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="5d4463ad67bbcc8f"></a>
### Basic Information

**Basic Information of CLUSTER_PACKET_ALLOCATION_TIMEOUT**

<a id="7339300b48c59cf3"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PACKET_ALLOCATION_TIMEOUT |
| Summary | a time limit (sec) for how long statements will wait to allocate packet memory |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| Default value | 3 |

<a id="9e03a15db0305ec0"></a>
### Description

It sets the maximum waiting time (in seconds) for allocating memory required for cluster packet configuration.

<a id="3a885dc1ed49ab08"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="a1852c9354312700"></a>
### Basic Information

<a id="aae77001d6f07848"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT |
| Summary | a time limit of failover policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="0e3906d1f8cceec4"></a>
### Description

It is the maximum time to wait for a response after sending the protocol in the cluster. If a response is not received within the specified time, GOLDILOCKS may either terminate the session or trigger a failover for the unresponsive remote cluster member, depending on the protocol. To set the time limit for the failover policy, use the CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT property, and to set the time limit for the session termination policy, use the [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#86d4646ca39a0798) property.

<a id="86d4646ca39a0798"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="9ef9c34647d26214"></a>
### Basic Information

<a id="870538786c6e7cd3"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT |
| Summary | a time limit of session fatal policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="f1867e6c46875ed3"></a>
### Description

It is the maximum time to wait for a response after sending the protocol in the cluster. If a response is not received within the specified time, GOLDILOCKS may either terminate the session or trigger a failover for the unresponsive remote cluster member, depending on the protocol. To set the time limit for the session termination policy, use the *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property, and to set the time limit for the failover policy, use the [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#3a885dc1ed49ab08) property.

<a id="b0c5912c9cc604fe"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="77bc687b176351ca"></a>
### Basic Information

<a id="a1b85f4365bbc76e"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_SESSION_HASH_BUCKETS |
| Summary | Number of hash buckets for cluster sessions |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 127 |
| MAX | 1073741824 |
| Default value | 127 |

<a id="d6486ea796315363"></a>
### Description

It sets the number of hash buckets used to control the cluster session.

<a id="77027a79e36b9077"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="2e8ef83935604e95"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY**

<a id="8000d6ed349649e7"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY |
| Summary | split brain resolution policy for cluster system |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="29392e290c2b4af0"></a>
### Description

It sets the policy for resolving split-brain situations in the cluster system. If the value is set to 1 or higher, it queries the locator for a solution.

> If a query to the locator times out, it will attempt to query again up to the number specified by CLUSTER_SPLIT_BRAIN_RETRY_COUNT. If it fails after retrying, it will forcibly proceed with the failover if the property value is 1, and it will terminate as fatal if the property value is 2.

<a id="e6891e5f0a93f43b"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="b89fbdb8441aaaaa"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RETRY_COUNT**

<a id="be4b5923941c28d0"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_SPLIT_BRAIN_RETRY_COUNT |
| Summary | retry count for split brain resolution policy(1 ~ 65536) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 65536 |
| Default value | 1 |

<a id="fc308f1a6ba63cec"></a>
### Description

It is used when the CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or higher in the cluster system. It specifies the number of times to retry the inquiry if there is no response to the query sent to the locator.

<a id="b58f3e8f05f5a1f6"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="fb3991acfeac1735"></a>
### Basic Information

**Basic Information of COMMITTER_HOT_POLICY_INTERVAL**

<a id="5e2cb967781eb1ab"></a>
| Item | Description |
| --- | --- |
| Name | COMMITTER_HOT_POLICY_INTERVAL |
| Summary | committer deque interval for busy waiting |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000 (1 day) |
| Default value | 0 (cold policy) |

<a id="fa1b4921585a465e"></a>
### Description

It sets the time interval for busy waiting when the commit server is dequeuing to read the commit protocol message. If it is set to 1,000,000 (1 second) and less than 1 second has passed since the last successful dequeue attempt, the timeout for the dequeue operation is set to 0, resulting in busy waiting.

<a id="c71c5e10f26ad9df"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="75e768b154e30579"></a>
### Basic Information

**Basic Information of CONTROL_FILE_0 ~ CONTROL_FILE_7**

<a id="84e54cf53b4e20dc"></a>
| Item | Description |
| --- | --- |
| Name | CONTROL_FILE_0 |
| Summary | control file name |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl |

<a id="823c2d96dc8e315c"></a>
### Description

If a control file is corrupted, the database cannot be used. Therefore, the control file is multiplexed to ensure the stability of the database. This property specifies the directory and file name for each stored control file.

<a id="db3f9d2549bfb7d1"></a>
## CONTROL_FILE_COUNT

<a id="518fa96dff98623d"></a>
### Basic Information

**Basic informatin of CONTROL_FILE_COUNT**

<a id="25d5bb6bc9cadcb5"></a>
| Item | Description |
| --- | --- |
| Name | CONTROL_FILE_COUNT |
| Summary | control file count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 2 |
| MAX | 8 |
| Default value | 2 |

<a id="4750f8c783b67256"></a>
### Description

If a control file is corrupted, the database cannot be used. The control file is multiplexed to ensure the stability of the database. CONTROL_FILE_COUNT specifies the number of multiplexed control files, with a minimum of 2 and a maximum of 8.

<a id="9a9c62d840ce7166"></a>
## CONTROL_FILE_TEMP_NAME

> It has not been supported since version 26c.1.

<a id="35c6686498923d12"></a>
### Basic Information

**Basic Information of CONTROL_FILE_TEMP_NAME**

<a id="198a0911f996b269"></a>
| Item | Description |
| --- | --- |
| Name | CONTROL_FILE_TEMP_NAME |
| Summary | temporary file name for control file |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/backup/control.tmp |

<a id="ad8dca10885234f5"></a>
### Description

During database operations, the control file is frequently updated, and a temporary copy can be created if necessary. CONTROL_FILE_TEMP_NAME specifies the directory and file name for temporarily storing the control file.

<a id="d0ccf8a742dc1752"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="3358d9b626f1dab9"></a>
### Basic Information

**Basic Information of COORDINATOR_COMMIT_WRITE_MODE**

<a id="a4f5c079c7ff311a"></a>
| Item | Description |
| --- | --- |
| Name | COORDINATOR_COMMIT_WRITE_MODE |
| Summary | coordinator commit write mode(0:disable, 1:wait mode) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="5b1d3a8c6ce11d13"></a>
### Description

It is a commit write mode applied to a coordinator. If TRANSACTION_COMMIT_WRITE_MODE is set to 'no wait' but this property is set to 'wait,' then the coordinator node operates in 'wait' mode while other nodes operate in 'no wait' mode.

<a id="4411cd971babc6ee"></a>
## DA_CLIENT_NUMA_NODE

<a id="15fbc4a7e31b5e65"></a>
### Basic Information

**Basic Information of DA_CLIENT_NUMA_NODE**

<a id="dcd92f770e960276"></a>
| Item | Description |
| --- | --- |
| Name | DA_CLIENT_NUMA_NODE |
| Summary | numa node for DA clients |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | -1 |
| MAX | 63 |
| Default value | -1 |

<a id="4a2266457cf91699"></a>
### Description

It sets the NUMA node ID to which the direct access (D/A) session is bound. This property is effective when the NUMA setting is set to ON.

<a id="cfac67863a2fc151"></a>
## DATA_STORE_MODE

<a id="4d189d2d8991c43c"></a>
### Basic Information

**Basic Information of DATA_STORE_MODE**

<a id="20382b3aaabd7332"></a>
| Item | Description |
| --- | --- |
| Name | DATA_STORE_MODE |
| Summary | data store mode(cds:1,tds:2) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 2 |
| Default value | 2 |

<a id="21142be8d4dc4265"></a>
### Description

It sets the storage method of the database.

- 1: CDS mode supports concurrency for multiple users but does not guarantee durability. It does not log all operations that modify the database, including data inserts/ deletes/ updates, so recovery from a failure is not possible.
- 2: TDS mode guarantees both concurrency for multiple users and durability through the use of logs.

<a id="5359eb010e9e4277"></a>
## DATABASE_INSTANCE_NAME

<a id="07e7822ca9154c12"></a>
### Basic Information

**Basic Information of DATABASE_INSTANCE_NAME**

<a id="f7885987dbe9518a"></a>
| Item | Description |
| --- | --- |
| Name | DATABASE_INSTANCE_NAME |
| Summary | database instance name |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | GOLDILOCKS |

<a id="2e1091d1bd3b9210"></a>
### Description

It is the name of the database instance.

<a id="0bd0e7c6c2fda98e"></a>
## DDL_AUTOCOMMIT

<a id="2048a2f04e7924d8"></a>
### Basic Information

**Basic Information of DDL_AUTOCOMMIT**

<a id="7bc0a197d431a701"></a>
| Item | Description |
| --- | --- |
| Name | DDL_AUTOCOMMIT |
| Summary | DDL auto commit |
| Data type | BOOL |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="812aef01021106aa"></a>
### Description

It sets whether to autocommit DDL operations that have not yet been autocommitted. For example, autocommit is not applied to operations such as creating/ altering a table. If DDL_AUTOCOMMIT is set to 0, table creation and alteration can be undone with a rollback. On the other hand, if DDL_AUTOCOMMIT is set to 1, DDL operations that do not have autocommit applied are committed immediately.

<a id="f7c0066758882150"></a>
## DDL_LOCK_TIMEOUT

<a id="92745a45aeee7284"></a>
### Basic Information

**Basic Information of DDL_LOCK_TIMEOUT**

<a id="74c9319b57bc59c1"></a>
| Item | Description |
| --- | --- |
| Name | DDL_LOCK_TIMEOUT |
| Summary | a time limit (sec) for how long DDL statements will wait |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="61946bf451af3f6a"></a>
### Description

It specifies the lock wait time when DDL operations are attempted on the same object simultaneously. The default value is 0 seconds, meaning that no wait occurs for a lock when a DDL operation is initiated.

When operations to alter a table structure occur simultaneously, they will wait for the duration specified in DDL_LOCK_TIMEOUT, without waiting for the termination of other transactions as follows.

• Transaction A

```
ALTER TABLE t1 ADD COLUMN ( new_column NUMBER );
```

• Transaction B

```
TRUNCATE TABLE t1;
```

If the waiting time exceeds DDL_LOCK_TIMEOUT, an error will occur as follows.

```
gSQL> TRUNCATE TABLE t1;

ERR-HYT00(14026): resource busy or timeout expired
```

<a id="88bcbb109e88bdb5"></a>
## DEADLOCK_PRIORITY

<a id="efa775a6a0c52912"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="5ade21b8088e580f"></a>
| Item | Description |
| --- | --- |
| Name | DEADLOCK_PRIORITY |
| Summary | importance to choose deadlock victim |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 9 |
| Default value | 5 |

<a id="0644d00fdca74714"></a>
### Description

When a deadlock occurs while processing multiple transactions simultaneously, a specific transaction with the lower weight is selected as a victim among transactions which caused the deadlock, to solve the problem. If a deadlock occurs between a transaction initiated in sessions with a higher value for this property and a transaction in sessions with a lower value, the latter is selected as the deadlock victim. Therefore, set this property according to the priority of each transaction.

Start the transaction after setting this property value to ensure that it is applied as the weight of that transaction. The transaction weight will not change if this value is modified after the transaction has already started.

<a id="9db1a1d54cafa67a"></a>
## DEFAULT_ASC_NULLS_ORDER

<a id="f81e7a5161b22ec1"></a>
### Basic Information

<a id="5bc30f8f760d4153"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_ASC_NULLS_ORDER |
| Summary | default nulls order for ascending sort (0:nulls_first, 1:nulls_last) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 1 |

<a id="95d1033c92d8aac5"></a>
### Description

It sets the default nulls order when the sort order is ascending and the nulls order is omitted. If this value is 0, the order is NULLS FIRST. If this value is 1, the order is NULLS LAST.

This property value is applied to the system when the server is started.

When the sort order is ascending, the Default Nulls Order for each DBMS is as follows.

- NULLS FIRST: MSSQL, MySQL, SQLite
- NULLS LAST (default): PostgreSQL, ORACLE, DB2

<a id="9794e87fa1b7a607"></a>
## DEFAULT_DESC_NULLS_ORDER

<a id="29690f082ce80696"></a>
### Basic Information

<a id="36a3dd0f43b9e46b"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_DESC_NULLS_ORDER |
| Summary | default nulls order for descending sort (0:nulls_first, 1:nulls_last) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 1 |

<a id="d1885be88f486bcd"></a>
### Description

It sets the default nulls order when the sort order is descending and the nulls order is omitted. If this value is 0, the order is NULLS FIRST. If this value is 1, the order is NULLS LAST.

This property value is applied to the system when the server is started.

When the sort order is descending, the Default Nulls Order for each DBMS is as follows.

- NULLS FIRST: PostgreSQL, ORACLE, DB2
- NULLS LAST (default): MSSQL, MySQL, SQLite

<a id="f521d98b5f13c26a"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="81cc21b2051e7e0d"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="ab3b31b43c619654"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION |
| Summary | specifies whether or not create global secondary index at table creation |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="529cd274a39077a5"></a>
### Description

It determines whether to create a global secondary index when creating a table in a cluster system. A non-deterministic query on a table that does not have a global secondary index will fail. If set to NO, a global secondary index can be created separately after the table is established.

<a id="6e47045c6e914b88"></a>
## DEFAULT_INDEX_LOGGING

> It has not been supported since version 3.2.

<a id="79946151abab21f3"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_LOGGING**

<a id="dcfe04dd90257523"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_INDEX_LOGGING |
| Summary | default logging flag of indexes |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="44a7f0d4e84e8390"></a>
### Description

If the LOGGING property is not explicitly set by the user when an index is created, it defaults to the DEFAULT_INDEX_LOGGING value. If an index is created in a LOGGING tablespace, the LOGGING property must be set.

<a id="74782b3e0126d31c"></a>
## DEFAULT_INDEX_PCTFREE

<a id="71e813f1b1f0e022"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_PCTFREE**

<a id="096964a70e86c2cf"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_INDEX_PCTFREE |
| Summary | default pctfree value of indexes ( % ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| Default value | 10 |

<a id="847830584f6b6425"></a>
### Description

If a user does not explicitly specify the PCTFREE syntax when creating an index. The PCTFREE value is set to the DEFAULT_INDEX_PCTFREE property.

<a id="d63e2db0e2bc069a"></a>
## DEFAULT_INITRANS

<a id="923788057595726e"></a>
### Basic Information

**Basic Information of DEFAULT_INITRANS**

<a id="0f7193a331cb1b27"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_INITRANS |
| Summary | default initrans value of tables |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 32 |
| Default value | 4 |

<a id="6a41d99124020265"></a>
### Description

If a user does not explicitly set the INITRANS syntax when creating a table or an index, the INITRANS value defaults to the DEFAULT_INITRANS property.

<a id="c44fafa3bbc35d7b"></a>
## DEFAULT_MAXTRANS

<a id="d328f93952937ed4"></a>
### Basic Information

**Basic Information of DEFAULT_MAXTRANS**

<a id="da854380abb2d3ee"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_MAXTRANS |
| Summary | default maxtrans value of tables |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 32 |
| Default value | 32 |

<a id="ca0b5cf50e6f7da4"></a>
### Description

If a user does not explicitly set the INITRANS syntax when creating a table or an index, the INITRANS value defaults to the DEFAULT_INITRANS property.

<a id="011a3f74f05ea6f8"></a>
## DEFAULT_PCTFREE

<a id="d66da4ab31e60524"></a>
### Basic Information

**Basic Information of DEFAULT_PCTFREE**

<a id="4a3331f58597e257"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_PCTFREE |
| Summary | default pctfree value of tables ( % ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| Default value | 10 |

<a id="fb20625adab0518e"></a>
### Description

If a user does not explicitly set the PCTFREE property when creating a table, it defaults to the value of the DEFAULT_PCTFREE property.

<a id="9098b1ace48f012d"></a>
## DEFAULT_PCTUSED

<a id="51a913a207ed71b7"></a>
### Basic Information

**Basic Information of DEFAULT_PCTUSED**

<a id="5002dda3f6925778"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_PCTUSED |
| Summary | default pctused value of tables ( % ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| Default value | 60 |

<a id="7f6aae4f714af610"></a>
### Description

If a user does not explicitly set the PCTUSED property when creating a table, it defaults to the value of the DEFAULT_PCTUSED property.

<a id="8b4167ab13e3dbee"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="f790c592f1693c6b"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_BACKUP_FILE**

<a id="a6dddad24c62ce83"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_REMOVAL_BACKUP_FILE |
| Summary | default removal flag of incremental backup files |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="bede7c81c184bf25"></a>
### Description

It specifies whether to delete the backup file when the backup list is deleted.

<a id="624e80642ee338a3"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="344f759c4d2bb872"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST**

<a id="a8aca3200784db89"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST |
| Summary | default removal flag of obsolete incremental backup lists |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="71bafbf1854b9eb9"></a>
### Description

It specifies whether to delete the previous obsoleted backup list when executing an INCREMENTAL BACKUP.

<a id="b42b1ed9a19b2182"></a>
## DEFAULT_SHARDING

<a id="8260c79596b63040"></a>
### Basic Information

**Basic Information of DEFAULT_SHARDING**

<a id="edce621ee2a6ab0d"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_SHARDING |
| Summary | default sharding strategy (0: cloned, 1: hash sharding) |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="f067d13f98eb1735"></a>
### Description

It sets the default sharding strategy to be used if a sharding strategy is not specified when creating a table.

The following is an example of executing a CREATE TABLE statement.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

If the DEFAULT_SHARDING value is 0 (cloned), the table is created as a cloned table as follows.

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

If the DEFAULT_SHARDING value is 1 (hash sharding), the table is created as a hash-sharded table as follows.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
)
SHARDING BY HASH (id)
    SHARD COUNT 24
    AT CLUSTER WIDE
;
```

If DEFAULT_SHARDING is 1 (hash sharding) and the &lt;table sharding strategy&gt; is not specified, the hash sharding key is determined in the following order.

1. If a PRIMARY KEY constraint is defined, the primary key is used as the sharding key.

• The original message

```
CREATE TABLE t1 ( id INTEGER PRIMARY KEY, name VARCHAR(128) );
```

• Translation

```
CREATE TABLE t1 ( id INTEGER PRIMARY KEY, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

2. If a UNIQUE constraint is defined, the first specified UNIQUE constraint is used as the sharding key.

• The original message

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) UNIQUE );
```

• Translation

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) UNIQUE )
    SHARDING BY HASH(name)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

3. If a key constraint is not defined, the first column, excluding the following data types, is used as the sharding key.
** Excluded data types: LONG VARCHAR, LONG VARBINARY, BOOLEAN

• The original message

```
CREATE TABLE t1 ( is_man BOOLEAN, id INTEGER, name VARCHAR(128) );
```

• Translation

```
CREATE TABLE t1 ( is_man BOOLEAN, id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

<a id="8b8ba8428c56db39"></a>
## DISABLE_DDL

<a id="f3ddf2e4c5a7c58c"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="d2b251e63d855d92"></a>
| Item | Description |
| --- | --- |
| Name | DISABLE_DDL |
| Summary | disable All DDL |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="d2d0535d357041f9"></a>
### Description

It prevents the execution of all DDL statements.

The SQL statements affected by DISABLE_DDL can be queried as follows.

```
gSQL>
SELECT command
  FROM v$sql_command
 WHERE is_ddl = 'YES'
 ORDER BY 1
;

COMMAND                                                  
---------------------------------------------------------
ALTER AUDIT POLICY                                       
ALTER CLUSTER GROUP .. ADD CLUSTER MEMBER                
ALTER DATABASE ADD LOGFILE GROUP                         
ALTER DATABASE ADD LOGFILE MEMBER                        
ALTER DATABASE ARCHIVELOG                                
ALTER DATABASE CLEAR AUDIT TRAIL                         
ALTER DATABASE CLEAR PASSWORD HISTORY                    
ALTER DATABASE DATAFILE AUTOEXTEND ..                    
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS             
ALTER DATABASE DROP LOGFILE GROUP                        
ALTER DATABASE DROP LOGFILE MEMBER                       
ALTER DATABASE NOARCHIVELOG                              
ALTER DATABASE RENAME CHANGE TRACKING                    
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE         
ALTER DATABASE RENAME LOGFILE                            
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                
ALTER FUNCTION                                           
ALTER INDEX .. DISABLE                                   
ALTER INDEX .. ENABLE                                    
ALTER INDEX .. REBUILD                                   
ALTER INDEX .. RENAME                                    
ALTER INDEX .. STORAGE                                   
ALTER INDEX AGING                                        
ALTER PACKAGE                                            
ALTER PROCEDURE                                          
ALTER PROFILE                                            
ALTER SEQUENCE                                           
ALTER SEQUENCE .. SYNCHRONIZE                            
ALTER SYSTEM SWITCH LOGFILE                              
ALTER TABLE .. ADD COLUMN                                
ALTER TABLE .. ADD CONSTRAINT                            
ALTER TABLE .. ADD GLOBAL SECONDARY INDEX                
ALTER TABLE .. ADD SUPPLEMENTAL LOG                      
ALTER TABLE .. ALTER COLUMN .. AS IDENTITY               
ALTER TABLE .. ALTER COLUMN .. DROP DEFAULT              
ALTER TABLE .. ALTER COLUMN .. DROP IDENTITY             
ALTER TABLE .. ALTER COLUMN .. DROP NOT NULL             
ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE             
ALTER TABLE .. ALTER COLUMN .. SET DEFAULT               
ALTER TABLE .. ALTER COLUMN .. SET NOT NULL              
ALTER TABLE .. ALTER CONSTRAINT                          
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX              
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX AGING        
ALTER TABLE .. DROP CONSTRAINT                           
ALTER TABLE .. DROP GLOBAL SECONDARY INDEX               
ALTER TABLE .. DROP OFFLINE SEGMENTS                     
ALTER TABLE .. DROP SUPPLEMENTAL LOG                     
ALTER TABLE .. DROP UNUSABLE SEGMENTS                    
ALTER TABLE .. MERGE SHARDS .. INTO ..                   
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..         
ALTER TABLE .. OFFLINE INACTIVE CLUSTER MEMBERS          
ALTER TABLE .. READ ONLY                                 
ALTER TABLE .. READ WRITE                                
ALTER TABLE .. REBALANCE ..                              
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX            
ALTER TABLE .. RENAME COLUMN                             
ALTER TABLE .. RENAME CONSTRAINT                         
ALTER TABLE .. RENAME SHARD .. TO ..                     
ALTER TABLE .. RENAME TO ..                              
ALTER TABLE .. REORGANIZE                                
ALTER TABLE .. SET TRIGGER ORDER ..                      
ALTER TABLE .. SET UNUSED COLUMN                         
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP ..
ALTER TABLE .. STORAGE                                   
ALTER TABLE .. SYNCHRONIZE ..                            
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN               
ALTER TABLESPACE .. ADD                                  
ALTER TABLESPACE .. DROP                                 
ALTER TABLESPACE .. OFFLINE                              
ALTER TABLESPACE .. ONLINE                               
ALTER TABLESPACE .. RENAME TO                            
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }         
ALTER TRIGGER .. COMPILE                                 
ALTER TRIGGER .. DISABLE                                 
ALTER TRIGGER .. ENABLE                                  
ALTER TRIGGER .. RENAME TO ..                            
ALTER USER                                               
ALTER USER .. IDENTIFIED BY                              
ALTER VIEW                                               
ANALYZE SYSTEM COMPUTE STATISTICS                        
ANALYZE SYSTEM DELETE STATISTICS                         
ANALYZE TABLE .. DELETE STATISTICS                       
ANALYZE TABLE .. [COMPUTE|ESTIMATE] STATISTICS           
AUDIT POLICY                                             
COMMENT ON .. IS                                         
CREATE AUDIT POLICY                                      
CREATE CLUSTER GROUP                                     
CREATE FUNCTION                                          
CREATE INDEX                                             
CREATE LIBRARY                                           
CREATE PACKAGE                                           
CREATE PACKAGE BODY                                      
CREATE PROCEDURE                                         
CREATE PROFILE                                           
CREATE ROLE                                              
CREATE SCHEMA                                            
CREATE SEQUENCE                                          
CREATE SYNONYM                                           
CREATE TABLE                                             
CREATE TABLE ... AS SELECT                               
CREATE TABLESPACE                                        
CREATE TRIGGER                                           
CREATE USER                                              
CREATE VIEW                                              
DROP AUDIT POLICY                                        
DROP CLUSTER GROUP                                       
DROP FUNCTION                                            
DROP INDEX                                               
DROP LIBRARY                                             
DROP PACKAGE                                             
DROP PROCEDURE                                           
DROP PROFILE                                             
DROP ROLE                                                
DROP SCHEMA                                              
DROP SEQUENCE                                            
DROP SYNONYM                                             
DROP TABLE                                               
DROP TABLESPACE                                          
DROP TRIGGER                                             
DROP USER                                                
DROP VIEW                                                
FLASHBACK TABLE                                          
GRANT .. ON DATABASE                                     
GRANT .. ON LIBRARY                                      
GRANT .. ON PACKAGE                                      
GRANT .. ON PROCEDURE                                    
GRANT .. ON SCHEMA                                       
GRANT .. ON TABLE                                        
GRANT .. ON TABLESPACE                                   
GRANT USAGE ON ..                                        
GRANT role TO                                            
NOAUDIT POLICY                                           
PURGE CONSTRAINT                                         
PURGE DBA_RECYCLEBIN                                     
PURGE INDEX                                              
PURGE RECYCLEBIN                                         
PURGE TABLE                                              
PURGE TABLESPACE                                         
PURGE TRIGGER                                            
REVOKE .. ON DATABASE                                    
REVOKE .. ON LIBRARY                                     
REVOKE .. ON PACKAGE                                     
REVOKE .. ON PROCEDURE                                   
REVOKE .. ON SCHEMA                                      
REVOKE .. ON TABLE                                       
REVOKE .. ON TABLESPACE                                  
REVOKE USAGE ON ..                                       
REVOKE role TO                                           
TRUNCATE TABLE                                           

149 rows selected.
```

<a id="d5cef4fce2a220f8"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="9f8dcf90f3c80c1f"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="f92ef3d8665fc48c"></a>
| Item | Description |
| --- | --- |
| Name | DISABLE_DDL_CDC_GIVEUP |
| Summary | disable DDL which causing CDC give-up |
| Data type | BOOLEAN |
| Applicable phase | OPEN |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="dba27fc58d64b271"></a>
### Description

It prohibits DDL operations on tables with supplemental logging, because this affects the CDC's give up.  
For more information, refer to [The occurrence of give up and whether to allow DDL statement according to DDL category](../part-07-replication/55-cyclone.md#cd8a6e3b782422b6).

<a id="33d1778f51986829"></a>
## DISABLE_SERIAL_DDL

<a id="41e3622602bb9482"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="ff31987e14ca4437"></a>
| Item | Description |
| --- | --- |
| Name | DISABLE_SERIAL_DDL |
| Summary | disable Serial DDL |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="393714997ab8acac"></a>
### Description

DDL is executed for all cluster members after sequentially acquiring locks in a cluster environment, as described in [Processing DDL in Cluster](../part-03-sql-manual/12-sql-languages.md#5a68da92fee10cd0).  
DDL executed in this manner using the serial lock method is called serial DDL.

DDL statements affected by DISABLE_SERIAL_DDL can be queried as follows, and most schema DDLs fall under this category.

```
gSQL>
SELECT command
     , is_ddl
     , cluster_lock_mode
  FROM v$sql_command
 WHERE is_ddl = 'YES'
   AND cluster_lock_mode = 'SERIAL'
 ORDER BY 1
;

COMMAND                                           IS_DDL CLUSTER_LOCK_MODE
------------------------------------------------- ------ -----------------
ALTER AUDIT POLICY                                YES    SERIAL           
ALTER DATABASE CLEAR AUDIT TRAIL                  YES    SERIAL           
ALTER DATABASE CLEAR PASSWORD HISTORY             YES    SERIAL           
ALTER DATABASE DATAFILE AUTOEXTEND ..             YES    SERIAL           
ALTER FUNCTION                                    YES    SERIAL           
ALTER INDEX .. DISABLE                            YES    SERIAL           
ALTER INDEX .. ENABLE                             YES    SERIAL           
ALTER INDEX .. REBUILD                            YES    SERIAL           
ALTER INDEX .. RENAME                             YES    SERIAL           
ALTER INDEX .. STORAGE                            YES    SERIAL           
ALTER INDEX AGING                                 YES    SERIAL           
ALTER PACKAGE                                     YES    SERIAL           
ALTER PROCEDURE                                   YES    SERIAL           
ALTER PROFILE                                     YES    SERIAL           
ALTER SEQUENCE                                    YES    SERIAL           
ALTER TABLE .. ADD COLUMN                         YES    SERIAL           
ALTER TABLE .. ADD CONSTRAINT                     YES    SERIAL           
ALTER TABLE .. ADD GLOBAL SECONDARY INDEX         YES    SERIAL           
ALTER TABLE .. ADD SUPPLEMENTAL LOG               YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. AS IDENTITY        YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP DEFAULT       YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP IDENTITY      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP NOT NULL      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET DEFAULT        YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET NOT NULL       YES    SERIAL           
ALTER TABLE .. ALTER CONSTRAINT                   YES    SERIAL           
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX       YES    SERIAL           
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX AGING YES    SERIAL           
ALTER TABLE .. DROP CONSTRAINT                    YES    SERIAL           
ALTER TABLE .. DROP GLOBAL SECONDARY INDEX        YES    SERIAL           
ALTER TABLE .. DROP OFFLINE SEGMENTS              YES    SERIAL           
ALTER TABLE .. DROP SUPPLEMENTAL LOG              YES    SERIAL           
ALTER TABLE .. DROP UNUSABLE SEGMENTS             YES    SERIAL           
ALTER TABLE .. READ ONLY                          YES    SERIAL           
ALTER TABLE .. READ WRITE                         YES    SERIAL           
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX     YES    SERIAL           
ALTER TABLE .. RENAME COLUMN                      YES    SERIAL           
ALTER TABLE .. RENAME CONSTRAINT                  YES    SERIAL           
ALTER TABLE .. RENAME SHARD .. TO ..              YES    SERIAL           
ALTER TABLE .. RENAME TO ..                       YES    SERIAL           
ALTER TABLE .. SET TRIGGER ORDER ..               YES    SERIAL           
ALTER TABLE .. SET UNUSED COLUMN                  YES    SERIAL           
ALTER TABLE .. STORAGE                            YES    SERIAL           
ALTER TABLESPACE .. ADD                           YES    SERIAL           
ALTER TABLESPACE .. DROP                          YES    SERIAL           
ALTER TABLESPACE .. OFFLINE                       YES    SERIAL           
ALTER TABLESPACE .. ONLINE                        YES    SERIAL           
ALTER TABLESPACE .. RENAME TO                     YES    SERIAL           
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }  YES    SERIAL           
ALTER TRIGGER .. COMPILE                          YES    SERIAL           
ALTER TRIGGER .. DISABLE                          YES    SERIAL           
ALTER TRIGGER .. ENABLE                           YES    SERIAL           
ALTER TRIGGER .. RENAME TO ..                     YES    SERIAL           
ALTER USER                                        YES    SERIAL           
ALTER USER .. IDENTIFIED BY                       YES    SERIAL           
ALTER VIEW                                        YES    SERIAL           
ANALYZE SYSTEM COMPUTE STATISTICS                 YES    SERIAL           
ANALYZE SYSTEM DELETE STATISTICS                  YES    SERIAL           
ANALYZE TABLE .. DELETE STATISTICS                YES    SERIAL           
ANALYZE TABLE .. [COMPUTE|ESTIMATE] STATISTICS    YES    SERIAL           
AUDIT POLICY                                      YES    SERIAL           
COMMENT ON .. IS                                  YES    SERIAL           
CREATE AUDIT POLICY                               YES    SERIAL           
CREATE FUNCTION                                   YES    SERIAL           
CREATE INDEX                                      YES    SERIAL           
CREATE LIBRARY                                    YES    SERIAL           
CREATE PACKAGE                                    YES    SERIAL           
CREATE PACKAGE BODY                               YES    SERIAL           
CREATE PROCEDURE                                  YES    SERIAL           
CREATE PROFILE                                    YES    SERIAL           
CREATE ROLE                                       YES    SERIAL           
CREATE SCHEMA                                     YES    SERIAL           
CREATE SEQUENCE                                   YES    SERIAL           
CREATE SYNONYM                                    YES    SERIAL           
CREATE TABLE                                      YES    SERIAL           
CREATE TABLE ... AS SELECT                        YES    SERIAL           
CREATE TABLESPACE                                 YES    SERIAL           
CREATE TRIGGER                                    YES    SERIAL           
CREATE USER                                       YES    SERIAL           
CREATE VIEW                                       YES    SERIAL           
DROP AUDIT POLICY                                 YES    SERIAL           
DROP FUNCTION                                     YES    SERIAL           
DROP INDEX                                        YES    SERIAL           
DROP LIBRARY                                      YES    SERIAL           
DROP PACKAGE                                      YES    SERIAL           
DROP PROCEDURE                                    YES    SERIAL           
DROP PROFILE                                      YES    SERIAL           
DROP ROLE                                         YES    SERIAL           
DROP SCHEMA                                       YES    SERIAL           
DROP SEQUENCE                                     YES    SERIAL           
DROP SYNONYM                                      YES    SERIAL           
DROP TABLE                                        YES    SERIAL           
DROP TABLESPACE                                   YES    SERIAL           
DROP TRIGGER                                      YES    SERIAL           
DROP USER                                         YES    SERIAL           
DROP VIEW                                         YES    SERIAL           
FLASHBACK TABLE                                   YES    SERIAL           
GRANT .. ON DATABASE                              YES    SERIAL           
GRANT .. ON LIBRARY                               YES    SERIAL           
GRANT .. ON PACKAGE                               YES    SERIAL           
GRANT .. ON PROCEDURE                             YES    SERIAL           
GRANT .. ON SCHEMA                                YES    SERIAL           
GRANT .. ON TABLE                                 YES    SERIAL           
GRANT .. ON TABLESPACE                            YES    SERIAL           
GRANT USAGE ON ..                                 YES    SERIAL           
GRANT role TO                                     YES    SERIAL           
NOAUDIT POLICY                                    YES    SERIAL           
PURGE CONSTRAINT                                  YES    SERIAL           
PURGE DBA_RECYCLEBIN                              YES    SERIAL           
PURGE INDEX                                       YES    SERIAL           
PURGE RECYCLEBIN                                  YES    SERIAL           
PURGE TABLE                                       YES    SERIAL           
PURGE TABLESPACE                                  YES    SERIAL           
PURGE TRIGGER                                     YES    SERIAL           
REVOKE .. ON DATABASE                             YES    SERIAL           
REVOKE .. ON LIBRARY                              YES    SERIAL           
REVOKE .. ON PACKAGE                              YES    SERIAL           
REVOKE .. ON PROCEDURE                            YES    SERIAL           
REVOKE .. ON SCHEMA                               YES    SERIAL           
REVOKE .. ON TABLE                                YES    SERIAL           
REVOKE .. ON TABLESPACE                           YES    SERIAL           
REVOKE USAGE ON ..                                YES    SERIAL           
REVOKE role TO                                    YES    SERIAL           
TRUNCATE TABLE                                    YES    SERIAL           

125 rows selected.
```

DDL statements that are not affected by DISABLE_SERIAL_DDL can be queried as follows, and most cluster DDLs fall under this category.

```
gSQL>
SELECT command
     , is_ddl
     , cluster_lock_mode
  FROM v$sql_command
 WHERE is_ddl = 'YES'
   AND cluster_lock_mode <> 'SERIAL'
 ORDER BY 1
;

COMMAND                                                   IS_DDL CLUSTER_LOCK_MODE
--------------------------------------------------------- ------ -----------------
ALTER CLUSTER GROUP .. ADD CLUSTER MEMBER                 YES    MANUAL           
ALTER DATABASE ADD LOGFILE GROUP                          YES    NONE             
ALTER DATABASE ADD LOGFILE MEMBER                         YES    NONE             
ALTER DATABASE ARCHIVELOG                                 YES    NONE             
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS              YES    MANUAL           
ALTER DATABASE DROP LOGFILE GROUP                         YES    NONE             
ALTER DATABASE DROP LOGFILE MEMBER                        YES    NONE             
ALTER DATABASE NOARCHIVELOG                               YES    NONE             
ALTER DATABASE RENAME CHANGE TRACKING                     YES    NONE             
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE          YES    NONE             
ALTER DATABASE RENAME LOGFILE                             YES    NONE             
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                 YES    NONE             
ALTER SEQUENCE .. SYNCHRONIZE                             YES    MANUAL           
ALTER SYSTEM SWITCH LOGFILE                               YES    NONE             
ALTER TABLE .. MERGE SHARDS .. INTO ..                    YES    MANUAL           
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..          YES    MANUAL           
ALTER TABLE .. OFFLINE INACTIVE CLUSTER MEMBERS           YES    MANUAL           
ALTER TABLE .. REBALANCE ..                               YES    MANUAL           
ALTER TABLE .. REORGANIZE                                 YES    MANUAL           
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP .. YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE ..                             YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

24 rows selected.
```

<a id="0077b3010638de68"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="ab7455c951ddff92"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="a3fe6c91c60c96f4"></a>
| Item | Description |
| --- | --- |
| Name | DISABLE_UPDATE_PK_CDC_GIVEUP |
| Summary | disable UPDATE primary key which caused CDC give-up |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="288afe31b46e7ef7"></a>
### Description

It disables the UPDATE operation on the primary key that causes CDC to give up.

<a id="dc1c42f04b9c279e"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="1f34d71bd42d3d1d"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE**

<a id="980e60d23bef7ed4"></a>
| Item | Description |
| --- | --- |
| Name | DISALLOWED_PROTOCOL_TARGETTYPE |
| Summary | disallowed TARGETTYPE protocol |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="8832b33f56a6c8a3"></a>
### Description

It disallows the TARGETTYPE protocol.

<a id="689e7bac4445f958"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="fe7d44dfd7105654"></a>
### Basic Information

<a id="a0845aed035da60e"></a>
| Item | Description |
| --- | --- |
| Name | DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL |
| Summary | disallowed TARGETTYPE_WITH_ALL protocol |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="97778396501bac3c"></a>
### Description

It disallows the TARGETTYPE_WITH_ALL protocol.

<a id="ff80fe8d691a9a95"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="62735002012fdbbd"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="0a43d940d7abe9e2"></a>
| Item | Description |
| --- | --- |
| Name | DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME |
| Summary | disallowed TARGETTYPE_WITH_NAME protocol |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="e9a8ea648c674bcb"></a>
### Description

It disallows the TARGETTYPE_WITH_NAME protocol.

<a id="0bdea21f3c641073"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="b5385b3ca7ca3e14"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_BUFFER_SIZE**

<a id="6e59054c6660fae5"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_CM_BUFFER_SIZE |
| Summary | communication buffer size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 10485760 |
| MAX | 34359738368 |
| Default value | 31457280 |

<a id="cbd5474dd90a7e21"></a>
### Description

It is the size of the entire communication buffer used in shared mode. This buffer is allocated to and utilized in the Shared Static Area (SSA).

<a id="fdf1bd2d5fac934e"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="a971674016f22019"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_UNIT_SIZE**

<a id="e974e8e24799166b"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_CM_UNIT_SIZE |
| Summary | communication unit size |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1024 |
| MAX | 10485760 |
| Default value | 1024 |

<a id="2b75a7230f40d5be"></a>
### Description

It is the unit size managed by the dispatcher in shared mode. If the size is large, the memory is wasted. If it is small, performance can be degraded. It is set to the maximum size of the communication packet in shared mode.

<a id="75c88642137f1069"></a>
## DISPATCHER_CONNECTIONS

<a id="8e38c0547bf58cd8"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="c72a4aa6a49c6fa7"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_CONNECTIONS |
| Summary | maximum number of connections for each dispatcher |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10 |
| MAX | 32768 |
| Default value | 950 |

<a id="39a8751511b32d08"></a>
### Description

It is the maximum number of connections (clients) that a dispatcher can manage in shared mode.  
If the system- supported maximum value is smaller than the specified value, it is internally adjusted to the system maximum.

<a id="ac8b7c5b00cbd080"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="6b9254d9cab24427"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="ea09c467661e0d43"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_HOT_POLICY_INTERVAL |
| Summary | dispatcher dequeue interval for busy waiting |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000: 1 day |
| Default value | 100000: 0.1 second |

<a id="f245ed1cfd369d14"></a>
### Description

It is the dispatcher dequeue interval for busy waiting. (in microseconds)

<a id="0b50c94cb7c94bdd"></a>
## DISPATCHER_LOAD_BALANCING

<a id="9d6949ccb8ac4f89"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="d3b1c974c98e855a"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_LOAD_BALANCING |
| Summary | load balancing algorithm for shared mode (0: number of clients, 1: round robin) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="191186fdbccaf6a6"></a>
### Description

It is an algorithm that allocates a dispatcher when connecting to a client in shared mode.

- 0: It allocates to a dispatcher with a small number of currently connected clients.
- 1: It allocates sequentially to a dispatcher.

<a id="44c534c4fc99a77b"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="38fd3e74322b2a3f"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="ee32816fffa4ddf2"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_NUMA_STREAM_MAP |
| Summary | numa stream map for dispatcher |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | 'x' : no binding |

<a id="df438947f9cdfa85"></a>
### Description

It determines the NUMA node to which dispatchers are connected. This property is effective when the NUMA property is set to on.

The following is an example of three dispatchers. It connects stream number 0 to NUMA node 0, stream number 1 to NUMA node 1, and stream number 2 to NUMA node 2.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="e91129340723ac29"></a>
## DISPATCHER_QUEUE_SIZE

<a id="580aac33e1a7e0e8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="1109b72bcd8fbc1d"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_QUEUE_SIZE |
| Summary | dispatcher queue size |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1024 |
| MAX | 32768 |
| Default value | 1024 |

<a id="e984c5f738a0ec50"></a>
### Description

In shared mode, it sets the queue size for communication between the dispatcher and the shared-server.

<a id="d3254b52387959dc"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="e271f4c462b2fdbc"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="fa7b50abb5f6f1ed"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_REQUEST_MINI_QUEUE_COUNT |
| Summary | count of mini queue per request queue |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 16 |
| Default value | 4 |

<a id="45d207981af5c95d"></a>
### Description

It is the count of mini queues per request queue.

<a id="7b21c28690e2d157"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="f79397ffb5d4b7ff"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="41e33a6e0c9b1c7a"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHER_RESPONSE_MINI_QUEUE_COUNT |
| Summary | count of mini queue per response queue |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 16 |
| Default value | 4 |

<a id="e4ba9c33970eca61"></a>
### Description

It is the count of mini queues per response queue.

<a id="7bc8d5c1580a913f"></a>
## DISPATCHERS

<a id="fc4534a66b8cb7c4"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="d0929e40fbcb75d8"></a>
| Item | Description |
| --- | --- |
| Name | DISPATCHERS |
| Summary | number of dispatcher processes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 256 |
| Default value | 2 |

<a id="c1ca057aa07bdc26"></a>
### Description

It sets the number of dispatcher processes when using the shared mode.  
During the open phase, the value can not be reduced using the alter system.

<a id="47d0b7665fc30c18"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="f082421eeacce180"></a>
### Basic Information

<a id="2e09efe1b166ecb8"></a>
| Item | Description |
| --- | --- |
| Name | EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY |
| Summary | execute instant hash table using available memory even if not enough |
| Data type | BOOLEAN |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="e47d862f7be833c6"></a>
### Description

If there is insufficient memory to expand the hash bucket in a query using an instant hash table, it determines whether to fail the query or to execute it without expanding the hash bucket.

<a id="f3a4f80921f33e10"></a>
## EXTLIB_DIR

<a id="4b047a4fcbf955bd"></a>
### Basic Information

<a id="3f9f94867e539b42"></a>
| Item | Description |
| --- | --- |
| Name | EXTLIB_DIR |
| Summary | external library directory |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/extlib |

<a id="78e9913f007efff0"></a>
### Description

It specifies the path for the shared library used to call external library functions.

<a id="a93164f29fe016c1"></a>
## FETCH_FAILOVER

<a id="054657cf67bd4b8b"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="2c217af655737eed"></a>
| Item | Description |
| --- | --- |
| Name | FETCH_FAILOVER |
| Summary | enable fetch failover |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="c11a03dabd21093d"></a>
### Description

It enables fetch failover.

<a id="bb021e3d6953b2ba"></a>
## FULL_TABLE_SCAN_CACHING_THRESHOLD

<a id="f35b8cbc19c1a1f5"></a>
### Basic Information

<a id="b0ed073dbbf5a3fb"></a>
| Item | Description |
| --- | --- |
| Name | FULL_TABLE_SCAN_CACHING_THRESHOLD |
| Summary | upper threshold of table size for buffer caching while full scan |
| Data type | BIGINT |
| Applicable phase | NO MOUNT above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1000 |
| Default value | 20 |

<a id="ee46401a1144b997"></a>
### Description

The table size threshold determines whether to cache tables created in the disk tablespace to the buffer cache during a full scan. The FULL_TABLE_SCAN_CACHING_THRESHOLD sets this threshold value. The default value is 20. In this case, only tables using a number of pages less than or equal to 2.0% of [BUFFER_CACHE_SIZE](#42a6f9bb91593e38) are cached. If this value is set to 1000 (100%), all tables will be cached in the buffer during a full scan.

For example, if BUFFER_CACHE_SIZE is 8192 and FULL_TABLE_SCAN_CACHING_THRESHOLD is 509 (50.9%), then only tables using a number of pages less than or equal to 4169 (50.9% of 8192) will be cached in the buffer during a full scan.

<a id="6080055e2e0683b7"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="802cf58aaabb3747"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="ce19c067ff2114be"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY |
| Summary | allowed session dependent features in global connection |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="057abdfc967590d1"></a>
### Description

It determines whether to support query execution that includes session-dependent information in the global connection.

<a id="cb6ae834b617697c"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="95b8b34833e8ce65"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="04e406c442fcacfd"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_JOURNAL_BUFFER_SIZE |
| Summary | global journal buffer size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1024 |
| MAX | 10 Giga |
| Default value | 1 Mega |

<a id="d38fecf4f0b9ac1a"></a>
### Description

It is the size of the global journal buffer.

<a id="023794ec2991441e"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="fab36644f344d545"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="adbf3c200f57ee7a"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE |
| Summary | global journal buffer total max size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 Mega |
| MAX | 100 Giga |
| Default value | 64 Mega |

<a id="a174252cec2e9fb8"></a>
### Description

It is the total max size of the global journal buffer.

<a id="11daa03bc52629e8"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="cadb47d8f652ce09"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="5d4f64f8d5641b57"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_PROPERTY_LOCK_TIMEOUT |
| Summary | a time limit(second) for how long global property lock statements will wait |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 (infinite) |
| MAX | 100000000 |
| Default value | 0 |

<a id="ac481b3823e2d7f5"></a>
### Description

When changing the global property, a lock is performed to control concurrency. In this case, the waiting time to acquire the lock is set.

<a id="2ae67e099f2e725b"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="a1f969d58a9fb502"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="f3665e8b36179754"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_COMMIT_WRITE_MODE |
| Summary | global transaction commit write mode (0: no_wait, 1: wait, 2: disable) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| Default value | 2 |

<a id="a2b91ca4c5073fde"></a>
### Description

It is a property that changes the commit write mode of the global transaction. The TRANSACTION_COMMIT_WRITE_MODE property applies to all transactions, but the GLOBAL_TRANSACTION_COMMIT_WRITE_MODE property applies only to global transactions. If the property is set to 2, it follows the TRANSACTION_COMMIT_WRITE_MODE.

- 0: It does not wait.
- 1: It waits.
- 2: It follows the value of TRANSACTION_COMMIT_WRITE_MODE.

<a id="3d52157e6a61d4b1"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="29c8cc579732612c"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="5d43cf869438a6ab"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_ISOLATION_SCOPE |
| Summary | isolation scope for global transaction(0: system, 1: group) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="b1a3064a43308286"></a>
### Description

It determines whether to process the data with a global transaction or with multiple domain transactions when the transaction modifies data across two cluster groups.

- 0: It processes with a global transaction.
- 1: It processes with multiple domain transactions.

> If this property is set to 1, it commits each cluster group with a separate transaction, which does not guarantee transaction atomicity.

<a id="66a67ed16a51a315"></a>
## GLOBAL_TRANSACTION_LOG_BLOCK_SIZE

<a id="735fe254a74d00e4"></a>
### Basic Information

<a id="3bc954a7471403fe"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_LOG_BLOCK_SIZE |
| Summary | block size of global transaction log file(byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 512 |
| MAX | 4096 |
| Default value | 512 |

<a id="440cb5691f1b8e7c"></a>
### Description

GLOBAL_TRANSACTION_LOG_BLOCK_SIZE specifies the block size of the global transaction log file. It should be set to one of 512, 1024, 2048, 4096.

<a id="fdd8749dd961dc3f"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="b93a62f2dd65c778"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="1e50cafa3b26a4de"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_LOG_DIR |
| Summary | default global transaction log directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/wal |

<a id="2f0b93e037db378f"></a>
### Description

It is the default directory for the global transaction log.

<a id="e45094e961735bb5"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="087263a5c5898e50"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="70a71e628b7bb4ee"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_LOG_FILE_SIZE |
| Summary | global transaction log file size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 20 Mega |
| MAX | 10 Giga |
| Default value | 100 Mega |

<a id="20c20c8f3b81bae1"></a>
### Description

It is the file size of the global transaction log.

<a id="85439fd49ea5a0af"></a>
## GMASTER_NUMA_NODE

<a id="2b71956a9ce0d613"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="aeba9c5c5dcd0a50"></a>
| Item | Description |
| --- | --- |
| Name | GMASTER_NUMA_NODE |
| Summary | numa node for gmaster process |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | -1 |
| MAX | 63 |
| Default value | -1 |

<a id="a69b7d510e57226c"></a>
### Description

It sets the ID of the NUMA node to be used by the gmaster daemon. This property is effective when the NUMA property is set to on.

<a id="ffc29a216715856f"></a>
## GMON_AUTOSTART

<a id="a625cb52106918c4"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="257db010f875f171"></a>
| Item | Description |
| --- | --- |
| Name | GMON_AUTOSTART |
| Summary | Indicate whether gmon process automatically starts or not ( 0 \| 1 ) |
| Data type | BOOLEAN |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 1 |

<a id="991c953d5deeb30f"></a>
### Description

It determines whether to start the gmon process automatically.

<a id="da1704a6f1c24ba1"></a>
## HINT_ERROR

<a id="ec84ce06e1d008fc"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="f395883736369317"></a>
| Item | Description |
| --- | --- |
| Name | HINT_ERROR |
| Summary | enable hint error |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="f9b5d6d68e44af8b"></a>
### Description

It sets whether to check for syntax errors and validation errors in hint syntax.

<a id="72887d9d523d11fa"></a>
## HISTOGRAM_BALANCE_BUCKET_COUNT

<a id="78743469c51d99a0"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="c5a5fd8a71015e26"></a>
| Item | Description |
| --- | --- |
| Name | HISTOGRAM_BALANCE_BUCKET_COUNT |
| Summary | bucket count for height-balanced histogram when ANALYZE TABLE |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 0 |
| MAX | 1000 |
| Default value | 0 |

<a id="38fe34269d6c2d66"></a>
### Description

It is the number of buckets required to create a height-balanced histogram when performing ANALYZE TABLE.

The recommended value is 20.

If the value is 5 or smaller, the histogram information is not built.

<a id="1fd9a37f61769b96"></a>
## HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT

<a id="84646893120721c8"></a>
### Basic Information

<a id="f3ff77b5bb46ecf9"></a>
| Item | Description |
| --- | --- |
| Name | HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT |
| Summary | maximum sampling count for height-balanced histogram when ANALYZE TABLE |
| Data type | BIGINT |
| Applicable phase | OPEN or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 100000 |
| MAX | 1000000000 |
| Default value | 100000 |

<a id="ccd54d953f50b1fd"></a>
### Description

It is the maximum number of data items to sample when building height-balanced histogram information.

<a id="7628241bceaa2159"></a>
## HISTOGRAM_FREQUENCY_BUCKET_COUNT

<a id="79e7fd152b3f464d"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="3724e10cf32804f9"></a>
| Item | Description |
| --- | --- |
| Name | HISTOGRAM_FREQUENCY_BUCKET_COUNT |
| Summary | bucket count for frequency histogram when ANALYZE TABLE |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 0 |
| MAX | 1000 |
| Default value | 0 |

<a id="f887d7f918e2e802"></a>
### Description

It is the number of buckets used as the standard for creating the frequency histogram when performing ANALYZE TABLE.

The recommended value is 20.

If the value is 5 or smaller, the histogram information is not built.

If the number of frequency buckets to create is greater than the HISTOGRAM_FREQUENCY_BUCKET_COUNT property, then the frequency histogram is not created.

<a id="c0e55cde3ca3e473"></a>
## IDLE_TIMEOUT

<a id="0e063cb5b281e1ad"></a>
### Basic Information

**Basic Information of IDLE_TIMEOUT**

<a id="91b7d23f77e7c648"></a>
| Item | Description |
| --- | --- |
| Name | IDLE_TIMEOUT |
| Summary | idle timeout(s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="41a0421087d0cf7d"></a>
### Description

It sets the maximum IDLE time that can be waited in a C/S session. If it exceeds the specified idle time, a TIMEOUT error occurs.

- 0: It means infinite waiting, and a TIMEOUT error does not occur.

<a id="7e27fada251494d2"></a>
## IN_DOUBT_DECISION

<a id="b885fa8133ec4270"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="c96c072758ef707c"></a>
| Item | Description |
| --- | --- |
| Name | IN_DOUBT_DECISION |
| Summary | decision for in-doubt transaction |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| Default value | 2 |

<a id="724b556d0497fb6a"></a>
### Description

It determines whether to commit or roll back the in-doubt transaction of distributed transactions.

- 1: Commit
- 2: Rollback

<a id="8ca9b07ef087d4d0"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="e103a5301f498650"></a>
### Basic Information

<a id="ed746a1925a817e6"></a>
| Item | Description |
| --- | --- |
| Name | IN_KEY_RANGE_ARRAY_COUNT |
| Summary | array count for in key range scan |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| Default value | 20 |

<a id="93385018158bcd7a"></a>
### Description

It is the maximum number of target values of the *in key range* that can perform the *in key range scan* based on the array.

- IN_KEY_RANGE_ARRAY_COUNT must be 3 or greater to perform the *in key range scan* based on an array for the statement below.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

If the maximum number of target values of the *in key range* exceeds the IN_KEY_RANGE_ARRAY_COUNT value, the *in key range scan* is performed based on an instant table.

<a id="a1e92d22f453f73b"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="8c5408a8d804eaf2"></a>
### Basic Information

<a id="82a13110b53b9bd2"></a>
| Item | Description |
| --- | --- |
| Name | INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE |
| Summary | number of pages read in one I/O operation during an incremental backup |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| Default value | 32 |

<a id="ccbf028e5b5752d2"></a>
### Description

It sets the number of pages to read in a single disk IO operation for performing an incremental backup of the disk tablespace.

<a id="208b2579f8a70601"></a>
## INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA

<a id="0589574e93cb5bd9"></a>
### Basic Information

<a id="ddc00c0e9deb6d51"></a>
| Item | Description |
| --- | --- |
| Name | INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA |
| Summary | criteria for the number of flush page count to update datafile header |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1000 |
| MAX | 134217728 |
| Default value | 134217728 |

<a id="376dd90b232a664d"></a>
### Description

It sets the criteria for updating the data file header in the disk tablespace. It specifies the LSN to start recovery in the datafile header when the number of pages updated reaches the specified value, while the IO slave applies the pages updated in the buffer cache to the disk. This approach reduces disk I/O during restart recovery.

<a id="bb198743308571ad"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="c00b2ad3aafffe9d"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="555af715603375d8"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_BUILD_PARALLEL_FACTOR |
| Summary | index build parallel factor |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| Default value | 0 |

<a id="1e3bdef446a41a4c"></a>
### Description

When creating an index, it specifies the parallel factor.

- 0: It is specified as the number of core factors in the system.

<a id="589f961b7faeb58f"></a>
## INDEX_MERGE_RUN_COUNT

<a id="42cd3f633551be07"></a>
### Basic Information

**Basic Information of MEMORY_MERGE_RUN_COUNT**

<a id="37e43fe1e82a74ff"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_MERGE_RUN_COUNT |
| Summary | merge run count for memory index |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 64 |
| Default value | 32 |

<a id="3cc5c83052368388"></a>
### Description

The memory B-tree index using a bottom-up approach is created by extracting all keys from a table, sorting them in units defined by a specific block size (INDEX_SORT_RUN_SIZE), merging the sorted blocks, and generating the internal node. INDEX_MERGE_RUN_COUNT sets the number of sorted blocks to be merged at one time.

<a id="93733976ef35cbc1"></a>
### ALIAS

<a id="e2e0c5cd1b996eee"></a>
| Item | Description |
| --- | --- |
| Original name | INDEX_MERGE_RUN_COUNT |
| ALIAS | MEMORY_MERGE_RUN_COUNT |

<a id="13a1c933a43df373"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="ffc5655863d056e6"></a>
### Basic Information

<a id="3e0a9f739218ccf1"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_REBUILD_BLOCK_READ_COUNT |
| Summary | value count for a block read for index rebuild |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| Default value | 100 |

<a id="902838c023e9ff3f"></a>
### Description

When DML operations are performed while rebuilding the index in ONLINE mode, the journal data is stored. The index is rebuilt based on the data at the start of the rebuilding process, and the updated data during the rebuild is applied to the index using the journal data. INDEX_REBUILD_BLOCK_READ_COUNT sets the amount of journal data to be read and applied to the index during this process.

<a id="480eea6bbf3d02b1"></a>
## INDEX_SELF_AGING_TRHESHOLD

<a id="09a42b34fc0e94c1"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="c2bbec07183c0d87"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_SELF_AGING_THRESHOLD |
| Summary | the threshold for processing empty nodes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1048576 |
| Default value | 0 |

<a id="68c47de10bf6da04"></a>
### Description

An index page is not removed from the index even when all keys are deleted and is managed as an empty node. When a new page is required, the possibility of reusing the empty node is checked, and if it can be reused, it is returned to the index segment (aging).  
If an empty node exists in the index, deleted keys are also included in index scans, which may affect performance.  
INDEX_SELF_AGING_THRESHOLD sets the number of empty nodes at which empty node aging is performed when deleting keys from an index. That is, aging is attempted when the number of empty nodes is greater than or equal to INDEX_SELF_AGING_THRESHOLD during key deletion.

- 0: Empty node aging is not performed when deleting keys.

> When deleting keys, the possibility of aging an empty node is checked to perform self aging. However, performance may degrade because self aging may still be attempted even when aging is not possible. Therefore, using INDEX_SELF_AGING_THRESHOLD is recommended when deleting a large number of records through index scans.

<a id="b49e5c4915accfc6"></a>
## INDEX_SORT_RUN_SIZE

<a id="2aed6ec32f7a2860"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="34cb96f10f3e4f47"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_SORT_RUN_SIZE |
| Summary | sort run size for memory index (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8192 |
| MAX | 1048576 |
| Default value | 1048576 |

<a id="1c0419c0eaff6f60"></a>
### Description

The memory B-tree index using a bottom-up approach is created by extracting all keys from a table, sorting them in units defined by a specific block size (INDEX_SORT_RUN_SIZE), merging the sorted blocks, and generating the internal node. INDEX_SORT_RUN_SIZE sets the size of a single block to be sorted.

<a id="88ab7d2af4cf95e6"></a>
### ALIAS

<a id="78f66b669319b9de"></a>
| Item | Description |
| --- | --- |
| Original name | INDEX_SORT_RUN_SIZE |
| ALIAS | MEMORY_SORT_RUN_SIZE |

<a id="45d0e04414478b3e"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="c7dd0096d7e39aa2"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="072cb3c80cdf8f41"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_TREE_MERGE_PARALLEL_FACTOR |
| Summary | parallel factor for merging sub-trees |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| Default value | 0 |

<a id="ef76fe165e0cf81d"></a>
### Description

When creating an index, it specifies the number of parallel factors for merging the sub-trees.   
If this value exceeds INDEX_BUILD_PARALLEL_FACTOR, then INDEX_BUILD_PARALLEL_FACTOR is used.

- 0: It follows the INDEX_BUILD_PARALLEL_FACTOR.

<a id="dfe7194142dd5f21"></a>
## INST_ALLOCATOR_COUNT

<a id="b1389becdd459817"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="9ebfd150903bb0fc"></a>
| Item | Description |
| --- | --- |
| Name | INST_ALLOCATOR_COUNT |
| Summary | memory allocator count for instant tables or indexes |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 3 |
| MAX | 128 |
| Default value | 3 |

<a id="140bfb19104f3718"></a>
### Description

This property increases the parallelism of operations that allocate or delete an instant block.

<a id="06aef1f45d49b860"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="2fa20ed4318235cc"></a>
### Basic Information

<a id="2ba8eaa48113aa88"></a>
| Item | Description |
| --- | --- |
| Name | INST_HASH_TABLE_BUCKET_MAX_COUNT |
| Summary | instant hash table bucket max count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 4294967295 |
| Default value | 0 |

<a id="efc1d5c49ae5f74f"></a>
### Description

It sets the maximum expected bucket counts for the hash instant table.

<a id="b88cb19b3df8ec64"></a>
## INST_TABLE_PAGE_SIZE

<a id="4ecb7e1f7ce8b7f5"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="09a2a8fb09642c7c"></a>
| Item | Description |
| --- | --- |
| Name | INST_TABLE_PAGE_SIZE |
| Summary | a page size of instant tables |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8192 |
| MAX | 1048576 |
| Default value | 16384 |

<a id="4a82aca1caf6d892"></a>
### Description

It determines the page size of an instant table. If the anchor area of an instant record is larger than the instant block, then the following error occurs.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="9561dd96312827c4"></a>
### ALIAS

<a id="8d48df6fb1504180"></a>
| Item | Description |
| --- | --- |
| Original name | INST_TABLE_PAGE_SIZE |
| ALIAS | INST_TABLE_BLOCK_SIZE |

<a id="58a8930e680eb3f9"></a>
## INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD

<a id="6111eab4db3c2987"></a>
### Basic Information

<a id="5118f0d87c26a14b"></a>
| Item | Description |
| --- | --- |
| Name | INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD |
| Summary | threshold of the size to be stored as a reference column in an instant index |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 8192 |
| Default value | 64 |

<a id="81a29cd627f625a9"></a>
### Description

It stores columns whose sizes are greater than or equal to this property as references when storing columns in the instant index.

If the key of the instant index exceeds the size limit (16,000 bytes), adjust this property to reduce the key size. Storing columns as references can decrease the size of the instant index by reducing the key size, but this may downgrade performance.

```
gSQL> SELECT /*+ USE_GROUP_SORT */ * FROM T1 GROUP BY C1,C2,C3,C4,C5,C6,C7,C8;

ERR-RD000(14066): key size(16025) of the instant index exceeds the limit(16000)

gSQL> ALTER SESSION SET INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD = 64;

Session altered.

gSQL> SELECT /*+ USE_GROUP_SORT */ * FROM T1 GROUP BY C1,C2,C3,C4,C5,C6,C7,C8;

1 row selected.
```

<a id="646a826ca4ce41ac"></a>
## INSTANT_WORK_AREA_SIZE

<a id="a0cccadc30a297b4"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="035e6a41bf8fe5f7"></a>
| Item | Description |
| --- | --- |
| Name | INSTANT_WORK_AREA_SIZE |
| Summary | memory area size for instant segment |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 ( 1 Terabytes ) |
| Default value | 65536 |

<a id="e73ff7a9b7dbec71"></a>
### Description

An instant table is used when temporary storage space is required, such as for ORDER BY operations. It is stored in memory up to the size specified by this property when stacking the instant table, and if more space is needed, the TEMPORARY TABLESPACE allocates the additional space.

> To query the FIXED TABLE, this property value is assumed to be infinite until the MOUNT phase or below.

<a id="a85f077bb2745e31"></a>
## IPC_CHANNEL_COUNT

<a id="2999b526e56b64b0"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="073d67740f5c75b6"></a>
| Item | Description |
| --- | --- |
| Name | IPC_CHANNEL_COUNT |
| Summary | IPC Channel Count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 2048 |
| Default value | 0 |

<a id="358c31d29cebe02f"></a>
### Description

It sets the number of channels for IPC communication.

<a id="91f84ac97314c2ee"></a>
## JOURNAL_TEMP_DIR

<a id="6593a8f09b07c516"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="337dd9b5a6120326"></a>
| Item | Description |
| --- | --- |
| Name | JOURNAL_TEMP_DIR |
| Summary | journaling temporary directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/journal |

<a id="0de27a42488d0bf3"></a>
### Description

It is the temporary directory for journaling.

<a id="d2150461932a63b0"></a>
## KEEPALIVE_IDLE_TIME

<a id="3fd2fef3e4b93ede"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="37432ca254ebc25f"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Summary | tcp keepalive idle time for checking dead client session (sec) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 16383 |
| Default value | 300 |

<a id="1783f81418e3116d"></a>
### Description

It means the idle duration between the server and client without tcp packet exchange before sending a keep alive packet. If there is no tcp packet exchange for the specified duration (KEEPALIVE_IDLE_TIME), the keep alive mechanism is activated to detect dead connections on the server side.

<a id="d611c345309d2964"></a>
## LOCAL_CLUSTER_MEMBER

<a id="55c6a857b9d2ee87"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="ba81170bb5ebe2ed"></a>
| Item | Description |
| --- | --- |
| Name | LOCAL_CLUSTER_MEMBER |
| Summary | local cluster member name |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | N/A |
| MAX | N/A |
| Default value | 'G1N1' |

<a id="0e5cc77aafb9dc32"></a>
### Description

It is the name of the local cluster member.

<a id="a377ee96979d13cf"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="fc16f9c750f07de1"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="8aea854cbf49cc42"></a>
| Item | Description |
| --- | --- |
| Name | LOCAL_CLUSTER_MEMBER_HOST |
| Summary | host name of local cluster member |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | N/A |
| MAX | N/A |
| Default value | '127.0.0.1' |

<a id="56130c92e64762e6"></a>
### Description

It is the host name of the local cluster member.

<a id="5ab74975c2e29251"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="387cd15d7b26c9e4"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="83335f6b9e7a2014"></a>
| Item | Description |
| --- | --- |
| Name | LOCAL_CLUSTER_MEMBER_PORT |
| Summary | listen port of local cluster member |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 1024 |
| MAX | 49151 |
| Default value | 10101 |

<a id="4f5ec51b472ca935"></a>
### Description

It is the listen port of the local cluster member.

<a id="89f1f1736156856e"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="06ce19dece16e105"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="0dda2f42667d8445"></a>
| Item | Description |
| --- | --- |
| Name | LOCAL_JOURNAL_BUFFER_SIZE |
| Summary | local journal buffer size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1024 |
| MAX | 10737418240 (10 Giga) |
| Default value | 65536 |

<a id="65df71c24339b09e"></a>
### Description

It is the size of the local journal buffer.

<a id="05f219122b42a044"></a>
## LOCATION_FILE

<a id="298e81c37c7826ff"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="a5f4ad7507bb7540"></a>
| Item | Description |
| --- | --- |
| Name | LOCATION_FILE |
| Summary | location file name |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/wal/location.ctl |

<a id="99b154bd736c2bbc"></a>
### Description

It is the location file name.

<a id="1efe52fc87229d75"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="fbf669cc7fa9ca47"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="baa3872baf1e02cb"></a>
| Item | Description |
| --- | --- |
| Name | LOCATOR_QUERY_TIMEOUT |
| Summary | timeout for waiting locator response (sec) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 20 |

<a id="c3f96ee29ebd7004"></a>
### Description

It sets the waiting time (in seconds) for a response after the cluster system inquires a locator about the resolution of a split-brain situation. This property is only utilized when the CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or higher.

<a id="61de995a1abc3682"></a>
## LOCK_HASH_TABLE_SIZE

<a id="cd096c81753438aa"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="38eda3e947a4e956"></a>
| Item | Description |
| --- | --- |
| Name | LOCK_HASH_TABLE_SIZE |
| Summary | lock manager hash table size (The number of buckets) |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 1000000 |
| Default value | 65519 |

<a id="7f238d497efe4041"></a>
### Description

It specifies the maximum size of the hash table managed by the lock manager.

<a id="54f5ea2ce441327f"></a>
## LOCKABLE_DISPATCHER_CM_BUFFER_COUNT

<a id="70019df144293398"></a>
### Basic Information

<a id="4191d886a53eca98"></a>
| Item | Description |
| --- | --- |
| Name | LOCKABLE_DISPATCHER_CM_BUFFER_COUNT |
| Summary | communication buffer count for lockable dispatcher |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 128 |
| Default value | 1 |

<a id="610b71155437aa85"></a>
### Description

It specifies the number of communication buffers for the cluster lockable dispatcher.

<a id="eb9179b865f989bf"></a>
## LOCKLESS_DISPATCHER_CM_BUFFER_COUNT

<a id="b3f9d7a228ea7b3a"></a>
### Basic Information

<a id="3b3e21ffa3b2e818"></a>
| Item | Description |
| --- | --- |
| Name | LOCKLESS_DISPATCHER_CM_BUFFER_COUNT |
| Summary | communication buffer count for lockless dispatcher |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 128 |
| Default value | 1 |

<a id="ff71156ad436bcbc"></a>
### Description

It specifies the number of communication buffers for the cluster lockless dispatcher.

<a id="4fb5ce095be99e73"></a>
## LOG_BLOCK_SIZE

<a id="91c1d5fcc68e886e"></a>
### Basic Information

**Basic Information of LOG_BLOCK_SIZE**

<a id="99963ef250b758ab"></a>
| Item | Description |
| --- | --- |
| Name | LOG_BLOCK_SIZE |
| Summary | log block size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 512 |
| MAX | 4096 |
| Default value | 512 |

<a id="903d970c573b5853"></a>
### Description

It indicates the minimum size of the log buffer that is flushed to the log file on the disk. Its value must be set to one of 512, 1024, 2048, 4096.

<a id="76954616ac7cdede"></a>
## LOG_BUFFER_SIZE

<a id="069896b00f41f37a"></a>
### Basic Information

**Basic Information of LOG_BUFFER_SIZE**

<a id="7f2eb07bd32b0d54"></a>
| Item | Description |
| --- | --- |
| Name | LOG_BUFFER_SIZE |
| Summary | default log buffer size (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1048576 |
| MAX | 10737418240 |
| Default value | 10485760 |

<a id="20f0aec42714507a"></a>
### Description

A log buffer is a shared memory space where redo logs generated by DML/DDL operations in the database are stored. The LOG_BUFFER_SIZE parameter is referenced to set the memory size for the log buffer.

<a id="947fe6d80bb1be80"></a>
## LOG_DIR

<a id="2e2f6982fe20c9be"></a>
### Basic Information

**Basic Information of LOG_DIR**

<a id="e2fdbe39f4f5fd64"></a>
| Item | Description |
| --- | --- |
| Name | LOG_DIR |
| Summary | default log direcotry |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/wal |

<a id="c28d85ecf00696c9"></a>
### Description

The log recorded in the log buffer is flushed to a logfile located on a non-volatile storage device to ensure database durability. The LOG_DIR parameter sets the path to the log file.

<a id="f505fc3f76ab187c"></a>
## LOG_FILE_SIZE

<a id="369227c9caa4bd27"></a>
### Basic Information

**Basic Information of LOG_FILE_SIZE**

<a id="e3c6c0a0071dcd4f"></a>
| Item | Description |
| --- | --- |
| Name | LOG_FILE_SIZE |
| Summary | log file size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 20 Mbytes |
| MAX | 120 Gbytes |
| Default value | 100 Mbytes |

<a id="3cb167506b0c612a"></a>
### Description

It sets the size of the logfile used in the database. This parameter is referenced only when creating the database, and the log file size can not be updated thereafter.

<a id="87f158ec6117968a"></a>
## LOG_FLUSHER_HOT_POLICY_INTERVAL

<a id="a3e6a269506117a2"></a>
### Basic Information

<a id="51577b72cf7bac00"></a>
| Item | Description |
| --- | --- |
| Name | LOG_FLUSHER_HOT_POLICY_INTERVAL |
| Summary | log flushing interval for busy waiting(us) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000(1 day) |
| Default value | 0 |

<a id="e60ae3e9f1a1b78a"></a>
### Description

Specifies the time the gmaster log flusher thread performs busy waiting while waiting for an event.  
The unit is microseconds. Increasing this value increases CPU usage but writes logs from the buffer to disk more quickly.  
The default value is 0, which disables busy waiting.

<a id="cf03b0164ddd52ba"></a>
## LOG_GROUP_COUNT

<a id="1bd0974eefe3eebf"></a>
### Basic Information

**Basic Information of LOG_GROUP_COUNT**

<a id="b846d1bac270d322"></a>
| Item | Description |
| --- | --- |
| Name | LOG_GROUP_COUNT |
| Summary | initial count of log group |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 4 |
| MAX | 254 |
| Default value | 4 |

<a id="31651ad7a0318cb1"></a>
### Description

It sets the number of log groups used in the database. This parameter is referenced only when creating the database and does not affect any operations thereafter. Once the database is created, adding or removing a log group is supported through a separate syntax.

<a id="af73b526c2dbf3f1"></a>
## LOG_MIRROR_MODE

<a id="0074338ef4e20d4f"></a>
### Basic Information

**Basic Information of LOG_MIRROR_MODE**

<a id="7f9649a806a2a1eb"></a>
| Item | Description |
| --- | --- |
| Name | LOG_MIRROR_MODE |
| Summary | LogMirror Mode (1:Enable, 0:Disable) |
| Data type | BOOLEAN |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="d3069c26282f8f4d"></a>
### Description

It is the property that configures the required shared memory for operating LogMirror, the redo log replication tool, at database startup.  
It must be enabled to execute LogMirror. The size of the shared memory can be adjusted using LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE.

<a id="0ff309b1804df507"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="af984e1cb141b9e6"></a>
### Basic Information

**Basic Information of LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE**

<a id="c47850b0e49696fa"></a>
| Item | Description |
| --- | --- |
| Name | LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE |
| Summary | shared memory size for LogMirror (byte) |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10485760 (10 M) |
| MAX | 1073741824 (1 G) |
| Default value | 104857600 (100 M) |

<a id="6d7abca415c64cc9"></a>
### Description

It sets the size of the shared memory used by LogMirror, the redo log replication tool.   
This setting is applied when LOG_MIRROR_MODE is enabled.

<a id="7adc6784561f1f99"></a>
## LOG_MIRROR_TIMEOUT

<a id="014aca5be5140116"></a>
### Basic Information

**Basic Information of LOG_MIRROR_TIMEOUT**

<a id="90f58bde5c0565a9"></a>
| Item | Description |
| --- | --- |
| Name | LOG_MIRROR_TIMEOUT |
| Summary | logmirror retry timeout (sec) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="4d39e5eedfa89142"></a>
### Description

It is the response waiting time for LogMirror.   
If its value is set to 0, it waits indefinitely. Otherwise, it waits for the specified duration before a TIMEOUT occurs, which stops the LogMirror service. The server will then operate normally.  
This setting is applied when LOG_MIRROR_MODE is enabled.

<a id="58870ab8da87df4e"></a>
## LOG_SYNC_INTERVAL

<a id="eb90e6f55e493c5d"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="7a6df7e8b81c1660"></a>
| Item | Description |
| --- | --- |
| Name | LOG_SYNC_INTERVAL |
| Summary | interval for synchronize log (s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 10000 |
| Default value | 3 |

<a id="dd38028ae4b4fc9e"></a>
### Description

The log flusher of GOLDILOCKS is a system thread that flushes the contents of the log buffer to the disk logfile. When the log flusher wakes up during the idle phase, it checks for any logs to flush and proceeds to flush them if available.  
If the log flusher has not flushed within the time set in LOG_SYNC_INTERVAL, it synchronizes the log buffer with the log file by performing a flush until the last block of the current log buffer.

<a id="c42283867b123bcd"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="a657034c010f1401"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="bcd9f3cb488bd18c"></a>
| Item | Description |
| --- | --- |
| Name | LOG_SYNC_INTERVAL_MSEC |
| Summary | milli-second interval for synchronize log |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="d39577395fb3c133"></a>
### Description

It is the interval, in milliseconds, for synchronizing the log.

<a id="cf0064462b0d0c55"></a>
## MAX_GROUP_COUNT

<a id="b122d4518621c6ed"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="9f75547cdfe5beae"></a>
| Item | Description |
| --- | --- |
| Name | MAX_GROUP_COUNT |
| Summary | maximum group count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 8192 |
| Default value | 32 |

<a id="c57ad79e86ac8914"></a>
### Description

It is the maximum group count in the cluster system.

<a id="914d4fb82d1e629f"></a>
## MAX_GROUPING_SETS_COUNT

<a id="0fcdec8599a45aab"></a>
### Basic Information

<a id="06bdbab382c36c60"></a>
| Item | Description |
| --- | --- |
| Name | MAX_GROUPING_SETS_COUNT |
| Summary | maximum grouping sets count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | TRUE |
| MIN | 1 |
| MAX | 131072 |
| Default value | 4096 |

<a id="8baa4f57359c286d"></a>
### Description

It is the maximum number of grouping sets that can be defined in a group by clause.

<a id="4253602dfd6b92fe"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="ece312f2a6f78e62"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="70df1af1232f80cf"></a>
| Item | Description |
| --- | --- |
| Name | MAX_JOURNAL_FILE_SIZE |
| Summary | maximum journal file size |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 (1 Terabytes) |
| Default value | 0 (no limit) |

<a id="ffff228647262bbb"></a>
### Description

It sets the maximum size (quota) of the global journaling file, which internally stores journaling data when journaling occurs in the cluster system.

<a id="a239b812d73d78fd"></a>
## MAX_NODE_COUNT

<a id="2609d1f8969dda66"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="38590aefa0e73103"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Summary | maximum node count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 8192 |
| Default value | 64 |

<a id="f9de14fadf1cf697"></a>
### Description

It is the maximum node (instance) count that can join the cluster system.

<a id="5b8124ef92ae7188"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="a5e89fba4f8765d4"></a>
### Basic Information

**Basic Information of MAXIMUM_CONCURRENT_ACTIVITIES**

<a id="ee87a12b1d406584"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_CONCURRENT_ACTIVITIES |
| Summary | maximum number of active statements that the driver can support for a connection |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65535 |
| Default value | 1024 |

<a id="75da2121fdbc4bad"></a>
### Description

It sets the number of statements that can be executed simultaneously.

<a id="d89c50a86c9ce456"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="527f867ac0fb9236"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="62c24b983e4346cf"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_FILE_CACHE_SIZE |
| Summary | the limit of file descriptor cache |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 16 |
| MAX | 32768 |
| Default value | 128 |

<a id="c2ee29fc2cb7b89b"></a>
### Description

It sets the maximum number of file caches being used in the session.

<a id="265de6bb22f1bfaa"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="626dc06e83dfcc14"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="2652b2f9479aeeae"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_FLUSH_BUFFER_PAGE_COUNT |
| Summary | maximum number of buffer page count to be flushing |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| Default value | 64 |

<a id="a69d084c5c53ae10"></a>
### Description

It sets the maximum number of pages that can be recorded per disk writing operation. When pages in the disk tablespace are updated in the buffer, the IO thread records them on the disk. Recording nearby pages together during the disk writing operation increases system resource efficiency by reducing the number of disk write operations.

<a id="cd884be1abc1f336"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="a3b63f8d3a8f44ac"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="5b8f85101a6977c1"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_FLUSH_LOG_BLOCK_COUNT |
| Summary | maximum number of log block count to be flushing |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1000 |
| MAX | 2000000 |
| Default value | 100000 |

<a id="70106d77fb6022fe"></a>
### Description

When flushing the contents of the log buffer to the disk log file, it sets the maximum number of log blocks that can be flushed in a single write operation.

<a id="c88f72ae27022abe"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="50bab1dd6d7b8924"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_PAGE_COUNT**

<a id="8fa6761db0269ced"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_FLUSH_PAGE_COUNT |
| Summary | maximum number of page count to be flushing |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| Default value | 1024 |

<a id="7fe7fbf9ab6c15e4"></a>
### Description

GOLDILOCKS datafiles are flushed to disk by the checkpoint process and certain DDL statements. It sets the maximum number of data pages to be flushed in a single write operation for flushing the data file.

<a id="31c745d9681936f6"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="1ca58b378feb05e6"></a>
### Basic Information

<a id="df4f03d7de1a726e"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT |
| Summary | maximum number of replaying journals for rebuild index |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| Default value | 2 |

<a id="97246ea94a320bd9"></a>
### Description

When rebuilding the index in ONLINE mode, it can be performed concurrently with DML operations, which record updates in the journal log. The index is rebuilt based on the data at the start of the rebuilding process, and the updated data during the rebuild is applied to the index through the journal log. The journal logs are first applied, followed by the logs that were accumulated while applying the journal logs. This property sets the number of times the journal logs are applied in this manner.

<a id="d3f843462cbea1d2"></a>
## MAXIMUM_LOADED_LIBRARY_COUNT

<a id="07fdc805361fa22b"></a>
### Basic Information

<a id="589bb9f45a99d928"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_LOADED_LIBRARY_COUNT |
| Summary | maximum number of loaded library |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 128 |
| Default value | 16 |

<a id="c63ca8106faac626"></a>
### Description

In a database, the maximum number of concurrent shared libraries that can be loaded when executing an external routine is restricted. This property sets an upper limit on the total number of dynamic library handles that the database process can maintain, thereby preventing excessive memory consumption, handle exhaustion, and performance degradation caused by faulty external code or configuration errors.

<a id="41b4095c2a4f2c81"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="61aa00a3e730acd4"></a>
### Basic Information

**Basic Information of MAXIMUM_NAMED_CURSOR_COUNT**

<a id="90ea4db0a39295fe"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_NAMED_CURSOR_COUNT |
| Summary | maximum number of named cursor that the driver can support for a connection |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 100000 |
| Default value | 128 |

<a id="6cde9303fbe8a0d1"></a>
### Description

It is the maximum number of named cursors that can be used within a single session.  
A named cursor is created in the following cases.

- When a named cursor is declared using functions such as SQLSetCursorName(), SQLGetCursorName()

```
{
    ...
    SQLSetCursorName( stmt,
                      "my_cursor",
                      SQL_NTS );
    ...
}
```

- When the DECLARE cursor statement is used in functions such as SQLExecDirect (), SQLPrepare ()

```
{
    ...
    SQLExecDirect( stmt,
                   "DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name",
                   SQL_NTS );
    ...
}
```

- When the DECLARE cursor FOR UPDATE statement is used in embedded SQL

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name FOR UPDATE;
    ...
    EXEC SQL OPEN my_cursor;
    ...
    EXEC SQL FETCH my_cursor INTO :data;
    EXEC SQL DELETE FROM tab_name WHERE CURRENT OF my_cursor;
    ...
    EXEC SQL CLOSE my_cursor;
}
```

> In embedded SQL, the DECLARE CURSOR statement without FOR UPDATE, as follows, does not create a named cursor in the session.

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name;
    ...
}
```

<a id="e9de480622802e4a"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="4d767a7e5e4e5a69"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="7c9e56fe91b951f8"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_PACKAGE_INSTANCE_COUNT |
| Summary | maximum number of package instance that the driver can support for a connection |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 100000 |
| Default value | 128 |

<a id="8bfb61b67002f05c"></a>
### Description

It is the maximum number of package instances available in a single session.   
A package instance is created when using a stateful package within the session.

<a id="8052d471f8a15808"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="65cb32879c25a0a3"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="726d4e29f1710f54"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_SESSION_CM_BUFFER_SIZE |
| Summary | maximum communication bytes per shared mode session |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 1073741824 |
| Default value | 20971520 |

<a id="0ed88d7150e737af"></a>
### Description

It sets the maximum buffer size available in a single session connected in shared mode.  
For more information, refer to [DISPATCHER_CM_BUFFER_SIZE](#0bdea21f3c641073).

<a id="d31f89496c61c8c6"></a>
## MEASURE_CLUSTER_LATENCY

<a id="eb202ce2c1320d46"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="1258b570a91efe77"></a>
| Item | Description |
| --- | --- |
| Name | MEASURE_CLUSTER_LATENCY |
| Summary | measure cluster latency |
| Data type | BOOL |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="1df8db255c12ce76"></a>
### Description

It is the latency of the measure cluster.

<a id="5f580fabe4bc17e5"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="8032e92f838ceccb"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="6dcafe77659e247d"></a>
| Item | Description |
| --- | --- |
| Name | MIN_SAMPLE_ROW_COUNT |
| Summary | minimum sampling row count for analyze table |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 9223372036854775807 (INT64_MAX) |
| Default value | 100000 |

<a id="9e5bcecf4de6b144"></a>
### Description

It is the minimum number of sampling rows when performing [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#1dbf53dac8b0496f) using sampling.

<a id="8799b74cc4cdda2d"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="5496faf219eac3b6"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="145746e77a7c4e01"></a>
| Item | Description |
| --- | --- |
| Name | MINIMUM_UNDO_PAGE_COUNT |
| Summary | minimum undo page count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 16 |
| MAX | 1048576 |
| Default value | 16 |

<a id="6b82b98ba923c024"></a>
### Description

DML uses the undo page to store the previous image. DML uses one undo segment at a time to consume undo pages. If all pages of the allocated undo segment are exhausted, pages from another undo segment can be used. MINIMUM UNDO PAGE_COUNT specifies the minimum number of undo pages required to import pages from an undo segment when there are insufficient undo pages. If the available undo pages are insufficient, pages can only be imported from an undo segment that has more pages than the MINIMUM UNDO PAGE_COUNT.

<a id="c59f5f9ac5b4f16d"></a>
## NET_BUFFER_SIZE

<a id="3ba6d08d80254f28"></a>
### Basic Information

**Basic Information of NET_BUFFER_SIZE**

<a id="d88bf09162dbd201"></a>
| Item | Description |
| --- | --- |
| Name | NET_BUFFER_SIZE |
| Summary | TCP network buffer size (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1024 |
| MAX | 1073741824 |
| Default value | 32768 |

<a id="9f7b19119d46266e"></a>
### Description

It sets the TCP communications buffer size.   
In dedicated mode, it is set to the maximum communication packet size.  
In shared mode, it is set to [DISPATCHER_CM_UNIT_SIZE](#fdf1bd2d5fac934e).

<a id="86120b98fe0558e4"></a>
## NLS_DATE_FORMAT

<a id="87a1ce1517ff0aa3"></a>
### Basic Information

**Basic Information of NLS_DATE_FORMAT**

<a id="af1ea188a78e7c1d"></a>
| Item | Description |
| --- | --- |
| Name | NLS_DATE_FORMAT |
| Summary | nls date format |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | YYYY-MM-DD |

<a id="493b67032dfebd3d"></a>
### Description

NLS_DATE_FORMAT specifies the default date format for the TO_CHAR and TO_DATE functions.

<a id="b303d4bd630c0388"></a>
## NLS_TIME_FORMAT

<a id="ba1965bb38c58d71"></a>
### Basic Information

**Basic Information of NLS_TIME_FORMAT**

<a id="22e573aea9a0cba8"></a>
| Item | Description |
| --- | --- |
| Name | NLS_TIME_FORMAT |
| Summary | nls time format |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | HH24:MI:SS.FF6 |

<a id="e42f1c4741036c74"></a>
### Description

NLS_DATE_FORMAT specifies the default time format for the TO_CHAR and TO_DATE functions.

<a id="81aefd62dd9e1a5a"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="caa5999347122a8d"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="c1acf0e2e0823118"></a>
| Item | Description |
| --- | --- |
| Name | NLS_TIME_WITH_TIME_ZONE_FORMAT |
| Summary | nls time with time zone format |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | HH24:MI:SS.FF6 TZH:TZM |

<a id="2953b0ae805e3f63"></a>
### Description

NLS_TIME_WITH_TIME_ZONE FORMAT specifies the default time with time zone format for the TO_CHAR and TO_TIME_WITH_TIME_ZONE functions.

<a id="5129c923d9116f8d"></a>
## NLS_TIMESTAMP_FORMAT

<a id="ac9e4cd5d1d8420c"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="991ec64041c59848"></a>
| Item | Description |
| --- | --- |
| Name | NLS_TIMESTAMP_FORMAT |
| Summary | nls timestamp format |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | YYYY-MM-DD HH24:MI:SS.FF6 |

<a id="6053f551442b535e"></a>
### Description

NLS_TIMESTAMP_FORMAT specifies the default timestamp format for the TO_CHAR and TO_TIMESTAMP functions.

<a id="8a228be667cdaef8"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="64bf6e6e8718edd2"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="88b7a5ed923907fc"></a>
| Item | Description |
| --- | --- |
| Name | NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT |
| Summary | nls timestamp with time zone format |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM |

<a id="aa09e725f623933e"></a>
### Description

NLS_TIMESTAMP_WITH_TIME_ZONE FORMAT specifies the default timestamp with time zone format for the TO_CHAR and TO_TIMESTAMP WITH TIMEZONE functions.

<a id="ca02e9387a2c237e"></a>
## NUMA

<a id="be18691dd1354fe4"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="11026764d1e55489"></a>
| Item | Description |
| --- | --- |
| Name | NUMA |
| Summary | enable numa |
| Data type | BOOLEAN |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="fb13863d3cfd249a"></a>
### Description

It enables NUMA.

> To use the NUMA property in AIX, the user account must be modified. Execute the following command as the root user.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" &lt;username&gt;  
> `  
>   
> &lt;username&gt; is a user account in AIX and not a root user.   
> To apply the changes, log out and then log back in.

<a id="1839f4a94d18e514"></a>
## NUMA_MAP

<a id="4a9487a9ebdb8fdf"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="d2553669df70941b"></a>
| Item | Description |
| --- | --- |
| Name | NUMA_MAP |
| Summary | numa node map |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | 'x' : no binding |

<a id="ae10fc031515a361"></a>
### Description

It sets the mapping to connect the system's CPU cores to their NUMA nodes. This property is applied when the NUMA property is set to on.

The following is an example of a system with four cores.

- Connect core 0 and core 1 to NUMA node 0, and core 2 and core 3 to NUMA node 1.

```
NUMA_MAP = '0:0:1:1' # core
```

- Connect core 0 and core 1 to NUMA node 0, core 2 and core 3 to NUMA node 1, and core 1 and core 3 to NUMA node 2.

```
NUMA_MAP = '0:0,2:1:1,2' # core
```

<a id="8a7856f6c42511aa"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="b84f8c33f592facf"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="a9a8c68d90dafd78"></a>
| Item | Description |
| --- | --- |
| Name | OFFLINE_MEMBER_AFTER_FAILOVER |
| Summary | Automatically offline member after failover |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="faf7d119d1a55e8f"></a>
### Description

The background process automatically takes the errored member offline after completing the failover caused by the node error.

If it is not possible to take the errored member offline because it is set to *NO*, execute the following syntax before the errored member rejoins the system.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="01c6d9aec58015c6"></a>
## ONLINE_DDL_BLOCK_READ_COUNT

<a id="9afa9c343fe00f68"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="1cd3aa0018ba6ce7"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_DDL_BLOCK_READ_COUNT |
| Summary | block read count for online DDL |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| Default value | 1 |

<a id="a472c0c0e1d8a7b7"></a>
### Description

Specifies the block size during online DDL execution.  
Each block stores as many records as there are properties and is transmitted remotely in block units.

<a id="6d34d4485d097e76"></a>
## ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD

<a id="75b800d022c39db1"></a>
### Basic Information

<a id="b0ed196815e77c20"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD |
| Summary | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 (10G) |
| Default value | 1048576 (1M) |

<a id="68310e6b1325d032"></a>
### Description

In a cluster environment, Online DDL applies the journal logs generated by DML operations during execution in multiple iterations.  
The maximum number of iterations for applying journal logs is determined by ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT.  
However, if the remaining journal logs are not numerous, it does not repeat the maximum number of iterations and immediately acquires an EXCLUSIVE lock on the table to use it as a threshold for applying the final journal logs.

<a id="5d8871acc0f7c38f"></a>
## ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="ca1fc40be86da47e"></a>
### Basic Information

<a id="ba764f7bfaf34d77"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT |
| Summary | maximum number of replaying journals for online DDL |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| Default value | 2 |

<a id="be3e7fc7e78031ab"></a>
### Description

In a cluster environment, Online DDL can be executed concurrently with DML, which records changes in journal logs.   
While running concurrently, Online DDL first applies the journal logs generated during table synchronization and then applies any accumulated logs in subsequent passes.   
This property specifies the maximum number of times journal logs are applied in this process.

<a id="10db0f046d22a3e2"></a>
## ONLINE_DDL_SCAN_PARTITION

<a id="14cc5a4071e9dcc9"></a>
### Basic Information

<a id="66483134f9a3fed3"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_DDL_SCAN_PARTITION |
| Summary | partition factor of shard upon online DDL |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 1000 |
| Default value | 5 |

<a id="ed5e5bd96044cfe8"></a>
### Description

Specifies the number of shards to divide for synchronization during online DDL.  
For more information, refer to [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#f207258645781242).

<a id="07b8383fb0151e9f"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="056ed21dda4910e5"></a>
### Basic Information

<a id="f59ede8e09a88bfd"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD |
| Summary | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 |
| Default value | 1048576 |

<a id="e95b13aa9e995e71"></a>
### Description

DML operations performed during the index rebuilding process in ONLINE mode are recorded in the journal log. The journals are applied to the index multiple times upon completing the rebuild. The parameter [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#31c745d9681936f6) defines how many times the journal logs are applied. However, if the number of journal logs to be applied is small, the process does not repeat the maximum count set; instead, it immediately places an EXCLUSIVE lock on the table and uses this as the threshold to apply the last journal log.

<a id="c6c25b0f764418b0"></a>
## OS_GROUP_ACCESS

<a id="60c6395856328809"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="fa9ec58a82f22be6"></a>
| Item | Description |
| --- | --- |
| Name | OS_GROUP_ACCESS |
| Summary | enable access database with OS group permission |
| Data type | BOOLEAN |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="364a43872f57728f"></a>
### Description

To connect to DA with another user from the same group, this property must be set to *YES*. Additionally, the system's umask must be modified to *0002*.

<a id="65f6eac1a4823cd9"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="62f8aa26c5adbe13"></a>
### Basic Information

<a id="19d5161272e4e6eb"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_COMPRESSION_THRESHOLD |
| Summary | The size limit at which packets are compressed(bytes) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| Default value | 2113929216 |

<a id="4a65157103be8bd0"></a>
### Description

If the data size to be sent to the client exceeds the PACKET_COMPRESSION_THRESHOLD, the communication data will be compressed.

<a id="45271d23b2ad2617"></a>
## PAGE_CHECKSUM_TYPE

<a id="d1b3a2cb1ab81190"></a>
### Basic Information

**Basic Information of PAGE_CHECKSUM_TYPE**

<a id="fd05492c3485f23a"></a>
| Item | Description |
| --- | --- |
| Name | PAGE_CHECKSUM_TYPE |
| Summary | page checksum type (0:LSN, 1:CRC) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="d1756f179875ce18"></a>
### Description

A checksum is used to ensure the physical consistency of each page in the datafile. GOLDILOCKS supports a page checksum based on the LSN and CRC scheme.

- 0: LSN
- 1: CRC

<a id="250c145fdbcbb2a5"></a>
## PARALLEL_IO_FACTOR

<a id="c81af959b42e7a34"></a>
### Basic Information

**Basic Information of PARALLEL_IO_FACTOR**

<a id="6401bb8f6468d538"></a>
| Item | Information |
| --- | --- |
| Name | PARALLEL_IO_FACTOR |
| Summary | parallel load factor |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 16 |
| Default value | 1 |

<a id="4d4e0d8a1c176d31"></a>
### Description

It sets the number of threads for parallel loading of the data file when starting the database, as well as the number of threads for parallel recording of the data file during a checkpoint.

<a id="4b161b7309d52c21"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

> It has not been supported since version 22c.1.

<a id="3ec0dec48730ee9d"></a>
### Basic Information

**Basic Information of PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16**

<a id="6c8a6a9da31aef23"></a>
| Item | Description |
| --- | --- |
| Name | PARALLEL_IO_GROUP_1 |
| Summary | parallel load group 1 |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/db |

<a id="b174718ee0c451e8"></a>
### Description

It sets the group directory for parallel I/O of the data file. The number of groups is determined by the PARALLEL_IO_FACTOR, allowing parallel I/O to be performed on the data file units belonging to each group.

<a id="0b4736e65296d924"></a>
## PARALLEL_LOAD_FACTOR

<a id="997ec0637d8a3440"></a>
### Basic Information

**Basic Information of PARALLEL_LOAD_FACTOR**

<a id="a128d06561023634"></a>
| Item | Description |
| --- | --- |
| Name | PARALLEL_LOAD_FACTOR |
| Summary | parallel load factor |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 64 |
| Default value | 1 |

<a id="783640b224018b86"></a>
### Description

When starting the database, it sets the number of threads for parallel operations after loading the memory of the data file.

<a id="3df40cfc1494f02a"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="3490d113c6491873"></a>
### Basic Information

**Basic Information of PENDING_LOG_BUFFER_COUNT**

<a id="103c09a1a1cd10ca"></a>
| Item | Description |
| --- | --- |
| Name | PENDING_LOG_BUFFER_COUNT |
| Summary | default pending log buffer count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 32 |
| Default value | 4 |

<a id="1a1f3f2f1c0957a0"></a>
### Description

When multiple transactions are running simultaneously, the pending log buffer is used to reduce competition for the log buffer. The PENDING LOG_BUFFER COUNT sets the number of pending log buffers that can be used simultaneously.

<a id="0a0b8d9214422128"></a>
## PLAN_CACHE

<a id="193a522c4f569e90"></a>
### Basic Information

**Basic Information of PLAN_CACHE**

<a id="9b8643d3dcd05b8c"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_CACHE |
| Summary | caching sql plan |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="9d10a6fe57f528a3"></a>
### Description

It determines whether to use the plan cache.

<a id="47de4d307c34ef0c"></a>
## PLAN_CACHE_SIZE

<a id="943c0b09beba39df"></a>
### Basic Information

**Basic Information of PLAN_CACHE_SIZE**

<a id="04bf23f0d1afe521"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_CACHE_SIZE |
| Summary | sql plan cache size (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | TRUE |
| MIN | 20971520 |
| MAX | 1099511627776 |
| Default value | 104857600 |

<a id="a9f04d8f05b7fa05"></a>
### Description

It sets the memory size to be used for the plan cache.

<a id="e0f75fd40ca66877"></a>
## PLAN_HISTORY

<a id="00fcd7945c529558"></a>
### Basic Information

<a id="2c6034ad83458e9b"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_HISTORY |
| Summary | plan history for SQLs |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="393b56ba7233c359"></a>
### Description

It determines whether to use the plan history.

<a id="205d585cde746f08"></a>
## PLAN_HISTORY_SIZE

<a id="cc21a237524a0b45"></a>
### Basic Information

<a id="b5425c28bde0c533"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_HISTORY_SIZE |
| Summary | plan history size |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| Default value | 0 |

<a id="59508c57fb982f28"></a>
### Description

It sets the number of plans to be stored in the plan history.

<a id="d863a253cfe7df0c"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="de01427c9e229c1f"></a>
### Basic Information

<a id="12e2f2e61a5645ac"></a>
| Item | Description |
| --- | --- |
| Name | PRIVATE_STATIC_AREA_INIT_SIZE |
| Summary | Initial size of Private Static Area (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 34359738368 |
| Default value | 10485760 |

<a id="be2a8c5ffc7b04d2"></a>
### Description

It sets the initial size of the heap memory to be used in the session. Even if there is unused memory during the session, that memory is not returned to the operating system.

<a id="b05d0bf74ebb144c"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="1e9dc33ed3b4b9ad"></a>
### Basic Information

<a id="ca8f723e92a05ba1"></a>
| Item | Description |
| --- | --- |
| Name | PRIVATE_STATIC_AREA_NEXT_SIZE |
| Summary | Next size of Private Static Area (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1024 |
| MAX | 34359738368 |
| Default value | 10485760 |

<a id="a33b0cb3ab4625fd"></a>
### Description

It sets the size of memory to be allocated when the session extends the heap memory.

<a id="314dd828a2ae3b49"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="2d20550781e96f2a"></a>
### Basic Information

<a id="35311cd637b51232"></a>
| Item | Description |
| --- | --- |
| Name | PRIVATE_STATIC_AREA_SHRINK_THRESHOLD |
| Summary | Threshold bytes to attempt to shrink private static area(byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 34359738368 |
| Default value | 10485760 |

<a id="64d48bcc118547c8"></a>
### Description

The memory size is maintained at this value even when there are unused heap memories in the session, and those memories are not returned to the system but are instead reused within the session.

Even if it is set smaller than PRIVATE_STATIC_AREA_INIT_SIZE, it will not be reduced below that size.

<a id="099bad76ad55b880"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="4a93d46d98a9e6b9"></a>
### Basic Information

**Basic Information of PRIVATE_STATIC_AREA_SIZE**

<a id="0866c59127cc77d9"></a>
| Item | Description |
| --- | --- |
| Name | PRIVATE_STATIC_AREA_SIZE |
| Summary | Shared Static Area Size (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 104857600 |
| MAX | 34359738368 |
| Default value | 104857600 |

<a id="1cd4587159ca7213"></a>
### Description

It specifies the maximum heap memory size that can be allocated by the session.

<a id="3d154ab8b4775d4e"></a>
## PROCESS_MAX_COUNT

<a id="8d30233db0bc45d2"></a>
### Basic Information

**Basic Information of PROCESS_MAX_COUNT**

<a id="2a07f43afc7f8b3b"></a>
| Item | Description |
| --- | --- |
| Name | PROCESS_MAX_COUNT |
| Summary | Process Max Count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 12 |
| MAX | 65535 |
| Default value | 128 |

<a id="7831bf3385b2bba9"></a>
### Description

It specifies the maximum number of processes (threads) available on the system.

Creating system processes  
• A process is created each time a connection is made in D/A mode or C/S dedicated mode.  
• In C/S shared mode, the processes include the basic balancer, dispatcher and shared-server.   
&nbsp;&nbsp;A process is not created when connecting from a client.

<a id="b4a1fadca6bd70e8"></a>
## QUERY_TIMEOUT

<a id="8da3dd1049bcaf07"></a>
### Basic Information

**Basic Information of QUERY_TIMEOUT**

<a id="9cf5784ff51ae787"></a>
| Item | Description |
| --- | --- |
| Name | QUERY_TIMEOUT |
| Summary | query timeout (s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="f57868b64efe2136"></a>
### Description

It specifies the maximum time that a command received from the session can be executed. If the execution time exceeds this limit, a TIMEOUT error occurs.

- 0: It indicates infinite waiting, meaning that a TIMEOUT error will not occur.

<a id="b84c9115b9d104f1"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="0d80a2ef917efdca"></a>
### Basic Information

**Basic Information of READABLE_ARCHIVELOG_DIR_COUNT**

<a id="95ee793c232a51fe"></a>
| Item | Description |
| --- | --- |
| Name | READABLE_ARCHIVELOG_DIR_COUNT |
| Summary | readable archive log directory count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 10 |
| Default value | 1 |

<a id="5432ea81a35e4dbe"></a>
### Description

It sets the number of directories containing archive redo logs used during media recovery.

<a id="32268374c69192a6"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="e514eb075bbec42f"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="14cfee5caee22aea"></a>
| Item | Description |
| --- | --- |
| Name | READABLE_BACKUP_DIR_COUNT |
| Summary | readable backup directory count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 10 |
| Default value | 1 |

<a id="1337aee235b56dcb"></a>
### Description

It sets the number of directories that contain incremental backups when restoring files using incremental backups.

<a id="28023b937a43e4d2"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> It is no longer supported after version 3.1.

<a id="8ff5d0239248836c"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="4ba0584913965493"></a>
| Item | Description |
| --- | --- |
| Name | RECOMPILE_CHECK_MINIMUM_PAGE_COUNT |
| Summary | minimum page count for recompile check |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 10000 |
| Default value | 64 |

<a id="2f31e856d71b92a5"></a>
### Description

It sets the minimum page count to check whether the plan has been recompiled due to changes in the page count.

<a id="aec6db6c9f5fc8a9"></a>
## RECOMPILE_PAGE_PERCENT

> It is no longer supported after version 3.1.

<a id="01b4cd37a72663f7"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="b339fbf6dd583534"></a>
| Item | Description |
| --- | --- |
| Name | RECOMPILE_PAGE_PERCENT |
| Summary | recompile page percent |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1000 |
| Default value | 30 |

<a id="0c78a071e94afd9e"></a>
### Description

It sets the page percentage for recompiling the plan due to changes in the page count. If the value is 0, recompilation will not occur as a result of the page count modification.

<a id="30f1f6f501016713"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="6145967c85a8820d"></a>
### Basic Information

<a id="21a0eb498116bf53"></a>
| Item | Description |
| --- | --- |
| Name | RECOVERY_LOG_BUFFER_SIZE |
| Summary | default log buffer size for recovery |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 786432 |
| MAX | 32 Mega |
| Default value | 10 Mega |

<a id="d84ddbfda059f109"></a>
### Description

It is the default size of the log buffer for recovery.

<a id="10b2624db09467fe"></a>
## RECOVERY_SLAVES

<a id="5dae396c137926f3"></a>
### Basic Information

<a id="6d24116b5d90e850"></a>
| Item | Description |
| --- | --- |
| Name | RECOVERY_SLAVES |
| Summary | the number of slave threads to participate in instance or crash recovery |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| Default value | 8 |

<a id="f757625a0d443043"></a>
### Description

It sets the number of slave threads for parallel recovery. If this property is set to 0, recovery will be performed using only master threads, without any slave threads.

<a id="2656c2ec034f2f65"></a>
## RECYCLEBIN

<a id="d88de2c6eb98a53d"></a>
### Basic Information

<a id="a4ee1df0adb7afb4"></a>
| Item | Description |
| --- | --- |
| Name | RECYCLEBIN |
| Summary | enable or disable recyclebin feature |
| Data type | BOOLEAN |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="7c34797a4751b377"></a>
### Description

It sets whether to activate the recyclebin feature.

<a id="df1393b865447fdd"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="4d75badb1b8ed5c8"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="48f54535a52b4fcd"></a>
| Item | Description |
| --- | --- |
| Name | REDO_LOG_COMPRESSION_THRESHOLD |
| Summary | The size limit at which redo log are compressed(bytes) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| Default value | 2113929216 |

<a id="70e831f8c5abbda1"></a>
### Description

If the size of the created REDO LOG exceeds the REDO_LOG_COMPRESSION_THRESHOLD value, the REDO LOG will be compressed.

<a id="fc97a492acbd2b65"></a>
## REDO_LOGGING_THROTTLING

<a id="b35a93f55ef5b17b"></a>
### Basic Information

<a id="173be0d859a55474"></a>
| Item | Description |
| --- | --- |
| Name | REDO_LOGGING_THROTTLING |
| Summary | The limit on the number of dirty blocks in the log buffer for large-scale redo logging |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| Default value | 10737418240 |

<a id="896c56ff51c9484b"></a>
### Description

This property is used to prevent system overload caused by a large volume of logs and to minimize the impact on online services.

When logging, if there are more dirty blocks in the log buffer than the value set by the property, the system will wait until the dirty blocks are flushed to the disk.

<a id="61031a199967c435"></a>
### ALIAS

<a id="876c81c6302892f8"></a>
| Item | Description |
| --- | --- |
| Original name | REDO_LOGGING_THROTTLING |
| ALIAS | INDEX_LOGGING_THROTTLING |

<a id="4ef2b0c267f384b2"></a>
## REFINE_RELATION

<a id="d9bcd683f55fb8c4"></a>
### Basic Information

<a id="06eb8ed06a83c346"></a>
| Item | Description |
| --- | --- |
| Name | REFINE_RELATION |
| Summary | refine aged relations |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="563565c9227eafc5"></a>
### Description

If this property is set to NO, the REFINE RELATION process will not be performed when restarting the server.

This property can be used when an error occurs during the REFINE RELATION process. However, segments of RELATIONs (tables or indexes) that were dropped but not REFINEd can not be reused. When resolving the error, setting this property to YES and restarting will attempt to REFINE the relations that were not dropped.

<a id="4d8778eb8a48b2d3"></a>
## RESTORE_BUFFER_SIZE

<a id="087487ffc7330dce"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="e8c19dcbe1aad098"></a>
| Item | Description |
| --- | --- |
| Name | RESTORE_BUFFER_SIZE |
| Summary | buffer size for datafile retsore |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1048576 |
| MAX | 1073741824 |
| Default value | 1048576 |

<a id="993c0e3ccd653db9"></a>
### Description

Sets the buffer size used to read data from disk in a single read operation when performing [ALTER DATABASE RESTORE](../part-03-sql-manual/18-sql-references-a-b.md#22625d6afdeafdcd) on a disk tablespace using a backup. The same setting is applied to the restore process when performing [ALTER DATABASE RECOVER](../part-03-sql-manual/18-sql-references-a-b.md#91d87d0b29aa6323) on a disk tablespace using a backup.

<a id="8764c71c9674031f"></a>
## SESSION_FATAL_BEHAVIOR

<a id="b541ce7a6d8281b8"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="09a0ff25c0010eec"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_FATAL_BEHAVIOR |
| Summary | session fatal behavior |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="fc90c79db39d2da5"></a>
### Description

When a session fatal occurs, this property determines whether to terminate only the thread that caused the fatal or to terminate the entire process.

- 0: It terminates only the thread that caused the fatal.
- 1: It terminates the entire process.  
  If multiple sessions are running simultaneously in the process, the process will be terminated after all sessions finish using the database.

<a id="375cd950ca0420e6"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="a0a398675b55f490"></a>
### Basic Information

<a id="812967340bc3a762"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_MEMORY_INIT_SIZE |
| Summary | initial memory size for dedicated sessions |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 524288 (512K) |

<a id="be31b0c2d1833d85"></a>
### Description

It sets the initial size of the memory to be used in the dedicated session.

<a id="eecf6fc862269081"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="b03c5938c8aad2a9"></a>
### Basic Information

<a id="346040c417b35ff4"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_MEMORY_SHRINK_THRESHOLD |
| Summary | threshold bytes to attempt to shrink session memory allocator ( byte ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 131072 (128K) |

<a id="4d9faad0db27c327"></a>
### Description

It sets a threshold value to determine whether to return unused dynamic shared memory to the system when releasing the dynamic shared memory used in the session. In other words, if there is an unused memory chunk larger than the specified value, it will be returned to the system.

<a id="529dd1901bde6130"></a>
## SESSION_POOL_INIT_SIZE

<a id="deb927fc5574c5ce"></a>
### Basic Information

<a id="cbc5982fd74759b8"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_POOL_INIT_SIZE |
| Summary | initial memory size for session pool |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1099511627776 (1T) |
| Default value | 0 |

<a id="95a123421be17c4e"></a>
### Description

It sets the initial memory size for the session pool.

If each session requires memory, space is allocated from the session pool. If the session pool is insufficient, space is then allocated from SSA.   
The session pool is designed to prevent sessions from frequently accessing SSA. If it is set to "0", the session pool feature is disabled.

<a id="6cff9b08f53ec58d"></a>
## SESSION_POOL_NEXT_SIZE

<a id="ef32384b789af464"></a>
### Basic Information

<a id="84dcbf518623a5b7"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_POOL_NEXT_SIZE |
| Summary | memory size to be expanded in session pool |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 1048576 (1M) |

<a id="6f471ea86604048a"></a>
### Description

It sets the amount by which to increase the memory size in the session pool when expanding the session pool space.  
This setting is valid only when SESSION_POOL_INIT_SIZE is greater than 0.

<a id="0f3215c3a9121108"></a>
## SHARED_MEMORY_ADDRESS

<a id="c77538bb2241af76"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_ADDRESS**

<a id="d20b946610c25667"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_MEMORY_ADDRESS |
| Summary | shared memory address |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | 1610612736 |

<a id="a1ebd3333168303a"></a>
### Description

It specifies the address of the Shared Static Area (SSA).

<a id="3c43113ec551fba8"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="23afa3437140e53b"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_KEY**

<a id="57ccb88bc52ebf21"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_MEMORY_STATIC_KEY |
| Summary | Shared Memory Static KEY |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | 542353 |

<a id="5b73ff16c5405ac5"></a>
### Description

When running the server, it specifies the shared memory key values used to allocate space for the Static Shared Area (SSA).

<a id="ad1981be3ac0fea8"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="e03c6f2f83a31955"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_NAME**

<a id="af12fafbcadff427"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_MEMORY_STATIC_NAME |
| Summary | Shared Memory Static Name |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | _STATIC |

<a id="1ab36bb284e16a8d"></a>
### Description

When running the server, it specifies the shared memory name used to allocate space for the Static Shared Area (SSA).

<a id="6bbbc914a0e83be3"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="2e7f89cbd889436e"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_SIZE**

<a id="3768f1f756fc513e"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_MEMORY_STATIC_SIZE |
| Summary | Shared Memory Static Size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 104857600 |
| MAX | 1099511627776 |
| Default value | 838860800 (800M) |

<a id="6d09b6ea8c76f86d"></a>
### Description

It specifies the size of the Shared Static Area (SSA).

<a id="d792ae80a967ee51"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="66a35787c0671546"></a>
### Basic Information

**Basic Information of SHARED_REQUEST_QUEUE_COUNT**

<a id="a39ee0825138e296"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_REQUEST_QUEUE_COUNT |
| Summary | count of global request queue |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 16 |
| Default value | 1 |

<a id="a0334676d16e74f7"></a>
### Description

In shared mode, it sets the number of queues that the dispatcher requests from the shared server. A queue is used when multiple dispatchers allocate user requests to the shared server, and generally one queue is used for load balancing.   
However, as the number of dispatchers and shared servers increases, conflicts may arise in the queues, leading to performance degradation, so this value is increased. If the value becomes too large, load balancing can become inefficient, and the risk of deadlock increases.

<a id="2e6df03efe2fb4dd"></a>
## SHARED_SERVERS

<a id="133056f8f299c044"></a>
### Basic Information

**Basic Information of SHARED_SERVERS**

<a id="683b332dad6c7e6f"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_SERVERS |
| Summary | number of shared-server processes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 10 |

<a id="00935cbb7822cfb0"></a>
### Description

It sets the number of shared server processes in shared mode.  
During the open phase, the value can not be decreased using the 'ALTER SYSTEM' command.

<a id="22268a69adccc0da"></a>
## SHARED_SESSION

<a id="0331c5c07701a841"></a>
### Basic Information

**Basic Information of SHARED_SESSION**

<a id="e8e7b323f9510ff1"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_SESSION |
| Summary | to enable shared session |
| Data type | BOOL |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="c42203afeb532e05"></a>
### Description

It sets whether to activate shared mode. If the value is set to *NO*, the load balancer (gbalancer), dispatcher (gdispatcher), and shared-server (gserver) will not be executed.

<a id="450e0fbecfe9e8a7"></a>
## SHARED_SESSION_MEMORY_INIT_SIZE

<a id="9c287f72835c6b46"></a>
### Basic Information

<a id="855501f13beda886"></a>
| Item | Description |
| --- | --- |
| Name | SHARED_SESSION_MEMORY_INIT_SIZE |
| Summary | initial memory size for shared sessions |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 786432 (768K) |

<a id="7eb3f557a7a69e8e"></a>
### Description

It sets the initial size of the memory to be used for the shared session.

<a id="ab2613a4a323acf3"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="c763b7e8b64d9032"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="01b4789594fa9f38"></a>
| Item | Description |
| --- | --- |
| Name | SNAPSHOT_STATEMENT_TIMEOUT |
| Summary | snapshot statement timeout (s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 22118400 (1 year) |
| Default value | 22118400 (1 year) |

<a id="70ab9c2a41077a39"></a>
### Description

It sets the maximum holding time for the statement required for the snapshot read. A TIMEOUT error occurs for a snapshot statement that exceeds this time.

<a id="fd420e547296e493"></a>
## SQL_HISTORY_SIZE

<a id="7b8af99feee29257"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="9324024240b3d90b"></a>
| Item | Description |
| --- | --- |
| Name | SQL_HISTORY_SIZE |
| Summary | history size for SQLs |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| Default value | 0 |

<a id="4f7d47e27adb6ffc"></a>
### Description

It is the history size for SQLs.

<a id="dfe480be695eb135"></a>
## SQL_HISTORY_TYPE

<a id="562bfb8c6ecdf413"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="2f631eae3bd606e0"></a>
| Item | Description |
| --- | --- |
| Name | SQL_HISTORY_TYPE |
| Summary | history type for SQLs |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="ab1147f75a5b877e"></a>
### Description

It is the history type for SQLs.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="2f0f6920b29850b0"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="318a91660bf57737"></a>
### Basic Information

**Basic Information of SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY**

<a id="e814676a3c3cddcb"></a>
| Item | Description |
| --- | --- |
| Name | SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY |
| Summary | supplemental log data of primary key columns be logged in redo log files |
| Data type | BOOLEAN |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="e1ceb3823b42b536"></a>
### Description

It records supplemental logs for all changes made to the database.

<a id="21af781f9dbcb62c"></a>
## SYNC_DISPATCHER_CM_BUFFER_COUNT

<a id="e1d1b9eb275d0b7c"></a>
### Basic Information

<a id="5ae088494e823784"></a>
| Item | Description |
| --- | --- |
| Name | SYNC_DISPATCHER_CM_BUFFER_COUNT |
| Summary | communication buffer count for synchronization dispatcher |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 128 |
| Default value | 1 |

<a id="901d36ec44aa1939"></a>
### Description

It specifies the number of communication buffers for the cluster synchronization dispatcher.

<a id="453ee60f2dc79cae"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="a3caa55d49bf49cc"></a>
### Basic Information

<a id="971b7fbd02389902"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_DISK_DATA_TABLESPACE_SIZE |
| Summary | default system disk data tablespace size(byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 200 Mega |

<a id="d9b13d141d89fd28"></a>
### Description

It sets the initial size of the DISK_DATA_TBS tablespace when creating the database.

<a id="10a5d0fcb9592546"></a>
## SYSTEM_FILE_IO

<a id="0056baefeec29bad"></a>
### Basic Information

<a id="18e10add772bad8f"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_FILE_IO |
| Summary | i/o type for system file ( 0: direct io, 1: buffered io ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="39c5f60d45610f69"></a>
### Description

It sets the IO type when using the database file, excluding the data file and the log file.

<a id="c1ed97e04fe039ea"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="4ec8ec3eb067b84e"></a>
### Basic Information

<a id="23bf76e0b8afa506"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_MEMORY_AUX_TABLESPACE_SIZE |
| Summary | default system memory auxiliary tablespace size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 200 Mega |

<a id="49e38b2dfaf2bf1a"></a>
### Description

It determines the initial size of the MEM_AUX_TBS tablespace when creating the database.

<a id="0cade8a151ace5e4"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="03eb9896fd223f06"></a>
### Basic Information

<a id="ed5f1743d6fc339b"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_MEMORY_DATA_TABLESPACE_SIZE |
| Summary | default system memory data tablespace size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 200 Mega |

<a id="bb11c58fe83564f6"></a>
### Description

It determines the initial size of the MEM_DATA_TBS tablespace when creating the database.

<a id="634f51a2f1a79a7b"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="a984fac0f33a247e"></a>
### Basic Information

<a id="662d42e5a826bd92"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_MEMORY_DICT_TABLESPACE_SIZE |
| Summary | default dictionary tablespace size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 256 Mega |
| MAX | 30 Giga |
| Default value | 256 Mega |

<a id="e06978701405e827"></a>
### Description

It determines the initial size of the DICTIONARY_TBS tablespace when creating the database.

<a id="9183fd5a51bbd032"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="2baa071fafaba4e8"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE**

<a id="e94b59482c7b1e44"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE |
| Summary | default system memory temporary tablespace size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 200 Mega |

<a id="d477c05a0d968f36"></a>
### Description

It determines the initial size of the MEM_TEMP_TBS tablespace when creating the database.

<a id="5ad8cad50c3fa915"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="7ca451037db728ea"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE**

<a id="1daa29ba6ad1f43b"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE |
| Summary | default system memory undo tablespace size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 32 Mega |

<a id="f15a60cb80308bd6"></a>
### Description

It determines the initial size of the MEM_UNDO_TBS tablespace when creating the database.

<a id="fc268a520f68aa64"></a>
## SYSTEM_TABLESPACE_DIR

<a id="5732f7a940d1e249"></a>
### Basic Information

<a id="50738c3c98c88715"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_TABLESPACE_DIR |
| Summary | system tablespace directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/db |

<a id="e61197690c838834"></a>
### Description

It sets the path where the initial system tablespaces are stored when creating the database.

<a id="d6329f05f382efa2"></a>
## SYSTEM_UDS_DIR

<a id="2b7686299b033c33"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="4e7abeca564f75e6"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_UDS_DIR |
| Summary | system unix domain socket directory |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | '/tmp' |

<a id="49623e7c65809c78"></a>
### Description

It sets the directory where the unix domain socket file is created.  
The directory setting for the unix domain socket, such as glsnr, other than the DB system, is managed by a separate configuration file.   
The maximum setting size is 60 bytes. (The maximum size of the absolute path for the unix domain socket file, including the directory and file name, varies by OS, but is generally around 100 bytes.)

<a id="e1b88a32fa6550c2"></a>
## TCP_CLIENT_NUMA_NODE

<a id="ac3b94d47a684306"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="c8e079cf791db8f1"></a>
| Item | Description |
| --- | --- |
| Name | TCP_CLIENT_NUMA_NODE |
| Summary | numa node for TCP clients |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | -1 |
| MAX | 63 |
| Default value | -1 |

<a id="327d6bfb8401124c"></a>
### Description

It sets the NUMA node ID to which the client server session is bound. This property operates when the NUMA property is set to on.

<a id="7a0730e8700d5640"></a>
## TCP_NODELAY

<a id="c1161ff3cd77f01b"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="f657874987d47dad"></a>
| Item | Description |
| --- | --- |
| Name | TCP_NODELAY |
| Summary | no delays in buffer flushing within the TCP/IP protocol stack |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="699e4a442221e364"></a>
### Description

It sets the TCP_NODELAY option of the socket when transferring data to a client using the C/S method (TCP socket).  
Set it to *NO* when fast latency is not required and reducing the network load is necessary.

<a id="8f4cc8ddb7e36514"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="677dccc909e0bc9e"></a>
### Basic Information

<a id="f8f4adff5aa30113"></a>
| Item | Description |
| --- | --- |
| Name | TEMP_SEGMENT_CACHE_SIZE |
| Summary | the number of segments to be cached for global temporary tables and indexes in each session |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 4294967295 |
| Default value | 3 |

<a id="e5ab0a09761d8b38"></a>
### Description

It sets the number of segments to be cached in a session instead of returning them to a tablespace when dropping a global temporary table or a global temporary index segment. Segments in the segment cache are reused later in a global temporary table or a global temporary index.

- 0: It does not use a segment cache for a global temporary table or of a global temporary index in a session.
- 1 ~ 4294967295: It retains a specific number of segment caches for a global temporary table or a global temporary index in a session.

<a id="a588c25ed5256ce6"></a>
## TEMP_UNDO_ENABLED

<a id="9421afbf603173a0"></a>
### Basic Information

<a id="458c9fca1fcc7435"></a>
| Item | Description |
| --- | --- |
| Name | TEMP_UNDO_ENABLED |
| Summary | enables writing undo records of global temporary tables to the temp tablespace |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="c3d030ca29424259"></a>
### Description

It specifies the location of logging undo records for a global temporary table.

- 0 (FALSE): It records the undo records in the default undo tablespace of the database. 
- 1 (TRUE): It records the undo records in the default temporary tablespace of the database.

<a id="d93e183e4f0cccee"></a>
## TEMP_UNDO_SHRINK_THRESHOLD

<a id="531463e9d9d174ff"></a>
### Basic Information

<a id="e9915d8345cc6d62"></a>
| Item | Description |
| --- | --- |
| Name | TEMP_UNDO_SHRINK_THRESHOLD |
| Summary | threshold bytes to attempt to shrink temp undo segment ( byte ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 107374182400 |
| Default value | 10485760 |

<a id="b5c54a401ae2331c"></a>
### Description

When a session stores undo records for a global temporary table in the temp tablespace, this property specifies the minimum amount of undo space to retain for the session when reclaiming the undo space used by completed transactions. This reduces the overhead of allocating space required to store undo records.

<a id="35b97f5f1621ae1e"></a>
## TIMED_STATISTICS

<a id="9da70283eda5ffee"></a>
### Basic Information

<a id="ed53b875a9526bea"></a>
| Item | Description |
| --- | --- |
| Name | TIMED_STATISTICS |
| Summary | timed statistics |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="a9f113be991d3faa"></a>
### Description

It indicates whether to check the wait event.  
To record statistics related to wait events in the v$system_event, v$session_event and v$session_wait table, set this property.

- 0: It does not record the statistics.
- 1: It records the statistics.
- 2: It records the statistics using the high-precision timer.

<a id="03661ff1fd2b8a63"></a>
## TIMER_INTERVAL

<a id="0a575bb51b9a5a1a"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="3ea1dafc0a814058"></a>
| Item | Description |
| --- | --- |
| Name | TIMER_INTERVAL |
| Summary | timer interval time(us) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 10 |
| MAX | 100000 |
| Default value | 10000 |

<a id="fc3ecda0f14c596d"></a>
### Description

It sets the time interval required for the timer thread to set the system time.

<a id="f9d2b587e8535ce0"></a>
## TIMEZONE

<a id="d014d8e29bb9ff06"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="0d167fa86cfb8e6c"></a>
| Item | Description |
| --- | --- |
| Name | TIMEZONE |
| Summary | timezone |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | +09:00 |

<a id="f87d9d6d1001edec"></a>
### Description

It is the time zone value of the database.  
It is applied when creating the database and uses a value in the range from '-14:00' to '+14:00'.

<a id="f31e6a0d94ac3a59"></a>
## TRACE_ALTER_SYSTEM

<a id="6a237b29dcb1e081"></a>
### Basic Information

**Basic Information of TRACE_ALTER_SYSTEM**

<a id="181a1d5224122180"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_ALTER_SYSTEM |
| Summary | write trace messages for ALTER SYSTEM |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="2f54b3412b3000e7"></a>
### Description

It records the SQL statements in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) when executing the ALTER SYSTEM syntax.

Set the TRACE_ALTER_SYSTEM property to *ON* to record system changes.

The TRACE_ALTER_SYSTEM property is unrelated to the execution of SELECT queries, INSERT, UPDATE, and DELETE statements, so it does not affect performance.

<a id="72fb748ffdcf9f43"></a>
## TRACE_DDL

<a id="d33b851cc82f8d42"></a>
### Basic Information

**Basic Information of TRACE_DDL**

<a id="ddef60cde98ce555"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_DDL |
| Summary | write trace messages for DDL |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="7dcea3c299c04491"></a>
### Description

When executing DDL statements, it records the executed SQL statements in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

Set the *TRACE_ALTER_SYSTEM* property to *ON* to record the execution of SQL statements such as CREATE/DROP/ALTER table.

The TRACE_DDL property affects only DDL statements. However, it is unrelated to SELECT inquiries, and the execution of INSERT, UPDATE, and DELETE statements. Therefore, it does not affect performance.

<a id="3a2eadb24d0f23d0"></a>
## TRACE_LOG_ID

<a id="ab8354da55296092"></a>
### Basic Information

**Basic Information of TRACE_LOG_ID**

<a id="e8964c78bb2c1e46"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOG_ID |
| Summary | trace log ID |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="38ff9c4262921d03"></a>
### Description

The execution plan for the query and other related information are recorded in the trace file (opt_p[process ID_s [session ID].trc) under the trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) when processing queries.

To record the SQL statement, execution plan, and execution time for the query, configure the flags in the table below.

**Flag information for TRACE_LOG_ID**

<a id="df673da80227954c"></a>
| Information | Flag(on) | Flag(off) |
| --- | --- | --- |
| Output options for PSM (procedure/function) call flow | 1000000 | 0 |
| Output options for successful SQL queries | 100000 | 0 |
| Output options for failed SQL queries | 10000 | 0 |
| Output options for execution plans | 1000 | 0 |
| Output options for execution types (direct/prepare) | 100 | 0 |
| Output options for bind values | 10 | 0 |
| Output options for execution time per section | 1 | 0 |

To set it in the form of "output the successful SQL query" + "output the execution plan" + "output the bind value", set the TRACE_LOG_ID value to 101010.

<a id="5d05dc0d3c817577"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="c738000086b0f8f7"></a>
### Basic Information

<a id="269fe042a68a3875"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOG_MSGBUF_SIZE |
| Summary | memory buffer size for trace log message |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 8192 |
| MAX | 10485760 |
| Default value | 24576 |

<a id="c61b2bfa44db76eb"></a>
### Description

It sets the size of the heap memory buffer used to configure the log message to be recorded in the trace logfile.

<a id="56e018f2fb70f25f"></a>
## TRACE_LOG_TIME_DETAIL

<a id="ee11809d28dda450"></a>
### Basic Information

**Basic Information of TRACE_LOG_TIME_DETAIL**

<a id="217adc13dad1be3b"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOG_TIME_DETAIL |
| Summary | detail trace log time |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="8a81091d3dd3d8a9"></a>
### Description

It sets whether to increase the time accuracy when recording the trace log.  
If the value is ON, it has an accuracy of 1 us.  
If the value is OFF, it has an accuracy of 10 ms.

<a id="c74ee87eab383287"></a>
## TRACE_LOGGER

<a id="e369784d68f726f6"></a>
### Basic Information

<a id="86073b53443c18bc"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER |
| Summary | trace log type ( 1:file, 2:file & remote ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| Default value | 1 |

<a id="613ed9c21f0e381b"></a>
### Description

It sets the target for recording the trace log.  
If it is set to 1, the logs are recorded in a file; if it is set to 2, they are recorded in a file remotely.  
When recorded remotely, the trace logs are collected from gtrclogger and written to a file.

<a id="bf86c59b0cbd7538"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="dc963958f6dfb3d6"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="b2f1785e77d3995f"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER_REMOTE_HOST |
| Summary | remote host for trace logger |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 255255255255 |
| Default value | 127000000001 |

<a id="d091054d2dbcca9c"></a>
### Description

It sets the host to which the trace log is remotely transferred when TRACE_LOGGER is set to 2.

<a id="2f8d760bbda98891"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="d7065ded64169d8c"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="caa3413cffae5646"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER_REMOTE_PORT |
| Summary | remote port for trace logger |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1024 |
| MAX | 49151 |
| Default value | 21470 |

<a id="ad2051fc29e2ba69"></a>
### Description

It sets the port to which the trace log is remotely transferred when TRACE_LOGGER is set to 2.

<a id="4b5eaac350455b21"></a>
## TRACE_LOGIN

<a id="aa5703fab0efb1b6"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="b0d6ec7c20057618"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGIN |
| Summary | write login trace messages for user |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="98369bbfa0c7f977"></a>
### Description

It records the relevant access information in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc) during login.  
Set the TRACE_LOGIN property to *ON* to log the relevant information during login.

<a id="d4aecd208d05c547"></a>
## TRACE_LONG_RUN_CURSOR

<a id="b29c91e3f19a040b"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_CURSOR**

<a id="bd944a1dcf6b342d"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LONG_RUN_CURSOR |
| Summary | write trace SQL for cursor life-time over specific time (mili-sec. 0 ~ 10000000) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="bd3079fe648afe93"></a>
### Description

When the cursor lifetime exceeds the specified property time, the SQL statement of the cursor is recorded in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record any information.
    - Recommended value: 20 milliseconds or more
    - Execution time is measured using a time tick with a 10 ms interval, so a value of 20 or higher is advised.
    - For higher precision, use the [TRACE_LONG_RUN_TIMER](#0e42b3eddb73ba15) property.

- The following is an example of recording the SQL statement for a cursor whose lifetime exceeds 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR = 1000;
```

- The following is an example of restoring the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR TO DEFAULT;
```

It is used to trace the user program that maintains the cursor for an extended period as follows.

```
int main()
{
   ...
   EXEC SQL DECLARE cur1 CURSOR FOR SELECT name FROM t1 WHERE pk = :s_id;
   EXEC SQL OPEN cur1
   EXEC SQL FETCH cur1 INTO :s_name;
   ...
   long_run_user_logic( s_name ); ❶ Due to the user logic, ager fails to clean up resources for a long time.
   ...
   EXEC SQL CLOSE cur1;
   ...
}
```

<a id="c4af8f1256e31a55"></a>
## TRACE_LONG_RUN_SQL

<a id="71e52e912d552f8c"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="f960ae8dd9c5e650"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LONG_RUN_SQL |
| Summary | write trace for long-run SQL over specific execution time (mili-sec. 0 ~ 10000000) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="436c1ba3b53508d5"></a>
### Description

It records the SQL statement whose execution time exceeds the specified property time in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record any information.
    - Recommended value: 20 milliseconds or more
    - Execution time is measured using a time tick with a 10 ms interval, so a value of 20 or higher is advised.
    - For higher precision, use the [TRACE_LONG_RUN_TIMER](#0e42b3eddb73ba15) property.

The following is an example of recording the SQL statement whose execution time exceeds 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

The following is an example of restoring the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="0e42b3eddb73ba15"></a>
## TRACE_LONG_RUN_TIMER

<a id="68eabf405e84cb5d"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="3d7555b179f3610c"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LONG_RUN_TIMER |
| Summary | trace long-run timer resolution ( 0: timer thread(10 ms interval), 1: gettimeofday() ) |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="f52a5ecd08a60f5d"></a>
### Description

It controls the measurement precision for the execution time of the SQL statement using the following properties.

- [TRACE_LONG_RUN_CURSOR](#d4aecd208d05c547)
- [TRACE_LONG_RUN_SQL](#c4af8f1256e31a55)

- Description of value
    - 0: It uses a timer thread with an interval of 10 milliseconds
    - 1: It measures time using the gettimeofday() function. This provides higher precision, but the system call can increase the workload.

<a id="03a6bc4279f688d4"></a>
## TRACE_SYSTEM_DIR

<a id="239b82c15bc48fe6"></a>
### Basic Information

<a id="aaa009dba1cf0171"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_SYSTEM_DIR |
| Summary | system logger directory |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/trc |

<a id="f15e19efbc2c87c1"></a>
### Description

It sets the disk path where the trace log message is recorded.

<a id="8e0c88163611ab3d"></a>
### ALIAS

<a id="39b0e5bd963bb0b4"></a>
| Item | Description |
| --- | --- |
| Original name | TRACE_SYSTEM_DIR |
| ALIAS | SYSTEM_LOGGER_DIR |

<a id="13eb316777fe905d"></a>
## TRACE_XA

<a id="64b83f07a6c64563"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="629dbc823e57c05a"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_XA |
| Summary | logging trace log for xa interfaces |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="0122671bfe1fada0"></a>
### Description

It specifies whether to output trace messages when using the XA interface. The messages are output to 'SYSTEM_LOGGER_DIR / xa.trc'.

<a id="9dfab130bafa0432"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="9483fbc8c59c347e"></a>
### Basic Information

<a id="2ff11956c6717b41"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_ALLOCATION_TIMEOUT |
| Summary | a time limit (sec) for allocating transaction slot |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 3 |

<a id="563aede66f36f344"></a>
### Description

It is the maximum waiting time when allocating a transaction slot.

An error occurs as follows if the waiting time exceeds TRANSACTION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="c24d41a3cab48979"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="1eecaa7d9fe9e192"></a>
### Basic Information

**Basic Information of TRANSACTION_COMMIT_WRITE_MODE**

<a id="b7f263e770165d87"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_COMMIT_WRITE_MODE |
| Summary | transaction commit write mode (0: no_wait, 1: wait) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="0d38af81a77622d1"></a>
### Description

TRANSACTION_COMMIT_WRITE_MODE specifies whether the log generated by the transaction is flushed to the disk log file when the transaction is committed. If TRANSACTION_COMMIT_WRITE_MODE is '1', the log will be flushed to the disk log file at the time of the transaction commit. Otherwise, the transaction is committed regardless of whether the log is flushed.

If the system operates with TRANSACTION_COMMIT_WRITE_MODE set to '0', the latest data will be lost if GOLDILOCKS is abnormally terminated without flushing the log after a COMMIT transaction. This occurs because the logs are not recorded in this case.

Therefore, if all transactions must remain in the database upon completion, the system must be operated with TRANSACTION_COMMIT_WRITE_MODE set to '1', or the 'ALTER SYSTEM FLUSH LOGS' statement must be explicitly executed at the time of transaction completion to flush the logs if TRANSACTION_COMMIT_WRITE_MODE is set to '0'.

- 0: no wait
- 1: wait

<a id="aa925eab1a72b511"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="6be4a9bbe7456a2f"></a>
### Basic Information

**Basic Information of TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT**

<a id="719a7edf6ba246e8"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT |
| Summary | The maximum number of undo pages that a transaction can write. |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 13107200 |
| Default value | 13107200 |

<a id="8345c1f1f935fbcd"></a>
### Description

It refers to the maximum number of undo pages that a transaction can record. The minimum value is 1, which is 8 Kbytes, and the maximum value is 13,107,200 which is 100 Gbytes.

<a id="c44799be03ce68e7"></a>
## TRANSACTION_TABLE_SIZE

<a id="6e337598da0fd9a3"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="eb580b28288c66fd"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_TABLE_SIZE |
| Summary | transaction table size |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 64 |
| MAX | 10240 |
| Default value | 1024 |

<a id="2214938847747113"></a>
### Description

It sets the maximum number of transaction tables that can be executed in the database. To change the number of transaction tables, the database must be restarted, and the new value can always be modified as long as it is greater than the previously set value. However, if it is changed to a smaller value, the restart will fail if it is less than or equal to the maximum value of the transaction slot identifier used by the transactions prepared after the restart recovery.

For example, if the value set to 1,024 is changed to 512, and the maximum value of the transaction slot identifier used by the transactions prepared during the restart is also 512, then the restart will fail as follows. In this case, if it is set to a value greater than 512, the restart will succeed.

```
gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 512 SCOPE = FILE;

System altered.

gSQL> \CONNECT sys gliese as sysdba
gSQL> \SHUTDOWN

Shutdown success
```

- The restart fails.

```
gSQL> \STARTUP

ERR-HY000(14118): TRANSACTION_TABLE_SIZE property value must be equal to or greater than '513'

gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 513 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

<a id="2d91aff00446dda3"></a>
## TRANSACTION_TIMEOUT

<a id="9e3af1b18f830b30"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="1d56a8032394bae9"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_TIMEOUT |
| Summary | transaction timeout (s) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| Default value | 0 |

<a id="2b095573d0c17c8e"></a>
### Description

It sets the duration for which a transaction remains active. This is used to prevent potential side effects when a transaction is active for an extended period. If a transaction exceeds the specified time, the gmaster daemon automatically terminates the session owned by that transaction.

<a id="2cdc1a019f1093c3"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="22a17789ebcdcec8"></a>
### Basic Information

<a id="4aa60bf6791822e7"></a>
| Item | Description |
| --- | --- |
| Name | UNDO_RELATION_ALLOCATION_TIMEOUT |
| Summary | a time limit (sec) for allocating undo relation |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 3 |

<a id="ef938efb69bad2d6"></a>
### Description

It is the maximum waiting time for allocating undo relations.

The following error occurs if the waiting time exceeds UNDO_RELATION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="1fec08573d402977"></a>
## UNDO_RELATION_COUNT

<a id="537690b87cea46bb"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="969674e3f77b74d0"></a>
| Item | Description |
| --- | --- |
| Name | UNDO_RELATION_COUNT |
| Summary | undo relation count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8 |
| MAX | 10240 |
| Default value | 128 |

<a id="b6543bfbbd90e7d2"></a>
### Description

It sets the number of undo relations to be used in the database. An undo relation is allocated so that transactions executing DML operations can use the undo segment. To modify the number of undo relations, the database must be restarted, and the new number can only be increased beyond the previously specified value.

If it is modified to a smaller number, the restart will fail. For example, if the value set to 128 is changed to 64, the restart will fail. In this case, if it is modified to 128 or a larger value, the restart will succeed.

```
gSQL> ALTER SYSTEM SET UNDO_RELATION_COUNT = 64 SCOPE = FILE;

System altered.

gSQL> \CONNECT sys gliese as sysdba
gSQL> \SHUTDOWN

Shutdown success
```

- The restart fails.

```
gSQL> \STARTUP

ERR-HY000(14119): UNDO_RELATION_COUNT property value must be equal to or greater than '128'

gSQL> ALTER SYSTEM SET UNDO_RELATION_COUNT = 128 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

<a id="2b09b14b986a7170"></a>
## UNDO_SHRINK_THRESHOLD

<a id="c68ff051908fb403"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="7e4d657c2934a5ef"></a>
| Item | Description |
| --- | --- |
| Name | UNDO_SHRINK_THRESHOLD |
| Summary | threshold bytes to attempt to shrink undo segment (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 107374182400 |
| Default value | 10485760 |

<a id="b3add51c6c70d739"></a>
### Description

The ager thread periodically checks the undo segment space every 10 seconds. If the space occupied exceeds this property value, the reusable space is returned to the tablespace. The attempt to return space continues until the undo segment space meets this property value (in bytes), and the process finishes when the remaining amount of undo pages is less than MINIMUM_UNDO_PAGE_COUNT.

<a id="52c22536963804dd"></a>
## USE_LARGE_PAGES

<a id="ea543aac6f12a458"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="5c313b68e27a1cea"></a>
| Item | Description |
| --- | --- |
| Name | USE_LARGE_PAGES |
| Summary | use large pages |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| Default value | 0 |

<a id="816b3bad62257ca5"></a>
### Description

It uses HugePage. To use the USE_LARGE_PAGES property, HugePages must be configured on the device first.

- 0: It does not use large pages.
- 1: It uses large pages. An error occurs if allocation of shared memory fails.
- 2: It attempts to allocate shared memory using large pages. If the allocation of shared memory fails, it allocates memory using regular pages.

> It can be used with Linux kernel version 2.6.32-573 or higher.

<a id="8f200024b7809225"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="a98d868d192ef6c8"></a>
### Basic Information

<a id="d974cf45a45379c7"></a>
| Item | Description |
| --- | --- |
| Name | USER_DATA_TABLESPACE_MEDIA_TYPE |
| Summary | default media type of user data tablespace |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 ( Memory ) |
| MAX | 1 ( Disk ) |
| Default value | 0 ( Memory ) |

<a id="7aa4c4baf7dd84ed"></a>
### Description

It sets the default media type for the tablespace if the media type is omitted when creating the user data tablespace. A value of 0 represents memory, while a value of 1 represents disk.

<a id="0ce283b7449766fb"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="dfe5c130fc4f9f31"></a>
### Basic Information

<a id="ec5e7992415a0523"></a>
| Item | Description |
| --- | --- |
| Name | USER_DATA_TABLESPACE_SIZE |
| Summary | default user data tablespace size(byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 32 Mega |

<a id="e158e2f1361cc3d8"></a>
### Description

It sets the default size for the data file if the size is omitted when creating the user data tablespace or adding a data file.

<a id="579125e9a2314dd9"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="60ac8df4bfa37c79"></a>
### Basic Information

<a id="1d0194fdf4f7caec"></a>
| Item | Description |
| --- | --- |
| Name | USER_DISK_DATA_TABLESPACE_NEXTSIZE |
| Summary | default next size of user data tablespace |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 3554432 Byte |
| MAX | 30 Giga |
| Default value | 10 Mega |

<a id="422eebcd98630f60"></a>
### Description

It sets the default size for extension if the size to be extended is not specified when the data file of the user disk data tablespace needs to be extended.

<a id="8c4ac75fabb894fd"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="631fed1d51f1622a"></a>
### Basic Information

<a id="5adaaa887fb51add"></a>
| Item | Description |
| --- | --- |
| Name | USER_TEMP_TABLESPACE_SIZE |
| Summary | default user temp tablespace size(byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| Default value | 32 Mega |

<a id="681bea6a38f36940"></a>
### Description

It sets the default size for the data file if the size is omitted when creating the user temp tablespace or adding a data file.

<a id="c0d517ef1161f407"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="adde908a3e344242"></a>
### Basic Information

<a id="83d1c362a4e40a86"></a>
| Item | Description |
| --- | --- |
| Name | XA_TRANSACTION_IDLE_TIMEOUT |
| Summary | idle timeout for xa transaction |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 ( no limit ) |
| MAX | 10000000 |
| Default value | 60 |

<a id="6a1b11010054bc88"></a>
### Description

It specifies the maximum waiting time for an xa transaction in an idle state (the duration between the beginning of the XA transaction and the next transaction). If it remains idle beyond this time, the xa transaction is rolled back.

If set to 0, the XA transaction will wait indefinitely, even while idle.

---

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
