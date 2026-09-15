<a id="6c2d42da1f4f968c"></a>

# 10. Server Property

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/6c2d42da1f4f968c)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="db97823c74b620a1"></a>
## Server Property Information

For more information about SQL syntax to change properties, refer to the followings.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/16-sql-references.md#d5748a5f89f15f32)
- [ALTER SESSION SET property_name](../part-03-sql-manual/16-sql-references.md#c7a0e93656726619)

For more information about property types, refer to the followings.

- [V$PROPERTY](9-database-information.md#6460f1d2e272099c)
- [V$SPROPERTY](9-database-information.md#880f62d4ee4b6161)

The followings describe basic information items of property in this manual.

**Basic Information item of property**

<a id="2524ae74ec302c18"></a>
| Item | Description |
| --- | --- |
| Name | Property name |
| Summary | Short description of the property |
| Data type | Data type of the property value |
| Applicable phase | A startup phase which can be updated with ALTER SYSTEM or ALTER SESSION * NONE: Applicable phase does not exist. (If it can be updated, but applicable phase is NONE, then use *SCOPE = FILE* option.) |
| Updatable | Whether property is updatable or not * If the property value is TRUE, it is updatable.  * If the property value is FALSE, only the read-only is possible. |
| ALTER SESSION | Whether property is updatable or not by using [ALTER SESSION SET property_name](../part-03-sql-manual/16-sql-references.md#c7a0e93656726619) |
| ALTER SYSTEM | Whether property is updatable or not by using [ALTER SYSTEM SET property_name](../part-03-sql-manual/16-sql-references.md#d5748a5f89f15f32) * IMMEDIATE: The updated value is immediately reflected in all session after execution. * DEFERRED: The updated value is reflected only in the session which is connected after execution. However, it is not reflected in already connected session. * FALSE: The updated value is not reflected in the session during execution. However, the updated value is reflected after restart, (Properties are updatable by using only *SCOPE=FILE* option.) * NONE: It is not updatable. |
| MIN | If the data type is BIGINT, it is the minimum value of property. If the data type is VARCHAR, the minimum value of property is N/A. |
| MAX | If the data type is BIGINT, it is the maximum value of property. If the data type is VARCHAR, the maximum value of property is N/A. |
| Default value | Default value of the property |

<a id="33164164d39e88eb"></a>
## AGING_INTERVAL

<a id="1a96191e97502932"></a>
### Basic Information

**Basic Information of AGING_INTERVAL**

<a id="5b6f3928b12ef9a0"></a>
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

<a id="ef6bedd3da51cbc0"></a>
### Description

It sets the idle time (second) when an ager thread which deletes the previous version data does not have a job to process in MVCC based database.

<a id="bf651b98dac3207f"></a>
## AGING_PLAN_INTERVAL

<a id="852bd7d184e76e46"></a>
### Basic Information

**Basic Information of AGING_PLAN_INTERVAL**

<a id="7627ab27d98d535e"></a>
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

<a id="5adc6f4af9b0ef86"></a>
### Description

The SQL plan which is older than AGING_PLAN_INTERVAL becomes the aging target.

<a id="2dc057a21fe0d8e5"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="e899fd0e658ee50c"></a>
### Basic Information

**Basic Information of ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10**

<a id="a2707365bb27f331"></a>
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

<a id="f6e2e40117a8b80d"></a>
### Description

It specifies archiving directory of GOLDILOCKS database's online redo log file. Also, it specifies where to read of archive redo log file at media recovery. The online redo log file creates archive redo log file only in ARCHIVELOG_DIR_1.

ARCHIVELOG_DIR_1 sets only the system, but ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10 sets the session.

<a id="b21ca41464ff71bf"></a>
## ARCHIVELOG_FILE

<a id="cc8016c286c09403"></a>
### Basic Information

**Basic Information of ARCHIVELOG_FILE**

<a id="d3368e0a51247ff6"></a>
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

<a id="18074e3db96824ad"></a>
### Description

It sets the prefix of the targeted file name stored in the archive directory when archiving the online redo logfile. The archive logfile's name consists of the prefix defined in ARCHIVELOG_FILE, followed by '_', the file sequence and the file extension 'log'. For example, the online logfile with a sequence number of 0 is archived as 'archive_0.log'.

<a id="488c35940c110d6f"></a>
## ARCHIVELOG_MODE

<a id="eb60db63f45eed2c"></a>
### Basic Information

**Basic Information of ARCHIVELOG_MODE**

<a id="642f56f4dc9a31be"></a>
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

<a id="5a109c7c1745bf52"></a>
### Description

The property is applied at database creation. The archivelog mode can be set to one of the following value.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

It does not affect archive log mode during operation after database is created. The archive log mode can be modified by using *ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}* in MOUNT phase.

<a id="72adef21ed6a2810"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="4bdb83dd1c47c233"></a>
### Basic Information

**Basic Information of BACKUP_DIR_1 ~ BACKUP_DIR_10**

<a id="29e36e9b377bb199"></a>
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

<a id="ad30a1dc95456779"></a>
### Description

A backup file is created when incremental backup is executed. Then it sets a directory of backup file to be read when restoring files using incremental backup. Incremental backups are created only in the directory set in BACKUP_DIR_1.

BACKUP_DIR_1 sets only the system, but BACKUP_DIR_2 ~ BACKUP_DIR_10 sets the session.

<a id="7ec95d5a5fa34bd5"></a>
## BLOCK_READ_COUNT

<a id="4f1195c97dbff2d7"></a>
### Basic Information

**Basic Information of BLOCK_READ_COUNT**

<a id="78b0d2cfd48cf6ad"></a>
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

<a id="789de1e6388d3c0e"></a>
### Description

The SQL executes operation by reading row in the unit of BLOCK_READ_COUNT which is a row bundle. BLOCK_READ_COUNT  means the number of rows to be processed at a time when operation is executed. It is a basic unit of  pipe-lining process of execution nodes which are used in SQL query processing.

If BLOCK_READ_COUNT value is big the processing performance improves, but many memory resources are used.    
The value between 10 and 100 is recommended.  
If the value becomes bigger than 100 the resource usage increases  proportionately, but the performance improvement does not increase proportionately.

<a id="4c16634a55db2804"></a>
## BULK_IO_PAGE_COUNT

<a id="4e36cfa9039d7b36"></a>
### Basic Information

**Basic Information of BULK_IO_PAGE_COUNT**

<a id="6da25ad3a6e2de41"></a>
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

<a id="7b596cead3c9c48a"></a>
### Description

It is used when IO READ of the data file occurs during server restart, or when IO WRITE occurs during creating a data file.

The heap memory is allocated as big as BULK_IO_PAGE_COUNT * 8192 when server restarts or data file is created. If the session's PRIVATE_STATIC_AREA_SIZE is smaller than the heap memory size, an error of insufficient memory may occur. In this case, extend PRIVATE_STATIC_AREA_SIZE.

<a id="06c90f6a1ef6b2b6"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="2f278c24a971da57"></a>
### Basic Information

**Basic Information of CDISPATCHER_HOT_POLICY_INTERVAL**

<a id="69142aa3894477ad"></a>
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

<a id="9b3ea91a6f31d99f"></a>
### Description

It is the time of the busy waiting when performing the dequeue in the cdispatcher. It is a micro second unit. If this value is big, it uses more cpu but the user response time (latency) is decreased.

<a id="e5b55c7feb30c9ef"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="8e992d6771a5f6cd"></a>
### Basic Information

**Basic Information of CDISPATCHER_SOCKET_BUFFER_SIZE**

<a id="8e009083e3b1a45d"></a>
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

<a id="acf25c741da21680"></a>
### Description

It is the socket buffer(sender, receiver) size of cdispatcher.

<a id="9f71b9cdc5af8fad"></a>
## CDISPATCHER_SYNC_THREADS

<a id="9677ae1233ee0a7f"></a>
### Basic Information

**Basic Information of CDISPATCHER_SYNC_THREADS**

<a id="7557e02c68ad94a2"></a>
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

<a id="ae42bfa566405e36"></a>
### Description

It is the thread count of cdispatcher sync.

<a id="47961e204d8ac695"></a>
## CDISPATCHER_THREADS

<a id="4e513835e5ef6293"></a>
### Basic Information

**Basic Information of CDISPATCHER_THREADS**

<a id="9b757b8a056bab07"></a>
| Item | Description |
| --- | --- |
| Name | CDISPATCHER_THREADS |
| Summary | cdispatcher sender, receiver thread count |
| Data type | BIGINT |
| Applicable phase | NONE |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | FALSE |
| MIN | 1 |
| MAX | 32 |
| Default value | 1 |

<a id="3a99d09e34a5ac82"></a>
### Description

It is the thread count of cdispatcher sender and receiver.

<a id="3633168d2f3bb347"></a>
## CHARACTER_SET

<a id="6d3ee1c8afc16a4f"></a>
### Basic Information

**Basic Information of CHARACTER_SET**

<a id="d60abe40a69a6415"></a>
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

<a id="ccb71097c75425d3"></a>
### Description

It is a character set of database, and it is applied when database is created.  
The property is set to one of the following values.

**Character set**

<a id="7d814fcf50505d26"></a>
| Character set | Description |
| --- | --- |
| SQL_ASCII | ASCII standards |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standards |

<a id="e6ecf251502c667b"></a>
## CHAR_LENGTH_UNITS

<a id="67a148c07fdb9810"></a>
### Basic Information

**Basic Information of CHAR_LENGTH_UNITS**

<a id="265b129ac051eb37"></a>
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

<a id="af1dde67ba15fa64"></a>
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

<a id="39401290cd63541e"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="ac402e0a1cfccd34"></a>
### Basic Information

**Basic Information of CHECK_DEDICATE_CONNECTION_INTERVAL**

<a id="c73d7597bfadd268"></a>
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

<a id="26c1b8c7bf1fe752"></a>
### Description

It is the interval of checking for when the client forcibly cut the connection in C/S dedicate environment. The dedicate server(gserver) checks the socket, and it terminates it if it was cut. The default value is 1,000 millisecond (1 second).

<a id="790ce722e87d47b1"></a>
## CLIENT_MAX_COUNT

<a id="810eb9d3a91cd851"></a>
### Basic Information

**Basic Information of CLIENT_MAX_COUNT**

<a id="b616c73d7ca9756d"></a>
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

<a id="10587c2d450daa3d"></a>
### Description

It sets the maximum number of sessions to connect.

<a id="fbd48cf4458fbd17"></a>
## CLIENT_NUMA_POLICY

<a id="c8dfc6999ab577eb"></a>
### Basic Information

**Basic Information of CLIENT_NUMA_POLICY**

<a id="cb4cfe9e97e1ae7e"></a>
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

<a id="86d5b12d9b06e0eb"></a>
### Description

It determines the policy to distribute client processes to NUMA nodes. This property is operated when NUMA property is set to on.

- 0: It determines the NUMA node to be connected by modularizing the session ID.
- 1: It connects to the NUMA node of which is the least connected based on the statistics information.
- 2: C/S client is determined by TCP_CLIENT_NUMA_NODE property, D/A client is determined by DA_CLIENT_ NUMA_NODE property.

<a id="e75ee432884cc776"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="2270091948caf776"></a>
### Basic Information

**Basic Information of CLOSE_PSM_CHILD_STMTS**

<a id="90839f941175a75e"></a>
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

<a id="311fa87843f1296e"></a>
### Description

It closes the child statement of PSM at the end of each execution.

<a id="08eb93c983f66f11"></a>
## CLUSTER_ASYNC_COMMIT

<a id="d2979c9bab85729d"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="4f62b6e2462aa872"></a>
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

<a id="5dbc125d0f1c71c0"></a>
### Description

It determines whether to internally process the commit protocol on an async mode in cluster system.

> If this property is set to on, it asynchronously commits each node, so the temporary inconsistency among nodes may occur. On the other hand, if it is set to off, it synchronizes everytime it commits, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="7a312d4d9c3607e3"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="152d8c2b8447ecd7"></a>
### Basic Information

**Basic Information of CLUSTER_ASYNC_COMMIT**

<a id="7181873184da1199"></a>
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

<a id="0a60a4f3cde4abd4"></a>
### Description

It determines whether to internally process the replication on an async mode in cluster system.

> If this property is set to on, it asynchronously reflects the data on each node, so the response time varies upon on which node is connected furing the operation. On the other hand, if it is set to off, it synchronizes everytime the data is updated, so it may reduce the performance. Therefore, it is required to determine the appropriate property depending on the purpose.

<a id="d75ae2b8126d4aba"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="03f16fa655287168"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_COUNT**

<a id="e80fbecb7dfb5592"></a>
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

<a id="5594c5e8986fdac6"></a>
### Description

It is the communication buffer count for cluster.

<a id="fed0b9597a09e502"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="53629beb459fa353"></a>
### Basic Information

**Basic Information of CLUSTER_CM_BUFFER_SIZE**

<a id="106644e30c629c33"></a>
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

<a id="2d6d5d0cfbc8bb37"></a>
### Description

It is the communication buffer size for cluster.

<a id="9225f2c4f397ede2"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="0f5a882292c7415c"></a>
### Basic Information

**Basic Information of CLUSTER_CM_READ_BUFFER_SIZE**

<a id="7b3a23a54cf60233"></a>
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

<a id="2ec15676687c68db"></a>
### Description

It is the communication read block size.

<a id="c6c8c9370bf66f02"></a>
## CLUSTER_COMMIT_SLAVES

<a id="7ee902d7658bd964"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_SLAVES**

<a id="67ff947349d08560"></a>
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

<a id="ba5de813582f0f9d"></a>
### Description

It is the number of commit slaves.

<a id="ed8854c1d97362cb"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="171a7e976eaacc0d"></a>
### Basic Information

**Basic Information of CLUSTER_COMMIT_STREAM_ISOLATION**

<a id="db6d35b80b022d99"></a>
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

<a id="5b436bbc35a3e263"></a>
### Description

It determines whether to internally perform the commit process flow in the cluster system separately from other protocol process. The performance may be improved when seperating the commit process according to the system environment.

<a id="e4752b2b41fbaa17"></a>
## CLUSTER_CONNECTION

<a id="6d007f3f6469239c"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION**

<a id="e7a17061e99cbf05"></a>
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

<a id="224367cac3210562"></a>
### Description

It is the connection mode for cluster. ( socket:0, rdma:1 )

<a id="2814eade1e6b35a3"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="d7ae7c4c0fbe6346"></a>
### Basic Information

**Basic Information of CLUSTER_CONNECTION_TIMEOUT_SEC**

<a id="52fbabbc0a335ad6"></a>
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

<a id="99492e8ab211b7bb"></a>
### Description

It is the connection timeout for cluster.

<a id="63974675dda9401c"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="0111e956aebebffa"></a>
### Basic Information

**Basic Information of CLUSTER_DATA_SYNC_SERVERS**

<a id="b7bd3f6066015dbf"></a>
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

<a id="70e204c2fa7829c9"></a>
### Description

It is the count of data synchronization server.

<a id="99b0b6568e8b4fab"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="3672b7cd58b62cb7"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_IN_QUEUE_SIZE**

<a id="303858ce997c659b"></a>
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

<a id="8859295295176aec"></a>
### Description

It is the in-queue size for cluster dispatcher.

<a id="d69ae134e355a9f6"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="c377c1070658b3c5"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_NUMA_STREAM_MAP**

<a id="34130a6461c5a01c"></a>
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

<a id="38696b2dd599e086"></a>
### Description

It determines a NUMA node to which the cluster dispatcher is to be connected. This property is operated when NUMA property is set to on.

> If CLUSTER_COMMIT_STREAM_ISOLATION property is set to on, then the 0 stream is set to NUMA node of a commit stream.

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="6395b56cd0a6b542"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="198989e69418e086"></a>
### Basic Information

**Basic Information of CLUSTER_DISPATCHER_OUT_QUEUE_SIZE**

<a id="38dcac72d2e2a2ef"></a>
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

<a id="8ca21c87bbaa0341"></a>
### Description

It is the out-queue size for cluster dispatcher.

<a id="0490587ecbbb652b"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="fa0868e5709d73dc"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_INTERVAL**

<a id="984a17cc7c3767c0"></a>
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

<a id="68edf86e2d49c214"></a>
### Description

It is the interval seconds for health checking of cluster. 0 means that it is disabled.

<a id="4d795ecd5148985c"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="e91feea6047b35cd"></a>
### Basic Information

**Basic Information of CLUSTER_HEARTBEAT_RETRY_COUNT**

<a id="053ff96d0336e177"></a>
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

<a id="80fcbe6f30588148"></a>
### Description

It is the retry count for health checking of cluster.

<a id="daeff2402c963ef7"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="14ed82cc2c652b40"></a>
### Basic Information

**Basic Information of CLUSTER_IGNORE_INACTIVE_MEMBER**

<a id="dac7c09181116589"></a>
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

<a id="abbf981660a40183"></a>
### Description

It ignores in-active member for cluster.

<a id="4c155ef54a54fa75"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="71dfe4f6ff51c33a"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PACKET_SIZE**

<a id="ba7e3d03c6ed427f"></a>
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

<a id="e5150ffeb481f4d4"></a>
### Description

It sets the maximum packet size of which the remote protocol can transfer at a time. If the column size to be remotely transferred exceeds the property size, then the property size should be set bigger than the column size.

<a id="117cfc4bc45adb12"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="931b0831eec7910b"></a>
### Basic Information

**Basic Information of CLUSTER_MAX_PAYLOAD_SIZE**

<a id="529b6b3ab73811aa"></a>
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

<a id="d51b6ada0a8367e9"></a>
### Description

The cluster packet which is remotely transferred may be delivered in pieces, and this property sets the maximum size of data to be stored in a piece.

<a id="fd1950e6d1224a44"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="d792ef4f5f24f033"></a>
### Basic Information

**Basic Information of CLUSTER_PACKET_ALLOCATION_TIMEOUT**

<a id="435e281e4b0ee475"></a>
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

<a id="c15f3ad4859303b7"></a>
### Description

It sets the maximum time (second) of waiting when allocating memory required for cluster packet configuration.

<a id="30569b05453f1dcd"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="e640d58211b435cf"></a>
### Basic Information

<a id="f83e74a35e182364"></a>
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

<a id="322c2321c8bfdaba"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property to use the policy terminating the session. However, specify the time limit by using [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#bc867ec7116a99bb) property to use the failover policy.

<a id="bc867ec7116a99bb"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="a28dfa87d4f59cd3"></a>
### Basic Information

<a id="5383dc39d981ccb9"></a>
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

<a id="8564d96af92bf65f"></a>
### Description

It is the maximum time of when waiting for the response after transferring the protocol in cluster. If it does not responds within the specified time, then GOLDILOCKS, depending on the protocol, may terminate the protocol or make the remote cluster member which does not responds to be failover. Specify the time limit by using *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property to use the failover policy. However, specify the time limit by using [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#30569b05453f1dcd) property to use the policy terminating the session.

<a id="7e479fa7b15c67b6"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="b33d4f0ff11dd0af"></a>
### Basic Information

**Basic Information of CLUSTER_SERVER_RESPONSE_QUEUE_SIZE**

<a id="80b98b39c0b218b5"></a>
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

<a id="b53ffc1352740fba"></a>
### Description

It sets the maximum queue size to get response from the remote server.

<a id="b8d613aa2234587a"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="73d579aaae3a86e0"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY**

<a id="d3b7d91d2b7cf0f7"></a>
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

<a id="944b181d0f44bc93"></a>
### Description

It sets the policy to resolve split-brain situation in the cluster system. If the value is set to 1 or over, it enquires the solution of a locator.

> If the query for a locator is timed out, it tries to enquire as many times as CLUSTER_SPLIT_BRAIN_RETRY_COUNT. If the property value after the retry failure is 1, then it forcibly proceeds the failover. If it is 2, then it terminates the fatal.

<a id="1e5e129c4789c487"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="1545d0cf99c23979"></a>
### Basic Information

**Basic Information of CLUSTER_SPLIT_BRAIN_RETRY_COUNT**

<a id="3d48996a07777019"></a>
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

<a id="4bcdadf7f5c377a9"></a>
### Description

It is used when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or over in cluster system. It sets the times of retrying to enquire when the query to a locator does not respond.

<a id="ac3e36b81d8a3de7"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="cfa0110fa01baa9a"></a>
### Basic Information

**Basic Information of COMMITTER_HOT_POLICY_INTERVAL**

<a id="e08795742e1d113e"></a>
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

<a id="6a90a6446e4df6a4"></a>
### Description

It sets the timezone interval of busy waiting when the commit cserver is dequeing to read the commit protocol message. If it is set to 1,000,000 (1 second), and the time is not passed over 1 second from the last deque success to another deque retry, then it sets the timeout in deque to 0 and performs the busy waiting.

<a id="182868278c1a2a45"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="64feb684402a1a86"></a>
### Basic Information

**Basic Information of CONTROL_FILE_0 ~ CONTROL_FILE_7**

<a id="082a1668d64c10d9"></a>
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

<a id="0e6c850e16cecb49"></a>
### Description

If a control file is corrupted, database can not be used. Therefore, the control file is multiplexed for stability of database. It specifies the directory and file name of which stores each control file.

<a id="5e236d92b9369caf"></a>
## CONTROL_FILE_COUNT

<a id="8dc48cf5c4563dc8"></a>
### Basic Information

**Basic informatin of CONTROL_FILE_COUNT**

<a id="8176499df00c96c2"></a>
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

<a id="53d055ea776078a7"></a>
### Description

If a control file is corruped, database can not be used. The control file is multiplexed for stability of database. CONTROL_FILE_COUNT specifies the multiplexing number of control files. A control file is multiplexed at least 2 up to 8.

<a id="283c1a7102609421"></a>
## CONTROL_FILE_TEMP_NAME

<a id="8e648e174bb8af21"></a>
### Basic Information

**Basic Information of CONTROL_FILE_TEMP_NAME**

<a id="017864ac48d38158"></a>
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

<a id="a194e40a6b0ddf02"></a>
### Description

During database operation, a control file is frequently changed, and its temporary copy can be made if necessary. CONTROL_FILE_TEMP_NAME specifies the directory and its file name to temporarily store the control file.

<a id="74b0f40db7604972"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="1478698afde846f0"></a>
### Basic Information

**Basic Information of COORDINATOR_COMMIT_WRITE_MODE**

<a id="776d5ddbe52d715d"></a>
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

<a id="00285a44bbb19b44"></a>
### Description

It is a commit write mode applied to a coordinator. If TRANSACTION_COMMIT_WRITE_MODE is *no wait*, and its property is *wait*, then the coordinator node is operated as *wait*, and other nodes are operated as *no wait*.

<a id="85d0e9ba6d447c3e"></a>
## CSERVERS

<a id="428cf091739a006e"></a>
### Basic Information

**Basic Information of CSERVERS**

<a id="2bf358bf9bc198b3"></a>
| Item | Description |
| --- | --- |
| Name | CSERVERS |
| Summary | number of cserver processes |
| Data type | BIGINT |
| Applicable phase | MOUNT or below |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMMEDIATE |
| MIN | 1 |
| MAX | 512 |
| Default value | 10 |

<a id="4520844f955383b5"></a>
### Description

It is a number of cserver process.

<a id="337a3309dac47621"></a>
## DATABASE_ACCESS_MODE

<a id="14dffa7de028df21"></a>
### Basic Information

**Basic Information of DATABASE_ACCESS_MODE**

<a id="02238c2478b45794"></a>
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

<a id="61851b4f3ad834e5"></a>
### Description

When database starts, it sets the access mode.

- 0: It is able to read operation, but unable to insert/ update/ delete operations on database.
- 1: It is able to read/ insert/ update/ delete operations on database.

<a id="e5c9bf48221d1162"></a>
## DATABASE_INSTANCE_NAME

<a id="9ad08028df0c80fa"></a>
### Basic Information

**Basic Information of DATABASE_INSTANCE_NAME**

<a id="68f0d4ca49884ef6"></a>
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

<a id="86303dbf5151d61e"></a>
### Description

It is the database instance name.

<a id="49a54c9e9b052a35"></a>
## DATA_STORE_MODE

<a id="6b9b305574c7f5eb"></a>
### Basic Information

**Basic Information of DATA_STORE_MODE**

<a id="899e481bd0be84e1"></a>
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

<a id="21e6cbccd87ba31f"></a>
### Description

It sets the storing method of database.

- 1: CDS mode supports the concurrency for multiple users but it does not guarantee the durability. It does not record logs for all update operations such as insert/ delete/ update data, consequentially a failure can not be recovered.
- 2: TDS mode guarantees the concurrency for multiple users and the durability using logs.

<a id="5f2f27b454102397"></a>
## DA_CLIENT_NUMA_NODE

<a id="3c74b76117fbf9b6"></a>
### Basic Information

**Basic Information of DA_CLIENT_NUMA_NODE**

<a id="4bf363ce18f66ede"></a>
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

<a id="ff097d72cd07e8fc"></a>
### Description

It sets the NUMA node ID to which the direct access (D/A) session is to be bound. This property is operated when NUMA property is set to ON.

<a id="9fa3b9a18490837b"></a>
## DDL_AUTOCOMMIT

<a id="496b7b49aeabc101"></a>
### Basic Information

**Basic Information of DDL_AUTOCOMMIT**

<a id="de72489bad06c2f1"></a>
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

<a id="c5d85b4f27c72436"></a>
### Description

It sets whether to autocommit DDL operations which is not autocommitted yet. For example, autocommit is not applied to the operations such as creating/altering a table, so if DDL_AUTOCOMMIT is 0, a table creation and alteration can be undone by the rollback. On the other hand, if DDL_AUTOCOMMIT is 1, DDL to which autocommit is not applied is committed immediately.

<a id="0a58634ab8c6ecd8"></a>
## DDL_LOCK_TIMEOUT

<a id="1778254a9aedebdb"></a>
### Basic Information

**Basic Information of DDL_LOCK_TIMEOUT**

<a id="fcb4987d649b6b54"></a>
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

<a id="fb10270dd40ae706"></a>
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

<a id="22707b2c9580c589"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="6f25e09e4f18206f"></a>
### Basic Information

**Basic Information of DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION**

<a id="714c103a6b3db031"></a>
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

<a id="9064f27bf8e00375"></a>
### Description

It sets whether to create the global secondary index when creating a table in cluster system. A non-deterministic query for the table which did not created the global secondary index fails. The global secondary index can be separately created after creating the table when the property is set to NO.

<a id="40a3a5c73e188fea"></a>
## DEFAULT_INDEX_LOGGING

<a id="f0a9c52c07bb559a"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_LOGGING**

<a id="522cb92e4c27550c"></a>
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

<a id="83eab60987e3fdcf"></a>
### Description

If LOGGING property is not explicitly set by a user when an index is created, then it is set to DEFAULT_INDEX_LOGGING value. If an index is created in LOGGING tablespace, the LOGGING property should be set.

<a id="10598edaf38e09bb"></a>
## DEFAULT_INDEX_PCTFREE

<a id="d42a6a43610250d8"></a>
### Basic Information

**Basic Information of DEFAULT_INDEX_PCTFREE**

<a id="f5156155d6605503"></a>
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

<a id="c8467815e3b934a5"></a>
### Description

If a user does not explicitly specify PCTFREE syntax when creating an index. The PCTFREE is set to DEFAULT_INDEX_PCTFREE property value.

<a id="797ca05082a2fe17"></a>
## DEFAULT_INITRANS

<a id="1f5eebb75186ba67"></a>
### Basic Information

**Basic Information of DEFAULT_INITRANS**

<a id="76c7477032708d0a"></a>
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

<a id="77a2feca5f4994b2"></a>
### Description

If a user does not explicitly set INITRANS syntax when creating a table or an index, then it is set to DEFAULT_INITRANS property value.

<a id="3b49f5a6e1dcb213"></a>
## DEFAULT_MAXTRANS

<a id="6903610f9e79b57d"></a>
### Basic Information

**Basic Information of DEFAULT_MAXTRANS**

<a id="44132a246965a893"></a>
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

<a id="640358e9b25f6a2a"></a>
### Description

If a user does not explicitly set the MAXTRANS syntax when creating a table or an index, then it is set to DEFAULT_MAXTRANS property value.

<a id="06690e112276c4b8"></a>
## DEFAULT_PCTFREE

<a id="7d6a73cb7b8b80b0"></a>
### Basic Information

**Basic Information of DEFAULT_PCTFREE**

<a id="0f792808a29622e0"></a>
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

<a id="833289d92eb495be"></a>
### Description

If a user does not explicitly set the PCTFREE property when creating a table, it is set to DEFAULT_PCTFREE property value.

<a id="f2bc463b0390c373"></a>
## DEFAULT_PCTUSED

<a id="d24ca5db33fdeef6"></a>
### Basic Information

**Basic Information of DEFAULT_PCTUSED**

<a id="56d4f8cd3bd8db3f"></a>
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

<a id="83ce2c630d108c37"></a>
### Description

If a user does not explicitly set the PCTUSED property when creating a table, it is set to DEFAULT_PCTUSED value.

<a id="6bf677c5e996fd5a"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="d42796a64f562819"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_BACKUP_FILE**

<a id="5e5fabadd2488ad5"></a>
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

<a id="2b524c7f742b3a33"></a>
### Description

It specifies whether to delete the backup file when deleting the backup list.

<a id="b1317c550bc5a1ab"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="3ae8c8eb121a6597"></a>
### Basic Information

**Basic Information of DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST**

<a id="c1e978d921197bdb"></a>
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

<a id="34ca45122661f9c0"></a>
### Description

It specifies whether to delete the previous obsoleted backup list when executing INCREMENTAL BACKUP.

<a id="30cbcb4f35b1117e"></a>
## DEFAULT_SHARDING

<a id="ce880f56a5dcd0a9"></a>
### Basic Information

**Basic Information of DEFAULT_SHARDING**

<a id="4a6b86aa011f9e7b"></a>
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

<a id="add9732d8adeb5da"></a>
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

<a id="ee662f3673d3922e"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="6306627a39cc1d3d"></a>
### Basic Information

**Basic Information of DISABLE_DDL_CDC_GIVEUP**

<a id="5b26a4c0562e7d62"></a>
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

<a id="0cbdca003a712f16"></a>
### Description

It prohibits DDL operation on the table of supplemental log, because it affects CDC's give up.  
For more information, refer to [The table-related DDL causing Replication Give-up](../part-07-replication/44-cyclone.md#0304d5f6f35e4530).

<a id="feaf9cd4448e4c40"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="763955edda4ed8ad"></a>
### Basic Information

**Basic Information of DISABLE_UPDATE_PK_CDC_GIVEUP**

<a id="91f045d58f21f4df"></a>
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

<a id="b841baf9ce097abe"></a>
### Description

It disables UPDATE primary key which caused CDC give up.

<a id="3c12aee84f464507"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="80663fa728351020"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE**

<a id="2a1fdff116342112"></a>
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

<a id="d0cb1d6517ecaca0"></a>
### Description

It disallows TARGETTYPE protocol.

<a id="244c4b63005edb01"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="17f6602db7ca68e5"></a>
### Basic Information

<a id="e2658e5e8ad434f3"></a>
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

<a id="c91cfa47f038fc1b"></a>
### Description

It disallows TARGETTYPE_WITH_ALL protocol.

<a id="eb4cd55b5e382c31"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="baf535112f2bc08b"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="858e423c3841fb8e"></a>
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

<a id="d8509c59a4116cca"></a>
### Description

It disallows TARGETTYPE_WITH_NAME protocol.

<a id="8679ba3a14fae8dd"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="fdde2bf0715221f9"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_BUFFER_SIZE**

<a id="b69fc1b81fde7f59"></a>
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

<a id="484ccdcb7fd27a44"></a>
### Description

It is the size of entire communication buffer used in shared mode. It is allocated to and used in Shared Static Area (SSA).

<a id="f1c20f52c4e0a5b5"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="58f23da48a03a2a3"></a>
### Basic Information

**Basic Information of DISPATCHER_CM_UNIT_SIZE**

<a id="7ab3046dfefd57ea"></a>
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

<a id="8e6d62edd63d2d2e"></a>
### Description

It is the unit size managed by dispatcher in shared mode. If the size is large, the memory is wasted. If it is small, the performance is degraded. It is set to the maximum communication packet size in the shared mode.

<a id="8f8b7521164fbe65"></a>
## DISPATCHER_CONNECTIONS

<a id="a068025539a2bb1f"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="3e9ccc09bf718ca3"></a>
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

<a id="6dd70f9308ea909e"></a>
### Description

It is the maximum number of connection (client) which a dispatcher can manage in shared mode.  
If the system- supported maximum value is smaller than the set value, it is internally set to the system maximum.

<a id="0a9cadf222f689c7"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="8253da1366be20b8"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="5cba5dbfec7f8125"></a>
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

<a id="329bd0c818f09275"></a>
### Description

It is the dispatcher dequeue interval for busy waiting. (micro second)

<a id="e36484de11d60606"></a>
## DISPATCHER_LOAD_BALANCING

<a id="aec830b54411792a"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="7df96d7d5bea65d5"></a>
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

<a id="dd67ad3af4386196"></a>
### Description

It is an algorithm allocating a dispatcher when connecting to a client in the shared mode.

- 0: It is allocated to a dispatcher of which the number of currently attached clients are small.
- 1: It is sequentially allocated to a dispatcher.

<a id="0c6c5b9f64886421"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="4e155763449b83b6"></a>
### Basic Information

**Basic Information of DISPATCHER_CONNECTIONS**

<a id="6bf4d643973ebf30"></a>
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

<a id="1d7d5ee83bc7fdbf"></a>
### Description

It determines NUMA node to which dispatchers are to be connected. This property is operated when NUMA property is set to on.  

The following is an example of three dispatchers. It connects number 0 stream to number 0 NUMA node, connects number 1 stream to number 1 NUMA node, and number 2 stream to number 2 NUMA node.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="c70544e36e2c0d1b"></a>
## DISPATCHER_QUEUE_SIZE

<a id="1cc082280d338a25"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="1265b864f27e5978"></a>
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

<a id="6e12666fb497d6f8"></a>
### Description

In shared mode, it sets the queue size for the communication between the dispatcher and the shared-server.

<a id="c47c92da1a129ac9"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="116ee34e7738b1b7"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="c2928a988fcaaccc"></a>
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

<a id="d50599452bff4f87"></a>
### Description

It is the count of mini queue per request queue.

<a id="5475e188f40a72e0"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="105025495d0c26a1"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="0cd3022ba4ceb105"></a>
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

<a id="56410020768b3619"></a>
### Description

It is the count of mini queue per response queue.

<a id="e77cc5bed51007b1"></a>
## DISPATCHERS

<a id="09286b9b8780a627"></a>
### Basic Information

**Basic Information of DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME**

<a id="b481f968e19fd285"></a>
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

<a id="f5d7a90a3278837b"></a>
### Description

It sets the number of dispatcher processes when using the shared mode.  
It can not reduce the value by using alter system on open phase.

<a id="7e77fea2fc5808ef"></a>
## FETCH_FAILOVER

<a id="29c35227f3a90ff2"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="7dddac4ae9fd9135"></a>
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

<a id="5e6e575d9c8a6301"></a>
### Description

It enables the fetch failover.

<a id="9f3b773f0fb6eaac"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="f5f786a9410a8128"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="8583d7690b592570"></a>
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

<a id="d3cf3bd4f8535400"></a>
### Description

It sets whether to support the query execution including the session dependent information in the global connection.

<a id="098ea3790b064b8c"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="d558e866828f2da8"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="434261a3587a3846"></a>
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

<a id="207506b7415e55e6"></a>
### Description

It is the size of global journal buffer.

<a id="f6195283f349ab2e"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="5a14a2b83f811a57"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="a400c49330693625"></a>
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

<a id="054a24dadfea827e"></a>
### Description

It is the total max size of global journal buffer.

<a id="825d985495dbd559"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="ca9221494c0d3c7e"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="60d3911ad59db702"></a>
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

<a id="cdbe8316ef450a1c"></a>
### Description

When changing the global property, it performs the lock to control the concurrency. In this case, the waiting time to perform the lock is set.

<a id="96649c51aa7a2be8"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="8d8e8354799d2bd1"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="f1762ca6bda51e72"></a>
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

<a id="31c331d5d20da95f"></a>
### Description

It is a property to change the commit write mode of the global transaction. TRANSACTION_COMMIT_WRITE_MODE property is applied to all transactions, but GLOBAL_TRANSACTION_COMMIT_WRITE_MODE property is applied only to a global transaction. If the property is set to 2, then it follows the TRANSACTION_COMMIT_WRITE_MODE.

- 0: It does not wait.
- 1: It waits.
- 2: It follows the value of TRANSACTION_COMMIT_WRITE_MODE.

<a id="057817709668221e"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="c3f5ecfcb56198fe"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="3c9462ff7d956e2c"></a>
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

<a id="44c1133e279f1900"></a>
### Description

It determines whether to process the data with a global transaction or with multiple domain transactions when the transaction changed the data through two cluster groups.

- 0: It processes with a global transaction.
- 1: It processes with multiple domain transactions.

> If this property is set to 1, it commits each cluster group with a separate transaction, so it does not guarantees the transaction atomicity.

<a id="922f5ed0f2f89eb6"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="0d5a77529dc8c7c1"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="b9227179d6e3bcd4"></a>
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

<a id="5c0dcd9fb01ddbc9"></a>
### Description

It is the default directory of global transaction log.

<a id="ce8daa3432035719"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="653b179147126bc6"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="031d4ed2c4b1b863"></a>
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

<a id="0a5513c841e37ecd"></a>
### Description

It is the file size of global transaction log.

<a id="9659bed29360455c"></a>
## GMASTER_NUMA_NODE

<a id="7a92e70e41dfc042"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="96be6c00727ba16f"></a>
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

<a id="a28be5ffc1f431d9"></a>
### Description

It sets the ID of NUMA node to be used by gmaster daemon. This property is operated when NUMA property is set to on.

<a id="3a629083fb79fde0"></a>
## GMON_AUTOSTART

<a id="7071c455dea16112"></a>
### Basic Information

**Basic Information of DISPATCHER_QUEUE_SIZE**

<a id="3173c34de3461936"></a>
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

<a id="16e5f67691efcce6"></a>
### Description

It sets whether to start gmon process automatically.

<a id="71df2c06fa9b9f24"></a>
## HINT_ERROR

<a id="4e0a6ce55a68f3fb"></a>
### Basic Information

**Basic Information of HINT_ERROR**

<a id="6fe41dc13b1f8cba"></a>
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

<a id="b2fafdd5ff0bec2d"></a>
### Description

It sets whether to check syntax error and validation error for hint syntax.

<a id="ebef4c4cbdb76cf1"></a>
## IDLE_TIMEOUT

<a id="8c5280738359a0e1"></a>
### Basic Information

**Basic Information of IDLE_TIMEOUT**

<a id="d924762950639a42"></a>
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

<a id="b82cb069412c2e11"></a>
### Description

It sets the maximum IDLE time possible to  wait in C/S session. If it exceeds the specified idle time, TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="d79abda3bf210d81"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="3b941138259dbee5"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="157ccf06fd85e33c"></a>
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

<a id="5103d3ee67e15dd7"></a>
### Description

When creating an index, it specifies the number of parallel factor.

- 0: It is specified as the number of the core factor in the system.

<a id="df71fd613e3de179"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="81de23183001d9b4"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="60af5e439ee31cbe"></a>
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

<a id="79402d4c1e2b986b"></a>
### Description

When creating an index, it specifies the number of parallel factor to merge the sub-tree.   
If that value is bigger than INDEX_BUILD_PARALLEL_FACTOR, then INDEX_BUILD_PARALLEL_FACTOR is used.

- 0: It follows INDEX_BUILD_PARALLEL_FACTOR.

<a id="7b245b773245b046"></a>
## INST_ALLOCATOR_COUNT

<a id="a694d9eaa1899e7a"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="319b1ce5219c8339"></a>
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

<a id="6bef4a06ce4c3b4b"></a>
### Description

This property increases the parallel property of operation allocating or deleting an instant block.

<a id="ddc62d33552ade28"></a>
## INST_TABLE_BLOCK_SIZE

<a id="72bb1e65f5612d59"></a>
### Basic Information

**Basic Information of INDEX_BUILD_PARALLEL_FACTOR**

<a id="36b6a1d600596572"></a>
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

<a id="fc0e4075f8964508"></a>
### Description

It determines the size of an instant block. If the anchor area of an instant record is bigger than an instant block, then the following error occurs.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="c7f3327bf555b5d9"></a>
## IN_DOUBT_DECISION

<a id="545b22e227c05eac"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="5fe2b13a4892c449"></a>
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

<a id="cee71f4154745ce6"></a>
### Description

It determines whether to commit or to rollback the in-doubt transaction of distributed transactions.

- 1: Commit
- 2: Rollback

<a id="94169732706b85f4"></a>
## JOURNAL_TEMP_DIR

<a id="e0ee3e2258dbdabf"></a>
### Basic Information

**Basic Information of IN_DOUBT_DECISION**

<a id="792318667453634f"></a>
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

<a id="143bd753d173bc62"></a>
### Description

It is the temporary directory of journaling.

<a id="f3dbc853119465a6"></a>
## KEEPALIVE_IDLE_TIME

<a id="a5474759d097c705"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="84e67d42238e27e8"></a>
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

<a id="faa84572e726280e"></a>
### Description

It means the idle duration between the server and client without tcp packet exchange before sending keep alive packet. If there is not tcp packet exchange for seconds (KEEPALIVE_IDLE_TIME), keep alive mechanism starts execution to detect the dead connection on the server side.

<a id="e714f13bad7da40d"></a>
## LOCAL_CLUSTER_MEMBER

<a id="e213ef890b191356"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="bc710d8b1e52bd23"></a>
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

<a id="3f093ed0264f48ce"></a>
### Description

It is the local cluster member name.

<a id="e7dc505606e6ecb1"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="d54ed6e1eb3545d0"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="a4d46265bcc3ca85"></a>
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

<a id="7e408dc98a7e2d28"></a>
### Description

It is host name of local cluster member.

<a id="15aa99489918a150"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="6bb99ae2b46e0192"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="cb14d01228afcb01"></a>
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

<a id="1d0413ab12f0cdea"></a>
### Description

It is listen port of local cluster member.

<a id="0adc1a722fd6eaa5"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="5c3b50fe9d3e5bfc"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="e6f4fe029db448fc"></a>
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

<a id="0ea4ac9ffcd062a9"></a>
### Description

It is the local journal buffer size.

<a id="ddc9f54027699d3a"></a>
## LOCATION_FILE

<a id="bfc6bd8d019b35c8"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="33b1684855ea6e95"></a>
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

<a id="84d61f2b50296178"></a>
### Description

It is the location file name.

<a id="340931bd657d1e3a"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="cc94bdff80eb5ce9"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="57441e0a75a61833"></a>
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

<a id="6417a615127d62c1"></a>
### Description

It sets the time (second) waiting for the response after the cluster system enquires of a locator about the solution of split-brain situation. This property is used only when CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or more.

<a id="bfec5e85d069c775"></a>
## LOCK_HASH_TABLE_SIZE

<a id="a7facb7a40e6113b"></a>
### Basic Information

**Basic Information of KEEPALIVE_IDLE_TIME**

<a id="f8c427e53a0de837"></a>
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

<a id="bed0a932303c4ee2"></a>
### Description

It specifies the maximum hash table size managed by a lock manager.

<a id="22997f304de18145"></a>
## LOG_BLOCK_SIZE

<a id="1bce1d31f6d276b6"></a>
### Basic Information

**Basic Information of LOG_BLOCK_SIZE**

<a id="20d774063ec00e63"></a>
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

<a id="03db6b430d1db396"></a>
### Description

It means the minimum size of what log buffer is flushed to the log file of the disk. Its value should be set to one of 512, 1024, 2048, 4096.

<a id="e55476cecef7dbfc"></a>
## LOG_BUFFER_SIZE

<a id="1ed53e0267e35fd3"></a>
### Basic Information

**Basic Information of LOG_BUFFER_SIZE**

<a id="13d9c62f0386a17e"></a>
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

<a id="0ce9d89b905e298f"></a>
### Description

A log buffer is the shared memory space in which the redo logs generated in database by the DML/DDL operations are stored. LOG_BUFFER_SIZE is referenced to set the memory size for the log buffer.

<a id="df65d36985bdd29b"></a>
## LOG_DIR

<a id="6f01fc11670ca16d"></a>
### Basic Information

**Basic Information of LOG_DIR**

<a id="2b9700bffd5582d1"></a>
| Item | Description |
| --- | --- |
| Name | LOG_DIR |
| Summary | default log directory |
| Data type | VARCHAR |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| Default value | &lt;GOLDILOCKS_DATA&gt;/wal |

<a id="ceb2ae6004aea8cf"></a>
### Description

The log recorded in the log buffer is flushed to the logfile which exists in a non-volatile storage device to ensure the database durability. LOG_DIR sets the path to the log file.

<a id="2b0d38376270722c"></a>
## LOG_FILE_SIZE

<a id="ac3e63680bd94c1a"></a>
### Basic Information

**Basic Information of LOG_FILE_SIZE**

<a id="f3355d8a21d5b13d"></a>
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
| MAX | 60 Gbytes |
| Default value | 100 Mbytes |

<a id="e8c63cf3c4c053fe"></a>
### Description

It sets the size of the logfile used in database. It is referenced only when creating the database, then log file size can not be updated after then.

<a id="86a51905608cc5fa"></a>
## LOG_GROUP_COUNT

<a id="c3ea5e75cd2931af"></a>
### Basic Information

**Basic Information of LOG_GROUP_COUNT**

<a id="00bb05a86369787b"></a>
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

<a id="a237c827b098a9c9"></a>
### Description

It sets the number of log group used in database. It is referenced only when creating the database, but after that, it does not affect any operations. After creating database, the operation to add or remove a log group is supported by a separate syntax.

<a id="4cbe173baed7b850"></a>
## LOG_MIRROR_MODE

<a id="d341b1a8fcbb3ec7"></a>
### Basic Information

**Basic Information of LOG_MIRROR_MODE**

<a id="e8b979636a0ea6a1"></a>
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

<a id="83be13dd9121039a"></a>
### Description

It is the property to configure the required shared memory when operating LogMirror, the redo log replication tool, at database startup.  
It should be enabled to execute the LogMirror.  
The size of the shared Memory can be changed using LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE.

<a id="3cce9e2b265c22a5"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="0dd3bee35174336b"></a>
### Basic Information

**Basic Information of LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE**

<a id="07c8f146ffa9be00"></a>
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

<a id="27920e4386de9431"></a>
### Description

It sets the size of the shared memory used in LogMirror, the redo-log replication tool.   
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="5b4eb361f737fbb6"></a>
## LOG_MIRROR_TIMEOUT

<a id="4ca91593d500390c"></a>
### Basic Information

**Basic Information of LOG_MIRROR_TIMEOUT**

<a id="d70d078e267969b7"></a>
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

<a id="294763238644d470"></a>
### Description

It is the response waiting time of the LogMirror.   
If its value is 0, it waits indefinitely. Otherwise, it waits as long as the value set, then TIMEOUT occurs, and it stops LogMirror service. Later, the server is operated normally.  
It is applied in the state which LOG_MIRROR_MODE is enabled.

<a id="a200517e3a35c460"></a>
## LOG_SYNC_INTERVAL

<a id="a6ca92f7e472bf30"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="aab8a78e3b26455a"></a>
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

<a id="bf23f078c882bc52"></a>
### Description

Log flusher of GOLDILOCKS is a system thread which flushes the log buffer contents to disk logfile. When log flusher wakes up in the idle phase, it checks if log to flush exists. Then it flushes the log if any.  
If the log flusher did not flush within the time set in LOG_SYNC_INTERVAL, it synchronizes the log buffer and the log file by performing a flush until the last block of the current log buffer.

<a id="f12463c8001e4168"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="909489579beb162b"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="4cdc4da825938e17"></a>
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

<a id="f80ce20adef36684"></a>
### Description

It is the millisecond interval for synchronize log.

<a id="6c528d3ea6113b2b"></a>
## MAX_GROUP_COUNT

<a id="cf6a69c2684a3eb2"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="19f0257d2645bb62"></a>
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

<a id="1c34b9573b27bc41"></a>
### Description

It is the maximum group count.

<a id="538af4a7f8a614ab"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="567ed2e5496a4c5a"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="8b1d02d7495188af"></a>
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

<a id="a82bd238e132daa8"></a>
### Description

It sets the maximum size (quota) of the global journaling file which internally stores journaling data when a journaling occurs in cluster system.

<a id="ea24b7286f89a784"></a>
## MAX_NODE_COUNT

<a id="cee267a9cefca975"></a>
### Basic Information

**Basic Information of LOG_SYNC_INTERVAL**

<a id="c41bd261024e4aca"></a>
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

<a id="1ff8fefc946d1d1e"></a>
### Description

It is the maximum node count.

<a id="cd0d8555e41a42c6"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="8875d1c13b6d3bfb"></a>
### Basic Information

**Basic Information of MAXIMUM_CONCURRENT_ACTIVITIES**

<a id="cbc277c71a0a5bbd"></a>
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

<a id="c21aa8d13f141e9a"></a>
### Description

It sets the number of statements which can be executed simultaneously.

<a id="56da1e8ca4ed0c44"></a>
## MAXIMUM_FLANGE_COUNT

<a id="7748f2f611d920d0"></a>
### Basic Information

**Basic Information of MAXIMUM_FLANGE_COUNT**

<a id="b0bb6f9b1aece76c"></a>
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

<a id="8db8f53c1bc54e3c"></a>
### Description

It is the maximum number of flanges which can be expanded in plan clock.

<a id="3340b96f73909992"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="694dce1e14ac58e3"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_LOG_BLOCK_COUNT**

<a id="9482fcecd03f260b"></a>
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

<a id="76782efa55a0bde8"></a>
### Description

When flushing the contents of the log buffer to disk log file, it sets the maximum number of log blocks to be flushed with a single writing operation.

<a id="874873dc2e1c6c04"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="36468cfbfa83156d"></a>
### Basic Information

**Basic Information of MAXIMUM_FLUSH_PAGE_COUNT**

<a id="cc455cc8496f4ab9"></a>
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

<a id="8ef8ca56591191d7"></a>
### Description

GOLDILOCKS datafiles are flushed to the disk by the checkpoint and certain DDL statements. For flushing datafiles, it sets the maximum number of data pages to be flushed with a single writing operation.

<a id="75e3127df3e47bdb"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="9508c8c6bda7409a"></a>
### Basic Information

<a id="6530085b0d5d40de"></a>
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

<a id="6ce655b6768edf38"></a>
### Description

The table rebalancing online can be performed together with dml in the cluster environment, and dml records the updates on the journal log at that moment. The table rebalancing initially applies the journal logs which occurred during synchronizing tables, then applies journal logs which were accumulated while applying the journal logs. This property sets how may times the journal logs are applied in this way.

<a id="73119ff8c8a4c76c"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="b873080c7b0a17d3"></a>
### Basic Information

**Basic Information of MAXIMUM_NAMED_CURSOR_COUNT**

<a id="3173aa786f72528c"></a>
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

<a id="7912e451cbe8f232"></a>
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

<a id="9ada4bacee7459fc"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="978c01d1bda7f6e6"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="4ac040399e741a02"></a>
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

<a id="f4f84036896495ed"></a>
### Description

It sets the maximum buffer size available in a single session which is connected to shared mode.  
For more information, refer to [DISPATCHER_CM_BUFFER_SIZE](#8679ba3a14fae8dd).

<a id="b2c8f6be9da1ddc8"></a>
## MEASURE_CLUSTER_LATENCY

<a id="3f303e13ad681247"></a>
### Basic Information

**Basic Information of MAXIMUM_SESSION_CM_BUFFER_SIZE**

<a id="eb47f93a425f15b2"></a>
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

<a id="9ac24573df89670c"></a>
### Description

It is the measure cluster latency.

<a id="3b410382bd344153"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="8cfe2b590817c2a4"></a>
### Basic Information

**Basic Information of MEMORY_MERGE_RUN_COUNT**

<a id="e0835bc0dc9c8340"></a>
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

<a id="7e835f7dc6dec5b3"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in certain block size (MEMORY_SORT_RUN_SIZE) units, merging the sorted blocks, and generating the internal node. MEMORY_MERGE_RUN_COUNT sets the number of the sorted blocks to be merged at a time.

<a id="e254f2766b2c0489"></a>
## MEMORY_SORT_RUN_SIZE

<a id="00e477e6d8da8832"></a>
### Basic Information

**Basic Information of MEMORY_SORT_RUN_SIZE**

<a id="2b72d96a45df74e6"></a>
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

<a id="a7d93111e316c501"></a>
### Description

Memory B-tree index of bottom-up approach is created by extracting all keys from a table, sorting them in a certain block size (MEMORY_SORT_RUN_SIZE) unit, merging the sorted blocks, and generating the internal node. MEMORY_SORT_RUN_SIZE sets the size of a single block to be sorted.

<a id="ecc88490711f30cf"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="58282506fc671de9"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="0953049363693b15"></a>
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

<a id="697828413c806496"></a>
### Description

DML uses the undo page to store the previous image. Undo page is consumed by using a single undo segment per DML. If all allocated pages of undo segments are consumed, the page of another undo segment can be used. MINIMUM UNDO PAGE_COUNT is the minimum number of undo page to specify the undo segment to import page when undo pages are insufficient. If the undo pages are insufficient, the pages can be imported only from the undo segment having more pages than MINIMUM UNDO PAGE_COUNT.

<a id="43c982a68399a772"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="0d5f20b01ea3bb75"></a>
### Basic Information

**Basic Information of MINIMUM_UNDO_PAGE_COUNT**

<a id="3a70f5079b78538a"></a>
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

<a id="5c10242884041545"></a>
### Description

It is the minimum number of sampling rows when executing [ANALYZE TABLE](../part-03-sql-manual/16-sql-references.md#7a194a6cfef8c726) by using the sampling.

<a id="4716fa2373473e7b"></a>
## NET_BUFFER_SIZE

<a id="beaa7ce8e9994432"></a>
### Basic Information

**Basic Information of NET_BUFFER_SIZE**

<a id="ce8ab9ea04a24237"></a>
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

<a id="8eadc07d666b63dd"></a>
### Description

It sets the TCP communications buffer size.   
In the dedicated mode, it is set to the maximum communication packet size.  
In the shared mode, it is set to [DISPATCHER_CM_UNIT_SIZE](#f1c20f52c4e0a5b5).

<a id="6c5301741d86446c"></a>
## NLS_DATE_FORMAT

<a id="121220f3d70e3f76"></a>
### Basic Information

**Basic Information of NLS_DATE_FORMAT**

<a id="7f4eeb18b65ea28e"></a>
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

<a id="aa6af8e378fc33d7"></a>
### Description

NLS_DATE_FORMAT specifies the default date format of TO_CHAR and TO_DATE functions.

<a id="3eb7e8d0be6c45dd"></a>
## NLS_TIME_FORMAT

<a id="132fd93037ddb79f"></a>
### Basic Information

**Basic Information of NLS_TIME_FORMAT**

<a id="5f5c2628453e40e5"></a>
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

<a id="886383565c7f0860"></a>
### Description

NLS_DATE_FORMAT specifies the default time format of TO_CHAR and TO_DATE functions.

<a id="dc93f1addc88cbde"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="e9ed7f648daef533"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="3f03f919b015f0b1"></a>
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

<a id="f7e243af8c5e1fbe"></a>
### Description

NLS_TIME_WITH_TIME_ZONE FORMAT specifies the default time with time zone format of TO_CHAR and TO_TIME_WITH_TIME_ZONE functions.

<a id="f04f20ba0ffa3caf"></a>
## NLS_TIMESTAMP_FORMAT

<a id="cbc11e0869f7c085"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="55091445761de7c9"></a>
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

<a id="e290322655bf1a61"></a>
### Description

NLS_TIMESTAMP_FORMAT specifies the default timestamp format of TO_CHAR and TO_TIMESTAMP functions.

<a id="edba3110d229ce95"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="0c9b7709660a3343"></a>
### Basic Information

**Basic Information of NLS_TIMESTAMP_FORMAT**

<a id="3c2c9d6bc48f99a6"></a>
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

<a id="dc65b9c931e788b1"></a>
### Description

NLS_TIMESTAMP_WITH_TIME_ZONE FORMAT specifies the default timestamp with time zone format of TO_CHAR and TO_TIMESTAMP WITH TIMEZONE functions.

<a id="a3946de4fe4757ef"></a>
## NUMA

<a id="2f7f50fef8505159"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="9435591759dbed7e"></a>
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

<a id="66bb1c509e721d71"></a>
### Description

It enables NUMA.

> To use the NUMA property in AIX, the user account should be modified. Execute the following command as a root user.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> &lt;username&gt; is not a root but it is a user account of AIX.  
> Logout then login again to apply the modifications.

<a id="4ebf4c592ee18019"></a>
## NUMA_MAP

<a id="97b7ffb7a09b38e1"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="65d198cd9eceb4a1"></a>
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

<a id="63f1dda8382d0082"></a>
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

<a id="e25c07279cb0e6d8"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="2f4f278068617469"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="bdc90ceb93fbde46"></a>
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

<a id="c980f19187920457"></a>
### Description

The background process automatically takes the errored member offline after completing the failover caused by the node error.   

If it is not possible to take the errored member offline because it is set to *NO*, then execute the following syntax before the errored member joins the system again.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="44f3605d5c8218d7"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="72bae9046290e701"></a>
### Basic Information

<a id="b2a218c02d3bf030"></a>
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

<a id="08cd8441e409eca5"></a>
### Description

The table rebalancing online applies journal logs several times which were recorded by dml occurred during the performance in the cluster environment. MAXIMUM_JOURNAL_REPLAY_COUNT sets how many times to apply the journal logs. However, if the amount of journal logs to be applied are small, then it is not repeated as many as it is set to be, but instantly set the table the EXCLUSIVE lock, and uses it as the threshold value to apply the last journal log.

<a id="e6122346500d57e2"></a>
## OS_GROUP_ACCESS

<a id="c3018c1620730875"></a>
### Basic Information

**Basic Information of NLS_TIME_WITH_TIME_ZONE_FORMAT**

<a id="8ec52802e9508518"></a>
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

<a id="2a77253aad50d062"></a>
### Description

To connect to DA with another user of the same group, this property should be set to *YES*. Also, the umask of the system should be modified to *0002*.

<a id="fbb85a80a54ba497"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="0fd82c2c3bf6e76e"></a>
### Basic Information

<a id="c7c92826ed42af3f"></a>
| Item | Description |
| --- | --- |
| Name | PACKET_COMPRESSION_THRESHOLD |
| Summary | The size limit at which packets are compressed(bytes) |
| Data type | BIGINT |
| Applicable phase | NO MOUNT or above |
| Updatable | TRUE |
| ALTER SESSION | FALSE |
| ALTER SYSTEM | IMNEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| Default value | 2113929216 |

<a id="7669962dcfa83ec4"></a>
### Description

If the data size to be sent to the client is bigger than PACKET_COMPRESSION_THRESHOLD, it compresses the communication data.

<a id="984df5f741d0dddd"></a>
## PAGE_CHECKSUM_TYPE

<a id="774c22fc65147bf7"></a>
### Basic Information

**Basic Information of PAGE_CHECKSUM_TYPE**

<a id="7f222954e361bbd5"></a>
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

<a id="af0881f28782c262"></a>
### Description

A checksum is used to guarantee the physical consistency for each page of the datafile. GOLDILOCKS supports a page checksum of LSN, CRC scheme.

- 0: LSN
- 1: CRC

<a id="b8af8f0343fb73d1"></a>
## PARALLEL_IO_FACTOR

<a id="89f4739ff13c4e57"></a>
### Basic Information

**Basic Information of PARALLEL_IO_FACTOR**

<a id="f5b2965e871c8435"></a>
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

<a id="2e45187c24cadbb6"></a>
### Description

It sets the number of threads for the parallel loading of data file when starting database and the number of threads for parallel recording of data file at checkpoint.

<a id="d509fe567301ea85"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="ffdf9ff2c2619aa7"></a>
### Basic Information

**Basic Information of PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16**

<a id="c72dc5687342a69f"></a>
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

<a id="c98401fbd1c2f51f"></a>
### Description

It sets the group directory for parallel I/O of data file. It sets the number of group as many as PARALLEL_IO_FACTOR, then parallel I/O is performed in data file unit which belongs to each group.

<a id="374cf04edee92599"></a>
## PARALLEL_LOAD_FACTOR

<a id="623c2341697fb68d"></a>
### Basic Information

**Basic Information of PARALLEL_LOAD_FACTOR**

<a id="1034ba94bae632e8"></a>
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

<a id="de9c91f6d12fbbbf"></a>
### Description

When starting database, it sets the number of threads for parallel operation after loading the memory of a data file.

<a id="83ec657f153b005d"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="7b7196e6505be425"></a>
### Basic Information

**Basic Information of PENDING_LOG_BUFFER_COUNT**

<a id="e3c9b737fee1c3ad"></a>
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

<a id="45106d2066793bdb"></a>
### Description

When multiple transactions are simultaneously running, the pending log buffer is used to reduce the competition for the log buffer. PENDING LOG_BUFFER COUNT sets the number of pending log buffer which can be used simultaneously.

<a id="09468050ddd33c8a"></a>
## PLAN_CACHE

<a id="e0930cf3303f8938"></a>
### Basic Information

**Basic Information of PLAN_CACHE**

<a id="dd413adfff48f65a"></a>
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

<a id="809cead6d46e72d3"></a>
### Description

It determines whether to use the plan cache.

<a id="24e016228c42e6b3"></a>
## PLAN_CACHE_SIZE

<a id="68d562b973b6efba"></a>
### Basic Information

**Basic Information of PLAN_CACHE_SIZE**

<a id="24d8931e1c342702"></a>
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

<a id="c70fd9a9898db319"></a>
### Description

It sets the memory size to be used for the plan cache.

<a id="722f65ccf4edf334"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="03b4d971a347f27b"></a>
### Basic Information

**Basic Information of PRIVATE_STATIC_AREA_SIZE**

<a id="d7e554ad41e0c44e"></a>
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

<a id="960fa3d2b0ad8dcf"></a>
### Description

It specifies the maximum heap memory size to be allocated by the session.

<a id="e6be5a40eced0bcb"></a>
## PROCESS_MAX_COUNT

<a id="4ac3258076f46ce4"></a>
### Basic Information

**Basic Information of PROCESS_MAX_COUNT**

<a id="0a6710172b519421"></a>
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

<a id="9992f951821e7e53"></a>
### Description

It specifies the maximum number of processes (threads) available on the system.

Creating system process  
• The process is created each time of connection to D/A mode or C/S dedicated mode.  
• In C/S shared mode, processes are basic balancer, dispatcher and shared-server. A process is   
&nbsp;&nbsp;not created when connecting from client.

<a id="d41346e6fc64764e"></a>
## QUERY_TIMEOUT

<a id="0897ab4b11bab06a"></a>
### Basic Information

**Basic Information of QUERY_TIMEOUT**

<a id="d686283d84f2ffab"></a>
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

<a id="7f61313497b67ad2"></a>
### Description

It specifies the maximum time which a command received from the session can be executed. If the execution time exceeds, the TIMEOUT error occurs.

- 0: It means infinite waiting, and TIMEOUT error does not occur.

<a id="aebf653c4cfecf7e"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="e8a1b5dd97883db4"></a>
### Basic Information

**Basic Information of READABLE_ARCHIVELOG_DIR_COUNT**

<a id="4e932848b415a550"></a>
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

<a id="399b003c6b688e01"></a>
### Description

It sets the number of directories in which archive redo logs exist when executing media recovery.

<a id="84ad7223f821541b"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="8667242ad329e717"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="fee4a8e2b25a63f3"></a>
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

<a id="3a69ca2a30af0fcd"></a>
### Description

It sets the number of directories in which incremental backups exist when restoring files using incremental backups.

<a id="33932bd342844e56"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="29f37b59b8c81154"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="0fa227986ded455a"></a>
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

<a id="8be2ec997e2969e4"></a>
### Description

It is the block read count for rebalance.

<a id="ae66ced73047c8e0"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> It is not supported after 3.1.

<a id="ecb34dc44e93f882"></a>
### Basic Information

**Basic Information of READABLE_BACKUP_DIR_COUNT**

<a id="622e8f896d7c2e8b"></a>
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

<a id="d25e8c3fbeb3c379"></a>
### Description

It sets the minimum page count to check if the plan is recompiled due to the page count modification.

<a id="d90a5fd3aaa1ed78"></a>
## RECOMPILE_PAGE_PERCENT

> It is not supported after 3.1.

<a id="c41b9888cc4740a8"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="c7273cef68d84123"></a>
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

<a id="0fa02ef78277d140"></a>
### Description

It sets the page percentage when recompiles the plan due to the page count modification. If its value is 0, it does not recompile due to the page count modification.

<a id="4c30cfb26db3d2ad"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="5a171db9b498c3c7"></a>
### Basic Information

<a id="d9c9a862a677a3de"></a>
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

<a id="ed21fc86aba150b7"></a>
### Description

It is the default log buffer size for recovery.

<a id="359482e7ceb5193e"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="16d6f6b082357810"></a>
### Basic Information

**Basic Information of RECOMPILE_PAGE_PERCENT**

<a id="88e0d41b3a2f5c17"></a>
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
| Default value | 256 |

<a id="f214da99d2531b5e"></a>
### Description

If the size of the created REDO LOG is bigger than REDO_LOG_COMPRESSION_THRESHOLD value, it compresses REDO LOG.

<a id="c3024be0d33635c2"></a>
## REFINE_RELATION

<a id="95e21d52548225b6"></a>
### Basic Information

<a id="107b4541f6239ee2"></a>
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

<a id="45ec4feccb4c3712"></a>
### Description

If this property is set to NO, then REFINE RELATION process is not preformed when restarting the server.

This property can be used when an error occurs during the REFINE RELATION process. However, segments of RELATIONs (tables or indexes) which were dropped but not REFINEd can not be reused. When resolving the error then setting this property to YES and restarting, it tries to REFINE relations which were not dropped.

<a id="06934126d865acc3"></a>
## SESSION_FATAL_BEHAVIOR

<a id="13cd21eb97dc798a"></a>
### Basic Information

**Basic Information of SESSION_FATAL_BEHAVIOR**

<a id="5ec89b21fc7636bd"></a>
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

<a id="a926c963c4749b6c"></a>
### Description

When session fatal occurs, it determines whether to terminate only the thread which caused the fatal or to terminate the process.

- 0: It terminates only the thread which caused fatal.
- 1: It terminates the process.  
  If multiple sessions are simultaneously performed in the process, the process is terminated after all sessions finish using database.

<a id="eb64f1e0a7cb533d"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="d767773a509988e4"></a>
### Basic Information

<a id="01fff3aa7ad70b27"></a>
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

<a id="766afd26c989b627"></a>
### Description

It sets the shared memory size to be allocated in advance so that it can be used in the session.

<a id="6f03cb96ef7506a0"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="9fd17cf40de59641"></a>
### Basic Information

<a id="640748fcca3c5814"></a>
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

<a id="3a7466569ea83247"></a>
### Description

It sets the threshold value to determine whether to return the dynamic shared memory which is not used by the session to the system when releasing the dynamic shared memory used in the session. In other words, if the memory chunk which is bigger than the set value among unused memory exists, then it is returned to the system.

<a id="e1d37fe11b4892fe"></a>
## SHARED_MEMORY_ADDRESS

<a id="174a57c07e91e9b2"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_ADDRESS**

<a id="5d3c82250e135cf1"></a>
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

<a id="7aac36f119610917"></a>
### Description

It specifies the address of Shared Static Area (SSA).

<a id="272f565dc3f2cfc9"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="4f9223875a8dcb53"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_KEY**

<a id="7912193ad6f51dec"></a>
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

<a id="980e9e8f4e0d6336"></a>
### Description

When running server, it specifies the shared memory key values which are used to allocate Static Shared Area (SSA) space.

<a id="782a487318613280"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="14aac38ed55afc4b"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_NAME**

<a id="37fe23a6e08a0ec4"></a>
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

<a id="165c061ed60c27ef"></a>
### Description

When running server, it specifies the shared memory name which is used to allocate Static Shared Area (SSA) space.

<a id="8041640dedffa5a3"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="c63323275ed46980"></a>
### Basic Information

**Basic Information of SHARED_MEMORY_STATIC_SIZE**

<a id="73d8d81e41155251"></a>
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

<a id="ce507be241b92252"></a>
### Description

It specifies the size of the Shared Static Area (SSA).

<a id="aed2727fce81109e"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="15f15263fad77fc1"></a>
### Basic Information

**Basic Information of SHARED_REQUEST_QUEUE_COUNT**

<a id="757f1e79045120a3"></a>
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

<a id="548d1c370be7014c"></a>
### Description

In shared mode, it sets the number of queues of which the dispatcher requests to the shared-server. A queue is used when multiple dispatchers allocate user's requests to the shared-server. Generally, a single queue is used for the load-balance.   
However, SHARED_REQUEST_QUEUE_COUNT value is increased because if the number of dispatchers and shared-servers increase, then a conflict to the queue causes performance degradation.   
If the value becomes bigger, the load-balance can be inefficient and the possibility of deadlock increases.

<a id="10a21617473175db"></a>
## SHARED_SERVERS

<a id="b6f005ce224fe140"></a>
### Basic Information

**Basic Information of SHARED_SERVERS**

<a id="32e92fb36fbfa297"></a>
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

<a id="310f57b8af12d1ec"></a>
### Description

It sets the number of shared-server processes on shared mode.  
At open phase, the value can not be decreased by using alter system.

<a id="9bbb68283f9dda80"></a>
## SHARED_SESSION

<a id="6a1d75eaf11ff72d"></a>
### Basic Information

**Basic Information of SHARED_SESSION**

<a id="94e208f9c769eb22"></a>
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

<a id="35f8cdb7e2a23591"></a>
### Description

It sets whether to activate shared mode. If the value is set to *NO*, load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver) are not executed.

<a id="f4d1789453b550dd"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="47a2db97a8a6cfd4"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="9468190e7229f314"></a>
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

<a id="cc38067a2cbaa2e6"></a>
### Description

It sets the maximum holding time of the statement required for the snapshot read. TIMEOUT error occurs for a snapshot statement which exceeds the time.

<a id="aa61c2ce9c14e237"></a>
## SQL_HISTORY_SIZE

<a id="0c126358df518a11"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="3b28e5895911c266"></a>
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

<a id="24d5f41a21baa80d"></a>
### Description

It is the history size for SQLs.

<a id="3284213803b3f5ef"></a>
## SQL_HISTORY_TYPE

<a id="6266f031c73b2d35"></a>
### Basic Information

**Basic Information of SNAPSHOT_STATEMENT_TIMEOUT**

<a id="93bf2f1ab299d78f"></a>
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

<a id="65955ef4644b94f2"></a>
### Description

It is the history type for SQLs.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="8a3483fc31569df3"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="2d74105d2949f5d4"></a>
### Basic Information

**Basic Information of SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY**

<a id="aed557e9eedd3d02"></a>
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

<a id="30430f343ae8b7e1"></a>
### Description

It records supplemental log for all changes in the database.

<a id="904a35dbd39b1ec5"></a>
## SYSTEM_LOGGER_DIR

<a id="367e6682cb29c332"></a>
### Basic Information

<a id="eca95e69f0418dc0"></a>
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

<a id="3e8af975028491be"></a>
### Description

It sets the disk path on which the trace log message is recorded.

<a id="aa09534fd27a4c07"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="1ee3f6c6a35dd437"></a>
### Basic Information

<a id="a5dd2ff1ebb7f8c8"></a>
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

<a id="3cead1ed85cc9e2a"></a>
### Description

It determines the size of initial MEM_AUX_TBS tablespace when creating the database.

<a id="82fe4c539270cd7b"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="ef8f43e66fa28145"></a>
### Basic Information

<a id="5a481cf4ba63669c"></a>
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

<a id="24d3442926299d4b"></a>
### Description

It determines the initial tablespace size of MEM_DATA_TBS when creating database.

<a id="3cd49ea545591df4"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="271c9965d97b06c2"></a>
### Basic Information

<a id="7362f86cf6dfedcb"></a>
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

<a id="d2539f7594e25543"></a>
### Description

It determines the initial tablespace size of DICTIONARY_TBS when creating database.

<a id="d57294040c37696f"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="afc95819fd866c9e"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE**

<a id="02b45c2ddd4f6958"></a>
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

<a id="f0c8536cf538e32a"></a>
### Description

It determines the initial tablespace size of MEM_TEMP_TBS when creating database.

<a id="fa913700b8ae00ac"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="7c436674af2c0918"></a>
### Basic Information

**Basic Information of SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE**

<a id="91adfe5d4e61f289"></a>
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

<a id="9563006ad2a7a768"></a>
### Description

It determines the initial tablespace size of MEM_UNDO_TBS when creating database.

<a id="c215123430e1cdbf"></a>
## SYSTEM_TABLESPACE_DIR

<a id="fbe0d4143a654dfa"></a>
### Basic Information

<a id="13f94741d6e08967"></a>
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

<a id="312ac084f0bfb771"></a>
### Description

It sets the path to which the initial system tablespaces are stored when creating database.

<a id="fc821225ee6f6d0a"></a>
## SYSTEM_UDS_DIR

<a id="e0308901d3f6c0fb"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="dfe398e47293b2e8"></a>
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

<a id="989b0254362024b2"></a>
### Description

It sets a directory on which the unix domain socket file is created.  
Setting the directory for the unix domain socket except for DB system, such asglsnr, is managed by a separate configuration file.  
The maximum setting value is 60 bytes. (The maximum size of the absolute path (directory + file name) for the unix domain socket file varies according to OS, but generally it is around 100 bytes.)

<a id="db164012dd41c7ba"></a>
## TCP_CLIENT_NUMA_NODE

<a id="8a217cba68fd9a02"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="8e09b65441c16ece"></a>
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

<a id="f4cfad23377c67a1"></a>
### Description

It sets the NUMA node ID to which the client server session is bound. This property is operated when NUMA property is set to on.

<a id="c7f214399bbbcfb6"></a>
## TCP_NODELAY

<a id="6d68cce3e9edd4f8"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="fe12ff259548bf39"></a>
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

<a id="c14fe0dfbab7a3c1"></a>
### Description

It sets TCP_NODELAY option of the socket when transferring the data to a client in C/S method (TCP socket).  
Set it to *NO* when fast latency is not required and reducing the network load is needed.

<a id="6d1ca0c0fae9e706"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="f2cfc783711e82ba"></a>
### Basic Information

<a id="2409018a84d50edb"></a>
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

<a id="b49511a1bad9c288"></a>
### Description

It sets the number of segments to be cached in a session instead of returning them to a tablespace when dropping a global temporary table or a global temporary index segment. Segments in the segment cache are reused later in a global temporary table or a global temporary index.

- 0: It does not use a segment cache of a global temporary table or of a global temporary index in a session.
- 1 ~ 4294967295: It keeps the specific number of segment caches of a global temporary table or a global temporary index in a session.

<a id="dd4d5a08e3407bc2"></a>
## TEMP_UNDO_ENABLED

<a id="a426a893139e8092"></a>
### Basic Information

<a id="2658d173056d7289"></a>
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

<a id="7e4c52f526dba2d9"></a>
### Description

It defines the location of logging undo records for a global temporary table.

- 0 (FALSE): It records the undo records in the default undo tablespace of database. 
- 1 (TRUE): It records the undo records in the default temporary tablespace of database.

<a id="8f4e742e91bb96c1"></a>
## TIMED_STATISTICS

<a id="1fdbf4c40aee628e"></a>
### Basic Information

**Basic Information of SYSTEM_TABLESPACE_DIR**

<a id="4d1d8821beafc988"></a>
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

<a id="4b37d0dddc0498f2"></a>
### Description

It is whether to check the wait event.  
To record the statistics related to wait event on v$system_event, v$session_event and v$session_wait table, set this property.

- 0: It does not record the statistics.
- 1: It records the statistics.
- 2: It records the statistics by using the high precision timer.

<a id="c44fdc9c88a6cf8e"></a>
## TIMEZONE

<a id="cac0036963e56bb9"></a>
### Basic Information

**Basic Information of TIMEZONE**

<a id="b9c437f7b1dfe87e"></a>
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

<a id="4e5dd9aa7a8b6ad7"></a>
### Description

It is a time zone value of database.  
It is applied when creating database, and it uses the value of the range from '-14:00' to '+14:00'.

<a id="8fae541b6c1a3a58"></a>
## TRACE_ALTER_SYSTEM

<a id="a2bf031a892707d4"></a>
### Basic Information

**Basic Information of TRACE_ALTER_SYSTEM**

<a id="56d45593c12076e3"></a>
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

<a id="f01cdca76973594e"></a>
### Description

It records the SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) when executing ALTER SYSTEM syntax.

Set TRACE_ALTER_SYSTEM property to *ON* to record system changes.

SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax have nothing to do with TRACE_ALTER_SYSTEM property, so they do not affect the performance of TRACE_ALTER_SYSTEM.

<a id="473ad34ba1f8053f"></a>
## TRACE_DDL

<a id="c73f0717b8e07898"></a>
### Basic Information

**Basic Information of TRACE_DDL**

<a id="dc66999482b66265"></a>
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

<a id="f7eb57f194eb1df0"></a>
### Description

When executing DDL, it records the executed SQL statements in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

Set *TRACE_ALTER_SYSTEM* property to *ON* to record SQL statements execution such as CREATE/DROP/ALTER table.

TRACE_DDL property affects only to DDL statements. However, it has nothing to do with SELECT inquiry, and execution of INSERT, UPDATE, DELETE syntax. Therefore, it does not affect the performance.

<a id="c84f8aaff4a549a8"></a>
## TRACE_LOG_ID

<a id="1ede902e285e5839"></a>
### Basic Information

**Basic Information of TRACE_LOG_ID**

<a id="cea34ea00edb698c"></a>
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

<a id="6234d096c145d472"></a>
### Description

The execution plan for the query, and other related information are recorded in the trace file (opt_p[process ID_s [session ID].trc) under the trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) when processing queries.

To record SQL statement for the query, the execution plan and the execution time, refer to the following flag information.

**Flag information for TRACE_LOG_ID**

<a id="b5a45e880754b925"></a>
| Information | Flag(on) | Flag(off) |
| --- | --- | --- |
| Whether to output the successful SQL query | 100000 | 0 |
| Whether to output the failed SQL query | 10000 | 0 |
| Whether to output the execution plan | 1000 | 0 |
| Whether to output the execution type (direct/prepare) | 100 | 0 |
| Whether to output the bind value | 10 | 0 |
| Whether to output the execution time per section | 1 | 0 |

To set it in a form of "output the successful SQL query" + "output the execution plan" + "output the bind value", set the TRACE_LOG_ID value to 101010.

<a id="75c8b16b181aa8fa"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="d25130bfaf0ca2f0"></a>
### Basic Information

<a id="d96731b8d3bb8a75"></a>
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
| Default value | 8192 |

<a id="67086810752fe22a"></a>
### Description

It sets the size of the heap memory buffer which is used to configure the log message to be recorded in the trace logfile.

<a id="bb3403753f23bba1"></a>
## TRACE_LOG_TIME_DETAIL

<a id="f66d5607b3825fe1"></a>
### Basic Information

**Basic Information of TRACE_LOG_TIME_DETAIL**

<a id="84ec54825f3b92dd"></a>
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

<a id="81f698405ac9936c"></a>
### Description

It sets whether to increase the time accuracy when recording trace log.  
If the value is ON, it has an accuracy of 1 us.  
If the value is OFF, it has an accuracy of 10 ms.

<a id="c80d288fb9b30a69"></a>
## TRACE_LOGGER

<a id="19c62a95a2ff1c4e"></a>
### Basic Information

<a id="da9971530cd66849"></a>
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

<a id="8ad05527a23baf3a"></a>
### Description

It sets the target on which the trace log is written.  
If it is 1, then it is recorded in a file, and if it is 2, then it is remotely recorded in a file.  
When it is remotely written, then it remotely collects trace logs from gtrclogger and records in a file.

<a id="3c8688fe2a78e1dd"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="cdc0d0620ebb0e87"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="b62727c2535a0f35"></a>
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

<a id="d84aa91d510e9322"></a>
### Description

It sets the host to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="ebc8e4c0f581c684"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="77ec4ae7b280dfbb"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="9450c753ecd9af16"></a>
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

<a id="42cbd66518412f48"></a>
### Description

It sets the port to which the trace log is remotely transferred by setting TRACE_LOGGER to 2.

<a id="429fdaf58469d325"></a>
## TRACE_LOGIN

<a id="120838561a21bd5d"></a>
### Basic Information

**Basic Information of TRACE_LOGIN**

<a id="902c1071a302b6ab"></a>
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

<a id="7043931e902742d0"></a>
### Description

It records the related access information in trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc) on login.  
Set TRACE_LOGIN property to *ON* to record the related information on login.

<a id="3a76766465577107"></a>
## TRACE_LONG_RUN_CURSOR

<a id="5ddbcce4bf84009b"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_CURSOR**

<a id="02c8434ae502710e"></a>
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

<a id="7e7f0efd1d57ab01"></a>
### Description

When cursor life-time is longer than the specified property time, then it records the SQL statement of the cursor in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.

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
```

- Due to the user logic, ager fails to clean up resources for a long time.

```
long_run_user_logic( s_name );

   EXEC SQL CLOSE cur1;
   ...
}
```

<a id="3a07d3f71a86e02e"></a>
## TRACE_LONG_RUN_SQL

<a id="9fbf0181c642923b"></a>
### Basic Information

**Basic Information of TRACE_LONG_RUN_SQL**

<a id="6c055ed3aa5242be"></a>
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

<a id="237b7b5c7ac8849f"></a>
### Description

It records the SQL statement whose execution time is longer than the specified property time in the trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc).

- Description of value
    - Unit: millisecond
    - Value 0: It does not record information.
    - Recommended value: 20 (millisecond) or longer
    - The value of 20 or longer is recommended because the execution time is measured using the time tic in 10 ms period.

The following is an example of recording the SQL statement whose execution time is longer than 1 second.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

The following is an example of restoring to the default value.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="8aa6cecfec9a8cd2"></a>
## TRACE_XA

<a id="179c2dc69aba728f"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="fdcb878d77927bbf"></a>
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

<a id="6ba298487be57655"></a>
### Description

It specifies whether to output trace messages when using XA interface. Message is output to the 'SYSTEM_LOGGER_DIR / xa.trc'.

<a id="15e89cc52748e97b"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="049d72793ac007ea"></a>
### Basic Information

**Basic Information of TRACE_XA**

<a id="8e4b42a2adb38e2e"></a>
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

<a id="b1d44c44e1d1b38e"></a>
### Description

It is the maximum waiting time when allocating transaction slots.

The following error occurs when the waiting time exceeds TRANSACTION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="b15ab11f95d1bff6"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="cceb2b1b2e73d934"></a>
### Basic Information

**Basic Information of TRANSACTION_COMMIT_WRITE_MODE**

<a id="57c6771510ab3d62"></a>
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

<a id="0f320b77913c3a6f"></a>
### Description

TRANSACTION_COMMIT_WRITE_MODE specifies whether a log generated by the transaction is flushed to the disk log file, when the transaction is committed. If TRANSACTION_COMMIT_WRITE_MODE is '1', the log should be flushed to the disk log file at the time of the transaction commit. Otherwise the transaction is committed regardless of log flush.

If the system is operated when TRANSACTION_COMMIT_WRITE_MODE is set to '0', the latest data willbe lost when GOLDILOCKS is abnormally terminated without log flush after COMMIT transaction. It is because the logs are not recorded in this case.

Therefore, if all committed transactions should be remained (stored) in database, the system should be operated after setting TRANSACTION_COMMIT_WRITE_MODE to '1'. Or, 'ALTER SYSTEM FLUSH LOGS' statement should be explicitly performed at the time of transaction commit in order to flush log after TRANSACTION_COMMIT_WRITE_MODE is set to '0'.

- 0: no wait
- 1: wait

<a id="596c757cd074198e"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="5d70dcabb04e8a17"></a>
### Basic Information

**Basic Information of TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT**

<a id="ee9aa038cfd2b672"></a>
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
| MAX | 838860800 |
| Default value | 838860800 |

<a id="1daff82b0fc5d21a"></a>
### Description

It means the maximum number of undo pages which the transaction can record. The minimum value is 1 (8 Kbytes) and the maximum value is 838860800 (100 Gbytes).

<a id="69904313042bebe3"></a>
## TRANSACTION_TABLE_SIZE

<a id="fb9cf229e26119b2"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="10fef79997c84f3d"></a>
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

<a id="ac2f8c3f2e98f907"></a>
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

<a id="1ec27a4ff5980889"></a>
## TRANSACTION_TIMEOUT

<a id="db5a95ef8211cd31"></a>
### Basic Information

**Basic Information of TRANSACTION_TABLE_SIZE**

<a id="7dc6899b5bb76d8f"></a>
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

<a id="b5cfd8e54cb9829b"></a>
### Description

It sets the duration of when the transaction is activated. It is used to prevent the side effects of when the transaction is activated for a long time. If a transaction exceeds the specified time, then gmaster daemon automatically terminates the session owned by that transaction.

<a id="70a7aaa26d88eab5"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="ed4cab30fa0e4a7c"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="3f00de8714558af6"></a>
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

<a id="61b35fa37903ee49"></a>
### Description

It is the maximum waiting time when allocating undo relations.

The following error occurs when the waiting time exceeds UNDO_RELATION_ALLOCATION_TIMEOUT.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="16bc24d1ebe8cc2a"></a>
## UNDO_RELATION_COUNT

<a id="30224313611dc875"></a>
### Basic Information

**Basic Information of UNDO_RELATION_COUNT**

<a id="921bf4dbd5a8907b"></a>
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

<a id="0bab760f42d1c8c3"></a>
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

<a id="c1e2a3491298981a"></a>
## UNDO_SHRINK_THRESHOLD

<a id="8c6d28d17792525b"></a>
### Basic Information

**Basic Information of UNDO_SHRINK_THRESHOLD**

<a id="93e6d49021214721"></a>
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

<a id="8a253e16368874da"></a>
### Description

Ager thread periodically (10 seconds) checks the undo segment space. If an undo segment uses too much space, a part of it is returned to the tablespace. The property specifies the size (in bytes) of the space to be returned at a time.

<a id="5a65cc9ecf6f9b46"></a>
## USE_LARGE_PAGES

<a id="19163d3f2fbe8de6"></a>
### Basic Information

<a id="143e23852e7d33e3"></a>
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

<a id="ce06833ff3c80ed3"></a>
### Description

It uses HugePage. HugePage should be set in the device beforehand to use USE_LARGE_PAGES.

- 0: It does not use the large page.
- 1: It uses the large page. If it fails to allocate the shared memory, then an error occurs. 
- 2: It tries to allocate the shared memory by using the large page. If it fails to allocate the shared memory, then it allocates the memory by using the regular page.

> It can be used only in Linux kernel 2.6.32-573 or higher.

---

[← 9. Database Information](9-database-information.md) · [Table of contents](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
