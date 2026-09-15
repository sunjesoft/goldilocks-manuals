<a id="78ed04587a99cbee"></a>

# 4. What's New

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/78ed04587a99cbee)  
> 태그: `21c.1_35_tag`

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<a id="2dc8e2c159137e7d"></a>
## Feature Matrix

본 장에서는 각 major version 별로 추가된 주요 기능들에 대해 간략히 설명한다.

<a id="78fc48100ce62636"></a>
### Architecture

<a id="427dcdbb05165b13"></a>
#### System Architecture

System architecture에 대한 feature matrix는 다음과 같다.

**System architecture의 feature matrix**

<a id="9de466f775494324"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| Shared Nothing Cluster | X | O | O | O |
| DA (Direct Attach) | O | O | O | O |
| JDBC DA (Direct Attach) | X | O | O | O |
| C/S (Client/Server) Dedicated | O | O | O | O |
| C/S (Client/Server) Shared | O | O | O | O |
| multi-process applications | O | O | O | O |
| multi-threaded applications | O | O | O | O |
| Linux platform | O | O | O | O |
| HP platform | O | O | O | O |
| AIX platform | O | O | O | O |
| Windows Client Platform | O | O | O | O |
| CDC(Change Data Capture) replication | O | O | O | O |
| CDC replication with log mirror | O | O | O | O |
| multi-level start up | O | O | O | O |
| parallel database loading | O | O | O | O |
| parallel index build | O | O | O | O |
| SQL plan cache | O | O | O | O |
| IPC | X | X | X | O |

<a id="b7c758066bce5961"></a>
#### Storage Internal

Storage internal에 대한 feature matrix는 다음과 같다.

**Storage internal의 feature matrix**

<a id="7512de45ca28eaa6"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| memory dictionary tablespace | O | O | O | O |
| memory data tablespace | O | O | O | O |
| memory undo tablespace | O | O | O | O |
| memory temporary tablespace | O | O | O | O |
| memory bitmap data segment | O | O | O | O |
| memory bitmap undo segment | O | O | O | O |
| memory bitmap instant segment | O | O | O | O |
| memory heap table | O | O | O | O |
| memory instant table | O | O | O | O |
| memory B-tree index | O | O | O | O |
| memory instant B-tree | O | O | O | O |
| memory instant hash | O | O | O | O |
| global secondary index | X | O | O | O |
| disk data tablespace | X | X | O | O |
| disk bitmap data segment | X | X | O | O |
| disk B-tree index | X | X | O | O |
| disk global secondary index | X | X | O | O |

<a id="c172c010c5e4c9cc"></a>
#### Transaction Control

Transaction control에 대한 feature matrix는 다음과 같다.

**Transaction control의 feature matrix**

<a id="0acbd8b86cdeb70a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| CDS(Concurrency Data Store) database mode | O | O | O | O |
| TDS(Transactional Data Store) database mode | O | O | O | O |
| read-only database | O | O | O | O |
| read/write database | O | O | O | O |
| flat transaction | O | O | O | O |
| distributed transaction | O | O | O | O |
| read-only transaction | O | O | O | O |
| read/write transaction | O | O | O | O |
| READ COMMITTED isolation level | O | O | O | O |
| SERIALIZABLE isolation level with SELECT FOR UPDATE | O | O | O | O |
| MVCC(Multi Version Concurrency Control) | O | O | O | O |
| multi-version read consistency | O | O | O | O |
| multi-statement consistent read | O | O | O | O |
| implicit lock for DML | O | O | O | O |
| writer don't blocks readers | O | O | O | O |
| row-level locking | O | O | O | O |
| deadlock detection | O | O | O | O |
| deadlock resolution | O | O | O | O |
| lock granularity | O | O | O | O |
| read lock | O | O | O | O |
| write lock | O | O | O | O |
| intention lock | O | O | O | O |
| WAL(Write Ahead Logging) | O | O | O | O |
| repeat history | O | O | O | O |
| restart recovery | O | O | O | O |
| circular logging | O | O | O | O |
| buffered logging | O | O | O | O |
| logging group | O | O | O | O |
| supplemental logging | O | O | O | O |
| mirrored logging | O | O | O | O |
| synchronous commit | O | O | O | O |
| asynchronous commit | O | O | O | O |
| grouped commit | O | O | O | O |
| total rollback | O | O | O | O |
| implicit statement rollback | O | O | O | O |
| savepoint management | O | O | O | O |

<a id="6d8a1e4377088f40"></a>
#### Backup & Recovery

Backup & recovery에 대한 feature matrix는 다음과 같다.

**Backup & recovery의 feature matrix**

<a id="ad298b69188faeca"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| off-line backup | O | O | O | O |
| on-line backup | O | O | O | O |
| full backup | O | O | O | O |
| incremental backup | O | O | O | O |
| complete recovery | O | O | O | O |
| incomplete recovery | O | O | O | O |
| auto instance recovery | O | O | O | O |
| tablespace recovery | O | O | O | O |
| file recovery | O | O | O | O |
| change tracking | X | X | O | O |

<a id="8139a50bf1ea21f0"></a>
#### Database Information

<a id="326759c319624885"></a>
##### DICTIONARY_SCHEMA 스키마

DICTIONARY_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

<a id="4ac21ea766a1f09a"></a>
<table class="table column_count_6"><caption>DICTIONARY_SCHEMA schema의 feature matrix</caption><thead><tr><th class="to_center"><div>계열</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="56"><div>ALL_ 계열 view</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="48"><div>DBA_ 계열 view</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="53"><div>USER_ 계열 view</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="15"><div>기타 view</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="f30b29dba5ea5e3f"></a>
##### INFORMATION_SCHEMA 스키마

INFORMATION_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**INFORMATION_SCHEMA schema의 feature matrix**

<a id="a805a57d7ab20acb"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| COLUMNS | O | O | O | O |
| COLUMN_PRIVILEGES | O | O | O | O |
| CONSTRAINT_COLUMN_USAGE | O | O | O | O |
| CONSTRAINT_TABLE_USAGE | O | O | O | O |
| INFORMATION_SCHEMA_CATALOG_NAME | O | O | O | O |
| KEY_COLUMN_USAGE | O | O | O | O |
| MODULES | X | X | O | O |
| MODULE_BODY | X | X | O | O |
| MODULE_BODY_MODULE_USAGE | X | X | O | O |
| MODULE_BODY_ROUTINE_USAGE | X | X | O | O |
| MODULE_BODY_SEQUENCE_USAGE | X | X | O | O |
| MODULEBODY_TABLE_USAGE | X | X | O | O |
| MODULE_MODULE_USAGE | X | X | O | O |
| MODULE_PRIVILEGES | X | X | O | O |
| MODULE_ROUTINE_USAGE | X | X | O | O |
| MODULE_SEQUENCE_USAGE | X | X | O | O |
| MODULE_TABLE_USAGE | X | X | O | O |
| PARAMETERS | X | O | O | O |
| REFERENTIAL_CONSTRAINTS | O | O | O | O |
| ROUTINES | X | O | O | O |
| ROUTINE_MODULE_USAGE | X | X | O | O |
| ROUTINE_PRIVILEGES | X | O | O | O |
| ROUTINE_ROUTINE_USAGE | X | O | O | O |
| ROUTINE_SEQUENCE_USAGE | X | O | O | O |
| ROUTINE_TABLE_USAGE | X | O | O | O |
| SCHEMATA | O | O | O | O |
| SEQUENCES | O | O | O | O |
| SQL_FEATURES | O | O | O | O |
| SQL_IMPLEMENTATION_INFO | O | O | O | O |
| SQL_PACKAGES | O | O | O | O |
| SQL_PARTS | O | O | O | O |
| SQL_SIZING | O | O | O | O |
| STATISTICS | O | O | O | O |
| TABLES | O | O | O | O |
| TABLE_CONSTRAINTS | O | O | O | O |
| TABLE_PRIVILEGES | O | O | O | O |
| USAGE_PRIVILEGES | O | O | O | O |
| VIEWS | O | O | O | O |
| VIEW_MODULE_USAGE | X | X | O | O |
| VIEW_ROUTINE_USAGE | X | O | O | O |
| VIEW_TABLE_USAGE | O | O | O | O |

<a id="38283a337dd48b42"></a>
##### PERFORMANCE_VIEW_SCHEMA 스키마

PERFORMANCE_VIEW_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**PERFORMANCE_VIEW_SCHEMA schema의 feature matrix**

<a id="203167eea0d3a4ac"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| GV$____ | X | O | O | O |
| V$AGABLE_INFO | X | O | O | O |
| V$ARCHIVELOG | O | O | O | O |
| V$AUDITABLE_DB_PRIVILEGES | X | O | O | O |
| V$AUDITABLE_SYSTEM_ACTIONS | X | O | O | O |
| V$BACKUP | O | O | O | O |
| V$BALANCER | O | O | O | O |
| V$BCH | X | X | O | O |
| V$BUFFER_STAT | X | X | O | O |
| V$CLUSTER_DISPATCHER | X | O | O | O |
| V$CLUSTER_LOCATION | X | O | O | O |
| V$CLUSTER_MEMBER | X | O | O | O |
| V$COLUMNS | O | O | O | O |
| V$CONTROLFILE | O | O | O | O |
| V$DATAFILE | O | O | O | O |
| V$DB_CHANGE_TRACKING | X | X | O | O |
| V$DB_FILE | O | O | O | O |
| V$DISPATCHER | O | O | O | O |
| V$ERROR_CODE | O | O | O | O |
| V$GLOBAL_TRANSACTION | O | O | O | O |
| V$JOURNALING | X | O | O | O |
| V$INCREMENTAL_BACKUP | O | O | O | O |
| V$INSTANCE | O | O | O | O |
| V$KEYWORDS | O | O | O | O |
| V$LATCH | O | O | O | O |
| V$LOCK_WAIT | O | O | O | O |
| V$LOCKED_OBJECT | X | X | O | O |
| V$LOGFILE | O | O | O | O |
| V$PLAN_HISTORY | X | X | X | O |
| V$PLAN_HISTORY_LATEST | X | X | X | O |
| V$PROCESS_MEM_STAT | O | O | O | O |
| V$PROCESS_SQL_STAT | O | O | O | O |
| V$PROCESS_STAT | O | O | O | O |
| V$PROPERTY | O | O | O | O |
| V$PSM_RESERVED_WORDS | X | O | O | O |
| V$QUEUE | O | O | O | O |
| V$RESERVED_WORDS | O | O | O | O |
| V$SESSION | O | O | O | O |
| V$SESSION_AUDIT | X | O | O | O |
| V$SESSION_CONNECT_INFO | O | O | O | O |
| V$SESSION_EVENT | X | O | O | O |
| V$SESSION_MEM_STAT | O | O | O | O |
| V$SESSION_MEM_USAGE | X | X | X | O |
| V$SESSION_SQL_STAT | O | O | O | O |
| V$SESSION_STAT | O | O | O | O |
| V$SESSION_WAIT | X | O | O | O |
| V$SHARED_MODE | O | O | O | O |
| V$SHARED_SERVER | O | O | O | O |
| V$SHM_SEGMENT | O | O | O | O |
| V$SPROPERTY | O | O | O | O |
| V$SQLFN_METADATA | O | O | O | O |
| V$SQL_CACHE | O | O | O | O |
| V$SQL_COMMAND | X | O | O | O |
| V$SQL_HISTORY | X | O | O | O |
| V$STATEMENT | O | O | O | O |
| V$SYSTEM_EVENT | X | O | O | O |
| V$SYSTEM_MEM_STAT | O | O | O | O |
| V$SYSTEM_SQL_STAT | O | O | O | O |
| V$SYSTEM_STAT | O | O | O | O |
| V$TABLES | O | O | O | O |
| V$TABLESPACE | O | O | O | O |
| V$TABLESPACE_STAT | X | O | O | O |
| V$TRANSACTION | O | O | O | O |
| V$WAIT_EVENT_CLASS_NAME | X | O | O | O |
| V$WAIT_EVENT_NAME | X | O | O | O |
| V$XA_TRANSATION | X | O | O | O |

<a id="40d70df1d299474f"></a>
#### Server Property

Server property에 대한 feature matrix는 다음과 같다.

**Server property의 feature matrix**

<a id="7bfb649692dc8ede"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| AGING_INTERVAL | O | O | O | O |
| AGING_PLAN_INTERVAL | O | O | O | O |
| ARCHIVE_LOG_THROTTLING | X | X | X | O |
| ARCHIVELOG_DIR | O | X | X | X |
| ARCHIVELOG_DIR_1 ~ DIR_10 | O | O | O | O |
| ARCHIVELOG_FILE | O | O | O | O |
| ARCHIVELOG_MODE | O | O | O | O |
| BACKUP_DIR_1 ~ DIR_10 | O | O | O | O |
| BLOCK_READ_COUNT | O | O | O | O |
| BROADCAST_INDEX_REBUILD_PROTOCOL | X | X | X | O |
| BROADCAST_REBALANCE_PROTOCOL | X | X | O | O |
| BUFFER_CACHE_SIZE | X | X | O | O |
| BUFFER_CHECKPOINT_LIST_COUNT | X | X | O | X |
| BUFFER_FLUSH_THREADS | X | X | O | X |
| BUFFER_FLUSHING_INTERVAL | X | X | O | X |
| BUFFER_FREE_LIST_COUNT | X | X | O | O |
| BUFFER_HASH_BUCKETS | X | X | O | O |
| BUFFER_HOT_REGION_CRITERIA | X | X | O | O |
| BUFFER_HOT_REGION_PERCENT | X | X | O | O |
| BUFFER_LRU_LIST_COUNT | X | X | O | O |
| BUFFER_MULTIPAGE_READ_COUNT | X | X | O | O |
| BUFFER_PREFETCH_PAGE_COUNT | X | X | X | O |
| BULK_IO_PAGE_COUNT | O | O | O | O |
| CDISPATCHER_HOT_POLICY_INTERVAL | X | O | O | O |
| CDISPATCHER_LOCKLESS_THREADS | X | X | O | O |
| CDISPATCHER_SOCKET_BUFFER_SIZE | X | O | O | O |
| CDISPATCHER_THREADS | X | O | O | O |
| CHANGE_TRACKING | X | X | O | O |
| CHANGE_TRACKING_EXTENT_SIZE | X | X | O | O |
| CHANGE_TRACKING_FILE | X | X | O | O |
| CHAR_LENGTH_UNITS | O | O | O | O |
| CHARACTER_SET | O | O | O | O |
| CHECK_DEDICATE_CONNECTION_INTERVAL | X | O | O | O |
| CHECK_DEDICATE_SOCKET | X | X | X | X |
| CLIENT_MAX_COUNT | O | O | O | O |
| CLIENT_NUMA_POLICY | X | O | O | O |
| CLOSE_PSM_CHILD_STMTS | X | O | O | O |
| CLUSTER_ASYNC_COMMIT | X | O | O | O |
| CLUSTER_ASYNC_REPLICATION | X | O | O | O |
| CLUSTER_CM_BUFFER_COUNT | X | O | O | O |
| CLUSTER_CM_BUFFER_SIZE | X | O | O | O |
| CLUSTER_CM_READ_BUFFER_SIZE | X | O | O | O |
| CLUSTER_COMMIT_SLAVES | X | O | O | O |
| CLUSTER_COMMIT_STREAM_ISOLATION | X | O | O | O |
| CLUSTER_CONNECTION | X | O | O | O |
| CLUSTER_CONNECTION_TIMEOUT_SEC | X | O | O | O |
| CLUSTER_DATA_SYNC_SERVERS | X | O | O | O |
| CLUSTER_DEADLOCK_TIMEOUT | X | X | O | O |
| CLUSTER_DISPATCHER_IN_QUEUE_SIZE | X | O | O | O |
| CLUSTER_DISPATCHER_NUMA_STREAM_MAP | X | O | O | O |
| CLUSTER_DISPATCHER_OUT_QUEUE_SIZE | X | O | O | O |
| CLUSTER_HEARTBEAT_INTERVAL | X | O | O | O |
| CLUSTER_HEARTBEAT_RETRY_COUNT | X | O | O | O |
| CLUSTER_IGNORE_INACTIVE_MEMBER | X | O | O | O |
| CLUSTER_MAX_PACKET_SIZE | X | O | O | O |
| CLUSTER_MAX_PAYLOAD_SIZE | X | O | O | O |
| CLUSTER_PACKET_ALLOCATION_TIMEOUT | X | O | O | O |
| CLUSTER_SERVER_RESPONSE_QUEUE_SIZE | X | O | O | O |
| CLUSTER_SESSION_HASH_BUCKETS | X | X | O | O |
| CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY | X | O | O | O |
| CLUSTER_SPLIT_BRAIN_RETRY_COUNT | X | O | O | O |
| COMMITTER_HOT_POLICY_INTERVAL | X | O | O | O |
| CONTROL_FILE_0 ~ FILE_7 | O | O | O | O |
| CONTROL_FILE_COUNT | O | O | O | O |
| CONTROL_FILE_TEMP_NAME | O | O | O | O |
| COORDINATOR_COMMIT_WRITE_MODE | X | O | O | O |
| CSERVERS | X | O | O | O |
| DA_CLIENT_NUMA_MODE | X | O | O | O |
| DATA_STORE_MODE | O | O | O | O |
| DATABASE_ACCESS_MODE | O | O | O | O |
| DATABASE_INSTANCE_NAME | X | O | O | O |
| DDL_AUTOCOMMIT | O | O | O | O |
| DDL_LOCK_TIMEOUT | O | O | O | O |
| DEADLOCK_PRIORITY | X | X | O | O |
| DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION | X | O | O | O |
| DEFAULT_INDEX_LOGGING | O | O | X | X |
| DEFAULT_INDEX_PCTFREE | X | O | O | O |
| DEFAULT_INITRANS | O | O | O | O |
| DEFAULT_MAXTRANS | O | O | O | O |
| DEFAULT_PCTFREE | O | O | O | O |
| DEFAULT_PCTUSED | O | O | O | O |
| DEFAULT_REMOVAL_BACKUP_FILE | O | O | O | O |
| DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST | O | O | O | O |
| DEFAULT_SHARDING | X | O | O | O |
| DISABLE_DDL | X | X | X | O |
| DISABLE_DDL_CDC_GIVEUP | O | O | O | O |
| DISABLE_SERIAL_DDL | X | X | X | O |
| DISABLE_UPDATE_PK_CDC_GIVEUP | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE | X | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL | X | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME | X | O | O | O |
| DISPATCHERS | O | O | O | O |
| DISPATCHER_CM_BUFFER_SIZE | O | O | O | O |
| DISPATCHER_CM_UNIT_SIZE | O | O | O | O |
| DISPATCHER_CONNECTIONS | O | O | O | O |
| DISPATCHER_HOT_POLICY_INTERVAL | X | O | O | O |
| DISPATCHER_LOAD_BALANCING | X | O | O | O |
| DISPATCHER_NUMA_STREAM_MAP | X | O | O | O |
| DISPATCHER_QUEUE_SIZE | O | O | O | O |
| DISPATCHER_REQUEST_MINI_QUEUE_COUNT | X | O | O | O |
| DISPATCHER_RESPONSE_MINI_QUEUE_COUNT | X | O | O | O |
| EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY | X | X | X | O |
| FETCH_FAILOVER | X | O | O | O |
| GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY | X | O | O | O |
| GLOBAL_JOURNAL_BUFFER_SIZE | X | O | O | O |
| GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE | X | O | O | O |
| GLOBAL_PROPERTY_LOCK_TIMEOUT | X | O | O | O |
| GLOBAL_TRANSACTION_COMMIT_WRITE_MODE | X | O | O | O |
| GLOBAL_TRANSACTION_ISOLATION_SCOPE | X | O | O | O |
| GLOBAL_TRANSACTION_LOG_DIR | X | O | O | O |
| GLOBAL_TRANSACTION_LOG_FILE_SIZE | X | O | O | O |
| GMASTER_NUMA_NODE | X | O | O | O |
| GMON_AUTOSTART | X | O | O | O |
| HINT_ERROR | O | O | O | O |
| IDLE_TIMEOUT | O | O | O | O |
| IN_DOUBT_DECISION | O | O | O | O |
| IN_KEY_RANGE_ARRAY_COUNT | X | X | O | O |
| INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE | X | X | O | O |
| INDEX_BUILD_PARALLEL_FACTOR | O | O | O | O |
| INDEX_LOGGING_THROTTLING | X | X | X | O |
| INDEX_REBUILD_BLOCK_READ_COUNT | X | X | O | O |
| INDEX_TREE_MERGE_PARALLEL_FACTOR | X | O | O | O |
| INST_ALLOCATOR_COUNT | X | O | O | O |
| INST_HASH_TABLE_BUCKET_MAX_COUNT | X | X | X | O |
| INST_TABLE_BLOCK_SIZE | X | O | O | O |
| IPC_CHANNEL_COUNT | X | X | X | O |
| JOURNAL_TEMP_DIR | X | O | O | O |
| KEEPALIVE_IDLE_TIME | O | O | O | O |
| LOCAL_CLUSTER_MEMBER | X | O | O | O |
| LOCAL_CLUSTER_MEMBER_HOST | X | O | O | O |
| LOCAL_CLUSTER_MEMBER_PORT | X | O | O | O |
| LOCAL_JOURNAL_BUFFER_SIZE | X | O | O | O |
| LOCATION_FILE | X | O | O | O |
| LOCATOR_QUERY_TIMEOUT | X | O | O | O |
| LOCK_HASH_TABLE_SIZE | O | O | O | O |
| LOCKLESS_CSERVERS | X | X | O | O |
| LOG_BLOCK_SIZE | O | O | O | O |
| LOG_BUFFER_SIZE | O | O | O | O |
| LOG_DIR | O | O | O | O |
| LOG_FILE_SIZE | O | O | O | O |
| LOG_GROUP_COUNT | O | O | O | O |
| LOG_MIRROR_MODE | O | O | O | O |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | O | O | O | O |
| LOG_MIRROR_TIMEOUT | O | O | O | O |
| LOG_SYNC_INTERVAL | O | O | O | O |
| LOG_SYNC_INTERVAL_MSEC | X | O | O | O |
| MAX_GROUP_COUNT | X | O | O | O |
| MAX_JOURNAL_FILE_SIZE | X | O | O | O |
| MAX_NODE_COUNT | X | O | O | O |
| MAXIMUM_CONCURRENT_ACTIVITIES | O | O | O | O |
| MAXIMUM_FILE_CACHE_SIZE | X | X | X | O |
| MAXIMUM_FLANGE_COUNT | X | O | O | O |
| MAXIMUM_FLUSH_BUFFER_PAGE_COUNT | X | X | X | O |
| MAXIMUM_FLUSH_LOG_BLOCK_COUNT | O | O | O | O |
| MAXIMUM_FLUSH_PAGE_COUNT | O | O | O | O |
| MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT | X | X | O | O |
| MAXIMUM_JOURNAL_REPLAY_COUNT | X | O | O | O |
| MAXIMUM_NAMED_CURSOR_COUNT | O | O | O | O |
| MAXIMUM_PACKAGE_INSTANCE_COUNT | X | X | X | O |
| MAXIMUM_SESSION_CM_BUFFER_SIZE | O | O | O | O |
| MEASURE_CLUSTER_LATENCY | X | O | O | O |
| MEDIA_RECOVERY_LOG_BUFFER_SIZE | O | X | X | X |
| MEMORY_MERGE_RUN_COUNT | O | O | O | O |
| MEMORY_SORT_RUN_SIZE | O | O | O | O |
| MIN_SAMPLE_ROW_COUNT | X | O | O | O |
| MINIMUM_UNDO_PAGE_COUNT | O | O | O | O |
| NET_BUFFER_SIZE | O | O | O | O |
| NLS_DATE_FORMAT | O | O | O | O |
| NLS_TIME_FORMAT | O | O | O | O |
| NLS_TIME_WITH_TIME_ZONE_FORMAT | O | O | O | O |
| NLS_TIMESTAMP_FORMAT | O | O | O | O |
| NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT | O | O | O | O |
| NUMA | X | O | O | O |
| NUMA_MAP | X | O | O | O |
| OFFLINE_MEMBER_AFTER_FAILOVER | X | O | O | O |
| ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD | X | X | O | O |
| ONLINE_JOURNAL_REPLAY_THRESHOLD | X | O | O | O |
| OS_GROUP_ACCESS | X | O | O | O |
| PACKET_COMPRESSION_THRESHOLD | X | X | O | O |
| PAGE_CHECKSUM_TYPE | O | O | O | O |
| PARALLEL_IO_FACTOR | O | O | O | O |
| PARALLEL_IO_GROUP_1 ~ GROUP_16 | O | O | O | O |
| PARALLEL_LOAD_FACTOR | O | O | O | O |
| PENDING_LOG_BUFFER_COUNT | O | O | O | O |
| PLAN_CACHE | O | O | O | O |
| PLAN_CACHE_SIZE | O | O | O | O |
| PLAN_HISTORY | X | X | X | O |
| PLAN_HISTORY_SIZE | X | X | X | O |
| PRIVATE_STATIC_AREA_INIT_SIZE | X | X | O | O |
| PRIVATE_STATIC_AREA_NEXT_SIZE | X | X | O | O |
| PRIVATE_STATIC_AREA_SHRINK_THRESHOLD | X | X | O | O |
| PRIVATE_STATIC_AREA_SIZE | O | O | O | O |
| PROCESS_MAX_COUNT | O | O | O | O |
| QUERY_TIMEOUT | O | O | O | O |
| READABLE_ARCHIVELOG_DIR_COUNT | O | O | O | O |
| READABLE_BACKUP_DIR_COUNT | O | O | O | O |
| REBALANCE_BLOCK_READ_COUNT | X | O | O | O |
| RECOMPILE_CHECK_MINIMUM_PAGE_COUNT | O | X | X | X |
| RECOMPILE_PAGE_PERCENT | O | X | X | X |
| RECOVERY_LOG_BUFFER_SIZE | X | O | O | O |
| RECYCLEBIN | X | X | O | O |
| REDO_LOG_COMPRESSION_THRESHOLD | X | O | O | O |
| REFINE_RELATION | O | O | O | O |
| SESSION_FATAL_BEHAVIOR | O | O | O | O |
| SESSION_MEMORY_INIT_SIZE | X | O | O | O |
| SESSION_MEMORY_SHRINK_THRESHOLD | X | O | O | O |
| SHARED_MEMORY_ADDRESS | O | O | O | O |
| SHARED_MEMORY_STATIC_KEY | O | O | O | O |
| SHARED_MEMORY_STATIC_NAME | O | O | O | O |
| SHARED_MEMORY_STATIC_SIZE | O | O | O | O |
| SHARED_REQUEST_QUEUE_COUNT | O | O | O | O |
| SHARED_SERVERS | O | O | O | O |
| SHARED_SESSION | O | O | O | O |
| SNAPSHOT_STATEMENT_TIMEOUT | O | O | O | O |
| SQL_HISTORY_SIZE | X | O | O | O |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | O | O | O | O |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | X | X | O | O |
| SYSTEM_FILE_IO | O | O | O | O |
| SYSTEM_LOGGER_DIR | O | O | O | O |
| SYSTEM_MEMORY_AUX_TABLESPACE_SIZE | X | O | O | O |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_TABLESPACE_DIR | O | O | O | O |
| SYSTEM_UDS_DIR | X | O | O | O |
| TCP_NODELAY | X | O | O | O |
| TEMP_SEGMENT_CACHE_SIZE | X | O | O | O |
| TEMP_UNDO_ENABLED | X | O | O | O |
| TIMED_STATISTICS | X | O | O | O |
| TIMER_INTERVAL | O | X | X | O |
| TIMEZONE | O | O | O | O |
| TRACE_ALTER_SYSTEM | O | O | O | O |
| TRACE_DDL | O | O | O | O |
| TRACE_LOG_ID | O | O | O | O |
| TRACE_LOG_MSGBUG_SIZE | X | O | O | O |
| TRACE_LOG_TIME_DETAIL | O | O | O | O |
| TRACE_LOGGER | X | O | O | O |
| TRACE_LOGGER_REMOTE_HOST | X | O | O | O |
| TRACE_LOGGER_REMOTE_PORT | X | O | O | O |
| TRACE_LOGIN | O | O | O | O |
| TRACE_LONG_RUN_CURSOR | O | O | O | O |
| TRACE_LONG_RUN_SQL | O | O | O | O |
| TRACE_LONG_RUN_TIMER | X | X | O | O |
| TRACE_XA | O | O | O | O |
| TRANSACTION_ALLOCATION_TIMEOUT | X | O | O | O |
| TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O |
| TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT | O | O | O | O |
| TRANSACTION_TABLE_SIZE | O | O | O | O |
| TRANSACTION_TIMEOUT | X | O | O | O |
| UNDO_RELATION_ALLOCATION_TIMEOUT | X | O | O | O |
| UNDO_RELATION_COUNT | O | O | O | O |
| UNDO_SHRINK_THRESHOLD | O | O | O | O |
| USE_LARGE_PAGES | X | X | O | O |
| USER_DATA_TABLESPACE_MEDIA_TYPE | X | X | O | O |
| USER_DATA_TABLESPACE_SIZE | X | X | O | O |
| USER_DISK_DATA_TABLESPACE_NEXTSIZE | X | X | O | O |
| USER_TEMP_TABLESPACE_SIZE | O | O | O | O |
| XA_TRANSACTION_IDLE_TIMEOUT | X | X | O | O |

<a id="3fdf693d9d91ccc1"></a>
### SQL

<a id="2906ce746d7d9511"></a>
#### SQL Element

<a id="6f464678171b43e4"></a>
##### Data Type

데이터 타입에 대한 feature matrix는 다음과 같다.

<a id="17c242084ae29708"></a>
<table class="table column_count_6"><caption>Data type의 feature matrix</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>문자 스트링 타입</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>이진 스트링 타입</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>십진 숫자 타입</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>이진 숫자 타입</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN 타입</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>날짜/시간 타입</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL 타입</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROWID 타입</div></td><td><div>ROWID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="0db4c70fc1fb41a2"></a>
##### Function

함수 및 연산자에 대한 feature matrix는 다음과 같다.

**Function의 feature matrix**

<a id="3dce1290c526942a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| expr1 * expr2 | O | O | O | O |
| expr1 + expr2 | O | O | O | O |
| datetime + interval | O | O | O | O |
| ＋ expr | O | O | O | O |
| expr1 - expr2 | O | O | O | O |
| datetime - interval | O | O | O | O |
| - expr | O | O | O | O |
| expr1 / expr2 | O | O | O | O |
| str1 \|\| str2 | O | O | O | O |
| expr &lt;comp&gt; expr | O | O | O | O |
| expr &lt;comp&gt; ( subquery ) | O | O | O | O |
| ( subquery ) &lt;comp&gt; expr | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( subquery ) | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( expr, ... ) | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( subquery ) | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( expr, ... ) | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | O | O | O | O |
| ABS( num ) | O | O | O | O |
| ACOS( num ) | O | O | O | O |
| ADDDATE( date, interval ) | O | O | O | O |
| ADDDATE( expr, days ) | O | O | O | O |
| ADDTIME( expr1, expr2 ) | O | O | O | O |
| ADD_MONTHS( date, number ) | O | O | O | O |
| AND | O | O | O | O |
| ASCII( char ) | X | O | O | O |
| ASIN( num ) | O | O | O | O |
| ATAN( num ) | O | O | O | O |
| ATAN2( num1, num2 ) | O | O | O | O |
| AVG( num ) | O | O | O | O |
| expr1 [NOT] BETWEEN [ASYMMETRIC\|SYMMETRIC] expr2 AND expr3 | O | O | O | O |
| BITAND( num1, num2 ) | O | O | O | O |
| BITNOT( num ) | O | O | O | O |
| BITOR( num1, num2 ) | O | O | O | O |
| BITXOR( num1, num2 ) | O | O | O | O |
| BIT_LENGTH( str ) | O | O | O | O |
| BYTE_LENGTH( str ) | O | O | O | O |
| CASE .. WHEN .. THEN .. ELSE .. END | O | O | O | O |
| CASE2( condition, result, ... ) | O | O | O | O |
| CAST( expr AS datatype ) | O | O | O | O |
| CBRT( num ) | O | O | O | O |
| CEIL( num ) | O | O | O | O |
| CEILING( num ) | O | O | O | O |
| CHAR_LENGTH( str ) | O | O | O | O |
| CHARACTER_LENGTH( str ) | O | O | O | O |
| CHR( num ) | X | O | O | O |
| CLOCK_DATE() | O | O | O | O |
| CLOCK_LOCALTIME() | O | O | O | O |
| CLOCK_LOCALTIMESTAMP() | O | O | O | O |
| CLOCK_TIME() | O | O | O | O |
| CLOCK_TIMESTAMP() | O | O | O | O |
| COALESCE( expr1, ..., exprN ) | O | O | O | O |
| CONCAT( str1, str2 ) | O | O | O | O |
| CONCATENATE( str1, str2 ) | O | O | O | O |
| CONNECT_BY_ISCYCLE | X | X | X | O |
| CONNECT_BY_ISLEAF | X | X | X | O |
| CONNECT_BY_ROOT expr | X | X | X | O |
| COS( num ) | O | O | O | O |
| COT( num ) | O | O | O | O |
| COUNT( expr ) | O | O | O | O |
| COUNT(*) | O | O | O | O |
| CURRENT_CATALOG | O | O | O | O |
| CURRENT_DATE | O | O | O | O |
| CURRENT_SCHEMA | O | O | O | O |
| CURRENT_TIME | O | O | O | O |
| CURRENT_TIMESTAMP | O | O | O | O |
| CURRENT_USER | O | O | O | O |
| seq.CURRVAL | O | O | O | O |
| CURRVAL( seq ) | O | O | O | O |
| DATEADD( datepart, number, date ) | O | O | O | O |
| DATEDIFF( datepart, startdate, enddate ) | O | O | O | O |
| DATE_ADD( date, interval ) | O | O | O | O |
| DATE_PART( field, datetime ) | O | O | O | O |
| DECODE( expr, comparison, result, ... ) | O | O | O | O |
| DEGREES( radians ) | O | O | O | O |
| DIGEST ( data, type ) | X | O | O | O |
| DUMP( expr ) | O | O | O | O |
| EXISTS( subquery ) | O | O | O | O |
| EXP( num ) | O | O | O | O |
| EXTRACT( field FROM datetime ) | O | O | O | O |
| FACTORIAL( num ) | O | O | O | O |
| FLOOR( num ) | O | O | O | O |
| FROM_BASE64( str ) | X | O | O | O |
| FROM_TZ( timestamp, timezone ) | X | X | X | O |
| GREATEST( expr, ... ) | O | O | O | O |
| HASH32( expr [,expr] ... ) | X | X | X | O |
| HEX( str ) | X | O | O | O |
| expr1 [NOT] IN ( expr, ... ) | O | O | O | O |
| expr1 [NOT] IN ( subquery ) | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt; ) | O | O | O | O |
| subquery [NOT] IN ( subquery ) | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( subquery ) | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O |
| INITCAP( str ) | O | O | O | O |
| INSTR( str, substr, ... ) | O | O | O | O |
| IS NOT NULL | O | O | O | O |
| IS NULL | O | O | O | O |
| LAST_DAY( date ) | O | O | O | O |
| LAST_IDENTITY_VALUE() | X | O | O | O |
| LEAST( expr, ... ) | O | O | O | O |
| LENGTH( str ) | O | O | O | O |
| LENGTHB( str ) | O | O | O | O |
| LEVEL | X | X | X | O |
| string [NOT] LIKE pattern ESCAPE escape_char | O | O | O | O |
| LN( num ) | O | O | O | O |
| LNNVL( expr ) | X | X | O | O |
| LOCALTIME | O | O | O | O |
| LOCALTIMESTAMP | O | O | O | O |
| LOCAL_GROUP_ID() | X | O | O | O |
| LOCAL_GROUP_NAME() | X | O | O | O |
| LOCAL_MEMBER_ID() | X | O | O | O |
| LOCAL_MEMBER_NAME() | X | O | O | O |
| LOG( num2 ) | O | O | O | O |
| LOG( num1, num2 ) | O | O | O | O |
| LOGON_USER() | O | O | O | O |
| LOWER( str ) | O | O | O | O |
| LPAD( str, length, fill ) | O | O | O | O |
| LTRIM( str, [ str ] ) | O | O | O | O |
| MAX( expr ) | O | O | O | O |
| MIN( expr ) | O | O | O | O |
| MOD( num1, num2 ) | O | O | O | O |
| MONTHS_BETWEEN( date1, date2 ) | X | O | O | O |
| NEXT_DAY( date, day ) | X | O | O | O |
| seq.NEXTVAL | O | O | O | O |
| NEXTVAL( seq ) | O | O | O | O |
| NEXT VALUE FOR seq | O | O | O | O |
| NOT | O | O | O | O |
| NULLIF( expr1, expr2 ) | O | O | O | O |
| NUMTODSINTERVAL( num, interval_indicator ) | X | X | O | O |
| NUMTOYMINTERVAL( num, interval_indicator ) | X | X | O | O |
| NVL( expr1, expr2 ) | O | O | O | O |
| NVL2( expr1, expr2, expr3 ) | O | O | O | O |
| OCTET_LENGTH( str ) | O | O | O | O |
| OVERLAY( str1 PLACING str2 FROM start FOR length ) | O | O | O | O |
| OR | O | O | O | O |
| PHYSICAL_LENGTH( expr ) | X | X | O | O |
| PI() | O | O | O | O |
| POSITION( str1 IN str2 ) | O | O | O | O |
| POWER( num1, num2 ) | O | O | O | O |
| PRIOR expr | X | X | X | O |
| RADIANS( degrees ) | O | O | O | O |
| RANDOM( min, max ) | O | O | O | O |
| REPEAT( str, num ) | O | O | O | O |
| REPLACE( str, from, to ) | O | O | O | O |
| REVERSE( str ) | X | O | O | O |
| ROUND( num ) | O | O | O | O |
| ROUND( date, fmt ) | O | O | O | O |
| ROWID_GRID_BLOCK_ID( rowid ) | X | O | O | O |
| ROWID_GRID_BLOCK_SEQ( rowid ) | X | O | O | O |
| ROWID_MEMBER_ID( rowid ) | X | O | O | O |
| ROWID_OBJECT_ID( rowid ) | O | O | O | O |
| ROWID_PAGE_ID( rowid ) | O | O | O | O |
| ROWID_ROW_NUMBER( rowid ) | O | O | O | O |
| ROWID_SHARD_ID( rowid ) | X | O | O | O |
| ROWID_TABLESPACE_ID( rowid ) | O | O | O | O |
| ROWNUM | X | O | O | O |
| RPAD( str, length, fill ) | O | O | O | O |
| RTRIM( str, [ str ] ) | O | O | O | O |
| SESSION_ID() | O | O | O | O |
| SESSION_SERIAL() | O | O | O | O |
| SESSION_USER | O | O | O | O |
| SHARD_GROUP_ID( table, expr ) | X | O | O | O |
| SHARD_GROUP_NAME( table_name, shard_key_value [, ...] ) | X | O | O | O |
| SHARD_ID( table, expr ) | X | O | O | O |
| SHARD_NAME( table_name, shard_key_value [, ...] ) | X | O | O | O |
| SHIFT_LEFT( num, cnt ) | O | O | O | O |
| SHIFT_RIGHT( num, cnt ) | O | O | O | O |
| SIGN( num ) | O | O | O | O |
| SIN( num ) | O | O | O | O |
| SPLIT_PART( str, delimiter, field ) | O | O | O | O |
| SQRT( num ) | O | O | O | O |
| STATEMENT_DATE() | O | O | O | O |
| STATEMENT_LOCALTIME() | O | O | O | O |
| STATEMENT_LOCALTIMESTAMP() | O | O | O | O |
| STATEMENT_TIME() | O | O | O | O |
| STATEMENT_TIMESTAMP() | O | O | O | O |
| STATEMENT_VIEW_SCN() | O | O | O | O |
| STATEMENT_VIEW_SCN_DCN() | X | O | O | O |
| STATEMENT_VIEW_SCN_GCN() | X | O | O | O |
| STATEMENT_VIEW_SCN_LCN() | X | O | O | O |
| STDDEV( [ ALL \| DISTINCT ] expr ) | X | O | O | O |
| STDDEV_POP( expr ) | X | O | O | O |
| STDDEV_SAMP( expr ) | X | O | O | O |
| SUBSTR( str FROM start FOR length ) | O | O | O | O |
| SUBSTR( str, start, length ) | O | O | O | O |
| SUBSTRB( str, start, length ) | O | O | O | O |
| SUBSTRING( str FROM start FOR length ) | O | O | O | O |
| SUBSTRING( str, start, length ) | O | O | O | O |
| SUM( expr ) | O | O | O | O |
| SYSDATE | O | O | O | O |
| SYS_CONNECT_BY_PATH( expr, 'string' ) | X | X | X | O |
| SYS_EXTRACT_UTC( datetime_with_timezone ) | X | O | O | O |
| SYSTIME | O | O | O | O |
| SYSTIMESTAMP | O | O | O | O |
| TAN( num ) | O | O | O | O |
| TO_CHAR( datetime, fmt ) | O | O | O | O |
| TO_CHAR( number, fmt ) | O | O | O | O |
| TO_BASE64( str ) | X | O | O | O |
| TO_DATE( str, fmt ) | O | O | O | O |
| TO_NATIVE_BIGINT( str, fmt ) | X | X | O | O |
| TO_NATIVE_DOUBLE( str, fmt ) | O | O | O | O |
| TO_NATIVE_INTEGER( str, fmt ) | X | X | O | O |
| TO_NATIVE_REAL( str, fmt ) | O | O | O | O |
| TO_NATIVE_SMALLINT( str, fmt ) | X | X | O | O |
| TO_NUMBER( num, fmt ) | O | O | O | O |
| TO_TIME( str, fmt ) | O | O | O | O |
| TO_TIME_TZ( str, fmt ) | O | O | O | O |
| TO_TIME_WITH_TIME_ZONE( str, fmt ) | O | O | O | O |
| TO_TIMESTAMP( str, fmt ) | O | O | O | O |
| TO_TIMESTAMP_TZ( str, fmt ) | O | O | O | O |
| TO_TIMESTAMP_WITH_TIME_ZONE( str, fmt ) | O | O | O | O |
| TRANSACTION_DATE() | O | O | O | O |
| TRANSACTION_LOCALTIME() | O | O | O | O |
| TRANSACTION_LOCALTIMESTAMP() | O | O | O | O |
| TRANSACTION_TIME() | O | O | O | O |
| TRANSACTION_TIMESTAMP() | O | O | O | O |
| TRANSLATE( str, from, to ) | O | O | O | O |
| TRIM( LEADING\|TRAILING\|BOTH trim_char FROM source ) | O | O | O | O |
| TRUNC( num, scale ) | O | O | O | O |
| TRUNC( date, fmt ) | O | O | O | O |
| UPPER( str ) | O | O | O | O |
| UNHEX( str ) | X | O | O | O |
| UNHEX_TO_CHARSTR( str ) | X | O | O | O |
| USER_ID() | O | O | O | O |
| UUID() | X | O | O | O |
| VAR_POP( expr ) | X | O | O | O |
| VAR_SAMP( expr ) | X | O | O | O |
| VARIANCE( [ ALL \| DISTINCT ] expr ) | X | O | O | O |
| VERSION() | O | O | O | O |
| WIDTH_BUCKET( num, min, max, cnt ) | O | O | O | O |

