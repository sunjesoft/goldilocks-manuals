<a id="3e2aab7d9ea1ac35"></a>

# 4. What's New

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/3e2aab7d9ea1ac35)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<a id="36b30c810ddcba44"></a>
## Feature Matrix

본 장에서는 각 major version 별로 추가된 주요 기능들에 대해 간략히 설명한다.

<a id="6cebc205722b12f1"></a>
### Architecture

<a id="f538b29999f2cf21"></a>
#### System Architecture

System architecture에 대한 feature matrix는 다음과 같다.

**System architecture의 feature matrix**

<a id="a827679ffe7d3dba"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| Shared Nothing Cluster | X | X | O | O |
| DA (Direct Attach) | O | O | O | O |
| JDBC DA (Direct Attach) | X | X | O | O |
| C/S (Client/Server) Dedicated | X | O | O | O |
| C/S (Client/Server) Shared | X | O | O | O |
| multi-process applications | O | O | O | O |
| multi-threaded applications | O | O | O | O |
| Linux platform | O | O | O | O |
| HP platform | X | O | O | O |
| AIX platform | X | O | O | O |
| Windows Client Platform | X | O | O | O |
| CDC(Change Data Capture) replication | X | O | O | O |
| CDC replication with log mirror | X | O | O | O |
| multi-level start up | X | O | O | O |
| parallel database loading | O | O | O | O |
| parallel index build | X | O | O | O |
| SQL plan cache | X | O | O | O |

<a id="046e974c9fb983f6"></a>
#### Storage Internal

Storage internal에 대한 feature matrix는 다음과 같다.

**Storage internal의 feature matrix**

<a id="0b5fcac9cab1ae57"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| memory dictionary tablespace | O | O | O | O |
| memory data tablespace | O | O | O | O |
| memory undo tablespace | O | O | O | O |
| memory temporary tablespace | X | O | O | O |
| memory bitmap data segment | O | O | O | O |
| memory bitmap undo segment | O | O | O | O |
| memory bitmap instant segment | X | O | O | O |
| memory heap table | O | O | O | O |
| memory instant table | X | O | O | O |
| memory B-tree index | O | O | O | O |
| memory instant B-tree | X | O | O | O |
| memory instant hash | X | O | O | O |
| global secondary index | X | X | O | O |

<a id="a00f001d117a4d3a"></a>
#### Transaction Control

Transaction control에 대한 feature matrix는 다음과 같다.

**Transaction control의 feature matrix**

<a id="2c75a51d0191155b"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| CDS(Concurrency Data Store) database mode | O | O | O | O |
| TDS(Transactional Data Store) database mode | O | O | O | O |
| read-only database | X | O | O | O |
| read/write database | O | O | O | O |
| flat transaction | O | O | O | O |
| distributed transaction | X | O | O | O |
| read-only transaction | X | O | O | O |
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
| logging group | X | O | O | O |
| supplemental logging | X | O | O | O |
| mirrored logging | X | O | O | O |
| synchronous commit | O | O | O | O |
| asynchronous commit | O | O | O | O |
| grouped commit | O | O | O | O |
| total rollback | O | O | O | O |
| implicit statement rollback | O | O | O | O |
| savepoint management | X | O | O | O |

<a id="848a4435e26ea322"></a>
#### Backup & Recovery

Backup & recovery에 대한 feature matrix는 다음과 같다.

**Backup & recovery의 feature matrix**

<a id="d794a09406b1a626"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| off-line backup | O | O | O | O |
| on-line backup | X | O | O | O |
| full backup | X | O | O | O |
| incremental backup | X | O | O | O |
| complete recovery | O | O | O | O |
| incomplete recovery | X | O | O | O |
| auto instance recovery | O | O | O | O |
| tablespace recovery | X | O | O | O |
| file recovery | X | O | O | O |

<a id="351d5f0e7724f6bd"></a>
#### Database Information

<a id="5f17009a29d9bc20"></a>
##### DICTIONARY_SCHEMA 스키마

DICTIONARY_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

<a id="1e41148a7d31dfdf"></a>
<table class="table column_count_6"><caption>DICTIONARY_SCHEMA schema의 feature matrix</caption><thead><tr><th class="to_center"><div>계열</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="53"><div>ALL_ 계열 view</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="46"><div>DBA_ 계열 view</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="49"><div>USER_ 계열 view</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="14"><div>기타 view</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="a03f43e959f47cdc"></a>
##### INFORMATION_SCHEMA 스키마

INFORMATION_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**INFORMATION_SCHEMA schema의 feature matrix**

<a id="9d5953ae63607573"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| COLUMNS | X | O | O | O |
| COLUMN_PRIVILEGES | X | O | O | O |
| CONSTRAINT_COLUMN_USAGE | X | O | O | O |
| CONSTRAINT_TABLE_USAGE | X | O | O | O |
| INFORMATION_SCHEMA_CATALOG_NAME | X | O | O | O |
| KEY_COLUMN_USAGE | X | O | O | O |
| PARAMETERS | X | X | O | O |
| REFERENTIAL_CONSTRAINTS | X | O | O | O |
| ROUTINES | X | X | O | O |
| ROUTINE_PRIVILEGES | X | X | O | O |
| ROUTINE_ROUTINE_USAGE | X | X | O | O |
| ROUTINE_SEQUENCE_USAGE | X | X | O | O |
| ROUTINE_TABLE_USAGE | X | X | O | O |
| SCHEMATA | X | O | O | O |
| SEQUENCES | X | O | O | O |
| SQL_FEATURES | X | O | O | O |
| SQL_IMPLEMENTATION_INFO | X | O | O | O |
| SQL_PACKAGES | X | O | O | O |
| SQL_PARTS | X | O | O | O |
| SQL_SIZING | X | O | O | O |
| STATISTICS | X | O | O | O |
| TABLES | X | O | O | O |
| TABLE_CONSTRAINTS | X | O | O | O |
| TABLE_PRIVILEGES | X | O | O | O |
| USAGE_PRIVILEGES | X | O | O | O |
| VIEWS | X | O | O | O |
| VIEW_ROUTINE_USAGE | X | X | O | O |
| VIEW_TABLE_USAGE | X | O | O | O |

<a id="f97dce0dc7d1e2eb"></a>
##### PERFORMANCE_VIEW_SCHEMA 스키마

PERFORMANCE_VIEW_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**PERFORMANCE_VIEW_SCHEMA schema의 feature matrix**

<a id="c34989fc0fe394c6"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| GV$____ | X | X | O | O |
| V$AGABLE_INFO | X | X | O | O |
| V$ARCHIVELOG | X | O | O | O |
| V$AUDITABLE_DB_PRIVILEGES | X | X | X | O |
| V$AUDITABLE_SYSTEM_ACTIONS | X | X | X | O |
| V$BACKUP | X | O | O | O |
| V$BALANCER | X | O | O | O |
| V$CLUSTER_DISPATCHER | X | X | O | O |
| V$CLUSTER_LOCATION | X | X | O | O |
| V$CLUSTER_MEMBER | X | X | O | O |
| V$COLUMNS | X | O | O | O |
| V$CONTROLFILE | X | O | O | O |
| V$DATAFILE | X | O | O | O |
| V$DB_FILE | X | O | O | O |
| V$DISPATCHER | X | O | O | O |
| V$ERROR_CODE | X | O | O | O |
| V$GLOBAL_TRANSACTION | X | O | O | O |
| V$JOURNALING | X | X | O | O |
| V$INCREMENTAL_BACKUP | X | O | O | O |
| V$INSTANCE | X | O | O | O |
| V$KEYWORDS | X | O | O | O |
| V$LATCH | X | O | O | O |
| V$LOCK_WAIT | X | O | O | O |
| V$LOGFILE | X | O | O | O |
| V$PROCESS_MEM_STAT | X | O | O | O |
| V$PROCESS_SQL_STAT | X | O | O | O |
| V$PROCESS_STAT | X | O | O | O |
| V$PROPERTY | X | O | O | O |
| V$PSM_RESERVED_WORDS | X | X | O | O |
| V$QUEUE | X | O | O | O |
| V$RESERVED_WORDS | X | O | O | O |
| V$SESSION | X | O | O | O |
| V$SESSION_AUDIT | X | X | X | O |
| V$SESSION_CONNECT_INFO | X | O | O | O |
| V$SESSION_EVENT | X | X | O | O |
| V$SESSION_MEM_STAT | X | O | O | O |
| V$SESSION_SQL_STAT | X | O | O | O |
| V$SESSION_STAT | X | O | O | O |
| V$SESSION_WAIT | X | X | O | O |
| V$SHARED_MODE | X | O | O | O |
| V$SHARED_SERVER | X | O | O | O |
| V$SHM_SEGMENT | X | O | O | O |
| V$SPROPERTY | X | O | O | O |
| V$SQLFN_METADATA | X | O | O | O |
| V$SQL_CACHE | X | O | O | O |
| V$SQL_COMMAND | X | X | O | O |
| V$SQL_HISTORY | X | X | O | O |
| V$STATEMENT | X | O | O | O |
| V$SYSTEM_EVENT | X | X | O | O |
| V$SYSTEM_MEM_STAT | X | O | O | O |
| V$SYSTEM_SQL_STAT | X | O | O | O |
| V$SYSTEM_STAT | X | O | O | O |
| V$TABLES | X | O | O | O |
| V$TABLESPACE | X | O | O | O |
| V$TABLESPACE_STAT | X | X | O | O |
| V$TRANSACTION | X | O | O | O |
| V$WAIT_EVENT_CLASS_NAME | X | X | O | O |
| V$WAIT_EVENT_NAME | X | X | O | O |
| V$XA_TRANSATION | X | X | O | O |

<a id="23b8a86809847e08"></a>
#### Server Property

Server Property에 대한 feature matrix는 다음과 같다.

**Server property의 feature matrix**

<a id="eb76101bf6f637b9"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| AGING_INTERVAL | O | O | O | O |
| AGING_PLAN_INTERVAL | X | O | O | O |
| ARCHIVELOG_DIR | O | O | X | X |
| ARCHIVELOG_DIR_1 ~ DIR_10 | X | O | O | O |
| ARCHIVELOG_FILE | X | O | O | O |
| ARCHIVELOG_MODE | X | O | O | O |
| BACKUP_DIR_1 ~ DIR_10 | X | O | O | O |
| BLOCK_READ_COUNT | O | O | O | O |
| BULK_IO_PAGE_COUNT | X | O | O | O |
| CDISPATCHER_HOT_POLICY_INTERVAL | X | X | O | O |
| CDISPATCHER_SOCKET_BUFFER_SIZE | X | X | O | O |
| CDISPATCHER_THREADS | X | X | O | O |
| CHAR_LENGTH_UNITS | X | O | O | O |
| CHARACTER_SET | X | O | O | O |
| CHECK_DEDICATE_CONNECTION_INTERVAL | X | X | O | O |
| CHECK_DEDICATE_SOCKET | X | X | O | X |
| CLIENT_MAX_COUNT | O | O | O | O |
| CLIENT_NUMA_POLICY | X | X | O | O |
| CLOSE_PSM_CHILD_STMTS | X | X | O | O |
| CLUSTER_ASYNC_COMMIT | X | X | O | O |
| CLUSTER_ASYNC_REPLICATION | X | X | O | O |
| CLUSTER_CM_BUFFER_COUNT | X | X | O | O |
| CLUSTER_CM_BUFFER_SIZE | X | X | O | O |
| CLUSTER_CM_READ_BUFFER_SIZE | X | X | O | O |
| CLUSTER_COMMIT_SLAVES | X | X | O | O |
| CLUSTER_COMMIT_STREAM_ISOLATION | X | X | O | O |
| CLUSTER_CONNECTION | X | X | O | O |
| CLUSTER_CONNECTION_TIMEOUT_SEC | X | X | O | O |
| CLUSTER_DATA_SYNC_SERVERS | X | X | O | O |
| CLUSTER_DISPATCHER_IN_QUEUE_SIZE | X | X | O | O |
| CLUSTER_DISPATCHER_NUMA_STREAM_MAP | X | X | O | O |
| CLUSTER_DISPATCHER_OUT_QUEUE_SIZE | X | X | O | O |
| CLUSTER_HEARTBEAT_INTERVAL | X | X | O | O |
| CLUSTER_HEARTBEAT_RETRY_COUNT | X | X | O | O |
| CLUSTER_IGNORE_INACTIVE_MEMBER | X | X | O | O |
| CLUSTER_MAX_PACKET_SIZE | X | X | O | O |
| CLUSTER_MAX_PAYLOAD_SIZE | X | X | O | O |
| CLUSTER_PACKET_ALLOCATION_TIMEOUT | X | X | O | O |
| CLUSTER_SERVER_RESPONSE_QUEUE_SIZE | X | X | O | O |
| CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY | X | X | O | O |
| CLUSTER_SPLIT_BRAIN_RETRY_COUNT | X | X | O | O |
| COMMITTER_HOT_POLICY_INTERVAL | X | X | O | O |
| CONTROL_FILE_0 ~ FILE_7 | X | O | O | O |
| CONTROL_FILE_COUNT | X | O | O | O |
| CONTROL_FILE_TEMP_NAME | X | O | O | O |
| COORDINATOR_COMMIT_WRITE_MODE | X | X | O | O |
| CSERVERS | X | X | O | O |
| DA_CLIENT_NUMA_MODE | X | X | O | O |
| DATA_STORE_MODE | O | O | O | O |
| DATABASE_ACCESS_MODE | X | O | O | O |
| DATABASE_INSTANCE_NAME | X | X | O | O |
| DDL_AUTOCOMMIT | X | O | O | O |
| DDL_LOCK_TIMEOUT | O | O | O | O |
| DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION | X | X | O | O |
| DEFAULT_INDEX_LOGGING | X | O | O | O |
| DEFAULT_INDEX_PCTFREE | X | X | O | O |
| DEFAULT_INITRANS | O | O | O | O |
| DEFAULT_MAXTRANS | O | O | O | O |
| DEFAULT_PCTFREE | O | O | O | O |
| DEFAULT_PCTUSED | O | O | O | O |
| DEFAULT_REMOVAL_BACKUP_FILE | X | O | O | O |
| DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST | X | O | O | O |
| DEFAULT_SHARDING | X | X | O | O |
| DISABLE_DDL_CDC_GIVEUP | X | O | O | O |
| DISABLE_UPDATE_PK_CDC_GIVEUP | X | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE | X | X | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL | X | X | X | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME | X | X | O | O |
| DISPATCHERS | X | O | O | O |
| DISPATCHER_CM_BUFFER_SIZE | X | O | O | O |
| DISPATCHER_CM_UNIT_SIZE | X | O | O | O |
| DISPATCHER_CONNECTIONS | X | O | O | O |
| DISPATCHER_HOT_POLICY_INTERVAL | X | X | O | O |
| DISPATCHER_LOAD_BALANCING | X | X | O | O |
| DISPATCHER_NUMA_STREAM_MAP | X | X | O | O |
| DISPATCHER_QUEUE_SIZE | X | O | O | O |
| DISPATCHER_REQUEST_MINI_QUEUE_COUNT | X | X | O | O |
| DISPATCHER_RESPONSE_MINI_QUEUE_COUNT | X | X | O | O |
| FETCH_FAILOVER | X | X | O | O |
| GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY | X | X | X | O |
| GLOBAL_JOURNAL_BUFFER_SIZE | X | X | O | O |
| GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE | X | X | O | O |
| GLOBAL_PROPERTY_LOCK_TIMEOUT | X | X | O | O |
| GLOBAL_TRANSACTION_COMMIT_WRITE_MODE | X | X | O | O |
| GLOBAL_TRANSACTION_ISOLATION_SCOPE | X | X | O | O |
| GLOBAL_TRANSACTION_LOG_DIR | X | X | O | O |
| GLOBAL_TRANSACTION_LOG_FILE_SIZE | X | X | O | O |
| GMASTER_NUMA_NODE | X | X | O | O |
| GMON_AUTOSTART | X | X | O | O |
| HINT_ERROR | X | O | O | O |
| IDLE_TIMEOUT | O | O | O | O |
| IN_DOUBT_DECISION | X | O | O | O |
| INDEX_BUILD_PARALLEL_FACTOR | X | O | O | O |
| INDEX_TREE_MERGE_PARALLEL_FACTOR | X | X | O | O |
| INST_ALLOCATOR_COUNT | X | X | O | O |
| INST_TABLE_BLOCK_SIZE | X | X | O | O |
| JOURNAL_TEMP_DIR | X | X | O | O |
| KEEPALIVE_IDLE_TIME | X | O | O | O |
| LOCAL_CLUSTER_MEMBER | X | X | O | O |
| LOCAL_CLUSTER_MEMBER_HOST | X | X | O | O |
| LOCAL_CLUSTER_MEMBER_PORT | X | X | O | O |
| LOCAL_JOURNAL_BUFFER_SIZE | X | X | O | O |
| LOCATION_FILE | X | X | O | O |
| LOCATOR_QUERY_TIMEOUT | X | X | O | O |
| LOCK_HASH_TABLE_SIZE | X | O | O | O |
| LOG_BLOCK_SIZE | O | O | O | O |
| LOG_BUFFER_SIZE | O | O | O | O |
| LOG_DIR | O | O | O | O |
| LOG_FILE_SIZE | O | O | O | O |
| LOG_GROUP_COUNT | O | O | O | O |
| LOG_MIRROR_MODE | X | O | O | O |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | X | O | O | O |
| LOG_MIRROR_TIMEOUT | X | O | O | O |
| LOG_SYNC_INTERVAL | X | O | O | O |
| LOG_SYNC_INTERVAL_MSEC | X | X | O | O |
| MAX_GROUP_COUNT | X | X | O | O |
| MAX_JOURNAL_FILE_SIZE | X | X | O | O |
| MAX_NODE_COUNT | X | X | O | O |
| MAXIMUM_CONCURRENT_ACTIVITIES | X | O | O | O |
| MAXIMUM_FLANGE_COUNT | X | X | O | O |
| MAXIMUM_FLUSH_LOG_BLOCK_COUNT | O | O | O | O |
| MAXIMUM_FLUSH_PAGE_COUNT | O | O | O | O |
| MAXIMUM_JOURNAL_REPLAY_COUNT | X | X | X | O |
| MAXIMUM_NAMED_CURSOR_COUNT | X | O | O | O |
| MAXIMUM_SESSION_CM_BUFFER_SIZE | X | O | O | O |
| MEASURE_CLUSTER_LATENCY | X | X | O | O |
| MEDIA_RECOVERY_LOG_BUFFER_SIZE | X | O | X | X |
| MEMORY_MERGE_RUN_COUNT | X | O | O | O |
| MEMORY_SORT_RUN_SIZE | X | O | O | O |
| MIN_SAMPLE_ROW_COUNT | X | X | O | O |
| MINIMUM_UNDO_PAGE_COUNT | O | O | O | O |
| NET_BUFFER_SIZE | X | O | O | O |
| NLS_DATE_FORMAT | X | O | O | O |
| NLS_TIME_FORMAT | X | O | O | O |
| NLS_TIME_WITH_TIME_ZONE_FORMAT | X | O | O | O |
| NLS_TIMESTAMP_FORMAT | X | O | O | O |
| NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT | X | O | O | O |
| NUMA | X | X | O | O |
| NUMA_MAP | X | X | O | O |
| OFFLINE_MEMBER_AFTER_FAILOVER | X | X | O | O |
| ONLINE_JOURNAL_REPLAY_THRESHOLD | X | X | X | O |
| OS_GROUP_ACCESS | X | X | O | O |
| PACKET_COMPRESSION_THRESHOLD | X | X | X | O |
| PAGE_CHECKSUM_TYPE | X | O | O | O |
| PARALLEL_IO_FACTOR | O | O | O | O |
| PARALLEL_IO_GROUP_1 ~ GROUP_16 | O | O | O | O |
| PARALLEL_LOAD_FACTOR | O | O | O | O |
| PENDING_LOG_BUFFER_COUNT | O | O | O | O |
| PLAN_CACHE | X | O | O | O |
| PLAN_CACHE_SIZE | X | O | O | O |
| PRIVATE_STATIC_AREA_SIZE | X | O | O | O |
| PROCESS_MAX_COUNT | O | O | O | O |
| QUERY_TIMEOUT | O | O | O | O |
| READABLE_ARCHIVELOG_DIR_COUNT | X | O | O | O |
| READABLE_BACKUP_DIR_COUNT | X | O | O | O |
| REBALANCE_BLOCK_READ_COUNT | X | X | O | O |
| RECOMPILE_CHECK_MINIMUM_PAGE_COUNT | X | O | O | X |
| RECOMPILE_PAGE_PERCENT | X | O | O | X |
| RECOVERY_LOG_BUFFER_SIZE | X | X | O | O |
| REDO_LOG_COMPRESSION_THRESHOLD | X | X | X | O |
| REFINE_RELATION | X | O | O | O |
| SESSION_FATAL_BEHAVIOR | X | O | O | O |
| SESSION_MEMORY_INIT_SIZE | X | X | X | O |
| SESSION_MEMORY_SHRINK_THRESHOLD | X | X | X | O |
| SHARED_MEMORY_ADDRESS | O | O | O | O |
| SHARED_MEMORY_STATIC_KEY | O | O | O | O |
| SHARED_MEMORY_STATIC_NAME | O | O | O | O |
| SHARED_MEMORY_STATIC_SIZE | O | O | O | O |
| SHARED_REQUEST_QUEUE_COUNT | X | O | O | O |
| SHARED_SERVERS | X | O | O | O |
| SHARED_SESSION | X | O | O | O |
| SNAPSHOT_STATEMENT_TIMEOUT | X | O | O | O |
| SQL_HISTORY_SIZE | X | X | O | O |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | X | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O |
| SYSTEM_MEMORY_AUX_TABLESPACE_SIZE | X | X | X | O |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | O | O | O | O |
| SYSTEM_TABLESPACE_DIR | O | O | O | O |
| SYSTEM_UDS_DIR | X | X | O | O |
| TCP_NODELAY | X | X | O | O |
| TEMP_SEGMENT_CACHE_SIZE | X | X | X | O |
| TEMP_UNDO_ENABLED | X | X | X | O |
| TIMED_STATISTICS | X | X | O | O |
| TIMER_INTERVAL | O | O | X | X |
| TIMEZONE | X | O | O | O |
| TRACE_ALTER_SYSTEM | X | O | O | O |
| TRACE_DDL | O | O | O | O |
| TRACE_LOG_ID | X | O | O | O |
| TRACE_LOG_MSGBUG_SIZE | X | X | O | O |
| TRACE_LOG_TIME_DETAIL | X | O | O | O |
| TRACE_LOGGER | X | X | O | O |
| TRACE_LOGGER_REMOTE_HOST | X | X | O | O |
| TRACE_LOGGER_REMOTE_PORT | X | X | O | O |
| TRACE_LOGIN | X | O | O | O |
| TRACE_LONG_RUN_CURSOR | X | O | O | O |
| TRACE_LONG_RUN_SQL | X | O | O | O |
| TRACE_XA | X | O | O | O |
| TRANSACTION_ALLOCATION_TIMEOUT | X | X | X | O |
| TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O |
| TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT | X | O | O | O |
| TRANSACTION_TABLE_SIZE | O | O | O | O |
| TRANSACTION_TIMEOUT | X | X | O | O |
| UNDO_RELATION_ALLOCATION_TIMEOUT | X | X | X | O |
| UNDO_RELATION_COUNT | O | O | O | O |
| UNDO_SHRINK_THRESHOLD | X | O | O | O |
| USE_LARGE_PAGES | X | X | X | O |

