<a id="451ba7bc1cac94dc"></a>

# 4. What's New

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/451ba7bc1cac94dc)  
> 태그: `26c.1_0_tag`

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<a id="706a9db62cf2e65a"></a>
## Feature Matrix

본 장에서는 각 major version 별로 추가된 주요 기능들에 대해 간략히 설명한다.

<a id="02803adb8c51e183"></a>
### Architecture

<a id="bb5de6a7b9a869e8"></a>
#### System Architecture

System architecture에 대한 feature matrix는 다음과 같다.

**System architecture의 feature matrix**

<a id="f47994317d9e7a83"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| Shared Nothing Cluster | O | O | O | O | O |
| DA (Direct Attach) | O | O | O | O | O |
| JDBC DA (Direct Attach) | O | O | O | O | O |
| C/S (Client/Server) Dedicated | O | O | O | O | O |
| C/S (Client/Server) Shared | O | O | O | O | O |
| multi-process applications | O | O | O | O | O |
| multi-threaded applications | O | O | O | O | O |
| Linux platform | O | O | O | O | O |
| HP platform | O | O | O | O | X |
| AIX platform | O | O | O | O | X |
| Windows Client Platform | O | O | O | O | O |
| CDC(Change Data Capture) replication | O | O | O | O | O |
| CDC replication with log mirror | O | O | O | O | O |
| multi-level start up | O | O | O | O | O |
| parallel database loading | O | O | O | O | O |
| parallel index build | O | O | O | O | O |
| SQL plan cache | O | O | O | O | O |
| IPC | X | X | O | O | O |

<a id="bdfb366883310a3e"></a>
#### Storage Internal

Storage internal에 대한 feature matrix는 다음과 같다.

**Storage internal의 feature matrix**

<a id="3fdee14e8539eb6c"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| memory dictionary tablespace | O | O | O | O | O |
| memory data tablespace | O | O | O | O | O |
| memory undo tablespace | O | O | O | O | O |
| memory temporary tablespace | O | O | O | O | O |
| memory bitmap data segment | O | O | O | O | O |
| memory bitmap undo segment | O | O | O | O | O |
| memory bitmap instant segment | O | O | O | O | O |
| memory heap table | O | O | O | O | O |
| memory instant table | O | O | O | O | O |
| memory B-tree index | O | O | O | O | O |
| memory instant B-tree | O | O | O | O | O |
| memory instant hash | O | O | O | O | O |
| global secondary index | O | O | O | O | O |
| disk data tablespace | X | O | O | O | O |
| disk bitmap data segment | X | O | O | O | O |
| disk B-tree index | X | O | O | O | O |
| disk global secondary index | X | O | O | O | O |

<a id="d80b929ee83d92f3"></a>
#### Transaction Control

Transaction control에 대한 feature matrix는 다음과 같다.

**Transaction control의 feature matrix**

<a id="52db231787aba3af"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| CDS(Concurrency Data Store) database mode | O | O | O | O | O |
| TDS(Transactional Data Store) database mode | O | O | O | O | O |
| read-only database | O | O | O | O | O |
| read/write database | O | O | O | O | O |
| flat transaction | O | O | O | O | O |
| distributed transaction | O | O | O | O | O |
| read-only transaction | O | O | O | O | O |
| read/write transaction | O | O | O | O | O |
| READ COMMITTED isolation level | O | O | O | O | O |
| SERIALIZABLE isolation level with SELECT FOR UPDATE | O | O | O | O | O |
| MVCC(Multi Version Concurrency Control) | O | O | O | O | O |
| multi-version read consistency | O | O | O | O | O |
| multi-statement consistent read | O | O | O | O | O |
| implicit lock for DML | O | O | O | O | O |
| writer don't blocks readers | O | O | O | O | O |
| row-level locking | O | O | O | O | O |
| deadlock detection | O | O | O | O | O |
| deadlock resolution | O | O | O | O | O |
| lock granularity | O | O | O | O | O |
| read lock | O | O | O | O | O |
| write lock | O | O | O | O | O |
| intention lock | O | O | O | O | O |
| WAL(Write Ahead Logging) | O | O | O | O | O |
| repeat history | O | O | O | O | O |
| restart recovery | O | O | O | O | O |
| circular logging | O | O | O | O | O |
| buffered logging | O | O | O | O | O |
| logging group | O | O | O | O | O |
| supplemental logging | O | O | O | O | O |
| mirrored logging | O | O | O | O | O |
| synchronous commit | O | O | O | O | O |
| asynchronous commit | O | O | O | O | O |
| grouped commit | O | O | O | O | O |
| total rollback | O | O | O | O | O |
| implicit statement rollback | O | O | O | O | O |
| savepoint management | O | O | O | O | O |

<a id="3d00e2abb84a2829"></a>
#### Backup & Recovery

Backup & recovery에 대한 feature matrix는 다음과 같다.

**Backup & recovery의 feature matrix**

<a id="b2b1222860ba8485"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| off-line backup | O | O | O | O | O |
| on-line backup | O | O | O | O | O |
| full backup | O | O | O | O | O |
| incremental backup | O | O | O | O | O |
| complete recovery | O | O | O | O | O |
| incomplete recovery | O | O | O | O | O |
| auto instance recovery | O | O | O | O | O |
| tablespace recovery | O | O | O | O | O |
| file recovery | O | O | O | O | O |
| change tracking | X | O | O | O | O |
| parallel recovery | X | X | X | X | O |
| parallel backup | X | X | X | X | O |
| parallel restore | X | X | X | X | O |

<a id="51409206757499ed"></a>
#### Database Information

<a id="8b880ed7ded9f7a5"></a>
##### DICTIONARY_SCHEMA 스키마

DICTIONARY_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

<a id="17a9c7307959326b"></a>
<table class="table column_count_7"><caption>DICTIONARY_SCHEMA schema의 feature matrix</caption><thead><tr><th class="to_center"><div>계열</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="64"><div>ALL_ 계열 view</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="56"><div>DBA_ 계열 view</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ROLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="62"><div>USER_ 계열 view</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="28"><div>기타 view</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GLOBAL_DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_ROLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4639f8d8876963f2"></a>
##### INFORMATION_SCHEMA 스키마

INFORMATION_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**INFORMATION_SCHEMA schema의 feature matrix**

<a id="f5e2289475413a9f"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| ADMINISTRABLE_ROLE_AUTHORIZATIONS | X | X | X | X | O |
| APPLICABLE_ROLES | X | X | X | X | O |
| CHECK_CONSTRAINTS | X | X | X | X | O |
| COLUMNS | O | O | O | O | O |
| COLUMN_PRIVILEGES | O | O | O | O | O |
| CONSTRAINT_COLUMN_USAGE | O | O | O | O | O |
| CONSTRAINT_TABLE_USAGE | O | O | O | O | O |
| ENABLED_ROLES | X | X | X | X | O |
| INFORMATION_SCHEMA_CATALOG_NAME | O | O | O | O | O |
| KEY_COLUMN_USAGE | O | O | O | O | O |
| MODULES | X | O | O | O | O |
| MODULE_BODY | X | O | O | O | O |
| MODULE_BODY_MODULE_USAGE | X | O | O | O | O |
| MODULE_BODY_ROUTINE_USAGE | X | O | O | O | O |
| MODULE_BODY_SEQUENCE_USAGE | X | O | O | O | O |
| MODULE_BODY_TABLE_USAGE | X | O | O | O | O |
| MODULE_MODULE_USAGE | X | O | O | O | O |
| MODULE_PRIVILEGES | X | O | O | O | O |
| MODULE_ROUTINE_USAGE | X | O | O | O | O |
| MODULE_SEQUENCE_USAGE | X | O | O | O | O |
| MODULE_TABLE_USAGE | X | O | O | O | O |
| PARAMETERS | O | O | O | O | O |
| REFERENTIAL_CONSTRAINTS | O | O | O | O | O |
| ROLE_COLUMN_GRANTS | X | X | X | X | O |
| ROLE_MODULE_GRANTS | X | X | X | X | O |
| ROLE_ROUTINE_GRANTS | X | X | X | X | O |
| ROLE_TABLE_GRANTS | X | X | X | X | O |
| ROLE_USAGE_GRANTS | X | X | X | X | O |
| ROUTINES | O | O | O | O | O |
| ROUTINE_MODULE_USAGE | X | O | O | O | O |
| ROUTINE_PRIVILEGES | O | O | O | O | O |
| ROUTINE_ROUTINE_USAGE | O | O | O | O | O |
| ROUTINE_SEQUENCE_USAGE | O | O | O | O | O |
| ROUTINE_TABLE_USAGE | O | O | O | O | O |
| SCHEMATA | O | O | O | O | O |
| SEQUENCES | O | O | O | O | O |
| SQL_FEATURES | O | O | O | O | O |
| SQL_IMPLEMENTATION_INFO | O | O | O | O | O |
| SQL_PACKAGES | O | O | O | O | O |
| SQL_PARTS | O | O | O | O | O |
| SQL_SIZING | O | O | O | O | O |
| STATISTICS | O | O | O | O | O |
| TABLES | O | O | O | O | O |
| TABLE_CONSTRAINTS | O | O | O | O | O |
| TABLE_PRIVILEGES | O | O | O | O | O |
| TRIGGER_EVENT_ORDER | X | X | X | X | O |
| TRIGGER_MODULE_USAGE | X | X | X | X | O |
| TRIGGER_ROUTINE_USAGE | X | X | X | X | O |
| TRIGGER_SEQUENCE_USAGE | X | X | X | X | O |
| TRIGGER_TABLE_USAGE | X | X | X | X | O |
| TRIGGERED_UPDATE_COLUMNS | X | X | X | X | O |
| TRIGGERS | X | X | X | X | O |
| USAGE_PRIVILEGES | O | O | O | O | O |
| VIEWS | O | O | O | O | O |
| VIEW_MODULE_USAGE | X | O | O | O | O |
| VIEW_ROUTINE_USAGE | O | O | O | O | O |
| VIEW_TABLE_USAGE | O | O | O | O | O |

<a id="8ddbeb7e1ad40534"></a>
##### PERFORMANCE_VIEW_SCHEMA 스키마

PERFORMANCE_VIEW_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**PERFORMANCE_VIEW_SCHEMA schema의 feature matrix**

<a id="fd9e58a5c3d18c58"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| GV$____ | O | O | O | O | O |
| V$AGABLE_INFO | O | O | O | O | O |
| V$ALLOCATOR | X | X | X | X | O |
| V$ARCHIVELOG | O | O | O | O | O |
| V$AUDITABLE_DB_PRIVILEGES | O | O | O | O | O |
| V$AUDITABLE_SYSTEM_ACTIONS | O | O | O | O | O |
| V$BACKUP | O | O | O | O | O |
| V$BALANCER | O | O | O | O | O |
| V$BCH | X | O | O | O | O |
| V$BUFFER_STAT | X | O | O | O | O |
| V$CLUSTER_COMMAND | X | X | X | X | O |
| V$CLUSTER_CONNECTION | X | X | X | X | O |
| V$CLUSTER_DISPATCHER | O | O | O | O | O |
| V$CLUSTER_LOCATION | O | O | O | O | O |
| V$CLUSTER_MEMBER | O | O | O | O | O |
| V$CLUSTER_QUEUE | X | X | X | X | O |
| V$COLUMNS | O | O | O | O | O |
| V$CONTROLFILE | O | O | O | O | O |
| V$DATAFILE | O | O | O | O | O |
| V$DB_CHANGE_TRACKING | X | O | O | O | O |
| V$DB_FILE | O | O | O | O | O |
| V$DB_PROPERTY | X | X | X | O | O |
| V$DISPATCHER | O | O | O | O | O |
| V$ERROR_CODE | O | O | O | O | O |
| V$GLOBAL_TRANSACTION | O | O | O | O | O |
| V$JOURNALING | O | O | O | O | O |
| V$INCREMENTAL_BACKUP | O | O | O | O | O |
| V$INSTANCE | O | O | O | O | O |
| V$KEYWORDS | O | O | O | O | O |
| V$LATCH | O | O | O | O | O |
| V$LICENSE | X | X | X | O | O |
| V$LOCK_WAIT | O | O | O | O | O |
| V$LOCKED_OBJECT | X | O | O | O | O |
| V$LOGFILE | O | O | O | O | O |
| V$OPEN_CURSOR | X | X | X | O | O |
| V$PLAN_HISTORY | X | X | O | O | O |
| V$PLAN_HISTORY_LATEST | X | X | O | O | O |
| V$PROCESS_MEM_STAT | O | O | O | O | O |
| V$PROCESS_SQL_STAT | O | O | O | O | O |
| V$PROCESS_STAT | O | O | O | O | O |
| V$PROPERTY | O | O | O | O | O |
| V$PROPERTY_ALIAS | X | X | X | O | O |
| V$PSM_RESERVED_WORDS | O | O | O | O | O |
| V$QUEUE | O | O | O | O | O |
| V$RELATION | X | X | X | X | O |
| V$RESERVED_WORDS | O | O | O | O | O |
| V$SEQUENCE | X | O | O | O | O |
| V$SESSION | O | O | O | O | O |
| V$SESSION_AUDIT | O | O | O | O | O |
| V$SESSION_CONNECT_INFO | O | O | O | O | O |
| V$SESSION_EVENT | O | O | O | O | O |
| V$SESSION_MEM_STAT | O | O | O | O | O |
| V$SESSION_MEM_USAGE | X | X | O | O | O |
| V$SESSION_SQL_STAT | O | O | O | O | O |
| V$SESSION_STAT | O | O | O | O | O |
| V$SESSION_WAIT | O | O | O | O | O |
| V$SHARED_MODE | O | O | O | O | O |
| V$SHARED_SERVER | O | O | O | O | O |
| V$SHM_SEGMENT | O | O | O | O | O |
| V$SPROPERTY | O | O | O | O | O |
| V$SQLFN_METADATA | O | O | O | O | O |
| V$SQL_CACHE | O | O | O | O | O |
| V$SQL_COMMAND | O | O | O | O | O |
| V$SQL_HISTORY | O | O | O | O | O |
| V$STATEMENT | O | O | O | O | O |
| V$SYSTEM_EVENT | O | O | O | O | O |
| V$SYSTEM_MEM_STAT | O | O | O | O | O |
| V$SYSTEM_SQL_STAT | O | O | O | O | O |
| V$SYSTEM_STAT | O | O | O | O | O |
| V$TABLES | O | O | O | O | O |
| V$TABLESPACE | O | O | O | O | O |
| V$TABLESPACE_STAT | O | O | O | O | O |
| V$TCL_LOGFILE | X | X | X | X | O |
| V$TRANSACTION | O | O | O | O | O |
| V$UNDO_SEGMENT | X | X | X | X | O |
| V$WAIT_EVENT_CLASS_NAME | O | O | O | O | O |
| V$WAIT_EVENT_NAME | O | O | O | O | O |
| V$XA_TRANSACTION | O | O | O | O | O |

<a id="5a7117460d6f0643"></a>
#### Server Property

Server property에 대한 feature matrix는 다음과 같다.

**Server property의 feature matrix**