<a id="717d5e7d209d9a15"></a>
#### Object

<a id="613ed07c50ff543d"></a>
##### SQL Object

SQL 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="a06debbf427b4147"></a>
<table class="table column_count_6"><caption>SQL 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center"><div>객체</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Database 
객체</div></td><td><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE REGISTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RESTORE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMENT ON object IS ..</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
객체</div></td><td><div>CREATE PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
객체</div></td><td><div>CREATE AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NOAUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
객체</div></td><td><div>CREATE USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GRANT privileges TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REVOKE privileges FROM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 객체</div></td><td><div>CREATE SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
객체</div></td><td><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="24"><div>Table 
객체</div></td><td><div>CREATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE TABLE AS SELECT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRUNCATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. STORAGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLASHBACK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PURGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
객체</div></td><td><div>CREATE VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Index 
객체</div></td><td><div>CREATE INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. AGING</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. STORAGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. RENAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. REBUILD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
객체</div></td><td><div>CREATE SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
객체</div></td><td><div>CREATE SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PUBLIC SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
객체</div></td><td><div>CREATE PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
객체</div></td><td><div>CREATE FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package
객체</div></td><td class="to_middle"><div>CREATE PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PACKAGE BODY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="efe672fe0c21bdc6"></a>
##### Cluster Object

Cluster 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="fb96dd2613661961"></a>
<table class="table column_count_6"><caption>Cluster 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>객체</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Cluster system 
객체</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
객체</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster table과 shard
객체</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Global 
secondary index
객체</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="cb9f6d091933f0af"></a>
#### SQL Language

<a id="28f37e15a5fb5d80"></a>
##### DML

데이터를 조작하는 DML 구문의 feature matrix는 다음과 같다.

**DML의 feature matrix**

<a id="e715ccabe3849a88"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| INSERT INTO .. | O | O | O | O |
| INSERT INTO .. RETURNING query | O | O | O | O |
| INSERT INTO .. RETURNING .. INTO .. | O | O | O | O |
| INSERT INTO .. UPDATE | X | X | X | O |
| INSERT INTO .. UPDATE .. RETURNING .. | X | X | X | O |
| INSERT INTO .. UPDATE .. RETURNING .. INTO .. | X | X | X | O |
| DELETE FROM .. | O | O | O | O |
| DELETE FROM .. RETURNING query | O | O | O | O |
| DELETE FROM .. RETURNING .. INTO .. | O | O | O | O |
| DELETE FROM .. WHERE CURRENT OF cursor | O | O | O | O |
| UPDATE .. | O | O | O | O |
| UPDATE .. RETURNING query | O | O | O | O |
| UPDATE .. RETURNING .. INTO .. | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O |
| CALL proc_name | X | O | O | O |

<a id="6d312618a5b9fe88"></a>
##### Query

데이터를 조회하는 SELECT 구문의 feature matrix는 다음과 같다.

**SELECT의 feature matrix**

<a id="88d2a674be7696e8"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| &lt;query expression&gt; | O | O | O | O |
| &lt;query specification&gt; | O | O | O | O |
| &lt;select list&gt; | O | O | O | O |
| &lt;from clause&gt; | O | O | O | O |
| &lt;joined table&gt; | O | O | O | O |
| &lt;where clause&gt; | O | O | O | O |
| &lt;group by clause&gt; | O | O | O | O |
| &lt;order by clause&gt; | O | O | O | O |
| &lt;offset limit clause&gt; | O | O | O | O |
| &lt;set operator&gt; | O | O | O | O |
| &lt;subquery&gt; | O | O | O | O |
| &lt;hint clause&gt; | O | O | O | O |
| &lt;with clause&gt; | X | X | X | O |
| &lt;search clause&gt; | X | X | X | O |
| &lt;cycle clause&gt; | X | X | X | O |
| &lt;start with clause&gt; | X | X | X | O |
| &lt;connect by clause&gt; | X | X | X | O |
| &lt;order siblings by clause&gt; | X | X | X | O |

<a id="0c8e3cb265d894e0"></a>
##### Control Language

제어 구문의 feature matrix는 다음과 같다.

<a id="01cf44be8c44aa45"></a>
<table class="table column_count_6"><caption>제어 구문의 feature matrix</caption><thead><tr><th class="to_center"><div>구분</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="b7611171514b5e88"></a>
#### PSM Language

Persistent Stored Module (PSM) language element의 feature matrix는 다음과 같다.

**Persistent Stored Module (PSM) language element의 feature matrix**

<a id="22e7941cb500589a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| Assignment Statement | X | O | O | O |
| Basic LOOP Statement | X | O | O | O |
| Block (BEGIN .. END) | X | O | O | O |
| CASE Statement | X | O | O | O |
| CLOSE Statement | X | O | O | O |
| Collection Method Invocation | X | O | O | O |
| Collection Variable Declaration | X | O | O | O |
| CONTINUE Statement | X | O | O | O |
| Cursor FOR LOOP Statement | X | O | O | O |
| Cursor Variable Declaration | X | O | O | O |
| DELETE Statement Extension | X | O | O | O |
| EXCEPTION_INIT Pragma | X | O | O | O |
| Exception Declaration | X | O | O | O |
| Exception Handler | X | O | O | O |
| EXECUTE IMMEDIATE Statement | X | O | O | O |
| EXIT Statement | X | O | O | O |
| Explicit Cursor Declaration and Definition | X | O | O | O |
| FETCH Statement | X | O | O | O |
| FOR LOOP Statement | X | O | O | O |
| GOTO Statement | X | O | O | O |
| IF Statement | X | O | O | O |
| Implicit Cursor Attribute | X | O | O | O |
| INSERT Statement Extension | X | O | O | O |
| Named Cursor Attribute | X | O | O | O |
| NULL Statement | X | O | O | O |
| OPEN Statement | X | O | O | O |
| OPEN FOR Statement | X | O | O | O |
| Procedure Call | X | O | O | O |
| Procedure Declaration and Definition | X | O | O | O |
| RAISE Statement | X | O | O | O |
| Record Variable Declaration | X | O | O | O |
| RETURN Statement | X | O | O | O |
| RETURNING INTO clause | X | O | O | O |
| %ROWTYPE Attribute | X | O | O | O |
| Scalar Variable Declaration | X | O | O | O |
| SELECT INTO Statement | X | O | O | O |
| SQLCODE Function | X | O | O | O |
| SQLERRM Function | X | O | O | O |
| %TYPE Attribute | X | O | O | O |
| UPDATE Statement Extension | X | O | O | O |
| WHILE LOOP Statement | X | O | O | O |

Built-in Package 의 feature matrix는 다음과 같다.

<a id="1599a73a23f9e557"></a>
<table class="table column_count_6"><caption>Built-in Package의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="017e6e1fb94d939e"></a>
### API

<a id="026149601e68f0f9"></a>
#### ODBC

ODBC 표준 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 feature matrix**

<a id="71bd5ddd73448660"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| SQLAllocHandle() | O | O | O | O |
| SQLBindCol() | O | O | O | O |
| SQLBindParameter() | O | O | O | O |
| SQLCloseCursor() | O | O | O | O |
| SQLColAttribute() | O | O | O | O |
| SQLColumnPrivileges() | O | O | O | O |
| SQLColumns() | O | O | O | O |
| SQLConnect() | O | O | O | O |
| SQLDescribeCol() | O | O | O | O |
| SQLDescribeParam() | O | O | O | O |
| SQLDisconnect() | O | O | O | O |
| SQLDriverConnect() | O | O | O | O |
| SQLEndTran() | O | O | O | O |
| SQLExecDirect() | O | O | O | O |
| SQLExecute() | O | O | O | O |
| SQLExtendedFetch() | O | O | O | O |
| SQLFetch() | O | O | O | O |
| SQLFetchScroll() | O | O | O | O |
| SQLForeignKeys() | O | O | O | O |
| SQLFreeHandle() | O | O | O | O |
| SQLFreeStmt() | O | O | O | O |
| SQLGetConnectAttr() | O | O | O | O |
| SQLGetCursorName() | O | O | O | O |
| SQLGetData() | O | O | O | O |
| SQLGetDescField() | O | O | O | O |
| SQLGetDescRec() | O | O | O | O |
| SQLGetDiagField() | O | O | O | O |
| SQLGetDiagRec() | O | O | O | O |
| SQLGetEnvAttr() | O | O | O | O |
| SQLGetFunctions() | O | O | O | O |
| SQLGetInfo() | O | O | O | O |
| SQLGetStmtAttr() | O | O | O | O |
| SQLGetTypeInfo() | O | O | O | O |
| SQLMoreResults() | O | O | O | O |
| SQLNumParams() | O | O | O | O |
| SQLNumResultCols() | O | O | O | O |
| SQLParamData() | O | O | O | O |
| SQLPrepare() | O | O | O | O |
| SQLPrimaryKeys() | O | O | O | O |
| SQLProcedureColumns() | O | O | O | O |
| SQLProcedures() | O | O | O | O |
| SQLPutData() | O | O | O | O |
| SQLRowCount() | O | O | O | O |
| SQLSetConnectAttr() | O | O | O | O |
| SQLSetCursorName() | O | O | O | O |
| SQLSetDescField() | O | O | O | O |
| SQLSetDescRec() | O | O | O | O |
| SQLSetEnvAttr() | O | O | O | O |
| SQLSetPos() | O | O | O | O |
| SQLSetStmtAttr() | O | O | O | O |
| SQLSpecialColumns() | O | O | O | O |
| SQLStatistics() | O | O | O | O |
| SQLTablePrivileges() | O | O | O | O |
| SQLTables() | O | O | O | O |

ODBC 표준 이외의 부가적으로 지원하는 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 외 함수의 feature matrix**

<a id="a8bffd26aa2dbd20"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| xa_open | O | O | O | O |
| xa_close | O | O | O | O |
| xa_start | O | O | O | O |
| xa_end | O | O | O | O |
| xa_rollback | O | O | O | O |
| xa_prepare | O | O | O | O |
| xa_commit | O | O | O | O |
| xa_recover | O | O | O | O |
| xa_forget | O | O | O | O |
| SQLGetXaSwitch | O | O | O | O |
| SQLGetXaConnectionHandle | O | O | O | O |
| SQLGetGroupCount | X | O | O | O |
| SQLGetGroupIDs | X | O | O | O |
| SQLGetGroupName | X | O | O | O |
| SQLGetSuitableGroupID | X | O | O | O |

<a id="d0a8156b8c00b0b8"></a>
#### JDBC

JDBC에 대한 class feature matrix는 다음과 같다.

**JDBC class의 feature matrix**

<a id="433d23939492c52a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| CallableStatement | X | O | O | O |
| CommonDataSource | O | O | O | O |
| Connection | O | O | O | O |
| ConnectionPoolDataSource | O | O | O | O |
| DatabaseMetaData | O | O | O | O |
| DataSource | O | O | O | O |
| Driver | O | O | O | O |
| ParameterMetaData | O | O | O | O |
| PooledConnection | O | O | O | O |
| PreparedStatement | O | O | O | O |
| ResultSet | O | O | O | O |
| ResultSetMetaData | O | O | O | O |
| RowId | O | O | O | O |
| Savepoint | O | O | O | O |
| Statement | O | O | O | O |
| XAConnection | O | O | O | O |
| XADataSource | O | O | O | O |
| XAResource | O | O | O | O |
| GoldilocksInterval | O | O | O | O |
| GoldilocksTypes | O | O | O | O |

<a id="1c71fb5dfbde6168"></a>
#### Embedded SQL

<a id="53d7389548dce5d9"></a>
##### Precompiler Option

Precompiler의 option에 대한 feature matrix는 다음과 같다.

**Precompiler option의 feature matrix**

<a id="d8a651f6e3720b62"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --help | O | O | O | O |
| --include-path | O | O | O | O |
| --no-prompt | O | O | O | O |
| --output | O | O | O | O |
| --unsafe-null | O | O | O | O |
| --version | O | O | O | O |
| --no-lineinfo | X | O | O | O |
| --char_map | X | O | O | O |
| --cumulative | X | X | O | O |
| --autocommit | X | X | X | O |
| --parse | X | X | O | O |

<a id="a2c86aa7b1cef09c"></a>
##### Embedded SQL 전용 구문

Embedded SQL에서만 사용 가능한 SQL 구문에 대한 feature matrix는 다음과 같다.

**Embedded SQL 전용 구문의 feature matrix**

<a id="2169da0336526186"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| EXEC SQL AT | O | O | O | O |
| EXEC SQL ATOMIC INSERT | O | O | O | O |
| EXEC SQL AUTOCOMMIT | O | O | O | O |
| EXEC SQL BEGIN DECLARE SECTION | O | O | O | O |
| EXEC SQL COMMIT RELEASE | O | O | O | O |
| EXEC SQL CONNECT | O | O | O | O |
| EXEC SQL CONTEXT ALLOCATE | O | O | O | O |
| EXEC SQL CONTEXT FREE | O | O | O | O |
| EXEC SQL CONTEXT USE | O | O | O | O |
| EXEC SQL DISCONNECT | O | O | O | O |
| EXEC SQL END DECLARE SECTION | O | O | O | O |
| EXEC SQL FOR | O | O | O | O |
| EXEC SQL GET GROUPID | X | O | O | O |
| EXEC SQL INCLUDE | O | O | O | O |
| EXEC SQL INCLUDE SQLCA | O | O | O | O |
| EXEC SQL OPTION | O | O | O | O |
| EXEC SQL ROLLBACK RELEASE | O | O | O | O |
| EXEC SQL WHENEVER | O | O | O | O |
| EXEC SQL BEGIN ARGUMENT SECTION | X | X | X | O |
| EXEC SQL END ARGUMENT SECTION | X | X | X | O |

<a id="996684c93254e722"></a>
##### Host Variable Data Type

Host 변수에 사용할 수 있는 embbeded SQL data type의 feature matrix는 다음과 같다.

**Host data type의 feature matrix**

<a id="d885cf3e7aacf633"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| C native type | O | O | O | O |
| struct, union | O | O | O | O |
| typedef | O | O | O | O |
| VARCHAR | O | O | O | O |
| LONG VARCHAR | O | O | O | O |
| BINARY | O | O | O | O |
| LONG VARBINARY | O | O | O | O |
| BOOLEAN | O | O | O | O |
| NUMBER | O | O | O | O |
| DATE | O | O | O | O |
| TIME | O | O | O | O |
| TIME WITH TIMEZONE | O | O | O | O |
| TIMESTAMP | O | O | O | O |
| TIMESTAMP WITH TIMEZONE | O | O | O | O |
| INTERVAL YEAR | O | O | O | O |
| INTERVAL MONTH | O | O | O | O |
| INTERVAL DAY | O | O | O | O |
| INTERVAL HOUR | O | O | O | O |
| INTERVAL MINUTE | O | O | O | O |
| INTERVAL SECOND | O | O | O | O |
| INTERVAL YEAR TO MONTH | O | O | O | O |
| INTERVAL DAY TO HOUR | O | O | O | O |
| INTERVAL DAY TO MINUTE | O | O | O | O |
| INTERVAL DAY TO SECOND | O | O | O | O |
| INTERVAL HOUR TO MINUTE | O | O | O | O |
| INTERVAL HOUR TO SECOND | O | O | O | O |
| INTERVAL MINUTE TO SECOND | O | O | O | O |

<a id="3e5e2d598ae9719b"></a>
##### Dynamic SQL

Dynamic SQL에 대한 feature matrix는 다음과 같다.

**Dynamic SQL의 feature matrix**

<a id="01ab74c70d1d7c68"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| SELECT .. INTO | O | O | O | O |
| EXECUTE IMMEDIATE sql | O | O | O | O |
| PREPARE stmt | O | O | O | O |
| EXECUTE stmt | O | O | O | O |
| DECLARE cursor FOR sql | O | O | O | O |
| DECLARE cursor FOR stmt | O | O | O | O |
| OPEN cursor | O | O | O | O |
| OPEN cursor USING | O | O | O | O |
| FETCH cursor INTO | O | O | O | O |
| CLOSE cursor | O | O | O | O |
| DELETE .. WHERE CURRENT OF cursor | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O |

<a id="db4af199ffa9bcbf"></a>
#### PyDBC

<a id="981e6572ee02716c"></a>
##### Module

PyDBC가 제공하는 pygoldilocks의 method feature matrix는 다음과 같다.

**pygoldilock method의 feature matrix**

<a id="74b38252a8bdbdd3"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| connect | X | O | O | O |
| Date | X | O | O | O |
| Time | X | O | O | O |
| Timestamp | X | O | O | O |
| DateFromTicks | X | O | O | O |
| TimeFromTicks | X | O | O | O |
| TimestampFromTicks | X | O | O | O |
| Binary | X | O | O | O |
| STRING | X | O | O | O |
| BINARY | X | O | O | O |
| NUMBER | X | O | O | O |
| DATETIME | X | O | O | O |
| ROWID | X | O | O | O |
| getDecimalSeparator | X | O | O | O |
| setDecimalSeparator | X | O | O | O |

pygoldilocks module의 attribute feature matrix는 다음과 같다.

**pygoldilock attribute의 feature matrix**

<a id="398c91836ca9da5e"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| apilevel | X | O | O | O |
| threadsafety | X | O | O | O |
| paramstyle | X | O | O | O |
| version | X | O | O | O |
| lowercase | X | O | O | O |

<a id="a15e73702b0d5ac1"></a>
##### Connection

Connection 객체의 method feature matrix는 다음과 같다.

**Connection method의 feature matrix**

<a id="c876061fffd0cd03"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| cursor | X | O | O | O |
| commit | X | O | O | O |
| rollback | X | O | O | O |
| close | X | O | O | O |
| getinfo | X | O | O | O |
| execute | X | O | O | O |
| set_attr | X | O | O | O |

Connection 객체의 attribute feature matrix는 다음과 같다.

**Connection attribute의 feature matrix**

<a id="45c69709094a5575"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| autocommit | X | O | O | O |
| searchescape | X | O | O | O |
| timeout | X | O | O | O |

<a id="d621d91e0551a0c4"></a>
##### Cursor

Cursor 객체의 method feature matrix는 다음과 같다.

**Cursor method의 feature matrix**

<a id="445965fc5e0147db"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| excute | X | O | O | O |
| executemany | X | O | O | O |
| fetchone | X | O | O | O |
| fetchall | X | O | O | O |
| fetchmany | X | O | O | O |
| commit | X | O | O | O |
| rollback | X | O | O | O |
| skip | X | O | O | O |
| nextset | X | O | O | O |
| close | X | O | O | O |
| setinputsizes | X | O | O | O |
| setoutputsize | X | O | O | O |
| callproc | X | O | O | O |
| callfunc | X | O | O | O |
| tables | X | O | O | O |
| columns | X | O | O | O |
| statistics | X | O | O | O |
| rowIdColumns | X | O | O | O |
| rowVerColumns | X | O | O | O |
| primaryKeys | X | O | O | O |
| foreignKeys | X | O | O | O |
| procedures | X | O | O | O |
| getTypeInfo | X | O | O | O |

Cursor 객체의 attribute feature matrix는 다음과 같다.

**Cursor attribute의 feature matrix**

<a id="340857aae25bdb0b"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| Description | X | O | O | O |
| rowcount | X | O | O | O |
| arraysize | X | O | O | O |
| connection | X | O | O | O |
| fast_executemany | X | O | O | O |

<a id="2effe38232e4f5a9"></a>
##### Row

Row 객체의 attribute feature matrix는 다음과 같다.

**Row attribute의 feature matrix**

<a id="6c17d1a56cb0d551"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| cursor_description | X | O | O | O |

<a id="d75dcdfdb4d2460c"></a>
### Utility

<a id="d67a006518f4e4c4"></a>
#### gcreatedb

<a id="68602b31b4af0bd5"></a>
##### Command Usage

gcreatedb의 command usage에 대한 feature matrix는 다음과 같다.

**gcreatedb command usage의 feature matrix**

<a id="5af8716fe2bf3938"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --character_set | O | O | O | O |
| --char_length_units | O | O | O | O |
| --cluster | X | O | O | O |
| --db_comment | O | O | O | O |
| --help | O | O | O | O |
| --host | X | O | O | O |
| --member | X | O | O | O |
| --port | X | O | O | O |
| --silent | O | O | O | O |
| --timezone | O | O | O | O |

<a id="522e8d621eac4bbd"></a>
#### glsnr

<a id="4ca3d0f508dd6c11"></a>
##### Command Usage

glsnr의 command usage에 대한 feature matrix는 다음과 같다.

**glsnr command usage의 feature matrix**

<a id="681e5dc790b9ef9e"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --help | O | O | O | O |
| --home | X | O | O | O |
| --silent | O | O | O | O |
| --start | O | O | O | O |
| --status | O | O | O | O |
| --stop | O | O | O | O |

<a id="80defaef314ea13d"></a>
##### Configuration File

glsnr의 configuration에 대한 feature matrix는 다음과 같다.

**glsnr configuration file syntax의 feature matrix**

<a id="8e1f5070ba8f0f79"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| BACKLOG | O | O | O | O |
| DEFAULT_CS_MODE | O | O | O | O |
| LISTENER_LOG_DIR | X | O | O | O |
| LISTEN_PORT | O | O | O | O |
| TCP_EXCLUDED | O | O | O | O |
| TCP_INVITED | O | O | O | O |
| TCP_HOST | O | O | O | O |
| TCP_VALIDNODE_CHECKING | O | O | O | O |
| TIMEOUT | O | O | O | O |
| USR_DIR | X | O | O | O |

<a id="1007f7137d0f70f8"></a>
#### gsql/gsqlnet

<a id="f2bb53737fda94b9"></a>
##### Command Usage

gsql의 command usage에 대한 feature matrix는 다음과 같다.

**gsql command usage의 feature matrix**

<a id="052c5ab14712ddfd"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| username password | O | O | O | O |
| --as {SYSDBA\|ADMIN} | O | O | O | O |
| --conn-string | O | O | O | O |
| --dsn | O | O | O | O |
| --enable-color | O | O | O | O |
| --help | O | O | O | O |
| --import | O | O | O | O |
| --no-prompt | O | O | O | O |
| --prompt | O | O | O | O |
| --silent | O | O | O | O |
| --version | O | O | O | O |

<a id="2470ca6624072541"></a>
##### Interactive gsql Command

gsql 프롬프트 상태에서 사용하는 interactive gsql command에 대한 feature matrix는 다음과 같다.

**Interactive gsql command의 feature matrix**

<a id="d7abd97f44e793ca"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| `\\` | O | O | O | O |
| `\connect userid password [as sysdba] ` | O | O | O | O |
| `\cshutdown` | X | O | O | O |
| `\cstartup` | X | O | O | O |
| `\ddl_cluster` | X | O | O | O |
| `\ddl_db` | O | O | O | O |
| `\ddl_tablespace` | O | O | O | O |
| `\ddl_profile` | O | O | O | O |
| `\ddl_audit_policy` | X | O | O | O |
| `\ddl_auth` | O | O | O | O |
| `\ddl_schema` | O | O | O | O |
| `\ddl_public_synonym` | O | O | O | O |
| `\ddl_table` | O | O | O | O |
| `\ddl_constraint` | O | O | O | O |
| `\ddl_index` | O | O | O | O |
| `\ddl_view` | O | O | O | O |
| `\ddl_sequence` | O | O | O | O |
| `\ddl_synonym` | O | O | O | O |
| `\ddl_procedure` | X | O | O | O |
| `\ddl_package` | X | X | O | O |
| `\desc ` | O | O | O | O |
| `\dynamic sql :var ` | O | O | O | O |
| `\exec ` | O | O | O | O |
| `\exec :var := :value` | O | O | O | O |
| `\exec sql ` | O | O | O | O |
| `\explain plan [on\|only] ` | O | O | O | O |
| `\help ` | O | O | O | O |
| `\history` | O | O | O | O |
| `\host {os_command}` | X | O | O | O |
| `\import` | O | O | O | O |
| `\idesc ` | O | O | O | O |
| `\{n} ` | O | O | O | O |
| `\prepare sql ` | O | O | O | O |
| `\print ` | O | O | O | O |
| `\quit` | O | O | O | O |
| `\set autocommit ` | O | O | O | O |
| `\set color ` | O | O | O | O |
| `\set colsize ` | O | O | O | O |
| `\set ddlsize` | O | O | O | O |
| `\set error ` | O | O | O | O |
| `\set history ` | O | O | O | O |
| `\set linesize ` | O | O | O | O |
| `\set numsize ` | O | O | O | O |
| `\set pagesize ` | O | O | O | O |
| `\set timing ` | O | O | O | O |
| `\set vertical ` | O | O | O | O |
| `\shutdown {abort\|immediate\|transactional\|normal}` | O | O | O | O |
| `\startup {nomount\|mount\|open} ` | O | O | O | O |
| `\var ` | O | O | O | O |

<a id="080f0201779d9cc7"></a>
#### gloader/gloadernet

<a id="6fc50b7151a8bc49"></a>
##### Command Usage

gloader의 command usage에 대한 feature matrix는 다음과 같다.

**gloader command usage의 feature matrix**

<a id="86ac85a33d443a8a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| username password | O | O | O | O |
| --array | O | O | O | O |
| --atomic | O | O | O | O |
| --bad | O | O | O | O |
| --buffered | O | O | O | O |
| --commit | O | O | O | O |
| --control | O | O | O | O |
| --data | O | O | O | O |
| --dsn | O | O | O | O |
| --errors | O | O | O | O |
| --export | O | O | O | O |
| --fieldterm | X | O | O | O |
| --filesize | O | O | O | O |
| --format | O | O | O | O |
| --help | O | O | O | O |
| --import | O | O | O | O |
| --lineterm | X | O | O | O |
| --log | O | O | O | O |
| --no-prompt | O | O | O | O |
| --parallel | O | O | O | O |
| --propagation | O | O | O | O |
| --qualifier | X | O | O | O |
| --silent | O | O | O | O |
| --AsTIMESTAMP | O | O | O | O |
| --where | X | O | O | O |
| --group-id | X | O | O | O |
| --directio-size | X | O | O | O |

<a id="e3cc0d2f7cb51634"></a>
##### Control File Syntax

gloader의 control file syntax에 대한 feature matrix는 다음과 같다.

**gloader control file syntax의 feature matrix**

<a id="82ecbb0db2b9bdab"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| CHARACTERSET | O | O | O | O |
| FIELDS TERMINATED BY | O | O | O | O |
| OPTIONALLY ENCLOSED BY | O | O | O | O |
| TABLE table_name | O | O | O | O |
| TABLE schema_name.table_name | O | O | O | O |
| LTRIM | X | O | O | O |
| RTRIM | X | O | O | O |
| LINES TERMINATED BY | X | O | O | O |
| WHERE | X | O | O | O |

<a id="86bdd181af056105"></a>
#### gdump

<a id="b89fe638a67586ac"></a>
##### Command Usage

gdump의 command usage에 대한 feature matrix는 다음과 같다.

<a id="71fc7e65e14db2be"></a>
<table class="table column_count_6"><caption>gdump command usage의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="c89f31dfc3ced8ea"></a>
#### tablediff

<a id="1ee0a3e01c33f200"></a>
##### Configuration File

tablediff의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="6cd65ee3e732e07f"></a>
<table class="table column_count_6"><caption>tablediff configuration file의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td><div>SOURCE_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td><div>TARGET_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td><div>TARGET_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_UPDATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_DELETE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td><div>DIFF_BIN_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DIFF_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_CALL_STACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_ROW_UNIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>EXCLUDE_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_DIFF</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_SUCCESS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_QUEUE_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_THREAD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_UNIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PARTITION_RANGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>WHERE_CLAUSE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4481a5dc679ffe6b"></a>
#### gsyncher

<a id="59775c226055e92a"></a>
##### Command Usage

gsyncher의 command usage에 대한 feature matrix는 다음과 같다.

**gsyncher command usage의 feature matrix**

<a id="596ed5552c99567c"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --log | O | O | O | O |
| --silent | O | O | O | O |
| --home | X | O | O | O |
| --copy-right | O | O | O | O |
| --backup-path | O | O | O | O |
| --help | O | O | O | O |

<a id="ca35225e8a8a8c92"></a>
#### gmon

<a id="70fb76edc6a02062"></a>
##### Command Usage

gmon의 command usage에 대한 feature matrix는 다음과 같다.

**gmon command usage의 feature matrix**

<a id="4382a61b87efff35"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --start | X | O | O | O |
| --stop | X | O | O | O |
| --status | X | O | O | O |
| --home | X | O | O | O |
| --uds_dir | X | X | O | O |
| --silent | X | O | O | O |
| --no-copyright | X | O | O | O |
| --help | X | O | O | O |

<a id="ed9efa8896257b9f"></a>
#### gtrclogger

<a id="e0dd6e57c53b507a"></a>
##### Command Usage

gtrclogger의 command usage에 대한 feature matrix는 다음과 같다.

**gtrclogger command usage의 feature matrix**

<a id="7552740ee1959f0d"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --dir | X | O | O | O |
| --help | X | O | O | O |
| --port | X | O | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |

<a id="4ee326ff1da06b40"></a>
#### glocator

<a id="e6f1b6d5911f67fa"></a>
##### Command Usage

glocator의 command usage에 대한 feature matrix는 다음과 같다.

**glocator command usage의 feature matrix**

<a id="19f85cc279c6c697"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --create | X | O | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |
| --conf | X | O | O | O |
| --status | X | O | O | O |
| --sync | X | O | O | O |
| --silent | X | O | O | O |
| --no-copyright | X | O | O | O |
| --help | X | O | O | O |

<a id="acf8361b478af7df"></a>
##### Configuration File

glocator의 configuration file에 대한 feature matrix는 다음과 같다.

**glocator configuration file의 feature matrix**

<a id="699a10ef3869bdc2"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| PORT | X | O | O | O |
| WORKER_COUNT | X | O | O | O |
| SESSION_QUEUE_SIZE | X | O | O | O |
| SESSION_ALLOCATOR_SIZE | X | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O |
| SYSTEM_UDS_DIR | X | O | O | O |
| LOCATION_FILE_DIR | X | O | O | O |
| LOCATION_FILE_SIZE | X | O | O | O |
| LOCATION_FILE_MAX_SIZE | X | O | O | O |
| SESSION_TIMEOUT | X | O | O | O |
| FAILOVER_TIMEOUT | X | O | O | O |
| ALTERNATE_LOCATORS | X | O | O | O |
| SYNC_RETRY_COUNT | X | O | O | O |
| SYNC_RESPONSE_TIMEOUT | X | O | O | O |

<a id="feb8f7c07d7e3dc9"></a>
#### gagent

<a id="1660cd3439992704"></a>
##### Command Usage

gagent의 command usage에 대한 feature matrix는 다음과 같다.

**gagent command usage의 feature matrix**

<a id="44a152cef9a17df9"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --start | X | O | O | O |
| --stop | X | O | O | O |
| --conf | X | O | O | O |
| --status | X | O | O | O |
| --home | X | O | O | O |
| --silent | X | O | O | O |
| --no-copyright | X | O | O | O |
| --help | X | O | O | O |

<a id="48cbcb30d6855fb6"></a>
##### Configuration File

gagent의 configuration file에 대한 feature matrix는 다음과 같다.

**gagent configuration file의 feature matrix**

<a id="cd3409b73c01a6d6"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| PORT | X | O | O | O |
| LOCATOR_HOST | X | O | O | O |
| LOCATOR_PORT | X | O | O | O |
| COMMAND_QUEUE_SIZE | X | O | O | O |
| COMMAND_ALLOCATOR_SIZE | X | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O |
| SESSION_TIMEOUT | X | O | O | O |
| UPDATE_LOCATION_TIME | X | O | O | O |
| ALTERNATE_LOCATORS | X | O | O | O |

<a id="74a2d8b79217d690"></a>
#### gloctl

<a id="8af655270799afa1"></a>
##### Command Usage

gloctl의 command usage에 대한 feature matrix는 다음과 같다.

**gloctl command usage의 feature matrix**

<a id="a2306b98e856b82f"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --dsn | X | X | X | X |
| --conf | X | O | O | O |
| --ip | X | O | O | O |
| --port | X | O | O | O |
| --import | X | O | O | O |
| --silent | X | O | O | O |
| --no-copyright | X | O | O | O |
| --help | X | O | O | O |

<a id="1ea83ec655fcfa7e"></a>
##### Configuration File

gloctl의 configuration file에 대한 feature matrix는 다음과 같다.

**gloctl configuration file의 feature matrix**

<a id="b8a9ab1ffba0123b"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| PORT | X | O | O | O |
| LOCATOR_HOST | X | O | O | O |
| LOCATOR_PORT | X | O | O | O |

<a id="4923cb7126711abf"></a>
### Replication

<a id="d7ec275e15e64411"></a>
#### cyclone

<a id="1d58d4aa24301229"></a>
##### Command Usage

cyclone의 command usage에 대한 feature matrix는 다음과 같다.

**cyclone command usage의 feature matrix**

<a id="e5e3be7c62b9f52b"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --conf | O | O | O | O |
| --encrypt | X | O | O | O |
| --group | O | O | O | O |
| --help | O | O | O | O |
| --key | X | O | O | O |
| --master | O | O | O | O |
| --reset | O | O | O | O |
| --silent | O | O | O | O |
| --slave | O | O | O | O |
| --start | O | O | O | O |
| --status | O | O | O | O |
| --stop | O | O | O | O |
| --sync | O | O | O | O |
| --stand-alone | X | O | O | O |
| --recovery | X | O | O | O |
| --local | X | O | O | O |

<a id="194c57d18ccd9132"></a>
##### Configuration File

cyclone의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="d82f2ce72151ed24"></a>
<table class="table column_count_6"><caption>cyclone configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="ee5637a7e1049dc7"></a>
#### logmirror

<a id="6e18405f9ad5ed41"></a>
##### Command Usage

logmirror의 command usage에 대한 feature matrix는 다음과 같다.

**logmirror command usage의 feature matrix**