<a id="960f9421c6c0dad7"></a>
### SQL

<a id="a619dd78b9e747dc"></a>
#### SQL Element

<a id="ddcd73e1b43c7889"></a>
##### Data Type

데이터 타입에 대한 feature matrix는 다음과 같다.

<a id="23955c1439d9f780"></a>
<table class="table column_count_6"><caption>Data type의 feature matrix</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>문자 스트링 타입</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>이진 스트링 타입</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>십진 숫자 타입</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>이진 숫자 타입</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN 타입</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>날짜/시간 타입</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL 타입</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROWID 타입</div></td><td><div>ROWID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="ad583b5b678af030"></a>
##### Function

함수 및 연산자에 대한 feature matrix는 다음과 같다.

**Function의 feature matrix**

<a id="c99d78cbc87f4f86"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| expr1 * expr2 | O | O | O | O |
| expr1 + expr2 | O | O | O | O |
| datetime + interval | X | O | O | O |
| ＋ expr | O | O | O | O |
| expr1 - expr2 | O | O | O | O |
| datetime - interval | X | O | O | O |
| - expr | O | O | O | O |
| expr1 / expr2 | O | O | O | O |
| str1 \|\| str2 | O | O | O | O |
| expr &lt;comp&gt; expr | O | O | O | O |
| expr &lt;comp&gt; ( subquery ) | X | O | O | O |
| ( subquery ) &lt;comp&gt; expr | X | O | O | O |
| ( subquery ) &lt;comp&gt; ( subquery ) | X | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( expr, ... ) | X | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( subquery ) | X | O | O | O |
| ( subquery ) &lt;comp&gt; ( expr, ... ) | X | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | X | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | X | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | X | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | X | O | O | O |
| ABS( num ) | O | O | O | O |
| ACOS( num ) | O | O | O | O |
| ADDDATE( date, interval ) | X | O | O | O |
| ADDDATE( expr, days ) | X | O | O | O |
| ADDTIME( expr1, expr2 ) | X | O | O | O |
| ADD_MONTHS( date, number ) | X | O | O | O |
| AND | O | O | O | O |
| ASCII( char ) | X | X | O | O |
| ASIN( num ) | O | O | O | O |
| ATAN( num ) | O | O | O | O |
| ATAN2( num1, num2 ) | O | O | O | O |
| AVG( num ) | X | O | O | O |
| expr1 [NOT] BETWEEN [ASYMMETRIC\|SYMMETRIC] expr2 AND expr3 | X | O | O | O |
| BITAND( num1, num2 ) | O | O | O | O |
| BITNOT( num ) | O | O | O | O |
| BITOR( num1, num2 ) | O | O | O | O |
| BITXOR( num1, num2 ) | O | O | O | O |
| BIT_LENGTH( str ) | O | O | O | O |
| BYTE_LENGTH( str ) | O | O | O | O |
| CASE .. WHEN .. THEN .. ELSE .. END | X | O | O | O |
| CASE2( condition, result, ... ) | X | O | O | O |
| CAST( expr AS datatype ) | O | O | O | O |
| CBRT( num ) | O | O | O | O |
| CEIL( num ) | O | O | O | O |
| CEILING( num ) | O | O | O | O |
| CHAR_LENGTH( str ) | O | O | O | O |
| CHARACTER_LENGTH( str ) | O | O | O | O |
| CHR( num ) | X | X | O | O |
| CLOCK_DATE() | O | O | O | O |
| CLOCK_LOCALTIME() | O | O | O | O |
| CLOCK_LOCALTIMESTAMP() | O | O | O | O |
| CLOCK_TIME() | O | O | O | O |
| CLOCK_TIMESTAMP() | O | O | O | O |
| COALESCE( expr1, ..., exprN ) | X | O | O | O |
| CONCAT( str1, str2 ) | O | O | O | O |
| CONCATENATE( str1, str2 ) | O | O | O | O |
| COS( num ) | O | O | O | O |
| COT( num ) | O | O | O | O |
| COUNT( expr ) | X | O | O | O |
| COUNT(*) | X | O | O | O |
| CURRENT_CATALOG | O | O | O | O |
| CURRENT_DATE | O | O | O | O |
| CURRENT_SCHEMA | O | O | O | O |
| CURRENT_TIME | O | O | O | O |
| CURRENT_TIMESTAMP | O | O | O | O |
| CURRENT_USER | O | O | O | O |
| seq.CURRVAL | O | O | O | O |
| CURRVAL( seq ) | O | O | O | O |
| DATEADD( datepart, number, date ) | O | O | O | O |
| DATEDIFF( datepart, startdate, enddate ) | X | O | O | O |
| DATE_ADD( date, interval ) | X | O | O | O |
| DATE_PART( field, datetime ) | X | O | O | O |
| DECODE( expr, comparison, result, ... ) | X | O | O | O |
| DEGREES( radians ) | O | O | O | O |
| DIGEST ( data, type ) | X | X | O | O |
| DUMP( expr ) | X | O | O | O |
| EXISTS( subquery ) | X | O | O | O |
| EXP( num ) | O | O | O | O |
| EXTRACT( field FROM datetime ) | X | O | O | O |
| FACTORIAL( num ) | O | O | O | O |
| FLOOR( num ) | O | O | O | O |
| FROM_BASE64( str ) | X | X | O | O |
| GREATEST( expr, ... ) | X | O | O | O |
| HEX( str ) | X | X | O | O |
| expr1 [NOT] IN ( expr, ... ) | X | O | O | O |
| expr1 [NOT] IN ( subquery ) | X | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt; ) | X | O | O | O |
| subquery [NOT] IN ( subquery ) | X | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( &lt;expr_list&gt;, ... ) | X | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( subquery ) | X | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt;, ... ) | X | O | O | O |
| INITCAP( str ) | X | O | O | O |
| INSTR( str, substr, ... ) | X | O | O | O |
| IS NOT NULL | O | O | O | O |
| IS NULL | O | O | O | O |
| LAST_DAY( date ) | X | O | O | O |
| LAST_IDENTITY_VALUE() | X | X | O | O |
| LEAST( expr, ... ) | X | O | O | O |
| LENGTH( str ) | O | O | O | O |
| LENGTHB( str ) | O | O | O | O |
| string [NOT] LIKE pattern ESCAPE escape_char | X | O | O | O |
| LN( num ) | O | O | O | O |
| LOCALTIME | O | O | O | O |
| LOCALTIMESTAMP | O | O | O | O |
| LOCAL_GROUP_ID() | X | X | O | O |
| LOCAL_GROUP_NAME() | X | X | O | O |
| LOCAL_MEMBER_ID() | X | X | O | O |
| LOCAL_MEMBER_NAME() | X | X | O | O |
| LOG( num2 ) | O | O | O | O |
| LOG( num1, num2 ) | O | O | O | O |
| LOGON_USER() | X | O | O | O |
| LOWER( str ) | O | O | O | O |
| LPAD( str, length, fill ) | X | O | O | O |
| LTRIM( str, [ str ] ) | X | O | O | O |
| MAX( expr ) | X | O | O | O |
| MIN( expr ) | X | O | O | O |
| MOD( num1, num2 ) | O | O | O | O |
| MONTHS_BETWEEN( date1, date2 ) | X | X | X | O |
| NEXT_DAY( date, day ) | X | X | O | O |
| seq.NEXTVAL | O | O | O | O |
| NEXTVAL( seq ) | O | O | O | O |
| NEXT VALUE FOR seq | O | O | O | O |
| NOT | X | O | O | O |
| NULLIF( expr1, expr2 ) | X | O | O | O |
| NVL( expr1, expr2 ) | X | O | O | O |
| NVL2( expr1, expr2, expr3 ) | X | O | O | O |
| OCTET_LENGTH( str ) | O | O | O | O |
| OVERLAY( str1 PLACING str2 FROM start FOR length ) | X | O | O | O |
| OR | X | O | O | O |
| PI() | O | O | O | O |
| POSITION( str1 IN str2 ) | O | O | O | O |
| POWER( num1, num2 ) | O | O | O | O |
| RADIANS( degrees ) | O | O | O | O |
| RANDOM( min, max ) | O | O | O | O |
| REPEAT( str, num ) | X | O | O | O |
| REPLACE( str, from, to ) | X | O | O | O |
| REVERSE( str ) | X | X | X | O |
| ROUND( num ) | X | O | O | O |
| ROUND( date, fmt ) | X | O | O | O |
| ROWID_GRID_BLOCK_ID( rowid ) | X | X | O | O |
| ROWID_GRID_BLOCK_SEQ( rowid ) | X | X | O | O |
| ROWID_MEMBER_ID( rowid ) | X | X | O | O |
| ROWID_OBJECT_ID( rowid ) | X | O | O | O |
| ROWID_PAGE_ID( rowid ) | X | O | O | O |
| ROWID_ROW_NUMBER( rowid ) | X | O | O | O |
| ROWID_SHARD_ID( rowid ) | X | X | O | O |
| ROWID_TABLESPACE_ID( rowid ) | X | O | O | O |
| ROWNUM | X | X | O | O |
| RPAD( str, length, fill ) | X | O | O | O |
| RTRIM( str, [ str ] ) | X | O | O | O |
| SESSION_ID() | X | O | O | O |
| SESSION_SERIAL() | X | O | O | O |
| SESSION_USER | X | O | O | O |
| SHARD_GROUP_ID( table, expr ) | X | X | O | O |
| SHARD_GROUP_NAME( table_name, shard_key_value [, ...] ) | X | X | O | O |
| SHARD_ID( table, expr ) | X | X | O | O |
| SHARD_NAME( table_name, shard_key_value [, ...] ) | X | X | O | O |
| SHIFT_LEFT( num, cnt ) | O | O | O | O |
| SHIFT_RIGHT( num, cnt ) | O | O | O | O |
| SIGN( num ) | O | O | O | O |
| SIN( num ) | O | O | O | O |
| SPLIT_PART( str, delimiter, field ) | X | O | O | O |
| SQRT( num ) | O | O | O | O |
| STATEMENT_DATE() | O | O | O | O |
| STATEMENT_LOCALTIME() | O | O | O | O |
| STATEMENT_LOCALTIMESTAMP() | O | O | O | O |
| STATEMENT_TIME() | O | O | O | O |
| STATEMENT_TIMESTAMP() | O | O | O | O |
| STATEMENT_VIEW_SCN() | X | O | O | O |
| STATEMENT_VIEW_SCN_DCN() | X | X | O | O |
| STATEMENT_VIEW_SCN_GCN() | X | X | O | O |
| STATEMENT_VIEW_SCN_LCN() | X | X | O | O |
| STDDEV( [ ALL \| DISTINCT ] expr ) | X | X | X | O |
| STDDEV_POP( expr ) | X | X | X | O |
| STDDEV_SAMP( expr ) | X | X | X | O |
| SUBSTR( str FROM start FOR length ) | X | O | O | O |
| SUBSTR( str, start, length ) | X | O | O | O |
| SUBSTRB( str, start, length ) | X | O | O | O |
| SUBSTRING( str FROM start FOR length ) | X | O | O | O |
| SUBSTRING( str, start, length ) | X | O | O | O |
| SUM( expr ) | X | O | O | O |
| SYSDATE | O | O | O | O |
| SYS_EXTRACT_UTC( datetime_with_timezone ) | X | X | O | O |
| SYSTIME | O | O | O | O |
| SYSTIMESTAMP | O | O | O | O |
| TAN( num ) | O | O | O | O |
| TO_CHAR( datetime, fmt ) | X | O | O | O |
| TO_CHAR( number, fmt ) | X | O | O | O |
| TO_BASE64( str ) | X | X | O | O |
| TO_DATE( str, fmt ) | X | O | O | O |
| TO_NATIVE_DOUBLE( str, fmt ) | X | O | O | O |
| TO_NATIVE_REAL( str, fmt ) | X | O | O | O |
| TO_NUMBER( num, fmt ) | X | O | O | O |
| TO_TIME( str, fmt ) | X | O | O | O |
| TO_TIME_TZ( str, fmt ) | X | O | O | O |
| TO_TIME_WITH_TIME_ZONE( str, fmt ) | X | O | O | O |
| TO_TIMESTAMP( str, fmt ) | X | O | O | O |
| TO_TIMESTAMP_TZ( str, fmt ) | X | O | O | O |
| TO_TIMESTAMP_WITH_TIME_ZONE( str, fmt ) | X | O | O | O |
| TRANSACTION_DATE() | O | O | O | O |
| TRANSACTION_LOCALTIME() | O | O | O | O |
| TRANSACTION_LOCALTIMESTAMP() | O | O | O | O |
| TRANSACTION_TIME() | O | O | O | O |
| TRANSACTION_TIMESTAMP() | O | O | O | O |
| TRANSLATE( str, from, to ) | X | O | O | O |
| TRIM( LEADING\|TRAILING\|BOTH trim_char FROM source ) | O | O | O | O |
| TRUNC( num, scale ) | X | O | O | O |
| TRUNC( date, fmt ) | X | O | O | O |
| UPPER( str ) | O | O | O | O |
| UNHEX( str ) | X | X | O | O |
| UNHEX_TO_CHARSTR( str ) | X | X | O | O |
| USER_ID() | O | O | O | O |
| UUID() | X | X | O | O |
| VAR_POP( expr ) | X | X | X | O |
| VAR_SAMP( expr ) | X | X | X | O |
| VARIANCE( [ ALL \| DISTINCT ] expr ) | X | X | X | O |
| VERSION() | O | O | O | O |
| WIDTH_BUCKET( num, min, max, cnt ) | O | O | O | O |

<a id="6f2b0507efc34c68"></a>
#### Object

<a id="a5788b9e708f2e6f"></a>
##### SQL Object