<a id="8268ddd7c2045853"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| ADMIN_SESSION_POOL_INIT_SIZE | X | X | X | O | O |
| ADMIN_SESSION_POOL_NEXT_SIZE | X | X | X | O | O |
| AGING_INTERVAL | O | O | O | O | O |
| AGING_PLAN_INTERVAL | O | O | O | O | O |
| ARCHIVE_LOG_THROTTLING | X | X | O | O | O |
| ARCHIVELOG_DIR | X | X | X | X | X |
| ARCHIVELOG_DIR_1 ~ DIR_10 | O | O | O | O | O |
| ARCHIVELOG_FILE | O | O | O | O | O |
| ARCHIVELOG_MODE | O | O | O | O | O |
| BACKUP_DIR_1 ~ DIR_10 | O | O | O | O | O |
| BLOCK_READ_COUNT | O | O | O | O | O |
| BROADCAST_INDEX_REBUILD_PROTOCOL | X | O | O | O | O |
| BROADCAST_REBALANCE_PROTOCOL | X | O | O | O | O |
| BUFFER_CACHE_SIZE | X | O | O | O | O |
| BUFFER_CHECKPOINT_LIST_COUNT | X | O | X | X | X |
| BUFFER_DIRTY_PAGE_LIMIT | X | X | X | O | O |
| BUFFER_FLUSH_THREADS | X | O | X | X | X |
| BUFFER_FLUSHING_INTERVAL | X | O | X | X | X |
| BUFFER_FREE_LIST_COUNT | X | O | O | O | O |
| BUFFER_HASH_BUCKETS | X | O | O | O | O |
| BUFFER_HOT_REGION_CRITERIA | X | O | O | O | O |
| BUFFER_HOT_REGION_PERCENT | X | O | O | O | O |
| BUFFER_LRU_LIST_COUNT | X | O | O | O | O |
| BUFFER_LRU_SCAN_PERCENT | X | X | X | O | O |
| BUFFER_MULTIPAGE_READ_COUNT | X | O | O | O | O |
| BUFFER_PREFETCH_PAGE_COUNT | X | X | O | O | O |
| BULK_IO_PAGE_COUNT | O | O | O | O | O |
| CDISPATCHER_HOT_POLICY_INTERVAL | O | O | O | O | O |
| CDISPATCHER_LOCKABLE_THREADS | X | X | X | O | O |
| CDISPATCHER_LOCKLESS_THREADS | X | O | O | O | O |
| CDISPATCHER_MAX_PACKET_BUFFER_SIZE | X | X | X | O | O |
| CDISPATCHER_SOCKET_BUFFER_SIZE | O | O | O | O | O |
| CDISPATCHER_SYNC_THREADS | O | O | O | O | O |
| CHANGE_TRACKING | X | O | O | O | O |
| CHANGE_TRACKING_EXTENT_SIZE | X | O | O | O | O |
| CHANGE_TRACKING_FILE | X | O | O | O | O |
| CHAR_LENGTH_UNITS | O | O | O | O | O |
| CHARACTER_SET | O | O | O | O | O |
| CHECK_DEDICATE_CONNECTION_INTERVAL | O | O | O | O | O |
| CHECK_DEDICATE_SOCKET | X | X | X | X | X |
| CHECKPOINT_LIST_COUNT_PER_IO_GROUP | X | X | X | O | O |
| CLIENT_MAX_COUNT | O | O | O | O | O |
| CLIENT_NUMA_POLICY | O | O | O | O | O |
| CLOSE_PSM_CHILD_STMTS | O | O | O | O | O |
| CLUSTER_ASYNC_COMMIT | O | O | O | O | O |
| CLUSTER_ASYNC_REPLICATION | O | O | O | X | X |
| CLUSTER_CM_BUFFER_COUNT | O | O | O | X | X |
| CLUSTER_CM_BUFFER_SIZE | O | O | O | O | O |
| CLUSTER_CM_READ_BUFFER_SIZE | O | O | O | O | O |
| CLUSTER_COMMIT_SLAVE_CSERVERS | X | X | X | O | O |
| CLUSTER_COMMIT_STREAM_ISOLATION | O | O | O | O | X |
| CLUSTER_CONNECTION | O | O | O | O | O |
| CLUSTER_CONNECTION_TIMEOUT_SEC | O | O | O | O | O |
| CLUSTER_DATA_SYNC_SERVERS | O | O | O | O | O |
| CLUSTER_DEADLOCK_TIMEOUT | X | O | O | O | X |
| CLUSTER_DISPATCHER_IN_QUEUE_SIZE | O | O | O | O | O |
| CLUSTER_DISPATCHER_NUMA_STREAM_MAP | O | O | O | O | O |
| CLUSTER_DISPATCHER_OUT_QUEUE_SIZE | O | O | O | O | O |
| CLUSTER_FETCH_ORDER | X | X | X | X | O |
| CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE | X | X | X | O | O |
| CLUSTER_HEARTBEAT_INTERVAL | O | O | O | O | O |
| CLUSTER_HEARTBEAT_RETRY_COUNT | O | O | O | O | O |
| CLUSTER_IGNORE_INACTIVE_MEMBER | O | O | O | O | O |
| CLUSTER_KEEPALIVE_IDLE_TIME | X | X | X | O | O |
| CLUSTER_LOCKABLE_CSERVERS | X | X | X | O | O |
| CLUSTER_LOCKLESS_CSERVERS | X | X | X | O | O |
| CLUSTER_MAX_PACKET_SIZE | O | O | O | O | O |
| CLUSTER_MAX_PAYLOAD_SIZE | O | O | O | O | O |
| CLUSTER_PACKET_ALLOCATION_TIMEOUT | O | O | O | O | O |
| CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT | O | O | O | O | O |
| CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT | O | O | O | O | O |
| CLUSTER_SESSION_HASH_BUCKETS | X | O | O | O | O |
| CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY | O | O | O | O | O |
| CLUSTER_SPLIT_BRAIN_RETRY_COUNT | O | O | O | O | O |
| COMMITTER_HOT_POLICY_INTERVAL | O | O | O | O | O |
| CONTROL_FILE_0 ~ FILE_7 | O | O | O | O | O |
| CONTROL_FILE_COUNT | O | O | O | O | O |
| CONTROL_FILE_TEMP_NAME | O | O | O | O | X |
| COORDINATOR_COMMIT_WRITE_MODE | O | O | O | O | O |
| DA_CLIENT_NUMA_MODE | O | O | O | O | O |
| DATA_STORE_MODE | O | O | O | O | O |
| DATABASE_ACCESS_MODE | O | O | O | X | X |
| DATABASE_INSTANCE_NAME | O | O | O | O | O |
| DDL_AUTOCOMMIT | O | O | O | O | O |
| DDL_LOCK_TIMEOUT | O | O | O | O | O |
| DEADLOCK_PRIORITY | X | O | O | O | O |
| DEFAULT_ASC_NULLS_ORDER | X | X | X | X | O |
| DEFAULT_DESC_NULLS_ORDER | X | X | X | X | O |
| DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION | O | O | O | O | O |
| DEFAULT_INDEX_LOGGING | O | X | X | X | X |
| DEFAULT_INDEX_PCTFREE | O | O | O | O | O |
| DEFAULT_INITRANS | O | O | O | O | O |
| DEFAULT_MAXTRANS | O | O | O | O | O |
| DEFAULT_PCTFREE | O | O | O | O | O |
| DEFAULT_PCTUSED | O | O | O | O | O |
| DEFAULT_REMOVAL_BACKUP_FILE | O | O | O | O | O |
| DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST | O | O | O | O | O |
| DEFAULT_SHARDING | O | O | O | O | O |
| DISABLE_DDL | X | X | O | O | O |
| DISABLE_DDL_CDC_GIVEUP | O | O | O | O | O |
| DISABLE_SERIAL_DDL | X | X | O | O | O |
| DISABLE_UPDATE_PK_CDC_GIVEUP | O | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE | O | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL | O | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME | O | O | O | O | O |
| DISPATCHERS | O | O | O | O | O |
| DISPATCHER_CM_BUFFER_SIZE | O | O | O | O | O |
| DISPATCHER_CM_UNIT_SIZE | O | O | O | O | O |
| DISPATCHER_CONNECTIONS | O | O | O | O | O |
| DISPATCHER_HOT_POLICY_INTERVAL | O | O | O | O | O |
| DISPATCHER_LOAD_BALANCING | O | O | O | O | O |
| DISPATCHER_NUMA_STREAM_MAP | O | O | O | O | O |
| DISPATCHER_QUEUE_SIZE | O | O | O | O | O |
| DISPATCHER_REQUEST_MINI_QUEUE_COUNT | O | O | O | O | O |
| DISPATCHER_RESPONSE_MINI_QUEUE_COUNT | O | O | O | O | O |
| EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY | X | X | O | O | O |
| EXTLIB_DIR | X | X | X | X | O |
| FETCH_FAILOVER | O | O | O | O | O |
| FULL_TABLE_SCAN_CACHING_THRESHOLD | X | X | X | O | O |
| GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY | O | O | O | O | O |
| GLOBAL_JOURNAL_BUFFER_SIZE | O | O | O | O | O |
| GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE | O | O | O | O | O |
| GLOBAL_PROPERTY_LOCK_TIMEOUT | O | O | O | O | O |
| GLOBAL_TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O | O |
| GLOBAL_TRANSACTION_ISOLATION_SCOPE | O | O | O | O | O |
| GLOBAL_TRANSACTION_LOG_BLOCK_SIZE | X | X | X | X | O |
| GLOBAL_TRANSACTION_LOG_DIR | O | O | O | O | O |
| GLOBAL_TRANSACTION_LOG_FILE_SIZE | O | O | O | O | O |
| GMASTER_NUMA_NODE | O | O | O | O | O |
| GMON_AUTOSTART | O | O | O | O | O |
| HINT_ERROR | O | O | O | O | O |
| HISTOGRAM_BALANCE_BUCKET_COUNT | X | X | X | X | O |
| HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT | X | X | X | X | O |
| HISTOGRAM_FREQUENCY_BUCKET_COUNT | X | X | X | X | O |
| IDLE_TIMEOUT | O | O | O | O | O |
| IN_DOUBT_DECISION | O | O | O | O | O |
| IN_KEY_RANGE_ARRAY_COUNT | X | O | O | O | O |
| INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE | X | O | O | O | O |
| INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA | X | X | X | O | O |
| INDEX_BUILD_PARALLEL_FACTOR | O | O | O | O | O |
| INDEX_LOGGING_THROTTLING | X | X | O | O | X |
| INDEX_MERGE_RUN_COUNT | O | O | O | O | O |
| INDEX_REBUILD_BLOCK_READ_COUNT | X | O | O | O | O |
| INDEX_SELF_AGING_THRESHOLD | X | X | X | O | O |
| INDEX_SORT_RUN_SIZE | O | O | O | O | O |
| INDEX_TREE_MERGE_PARALLEL_FACTOR | O | O | O | O | O |
| INST_ALLOCATOR_COUNT | O | O | O | O | O |
| INST_HASH_TABLE_BUCKET_MAX_COUNT | X | X | O | O | O |
| INST_TABLE_PAGE_SIZE | O | O | O | O | O |
| INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD | X | X | X | X | O |
| INSTANT_WORK_AREA_SIZE | X | X | X | X | O |
| IPC_CHANNEL_COUNT | X | X | O | O | O |
| JOURNAL_TEMP_DIR | O | O | O | O | O |
| KEEPALIVE_IDLE_TIME | O | O | O | O | O |
| LOCAL_CLUSTER_MEMBER | O | O | O | O | O |
| LOCAL_CLUSTER_MEMBER_HOST | O | O | O | O | O |
| LOCAL_CLUSTER_MEMBER_PORT | O | O | O | O | O |
| LOCAL_JOURNAL_BUFFER_SIZE | O | O | O | O | O |
| LOCATION_FILE | O | O | O | O | O |
| LOCATOR_QUERY_TIMEOUT | O | O | O | O | O |
| LOCK_HASH_TABLE_SIZE | O | O | O | O | O |
| LOCKABLE_DISPATCHER_CM_BUFFER_COUNT | X | X | X | O | O |
| LOCKLESS_DISPATCHER_CM_BUFFER_COUNT | X | X | X | O | O |
| LOG_BLOCK_SIZE | O | O | O | O | O |
| LOG_BUFFER_SIZE | O | O | O | O | O |
| LOG_DIR | O | O | O | O | O |
| LOG_FILE_SIZE | O | O | O | O | O |
| LOG_FLUSHER_HOT_POLICY_INTERVAL | X | X | X | X | O |
| LOG_GROUP_COUNT | O | O | O | O | O |
| LOG_MIRROR_MODE | O | O | O | O | O |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | O | O | O | O | O |
| LOG_MIRROR_TIMEOUT | O | O | O | O | O |
| LOG_SYNC_INTERVAL | O | O | O | O | O |
| LOG_SYNC_INTERVAL_MSEC | O | O | O | O | O |
| MAX_GROUP_COUNT | O | O | O | O | O |
| MAX_GROUPING_SETS_COUNT | X | X | X | X | O |
| MAX_JOURNAL_FILE_SIZE | O | O | O | O | O |
| MAX_NODE_COUNT | O | O | O | O | O |
| MAXIMUM_CONCURRENT_ACTIVITIES | O | O | O | O | O |
| MAXIMUM_FILE_CACHE_SIZE | X | X | O | O | O |
| MAXIMUM_FLANGE_COUNT | O | O | O | X | X |
| MAXIMUM_FLUSH_BUFFER_PAGE_COUNT | X | X | O | O | O |
| MAXIMUM_FLUSH_LOG_BLOCK_COUNT | O | O | O | O | O |
| MAXIMUM_FLUSH_PAGE_COUNT | O | O | O | O | O |
| MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT | X | O | O | O | O |
| MAXIMUM_LOADED_LIBRARY_COUNT | X | X | X | X | O |
| MAXIMUM_NAMED_CURSOR_COUNT | O | O | O | O | O |
| MAXIMUM_PACKAGE_INSTANCE_COUNT | X | X | O | O | O |
| MAXIMUM_SESSION_CM_BUFFER_SIZE | O | O | O | O | O |
| MEASURE_CLUSTER_LATENCY | O | O | O | O | O |
| MEDIA_RECOVERY_LOG_BUFFER_SIZE | X | X | X | X | X |
| MIN_SAMPLE_ROW_COUNT | O | O | O | O | O |
| MINIMUM_UNDO_PAGE_COUNT | O | O | O | O | O |
| NET_BUFFER_SIZE | O | O | O | O | O |
| NLS_DATE_FORMAT | O | O | O | O | O |
| NLS_TIME_FORMAT | O | O | O | O | O |
| NLS_TIME_WITH_TIME_ZONE_FORMAT | O | O | O | O | O |
| NLS_TIMESTAMP_FORMAT | O | O | O | O | O |
| NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT | O | O | O | O | O |
| NUMA | O | O | O | O | O |
| NUMA_MAP | O | O | O | O | O |
| OFFLINE_MEMBER_AFTER_FAILOVER | O | O | O | O | O |
| ONLINE_DDL_BLOCK_READ_COUNT | X | X | X | X | O |
| ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD | X | X | X | X | O |
| ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT | X | X | X | X | O |
| ONLINE_DDL_SCAN_PARTITION | X | X | X | X | O |
| ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD | X | O | O | O | O |
| OS_GROUP_ACCESS | O | O | O | O | O |
| PACKET_COMPRESSION_THRESHOLD | X | O | O | O | O |
| PAGE_CHECKSUM_TYPE | O | O | O | O | O |
| PARALLEL_IO_FACTOR | O | O | O | O | O |
| PARALLEL_IO_GROUP_1 ~ GROUP_16 | O | O | O | X | X |
| PARALLEL_LOAD_FACTOR | O | O | O | O | O |
| PENDING_LOG_BUFFER_COUNT | O | O | O | O | O |
| PLAN_CACHE | O | O | O | O | O |
| PLAN_CACHE_SIZE | O | O | O | O | O |
| PLAN_HISTORY | X | X | O | O | O |
| PLAN_HISTORY_SIZE | X | X | O | O | O |
| PRIVATE_STATIC_AREA_INIT_SIZE | X | O | O | O | O |
| PRIVATE_STATIC_AREA_NEXT_SIZE | X | O | O | O | O |
| PRIVATE_STATIC_AREA_SHRINK_THRESHOLD | X | O | O | O | O |
| PRIVATE_STATIC_AREA_SIZE | O | O | O | O | O |
| PROCESS_MAX_COUNT | O | O | O | O | O |
| QUERY_TIMEOUT | O | O | O | O | O |
| READABLE_ARCHIVELOG_DIR_COUNT | O | O | O | O | O |
| READABLE_BACKUP_DIR_COUNT | O | O | O | O | O |
| RECOMPILE_CHECK_MINIMUM_PAGE_COUNT | X | X | X | X | X |
| RECOMPILE_PAGE_PERCENT | X | X | X | X | X |
| RECOVERY_LOG_BUFFER_SIZE | O | O | O | O | O |
| RECOVERY_SLAVES | X | X | X | X | O |
| RECYCLEBIN | X | O | O | O | O |
| REDO_LOG_COMPRESSION_THRESHOLD | O | O | O | O | O |
| REDO_LOGGING_THROTTLING | X | X | X | X | O |
| REFINE_RELATION | O | O | O | O | O |
| RESTORE_BUFFER_SIZE | X | O | O | O | O |
| SESSION_FATAL_BEHAVIOR | O | O | O | O | O |
| SESSION_MEMORY_INIT_SIZE | O | O | O | O | O |
| SESSION_MEMORY_SHRINK_THRESHOLD | O | O | O | O | O |
| SESSION_POOL_INIT_SIZE | X | X | X | O | O |
| SESSION_POOL_NEXT_SIZE | X | X | X | O | O |
| SHARED_MEMORY_ADDRESS | O | O | O | O | O |
| SHARED_MEMORY_STATIC_KEY | O | O | O | O | O |
| SHARED_MEMORY_STATIC_NAME | O | O | O | O | O |
| SHARED_MEMORY_STATIC_SIZE | O | O | O | O | O |
| SHARED_REQUEST_QUEUE_COUNT | O | O | O | O | O |
| SHARED_SERVERS | O | O | O | O | O |
| SHARED_SESSION | O | O | O | O | O |
| SHARED_SESSION_MEMORY_INIT_SIZE | X | X | X | X | O |
| SNAPSHOT_STATEMENT_TIMEOUT | O | O | O | O | O |
| SQL_HISTORY_SIZE | O | O | O | O | O |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | O | O | O | O | O |
| SYNC_DISPATCHER_CM_BUFFER_COUNT | X | X | X | O | O |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | X | O | O | O | O |
| SYSTEM_FILE_IO | O | O | O | O | O |
| SYSTEM_MEMORY_AUX_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_TABLESPACE_DIR | O | O | O | O | O |
| SYSTEM_UDS_DIR | O | O | O | O | O |
| TCP_CLIENT_NUMA_MODE | O | O | O | O | O |
| TCP_NODELAY | O | O | O | O | O |
| TEMP_SEGMENT_CACHE_SIZE | O | O | O | O | O |
| TEMP_UNDO_ENABLED | O | O | O | O | O |
| TEMP_UNDO_SHRINK_THRESHOLD | O | O | O | O | O |
| TIMED_STATISTICS | O | O | O | O | O |
| TIMER_INTERVAL | X | X | O | O | O |
| TIMEZONE | O | O | O | O | O |
| TRACE_ALTER_SYSTEM | O | O | O | O | O |
| TRACE_DDL | O | O | O | O | O |
| TRACE_LOG_ID | O | O | O | O | O |
| TRACE_LOG_MSGBUF_SIZE | O | O | O | O | O |
| TRACE_LOG_TIME_DETAIL | O | O | O | O | O |
| TRACE_LOGGER | O | O | O | O | O |
| TRACE_LOGGER_REMOTE_HOST | O | O | O | O | O |
| TRACE_LOGGER_REMOTE_PORT | O | O | O | O | O |
| TRACE_LOGIN | O | O | O | O | O |
| TRACE_LONG_RUN_CURSOR | O | O | O | O | O |
| TRACE_LONG_RUN_SQL | O | O | O | O | O |
| TRACE_LONG_RUN_TIMER | X | O | O | O | O |
| TRACE_SYSTEM_DIR | X | X | X | O | O |
| TRACE_XA | O | O | O | O | O |
| TRANSACTION_ALLOCATION_TIMEOUT | O | O | O | O | O |
| TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O | O |
| TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT | O | O | O | O | O |
| TRANSACTION_TABLE_SIZE | O | O | O | O | O |
| TRANSACTION_TIMEOUT | O | O | O | O | O |
| UNDO_RELATION_ALLOCATION_TIMEOUT | O | O | O | O | O |
| UNDO_RELATION_COUNT | O | O | O | O | O |
| UNDO_SHRINK_THRESHOLD | O | O | O | O | O |
| USE_LARGE_PAGES | X | O | O | O | O |
| USER_DATA_TABLESPACE_MEDIA_TYPE | X | O | O | O | O |
| USER_DATA_TABLESPACE_SIZE | X | O | O | O | O |
| USER_DISK_DATA_TABLESPACE_NEXTSIZE | X | O | O | O | O |
| USER_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| XA_TRANSACTION_IDLE_TIMEOUT | X | O | O | O | O |