<a id="5d81df81a4484c36"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --conf | O | O | O | O |
| --help | O | O | O | O |
| --infiniband | O | O | O | O |
| --master | O | O | O | O |
| --silent | O | O | O | O |
| --slave | O | O | O | O |
| --start | O | O | O | O |
| --stop | O | O | O | O |

<a id="7181963b57dfbc5a"></a>
##### Configuration File

logmirror의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="7fa15a6e033538d3"></a>
<table class="table column_count_6"><caption>logmirror configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="b989ddfe694249d8"></a>
#### cymon

<a id="683bdf03593aade5"></a>
##### Command Usage

cymon의 command usage에 대한 feature matrix는 다음과 같다.

**cymon command usage의 feature matrix**

<a id="18e47540689c3a1d"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --conf | O | O | O | O |
| --help | O | O | O | O |
| --cycle | O | O | O | O |
| --key | X | O | O | O |
| --start | O | O | O | O |
| --stop | O | O | O | O |
| --status | O | O | O | O |

<a id="f4d3ea7354715fec"></a>
#### cyfile

<a id="14b97d49798acb06"></a>
##### Command Usage

cyfile의 command usage에 대한 feature matrix는 다음과 같다.

**cyfile command usage의 feature matrix**

<a id="d99d089dcd210191"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --conf | X | X | O | O |
| --help | X | X | O | O |
| --reset | X | X | O | O |
| --key | X | X | O | O |
| --silent | X | X | O | O |
| --info | X | X | O | O |
| --start | X | X | O | O |
| --stop | X | X | O | O |
| --group | X | X | O | O |
| --encrypt | X | X | O | O |
| --status | X | X | O | O |

<a id="bcd57a5bbebe6de8"></a>
##### Configuration File

cyfile의 configuration file에 대한 feature matrix는 다음과 같다.

**cyfile configuration file의 feature matrix**

<a id="e6e12786dda0f4e8"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| DSN | X | X | O | O |
| HOST_IP | X | X | O | O |
| HOST_PORT | X | X | O | O |
| PROTOCOL | X | X | O | O |
| USER_ID | X | X | O | O |
| USER_PW | X | X | O | O |
| GROUP_NAME | X | X | O | O |
| USER_ENCRYPT_PW | X | X | O | O |
| CAPTURE_TABLE | X | X | O | O |
| READ_LOG_BLOCK_COUNT | X | X | O | O |
| TRANS_SORT_AREA_SIZE | X | X | O | O |
| TRANS_FILE_PATH | X | X | O | O |
| LOG_CAPTURE_INTERVAL_1 | X | X | O | O |
| LOG_CAPTURE_INTERVAL_2 | X | X | O | O |
| DATA_FILE_PATH | X | X | O | O |
| DATA_FILE_PREFIX | X | X | O | O |
| DATA_FILE_SIZE | X | X | O | O |
| UPDATE_BEFORE_VALUE | X | X | O | O |

<a id="ce946c44921d964a"></a>
## What's New in GOLDILOCKS 21c.1

본 장은 GOLDILOCKS 21c.1에 새로 추가된 기능들에 대해 간략히 설명한다.

<a id="b0457eda687562d3"></a>
### Architecture

<a id="77fe91385d48462b"></a>
#### System Architecture

변동 사항 없음

<a id="69e1ecc62ee7d01c"></a>
#### Storage Internal

변동 사항 없음

<a id="c03ddc960307c2de"></a>
#### Transaction Control

변동 사항 없음

<a id="db1f99418f38249d"></a>
#### Backup & Recovery

변동 사항 없음

<a id="bb051cbc04a915b2"></a>
#### Database Information

<a id="af4851a7c3eb9a16"></a>
##### DICTIONARY_SCHEMA

변동 사항 없음

<a id="0573b0e71883364e"></a>
##### INFORMATION_SCHEMA

변동 사항 없음

<a id="f8a520d517655480"></a>
##### PERFORMANCE_VIEW_SCHEMA

