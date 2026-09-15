<a id="c171f73580b90b3a"></a>

# 4. What's New

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/c171f73580b90b3a)  
> Tag: `26c.1_0_tag`

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<a id="392774851783a177"></a>
## Feature Matrix

This chapter briefly describes the features added in each major version.

<a id="de518c19b5f3c2ff"></a>
### Architecture

<a id="627e3ca5072f1fc5"></a>
#### System Architecture

The following is a feature matrix for the system architecture.

**Feature matrix for system architecture**

<a id="e71b2943b3d5607a"></a>
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

<a id="114a5c7a6ae36abf"></a>
#### Storage Internal

The following is a feature matrix for the storage internal.

**Feature matrix for storage internal**

<a id="6cb6e9fcc0e1e0a0"></a>
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

<a id="b82bfbc2bdfd7c28"></a>
#### Transaction Control

The following is a feature matrix for the transaction control.

**Feature matrix for transaction control**

<a id="2c8e9f028813f465"></a>
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

<a id="1c70a4dbf410e00d"></a>
#### Backup & Recovery

The following is a feature matrix for the backup & recovery.

**Feature matrix for backup & recovery**

<a id="5ee87af5f7c00115"></a>
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

<a id="b586517985b57f40"></a>
#### Database Information

<a id="2e93c3e2acc875e9"></a>
##### DICTIONARY_SCHEMA Schema

The following is a feature matrix for the DICTIONARY_SCHEMA schema.

<a id="26f7ee93042b7049"></a>
<table class="table column_count_7"><caption>Feature matrix for DICTIONARY_SCHEMA schema </caption><thead><tr><th class="to_center"><div>Family</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="64"><div>ALL_family Views</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_LIBRARY_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="56"><div>DBA_family Views</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ROLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="62"><div>USER_family Views</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_HISTOGRAM_BALANCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_HISTOGRAM_FREQUENCY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_LIBRARY_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_STAT_COLUMN_GROUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TRIGGERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="28"><div>Other views</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GLOBAL_DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_LIBRARY_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_ROLE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLE_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_ROLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="9432f4d8a4db372d"></a>
##### INFORMATION_SCHEMA Schema

The following is a feature matrix for the INFORMATION_SCHEMA schema.

**Feature matrix for INFORMATION_SCHEMA schema**

<a id="6ba51bccff2d412c"></a>
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

<a id="5256d0e19bac60ec"></a>
##### PERFORMANCE_VIEW_SCHEMA Schema

The following is a feature matrix for the PERFORMANCE_VIEW_SCHEMA schema.

**Feature matrix for PERFORMANCE_VIEW_SCHEMA schema**

<a id="cf9b7e1ae8fa18b1"></a>
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

<a id="3b282c518f7e5e82"></a>
#### Server Property

The following is a feature matrix for the server property.

**Feature matrix for server property**

<a id="460de1fa81eec1c7"></a>
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

<a id="578e12425e1987b4"></a>
#### Property Alias

The following is a feature matrix for the property alias.

**Feature matrix for property alias**

<a id="edadfda2d47da4a4"></a>
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

<a id="6fda704687b2815c"></a>
### SQL

<a id="c46ad9b0c448a51c"></a>
#### SQL Element

<a id="17dd43fb9099d929"></a>
##### Data Type

The following is a feature matrix for the data type.

<a id="5c380766f5eac7c6"></a>
<table class="table column_count_7"><caption>Feature matrix for data type</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>Character string type</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Binary string type</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Decimal number type</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Binary number type</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN type</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Date/ time type</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL type</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ROWID type</div></td><td><div>ROWID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="a2ec5d768703aab1"></a>
##### Function

The following is a feature matrix for the function.

**Feature matrix for function**

<a id="d8b65e51c5c0062a"></a>
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

<a id="ec880f726f49c77c"></a>
#### Object DDL

<a id="415db30374c27fa9"></a>
##### SQL Object DDL

The following is a feature matrix for DDL operations that create, drop, or alter SQL objects.

<a id="bb9a79a273d8bdba"></a>
<table class="table column_count_7"><caption>Feature matrix for SQL object DDL</caption><thead><tr><th class="to_center to_middle"><div>Object</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="13"><div>Database 
object</div></td><td class="to_middle"><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME CHANGE TRACKING FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE REGISTER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESTORE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE SYSTEM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>COMMENT ON object IS ..</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
object</div></td><td class="to_middle"><div>CREATE PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
object</div></td><td class="to_middle"><div>CREATE AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>AUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>NOAUDIT POLICY</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Authorization 
object</div></td><td><div>CREATE ROLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>DROP ROLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GRANT privileges TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>GRANT role TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>REVOKE privileges FROM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>REVOKE role from</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 
object</div></td><td class="to_middle"><div>CREATE SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
object</div></td><td class="to_middle"><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLESPACE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="26"><div>Table 
object</div></td><td class="to_middle"><div>CREATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TRUNCATE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. REORGANIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name SET TRIGGER ORDER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ANALYZE TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>FLASHBACK TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PURGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
object</div></td><td class="to_middle"><div>CREATE VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER VIEW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>Index 
object</div></td><td class="to_middle"><div>CREATE INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. AGING</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. STORAGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. RENAME</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER INDEX .. COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. ENABLE/DISABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
object</div></td><td class="to_middle"><div>CREATE SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SEQUENCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
object</div></td><td class="to_middle"><div>CREATE SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PUBLIC SYNONYM</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
object</div></td><td class="to_middle"><div>CREATE PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PROCEDURE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
object</div></td><td class="to_middle"><div>CREATE FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER FUNCTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package 
object</div></td><td class="to_middle"><div>CREATE PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE PACKAGE BODY</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP PACKAGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td rowspan="2"><div>Library
object</div></td><td><div>CREATE LIBRARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP LIBRARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Trigger
object</div></td><td><div>CREATE TRIGGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TRIGGER name COMPILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TRIGGER name ENABLE/DISABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TRIGGER name RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TRIGGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="03c184476a513894"></a>
##### Cluster Object DDL

The following is a feature matrix for DDL operations that create, drop, or alter cluster objects.

<a id="6a4e6511d6014e5e"></a>
<table class="table column_count_7"><caption>Feature matrix for cluster object DDL </caption><thead><tr><th class="to_center to_middle"><div>Object</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="6"><div>Cluster system 
object</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP UNUSABLE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
object</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
object</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
object</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Cluster table and shard object</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP OFFLINE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP UNUSABLE SEGMENTS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name OFFLINE INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SYNCHRONIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Global secondary index object</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX AGING</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX COALESCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="63edb0728825db78"></a>
#### SQL Language

<a id="84870a2730b58eb3"></a>
##### DML

The following is a feature matrix for DML operations that manipulate data.

**Feature matrix for DML**

<a id="9ca051e44d99a8f3"></a>
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

<a id="3965bcf04d5e7c1f"></a>
##### Query

The following is a feature matrix for the SELECT statement, which queries data.

**Feature matrix for SELECT**

<a id="c64dde4851d7fd9d"></a>
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

<a id="e1db5ad4d0d091f7"></a>
##### Control Language

The following is a feature matrix for the control statement.

<a id="de222d890a374734"></a>
<table class="table column_count_7"><caption>Feature matrix for control statement</caption><thead><tr><th class="to_center to_middle"><div>Control statement</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_middle"><div>22c.1</div></th><th class="to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Session</div></td><td><div>SET ROLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CANCEL SESSION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM FLUSH LOGS</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="6a3163870461a73c"></a>
#### PSM Language