SQL 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="245cb94519201525"></a>
<table class="table column_count_6"><caption>SQL 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center"><div>객체</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Database 
객체</div></td><td><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE REGISTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RESTORE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMENT ON object IS ..</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
객체</div></td><td><div>CREATE PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
객체</div></td><td><div>CREATE AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NOAUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
객체</div></td><td><div>CREATE USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GRANT privileges TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REVOKE privileges FROM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 
객체</div></td><td><div>CREATE SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
객체</div></td><td><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="20"><div>Table 
객체</div></td><td><div>CREATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRUNCATE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
객체</div></td><td><div>CREATE VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Index 
객체</div></td><td><div>CREATE INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. AGING</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. RENAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
객체</div></td><td><div>CREATE SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SEQUENCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
객체</div></td><td><div>CREATE SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
객체</div></td><td><div>CREATE PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
객체</div></td><td><div>CREATE FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="656d17ab30428f33"></a>
##### Cluster Object

Cluster 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="7d9c1aa9b9a2fe6a"></a>
<table class="table column_count_6"><caption>Cluster 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center"><div>객체</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Cluster system 
객체</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
객체</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Cluster table과 shard
객체</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Global 
secondary index
객체</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="265a59be3f2eb1be"></a>
#### SQL Language

<a id="64c361f94ce9692b"></a>
##### DML

데이터를 조작하는 DML 구문의 feature matrix는 다음과 같다.

**DML의 feature matrix**

<a id="27ceebd2e6310847"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| INSERT INTO .. | O | O | O | O |
| INSERT INTO .. RETURNING query | X | O | O | O |
| INSERT INTO .. RETURNING .. INTO .. | X | O | O | O |
| DELETE FROM .. | O | O | O | O |
| DELETE FROM .. RETURNING query | X | O | O | O |
| DELETE FROM .. RETURNING .. INTO .. | X | O | O | O |
| DELETE FROM .. WHERE CURRENT OF cursor | X | O | O | O |
| UPDATE .. | O | O | O | O |
| UPDATE .. RETURNING query | X | O | O | O |
| UPDATE .. RETURNING .. INTO .. | X | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | X | O | O | O |
| CALL proc_name | X | X | O | O |

<a id="59479ffae773aa6b"></a>
##### Query

데이터를 조회하는 SELECT 구문의 feature matrix는 다음과 같다.

**SELECT의 feature matrix**

<a id="07a4eadad0612598"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| &lt;query expression&gt; | O | O | O | O |
| &lt;query specification&gt; | O | O | O | O |
| &lt;select list&gt; | O | O | O | O |
| &lt;from clause&gt; | O | O | O | O |
| &lt;joined table&gt; | X | O | O | O |
| &lt;where clause&gt; | O | O | O | O |
| &lt;group by clause&gt; | X | O | O | O |
| &lt;order by clause&gt; | X | O | O | O |
| &lt;offset limit clause&gt; | O | O | O | O |
| &lt;set operator&gt; | X | O | O | O |
| &lt;subquery&gt; | X | O | O | O |
| &lt;hint clause&gt; | X | O | O | O |

<a id="96e523a5a857641c"></a>
##### Control Language

제어 구문의 feature matrix는 다음과 같다.

<a id="89331f5387846a21"></a>
<table class="table column_count_6"><caption>제어 구문의 feature matrix</caption><thead><tr><th class="to_center"><div>구분</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="d46810ad92fcc715"></a>
#### PSM Language

Persistent Stored Module (PSM) language element의 feature matrix는 다음과 같다.

**Persistent Stored Module (PSM) language element의 feature matrix**

<a id="2b737de5993f88e5"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| Assignment Statement | X | X | O | O |
| Basic LOOP Statement | X | X | O | O |
| Block (BEGIN .. END) | X | X | O | O |
| CASE Statement | X | X | O | O |
| CLOSE Statement | X | X | O | O |
| Collection Method Invocation | X | X | O | O |
| Collection Variable Declaration | X | X | O | O |
| CONTINUE Statement | X | X | O | O |
| Cursor FOR LOOP Statement | X | X | O | O |
| Cursor Variable Declaration | X | X | O | O |
| DELETE Statement Extension | X | X | O | O |
| EXCEPTION_INIT Pragma | X | X | O | O |
| Exception Declaration | X | X | O | O |
| Exception Handler | X | X | O | O |
| EXECUTE IMMEDIATE Statement | X | X | O | O |
| EXIT Statement | X | X | O | O |
| Explicit Cursor Declaration and Definition | X | X | O | O |
| FETCH Statement | X | X | O | O |
| FOR LOOP Statement | X | X | O | O |
| GOTO Statement | X | X | O | O |
| IF Statement | X | X | O | O |
| Implicit Cursor Attribute | X | X | O | O |
| INSERT Statement Extension | X | X | O | O |
| Named Cursor Attribute | X | X | O | O |
| NULL Statement | X | X | O | O |
| OPEN Statement | X | X | O | O |
| OPEN FOR Statement | X | X | O | O |
| Procedure Call | X | X | O | O |
| Procedure Declaration and Definition | X | X | O | O |
| RAISE Statement | X | X | O | O |
| Record Variable Declaration | X | X | O | O |
| RETURN Statement | X | X | O | O |
| RETURNING INTO clause | X | X | O | O |
| %ROWTYPE Attribute | X | X | O | O |
| Scalar Variable Declaration | X | X | O | O |
| SELECT INTO Statement | X | X | O | O |
| SQLCODE Function | X | X | O | O |
| SQLERRM Function | X | X | O | O |
| %TYPE Attribute | X | X | O | O |
| UPDATE Statement Extension | X | X | O | O |
| WHILE LOOP Statement | X | X | O | O |

<a id="dcc32f655e2b28c0"></a>
### API

<a id="6de80d3caa51520e"></a>
#### ODBC

ODBC 표준 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 feature matrix**

<a id="1e49e450d6d9fbe9"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| SQLAllocHandle() | O | O | O | O |
| SQLBindCol() | O | O | O | O |
| SQLBindParameter() | O | O | O | O |
| SQLCloseCursor() | O | O | O | O |
| SQLColAttribute() | X | O | O | O |
| SQLColumnPrivileges() | X | O | O | O |
| SQLColumns() | X | O | O | O |
| SQLConnect() | O | O | O | O |
| SQLDescribeCol() | O | O | O | O |
| SQLDescribeParam() | O | O | O | O |
| SQLDisconnect() | O | O | O | O |
| SQLDriverConnect() | X | O | O | O |
| SQLEndTran() | O | O | O | O |
| SQLExecDirect() | O | O | O | O |
| SQLExecute() | O | O | O | O |
| SQLExtendedFetch() | X | O | O | O |
| SQLFetch() | O | O | O | O |
| SQLFetchScroll() | X | O | O | O |
| SQLForeignKeys() | X | O | O | O |
| SQLFreeHandle() | O | O | O | O |
| SQLFreeStmt() | O | O | O | O |
| SQLGetConnectAttr() | O | O | O | O |
| SQLGetCursorName() | X | O | O | O |
| SQLGetData() | X | O | O | O |
| SQLGetDescField() | O | O | O | O |
| SQLGetDescRec() | O | O | O | O |
| SQLGetDiagField() | O | O | O | O |
| SQLGetDiagRec() | O | O | O | O |
| SQLGetEnvAttr() | O | O | O | O |
| SQLGetFunctions() | O | O | O | O |
| SQLGetInfo() | X | O | O | O |
| SQLGetStmtAttr() | O | O | O | O |
| SQLGetTypeInfo() | X | O | O | O |
| SQLMoreResults() | X | O | O | O |
| SQLNumParams() | O | O | O | O |
| SQLNumResultCols() | O | O | O | O |
| SQLParamData() | X | O | O | O |
| SQLPrepare() | O | O | O | O |
| SQLPrimaryKeys() | X | O | O | O |
| SQLProcedureColumns() | X | O | O | O |
| SQLProcedures() | X | O | O | O |
| SQLPutData() | X | O | O | O |
| SQLRowCount() | O | O | O | O |
| SQLSetConnectAttr() | O | O | O | O |
| SQLSetCursorName() | X | O | O | O |
| SQLSetDescField() | O | O | O | O |
| SQLSetDescRec() | O | O | O | O |
| SQLSetEnvAttr() | O | O | O | O |
| SQLSetPos() | X | O | O | O |
| SQLSetStmtAttr() | O | O | O | O |
| SQLSpecialColumns() | X | O | O | O |
| SQLStatistics() | X | O | O | O |
| SQLTablePrivileges() | X | O | O | O |
| SQLTables() | X | O | O | O |

ODBC 표준 이외의 부가적으로 지원하는 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 외 함수의 feature matrix**

<a id="b9be1b2bd377ac65"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| xa_open | X | O | O | O |
| xa_close | X | O | O | O |
| xa_start | X | O | O | O |
| xa_end | X | O | O | O |
| xa_rollback | X | O | O | O |
| xa_prepare | X | O | O | O |
| xa_commit | X | O | O | O |
| xa_recover | X | O | O | O |
| xa_forget | X | O | O | O |
| SQLGetXaSwitch | X | O | O | O |
| SQLGetXaConnectionHandle | X | O | O | O |
| SQLGetGroupCount | X | X | X | O |
| SQLGetGroupIDs | X | X | X | O |
| SQLGetGroupName | X | X | X | O |
| SQLGetSuitableGroupID | X | X | X | O |

<a id="3e0fdd1545c9d80c"></a>
#### JDBC

JDBC에 대한 class feature matrix는 다음과 같다.

**JDBC class의 feature matrix**

<a id="f631a26126ee5635"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| CallableStatement | X | X | O | O |
| CommonDataSource | X | O | O | O |
| Connection | X | O | O | O |
| ConnectionPoolDataSource | X | O | O | O |
| DatabaseMetaData | X | O | O | O |
| DataSource | X | O | O | O |
| Driver | X | O | O | O |
| ParameterMetaData | X | O | O | O |
| PooledConnection | X | O | O | O |
| PreparedStatement | X | O | O | O |
| ResultSet | X | O | O | O |
| ResultSetMetaData | X | O | O | O |
| RowId | X | O | O | O |
| Savepoint | X | O | O | O |
| Statement | X | O | O | O |
| XAConnection | X | O | O | O |
| XADataSource | X | O | O | O |
| XAResource | X | O | O | O |
| GoldilocksInterval | X | O | O | O |
| GoldilocksTypes | X | O | O | O |

<a id="d69306a0564939e8"></a>
#### Embedded SQL

<a id="0c92955f8900fa5a"></a>
##### Precompiler Option

Precompiler의 option에 대한 feature matrix는 다음과 같다.

**Precompiler option의 feature matrix**

<a id="bfb997a5f898716e"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --help | X | O | O | O |
| --include-path | X | O | O | O |
| --no-prompt | X | O | O | O |
| --output | X | O | O | O |
| --unsafe-null | X | O | O | O |
| --version | X | O | O | O |

<a id="3c2c589a8b4cbe4e"></a>
##### Embedded SQL 전용 구문

Embedded SQL에서만 사용할 수 있는 SQL 구문에 대한 feature matrix는 다음과 같다.

**Embedded SQL 전용 구문의 feature matrix**

<a id="a9d2987c8a126468"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| EXEC SQL AT | X | O | O | O |
| EXEC SQL ATOMIC INSERT | X | O | O | O |
| EXEC SQL AUTOCOMMIT | X | O | O | O |
| EXEC SQL BEGIN DECLARE SECTION | X | O | O | O |
| EXEC SQL COMMIT RELEASE | X | O | O | O |
| EXEC SQL CONNECT | X | O | O | O |
| EXEC SQL CONTEXT ALLOCATE | X | O | O | O |
| EXEC SQL CONTEXT FREE | X | O | O | O |
| EXEC SQL CONTEXT USE | X | O | O | O |
| EXEC SQL DISCONNECT | X | O | O | O |
| EXEC SQL END DECLARE SECTION | X | O | O | O |
| EXEC SQL FOR | X | O | O | O |
| EXEC SQL GET GROUPID | X | X | X | O |
| EXEC SQL INCLUDE | X | O | O | O |
| EXEC SQL INCLUDE SQLCA | X | O | O | O |
| EXEC SQL OPTION | X | O | O | O |
| EXEC SQL ROLLBACK RELEASE | X | O | O | O |
| EXEC SQL WHENEVER | X | O | O | O |

<a id="10c6ffba4a112cf6"></a>
##### Host Variable Data Type

Host 변수에 사용할 수 있는 embbeded SQL data type의 feature matrix는 다음과 같다.

**Host data type의 feature matrix**

<a id="eaa9df8b08d958a1"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| C native type | X | O | O | O |
| struct, union | X | O | O | O |
| typedef | X | O | O | O |
| VARCHAR | X | O | O | O |
| LONG VARCHAR | X | O | O | O |
| BINARY | X | O | O | O |
| LONG VARBINARY | X | O | O | O |
| BOOLEAN | X | O | O | O |
| NUMBER | X | O | O | O |
| DATE | X | O | O | O |
| TIME | X | O | O | O |
| TIME WITH TIMEZONE | X | O | O | O |
| TIMESTAMP | X | O | O | O |
| TIMESTAMP WITH TIMEZONE | X | O | O | O |
| INTERVAL YEAR | X | O | O | O |
| INTERVAL MONTH | X | O | O | O |
| INTERVAL DAY | X | O | O | O |
| INTERVAL HOUR | X | O | O | O |
| INTERVAL MINUTE | X | O | O | O |
| INTERVAL SECOND | X | O | O | O |
| INTERVAL YEAR TO MONTH | X | O | O | O |
| INTERVAL DAY TO HOUR | X | O | O | O |
| INTERVAL DAY TO MINUTE | X | O | O | O |
| INTERVAL DAY TO SECOND | X | O | O | O |
| INTERVAL HOUR TO MINUTE | X | O | O | O |
| INTERVAL HOUR TO SECOND | X | O | O | O |
| INTERVAL MINUTE TO SECOND | X | O | O | O |

<a id="cf6e3fb94b733364"></a>
##### Dynamic SQL

Dynamic SQL에 대한 feature matrix는 다음과 같다.

**Dynamic SQL의 feature matrix**

<a id="9d3969f588144414"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| SELECT .. INTO | X | O | O | O |
| EXECUTE IMMEDIATE sql | X | O | O | O |
| PREPARE stmt | X | O | O | O |
| EXECUTE stmt | X | O | O | O |
| DECLARE cursor FOR sql | X | O | O | O |
| DECLARE cursor FOR stmt | X | O | O | O |
| OPEN cursor | X | O | O | O |
| OPEN cursor USING | X | O | O | O |
| FETCH cursor INTO | X | O | O | O |
| CLOSE cursor | X | O | O | O |
| DELETE .. WHERE CURRENT OF cursor | X | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | X | O | O | O |

<a id="06bd25e746729975"></a>
#### PyDBC

<a id="3036eca7ef8e7c44"></a>
##### Module

PyDBC가 제공하는 pygoldilocks의 method feature matrix는 다음과 같다.

**pygoldilock method의 feature matrix**

<a id="11d68f84e45f986f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| connect | X | X | X | O |
| Date | X | X | X | O |
| Time | X | X | X | O |
| Timestamp | X | X | X | O |
| DateFromTicks | X | X | X | O |
| TimeFromTicks | X | X | X | O |
| TimestampFromTicks | X | X | X | O |
| Binary | X | X | X | O |
| STRING | X | X | X | O |
| BINARY | X | X | X | O |
| NUMBER | X | X | X | O |
| DATETIME | X | X | X | O |
| ROWID | X | X | X | O |
| getDecimalSeparator | X | X | X | O |
| setDecimalSeparator | X | X | X | O |

pygoldilocks module의 attribute feature matrix는 다음과 같다.

**pygoldilock attribute의 feature matrix**

<a id="414c807216f56f82"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| apilevel | X | X | X | O |
| threadsafety | X | X | X | O |
| paramstyle | X | X | X | O |
| version | X | X | X | O |
| lowercase | X | X | X | O |

<a id="66a99a37455dc501"></a>
##### Connection

Connection 객체의 method feature matrix는 다음과 같다.

**Connection method의 feature matrix**

<a id="6d664f2b50cd0133"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| cursor | X | X | X | O |
| commit | X | X | X | O |
| rollback | X | X | X | O |
| close | X | X | X | O |
| getinfo | X | X | X | O |
| execute | X | X | X | O |
| set_attr | X | X | X | O |

Connection 객체의 attribute feature matrix는 다음과 같다.

**Connection attribute의 feature matrix**

<a id="89f15edab1c1f2d7"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| autocommit | X | X | X | O |
| searchescape | X | X | X | O |
| timeout | X | X | X | O |

<a id="e034161c02103a32"></a>
##### Cursor

Cursor 객체의 method feature matrix는 다음과 같다.

**Cursor method의 feature matrix**

<a id="1c71103ebc8f6c25"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| excute | X | X | X | O |
| executemany | X | X | X | O |
| fetchone | X | X | X | O |
| fetchall | X | X | X | O |
| fetchmany | X | X | X | O |
| commit | X | X | X | O |
| rollback | X | X | X | O |
| skip | X | X | X | O |
| nextset | X | X | X | O |
| close | X | X | X | O |
| setinputsizes | X | X | X | O |
| setoutputsize | X | X | X | O |
| callproc | X | X | X | O |
| callfunc | X | X | X | O |
| tables | X | X | X | O |
| columns | X | X | X | O |
| statistics | X | X | X | O |
| rowIdColumns | X | X | X | O |
| rowVerColumns | X | X | X | O |
| primaryKeys | X | X | X | O |
| foreignKeys | X | X | X | O |
| procedures | X | X | X | O |
| getTypeInfo | X | X | X | O |

Cursor 객체의 attribute feature matrix는 다음과 같다.

**Cursor attribute의 feature matrix**

<a id="9731aae81a95372f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| Description | X | X | X | O |
| rowcount | X | X | X | O |
| arraysize | X | X | X | O |
| connection | X | X | X | O |
| fast_executemany | X | X | X | O |

<a id="cc15aef719ce5ccb"></a>
##### Row

Row 객체의 attribute feature matrix는 다음과 같다.

**Row attribute의 feature matrix**

<a id="fc4acf5d73cb323f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| cursor_description | X | X | X | O |

<a id="3c9bef488e637739"></a>
### Utility

<a id="18c777af286e05e6"></a>
#### gcreatedb

<a id="ae2621d5fde71b61"></a>
##### Command Usage

gcreatedb의 command usage에 대한 feature matrix는 다음과 같다.

**gcreatedb command usage의 feature matrix**

