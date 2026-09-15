<a id="6333a1a5ee464a14"></a>

# 10. Server Property

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/6333a1a5ee464a14)  
> Tag: `20c.1_30_tag`

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="0c5011fac59f52b3"></a>
## Server Property Information

For more information about SQL syntax to change properties, refer to the followings.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references.md#2301d83a1155f4f2)
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references.md#97223cf2447012a2)

For more information about property types, refer to the followings.

- [V$PROPERTY](9-database-information.md#1ef9c35e47b8a25c)
- [V$SPROPERTY](9-database-information.md#517fb1390b7a935f)

The followings describe basic information items of property in this manual.

**Basic Information item of property**

<a id="6c1dda483874dd0a"></a>
| Item | Description |
| --- | --- |
| Name | Property name |
| Summary | Short description of the property |
| Data type | Data type of the property value |
| Applicable phase | A startup phase which can be updated with ALTER SYSTEM or ALTER SESSION * NONE: Applicable phase does not exist. (If it can be updated, but applicable phase is NONE, then use *SCOPE = FILE* option.) |
| Updatable | Whether property is updatable or not * If the property value is TRUE, it is updatable.  * If the property value is FALSE, only the read-only is possible. |
| ALTER SESSION | Whether property is updatable or not by using [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references.md#97223cf2447012a2) |
| ALTER SYSTEM | Whether property is updatable or not by using [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references.md#2301d83a1155f4f2) * IMMEDIATE: The updated value is immediately reflected in all session after execution. * DEFERRED: The updated value is reflected only in the session which is connected after execution. However, it is not reflected in already connected session. * FALSE: The updated value is not reflected in the session during execution. However, the updated value is reflected after restart, (Properties are updatable by using only *SCOPE=FILE* option.) * NONE: It is not updatable. |
| MIN | If the data type is BIGINT, it is the minimum value of property. If the data type is VARCHAR, the minimum value of property is N/A. |
| MAX | If the data type is BIGINT, it is the maximum value of property. If the data type is VARCHAR, the maximum value of property is N/A. |
| Default value | Default value of the property |

<a id="b9aa05d6712aeeb0"></a>
## AGING_INTERVAL

<a id="e24cbb67a2b5bb33"></a>
### Basic Information

**Basic Information of AGING_INTERVAL**

<a id="20ce690b50b2e86e"></a>
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

<a id="99b7bceacd5fdbc2"></a>
### Description

It sets the idle time (second) when an ager thread which deletes the previous version data does not have a job to process in MVCC based database.

<a id="d8e248f0b01a508c"></a>
## AGING_PLAN_INTERVAL

<a id="5e4ac69628902bb6"></a>
### Basic Information

**Basic Information of AGING_PLAN_INTERVAL**

<a id="62f35366a8f35e60"></a>
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

<a id="67e72ff094933fe9"></a>
### Description

The SQL plan which is older than AGING_PLAN_INTERVAL becomes the aging target.

<a id="95ae2f007f29082f"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="2d6f360671c71613"></a>
### Basic Information

**Basic Information of ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10**

<a id="8bdf050f98842cf9"></a>
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

<a id="dd42be7501da13ce"></a>
### Description

It specifies archiving directory of GOLDILOCKS database's online redo log file. Also, it specifies where to read of archive redo log file at media recovery. The online redo log file creates archive redo log file only in ARCHIVELOG_DIR_1.

ARCHIVELOG_DIR_1 sets only the system, but ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10 sets the session.

<a id="ad9deeefe70f591d"></a>
## ARCHIVELOG_FILE

<a id="d24c4c76f5c02374"></a>
### Basic Information

**Basic Information of ARCHIVELOG_FILE**

<a id="b4e23c47f62c18fe"></a>
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

<a id="6fb47cea6c3d90fe"></a>
### Description

It sets the prefix of the targeted file name stored in the archive directory when archiving the online redo logfile. The archive logfile's name consists of the prefix defined in ARCHIVELOG_FILE, followed by '_', the file sequence and the file extension 'log'. For example, the online logfile with a sequence number of 0 is archived as 'archive_0.log'.

<a id="bcc906e3e7254f1b"></a>
## ARCHIVELOG_MODE

<a id="0db651a08771262b"></a>
### Basic Information

**Basic Information of ARCHIVELOG_MODE**

<a id="c5e2eab7e077d6d2"></a>
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

<a id="b19c77b545f8d00f"></a>
### Description

The property is applied at database creation. The archivelog mode can be set to one of the following value.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

It does not affect archive log mode during operation after database is created. The archive log mode can be modified by using *ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}* in MOUNT phase.

<a id="aaa93e2e6360f568"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="bff3fdc1c21bddd6"></a>
### Basic Information

**Basic Information of BACKUP_DIR_1 ~ BACKUP_DIR_10**

<a id="fda0f5f2562a15f6"></a>
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

<a id="44ac6b5ea7d53fe5"></a>
### Description

A backup file is created when incremental backup is executed. Then it sets a directory of backup file to be read when restoring files using incremental backup. Incremental backups are created only in the directory set in BACKUP_DIR_1.

BACKUP_DIR_1 sets only the system, but BACKUP_DIR_2 ~ BACKUP_DIR_10 sets the session.

<a id="fa15fa305d31a8e2"></a>
## BLOCK_READ_COUNT

<a id="6c8ab2efcadf884c"></a>
### Basic Information

**Basic Information of BLOCK_READ_COUNT**

<a id="8678b8294568f5cf"></a>
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

<a id="d528ed1feec63983"></a>
### Description

The SQL executes operation by reading row in the unit of BLOCK_READ_COUNT which is a row bundle. BLOCK_READ_COUNT  means the number of rows to be processed at a time when operation is executed. It is a basic unit of  pipe-lining process of execution nodes which are used in SQL query processing.

If BLOCK_READ_COUNT value is big the processing performance improves, but many memory resources are used.    
The value between 10 and 100 is recommended.  
If the value becomes bigger than 100 the resource usage increases  proportionately, but the performance improvement does not increase proportionately.

<a id="4c6034f9c28ad9e5"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="571b70e9223f3a8e"></a>
### Basic Information

<a id="49a0c3b3210a57cf"></a>
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

<a id="a9b8f55b12b35a3d"></a>
### Description

It sets whether to simultaneously rebuild the indexes on multiple members when rebuilding the index in cluster environment.

<a id="f78c810f96650287"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="325e2e3331df1abc"></a>
### Basic Information

<a id="0b3c04c63e04febb"></a>
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

<a id="47757d6d50d4f699"></a>
### Description

It sets whether to simultaneously process protocol which can be processed on multiple members at the same time when performing table rebalancing in a cluster environment.

<a id="d438f35f7fc39b51"></a>
## BUFFER_CACHE_SIZE

<a id="91b088225b82049a"></a>
### Basic Information

<a id="5e16a021c741afb6"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_CACHE_SIZE |
| Summary | buffer cache size ( byte ) |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 MB |
| MAX | 1 TB |
| Default value | 64 MB |

<a id="642d7fe7889bf733"></a>
### Description

It sets the size of the buffer which cashes the page in the disk tablespace.

<a id="005d4e68f933e38a"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="626963ade6f17186"></a>
### Basic Information

<a id="9d2bd7cbba4b4953"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_CHECKPOINT_LIST_COUNT |
| Summary | number of buffer checkpoint lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 36 |
| Default value | 1 |

<a id="e289daac4a757994"></a>
### Description

It is linked to the checklist when pages of disk tablespace cached to the buffer are updated. Each checkpoint list flushes updated pages linked to the checkpoint list by its own flush thread to the disk, and BUFFER_CHECKPOINT_LIST_COUNT sets the number of checkpoint lists and the number of flush threads.

<a id="4c54e6675f656479"></a>
## BUFFER_FLUSH_THREADS

<a id="e790f671da4de634"></a>
### Basic Information

<a id="9ccd9368b5a5378f"></a>
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

<a id="5ab533d0563444de"></a>
### Description

It is linked to the flush list then requests flush to the buffer flusher, to reuse bch which cached the updated pages in the buffer lru list. In this case, BUFFER_FLUSH_THREADS sets the number of buffer flushers and flush lists to be used in the database.

<a id="0ee83d428c6c0d54"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="43b0fc47f0237f6f"></a>
### Basic Information

<a id="30bcc804fceb71f7"></a>
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

<a id="3fded417291e8fe2"></a>
### Description

It sets the idle time (sec) when the job to be processed by the buffer flusher flushing updated disk tablespace pages to the disk does not exist.

<a id="5c2850ace46ec79c"></a>
## BUFFER_FREE_LIST_COUNT

<a id="4e268748091bd97f"></a>
### Basic Information

<a id="d8b1d6dd634c09ef"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_FREE_LIST_COUNT |
| Summary | number of buffer free lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 64 |
| Default value | 16 |

<a id="590c5490e520ab55"></a>
### Description

It sets the number of buffer free lists connecting bch which are instantly available to use in the buffer cache.

<a id="22df381968cc09ab"></a>
## BUFFER_HASH_BUCKETS

<a id="3e859bec1f82567f"></a>
### Basic Information

<a id="4d7abddf1193ed38"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_HASH_BUCKETS |
| Summary | number of buffer hash buckets |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 0 |
| MAX | 1073741824 |
| Default value | 0 |

<a id="1b8d84ab3e72f1c2"></a>
### Description

It sets the number of hash buckets for the disk tablespace pages cached in the buffer. It can be set from 0 to 1073741824, and 0 is set by calculating hash buckets as many as pages which can be cached to the buffer which is set according to BUFFER_CACHE_SIZE. If the buffer size is smaller than the specified value, then it adjusts the number of hash buckets to the buffer size.

<a id="e0e997271e9e7970"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="a989c6abae85d36e"></a>
### Basic Information

<a id="2a005d0ba47f2f15"></a>
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

<a id="f8a1a99802c9a17b"></a>
### Description

It sets touch count to transfer pages existing in the cold region to the hot region in buffer lru list.

<a id="0116b509d070906f"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="b4c01328e237d361"></a>
### Basic Information

<a id="7fee52cedae3f23e"></a>
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

<a id="1b7818e0a9c60044"></a>
### Description

It sets the proportion (percentage) of hot region pages to the entire page in the buffer lru list.

<a id="58313b5de02bdcbb"></a>
## BUFFER_LRU_LIST_COUNT

<a id="33792cfb0f00699f"></a>
### Basic Information

<a id="67acf2548542f371"></a>
| Item | Description |
| --- | --- |
| Name | BUFFER_LRU_LIST_COUNT |
| Summary | number of buffer LRU lists |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | FALSE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 64 |
| Default value | 16 |

<a id="36511c9375ea5851"></a>
### Description

It sets the number of lru lists to select a victim among pages in use by caching when the free buffer for caching disk tablespace pages does not exist.

<a id="21c7fc13eb798f14"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="6414e9aa2cbb6c0c"></a>
### Basic Information

<a id="5fdcc849a63281d2"></a>
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

<a id="6ce5feb029ae0adc"></a>
### Description

It sets the maximum number of pages to be used for one time disk IO when full scanning the disk table.

<a id="556f8271bc8410c0"></a>
## BULK_IO_PAGE_COUNT

<a id="73293464c93a3097"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="091479145dfb4902"></a>
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

<a id="4f917fe2379324ea"></a>
### Description

It is used when IO READ of the data file occurs during server restart, or when IO WRITE occurs during creating a data file.

The heap memory is allocated as big as BULK_IO_PAGE_COUNT * 8192 when server restarts or data file is created. If the session's PRIVATE_STATIC_AREA_SIZE is smaller than the heap memory size, an error of insufficient memory may occur. In this case, extend PRIVATE_STATIC_AREA_SIZE.

<a id="babd389cff7834e2"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="2f00d4526ce06167"></a>
### Basic Information

**Basic Information of CDISPATCHER_HOT_POLICY_INTERVAL**

<a id="1e6e123edb70b1eb"></a>
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
| Default value | 100000 |

<a id="0630f41f42eedd29"></a>
### Description

It is the time of the busy waiting when performing the dequeue in the cdispatcher. It is a micro second unit. If this value is big, it uses more cpu but the user response time (latency) is decreased.

<a id="87b7f50f61765e56"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="894314b188be0a20"></a>
### Basic Information

<a id="3be98af410b53efd"></a>
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
| MAX | 32 |
| Default value | 1 |

<a id="6314109ab5975f00"></a>
### Description

It sets the number of cdispatcher threads of lockless data sender and receiver. However, the number of cdispatcher threads of lockable data sender and receiver is set by using [CDISPATCHER_THREADS](#c988761bfc6a1199).

<a id="ddaed01b542d51cc"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="492922ae2f565d63"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="2f1c83e79fb3fcca"></a>
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

<a id="6ee053c52d69348e"></a>
### Description

It is the socket buffer(sender, receiver) size of cdispatcher.

<a id="686836e60b951d7c"></a>
## CDISPATCHER_SYNC_THREADS

<a id="e596aba6dc8fc76f"></a>
### Basic Information

**Basic Information of CDISPATCHER_SYNC_THREADS**

<a id="9153936fae5a96dd"></a>
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
| MAX | 32 |
| Default value | 1 |

<a id="63b92883120431cf"></a>
### Description

It is the thread count of cdispatcher sync.

<a id="c988761bfc6a1199"></a>
## CDISPATCHER_THREADS

<a id="064a7551afb10f03"></a>
### Basic Information

**Basic Information of CDISPATCHER_THREADS**

<a id="b5667393354ffa10"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_THREADS |
| Summary | cdispatcher lockable sender, receiver thread count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 32 |
| Default value | 1 |

<a id="aa66eed5060860f7"></a>
### Description

It sets the number of cdispatcher threads of lockable data sender and receiver. However, the number of cdispatcher threads of lockless  data sender and receiver is set by using [CDISPATCHER_LOCKLESS_THREADS](#87b7f50f61765e56).

<a id="99b038a7da685780"></a>
## CHANGE_TRACKING

<a id="7f925e31d09fe25b"></a>
### Basic Information

<a id="b7e25775a3dce1e4"></a>
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

<a id="dfc9c53fb9dc1160"></a>
### Description

It sets whether to track the updated pages to perform the incremental backup of disk tablespace.

- NO: disable change tracking
- YES: enable change tracking

*change tracking* can be enabled by using ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING on mount or above phase only when the database is operated in archivelog.

<a id="417b6dfe23b70666"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="9da99c6bbcaa474a"></a>
### Basic Information

<a id="bb947cb61ece22c8"></a>
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

<a id="36ec3488190b0166"></a>
### Description

It sets the number of pages to display with one dirty flag when change tracking. For example, if it is set to 32, then one dirty flag is used per 32 pages, and if it is set to 128, then then one dirty flag is used per 128 pages.

<a id="c72973af494b6dce"></a>
## CHANGE_TRACKING_FILE

<a id="2475bc84878390dc"></a>
### Basic Information

<a id="d4df809436dabff4"></a>
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

<a id="2b0f6223795ee09f"></a>
### Description

It sets the file directory which stores the change tracking, and the file name.

<a id="3c69a6a4ea2b681f"></a>
## CHAR_LENGTH_UNITS

<a id="6f0426986571aacd"></a>
### Basic Information

**Basic Information of CHAR_LENGTH_UNITS**

<a id="fc88808783a30c77"></a>
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

<a id="8faad6d7d7c82a27"></a>
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

<a id="be7fc290b526b319"></a>
## CHARACTER_SET

<a id="dbd02b822669b7b7"></a>
### Basic Information

**Basic Information of CHARACTER_SET**

<a id="7658480267da2626"></a>
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

<a id="98dcc1983f9a9052"></a>
### Description

It is a character set of database, and it is applied when database is created.  
The property is set to one of the following values.

**Character set**

<a id="fb188de4b2ee1e74"></a>
| Character set | Description |
| --- | --- |
| SQL_ASCII | ASCII standards |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standards |

<a id="38e5e646cbdd59ca"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="777551f51f63a2d1"></a>
### Basic Information

**Basic Information of CHECK_DEDICATE_CONNECTION_INTERVAL**

<a id="f67ce1c201886a04"></a>
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

<a id="a7c65bbfa5a3c316"></a>
### Description

It is the interval of checking for when the client forcibly cut the connection in C/S dedicate environment. The dedicate server(gserver) checks the socket, and it terminates it if it was cut. The default value is 1,000 millisecond (1 second).

<a id="41a65b890f814e94"></a>
## CLIENT_MAX_COUNT

<a id="b02c51229683a345"></a>
### Basic Information

**Basic Information of CLIENT_MAX_COUNT**

<a id="c5177d922ad5e3ce"></a>
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

<a id="0deb36ea70c92ab2"></a>
### Description

It sets the maximum number of sessions to connect.

<a id="f7e127392401c8b6"></a>
## CLIENT_NUMA_POLICY

<a id="fde325cb4b4502ff"></a>
### Basic Information

**Basic Information of CLIENT_NUMA_POLICY**

<a id="71c7670e8538d398"></a>
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

<a id="e73c4e4249e46380"></a>
### Description

It determines the policy to distribute client processes to NUMA nodes. This property is operated when NUMA property is set to on.

- 0: It determines the NUMA node to be connected by modularizing the session ID.
- 1: It connects to the NUMA node of which is the least connected based on the statistics information.
- 2: C/S client is determined by TCP_CLIENT_NUMA_NODE property, D/A client is determined by DA_CLIENT_ NUMA_NODE property.

<a id="e546c57d6784a918"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="19c75155792324a5"></a>
### Basic Information

**Basic Information of CLOSE_PSM_CHILD_STMTS**

<a id="3617c6d027258880"></a>
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

<a id="b2c89ae851cbac1d"></a>
### Description

It closes the child statement of PSM at the end of each execution.

<a id="1010c27f657ec525"></a>
## CLUSTER_ASYNC_COMMIT

<a id="faf95e9f40de7d05"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="095e8ac86210ce14"></a>
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

<a id="6ed1923c91b242f4"></a>
### Description

It determines whether to internally process the commit protocol on an async mode in cluster system.

> If this property is set to on, it asynchronously commits each node, so the temporary inconsistency among nodes may occur. On the other hand, if it is set to off, it synchronizes everytime it commits, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="15d89afa70928f15"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="b961d379b3190abe"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="2c71c6b7ee9a439b"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_ASYNC_REPLICATION |
| Summary | enable asynchronous replication |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | YES |

<a id="01e4ae6574587b69"></a>
### Description

It determines whether to internally process the replication on an async mode in cluster system.

> If this property is set to on, it asynchronously reflects the data on each node, so the response time varies upon on which node is connected furing the operation. On the other hand, if it is set to off, it synchronizes everytime the data is updated, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="67aadf1f7839a34b"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="a38dee73f1a140f8"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_COUNT**

<a id="805d74b136f97dc5"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_CM_BUFFER_COUNT |
| Summary | communication buffer count for cluster |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 256 |
| Default value | 4 |

<a id="9684b310f11a28e2"></a>
### Description

It is the communication buffer count for cluster.

<a id="a91000da99deb3ec"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="7f7659d1cc4043d9"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_SIZE**

<a id="b7189eaaf66280fa"></a>
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

<a id="40b791241af393b4"></a>
### Description

It is the communication buffer size for cluster.

<a id="3ac780a7875b163c"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="c9b599a4a67ea979"></a>
### Basic Information

**Basic Information of CLUSTER_CM_READ_BUFFER_SIZE**

<a id="04320c8355d1de67"></a>
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

<a id="92bc6792700d17c5"></a>
### Description

It is the communication read block size.

<a id="baa24f0b1163f477"></a>
## CLUSTER_COMMIT_SLAVES

<a id="81df64c693610c9f"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_SLAVES**

<a id="a727718e5ed8f211"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_COMMIT_SLAVES |
| Summary | number of commit slaves |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 8 |
| Default value | 1 |

<a id="91624a19b05446d6"></a>
### Description

It is the number of commit slaves.

<a id="78280ec5ecaddf6e"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="0386e6312fcbd818"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_STREAM_ISOLATION**

<a id="94dfac8a9dddb489"></a>
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

<a id="23fe75f1bf671ddf"></a>
### Description

It determines whether to internally perform the commit process flow in the cluster system separately from other protocol process. The performance may be improved when seperating the commit process according to the system environment.

<a id="ca082ed4f1af1527"></a>
## CLUSTER_CONNECTION

<a id="d92bd2b4907dc307"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION**

<a id="6f81ad2e276a80c0"></a>
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

<a id="c1a1a454ba1d2cac"></a>
### Description

It is the connection mode for cluster. ( socket:0, rdma:1 )

<a id="f633a917bf6822a2"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="9050af61d76075b5"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION_TIMEOUT_SEC**

<a id="e693d4d4c07217d9"></a>
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
| Default value | 5 |

<a id="a3b29645d5f3df29"></a>
### Description

It is the connection timeout for cluster.

<a id="814a34041210856d"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="dac943d677ae86fa"></a>
### Basic Information

**Basic Information of CLUSTER_DATA_SYNC_SERVERS**

<a id="3692df113c5046a2"></a>
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

<a id="c3a5426bfff6263e"></a>
### Description

It is the count of data synchronization server.

<a id="bcc389ceff77f7bf"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="47300dbb216abff2"></a>
### Basic Information

<a id="56aa8fe34d23abe7"></a>
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

<a id="d060c75ab0b51ba9"></a>
### Description

If the competition to occupy the cluster server becomes keen due to the lack of the lockable cluster server, then the cluster deadlock may occur. When cluster deadlock occurs, it waits for the deadlock to be resolved as long as the time set in this property. However, if it is not resolved, then CLUSTER_DEADLOCK_TIMEOUT error occurs.

<a id="15ef99ff9a039303"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="f86d84430283b75d"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_IN_QUEUE_SIZE**

<a id="ec09773fdab562c1"></a>
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

<a id="401eb1f5e4ee77c4"></a>
### Description

It is the in-queue size for cluster dispatcher.

<a id="9f1f8ba4f89a289d"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="1c56c8fa96d1d22e"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_NUMA_STREAM_MAP**

<a id="cbef2adb7271b4bb"></a>
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

<a id="c119d29f3940783e"></a>
### Description

It determines a NUMA node to which the cluster dispatcher is to be connected. This property is operated when NUMA property is set to on.

> If CLUSTER_COMMIT_STREAM_ISOLATION property is set to on, then the 0 stream is set to NUMA node of a commit stream.

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="80ea66a1f3420975"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="8b2e52f165ed8bf2"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_OUT_QUEUE_SIZE**

<a id="560a59e1088181ba"></a>
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

<a id="9fb478470b56286a"></a>
### Description

It is the out-queue size for cluster dispatcher.

<a id="c6cf733ee79925ea"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="b119efbaeae18aae"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_INTERVAL**

<a id="438ee40199b2aec1"></a>
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

<a id="bbe2910da7f0dc03"></a>
### Description

It is the interval seconds for health checking of cluster. 0 means that it is disabled.

<a id="091c90e0c87f98cc"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="9020b6e244f47352"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_RETRY_COUNT**

<a id="0110447396f62a5e"></a>
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

<a id="76bc0b3f3c61a98b"></a>
### Description

It is the retry count for health checking of cluster.

<a id="330c19949c6afa1a"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="8101729cbf19e801"></a>
### Basic Information

**Basic Information of CLUSTER_IGNORE_INACTIVE_MEMBER**

<a id="101c9e6377ec071a"></a>
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

<a id="b147e99ecd9937db"></a>
### Description

It ignores in-active member for cluster.

<a id="8b2c97c361d3d18b"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="1d8f1118dcf54e34"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PACKET_SIZE**

<a id="ebd5d7656c42522a"></a>
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

<a id="8974bbff2f6314e5"></a>
### Description

It sets the maximum packet size of which the remote protocol can transfer at a time. If the column size to be remotely transferred exceeds the property size, then the property size should be set bigger than the column size.

<a id="8379ac916e148820"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="8e50ff8e5946f8ff"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PAYLOAD_SIZE**

<a id="276b12ebafa0e94d"></a>
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

<a id="70b418447617b757"></a>
### Description

The cluster packet which is remotely transferred may be delivered in pieces, and this property sets the maximum size of data to be stored in a piece.

<a id="dcbd220c8e7b4d6d"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="fb2a3cfa23ba538d"></a>
### Basic Information

**Basic Information of CLUSTER_PACKET_ALLOCATION_TIMEOUT**

<a id="e88e1bb48c2ac5cf"></a>
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

<a id="4a5d382d4829fc7e"></a>
### Description

It sets the maximum time (second) of waiting when allocating memory required for cluster packet configuration.

<a id="63202eb596899658"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="de9cd478fc2a53c3"></a>
### Basic Information

<a id="e11948c51b10da96"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT |
| Summary | a time limit of failover policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="e3e3a4dde7ece9af"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property to use the failover policy. However, specify the time limit by using [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#9f0b9368e82656b3) property to use the policy terminating the session.

<a id="9f0b9368e82656b3"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="dc194b99326f5072"></a>
### Basic Information

<a id="d58472ab9e3c0a93"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT |
| Summary | a time limit of session fatal policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| Applicable phase | NO_MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| Default value | 0 |

<a id="d4721bff1220045b"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property to use the policy terminating the session. However, specify the time limit by using [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#63202eb596899658) property to use the failover policy.

<a id="45225a60cfa0201a"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="45e1d28a2aaf495e"></a>
### Basic Information

**Basic Information of CLUSTER_SERVER_RESPONSE_QUEUE_SIZE**

<a id="a78f9222c922290c"></a>
| Item | Description |
| --- | --- |
| Name | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |
| Summary | response queue size for cluster server |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 30 |
| MAX | 32768 |
| Default value | 30 |

<a id="81813a0705a5c42a"></a>
### Description

It sets the maximum queue size to get response from the remote server.

<a id="5001e0a508492aa3"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="afa03be7f0a10f34"></a>
### Basic Information

<a id="309091f57614f6fe"></a>
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

<a id="5008630f04199561"></a>
### Description

It sets the number of hash buckets to control the cluster session.

<a id="26f74ad6f85847fb"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="a480146fa7888213"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY**

<a id="962bdb7a54202de4"></a>
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

<a id="33a5c9e079736bf3"></a>
### Description

It sets the policy to resolve split-brain situation in the cluster system. If the value is set to 1 or over, it enquires the solution of a locator.

> If the query for a locator is timed out, it tries to enquire as many times as CLUSTER_SPLIT_BRAIN_RETRY_COUNT. If the property value after the retry failure is 1, then it forcibly proceeds the failover. If it is 2, then it terminates the fatal.

<a id="97e591676118d894"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="2d384a07089d6185"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RETRY_COUNT**

<a id="4ca0296370c752cf"></a>
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
| Default value | 4 |

<a id="add924cf417ca756"></a>
### Description

It is used when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or over in cluster system. It sets the times of retrying to enquire when the query to a locator does not respond.

<a id="71dcebf57c889e69"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="85c535ebbc47883f"></a>
### Basic Information

**Basic Information of COMMITTER_HOT_POLICY_INTERVAL**

<a id="d9e7e3168d4399ca"></a>
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

<a id="a94c9a95c9208b8e"></a>
### Description

It sets the timezone interval of busy waiting when the commit cserver is dequeing to read the commit protocol message. If it is set to 1,000,000 (1 second), and the time is not passed over 1 second from the last deque success to another deque retry, then it sets the timeout in deque to 0 and performs the busy waiting.

<a id="b6b6a5ff7ef5f165"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="7177df2b13e9909e"></a>
### Basic Information

**Basic Information of CONTROL_FILE_0 ~ CONTROL_FILE_7**

<a id="83dae74751a6cdf9"></a>
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

<a id="88688a6834a062ac"></a>
### Description

If a control file is corrupted, database can not be used. Therefore, the control file is multiplexed for stability of database. It specifies the directory and file name of which stores each control file.

<a id="00f5f7b5d1bfe3f8"></a>
## CONTROL_FILE_COUNT

<a id="acc3f95ac801e766"></a>
### Basic Information

**Basic informatin of CONTROL_FILE_COUNT**

<a id="6edaa3b87d6773d1"></a>
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

<a id="520916169b81ff1d"></a>
### Description

If a control file is corruped, database can not be used. The control file is multiplexed for stability of database. CONTROL_FILE_COUNT specifies the multiplexing number of control files. A control file is multiplexed at least 2 up to 8.

<a id="b22106d328755557"></a>
## CONTROL_FILE_TEMP_NAME

<a id="959b5ccb64ece140"></a>
### Basic Information

**Basic Information of CONTROL_FILE_TEMP_NAME**

<a id="cb516b17771e0f05"></a>
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

<a id="9530a47d2e79c473"></a>
### Description

During database operation, a control file is frequently changed, and its temporary copy can be made if necessary. CONTROL_FILE_TEMP_NAME specifies the directory and its file name to temporarily store the control file.

<a id="74d411ac65a2470e"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="65727dc155abdae1"></a>
### Basic Information

**Basic Information of COORDINATOR_COMMIT_WRITE_MODE**

<a id="e3e80f90d07c2b32"></a>
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

<a id="bc642368359743f2"></a>
### Description

It is a commit write mode applied to a coordinator. If TRANSACTION_COMMIT_WRITE_MODE is *no wait*, and its property is *wait*, then the coordinator node is operated as *wait*, and other nodes are operated as *no wait*.

<a id="22dfbbb764c3ce6d"></a>
## CSERVERS

<a id="fdb49fea295d0435"></a>
### Basic Information

**Basic Information of CSERVERS**

<a id="564e367e2665ccd3"></a>
| Item | Description |
| --- | --- |
| Name | CSERVERS |
| Summary | number of lockable cserver processes |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 512 |
| Default value | 10 |

<a id="28bec91530d956af"></a>
### Description

It sets the number of cluster server processes performing the operation which acquires the lock. The number of cluster server processes performing the operation which does not acquire the lock is set by using [LOCKLESS_CSERVERS](#9d7cee165bbfc221).

<a id="0b412e7cffd00667"></a>
## DA_CLIENT_NUMA_NODE

<a id="e5d0dd6fffa1a03e"></a>
### Basic Information

**Basic Information of DA_CLIENT_NUMA_NODE**

<a id="40f4a22076a77d66"></a>
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

<a id="6ad26bcfddd182ca"></a>
### Description

It sets the NUMA node ID to which the direct access (D/A) session is to be bound. This property is operated when NUMA property is set to ON.

<a id="5518bdf83698094b"></a>
## DATA_STORE_MODE

<a id="b4bee4baf163a927"></a>
### Basic Information

**Basic Information of DATA_STORE_MODE**

<a id="b59c31c2f6e86f4a"></a>
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

<a id="91166a22e85d467b"></a>
### Description

It sets the storing method of database.

- 1: CDS mode supports the concurrency for multiple users but it does not guarantee the durability. It does not record logs for all update operations such as insert/ delete/ update data, consequentially a failure can not be recovered.
- 2: TDS mode guarantees the concurrency for multiple users and the durability using logs.

<a id="597d80b71750346d"></a>
## DATABASE_ACCESS_MODE

<a id="4c3c67dd24d05542"></a>
### Basic Information

**Basic Information of DATABASE_ACCESS_MODE**

<a id="d12da21fb3762c83"></a>
| Item | Description |
| --- | --- |
| Name | DATABASE_ACCESS_MODE |
| Summary | database access mode ( 0: read only, 1: read write ) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| Default value | 1 |

<a id="08b33bc859bf9d85"></a>
### Description

When database starts, it sets the access mode.

- 0: It is able to read operation, but unable to insert/ update/ delete operations on database.
- 1: It is able to read/ insert/ update/ delete operations on database.

<a id="272853e9b47ad3f1"></a>
## DATABASE_INSTANCE_NAME

<a id="a97c680b1d771294"></a>
### Basic Information

**Basic Information of DATABASE_INSTANCE_NAME**

<a id="aff2b91f4b6906ed"></a>
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

<a id="d53ce25a6c0f5a06"></a>
### Description

It is the database instance name.

<a id="2c8c077ee5487f1e"></a>
## DDL_AUTOCOMMIT

<a id="62aa957c890cd75b"></a>
### Basic Information

**Basic Information of DDL_AUTOCOMMIT**

<a id="09652556acd94400"></a>
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

<a id="2f8cbd2820ad459b"></a>
### Description

It sets whether to autocommit DDL operations which are not autocommitted yet. For example, autocommit is not applied to the operations such as creating/altering a table, so if DDL_AUTOCOMMIT is 0, a table creation and alteration can be undone by the rollback. On the other hand, if DDL_AUTOCOMMIT is 1, DDL to which autocommit is not applied is committed immediately.

<a id="573d7363d8a5b3e1"></a>
## DDL_LOCK_TIMEOUT

<a id="67ad6970fbaadf4e"></a>
### Basic Information

**Basic Information of DDL_LOCK_TIMEOUT**

<a id="a56159e8d2ad6427"></a>
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

<a id="fbe6f486b864e2e5"></a>
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

<a id="661ef139ef73c8cf"></a>
## DEADLOCK_PRIORITY

<a id="57ba1018e1ff3dcd"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="2c9030c696b878ad"></a>
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

<a id="bbbd71c70184f1c9"></a>
### Description

When a deadlock occurs while simultaneously processing multiple transactions, a specific transaction with the low weight is selected as a victim among transactions which caused the deadlock, to solve the problem. If a deadlock occurs between a transaction started in sessions which have higher value for this property and a transaction started in sessions which have lower value for this property, then latter is selected as a deadlock victim. Therefore, set this property according to the priority of each transaction.

Start the transaction after setting this property value so that this value is applied as a weight of that transaction. The transaction weight is not altered if this value is changed after the transaction already has been started.

<a id="ad829fbb24a70f70"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="82d07ca5a7173d8b"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="99a378c8e24c72df"></a>
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

<a id="013b2e5b8eb71ea8"></a>
### Description

It sets whether to create the global secondary index when creating a table in cluster system. A non-deterministic query for the table which did not created the global secondary index fails. The global secondary index can be separately created after creating the table when the property is set to NO.

<a id="1e583e90ced0bf37"></a>
## DEFAULT_INDEX_LOGGING

> It is not supported after 3.2.

<a id="1aaa01a45429f198"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_LOGGING**

<a id="0a67773767463203"></a>
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

<a id="5e4406f975376056"></a>
### Description

If LOGGING property is not explicitly set by a user when an index is created, then it is set to DEFAULT_INDEX_LOGGING value. If an index is created in LOGGING tablespace, the LOGGING property should be set.

<a id="30499f3c25d65366"></a>
## DEFAULT_INDEX_PCTFREE

<a id="8a573c08149c40c9"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_PCTFREE**

<a id="2e9365688a00188c"></a>
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
| Default value | 0 |

<a id="d29614c155a9a6fb"></a>
### Description

If a user does not explicitly specify PCTFREE syntax when creating an index. The PCTFREE is set to DEFAULT_INDEX_PCTFREE property value.

<a id="2b6a2d2f5865783f"></a>
## DEFAULT_INITRANS

<a id="4d6e890ab13fa770"></a>
### Basic Information

**Basic Information of DEFAULT_INITRANS**

<a id="25dc22816fddeb4e"></a>
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

<a id="609fd3b143d1baa6"></a>
### Description

If a user does not explicitly set INITRANS syntax when creating a table or an index, then it is set to DEFAULT_INITRANS property value.

<a id="0cecc83670da09f1"></a>
## DEFAULT_MAXTRANS

<a id="b46dc7386056fd25"></a>
### Basic Information

**Basic Information of DEFAULT_MAXTRANS**

<a id="2a074344b92f7cae"></a>
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
| Default value | 8 |

<a id="bfdad505f407cf0c"></a>
### Description

If a user does not explicitly set the MAXTRANS syntax when creating a table or an index, then it is set to DEFAULT_MAXTRANS property value.

<a id="5a139fc4b65b74f5"></a>
## DEFAULT_PCTFREE

<a id="3f1e8cb59b7de72e"></a>
### Basic Information

**Basic Information of DEFAULT_PCTFREE**

<a id="a911272dbd844f0b"></a>
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

<a id="6788ea99d90da7fe"></a>
### Description

If a user does not explicitly set the PCTFREE property when creating a table, it is set to DEFAULT_PCTFREE property value.

<a id="2fb8c696a4a6c964"></a>
## DEFAULT_PCTUSED

<a id="a6c696624f430913"></a>
### Basic Information

**Basic Information of DEFAULT_PCTUSED**

<a id="94da971e6a1939f8"></a>
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

<a id="7a0546ab00aff4c2"></a>
### Description

If a user does not explicitly set the PCTUSED property when creating a table, it is set to DEFAULT_PCTUSED value.

<a id="1bb366e1643694a1"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="9ceb51eb1018faea"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_BACKUP_FILE**

<a id="cd1be2458627b785"></a>
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

<a id="272d0a9d96f3b417"></a>
### Description

It specifies whether to delete the backup file when deleting the backup list.

<a id="764c942a2d73edbe"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="39a21021c8913893"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST**

<a id="1ae6518c1f228b64"></a>
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

<a id="f9c3b4bf2f141daa"></a>
### Description

It specifies whether to delete the previous obsoleted backup list when executing INCREMENTAL BACKUP.

<a id="94ad7bb7c7a05563"></a>
## DEFAULT_SHARDING

<a id="d9bcda5e9240e5d6"></a>
### Basic Information

**Basic Information of DEFAULT_SHARDING**

<a id="e851bfa93b213045"></a>
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

<a id="1590608c21579859"></a>
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

<a id="36aaa8c8b9b62794"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="b20e906a3c6f6e87"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="c80f105cfd6c9454"></a>
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

<a id="a2243eb3be83ec66"></a>
### Description

It prohibits DDL operation on the table of supplemental log, because it affects CDC's give up.  
For more information, refer to [The table-related DDL causing Replication Give-up](../part-07-replication/48-cyclone.md#07b147d55f0db631).

<a id="644e62e8b4ce59b8"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="d75600688efe29c8"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="b7faccd7d6a6513d"></a>
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

<a id="1dbc11c40fb65560"></a>
### Description

It disables UPDATE primary key which caused CDC give up.

<a id="e509d3e11fdb82c7"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="49020ba37771fa88"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE**

<a id="c1b4cfdc229ea78a"></a>
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

<a id="4db924b344f3edd6"></a>
### Description

It disallows TARGETTYPE protocol.

<a id="2e75519226ae54f9"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="752764a48cbc3636"></a>
### Basic Information

<a id="4ee5fabacf60a920"></a>
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

<a id="fce947adc4c8261d"></a>
### Description

It disallows TARGETTYPE_WITH_ALL protocol.

<a id="6f2d4a972b5cda3e"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="a93afcd5b105916d"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="d120f962bb1250ca"></a>
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

<a id="58b89b8fca583dbe"></a>
### Description

It disallows TARGETTYPE_WITH_NAME protocol.

<a id="1010b478a110db28"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="9e1b80f821480398"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_BUFFER_SIZE**

<a id="7d6923038aea052c"></a>
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

<a id="7906ce0a3ce1439b"></a>
### Description

It is the size of entire communication buffer used in shared mode. It is allocated to and used in Shared Static Area (SSA).

<a id="bf39ff9e722c1e5d"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="614251f8bca2183a"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_UNIT_SIZE**

<a id="6ed2b39c933b50cd"></a>
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

<a id="8e4dab88d98f1cc0"></a>
### Description

It is the unit size managed by dispatcher in shared mode. If the size is large, the memory is wasted. If it is small, the performance is degraded. It is set to the maximum communication packet size in the shared mode.

<a id="7ceceb47d4a78131"></a>
## DISPATCHER_CONNECTIONS

<a id="95828f31a4750cd3"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="7e0ea450c729458f"></a>
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

<a id="afa27a10cbd7c02a"></a>
### Description

It is the maximum number of connection (client) which a dispatcher can manage in shared mode.  
If the system- supported maximum value is smaller than the set value, it is internally set to the system maximum.

<a id="b7ac930af59e001a"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="0edc66e203e29784"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="11fc62ef329a8b5f"></a>
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

<a id="8d68de51e749f329"></a>
### Description

It is the dispatcher dequeue interval for busy waiting. (micro second)

<a id="f0060375fb49981f"></a>
## DISPATCHER_LOAD_BALANCING

<a id="cae33586af5f3107"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="29924fddedddf536"></a>
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

<a id="ec472cc1f7b2fbcc"></a>
### Description

It is an algorithm allocating a dispatcher when connecting to a client in the shared mode.

- 0: It is allocated to a dispatcher of which the number of currently attached clients are small.
- 1: It is sequentially allocated to a dispatcher.

<a id="4e6e09c46390a02a"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="2f82336ab0609e4e"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="6382d38233bff9eb"></a>
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

<a id="4aae6bae33679486"></a>
### Description

It determines NUMA node to which dispatchers are to be connected. This property is operated when NUMA property is set to on.  

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="4a698c738185c6bb"></a>
## DISPATCHER_QUEUE_SIZE

<a id="51694fbd3ee7b60f"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="01e0c693b5b6c7dc"></a>
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

<a id="cb3c2cf79aa4fb5b"></a>
### Description

In shared mode, it sets the queue size for the communication between the dispatcher and the shared-server.

<a id="77baea8b41b3dcd7"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="4e169e68461f41d3"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="e3e0c9e3661d9f52"></a>
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

<a id="52d8cdf32af8fd38"></a>
### Description

It is the count of mini queue per request queue.

<a id="e79f97a9cec3872d"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="cc39dbcd14094e79"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="619e937e415f0d27"></a>
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

<a id="0c4c27e5ed21c61e"></a>
### Description

It is the count of mini queue per response queue.

<a id="24cd3ce23a2b816d"></a>
## DISPATCHERS

<a id="dfd2eb42838f94d2"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="f8775afaf3fe47cb"></a>
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

<a id="0305ce4936a8cbc0"></a>
### Description

It sets the number of dispatcher processes when using the shared mode.  
It can not reduce the value by using alter system on open phase.

<a id="23c167bcaace82cc"></a>
## FETCH_FAILOVER

<a id="5e62caf4e96a2e08"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="72ada2da8e33726a"></a>
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

<a id="d6a53c39c8cfbfe7"></a>
### Description

It enables the fetch failover.

<a id="e872ea7a2e92e6d0"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="045330127be097f4"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="525d7676b06b4d4c"></a>
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

<a id="d84e8f088def1035"></a>
### Description

It sets whether to support the query execution including the session dependent information in the global connection.

<a id="f64ca5f4b043512b"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="9121aa95860b287d"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="fc44e61da1ea0b2e"></a>
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

<a id="71b419199e71587a"></a>
### Description

It is the size of global journal buffer.

<a id="cacb2074d269395e"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="5fc86dcb97d59d56"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="d2e19ebd6ada513c"></a>
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

<a id="1e37d428fbc06d61"></a>
### Description

It is the total max size of global journal buffer.

<a id="0930af3e1fc4745c"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="5824d066895e7f0d"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="e227fd4bebe11ac4"></a>
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

<a id="41828a0282cb8c7c"></a>
### Description

When changing the global property, it performs the lock to control the concurrency. In this case, the waiting time to perform the lock is set.

<a id="94340483f1a591a6"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="31eefbd0d0c57f74"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="1909b63265c5f199"></a>
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

<a id="a63aa5b8c14e243b"></a>
### Description

It is a property to change the commit write mode of the global transaction. TRANSACTION_COMMIT_WRITE_MODE property is applied to all transactions, but GLOBAL_TRANSACTION_COMMIT_WRITE_MODE property is applied only to a global transaction. If the property is set to 2, then it follows the TRANSACTION_COMMIT_WRITE_MODE.

- 0: It does not wait.
- 1: It waits.
- 2: It follows the value of TRANSACTION_COMMIT_WRITE_MODE.

<a id="33751c0e06ecb43f"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="aeead9b4e0da0ed8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="f63e57fc1515213f"></a>
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

<a id="7c64d4b0e9f2be95"></a>
### Description

It determines whether to process the data with a global transaction or with multiple domain transactions when the transaction changed the data through two cluster groups.

- 0: It processes with a global transaction.
- 1: It processes with multiple domain transactions.

> If this property is set to 1, it commits each cluster group with a separate transaction, so it does not guarantees the transaction atomicity.

<a id="eb0cdac4dde425a1"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="860fb03163df9fb4"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="ab3198cb8791e073"></a>
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

<a id="86c7bddf4c0990ef"></a>
### Description

It is the default directory of global transaction log.

<a id="afd5e6ed505ce964"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="35d6aa128c4655e4"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="42826a2e239e6cef"></a>
| Item | Description |
| --- | --- |
| Name | GLOBAL_TRANSACTION_LOG_FILE_SIZE |
| Summary | global transaction log file size |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 20 Mega |
| MAX | 10 Giga |
| Default value | 100 Mega |

<a id="6c922ea3fc46d055"></a>
### Description

It is the file size of global transaction log.

<a id="44d37fbc448f11b2"></a>
## GMASTER_NUMA_NODE

<a id="e71d1e4ff47ce03a"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="6948574bf7e5d81f"></a>
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

<a id="f55fd34812f5c516"></a>
### Description

It sets the ID of NUMA node to be used by gmaster daemon. This property is operated when NUMA property is set to on.

<a id="fe4994faed0e8a01"></a>
## GMON_AUTOSTART

<a id="6de93b4dfb42740a"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="972c42ddfa19a5aa"></a>
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

<a id="6976c7d784873362"></a>
### Description

It sets whether to start gmon process automatically.

<a id="45d66081bfdb5288"></a>
## HINT_ERROR

<a id="f992a4363e8d57a2"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="610e629262b1d018"></a>
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

<a id="4ba4a3869a6b22f6"></a>
### Description

It sets whether to check syntax error and validation error for hint syntax.

<a id="4f50455530b53b3c"></a>
## IDLE_TIMEOUT

<a id="ce9f69d3a94be649"></a>
### Basic Information

**Basic Information of IDLE_TIMEOUT**

<a id="ee15fe5a047840b1"></a>
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

<a id="75dcca79ba8c80aa"></a>
### Description

It sets the maximum IDLE time possible to wait in C/S session. If it exceeds the specified idle time, TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="956ce197690627ef"></a>
## IN_DOUBT_DECISION

<a id="6abbc6b8098d51e2"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="e48c611760d46118"></a>
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

<a id="3d2b32001479bd98"></a>
### Description

It determines whether to commit or to rollback the in-doubt transaction of distributed transactions.

- 1: Commit
- 2: Rollback

<a id="4656d2ae248373f8"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="20455bb0dc1284f7"></a>
### Basic Information

<a id="06cd75ac129964a2"></a>
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

<a id="e475b3314d9dd68c"></a>
### Description

It is the maximum number of values which are targets of *in key range* performing the *in key range scan* based on array.

- IN_KEY_RANGE_ARRAY_COUNT should be 3 or bigger to perform the *in key range scan* based on array for the statement below.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

If the maximum number of in key range target values are bigger than IN_KEY_RANGE_ARRAY_COUNT value, then in key range in key range scan is performed based on instant table.

<a id="d82fc4412501b069"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="33a3af234bb62f2a"></a>
### Basic Information

<a id="096b63f417f69d83"></a>
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

<a id="4ee7b3d067898aff"></a>
### Description

It sets the number of pages to read by one time disk IO for performing incremental backup of the disk tablespace.

<a id="5f4727465a0c7c41"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="98a1669ca9375977"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="0865cb00a5ae9287"></a>
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

<a id="49d117f6bed7cb28"></a>
### Description

When creating an index, it specifies the number of parallel factor.

- 0: It is specified as the number of the core factor in the system.

<a id="9ec86456d6d45402"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="1177e47e84218f3c"></a>
### Basic Information

<a id="20a6fb2ceb1e5f60"></a>
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

<a id="6a3fbdc24b35a924"></a>
### Description

When DML is performed while rebuilding the index on ONLINE mode, the journal data is stored. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal data. INDEX_REBUILD_BLOCK_READ_COUNT sets how much journal data to be read and applied to the index during this process.

<a id="6e663d960d04762f"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="2ae8603258b41701"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="667129ec9a72e901"></a>
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

<a id="dfaaf5b89a97d206"></a>
### Description

When creating an index, it specifies the number of parallel factor to merge the sub-tree.   
If that value is bigger than INDEX_BUILD_PARALLEL_FACTOR, then INDEX_BUILD_PARALLEL_FACTOR is used.

- 0: It follows INDEX_BUILD_PARALLEL_FACTOR.

<a id="3039a5d345c11638"></a>
## INST_ALLOCATOR_COUNT

<a id="65e0229ca4f9bff4"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="321dd9b7bfa9f406"></a>
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

<a id="cc01183a5c5e8dcb"></a>
### Description

This property increases the parallel property of operation allocating or deleting an instant block.

<a id="f45734c6050abcd4"></a>
## INST_TABLE_BLOCK_SIZE

<a id="5900c82f5d2f142b"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="c4eff9b52d13a32a"></a>
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

<a id="024db446df407d20"></a>
### Description

It determines the size of an instant block. If the anchor area of an instant record is bigger than an instant block, then the following error occurs.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="bb228e1fb35a6f6e"></a>
## JOURNAL_TEMP_DIR

<a id="25f8978bcc917f23"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="77f1773a92373030"></a>
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

<a id="60b3271a0ca0f2ec"></a>
### Description

It is the temporary directory of journaling.

<a id="8db6caa2a8494892"></a>
## KEEPALIVE_IDLE_TIME

<a id="76efddeb12970167"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="86ce95ad5843ceb9"></a>
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

<a id="88c5dc19cf4f3898"></a>
### Description

It means the idle duration between the server and client without tcp packet exchange before sending keep alive packet. If there is not tcp packet exchange for seconds (KEEPALIVE_IDLE_TIME), keep alive mechanism starts execution to detect the dead connection on the server side.

<a id="81cb25973587726d"></a>
## LOCAL_CLUSTER_MEMBER

<a id="07527678794261a9"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="5c25dcd9301bb2ce"></a>
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

<a id="e75b4a15fbc13750"></a>
### Description

It is the local cluster member name.

<a id="167290f6ff1f9c94"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="ee2dfda6cd7cee93"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="c7fea8c38594d8f9"></a>
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

<a id="a2192b904ebf0b42"></a>
### Description

It is host name of local cluster member.

<a id="dcb452601b121b4c"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="d2875b0a3ded0bfe"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="0be9c5626b6f361a"></a>
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

<a id="a3e5f9bfa6385b37"></a>
### Description

It is listen port of local cluster member.

<a id="d81171f29580bb58"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="0ea6fe42341ed81d"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="29fc5323f4ef2426"></a>
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

<a id="ea43a2fea8dc750a"></a>
### Description

It is the local journal buffer size.

<a id="faeaa3d44518f1f7"></a>
## LOCATION_FILE

<a id="06c6a963453875e5"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="3a684f02e2bbdd70"></a>
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

<a id="3609ff914323610b"></a>
### Description

It is the location file name.

<a id="11fc47d8eb3dc574"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="82927711c31cb6de"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="b448af7974e54fa9"></a>
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

<a id="f6842b003a41e51f"></a>
### Description

It sets the time (second) waiting for the response after the cluster system enquires of a locator about the solution of split-brain situation. This property is used only when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or more.

<a id="c5d94bf4689ade1c"></a>
## LOCK_HASH_TABLE_SIZE

<a id="ce3fd43048f0700f"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="46bfbe188e19fa5c"></a>
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

<a id="5c1a52a63ab990e7"></a>
### Description

It specifies the maximum hash table size managed by a lock manager.

<a id="9d7cee165bbfc221"></a>
## LOCKLESS_CSERVERS

<a id="e7f216d9316d9bb3"></a>
### Basic Information

<a id="7d1d4fb8bbbc847d"></a>
| Item | Description |
| --- | --- |
| Name | LOCKLESS_CSERVERS |
| Summary | number of lockless cserver processes |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| Default value | 5 |

<a id="9a99fa6921cb63a9"></a>
### Description

It sets the number of cluster server processes performing the operation which does not acquire the lock. The number of cluster server processes performing the operation which acquires the lock is set by using [CSERVERS](#22dfbbb764c3ce6d).

<a id="e2b1d0f199c06141"></a>
## LOG_BLOCK_SIZE

<a id="f0d3a8dd757a5684"></a>
### Basic Information

**Basic Information of LOG_BLOCK_SIZE**

<a id="9afb590666c5dfdd"></a>
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

<a id="5e8bb85d6a0fb4fd"></a>
### Description

It means the minimum size of what log buffer is flushed to the log file of the disk. Its value should be set to one of 512, 1024, 2048, 4096.

<a id="a2733ceba2c4f693"></a>
## LOG_BUFFER_SIZE

<a id="691a20bfd5c154d0"></a>
### Basic Information

**Basic Information of LOG_BUFFER_SIZE**

<a id="df9e2be74a2a21f8"></a>
| Item | Description |
| --- | --- |
| Name | LOG_BUFFER_SIZE |
| Summary | default log buffer size (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| Default value | 10485760 |

<a id="1423103f20973231"></a>
### Description

A log buffer is the shared memory space in which the redo logs generated in database by the DML/DDL operations are stored. LOG_BUFFER_SIZE is referenced to set the memory size for the log buffer.

<a id="aaed0cb2b06df90a"></a>
## LOG_DIR

<a id="e0b2d4b438c198eb"></a>
### Basic Information

**Basic Information of LOG_DIR**

<a id="9ab405f7ed7e1cef"></a>
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

<a id="60a9bda6cb2dcb00"></a>
### Description

The log recorded in the log buffer is flushed to the logfile which exists in a non-volatile storage device to ensure the database durability. LOG_DIR sets the path to the log file.

<a id="18a7ce336fdf355d"></a>
## LOG_FILE_SIZE

<a id="3639c47c4a9c790a"></a>
### Basic Information

**Basic Information of LOG_FILE_SIZE**

<a id="4763aae7bbcb8bb8"></a>
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

<a id="6fbd2db224613fcb"></a>
### Description

It sets the size of the logfile used in database. It is referenced only when creating the database, then log file size can not be updated after then.

<a id="09e398e7169aaa04"></a>
## LOG_GROUP_COUNT

<a id="d4a1e9b108571aa8"></a>
### Basic Information

**Basic Information of LOG_GROUP_COUNT**

<a id="1bd7fbe37ae717b4"></a>
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

<a id="47674964a34a25c1"></a>
### Description

It sets the number of log group used in database. It is referenced only when creating the database, but after that, it does not affect any operations. After creating database, the operation to add or remove a log group is supported by a separate syntax.

<a id="8f546c76ae6ddd2a"></a>
## LOG_MIRROR_MODE

<a id="9123e4b4f8a38242"></a>
### Basic Information

**Basic Information of LOG_MIRROR_MODE**

<a id="f63b85902453ddd7"></a>
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

<a id="eb13a1f21d6f3d24"></a>
### Description

It is the property to configure the required shared memory when operating LogMirror, the redo log replication tool, at database startup.  
It should be enabled to execute the LogMirror.  
The size of the shared Memory can be changed using LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE.

<a id="10fe01bdde6e6500"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="f6996c69c7cb4df4"></a>
### Basic Information

**Basic Information of LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE**

<a id="ca6867c918f95fe3"></a>
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

<a id="3b088aac5daa2948"></a>
### Description

It sets the size of the shared memory used in LogMirror, the redo log replication tool.   
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="12e6457ea12c4288"></a>
## LOG_MIRROR_TIMEOUT

<a id="60c09926db78639e"></a>
### Basic Information

**Basic Information of LOG_MIRROR_TIMEOUT**

<a id="66d1c96e0f9fb2c5"></a>
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

<a id="64e763a770ef8e68"></a>
### Description

It is the response waiting time of the LogMirror.   
If its value is 0, it waits indefinitely. Otherwise, it waits as long as the value set, then TIMEOUT occurs, and it stops LogMirror service. Later, the server is operated normally.  
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="eb59dd80718bff39"></a>
## LOG_SYNC_INTERVAL

<a id="6e51cef54bdc7e83"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="fd18cd5f5657ec87"></a>
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

<a id="e5b84fbd963fda34"></a>
### Description

Log flusher of GOLDILOCKS is a system thread which flushes the log buffer contents to disk logfile. When log flusher wakes up in the idle phase, it checks if log to flush exists. Then it flushes the log if any.  
If the log flusher did not flush within the time set in LOG_SYNC_INTERVAL, it synchronizes the log buffer and the log file by performing a flush until the last block of the current log buffer.

<a id="01329ec2bc5a9674"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="976e52f7a6b44174"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="5577ef8b317ef5b4"></a>
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

<a id="07de34ff63a8ebb7"></a>
### Description

It is the millisecond interval for synchronize log.

<a id="9b1e62e3acd5205a"></a>
## MAX_GROUP_COUNT

<a id="21a5895839099efe"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="7b660d8f0310bbfe"></a>
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

<a id="e914eaa6e1a383c8"></a>
### Description

It is the maximum group count.

<a id="096ee63507807de1"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="81447feacfb4cfc0"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="6f8a49fcd936c5b4"></a>
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

<a id="17555124d50f569d"></a>
### Description

It sets the maximum size (quota) of the global journaling file which internally stores journaling data when a journaling occurs in cluster system.

<a id="9273a767f8a189ab"></a>
## MAX_NODE_COUNT

<a id="3d88c37a7cab2309"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="5143d9e556c1ae81"></a>
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

<a id="501b690169ea0fd6"></a>
### Description

It is the maximum node count.

<a id="9583b028f1eacaf9"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="9f2f05bffa85f8b1"></a>
### Basic Information

**Basic Information of MAXIMUM_CONCURRENT_ACTIVITIES**

<a id="ee5c70490c784b33"></a>
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

<a id="263529de3c08a532"></a>
### Description

It sets the number of statements which can be executed simultaneously.

<a id="4b4d270cc8e84c05"></a>
## MAXIMUM_FLANGE_COUNT

<a id="2fd3edce37b579ee"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="3b27a8142348054d"></a>
| Item | Description |
| --- | --- |
| Name | MAXIMUM_FLANGE_COUNT |
| Summary | maximum flange count in a plan clock |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 128 |
| MAX | 65535 |
| Default value | 1024 |

<a id="d0c023bcf2a44b6d"></a>
### Description

It is the maximum number of flanges which can be expanded in plan clock.

<a id="21132e1b293b83b1"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="c73c0d3b6438ae7f"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="3c34cf8c6a625a02"></a>
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

<a id="612dd345703904fb"></a>
### Description

When flushing the contents of the log buffer to disk log file, it sets the maximum number of log blocks to be flushed with a single writing operation.

<a id="28df54a5bdb5899a"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="4df1300de9e6d6f1"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_PAGE_COUNT**

<a id="ae0d24109bf442e3"></a>
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

<a id="3faa84dc3ab27f1a"></a>
### Description

GOLDILOCKS datafiles are flushed to the disk by the checkpoint and certain DDL statements. For flushing datafiles, it sets the maximum number of data pages to be flushed with a single writing operation.

<a id="a25c8da35a9a6e97"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="666ac287227abcee"></a>
### Basic Information

<a id="df82aa95c0e3c3eb"></a>
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

<a id="8b77bc27741aae12"></a>
### Description

When rebuilding the index on ONLINE mode, it can be performed together with DML, and DML records the updates on the journal log. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal log. The journal logs are initially applied, then journal logs which were accumulated while applying the journal logs are applied. This property sets how may times the journal logs are applied in this way.

<a id="32bab96e1c5790db"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="ed7d1ab5c5ac30be"></a>
### Basic Information

<a id="8aa2a0a376741e8f"></a>
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

<a id="9d80eda18b2594e8"></a>
### Description

The table rebalancing online can be performed together with DML in the cluster environment, and DML records the updates on the journal log at that moment. The table rebalancing initially applies the journal logs which occurred during synchronizing tables, then applies journal logs which were accumulated while applying the journal logs. This property sets how may times the journal logs are applied in this way.

<a id="5dc16e9bfc3845c5"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="c94bc30208d391c9"></a>
### Basic Information

**Basic Information of MAXIMUM_NAMED_CURSOR_COUNT**

<a id="b3772ec9b2b33dfc"></a>
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

<a id="6af7b23f329b2259"></a>
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

<a id="62f4d4b60f75e6e2"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="7387558515a91d36"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="e2d295bb6144ecf6"></a>
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

<a id="f8486632396efd8f"></a>
### Description

It sets the maximum buffer size available in a single session which is connected to shared mode.  
For more information, refer to [DISPATCHER_CM_BUFFER_SIZE](#1010b478a110db28).

<a id="c78df464e48cef8c"></a>
## MEASURE_CLUSTER_LATENCY

<a id="7e2bd7510ab2a1dd"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="ad8e3f4740a27364"></a>
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

<a id="e969c4c3980580a7"></a>
### Description

It is the measure cluster latency.

<a id="f340bd1fe0b92c2f"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="cd813c370ea669d2"></a>
### Basic Information

**Basic Information of MEMORY_MERGE_RUN_COUNT**

<a id="958f7b4528aa5908"></a>
| Item | Description |
| --- | --- |
| Name | MEMORY_MERGE_RUN_COUNT |
| Summary | merge run count for memory index |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 2 |
| MAX | 64 |
| Default value | 32 |

<a id="1c8c8dafab973a2b"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in certain block size (MEMORY_SORT_RUN_SIZE) units, merging the sorted blocks, and generating the internal node. MEMORY_MERGE_RUN_COUNT sets the number of the sorted blocks to be merged at a time.

<a id="b021886121bf4e8e"></a>
## MEMORY_SORT_RUN_SIZE

<a id="c22ab024cfe31887"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="68370c904fd930cc"></a>
| Item | Description |
| --- | --- |
| Name | MEMORY_SORT_RUN_SIZE |
| Summary | sort run size for memory index (byte) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | TRUE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 8192 |
| MAX | 32768 |
| Default value | 8192 |

<a id="ae9157e1b9b06400"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in a certain block size (MEMORY_SORT_RUN_SIZE) unit, merging the sorted blocks, and generating the internal node. MEMORY_SORT_RUN_SIZE sets the size of a single block to be sorted.

<a id="1a0a3d03d160a50c"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="c78531cc26efae0a"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="8508f9b0639e1709"></a>
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

<a id="d9ed8d8ccbc35ee5"></a>
### Description

It is the minimum number of sampling rows when executing [ANALYZE TABLE](../part-03-sql-manual/18-sql-references.md#219201f7a44b0188) by using the sampling.

<a id="f1fd90f22de4c8c6"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="8e226280fd00958a"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="c017911c1a562384"></a>
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

<a id="82d2d0289ad8e685"></a>
### Description

DML uses the undo page to store the previous image. Undo page is consumed by using a single undo segment per DML. If all allocated pages of undo segments are consumed, the page of another undo segment can be used. MINIMUM UNDO PAGE_COUNT is the minimum number of undo page to specify the undo segment to import page when undo pages are insufficient. If the undo pages are insufficient, the pages can be imported only from the undo segment having more pages than MINIMUM UNDO PAGE_COUNT.

<a id="b751118f3582f51f"></a>
## NET_BUFFER_SIZE

<a id="cc2f82a7ab47d80a"></a>
### Basic Information

**Basic Information of NET_BUFFER_SIZE**

<a id="132d940159dc1192"></a>
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

<a id="a58a096be2bc0c72"></a>
### Description

It sets the TCP communications buffer size.   
In the dedicated mode, it is set to the maximum communication packet size.  
In the shared mode, it is set to [DISPATCHER_CM_UNIT_SIZE](#bf39ff9e722c1e5d).

<a id="60cec08fdb546878"></a>
## NLS_DATE_FORMAT

<a id="79199e48cfb5a527"></a>
### Basic Information

**Basic Information of NLS_DATE_FORMAT**

<a id="93b6e7bce87e8571"></a>
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

<a id="800c64e99f9c4ae2"></a>
### Description

NLS_DATE_FORMAT specifies the default date format of TO_CHAR and TO_DATE functions.

<a id="d04abb17d05e3a69"></a>
## NLS_TIME_FORMAT

<a id="49a94e87441cf1ec"></a>
### Basic Information

**Basic Information of NLS_TIME_FORMAT**

<a id="73a349a5385d048f"></a>
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

<a id="8f90b598d7c35fcd"></a>
### Description

NLS_DATE_FORMAT specifies the default time format of TO_CHAR and TO_DATE functions.

<a id="74c3e90b61fe6686"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="d30228c73b88713c"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="fe15d7f7cd90aef6"></a>
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

<a id="9cba8db2076fbdde"></a>
### Description

NLS_TIME_WITH_TIME_ZONE FORMAT specifies the default time with time zone format of TO_CHAR and TO_TIME_WITH_TIME_ZONE functions.

<a id="c7bd2aeb63024fb5"></a>
## NLS_TIMESTAMP_FORMAT

<a id="cafca834cb18f4dc"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="4e4d9634c8eb135c"></a>
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

<a id="adb531551840cf4b"></a>
### Description

NLS_TIMESTAMP_FORMAT specifies the default timestamp format of TO_CHAR and TO_TIMESTAMP functions.

<a id="3de636e485510342"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="06ec1429163a0adc"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="65569e57b68fa2eb"></a>
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

<a id="be3373b29ba3014b"></a>
### Description

NLS_TIMESTAMP_WITH_TIME_ZONE FORMAT specifies the default timestamp with time zone format of TO_CHAR and TO_TIMESTAMP WITH TIMEZONE functions.

<a id="8bb412e378c50ce1"></a>
## NUMA

<a id="e1489110ac80950d"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="fa7d6f75408a5d84"></a>
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

<a id="0132169e68bb448e"></a>
### Description

It enables NUMA.

> To use the NUMA property in AIX, the user account should be modified. Execute the following command as a root user.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> &lt;username&gt; is not a root but it is a user account of AIX.  
> Logout then login again to apply the modifications.

<a id="01ee48e7da3392ee"></a>
## NUMA_MAP

<a id="664ab5a124715489"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="565ada413fee4f4a"></a>
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

<a id="f14bd33789c71f7b"></a>
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

<a id="3cb11336c71c7834"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="73442110821be088"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="c3a154f24b63fade"></a>
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

<a id="18c0567309174ebc"></a>
### Description

The background process automatically takes the errored member offline after completing the failover caused by the node error.   

If it is not possible to take the errored member offline because it is set to *NO*, then execute the following syntax before the errored member joins the system again.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="fd7d6cab4b02feac"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="c24719c8058fbcb7"></a>
### Basic Information

<a id="32bd6ef0f9e27c33"></a>
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

<a id="f9fa33dc2500cb0b"></a>
### Description

DML performed during rebuilding the index on ONLINE mode records the journal log. The journals are applied to the index multiple times when finishing rebuilding the index. [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#a25c8da35a9a6e97) sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="80ff3c60945f5b80"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="953757525b2faae9"></a>
### Basic Information

<a id="c7ab2cfe841a183d"></a>
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

<a id="0a49f89d949f4aaa"></a>
### Description

The table rebalancing online applies journal logs several times which were recorded by dml occurred during the performance in the cluster environment. MAXIMUM_JOURNAL_REPLAY_COUNT sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="136265a47857e4e6"></a>
## OS_GROUP_ACCESS

<a id="4dc6369f36a833f8"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="1a824287a6a2d6ed"></a>
| Item | Description |
| --- | --- |
| Name | OS_GROUP_ACCESS |
| Summary | enable access database with OS group permission |
| Data type | BOOLEAN |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| Default value | NO |

<a id="65f8dd9e5cf4a223"></a>
### Description

To connect to DA with another user of the same group, this property should be set to *YES*. Also, the umask of the system should be modified to *0002*.

<a id="89c2351181bc2e95"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="4972c64ed1b7893f"></a>
### Basic Information

<a id="4b26ac25c63a69ae"></a>
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

<a id="bda6b69a6949d79b"></a>
### Description

If the data size to be sent to the client is bigger than PACKET_COMPRESSION_THRESHOLD, it compresses the communication data.

<a id="d45c15cda9031d6b"></a>
## PAGE_CHECKSUM_TYPE

<a id="10b12749466cc49e"></a>
### Basic Information

**Basic Information of PAGE_CHECKSUM_TYPE**

<a id="7387e12d3256eab5"></a>
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

<a id="c337242ec2c043e5"></a>
### Description

A checksum is used to guarantee the physical consistency for each page of the datafile. GOLDILOCKS supports a page checksum of LSN, CRC scheme.

- 0: LSN
- 1: CRC

<a id="9b37933d1e325c77"></a>
## PARALLEL_IO_FACTOR

<a id="67c716ca25d0250a"></a>
### Basic Information

**Basic Information of PARALLEL_IO_FACTOR**

<a id="200669c2e744e996"></a>
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

<a id="e140f04241ce28d3"></a>
### Description

It sets the number of threads for the parallel loading of data file when starting database and the number of threads for parallel recording of data file at checkpoint.

<a id="361977d7e0b21f7c"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="7f3e0b1912bdb63d"></a>
### Basic Information

**Basic Information of PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16**

<a id="f02e770f996079b1"></a>
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

<a id="59b7f7a258ae9de4"></a>
### Description

It sets the group directory for parallel I/O of data file. It sets the number of group as many as PARALLEL_IO_FACTOR, then parallel I/O is performed in data file unit which belongs to each group.

<a id="b3008a1c8bab9dc8"></a>
## PARALLEL_LOAD_FACTOR

<a id="03f8147594ad7f0a"></a>
### Basic Information

**Basic Information of PARALLEL_LOAD_FACTOR**

<a id="d1bce80c34e58032"></a>
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

<a id="a0a136f742a9069a"></a>
### Description

When starting database, it sets the number of threads for parallel operation after loading the memory of a data file.

<a id="8a0e5964e6a2361e"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="6ee1972759ef4446"></a>
### Basic Information

**Basic Information of PENDING_LOG_BUFFER_COUNT**

<a id="878b7fcab6770a1d"></a>
| Item | Description |
| --- | --- |
| Name | PENDING_LOG_BUFFER_COUNT |
| Summary | default pending log buffer count |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 0 |
| MAX | 32 |
| Default value | 4 |

<a id="45d7c4b9885e0b26"></a>
### Description

When multiple transactions are simultaneously running, the pending log buffer is used to reduce the competition for the log buffer. PENDING LOG_BUFFER COUNT sets the number of pending log buffer which can be used simultaneously.

<a id="5c0788a1c530d348"></a>
## PLAN_CACHE

<a id="104e2e8db1b44f89"></a>
### Basic Information

**Basic Information of PLAN_CACHE**

<a id="a58b62fcdc367059"></a>
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

<a id="8e71c38fd3410232"></a>
### Description

It determines whether to use the plan cache.

<a id="ef0cca938c856c3f"></a>
## PLAN_CACHE_SIZE

<a id="d38b68bcb733de02"></a>
### Basic Information

**Basic Information of PLAN_CACHE_SIZE**

<a id="746501fd4486ab49"></a>
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

<a id="ab233e841ec7418c"></a>
### Description

It sets the memory size to be used for the plan cache.

<a id="4746612d327d9a90"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="62fe01b1f986b848"></a>
### Basic Information

<a id="aaefd978b9230d24"></a>
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

<a id="b9e73fbed6a87a0e"></a>
### Description

It sets the initial size of the heap memory to use in the session. Even when there are memories which are not used in the session, the memories are not returned to operating system.

<a id="10cf87c76ee80f11"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="7e78d9ba2532257b"></a>
### Basic Information

<a id="479f52d871407108"></a>
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

<a id="d66f15381fa8742e"></a>
### Description

It sets the size of memory to extend when the session allocates additional heap memory.

<a id="2e15415517a51a84"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="1c78f920373fc4de"></a>
### Basic Information

<a id="2bf3bc22e553f3a4"></a>
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

<a id="d6717b4d19330b2d"></a>
### Description

The memory size is preserved as big as this property even when there are unused heap memories in the session, and those memories are not returned to the system but are reused in the session.

Even when it is set to smaller than PRIVATE_STATIC_AREA_INIT_SIZE, it is not decreased to smaller than the size.

<a id="cce12a09332c588d"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="20457e32efab2f68"></a>
### Basic Information

**Basic Information of PRIVATE_STATIC_AREA_SIZE**

<a id="9175e903ec3b858c"></a>
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

<a id="d84dbd73d020a03a"></a>
### Description

It specifies the maximum heap memory size to be allocated by the session.

<a id="1f004a54c1d9d82e"></a>
## PROCESS_MAX_COUNT

<a id="59415a59b151a7da"></a>
### Basic Information

**Basic Information of PROCESS_MAX_COUNT**

<a id="9160e163ba2af948"></a>
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

<a id="3c5c00e2ec9e5feb"></a>
### Description

It specifies the maximum number of processes (threads) available on the system.

Creating system process  
• The process is created each time of connection to D/A mode or C/S dedicated mode.  
• In C/S shared mode, processes are basic balancer, dispatcher and shared-server. A process is   
&nbsp;&nbsp;not created when connecting from client.

<a id="9c8eb68123ca4add"></a>
## QUERY_TIMEOUT

<a id="7210b8f4e9d478f5"></a>
### Basic Information

**Basic Information of QUERY_TIMEOUT**

<a id="95e13eaf68bdafc5"></a>
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

<a id="424013bacf0cbead"></a>
### Description

It specifies the maximum time which a command received from the session can be executed. If the execution time exceeds, the TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="35e6dd2211838035"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="0e3dcd642d20df06"></a>
### Basic Information

**Basic Information of READABLE_ARCHIVELOG_DIR_COUNT**

<a id="b56e024b2a1c8925"></a>
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

<a id="a98b4231087e5c68"></a>
### Description

It sets the number of directories in which archive redo logs exist when executing media recovery.

<a id="20e34f0df807d01a"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="83e4117f37db531a"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="72335efcdc9c170e"></a>
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

<a id="fea487314c5e53eb"></a>
### Description

It sets the number of directories in which incremental backups exist when restoring files using incremental backups.

<a id="b4a29916dafa188b"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="d5b66bb9c048e529"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="5ba2836793e32d73"></a>
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

<a id="fa33eea7f31c94c8"></a>
### Description

It is the block read count for rebalance.

<a id="90f53012f41fba12"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> It is not supported after 3.1.

<a id="1b20b1fbbe4ac319"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="f4131313c9aab66e"></a>
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

<a id="780e9154fbf20e67"></a>
### Description

It sets the minimum page count to check if the plan is recompiled due to the page count modification.

<a id="c69d7273a1488ba9"></a>
## RECOMPILE_PAGE_PERCENT

> It is not supported after 3.1.

<a id="e52d98ee0b5e0bc7"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="e2c390b193f453fa"></a>
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

<a id="f339be7797b66b48"></a>
### Description

It sets the page percentage when recompiles the plan due to the page count modification. If its value is 0, it does not recompile due to the page count modification.

<a id="eaec5a292f2ccdee"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="28797d58b1b411d0"></a>
### Basic Information

<a id="a3976a88d7daaaf3"></a>
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

<a id="5b9348fa96aff31c"></a>
### Description

It is the default log buffer size for recovery.

<a id="66227b4a108abd8d"></a>
## RECYCLEBIN

<a id="61be93ada6ca602d"></a>
### Basic Information

<a id="bfe4d63a0437fea5"></a>
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

<a id="c15bbf2126043e1f"></a>
### Description

It sets whether to activate the recyclebin feature.

<a id="7d7c66aade580fc0"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="44c0d3eab405e3d9"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="9afc4a7b129865c3"></a>
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

<a id="e1bcff297606450b"></a>
### Description

If the size of the created REDO LOG is bigger than REDO_LOG_COMPRESSION_THRESHOLD value, it compresses REDO LOG.

<a id="19492a839372dbf7"></a>
## REFINE_RELATION

<a id="2c7924b4de6d571f"></a>
### Basic Information

<a id="e410299fba9f7a51"></a>
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

<a id="cff3fa8d3feb933e"></a>
### Description

If this property is set to NO, then REFINE RELATION process is not performed when restarting the server.

This property can be used when an error occurs during the REFINE RELATION process. However, segments of RELATIONs (tables or indexes) which were dropped but not REFINEd can not be reused. When resolving the error then setting this property to YES and restarting, it tries to REFINE relations which were not dropped.

<a id="1ac8aaf300c648c3"></a>
## SESSION_FATAL_BEHAVIOR

<a id="06e501a98bc7c18b"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="6baefca7924f0c74"></a>
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

<a id="9daa9a561560e27c"></a>
### Description

When session fatal occurs, it determines whether to terminate only the thread which caused the fatal or to terminate the process.

- 0: It terminates only the thread which caused fatal.
- 1: It terminates the process.  
  If multiple sessions are simultaneously performed in the process, the process is terminated after all sessions finish using database.

<a id="5a66573dcabc4ca1"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="69b7baba6622776d"></a>
### Basic Information

<a id="6919c2ebca794621"></a>
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

<a id="1024953150c9fdc8"></a>
### Description

It sets the shared memory size to be allocated in advance so that it can be used in the session.

<a id="fdc6e73c8d8676c3"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="86a37b00185e1139"></a>
### Basic Information

<a id="e533c3d572b7dc72"></a>
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

<a id="e20a183c710f33e1"></a>
### Description

It sets the threshold value to determine whether to return the dynamic shared memory which is not used by the session to the system when releasing the dynamic shared memory used in the session. In other words, if the memory chunk which is bigger than the set value among unused memory exists, then it is returned to the system.

<a id="508a8ce6be092192"></a>
## SHARED_MEMORY_ADDRESS

<a id="eb7743a505d29572"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_ADDRESS**

<a id="d5d3bbed7032729f"></a>
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

<a id="e4be1db9a34397c4"></a>
### Description

It specifies the address of Shared Static Area (SSA).

<a id="c9cceee33d7bae5f"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="b221ae8481a86d13"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_KEY**

<a id="118825a0ed6e9ce3"></a>
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

<a id="0fc6532c61ac24e7"></a>
### Description

When running server, it specifies the shared memory key values which are used to allocate Static Shared Area (SSA) space.

<a id="3f4dfbe3ff7b6277"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="7b2fbf4ab3289f2f"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_NAME**

<a id="656a657f1cf29892"></a>
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

<a id="7fe21849dce12708"></a>
### Description

When running server, it specifies the shared memory name which is used to allocate Static Shared Area (SSA) space.

<a id="d0d212d5b93cb3bd"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="0724fe64e7615e83"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_SIZE**

<a id="138fc299f2527dac"></a>
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
| Default value | 763363328 |

<a id="8e2c380610e3601b"></a>
### Description

It specifies the size of the Shared Static Area (SSA).

<a id="e7579e8eae44d652"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="4553e00a42dd29c0"></a>
### Basic Information

**Basic Information of SHARED_REQUEST_QUEUE_COUNT**

<a id="b888877080f84a6b"></a>
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

<a id="9d5ef255212b65bd"></a>
### Description

In shared mode, it sets the number of queues of which the dispatcher requests to the shared-server. A queue is used when multiple dispatchers allocate user's requests to the shared-server. Generally, a single queue is used for the load-balance.   
However, SHARED_REQUEST_QUEUE_COUNT value is increased because if the number of dispatchers and shared-servers increase, then a conflict to the queue causes performance degradation.   
If the value becomes bigger, the load-balance can be inefficient and the possibility of deadlock increases.

<a id="a78837c4ec1162c4"></a>
## SHARED_SERVERS

<a id="a287630d04f17832"></a>
### Basic Information

**Basic Information of SHARED_SERVERS**

<a id="35b8d294e081ebd6"></a>
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

<a id="c0d3dc1d650b5be4"></a>
### Description

It sets the number of shared-server processes on shared mode.  
At open phase, the value can not be decreased by using alter system.

<a id="84370adae9867df2"></a>
## SHARED_SESSION

<a id="0894924d3172a284"></a>
### Basic Information

**Basic Information of SHARED_SESSION**

<a id="9c094a2f390b3ef2"></a>
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

<a id="01df90436bfd2c35"></a>
### Description

It sets whether to activate shared mode. If the value is set to *NO*, load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver) are not executed.

<a id="c543a79bbcb8d3af"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="8d853d94ed1fe4de"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="a58f49968a07b6bb"></a>
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

<a id="06316e6a0d71ed90"></a>
### Description

It sets the maximum holding time of the statement required for the snapshot read. TIMEOUT error occurs for a snapshot statement which exceeds the time.

<a id="5a55d1aa3cbfc4a4"></a>
## SQL_HISTORY_SIZE

<a id="667f14dff5f805f0"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="879f33e606238436"></a>
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

<a id="bb4916466dd2a501"></a>
### Description

It is the history size for SQLs.

<a id="81754a03e0765e5a"></a>
## SQL_HISTORY_TYPE

<a id="29ff25866bc52acb"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="60ef4dcd57eb5eba"></a>
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

<a id="42611269e0fc2161"></a>
### Description

It is the history type for SQLs.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="5b3e5cb1d5e5c5b7"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="8a9fae9946130a49"></a>
### Basic Information

**Basic Information of SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY**

<a id="3c454b6ccd2452fc"></a>
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

<a id="db0f213c5f709df8"></a>
### Description

It records supplemental log for all changes in the database.

<a id="97522be350b538cc"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="a3b94db28368d250"></a>
### Basic Information

<a id="57bf76500f213f2e"></a>
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

<a id="03e43e444a327c3f"></a>
### Description

It sets the initial DISK_DATA_TBS tablespace size when creating the database.

<a id="9ccf60f6958d9c3a"></a>
## SYSTEM_FILE_IO

<a id="6f1dd8984297f9c2"></a>
### Basic Information

<a id="2d38ca1c9c657477"></a>
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

<a id="86163b5808d4406c"></a>
### Description

It sets IO type of when using the database file except for the data file and the log file.

<a id="3bd4d96a69b626d9"></a>
## SYSTEM_LOGGER_DIR

<a id="ee3c4cfc19a9914e"></a>
### Basic Information

<a id="a0a7a45bb050b0ca"></a>
| Item | Description |
| --- | --- |
| Name | SYSTEM_LOGGER_DIR |
| Summary | system logger directory |
| Data type | VARCHAR |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/trc |

<a id="b36e4b0f655bd063"></a>
### Description

It sets the disk path on which the trace log message is recorded.

<a id="735ddf8b80e83b18"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="1f80ccc74b7ecc8c"></a>
### Basic Information

<a id="02db61cef3f5cbbb"></a>
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

<a id="cad10730783ba4d0"></a>
### Description

It determines the size of initial MEM_AUX_TBS tablespace when creating the database.

<a id="b974e3aef9038834"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="a45fe77137c0ec00"></a>
### Basic Information

<a id="b5033f8dcaef0dcc"></a>
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

<a id="f5ba2cf21c14631b"></a>
### Description

It determines the initial tablespace size of MEM_DATA_TBS when creating database.

<a id="29399bc205e2bdc0"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="9913b506a1a7251c"></a>
### Basic Information

<a id="8a8fe093e1cb1eba"></a>
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

<a id="6f7f3af7d6d0b816"></a>
### Description

It determines the initial tablespace size of DICTIONARY_TBS when creating database.

<a id="d1056e1631a19521"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="33bb958505ae6ecd"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE**

<a id="c09c20e460f317e0"></a>
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

<a id="f946a40cf2215897"></a>
### Description

It determines the initial tablespace size of MEM_TEMP_TBS when creating database.

<a id="f0e2bded972c8e6d"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="7fcb7bdc9fff5c5b"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE**

<a id="83cee8bd38fb725e"></a>
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

<a id="d3b8c3e6269b2908"></a>
### Description

It determines the initial tablespace size of MEM_UNDO_TBS when creating database.

<a id="316f8a44b8e4be82"></a>
## SYSTEM_TABLESPACE_DIR

<a id="3ebb37c3c9b50fc5"></a>
### Basic Information

<a id="51c2d60d857c7e69"></a>
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

<a id="823c8d26ce46c87a"></a>
### Description

It sets the path to which the initial system tablespaces are stored when creating database.

<a id="102740a86dcbf3f5"></a>
## SYSTEM_UDS_DIR

<a id="a951811d73ff6991"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="f9e594f294dc44c7"></a>
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

<a id="44231ca510bf2d7e"></a>
### Description

It sets a directory on which the unix domain socket file is created.  
Setting the directory for the unix domain socket except for DB system, such asglsnr, is managed by a separate configuration file.  
The maximum setting value is 60 bytes. (The maximum size of the absolute path (directory + file name) for the unix domain socket file varies according to OS, but generally it is around 100 bytes.)

<a id="48e403e293b3aa8b"></a>
## TCP_CLIENT_NUMA_NODE

<a id="95ea1c985e44f1be"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="751f38d8e3b7a298"></a>
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

<a id="26b62349fdefbbce"></a>
### Description

It sets the NUMA node ID to which the client server session is bound. This property is operated when NUMA property is set to on.

<a id="2af6f6026a24817c"></a>
## TCP_NODELAY

<a id="ee3de00942080286"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="5e46aeb945b5d20d"></a>
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

<a id="1d88b92ee6311e49"></a>
### Description

It sets TCP_NODELAY option of the socket when transferring the data to a client in C/S method (TCP socket).  
Set it to *NO* when fast latency is not required and reducing the network load is needed.

<a id="594cc19efde52dde"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="1735725bd25ac60f"></a>
### Basic Information

<a id="80ed4da496be65b6"></a>
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

<a id="fdce1d93fcbb803f"></a>
### Description

It sets the number of segments to be cached in a session instead of returning them to a tablespace when dropping a global temporary table or a global temporary index segment. Segments in the segment cache are reused later in a global temporary table or a global temporary index.

- 0: It does not use a segment cache of a global temporary table or of a global temporary index in a session.
- 1 ~ 4294967295: It keeps the specific number of segment caches of a global temporary table or a global temporary index in a session.

<a id="65d781e2a3f1a6a7"></a>
## TEMP_UNDO_ENABLED

<a id="530bed7542b02a92"></a>
### Basic Information

<a id="c5b146bab7621a18"></a>
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

<a id="3f03ece1a3a4146f"></a>
### Description

It defines the location of logging undo records for a global temporary table.

- 0 (FALSE): It records the undo records in the default undo tablespace of database. 
- 1 (TRUE): It records the undo records in the default temporary tablespace of database.

<a id="5c98d628d5cbd739"></a>
## TIMED_STATISTICS

<a id="4cbfbd12ee262cc1"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="f8b6995d196f4185"></a>
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

<a id="6f60025b9ab4375d"></a>
### Description

It is whether to check the wait event.  
To record the statistics related to wait event on v$system_event, v$session_event and v$session_wait table, set this property.

- 0: It does not record the statistics.
- 1: It records the statistics.
- 2: It records the statistics by using the high precision timer.

<a id="0211eda8f9578dfb"></a>
## TIMEZONE

<a id="7b28ea7882b5c4d8"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="1f416890b05371b9"></a>
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

<a id="bfed584b509129c7"></a>
### Description

It is a time zone value of database.  
It is applied when creating database, and it uses the value of the range from '-14:00' to '+14:00'.

<a id="cdef9ebf87967b9c"></a>
## TRACE_ALTER_SYSTEM

<a id="63c0ea70ab965482"></a>
### Basic Information

**Basic Information of TRACE_ALTER_SYSTEM**

<a id="188a55eee2e76fe9"></a>
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
| Default value | NO |

<a id="97354e98114fa29e"></a>
### Description

It records the SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) when executing ALTER SYSTEM syntax.

Set TRACE_ALTER_SYSTEM property to *ON* to record system changes.

SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax have nothing to do with TRACE_ALTER_SYSTEM property, so they do not affect the performance of TRACE_ALTER_SYSTEM.

<a id="34b645f038634f61"></a>
## TRACE_DDL

<a id="7d732f3ecfc5934a"></a>
### Basic Information

**Basic Information of TRACE_DDL**

<a id="60bbaa69fcac74a8"></a>
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
| Default value | NO |

<a id="46fad487a9692420"></a>
### Description

When executing DDL, it records the executed SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

Set *TRACE_ALTER_SYSTEM* property to *ON* to record SQL statements execution such as CREATE/DROP/ALTER table.

TRACE_DDL property affects only to DDL statements. However, it has nothing to do with SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax. Therefore, it does not affect the performance.

<a id="6bf8e2abffa689a8"></a>
## TRACE_LOG_ID

<a id="2ee07b36459fe669"></a>
### Basic Information

**Basic Information of TRACE_LOG_ID**

<a id="5826d6829436783f"></a>
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

<a id="b935a3005d866bd4"></a>
### Description

The execution plan for the query, and other related information are recorded in the trace file (opt_p[process ID_s [session ID].trc) under the trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) when processing queries.

To record SQL statement for the query, the execution plan and the execution time, refer to the following flag information.

**Flag information for TRACE_LOG_ID**

<a id="e06be78b4e200265"></a>
| Information | Flag(on) | Flag(off) |
| --- | --- | --- |
| Whether to output the successful SQL query | 100000 | 0 |
| Whether to output the failed SQL query | 10000 | 0 |
| Whether to output the execution plan | 1000 | 0 |
| Whether to output the execution type (direct/prepare) | 100 | 0 |
| Whether to output the bind value | 10 | 0 |
| Whether to output the execution time per section | 1 | 0 |

To set it in a form of "output the successful SQL query" + "output the execution plan" + "output the bind value", set the TRACE_LOG_ID value to 101010.

<a id="31502ce66fe333fb"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="11ca059ba7340125"></a>
### Basic Information

<a id="8816525c853832bf"></a>
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

<a id="31933f605e05fb78"></a>
### Description

It sets the size of the heap memory buffer which is used to configure the log message to be recorded in the trace logfile.

<a id="14b02ed91c70a5dc"></a>
## TRACE_LOG_TIME_DETAIL

<a id="2e33906818262fc7"></a>
### Basic Information

**Basic Information of TRACE_LOG_TIME_DETAIL**

<a id="9ad4dc7269641012"></a>
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

<a id="e5b2dc7aecc08190"></a>
### Description

It sets whether to increase the time accuracy when recording trace log.  
If the value is ON, it has an accuracy of 1 us.  
If the value is OFF, it has an accuracy of 10 ms.

<a id="4cd20f12fcf45db2"></a>
## TRACE_LOGGER

<a id="0d02cc5276dfc031"></a>
### Basic Information

<a id="5f6a7c89c6194fb3"></a>
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

<a id="082bc479b76a5160"></a>
### Description

It sets the target on which the trace log is written.  
If it is 1, then it is recorded in a file, and if it is 2, then it is remotely recorded in a file.  
When it is remotely written, then it remotely collects trace logs from gtrclogger and records in a file.

<a id="bb947853ba142e78"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="82919cbb9610a99e"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="074161b95640bb93"></a>
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

<a id="bbc6b88b15cb200b"></a>
### Description

It sets the host to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="c84bbd0b8628c656"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="0cd94cf2a08148fd"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="1b1a2975094248ad"></a>
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

<a id="57de697da4709980"></a>
### Description

It sets the port to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="f6e659ce216503c5"></a>
## TRACE_LOGIN

<a id="9f2c4f266a15543f"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="8e3b2dd88f43f26d"></a>
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

<a id="8ef27b79122eaf86"></a>
### Description

It records the related access information in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc) on login.  
Set TRACE_LOGIN property to *ON* to record the related information on login.

<a id="095a96ed03a5a351"></a>
## TRACE_LONG_RUN_CURSOR

<a id="e49b0d7fc0fa66ce"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_CURSOR**

<a id="c026630b1a7a52f9"></a>
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

<a id="c8ad4314a67fdaa0"></a>
### Description

When cursor life-time is longer than the specified property time, then it records the SQL statement of the cursor in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#e838aee7eaff0357) property to increase the precision.

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

<a id="fb5eec46d412b55f"></a>
## TRACE_LONG_RUN_SQL

<a id="a32610fed05d44c1"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="b16d687ba1efaf5d"></a>
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

<a id="f69cb7b8d10d22ff"></a>
### Description

It records the SQL statement whose execution time is longer than the specified property time in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#e838aee7eaff0357) property to increase the precision.

The following is an example of recording the SQL statement whose execution time is longer than 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

The following is an example of restoring to the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="e838aee7eaff0357"></a>
## TRACE_LONG_RUN_TIMER

<a id="dd728883d7024eb7"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="fbf3e0aeddc27c5b"></a>
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

<a id="c7ffaf7e31b5eb6e"></a>
### Description

It controls the measurement precision when measuring the execution time of the SQL statement by using the following properties.

- [TRACE_LONG_RUN_CURSOR](#095a96ed03a5a351)
- [TRACE_LONG_RUN_SQL](#fb5eec46d412b55f)

- Description of value
    - 0: It uses the timer thread whose interval is 10 milliseconds.
    - 1: It measures the time by using gettimeofday() function. In this case, the precision is higher but the system call causes the work load.

<a id="70f58a81d150075e"></a>
## TRACE_XA

<a id="25697c968e02d468"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="fe853a5ce8d99eb1"></a>
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

<a id="64cbc6a04eb80994"></a>
### Description

It specifies whether to output trace messages when using XA interface. Message is output to the 'SYSTEM_LOGGER_DIR / xa.trc'.

<a id="84e1f947f78fa722"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="a87ee65e69599b22"></a>
### Basic Information

<a id="9e6f077f05fc4f75"></a>
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

<a id="47caca597c2fbab1"></a>
### Description

It is the maximum waiting time when allocating transaction slots.

The following error occurs when the waiting time exceeds TRANSACTION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="8e31efee2a6d87da"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="7228e60bd34fcb89"></a>
### Basic Information

**Basic Information of TRANSACTION_COMMIT_WRITE_MODE**

<a id="dbe0996437ba97a8"></a>
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

<a id="e4dded433f242ceb"></a>
### Description

TRANSACTION_COMMIT_WRITE_MODE specifies whether a log generated by the transaction is flushed to the disk log file, when the transaction is committed. If TRANSACTION_COMMIT_WRITE_MODE is '1', the log should be flushed to the disk log file at the time of the transaction commit. Otherwise the transaction is committed regardless of log flush.

If the system is operated when TRANSACTION_COMMIT_WRITE_MODE is set to '0', the latest data will be lost when GOLDILOCKS is abnormally terminated without log flush after COMMIT transaction. It is because the logs are not recorded in this case.

Therefore, if all committed transactions should be remained (stored) in database, the system should be operated after setting TRANSACTION_COMMIT_WRITE_MODE to '1'. Or, 'ALTER SYSTEM FLUSH LOGS' statement should be explicitly performed at the time of transaction commit in order to flush log after TRANSACTION_COMMIT_WRITE_MODE is set to '0'.

- 0: no wait
- 1: wait

<a id="2216c13e8a31113c"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="861f0695ac43bc0e"></a>
### Basic Information

**Basic Information of TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT**

<a id="219aa9b45fb9a73c"></a>
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

<a id="a0815bb409ab566e"></a>
### Description

It means the maximum number of undo pages which the transaction can record. The minimum value is 1 (8 Kbytes) and the maximum value is 13107200 (100 Gbytes).

<a id="99be1050691e20a9"></a>
## TRANSACTION_TABLE_SIZE

<a id="9591c64d73f55bcb"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="2ab9fc5fb06e8f4d"></a>
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

<a id="7d265511176024ac"></a>
### Description

It sets the maximum number of transaction tables that can be executed in the database. These tables are allocated to ensure the ACID properties of transactions when updating the database. The database should restart to modify the number of transaction tables, and the number can be modified only to the number bigger than the previously specified number.

If it is modified to a smaller number, then the restart fails. For example, if the value set as 1,024 is modified to 512, then the restart fails as follows. In this case, modify it to 1,024 or bigger, then the restart succeeds.

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

ERR-HY000(14118): TRANSACTION_TABLE_SIZE property value must be equal to or greater than '1024'

gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 1024 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

<a id="58502a4b6008ed38"></a>
## TRANSACTION_TIMEOUT

<a id="a1a725ed63a72290"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="a5a8f2debd5977bb"></a>
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

<a id="45cb6c2dd4a832ee"></a>
### Description

It sets the duration of when the transaction is activated. It is used to prevent the side effects of when the transaction is activated for a long time. If a transaction exceeds the specified time, then gmaster daemon automatically terminates the session owned by that transaction.

<a id="c644945f24a50e13"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="9cea9c13d22f6a81"></a>
### Basic Information

<a id="3547c9b59ce03528"></a>
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

<a id="8d06ca308bcfd026"></a>
### Description

It is the maximum waiting time when allocating undo relations.

The following error occurs when the waiting time exceeds UNDO_RELATION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="41e1043c83a0a465"></a>
## UNDO_RELATION_COUNT

<a id="44b67c1733ce0bea"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="4dbd77e64304b022"></a>
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

<a id="c1d48a783e3d8d8d"></a>
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

<a id="1d69b3f8afc877e3"></a>
## UNDO_SHRINK_THRESHOLD

<a id="9d6583289cf175d8"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="9d0ed3727e2ed36e"></a>
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

<a id="076e5d412e5089b1"></a>
### Description

Ager thread periodically (10 seconds) checks the undo segment space. If an undo segment uses too much space, a part of it is returned to the tablespace. The property specifies the size (in bytes) of the space to be returned at a time.

<a id="f838d6d20a8a1377"></a>
## USE_LARGE_PAGES

<a id="bee6c9d88a016a5f"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="b87b881d98081526"></a>
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

<a id="e099e5bd3dad7f4d"></a>
### Description

It uses HugePage. HugePage should first be set in the device to use USE_LARGE_PAGES property.

- 0: It does not use the large page.
- 1: It uses the large page. When it fails to allocate the shared memory, then an error occurs.
- 2: It tries to allocate the shared memory by using the large page. When it fails to allocate the shared memory, then it allocates the memory by using the regular page.

> It can be used in Linux kernel 2.6.32-573 or higher.

<a id="79aa027e79a7b50d"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="a9a80c62157f5b16"></a>
### Basic Information

<a id="8b8581f8972973c0"></a>
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

<a id="44861293cae6a46c"></a>
### Description

It sets the default media type if the media type of the tablespace is omitted when creating the user data tablespace. 0 is memory and 1 is the disk.

<a id="e3542e99dbc097cf"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="2d366ea391658339"></a>
### Basic Information

<a id="dfd72fb51f2d2a1c"></a>
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

<a id="927f790b973cd672"></a>
### Description

It sets the default size if the data file size is omitted when creating the user data tablespace or adding the data file.

<a id="0175e393e2c1b58e"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="df8672eafb01322f"></a>
### Basic Information

<a id="bf386f0d45f4dc04"></a>
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

<a id="8296e6106fa4adc3"></a>
### Description

It sets the default size if the size to be extended is not set when it is required to extend the data file of the user disk data tablespace.

<a id="0f5a0f4a8b6edf18"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="2b8ec53dbbd77ae7"></a>
### Basic Information

<a id="640ec0b177e3e0a3"></a>
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

<a id="c7c6929c33db0116"></a>
### Description

It sets the default size if the data file size is omitted when creating the user temp tablespace or adding the data file.

<a id="97290fabed996692"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="39d1694b7c22af33"></a>
### Basic Information

<a id="8a70cc12d1b8b466"></a>
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

<a id="6bec3ad2b0155556"></a>
### Description

It is the maximum waiting time of xa transaction in idle (The duration between the beginning of XA and the next transaction). If it remains in Idle exceeding this time, then xa transaction is rolled back.

If it is set to 0, then XA infinitely waits even in idle.

---

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