The following is a feature matrix for the Persistent Stored Module (PSM) language element.

**Feature matrix for Persistent Stored Module (PSM) language element**

<a id="968eb141337d170a"></a>
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

The following is a feature matrix for the Built-In Package.

<a id="b70328ac739c61d6"></a>
<table class="table column_count_7"><caption>Feature matrix for Built-in Package</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="d8bb72ee77f6671a"></a>
### API

<a id="2f92e8233f1b0115"></a>
#### ODBC

The following is a feature matrix for the ODBC standard API.

**Feature matrix for ODBC standard API**

<a id="634fbd1b211aa007"></a>
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

The following is a feature matrix for APIs other than the ODBC standard API.

**Feature matrix for API other than ODBC standard**

<a id="116b72e8c6c82748"></a>
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

<a id="bd5759549934bcf1"></a>
#### JDBC

The following is a class feature matrix for JDBC.

**Class feature matrix for JDBC**

<a id="7b269dba1231ac6e"></a>
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

<a id="1144a55fefbe21fd"></a>
#### Embedded SQL

<a id="9507ca45e56738b8"></a>
##### Precompiler Option

The following is a feature matrix for precompiler options.

**Feature matrix for precompiler option**

<a id="2103d28410dd1a5c"></a>
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

<a id="18bc15c96f35a7f0"></a>
##### Embedded SQL-only Syntax

The following is a feature matrix for embedded SQL-only syntax.

**Feature matrix for embedded SQL-only syntax**

<a id="bc50200d338a0e17"></a>
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

<a id="e9b274ca4c28c30c"></a>
##### Host Variable Data Type

The following is a feature matrix for embedded SQL data types used for HOST variables.

**Feature matrix for host variable data type**

<a id="e1af9649b1f2c0df"></a>
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

<a id="49db72dc41bd7a06"></a>
##### Dynamic SQL

The following is a feature matrix for dynamic SQL features.

**Feature matrix for dynamic SQL**

<a id="17e4d0c18991fec4"></a>
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

<a id="c08559537955f8be"></a>
#### PyDBC

<a id="1fbad70a356fb7cf"></a>
##### Module

The following is a method feature matrix for pygoldilocks, provided by PyDBC.

**Feature matrix for pygoldilock method**

<a id="b00a3c8e7b833037"></a>
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

The following is an attribute feature matrix for the pygoldilocks module.

**Feature matrix for pygoldilock attribute**

<a id="2a16c4e8d684e569"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| apilevel | O | O | O | O | O |
| threadsafety | O | O | O | O | O |
| paramstyle | O | O | O | O | O |
| version | O | O | O | O | O |
| lowercase | O | O | O | O | O |

<a id="8733a4b03ac962e9"></a>
##### Connection

The following is a method feature matrix for the connection object.

**Feature matrix for connection method**

<a id="5477e5562ffce523"></a>
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
| clear_output_converter | X | X | X | X | O |
| setencoding | X | X | X | X | O |
| setdecoding | X | X | X | X | O |
| __enter__ | X | X | X | X | O |
| __exit__ | X | X | X | X | O |

The following is an attribute feature matrix for the connection object.

**Feature matrix for connection attribute**

<a id="74be1a8a85d4d3e2"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| autocommit | O | O | O | O | O |
| closed | X | X | X | X | O |
| maxwrite | X | X | X | X | O |
| messages | X | X | X | X | O |
| searchescape | O | O | O | O | O |
| timeout | O | O | O | O | O |

<a id="bb3fdbef7863de9e"></a>
##### Cursor

The following is a method feature matrix for the cursor object.

**Feature matrix for cursor method**

<a id="b38d3c9e61d3fd9b"></a>
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

The following is an attribute feature matrix for the cursor object.

**Feature matrix for cursor attribute**

<a id="9000957e4c199e1e"></a>
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

<a id="e0754bc3821de341"></a>
##### Row

The following is an attribute feature matrix for the row object.

**Feature matrix for row attribute**

<a id="f26b70c4a57dc9dd"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor_description | O | O | O | O | O |

<a id="7d2f37d4721e4832"></a>
### Utility

<a id="281401a3e377ecc0"></a>
#### gcreatedb

<a id="20784c9d4908089e"></a>
##### Command Usage

The following is a feature matrix for the command usage of gcreatedb.

**Feature matrix for command usage of gcreatedb**

<a id="6ccb35128f04ca0e"></a>
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

<a id="c58af56fdc68946e"></a>
#### glsnr

<a id="702e7fef18d13815"></a>
##### Command Usage

The following is a feature matrix for the command usage of glsnr.

**Feature matrix for command usage of glsnr**

<a id="aff9bc92c6a5d1e7"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | O | O | O | O | O |
| --home | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --start | O | O | O | O | O |
| --status | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="c29115915c4cc374"></a>
##### Configuration File

The following is a feature matrix for the configuration of glsnr.

**Feature matrix for configuration of glsnr**

<a id="b266c4868163e372"></a>
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

<a id="f8eb0dc74dfbfeb2"></a>
#### gsql/ gsqlnet

<a id="7deb92ac8b4b8889"></a>
##### Command Usage

The following is a feature matrix for the command usage of gsql.

**Feature matrix for command usage of gsql**

<a id="23d86e55dcd33f6b"></a>
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

<a id="9fd851877c18ba78"></a>
##### Interactive gsql Command

The following is a feature matrix for the interactive gsql commands used in the gsql prompt state.

**Feature matrix for interactive gsql command**

<a id="a03653eecf0ef47b"></a>
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

<a id="f0972ae357cb4380"></a>
#### gloader/ gloadernet

<a id="65f4d799217ef2d1"></a>
##### Command Usage

The following is a feature matrix for the command usage of gloader.

**Feature matrix for command usage of gloader**

<a id="14cef11ddd165458"></a>
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

<a id="58655aa15ec800ea"></a>
##### Control File Syntax

The following is a feature matrix for the control file syntax of gloader.

**Feature matrix for control file syntax of gloader**

<a id="a17ef2ed94d58b77"></a>
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

<a id="e8e2e53f1ead3be0"></a>
#### gdump

<a id="70ea01b1c194382e"></a>
##### Command Usage

The following is a feature matrix for the command usage of gdump.

<a id="c2fc9624db971e7c"></a>
<table class="table column_count_7"><caption>Feature matrix for command usage of gdump</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CHANGE_TRACK</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCATION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REDO_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="7891ac888f662ff8"></a>
#### tablediff

<a id="7a69ea15fd6f92fb"></a>
##### Configuration File

The following is a feature matrix for the configuration file of tablediff.

<a id="d9cedbc6ff915a40"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of tablediff</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td class="to_middle"><div>SOURCE_PASSWORD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_URL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td class="to_middle"><div>TARGET_PASSWORD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_SCHEMA</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_URL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_USER</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td class="to_middle"><div>TARGET_INSERT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_UPDATE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_DELETE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_INSERT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td class="to_middle"><div>DIFF_BIN_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DIFF_OUT_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_CALL_STACK</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_ROW_UNIT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>EXCLUDE_COLUMNS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_DIFF</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_SUCCESS</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_QUEUE_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_THREAD</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_UNIT_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PARTITION_RANGE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SYNC_OUT_FILE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>WHERE_CLAUSE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="d772fa6b7e7a8376"></a>
#### gsyncher