Plan history 기능을 통해 관리되고 있는 plan들을 조회할 수 있는 [V$PLAN_HISTORY](../part-02-administration-manual/9-database-information.md#df906f39614f5417) view가 추가되었다.

Plan history 기능을 통해 관리되고 있는 최신 plan을 조회할 수 있는 [V$PLAN_HISTORY_LATEST](../part-02-administration-manual/9-database-information.md#eca5f3dbf7c49156) view가 추가되었다.

<a id="c9b96749017c92d3"></a>
#### Server Property

Session 내에서 사용할 수 있는 package instance 개수를 제어하는 [MAXIMUM_PACKAGE_INSTANCE_COUNT](../part-02-administration-manual/10-server-property.md#f7501c03d2e338e0) 프로퍼티가 추가되었다.

Session 내에서 사용할 수 있는 파일 캐쉬의 최대 개수를 제어하는 [MAXIMUM_FILE_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#dd076383d1e9db22) 프로퍼티가 추가되었다.

IO thread가 버퍼에서 변경된 페이지를 디스크로 쓸 때, 한 번의 쓰기 연산으로 디스크에 기록할 최대 페이지 수를 제어하는 [MAXIMUM_FLUSH_BUFFER_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#01e975f1c939c3b7) 프로퍼티가 추가되었다.

Session이 버퍼에 존재하지 않는 디스크 테이블스페이스의 페이지에 접근할 때 한 번의 디스크 IO로 프리 페치할 최대 페이지 수를 제어하는 [BUFFER_PREFETCH_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#0ccb362b42900cce) 프로퍼티가 추가되었다.

Plan history 사용 여부를 설정하는 [PLAN_HISTORY](../part-02-administration-manual/10-server-property.md#ded1a20f3222603b) 프로퍼티가 추가되었다.

Plan history에 저장할 plan 개수를 제어하는 [PLAN_HISTORY_SIZE](../part-02-administration-manual/10-server-property.md#1348bca7461d1635) 프로퍼티가 추가되었다.

클러스터 환경에서 인덱스를 재구축할 때 모든 멤버에 동시에 재구축할지 여부를 설정하는 [BROADCAST_INDEX_REBUILD_PROTOCOL](../part-02-administration-manual/10-server-property.md#b70c377d862562f2) 프로퍼티가 추가되었다.

타이머 thread가 시스템 시간을 설정할 수 있도록 시간 간격을 설정하는 [TIMER_INTERVAL](../part-02-administration-manual/10-server-property.md#64210712883ef70a) 프로퍼티가 추가되었다.

[DEFAULT_INDEX_PCTFREE](../part-02-administration-manual/10-server-property.md#222c05a8df683df0)의 기본값이 10으로 변경되었다.

[DEFAULT_MAXTRANS](../part-02-administration-manual/10-server-property.md#9d86fd050489a563)의 기본값이 32로 변경되었다.

Hash instant table의 예상 bucket count의 최대값을 설정하는 [INST_HASH_TABLE_BUCKET_MAX_COUNT](../part-02-administration-manual/10-server-property.md#ffcbb52c42b37a79) 프로퍼티가 추가되었다.

인덱스 구축 및 재구축 시 발생하는 로그의 기록 속도를 제어할 수 있는 [INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#e613f53aef76fcfb) 프로퍼티가 추가되었다.

Redo log archiving 시 디스크 I/O 성능을 제어할 수 있는 [ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#453ac01cb35a1161) 프로퍼티가 추가되었다.

<a id="4694018430516939"></a>
### SQL

<a id="c236da9ff2e92c70"></a>
#### SQL Element

<a id="5d31a51f5f39ad99"></a>
##### Data Type

변동 사항 없음

<a id="927aab0ca42224cf"></a>
##### Function

[FROM_TZ](../part-03-sql-manual/17-built-in-function-references.md#5afecf371a5e4324) 함수가 추가되었다.

다음과 같이 CONNECT BY 절과 함께 사용할 수 있는 [&lt;hierarchy expression&gt;](../part-03-sql-manual/20-sql-references-h-z.md#2bf5302b069389ff)이 추가되었다.

- LEVEL
- CONNECT_BY_ISCYCLE
- CONNECT_BY_ISLEAF
- PRIOR expr
- CONNECT_BY_ROOT expr
- SYS_CONNECT_BY_PATH( expr, 'string' )

<a id="5c5227b31a4d6250"></a>
#### Object

<a id="2360530d431b77c2"></a>
##### SQL Object

변동 사항 없음

<a id="e82066b3893d681e"></a>
##### Cluster Object

변동 사항 없음

<a id="05e7381dfe08056e"></a>
#### SQL Language

<a id="2805e8f20fcdc899"></a>
##### DML

Upsert 구문이 추가되었다.

- [INSERT INTO name ... UPDATE](../part-03-sql-manual/20-sql-references-h-z.md#315b27f6d7731e80)
- [INSERT INTO name ... UPDATE RETURNING](../part-03-sql-manual/20-sql-references-h-z.md#081d2bcbdca6ff97)
- [INSERT INTO name ... UPDATE RETURNING ... INTO](../part-03-sql-manual/20-sql-references-h-z.md#ab208d18bb5b972b)

<a id="e33aba77391a6bfe"></a>
##### Query

<a id="5fd0394030598a4b"></a>
###### **WITH 절**

WITH 절을 이용한 Common Table Expression (CTE) 기능이 추가되었다

- [Common Table Expression (CTE)](../part-03-sql-manual/12-sql-languages.md#ebefe35fc793d759)
- [with clause](../part-03-sql-manual/20-sql-references-h-z.md#aff9b6d695a9956c)
- [&lt; cte query hints &gt;](../part-03-sql-manual/15-sql-tuning.md#e6baef4295220339)

<a id="b813fb31fde26de0"></a>
###### **Hierarchy Query**

Hierarchy query 기능이 추가되었다.

- [계층 질의 (Hierarchical Query)](../part-03-sql-manual/12-sql-languages.md#be70d248ca053a9c)
- [hierarchical query clause](../part-03-sql-manual/20-sql-references-h-z.md#d83052c3f143e6bf)

<a id="e3c1ec5d4bb8b966"></a>
##### Control Language

<a id="c4acfdd047b6fa06"></a>
###### **SET SCHEMA**

현재 session의 기본 schema를 변경할 수 있는 [SET SCHEMA schema_name](../part-03-sql-manual/20-sql-references-h-z.md#b3cf2a9e0bb98f09) 구문이 추가되었다.

<a id="0544ad676d75eaf7"></a>
#### PSM Language

변동 사항 없음

<a id="7af7120d1182516d"></a>
### API

<a id="0c047447b93cde74"></a>
#### ODBC

[데이터 원본 스펙 섹션의 키워드](../part-05-developer-manual/31-odbc.md#2df41668cfd6cad9)에 PREFER_IPV6가 추가되었다.

[데이터 원본 스펙 섹션의 키워드](../part-05-developer-manual/31-odbc.md#2df41668cfd6cad9)에 DOT_NET_FOR_ODBC가 추가되었다.

<a id="abfa39970dc8547a"></a>
#### JDBC

[Blob](../part-05-developer-manual/32-jdbc.md#08f843ae785a1ec8)과 [Clob](../part-05-developer-manual/32-jdbc.md#c228a13aa117552a) 중 일부를 지원한다.

[연결 프로퍼티](../part-05-developer-manual/32-jdbc.md#e3c758cdb76c5896)에 prefer_ipv6와 locality_on_demand가 추가되었다.

[Statement Pooling](../part-05-developer-manual/32-jdbc.md#e44dadf3cdf3075c) 기능이 추가되었다.

[Connection](../part-05-developer-manual/32-jdbc.md#e402602131b01bd7) 클래스의 [getNetworkTimeout](../part-05-developer-manual/32-jdbc.md#5a93afbfcec7722b), [setNetworkTimeout](../part-05-developer-manual/32-jdbc.md#c5b3b31684eeb4f3) method를 지원한다.

<a id="cd7e80ea682de241"></a>
#### Embedded SQL

<a id="d02e4771d4adf1bd"></a>
##### Precompiler Option

[--autocommit](../part-05-developer-manual/33-embedded-sql.md#aed2414c2bfbe7a4)이 추가되었다.

gpec에 [--parse](../part-05-developer-manual/33-embedded-sql.md#593831b12b079aa2) 옵션이 추가되었다.

<a id="ca63e76406c3ea47"></a>
##### Embedded SQL 전용 구문

gpec에서 [함수 인자 선언](../part-05-developer-manual/33-embedded-sql.md#54341bc72038b5e4) 을 지원한다.

<a id="57860666616780a5"></a>
##### Host Variable Data Type

변동 사항 없음

<a id="e9e7fabdeac52556"></a>
##### Dynamic SQL

변동 사항 없음

<a id="9cb1db3f543ca1c5"></a>
#### PDO

변동 사항 없음

<a id="608be47588cbf4ea"></a>
#### PyDBC

변동 사항 없음

<a id="dc1b9b34aeda1df5"></a>
#### Ruby

변동 사항 없음

<a id="7d184d0cccabc43a"></a>
#### Hibernate

변동 사항 없음

<a id="3606b1a7128e323c"></a>
### Utility

<a id="99f28ff22d9a4ff1"></a>
#### gcreatedb

변동 사항 없음

<a id="c6c8c34a7d0df736"></a>
#### glsnr

IPv6를 지원한다.

<a id="a782e72b43e6c453"></a>
#### gsql/gsqlnet

변동 사항 없음

<a id="9ac2dc6aaf8f4d63"></a>
#### gloader/gloadernet

Binary 파일의 구조가 변경되었다.

<a id="65e1c1a8dba02d9f"></a>
#### gdump

변동 사항 없음

<a id="66b1c7958c388be3"></a>
#### tablediff

변동 사항 없음

<a id="c1e1266e8d84af1b"></a>
#### gsyncher

변동 사항 없음

<a id="ae6efaa53038472f"></a>
#### gmon

변동 사항 없음

<a id="7c46fc7a19a1cc3d"></a>
#### gtrclogger

변동 사항 없음

<a id="83f55e0bf9cae43a"></a>
#### glocator

변동 사항 없음

<a id="552d38e6e7563353"></a>
#### gagent

변동 사항 없음

<a id="0093325e593ee400"></a>
#### gloctl

변동 사항 없음

<a id="82c97ca50d6a8fb5"></a>
### Replication

<a id="25e6e20770daca79"></a>
#### cyclone

CYCLONE을 운영할 때 연동되는 target database에 IBM DB2 database가 추가되었다.

<a id="ad755f1b7b789fc1"></a>
#### logmirror

변동 사항 없음

<a id="62035823c65b5bc9"></a>
#### cymon

변동 사항 없음

<a id="8653fc2297d28b69"></a>
#### cyfile

CDC 방식을 사용하여 원본 데이터베이스의 transaction을 CSV 형식의 파일로 저장/ 기록하는 툴이 추가되었다.

<a id="477e7f468b205938"></a>
## Patch Notes

<a id="6ec6d9e072f3168d"></a>
### 21c.1.35 Patch Notes

<a id="5b5d824ec03311f9"></a>
#### <kbd>ISSUE-8012</kbd> Redo log archving 시 과도한 디스크 I/O 로 인해 서비스 성능이 저하되는 문제가 있어 이를 수정하였다.

<a id="364c07848a3a0d55"></a>
##### 개요

Redo log archiving 과정에서 과도한 디스크 I/O로 인해 발생하는 서비스 성능 저하 문제를 [ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#453ac01cb35a1161) 프로퍼티를 통해 해결하였다.

<a id="977c42c9c66f535d"></a>
##### 현상 및 증상

Redo log archiving 시 과도한 디스크 I/O로 인해 서비스 성능이 저하되는 현상이 발생한다.

<a id="d0888c4ca29937a1"></a>
##### 수정 전 대처

없음

<a id="484619361fc98ada"></a>
#### <kbd>ISSUE-5452</kbd> Cyclone이 ORACLE과 연동하는 과정에서 LONG VARBINARY 타입 column의 4000byte 초과 데이터가 정상적으로 replication, sync 되지 않는 문제가 있어 이를 수정하였다.

<a id="a4073c00b0383be2"></a>
##### 개요

Cyclone이 ORACLE과 연동하는 과정에서 LONG VARBINARY 타입 column의 4000byte 초과 데이터가 정상적으로 이중화 되지 않는 문제가 있었다.

<a id="b927d841fc1a76dc"></a>
##### 현상 및 증상

GOLDILOCKS-ORACLE 연동 환경에서 cyclone을 통한 replication 및 sync 수행 시, LONG VARBINARY 타입 데이터가 4000byte를 초과할 경우 에러 없이 처리되지만 실제 데이터는 일부만 반영되는 문제가 발생하였다.

<a id="eb609000c7587dbd"></a>
##### 수정 전 대처

없음

<a id="a80f6847029e1cc7"></a>
#### <kbd>ISSUE-7939</kbd> 변별력이 낮은 composite index 추가 시, 기존에 index scan 하던 query를 full scan 하게 되어 이를 수정하였다.

<a id="3bb74ae3ee9da355"></a>
##### 개요

변별력이 낮은 composite index를 추가하면 기존에 index scan 하던 query가 full scan을 수행하는 문제가 발생하여 이를 수정하였다.   
단, 이 문제는 다음 조건을 모두 만족하는 경우에 발생한다.  
• 기존에 사용되던 인덱스가 composite index일 것  
• index key column 전체에 대해 '=' 조건이 존재하지 않고 일부 column에만 '=' 조건이 적용될 것

<a id="40f2a0492ee252c7"></a>
##### 현상 및 증상

다음과 같이 변별력이 높은 column과 낮은 column이 함께 포함된 composite index가 존재하는 경우, 옵티마이저가 기존 index scan 대신 full scan을 선택하는 현상이 발생할 수 있다.

```
DROP TABLE t1;
COMMIT;

CREATE TABLE t1 ( c_good  INTEGER
                , c_bad_1 INTEGER
                , c_bad_2 INTEGER
                , c_bad_3 INTEGER
                , c_bad_4 INTEGER
                , c_bad_5 INTEGER );
                
CREATE INDEX idx1 ON t1( c_good
                       , c_bad_1
                       , c_bad_2
                       , c_bad_3
                       , c_bad_4 );
COMMIT;

BEGIN
   FOR i IN 1 .. 10000 LOOP
       INSERT INTO t1 VALUES ( i, 0, 0, 0, 0, 0 );
   END LOOP;
END;
/

COMMIT;

ANALYZE TABLE t1;
COMMIT;
```

Composite index ( c_good, c_bad_1, c_bad_2, c_bad_3, c_bad_4) 가 존재하고, 해당 index의 모든 key column이 아닌 일부 column ( c_good, c_bad_1, c_bad_2, c_bad_3 )에 대해서만 filter 조건을 사용하는 query가 index scan을 수행하고 있다.

```
\explain plan
SELECT *
  FROM t1
 WHERE c_good  = 999
   AND c_bad_1 = 0    
   AND c_bad_2 = 0
   AND c_bad_3 = 0
;

C_GOOD C_BAD_1 C_BAD_2 C_BAD_3 C_BAD_4 C_BAD_5
------ ------- ------- ------- ------- -------
   999       0       0       0       0       0

1 row selected.

>>>  start print plan

< Execution Plan >
======================================================================
|  IDX  |  NODE DESCRIPTION                |                    ROWS |
----------------------------------------------------------------------
|    0  |  SELECT STATEMENT                |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")     |                       1 |
|    2  |      INDEX ACCESS ("T1", "IDX1") | (         1)          1 |
======================================================================

     1  -  TARGET : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4, T1.C_BAD_5
     2  -  READ INDEX COLUMN : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4
           READ TABLE COLUMN : T1.C_BAD_5
             MIN RANGE : T1.C_GOOD = 999 AND T1.C_BAD_1 = 0 AND T1.C_BAD_2 = 0 AND T1.C_BAD_3 = 0
             MAX RANGE : T1.C_GOOD = 999 AND T1.C_BAD_1 = 0 AND T1.C_BAD_2 = 0 AND T1.C_BAD_3 = 0

<<<  end print plan
```

이 때 아래와 같이 변별력이 낮은 column들로 구성된 composite index가 추가되면, 기존에 index scan을 수행하던 query가 full scan으로 변경될 수 있다.

```
--##########################################
--# 변별력이 낮은 composite index 추가 
--##########################################

CREATE INDEX idx2 ON t1( c_bad_2
                       , c_bad_3 );
COMMIT;

ANALYZE TABLE t1;
COMMIT;

\explain plan
SELECT *
  FROM t1
 WHERE c_good  = 999
   AND c_bad_1 = 0  
   AND c_bad_2 = 0
   AND c_bad_3 = 0
;

C_GOOD C_BAD_1 C_BAD_2 C_BAD_3 C_BAD_4 C_BAD_5
------ ------- ------- ------- ------- -------
   999       0       0       0       0       0

1 row selected.

>>>  start print plan

< Execution Plan >
======================================================================
|  IDX  |  NODE DESCRIPTION                |                    ROWS |
----------------------------------------------------------------------
|    0  |  SELECT STATEMENT                |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")     |                       1 |
|    2  |      TABLE ACCESS ("T1")         |                       1 |
======================================================================

     1  -  TARGET : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4, T1.C_BAD_5
     2  -  READ COLUMN : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4, T1.C_BAD_5
             PHYSICAL FILTER : T1.C_GOOD = 999 AND T1.C_BAD_1 = 0 AND T1.C_BAD_2 = 0 AND T1.C_BAD_3 = 0

<<<  end print plan
```

<a id="bbab232a235075df"></a>
##### 수정 전 대처

INDEX hint를 사용하여 해당 query가 index scan을 수행하도록 강제한다.

```
\explain plan
SELECT /*+ INDEX( t1, idx1) */
       *
  FROM t1
 WHERE c_good  = 999
   AND c_bad_1 = 0  
   AND c_bad_2 = 0
   AND c_bad_3 = 0
;

C_GOOD C_BAD_1 C_BAD_2 C_BAD_3 C_BAD_4 C_BAD_5
------ ------- ------- ------- ------- -------
   999       0       0       0       0       0

1 row selected.

>>>  start print plan

< Execution Plan >
======================================================================
|  IDX  |  NODE DESCRIPTION                |                    ROWS |
----------------------------------------------------------------------
|    0  |  SELECT STATEMENT                |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")     |                       1 |
|    2  |      INDEX ACCESS ("T1", "IDX1") | (         1)          1 |
======================================================================
     1  -  TARGET : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4, T1.C_BAD_5
     2  -  READ INDEX COLUMN : T1.C_GOOD, T1.C_BAD_1, T1.C_BAD_2, T1.C_BAD_3, T1.C_BAD_4
           READ TABLE COLUMN : T1.C_BAD_5
             MIN RANGE : T1.C_GOOD = 999 AND T1.C_BAD_1 = 0 AND T1.C_BAD_2 = 0 AND T1.C_BAD_3 = 0
             MAX RANGE : T1.C_GOOD = 999 AND T1.C_BAD_1 = 0 AND T1.C_BAD_2 = 0 AND T1.C_BAD_3 = 0

<<<  end print plan
```

<a id="1727ee48526f765e"></a>
### 21c.1.34 Patch Notes

<a id="35cd0325d7a1400a"></a>
#### <kbd>ISSUE-7805</kbd> ODBC의 LONG VARCHAR, LONG VARBINARY 타입 처리 과정에서 할당된 메모리가 정상적으로 해제되지 않는 문제가 있어 이를 수정하였다.

<a id="8ee42b99f02377e2"></a>
##### 개요

FETCH 작업 중인 테이블의 스키마 구조가 변경된 뒤 동일 테이블에 대해 다시 FETCH 작업을 수행할 경우, 메타데이터 재구축 과정에서 LONG VARCHAR, LONG VARBINARY 타입 column에 대해 메모리 누수가 발생하였다.

<a id="92d0fbbd444d4c66"></a>
##### 현상 및 증상

클라이언트-서버 (CS) 환경에서 ODBC를 사용해 데이터를 조회하는 과정에서, FETCH 작업 도중 해당 테이블에 대해 ALTER 구문으로 테이블 구조가 변경되면 메타데이터를 재구축한다. 이 때 테이블에 LONG VARCHAR, LONG VARBINARY 타입 column이 존재하면 해당 column 타입에 대해 동적으로 할당된 메모리가 해제되지 않아 메모리 누수가 발생하였다.

<a id="fb5bf2519f6bc520"></a>
##### 수정 전 대처

이 문제가 수정되기 전까지는 fetch 작업 중 테이블 구조를 변경하지 않는 것이 가장 안정적인 방법이다. 부득이하게 테이블 구조가 변경되는 경우에는 해당 SQLHSTMT 핸들에 대해 SQLFreeHandle을 호출한 뒤, SQLAllocHandle 다시 수행하여 핸들을 재할당해야 한다.

<a id="99f3745dba8fc5ab"></a>
### 21c.1.33 Patch Notes

<a id="b1858463d7690b62"></a>
#### <kbd>ISSUE-7782</kbd> gpec에 parse 옵션을 추가하였다.

<a id="dadc3059da917791"></a>
##### 개요

gpec에 소스 파싱 동작을 제어하기 위한 parse 옵션을 추가하였다. 해당 옵션값으로 none 또는 partial을 지정할 수 있으며, 별도로 지정하지 않을 경우 기본값은 partial이다.

<a id="2ca02d2716a837ca"></a>
##### 현상 및 증상

없음

<a id="76d71c5c0180b8db"></a>
##### 수정 전 대처

없음

<a id="b276eea7f27c2bc1"></a>
#### <kbd>ISSUE-7782</kbd> gpec 전처리기의 코드 처리 방식을 수정하였다.

<a id="6bdd9ab031d2cde1"></a>
##### 개요

gpec 전처리기에서 조건이 false로 평가되는 전처리기 분기 (#if, #elif, #else, #ifdef, #ifndef)에 포함된 코드의 처리 방식이 변경되었다.   
기존에는 false 조건에 해당하는 코드를 출력 결과에서 제거하였으나, 패치 이후에는 해당 코드를 삭제하지 않고 그대로 출력하도록 수정하였다.

<a id="07fef9c80d168369"></a>
##### 현상 및 증상

일부 헤더 파일에서 정의된 매크로를 gpec 전처리기가 인식하지 못하는 경우가 있었다. 이 경우 gpec은 전처리기 조건을 false 로 간주하여 관련 코드 전체를 삭제하였다. 그 결과 실제 컴파일 환경에서는 유효한 코드임에도 불구하고 gpec 처리 결과에서는 누락되는 문제가 발생하였다.  
즉, 전처리기 차이에 의해 gpec 결과물이 실제 빌드 결과와 불일치하는 상황이 발생할 수 있었다.

예를 들어, 다음과 같이 gc 파일에서 EXEC SQL INCLUDE 문으로 헤더 파일을 포함하는 경우, 해당 헤더가 다른 헤더에 정의된 매크로를 참조하면 gpec은 해당 매크로를 해석할 수 없으므로 조건을 false로 판단한다. 그 결과 삭제되어서는 안되는 코드가 제거되는 문제가 발생한다.

다음은 gpec에서 참조되지 않은 헤더 파일 예시이다.

```
#ifndef SYS_FLAG_H
#define SYS_FLAG_H
#define SYS_FEATURE_FLAG 1
#endif /* SYS_FLAG_H */
```

다음은 gpec에서 정상적으로 참조된 헤더 파일 예시이다.

```
#ifndef SYS_CONFIG_H
#define SYS_CONFIG_H

/* 다른 헤더에 정의된 매크로를 참조 */
#define ENABLE_FEATURE SYS_FEATURE_FLAG

#endif /* SYS_CONFIG_H */
```

다음은 gc 파일이다.

```
EXEC SQL INCLUDE sys_config.h;
int main(void)
{
#if ENABLE_FEATURE
/* 실제 컴파일 환경에서는 SYS_FEATURE_FLAG == 1 이므로
이 코드가 포함되어야 한다. */
feature_func();
#endif
return 0;
}
```

sys_config.h는 다른 헤더에 정의된 매크로를 참조하고 있으나, gpec은 해당 매크로를 해석하지 못한다. 그 결과 ENABLE_FEATURE 조건이 false로 평가되고, 실제 컴파일 환경에서는 유효한 코드임에도 gpec 처리 결과에서는 삭제된다.

<a id="9f342f422584e8e1"></a>
##### 수정 전 대처

gc 파일에서 사용하는 전처리 조건과 매크로는 EXEC SQL INCLUDE로 포함되는 헤더 파일 내에서 정의되도록 구성한다.

<a id="1afe698514943afe"></a>
#### <kbd>ISSUE-5401</kbd> cyclone recovery 과정 중에도 conflict 이외의 에러가 발생하면 출력하도록 변경하였다.

<a id="08e1a7236208df6b"></a>
##### 개요

기존에는 recovery 과정에서 trace log에 에러를 기록하지 않아 conflict 이외의 에러를 확인할 수 없는 문제가 있어, 이를 수정하였다.

<a id="760c55b0decc652d"></a>
##### 현상 및 증상

기존에는 recovery 과정에서 trace log에 에러를 기록하지 않아 에러 내용을 확인할 수 없었다.

```
[2025-01-24 10:55:17.793633 THREAD(2503,139847152563968)] 
[APPLIER #1(SID:65)] Error Occurred.

[2025-01-24 10:55:17.804159 THREAD(2503,139847100114688)] 
[HEARTBEAT(#0)] Finalize Done.
```

수정 이후에는 recovery 단계에서도 에러가 출력되며, 다음과 같이 확인할 수 있다.

```
[2025-01-24 10:55:17.793568 THREAD(2503,139847152563968)] 
[APPLIER #1(SID:65)-INSERT] ERR-42R01(16357) : must be accessible to at least one member of group 'G2'
  [TABLE_NAME : PUBLIC.TEST]
  [PRIMARY KEY INFO] 
    [NAME:C1, VALUE:101] 

[2025-01-24 10:55:17.793614 THREAD(2503,139847152563968)] 
[Table Information](LSN:232028) - Analyze
 - Master       : PUBLIC.TEST
 - Slave        : PUBLIC.TEST
 - Column Count : 2
 - Physical Id  : 100452

[2025-01-24 10:55:17.793633 THREAD(2503,139847152563968)] 
[APPLIER #1(SID:65)] Error Occurred.

[2025-01-24 10:55:17.793655 THREAD(2503,139847152563968)] 
ERR-HY000(46007): Internal error occurred (ztcdDoInsertNExecute(not unique constraint violated))

[2025-01-24 10:55:17.804159 THREAD(2503,139847100114688)] 
[HEARTBEAT(#0)] Finalize Done.
```

<a id="200ac70cedf10c02"></a>
##### 수정 전 대처

없음

<a id="5f6b666d738d0d32"></a>
#### <kbd>ISSUE-7743</kbd> gpec 전처리기에서 중첩된 #if / #endif 구문을 처리하는 과정에서 발생하던 오류를 수정하였다.

<a id="6dcdee8b298549d8"></a>
##### 개요

gpec 전처리기는 #if 전처리기 구문을 처리할 때, 조건이 false 로 평가되면 해당 #endif 구문까지의 모든 문장을 제거 (빈 문자열로 치환)한다.   
그러나 #if / #endif 구문이 중첩되어 사용되는 경우, 내부 전처리기 블록에 포함된 일부 문장이 정상적으로 제거되지 않는 오류가 확인되어 이를 수정하였다.   
본 수정 사항은 #if 구문뿐만 아니라 #elif, #else, #ifdef, #ifndef 등 모든 조건부 전처리기 구문에 동일하게 적용된다.

<a id="4c3342509d73879b"></a>
##### 현상 및 증상

다음은 중첩된 #if / #endif 구문을 포함한 gc 파일의 일부이다.

```
#if 0
    #if 0
        printf("error 1");
    #else
        printf("error 2");
    #endif
    printf("error 3");
#endif
```

위 코드를 gpec 전처리기를 통해 변환하여 생성된 c 파일의 일부는 다음과 같다.

```
printf("error 3");
```

중첩된 #if 0 조건에 따라 세 개의 printf 문장은 모두 제거되어야 하나, 변환 결과물에는 printf("error 3"); 문장이 남아 있는 문제가 발생하였다.

<a id="49862472c1e7eb40"></a>
##### 수정 전 대처

중첩된 #if, #endif 구문의 사용을 피하거나, 다음과 같이 #endif 구문 이후에 실행 문장을 작성하지 않아야 한다.

```
#if 0
    #if 0
        printf("error 1");
    #else
        printf("error 2");
    #endif                 // 이 구문 이하는 정상적으로 처리 되지 않음.
    printf("error 3");
#endif
```

<a id="bc4d4f381d3da98a"></a>
#### <kbd>ISSUE-7353</kbd> ODBC fetch 중 배열 크기 변경 시 데이터가 누락되는 문제가 있어 이를 수정하였다.

<a id="8e35cf9e8aba2b7e"></a>
##### 개요

ODBC 클라이언트-서버 환경에서 데이터 fetch 도중 배열 크기(array size) 를 동적으로 변경할 때 발생하는 데이터 조회 실패 문제를 수정하였다.

<a id="4293519ed0d9729b"></a>
##### 현상 및 증상

클라이언트-서버(CS) 환경에서 ODBC를 사용하여 데이터를 조회할 때, fetch 작업 도중 배열 크기를 변경하면 데이터를 정상적으로 가져오지 못하는 문제가 발생했다. 이 문제는 SQLExtendedFetch, SQLFetch, SQLFetchScroll 함수를 사용할 때 공통적으로 나타났으며, 특히 작은 배열 크기(예: 1건) 로 fetch를 시작한 후 큰 배열 크기(예: 100건) 로 변경하는 경우에 발생했다.

구체적인 증상으로는 SQL_ROWSET_SIZE 또는 SQL_ATTR_ROW_ARRAY_SIZE 속성을 변경한 후, 실제로는 더 많은 데이터가 존재함에도 불구하고 SQL_NO_DATA가 조기에 반환되어 일부 데이터만 조회되는 현상이 있었다.

<a id="e030462ab2d235be"></a>
##### 수정 전 대처

이 문제가 수정되기 전까지는 fetch 작업 중 배열 크기를 변경하지 않고 고정된 크기로 유지하는 것이 가장 안정적인 방법이다. 만약 배열 크기를 반드시 변경해야 하는 경우라면, SQLCloseCursor 함수를 사용하여 현재 커서를 닫은 후에 쿼리를 다시 실행하여 새로운 배열 크기로 처음부터 fetch를 수행해야 한다. 성능보다 안정성이 중요한 경우에는 배열 크기를 1로 고정하여 단일 행 씩 fetch 하는 방법을 사용할 수 있다.

<a id="c16b87d76572992d"></a>
### 21c.1.32 Patch Notes

<a id="84ebd39e35c16176"></a>
#### <kbd>ISSUE-6939</kbd> IN KEY RANGE scan 시 offset limit 구문을 사용하면 결과에 오류가 발생한다.

<a id="50db3f86c18d2723"></a>
##### 개요

OFFSET 구문이 포함된 질의를 수행할 때 IN KEY RANGE을 이용하면 결과에 오류가 발생하여 이를 수정하였다.

<a id="74c7afe253ec6a2b"></a>
##### 현상 및 증상

OFFSET LIMIT 구문이 포함된 질의에서 IN KEY RANGE scan을 수행하면, OFFSET과 LIMIT 정보가 올바르게 누적되지 않아 사용자가 지정한 값보다 더 큰 OFFSET과 LIMIT이 적용되는 문제가 발생한다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES ( 1 ), ( 2 ), ( 3 ), ( 4 ), ( 5 );

5 rows created.

gSQL> CREATE INDEX IDX_t1 ON t1 ( c1 );

Index created.

gSQL> \EXPLAIN PLAN
SELECT /*+ FULL(t1) */ * FROM t1 WHERE c1 IN ( 2, 3, 5 ) OFFSET 2 LIMIT 10;
    
C1
--
 5

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : T1.C1
     2  -  CLONED 
           READ COLUMN : T1.C1
             PHYSICAL FILTER : ( T1.C1 ) IN ( 2, 3, 5 )

<<<  end print plan


--# BUGBUG
gSQL> \EXPLAIN PLAN
SELECT /*+ IN_KEY_RANGE(t1) */ * FROM t1 WHERE c1 IN ( 2, 3, 5 ) OFFSET 2 LIMIT 10;
    
no rows selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       0 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       0 |
|    2  |      INDEX ACCESS ("T1", "IDX_T1")                           | (         3)          0 |
==================================================================================================

     1  -  TARGET : T1.C1
     2  -  CLONED 
           READ INDEX COLUMN : T1.C1
           IN KEY RANGE
             MIN RANGE : T1.C1 = ?
             MAX RANGE : T1.C1 = ?

<<<  end print plan
```

<a id="6babb729c5f0abdd"></a>
##### 수정 전 대처

없음

<a id="dd2f56a889b8de1b"></a>
### 21c.1.31 Patch Notes

<a id="919f62ce4fbedba8"></a>
#### <kbd>ISSUE-6803</kbd> 잘못된 segment hint 메모리에 접근할 수 있다.

<a id="421471df6f87b6b0"></a>
##### 개요

Segment hint cache의 replacement 발생 횟수가 signed integer 범위 (2147483647)를 초과하면, segment hint 메모리 공간을 벗어나 메모리를 읽거나 쓸 수 있다. 이로 인해 segment fault 및 비정상적인 동작이 발생할 수 있어, 해당 문제를 수정하였다.

<a id="4c87804394c9e5dc"></a>
##### 현상 및 증상

할당된 메모리 범위를 벗어나 읽거나 쓸 수 있으며, 이 경우 segment fault 및 비정상적인 동작을 유발할 수 있다.

<a id="468cab06bdff70de"></a>
##### 수정 전 대처

없음

<a id="735cdfb835cd37ca"></a>
#### <kbd>ISSUE-6797</kbd> Gmaster의 session fatal은 system fatal로 처리한다.

<a id="bfab7653ea580ff3"></a>
##### 개요

Gmaster thread에서 session fatal이 발생하면 hang이 걸려 정상적인 cleanup이 불가능하므로 system fatal로 처리한다.

<a id="10fa4c9e1b741bff"></a>
##### 현상 및 증상

Gmaster thread에서 session fatal이 발생하면 hang이 걸리는 문제가 발생한다.

<a id="f7468e12ba042a37"></a>
##### 수정 전 대처

없음

<a id="d093b15551f75bff"></a>
#### <kbd>ISSUE-6687</kbd> Redo log member가 다중화되어 있을 경우, redo log switch 이후 cyclone이 다음 redo log를 읽지 못하는 현상이 발생한다.

<a id="625a57a1a0ba2c60"></a>
##### 개요

Redo log member가 다중화되어 있을 경우, log switch 이후 cyclone이 이를 정상적으로 처리하지 못하는 현상이 발생하여 이를 수정하였다.

<a id="b36c141b20b674c4"></a>
##### 현상 및 증상

이중화가 이루어지지 않고, cyclone이 지속적으로 다음 파일을 기다리는 현상이 발생한다.

<a id="3287e4c616e9ffeb"></a>
##### 수정 전 대처

Redo log member를 제거하고 cyclone을 재실행한다.

<a id="6409b1439b101b2f"></a>
#### <kbd>ISSUE-6605</kbd> UPSERT statement에서 RETURING 절을 사용하면 결과에 오류가 발생한다.

<a id="71f99541febcf8df"></a>
##### 개요

UPSERT statement에서 RETURNING 절을 사용할 경우, 중복된 키 값이 존재하지 않아 INSERT 연산이 수행될 때 결과에 오류가 발생한다.

<a id="f8849897f82d967c"></a>
##### 현상 및 증상

UPSERT statement에서 RETURNING 절을 사용할 때 RETURNING 절에 명시된 column 순서가 base table의 column 구성 순서와 다르면 결과에 오류가 발생한다.

```
gSQL> CREATE TABLE t1( c1 INTEGER, c2 INTEGER, c3 INTEGER );

Table created.

gSQL> CREATE UNIQUE INDEX uni_idx_t1 ON t1 ( c1 );

Index created.

--# BUGBUG
--# result :   1   3
gSQL> INSERT INTO t1 VALUES ( 1, 2, 3 ) ON DUPLICATE KEY DO UPDATE c1 = c1 + 1 RETURN c1, c3;

C1 C3
-- --
 1  2

1 row created.

--# BUGBUG
--# result :   1   2   3
gSQL> SELECT * FROM t1;

C1 C2   C3
-- -- ----
 1  2 null

1 row selected.
```

<a id="81b78f4e3ec7de64"></a>
##### 수정 전 대처

없음

<a id="bbff61ba2033b752"></a>
#### <kbd>ISSUE-6575</kbd> Fetch statement의 INTO 절에 record type variable의 field만 명시하면 에러가 발생한다.

<a id="954a5e64c3dab5a5"></a>
##### 개요

Fetch statement에 fetch 하려는 cursor의 target 수와 INTO 절의 target 수가 동일함에도 record type variable의 field를 명시하면 에러가 발생한다.

<a id="86b36fb9b042b5d5"></a>
##### 현상 및 증상

Cursor의 SELECT statement의 target 수와 fetch into 절의 target 수가 동일함에도 에러가 발생한다.

```
gSQL>
DECLARE
  TYPE rec1 IS RECORD( c1 INTEGER , c2 INTEGER );
  v_rec rec1;
  
  CURSOR cur1 IS SELECT 100 FROM dual;
BEGIN
  OPEN cur1;
  FETCH cur1 INTO v_rec.c2;
  CLOSE cur1;
END;
/

ERR-2F000(17032): PSM compilation error : 
(1) at (8:3): ERR-2F000(17040): fetch target count mismatch
```

현재는 정상 동작하도록 수정되었다.

```
gSQL>
DECLARE
  TYPE rec1 IS RECORD( c1 INTEGER , c2 INTEGER );
  v_rec rec1;
  
  CURSOR cur1 IS SELECT 100 FROM dual;
BEGIN
  OPEN cur1;
  FETCH cur1 INTO v_rec.c2;
  CLOSE cur1;
END;
/

Anonymous PL block executed.
```

<a id="68683bc4d60342f1"></a>
##### 수정 전 대처

Scalar type variable을 사용한다.

```
gSQL>
DECLARE
  TYPE rec1 IS RECORD( c1 INTEGER , c2 INTEGER );
  v_rec rec1;
  
  var1 INTEGER;
  
  CURSOR cur1 IS SELECT 100 FROM dual;
BEGIN
  OPEN cur1;
  FETCH cur1 INTO var1;
  v_rec.c2 := var1;
  CLOSE cur1;
END;
/

Anonymous PL block executed.
```

<a id="309fd499468503da"></a>
### 21c.1.30 Patch Notes

<a id="57608c9ba8df9aa8"></a>
#### <kbd>ISSUE-6358</kbd> Weak memory ordering 장비에서 cache coherency 문제가 발생하여 이를 수정하였다.

<a id="d07f3b0a378886ee"></a>
##### 개요

Weak memory ordering 장비에서 memory 접근 순서가 program order와 달라져 서버가 비정상적으로 종료되는 현상이 발생하여 이를 수정하였다.

<a id="33ed6e3d42247ca1"></a>
##### 현상 및 증상

메모리에 있는 최신 data가 아닌 CPU cache에 있는 old data를 사용함으로써 서버가 오동작하거나 비정상적으로 종료될 수 있다.

<a id="dad467defa1a1057"></a>
##### 수정 전 대처

없음

<a id="1744a1438805331f"></a>
#### <kbd>ISSUE-6557</kbd> Outer join을 사용할 때, where 절에 right table의 column이 포함된 DECODE, stored function, concat과 같은 함수가 존재하면 잘못된 결과가 도출될 수 있다.

<a id="d43c46dc8a6d6bbf"></a>
##### 개요

Where 절에 right table의 column이 포함된 DECODE, stored function, concat과 같은 함수가 존재할 경우, 아래와 같은 outer join operation elimination이 적용되어서는 안 되지만 실제로는 적용되는 문제가 발생했다.

- Left outer join이 inner join으로 transform 되었다.
- Full outer join이 left outer join으로 transform 되었다.

<a id="46912499777943ad"></a>
##### 현상 및 증상

다음과 같이 outer join operation elimination이 발생하는 경우, where 절에 DECODE, stored function 등이 포함되면 잘못된 결과가 도출된다.

수정 전에는 다음과 같이 잘못된 결과가 도출되었다.

```
CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER );
INSERT INTO t1 VALUES(1,1);
INSERT INTO t1 VALUES(2,2);
CREATE TABLE t2 ( c1 INTEGER, c2 INTEGER );
INSERT INTO t2 VALUES(1,1);
COMMIT;


gSQL> \EXPLAIN PLAN 
SELECT t1.c1, t2.c1
  FROM t1 LEFT OUTER JOIN t2
    ON t1.c1 = t2.c1
 WHERE DECODE( t2.c2, NULL, 'A', 'B' ) = 'A'
; 

no rows selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (INNER JOIN)                                  |
|    3  |        TABLE ACCESS ("T1")                                   |
|    4  |        HASH JOIN INSTANT                                     |
|    5  |          TABLE ACCESS ("T2")                                 |
========================================================================

     1  -  TARGET : T1.C1, T2.C1
     2  -  JOINED COLUMN : T1.C1, T2.C1
     3  -  READ COLUMN : T1.C1
     4  -  HASH KEY : T2.C1
           READ KEY COLUMN : T2.C1
             HASH FILTER : T2.C1 = T1.C1
     5  -  READ COLUMN : T2.C1, T2.C2
             LOGICAL FILTER : DECODE(T2.C2,NULL,'A','B') = 'A'

<<<  end print plan
```

수정 후, 올바른 plan과 결과는 다음과 같다.

```
\EXPLAIN PLAN 
SELECT t1.c1, t2.c1
  FROM t1 LEFT OUTER JOIN t2
    ON t1.c1 = t2.c1
 WHERE DECODE( t2.c2, NULL, 'A', 'B' ) = 'A'
;

C1   C1
-- ----
 2 null

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (LEFT OUTER JOIN)                             |
|    3  |        TABLE ACCESS ("T1")                                   |
|    4  |        HASH JOIN INSTANT                                     |
|    5  |          TABLE ACCESS ("T2")                                 |
========================================================================

     1  -  TARGET : T1.C1, T2.C1
     2  -  JOINED COLUMN : T2.C2, T1.C1, T2.C1
             WHERE FILTER : DECODE(T2.C2,NULL,'A','B') = 'A'
     3  -  READ COLUMN : T1.C1
     4  -  HASH KEY : T2.C1
           RECORD COLUMN : T2.C2
           READ KEY COLUMN : T2.C1, T2.C2
             HASH FILTER : T2.C1 = T1.C1
     5  -  READ COLUMN : T2.C1, T2.C2

<<<  end print plan
```

<a id="dbde55193f39a059"></a>
##### 수정 전 대처

다음과 같이 NO_QUERY_TRANSFORMATION hint를 사용한다.

```
\EXPLAIN PLAN 
SELECT /*+ NO_QUERY_TRANSFORMATION */
       t1.c1, t2.c1
  FROM t1 LEFT OUTER JOIN t2
    ON t1.c1 = t2.c1
 WHERE DECODE( t2.c2, NULL, 'A', 'B' ) = 'A'
;

C1   C1
-- ----
 2 null

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (LEFT OUTER JOIN)                             |
|    3  |        TABLE ACCESS ("T1")                                   |
|    4  |        HASH JOIN INSTANT                                     |
|    5  |          TABLE ACCESS ("T2")                                 |
========================================================================

     1  -  TARGET : T1.C1, T2.C1
     2  -  JOINED COLUMN : T2.C2, T1.C1, T2.C1
             WHERE FILTER : DECODE(T2.C2,NULL,'A','B') = 'A'
     3  -  READ COLUMN : T1.C1
     4  -  HASH KEY : T2.C1
           RECORD COLUMN : T2.C2
           READ KEY COLUMN : T2.C1, T2.C2
             HASH FILTER : T2.C1 = T1.C1
     5  -  READ COLUMN : T2.C1, T2.C2

<<<  end print plan
```

<a id="b88491180a66c642"></a>
#### <kbd>ISSUE-6537</kbd> CAST( 'ABCDE' AS CHAR(3) ) 와 같이 string type 간에 cast 연산 시, source value가 dest precision 보다 크면 에러가 발생한다.

<a id="8760f1722792791d"></a>
##### 개요

CAST( 'ABCDE' AS CHAR(3) ) 와 같이 string type 간에 cast 연산 시, source value가 dest precision 보다 크면 에러가 발생한다.

이 경우, 변환하려는 string type의 precision에 맞춰 truncate 하여 cast 연산이 수행되게 한다.

<a id="44ef0ecfe9fbffa8"></a>
##### 현상 및 증상

수정 전에는 다음과 같이 에러가 발생하였다.

```
DROP TABLE t1;
CREATE TABLE t1 ( c1 CHAR( 5 ) );
INSERT INTO t1 VALUES ( 'ABCDE' );
COMMIT;

gSQL> SELECT CAST( c1 AS CHAR(3) ) FROM t1;
ERR-22001(12002): byte length of data greater than column length :
SELECT CAST( c1 AS CHAR(3) ) FROM t1
       *
ERROR at line 1:
```

수정 후, 변환하려는 string type의 precision에 맞춰 truncate가 이루어지고, 그에 따라 cast 연산이 수행된다.

```
gSQL> SELECT CAST( c1 AS CHAR(3) ) FROM t1;
CAST( C1 AS CHAR(3) )
---------------------
ABC                  
1 row selected.
```

<a id="00064779d23c7164"></a>
##### 수정 전 대처

변환하려는 string type의 precision을 source value가 포함될 수 있는 크기로 지정한다.

<a id="e2c4c7822a55fbe8"></a>
#### <kbd>ISSUE-6536</kbd> Bulk logging 으로 인한 DML jitter 현상을 제거하였다.

<a id="52bcb9d418eced2b"></a>
##### 개요

Online index rebuild 중에 발생한 대량의 로그로 인해 DML에서 jitter가 발생하는 현상을 제거하였다.

<a id="0e1b4c95798ac722"></a>
##### 현상 및 증상

대량 로그는 log flusher를 느리게 만들고 이로 인해 online index rebuild가 lock을 잡고 있는 시간이 늘어나 DML 지연 현상을 유발할 수 있다.

[INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#e613f53aef76fcfb) 프로퍼티를 새로 추가하였다. 이를 이용하면 index rebuild 시 대량 로그가 짧은 시간 안에 기록되는 것을 방지할 수 있다.

<a id="1d45ce38f61653f3"></a>
##### 수정 전 대처

없음

<a id="1126796500d85341"></a>
#### <kbd>ISSUE-6543</kbd> 두 개 이상의 멤버에서 동시에 startup phase를 global open으로 올리면 서버가 비정상 종료된다.

<a id="6cf32d054828aa12"></a>
##### 개요

두 개 이상의 멤버에서 동시에 startup phase를 global open 단계로 올리면 서버가 비정상 종료되는 현상을 제거하였다.

<a id="3f45b84b5b5309d2"></a>
##### 현상 및 증상

두 개 이상의 멤버에서 동시에 startup phase를 global open 단계로 올리면 서버에 hang이 걸리거나 비정상 종료된다.

<a id="58a6dae11a1ecc0d"></a>
##### 수정 전 대처

한 개의 멤버에서만 startup phase를 global open 단계로 올려야 한다.

<a id="93c0671040ce87a3"></a>
#### <kbd>ISSUE-5544</kbd> Cluster 환경에서 cyclone을 사용하여 이중화 하는 도중에 master 와의 연결이 종료되어 트랜잭션 처리에 실패할 경우, rollback logic이 대기한다.

<a id="222e70694e806583"></a>
##### 개요

1. Cluster 이중화 환경에서만 발생한다. Cyclone을 사용하여 이중화하는 도중에 master가 종료되어 slave 측에서 트랜잭션 처리에 실패했을 때 이전에 처리되던 트랜잭션을 rollback 하면 cyclone이 대기하는 현상이 발생할 수 있다.

2. 이를 해결하기 위하여 slave의 rollback 로직을 제거하고, 데이터를 모두 저장한 후에 트랜잭션을 실행하도록 수정하였다.

<a id="99051b57a6650a78"></a>
##### 현상 및 증상

경우에 따라 다음과 같은 내용이 slave trace log에 지속적으로 기록되며, 대기 현상이 계속될 수 있다.

```
[RECEIVER(#2)] [INFO]WAIT_WRITE_RESTART_INFO_FOR_SKIP(AnalyzeState = 1)SCN(705:10166:18)
```

<a id="81c2e5d418cc0ce7"></a>
##### 수정 전 대처

없음

<a id="7a7d061640ecc7bd"></a>
#### <kbd>ISSUE-4334</kbd> Global Open 으로 상승할 때 SCN 차이로 인해 노드 JOIN에 실패한다.

<a id="bb2f4a78c886bfa7"></a>
##### 개요

특정 멤버의 scn이 cluster의 최대 scn 보다 작아서 cluster에 조인하지 못하는 현상이 있어 이를 수정하였다.

<a id="93d2cc4a9bcbb830"></a>
##### 현상 및 증상

다음과 같은 에러와 함께 Global Open 으로 올라오지 못하는 현상이 발생한다.

```
gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

ERR-42000(16410): Startup driver node must have the latest data - a suitable startup driver node is 'G1N1' member
```

<a id="4c2ae9a67aaabce7"></a>
##### 수정 전 대처

없음

<a id="7494de2c26b93a3f"></a>
#### <kbd>ISSUE-6255</kbd> [CDC] trace log에 기록되는 connection string에 PWD 항목이 노출되어, 이를 '*' 으로 대체하여 기록되도록 하였다.

<a id="931cba44cedc6839"></a>
##### 개요

cyclone, cymon, cyfile 에서 trace log에 기록되는 connection string에 PWD 항목이 노출되어, 이를 '*' 으로 대체하여 기록되도록 수정하였다.

<a id="ed0707daf123d7e7"></a>
##### 현상 및 증상

cyclone, cymon, cyfile 에서 connection string 에 PWD 항목이 노출되어 trace log에 기록되었다.

```
connection string [PROTOCOL=DA;DSN=goldilocks_jinsil;PORT=11100;UID=test;PWD=test]
```

<a id="c63ce19d1a464b2a"></a>
##### 수정 전 대처

없음

<a id="c68121291827c66a"></a>
#### <kbd>ISSUE-6030</kbd> Cluster 환경에서 Member의 Rebalance를 수행할 때 Cyclone에 발생하는 오류를 수정하였다.

<a id="8439952220c2b674"></a>
##### 개요

Cluster 환경에서 Cyclone 운영 중인 상황에서 Cluster Member의 Rebalance를 수행하면 Cyclone에서 이를 정상적으로 처리하지 못하는 현상이 있어 이를 수정하였다.

<a id="ea9ecfe469c04709"></a>
##### 현상 및 증상

Rebalance가 수행된 Cluster Member에서 동작하는 Cyclone에서 다음과 같은 내용이 기록되고 더 이상 진행이 되지 않았다.

```
[2023-12-08 16:33:58.782398 THREAD(3292,140620625983232)] 
Ready to Rebalance-Tx commit. (Waiting for slave response)
```

<a id="a14b619abdfeabfc"></a>
##### 수정 전 대처

없음

<a id="4c30d262ad300cb9"></a>
#### <kbd>ISSUE-6231</kbd> 유효하지 않은 IP 를 가지고 GLOBAL OPEN 으로 진입하는 경우 에러가 발생한다.

<a id="fe636eed69d6f3d6"></a>
##### 개요

유효하지 않은 원격 IP 를 가지고 GLOBAL OPEN 으로 올라가려 할 때 실패하는 현상이 있어 이를 수정하였다.

<a id="091490595ddd1945"></a>
##### 현상 및 증상

유효하지 않은 원격 IP 를 가지고 GLOBAL OPEN 으로 올라가려 할 때 그 노드를 제외하고 GLOBAL OPEN 으로 올라가야 하는데 다음과 같이 실패한다.

```
gSQL> alter system open global database;

ERR-HY000(11047): MEMBER(G1N2): invalid network address : invalid address()
```

<a id="023a1b107525ab0e"></a>
##### 수정 전 대처

ALTER CLUSTER LOCATION 구문을 사용해 문제가 발생한 노드의 IP 를 유효한 IP로 변경한다.

```
gSQL> alter cluster location g1n2 host '127.0.0.1' port 12150;

altered.
```

<a id="61b316108fce0f1a"></a>
### 21c.1.29 Patch Notes

<a id="dba298e242c2d276"></a>
#### <kbd>ISSUE-5933</kbd> 서버가 cluster failover를 진행하면 glocator에서 멈춰 있는 현상이 있다.

<a id="d07e79b0be4c9bc5"></a>
##### 개요

서버 속성 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 또는 2로 설정되고 cluster failover 과정에서 glocator가 패킷을 받기 위해 대기하고 있다.

<a id="a61b1ff06a7f911a"></a>
##### 현상 및 증상

Cluster failover 과정에서 glocator가 gagent와 통신을 하는 도중에 gagent로부터 패킷을 받지 못하고 대기하고 있다.

<a id="d4d4199ec898edb1"></a>
##### 수정 전 대처

없음

<a id="8c2bd42dcc6e8788"></a>
#### <kbd>ISSUE-5862</kbd> JDBC, Connection 클래스에 getNetworkTimeout, setNetworkTimeout method를 지원한다.

<a id="f69ea14c30fa5514"></a>
##### 개요

Connection 클래스에 getNetworkTimeout, setNetworkTimeout method를 지원한다.

<a id="ae3024962266ea7e"></a>
##### 현상 및 증상

없음

<a id="4ccbf7b8a831d596"></a>
##### 수정 전 대처

없음

<a id="074533a234182dc6"></a>
#### <kbd>ISSUE-5862</kbd> JDBC, connection 객체를 멀티 thread에서 공유하고 thread stop 또는 interrupt로 thread를 종료하면 프로그램에 hang이 걸린다.

<a id="5a564c24b85e10bb"></a>
##### 개요

Connection 객체를 여러 thread에서 공유하고 statement 객체를 개별로 사용하는 프로그램에서 각 thread를 Thread.stop() 또는 Thread.interrupt()로 종료시키면 프로그램에 hang이 걸린다.

<a id="bd4ef2e2fb8f53e7"></a>
##### 현상 및 증상

Thread.stop() 또는 Thread.interrupt() 메소드를 사용하여 thread를 종료하면 통신 과정에서 문제가 생길 수 있다. 따라서 통신 과정에서 thread가 비정상 종료하면 connection 객체는 closed 상태로 처리했어야 한다. 통신 과정에서 프로토콜이 어긋나고 connection 객체가 open 된 상태에서 다른 thread가 connection 객체를 사용하다 보니 프로그램이 대기 상태로 멈춰 있는 현상이 발생한다.

<a id="0954f6fe27afb831"></a>
##### 수정 전 대처

없음

<a id="e3147e0d24d6b3b7"></a>
#### <kbd>ISSUE-5799</kbd> CREATE TABLE/ ALTER TABLE을 수행할 때 default expression이 valid 하지 않음에도 에러가 발생하지 않았다.

<a id="c69fab993927ebfb"></a>
##### 개요

CREATE TABLE/ ALTER TABLE을 수행할 때 default clause를 정의하면 default expression이 valid 한지 체크한다.

<a id="37918bb516683bfa"></a>
##### 현상 및 증상

default expression이 valid하지 않음에도 에러가 발생하지 않았다.

```
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

Table created.
```

현재는 다음과 같이 에러가 발생하도록 수정하였다.

```
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

ERR-22012(12122): divisor is equal to zero
```

<a id="4ed2fb3285516363"></a>
##### 수정 전 대처

없음

<a id="40aa1eaf8a443460"></a>
#### <kbd>ISSUE-5828</kbd> ROWNUM을 포함한 join 질의는 원격 노드로 보낼 수 없는데 보내는 경우가 있다.

<a id="5a33c1062746df90"></a>
##### 개요

ROWNUM을 포함한 join 질의는 원격 노드로 보낼 수 없다. Clone 테이블이라 하더라도 각 노드마다 data의 저장 순서가 다를 경우, 잘못된 결과가 도출될 수 있다.

<a id="6bea138764a3837f"></a>
##### 현상 및 증상

```
\explain plan
SELECT COUNT(*)
  FROM ( SELECT c1
           FROM t_clone
          WHERE ROWNUM <= 1000
       ) X
     , t_shard Y
 WHERE X.c1 = Y.c1
; 

COUNT(*)
--------
    1005

1 row selected.

>>>  start print plan

< Execution Plan >
============================================================================
|IDX| NODE DESCRIPTION                                                     |
----------------------------------------------------------------------------
|  0|  SELECT STATEMENT                                                    |
|  1|    QUERY BLOCK ("$QB_IDX_2")                                         |
|  2|      SINGLE CLUSTER                                                  |
|  3|        CLUSTER PUSHER ("_$NI_6")                                     |
|  4|          INLINE_VIEW ("X")                                           |
|  5|            QUERY BLOCK ("$QB_IDX_6")                                 |
|  6|              COUNT                                                   |
|  7|                TABLE ACCESS ("T_CLONE")                              |
|  8|        AGGREGATION BY HASH                                           |
|  9|          NESTED JOIN (INNER JOIN)                                    |
| 10|            PUSHER TABLE ACCESS ("_$NI_6")                            |
| 11|            INDEX ACCESS ("T_SHARD" AS Y, "T_SHARD_PRIMARY_KEY_INDEX")|
============================================================================

     1  -  TARGET : COUNT(*)
     2  -  SQL : SELECT /*+ KEEP_JOINED_TABLE USE_HASH_IN( _A1, 7801 ) NO_MERGE( _A2 ) INDEX( _A1, "PUBLIC"."T_SHARD_PRIMARY_KEY_INDEX" ) */ COUNT(*) FROM ( ( SELECT /*+ FULL( _A3 ) */ "_A3"."C1" FROM "PUBLIC"."T_CLONE"@LOCAL AS "_A3" WHERE ROWNUM <= :_V0 ) AS "_A2"("C1") INNER JOIN "PUBLIC"."T_SHARD"@LOCAL AS "_A1" ON "_A1"."C1" = "_A2"."C1") ALIAS "_A4"
           TARGET DOMAIN : G1(G1N1) 1 rows, G2(G2N1) 1 rows, G3(G3N1) 1 rows
           RE-AGGREGATION
             AGGREGATION : SUM( COUNT(*) )
     4  -  TARGET : COUNT(*)
     5  -  AGGREGATION : COUNT(*)
     6  -  JOINED COLUMN : NOTHING
     7  -  COLUMN : _A3.C1 AS C1
     8  -  TARGET : _A3.C1
     9  -  STOP KEY FILTER : ROWNUM <= :_V0
    10  -  CLONED 
           READ COLUMN : _A3.C1
    11  -  HASH KEY : _A1.C1
           READ KEY COLUMN : _A1.C1
             HASH FILTER : _A1.C1 = _A2.C1
           FETCH ONE ROW
    12  -  HASH SHARD ( # 3 ) 
           READ INDEX COLUMN : _A1.C1

<<<  end print plan
```

ROWNUM을 포함한 join 질의는 원격 노드로 보낼 수 없는데, 위 질의를 보면 ROWNUM filter를 원격 질의 노드로 보내고 있다.

<a id="95b1a58c3827dd55"></a>
##### 수정 전 대처

/*+ LOCAL_JOIN(Y) */ hint를 사용한다.

<a id="ad4711a6d4d6d433"></a>
### 21c.1.28 Patch Notes

<a id="a408b1d7d93fb5eb"></a>
#### <kbd>ISSUE-5810</kbd> [CYCLONE] long varchar column을 포함하는 테이블에 record가 없으면 SYNC에 실패한다.

<a id="ceb2105645d91c92"></a>
##### 개요

SYNC 할 때 master의 해당 테이블의 record 유무를 확인하는 과정 중에 long varchar column에 대한 null 체크가 잘못되어 발생한다. 실제 record가 없음에도 불구하고 record가 있다고 판단하여 null 데이터를 slave로 INSERT 시도하며, 이로 인하여 "cannot insert NULL into " 관련 에러 메시지를 출력한 뒤 SYNC에 실패한다.

<a id="58899f73ad8239b1"></a>
##### 현상 및 증상

CYCLONE을 이용한 이중화에서 SYNC 기능을 사용하여 master의 데이터를 slave로 옮기는 과정에서 long varchar column을 포함하는 테이블에 record가 없으면 "cannot insert NULL into" 관련 에러가 발생하며, SYNC에 실패한다.

<a id="5ee2d1c6ae63bc3c"></a>
##### 수정 전 대처

없음

<a id="a5aa2fa5a087a7f6"></a>
### 21c.1.27 Patch Notes

<a id="4755a56d7620d59e"></a>
#### <kbd>ISSUE-5740</kbd> DDL 수행을 막을 수 있는 프로퍼티를 추가하였다.

<a id="1b89eff4f5d3759b"></a>
##### 개요

DDL 수행을 막을 수 있는 프로퍼티를 추가하였다.

- [DISABLE_DDL](../part-02-administration-manual/10-server-property.md#5304e2d2d318a2c8)
- [DISABLE_SERIAL_DDL](../part-02-administration-manual/10-server-property.md#877f3ecf2a376572)

<a id="4a83d584f743ce69"></a>
##### 현상 및 증상

없음

<a id="198c4acb641e9597"></a>
##### 수정 전 대처

없음

<a id="759d0676ace1e949"></a>
#### <kbd>ISSUE-5665</kbd> 세 개 이상의 테이블이 포함된 join이 instant nested loop join method 방식으로 수행되면 잘못된 결과가 도출될 수 있다.

<a id="536caf60002913a7"></a>
##### 개요

세 개 이상의 테이블이 포함된 join이 instant nested loop join method 방식으로 수행되면 잘못된 결과가 도출될 수 있다.

<a id="6e49401aec17d53d"></a>
##### 현상 및 증상

```
--# result : 27
\EXPLAIN PLAN
SELECT COUNT(t2.col1)
  FROM t2, t3, t4, t1
 WHERE t2.col1 + t1.col1 = t4.col1
   AND t3.col1 + t1.col1 = t4.col1;

COUNT(T2.COL1)
--------------
             0

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      AGGREGATION BY HASH                                     |
|    3  |        NESTED JOIN (INNER JOIN)                              |
|    4  |          TABLE ACCESS ("T1")                                 |
|    5  |          SORT JOIN INSTANT                                   |
|    6  |            NESTED JOIN (INNER JOIN)                          |
|    7  |              NESTED JOIN (INNER JOIN)                        |
|    8  |                INDEX ACCESS ("T2", "T2_COL1")                |
|    9  |                INDEX ACCESS ("T3", "T3_COL1")                |
|   10  |              INDEX ACCESS ("T4", "T4_COL1")                  |
========================================================================

     1  -  TARGET : COUNT( T2.COL1 )
     2  -  AGGREGATION : COUNT( T2.COL1 )
     3  -  JOINED COLUMN : T2.COL1
     4  -  READ COLUMN : T1.COL1
     5  -  SORT KEY : "T4.COL1 ASC NULLS LAST"
           RECORD COLUMN : T2.COL1
           READ KEY COLUMN : T4.COL1
           READ RECORD COLUMN : T2.COL1
             MIN RANGE : T4.COL1 = T2.COL1 + {T1.COL1} AND T4.COL1 = T3.COL1 + {T1.COL1}
             MAX RANGE : T4.COL1 = T2.COL1 + {T1.COL1} AND T4.COL1 = T3.COL1 + {T1.COL1}
     6  -  JOINED COLUMN : T4.COL1, T2.COL1, T3.COL1
     7  -  JOINED COLUMN : T2.COL1, T3.COL1
     8  -  READ INDEX COLUMN : T2.COL1
     9  -  READ INDEX COLUMN : T3.COL1
    10  -  READ INDEX COLUMN : T4.COL1

<<<  end print plan
```

위 질의의 결과는 '27' 이어야 하지만 실제 결과는 '0' 이 도출된다.

WHERE 절 조건 'T4.COL1 = T2.COL1 + T1.COL1 AND T4.COL1 = T3.COL1 + T1.COL1'은 index range 조건으로 사용될 수 없는데 실제로는 사용되고 있다.

문제를 수정하면 다음과 같이 결과가 정상적으로 도출된다.

```
\EXPLAIN PLAN
SELECT COUNT(t2.col1)
  FROM t2, t3, t4, t1
 WHERE t2.col1 + t1.col1 = t4.col1
   AND t3.col1 + t1.col1 = t4.col1;

COUNT(T2.COL1)
--------------
            27

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      AGGREGATION BY HASH                                     |
|    3  |        NESTED JOIN (INNER JOIN)                              |
|    4  |          NESTED JOIN (INNER JOIN)                            |
|    5  |            NESTED JOIN (INNER JOIN)                          |
|    6  |              INDEX ACCESS ("T2", "T2_COL1")                  |
|    7  |              INDEX ACCESS ("T3", "T3_COL1")                  |
|    8  |            INDEX ACCESS ("T4", "T4_COL1")                    |
|    9  |          FLAT JOIN INSTANT                                   | 
|   10  |            TABLE ACCESS ("T1")                               |
========================================================================

     1  -  TARGET : COUNT( T2.COL1 )
     2  -  AGGREGATION : COUNT( T2.COL1 )
     3  -  JOINED COLUMN : T3.COL1, T1.COL1, T4.COL1, T2.COL1
             ON FILTER : ( T3.COL1 + T1.COL1 ) = T4.COL1 AND ( T2.COL1 + T1.COL1 ) = T4.COL1
     4  -  JOINED COLUMN : T3.COL1, T4.COL1, T2.COL1
     5  -  JOINED COLUMN : T3.COL1, T2.COL1
     6  -  READ INDEX COLUMN : T2.COL1
     7  -  READ INDEX COLUMN : T3.COL1
     8  -  READ INDEX COLUMN : T4.COL1
     9  -  RECORD COLUMN : T1.COL1
           READ COLUMN : T1.COL1
    10  -  READ COLUMN : T1.COL1

<<<  end print plan
```

<a id="d45b52b5e7e59176"></a>
##### 수정 전 대처

USE_INL(t1) 외의 다른 hint를 사용한다. 예를 들면 USE_NL(t1), USE_HASH(t1), USE_MERGE(t1) 등을 사용한다.

<a id="78a59a2343aefa33"></a>
#### <kbd>ISSUE-5447</kbd> CYCLONE 이중화 중, rollback 된 transaction이 이중화되는 경우가 있어 이를 수정하였다.

<a id="8d5a3dc25ca6fcd7"></a>
##### 개요

Unique key 없이 primary key가 존재하는 table을 이중화하는 경우에 발생한다. CYCLONE master로 운영 중인 database에서 수행된 transaction이 PK constraint 위배로 rollback 된 statement를 포함하고 있는 경우, 해당 transaction이 의도치 않게 이중화된다. 이 경우, CYCLONE slave에서도 이중화가 동일하게 수행되어 PK constraint 위배 오류가 CYCLONE 로그에 기록된다.

<a id="1c3cda2e5d8f3dbc"></a>
##### 현상 및 증상

```
CREATE TABLE T1
(
   I1 INTEGER PRIMARY KEY,
   I2 VARCHAR(10)
)
COMMIT;

INSERT INTO T1 VALUES ( 1, 'TEST1' );
COMMIT;

INSERT INTO T1 VALUES ( 1, 'TEST1' );
ERR-23000(16057): unique constraint (PUBLIC.T1_PRIMARY_KEY) violated
COMMIT;
```

<a id="a700b892a9308e55"></a>
##### 수정 전 대처

없음

<a id="96a0bc9018ae3788"></a>
#### <kbd>ISSUE-5695</kbd> 디스크 테이블스페이스 확장할 때 hang 걸리는 문제가 있다.

<a id="c8791c2d96e7d40c"></a>
##### 개요

NEXT의 크기가 128 MB 이상으로 설정된 테이블스페이스를 확장할 때 hang에 빠지는 문제가 있다.

<a id="52aa57ba3d7d41df"></a>
##### 현상 및 증상

```
DROP TABLESPACE TEST_TBS INCLUDING CONTENTS AND DATAFILES;
COMMIT;

CREATE DISK TABLESPACE TEST_TBS
   DATAFILE 'test.dbf' SIZE 256M AUTOEXTEND ON NEXT 128M MAXSIZE 512M;

CREATE TABLE T1
(
   I1 INTEGER,
   I2 CHAR(2000),
   I3 CHAR(2000),
   I4 CHAR(2000),
   I5 CHAR(1000)
)
TABLESPACE TEST_TBS;
COMMIT;

INSERT INTO T1 VALUES ( 1, 1, 1, 1, 1 );
INSERT INTO T1 SELECT * FROM T1 LIMIT 8192;
INSERT INTO T1 SELECT * FROM T1 LIMIT 8192;
...(생략)...
INSERT INTO T1 SELECT * FROM T1 LIMIT 8192;  -- hang
```

<a id="915934c2ab2c0351"></a>
##### 수정 전 대처

테이블스페이스의 NEXT 크기를 128 MB 이하로 설정한다.

<a id="4fb779ea25576771"></a>
#### <kbd>ISSUE-5667</kbd> Subquery에서 외부 query를 참조할 때, materialized view와 일반 table 모두를 참조하면 비정상 종료할 수 있다.

<a id="d6c1d33211cc379a"></a>
##### 개요

다음 조건을 모두 만족하면 비정상 종료한다.

1. &lt;from clause&gt;에 table이 나열될 때, &lt;with clause&gt;에 의해 명시된 materialized view가 먼저 나열되고 일반 table이 나열된다.
2. Subquery가 있고, 그 subquery가 materialized view와 일반 테이블을 모두 참조한다.

<a id="fe74f5145403fcb9"></a>
##### 현상 및 증상

```
DROP TABLE IF EXISTS r;
DROP TABLE IF EXISTS s;
DROP TABLE IF EXISTS t;

CREATE TABLE r ( c1 INTEGER, c2 INTEGER );
INSERT INTO r VALUES(1,1);

CREATE TABLE s ( c1 INTEGER, c2 INTEGER, c3 INTEGER );
INSERT INTO s VALUES(1,1,1);

CREATE TABLE t ( c1 INTEGER, c2 INTEGER );
INSERT INTO t VALUES(1,1);
COMMIT;

--# result : 1 row
\EXPLAIN PLAN
WITH w AS ( SELECT /*+ MATERIALIZE */
                    c1
               FROM r
              WHERE c1 > 0 )
SELECT *
  FROM w, s
 WHERE s.c1 IN ( SELECT t.c1
                   FROM t
                  WHERE s.c1 = t.c1
                    AND w.c1 = t.c2
               ) ;
```

위 질의를 보면 FROM 절에 w, s 순서로 나열되어 있고, subquery에서 s.c1과 w.c1을 참조하고 있다. 이와 같은 상황이면 서버가 비정상 종료한다.

<a id="0678868103d14081"></a>
##### 수정 전 대처

FROM 절에서 materialized view를 제일 뒤에 나열한다.

<a id="1f9b14b3beb3a50a"></a>
### 21c.1.26 Patch Notes

<a id="aea864458fd14872"></a>
#### <kbd>ISSUE-5442</kbd> [CYCLONE] unique 속성을 갖는 column을 이중화 할 경우, 트랜잭션이 실패할 수 있다.

<a id="92f8d76cccf4903c"></a>
##### 개요

이중화하는 table에 unique 속성을 갖는 column이 있을 경우, 원본 database에서는 정상적으로 처리되지만 원격 database에서는 unique violation 또는 NO_ROWS 에러가 발생할 수 있다. 이를 해결하기 위하여 unique 속성을 갖는 column을 이중화 할 경우, 해당 column의 동시성을 제어하는 기능을 추가하였다.

<a id="f8fbcf4ba1f371de"></a>
##### 현상 및 증상

```
[APPLIER #1(SID:100)-INSERT] ERR-23000(16057) : unique constraint (PUBLIC.TEST1) violated

[APPLIER #2(SID:101)-UPDATE] Conflict.

[APPLIER #3(SID:102)-DELETE] Conflict.
```

이중화 table에 unique 속성을 갖는 column이 있을 경우, 위와 같은 log가 빈번하게 slave의 trace log에 기록된다.

<a id="9e00f6a968796ceb"></a>
##### 수정 전 대처

없음

<a id="2f5f9ac13da4383e"></a>
#### <kbd>ISSUE-5568</kbd> [CYCLONE] 이중화 recovery가 두 개의 redo log 파일에 걸쳐 있을 경우, recovery 시작점이 잘못 설정된다.

<a id="bbf81e6aa79650b7"></a>
##### 개요

이중화 종료 후 restart 할 때 cyclone은 기존에 운영되었던 applier에 반영된 정보를 사용하여 recovery 시작 위치를 찾고 이중화를 다시 시작하게 된다.

Recovery 할 때는 여러 applier 간의 정보를 비교하면서 최적의 시작 위치를 찾는다. 만약 redo log file 정보들의 applier 간에 운영 정보가 서로 다를 경우, 이전 redo log file의 대한 정보를 버리고 새로운 redo log file 정보만 사용해서 recovery 시작 위치를 정하는 문제가 있어서 이를 수정하였다.

<a id="24e63849ef21d1c6"></a>
##### 현상 및 증상

이중화 종료 후 재시작시 이중화되지 못하는 transaction이 있을 수 있다.

<a id="0716b9375f81db22"></a>
##### 수정 전 대처

없음

<a id="525923d796b759fe"></a>
### 21c.1.25 Patch Notes

<a id="3c2ecc79a36375b8"></a>
#### <kbd>ISSUE-5511</kbd> [CYCLONE] Distributor에서 internal transaction ID가 잘못 세팅되는 경우가 있다.

<a id="11a0db5cc73cc013"></a>
##### 개요

원본 database에서 동시에 수행되는 transaction 간에 transaction ID 값은 중복될 수 없음을 보장한다. 그렇지만 수행이 완료된 transaction ID는 후에 재사용될 수 있다.

원본 transaction을 추출하여 이중화하기 위해 slave에 전송된 시점에서는 parallel apply로 인하여 해당 transaction ID의 실행시점이 원본과 다를 수 있다. 이 경우, transaction ID 재사용에 의한 ID 중복을 방지하기 위해 slave에서는 독립적인 transaction ID를 내부적으로 구분할 수 있는 internal ID 값으로 변경한다.

이러한 internal transaction ID는 distributor에서 할당하는데, 특정 로그를 분석하는 과정에서 internal 값이 아닌 원본 값을 사용함으로써 하나의 transaction이 두 개의 transaction ID를 갖는 문제가 발생하였다.

Distributor에서 동시성 제어의 구분자 값으로 사용되는 transaction ID 값 두 개가 하나의 transaction에 할당되어, 특정 상황에서 self dead-lock이 발생할 수 있다.

<a id="6d75d7145aa84c81"></a>
##### 현상 및 증상

```
CREATE TABLE T1 ( C1 INTEGER PRIMARY KEY, C2 LONG VARCHAR );

INSERT INTO T1 VALUES( 1, 'AAA' );
DELETE FROM T1 WHERE C1=1;
INSERT INTO T1 VALUES( 1,'AAAAAAA .......' );  ❶ 8K가 넘는 데이터 INSERT
COMMIT;
```

위와 같이 하나의 transaction 내에서 동일한 key 값을 처리하는 query와 레코드 사이즈가 8K가 넘는 INSERT가 수행되면 dead-lock이 발생한다.

<a id="fd9dcb3c8fd2cd83"></a>
##### 수정 전 대처

없음

<a id="3a22092dd4e290f4"></a>
#### <kbd>ISSUE-5505</kbd> Join의 가장 왼쪽 테이블에 대한 access method가 unique index access 이고, group by의 key column 중 일부만 그 unique index에 속하는 경우, 잘못된 결과가 도출될 수 있다.

<a id="22733ba9d4d437b3"></a>
##### 개요

Join의 가장 왼쪽 테이블에 대한 access method가 unique index access 이고, group by의 key column 중 일부만 그 unique index에 속하는 경우, 잘못된 결과가 도출될 수 있다.

<a id="4d88ea9ec93b0858"></a>
##### 현상 및 증상

```
DROP TABLE IF EXISTS r;
DROP TABLE IF EXISTS s;
DROP TABLE IF EXISTS t;

CREATE TABLE r( c1 INTEGER, c2 INTEGER, c3 INTEGER, c4 INTEGER, c5 INTEGER );

INSERT INTO r VALUES(1, 1, 1, 1, 1);
INSERT INTO r VALUES(1, 2, 1, 1, 1);
INSERT INTO r VALUES(1, 2, 1, 1, 1);
INSERT INTO r VALUES(2, 1, 2, 1, 1);
INSERT INTO r VALUES(2, 1, 2, 2, 1);
INSERT INTO r VALUES(3, 1, 2, 2, 1);
INSERT INTO r VALUES(3, 2, 3, 2, 1);
INSERT INTO r VALUES(4, 1, 3, 3, 1);
INSERT INTO r VALUES(5, 1, 3, 3, 1);
INSERT INTO r VALUES(1, 3, 2, 1, 1);
INSERT INTO r VALUES(1, 1, 1, 1, 1);

COMMIT;

CREATE TABLE s( c1 INTEGER PRIMARY KEY, c2 INTEGER, c3 INTEGER, c4 INTEGER, c5 INTEGER );

INSERT INTO s VALUES(1, 1, 1, 1, 1);
INSERT INTO s VALUES(2, 3, 1, 1, 1);
INSERT INTO s VALUES(3, 3, 1, 1, 1);
INSERT INTO s VALUES(4, 2, 2, 1, 1);
INSERT INTO s VALUES(5, 2, 2, 2, 1);
INSERT INTO s VALUES(6, 1, 2, 2, 1);
INSERT INTO s VALUES(7, 1, 3, 2, 1);
INSERT INTO s VALUES(8, 3, 3, 3, 1);
INSERT INTO s VALUES(9, 3, 3, 3, 1);

COMMIT;


CREATE TABLE t( c1 INTEGER, c2 INTEGER, c3 INTEGER, c4 INTEGER, c5 INTEGER );

INSERT INTO t VALUES(1, 1, 1, 1, 1);
INSERT INTO t VALUES(1, 3, 3, 1, 1);
INSERT INTO t VALUES(1, 3, 3, 1, 1);
INSERT INTO t VALUES(1, 2, 2, 1, 1);
INSERT INTO t VALUES(1, 2, 2, 1, 1);
INSERT INTO t VALUES(2, 3, 1, 1, 1);
INSERT INTO t VALUES(3, 3, 1, 1, 1);
INSERT INTO t VALUES(4, 2, 2, 1, 1);
INSERT INTO t VALUES(5, 2, 2, 2, 1);

COMMIT;

--# result : 6 rows
\EXPLAIN PLAN
SELECT s.c1, s.c2, t.c3
  FROM s, r, t
 WHERE s.c1 > 0 AND s.c1 < 5
   AND s.c1 = r.c1
   AND r.c1 = t.c1
 GROUP BY s.c1, s.c2, t.c3;


C1 C2 C3
-- -- --
 1  1  2
 1  1  3
 1  1  1
 1  1  2
 1  1  3
 1  1  1
 1  1  2
...
18 rows selected

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      GROUP                                                   |
|    3  |        HASH JOIN (INNER JOIN)                                |
|    4  |          MERGE JOIN (INNER JOIN)                             |
|    5  |            INDEX ACCESS ("S", "S_PRIMARY_KEY_INDEX")         |
|    6  |            INDEX ACCESS ("R", "R_IDX")                       |
|    7  |          HASH JOIN INSTANT                                   |
|    8  |            TABLE ACCESS ("T")                                |
========================================================================
```

위 질의 수행 결과는 6 rows 이어야 하는데, 18 rows가 출력되고 있다. 가장 왼쪽 테이블 s가 'S_PRIMARY_KEY_INDEX'를 이용하기 때문에 join의 결과는 s.c1에 대하여 정렬되어 올라온다. 위 plan을 보면 group by가 join의 정렬된 결과를 이용하여 grouping을 수행한다. 그러나 그 정렬된 record들은 모든 group key 칼럼에 대하여 정렬된 것이 아니기 때문에 틀린 결과가 도출될 수 있다.

<a id="dab9a04ea96e29da"></a>
##### 수정 전 대처

/*+ USE_GROUP_HASH */ hint를 사용한다.

<a id="3f5abd4ba8e3401b"></a>
#### <kbd>ISSUE-5445</kbd> ADD LOGFILE GROUP 수행 시, LOGFILE GROUP의 크기를 충분하게 설정하더라도 LOGFILE GROUP을 추가하지 못하는 경우가 있다.

<a id="b58faf606b74594f"></a>
##### 개요

충분한 크기의 LOGFILE GROUP을 설정해도 logfile이 최소 크기보다 작다는 에러 메세지와 함께 LOGFILE GROUP을 추가하지 못한다.  
ADD LOGFILE GROUP을 수행할 때, startup 과정에서 보정했던 log buffer와 pending log buffer 개수를 기준으로 logfile의 최소 크기를 계산해야 하는데 실제로는 property 값을 기준으로 최소 크기를 계산하기 때문이다.

<a id="77f44892814809c2"></a>
##### 현상 및 증상

다음과 같이 PROPERTY를 설정한 상태에서 mount 단계까지 startup 한 뒤, logfile group을 추가하려 하면 실패한다.

```
LOG_BUFFER_SIZE=1G
PENDING_LOG_BUFFER_COUNT=32
```

```
gSQL> STARTUP MOUNT

Startup success

gSQL> ALTER DATABASE ADD LOGFILE GROUP 4 ('redo_4_0.log') SIZE 512M;

ERR-42000(16198): size of log file is smaller than minimum size of log file(1107296256 bytes).
```

<a id="9e00ef31b697617d"></a>
##### 수정 전 대처

LOG_BUFFER_SIZE와 PENDING_LOG_BUFFER_COUNT property를 변경하여 logfile group을 생성한다.

<a id="0b024eb772204034"></a>
#### <kbd>ISSUE-5424</kbd> Embedded SQL에서 INTO 절 없이 SELECT 구문을 실행하면 데이터가 있는 경우에도 에러가 발생하여 이를 수정하였다.

<a id="9ebc77e14727aa89"></a>
##### 개요

Embedded SQL에서 INTO 절이 없는 SELECT 구문을 반복적으로 실행하면 에러가 발생하여 이를 수정하였다.

<a id="1c52f603c985ddcd"></a>
##### 현상 및 증상

```
EXEC SQL SELECT 1 FROM DUAL;

EXEC SQL SELECT 1 FROM DUAL;
```

위와 같이 동일한 SELECT 구문을 반복 실행하면 다음과 같은 에러가 발생한다.

```
Invalid cursor state : A cursor was open on the StatementHandle.
```

<a id="77e0d7f4799f61d5"></a>
##### 수정 전 대처

SELECT 구문에 INTO 절을 추가하여 실행한다.

<a id="de21581455b69379"></a>
#### <kbd>ISSUE-5407</kbd> Lock이 풀리길 기다리는 cluster peer가 driver node가 죽은 것을 인식하지 못한다.

<a id="fb6ccb17c5fe7660"></a>
##### 개요

원격에서 lock이 풀리길 기다리고 있는 driver member가 비정상 종료되면 원격에 만들어진 세션이 살아있는 상태로 유지되는 문제가 있다.

<a id="a0a710786c272131"></a>
##### 현상 및 증상

다음 예제는 cluster group G1이 G1N1, G1N2를 멤버로 갖고, 테이블 T1이 생성된 환경이다.

G1N1에서 테이블 T1의 record를 update 한다.

```
gSQL> UPDATE T1 SET A = A + 1 WHERE A = 1;

1 row updated.
```

G1N2에서 같은 record에 update를 수행하면 대기하게 된다.

```
gSQL> UPDATE T1 SET A = 10 WHERE A = 1;
```

G1N1의 session을 확인하면, G1N2에서 보낸 update를 위해 대기 중인 cluster session을 확인할 수 있다.

```
gSQL> SELECT SESSION_STATUS FROM V$SESSION@G1N1
       WHERE PROGRAM_NAME = 'cluster peer';

SESSION_STATUS
--------------
CONNECTED
```

G1N2에서 보낸 update를 위해 대기 중인 gsql을 kill 시켜도 다음과 같이 G1N1에서 해당 session이 살아있는 상태로 남아 있다.

```
gSQL> SELECT SESSION_STATUS FROM V$SESSION@G1N1
       WHERE PROGRAM_NAME = 'cluster peer';

SESSION_STATUS
--------------
CONNECTED
```

<a id="71c4515f477b4672"></a>
##### 수정 전 대처

없음

<a id="c631c493bbe0af12"></a>
### 21c.1.24 Patch Notes

<a id="0f9cc2538a3bc6c4"></a>
#### <kbd>ISSUE-5398</kbd> gloader가 text 모드로 데이터를 업로드할 때 데이터가 손실되는 문제가 있어 이를 수정하였다.

<a id="5f5a8ebaf484b454"></a>
##### 개요

gloader는 text 모드로 데이터를 업로드할 때 동일한 문자로 시작하는 field 구분자와 line 구분자를 사용한다. 데이터에도 이 구분자의 첫 문자가 포함될 경우, 데이터가 잘려서 유효하지 않은 형태로 업로드 되는 문제가 있어서 이를 수정하였다.

<a id="88eb6c2d802420df"></a>
##### 현상 및 증상

다음은 data file의 예이다.

```
data 1^^^Cc__Cc^data 2^Rr__Rr
```

다음은 control file의 예이다.

```
TABLE TEST
FIELD TERMINATED BY '^Cc__Cc^'
LINE TERMINATED BY '^Rr__Rr\n'
```

위와 같은 control file과 data file을 사용하여 업로드 할 경우 데이터가 잘린다.

```
gloader test test -i --control test.ctl --data test.dat --array 1 --no-copyright
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS

gSQL> SELECT * FROM TEST;
C1      C2           
------- -------------
data 1^ null         
^       null         
null    data 2^Rr__Rr
```

<a id="debc64836b4c5288"></a>
##### 수정 전 대처

동일한 문자로 시작하지 않는 field 구분자와 line 구분자를 사용한다.

<a id="eb9d19ef294514c2"></a>
#### <kbd>ISSUE-5174</kbd> gpec에서 함수 인자 선언을 지원한다.

<a id="0412a70c9e211b36"></a>
##### 개요

gpec에서 함수 인자 선언을 지원한다. 자세한 내용은 [함수 인자 선언](../part-05-developer-manual/33-embedded-sql.md#54341bc72038b5e4)을 참조한다.

<a id="212986604f671461"></a>
##### 현상 및 증상

없음

<a id="b67aed8449553f99"></a>
##### 수정 전 대처

없음

<a id="848cfc6411caf4ba"></a>
#### <kbd>ISSUE-5353</kbd> 윈도우 ODBC 연결 및 해제 시 프로그램 handle 개수가 증가하는 문제가 있어 이를 수정하였다.

<a id="706c2c2860d18284"></a>
##### 개요

윈도우 ODBC를 사용해 연결과 해제를 반복할 경우 프로그램의 전체 handle 개수가 증가되는 문제가 있어 수정하였다.

<a id="48c076b4fe57a215"></a>
##### 현상 및 증상

윈도우 ODBC를 사용해 연결과 해제를 반복할 경우 프로그램의 전체 handle 수가 증가한다.

<a id="a973a2640739dd30"></a>
##### 수정 전 대처

없음

<a id="5b79d1b5a4e9b6d9"></a>
#### <kbd>ISSUE-5344</kbd> View projection pruning을 수행할 때 상위 block에서 사용하는 column까지 삭제하는 문제가 있다.

<a id="443f0b9ce66e6a20"></a>
##### 개요

다음 조건을 만족하는 경우, 잘못 수행된 view projection pruning으로 인해 서버가 비정상 종료할 수 있다.

- View 내부에 group by 또는 order by가 있다.
- View의 select list에서 삭제하려는 expr이 다른 function expression의 argument 이다.

<a id="a139a72f3da0fee8"></a>
##### 현상 및 증상

다음은 문제가 발생할 수 있는 질의의 예이다.

```
SELECT sum_col1
  FROM ( SELECT sum(col1) as sum_col1
              , DECODE( sum(col1), NULL, 0 ) as decode_sum_col1
           FROM t1
          GROUP BY col2 
       ) v1;
```

v1에서 decode_sum_col1은 상위 block에서 쓰이지 않기 때문에 pruning 된다. 그런데 이 때 DECODE의 argument인 sum(col1)도 pruning 하는 문제가 있다. 하지만 sum(col1)은 select list에 이미 명시되어 있고 view 상위 block에서 쓰고 있으므로 삭제하면 안된다.

<a id="3280a22890b67b88"></a>
##### 수정 전 대처

없음

<a id="32509ca970637dae"></a>
#### <kbd>ISSUE-5336</kbd> gpec의 SELECT INTO 구문에 SUBQUERY를 사용하면 SELECT INTO 구문으로 처리하지 못한다.

<a id="ce2c0c37cd30e7c6"></a>
##### 개요

gpec이 SELECT INTO 구문 뒤에 SUBQUERY가 있는 SQL을 파싱하면 SELECT INTO 구문으로 처리하지 못하였다.

<a id="19703e71f1110bcf"></a>
##### 현상 및 증상

다음은 SELECT INTO 절에 호스트 변수 배열을 사용한 후 SUBQUERY를 사용하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
int no[10];
int count[10];
EXEC SQL END DECLARE SECTION;

EXEC SQL SELECT empno, B.COUNT 
    INTO :no, :count,
    FROM emp, (SELECT count(*) as COUNT FROM emp);
```

위 예제를 실행하면 다음과 같은 에러가 발생한다.

```
SQLCODE :-16289
SQLSTATE: 42000
ERROR MSG : into clause can have only one row
```

<a id="d81f6ab018bba5fe"></a>
##### 수정 전 대처

SELECT INTO 구문에 호스트 변수 배열을 사용하는 대신 cursor를 fetch 한다.

<a id="3ef0a1fade138126"></a>
#### <kbd>ISSUE-4945</kbd> CYCLONE, CYMON을 운영하기 위해 table을 생성하는 과정에서 SQLTables를 사용하여 table 존재 여부를 확인한다.

<a id="6e388c29fb756f65"></a>
##### 개요

CYCLONE, CYMON을 운영하기 위해 필요한 table이 존재하는지 여부를 SQLTables로 확인한 후에 table을 생성하도록 수정하였다.

<a id="49f530308f0ae262"></a>
##### 현상 및 증상

없음

<a id="d28771edd0a88fc4"></a>
##### 수정 전 대처

Prepare 할 때 table exist에 관한 validate를 수행한 후 그 결과를 가지고 table 존재 여부를 판단한다.

<a id="2fed1d4e0d013f23"></a>
#### <kbd>ISSUE-5245</kbd> CLUSTER_PACKET_ALLOCATION_TIMEOUT은 second 단위로 처리해야 한다.

<a id="097fd4444be7d466"></a>
##### 개요

CLUSTER_PACKET_ALLOCATION_TIMEOUT의 단위는 초이지만, 내부에서 micro second로 처리하고 있다.

<a id="10d2880d88b074b3"></a>
##### 현상 및 증상

Cluster pusher plan에 의해 다수의 load protocol이 발생하면 아래와 같은 에러가 빈번히 발생할 수 있다.

```
SELECT /*+
           REMOTE_JOIN(s)
           PUSHER(s)
        */
       COUNT(*)
  FROM r, s
 WHERE r.c1 = s.sk
;

ERR-40000(56008): transaction rollback: failed to synchronize replicas
ERR-HYT00(13059): Exceeded maximum packet allocation time
```

<a id="3bb7e96a73e9af83"></a>
##### 수정 전 대처

없음

<a id="6b4619be8d2c095d"></a>
#### <kbd>ISSUE-5029</kbd> Cluster 환경에서 Cyclone 운영 중에 master가 reset all 옵션으로 re-join 했음에도 기존 이중화 정보를 초기화하지 않는다.

<a id="c43fe26ebf1436fb"></a>
##### 개요

Cluster 환경에서 Cyclone이 운영 중인 상태에서 reset all 옵션을 사용하여 기존에 운영되던 master를 재시작할 경우, 기존의 이중화 정보를 사용하지 말고 현재 시점부터 이중화를 재개해야 한다.

<a id="2046e15aad5760ea"></a>
##### 현상 및 증상

Reset all 옵션을 사용하여 master를 재시작했음에도 기존의 이중화 운영정보를 사용하여 recovery를 수행한다.

<a id="e871c6e12d2f782a"></a>
##### 수정 전 대처

없음

<a id="b7c1fdfe46fcc4f4"></a>
### 21c.1.23 Patch Notes

<a id="d1ab054810ede080"></a>
#### <kbd>ISSUE-5132</kbd> Cluster 환경에서 global secondary index가 없는 single domain 테이블에 대한 DML 수행을 지원한다.

<a id="c57dfa7ce8164418"></a>
##### 개요

Cluster 환경에서 하나의 domain을 갖는 테이블에 대해 DML을 수행할 때 global secondary index를 구성하지 않으면 실패할 수 있다. DML 질의에서 global secondary index를 요구하는 이유는 server 간의 데이터 일관성을 보장하기 위해서이다. 따라서 하나의 server에만 데이터가 적재되어 server 간의 데이터 일관성을 보장할 필요가 없는 경우 global secondary index 없이도 DML을 지원하도록 하였다.

Cluster 환경에서 하나의 테이블을 다수의 server에서 관리하려면 global secondary index 구성을 권장한다.

<a id="41aff8038b180524"></a>
##### 현상 및 증상

```
--# G4 group에는 G4N1만 존재
CREATE TABLE r ( c1 INTEGER )
   CLONED
   AT CLUSTER GROUP g4
   WITHOUT GLOBAL SECONDARY INDEX;

--# result: success
INSERT INTO r VALUES (1), (2), (3);

--# 개선 사항
--# result: success
DELETE FROM r WHERE c1 = 2;

ERR-42000(16519): global secondary index expected in cluster DML
```

<a id="02e2899e8747c161"></a>
##### 수정 전 대처

없음

<a id="bad2aa998aa7edd3"></a>
#### <kbd>ISSUE-5193</kbd> Cluster 환경에서 index backward scan을 포함한 질의 수행시 결과에 오류가 발생한다.

<a id="968e8b9609a504a0"></a>
##### 개요

Cluster 환경에서 사용자 질의를 수행할 때 remote 서버에 접근해야 하고, ORDER BY 구문 또는 hint에 의해 index backward scan을 포함한 경우, 질의 결과가 index forward scan 순으로 나올 수 있다.

<a id="8415271219d0200a"></a>
##### 현상 및 증상

Cluster 환경에서 사용자 질의를 수행할 때 remote 서버에 접근이 필요한 경우 generated query를 구성하여 remote 서버에 전달한다. Index backward scan을 포함하는 generated query를 구성할 때 access path hint 정보가 잘못 구성되어 remote 서버에서는 index forward scan을 수행하는 경우가 발생하였다.

```
CREATE TABLE t1 
(
    c1 INTEGER
)
    SHARDING BY RANGE ( c1 )
    SHARD s1 VALUES LESS THAN ( 10 )       AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g2;

INSERT INTO t1 VALUES ( 12 );
INSERT INTO t1 VALUES ( 11 );
INSERT INTO t1 VALUES ( NULL );

CREATE INDEX t1_idx1 ON t1( c1 ASC NULLS LAST );


--# BUGBUG
--# result: 3 rows
--#         null
--#           12
--#           11
\EXPLAIN PLAN
SELECT c1 FROM t1@g2 ORDER BY c1 DESC NULLS FIRST;

  C1
----
  11
  12
null

3 rows selected.
```

<a id="e84a3b89dd8a35c8"></a>
##### 수정 전 대처

없음

<a id="23071a7f2c8e7955"></a>
#### <kbd>ISSUE-5109</kbd> Shard 재배치, split brain 후에 Cyclone이 오동작하는 문제를 수정하였다.

<a id="962a917fd19bf80b"></a>
##### 개요

Shard를 재배치하거나 split brain 상황 이후에 복구할 때 Cyclone이 "internal error occurred (Not Need Rebalance)" 에러를 내면서 종료된다.

<a id="e7b12b9fd69a7784"></a>
##### 현상 및 증상

Cyclone이 판단하기에 rebalance가 필요없는 상황인데도 rebalance가 수행되는 경우가 있는데 이런 일은 shard 재배치 또는 split brain 상황에서 발생할 수 있다.

<a id="0b01b0624cfa2f92"></a>
##### 수정 전 대처

Cyclone을 --reset으로 재기동한다.

<a id="c84a4c7a549da464"></a>
#### <kbd>ISSUE-5162</kbd> ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정했어도 오랜 시간 동안 대기하는 문제를 수정하였다.

<a id="5a8a0307ae595424"></a>
##### 개요

네트워크 단절을 인지하기 위해 ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정했는데도 주어진 TIMEOUT 보다 더 오래 대기하는 문제를 수정하였다.

<a id="353bd840962f9185"></a>
##### 현상 및 증상

ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정하였지만 특정 상황에서 네트워크 단절을 인지하지 못해 ODBC에서 서버 응답을 계속 기다리는 문제가 있다.

<a id="4b0c328014447f48"></a>
##### 수정 전 대처

odbc.ini에 다음 속성을 추가하여 네트워크 단절을 빨리 인지할 수 있도록 한다.

- KEEPALIVE_IDLE_TIME
- KEEPALIVE_INTERVAL
- KEEPALIVE_COUNT

또는 다음 커널 속성을 변경하여 네트워크 단절을 빨리 인지할 수 있도록 한다.

- net.ipv4.tcp_keepalive_intvl
- net.ipv4.tcp_keepalive_probes
- net.ipv4.tcp_keepalive_time
- net.ipv4.tcp_retries2

<a id="b9e803436a5975ba"></a>
#### <kbd>ISSUE-5160</kbd> ODBC global connection 환경에서 LONGVARCHAR, LONGVARBINARY 파라미터가 있을 경우 클라이언트 메모리가 증가하는 문제를 수정하였다.

<a id="068ab2801dd7b0bb"></a>
##### 개요

ODBC global connection 환경에서 LONGVARCHAR, LONGVARBINARY 파라미터가 있는 statement를 반복적으로 수행할 경우 클라이언트 메모리가 증가하는 문제를 수정하였다.

<a id="0c0f82a2b6b9f264"></a>
##### 현상 및 증상

ODBC global connection 환경에서 같은 statement로 LONGVARCHAR, LONGVARBINARY 파라미터가 있는 SQL을 반복적으로 수행할 경우 클라이언트 메모리가 증가하였다.

<a id="7f9830ec0a681e89"></a>
##### 수정 전 대처

없음

<a id="1ecaa4108bc84ca2"></a>
#### <kbd>ISSUE-5156</kbd> 일부 에러의 SQLSTATE를 변경하였다.

<a id="941950196aa65dc0"></a>
##### 개요

일부 에러의 SQLSTATE를 변경하였다.

<a id="8e7a34b3f1eb3f93"></a>
##### 현상 및 증상

변경된 에러의 SQLSTATE는 다음과 같다.

<a id="93e5d92a946c4cee"></a>
| 에러 번호 | 기존 SQLSTATE | 변경된 SQLSTATE | 메세지 |
| --- | --- | --- | --- |
| 13034 | RD000 | 08S01 | Service is not available |
| 16351 | 08000 | HY000 | failed to connect to the cluster member '%s' |
| 16523 | HY000 | 08S01 | the database system is shutting down |
| 25001 | HY000 | 08001 | Server is not running |

<a id="80b80695e96760fe"></a>
##### 수정 전 대처

없음

<a id="cb70f30718687585"></a>
#### <kbd>ISSUE-5147</kbd> CYMON에서 환경설정에 PROTOCOL=TCP로 설정하더라도 DA로 접속하던 문제를 수정하였다.

<a id="9fc5fbdc47973e6f"></a>
##### 개요

CYMON이 환경설정에 PROTOCOL=TCP로 설정하더라도 DA로 접속하던 문제를 수정하여 TCP로 접속하도록 수정하였다.

<a id="1c78d67f8348f5aa"></a>
##### 현상 및 증상

CYMON 환경설정 파일에 PROTOCOL=TCP로 설정할 경우, TCP를 사용하여 접속하여야 하는데 DA로 접속하고 있었다.

<a id="5b37349a542eb224"></a>
##### 수정 전 대처

없음

<a id="e126aae638ef3bb4"></a>
#### <kbd>ISSUE-5124</kbd> Dynamic memory를 할당하다 실패하면 동시성 문제로 서버가 죽을 수 있다.

<a id="7102acb2c2b49a37"></a>
##### 개요

Dynamic memory를 할당하다 실패할 경우 동시성 문제로 서버가 죽을 수 있다.

<a id="3fef5ec330b44589"></a>
##### 현상 및 증상

한 개의 dynamic memory를 여러 thread에서 할당하다가 실패하면 동시성 문제로 서버가 죽을 수 있다.

<a id="0cd73e35db4dd653"></a>
##### 수정 전 대처

없음

<a id="c000f1a8caf660d4"></a>
#### <kbd>ISSUE-4985</kbd> CYCLONE의 모니터링 정보에 slave의 진행 정보를 추가하였다.

<a id="33181372f9706a85"></a>
##### 개요

CYCLONE의 모니터링 정보에 slave에서 처리 중인 정보 (Apply_FileSeq, Apply_BlockSeq, Apply_Commit_Lsn)를 추가하였다.

<a id="2d164184ffe715ca"></a>
##### 현상 및 증상

없음

<a id="c6a8a788c8243357"></a>
##### 수정 전 대처

없음

<a id="af0bbd1039925fb3"></a>
#### <kbd>ISSUE-4882</kbd> CYCLONE SYNC 처리 중 오류 발생 시, 오류를 상세화하여 리포팅하도록 수정하였다.

<a id="ad5673a1b237a240"></a>
##### 개요

CYCLONE의 SYNC를 처리하는 도중에 오류가 발생하면 ERROR OCCURRED 메세지와 함께 에러 내용을 상세하게 trace log에 기록하도록 하였다.

<a id="732efb1d5adc0c0b"></a>
##### 현상 및 증상

없음

<a id="dacdefca9d163b14"></a>
##### 수정 전 대처

없음

<a id="dc4634850cd1cc86"></a>
### 21c.1.22 Patch Notes

<a id="c32153ba3e55b2f6"></a>
#### <kbd>ISSUE-5030</kbd> ALTER SYSTEM JOIN DATABASE를 수행하면 SNIPED된 세션이 정리되지 않는 문제가 발생한다.

<a id="3d55e454371871c9"></a>
##### 개요

ALTER SYSTEM JOIN DATABASE를 수행하면 cluster member간 topology 정보가 일시적으로 달라지는 시점이 발생한다. 그 시점에 COMMIT이 발생하면 잘못된 topology 정보로 인해 유효하지 않은 COMMIT 결과를 무한정 기다리게 된다.

<a id="39218ed7499a6e81"></a>
##### 현상 및 증상

Cluster 환경에서 한 멤버가 재시작한 뒤 ALTER SYSTEM JOIN DATABASE를 수행할 때, 그 멤버에 COMMIT이 발생하면 정상처리 되지 못하고 무한 대기하는 문제가 간헐적으로 발생한다.

<a id="e2f8821b985bb041"></a>
##### 수정 전 대처

서버를 재시작한다.

<a id="d3038140c4e50c3d"></a>
#### <kbd>ISSUE-5004</kbd> Cluster 환경에서 cyclone으로 이중화하는 도중에 slave의 pre-process 단계에서 deadlock이 발생한다.

<a id="b4692950da66bb4f"></a>
##### 개요

Cluster 환경에서 cyclone으로 이중화하는 도중에 간헐적으로 deadlock이 발생할 수 있다.

<a id="acbab1628aa7959f"></a>
##### 현상 및 증상

이중화가 더 이상 진행되지 않으며 멈춰 있는 것처럼 보이는 현상이 발생한다. 이는 cluster 환경에서 이중화 처리를 위해 pre-process 하는 도중에 deadlock이 발생한 경우이며, cymon으로 모니터링 하더라도 더 이상 이중화가 진행되지 않는다.

<a id="a761aa9bd3d1bf07"></a>
##### 수정 전 대처

Cyclone master와 slave를 reset 한다.

<a id="749f33773733ada7"></a>
### 21c.1.21 Patch Notes

<a id="3962c25a62633038"></a>
#### <kbd>ISSUE-4933</kbd> JDBC XA 사용 도중 서버가 내려가면 클라이언트에게 XA 에러를 전달해야 한다.

<a id="78f15ead5bb0d32e"></a>
##### 개요

JDBC XA를 사용하는 도중에 서버가 내려가면 클라이언트에게 XA 에러를 전달해야 한다.

<a id="1d012ea1121b4732"></a>
##### 현상 및 증상

JDBC XA를 사용하는 도중에 서버가 내려가면 클라이언트에게 XA 에러를 전달해야 하지만 실제로는 그렇게 하지 못해 XA 동작이 성공한 것처럼 동작한다.

<a id="726bb0ff0a19f8a7"></a>
##### 수정 전 대처

없음

<a id="21ef02f2afa1c81c"></a>
#### <kbd>ISSUE-4882</kbd> Cyclone sync를 수행할 때 long variable datatype의 string data, right truncated 에러가 발생한다.

<a id="deb798c616f50ef4"></a>
##### 개요

Cyclone의 sync 기능을 수행하는 도중에 string data, right truncated 에러가 발생한다.

<a id="b102130234ea763c"></a>
##### 현상 및 증상

Long varchar/ varbinary 타입의 column을 포함하고 있는 테이블을 sync 할 때 에러가 발생할 수 있다. Sync 기능에 사용하는 버퍼의 null padding이 손실되어 발생하는 에러로써 column 데이터 사이즈가 8 Kb 일 때만 발생한다.

<a id="a8d3ae721b4276dc"></a>
##### 수정 전 대처

없음

<a id="4e9beb09b344d559"></a>
#### <kbd>ISSUE-4873</kbd> 세션에서 dissociate 되지 않은 XA 트랜잭션에 대한 XA rollback 기능을 지원한다.

<a id="bf2a267e3d1d29cc"></a>
##### 개요

XA 트랜잭션은 xa end가 수행되기 전까지 세션에 associate 되어 있는데 이 XA 트랜잭션을 commit 하거나 rollback 하려면 세션과 dissociate 해야만 한다. 그런데 타 DBMS의 경우, 세션에서 dissociate하지 않은 상태에서도 rollback 할 수 있는 기능을 지원하고 있어 이에 맞춰 동일한 기능을 지원하도록 개선하였다.

<a id="435ffe33b9a23b29"></a>
##### 현상 및 증상

세션에서 수행 중인 XA 트랜잭션을 xa end 하지 않고 xa rollback 하면 에러가 발생하고, xa end 후에 xa rollback을 하면 정상적으로 동작한다.

```
gSQL> XA START 10

XA transaction started

gSQL> INSERT INTO T1 VALUES ( 1 );

1 row created.

gSQL> XA ROLLBACK 10   

ERR-HY000(40035): resource manager unavailable

gSQL> XA END 10 SUCCESS

XA transaction ended

gSQL> XA ROLLBACK 10  

Rollback completed
```

<a id="267f5e3fe7ac28e8"></a>
##### 수정 전 대처

없음

<a id="1d857577c076fb99"></a>
#### <kbd>ISSUE-4864</kbd> Drop shard 후에 restart 하면 shard가 refine 되지 않는다.

<a id="d687417823201b85"></a>
##### 개요

ALTER TABLE REBALANCE와 같은 구문에서 shard가 이동될 경우, shard가 drop될 수 있습니다. ager가 drop 된 shard들을 정리하기 전에 서버를 restart 하면 drop 된 shard가 제거되지 않을 수 있다.

<a id="bbfe6537f21c531c"></a>
##### 현상 및 증상

다음과 같이 REBALANCE 후에 바로 SHUTDOWN 하면 이동된 shard가 제거되지 않을 수 있다.

```
gSQL> ALTER TABLE T1 REBALANCE;

Table altered.

gSQL> \SHUTDOWN ABORT

Shutdown success
```

<a id="28c0ec6b7eb92939"></a>
##### 수정 전 대처

없음

<a id="dc0ceccf646b1eed"></a>
#### <kbd>ISSUE-4863</kbd> REBALANCE 후에 lock이 optimistic mode로 전환되지 않는다.

<a id="d172f02db364c65e"></a>
##### 개요

ALTER TABLE REBALANCE 하는 도중에 pessimistic mode로 전환된 lock이 optimistic mode로 전환되지 않아 성능이 저하될 수 있다.

<a id="8d2fce1b159c11ae"></a>
##### 현상 및 증상

DML이 발생한 상황에서 ALTER TABLE REBALANCE ONLINE을 수행하면 성능이 저하될 수 있다.

<a id="e9c1e7503ea007db"></a>
##### 수정 전 대처

없음

<a id="1524d4f47d21b68d"></a>
#### <kbd>ISSUE-4850</kbd> async commit을 사용하면 journal record의 기록 순서가 역전될 수 있다.

<a id="2ff1c805b75c7e9e"></a>
##### 개요

Asynchronous commit이 설정된 환경에서 ONLINE REBALANCE를 수행하던 도중에 DML이 발생하면 journal record의 기록 순서가 역전되어 REBALANCE를 수행 중인 프로세스가 journal replay 중에 비정상적 종료될 수 있다.

<a id="cb477ccc0b4bb328"></a>
##### 현상 및 증상

다음과 같이 asynchronous commit이 설정된 상황에서 REBALANCE를 수행하고, 각기 다른 트랜잭션의 동일한 record에 insert와 delete가 발생하면, REBALANCE를 수행 중인 프로세스가 비정상 종료될 수 있습니다.

```
gSQL> ALTER SYSTEM SET CLUSTER_ASYNC_COMMIT = TRUE;

System altered.

gSQL> ALTER TABLE T1 REBALANCE;
```

```
gSQL> INSERT INTO T1 VALUES (1);

1 row created.

gSQL> COMMIT;

Commit complete.
```

```
gSQL> DELETE FROM T1 WHERE I1 = 1;

1 row deleted.

gSQL> COMMIT;

Commit complete.
```

<a id="1e96756f503d409f"></a>
##### 수정 전 대처

Asynchronous commit을 FALSE로 설정한다.

<a id="f9fd664a6ab7338e"></a>
### 21c.1.20 Patch Notes

<a id="7d3ee8a0948462b0"></a>
#### <kbd>ISSUE-4753</kbd> USER_TABLES를 조회할 때 global temporary table이 조회되지 않는다.

<a id="6dcaa2aa7ca0c7b8"></a>
##### 개요

USER_TABLES, ALL_TABLES, DBA_TABLES와 같은 dictionary view를 조회할 때 global temporary table이 조회되지 않는다.

<a id="99a0262b0c589604"></a>
##### 현상 및 증상

다음과 같이 global temporary table을 생성한 후에 USER_TABLES을 통해 조회해도 조회되지 않는다.

```
gSQL> CREATE GLOBAL TEMPORARY TABLE gt1 ( c1 INTEGER ) ON COMMIT DELETE ROWS;

Table created.

gSQL> CREATE GLOBAL TEMPORARY TABLE gt2 ( c1 INTEGER ) ON COMMIT PRESERVE ROWS;

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> 
SELECT table_schema
     , table_name
     , temporary
     , duration
  FROM USER_TABLES
 WHERE table_name IN ( 'GT1', 'GT2' )
 ORDER BY 2
; 

no rows selected.
```

패치하면 다음과 같이 올바른 결과를 조회할 수 있다.

```
gSQL>
SELECT table_schema
     , table_name
     , table_type
     , commit_action
  FROM TABLES
 WHERE table_name IN ( 'GT1', 'GT2' )
 ORDER BY 2
; 

TABLE_SCHEMA TABLE_NAME TABLE_TYPE       COMMIT_ACTION
------------ ---------- ---------------- -------------
PUBLIC       GT1        GLOBAL TEMPORARY DELETE       
PUBLIC       GT2        GLOBAL TEMPORARY PRESERVE     

2 rows selected.
```

해당 패치를 적용하려면 다음과 같이 DictionarySchema.sql을 실행해야 한다.

- Standalone의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
```

- Cluster의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
```

<a id="540ee9c74a145406"></a>
##### 수정 전 대처

SQL 표준인 INFORMATION_SCHEMA.TABLES를 조회한다.

```
gSQL>
SELECT table_schema
     , table_name
     , table_type
     , commit_action
  FROM TABLES
 WHERE table_name IN ( 'GT1', 'GT2' )
 ORDER BY 2
; 

TABLE_SCHEMA TABLE_NAME TABLE_TYPE       COMMIT_ACTION
------------ ---------- ---------------- -------------
PUBLIC       GT1        GLOBAL TEMPORARY DELETE       
PUBLIC       GT2        GLOBAL TEMPORARY PRESERVE     

2 rows selected.
```

<a id="b5e76d97a118e0ed"></a>
#### <kbd>ISSUE-4720</kbd> 파일 시스템 저장 공간이 한계에 도달했을 때 시스템 thread가 비정상 종료된다.

<a id="03f7fe0c6036d6f0"></a>
##### 개요

기존에는 아카이브 로그를 위한 파일 시스템의 저장 공간이 한계에 도달했을 때 gmaster 아카이브 thread가 비정상 종료되었다. 이에 아카이브가 실패하더라도 비정상 종료되지 않고 파일 시스템에 여유가 생기면 실패한 아카이브를 다시 수행하도록 수정하였다.

<a id="73f94ff9d5b86c86"></a>
##### 현상 및 증상

아카이브 로그를 생성하다가 파일 시스템이 가득 차면 아카이브가 실패하고, 이로 인해 gmaster 아카이브 thread가 비정상 종료되었다.

<a id="0d12148cb02a0f48"></a>
##### 수정 전 대처

없음

<a id="9293e041f0686f52"></a>
### 21c.1.19 Patch Notes

<a id="651a72c195d9e74f"></a>
#### <kbd>ISSUE-4713</kbd> Cyclone을 이중화할 때 slave에 conflict 오류가 발생한다.

<a id="c61d9396ca0a03d7"></a>
##### 개요

Slave 장비의 CLUSTER_ASYNC_COMMIT 프로퍼티가 YES로 설정되어 있으면 update conflict 오류가 발생한다.

<a id="3d4a17e7da690699"></a>
##### 현상 및 증상

CLUSTER_ASYNC_COMMIT 프로퍼티가 YES로 설정되어 있을 때 applier가 반영한 값이 완전히 commit 되지 않은 상태에서 다른 applier가 방금 반영한 record에 접근할 경우 conflict가 발생할 수 있다.

이에 cyclone slave를 시작할 때 CLUSTER_ASYNC_COMMIT을 NO로 바꾸도록 수정하였다.

<a id="8aa059a9b17ba515"></a>
##### 수정 전 대처

Slave가 운영되는 GOLDILOCKS의 CLUSTER_ASYNC_COMMIT을 NO로 설정한다.

```
gSQL> ALTER SYSTEM SET CLUSTER_ASYNC_COMMIT=NO;
System altered.
```

<a id="ea0b65f1dc901660"></a>
#### <kbd>ISSUE-4709</kbd> Local open 단계에서 local 노드에 대한 질의 수행이 실패하는 경우가 있다.

<a id="bc32c49481496ecd"></a>
##### 개요

Cluster 환경에서 local open 상태인 노드에 접속하여 테이블을 조회할 때 에러가 발생한다.

<a id="cb605eebfffcbf2d"></a>
##### 현상 및 증상

접속한 노드가 local open 상태일 경우 remote 노드에는 접근할 수 없지만 local 노드에는 접근할 수 있다. 하지만 local open 상태의 노드에서 local 노드로 접속할 수 없다고 판단하여 질의가 실패하는 경우가 있다.

다음은 local open 상태인 G1N1에서 질의를 수행했을 때 에러가 발생하는 예이다.

```
gSQL> SELECT * FROM v$datafile;

ERR-HY000(16354): connection of member 'G1N1' is broken
```

현재 노드에서 특정 노드로 접근할 수 있는지 여부는 connection 정보를 기준으로 판단한다. 그런데 local open 단계와 같이 connection 정보를 참조할 수 없는 경우에는 현재 노드에도 접근할 수 없다고 판단하는 경우가 있다.

Connection 정보를 참조할 수 없는 경우에도 현재 노드로의 접근은 가능하다고 판단할 수 있게 수정하였다.

<a id="cd6e56273e6b2055"></a>
##### 수정 전 대처

없음

<a id="49326fbbe706f449"></a>
#### <kbd>ISSUE-4693</kbd> View 내부 query가 on filter, where filter를 모두 가진 left outer join이고, 이 view가 merging 되면 잘못된 결과가 나올 수 있다.

<a id="85c222a62b2cfa68"></a>
##### 개요

View 내부 query가 on filter, where filter를 모두 가진 left outer join이고, 이 view가 merging 되면 잘못된 결과가 나올 수 있다.

<a id="2e60919170254157"></a>
##### 현상 및 증상

아래 질의 결과는 1인데 실제 출력된 결과는 2 이다.

```
CREATE TABLE r ( r_c1 INTEGER NOT NULL, r_c2 INTEGER );
CREATE TABLE s ( s_c1 INTEGER NOT NULL, s_c2 INTEGER );
CREATE TABLE t ( t_c1 INTEGER NOT NULL, t_c2 INTEGER );


CREATE UNIQUE INDEX idx_r_c1 ON r( r_c1 );
CREATE UNIQUE INDEX idx_s_c1 ON s( s_c1 );
CREATE UNIQUE INDEX idx_t_c1 ON t( t_c1 );

INSERT INTO r VALUES ( 1, 1 );
INSERT INTO r VALUES ( 2, 2 );
INSERT INTO s VALUES ( 1, 1 );
INSERT INTO s VALUES ( 2, 2 );
INSERT INTO t VALUES ( 1, 1 );
INSERT INTO t VALUES ( 2, 2 );
COMMIT;

SELECT 
       COUNT(*)
  FROM ( SELECT r_c1
              , s_c1
           FROM r
                LEFT JOIN
                s
                ON r_c1 = s_c1
          WHERE
                r_c2 = 1
       ) v1
     , t
 WHERE v1.r_c1 = t_c2
;

COUNT(*)
--------
       2

1 row selected.
```

위 질의에서 v1 내부 query의 s_c1 column은 view 외부에서 사용되지 않는다. 따라서 query transform 단계에서 제거된 후, simple view merging 된다.

```
SELECT 
       COUNT(*)
  FROM r LEFT JOIN s ON r_c1 = s_c1
     , t
 WHERE v1.r_c1 = t_c2
   AND r_c2 = 1
;
```

그 후, s_c1은 unique key column 이고, left outer join 외의 다른 어떤 곳에서도 사용되지 않기 때문에 아래와 같이 left outer join 자체가 제거될 수 있다.

```
SELECT 
       COUNT(*)
  FROM r
     , t
 WHERE v1.r_c1 = t_c2
   AND r_c2 = 1
;
```

위와 같이 query transform 되는 과정에서 r_c2 = 1이 유실되는 문제가 있었다. 이에 이 문제를 해결하여 다음과 같이 정상적인 결과가 나오도록 하였다.

```
\EXPLAIN PLAN 
SELECT 
       COUNT(*)
  FROM ( SELECT r_c1
              , s_c1
           FROM r
                LEFT JOIN
                s
                ON r_c1 = s_c1
          WHERE
                r_c2 = 1
       ) v1
     , t
 WHERE v1.r_c1 = t_c2
;

COUNT(*)
--------
       1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      AGGREGATION BY HASH                                     |
|    3  |        HASH JOIN (INNER JOIN)                                |
|    4  |          TABLE ACCESS ("T")                                  |
|    5  |          HASH JOIN INSTANT                                   |
|    6  |            TABLE ACCESS ("R")                                |
========================================================================

     1  -  TARGET : COUNT(*)
     2  -  AGGREGATION : COUNT(*)
     3  -  JOINED COLUMN : NOTHING
     4  -  READ COLUMN : T.T_C2
     5  -  HASH KEY : R.R_C1
           READ KEY COLUMN : R.R_C1
             HASH FILTER : R.R_C1 = T.T_C2
           FETCH ONE ROW
     6  -  READ COLUMN : R.R_C1, R.R_C2
             PHYSICAL FILTER : R.R_C2 = 1

<<<  end print plan
```

<a id="5a1d14519b4b015d"></a>
##### 수정 전 대처

/*+ NO_MERGE(v1) */ hint를 사용한다.

<a id="a8c61112d81c2481"></a>
#### <kbd>ISSUE-4696</kbd> Cluster table의 update master 정보를 조회하기 위한 view column을 추가하였다.

<a id="feb463ef4a91edcd"></a>
##### 개요

Cluster table의 update master는 table에 DML이 발생할 경우 가장 먼저 DML이 수행되는 member node 이다.

각 cluster table의 update master를 결정하는데 영향을 주는 요소는 다음과 같다.

- Cluster table 배치
- Cluster group 내 member들의 position
- Online/ offline 여부
- Rebalance 수행 여부

운영 중에 변경될 수 있는 update master 정보를 쉽게 조회할 수 있도록 아래 dictionary view에 IS_UPDATE_MASTER column을 추가하였다.

- [DBA_TAB_PLACE](../part-02-administration-manual/9-database-information.md#235d293ebeeda681)
- [ALL_TAB_PLACE](../part-02-administration-manual/9-database-information.md#983b4475fb40b868)
- [USER_TAB_PLACE](../part-02-administration-manual/9-database-information.md#95a5231ea16425fb)

<a id="4450746835460f88"></a>
##### 현상 및 증상

다음과 같이 조회할 수 있다.

```
SELECT group_name, member_name, is_update_master 
  FROM user_tab_place 
 WHERE table_name = 'R';

GROUP_NAME MEMBER_NAME IS_UPDATE_MASTER
---------- ----------- ----------------
G1         G1N1        TRUE            
G1         G1N2        FALSE           
G2         G2N1        TRUE            
G2         G2N2        FALSE           
G3         G3N1        TRUE            
G3         G3N2        FALSE           

6 rows selected.
```

Cluster table R은 G1, G2, G3 그룹에 배치되어 있는데 각 그룹에서 update master에 해당하는 멤버는 G1N1, G2N1, G3N1 이다.

<a id="b57dabe36ca44523"></a>
##### 수정 전 대처

없음

<a id="6dc619f2256e168f"></a>
### 21c.1.18 Patch Notes

<a id="01c5821579324e16"></a>
#### <kbd>ISSUE-4646</kbd> View 내부 query가 set 이고 order by 절이 있으면 잘못된 결과가 나온다.

<a id="a055f8b1d0fcfe3b"></a>
##### 개요

View 내부 query가 set이고 order by 절이 있으면 잘못된 결과가 나온다. 이 경우, set에는 union all만 있어야 하고, view의 column들 중에 일부만 사용해야 한다.

<a id="39d1137b3e8bd2ed"></a>
##### 현상 및 증상

다음 예에서 v1 view에는 c1, c2, c3, c4가 있지만 실제로 읽는 건 c1, c3 column 뿐이다. 또한 view 내부 query는 union all만 쓰인 set 절이고, order by가 있다.

이 경우 잘못된 결과가 나온다.

```
CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER, c3 INTEGER, c4 INTEGER );
INSERT INTO t1 VALUES(1,1,1,1);
INSERT INTO t1 VALUES(2,1,3,1);

CREATE TABLE t2 ( c1 INTEGER, c2 INTEGER, c3 INTEGER, c4 INTEGER );
INSERT INTO t2 VALUES(1,1,1,1);
INSERT INTO t2 VALUES(2,1,3,1);

COMMIT;

SELECT c1, c3
  FROM ( SELECT c1, c2, c3, c4 FROM t1
         UNION ALL 
         SELECT c1, c2, c3, c4 FROM t2
         ORDER BY c1
       ) v1;

  C1 C3
---- --
   1  1
   2  1
null  3
null  3

4 rows selected.
```

문제를 수정하면 다음과 같이 정상적인 결과가 나온다.

```
SELECT c1, c3
  FROM ( SELECT c1, c2, c3, c4 FROM t1
         UNION ALL 
         SELECT c1, c2, c3, c4 FROM t2
         ORDER BY c1
       ) v1;

C1 C3
-- --
 1  1
 1  1
 2  3
 2  3

4 rows selected.
```

<a id="db341e56dc8d9f06"></a>
##### 수정 전 대처

없음

<a id="90ac1bc39f28a1b9"></a>
#### <kbd>ISSUE-4642</kbd> Offline member가 존재할 경우, pusher 없이 remote join 가능한 상황임에도 불구하고 pusher를 생성하여 remote join을 수행한다.

<a id="61b094451f28eacd"></a>
##### 개요

Offline member가 존재할 경우, pusher 없이 remote join 가능한 상황임에도 불구하고 pusher를 생성하여 remote join을 수행한다.

<a id="f2dc30243dd6aab9"></a>
##### 현상 및 증상

다음 예에서 LC 테이블의 member (g1n2)가 offline 되면, remote join 할 때 pusher가 생성된다.

```
CREATE TABLE LC ( c1 INTEGER, c2 INTEGER ) CLONED;
CREATE TABLE RS ( sk INTEGER, c2 INTEGER ) SHARDING BY (sk);

\explain plan
SELECT 
       LC.c1
     , RS.sk
  FROM LC
     , RS
 WHERE LC.c1 = RS.sk
 ORDER BY 1
;

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      MULTIPLE CLUSTER                                        |
|    3  |        CLUSTER PUSHER ("_$NI_8")                             |
|    4  |          TABLE ACCESS ("LC")                                 |
|    5  |        SELECT STATEMENT                                      |
|    6  |          QUERY BLOCK ("$QB_IDX_2")                           |
|    7  |            SORT INSTANT                                      |
|    8  |              HASH JOIN (INNER JOIN)                          |
|    9  |                TABLE ACCESS ("RS" AS _A2)                    |
|   10  |                HASH JOIN INSTANT                             |
|   11  |                  PUSHER TABLE ACCESS ("_$NI_8" AS _A1)       |
========================================================================

     1  -  TARGET : _$NI_8.C1, RS.SK
     2  -  SQL : SELECT /*+ USE_ORDER_SORT KEEP_JOINED_TABLE USE_HASH_IN( _A1, 10 ) FULL( _A2 ) FULL( _A1 ) */ "_A1"."C1", "_A2"."SK" FROM ( "PUBLIC"."RS"@LOCAL AS "_A2" INNER JOIN "SESSION_SCHEMA"."_$NI_8"@LOCAL AS "_A1" ON "_A1"."C1" = "_A2"."SK") ALIAS "_A3" ORDER BY "_A1"."C1" ASC NULLS LAST
           TARGET DOMAIN : G1(G1N1,G1N2) 0 rows, G2(G2N1,G2N2) 0 rows, G3(G3N1,G3N2) 0 rows
           MERGE SORTING
             SORT KEY : _$NI_8.C1
     3  -  SQL : DECLARE INSTANT TABLE "SESSION_SCHEMA"."_$NI_8" ( "C1" NUMBER(10, 0) ) 
           COLUMN : LC.C1 AS C1
           SHARDED : LC.C1
           TARGET DOMAIN : G1(G1N1,G1N2) 0 rows, G2(G2N1,G2N2) 0 rows, G3(G3N1,G3N2) 0 rows
     4  -  CLONED 
           READ COLUMN : LC.C1
     6  -  TARGET : _A1.C1, _A2.SK
     7  -  SORT KEY : "_A1.C1 ASC NULLS LAST"
           RECORD COLUMN : _A2.SK
           READ KEY COLUMN : _A1.C1
           READ RECORD COLUMN : _A2.SK
     8  -  JOINED COLUMN : _A1.C1, _A2.SK
     9  -  HASH SHARD ( # 3 ) 
           READ COLUMN : _A2.SK
    10  -  HASH KEY : _A1.C1
           READ KEY COLUMN : _A1.C1
             HASH FILTER : _A1.C1 = _A2.SK
    11  -  READ COLUMN : _A1.C1

<<<  end print plan
```

문제를 수정하면 다음과 같이 LC 테이블의 member (g1n2)가 offline 이라도 pusher 없이 remote join 할 수 있다.

```
\explain plan
SELECT 
       LC.c1
     , RS.sk
  FROM LC
     , RS
 WHERE LC.c1 = RS.sk
 ORDER BY 1
;
< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      MULTIPLE CLUSTER                                        |
|    3  |        SELECT STATEMENT                                      |
|    4  |          QUERY BLOCK ("$QB_IDX_2")                           |
|    5  |            SORT INSTANT                                      |
|    6  |              HASH JOIN (INNER JOIN)                          |
|    7  |                TABLE ACCESS ("LC" AS _A2)                    |
|    8  |                HASH JOIN INSTANT                             |
|    9  |                  TABLE ACCESS ("RS" AS _A1)                  |
========================================================================

     1  -  TARGET : LC.C1, RS.SK
     2  -  SQL : SELECT /*+ USE_ORDER_SORT KEEP_JOINED_TABLE USE_HASH_IN( _A1, 10 ) FULL( _A2 ) FULL( _A1 ) */ "_A2"."C1", "_A1"."SK" FROM ( "PUBLIC"."LC"@LOCAL AS "_A2" INNER JOIN "PUBLIC"."RS"@LOCAL AS "_A1" ON "_A1"."SK" = "_A2"."C1") ALIAS "_A3" ORDER BY "_A2"."C1" ASC NULLS LAST
           TARGET DOMAIN : G1(G1N1) 0 rows, G2(G2N1,G2N2) 0 rows, G3(G3N1,G3N2) 0 rows
           MERGE SORTING
             SORT KEY : LC.C1
     4  -  TARGET : _A2.C1, _A1.SK
     5  -  SORT KEY : "_A2.C1 ASC NULLS LAST"
           RECORD COLUMN : _A1.SK
           READ KEY COLUMN : _A2.C1
           READ RECORD COLUMN : _A1.SK
     6  -  JOINED COLUMN : _A2.C1, _A1.SK
     7  -  CLONED 
           READ COLUMN : _A2.C1
     8  -  HASH KEY : _A1.SK
           READ KEY COLUMN : _A1.SK
             HASH FILTER : _A1.SK = _A2.C1
     9  -  HASH SHARD ( # 3 ) 
           READ COLUMN : _A1.SK

<<<  end print plan
```

<a id="8e9d8ac84f857b89"></a>
##### 수정 전 대처

없음

<a id="d1f1eb7f59477893"></a>
#### <kbd>ISSUE-4678</kbd> gpec이 SELECT 구문을 SELECT INTO 구문으로 처리하는 경우가 있다.

<a id="c56147f5cf5ee167"></a>
##### 개요

Embedded SQL의 SELECT 구문과 SELECT INTO 구문은 각각 구분하여 처리해야 한다. 그러나 gpec이 embedded SQL의 SELECT 구문을 처리할 때 SELECT INTO 구문으로 잘못 처리하여 간헐적으로 비정상 종료되는 경우가 있다.

<a id="76d3906ed9343b77"></a>
##### 현상 및 증상

gpec은 원래 다음 SQL 구문을 SELECT 구문으로 처리해야 하는데 쓰레기 값 때문에 SELECT INTO 구문으로 처리하였다.

```
EXEC SQL SELECT * FROM DUAL;
```

<a id="86a2e7df910324c3"></a>
##### 수정 전 대처

SELECT 구문에 INTO 절을 사용한다.

<a id="5b675553f3b51eb7"></a>
### 21c.1.17 Patch Notes

<a id="c129e6de188074f4"></a>
#### <kbd>ISSUE-4594</kbd> NOT IN subquery unnesting을 수행할 때, subquery 내에 query set이 있으면 시스템이 비정상 종료된다.

<a id="2489346d4bf9f188"></a>
##### 개요

NOT IN subquery unnesting을 수행할 때, subquery 내에 query set이 있으면 시스템이 비정상 종료된다.

<a id="8029260155d89c7d"></a>
##### 현상 및 증상

다음과 같이 질의하면 시스템이 비정상 종료된다.

```
gSQL> CREATE TABLE r ( r_c1 INTEGER PRIMARY KEY, r_c2 INTEGER );

Table created.

gSQL> CREATE TABLE s ( s_c1 INTEGER PRIMARY KEY, s_c2 INTEGER );

Table created.

gSQL> CREATE TABLE t ( t_c1 INTEGER PRIMARY KEY, t_c2 INTEGER );

Table created.

gSQL> CREATE TABLE u ( u_c1 INTEGER PRIMARY KEY, u_c2 INTEGER );

Table created.

gSQL> commit;

Commit complete.

gSQL> \EXPLAIN PLAN
SELECT * 
  FROM r
 WHERE r_c1 NOT IN ( SELECT s_c1 FROM s 
                     UNION ALL
                     SELECT t_c1 FROM t  
                     UNION ALL
                     SELECT u_c1 FROM u
                   )
;
```

문제를 수정하면 정상적으로 수행된다.

```
gSQL> \EXPLAIN PLAN
SELECT * 
  FROM r
 WHERE r_c1 NOT IN ( SELECT s_c1 FROM s 
                     UNION ALL
                     SELECT t_c1 FROM t  
                     UNION ALL
                     SELECT u_c1 FROM u
                   )
;    2     3     4     5     6     7     8     9    10 

no rows selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (ANTI SEMI)                                   |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        HASH JOIN INSTANT (UNIQUE)                            |
|    5  |          INLINE_VIEW ("$V6")                                 |
|    6  |            QUERY BLOCK ("$QB_IDX_6")                         |
|    7  |              UNION-ALL                                       |
|    8  |                QUERY BLOCK ("$QB_IDX_9")                     |
|    9  |                  INDEX ACCESS ("S", "S_PRIMARY_KEY_INDEX")   |
|   10  |                QUERY BLOCK ("$QB_IDX_12")                    |
|   11  |                  INDEX ACCESS ("T", "T_PRIMARY_KEY_INDEX")   |
|   12  |                QUERY BLOCK ("$QB_IDX_15")                    |
|   13  |                  INDEX ACCESS ("U", "U_PRIMARY_KEY_INDEX")   |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2
     2  -  JOINED COLUMN : R.R_C1, R.R_C2
     3  -  READ COLUMN : R.R_C1, R.R_C2
     4  -  HASH KEY : $V6.S_C1
           READ KEY COLUMN : $V6.S_C1
             HASH FILTER : $V6.S_C1 = R.R_C1
           FETCH ONE ROW
     5  -  COLUMN : S_C1 AS S_C1
     6  -  TARGET : S_C1
     7  -  SET TARGET : S_C1
     8  -  TARGET : S.S_C1
     9  -  READ INDEX COLUMN : S.S_C1
    10  -  TARGET : T.T_C1
    11  -  READ INDEX COLUMN : T.T_C1
    12  -  TARGET : U.U_C1
    13  -  READ INDEX COLUMN : U.U_C1

<<<  end print plan
```

<a id="263e609135906f91"></a>
##### 수정 전 대처

```
gSQL> \EXPLAIN PLAN
SELECT * 
  FROM r
 WHERE r_c1 NOT IN ( SELECT /*+ NO_UNNEST */ s_c1 FROM s 
                     UNION ALL
                     SELECT t_c1 FROM t  
                     UNION ALL
                     SELECT u_c1 FROM u
                   )
;
```

<a id="e1205cd172303b28"></a>
#### <kbd>ISSUE-4588</kbd> Oracle과의 호환성을 위해 SQL에서 참조하는 function에서 no data found 에러가 발생하면 NULL을 반환하도록 하였다.

<a id="7a546e3bc2004a57"></a>
##### 개요

SQL에서 참조하는 function에서 no data found 에러가 발생하면 NULL을 반환한다.

<a id="c938be73f13ec7e1"></a>
##### 현상 및 증상

기존에는 SQL에서 참조하는 function에서 no data found 에러가 발생하면 에러를 반환하였다.

```
gSQL> CREATE TABLE t1( c1 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> 
CREATE OR REPLACE FUNCTION func1 RETURN INTEGER AS
  v1 INTEGER;
BEGIN
  SELECT c1 INTO v1 FROM t1 WHERE c1 = 2;
  RETURN v1;
END;
/

Function created.

gSQL> SELECT func1 FROM DUAL;

ERR-2F000(17045): no data found : 
  SELECT c1 INTO v1 FROM t1 WHERE c1 = 2;
  *
ERROR at line 4:
ERROR at FUNCTION("FUNC1")
```

<a id="515a8fe32f1f249f"></a>
##### 수정 전 대처

```
gSQL> CREATE TABLE t1( c1 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE OR REPLACE FUNCTION func1 RETURN INTEGER AS
  v1 INTEGER;
BEGIN
  SELECT c1 INTO v1 FROM t1 WHERE c1 = 2;
  RETURN v1;
EXCEPTION WHEN NO_DATA_FOUND THEN
  RETURN NULL;
END;
/

Function created.

gSQL> SELECT func1 FROM DUAL;

FUNC1
-----
 null

1 row selected.
```

<a id="483ef5b9890c68f0"></a>
#### <kbd>ISSUE-4609</kbd> Join combine이 포함된 subquery expression을 둘 이상 사용할 경우 segment fault가 발생한다.

<a id="2212a96ee27c29e6"></a>
##### 개요

Join combine이 포함된 subquery expression이 둘 이상 사용된 구문에서 subquery expression의 정보를 참조할 때 segment fault가 발생한다.

다음과 같은 절에서 문제가 발생하였다.

- TARGET 절
- WHERE 절
- HAVING 절
- ORDER BY 절

<a id="aa063c1b9940fe4c"></a>
##### 현상 및 증상

Subquery expression이 포함된 clause에서 subquery expression를 참조하기 위한 정보를 구축할 때  
관련된 expression을 찾지 못하여 expression 검색을 무한정 시도한다. 이로 인해 segment fault가 발생하였다.

```
CREATE TABLE T1(
       C1   NUMBER,
       C2   NUMBER,
       C3   NUMBER,
       C4   NUMBER );

CREATE TABLE T2(
       C1   NUMBER,   
       C2   NUMBER,
       C3   NUMBER,
       C4   NUMBER );

--# Segment Fault
SELECT 
     (
      SELECT t1.c1 
        FROM T1
             INNER 
             JOIN
             T2
             ON ( t1.c3 = t2.c2 OR t1.c3 = t2.c3 ) 
     )
   , (  
      SELECT t1.c1 
        FROM T1
             INNER 
             JOIN
             T2
             ON ( t1.c3 = t2.c2 OR t1.c3 = t2.c3 ) 
     ) AS DS2
  FROM dual;
```

<a id="2abc41c6fa6e591d"></a>
##### 수정 전 대처

없음

<a id="d4d0cbe50bc57ab6"></a>
#### <kbd>ISSUE-4589</kbd> SELECT FOR UPDATE, UPDATE, DELETE는 complex view merging을 지원하지 않고 있는데도 complex view merging으로 처리되는 것을 막지 못하였다.

<a id="9fefd7f226c46c40"></a>
##### 개요

SELECT FOR UPDATE, UPDATE, DELETE 구문은 complex view merging을 지원하지 않고 있는데도complex view merging으로 처리한다.

<a id="deb1beca85052c11"></a>
##### 현상 및 증상

다음 질의는 complex view merging 하지 말아야 한다. 그러나 subquery unnesting 후에 complex view merging 처리하여 서버가 비정상적으로 종료되었다.

```
DROP TABLE IF EXISTS t1;

CREATE TABLE t1
(
    c1 INTEGER
  , c2 INTEGER
  , c3 INTEGER
  , c4 INTEGER
);

COMMIT;

UPDATE t1
   SET c1 = 1
 WHERE ( c1, c2, c3, c4 )
    IN ( SELECT c1, c2, c3, c4
           FROM t1
          GROUP BY c1, c2, c3, c4
       );
```

<a id="31a780f6c8ab0e06"></a>
##### 수정 전 대처

없음

<a id="14d6814e40455ce4"></a>
#### <kbd>ISSUE-4575</kbd> Embedded SQL에서 동일한 SQL 문이 중복 캐시된다.

<a id="b033b4481a420b9f"></a>
##### 개요

Embedded SQL은 DML과 query 구문을 캐시하여 동일한 SQL을 사용할 때 재활용 한다. char 포인터가 호스트 변수로 사용되는 경우에는 동일한 SQL 문이 중복 캐시된다.

<a id="2aa62465b717c659"></a>
##### 현상 및 증상

다음과 같이 char 포인터가 호스트 변수로 사용되고 이 char 포인터의 문자열 길이가 달라지면 SQL 구문이 새로 생성된다.

```
void func(char * data)
{
    EXEC SQL BEGIN DECLARE SECTION;
    char * strPtr;
    EXEC SQL END DECLARE SECTION;
	strPtr = data;
    EXEC SQL DELETE FROM TEST WHERE C1 = :strPtr;
    if(sqlca.sqlcode == 0 )
    ....
}
```

<a id="56966ebdc4d53f42"></a>
##### 수정 전 대처

호스트 변수로 char 포인터를 사용하는 대신에 char array를 사용한다.

<a id="a1effb8a5901e3c8"></a>
#### <kbd>ISSUE-4566</kbd> 숫자 타입을 NUMBER 타입으로 변환할 때 반올림 후 자리수가 늘어났는데 overflow 처리를 하지 못하는 경우가 있다.

<a id="fc03f78d23b3b947"></a>
##### 개요

숫자 타입을 NUMBER 타입으로 변환할 때 반올림 후 자리수가 늘어났는데 overflow 처리를 하지 못하는 경우가 있다.

<a id="ba42ce136380ea23"></a>
##### 현상 및 증상

다음 질의는 원래 overflow 오류가 발생해야 하는 경우이다.

```
gSQL> SELECT CAST( 9999999999.9 AS NUMBER(10,0)) FROM dual;

CAST( 9999999999.9 AS NUMBER(10,0))
-----------------------------------
                        10000000000

1 row selected.
```

<a id="6445e1c6d2efccac"></a>
##### 수정 전 대처

문자 타입으로 변환한 후에 NUMBER 타입으로 변환한다.

```
gSQL> SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual;

ERR-22003(12060): data is outside the range of the data type to which the number is being converted : 
SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual
       *
ERROR at line 1:
```

<a id="0215a7f73816e328"></a>
#### <kbd>ISSUE-4559</kbd> SELECT INTO 구문에 cursor가 없는데도 TRACE_LONG_RUN_CURSOR로 trace log가 출력되는 경우가 있다.

<a id="abe1d50b88443dd9"></a>
##### 개요

TRACE_LONG_RUN_CURSOR property는 지정된 시간 이상의 long run cursor들을 trace log에 기록한다. SELECT INTO 구문에는 cursor가 필요없는데도 long run cursor로 분류되어 trace log에 남겨지는 경우가 있어 이를 수정하였다.

<a id="cfaa0303b64430af"></a>
##### 현상 및 증상

다음 예와 같이 SELECT INTO 구문이 실패할 경우 TRACE_LONG_RUN_CURSOR로 판단되어 trace log가 남는다.

```
gSQL> CREATE TABLE r ( c1 INTEGER );

Table created.

gSQL> INSERT INTO r VALUES ( 1 );

1 row created.


--# 1 초 이상 걸리는 long run cursor trace
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR = 1000;

System altered.


gSQL> \var v1 INTEGER
gSQL> \prepare sql SELECT c1 INTO :v1 FROM r WHERE c1 = 1 FOR UPDATE;

SQL prepared.

--# Trace log에 TRACE_LONG_RUN_CURSOR으로 기록되지 않음
gSQL> \exec

V1
--
 1

1 row selected.


gSQL> INSERT INTO r VALUES ( 1 );

1 row created.


--# 2 초 후 수행
--# Trace log에 TRACE_LONG_RUN_CURSOR으로 기록됨
gSQL> \exec

ERR-42000(16289): into clause can have only one row
```

<a id="9cb7c6e89b59bb35"></a>
##### 수정 전 대처

없음

<a id="f0d59a022b378fa8"></a>
#### <kbd>ISSUE-4549</kbd> 특정 topology 상황에서 ADD MEMBER를 수행할 때 유효하지 않은 멤버가 domain coordinator로 변경되는 경우가 있다.

<a id="c9a30fd481ca4b2a"></a>
##### 개요

ADD MEMBER를 수행할 때 추가된 멤버가 domain coordinator로 변경되면 기존 domain coordinator로부터의 응답을 기다리던 트랜잭션은 hang이 걸릴 수 있다. 따라서 ADD MEMBER를 수행할 때 coordinator 위치가 변경되지 않도록 해야 한다.

<a id="3c8428e0a7486b30"></a>
##### 현상 및 증상

그룹 G2에 global coordinator가 위치하고, 그룹 G1의 domain coordinator인 멤버인 G1N2에서 G1N1 멤버를 ADD한다.

```
ALTER CLUSTER GROUP G1 ADD CLUSTER MEMBER G1N1 HOST '127.0.0.1' PORT 11150;
```

ADD MEMBER로 인해 domain coordinator가 G1N2에서 새로 추가된 멤버인 G1N1으로 변경되면 기존 domain coordinator였던 G1N2으로부터의 응답을 기다리던 transaction들은 hang에 걸릴 수 있다.

<a id="cef43dd77463ded7"></a>
##### 수정 전 대처

Global coordinator에서 ADD MEMBER를 수행한다.

<a id="c2ef3dc6b5b65483"></a>
#### <kbd>ISSUE-4546</kbd> Cluster 환경에서 ORDER BY LIMIT 질의를 수행할 때, local method로 수행되면 결과에 오류가 발생한다.

<a id="86e716398669704e"></a>
##### 개요

Cluster 환경에서 ORDER BY LIMIT 질의를 수행할 때, local method로 수행되면 결과 오류가 발생한다.   
GROUP BY LIMIT나 DISTINCT LIMIT를 수행할 때도 동일한 문제가 발생한다.

<a id="35793c1516f4455d"></a>
##### 현상 및 증상

```
--# result: success
CREATE TABLE r ( sk INTEGER, nk INTEGER ) SHARDING BY ( sk );
COMMIT;

--# result: success
INSERT INTO r VALUES(1111, 1);
INSERT INTO r VALUES(1111, 1);
INSERT INTO r VALUES(1111, 1);
INSERT INTO r VALUES(1111, 1);
INSERT INTO r VALUES(1111, 2);
INSERT INTO r VALUES(2222, 1);
INSERT INTO r VALUES(2222, 1);
INSERT INTO r VALUES(2222, 1);
INSERT INTO r VALUES(2222, 1);
INSERT INTO r VALUES(2222, 3);
INSERT INTO r VALUES(3333, 1);
INSERT INTO r VALUES(3333, 1);
INSERT INTO r VALUES(3333, 1);
INSERT INTO r VALUES(3333, 1);
INSERT INTO r VALUES(3333, 4);
COMMIT;
```

위와 같은 테이블에 대해 다음과 같이 ORDER BY LIMIT 구문을 local method로 수행하면 결과에 오류가 발생한다.

```
SELECT /*+ LOCAL_ORDER */ 
       nk
  FROM r
 ORDER BY nk DESC
 LIMIT 3; 

NK
--
 2
 1
 1

3 rows selected.
```

문제 해결 후, 다음과 같이 결과가 정상적으로 출력되는 것을 확인할 수 있다.

```
SELECT /*+ LOCAL_ORDER */ 
       nk
  FROM r
 ORDER BY nk DESC
 LIMIT 3; 

NK
--
 4
 3
 2

3 rows selected.
```

<a id="a5f3456490a10e2e"></a>
##### 수정 전 대처

limit 대신 rownum을 이용한다.

```
gSQL> 
SELECT * 
  FROM ( SELECT /*+ LOCAL_ORDER */ 
                nk
           FROM r
          ORDER BY nk DESC
         )
 WHERE rownum < 4; 

NK
--
 4
 3
 2

3 rows selected.
```

<a id="e05306f29d373243"></a>
#### <kbd>ISSUE-4537</kbd> 잘못된 DROP TABLESPACE 구문이 성공한 후에 ADD MEMBER를 수행하면 새로운 member가 비정상 종료된다.

<a id="6435001778469b24"></a>
##### 개요

Cluster 환경에서 실패해야 할 DROP TABLESPACE 구문이 성공한 경우, ADD MEMBER를 수행하면 새로 추가할 cluster member가 비정상적으로 종료되어 ADD MEMBER가 실패한다.

DROP TABLESPACE 대상이 되는 tablespace가 사용자의 기본 tablespace로 지정된 경우 에러가 발생하도록 수정하였다.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1
         TEMPORARY TABLESPACE temp_tbs;

User created.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

ERR-42000(16133): cannot drop tablespace: "TEMP_TBS" is default tablespace of user "U1"
```

해당 tablespace를 제거하려면 다음과 같이 사용자의 기본 tablespace를 먼저 변경한 후에 제거해야 한다.

```
gSQL> ALTER USER u1 TEMPORARY TABLESPACE mem_temp_tbs;

User altered.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

Tablespace dropped.
```

<a id="a5c7daf81a004be3"></a>
##### 현상 및 증상

다음과 같이 사용자의 기본 tablespace는 제거할 수 없음에도 불구하고 DROP TABLESPACE가 성공하였다.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1
         TEMPORARY TABLESPACE temp_tbs;

User created.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

Tablespace dropped.
```

이후 다음과 같이 새로운 cluster member를 추가하면 새로운 member(g2n3)가 비정상적으로 종료되어 ADD MEMBER가 실패한다.

```
gSQL> ALTER CLUSTER GROUP g2 ADD CLUSTER MEMBER g2n3 HOST '127.0.0.1' PORT 12350;
```

<a id="917a34fbbb5e09e6"></a>
##### 수정 전 대처

ADD MEMBER를 수행하기 전에 다음과 같이 DROP TABLESPACE 무결성을 위반한 사용자를 찾아 사용자의 기본 tablespace를 변경해야 한다.

다음 질의 결과가 존재하는 경우, 해당 user의 default tablespace를 변경해야 한다.

```
SELECT auth.authorization_name
  FROM definition_schema.authorizations@local AS auth
     , definition_schema.users@local AS usr
 WHERE auth.auth_id = usr.auth_id
   AND NOT EXISTS ( SELECT *
                      FROM definition_schema.tablespaces@local AS tbs
                     WHERE tbs.tablespace_id = usr.default_data_tablespace_id );
```

다음 질의 결과가 존재하는 경우, 해당 user의 temporary tablespace를 변경해야 한다.

```
SELECT auth.authorization_name
  FROM definition_schema.authorizations@local AS auth
     , definition_schema.users@local AS usr
 WHERE auth.auth_id = usr.auth_id
   AND NOT EXISTS ( SELECT *
                      FROM definition_schema.tablespaces@local AS tbs
                     WHERE tbs.tablespace_id = usr.default_temp_tablespace_id );
```

다음 질의 결과가 존재하는 경우, 해당 user의 index tablespace를 변경해야 한다.

```
SELECT auth.authorization_name
  FROM definition_schema.authorizations@local AS auth
     , definition_schema.users@local AS usr
 WHERE auth.auth_id = usr.auth_id
   AND NOT EXISTS ( SELECT *
                      FROM definition_schema.tablespaces@local AS tbs
                     WHERE tbs.tablespace_id = usr.default_index_tablespace_id )
;
```

<a id="7f5397c0d1aebea0"></a>
### 21c.1.16 Patch Notes

<a id="10160573adef5734"></a>
#### <kbd>ISSUE-4500</kbd> Join condition이 OR 조건을 포함할 때 또다른 OR 조건을 이용하여 index scan을 수행하면 질의가 무한 대기한다.

<a id="997e8094d9ee8a0b"></a>
##### 개요

OR 조건을 포함하는 join condition에 의해 join combine 기법이 선택되고, 또 다른 join에 속한 relation에서 join combine에 포함된 column을 참조하면 무한 대기가 발생한다.

<a id="437c2e6516eae909"></a>
##### 현상 및 증상

다음 예와 같이 join combine으로 구성된 join에 포함된 column을 참조하면 column 정보를 찾지 못하여 무한 대기가 발생한다.

```
gSQL> CREATE TABLE T1( C1 INT, C2 INT );

Table created.

gSQL> CREATE INDEX IDX_T1_C1 ON T1( C1 );

Index created.

gSQL> CREATE INDEX IDX_T1_C2 ON T1( C2 );

Index created.

gSQL> INSERT INTO T1 VALUES ( 1, 1 );

1 row created.

--# 무한 대기
gSQL> SELECT *
  FROM T1 A, T1 B
 WHERE ( A.C1 = B.C1 OR A.C1 = B.C2 )
   AND EXISTS( SELECT 1
                 FROM T1 C
                WHERE ( C.C1 = A.C1 OR C.C2 = A.C1 ) );
```

<a id="05d0b3676ef60c78"></a>
##### 수정 전 대처

다음과 같이 JOIN COMBINE이 구성되지 않도록 NO_USE_JOIN_COMBINE hint를 부여한다.

```
gSQL> SELECT /*+ NO_USE_JOIN_COMBINE( A ) */ *
  FROM T1 A, T1 B
 WHERE ( A.C1 = B.C1 OR A.C1 = B.C2 )
   AND EXISTS( SELECT 1
                 FROM T1 C
                WHERE ( C.C1 = A.C1 OR C.C2 = A.C1 ) );

C1 C2 C1 C2
-- -- -- --
 1  1  1  1

1 rows selected.
```

<a id="94ebc7fe139c8859"></a>
### 21c.1.15 Patch Notes

<a id="3f5d5dada417a397"></a>
#### <kbd>ISSUE-4480</kbd> Reserved word가 column name인 column을 참조하는 %TYPE을 정의하면 에러가 발생한다.

<a id="6b7ad39816f66ab4"></a>
##### 개요

Reserved word가 column name인 column을 참조하는 %TYPE을 정의하면 에러가 발생한다.

<a id="2fdd85a59270bdd8"></a>
##### 현상 및 증상

다음 예와 같이 table에 OFFSET이라는 column이 있음에도 불구하고 column 정보를 찾지 못하고 에러가 발생한다.

```
gSQL> CREATE TABLE t1( "OFFSET" INTEGER, LENGTH INTEGER );

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE OR REPLACE PROCEDURE proc1( p1 public.t1."OFFSET"%TYPE )
      AS
      BEGIN
        NULL;
      END;
      /

ERR-2F000(17012): unknown type name : 
CREATE OR REPLACE PROCEDURE proc1( p1 public.t1."OFFSET"%TYPE )
```

<a id="9a7239c0858fdc24"></a>
##### 수정 전 대처

없음

<a id="9d174ff1e23cf071"></a>
#### <kbd>ISSUE-4472</kbd> DDL_DB 출력 시 schema privilege DDL이 출력되지 않는다.

<a id="a5856a8a1b00d4b1"></a>
##### 개요

Schema가 두 개 이상 생성되어 있을 때, DDL_DB를 출력하면 일부만 출력되고 일부는 출력되지 않는 문제가 발생한다.

<a id="fc02f67526dc9c72"></a>
##### 현상 및 증상

다음 예에서는 schema privilege DDL이 세 개 생겨야 하는데 실제로는 하나만 발생했다.

```
gSQL> CREATE SCHEMA s1;

Schema created.

gSQL> CREATE SCHEMA s2;

Schema created.

gSQL> CREATE SCHEMA s3;

Schema created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE USER u1 IDENTIFIED BY u1 WITHOUT SCHEMA;

User created.

gSQL> CREATE USER u2 IDENTIFIED BY u2 WITHOUT SCHEMA;

User created.

gSQL> CREATE USER u3 IDENTIFIED BY u3 WITHOUT SCHEMA;

User created.

gSQL> COMMIT;

Commit complete.

gSQL> GRANT CREATE TABLE ON SCHEMA s1 TO u1;

Grant succeeded.

gSQL> GRANT CREATE VIEW  ON SCHEMA s2 TO u2, u3;

Grant succeeded.

gSQL> COMMIT;

Commit complete.

gSQL> \ddl_db


--##################################################### 
--# Database DDL 
--##################################################### 


SET SESSION AUTHORIZATION "SYS"; 
COMMENT 
    ON DATABASE 
    IS 'goldilocks database' 
;
COMMIT;

...중략...

--##################################################### 
--# Schema Privilege DDL 
--##################################################### 


SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE TABLE ON SCHEMA "S1" 
    TO "U1" 
;
COMMIT;

--##################################################### 
--# Public Synonym DDL 
--##################################################### 

...생략...
```

문제를 수정한 후에 schema privilege DDL이 세 개 모두 정상적으로 발생한 것을 확인할 수 있다.

```
gSQL> CREATE SCHEMA s1;

Schema created.

gSQL> CREATE SCHEMA s2;

Schema created.

gSQL> CREATE SCHEMA s3;

Schema created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE USER u1 IDENTIFIED BY u1 WITHOUT SCHEMA;

User created.

gSQL> CREATE USER u2 IDENTIFIED BY u2 WITHOUT SCHEMA;

User created.

gSQL> CREATE USER u3 IDENTIFIED BY u3 WITHOUT SCHEMA;

User created.

gSQL> COMMIT;

Commit complete.

gSQL> GRANT CREATE TABLE ON SCHEMA s1 TO u1;

Grant succeeded.

gSQL> GRANT CREATE VIEW  ON SCHEMA s2 TO u2, u3;

Grant succeeded.

gSQL> COMMIT;

Commit complete.

gSQL> \ddl_db


--##################################################### 
--# Database DDL 
--##################################################### 


SET SESSION AUTHORIZATION "SYS"; 
COMMENT 
    ON DATABASE 
    IS 'goldilocks database' 
;
COMMIT;

...중략...

--##################################################### 
--# Schema Privilege DDL 
--##################################################### 


SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE TABLE ON SCHEMA "S1" 
    TO "U1" 
;
COMMIT;

SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE VIEW ON SCHEMA "S2" 
    TO "U2" 
;
COMMIT;

SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE VIEW ON SCHEMA "S2" 
    TO "U3" 
;
COMMIT;

--##################################################### 
--# Public Synonym DDL 
--##################################################### 

...생략...
```

<a id="82479e9368e25814"></a>
##### 수정 전 대처

Schema 별로 GRANT 정보를 출력한다.

```
gSQL> \ddl_schema s1 GRANT


SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE TABLE ON SCHEMA "S1" 
    TO "U1" 
;
COMMIT;

gSQL> \ddl_schema s2 GRANT


SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE VIEW ON SCHEMA "S2" 
    TO "U2" 
;
COMMIT;

SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    CREATE VIEW ON SCHEMA "S2" 
    TO "U3" 
;
COMMIT;
```

<a id="37ce7f494caed3bd"></a>
#### <kbd>ISSUE-4471</kbd> DDL_DB 명령어로 출력된 DISK TABLESPACE 구문으로 TABLESPACE를 생성할 때 syntax error가 발생한다.

<a id="8c74c1ff28c36129"></a>
##### 개요

DDL_DB 명령어로 출력된 CREATE DISK TABLESPACE 구문으로 TABLESPACE를 생성할 때 syntax error가 발생한다.

<a id="b03c2ef4d28f9dc9"></a>
##### 현상 및 증상

3. Tablespace를 생성한다.

```
gSQL> CREATE DISK DATA TABLESPACE disk_test_01 DATAFILE 'DISK_TEST_01.dbf' SIZE 100M;
COMMIT;
```

4. \ddl_db를 입력한다.

```
gSQL> \ddl_db

--##################################################### 
--# Database DDL 
--##################################################### 


SET SESSION AUTHORIZATION "SYS"; 
COMMENT 
    ON DATABASE 
    IS 'goldilocks database' 
;
COMMIT;

--##################################################### 
--# Tablespace DDL 
--##################################################### 

SET SESSION AUTHORIZATION "SYS"; 
CREATE DISK DATA TABLESPACE "DISK_TEST_01" 
    DATAFILE 
        '/home/product/Gliese/home/g1n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AT "G1N1" 
        AUTOEXTEND OFF 
      , 
        '/home/product/Gliese/home/g2n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AT "G2N1" 
        AUTOEXTEND OFF 
    ONLINE 
    EXTSIZE 262144 
;
COMMIT;

... 생략 ...
```

5. 2 단계에서 \ddl_db 명령어를 수행하여 출력된 tablespace DDL 구문을 입력한다.

```
gSQL> CREATE DISK DATA TABLESPACE "DISK_TEST_01" 
    DATAFILE 
        '/home/product/Gliese/home/g1n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AT "G1N1" 
        AUTOEXTEND OFF 
      , 
        '/home/product/Gliese/home/g2n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AT "G2N1" 
        AUTOEXTEND OFF 
    ONLINE 
    EXTSIZE 262144 
;

ERR-42000(40000): syntax error: 
        AUTOEXTEND OFF 
        ^        ^
Error at line 6
```

<a id="dd184be63270a836"></a>
##### 수정 전 대처

\ddl_db로 출력된 CREATE TABLESPACE 구문에서 AUTOEXTEND OFF와 AT &lt;domain_name&gt; 위치를 수정하여 실행한다.

```
gSQL> CREATE DISK DATA TABLESPACE "DISK_TEST_01" 
    DATAFILE 
        '/home/product/Gliese/home/g1n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AUTOEXTEND OFF 
        AT "G1N1" 
      , 
        '/home/product/Gliese/home/g2n1_home/db/DISK_TEST_01.dbf' 
        SIZE 104857600 REUSE 
        AUTOEXTEND OFF 
        AT "G2N1" 
    ONLINE 
    EXTSIZE 262144 
;

Tablespace created.
```

<a id="1c4e59b309f75cf7"></a>
### 21c.1.14 Patch Notes

<a id="f1ec82af14e2c08e"></a>
#### <kbd>ISSUE-4467</kbd> failed to synchronize replicas 에러가 발생하면 trace log에 출력한다.

<a id="297f30b747275bfe"></a>
##### 개요

[ERR-56008] failed to synchronize replicas 에러가 발생하면 trace log에 출력한다.

<a id="951530fc5faca89f"></a>
##### 현상 및 증상

없음

<a id="b412849abc227915"></a>
##### 수정 전 대처

없음

<a id="f01aae5c5f69f179"></a>
### 21c.1.13 Patch Notes

<a id="a2135529f17e0e60"></a>
#### <kbd>ISSUE-4454</kbd> TRACE_LOG_ID = xxxxx1로 설정한 환경에서 수행한 질의의 구간별 수행 시간이 trace log에 출력되지 않는다.

<a id="7725b57d0a6ba279"></a>
##### 개요

Property TRACE_LOG_ID = xxxxx1로 설정한 환경에서 수행한 질의의 구간별 수행 시간이 trace log에 출력되지 않는 문제가 있다. TRACE_LOG_ID에서 1의 자리는 구간별 수행시간 출력 여부를 판단하는 flag로써 이 값이 1이면 수행한 질의의 구간별 수행시간을 출력한다.

<a id="e4c04df5a270d2cc"></a>
##### 현상 및 증상

TRACE_LOG_ID = xxxxx1로 설정한 환경에서 수행한 질의의 구간별 수행 시간이 trace log에 출력되지 않는다.

```
[S][0.000000] SELECT * FROM dual

... 중략 ...

< Time Info >
======================================================
| Module    | Time             | Rate     | Call     |
------------------------------------------------------
| Parse     |   0:00:00.000000 |   0.00 % |        1 |
| Validate  |   0:00:00.000000 |   0.00 % |        1 |
| Cost Opt  |   0:00:00.000000 |   0.00 % |        1 |
| Code Opt  |   0:00:00.000000 |   0.00 % |        1 |
| Data Opt  |   0:00:00.000000 |   0.00 % |        1 |
| Execute   |   0:00:00.000000 |   0.00 % |        1 |
| Fetch     |   0:00:00.000000 |   0.00 % |        1 |
| Total     |   0:00:00.000000 | 100.00 % |          |
======================================================
```

<a id="9eb2e941294da598"></a>
##### 수정 전 대처

없음

<a id="a5a3b8a1361f8736"></a>
#### <kbd>ISSUE-4439</kbd> WHERE 절에 boolean type이 아닌 column만 명시된 경우, 비정상 종료될 수 있다.

<a id="c663c164bfe8e2f1"></a>
##### 개요

WHERE 절에 boolean type이 아닌 column만 명시된 경우, 비정상 종료될 수 있다. 비정상 종료되지 않더라도 physical filter로 분류될 경우 이 역시 bug 이다.

<a id="fa89c6c8a3d8c734"></a>
##### 현상 및 증상

다음 질의에서 table_name은 varchar type 인데 physical filter로 분류되어 처리되던 도중에 비정상 종료된다.

```
SELECT table_name 
  FROM DICTIONARY_SCHEMA.USER_TABLES
 WHERE table_name;
```

Bug를 fix한 후에 다음과 같이 정상적으로 수행되어 error가 발생한다.

```
SELECT table_name 
  FROM DICTIONARY_SCHEMA.USER_TABLES
 WHERE table_name;

ERR-22018(12123): data is not boolean literal
```

<a id="54bb60fca4d36673"></a>
##### 수정 전 대처

없음

<a id="4e9221355196b823"></a>
#### <kbd>ISSUE-4434</kbd> Rebalance 대상이 없는 멤버에서 REBALANCE를 수행하면 HANG이 걸린다.

<a id="6d1de5ae7b28a3d1"></a>
##### 개요

Rebalance 하려는 테이블을 포함하지 않은 cluster member에서 해당 테이블에 REBALANCE를 수행하면 HANG이 걸리는 문제가 발생한다.

<a id="2384360b3915089f"></a>
##### 현상 및 증상

Rebalance 할 테이블을 포함하지 않는 노드에서 TABLE REBALANCE를 수행하면 HANG 걸리는 문제가 발생한다.

<a id="67e26dbd33a7018e"></a>
##### 수정 전 대처

없음

<a id="7809ed1043c2afb2"></a>
### 21c.1.12 Patch Notes

<a id="449260f1293f1eae"></a>
#### <kbd>ISSUE-4410</kbd> SET 연산을 가진 subquery도 unnest 가능하도록 지원한다.

<a id="279b25f60379e52a"></a>
##### 개요

SET 연산을 가진 subquery는 unnesting 되지 않았으나, 이 patch로 인해 unnesting이 가능하게 되었다.

<a id="466e6042ff13798e"></a>
##### 현상 및 증상

SET 연산을 가진 subquery는 다음과 같이 unnest 되지 않고 있었다.

```
\EXPLAIN PLAN
SELECT * 
  FROM r
 WHERE r_c1 IN ( SELECT s_c1 FROM s 
                 UNION ALL
                 SELECT t_c1 FROM t  
                 UNION ALL
                 SELECT u_c1 FROM u
               )
;

R_C1 R_C2 R_C3 R_C4
---- ---- ---- ----
   1    1    1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      TABLE ACCESS ("R")                                      |
|    3  |  SUB QUERY LIST                                              |
|    4  |    INLINE_VIEW ("$V4") (MATERIALIZED)                        |
|    5  |      QUERY BLOCK ("$QB_IDX_6")                               |
|    6  |        UNION-ALL                                             |
|    7  |          QUERY BLOCK ("$QB_IDX_9")                           |
|    8  |            INDEX ACCESS ("S", "S_PRIMARY_KEY_INDEX")         |
|    9  |          QUERY BLOCK ("$QB_IDX_13")                          |
|   10  |            INDEX ACCESS ("T", "T_PRIMARY_KEY_INDEX")         |
|   11  |          QUERY BLOCK ("$QB_IDX_17")                          |
|   12  |            INDEX ACCESS ("U", "U_PRIMARY_KEY_INDEX")         |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2, R.R_C3, R.R_C4
     2  -  READ COLUMN : R.R_C1, R.R_C2, R.R_C3, R.R_C4
             POST FILTER : ( R.R_C1 ) IN ( $V4.S_C1 )
     4  -  COLUMN : S_C1 AS S_C1
     5  -  TARGET : S_C1
     6  -  SET TARGET : S_C1
     7  -  TARGET : S.S_C1
     8  -  READ INDEX COLUMN : S.S_C1
     9  -  TARGET : T.T_C1
    10  -  READ INDEX COLUMN : T.T_C1
    11  -  TARGET : U.U_C1
    12  -  READ INDEX COLUMN : U.U_C1

<<<  end print plan
```

이를 다음과 같이 unnest 되도록 변경하였다.

```
\EXPLAIN PLAN
SELECT * 
  FROM r
 WHERE r_c1 IN ( SELECT s_c1 FROM s 
                 UNION ALL
                 SELECT t_c1 FROM t  
                 UNION ALL
                 SELECT u_c1 FROM u
               )
;

R_C1 R_C2 R_C3 R_C4
---- ---- ---- ----
   1    1    1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      NESTED JOIN (SEMI)                                      |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        INLINE_VIEW ("$V5")                                   |
|    5  |          QUERY BLOCK ("$QB_IDX_6")                           |
|    6  |            UNION-ALL                                         |
|    7  |              QUERY BLOCK ("$QB_IDX_9")                       |
|    8  |                INDEX ACCESS ("S", "S_PRIMARY_KEY_INDEX")     |
|    9  |              QUERY BLOCK ("$QB_IDX_13")                      |
|   10  |                INDEX ACCESS ("T", "T_PRIMARY_KEY_INDEX")     |
|   11  |              QUERY BLOCK ("$QB_IDX_17")                      |
|   12  |                INDEX ACCESS ("U", "U_PRIMARY_KEY_INDEX")     |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2, R.R_C3, R.R_C4
     2  -  JOINED COLUMN : R.R_C1, R.R_C2, R.R_C3, R.R_C4
     3  -  READ COLUMN : R.R_C1, R.R_C2, R.R_C3, R.R_C4
     4  -  COLUMN : S_C1 AS S_C1
     5  -  TARGET : S_C1
     6  -  SET TARGET : S_C1
     7  -  TARGET : S.S_C1
     8  -  READ INDEX COLUMN : S.S_C1
             MIN RANGE : S.S_C1 = {R.R_C1}
             MAX RANGE : S.S_C1 = {R.R_C1}
           FETCH ONE ROW
     9  -  TARGET : T.T_C1
    10  -  READ INDEX COLUMN : T.T_C1
             MIN RANGE : T.T_C1 = {R.R_C1}
             MAX RANGE : T.T_C1 = {R.R_C1}
           FETCH ONE ROW
    11  -  TARGET : U.U_C1
    12  -  READ INDEX COLUMN : U.U_C1
             MIN RANGE : U.U_C1 = {R.R_C1}
             MAX RANGE : U.U_C1 = {R.R_C1}
           FETCH ONE ROW

<<<  end print plan
```

<a id="5ed6df057e182c6c"></a>
##### 수정 전 대처

없음

<a id="b6fe315dc2d0331c"></a>
#### <kbd>ISSUE-4404</kbd> 특정 노드를 fail-back 할 때 rebalance로 인해 전체 시스템이 멈추는 현상을 개선하였다.

<a id="0c30c3a9d430e25b"></a>
##### 개요

특정 노드를 fail-back 할 때 rebalance를 수행하면 노드와 관련된 group만 X lock 하는 것이 아니라 cluster 전체를 lock 하고 있었다. 이에 rebalance와 관련된 노드들만 lock 하도록 수정하였다.

<a id="7b77fbefabc71a69"></a>
##### 현상 및 증상

REBALANCE 수행과 관련 없는 노드의 테이블을 X-LOCK 하여 테이블을 사용할 수 없게 된다.

<a id="f7ae6bf390a8ac91"></a>
##### 수정 전 대처

없음

<a id="1a5354f41ccc1d55"></a>
### 21c.1.11 Patch Notes

<a id="ce4a9670e85e88fc"></a>
#### <kbd>ISSUE-4370</kbd> Outer join 일 때 where 절에 case function을 포함하는 filter가 사용되면 비정상 종료될 수 있다.

<a id="6b25a1fa068aff61"></a>
##### 개요

Outer join 일 때 where 절에 case function을 포함하는 filter가 사용되면 비정상 종료될 수 있다.

<a id="1a81dd704c4fccf8"></a>
##### 현상 및 증상

Outer join이면 outer join operation elimination이 가능한지 검사한다. 이 때 where 절에 case function이 있으면 비정상 종료된다.

```
DROP TABLE r;
DROP TABLE s;
COMMIT;

CREATE TABLE r ( r_c1 INTEGER, r_c2 INTEGER );
INSERT INTO r VALUES ( 1, 1 );
COMMIT;

CREATE TABLE s ( s_c1 INTEGER, s_c2 INTEGER );
INSERT INTO s VALUES ( 1, 1 );
COMMIT;

\explain plan
SELECT *
  FROM r LEFT OUTER JOIN s ON r_c1 = s_c1
 WHERE CASE WHEN s_c1 > 0 THEN 1 ELSE 0 END = 1 
;  

R_C1 R_C2 S_C1 S_C2
---- ---- ---- ----
   1    1    1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (INNER JOIN)                                  |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        HASH JOIN INSTANT                                     |
|    5  |          TABLE ACCESS ("S")                                  |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2, S.S_C1, S.S_C2
     2  -  JOINED COLUMN : R.R_C1, R.R_C2, S.S_C1, S.S_C2
     3  -  READ COLUMN : R.R_C1, R.R_C2
     4  -  HASH KEY : S.S_C1
           RECORD COLUMN : S.S_C2
           READ KEY COLUMN : S.S_C1, S.S_C2
             HASH FILTER : S.S_C1 = R.R_C1
     5  -  READ COLUMN : S.S_C1, S.S_C2
             LOGICAL FILTER : CASE WHEN S.S_C1 > 0 THEN 1 ELSE 0 END  = 1

<<<  end print plan
```

<a id="7e67e33e113aad6d"></a>
##### 수정 전 대처

없음

<a id="3cfc5270311b4998"></a>
### 21c.1.10 Patch Notes

<a id="a2dd270324343ed2"></a>
#### <kbd>ISSUE-4285</kbd> Stored function을 포함하는 filter도 index join을 수행할 수 있게 되었다.

<a id="e39f264e9261c6ba"></a>
##### 개요

Stored function이나 non-deterministic built-in function (예: RANDOM)이 포함된 filter는 join method를 결정하는 filter로 사용되지 못했는데 이를 사용할 수 있도록 수정하였다.

<a id="341b816c890f073f"></a>
##### 현상 및 증상

다음은 join condition이 있지만 full nested join으로 수행한 후에 s_c1 = func1( r_c1 )를 적용하여 결과를 도출하는 예이다.

```
DROP TABLE r;
DROP TABLE s;
COMMIT;


CREATE TABLE r ( r_c1 INTEGER, r_c2 INTEGER );
COMMIT;

INSERT INTO r VALUES ( 1, 1 );
COMMIT;

CREATE TABLE s ( s_c1 INTEGER, s_c2 INTEGER );
CREATE UNIQUE INDEX idx_s ON s( s_c1 );
COMMIT;

INSERT INTO s VALUES ( 1, 1 );
COMMIT;


CREATE OR REPLACE FUNCTION func1( a1 INTEGER ) RETURN INTEGER
AS
   v1 INTEGER;
BEGIN
   SELECT 0 + a1 INTO v1
     FROM dual;
   RETURN v1;
END;
/


\explain plan
SELECT *
  FROM r, s
 WHERE s_c1 = func1( r_c1 )
   AND r_c2 = 1
;  

R_C1 R_C2 S_C1 S_C2
---- ---- ---- ----
   1    1    1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      NESTED JOIN (INNER JOIN)                                |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        TABLE ACCESS ("S")                                    |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2, S.S_C1, S.S_C2
     2  -  JOINED COLUMN : S.S_C1, R.R_C1, R.R_C2, S.S_C2
             POST WHERE FILTER : S.S_C1 = "FUNC1"( R.R_C1 )
     3  -  READ COLUMN : R.R_C1, R.R_C2
             PHYSICAL FILTER : R.R_C2 = 1
     4  -  READ COLUMN : S.S_C1, S.S_C2

<<<  end print plan
```

다음은 수정 후 동일한 질의를 수행한 결과이다. Index nested loop join으로 수행할 수 있게 되었다.

```
gSQL> \explain plan
SELECT *
  FROM r, s
 WHERE s_c1 = func1( r_c1 )
   AND r_c2 = 1
;
    
R_C1 R_C2 S_C1 S_C2
---- ---- ---- ----
   1    1    1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       
|    2  |      NESTED JOIN (INNER JOIN)                                |                      
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        INDEX ACCESS ("S", "IDX_S")                           |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2, S.S_C1, S.S_C2
     2  -  JOINED COLUMN : R.R_C1, R.R_C2, S.S_C1, S.S_C2
     3  -  READ COLUMN : R.R_C1, R.R_C2
             PHYSICAL FILTER : R.R_C2 = 1
     4  -  READ INDEX COLUMN : S.S_C1
           READ TABLE COLUMN : S.S_C2
             MIN RANGE : S.S_C1 = "FUNC1"( {R.R_C1} )
             MAX RANGE : S.S_C1 = "FUNC1"( {R.R_C1} )
           FETCH ONE ROW

<<<  end print plan
```

<a id="a91720de109a6d84"></a>
##### 수정 전 대처

없음

<a id="d79d9307b742f12b"></a>
### 21c.1.9 Patch Notes

<a id="38f7b4fa05910a1a"></a>
#### <kbd>ISSUE-3496</kbd> IPC 연결을 지원한다.

<a id="9c3e741fc646603f"></a>
##### 개요

같은 장비에 있는 서버와 ODBC 클라이언트의 IPC 연결을 지원한다.

<a id="5a39516d704deb04"></a>
##### 현상 및 증상

없음

<a id="a9d17508fdd9320c"></a>
##### 수정 전 대처

없음

<a id="4ece6aca38af3566"></a>
#### <kbd>ISSUE-4357</kbd> JDBC의 연결 프로퍼티에 boolean 타입을 추가하여 유효값을 변경하였다.

<a id="9a2aa9c0b8922f79"></a>
##### 개요

JDBC에는 {true, false}, {on, off}, {0, 1}을 유효값으로 사용하는 [연결 프로퍼티](../part-05-developer-manual/32-jdbc.md#9b0cd1f4eef62747)가 있다. 이런 연결 프로퍼티들을 boolean 타입으로 간주하여 true, on, yes, 1 / false, off, no, 0을 동치인 유효값으로 처리하도록 하였다.

<a id="a89887db10e2a2ef"></a>
##### 현상 및 증상

연결 프로퍼티 statement_pool_on의 유효값은 "1" 또는 "0" 이다. 그 외의 값이 사용되면 에러가 발생한다. include_synonyms의 유효값은 "true" 또는 "false" 이고 trace_log의 유효값은 "on" 또는 any string 이다. 이런 연결 프로퍼티의 공통점은 유효값이 boolean 타입으로 사용된다는 것이다. Boolean 타입에 연결 프로퍼티의 혼동을 줄이기 위해 true, on, yes, 1 / false, off, no, 0을 동치로 사용하도록 하였다.

<a id="b1a966ac8f9da98a"></a>
##### 수정 전 대처

없음

<a id="a56059fe6ad2876e"></a>
#### <kbd>ISSUE-4355</kbd> ODBC에 FAILOVER_ROUTING_POLICY 속성을 추가하였다.

<a id="ac0c33f8a87bef05"></a>
##### 개요

ODBC에 FAILOVER_ROUTING_POLICY 속성을 추가하였다.

<a id="ffe4f0ac745fd9d5"></a>
##### 현상 및 증상

기존 ODBC는 ALTERNATE_SERVERS의 마지막 서버에서 장애가 발생하면 처음 접속한 서버로 failover를 진행한다.  ALTERNATE_SERVERS의 마지막 서버에서 장애가 발생했을 때 failover가 종료되도록 ODBC에 FAILOVER_ROUTING_POLICY 속성을 추가하였다.

<a id="e6113d57111e54d4"></a>
##### 수정 전 대처

없음

<a id="1a6fa1029e301e15"></a>
#### <kbd>ISSUE-4354</kbd> POSIX timer를 생성하여 signal이 주기적으로 발생하면 ODBC의 login timeout과 connection timeout이 정상적으로 동작하지 않는다.

<a id="b08356a893ea76af"></a>
##### 개요

POSIX timer를 생성하여 signal이 주기적으로 발생하면 ODBC의 login timeout과 connection timeout이 정상적으로 동작하지 않는다.

<a id="5f867744791063d5"></a>
##### 현상 및 증상

ODBC에서 SQL_ATTR_LOGIN_TIMEOUT과 SQL_ATTR_CONNECTION_TIMEOUT으로 설정된 timeout 만큼 대기하는 도중에 POSIX timer로부터 주기적으로 signal을 받을 경우 설정된 timeout 보다 더 긴 시간 동안 대기한다.

<a id="4256585a7771aaa3"></a>
##### 수정 전 대처

Login timeout과 connection timeout을 사용할 경우 POSIX timer를 사용하지 않는다.

<a id="e9cb388bcb6bb7cf"></a>
### 21c.1.8 Patch Notes

<a id="b07069eecce9d4a0"></a>
#### <kbd>ISSUE-4348</kbd> ODBC 환경에서 login timeout 및 connection timeout이 발생하면 failover가 가능하도록 한다.

<a id="51b32d83e1d4a0d5"></a>
##### 개요

SQL_ATTR_LOGIN_TIMEOUT과 SQL_ATTR_CONNECTION_TIMEOUT을 설정하여 timeout이 발생한 경우, alternate_servers에 있는 서버로 failover가 되지 않는다.

<a id="d082628c73eb9b1a"></a>
##### 현상 및 증상

ODBC 환경에서 login timeout 및 connection timeout이 발생하면 failover가 동작하지 않고 바로 에러가 반환된다.

<a id="ef841c83de10d839"></a>
##### 수정 전 대처

없음

<a id="7518c5811509edc5"></a>
#### <kbd>ISSUE-4316</kbd> V$STATEMENT를 수행하면 간헐적으로 datatime field overflow 에러가 발생한다.

<a id="9a132dc260d27127"></a>
##### 개요

V$STATEMENT를 수행하는 도중에 session이 죽거나 종료되면 쓰레기 값을 읽어오는 문제가 발생할 수 있다. 쓰레기 값을 읽어서 출력하려다보니 datatime field overflow가 발생한다.

<a id="021a58a81fd72779"></a>
##### 현상 및 증상

여러 statement들이 수행되는 도중에 V$STATEMENT를 수행하면 간헐적으로 datatime field overflow 에러가 발생한다.

<a id="a979333bae959c12"></a>
##### 수정 전 대처

올바른 값이 출력될 때까지 다시 수행한다.

<a id="3c321d9c9173723b"></a>
### 21c.1.7 Patch Notes

<a id="ad82dcdf1f6d92a6"></a>
#### <kbd>ISSUE-4327</kbd> 클러스터 환경에서 동시에 여러 멤버에서 재시작 복구를 수행하면 in doubt 트랜잭션의 잘못된 복구로 인해 조인에 실패한다.

<a id="f8de3304b4b1604a"></a>
##### 개요

클러스터 환경에서 클러스터 멤버가 재시작 복구를 수행할 때 PREPARE 상태의 in doubt 트랜잭션도 복구한다. in doubt 트랜잭션의 복구는 MOUNT 단계 이상의 다른 클러스터 멤버들에게 트랜잭션 처리 결과를 요청하고 취합하여 COMMIT 또는 ROLLBACK 하는 방식으로 수행된다.  
두 개의 멤버들이 동일한 in doubt 트랜잭션을 동시에 복구할 때 트랜잭션의 상태와 SCN을 설정하고 구하는 과정이 atomic하게 처리되지 않는 오류로 인해 유효하지 않은 값이 시스템 SCN에 설정되어 조인에 실패한다.

<a id="0feedf1960f878c8"></a>
##### 현상 및 증상

시스템 SCN이 유효하지 않은 값으로 설정되어 멤버가 클러스터 데이터베이스에 조인하지 못한다.

<a id="52b32b24ba6dd475"></a>
##### 수정 전 대처

잘못된 SCN이 설정된 클러스터 멤버를 클러스터에서 제거하거나 새로운 멤버를 추가한다.

<a id="faae4831a73e5c76"></a>
### 21c.1.6 Patch Notes

<a id="6746f97433c48312"></a>
#### <kbd>ISSUE-5678</kbd> PSM 내에서 사용하는 모든 SQL 구문에 NULL 상수를 사용하면 잘못된 메모리에 접근할 수 있다.

<a id="efd642fa978bf0f7"></a>
##### 개요

PSM 내의 SQL 구문에 PSM 변수와 NULL 값을 함께 사용하면 잘못된 메모리에 접근한다.

<a id="31cdc90088aa3b33"></a>
##### 현상 및 증상

다음과 같은 쿼리를 수행하면 서버가 비정상적으로 종료된다.

```
gSQL> DECLARE
        v1 NUMBER := 1;
      BEGIN
        INSERT INTO t1 ( c1, c2, c3, c4 )
         VALUES ( 1, null, null, null );
      END;
      /
```

<a id="95c772545fab8c90"></a>
##### 수정 전 대처

SQL 구문에 NULL과 PSM 변수를 함께 사용하지 않는다.

```
gSQL> 
DECLARE
  v1 NUMBER;
  v2 NUMBER;
  v3 NUMBER;
  v4 NUMBER;
BEGIN
  v1 := 1;
  v2 := null;
  v3 := null;
  v4 := null;
  
  INSERT INTO t1 ( c1, c2, c3, c4 )
         VALUES( v1, v2, v3, v4 );
END;
/
```

<a id="2f51686f5c88771a"></a>
#### <kbd>ISSUE-4286</kbd> 조건을 비교하여 결과를 선택하는 함수를 수행할 때 함수 인자에 오류가 있을 경우, 그 인자를 수행할 필요가 없는 경우에도 수행하여 오류가 발생한다.

<a id="761f1d9bcb6ce6c7"></a>
##### 개요

CASE2, DECODE, NVL, NVL2, COALESCE와 같이 조건을 비교하여 결과를 선택하는 함수를 수행할 때  
함수 인자들을 모두 수행한 후에 조건을 비교하여 결과를 선택한다. 따라서 함수 인자에 오류가 있을 경우 수행할 필요가 없는 인자들에 대해서도 오류가 발생한다.

<a id="a853598b4b8faa70"></a>
##### 현상 및 증상

```
gSQL> CREATE TABLE r ( c1 INTEGER );

Table created.

gSQL> INSERT INTO r VALUES ( 0 );

1 row created.

gSQL> COMMIT;

Commit complete.


gSQL> 
SELECT CASE2( c1 <> 0, 100/c1, c1 ) AS result
  FROM r;

ERR-22012(12122): divisor is equal to zero : 
       CASE2( c1 <> 0, 100/c1, c1 ) AS result
                       *
ERROR at line 2:

gSQL> 
SELECT DECODE( c1, 0, c1, 100/c1 ) AS result
  FROM r;

ERR-22012(12122): divisor is equal to zero : 
       DECODE( c1, 0, c1, 100/c1 ) AS result
                          *
ERROR at line 2:

gSQL> 
SELECT NVL( c1, 100/c1 ) AS result
  FROM r;

ERR-22012(12122): divisor is equal to zero : 
       NVL( c1, 100/c1 ) AS result
                *
ERROR at line 2:

gSQL> 
SELECT NVL2( c1, c1, 100/c1 ) AS result
  FROM r;

ERR-22012(12122): divisor is equal to zero : 
       NVL2( c1, c1, 100/c1 ) AS result
                     *
ERROR at line 2:

gSQL> 
SELECT COALESCE( c1, 100/c1 ) AS result
  FROM r;

ERR-22012(12122): divisor is equal to zero : 
SELECT COALESCE( c1, 100/c1 ) AS result
                     *
ERROR at line 1:
```

<a id="4c3ad83de6ed508c"></a>
##### 수정 후

조건을 비교하여 결과가 TRUE이면 대응되는 result를 반환하고, 그 이후에는 평가하지 않는다.

Result에 해당되는 expression이 상수인 경우, prepare 중에 타입 변환을 수행하도록 변경하였다. 따라서 상수 result expression으로 인한 타입 변환 에러가 발생하지 않을 수 있다.  
(수정하기 전에는 execute 도중에 조건을 수행하여 그에 해당하는 상수 result expression의 타입을 변환한 후에 결과로 반환되었다.)

다음 예제의 결과 타입은 number 이다.  
Default인 'DEFAULT VALUE'는 숫자로 변환될 수 있는 문자가 아니므로 number 타입으로 변환하는 도중에 에러가 발생한다. 이 에러는 prepare 과정 중에 발생한다.

```
gSQL>
SELECT DECODE( c1, 0, c1, 'DEFAULT VALUE' ) FROM r WHERE c1 = 0;

ERR-22018(12006): data value is not a numeric literal : 
SELECT DECODE( c1, 0, c1, 'DEFAULT VALUE' ) FROM r WHERE c1 = 0
                          *
ERROR at line 1:
```

<a id="4cfa9f0feaed8987"></a>
##### 결과 타입의 부가 정보

- 결과 타입이 time, time with time zone, timestamp, timestamp with time zone, interval 인 경우,   
  각 result expression을 포함할 수 있는 정보로 설정한다.  
  (수정 전에는 첫 번째 result expression의 부가 정보로 설정하였다. )

- 결과 타입이 time, time with time zone, timestamp, timestamp with time zone 인 경우,  
  precision을 각 expression에서 가장 큰 값으로 지정한다.

- 결과 타입이 interval인 경우,  
  interval indicator는 각 expression의 indicator를 조합한다.  
  precision과 scale은 각 expression에서 제일 큰 값으로 지정한다.

<a id="efeaeb27793b5ded"></a>
##### 수정 전 대처

CASE 구문으로 표현할 수 있다.

```
SELECT CASE2( c1 <> 0, 100/c1, c1 ) AS result
  FROM r;
==>
gSQL> 
SELECT CASE WHEN c1 <> 0
            THEN 100/c1
            ELSE c1
        END AS result
  FROM r;

RESULT
------
     0

1 row selected.


SELECT DECODE( c1, 0, c1, 100/c1 ) AS result
  FROM r;
==>
gSQL> 
SELECT CASE WHEN ( c1 = 0 ) OR ( c1 IS NULL AND 0 IS NULL ) 
            THEN c1
            ELSE 100/c1
       END AS result
  FROM r;

RESULT
------
     0

1 row selected.


SELECT COALESCE( c1, 100/c1 ) AS result
  FROM r;
==>
gSQL> 
SELECT CASE WHEN c1 IS NOT NULL 
            THEN c1
            ELSE 100/c1
       END AS result
  FROM r;

RESULT
------
     0

1 row selected.


SELECT NVL( c1, 100/c1 ) AS result
  FROM r;
==>
gSQL> 
SELECT CASE WHEN c1 IS NOT NULL 
            THEN c1
            ELSE 100/c1
       END AS result
  FROM r;

RESULT
------
     0

1 row selected.


SELECT NVL2( c1, c1, 100/c1 ) AS result
  FROM r;
==>
gSQL> 
SELECT CASE WHEN c1 IS NOT NULL
            THEN c1
            ELSE 100/c1
       END AS result
  FROM r;

RESULT
------
     0

1 row selected.
```

<a id="bdf8a01dfcfb24b0"></a>
#### <kbd>ISSUE-4317</kbd> SQL_ATTR_CONNECTION_TIMEOUT 속성을 지원한다.

<a id="60d5f4ddbbe44d75"></a>
##### 개요

네트워크가 불안정할 경우, 클라이언트가 서버에 질의한 후에 응답을 받지 못하고 계속 blocking 상태에 머물 수 있다. 이런 문제를 해결하기 위해 SQLSetConnectAttr()의 SQL_ATTR_CONNECTION_TIMEOUT 속성을 지원한다.

SQL_ATTR_CONNECTION_TIMEOUT 값을 설정하면 클라이언트는 서버에 질의한 후에 해당 시간만큼 응답을 기다린다. 만일 주어진 시간 동안 응답이 없을 경우 클라이언트는 서버와의 연결을 끊고, HYT01 Connection timeout expired 에러를 반환한다.

<a id="05f5f47c6f95ada2"></a>
##### 현상 및 증상

네트워크가 불안정할 경우 클라이언트는 서버에 응답을 요청한 후 일정 시간 동안 대기한다.

<a id="e6cb284846d0308b"></a>
##### 수정 전 대처

다음과 같이 kernel 속성값을 변경하면 클라이언트와 서버의 연결에 이상이 있는지 여부를 빨리 감지할 수 있다.

```
net.ipv4.tcp_keepalive_time = 3
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.tcp_keepalive_intvl = 3
net.ipv4.tcp_retries2 = 5
```

<a id="fde5eaa6bb46b4ef"></a>
#### <kbd>ISSUE-4031</kbd> .Net Framework에서 테이블의 column 이름이 정상적으로 표시되지 않는다.

<a id="91901427dc01d421"></a>
##### 개요

SQLColAttribute()와 SQLGetDescField()에서 column 이름을 조회할 때 사용되는 속성은 SQL_DESC_LABEL, SQL_DESC_NAME 또는 SQL_DESC_BASE_COLUMN_NAME 이다. SQL_DESC_LABEL은 column의 label이 있는 경우 label을 반환한다. SQL_DESC_NAME은 column의 alias가 있을 경우 alias를 반환한다. SQL_DESC_BASE_COLUMN_NAME은 column name을 반환한다.

Data provider for ODBC인 .Net Framework는 column 이름을 조회할 때 SQL_DESC_NAME을 사용하는데 column 이름에 label을 부여할 경우 의도치 않은 column 이름이 조회된다. 따라서 .Net Framework를 위한 연결 속성 DOT_NET_FOR_ODBC를 추가하여 이를 개선하였다.

<a id="a46da4ce7d14ad70"></a>
##### 현상 및 증상

gsql에서 다음과 같은 query를 실행하면 column 이름은 다음과 같이 조회된다.

```
gSQL> SELECT I1, I1 + I1, I1 AS C1 FROM TEST;

I1 I1 + I1 C1
-- ------- --
 1       2  1
```

Data provider for ODBC인 .Net Framework에서 위의 query를 실행하면 다음과 같이 조회된다.

```
SELECT I1, I1 + I1, I1 AS C1 FROM TEST;
I1 NULL C1
-- ---- --
 1    2  1
```

<a id="25656e388e0cf40d"></a>
##### 수정 전 대처

없음

<a id="05f8f42103a80dbe"></a>
#### <kbd>ISSUE-4302</kbd> 클러스터 환경에서 트랜잭션을 commit 하면 commit 서버가 비정상 종료된다.

<a id="cd5be9fd63845372"></a>
##### 개요

클러스터 환경에서 많은 테이블을 갱신한 트랜잭션을 commit 하면 commit 서버가 비정상적으로 종료되고 재시작에 실패한다.

<a id="1dec77bba934afa4"></a>
##### 현상 및 증상

클러스터 환경에서 트랜잭션을 commit 하면 해당 트랜잭션이 갱신한 모든 테이블들에 대해 테이블 SCN을 설정하고 로깅한다. 하나의 트랜잭션이 500 개 이상의 테이블들을 갱신할 경우 로깅을 위해 사용한 버퍼의 크기가 부족해져서 commit 서버가 비정상적으로 종료된다. 또한 로그도 정상적으로 기록되지 않아서 재시작에 실패한다.

<a id="d6f4ee7ff965fb51"></a>
##### 수정 전 대처

없음

<a id="0cb5c60e41dd026e"></a>
#### <kbd>ISSUE-4308</kbd> View name이 명시되지 않은 sub table을 포함하는 hierarchy query 수행시 잘못된 결과가 나온다.

<a id="a149068dc7cc796a"></a>
##### 개요

View name이 명시되지 않은 sub table을 포함하는 hierarchy query를 수행하면 잘못된 결과가 나온다.

<a id="4e0ffbfe4a6b79e0"></a>
##### 현상 및 증상

```
--# 정상적인 상황
--# result : 1 row
--#          1,   0
gSQL> SELECT C1, C2
  FROM T1
 START WITH C1 = C1
 CONNECT BY C1 = PRIOR C2;
    
C1 C2
-- --
 1  0

1 row selected.



--# BUGBUG
--# result : 1 row
--#          1,   0
gSQL> SELECT C1, C2
  FROM ( SELECT C1, C2 FROM T1 )
 START WITH C1 = C1
 CONNECT BY C1 = PRIOR C2;
     
  C1 C2
---- --
null  0

1 row selected.
```

<a id="76aec85ef0b228b1"></a>
##### 수정 전 대처

Sub table에 view name을 명시한다.

```
gSQL>  SELECT C1, C2
  FROM ( SELECT C1, C2 FROM T1 ) V1
 START WITH C1 = C1
 CONNECT BY C1 = PRIOR C2;
 
C1 C2
-- --
 1  0

1 row selected.
```

<a id="7c2cc008bcbb34e9"></a>
#### <kbd>ISSUE-4244</kbd> Package 생성 후 실행하면 invalid package object status 에러가 발생한다.

<a id="df41b42e7eefc837"></a>
##### 개요

Package를 생성한 후에 실행하면 invalid package object status 에러가 발생한다.

<a id="cbc0f03bac1748e6"></a>
##### 현상 및 증상

다음 예와 같이 package를 생성한 후에 처음으로 실행하면 invalid package object status 에러가 발생한다.

```
gSQL> CREATE TABLE r ( r_c1 INTEGER, r_c2 INTEGER );

Table created.

gSQL> INSERT INTO r VALUES ( 1, 1 );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> CREATE PACKAGE pkg1 AS
  v1 INTEGER;

  PROCEDURE proc1;
  PROCEDURE proc2;
END;
/

Package created.

gSQL> CREATE PACKAGE BODY pkg1 AS
  PROCEDURE proc1 AS
    x1 INTEGER;
  BEGIN
    INSERT INTO r VALUES ( 1, 1 );
    COMMIT;

    proc2;

    x1 := pkg1.v1;
  END;

  PROCEDURE proc2 AS
  BEGIN
    SELECT r_c1 INTO pkg1.v1
      FROM r
     LIMIT 1;
  END;
END;
/

Package created.

gSQL> COMMIT;

Commit complete.

gSQL> CALL pkg1.proc1;

ERR-2F000(17088): invalid package (PKG1) object status
ERR-2F000(17007): invalid expression :
    x1 := pkg1.v1;
          *
ERROR at line 9:
```

<a id="f69cb76d0c0ece6d"></a>
##### 수정 전 대처

없음

<a id="8795be5de5728e8d"></a>
#### <kbd>ISSUE-4156</kbd> gloader binary 모드의 구조가 변경되었다.

<a id="598c930d8c547482"></a>
##### 개요

gloader binary 모드의 구조가 개선되었다. 이로 인해 binary 파일의 구조가 변경되어 이전 버전의 binary 파일과 호환되지 않는다.

<a id="a018d2414ef7b996"></a>
##### 현상 및 증상

없음

<a id="38849187d96486d4"></a>
##### 수정 전 대처

없음

<a id="d2eed774ade70649"></a>
#### <kbd>ISSUE-4263</kbd> Sharded 테이블을 merge shard 한 후에 split shard가 실패한다.

<a id="5b7a8f79469f6649"></a>
##### 개요

Sharded 테이블을 merge shard 한 후에 split shard를 수행할 때 테이블에서 사용 중인 shard id가 새로운 shard에 할당되어 split이 실패한다. Split shard를 수행하면서 새로운 shard id를 구할 때 오류가 생겨 발생하는 문제이다.

<a id="881485e320877070"></a>
##### 현상 및 증상

Sharded 테이블을 merge shard 한 후에 split shard를 수행하면 다음과 같이 실패한다.

```
gSQL> CREATE TABLE T1
( 
    I1 INTEGER,
    I2 INTEGER,
    I3 LONG VARCHAR
) 
    SHARDING BY RANGE (I1)
    SHARD S1 VALUES LESS THAN ( 200 )    AT CLUSTER GROUP G1,
    SHARD S2 VALUES LESS THAN ( 400 )    AT CLUSTER GROUP G1,
    SHARD S3 VALUES LESS THAN ( 600 )    AT CLUSTER GROUP G2,
    SHARD S4 VALUES LESS THAN ( 800 )    AT CLUSTER GROUP G2,
    SHARD S5 VALUES LESS THAN ( 1000 )   AT CLUSTER GROUP G3,
    SHARD S6 VALUES LESS THAN (MAXVALUE) AT CLUSTER GROUP G3
;

Table created.

gSQL> ALTER TABLE T1 MERGE SHARDS S1, S2, S3 INTO S123 AT CLUSTER GROUP G2;

Table altered.

gSQL> ALTER TABLE T1 SPLIT SHARD S5 INTO ( SHARD S7 VALUES LESS THAN ( 900 ) AT CLUSTER GROUP G3 );

ERR-23000(15006): "SHARD_RANGE_PRIMARY_KEY": dictionary integrity constraint violation by concurrent DDL execution
```

<a id="98a59bc4d8ce65ac"></a>
##### 수정 전 대처

없음

<a id="767b95ebfab2658f"></a>
#### <kbd>ISSUE-4247</kbd> Precompiler gpec에 autocommit 옵션을 지원한다.

<a id="c58acdcd25bff33e"></a>
##### 개요

gpec 옵션으로 autocommit을 지원한다. gpec의 autocommit 옵션이 주어지면 gc 파일에 있는 모든 연결이 AUTO COMMIT ON으로 실행된다.

<a id="7455193ef1251ed9"></a>
##### 현상 및 증상

없음

<a id="02520123e42bd3ff"></a>
##### 수정 전 대처

없음

<a id="9f55fe0ea45df94e"></a>
#### <kbd>ISSUE-3825</kbd> JDBC에서 blob과 clob 클래스를 지원한다.

<a id="84d1ff8342fb4323"></a>
##### 개요

JDBC에서 blob과 clob 클래스를 지원한다.

<a id="f0fcc8dd6c7bb7cf"></a>
##### 현상 및 증상

없음

<a id="0b86aed879ff4989"></a>
##### 수정 전 대처

없음

<a id="0f183ddd63653d0a"></a>
#### <kbd>ISSUE-4261</kbd> 특정 크기의 데이터 파일을 생성하면 validation 오류가 발생한다.

<a id="0fc400504db0076c"></a>
##### 개요

테이블스페이스를 생성하거나 데이터 파일을 추가할 때 데이터 파일 크기를 특정값으로 설정하면 세션이 비정상적으로 종료된다. 데이터 파일 크기 중 특정값에 대한 validation 오류로 인해 발생하는 문제이다.

<a id="2ba07976057b0bbf"></a>
##### 현상 및 증상

테이블스페이스를 생성할 때 데이터 파일 크기를 특정값으로 설정하면 다음과 같이 세션이 비정상적으로 종료된다.

```
gSQL> CREATE TABLESPACE TEST_TBS DATAFILE 'test.dbf' SIZE 314630144;
=================================================
CALL STACK
=================================================
...
gsql(main+0x413)[0x558c34]
/lib64/libc.so.6(__libc_start_main+0xf5)[0x7fb3399f9555]
gsql[0x5396f9]
```

<a id="e3101ee6036c80ae"></a>
##### 수정 전 대처

생성하려는 데이터 파일 크기를 다른 값으로 설정한다.

<a id="8e8ac632054ac0b0"></a>
#### <kbd>ISSUE-4254</kbd> Cluster에서 DISTINCT가 포함된 subquery를 수행하면 remote server에서 구문 에러가 발생한다.

<a id="816e53bb060b82fa"></a>
##### 개요

Cluster system에 DISTINCT가 포함된 subquery가 기술되어 있고, 참조되지 않은 subquery의 target이 존재할 경우 해당 질의로 cluster query를 구성하여 수행하면 remote server에서 구문 에러가 발생한다.  
생성된 cluster query의 target expression 개수와 view column name 개수가 불일치하여 발생하는 문제이다.

<a id="546537168aea7478"></a>
##### 현상 및 증상

```
gSQL> CREATE TABLE t1 ( i1 INTEGER, i2 INTEGER ) SHARDING BY HASH( i1 );

Table created.

gSQL> commit;

Commit complete.

gSQL> SELECT v1.i1 FROM ( SELECT DISTINCT i1, i2 FROM t1) v1;

ERR-42000(16241): MEMBER(G2N1): invalid number of column names specified : 
SELECT /*+ NO_MERGE( _A1 ) */ * FROM ( SELECT /*+ USE_DISTINCT_HASH(50) FULL( _A2 ) */ DISTINCT "_A2"."I1", "_A2"."I2" FROM "PUBLIC"."T1"@LOCAL AS "_A2" ) AS "_A1"("I1")
                                                                                                                                                              *
ERROR at line 1:
```

<a id="95d368257dc7966e"></a>
##### 수정 전 대처

DISTINCT 구문을 GROUP BY 구문으로 변환한다.

DISTINCT를 기술한 query 내에 GROUP BY가 기술되지 않은 경우, DISTINCT 대상들을 모두 GROUP BY로 정의하고 DISTINCT를 생략한다.

```
gSQL> SELECT v1.i1 FROM ( SELECT i1, i2 FROM t1 GROUP BY i1, i2 ) v1;

no rows selected.
```

<a id="2f828a2e8fcb5307"></a>
#### <kbd>ISSUE-4246</kbd> EXEC SQL AUTOCOMMIT 구문에서 AT 절을 사용하면 에러가 발생한다.

<a id="8f5297efedcd93ec"></a>
##### 개요

EXEC SQL AT :db_name AUTOCOMMIT 구문에서 AT 절을 인식하지 못하여 INVALID HANDLE 에러가 발생한다.

<a id="916a4c069812919d"></a>
##### 현상 및 증상

다음 구문에서 에러가 발생한다.

```
EXEC SQL BEGIN DECLARE SECTION;
char         sConnName[10]="con";
EXEC SQL END DECLARE SECTION;

EXEC SQL AT :sConnName AUTOCOMMIT ON;
```

```
[ERROR] SQL ERROR -
SQLCODE : -2
SQLSTATE : HY000
ERROR MSG : Invalid handle
FAILURE
```

<a id="fb438538534b1e02"></a>
##### 수정 전 대처

없음

<a id="6de16c6d5bdb7ba4"></a>
### 21c.1.5 Patch Notes

<a id="3d88e1389cb37d95"></a>
#### <kbd>ISSUE-4234</kbd> ADD MEMBER 후 PSM DDL을 수행하면 ROUTINE primary key에 대한 dictionary integrity constraint violation 에러가 발생할 수 있다.

<a id="c5c9585a8ba13125"></a>
##### 개요

ADD MEMBER 후 PSM DDL을 수행하면 ROUTINE primary key에 대한 dictionary integrity constraint violation 에러가 발생하는 문제가 있어 이를 수정하였다.

<a id="46f29aa2cd6527bc"></a>
##### 현상 및 증상

다음과 같이 routine을 생성한 후에 cluster member를 추가하고 나서 routine을 생성하면 에러가 발생한다.

```
gSQL> 
CREATE OR REPLACE FUNCTION u1.func1 ()
RETURN INTEGER
AS
BEGIN
    RETURN 0;
END;
/

Function created.

gSQL> 
CREATE OR REPLACE FUNCTION u1.func2 ()
RETURN INTEGER
AS
BEGIN
    RETURN 0;
END;
/

Function created.

gSQL> 
CREATE OR REPLACE FUNCTION u1.func3 ()
RETURN INTEGER
AS
BEGIN
    RETURN 0;
END;
/

Function created.

gSQL> 
CREATE OR REPLACE FUNCTION u1.func4 ()
RETURN INTEGER
AS
BEGIN
    RETURN 0;
END;
/

Function created.
```

```
\connect as sysdba

gSQL> ALTER CLUSTER GROUP G3 ADD CLUSTER MEMBER G3N3 HOST '127.0.0.1' PORT 13350;
```

```
gSQL>
CREATE OR REPLACE FUNCTION u1.func5 ()
RETURN INTEGER
AS
BEGIN
    RETURN 0;
END;
/

ERR-23000(15006): MEMBER(G3N3): "ROUTINES_PRIMARY_KEY": dictionary integrity constraint violation by concurrent DDL execution
```

<a id="211d78df5dd56389"></a>
##### 수정 전 대처

없음

<a id="8ba538feffbc4371"></a>
#### <kbd>ISSUE-4215</kbd> EXECUTE IMMEDIATE의 using 절 변수가 IN OUT type이면 에러가 발생한다.

<a id="62d214b10641b8d8"></a>
##### 개요

EXECUTE IMMEDIATE의 using 절 변수의 bind type이 IN OUT type이면 에러가 발생한다.

<a id="a630edde9bcf34ec"></a>
##### 현상 및 증상

다음과 같이 에러가 발생한다.

```
CREATE OR REPLACE PROCEDURE proc_inout( p1 IN OUT INTEGER ) AS
  var1 INTEGER := 0;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'p1 : ' || p1 );

  var1 := p1;
  p1 := var1 + 10;
END;
/
COMMIT;

DECLARE
  var1 INTEGER;
BEGIN
  var1 := 30;

  EXECUTE IMMEDIATE 'BEGIN proc_inout( ? ); END;' USING IN OUT var1;

  DBMS_OUTPUT.PUT_LINE( 'var1 : ' || var1 );
END;
/


ERR-07006(16098): bind type mismatch of parameter number (1) : 
BEGIN proc_inout( ? ); END;
*
ERROR at line 1:
ERR-2F000(17041): execution fail : 
  EXECUTE IMMEDIATE 'BEGIN proc_inout( ? ); END;' USING IN OUT var1;
  *
ERROR at line 6:
```

<a id="7e28ac4cf3280b1c"></a>
##### 수정 전 대처

없음

<a id="77c33c40304b2540"></a>
### 21c.1.4 Patch Notes

<a id="21e57aaba4e2bd2c"></a>
#### <kbd>ISSUE-4207</kbd> Rowid를 이용하는 레코드를 조회하면 에러가 발생한다.

<a id="6add84e6a09bb773"></a>
##### 개요

4 GB 보다 큰 데이터 파일을 가지고 메모리 테이블스페이스를 사용할 때 시스템을 재시작한 후에 rowid를 이용하는 레코드를 조회하면 에러가 발생한다. 이는 시스템을 재시작할 때 전체 페이지 수를 잘못 계산하기 때문이므로 이 오류를 수정하였다.

<a id="14d635ac0228f83a"></a>
##### 현상 및 증상

다음과 같이 시스템을 재시작한 후에 rowid를 이용하는 레코드를 조회하면 에러가 발생한다.

```
CREATE TABLESPACE TEST_TBS DATAFILE 'test.dbf' SIZE 5G;

Tablespace created.

CREATE TABLE T1 ( C1 INTEGER, C2 VARCHAR(20) ) TABLESPACE TEST_TBS;

Table created.


INSERT INTO T1 VALUES ( 1, 'aa' );

1 row created.

COMMIT;

Commit complete.

SELECT ROWID, C1,C2 FROM T1;

                  ROWID C1 C2
----------------------- -- --
AAAAAAAAYe9AAGAAAAAiAAA  1 aa

1 row selected.

SELECT C1, C2 FROM T1 WHERE ROWID = 'AAAAAAAAYe9AAGAAAAAiAAA';

C1 C2
-- --
 1 aa

1 row selected.

// server restart

SELECT C1, C2 FROM T1 WHERE ROWID = 'AAAAAAAAYe9AAGAAAAAiAAA';

ERR-42000(14036): invalid ROWID
```

<a id="46c71542e4b58ea6"></a>
##### 수정 전 대처

없음

<a id="60b2f6243728f45e"></a>
### 21c.1.3 Patch Notes

<a id="19f23b7eafb481a2"></a>
#### <kbd>ISSUE-4189</kbd> Parameter가 ref cursor, DB type 순으로 되어 있는 procedure를 생성했을 때 이를 실행하면 에러가 발생한다.

<a id="249e66e8a8119727"></a>
##### 개요

Parameter가 ref cursor, DB type 순으로 되어 있는 procedure를 생성했을 때 이를 실행하면 에러가 발생한다.

<a id="d108f0726bb683d9"></a>
##### 현상 및 증상

다음과 같이 사용자가 procedure를 호출하면 에러가 발생한다.

```
CREATE OR REPLACE PROCEDURE p_test( p1 IN OUT SYS_REFCURSOR,
                                    p2 IN INTEGER ) AS
BEGIN
  IF p2 = 1 THEN
    OPEN p1 FOR SELECT * FROM t1;
  ELSIF p2 = 2 THEN
    OPEN p1 FOR SELECT * FROM t2;
  END IF;
END;
/

Procedure created.



DECLARE
  refcur1 SYS_REFCURSOR;
BEGIN
  p_test( refcur1 , 1 );
END;
/

ERR-2F000(17032): PSM compilation error : 
(1) at (4:21): ERR-2F000(17068): wrong number or types of arguments
```

<a id="f033f4f9e6f19dc6"></a>
##### 수정 전 대처

Procedure를 선언할 때 parameter를 정의하는 순서를 변경한다.

```
CREATE OR REPLACE PROCEDURE p_test( p2 IN INTEGER,
                                    p1 IN OUT SYS_REFCURSOR) AS
BEGIN
  IF p2 = 1 THEN
    OPEN p1 FOR SELECT * FROM t1;
  ELSIF p2 = 2 THEN
    OPEN p1 FOR SELECT * FROM t2;
  END IF;
END;
/

Procedure created.



DECLARE
  refcur1 SYS_REFCURSOR;
BEGIN
  p_test( 1, refcur1 );
END;
/

Anonymous PL block executed.
```

<a id="0c7e677b2c2da99b"></a>
#### <kbd>ISSUE-4188</kbd> Like 연산을 equal 비교 연산으로 변경 가능한 경우 변환을 지원한다.

<a id="0a7fd23fa1820f68"></a>
##### 개요

LIKE 연산의 pattern이 wildcard (%)나 underscore (_)가 사용되지 않은 literal 형태인 경우 equal 비교 연산으로의 변환을 지원한다.

<a id="68746e245601d213"></a>
##### 현상 및 증상

Equal 비교 연산과 동일한 의미를 갖는 LIKE 연산은 plan 최적화를 방해하는 요소이다. LIKE 연산을 equal 비교 연산으로 변경 가능한 경우 equal 비교 연산으로의 변환을 지원한다.

```
\EXPLAIN PLAN SELECT c_char LIKE 'a' FROM t1;

C_CHAR LIKE 'a'
---------------
TRUE           

1 row selected.

>>>  start print plan

< Execution Plan >
============================================================
|  IDX  |  NODE DESCRIPTION                        |  ROWS |
------------------------------------------------------------
|    0  |  SELECT STATEMENT                        |     1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")             |     1 |
|    2  |      TABLE ACCESS ("T1")                 |     1 |
============================================================

     1  -  TARGET : T1.C_CHAR = 'a'
     2  -  READ COLUMN : T1.C_CHAR

<<<  end print plan
```

<a id="e82faa6cb6d7cb7c"></a>
##### 수정 전 대처

LIKE 연산을 equal 비교 연산으로 변경하여 기술한다.

<a id="9e10643cfed081d1"></a>
#### <kbd>ISSUE-4190</kbd> Subquery가 inner join이나 semi join으로 unnesting 될 경우, left table로 push 가능한 filter는 push down 된다.

<a id="52e892eebe3fd73e"></a>
##### 개요

Subquery가 inner join이나 semi join으로 unnesting 될 경우, right table은 subquery가 되고 left table은 subquery의 outer table이 된다. 이 때, left table로 push 가능한 filter는 push down 된다.

<a id="6082db342129e493"></a>
##### 현상 및 증상

패치 전에는 subquery의 내부에 있던 r_c1 = 1이 left table r에 push down 되지 못한 채 join에 있다가 hash join으로 선택된 후에 hash instant의 filter에 연결되어 처리되고 있었다.

```
gSQL> \EXPLAIN PLAN
SELECT *
  FROM r
 WHERE EXISTS ( SELECT *
                  FROM s
                 WHERE r_c1 = s_c1 
                   AND r_c1 = 1
                   AND s_c2 = 1
              );

R_C1 R_C2
---- ----
   1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (SEMI)                                        |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        HASH JOIN INSTANT                                     |
|    5  |          TABLE ACCESS ("S")                                  |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2
     2  -  JOINED COLUMN : R.R_C1, R.R_C2
     3  -  READ COLUMN : R.R_C1, R.R_C2
     4  -  HASH KEY : S.S_C1
           READ KEY COLUMN : S.S_C1
             HASH FILTER : S.S_C1 = R.R_C1
             LOGICAL FILTER : {R.R_C1} = 1
     5  -  READ COLUMN : S.S_C1, S.S_C2
             PHYSICAL FILTER : S.S_C2 = 1

<<<  end print plan
```

패치하고 나면 r_c1 = 1이 해당 filter와 관련된 left table r에 위치한다.

```
\EXPLAIN PLAN
SELECT *
  FROM r
 WHERE EXISTS ( SELECT *
                  FROM s
                 WHERE r_c1 = s_c1 
                   AND r_c1 = 1
                   AND s_c2 = 1
              );

R_C1 R_C2
---- ----
   1    1

1 row selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      HASH JOIN (SEMI)                                        |
|    3  |        TABLE ACCESS ("R")                                    |
|    4  |        HASH JOIN INSTANT (UNIQUE)                            |
|    5  |          TABLE ACCESS ("S")                                  |
========================================================================

     1  -  TARGET : R.R_C1, R.R_C2
     2  -  JOINED COLUMN : R.R_C1, R.R_C2
     3  -  READ COLUMN : R.R_C1, R.R_C2
             PHYSICAL FILTER : R.R_C1 = 1
     4  -  HASH KEY : S.S_C1
           READ KEY COLUMN : S.S_C1
             HASH FILTER : S.S_C1 = R.R_C1
           FETCH ONE ROW
     5  -  READ COLUMN : S.S_C1, S.S_C2
             PHYSICAL FILTER : S.S_C2 = 1

<<<  end print plan
```

<a id="fcfb47f24da4c0c9"></a>
##### 수정 전 대처

없음

<a id="c6be7bde986ef185"></a>
### 21c.1.2 Patch Notes

<a id="4d133fa8a61d6759"></a>
#### <kbd>ISSUE-4183</kbd> Procedure의 actual parameter가 bind parameter인 경우 잘못된 정보가 설정된다.

<a id="4c1ca9fa1b5e3e88"></a>
##### 개요

Procedure의 actual parameter가 bind parameter인 경우 잘못된 정보가 설정되어 서버가 비정상적으로 종료된다.

<a id="4cdc4caf3f5bf9fd"></a>
##### 현상 및 증상

Procedure의 actual parameter가 bind parameter인 경우 잘못된 정보가 설정되어 서버가 비정상적으로 종료된다.

```
gSQL> CREATE OR REPLACE PROCEDURE proc1 ( p1 IN VARCHAR2,
                                          p2 IN VARCHAR2,
                                          p3 IN VARCHAR2,
                                          p4 IN VARCHAR2,
                                          p5 IN NUMBER,
                                          p6 IN VARCHAR2,
                                          p7 IN VARCHAR2,
                                          p8 OUT NUMBER ) AS
      BEGIN
        NULL;
      END;
      /
Procedure created.

\var a number

gSQL> BEGIN
        proc1( '20210728', '2' , '068C009581', '01', 0, 'DAILY', 'SYSTEM', :a );
      END;
      /


비정상 종료
```

<a id="ed449306e567a297"></a>
##### 수정 전 대처

없음

<a id="ef1af3580bb21054"></a>
#### <kbd>ISSUE-4178</kbd> DBMS_OUTPUT.PUT_LINE()을 두 번 출력한다.

<a id="ac28c811ebcfe33f"></a>
##### 개요

DBMS_OUTPUT.PUT_LINE()가 actual parameter인 DBMS_OUTPUT.PUT_LINE()을 포함하는 function을 호출하면 function 내용이 두 번 출력된다.

<a id="aaa7f4a1683c3308"></a>
##### 현상 및 증상

DBMS_OUTPUT.PUT_LINE을 수행할 때 actual parameter인 function이 두 번 수행되어 function 안에 있는 DBMS_OUTPUT.PUT_LINE()도 두 번 수행된다.

```
DECLARE
  FUNCTION sub( p1 INTEGER ) RETURN INTEGER AS
  BEGIN 
    DBMS_OUTPUT.PUT_LINE( 'p1 = ' || p1 );
    RETURN p1;
  END;
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'sub(x) = ' || sub(10) );
END;
/

p1 = 10
p1 = 10
sub(x) = 10
Anonymous PL block executed.
```

<a id="10f600158f07bb22"></a>
##### 수정 전 대처

없음

<a id="487002d5806d5f93"></a>
#### <kbd>ISSUE-4171</kbd> Bind parameter를 포함하여 CTE를 구성하면 시스템이 비정상적으로 종료된다.

<a id="311a54ada2cb88cb"></a>
##### 개요

Bind parameter를 포함하여 CTE를 구성한 후에 main query에서 해당 CTE를 사용하지 않으면 시스템이 비정상적으로 종료된다.

<a id="bbc09d5d394aaaa2"></a>
##### 현상 및 증상

사용하지 않은 CTE들에 포함된 bind parameter 정보들은 구성되지 않으므로 bind parameter 정보를 참조할 때 시스템이 비정상적으로 종료된다.

```
CREATE TABLE t1 ( c1 INTEGER );

VAR v1 VARCHAR(10)

--# fatal
WITH w1 AS ( SELECT * FROM t1 WHERE c1 = :v1 )
   , w2 AS ( SELECT * FROM t1 )
SELECT * FROM w2;
```

<a id="9b6feeb1eaef71de"></a>
##### 수정 전 대처

다음과 같이 사용하지 않는 CTE는 정의하지 않는다.

```
CREATE TABLE t1 ( c1 INTEGER );

VAR v1 VARCHAR(10)

WITH w2 AS ( SELECT * FROM t1 )
SELECT * FROM w2;
```

<a id="765e751beb8fc05e"></a>
#### <kbd>ISSUE-4174</kbd> Global sequence의 local cache가 고갈되었을 때의 성능을 개선하였다.

<a id="d8ea1302d6756f0e"></a>
##### 개요

Global sequence의 local cache가 고갈될 경우 성능이 급격하게 저하되는 문제가 있어 이를 수정하였다.

<a id="ca76de913145b4f5"></a>
##### 현상 및 증상

Sequence를 사용하는 모든 서버들은 local cache가 고갈될 경우 global cache로부터 local cache를 확보하기 위한 작업을 진행한다. 이 과정에서 원격 cserver를 경쟁적으로 확보하려 하기 때문에 성능이 급격하게 저하될 수 있다.

<a id="c9e7414e4909fffd"></a>
##### 수정 전 대처

없음

<a id="0956d790aa33d50e"></a>
#### <kbd>ISSUE-4182</kbd> Cyfile을 restart 할 때 recovery가 정상적으로 동작하지 않을 수 있다.

<a id="5e6a05c98d1e0fb4"></a>
##### 개요

여러 transaction이 동시에 수행되고 있는 도중에 cyfile을 stop 한 후 restart 하면 recovery가 정상적으로 동작하지 않는 문제가 있어 이를 수정하였다.

<a id="270bca713f0bbdf7"></a>
##### 현상 및 증상

여러 session에서 transaction을 수행하는 도중에 cyfile을 stop 한 후 restart 하면 이미 저장된 transaction이 다시 한 번 데이터 파일에 저장되어 문제가 발생한다.

<a id="875fac9221ccd842"></a>
##### 수정 전 대처

없음

<a id="4901a8793c0f9c15"></a>
### 21c.1.1 Patch Notes

<a id="f62825493e3ec0f1"></a>
#### <kbd>ISSUE-4157</kbd> PSM 내의 select into 구문에서 into와 into parameter의 간격에 따라 syntax error가 발생한다.

<a id="e94c81a8b1f7f391"></a>
##### 개요

PSM 내의 select into 구문에서 into와 into parameter의 간격이 두 칸 이상이면 syntax error가 발생한다.

<a id="b0b63cc3c6004a46"></a>
##### 현상 및 증상

다음과 같이 PSM 내의 select into 구문에서 into와 into parameter의 간격이 두 칸 이상이면 syntax error가 발생한다.

```
gSQL> CREATE OR REPLACE PROCEDURE proc1 AS
        v1 INTEGER;
      BEGIN 
        SELECT 0 x
          INTO  v1
          FROM dual;
      END;
      /

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-2F000(17100): PSM(PROC1) compilation error : 
(1) at (4:3): ERR-42000(16062): syntax error
Procedure created.
```

<a id="1795f93cdb4133fc"></a>
##### 수정 전 대처

다음과 같이 PSM 내의 select into 구문에서 into와 into parameter의 간격을 한 칸으로 만든다.

```
gSQL> CREATE OR REPLACE PROCEDURE proc1 AS
        v1 INTEGER;
      BEGIN 
        SELECT 0 x
          INTO v1
          FROM dual;
      END;
      /

Procedure created.
```

<a id="8b6bed49f9a6de0d"></a>
#### <kbd>ISSUE-4143</kbd> Hierarchy를 포함하는 query의 FROM 구문에서 테이블 참조 에러가 발생한다.

<a id="402db0976eb901dd"></a>
##### 개요

Hierarchy를 포함한 query의 FROM 구문에서 WITH 구문을 통해 정의된 테이블을 참조할 경우 에러가 발생한다.

<a id="14f07ab6b217b704"></a>
##### 현상 및 증상

Query의 FROM 절이 sub table로 구성되어 있고 sub table은 hierarchy를 포함하는 query로 구성된 경우, sub table 내에서 상위 query의 WITH 구문을 통해 정의된 Common Table Expression (CTE)을 참조하면 에러가 발생한다.

```
gSQL> with
w1 as (
        select * from dual
      ),
w2 as (
        select 1 from dual
      )
SELECT *
  FROM
       (
         SELECT * 
         FROM w1, w2
         CONNECT BY level < 0
       )
;
    2     3     4     5     6     7     8     9    10    11    12    13    14    15 
ERR-42000(16528): illegal reference of a query name in WITH clause : 
         FROM w1, w2
                  *
ERROR at line 12:
```

<a id="4b7829dd5c8a68df"></a>
##### 수정 전 대처

없음

<a id="eb4c2de1549e34cf"></a>
#### <kbd>ISSUE-4141</kbd> Hierarchy를 포함하는 query의 target 절에 relation_name.*를 명시할 경우 에러가 발생한다.

<a id="d144d98bd4b0ec3a"></a>
##### 개요

Hierarchy를 포함한 query의 target 절에 relation_name.*를 명시한 경우 에러가 발생한다.

<a id="1256ce209e37ae77"></a>
##### 현상 및 증상

Hierarchy를 포함한 query의 target 절에서 relation을 명시한 asterisk(rel.*) 대상을 찾으려 할 때 relation 이름에 해당하는 expression을 찾지 못하는 경우가 발생한다.

```
gSQL> SELECT t1.* FROM t1 CONNECT BY LEVEL < 0;

ERR-42000(16036): 'T1': invalid identifier : 
SELECT t1.* FROM t1 CONNECT BY LEVEL < 0
       *
ERROR at line 1:
```

<a id="b64a4d590fcd8f20"></a>
##### 수정 전 대처

없음

<a id="95aa064ac0409094"></a>
#### <kbd>ISSUE-4139</kbd> WITH 구문에서 현재 with element가 이전에 명시된 with element를 참조하고, 참조된 해당 with element가 materialize 방식으로 수행되었을 경우에 비정상 종료된다.

<a id="e145c40b4b9e1dce"></a>
##### 개요

WITH 구문에서 현재 with element가 이전에 명시된 with element를 참조하고, 참조된 해당 with element가 materialize 방식으로 수행되었을 경우에 비정상 종료된다.

<a id="fb44af3b890bc2f4"></a>
##### 현상 및 증상

w2에서 w1을 찾지 못해 잘못 처리되어 비정상 종료한다.

```
WITH
    w1 AS (  SELECT * FROM dual CONNECT BY level < 0  ),
    w2 AS (  SELECT 1 FROM w1 )
SELECT 1 FROM w2, w2;
```

<a id="462f257a618efa0a"></a>
##### 수정 전 대처

INLINE hint를 사용한다.

```
WITH
    w1 AS (  SELECT /*+ INLINE */ * FROM dual CONNECT BY level < 0  ),
    w2 AS (  SELECT 1 FROM w1 )
SELECT 1 FROM w2, w2;
```

---

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
