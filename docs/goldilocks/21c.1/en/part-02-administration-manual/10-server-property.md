<a id="5d474603dd66e8e7"></a>

# 10. Server Property

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/5d474603dd66e8e7)  
> Tag: `21c.1_35_tag`

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="448f1b40820b2964"></a>
## Server Property Information

For more information about SQL syntax to change properties, refer to the followings.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#8524798b9d7f6a03)
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#9478b0e9e0d1d5e2)

For more information about property types, refer to the followings.

- [V$PROPERTY](9-database-information.md#632f738a2348c556)
- [V$SPROPERTY](9-database-information.md#574101610fde824e)

The followings describe basic information items of property in this manual.

**Basic Information item of property**

<a id="dc65e9f5c83fe8a6"></a>
| Item | Description |
| --- | --- |
| Name | Property name |
| Summary | Short description of the property |
| Data type | Data type of the property value |
| Applicable phase | A startup phase which can be updated with ALTER SYSTEM or ALTER SESSION * NONE: Applicable phase does not exist. (If it can be updated, but applicable phase is NONE, then use *SCOPE = FILE* option.) |
| Updatable | Whether property is updatable or not * If the property value is TRUE, it is updatable.  * If the property value is FALSE, only the read-only is possible. |
| ALTER SESSION | Whether property is updatable or not by using [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#9478b0e9e0d1d5e2) |
| ALTER SYSTEM | Whether property is updatable or not by using [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#8524798b9d7f6a03) * IMMEDIATE: The updated value is immediately reflected in all session after execution. * DEFERRED: The updated value is reflected only in the session which is connected after execution. However, it is not reflected in already connected session. * FALSE: The updated value is not reflected in the session during execution. However, the updated value is reflected after restart, (Properties are updatable by using only *SCOPE=FILE* option.) * NONE: It is not updatable. |
| MIN | If the data type is BIGINT, it is the minimum value of property. If the data type is VARCHAR, the minimum value of property is N/A. |
| MAX | If the data type is BIGINT, it is the maximum value of property. If the data type is VARCHAR, the maximum value of property is N/A. |
| Default value | Default value of the property |

<a id="1fa45da774c40caf"></a>
## AGING_INTERVAL

<a id="2b742abdf425211b"></a>
### Basic Information

**Basic Information of AGING_INTERVAL**

<a id="f5bb4255d7cfeff0"></a>
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

<a id="5022eabad8c11228"></a>
### Description

It sets the idle time (second) when an ager thread which deletes the previous version data does not have a job to process in MVCC based database.

<a id="c914f32207c58377"></a>
## AGING_PLAN_INTERVAL

<a id="35dee7b4c5a56537"></a>
### Basic Information

**Basic Information of AGING_PLAN_INTERVAL**

<a id="723135e2aa676048"></a>
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

<a id="f332e351989e5031"></a>
### Description

The SQL plan which is older than AGING_PLAN_INTERVAL becomes the aging target.

<a id="b967aa5fdd50fec5"></a>
## ARCHIVE_LOG_THROTTLING

<a id="994a095bdbd6d9a6"></a>
### Basic Information

<a id="de2490ab94c65e2c"></a>
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

<a id="89261a9f4c18998e"></a>
### Description

This property is used to control disk I/O performance during redo log archiving.   
It causes the process to sleep each time the amount of data copied to the destination file exceeds the specified property value.

<a id="e7c9bfa1fbba1929"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="c56447861a8f47f5"></a>
### Basic Information

**Basic Information of ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10**

<a id="80542741c87449dd"></a>
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

<a id="bfb68ad2d5c2e2ea"></a>
### Description

It specifies archiving directory of GOLDILOCKS database's online redo log file. Also, it specifies where to read of archive redo log file at media recovery. The online redo log file creates archive redo log file only in ARCHIVELOG_DIR_1.

ARCHIVELOG_DIR_1 sets only the system, but ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10 sets the session.

<a id="b43dcaf8d821ff6a"></a>
## ARCHIVELOG_FILE

<a id="441935c05a851559"></a>
### Basic Information

**Basic Information of ARCHIVELOG_FILE**

<a id="ce958ae767309292"></a>
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

<a id="a46fa77b5c5cd6a9"></a>
### Description

It sets the prefix of the targeted file name stored in the archive directory when archiving the online redo logfile. The archive logfile's name consists of the prefix defined in ARCHIVELOG_FILE, followed by '_', the file sequence and the file extension 'log'. For example, the online logfile with a sequence number of 0 is archived as 'archive_0.log'.

<a id="d6ae9393853bccbb"></a>
## ARCHIVELOG_MODE

<a id="42107628b4e40d81"></a>
### Basic Information

**Basic Information of ARCHIVELOG_MODE**

<a id="3d5249d09a4b1cc8"></a>
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

<a id="6d142fa24780cc86"></a>
### Description

The property is applied at database creation. The archivelog mode can be set to one of the following value.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

It does not affect archive log mode during operation after database is created. The archive log mode can be modified by using *ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}* in MOUNT phase.

<a id="aa4a9e03f36b0c11"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="67ede7e987bfb3a8"></a>
### Basic Information

**Basic Information of BACKUP_DIR_1 ~ BACKUP_DIR_10**

<a id="a36bf04ed681a026"></a>
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

<a id="5cd39ec02173103b"></a>
### Description

A backup file is created when incremental backup is executed. Then it sets a directory of backup file to be read when restoring files using incremental backup. Incremental backups are created only in the directory set in BACKUP_DIR_1.

BACKUP_DIR_1 sets only the system, but BACKUP_DIR_2 ~ BACKUP_DIR_10 sets the session.

<a id="672b2e662eff7088"></a>
## BLOCK_READ_COUNT

<a id="b62527c3ed41c497"></a>
### Basic Information

**Basic Information of BLOCK_READ_COUNT**

<a id="1411793fc2136b17"></a>
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

<a id="9fda504ad8704b7d"></a>
### Description

The SQL executes operation by reading row in the unit of BLOCK_READ_COUNT which is a row bundle. BLOCK_READ_COUNT  means the number of rows to be processed at a time when operation is executed. It is a basic unit of  pipe-lining process of execution nodes which are used in SQL query processing.

If BLOCK_READ_COUNT value is big the processing performance improves, but many memory resources are used.    
The value between 10 and 100 is recommended.  
If the value becomes bigger than 100 the resource usage increases  proportionately, but the performance improvement does not increase proportionately.

<a id="078656a5e697d814"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="39c4b7c4b15e3b20"></a>
### Basic Information

<a id="77b1b043c5cb55b0"></a>
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

<a id="37f23cee1381852f"></a>
### Description

It sets whether to simultaneously rebuild the indexes on multiple members when rebuilding the index in cluster environment.

<a id="b37897c889af1c26"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="e2b0eb1bece3a2e3"></a>
### Basic Information

<a id="49a216eba1126153"></a>
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

<a id="975f6bee67db140e"></a>
### Description

It sets whether to simultaneously process protocol which can be processed on multiple members at the same time when performing table rebalancing in a cluster environment.

<a id="25de647e46b090d0"></a>
## BUFFER_CACHE_SIZE

<a id="935f45abdd809faa"></a>
### Basic Information

<a id="ed9800c90e82024e"></a>
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

<a id="f8be06c0e0dedd6c"></a>
### Description

It sets the size of the buffer which cashes the page in the disk tablespace.

<a id="24c97c83343d7d0b"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="8001790893d5cc34"></a>
### Basic Information

<a id="e069a71fb325e52f"></a>
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

<a id="4c6ec4940c42570c"></a>
### Description

It is linked to the checklist when pages of disk tablespace cached to the buffer are updated. Each checkpoint list flushes updated pages linked to the checkpoint list by its own flush thread to the disk, and BUFFER_CHECKPOINT_LIST_COUNT sets the number of checkpoint lists and the number of flush threads.

<a id="d044842eeb9da9d5"></a>
## BUFFER_FLUSH_THREADS

<a id="79c7e0c218488fe4"></a>
### Basic Information

<a id="e821ac88ddbbe213"></a>
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

<a id="9e3c22df3b389d10"></a>
### Description

It is linked to the flush list then requests flush to the buffer flusher, to reuse bch which cached the updated pages in the buffer lru list. In this case, BUFFER_FLUSH_THREADS sets the number of buffer flushers and flush lists to be used in the database.

<a id="8184f2dfdfb9d6be"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="25997db32f7b518b"></a>
### Basic Information

<a id="9edf0388ea25611d"></a>
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

<a id="b0b0ad7e6e8860ae"></a>
### Description

It sets the idle time (sec) when the job to be processed by the buffer flusher flushing updated disk tablespace pages to the disk does not exist.

<a id="d096bf6d63166bf3"></a>
## BUFFER_FREE_LIST_COUNT

<a id="457ae9d56ea83d6b"></a>
### Basic Information

<a id="da82df0c7725a682"></a>
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

<a id="f66f49b61cfb0a18"></a>
### Description

It sets the number of buffer free lists connecting bch which are instantly available to use in the buffer cache.

<a id="f6d27c5028546295"></a>
## BUFFER_HASH_BUCKETS

<a id="f72b3daf83bfa11f"></a>
### Basic Information

<a id="368b8a8f0e9bc7ec"></a>
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

<a id="02f0a6e7c998216d"></a>
### Description

It sets the number of hash buckets for the disk tablespace pages cached in the buffer. It can be set from 0 to 1073741824, and 0 is set by calculating hash buckets as many as pages which can be cached to the buffer which is set according to BUFFER_CACHE_SIZE. If the buffer size is smaller than the specified value, then it adjusts the number of hash buckets to the buffer size.

<a id="82dc27dfe435e89b"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="e096077de971ee0b"></a>
### Basic Information

<a id="6fadbfb3c94def53"></a>
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

<a id="d79ae4c20e62da59"></a>
### Description

It sets touch count to transfer pages existing in the cold region to the hot region in buffer lru list.

<a id="c53ddbab0f0bd57b"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="28fb1e4dd0603797"></a>
### Basic Information

<a id="0705a3e48f2db17d"></a>
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

<a id="29d159aec4ed4fee"></a>
### Description

It sets the proportion (percentage) of hot region pages to the entire page in the buffer lru list.

<a id="fa570e2d402c65df"></a>
## BUFFER_LRU_LIST_COUNT

<a id="c5e83c613f6cccc1"></a>
### Basic Information

<a id="ea8d6d0d94c18708"></a>
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

<a id="bf223cd5720e8d50"></a>
### Description

It sets the number of lru lists to select a victim among pages in use by caching when the free buffer for caching disk tablespace pages does not exist.

<a id="64d202a3b681ab07"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="c689373f59272c26"></a>
### Basic Information

<a id="e8cec69153a59103"></a>
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

<a id="066836129fbd96da"></a>
### Description

It sets the maximum number of pages to be used for one time disk IO when full scanning the disk table.

<a id="4b7d7ca789c523bb"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="4411587c84d957c7"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="a523f2a521b9655f"></a>
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

<a id="497c2c15d08fb581"></a>
### Description

It sets the maximum number of pages nearby to be prefetched per a disk I/O when accessing to the page in the disk tablespace which does not exist in the buffer.

<a id="3ea76004d1b841b4"></a>
## BULK_IO_PAGE_COUNT

<a id="e233af6ee13e6836"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="edf196786fe6da85"></a>
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

<a id="67b953b465c6e6a3"></a>
### Description

It is used when IO READ of the data file occurs during server restart, or when IO WRITE occurs during creating a data file.

The heap memory is allocated as big as BULK_IO_PAGE_COUNT * 8192 when server restarts or data file is created. If the session's PRIVATE_STATIC_AREA_SIZE is smaller than the heap memory size, an error of insufficient memory may occur. In this case, extend PRIVATE_STATIC_AREA_SIZE.

<a id="a4c3c152f92b0df8"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="607fcb1d92b5257f"></a>
### Basic Information

**Basic Information of CDISPATCHER_HOT_POLICY_INTERVAL**

<a id="76d8681b05e2e921"></a>
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

<a id="485416f96e3a9cf2"></a>
### Description

It is the time of the busy waiting when performing the dequeue in the cdispatcher. It is a micro second unit. If this value is big, it uses more cpu but the user response time (latency) is decreased.  
The default value is 0, and the busy waiting is not allowed.

<a id="1e83f468b159047b"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="36c595df1183ada1"></a>
### Basic Information

<a id="dc377c7f933915bb"></a>
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

<a id="914fbfb14cdb15c4"></a>
### Description

It sets the number of cdispatcher threads of lockless data sender and receiver. However, the number of cdispatcher threads of lockable data sender and receiver is set by using [CDISPATCHER_THREADS](#075fe5e02602ceae).

<a id="79e1f6ab9cccbd20"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="ab9049404005f0f8"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="e231a27c1b340263"></a>
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

<a id="ce07904b558feb3d"></a>
### Description

It is the socket buffer(sender, receiver) size of cdispatcher.

<a id="a80653a34c12039b"></a>
## CDISPATCHER_SYNC_THREADS

<a id="ee166fbf37ac2f15"></a>
### Basic Information

**Basic Information of CDISPATCHER_SYNC_THREADS**

<a id="4c479e2074c032bd"></a>
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

<a id="06b8950fb3aa698c"></a>
### Description

It is the thread count of cdispatcher sync.

<a id="075fe5e02602ceae"></a>
## CDISPATCHER_THREADS

<a id="3d0a9bbdb82013e1"></a>
### Basic Information

**Basic Information of CDISPATCHER_THREADS**

<a id="a3bef4baefac982c"></a>
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
| MAX | 30 |
| Default value | 1 |

<a id="c52d61445a770564"></a>
### Description

It sets the number of cdispatcher threads of lockable data sender and receiver. However, the number of cdispatcher threads of lockless  data sender and receiver is set by using [CDISPATCHER_LOCKLESS_THREADS](#1e83f468b159047b).

<a id="65a4dd05cb7195c8"></a>
## CHANGE_TRACKING

<a id="130eef9ba9553363"></a>
### Basic Information

<a id="eb7380c8e8e6e758"></a>
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

<a id="9d22bb0348878dba"></a>
### Description

It sets whether to track the updated pages to perform the incremental backup of disk tablespace.

- NO: disable change tracking
- YES: enable change tracking

*change tracking* can be enabled by using ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING on mount or above phase only when the database is operated in archivelog.

<a id="a34b998f6778d846"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="d93961a6ffd4552e"></a>
### Basic Information

<a id="e59906d8384e3444"></a>
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

<a id="f12866b5989e5582"></a>
### Description

It sets the number of pages to display with one dirty flag when change tracking. For example, if it is set to 32, then one dirty flag is used per 32 pages, and if it is set to 128, then then one dirty flag is used per 128 pages.

<a id="54fa98564b51e415"></a>
## CHANGE_TRACKING_FILE

<a id="fecfa8c009b8eb14"></a>
### Basic Information

<a id="10ef43a89dfd6d53"></a>
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

<a id="94fe56a75f7a8093"></a>
### Description

It sets the file directory which stores the change tracking, and the file name.

<a id="305fe0fd4eb06210"></a>
## CHAR_LENGTH_UNITS

<a id="8d5f9afc41517040"></a>
### Basic Information

**Basic Information of CHAR_LENGTH_UNITS**

<a id="ca353f1a95af982b"></a>
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

<a id="36a7bcc4f43384bf"></a>
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

<a id="252318a04d4fbe0e"></a>
## CHARACTER_SET

<a id="218bff0a73f2d0df"></a>
### Basic Information

**Basic Information of CHARACTER_SET**

<a id="97a5d19d55d4f985"></a>
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

<a id="9e64110d053eb7a0"></a>
### Description

It is a character set of database, and it is applied when database is created.  
The property is set to one of the following values.

**Character set**

<a id="4952f159e07ad205"></a>
| Character set | Description |
| --- | --- |
| SQL_ASCII | ASCII standards |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standards |

<a id="441b40591e4cc200"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="a1169dc6b0ea0406"></a>
### Basic Information

**Basic Information of CHECK_DEDICATE_CONNECTION_INTERVAL**

<a id="c030d4fdf71cb3b1"></a>
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

<a id="8dde26866c6bf33a"></a>
### Description

It is the interval of checking for when the client forcibly cut the connection in C/S dedicate environment. The dedicate server(gserver) checks the socket, and it terminates it if it was cut. The default value is 1,000 millisecond (1 second).

<a id="f6717d65883e6151"></a>
## CLIENT_MAX_COUNT

<a id="bf932783c3a7aaf0"></a>
### Basic Information

**Basic Information of CLIENT_MAX_COUNT**

<a id="0a75c3e395a3e1b6"></a>
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

<a id="796e6631414598d3"></a>
### Description

It sets the maximum number of sessions to connect.

<a id="22a528656d5e5e18"></a>
## CLIENT_NUMA_POLICY

<a id="f91ab43687671aae"></a>
### Basic Information

**Basic Information of CLIENT_NUMA_POLICY**

<a id="cef9700c1cbbd0d6"></a>
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

<a id="3ee416ccb8e1d19f"></a>
### Description

It determines the policy to distribute client processes to NUMA nodes. This property is operated when NUMA property is set to on.

- 0: It determines the NUMA node to be connected by modularizing the session ID.
- 1: It connects to the NUMA node of which is the least connected based on the statistics information.
- 2: C/S client is determined by TCP_CLIENT_NUMA_NODE property, D/A client is determined by DA_CLIENT_ NUMA_NODE property.

<a id="3ebdc3c905a12353"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="960c6bdcf50f06cb"></a>
### Basic Information

**Basic Information of CLOSE_PSM_CHILD_STMTS**

<a id="b4af2c25e7246cdf"></a>
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

<a id="80ac8e47f5136033"></a>
### Description

It closes the child statement of PSM at the end of each execution.

<a id="5fe3c0017fd2d5a3"></a>
## CLUSTER_ASYNC_COMMIT

<a id="f4b66951251de5f3"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="aa9da983203bedbe"></a>
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

<a id="97c870108454b6ff"></a>
### Description

It determines whether to internally process the commit protocol on an async mode in cluster system.

> If this property is set to on, it asynchronously commits each node, so the temporary inconsistency among nodes may occur. On the other hand, if it is set to off, it synchronizes everytime it commits, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="4e8d9c0b37211471"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="b241996985c69891"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="5fedd1806e19be98"></a>
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

<a id="486d07743a59d5bd"></a>
### Description

It determines whether to internally process the replication on an async mode in cluster system.

> If this property is set to on, it asynchronously reflects the data on each node, so the response time varies upon on which node is connected furing the operation. On the other hand, if it is set to off, it synchronizes everytime the data is updated, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="0877a44068f692e1"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="c7cd5251e69f49af"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_COUNT**

<a id="0484300de78287f1"></a>
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

<a id="a4c6f9b18b2037de"></a>
### Description

It is the communication buffer count for cluster.

<a id="847ad593560897ee"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="bd621a3b062af091"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_SIZE**

<a id="d2d8f86b7908a808"></a>
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

<a id="ca0be33a8dd616c0"></a>
### Description

It is the communication buffer size for cluster.

<a id="c06e8a62d2533416"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="490146ef2802e073"></a>
### Basic Information

**Basic Information of CLUSTER_CM_READ_BUFFER_SIZE**

<a id="698d19420d778fa7"></a>
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

<a id="a4b56dcaf5f02047"></a>
### Description

It is the communication read block size.

<a id="1cde2a8850ca2410"></a>
## CLUSTER_COMMIT_SLAVES

<a id="dc00e689a0a9ffe9"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_SLAVES**

<a id="79f30d1e1376277c"></a>
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

<a id="525d89d84859d34a"></a>
### Description

It is the number of commit slaves.

<a id="ce2db961f043ff42"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="8bd049b310b22976"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_STREAM_ISOLATION**

<a id="0d4741038b28cdc8"></a>
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

<a id="0aa2806e24bee2b0"></a>
### Description

It determines whether to internally perform the commit process flow in the cluster system separately from other protocol process. The performance may be improved when seperating the commit process according to the system environment.

<a id="a0a85295d8ed6045"></a>
## CLUSTER_CONNECTION

<a id="955e1d7d8f6a58a6"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION**

<a id="5f5cae3614197b66"></a>
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

<a id="2b6480ebb210426d"></a>
### Description

It is the connection mode for cluster. ( socket:0, rdma:1 )

<a id="563e5d4ecfb6d28d"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="e6039bf14d6e9d2b"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION_TIMEOUT_SEC**

<a id="fe5be058ce75255d"></a>
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

<a id="dd3650ce30d61e51"></a>
### Description

It is the connection timeout for cluster.

<a id="a8da8620a8605e54"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="4607fba481757917"></a>
### Basic Information

**Basic Information of CLUSTER_DATA_SYNC_SERVERS**

<a id="f71abce82ca5c3da"></a>
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

<a id="9f14791660d239b3"></a>
### Description

It is the count of data synchronization server.

<a id="d707fbd62568b15c"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="cec174c4112ddb12"></a>
### Basic Information

<a id="59ca7f31619d3dff"></a>
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

<a id="5dfc118e6011b61d"></a>
### Description

If the competition to occupy the cluster server becomes keen due to the lack of the lockable cluster server, then the cluster deadlock may occur. When cluster deadlock occurs, it waits for the deadlock to be resolved as long as the time set in this property. However, if it is not resolved, then CLUSTER_DEADLOCK_TIMEOUT error occurs.

<a id="1b92be8141c7eaff"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="f93034c5824de4fd"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_IN_QUEUE_SIZE**

<a id="72c5a8968dc0828c"></a>
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

<a id="06b0cc6768f3f6f9"></a>
### Description

It is the in-queue size for cluster dispatcher.

<a id="f7a11ac7573810b2"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="ecf1a4d1565795ec"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_NUMA_STREAM_MAP**

<a id="735e5330afa22a4a"></a>
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

<a id="18da0e6187f15cb9"></a>
### Description

It determines a NUMA node to which the cluster dispatcher is to be connected. This property is operated when NUMA property is set to on.

> If CLUSTER_COMMIT_STREAM_ISOLATION property is set to on, then the 0 stream is set to NUMA node of a commit stream.

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="160731944a61713d"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="d2009ac7e19b1d2c"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_OUT_QUEUE_SIZE**

<a id="e640a9896e9bfe6f"></a>
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

<a id="d68968961bf8c1c4"></a>
### Description

It is the out-queue size for cluster dispatcher.

<a id="b2f39c5fa7833d01"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="7e7f66a24df0a173"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_INTERVAL**

<a id="2a772f0a4957a656"></a>
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

<a id="51f7e9859298602c"></a>
### Description

It is the interval seconds for health checking of cluster. 0 means that it is disabled.

<a id="3761f0fffbcb971d"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="ec7c4c2004d56460"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_RETRY_COUNT**

<a id="c627649587df87fd"></a>
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

<a id="a60e4d4e680980e3"></a>
### Description

It is the retry count for health checking of cluster.

<a id="726425772ae2fcf8"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="fe402f2a772f7583"></a>
### Basic Information

**Basic Information of CLUSTER_IGNORE_INACTIVE_MEMBER**

<a id="6ff529eb75eca89b"></a>
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

<a id="c6547287b7b7cbb0"></a>
### Description

It ignores in-active member for cluster.

<a id="f47bb862562d46ce"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="2e65ea9945b56366"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PACKET_SIZE**

<a id="c308db1c6610de3e"></a>
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

<a id="b97501d216d01dc5"></a>
### Description

It sets the maximum packet size of which the remote protocol can transfer at a time. If the column size to be remotely transferred exceeds the property size, then the property size should be set bigger than the column size.

<a id="4cc24cfd0234f344"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="9ce240699736e806"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PAYLOAD_SIZE**

<a id="2d53d8a7dff46b77"></a>
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

<a id="3b5483c87fe93d13"></a>
### Description

The cluster packet which is remotely transferred may be delivered in pieces, and this property sets the maximum size of data to be stored in a piece.

<a id="b40abd9631df080a"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="8171b3af2278b746"></a>
### Basic Information

**Basic Information of CLUSTER_PACKET_ALLOCATION_TIMEOUT**

<a id="b2c1123c33a4074a"></a>
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

<a id="410dceecb89131c8"></a>
### Description

It sets the maximum time (second) of waiting when allocating memory required for cluster packet configuration.

<a id="1fce5ad26e28fafd"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="fba9cbdfee8f3977"></a>
### Basic Information

<a id="df327342d3208cdb"></a>
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

<a id="502ccd7fb4ad6d85"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property to use the failover policy. However, specify the time limit by using [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#624193135c95ae49) property to use the policy terminating the session.

<a id="624193135c95ae49"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="30598d3550fa299b"></a>
### Basic Information

<a id="88376ce231a2484a"></a>
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

<a id="d913a548d1977a5b"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property to use the policy terminating the session. However, specify the time limit by using [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#1fce5ad26e28fafd) property to use the failover policy.

<a id="c87b061bfbbe2c32"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="459aca66ceae9ec9"></a>
### Basic Information

**Basic Information of CLUSTER_SERVER_RESPONSE_QUEUE_SIZE**

<a id="49e475d813c9a70d"></a>
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

<a id="714365b5eab21031"></a>
### Description

It sets the maximum queue size to get response from the remote server.

<a id="f77698138fbe187f"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="144439035063fa2a"></a>
### Basic Information

<a id="5ecd9fb346300baa"></a>
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

<a id="b43e882ba49e74f3"></a>
### Description

It sets the number of hash buckets to control the cluster session.

<a id="29c2f9aec1f69689"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="c48b6ca9577e152d"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY**

<a id="b0243b1ee7907858"></a>
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

<a id="96fcbfdbdb1ae096"></a>
### Description

It sets the policy to resolve split-brain situation in the cluster system. If the value is set to 1 or over, it enquires the solution of a locator.

> If the query for a locator is timed out, it tries to enquire as many times as CLUSTER_SPLIT_BRAIN_RETRY_COUNT. If the property value after the retry failure is 1, then it forcibly proceeds the failover. If it is 2, then it terminates the fatal.

<a id="a42e52432a379da1"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="4d90d170863721b3"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RETRY_COUNT**

<a id="bddb7447fa0b62b6"></a>
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

<a id="52af0d0f4d90ce6c"></a>
### Description

It is used when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or over in cluster system. It sets the times of retrying to enquire when the query to a locator does not respond.

<a id="429c83799fd4afc7"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="4de6b4543696960b"></a>
### Basic Information

**Basic Information of COMMITTER_HOT_POLICY_INTERVAL**

<a id="c6548204eefa4c3c"></a>
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

<a id="35c9566a261e786c"></a>
### Description

It sets the timezone interval of busy waiting when the commit cserver is dequeing to read the commit protocol message. If it is set to 1,000,000 (1 second), and the time is not passed over 1 second from the last deque success to another deque retry, then it sets the timeout in deque to 0 and performs the busy waiting.

<a id="6713e926964ab592"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="da72a00dbe1aa555"></a>
### Basic Information

**Basic Information of CONTROL_FILE_0 ~ CONTROL_FILE_7**

<a id="b641f30ff1576b68"></a>
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

<a id="4679d276fc4b6795"></a>
### Description

If a control file is corrupted, database can not be used. Therefore, the control file is multiplexed for stability of database. It specifies the directory and file name of which stores each control file.

<a id="be260ba9aa3567d7"></a>
## CONTROL_FILE_COUNT

<a id="dc22fd53edab9a3f"></a>
### Basic Information

**Basic informatin of CONTROL_FILE_COUNT**

<a id="6356a89a591c2f24"></a>
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

<a id="b0eee45e52fbfffd"></a>
### Description

If a control file is corruped, database can not be used. The control file is multiplexed for stability of database. CONTROL_FILE_COUNT specifies the multiplexing number of control files. A control file is multiplexed at least 2 up to 8.

<a id="1ab281be45e9aba4"></a>
## CONTROL_FILE_TEMP_NAME

<a id="79e2c2ea79804290"></a>
### Basic Information

**Basic Information of CONTROL_FILE_TEMP_NAME**

<a id="4c9a88454a2cf43e"></a>
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

<a id="d4c406abf6abd391"></a>
### Description

During database operation, a control file is frequently changed, and its temporary copy can be made if necessary. CONTROL_FILE_TEMP_NAME specifies the directory and its file name to temporarily store the control file.

<a id="572c5669f22ac6fe"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="0eaca8d5eb3e1220"></a>
### Basic Information

**Basic Information of COORDINATOR_COMMIT_WRITE_MODE**

<a id="1ebed326ca14c9a1"></a>
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

<a id="0af08b0c0e6f7c1e"></a>
### Description

It is a commit write mode applied to a coordinator. If TRANSACTION_COMMIT_WRITE_MODE is *no wait*, and its property is *wait*, then the coordinator node is operated as *wait*, and other nodes are operated as *no wait*.

<a id="ef4b111b5e382d63"></a>
## CSERVERS

<a id="03cd757509f50cf3"></a>
### Basic Information

**Basic Information of CSERVERS**

<a id="20274c8e3a72d2df"></a>
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

<a id="3b54a53bf06383b4"></a>
### Description

It sets the number of cluster server processes performing the operation which acquires the lock. The number of cluster server processes performing the operation which does not acquire the lock is set by using [LOCKLESS_CSERVERS](#51bccd1c9f6597d0).

<a id="854608a5b97a4867"></a>
## DA_CLIENT_NUMA_NODE

<a id="fd0edd51bc63b9e0"></a>
### Basic Information

**Basic Information of DA_CLIENT_NUMA_NODE**

<a id="526ac8492d752087"></a>
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

<a id="510c717754856ee0"></a>
### Description

It sets the NUMA node ID to which the direct access (D/A) session is to be bound. This property is operated when NUMA property is set to ON.

<a id="80df872fd5814188"></a>
## DATA_STORE_MODE

<a id="c9ccaef24086a23f"></a>
### Basic Information

**Basic Information of DATA_STORE_MODE**

<a id="cd815f1e06d816df"></a>
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

<a id="33749223b286b2ab"></a>
### Description

It sets the storing method of database.

- 1: CDS mode supports the concurrency for multiple users but it does not guarantee the durability. It does not record logs for all update operations such as insert/ delete/ update data, consequentially a failure can not be recovered.
- 2: TDS mode guarantees the concurrency for multiple users and the durability using logs.

<a id="289fe02b3bffc5a9"></a>
## DATABASE_ACCESS_MODE

<a id="22220b8ec8c19b97"></a>
### Basic Information

**Basic Information of DATABASE_ACCESS_MODE**

<a id="943c6a3bceaed78e"></a>
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

<a id="c68cc1fd9514a460"></a>
### Description

When database starts, it sets the access mode.

- 0: It is able to read operation, but unable to insert/ update/ delete operations on database.
- 1: It is able to read/ insert/ update/ delete operations on database.

<a id="67a33b17df156534"></a>
## DATABASE_INSTANCE_NAME

<a id="73e7760d73ed8c01"></a>
### Basic Information

**Basic Information of DATABASE_INSTANCE_NAME**

<a id="59b40b696d9169f7"></a>
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

<a id="798ecc46e7e116c7"></a>
### Description

It is the database instance name.

<a id="bc5ecd3f33f5643a"></a>
## DDL_AUTOCOMMIT

<a id="a99fd5e21328c118"></a>
### Basic Information

**Basic Information of DDL_AUTOCOMMIT**

<a id="a8ad2a804af06cbc"></a>
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

<a id="e82b7ac376f8a2bc"></a>
### Description

It sets whether to autocommit DDL operations which are not autocommitted yet. For example, autocommit is not applied to the operations such as creating/altering a table, so if DDL_AUTOCOMMIT is 0, a table creation and alteration can be undone by the rollback. On the other hand, if DDL_AUTOCOMMIT is 1, DDL to which autocommit is not applied is committed immediately.

<a id="7ccb677c22738745"></a>
## DDL_LOCK_TIMEOUT

<a id="c2ef434635774f8c"></a>
### Basic Information

**Basic Information of DDL_LOCK_TIMEOUT**

<a id="23e1914e9a48a714"></a>
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

<a id="8a0286de81d001fe"></a>
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

<a id="ae9a3e1e6789368b"></a>
## DEADLOCK_PRIORITY

<a id="e0c970172305d4bb"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="f96bcbbaa44faa2e"></a>
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

<a id="828426926a16c234"></a>
### Description

When a deadlock occurs while simultaneously processing multiple transactions, a specific transaction with the low weight is selected as a victim among transactions which caused the deadlock, to solve the problem. If a deadlock occurs between a transaction started in sessions which have higher value for this property and a transaction started in sessions which have lower value for this property, then latter is selected as a deadlock victim. Therefore, set this property according to the priority of each transaction.

Start the transaction after setting this property value so that this value is applied as a weight of that transaction. The transaction weight is not altered if this value is changed after the transaction already has been started.

<a id="f05c08eb934d4a66"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="6146e97e20ff99f5"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="e05ecdf25e3f9c80"></a>
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

<a id="579dd705a515fef3"></a>
### Description

It sets whether to create the global secondary index when creating a table in cluster system. A non-deterministic query for the table which did not created the global secondary index fails. The global secondary index can be separately created after creating the table when the property is set to NO.

<a id="71f2d95a0e713d85"></a>
## DEFAULT_INDEX_LOGGING

> It is not supported after 3.2.

<a id="871a43c68700253a"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_LOGGING**

<a id="1d0300064ad0ebf7"></a>
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

<a id="328a4da02f557085"></a>
### Description

If LOGGING property is not explicitly set by a user when an index is created, then it is set to DEFAULT_INDEX_LOGGING value. If an index is created in LOGGING tablespace, the LOGGING property should be set.

<a id="6365821a90b522f1"></a>
## DEFAULT_INDEX_PCTFREE

<a id="23614c622b3931b3"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_PCTFREE**

<a id="3ae55ff739fa2299"></a>
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

<a id="645a97c6e5aac71f"></a>
### Description

If a user does not explicitly specify PCTFREE syntax when creating an index. The PCTFREE is set to DEFAULT_INDEX_PCTFREE property value.

<a id="7790c7541f51206b"></a>
## DEFAULT_INITRANS

<a id="a53f7972503dbf98"></a>
### Basic Information

**Basic Information of DEFAULT_INITRANS**

<a id="92b0455763cf428b"></a>
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

<a id="2919369042207095"></a>
### Description

If a user does not explicitly set INITRANS syntax when creating a table or an index, then it is set to DEFAULT_INITRANS property value.

<a id="0cdf26f13b3ef647"></a>
## DEFAULT_MAXTRANS

<a id="f6c54e88b1d5df08"></a>
### Basic Information

**Basic Information of DEFAULT_MAXTRANS**

<a id="63ec55d30dd0336f"></a>
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

<a id="a8e07907978b3e1f"></a>
### Description

If a user does not explicitly set the MAXTRANS syntax when creating a table or an index, then it is set to DEFAULT_MAXTRANS property value.

<a id="2fedd19366e713cc"></a>
## DEFAULT_PCTFREE

<a id="620f83c0e83367fe"></a>
### Basic Information

**Basic Information of DEFAULT_PCTFREE**

<a id="7e0aaff0726f57d8"></a>
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

<a id="5e67f18a6e5f189f"></a>
### Description

If a user does not explicitly set the PCTFREE property when creating a table, it is set to DEFAULT_PCTFREE property value.

<a id="57a464d5a377892a"></a>
## DEFAULT_PCTUSED

<a id="a18b09cf76837577"></a>
### Basic Information

**Basic Information of DEFAULT_PCTUSED**

<a id="2cb4ced3fb834eb9"></a>
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

<a id="eefaf4db21923b74"></a>
### Description

If a user does not explicitly set the PCTUSED property when creating a table, it is set to DEFAULT_PCTUSED value.

<a id="c6e08d7770a6f20f"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="45e48ffa119ffcc0"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_BACKUP_FILE**

<a id="42a6ae390415e5cd"></a>
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

<a id="e2ff0312254d11cd"></a>
### Description

It specifies whether to delete the backup file when deleting the backup list.

<a id="4210b796fee0d49c"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="b873de6bbc62c234"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST**

<a id="b11aa8025969ce35"></a>
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

<a id="e994a0ceb8ce61a9"></a>
### Description

It specifies whether to delete the previous obsoleted backup list when executing INCREMENTAL BACKUP.

<a id="538c33a1508d31f9"></a>
## DEFAULT_SHARDING

<a id="519d3cecb2fe1df0"></a>
### Basic Information

**Basic Information of DEFAULT_SHARDING**

<a id="5d2d2a21c38b1813"></a>
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

<a id="309b71c57aec1365"></a>
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

<a id="fec2f6eb293eabc1"></a>
## DISABLE_DDL

<a id="70df33d9737aca04"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="d5ff057d3a44201a"></a>
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

<a id="74e8e00c0f5d132f"></a>
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

125 rows selected.
```

<a id="4d88079d7c0cdeb6"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="ceec1a1ea96af412"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="6bf6de1afc18f5ca"></a>
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

<a id="d4dc994ae153bfe5"></a>
### Description

It prohibits DDL operation on the table of supplemental log, because it affects CDC's give up.  
For more information, refer to [The table-related DDL causing Replication Give-up](../part-07-replication/50-cyclone.md#f595e5552e753895).

<a id="72b564a5057a2ea2"></a>
## DISABLE_SERIAL_DDL

<a id="3c4d286110c1ba85"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="0d029c803e6ef2cf"></a>
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

<a id="61ad2eaea0aa7584"></a>
### Description

DDL is executed for all cluster members after sequentially acquiring locks in cluster environment as described in [Processing DDL in Cluster](../part-03-sql-manual/12-sql-languages.md#cf4290065c4a2d4f).  
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

102 rows selected.
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
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

23 rows selected.
```

<a id="cf1a29c9baf62835"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="9f52752b38aef0bb"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="a747f4b8f9d23b7c"></a>
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

<a id="dacea05375751d7b"></a>
### Description

It disables UPDATE primary key which caused CDC give up.

<a id="db9fda9b74cb7a95"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="5b5bc56980217f89"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE**

<a id="9cb119349e9bd294"></a>
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

<a id="e2b8b99317cc302f"></a>
### Description

It disallows TARGETTYPE protocol.

<a id="8f109104eac2b4af"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="c713fd701df8b357"></a>
### Basic Information

<a id="9f5c821837bf1e60"></a>
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

<a id="5b1c69bfa392513d"></a>
### Description

It disallows TARGETTYPE_WITH_ALL protocol.

<a id="1efc614873e2f394"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="86a9e09599297ab3"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="1741053c46ebde2e"></a>
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

<a id="c6161ef241961cb7"></a>
### Description

It disallows TARGETTYPE_WITH_NAME protocol.

<a id="03348850a71c3292"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="c108b2ace4b115a5"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_BUFFER_SIZE**

<a id="2a90c6ecd07e7ef9"></a>
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

<a id="e8be255b02299d8a"></a>
### Description

It is the size of entire communication buffer used in shared mode. It is allocated to and used in Shared Static Area (SSA).

<a id="e2a66ec4e90fa395"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="00706bd0561f7cf4"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_UNIT_SIZE**

<a id="fd2fc28371c3fb59"></a>
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

<a id="86623eec975fd682"></a>
### Description

It is the unit size managed by dispatcher in shared mode. If the size is large, the memory is wasted. If it is small, the performance is degraded. It is set to the maximum communication packet size in the shared mode.

<a id="7105cf54e1f4d12e"></a>
## DISPATCHER_CONNECTIONS

<a id="d01510617397d187"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="ed49b43b92200df2"></a>
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

<a id="65593ed8a395373c"></a>
### Description

It is the maximum number of connection (client) which a dispatcher can manage in shared mode.  
If the system- supported maximum value is smaller than the set value, it is internally set to the system maximum.

<a id="8cbbf0d74a3d55ab"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="b548c7afa1c7999f"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="3fd5afe40e5be747"></a>
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

<a id="9b15872e6355ed15"></a>
### Description

It is the dispatcher dequeue interval for busy waiting. (micro second)

<a id="3d718281e60c9aba"></a>
## DISPATCHER_LOAD_BALANCING

<a id="a29615482c41335a"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="47412675f5a9fc31"></a>
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

<a id="b78e607129cd7bb9"></a>
### Description

It is an algorithm allocating a dispatcher when connecting to a client in the shared mode.

- 0: It is allocated to a dispatcher of which the number of currently attached clients are small.
- 1: It is sequentially allocated to a dispatcher.

<a id="0c2f352988760a9c"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="db977fe5ca01c072"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="ac715138b4162697"></a>
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

<a id="75935fcd26429c93"></a>
### Description

It determines NUMA node to which dispatchers are to be connected. This property is operated when NUMA property is set to on.  

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="8b3ef47ac4bade67"></a>
## DISPATCHER_QUEUE_SIZE

<a id="5f7087c5064053f8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="12e2f6b070dccb20"></a>
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

<a id="8ddb08e1a3e327be"></a>
### Description

In shared mode, it sets the queue size for the communication between the dispatcher and the shared-server.

<a id="490e8c80cf47f73a"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="c7b826986a19eed4"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="cc12bf83329d6bed"></a>
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

<a id="b82fca921d4c512f"></a>
### Description

It is the count of mini queue per request queue.

<a id="80e81be88d2b5d49"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="37bb64141c01c4e0"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="6599076658786319"></a>
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

<a id="2ee696cbb70c162d"></a>
### Description

It is the count of mini queue per response queue.

<a id="94045d4bf8a00efa"></a>
## DISPATCHERS

<a id="351996db5a1db742"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="19cf8f0927879e98"></a>
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

<a id="85c34504ee390b4b"></a>
### Description

It sets the number of dispatcher processes when using the shared mode.  
It can not reduce the value by using alter system on open phase.

<a id="896dc965c4b8332c"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="e34f41b504f0e5e7"></a>
### Basic Information

<a id="3c516699069d9da5"></a>
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

<a id="924b1a5355a01daa"></a>
### Description

If the memory is not sufficient to expand the hash bucket in the query using an instant hash table, then it determines whether to fail the query or to perform the query without expanding the hash bucket.

<a id="6e7ec84e99d65b31"></a>
## FETCH_FAILOVER

<a id="cd525c8cb534f4b3"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="246a3ff529564f23"></a>
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

<a id="79db285e37d95386"></a>
### Description

It enables the fetch failover.

<a id="92dc87149743eac7"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="b7cd2eaf5d681254"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="e97495dd22ff4274"></a>
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

<a id="82ae422840e1ced3"></a>
### Description

It sets whether to support the query execution including the session dependent information in the global connection.

<a id="13d867dc2ae82f47"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="36c3a56e5739f160"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="ccef80c636744008"></a>
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

<a id="0fed301f1c939eae"></a>
### Description

It is the size of global journal buffer.

<a id="f9e6bc3b150ec3f7"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="0125f22c2b3c6d4b"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="3654ac3762f200bf"></a>
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

<a id="110b5ea46e8beef2"></a>
### Description

It is the total max size of global journal buffer.

<a id="4ce9a89492b024f6"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="59a86bd8c1a069d3"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="fc48a7d319a3e990"></a>
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

<a id="6513bf0e38166ed0"></a>
### Description

When changing the global property, it performs the lock to control the concurrency. In this case, the waiting time to perform the lock is set.

<a id="7947d30b34020319"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="d49023e9b9effe40"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="6b6e265e994e40f2"></a>
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

<a id="ffe2dd46cc48c5ef"></a>
### Description

It is a property to change the commit write mode of the global transaction. TRANSACTION_COMMIT_WRITE_MODE property is applied to all transactions, but GLOBAL_TRANSACTION_COMMIT_WRITE_MODE property is applied only to a global transaction. If the property is set to 2, then it follows the TRANSACTION_COMMIT_WRITE_MODE.

- 0: It does not wait.
- 1: It waits.
- 2: It follows the value of TRANSACTION_COMMIT_WRITE_MODE.

<a id="adf4b768a2796eec"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="6f31ee91bf9659f5"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="ecd9de31a9e04df3"></a>
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

<a id="3c8f2d1c5da87bcd"></a>
### Description

It determines whether to process the data with a global transaction or with multiple domain transactions when the transaction changed the data through two cluster groups.

- 0: It processes with a global transaction.
- 1: It processes with multiple domain transactions.

> If this property is set to 1, it commits each cluster group with a separate transaction, so it does not guarantees the transaction atomicity.

<a id="9b479703ed95c235"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="6701886421ca8d96"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="8fcb66c246a80f07"></a>
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

<a id="ceb4dd22ad144cf1"></a>
### Description

It is the default directory of global transaction log.

<a id="ef1bb2dca7cf4480"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="e6f0a072329b0264"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="5145432db9993172"></a>
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

<a id="da94a76ed344767a"></a>
### Description

It is the file size of global transaction log.

<a id="b19f95a28a643457"></a>
## GMASTER_NUMA_NODE

<a id="6a27cc5c151924d9"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="32848b2286f65d50"></a>
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

<a id="3ae93467d8a8e50b"></a>
### Description

It sets the ID of NUMA node to be used by gmaster daemon. This property is operated when NUMA property is set to on.

<a id="df1bf316c1ae57fd"></a>
## GMON_AUTOSTART

<a id="5d61ae818133b5fd"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="047c1228b69c049a"></a>
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

<a id="b33cfaf4fd6b4ea2"></a>
### Description

It sets whether to start gmon process automatically.

<a id="87f9ef66d29fd0e6"></a>
## HINT_ERROR

<a id="90dd2ae7dee1b28a"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="2a3050e3bfe3366d"></a>
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

<a id="9b83d05eb2edb39e"></a>
### Description

It sets whether to check syntax error and validation error for hint syntax.

<a id="4b818ad1fd1f9997"></a>
## IDLE_TIMEOUT

<a id="90b258362f25acc8"></a>
### Basic Information

**Basic Information of IDLE_TIMEOUT**

<a id="1ae49e7217376287"></a>
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

<a id="99a81bd61be8ff3c"></a>
### Description

It sets the maximum IDLE time possible to wait in C/S session. If it exceeds the specified idle time, TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="b2afcf96d548ee1b"></a>
## IN_DOUBT_DECISION

<a id="c48281f23e713d23"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="f96f0ff9395b1522"></a>
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

<a id="b975df143eebfddc"></a>
### Description

It determines whether to commit or to rollback the in-doubt transaction of distributed transactions.

- 1: Commit
- 2: Rollback

<a id="6082674cd9a7d7ae"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="30202e38e469962b"></a>
### Basic Information

<a id="cfa601c2061892e8"></a>
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

<a id="a54b6f4c8649b1ad"></a>
### Description

It is the maximum number of values which are targets of *in key range* performing the *in key range scan* based on array.

- IN_KEY_RANGE_ARRAY_COUNT should be 3 or bigger to perform the *in key range scan* based on array for the statement below.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

If the maximum number of in key range target values are bigger than IN_KEY_RANGE_ARRAY_COUNT value, then in key range in key range scan is performed based on instant table.

<a id="ee97c4c0cbac8511"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="fc78695511189eb6"></a>
### Basic Information

<a id="343adc14e407cefc"></a>
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

<a id="1d3e11850ea54ced"></a>
### Description

It sets the number of pages to read by one time disk IO for performing incremental backup of the disk tablespace.

<a id="4b950d7a89c5f767"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="be45e4645cdd72fd"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="8bf34a791b25b98c"></a>
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

<a id="22a5d636a8fa7bc3"></a>
### Description

When creating an index, it specifies the number of parallel factor.

- 0: It is specified as the number of the core factor in the system.

<a id="2735d24d76cc77e1"></a>
## INDEX_LOGGING_THROTTLING

<a id="fb57d650fa1a29ba"></a>
### Basic Information

<a id="a91fb565ee156d68"></a>
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

<a id="3bffd3327cd39146"></a>
### Description

This property is used to prevent system overload caused by bulk logging during index creation and rebuild, ensuring that online services are not affected.

If there are more dirty blocks than the specified property value in the log buffer during index logging, it will wait until the dirty blocks are flushed to disk.

<a id="e4f5d0bc0590ed64"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="1e30bd6540a47988"></a>
### Basic Information

<a id="6c042b80072e4f64"></a>
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

<a id="d25be1522aa1f610"></a>
### Description

When DML is performed while rebuilding the index on ONLINE mode, the journal data is stored. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal data. INDEX_REBUILD_BLOCK_READ_COUNT sets how much journal data to be read and applied to the index during this process.

<a id="455e18dfbe21f37d"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="c2048e390e6ff902"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="31a1e2f24902e2d5"></a>
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

<a id="c1f05d6a874c951b"></a>
### Description

When creating an index, it specifies the number of parallel factor to merge the sub-tree.   
If that value is bigger than INDEX_BUILD_PARALLEL_FACTOR, then INDEX_BUILD_PARALLEL_FACTOR is used.

- 0: It follows INDEX_BUILD_PARALLEL_FACTOR.

<a id="6dd246849851d979"></a>
## INST_ALLOCATOR_COUNT

<a id="f3f030d3c532ec35"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="5bcd6c50aabec710"></a>
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

<a id="106ec1894d775678"></a>
### Description

This property increases the parallel property of operation allocating or deleting an instant block.

<a id="e8948e1ccae8b84e"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="a2d47d9c8b26dbd8"></a>
### Basic Information

<a id="5414cb3aa2bdd597"></a>
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

<a id="ac12c5ef3e6c9b38"></a>
### Description

It sets the maximum expected bucket counts of the hash instant table.

<a id="49d5090be5da7277"></a>
## INST_TABLE_BLOCK_SIZE

<a id="f39a4ced43db918f"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="2cbbe141a58c7849"></a>
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

<a id="1d098178b6543fe9"></a>
### Description

It determines the size of an instant block. If the anchor area of an instant record is bigger than an instant block, then the following error occurs.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="6d499890ead11777"></a>
## IPC_CHANNEL_COUNT

<a id="2274c8d5af732abb"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="8b1775527aced1c1"></a>
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

<a id="e78a37033f0ba15d"></a>
### Description

It sets the number of channels for IPC communication.

<a id="15f1008331808e02"></a>
## JOURNAL_TEMP_DIR

<a id="71e5cd5e22d65848"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="cc153891def2d135"></a>
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

<a id="82c4277b1f71d3f2"></a>
### Description

It is the temporary directory of journaling.

<a id="f500407cbd693a3f"></a>
## KEEPALIVE_IDLE_TIME

<a id="4f216bc0d1e4e26e"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="1336b54f4b466cfc"></a>
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

<a id="76ce8e9b0c1ae660"></a>
### Description

It means the idle duration between the server and client without tcp packet exchange before sending keep alive packet. If there is not tcp packet exchange for seconds (KEEPALIVE_IDLE_TIME), keep alive mechanism starts execution to detect the dead connection on the server side.

<a id="34f647d662260b28"></a>
## LOCAL_CLUSTER_MEMBER

<a id="f5ca623d4faea438"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="14bcc5d51d1cbeb1"></a>
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

<a id="7a1a131b4e1704dc"></a>
### Description

It is the local cluster member name.

<a id="0006201faadcb75c"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="edd9aa290e4e05b4"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="52697d9a957fc073"></a>
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

<a id="0d28b74c8d1605aa"></a>
### Description

It is host name of local cluster member.

<a id="e23ea6c79031be49"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="83b9be66b5b3cba0"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="b17860792e47e919"></a>
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

<a id="8b36a0153cd00a2d"></a>
### Description

It is listen port of local cluster member.

<a id="33bfe07f81cbe43f"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="29408bbbae170c69"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="b4c430fc5e83c028"></a>
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

<a id="e555d312b1d03b10"></a>
### Description

It is the local journal buffer size.

<a id="849787c22e2f9909"></a>
## LOCATION_FILE

<a id="3c98920369ac4c39"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="84c5c3f6d6b4a785"></a>
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

<a id="36cee99bcfad791e"></a>
### Description

It is the location file name.

<a id="dbae42f18a840e40"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="b24d72adc80e95a3"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="0438215fff9201ba"></a>
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

<a id="48ebf9f3f6563d4f"></a>
### Description

It sets the time (second) waiting for the response after the cluster system enquires of a locator about the solution of split-brain situation. This property is used only when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or more.

<a id="0a298eb370aa2aa2"></a>
## LOCK_HASH_TABLE_SIZE

<a id="ffdf15c20e169e2b"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="0fdda172c1203346"></a>
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

<a id="af14c92b3d84bec6"></a>
### Description

It specifies the maximum hash table size managed by a lock manager.

<a id="51bccd1c9f6597d0"></a>
## LOCKLESS_CSERVERS

<a id="02b102f885f58d29"></a>
### Basic Information

<a id="8d6ce547ef2bb2b3"></a>
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

<a id="69e6524fe05eaa9a"></a>
### Description

It sets the number of cluster server processes performing the operation which does not acquire the lock. The number of cluster server processes performing the operation which acquires the lock is set by using [CSERVERS](#ef4b111b5e382d63).

<a id="d54fdf7becbdb0f7"></a>
## LOG_BLOCK_SIZE

<a id="14185341900033d0"></a>
### Basic Information

**Basic Information of LOG_BLOCK_SIZE**

<a id="19bb9e4e3379d8e7"></a>
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

<a id="97dfd8bdf6202028"></a>
### Description

It means the minimum size of what log buffer is flushed to the log file of the disk. Its value should be set to one of 512, 1024, 2048, 4096.

<a id="c3d1b92a4449722e"></a>
## LOG_BUFFER_SIZE

<a id="acba369e7f26e64d"></a>
### Basic Information

**Basic Information of LOG_BUFFER_SIZE**

<a id="9d57546168c50794"></a>
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

<a id="083ff9fb88519ed2"></a>
### Description

A log buffer is the shared memory space in which the redo logs generated in database by the DML/DDL operations are stored. LOG_BUFFER_SIZE is referenced to set the memory size for the log buffer.

<a id="6bc42cad8c77c6b4"></a>
## LOG_DIR

<a id="736534ae6d832642"></a>
### Basic Information

**Basic Information of LOG_DIR**

<a id="3e26a21b5dcf2d5e"></a>
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

<a id="5889cc3e2c6ff42b"></a>
### Description

The log recorded in the log buffer is flushed to the logfile which exists in a non-volatile storage device to ensure the database durability. LOG_DIR sets the path to the log file.

<a id="4c71d7f219271e8a"></a>
## LOG_FILE_SIZE

<a id="907aab9d0e1a8ec7"></a>
### Basic Information

**Basic Information of LOG_FILE_SIZE**

<a id="dfa383bf86ed82cc"></a>
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

<a id="b56b821ca53a4ad4"></a>
### Description

It sets the size of the logfile used in database. It is referenced only when creating the database, then log file size can not be updated after then.

<a id="f4ccdfb4861c58ca"></a>
## LOG_GROUP_COUNT

<a id="8484aca0dfb3325d"></a>
### Basic Information

**Basic Information of LOG_GROUP_COUNT**

<a id="472520ee51a1f199"></a>
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

<a id="eb427d80c83900d5"></a>
### Description

It sets the number of log group used in database. It is referenced only when creating the database, but after that, it does not affect any operations. After creating database, the operation to add or remove a log group is supported by a separate syntax.

<a id="0d5e8206f92e6b0a"></a>
## LOG_MIRROR_MODE

<a id="e765ddd35548835d"></a>
### Basic Information

**Basic Information of LOG_MIRROR_MODE**

<a id="f64fef14e1da53ea"></a>
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

<a id="78c7711228d5a183"></a>
### Description

It is the property to configure the required shared memory when operating LogMirror, the redo log replication tool, at database startup.  
It should be enabled to execute the LogMirror.  
The size of the shared Memory can be changed using LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE.

<a id="05044794746046b2"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="4c5591a99759a239"></a>
### Basic Information

**Basic Information of LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE**

<a id="9fdcd4408b3c8084"></a>
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

<a id="c5166a2876ab363e"></a>
### Description

It sets the size of the shared memory used in LogMirror, the redo log replication tool.   
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="761617a538ff5dcc"></a>
## LOG_MIRROR_TIMEOUT

<a id="80e05fcfea3b006e"></a>
### Basic Information

**Basic Information of LOG_MIRROR_TIMEOUT**

<a id="93a63c768d59758b"></a>
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

<a id="9e1f85a02234757d"></a>
### Description

It is the response waiting time of the LogMirror.   
If its value is 0, it waits indefinitely. Otherwise, it waits as long as the value set, then TIMEOUT occurs, and it stops LogMirror service. Later, the server is operated normally.  
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="fe37330ca04276fa"></a>
## LOG_SYNC_INTERVAL

<a id="6bfaa5ef412d9c9d"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="c76b2e1558121f4c"></a>
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

<a id="ee798b32b5133700"></a>
### Description

Log flusher of GOLDILOCKS is a system thread which flushes the log buffer contents to disk logfile. When log flusher wakes up in the idle phase, it checks if log to flush exists. Then it flushes the log if any.  
If the log flusher did not flush within the time set in LOG_SYNC_INTERVAL, it synchronizes the log buffer and the log file by performing a flush until the last block of the current log buffer.

<a id="5392a4c9de6fea24"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="b04b0ef49a741b3b"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="16cd13da4f19c952"></a>
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

<a id="ad5eb5ea3a366726"></a>
### Description

It is the millisecond interval for synchronize log.

<a id="19aad2fe62baa4a6"></a>
## MAX_GROUP_COUNT

<a id="84956bce91fc46a6"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="08626770dab19f9f"></a>
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

<a id="5810e0bd0dca3fc0"></a>
### Description

It is the maximum group count in the cluster system.

<a id="174235a9a74439c2"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="8f0adf497fcacd6d"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="0be48f0afb162d1d"></a>
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

<a id="ddb5bb8d07872e89"></a>
### Description

It sets the maximum size (quota) of the global journaling file which internally stores journaling data when a journaling occurs in cluster system.

<a id="e05dc088a51fe509"></a>
## MAX_NODE_COUNT

<a id="179e7e930ffa9db4"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="3b44cb352ef7571a"></a>
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

<a id="a950c9e41bea1403"></a>
### Description

It is the maximum node (instance) count which can join the cluster system.

<a id="270deb1019b2d297"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="b0e8b16eeaf2e22d"></a>
### Basic Information

**Basic Information of MAXIMUM_CONCURRENT_ACTIVITIES**

<a id="b02517fa68caad86"></a>
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

<a id="6472a4cb715b167d"></a>
### Description

It sets the number of statements which can be executed simultaneously.

<a id="35e269bc8b957dbf"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="d083fdc5336a2388"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="5333cae171b664da"></a>
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

<a id="b6d3b68e23ced8a4"></a>
### Description

It sets the maximum number of file caches which is being used in the session.

<a id="b025fccd1359c56b"></a>
## MAXIMUM_FLANGE_COUNT

<a id="b8f9d7554a567c68"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="60976cd057fc50c0"></a>
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

<a id="b8b1137df248d788"></a>
### Description

It is the maximum number of flanges which can be expanded in plan clock.

<a id="71b3d691b0589a47"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="d5597cd56bc7ce8a"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="077b6300f633c229"></a>
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

<a id="4c1989d3f69aeb9d"></a>
### Description

It sets the maximum number of pages which can be recorded per disk writing operation. If the pages in the disk tablespace are updated in the buffer, then IO thread records them on the disk. If recording nearby pages together when performing disk writing operation, then it increases the efficiency of the system resource by decreasing the number of disk recording.

<a id="79789bf6b4210041"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="eca6bb421669e52e"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="2a897ca5efd261f6"></a>
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

<a id="21b8886ac5aa9458"></a>
### Description

When flushing the contents of the log buffer to disk log file, it sets the maximum number of log blocks to be flushed with a single writing operation.

<a id="9ffb198d8cb15d1c"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="2133198f8ac1fb7f"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_PAGE_COUNT**

<a id="e9df1e4cf53b3b61"></a>
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

<a id="0638f166d5bbf794"></a>
### Description

GOLDILOCKS datafiles are flushed to the disk by the checkpoint and certain DDL statements. For flushing datafiles, it sets the maximum number of data pages to be flushed with a single writing operation.

<a id="fc4dd63e4dc5d7f6"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="e1890ab4138c86bf"></a>
### Basic Information

<a id="d69b762f8c1f0cb8"></a>
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

<a id="4bb91d4e623cedab"></a>
### Description

When rebuilding the index on ONLINE mode, it can be performed together with DML, and DML records the updates on the journal log. The index is rebuilt based on the data at the time of beginning of the rebuilding, then the updated data during the rebuilding is applied to the index through the journal log. The journal logs are initially applied, then journal logs which were accumulated while applying the journal logs are applied. This property sets how may times the journal logs are applied in this way.

<a id="73bdf3708d122213"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="33d812beef664f96"></a>
### Basic Information

<a id="047acd78b4883258"></a>
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

<a id="5ebc6c39e11b9fc2"></a>
### Description

The table rebalancing online can be performed together with DML in the cluster environment, and DML records the updates on the journal log at that moment. The table rebalancing initially applies the journal logs which occurred during synchronizing tables, then applies journal logs which were accumulated while applying the journal logs. This property sets how may times the journal logs are applied in this way.

<a id="cfa1736a1728808c"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="f7a4b250fb097e26"></a>
### Basic Information

**Basic Information of MAXIMUM_NAMED_CURSOR_COUNT**

<a id="53278a832e63a951"></a>
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

<a id="c78ac000ba6d4711"></a>
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

<a id="3bd4460bd15278dc"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="0ada435b7a098bdc"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="8cbe31d984a25e18"></a>
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

<a id="08a18ca222cf58ef"></a>
### Description

It is the maximum number of package instances which are available in a single session.   
A package instance is created when using the stateful package in the session.

<a id="3fd76794d9f73db5"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="5e6beb83068432d0"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="8ff0a2f1ade5f103"></a>
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

<a id="e39e974791c93f24"></a>
### Description

It sets the maximum buffer size available in a single session which is connected to shared mode.  
For more information, refer to [DISPATCHER_CM_BUFFER_SIZE](#03348850a71c3292).

<a id="fdf7f1db910b7235"></a>
## MEASURE_CLUSTER_LATENCY

<a id="079cf71b512a57f3"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="12c576f12b3aebfc"></a>
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

<a id="7754c26dc16e0c9a"></a>
### Description

It is the measure cluster latency.

<a id="6bd79338ef50d862"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="535918dddfaa24ec"></a>
### Basic Information

**Basic Information of MEMORY_MERGE_RUN_COUNT**

<a id="e637e17d3f1d5e3d"></a>
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

<a id="673b41e786b8f07f"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in certain block size (MEMORY_SORT_RUN_SIZE) units, merging the sorted blocks, and generating the internal node. MEMORY_MERGE_RUN_COUNT sets the number of the sorted blocks to be merged at a time.

<a id="e8776cb38f349d92"></a>
## MEMORY_SORT_RUN_SIZE

<a id="d15bb624e855af67"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="1c719227b5eb6bda"></a>
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

<a id="0d03dc674bdd218d"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in a certain block size (MEMORY_SORT_RUN_SIZE) unit, merging the sorted blocks, and generating the internal node. MEMORY_SORT_RUN_SIZE sets the size of a single block to be sorted.

<a id="b04be52f7248ccb2"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="ddd6057a9790e105"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="6ea0992d5a66ae5f"></a>
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

<a id="64bc1145da281680"></a>
### Description

It is the minimum number of sampling rows when executing [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#30fc30b6cd667055) by using the sampling.

<a id="32b134fcc1da2809"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="2d00f7d97b96f2cf"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="908d6f60f7268c48"></a>
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

<a id="a30568197b51eb68"></a>
### Description

DML uses the undo page to store the previous image. Undo page is consumed by using a single undo segment per DML. If all allocated pages of undo segments are consumed, the page of another undo segment can be used. MINIMUM UNDO PAGE_COUNT is the minimum number of undo page to specify the undo segment to import page when undo pages are insufficient. If the undo pages are insufficient, the pages can be imported only from the undo segment having more pages than MINIMUM UNDO PAGE_COUNT.

<a id="fd354d00b3351f23"></a>
## NET_BUFFER_SIZE

<a id="d89697fe8b6f1a50"></a>
### Basic Information

**Basic Information of NET_BUFFER_SIZE**

<a id="d4f812f567a16ffa"></a>
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

<a id="f37fc8179b47648a"></a>
### Description

It sets the TCP communications buffer size.   
In the dedicated mode, it is set to the maximum communication packet size.  
In the shared mode, it is set to [DISPATCHER_CM_UNIT_SIZE](#e2a66ec4e90fa395).

<a id="f225d3a5b17e6d4e"></a>
## NLS_DATE_FORMAT

<a id="ab985cdaedf3a88d"></a>
### Basic Information

**Basic Information of NLS_DATE_FORMAT**

<a id="f2adcc4282f5485b"></a>
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

<a id="39593e1c0d824ce5"></a>
### Description

NLS_DATE_FORMAT specifies the default date format of TO_CHAR and TO_DATE functions.

<a id="7158a76ad2c0e3ca"></a>
## NLS_TIME_FORMAT

<a id="e361ae2608931f96"></a>
### Basic Information

**Basic Information of NLS_TIME_FORMAT**

<a id="64a8613fdcbddb82"></a>
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

<a id="761467365c301fbc"></a>
### Description

NLS_DATE_FORMAT specifies the default time format of TO_CHAR and TO_DATE functions.

<a id="41f3a85cc18588b8"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="88931a67b06f655c"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="2ca9572647e9c2f8"></a>
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

<a id="d2ad314409a52e53"></a>
### Description

NLS_TIME_WITH_TIME_ZONE FORMAT specifies the default time with time zone format of TO_CHAR and TO_TIME_WITH_TIME_ZONE functions.

<a id="43c4980b87076f57"></a>
## NLS_TIMESTAMP_FORMAT

<a id="f49c6768b2b62c6a"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="f929d9171a5dd2ea"></a>
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

<a id="aa049891fac267de"></a>
### Description

NLS_TIMESTAMP_FORMAT specifies the default timestamp format of TO_CHAR and TO_TIMESTAMP functions.

<a id="dd69442f6469d388"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="4dc07824d0dfe946"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="f823ba8d5b4c5245"></a>
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

<a id="f5033bb4d38a997d"></a>
### Description

NLS_TIMESTAMP_WITH_TIME_ZONE FORMAT specifies the default timestamp with time zone format of TO_CHAR and TO_TIMESTAMP WITH TIMEZONE functions.

<a id="5877207c753bb727"></a>
## NUMA

<a id="b4259358733138da"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="3a545c754ee0edc4"></a>
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

<a id="06088158fa1099dc"></a>
### Description

It enables NUMA.

> To use the NUMA property in AIX, the user account should be modified. Execute the following command as a root user.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> &lt;username&gt; is not a root but it is a user account of AIX.  
> Logout then login again to apply the modifications.

<a id="90cb8af5aeaaa5a2"></a>
## NUMA_MAP

<a id="a9abc77ec954087b"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="4ef5fabda19b7343"></a>
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

<a id="2851332ddc96f665"></a>
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

<a id="211bcf72ad7f4081"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="dd2de581741ed38a"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="6888426daece74dd"></a>
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

<a id="b9e1348e6e1e3aeb"></a>
### Description

The background process automatically takes the errored member offline after completing the failover caused by the node error.   

If it is not possible to take the errored member offline because it is set to *NO*, then execute the following syntax before the errored member joins the system again.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="b2a70bc1314a1b6b"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="10b4231de17ef499"></a>
### Basic Information

<a id="0dcce8d4dc18673d"></a>
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

<a id="b384ffa8a36416de"></a>
### Description

DML performed during rebuilding the index on ONLINE mode records the journal log. The journals are applied to the index multiple times when finishing rebuilding the index. [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#fc4dd63e4dc5d7f6) sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="0e684339551b7aaa"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="26e1970b52863748"></a>
### Basic Information

<a id="3d1d63d9e8499a5e"></a>
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

<a id="ba1e01660c18a49b"></a>
### Description

The table rebalancing online applies journal logs several times which were recorded by dml occurred during the performance in the cluster environment. MAXIMUM_JOURNAL_REPLAY_COUNT sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="5ab9fec5d6b0f300"></a>
## OS_GROUP_ACCESS

<a id="ca027d6ed9f223bb"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="52ca35e78b28dfcc"></a>
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

<a id="d071b76664cfd73c"></a>
### Description

To connect to DA with another user of the same group, this property should be set to *YES*. Also, the umask of the system should be modified to *0002*.

<a id="7640c5280aa1118e"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="34a52dfbab110ccc"></a>
### Basic Information

<a id="ebe1552fd430d4f4"></a>
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

<a id="78d37b7e49e65391"></a>
### Description

If the data size to be sent to the client is bigger than PACKET_COMPRESSION_THRESHOLD, it compresses the communication data.

<a id="5c6efe925534f941"></a>
## PAGE_CHECKSUM_TYPE

<a id="44238416ee6b0e77"></a>
### Basic Information

**Basic Information of PAGE_CHECKSUM_TYPE**

<a id="4b9d4e61f88f46dd"></a>
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

<a id="1a88c0261c44507b"></a>
### Description

A checksum is used to guarantee the physical consistency for each page of the datafile. GOLDILOCKS supports a page checksum of LSN, CRC scheme.

- 0: LSN
- 1: CRC

<a id="bd0452b8c0fee899"></a>
## PARALLEL_IO_FACTOR

<a id="2921d2bcdd41e93d"></a>
### Basic Information

**Basic Information of PARALLEL_IO_FACTOR**

<a id="3168d23c731c4b43"></a>
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

<a id="16e124d6f4321f64"></a>
### Description

It sets the number of threads for the parallel loading of data file when starting database and the number of threads for parallel recording of data file at checkpoint.

<a id="ef9213258c34ca6b"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="0a1190a74b3bc98e"></a>
### Basic Information

**Basic Information of PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16**

<a id="ef933e70fea2733e"></a>
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

<a id="f0f6de4de197b16e"></a>
### Description

It sets the group directory for parallel I/O of data file. It sets the number of group as many as PARALLEL_IO_FACTOR, then parallel I/O is performed in data file unit which belongs to each group.

<a id="cef737b5ec48da88"></a>
## PARALLEL_LOAD_FACTOR

<a id="cf93a893051dc8e3"></a>
### Basic Information

**Basic Information of PARALLEL_LOAD_FACTOR**

<a id="c4268a8e6c3f022e"></a>
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

<a id="7aa647992db16324"></a>
### Description

When starting database, it sets the number of threads for parallel operation after loading the memory of a data file.

<a id="86c237840354b7f0"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="af5c40911ac4c4ac"></a>
### Basic Information

**Basic Information of PENDING_LOG_BUFFER_COUNT**

<a id="89666633395012e3"></a>
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

<a id="6bfe587eb5b28437"></a>
### Description

When multiple transactions are simultaneously running, the pending log buffer is used to reduce the competition for the log buffer. PENDING LOG_BUFFER COUNT sets the number of pending log buffer which can be used simultaneously.

<a id="d45608ff97c4bd7c"></a>
## PLAN_CACHE

<a id="9ef96c1d206d5de7"></a>
### Basic Information

**Basic Information of PLAN_CACHE**

<a id="98c320c7ec32ef01"></a>
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

<a id="a750b5583897e161"></a>
### Description

It determines whether to use the plan cache.

<a id="e29ea70898ef1334"></a>
## PLAN_CACHE_SIZE

<a id="6d20cd0b779e37f6"></a>
### Basic Information

**Basic Information of PLAN_CACHE_SIZE**

<a id="b9d154b4ad63457d"></a>
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

<a id="38c2ff69107b0da9"></a>
### Description

It sets the memory size to be used for the plan cache.

<a id="0f6636d35ba1083a"></a>
## PLAN_HISTORY

<a id="cf8a86bf647ca604"></a>
### Basic Information

<a id="0bc6b3a0dea24ebf"></a>
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

<a id="08ce7794c0c65393"></a>
### Description

It sets whether to use the plan history.

<a id="15548e9ceb65ea36"></a>
## PLAN_HISTORY_SIZE

<a id="f36614a7f02607e4"></a>
### Basic Information

<a id="cd3d14b05bd64bf9"></a>
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

<a id="92152d68914bf798"></a>
### Description

It sets the number of plans to be stored in the plan history.

<a id="ecc4eaa33c62333c"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="497e00cf6b822cfc"></a>
### Basic Information

<a id="8a56c109efe918e2"></a>
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

<a id="d2dcd9c3ca9f6ab2"></a>
### Description

It sets the initial size of the heap memory to use in the session. Even when there are memories which are not used in the session, the memories are not returned to operating system.

<a id="7fc4815c858d2517"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="d70b0b019bc14e35"></a>
### Basic Information

<a id="5ff8bff2dd07dd3b"></a>
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

<a id="4dead9c066ec5927"></a>
### Description

It sets the size of memory to extend when the session allocates additional heap memory.

<a id="8916e2028ef8542c"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="30068107a84898ef"></a>
### Basic Information

<a id="f3e7f8e4d486962f"></a>
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

<a id="5411b40db7f04ce3"></a>
### Description

The memory size is preserved as big as this property even when there are unused heap memories in the session, and those memories are not returned to the system but are reused in the session.

Even when it is set to smaller than PRIVATE_STATIC_AREA_INIT_SIZE, it is not decreased to smaller than the size.

<a id="697022ef0dc019e2"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="3e79cb8b677ab73f"></a>
### Basic Information

**Basic Information of PRIVATE_STATIC_AREA_SIZE**

<a id="0820895f1ec325be"></a>
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

<a id="d0f7e97861278ec4"></a>
### Description

It specifies the maximum heap memory size to be allocated by the session.

<a id="cb34e53e9bfbacdd"></a>
## PROCESS_MAX_COUNT

<a id="2990e33fdd7f2160"></a>
### Basic Information

**Basic Information of PROCESS_MAX_COUNT**

<a id="a4dc9fe923824b45"></a>
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

<a id="c67a2845d43a644e"></a>
### Description

It specifies the maximum number of processes (threads) available on the system.

Creating system process  
• The process is created each time of connection to D/A mode or C/S dedicated mode.  
• In C/S shared mode, processes are basic balancer, dispatcher and shared-server. A process is   
&nbsp;&nbsp;not created when connecting from client.

<a id="2d02e0a99199225b"></a>
## QUERY_TIMEOUT

<a id="953ded6b45297d6c"></a>
### Basic Information

**Basic Information of QUERY_TIMEOUT**

<a id="436528be7c2bcecf"></a>
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

<a id="616f63ca6180946d"></a>
### Description

It specifies the maximum time which a command received from the session can be executed. If the execution time exceeds, the TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="a5b5c8d0c1d783f1"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="c038ff59914bcb16"></a>
### Basic Information

**Basic Information of READABLE_ARCHIVELOG_DIR_COUNT**

<a id="9f77f56db5a72af6"></a>
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

<a id="4bfe3c544c6620af"></a>
### Description

It sets the number of directories in which archive redo logs exist when executing media recovery.

<a id="128312c651195083"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="016c6990d9398fd6"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="49b942d834e2d169"></a>
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

<a id="46722539cd5628a7"></a>
### Description

It sets the number of directories in which incremental backups exist when restoring files using incremental backups.

<a id="9b051374a7f174a1"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="2fb4dfd398db261d"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="63d80821aa69aac4"></a>
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

<a id="866847e3b759168b"></a>
### Description

It is the block read count for rebalance.

<a id="25d74a8e4dcd8fb4"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> It is not supported after 3.1.

<a id="361008117f8b0e54"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="b866fafc4d68db35"></a>
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

<a id="67e85fcb4a73539b"></a>
### Description

It sets the minimum page count to check if the plan is recompiled due to the page count modification.

<a id="55503b6088117989"></a>
## RECOMPILE_PAGE_PERCENT

> It is not supported after 3.1.

<a id="fbb63f0016cc0224"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="bfe9cd37b8d8cdf0"></a>
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

<a id="8cbf4a5c9e3db14f"></a>
### Description

It sets the page percentage when recompiles the plan due to the page count modification. If its value is 0, it does not recompile due to the page count modification.

<a id="8b8ccbe23a71264c"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="8d5311ed18b8d960"></a>
### Basic Information

<a id="53b259232545e8c7"></a>
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

<a id="5b59a092b629bfab"></a>
### Description

It is the default log buffer size for recovery.

<a id="271e64a9002836f6"></a>
## RECYCLEBIN

<a id="fade91c537054427"></a>
### Basic Information

<a id="724c243a44e01671"></a>
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

<a id="5976fa48a6bd64a3"></a>
### Description

It sets whether to activate the recyclebin feature.

<a id="cbb38cc250214ddc"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="357397ad3d1e669d"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="597260c1c842bf1e"></a>
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

<a id="bd3e0f818ec8b65c"></a>
### Description

If the size of the created REDO LOG is bigger than REDO_LOG_COMPRESSION_THRESHOLD value, it compresses REDO LOG.

<a id="f2f607e181efc7de"></a>
## REFINE_RELATION

<a id="2a8797357918048b"></a>
### Basic Information

<a id="b6aff57679ed8abc"></a>
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

<a id="06a0606c7206ebed"></a>
### Description

If this property is set to NO, then REFINE RELATION process is not performed when restarting the server.

This property can be used when an error occurs during the REFINE RELATION process. However, segments of RELATIONs (tables or indexes) which were dropped but not REFINEd can not be reused. When resolving the error then setting this property to YES and restarting, it tries to REFINE relations which were not dropped.

<a id="abff02de68596df4"></a>
## SESSION_FATAL_BEHAVIOR

<a id="7af86ffa3504ba9d"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="21bbe6d9e0956807"></a>
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

<a id="25647eee0aedae70"></a>
### Description

When session fatal occurs, it determines whether to terminate only the thread which caused the fatal or to terminate the process.

- 0: It terminates only the thread which caused fatal.
- 1: It terminates the process.  
  If multiple sessions are simultaneously performed in the process, the process is terminated after all sessions finish using database.

<a id="6a9ae6bddacf27ef"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="a56185bde17b3c59"></a>
### Basic Information

<a id="c601fd6f1cf7e83d"></a>
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

<a id="29259a33688c3ccc"></a>
### Description

It sets the shared memory size to be allocated in advance so that it can be used in the session.

<a id="92dde93ae12443c8"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="87f3a413e46b043e"></a>
### Basic Information

<a id="a5c3acc4b33b2bf5"></a>
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

<a id="76159881bd3cefa9"></a>
### Description

It sets the threshold value to determine whether to return the dynamic shared memory which is not used by the session to the system when releasing the dynamic shared memory used in the session. In other words, if the memory chunk which is bigger than the set value among unused memory exists, then it is returned to the system.

<a id="346450cd5aec1c6c"></a>
## SHARED_MEMORY_ADDRESS

<a id="22b3665d9686f8e5"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_ADDRESS**

<a id="b9d072505b76f471"></a>
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

<a id="1716e94f640023ec"></a>
### Description

It specifies the address of Shared Static Area (SSA).

<a id="8c758b0eb012e6c8"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="70a92b916a4c01e3"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_KEY**

<a id="1541ffbf51015c04"></a>
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

<a id="683425e3efb0201f"></a>
### Description

When running server, it specifies the shared memory key values which are used to allocate Static Shared Area (SSA) space.

<a id="ba77a134587ee253"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="0079ce9fa8b94435"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_NAME**

<a id="9191d801fdef5ace"></a>
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

<a id="fbbe305b30727c76"></a>
### Description

When running server, it specifies the shared memory name which is used to allocate Static Shared Area (SSA) space.

<a id="21a645ba81300a01"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="b1361b9c7c27de35"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_SIZE**

<a id="5d233f777bcf73db"></a>
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

<a id="4031f7ac8bce96d4"></a>
### Description

It specifies the size of the Shared Static Area (SSA).

<a id="d1519aa2c72fac36"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="aa7dece6967d4beb"></a>
### Basic Information

**Basic Information of SHARED_REQUEST_QUEUE_COUNT**

<a id="12e84d3589d0379b"></a>
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

<a id="47822f8572d89976"></a>
### Description

In shared mode, it sets the number of queues of which the dispatcher requests to the shared-server. A queue is used when multiple dispatchers allocate user's requests to the shared-server. Generally, a single queue is used for the load-balance.   
However, SHARED_REQUEST_QUEUE_COUNT value is increased because if the number of dispatchers and shared-servers increase, then a conflict to the queue causes performance degradation.   
If the value becomes bigger, the load-balance can be inefficient and the possibility of deadlock increases.

<a id="9d9358740604ed14"></a>
## SHARED_SERVERS

<a id="e3c6de08561cd186"></a>
### Basic Information

**Basic Information of SHARED_SERVERS**

<a id="26d481f8d5eff2dd"></a>
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

<a id="cdaa3c0b19e5460d"></a>
### Description

It sets the number of shared-server processes on shared mode.  
At open phase, the value can not be decreased by using alter system.

<a id="a42640a416209e2d"></a>
## SHARED_SESSION

<a id="27782d38552b785a"></a>
### Basic Information

**Basic Information of SHARED_SESSION**

<a id="08d5aeb5bde5a7aa"></a>
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

<a id="03a8c17611e6b898"></a>
### Description

It sets whether to activate shared mode. If the value is set to *NO*, load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver) are not executed.

<a id="a09339d5a304db42"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="e3f8795c5722c768"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="55b76a42e2822eee"></a>
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

<a id="605058ba01fccba6"></a>
### Description

It sets the maximum holding time of the statement required for the snapshot read. TIMEOUT error occurs for a snapshot statement which exceeds the time.

<a id="4427da1cb368eb6b"></a>
## SQL_HISTORY_SIZE

<a id="bc1d1a3ae211d151"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="18d0043e4c876ecd"></a>
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

<a id="e596f64208a8c354"></a>
### Description

It is the history size for SQLs.

<a id="7c8140a3febd3f0b"></a>
## SQL_HISTORY_TYPE

<a id="ad200e9e30f30111"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="06da0c4e192ce4ee"></a>
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

<a id="aa86eb9d67e64ed0"></a>
### Description

It is the history type for SQLs.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="a779f6b753ca04d7"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="e730ea8e60a412b0"></a>
### Basic Information

**Basic Information of SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY**

<a id="c737bf20dd1c2f73"></a>
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

<a id="7cf1e62ef5a125c5"></a>
### Description

It records supplemental log for all changes in the database.

<a id="b2a240135509d84e"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="d147dfa4e9a8f533"></a>
### Basic Information

<a id="09acb0ebea05ebac"></a>
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

<a id="7a19240c9822642a"></a>
### Description

It sets the initial DISK_DATA_TBS tablespace size when creating the database.

<a id="03bd7d1abb54a702"></a>
## SYSTEM_FILE_IO

<a id="f299573d64e4eede"></a>
### Basic Information

<a id="2dbe683bbe8dcdcf"></a>
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

<a id="fd9031aefb1f350d"></a>
### Description

It sets IO type of when using the database file except for the data file and the log file.

<a id="64e80d182c719cc3"></a>
## SYSTEM_LOGGER_DIR

<a id="d92497ec424dd035"></a>
### Basic Information

<a id="f53cc7a8e4cc54a4"></a>
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

<a id="b4bb23d7d4acaa6c"></a>
### Description

It sets the disk path on which the trace log message is recorded.

<a id="d00cee8300164acf"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="c4946cb7ee4a95b9"></a>
### Basic Information

<a id="d944ca8937b8ec7c"></a>
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

<a id="c37dc7fd1c422516"></a>
### Description

It determines the size of initial MEM_AUX_TBS tablespace when creating the database.

<a id="38020ab7ba623c53"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="d8d179c1fc8fce92"></a>
### Basic Information

<a id="09fe39f4962bdbb8"></a>
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

<a id="dd26cb60223869a7"></a>
### Description

It determines the initial tablespace size of MEM_DATA_TBS when creating database.

<a id="107b6dd15abc5019"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="c9b6099f16cb5dc5"></a>
### Basic Information

<a id="9f6448af9aad40d4"></a>
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

<a id="52acf9fea054111b"></a>
### Description

It determines the initial tablespace size of DICTIONARY_TBS when creating database.

<a id="0a0ab906bd34adc6"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="a15d0e7e70ac6d4d"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE**

<a id="3850dcd69e9b4cf3"></a>
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

<a id="8dfe5d488b6b2680"></a>
### Description

It determines the initial tablespace size of MEM_TEMP_TBS when creating database.

<a id="d872475f298e6da6"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="8d1de846d3efdd52"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE**

<a id="4bbdca0cfcb5fcce"></a>
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

<a id="c61cc1d397f389a4"></a>
### Description

It determines the initial tablespace size of MEM_UNDO_TBS when creating database.

<a id="34d94b6ff00c2639"></a>
## SYSTEM_TABLESPACE_DIR

<a id="0e2c347048dcb78b"></a>
### Basic Information

<a id="3199d3794d47d282"></a>
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

<a id="a9b14fecdab8d9aa"></a>
### Description

It sets the path to which the initial system tablespaces are stored when creating database.

<a id="faeed683af780c44"></a>
## SYSTEM_UDS_DIR

<a id="bdb3b025a8629c77"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="0b16b6c80bcc6bef"></a>
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

<a id="ac0da7efc8f63f0f"></a>
### Description

It sets a directory on which the unix domain socket file is created.  
Setting the directory for the unix domain socket except for DB system, such asglsnr, is managed by a separate configuration file.  
The maximum setting value is 60 bytes. (The maximum size of the absolute path (directory + file name) for the unix domain socket file varies according to OS, but generally it is around 100 bytes.)

<a id="92befe8e6f0b8b7c"></a>
## TCP_CLIENT_NUMA_NODE

<a id="0690fe812732fcd3"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="253539a2327679e2"></a>
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

<a id="fc0e0decf1cb2651"></a>
### Description

It sets the NUMA node ID to which the client server session is bound. This property is operated when NUMA property is set to on.

<a id="16573cfbcbb6e496"></a>
## TCP_NODELAY

<a id="47b5eec6cde08324"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="fb76d37a1813ddc3"></a>
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

<a id="461e1894731d46f7"></a>
### Description

It sets TCP_NODELAY option of the socket when transferring the data to a client in C/S method (TCP socket).  
Set it to *NO* when fast latency is not required and reducing the network load is needed.

<a id="da81cdda6f7266a3"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="11660a8aaf7e6098"></a>
### Basic Information

<a id="db2844a314f14185"></a>
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

<a id="1cfe559a4539947d"></a>
### Description

It sets the number of segments to be cached in a session instead of returning them to a tablespace when dropping a global temporary table or a global temporary index segment. Segments in the segment cache are reused later in a global temporary table or a global temporary index.

- 0: It does not use a segment cache of a global temporary table or of a global temporary index in a session.
- 1 ~ 4294967295: It keeps the specific number of segment caches of a global temporary table or a global temporary index in a session.

<a id="be066a02da8772a9"></a>
## TEMP_UNDO_ENABLED

<a id="0a04083f4011a7c5"></a>
### Basic Information

<a id="6362ece70808cd6c"></a>
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

<a id="a071810ab459ea8a"></a>
### Description

It defines the location of logging undo records for a global temporary table.

- 0 (FALSE): It records the undo records in the default undo tablespace of database. 
- 1 (TRUE): It records the undo records in the default temporary tablespace of database.

<a id="c2ec822aa3b3de9a"></a>
## TIMED_STATISTICS

<a id="2128e6e69c1918c5"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="d2812971b467c8bf"></a>
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

<a id="a7e22cee765c2f95"></a>
### Description

It is whether to check the wait event.  
To record the statistics related to wait event on v$system_event, v$session_event and v$session_wait table, set this property.

- 0: It does not record the statistics.
- 1: It records the statistics.
- 2: It records the statistics by using the high precision timer.

<a id="e3fb26d21297b93a"></a>
## TIMER_INTERVAL

<a id="27ba8ac9b6529c5b"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="ef9c3b2490e323e4"></a>
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

<a id="0b90593b9414d943"></a>
### Description

It sets the time interval which is required when the timer thread sets the system time.

<a id="add5466e40448a63"></a>
## TIMEZONE

<a id="e587bfe4e23eab98"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="9a1975476c034ceb"></a>
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

<a id="c9206fa867cd60d1"></a>
### Description

It is a time zone value of database.  
It is applied when creating database, and it uses the value of the range from '-14:00' to '+14:00'.

<a id="6d4b7d03e1ec5d02"></a>
## TRACE_ALTER_SYSTEM

<a id="e2b7c8e9b44997a6"></a>
### Basic Information

**Basic Information of TRACE_ALTER_SYSTEM**

<a id="249d6a3229886056"></a>
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

<a id="99d1948e789e8f4c"></a>
### Description

It records the SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) when executing ALTER SYSTEM syntax.

Set TRACE_ALTER_SYSTEM property to *ON* to record system changes.

SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax have nothing to do with TRACE_ALTER_SYSTEM property, so they do not affect the performance of TRACE_ALTER_SYSTEM.

<a id="c256de99f037631c"></a>
## TRACE_DDL

<a id="c53ded5b2ebf2f80"></a>
### Basic Information

**Basic Information of TRACE_DDL**

<a id="ed8d6b10f7490549"></a>
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

<a id="7f4ceb9a0662c885"></a>
### Description

When executing DDL, it records the executed SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

Set *TRACE_ALTER_SYSTEM* property to *ON* to record SQL statements execution such as CREATE/DROP/ALTER table.

TRACE_DDL property affects only to DDL statements. However, it has nothing to do with SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax. Therefore, it does not affect the performance.

<a id="7d9bb4095129a530"></a>
## TRACE_LOG_ID

<a id="555a4db799d35e5c"></a>
### Basic Information

**Basic Information of TRACE_LOG_ID**

<a id="c1fe0c392fe3c561"></a>
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

<a id="c1a6c691bc8a5e63"></a>
### Description

The execution plan for the query, and other related information are recorded in the trace file (opt_p[process ID_s [session ID].trc) under the trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) when processing queries.

To record SQL statement for the query, the execution plan and the execution time, refer to the following flag information.

**Flag information for TRACE_LOG_ID**

<a id="508b2a41f8417386"></a>
| Information | Flag(on) | Flag(off) |
| --- | --- | --- |
| Whether to output the successful SQL query | 100000 | 0 |
| Whether to output the failed SQL query | 10000 | 0 |
| Whether to output the execution plan | 1000 | 0 |
| Whether to output the execution type (direct/prepare) | 100 | 0 |
| Whether to output the bind value | 10 | 0 |
| Whether to output the execution time per section | 1 | 0 |

To set it in a form of "output the successful SQL query" + "output the execution plan" + "output the bind value", set the TRACE_LOG_ID value to 101010.

<a id="9ef11ef748ca24e3"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="9f157da982cd22cc"></a>
### Basic Information

<a id="a5ad40006373dd86"></a>
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

<a id="721d2536e37416f9"></a>
### Description

It sets the size of the heap memory buffer which is used to configure the log message to be recorded in the trace logfile.

<a id="1440ee0e87acca1d"></a>
## TRACE_LOG_TIME_DETAIL

<a id="a441158091552a3c"></a>
### Basic Information

**Basic Information of TRACE_LOG_TIME_DETAIL**

<a id="663032e126334004"></a>
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

<a id="2ae339aa989974e1"></a>
### Description

It sets whether to increase the time accuracy when recording trace log.  
If the value is ON, it has an accuracy of 1 us.  
If the value is OFF, it has an accuracy of 10 ms.

<a id="93050edeacb93cd0"></a>
## TRACE_LOGGER

<a id="5a0e1b267b736f03"></a>
### Basic Information

<a id="080cb91877ea556c"></a>
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

<a id="329b5dae42fce7cf"></a>
### Description

It sets the target on which the trace log is written.  
If it is 1, then it is recorded in a file, and if it is 2, then it is remotely recorded in a file.  
When it is remotely written, then it remotely collects trace logs from gtrclogger and records in a file.

<a id="e6fd5a84b33d7fe5"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="dfbe622b91a750ae"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="b8b7d08b1968234b"></a>
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

<a id="aebcb3773bc44956"></a>
### Description

It sets the host to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="16017b0c1bf1ea3f"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="72acc983e582f33a"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="bedf54ca58dfa4ad"></a>
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

<a id="25fefd6c6cc2b037"></a>
### Description

It sets the port to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="a42dc970cfeb7755"></a>
## TRACE_LOGIN

<a id="7189547d5ef94e3a"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="92d75c2adab97a69"></a>
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

<a id="f19f325bea19df00"></a>
### Description

It records the related access information in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc) on login.  
Set TRACE_LOGIN property to *ON* to record the related information on login.

<a id="c59033212ebf4f43"></a>
## TRACE_LONG_RUN_CURSOR

<a id="2945b931ef7afb2f"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_CURSOR**

<a id="dc5d54d6bd7f1e04"></a>
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

<a id="fc75074729b4953c"></a>
### Description

When cursor life-time is longer than the specified property time, then it records the SQL statement of the cursor in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#399e1d3f4ff93fab) property to increase the precision.

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

<a id="c9e250fcf795b12b"></a>
## TRACE_LONG_RUN_SQL

<a id="5cb6bc785f5b738b"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="14832c17528bc68f"></a>
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

<a id="b54d18d75136e560"></a>
### Description

It records the SQL statement whose execution time is longer than the specified property time in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.
    - Use [TRACE_LONG_RUN_TIMER](#399e1d3f4ff93fab) property to increase the precision.

The following is an example of recording the SQL statement whose execution time is longer than 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

The following is an example of restoring to the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="399e1d3f4ff93fab"></a>
## TRACE_LONG_RUN_TIMER

<a id="3bd1ffa8822a6104"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="138668feaca6191b"></a>
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

<a id="f60a86935c74e599"></a>
### Description

It controls the measurement precision when measuring the execution time of the SQL statement by using the following properties.

- [TRACE_LONG_RUN_CURSOR](#c59033212ebf4f43)
- [TRACE_LONG_RUN_SQL](#c9e250fcf795b12b)

- Description of value
    - 0: It uses the timer thread whose interval is 10 milliseconds.
    - 1: It measures the time by using gettimeofday() function. In this case, the precision is higher but the system call causes the work load.

<a id="36e70bca80ae5da7"></a>
## TRACE_XA

<a id="dec453ed26c273df"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="3705ea3c6e9f8525"></a>
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

<a id="bf6f87043ca09e48"></a>
### Description

It specifies whether to output trace messages when using XA interface. Message is output to the 'SYSTEM_LOGGER_DIR / xa.trc'.

<a id="862f7dac7de00c85"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="906112e7feabb784"></a>
### Basic Information

<a id="8518ef7d5234e8d9"></a>
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

<a id="981a6914d5d8b4da"></a>
### Description

It is the maximum waiting time when allocating transaction slots.

The following error occurs when the waiting time exceeds TRANSACTION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="36cd827327a5e6a9"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="8a7ad03a72b286a6"></a>
### Basic Information

**Basic Information of TRANSACTION_COMMIT_WRITE_MODE**

<a id="34def7ae3d38e2bf"></a>
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

<a id="aa202749d5c0f524"></a>
### Description

TRANSACTION_COMMIT_WRITE_MODE specifies whether a log generated by the transaction is flushed to the disk log file, when the transaction is committed. If TRANSACTION_COMMIT_WRITE_MODE is '1', the log should be flushed to the disk log file at the time of the transaction commit. Otherwise the transaction is committed regardless of log flush.

If the system is operated when TRANSACTION_COMMIT_WRITE_MODE is set to '0', the latest data will be lost when GOLDILOCKS is abnormally terminated without log flush after COMMIT transaction. It is because the logs are not recorded in this case.

Therefore, if all committed transactions should be remained (stored) in database, the system should be operated after setting TRANSACTION_COMMIT_WRITE_MODE to '1'. Or, 'ALTER SYSTEM FLUSH LOGS' statement should be explicitly performed at the time of transaction commit in order to flush log after TRANSACTION_COMMIT_WRITE_MODE is set to '0'.

- 0: no wait
- 1: wait

<a id="584a48ae5a7e324e"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="b898c31e6619732a"></a>
### Basic Information

**Basic Information of TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT**

<a id="fb9502e5eb1ed5d5"></a>
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

<a id="c302208f6d052d75"></a>
### Description

It means the maximum number of undo pages which the transaction can record. The minimum value is 1 (8 Kbytes) and the maximum value is 13107200 (100 Gbytes).

<a id="0f3b51a10fa12660"></a>
## TRANSACTION_TABLE_SIZE

<a id="b56dcaccf42b1ffc"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="94dddede78847703"></a>
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

<a id="98e83a531ff631d4"></a>
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

<a id="47f09e718ff0593b"></a>
## TRANSACTION_TIMEOUT

<a id="acf44533e7509991"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="c5053a97a9c608fe"></a>
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

<a id="68f81ba18a3e4e7d"></a>
### Description

It sets the duration of when the transaction is activated. It is used to prevent the side effects of when the transaction is activated for a long time. If a transaction exceeds the specified time, then gmaster daemon automatically terminates the session owned by that transaction.

<a id="71a8908143a9c8e1"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="a3bc46bba9a757f8"></a>
### Basic Information

<a id="130dd8ee121f329e"></a>
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

<a id="ab5fec775f0b9c79"></a>
### Description

It is the maximum waiting time when allocating undo relations.

The following error occurs when the waiting time exceeds UNDO_RELATION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="a8ed5e98828373fd"></a>
## UNDO_RELATION_COUNT

<a id="b9be7fcb90c4071c"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="6cbf32674d84439e"></a>
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

<a id="c989b7e6aa43f847"></a>
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

<a id="ef1d6c736cf8653b"></a>
## UNDO_SHRINK_THRESHOLD

<a id="71b3d58cd6c80d2d"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="c3f99a55470ead8e"></a>
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

<a id="741222799f110363"></a>
### Description

Ager thread periodically (10 seconds) checks the undo segment space. If it occupies more space than this property value, then the reusable space is returned to the tablespace. The attempt to return is made until the undo segment space remains as big as this property (byte), and the return is finished when the amount of the remaining undo page becomes smaller than MINIMUM_UNDO_PAGE_COUNT.

<a id="9549775ae2407d7c"></a>
## USE_LARGE_PAGES

<a id="7a9146b5a2fd8972"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="4dd71604d20cbe40"></a>
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

<a id="7ac04f84b52b0159"></a>
### Description

It uses HugePage. HugePage should first be set in the device to use USE_LARGE_PAGES property.

- 0: It does not use the large page.
- 1: It uses the large page. When it fails to allocate the shared memory, then an error occurs.
- 2: It tries to allocate the shared memory by using the large page. When it fails to allocate the shared memory, then it allocates the memory by using the regular page.

> It can be used in Linux kernel 2.6.32-573 or higher.

<a id="c094f7c1f76eb5dd"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="1dda74a578b671a0"></a>
### Basic Information

<a id="771cb680f0e8b1e2"></a>
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

<a id="755c68226d7c9bbd"></a>
### Description

It sets the default media type if the media type of the tablespace is omitted when creating the user data tablespace. 0 is memory and 1 is the disk.

<a id="e54ea947ebdf6d19"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="8b3c6928e0f1fe47"></a>
### Basic Information

<a id="dc5db265ec7330dc"></a>
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

<a id="e6ea3f00bde4cc3f"></a>
### Description

It sets the default size if the data file size is omitted when creating the user data tablespace or adding the data file.

<a id="e4b4cdadc701998c"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="afa7a2afdf12e1de"></a>
### Basic Information

<a id="1a6bb55d34abe62f"></a>
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

<a id="6671faa018d17af3"></a>
### Description

It sets the default size if the size to be extended is not set when it is required to extend the data file of the user disk data tablespace.

<a id="c074bd1e8ec078ef"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="b310bb7f29a95987"></a>
### Basic Information

<a id="a8b70916e4e1bbd4"></a>
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

<a id="597669b51628f328"></a>
### Description

It sets the default size if the data file size is omitted when creating the user temp tablespace or adding the data file.

<a id="36813f733037d933"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="ede110647720b48f"></a>
### Basic Information

<a id="373aed0ed0d4b9ad"></a>
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

<a id="a9ae47581b5db3ad"></a>
### Description

It is the maximum waiting time of xa transaction in idle (The duration between the beginning of XA and the next transaction). If it remains in Idle exceeding this time, then xa transaction is rolled back.

If it is set to 0, then XA infinitely waits even in idle.

---

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
