<a id="2b92c76bcae133a2"></a>

# 4. What's New

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/2b92c76bcae133a2)  
> Tag: `21c.1_35_tag`

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<a id="7afd3e87db0c2191"></a>
## Feature Matrix

This chapter briefly describes the features added to each major version.

<a id="8e7760b833c03740"></a>
### Architecture

<a id="9961708f4fd35193"></a>
#### System Architecture

The following is a feature matrix for system architecture.

**Feature matrix for system architecture**

<a id="17fed7e1a589bbdb"></a>
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

<a id="185650b0fdeeeb22"></a>
#### Storage Internal

The following is a feature matrix for storage internal.

**Feature matrix for storage internal**

<a id="5366c654470de61d"></a>
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

<a id="b9006c279ea1dce2"></a>
#### Transaction Control

The following is a feature matrix for transaction control.

**Feature matrix for transaction control**

<a id="761c5d8be5b772da"></a>
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

<a id="2a54fb5647cb3ba3"></a>
#### Backup & Recovery

The following is a feature matrix for backup & recovery.

**Feature matrix for backup & recovery**

<a id="98428e668c96724e"></a>
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

<a id="6aedadaa20d0d914"></a>
#### Database Information

<a id="72fea8a20627a27d"></a>
##### DICTIONARY_SCHEMA Schema

The following is a feature matrix for DICTIONARY_SCHEMA schema.

<a id="a65b0d088371e1a5"></a>
<table class="table column_count_6"><caption>Feature matrix for DICTIONARY_SCHEMA schema </caption><thead><tr><th class="to_center"><div>Family</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="56"><div>Views of ALL_family</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="48"><div>Views of DBA_family</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="53"><div>Views of USER_family</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="15"><div>Other views</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="e0365a0f833674ef"></a>
##### INFORMATION_SCHEMA Schema

The following is a feature matrix for INFORMATION_SCHEMA schema.

**Feature matrix for INFORMATION_SCHEMA schema**

<a id="78122917d61f2f43"></a>
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

<a id="f5490533b007f63f"></a>
##### PERFORMANCE_VIEW_SCHEMA Schema

The following is a feature matrix for PERFORMANCE_VIEW_SCHEMA schema.

**Feature matrix for PERFORMANCE_VIEW_SCHEMA schema**

<a id="59b1e0daa5bba26c"></a>
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

<a id="e9fc9eede52d1807"></a>
#### Server Property

The following is a feature matrix for server property.

**Feature matrix for server property**

<a id="b3c2d7d17a0c055e"></a>
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

<a id="46405fb7ed8888a8"></a>
### SQL

<a id="9d7f2d0820f398de"></a>
#### SQL Element

<a id="ff2344860582e0df"></a>
##### Data Type

The following is a feature matrix for data type.

<a id="22917f5494b43892"></a>
<table class="table column_count_6"><caption>Feature matrix for data type</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>Character string type</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Binary string type</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Decimal number type</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Binary number type</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN type</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Date/ time type</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL type</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ROWID type</div></td><td><div>ROWID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="cf297798aed47ecf"></a>
##### Function

The following is a feature matrix for function.

**Feature matrix for function**

<a id="37b0a6b46872bc4e"></a>
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

<a id="ee2cf9eaa1ff704e"></a>
#### Object

<a id="ec0491be626d03f7"></a>
##### SQL Object

The following is a feature matrix for DDL which creates/ drops/ alters an SQL object.

<a id="5790e76a2133238e"></a>
<table class="table column_count_6"><caption>Feature matrix for SQL object DDL</caption><thead><tr><th class="to_center"><div>Object</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Database 
object</div></td><td><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE REGISTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RESTORE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMENT ON object IS ..</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
object</div></td><td><div>CREATE PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
object</div></td><td><div>CREATE AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NOAUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
object</div></td><td><div>CREATE USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER USER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GRANT privileges TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REVOKE privileges FROM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 
object</div></td><td><div>CREATE SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SCHEMA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
object</div></td><td><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLESPACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="24"><div>Table 
object</div></td><td><div>CREATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE TABLE AS SELECT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRUNCATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. STORAGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLASHBACK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PURGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
object</div></td><td><div>CREATE VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER VIEW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Index 
object</div></td><td><div>CREATE INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. AGING</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. STORAGE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. RENAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. REBUILD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
object</div></td><td><div>CREATE SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
object</div></td><td><div>CREATE SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PUBLIC SYNONYM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
object</div></td><td><div>CREATE PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
object</div></td><td><div>CREATE FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package object</div></td><td><div>CREATE PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PACKAGE BODY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="34a1ad75171f4e31"></a>
##### Cluster Object

The following is a feature matrix for DDL which creates/ drops/ alters a cluster object.

<a id="546d9c9a4a12f5bc"></a>
<table class="table column_count_6"><caption>Feature matrix for cluster object DDL </caption><thead><tr><th class="to_center to_middle"><div>Object</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Cluster system 
object</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
object</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
object</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
object</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster table and shard object</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Global secondary index
object</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="615d166696348960"></a>
#### SQL Language

<a id="3254b05066816df2"></a>
##### DML

The following is a feature matrix for DML which manipulates data.

**Feature matrix for DML**

<a id="b3b7f2153825c84b"></a>
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

<a id="d2aa1955f7c0d779"></a>
##### Query

The following is a feature matrix for SELECT statement which enquires data.

**Feature matrix for SELECT**

<a id="025375563a7681fa"></a>
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

<a id="54391d77872d689f"></a>
##### Control Language

The following is a feature matrix for control statement.

<a id="3ed30d2cd8c4391d"></a>
<table class="table column_count_6"><caption>Feature matrix for control statement</caption><thead><tr><th class="to_center to_middle"><div>Control statement</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4e957ab833ea42f9"></a>
#### PSM Language

The following is a feature matrix for Persistent Stored Module (PSM) language element.

**Feature matrix for Persistent Stored Module (PSM) language element**

<a id="dfb08736ea9b8d11"></a>
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

The following is a feature matrix for the Built-In Package.

<a id="25fa8a1835fa60b2"></a>
<table class="table column_count_6"><caption>Feature matrix for Built-in Package</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="577ef0ade6ee4652"></a>
### API

<a id="ccc5827b2ae641f2"></a>
#### ODBC

The following is a feature matrix for the ODBC standard API.

**Feature matrix for the ODBC standard API**

<a id="ca50931431700f68"></a>
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

The following is a feature matrix for API other than the ODBC standard API.

**Feature matrix for API other than the ODBC standard**

<a id="4d45a930f95ce727"></a>
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

<a id="994794731c436a26"></a>
#### JDBC

The following is a class feature matrix for JDBC.

**Class feature matrix for JDBC**

<a id="dd4bd5030fbb005b"></a>
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

<a id="55e5559aa9dfafb9"></a>
#### Embedded SQL

<a id="6bb1acd3be857109"></a>
##### Precompiler Option

The following is a feature matrix for precompiler option.

**Feature matrix for precompiler option**

<a id="aab775bda956fa43"></a>
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

<a id="39d3121c03e78a19"></a>
##### Embedded SQL-only Syntax

The following is a feature matrix of embedded SQL-only syntax.

**Feature matrix for embedded SQL-only syntax**

<a id="dca744e6a0c7cc0b"></a>
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

<a id="46a5a941394a78aa"></a>
##### Host Variable Data Type

The following is a feature matrix for embedded SQL data type which can be used for HOST variables.

**Feature matrix for host variable data type**

<a id="538ec2fe50333ce0"></a>
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

<a id="73d1f2936f0f45a4"></a>
##### Dynamic SQL

The following is a feature matrix for dynamic SQL.

**Feature matrix for dynamic SQL**

<a id="873d69954addc917"></a>
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

<a id="00267fa01e4160ac"></a>
#### PyDBC

<a id="02e7853d105726ed"></a>
##### Module

The following is a method feature matrix for pygoldilocks provided by PyDBC.

**Feature matrix for pygoldilock method**

<a id="f9584c5dd6b92c6d"></a>
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

The following is an attribute feature matrix for pygoldilocks module.

**Feature matrix for pygoldilock attribute**

<a id="61b222aadac387cf"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| apilevel | X | O | O | O |
| threadsafety | X | O | O | O |
| paramstyle | X | O | O | O |
| version | X | O | O | O |
| lowercase | X | O | O | O |

<a id="6a30239f72067472"></a>
##### Connection

The following is a method feature matrix for connection object.

**Feature matrix for connection method**

<a id="6f29ce5adfa95fd9"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| cursor | X | O | O | O |
| commit | X | O | O | O |
| rollback | X | O | O | O |
| close | X | O | O | O |
| getinfo | X | O | O | O |
| execute | X | O | O | O |
| set_attr | X | O | O | O |

The following is an attribute feature matrix for connection object.

**Feature matrix for connection attribute**

<a id="3dd4db07da2a6a5f"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| autocommit | X | O | O | O |
| searchescape | X | O | O | O |
| timeout | X | O | O | O |

<a id="35af5edff4c5bdc8"></a>
##### Cursor

The following is a method feature matrix for cursor object.

**Feature matrix for cursor method**

<a id="6254efe9edfa63ad"></a>
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

The following is an attribute feature matrix for cursor object.

**Feature matrix for cursor attribute**

<a id="618f1edac440386e"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| Description | X | O | O | O |
| rowcount | X | O | O | O |
| arraysize | X | O | O | O |
| connection | X | O | O | O |
| fast_executemany | X | O | O | O |

<a id="bf0426f29558d2d8"></a>
##### Row

The following is an attribute feature matrix for row object.

**Feature matrix for row attribute**

<a id="7a00c5d26e1662f5"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| cursor_description | X | O | O | O |

<a id="d530c2f2bd6f9f21"></a>
### Utility

<a id="622bda0a57581fb5"></a>
#### gcreatedb

<a id="860a8156ce3d14b8"></a>
##### Command Usage

The following is a feature matrix for command usage of gcreatedb.

**Feature matrix for command usage of gcreatedb**

<a id="dca03d7e67863e7f"></a>
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

<a id="3ed2379127e2fe81"></a>
#### glsnr

<a id="93e36e0caa32eb82"></a>
##### Command Usage

The following is a feature matrix for command usage of glsnr.

**Feature matrix for command usage of glsnr**

<a id="bbece88403a84080"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --help | O | O | O | O |
| --home | X | O | O | O |
| --silent | O | O | O | O |
| --start | O | O | O | O |
| --status | O | O | O | O |
| --stop | O | O | O | O |

<a id="4e2d62d60f918018"></a>
##### Configuration File

The following is a feature matrix for configuration of glsnr.

**Feature matrix for configuration of glsnr**

<a id="af393842c2d35d5d"></a>
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

<a id="fd533d6f6ebe5cfc"></a>
#### gsql/ gsqlnet

<a id="f6b459ca0c8def43"></a>
##### Command Usage

The following is a feature matrix for command usage of gsql.

**Feature matrix for command usage of gsql**

<a id="d4fde296d91e50ad"></a>
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

<a id="c83a584ebcff134c"></a>
##### Interactive gsql Command

The following is a feature matrix for interactive gsql command which is used in gsql prompt state.

**Feature matrix for interactive gsql command**

<a id="39f767a8beb4c79d"></a>
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
| `\ddl_package` | X | O | O | O |
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

<a id="0ab6c504dee09d99"></a>
#### gloader/ gloadernet

<a id="5183e2567a780ff2"></a>
##### Command Usage

The following is a feature matrix for command usage of gloader.

**Feature matrix for command usage of gloader**

<a id="cb1cf0e353659a8c"></a>
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

<a id="160ec42c20096975"></a>
##### Control File Syntax

The following is a feature matrix for control file syntax of gloader.

**Feature matrix for control file syntax of gloader**

<a id="8282cd457a8d6309"></a>
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

<a id="333ed1aa2ba07cae"></a>
#### gdump

<a id="f9098651003ac0e9"></a>
##### Command Usage

The following is a feature matrix for command usage of gdump.

<a id="a55ec9b8c6bcfab5"></a>
<table class="table column_count_6"><caption>Feature matrix for command usage of gdump</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="d39618ec6a0968f7"></a>
#### tablediff

<a id="846f058adf05e2a7"></a>
##### Configuration File

The following is a feature matrix for configuration file of tablediff.

<a id="c24bb901787f3b13"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of tablediff</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td class="to_middle"><div>SOURCE_PASSWORD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_URL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td class="to_middle"><div>TARGET_PASSWORD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_URL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td class="to_middle"><div>TARGET_INSERT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_UPDATE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_DELETE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_INSERT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td class="to_middle"><div>DIFF_BIN_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DIFF_OUT_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_CALL_STACK</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_ROW_UNIT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>EXCLUDE_COLUMNS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_DIFF</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_SUCCESS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_QUEUE_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_THREAD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_UNIT_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PARTITION_RANGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SYNC_OUT_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>WHERE_CLAUSE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="42d912c63724cc9c"></a>
#### gsyncher

<a id="0f85b12908d5670b"></a>
##### Command Usage

The following is a feature matrix for command usage of gsyncher.

**Feature matrix for command usage of gsyncher**

<a id="136d84eb3c4fa9a6"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --log | O | O | O | O |
| --silent | O | O | O | O |
| --home | X | O | O | O |
| --copy-right | O | O | O | O |
| --backup-path | O | O | O | O |
| --help | O | O | O | O |

<a id="14cc372f45360d3e"></a>
#### gmon

<a id="d250a5b1bc6a9cc4"></a>
##### Command Usage

The following is a feature matrix for command usage of gmon.

**Feature matrix for command usage of gmon**

<a id="6feb2760ab585817"></a>
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

<a id="e8afa75ba5199849"></a>
#### gtrclogger

<a id="ab80132705922f06"></a>
##### Command Usage

The following is a feature matrix for command usage of gtrclogger.

**Feature matrix for command usage of gtrclogger**

<a id="4e5ee441d795e6d7"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --dir | X | O | O | O |
| --help | X | O | O | O |
| --port | X | O | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |

<a id="2d5d20727ee251e8"></a>
#### glocator

<a id="715c14e8d6d9b6e5"></a>
##### Command Usage

The following is a feature matrix for command usage of glocator.

**Feature matrix for command usage of glocator**

<a id="4023c22267ee8053"></a>
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

<a id="179644cdab78c088"></a>
##### Configuration File

The following is a feature matrix for configuration file of glocator.

**Feature matrix for configuration file of glocator**

<a id="56cd599627e4a038"></a>
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

<a id="622ed8ea7319bcb0"></a>
#### gagent

<a id="cd90f16f210923a6"></a>
##### Command Usage

The following is a feature matrix for command usage of gagent.

**Feature matrix for command usage of gagent**

<a id="8e30c97de2921bed"></a>
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

<a id="0984cb57d9fcde98"></a>
##### Configuration File

The following is a feature matrix for configuration file of gagent.

**Feature matrix for configuration file of gagent**

<a id="1f6815d43805953c"></a>
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

<a id="944e19b8328483d3"></a>
#### gloctl

<a id="a64b78b5197c0873"></a>
##### Command Usage

The following is a feature matrix for command usage of gloctl.

**Feature matrix for command usage of gloctl**

<a id="a65bf1b9e6f282a6"></a>
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

<a id="875dfb3c712a6a99"></a>
##### Configuration File

The following is a feature matrix for configuration file of gloctl.

**Feature matrix for configuration file of gloctl**

<a id="705182177279e5a5"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| PORT | X | O | O | O |
| LOCATOR_HOST | X | O | O | O |
| LOCATOR_PORT | X | O | O | O |

<a id="6a7e5b839df7d5e5"></a>
### Replication

<a id="fc97a8b3ee053fd0"></a>
#### cyclone

<a id="92cfd1273d8e81cb"></a>
##### Command Usage

The following is a feature matrix for command usage of cyclone.

**Feature matrix for command usage of cyclone**

<a id="5457728a6515365e"></a>
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

<a id="2f9f90c76f6aea19"></a>
##### Configuration File

The following is a feature matrix for configuration file of cyclone.

<a id="d38451eb7065b354"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of cyclone</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="69dc890acd33025c"></a>
#### logmirror

<a id="923487513e9e9737"></a>
##### Command Usage

The following is a feature matrix for command usage of logmirror.

**Feature matrix for command usage of logmirror**

<a id="4bcf7c031cf01b04"></a>
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

<a id="cb489b4d2332add4"></a>
##### Configuration File

The following is a feature matrix for configuration file of logmirror.

<a id="63bb397452621b38"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of logmirror</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="7fbbdb8fa2509fba"></a>
#### cymon

<a id="33fd73ef211fb520"></a>
##### Command Usage

The following is a feature matrix for command usage of cymon.

**Feature matrix for command usage of cymon**

<a id="f436d305ebc8b1e3"></a>
| Feature | 2.x | 3.x | 20c.1 | 21c.1 |
| --- | --- | --- | --- | --- |
| --conf | O | O | O | O |
| --help | O | O | O | O |
| --cycle | O | O | O | O |
| --key | X | O | O | O |
| --start | O | O | O | O |
| --stop | O | O | O | O |
| --status | O | O | O | O |

<a id="8ae42d1f997c2b59"></a>
#### cyfile

<a id="7cb17ed629a8753c"></a>
##### Command Usage

The following is a feature matrix for command usage of cyfile.

**Feature matrix for command usage of cyfile**

<a id="4a7c64a368c75028"></a>
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

<a id="9fa4c0468b0f571e"></a>
##### Configuration File

The following is a feature matrix for configuration file of cyfile.

**Feature matrix for configuration file of cyfile**

<a id="bb196ea843c4bebb"></a>
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

<a id="25156e25da5c2afd"></a>
## What's New in GOLDILOCKS 21c.1

This chapter briefly describes the features added to GOLDILOCKS 21c.1.