<a id="9acd349c08b3b68f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --character_set | O | O | O | O |
| --char_length_units | X | O | O | O |
| --cluster | X | X | O | O |
| --db_comment | O | O | O | O |
| --help | O | O | O | O |
| --host | X | X | O | O |
| --member | X | X | O | O |
| --port | X | X | O | O |
| --silent | O | O | O | O |
| --timezone | X | O | O | O |

<a id="72f2d828c572db8b"></a>
#### glsnr

<a id="a12be70b1b1d088c"></a>
##### Command Usage

glsnr의 command usage에 대한 feature matrix는 다음과 같다.

**glsnr command usage의 feature matrix**

<a id="67373ba49033e2f7"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --help | X | O | O | O |
| --home | X | X | O | O |
| --silent | X | O | O | O |
| --start | X | O | O | O |
| --status | X | O | O | O |
| --stop | X | O | O | O |

<a id="d86adddf6034fe6e"></a>
##### Configuration File

glsnr의 configuration에 대한 feature matrix는 다음과 같다.

**glsnr configuration file syntax의 feature matrix**

<a id="881b593779562eff"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| BACKLOG | X | O | O | O |
| DEFAULT_CS_MODE | X | O | O | O |
| LISTENER_LOG_DIR | X | X | O | O |
| LISTEN_PORT | X | O | O | O |
| TCP_EXCLUDED | X | O | O | O |
| TCP_INVITED | X | O | O | O |
| TCP_HOST | X | O | O | O |
| TCP_VALIDNODE_CHECKING | X | O | O | O |
| TIMEOUT | X | O | O | O |
| USR_DIR | X | X | O | O |

<a id="9bf5322b1e56fa5a"></a>
#### gsql/ gsqlnet

<a id="74d8d9b2aaa8f53c"></a>
##### Command Usage

gsql의 command usage에 대한 feature matrix는 다음과 같다.

**gsql command usage의 feature matrix**

<a id="f8bcdd04e794e203"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| username password | O | O | O | O |
| --as {SYSDBA\|ADMIN} | X | O | O | O |
| --conn-string | X | O | O | O |
| --dsn | X | O | O | O |
| --enable-color | O | O | O | O |
| --help | O | O | O | O |
| --import | O | O | O | O |
| --no-prompt | O | O | O | O |
| --prompt | O | O | O | O |
| --silent | O | O | O | O |
| --version | O | O | O | O |

<a id="82bef1b1d9895696"></a>
##### Interactive gsql Command

gsql 프롬프트 상태에서 사용하는 interactive gsql command에 대한 feature matrix는 다음과 같다.

**Interactive gsql command의 feature matrix**

<a id="91675309c9f380cf"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| `\\` | O | O | O | O |
| `\connect userid password [as sysdba] ` | X | O | O | O |
| `\cshutdown` | X | X | O | O |
| `\cstartup` | X | X | O | O |
| `\ddl_cluster` | X | X | O | O |
| `\ddl_db` | X | O | O | O |
| `\ddl_tablespace` | X | O | O | O |
| `\ddl_profile` | X | O | O | O |
| `\ddl_audit_policy` | X | X | X | O |
| `\ddl_auth` | X | O | O | O |
| `\ddl_schema` | X | O | O | O |
| `\ddl_publicsynonym` | X | O | O | O |
| `\ddl_table` | X | O | O | O |
| `\ddl_constraint` | X | O | O | O |
| `\ddl_index` | X | O | O | O |
| `\ddl_view` | X | O | O | O |
| `\ddl_sequence` | X | O | O | O |
| `\ddl_synonym` | X | O | O | O |
| `\ddl_procedure` | X | X | O | O |
| `\desc ` | O | O | O | O |
| `\dynamic sql :var ` | X | O | O | O |
| `\exec ` | O | O | O | O |
| `\exec :var := :value` | O | O | O | O |
| `\exec sql ` | O | O | O | O |
| `\explain plan [on\|only] ` | O | O | O | O |
| `\help ` | O | O | O | O |
| `\history` | O | O | O | O |
| `\host {os_command}` | X | X | O | O |
| `\import` | O | O | O | O |
| `\idesc ` | O | O | O | O |
| `\{n} ` | O | O | O | O |
| `\prepare sql ` | O | O | O | O |
| `\print ` | O | O | O | O |
| `\quit` | O | O | O | O |
| `\set autocommit ` | O | O | O | O |
| `\set color ` | O | O | O | O |
| `\set colsize ` | X | O | O | O |
| `\set ddlsize` | X | O | O | O |
| `\set error ` | O | O | O | O |
| `\set history ` | O | O | O | O |
| `\set linesize ` | O | O | O | O |
| `\set numsize ` | X | O | O | O |
| `\set pagesize ` | O | O | O | O |
| `\set timing ` | O | O | O | O |
| `\set vertical ` | O | O | O | O |
| `\shutdown {abort\|immediate\|transactional\|normal}` | X | O | O | O |
| `\startup {nomount\|mount\|open} ` | X | O | O | O |
| `\var ` | O | O | O | O |

<a id="69e3be1a4d581ca0"></a>
#### gloader/ gloadernet

<a id="e6becd09b995aae4"></a>
##### Command Usage

gloader의 command usage에 대한 feature matrix는 다음과 같다.

**gloader command usage의 feature matrix**

<a id="b7dfe1e03dc6ae5a"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| username password | O | O | O | O |
| --array | O | O | O | O |
| --atomic | O | O | O | O |
| --bad | O | O | O | O |
| --buffered | X | O | O | O |
| --commit | O | O | O | O |
| --control | O | O | O | O |
| --data | O | O | O | O |
| --dsn | X | O | O | O |
| --errors | X | O | O | O |
| --export | O | O | O | O |
| --fieldterm | X | X | O | O |
| --filesize | X | O | O | O |
| --format | X | O | O | O |
| --help | O | O | O | O |
| --import | O | O | O | O |
| --lineterm | X | X | O | O |
| --log | O | O | O | O |
| --no-prompt | O | O | O | O |
| --parallel | O | O | O | O |
| --propagation | X | O | O | O |
| --qualifier | X | X | O | O |
| --silent | O | O | O | O |
| --AsTIMESTAMP | X | O | O | O |
| --where | X | X | X | O |
| --group-id | X | X | X | O |
| --directio-size | X | X | X | O |

<a id="d044077c97fbe4db"></a>
##### Control File Syntax

gloader의 control file syntax에 대한 feature matrix는 다음과 같다.

**gloader control file syntax의 feature matrix**

<a id="ed229256ce61f566"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| CHARACTERSET | X | O | O | O |
| FIELDS TERMINATED BY | O | O | O | O |
| OPTIONALLY ENCLOSED BY | O | O | O | O |
| TABLE table_name | O | O | O | O |
| TABLE schema_name.table_name | X | O | O | O |
| LTRIM | X | X | O | O |
| RTRIM | X | X | O | O |
| LINES TERMINATED BY | X | X | O | O |
| WHERE | X | X | X | O |

<a id="e7a824d8032ede3b"></a>
#### gdump

<a id="e97b9ed289f42247"></a>
##### Command Usage

gdump의 command usage에 대한 feature matrix는 다음과 같다.

<a id="c480c5fdb2d3fdf0"></a>
<table class="table column_count_6"><caption>gdump command usage의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="14ae66e999ef4a27"></a>
#### tablediff

<a id="d9bacc0163871b94"></a>
##### Configuration File

tablediff의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="9c7d1ab2782fb596"></a>
<table class="table column_count_6"><caption>tablediff configuration file의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td><div>SOURCE_PASSWORD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_URL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td><div>TARGET_PASSWORD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_URL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td><div>TARGET_INSERT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_UPDATE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_DELETE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_INSERT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td><div>DIFF_BIN_FILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DIFF_OUT_FILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_CALL_STACK</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_ROW_UNIT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>EXCLUDE_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_DIFF</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_SUCCESS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_QUEUE_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_THREAD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_UNIT_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PARTITION_RANGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_OUT_FILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>WHERE_CLAUSE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="1ae5a8726d1f8575"></a>
#### gsyncher

<a id="d8345f6960be753b"></a>
##### Command Usage

gsyncher의 command usage에 대한 feature matrix는 다음과 같다.

**gsyncher command usage의 feature matrix**

<a id="f45a662fa9729191"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --log | X | O | O | O |
| --silent | X | O | O | O |
| --home | X | X | O | O |
| --copy-right | X | O | O | O |
| --backup-path | X | O | O | O |
| --help | X | O | O | O |

<a id="7000adf3ebb35659"></a>
#### gmon

<a id="fe46cfc29f6cb5ee"></a>
##### Command Usage

gmon의 command usage에 대한 feature matrix는 다음과 같다.

**gmon command usage의 feature matrix**

<a id="e3e959e116a530a0"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --start | X | X | O | O |
| --stop | X | X | O | O |
| --status | X | X | O | O |
| --home | X | X | O | O |
| --silent | X | X | O | O |
| --no-copyright | X | X | O | O |
| --help | X | X | O | O |

<a id="3a8c8a9e2f2dc723"></a>
#### gtrclogger

<a id="0677d232daadca3a"></a>
##### Command Usage

gtrclogger의 command usage에 대한 feature matrix는 다음과 같다.

**gtrclogger command usage의 feature matrix**

<a id="8b7b2b9e6a26d68e"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --dir | X | X | O | O |
| --help | X | X | O | O |
| --port | X | X | O | O |
| --start | X | X | O | O |
| --stop | X | X | O | O |

<a id="e609cae483c440aa"></a>
#### glocator

<a id="d808d83dde540251"></a>
##### Command Usage

glocator의 command usage에 대한 feature matrix는 다음과 같다.

**glocator command usage의 feature matrix**

<a id="bc423aab495a6968"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --create | X | X | O | O |
| --start | X | X | O | O |
| --stop | X | X | O | O |
| --conf | X | X | O | O |
| --status | X | X | O | O |
| --sync | X | X | X | O |
| --silent | X | X | O | O |
| --no-copyright | X | X | O | O |
| --help | X | X | O | O |

<a id="054d1656ac44abb4"></a>
##### Configuration File

glocator의 configuration file에 대한 feature matrix는 다음과 같다.

**glocator command usage의 feature matrix**

<a id="5af3046d2bc5f053"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| PORT | X | X | O | O |
| WORKER_COUNT | X | X | O | O |
| SESSION_QUEUE_SIZE | X | X | O | O |
| SESSION_ALLOCATOR_SIZE | X | X | O | O |
| PACKET_ALLOCATOR_SIZE | X | X | O | O |
| SYSTEM_LOGGER_DIR | X | X | O | O |
| SYSTEM_UDS_DIR | X | X | O | O |
| LOCATION_FILE_DIR | X | X | O | O |
| LOCATION_FILE_SIZE | X | X | O | O |
| LOCATION_FILE_MAX_SIZE | X | X | O | O |
| SESSION_TIMEOUT | X | X | O | O |
| FAILOVER_TIMEOUT | X | X | O | O |
| ALTERNATE_LOCATORS | X | X | X | O |
| SYNC_RETRY_COUNT | X | X | X | O |
| SYNC_RESPONSE_TIMEOUT | X | X | X | O |

<a id="35f4bbba115f2d23"></a>
#### gagent

<a id="d28ae2cac1431028"></a>
##### Command Usage

gagent의 command usage에 대한 feature matrix는 다음과 같다.

**gagent command usage의 feature matrix**

<a id="d4d7d6e1fd227842"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --start | X | X | O | O |
| --stop | X | X | O | O |
| --conf | X | X | O | O |
| --status | X | X | O | O |
| --home | X | X | O | O |
| --silent | X | X | O | O |
| --no-copyright | X | X | O | O |
| --help | X | X | O | O |

<a id="c97c4117358602d9"></a>
##### Configuration File

gagent의 configuration file에 대한 feature matrix는 다음과 같다.

**gagent configuration file의 feature matrix**

<a id="38d5f2771202deac"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| PORT | X | X | O | O |
| LOCATOR_HOST | X | X | O | O |
| LOCATOR_PORT | X | X | O | O |
| COMMAND_QUEUE_SIZE | X | X | O | O |
| COMMAND_ALLOCATOR_SIZE | X | X | O | O |
| PACKET_ALLOCATOR_SIZE | X | X | O | O |
| SYSTEM_LOGGER_DIR | X | X | O | O |
| SESSION_TIMEOUT | X | X | O | O |
| UPDATE_LOCATION_TIME | X | X | O | O |
| ALTERNATE_LOCATORS | X | X | X | O |

<a id="a708b21e79d02f9d"></a>
#### gloctl

<a id="f6ddcf5d3db13aeb"></a>
##### Command Usage

gloctl의 command usage에 대한 feature matrix는 다음과 같다.

**gloctl command usage의 feature matrix**

<a id="414984bfc29ef6a7"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --dsn | X | X | O | X |
| --conf | X | X | X | O |
| --ip | X | X | O | O |
| --port | X | X | O | O |
| --import | X | X | O | O |
| --silent | X | X | O | O |
| --no-copyright | X | X | O | O |
| --help | X | X | O | O |

<a id="0b430d6b8b274522"></a>
##### Configuration File

gloctl의 configuration file에 대한 feature matrix는 다음과 같다.

**gloctl configuration file의 feature matrix**

<a id="5d6fa189679f2ae6"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| PORT | X | X | X | O |
| LOCATOR_HOST | X | X | X | O |
| LOCATOR_PORT | X | X | X | O |

<a id="65f12fc84b08c09b"></a>
### Replication

<a id="9dbcc5c279723e79"></a>
#### cyclone

<a id="a4670ebedcd9204e"></a>
##### Command Usage

cyclone의 command usage에 대한 feature matrix는 다음과 같다.

**cyclone command usage의 feature matrix**

<a id="69a0b0acd659d388"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --conf | X | O | O | O |
| --encrypt | X | X | O | O |
| --group | X | O | O | O |
| --help | X | O | O | O |
| --key | X | X | O | O |
| --master | X | O | O | O |
| --reset | X | O | O | O |
| --silent | X | O | O | O |
| --slave | X | O | O | O |
| --start | X | O | O | O |
| --status | X | O | O | O |
| --stop | X | O | O | O |
| --sync | X | O | O | O |
| --stand-alone | X | X | X | O |
| --recovery | X | X | X | O |
| --local | X | X | X | O |

<a id="6e22ac8b7a993dfb"></a>
##### Configuration File

cyclone의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="2e27135197a9a8da"></a>
<table class="table column_count_6"><caption>cyclone configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="785b35353feabd96"></a>
#### logmirror

<a id="859e7e28650d46e4"></a>
##### Command Usage

logmirror의 command usage에 대한 feature matrix는 다음과 같다.

**logmirror command usage의 feature matrix**

<a id="fa7166a61e7fa620"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --conf | X | O | O | O |
| --help | X | O | O | O |
| --infiniband | X | O | O | O |
| --master | X | O | O | O |
| --silent | X | O | O | O |
| --slave | X | O | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |

<a id="898eb78823deb45b"></a>
##### Configuration File

logmirror의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="8ed0373154f79fc8"></a>
<table class="table column_count_6"><caption>logmirror configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="cdb8f96b74963b25"></a>
#### cymon

<a id="dc0341ed9a24c035"></a>
##### Command Usage

cymon의 command usage에 대한 feature matrix는 다음과 같다.

**cymon command usage의 feature matrix**

<a id="7d85a4693e4d5be7"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --conf | X | O | O | O |
| --help | X | O | O | O |
| --cycle | X | O | O | O |
| --key | X | X | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |
| --status | X | O | O | O |

<a id="a3a057dce8a31fd1"></a>
## What's New in GOLDILOCKS 3.2

본 장에서는 GOLDILOCKS 3.2에 새로 추가된 기능들에 대해 간략히 설명한다.

<a id="1ae0dcc961585459"></a>
### Architecture

<a id="cc3bc452e2343489"></a>
#### System Architecture

변동 사항 없음

<a id="59697a02506cfc04"></a>
#### Storage Internal

변동 사항 없음

<a id="c5b001d23a0323b2"></a>
#### Transaction Control

변동 사항 없음

<a id="066c9c29f84eb47f"></a>
#### Backup & Recovery

변동 사항 없음

<a id="be4eae71db5db81c"></a>
#### Database Information

<a id="d4b361fb1d7c7211"></a>
##### DICTIONARY_SCHEMA

Audit policy 객체 정보를 조회하기 위한 다음 view가 추가되었다.

