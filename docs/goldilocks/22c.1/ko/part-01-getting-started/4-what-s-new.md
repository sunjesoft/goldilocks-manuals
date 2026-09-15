<a id="312106e542a48c14"></a>

# 4. What's New

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/312106e542a48c14)  
> 태그: `22c.1_10_tag`

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<a id="ea3cb6e5df19a546"></a>
## Feature Matrix

본 장에서는 각 major version 별로 추가된 주요 기능들에 대해 간략히 설명한다.

<a id="a261e3a55f19bb1c"></a>
### Architecture

<a id="b9e33a5d39549ce0"></a>
#### System Architecture

System architecture에 대한 feature matrix는 다음과 같다.

**System architecture의 feature matrix**

<a id="39121c88be45393a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| Shared Nothing Cluster | X | O | O | O | O |
| DA (Direct Attach) | O | O | O | O | O |
| JDBC DA (Direct Attach) | X | O | O | O | O |
| C/S (Client/Server) Dedicated | O | O | O | O | O |
| C/S (Client/Server) Shared | O | O | O | O | O |
| multi-process applications | O | O | O | O | O |
| multi-threaded applications | O | O | O | O | O |
| Linux platform | O | O | O | O | O |
| HP platform | O | O | O | O | O |
| AIX platform | O | O | O | O | O |
| Windows Client Platform | O | O | O | O | O |
| CDC(Change Data Capture) replication | O | O | O | O | O |
| CDC replication with log mirror | O | O | O | O | O |
| multi-level start up | O | O | O | O | O |
| parallel database loading | O | O | O | O | O |
| parallel index build | O | O | O | O | O |
| SQL plan cache | O | O | O | O | O |
| IPC | X | X | X | O | O |

<a id="147cff1ad5749ca7"></a>
#### Storage Internal

Storage internal에 대한 feature matrix는 다음과 같다.

**Storage internal의 feature matrix**

<a id="0a35a99d8d9f7756"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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
| global secondary index | X | O | O | O | O |
| disk data tablespace | X | X | O | O | O |
| disk bitmap data segment | X | X | O | O | O |
| disk B-tree index | X | X | O | O | O |
| disk global secondary index | X | X | O | O | O |

<a id="6a3401a0219e58a6"></a>
#### Transaction Control

Transaction control에 대한 feature matrix는 다음과 같다.

**Transaction control의 feature matrix**

<a id="4bde1666ec0d1c32"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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

<a id="0d59fcca7a587ae5"></a>
#### Backup & Recovery

Backup & recovery에 대한 feature matrix는 다음과 같다.

**Backup & recovery의 feature matrix**

<a id="387f2a77399c455a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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
| change tracking | X | X | O | O | O |

<a id="3b6ba43f4727e511"></a>
#### Database Information

<a id="0bf6b1e391551160"></a>
##### DICTIONARY_SCHEMA 스키마

DICTIONARY_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

<a id="a29f93233c4a7c20"></a>
<table class="table column_count_7"><caption>DICTIONARY_SCHEMA schema의 feature matrix</caption><thead><tr><th class="to_center"><div>계열</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="56"><div>ALL_ 계열 view</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="48"><div>DBA_ 계열 view</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="53"><div>USER_ 계열 view</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="15"><div>기타 view</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="2eeb0574c0c17a7c"></a>
##### INFORMATION_SCHEMA 스키마

INFORMATION_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**INFORMATION_SCHEMA schema의 feature matrix**

<a id="90c0671043eda4d9"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| COLUMNS | O | O | O | O | O |
| COLUMN_PRIVILEGES | O | O | O | O | O |
| CONSTRAINT_COLUMN_USAGE | O | O | O | O | O |
| CONSTRAINT_TABLE_USAGE | O | O | O | O | O |
| INFORMATION_SCHEMA_CATALOG_NAME | O | O | O | O | O |
| KEY_COLUMN_USAGE | O | O | O | O | O |
| MODULES | X | X | O | O | O |
| MODULE_BODY | X | X | O | O | O |
| MODULE_BODY_MODULE_USAGE | X | X | O | O | O |
| MODULE_BODY_ROUTINE_USAGE | X | X | O | O | O |
| MODULE_BODY_SEQUENCE_USAGE | X | X | O | O | O |
| MODULEBODY_TABLE_USAGE | X | X | O | O | O |
| MODULE_MODULE_USAGE | X | X | O | O | O |
| MODULE_PRIVILEGES | X | X | O | O | O |
| MODULE_ROUTINE_USAGE | X | X | O | O | O |
| MODULE_SEQUENCE_USAGE | X | X | O | O | O |
| MODULE_TABLE_USAGE | X | X | O | O | O |
| PARAMETERS | X | O | O | O | O |
| REFERENTIAL_CONSTRAINTS | O | O | O | O | O |
| ROUTINES | X | O | O | O | O |
| ROUTINE_MODULE_USAGE | X | X | O | O | O |
| ROUTINE_PRIVILEGES | X | O | O | O | O |
| ROUTINE_ROUTINE_USAGE | X | O | O | O | O |
| ROUTINE_SEQUENCE_USAGE | X | O | O | O | O |
| ROUTINE_TABLE_USAGE | X | O | O | O | O |
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
| USAGE_PRIVILEGES | O | O | O | O | O |
| VIEWS | O | O | O | O | O |
| VIEW_MODULE_USAGE | X | X | O | O | O |
| VIEW_ROUTINE_USAGE | X | O | O | O | O |
| VIEW_TABLE_USAGE | O | O | O | O | O |

<a id="dcfd2611c08b7a67"></a>
##### PERFORMANCE_VIEW_SCHEMA 스키마

PERFORMANCE_VIEW_SCHEMA 스키마에 대한 feature matrix는 다음과 같다.

**PERFORMANCE_VIEW_SCHEMA schema의 feature matrix**

<a id="ad095c41dffe8cc5"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| GV$____ | X | O | O | O | O |
| V$AGABLE_INFO | X | O | O | O | O |
| V$ARCHIVELOG | O | O | O | O | O |
| V$AUDITABLE_DB_PRIVILEGES | X | O | O | O | O |
| V$AUDITABLE_SYSTEM_ACTIONS | X | O | O | O | O |
| V$BACKUP | O | O | O | O | O |
| V$BALANCER | O | O | O | O | O |
| V$BCH | X | X | O | O | O |
| V$BUFFER_STAT | X | X | O | O | O |
| V$CLUSTER_DISPATCHER | X | O | O | O | O |
| V$CLUSTER_LOCATION | X | O | O | O | O |
| V$CLUSTER_MEMBER | X | O | O | O | O |
| V$COLUMNS | O | O | O | O | O |
| V$CONTROLFILE | O | O | O | O | O |
| V$DATAFILE | O | O | O | O | O |
| V$DB_CHANGE_TRACKING | X | X | O | O | O |
| V$DB_FILE | O | O | O | O | O |
| V$DB_PROPERTY | X | X | X | X | O |
| V$DISPATCHER | O | O | O | O | O |
| V$ERROR_CODE | O | O | O | O | O |
| V$GLOBAL_TRANSACTION | O | O | O | O | O |
| V$JOURNALING | X | O | O | O | O |
| V$INCREMENTAL_BACKUP | O | O | O | O | O |
| V$INSTANCE | O | O | O | O | O |
| V$KEYWORDS | O | O | O | O | O |
| V$LATCH | O | O | O | O | O |
| V$LICENSE | X | X | X | X | O |
| V$LOCK_WAIT | O | O | O | O | O |
| V$LOCKED_OBJECT | X | X | O | O | O |
| V$LOGFILE | O | O | O | O | O |
| V$OPEN_CURSOR | X | X | X | X | O |
| V$PLAN_HISTORY | X | X | X | O | O |
| V$PLAN_HISTORY_LATEST | X | X | X | O | O |
| V$PROCESS_MEM_STAT | O | O | O | O | O |
| V$PROCESS_SQL_STAT | O | O | O | O | O |
| V$PROCESS_STAT | O | O | O | O | O |
| V$PROPERTY | O | O | O | O | O |
| V$PROPERTY_ALIAS | X | X | X | X | O |
| V$PSM_RESERVED_WORDS | X | O | O | O | O |
| V$QUEUE | O | O | O | O | O |
| V$RESERVED_WORDS | O | O | O | O | O |
| V$SESSION | O | O | O | O | O |
| V$SESSION_AUDIT | X | O | O | O | O |
| V$SESSION_CONNECT_INFO | O | O | O | O | O |
| V$SESSION_EVENT | X | O | O | O | O |
| V$SESSION_MEM_STAT | O | O | O | O | O |
| V$SESSION_MEM_USAGE | X | X | X | O | O |
| V$SESSION_SQL_STAT | O | O | O | O | O |
| V$SESSION_STAT | O | O | O | O | O |
| V$SESSION_WAIT | X | O | O | O | O |
| V$SHARED_MODE | O | O | O | O | O |
| V$SHARED_SERVER | O | O | O | O | O |
| V$SHM_SEGMENT | O | O | O | O | O |
| V$SPROPERTY | O | O | O | O | O |
| V$SQLFN_METADATA | O | O | O | O | O |
| V$SQL_CACHE | O | O | O | O | O |
| V$SQL_COMMAND | X | O | O | O | O |
| V$SQL_HISTORY | X | O | O | O | O |
| V$STATEMENT | O | O | O | O | O |
| V$SYSTEM_EVENT | X | O | O | O | O |
| V$SYSTEM_MEM_STAT | O | O | O | O | O |
| V$SYSTEM_SQL_STAT | O | O | O | O | O |
| V$SYSTEM_STAT | O | O | O | O | O |
| V$TABLES | O | O | O | O | O |
| V$TABLESPACE | O | O | O | O | O |
| V$TABLESPACE_STAT | X | O | O | O | O |
| V$TRANSACTION | O | O | O | O | O |
| V$WAIT_EVENT_CLASS_NAME | X | O | O | O | O |
| V$WAIT_EVENT_NAME | X | O | O | O | O |
| V$XA_TRANSATION | X | O | O | O | O |

<a id="002551a0d5e07a8c"></a>
#### Server Property

Server property에 대한 feature matrix는 다음과 같다.

**Server property의 feature matrix**

<a id="39f5073971c6b4b1"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| ADMIN_SESSION_POOL_INIT_SIZE | X | X | X | X | O |
| ADMIN_SESSION_POOL_NEXT_SIZE | X | X | X | X | O |
| AGING_INTERVAL | O | O | O | O | O |
| AGING_PLAN_INTERVAL | O | O | O | O | O |
| ARCHIVELOG_DIR | O | X | X | X | X |
| ARCHIVELOG_DIR_1 ~ DIR_10 | O | O | O | O | O |
| ARCHIVELOG_FILE | O | O | O | O | O |
| ARCHIVELOG_MODE | O | O | O | O | O |
| BACKUP_DIR_1 ~ DIR_10 | O | O | O | O | O |
| BLOCK_READ_COUNT | O | O | O | O | O |
| BROADCAST_INDEX_REBUILD_PROTOCOL | X | X | X | O | O |
| BROADCAST_REBALANCE_PROTOCOL | X | X | O | O | O |
| BUFFER_CACHE_SIZE | X | X | O | O | O |
| BUFFER_CHECKPOINT_LIST_COUNT | X | X | O | X | X |
| BUFFER_DIRTY_PAGE_LIMIT | X | X | X | X | O |
| BUFFER_FLUSH_THREADS | X | X | O | X | X |
| BUFFER_FLUSHING_INTERVAL | X | X | O | X | X |
| BUFFER_FREE_LIST_COUNT | X | X | O | O | O |
| BUFFER_HASH_BUCKETS | X | X | O | O | O |
| BUFFER_HOT_REGION_CRITERIA | X | X | O | O | O |
| BUFFER_HOT_REGION_PERCENT | X | X | O | O | O |
| BUFFER_LRU_LIST_COUNT | X | X | O | O | O |
| BUFFER_LRU_SCAN_PERCENT | X | X | X | X | O |
| BUFFER_MULTIPAGE_READ_COUNT | X | X | O | O | O |
| BUFFER_PREFETCH_PAGE_COUNT | X | X | X | O | O |
| BULK_IO_PAGE_COUNT | O | O | O | O | O |
| CDISPATCHER_HOT_POLICY_INTERVAL | X | O | O | O | O |
| CDISPATCHER_LOCKABLE_THREADS | X | X | X | X | O |
| CDISPATCHER_LOCKLESS_THREADS | X | X | O | O | O |
| CDISPATCHER_MAX_PACKET_BUFFER_SIZE | X | X | X | X | O |
| CDISPATCHER_SOCKET_BUFFER_SIZE | X | O | O | O | O |
| CHANGE_TRACKING | X | X | O | O | O |
| CHANGE_TRACKING_EXTENT_SIZE | X | X | O | O | O |
| CHANGE_TRACKING_FILE | X | X | O | O | O |
| CHAR_LENGTH_UNITS | O | O | O | O | O |
| CHARACTER_SET | O | O | O | O | O |
| CHECK_DEDICATE_CONNECTION_INTERVAL | X | O | O | O | O |
| CHECK_DEDICATE_SOCKET | X | X | X | X | X |
| CHECKPOINT_LIST_COUNT_PER_IO_GROUP | X | X | X | X | O |
| CLIENT_MAX_COUNT | O | O | O | O | O |
| CLIENT_NUMA_POLICY | X | O | O | O | O |
| CLOSE_PSM_CHILD_STMTS | X | O | O | O | O |
| CLUSTER_ASYNC_COMMIT | X | O | O | O | O |
| CLUSTER_ASYNC_REPLICATION | X | O | O | O | X |
| CLUSTER_CM_BUFFER_COUNT | X | O | O | O | X |
| CLUSTER_CM_BUFFER_SIZE | X | O | O | O | O |
| CLUSTER_CM_READ_BUFFER_SIZE | X | O | O | O | O |
| CLUSTER_COMMIT_SLAVE_CSERVERS | X | X | X | X | O |
| CLUSTER_COMMIT_STREAM_ISOLATION | X | O | O | O | O |
| CLUSTER_CONNECTION | X | O | O | O | O |
| CLUSTER_CONNECTION_TIMEOUT_SEC | X | O | O | O | O |
| CLUSTER_DATA_SYNC_SERVERS | X | O | O | O | O |
| CLUSTER_DEADLOCK_TIMEOUT | X | X | O | O | O |
| CLUSTER_DISPATCHER_IN_QUEUE_SIZE | X | O | O | O | O |
| CLUSTER_DISPATCHER_NUMA_STREAM_MAP | X | O | O | O | O |
| CLUSTER_DISPATCHER_OUT_QUEUE_SIZE | X | O | O | O | O |
| CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE | X | X | X | X | O |
| CLUSTER_HEARTBEAT_INTERVAL | X | O | O | O | O |
| CLUSTER_HEARTBEAT_RETRY_COUNT | X | O | O | O | O |
| CLUSTER_IGNORE_INACTIVE_MEMBER | X | O | O | O | O |
| CLUSTER_KEEPALIVE_IDLE_TIME | X | X | X | X | O |
| CLUSTER_LOCKABLE_CSERVERS | X | X | X | X | O |
| CLUSTER_LOCKLESS_CSERVERS | X | X | X | X | O |
| CLUSTER_MAX_PACKET_SIZE | X | O | O | O | O |
| CLUSTER_MAX_PAYLOAD_SIZE | X | O | O | O | O |
| CLUSTER_PACKET_ALLOCATION_TIMEOUT | X | O | O | O | O |
| CLUSTER_SESSION_HASH_BUCKETS | X | X | O | O | O |
| CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY | X | O | O | O | O |
| CLUSTER_SPLIT_BRAIN_RETRY_COUNT | X | O | O | O | O |
| COMMITTER_HOT_POLICY_INTERVAL | X | O | O | O | O |
| CONTROL_FILE_0 ~ FILE_7 | O | O | O | O | O |
| CONTROL_FILE_COUNT | O | O | O | O | O |
| CONTROL_FILE_TEMP_NAME | O | O | O | O | O |
| COORDINATOR_COMMIT_WRITE_MODE | X | O | O | O | O |
| DA_CLIENT_NUMA_MODE | X | O | O | O | O |
| DATA_STORE_MODE | O | O | O | O | O |
| DATABASE_ACCESS_MODE | O | O | O | O | O |
| DATABASE_INSTANCE_NAME | X | O | O | O | O |
| DDL_AUTOCOMMIT | O | O | O | O | O |
| DDL_LOCK_TIMEOUT | O | O | O | O | O |
| DEADLOCK_PRIORITY | X | X | O | O | O |
| DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION | X | O | O | O | O |
| DEFAULT_INDEX_LOGGING | O | O | X | X | X |
| DEFAULT_INDEX_PCTFREE | X | O | O | O | O |
| DEFAULT_INITRANS | O | O | O | O | O |
| DEFAULT_MAXTRANS | O | O | O | O | O |
| DEFAULT_PCTFREE | O | O | O | O | O |
| DEFAULT_PCTUSED | O | O | O | O | O |
| DEFAULT_REMOVAL_BACKUP_FILE | O | O | O | O | O |
| DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST | O | O | O | O | O |
| DEFAULT_SHARDING | X | O | O | O | O |
| DISABLE_DDL | X | X | X | O | O |
| DISABLE_DDL_CDC_GIVEUP | O | O | O | O | O |
| DISABLE_SERIAL_DDL | X | X | X | O | O |
| DISABLE_UPDATE_PK_CDC_GIVEUP | O | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE | X | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL | X | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME | X | O | O | O | O |
| DISPATCHERS | O | O | O | O | O |
| DISPATCHER_CM_BUFFER_SIZE | O | O | O | O | O |
| DISPATCHER_CM_UNIT_SIZE | O | O | O | O | O |
| DISPATCHER_CONNECTIONS | O | O | O | O | O |
| DISPATCHER_HOT_POLICY_INTERVAL | X | O | O | O | O |
| DISPATCHER_LOAD_BALANCING | X | O | O | O | O |
| DISPATCHER_NUMA_STREAM_MAP | X | O | O | O | O |
| DISPATCHER_QUEUE_SIZE | O | O | O | O | O |
| DISPATCHER_REQUEST_MINI_QUEUE_COUNT | X | O | O | O | O |
| DISPATCHER_RESPONSE_MINI_QUEUE_COUNT | X | O | O | O | O |
| EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY | X | X | X | O | O |
| FETCH_FAILOVER | X | O | O | O | O |
| FULL_TABLE_SCAN_CACHING_THRESHOLD | X | X | X | X | O |
| GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY | X | O | O | O | O |
| GLOBAL_JOURNAL_BUFFER_SIZE | X | O | O | O | O |
| GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE | X | O | O | O | O |
| GLOBAL_PROPERTY_LOCK_TIMEOUT | X | O | O | O | O |
| GLOBAL_TRANSACTION_COMMIT_WRITE_MODE | X | O | O | O | O |
| GLOBAL_TRANSACTION_ISOLATION_SCOPE | X | O | O | O | O |
| GLOBAL_TRANSACTION_LOG_DIR | X | O | O | O | O |
| GLOBAL_TRANSACTION_LOG_FILE_SIZE | X | O | O | O | O |
| GMASTER_NUMA_NODE | X | O | O | O | O |
| GMON_AUTOSTART | X | O | O | O | O |
| HINT_ERROR | O | O | O | O | O |
| IDLE_TIMEOUT | O | O | O | O | O |
| IN_DOUBT_DECISION | O | O | O | O | O |
| IN_KEY_RANGE_ARRAY_COUNT | X | X | O | O | O |
| INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE | X | X | O | O | O |
| INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA | X | X | X | X | O |
| INDEX_BUILD_PARALLEL_FACTOR | O | O | O | O | O |
| INDEX_MERGE_RUN_COUNT | O | O | O | O | O |
| INDEX_LOGGING_THROTTLING | X | X | X | O | O |
| INDEX_REBUILD_BLOCK_READ_COUNT | X | X | O | O | O |
| INDEX_SORT_RUN_SIZE | O | O | O | O | O |
| INDEX_TREE_MERGE_PARALLEL_FACTOR | X | O | O | O | O |
| INST_ALLOCATOR_COUNT | X | O | O | O | O |
| INST_HASH_TABLE_BUCKET_MAX_COUNT | X | X | X | O | O |
| INST_TABLE_BLOCK_SIZE | X | O | O | O | O |
| IPC_CHANNEL_COUNT | X | X | X | O | O |
| JOURNAL_TEMP_DIR | X | O | O | O | O |
| KEEPALIVE_IDLE_TIME | O | O | O | O | O |
| LOCAL_CLUSTER_MEMBER | X | O | O | O | O |
| LOCAL_CLUSTER_MEMBER_HOST | X | O | O | O | O |
| LOCAL_CLUSTER_MEMBER_PORT | X | O | O | O | O |
| LOCAL_JOURNAL_BUFFER_SIZE | X | O | O | O | O |
| LOCATION_FILE | X | O | O | O | O |
| LOCATOR_QUERY_TIMEOUT | X | O | O | O | O |
| LOCK_HASH_TABLE_SIZE | O | O | O | O | O |
| LOCKABLE_DISPATCHER_CM_BUFFER_COUNT | X | X | X | X | O |
| LOCKLESS_DISPATCHER_CM_BUFFER_COUNT | X | X | X | X | O |
| LOG_BLOCK_SIZE | O | O | O | O | O |
| LOG_BUFFER_SIZE | O | O | O | O | O |
| LOG_DIR | O | O | O | O | O |
| LOG_FILE_SIZE | O | O | O | O | O |
| LOG_GROUP_COUNT | O | O | O | O | O |
| LOG_MIRROR_MODE | O | O | O | O | O |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | O | O | O | O | O |
| LOG_MIRROR_TIMEOUT | O | O | O | O | O |
| LOG_SYNC_INTERVAL | O | O | O | O | O |
| LOG_SYNC_INTERVAL_MSEC | X | O | O | O | O |
| MAX_GROUP_COUNT | X | O | O | O | O |
| MAX_JOURNAL_FILE_SIZE | X | O | O | O | O |
| MAX_NODE_COUNT | X | O | O | O | O |
| MAXIMUM_CONCURRENT_ACTIVITIES | O | O | O | O | O |
| MAXIMUM_FILE_CACHE_SIZE | X | X | X | O | O |
| MAXIMUM_FLANGE_COUNT | X | O | O | O | X |
| MAXIMUM_FLUSH_BUFFER_PAGE_COUNT | X | X | X | O | O |
| MAXIMUM_FLUSH_LOG_BLOCK_COUNT | O | O | O | O | O |
| MAXIMUM_FLUSH_PAGE_COUNT | O | O | O | O | O |
| MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT | X | X | O | O | O |
| MAXIMUM_JOURNAL_REPLAY_COUNT | X | O | O | O | O |
| MAXIMUM_NAMED_CURSOR_COUNT | O | O | O | O | O |
| MAXIMUM_PACKAGE_INSTANCE_COUNT | X | X | X | O | O |
| MAXIMUM_SESSION_CM_BUFFER_SIZE | O | O | O | O | O |
| MEASURE_CLUSTER_LATENCY | X | O | O | O | O |
| MEDIA_RECOVERY_LOG_BUFFER_SIZE | O | X | X | X | X |
| MIN_SAMPLE_ROW_COUNT | X | O | O | O | O |
| MINIMUM_UNDO_PAGE_COUNT | O | O | O | O | O |
| NET_BUFFER_SIZE | O | O | O | O | O |
| NLS_DATE_FORMAT | O | O | O | O | O |
| NLS_TIME_FORMAT | O | O | O | O | O |
| NLS_TIME_WITH_TIME_ZONE_FORMAT | O | O | O | O | O |
| NLS_TIMESTAMP_FORMAT | O | O | O | O | O |
| NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT | O | O | O | O | O |
| NUMA | X | O | O | O | O |
| NUMA_MAP | X | O | O | O | O |
| OFFLINE_MEMBER_AFTER_FAILOVER | X | O | O | O | O |
| ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD | X | X | O | O | O |
| ONLINE_JOURNAL_REPLAY_THRESHOLD | X | O | O | O | O |
| OS_GROUP_ACCESS | X | O | O | O | O |
| PACKET_COMPRESSION_THRESHOLD | X | X | O | O | O |
| PAGE_CHECKSUM_TYPE | O | O | O | O | O |
| PARALLEL_IO_FACTOR | O | O | O | O | O |
| PARALLEL_IO_GROUP_1 ~ GROUP_16 | O | O | O | O | O |
| PARALLEL_LOAD_FACTOR | O | O | O | O | O |
| PENDING_LOG_BUFFER_COUNT | O | O | O | O | O |
| PLAN_CACHE | O | O | O | O | O |
| PLAN_CACHE_SIZE | O | O | O | O | O |
| PLAN_HISTORY | X | X | X | O | O |
| PLAN_HISTORY_SIZE | X | X | X | O | O |
| PRIVATE_STATIC_AREA_INIT_SIZE | X | X | O | O | O |
| PRIVATE_STATIC_AREA_NEXT_SIZE | X | X | O | O | O |
| PRIVATE_STATIC_AREA_SHRINK_THRESHOLD | X | X | O | O | O |
| PRIVATE_STATIC_AREA_SIZE | O | O | O | O | O |
| PROCESS_MAX_COUNT | O | O | O | O | O |
| QUERY_TIMEOUT | O | O | O | O | O |
| READABLE_ARCHIVELOG_DIR_COUNT | O | O | O | O | O |
| READABLE_BACKUP_DIR_COUNT | O | O | O | O | O |
| REBALANCE_BLOCK_READ_COUNT | X | O | O | O | O |
| REBALANCE_SHARD_DIVISOR | X | X | X | X | O |
| RECOMPILE_CHECK_MINIMUM_PAGE_COUNT | O | X | X | X | X |
| RECOMPILE_PAGE_PERCENT | O | X | X | X | X |
| RECOVERY_LOG_BUFFER_SIZE | X | O | O | O | O |
| RECYCLEBIN | X | X | O | O | O |
| REDO_LOG_COMPRESSION_THRESHOLD | X | O | O | O | O |
| REFINE_RELATION | O | O | O | O | O |
| SESSION_FATAL_BEHAVIOR | O | O | O | O | O |
| SESSION_MEMORY_INIT_SIZE | X | O | O | O | O |
| SESSION_MEMORY_SHRINK_THRESHOLD | X | O | O | O | O |
| SESSION_POOL_INIT_SIZE | X | X | X | X | O |
| SESSION_POOL_NEXT_SIZE | X | X | X | X | O |
| SHARED_MEMORY_ADDRESS | O | O | O | O | O |
| SHARED_MEMORY_STATIC_KEY | O | O | O | O | O |
| SHARED_MEMORY_STATIC_NAME | O | O | O | O | O |
| SHARED_MEMORY_STATIC_SIZE | O | O | O | O | O |
| SHARED_REQUEST_QUEUE_COUNT | O | O | O | O | O |
| SHARED_SERVERS | O | O | O | O | O |
| SHARED_SESSION | O | O | O | O | O |
| SNAPSHOT_STATEMENT_TIMEOUT | O | O | O | O | O |
| SQL_HISTORY_SIZE | X | O | O | O | O |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | O | O | O | O | O |
| SYNC_DISPATCHER_CM_BUFFER_COUNT | X | X | X | X | O |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | X | X | O | O | O |
| SYSTEM_FILE_IO | O | O | O | O | O |
| SYSTEM_MEMORY_AUX_TABLESPACE_SIZE | X | O | O | O | O |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_TABLESPACE_DIR | O | O | O | O | O |
| SYSTEM_UDS_DIR | X | O | O | O | O |
| TCP_NODELAY | X | O | O | O | O |
| TEMP_SEGMENT_CACHE_SIZE | X | O | O | O | O |
| TEMP_UNDO_ENABLED | X | O | O | O | O |
| TIMED_STATISTICS | X | O | O | O | O |
| TIMER_INTERVAL | O | X | X | O | O |
| TIMEZONE | O | O | O | O | O |
| TRACE_ALTER_SYSTEM | O | O | O | O | O |
| TRACE_DDL | O | O | O | O | O |
| TRACE_LOG_ID | O | O | O | O | O |
| TRACE_LOG_MSGBUG_SIZE | X | O | O | O | O |
| TRACE_LOG_TIME_DETAIL | O | O | O | O | O |
| TRACE_LOGGER | X | O | O | O | O |
| TRACE_LOGGER_REMOTE_HOST | X | O | O | O | O |
| TRACE_LOGGER_REMOTE_PORT | X | O | O | O | O |
| TRACE_LOGIN | O | O | O | O | O |
| TRACE_LONG_RUN_CURSOR | O | O | O | O | O |
| TRACE_LONG_RUN_SQL | O | O | O | O | O |
| TRACE_LONG_RUN_TIMER | X | X | O | O | O |
| TRACE_SYSTEM_DIR | X | X | X | X | O |
| TRACE_XA | O | O | O | O | O |
| TRANSACTION_ALLOCATION_TIMEOUT | X | O | O | O | O |
| TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O | O |
| TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT | O | O | O | O | O |
| TRANSACTION_TABLE_SIZE | O | O | O | O | O |
| TRANSACTION_TIMEOUT | X | O | O | O | O |
| UNDO_RELATION_ALLOCATION_TIMEOUT | X | O | O | O | O |
| UNDO_RELATION_COUNT | O | O | O | O | O |
| UNDO_SHRINK_THRESHOLD | O | O | O | O | O |
| USE_LARGE_PAGES | X | X | O | O | O |
| USER_DATA_TABLESPACE_MEDIA_TYPE | X | X | O | O | O |
| USER_DATA_TABLESPACE_SIZE | X | X | O | O | O |
| USER_DISK_DATA_TABLESPACE_NEXTSIZE | X | X | O | O | O |
| USER_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| XA_TRANSACTION_IDLE_TIMEOUT | X | X | O | O | O |

