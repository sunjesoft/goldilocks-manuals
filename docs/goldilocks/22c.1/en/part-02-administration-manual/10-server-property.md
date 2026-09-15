<a id="97198d2eb5a65df9"></a>

# 10. Server Property

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/97198d2eb5a65df9)  
> Tag: `22c.1_10_tag`

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="afa9044136ce038e"></a>
## Server Property Information

For more information about SQL syntax to change properties, refer to the followings.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#77b4edc18193b02e)
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#92680bbe05326073)

For more information about property types, refer to the followings.

- [V$PROPERTY](9-database-information.md#293ee5f5b7377b02): It displays the property list which can be altered while the system is operating or is restarting.
- [V$SPROPERTY](9-database-information.md#4227ee95f859e378): It is either the property which was set by reading the binary file, or the property list which is stored in the binary file.
- [V$DB_PROPERTY](9-database-information.md#65585230f1401eab): It is a read-only property list which can be altered only when creating the database, and it can not be altered afterwards.

The followings describe basic information items of property in this manual.

**Basic Information item of property**

<a id="cf5a2e3625692428"></a>
| Item | Description |
| --- | --- |
| Name | Property name |
| Summary | Short description of the property |
| Data type | Data type of the property value |
| Applicable phase | A startup phase which can be updated with ALTER SYSTEM or ALTER SESSION * NONE: Applicable phase does not exist. (If it can be updated, but applicable phase is NONE, then use *SCOPE = FILE* option.) |
| Updatable | Whether property is updatable or not * If the property value is TRUE, it is updatable.  * If the property value is FALSE, only the read-only is possible. |
| ALTER SESSION | Whether property is updatable or not by using [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#92680bbe05326073) |
| ALTER SYSTEM | Whether property is updatable or not by using [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#77b4edc18193b02e) * IMMEDIATE: The updated value is immediately reflected in all session after execution. * DEFERRED: The updated value is reflected only in the session which is connected after execution. However, it is not reflected in already connected session. * FALSE: The updated value is not reflected in the session during execution. However, the updated value is reflected after restart, (Properties are updatable by using only *SCOPE=FILE* option.) * NONE: It is not updatable. |
| MIN | If the data type is BIGINT, it is the minimum value of property. If the data type is VARCHAR, the minimum value of property is N/A. |
| MAX | If the data type is BIGINT, it is the maximum value of property. If the data type is VARCHAR, the maximum value of property is N/A. |
| Default value | Default value of the property |

<a id="90cbaed2dce93765"></a>
## Property Alias Information

The information about the property alias is viewed through [V$PROPERTY_ALIAS](9-database-information.md#6b38901dc4eaec7c).

The basic information about the property alias written in this manual is as follows.

<a id="48b9d576e6db883e"></a>
| Item | Description |
| --- | --- |
| Original name | It is the original name of the property. |
| ALIAS | It is the name of the property alias. |

For more information about property alias list, refer to [Property Alias](../part-01-getting-started/4-what-s-new.md#f33d406ddc1f95de).

<a id="4070bb58d378f591"></a>
### CDISPATCHER_THREADS

It is an alias of [CDISPATCHER_LOCKABLE_THREADS](#aee1529550e48527).

<a id="65579661f320d9ec"></a>
### CLUSTER_COMMIT_SLAVES

It is an alias of [CLUSTER_COMMIT_SLAVE_CSERVERS](#ddf6c0921da01928).

<a id="eb843d4d3ac8c3ca"></a>
### CLUSTER_SERVER_RESPONSE_ QUEUE_SIZE

It is an alias of [CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE](#6bc22a83cdc66634).

<a id="e01a3a0f5d2fb440"></a>
### CSERVER

It is an alias of [CLUSTER_LOCKABLE_CSERVERS](#5239cac3f236b022).

<a id="c2bb60feeb9f1de4"></a>
### INCREMENTAL_CHECKPOINT_CRITERIA

It is an alias of [BUFFER_DIRTY_PAGE_LIMIT](#9a788e0a29630941).

<a id="e08ea044b274b008"></a>
### LOCKLESS_CSERVERS

It is an alias of [CLUSTER_LOCKLESS_CSERVERS](#6e5ee0fd1db4efa5).

<a id="8966dc66de4586d6"></a>
### MEMORY_MERGE_RUN_COUNT

It is an alias of [INDEX_MERGE_RUN_COUNT](#cefcf6aa4b9eb526).

<a id="db4c6696c135d97e"></a>
### MEMORY_SORT_RUN_SIZE

It is an alias of [INDEX_SORT_RUN_SIZE](#d5606acf31baae4c).

<a id="e2b97f314241ca8f"></a>
### SYSTEM_LOGGER_DIR

It is an alias of [TRACE_SYSTEM_DIR](#4564418725d2984b).

<a id="8e687895744d1fcb"></a>
## ADMIN_SESSION_POOL_INIT_SIZE

<a id="4341e4b48da6d2bb"></a>
### Basic Information

<a id="2713205502e8f642"></a>
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

<a id="9290c172c2ed51f2"></a>
### Description

It sets the initial memory size of the admin session pool.

<a id="16c0f2d716d38eeb"></a>
## ADMIN_SESSION_POOL_NEXT_SIZE

<a id="79ab7d53700d6fc5"></a>
### Basic Information

<a id="9811244a4c5af919"></a>
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

<a id="f8e3be0520fa8303"></a>
### Description

It sets how much to extend the memory size in the session pool when expanding the admin session pool space.   
It is valid only when ADMIN_SESSION_POOL_INIT_SIZE is bigger than 0.

<a id="88075c11b57a9d46"></a>
## AGING_INTERVAL

<a id="0c101ca8a83f1def"></a>
### Basic Information

**Basic Information of AGING_INTERVAL**

<a id="dc787eeba0680081"></a>
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

<a id="46b9064095b9a749"></a>
### Description

It sets the idle time (second) when an ager thread which deletes the previous version data does not have a job to process in MVCC based database.

<a id="786d86620f9494fa"></a>
## AGING_PLAN_INTERVAL

<a id="f9d26196e929844b"></a>
### Basic Information

**Basic Information of AGING_PLAN_INTERVAL**

<a id="e0d68cd697e37a6a"></a>
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
| Default value | 0 |

<a id="edb26d1bb221d1e8"></a>
### Description

The SQL plan which is older than AGING_PLAN_INTERVAL becomes the aging target.

<a id="ad0c76f562466fd6"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="c715c8aeac3eeda5"></a>
### Basic Information

**Basic Information of ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10**

<a id="918fbf39a3d2c71f"></a>
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

<a id="a200c2ddb0ddb636"></a>
### Description

It specifies archiving directory of GOLDILOCKS database's online redo log file. Also, it specifies where to read of archive redo log file at media recovery. The online redo log file creates archive redo log file only in ARCHIVELOG_DIR_1.

ARCHIVELOG_DIR_1 sets only the system, but ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10 sets the session.

<a id="07e80a8f2ab805cc"></a>
## ARCHIVELOG_FILE

<a id="63721bee2682e204"></a>
### Basic Information

**Basic Information of ARCHIVELOG_FILE**

<a id="1417d8c7902000a1"></a>
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

<a id="511b526e1aef347b"></a>
### Description

It sets the prefix of the targeted file name stored in the archive directory when archiving the online redo logfile. The archive logfile's name consists of the prefix defined in ARCHIVELOG_FILE, followed by '_', the file sequence and the file extension 'log'. For example, the online logfile with a sequence number of 0 is archived as 'archive_0.log'.

<a id="75ad49149838f7b2"></a>
## ARCHIVELOG_MODE

<a id="781e56127dbf9fd4"></a>
### Basic Information

**Basic Information of ARCHIVELOG_MODE**

<a id="61460b7bc14bc269"></a>
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

<a id="33b8da5b96a8798c"></a>
### Description

The property is applied at database creation. The archivelog mode can be set to one of the following value.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

It does not affect archive log mode during operation after database is created. The archive log mode can be modified by using *ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}* in MOUNT phase.

<a id="64c840b9d89b6b2b"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="cec93d79b887611d"></a>
### Basic Information

**Basic Information of BACKUP_DIR_1 ~ BACKUP_DIR_10**

<a id="975017740feb556d"></a>
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

<a id="a1dff51812f55556"></a>
### Description

A backup file is created when incremental backup is executed. Then it sets a directory of backup file to be read when restoring files using incremental backup. Incremental backups are created only in the directory set in BACKUP_DIR_1.

BACKUP_DIR_1 sets only the system, but BACKUP_DIR_2 ~ BACKUP_DIR_10 sets the session.

<a id="474dae54c8c36c5d"></a>
## BLOCK_READ_COUNT

<a id="9a166db8b4c42d6f"></a>
### Basic Information

**Basic Information of BLOCK_READ_COUNT**

<a id="5b62ba102100598b"></a>
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

<a id="406a95be4095ab0e"></a>
### Description

The SQL executes operation by reading row in the unit of BLOCK_READ_COUNT which is a row bundle. BLOCK_READ_COUNT  means the number of rows to be processed at a time when operation is executed. It is a basic unit of  pipe-lining process of execution nodes which are used in SQL query processing.

If BLOCK_READ_COUNT value is big the processing performance improves, but many memory resources are used.    
The value between 10 and 100 is recommended.  
If the value becomes bigger than 100 the resource usage increases  proportionately, but the performance improvement does not increase proportionately.

<a id="c3841ab7cfb9e1db"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="e197c39e7ed5f5de"></a>
### Basic Information

<a id="485e747fef2b361e"></a>
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

<a id="03b9ef86577b89ce"></a>
### Description

It sets whether to simultaneously rebuild the indexes on multiple members when rebuilding the index in cluster environment.

<a id="baaf86b40d52dd54"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="ac62bb5b72b1d8ec"></a>
### Basic Information

<a id="b1175d22402db8c1"></a>
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

<a id="2ea9834793810338"></a>
### Description

It sets whether to simultaneously process protocol which can be processed on multiple members at the same time when performing table rebalancing in a cluster environment.

<a id="c97c648cbb2c2128"></a>
## BUFFER_CACHE_SIZE

<a id="0548e75369a21509"></a>
### Basic Information

<a id="cf61f10f6b33051f"></a>
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

<a id="315eddca78acb915"></a>
### Description

It sets the size of the buffer which cashes the page in the disk tablespace.

<a id="dc95545c760ec1ba"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="6114d484d7426dee"></a>
### Basic Information

<a id="05f280367847556c"></a>
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

<a id="73cad9576d2ac03d"></a>
### Description

It is linked to the checklist when pages of disk tablespace cached to the buffer are updated. Each checkpoint list flushes updated pages linked to the checkpoint list by its own flush thread to the disk, and BUFFER_CHECKPOINT_LIST_COUNT sets the number of checkpoint lists and the number of flush threads.

<a id="9a788e0a29630941"></a>
## BUFFER_DIRTY_PAGE_LIMIT

<a id="e1c9681033cabb83"></a>
### Basic Information

<a id="f50f5649faf3288c"></a>
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

<a id="2c39a1296adedd6f"></a>
### Description

Pages updated in the system buffer cache is applied to the disk at checkpoint, and if the buffer cache size is big and updated pages are a lot, then the checkpoint takes a long time and it affects the service. GOLDILOCKS performs the incremental checkpoint which applies updated pages to the disk when the number of updated pages are over a specified number in the system. And BUFFER_DIRTY_PAGE_LIMIT sets the criteria to perform the incremental checkpoint.

For example, when this value is set to 1000, if the updated pages are less than 1000 in the system, then the updated pages are not applied to the disk. However, if the updated pages are 1000 or above, then the updated pages in the buffer are applied to the disk.

The default value is 0, and it means infinity. In this case, it does not perform the incremental checkpoint even when all cached pages in the buffer are updated.

Set the appropriate value for BUFFER_DIRTY_PAGE_LIMIT and [INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA](#e72b9e2dffe55883) considering the restart recovery time and its effect on the service.

<a id="cf4a031d067ca1ee"></a>
### ALIAS

<a id="6c9c6d18a1abf80f"></a>
| Item | Description |
| --- | --- |
| Original name | BUFFER_DIRTY_PAGE_LIMIT |
| ALIAS | INCREMENTAL_CHECKPOINT_CRITERIA |

<a id="cf0e82eb2ccfeaf6"></a>
## BUFFER_FLUSH_THREADS

<a id="89625ad0c795b818"></a>
### Basic Information

<a id="a933c613983143f1"></a>
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

<a id="ee253d89ee35c5ad"></a>
### Description

It is linked to the flush list then requests flush to the buffer flusher, to reuse bch which cached the updated pages in the buffer lru list. In this case, BUFFER_FLUSH_THREADS sets the number of buffer flushers and flush lists to be used in the database.

<a id="f12a6450c13276f5"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="082651b57133bb34"></a>
### Basic Information

<a id="ef6a529a95ed1b2f"></a>
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

<a id="adfb97cec1a2210c"></a>
### Description

It sets the idle time (sec) when the job to be processed by the buffer flusher flushing updated disk tablespace pages to the disk does not exist.

<a id="82ffdc4f419d4df9"></a>
## BUFFER_FREE_LIST_COUNT

<a id="50e762372147f47a"></a>
### Basic Information

<a id="1f5b100372509d16"></a>
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

<a id="26a438e9da1b8522"></a>
### Description

It sets the number of buffer free lists connecting bch which are instantly available to use in the buffer cache.

<a id="b84e54b880a140ba"></a>
## BUFFER_HASH_BUCKETS

<a id="e565fea33fa445b1"></a>
### Basic Information

<a id="eb809f91eb3f6ece"></a>
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

<a id="fac20ce7f4ce3e0c"></a>
### Description

It sets the number of hash buckets for the disk tablespace pages cached in the buffer. It can be set from 0 to 1073741824, and 0 is set by calculating hash buckets as many as pages which can be cached to the buffer which is set according to BUFFER_CACHE_SIZE. If the buffer size is smaller than the specified value, then it adjusts the number of hash buckets to the buffer size.

<a id="d03fab1db489fc91"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="4329e99c8598110d"></a>
### Basic Information

<a id="8cb0800d396da6d1"></a>
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

<a id="aabaedd6f4ca1ad8"></a>
### Description

It sets touch count to transfer pages existing in the cold region to the hot region in buffer lru list.

<a id="c5076d8636e86238"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="92019198fcdeed99"></a>
### Basic Information

<a id="b969175821e82c83"></a>
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
| Default value | 20 |

<a id="ab307b1d524f5c2c"></a>
### Description

It sets the proportion (percentage) of hot region pages to the entire page in the buffer lru list.

<a id="f189abb44940cc9c"></a>
## BUFFER_LRU_LIST_COUNT

<a id="effeaff93a18e7df"></a>
### Basic Information

<a id="76edb85f92c41a53"></a>
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

<a id="b08cf28e99d08459"></a>
### Description

It sets the number of lru lists to select a victim among pages in use by caching when the free buffer for caching disk tablespace pages does not exist.

<a id="443c94cf1c0004d3"></a>
## BUFFER_LRU_SCAN_PERCENT

<a id="173600e68596a9ce"></a>
### Basic Information

<a id="95e35575672902ef"></a>
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

<a id="07cc57c16305eab1"></a>
### Description

If the free buffer available right now does not exist in the system, then it searches for the reusable buffer from the lru list to cache the disk tablespace page to the buffer. BUFFER_LRU_SCAN_PERCENT sets the percent of the buffer pages set in [BUFFER_CACHE_SIZE](#c97c648cbb2c2128), so that it can determine the number of pages to check to find the reusable buffer from lru list.

<a id="c55b513f2f322a38"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="5b37be0af2104a81"></a>
### Basic Information

<a id="f1f0a76cd5d54510"></a>
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

<a id="36afdc940e949862"></a>
### Description

It sets the maximum number of pages to be used for one time disk IO when full scanning the disk table.

<a id="ad18de329fefc552"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="61051aa0c85bb5a7"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="478dfa52dfe60f96"></a>
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
| Default value | 32 |

<a id="864fc8b42c08a96c"></a>
### Description

It sets the maximum number of pages nearby to be prefetched per a disk I/O when accessing to the page in the disk tablespace which does not exist in the buffer.

<a id="8a0b43aa46a6742f"></a>
## BULK_IO_PAGE_COUNT

<a id="4f6df46afa3e4b8c"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="b1fff10e0472a3dd"></a>
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

<a id="0b316f5cb1ab95e3"></a>
### Description

It is used when IO READ of the data file occurs during server restart, or when IO WRITE occurs during creating a data file.

The heap memory is allocated as big as BULK_IO_PAGE_COUNT * 8192 when server restarts or data file is created. If the session's PRIVATE_STATIC_AREA_SIZE is smaller than the heap memory size, an error of insufficient memory may occur. In this case, extend PRIVATE_STATIC_AREA_SIZE.

<a id="5282ad462b347e69"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="8db7e075f4bf3d24"></a>
### Basic Information

**Basic Information of CDISPATCHER_HOT_POLICY_INTERVAL**

<a id="f5b77d926cdce169"></a>
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

<a id="9a1dd3d9c4f3e1e3"></a>
### Description

It is the time of the busy waiting when performing the dequeue in the cdispatcher. It is a micro second unit. If this value is big, it uses more cpu but the user response time (latency) is decreased.  
The default value is 0, and the busy waiting is not allowed.

<a id="aee1529550e48527"></a>
## CDISPATCHER_LOCKABLE_THREADS

<a id="284c612ffee12dc8"></a>
### Basic Information

<a id="e2cd15638a576165"></a>
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

<a id="9dc9f0475e12e1fe"></a>
### Description

It sets the number of cdispatcher threads of lockble data sender and receiver. However, the number of cdispatcher threads of lockless data sender and receiver is set by using [CDISPATCHER_LOCKLESS_THREADS](#e140957910caf698).

<a id="66abbf5619a34764"></a>
### ALIAS

<a id="6e652e51ce8740f8"></a>
| Item | Description |
| --- | --- |
| Original name | CDISPATCHER_LOCKABLE_THREADS |
| ALIAS | CDISPATCHER_THREADS |

<a id="e140957910caf698"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="6b9e0d1ceb5696e3"></a>
### Basic Information

<a id="b73d16cb34013cbc"></a>
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

<a id="397b6b668e77ab63"></a>
### Description

It sets the number of cdispatcher threads of lockless data sender and receiver. However, the number of cdispatcher threads of lockable data sender and receiver is set by using [CDISPATCHER_LOCKABLE_THREADS](#aee1529550e48527).

<a id="5e07c8c236d41074"></a>
## CDISPATCHER_MAX_PACKET_BUFFER_SIZE

<a id="44ddc369ffab3f3b"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="3778dc7c1d43e4c6"></a>
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

<a id="9282e8a974f41948"></a>
### Description

It sets the maximum size of the buffer where the data sender and receiver of cdispatcher stores the sent/ received packets.

<a id="996efa02d96ae57f"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="304f2017925ecf6c"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="5d3d34c019b353ac"></a>
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

<a id="0c3f322b8a58a649"></a>
### Description

It is the socket buffer(sender, receiver) size of cdispatcher.

<a id="9e007210b08a9ea0"></a>
## CDISPATCHER_SYNC_THREADS

<a id="666869fb896870b1"></a>
### Basic Information

**Basic Information of CDISPATCHER_SYNC_THREADS**

<a id="1ab2d45d02b8fe87"></a>
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

<a id="d6deb8baee85b9e9"></a>
### Description

It is the thread count of cdispatcher sync.

<a id="c7654522b894624c"></a>
## CHANGE_TRACKING

<a id="97e11a3249397ae5"></a>
### Basic Information

<a id="dae30581ab769d1a"></a>
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

<a id="cf93d99ed30df7d9"></a>
### Description

It sets whether to track the updated pages to perform the incremental backup of disk tablespace.

- NO: disable change tracking
- YES: enable change tracking

*change tracking* can be enabled by using ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING on mount or above phase only when the database is operated in archivelog.

<a id="b9f3dd8d63b97b97"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="d46007e24096f449"></a>
### Basic Information

<a id="fb3a94c7277d7ced"></a>
| Item | Description |
| --- | --- |
| Name | CHANGE_TRACKING_EXTENT_SIZE |
| Summary | number of pages to track changed of incremental backup |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 16 |
| MAX | 128 |
| Default value | 32 |

<a id="f63f5a87cbf72b34"></a>
### Description

It sets the number of pages to display with one dirty flag when change tracking. For example, if it is set to 32, then one dirty flag is used per 32 pages, and if it is set to 128, then then one dirty flag is used per 128 pages.

<a id="47aa752da6ac4a5d"></a>
## CHANGE_TRACKING_FILE

<a id="f2aa36921eef7351"></a>
### Basic Information

<a id="8185675f3cd64ae5"></a>
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

<a id="3cd91c0346a7374e"></a>
### Description

It sets the file directory which stores the change tracking, and the file name.

<a id="24f01f5e333485e5"></a>
## CHAR_LENGTH_UNITS

<a id="9532373190fc9f84"></a>
### Basic Information

**Basic Information of CHAR_LENGTH_UNITS**

<a id="b927776fed1e2409"></a>
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

<a id="d530f5f2941de17a"></a>
### Description

It is the value of char length units used when defining character string such as CHAR, VARCHAR and omitting char length unit as follows.

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
- addr VARCHAR( 128 ) means that this value is referenced when char length unit is omitted.

When database is created, the property is set to either OCTETS or CHARACTERS. OCTETS is the number of bytes, and CHARACTERS is the number of characters.

> The SQL standard defines CHARACTERS as default value. Other DBMS defines the default value of char length unit as follows. 
> 
> - Oracle and DB2 define OCTETS as default value. 
> - MS-SQL, MySQL, PostgreSQL define CHARACTERS as default value.
> 

<a id="43f975ccd5788104"></a>
## CHARACTER_SET

<a id="fb56a059478c6a27"></a>
### Basic Information

**Basic Information of CHARACTER_SET**

<a id="33019c383b97f844"></a>
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

<a id="071cf60a7e964dbc"></a>
### Description

It is a character set of database, and it is applied when database is created.  
The property is set to one of the following values.

**Character set**

<a id="f4f25afb4b06689e"></a>
| Character set | Description |
| --- | --- |
| SQL_ASCII | ASCII standards |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standards |

<a id="0bfc3c6783aac66e"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="adbd27c06047192b"></a>
### Basic Information

**Basic Information of CHECK_DEDICATE_CONNECTION_INTERVAL**

<a id="5857c7af391a8f3a"></a>
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

<a id="ffea312ee6bef833"></a>
### Description

It is the interval of checking for when the client forcibly cut the connection in C/S dedicate environment. The dedicate server(gserver) checks the socket, and it terminates it if it was cut. The default value is 1,000 millisecond (1 second).

<a id="2ca326a3b252d9c0"></a>
## CHECKPOINT_LIST_COUNT_PER_IO_GROUP

<a id="521e0d82b3d4fb35"></a>
### Basic Information

<a id="9f4c1177bf123d7c"></a>
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

<a id="386712b51561a410"></a>
### Description

It sets the number of checkpoint lists to be processed by each IO slave set by [PARALLEL_IO_FACTOR](#23143ed50dbdc842). It specifies the appropriate value to efficiently process the concurrency when connecting the updated pages to the checkpoint lists. The default value is 0, and in this case, each IO slave creates the checkpoint lists as many as the number of CPU and processes it.

<a id="4d24d02b453a7390"></a>
## CLIENT_MAX_COUNT

<a id="66dcd4b3734ae370"></a>
### Basic Information

**Basic Information of CLIENT_MAX_COUNT**

<a id="e4661efd5e752223"></a>
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

<a id="09866303516f50e1"></a>
### Description

It sets the maximum number of sessions to connect.

<a id="1da616638584c4ce"></a>
## CLIENT_NUMA_POLICY

<a id="6c001dd87d245ef1"></a>
### Basic Information

**Basic Information of CLIENT_NUMA_POLICY**

<a id="090e8a3111bcc34a"></a>
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

<a id="a9f08ca15983e3dd"></a>
### Description

It determines the policy to distribute client processes to NUMA nodes. This property is operated when NUMA property is set to on.

- 0: It determines the NUMA node to be connected by modularizing the session ID.
- 1: It connects to the NUMA node of which is the least connected based on the statistics information.
- 2: C/S client is determined by TCP_CLIENT_NUMA_NODE property, D/A client is determined by DA_CLIENT_ NUMA_NODE property.

<a id="aefbf8c6856e4415"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="41c96e26fa38af50"></a>
### Basic Information

**Basic Information of CLOSE_PSM_CHILD_STMTS**

<a id="4903fa3d7eee5e34"></a>
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

<a id="b8a99e054514e72b"></a>
### Description

It closes the child statement of PSM at the end of each execution.

<a id="09dc196f6427c16f"></a>
## CLUSTER_ASYNC_COMMIT

<a id="aadc430bba4e8e69"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="9e2e05f0dce90c18"></a>
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

<a id="881364e441a1a1e8"></a>
### Description

It determines whether to internally process the commit protocol on an async mode in cluster system.

> If this property is set to on, it asynchronously commits each node, so the temporary inconsistency among nodes may occur. On the other hand, if it is set to off, it synchronizes everytime it commits, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="1ac85d074a7014d7"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="5e1fc701d4c6db30"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_SIZE**

<a id="5225d7f73cebcc2a"></a>
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

<a id="5f10668b972fe636"></a>
### Description

It is the communication buffer size for cluster.

<a id="11c1d302d14ebba1"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="92de2c5a2876b45b"></a>
### Basic Information

**Basic Information of CLUSTER_CM_READ_BUFFER_SIZE**

<a id="9b6c74c48725b6cc"></a>
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

<a id="2f43282ab213c07a"></a>
### Description

It is the communication read block size.

<a id="ddf6c0921da01928"></a>
## CLUSTER_COMMIT_SLAVE_CSERVERS

<a id="e5041d341ee7177b"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_SLAVES**

<a id="fad348877d757398"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_COMMIT_SLAVE_CSERVERS |
| Summary | number of commit slave cservers |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 8 |
| Default value | 0 |

<a id="002adf4261cf50aa"></a>
### Description

It is the number of commit slaves.

<a id="3ddc82b3d6457317"></a>
### ALIAS

<a id="cbd992d97ed22dad"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_COMMIT_SLAVE_CSERVERS |
| ALIAS | CLUSTER_COMMIT_SLAVES |

<a id="0948488c41214a75"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="bc3c85438d61f7c8"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_STREAM_ISOLATION**

<a id="2d09bf2750feef34"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_COMMIT_STREAM_ISOLATION |
| Summary | isolate cluster dispatcher stream for commit protocol |
| Data type | BOOLEAN |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 0 |

<a id="d125f71673864633"></a>
### Description

It determines whether to internally perform the commit process flow in the cluster system separately from other protocol process. The performance may be improved when seperating the commit process according to the system environment.

<a id="25a1f04b7d30b891"></a>
## CLUSTER_CONNECTION

<a id="929a1e52338c7da8"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION**

<a id="a172ae28d6042768"></a>
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

<a id="429478428ea32ae6"></a>
### Description

It is the connection mode for cluster. ( socket:0, rdma:1 )

<a id="bb3f6a7d23ac9191"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="1433b4b75919cbf5"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION_TIMEOUT_SEC**

<a id="8623a3abaadc6c92"></a>
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

<a id="2a08da32e1c36735"></a>
### Description

It is the connection timeout for cluster.

<a id="8ff2020dc5643957"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="26b61ac551f53332"></a>
### Basic Information

**Basic Information of CLUSTER_DATA_SYNC_SERVERS**

<a id="6667edb448706b69"></a>
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

<a id="5f5db72f892068a2"></a>
### Description

It is the count of data synchronization server.

<a id="c46dac65dd8cdf5e"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="67cd1729f4e76050"></a>
### Basic Information

<a id="d8d6d3198c534289"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_DEADLOCK_TIMEOUT |
| Summary | a time limit (sec) for resolving cluster deadlock |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 3600 (1 hour) |
| Default value | 3600 (1 hour) |

<a id="a54f436888818ff1"></a>
### Description

If the competition to occupy the cluster server becomes keen due to the lack of the lockable cluster server, then the cluster deadlock may occur. When cluster deadlock occurs, it waits for the deadlock to be resolved as long as the time set in this property. However, if it is not resolved, then CLUSTER_DEADLOCK_TIMEOUT error occurs.

<a id="6b1019cd3cd4a0e4"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="941f39fffddb2057"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_IN_QUEUE_SIZE**

<a id="8e39346a0b6bdb46"></a>
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

<a id="5c9e5d7592ef2a4f"></a>
### Description

It is the in-queue size for cluster dispatcher.

<a id="7342f7990b6544a8"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="92e6ebf2b6965372"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_NUMA_STREAM_MAP**

<a id="909e69a809d65cf2"></a>
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

<a id="ff74526d0da75075"></a>
### Description

It determines a NUMA node to which the cluster dispatcher is to be connected. This property is operated when NUMA property is set to on.

> If CLUSTER_COMMIT_STREAM_ISOLATION property is set to on, then the 0 stream is set to NUMA node of a commit stream.

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="737b77607d1498b8"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="bfad161dd73b2ec3"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_OUT_QUEUE_SIZE**

<a id="c07e7f7a3b5bcd47"></a>
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

<a id="a207e2e21556cc0f"></a>
### Description

It is the out-queue size for cluster dispatcher.

<a id="6bc22a83cdc66634"></a>
## CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE

<a id="ee33edb158f2aa3d"></a>
### Basic Information

<a id="3cb1528be20a8957"></a>
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

<a id="efe12db09559e197"></a>
### Description

It sets the maximum queue size to receive the response from the remote server.

<a id="0dfcb2672f1f18e6"></a>
### ALIAS

<a id="23f10a8aab3d9e65"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| ALIAS | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |

<a id="019e4be5ee4521be"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="5a6f04caed9cb0a1"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_INTERVAL**

<a id="66d6f22fbf9dea56"></a>
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

<a id="54c763b04c8c3f51"></a>
### Description

It is the interval seconds for health checking of cluster. 0 means that it is disabled.

<a id="a0bbef81a70acb38"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="c874757de9c595f6"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_RETRY_COUNT**

<a id="d8a60423220a50d3"></a>
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

<a id="d0fa2004cc12a705"></a>
### Description

It is the retry count for health checking of cluster.

<a id="5f600c181247fdb2"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="d25c77827908f13c"></a>
### Basic Information

**Basic Information of CLUSTER_IGNORE_INACTIVE_MEMBER**

<a id="8c9abefdb20fc96c"></a>
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

<a id="f30e4bdfb686b9cb"></a>
### Description

It ignores in-active member for cluster.

<a id="33509b8b48716ae1"></a>
## CLUSTER_KEEPALIVE_IDLE_TIME

<a id="ed641d8e6294f555"></a>
### Basic Information

<a id="57baf25460c025ab"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_KEEPALIVE_IDLE_TIME |
| Summary | The number of seconds a cluster connection needs to be idle |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 16383 |
| Default value | 0 |

<a id="98e694eaf9368986"></a>
### Description

It is the idle time which is the duration without sending or receiving TCP packets between a cluster session and a cdispatcher before sending a keep alive packet. In other words, if TCP packets are not exchanged during the seconds set in CLUSTER_KEEPALIVE_IDLE_TIME, then the keep alive mechanism is performed on cdispatcher side to detect the dead connection.

The default value is 0, in which case the keep alive feature is disabled.

<a id="5239cac3f236b022"></a>
## CLUSTER_LOCKABLE_CSERVERS

<a id="b99243e6cf4b1db2"></a>
### Basic Information

<a id="5ebcb6d9ea010c90"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_LOCKABLE_CSERVERS |
| Summary | number of lockable cserver processes |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 5 |

<a id="0bdb70a757eb0342"></a>
### Description

It sets the number of cluster server processes performing the operation which acquires lock. However, the number of cluster server processes performing the operation which does not acquire lock is set by using [CLUSTER_LOCKLESS_CSERVERS](#6e5ee0fd1db4efa5).

<a id="52d7b1eda1ad1327"></a>
### ALIAS

<a id="a61ce83ac38cad45"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_LOCKABLE_CSERVERS |
| ALIAS | CSERVERS |

<a id="6e5ee0fd1db4efa5"></a>
## CLUSTER_LOCKLESS_CSERVERS

<a id="520d0e14baf91547"></a>
### Basic Information

<a id="7a6b92c545d59b92"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_LOCKLESS_CSERVERS |
| Summary | number of lockless cserver processes |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 5 |

<a id="ea85f3af2817407d"></a>
### Description

It sets the number of cluster server processes performing the operation which does not acquire lock. However, the number of cluster server processes performing the operation which acquires lock is set by using [CLUSTER_LOCKABLE_CSERVERS](#5239cac3f236b022).

<a id="822205884af1199d"></a>
### ALIAS

<a id="d9a5df8e97acf70f"></a>
| Item | Description |
| --- | --- |
| Original name | CLUSTER_LOCKLESS_CSERVERS |
| ALIAS | LOCKLESS_CSERVERS |

<a id="e5c212b24319d7d7"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="059f54c1f8e94235"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PACKET_SIZE**

<a id="ec23c5ac28ea6566"></a>
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

<a id="7f461913c1a4697f"></a>
### Description

It sets the maximum packet size of which the remote protocol can transfer at a time. If the column size to be remotely transferred exceeds the property size, then the property size should be set bigger than the column size.

<a id="4954b1192352f3e0"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="ebed0d47035cc46e"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PAYLOAD_SIZE**

<a id="ca44cf724bc0c85c"></a>
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

<a id="ef3fed9362969e12"></a>
### Description

The cluster packet which is remotely transferred may be delivered in pieces, and this property sets the maximum size of data to be stored in a piece.

<a id="b7850079c3e82c50"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="be2da9dbb7b8f5f8"></a>
### Basic Information

**Basic Information of CLUSTER_PACKET_ALLOCATION_TIMEOUT**

<a id="6e62d1802e7b2801"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PACKET_ALLOCATION_TIMEOUT |
| Summary | a time limit (sec) for how long statemets will wait to allocate packet memory |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| Default value | 3 |

<a id="97adb395b4cac3c8"></a>
### Description

It sets the maximum time (second) of waiting when allocating memory required for cluster packet configuration.

<a id="5d5c3aca5b6056ae"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="6a9592183af0e17f"></a>
### Basic Information

<a id="6864d7997171ca37"></a>
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

<a id="f42a0b5d661c8eab"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property to use the failover policy. However, specify the time limit by using [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#aeefe0068656cdb6) property to use the policy terminating the session.

<a id="aeefe0068656cdb6"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="6c8c1af1459b8824"></a>
### Basic Information

<a id="4275e173e8767fd1"></a>
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

<a id="d5c56ff10ddd5a44"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property to use the policy terminating the session. However, specify the time limit by using [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#5d5c3aca5b6056ae) property to use the failover policy.

<a id="4270fb9514494c79"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="94a290d78829d8d3"></a>
### Basic Information

<a id="d7a61ba727a001a6"></a>
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

<a id="6b1905710fc1e001"></a>
### Description

It sets the number of hash buckets to control the cluster session.

<a id="be19510d2caed4c1"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="f793c94bef3565b7"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY**

<a id="4c726755c8f5b70a"></a>
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

<a id="3fd77d06c0ba4fd1"></a>
### Description

It sets the policy to resolve split-brain situation in the cluster system. If the value is set to 1 or over, it enquires the solution of a locator.

> If the query for a locator is timed out, it tries to enquire as many times as CLUSTER_SPLIT_BRAIN_RETRY_COUNT. If the property value after the retry failure is 1, then it forcibly proceeds the failover. If it is 2, then it terminates the fatal.

<a id="047d8ef8e5e13bea"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="ac72301e66ac83c2"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RETRY_COUNT**

<a id="67a54027bda78ebe"></a>
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

<a id="1aa4ffa50db5e42c"></a>
### Description

It is used when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or over in cluster system. It sets the times of retrying to enquire when the query to a locator does not respond.

<a id="7b290ecae83a21ea"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="1c10b370c8e07b5e"></a>
### Basic Information

**Basic Information of COMMITTER_HOT_POLICY_INTERVAL**

<a id="514c2e599ba79b5a"></a>
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

<a id="850a3243581d8427"></a>
### Description

It sets the timezone interval of busy waiting when the commit cserver is dequeing to read the commit protocol message. If it is set to 1,000,000 (1 second), and the time is not passed over 1 second from the last deque success to another deque retry, then it sets the timeout in deque to 0 and performs the busy waiting.

<a id="b32f6d37393fb331"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="48fc08e69fa5ab4e"></a>
### Basic Information

**Basic Information of CONTROL_FILE_0 ~ CONTROL_FILE_7**

<a id="f725baf8fda08846"></a>
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

<a id="563246c8488c9d0b"></a>
### Description

If a control file is corrupted, database can not be used. Therefore, the control file is multiplexed for stability of database. It specifies the directory and file name of which stores each control file.

<a id="62ae272bd11352c7"></a>
## CONTROL_FILE_COUNT

<a id="74d044f6fc49827a"></a>
### Basic Information

**Basic informatin of CONTROL_FILE_COUNT**

<a id="e2966070f0925d4f"></a>
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

<a id="92e848c3cd80588c"></a>
### Description

If a control file is corruped, database can not be used. The control file is multiplexed for stability of database. CONTROL_FILE_COUNT specifies the multiplexing number of control files. A control file is multiplexed at least 2 up to 8.

<a id="4a2041a7ae9de4c3"></a>
## CONTROL_FILE_TEMP_NAME

<a id="49ffe26c580e8425"></a>
### Basic Information

**Basic Information of CONTROL_FILE_TEMP_NAME**

<a id="ee6abf8b68deba6f"></a>
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

<a id="42fd8138d55e5600"></a>
### Description

During database operation, a control file is frequently changed, and its temporary copy can be made if necessary. CONTROL_FILE_TEMP_NAME specifies the directory and its file name to temporarily store the control file.

<a id="9aa3449ef55f50df"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="da9b4ff8d5e26df8"></a>
### Basic Information

**Basic Information of COORDINATOR_COMMIT_WRITE_MODE**

<a id="eb13b3d55e201f54"></a>
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

<a id="97989c14eb812634"></a>
### Description

It is a commit write mode applied to a coordinator. If TRANSACTION_COMMIT_WRITE_MODE is *no wait*, and its property is *wait*, then the coordinator node is operated as *wait*, and other nodes are operated as *no wait*.

<a id="af9504b618dc3c27"></a>
## DA_CLIENT_NUMA_NODE

<a id="dddafeaf6a4f798d"></a>
### Basic Information

**Basic Information of DA_CLIENT_NUMA_NODE**

<a id="86afb75233098f1c"></a>
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

<a id="948e8447c5cbff9b"></a>
### Description

It sets the NUMA node ID to which the direct access (D/A) session is to be bound. This property is operated when NUMA property is set to ON.

<a id="80bd309c239e2f19"></a>
## DATA_STORE_MODE

<a id="2ddc01a16b1248d4"></a>
### Basic Information

**Basic Information of DATA_STORE_MODE**

<a id="cba6a54ce5c580de"></a>
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

<a id="8195b27bf0efc24c"></a>
### Description

It sets the storing method of database.

- 1: CDS mode supports the concurrency for multiple users but it does not guarantee the durability. It does not record logs for all update operations such as insert/ delete/ update data, consequentially a failure can not be recovered.
- 2: TDS mode guarantees the concurrency for multiple users and the durability using logs.

<a id="01c1a1a23d4bf747"></a>
## DATABASE_INSTANCE_NAME

<a id="f89b1bdea32d2077"></a>
### Basic Information

**Basic Information of DATABASE_INSTANCE_NAME**

<a id="adfa7b38060a1e86"></a>
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

<a id="68c954d1fb066f83"></a>
### Description

It is the database instance name.

<a id="57d2ab2db75d5733"></a>
## DDL_AUTOCOMMIT

<a id="74f220e75802aafe"></a>
### Basic Information

**Basic Information of DDL_AUTOCOMMIT**

<a id="970a7d4acb25a792"></a>
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

<a id="69b1d998ea4a549a"></a>
### Description

It sets whether to autocommit DDL operations which are not autocommitted yet. For example, autocommit is not applied to the operations such as creating/altering a table, so if DDL_AUTOCOMMIT is 0, a table creation and alteration can be undone by the rollback. On the other hand, if DDL_AUTOCOMMIT is 1, DDL to which autocommit is not applied is committed immediately.

<a id="4740b5c57d0addc2"></a>
## DDL_LOCK_TIMEOUT

<a id="0fd0732ee3061dfc"></a>
### Basic Information

**Basic Information of DDL_LOCK_TIMEOUT**

<a id="6fd8ce1514e8b392"></a>
| Item | Description |
| --- | --- |
| Name | DDL_LOCK_TIMEOUT |
| Summary | a time limit (sec) for how long DDL statemets will wait |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="20cb0058177cd086"></a>
### Description

It means the lock wait time when DDL operations occur to the same object at the same time.  
The default value is 0 second, and it does not wait for a lock when the DDL operation occurs.

When operations of altering a table structure simultaneously occur, they wait for the time specified in DDL_LOCK_TIMEOUT, without waiting for other transactions termination as follows.

• Transaction A

```
ALTER TABLE t1 ADD COLUMN ( new_column NUMBER );
```

• Transaction B

```
TRUNCATE TABLE t1;
```

If the waiting time exceeds DDL_LOCK_TIMEOUT, an error occurs as follows.

```
gSQL> TRUNCATE TABLE t1;

ERR-HYT00(14026): resource busy or timeout expired
```

<a id="7726599df17a6c02"></a>
## DEADLOCK_PRIORITY

<a id="7a2b8574b2910c7a"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="e5d70d3fc2b44a75"></a>
| Item | Description |
| --- | --- |
| Name | DEADLOCK_PRIORITY |
| Summary | importance to choose deadlock victim |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 9 |
| Default value | 5 |

<a id="fbf410d659ac2e31"></a>
### Description

When a deadlock occurs while simultaneously processing multiple transactions, a specific transaction with the low weight is selected as a victim among transactions which caused the deadlock, to solve the problem. If a deadlock occurs between a transaction started in sessions which have higher value for this property and a transaction started in sessions which have lower value for this property, then latter is selected as a deadlock victim. Therefore, set this property according to the priority of each transaction.

Start the transaction after setting this property value so that this value is applied as a weight of that transaction. The transaction weight is not altered if this value is changed after the transaction already has been started.

<a id="e5a7a42edbaa6a76"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="24b32fc4839e3caa"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="3b8ffaa218037259"></a>
| Item | Description |
| --- | --- |
| Name | DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION |
| Summary | specifies whether or not create global secondary index at table creation |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="7528b3acbaee9bdc"></a>
### Description

It sets whether to create the global secondary index when creating a table in cluster system. A non-deterministic query for the table which did not created the global secondary index fails. The global secondary index can be separately created after creating the table when the property is set to NO.

<a id="340653cbe10f6a55"></a>
## DEFAULT_INDEX_LOGGING

> It is not supported after 3.2.

<a id="f24aa88cf452dc2c"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_LOGGING**

<a id="391fd766ff6aa4a8"></a>
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

<a id="412c63632dc8b3f8"></a>
### Description

If LOGGING property is not explicitly set by a user when an index is created, then it is set to DEFAULT_INDEX_LOGGING value. If an index is created in LOGGING tablespace, the LOGGING property should be set.

<a id="0e06170371295455"></a>
## DEFAULT_INDEX_PCTFREE

<a id="632845f318ec0a05"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_PCTFREE**

<a id="b59e4e42ef0eb50f"></a>
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

<a id="d3d16dae495e6c59"></a>
### Description

If a user does not explicitly specify PCTFREE syntax when creating an index. The PCTFREE is set to DEFAULT_INDEX_PCTFREE property value.

<a id="ed3be66674aa3949"></a>
## DEFAULT_INITRANS

<a id="bc358283958175c5"></a>
### Basic Information

**Basic Information of DEFAULT_INITRANS**

<a id="7d3f441b743b7005"></a>
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

<a id="c46154cd66f1392e"></a>
### Description

If a user does not explicitly set INITRANS syntax when creating a table or an index, then it is set to DEFAULT_INITRANS property value.

<a id="df5a4014da046301"></a>
## DEFAULT_MAXTRANS

<a id="9a490ac73a38cd9a"></a>
### Basic Information

**Basic Information of DEFAULT_MAXTRANS**

<a id="6b995ba5f0506e8c"></a>
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

<a id="8f30cbf0f7c93a23"></a>
### Description

If a user does not explicitly set the MAXTRANS syntax when creating a table or an index, then it is set to DEFAULT_MAXTRANS property value.

<a id="8c0a928324f4e04d"></a>
## DEFAULT_PCTFREE

<a id="1ffa9b12fefac703"></a>
### Basic Information

**Basic Information of DEFAULT_PCTFREE**

<a id="fd431f5dc93ac953"></a>
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

<a id="ab3b132d6589373c"></a>
### Description

If a user does not explicitly set the PCTFREE property when creating a table, it is set to DEFAULT_PCTFREE property value.

<a id="de8a640186294298"></a>
## DEFAULT_PCTUSED

<a id="c9461aa98e599f9b"></a>
### Basic Information

**Basic Information of DEFAULT_PCTUSED**

<a id="5765f5031383cb32"></a>
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

<a id="093edcef6b2b683e"></a>
### Description

If a user does not explicitly set the PCTUSED property when creating a table, it is set to DEFAULT_PCTUSED value.

<a id="8f0b6b578c950a6e"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="165c568f2ffa8101"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_BACKUP_FILE**

<a id="aa4bf450c6976012"></a>
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

<a id="cd95fcc5c48ac848"></a>
### Description

It specifies whether to delete the backup file when deleting the backup list.

<a id="1780746df454ac0e"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="3cb3a1c904dc5cb2"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST**

<a id="dc0d8aaaee85d463"></a>
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

<a id="a8797c956b709fe1"></a>
### Description

It specifies whether to delete the previous obsoleted backup list when executing INCREMENTAL BACKUP.

<a id="02a4c03462986f52"></a>
## DEFAULT_SHARDING

<a id="741928e6e453e41a"></a>
### Basic Information

**Basic Information of DEFAULT_SHARDING**

<a id="b7657aa6d8b736b5"></a>
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

<a id="daab6122d1c22be4"></a>
### Description

It sets the default sharding strategy to be used if the sharding strategy is not determined when creating a table.

The following is an example of executing CREATE TABLE statement.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

If DEFAULT_SHARDING value is 0 (cloned), the table is created as a cloned table as follows.

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

If DEFAULT_SHARDING value is 1 (hash sharding), the table is created as a hash-sharded table as follows.

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

If DEFAULT_SHARDING is 1 (hash sharding) and &lt;table sharding strategy&gt; is not described, then the hash sharding key is determined based on the following order.

1. If PRIMARY KEY constraint is defined, primary key is used as a sharding key.

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

2. If UNIQUE constraint is defined, the firstly described UNIQUE constraint is used as the sharding key.

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

3. If key constraint is not defined, the first column except for the following excluded data type is used as a sharding key.
** The excluded data type: LONG VARCHAR, LONG VARBINARY, BOOLEAN

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

<a id="b0aa5d8fa3e4e5b8"></a>
## DISABLE_DDL

<a id="4af8ae6bfc57bcb9"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="97a1d822c04be7dc"></a>
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

<a id="2a53b814c6ed8718"></a>
### Description

It prevents all DDL execution.

The SQL statements which are affected by DISABLE_DDL are queried as follows.

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
ALTER CLUSTER GROUP .. OFFLINE CLUSTER MEMBER            
ALTER DATABASE ADD LOGFILE GROUP                         
ALTER DATABASE ADD LOGFILE MEMBER                        
ALTER DATABASE ARCHIVELOG                                
ALTER DATABASE CLEAR PASSWORD HISTORY                    
ALTER DATABASE DATAFILE AUTOEXTEND ..                    
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS             
ALTER DATABASE DROP LOGFILE GROUP                        
ALTER DATABASE DROP LOGFILE MEMBER                       
ALTER DATABASE NOARCHIVELOG                              
ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS          
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE         
ALTER DATABASE RENAME LOGFILE                            
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                
ALTER FUNCTION                                           
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
ALTER TABLE .. MERGE SHARDS .. INTO ..                   
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..         
ALTER TABLE .. READ ONLY                                 
ALTER TABLE .. READ WRITE                                
ALTER TABLE .. REBALANCE ..                              
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX            
ALTER TABLE .. RENAME COLUMN                             
ALTER TABLE .. RENAME CONSTRAINT                         
ALTER TABLE .. RENAME SHARD .. TO ..                     
ALTER TABLE .. RENAME TO ..                              
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
CREATE PACKAGE                                           
CREATE PACKAGE BODY                                      
CREATE PROCEDURE                                         
CREATE PROFILE                                           
CREATE SCHEMA                                            
CREATE SEQUENCE                                          
CREATE SYNONYM                                           
CREATE TABLE                                             
CREATE TABLE ... AS SELECT                               
CREATE TABLESPACE                                        
CREATE USER                                              
CREATE VIEW                                              
DROP AUDIT POLICY                                        
DROP CLUSTER GROUP                                       
DROP FUNCTION                                            
DROP INDEX                                               
DROP PACKAGE                                             
DROP PROCEDURE                                           
DROP PROFILE                                             
DROP SCHEMA                                              
DROP SEQUENCE                                            
DROP SYNONYM                                             
DROP TABLE                                               
DROP TABLESPACE                                          
DROP USER                                                
DROP VIEW                                                
FLASHBACK TABLE                                          
GRANT .. ON DATABASE                                     
GRANT .. ON PACKAGE                                      
GRANT .. ON PROCEDURE                                    
GRANT .. ON SCHEMA                                       
GRANT .. ON TABLE                                        
GRANT .. ON TABLESPACE                                   
GRANT USAGE ON ..                                        
NOAUDIT POLICY                                           
PURGE CONSTRAINT                                         
PURGE DBA_RECYCLEBIN                                     
PURGE INDEX                                              
PURGE RECYCLEBIN                                         
PURGE TABLE                                              
PURGE TABLESPACE                                         
REVOKE .. ON DATABASE                                    
REVOKE .. ON PACKAGE                                     
REVOKE .. ON PROCEDURE                                   
REVOKE .. ON SCHEMA                                      
REVOKE .. ON TABLE                                       
REVOKE .. ON TABLESPACE                                  
REVOKE USAGE ON ..                                       
TRUNCATE TABLE                                           

128 rows selected.
```

<a id="626249d01000fc6a"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="6f8689e4887630a2"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="219c76d9075283e4"></a>
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

<a id="2e81515e52a8e32e"></a>
### Description

It prohibits DDL operation on the table of supplemental log, because it affects CDC's give up.  
For more information, refer to [The occurrence of give up and whether to allow DDL statement according to DDL category](../part-07-replication/50-cyclone.md#ec779fc67c96906b).

<a id="e0d2b6180ff232ac"></a>
## DISABLE_SERIAL_DDL

<a id="01bd2b4ee5199040"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="a7f5891c75603e28"></a>
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

<a id="08e44845e9980a26"></a>
### Description

DDL is executed for all cluster members after sequentially acquiring locks in cluster environment as described in [Processing DDL in Cluster](../part-03-sql-manual/12-sql-languages.md#f61ca2e8df9e4275).  
The DDL which is performed in the serial lock method is called as the serial DDL.

DDL statements which are affected by DISABLE_SERIAL_DDL are queried as follows, and most of schema DDLs are affected.

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
ALTER DATABASE CLEAR PASSWORD HISTORY             YES    SERIAL           
ALTER DATABASE DATAFILE AUTOEXTEND ..             YES    SERIAL           
ALTER FUNCTION                                    YES    SERIAL           
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
ALTER TABLE .. READ ONLY                          YES    SERIAL           
ALTER TABLE .. READ WRITE                         YES    SERIAL           
ALTER TABLE .. RENAME COLUMN                      YES    SERIAL           
ALTER TABLE .. RENAME CONSTRAINT                  YES    SERIAL           
ALTER TABLE .. RENAME SHARD .. TO ..              YES    SERIAL           
ALTER TABLE .. RENAME TO ..                       YES    SERIAL           
ALTER TABLE .. SET UNUSED COLUMN                  YES    SERIAL           
ALTER TABLE .. STORAGE                            YES    SERIAL           
ALTER TABLESPACE .. ADD                           YES    SERIAL           
ALTER TABLESPACE .. DROP                          YES    SERIAL           
ALTER TABLESPACE .. OFFLINE                       YES    SERIAL           
ALTER TABLESPACE .. ONLINE                        YES    SERIAL           
ALTER TABLESPACE .. RENAME TO                     YES    SERIAL           
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }  YES    SERIAL           
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
CREATE PACKAGE                                    YES    SERIAL           
CREATE PACKAGE BODY                               YES    SERIAL           
CREATE PROCEDURE                                  YES    SERIAL           
CREATE PROFILE                                    YES    SERIAL           
CREATE SCHEMA                                     YES    SERIAL           
CREATE SEQUENCE                                   YES    SERIAL           
CREATE SYNONYM                                    YES    SERIAL           
CREATE TABLE                                      YES    SERIAL           
CREATE TABLE ... AS SELECT                        YES    SERIAL           
CREATE TABLESPACE                                 YES    SERIAL           
CREATE USER                                       YES    SERIAL           
CREATE VIEW                                       YES    SERIAL           
DROP AUDIT POLICY                                 YES    SERIAL           
DROP FUNCTION                                     YES    SERIAL           
DROP INDEX                                        YES    SERIAL           
DROP PACKAGE                                      YES    SERIAL           
DROP PROCEDURE                                    YES    SERIAL           
DROP PROFILE                                      YES    SERIAL           
DROP SCHEMA                                       YES    SERIAL           
DROP SEQUENCE                                     YES    SERIAL           
DROP SYNONYM                                      YES    SERIAL           
DROP TABLE                                        YES    SERIAL           
DROP TABLESPACE                                   YES    SERIAL           
DROP USER                                         YES    SERIAL           
DROP VIEW                                         YES    SERIAL           
FLASHBACK TABLE                                   YES    SERIAL           
GRANT .. ON DATABASE                              YES    SERIAL           
GRANT .. ON PACKAGE                               YES    SERIAL           
GRANT .. ON PROCEDURE                             YES    SERIAL           
GRANT .. ON SCHEMA                                YES    SERIAL           
GRANT .. ON TABLE                                 YES    SERIAL           
GRANT .. ON TABLESPACE                            YES    SERIAL           
GRANT USAGE ON ..                                 YES    SERIAL           
NOAUDIT POLICY                                    YES    SERIAL           
PURGE CONSTRAINT                                  YES    SERIAL           
PURGE DBA_RECYCLEBIN                              YES    SERIAL           
PURGE INDEX                                       YES    SERIAL           
PURGE RECYCLEBIN                                  YES    SERIAL           
PURGE TABLE                                       YES    SERIAL           
PURGE TABLESPACE                                  YES    SERIAL           
REVOKE .. ON DATABASE                             YES    SERIAL           
REVOKE .. ON PACKAGE                              YES    SERIAL           
REVOKE .. ON PROCEDURE                            YES    SERIAL           
REVOKE .. ON SCHEMA                               YES    SERIAL           
REVOKE .. ON TABLE                                YES    SERIAL           
REVOKE .. ON TABLESPACE                           YES    SERIAL           
REVOKE USAGE ON ..                                YES    SERIAL           
TRUNCATE TABLE                                    YES    SERIAL           

103 rows selected.
```

DDL statements which are not affected by DISABLE_SERIAL_DDL are queried as follows, and most of cluster DDLs are affected.

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
ALTER CLUSTER GROUP .. OFFLINE CLUSTER MEMBER             YES    MANUAL           
ALTER DATABASE ADD LOGFILE GROUP                          YES    NONE             
ALTER DATABASE ADD LOGFILE MEMBER                         YES    NONE             
ALTER DATABASE ARCHIVELOG                                 YES    NONE             
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS              YES    MANUAL           
ALTER DATABASE DROP LOGFILE GROUP                         YES    NONE             
ALTER DATABASE DROP LOGFILE MEMBER                        YES    NONE             
ALTER DATABASE NOARCHIVELOG                               YES    NONE             
ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS           YES    MANUAL           
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE          YES    NONE             
ALTER DATABASE RENAME LOGFILE                             YES    NONE             
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                 YES    NONE             
ALTER INDEX .. REBUILD                                    YES    MANUAL           
ALTER SEQUENCE .. SYNCHRONIZE                             YES    MANUAL           
ALTER SYSTEM SWITCH LOGFILE                               YES    NONE             
ALTER TABLE .. MERGE SHARDS .. INTO ..                    YES    MANUAL           
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..          YES    MANUAL           
ALTER TABLE .. REBALANCE ..                               YES    MANUAL           
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX             YES    MANUAL           
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP .. YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE ..                             YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

25 rows selected.
```

<a id="2e594dab6ae3b224"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="5e2c6edb47318106"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="a0f77978e700c9c8"></a>
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

<a id="cd0944d1dce6818f"></a>
### Description

It disables UPDATE primary key which caused CDC give up.

<a id="d27237222d211e7a"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="4607ff8113467dc4"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE**

<a id="02e7745b2469e44e"></a>
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

<a id="bef2f4e48168d268"></a>
### Description

It disallows TARGETTYPE protocol.

<a id="5927a36655afb4c3"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="ce6f37b52912ac1c"></a>
### Basic Information

<a id="0acba712001929c5"></a>
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

<a id="92294a5e08d8dd0e"></a>
### Description

It disallows TARGETTYPE_WITH_ALL protocol.

<a id="69f58f7ed50fc6b3"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="c81abbaac4a3bd22"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="f9b9ca8d7e7446af"></a>
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

<a id="53e7533f3adfaf3d"></a>
### Description

It disallows TARGETTYPE_WITH_NAME protocol.

<a id="6ec2639a38c5b75b"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="9137360a8a57659a"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_BUFFER_SIZE**

<a id="a07d1416683b6e04"></a>
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

<a id="e216da985ef45053"></a>
### Description

It is the size of entire communication buffer used in shared mode. It is allocated to and used in Shared Static Area (SSA).

<a id="3596f85b9205a952"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="866f40a40c86ba7c"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_UNIT_SIZE**

<a id="31147cb2cfa36b9c"></a>
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

<a id="14703eb92983644a"></a>
### Description

It is the unit size managed by dispatcher in shared mode. If the size is large, the memory is wasted. If it is small, the performance is degraded. It is set to the maximum communication packet size in the shared mode.

<a id="98322cf8ee72bf9d"></a>
## DISPATCHER_CONNECTIONS

<a id="f37d693ccde9d03d"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="8687cbd19b172382"></a>
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

<a id="45082dde767dc332"></a>
### Description

It is the maximum number of connection (client) which a dispatcher can manage in shared mode.  
If the system- supported maximum value is smaller than the set value, it is internally set to the system maximum.

<a id="a177cbf320156c7b"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="5f7565493a5034f3"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="cb29dbab6c938378"></a>
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

<a id="206e6de6df5c3dbe"></a>
### Description

It is the dispatcher dequeue interval for busy waiting. (micro second)

<a id="b5ed4ff64f45cc61"></a>
## DISPATCHER_LOAD_BALANCING

<a id="75f005361562d08b"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="8f3f007f48d4790d"></a>
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

<a id="9d3f18923f2b15f5"></a>
### Description

It is an algorithm allocating a dispatcher when connecting to a client in the shared mode.

- 0: It is allocated to a dispatcher of which the number of currently attached clients are small.
- 1: It is sequentially allocated to a dispatcher.

<a id="9b7a6dbb1a64a8fb"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="ed048de4c395fe9c"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="0f35dd062b1cc66c"></a>
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

<a id="5199c9deac20da03"></a>
### Description

It determines NUMA node to which dispatchers are to be connected. This property is operated when NUMA property is set to on.  

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="51109c8fc970ee96"></a>
## DISPATCHER_QUEUE_SIZE

<a id="6361c5832bc7fc4d"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="3f1786dd76da1486"></a>
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

<a id="6bdb0adcc0cd95b4"></a>
### Description

In shared mode, it sets the queue size for the communication between the dispatcher and the shared-server.

<a id="24f36f46870dd37a"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="2d0d890c2d2ad8c2"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="5a0051f299b19756"></a>
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

<a id="42e94a95285a8e18"></a>
### Description

It is the count of mini queue per request queue.

<a id="542dbca54ce6c726"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="d1d9f0272a0382a6"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="07fbd55271b5bd5c"></a>
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

<a id="9d171943457cdafe"></a>
### Description

It is the count of mini queue per response queue.

<a id="18328bbb2dede094"></a>
## DISPATCHERS

<a id="af8d21c699c20231"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="74d4997ef3df1d8b"></a>
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

<a id="c3c2043de2b72567"></a>
### Description

It sets the number of dispatcher processes when using the shared mode.  
It can not reduce the value by using alter system on open phase.

<a id="2ec12732f0fe8e3c"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="1f73101a17ab2c4b"></a>
### Basic Information

<a id="ed13bb7ebb785f7e"></a>
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

<a id="66ca41189ada0119"></a>
### Description

If the memory is not sufficient to expand the hash bucket in the query using an instant hash table, then it determines whether to fail the query or to perform the query without expanding the hash bucket.

<a id="587e079bec9ec589"></a>
## FETCH_FAILOVER

<a id="85ffc4053fca9e08"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="4dfbd948c0de3907"></a>
| Item | Description |
| --- | --- |
| Name | FETCH_FAILOVER |
| Summary | enable fetch failover |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="d53f934c4bebbd17"></a>
### Description

It enables the fetch failover.

<a id="de72f2b557f6224c"></a>
## FULL_TABLE_SCAN_CACHING_THRESHOLD

<a id="b3a67451e1d1af6c"></a>
### Basic Information

<a id="abd1bf3e30f29362"></a>
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

<a id="d2a108d72f6518e7"></a>
### Description

The threshold of the table size determines whether to cache the tables created in the disk tablespace to buffer cache when performing a full scan. FULL_TABLE_SCAN_CACHING_THRESHOLD sets this threshold value. The default value is 20. In this case, it caches only the tables which are using the number of pages equal to or less than 2.0% of [BUFFER_CACHE_SIZE](#c97c648cbb2c2128). If this value is 1000 (100%), then all tables are cached to the buffer when performing the full scan.

For example, if BUFFER_CACHE_SIZE is 8192 and FULL_TABLE_SCAN_CACHING_THRESHOLD is 509 (50.9%), then only the tables which are using the number of pages equal to or less than 4169 (50.9% of 8192) are cached to the buffer when performing the full scan.

<a id="a81417c7644b6ecc"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="0637dc52ae06ad17"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="e77fad461e83378d"></a>
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

<a id="79eaa12d0bcaf905"></a>
### Description

It sets whether to support the query execution including the session dependent information in the global connection.

<a id="5cd2373bed8487ff"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="f8a15fe6aa4a10e8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="a80a5a322ff65d19"></a>
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

<a id="20234330a3682617"></a>
### Description

It is the size of global journal buffer.

<a id="5ca4e4f699530e81"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="e22dabbb37f1a76d"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="241aede10c2f191e"></a>
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

<a id="e860140ac167e113"></a>
### Description

It is the total max size of global journal buffer.

<a id="2ebd90a05e29e798"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="610cbd57a7eb56eb"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="78b4438b8be6f817"></a>
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

<a id="545a96fa8031c6d4"></a>
### Description

When changing the global property, it performs the lock to control the concurrency. In this case, the waiting time to perform the lock is set.

<a id="dc34e153c311d484"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="9cbb00e34662f446"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="125c88242181c56b"></a>
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

<a id="84933164ce13104b"></a>
### Description

It is a property to change the commit write mode of the global transaction. TRANSACTION_COMMIT_WRITE_MODE property is applied to all transactions, but GLOBAL_TRANSACTION_COMMIT_WRITE_MODE property is applied only to a global transaction. If the property is set to 2, then it follows the TRANSACTION_COMMIT_WRITE_MODE.

- 0: It does not wait.
- 1: It waits.
- 2: It follows the value of TRANSACTION_COMMIT_WRITE_MODE.

<a id="a65631dea99eb0dd"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="5449525c582deda8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="2746de4e3f7894fb"></a>
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

<a id="097b8bdb86ea6c4a"></a>
### Description

It determines whether to process the data with a global transaction or with multiple domain transactions when the transaction changed the data through two cluster groups.

- 0: It processes with a global transaction.
- 1: It processes with multiple domain transactions.

> If this property is set to 1, it commits each cluster group with a separate transaction, so it does not guarantees the transaction atomicity.

<a id="b200d3c63425de05"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="7d9fcd4f0d8d1367"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="600c68fe9be4da31"></a>
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

<a id="5a2f47c26139bf72"></a>
### Description

It is the default directory of global transaction log.

<a id="3aad66be913ffdca"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="984c407b5734d26f"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="55809546c6a3c2b0"></a>
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

<a id="e74ad9cc4ce2822d"></a>
### Description

It is the file size of global transaction log.

<a id="5eb52cf90f782e4e"></a>
## GMASTER_NUMA_NODE

<a id="5465d430f511b812"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="a1a8be889282c2ba"></a>
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

<a id="c4e7742b7af3a9a0"></a>
### Description

It sets the ID of NUMA node to be used by gmaster daemon. This property is operated when NUMA property is set to on.

<a id="b2b9e5b195fdcd99"></a>
## GMON_AUTOSTART

<a id="4cb765c89da68dcc"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="0eb449029ee646be"></a>
| Item | Description |
| --- | --- |
| Name | GMON_AUTOSTART |
| Summary | Indicate whether gmon process automatically starts or not ( 0 \| 1 ) |
| Data type | BOOLEAN |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | 1 |

<a id="b35537a266d7decd"></a>
### Description

It sets whether to start gmon process automatically.

<a id="db347b3a0d67208e"></a>
## HINT_ERROR

<a id="e9b9773914a7bbdf"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="e26b0490edca2c1a"></a>
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

<a id="d65b247989872a2e"></a>
### Description

It sets whether to check syntax error and validation error for hint syntax.

<a id="f1a72ddd06ea47a5"></a>
## IDLE_TIMEOUT

<a id="20b6a2c98a54a4f1"></a>
### Basic Information

**Basic Information of IDLE_TIMEOUT**

<a id="19b1486db8f198f8"></a>
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

<a id="cb6ce9ca1e60847f"></a>
### Description

It sets the maximum IDLE time possible to wait in C/S session. If it exceeds the specified idle time, TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="1a3b1edfffdafecd"></a>
## IN_DOUBT_DECISION

<a id="a57a98a04e4c8af7"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="6aa370d85eb9a855"></a>
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

<a id="8b720b595363c0ad"></a>
### Description

It determines whether to commit or to rollback the in-doubt transaction of distributed transactions.

- 1: Commit
- 2: Rollback

<a id="3e3cdf0a65d90e60"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="67478d6021a280c3"></a>
### Basic Information

<a id="1a93a8c82cf547cc"></a>
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

<a id="88d861d1f9c97bb2"></a>
### Description

It is the maximum number of values which are targets of *in key range* performing the *in key range scan* based on array.

- IN_KEY_RANGE_ARRAY_COUNT should be 3 or bigger to perform the *in key range scan* based on array for the statement below.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

If the maximum number of in key range target values are bigger than IN_KEY_RANGE_ARRAY_COUNT value, then in key range in key range scan is performed based on instant table.

<a id="dddde93e51ba0d40"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="95ac4784f3cb7865"></a>
### Basic Information

<a id="80876edc397aed50"></a>
| Item | Description |
| --- | --- |
| Name | INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE |
| Summary | number of pages read in one I/O operation during an incremental backup |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 8192 |
| Default value | 32 |

<a id="7027f4a910bcd8f5"></a>
### Description

It sets the number of pages to read by one time disk IO for performing incremental backup of the disk tablespace.

<a id="e72b9e2dffe55883"></a>
## INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA

<a id="05df2955c2fbac23"></a>
### Basic Information

<a id="7e1ca51e9a147b44"></a>
| Item | Description |
| --- | --- |
| Name | INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA |
| Summary | criteria for the number of flush page count to update datafile header |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 134217728 |
| Default value | 134217728 |

<a id="ddc79ffa4744e466"></a>
### Description

It sets the criteria of updating the data file header in the disk tablespace. It sets the LSN to start recovery in the datafile header when the pages updated as many as the set value is applied while IO slave applies the pages updated in the buffer cache to the disk. In this way, disk IO is decreased at restart recovery.

<a id="daa13fdb0a513198"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="ee9c5a6a9a47edfc"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="7f26ea11948cfb89"></a>
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

<a id="f49950d566f900c6"></a>
### Description

When creating an index, it specifies the number of parallel factor.

- 0: It is specified as the number of the core factor in the system.

<a id="14b0299642216617"></a>
## INDEX_LOGGING_THROTTLING

<a id="7c05b3b6158780b2"></a>
### Basic Information

<a id="19ed56a6a7a86cef"></a>
| Item | Description |
| --- | --- |
| Name | INDEX_LOGGING_THROTTLING |
| Summary | The limit on the number of dirty blocks in the log buffer during index building or rebuilding |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| Default value | 10737418240 |

<a id="8b5d91c8308d004d"></a>
### Description

This property is used to prevent system overload caused by bulk logging during index creation and rebuild, ensuring that online services are not affected.

If there are more dirty blocks than the specified property value in the log buffer during index logging, it will wait until the dirty blocks are flushed to disk.

<a id="cefcf6aa4b9eb526"></a>
## INDEX_MERGE_RUN_COUNT

<a id="cd025f6d12708094"></a>
### Basic Information

**Basic Information of MEMORY_MERGE_RUN_COUNT**

<a id="50211440b5aaa32c"></a>
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

<a id="d6a1ee7caa9c7856"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in certain block size (INDEX_SORT_RUN_SIZE) units, merging the sorted blocks, and generating the internal node. INDEX_MERGE_RUN_COUNT sets the number of the sorted blocks to be merged at a time.

<a id="9398c2ccf14e470a"></a>
### ALIAS

<a id="11b34dc5f00c227f"></a>
| Item | Description |
| --- | --- |
| Original name | INDEX_MERGE_RUN_COUNT |
| ALIAS | MEMORY_MERGE_RUN_COUNT |

<a id="490d142ef9762b04"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="52a6617e806e531d"></a>
### Basic Information

<a id="c83cf441c42e2f88"></a>
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

<a id="6a4a320b72cea774"></a>
### Description

When DML is performed while rebuilding the index on ONLINE mode, the journal data is stored. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal data. INDEX_REBUILD_BLOCK_READ_COUNT sets how much journal data to be read and applied to the index during this process.

<a id="d5606acf31baae4c"></a>
## INDEX_SORT_RUN_SIZE

<a id="8588d3c2fa5e7fd8"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="02e0149a839d8b4f"></a>
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
| MAX | 32768 |
| Default value | 8192 |

<a id="8f0b4f43dcfb91ed"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in a certain block size (INDEX_SORT_RUN_SIZE) unit, merging the sorted blocks, and generating the internal node. INDEX_SORT_RUN_SIZE sets the size of a single block to be sorted.

<a id="84f04449299e9972"></a>
### ALIAS

<a id="a7ac9a14c025aa8d"></a>
| Item | Description |
| --- | --- |
| Original name | INDEX_SORT_RUN_SIZE |
| ALIAS | MEMORY_SORT_RUN_SIZE |

<a id="62d057d42e0d9413"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="0a3d240f5d5a3f56"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="d8f514a17814fb97"></a>
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

<a id="ed2c2ba02c4c29c5"></a>
### Description

When creating an index, it specifies the number of parallel factor to merge the sub-tree.   
If that value is bigger than INDEX_BUILD_PARALLEL_FACTOR, then INDEX_BUILD_PARALLEL_FACTOR is used.

- 0: It follows INDEX_BUILD_PARALLEL_FACTOR.

<a id="2b861956d54dc475"></a>
## INST_ALLOCATOR_COUNT

<a id="38a207fedec798ee"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="9d552fd82d3cc3b1"></a>
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

<a id="9c7b9867d5ba2356"></a>
### Description

This property increases the parallel property of operation allocating or deleting an instant block.

<a id="274309ed5a245725"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="45d8fae1f7e59c27"></a>
### Basic Information

<a id="11787ed7854d4985"></a>
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

<a id="035d6fa2546b07ff"></a>
### Description

It sets the maximum expected bucket counts of the hash instant table.

<a id="3109d5fcd61ac628"></a>
## INST_TABLE_BLOCK_SIZE

<a id="bd2998086b2eb72e"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="4a08b2b95eaa96c9"></a>
| Item | Description |
| --- | --- |
| Name | INST_TABLE_BLOCK_SIZE |
| Summary | a block size of instant tables or indexes |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8192 |
| MAX | 1048576 |
| Default value | 16384 |

<a id="6a33676ba018e2c8"></a>
### Description

It determines the size of an instant block. If the anchor area of an instant record is bigger than an instant block, then the following error occurs.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="57bef35ddf70b811"></a>
## IPC_CHANNEL_COUNT

<a id="503ca23b15034408"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="6dbee0d8604ab9d8"></a>
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

<a id="d0306b7d4b7394f6"></a>
### Description

It sets the number of channels for IPC communication.

<a id="d6d6c3fce6ae89aa"></a>
## JOURNAL_TEMP_DIR

<a id="d243d2cc7816b51d"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="aba9f9a5777bba8e"></a>
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

<a id="1c9a50017293d9b6"></a>
### Description

It is the temporary directory of journaling.

<a id="e1807026ca376c4d"></a>
## KEEPALIVE_IDLE_TIME

<a id="c2cf83cd32f3b6ce"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="20f386808a0a0360"></a>
| Item | Description |
| --- | --- |
| Name | KEEPALIVE_IDLE_TIME |
| Summary | tcp keepalive idle time for checking dead client session (sec) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 16383 |
| Default value | 300 |

<a id="7298f54a9d65c14f"></a>
### Description

It means the idle duration between the server and client without tcp packet exchange before sending keep alive packet. If there is not tcp packet exchange for seconds (KEEPALIVE_IDLE_TIME), keep alive mechanism starts execution to detect the dead connection on the server side.

<a id="c7e3c40f88d4d5bc"></a>
## LOCAL_CLUSTER_MEMBER

<a id="99ae1fe2a30bdddb"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="6a3ee22a47ee9568"></a>
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

<a id="7a0a95d8c4d4e91b"></a>
### Description

It is the local cluster member name.

<a id="02601caa8dd5fbf0"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="2d4f29a249670d6d"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="ff24723627062af3"></a>
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

<a id="e0c2701b04881598"></a>
### Description

It is host name of local cluster member.

<a id="e9732346e7a00490"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="1b875650eadeba86"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="1f2a67d61e4bdef3"></a>
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

<a id="e03c539b5c56490d"></a>
### Description

It is listen port of local cluster member.

<a id="eaee639b5e29bf01"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="39a5664378c02bc2"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="9f78346052215487"></a>
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

<a id="cb256dad2c5c39ec"></a>
### Description

It is the local journal buffer size.

<a id="a3b112653cf03273"></a>
## LOCATION_FILE

<a id="e2758cab6b3ee762"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="c954a6cb59501228"></a>
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

<a id="f3b2d63c6c35b2cd"></a>
### Description

It is the location file name.

<a id="6b7fa52b25651341"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="b677006dd44aad89"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="2dc73f4c7943d6d1"></a>
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
| Default value | 3 |

<a id="f8728a0fe13501b6"></a>
### Description

It sets the time (second) waiting for the response after the cluster system enquires of a locator about the solution of split-brain situation. This property is used only when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or more.

<a id="b81af8556808af6c"></a>
## LOCK_HASH_TABLE_SIZE

<a id="68c2e468b9567094"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="ae3d2ab4f6b4c65f"></a>
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

<a id="382a5e201b6ac2af"></a>
### Description

It specifies the maximum hash table size managed by a lock manager.

<a id="2256e19131bf9561"></a>
## LOCKABLE_DISPATCHER_CM_BUFFER_COUNT

<a id="18703736952d1747"></a>
### Basic Information

<a id="f69b45d6ebfd5600"></a>
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

<a id="587384bc987b4205"></a>
### Description

It specifies the number of cluster lockable dispatcher's communication buffers.

<a id="b50214cebc9db33b"></a>
## LOCKLESS_DISPATCHER_CM_BUFFER_COUNT

<a id="17d0a996750926bc"></a>
### Basic Information

<a id="b450499b35c5eb86"></a>
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

<a id="3b8cc493bb1a50cf"></a>
### Description

It specifies the number of cluster lockless dispatcher's communication buffers.

<a id="2d4cce734a3ff0bc"></a>
## LOG_BLOCK_SIZE

<a id="21db9d022abdbb75"></a>
### Basic Information

**Basic Information of LOG_BLOCK_SIZE**

<a id="baf7031d76b0aa9c"></a>
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

<a id="30362b7dd3e3d7f9"></a>
### Description

It means the minimum size of what log buffer is flushed to the log file of the disk. Its value should be set to one of 512, 1024, 2048, 4096.

<a id="1a4ea73b5f7e9abb"></a>
## LOG_BUFFER_SIZE

<a id="1550c391f1e3ac0b"></a>
### Basic Information

**Basic Information of LOG_BUFFER_SIZE**

<a id="cd21f15389ca90fd"></a>
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

<a id="31bdaa1037a4baf8"></a>
### Description

A log buffer is the shared memory space in which the redo logs generated in database by the DML/DDL operations are stored. LOG_BUFFER_SIZE is referenced to set the memory size for the log buffer.

<a id="86a9cb6bd5c337bb"></a>
## LOG_DIR

<a id="b2e775f48f135104"></a>
### Basic Information

**Basic Information of LOG_DIR**

<a id="d89c47bfd1f87a1c"></a>
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

<a id="7c2b0b8c097ce2a9"></a>
### Description

The log recorded in the log buffer is flushed to the logfile which exists in a non-volatile storage device to ensure the database durability. LOG_DIR sets the path to the log file.

<a id="2e7c3e628109a146"></a>
## LOG_FILE_SIZE

<a id="be85a8041aabc450"></a>
### Basic Information

**Basic Information of LOG_FILE_SIZE**

<a id="309a67ae61584344"></a>
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

<a id="0b9c42f8aafd7fc8"></a>
### Description

It sets the size of the logfile used in database. It is referenced only when creating the database, then log file size can not be updated after then.

<a id="2d2770bc54cb7409"></a>
## LOG_GROUP_COUNT

<a id="5f9a3b44baa9800a"></a>
### Basic Information

**Basic Information of LOG_GROUP_COUNT**

<a id="a6a4b1996274dba0"></a>
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

<a id="6c445ae5b394f418"></a>
### Description

It sets the number of log group used in database. It is referenced only when creating the database, but after that, it does not affect any operations. After creating database, the operation to add or remove a log group is supported by a separate syntax.

<a id="2aced76fa4ee00a6"></a>
## LOG_MIRROR_MODE

<a id="e7d4a77055c2caf4"></a>
### Basic Information

**Basic Information of LOG_MIRROR_MODE**

<a id="a9633f69bb18986e"></a>
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

<a id="174eb1afe6658b05"></a>
### Description

It is the property to configure the required shared memory when operating LogMirror, the redo log replication tool, at database startup.  
It should be enabled to execute the LogMirror.  
The size of the shared Memory can be changed using LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE.

<a id="d321e6b904fe0a8b"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="3e5552bfbe910aae"></a>
### Basic Information

**Basic Information of LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE**

<a id="3670dd1ac8c78ee0"></a>
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

<a id="5f2c5206a743c85f"></a>
### Description

It sets the size of the shared memory used in LogMirror, the redo log replication tool.   
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="8d12573f1d43cf2c"></a>
## LOG_MIRROR_TIMEOUT

<a id="457d1d8feabeeeff"></a>
### Basic Information

**Basic Information of LOG_MIRROR_TIMEOUT**

<a id="b612c0672d47c757"></a>
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

<a id="c25a7a7833c24f8d"></a>
### Description

It is the response waiting time of the LogMirror.   
If its value is 0, it waits indefinitely. Otherwise, it waits as long as the value set, then TIMEOUT occurs, and it stops LogMirror service. Later, the server is operated normally.  
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="6241d9d9aad32506"></a>
## LOG_SYNC_INTERVAL

<a id="ec9e3c7ecec7d9b3"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="343133cd19c732fe"></a>
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

<a id="028061d599ab628a"></a>
### Description

Log flusher of GOLDILOCKS is a system thread which flushes the log buffer contents to disk logfile. When log flusher wakes up in the idle phase, it checks if log to flush exists. Then it flushes the log if any.  
If the log flusher did not flush within the time set in LOG_SYNC_INTERVAL, it synchronizes the log buffer and the log file by performing a flush until the last block of the current log buffer.

<a id="a0281bab2d8da548"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="3a8299c71fe310c6"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="be9000be192e913f"></a>
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

<a id="830de0357ba5a579"></a>
### Description

It is the millisecond interval for synchronize log.

<a id="f873ade734b815e6"></a>
## MAX_GROUP_COUNT

<a id="4122f7fa3b58b860"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="7afff020250f211e"></a>
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

<a id="810c750f53c625f5"></a>
### Description

It is the maximum group count in the cluster system.

<a id="d4a54b811175ffe3"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="9b03cca5eee7b0ff"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="f914634aa28e30d8"></a>
| Item | Description |
| --- | --- |
| Name | MAX_JOURNAL_FILE_SIZE |
| Summary | maximum journal file size |
| Data type | BIGINT |
| Applicable phase | MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 (1 Terabytes) |
| Default value | 0 (no limit) |

<a id="5c2686c502f30757"></a>
### Description

It sets the maximum size (quota) of the global journaling file which internally stores journaling data when a journaling occurs in cluster system.

<a id="7e5d9c607849361a"></a>
## MAX_NODE_COUNT

<a id="672aebd4bddc67e5"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="1462931d7d1e647d"></a>
| Item | Description |
| --- | --- |
| Name | MAX_NODE_COUNT |
| Summary | maximum node count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | NONE |
| MIN | 1 |
| MAX | 8192 |
| Default value | 64 |

<a id="a2929f17bc1e93d9"></a>
### Description

It is the maximum node (instance) count which can join the cluster system.

<a id="3a84eaecf1767cb2"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="6ef85fe693ada800"></a>
### Basic Information

**Basic Information of MAXIMUM_CONCURRENT_ACTIVITIES**

<a id="d885e6606c675b0a"></a>
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

<a id="f4a3354b768f0501"></a>
### Description

It sets the number of statements which can be executed simultaneously.

<a id="07a8e7629f79e351"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="ee2871b6882a910a"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="41dd9dbb9afc7dbc"></a>
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

<a id="9c77c9c0bf99fded"></a>
### Description

It sets the maximum number of file caches which is being used in the session.

<a id="115d7924306cce30"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="6a7e6e9892703523"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="4ec715e926400cbc"></a>
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

<a id="7982b9ff62e04ad1"></a>
### Description

It sets the maximum number of pages which can be recorded per disk writing operation. If the pages in the disk tablespace are updated in the buffer, then IO thread records them on the disk. If recording nearby pages together when performing disk writing operation, then it increases the efficiency of the system resource by decreasing the number of disk recording.

<a id="79177e7a3d5a1737"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="a23ba17dcf63d224"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="5f4c6bff7cb3155f"></a>
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

<a id="38e3ac821c7c5810"></a>
### Description

When flushing the contents of the log buffer to disk log file, it sets the maximum number of log blocks to be flushed with a single writing operation.

<a id="992987d17129ea86"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="5f2bf07067e1c3ce"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_PAGE_COUNT**

<a id="40ba146e5cef57a9"></a>
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

<a id="e026b43dc2f0c710"></a>
### Description

GOLDILOCKS datafiles are flushed to the disk by the checkpoint and certain DDL statements. For flushing datafiles, it sets the maximum number of data pages to be flushed with a single writing operation.

<a id="e9d82cdbd98d3c13"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="d68a1284e207daac"></a>
### Basic Information

<a id="59975c38c5c9b950"></a>
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

<a id="ded79bb1cdfa9c5e"></a>
### Description

When rebuilding the index on ONLINE mode, it can be performed together with DML, and DML records the updates on the journal log. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal log. The journal logs are initially applied, then journal logs which were accumulated while applying the journal logs are applied. This property sets how may times the journal logs are applied in this way.

<a id="4465980b7947d716"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="55a0cd3528794c58"></a>
### Basic Information

<a id="6f9c39cbf6c3c077"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_JOURNAL_REPLAY_COUNT |
| Summary | maximum number of replaying journals for rebalance table |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| Default value | 2 |

<a id="d7d4563992ed72cb"></a>
### Description

The table rebalancing online can be performed together with DML in the cluster environment, and DML records the updates on the journal log at that moment. The table rebalancing initially applies the journal logs which occurred during synchronizing tables, then applies journal logs which were accumulated while applying the journal logs. This property sets how may times the journal logs are applied in this way.

<a id="0b74f2cdd6c00d60"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="c7671f9915211c4d"></a>
### Basic Information

**Basic Information of MAXIMUM_NAMED_CURSOR_COUNT**

<a id="f34602e9d9825de0"></a>
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

<a id="8cb8c4c1b54b88d3"></a>
### Description

It is the maximum number of named cursor which can be used within a single session.  
A named cursor is created in the following cases.

- When a named cursor is declared using functions like SQLSetCursorName(), SQLGetCursorName()

```
{
    ...
    SQLSetCursorName( stmt,
                      "my_cursor",
                      SQL_NTS );
    ...
}
```

- When the DECLARE cursor syntax is used by a function such as SQLExecDirect (), SQLPrepare ()

```
{
    ...
    SQLExecDirect( stmt,
                   "DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name",
                   SQL_NTS );
    ...
}
```

- When DECLARE cursor FOR UPDATE syntax is used in an embedded SQL

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

> In an embedded SQL, DECLARE CURSOR syntax without FOR UPDATE as follows does not create a named cursor on the session.

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name;
    ...
}
```

<a id="36de1b60782605ff"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="1795f2a8a9b004a0"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="2d6780c09e93638c"></a>
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

<a id="5977212ac766f34d"></a>
### Description

It is the maximum number of package instances which are available in a single session.   
A package instance is created when using the stateful package in the session.

<a id="f53bd20f6b2309c3"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="53ba6b9925a4530c"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="9ce982b1831ee8a0"></a>
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

<a id="5a0872b2aba82373"></a>
### Description

It sets the maximum buffer size available in a single session which is connected to shared mode.  
For more information, refer to [DISPATCHER_CM_BUFFER_SIZE](#6ec2639a38c5b75b).

<a id="a7a2793ae2af3ae8"></a>
## MEASURE_CLUSTER_LATENCY

<a id="4000118a34999be0"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="afe6c0b39bac3947"></a>
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

<a id="402e79845db96f3c"></a>
### Description

It is the measure cluster latency.

<a id="0ad29f72f6579a87"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="de320f58b1d4e9ab"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="97b287c2564c59c8"></a>
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

<a id="6fb8e51ca1ec4e27"></a>
### Description

It is the minimum number of sampling rows when executing [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#91123fc2969654b9) by using the sampling.

<a id="50927aaaedba094e"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="b2ef797e3793187c"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="89190388dbf75834"></a>
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

<a id="f4f1563a17bdc184"></a>
### Description

DML uses the undo page to store the previous image. Undo page is consumed by using a single undo segment per DML. If all allocated pages of undo segments are consumed, the page of another undo segment can be used. MINIMUM UNDO PAGE_COUNT is the minimum number of undo page to specify the undo segment to import page when undo pages are insufficient. If the undo pages are insufficient, the pages can be imported only from the undo segment having more pages than MINIMUM UNDO PAGE_COUNT.

<a id="0bcf25fe7adb2b66"></a>
## NET_BUFFER_SIZE

<a id="3c062f9c0924bf21"></a>
### Basic Information

**Basic Information of NET_BUFFER_SIZE**

<a id="d04219b7b8e5a6b7"></a>
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

<a id="88255e191075244a"></a>
### Description

It sets the TCP communications buffer size.   
In the dedicated mode, it is set to the maximum communication packet size.  
In the shared mode, it is set to [DISPATCHER_CM_UNIT_SIZE](#3596f85b9205a952).

<a id="7ea8c558693ab9b8"></a>
## NLS_DATE_FORMAT

<a id="f31c6495d0ef8088"></a>
### Basic Information

**Basic Information of NLS_DATE_FORMAT**

<a id="c380d7c74a033436"></a>
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

<a id="7c44dd1ecfa98352"></a>
### Description

NLS_DATE_FORMAT specifies the default date format of TO_CHAR and TO_DATE functions.

<a id="fff3ca3eeeea7a35"></a>
## NLS_TIME_FORMAT

<a id="2dc81b226e396522"></a>
### Basic Information

**Basic Information of NLS_TIME_FORMAT**

<a id="ed6682e13268c739"></a>
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

<a id="f6b285ba6ea98f72"></a>
### Description

NLS_DATE_FORMAT specifies the default time format of TO_CHAR and TO_DATE functions.

<a id="6a87f7e07e80669e"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="f90470cfa9e6d197"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="89f4c6f294e2545c"></a>
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

<a id="0ff4a829e0b2a0ad"></a>
### Description

NLS_TIME_WITH_TIME_ZONE FORMAT specifies the default time with time zone format of TO_CHAR and TO_TIME_WITH_TIME_ZONE functions.

<a id="f745ba729e1e8deb"></a>
## NLS_TIMESTAMP_FORMAT

<a id="8038e177d6884a3d"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="1414be0997a81bba"></a>
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

<a id="6bef71c1e5841cf5"></a>
### Description

NLS_TIMESTAMP_FORMAT specifies the default timestamp format of TO_CHAR and TO_TIMESTAMP functions.

<a id="226a187670420c2f"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="c1872f4bea998ca1"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="1272d2c2d7f207f1"></a>
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

<a id="72b463403c75c78f"></a>
### Description

NLS_TIMESTAMP_WITH_TIME_ZONE FORMAT specifies the default timestamp with time zone format of TO_CHAR and TO_TIMESTAMP WITH TIMEZONE functions.

<a id="dcc27b9ed7d05a05"></a>
## NUMA

<a id="c8b41333cd0c10f6"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="8a992f74d49bfef5"></a>
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

<a id="3691d4bbec43f6d5"></a>
### Description

It enables NUMA.

> To use the NUMA property in AIX, the user account should be modified. Execute the following command as a root user.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> &lt;username&gt; is not a root but it is a user account of AIX.  
> Logout then login again to apply the modifications.

<a id="6f9ff41af448b848"></a>
## NUMA_MAP

<a id="07bd3bb29a1223e4"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="5562fe897b1428a7"></a>
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

<a id="2408ecaf62d97a10"></a>
### Description

It sets the map to connect cores of the system to NUMA node. This property is operated when NUMA property is set to on.

The following is an example of the system having four cores.

- Connect core 0 and 1 to number 0 NUMA node, and core 2 and 3 to number 1 NUMA node.

```
NUMA_MAP = '0:0:1:1' # core
```

- Connect core 0 and 1 to number 0 NUMA node, and core 2 and 3 to number 1 NUMA node, and core 1 and 3 to number 2 NUMA node.

```
NUMA_MAP = '0:0,2:1:1,2' # core
```

<a id="ed4fadf089d79654"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="cbc167e86357e9c3"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="052761f216de9d3a"></a>
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

<a id="ae7030ab105aca2f"></a>
### Description

The background process automatically takes the errored member offline after completing the failover caused by the node error.   

If it is not possible to take the errored member offline because it is set to *NO*, then execute the following syntax before the errored member joins the system again.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="b1720f4512a0e95b"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="5fe2a547c9b4412c"></a>
### Basic Information

<a id="b03ff50a0b9f07e5"></a>
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

<a id="a596cad631fd196b"></a>
### Description

DML performed during rebuilding the index on ONLINE mode records the journal log. The journals are applied to the index multiple times when finishing rebuilding the index. [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#e9d82cdbd98d3c13) sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="203454513bdb7978"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="066e28994b8656c7"></a>
### Basic Information

<a id="5d848c97d7fef8be"></a>
| Item | Description |
| --- | --- |
| Name | ONLINE_JOURNAL_REPLAY_THRESHOLD |
| Summary | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 (10G) |
| Default value | 1048576 (1M) |

<a id="ad28f5fd3e7aca73"></a>
### Description

The table rebalancing online applies journal logs several times which were recorded by dml occurred during the performance in the cluster environment. MAXIMUM_JOURNAL_REPLAY_COUNT sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="d419707610c798e0"></a>
## OS_GROUP_ACCESS

<a id="8110476be1b123e1"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="8f63168b39a48b1e"></a>
| Item | Description |
| --- | --- |
| Name | OS_GROUP_ACCESS |
| Summary | enable access database with OS group permission |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="8334ddec70a36c4b"></a>
### Description

To connect to DA with another user of the same group, this property should be set to *YES*. Also, the umask of the system should be modified to *0002*.

<a id="f047eb6df2a1668f"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="fb4a20b5baa81946"></a>
### Basic Information

<a id="aad5760c4e17517e"></a>
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

<a id="3ef7b269e9465833"></a>
### Description

If the data size to be sent to the client is bigger than PACKET_COMPRESSION_THRESHOLD, it compresses the communication data.

<a id="2fe9863c67e942bf"></a>
## PAGE_CHECKSUM_TYPE

<a id="f442e8ea7023bd0b"></a>
### Basic Information

**Basic Information of PAGE_CHECKSUM_TYPE**

<a id="16dadbd504da7f0f"></a>
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

<a id="876cbdad5b530ae7"></a>
### Description

A checksum is used to guarantee the physical consistency for each page of the datafile. GOLDILOCKS supports a page checksum of LSN, CRC scheme.

- 0: LSN
- 1: CRC

<a id="23143ed50dbdc842"></a>
## PARALLEL_IO_FACTOR

<a id="4a9d1e37d1d42b57"></a>
### Basic Information

**Basic Information of PARALLEL_IO_FACTOR**

<a id="61b766481ead9955"></a>
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

<a id="e3ae91123c7df3f7"></a>
### Description

It sets the number of threads for the parallel loading of data file when starting database and the number of threads for parallel recording of data file at checkpoint.

<a id="737c3a62b982283d"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="33cd062871b99b1c"></a>
### Basic Information

**Basic Information of PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16**

<a id="17a0234cc9ad463c"></a>
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

<a id="cd4659eb59b36268"></a>
### Description

It sets the group directory for parallel I/O of data file. It sets the number of group as many as PARALLEL_IO_FACTOR, then parallel I/O is performed in data file unit which belongs to each group.

<a id="ee0fc762a714dc56"></a>
## PARALLEL_LOAD_FACTOR

<a id="67241a4cfacb5aaf"></a>
### Basic Information

**Basic Information of PARALLEL_LOAD_FACTOR**

<a id="3c3755ae173fb3d5"></a>
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

<a id="7ee23a26836c183c"></a>
### Description

When starting database, it sets the number of threads for parallel operation after loading the memory of a data file.

<a id="6c7a8f6a1e27d71f"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="d9bbcc4c055565b0"></a>
### Basic Information

**Basic Information of PENDING_LOG_BUFFER_COUNT**

<a id="2850b82e847dbf69"></a>
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

<a id="e950090d2374e5fa"></a>
### Description

When multiple transactions are simultaneously running, the pending log buffer is used to reduce the competition for the log buffer. PENDING LOG_BUFFER COUNT sets the number of pending log buffer which can be used simultaneously.

<a id="0649dd29528fdd05"></a>
## PLAN_CACHE

<a id="7a0366593bc53e4c"></a>
### Basic Information

**Basic Information of PLAN_CACHE**

<a id="54f3b2260f6492f4"></a>
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

<a id="d0bbbeb76553b555"></a>
### Description

It determines whether to use the plan cache.

<a id="0c154df2255d8b93"></a>
## PLAN_CACHE_SIZE

<a id="0bfae58f1ad48862"></a>
### Basic Information

**Basic Information of PLAN_CACHE_SIZE**

<a id="4b424a1db8d45f19"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_CACHE_SIZE |
| Summary | sql plan cache size (byte) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 20971520 |
| MAX | 1099511627776 |
| Default value | 104857600 |

<a id="444bebfa9acf8e9b"></a>
### Description

It sets the memory size to be used for the plan cache.

<a id="0024b25d01959540"></a>
## PLAN_HISTORY

<a id="4b097151a64e1adc"></a>
### Basic Information

<a id="541db284622eb4d9"></a>
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

<a id="5edf89a0483712d2"></a>
### Description

It sets whether to use the plan history.

<a id="89d00463854ba8c1"></a>
## PLAN_HISTORY_SIZE

<a id="3e21ae9e3dd9da72"></a>
### Basic Information

<a id="48905b90dcec5748"></a>
| Item | Description |
| --- | --- |
| Name | PLAN_HISTORY_SIZE |
| Summary | plan history size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| Default value | 0 |

<a id="b27713768dd39eb1"></a>
### Description

It sets the number of plans to be stored in the plan history.

<a id="922840afe977ee26"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="43afad2ce3c02a36"></a>
### Basic Information

<a id="f1fc125ca536b7df"></a>
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

<a id="53b6aeb7fb5f058d"></a>
### Description

It sets the initial size of the heap memory to use in the session. Even when there are memories which are not used in the session, the memories are not returned to operating system.

<a id="4617db87890c8e6d"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="5b9fd624e49251ab"></a>
### Basic Information

<a id="21e64de5a1c75d13"></a>
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

<a id="1e4dfb91de644d6f"></a>
### Description

It sets the size of memory to extend when the session allocates additional heap memory.

<a id="e127302e1ef5c5ae"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="c7e30ded09eb551b"></a>
### Basic Information

<a id="0bb12ce6e6bd4172"></a>
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

<a id="4d0abae102a566c2"></a>
### Description

The memory size is preserved as big as this property even when there are unused heap memories in the session, and those memories are not returned to the system but are reused in the session.

Even when it is set to smaller than PRIVATE_STATIC_AREA_INIT_SIZE, it is not decreased to smaller than the size.

<a id="56e151f31648af14"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="6cbf5fcae2bc46fb"></a>
### Basic Information

**Basic Information of PRIVATE_STATIC_AREA_SIZE**

<a id="f255a618a3ec3e39"></a>
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

<a id="3e7dd86d5dff0f8c"></a>
### Description

It specifies the maximum heap memory size to be allocated by the session.

<a id="b49578781962a8e2"></a>
## PROCESS_MAX_COUNT

<a id="d537df721ac617d7"></a>
### Basic Information

**Basic Information of PROCESS_MAX_COUNT**

<a id="bfe79fa427933407"></a>
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

<a id="9fd2e632e169ccd4"></a>
### Description

It specifies the maximum number of processes (threads) available on the system.

Creating system process  
• The process is created each time of connection to D/A mode or C/S dedicated mode.  
• In C/S shared mode, processes are basic balancer, dispatcher and shared-server. A process is   
&nbsp;&nbsp;not created when connecting from client.

<a id="bbd6daafcd3bf539"></a>
## QUERY_TIMEOUT

<a id="a3f086bab12b383e"></a>
### Basic Information

**Basic Information of QUERY_TIMEOUT**

<a id="08c0237db38478fe"></a>
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

<a id="a1743ab41ccc28c1"></a>
### Description

It specifies the maximum time which a command received from the session can be executed. If the execution time exceeds, the TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="aaed1ddc13a1c0ce"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="348f9563819e0e9e"></a>
### Basic Information

**Basic Information of READABLE_ARCHIVELOG_DIR_COUNT**

<a id="08c17c7463066018"></a>
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

<a id="8bfda519d82b6f64"></a>
### Description

It sets the number of directories in which archive redo logs exist when executing media recovery.

<a id="5d2a93105db97e24"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="42bcce558cbc7d9f"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="8e53705e5054f671"></a>
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

<a id="690403dfa3d369f8"></a>
### Description

It sets the number of directories in which incremental backups exist when restoring files using incremental backups.

<a id="ec8f10997977eca2"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="8527a1459b04726b"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="5a7ea8ad2614dae7"></a>
| Item | Description |
| --- | --- |
| Name | REBALANCE_BLOCK_READ_COUNT |
| Summary | block read count for rebalance |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| Default value | 1 |

<a id="7a9fb3653a7b4370"></a>
### Description

It is the block read count for rebalance.

<a id="77a87ff8500720c7"></a>
## REBALANCE_SHARD_DIVISOR

<a id="4340337b4090092b"></a>
### Basic Information

<a id="3c668b307cdc74be"></a>
| Item | Description |
| --- | --- |
| Name | REBALANCE_SHARD_DIVISOR |
| Summary | partition factor of shard upon rebalance |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 1000 |
| Default value | 1 |

<a id="ec8504f45dc1ffbc"></a>
### Description

It sets the number of shards to divide which are used to rebalance and synchronize the table.   
For more information, refer to [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#a5e30678f94e116b).

<a id="1ccc1195f7366ed3"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> It is not supported after 3.1.

<a id="7963e1e123d2d85d"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="cd1f6deff1f6c9fd"></a>
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

<a id="485d049db4f6eff3"></a>
### Description

It sets the minimum page count to check if the plan is recompiled due to the page count modification.

<a id="1f19af67f04471a4"></a>
## RECOMPILE_PAGE_PERCENT

> It is not supported after 3.1.

<a id="5e6226a353511380"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="5069f33cd2848156"></a>
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

<a id="9b160bb000216d96"></a>
### Description

It sets the page percentage when recompiles the plan due to the page count modification. If its value is 0, it does not recompile due to the page count modification.

<a id="687f6fe543843cc7"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="b4c30c9e7c40f2e1"></a>
### Basic Information

<a id="ad8e9563ecce52f3"></a>
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

<a id="73661bdf069ace47"></a>
### Description

It is the default log buffer size for recovery.

<a id="1e0110dea71091ce"></a>
## RECYCLEBIN

<a id="b91002e92bbab03d"></a>
### Basic Information

<a id="998a82efb247bd77"></a>
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

<a id="f09c9c8ce989d4eb"></a>
### Description

It sets whether to activate the recyclebin feature.

<a id="84e574cdda3cf85f"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="cfffacb5ef62b3a1"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="e830453494d250e1"></a>
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

<a id="7a0c01be8cc2dfbe"></a>
### Description

If the size of the created REDO LOG is bigger than REDO_LOG_COMPRESSION_THRESHOLD value, it compresses REDO LOG.

<a id="1560e2f7fcd4dfd5"></a>
## REFINE_RELATION

<a id="8cd08927564ee9c7"></a>
### Basic Information

<a id="42823dfc9bb04590"></a>
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

<a id="53888eadd5264c36"></a>
### Description

If this property is set to NO, then REFINE RELATION process is not performed when restarting the server.

This property can be used when an error occurs during the REFINE RELATION process. However, segments of RELATIONs (tables or indexes) which were dropped but not REFINEd can not be reused. When resolving the error then setting this property to YES and restarting, it tries to REFINE relations which were not dropped.

<a id="0a5e5d6bc202a69c"></a>
## SESSION_FATAL_BEHAVIOR

<a id="20dbff76524a89aa"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="fb657d84f98075e1"></a>
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

<a id="8346e36dd2b47fa6"></a>
### Description

When session fatal occurs, it determines whether to terminate only the thread which caused the fatal or to terminate the process.

- 0: It terminates only the thread which caused fatal.
- 1: It terminates the process.  
  If multiple sessions are simultaneously performed in the process, the process is terminated after all sessions finish using database.

<a id="165fdd9a9cd74ee7"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="10d40bdadbb6013d"></a>
### Basic Information

<a id="f43027ef01d67561"></a>
| Item | Description |
| --- | --- |
| Name | SESSION_MEMORY_INIT_SIZE |
| Summary | initial memory size for session |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| Default value | 131072 (128K) |

<a id="ddb7696866ea5969"></a>
### Description

It sets the shared memory size to be allocated in advance so that it can be used in the session.

<a id="d86af8a8a8a5c822"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="f245ed7dc046ff16"></a>
### Basic Information

<a id="b7228d2384f66af1"></a>
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

<a id="3373ebebea857b5d"></a>
### Description

It sets the threshold value to determine whether to return the dynamic shared memory which is not used by the session to the system when releasing the dynamic shared memory used in the session. In other words, if the memory chunk which is bigger than the set value among unused memory exists, then it is returned to the system.

<a id="7aec351f2e8fc857"></a>
## SESSION_POOL_INIT_SIZE

<a id="c05f8d56a45e5b80"></a>
### Basic Information

<a id="2339956178db5fc8"></a>
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

<a id="98f1650fe9959cb5"></a>
### Description

It sets the initial memory size of the session pool.

If each session needs a memory, then the space is allocated from the session pool. If the space in the session pool is insufficient, then the space is allocated from SSA.   
The session pool is used to prevent the session from frequently accessing to SSA, and if it is set to "0", then the session pool feature is inactivated.

<a id="7fc79f957f092e41"></a>
## SESSION_POOL_NEXT_SIZE

<a id="d38c10d69f175c53"></a>
### Basic Information

<a id="508219bd27202c5c"></a>
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

<a id="1d59ec1b24ca003d"></a>
### Description

It sets how much to extend the memory size in the session pool when expanding the session pool space.  
It is valid only when SESSION_POOL_INIT_SIZE is bigger than 0.

<a id="ef78380fe5427857"></a>
## SHARED_MEMORY_ADDRESS

<a id="a8774ae4225ba932"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_ADDRESS**

<a id="2318ff82cc1a3788"></a>
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

<a id="a755a3bd0b42eca3"></a>
### Description

It specifies the address of Shared Static Area (SSA).

<a id="dc8eed15d085684c"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="444d97627f23d4bf"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_KEY**

<a id="0517a719b03c5e98"></a>
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

<a id="be0068f6927f85cc"></a>
### Description

When running server, it specifies the shared memory key values which are used to allocate Static Shared Area (SSA) space.

<a id="574edb7046c42b58"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="c3df67a2d9181043"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_NAME**

<a id="3d17ac7d4309cadb"></a>
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

<a id="f0066b9130f5cfbe"></a>
### Description

When running server, it specifies the shared memory name which is used to allocate Static Shared Area (SSA) space.

<a id="37e13c2e7e676cbe"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="7b26824d582ef65d"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_SIZE**

<a id="69860587f8b0fa34"></a>
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
| Default value | 629145600 |

<a id="5023331613f664b2"></a>
### Description

It specifies the size of the Shared Static Area (SSA).

<a id="9161591b69a20d89"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="1c3b7bdb990cedcf"></a>
### Basic Information

**Basic Information of SHARED_REQUEST_QUEUE_COUNT**

<a id="41acfe2d8e15dc12"></a>
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

<a id="815c0e74c965020e"></a>
### Description

In shared mode, it sets the number of queues of which the dispatcher requests to the shared-server. A queue is used when multiple dispatchers allocate user's requests to the shared-server. Generally, a single queue is used for the load-balance.   
However, SHARED_REQUEST_QUEUE_COUNT value is increased because if the number of dispatchers and shared-servers increase, then a conflict to the queue causes performance degradation.   
If the value becomes bigger, the load-balance can be inefficient and the possibility of deadlock increases.

<a id="98388bbcd7e80b8a"></a>
## SHARED_SERVERS

<a id="57742506183cb3e4"></a>
### Basic Information

**Basic Information of SHARED_SERVERS**

<a id="0bdb9826198fc63e"></a>
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

<a id="ed916f413f03319c"></a>
### Description

It sets the number of shared-server processes on shared mode.  
At open phase, the value can not be decreased by using alter system.

<a id="029c13651420cf14"></a>
## SHARED_SESSION

<a id="c82ecc671269fb77"></a>
### Basic Information

**Basic Information of SHARED_SESSION**

<a id="dcca0ae24a90b126"></a>
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

<a id="2acbd2f389ed4054"></a>
### Description

It sets whether to activate shared mode. If the value is set to *NO*, load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver) are not executed.

<a id="65b1de175a29b0d3"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="e7b980530ae6c62f"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="a58373fa2deb50c3"></a>
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

<a id="fffaf32eb56d5e11"></a>
### Description

It sets the maximum holding time of the statement required for the snapshot read. TIMEOUT error occurs for a snapshot statement which exceeds the time.

<a id="5b38e9d577d1801d"></a>
## SQL_HISTORY_SIZE

<a id="d81787b42eac5cec"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="7fb269124464c3d8"></a>
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

<a id="5ba08d5ead52c02d"></a>
### Description

It is the history size for SQLs.

<a id="0d55862fab197364"></a>
## SQL_HISTORY_TYPE

<a id="fa246f875704b8df"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="d5c76bb2ba91e671"></a>
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

<a id="d33f35de01c4304e"></a>
### Description

It is the history type for SQLs.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="c452d1d665d3ca50"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="8f0e22268acac78a"></a>
### Basic Information

**Basic Information of SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY**

<a id="fe3168527d90aec6"></a>
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

<a id="430859dc8cf1fdcb"></a>
### Description

It records supplemental log for all changes in the database.

<a id="e921cc2ce82e9c05"></a>
## SYNC_DISPATCHER_CM_BUFFER_COUNT

<a id="52ace90baa53622c"></a>
### Basic Information

<a id="9b5745c0bbb3d4f2"></a>
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

<a id="9fa440ca8ccb8812"></a>
### Description

It specifies the number of cluster synchronization dispatcher's communication buffers.

<a id="897776dc0b9a4193"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="bfb40316c6fb3bde"></a>
### Basic Information

<a id="92eea47f6419b75d"></a>
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

<a id="ab5e50cc21cd86be"></a>
### Description

It sets the initial DISK_DATA_TBS tablespace size when creating the database.

<a id="1a50a859d565cff0"></a>
## SYSTEM_FILE_IO

<a id="6fc275c7eb3c64ea"></a>
### Basic Information

<a id="d8b284c23d98e9dc"></a>
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

<a id="d9cc1a6ce77cbf6f"></a>
### Description

It sets IO type of when using the database file except for the data file and the log file.

<a id="82742e413afb9bb9"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="4a52c826f731c4d2"></a>
### Basic Information

<a id="7adc7d994837b1ec"></a>
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

<a id="2b3a6fc04efd88fa"></a>
### Description

It determines the size of initial MEM_AUX_TBS tablespace when creating the database.

<a id="f0fdc0f4ad101e14"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="b795a2c17933bd08"></a>
### Basic Information

<a id="78fea994f55d9eb6"></a>
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

<a id="c08e72cf35e1f3d2"></a>
### Description

It determines the initial tablespace size of MEM_DATA_TBS when creating database.

<a id="14ae96224673fb9e"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="767af80cbf5efa9e"></a>
### Basic Information

<a id="49237f274b062d94"></a>
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

<a id="cfff82d4cfee4199"></a>
### Description

It determines the initial tablespace size of DICTIONARY_TBS when creating database.

<a id="3703ca4dee44e434"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="c4b173b09bc1872b"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE**

<a id="54e6efcf21c7aee7"></a>
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

<a id="420081353aece02f"></a>
### Description

It determines the initial tablespace size of MEM_TEMP_TBS when creating database.

<a id="0f4dd104bd6f64f8"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="288bf2482f0920ce"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE**

<a id="21f5416c957b81f9"></a>
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

<a id="1fc50c5636b92fcd"></a>
### Description

It determines the initial tablespace size of MEM_UNDO_TBS when creating database.

<a id="197ca317c49d8873"></a>
## SYSTEM_TABLESPACE_DIR

<a id="31c2e0faca81f6c0"></a>
### Basic Information

<a id="634880a0215e65f3"></a>
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

<a id="8a712356ec82b022"></a>
### Description

It sets the path to which the initial system tablespaces are stored when creating database.

<a id="bf470dc6e7df10c5"></a>
## SYSTEM_UDS_DIR

<a id="8e0a40faae832c5f"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="667605ba1c8b70c2"></a>
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

<a id="bae217789d2da32b"></a>
### Description

It sets a directory on which the unix domain socket file is created.  
Setting the directory for the unix domain socket except for DB system, such asglsnr, is managed by a separate configuration file.  
The maximum setting value is 60 bytes. (The maximum size of the absolute path (directory + file name) for the unix domain socket file varies according to OS, but generally it is around 100 bytes.)

<a id="47b6c8d5ea0b0fb6"></a>
## TCP_CLIENT_NUMA_NODE

<a id="255433340b6c8127"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="7c11e9fabc0556f8"></a>
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

<a id="05c527503a82f01d"></a>
### Description

It sets the NUMA node ID to which the client server session is bound. This property is operated when NUMA property is set to on.

<a id="3c4fbcf38ca3324f"></a>
## TCP_NODELAY

<a id="568989477622ac34"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="ba4e43a062fc9526"></a>
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

<a id="dbc46577e6b192d7"></a>
### Description

It sets TCP_NODELAY option of the socket when transferring the data to a client in C/S method (TCP socket).  
Set it to *NO* when fast latency is not required and reducing the network load is needed.

<a id="37a8f6e6c1929b93"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="ce31df80af002bbf"></a>
### Basic Information

<a id="b5f69d25bd55a74f"></a>
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

<a id="2418d20ad693eba1"></a>
### Description

It sets the number of segments to be cached in a session instead of returning them to a tablespace when dropping a global temporary table or a global temporary index segment. Segments in the segment cache are reused later in a global temporary table or a global temporary index.

- 0: It does not use a segment cache of a global temporary table or of a global temporary index in a session.
- 1 ~ 4294967295: It keeps the specific number of segment caches of a global temporary table or a global temporary index in a session.

<a id="7850f98b797a05af"></a>
## TEMP_UNDO_ENABLED

<a id="53259c53b3e67231"></a>
### Basic Information

<a id="8232134ac70d6eed"></a>
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

<a id="6fda31b261452db6"></a>
### Description

It defines the location of logging undo records for a global temporary table.

- 0 (FALSE): It records the undo records in the default undo tablespace of database. 
- 1 (TRUE): It records the undo records in the default temporary tablespace of database.

<a id="b2462927fda6ebc2"></a>
## TIMED_STATISTICS

<a id="d0ae900b5d291272"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="12601d0b581139a7"></a>
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

<a id="21e567837ef63d5e"></a>
### Description

It is whether to check the wait event.  
To record the statistics related to wait event on v$system_event, v$session_event and v$session_wait table, set this property.

- 0: It does not record the statistics.
- 1: It records the statistics.
- 2: It records the statistics by using the high precision timer.

<a id="fa8ff926ab3ef752"></a>
## TIMER_INTERVAL

<a id="120062e8b34ee13c"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="63b16544ab0562e1"></a>
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

<a id="c3774329030d8334"></a>
### Description

It sets the time interval which is required when the timer thread sets the system time.

<a id="f2521763b8497dc5"></a>
## TIMEZONE

<a id="87d73fc161f6642f"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="7cf7a746e4981bfb"></a>
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

<a id="26292a5153b35d3c"></a>
### Description

It is a time zone value of database.  
It is applied when creating database, and it uses the value of the range from '-14:00' to '+14:00'.

<a id="90d8f1dac14e1422"></a>
## TRACE_ALTER_SYSTEM

<a id="d698f7a6c02e8bcb"></a>
### Basic Information

**Basic Information of TRACE_ALTER_SYSTEM**

<a id="2b55944d70ce0016"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_ALTER_SYSTEM |
| Summary | write trace messages forALTER SYSTEM |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="7236ec68d2d66f94"></a>
### Description

It records the SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) when executing ALTER SYSTEM syntax.

Set TRACE_ALTER_SYSTEM property to *ON* to record system changes.

SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax have nothing to do with TRACE_ALTER_SYSTEM property, so they do not affect the performance of TRACE_ALTER_SYSTEM.

<a id="3bc19a12f3d68f8e"></a>
## TRACE_DDL

<a id="578e277047509c9c"></a>
### Basic Information

**Basic Information of TRACE_DDL**

<a id="9261a493fe175202"></a>
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

<a id="c7b7221131181f71"></a>
### Description

When executing DDL, it records the executed SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

Set *TRACE_ALTER_SYSTEM* property to *ON* to record SQL statements execution such as CREATE/DROP/ALTER table.

TRACE_DDL property affects only to DDL statements. However, it has nothing to do with SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax. Therefore, it does not affect the performance.

<a id="2d14f408e7d2e9fc"></a>
## TRACE_LOG_ID

<a id="abb183763aab6bca"></a>
### Basic Information

**Basic Information of TRACE_LOG_ID**

<a id="711246e308de492a"></a>
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

<a id="41ea1fa90fdc0405"></a>
### Description

The execution plan for the query, and other related information are recorded in the trace file (opt_p[process ID_s [session ID].trc) under the trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) when processing queries.

To record SQL statement for the query, the execution plan and the execution time, refer to the following flag information.

**Flag information for TRACE_LOG_ID**

<a id="52f8b9697c5f1f51"></a>
| Information | Flag(on) | Flag(off) |
| --- | --- | --- |
| Whether to output the PSM call flow (procedure/function) | 1000000 | 0 |
| Whether to output the successful SQL query | 100000 | 0 |
| Whether to output the failed SQL query | 10000 | 0 |
| Whether to output the execution plan | 1000 | 0 |
| Whether to output the execution type (direct/prepare) | 100 | 0 |
| Whether to output the bind value | 10 | 0 |
| Whether to output the execution time per section | 1 | 0 |

To set it in a form of "output the successful SQL query" + "output the execution plan" + "output the bind value", set the TRACE_LOG_ID value to 101010.

<a id="085eadb77b40ac36"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="02d5e53701f2f36a"></a>
### Basic Information

<a id="32b0f028ce3d2ee0"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOG_MSGBUF_SIZE |
| Summary | memory buffer size for trace log message |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 8192 |
| MAX | 10485760 |
| Default value | 24576 |

<a id="15e8f0e7e6ce081a"></a>
### Description

It sets the size of the heap memory buffer which is used to configure the log message to be recorded in the trace logfile.

<a id="f1337a7a22e73abe"></a>
## TRACE_LOG_TIME_DETAIL

<a id="3d5b12752f2999f8"></a>
### Basic Information

**Basic Information of TRACE_LOG_TIME_DETAIL**

<a id="53f7acd126ff9618"></a>
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

<a id="463b98d816dd8379"></a>
### Description

It sets whether to increase the time accuracy when recording trace log.  
If the value is ON, it has an accuracy of 1 us.  
If the value is OFF, it has an accuracy of 10 ms.

<a id="311cddd93fa28284"></a>
## TRACE_LOGGER

<a id="b2b6d4e9a10b4f28"></a>
### Basic Information

<a id="a889ae64f1a768ae"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER |
| Summary | trace log type ( 1:file, 2:file & remote ) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| Default value | 1 |

<a id="36fd386a5692db18"></a>
### Description

It sets the target on which the trace log is written.  
If it is 1, then it is recorded in a file, and if it is 2, then it is remotely recorded in a file.  
When it is remotely written, then it remotely collects trace logs from gtrclogger and records in a file.

<a id="9146d3a67f163640"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="31b38017b19400e2"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="4cb0ca7bc8738c4e"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER_REMOTE_HOST |
| Summary | remote host for trace logger |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 255255255255 |
| Default value | 127000000001 |

<a id="cfbb21276ac37bc0"></a>
### Description

It sets the host to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="88f2c35ff249ee7d"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="d7fc163a10469b4e"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="6f88b5e49d14d4f1"></a>
| Item | Description |
| --- | --- |
| Name | TRACE_LOGGER_REMOTE_PORT |
| Summary | remote port for trace logger |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1024 |
| MAX | 49151 |
| Default value | 21470 |

<a id="f98507b25854c86e"></a>
### Description

It sets the port to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="f4a40a9fb147e0e6"></a>
## TRACE_LOGIN

<a id="25c61fdcb4a636a9"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="2caaf108702f7fe5"></a>
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

<a id="50383470833b0a8e"></a>
### Description

It records the related access information in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc) on login.  
Set TRACE_LOGIN property to *ON* to record the related information on login.

<a id="c24bc0f3c23f01fd"></a>
## TRACE_LONG_RUN_CURSOR

<a id="08eeb8a630a19e8e"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_CURSOR**

<a id="b34316dfcedd8ac2"></a>
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

<a id="f63302a2083b2e2e"></a>
### Description

When cursor life-time is longer than the specified property time, then it records the SQL statement of the cursor in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#eea35396ae498598) property to increase the precision.

- The following is an example of recording the SQL statement whose cursor life-time is longer than 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR = 1000;
```

- The following is an example of restoring to the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR TO DEFAULT;
```

It is used to trace the user program maintaining the cursor for a long time as follows.

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

<a id="cf657fc70da6da9d"></a>
## TRACE_LONG_RUN_SQL

<a id="cf8a364d4a875d78"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="e9509ad37b06070e"></a>
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

<a id="2047e42b71711fe3"></a>
### Description

It records the SQL statement whose execution time is longer than the specified property time in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#eea35396ae498598) property to increase the precision.

The following is an example of recording the SQL statement whose execution time is longer than 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

The following is an example of restoring to the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="eea35396ae498598"></a>
## TRACE_LONG_RUN_TIMER

<a id="6f277c1a34f14994"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="e966feddcbc5ff04"></a>
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

<a id="018b3f61d9f7992f"></a>
### Description

It controls the measurement precision when measuring the execution time of the SQL statement by using the following properties.

- [TRACE_LONG_RUN_CURSOR](#c24bc0f3c23f01fd)
- [TRACE_LONG_RUN_SQL](#cf657fc70da6da9d)

- Description of value
    - 0: It uses the timer thread whose interval is 10 milliseconds.
    - 1: It measures the time by using gettimeofday() function. In this case, the precision is higher but the system call causes the work load.

<a id="4564418725d2984b"></a>
## TRACE_SYSTEM_DIR

<a id="f5174086717f025f"></a>
### Basic Information

<a id="4be2eab3d3c3066f"></a>
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

<a id="f6216f629157a8ed"></a>
### Description

It sets the disk path where the trace log message is recorded.

<a id="5521843983b3de41"></a>
### ALIAS

<a id="66510eb5e2399c8b"></a>
| Item | Description |
| --- | --- |
| Original name | TRACE_SYSTEM_DIR |
| ALIAS | SYSTEM_LOGGER_DIR |

<a id="91892dbde0a22c00"></a>
## TRACE_XA

<a id="13c0a3afb3b26c6e"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="096334b4ff062573"></a>
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

<a id="95d6950e4c867ffe"></a>
### Description

It specifies whether to output trace messages when using XA interface. Message is output to the 'SYSTEM_LOGGER_DIR / xa.trc'.

<a id="f4aa3adc5c2a7f16"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="7ca03798d1ea3791"></a>
### Basic Information

<a id="92b8793eecc87894"></a>
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

<a id="3bcf3ae52378793f"></a>
### Description

It is the maximum waiting time when allocating transaction slots.

The following error occurs when the waiting time exceeds TRANSACTION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="d2fafbd123d2d99c"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="31e8089094d4addb"></a>
### Basic Information

**Basic Information of TRANSACTION_COMMIT_WRITE_MODE**

<a id="1f6a3a6c68ab854e"></a>
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

<a id="ae89d351350d4f38"></a>
### Description

TRANSACTION_COMMIT_WRITE_MODE specifies whether a log generated by the transaction is flushed to the disk log file, when the transaction is committed. If TRANSACTION_COMMIT_WRITE_MODE is '1', the log should be flushed to the disk log file at the time of the transaction commit. Otherwise the transaction is committed regardless of log flush.

If the system is operated when TRANSACTION_COMMIT_WRITE_MODE is set to '0', the latest data will be lost when GOLDILOCKS is abnormally terminated without log flush after COMMIT transaction. It is because the logs are not recorded in this case.

Therefore, if all committed transactions should be remained (stored) in database, the system should be operated after setting TRANSACTION_COMMIT_WRITE_MODE to '1'. Or, 'ALTER SYSTEM FLUSH LOGS' statement should be explicitly performed at the time of transaction commit in order to flush log after TRANSACTION_COMMIT_WRITE_MODE is set to '0'.

- 0: no wait
- 1: wait

<a id="dee1a4bcb3ca5706"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="430a4ce4e4bd0a4f"></a>
### Basic Information

**Basic Information of TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT**

<a id="4628d9496074fb51"></a>
| Item | Description |
| --- | --- |
| Name | TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT |
| Summary | The maximum number of undo pages that a transaction can write. |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 13107200 |
| Default value | 13107200 |

<a id="942913b70942dd31"></a>
### Description

It means the maximum number of undo pages which the transaction can record. The minimum value is 1 (8 Kbytes) and the maximum value is 13107200 (100 Gbytes).

<a id="af3fe9cb94af25ac"></a>
## TRANSACTION_TABLE_SIZE

<a id="866d59b014002ebb"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="33ca58fb559d2c4c"></a>
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

<a id="4732194560e2b725"></a>
### Description

It sets the maximum number of transaction tables which are executed in database. The database should restart to modify the number of transaction tables, and the number can be modified as long as the number is bigger than the previously specified number. However, if it is modified to the smaller number, then the restart fails when it is same or smaller than the maximum value of the transaction slot identifier used by the transactions prepared after the restart recovery.

For example, if the value set as 1,024 is modified to 512 and the maximum value of the transaction slot identifier used by the transactions prepared at the restart is also 512, then the restart fails as follows. In this case, modify it to the number bigger than 512, then the restart succeeds.

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

> TRANSACTION_TABLE_SIZE of all cluster members should be same in cluster environment, so it is required to restart all cluster members to modify TRANSACTION_TABLE_SIZE.

<a id="9af58eab74c2f0ce"></a>
## TRANSACTION_TIMEOUT

<a id="be3595c650211b2f"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="1dda7d9b2b113579"></a>
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

<a id="588efe9150286f3f"></a>
### Description

It sets the duration of when the transaction is activated. It is used to prevent the side effects of when the transaction is activated for a long time. If a transaction exceeds the specified time, then gmaster daemon automatically terminates the session owned by that transaction.

<a id="7d24aecf8913426e"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="5958ec5e554ac39d"></a>
### Basic Information

<a id="e5ab7359a6c99534"></a>
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

<a id="b6923c7050f4d9eb"></a>
### Description

It is the maximum waiting time when allocating undo relations.

The following error occurs when the waiting time exceeds UNDO_RELATION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="3eaec8e1ec2c93c3"></a>
## UNDO_RELATION_COUNT

<a id="0df9736d05514da5"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="1f7501f27edca1ba"></a>
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

<a id="d9bf7bb9ef59235e"></a>
### Description

It sets the number of undo relation to be used in database. Undo relation is allocated for the purpose that the transaction executing DML uses undo segment. The database should restart to modify the number of undo relations, and the number can be modified only to the number bigger than the previously specified number.

If it is modified to a smaller number, then the restart fails. For example, if the value set as 128 is modified to 64, then the restart fails as follows. In this case, modify it to 128 or bigger, then the restart succeeds.

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

<a id="a58dbd3baa8cb8bd"></a>
## UNDO_SHRINK_THRESHOLD

<a id="34cff59d3f464311"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="e020226abc84d430"></a>
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

<a id="25a38ffbc354c910"></a>
### Description

Ager thread periodically (10 seconds) checks the undo segment space. If it occupies more space than this property value, then the reusable space is returned to the tablespace. The attempt to return is made until the undo segment space remains as big as this property (byte), and the return is finished when the amount of the remaining undo page becomes smaller than MINIMUM_UNDO_PAGE_COUNT.

<a id="d936fb96f9f443bb"></a>
## USE_LARGE_PAGES

<a id="25392f31fb704d1f"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="601d7686e2152d3d"></a>
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

<a id="a58195b77562dc4e"></a>
### Description

It uses HugePage. HugePage should first be set in the device to use USE_LARGE_PAGES property.

- 0: It does not use the large page.
- 1: It uses the large page. When it fails to allocate the shared memory, then an error occurs.
- 2: It tries to allocate the shared memory by using the large page. When it fails to allocate the shared memory, then it allocates the memory by using the regular page.

> It can be used in Linux kernel 2.6.32-573 or higher.

<a id="05be0f30c245a1be"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="d665a7197eb87a6c"></a>
### Basic Information

<a id="87b0c0b2cb727bfe"></a>
| Item | Description |
| --- | --- |
| Name | USER_DATA_TABLESPACE_MEDIA_TYPE |
| Summary | default media type of user data tablespace |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 ( Memory ) |
| MAX | 1 ( Disk ) |
| Default value | 0 ( Memory ) |

<a id="64c91944d574afc7"></a>
### Description

It sets the default media type if the media type of the tablespace is omitted when creating the user data tablespace. 0 is memory and 1 is the disk.

<a id="e944813a303ded06"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="ce151b02a45049dc"></a>
### Basic Information

<a id="48909670c33544cf"></a>
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

<a id="0f987bf84bf83ae1"></a>
### Description

It sets the default size if the data file size is omitted when creating the user data tablespace or adding the data file.

<a id="b57fc1a49ea938c0"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="901304e1fababe7d"></a>
### Basic Information

<a id="af914b7a0928407f"></a>
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

<a id="e6e833051bdbe7af"></a>
### Description

It sets the default size if the size to be extended is not set when it is required to extend the data file of the user disk data tablespace.

<a id="c6f8a23ae7fdd86f"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="eafb7c26b4068b4f"></a>
### Basic Information

<a id="70f388305d33aba1"></a>
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

<a id="d21d1349a0232d92"></a>
### Description

It sets the default size if the data file size is omitted when creating the user temp tablespace or adding the data file.

<a id="6174ace973c380f5"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="afa720d7eca537ef"></a>
### Basic Information

<a id="538515798706b3af"></a>
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

<a id="b08c1d089f5018bf"></a>
### Description

It is the maximum waiting time of xa transaction in idle (The duration between the beginning of XA and the next transaction). If it remains in Idle exceeding this time, then xa transaction is rolled back.

If it is set to 0, then XA infinitely waits even in idle.

---

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