- [AUDIT_POLICIES](../part-02-administration-manual/9-database-information.md#2aed231f5a379c46)
- [AUDIT_POLICY_OPTIONS](../part-02-administration-manual/9-database-information.md#513c1853a2e073df)
- [AUDIT_POLICY_ENABLED](../part-02-administration-manual/9-database-information.md#e60b8c262c2a23c3)

Audit record를 조회하기 위해 [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#2eb922e8e06a1b57)이 추가되었다.

다음 view가 제거되었다.

- ALL_COL_PLACE
- DBA_COL_PLACE
- USER_COL_PLACE

<a id="b5b36ab02395dc0d"></a>
##### INFORMATION_SCHEMA

변동 사항 없음

<a id="c5b2dd186f90ef07"></a>
##### PERFORMANCE_VIEW_SCHEMA

Audit policy의 옵션을 정의할 때 system action, privilege action에 나열할 수 있는 정보를 조회하기 위한 view가 추가되었다.

- [V$AUDITABLE_DB_PRIVILEGES](../part-02-administration-manual/9-database-information.md#d46668d49037a36a)
- [V$AUDITABLE_SYSTEM_ACTIONS](../part-02-administration-manual/9-database-information.md#b41cc53cda66f791)

<a id="05b7c3fd468a69f6"></a>
#### Server Property

<a id="59d9c7c3f2258ff7"></a>
##### Global Temporary Table을 위한 프로퍼티 추가

Global temporary table에 대해 undo logging tablespace를 지정하기 위해 [TEMP_UNDO_ENABLED](../part-02-administration-manual/10-server-property.md#7c831a78045be60a) 프로퍼티가 추가되었다.  
Global temporary table이나 global temporary index의 segment cache 크기를 지정하기 위해 [TEMP_SEGMENT_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#56e88319bfcad81c) 프로퍼티가 추가되었다.

<a id="1f2ab50a43841c3b"></a>
##### Page 개수 변경에 따른 Recompile 기능 제거

3.1 까지 지원하던 page 개수 변경에 따른 recompile 기능이 제거되었다.  
따라서 다음과 같은 프로퍼티를 지원하지 않는다.

- [RECOMPILE_CHECK_MINIMUM_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#b7d56d90a78c778e)
- [RECOMPILE_PAGE_PERCENT](../part-02-administration-manual/10-server-property.md#a6e4a785a58f7242)

<a id="951f0bf334bda5c4"></a>
##### Auxiliary Tablespace를 위한 프로퍼티 추가

Auxiliary tablespace의 크기를 결정하기 위한 [SYSTEM_MEMORY_AUX_TABLESPACE_SIZE](../part-02-administration-manual/10-server-property.md#4792ffa5a1cd100e) 프로퍼티가 추가되었다.

<a id="92e48761ce523ded"></a>
##### 통신 데이터 압축을 위한 프로퍼티 추가

통신 데이터 압축 여부를 결정하는 [PACKET_COMPRESSION_THRESHOLD](../part-02-administration-manual/10-server-property.md#9f68af2aa947bbca) 프로퍼티가 추가되었다.

<a id="013b613ee5119f08"></a>
##### Redo Log 압축을 위한 프로퍼티 추가

Redo log 압축 여부를 결정하는 [REDO_LOG_COMPRESSION_THRESHOLD](../part-02-administration-manual/10-server-property.md#9d0b6c8dcc448227) 프로퍼티가 추가되었다.

<a id="eedd6d75297c81ac"></a>
##### USE_LARGE_PAGES 프로퍼티 추가

HugePage를 사용하기 위해 [USE_LARGE_PAGES](../part-02-administration-manual/10-server-property.md#4f5b19b609458ab0) 프로퍼티가 추가되었다.

<a id="c472856fb58a06b2"></a>
### SQL

<a id="4e8ffaa7429bdca0"></a>
#### SQL Element

<a id="861393ce41453f7a"></a>
##### Data Type

변동 사항 없음

<a id="dc67902bafe90bab"></a>
##### Function

다음과 같이 분산 관련 aggregation 함수가 추가되었다.  

• [STDDEV](../part-03-sql-manual/11-sql-elements.md#55362e40aae95d6a)  
• [STDDEV_POP](../part-03-sql-manual/11-sql-elements.md#6402c3dcd4e4fe05)  
• [STDDEV_SAMP](../part-03-sql-manual/11-sql-elements.md#3cc8ea60b60a3c12)  
• [VARIANCE](../part-03-sql-manual/11-sql-elements.md#051de20384a5e1c8)  
• [VAR_POP](../part-03-sql-manual/11-sql-elements.md#46e177e0aaffbb82)  
• [VAR_SAMP](../part-03-sql-manual/11-sql-elements.md#345e88314b92a36d)  

문자열 함수 [REVERSE](../part-03-sql-manual/11-sql-elements.md#1809a812fddd9afb)가 추가되었다.  

날짜형 함수 [MONTHS_BETWEEN](../part-03-sql-manual/11-sql-elements.md#08319e67af5037d1)이 추가되었다.

<a id="736f1ac3442aba85"></a>
#### Object

<a id="da8522288b666b32"></a>
##### Audit Policy

SQL 수행을 감사할 수 있는 [Audit Policy](../part-03-sql-manual/13-sql-objects.md#d9b540771815ba3c) 객체가 추가되었다.

<a id="2b61f6d82007b749"></a>
##### Global Temporary Table

세션에 종속적인 임시 테이블인 [Global Temporary Table](../part-03-sql-manual/13-sql-objects.md#7715e064852d7bc8) 객체가 추가되었다.

<a id="de97718556efab23"></a>
#### SQL Language

<a id="efd860c8ed7635b7"></a>
##### ANALYZE TABLE 구문의 병렬처리

[ANALYZE TABLE](../part-03-sql-manual/16-sql-references.md#313298c58633e794) 구문에 병렬처리 옵션이 추가되었다.

<a id="c17d99922fa9d8bb"></a>
##### Audit Policy DDL

Audit Policy 객체를 제어할 수 있는 다음 DDL이 추가되었다.

- Audit policy 생성
    - [CREATE AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#676233f209f722e4)
- Audit policy 제거
    - [DROP AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#c1e1a11e6ac9443a)
- Audit policy 변경
    - [ALTER AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#2cfef6a9826bdadf)
- Audit policy 활성화
    - [AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#c789ab5113d50e70)
- Audit policy 비활성화
    - [NOAUDIT POLICY](../part-03-sql-manual/16-sql-references.md#2953451ac097af0c)
- Audit trail 삭제
    - [ALTER DATABASE CLEAR AUDIT TRAIL](../part-03-sql-manual/16-sql-references.md#016c886b7cddf620)

<a id="98c08ce535888a62"></a>
##### User DDL

사용자의 default index tablespace가 추가되었다.

- User 생성
    - [CREATE USER](../part-03-sql-manual/16-sql-references.md#339657c579ea782f)
- User 변경
    - [ALTER USER](../part-03-sql-manual/16-sql-references.md#c2d86feb760d5ff5)

<a id="2c8918d6c7091acb"></a>
##### Table DDL

테이블 객체를 변경하는 다음 DDL이 추가되었다.

- 테이블 제약 조건의 이름 변경
    - [ALTER TABLE name RENAME CONSTRAINT](../part-03-sql-manual/16-sql-references.md#eea8cc70d72eed91)
- 테이블의 속성 변경
    - [ALTER TABLE name READ { ONLY | WRITE }](../part-03-sql-manual/16-sql-references.md#0e36db5fd37b58b3)
- Cluster 환경에서 테이블의 특정 shard 이름 변경
    - [ALTER TABLE name RENAME SHARD](../part-03-sql-manual/16-sql-references.md#a2da1b506cc85d50)

[Global temporary table](../part-03-sql-manual/16-sql-references.md#cda0b9b5e565ed2c)을 생성하는 DDL이 추가되었다.

<a id="5ae700730041164e"></a>
##### Index DDL

인덱스 객체를 변경하는 다음과 같은 DDL이 추가되었다.

- 인덱스 이름 변경
    - [ALTER INDEX name RENAME TO](../part-03-sql-manual/16-sql-references.md#816edfcde4e7f3c5)

<a id="343eb4e5c9cefcfd"></a>
##### Cluster System DDL

Cluster system 객체를 변경하는 다음과 같은 DDL이 추가되었다.

- 회복 불가한 cluster member 지정
    - [ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER](../part-03-sql-manual/16-sql-references.md#98ba2c93e7943236)

<a id="61b0ae87e5c68a1d"></a>
##### System DCL

System 객체를 제어하는 다음과 같은 DCL이 추가되었다.

- GLOBAL CONNECTION을 사용하는 세션의 재접속 설정
    - [ALTER SYSTEM RECONNECT GLOBAL CONNECTION](../part-03-sql-manual/16-sql-references.md#26ff93695df9d6b1)

<a id="bc491716888709f1"></a>
### API

<a id="245e19e336f0ce09"></a>
#### ODBC

<a id="4dec011766493279"></a>
##### odbc.ini

[odbc.ini 파일](../part-05-developer-manual/25-odbc.md#78b0fc955ee2c6e5)에 data source name 키워드로 LOCATOR_SERVICE와 PACKET_COMPRESSION_THRESHOLD가 추가되었다.

Location 키워드로 ALTERNATE_LOCATORS와 CONNECTION_TIMEOUT이 추가되었다.

<a id="dfa9036f2c7b6974"></a>
##### GLOBAL CONNECTION

[GLOBAL CONNECTION](../part-05-developer-manual/25-odbc.md#6d615db06c59e6d5)을 지원한다.

<a id="169fb9ca326f404d"></a>
#### Statement Attributes

Statement 속성값으로 SQL_ATTR_FETCH_FAILOVER가 추가되었다.

<a id="175ca179354dfc11"></a>
#### JDBC

<a id="2c9f472e18df10a4"></a>
##### 연결 프로퍼티

[연결 프로퍼티](../part-05-developer-manual/26-jdbc.md#2e3a6037193b88a9)에 packet_compression_threshold가 추가되었다.

<a id="02b1472026aa5d61"></a>
#### Embedded SQL

[EXEC SQL GET GROUPID INTO](../part-05-developer-manual/27-embedded-sql.md#49e8f9f9ff6789e5) 명령이 추가되었다.

<a id="6f2dfeea7a9ff85f"></a>
#### PDO

Venus 3.2 버전부터 PDO에서 GOLDILOCKS에 접근할 수 있는 [PDO](../part-05-developer-manual/28-pdo.md#c4a284eb87b22dea) 드라이버를 제공한다.

<a id="2657ebf9fbe2ab11"></a>
#### PyDBC

Venus 3.2 버전부터 python 언어를 위한 API인 [PyDBC](../part-05-developer-manual/29-pydbc.md#7b056e2eababdd04)를 제공한다.

<a id="80494d4d2f8c39b2"></a>
#### Ruby

Venus 3.2 버전부터 ruby 언어를 위한 API인 [Ruby](#80494d4d2f8c39b2) 드라이버를 제공한다.

<a id="799d81fdca59e82b"></a>
#### Hibernate

Venus 3.2 버전부터 Java ORM 프레임워크인 [Hibernate](../part-05-developer-manual/30-hibernate.md#285a06f705a82a37)와 연동할 수 있는 소스를 제공한다.

<a id="e08fc7e86404c968"></a>
### Utility

<a id="fa3962c82946d8e3"></a>
#### gcreatedb

변동 사항 없음

<a id="b8db111ff71bc709"></a>
#### glsnr

변동 사항 없음

<a id="e691214b4b2f98e8"></a>
#### gsql/gsqlnet

<a id="0686c80be65ec841"></a>
##### Audit Policy 객체의 DDL 출력

Audit 객체에 대한 DDL을 출력하기 위해 interactive command [`\ddl_audit_policy`](../part-06-utility-manual/33-gsql-gsqlnet-interactive-sql-tool.md#921a93045ab9b362)가 추가되었다.

<a id="a06464e3c6c92be2"></a>
##### SET HEADING {ON | OFF}

질의 결과에 헤더를 출력할지 여부를 설정하기 위해 [`\set heading`](../part-06-utility-manual/33-gsql-gsqlnet-interactive-sql-tool.md#227e43038968397d)가 추가되었다.

<a id="294a299131b1ef1b"></a>
#### gloader/gloadernet

<a id="761a0a357f39a5fe"></a>
##### WHERE 절

export (데이터 다운로드)에 다음과 같은 조건문을 설정할 수 있도록 하였다.

- [WHERE](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#c457e62027ebd857)
- [--where](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#fb6d1df237ecff91)

<a id="b8013bdbee495bea"></a>
##### --group-id

gloader 명령 인자로 [--group-id](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#e2e635e5daf1d03c)가 추가되었다.

<a id="9c855dd7588e5ad9"></a>
##### --directio-size

gloader 명령 인자로 [--directio-size](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#504b5b9377ee61e0)가 추가되었다.

<a id="14eeb99ecc727e2e"></a>
#### gdump

변동 사항 없음

<a id="5ec68dc30bf9f34a"></a>
#### tablediff

변동 사항 없음

<a id="3f067416bf0ff6f6"></a>
#### gsyncher

변동 사항 없음

<a id="9b7190f469e21d83"></a>
#### gmon

변동 사항 없음

<a id="7cba80df25f77666"></a>
#### gtrclogger

변동 사항 없음

<a id="c4bf1ca76f37d97a"></a>
#### glocator

<a id="94f71515e6c2fb39"></a>
##### Configuration

다중화 관련 configuration 키워드로 [ALTERNATE_LOCATORS](../part-06-utility-manual/40-glocator.md#13cbee08541c5e65)가 추가되었다.

<a id="5943cc15ae3a3616"></a>
##### Argument

Argument에 --[sync](../part-06-utility-manual/40-glocator.md#fd3abd87e565d7f3) 옵션이 추가되었다.

<a id="feeba9c654bc2af3"></a>
#### gagent

<a id="91601d4fd19bfbd9"></a>
##### Configuration

Configuration 키워드로 [ALTERNATE_LOCATORS](../part-06-utility-manual/41-gagent.md#9471172b80ce27ec)가 추가되었다.

<a id="f0027f8969aefd39"></a>
#### gloctl

<a id="8172c93e7d1a8cc0"></a>
##### Configuration

gloctl의 구동 환경을 설정하는 [Configuration](../part-06-utility-manual/42-gloctl.md#56f751499f970703) 파일이 추가되었다.

Configuration 파일을 지정하는 [conf](../part-06-utility-manual/42-gloctl.md#976974a6e39954d8) option이 추가되었다.

<a id="7fec4ef1be0d05d2"></a>
##### --dsn

gloctl을 구동할 때 dsn 옵션이 제거되었다.

<a id="bbfc006fa7b6bd8e"></a>
### Replication

<a id="ec13d1bae91224e3"></a>
#### cyclone

[Recovery](../part-07-replication/44-cyclone.md#95fdc83c4d5e5955) 기능이 추가되었다.

[Cluster 환경에서 CYCLONE 운영](../part-07-replication/44-cyclone.md#1a4fd460e06f9573) 기능이 추가되었다.

Slave를 지원하는 database가 GOLDILOCKS 이외에 [ORACLE_DRIVER](../part-07-replication/44-cyclone.md#f7f770d51be300ce)를 지원한다.

Standalone의 [실행 옵션](../part-07-replication/44-cyclone.md#47901f6c3d9e7b15)이 추가되었다.

Local [실행 옵션](../part-07-replication/44-cyclone.md#47901f6c3d9e7b15)이 추가되었다.

<a id="6bb141c28b084a75"></a>
#### logmirror

변동 사항 없음

<a id="f8e6a1f44f9ac171"></a>
#### cymon

변동 사항 없음

<a id="68fce9cae10ca45f"></a>
## Patch Notes

<a id="82f302e1705e7073"></a>
### 3.2.14 Patch Note

<a id="1bcdee80b9d4896a"></a>
#### <kbd>ISSUE-6253</kbd> Large page 를 사용하는 공유 메모리 할당에 실패할 경우 normal page를 사용할 수 있는 property를 지원한다.

<a id="87ab4720dd4f82df"></a>
##### 개요

공유 메모리를 할당할 때 normal page와 large page를 사용할 수 있도록 하고, large page를 이용한 공유 메모리 할당에 실패하는 경우 normal page를 이용하여 공유 메모리를 할당할 수 있는 [USE_LARGE_PAGES](../part-02-administration-manual/10-server-property.md#4f5b19b609458ab0) property를 지원한다.

<a id="aee619c9df8ba734"></a>
##### 수정 전 대처

없음

<a id="b129648b38333986"></a>
### 3.2.13 Patch Note

<a id="583a50cfe3b3c134"></a>
#### <kbd>ISSUE-5862</kbd> JDBC, Multi-thread 프로그램에서 Connection 객체를 공유할 때 deadlock 현상이 발생한다.

<a id="557c6229daf6b2ad"></a>
##### 개요

Multi-thread 프로그램에서 Connection 객체를 공유하여 사용하면 deadlock이 발생한다.

<a id="ee3fae913d80aa1e"></a>
##### 수정 전 대처

Thread 별로 Connection 객체를 별도로 생성해서 사용한다.

<a id="d3c294250ffa7af0"></a>
### 3.2.12 Patch Note

<a id="cc8563966dba9450"></a>
#### <kbd>ISSUE-4362</kbd> Cluster에서 cserver가 free 된 메모리를 참조하여 비정상적으로 종료되었다.

<a id="0b1095cc8c632b45"></a>
##### 개요

Cluster에서 원격 멤버가 dml을 수행할 때 cserver 세션에서 사용한 메모리를 free 한 후에 다른 dml을 수행할 경우 free 된 메모리를 이용하는 버그로 인해 비정상적으로 종료되는 문제가 있어 이를 수정하였다.

<a id="203e1aadfdaafd8c"></a>
### 3.2.11 Patch Note

<a id="6b231b0c4871fe2b"></a>
#### <kbd>ISSUE-3869</kbd> ODBC에서 array fetch 할 때 row status의 결과가 잘못되었다.

<a id="2d731ed5268746fc"></a>
##### 개요

ODBC에서 array fetch 할 때 SQLFetch 함수를 호출한 후에 row의 status 값을 확인할 수 있다. 만일 SQLFetch의 반환값이 SQL_SUCCESS가 아닐 경우에는 row status나 diagnostic을 확인해야 한다.   
하지만 SQLFetch의 반환값이 SQL_SUCCESS_WITH_INFO인 상황에서 diagnostic 메시지는 조회할 수 있지만 row의 status는 모두 SQL_ROW_SUCCESS라고 잘못 나온다.

<a id="7d9807992cc2673f"></a>
##### 현상 및 증상

다음은 숫자로 변환하지 못하는 문자열 데이터이다.

```
CREATE TABLE T1 ( I1 VARCHAR(10) );
INSERT INTO T1 VALUES ( '1' );
INSERT INTO T1 VALUES ( '2A' );
INSERT INTO T1 VALUES ( '3' );
INSERT INTO T1 VALUES ( 'AB' );
COMMIT;
```

다음은 위 데이터를 숫자 타입으로 변환해서 array fetch하는 예제의 일부이다.

```
sRet = SQLPrepare( sStmt,
                   (SQLCHAR*)"SELECT I1 FROM T1 ORDER BY I1",
                   SQL_NTS );

sRet = SQLBindCol( sStmt,
                   1,
                   SQL_C_LONG,
                   sI1,
                   sizeof(SQLINTEGER),
                   sI1Ind );

sRet = SQLSetStmtAttr( sStmt,
                       SQL_ATTR_ROW_BIND_TYPE,
                       (SQLPOINTER)SQL_BIND_BY_COLUMN,
                       0 );

sRet = SQLSetStmtAttr( sStmt,
                       SQL_ATTR_ROW_STATUS_PTR,
                       sRowStatus,
                       0 );

sRet = SQLExecute( sStmt );

sRet = SQLFetch( sStmt );

switch( sRet )
{
    case SQL_SUCCESS_WITH_INFO:
        for( i = 0; i < sFetched; i++ )
            printf( "row status: %d\n", sRowStatus[i]);
        break;
    default
        break;
}
```

숫자로 변환하지 못하는 데이터가 포함되어 있지만 row status가 모두 SQL_ROW_SUCCESS라고 나온다.

```
row status: 0
row status: 0
row status: 0
row status: 0
```

<a id="1ea3916cc2ae1e02"></a>
##### 수정 전 대처

없음

<a id="c3796af1acc02416"></a>
#### <kbd>ISSUE-3534</kbd> Cluster failover를 처리하는 과정에서 gagent가 서버를 shutdown하지 않고 서버가 스스로 종료되도록 변경하였다.

<a id="6de8f8daa77052da"></a>
##### 개요

Cluster failover를 처리하는 과정에서 gagent가 non-viability 라는 결과를 수신할 경우, 기존에는 gagent가 SHUTDOWN ABORT를 실행하여 서버를 종료하였다. 그러나 gagent가 서버를 shutdown하지 않고 서버가 스스로 종료되도록 변경하였다.

<a id="06cff0e237b59121"></a>
#### <kbd>ISSUE-3534</kbd> Cluster failover를 처리하는 과정에서 glocator가 질의를 요청한 gagent로만 결과를 전송하도록 변경하였다.

<a id="78b4df14a497f68d"></a>
##### 개요

Cluster failover를 처리하는 과정에서 glocator는 질의를 요청한 gagent 뿐만 아니라 failover 대상인 gagent에도 failover 결과를 보낸다. 그러나 이 경우, failover 대상인 gagent도 glocator에게 질의를 보내어 cluster failover를 처리하게 된다. 따라서 glocator가 질의를 요청한 gagent에게만 결과를 보내도록 변경하였다.

<a id="0a2e4a2ac79394e0"></a>
#### <kbd>ISSUE-3314</kbd> JDBC, CallableStatement의 메소드인 registerOutParameter(), set..()이 동일한 파라미터에 사용되면 정상적인 값을 얻을 수 없다.

<a id="44057ee923a8866e"></a>
##### 개요

CallableStatement를 이용하여 bind type이 명확하지 않은 procedure를 호출하여 out parameter의 값을 얻으려고 할 때, registerOutParameter() 메소드와 set...() 메소드를 이용하여 bind type을 INPUT OUTPUT으로 설정한다. 그리고 out parameter의 결과값을 얻기 위해 get...() 메소드를 호출하면 정상적인 값을 반환하지 않는다.

<a id="ed878306daba90fe"></a>
##### 현상 및 증상

다음과 같이 table과 procedure를 생성한다.

```
CREATE TABLE PROC_TABLE ( I1 INTEGER );

INSERT INTO PROC_TABLE VALUES ( 1 );
INSERT INTO PROC_TABLE VALUES ( 2 );
INSERT INTO PROC_TABLE VALUES ( 3 );
INSERT INTO PROC_TABLE VALUES ( 4 );
INSERT INTO PROC_TABLE VALUES ( 5 );
INSERT INTO PROC_TABLE VALUES ( 6 );

COMMIT;

CREATE OR REPLACE PROCEDURE PROC_TEST_1( A1 INTEGER, A2 OUT INTEGER )
  IS
  BEGIN
    SELECT COUNT(*)
      INTO A2
      FROM PROC_TABLE
      WHERE I1 >= A1;
  END;
/
```

다음은 procedure PROC_TEST_1을 gsql에서 호출한 결과이다. 결과값은 두 번째 parameter의 out value에 저장된다.

```
gSQL> var v1 integer     
gSQL> var v2 integer
gSQL> exec :v1 := 1
gSQL> call proc_test_1 (:v1,:v2);

Procedure Call complete.

gSQL> print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                     1
V2                     6

gSQL>
```

다음은 procedure PROC_TEST_1을 호출하는 프로그램 코드의 일부이다.

```
CallableStatement sCstmt = aCon.prepareCall( "CALL PROC_TEST_1( ?, ? )" );

sCstmt.setInt( 1, 1 );
sCstmt.setInt( 2, 1 );
sCstmt.registerOutParameter( 1, Types.INTEGER );
sCstmt.registerOutParameter( 2, Types.INTEGER );

sCstmt.execute();

System.out.println("OUTPUT: " + sCstmt.getInt(1) + ", " + sCstmt.getInt(2) );

sCstmt.close();
```

해당 프로그램을 실행하면 다음과 같이 out parameter 값이 두 번째 parameter가 아닌 첫 번째 parameter에 저장된다.

```
OUTPUT: 6, 0
```

<a id="63de8cf8ea133c20"></a>
##### 수정 전 대처

다음과 같이 input, output 타입을 정확하게 확인하여 위와 같은 set 메소드와 registerOutParameter 메소드를 모두 사용하지 말아야 정상적인 값이 출력된다.

```
CallableStatement sCstmt = aCon.prepareCall( "CALL PROC_TEST_1( ?, ? )" );

sCstmt.setInt( 1, 1 );
sCstmt.registerOutParameter( 2, Types.INTEGER );

sCstmt.execute();

System.out.println("OUTPUT: " + sCstmt.getInt(1) + ", " + sCstmt.getInt(2) );
sCstmt.close();
```

```
OUTPUT: 1, 6
```

<a id="024ae9914ca383e0"></a>
#### <kbd>ISSUE-3302</kbd> JDBC, CallableStatement의 메소드인 getBytes() 메소드를 실행하면 에러가 발생한다.

<a id="dcb079069fa884b2"></a>
##### 개요

CallableStatement에서 out parameter의 타입이 BINARY, VARBINARY 또는 LONG VARBINARY인 경우 getBytes() 메소드를 사용하면 에러가 발생한다.

<a id="a77519cd1625b777"></a>
##### 현상 및 증상

다음은 CallableStatement에 Types.BINARY로 out parameter를 등록하는 예이다.

```
CallableStatement sCStmt = aCon.prepareCall( "BEGIN ? := x'aaff'; END; " );
sCStmt.registerOutParameter(1, java.sql.Types.BINARY);
sCStmt.executeUpdate();
byte[] sValue = sCStmt.getBytes(1);
```

위의 코드를 포함한 프로그램을 실행하면 다음과 같은 에러가 발생한다.

```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: -1
	at indep.jdbc.dt.RowCache.readBytes(RowCache.java:637)
	at indep.jdbc.dt.Column.getBytes(Column.java:589)
	at indep.jdbc.core.JdbcCallableStatement.getBytes(JdbcCallableStatement.java:316)
```

<a id="110057a63d46812f"></a>
##### 수정 전 대처

없음

<a id="6e0ee41d296cd745"></a>
#### gloader의 명령 인자로 --group-id를 추가하였다.

<a id="008a11be6078078d"></a>
##### 개요

[--group-id](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#e2e635e5daf1d03c) 인자는 클러스터 환경에서 sharded 테이블에 그룹별로 데이터를 업로드 할 수 있도록 한다.

<a id="1cf66fee898b2931"></a>
#### gloader의 명령 인자로 --directio-size를 추가하였다.

<a id="bd0b4234fdb81e37"></a>
##### 개요

[--directio-size](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#504b5b9377ee61e0) 인자를 이용하여 direct IO 크기를 조절할 수 있다.

<a id="288705a83f2c67f8"></a>
### 3.2.10 Patch Note

<a id="16d4e29cc6bf7e64"></a>
#### <kbd>ISSUE-3253</kbd> 서비스 도중에 오프라인 테이블스페이스를 복구하면 로그버퍼에 기록된 로그를 복구하지 않는 문제가 있다.

<a id="cae0832eb06394e4"></a>
##### 개요

GOLDILOCKS의 오프라인 테이블스페이스를 온라인으로 변경할 때 복구가 필요한 경우가 있고 그렇지 않은 경우도 있다. 복구가 필요한 경우는 오프라인 구문에서 IMMEDIATE 옵션을 사용하였거나, 운영 중에 데이터 파일에 문제가 발생하여 해당 테이블스페이스가 오프라인 된 경우이다. 이 경우, 해당 테이블스페이스에 대한 로그가 버퍼에 남아있을 수 있는데 로그 파일에 기록된 로그만으로 복구를 수행하여 시스템이 비정상 종료하거나 데이터베이스 일관성이 어긋나는 문제가 발생하였다.

<a id="6753ddf282076d40"></a>
##### 현상 및 증상

사용자가 생성한 테이블스페이스에 테이블 T1을 생성한 후 트랜잭션 TX1이 T1을 갱신하는 도중에 데이터 파일을 삭제하고 체크포인트를 발생시킨다. 체크포인트를 수행할 때 데이터 파일이 존재하지 않으면 해당 테이블스페이스를 오프라인으로 변경하고 이후 트랜잭션 TX1을 rollback한다. 그리고 로그버퍼의 로그가 디스크로 씌여지지 않은 상태에서 오프라인 된 테이블스페이스를 복구하고 온라인으로 변경하면 비정상적으로 종료된다.

<a id="ec17d740fc212ce6"></a>
##### 수정 전 대처

없음

<a id="ec47f51ad1c1363f"></a>
#### <kbd>ISSUE-3222</kbd> Cluster 환경에서 GOLDILOCKS 시스템 프로세스가 hangup 상태일 때 시스템 전체가 멈춘다.

<a id="c85e8377bd198142"></a>
##### 개요

Cluster 환경에서 원격 cluster member에 protocol을 전송한 후 응답을 기다릴 때, 원격 cluster member의 GOLDILOCKS 시스템 프로세스가 hangup 상태여서 응답을 보내주지 못하는 경우 응답을 기다리는 세션 뿐만 아니라 전체 시스템이 멈추는 현상이 발생한다. 이는 GOLDILOCKS 내부적으로 응답을 반드시 받아야만 하는 protocol에 대해 query timeout 이나 session 상태를 체크하지 않기 때문에 나타나는 현상이다. 이에, 특정 시간동안 응답이 없는 경우 세션을 종료시키거나 응답이 없는 원격 cluster member를 failover 시킨 후에 서비스를 진행하도록 수정하였다.

세션을 종료시키는 정책을 사용할 경우, [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](../part-02-administration-manual/10-server-property.md#d21aab50c1233764)에 설정된 시간(초) 동안 대기한 후에 세션을 종료시킨다. 반면에 failover 하는 정책을 사용할 경우, [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](../part-02-administration-manual/10-server-property.md#c153389143e691b5) 에 설정된 시간 (초) 만큼 대기한 후 응답이 없는 원격 cluster member를 failover 시킨다.

<a id="ee62ea48f1f8c3fe"></a>
##### 현상 및 증상

G1N1, G1N2로 구성된 1 by 2 cluster에서 G1N2 member의 commit 서버를 hangup 상태로 만든 후 G1N1에 접속한 세션에서 commit을 실행하면 세션이 응답을 받지 못하여 멈추게 된다.

G1N2 member의 gmaster를 hangup 상태로 만든 후 G1N1에 접속한 세션에서 *ALTER SYSTEM SWITCH LOGFILE*을 수행하면 세션이 응답을 받지 못하여 멈추게 된다.

<a id="beeddad4e2622444"></a>
##### 수정 전 대처

없음

<a id="eb0d1a24cd103293"></a>
#### <kbd>ISSUE-3175</kbd> gpec이 #define 구문에서 주석을 처리하지 못한다.

<a id="d5d82ff459eab312"></a>
##### 개요

#define 구문에 주석이 있는 경우 gpec이 이를 처리하지 못한다.

<a id="f5b8f9ba86ec6823"></a>
##### 현상 및 증상

다음 gc 파일의 매크로 AA는 1로 동일한 내용이어야 한다. 하지만 gpec이 매크로에 있는 주석을 처리하지 못하여 다른 내용으로 처리하고 있다. gpec이 다음 gc 파일을 처리하면 경고 메시지를 출력한다.

```
#define AA 1 /* comment */
#define AA 1
```

```
ERR-42000(41028): 'AA' macro is already defined at line 3, in file test.gc
```

<a id="9c35072414ee78b0"></a>
##### 수정 전 대처

없음

<a id="199948c0ae6c8788"></a>
#### <kbd>ISSUE-3175</kbd> gpec이 #if, #else에서 define 구문을 정상적으로 처리하지 못한다.

<a id="f1040ebb8fd97b57"></a>
##### 개요

#if와 #endif 또는 #else와 #endif 사이에 #define을 사용할 경우, gpec이 이를 정상적으로 처리하지 못한다.

<a id="e5dee97849d8a52c"></a>
##### 현상 및 증상

#if와 #endif 또는 #else와 #endif 사이에 false 조건에 속한 #define이 있을 경우 gpec이 이를 처리하지 않아야 함에도 불구하고 처리하고 있다.

다음과 같은 gc 파일이 있을 때 gpec은 false 조건에 해당하는 *#define AA 2*를 처리하지 않아야 한다. 그러나 실제로는 이를 무시하지 않고 처리하여 에러를 발생시킨다.

```
#if 1
#define AA 1
#else
#define AA 2
#endif
```

```
ERR-42000(41028): 'AA' macro is already defined at line 4, in file test.gc
```

<a id="8f9a752a11086330"></a>
##### 수정 전 대처

없음

<a id="d51ea19bf6acac87"></a>
#### <kbd>ISSUE-3175</kbd> gpec이 처리하는 #define 구문의 개수가 고정되어 있다.

<a id="08c2189bf3086fa7"></a>
##### 개요

gpec이 관리하는 #define 구문이 256 개로 고정되어 있으며 256 개를 초과하면 에러가 발생한다.

<a id="970055aaa7a43f3b"></a>
##### 현상 및 증상

gc 파일에 서로 다른 #define 구문이 256 개를 넘으면 다음과 같은 에러가 발생한다.

```
ERR-42000(41000): syntax error at line 258, in file test.gc
ERR-42000(41027): too many 'define' macro (256)
```

<a id="5889bbfc8833a4c0"></a>
##### 수정 전 대처

없음

<a id="cfd70007d86ab030"></a>
#### <kbd>ISSUE-3175</kbd> gpec이 비어있는 브라켓 주석을 정상적으로 처리하지 못한다.

<a id="f7c0c9f8263b0dd9"></a>
##### 개요

*/**/* 와 같이 내용 없이 비어있는 브라켓 주석 다음에 임의의 내용이 있는 브라켓 주석이 존재할 경우 gpec이 정상적으로 파싱하지 못한다.

<a id="1f4ccf1df37679b9"></a>
##### 현상 및 증상

다음은 빈 브라켓 주석과 일반적인 브라켓 주석이 함께 사용된 gc 파일이다.

```
/**/
EXEC SQL BEGIN DECLARE SECTION;
int  value;
EXEC SQL END DECLARE SECTION;  

/* comment */

EXEC SQL SELECT 1 INTO :value FROM DUAL;
```

이 gc 파일을 gpec이 파싱하면 도중에 다음과 같은 에러가 발생한다.

```
ERR-42000(41000): syntax error at line 8, in file a.gc: 
SELECT 1 INTO :value FROM DUAL;
                     ^  ^
Error at line 1
ERR-42000(41002): Host variable "value" not declared

ERR-42000(41006): Fatal error while doing embedded SQL precompiling
```

<a id="214e2784e4dbcb3d"></a>
##### 수정 전 대처

빈 브라켓 주석을 사용하지 않는다.

<a id="6c0636ef74df1c2f"></a>
#### <kbd>ISSUE-3243</kbd> glsnr이 잘못된 프로토콜을 받으면 종료된다.

<a id="546726464f293e98"></a>
##### 개요

glsnr이 잘못된 프로토콜을 받으면 종료되어 버리는 문제를 수정하였다. 수정 후 다음과 같은 로그 메세지를 출력하지만 glsnr이 종료되지는 않는다.

```
2020-01-15 17:57:51.835036 THREAD(27742,139777341413120)] 
[LISTENER] Invalid communication protocol : 192.168.0.123
```

<a id="a9613ca7424cf91e"></a>
##### 현상 및 증상

glsnr이 잘못된 프로토콜을 받을 경우 다음과 같은 로그 메세지를 남기며 종료된다.

```
[2020-01-15 11:14:28.738666 THREAD(5706,140285308184384)]
[LISTENER] abnormally terminated
ERR-08S01(24001): Invalid communication protocol
```

<a id="f6d9531911a94374"></a>
##### 수정 전 대처

없음

<a id="2ccf04428c623124"></a>
#### <kbd>ISSUE-3174</kbd> ODBC 속성에 LOCALITY_GROUP_POLICY, LOCALITY_GROUP_PATH, LOCALITY_MEMBER_POLICY, LOCALITY_MEMBER_PATH 항목을 추가하였다.

<a id="b91e876d1cdf608e"></a>
##### 개요

ODBC 속성에 다음 항목들을 추가하였다.

- LOCALITY_GROUP_POLICY
- LOCALITY_GROUP_PATH
- LOCALITY_MEMBER_POLICY
- LOCALITY_MEMBER_PATH

<a id="d85e0afc8f2df573"></a>
#### <kbd>ISSUE-3220</kbd> 세 개 이상의 join에 대해 다수의 subquery 조건이 존재하면 일부 subquery 조건이 누락되었다.

<a id="005ff4efb1e2d182"></a>
##### 개요

세 개 이상의 table을  join 할 때 두 개 이상의 subquery 조건이 존재할 경우 subquery 조건을 처리할 위치를 결정 (push-down subquery filter) 한다.  
이 때, 첫 번째 subquery 조건을 가장 하위의 table에 배치하고, 두 번째 subquery 조건을 그 상위 join에 배치할 경우, 첫 번째 subquery 조건이 누락된다.

<a id="123817bcd2313937"></a>
##### 현상 및 증상

다음과 같이 table과 data를 생성한다.

```
CREATE TABLE r ( r_c1 INTEGER,
                 r_c2 INTEGER );
COMMIT;

CREATE TABLE s ( s_c1 INTEGER,
                 s_c2 INTEGER );
COMMIT;

CREATE TABLE t ( t_c1 INTEGER,
                 t_c2 INTEGER );
COMMIT;

CREATE TABLE u ( u_c1 INTEGER,
                 u_c2 INTEGER );
COMMIT;

CREATE TABLE v ( v_c1 INTEGER,
                 v_c2 INTEGER );
COMMIT;


INSERT INTO r VALUES ( 1, 1 );
INSERT INTO s VALUES ( 1, 1 );
INSERT INTO t VALUES ( 1, 1 );
INSERT INTO u VALUES ( 1, 1 );
INSERT INTO v VALUES ( 1, 1 );
COMMIT;
```

다음 질의와 같이 EXISTS 조건이 존재할 경우, 조건을 만족하는 결과가 존재하지 않는다.

```
SELECT 
       *
  FROM r,
       s,
       t
 WHERE r_c1 = s_c1
   AND s_c1 = t_c1
   AND EXISTS (
                SELECT u_c1
                  FROM u
                 GROUP BY u_c1
                 HAVING u_c1 < 0
              )
;

no rows selected.
```

그러나 위의 질의에 다음과 같이 AND NOT EXISTS subquery 조건을 추가할 경우, 잘못된 질의 결과를 생성한다.

```
--# wrong result
SELECT 
       *
  FROM r,
       s,
       t
 WHERE r_c1 = s_c1
   AND s_c1 = t_c1
   AND EXISTS (
                SELECT u_c1
                  FROM u
                 GROUP BY u_c1
                 HAVING u_c1 < 0
              )
   AND NOT EXISTS ( SELECT *
                      FROM v
                     WHERE v_c1 = r_c1 + s_c1 )
;

R_C1 R_C2 S_C1 S_C2 T_C1 T_C2
---- ---- ---- ---- ---- ----
   1    1    1    1    1    1

1 row selected.
```

<a id="e9bdc83edd593d57"></a>
##### 수정 전 대처

다음과 같이 NOT EXISTS subquery에 NO_PUSH_SUBQ 힌트를 추가하면 올바른 결과를 얻을 수 있다.

```
SELECT 
       *
  FROM r,
       s,
       t
 WHERE r_c1 = s_c1
   AND s_c1 = t_c1
   AND EXISTS (
                SELECT u_c1
                  FROM u
                 GROUP BY u_c1
                 HAVING u_c1 < 0
              )
   AND NOT EXISTS ( SELECT /*+ NO_PUSH_SUBQ */ *
                      FROM v
                     WHERE v_c1 = r_c1 + s_c1 )
;

no rows selected.
```

<a id="c3a1fdf2da6e3d50"></a>
#### <kbd>ISSUE-3199</kbd> EmbeddedSQL에서 array로 GroupId를 얻을 때 정상적으로 처리하지 못한다.

<a id="0af190eb26b51904"></a>
##### 개요

Array로 GroupId를 얻고 캐시된 SQL 구문을 다시 실행하면 프로그램이 비정상적으로 종료된다.

<a id="a898802ae693407a"></a>
##### 현상 및 증상

```
EXEC SQL BEGIN DECLARE SECTION;
int sGroupId[5];
int sValue[5];
EXEC SQL END DECLARE SECTION;
int i;

for( i = 0; i < 5; i++ ) {
    sValue[i] = i;
}

EXEC SQL GET GROUPID INTO: sGroupId
        INSERT INTO TEST_T1 VALUES( :sValue );

EXEC SQL
        INSERT INTO TEST_T1 VALUES( :sValue );
```

캐시된 INSERT INTO TEST_T1 VALUES( :sValue ) 구문을 다시 수행하면 프로그램이 비정상적으로 종료된다.

<a id="978c5b1cf9e7fbda"></a>
##### 수정 전 대처

Array를 사용하지 않거나 캐시된 SQL 구문을 사용하지 않도록 호스트 변수를 변경한다.

<a id="97e1e8ca3ffa5a1b"></a>
#### <kbd>ISSUE-3197</kbd> gpec이 &lt; ... &gt; 문자열을 정상적으로 처리하지 못한다.

<a id="53e81d35442eaf1a"></a>
##### 개요

gpec이 파싱할 때 &lt; &gt; 가 같은 줄에 있으면 정상적으로 처리되지 않는다.

<a id="0503afeeb933cb55"></a>
##### 현상 및 증상

```
for( i = 0; i < 5; i++ ) { // > COMMENT
    sValue[i] = i;
}
```

&lt; 5; i++ ) { // &gt; 문자열을 정상적으로 처리하지 못하여 gpec을 수행할 때 에러가 발생한다.

<a id="a1c98934fdb12600"></a>
##### 수정 전 대처

다음과 같이 브라켓이나 주석의 위치를 변경하여 gc 파일을 작성한다.

```
for( i = 0; i < 5; i++ ) // > COMMENT
{
    sValue[i] = i;
}
```

```
for( i = 0; i < 5; i++ ) {
// > COMMENT
sValue[i] = i;
}
```

<a id="e7050326c01b51d3"></a>
### 3.2.9 Patch Note

<a id="0b24c4262635dd56"></a>
#### <kbd>ISSUE-3188</kbd> gsql에 set heading을 추가하였다.

<a id="c089389da716f371"></a>
##### 개요

set heading {on|off}를 이용하여 질의 결과에 헤더를 출력할지 여부를 설정할 수 있다.

<a id="5bc1457ff70e0900"></a>
### 3.2.8 Patch Note

<a id="a4b521dac596506d"></a>
#### <kbd>ISSUE-3175</kbd> gpec이 non-ascii 문자를 처리하지 못한다.

<a id="b2e171c73d907da8"></a>
##### 개요

gpec이 처리하는 preprocessor #if, #ifdef, #elif, #else가 false 그룹일 경우, 해당 그룹 안의 내용은 공백으로 바뀐다. 그러나 false 그룹 안의 non-ascii 문자는 공백으로 처리되지 못한다.

<a id="c4bce40d145cbaa1"></a>
##### 현상 및 증상

```
#if 0
    EXEC SQL INSERT INTO TEST_T1 VALUES( :sC1, :sC2 );  -- 주석
#endif
```

위 예제 코드를 gpec으로 처리하면 모두 공백으로 바뀌어야 하지만 non-ascii 문자는 남아 있다.

```
주석
```

<a id="cad528af2c6a58d2"></a>
##### 수정 전 대처

non-ascii 문자를 c 주석 형식으로 처리한다.

<a id="712f804eff109bef"></a>
#### <kbd>ISSUE-2958</kbd> Embedded SQL에서 SQL statement의 group ID를 얻을 수 있다.

<a id="24a5d9196b6e73c8"></a>
##### 개요

Global connection을 사용하는 cluster 환경에서 shard key가 설정된 table을 대상으로 delete/ insert/ select/ update 구문의 group ID를 얻을 수 있다. 자세한 내용은 embedded SQL의 [EXEC SQL GET GROUPID INTO](../part-05-developer-manual/27-embedded-sql.md#49e8f9f9ff6789e5)를 참조한다.

<a id="72e06ccfebf8c08c"></a>
#### <kbd>ISSUE-3186</kbd> 노드 두 개가 동시에 비정상 종료될 경우, failover 과정에서 hang이 발생할 수 있다.

<a id="d1f0527f91530acc"></a>
##### 개요

Domain coordinator 노드와 global coordinator 노드가 동시에 비정상 종료될 경우, failover 과정에서 hang이 발생할 수 있어 이를 수정하였다.

<a id="828f23ccb5f425f8"></a>
##### 현상 및 증상

failover 과정에서 hang이 발생함으로써 비정상 종료된 노드들이 속한 그룹들의 온라인 트랜잭션 서비스가 중지될수 있다.

<a id="189b5ccf385106b5"></a>
##### 수정 전 대처

없음

<a id="8d44f99b12aad80c"></a>
### 3.2.7 Patch Note

<a id="707e15ec81f0bb99"></a>
#### <kbd>ISSUE-3093</kbd> gpec이 preprocessor #define을 파싱하는 중에 에러가 발생한다.

<a id="8aedbf45fd68ba6f"></a>
##### 개요

Preprocessor #define의 대체 문자열에 C의 예약어가 올 경우, 에러가 발생한다.

<a id="84123bc346a8c9bc"></a>
##### 현상 및 증상

```
#define SQLCA_STORAGE_CLASS extern
```

gpec을 수행할 때 파싱 에러가 발생한다.

```
$ gpec test.gc

FileName: test.gc
Pre-compile test.gc -> test.c
ERR-42000(41000): syntax error at line 1, in file test.gc: 
#define SQLCA_STORAGE_CLASS extern
............................^
Error at line 1, in file test.gc
```

<a id="55e193436edf72ab"></a>
##### 수정 전 대처

gpec을 수행하지 않는 일반 헤더 파일에 키워드를 정의하여 사용한다.

<a id="cd29c03d9f355948"></a>
### 3.2.6 Patch Note

<a id="288199bd19ca203a"></a>
#### <kbd>ISSUE-3149</kbd> SELECT INTO 구문에 구조체 배열을 사용하는 파일을 gpec이 정상적으로 파싱하지 못한다.

<a id="5651bccf90878d75"></a>
##### 개요

SELECT INTO 구문에 호스트 변수로 구조체 배열을 사용하는 gc파일을 gpec이 정상적으로 처리하지 못한다.

<a id="fe022b5c40a56a03"></a>
##### 현상 및 증상

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct AA
{
    char c1[10+1];
    char c2[10+1];
    char c3[10+1];
    char c4[10+1];
} AA;
AA sArr[10];
EXEC SQL END DECLARE SECTION;

EXEC SQL SELECT c1,c2,c3, c4
    INTO  :sArr FROM EMP;
STL_TRY(sqlca.sqlcode == 0);
```

위 예제의 SELECT INTO 구문이 다음과 같이 올바르지 못한 구문으로 변경되었다.

```
sqlargs.sqlstmt = (char *)"SELECT c1,c2,c3,c4\n"
"    INTO  :sArr ?, ?FROM EMP\n"
```

<a id="b1260f788d088776"></a>
##### 수정 전 대처

없음

<a id="aefc0401b48acb67"></a>
#### <kbd>ISSUE-3145</kbd> 세션에서 사용 가능한 메모리가 있는데도 새로운 메모리를 할당하여 SSA가 증가한다.

<a id="228f556a3f7da83a"></a>
##### 개요

세션이 시작된 이후에 사용한 메모리는 세션에서 관리하며 재사용될 수 있고, 메모리 단편화를 고려하여 효율적으로 메모리를 할당하기 위해 메모리 크기에 따라 여러 개의 레벨로 관리된다. 사용 후에 해제된 메모리를 재할당하는 과정에서 단편화를 최소화하기 위해 재할당 할 수 있는 메모리가 있음에도 불구하고 새로운 메모리 청크를 할당함으로써 SSA가 지속적으로 증가하는 문제가 있어서 수정하였다.

<a id="804db8d65dd50345"></a>
##### 현상 및 증상

LONG VARBINARY 타입을 포함한 테이블을 조회할 때 V$SYSTEM_MEM_STAT을 살펴보면 VARIABLE_STATIC_ALLOC_SIZE가 지속적으로 증가하는 것을 확인할 수 있다.

```
gSQL> SELECT STAT_NAME, ROUND(STAT_VALUE/1024/1024) FROM V$SYSTEM_MEM_STAT WHERE STAT_NAME = 'VARIABLE_STATIC_ALLOC_SIZE';


STAT_NAME                  ROUND(STAT_VALUE/1024/1024)
-------------------------- ---------------------------
VARIABLE_STATIC_ALLOC_SIZE                     1800.25

1 row selected.


gSQL> SELECT STAT_NAME, ROUND(STAT_VALUE/1024/1024) FROM V$SYSTEM_MEM_STAT WHERE STAT_NAME = 'VARIABLE_STATIC_ALLOC_SIZE';


STAT_NAME                  ROUND(STAT_VALUE/1024/1024)
-------------------------- ---------------------------
VARIABLE_STATIC_ALLOC_SIZE                     3663.41

1 row selected.
```

<a id="df881fe3b17b2594"></a>
##### 수정 전 대처

없음

<a id="6993499315a81d0e"></a>
#### <kbd>ISSUE-3144</kbd> 필드 구분자와 라인 구분자의 첫 문자를 동일하게 사용하면 gloader가 데이터를 정상적으로 import하지 못한다.

<a id="6207a96134c05b35"></a>
##### 개요

필드 구분자와 라인 구분자의 첫 문자를 동일하게 사용하면 데이터가 누락되거나 gloader 프로세스가 비정상적으로 종료된다.

<a id="b6b50ef16b3c95f4"></a>
##### 현상 및 증상

```
>$ cat test.dat
1234^C2^C3456^S
>$ gloader test test -i --tablename TEST --fieldterm ^C --lineterm ^R\n --data test.dat

gSQL> SELECT * FROM TEST
I1   I2 I3     
---- -- -------
1234 C2 3456S

1 row selected.
```

위 예제에서 필드 구분자와 라인 구분자의 첫 문자가 ^로 동일하다. gloader가 import를 수행한 후에column I3의 정상적인 결과값은 3456^S 이 되어야 하지만 실제 결과는 ^ 문자가 누락된 비정상 데이터이다.

<a id="87db73bcd24652db"></a>
##### 수정 전 대처

필드 구분자와 라인 구분자의 첫 문자를 서로 다르게 사용한다.

<a id="c4e28edd627ce4cd"></a>
### 3.2.5 Patch Note

<a id="4d8dc3a99aca677b"></a>
#### <kbd>ISSUE-3093</kbd> #define과 #undef를 declare section 내에 선언해야 gpec이 이를 처리함 또한 #ifdef 와 같은 if group의 false 값에 대한 문장을 공백으로 변경하지 않는다.

<a id="85668fb20fa3126d"></a>
##### 개요

gpec이 declare section 내에 선언된 #define과 #undef를 처리하는 바람에 #if, #ifdef과 같은 if group에서 매크로를 정상적으로 처리하지 못하고 있다. 또한 false 값에 해당하는 if group의 c code를 공백으로 변경하지 않아 c code 또는 SQL statement 중간에 preprocessor를 사용할 수 없다.

<a id="58e84c1ecb6167a6"></a>
##### 현상 및 증상

Preprocessor #define과 #undef를 declare section 내에 선언하지 않으면 gpec이 처리하지 못하여 해당 매크로를 인식하지 못한다. SQL 중간에 if group에 해당하는 preprocessor를 사용하지 못하여 사용자가 같은 내용의 코드를 반복하여 작성해야 한다.

```
#define _DEV_
EXEC SQL BEGIN DECLARE SECTION;
char
#ifdef _DEV_                   ❶
sTrue[10];                     ❷
#else
sFalse[10]; 
#endif
EXEC SQL END DECLARE SECTION;

EXEC SQL SELECT                ❸
#ifdef _DEV_ 
         "true" INTO :sTrue
#else
         "false" INTO :sFalse
#endif
         FROM DUAL;
```

> 1 _DEV_ 가 declare section 밖에 선언되어 false가 된다.  
> 2 Preprocessor가 공백 처리되지 않아 gpec이 파싱 에러 처리한다.  
> 3 SQL 구문 파싱 중에 에러가 발생한다.

<a id="186c59f3aa2fd5af"></a>
##### 수정 전 대처

Preprocessor #define과 #undef를 declare section 내에 선언하여 사용하고, c code와 SQL 구문 중간에 preprocessor를 사용하지 않는다.

<a id="121d052c02557eec"></a>
#### <kbd>ISSUE-3075</kbd> JDBC의 PreparedStatement.setCharactertStream(int, Reader, int) method와 PreparedStatement.addBatch() method를 반복 수행할 때 data type이 변경되어 에러가 발생한다.

<a id="fae082f4f08b731b"></a>
##### 개요

JDBC의 PreparedStatement 클래스 method인 setAsciiStream(), setBinaryStream(), setCharacterStream() method를 수행할 때 기존에는 매개 변수 length로 data type을 결정하였던 것을 long data type만 사용하도록 변경하였다.

<a id="28107b91c640b384"></a>
##### 현상 및 증상

setCharacterStream() method로 VARCHAR 타입이 허용하는 길이의 데이터를 설정한 후에 addBatch() method를 호출하고, setCharacterStream() method로 VARCHAR 타입이 허용하는 길이를 초과하는 데이터를  설정하려고 시도하면 data type이 VARCHAR에서 LONG VARCHAR로 변경되어 에러가 발생한다.

```
gSQL> create table t1 ( i1 long varchar );

Table created.
```

```
sPstmt.setCharacterStream( 1, new StringReader( DATA ), DATA.length() );
sPstmt.addBatch();

sPstmt.setCharacterStream( 2, new StringReader(BIG_DATA), BIG_DATA.length() );
sPstmt.addBatch();
```

```
Caused by: java.sql.SQLException: Parameter type[LONG VARCHAR] is mismatch with previous type[VARCHAR] during batch
```

<a id="11b7237121ee2f08"></a>
##### 수정 전 대처

PrepraredStatement 클래스의 set Ascii/ Binary/ Character Stream() method에는 매개 변수 length가 주어진 method와 length가 없는 method 두 종류가 있다. 이 중에 매개 변수 length가 없는 method를 이용한다.

<a id="ebd0b16659ed0a85"></a>
#### <kbd>ISSUE-3056</kbd> JDBC의 ResultSet.getBoolean()을 수행했을 때 TRUE/ FALSE를 반환하는 문자열이 확장되었다.

<a id="1c1a17645643edd2"></a>
##### 개요

JDBC의 ResultSet.getBoolean()을 수행할 때 기존에는 "true", "false" 문자열만 boolean 타입으로 변환할 수 있었지만 "t", "f", "y", "n", "yes", "no", "on", "off", "1", "0" 문자열도 변환할 수 있도록 변경하였다.

<a id="45f22f49364d12d9"></a>
##### 현상 및 증상

문자열 "0", "1" 을 ResultSet.getBoolean()으로 읽을 경우, 에러가 발생한다.

```
gSQL> create table t1 ( i1 varchar(10) );

Table created.

gSQL> insert into t1 values ( '1' );

1 row created.

gSQL> commit;

Commit complete.
```

```
ResultSet rs = stmt.executeQuery("select * from t1");
        
while(rs.next())
{
    System.out.println( rs.getBoolean(1) );
}
```

```
Exception in thread "main" java.sql.SQLException: The value[1] is out of range of [boolean] type
```

<a id="d711acc2965361ca"></a>
##### 수정 전 대처

없음

<a id="b4af09991cfd48d0"></a>
#### <kbd>ISSUE-3055</kbd> 서버와 클라이언트의 character set이 다른 상태에서 연결할 때 invalid 문자를 전송한다.

<a id="32dbae35b04642bf"></a>
##### 개요

서버와 클라이언트의 character set이 다른 상태에서 연결할 경우 invalid 문자가 전송되는 문제를 수정하였다.

<a id="402cb0b70ae8a83f"></a>
##### 현상 및 증상

리눅스 서버에서 "가" 사용자가 생성된다.

```
gSQL> create user "가" identified by test;

User created.

gSQL> grant create session to "가";

Grant succeeded.

gSQL> commit;

Commit complete.
```

윈도우 클라이언트에서 리눅스 서버로 연결할 때 에러가 발생한다.

```
D:\goldilocks_home\bin>gsqlnet.exe "가" test

ERR-28000(16004): invalid username/password; logon denied
```

리눅스 클라이언트에서 리눅스 서버로 연결할 때는 정상적으로 동작한다.

```
% gsqlnet "가" test

gSQL>
```

<a id="49970f99bf6a5868"></a>
##### 수정 전 대처

서버와 클라이언트의 character set을 동일하게 설정하거나 연결할 때 사용되는 문자열에 ASCII만 포함시키도록 한다.

<a id="de57f44facc1847d"></a>
#### <kbd>ISSUE-2359</kbd> 부모 세션이 없는 cluster peer가 존재한다.

<a id="b044e44bcd4486d5"></a>
##### 개요

원격 노드에 부모 세션이 없는 cluster peer가 존재하는 문제가 발생하여 이를 수정하였다.

<a id="3eebfc6fdf62a4ce"></a>
##### 현상 및 증상

부모 세션이 로그인을 시도하다가 패스워드 변경 과정에서 에러가 발생한 경우, 원격 노드에 부모 세션이 없는 cluster peer가 남아 있을 수 있다.  
패스워드를 변경하는 과정에서 원격 노드에 cluster peer 세션이 만들어질 수 있고 패스워드 변경에 실패하면 cluster peer 세션을 종료하지 않은 상태에서 부모 세션을 종료한다.

<a id="fe125e6b920e4089"></a>
##### 수정 전 대처

없음

<a id="dce8817f74407c1c"></a>
### 3.2.4 Patch Note

<a id="cf29b716afda9df6"></a>
#### <kbd>ISSUE-3026</kbd> gsql에서 `\`ddl_tablespace 수행 시 AT 구문 위치를 수정하였다.

<a id="1dd52826d43cb097"></a>
##### 개요

gsql에서 `\`ddl_tablespace를 수행할 때 AT 구문 위치가 잘못되는 문제를 수정하였다.

<a id="cee8c668fcdb3b5d"></a>
##### 현상 및 증상

`\`ddl_tablespace로 생성된 SQL 구문을 실행할 때 오류가 발생한다.

```
gSQL> create tablespace test_tbs datafile 'test.dbf' size 10m;

Tablespace created.

gSQL> \ddl_tablespace test_tbs

SET SESSION AUTHORIZATION "SYS"; 
CREATE MEMORY DATA TABLESPACE "TEST_TBS" 
    DATAFILE 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        AT "G2N1" 
        SIZE 10485760 REUSE 
      , 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        AT "G2N2" 
        SIZE 10485760 REUSE 
    ONLINE 
    LOGGING 
    EXTSIZE 262144 
;
COMMIT;
```

```
gSQL> CREATE MEMORY DATA TABLESPACE "TEST_TBS" 
    DATAFILE 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        AT "G2N1" 
        SIZE 10485760 REUSE
      , 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        AT "G2N2" 
        SIZE 10485760 REUSE
    ONLINE 
    LOGGING 
    EXTSIZE 262144;

ERR-42000(40000): syntax error: 
        AT "G2N1" 
        ^^
Error at line 4
```

<a id="4da77f637b9ffa17"></a>
##### 수정 전 대처

`\`ddl_tablespace로 생성된 SQL에서 AT 구문 위치를 수정한다.

```
gSQL> CREATE MEMORY DATA TABLESPACE "TEST_TBS" 
    DATAFILE 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        SIZE 10485760 REUSE
        AT "G2N1" 
      , 
        '/home/sunje/goldilocks_data/db/test.dbf' 
        SIZE 10485760 REUSE
        AT "G2N2" 
    ONLINE     LOGGING 
    EXTSIZE 262144;

Tablespace created.
```

<a id="97129cf47259907a"></a>
#### <kbd>ISSUE-3023</kbd> BEGIN BACKUP AT DOMAIN을 사용할 때 오류가 있다.

<a id="fa90f7da61e0dd94"></a>
##### 개요

특정 그룹이나 멤버에서만 백업을 수행하기 위해 AT DOMAIN 절을 사용할 경우, 정상적으로 동작하지 않는 문제가 있어서 이를 수정하였다.

<a id="d7825c51f9487f01"></a>
##### 현상 및 증상

다음과 같이 G1N2 멤버가 ARCHIVELOG로 동작하고 있는데도 BEGIN BACKUP이 실패하는 문제가 있다.

```
gSQL> SELECT ARCHIVELOG_MODE FROM V$ARCHIVELOG;

ARCHIVELOG_MODE
---------------
ARCHIVELOG     

1 row selected.

gSQL> ALTER DATABASE BEGIN BACKUP AT G1N2;

ERR-HY000(16247): MEMBER(G1N1): cannot BACKUP; noarchivelog mode
```

<a id="7e6018ca93e93e0c"></a>
##### 수정 전 대처

AT DOMAIN을 사용하지 않고 BACKUP BEGIN/ END를 수행한다.

<a id="7c30d7d1be620715"></a>
### 3.2.3 Patch Note

<a id="aac3084917ef0bb5"></a>
#### <kbd>ISSUE-3006</kbd> EXPLAIN PLAN ONLY를 수행할 때 트랜잭션이 생성된다.

<a id="850cacadc0e97ec1"></a>
##### 개요

EXPLAIN PLAN ONLY를 수행할 때 트랜잭션이 생성되는 문제를 수정하였다.

<a id="4fdefbef6189a8a1"></a>
##### 현상 및 증상

```
gSQL> select * from x$transaction;

no rows selected.

gSQL> \explain plan only update t2 set c2 = 1 where c1 = 10;


>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  UPDATE STATEMENT                                            |                         |
|    1  |    UPDATE ("T2")                                             |                       0 |
|    2  |      INDEX ACCESS ("T2", "T2_PRIMARY_KEY_INDEX") [CLONED]    |                       0 |
==================================================================================================

     0  -  SQL : UPDATE "PUBLIC"."T2"@LOCAL "_A1" SET("C2")=(:_V0) WHERE "_A1"."C1" = :_V1
     2  -  READ INDEX COLUMNS : C1
             MIN RANGE : C1 = 10
             MAX RANGE : C1 = 10

<<<  end print plan


gSQL> select * from x$transaction;

PHYSICAL_TRANS_ID LOGICAL_TRANS_ID DRIVER_MEMBER_POS DRIVER_MEMBER_ID DRIVER_TRANS_ID SLOT_ID STATE  IS_XA INDOUBT_TRANS_BEHAVIOR ATTRIBUTE ISOLATION_LEVEL VIEW_SCN COMMIT_SCN PREV_COMMIT_SCN TCN BEGIN_LSN USED_UNDO_PAGE_COUNT UNDO_SEGMENT_ID SEQ BEGIN_TIME                 PROPAGATE_LOG REPREPARABLE GRID_SEQ WEIGHT
----------------- ---------------- ----------------- ---------------- --------------- ------- ------ ----- ---------------------- --------- --------------- -------- ---------- --------------- --- --------- -------------------- --------------- --- -------------------------- ------------- ------------ -------- ------
           -65480           458808                 0                1          458808      56 ACTIVE FALSE                      0 READ_ONLY READ COMMITTED  502.1.77 -1.-1.-1   502.0.77          1        -1                    0      4294901760   7 2019-07-02 17:40:13.659857 TRUE          TRUE                7 HIGH  

1 row selected.

gSQL> commit;

Commit complete.

gSQL> select * from x$transaction;

no rows selected.
```

<a id="12987a11d3a905c0"></a>
##### 수정 전 대처

없음

<a id="63ad40723e2de3fe"></a>
### 3.2.2 Patch Note

<a id="5e765e3163068978"></a>
#### <kbd>ISSUE-2947</kbd> Cluster 환경에서 동일한 세션에서 수행한 원격 그룹의 이전 버전 데이터를 조회한다.

<a id="681021dafb19befe"></a>
##### 개요

하나의 세션에서 특정 원격 그룹에서만 변경되는 domain 트랜잭션을 실행한 후 select 할 때 동일한 데이터의 이전 버전을 조회하는 문제를 수정하였다.

<a id="438b6fdd0bcf9775"></a>
##### 현상 및 증상

다음과 같이 G1, G2 클러스터 그룹에서 sharded table을 생성한 후 G1에 위치한 shard에 레코드를 추가한다.

```
gSQL> CREATE TABLE T1 ( C1 NUMBER ) SHARDING BY RANGE ( C1 )
SHARD S1 VALUES LESS THAN ( 1000 ) AT CLUSTER GROUP G1,
SHARD S2 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP G2;

Table created.

gSQL> ALTER TABLE T1 ADD PRIMARY KEY ( C1 );

Table altered.

gSQL> INSERT INTO T1 VALUES ( 1 );

1 row created.

gSQL> COMMIT;

Commit complete.
```

G2 그룹의 member에 접속한 세션 (session 1)에서 G1 그룹의 레코드를 삭제 (트랜잭션 T1)한 후, 다른 세션 (session 2)에서 global 트랜잭션 (트랜잭션 T2)을 수행하고 COMMIT 한다. 이 때 G1 그룹에서 T2가 완료되고, G2 그룹에서는 완료되지 않은 상태에서 T1을 COMMIT 한 다음 다시 G1의 레코드를 조회하면  삭제된 레코드가 조회되는 문제가 있다.

```
gSQL> DELETE FROM T1 WHERE C1 = 1;     // T1  -- session 1

1 row deleted.

gSQL> CREATE TABLE T2 ( I1 INTEGER );  // T2  -- session 2

Table created.

gSQL> COMMIT;                          // -- session 2

Commit complete.

gSQL> COMMIT;                          // -- session 1

Commit complete.

gSQL> SELECT * FROM T1 WHERE C1 = 1;   // -- session 1

C1
--
 1

1 row selected.
```

<a id="ef05927a629789a4"></a>
##### 수정 전 대처

동일한 세션에서 domain 트랜잭션을 수행한 후에 select를 수행할 경우, SELECT 문을 SELECT FOR UPDATE로 대체해서 수행한다.

<a id="20389467e542eb28"></a>
#### <kbd>ISSUE-2965</kbd> JDBC에서 BigDecimal 타입을 parameter로 사용하면 데이터가 손실된다.

<a id="fbf08a6733d9bacd"></a>
##### 개요

Double 타입의 정밀도를 벗어나는 값을 BigDecimal 타입으로 parameter로 사용하면 데이터가 손실되는 문제를 수정하였다.

<a id="fcb0fccedf43e895"></a>
##### 현상 및 증상

사용자의 의도와 다르게 데이터 손실이 발생한다.

```
gSQL> CREATE TABLE T1 ( C1 NUMBER );

Table created.
```

```
PreparedStatement pstmt = con.prepareStatement("INSERT INTO T1 VALUES (?)");
pstmt.setBigDecimal(1, new BigDecimal("12345678901234567890.123456789"));
pstmt.executeUpdate();
```

```
gSQL> select * from t1;

                  C1
--------------------
12345678901234600000

1 row selected.
```

<a id="5f641a0705e2cf9a"></a>
##### 수정 전 대처

BigDecimal 타입 대신 문자열로 처리한다.

```
pstmt.setString(1, "12345678901234567890.123456789");
```

```
gSQL> \set numsize 40
gSQL> select * from t1;

                            C1
------------------------------
12345678901234567890.123456789

1 row selected.
```

<a id="b8fbf6e390bd695d"></a>
#### <kbd>ISSUE-2955</kbd> Cluster 환경에서 gsqlnet이 cstartup 또는 cshutdown을 연속적으로 실행할 수 없다.

<a id="067cdbec1053b6e3"></a>
##### 개요

gsqlnet은 ODBC를 통해 location 파일과 glocator의 접속 정보를 구축한다.  
이 정보는  cstartup이나 cshutdown 명령을 처음으로 수행할 때 구축된다.  
cstartup이나 cshutdown 명령을 두 번째로 수행하면 정보 구축 과정을 무시하는데 이 때 flag 설정이 잘못되어 에러가 발생하였다.

<a id="e9efb4391be79f45"></a>
##### 현상 및 증상

gsqlnet 프로세스에서 cstartup이나 cshutdown을 수행 후 다시 cshutdown 또는 cstartup을 수행하면 에러가 발생한다.

<a id="dcaf2de2f221b791"></a>
##### 수정 전 대처

gsqlnet 세션을 재시작하여 cstartup 또는 cshutdown 명령을 해야 한다.

<a id="f78be1008af9d142"></a>
#### <kbd>ISSUE-2943</kbd> Cluster 환경에서 query timeout 발생 시 agable scn이 증가하지 않는다.

<a id="33b96765fed480c0"></a>
##### 개요

클러스터 환경에서 DML이 async로 처리될 때 원격 멤버들의 view scn 정보를 세션에 설정한다. 이 때 원격 멤버들 중 단 하나에게도 DML을 전송하지 못한 상태에서 query timeout과 같은 예외 상황이 발생하면 세션에 설정된 원격 멤버들의 view scn 정보가 초기화 되지 않는 버그가 있었다. 이로 인해 시스템에 수행 중인 statement가 없는데도 해당 세션이 연결되어 있는 동안 시스템의 agable scn이 증가하지 않는 문제가 있었다.

Async 처리에 예외 상황이 발생하면 원격 멤버들의 view scn 정보를 초기화하여 문제가 발생하지 않도록 수정하였다.

<a id="4b22484fb702482a"></a>
##### 현상 및 증상

클러스터 환경에서 query timeout이 발생한 후에 agable scn이 멈추게 되어 undo, data 공간이 부족해진다.

<a id="5d2384040351630a"></a>
##### 수정 전 대처

Query timeout이 발생한 세션을 종료한다.

<a id="acb73ea93d84bb61"></a>
#### <kbd>ISSUE-2927</kbd> 트랜잭션 슬롯 부족으로 인해 deadlock이 발생한다.

<a id="66777466f9e51814"></a>
##### 개요

트랜잭션 슬롯이 부족한 상황에서 모든 서버 프로세스들이 트랜잭션 슬롯을 할당하는 경우 기존 트랜잭션들이 슬롯을 해제하지 않으면 hang이 발생할 수 있다. 이 경우 정해진 시간이 경과하면 해당 패치에 에러가 발생하도록 수정하였다.

<a id="1637028613b107f1"></a>
##### 현상 및 증상

동시에 여러 세션에서 transaction이 발생할 때 transaction slot이 부족하여 hang이 발생한다.

<a id="1f008a8a4e33cc5f"></a>
##### 수정 전 대처

없음

<a id="83d84fc134c01f40"></a>
#### <kbd>ISSUE-2922</kbd> ODBC의 statement 속성에 SQL_ATTR_FETCH_FAILOVER를 추가하였다.

<a id="48dc592bd5b06bc2"></a>
##### 개요

ODBC의 statement 속성에 SQL_ATTR_FETCH_FAILOVER를 추가하였으며 다음과 같은 값을 설정할 수 있다.

- SQL_FETCH_FAILOVER_OFF
- SQL_FETCH_FAILOVER_ON

```
SQLSetStmtAttr( stmt, 
                SQL_ATTR_FETCH_FAILOVER,
                (SQLPOINTER)SQL_FETCH_FAILOVER_ON,
                0 )
```

<a id="74d89c64f1df94f9"></a>
##### 현상 및 증상

없음

<a id="1deac025b3f6f6cc"></a>
##### 수정 전 대처

없음

<a id="0ca5ea55b3cf9ec6"></a>
#### <kbd>ISSUE-2513</kbd> EXEC SQL AT :sConn DISCONNECT에서 VARCHAR 타입을 인식하지 못한다.

<a id="952ecf48f1556a11"></a>
##### 개요

gpec이 EXEC SQL AT 절에서 VARCHAR 타입을 char 타입으로 인식한다.

<a id="ce6692f8c6b0200e"></a>
##### 현상 및 증상

VARCHAR 타입 변수를 EXEC SQL AT 절에 사용했을 때 gpec이 VARCHAR 타입이 아닌 char 타입으로 처리한다.

- Example gc file

```
EXEC SQL BEGIN DECLARE SECTION;
VARCHAR sAT[20];
EXEC SQL END DECLARE SECTION;

EXEC SQL AT :sAT DISCONNECT;
```

- Example c file generated by gpec

```
sqlargs.conn = (char *)sAT;
sqlargs.sql_ca = &sqlca;
sqlargs.sql_state = SQLSTATE;
sqlargs.sqltype = 35;
sqlargs.sqlfn = (char *)__FILE__;
sqlargs.sqlln = __LINE__;
sqlargs.sqlstmt = NULL;
sqlargs.atomic = 0;
sqlargs.unsafenull = 0;
sqlargs.iters = 0;
DBESQL_Disconnect(NULL, &sqlargs, NULL, 0);
```

VARCHAR 타입을 char * 타입으로 처리하여 gpec이 생성한 c 파일을 컴파일하는 과정에서 에러가 발생한다.

<a id="0f90de32aae84555"></a>
##### 수정 전 대처

VARCHAR 타입 대신 char 타입을 사용한다.

<a id="744be36999880a20"></a>
#### <kbd>ISSUE-2349</kbd> gpec이 전처리기를 처리하는 경우 __LINE__ 매크로가 잘못된 라인을 가리킨다.

<a id="290e07d60c5079ca"></a>
##### 개요

gpec이 #if와 같은 전처리기를 처리할 때 __LINE__ 매크로가 잘못된 라인을 가리킨다.

<a id="fa07d93d3638d5a4"></a>
##### 현상 및 증상

gpec이 #if, #ifdef, #ifndef, #else, #elif 전처리기를 처리할 때 주석을 추가하면서 원래 의도하였던 __LINE__ 매크로 값이 아닌 잘못된 값이 도출된다.

- Example gc file

```
#if 0
    printf("[%s:%d] if\n", __FILE__, __LINE__);
#else
    printf("[%s:%d] else\n", __FILE__, __LINE__);
#endif
    printf("[%s:%d] endif\n", __FILE__, __LINE__);
```

gpec이 해당 코드를 처리한 결과는 다음과 같다.

- Example c file generated by gpec

```
#if 0
/*Macro condition FALSE*/
    printf("[%s:%d] if\n", __FILE__, __LINE__);
#else
/*Macro condition TRUE*/
    printf("[%s:%d] else\n", __FILE__, __LINE__);
#endif
    printf("[%s:%d] endif\n", __FILE__, __LINE__);
```

gpec이 생성한 c 파일을 실행하면 의도하지 않은 라인이 출력된다.

```
$ ./pp_bug
[pp_bug.gc:9] else
[pp_bug.gc:11] endif
```

정상적인 __LINE__ 매크로 값은 다음과 같다.

```
$ ./pp_bug
[pp_bug.gc:7] else
[pp_bug.gc:9] endif
```

<a id="ba71cd53470aa34a"></a>
##### 수정 전 대처

없음

<a id="d199069ee191d6e7"></a>
### 3.2.1 Patch Note

<a id="a2e15b8d8d295824"></a>
#### <kbd>ISSUE-2902</kbd> Cluster 환경에서 global sequence 값을 참조할 때 deadlock이 발생한다.

<a id="c647858a5a964dce"></a>
##### 개요

Cluster 환경에서 global sequence 값 참조 시 local member에 캐싱된 값이 고갈되어 다음 값을 구하기 위해 모든 cluster member 들에 global sequence latch를 잡아야 하는데, 이 과정에서 deadlock 이 발생하여 수정하였다.

<a id="92d692406a9bfa32"></a>
##### 현상 및 증상

동시에 여러 세션에서 global sequence 값을 참조하는 statement를 반복해서 수행할 때 deadlock으로 인해 hang이 발생한다.

<a id="98d4649f95a70838"></a>
##### 수정 전 대처

없음

---

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