<a id="ff5543ba546a3184"></a>
#### Property Alias

Property alias에 대한 feature matrix는 다음과 같다.

**Property alias의 feature matrix**

<a id="8914a92c7f9525c7"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| CDISPATCHER_THREADS | X | O | O | O | O |
| CLUSTER_COMMIT_SLAVES | X | O | O | O | O |
| CLUSTER_SEREVER_RESPONSE_QUEUE_SIZE | X | O | O | O | O |
| CSERVER | X | O | O | O | O |
| INCREMENTAL_CHECKPOINT_CRITERIA | X | X | X | X | O |
| LOCKLESS_CSERVERS | X | X | O | O | O |
| MEMORY_MERGE_RUN_COUNT | O | O | O | O | O |
| MEMORY_SORT_RUN_SIZE | O | O | O | O | O |
| SYSTEM_LOGGER_DIR | O | O | O | O | O |

<a id="f045f0a5afac5033"></a>
### SQL

<a id="7ac17d9ea7490ac9"></a>
#### SQL Element

<a id="27a91bf714e643b1"></a>
##### Data Type

데이터 타입에 대한 feature matrix는 다음과 같다.

<a id="03559f73efb39b2d"></a>
<table class="table column_count_7"><caption>Data type의 feature matrix</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>문자 스트링 타입</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>이진 스트링 타입</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>십진 숫자 타입</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>이진 숫자 타입</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN 타입</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>날짜/시간 타입</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL 타입</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROWID 타입</div></td><td><div>ROWID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="8025e72377e8009d"></a>
##### Function

함수 및 연산자에 대한 feature matrix는 다음과 같다.

**Function의 feature matrix**