<a id="ec6ee190b92cda3b"></a>
##### Command Usage

The following is a feature matrix for the command usage of gsyncher.

**Feature matrix for command usage of gsyncher**

<a id="9580a8c1f4acdd17"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --log | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --home | O | O | O | O | O |
| --copy-right | O | O | O | O | O |
| --backup-path | O | O | O | O | O |
| --help | O | O | O | O | O |

<a id="9837d5f4b4ff46ec"></a>
#### gmon

<a id="d334db38387aa2ad"></a>
##### Command Usage

The following is a feature matrix for the command usage of gmon.

**Feature matrix for command usage of gmon**

<a id="f5f8cb89e335db2a"></a>
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

<a id="9b545ef0ebc197ff"></a>
#### gtrclogger

<a id="6b4a7cb9df6ac3b9"></a>
##### Command Usage

The following is a feature matrix for the command usage of gtrclogger.

**Feature matrix for command usage of gtrclogger**

<a id="3ef38fb9de2d1e4f"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --dir | O | O | O | O | O |
| --help | O | O | O | O | O |
| --port | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |

<a id="1f4e0e8f2e802a15"></a>
#### glocator

<a id="a1f23077441a529b"></a>
##### Command Usage

The following is a feature matrix for the command usage of glocator.

**Feature matrix for command usage of glocator**

<a id="bf538f1c495628ad"></a>
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

<a id="13f696a80406eace"></a>
##### Configuration File

The following is a feature matrix for the configuration file of glocator.

**Feature matrix for configuration file of glocator**

<a id="8069e4f37a612989"></a>
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

<a id="6a14cd77adf3a738"></a>
#### gagent

<a id="f69af07d12bf62ef"></a>
##### Command Usage

The following is a feature matrix for the command usage of gagent.

**Feature matrix for command usage of gagent**

<a id="6540c59022a3f774"></a>
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

<a id="f9af2b3ab37e1e06"></a>
##### Configuration File

The following is a feature matrix for the configuration file of gagent.

**Feature matrix for configuration file of gagent**

<a id="da2fd83fd60cd807"></a>
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

<a id="7c663becc4a60b21"></a>
#### gloctl

<a id="3113ad80a3f5f9d6"></a>
##### Command Usage

The following is a feature matrix for the command usage of gloctl.

**Feature matrix for command usage of gloctl**

<a id="8cfe566fa1438929"></a>
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

<a id="0b061951412cdb1b"></a>
##### Configuration File

The following is a feature matrix for the configuration file of gloctl.

**Feature matrix for configuration file of gloctl**

<a id="7ad5929da6d0ae59"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | O | O | O | O | O |
| LOCATOR_HOST | O | O | O | O | O |
| LOCATOR_PORT | O | O | O | O | O |

<a id="aa18ff9c7c0b12c6"></a>
### Replication

<a id="7b0fe3f06bd25920"></a>
#### cyclone

<a id="b42bf7734c646f95"></a>
##### Command Usage

The following is a feature matrix for the command usage of cyclone.

**Feature matrix for command usage of cyclone**

<a id="8a16e01e32ddeb9e"></a>
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

<a id="df3ae2726ea34386"></a>
##### Configuration File

The following is a feature matrix for the configuration file of cyclone.

<a id="e2e60b533168c2dc"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of cyclone</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center to_middle"><div>3.x</div></th><th class="to_center to_middle"><div>20c.1</div></th><th class="to_center to_middle"><div>21c.1</div></th><th class="to_center to_middle"><div>22c.1</div></th><th class="to_center to_middle"><div>26c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="13"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>HEARTBEAT_TIMEOUT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRACE_LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="17"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SKIP_COMMENT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_FORCE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PACKET_COMPRESSION_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_MYSQL_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_DB2_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_TIBERO_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="16"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>UPDATE_APPLY_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DB2_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MYSQL_DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIBERO_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLIER_DEADLOCK_PRIORITY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLIER_TRACE_LOG_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4c00cf58d770e699"></a>
#### clustone

Clustone is deprecated.

<a id="4668710b925e04ff"></a>
#### logmirror

<a id="cec5bb9c60a5a710"></a>
##### Command Usage

The following is a feature matrix for the command usage of logmirror.

**Feature matrix for command usage of logmirror**

<a id="de0f1fe938a6d73d"></a>
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

<a id="86eac42fee29b53f"></a>
##### Configuration File

The following is a feature matrix for the configuration file of logmirror.

<a id="f26dd2c7ea5220b1"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of logmirror</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>3.x</div></th><th class="to_center"><div>20c.1</div></th><th class="to_center"><div>21c.1</div></th><th class="to_center"><div>22c.1</div></th><th class="to_center"><div>26c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="1e95b69b7916a5d8"></a>
#### cymon

<a id="c212ccf3792ed65f"></a>
##### Command Usage

The following is a feature matrix for the command usage of cymon.

**Feature matrix for command usage of cymon**

<a id="ff3e2cb2ac083b33"></a>
| Feature | 3.x | 20c.1 | 21c.1 | 22c.1 | 26c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | O | O | O | O | O |
| --help | O | O | O | O | O |
| --cycle | O | O | O | O | O |
| --key | O | O | O | O | O |
| --start | O | O | O | O | O |
| --stop | O | O | O | O | O |
| --status | O | O | O | O | O |

<a id="6f78316219bd73fe"></a>
#### cyfile

<a id="23587f4d477884d4"></a>
##### Command Usage

The following is a feature matrix for the command usage of cyfile.

**Feature matrix for command usage of cyfile**

<a id="a52957cd2dcfaf4e"></a>
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

<a id="70d178797a3a921b"></a>
##### Configuration File

The following is a feature matrix for the configuration file of cyfile.

**Feature matrix for configuration file of cyfile**

<a id="a3fb0696ba1fd287"></a>
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

<a id="44fddc936267fae6"></a>
## What's New in GOLDILOCKS 26c.1

This chapter briefly describes the features added to the GOLDILOCKS 26c.1.

<a id="d47fb8fbd0b68952"></a>
### Architecture

<a id="f65be420f9e3546a"></a>
#### System Architecture

The release platform no longer supports the following platforms.

- HP
- AIX
- PPC64

<a id="2d9cf75eb501f3ad"></a>
#### Storage Internal

It has not been changed.

<a id="952bf1585c178130"></a>
#### Transaction Control

Among the transaction ISOLATION LEVELs, SERIALIZABLE is no longer supported in the cluster system.

<a id="bfea85a34b00a98c"></a>
#### Backup & Recovery