<a id="a73b9045cc58f6e1"></a>
### Architecture

<a id="aff061167609c4ef"></a>
#### System Architecture

It has not been changed.

<a id="82f74d505f73e779"></a>
#### Storage Internal

It has not been changed.

<a id="394168445b5a909c"></a>
#### Transaction Control

It has not been changed.

<a id="f8519cbd831323a7"></a>
#### Backup & Recovery

It has not been changed.

<a id="fc59574fcebe61df"></a>
#### Database Information

<a id="c6980b14d1302b16"></a>
##### DICTIONARY_SCHEMA

It has not been changed.

<a id="95674d0588b3a9e9"></a>
##### INFORMATION_SCHEMA

It has not been changed.

<a id="d771d8da2db97783"></a>
##### PERFORMANCE_VIEW_SCHEMA

[V$PLAN_HISTORY](../part-02-administration-manual/9-database-information.md#dc17ecd200827f6a) view has been added, and it retrieves plans managed by the plan history feature.

[V$PLAN_HISTORY_LATEST](../part-02-administration-manual/9-database-information.md#fb1211db81c17df6) view has been added, and it retrieves the latest plan managed by the plan history feature.

<a id="576394b3dcf8bad7"></a>
#### Server Property

[MAXIMUM_PACKAGE_INSTANCE_COUNT](../part-02-administration-manual/10-server-property.md#3bd4460bd15278dc) property has been added, and it controls the number of package instances available in the session.

[MAXIMUM_FILE_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#35e269bc8b957dbf) property has been added, and it controls the maximum number of file caches available in the session.

[MAXIMUM_FLUSH_BUFFER_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#71b3d691b0589a47) property has been added, and it controls the maximum number of pages to be written in the disk per a writing operation when IO thread records the updated pages in the buffer into the disk.

[BUFFER_PREFETCH_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#4b7d7ca789c523bb) property has been added, and it controls the maximum number of pages to be prefetched per a disk IO when the session accesses to the page in the disk tablespace which does not exist in the buffer.

[PLAN_HISTORY](../part-02-administration-manual/10-server-property.md#0f6636d35ba1083a) property has been added, and it sets whether to use the plan history.

[PLAN_HISTORY_SIZE](../part-02-administration-manual/10-server-property.md#15548e9ceb65ea36) property has been added, and it controls the number of plans to be stored in the plan history.

[BROADCAST_INDEX_REBUILD_PROTOCOL](../part-02-administration-manual/10-server-property.md#078656a5e697d814) property has been added, and it sets whether to simultaneously rebuild the indexes on all members when rebuilding the index in cluster environment.

[TIMER_INTERVAL](../part-02-administration-manual/10-server-property.md#e3fb26d21297b93a) property has been added, and it sets the time interval which is required when the timer thread sets the system time.

The default value of [DEFAULT_INDEX_PCTFREE](../part-02-administration-manual/10-server-property.md#6365821a90b522f1) has been changed to 10.

The default value of [DEFAULT_MAXTRANS](../part-02-administration-manual/10-server-property.md#0cdf26f13b3ef647) has been changed to 32.

[INST_HASH_TABLE_BUCKET_MAX_COUNT](../part-02-administration-manual/10-server-property.md#e8948e1ccae8b84e) property has been added to set the maximum expected bucket counts of the hash instant table.

[INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#2735d24d76cc77e1) property has been added to control the logging speed during index creation and rebuild operations.

[ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#b967aa5fdd50fec5) property has been added to control disk I/O performance during redo log archiving.

<a id="be5bf0d19348fda4"></a>
### SQL

<a id="a8ba2f53dca5ad4d"></a>
#### SQL Element

<a id="3c50a7ad0d845161"></a>
##### Data Type

It has not been changed.

<a id="0e2476968326caad"></a>
##### Function

[FROM_TZ](../part-03-sql-manual/17-built-in-function-references.md#1415b60dacb7dc8b) function has been added.

The following [&lt;hierarchy expression&gt;](../part-03-sql-manual/20-sql-references-h-z.md#b3da5fac1511a4b0)s which are used together with CONNECT BY clause have been added.

- LEVEL
- CONNECT_BY_ISCYCLE
- CONNECT_BY_ISLEAF
- PRIOR expr
- CONNECT_BY_ROOT expr
- SYS_CONNECT_BY_PATH( expr, 'string' )

<a id="57c9314afa58693b"></a>
#### Object

<a id="f9b96937d3e709f4"></a>
##### SQL Object

It has not been changed.

<a id="c3b9e536f9601a39"></a>
##### Cluster Object

It has not been changed.

<a id="d5810deef6287f4d"></a>
#### SQL Language

<a id="04bfcdc4b57a4cad"></a>
##### DML

Upsert statements have been added.

- [INSERT INTO name ... UPDATE](../part-03-sql-manual/20-sql-references-h-z.md#4e4dcee4feb6ae13)
- [INSERT INTO name ... UPDATE RETURNING](../part-03-sql-manual/20-sql-references-h-z.md#6c7ecee515db5343)
- [INSERT INTO name ... UPDATE RETURNING ... INTO](../part-03-sql-manual/20-sql-references-h-z.md#c5846d898480b884)

<a id="cb277f077356f08e"></a>
##### Query

<a id="3b852ff24f38871b"></a>
###### **WITH Clause**

Common Table Expression (CTE) feature using WITH clause has been added.

- [Common Table Expression (CTE)](../part-03-sql-manual/12-sql-languages.md#e4c4d80df855548e)
- [with clause](../part-03-sql-manual/20-sql-references-h-z.md#ed5949685032d3b2)
- [&lt; cte query hints &gt;](../part-03-sql-manual/15-sql-tuning.md#7fd70f43a908cd5f)

<a id="c224abe20a79cd52"></a>
###### **Hierarchy Query**

Hierarchy query feature has been added.

- [Hierarchical Query](../part-03-sql-manual/12-sql-languages.md#c7e3b399195ed372)
- [hierarchical query clause](../part-03-sql-manual/20-sql-references-h-z.md#bf1d9a36c2b54771)

<a id="9a873520b492a0b8"></a>
##### Control Language

<a id="d4d407852e13dc5a"></a>
###### **SET SCHEMA**

[SET SCHEMA schema_name](../part-03-sql-manual/20-sql-references-h-z.md#5dea9f1e93eb2d19) statement which can alter the default schema of the current session has been added.

<a id="6949e97df6d52675"></a>
#### PSM Language

It has not been changed.

<a id="a685e3a0ebf7ee3c"></a>
### API

<a id="6a08cac863ec3acd"></a>
#### ODBC

PREFER_IPV6 has been added to [Keywords in the data source specification section](../part-05-developer-manual/31-odbc.md#753e6de9f2a389a2).

DOT_NET_FOR_ODBC has been added to [Keywords in the data source specification section](../part-05-developer-manual/31-odbc.md#753e6de9f2a389a2).

<a id="764a8f05efacbeb1"></a>
#### JDBC

It supports some [Blob](../part-05-developer-manual/32-jdbc.md#0843d9dcc6136065) and [Clob](../part-05-developer-manual/32-jdbc.md#0e11a9b92118d745).

prefer_ipv6 and locality_on_demand have been added to [Connection property](../part-05-developer-manual/32-jdbc.md#00de0770e9a7490d).

[Statement Pooling](../part-05-developer-manual/32-jdbc.md#143a16e29d609458) feature has been added.

It supports [getNetworkTimeout](../part-05-developer-manual/32-jdbc.md#59039e203360ee8f), [setNetworkTimeout](../part-05-developer-manual/32-jdbc.md#5535278f0d76b616) methods of [Connection](../part-05-developer-manual/32-jdbc.md#abcf14ed8a505e94) class.

<a id="29feb14fef14e05e"></a>
#### Embedded SQL

<a id="4a07918638b5d314"></a>
##### Precompiler Option

[--autocommit](../part-05-developer-manual/33-embedded-sql.md#a73f7475c5600a29) has been added.

The [--parse](../part-05-developer-manual/33-embedded-sql.md#b4b40f81ea50e3e7) option has been added to gpec.

<a id="4c581bd7da06a175"></a>
##### Embedded SQL-only Statement

gpec supports [Declaring Function Argument](../part-05-developer-manual/33-embedded-sql.md#f46118cf38208e11).

<a id="3fa94ee52ea548ba"></a>
##### Host Variable Data Type

It has not been changed.

<a id="0183570be3f7b9db"></a>
##### Dynamic SQL

It has not been changed.

<a id="850168d99204053b"></a>
#### PDO

It has not been changed.

<a id="b8bf3e946d919274"></a>
#### PyDBC

It has not been changed.

<a id="fb4c53111a8a28a6"></a>
#### Ruby

It has not been changed.

<a id="1ca28fb4e342f4cd"></a>
#### Hibernate

It has not been changed.

<a id="5a299cf061b1e11b"></a>
### Utility

<a id="416c564350504b02"></a>
#### gcreatedb

It has not been changed.

<a id="99194ce46c4f0e17"></a>
#### glsnr

It supports IPv6.

<a id="c604a3c3491e099a"></a>
#### gsql/gsqlnet

It has not been changed.

<a id="c6275603a1b6b44f"></a>
#### gloader/gloadernet

The binary file structure has been changed.

<a id="397246a2389147a6"></a>
#### gdump

It has not been changed.

<a id="d02454d3aef66e45"></a>
#### tablediff

It has not been changed.

<a id="05808ecd472d5a88"></a>
#### gsyncher

It has not been changed.

<a id="c7e090e3c78ce4f7"></a>
#### gmon

It has not been changed.

<a id="320a225878467085"></a>
#### gtrclogger

It has not been changed.

<a id="c29d0de772b272ef"></a>
#### glocator

It has not been changed.

<a id="1986145d47da94d0"></a>
#### gagent

It has not been changed.

<a id="5a1e8cefc1df258f"></a>
#### gloctl

It has not been changed.

<a id="543b490efd51ad20"></a>
### Replication

<a id="809fd777eb5a73da"></a>
#### cyclone

IBM DB2 database has been added as an interworking target database while operating CYCLONE.

<a id="b2bf223677a57869"></a>
#### logmirror

It has not been changed.

<a id="2574cb6f338c4854"></a>
#### cymon

It has not been changed.

<a id="acc106c3c0159b3d"></a>
#### cyfile

A tool which uses CDC method to store/ record the transaction of the original database in CSV format file has been added.

<a id="eee1384241282712"></a>
## Patch Notes

<a id="e5a9c5686f974438"></a>
### 21c.1.35 Patch Notes

<a id="cc0e35ceb80bdfe3"></a>
#### <kbd>ISSUE-8012</kbd> Excessive disk I/O during redo log archiving caused service performance degradation, and this issue has been fixed.

<a id="4d28217f933be951"></a>
##### Description

The service performance degradation caused by excessive disk I/O during redo log archiving has been resolved by introducing the [ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#b967aa5fdd50fec5) property.

<a id="51a9e055d8943ce4"></a>
##### Symptom

Service performance degradation occurs due to excessive disk I/O during redo log archiving.

<a id="7e8428e558fafd7a"></a>
##### Workaround

The patch is required.

<a id="2d461c31ff49237d"></a>
#### <kbd>ISSUE-5452</kbd> Data exceeding 4000 bytes in LONG VARBINARY columns was not properly replicated or synchronized during integration between Cyclone and Oracle, and this issue has been fixed.

<a id="ba12d53188695155"></a>
##### Description

During integration between Cyclone and Oracle, data exceeding 4000 bytes in LONG VARBINARY columns was not properly replicated.

<a id="2f76d799b522b0aa"></a>
##### Symptom

During integration between GOLDILOCKS and Oracle, data in LONG VARBINARY columns exceeding 4000 bytes was processed without errors; however, only partial data was applied during replication and synchronization.

<a id="c891bc6d18879b6b"></a>
##### Workaround

The patch is required.

<a id="73f60020d6844e75"></a>
#### <kbd>ISSUE-7939</kbd> Full table scan may occur after adding a low-selectivity composite index

<a id="a66e15560a24953f"></a>
##### Description

An issue was identified where adding a low-selectivity composite index could cause a query that previously performed an index scan to perform a full table scan instead. This issue has been fixed.  
This behavior occurred only when all of the following conditions were satisfied:  
• The index previously used by the query is a composite index.  
• The query specifies '=' conditions for only a subset of the index key columns, rather than for all columns in the index.

<a id="039bf727e51c2393"></a>
##### Symptom

When a composite index contains both high-selectivity columns and low-selectivity columns, the optimizer may choose a full table scan instead of the existing index scan.

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

In the example above, a composite index ( c_good, c_bad_1, c_bad_2, c_bad_3, c_bad_4) exists. The following query specifies filter conditions on only a subset of the index key columns ( c_good, c_bad_1, c_bad_2, c_bad_3 ), and therefore performs an index scan.

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

However, if another composite index consisting of low-selectivity columns is added as follows, the query that previously performed an index scan may instead perform a full scan.

```
--##########################################
--# Add a Low-Selectivity Composite Index 
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

<a id="da84714f3bf718f2"></a>
##### Workaround

Use an INDEX hint to force the query to perform an index scan.

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

<a id="9895f94fceb222a9"></a>
### 21c.1.34 Patch Notes

<a id="c67f2dac006120e2"></a>
#### <kbd>ISSUE-7805</kbd> The issue where memory allocated during the handling of the ODBC LONG VARCHAR and LONG VARBINARY types was not properly released has been fixed.

<a id="631e2a190421a9e7"></a>
##### Description

A memory leak occurred for LONG VARCHAR and LONG VARBINARY columns during metadata reconstruction when the table schema was altered during a FETCH and another FETCH was performed on the same table.

<a id="ef4ef7bf5b90c43d"></a>
##### Symptom

In a client-server (CS) environment, when querying data through ODBC, altering the table schema via an ALTER statement during a FETCH operation triggers metadata reconstruction. If the table contains LONG VARCHAR or LONG VARBINARY columns, memory dynamically allocated for those column types was not released properly, resulting in a memory leak.

<a id="d89f40d2383bf38c"></a>
##### Workaround

Before this issue was fixed, the safest approach was to avoid altering the table schema during a FETCH operation. If altering the schema was unavoidable, the affected SQLHSTMT handle had to be reallocated by calling SQLFreeHandle followed by SQLAllocHandle.

<a id="e67f7c4ad87849bd"></a>
### 21c.1.33 Patch Notes

<a id="58f53ee99de105e1"></a>
#### <kbd>ISSUE-7782</kbd> A parse option has been added to gpec.

<a id="dd8c563f27be29b9"></a>
##### Description

The parse option has been added to gpec to control source parsing. The option can be set to none or partial, and if not specified, the default value is partial.

<a id="40bb9587da68f393"></a>
##### Symptom

N/A

<a id="c99326dfccd041e4"></a>
##### Workaround

The patch is required.

<a id="7dedb2d59e819280"></a>
#### <kbd>ISSUE-7782</kbd> The code handling behavior of the gpec preprocessor has been modified.

<a id="cc59c2898aaa8b61"></a>
##### Description

The gpec preprocessor has been updated to change how it handles code in branches that evaluate to false (#if, #elif, #else, #ifdef, #ifndef).  
Before this update, code in false branches was removed from the output. It now remains intact and is included in the output.

<a id="ea723126682eadac"></a>
##### Symptom

In some cases, the gpec preprocessor was unable to recognize macros defined in certain header files. In such cases, gpec evaluated the relevant preprocessor conditions as false and deleted the associated code blocks. As a result, code that was valid in the actual compilation environment could be missing in the gpec output.  
In other words, discrepancies could arise between the gpec output and the actual build due to differences in preprocessor evaluation.

For example, when a gc file includes a header using the EXEC SQL INCLUDE statement, if that header references a macro defined in another header, gpec cannot interpret the macro and evaluates the condition as false.  
As a result, code that should not be removed may be deleted.

The following is an example of a header file not referenced by gpec:

```
#ifndef SYS_FLAG_H
#define SYS_FLAG_H
#define SYS_FEATURE_FLAG 1
#endif /* SYS_FLAG_H */
```

The following is an example of a header file successfully referenced by gpec:

```
#ifndef SYS_CONFIG_H
#define SYS_CONFIG_H

/* References a macro defined in another header */
#define ENABLE_FEATURE SYS_FEATURE_FLAG

#endif /* SYS_CONFIG_H */
```

The following is an example gc file:

```
EXEC SQL INCLUDE sys_config.h;
int main(void)
{
#if ENABLE_FEATURE
/* In the actual compilation environment, SYS_FEATURE_FLAG == 1,
so this code should be included. */
feature_func();
#endif
return 0;
}
```

Although sys_config.h refers to a macro defined in another header, gpec cannot interpret that macro. As a result, the ENABLE_FEATURE condition is evaluated as false, and code that is valid in the actual compilation environment may be removed from the gpec output.

<a id="cb1fc9711d7b84f6"></a>
##### Workaround

Preprocessor conditions and macros used in gc files should be defined within header files included using EXEC SQL INCLUDE.

<a id="b6231d4b7119422a"></a>
#### <kbd>ISSUE-5401</kbd> During Cyclone recovery, errors other than conflicts are now displayed.

<a id="d1b9bdaa2f2b5dd8"></a>
##### Description

Previously, errors occurring in the recovery process were not logged in the trace log, so non-conflict errors could not be verified. This issue has now been resolved.

<a id="23930a18d5af669b"></a>
##### Symptom

Previously, errors occurring in the recovery process were not logged in the trace log, so errors could not be verified.

```
[2025-01-24 10:55:17.793633 THREAD(2503,139847152563968)] 
[APPLIER #1(SID:65)] Error Occurred.

[2025-01-24 10:55:17.804159 THREAD(2503,139847100114688)] 
[HEARTBEAT(#0)] Finalize Done.
```

With this update, errors are now displayed during the recovery phase, and can be checked as follows.

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

<a id="f1ba70b18f7ad015"></a>
##### Workaround

The patch is required.

<a id="494540d853930645"></a>
#### <kbd>ISSUE-7743</kbd> An issue that occurred while processing nested #if / #endif directives in the gpec preprocessor has been fixed.

<a id="79247b6abf290cb4"></a>
##### Description

When processing #if preprocessor directives, the gpec preprocessor removes (replaces with empty strings) all statements up to the corresponding #endif directive if the condition is evaluated as false.  
However, when #if / #endif directives were used in a nested structure, some statements within the inner preprocessor blocks were not removed correctly. This issue has been identified and fixed.  
This fix applies not only to #if directives but also to all conditional preprocessor directives, including #elif, #else, #ifdef, and #ifndef.

<a id="2d544322203849ca"></a>
##### Symptom

The following is a portion of a gc file that contains nested #if / #endif directives.

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

The following is a portion of the generated c file produced by converting the above code using the gpec preprocessor:

```
printf("error 3");
```

Due to the nested #if 0 conditions, all three printf statements should have been removed. However, the converted c file incorrectly retained the printf("error 3"); statement.

<a id="4f081f344c42a102"></a>
##### Workaround

Avoid using nested #if / #endif directives. Alternatively, statements should not be placed after an inner #endif directive, as shown below.

```
#if 0
    #if 0
        printf("error 1");
    #else
        printf("error 2");
    #endif                 // Statements below this directive are not processed correctly.
    printf("error 3");
#endif
```

<a id="68cb073383688bba"></a>
#### <kbd>ISSUE-7353</kbd> Fixed missing data issue when changing array size during ODBC fetch

<a id="b9eb5db5d773a62c"></a>
##### Description

An issue was identified in the ODBC client-server environment where changing the array size dynamically during data fetch caused data retrieval to fail. This issue has been resolved.

<a id="851c6e3b69b36142"></a>
##### Symptom

When retrieving data using ODBC in a client-server (CS) environment, an issue occurred where data could not be fetched correctly if the array size was changed during the fetch operation. This problem commonly appeared when using the SQLExtendedFetch, SQLFetch, and SQLFetchScroll functions, and was particularly noticeable when the fetch started with a small array size (e.g., 1 row) and was later changed to a larger array size (e.g., 100 rows).

As a specific symptom, after changing the SQL_ROWSET_SIZE or SQL_ATTR_ROW_ARRAY_SIZE attribute, SQL_NO_DATA was returned prematurely, resulting in only a subset of the data being retrieved even though more data was actually available.

<a id="409d4006d0fce7de"></a>
##### Workaround

Prior to applying the patch for this issue, the most reliable approach was to keep the array size fixed rather than changing it. If changing the array size was unavoidable, the recommended method was to close the current cursor using the SQLCloseCursor function and then re-execute the query so that the fetch would begin with the new array size. When stability was more important than performance, the array size could be set to 1 to fetch data one row at a time.

<a id="03209f147575bea3"></a>
### 21c.1.32 Patch Notes

<a id="e7edebf8367ebf31"></a>
#### <kbd>ISSUE-6939</kbd> When using the offset limit clause during an IN KEY RANGE scan, incorrect results may occur.

<a id="c115f9e84dd1e408"></a>
##### Description

If the IN KEY RANGE scan is used when executing a query that includes an OFFSET clause, incorrect results may occur. This issue has been fixed.

<a id="0b35ce63781d998d"></a>
##### Symptom

When performing an IN KEY RANGE scan on a query that includes OFFSET LIMIT clause, the OFFSET and LIMIT values may not be accumulated correctly, leading to more rows being skipped or returned than intended.

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

<a id="05d961abf70d1635"></a>
##### Workaround

The patch is required.

<a id="cbc089b48e86cd5c"></a>
### 21c.1.31 Patch Notes

<a id="7959f815792a2df6"></a>
#### <kbd>ISSUE-6803</kbd> Access to invalid segment hint memory may occur.

<a id="0586fd3e0f7b740b"></a>
##### Description

If the number of replacements in the segment hint cache exceeds the signed integer range (2147483647), it may result in reading or writing outside the segment hint memory space. This can lead to segment faults and abnormal behavior, and the error has been fixed.

<a id="3eeef881ea0e5049"></a>
##### Symptom

It is possible to read or write outside the allocated memory range, which can lead to segment faults and abnormal behavior.

<a id="e9f3c02fa3f5d4fd"></a>
##### Workaround

The patch is required.

<a id="44120c9023591f37"></a>
#### <kbd>ISSUE-6797</kbd> The session fatal in Gmaster is handled as a system fatal.

<a id="6a301bc2e7f65924"></a>
##### Description

When a session fatal occurs in the Gmaster thread, a hang is triggered, preventing normal cleanup, so it is handled as a system fatal.

<a id="61fca45a29d5ac49"></a>
##### Symptom

When a session fatal occurs in the Gmaster thread, it causes a hang.

<a id="23c1a303240fbdf2"></a>
##### Workaround

The patch is required.

<a id="cf2bef7e023c1eb7"></a>
#### <kbd>ISSUE-6687</kbd> When the redo log members are replicated, the cyclone is unable to read the next redo log after a redo log switch.

<a id="bc3a9edb4ab60184"></a>
##### Description

When the redo log members are replicated, the cyclone fails to handle it correctly after a log switch, and this error has been fixed.

<a id="2139d248a7fddadd"></a>
##### Symptom

The cyclone continuously waits for the next file without replication being implemented.

<a id="36ac81e0577956a7"></a>
##### Workaround

Remove the redo log member and restart the cyclone.

<a id="41416c30cf4c4645"></a>
#### <kbd>ISSUE-6605</kbd> If the RETURNING clause is used in an UPSERT statement, it will result in an error."

<a id="11b00203a771b482"></a>
##### Description

If the RETURNING clause is used in an UPSERT statement, an error will occur during the INSERT operation because there are no duplicate key values.

<a id="81a6acdde7f9ccd0"></a>
##### Symptom

When using the RETURNING clause in an UPSERT statement, an error will occur if the order of the columns specified in the RETURNING clause differs from the order of the columns in the base table.

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

<a id="66d765dcf6439be7"></a>
##### Workaround

The patch is required.

<a id="54ba272e5754af58"></a>
#### <kbd>ISSUE-6575</kbd> An error occurs when only the fields of a record type variable are specified in the INTO clause of a FETCH statement.

<a id="cc800c47ab60c7d0"></a>
##### Description

An error occurs if fields of a record type variable are specified, even when the number of targets of the cursor in the FETCH statement matches the number of targets in the INTO clause.

<a id="f45588357baa3264"></a>
##### Symptom

An error occurs even when the number of targets in the cursor's SELECT statement matches the number of targets in the FETCH INTO clause.

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

It has now been modified to operate correctly.

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

<a id="7112b30c8c6fa2b8"></a>
##### Workaround

Use a scalar type variable.

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

<a id="411ccb0c49e0aa3f"></a>
### 21c.1.30 Patch Notes

<a id="a17facd6a507b813"></a>
#### <kbd>ISSUE-6358</kbd> A cache coherency issue occurred on the weak memory ordering device, and this error has been fixed.

<a id="d52cda30acadd4f2"></a>
##### Description

A memory access order discrepancy, where the order deviated from the program order, occurred on the weak memory ordering device, causing the server to terminate abnormally. This error has been fixed.

<a id="106f34da09728fc5"></a>
##### Symptom

Using old data from the CPU cache instead of the latest data in memory can cause the server to malfunction or terminate abnormally.

<a id="c462a75f2ec4b53a"></a>
##### Workaround

The patch is required.

<a id="f8fb56eae1dca3cd"></a>
#### <kbd>ISSUE-6557</kbd> When using an outer join, if functions such as DECODE, stored functions, or CONCAT that include columns from the right table are in the WHERE clause, it can lead to incorrect results.

<a id="e4c51c7260d8c771"></a>
##### Description

When functions such as DECODE, stored functions, or CONCAT that include columns from the right table exist in the WHERE clause, the following outer join operation elimination should not be applied; however, it was actually applied, resulting in an error.

- The left outer join was transformed into an inner join.
- The full outer join was transformed into a left outer join.

<a id="c017b42bae9db94c"></a>
##### Symptom

In cases where outer join operation elimination occurs as follows, the inclusion of DECODE, stored functions, etc., in the WHERE clause can lead to incorrect results.

Before the modification, the following incorrect results were output.

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

After the modification, the correct plan and results are as follows.

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

<a id="d9fc45da3dfbd24a"></a>
##### Workaround

Use the NO_QUERY_TRANSFORMATION hint as follows.

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

<a id="9b4b4c3dff8565a1"></a>
#### <kbd>ISSUE-6537</kbd> When performing a cast operation between string types, such as CAST('ABCDE' AS CHAR(3)), an error occurs if the source value exceeds the dest precision.

<a id="c1ba488c8dbe0ac9"></a>
##### Description

When performing a cast operation between string types, such as CAST('ABCDE' AS CHAR(3)), an error occurs if the source value exceeds the dest precision.

In this case, the cast operation is performed by truncating the source value to match the precision of the target string type.

<a id="d8d3d17d8925a931"></a>
##### Symptom

Before the modification, the following error occurred.

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

After the modification, the cast operation is performed by truncating the source value to match the precision of the target string type.

```
gSQL> SELECT CAST( c1 AS CHAR(3) ) FROM t1;
CAST( C1 AS CHAR(3) )
---------------------
ABC                  
1 row selected.
```

<a id="8928d7474f5059ca"></a>
##### Workaround

Specify the precision of the target string type to accommodate the source value.

<a id="9d962bd9f72c826f"></a>
#### <kbd>ISSUE-6536</kbd> The DML jitter issue caused by bulk logging has been eliminated.

<a id="3c5192092b6c5bd1"></a>
##### Description

The issue of DML jitter caused by bulk logging during online index rebuilds has been eliminated.

<a id="0548c48c5acfba11"></a>
##### Symptom

Bulk logging can slow down the log flusher, which in turn can increase the duration for which online index rebuilds hold locks, potentially causing delays in DML operations.

[INDEX_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#2735d24d76cc77e1) property has been newly added. It prevents bulk logging from occurring in a short period during index rebuilds.

<a id="4c67821a697db64f"></a>
##### Workaround

The patch is required.

<a id="d3cce74e1ad58ed0"></a>
#### <kbd>ISSUE-6543</kbd> If multiple members simultaneously raise the startup phase to global open, the server may terminate abnormally.

<a id="92901bc291cc4118"></a>
##### Description

The issue of the server's abnormal termination when multiple members simultaneously raise the startup phase to global open has been resolved.

<a id="f3850393f4d9b9a6"></a>
##### Symptom

When multiple members simultaneously raise the startup phase to global open, the server may hang or terminate abnormally.

<a id="a1b242cf9ffcb363"></a>
##### Workaround

Only one member must raise the startup phase to global open at a time.

<a id="d5701ad146eac230"></a>
#### <kbd>ISSUE-5544</kbd> If a transaction fails due to a disconnection with the master during replication in a cluster environment using Cyclone, the rollback logic may hang.

<a id="cdb73051d85f186d"></a>
##### Description

1. This issue occurs only in a cluster replication environment. If a previously processed transaction needs to be rolled back because the slave failed to process the transaction due to the master being terminated during replication with Cyclone, it can cause Cyclone to hang.

2. To address this, the rollback logic on the slave has been removed and replaced with a method to store all data before executing the transaction. This modification resolves the hanging issue.

<a id="3f44b12d39249df0"></a>
##### Symptom

In some cases, the slave trace log may continuously record the messages as follows, and the system may hang as a result.

```
[RECEIVER(#2)] [INFO]WAIT_WRITE_RESTART_INFO_FOR_SKIP(AnalyzeState = 1)SCN(705:10166:18)
```

<a id="19a1df42eb3f671e"></a>
##### Workaround

The patch is required.

<a id="a7df7d3424d06f60"></a>
#### <kbd>ISSUE-4334</kbd> It fails to join the node due to the SCN difference when ascending to Global Open.

<a id="dc7a3e5e285e4d23"></a>
##### Description

It fails to join a cluster because the scn of a specific member is smaller than a maximum scn of the cluster, and this error has been fixed.

<a id="d67fae005f513a94"></a>
##### Symptom

It can not ascend to Global Open with the following error.

```
gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

ERR-42000(16410): Startup driver node must have the latest data - a suitable startup driver node is 'G1N1' member
```

<a id="4e8a93bb4c2f39bd"></a>
##### Workaround

The patch is required.

<a id="b72885e5b4247510"></a>
#### <kbd>ISSUE-6255</kbd> [CDC] PWD was exposed in the connection string recorded in the trace log, so it is replaced with '*' when it is recorded.

<a id="475d2cb14503d36c"></a>
##### Description

PWD was exposed in the connection string recorded in the trace log of cyclone, cymon and cyfile, and this error has been fixed by replacing it with '*' when it is recorded.

<a id="e0acf79c682412e1"></a>
##### Symptom

PWD was exposed in the connection string of cyclone, cymon and cyfile when it was recorded in the trace log.

```
connection string [PROTOCOL=DA;DSN=goldilocks_jinsil;PORT=11100;UID=test;PWD=test]
```

<a id="37f9350a9d077dac"></a>
##### Workaround

The patch is required.

<a id="b25e2ba5310a0ddd"></a>
#### <kbd>ISSUE-6030</kbd> An error occurred in cyclone when rebalancing members in the Cluster environments, and this error has been fixed.

<a id="47bc2a8ab6ff1ff2"></a>
##### Description

When rebalancing cluster members while cyclone was in operation in a cluster environment, cyclone could not process it, and this error has been fixed.

<a id="7c5efd38dc799c8f"></a>
##### Symptom

The followings were recorded in cyclone operated in the cluster member where rebalancing was executed, and no further operation was executed.

```
[2023-12-08 16:33:58.782398 THREAD(3292,140620625983232)] 
Ready to Rebalance-Tx commit. (Waiting for slave response)
```

<a id="e780ac87806737ad"></a>
##### Workaround

The patch is required.

<a id="54083204b03789d7"></a>
#### <kbd>ISSUE-6231</kbd> An error occurs when entering GLOBAL OPEN with an invalid IP.

<a id="d50f485c4334a4ae"></a>
##### Description

It failed when trying to go up to GLOBAL OPEN with an invalid remote IP, and this error has been fixed.

<a id="c87667de55fce12b"></a>
##### Symptom

When trying to go up to GLOBAL OPEN with an invalid remote IP, it should have gone up to GLOBAL OPEN excluding the failed node, but it fails as follows.

```
gSQL> alter system open global database;

ERR-HY000(11047): MEMBER(G1N2): invalid network address : invalid address()
```

<a id="e7c64a313394db3e"></a>
##### Workaround

Alter the IP of the failed node to the valid IP by using ALTER CLUSTER LOCATION statement.

```
gSQL> alter cluster location g1n2 host '127.0.0.1' port 12150;

altered.
```

<a id="8b4e85173253c668"></a>
### 21c.1.29 Patch Notes

<a id="0b2c0c12a8b846c8"></a>
#### <kbd>ISSUE-5933</kbd> When the server performs the cluster failover, then the glocator stops.

<a id="1da642677d3509ac"></a>
##### Description

The server property CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY is set to 1 or 2, and the glocator is waiting to receive packets during the cluster failover.

<a id="ebf5123e5c7100e0"></a>
##### Symptom

The glocator is waiting without receiving packets from the gagent while the glocator communicates with the gagent during the cluster failover.

<a id="759fbfdd1b5326cb"></a>
##### Workaround

The patch is required.

<a id="2fee09ddfa262fe5"></a>
#### <kbd>ISSUE-5862</kbd> It supports getNetworkTimeout, setNetworkTimeout methods of JDBC connection class.

<a id="c384dc6a34a0dce6"></a>
##### Description

It supports getNetworkTimeout, setNetworkTimeout methods of connection class.

<a id="0a2ed7f78009c8c9"></a>
##### Symptom

N/A

<a id="9f37be2732794a28"></a>
##### Workaround

The patch is required.

<a id="3f4ef5b417f3bc61"></a>
#### <kbd>ISSUE-5862</kbd> If sharing JDBC connection object in multi threads and terminating the thread by the thread stop or the interrupt, then the program hangs.

<a id="a99dcf16032b5163"></a>
##### Description

If sharing the connection object in multiple threads and terminating each thread by Thread.stop() or Thread.interrupt() in the program which uses each separate statement, then the program hangs.

<a id="7468853fee66d663"></a>
##### Symptom

If terminating the thread by using Thread.stop() or Thread.interrupt(), then it may cause an error in the communication process. Therefore, the connection should have been closed when the thread was abnormally terminated during the communication process. The program hangs because the protocol is violated during the communication process and another thread uses the connection object while the connection object is open.

<a id="842c3dcf83796b60"></a>
##### Workaround

The patch is required.

<a id="cee4c5c806a83184"></a>
#### <kbd>ISSUE-5799</kbd> An error did not occur even though the default expression was not valid when performing CREATE TABLE/ ALTER TABLE.

<a id="56ee00aff0c6cf18"></a>
##### Description

If defining the default clause when performing CREATE TABLE/ ALTER TABLE, it checks whether the default expression is valid.

<a id="5e61fd124c412a84"></a>
##### Symptom

An error did not occur even though the default expression was not valid.

```
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

Table created.
```

It has been fixed now, so the error occurs as follows.

```
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

ERR-22012(12122): divisor is equal to zero
```

<a id="4516c4acdb581f31"></a>
##### Workaround

The patch is required.

<a id="dce0821125a834f0"></a>
#### <kbd>ISSUE-5828</kbd> The join query including ROWNUM should not be sent to the remote node, but sometimes it is sent.

<a id="6534674d8a6da129"></a>
##### Description

The join query including ROWNUM should not be sent to the remote node. If each node stores data in a different order then the result may be wrong even though it is a clone table.

<a id="81cbc717b7e0d3ec"></a>
##### Symptom

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

The join query including ROWNUM should not be sent to the remote node, but ROWNUM filter is sent to the remote query node in the query above.

<a id="c9ff74838ae804a7"></a>
##### Workaround

Use */*+ LOCAL_JOIN(Y) */* hint.

<a id="45a959363f17285b"></a>
### 21c.1.28 Patch Notes

<a id="3d4ec5bcc4644d55"></a>
#### <kbd>ISSUE-5810</kbd> [CYCLONE] If a record does not exists in the table containing a long varchar column, then it fails to SYNC.

<a id="f478d92a5a15652a"></a>
##### Description

The error occurs because the null check for a long varchar column is incorrectly performed while checking the existence of a record in the table of the master during SYNC. It determines that there is a record even though a record does not exist. Then, it tries to INSERT the null data to the slave, and it outputs the error message "cannot insert NULL into" and it fails to SYNC.

<a id="030d27195e702a11"></a>
##### Symptom

If a record does not exist in the table containing a long varchar column while transferring the data of the master to the slave by using SYNC feature during the replication using CYCLONE, then "cannot insert NULL into" error occurs, and it fails to SYNC.

<a id="f0c51e3e986fe199"></a>
##### Workaround

The patch is required.

<a id="46a269a23014318e"></a>
### 21c.1.27 Patch Notes

<a id="95ad9e50cf662a51"></a>
#### <kbd>ISSUE-5740</kbd> The property preventing DDL execution has been added.

<a id="0ebf88dafef031a4"></a>
##### Description

The property preventing DDL execution has been added.

- [DISABLE_DDL](../part-02-administration-manual/10-server-property.md#fec2f6eb293eabc1)
- [DISABLE_SERIAL_DDL](../part-02-administration-manual/10-server-property.md#72b564a5057a2ea2)

<a id="7b34749a3cda1e82"></a>
##### Symptom

N/A

<a id="d4308750e0dc2e51"></a>
##### Workaround

The patch is required.

<a id="3296253829b3491c"></a>
#### <kbd>ISSUE-5665</kbd> If the join including three or more tables is performed by using the instant nested loop join method, then the result may be wrong.

<a id="a0f7520778c09237"></a>
##### Description

If the join including three or more tables is performed by using the instant nested loop join method, then the result may be wrong.

<a id="3846e4f34237fcb1"></a>
##### Symptom

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

The result from the query above should be '27', but actually '0' is output.

The WHERE clause condition 'T4.COL1 = T2.COL1 + T1.COL1 AND T4.COL1 = T3.COL1 + T1.COL1' can not be used as an index range condition, but actually it is used.

However, if the query is modified, then the correct result is output as follows.

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

<a id="829159c07dfdfd6e"></a>
##### Workaround

Use a hint other than USE_INL(t1). For example, use USE_NL(t1), USE_HASH(t1) or USE_MERGE(t1).

<a id="89c381f93486b7ef"></a>
#### <kbd>ISSUE-5447</kbd> Rolled back transaction is sometimes replicated during CYCLONE replication, and this error has been fixed.

<a id="b148e005278eb542"></a>
##### Description

It happens when replicating the table which has a primary key without a unique key. If the transaction performed in the database operated as CYCLONE master includes the statement which was rolled back due to the PK constraint violation, then the transaction is unintentionally replicated. In this case, the transaction replication is performed in CYCLONE slave as well, and the PK constraint violation error is recorded on CYCLONE log.

<a id="ca82d933e247862b"></a>
##### Symptom

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

<a id="25602206bbff20d2"></a>
##### Workaround

The patch is required.

<a id="7d5c667095e89dbd"></a>
#### <kbd>ISSUE-5695</kbd> Hang occurs when expanding a disk tablespace.

<a id="4950500ad9cbb215"></a>
##### Description

Hang occurs when expanding a tablespace whose NEXT size is 128 MB or bigger.

<a id="1da18cb36cbd1f90"></a>
##### Symptom

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
...(Ellipsis)...
INSERT INTO T1 SELECT * FROM T1 LIMIT 8192;  -- hang
```

<a id="85aa66f800b11dbb"></a>
##### Workaround

Set the NEXT size of the tablespace to 128 MB or smaller.

<a id="bc1b0af690d453f4"></a>
#### <kbd>ISSUE-5667</kbd> When a subquery refers to the outer query, if the subquery refers to both a materialized view and an ordinary table, then the server is abnormally terminated.

<a id="b1166b9d51100a20"></a>
##### Description

If all of the following conditions are satisfied, then the server is abnormally terminated.

1. When tables are listed in &lt;from clause&gt;, the materialized view specified by &lt;with clause&gt; is listed ahead, followed by the ordinary table.
2. A subquery exists and the subquery refers to both a materialized view and an ordinary table.

<a id="e7e15172e9154cff"></a>
##### Symptom

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

In the query above, w and s are listed in an order of w,s in FROM clause, and the subquery refers to both s.c1 and w.c1. In this case, the server is abnormally terminated.

<a id="c1d049ec8a9c3ccb"></a>
##### Workaround

List the materialized view last in FROM clause.

<a id="e4e04a2cd94761c9"></a>
### 21c.1.26 Patch Notes

<a id="c2b946fdb7cb6e45"></a>
#### <kbd>ISSUE-5442</kbd> [CYCLONE] If replicating the column with a unique attribute, then the transaction may fail.

<a id="84f8ebb9857f55ad"></a>
##### Description

If a column has a unique attribute in the table to replicate, then it is normally processed in an source database, but unique violation or NO_ROWS error may occur in a remote database. Therefore, to solve this problem, the feature to control concurrency of the column has been added when replicating the column with the unique attribute.

<a id="cee071d4c544f8cc"></a>
##### Symptom

```
[APPLIER #1(SID:100)-INSERT] ERR-23000(16057) : unique constraint (PUBLIC.TEST1) violated

[APPLIER #2(SID:101)-UPDATE] Conflict.

[APPLIER #3(SID:102)-DELETE] Conflict.
```

If a column has a unique attribute in the replicating table, then logs are frequently recorded on the trace log of the slave as given above.

<a id="053833acea23f67a"></a>
##### Workaround

The patch is required.

<a id="ea16597ce8045e39"></a>
#### <kbd>ISSUE-5568</kbd> [CYCLONE] If replicating recovery spans two redo log files, then the starting point of the recovery is incorrectly set.

<a id="39703d2ef121787c"></a>
##### Description

When restarting after terminating the replication, cyclone finds the starting point of the recovery by using the information applied to the existing applier, then restarts the replication.

When recovering, it finds the optimal starting point by comparing the information between multiple appliers. If the redo log file information between appliers is different, then it discards the information of the old redo log file, and determines the starting point of the recovery by using only the new redo log file information, and this error has been fixed.

<a id="474d5f60d4cedf72"></a>
##### Symptom

When restarting after terminating the replication, a transaction may not be replicated.

<a id="57b24a1681fffe94"></a>
##### Workaround

The patch is required.

<a id="7ddba1741c74dcf6"></a>
### 21c.1.25 Patch Notes

<a id="37c03bb46e68f9b8"></a>
#### <kbd>ISSUE-5511</kbd> [CYCLONE] The internal transaction ID is set incorrectly in the distributor.

<a id="45cc0c618c885388"></a>
##### Description

It is guaranteed that the transaction IDs are not duplicated among simultaneously performed transactions in an original database. However, the completed transaction ID can be reused later.

When transferring the transaction to the slave after extracting the original transaction for the replication, the execution time of the transaction ID may be different from the original due to the parallel apply. In this case, the slave changes the separate transaction ID into the internally distinguishable ID to prevent identity duplication by reusing the transaction ID.

This internal transaction ID is allocated by the distributor, but it uses the original value instead of the internal value while analyzing specific logs, so the problem occurs, which a single transaction has two transaction IDs.

Two transaction ID values used as a delimiter value of concurrency control in distributor are allocated to a single transaction, so self dead-lock may occur in a specific situation.

<a id="ec091d14cb972aab"></a>
##### Symptom

```
CREATE TABLE T1 ( C1 INTEGER PRIMARY KEY, C2 LONG VARCHAR );

INSERT INTO T1 VALUES( 1, 'AAA' );
DELETE FROM T1 WHERE C1=1;
INSERT INTO T1 VALUES( 1,'AAAAAAA .......' );  ❶ INSERT the data over 8K
COMMIT;
```

As above, if performing the query processing the same key value and INSERT which inserts the record over 8K in a single transaction, then the dead-lock occurs.

<a id="6755aca98b2116b4"></a>
##### Workaround

The patch is required.

<a id="e2875e24f79be55a"></a>
#### <kbd>ISSUE-5505</kbd> If the access method for leftmost table in the join is the unique index access, and only part of key columns in the group by belong to the unique index, then the result may be wrong.

<a id="11fdc934318ab155"></a>
##### Description

If the access method for leftmost table in the join is the unique index access, and only part of key columns in the group by belong to the unique index, then the result may be wrong.

<a id="4d5ca5275f5d9c8c"></a>
##### Symptom

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

The result from the query above should be 6 rows, but actually 18 rows are output. The leftmost table s uses 'S_PRIMARY_KEY_INDEX', so the join result is sorted for s.c1. In the plan above, group by performs the grouping by using the sorted result of the join. However, the sorted records are not sorted for all group key columns, so it may lead to the wrong result.

<a id="9ff108bbd3f44a3f"></a>
##### Workaround

Use */*+ USE_GROUP_HASH */* hint.

<a id="8b4698def93ee811"></a>
#### <kbd>ISSUE-5445</kbd> Even if LOGFILE GROUP size is set sufficiently it fails to add LOGFILE GROUP when performing ADD LOGFILE GROUP.

<a id="6b1f1d2c787d0369"></a>
##### Description

Even if LOGFILE GROUP size is set sufficiently it fails to add LOGFILE GROUP with a error message saying the logfile is smaller than the minimum size.  
It is because the minimum size of the logfile should be calculated based on the number of log buffers and pending log buffers which were revised during the startup, but actually it is calculated based on the property value when performing ADD LOGFILE GROUP.

<a id="9e8e9a5e91e460bc"></a>
##### Symptom

If attempting to add a logfile group after starting up to mount phase with PROPERTY set as follows, then it fails.

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

<a id="3c9b5de43e5de0cd"></a>
##### Workaround

Create a logfile group by revising LOG_BUFFER_SIZE property and PENDING_LOG_BUFFER_COUNT property.

<a id="f233f90e24d0e3c8"></a>
#### <kbd>ISSUE-5424</kbd> If executing SELECT statement of an embedded SQL without INTO clause, then an error occurs even when the data exists, and this error has been fixed.

<a id="a707ce25a254feb0"></a>
##### Description

If repeatedly executing SELECT statement of an embedded SQL without INTO clause, then an error occurs, and this error has been fixed.

<a id="82a8d3f8b9f95cbf"></a>
##### Symptom

```
EXEC SQL SELECT 1 FROM DUAL;

EXEC SQL SELECT 1 FROM DUAL;
```

If repeatedly executing the same SELECT statement as given above, then the following error occurs.

```
Invalid cursor state : A cursor was open on the StatementHandle.
```

<a id="6aa7ca2c43c7e602"></a>
##### Workaround

Add INTO clause to the SELECT statement, then execute it.

<a id="312648ea9bb722b8"></a>
#### <kbd>ISSUE-5407</kbd> Cluster peer which is waiting for the lock to be release can not recognize that driver node is killed.

<a id="87ed5f674d6c5c48"></a>
##### Description

If the driver member is abnormally terminated while waiting for the lock to be released on the remote, then the remotely created session remains alive.

<a id="8bd4c20c14239686"></a>
##### Symptom

The following is an example of an environment that the cluster group G1 has G1N1, G1N2 as members, and the table T1 is created.

The record of table T1 is updated on G1N1.

```
gSQL> UPDATE T1 SET A = A + 1 WHERE A = 1;

1 row updated.
```

If the same record is updated on G1N2, then it will wait.

```
gSQL> UPDATE T1 SET A = 10 WHERE A = 1;
```

When checking the session on G1N1, then it is seen that the cluster session is waiting for the update sent from G1N2.

```
gSQL> SELECT SESSION_STATUS FROM V$SESSION@G1N1
       WHERE PROGRAM_NAME = 'cluster peer';

SESSION_STATUS
--------------
CONNECTED
```

Even when gsql waiting for the update sent from G1N2 is killed, the session still remains alive on G1N1 as follows.

```
gSQL> SELECT SESSION_STATUS FROM V$SESSION@G1N1
       WHERE PROGRAM_NAME = 'cluster peer';

SESSION_STATUS
--------------
CONNECTED
```

<a id="e4db503626d79be6"></a>
##### Workaround

The patch is required.

<a id="48629a167054b4e8"></a>
### 21c.1.24 Patch Notes

<a id="85315accfa87342a"></a>
#### <kbd>ISSUE-5398</kbd> The data is lost when gloader uploads the data in the text mode, and this error has been fixed.

<a id="4a133a742f9a5b0d"></a>
##### Description

gloader uses the field delimiter and the line delimiter which start with the same character when uploading the data in the text mode. If the data includes the first character of these delimiter, then the data is truncated and uploaded in an invalid form, and this error has been fixed.

<a id="d508eec972b0aec9"></a>
##### Symptom

The following is an example of a data file.

```
data 1^^^Cc__Cc^data 2^Rr__Rr
```

The following is an example of a control file.

```
TABLE TEST
FIELD TERMINATED BY '^Cc__Cc^'
LINE TERMINATED BY '^Rr__Rr\n'
```

If uploading the data by using the control file and the data file above, then the data is truncated.

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

<a id="e23f9ef1c7e96ae7"></a>
##### Workaround

Use the the field delimiter and the line delimiter which start with the different character each other.

<a id="79ab5b192c21bdac"></a>
#### <kbd>ISSUE-5174</kbd> gpec supports declaring function arguments.

<a id="25d5f9a973a32790"></a>
##### Description

gpec supports declaring function arguments. For more information, refer to [Declaring Function Argument](../part-05-developer-manual/33-embedded-sql.md#f46118cf38208e11).

<a id="7a9d22ab209fa8e5"></a>
##### Symptom

N/A

<a id="bccebb2db79e56a9"></a>
##### Workaround

The patch is required.

<a id="fd4ed202887c85ea"></a>
#### <kbd>ISSUE-5353</kbd> When connecting and disconnecting by using the window ODBC, then the number of program handles increase and this error has been fixed.

<a id="c712f5cd16ccce95"></a>
##### Description

When repeatedly connecting and disconnecting by using the window ODBC, then the number of entire program handles increase and this error has been fixed.

<a id="d952e24dd068c743"></a>
##### Symptom

When repeatedly connecting and disconnecting by using the window ODBC, then the number of entire program handles increase.

<a id="2940268703820557"></a>
##### Workaround

The patch is required.

<a id="445b52301b058153"></a>
#### <kbd>ISSUE-5344</kbd> When performing view projection pruning it deletes the column used in the upper block.

<a id="bd3408a8dfa80482"></a>
##### Description

If the following conditions are satisfied, the server may be abnormally terminated due to improperly performed view projection pruning.

- *group by* or *order by* exists within a view.
- expr to be deleted from the view's select list is an argument of another function expression.

<a id="bf84a4c34c386e11"></a>
##### Symptom

The following is a sample query which can cause an error.

```
SELECT sum_col1
  FROM ( SELECT sum(col1) as sum_col1
              , DECODE( sum(col1), NULL, 0 ) as decode_sum_col1
           FROM t1
          GROUP BY col2 
       ) v1;
```

decode_sum_col1 is not used in the upper block in v1, so it is pruned. Moreover, sum(col1) which is an argument of DECODE is also pruned. However, sum(col1) is already specified in select list and it is used in the view's upper block, so it should not be deleted.

<a id="5437a5c210b98837"></a>
##### Workaround

The patch is required.

<a id="6724252ac06f4b1c"></a>
#### <kbd>ISSUE-5336</kbd> When using SUBQUERY in SELECT INTO statement of gpec, then it is not processed as a SELECT INTO statement.

<a id="b4d2e2680e87d432"></a>
##### Description

If gpec parses the SQL which has SUBQUERY after a SELECT INTO statement, then it is not processed as a SELECT INTO statement.

<a id="4a57eec3036e0dd3"></a>
##### Symptom

The following is an example of using SUBQUERY after using the host variable array in a SELECT INTO statement.

```
EXEC SQL BEGIN DECLARE SECTION;
int no[10];
int count[10];
EXEC SQL END DECLARE SECTION;

EXEC SQL SELECT empno, B.COUNT 
    INTO :no, :count,
    FROM emp, (SELECT count(*) as COUNT FROM emp);
```

When performing the example above, then the following error occurs.

```
SQLCODE :-16289
SQLSTATE: 42000
ERROR MSG : into clause can have only one row
```

<a id="e8bd8655a612ce2a"></a>
##### Workaround

Fetch the cursor instead of using the host variable array in a SELECT INTO statement.

<a id="a930a246bbca18e7"></a>
#### <kbd>ISSUE-4945</kbd> Use SQLTables to check the existence of the table while creating a table to operate CYCLONE, CYMON.

<a id="c1f49951883aaffd"></a>
##### Description

It has been modified to create the table after checking the existence of the table required to operate CYCLONE, CYMON by using SQLTables.

<a id="ab7434e863591440"></a>
##### Symptom

N/A

<a id="7fdfd36b3d9ec590"></a>
##### Workaround

Validate the table existence when preparing, then use the result to determine whether the table exist.

<a id="4e29637143bec775"></a>
#### <kbd>ISSUE-5245</kbd> CLUSTER_PACKET_ALLOCATION_TIMEOUT should be processed in the unit of second.

<a id="6f9f254ffa21138a"></a>
##### Description

The unit of CLUSTER_PACKET_ALLOCATION_TIMEOUT is second, but it is internally processed in the unit of micro second.

<a id="34c8cfd8fdd35719"></a>
##### Symptom

If multiple load protocols occur due to the cluster pusher plan, then the following error frequently occurs.

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

<a id="1d58e8f249f84d13"></a>
##### Workaround

The patch is required.

<a id="3ba672ef18a8c6b6"></a>
#### <kbd>ISSUE-5029</kbd> Even when the master rejoins with reset all option while operating Cyclone in the cluster environment, but the existing replication information is not initialized.

<a id="0d43fad4f2e37de3"></a>
##### Description

When restarting the previously operated master with reset all option while Cyclone is operating in the cluster environment, then it should not use the existing replication information, and the replication should be resumed from the current time.

<a id="cb2e4874d9ac0536"></a>
##### Symptom

Even when restarting the master with reset all option, the recovery process uses the existing replication operating information.

<a id="cdee7dbc597c42a4"></a>
##### Workaround

The patch is required.

<a id="3e219725ae9a13da"></a>
### 21c.1.23 Patch Notes

<a id="46050d5fd8560502"></a>
#### <kbd>ISSUE-5132</kbd> It supports DML execution for the single domain table without the global secondary index in the cluster environment.

<a id="71e08ec8e6b7ae8a"></a>
##### Description

If the global secondary index is not configured when executing DML for the single domain table in cluster environment, then it may fail. DML query requires the global secondary index to guarantee the data consistency between servers. Therefore, if the data is stored in a single server, and it is not required to guarantee the data consistency between server, then it supports DML without the global secondary index.

It is recommended to configure the global secondary index to manage a single table in multiple servers in cluster environment.

<a id="cfe7b4cc0aef046b"></a>
##### Symptom

```
--# G4 group has G4N1 only.
CREATE TABLE r ( c1 INTEGER )
   CLONED
   AT CLUSTER GROUP g4
   WITHOUT GLOBAL SECONDARY INDEX;

--# result: success
INSERT INTO r VALUES (1), (2), (3);

--# Improvement
--# result: success
DELETE FROM r WHERE c1 = 2;

ERR-42000(16519): global secondary index expected in cluster DML
```

<a id="a7fbeadd971e1640"></a>
##### Workaround

The patch is required.

<a id="28dd3b6507ab635e"></a>
#### <kbd>ISSUE-5193</kbd> When executing a query including index backward scan in cluster environment, then the result is wrong.

<a id="0ee6f2da99d472fa"></a>
##### Description

When executing the user query in cluster environment, if it is required to access the remote server and the user query includes index backward scan by ORDER BY statement or by a hint, then the query result may be in an order of index forward scan.

<a id="db83bce3a72d7027"></a>
##### Symptom

If it is required to access the remote server when executing the user query in cluster environment, then the generated query is configured and transferred to the remote server. However, the remote server performs the index forward scan because the access path hint information is wrong when configuring the generated query including the index backward scan.

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

<a id="f450b7132fe69058"></a>
##### Workaround

The patch is required.

<a id="add890296ed3789f"></a>
#### <kbd>ISSUE-5109</kbd> Cyclone malfunctions after shard rebalancing and split brain, and this error has been fixed.

<a id="0a23cb5e5116b0c5"></a>
##### Description

When recovering after shard rebalancing and split brain, Cyclone is terminated with "internal error occurred (Not Need Rebalance)" error.

<a id="3b70b0045eaabe7f"></a>
##### Symptom

Even when cyclone determines rebalancing is not required, but it is rebalanced in a specific situation. This may happen in shard rebalancing and split brain situation.

<a id="1ff94efbc4bccdec"></a>
##### Workaround

Restart Cyclone with --reset.

<a id="f3fc8c7b332f8e3b"></a>
#### <kbd>ISSUE-5162</kbd> Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC, it may wait longer than the settings, and this error has been fixed.

<a id="03cb6c95ba825e0f"></a>
##### Description

Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC to detect the network disconnection, it may wait longer than the given timeout setting, and this error has been fixed.

<a id="41b4b6347a5f1f7b"></a>
##### Symptom

Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC, it can not detect the network disconnection in a specific situation, so it keeps waiting for the server's response in ODBC.

<a id="dcb270547038e354"></a>
##### Workaround

Add the following attributes to odbc.ini, so that it can quickly detect the network disconnection.

- KEEPALIVE_IDLE_TIME
- KEEPALIVE_INTERVAL
- KEEPALIVE_COUNT

Or, alter the following kernel attributes, so that it can quickly detect the network disconnection.

- net.ipv4.tcp_keepalive_intvl
- net.ipv4.tcp_keepalive_probes
- net.ipv4.tcp_keepalive_time
- net.ipv4.tcp_retries2

<a id="cf22ce57a25a2c77"></a>
#### <kbd>ISSUE-5160</kbd> When LONGVARCHAR, LONGVARBINARY parameters exist in ODBC global connection environment, the client's memory increases, and this error has been fixed.

<a id="cc7a9fddd1ec1425"></a>
##### Description

When repeatedly performing the statement including LONGVARCHAR, LONGVARBINARY parameters in ODBC global connection environment, the client's memory increases, and this error has been fixed.

<a id="058e5b2bda29e528"></a>
##### Symptom

When repeatedly performing the SQL including LONGVARCHAR, LONGVARBINARY parameters with the same statement in ODBC global connection environment, the client's memory increased.

<a id="14dd6d766cb8321f"></a>
##### Workaround

The patch is required.

<a id="905c653b043d2256"></a>
#### <kbd>ISSUE-5156</kbd> SQLSTATEs of some errors have been changed.

<a id="e649f65343bc31f8"></a>
##### Description

SQLSTATEs of some errors have been changed.

<a id="69de98346da46947"></a>
##### Symptom

SQLSTATEs of some errors have been changed as follows.

<a id="5e8979beecc29381"></a>
| Error number | Old SQLSTATE | Modified SQLSTATE | Message |
| --- | --- | --- | --- |
| 13034 | RD000 | 08S01 | Service is not available |
| 16351 | 08000 | HY000 | failed to connect to the cluster member '%s' |
| 16523 | HY000 | 08S01 | the database system is shutting down |
| 25001 | HY000 | 08001 | Server is not running |

<a id="5c237df1cec57f9f"></a>
##### Workaround

The patch is required.

<a id="789b6daa582a753e"></a>
#### <kbd>ISSUE-5147</kbd> Even when it was set as PROTOCOL=TCP in the configuration of CYMON, it was connected by using DA, and this error has been fixed.

<a id="b22f7060f4c08369"></a>
##### Description

Even when it was set as PROTOCOL=TCP in the configuration of CYMON, it was connected by using DA. However, this error has been fixed, so it is connected by using TCP now.

<a id="cae10374d99a1aee"></a>
##### Symptom

If it is set as PROTOCOL=TCP in the configuration of CYMON, it should be connected by using TCP, but, in reality, it is connected by using DA.

<a id="a6bc9315b6b1b541"></a>
##### Workaround

The patch is required.

<a id="24fcff8af73a30ba"></a>
#### <kbd>ISSUE-5124</kbd> If it fails to allocating dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="3d132868899e79fe"></a>
##### Description

If it fails to allocating dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="7eaf006b08be0146"></a>
##### Symptom

If it fails while multiple threads allocate a single dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="fa4002c50047f08f"></a>
##### Workaround

The patch is required.

<a id="67d55fd04ce4f2ac"></a>
#### <kbd>ISSUE-4985</kbd> The progressing information in slave has been added to the CYCLONE's monitoring information.

<a id="e2e938ca51a70552"></a>
##### Description

The information being processed in slave (Apply_FileSeq, Apply_BlockSeq, Apply_Commit_Lsn) has been added to the CYCLONE's monitoring information.

<a id="05cda7fdedb07fb1"></a>
##### Symptom

N/A

<a id="2573f7e54069a610"></a>
##### Workaround

The patch is required.

<a id="ff1cf4a7c2211833"></a>
#### <kbd>ISSUE-4882</kbd> It is modified to report the detatiled error message when an error occurs while processing CYCLONE SYNC.

<a id="3438fb1b4db0935e"></a>
##### Description

It is modified to record the detailed error message together with *ERROR OCCURRED* on the trace log when an error occurs while processing CYCLONE SYNC.

<a id="126dbd9389014f46"></a>
##### Symptom

N/A

<a id="cff04e25c6a4f769"></a>
##### Workaround

The patch is required.

<a id="912267075291a694"></a>
### 21c.1.22 Patch Notes

<a id="4225997cec93e7ad"></a>
#### <kbd>ISSUE-5030</kbd> When performing ALTER SYSTEM JOIN DATABASE, the SNIPED session is not cleared.

<a id="f57b86f037b873b7"></a>
##### Description

When performing ALTER SYSTEM JOIN DATABASE, topology information among cluster members temporarily do not match. And if COMMIT occurs at this moment, then it infinitely waits for invalid COMMIT result due to the wrong topology information.

<a id="fe25eb9629fe7dbc"></a>
##### Symptom

When performing ALTER SYSTEM JOIN DATABASE after restarting a member in cluster environment, if COMMIT occurs for the member, then intermittently it is not normally processed but it infinitely waits for the result.

<a id="a56fe5de39bfe85b"></a>
##### Workaround

Restart the server.

<a id="89745b54fd8500ff"></a>
#### <kbd>ISSUE-5004</kbd> A deadlock occurs on the slave's pre-process phase during the replication with cyclone in the cluster environment.

<a id="f44f44aa0357d86a"></a>
##### Description

A deadlock intermittently occurs during the replication with cyclone in the cluster environment.

<a id="eb48ac96f01bdcc0"></a>
##### Symptom

The replication is not proceeding and it seems to be stop. It is because a deadlock occurs during the pre-process for the replication in the cluster environment. The replication is not proceeding any more even when monitoring with cymon.

<a id="885c073fb7eeea3d"></a>
##### Workaround

Reset the master and the slave of cyclone.

<a id="8420a12ec7c2f06b"></a>
### 21c.1.21 Patch Notes

<a id="86baf93bca5230ab"></a>
#### <kbd>ISSUE-4933</kbd> If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client.

<a id="cc3426d43ebbc247"></a>
##### Description

If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client.

<a id="78c00031a4249255"></a>
##### Symptom

If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client. However, in reality, it does not transfer XA error and it is operated as if it succeeds.

<a id="bb6985ebf18b48d6"></a>
##### Workaround

The patch is required.

<a id="b2ce821c3a400f63"></a>
#### <kbd>ISSUE-4882</kbd> When performing cyclone sync, string data right truncated error occurs for the long variable datatype.

<a id="eafc2984761fe9c3"></a>
##### Description

While performing cyclone sync, string data right truncated error occurs.

<a id="9c6ea7fabd8b4be2"></a>
##### Symptom

An error may occur when syncing the table including a long varchar/ varbinary type column. This error occurs because the null padding of the buffer used for the sync is lost, and it occurs when the column data size is 8 Kb.

<a id="ab8b7d9294fe7a2d"></a>
##### Workaround

The patch is required.

<a id="507dafcb802c8b32"></a>
#### <kbd>ISSUE-4873</kbd> It supports XA rollback feature for XA transaction which is not dissociated from the session.

<a id="2b4cf0e3ec0f45ef"></a>
##### Description

XA transaction is associated with the session until performing xa end, and to commit or rollback the XA transaction, it should be dissociated from the session. However, other DBMS support the rollback feature even when the transaction is not dissociated from the session. Therefore, it has been improved to support the same feature.

<a id="efd028d124b29ce2"></a>
##### Symptom

If performing xa rollback without performing xa end for the XA transaction in progress in the session, then an error occurs. However, it is normally operated if performing xa rollback after performing xa end.

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

<a id="3b3cf1fe11b64fbb"></a>
##### Workaround

The patch is required.

<a id="3ba060e57088f521"></a>
#### <kbd>ISSUE-4864</kbd> The shard is not refined when restarting after dropping the shard.

<a id="fb74de92381ff5d8"></a>
##### Description

If the shard is moved in ALTER TABLE REBALANCE statement, then the shard may be dropped. If restarting the server before the ager refines the dropped shards, then the dropped shard may not be refined.

<a id="131ecfea39483e7b"></a>
##### Symptom

If performing SHUTDOWN right after REBALANCE as follows, then the moved shard may not be dropped.

```
gSQL> ALTER TABLE T1 REBALANCE;

Table altered.

gSQL> \SHUTDOWN ABORT

Shutdown success
```

<a id="37d842d72533500f"></a>
##### Workaround

The patch is required.

<a id="b914942cb22ebd63"></a>
#### <kbd>ISSUE-4863</kbd> Lock is not converted to optimistic mode after REBALANCE.

<a id="605e312c7a876ee5"></a>
##### Description

The lock which was converted to the pessimistic mode during ALTER TABLE REBALANCE is not converted to optimistic mode, so the performance may be degraded.

<a id="d1e5a0c72e9b99e0"></a>
##### Symptom

If performing ALTER TABLE REBALANCE ONLINE when DML occurs, then the performance may be degraded.

<a id="c7e7516e260f1324"></a>
##### Workaround

The patch is required.

<a id="6294efe52fed54b7"></a>
#### <kbd>ISSUE-4850</kbd> When using async commit, the sequence of the journal record may be reversed.

<a id="2072a172f469193c"></a>
##### Description

If DML occurs while performing ONLINE REBALANCE in the environment where asynchronous commit is set then the sequence of the journal record may be reversed. If so, the process performing REBALANCE may be abnormally terminated during the journal replay.

<a id="5a7a387af27591ce"></a>
##### Symptom

If performing REBALANCE in the environment where asynchronous commit is set, and insert and delete occur in the same record of each different transaction as follows, then the process performing REBALANCE may be abnormally terminated.

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

<a id="7513b76d111fec65"></a>
##### Workaround

Set *asynchronous commit* to FALSE.

<a id="16344bcdcca147c6"></a>
### 21c.1.20 Patch Notes

<a id="fc4c1ed0d0152d2b"></a>
#### <kbd>ISSUE-4753</kbd> When enquiring USER_TABLES, the global temporary table is not viewed.

<a id="736a7b2b78b03285"></a>
##### Description

When enquiring the dictionary view such as USER_TABLES, ALL_TABLES and DBA_TABLES, the global temporary table is not viewed.

<a id="6ac0e87ab596daaf"></a>
##### Symptom

Even though enquiring the global temporary table through USER_TABLES after the global temporary table has been created as follows, but the global temporary table is not viewed.

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

The correct result is viewed as follows after patching.

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

Execute DictionarySchema.sql to apply the patch as follows.

- Standalone

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
```

- Cluster

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
```

<a id="4361eeede59a13c4"></a>
##### Workaround

Enquire the SQL standard INFORMATION_SCHEMA.TABLES.

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

<a id="b1f0907977d9a031"></a>
#### <kbd>ISSUE-4720</kbd> When the file system storage space is full, then the system thread is abnormally terminated.

<a id="b5833bfec2565e71"></a>
##### Description

Previously, gmaster archive thread was abnormally terminated, when the file system storage space for the archive log was full. However, it is modified not to terminate the thread but to perform the failed archive again when the file system space becomes sufficient.

<a id="78c6525a29e192fe"></a>
##### Symptom

If the file system was full during creating the archive log, then the archive failed, and gmaster archive thread was abnormally terminated.

<a id="bd0b90343e11cb0b"></a>
##### Workaround

The patch is required.

<a id="dc4b63deb76e7eb0"></a>
### 21c.1.19 Patch Notes

<a id="db4bb6a9679e4da4"></a>
#### <kbd>ISSUE-4713</kbd> Conflict error occurs in slave when replicating cyclone.

<a id="ab4c0f1bdba19514"></a>
##### Description

If CLUSTER_ASYNC_COMMIT property for slave is set to YES, then update conflict error occurs.

<a id="fa541baf171e7246"></a>
##### Symptom

When CLUSTER_ASYNC_COMMIT property is set to YES, if the value applied by an applier is not completely committed and another applier accesses to the record which was just applied, then conflict error may occur.

Therefore, it is modified to set CLUSTER_ASYNC_COMMIT to NO when starting cyclone slave.

<a id="f8326ba18607a9b8"></a>
##### Workaround

Set CLUSTER_ASYNC_COMMIT of GOLDILOCKS where slave is operated to NO.

```
gSQL> ALTER SYSTEM SET CLUSTER_ASYNC_COMMIT=NO;
System altered.
```

<a id="5dd0f004e22d5781"></a>
#### <kbd>ISSUE-4709</kbd> Query execution for the local node may fail on local open phase.

<a id="67d43dbdcded41d6"></a>
##### Description

If enquiring the table by connecting to the node on local open phase in cluster environment, then an error occurs.

<a id="e6da3a00e13c2702"></a>
##### Symptom

If the connected node is on local open phase, then it can not access the remote node but it can access the local node. However, if it determines that the node on local open phase can not access the local node, then the query fails.

The following is an example of an error occurred when executing the query on G1N1 on local open phase.

```
gSQL> SELECT * FROM v$datafile;

ERR-HY000(16354): connection of member 'G1N1' is broken
```

It determines whether the current node can access a specific node based on the connection information. However, if it can not refer to the connection information in case when it is on local open phase, then it may determine that it can not access the current node either.

It is modified to determine that it can access the current node even when it can not refer to the connection information.

<a id="fe71a1982972e2ea"></a>
##### Workaround

The patch is required.

<a id="0a35a8b5b514c3f2"></a>
#### <kbd>ISSUE-4693</kbd> If the inner query of the view is left outer join which has both *on filter* and *where filter*, and this view is merged, then the result may be wrong.

<a id="3506271c15358a35"></a>
##### Description

If the inner query of the view is left outer join which has both *on filter* and *where filter*, and this view is merged, then the result may be wrong.

<a id="08998eb8a4cc44f5"></a>
##### Symptom

The result of the query below is 1, but the actual output result is 2.

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

In the query above, s_c1 column of v1's inner query is not used out of view. Therefore, it is dropped on query transform phase, then it is simple view merged.

```
SELECT 
       COUNT(*)
  FROM r LEFT JOIN s ON r_c1 = s_c1
     , t
 WHERE v1.r_c1 = t_c2
   AND r_c2 = 1
;
```

After that, left outer join whole may be dropped as follows because s_c1 is a unique key column and it is not used except for left outer join.

```
SELECT 
       COUNT(*)
  FROM r
     , t
 WHERE v1.r_c1 = t_c2
   AND r_c2 = 1
;
```

r_c2 = 1 was lost on query transform phase as given above, and it was an error. However, the error is fixed now, so the result is correct as follows.

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

<a id="ecee28b7547e2377"></a>
##### Workaround

Use */*+ NO_MERGE(v1) */* hint.

<a id="bc73ebd71b0f6b9e"></a>
#### <kbd>ISSUE-4696</kbd> View columns have been added to view the update master information of the cluster table.

<a id="2742a475e6cdd55a"></a>
##### Description

The update master in the cluster table is a member node where DML is first performed when DML occurs in the table.

The followings affect determining the update master of each cluster table.

- Positioning cluster table
- Position of members in the cluster group
- Whether it is online/ offline
- Whether to perform rebalance

IS_UPDATE_MASTER column has been added to the following dictionary views to easily view the update master information which is subject to change during the operation.

- [DBA_TAB_PLACE](../part-02-administration-manual/9-database-information.md#800e812cf3a04347)
- [ALL_TAB_PLACE](../part-02-administration-manual/9-database-information.md#a4e803ae54843007)
- [USER_TAB_PLACE](../part-02-administration-manual/9-database-information.md#4fab79a17608da9e)

<a id="e6044db0c911d57b"></a>
##### Symptom

View it as follows.

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

Cluster table R is located in groups G1, G2, G3, and the member corresponding to update master in each group is G1N1, G2N1 and G3N1.

<a id="33e36b2e0f141c9f"></a>
##### Workaround

The patch is required.

<a id="0db2fd75bf9225a8"></a>
### 21c.1.18 Patch Notes

<a id="03c8f9fa7ded14b2"></a>
#### <kbd>ISSUE-4646</kbd> If the inner query of the view is a set and it has *order by* clause, then the result is wrong.

<a id="e6b6b6c489f7911b"></a>
##### Description

If the inner query of the view is a set and it has *order by* clause, then the result is wrong. In this case, only *union all* is allowed in the set and only some view columns should be used.

<a id="8255c599754fbd71"></a>
##### Symptom

v1 view in the following example has c1, c2, c3 and c4, but it only reads c1, c3 columns. Moreover, the inner query of the view is a set clause which used *union all* only, and it has *order by*.

In this case, the result is wrong.

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

It gets the correct result after fixing the error as follows.

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

<a id="6103431f4c892504"></a>
##### Workaround

The patch is required.

<a id="7445d56e1bd724a1"></a>
#### <kbd>ISSUE-4642</kbd> If an offline member exists, it creates a pusher and performs the remote join even when it is possible to perform the remote join without the pusher.

<a id="da55ba0eb88f05fa"></a>
##### Description

If an offline member exists, it creates a pusher and performs the remote join even when it is possible to perform the remote join without the pusher.

<a id="2a83d474a2bb324b"></a>
##### Symptom

If a member of LC table (g1n2) becomes offline in the following example, then a pusher is created when performing the remote join.

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

The remote join is available without a pusher even when a member of LC table (g1n2) is offline after fixing the error as follows.

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

<a id="fee7b7871e2fa555"></a>
##### Workaround

The patch is required.

<a id="db49f83b3a6e25e3"></a>
#### <kbd>ISSUE-4678</kbd> gpec processes SELECT statement as SELECT INTO statement.

<a id="a4b6d029653435ee"></a>
##### Description

SELECT statement and SELECT INTO statement of the embedded SQL should be processed differently. However, gpec processes SELECT statement of the embedded SQL as SELECT INTO statement, then the program is intermittently and abnormally terminated.

<a id="4d71c6fde2ab3b81"></a>
##### Symptom

gpec was supposed to process the following SQL statement as SELECT statement, but it processed it as SELECT INTO statement because of the garbage value.

```
EXEC SQL SELECT * FROM DUAL;
```

<a id="0c1263ce14afa0a6"></a>
##### Workaround

Use INTO clause in SELECT statement.

<a id="31953dd17d10784e"></a>
### 21c.1.17 Patch Notes

<a id="eddb4051d298412b"></a>
#### <kbd>ISSUE-4594</kbd> If a query set exists in the subquery while performing NOT IN subquery unnesting, then the system is abnormally terminated.

<a id="fefa0c599c9fc2cb"></a>
##### Description

If a query set exists in the subquery while performing NOT IN subquery unnesting, then the system is abnormally terminated.

<a id="737eaa188ee5c3a8"></a>
##### Symptom

The following query abnormally terminates the system.

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

It is normally operated after fixing the error.

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

<a id="583e2da175b48b1b"></a>
##### Workaround

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

<a id="ad2cf738d2077fc3"></a>
#### <kbd>ISSUE-4588</kbd> It is modified to return NULL for the compatibility with Oracle when *no data found* error occurs in the function referenced from SQL.

<a id="b1605c97957af399"></a>
##### Description

If *no data found* error occurs in the function referenced from SQL, then it returns NULL.

<a id="5b503647d3efdbf1"></a>
##### Symptom

Previously, if *no data found* error occurred in the function referenced from SQL, then it returned an error.

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

<a id="67029146ecd37afd"></a>
##### Workaround

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

<a id="918dc1ba8867a819"></a>
#### <kbd>ISSUE-4609</kbd> When using two or more subquery expressions including a join combine, then a segment fault occurs.

<a id="07d35b794432d12d"></a>
##### Description

When referring to the information of the subquery expression in the statement in which two or more subquery expressions including a join combine are used, then a segment fault occurs.

The error occurred in the following clauses.

- TARGET clause
- WHERE clause
- HAVING clause
- ORDER BY clause

<a id="1f20426b015d0218"></a>
##### Symptom

When building the information to refer to the subquery expression in the clause including the subquery expression, then it can not find the related expression, so it never stops searching for the expression. Therefore, the segment fault occurs.

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

<a id="523239f07ccbebb0"></a>
##### Workaround

The patch is required.

<a id="0c61e10ee2a420f1"></a>
#### <kbd>ISSUE-4589</kbd> Complex view merging was executed even though SELECT FOR UPDATE, UPDATE, DELETE does not support the complex view merging.

<a id="aa3c68abf9ef0547"></a>
##### Description

Complex view merging was executed even though SELECT FOR UPDATE, UPDATE, DELETE does not support the complex view merging.

<a id="346a7c47759ff7c8"></a>
##### Symptom

The complex view merging should not be executed for the following query. However, the complex view merging is executed after the subquery unnesting, so the server is abnormally terminated.

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

<a id="554d749c02f1eaec"></a>
##### Workaround

The patch is required.

<a id="a7300a180899f41c"></a>
#### <kbd>ISSUE-4575</kbd> The same SQL statements are redundantly cached in an embedded SQL.

<a id="59bb553a4355c2e7"></a>
##### Description

The embedded SQL caches DML and the query statement, then recycles them when using the same SQL. If char pointer is used as the host variable, then the same SQL statements are redundantly cached.

<a id="65d69e7bc220d3b2"></a>
##### Symptom

If char pointer is used as the host variable as follows and the string length of this char pointer is changed, then SQL statement is newly created.

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

<a id="7849446abe55cac1"></a>
##### Workaround

Use char array as the host variable instead of char pointer.

<a id="1429489bf08b7874"></a>
#### <kbd>ISSUE-4566</kbd> It can not process the overflow even when the number of digits increased after the rounding off while converting the numeric type to NUMBER type.

<a id="0fb8c46549041568"></a>
##### Description

It can not process the overflow even when the number of digits increased after the rounding off while converting the numeric type to NUMBER type.

<a id="a28740aa3efa5393"></a>
##### Symptom

The following query was supposed to cause an overflow error.

```
gSQL> SELECT CAST( 9999999999.9 AS NUMBER(10,0)) FROM dual;

CAST( 9999999999.9 AS NUMBER(10,0))
-----------------------------------
                        10000000000

1 row selected.
```

<a id="306fff9c3f702390"></a>
##### Workaround

Convert it to NUMBER type after convert it to the character type.

```
gSQL> SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual;

ERR-22003(12060): data is outside the range of the data type to which the number is being converted : 
SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual
       *
ERROR at line 1:
```

<a id="25f4f315816d5f84"></a>
#### <kbd>ISSUE-4559</kbd> The trace log is output as TRACE_LONG_RUN_CURSOR even when the cursor does not exist in SELECT INTO statement.

<a id="5b9360433e1d442a"></a>
##### Description

TRACE_LONG_RUN_CURSOR property records the long run cursor which exceeds the specified time on the trace log. However, the trace log is output as TRACE_LONG_RUN_CURSOR even though SELECT INTO statement does not require the cursor, and this error has been fixed.

<a id="fc953c6f6d24bc88"></a>
##### Symptom

If SELECT INTO statement fails as follows, it is determined as TRACE_LONG_RUN_CURSOR so it records the trace log.

```
gSQL> CREATE TABLE r ( c1 INTEGER );

Table created.

gSQL> INSERT INTO r VALUES ( 1 );

1 row created.


--# It is the long run cursor trace which takes more than 1 second
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR = 1000;

System altered.


gSQL> \var v1 INTEGER
gSQL> \prepare sql SELECT c1 INTO :v1 FROM r WHERE c1 = 1 FOR UPDATE;

SQL prepared.

--# It is not recorded as TRACE_LONG_RUN_CURSOR on the trace log.
gSQL> \exec

V1
--
 1

1 row selected.


gSQL> INSERT INTO r VALUES ( 1 );

1 row created.


--# Execute after 2 seconds.
--# It is recorded as TRACE_LONG_RUN_CURSOR on the trace log.
gSQL> \exec

ERR-42000(16289): into clause can have only one row
```

<a id="1d487614cdfe9036"></a>
##### Workaround

The patch is required.

<a id="2ae35bf64f5dbcd7"></a>
#### <kbd>ISSUE-4549</kbd> When performing ADD MEMBER in a specific topology situation, an invalid member is changed to a domain coordinator.

<a id="1ce8ec6525391926"></a>
##### Description

If an added member is changed to a domain coordinator when performing ADD MEMBER, then the transaction waiting for the response from the existing domain coordinator may hang. Therefore, be cautious not to change the coordinator's location when performing ADD MEMBER.

<a id="ab722d52a121937d"></a>
##### Symptom

The global coordinator is located in the group G2, and G1N1 is ADDed at G1N2 which is a domain coordinator of the group G1.

```
ALTER CLUSTER GROUP G1 ADD CLUSTER MEMBER G1N1 HOST '127.0.0.1' PORT 11150;
```

If the domain coordinator is changed from G1N2 to a newly added member, G1N1, due to ADD MEMBER, then the transactions waiting for the response from the existing domain coordinator, G1N2, may hang.

<a id="473a71bb67c96f60"></a>
##### Workaround

Perform ADD MEMBER at the global coordinator.

<a id="d66189b62915f1ba"></a>
#### <kbd>ISSUE-4546</kbd> If it is performed in a local method when performing ORDER BY LIMIT query in cluster environment, then the result has an error.

<a id="6f04756b791f6ac7"></a>
##### Description

If it is performed in a local method when performing ORDER BY LIMIT query in cluster environment, then the result has an error.   
The same error occurs when performing GROUP BY LIMIT or DISTINCT LIMIT.

<a id="288d0e21555c366f"></a>
##### Symptom

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

When performing ORDER BY LIMIT statement in a local method as follows for the table above, then the result has an error.

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

The correct result is output as follows after fixing the error.

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

<a id="d0a23845d435fae3"></a>
##### Workaround

Use rownum instead of limit.

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

<a id="00bd08be626c176c"></a>
#### <kbd>ISSUE-4537</kbd> When performing ADD MEMBER after the incorrect DROP TABLESPACE statement succeeds, then the new member is abnormally terminated.

<a id="8e37c604445f14f0"></a>
##### Description

If performing ADD MEMBER when DROP TABLESPACE statement succeeds though it was supposed to fail, then the newly added cluster member is abnormally terminated, so ADD MEMBER fails.

It is modified to cause an error when the DROP TABLESPACE's target tablespace was set as the user's default tablespace.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1
         TEMPORARY TABLESPACE temp_tbs;

User created.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

ERR-42000(16133): cannot drop tablespace: "TEMP_TBS" is default tablespace of user "U1"
```

To drop the tablespace, modify the user's default tablespace as follows first then drop it.

```
gSQL> ALTER USER u1 TEMPORARY TABLESPACE mem_temp_tbs;

User altered.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

Tablespace dropped.
```

<a id="88617785d48ffae3"></a>
##### Symptom

DROP TABLESPACE succeeds as follows though the user's default tablespace was unable to drop.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1
         TEMPORARY TABLESPACE temp_tbs;

User created.

gSQL> DROP TABLESPACE temp_tbs CASCADE;

Tablespace dropped.
```

Then, if a new cluster member is added as follows, then the new member(g2n3) is abnormally terminated, so ADD MEMBER fails.

```
gSQL> ALTER CLUSTER GROUP g2 ADD CLUSTER MEMBER g2n3 HOST '127.0.0.1' PORT 12350;
```

<a id="0ce96131b5c5b260"></a>
##### Workaround

Before performing ADD MEMBER, it is required to find the user violating DROP TABLESPACE integrity and modify the user's default tablespace as follows.

If the result of the following query exists, then it is required to modify the user's default tablespace.

```
SELECT auth.authorization_name
  FROM definition_schema.authorizations@local AS auth
     , definition_schema.users@local AS usr
 WHERE auth.auth_id = usr.auth_id
   AND NOT EXISTS ( SELECT *
                      FROM definition_schema.tablespaces@local AS tbs
                     WHERE tbs.tablespace_id = usr.default_data_tablespace_id );
```

If the result of the following query exists, then it is required to modify the user's temporary tablespace.

```
SELECT auth.authorization_name
  FROM definition_schema.authorizations@local AS auth
     , definition_schema.users@local AS usr
 WHERE auth.auth_id = usr.auth_id
   AND NOT EXISTS ( SELECT *
                      FROM definition_schema.tablespaces@local AS tbs
                     WHERE tbs.tablespace_id = usr.default_temp_tablespace_id );
```

If the result of the following query exists, then it is required to modify the user's index tablespace.

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

<a id="c4a2ade32cb5856b"></a>
### 21c.1.16 Patch Notes

<a id="f1068385a4c5a33c"></a>
#### <kbd>ISSUE-4500</kbd> If performing the index scan by using another OR condition when the join condition includes OR condition, then the query waits infinitely.

<a id="bb5b4437446c5560"></a>
##### Description

When the join combine method is selected by the join condition including OR condition, and the column included in the join combine is referenced in the relation to which another join belongs, then it waits infinitely.

<a id="2ed275ae51baf410"></a>
##### Symptom

When referring to the column included in the join which consists of join combine as follows, then it can not find the column information, so it waits infinitely.

```
gSQL> CREATE TABLE T1( C1 INT, C2 INT );

Table created.

gSQL> CREATE INDEX IDX_T1_C1 ON T1( C1 );

Index created.

gSQL> CREATE INDEX IDX_T1_C2 ON T1( C2 );

Index created.

gSQL> INSERT INTO T1 VALUES ( 1, 1 );

1 row created.

--# Infinite waiting
gSQL> SELECT *
  FROM T1 A, T1 B
 WHERE ( A.C1 = B.C1 OR A.C1 = B.C2 )
   AND EXISTS( SELECT 1
                 FROM T1 C
                WHERE ( C.C1 = A.C1 OR C.C2 = A.C1 ) );
```

<a id="2755ba86dfb26af3"></a>
##### Workaround

Use NO_USE_JOIN_COMBINE hint as follows so that JOIN COMBINE would not be configured.

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

<a id="216e278e4d3eec4f"></a>
### 21c.1.15 Patch Notes

<a id="d45a096bcb9abe5d"></a>
#### <kbd>ISSUE-4480</kbd> When defining %TYPE which refers to the column whose reserved word is the column name, then an error occurs.

<a id="82c8ef199fb0ec56"></a>
##### Description

When defining %TYPE which refers to the column whose reserved word is the column name, then an error occurs.

<a id="12fa5e43f311c685"></a>
##### Symptom

An error occurs because it can not find the column information though OFFSET column exists in the table as follows.

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

<a id="e75f5cfb1fd31839"></a>
##### Workaround

The patch is required.

<a id="1c722c60254428b6"></a>
#### <kbd>ISSUE-4472</kbd> When outputting DDL_DB, the schema privilege DDL is not output.

<a id="1fae4c37056d8db6"></a>
##### Description

If outputting DDL_DB when two or more schema are created, then only part of them are output and other are not output.

<a id="6f0fb2b417c53a85"></a>
##### Symptom

Three schema privilege DDLs should have been created in the example below, but actually only one DDL is created.

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

...Ellipsis...

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

...Ellipsis...
```

Three schema privilege DDLs are created after solving the problem.

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

...Ellipsis...

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

...Ellipsis...
```

<a id="44343c967e5fc61d"></a>
##### Workaround

Output GRANT information per each schema.

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

<a id="ee4cbbed80b9e334"></a>
#### <kbd>ISSUE-4471</kbd> When creating TABLESPACE with DISK TABLESPACE statement which was output with DDL_DB command, then a syntax error occurs.

<a id="6ef251b221452641"></a>
##### Description

When creating TABLESPACE with CREATE DISK TABLESPACE statement which was output with DDL_DB command, then a syntax error occurs.

<a id="807d69d5deb4dfe1"></a>
##### Symptom

3. Create the tablespace.

```
gSQL> CREATE DISK DATA TABLESPACE disk_test_01 DATAFILE 'DISK_TEST_01.dbf' SIZE 100M;
COMMIT;
```

4. Input *\ddl_db*.

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

... Ellipsis ...
```

5. Input tablespace DDL statement which was output by executing *\ddl_db* command in step 2.

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

<a id="6a9046a987b368e0"></a>
##### Workaround

Modify the location of AUTOEXTEND OFF and AT &lt;domain_name&gt; in CREATE TABLESPACE statement which was output with *\ddl_db*, then execute it.

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

<a id="cbc56ad3a9614ef7"></a>
### 21c.1.14 Patch Notes

<a id="9bd2e34aa9f1c522"></a>
#### <kbd>ISSUE-4467</kbd> When *failed to synchronize replicas* error occurs, then it is output on the trace log.

<a id="73ed654e72c407b1"></a>
##### Description

When *[ERR-56008] failed to synchronize replicas* error occurs, then it is output on the trace log.

<a id="2810dc893f6aa6e8"></a>
##### Symptom

N/A

<a id="3478419af57a8062"></a>
##### Workaround

The patch is required.

<a id="41244751c1a6afad"></a>
### 21c.1.13 Patch Notes

<a id="46d914ea43389cd5"></a>
#### <kbd>ISSUE-4454</kbd> When TRACE_LOG_ID = xxxxx1 is set, the performance time of the query per section is not output on the trace log.

<a id="999598264b2a4ced"></a>
##### Description

When TRACE_LOG_ID = xxxxx1 is set, the performance time of the query per section is not output on the trace log. The ones place in TRACE_LOG_ID is the flag which determines whether to output the performance time per section, and it outputs the time when the value is 1.

<a id="3c787d704327ac3d"></a>
##### Symptom

When TRACE_LOG_ID = xxxxx1 is set, the performance time of the query per section is not output on the trace log.

```
[S][0.000000] SELECT * FROM dual

... Ellipsis ...

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

<a id="2243c6968b955547"></a>
##### Workaround

The patch is required.

<a id="ee018f8ace04488b"></a>
#### <kbd>ISSUE-4439</kbd> If only the column which is not boolean type is specified in WHERE clause, then it may abnormally terminated.

<a id="67d3306e92af0ca2"></a>
##### Description

If only the column which is not boolean type is specified in WHERE clause, then it may abnormally terminated. If it is classified as a physical filter, then it is also a bug even when it is not abnormally terminated.

<a id="7860b35306dfec0f"></a>
##### Symptom

table_name in the query below is varchar type and it is classified as a physical filter, then it is abnormally terminated during the process.

```
SELECT table_name 
  FROM DICTIONARY_SCHEMA.USER_TABLES
 WHERE table_name;
```

It is normally operated as follows after fixing the bug, and an error occurs.

```
SELECT table_name 
  FROM DICTIONARY_SCHEMA.USER_TABLES
 WHERE table_name;

ERR-22018(12123): data is not boolean literal
```

<a id="a116cc74d4129dad"></a>
##### Workaround

The patch is required.

<a id="eec96096a4dc28c1"></a>
#### <kbd>ISSUE-4434</kbd> Hang occurs when performing REBALANCE on the member who does not have the rebalance target.

<a id="de15cac8948e4ba4"></a>
##### Description

Hang occurs when performing REBALANCE on the cluster member who does not have the rebalance target target table.

<a id="0610d883e1a45c53"></a>
##### Symptom

Hang occurs when performing TABLE REBALANCE on the node who does not have the rebalance target target table.

<a id="348d95c0af0a0118"></a>
##### Workaround

The patch is required.

<a id="311268e481abcb03"></a>
### 21c.1.12 Patch Notes

<a id="4b34c4d7b8f3c5b6"></a>
#### <kbd>ISSUE-4410</kbd> It supports unnesting the subquery with SET operation.

<a id="7f09b9dcacb08521"></a>
##### Description

Unnesting the subquery with SET operation was not supported but it is now supported owe to this patch.

<a id="db5f3227c9c60e7e"></a>
##### Symptom

Unnesting the subquery with SET operation was not supported as follows.

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

However, it has been modified to enable the unnesting as follows.

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

<a id="a3699317b06168b6"></a>
##### Workaround

The patch is required.

<a id="6fdbea94b5e8abc1"></a>
#### <kbd>ISSUE-4404</kbd> The entire system stops due to the rebalancing when performing fail-back the specific node, and this has been resolved.

<a id="364b54d43a4723d2"></a>
##### Description

If rebalancing when performing fail-back the specific node, then the entire cluster is lock instead of performing x lock the group related to the node. Therefore, it has been modified to lock nodes related to the rebalance only.

<a id="2db63a7204234e62"></a>
##### Symptom

The node table which is not related to REBALANCE is X-LOCKed, so the table is not available.

<a id="11cb1316c0706477"></a>
##### Workaround

The patch is required.

<a id="7ec9239d066c4a05"></a>
### 21c.1.11 Patch Notes

<a id="45757374bc9c5a69"></a>
#### <kbd>ISSUE-4370</kbd> If the filter including the case function is used in where clause when performing the outer join, then it may abnormally terminated.

<a id="3cd4d893f96140e5"></a>
##### Description

If the filter including the case function is used in where clause when performing the outer join, then it may abnormally terminated.

<a id="db9820d90a9fd0cc"></a>
##### Symptom

It checks whether outer join operation elimination is allowed when performing the outer join. In this case, if the case function exists in the where clause, then it is abnormally terminated.

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

<a id="01326d5fc7205bfe"></a>
##### Workaround

The patch is required.

<a id="f7c67f652f4b3a94"></a>
### 21c.1.10 Patch Notes

<a id="df3d6faf0a6113fe"></a>
#### <kbd>ISSUE-4285</kbd> It has been changed to enable the filter including the stored function to perform the index join.

<a id="086984e018b8c7d3"></a>
##### Description

The filter which includes the stored function or the non-deterministic built-in function (e.g. RANDOM) could not be used as a filter determining the join method. However, it has been changed to enable it.

<a id="b83f0b36fff588fe"></a>
##### Symptom

The following is an example of obtaining the result by applying *s_c1 = func1( r_c1 )* after performing the full nested join even when the join condition exists.

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

The following is a result of performing the same query after the modification. It has been changed to perform the index nested loop join.

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

<a id="265af5c515138c2e"></a>
##### Workaround

The patch is required.

<a id="c26cc8672570d4de"></a>
### 21c.1.9 Patch Notes

<a id="e81599c899500207"></a>
#### <kbd>ISSUE-3496</kbd> It supports IPC connection.

<a id="003a011f981baf9b"></a>
##### Description

It supports IPC connection for the server and ODBC client which are located in the same device.

<a id="e7ad6058b21ce325"></a>
##### Symptom

N/A

<a id="7b2f5df4e465df96"></a>
##### Workaround

The patch is required.

<a id="3c97dbc2a9e3cde8"></a>
#### <kbd>ISSUE-4357</kbd> Boolean type has been added to the connection property of JDBC so that the effective value has been changed.

<a id="6e481e2bb4a4e7a1"></a>
##### Description

[Connection Properties](../part-05-developer-manual/32-jdbc.md#4a69930ca736a612) whose effective values are {true, false}, {on, off}, {0, 1} exist in JDBC. It has been changed to regard those connection properties as boolean type to process their effective values such as true, on, yes, 1 / false, off, no and 0 as the equivalent effective value.

<a id="9200c9d149c12252"></a>
##### Symptom

The effective value of statement_pool_on, the connection property, is either "1" or "0". If another value is used, then an error occurs. The effective value of include_synonyms is either "true" or "false", and the effective value of trace_log is either "on" or any string. What's in common for those connection properties is that the effective value is used as boolean type. Therefore, it is changed to use true, on, yes, 1 / false, off, no, 0 as the equivalent effective value to prevent the confusion in the boolean type connection properties.

<a id="c6a1c25477bbaed7"></a>
##### Workaround

The patch is required.

<a id="e994b11489c8d7c9"></a>
#### <kbd>ISSUE-4355</kbd> FAILOVER_ROUTING_POLICY property has been added in ODBC.

<a id="c21d623d42b0d5dd"></a>
##### Description

FAILOVER_ROUTING_POLICY property has been added in ODBC.

<a id="83d6987589852254"></a>
##### Symptom

Previously, if an error occurs in the last server of ALTERNATE_SERVERS, then the failover is operated in the first connected server. Therefore, FAILOVER_ROUTING_POLICY property has been added in ODBC so that the failover ends when the error occurs in the last server of ALTERNATE_SERVERS.

<a id="bab6d19fccb24cc9"></a>
##### Workaround

The patch is required.

<a id="9c8954d0a3899a27"></a>
#### <kbd>ISSUE-4354</kbd> When the signal is periodically generated by creating POSIX timer, then login timeout and connection timeout are not normally operated in ODBC.

<a id="e936d445fb7e2d8e"></a>
##### Description

When the signal is periodically generated by creating POSIX timer, then login timeout and connection timeout are not normally operated in ODBC.

<a id="fd632a5546740026"></a>
##### Symptom

If the signal is periodically received from POSIX timer while waiting as long as the timeout set through SQL_ATTR_LOGIN_TIMEOUT and SQL_ATTR_CONNECTION_TIMEOUT in ODBC, then it waits longer than the timeout set.

<a id="711b1d4e6e1027e2"></a>
##### Workaround

Do not use POSIX timer while using login timeout and connection timeout.

<a id="73405bf83a32937c"></a>
### 21c.1.8 Patch Notes

<a id="b55896d7be9e368c"></a>
#### <kbd>ISSUE-4348</kbd> Failover is operated when login timeout and connection timeout occur in ODBC environment.

<a id="22e36d388b6d6a94"></a>
##### Description

If timeout occurs when SQL_ATTR_LOGIN_TIMEOUT and SQL_ATTR_CONNECTION_TIMEOUT are set, the failover is not operated in server of alternate_servers.

<a id="cca733d5cd22de11"></a>
##### Symptom

If login timeout and connection timeout occur in ODBC environment, then failover is not operated but it immediately returns an error.

<a id="d6254d6b165771b3"></a>
##### Workaround

The patch is required.

<a id="f54f9b3bda8bb5d5"></a>
#### <kbd>ISSUE-4316</kbd> When executing V$STATEMENT, then intermittently *datatime field overflow* error occurs.

<a id="b1fbdc6b6b64a62c"></a>
##### Description

If a session is dead or terminated while executing V$STATEMENT, then it may import the garbage value. *datatime field overflow* occurs because it reads the garbage value and tries to output it.

<a id="797d9cf4f2c2d3b3"></a>
##### Symptom

When executing V$STATEMENT while executing multiple statement, then intermittently *datatime field overflow* error occurs.

<a id="b8b6f709ae4b8a13"></a>
##### Workaround

Execute it again until the correct value is output.

<a id="4183c7e351f25923"></a>
### 21c.1.7 Patch Notes

<a id="9dfddd171835cac0"></a>
#### <kbd>ISSUE-4327</kbd> When simultaneously executing the restart recovery on multiple members in cluster environment, then it fails to join due to the wrong recovery of *in doubt* transaction.

<a id="f9a6b4fc4da274b2"></a>
##### Description

When the cluster member in cluster environment executes the restart recovery, then it also recovers *in doubt* transaction in PREPARE status. *in doubt* transaction is recovered by requesting the transaction result to other cluster members on MOUNT or above phase, and collecting them, then COMMIT or ROLLBACK them.   
If two members simultaneously recover the same *in doubt* transaction, then the process to set and acquire the transaction status and SCN is not atomic. Therefore, the system SCN is set to the invalid value, and it fails to join.

<a id="2926be60d305da7a"></a>
##### Symptom

The member can not join the cluster database because the system SCN is set to the invalid value.

<a id="83025c83ad3e52b2"></a>
##### Workaround

Drop the cluster member whose SCN is wrong from the cluster, or add a new member.

<a id="5c76c3258695cc38"></a>
### 21c.1.6 Patch Notes

<a id="561fe9a84ccf60f2"></a>
#### <kbd>ISSUE-5678</kbd> If NULL constant is used in any SQL statement used in PSM, then it may access the wrong memory.

<a id="393924102a72da2e"></a>
##### Description

If PSM variable and NULL value are used together in SQL statement within PSM, then it accesses the wrong memory.

<a id="26d824999d35b6ca"></a>
##### Symptom

If the following query is executed, then the server is abnormally terminated.

```
gSQL> DECLARE
        v1 NUMBER := 1;
      BEGIN
        INSERT INTO t1 ( c1, c2, c3, c4 )
         VALUES ( 1, null, null, null );
      END;
      /
```

<a id="c63489a399efb295"></a>
##### Workaround

Do not use NULL and PSM variable together in SQL statement.

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

<a id="519a3795880f6298"></a>
#### <kbd>ISSUE-4286</kbd> If a function argument has an error when executing the function which selects the result by comparing conditions, then it performs the argument even when it is not required, so an error occurs.

<a id="180d13da3bff31af"></a>
##### Description

When executing the function which selects the result by comparing conditions such as CASE2, DECODE, NVL, NVL2, COALESCE, then it selects the result by comparing conditions after executing all function arguments. Therefore, if a function argument has an error, then an error occurs for the argument which is not required to be executed.

<a id="fdeaa2d7991979d9"></a>
##### Symptom

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

<a id="7eba6d86a14309cc"></a>
##### Amendment

If the result is TRUE after comparing the conditions, then it returns the corresponding result, and it does not evaluate any more.

It has been changed to execute the type conversion while preparing when the expression corresponding to the result is a constant number. Therefore, the type conversion error due to the constant  result expression may not occur.  
(Before the amendment, it executed the condition during the execution, and converted the corresponding constant result expression type, then returned it as a result.)

The result type of the following example is number.  
'DEFAULT VALUE', default, is a character which can not be converted to a number, so an error occurs while converting it to the number type. This error occurs while preparing.

```
gSQL>
SELECT DECODE( c1, 0, c1, 'DEFAULT VALUE' ) FROM r WHERE c1 = 0;

ERR-22018(12006): data value is not a numeric literal : 
SELECT DECODE( c1, 0, c1, 'DEFAULT VALUE' ) FROM r WHERE c1 = 0
                          *
ERROR at line 1:
```

<a id="1c826b6554d260df"></a>
##### Additional Information of Result Type

- If the result type is time, time with time zone, timestamp, timestamp with time zone, interval,  
  then it is set to the information including each result expression.  
  (Before the amendment, it was set to the additional information of the first result expression.)

- If the result type is time, time with time zone, timestamp, timestamp with time zone,  
  then the precision is set to the biggest value from each expression.

- If the result type is interval,  
  then, the interval indicator is the combination of each expression's indicator.  
  and the precision and the scale is set to the biggest number from each expression.

<a id="10f9a702e8019cc5"></a>
##### Workaround

Describe it by using CASE statement.

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

<a id="27694e98117e3651"></a>
#### <kbd>ISSUE-4317</kbd> It supports SQL_ATTR_CONNECTION_TIMEOUT property.

<a id="672e7340d145b697"></a>
##### Description

If the network is unstable, then the client can not receive the response and stays in blocking status, after sending a query to the server. Therefore, it supports SQL_ATTR_CONNECTION_TIMEOUT property of SQLSetConnectAttr() to solve this problem.

If SQL_ATTR_CONNECTION_TIMEOUT value is set, then the client sends a query to the server and waits for the response as long as the set time. If it can not get the response for the set time, then the client cuts the connection to the server and returns *HYT01 Connection timeout expired* error.

<a id="344eef3d796e02a3"></a>
##### Symptom

If the network is unstable, then the client waits for the set time after requesting the response to the server.

<a id="a2e14f44ae600a51"></a>
##### Workaround

Alter the kernel property value as follows, so that it can quickly detects whether the connection between the client and the server has an error.

```
net.ipv4.tcp_keepalive_time = 3
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.tcp_keepalive_intvl = 3
net.ipv4.tcp_retries2 = 5
```

<a id="4a1c1da5052bfc4f"></a>
#### <kbd>ISSUE-4031</kbd> The column name of the table is not properly displayed in .Net Framework.

<a id="e3e4d678f0bc08e1"></a>
##### Description

When querying the column name in SQLColAttribute() and SQLGetDescField(), SQL_DESC_LABEL property, SQL_DESC_NAME property or SQL_DESC_BASE_COLUMN_NAME property is used. SQL_DESC_LABEL returns the label, when the column has a label. SQL_DESC_NAME returns an alias when the column has an alias. And, SQL_DESC_BASE_COLUMN_NAME returns the column name.

.Net Framework, data provider for ODBC, uses SQL_DESC_NAME when querying the column name, and the column name is unintentionally retrieved when the label is given to the column. Therefore, DOT_NET_FOR_ODBC, the connection property, has been added for Net Framework to solve this problem.

<a id="5b4490a42e8399d7"></a>
##### Symptom

If executing the following query in gsql, then the column name is retrieved as follows.

```
gSQL> SELECT I1, I1 + I1, I1 AS C1 FROM TEST;

I1 I1 + I1 C1
-- ------- --
 1       2  1
```

If executing the query above in .Net Framework, data provider for ODBC, then the query result is as follows.

```
SELECT I1, I1 + I1, I1 AS C1 FROM TEST;
I1 NULL C1
-- ---- --
 1    2  1
```

<a id="0d17c8b2016cfb18"></a>
##### Workaround

The patch is required.

<a id="43897cc681f6d7c1"></a>
#### <kbd>ISSUE-4302</kbd> When committing the transaction in cluster environment, then the commit server is abnormally terminated.

<a id="b2c9b8bff5874e84"></a>
##### Description

If committing the transaction which updated many tables in cluster environment, then the commit server is abnormally terminated and fails to restart.

<a id="36819e7fbc1f79b5"></a>
##### Symptom

If committing the transaction in cluster environment, then the table SCN is set for the tables updated by the transaction and they are logged. If a single transaction updates 500 or more tables, then the buffer size used for the logging is insufficient, so the commit server is abnormally terminated. Also, the logging is not properly performed so it fails to restart.

<a id="a77b1e517b793b28"></a>
##### Workaround

The patch is required.

<a id="4f9d0259328c1232"></a>
#### <kbd>ISSUE-4308</kbd> When executing the hierarchy query including the sub table which does not specify the view name, then the result is wrong.

<a id="54b9eeff86936c68"></a>
##### Description

When executing the hierarchy query including the sub table which does not specify the view name, then the result is wrong.

<a id="88d64b7e984044cd"></a>
##### Symptom

```
--# Normal situation
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

<a id="970537b8649e20ad"></a>
##### Workaround

Specify the view name in the sub table.

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

<a id="75e5732132dcd827"></a>
#### <kbd>ISSUE-4244</kbd> When creating a package and executing it, then *invalid package object status* error occurs.

<a id="ff6e8127a8bf5ff9"></a>
##### Description

If creating a package and executing it, then *invalid package object status* error occurs.

<a id="ccb841ae02375746"></a>
##### Symptom

If executing the package for the first time after creating it, then *invalid package object status* error occurs as follows.

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

<a id="aa0a86d495454d0f"></a>
##### Workaround

The patch is required.

<a id="831c09c4bc1b025f"></a>
#### <kbd>ISSUE-4156</kbd> The structure of gloader binary mode has been modified.

<a id="5bae21dc29c22e62"></a>
##### Description

The structure of gloader binary mode has been improved. Accordingly, the binary file structure has been changed, so it is not compatible with the previous version binary file.

<a id="ef1f07a92ac80bd8"></a>
##### Symptom

N/A

<a id="5eb179cd7d91b1ef"></a>
##### Workaround

The patch is required.

<a id="98365b5cb9a92ab2"></a>
#### <kbd>ISSUE-4263</kbd> *Split shard* fails after executing *merge shard* on the sharded table.

<a id="9ef9b6f374a6dd1d"></a>
##### Description

Split fails when executing *split shard* after executing *merge shard* on the sharded table because the shard id being used in the table is allocated to the new shard. It happens because an error occurs when acquiring a new shard id while executing *split shard*.

<a id="d3a4fb623121efcc"></a>
##### Symptom

When executing *split shard* after executing *merge shard* on the sharded table, then it fails as follows.

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

<a id="29d77554e229ff3e"></a>
##### Workaround

The patch is required.

<a id="5fd76bc147610940"></a>
#### <kbd>ISSUE-4247</kbd> It supports autocommit option in the precompiler gpec.

<a id="6763b25535a271e3"></a>
##### Description

It supports autocommit as gpec option. If autocommit option of gpec is given, then all connections in gc file is executed with AUTO COMMIT ON.

<a id="aa442ecffc987533"></a>
##### Symptom

N/A

<a id="5d5212636729837e"></a>
##### Workaround

The patch is required.

<a id="9c6479161d3af4fc"></a>
#### <kbd>ISSUE-3825</kbd> It supports blob class and clob class in JDBC.

<a id="8f20aa91c50114ef"></a>
##### Description

It supports blob class and clob class in JDBC.

<a id="1811533dc1256529"></a>
##### Symptom

N/A

<a id="da1ba01523f481d8"></a>
##### Workaround

The patch is required.

<a id="123115a751dde86e"></a>
#### <kbd>ISSUE-4261</kbd> When creating the specific data file, then a validation error occurs.

<a id="64204185d03a7957"></a>
##### Description

If setting the data file size to a specific value when creating a tablespace or adding data file, then the session is abnormally terminated. It occurs due to the validation error for a specific data file size.

<a id="334f6a11f4a21bcb"></a>
##### Symptom

If setting the data file size to a specific value when creating a tablespace, then the session is abnormally terminated as follows.

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

<a id="5918bcfe307fb122"></a>
##### Workaround

Set the data file size to be created to another value.

<a id="75c3ebaad604b683"></a>
#### <kbd>ISSUE-4254</kbd> When executing a subquery containing DISTINCT in the cluster system, then a syntax error occurs in the remote server.

<a id="1a4fdaf204b704e9"></a>
##### Description

If configuring a cluster query by using the query and executing it when the subquery containing DISTINCT is described and the subquery target which is not referenced exists in the cluster system, then a syntax error occurs in the remote server.  
It is because the number of target expressions in the created cluster query and that of view column names do not match.

<a id="8edad4be7b9be245"></a>
##### Symptom

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

<a id="0f527dc53f3a1908"></a>
##### Workaround

Convert DISTINCT statement into GROUP BY statement.

If GROUP BY is not described within the query in which DISTINCT is described, then define all DISTINCT targets by using GROUP BY and omit DISTINCT.

```
gSQL> SELECT v1.i1 FROM ( SELECT i1, i2 FROM t1 GROUP BY i1, i2 ) v1;

no rows selected.
```

<a id="8736688d03382f39"></a>
#### <kbd>ISSUE-4246</kbd> When using AT clause in EXEC SQL AUTOCOMMIT statement, then an error occurs.

<a id="2590a5d898ef21c5"></a>
##### Description

AT clause is not recognizable in *EXEC SQL AT :db_name AUTOCOMMIT* statement, so *INVALID HANDLE* error occurs.

<a id="8cec1190eec3e4b5"></a>
##### Symptom

An error occurs in the following syntax.

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

<a id="f8a3b07c39d92656"></a>
##### Workaround

The patch is required.

<a id="60506e9f2095a8bf"></a>
### 21c.1.5 Patch Notes

<a id="47d541017fcd3000"></a>
#### <kbd>ISSUE-4234</kbd> When performing PSM DDL after ADD MEMBER, then a dictionary integrity constraint violation occurs for the ROUTINE primary key.

<a id="9ea2b93d184f5261"></a>
##### Description

When performing PSM DDL after ADD MEMBER, then a dictionary integrity constraint violation occurs for the ROUTINE primary key, and this error has been fixed.

<a id="c4487bfccbb3f754"></a>
##### Symptom

When creating a routine and adding a cluster member then creating a routine again, an error occurs as follows.

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

<a id="351bc3fb18d21d6e"></a>
##### Workaround

The patch is required.

<a id="bc02c67d267be287"></a>
#### <kbd>ISSUE-4215</kbd> If the variable of using clause in EXECUTE IMMEDIATE is IN OUT type, then an error occurs.

<a id="9f4bfa5e46257093"></a>
##### Description

If the variable bind type of using clause in EXECUTE IMMEDIATE is IN OUT type, then an error occurs.

<a id="b4fa77dc6f7a4a82"></a>
##### Symptom

An error occurs as follows.

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

<a id="ec30b3e7c4c976e6"></a>
##### Workaround

The patch is required.

<a id="2adbbe061c495eee"></a>
### 21c.1.4 Patch Notes

<a id="b1069a2f52fbde1e"></a>
#### <kbd>ISSUE-4207</kbd> When retrieving the records which use rowid, then an error occurs.

<a id="3fb4414575bfbf20"></a>
##### Description

If retrieving the records which use rowid after restarting the system when using the memory tablespace with the data file bigger than 4 GB, then an error occurs. It is because the calculation for the total number of pages is wrong when restarting the system, and this error has been fixed.

<a id="481c9ae7a7359d8c"></a>
##### Symptom

If retrieving the records which use rowid after restarting the system as follows, then an error occurs.

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

<a id="c001a15a88d39612"></a>
##### Workaround

The patch is required.

<a id="ace10b7f9e944fdd"></a>
### 21c.1.3 Patch Notes

<a id="52acdbc7bb9c81e1"></a>
#### <kbd>ISSUE-4189</kbd> If creating the procedure whose parameter is consisted in an order of ref cursor, DB type, and executing it, then an error occurs.

<a id="9fbbf262898932ce"></a>
##### Description

If creating the procedure whose parameter is consisted in an order of ref cursor, DB type, and executing it, then an error occurs.

<a id="971dfc55a6e1c51b"></a>
##### Symptom

If a user calls the parameter as follows, then an error occurs.

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

<a id="7768a36eae018ea2"></a>
##### Workaround

Change the order of defining the parameter when declaring the procedure.

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

<a id="d6c5a7bc6605b2df"></a>
#### <kbd>ISSUE-4188</kbd> When *like* operation is convertible to *equal* comparison operation, then the conversion is supported.

<a id="87f9f014d5a068f7"></a>
##### Description

If the pattern of LIKE operation is in literal format without using a wildcard (%) or an underscore (_), then it supports the conversion to *equal* comparison operation.

<a id="ed862ef03eccaa4a"></a>
##### Symptom

LIKE operation which has the same meaning as that of *equal* comparison operation prevents the plan optimization. If LIKE operation is convertible to *equal* comparison operation, then it supports the conversion to *equal* comparison operation.

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

<a id="381b67316d94f6e0"></a>
##### Workaround

Convert LIKE operation to *equal* comparison operation.

<a id="518bfc534135e8f6"></a>
#### <kbd>ISSUE-4190</kbd> If the subquery is unnested by inner join or semi join, then the filter which can be pushed to the left table is pushed down.

<a id="b2664dc99df2b36f"></a>
##### Description

If the subquery is unnested by inner join or semi join, then the right table becomes a subquery and the left table becomes an outer table of the subquery. In this case, the filter which can be pushed to the left table is pushed down.

<a id="af635e511ecef852"></a>
##### Symptom

Before applying the patch, *r_c1 = 1* within the subquery can not be pushed down to the left table *r*, but it remains in the join. Then, it is processed by being linked to the hash instant filter after it is selected as hash join.

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

After applying the patch, *r_c1 = 1* is located in left table *r* which is related to the corresponding filter.

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

<a id="8f6401f7efeecd99"></a>
##### Workaround

The patch is required.

<a id="d4cafc5e9b813ab1"></a>
### 21c.1.2 Patch Notes

<a id="bab5cdccabb42cf2"></a>
#### <kbd>ISSUE-4183</kbd> If the actual parameter of the procedure is a bind parameter, then the wrong information is set.

<a id="0180d8d187c73e4f"></a>
##### Description

If the actual parameter of the procedure is a bind parameter, then the wrong information is set and the server is abnormally terminated.

<a id="f0375a20354b6f76"></a>
##### Symptom

If the actual parameter of the procedure is a bind parameter, then the wrong information is set and the server is abnormally terminated.

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


The server is abnormally terminated.
```

<a id="04087dddc40c4d32"></a>
##### Workaround

The patch is required.

<a id="cbed40919d900772"></a>
#### <kbd>ISSUE-4178</kbd> DBMS_OUTPUT.PUT_LINE() is output twice.

<a id="36ef1838189f9f15"></a>
##### Description

When DBMS_OUTPUT.PUT_LINE() calls a function including an actual parameter, DBMS_OUTPUT.PUT_LINE(), then the contents of the function are output twice.

<a id="522924061aef59d6"></a>
##### Symptom

The function which is an actual parameter is executed twice when executing DBMS_OUTPUT.PUT_LINE, so DBMS_OUTPUT.PUT_LINE() within the function is also executed twice.

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

<a id="7fdf085c0595ca4c"></a>
##### Workaround

The patch is required.

<a id="d0d060f09a096497"></a>
#### <kbd>ISSUE-4171</kbd> When configuring CTE including a bind parameter, then the system is abnormally terminated.

<a id="9ae0e49a59904469"></a>
##### Description

If CTE is not used in the main query after configuring CTE including a bind parameter, then the system is abnormally terminated.

<a id="13a99baccee78934"></a>
##### Symptom

The information about a bind parameter included in the unused CTE is not configured, so the system is abnormally terminated when referring to the information about the bind parameter.

```
CREATE TABLE t1 ( c1 INTEGER );

VAR v1 VARCHAR(10)

--# fatal
WITH w1 AS ( SELECT * FROM t1 WHERE c1 = :v1 )
   , w2 AS ( SELECT * FROM t1 )
SELECT * FROM w2;
```

<a id="67b2175b8583cd50"></a>
##### Workaround

Do not define CTE which will not be used as follows.

```
CREATE TABLE t1 ( c1 INTEGER );

VAR v1 VARCHAR(10)

WITH w2 AS ( SELECT * FROM t1 )
SELECT * FROM w2;
```

<a id="3b47965aaf954754"></a>
#### <kbd>ISSUE-4174</kbd> The performance of when the local caches of the global sequence are run out has been improved.

<a id="df5db5cc67a825ce"></a>
##### Description

The performance was severely downgraded when the local cache of the global sequence were run out, and this problem has been solved.

<a id="5251b27fee64aaa0"></a>
##### Symptom

All servers using sequences proceed the operations to secure local caches from the global cache when the local caches are run out. In this case, they try to competitively secure the remote cserver, so it may downgrade the performance severely.

<a id="75f20ad86d1808c1"></a>
##### Workaround

The patch is required.

<a id="8fbd7f6b3c49fb40"></a>
#### <kbd>ISSUE-4182</kbd> When restarting cyfile, the recovery may not be operated normally.

<a id="2290648804b97e82"></a>
##### Description

If stopping and restarting cyfile while multiple transactions are simultaneously being processed, then the recovery may not be operated normally, and this problem has been solved.

<a id="7245119a7a379859"></a>
##### Symptom

If stopping and restarting cyfile while transactions are being processed in multiple sessions, then it causes a trouble because the previously stored transaction is stored again in the data file.

<a id="20b3a4e75909bff3"></a>
##### Workaround

The patch is required.

<a id="7507137862519148"></a>
### 21c.1.1 Patch Notes

<a id="0a1fd6514e682b2d"></a>
#### <kbd>ISSUE-4157</kbd> A syntax error occurs according to the space between *into* and *into parameter* in *select into* statement in PSM.

<a id="db9528f0a1a26b4c"></a>
##### Description

A syntax error occurs when two or more spaces exist between *into* and *into parameter* in *select into* statement in PSM.

<a id="afa1ece11e73e4ac"></a>
##### Symptom

A syntax error occurs when two or more spaces exist between *into* and *into parameter* in *select into* statement in PSM as follows.

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

<a id="fa016fd743bc13ab"></a>
##### Workaround

Set the space between *into* and *into parameter* in *select into* statement in PSM into one space.

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

<a id="93e148734f05584f"></a>
#### <kbd>ISSUE-4143</kbd> The table referencing error occurs in FROM statement of a query including a hierarchy.

<a id="cfd8a733345bf280"></a>
##### Description

An error occurs in FROM statement of a query including a hierarchy when referencing the table defined through WITH statement.

<a id="e6164d3919f1bf78"></a>
##### Symptom

If the FROM clause of a query consists of sub tables and the sub tables consist of a query including a hierarchy then a error occurs when referencing Common Table Expression (CTE) defined through WITH statement of a superordinate query within the sub table.

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

<a id="c2f10eeeefe7f6e2"></a>
##### Workaround

The patch is required.

<a id="e576679c1ce8c402"></a>
#### <kbd>ISSUE-4141</kbd> An error occurs when specifying *relation_name.** in the target clause of a query including a hierarchy.

<a id="db0b6bd4a69e36aa"></a>
##### Description

An error occurs when specifying *relation_name.** in the target clause of a query including a hierarchy.

<a id="033d4f8159eb905d"></a>
##### Symptom

The expression corresponding to the relation name can not be found when searching for *asterisk(rel.*)* target which specified the relation in the target clause in a query including a hierarchy.

```
gSQL> SELECT t1.* FROM t1 CONNECT BY LEVEL < 0;

ERR-42000(16036): 'T1': invalid identifier : 
SELECT t1.* FROM t1 CONNECT BY LEVEL < 0
       *
ERROR at line 1:
```

<a id="de39b9a73016452a"></a>
##### Workaround

The patch is required.

<a id="c2d3d697fde93a4a"></a>
#### <kbd>ISSUE-4139</kbd> When the current *with element* references the *with element* which was previously specified in WITH statement, and the referenced *with element* is executed in a materialize method, then it is abnormally terminated.

<a id="21f40e771c94d7e5"></a>
##### Description

When the current *with element* references the *with element* which was previously specified in WITH statement, and the referenced *with element* is executed in a materialize method, then it is abnormally terminated.

<a id="ea5c24839f2d2f7c"></a>
##### Symptom

w1 can not be found in w2, and it is processed wrong, so it is abnormally terminated.

```
WITH
    w1 AS (  SELECT * FROM dual CONNECT BY level < 0  ),
    w2 AS (  SELECT 1 FROM w1 )
SELECT 1 FROM w2, w2;
```

<a id="a3c67201b1df6807"></a>
##### Workaround

Use INLINE hint.

```
WITH
    w1 AS (  SELECT /*+ INLINE */ * FROM dual CONNECT BY level < 0  ),
    w2 AS (  SELECT 1 FROM w1 )
SELECT 1 FROM w2, w2;
```

---

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