<a id="65d2164c8498b9bc"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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
| ASCII( char ) | X | O | O | O | O |
| ASIN( num ) | O | O | O | O | O |
| ATAN( num ) | O | O | O | O | O |
| ATAN2( num1, num2 ) | O | O | O | O | O |
| AVG( num ) | O | O | O | O | O |
| AVG( expr ) OVER | X | X | X | X | O |
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
| CHR( num ) | X | O | O | O | O |
| CLOCK_DATE() | O | O | O | O | O |
| CLOCK_LOCALTIME() | O | O | O | O | O |
| CLOCK_LOCALTIMESTAMP() | O | O | O | O | O |
| CLOCK_TIME() | O | O | O | O | O |
| CLOCK_TIMESTAMP() | O | O | O | O | O |
| COALESCE( expr1, ..., exprN ) | O | O | O | O | O |
| CONCAT( str1, str2 ) | O | O | O | O | O |
| CONCATENATE( str1, str2 ) | O | O | O | O | O |
| CONNECT_BY_ISCYCLE | X | X | X | O | O |
| CONNECT_BY_ISLEAF | X | X | X | O | O |
| CONNECT_BY_ROOT expr | X | X | X | O | O |
| CORR( expr1, expr2 ) OVER | X | X | X | X | O |
| COS( num ) | O | O | O | O | O |
| COT( num ) | O | O | O | O | O |
| COUNT( expr ) | O | O | O | O | O |
| COUNT( expr ) OVER | X | X | X | X | O |
| COUNT(*) | O | O | O | O | O |
| COUNT(*) OVER | X | X | X | X | O |
| COVAR_POP( expr1, expr2 ) OVER | X | X | X | X | O |
| COVAR_SAMP( expr1, expr2 ) OVER | X | X | X | X | O |
| CUME_DIST() OVER | X | X | X | X | O |
| CURRENT_CATALOG | O | O | O | O | O |
| CURRENT_DATE | O | O | O | O | O |
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
| DENSE_RANK() OVER | X | X | X | X | O |
| DIGEST ( data, type ) | X | O | O | O | O |
| expr IS [NOT] DISTINCT FROM expr | X | X | X | X | O |
| ( expr, ... ) IS [NOT] DISTINCT FROM ( expr, ... ) | X | X | X | X | O |
| DUMP( expr ) | O | O | O | O | O |
| EXISTS( subquery ) | O | O | O | O | O |
| EXP( num ) | O | O | O | O | O |
| EXTRACT( field FROM datetime ) | O | O | O | O | O |
| FACTORIAL( num ) | O | O | O | O | O |
| FIRST : aggr_func KEEP ( DENSE_RANK FIRST ORDER BY expr, ... ) OVER | X | X | X | X | O |
| FIRST_VALUE( expr ) OVER | X | X | X | X | O |
| FLOOR( num ) | O | O | O | O | O |
| FROM_BASE64( str ) | X | O | O | O | O |
| FROM_TZ( timestamp, timezone ) | X | X | X | O | O |
| GREATEST( expr, ... ) | O | O | O | O | O |
| HASH32( expr [, expr] ... ) | X | X | X | O | O |
| HEX( str ) | X | O | O | O | O |
| expr1 [NOT] IN ( expr, ... ) | O | O | O | O | O |
| expr1 [NOT] IN ( subquery ) | O | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt; ) | O | O | O | O | O |
| subquery [NOT] IN ( subquery ) | O | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( subquery ) | O | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt;, ... ) | O | O | O | O | O |
| INITCAP( str ) | O | O | O | O | O |
| INSTR( str, substr, ... ) | O | O | O | O | O |
| IS NOT NULL | O | O | O | O | O |
| IS NULL | O | O | O | O | O |
| JSON_ARRAY( expr, ... ) | X | X | X | X | O |
| JSON_ARRAYAGG( expr ) | X | X | X | X | O |
| JSON_ARRAYAGG( expr ) OVER | X | X | X | X | O |
| JSON_OBJECT( name VALUE expr, ... ) | X | X | X | X | O |
| JSON_OBJECTAGG( name VALUE expr ) | X | X | X | X | O |
| JSON_OBJECTAGG( name VALUE expr ) OVER | X | X | X | X | O |
| LAG( expr [, offset [, default]] ) OVER | X | X | X | X | O |
| LAST : aggr_func KEEP ( DENSE_RANK LAST ORDER BY expr, ... ) OVER | X | X | X | X | O |
| LAST_DAY( date ) | O | O | O | O | O |
| LAST_IDENTITY_VALUE() | X | O | O | O | O |
| LAST_VALUE( expr ) OVER | X | X | X | X | O |
| LEAD( expr [, offset [, default]] ) OVER | X | X | X | X | O |
| LEAST( expr, ... ) | O | O | O | O | O |
| LENGTH( str ) | O | O | O | O | O |
| LENGTHB( str ) | O | O | O | O | O |
| LEVEL | X | X | X | O | O |
| string [NOT] LIKE pattern ESCAPE escape_char | O | O | O | O | O |
| LISTAGG( str [, delimiter] ) OVER | X | X | X | X | O |
| LN( num ) | O | O | O | O | O |
| LNNVL( expr ) | X | X | O | O | O |
| LOCALTIME | O | O | O | O | O |
| LOCALTIMESTAMP | O | O | O | O | O |
| LOCAL_GROUP_ID() | X | O | O | O | O |
| LOCAL_GROUP_NAME() | X | O | O | O | O |
| LOCAL_MEMBER_ID() | X | O | O | O | O |
| LOCAL_MEMBER_NAME() | X | O | O | O | O |
| LOG( num2 ) | O | O | O | O | O |
| LOG( num1, num2 ) | O | O | O | O | O |
| LOGON_USER() | O | O | O | O | O |
| LOWER( str ) | O | O | O | O | O |
| LPAD( str, length, fill ) | O | O | O | O | O |
| LTRIM( str, [ str ] ) | O | O | O | O | O |
| MAX( expr ) | O | O | O | O | O |
| MAX( expr ) OVER | X | X | X | X | O |
| MEDIAN( expr ) OVER | X | X | X | X | O |
| MIN( expr ) | O | O | O | O | O |
| MIN( expr ) OVER | X | X | X | X | O |
| MOD( num1, num2 ) | O | O | O | O | O |
| MONTHS_BETWEEN( date1, date2 ) | X | O | O | O | O |
| NEXT_DAY( date, day ) | X | O | O | O | O |
| seq.NEXTVAL | O | O | O | O | O |
| NEXTVAL( seq ) | O | O | O | O | O |
| NEXT VALUE FOR seq | O | O | O | O | O |
| NOT | O | O | O | O | O |
| NTH_VALUE( expr, n ) OVER | X | X | X | X | O |
| NTILE( expr ) OVER | X | X | X | X | O |
| NULLIF( expr1, expr2 ) | O | O | O | O | O |
| NUMTODSINTERVAL( num, interval_indicator ) | X | X | O | O | O |
| NUMTOYMINTERVAL( num, interval_indicator ) | X | X | O | O | O |
| NVL( expr1, expr2 ) | O | O | O | O | O |
| NVL2( expr1, expr2, expr3 ) | O | O | O | O | O |
| OCTET_LENGTH( str ) | O | O | O | O | O |
| OVERLAY( str1 PLACING str2 FROM start FOR length ) | O | O | O | O | O |
| OR | O | O | O | O | O |
| PERCENT_RANK() OVER | X | X | X | X | O |
| PERCENTILE_CONT( expr ) OVER | X | X | X | X | O |
| PERCENTILE_DISC( expr ) OVER | X | X | X | X | O |
| PHYSICAL_LENGTH( expr ) | X | X | O | O | O |
| PI() | O | O | O | O | O |
| POSITION( str1 IN str2 ) | O | O | O | O | O |
| POWER( num1, num2 ) | O | O | O | O | O |
| PRIOR expr | X | X | X | O | O |
| RADIANS( degrees ) | O | O | O | O | O |
| RANDOM( min, max ) | O | O | O | O | O |
| RANK() OVER | X | X | X | X | O |
| RATIO_TO_REPORT( expr ) OVER | X | X | X | X | O |
| REGR_AVGX( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_AVGY( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_COUNT( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_INTERCEPT( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_R2( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_SLOPE( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_SXX( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_SXY( expr1, expr2 ) OVER | X | X | X | X | O |
| REGR_SYY( expr1, expr2 ) OVER | X | X | X | X | O |
| REPEAT( str, num ) | O | O | O | O | O |
| REPLACE( str, from, to ) | O | O | O | O | O |
| REVERSE( str ) | X | O | O | O | O |
| ROUND( num ) | O | O | O | O | O |
| ROUND( date, fmt ) | O | O | O | O | O |
| ROW_NUMBER() OVER | X | X | X | X | O |
| ROWID_GRID_BLOCK_ID( rowid ) | X | O | O | O | O |
| ROWID_GRID_BLOCK_SEQ( rowid ) | X | O | O | O | O |
| ROWID_MEMBER_ID( rowid ) | X | O | O | O | O |
| ROWID_OBJECT_ID( rowid ) | O | O | O | O | O |
| ROWID_PAGE_ID( rowid ) | O | O | O | O | O |
| ROWID_ROW_NUMBER( rowid ) | O | O | O | O | O |
| ROWID_SHARD_ID( rowid ) | X | O | O | O | O |
| ROWID_TABLESPACE_ID( rowid ) | O | O | O | O | O |
| ROWNUM | X | O | O | O | O |
| RPAD( str, length, fill ) | O | O | O | O | O |
| RTRIM( str, [ str ] ) | O | O | O | O | O |
| SESSION_ID() | O | O | O | O | O |
| SESSION_SERIAL() | O | O | O | O | O |
| SESSION_USER | O | O | O | O | O |
| SESSIONTIMEZONE() | X | X | X | X | O |
| SHARD_GROUP_ID( table, expr ) | X | O | O | O | O |
| SHARD_GROUP_NAME( table_name, shard_key_value [, ...] ) | X | O | O | O | O |
| SHARD_ID( table, expr ) | X | O | O | O | O |
| SHARD_NAME( table_name, shard_key_value [, ...] ) | X | O | O | O | O |
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
| STATEMENT_VIEW_SCN_DCN() | X | O | O | O | O |
| STATEMENT_VIEW_SCN_GCN() | X | O | O | O | O |
| STATEMENT_VIEW_SCN_LCN() | X | O | O | O | O |
| STDDEV( [ ALL \| DISTINCT ] expr ) | X | O | O | O | O |
| STDDEV( expr ) OVER | X | X | X | X | O |
| STDDEV_POP( expr ) | X | O | O | O | O |
| STDDEV_POP( expr ) OVER | X | X | X | X | O |
| STDDEV_SAMP( expr ) | X | O | O | O | O |
| STDDEV_SAMP( expr ) OVER | X | X | X | X | O |
| STRING_AGG( str [, delimiter] ) OVER | X | X | X | X | O |
| SUBSTR( str FROM start FOR length ) | O | O | O | O | O |
| SUBSTR( str, start, length ) | O | O | O | O | O |
| SUBSTRB( str, start, length ) | O | O | O | O | O |
| SUBSTRING( str FROM start FOR length ) | O | O | O | O | O |
| SUBSTRING( str, start, length ) | O | O | O | O | O |
| SUM( expr ) | O | O | O | O | O |
| SUM( expr ) OVER | X | X | X | X | O |
| SYSDATE | O | O | O | O | O |
| SYS_CONNECT_BY_PATH( expr, 'string' ) | X | X | X | O | O |
| SYS_EXTRACT_UTC( datetime_with_timezone ) | X | O | O | O | O |
| SYSTIME | O | O | O | O | O |
| SYSTIMESTAMP | O | O | O | O | O |
| TAN( num ) | O | O | O | O | O |
| TO_CHAR( datetime, fmt ) | O | O | O | O | O |
| TO_CHAR( number, fmt ) | O | O | O | O | O |
| TO_BASE64( str ) | X | O | O | O | O |
| TO_DATE( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_BIGINT( str, fmt ) | X | X | O | O | O |
| TO_NATIVE_DOUBLE( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_INTEGER( str, fmt ) | X | X | O | O | O |
| TO_NATIVE_REAL( str, fmt ) | O | O | O | O | O |
| TO_NATIVE_SMALLINT( str, fmt ) | X | X | O | O | O |
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
| UNHEX( str ) | X | O | O | O | O |
| UNHEX_TO_CHARSTR( str ) | X | O | O | O | O |
| USER_ID() | O | O | O | O | O |
| UUID() | X | O | O | O | O |
| VAR_POP( expr ) | X | O | O | O | O |
| VAR_POP( expr ) OVER | X | X | X | X | O |
| VAR_SAMP( expr ) | X | O | O | O | O |
| VAR_SAMP( expr ) OVER | X | X | X | X | O |
| VARIANCE( [ ALL \| DISTINCT ] expr ) | X | O | O | O | O |
| VARIANCE( expr ) OVER | X | X | X | X | O |
| VERSION() | O | O | O | O | O |
| WIDTH_BUCKET( num, min, max, cnt ) | O | O | O | O | O |

<a id="0c005e783ced3f50"></a>
#### Object

<a id="21e741dac1c1aaef"></a>
##### SQL Object

SQL 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="6323eb3dc0676d18"></a>
<table class="table column_count_7"><caption>SQL 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center"><div>객체</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="12"><div>Database 
객체</div></td><td class="to_middle"><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE REGISTER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESTORE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE SYSTEM</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>COMMENT ON object IS ..</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
객체</div></td><td class="to_middle"><div>CREATE PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
객체</div></td><td class="to_middle"><div>CREATE AUDIT POLICY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP AUDIT POLICY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER AUDIT POLICY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>AUDIT POLICY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>NOAUDIT POLICY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
객체</div></td><td class="to_middle"><div>CREATE USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GRANT privileges TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>REVOKE privileges FROM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 객체</div></td><td class="to_middle"><div>CREATE SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
객체</div></td><td class="to_middle"><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="24"><div>Table 
객체</div></td><td class="to_middle"><div>CREATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TRUNCATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>FLASHBACK TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PURGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
객체</div></td><td class="to_middle"><div>CREATE VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Index 
객체</div></td><td class="to_middle"><div>CREATE INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. AGING</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. RENAME</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
객체</div></td><td class="to_middle"><div>CREATE SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
객체</div></td><td class="to_middle"><div>CREATE SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
객체</div></td><td class="to_middle"><div>CREATE PROCEDURE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROCEDURE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROCEDURE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
객체</div></td><td class="to_middle"><div>CREATE FUNCTION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP FUNCTION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER FUNCTION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package
객체</div></td><td class="to_middle"><div>CREATE PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PACKAGE BODY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="6109adab9e57c440"></a>
##### Cluster Object

Cluster 객체를 생성/ 제거/ 변경하는 DDL에 대한 feature matrix는 다음과 같다.

<a id="fea4abee110227c4"></a>
<table class="table column_count_7"><caption>Cluster 객체 DDL의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>객체</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="4"><div>Cluster system 
객체</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
객체</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
객체</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Cluster table과 shard
객체</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Global 
secondary index
객체</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="8a8592a45d0510d1"></a>
#### SQL Language

<a id="072e038aeb32db7d"></a>
##### DML

데이터를 조작하는 DML 구문의 feature matrix는 다음과 같다.

**DML의 feature matrix**

<a id="ac4946740c7cf5a6"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| INSERT INTO .. | O | O | O | O | O |
| INSERT INTO .. RETURNING query | O | O | O | O | O |
| INSERT INTO .. RETURNING .. INTO .. | O | O | O | O | O |
| INSERT INTO .. UPDATE | X | X | X | O | O |
| INSERT INTO .. UPDATE .. RETURNING .. | X | X | X | O | O |
| INSERT INTO .. UPDATE .. RETURNING .. INTO .. | X | X | X | O | O |
| DELETE FROM .. | O | O | O | O | O |
| DELETE FROM .. RETURNING query | O | O | O | O | O |
| DELETE FROM .. RETURNING .. INTO .. | O | O | O | O | O |
| DELETE FROM .. WHERE CURRENT OF cursor | O | O | O | O | O |
| UPDATE .. | O | O | O | O | O |
| UPDATE .. RETURNING query | O | O | O | O | O |
| UPDATE .. RETURNING .. INTO .. | O | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O | O |
| CALL proc_name | X | O | O | O | O |

<a id="2d5224615c9580db"></a>
##### Query

데이터를 조회하는 SELECT 구문의 feature matrix는 다음과 같다.

**SELECT의 feature matrix**

<a id="1a239257eeb932eb"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| &lt;query expression&gt; | O | O | O | O | O |
| &lt;query specification&gt; | O | O | O | O | O |
| &lt;select list&gt; | O | O | O | O | O |
| &lt;from clause&gt; | O | O | O | O | O |
| &lt;joined table&gt; | O | O | O | O | O |
| &lt;where clause&gt; | O | O | O | O | O |
| &lt;group by clause&gt; | O | O | O | O | O |
| &lt;window clause&gt; | X | X | X | X | O |
| &lt;window partition clause&gt; | X | X | X | X | O |
| &lt;window order clause&gt; | X | X | X | X | O |
| &lt;window frame clause&gt; | X | X | X | X | O |
| &lt;window frame exclusion&gt; | X | X | X | X | O |
| &lt;order by clause&gt; | O | O | O | O | O |
| &lt;offset limit clause&gt; | O | O | O | O | O |
| &lt;set operator&gt; | O | O | O | O | O |
| &lt;subquery&gt; | O | O | O | O | O |
| &lt;hint clause&gt; | O | O | O | O | O |
| &lt;with clause&gt; | X | X | X | O | O |
| &lt;search clause&gt; | X | X | X | O | O |
| &lt;cycle clause&gt; | X | X | X | O | O |
| &lt;start with clause&gt; | X | X | X | O | O |
| &lt;connect by clause&gt; | X | X | X | O | O |
| &lt;order siblings by clause&gt; | X | X | X | O | O |

<a id="eea3f9c63b84f4fd"></a>
##### Control Language

제어 구문의 feature matrix는 다음과 같다.

<a id="508a26ae2a1f49eb"></a>
<table class="table column_count_7"><caption>제어 구문의 feature matrix</caption><thead><tr><th class="to_center"><div>구분</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="c3d22bedf2e2fc2f"></a>
#### PSM Language

Persistent Stored Module (PSM) language element의 feature matrix는 다음과 같다.

**Persistent Stored Module (PSM) language element의 feature matrix**

<a id="5bd37893b4757b9f"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| Assignment Statement | X | O | O | O | O |
| Basic LOOP Statement | X | O | O | O | O |
| Block (BEGIN .. END) | X | O | O | O | O |
| CASE Statement | X | O | O | O | O |
| CLOSE Statement | X | O | O | O | O |
| Collection Method Invocation | X | O | O | O | O |
| Collection Variable Declaration | X | O | O | O | O |
| CONTINUE Statement | X | O | O | O | O |
| Cursor FOR LOOP Statement | X | O | O | O | O |
| Cursor Variable Declaration | X | O | O | O | O |
| DELETE Statement Extension | X | O | O | O | O |
| EXCEPTION_INIT Pragma | X | O | O | O | O |
| Exception Declaration | X | O | O | O | O |
| Exception Handler | X | O | O | O | O |
| EXECUTE IMMEDIATE Statement | X | O | O | O | O |
| EXIT Statement | X | O | O | O | O |
| Explicit Cursor Declaration and Definition | X | O | O | O | O |
| FETCH Statement | X | O | O | O | O |
| FOR LOOP Statement | X | O | O | O | O |
| GOTO Statement | X | O | O | O | O |
| IF Statement | X | O | O | O | O |
| Implicit Cursor Attribute | X | O | O | O | O |
| INSERT Statement Extension | X | O | O | O | O |
| Named Cursor Attribute | X | O | O | O | O |
| NULL Statement | X | O | O | O | O |
| OPEN Statement | X | O | O | O | O |
| OPEN FOR Statement | X | O | O | O | O |
| Procedure Call | X | O | O | O | O |
| Procedure Declaration and Definition | X | O | O | O | O |
| RAISE Statement | X | O | O | O | O |
| Record Variable Declaration | X | O | O | O | O |
| RETURN Statement | X | O | O | O | O |
| RETURN TABLE Statement | X | X | X | X | O |
| RETURNING INTO clause | X | O | O | O | O |
| %ROWTYPE Attribute | X | O | O | O | O |
| Scalar Variable Declaration | X | O | O | O | O |
| SELECT INTO Statement | X | O | O | O | O |
| SQLCODE Function | X | O | O | O | O |
| SQLERRM Function | X | O | O | O | O |
| %TYPE Attribute | X | O | O | O | O |
| UPDATE Statement Extension | X | O | O | O | O |
| WHILE LOOP Statement | X | O | O | O | O |

Built-in Package 의 feature matrix는 다음과 같다.

<a id="9a5ad228c02731a1"></a>
<table class="table column_count_7"><caption>Built-in Package의 feature matrix</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="c522954fe145b4e9"></a>
### API

<a id="8ebc471b58a12ee9"></a>
#### ODBC

ODBC 표준 API에 대한 feature matrix는 다음과 같다.

**ODBC 표준 feature matrix**

<a id="34f86f43c45fb51f"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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

<a id="f7a6cf00c5666a8d"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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
| SQLGetGroupCount | X | O | O | O | O |
| SQLGetGroupIDs | X | O | O | O | O |
| SQLGetGroupName | X | O | O | O | O |
| SQLGetSuitableGroupID | X | O | O | O | O |

<a id="3f85d22ab7d06dc8"></a>
#### JDBC

JDBC에 대한 class feature matrix는 다음과 같다.

**JDBC class의 feature matrix**

<a id="2245de530ceb9d5f"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| CallableStatement | X | O | O | O | O |
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

<a id="45d75b820539e6fa"></a>
#### Embedded SQL

<a id="aa55db6192d41361"></a>
##### Precompiler Option

Precompiler의 option에 대한 feature matrix는 다음과 같다.

**Precompiler option의 feature matrix**

<a id="62c2d7f527d3fe51"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | O | O | O | O | O |
| --include-path | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --output | O | O | O | O | O |
| --unsafe-null | O | O | O | O | O |
| --version | O | O | O | O | O |
| --no-lineinfo | X | O | O | O | O |
| --char_map | X | O | O | O | O |
| --cumulative | X | X | O | O | O |
| --autocommit | X | X | X | O | O |
| --parse | X | X | O | O | O |

<a id="fa05c19ee365ce41"></a>
##### Embedded SQL 전용 구문

Embedded SQL에서만 사용 가능한 SQL 구문에 대한 feature matrix는 다음과 같다.

**Embedded SQL 전용 구문의 feature matrix**

<a id="2eac0b2b6be22dd7"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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
| EXEC SQL GET GROUPID | X | O | O | O | O |
| EXEC SQL INCLUDE | O | O | O | O | O |
| EXEC SQL INCLUDE SQLCA | O | O | O | O | O |
| EXEC SQL OPTION | O | O | O | O | O |
| EXEC SQL ROLLBACK RELEASE | O | O | O | O | O |
| EXEC SQL WHENEVER | O | O | O | O | O |
| EXEC SQL BEGIN ARGUMENT SECTION | X | X | X | O | O |
| EXEC SQL END ARGUMENT SECTION | X | X | X | O | O |

<a id="f8e4bc59a65c8a45"></a>
##### Host Variable Data Type

Host 변수에 사용할 수 있는 embbeded SQL data type의 feature matrix는 다음과 같다.

**Host data type의 feature matrix**

<a id="71cc0d661cc99225"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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

<a id="9b2509eb8163a2b5"></a>
##### Dynamic SQL

Dynamic SQL에 대한 feature matrix는 다음과 같다.

**Dynamic SQL의 feature matrix**

<a id="fd2c46570d59268c"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| SELECT .. INTO | O | O | O | O | O |
| EXECUTE IMMEDIATE sql | O | O | O | O | O |
| PREPARE stmt | O | O | O | O | O |
| EXECUTE stmt | O | O | O | O | O |
| DECLARE cursor FOR sql | O | O | O | O | O |
| DECLARE cursor FOR stmt | O | O | O | O | O |
| OPEN cursor | O | O | O | O | O |
| OPEN cursor USING | O | O | O | O | O |
| FETCH cursor INTO | O | O | O | O | O |
| CLOSE cursor | O | O | O | O | O |
| DELETE .. WHERE CURRENT OF cursor | O | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | O | O | O | O | O |

<a id="e0ceabcddbb71092"></a>
#### PyDBC

<a id="083ad71b8b6b68e8"></a>
##### Module

PyDBC가 제공하는 pygoldilocks의 method feature matrix는 다음과 같다.

**pygoldilock method의 feature matrix**

<a id="40c3f8212cedfb64"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| connect | X | O | O | O | O |
| Date | X | O | O | O | O |
| Time | X | O | O | O | O |
| Timestamp | X | O | O | O | O |
| DateFromTicks | X | O | O | O | O |
| TimeFromTicks | X | O | O | O | O |
| TimestampFromTicks | X | O | O | O | O |
| Binary | X | O | O | O | O |
| STRING | X | O | O | O | O |
| BINARY | X | O | O | O | O |
| NUMBER | X | O | O | O | O |
| DATETIME | X | O | O | O | O |
| ROWID | X | O | O | O | O |
| getDecimalSeparator | X | O | O | O | O |
| setDecimalSeparator | X | O | O | O | O |

pygoldilocks module의 attribute feature matrix는 다음과 같다.

**pygoldilock attribute의 feature matrix**

<a id="e1c97b3b245900d3"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| apilevel | X | O | O | O | O |
| threadsafety | X | O | O | O | O |
| paramstyle | X | O | O | O | O |
| version | X | O | O | O | O |
| lowercase | X | O | O | O | O |

<a id="81bdab6764aca4be"></a>
##### Connection

Connection 객체의 method feature matrix는 다음과 같다.

**Connection method의 feature matrix**

<a id="fb082d475bafe8df"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor | X | O | O | O | O |
| commit | X | O | O | O | O |
| rollback | X | O | O | O | O |
| close | X | O | O | O | O |
| getinfo | X | O | O | O | O |
| execute | X | O | O | O | O |
| set_attr | X | O | O | O | O |

Connection 객체의 attribute feature matrix는 다음과 같다.

**Connection attribute의 feature matrix**

<a id="9f282dfe86069b05"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| autocommit | X | O | O | O | O |
| searchescape | X | O | O | O | O |
| timeout | X | O | O | O | O |

<a id="f0ddbf830cf57560"></a>
##### Cursor

Cursor 객체의 method feature matrix는 다음과 같다.

**Cursor method의 feature matrix**

<a id="27476e73f0bd55c1"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| excute | X | O | O | O | O |
| executemany | X | O | O | O | O |
| fetchone | X | O | O | O | O |
| fetchall | X | O | O | O | O |
| fetchmany | X | O | O | O | O |
| commit | X | O | O | O | O |
| rollback | X | O | O | O | O |
| skip | X | O | O | O | O |
| nextset | X | O | O | O | O |
| close | X | O | O | O | O |
| setinputsizes | X | O | O | O | O |
| setoutputsize | X | O | O | O | O |
| callproc | X | O | O | O | O |
| callfunc | X | O | O | O | O |
| tables | X | O | O | O | O |
| columns | X | O | O | O | O |
| statistics | X | O | O | O | O |
| rowIdColumns | X | O | O | O | O |
| rowVerColumns | X | O | O | O | O |
| primaryKeys | X | O | O | O | O |
| foreignKeys | X | O | O | O | O |
| procedures | X | O | O | O | O |
| getTypeInfo | X | O | O | O | O |

Cursor 객체의 attribute feature matrix는 다음과 같다.

**Cursor attribute의 feature matrix**

<a id="66c5e72739d8b18e"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| Description | X | O | O | O | O |
| rowcount | X | O | O | O | O |
| arraysize | X | O | O | O | O |
| connection | X | O | O | O | O |
| fast_executemany | X | O | O | O | O |

<a id="9de2910988badd89"></a>
##### Row

Row 객체의 attribute feature matrix는 다음과 같다.

**Row attribute의 feature matrix**

<a id="4f5f9dfa1aa0bea6"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor_description | X | O | O | O | O |

<a id="81da60c99a9faf27"></a>
### Utility

<a id="692b11cc5d3748c4"></a>
#### gcreatedb

<a id="b3b209a0a6b35f7f"></a>
##### Command Usage

gcreatedb의 command usage에 대한 feature matrix는 다음과 같다.

**gcreatedb command usage의 feature matrix**

<a id="77facf77bb99f613"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --character_set | O | O | O | O | O |
| --char_length_units | O | O | O | O | O |
| --cluster | X | O | O | O | O |
| --db_comment | O | O | O | O | O |
| --help | O | O | O | O | O |
| --host | X | O | O | O | O |
| --member | X | O | O | O | O |
| --port | X | O | O | O | O |
| --silent | O | O | O | O | O |
| --timezone | O | O | O | O | O |

<a id="4d28d3d182c8d671"></a>
#### glsnr

<a id="12bf407d84813083"></a>
##### Command Usage

glsnr의 command usage에 대한 feature matrix는 다음과 같다.

**glsnr command usage의 feature matrix**

<a id="0433d382029d65ad"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | O | O | O | O | O |
| --home | X | O | O | O | O |
| --silent | O | O | O | O | O |
| --start | O | O | O | O | O |
| --status | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="0b51aa9645c3c45f"></a>
##### Configuration File

glsnr의 configuration에 대한 feature matrix는 다음과 같다.

**glsnr configuration file syntax의 feature matrix**

<a id="c85e7f8a777b35be"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| BACKLOG | O | O | O | O | O |
| DEFAULT_CS_MODE | O | O | O | O | O |
| LISTENER_LOG_DIR | X | O | O | O | O |
| LISTEN_PORT | O | O | O | O | O |
| TCP_EXCLUDED | O | O | O | O | O |
| TCP_INVITED | O | O | O | O | O |
| TCP_HOST | O | O | O | O | O |
| TCP_VALIDNODE_CHECKING | O | O | O | O | O |
| TIMEOUT | O | O | O | O | O |
| USR_DIR | X | O | O | O | O |

<a id="792bf916e4ca74ac"></a>
#### gsql/gsqlnet

<a id="4c741772b524fe90"></a>
##### Command Usage

gsql의 command usage에 대한 feature matrix는 다음과 같다.

**gsql command usage의 feature matrix**

<a id="9e7334770adbbc49"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
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

<a id="d246f67176168b67"></a>
##### Interactive gsql Command

gsql 프롬프트 상태에서 사용하는 interactive gsql command에 대한 feature matrix는 다음과 같다.

**Interactive gsql command의 feature matrix**

<a id="b2ec9f9fb81e4848"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| `\\` | O | O | O | O | O |
| `\connect userid password [as sysdba] ` | O | O | O | O | O |
| `\cshutdown` | X | O | O | O | O |
| `\cstartup` | X | O | O | O | O |
| `\ddl_cluster` | X | O | O | O | O |
| `\ddl_db` | O | O | O | O | O |
| `\ddl_tablespace` | O | O | O | O | O |
| `\ddl_profile` | O | O | O | O | O |
| `\ddl_audit_policy` | X | O | O | O | O |
| `\ddl_auth` | O | O | O | O | O |
| `\ddl_schema` | O | O | O | O | O |
| `\ddl_public_synonym` | O | O | O | O | O |
| `\ddl_table` | O | O | O | O | O |
| `\ddl_constraint` | O | O | O | O | O |
| `\ddl_index` | O | O | O | O | O |
| `\ddl_view` | O | O | O | O | O |
| `\ddl_sequence` | O | O | O | O | O |
| `\ddl_synonym` | O | O | O | O | O |
| `\ddl_procedure` | X | O | O | O | O |
| `\ddl_package` | X | X | O | O | O |
| `\desc ` | O | O | O | O | O |
| `\dynamic sql :var ` | O | O | O | O | O |
| `\exec ` | O | O | O | O | O |
| `\exec :var := :value` | O | O | O | O | O |
| `\exec sql ` | O | O | O | O | O |
| `\explain plan [on\|only] ` | O | O | O | O | O |
| `\help ` | O | O | O | O | O |
| `\history` | O | O | O | O | O |
| `\host {os_command}` | X | O | O | O | O |
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
| `\set sqlprompt ` | X | X | X | X | O |
| `\set timing ` | O | O | O | O | O |
| `\set vertical ` | O | O | O | O | O |
| `\shutdown {abort\|immediate\|transactional\|normal}` | O | O | O | O | O |
| `\startup {nomount\|mount\|open} ` | O | O | O | O | O |
| `\var ` | O | O | O | O | O |

<a id="e1633a343bdcdf3f"></a>
#### gloader/gloadernet

<a id="f3e074bcae1edb10"></a>
##### Command Usage

gloader의 command usage에 대한 feature matrix는 다음과 같다.

**gloader command usage의 feature matrix**

<a id="2ba0c4b28f6c14b0"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| username password | O | O | O | O | O |
| --array | O | O | O | O | O |
| --atomic | O | O | O | O | O |
| --bad | O | O | O | O | O |
| --buffered | O | O | O | O | O |
| --commit | O | O | O | O | O |
| --control | O | O | O | O | O |
| --data | O | O | O | O | O |
| --dsn | O | O | O | O | O |
| --errors | O | O | O | O | O |
| --export | O | O | O | O | O |
| --fieldterm | X | O | O | O | O |
| --filesize | O | O | O | O | O |
| --format | O | O | O | O | O |
| --help | O | O | O | O | O |
| --import | O | O | O | O | O |
| --lineterm | X | O | O | O | O |
| --log | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --parallel | O | O | O | O | O |
| --propagation | O | O | O | O | O |
| --qualifier | X | O | O | O | O |
| --silent | O | O | O | O | O |
| --AsTIMESTAMP | O | O | O | O | O |
| --where | X | O | O | O | O |
| --group-id | X | O | O | O | O |
| --directio-size | X | O | O | O | O |

<a id="e259cc6a96e4df4a"></a>
##### Control File Syntax

gloader의 control file syntax에 대한 feature matrix는 다음과 같다.

**gloader control file syntax의 feature matrix**

<a id="9b29f4c9cb33fc1a"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| CHARACTERSET | O | O | O | O | O |
| FIELDS TERMINATED BY | O | O | O | O | O |
| OPTIONALLY ENCLOSED BY | O | O | O | O | O |
| TABLE table_name | O | O | O | O | O |
| TABLE schema_name.table_name | O | O | O | O | O |
| LTRIM | X | O | O | O | O |
| RTRIM | X | O | O | O | O |
| LINES TERMINATED BY | X | O | O | O | O |
| WHERE | X | O | O | O | O |

<a id="d2280fa01113a2c7"></a>
#### gdump

<a id="3c488f52de34a69a"></a>
##### Command Usage

gdump의 command usage에 대한 feature matrix는 다음과 같다.

<a id="1d0cea2589a70684"></a>
<table class="table column_count_7"><caption>gdump command usage의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="1ee6495cf7c00616"></a>
#### tablediff

<a id="361149f1b3d1f9b7"></a>
##### Configuration File

tablediff의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="997f11e4c962e4f3"></a>
<table class="table column_count_7"><caption>tablediff configuration file의 feature matrix</caption><thead><tr><th class="to_center" colspan="2"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td><div>SOURCE_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td><div>TARGET_PASSWORD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_URL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td><div>TARGET_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_UPDATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TARGET_DELETE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SOURCE_INSERT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td><div>DIFF_BIN_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DIFF_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_CALL_STACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DISPLAY_ROW_UNIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>EXCLUDE_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_DIFF</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOGGING_ON_SUCCESS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_QUEUE_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_THREAD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JOB_UNIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PARTITION_RANGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_OUT_FILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>WHERE_CLAUSE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="ef1a9a15256d0b72"></a>
#### gsyncher

<a id="ee08a069decec2f8"></a>
##### Command Usage

gsyncher의 command usage에 대한 feature matrix는 다음과 같다.

**gsyncher command usage의 feature matrix**

<a id="56aee2d145be5792"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --log | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --home | X | O | O | O | O |
| --copy-right | O | O | O | O | O |
| --backup-path | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="19d6ad7fcdcfbcaa"></a>
#### gmon

<a id="ef182c5993f62bad"></a>
##### Command Usage

gmon의 command usage에 대한 feature matrix는 다음과 같다.

**gmon command usage의 feature matrix**

<a id="a3373a3184cbdbd3"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --status | X | O | O | O | O |
| --home | X | O | O | O | O |
| --uds_dir | X | X | O | O | O |
| --silent | X | O | O | O | O |
| --no-copyright | X | O | O | O | O |
| --help | X | O | O | O | O |

<a id="17f223bea1ccefba"></a>
#### gtrclogger

<a id="59a0493755fc1e0b"></a>
##### Command Usage

gtrclogger의 command usage에 대한 feature matrix는 다음과 같다.

**gtrclogger command usage의 feature matrix**

<a id="e700fe5075081b63"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --dir | X | O | O | O | O |
| --help | X | O | O | O | O |
| --port | X | O | O | O | O |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |

<a id="5e11390e40286791"></a>
#### glocator

<a id="203891f8aa1f5877"></a>
##### Command Usage

glocator의 command usage에 대한 feature matrix는 다음과 같다.

**glocator command usage의 feature matrix**

<a id="7ea15de3858fb6c7"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --create | X | O | O | O | O |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --conf | X | O | O | O | O |
| --status | X | O | O | O | O |
| --sync | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --no-copyright | X | O | O | O | O |
| --help | X | O | O | O | O |

<a id="54b8af6d7fd17792"></a>
##### Configuration File

glocator의 configuration file에 대한 feature matrix는 다음과 같다.

**glocator configuration file의 feature matrix**

<a id="4e7884332ec6bf8e"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | O | O | O | O |
| WORKER_COUNT | X | O | O | O | O |
| SESSION_QUEUE_SIZE | X | O | O | O | O |
| SESSION_ALLOCATOR_SIZE | X | O | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | O | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O | O |
| SYSTEM_UDS_DIR | X | O | O | O | O |
| LOCATION_FILE_DIR | X | O | O | O | O |
| LOCATION_FILE_SIZE | X | O | O | O | O |
| LOCATION_FILE_MAX_SIZE | X | O | O | O | O |
| SESSION_TIMEOUT | X | O | O | O | O |
| FAILOVER_TIMEOUT | X | O | O | O | O |
| ALTERNATE_LOCATORS | X | O | O | O | O |
| SYNC_RETRY_COUNT | X | O | O | O | O |
| SYNC_RESPONSE_TIMEOUT | X | O | O | O | O |

<a id="916c25d812417d5d"></a>
#### gagent

<a id="c0fd6e7362adbd1c"></a>
##### Command Usage

gagent의 command usage에 대한 feature matrix는 다음과 같다.

**gagent command usage의 feature matrix**

<a id="5aa0a5fd1f0bc8bd"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --conf | X | O | O | O | O |
| --status | X | O | O | O | O |
| --home | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --no-copyright | X | O | O | O | O |
| --help | X | O | O | O | O |

<a id="dbee0fea3a9ddf53"></a>
##### Configuration File

gagent의 configuration file에 대한 feature matrix는 다음과 같다.

**gagent configuration file의 feature matrix**

<a id="d85aac5c56568136"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | O | O | O | O |
| LOCATOR_HOST | X | O | O | O | O |
| LOCATOR_PORT | X | O | O | O | O |
| COMMAND_QUEUE_SIZE | X | O | O | O | O |
| COMMAND_ALLOCATOR_SIZE | X | O | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | O | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O | O |
| SESSION_TIMEOUT | X | O | O | O | O |
| UPDATE_LOCATION_TIME | X | O | O | O | O |
| ALTERNATE_LOCATORS | X | O | O | O | O |

<a id="9a662699d00c1f19"></a>
#### gloctl

<a id="653d3f51e08f92f2"></a>
##### Command Usage

gloctl의 command usage에 대한 feature matrix는 다음과 같다.

**gloctl command usage의 feature matrix**

<a id="fd2f9787e19e7e79"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --dsn | X | X | X | X | X |
| --conf | X | O | O | O | O |
| --ip | X | O | O | O | O |
| --port | X | O | O | O | O |
| --import | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --no-copyright | X | O | O | O | O |
| --help | X | O | O | O | O |

<a id="1728261823c68232"></a>
##### Configuration File

gloctl의 configuration file에 대한 feature matrix는 다음과 같다.

**gloctl configuration file의 feature matrix**

<a id="68575cc672ccc33d"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | O | O | O | O |
| LOCATOR_HOST | X | O | O | O | O |
| LOCATOR_PORT | X | O | O | O | O |

<a id="8fe83b82cb691c3e"></a>
### Replication

<a id="d0583cfde5f18b57"></a>
#### cyclone

<a id="b39fea76758d3e39"></a>
##### Command Usage

cyclone의 command usage에 대한 feature matrix는 다음과 같다.

**cyclone command usage의 feature matrix**

<a id="90894e97d46cc5ea"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --encrypt | X | O | O | O | O |
| --group | O | O | O | O | O |
| --help | O | O | O | O | O |
| --key | X | O | O | O | O |
| --master | O | O | O | O | O |
| --reset | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --slave | O | O | O | O | O |
| --start | O | O | O | O | O |
| --status | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --sync | O | O | O | O | O |
| --stand-alone | X | O | O | O | O |
| --recovery | X | O | O | O | O |
| --local | X | O | O | O | O |
| --info | X | O | O | O | O |

<a id="f3b3ef2f7da81677"></a>
##### Configuration File

cyclone의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="8e561876ff795a50"></a>
<table class="table column_count_7"><caption>cyclone configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="12"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HEARTBEAT_TIMEOUT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="17"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SKIP_COMMENT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_FORCE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PACKET_COMPRESSION_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ORACLE_DRIVER</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    O</div></td></tr><tr><td><div>SYNC_MYSQL_DRIVER</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    O</div></td></tr><tr><td><div>SYNC_DB2_DRIVER</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    O</div></td></tr><tr><td><div>SYNC_TIBERO_DRIVER</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    X</div></td><td><div>    O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="14"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>UPDATE_APPLY_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIBERO_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="b659e9a246db8ecb"></a>
#### clustone

Clustone이 deprecate 되었다.

<a id="eb2224d4aecd5ebf"></a>
#### logmirror

<a id="d51eba0d4d2e0097"></a>
##### Command Usage

logmirror의 command usage에 대한 feature matrix는 다음과 같다.

**logmirror command usage의 feature matrix**

<a id="35f13e52542f64c9"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --help | O | O | O | O | O |
| --infiniband | O | O | O | O | O |
| --master | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --slave | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="1d5c05a41de40657"></a>
##### Configuration File

logmirror의 configuration file에 대한 feature matrix는 다음과 같다.

<a id="d4986a45b51f4351"></a>
<table class="table column_count_7"><caption>logmirror configuration file의 feature matrix</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="bedb2a40951abc51"></a>
#### cymon

<a id="17c633af834d4fae"></a>
##### Command Usage

cymon의 command usage에 대한 feature matrix는 다음과 같다.

**cymon command usage의 feature matrix**

<a id="9ec2cfef01c35da4"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --help | O | O | O | O | O |
| --cycle | O | O | O | O | O |
| --key | X | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --status | O | O | O | O | O |

<a id="9c7e895216b4f1c0"></a>
#### cyfile

<a id="dd99895ee356101b"></a>
##### Command Usage

cyfile의 command usage에 대한 feature matrix는 다음과 같다.

**cyfile command usage의 feature matrix**

<a id="a33bbe8dd1e5fdfb"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | X | X | O | O | O |
| --help | X | X | O | O | O |
| --reset | X | X | O | O | O |
| --key | X | X | O | O | O |
| --silent | X | X | O | O | O |
| --info | X | X | O | O | O |
| --start | X | X | O | O | O |
| --stop | X | X | O | O | O |
| --group | X | X | O | O | O |
| --encrypt | X | X | O | O | O |
| --status | X | X | O | O | O |

<a id="1a820de3c3ef182b"></a>
##### Configuration File

cyfile의 configuration file에 대한 feature matrix는 다음과 같다.

**cyfile configuration file의 feature matrix**

<a id="354ec2965e96b5fa"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 | 22c.1 |
| --- | --- | --- | --- | --- | --- |
| DSN | X | X | O | O | O |
| HOST_IP | X | X | O | O | O |
| HOST_PORT | X | X | O | O | O |
| PROTOCOL | X | X | O | O | O |
| USER_ID | X | X | O | O | O |
| USER_PW | X | X | O | O | O |
| GROUP_NAME | X | X | O | O | O |
| USER_ENCRYPT_PW | X | X | O | O | O |
| CAPTURE_TABLE | X | X | O | O | O |
| READ_LOG_BLOCK_COUNT | X | X | O | O | O |
| TRANS_SORT_AREA_SIZE | X | X | O | O | O |
| TRANS_FILE_PATH | X | X | O | O | O |
| LOG_CAPTURE_INTERVAL_1 | X | X | O | O | O |
| LOG_CAPTURE_INTERVAL_2 | X | X | O | O | O |
| DATA_FILE_PATH | X | X | O | O | O |
| DATA_FILE_PREFIX | X | X | O | O | O |
| DATA_FILE_SIZE | X | X | O | O | O |
| UPDATE_BEFORE_VALUE | X | X | O | O | O |

<a id="057d77487f4ceb62"></a>
## What's New in GOLDILOCKS 22c.1

본 장은 GOLDILOCKS 22c.1에 새로 추가된 기능들에 대해 간략히 설명한다.

<a id="de9924022aa36ea0"></a>
### Architecture

<a id="8b9fa08c7709e905"></a>
#### System Architecture

변동 사항 없음

<a id="26721fdd9ebe7398"></a>
#### Storage Internal

변동 사항 없음

<a id="95e37c2ea6994d5f"></a>
#### Transaction Control

변동 사항 없음

<a id="e6250d59957da9f3"></a>
#### Backup & Recovery

변동 사항 없음

<a id="3e8b6e78be0916d0"></a>
#### Database Information

<a id="cd0fdda08ea63643"></a>
##### DICTIONARY_SCHEMA

변동 사항 없음

<a id="e17bfa8c7888697a"></a>
##### INFORMATION_SCHEMA

변동 사항 없음

<a id="4bd98308dc94db64"></a>
##### PERFORMANCE_VIEW_SCHEMA

[V$OPEN_CURSOR](../part-02-administration-manual/9-database-information.md#bf9bc13dda482e1b)가 추가되었다.

[V$PROPERTY_ALIAS](../part-02-administration-manual/9-database-information.md#d3f8dde944bb64df)가 추가되었다.

[V$DB_PROPERTY](../part-02-administration-manual/9-database-information.md#b4b40238a392b16f)가 추가되었다.

[V$LICENSE](../part-02-administration-manual/9-database-information.md#93229538d36ad80a)가 추가되었다.

<a id="dca4c2018063dd39"></a>
#### Server Property

[REBALANCE_SHARD_DIVISOR](../part-02-administration-manual/10-server-property.md#094180606b5040d1)가 추가되었다.

[SESSION_POOL_INIT_SIZE](../part-02-administration-manual/10-server-property.md#9b2d649fa0590efa)가 추가되었다.

[SESSION_POOL_NEXT_SIZE](../part-02-administration-manual/10-server-property.md#7e53a73467a11870)가 추가되었다.

[ADMIN_SESSION_POOL_INIT_SIZE](../part-02-administration-manual/10-server-property.md#bd597ee2b6a74bc7)가 추가되었다.

[ADMIN_SESSION_POOL_NEXT_SIZE](../part-02-administration-manual/10-server-property.md#b59402fc3e1016bf)가 추가되었다.

[DEFAULT_INDEX_PCTFREE](../part-02-administration-manual/10-server-property.md#27b5f38a51f795ff)의 기본값이 10으로 변경되었다.

[DEFAULT_MAXTRANS](../part-02-administration-manual/10-server-property.md#2234f2bb86cf064c)의 기본값이 32로 변경되었다.

시스템의 증분 백업 수행을 위한 기준을 설정하는 기존 프로퍼티 INCREMENTAL_CHECKPOINT_CRITERIA의 이름이 [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#f27cdd06cf3054f4)로 변경되고 기본값도 0으로 변경되었다.

디스크 테이블스페이스를 위한 버퍼 관리 알고리즘을 개선하기 위해 [BUFFER_LRU_SCAN_PERCENT](../part-02-administration-manual/10-server-property.md#7fa83b9ff039b574) 프로퍼티가 추가되었다.

클러스터 환경에서 통신 버퍼 수를 지정하는 CLUSTER_CM_BUFFER_COUNT 프로퍼티가 deprecate되었다. 이를 대신하여 lockable, lockless, synchronization dispatcher를 위한 통신 버퍼 수를 지정하는 [LOCKABLE_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#eebec07b2adc98c5), [LOCKLESS_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#4a41ec8105158e4d), [SYNC_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#81fa17bd408ab6a5) 프로퍼티가 추가되었다.

디스크 테이블스페이스에 생성된 테이블을 전체 스캔할 때 버퍼에 캐싱할지 여부는 테이블 크기의 threshold에 따라 결정된다. 이 threshold 값을 설정하기 위해 [FULL_TABLE_SCAN_CACHING_THRESHOLD](../part-02-administration-manual/10-server-property.md#19cf338782b55190) 프로퍼티가 추가되었다.

Hash instant table의 예상 bucket count의 최대값을 설정하는 [INST_HASH_TABLE_BUCKET_MAX_COUNT](../part-02-administration-manual/10-server-property.md#097f27d8b9f9ca78) 프로퍼티가 추가되었다.

Plan cache에 캐싱할 SQL의 최대 개수를 제한하는 두 개의 property 중에 MAXIMUM_FLANGE_COUNT property는 deprecate 하고 [PLAN_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#211c5592125ca84f) 만으로 제어하도록 했다.

인덱스 구축 및 재구축시 발생하는 로그의 기록 속도를 제어할 수 있는 [INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#7bf6de118a3fa6de) 프로퍼티가 추가되었다.

<a id="dc98e82e89fe638b"></a>
### SQL

<a id="4450db2d9a75dd47"></a>
#### SQL Element

<a id="733be79040eb92c3"></a>
##### Data Type

변동 사항 없음

<a id="321ecb8133a2f808"></a>
##### Function

[DISTINCT Condition](../part-03-sql-manual/11-sql-elements.md#d251b0d782b872e6)이 추가되었다.

[SESSIONTIMEZONE](../part-03-sql-manual/17-built-in-function-references.md#2fc1c7ed2c2b786a)이 추가되었다.

[Window Function](../part-03-sql-manual/11-sql-elements.md#93c30dc4e927cb60)이 추가되었다.

<a id="ece3eab8ab65b984"></a>
#### Object

<a id="c760731aceb7a142"></a>
##### SQL Object

변동 사항 없음

<a id="aff2e6ecf6f3b89a"></a>
##### Cluster Object

[ALTER DATABASE DROP OFFLINE SEGMENTS](../part-03-sql-manual/18-sql-references-a-b.md#a56d9b8313449047) 구문이 추가되었다.

[ALTER DATABASE SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#7358cd448c66ad8b) 구문이 추가되었다.

[ALTER TABLE name DROP OFFLINE SEGMENTS](../part-03-sql-manual/18-sql-references-a-b.md#12188ac1593e923a) 구문이 추가되었다.

[ALTER TABLE name SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#c03af2d66eb7e9c7) 구문이 추가되었다.

[ALTER DATABASE MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#5068226dae906bd2), [ALTER DATABASE REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#f07ba634c9eef9cf), [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](../part-03-sql-manual/18-sql-references-a-b.md#66647a34894da55f), [ALTER TABLE name MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#a93d376fd2ef5b9b), [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#149294331f00fde7), [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](../part-03-sql-manual/18-sql-references-a-b.md#21c0fa70c04ce272) 구문들에 SHARD DIVISOR와 PARALLEL 옵션이 추가되었다.

ALTER TABLE REBUILD GLOBAL SECONDARY INDEX 구문이 [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#683708e586c10608)로 변경되었다.

<a id="65c7a2422e0a42ed"></a>
#### SQL Language

<a id="6e4f38b5b5b3dc15"></a>
##### DML

변동 사항 없음

<a id="cb0fc0629abdf124"></a>
##### Query

<a id="1786fd0bcc5a48c9"></a>
###### **Lateral Inline View**

[from clause](../part-03-sql-manual/20-sql-references-h-z.md#e3dedc5dda5dbad1)에 lateral inline view가 추가되었다.

<a id="4d5e370feadd5eb4"></a>
###### **Table Function Derived Table**

[from clause](../part-03-sql-manual/20-sql-references-h-z.md#e3dedc5dda5dbad1)에 table function derived table이 추가되었다.

<a id="3f87a34b14e3ae26"></a>
###### **WINDOW 절**

Window function의 수행 범위를 정의하는 WINDOW 절이 추가되었다.  
자세한 내용은 [window clause](../part-03-sql-manual/20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="38f697fd029d0611"></a>
##### Control Language

변동 사항 없음

<a id="c0e016a844f14518"></a>
#### PSM Language

<a id="fba29abb65604090"></a>
##### Table Function

[return clause](../part-04-psm-manual/29-psm-sql-references.md#59f36887c4d3edff)에 TABLE ( table function column list ) 문이 추가되었다.  
Function DDL 시 table type을 정의하여 table function을 생성할 수 있다.  
자세한 내용은 [CREATE FUNCTION](../part-04-psm-manual/29-psm-sql-references.md#ab87224881e1ecca)을 참조한다.

<a id="6db79ea3917f16d1"></a>
##### RETURN TABLE Statement

PSM statement에 [RETURN TABLE Statement](../part-04-psm-manual/28-psm-language-element-references.md#330d6da944781f1f)가 추가되었다.

<a id="452940accb4dd190"></a>
##### PSM Statement 성능 개선

다음과 같이 PSM statement의 성능이 개선되었다.

<a id="811d378696523058"></a>
![](../assets/images/e644f769bb3d3f2d.png)

<a id="056da505354988d6"></a>
### API

<a id="4f13008fcda7f233"></a>
#### ODBC

[데이터 원본 구성](../part-05-developer-manual/31-odbc.md#38509fa109f62339)에 TRACE_POLICY가 추가되었다.

<a id="cd08e92bf0ccaba1"></a>
#### JDBC

Time과 timestamp 타입을 문자열로 출력할 때 마이크로 초 단위가 손실되지 않도록 수정되었다.

Auto-generated key를 지원한다.

GoldilocksTypes.REF_CURSOR가 추가되었다.

JDBC 비 표준 함수인 GoldilocksPreparedStatement.setFixedCHAR()가 추가되었다.

<a id="8f3c1fb8997530f4"></a>
#### Embedded SQL

<a id="d997a6127e8b841b"></a>
##### Precompiler Option

gpec에 [--parse](../part-05-developer-manual/33-embedded-sql.md#e5309daff797b6e7) 옵션이 추가되었다.

<a id="9788110710c1dc9d"></a>
##### Embedded SQL 전용 구문

gpec에서 [함수 인자 선언](../part-05-developer-manual/33-embedded-sql.md#7c811efe04803265)을 지원한다.

<a id="ae7e0e34430a9b65"></a>
#### PDO

변동 사항 없음

<a id="31b69a59b474b208"></a>
#### PyDBC

변동 사항 없음

<a id="214e982aee4a2b6f"></a>
#### Ruby

변동 사항 없음

<a id="98f7f9e46ed266a4"></a>
#### Hibernate

변동 사항 없음

<a id="be0c8deff8ba22a7"></a>
### Utility

<a id="3fa49f2d593b490a"></a>
#### gcreatedb

변동 사항 없음

<a id="1df72ea2f14a73ef"></a>
#### glsnr

변동 사항 없음

<a id="7842107deb17e562"></a>
#### gsql/gsqlnet

`\`set sqlprompt 명령어가 추가되었다.

<a id="c9581458973f7673"></a>
#### gloader/gloadernet

변동 사항 없음

<a id="228a669235b77f8e"></a>
#### gdump

변동 사항 없음

<a id="1e7562efa8426d5e"></a>
#### tablediff

변동 사항 없음

<a id="42afea825a71348a"></a>
#### gsyncher

변동 사항 없음

<a id="583143fc45b8447e"></a>
#### gmon

변동 사항 없음

<a id="3daccca62c93060c"></a>
#### gtrclogger

변동 사항 없음

<a id="5ea1663bf67746a8"></a>
#### glocator

변동 사항 없음

<a id="22a06071aaf3d5ed"></a>
#### gagent

변동 사항 없음

<a id="79173fbbdde99026"></a>
#### gloctl

변동 사항 없음

<a id="c62b9e118e62a9f2"></a>
### Replication

<a id="edea5d28545160b1"></a>
#### cyclone

Oracle, DB2, MySQL, Tibero 등 타 DB로 데이터를 이전하는 기능을 추가하였다.

<a id="d1ab2d61e655a6b4"></a>
#### logmirror

변동 사항 없음

<a id="f3ca0364a0324d9c"></a>
#### cymon

변동 사항 없음

<a id="012d395c3123218d"></a>
#### cyfile

변동 사항 없음

<a id="85597e86f435c568"></a>
## Patch Notes

<a id="04484c3b0bc3a5aa"></a>
### 22c.1.10 Patch Notes

<a id="68404f8a69ac526b"></a>
#### <kbd>ISSUE-7939</kbd> 변별력이 낮은 composite index 추가 시, 기존에 index scan 하던 query를 full scan 하게 되어 이를 수정하였다.

<a id="b83a8e71574f70ae"></a>
##### 개요

변별력이 낮은 composite index를 추가하면 기존에 index scan 하던 query가 full scan을 수행하는 문제가 발생하여 이를 수정하였다.   
단, 이 문제는 다음 조건을 모두 만족하는 경우에 발생한다.  
• 기존에 사용되던 인덱스가 composite index일 것  
• index key column 전체에 대해 '=' 조건이 존재하지 않고 일부 column에만 '=' 조건이 적용될 것

<a id="450cb73b13e98fad"></a>
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

<a id="d360fc91fb1bb57a"></a>
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

<a id="69144adf9fdcbd2f"></a>
### 22c.1.9 Patch Notes

<a id="cf4376d1a0017549"></a>
#### <kbd>ISSUE-7805</kbd> ODBC의 LONG VARCHAR, LONG VARBINARY 타입 처리 과정에서 할당된 메모리가 정상적으로 해제되지 않는 문제가 있어 이를 수정하였다.

<a id="0c9e5557eaca3cfa"></a>
##### 개요

FETCH 작업 중인 테이블의 스키마 구조가 변경된 뒤 동일 테이블에 대해 다시 FETCH 작업을 수행할 경우, 메타데이터 재구축 과정에서 LONG VARCHAR, LONG VARBINARY 타입 column에 대해 메모리 누수가 발생하였다.

<a id="4f0df6f2ab1d734b"></a>
##### 현상 및 증상

클라이언트-서버 (CS) 환경에서 ODBC를 사용해 데이터를 조회하는 과정에서, FETCH 작업 도중 해당 테이블에 대해 ALTER 구문으로 테이블 구조가 변경되면 메타데이터를 재구축한다. 이 때 테이블에 LONG VARCHAR, LONG VARBINARY 타입 column이 존재하면 해당 column 타입에 대해 동적으로 할당된 메모리가 해제되지 않아 메모리 누수가 발생하였다.

<a id="c4ebe3415e1f4d7b"></a>
##### 수정 전 대처

이 문제가 수정되기 전까지는 fetch 작업 중 테이블 구조를 변경하지 않는 것이 가장 안정적인 방법이다. 부득이하게 테이블 구조가 변경되는 경우에는 해당 SQLHSTMT 핸들에 대해 SQLFreeHandle을 호출한 뒤, SQLAllocHandle 다시 수행하여 핸들을 재할당해야 한다.

<a id="5147aac66ba4cfaf"></a>
### 22c.1.8 Patch Notes

<a id="448920f5729015a3"></a>
#### <kbd>ISSUE-7782</kbd> gpec에 parse 옵션을 추가하였다.

<a id="d2266afb3bf0eacc"></a>
##### 개요

gpec에 소스 파싱 동작을 제어하기 위한 parse 옵션을 추가하였다. 해당 옵션값으로 none 또는 partial을 지정할 수 있으며, 별도로 지정하지 않을 경우 기본값은 partial이다.

<a id="8b01544e50541287"></a>
##### 현상 및 증상

없음

<a id="d79a634ac52c20f3"></a>
##### 수정 전 대처

없음

<a id="9d3ca80df919bff7"></a>
#### <kbd>ISSUE-7782</kbd> gpec 전처리기의 코드 처리 방식을 수정하였다.

<a id="118b22480e2fa993"></a>
##### 개요

gpec 전처리기에서 조건이 false로 평가되는 전처리기 분기 (#if, #elif, #else, #ifdef, #ifndef)에 포함된 코드의 처리 방식이 변경되었다.   
기존에는 false 조건에 해당하는 코드를 출력 결과에서 제거하였으나, 패치 이후에는 해당 코드를 삭제하지 않고 그대로 출력하도록 수정하였다.

<a id="b2a7d6647affe157"></a>
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

<a id="d926983c71cf93ce"></a>
##### 수정 전 대처

gc 파일에서 사용하는 전처리 조건과 매크로는 EXEC SQL INCLUDE로 포함되는 헤더 파일 내에서 정의되도록 구성한다.

<a id="e14002301b43f381"></a>
#### <kbd>ISSUE-5401</kbd> cyclone recovery 과정 중에도 conflict 이외의 에러가 발생하면 출력하도록 변경하였다.

<a id="807785bbf9952009"></a>
##### 개요

기존에는 recovery 과정에서 trace log에 에러를 기록하지 않아 conflict 이외의 에러를 확인할 수 없는 문제가 있어, 이를 수정하였다.

<a id="76d1107bc89c445b"></a>
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

<a id="a667b74994da9817"></a>
##### 수정 전 대처

없음

<a id="6853a59b10f3ef5b"></a>
#### <kbd>ISSUE-6503</kbd> Cyclone에 Oracle, DB2, MySQL, Tibero 등 타 DB로 데이터를 이전할 수 있는 기능을 추가하였다.

<a id="c49778ec73529e6f"></a>
##### 개요

기존에는 slave가 GOLDILOCKS인 경우에만 데이터 동기화가 가능했지만 기능 확장을 통해 slave가 Oracle, DB2, MySQL, Tibero인 경우에도 데이터 동기화를 수행할 수 있도록 하였다.

<a id="02be120280194a77"></a>
##### 현상 및 증상

Slave의 target DB가 GOLDILOCKS가 아닌 경우에는 SYNC 기능이 동작하지 않았다.

<a id="676b7a23e30f14d5"></a>
##### 수정 전 대처

없음

<a id="b30babfbbf1acdce"></a>
#### <kbd>ISSUE-7743</kbd> gpec 전처리기에서 중첩된 #if / #endif 구문을 처리하는 과정에서 발생하던 오류를 수정하였다.

<a id="cc2558eca2988b01"></a>
##### 개요

gpec 전처리기는 #if 전처리기 구문을 처리할 때, 조건이 false 로 평가되면 해당 #endif 구문까지의 모든 문장을 제거 (빈 문자열로 치환)한다.  
그러나 #if / #endif 구문이 중첩되어 사용되는 경우, 내부 전처리기 블록에 포함된 일부 문장이 정상적으로 제거되지 않는 오류가 확인되어 이를 수정하였다.  
본 수정 사항은 #if 구문뿐만 아니라 #elif, #else, #ifdef, #ifndef 등 모든 조건부 전처리기 구문에 동일하게 적용된다.

<a id="e30d657ba9f48b99"></a>
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

<a id="30aa32e2ad656002"></a>
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

<a id="96b873e5fc5d3d7c"></a>
#### <kbd>ISSUE-7660</kbd> IPC 사용 중에 idle timeout 이 발생했을 때 gserver 가 종료되지 않는 문제가 있어 이를 수정하였다.

<a id="8b4ccde06afec021"></a>
##### 개요

IPC 사용 중에 idle timeout이 발생하면 gserver가 세션을 정리하지만, 클라이언트 종료를 계속 기다리는 바람에 gserver 프로세스가 종료되지 않고 남아 있는 문제가 있어 이를 수정하였다.

<a id="be27383921480cd6"></a>
##### 현상 및 증상

IPC 사용 중에 idle timeout 이 발생하여 세션이 정리되었다는 trace log가 출력되었다.

```
[2025-12-01 17:52:02.791208 INSTANCE(GOLDILOCKS) THREAD(1554791,139737737000768)] [INFORMATION]
[DEDICATE_SERVER] ERR-HYT00(13038): Exceeded maximum idle time

[2025-12-01 17:52:02.836570 INSTANCE(GOLDILOCKS) THREAD(1554720,139906736981760)] [WARNING]
[CLEANUP] cleaning local session - env(12), session(13.8), local transaction(-1), program(gsqlnet), pid(1554791), thread(139737737000768)

[2025-12-01 17:52:02.836641 INSTANCE(GOLDILOCKS) THREAD(1554720,139906736981760)] [WARNING]
[CLEANUP] cleaning up 1 sessions
```

그러나 gserver 프로세스는 여전히 종료되지 않고 살아있는 상태로 남아 있다.

```
% ps -ef | grep gserver | grep ipc
goldilocks    1554791    7156  0 17:52 pts/1    00:00:00 gserver --dedicated /tmp/unix-glsnr.11100.0 -x 2 --ipc
```

<a id="067bd3e017339143"></a>
##### 수정 전 대처

클라이언트 프로세스를 수동으로 종료하면 gserver 프로세스도 종료된다.

<a id="15e5bb2049bb2462"></a>
#### <kbd>ISSUE-7365</kbd> Cymon을 이용한 Cyclone 모니터링 정보에 새로운 항목이 추가되었다.

<a id="e5e117fb2c774292"></a>
##### 개요

CYCLONE_MONITOR_INFO 테이블의 MASTER_STATE, SLAVE_STATE에 기존 상태 (N/A, READY, RUNNING) 외에 SYNCING 상태가 추가되었다. 이 SYNCING 상태는 --sync 옵션으로 데이터 동기화가 진행 중일 때 표시된다.

```
gSQL> \set vertical on
gSQL> select * from cyclone_monitor_info;
              GROUP_NAME # GROUP1
                    TIME # 2025-10-14 12:03:02
            MASTER_STATE # SYNCING
             SLAVE_STATE # SYNCING
             MASTER_PORT # 21102
                SLAVE_IP # 127.0.0.1
        REDO_LOG_FILESEQ # 0
       REDO_LOG_BLOCKSEQ # 101423
         CAPTURE_FILESEQ # 0
        CAPTURE_BLOCKSEQ # 0
           APPLY_FILESEQ # 0
          APPLY_BLOCKSEQ # 0
        CAPTURE_INTERVAL # 101423
   CAPTURE_INTERVAL_SIZE # 51928576
          TOTAL_TX_COUNT # 0
        CAPTURE_TX_COUNT # 0
      CAPTURE_COMMIT_LSN # 0
        APPLY_COMMIT_LSN # 0
```

<a id="b8b42f8cb950f5b4"></a>
##### 현상 및 증상

없음

<a id="9a1922e09f8891c2"></a>
##### 수정 전 대처

없음

<a id="95891710430f9514"></a>
#### <kbd>ISSUE-7633</kbd> SUPPLEMENTAL_LOG_FORCE_MODE 환경변수를 추가하였다.

<a id="540d5477bcfa3c3d"></a>
##### 개요

CYCLONE 실행 시 이중화 대상 table에 supplemental logging이 비활성화되어 있는 경우, SUPPELEMENTAL_LOG_FORCE_MODE를 1(Enable)로 설정하면 해당 테이블의 supplemental logging을 강제로 활성화한 후 이중화를 시작한다.

<a id="776488e78df07c7c"></a>
##### 현상 및 증상

없음

<a id="3c75c500f237cb6b"></a>
##### 수정 전 대처

없음

<a id="8289e8c2c74f3313"></a>
### 22c.1.7 Patch Notes

<a id="2022e893125a889a"></a>
#### <kbd>ISSUE-7412</kbd> Instant hash table의 column이 두 개 이상의 페이지에 걸쳐 저장될 경우, 해당 column을 제대로 읽지 못하는 문제가 있어 이를 수정하였다.

<a id="b8e935966a6e0ef1"></a>
##### 개요

Instant hash table의 column이 두 개 이상의 페이지에 걸쳐 저장될 경우, 해당 column을 제대로 읽지 못하거나 필터가 적용되지 않는 문제가 있어 이를 수정하였다.

<a id="ec05fdc33da50027"></a>
##### 현상 및 증상

예를 들어, 아래와 같은 질의를 수행했을 때 name1과 name2의 값은 항상 같아야 하지만, (null, 5)와 같이 서로 다른 값이 출력되는 문제가 발생한다.

```
SELECT *
  FROM
(
SELECT RTRIM( name1 )
     , RTRIM( name2 )
  FROM ( SELECT CAST( level AS CHAR( 2000 ) ) AS name1
              , CAST( level AS CHAR( 2000 ) ) AS name2
           FROM dual
           CONNECT BY level <= 5
         UNION DISTINCT
         SELECT 'X' AS name1
              , 'X' AS name2
           FROM dual
       )
) ORDER BY 1;

RTRIM( NAME1 ) RTRIM( NAME2 )
-------------- --------------
1              1             
2              2             
3              3             
4              4             
X              X             
null           5             

6 rows selected.
```

<a id="d356ae34c1b259bf"></a>
##### 수정 전 대처

없음

<a id="405117d67b1c67b2"></a>
#### <kbd>ISSUE-7353</kbd> ODBC fetch 중 배열 크기 변경 시 데이터가 누락되는 문제가 있어 이를 수정하였다.

<a id="42a19eee9b7a6ef0"></a>
##### 개요

ODBC 클라이언트-서버 환경에서 데이터 fetch 도중 배열 크기(array size) 를 동적으로 변경할 때 발생하는 데이터 조회 실패 문제를 수정하였다.

<a id="29b82d26bfbe141b"></a>
##### 현상 및 증상

클라이언트-서버(CS) 환경에서 ODBC를 사용하여 데이터를 조회할 때, fetch 작업 도중 배열 크기를 변경하면 데이터를 정상적으로 가져오지 못하는 문제가 발생했다. 이 문제는 SQLExtendedFetch, SQLFetch, SQLFetchScroll 함수를 사용할 때 공통적으로 나타났으며, 특히 작은 배열 크기(예: 1건) 로 fetch를 시작한 후 큰 배열 크기(예: 100건) 로 변경하는 경우에 발생했다.

구체적인 증상으로는 SQL_ROWSET_SIZE 또는 SQL_ATTR_ROW_ARRAY_SIZE 속성을 변경한 후, 실제로는 더 많은 데이터가 존재함에도 불구하고 SQL_NO_DATA가 조기에 반환되어 일부 데이터만 조회되는 현상이 있었다.

<a id="abb28a1ebba14a6d"></a>
##### 수정 전 대처

이 문제가 수정되기 전까지는 fetch 작업 중 배열 크기를 변경하지 않고 고정된 크기로 유지하는 것이 가장 안정적인 방법이다. 만약 배열 크기를 반드시 변경해야 하는 경우라면, SQLCloseCursor 함수를 사용하여 현재 커서를 닫은 후에 쿼리를 다시 실행하여 새로운 배열 크기로 처음부터 fetch를 수행해야 한다. 성능보다 안정성이 중요한 경우에는 배열 크기를 1로 고정하여 단일 행 씩 fetch 하는 방법을 사용할 수 있다.

<a id="92c8e13b0cba9b89"></a>
### 22c.1.6 Patch Notes

<a id="15271a34d24911f7"></a>
#### <kbd>ISSUE-7094</kbd> 라이선스의 CPU 개수 제한에 대한 NUMA_MAP 처리 방식이 개선되었다.

<a id="bdba5ab50dc7a00b"></a>
##### 개요

기존에는 실행 장비의 전체 CPU 개수가 라이선스에 명시된 허용 개수를 초과하면, 실제 사용하는 CPU 수와 관계없이 라이선스 오류가 발생했습니다. 그러나 일부 CPU만 선택적으로 사용하고자 하는 요구가 있어, goldilocks.properties.conf 파일의 NUMA_MAP 설정을 통해 실사용 CPU 수가 라이선스 허용 범위 이내인 경우에는 실행이 가능하도록 정책이 변경되었다.

<a id="c7bdf5ae494c8bf2"></a>
##### 현상 및 증상

실행 장비의 전체 CPU 개수가 라이선스에 명시된 허용 개수를 초과하면 프로그램은 라이선스 위반으로 판단하여 에러를 발생시켰다. 이에 사용자가 NUMA_MAP을 통해 사용 CPU를 제한하더라도 프로그램은 장비 전체의 CPU 수를 기준으로 라이선스를 검증했기 때문에 실행이 차단되었다.

<a id="d3e3c50493f5c982"></a>
##### 수정 전 대처

없음

<a id="846d1286df9f87ea"></a>
#### <kbd>ISSUE-7045</kbd> RETURNING LONG VARCHAR를 포함한 JSON aggregation 함수를 GROUP BY와 함께 사용하는 데 있었던 제약이 제거되었다.

<a id="6657252b2d2c5210"></a>
##### 개요

RETURNING LONG VARCHAR를 포함한 JSON aggregation 함수를 GROUP BY와 함께 사용할 수 없었던 제약을 제거하였다.

<a id="ed37bdc3be11a9e9"></a>
##### 현상 및 증상

다음과 같이 RETURNING LONG VARCHAR를 포함한 JSON aggregation 함수를 GROUP BY와 함께 사용할 경우 에러가 발생하였다.

```
CREATE TABLE t1 ( id INTEGER, data VARCHAR(1500) );
INSERT INTO t1 VALUES ( 1, 'A' );
INSERT INTO t1 VALUES ( 1, 'B' );
INSERT INTO t1 VALUES ( 2, 'A' );
INSERT INTO t1 VALUES ( 2, 'B' );
INSERT INTO t1 VALUES ( 2, 'C' );
INSERT INTO t1 VALUES ( 2, 'D' );
INSERT INTO t1 VALUES ( 3, RPAD( 'A', 1500, '_' ) );
INSERT INTO t1 VALUES ( 3, RPAD( 'B', 1500, '_' ) );
INSERT INTO t1 VALUES ( 3, RPAD( 'C', 1500, '_' ) );
COMMIT;

gSQL>
SELECT id
     , JSON_ARRAYAGG( data RETURNING LONG VARCHAR ) AS json_result
  FROM t1
 WHERE id <= 3
 GROUP BY id
;

ERR-42000(16246): illegal use of LONG VARCHAR data type : 
     , JSON_ARRAYAGG( data RETURNING LONG VARCHAR ) AS json_result
       *
ERROR at line 2:
```

수정 후에는 다음과 같이 제약없이 사용할 수 있다.

```
gSQL>
SELECT id, JSON_OBJECTAGG( 'data' VALUE data RETURNING LONG VARCHAR ) AS json_string
  FROM t1
 WHERE id <= 3
 GROUP BY id
 ORDER BY id
;

ID
--
JSON_STRING                                                                                         
----------------------------------------------------------------------------------------------------
 1
{"data":"A","data":"B"}                                                                             
 2
{"data":"A","data":"B","data":"C"}                                                                  
 3
{"data":"A___
...
중략
...
_________","data":"B______
...
중략
...
_______","data":"C_____
...
중략
...
________"}                                                                     

3 rows selected.
```

<a id="007fd707eab5b7cd"></a>
##### 수정 전 대처

다음과 같이 FROM 절을 ORDER BY 를 포함한 in-line view 로 변경한다.

```
gSQL>
SELECT id, JSON_ARRAYAGG( data RETURNING LONG VARCHAR ) AS json_string
  FROM ( SELECT id, data
           FROM t1
          WHERE id <= 3
          ORDER BY id
       )
 GROUP BY id
;

ID
--
JSON_STRING                                                                                         
----------------------------------------------------------------------------------------------------
 1
["A","B"]                                                                                           
 2
["A","B","C"]                                                                                       
 3
["A____________________________________
...
...
중략
...
...
________"]                                                                                          

3 rows selected.
```

<a id="ac076ddcfe6c9eba"></a>
### 22c.1.5 Patch Notes

<a id="d3a4954c44c0a1fe"></a>
#### <kbd>ISSUE-6974</kbd> JSON string constructor 함수를 추가하였다.

<a id="b852b2fba7ed55f4"></a>
##### 개요

[JSON String Constructor](../part-03-sql-manual/11-sql-elements.md#30f24d7eebfaa3e9) 함수를 추가하였다.

<a id="50c7b5cf024e5e67"></a>
##### 현상 및 증상

없음

<a id="a51de38fbbc19306"></a>
##### 수정 전 대처

없음

<a id="703a1b0e495538cd"></a>
#### <kbd>ISSUE-6157</kbd> 4K disk sector를 지원한다.

<a id="c4edbd6b97936868"></a>
##### 개요

최근 출시되는 HDD에서 채택하고 있는 4096 byte (4K advanced format)의 disk sector size를 지원한다.

<a id="305877f5ebeb7105"></a>
##### 현상 및 증상

DIRECT_IO가 512 byte로 define 되어 있어 최근 출시되는 HDD의 disk sector size인 4096 byte (4K advanced format)을 지원하지 못하였으나 이를 지원하도록 수정하였다.

<a id="ff387e767cf0f172"></a>
##### 수정 전 대처

없음

<a id="e7bfa652e08fdfca"></a>
#### <kbd>ISSUE-6939</kbd> IN KEY RANGE scan 시 offset limit 구문을 사용하면 결과에 오류가 발생한다.

<a id="b9b29c5a2a487486"></a>
##### 개요

OFFSET 구문이 포함된 질의를 수행할 때 IN KEY RANGE을 이용하면 결과에 오류가 발생하여 이를 수정하였다.

<a id="d845b6d9367defa2"></a>
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

<a id="61b42083ebe01c4f"></a>
##### 수정 전 대처

없음

<a id="b4e58acafb5a867a"></a>
#### <kbd>ISSUE-6845</kbd> Partial rollback 시 giveup 정보 초기화 누락으로 인한 처리 오류가 발생한다.

<a id="37705b238e301a99"></a>
##### 개요

Partial rollback을 수행하는 도중에 giveup 발생하면 giveup 관련 변수들을 초기화 하지 않는 문제가 있었다. 이 문제를 해결하기 위해 giveup 도 partial rollback 처리되도록 수정하였다.

<a id="efce4015d96cd9d2"></a>
##### 현상 및 증상

정상적으로 partial rollback이 이루어져야 하는 상황에서 giveup 정보가 남아있어, 의도하지 않은 giveup 이 발생한다.

<a id="e8b9d4c472f8a451"></a>
##### 수정 전 대처

없음

<a id="0b5cfb3abd339183"></a>
#### <kbd>ISSUE-6803</kbd> 잘못된 segment hint 메모리에 접근할 수 있다.

<a id="e5ff6dbdc0ae1a66"></a>
##### 개요

Segment hint cache의 replacement 발생 횟수가 signed integer 범위 (2147483647)를 초과하면, segment hint 메모리 공간을 벗어나 메모리를 읽거나 쓸 수 있다. 이로 인해 segment fault 및 비정상적인 동작이 발생할 수 있어, 해당 문제를 수정하였다.

<a id="89837f996c3d4368"></a>
##### 현상 및 증상

할당된 메모리 범위를 벗어나 읽거나 쓸 수 있으며, 이 경우 segment fault 및 비정상적인 동작을 유발할 수 있다.

<a id="8a2da61905d92045"></a>
##### 수정 전 대처

없음

<a id="5faf9db0e84aa5af"></a>
#### <kbd>ISSUE-6797</kbd> Gmaster의 session fatal은 system fatal로 처리한다.

<a id="41c660be18007a77"></a>
##### 개요

Gmaster thread에서 session fatal이 발생하면 hang이 걸려 정상적인 cleanup이 불가능하므로 system fatal로 처리한다.

<a id="ef6a0bdad9ef368e"></a>
##### 현상 및 증상

Gmaster thread에서 session fatal이 발생하면 hang이 걸리는 문제가 발생한다.

<a id="20a70433c5a0ee5c"></a>
##### 수정 전 대처

없음

<a id="67c7f3d6599825f5"></a>
#### <kbd>ISSUE-6687</kbd> Redo log member가 다중화되어 있을 경우, redo log switch 이후 cyclone이 다음 redo log를 읽지 못하는 현상이 발생한다.

<a id="aa0a0738884a72c6"></a>
##### 개요

Redo log member가 다중화되어 있을 경우, log switch 이후 cyclone이 이를 정상적으로 처리하지 못하는 현상이 발생하여 이를 수정하였다.

<a id="2bb5f52d050f36f1"></a>
##### 현상 및 증상

이중화가 이루어지지 않고, cyclone이 지속적으로 다음 파일을 기다리는 현상이 발생한다.

<a id="dd96dab14708e63f"></a>
##### 수정 전 대처

Redo log member를 제거하고 cyclone을 재실행한다.

<a id="2f8f923e6587e615"></a>
#### <kbd>ISSUE-6605</kbd> UPSERT statement에서 RETURING 절을 사용하면 결과에 오류가 발생한다.

<a id="5b4fdd7683906fe1"></a>
##### 개요

UPSERT statement에서 RETURNING 절을 사용할 경우, 중복된 키 값이 존재하지 않아 INSERT 연산이 수행될 때 결과에 오류가 발생한다.

<a id="cacc7ab6221b147a"></a>
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

<a id="8f3f651fbd3ffc57"></a>
##### 수정 전 대처

없음

<a id="36037e8884feb69f"></a>
#### <kbd>ISSUE-6575</kbd> Fetch statement의 INTO 절에 record type variable의 field만 명시하면 에러가 발생한다.

<a id="0c4bb4fdd337f708"></a>
##### 개요

Fetch statement에 fetch 하려는 cursor의 target 수와 INTO 절의 target 수가 동일함에도 record type variable의 field를 명시하면 에러가 발생한다.

<a id="c2014f9d64d73c69"></a>
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

<a id="ef8a2e47c8a84afc"></a>
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

<a id="4876919d1afd9d6e"></a>
#### <kbd>ISSUE-6557</kbd> Outer join을 사용할 때, where 절에 right table의 column이 포함된 DECODE, stored function, concat과 같은 함수가 존재하면 잘못된 결과가 도출될 수 있다.

<a id="b483199eb9169d9e"></a>
##### 개요

Where 절에 right table의 column이 포함된 DECODE, stored function, concat과 같은 함수가 존재할 경우, 아래와 같은 outer join operation elimination이 적용되어서는 안 되지만 실제로는 적용되는 문제가 발생했다.

- Left outer join이 inner join으로 transform 되었다.
- Full outer join이 left outer join으로 transform 되었다.

<a id="0f02fa5302b11cc7"></a>
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

<a id="3b8967ab6e3507c0"></a>
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

<a id="df4436acb2f14e2e"></a>
#### <kbd>ISSUE-6537</kbd> CAST( 'ABCDE' AS CHAR(3) ) 와 같이 string type 간에 cast 연산 시, source value가 dest precision 보다 크면 에러가 발생한다.

<a id="9405a7e0ae57714d"></a>
##### 개요

CAST( 'ABCDE' AS CHAR(3) ) 와 같이 string type 간에 cast 연산 시, source value가 dest precision 보다 크면 에러가 발생한다.

이 경우, 변환하려는 string type의 precision에 맞춰 truncate 하여 cast 연산이 수행되게 한다.

<a id="df491d29eb699e0f"></a>
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

<a id="997ff15181e59257"></a>
##### 수정 전 대처

변환하려는 string type의 precision을 source value가 포함될 수 있는 크기로 지정한다.

<a id="ae6451766a6cd87a"></a>
#### <kbd>ISSUE-6536</kbd> Bulk logging 으로 인한 DML jitter 현상을 제거하였다.

<a id="dc01a3a53bd17928"></a>
##### 개요

Online index rebuild 중에 발생한 대량의 로그로 인해 DML에서 jitter가 발생하는 현상을 제거하였다.

<a id="9364ce6297735d12"></a>
##### 현상 및 증상

대량 로그는 log flusher를 느리게 만들고 이로 인해 online index rebuild가 lock을 잡고 있는 시간이 늘어나 DML 지연 현상을 유발할 수 있다.

[INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#7bf6de118a3fa6de) 프로퍼티를 새로 추가하였다. 이를 이용하면 index rebuild 시 대량 로그가 짧은 시간 안에 기록되는 것을 방지할 수 있다.

<a id="57b9fdb53e97ca99"></a>
##### 수정 전 대처

없음

<a id="fac99ba9b80298fe"></a>
#### <kbd>ISSUE-6543</kbd> 두 개 이상의 멤버에서 동시에 startup phase를 global open으로 올리면 서버가 비정상 종료된다.

<a id="25b85b60568c6a3f"></a>
##### 개요

두 개 이상의 멤버에서 동시에 startup phase를 global open 단계로 올리면 서버가 비정상 종료되는 현상을 제거하였다.

<a id="fa5ffa4ca393410e"></a>
##### 현상 및 증상

두 개 이상의 멤버에서 동시에 startup phase를 global open 단계로 올리면 서버에 hang이 걸리거나 비정상 종료된다.

<a id="53938e9a47527d5e"></a>
##### 수정 전 대처

한 개의 멤버에서만 startup phase를 global open 단계로 올려야 한다.

<a id="6bc4115d95b3bfe7"></a>
#### <kbd>ISSUE-6511</kbd> Cluster member들 사이에 연결 단절로 인해 발생하는 에러의 SQLSTATE를 변경하였다.

<a id="3865ba1778f28e9c"></a>
##### 개요

Cluster member들 사이에 연결 단절로 인해 발생하는 에러의 SQLSTATE를 변경하였다.

<a id="f1b928e29d4feef9"></a>
##### 현상 및 증상

Cluster member들 사이에 연결 단절로 인해 발생하는 DML 에러의 SQLSTATE가 다음과 같이 변경되었다.

<a id="3cef41bb3cd65fe3"></a>
| 에러 번호 | 기존 SQLSTATE | 변경된 SQLSTATE | 메시지 |
| --- | --- | --- | --- |
| 16357 | 42000 | 42R01 | must be accessible to at least one member of group '%s' |
| 16358 | 42000 | 42R01 | accessible member does not exist |

Cluster member들 사이에 연결 단절로 인해 발생하는 DDL 에러의 SQLSTATE가 다음과 같이 변경되었다.

<a id="4d4d39ac348c3afb"></a>
| 에러 번호 | 기존 SQLSTATE | 변경된 SQLSTATE | 메시지 |
| --- | --- | --- | --- |
| 16360 | 42000 | 42R02 | cloned table "%s"."%s" must be accessible to at least one member |
| 16361 | 42000 | 42R02 | sharded table "%s"."%s" must be accessible to at least one member of group '%s' |
| 16412 | 42000 | 42R02 | all of shards in a table '%s' must be online. |
| 16482 | 42000 | 42R02 | database is not accessible; '%s' has detached from the cluster |
| 16545 | 42000 | 42R02 | cloned table "%s"."%s" must have at least one online replica |
| 16546 | 42000 | 42R02 | sharded table "%s"."%s" must have at least one online replica of group '%s' |

<a id="5dcd927f74f844f0"></a>
##### 수정 전 대처

없음

<a id="1db03c5524e58b30"></a>
### 22c.1.4 Patch Notes

<a id="9da91ce594893761"></a>
#### <kbd>ISSUE-5544</kbd> Cluster 환경에서 cyclone을 사용하여 이중화 하는 도중에 master 와의 연결이 종료되어 트랜잭션 처리에 실패할 경우, rollback logic이 대기한다.

<a id="bb1fdb02c851dfb9"></a>
##### 개요

1. Cluster 이중화 환경에서만 발생한다. Cyclone을 사용하여 이중화하는 도중에 master가 종료되어 slave 측에서 트랜잭션 처리에 실패했을 때 이전에 처리되던 트랜잭션을 rollback 하면 cyclone이 대기하는 현상이 발생할 수 있다.

2. 이를 해결하기 위하여 slave의 rollback 로직을 제거하고, 데이터를 모두 저장한 후에 트랜잭션을 실행하도록 수정하였다.

<a id="a89b7a4d1f1f2b22"></a>
##### 현상 및 증상

경우에 따라 다음과 같은 내용이 slave trace log에 지속적으로 기록되며, 대기 현상이 계속될 수 있다.

```
[RECEIVER(#2)] [INFO]WAIT_WRITE_RESTART_INFO_FOR_SKIP(AnalyzeState = 1)SCN(705:10166:18)
```

<a id="6abda09945275d59"></a>
##### 수정 전 대처

없음

<a id="6d54ca4c03d3a4a4"></a>
#### <kbd>ISSUE-6381</kbd> 숫자형 타입에서 문자형 타입으로의 변환 규칙이 다른 DBMS 들과 다르다.

<a id="d10a9d15f6f22873"></a>
##### 개요

1. 숫자형 타입을 varchar 타입으로 변환할 때 varchar precision을 고려하여 지수형 또는 실수형으로 변환하는데, 이 때 최대한 사용 공간에 맞게 표현할 수 있도록 반올림하여 변환한다.  
   이로 인해 원본 숫자에 대한 유효 숫자 표현의 정밀도가 감소한다.

2. 숫자형 타입 → CHAR 타입 변환과 숫자형 타입 → VARCHAR 타입 변환의 결과가 서로 다르다.
    1. NUMBER/ NUMERIC
        1. CHAR 로 변환: 실수형으로만 변환한다. (precision 내에 표현할 수 없으면 에러가 발생한다.)
        2. VARCHAR 로 변환: precision 에 맞게 표현할 수 있도록 반올림하여 지수형 또는 실수형으로 변환한다.
    2. NATIVE_REAL/ NATIVE_DOUBLE
        1. CHAR: 유효 숫자를 모두 표현할 수 있는 지수형으로 변환한다. (Truncate가 발생할 경우 에러가 발생한다.)
        2. VARCHAR: precision에 맞게 표현할 수 있도록 반올림하여 지수형으로 변환한다.

이를 해결하려면

- 숫자형 타입의 유효 숫자를 모두 표현할 수 있는 경우, 다음과 같이 변환하도록 수정한다.
    - NUMBER/ NUMERIC: 문자 타입의 precision을 고려하여 지수형 또는 실수형으로 변환한다.
    - NATIVE_REAL/ NATIVE_DOUBLE: 지수형으로 변환한다.
- 숫자형 타입 → CHAR 타입 변환과 숫자형 타입 → VARCHAR 타입 변환의 결과는 동일하다.

<a id="3d6d65a660bf1418"></a>
##### 현상 및 증상

최대한 사용 공간에 맞게 표현할 수 있도록 반올림하여 변환하므로 원본 숫자에 대한 유효숫자 표현의 정밀도가 감소한다.

```
gSQL> create table t1 ( c1 varchar(2) );
Table created.

gSQL> insert into t1 values ( 2.4 );
1 row created.

gSQL> insert into t1 values ( 2.5 ) ;
1 row created.

gSQL> commit;
Commit complete.

gSQL> select * from t1;
C1
--
2 
3
2 rows selected.
```

<a id="b9073565c70b2bec"></a>
##### 수정 전 대처

원본 숫자에 대한 유효 숫자가 모두 표현될 수 있도록 문자 타입의 precision을 적절하게 지정한다.

```
gSQL> create table t1 ( c1 varchar(10) );
Table created.

gSQL> insert into t1 values ( 2.4 );
1 row created.

gSQL> insert into t1 values ( 2.5 ) ;
1 row created.

gSQL> commit;
Commit complete.

gSQL> select * from t1;
C1 
---
2.4
2.5
2 rows selected.
```

<a id="db6a598b6d14d2b1"></a>
#### <kbd>ISSUE-6255</kbd> [CDC] trace log에 기록되는 connection string에 PWD 항목이 노출되어, 이를 '*' 으로 대체하여 기록되도록 하였다.

<a id="9492e9c48347f7ad"></a>
##### 개요

cyclone, cymon, cyfile 에서 trace log에 기록되는 connection string에 PWD 항목이 노출되어, 이를 '*' 으로 대체하여 기록되도록 수정하였다.

<a id="3a040cb82ac59345"></a>
##### 현상 및 증상

cyclone, cymon, cyfile 에서 connection string 에 PWD 항목이 노출되어 trace log에 기록되었다.

```
connection string [PROTOCOL=DA;DSN=goldilocks_jinsil;PORT=11100;UID=test;PWD=test]
```

<a id="6c5b5c4dfd791385"></a>
##### 수정 전 대처

없음

<a id="b8380755289fc5b9"></a>
#### <kbd>ISSUE-6030</kbd> Cluster 환경에서 Member의 Rebalance를 수행할 때 Cyclone에 발생하는 오류를 수정하였다.

<a id="9a12ddca0931871b"></a>
##### 개요

Cluster 환경에서 Cyclone 운영 중인 상황에서 Cluster Member의 Rebalance를 수행하면 Cyclone에서 이를 정상적으로 처리하지 못하는 현상이 있어 이를 수정하였다.

<a id="7345c5a3223daccb"></a>
##### 현상 및 증상

Rebalance가 수행된 Cluster Member에서 동작하는 Cyclone에서 다음과 같은 내용이 기록되고 더 이상 진행이 되지 않았다.

```
[2023-12-08 16:33:58.782398 THREAD(3292,140620625983232)] 
Ready to Rebalance-Tx commit. (Waiting for slave response)
```

<a id="c1ddbf9ee7c51c0d"></a>
##### 수정 전 대처

없음

<a id="053fe3911d161d43"></a>
#### <kbd>ISSUE-6116</kbd> Long Procedure 의 direct execution 성능이 개선되었다.

<a id="ef624b931a8378d5"></a>
##### 개요

매우 많은 PL stmt 와 expression 들로 구성된 procedure 의 direct execution 성능을 개선하였다.

<a id="3a060c8e7a875bc8"></a>
##### 현상 및 증상

다음 예에서 proc1 은 약 2000 개의 BEGIN .. END block, 약 12000 개의 PL stmt, 약 230,000 개의 expression 으로 구성된 procedure 이다.

다음과 같이 proc1() 호출하면 약 150 ms 이상의 시간이 소요되었다.

```
gSQL> call proc1(200,439);  

Procedure Call complete.  

Elapsed time: 157.09300 ms
```

procedure 실행을 위한 plan 의 크기와 optimization 과정을 대폭 개선하여 다음과 같이 성능을 개선하였다.

```
gSQL> call proc1(200,439);  

Procedure Call complete.  

Elapsed time: 12.35000 ms
```

<a id="c8fb860ad06d1d3c"></a>
##### 수정 전 대처

prepare-execution 으로 procedure 를 호출한다.

```
--# prepare
gSQL> \prepare sql call proc1(200,439);

SQL prepared.

--# 1st execution
--# data optimize - execute
gSQL> \exec

Procedure Call complete.

Elapsed time: 158.82600 ms 


--# 2nd execution
--# execute
gSQL> \exec

Procedure Call complete.

Elapsed time: 2.79600 ms
```

<a id="9f5d40b7444eaad6"></a>
#### <kbd>ISSUE-6231</kbd> 유효하지 않은 IP 를 가지고 GLOBAL OPEN 으로 진입하는 경우 에러가 발생한다.

<a id="b323058b39326100"></a>
##### 개요

유효하지 않은 원격 IP 를 가지고 GLOBAL OPEN 으로 올라가려 할 때 실패하는 현상이 있어 이를 수정하였다.

<a id="4dad8a4aedaf44d6"></a>
##### 현상 및 증상

유효하지 않은 원격 IP 를 가지고 GLOBAL OPEN 으로 올라가려 할 때 그 노드를 제외하고 GLOBAL OPEN 으로 올라가야 하는데 다음과 같이 실패한다.

```
gSQL> alter system open global database;

ERR-HY000(11047): MEMBER(G1N2): invalid network address : invalid address()
```

<a id="029140918ff915ce"></a>
##### 수정 전 대처

ALTER CLUSTER LOCATION 구문을 사용해 문제가 발생한 노드의 IP 를 유효한 IP로 변경한다.

```
gSQL> alter cluster location g1n2 host '127.0.0.1' port 12150;

Location altered.
```

<a id="ff13aaca5aa02c05"></a>
#### <kbd>ISSUE-6358</kbd> Weak Memory Ordering 장비에서의 Cache Coherency 문제

<a id="9ccc66fe3ed3afcb"></a>
##### 개요

Weak memory ordering 장비에서 memory 접근 순서가 program order 와 달라져서 서버가 비정상 종료되는 현상이 있어 이를 수정하였다.

<a id="74485ad051e4cb54"></a>
##### 현상 및 증상

메모리에 있는 최신 data가 아닌 CPU cache 에 있는 old data 를 사용하기 때문에 서버가 오동작하거나 비정상적으로 종료될 수 있다.

<a id="8dba1b6b0779d64f"></a>
##### 수정 전 대처

없음

<a id="828f91b21c05f2e7"></a>
### 22c.1.3 Patch Notes

<a id="5ae8e8b28355cbd9"></a>
#### <kbd>ISSUE-5799</kbd> CREATE TABLE/ ALTER TABLE을 수행할 때 default expression이 valid 하지 않음에도 에러가 발생하지 않았다.

<a id="52e0256b95d89395"></a>
##### 개요

CREATE TABLE/ ALTER TABLE을 수행할 때 default clause를 정의하면 default expression이 valid 한지 체크한다.

<a id="277de29c8843bde1"></a>
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

<a id="1d59035e96995e4c"></a>
##### 수정 전 대처

없음

<a id="46e233fdceb355e5"></a>
#### <kbd>ISSUE-5828</kbd> ROWNUM을 포함한 join 질의는 원격 노드로 보낼 수 없는데 보내는 경우가 있다.

<a id="b5badffea928407a"></a>
##### 개요

ROWNUM을 포함한 join 질의는 원격 노드로 보낼 수 없다. Clone 테이블이라 하더라도 각 노드마다 data의 저장 순서가 다를 경우, 잘못된 결과가 도출될 수 있다.

<a id="c4db19f2a235a3d8"></a>
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

<a id="c6638f9229c0a08d"></a>
##### 수정 전 대처

/*+ LOCAL_JOIN(Y) */ hint를 사용한다.

<a id="1e407fd84106258c"></a>
#### <kbd>ISSUE-5810</kbd> [CYCLONE] long varchar column을 포함하는 테이블에 record가 없으면 SYNC에 실패한다.

<a id="3bd62043b5c31a00"></a>
##### 개요

SYNC 할 때 master의 해당 테이블의 record 유무를 확인하는 과정 중에 long varchar column에 대한 null 체크가 잘못되어 발생한다. 실제 record가 없음에도 불구하고 record가 있다고 판단하여 null 데이터를 slave로 INSERT 시도하며, 이로 인하여 "cannot insert NULL into " 관련 에러 메시지를 출력한 뒤 SYNC에 실패한다.

<a id="beb27dea15087867"></a>
##### 현상 및 증상

CYCLONE을 이용한 이중화에서 SYNC 기능을 사용하여 master의 데이터를 slave로 옮기는 과정에서 long varchar column을 포함하는 테이블에 record가 없으면 "cannot insert NULL into" 관련 에러가 발생하며, SYNC에 실패한다.

<a id="1022c857c9cb7c54"></a>
##### 수정 전 대처

없음

<a id="90751539bc386eb5"></a>
#### <kbd>ISSUE-5665</kbd> 세 개 이상의 테이블이 포함된 join이 instant nested loop join method 방식으로 수행되면 잘못된 결과가 도출될 수 있다.

<a id="a4a63b2e345adaac"></a>
##### 개요

세 개 이상의 테이블이 포함된 join이 instant nested loop join method 방식으로 수행되면 잘못된 결과가 도출될 수 있다.

<a id="84e04444d115190a"></a>
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

<a id="15f54537311cecd9"></a>
##### 수정 전 대처

USE_INL(t1) 외의 다른 hint를 사용한다. 예를 들면 USE_NL(t1), USE_HASH(t1), USE_MERGE(t1) 등을 사용한다.

<a id="14b2d0dff16b5b5d"></a>
#### <kbd>ISSUE-5710</kbd> View 내부에 view가 있고, 가장 안쪽 view에 group by가 있는 경우, complex view merging이 연달아 발생하면서 error가 발생할 수 있다.

<a id="0de27e7926eec5d3"></a>
##### 개요

View 내부에 view가 있고, 가장 안쪽 view에 group by가 있는 경우, complex view merging이 연달아 발생하면서 error가 발생할 수 있다. 이 때, error가 발생하는 부분은 SELECT list의 aggregation expression 이다.

위 조건을 만족하더라도 SELECT list에 aggregation이 없으면 error는 발생하지 않는다.

<a id="11aec4f85f0fe2e8"></a>
##### 현상 및 증상

```
\EXPLAIN PLAN
SELECT sum(case_sum )
  FROM (
         SELECT 
                v1.col1, v1.col2, ( case when v1.sum > 0 then 2
                                    else 1
                                    end
                                  )as case_sum
          FROM ( SELECT col1, col2, sum(col3) as sum
                   FROM t1
                  WHERE col3 > 0  
                  GROUP BY col1, col2 
               ) v1
       ) v2
      , t2
 WHERE v2.col1 = t2.col1;

ERR-42000(12119): comparison is not applicable: ROWID and NUMBER :
```

v1이 먼저 merging 되고, v2에 대한 merging이 일어나면 'case when then' 구문의 v1.sum을 제대로 찾지 못하는 문제가 있다.

<a id="3087a352e5a21e57"></a>
##### 수정 전 대처

두 view 중 하나라도 merging이 되지 않으면 error가 발생하지 않는다. 따라서 /*+ NO_MERGE( v1) */ 또는 /*+ NO_MERGE(v2)*/ hint를 사용하면 된다.

<a id="7b5b1fd1f6f22d94"></a>
#### <kbd>ISSUE-5667</kbd> Subquery에서 외부 query를 참조할 때, materialized view와 일반 table 모두를 참조하면 비정상 종료할 수 있다.

<a id="75e94256b51b350d"></a>
##### 개요

다음 조건을 모두 만족하면 비정상 종료한다.

1. &lt;from clause&gt;에 table이 나열될 때, &lt;with clause&gt;에 의해 명시된 materialized view가 먼저 나열되고 일반 table이 나열된다.
2. Subquery가 있고, 그 subquery가 materialized view와 일반 테이블을 모두 참조한다.

<a id="f1a0e792001ea6c3"></a>
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

<a id="2ab60b8aa2e1367f"></a>
##### 수정 전 대처

FROM 절에서 materialized view를 제일 뒤에 나열한다.

<a id="85975150ba1ac565"></a>
#### <kbd>ISSUE-5634</kbd> V$LICENSE를 추가하였다.

<a id="0c647745601504db"></a>
##### 개요

현재 동작 중인 서버의 라이센스 정보를 확인할 수 있는 view를 추가하였다.

<a id="cead14e5d104c3f4"></a>
##### 현상 및 증상

없음

<a id="184ac98b43cf49e6"></a>
##### 수정 전 대처

없음

<a id="8364af0e0dd60314"></a>
#### <kbd>ISSUE-5442</kbd> [CYCLONE] unique 속성을 갖는 column을 이중화 할 경우, 트랜잭션이 실패할 수 있다.

<a id="652690e31410d408"></a>
##### 개요

이중화하는 table에 unique 속성을 갖는 column이 있을 경우, 원본 database에서는 정상적으로 처리되지만 원격 database에서는 unique violation 또는 NO_ROWS 에러가 발생할 수 있다. 이를 해결하기 위하여 unique 속성을 갖는 column을 이중화 할 경우, 해당 column의 동시성을 제어하는 기능을 추가하였다.

<a id="53e9dc6a5c50f584"></a>
##### 현상 및 증상

```
[APPLIER #1(SID:100)-INSERT] ERR-23000(16057) : unique constraint (PUBLIC.TEST1) violated

[APPLIER #2(SID:101)-UPDATE] Conflict.

[APPLIER #3(SID:102)-DELETE] Conflict.
```

이중화 table에 unique 속성을 갖는 column이 있을 경우, 위와 같은 log가 빈번하게 slave의 trace log에 기록된다.

<a id="55909db82819fbed"></a>
##### 수정 전 대처

없음

<a id="db45739f6a1ab51a"></a>
#### <kbd>ISSUE-5568</kbd> [CYCLONE] 이중화 recovery가 두 개의 redo log 파일에 걸쳐 있을 경우, recovery 시작점이 잘못 설정된다.

<a id="9ca342e5f2c8f86b"></a>
##### 개요

이중화 종료 후 restart 할 때 cyclone은 기존에 운영되었던 applier에 반영된 정보를 사용하여 recovery 시작 위치를 찾고 이중화를 다시 시작하게 된다.

Recovery 할 때는 여러 applier간의 정보를 비교하면서 최적의 시작 위치를 찾는다. 만약 redo log file 정보들의 applier 간에 운영 정보가 서로 다를 경우, 이전 redo log file의 대한 정보를 버리고 새로운 redo log file 정보만 사용해서 recovery 시작 위치를 정하는 문제가 있어서 이를 수정하였다.

<a id="64ce95fd47c1bc50"></a>
##### 현상 및 증상

이중화 종료 후 재시작시 이중화되지 못하는 transaction이 있을 수 있다.

<a id="60f78b4cd5e7f81d"></a>
##### 수정 전 대처

없음

<a id="e34250a624780596"></a>
#### <kbd>ISSUE-5511</kbd> [CYCLONE] Distributor에서 internal transaction ID가 잘못 세팅되는 경우가 있다.

<a id="fb3a11bb31f1b512"></a>
##### 개요

원본 database에서 동시에 수행되는 transaction 간에 transaction ID 값은 중복될 수 없음을 보장한다. 그렇지만 수행이 완료된 transaction ID는 후에 재사용될 수 있다.

원본 transaction을 추출하여 이중화하기 위해 slave에 전송된 시점에서는 parallel apply로 인하여 해당 transaction ID의 실행시점이 원본과 다를 수 있다. 이 경우, transaction ID 재사용에 의한 ID 중복을 방지하기 위해 slave에서는 독립적인 transaction ID를 내부적으로 구분할 수 있는 internal ID 값으로 변경한다.

이러한 internal transaction ID는 distributor에서 할당하는데, 특정 로그를 분석하는 과정에서 internal 값이 아닌 원본 값을 사용함으로써 하나의 transaction이 두 개의 transaction ID를 갖는 문제가 발생하였다.

Distributor에서 동시성 제어의 구분자 값으로 사용되는 transaction ID 값 두 개가 하나의 transaction에 할당되어, 특정 상황에서 self dead-lock이 발생할 수 있다.

<a id="99aeb2034a99a7ba"></a>
##### 현상 및 증상

```
CREATE TABLE T1 ( C1 INTEGER PRIMARY KEY, C2 LONG VARCHAR );

INSERT INTO T1 VALUES( 1, 'AAA' );
DELETE FROM T1 WHERE C1=1;
INSERT INTO T1 VALUES( 1,'AAAAAAA .......' );  ❶ 8K가 넘는 데이터 INSERT
COMMIT;
```

위와 같이 하나의 transaction 내에서 동일한 key 값을 처리하는 query와 레코드 사이즈가 8K가 넘는 INSERT가 수행되면 dead-lock이 발생한다.

<a id="987c1e0bd3c63383"></a>
##### 수정 전 대처

없음

<a id="2a85286a119bb7b6"></a>
#### <kbd>ISSUE-5499</kbd> Window function의 인자가 scalar subquery expression 인 경우 값이 평가되지 않는다.

<a id="a09b13826c1f944c"></a>
##### 개요

Cluster 환경에서 상수화 가능한 scalar subquery expression을 window function에 대한 인자로 사용할 경우 쿼리가 실행될 때 표현식이 평가되지 않아 결과가 NULL이 된다.

<a id="9dba9f1579b8178f"></a>
##### 현상 및 증상

```
--# BUGBUG
--# result : 1
SELECT SUM( ( SELECT 1 FROM dual ) ) OVER() AS C_NAME
  FROM dual@G2;

C_NAME
------
  null
```

Cluster 환경에서는 상수화 가능한 모든 expression을 driver node에서 평가하여 결과값을 generated query로 전달한다.

Subquery expression을 window function에 대한 인자로 사용하는 경우 상수화 구성 여부를 판단하지 않아 상수화가 이루어지지 않았다. Generated query를 통해 subquery expression의 결과값이 전달되어야 하는 경우 결과 오류가 발생한다.

Standalone 또는 cluster 환경이지만 local node에서만 수행하는 질의의 경우 상수화하지 않아도 window function 내 expression은 평가되어 문제가 발생하지 않는다.

<a id="388d30e74237ee83"></a>
##### 수정 전 대처

없음

<a id="b7df32249e6026c8"></a>
#### <kbd>ISSUE-5505</kbd> Join의 가장 왼쪽 테이블에 대한 access method가 unique index access 이고, group by의 key column 중 일부만 그 unique index에 속하는 경우, 잘못된 결과가 도출될 수 있다.

<a id="8ca76a6bf791e9a5"></a>
##### 개요

Join의 가장 왼쪽 테이블에 대한 access method가 unique index access 이고, group by의 key column 중 일부만 그 unique index에 속하는 경우, 잘못된 결과가 도출될 수 있다.

<a id="a24d38ea6e2d3bb4"></a>
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

<a id="3b47123aff7aa931"></a>
##### 수정 전 대처

/*+ USE_GROUP_HASH */ hint를 사용한다.

<a id="c982cc7cac3664fe"></a>
#### <kbd>ISSUE-5500</kbd> JDBC 비 표준 함수인 GoldilocksPreparedStatement.setFixedCHAR()를 추가하였다.

<a id="ededa2617519bf12"></a>
##### 개요

JDBC 비 표준 함수인 GoldilocksPreparedStatement.setFixedCHAR()를 추가하였다.

<a id="48dea488968bab65"></a>
##### 현상 및 증상

SELECT 문의 WHERE 절에 CHAR column을 PreparedStatement.setSrting()으로 바인딩 할 경우 결과가 검색되지 않는다.

```
<code>create table x (c char(4));
insert into x (c) values ('a');  -- inserts 'a   '
</code>
```

```
<code>PreparedStatement stmt = 
  conn.prepareStatement("select * from x where c = ?");
stmt.setString(1, "a");    // This won't return any records
stmt.executeQuery();</code>
```

<a id="75c2c9cbc94b1709"></a>
##### 수정 전 대처

CHAR column을 VARCHAR column으로 변경한다.

<a id="0cbed176b451b3d7"></a>
#### <kbd>ISSUE-5482</kbd> 불완전 복구 시 로그가 부족하면 복구에 실패할 수 있다.

<a id="1a30ce8f11c4a477"></a>
##### 개요

불완전 복구를 수행할 때 복구를 완료할 수 있는데도 불구하고 실패하는 경우가 있어서 수정하였다.

<a id="b3cf3e9f487c8365"></a>
##### 현상 및 증상

Redo log가 유실되어 이전에 백업받은 redo log를 이용하여 불완전 복구를 수행하는 경우, 백업 받은 redo log가 archive log보다 이전이면 archive log 이후의 로그를 찾지 못하여 발생한 문제이다.

```
gSQL> ALTER DATABASE RECOVER UNTIL TIME '2023-04-05 19:05:01.559752';

ERR-HY000(14068): logfile does not exist - '/goldilocks/goldilocks_data/archive_log/archive_4.log'
```

<a id="d4edb131d89c6934"></a>
##### 수정 전 대처

Archive log보다 이후의 redo log가 없는 경우 다음과 같이 훼손되지 않은 로그만 이용하여 복구를 수행하는 interactive 불완전 복구를 수행한다.

```
gSQL> ALTER DATABASE BEGIN INCOMPLETE RECOVERY;

ERR-01000(14104): Warning: suggestion '/goldilocks/archive_log/archive_0.log'
ERR-01000(14103): Warning: media recovery needs a logfile including log (Lsn 139992)
Database altered.

gSQL> ALTER DATABASE RECOVER AUTOMATICALLY;

ERR-01000(14104): Warning: suggestion '/goldilocks/archive_log/archive_4.log'
ERR-01000(14103): Warning: media recovery needs a logfile including log (Lsn 144143)
Database altered.

gSQL> ALTER DATABASE END INCOMPLETE RECOVERY;

Database altered.
```

<a id="847c0aacdb5af142"></a>
#### <kbd>ISSUE-5445</kbd> ADD LOGFILE GROUP 수행 시, LOGFILE GROUP의 크기를 충분하게 설정하더라도 LOGFILE GROUP을 추가하지 못하는 경우가 있다.

<a id="eab267fc9910a262"></a>
##### 개요

충분한 크기의 LOGFILE GROUP을 설정해도 logfile이 최소 크기보다 작다는 에러 메세지와 함께 LOGFILE GROUP을 추가하지 못한다.  
ADD LOGFILE GROUP을 수행할 때, startup 과정에서 보정했던 log buffer와 pending log buffer 개수를 기준으로 logfile의 최소 크기를 계산해야 하는데 실제로는 property 값을 기준으로 최소 크기를 계산하기 때문이다.

<a id="ee2231096e0fd17b"></a>
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

<a id="d75e86bb89aa15c8"></a>
##### 수정 전 대처

LOG_BUFFER_SIZE와 PENDING_LOG_BUFFER_COUNT property를 변경하여 logfile group을 생성한다.

<a id="fec0cf6382edae5f"></a>
#### <kbd>ISSUE-5424</kbd> Embedded SQL에서 INTO 절 없이 SELECT 구문을 실행하면 데이터가 있는 경우에도 에러가 발생하여 이를 수정하였다.

<a id="7b79574c3b26f0c5"></a>
##### 개요

Embedded SQL에서 INTO 절이 없는 SELECT 구문을 반복적으로 실행하면 에러가 발생하여 이를 수정하였다.

<a id="ea9a7afd007b2d64"></a>
##### 현상 및 증상

```
EXEC SQL SELECT 1 FROM DUAL;

EXEC SQL SELECT 1 FROM DUAL;
```

위와 같이 동일한 SELECT 구문을 반복 실행하면 다음과 같은 에러가 발생한다.

```
Invalid cursor state : A cursor was open on the StatementHandle.
```

<a id="55a47bd3d9cc6618"></a>
##### 수정 전 대처

SELECT 구문에 INTO 절을 추가하여 실행한다.

<a id="f3899463ef91bb5b"></a>
#### <kbd>ISSUE-5411</kbd> JDBC의 ResultSet 클래스의 getBinaryStream 메소드를 사용하면 NullPointerException 발생하여 이를 수정하였다.

<a id="3d61d34bff22c8f3"></a>
##### 개요

Long varbinary 타입의 null 데이터를 얻을 때, ResultSet 클래스의 getBinaryStream 메소드를 사용하면 NullPointerException이 발생하여 이를 수정하였다.

<a id="e82eb9a51fef3f2a"></a>
##### 현상 및 증상

테이블 TEST_LOB에 LONG VARBINARY 타입 C_BLOB은 NULL 데이터를 갖는다.

```
CREATE TABLE PUBLIC.TEST_LOB
(
   ID NUMBER( 10, 0 ),
   C_BLOB LONG VARBINARY
);

INSERT INTO TEST_LOB VALUES(1,UNHEX(HEX('XXXXXXXX')));
INSERT INTO TEST_LOB VALUES(2,null);
COMMIT;
```

다음은 LONG VARBINARY 타입의 데이터를 얻기 위해 getBinaryStream 메소드를 사용하는 코드이다.

```
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT ID, C_BLOB FROM TEST_LOB");

while (rs.next()) {
    try{
        InputStream is = rs.getBinaryStream("c_blob");
        byte[] bytes = new byte[0];
        bytes = new byte[is.available()];
        is.read(bytes);
    } catch( Exception e){
        System.out.println(e);
    }
}
```

위 코드를 실행하면 java.lang.NullPointerException이 발생한다.

<a id="52494dbf1d0e4637"></a>
##### 수정 전 대처

없음

<a id="bdcd949c5b2c7216"></a>
#### <kbd>ISSUE-5398</kbd> gloader가 text 모드로 데이터를 업로드할 때 데이터가 손실되는 문제가 있어 이를 수정하였다.

<a id="acba3335d461f314"></a>
##### 개요

gloader는 text 모드로 데이터를 업로드할 때 동일한 문자로 시작하는 field 구분자와 line 구분자를 사용한다. 데이터에도 이 구분자의 첫 문자가 포함될 경우, 데이터가 잘려서 유효하지 않은 형태로 업로드 되는 문제가 있어서 이를 수정하였다.

<a id="c7abc2e58637a88c"></a>
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

<a id="5279a4f20d0675e9"></a>
##### 수정 전 대처

동일한 문자로 시작하지 않는 field 구분자와 line 구분자를 사용한다.

<a id="1462ee7e5a222483"></a>
#### <kbd>ISSUE-5407</kbd> Lock이 풀리길 기다리는 cluster peer가 driver node가 죽은 것을 인식하지 못한다.

<a id="49195702499c1156"></a>
##### 개요

원격에서 lock이 풀리길 기다리고 있는 driver member가 비정상 종료되면 원격에 만들어진 세션이 살아있는 상태로 유지되는 문제가 있다.

<a id="629341802ef5733a"></a>
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

<a id="79ee6d2a1e4f0f34"></a>
##### 수정 전 대처

없음

<a id="9cfcdeaf04d039d4"></a>
### 22c.1.2 Patch Notes

<a id="e1448c069cb829a4"></a>
#### <kbd>ISSUE-5174</kbd> gpec에서 함수 인자 선언을 지원한다.

<a id="781f8297f87ebce6"></a>
##### 개요

gpec에서 함수 인자 선언을 지원한다. 자세한 내용은 [함수 인자 선언](../part-05-developer-manual/33-embedded-sql.md#7c811efe04803265)을 참조한다.

<a id="da6b24a4b80e1e25"></a>
##### 현상 및 증상

없음

<a id="7a132257bfcb662d"></a>
##### 수정 전 대처

없음

<a id="4ed409420f4d7154"></a>
#### <kbd>ISSUE-5353</kbd> 윈도우 ODBC 연결 및 해제 시 프로그램 handle 개수가 증가하는 문제가 있어 이를 수정하였다.

<a id="3b97a7ec45e6701d"></a>
##### 개요

윈도우 ODBC를 사용해 연결과 해제를 반복할 경우 프로그램의 전체 handle 개수가 증가되는 문제가 있어 수정하였다.

<a id="ccece6735890f2d3"></a>
##### 현상 및 증상

윈도우 ODBC를 사용해 연결과 해제를 반복할 경우 프로그램의 전체 handle 수가 증가한다.

<a id="665cc3f37e4b8f7e"></a>
##### 수정 전 대처

없음

<a id="e8a656400cc4561d"></a>
#### <kbd>ISSUE-5344</kbd> View projection pruning을 수행할 때 상위 block에서 사용하는 column까지 삭제하는 문제가 있다.

<a id="498ce6e1529a7d84"></a>
##### 개요

다음 조건을 만족하는 경우, 잘못 수행된 view projection pruning으로 인해 서버가 비정상 종료할 수 있다.

- View 내부에 group by 또는 order by가 있다.
- View의 select list에서 삭제하려는 expr이 다른 function expression의 argument 이다.

<a id="7cb26df2608b6a39"></a>
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

<a id="12ffca1d5dde069f"></a>
##### 수정 전 대처

없음

<a id="60d3952f154951b1"></a>
#### <kbd>ISSUE-5336</kbd> gpec의 SELECT INTO 구문에 SUBQUERY를 사용하면 SELECT INTO 구문으로 처리하지 못한다.

<a id="9f0a7e2b813714e4"></a>
##### 개요

gpec이 SELECT INTO 구문 뒤에 SUBQUERY가 있는 SQL을 파싱하면 SELECT INTO 구문으로 처리하지 못하였다.

<a id="509b9cf4adf34aa3"></a>
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

<a id="8c802f0384a48748"></a>
##### 수정 전 대처

SELECT INTO 구문에 호스트 변수 배열을 사용하는 대신 cursor를 fetch 한다.

<a id="3bece7716c4a76d2"></a>
#### <kbd>ISSUE-5277</kbd> 디스크 테이블스페이스 삭제 후 버퍼를 재사용하지 못해 hang이 발생한다.

<a id="837e998004b93e48"></a>
##### 개요

디스크 테이블스페이스 삭제되면 ager thread가 삭제된 테이블스페이스의 페이지를 캐싱한 버퍼 캐시를 free list로 옮긴다. 이 때 dirty 페이지의 경우 discard 되어야 한다고 표시만 한다. 그러나 체크포인트가 발생하지 않으면 discard 페이지를 재사용하지 못하여 free 버퍼를 구하는 세션들에서 hang이 발생하는 문제가 있어서 이를 수정하였다.

<a id="49a12f2b38b6ce70"></a>
##### 현상 및 증상

삭제된 디스크 테이블스페이스의 페이지를 캐싱한 버퍼가 dirty 페이지가 된 경우, 디스크 테이블에 접근하는 세션에서 free 버퍼를 구하지 못해 hang이 발생한다.

<a id="2a9a7373d4940846"></a>
##### 수정 전 대처

체크포인트를 수행하여 삭제된 디스크 테이블스페이스의 dirty 페이지를 정리한다.

<a id="f3f97b164cdcf518"></a>
#### <kbd>ISSUE-4945</kbd> CYCLONE, CYMON을 운영하기 위해 table을 생성하는 과정에서 SQLTables를 사용하여 table 존재 여부를 확인한다.

<a id="ee93b1aa56cc498c"></a>
##### 개요

CYCLONE, CYMON을 운영하기 위해 필요한 table이 존재하는지 여부를 SQLTables로 확인한 후에 table을 생성하도록 수정하였다.

<a id="6dd8f8fec8684022"></a>
##### 현상 및 증상

없음

<a id="e57845b776fbef02"></a>
##### 수정 전 대처

Prepare 할 때 table exist에 관한 validate를 수행한 후 그 결과를 가지고 table 존재 여부를 판단한다.

<a id="3f07bacddfe5989a"></a>
#### <kbd>ISSUE-5218</kbd> Async commit을 사용하면 한 세션에서 트랜잭션이 과도하게 사용될 수 있다.

<a id="aaa27294976ed882"></a>
##### 개요

Cluster 환경에서 async commit을 사용하면 트랜잭션이 종료되지 않은 상태에서도 새로운 트랜잭션을 사용할 수 있기 때문에 한 세션에서 두 개 이상의 트랜잭션을 사용할 수 있다.

<a id="89c725b647835c87"></a>
##### 현상 및 증상

트랜잭션을 과도하게 사용함으로써 트랜잭션 부족 현상이 발생할 수 있다.

<a id="9baaf9931e69b87a"></a>
##### 수정 전 대처

없음

<a id="840b506e627b13aa"></a>
#### <kbd>ISSUE-5029</kbd> Cluster 환경에서 Cyclone 운영 중에 master가 reset all 옵션으로 re-join 했음에도 기존 이중화 정보를 초기화하지 않는다.

<a id="0f5e4abbbc19e4c4"></a>
##### 개요

Cluster 환경에서 Cyclone이 운영 중인 상태에서 reset all 옵션을 사용하여 기존에 운영되던 master를 재시작할 경우, 기존의 이중화 정보를 사용하지 말고 현재 시점부터 이중화를 재개해야 한다.

<a id="7d18f64ee007c62b"></a>
##### 현상 및 증상

Reset all 옵션을 사용하여 master를 재시작했음에도 기존의 이중화 운영정보를 사용하여 recovery를 수행한다.

<a id="3ee4a47f2e5fabc0"></a>
##### 수정 전 대처

없음

<a id="a842e5ea0ca0b529"></a>
### 22c.1.1 Patch Notes

<a id="2710b570a3e95f1e"></a>
#### <kbd>ISSUE-5132</kbd> Cluster 환경에서 global secondary index가 없는 single domain 테이블에 대한 DML 수행을 지원한다.

<a id="b623429f154b07a8"></a>
##### 개요

Cluster 환경에서 하나의 domain을 갖는 테이블에 대해 DML을 수행할 때 global secondary index를 구성하지 않으면 실패할 수 있다. DML 질의에서 global secondary index를 요구하는 이유는 server 간의 데이터 일관성을 보장하기 위해서이다. 따라서 하나의 server에만 데이터가 적재되어 server 간의 데이터 일관성을 보장할 필요가 없는 경우 global secondary index 없이도 DML을 지원하도록 하였다.

Cluster 환경에서 하나의 테이블을 다수의 server에서 관리하려면 global secondary index를 구성하기를 권장한다.

<a id="6025b1e8e21acee1"></a>
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

<a id="ad99668e570f2a87"></a>
##### 수정 전 대처

없음

<a id="1584a25e82d37181"></a>
#### <kbd>ISSUE-5193</kbd> Cluster 환경에서 index backward scan을 포함한 질의 수행시 결과에 오류가 발생한다.

<a id="69532d1d05a4a8f7"></a>
##### 개요

Cluster 환경에서 사용자 질의를 수행할 때 remote 서버에 접근해야 하고, ORDER BY 구문 또는 hint에 의해 index backward scan을 포함한 경우, 질의 결과가 index forward scan 순으로 나올 수 있다.

<a id="0e58f3e04678a348"></a>
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

<a id="94aea65368f59305"></a>
##### 수정 전 대처

없음

<a id="9efb839ea6ce1f28"></a>
#### <kbd>ISSUE-5109</kbd> Shard 재배치, split brain 후에 Cyclone이 오동작하는 문제를 수정하였다.

<a id="4415762d9904d181"></a>
##### 개요

Shard를 재배치하거나 split brain 상황 이후에 복구할 때 Cyclone이 "internal error occurred (Not Need Rebalance)" 에러를 내면서 종료된다.

<a id="e41f3d571127808f"></a>
##### 현상 및 증상

Cyclone이 판단하기에 rebalance가 필요없는 상황인데도 rebalance가 수행되는 경우가 있는데 이런 일은 shard 재배치 또는 split brain 상황에서 발생할 수 있다.

<a id="d549e4f8f42d49f9"></a>
##### 수정 전 대처

Cyclone을 --reset으로 재기동한다.

<a id="7d9d8b8554c4c366"></a>
#### <kbd>ISSUE-5162</kbd> ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정했어도 오랜 시간 동안 대기하는 문제를 수정하였다.

<a id="16e6da37f2c3d34c"></a>
##### 개요

네트워크 단절을 인지하기 위해 ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정했는데도 주어진 TIMEOUT 보다 더 오래 대기하는 문제를 수정하였다.

<a id="9e88a1f303209ad7"></a>
##### 현상 및 증상

ODBC의 SQL_ATTR_CONNECTION_TIMEOUT을 설정하였지만 특정 상황에서 네트워크 단절을 인지하지 못해 ODBC에서 서버 응답을 계속 기다리는 문제가 있다.

<a id="4302fb927b590e19"></a>
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

<a id="aacc4978c44acdf9"></a>
#### <kbd>ISSUE-5160</kbd> ODBC global connection 환경에서 LONGVARCHAR, LONGVARBINARY 파라미터가 있을 경우 클라이언트 메모리가 증가하는 문제를 수정하였다.

<a id="824077f58f142ab6"></a>
##### 개요

ODBC global connection 환경에서 LONGVARCHAR, LONGVARBINARY 파라미터가 있는 statement를 반복적으로 수행할 경우 클라이언트 메모리가 증가하는 문제를 수정하였다.

<a id="ddd473eb1d9e5763"></a>
##### 현상 및 증상

ODBC global connection 환경에서 같은 statement로 LONGVARCHAR, LONGVARBINARY 파라미터가 있는 SQL을 반복적으로 수행할 경우 클라이언트 메모리가 증가하였다.

<a id="708c5011c7cc846c"></a>
##### 수정 전 대처

없음

<a id="4fe9fca7ffd21eee"></a>
#### <kbd>ISSUE-5156</kbd> 일부 에러의 SQLSTATE를 변경하였다.

<a id="a5d8494b3e1c000e"></a>
##### 개요

일부 에러의 SQLSTATE를 변경하였다.

<a id="95777108af31fae6"></a>
##### 현상 및 증상

변경된 에러의 SQLSTATE는 다음과 같다.

<a id="2046129c6f78e5c5"></a>
| 에러 번호 | 기존 SQLSTATE | 변경된 SQLSTATE | 메세지 |
| --- | --- | --- | --- |
| 13034 | RD000 | 08S01 | Service is not available |
| 16351 | 08000 | HY000 | failed to connect to the cluster member '%s' |
| 16523 | HY000 | 08S01 | the database system is shutting down |
| 25001 | HY000 | 08001 | Server is not running |

<a id="9dbbc7ee0dca9322"></a>
##### 수정 전 대처

없음

<a id="c16ee5a6cb9945ee"></a>
#### <kbd>ISSUE-5147</kbd> CYMON에서 환경설정에 PROTOCOL=TCP로 설정하더라도 DA로 접속하던 문제를 수정하였다.

<a id="cbd7ef9941dac82d"></a>
##### 개요

CYMON이 환경설정에 PROTOCOL=TCP로 설정하더라도 DA로 접속하던 문제를 수정하여 TCP로 접속하도록 수정하였다.

<a id="d8c11aa10c90cd99"></a>
##### 현상 및 증상

CYMON 환경설정 파일에 PROTOCOL=TCP로 설정할 경우, TCP를 사용하여 접속하여야 하는데 DA로 접속하고 있었다.

<a id="99be1a9e8d8ce4f4"></a>
##### 수정 전 대처

없음

<a id="c6eeb37b9be14ef7"></a>
#### <kbd>ISSUE-5004</kbd> Cluster 환경에서 CYCLONE으로 이중화하는 도중에 slave의 pre-process 단계에서 deadlock이 발생한다.

<a id="9b20b0637569e5fa"></a>
##### 개요

Cluster 환경에서 CYCLONE으로 이중화하는 도중에 간헐적으로 deadlock이 발생할 수 있다.

<a id="fb0b0f10a7b76aae"></a>
##### 현상 및 증상

이중화가 더 이상 진행되지 않으며 멈춰 있는 것처럼 보이는 현상이 발생한다. 이는 cluster 환경에서 이중화 처리를 위해 pre-process 하는 도중에 deadlock이 발생한 경우이며, CYMON으로 모니터링 하더라도 더 이상 이중화가 진행되지 않는다.

<a id="c00210fa66dfd06e"></a>
##### 수정 전 대처

CYCLONE master와 slave를 reset 한다.

<a id="c669b6518c58b658"></a>
#### <kbd>ISSUE-4985</kbd> CYCLONE의 모니터링 정보에 slave의 진행 정보를 추가하였다.

<a id="48a0a3e1fd5aff58"></a>
##### 개요

CYCLONE의 모니터링 정보에 slave에서 처리 중인 정보 (Apply_FileSeq, Apply_BlockSeq, Apply_Commit_Lsn)를 추가하였다.

<a id="3cabdfa3fa79f299"></a>
##### 현상 및 증상

없음

<a id="0af068e4e8bef352"></a>
##### 수정 전 대처

없음

<a id="14bbb370b0d5db25"></a>
#### <kbd>ISSUE-4882</kbd> CYCLONE SYNC 처리 중 오류 발생 시, 오류를 상세화하여 리포팅하도록 수정하였다.

<a id="abf75e8523d5665a"></a>
##### 개요

CYCLONE의 SYNC를 처리하는 도중에 오류가 발생하면 *ERROR OCCURRED* 메세지와 함께 에러 내용을 상세하게 trace log에 기록하도록 하였다.

<a id="f48e26f93041486a"></a>
##### 현상 및 증상

없음

<a id="6a5be911b0e865b3"></a>
##### 수정 전 대처

없음

---

[← 3. Cluster 튜토리얼](3-cluster-튜토리얼.md) · [전체 목차](../README.md) · [5. GOLDILOCKS 데이터베이스 관리 기본 →](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