[Parallel recovery feature](../part-03-sql-manual/18-sql-references-a-b.md#91d87d0b29aa6323) has been added for the parallel recovery.

[Parallel backup feature](../part-03-sql-manual/18-sql-references-a-b.md#a9f4f713f7a7547c) has been added for the parallel backup.

[Parallel restore feature](../part-03-sql-manual/18-sql-references-a-b.md#22625d6afdeafdcd) has been added for the parallel recovery.

<a id="c8928c43b6b6d7ed"></a>
#### Database Information

<a id="6b5ca5869f3bab2b"></a>
##### DICTIONARY_SCHEMA

The following views have been added to retrieve information about roles.

- [DBA_ROLES](../part-02-administration-manual/9-database-information.md#d223e919e7d8cbcf)
- [DBA_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#790f7bf74bbe0612)
- [USER_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#eb598e0f61d3dc2b)
- [ROLE_COL_PRIVS](../part-02-administration-manual/9-database-information.md#0362c8010b744207)
- [ROLE_DB_PRIVS](../part-02-administration-manual/9-database-information.md#a1d32196ef920b4f)
- [ROLE_PACKAGE_PRIVS](../part-02-administration-manual/9-database-information.md#cd4eddbf83f55151)
- [ROLE_PROC_PRIVS](../part-02-administration-manual/9-database-information.md#9505f2f174b6e0d0)
- [ROLE_ROLE_PRIVS](../part-02-administration-manual/9-database-information.md#c3ddbd7adbe9b3ea)
- [ROLE_SCHEMA_PRIVS](../part-02-administration-manual/9-database-information.md#3c1f5a47990be7b1)
- [ROLE_SEQ_PRIVS](../part-02-administration-manual/9-database-information.md#c3557b04b47eaff3)
- [ROLE_SYS_PRIVS](../part-02-administration-manual/9-database-information.md#a876f799f390957e)
- [ROLE_TAB_PRIVS](../part-02-administration-manual/9-database-information.md#53b9c7ced9db0caf)
- [ROLE_TBS_PRIVS](../part-02-administration-manual/9-database-information.md#d26050d8f4171f56)
- [SESSION_ROLES](../part-02-administration-manual/9-database-information.md#584f1238757a5f38)

The following views have been added to retrieve information about histograms.

- [ALL_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#599e0d6590c85740)
- [ALL_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#253929e92938a31f)
- [DBA_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#2ab9de6d2cf9a0ef)
- [DBA_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#6b8ef0c50e621009)
- [USER_HISTOGRAM_BALANCE](../part-02-administration-manual/9-database-information.md#3bf211ff1d446705)
- [USER_HISTOGRAM_FREQUENCY](../part-02-administration-manual/9-database-information.md#5f6bd4931f585e44)

The following views have been added to retrieve information about library objects.

- [ALL_LIBRARIES](../part-02-administration-manual/9-database-information.md#155ee201f004fd92)
- [ALL_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#51bd1783fca5e8d1)
- [ALL_LIBRARY_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#438923e9ade5fcc1)
- [ALL_LIBRARY_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#fc08a0b4384723e1)
- [DBA_LIBRARIES](../part-02-administration-manual/9-database-information.md#952804c1df5a1b29)
- [DBA_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#b67b02fbd2dcd918)
- [USER_LIBRARIES](../part-02-administration-manual/9-database-information.md#8b61cb11ed095a87)
- [USER_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#5bef86cea07012c8)
- [USER_LIBRARY_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#a308e3b0cae17696)
- [USER_LIBRARY_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#ac47c929c0c2cbbe)
- [ROLL_LIBRARY_PRIVS](../part-02-administration-manual/9-database-information.md#41069f302b0a4e68)

The following views have been added to retrieve information about trigger objects.

- [ALL_TRIGGERS](../part-02-administration-manual/9-database-information.md#4789e39e2071e756)
- [DBA_TRIGGERS](../part-02-administration-manual/9-database-information.md#8b012ad1752dc3f6)
- [USER_TRIGGERS](../part-02-administration-manual/9-database-information.md#125a83ede339f5ba)

<a id="ce1342b28aeb7120"></a>
##### INFORMATION_SCHEMA

The following views have been added to retrieve information about roles.

- [ADMINISTRABLE_ROLE_AUTHORIZATIONS](../part-02-administration-manual/9-database-information.md#8e7583d4353310e1)
- [APPLICABLE_ROLES](../part-02-administration-manual/9-database-information.md#d335d5c98369d448)
- [ENABLED_ROLES](../part-02-administration-manual/9-database-information.md#a26bb75effecff09)
- [ROLE_COLUMN_GRANTS](../part-02-administration-manual/9-database-information.md#beca865ea413d618)
- [ROLE_MODULE_GRANTS](../part-02-administration-manual/9-database-information.md#48e5d9bffc63ac2b)
- [ROLE_ROUTINE_GRANTS](../part-02-administration-manual/9-database-information.md#69764f4d3d345f79)
- [ROLE_TABLE_GRANTS](../part-02-administration-manual/9-database-information.md#f5c1974d7cb98709)
- [ROLE_USAGE_GRANTS](../part-02-administration-manual/9-database-information.md#e5bffa6ba85b297c)

[CHECK_CONSTRAINTS](../part-02-administration-manual/9-database-information.md#b1c103e1755d23c3) view has been added to retrieve information about check constraints.

The following views have been added to retrieve information about triggers.

- [TRIGGERED_UPDATE_COLUMNS](../part-02-administration-manual/9-database-information.md#6bbf2cdd5c1ad681)
- [TRIGGERS](../part-02-administration-manual/9-database-information.md#aff8e3dd7e5fce2f)
- [TRIGGER_EVENT_ORDER](../part-02-administration-manual/9-database-information.md#e903929c38dea03d)
- [TRIGGER_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#3885ef4121d7f56d)
- [TRIGGER_ROUTINE_USAGE](../part-02-administration-manual/9-database-information.md#949066dc5b4c1719)
- [TRIGGER_SEQUENCE_USAGE](../part-02-administration-manual/9-database-information.md#464e02e252c3ddd3)
- [TRIGGER_TABLE_USAGE](../part-02-administration-manual/9-database-information.md#f6d01ffe4116af38)

<a id="5251e371f7efc32f"></a>
##### PERFORMANCE_VIEW_SCHEMA

The following views have been added.

- [V$DB_PROPERTY](../part-02-administration-manual/9-database-information.md#5dce0d3509d51946)
- [V$RELATION](../part-02-administration-manual/9-database-information.md#6bfdcd425ad0df84)
- [V$TCL_LOGFILE](../part-02-administration-manual/9-database-information.md#0750dd6eccd6122f)
- [V$ALLOCATOR](../part-02-administration-manual/9-database-information.md#0a5ec09e543f0914)
- [V$CLUSTER_CONNECTION](../part-02-administration-manual/9-database-information.md#0fc3f295559a8e2b)
- [V$CLUSTER_QUEUE](../part-02-administration-manual/9-database-information.md#6ebe93101755846e)
- [V$UNDO_SEGMENT](../part-02-administration-manual/9-database-information.md#992cd8dbb2469a94)

<a id="e9def4062249e4ee"></a>
#### Server Property

The default value of [DEFAULT_INDEX_PCTFREE](../part-02-administration-manual/10-server-property.md#74782b3e0126d31c) has been changed to 10.

Parallel recovery has been added, so the [RECOVERY_SLAVES](../part-02-administration-manual/10-server-property.md#10b2624db09467fe) property also has been added to control the degree of parallelism.

The default value of [DEFAULT_MAXTRANS](../part-02-administration-manual/10-server-property.md#c44fafa3bbc35d7b) has been changed to 32.

New properties for controlling histogram bucket numbers during ANALYZE TABLE have been added:  
• [HISTOGRAM_BALANCE_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#72887d9d523d11fa)  
• [HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT](../part-02-administration-manual/10-server-property.md#1fd9a37f61769b96)  
• [HISTOGRAM_FREQUENCY_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#7628241bceaa2159)

The property INCREMENTAL_CHECKPOINT_CRITERIA, which sets the criteria for performing incremental checkpoints, has been renamed to [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#5c88ba27554a8c6b), with its default value changed to 0.

The [BUFFER_LRU_SCAN_PERCENT](../part-02-administration-manual/10-server-property.md#d2822bb6ed31f752) property has been added to improve the buffer management algorithm of disk tablespace.

The CLUSTER_CM_BUFFER_COUNT property, which specified the number of communication buffers in a cluster environment, has been deprecated. Instead, the properties [LOCKABLE_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#54f5ea2ce441327f), [LOCKLESS_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#eb9179b865f989bf), and [SYNC_DISPATCHER_CM_BUFFER_COUNT](../part-02-administration-manual/10-server-property.md#21af781f9dbcb62c) have been added to specify the number of communication buffers for lockable, lockless, and synchronization dispatchers, respectively.

The threshold of table size determines whether tables created in the disk tablespace are cached to the buffer cache during a full scan. The [FULL_TABLE_SCAN_CACHING_THRESHOLD](../part-02-administration-manual/10-server-property.md#bb021e3d6953b2ba) property has been added to set this threshold value.

The [INST_HASH_TABLE_BUCKET_MAX_COUNT](../part-02-administration-manual/10-server-property.md#06aef1f45d49b860) property has been added to set the maximum number of buckets expected for the hash instant table.

The maximum number of SQL that can be cached in the plan cache used to be controlled by two properties. The MAXIMUM_FLANGE_COUNT property was deprecated, so now only the [PLAN_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#47de4d307c34ef0c) property controls the maximum number of SQL that can be cached.

The [PLAN_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#47de4d307c34ef0c) property has been updated. Previously, changes to the PLAN_CACHE_SIZE property required a server restart to take effect.  It has now been updated to apply changes immediately and online, without the need for a restart.

The [V$SQL_CACHE](../part-02-administration-manual/9-database-information.md#19c53ba9251da235) column has been removed from the V$SQL_CACHE view.

The default value of the [AGING_PLAN_INTERVAL](../part-02-administration-manual/10-server-property.md#f172c22d22687c8a) property has been changed from 0 to 3.

The default value of the [SESSION_MEMORY_INIT_SIZE](../part-02-administration-manual/10-server-property.md#375cd950ca0420e6) has been changed from 131,072 to 524,288.

The [GLOBAL_TRANSACTION_LOG_BLOCK_SIZE](../part-02-administration-manual/10-server-property.md#66a67ed16a51a315) property has been added to configure the block size of the global transaction log file.

The [SHARED_SESSION_MEMORY_INIT_SIZE](../part-02-administration-manual/10-server-property.md#450e0fbecfe9e8a7) property has been added to specify the initial memory size of shared sessions.

The [INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD](../part-02-administration-manual/10-server-property.md#58a8930e680eb3f9) property has been added to reduce the space usage of instant indexes.

The constraint that all members in the cluster must have the same [TRANSACTION_TABLE_SIZE](../part-02-administration-manual/10-server-property.md#c44799be03ce68e7) has been removed.

The CLUSTER_DEADLOCK_TIMEOUT property has been deprecated as cluster now detects deadlocks internally without using this property.

When applying replicas in cluster, the async replica mode is now used by default. If async replication cannot be used, it is handled internally, and therefore the CLUSTER_ASYNC_REPLICATION property has also been deprecated.

The default value of [SHARED_MEMORY_STATIC_SIZE](../part-02-administration-manual/10-server-property.md#6bbbc914a0e83be3) has been changed to 800M.

INST_TABLE_BLOCK_SIZE has been renamed to [INST_TABLE_PAGE_SIZE](../part-02-administration-manual/10-server-property.md#b88cb19b3df8ec64).

The [REDO_LOGGING_THROTTLING](../part-02-administration-manual/10-server-property.md#fc97a492acbd2b65) property has been added to control the logging speed during index creation and rebuild operations.

The CLUSTER_COMMIT_STREAM_ISOLATION property has been deprecated as commit-related protocols in cluster have been improved to use a separate dispatcher and queue.

The CONTROL_FILE_TEMP_NAME property has been deprecated as control files are now saved without using temporary files.

The following properties have been renamed.

- [REBALANCE_BLOCK_READ_COUNT](../part-02-administration-manual/10-server-property.md#2a27486980a4c5d5) has been changed to [ONLINE_DDL_BLOCK_READ_COUNT](../part-02-administration-manual/10-server-property.md#01c6d9aec58015c6).
- [REBALANCE_SHARD_DIVISOR](../part-02-administration-manual/10-server-property.md#ff73df2a9aab0ece) has been changed to [ONLINE_DDL_SCAN_PARTITION](../part-02-administration-manual/10-server-property.md#10db0f046d22a3e2).
- [MAXIMUM_JOURNAL_REPLAY_COUNT](../part-02-administration-manual/10-server-property.md#41f664f7c9f0ea59) has been changed to [ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT](../part-02-administration-manual/10-server-property.md#5d8871acc0f7c38f).
- [ONLINE_JOURNAL_REPLAY_THRESHOLD](../part-02-administration-manual/10-server-property.md#d1f0ca9e9460368a) has been changed to [ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD](../part-02-administration-manual/10-server-property.md#6d34d4485d097e76).

The [LOG_FLUSHER_HOT_POLICY_INTERVAL](../part-02-administration-manual/10-server-property.md#87f158ec6117968a) property has been added to control how long the gmaster log flusher thread performs busy waiting for an event.

[ARCHIVE_LOG_THROTTLING](../part-02-administration-manual/10-server-property.md#5d1bcc692e3875ff) property has been added to control disk I/O performance during redo log archiving.

<a id="d682c180ccd4c339"></a>
### SQL

<a id="3bf3ee6bcf4948b1"></a>
#### SQL Element

<a id="f33b44d9d5476242"></a>
##### Data Type

It has not been changed.

<a id="56547e706e6c9e1c"></a>
##### Function

The system information functions [CURRENT_ROLE](../part-03-sql-manual/17-built-in-function-references.md#38ee0469541ddc0f) and [LOCAL_MEMBER_POSITION](../part-03-sql-manual/17-built-in-function-references.md#3e18ea582f6a25fa) have been added.

The built-in functions [GROUPING](../part-03-sql-manual/17-built-in-function-references.md#6618c1617cf70e9a) and [GROUPING_ID](../part-03-sql-manual/17-built-in-function-references.md#fd268ffdd95f2b3b) have been added.

The built-in functions, regular expressions, have been added.

- [REGEXP_COUNT](../part-03-sql-manual/17-built-in-function-references.md#54924611a881f204)
- [REGEXP_INSTR](../part-03-sql-manual/17-built-in-function-references.md#75e1a53f48309d9a)
- [REGEXP_LIKE Condition](../part-03-sql-manual/11-sql-elements.md#f7b851fa4ca3e27d)
- [REGEXP_REPLACE](../part-03-sql-manual/17-built-in-function-references.md#42d99f66190078af)
- [REGEXP_SUBSTR](../part-03-sql-manual/17-built-in-function-references.md#be5a2413d7c8ae27)

The PRETTY option has been added to the [JSON output clause](../part-03-sql-manual/11-sql-elements.md#91fe9ef765ec473f) of the built-in function [JSON String Constructor](../part-03-sql-manual/11-sql-elements.md#5f5005d01175dec7).

A [JSON Key Uniqueness Constraint](../part-03-sql-manual/11-sql-elements.md#2b244b19e881dcb5) option has been added to the built-in functions [JSON_OBJECT](../part-03-sql-manual/17-built-in-function-references.md#fbd9eb4c70306dc1), [JSON_OBJECTAGG](../part-03-sql-manual/17-built-in-function-references.md#61c76e5d901661ed), and [JSON_OBJECTAGG() OVER](../part-03-sql-manual/17-built-in-function-references.md#821bcca33f74cbfd).

A [JSON Array Aggregate Order By Clause](../part-03-sql-manual/11-sql-elements.md#d705909cfd7dce0a) option has been added to the built-in functions [JSON_ARRAYAGG](../part-03-sql-manual/17-built-in-function-references.md#7bc8aa387314ee48) and [JSON_ARRAYAGG() OVER()](../part-03-sql-manual/17-built-in-function-references.md#b3c3b1418c509029).

The approximate aggregation function [APPROX_COUNT_DISTINCT](../part-03-sql-manual/17-built-in-function-references.md#051f809810e5e2aa) has been added to the aggregation function.

The statistics information functions [TABLE_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#77a8c39a1b430f52), [INDEX_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#483bdb639e6046de) and [GSI_PHYSICAL_STATS](../part-03-sql-manual/17-built-in-function-references.md#d60f8977301c682f) have been added.

<a id="af0cd0148e744684"></a>
#### Object DDL

<a id="05924a5037819c55"></a>
##### SQL Object DDL

<a id="0f5bedfebc0f3447"></a>
###### **ROLE**

A DDL statement for roles (authorization objects) has been added.

- Creating ROLE
    - [CREATE ROLE](../part-03-sql-manual/19-sql-references-c-g.md#635504efdc11b072)
- Dropping ROLE
    - [DROP ROLE](../part-03-sql-manual/19-sql-references-c-g.md#9c173c3287657d63)
- Granting ROLE
    - [GRANT role TO](../part-03-sql-manual/19-sql-references-c-g.md#08d2b8947feab7b4)
- Revoking ROLE
    - [REVOKE role FROM](../part-03-sql-manual/20-sql-references-h-z.md#56d94492714e9b12)

<a id="fb4739b4d47681a6"></a>
###### **Building Histogram Information When Performing ANALYZE TABLE**

It can build the following the histogram information when executing the [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#1dbf53dac8b0496f) statement.

- Height-balanced histogram
- Frequency histogram

To build histogram information, the relevant property must be enabled.

- [HISTOGRAM_BALANCE_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#72887d9d523d11fa)
- [HISTOGRAM_FREQUENCY_BUCKET_COUNT](../part-02-administration-manual/10-server-property.md#7628241bceaa2159)

<a id="0fe0f420420d1072"></a>
###### **Adding FOR COLUMN GROUPS Clause to ANALYZE TABLE Statement**

The FOR COLUMN GROUPS clause has been added to the [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#1dbf53dac8b0496f) statement to build statistical information for column groups.

<a id="d0dc79e929653ef8"></a>
###### **Improved Accuracy of ANALYZE Sampling**

The performance and accuracy of ANALYZE sampling have been enhanced by introducing the following techniques:

- Repeatable random sampling
- Approximate NUM_DISTINCT (Hyper log algorithm)
- NUM_DISTINCT adjustment based on an exponential curve

Even at a 10% ANALYZE sampling rate, all 22 TPC-H queries produce execution plans equivalent to those from a full ANALYZE.

<a id="f1c0d33a1ac71d57"></a>
###### **Audit Policy**

The [&lt;role_audit_clause&gt;](../part-03-sql-manual/19-sql-references-c-g.md#6c9f34fc393f06e8) has been added to both the [CREATE AUDIT POLICY](../part-03-sql-manual/19-sql-references-c-g.md#9b9979f490f84f42) statement and [ALTER AUDIT POLICY](../part-03-sql-manual/18-sql-references-a-b.md#1ee1c2c985e74ad3) statements.

<a id="71be6c8bd8a80173"></a>
###### **RENAME CHANGE TRACKING FILE**

The [ALTER DATABASE RENAME CHANGE TRACKING FILE](../part-03-sql-manual/18-sql-references-a-b.md#e844d07cccb4db29) statement has been added.

<a id="d4232e172245b496"></a>
###### **ALTER INDEX COALESCE**

[ALTER INDEX COALESCE](../part-03-sql-manual/18-sql-references-a-b.md#5333ab1d309d9a83) cannot be executed concurrently with other ALTER statements. (This is possible in version 22c.1.)

<a id="1b50933d3caa2f91"></a>
###### **CHECK constraint**

CHECK constraints have been added.

- [CHECK Constraint](../part-03-sql-manual/19-sql-references-c-g.md#acfcee22d5012787)
- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#47f3ce328094503e)
- [ALTER TABLE name ADD COLUMN](../part-03-sql-manual/18-sql-references-a-b.md#a075befc84515f66)
- [ALTER TABLE name ADD CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#35d842d05c006ac4)

<a id="86c16b15231b2f50"></a>
###### **FOREIGN KEY constraint**

FOREIGN KEY constraints have been added.

- [FOREIGN KEY Constraint](../part-03-sql-manual/19-sql-references-c-g.md#5ad53eb3db4e69ec)
- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#47f3ce328094503e)
- [ALTER TABLE name ADD COLUMN](../part-03-sql-manual/18-sql-references-a-b.md#a075befc84515f66)
- [ALTER TABLE name ADD CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#35d842d05c006ac4)

<a id="53e29b1b1d584586"></a>
###### **&lt;constraint enforcement&gt; **

As part of the &lt;constraint enforcement&gt; option, the [ALTER TABLE name ALTER CONSTRAINT](../part-03-sql-manual/18-sql-references-a-b.md#eb62db9bb8f75d76) statement has been added to enable or disable constraints.

<a id="c38798685445649a"></a>
###### **&lt;index enforcement&gt; **

As part of the &lt;index enforcement&gt; feature, the [ALTER INDEX name ENABLE/DISABLE](../part-03-sql-manual/18-sql-references-a-b.md#dbe18eea896189bf) statement has been added to enable or disable indexes.

<a id="8eb9a8647c66dc16"></a>
###### **Removal of ADD CONSTRAINT ON SCHEMA privilege**

The ADD CONSTRAINT ON SCHEMA privilege has been removed.

- ADD CONSTRAINT of the table owner
    - The ALTER ON TABLE privilege is granted when executing CREATE TABLE.
    - ADD CONSTRAINT is executed using the ALTER ON TABLE privilege.
- ADD CONSTRAINT of a non-owner
    - Requires either the ALTER ON TABLE privilege
    - or the ALTER TABLE ON SCHEMA privilege.
- Constraint ownership when executing ADD CONSTRAINT
    - The owner of the table to which the constraint belongs

<a id="a60fe86a60f3fa18"></a>
###### **Removal of PUBLIC from User Schema Path When Executing CREATE USER**

When executing CREATE USER, PUBLIC is now removed from the user's schema path.

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

To maintain the same behavior as in version 22c and earlier, adjust the schema path as shown below.

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

<a id="8a221f9f3c2c4a3a"></a>
###### **ALTER TABLE name SET TRIGGER ORDER**

The [ALTER TABLE name SET TRIGGER ORDER](../part-03-sql-manual/18-sql-references-a-b.md#24a95716d0044b84) statement has been added to change the execution order of triggers created on a table.

<a id="a9c7051fb4871663"></a>
###### **ALTER TABLE name REORGANIZE**

The [ALTER TABLE name REORGANIZE](../part-03-sql-manual/18-sql-references-a-b.md#64d12151db2fcee0) statement has been added to physically reorganize a table.

<a id="8aff5fd58a9a82d1"></a>
###### **&lt;shard divisor&gt; **

The &lt;shard divisor&gt; option used in the online DDL statements has been changed to &lt;scan partition&gt;.

The following are the updated online DDL statements.

- [ALTER DATABASE MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#ddb148eaa7b01843)
- [ALTER DATABASE REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#eba0a85e4ceddd6e)
- [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](../part-03-sql-manual/18-sql-references-a-b.md#06645397a8a0d575)
- [ALTER DATABASE SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#8e0788c3012778c5)
- [ALTER TABLE name MOVE SHARD](../part-03-sql-manual/18-sql-references-a-b.md#b53aef713ebb21be)
- [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#f207258645781242)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](../part-03-sql-manual/18-sql-references-a-b.md#af45593c0739dbf2)
- [ALTER TABLE name SYNCHRONIZE](../part-03-sql-manual/18-sql-references-a-b.md#bc55498003b53106)

<a id="ed7a214da6219177"></a>
###### **Removal of MINSIZE from the STORAGE clause**

The following DDL statements no longer support the use of MINSIZE within the STORAGE clause.

- [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#47f3ce328094503e)
- [CREATE TABLE AS SELECT](../part-03-sql-manual/19-sql-references-c-g.md#13b906a980351a1f)
- [CREATE INDEX](../part-03-sql-manual/19-sql-references-c-g.md#c758c010adf913ce)
- [ALTER INDEX name STORAGE](../part-03-sql-manual/18-sql-references-a-b.md#22d2f0569f8a174c)
- [ALTER INDEX name REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#2c9ae90a7a32ddcf)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#c0be2a6bcfa14f9c)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#0a0bd7ac1ecae05e)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#1e71f92616f9896b)

<a id="238252c9fa3f2290"></a>
###### **Removal of MAXSIZE from the INDEX STORAGE Clause**

The use of MAXSIZE in the STORAGE clause is no longer supported in the following DDL statements.

- [CREATE INDEX](../part-03-sql-manual/19-sql-references-c-g.md#c758c010adf913ce)
- [ALTER INDEX name STORAGE](../part-03-sql-manual/18-sql-references-a-b.md#22d2f0569f8a174c)
- [ALTER INDEX name REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#2c9ae90a7a32ddcf)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#c0be2a6bcfa14f9c)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references-a-b.md#0a0bd7ac1ecae05e)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX REBUILD](../part-03-sql-manual/18-sql-references-a-b.md#1e71f92616f9896b)

<a id="b83b5fd3b3350ec2"></a>
##### Cluster Object DDL

<a id="3f229cbdb3a0edc0"></a>
###### **ALTER TABLE ALTER GLOBAL SECONDARY INDEX COALESCE**

[ALTER TABLE ALTER GLOBAL SECONDARY INDEX COALESCE](../part-03-sql-manual/18-sql-references-a-b.md#91641d53f6bfbfad) cannot be executed concurrently with other ALTER statements. (This is possible in version 22c.1.)

<a id="b5468fafa15e5995"></a>
#### SQL Language

<a id="e9bbb51ff762a501"></a>
##### DML

<a id="a4bef4eb9ea5c045"></a>
###### **MERGE**

The MERGE statement has been added.  
For more information, refer to [MERGE](../part-03-sql-manual/20-sql-references-h-z.md#2ce51d1a09e94307).

<a id="7002861dd59672f2"></a>
###### **APPEND INSERT **

Support for adding data using the APPEND INSERT method and the hint that enables this feature has been added.  
For more information, refer to [Adding Data Using the APPEND INSERT Method](../part-03-sql-manual/12-sql-languages.md#df02d66ddd4d5aa0).

<a id="66515bb378c147de"></a>
###### **&lt;local shard limit&gt; Clause of DELETE FROM**

The &lt;local shard limit clause&gt; has been added to the DELETE FROM statement.  
For more information, refer to [&lt;local shard limit clause&gt;](../part-03-sql-manual/19-sql-references-c-g.md#59f650a785d26d85).

<a id="cd8a6ee3a6b06581"></a>
##### Query

<a id="71ee0680b3ba562a"></a>
###### **Support for extending &lt;grouping element&gt; in the** [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#124ff4a28b194dde)

The ROLLUP, CUBE and GROUPING SET have been added to &lt;grouping element&gt;.  
For more information, refer to [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#124ff4a28b194dde).

<a id="b27ed239312f9010"></a>
###### **Support for referencing select list aliases in the group by clause**

Select list aliases have been added to the &lt;grouping column reference&gt;.  
For more information, refer to [group by clause](../part-03-sql-manual/20-sql-references-h-z.md#124ff4a28b194dde).

<a id="1666eb326891bc68"></a>
###### **Pivot Clause**

A pivot clause has been added to describe a cross table that converts rows into a columns.  
For more information, refer to [pivot clause](../part-03-sql-manual/20-sql-references-h-z.md#4f854e69606a7ccb).

<a id="131b21a3fc8b5314"></a>
###### **Unpivot Clause**

An unpivot clause has been added to describe a cross table that converts columns into rows.   
For more information, refer to [unpivot clause](../part-03-sql-manual/20-sql-references-h-z.md#19bb3872a694c77c).

<a id="ffafe49f1b35ab07"></a>
###### **Sample Clause**

A sample clause has been added to randomly extract only a subset of rows instead of processing the entire data in the table.  
For more information, refer to [sample clause](../part-03-sql-manual/20-sql-references-h-z.md#f11bfbfa622bd200).

<a id="e55d08c3643fbebe"></a>
###### **Aggregation Filter**

A FILTER feature has been added to [Aggregate Function](../part-03-sql-manual/11-sql-elements.md#f67400ca8ab799e1).

A FILTER feature has been added to [JSON aggregate Constructor](../part-03-sql-manual/11-sql-elements.md#8f919c556b771612).

<a id="9baf80013d830096"></a>
###### **Add SQL Hint**

The following SQL hints have been added.

- [&lt;window hints&gt;](../part-03-sql-manual/15-sql-tuning.md#9d38b8f7f285d6f3)
- [&lt; union all driver hints &gt;](../part-03-sql-manual/15-sql-tuning.md#5e6b662bc51f4f88)

<a id="b64a7a4d8be2b2f3"></a>
##### Control Language

The [ALTER SYSTEM CANCEL SESSION](../part-03-sql-manual/18-sql-references-a-b.md#2a0ab5d4f5714813) statement has been added to cancel the operation currently being executed in a session.

<a id="77f5793dca724a54"></a>
###### **SET ROLE**

The [SET ROLE role_name](../part-03-sql-manual/20-sql-references-h-z.md#6150b8d582737fc5) statement has been added to change the role of the current session.

<a id="5dc699e50a203166"></a>
#### PSM Language

<a id="badbcc3a80fb91f2"></a>
##### External Routine

[External Routine](../part-04-sql-psm-manual/28-external-routine.md#2fb71bf0a9a14e30) have been added, allowing you to execute user-written C programs.

<a id="944dbda704f50597"></a>
##### Triggger

A [Trigger](../part-04-sql-psm-manual/29-trigger.md#9e3bdbcf1ed13933) object has been added that allows specific actions to be automatically executed whenever DML operations are performed on a given table.

<a id="63aedd98ae8d9b10"></a>
##### PL Statement

The [Call Specification](../part-04-sql-psm-manual/30-psm-language-element-references.md#f24bb921ad663f66) statement has been added to match external C functions with routine information.

<a id="4ce424627f43c981"></a>
##### Library Object DDL

- [CREATE LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#d3c4a1abc483c544)
- [DROP LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#ac5c19f8f617c881)

<a id="59e7874b3428cf02"></a>
##### Trigger Object DDL

- [CREATE TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#44e30f425949fd8e)
- [DROP TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#c5e9e28a6d05bf8b)
- [ALTER TRIGGER name COMPILE](../part-04-sql-psm-manual/31-psm-sql-references.md#d86df859bc319efc)
- [ALTER TRIGGER name ENABLE/DISABLE](../part-04-sql-psm-manual/31-psm-sql-references.md#87a5b7084ef9f6ba)
- [ALTER TRIGGER name RENAME TO](../part-04-sql-psm-manual/31-psm-sql-references.md#7a2a65b5c770fb59)

<a id="6ae9ce2bbbb8f2c9"></a>
##### Built-in Package

The built-in package SQL has been added so that users can install packages as needed.

Users who used built-in packages in versions 22c or earlier must install the built-in package as shown below.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="c68dab68b9a233c9"></a>
### API

<a id="1a92212b8a592ff3"></a>
#### ODBC

The connection property ALTERNATE_LOCATORS has been changed to ALTERNATE_LOCATOR.

The field configuration of the SQL_LONG_VARIABLE_LENGTH_STRUCT structure has been modified.  
The roles have been separated into buf_len, which represents the capacity of the buffer arr (in bytes), and len, which represents the actual data length (in bytes).  
([Non-standard data type](../part-05-developer-manual/34-odbc.md#fa621b58d9961f03))

<a id="9adc3703c4ff2017"></a>
#### JDBC

The connection property ALTERNATE_LOCATORS has been changed to ALTERNATE_LOCATOR.

The connection property commit_write_mode has been added.

<a id="45a66fc680e99b35"></a>
#### Embedded SQL

<a id="a3483b0f2c8b28ef"></a>
##### Precompiler Option

The [--parse](../part-05-developer-manual/36-embedded-sql.md#24a6678c2ab04fa6) option has been added to gpec.

<a id="2a4025784cc7f03c"></a>
##### Embedded SQL-only Statement

The GET GROUPID statement has been renamed to GET CLUSTER_GROUP_ID.

<a id="b652288d5e39901a"></a>
##### Host Variable Data Type

The field configuration of the SQL_LONG_VARIABLE_LENGTH_STRUCT structure has been modified. The roles have been separated into buf_len, which represents the capacity of the buffer arr (in bytes), and len, which represents the actual data length (in bytes).([LONG VARCHAR](../part-05-developer-manual/36-embedded-sql.md#62ea82597d663608))

The error handling has been modified so that an error is now raised when a negative value is set for the length member variable (len) of a VARCHAR or VARBINARY variable used as an IN or IN_OUT parameter.

<a id="3b7c8bda3aa54fbb"></a>
##### Dynamic SQL

It supports dynamic SQL Method 4.

<a id="dac485e00f61bd56"></a>
#### PDO

It has not been changed.

<a id="b726950e70de64de"></a>
#### PyDBC

<a id="9f0889c2bb627143"></a>
##### Installation and Packaging

pyproject.toml-based build and wheel/sdist packaging has been applied to the Python 3 package.

The pygoldilocks.pyi type stub has been added to the Python 3 package for IDEs and static type checkers.

<a id="433fb07b2bd686be"></a>
##### connection

setencoding() and setdecoding() are supported in Python 3 for configuring the codec of character data.

connection.messages, character_set_name(), and SQL type-specific output converters are supported in Python 3.

connection.maxwrite is supported for handling large character and binary parameters.

<a id="16382bc4f309d915"></a>
##### Result set and PSM

Multiple result sets returned by procedures can be processed sequentially using cursor.nextset(). It returns True if the next result set exists and None when all result sets have been processed.

procedureColumns() has been added to retrieve IN, OUT, and INOUT parameter metadata of procedures.

fetchval(), cursor iterator, and statement cancel features are supported.

ursor.lastrowid is not supported and always returns None.

<a id="f888c1f6e1ff6738"></a>
##### Data Type

In Python 3, TIME WITH TIME ZONE and TIMESTAMP WITH TIME ZONE are returned as timezone-aware datetime objects with preserved UTC offsets.

In Python 2, time zone types are returned as strings.

The conversion of fractional seconds and microseconds for TIME and TIMESTAMP has been improved.

The handling of precision/scale for NUMBER, NUMERIC, and DECIMAL has been improved, and decimal values such as NaN and Infinity are not supported.

<a id="6cecc72444e08c91"></a>
#### SQLAlchemy

It supports SQLAlchemy 1.4 and 2.0.

<a id="6d027d4d07fd498b"></a>
#### Hibernate

It supports hibernate version 6, 7 and 8.

<a id="2c9d79b09da3ce39"></a>
### Utility

<a id="4c6013749cec9143"></a>
#### gcreatedb

It has not been changed.

<a id="be8f6a9362967473"></a>
#### glsnr

It has not been changed.

<a id="5295112b8ce9e52a"></a>
#### gsql/gsqlnet

<a id="410453075076b56c"></a>
##### ROLE

`The [\ddl_role](../part-06-utility-manual/44-gsql-gsqlnet-interactive-sql-tool.md#ed2c1c9efa24cd42) ` feature has been added to export DDL statements related to role objects.

<a id="38354fc51b688ad2"></a>
##### TRIGGER

The [\ddl_trigger](../part-06-utility-manual/44-gsql-gsqlnet-interactive-sql-tool.md#468a1a5f912f53c6) feature has been added to export DDL statements related to trigger objects.

<a id="09df3d52121939bf"></a>
#### gloader/gloadernet

The directio-size option has been deprecated.

Added support for [APPEND INSERT](../part-03-sql-manual/12-sql-languages.md#df02d66ddd4d5aa0), along with the merge, skip_index_maintenance, and nologging options.

<a id="e651c3ab9e9beeae"></a>
#### gdump

The log option name has been changed to redo_log.

The data option name has been changed to datafile.

<a id="da16e35ccad4872c"></a>
#### tablediff

It has not been changed.

<a id="b2362c4461684cda"></a>
#### gsyncher

It has not been changed.

<a id="a849f2df3562c14e"></a>
#### gmon

It has not been changed.

<a id="81816a37560a8e39"></a>
#### gtrclogger

It has not been changed.

<a id="26d35bf90c8e67b5"></a>
#### glocator

The configuration property ALTERNATE_LOCATORS has been changed to ALTERNATE_LOCATOR.

The glocator multiplication has been changed to replication.

It has been changed not to use any arguments in the sync option.

<a id="2e7aa6c0aae3c99e"></a>
#### gagent

The configuration property ALTERNATE_LOCATORS has been changed to ALTERNATE_LOCATOR.

<a id="7984e50db29adcd0"></a>
#### gloctl

It has not been changed.

<a id="01e57af8f935f759"></a>
### Replication

<a id="488cc51e85ea2a4e"></a>
#### cyclone

A data migration feature to external databases (Oracle, DB2, MySQL, Tibero) has been added.

The heartbeat protocol has been separated from the data protocol.

<a id="d49de5d54a193cbc"></a>
#### logmirror

It has not been changed.

<a id="f6b42aa1008cbd50"></a>
#### cymon

It has not been changed.

<a id="7104ef1b814d7e0e"></a>
#### cyfile

It has not been changed.

---

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