<a id="f6827c242fa41236"></a>
#### Property Alias

Property alias에 대한 feature matrix는 다음과 같다.

**Property alias의 feature matrix**

<a id="1015ebd10f153b71"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| CDISPATCHER_THREADS | O | O | O | O | O |
| CLUSTER_COMMIT_SLAVES | O | O | O | O | O |
| CLUSTER_SERVER_RESPONSE_QUEUE_SIZE | O | O | O | O | O |
| CSERVER | O | O | O | O | O |
| INCREMENTAL_CHECKPOINT_CRITERIA | X | X | X | O | O |
| INDEX_LOGGING_THROTTLING | X | X | O | O | O |
| INST_TABLE_BLOCK_SIZE | O | O | O | O | O |
| LOCKLESS_CSERVERS | X | O | O | O | O |
| MAXIMUM_JOURNAL_REPLAY_COUNT | X | X | X | X | O |
| MEMORY_MERGE_RUN_COUNT | O | O | O | O | O |
| MEMORY_SORT_RUN_SIZE | O | O | O | O | O |
| ONLINE_JOURNAL_REPLAY_THRESHOLD | X | X | X | X | O |
| REBALANCE_BLOCK_READ_COUNT | X | X | X | X | O |
| REBALANCE_SHARD_DIVISOR | X | X | X | X | O |
| SYSTEM_LOGGER_DIR | O | O | O | O | O |

<a id="734fbfbc51884950"></a>
### SQL

<a id="73a95e22230fc880"></a>
#### SQL Element

<a id="1f6652c86d6af14c"></a>
##### Data Type

데이터 타입에 대한 feature matrix는 다음과 같다.

<a id="ca3e3660f9be960d"></a>
<table class="table column_count_7"><caption>Data type의 feature matrix</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>문자 스트링 타입</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>이진 스트링 타입</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>십진 숫자 타입</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>이진 숫자 타입</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN 타입</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>날짜/시간 타입</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL 타입</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROWID 타입</div></td><td><div>ROWID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="2be439ef4016b8db"></a>
##### Function

함수 및 연산자에 대한 feature matrix는 다음과 같다.

**Function의 feature matrix**

<a id="004a5a23150f00f7"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| expr1 * expr2 | O | O | O | O | O |
| expr1 + expr2 | O | O | O | O | O |
| datetime + interval | O | O | O | O | O |
| ＋ expr | O | O | O | O | O |
| expr1 - expr2 | O | O | O | O | O |
| datetime - interval | O | O | O | O | O |
| - expr | O | O | O | O | O |
| expr1 / expr2 | O | O | O | O | O |
| str1 \|\| str2 | O | O | O | O | O |
| expr &lt;comp&gt; expr | O | O | O | O | O |
| expr &lt;comp&gt; ( subquery ) | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; expr | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( subquery ) | O | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( expr, ... ) | O | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( subquery ) | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( expr, ... ) | O | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | O | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | O | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | O | O | O | O | O |
| ABS( num ) | O | O | O | O | O |
| ACOS( num ) | O | O | O | O | O |
| ADDDATE( date, interval ) | O | O | O | O | O |
| ADDDATE( expr, days ) | O | O | O | O | O |
| ADDTIME( expr1, expr2 ) | O | O | O | O | O |
| ADD_MONTHS( date, number ) | O | O | O | O | O |
| AND | O | O | O | O | O |
| APPROX_COUNT_DISTINCT( expr [, expr ...] ) | X | X | X | X | O |
| APPROX_COUNT_DISTINCT( expr [, expr ...] ) FILTER | X | X | X | X | O |
| ASCII( char ) | O | O | O | O | O |
| ASIN( num ) | O | O | O | O | O |
| ATAN( num ) | O | O | O | O | O |
| ATAN2( num1, num2 ) | O | O | O | O | O |
| AVG( num ) | O | O | O | O | O |
| AVG( num ) FILTER | X | X | X | X | O |
| AVG( expr ) OVER | X | X | X | O | O |
| expr1 [NOT] BETWEEN [ASYMMETRIC\|SYMMETRIC] expr2 AND expr3 | O | O | O | O | O |
| BITAND( num1, num2 ) | O | O | O | O | O |
| BITNOT( num ) | O | O | O | O | O |
| BITOR( num1, num2 ) | O | O | O | O | O |
| BITXOR( num1, num2 ) | O | O | O | O | O |
| BIT_LENGTH( str ) | O | O | O | O | O |
| BYTE_LENGTH( str ) | O | O | O | O | O |
| CASE .. WHEN .. THEN .. ELSE .. END | O | O | O | O | O |
| CASE2( condition, result, ... ) | O | O | O | O | O |
| CAST( expr AS datatype ) | O | O | O | O | O |
| CBRT( num ) | O | O | O | O | O |
| CEIL( num ) | O | O | O | O | O |
| CEILING( num ) | O | O | O | O | O |
| CHAR_LENGTH( str ) | O | O | O | O | O |
| CHARACTER_LENGTH( str ) | O | O | O | O | O |
| CHR( num ) | O | O | O | O | O |
| CLOCK_DATE() | O | O | O | O | O |
| CLOCK_LOCALTIME() | O | O | O | O | O |
| CLOCK_LOCALTIMESTAMP() | O | O | O | O | O |
| CLOCK_TIME() | O | O | O | O | O |
| CLOCK_TIMESTAMP() | O | O | O | O | O |
| COALESCE( expr1, ..., exprN ) | O | O | O | O | O |
| CONCAT( str1, str2 ) | O | O | O | O | O |
| CONCATENATE( str1, str2 ) | O | O | O | O | O |
| CONNECT_BY_ISCYCLE | X | X | O | O | O |
| CONNECT_BY_ISLEAF | X | X | O | O | O |
| CONNECT_BY_ROOT expr | X | X | O | O | O |
| CORR( expr1, expr2 ) OVER | X | X | X | O | O |
| COS( num ) | O | O | O | O | O |
| COT( num ) | O | O | O | O | O |
| COUNT( expr ) | O | O | O | O | O |
| COUNT( expr ) FILTER | X | X | X | X | O |
| COUNT( expr ) OVER | X | X | X | O | O |
| COUNT(*) | O | O | O | O | O |
| COUNT(*) FILTER | X | X | X | X | O |
| COUNT(*) OVER | X | X | X | O | O |
| COVAR_POP( expr1, expr2 ) OVER | X | X | X | O | O |
| COVAR_SAMP( expr1, expr2 ) OVER | X | X | X | O | O |
| CUME_DIST() OVER | X | X | X | O | O |
| CURRENT_CATALOG | O | O | O | O | O |
| CURRENT_DATE | O | O | O | O | O |
| CURRENT_ROLE | X | X | X | X | O |
| CURRENT_SCHEMA | O | O | O | O | O |
| CURRENT_TIME | O | O | O | O | O |
| CURRENT_TIMESTAMP | O | O | O | O | O |
| CURRENT_USER | O | O | O | O | O |
| seq.CURRVAL | O | O | O | O | O |
| CURRVAL( seq ) | O | O | O | O | O |
| DATEADD( datepart, number, date ) | O | O | O | O | O |
| DATEDIFF( datepart, startdate, enddate ) | O | O | O | O | O |
| DATE_ADD( date, interval ) | O | O | O | O | O |
| DATE_PART( field, datetime ) | O | O | O | O | O |
| DECODE( expr, comparison, result, ... ) | O | O | O | O | O |
| DEGREES( radians ) | O | O | O | O | O |
| DENSE_RANK() OVER | X | X | X | O | O |
| DIGEST ( data, type ) | O | O | O | O | O |
| expr IS [NOT] DISTINCT FROM expr | X | X | X | O | O |
| ( expr, ... ) IS [NOT] DISTINCT FROM ( expr, ... ) | X | X | X | O | O |
| DUMP( expr ) | O | O | O | O | O |
| EXISTS( subquery ) | O | O | O | O | O |
| EXP( num ) | O | O | O | O | O |
| EXTRACT( field FROM datetime ) | O | O | O | O | O |
| FACTORIAL( num ) | O | O | O | O | O |
| FIRST : aggr_func KEEP ( DENSE_RANK FIRST ORDER BY expr, ... ) OVER | X | X | X | O | O |
| FIRST_VALUE( expr ) OVER | X | X | X | O | O |
| FLOOR( num ) | O | O | O | O | O |
| FROM_BASE64( str ) | O | O | O | O | O |
| FROM_TZ( timestamp, timezone ) | X | X | O | O | O |
| GREATEST( expr, ... ) | O | O | O | O | O |
| GSI_PHYSICAL_STATS( table_name, num ) | X | X | X | X | O |
| HASH32( expr [, expr] ... ) | X | X | O | O | O |
| HEX( str ) | O | O | O | O | O |
| expr1 [NOT] IN ( expr, ... ) | O | O | O | O | O |
| expr1 [NOT] IN ( subquery ) | O | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt; ) | O | O | O | O | O |
| subquery [NOT] IN ( subquery ) | O | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( subquery ) | O | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O | O |
| INDEX_PHYSICAL_STATS( index_name, num ) | X | X | X | X | O |
| INITCAP( str ) | O | O | O | O | O |
| INSTR( str, substr, ... ) | O | O | O | O | O |
| IS NOT NULL | O | O | O | O | O |
| IS NULL | O | O | O | O | O |
| JSON_ARRAY( expr, ... ) | X | X | X | O | O |
| JSON_ARRAYAGG( expr ) | X | X | X | O | O |
| JSON_ARRAYAGG( expr ) OVER | X | X | X | O | O |
| JSON_OBJECT( name VALUE expr, ... ) | X | X | X | O | O |
| JSON_OBJECTAGG( name VALUE expr ) | X | X | X | O | O |
| JSON_OBJECTAGG( name VALUE expr ) OVER | X | X | X | O | O |
| LAG( expr [, offset [, default]] ) OVER | X | X | X | O | O |
| LAST : aggr_func KEEP ( DENSE_RANK LAST ORDER BY expr, ... ) OVER | X | X | X | O | O |
| LAST_DAY( date ) | O | O | O | O | O |
| LAST_IDENTITY_VALUE() | O | O | O | O | O |
| LAST_VALUE( expr ) OVER | X | X | X | O | O |
| LEAD( expr [, offset [, default]] ) OVER | X | X | X | O | O |
| LEAST( expr, ... ) | O | O | O | O | O |
| LENGTH( str ) | O | O | O | O | O |
| LENGTHB( str ) | O | O | O | O | O |
| LEVEL | X | X | O | O | O |
| string [NOT] LIKE pattern ESCAPE escape_char | O | O | O | O | O |
| LISTAGG( str [, delimiter] ) OVER | X | X | X | O | O |
| LN( num ) | O | O | O | O | O |
| LNNVL( expr ) | X | O | O | O | O |
| LOCAL_GROUP_ID() | O | O | O | O | O |
| LOCAL_GROUP_NAME() | O | O | O | O | O |
| LOCAL_MEMBER_ID() | O | O | O | O | O |
| LOCAL_MEMBER_NAME() | O | O | O | O | O |
| LOCAL_MEMBER_POSITION() | X | X | X | X | O |
| LOCALTIME | O | O | O | O | O |
| LOCALTIMESTAMP | O | O | O | O | O |
| LOG( num2 ) | O | O | O | O | O |
| LOG( num1, num2 ) | O | O | O | O | O |
| LOGON_USER() | O | O | O | O | O |
| LOWER( str ) | O | O | O | O | O |
| LPAD( str, length, fill ) | O | O | O | O | O |
| LTRIM( str, [ str ] ) | O | O | O | O | O |
| MAX( expr ) | O | O | O | O | O |
| MAX( expr ) FILTER | X | X | X | X | O |
| MAX( expr ) OVER | X | X | X | O | O |
| MEDIAN( expr ) OVER | X | X | X | O | O |
| MIN( expr ) | O | O | O | O | O |
| MIN( expr ) FILTER | X | X | X | X | O |
| MIN( expr ) OVER | X | X | X | O | O |
| MOD( num1, num2 ) | O | O | O | O | O |
| MONTHS_BETWEEN( date1, date2 ) | O | O | O | O | O |
| NEXT_DAY( date, day ) | O | O | O | O | O |
| seq.NEXTVAL | O | O | O | O | O |
| NEXTVAL( seq ) | O | O | O | O | O |
| NEXT VALUE FOR seq | O | O | O | O | O |
| NOT | O | O | O | O | O |
| NTH_VALUE( expr, n ) OVER | X | X | X | O | O |
| NTILE( expr ) OVER | X | X | X | O | O |
| NULLIF( expr1, expr2 ) | O | O | O | O | O |
| NUMTODSINTERVAL( num, interval_indicator ) | X | O | O | O | O |
| NUMTOYMINTERVAL( num, interval_indicator ) | X | O | O | O | O |
| NVL( expr1, expr2 ) | O | O | O | O | O |
| NVL2( expr1, expr2, expr3 ) | O | O | O | O | O |
| OCTET_LENGTH( str ) | O | O | O | O | O |
| OVERLAY( str1 PLACING str2 FROM start FOR length ) | O | O | O | O | O |
| OR | O | O | O | O | O |
| PERCENT_RANK() OVER | X | X | X | O | O |
| PERCENTILE_CONT( expr ) OVER | X | X | X | O | O |
| PERCENTILE_DISC( expr ) OVER | X | X | X | O | O |
| PHYSICAL_LENGTH( expr ) | X | O | O | O | O |
| PI() | O | O | O | O | O |
| POSITION( str1 IN str2 ) | O | O | O | O | O |
| POWER( num1, num2 ) | O | O | O | O | O |
| PRIOR expr | X | X | O | O | O |
| RADIANS( degrees ) | O | O | O | O | O |
| RANDOM( min, max ) | O | O | O | O | O |
| RANK() OVER | X | X | X | O | O |
| RATIO_TO_REPORT( expr ) OVER | X | X | X | O | O |
| REGEXP_COUNT | X | X | X | X | O |
| REGEXP_INSTR | X | X | X | X | O |
| REGEXP_LIKE | X | X | X | X | O |
| REGEXP_REPLACE | X | X | X | X | O |
| REGEXP_SUBSTR | X | X | X | X | O |
| REGR_AVGX( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_AVGY( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_COUNT( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_INTERCEPT( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_R2( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_SLOPE( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_SXX( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_SXY( expr1, expr2 ) OVER | X | X | X | O | O |
| REGR_SYY( expr1, expr2 ) OVER | X | X | X | O | O |
| REPEAT( str, num ) | O | O | O | O | O |
| REPLACE( str, from, to ) | O | O | O | O | O |
| REVERSE( str ) | O | O | O | O | O |
| ROUND( num ) | O | O | O | O | O |
| ROUND( date, fmt ) | O | O | O | O | O |
| ROW_NUMBER() OVER | X | X | X | O | O |
| ROWID_GRID_BLOCK_ID( rowid ) | O | O | O | O | O |
| ROWID_GRID_BLOCK_SEQ( rowid ) | O | O | O | O | O |
| ROWID_MEMBER_ID( rowid ) | O | O | O | O | O |
| ROWID_OBJECT_ID( rowid ) | O | O | O | O | O |
| ROWID_PAGE_ID( rowid ) | O | O | O | O | O |
| ROWID_ROW_NUMBER( rowid ) | O | O | O | O | O |
| ROWID_SHARD_ID( rowid ) | O | O | O | O | O |
| ROWID_TABLESPACE_ID( rowid ) | O | O | O | O | O |
| ROWNUM | O | O | O | O | O |
| RPAD( str, length, fill ) | O | O | O | O | O |
| RTRIM( str, [ str ] ) | O | O | O | O | O |
| SESSION_ID() | O | O | O | O | O |
| SESSION_SERIAL() | O | O | O | O | O |
| SESSION_USER | O | O | O | O | O |
| SESSIONTIMEZONE() | X | X | X | O | O |
| SHARD_GROUP_ID( table, expr ) | O | O | O | O | O |
| SHARD_GROUP_NAME( table_name, shard_key_value [, ...] ) | O | O | O | O | O |
| SHARD_ID( table, expr ) | O | O | O | O | O |
| SHARD_NAME( table_name, shard_key_value [, ...] ) | O | O | O | O | O |
| SHIFT_LEFT( num, cnt ) | O | O | O | O | O |
| SHIFT_RIGHT( num, cnt ) | O | O | O | O | O |
| SIGN( num ) | O | O | O | O | O |
| SIN( num ) | O | O | O | O | O |
| SPLIT_PART( str, delimiter, field ) | O | O | O | O | O |
| SQRT( num ) | O | O | O | O | O |
| STATEMENT_DATE() | O | O | O | O | O |
| STATEMENT_LOCALTIME() | O | O | O | O | O |
| STATEMENT_LOCALTIMESTAMP() | O | O | O | O | O |
| STATEMENT_TIME() | O | O | O | O | O |
| STATEMENT_TIMESTAMP() | O | O | O | O | O |
| STATEMENT_VIEW_SCN() | O | O | O | O | O |
| STATEMENT_VIEW_SCN_DCN() | O | O | O | O | O |
| STATEMENT_VIEW_SCN_GCN() | O | O | O | O | O |
| STATEMENT_VIEW_SCN_LCN() | O | O | O | O | O |
| STDDEV( expr ) | O | O | O | O | O |
| STDDEV( expr ) FILTER | X | X | X | X | O |
| STDDEV( expr ) OVER | X | X | X | O | O |
| STDDEV_POP( expr ) | O | O | O | O | O |
| STDDEV_POP( expr ) FILTER | X | X | X | X | O |
| STDDEV_POP( expr ) OVER | X | X | X | O | O |
| STDDEV_SAMP( expr ) | O | O | O | O | O |
| STDDEV_SAMP( expr ) FILTER | X | X | X | X | O |
| STDDEV_SAMP( expr ) OVER | X | X | X | O | O |
| STRING_AGG( str [, delimiter] ) OVER | X | X | X | O | O |
| SUBSTR( str FROM start FOR length ) | O | O | O | O | O |
| SUBSTR( str, start, length ) | O | O | O | O | O |
| SUBSTRB( str, start, length ) | O | O | O | O | O |
| SUBSTRING( str FROM start FOR length ) | O | O | O | O | O |
| SUBSTRING( str, start, length ) | O | O | O | O | O |
| SUM( expr ) | O | O | O | O | O |
| SUM( expr ) FILTER | X | X | X | X | O |
| SUM( expr ) OVER | X | X | X | O | O |
| SYSDATE | O | O | O | O | O |
| SYS_CONNECT_BY_PATH( expr, 'string' ) | X | X | O | O | O |
| SYS_EXTRACT_UTC( datetime_with_timezone ) | O | O | O | O | O |
| SYSTIME | O | O | O | O | O |
| SYSTIMESTAMP | O | O | O | O | O |
| TABLE_PHYSICAL_STATS( table_name, num ) | X | X | X | X | O |
| TAN( num ) | O | O | O | O | O |
| TO_CHAR( datetime, fmt ) | O | O | O | O | O |
| TO_CHAR( number, fmt ) | O | O | O | O | O |
| TO_BASE64( str ) | O | O | O | O | O |
| TO_DATE( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_BIGINT( str, fmt ) | X | O | O | O | O |
| TO_NATIVE_DOUBLE( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_INTEGER( str, fmt ) | X | O | O | O | O |
| TO_NATIVE_REAL( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_SMALLINT( str, fmt ) | X | O | O | O | O |
| TO_NUMBER( num, fmt ) | O | O | O | O | O |
| TO_TIME( str, fmt ) | O | O | O | O | O |
| TO_TIME_TZ( str, fmt ) | O | O | O | O | O |
| TO_TIME_WITH_TIME_ZONE( str, fmt ) | O | O | O | O | O |
| TO_TIMESTAMP( str, fmt ) | O | O | O | O | O |
| TO_TIMESTAMP_TZ( str, fmt ) | O | O | O | O | O |
| TO_TIMESTAMP_WITH_TIME_ZONE( str, fmt ) | O | O | O | O | O |
| TRANSACTION_DATE() | O | O | O | O | O |
| TRANSACTION_LOCALTIME() | O | O | O | O | O |
| TRANSACTION_LOCALTIMESTAMP() | O | O | O | O | O |
| TRANSACTION_TIME() | O | O | O | O | O |
| TRANSACTION_TIMESTAMP() | O | O | O | O | O |
| TRANSLATE( str, from, to ) | O | O | O | O | O |
| TRIM( LEADING\|TRAILING\|BOTH trim_char FROM source ) | O | O | O | O | O |
| TRUNC( num, scale ) | O | O | O | O | O |
| TRUNC( date, fmt ) | O | O | O | O | O |
| UPPER( str ) | O | O | O | O | O |
| UNHEX( str ) | O | O | O | O | O |
| UNHEX_TO_CHARSTR( str ) | O | O | O | O | O |
| USER_ID() | O | O | O | O | O |
| UUID() | O | O | O | O | O |
| VAR_POP( expr ) | O | O | O | O | O |
| VAR_POP( expr ) FILTER | X | X | X | X | O |
| VAR_POP( expr ) OVER | X | X | X | O | O |
| VAR_SAMP( expr ) | O | O | O | O | O |
| VAR_SAMP( expr ) FILTER | X | X | X | X | O |
| VAR_SAMP( expr ) OVER | X | X | X | O | O |
| VARIANCE( expr ) | O | O | O | O | O |
| VARIANCE( expr ) FILTER | X | X | X | X | O |
| VARIANCE( expr ) OVER | X | X | X | O | O |
| VERSION() | O | O | O | O | O |
| WIDTH_BUCKET( num, min, max, cnt ) | O | O | O | O | O |

<a id="9088e24186b6b637"></a>
#### Object DDL

<a id="81264d1fb248759d"></a>
##### SQL Object DDL

SQL 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="0123ee12190a0ecd"></a>
<table class="table column_count_7"><caption>SQL 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>객체</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="13"><div>Database 
객체</div></td><td class="to_middle"><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME CHANGE TRACKING FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE REGISTER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESTORE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE SYSTEM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>COMMENT ON object IS ..</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
객체</div></td><td class="to_middle"><div>CREATE PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
객체</div></td><td class="to_middle"><div>CREATE AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>NOAUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Authorization
객체</div></td><td class="to_middle"><div>CREATE ROLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP ROLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GRANT privileges TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GRANT role TO</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>REVOKE privileges FROM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>REVOKE role FROM</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 객체</div></td><td class="to_middle"><div>CREATE SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
객체</div></td><td class="to_middle"><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="26"><div>Table 
객체</div></td><td class="to_middle"><div>CREATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TRUNCATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. REORGANIZE</div></td><td class="to_center to_middle"><div>X
</div></td><td class="to_center to_middle"><div>X
</div></td><td class="to_center to_middle"><div>X
</div></td><td class="to_center to_middle"><div>X
</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SET TRIGGER ORDER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>FLASHBACK TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PURGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
객체</div></td><td class="to_middle"><div>CREATE VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>Index 
객체</div></td><td class="to_middle"><div>CREATE INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. AGING</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. RENAME</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. ENABLE/DISABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
객체</div></td><td class="to_middle"><div>CREATE SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
객체</div></td><td class="to_middle"><div>CREATE SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
객체</div></td><td class="to_middle"><div>CREATE PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
객체</div></td><td class="to_middle"><div>CREATE FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package
객체</div></td><td class="to_middle"><div>CREATE PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PACKAGE BODY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Library 
객체</div></td><td class="to_middle"><div>CREATE LIBRARY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP LIBRARY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Trigger
객체</div></td><td class="to_middle"><div>CREATE TRIGGER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TRIGGER name COMPILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TRIGGER name ENABLE/DISABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TRIGGER name RENAME TO</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TRIGGER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="5a401af0f26817f4"></a>
##### Cluster Object DDL

Cluster 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="3ba6c30a6e2ad94a"></a>
<table class="table column_count_7"><caption>Cluster 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>객체</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="6"><div>Cluster system 
객체</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP UNUSABLE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
객체</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Cluster table과 shard
객체</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name DROP UNUSABLE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name OFFLINE INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Global 
secondary index
객체</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX AGING</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="10fb1bb8d8c6652a"></a>
#### SQL Language

<a id="f9089ebbd34903d1"></a>
##### DML

데이터를 조작하는 DML 구문의 feature matrix는 다음과 같다.

**DML의 feature matrix**

<a id="33de1906670f113d"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| INSERT INTO .. | O | O | O | O | O |
| INSERT INTO .. RETURNING query | O | O | O | O | O |
| INSERT INTO .. RETURNING .. INTO .. | O | O | O | O | O |
| INSERT INTO .. UPDATE | X | X | O | O | O |
| INSERT INTO .. UPDATE .. RETURNING .. | X | X | O | O | O |
| INSERT INTO .. UPDATE .. RETURNING .. INTO .. | X | X | O | O | O |
| DELETE FROM .. | O | O | O | O | O |
| DELETE FROM .. RETURNING query | O | O | O | O | O |
| DELETE FROM .. RETURNING .. INTO .. | O | O | O | O | O |
| DELETE FROM .. WHERE CURRENT OF cursor | O | O | O | O | O |
| UPDATE .. | O | O | O | O | O |
| UPDATE .. RETURNING query | O | O | O | O | O |
| UPDATE .. RETURNING .. INTO .. | O | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O | O |
| MERGE .. | X | X | X | X | O |
| CALL proc_name | O | O | O | O | O |

<a id="626dd884bc3902b6"></a>
##### Query

데이터를 조회하는 SELECT 구문의 feature matrix는 다음과 같다.

**SELECT의 feature matrix**

<a id="d5cf0ced9ed15aeb"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| &lt;query expression&gt; | O | O | O | O | O |
| &lt;query specification&gt; | O | O | O | O | O |
| &lt;select list&gt; | O | O | O | O | O |
| &lt;from clause&gt; | O | O | O | O | O |
| &lt;joined table&gt; | O | O | O | O | O |
| &lt;pivot clause&gt; | X | X | X | X | O |
| &lt;unpivot clause&gt; | X | X | X | X | O |
| &lt;sample clause&gt; | X | X | X | X | O |
| &lt;where clause&gt; | O | O | O | O | O |
| &lt;group by clause&gt; | O | O | O | O | O |
| &lt;rollup list&gt; | X | X | X | X | O |
| &lt;cube list&gt; | X | X | X | X | O |
| &lt;grouping sets specification&gt; | X | X | X | X | O |
| &lt;window clause&gt; | X | X | X | O | O |
| &lt;window partition clause&gt; | X | X | X | O | O |
| &lt;window order clause&gt; | X | X | X | O | O |
| &lt;window frame clause&gt; | X | X | X | O | O |
| &lt;window frame exclusion&gt; | X | X | X | O | O |
| &lt;order by clause&gt; | O | O | O | O | O |
| &lt;offset limit clause&gt; | O | O | O | O | O |
| &lt;set operator&gt; | O | O | O | O | O |
| &lt;subquery&gt; | O | O | O | O | O |
| &lt;hint clause&gt; | O | O | O | O | O |
| &lt;with clause&gt; | X | X | O | O | O |
| &lt;search clause&gt; | X | X | O | O | O |
| &lt;cycle clause&gt; | X | X | O | O | O |
| &lt;start with clause&gt; | X | X | O | O | O |
| &lt;connect by clause&gt; | X | X | O | O | O |
| &lt;order siblings by clause&gt; | X | X | O | O | O |

<a id="80fb04cec4453d84"></a>
##### Control Language

제어 구문의 feature matrix는 다음과 같다.

<a id="b80c80e28a15b83f"></a>
<table class="table column_count_7"><caption>제어 구문의 feature matrix</caption><thead><tr><th class="to_center"><div>구분</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Session</div></td><td><div>SET ROLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CANCEL SESSION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM FLUSH LOGS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="993bdcad3fd162ca"></a>
#### PSM Language

Persistent Stored Module (PSM) language element의 feature matrix는 다음과 같다.

**Persistent Stored Module (PSM) language element의 feature matrix**

<a id="798f5ed53932ea79"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| Assignment Statement | O | O | O | O | O |
| Basic LOOP Statement | O | O | O | O | O |
| Block (BEGIN .. END) | O | O | O | O | O |
| Call Specification | X | X | X | X | O |
| CASE Statement | O | O | O | O | O |
| CLOSE Statement | O | O | O | O | O |
| Collection Method Invocation | O | O | O | O | O |
| Collection Variable Declaration | O | O | O | O | O |
| CONTINUE Statement | O | O | O | O | O |
| Cursor FOR LOOP Statement | O | O | O | O | O |
| Cursor Variable Declaration | O | O | O | O | O |
| DELETE Statement Extension | O | O | O | O | O |
| EXCEPTION_INIT Pragma | O | O | O | O | O |
| Exception Declaration | O | O | O | O | O |
| Exception Handler | O | O | O | O | O |
| EXECUTE IMMEDIATE Statement | O | O | O | O | O |
| EXIT Statement | O | O | O | O | O |
| Explicit Cursor Declaration and Definition | O | O | O | O | O |
| FETCH Statement | O | O | O | O | O |
| FOR LOOP Statement | O | O | O | O | O |
| GOTO Statement | O | O | O | O | O |
| IF Statement | O | O | O | O | O |
| Implicit Cursor Attribute | O | O | O | O | O |
| INSERT Statement Extension | O | O | O | O | O |
| Named Cursor Attribute | O | O | O | O | O |
| NULL Statement | O | O | O | O | O |
| OPEN Statement | O | O | O | O | O |
| OPEN FOR Statement | O | O | O | O | O |
| Procedure Call | O | O | O | O | O |
| Procedure Declaration and Definition | O | O | O | O | O |
| RAISE Statement | O | O | O | O | O |
| Record Variable Declaration | O | O | O | O | O |
| RETURN Statement | O | O | O | O | O |
| RETURN TABLE Statement | X | X | X | O | O |
| RETURNING INTO clause | O | O | O | O | O |
| %ROWTYPE Attribute | O | O | O | O | O |
| Scalar Variable Declaration | O | O | O | O | O |
| SELECT INTO Statement | O | O | O | O | O |
| SQLCODE Function | O | O | O | O | O |
| SQLERRM Function | O | O | O | O | O |
| %TYPE Attribute | O | O | O | O | O |
| UPDATE Statement Extension | O | O | O | O | O |
| WHILE LOOP Statement | O | O | O | O | O |

Built-in Package 의 feature matrix는 다음과 같다.

<a id="6fd354f9058c3535"></a>
<table class="table column_count_7"><caption>Built-in Package의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="3f27cd25e31f0d93"></a>
### API

<a id="338f8675bdd65036"></a>
#### ODBC

ODBC 표준 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 feature matrix**

<a id="324f02cf6c3e6976"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| SQLAllocHandle() | O | O | O | O | O |
| SQLBindCol() | O | O | O | O | O |
| SQLBindParameter() | O | O | O | O | O |
| SQLCloseCursor() | O | O | O | O | O |
| SQLColAttribute() | O | O | O | O | O |
| SQLColumnPrivileges() | O | O | O | O | O |
| SQLColumns() | O | O | O | O | O |
| SQLConnect() | O | O | O | O | O |
| SQLDescribeCol() | O | O | O | O | O |
| SQLDescribeParam() | O | O | O | O | O |
| SQLDisconnect() | O | O | O | O | O |
| SQLDriverConnect() | O | O | O | O | O |
| SQLEndTran() | O | O | O | O | O |
| SQLExecDirect() | O | O | O | O | O |
| SQLExecute() | O | O | O | O | O |
| SQLExtendedFetch() | O | O | O | O | O |
| SQLFetch() | O | O | O | O | O |
| SQLFetchScroll() | O | O | O | O | O |
| SQLForeignKeys() | O | O | O | O | O |
| SQLFreeHandle() | O | O | O | O | O |
| SQLFreeStmt() | O | O | O | O | O |
| SQLGetConnectAttr() | O | O | O | O | O |
| SQLGetCursorName() | O | O | O | O | O |
| SQLGetData() | O | O | O | O | O |
| SQLGetDescField() | O | O | O | O | O |
| SQLGetDescRec() | O | O | O | O | O |
| SQLGetDiagField() | O | O | O | O | O |
| SQLGetDiagRec() | O | O | O | O | O |
| SQLGetEnvAttr() | O | O | O | O | O |
| SQLGetFunctions() | O | O | O | O | O |
| SQLGetInfo() | O | O | O | O | O |
| SQLGetStmtAttr() | O | O | O | O | O |
| SQLGetTypeInfo() | O | O | O | O | O |
| SQLMoreResults() | O | O | O | O | O |
| SQLNumParams() | O | O | O | O | O |
| SQLNumResultCols() | O | O | O | O | O |
| SQLParamData() | O | O | O | O | O |
| SQLPrepare() | O | O | O | O | O |
| SQLPrimaryKeys() | O | O | O | O | O |
| SQLProcedureColumns() | O | O | O | O | O |
| SQLProcedures() | O | O | O | O | O |
| SQLPutData() | O | O | O | O | O |
| SQLRowCount() | O | O | O | O | O |
| SQLSetConnectAttr() | O | O | O | O | O |
| SQLSetCursorName() | O | O | O | O | O |
| SQLSetDescField() | O | O | O | O | O |
| SQLSetDescRec() | O | O | O | O | O |
| SQLSetEnvAttr() | O | O | O | O | O |
| SQLSetPos() | O | O | O | O | O |
| SQLSetStmtAttr() | O | O | O | O | O |
| SQLSpecialColumns() | O | O | O | O | O |
| SQLStatistics() | O | O | O | O | O |
| SQLTablePrivileges() | O | O | O | O | O |
| SQLTables() | O | O | O | O | O |

ODBC 표준 이외의 부가적으로 지원하는 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 외 함수의 feature matrix**

<a id="8849351657ec4979"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| xa_open | O | O | O | O | O |
| xa_close | O | O | O | O | O |
| xa_start | O | O | O | O | O |
| xa_end | O | O | O | O | O |
| xa_rollback | O | O | O | O | O |
| xa_prepare | O | O | O | O | O |
| xa_commit | O | O | O | O | O |
| xa_recover | O | O | O | O | O |
| xa_forget | O | O | O | O | O |
| SQLGetXaSwitch | O | O | O | O | O |
| SQLGetXaConnectionHandle | O | O | O | O | O |
| SQLGetGroupCount | O | O | O | O | O |
| SQLGetGroupIDs | O | O | O | O | O |
| SQLGetGroupName | O | O | O | O | O |
| SQLGetSuitableGroupID | O | O | O | O | O |

<a id="170e19e9ce151d2a"></a>
#### JDBC

JDBC에 대한 class feature matrix는 다음과 같다.

**JDBC class의 feature matrix**

<a id="11402459178e5285"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| CallableStatement | O | O | O | O | O |
| CommonDataSource | O | O | O | O | O |
| Connection | O | O | O | O | O |
| ConnectionPoolDataSource | O | O | O | O | O |
| DatabaseMetaData | O | O | O | O | O |
| DataSource | O | O | O | O | O |
| Driver | O | O | O | O | O |
| ParameterMetaData | O | O | O | O | O |
| PooledConnection | O | O | O | O | O |
| PreparedStatement | O | O | O | O | O |
| ResultSet | O | O | O | O | O |
| ResultSetMetaData | O | O | O | O | O |
| RowId | O | O | O | O | O |
| Savepoint | O | O | O | O | O |
| Statement | O | O | O | O | O |
| XAConnection | O | O | O | O | O |
| XADataSource | O | O | O | O | O |
| XAResource | O | O | O | O | O |
| GoldilocksInterval | O | O | O | O | O |
| GoldilocksTypes | O | O | O | O | O |

<a id="4b634efb58aa0670"></a>
#### Embedded SQL

<a id="c2e1bb721f6f6c40"></a>
##### Precompiler Option

Precompiler의 option에 대한 feature matrix는 다음과 같다.

**Precompiler option의 feature matrix**

<a id="0d25a1b269721ac8"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | O | O | O | O | O |
| --include-path | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --output | O | O | O | O | O |
| --unsafe-null | O | O | O | O | O |
| --version | O | O | O | O | O |
| --no-lineinfo | O | O | O | O | O |
| --char_map | O | O | O | O | O |
| --cumulative | X | O | O | O | O |
| --autocommit | X | X | O | O | O |
| --parse | X | O | O | O | O |

<a id="839a34de02f2fb7b"></a>
##### Embedded SQL 전용 구문

Embedded SQL에서만 사용 가능한 SQL 구문에 대한 feature matrix는 다음과 같다.

**Embedded SQL 전용 구문의 feature matrix**

<a id="b0d053ae1ea69ad8"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| EXEC SQL AT | O | O | O | O | O |
| EXEC SQL ATOMIC INSERT | O | O | O | O | O |
| EXEC SQL AUTOCOMMIT | O | O | O | O | O |
| EXEC SQL BEGIN DECLARE SECTION | O | O | O | O | O |
| EXEC SQL COMMIT RELEASE | O | O | O | O | O |
| EXEC SQL CONNECT | O | O | O | O | O |
| EXEC SQL CONTEXT ALLOCATE | O | O | O | O | O |
| EXEC SQL CONTEXT FREE | O | O | O | O | O |
| EXEC SQL CONTEXT USE | O | O | O | O | O |
| EXEC SQL DISCONNECT | O | O | O | O | O |
| EXEC SQL END DECLARE SECTION | O | O | O | O | O |
| EXEC SQL FOR | O | O | O | O | O |
| EXEC SQL GET CLUSTER_GROUP_ID | X | X | X | X | O |
| EXEC SQL GET GROUPID | O | O | O | O | X |
| EXEC SQL INCLUDE | O | O | O | O | O |
| EXEC SQL INCLUDE SQLCA | O | O | O | O | O |
| EXEC SQL OPTION | O | O | O | O | O |
| EXEC SQL ROLLBACK RELEASE | O | O | O | O | O |
| EXEC SQL WHENEVER | O | O | O | O | O |
| EXEC SQL BEGIN ARGUMENT SECTION | X | X | O | O | O |
| EXEC SQL END ARGUMENT SECTION | X | X | O | O | O |

<a id="254a948f3ffd0140"></a>
##### Host Variable Data Type

Host 변수에 사용할 수 있는 embbeded SQL data type의 feature matrix는 다음과 같다.

**Host data type의 feature matrix**

<a id="08acb79085a0e760"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| C native type | O | O | O | O | O |
| struct, union | O | O | O | O | O |
| typedef | O | O | O | O | O |
| VARCHAR | O | O | O | O | O |
| LONG VARCHAR | O | O | O | O | O |
| BINARY | O | O | O | O | O |
| LONG VARBINARY | O | O | O | O | O |
| BOOLEAN | O | O | O | O | O |
| NUMBER | O | O | O | O | O |
| DATE | O | O | O | O | O |
| TIME | O | O | O | O | O |
| TIME WITH TIMEZONE | O | O | O | O | O |
| TIMESTAMP | O | O | O | O | O |
| TIMESTAMP WITH TIMEZONE | O | O | O | O | O |
| INTERVAL YEAR | O | O | O | O | O |
| INTERVAL MONTH | O | O | O | O | O |
| INTERVAL DAY | O | O | O | O | O |
| INTERVAL HOUR | O | O | O | O | O |
| INTERVAL MINUTE | O | O | O | O | O |
| INTERVAL SECOND | O | O | O | O | O |
| INTERVAL YEAR TO MONTH | O | O | O | O | O |
| INTERVAL DAY TO HOUR | O | O | O | O | O |
| INTERVAL DAY TO MINUTE | O | O | O | O | O |
| INTERVAL DAY TO SECOND | O | O | O | O | O |
| INTERVAL HOUR TO MINUTE | O | O | O | O | O |
| INTERVAL HOUR TO SECOND | O | O | O | O | O |
| INTERVAL MINUTE TO SECOND | O | O | O | O | O |

<a id="067ac9267e1629cb"></a>
##### Dynamic SQL

Dynamic SQL에 대한 feature matrix는 다음과 같다.

**Dynamic SQL의 feature matrix**

<a id="d6070f4e40b03189"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| SELECT .. INTO | O | O | O | O | O |
| EXECUTE IMMEDIATE sql | O | O | O | O | O |
| PREPARE stmt | O | O | O | O | O |
| ALLOCATE DESCRIPTOR | X | X | X | X | O |
| DEALLOCATE DESCRIPTOR | X | X | X | X | O |
| DESCRIBE INPUT stmt USING desc | X | X | X | X | O |
| DESCRIBE OUTPUT stmt USING desc | X | X | X | X | O |
| GET DESCRIPTOR | X | X | X | X | O |
| SET DESCRIPTOR | X | X | X | X | O |
| EXECUTE stmt | O | O | O | O | O |
| EXECUTE stmt USING DESCRIPTOR | X | X | X | X | O |
| EXECUTE stmt INTO DESCRIPTOR | X | X | X | X | O |
| DECLARE cursor FOR sql | O | O | O | O | O |
| DECLARE cursor FOR stmt | O | O | O | O | O |
| OPEN cursor | O | O | O | O | O |
| OPEN cursor USING | O | O | O | O | O |
| FETCH cursor INTO | O | O | O | O | O |
| FETCH cursor INTO DESCRIPTOR | X | X | X | X | O |
| CLOSE cursor | O | O | O | O | O |
| DELETE .. WHERE CURRENT OF cursor | O | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O | O |

<a id="1c4e38929d97664b"></a>
#### PyDBC

<a id="bfabe27d345df657"></a>
##### Module

PyDBC가 제공하는 pygoldilocks의 method feature matrix는 다음과 같다.

**pygoldilock method의 feature matrix**

<a id="9b292c06f711f982"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| connect | O | O | O | O | O |
| Date | O | O | O | O | O |
| Time | O | O | O | O | O |
| Timestamp | O | O | O | O | O |
| DateFromTicks | O | O | O | O | O |
| TimeFromTicks | O | O | O | O | O |
| TimestampFromTicks | O | O | O | O | O |
| Binary | O | O | O | O | O |
| STRING | O | O | O | O | O |
| BINARY | O | O | O | O | O |
| NUMBER | O | O | O | O | O |
| DATETIME | O | O | O | O | O |
| ROWID | O | O | O | O | O |
| getDecimalSeparator | O | O | O | O | O |
| setDecimalSeparator | O | O | O | O | O |

pygoldilocks module의 attribute feature matrix는 다음과 같다.

**pygoldilock attribute의 feature matrix**

<a id="6a5cb68ab64ebf7d"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| apilevel | O | O | O | O | O |
| threadsafety | O | O | O | O | O |
| paramstyle | O | O | O | O | O |
| version | O | O | O | O | O |
| lowercase | O | O | O | O | O |

<a id="553c1317f255b7a3"></a>
##### Connection

Connection 객체의 method feature matrix는 다음과 같다.

**Connection method의 feature matrix**

<a id="2f985f16b5e7bff4"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor | O | O | O | O | O |
| commit | O | O | O | O | O |
| rollback | O | O | O | O | O |
| close | O | O | O | O | O |
| getinfo | O | O | O | O | O |
| execute | O | O | O | O | O |
| set_attr | O | O | O | O | O |
| character_set_name | X | X | X | X | O |
| get_output_converter | X | X | X | X | O |
| add_output_converter | X | X | X | X | O |
| remove_output_converter | X | X | X | X | O |
| clear_output_converters | X | X | X | X | O |
| setencoding | X | X | X | X | O |
| setdecoding | X | X | X | X | O |
| __enter__ | X | X | X | X | O |
| __exit__ | X | X | X | X | O |

Connection 객체의 attribute feature matrix는 다음과 같다.

**Connection attribute의 feature matrix**

<a id="4d80a7e97d8a99b7"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| autocommit | O | O | O | O | O |
| closed | X | X | X | X | O |
| maxwrite | X | X | X | X | O |
| messages | X | X | X | X | O |
| searchescape | O | O | O | O | O |
| timeout | O | O | O | O | O |

<a id="aa471840ce97f4b7"></a>
##### Cursor

Cursor 객체의 method feature matrix는 다음과 같다.

**Cursor method의 feature matrix**

<a id="ca71a3ae1df32ca9"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| execute | O | O | O | O | O |
| executemany | O | O | O | O | O |
| fetchone | O | O | O | O | O |
| fetchall | O | O | O | O | O |
| fetchmany | O | O | O | O | O |
| fetchval | X | X | X | X | O |
| commit | O | O | O | O | O |
| rollback | O | O | O | O | O |
| skip | O | O | O | O | O |
| nextset | O | O | O | O | O |
| close | O | O | O | O | O |
| setinputsizes | O | O | O | O | O |
| setoutputsize | O | O | O | O | O |
| callproc | O | O | O | O | O |
| callfunc | O | O | O | O | O |
| tables | O | O | O | O | O |
| columns | O | O | O | O | O |
| statistics | O | O | O | O | O |
| rowIdColumns | O | O | O | O | O |
| rowVerColumns | O | O | O | O | O |
| primaryKeys | O | O | O | O | O |
| foreignKeys | O | O | O | O | O |
| procedures | O | O | O | O | O |
| procedureColumns | X | X | X | X | O |
| getTypeInfo | O | O | O | O | O |
| cancel | X | X | X | X | O |
| __enter__ | X | X | X | X | O |
| __exit__ | X | X | X | X | O |

Cursor 객체의 attribute feature matrix는 다음과 같다.

**Cursor attribute의 feature matrix**

<a id="41de73f9822ccc15"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| Description | O | O | O | O | O |
| rowcount | O | O | O | O | O |
| arraysize | O | O | O | O | O |
| connection | O | O | O | O | O |
| fast_executemany | O | O | O | O | O |
| closed | X | X | X | X | O |
| lastrowid | X | X | X | X | O |
| messages | X | X | X | X | O |
| timeout | X | X | X | X | O |

<a id="d29a5432df7ac73c"></a>
##### Row

Row 객체의 attribute feature matrix는 다음과 같다.

**Row attribute의 feature matrix**

<a id="816b645ff19a6a87"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor_description | O | O | O | O | O |

<a id="99c9f629caef2ec2"></a>
### Utility

<a id="afe1466db96b938b"></a>
#### gcreatedb

<a id="5520f45e63646381"></a>
##### Command Usage

gcreatedb의 command usage에 대한 feature matrix는 다음과 같다.

**gcreatedb command usage의 feature matrix**

<a id="4fc03dbd4b64e6e9"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --character_set | O | O | O | O | O |
| --char_length_units | O | O | O | O | O |
| --cluster | O | O | O | O | O |
| --db_comment | O | O | O | O | O |
| --db_name | O | O | O | O | O |
| --help | O | O | O | O | O |
| --host | O | O | O | O | O |
| --member | O | O | O | O | O |
| --port | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --timezone | O | O | O | O | O |

<a id="23bf22a73c285f4f"></a>
#### glsnr

<a id="faf84a7af5f99305"></a>
##### Command Usage

glsnr의 command usage에 대한 feature matrix는 다음과 같다.

**glsnr command usage의 feature matrix**

<a id="c3846c11d094dd59"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | O | O | O | O | O |
| --home | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --start | O | O | O | O | O |
| --status | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="d3a8e407aa3f0e85"></a>
##### Configuration File

glsnr의 configuration에 대한 feature matrix는 다음과 같다.

**glsnr configuration file syntax의 feature matrix**

<a id="5d25da6c00f3337a"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| BACKLOG | O | O | O | O | O |
| DEFAULT_CS_MODE | O | O | O | O | O |
| LISTENER_LOG_DIR | O | O | O | O | O |
| LISTEN_PORT | O | O | O | O | O |
| TCP_EXCLUDED | O | O | O | O | O |
| TCP_INVITED | O | O | O | O | O |
| TCP_HOST | O | O | O | O | O |
| TCP_VALIDNODE_CHECKING | O | O | O | O | O |
| TIMEOUT | O | O | O | O | O |
| USR_DIR | O | O | O | O | O |

<a id="79ae0d28d8a2eb07"></a>
#### gsql/gsqlnet

<a id="bf25f1608d81d4cc"></a>
##### Command Usage

gsql의 command usage에 대한 feature matrix는 다음과 같다.

**gsql command usage의 feature matrix**

<a id="048ede8203cdfb7e"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| username password | O | O | O | O | O |
| --as {SYSDBA\|ADMIN} | O | O | O | O | O |
| --conn-string | O | O | O | O | O |
| --dsn | O | O | O | O | O |
| --enable-color | O | O | O | O | O |
| --help | O | O | O | O | O |
| --import | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --prompt | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --version | O | O | O | O | O |

<a id="af19b792e644f74b"></a>
##### Interactive gsql Command

gsql 프롬프트 상태에서 사용하는 interactive gsql command에 대한 feature matrix는 다음과 같다.

**Interactive gsql command의 feature matrix**

<a id="d3d11326479e0935"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| `\\` | O | O | O | O | O |
| `\connect userid password [as sysdba] ` | O | O | O | O | O |
| `\cshutdown` | O | O | O | O | O |
| `\cstartup` | O | O | O | O | O |
| `\ddl_cluster` | O | O | O | O | O |
| `\ddl_db` | O | O | O | O | O |
| `\ddl_tablespace` | O | O | O | O | O |
| `\ddl_profile` | O | O | O | O | O |
| `\ddl_audit_policy` | O | O | O | O | O |
| `\ddl_user` | O | O | O | O | O |
| `\ddl_role` | X | X | X | X | O |
| `\ddl_schema` | O | O | O | O | O |
| `\ddl_public_synonym` | O | O | O | O | O |
| `\ddl_table` | O | O | O | O | O |
| `\ddl_constraint` | O | O | O | O | O |
| `\ddl_index` | O | O | O | O | O |
| `\ddl_view` | O | O | O | O | O |
| `\ddl_sequence` | O | O | O | O | O |
| `\ddl_synonym` | O | O | O | O | O |
| `\ddl_procedure` | O | O | O | O | O |
| `\ddl_package` | X | O | O | O | O |
| `\ddl_trigger` | X | X | X | X | O |
| `\desc ` | O | O | O | O | O |
| `\dynamic sql :var ` | O | O | O | O | O |
| `\exec ` | O | O | O | O | O |
| `\exec :var := :value` | O | O | O | O | O |
| `\exec sql ` | O | O | O | O | O |
| `\explain plan [on\|only] ` | O | O | O | O | O |
| `\help ` | O | O | O | O | O |
| `\history` | O | O | O | O | O |
| `\host {os_command}` | O | O | O | O | O |
| `\import` | O | O | O | O | O |
| `\idesc ` | O | O | O | O | O |
| `\{n} ` | O | O | O | O | O |
| `\prepare sql ` | O | O | O | O | O |
| `\print ` | O | O | O | O | O |
| `\quit` | O | O | O | O | O |
| `\set autocommit ` | O | O | O | O | O |
| `\set color ` | O | O | O | O | O |
| `\set colsize ` | O | O | O | O | O |
| `\set ddlsize` | O | O | O | O | O |
| `\set error ` | O | O | O | O | O |
| `\set history ` | O | O | O | O | O |
| `\set linesize ` | O | O | O | O | O |
| `\set numsize ` | O | O | O | O | O |
| `\set pagesize ` | O | O | O | O | O |
| `\set sqlprompt` | X | X | X | O | O |
| `\set timing ` | O | O | O | O | O |
| `\set vertical ` | O | O | O | O | O |
| `\shutdown {abort\|immediate\|transactional\|normal}` | O | O | O | O | O |
| `\startup {nomount\|mount\|open} ` | O | O | O | O | O |
| `\var ` | O | O | O | O | O |

<a id="9fd2774b9e1c9936"></a>
#### gloader/gloadernet

<a id="de41baa2b2495d6a"></a>
##### Command Usage

gloader의 command usage에 대한 feature matrix는 다음과 같다.

**gloader command usage의 feature matrix**

<a id="2d030d2a033ef054"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| username password | O | O | O | O | O |
| --append | X | X | X | X | O |
| --array | O | O | O | O | O |
| --atomic | O | O | O | O | O |
| --bad | O | O | O | O | O |
| --buffered | O | O | O | O | O |
| --commit | O | O | O | O | O |
| --comment | O | O | O | O | O |
| --control | O | O | O | O | O |
| --data | O | O | O | O | O |
| --dsn | O | O | O | O | O |
| --errors | O | O | O | O | O |
| --export | O | O | O | O | O |
| --fieldterm | O | O | O | O | O |
| --filesize | O | O | O | O | O |
| --format | O | O | O | O | O |
| --help | O | O | O | O | O |
| --import | O | O | O | O | O |
| --lineterm | O | O | O | O | O |
| --log | O | O | O | O | O |
| --no-copyright | O | O | O | O | O |
| --parallel | O | O | O | O | O |
| --propagation | O | O | O | O | O |
| --qualifier | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --skip | X | X | X | X | O |
| --tablename | O | O | O | O | O |
| --AsTIMESTAMP | O | O | O | O | O |
| --where | O | O | O | O | O |
| --group-id | O | O | O | O | O |
| --directio-size | O | O | O | O | X |
| --merge | X | X | X | X | O |
| --skip_index_maintenance | X | X | X | X | O |
| --nologging | X | X | X | X | O |

<a id="34cc10023900742b"></a>
##### Control File Syntax

gloader의 control file syntax에 대한 feature matrix는 다음과 같다.

**gloader control file syntax의 feature matrix**

<a id="e8a637671a39c5c8"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| APPEND | X | X | X | X | O |
| CHARACTERSET | O | O | O | O | O |
| FIELDS TERMINATED BY | O | O | O | O | O |
| OPTIONALLY ENCLOSED BY | O | O | O | O | O |
| TABLE [schema_name.]table_name | O | O | O | O | O |
| TABLE table_name [ ( column_description) ] | X | X | X | X | O |
| LTRIM | O | O | O | O | O |
| RTRIM | O | O | O | O | O |
| LINES TERMINATED BY | O | O | O | O | O |
| WHERE | O | O | O | O | O |

<a id="232a86e769e677d8"></a>
#### gdump

<a id="fa2a5433701e3323"></a>
##### Command Usage

gdump의 command usage에 대한 feature matrix는 다음과 같다.

<a id="542b180329ffd2a1"></a>
<table class="table column_count_7"><caption>gdump command usage의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CHANGE_TRACK</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCATION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REDO_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="3356face8c56e967"></a>
#### tablediff

<a id="b740b6803864a5a2"></a>
##### Configuration File

tablediff의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="6b8cb7bbf93d60c3"></a>
<table class="table column_count_7"><caption>tablediff configuration file의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td><div>SOURCE_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td><div>TARGET_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td><div>TARGET_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_UPDATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_DELETE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td><div>DIFF_BIN_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DIFF_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_CALL_STACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_ROW_UNIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>EXCLUDE_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_DIFF</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_SUCCESS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_QUEUE_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_THREAD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_UNIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PARTITION_RANGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>WHERE_CLAUSE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="1f29168c67951e2f"></a>
#### gsyncher

<a id="ae169898317b0a99"></a>
##### Command Usage

gsyncher의 command usage에 대한 feature matrix는 다음과 같다.

**gsyncher command usage의 feature matrix**

<a id="d453a20429ea14a8"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --log | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --home | O | O | O | O | O |
| --copy-right | O | O | O | O | O |
| --backup-path | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="7c078e83112fcd47"></a>
#### gmon

<a id="b67ae74e8667b1c1"></a>
##### Command Usage

gmon의 command usage에 대한 feature matrix는 다음과 같다.

**gmon command usage의 feature matrix**

<a id="7013c43021f04669"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --status | O | O | O | O | O |
| --home | O | O | O | O | O |
| --uds_dir | X | O | O | O | O |
| --silent | O | O | O | O | O |
| --no-copyright | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="bf154453ae0a7962"></a>
#### gtrclogger

<a id="26f6f222b9c67efd"></a>
##### Command Usage

gtrclogger의 command usage에 대한 feature matrix는 다음과 같다.

**gtrclogger command usage의 feature matrix**

<a id="b1caf59dacca07d2"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --dir | O | O | O | O | O |
| --help | O | O | O | O | O |
| --port | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="0b9aec940bf00777"></a>
#### glocator

<a id="c98e1e0909765614"></a>
##### Command Usage

glocator의 command usage에 대한 feature matrix는 다음과 같다.

**glocator command usage의 feature matrix**

<a id="3fa59f15c1ee3d04"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --create | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --conf | O | O | O | O | O |
| --status | O | O | O | O | O |
| --sync | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --no-copyright | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="7621d3a0f01c017e"></a>
##### Configuration File

glocator의 configuration file에 대한 feature matrix는 다음과 같다.

**glocator configuration file의 feature matrix**

<a id="a41703e3ffc67f69"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| HOST | O | O | O | O | O |
| PORT | O | O | O | O | O |
| WORKER_COUNT | O | O | O | O | O |
| MAX_NODE_COUNT | O | O | O | O | O |
| MESSAGE_QUEUE_SIZE | O | O | O | O | O |
| MESSGE_ALLOCATOR_SIZE | O | O | O | O | O |
| PACKET_ALLOCATOR_SIZE | O | O | O | O | O |
| SYSTEM_LOGGER_DIR | O | O | O | O | O |
| SYSTEM_UDS_DIR | O | O | O | O | O |
| LOCATION_FILE_DIR | O | O | O | O | O |
| LOCATION_FILE_SIZE | O | O | O | O | O |
| LOCATION_FILE_MAX_SIZE | O | O | O | O | O |
| MESSAGE_TIMEOUT | O | O | O | O | O |
| ALTERNATE_LOCATOR | O | O | O | O | O |
| SYNC_RETRY_COUNT | O | O | O | O | O |
| SYNC_RESPONSE_TIMEOUT | O | O | O | O | O |
| KEEPALIVE_IDLE_TIME | O | O | O | O | O |
| KEEPALIVE_COUNT | O | O | O | O | O |
| KEEPALIVE_INTERVAL | O | O | O | O | O |

<a id="b13eea4ef652e41f"></a>
#### gagent

<a id="3d28a67c84d24ab4"></a>
##### Command Usage

gagent의 command usage에 대한 feature matrix는 다음과 같다.

**gagent command usage의 feature matrix**

<a id="cccb4206f2c9ac42"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --conf | O | O | O | O | O |
| --status | O | O | O | O | O |
| --home | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --no-copyright | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="41ed4d99556426ed"></a>
##### Configuration File

gagent의 configuration file에 대한 feature matrix는 다음과 같다.

**gagent configuration file의 feature matrix**

<a id="5035241e5007d29c"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| REQUEST_PORT | X | O | O | O | O |
| RESPONSE_PORT | X | O | O | O | O |
| HOST | X | O | O | O | O |
| LOCATOR_HOST | O | O | O | O | O |
| LOCATOR_PORT | O | O | O | O | O |
| SYSTEM_LOGGER_DIR | O | O | O | O | O |
| SYSTEM_UDS_DIR | O | O | O | O | O |
| ALTERNATE_LOCATOR | O | O | O | O | O |
| KEEPALIVE_IDLE_TIME | X | O | O | O | O |
| KEEPALIVE_COUNT | X | O | O | O | O |
| KEEPALIVE_INTERVAL | X | O | O | O | O |

<a id="f7f38d85bb64204b"></a>
#### gloctl

<a id="746c27ecafe8b398"></a>
##### Command Usage

gloctl의 command usage에 대한 feature matrix는 다음과 같다.

**gloctl command usage의 feature matrix**

<a id="e2f1d825aebcb830"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --dsn | X | X | X | X | X |
| --conf | O | O | O | O | O |
| --ip | O | O | O | O | O |
| --port | O | O | O | O | O |
| --import | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --no-copyright | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="c9621218a914d1ae"></a>
##### Configuration File

gloctl의 configuration file에 대한 feature matrix는 다음과 같다.

**gloctl configuration file의 feature matrix**

<a id="dda08de92d4799d8"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | O | O | O | O | O |
| LOCATOR_HOST | O | O | O | O | O |
| LOCATOR_PORT | O | O | O | O | O |

<a id="31ea5c069e635ac4"></a>
### Replication

<a id="623ab5d6027db2bd"></a>
#### cyclone

<a id="ffcbe876c8ae5a42"></a>
##### Command Usage

cyclone의 command usage에 대한 feature matrix는 다음과 같다.

**cyclone command usage의 feature matrix**

<a id="f55863561f6dacdc"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --encrypt | O | O | O | O | O |
| --group | O | O | O | O | O |
| --help | O | O | O | O | O |
| --key | O | O | O | O | O |
| --master | O | O | O | O | O |
| --reset | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --slave | O | O | O | O | O |
| --start | O | O | O | O | O |
| --status | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --sync | O | O | O | O | O |
| --stand-alone | O | O | O | O | O |
| --recovery | O | O | O | O | O |
| --local | O | O | O | O | O |
| --info | O | O | O | O | O |

<a id="17c065ae6057c2b4"></a>
##### Configuration File

cyclone의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="f3bec42f5683234d"></a>
<table class="table column_count_7"><caption>cyclone configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="13"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HEARTBEAT_TIMEOUT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRACE_LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="17"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SKIP_COMMENT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_FORCE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PACKET_COMPRESSION_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_MYSQL_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_DB2_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_TIBERO_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="16"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>UPDATE_APPLY_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIBERO_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLIER_DEADLOCK_PRIORITY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLIER_TRACE_LOG_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="2317b1f76bb428f7"></a>
#### clustone

Clustone이 deprecate 되었다.

<a id="da9f372c2419a32f"></a>
#### logmirror

<a id="730b64c86977a8f1"></a>
##### Command Usage

logmirror의 command usage에 대한 feature matrix는 다음과 같다.

**logmirror command usage의 feature matrix**

<a id="1352460f0c8ed54a"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --help | O | O | O | O | O |
| --infiniband | O | O | O | O | O |
| --master | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --slave | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --key | O | O | O | O | O |
| --encrypt | O | O | O | O | O |

<a id="14e8b7c239266371"></a>
##### Configuration File

logmirror의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="91169a2e12f92cb2"></a>
<table class="table column_count_7"><caption>logmirror configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4b0a50a601bb9f98"></a>
#### cymon

<a id="2a79b8c8f7e08349"></a>
##### Command Usage

cymon의 command usage에 대한 feature matrix는 다음과 같다.

**cymon command usage의 feature matrix**

<a id="109c630aadbb4302"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --help | O | O | O | O | O |
| --cycle | O | O | O | O | O |
| --key | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --status | O | O | O | O | O |

<a id="be8ea04d7e2d89d0"></a>
#### cyfile

<a id="8d867195bad5ffa3"></a>
##### Command Usage

cyfile의 command usage에 대한 feature matrix는 다음과 같다.

**cyfile command usage의 feature matrix**

<a id="4e58eafea03e25d0"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | X | O | O | O | O |
| --help | X | O | O | O | O |
| --reset | X | O | O | O | O |
| --key | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --info | X | O | O | O | O |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --group | X | O | O | O | O |
| --encrypt | X | O | O | O | O |
| --status | X | O | O | O | O |
| --stand-alone | X | O | O | O | O |

<a id="a28afae8ba28365b"></a>
##### Configuration File

cyfile의 configuration file에 대한 feature matrix는 다음과 같다.

**cyfile configuration file의 feature matrix**

<a id="aea3bb9621119205"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| DSN | X | O | O | O | O |
| HOST_IP | X | O | O | O | O |
| HOST_PORT | X | O | O | O | O |
| PROTOCOL | X | O | O | O | O |
| USER_ID | X | O | O | O | O |
| USER_PW | X | O | O | O | O |
| GROUP_NAME | X | O | O | O | O |
| USER_ENCRYPT_PW | X | O | O | O | O |
| CAPTURE_TABLE | X | O | O | O | O |
| READ_LOG_BLOCK_COUNT | X | O | O | O | O |
| TRANS_SORT_AREA_SIZE | X | O | O | O | O |
| TRANS_FILE_PATH | X | O | O | O | O |
| LOG_CAPTURE_INTERVAL_1 | X | O | O | O | O |
| LOG_CAPTURE_INTERVAL_2 | X | O | O | O | O |
| DATA_FILE_PATH | X | O | O | O | O |
| DATA_FILE_PREFIX | X | O | O | O | O |
| DATA_FILE_SIZE | X | O | O | O | O |
| UPDATE_BEFORE_VALUE | X | O | O | O | O |

<a id="ad5c48c6110955dd"></a>
## What's New in GOLDILOCKS 26c.1

본 장은 GOLDILOCKS 26c.1에 새로 추가된 기능들에 대해 간략히 설명한다.

<a id="aeea74eb494e3876"></a>
### Architecture

<a id="9b497229d48e7da7"></a>
#### System Architecture

릴리즈 플랫폼에서 다음과 같은 platform 이 제거되었다.

- HP
- AIX
- PPC64

<a id="11bea9afd9211abf"></a>
#### Storage Internal

변동 사항 없음

<a id="bc9f7a3a3dc4fdfb"></a>
#### Transaction Control

트랜잭션의 ISOLATION LEVEL 중 SERIALIZABLE 은 cluster system 에서 더 이상 지원하지 않는다.

<a id="a99849e28860e55f"></a>
#### Backup & Recovery

병렬 복구를 위한 [parallel recovery 기능](../part-03-sql-manual/18-sql-references-a-b.md#233fbcf85decd22e)이 추가되었다.

병렬 백업을 위한 [parallel backup 기능](../part-03-sql-manual/18-sql-references-a-b.md#93565f80d30924b0)이 추가되었다.

병렬 복원을 위한 [parallel restore 기능](../part-03-sql-manual/18-sql-references-a-b.md#60ea018060bd0c35)이 추가되었다.

<a id="1cd62460e1e83b6f"></a>
#### Database Information

<a id="bfbc97f74a6c2a67"></a>
##### DICTIONARY_SCHEMA

Role에 대한 정보를 조회하기 위해 다음 view들이 추가되었다.

- [DBA_ROLES](../part-02-administration-manual/9-database-information.md#18c475b2ae70e7f4)
- [DBA_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#73ae5fee2af31c6b)
- [USER_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#f5acc6f79a1ec982)
- [ROLE_COL_PRIVS](../part-02-administration-manual/9-database-information.md#cb971b9e672523a4)
- [ROLE_DB_PRIVS](../part-02-administration-manual/9-database-information.md#acb5f5769893d030)
- [ROLE_PACKAGE_PRIVS](../part-02-administration-manual/9-database-information.md#dc87b0d3eaab2580)
- [ROLE_PROC_PRIVS](../part-02-administration-manual/9-database-information.md#09d06287320caea3)
- [ROLE_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#2404a08308b1e2c0)
- [ROLE_SCHEMA_PRIVS](../part-02-administration-manual/9-database-information.md#f989b2154a832373)
- [ROLE_SEQ_PRIVS](../part-02-administration-manual/9-database-information.md#5f7e282867bb459c)
- [ROLE_SYS_PRIVS](../part-02-administration-manual/9-database-information.md#418c8aa9b1d53846)
- [ROLE_TAB_PRIVS](../part-02-administration-manual/9-database-information.md#25e9323ff840e05c)
- [ROLE_TBS_PRIVS](../part-02-administration-manual/9-database-information.md#462dc6980831d98c)
- [SESSION_ROLES](../part-02-administration-manual/9-database-information.md#dcbd0ed855449050)

Histogram 정보를 조회하기 위해 다음 view들이 추가되었다.

- [ALL_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#b7f4d01b2a94e713)
- [ALL_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#dad9ef0d72ca81dd)
- [DBA_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#09c3d6ca433f6967)
- [DBA_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#dff4e7fbc504613c)
- [USER_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#267df225b64b2f0d)
- [USER_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#c1c6f648a3e9c3c4)

Library 객체 정보를 조회하기 위해 다음 view들이 추가되었다.

- [ALL_LIBRARIES](../part-02-administration-manual/9-database-information.md#d98055987666e009)
- [ALL_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#ecc689fec6b9a03d)
- [ALL_LIBRARY_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#dbe2595e1791998b)
- [ALL_LIBRARY_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#3c76a7b72dfc2ce6)
- [DBA_LIBRARIES](../part-02-administration-manual/9-database-information.md#fe133756d9523ec8)
- [DBA_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#c45ee9ed4bd8719b)
- [USER_LIBRARIES](../part-02-administration-manual/9-database-information.md#68259f0728c9d8db)
- [USER_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#011adb422490cceb)
- [USER_LIBRARY_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#64751101e6ed0d23)
- [USER_LIBRARY_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#2159518323a3b7fa)
- [ROLE_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#bd0a54d96c906072)

Trigger 객체 정보를 조회하기 위해 다음 view들이 추가되었다.

- [ALL_TRIGGERS](../part-02-administration-manual/9-database-information.md#4411cc85725f6776)
- [DBA_TRIGGERS](../part-02-administration-manual/9-database-information.md#2faa31e61f2379f1)
- [USER_TRIGGERS](../part-02-administration-manual/9-database-information.md#da4c6f4ef1c163db)

<a id="09789bb3fd03ab71"></a>
##### INFORMATION_SCHEMA

Role에 대한 정보를 조회하기 위해 다음 view들이 추가되었다.

- [ADMINISTRABLE_ROLE_AUTHORIZATIONS](../part-02-administration-manual/9-database-information.md#b79db007a27dc6cf)
- [APPLICABLE_ROLES](../part-02-administration-manual/9-database-information.md#bd47c46100f17655)
- [ENABLED_ROLES](../part-02-administration-manual/9-database-information.md#1a74c1aceda9783b)
- [ROLE_COLUMN_GRANTS](../part-02-administration-manual/9-database-information.md#3d2b11ed66218115)
- [ROLE_MODULE_GRANTS](../part-02-administration-manual/9-database-information.md#2c8b0992131aaabd)
- [ROLE_ROUTINE_GRANTS](../part-02-administration-manual/9-database-information.md#9619508606d2776e)
- [ROLE_TABLE_GRANTS](../part-02-administration-manual/9-database-information.md#fc8b32800e452fd1)
- [ROLE_USAGE_GRANTS](../part-02-administration-manual/9-database-information.md#7955d1c7839ad3b9)

CHECK 제약 조건 정보를 조회하기 위해 [CHECK_CONSTRAINTS](../part-02-administration-manual/9-database-information.md#ac3225f1a6a74612) view가 추가되었다.

Trigger 정보를 조회할 수 있는 다음과 같은 view 들이 추가되었다.

- [TRIGGERED_UPDATE_COLUMNS](../part-02-administration-manual/9-database-information.md#b05f349928e40ed8)
- [TRIGGERS](../part-02-administration-manual/9-database-information.md#e81a9859de741ee3)
- [TRIGGER_EVENT_ORDER](../part-02-administration-manual/9-database-information.md#7a2acb29cb1714e9)
- [TRIGGER_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#d4fcbd71fb7e1511)
- [TRIGGER_ROUTINE_USAGE](../part-02-administration-manual/9-database-information.md#c645c53788b61e17)
- [TRIGGER_SEQUENCE_USAGE](../part-02-administration-manual/9-database-information.md#bc3e28cc394151cd)
- [TRIGGER_TABLE_USAGE](../part-02-administration-manual/9-database-information.md#5408701b0cf2b9e9)

<a id="8fa3eafd64ffde05"></a>
##### PERFORMANCE_VIEW_SCHEMA

다음과 같은 view 들이 추가되었다.

- [V$DB_PROPERTY](../part-02-administration-manual/9-database-information.md#b51644ad5d756018)
- [V$RELATION](../part-02-administration-manual/9-database-information.md#968718f4c44e1f4a)
- [V$TCL_LOGFILE](../part-02-administration-manual/9-database-information.md#0970c7bb710b15d4)
- [V$ALLOCATOR](../part-02-administration-manual/9-database-information.md#71b3c73a3fd79d8d)
- [V$CLUSTER_CONNECTION](../part-02-administration-manual/9-database-information.md#9237f1978b67a40a)
- [V$CLUSTER_QUEUE](../part-02-administration-manual/9-database-information.md#cb1d377a01eb9832)
- [V$UNDO_SEGMENT](../part-02-administration-manual/9-database-information.md#426d35a70c53845c)

<a id="d5d8a2d47135b8cd"></a>
#### Server Property

[DEFAULT_INDEX_PCTFREE](../part-02-administration-manual/10-server-property.md#a70319f95fa6c573)의 기본값이 10으로 변경되었다.

병렬 복구 기능이 추가되었고, 병렬화 정도를 제어하기 위해 [RECOVERY_SLAVES](../part-02-administration-manual/10-server-property.md#0f33ffc599e55ae7) 프로퍼티가 추가되었다.

[DEFAULT_MAXTRANS](../part-02-administration-manual/10-server-property.md#38446e3a7bf4bd60)의 기본값이 32로 변경되었다.

ANALYZE TABLE 수행 시 histogram bucket의 개수를 제어하기 위해 다음 프로퍼티가 추가되었다.  
• [HISTOGRAM_BALANCE_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#0646042872327a32)  
• [HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT](../part-02-administration-manual/10-server-property.md#4e46aae7c1ded5d0)  
• [HISTOGRAM_FREQUENCY_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#ef42f2f75da19f94)

시스템의 증분 백업 수행을 위한 기준을 설정하는 기존 프로퍼티 INCREMENTAL_CHECKPOINT_CRITERIA의 이름이 [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#141a470d8d601f73)로 변경되고 기본값도 0으로 변경되었다.

디스크 테이블스페이스를 위한 버퍼 관리 알고리즘을 개선하기 위해 [BUFFER_LRU_SCAN_PERCENT](../part-02-administration-manual/10-server-property.md#1cabedb4fd0fbd38) 프로퍼티가 추가되었다.

클러스터 환경에서 통신 버퍼 수를 지정하는 CLUSTER_CM_BUFFER_COUNT property가 deprecate되었다. 이를 대신하여 lockable, lockless, synchronization dispatcher를 위한 통신 버퍼 수를 지정하는 [LOCKABLE_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#6ea8fae775896cf8), [LOCKLESS_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#4ddbc6e597502b57), [SYNC_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#3e14bf273b75b9e8) 프로퍼티가 추가되었다.

디스크 테이블스페이스에 생성된 테이블을 전체 스캔할 때 버퍼에 캐싱할지 여부는 테이블 크기의 threshold에 따라 결정된다. 이 threshold 값을 설정하기 위해 [FULL_TABLE_SCAN_CACHING_THRESHOLD](../part-02-administration-manual/10-server-property.md#0aad276c305d59dd) 프로퍼티가 추가되었다.

Hash instant table의 예상 bucket count의 최대값을 설정하는 [INST_HASH_TABLE_BUCKET_MAX_COUNT](../part-02-administration-manual/10-server-property.md#6fb8b231e1d09cef) 프로퍼티가 추가되었다.

Plan cache에 캐싱할 SQL의 최대 개수를 제한하는 두 개의 property 중에 MAXIMUM_FLANGE_COUNT property는 deprecate 하고 [PLAN_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#20b7c3ce69752590) 만으로 제어하도록 했다.

[PLAN_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#20b7c3ce69752590) 의 프로퍼티 속성이 변경되었다. 기존에는 서버를 재시작해야만 적용되던 속성인데 재시작없이 온라인에서 즉시 변경되도록 수정되었다.

[V$SQL_CACHE](../part-02-administration-manual/9-database-information.md#752ef279734cff3f)에서 REF_COUNT 컬럼이 제거되었다.

[AGING_PLAN_INTERVAL](../part-02-administration-manual/10-server-property.md#057ca3b036d23605)의 기본값이 0 에서 3 으로 변경되었다.

[SESSION_MEMORY_INIT_SIZE](../part-02-administration-manual/10-server-property.md#9d01096d9cfaec26)의 기본값이 131072 에서 524288 로 변경되었다.

Global transaction 로그 파일의 블록 크기를 설정할 수 있는 [GLOBAL_TRANSACTION_LOG_BLOCK_SIZE](../part-02-administration-manual/10-server-property.md#0c5e9ac0a13685cd) 프로퍼티가 추가되었다.

공유 세션 (shared session)의 초기 메모리 크기를 설정할 수 있는 [SHARED_SESSION_MEMORY_INIT_SIZE](../part-02-administration-manual/10-server-property.md#6a10fcab391aff45) 프로퍼티가 추가되었다.

인스턴트 인덱스의 공간 사용량을 줄일 수 있는 [INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD](../part-02-administration-manual/10-server-property.md#f8c688afe0275310) 프로퍼티가 추가되었다.

Cluster 에서 모든 멤버가 같은 [TRANSACTION_TABLE_SIZE](../part-02-administration-manual/10-server-property.md#e20fffefb153528b)를 가져야 하는 제약이 제거되었다.

Cluster에서 CLUSTER_DEADLOCK_TIMEOUT 프로퍼티를 사용하지 않고 자체적으로 데드락을 검출하도록 변경되면서, 해당 프로퍼티는 deprecate 되었다.

Cluster에서 replica를 반영할 때 기본적으로 async replica 방식을 사용하도록 개선되었다. 다만 async replica 방식을 사용할 수 없을 경우에는 내부적으로 자동 처리되도록 하여, CLUSTER_ASYNC_REPLICATION 프로퍼티가 deprecate 되었다.

[SHARED_MEMORY_STATIC_SIZE](../part-02-administration-manual/10-server-property.md#eadde14e86afa8c7)의 기본값이 800M로 변경되었다.

INST_TABLE_BLOCK_SIZE가 [INST_TABLE_PAGE_SIZE](../part-02-administration-manual/10-server-property.md#b38e42dbc41377ae)로 이름이 변경되었다.

인덱스 구축 및 재구축 시 발생하는 로그의 기록 속도를 제어할 수 있는 [REDO_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#c462a3db9feff284) 프로퍼티가 추가되었다.

Cluster에서 commit 관련 프로토콜이 별도의 dispatcher와 queue를 사용하도록 개선되면서 CLUSTER_COMMIT_STREAM_ISOLATION 프로퍼티가 deprecate 되었다.

컨트롤 파일을 저장할 때 임시 파일을 이용하지 않는 방식으로 변경됨에 따라 CONTROL_FILE_TEMP_NAME 프로퍼티가 deprecate 되었다.

다음 프로퍼티들의 이름이 변경되었다.

- [REBALANCE_BLOCK_READ_COUNT](../part-02-administration-manual/10-server-property.md#98e553f99018623b) 가 [ONLINE_DDL_BLOCK_READ_COUNT](../part-02-administration-manual/10-server-property.md#3ecfa3edb0e08bb5) 로 변경되었다.
- [REBALANCE_SHARD_DIVISOR](../part-02-administration-manual/10-server-property.md#3137b14c38b962c3) 가 [ONLINE_DDL_SCAN_PARTITION](../part-02-administration-manual/10-server-property.md#20196df5e431393d) 으로 변경되었다.
- [MAXIMUM_JOURNAL_REPLAY_COUNT](../part-02-administration-manual/10-server-property.md#90a84bfae7d953f9) 가 [ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT](../part-02-administration-manual/10-server-property.md#fa65edf9db034833) 로 변경되었다.
- [ONLINE_JOURNAL_REPLAY_THRESHOLD](../part-02-administration-manual/10-server-property.md#e62842c82d708977) 가 [ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD](../part-02-administration-manual/10-server-property.md#39cb80c592e7815c) 로 변경되었다.

gmaster의 log flusher thread가 event를 기다리는 동안 busy waiting을 수행하는 시간을 조절할 수 있는 [LOG_FLUSHER_HOT_POLICY_INTERVAL](../part-02-administration-manual/10-server-property.md#ac2066d1577ab221) 프로퍼티가 추가되었다.

Redo log archiving 시 디스크 I/O 성능을 제어할 수 있는 [ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#0dcd99b270ed698c) 프로퍼티가 추가되었다.

<a id="63be70cd1cf5c83c"></a>
### SQL

<a id="ba457bf7b4b63cbd"></a>
#### SQL Element

<a id="f1354f46dd0b3784"></a>
##### Data Type

변동 사항 없음

<a id="7cbbec366dc5a386"></a>
##### Function

System information function인 [CURRENT_ROLE](../part-03-sql-manual/17-built-in-function-references.md#84f3b85ed9383e58) 과 [LOCAL_MEMBER_POSITION](../part-03-sql-manual/17-built-in-function-references.md#afd5f1462dcfbc60)이 추가되었다.

Built-in function인 [GROUPING](../part-03-sql-manual/17-built-in-function-references.md#6be942edd0b74700) 과 [GROUPING_ID](../part-03-sql-manual/17-built-in-function-references.md#34f7482b59045a4e)가 추가되었다.

Built-in function인 regular expression이 추가되었다.

- [REGEXP_COUNT](../part-03-sql-manual/17-built-in-function-references.md#5a9c61acf90fd5c1)
- [REGEXP_INSTR](../part-03-sql-manual/17-built-in-function-references.md#3a5d8345b833199f)
- [REGEXP_LIKE Condition](../part-03-sql-manual/11-sql-elements.md#bd7439f58b8d5d07)
- [REGEXP_REPLACE](../part-03-sql-manual/17-built-in-function-references.md#cbbf5abf3bd78123)
- [REGEXP_SUBSTR](../part-03-sql-manual/17-built-in-function-references.md#cefe81f21ed82b68)

Built-in function인 [JSON String Constructor](../part-03-sql-manual/11-sql-elements.md#d0188a14aead086d)의 [JSON Output Clause](../part-03-sql-manual/11-sql-elements.md#d8ec54a70fd9d3a7)에 PRETTY 옵션이 추가되었다.

Built-in function인 [JSON_OBJECT](../part-03-sql-manual/17-built-in-function-references.md#8cd5e69d1f7d5ba9), [JSON_OBJECTAGG](../part-03-sql-manual/17-built-in-function-references.md#f2ed9f8209629cd7), [JSON_OBJECTAGG() OVER](../part-03-sql-manual/17-built-in-function-references.md#4b6cac5f93cac0c0)에 [JSON Key Uniqueness Constraint](../part-03-sql-manual/11-sql-elements.md#2bce9d5d0bac743d) 옵션이 추가되었다.

Built-in function인 [JSON_ARRAYAGG](../part-03-sql-manual/17-built-in-function-references.md#6a1307addaa8d032), [JSON_ARRAYAGG() OVER](../part-03-sql-manual/17-built-in-function-references.md#677ae68f770b3e92)에 [JSON Array Aggregate Order By Clause](../part-03-sql-manual/11-sql-elements.md#90516a21bfc51e9b) 옵션이 추가되었다.

Aggregation function 중 approximate aggregation인 [APPROX_COUNT_DISTINCT](../part-03-sql-manual/17-built-in-function-references.md#4bd83f1213792549)가 추가되었다.

Statistics information function 인 [TABLE_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#b6629b53c0b75cd5), [INDEX_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#8ecc511dde1fe96e), [GSI_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#07153d77d1b51d4a) 가 추가되었다.

<a id="53df3045b84e8270"></a>
#### Object DDL

<a id="fb00b13e4b6258aa"></a>
##### SQL Object DDL

<a id="b317d9c9cf3e7c23"></a>
###### **ROLE**

Authorization 객체인 role에 대한 DDL 구문이 추가되었다.

- ROLE 생성
    - [CREATE ROLE](../part-03-sql-manual/19-sql-references-c-g.md#0d487ff524efb8bf)
- ROLE 제거
    - [DROP ROLE](../part-03-sql-manual/19-sql-references-c-g.md#84a501362442f591)
- ROLE 부여
    - [GRANT role TO](../part-03-sql-manual/19-sql-references-c-g.md#fd27b8c95b0f1bc2)
- ROLE 회수
    - [REVOKE role FROM](../part-03-sql-manual/20-sql-references-h-z.md#25b534416caec4de)

<a id="c402a562d247c639"></a>
###### **ANALYZE TABLE 수행 시 Histogram 정보 구축**

[ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#2c58b21ce5cb8f13)을 수행할 때 다음과 같은 histogram 정보를 구축할 수 있다.

- Height-balanced histogram
- Frequency histogram

Histogram 정보를 구축하려면 관련 프로퍼티를 활성화해야 한다.

- [HISTOGRAM_BALANCE_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#0646042872327a32)
- [HISTOGRAM_FREQUENCY_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#ef42f2f75da19f94)

<a id="b62304ff9ec3cc09"></a>
###### **ANALYZE TABLE 구문에 FOR COLUMN GROUPS 절 추가**

Column group 통계 정보를 구축할 수 있도록 [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#2c58b21ce5cb8f13) 구문에 FOR COLUMN GROUPS 절을 추가하였다.

<a id="09ed959d4ab61d16"></a>
###### **ANALYZE sampling 정확도 개선**

아래와 같은 기법을 도입하여 ANALYZE sampling 의 성능과 정확도를 개선하였다.

- Repeatable random sampling
- Approximate NUM_DISTINCT (Hyper log 알고리즘)
- Exponent 곡선에 의한 NUM_DISTINCT 보정

예를 들어, ANALYZE 샘플링 비율을 10%로 설정해도 TPC-H의 22개 모든 질의에 대해 전수조사 ANALYZE와 동일한 실행 계획이 생성된다.

<a id="6d6efa7d489ee2ca"></a>
###### **Audit Policy**

[CREATE AUDIT POLICY](../part-03-sql-manual/19-sql-references-c-g.md#079c12405d0687f7) 구문과 [ALTER AUDIT POLICY](../part-03-sql-manual/18-sql-references-a-b.md#e6d664ed42cb125a) 구문에 [&lt;role_audit_clause&gt;](../part-03-sql-manual/19-sql-references-c-g.md#b7a0a0fef8e44e9b) 구문이 추가되었다.

<a id="cf742bfa2cabb96f"></a>
###### **RENAME CHANGE TRACKING FILE**

[ALTER DATABASE RENAME CHANGE TRACKING FILE](../part-03-sql-manual/18-sql-references-a-b.md#86093b65db0319c4) 구문이 추가되었다.

<a id="5643abc945d54f0f"></a>
###### **ALTER INDEX COALESCE**

[ALTER INDEX COALESCE](../part-03-sql-manual/18-sql-references-a-b.md#ba3aecf4b34c844b)는 다른 ALTER 구문들과 동시에 실행할 수 없다. (단, 22c.1 버전에서는 가능하다.)

<a id="76477ac46b73fd90"></a>
###### **CHECK constraint**

CHECK 제약조건이 추가되었다.

- [CHECK 제약 조건](../part-03-sql-manual/19-sql-references-c-g.md#9d54718478517ebd)
- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#ce6ecbcf1ea593ea)
- [ALTER TABLE name ADD COLUMN](../part-03-sql-manual/18-sql-references-a-b.md#5bf457087cd2404f)
- [ALTER TABLE name ADD CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#b1bf02c95ebfb66d)

<a id="19fd137b9a82e898"></a>
###### **FOREIGN KEY constraint**

FOREIGN KEY 제약조건이 추가되었다.

- [FOREIGN KEY 제약 조건](../part-03-sql-manual/19-sql-references-c-g.md#254ccdad9ba898ff)
- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#ce6ecbcf1ea593ea)
- [ALTER TABLE name ADD COLUMN](../part-03-sql-manual/18-sql-references-a-b.md#5bf457087cd2404f)
- [ALTER TABLE name ADD CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#b1bf02c95ebfb66d)

<a id="dfe7f569766dcbcd"></a>
###### **&lt;constraint enforcement&gt; **

제약 조건을 활성화 또는 비활성화 할 수 있는 &lt;constraint enforcement&gt; 옵션으로 [ALTER TABLE name ALTER CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#75005eef58445700)가 추가되었다.

<a id="55ff831bb1bfcef4"></a>
###### **&lt;index enforcement&gt; **

인덱스를 활성화 또는 비활성화 할 수 있는 &lt;index enforcement&gt; 기능인 [ALTER INDEX name ENABLE/DISABLE](../part-03-sql-manual/18-sql-references-a-b.md#8c8f90f0415b3a2e)이 추가되었다.

<a id="a174eb2161de52cd"></a>
###### **ADD CONSTRAINT ON SCHEMA 권한 제거 **

ADD CONSTRAINT ON SCHEMA 권한이 제거되었다.

- 테이블 소유자의 ADD CONSTRAINT
    - CREATE TABLE을 수행하면 ALTER ON TABLE 권한이 부여된다.
    - ADD CONSTRAINT는 ALTER ON TABLE 권한으로 수행한다.
- 테이블 비소유자의 ADD CONSTRAINT
    - ALTER ON TABLE 권한 
    - 또는 ALTER TABLE ON SCHEMA 권한이 필요하다.
- ADD CONSTRAINT를 수행할 때 제약 조건의 소유자
    - Constraint 가 속한 table 의 소유자

<a id="e2b6660692fc96af"></a>
###### **CREATE USER 수행 시 user schema path 에서 PUBLIC 제거 **

다음과 같이 CREATE USER를 수행하면, user schema path에서 PUBLIC이 제거되도록 변경되었다.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1;
gSQL> 
SELECT auth_name
     , schema_name
     , search_order
  FROM dictionary_schema.dba_schema_path
 WHERE auth_name = 'U1'
; 

AUTH_NAME SCHEMA_NAME SEARCH_ORDER
--------- ----------- ------------
U1        U1                     1
```

22c 이하 버전과 동일하게 사용하고자 할 경우, 다음과 같이 schema path 를 조정한다.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1;
gSQL> ALTER USER u1 SCHEMA PATH ( u1, public );

gSQL> 
SELECT auth_name
     , schema_name
     , search_order
  FROM dictionary_schema.dba_schema_path
 WHERE auth_name = 'U1'
; 

AUTH_NAME SCHEMA_NAME SEARCH_ORDER
--------- ----------- ------------
U1        U1                     1
U1        PUBLIC                 2
```

<a id="0b4cf31adc615390"></a>
###### **ALTER TABLE name SET TRIGGER ORDER**

Table 에 생성한 trigger 들의 실행 순서를 변경하는 [ALTER TABLE name SET TRIGGER ORDER](../part-03-sql-manual/18-sql-references-a-b.md#e99539acedd7cb13) 구문이 추가되었다.

<a id="19873ecade46953e"></a>
###### **ALTER TABLE name REORGANIZE**

테이블을 물리적으로 재구성하는 [ALTER TABLE name REORGANIZE](../part-03-sql-manual/18-sql-references-a-b.md#b33b38d54cfadfd0) 구문이 추가되었다.

<a id="8d471c47d5c965bb"></a>
###### **&lt;shard divisor&gt; **

Online DDL 구문에서 사용하는 &lt;shard divisor&gt; 옵션이 &lt;scan partition&gt; 으로 변경되었다.

다음은 변경된 online DDL 구문들이다.

- [ALTER DATABASE MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#4752ea45b3668af4)
- [ALTER DATABASE REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#045abf2d149b6478)
- [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](../part-03-sql-manual/18-sql-references-a-b.md#b2d27be01aaaa9b7)
- [ALTER DATABASE SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#1620340d3358eb5b)
- [ALTER TABLE name MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#b64b6ca52ad7b811)
- [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#4dcbc8cc43487ef2)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](../part-03-sql-manual/18-sql-references-a-b.md#5f2f7d4e4bdedbe5)
- [ALTER TABLE name SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#baf7d0e8598b3f6a)

<a id="00e884ba6d61f4f8"></a>
###### **STORAGE 절의 MINSIZE 제거**

다음 DDL 구문에서는 STORAGE 절 내 MINSIZE 사용을 더 이상 지원하지 않는다.

- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#ce6ecbcf1ea593ea)
- [CREATE TABLE AS SELECT](../part-03-sql-manual/19-sql-references-c-g.md#092851c0db1d8a7a)
- [CREATE INDEX](../part-03-sql-manual/19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX name STORAGE](../part-03-sql-manual/18-sql-references-a-b.md#ba7154f8d22befe2)
- [ALTER INDEX name REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#56aed70ce2b90a69)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#ef80852f02ba2cc6)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#71b8f952e7d629e8)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#5941392c8f076e6f)

<a id="d8c2d827f558c9cb"></a>
###### **INDEX STORAGE 절에서 MAXSIZE 제거**

다음 DDL 구문에서는 STORAGE 절 내 MAXSIZE 사용을 더 이상 지원하지 않는다.

- [CREATE INDEX](../part-03-sql-manual/19-sql-references-c-g.md#1b99962ed891aa4f)
- [ALTER INDEX name STORAGE](../part-03-sql-manual/18-sql-references-a-b.md#ba7154f8d22befe2)
- [ALTER INDEX name REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#56aed70ce2b90a69)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#ef80852f02ba2cc6)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#71b8f952e7d629e8)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#5941392c8f076e6f)

<a id="96411af67bf6df89"></a>
##### Cluster Object DDL

<a id="90f7299e33cee57a"></a>
###### **ALTER TABLE ALTER GLOBAL SECONDARY INDEX COALESCE**

[ALTER TABLE ALTER GLOBAL SECONDARY INDEX COALESCE](../part-03-sql-manual/18-sql-references-a-b.md#ea78d0d51ae40ba7) 구문은 다른 ALTER 구문들과 동시에 실행할 수 없다. (단, 22c.1 버전에서는 가능하다.)

<a id="ac00784d5105b079"></a>
#### SQL Language

<a id="1f27bc728d7fef7e"></a>
##### DML

<a id="9d62626a4fc91c9d"></a>
###### **MERGE**

MERGE 구문이 추가되었다.  
자세한 내용은 [MERGE](../part-03-sql-manual/20-sql-references-h-z.md#bc136bf193bf403b)를 참조한다.

<a id="c737eae7e20d10be"></a>
###### **APPEND INSERT **

APPEND INSERT 방식으로 데이터를 추가하는 기능과 이를 지원하는 힌트가 추가되었다.  
자세한 내용은 [APPEND INSERT 방식의 데이터 추가](../part-03-sql-manual/12-sql-languages.md#9fdab7fa44252736)를 참조한다.

<a id="cfae691d392e221b"></a>
###### **DELETE FROM의 &lt;local shard limit&gt; 절**

DELETE FROM 구문에 데이터 절체를 위한 &lt;local shard limit clause&gt; 가 추가되었다.  
자세한 내용은 [&lt;local shard limit clause&gt;](../part-03-sql-manual/19-sql-references-c-g.md#d23d83f814803841)  를 참조한다.

<a id="c3d7116f3b31af6e"></a>
##### Query

<a id="a1d56657ae135080"></a>
###### [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#14659507262e5348)**의 &lt;grouping element&gt; 확장 지원**

&lt;grouping element&gt;에 ROLLUP, CUBE, GROUPING SET가 추가되었다.  
자세한 내용은 [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#14659507262e5348)를 참조한다.

<a id="247e289f468149d6"></a>
###### **group by clause에서 select list alias 참조 지원**

&lt;grouping column reference&gt;에 select list alias가 추가되었다.  
자세한 내용은 [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#14659507262e5348)를 참조한다.

<a id="098bd464046f7226"></a>
###### **Pivot 절**

Row를 column으로 변환하는 cross table을 기술하기 위한 pivot 절이 추가되었다.   
자세한 내용은 [pivot clause](../part-03-sql-manual/20-sql-references-h-z.md#fc4e37ea9e697ac1)를 참조한다.

<a id="70fa187ae4db80d1"></a>
###### **Unpivot 절**

Column을 row로 변환하는 cross table을 기술하기 위한 unpivot 절이 추가되었다.   
자세한 내용은 [unpivot clause](../part-03-sql-manual/20-sql-references-h-z.md#e4262e566d20f76e)를 참조한다.

<a id="5f97b7d7c180e824"></a>
###### **Sample 절**

테이블의 전체 데이터를 처리하지 않고 일부 row만 무작위로 추출하기 위한 sample 절이 추가되었다.  
자세한 내용은 [sample clause](../part-03-sql-manual/20-sql-references-h-z.md#778d71bbe6c00108)를 참조한다.

<a id="76df59cf203f7dad"></a>
###### **Aggregation Filter**

[Aggregate Function](../part-03-sql-manual/11-sql-elements.md#67ffc000313e5858)에 FILTER 기능이 추가되었다.

[JSON aggregate Constructor](../part-03-sql-manual/11-sql-elements.md#900d89639c906cbd)에 FILTER 기능이 추가되었다.

<a id="4ad138ab70d0835e"></a>
###### **SQL Hint 추가**

다음과 같은 SQL hint가 추가되었다.

- [&lt;window hints&gt;](../part-03-sql-manual/15-sql-tuning.md#3a7dfb615d23e291)
- [&lt; union all driver hints &gt;](../part-03-sql-manual/15-sql-tuning.md#d5ea01efbed17bab)

<a id="6c8596d9ba707906"></a>
##### Control Language

세션에서 수행되는 작업을 취소할 수 있는 [ALTER SYSTEM CANCEL SESSION](../part-03-sql-manual/18-sql-references-a-b.md#a9639e899e14c803) 구문이 추가되었다.

<a id="ed47e6197dfee8da"></a>
###### **SET ROLE**

현재 session의 role을 변경할 수 있는 [SET ROLE role_name](../part-03-sql-manual/20-sql-references-h-z.md#0af7a3d47e76664e) 구문이 추가되었다.

<a id="49975d9f573ac98f"></a>
#### PSM Language

<a id="997f93d46da04b91"></a>
##### External Routine

사용자가 작성한 C 프로그램을 실행할 수 있는 [External Routine](../part-04-sql-psm-manual/28-external-routine.md#5edbddf52d93deaf)이 추가되었다.

<a id="aeebaf6edad978d5"></a>
##### Triggger

특정 테이블에서 DML이 수행될 때마다 자동으로 실행될 동작을 정의하는 [Trigger](../part-04-sql-psm-manual/29-trigger.md#0363dbb16b7f9218) 객체가 추가되었다.

<a id="bd413d954c83449f"></a>
##### PL Statement

External C Function과 Routine 정보를 대응시키는 [Call Specification](../part-04-sql-psm-manual/30-psm-language-element-references.md#1663813aaf9c3eb4) 구문이 추가되었다.

<a id="611e1605c963a619"></a>
##### Library 객체 DDL

- [CREATE LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#e6a29c79119e1af1)
- [DROP LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#11be420b5d5517c9)

<a id="21d4db6cad731e3d"></a>
##### Trigger 객체 DDL

- [CREATE TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#c36270132fc5138d)
- [DROP TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#405a8fa6b4a11ae3)
- [ALTER TRIGGER name COMPILE](../part-04-sql-psm-manual/31-psm-sql-references.md#7ef86e0333181a4e)
- [ALTER TRIGGER name ENABLE/DISABLE](../part-04-sql-psm-manual/31-psm-sql-references.md#f14d8e926a633165)
- [ALTER TRIGGER name RENAME TO](../part-04-sql-psm-manual/31-psm-sql-references.md#ae1a37f358aeb5db)

<a id="59abdeece5b3fe30"></a>
##### Built-in Package

사용자가 필요에 따라 package 를 설치할 수 있도록 built-in package SQL 이 추가되었다.

기존 22c 이하에서 built-in package 를 사용하던 사용자는 아래와 같이 built-in package 를 설치해야 한다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="fc823c83c8905f8d"></a>
### API

<a id="6a391c7b77e08dda"></a>
#### ODBC

연결 속성 ALTERNATE_LOCATORS가 ALTERNATE_LOCATOR로 변경되었다.

구조체 SQL_LONG_VARIABLE_LENGTH_STRUCT의 필드 구성이 변경되었다. 버퍼 arr의 용량을 나타내는 buf_len (byte 단위)과 실제 데이터 길이를 나타내는 len (byte 단위)으로 역할이 분리되었다. ([비표준 데이터 타입](../part-05-developer-manual/34-odbc.md#91ee28076bf86d51))

<a id="1ddd5c51500c7689"></a>
#### JDBC

연결 속성 ALTERNATE_LOCATORS가 ALTERNATE_LOCATOR로 변경되었다.

연결 속성 commit_write_mode가 추가되었다.

<a id="4b6aafbc8ddbd424"></a>
#### Embedded SQL

<a id="0a9a733eba7fdb21"></a>
##### Precompiler Option

gpec에 [--parse](../part-05-developer-manual/36-embedded-sql.md#49761b68c953cb6c) 옵션이 추가되었다.

<a id="df50446336216358"></a>
##### Embedded SQL 전용 구문

GET GROUPID 구문이 GET CLUSTER_GROUP_ID로 변경되었다.

<a id="cf39f570b350b4f1"></a>
##### Host Variable Data Type

구조체 SQL_LONG_VARIABLE_LENGTH_STRUCT의 필드 구성이 변경되었다. 버퍼 arr의 용량을 나타내는 buf_len (byte 단위)과 실제 데이터 길이를 나타내는 len (byte 단위)으로 역할이 분리되었다. ([LONG VARCHAR](../part-05-developer-manual/36-embedded-sql.md#6f9127f189a796e4))

VARCHAR 또는 VARBINARY 변수를 IN 또는 IN_OUT 매개변수로 사용할 경우, 내부적으로 해당 변수의 길이 (len)에 음수 값이 설정되면 오류가 발생하도록 오류 처리 방식이 변경되었다.

<a id="5f12dea8833bff40"></a>
##### Dynamic SQL

Dynamic SQL Method 4를 지원한다.

<a id="86960f4092b677bf"></a>
#### PDO

변동 사항 없음

<a id="ce27b23495c85c93"></a>
#### PyDBC

<a id="f3618347a3c67a68"></a>
##### 설치 및 패키징

Python 3 패키지에 pyproject.toml 기반 빌드와 wheel/sdist 패키징을 적용하였다.

Python 3 패키지에 IDE 및 정적 타입 검사 도구에서 사용할 수 있는 pygoldilocks.pyi 타입 stub을 추가하였다.

<a id="10b0fc96900d3003"></a>
##### connection

Python 3에서 문자 데이터의 codec을 설정하기 위한 setencoding() 및 setdecoding() 을 지원한다.

Python 3에서 connection.messages, character_set_name(), 그리고 SQL 타입별 output converter를 지원한다.

대용량 문자 및 바이너리 매개변수 처리를 위해 connection.maxwrite를 지원한다.

<a id="6b2b08c282870a63"></a>
##### Result set 및 PSM

Procedure가 반환하는 여러 result set을 cursor.nextset()으로 순차적으로 처리할 수 있다. 다음 result set이 있으면 True, 모두 처리한 경우 None을 반환한다.

procedureColumns()를 추가하여 procedure의 IN, OUT 및 INOUT parameter metadata를 조회할 수 있다.

fetchval(), cursor iterator 및 statement cancel 기능을 지원한다.

cursor.lastrowid는 지원되지 않는 값이므로 항상 None을 반환한다.

<a id="f2226f42e53ea87d"></a>
##### Data Type

Python 3에서 TIME WITH TIME ZONE과 TIMESTAMP WITH TIME ZONE을 UTC offset이 보존된 timezone-aware datetime 객체로 반환한다.

Python 2에서는 time zone 타입을 문자열로 반환한다.

TIME 및 TIMESTAMP 의 fractional second 와 microsecond 변환 처리가 개선되었다.

NUMBER, NUMERIC 및 DECIMAL의 precision/scale 처리가 개선되었으며, NaN 및 Infinity 와 같은 decimal 값은 허용하지 않는다.

<a id="9c90fa070805b1bb"></a>
#### SQLAlchemy

SQLAlchemy 1.4 및 2.0을 지원한다.

<a id="55631c28ff64a532"></a>
#### Hibernate

Hibernate version 6, 7, 8 을 지원한다.

<a id="acc7b91c830cddc0"></a>
### Utility

<a id="05418e17830ed7af"></a>
#### gcreatedb

변동 사항 없음

<a id="218d744a28254a93"></a>
#### glsnr

변동 사항 없음

<a id="04789b2223a7230b"></a>
#### gsql/gsqlnet

<a id="e92160bc10a64ea4"></a>
##### ROLE

Role 객체와 관련된 DDL 구문을 export 하기 위해 [`\ddl_role`](../part-06-utility-manual/44-gsql-gsqlnet-interactive-sql-tool.md#30ba33e56e23343e) 기능이 추가되었다.

<a id="1459b4bfc5f5100d"></a>
##### TRIGGER

Trigger 객체와 관련된 DDL 구문을 export 하기 위해 [`\ddl_trigger`](../part-06-utility-manual/44-gsql-gsqlnet-interactive-sql-tool.md#99c01d5516325b59) 기능이 추가되었다.

<a id="dd601301d7fbb4c5"></a>
#### gloader/gloadernet

directio-size 옵션이 deprecated 되었다.

[APPEND INSERT 방식](../part-03-sql-manual/12-sql-languages.md#9fdab7fa44252736)의 데이터 추가 기능이 추가되면서, 이를 지원하기 위한 옵션 (merge, skip_index_maintenance, nologging) 도 함께 추가되었다.

<a id="2c9514dfd1417b59"></a>
#### gdump

Log 옵션 이름이 redo_log 로 변경되었다.

Data 옵션 이름이 datafile 로 변경되었다.

<a id="10c4c263237cd0f2"></a>
#### tablediff

변동 사항 없음

<a id="51f98c231920eec6"></a>
#### gsyncher

변동 사항 없음

<a id="34aa40a7b262be3c"></a>
#### gmon

변동 사항 없음

<a id="84ac8ce42b5a0fd5"></a>
#### gtrclogger

변동 사항 없음

<a id="c8fb86bfd77273fb"></a>
#### glocator

Configuration property 중에 ALTERNATE_LOCATORS가 ALTERNATE_LOCATOR로 변경되었다.

glocator 다중화는 이중화로 변경되었다.

sync 옵션에 인자를 사용하지 않도록 변경되었다.

<a id="f70801599fca38bf"></a>
#### gagent

Configuration property 중에 ALTERNATE_LOCATORS가 ALTERNATE_LOCATOR로 변경되었다.

<a id="cb1542c7fdbd46e6"></a>
#### gloctl

변동 사항 없음

<a id="80d1972663bc3c3e"></a>
### Replication

<a id="f3ec635881eeb0e7"></a>
#### cyclone

Oracle, DB2, MySQL, Tibero 등 타 DB로 데이터를 이전하는 기능을 추가하였다.

Heartbeat protocol을 data protocol과 분리하여 구성하였다.

<a id="ddf086a6f68d6339"></a>
#### logmirror

변동 사항 없음

<a id="4e77ed01b498b81b"></a>
#### cymon

변동 사항 없음

<a id="3b3a186f02c68c0b"></a>
#### cyfile

변동 사항 없음

---

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
