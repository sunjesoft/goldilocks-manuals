<a id="a42c13f097b7570b"></a>

# 4. What's New

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/a42c13f097b7570b)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<a id="c9232fa3f25a2c97"></a>
## Feature Matrix

This chapter briefly describes the features added to each major version.

<a id="b0fb5136cbc96a8d"></a>
### Architecture

<a id="1d06fdb749cbe8fd"></a>
#### System Architecture

The following is a feature matrix for system architecture.

**Feature matrix for system architecture**

<a id="734922be1130e2e5"></a>
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

<a id="77b3818fd5e54e09"></a>
#### Storage Internal

The following is a feature matrix for storage internal.

**Feature matrix for storage internal**

<a id="5d7c36b3d6db03cf"></a>
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

<a id="da24901878998725"></a>
#### Transaction Control

The following is a feature matrix for transaction control.

**Feature matrix for transaction control**

<a id="389ec66f462ece2c"></a>
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

<a id="42cf7d8cf31d486c"></a>
#### Backup & Recovery

The following is a feature matrix for backup & recovery.

**Feature matrix for backup & recovery**

<a id="103f104b6d5009c4"></a>
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

<a id="9c70ea8b941be246"></a>
#### Database Information

<a id="be78f06d20e734c5"></a>
##### DICTIONARY_SCHEMA Schema

The following is a feature matrix for DICTIONARY_SCHEMA schema.

<a id="558cbd5b486d1f9a"></a>
<table class="table column_count_6"><caption>Feature matrix for DICTIONARY_SCHEMA schema </caption><thead><tr><th class="to_center"><div>Family</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="53"><div>Views of ALL_family</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="46"><div>Views of DBA_family</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="49"><div>Views of USER_family</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="14"><div>Other views</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Aliased Synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="8b35925656951ad0"></a>
##### INFORMATION_SCHEMA Schema

The following is a feature matrix for INFORMATION_SCHEMA schema.

**Feature matrix for INFORMATION_SCHEMA schema**

<a id="c3ae4fc6c8344dcd"></a>
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

<a id="df413ced1362067c"></a>
##### PERFORMANCE_VIEW_SCHEMA Schema

The following is a feature matrix for PERFORMANCE_VIEW_SCHEMA schema.

**Feature matrix for PERFORMANCE_VIEW_SCHEMA schema**

<a id="dade34de5ccf6b60"></a>
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

<a id="bf2445f053e0db58"></a>
#### Server Property

The following is a feature matrix for server property.

**Feature matrix for server property**

<a id="34f7d6d6826028fd"></a>
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

<a id="6757748b70fd709c"></a>
### SQL

<a id="88e34f9a890451f3"></a>
#### SQL Element

<a id="55b16aa93e9d85d3"></a>
##### Data Type

The following is a feature matrix for data type.

<a id="bdb29601d0092390"></a>
<table class="table column_count_6"><caption>Feature matrix for data type</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>Character string type</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Binary string type</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Decimal number type</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Binary number type</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN type</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Date/ time type</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL type</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ROWID type</div></td><td><div>ROWID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="c2c3530448f455d4"></a>
##### Function

The following is a feature matrix for function.

**Feature matrix for function**

<a id="e82e84bf949cd333"></a>
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

<a id="c05cff2024c4990f"></a>
#### Object

<a id="0af19ed509999b1f"></a>
##### SQL Object

The following is a feature matrix for DDL which creates/ drops/ alters an SQL object.

<a id="2c43f367cf76713d"></a>
<table class="table column_count_6"><caption>Feature matrix for SQL object DDL</caption><thead><tr><th class="to_center"><div>Object</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Database 
object</div></td><td><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE REGISTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RESTORE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMENT ON object IS ..</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
object</div></td><td><div>CREATE PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
object</div></td><td><div>CREATE AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NOAUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
object</div></td><td><div>CREATE USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GRANT privileges TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REVOKE privileges FROM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 
object</div></td><td><div>CREATE SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
object</div></td><td><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="20"><div>Table 
object</div></td><td><div>CREATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRUNCATE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
object</div></td><td><div>CREATE VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Index 
object</div></td><td><div>CREATE INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. AGING</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. RENAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
object</div></td><td><div>CREATE SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SEQUENCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
object</div></td><td><div>CREATE SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
object</div></td><td><div>CREATE PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
object</div></td><td><div>CREATE FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="fce383aaf6f619c2"></a>
##### Cluster Object

The following is a feature matrix for DDL which creates/ drops/ alters a cluster object.

<a id="8261c0e5d5f1dc3e"></a>
<table class="table column_count_6"><caption>Feature matrix for cluster object DDL </caption><thead><tr><th class="to_center"><div>Object</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Cluster system 
object</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
object</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
object</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
object</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Cluster table and shard object</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Global secondary index
object</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="a250ba37257d7e20"></a>
#### SQL Language

<a id="99080604bd3b9778"></a>
##### DML

The following is a feature matrix for DML which manipulates data.

**Feature matrix for DML**

<a id="335c0818ddc620cb"></a>
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

<a id="684771aa9537c28f"></a>
##### Query

The following is a feature matrix for SELECT statement which enquires data.

**Feature matrix for SELECT**

<a id="ac6b9ce7cd298a6b"></a>
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

<a id="b2921e071c1d1712"></a>
##### Control Language

The following is a feature matrix for control statement.

<a id="6df5e00a5e2f6bec"></a>
<table class="table column_count_6"><caption>Feature matrix for control statement</caption><thead><tr><th class="to_center"><div>Control statement</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="7b3f4a0afd4e13d9"></a>
#### PSM Language

The following is a feature matrix for persistent stored module (PSM) language element.

**Feature matrix for persistent stored module (PSM) language element**

<a id="58c7f56d68bc8ec3"></a>
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

<a id="465e679c864abfd2"></a>
### API

<a id="61317d5aea0690b4"></a>
#### ODBC

The following is a feature matrix for the ODBC standard API.

**Feature matrix for the ODBC standard API**

<a id="ab287ec14a0d210f"></a>
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

The following is a feature matrix for API other than the ODBC standard API.

**Feature matrix for API other than the ODBC standard**

<a id="ca874f7173e6bb7d"></a>
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

<a id="c7b574d1c0dcc44a"></a>
#### JDBC

The following is a class feature matrix for JDBC.

**Class feature matrix for JDBC**

<a id="087cb6527a0e3294"></a>
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

<a id="20845c5179263b68"></a>
#### Embedded SQL

<a id="e9ce934a743d91ba"></a>
##### Precompiler Option

The following is a feature matrix for precompiler option.

**Feature matrix for precompiler option**

<a id="e0324a6c402c9e1c"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --help | X | O | O | O |
| --include-path | X | O | O | O |
| --no-prompt | X | O | O | O |
| --output | X | O | O | O |
| --unsafe-null | X | O | O | O |
| --version | X | O | O | O |

<a id="e487eaef5e49d82c"></a>
##### Embedded SQL-only Syntax

The following is a feature matrix of embedded SQL-only syntax.

**Feature matrix for embedded SQL-only syntax**

<a id="64559d632a3755d7"></a>
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

<a id="2b45ce7567428a74"></a>
##### Host Variable Data Type

The following is a feature matrix for embedded SQL data type which can be used for HOST variables.

**Feature matrix for host variable data type**

<a id="742733e0d017c8d0"></a>
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

<a id="13c0116d46ad4b95"></a>
##### Dynamic SQL

The following is a feature matrix for dynamic SQL.

**Feature matrix for dynamic SQL**

<a id="4b02de21c7032c21"></a>
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

<a id="8f462639f9a2392a"></a>
#### PyDBC

<a id="362620761e9d6d3b"></a>
##### Module

The following is a method feature matrix for pygoldilocks provided by PyDBC.

**Feature matrix for pygoldilock method**

<a id="74ea24dffc1f3a86"></a>
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

The following is an attribute feature matrix for pygoldilocks module.

**Feature matrix for pygoldilock attribute**

<a id="e36f43b5a7b85469"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| apilevel | X | X | X | O |
| threadsafety | X | X | X | O |
| paramstyle | X | X | X | O |
| version | X | X | X | O |
| lowercase | X | X | X | O |

<a id="15e61bd4cbb41ffc"></a>
##### Connection

The following is a method feature matrix for connection object.

**Feature matrix for connection method**

<a id="86e640d6c5d51151"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| cursor | X | X | X | O |
| commit | X | X | X | O |
| rollback | X | X | X | O |
| close | X | X | X | O |
| getinfo | X | X | X | O |
| execute | X | X | X | O |
| set_attr | X | X | X | O |

The following is an attribute feature matrix for connection object.

**Feature matrix for connection attribute**

<a id="309948ed690cad63"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| autocommit | X | X | X | O |
| searchescape | X | X | X | O |
| timeout | X | X | X | O |

<a id="1d047ec18186a368"></a>
##### Cursor

The following is a method feature matrix for cursor object.

**Feature matrix for cursor method**

<a id="e6292e265be03d66"></a>
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

The following is an attribute feature matrix for cursor object.

**Feature matrix for cursor attribute**

<a id="cd916f381b591150"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| Description | X | X | X | O |
| rowcount | X | X | X | O |
| arraysize | X | X | X | O |
| connection | X | X | X | O |
| fast_executemany | X | X | X | O |

<a id="75c8044ba34eabe5"></a>
##### Row

The following is an attribute feature matrix for row object.

**Feature matrix for row attribute**

<a id="1da83cf609b7c334"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| cursor_description | X | X | X | O |

<a id="0cde39783c7e7f5b"></a>
### Utility

<a id="72fb6a01e310c4d1"></a>
#### gcreatedb

<a id="1d111cdfc9da58f8"></a>
##### Command Usage

The following is a feature matrix for command usage of gcreatedb.

**Feature matrix for command usage of gcreatedb**

<a id="9ae62121583a8da3"></a>
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

<a id="6c4b3beffeabea94"></a>
#### glsnr

<a id="16f74531ddb0d87e"></a>
##### Command Usage

The following is a feature matrix for command usage of glsnr.

**Feature matrix for command usage of glsnr**

<a id="37affc3095e34e18"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --help | X | O | O | O |
| --home | X | X | O | O |
| --silent | X | O | O | O |
| --start | X | O | O | O |
| --status | X | O | O | O |
| --stop | X | O | O | O |

<a id="1946b5b16f10a7ef"></a>
##### Configuration File

The following is a feature matrix for configuration of glsnr.

**Feature matrix for configuration of glsnr**

<a id="cbde6e2214cb13e7"></a>
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

<a id="41919db2bfbdcf78"></a>
#### gsql/gsqlnet

<a id="b408a7590089fb13"></a>
##### Command Usage

The following is a feature matrix for command usage of gsql.

**Feature matrix for command usage of gsql**

<a id="79ce61ec5f878f6a"></a>
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

<a id="c3d1fe3c9e33362c"></a>
##### Interactive gsql Command

The following is a feature matrix for interactive gsql command.

**Feature matrix for interactive gsql command**

<a id="5ff562f8ceb5550f"></a>
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

<a id="4d33219cc2ece909"></a>
#### gloader/gloadernet

<a id="1cb2f906fce1d141"></a>
##### Command Usage

The following is a feature matrix for command usage of gloader.

**Feature matrix for command usage of gloader**

<a id="44fee9207d4b98c1"></a>
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

<a id="a78ebde938cbf43f"></a>
##### Control File Syntax

The following is a feature matrix for control file syntax of gloader.

**Feature matrix for control file syntax of gloader**

<a id="54bbde3319a93b52"></a>
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

<a id="0f7653fa020a3b9e"></a>
#### gdump

<a id="51186cf6df690e05"></a>
##### Command Usage

The following is a feature matrix for command usage of gdump.

<a id="ca1b37f52c7206af"></a>
<table class="table column_count_6"><caption>Feature matrix for command usage of gdump</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle"><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="22b8867886d15fd7"></a>
#### tablediff

<a id="03bbaf2e2fa96b90"></a>
##### Configuration File

The following is a feature matrix for configuration file of tablediff.

<a id="ba1599f6c3aa7d57"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of tablediff</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td class="to_middle"><div>SOURCE_PASSWORD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_SCHEMA</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_URL</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_USER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td class="to_middle"><div>TARGET_PASSWORD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_SCHEMA</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_URL</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_USER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td class="to_middle"><div>TARGET_INSERT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_UPDATE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_DELETE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_INSERT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td class="to_middle"><div>DIFF_BIN_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DIFF_OUT_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_CALL_STACK</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_ROW_UNIT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>EXCLUDE_COLUMNS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_DIFF</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_SUCCESS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_QUEUE_SIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_THREAD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_UNIT_SIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PARTITION_RANGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SYNC_OUT_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>WHERE_CLAUSE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="2d0e954a09a33249"></a>
#### gsyncher

<a id="c75a47b0a2380e70"></a>
##### Command Usage

The following is a feature matrix for command usage of gsyncher.

**Feature matrix for command usage of gsyncher**

<a id="743d98b25e932ecb"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --log | X | O | O | O |
| --silent | X | O | O | O |
| --home | X | X | O | O |
| --copy-right | X | O | O | O |
| --backup-path | X | O | O | O |
| --help | X | O | O | O |

<a id="e69b1ee329acd2d8"></a>
#### gmon

<a id="79d2b58787395b40"></a>
##### Command Usage

The following is a feature matrix for command usage of gmon.

**Feature matrix for command usage of gmon**

<a id="6b1ee091674624ff"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --start | X | X | O | O |
| --stop | X | X | O | O |
| --status | X | X | O | O |
| --home | X | X | O | O |
| --silent | X | X | O | O |
| --no-copyright | X | X | O | O |
| --help | X | X | O | O |

<a id="a586f225ec9acd5c"></a>
#### gtrclogger

<a id="e21538fecb7858b8"></a>
##### Command Usage

The following is a feature matrix for command usage of gtrclogger.

**Feature matrix for command usage of gtrclogger**

<a id="018bd87ce4870e1e"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --dir | X | X | O | O |
| --help | X | X | O | O |
| --port | X | X | O | O |
| --start | X | X | O | O |
| --stop | X | X | O | O |

<a id="0c8889ee139c588d"></a>
#### glocator

<a id="d3be5c8d748b1786"></a>
##### Command Usage

The following is a feature matrix for command usage of glocator.

**Feature matrix for command usage of glocator**

<a id="2025a971f3ddcf24"></a>
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

<a id="e6c9883e16978269"></a>
##### Configuration File

The following is a feature matrix for configuration file of glocator.

**Feature matrix for configuration file of glocator**

<a id="f9d81c0e6becead0"></a>
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

<a id="a8a07c83b57983bf"></a>
#### gagent

<a id="b6370591f7ff3a09"></a>
##### Command Usage

The following is a feature matrix for command usage of gagent.

**Feature matrix for command usage of gagent**

<a id="45ff9334538aec2c"></a>
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

<a id="f3ce41ee641750d9"></a>
##### Configuration File

The following is a feature matrix for configuration file of gagent.

**Feature matrix for configuration file of gagent**

<a id="839797187ba6edc2"></a>
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

<a id="0eb49377c7c6fa3f"></a>
#### gloctl

<a id="ea216e587371d37d"></a>
##### Command Usage

The following is a feature matrix for command usage of gloctl.

**Feature matrix for command usage of gloctl**

<a id="3eea82df5280695a"></a>
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

<a id="a8bb30016647bbbc"></a>
##### Configuration File

The following is a feature matrix for configuration file of gloctl.

**Feature matrix for configuration file of gloctl**

<a id="dfd3b895d2760834"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| PORT | X | X | X | O |
| LOCATOR_HOST | X | X | X | O |
| LOCATOR_PORT | X | X | X | O |

<a id="103bd451acc8e383"></a>
### Replication

<a id="90e284d9448c05a5"></a>
#### cyclone

<a id="d3240d31a69b18f9"></a>
##### Command Usage

The following is a feature matrix for command usage of cyclone.

**Feature matrix for command usage of cyclone**

<a id="77be4135e88aa9ef"></a>
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

<a id="668e22eccaa2ac2f"></a>
##### Configuration File

The following is a feature matrix for configuration file of cyclone.

<a id="4fade65e29090cbd"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of cyclone</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="10"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="094d3d5c28a10d66"></a>
#### logmirror

<a id="6a640360f13341a7"></a>
##### Command Usage

The following is a feature matrix for command usage of logmirror.

**Feature matrix for command usage of logmirror**

<a id="ff71828010c43355"></a>
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

<a id="90beaa67d9baa0b7"></a>
##### Configuration File

The following is a feature matrix for configuration file of logmirror.

<a id="21dd4f222d97c87d"></a>
<table class="table column_count_6"><caption>Feature matrix for configuration file of logmirror</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="f47088356cd597ae"></a>
#### cymon

<a id="7e462c94c808b37b"></a>
##### Command Usage

The following is a feature matrix for command usage of cymon.

**Feature matrix for command usage of cymon**

<a id="a9e15c6f70b029b5"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 |
| --- | --- | --- | --- | --- |
| --conf | X | O | O | O |
| --help | X | O | O | O |
| --cycle | X | O | O | O |
| --key | X | X | O | O |
| --start | X | O | O | O |
| --stop | X | O | O | O |
| --status | X | O | O | O |

<a id="d09746270dd9b714"></a>
## What's New in GOLDILOCKS 3.2

This chapter briefly describes the features added to GOLDILOCKS 3.2.

<a id="67bfe5c82187f15e"></a>
### Architecture

<a id="8b9d3b7c986647d4"></a>
#### System Architecture

It has not been changed.

<a id="8f1241496b48fa3c"></a>
#### Storage Internal

It has not been changed.

<a id="052487ecd1531a93"></a>
#### Transaction Control

It has not been changed.

<a id="6bda8e846627ea8a"></a>
#### Backup & Recovery

It has not been changed.

<a id="f8e2ffa2bfeba61e"></a>
#### Database Information

<a id="5600a7e2c2c35a17"></a>
##### DICTIONARY_SCHEMA

The following views have been added to enquire the information about audit policy object.

- [AUDIT_POLICIES](../part-02-administration-manual/9-database-information.md#ead3d16d2bd20d7e)
- [AUDIT_POLICY_OPTIONS](../part-02-administration-manual/9-database-information.md#d838aa0749749ad8)
- [AUDIT_POLICY_ENABLED](../part-02-administration-manual/9-database-information.md#a5e3ef0be7883956)

[AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6) has been added to enquire the audit record.

The following views are deleted.

- ALL_COL_PLACE
- DBA_COL_PLACE
- USER_COL_PLACE

<a id="b6f1d87fefc6609f"></a>
##### INFORMATION_SCHEMA

It has not been changed.

<a id="07092f24cf37cf73"></a>
##### PERFORMANCE_VIEW_SCHEMA

The following views have been added to enquire the information which can be listed in a system action and in a privilege action when defining audit policy options.

- [V$AUDITABLE_DB_PRIVILEGES](../part-02-administration-manual/9-database-information.md#fb0895b2ad2050fa)
- [V$AUDITABLE_SYSTEM_ACTIONS](../part-02-administration-manual/9-database-information.md#d057b6861f9678f8)

<a id="a744b5683c9d76e7"></a>
#### Server Property

<a id="ee17af6fce90e751"></a>
##### Property for Global Temporary Table Has Been Added

[TEMP_UNDO_ENABLED](../part-02-administration-manual/10-server-property.md#dd4d5a08e3407bc2) property has been added to assign the undo logging tablespace for the global temporary table.  
[TEMP_SEGMENT_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#6d1ca0c0fae9e706) has been added to assign the segment cache size of the global temporary table or the global temporary index.

<a id="76e63060d5ed1e21"></a>
##### Recompile Feature Based on the Change of Pages Are Deleted

The recompile feature based on the change of pages, which is supported until 3.1, are deleted. Therefore, the following properties are not supported any more.

- [RECOMPILE_CHECK_MINIMUM_PAGE_COUNT](../part-02-administration-manual/10-server-property.md#ae66ced73047c8e0)
- [RECOMPILE_PAGE_PERCENT](../part-02-administration-manual/10-server-property.md#d90a5fd3aaa1ed78)

<a id="f0140e8abd8a98d3"></a>
##### Property for Auxiliary Tablespace Has Been Added

[SYSTEM_MEMORY_AUX_TABLESPACE_SIZE](../part-02-administration-manual/10-server-property.md#aa09534fd27a4c07) property has been added to determine the size of the auxiliary tablespace

<a id="1af5cfe4297ddef4"></a>
##### Property for Communication Data Compression Has Been Added

[PACKET_COMPRESSION_THRESHOLD](../part-02-administration-manual/10-server-property.md#fbb85a80a54ba497) property has been added to determine whether to compress the communication data.

<a id="9db71a4bcd351319"></a>
##### Property for Redo Log Compression Has Been Added

[REDO_LOG_COMPRESSION_THRESHOLD](../part-02-administration-manual/10-server-property.md#359482e7ceb5193e) property has been added to determine whether to compress the redo log.

<a id="0a743fed5b3b6aab"></a>
##### USE_LARGE_PAGES Property Has Been Added

[USE_LARGE_PAGES](../part-02-administration-manual/10-server-property.md#5a65cc9ecf6f9b46) property has been added to use HugePage.

<a id="9ae63d49e24a4a6f"></a>
### SQL

<a id="0b4053eac814d39a"></a>
#### SQL Element

<a id="8f04db6ee2a8b36e"></a>
##### Data Type

It has not been changed.

<a id="6ad20323f8f7cebc"></a>
##### Function

The following aggregation functions related to variation have been added.  

[STDDEV](../part-03-sql-manual/11-sql-elements.md#aa121de14f05d3e8)  
[STDDEV_POP](../part-03-sql-manual/11-sql-elements.md#70c13c621cbfb9c8)  
[STDDEV_SAMP](../part-03-sql-manual/11-sql-elements.md#3aed39af2add9685)  
[VARIANCE](../part-03-sql-manual/11-sql-elements.md#80ab44261e08c113)  
[VAR_POP](../part-03-sql-manual/11-sql-elements.md#a6f898169be957da)  
[VAR_SAMP](../part-03-sql-manual/11-sql-elements.md#9881748ecbb23c59)  

The string function [REVERSE](../part-03-sql-manual/11-sql-elements.md#ebd260b7c3d0fd65) has been added.  
The date function [MONTH_BETWEEN](../part-03-sql-manual/11-sql-elements.md#d02398fbef36e530) has been added.

<a id="ded2df71876aa223"></a>
#### Object

<a id="ab2ebe204a873919"></a>
##### Audit Policy

[Audit policy](../part-03-sql-manual/13-sql-objects.md#d65bdf8ed1ea4a2a) object which can audit SQL performance has been added.

<a id="82eff66019f38b21"></a>
##### Global Temporary Table

[Global temporary table](../part-03-sql-manual/13-sql-objects.md#d74235a3a28eef92) which is a temporary table depending on the session has been added.

<a id="5ab480aebc59e814"></a>
#### SQL Language

<a id="8dcd8e71a2bb2f85"></a>
##### Parallel Processing of ANALYZE TABLE Statement

Parallel processing option has been added to [ANALYZE TABLE](../part-03-sql-manual/16-sql-references.md#7a194a6cfef8c726) statement.

<a id="ea0f0d5219abcf7f"></a>
##### Audit Policy DDL

The following DDLs which can control audit policy objects have been added.

- Creating audit policy
    - [CREATE AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#6be201c413853041)
- Dropping audit policy
    - [DROP AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#bd602160c2b9fd00)
- Altering audit policy
    - [ALTER AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#41e688c628dec27b)
- Activating audit policy
    - [AUDIT POLICY](../part-03-sql-manual/16-sql-references.md#7207b4f12e0bf6f6)
- Deactivating audit policy
    - [NOAUDIT POLICY](../part-03-sql-manual/16-sql-references.md#bd9d827360468b68)
- Dropping audit trail
    - [ALTER DATABASE CLEAR AUDIT TRAIL](../part-03-sql-manual/16-sql-references.md#4bae50ba8bf61053)

<a id="351e4a85407b83de"></a>
##### User DDL

User's default index tablespace has been added.

- Creating a user
    - [CREATE USER](../part-03-sql-manual/16-sql-references.md#524780362f90ebc8)
- Altering a user
    - [ALTER USER](../part-03-sql-manual/16-sql-references.md#ed40a6862d9c8f12)

<a id="f3d63653eeda9d77"></a>
##### Table DDL

The following DDLs which alters the table object have been added.

- Altering the name of the table constraints
    - [ALTER TABLE name RENAME CONSTRAINT](../part-03-sql-manual/16-sql-references.md#fdce17f8e7a2137b)
- Altering the table properties
    - [ALTER TABLE name READ { ONLY | WRITE }](../part-03-sql-manual/16-sql-references.md#7ec007f109a6e713)
- Altering the specific shard name of a table in a cluster environment
    - [ALTER TABLE name RENAME SHARD](../part-03-sql-manual/16-sql-references.md#c7ea8d74ec6bdc02)

DDL creating [global temporary table](../part-03-sql-manual/16-sql-references.md#5d245a0d6b896d4d) has been added.

<a id="4984449a97a1e5e1"></a>
##### Index DDL

The following DDL altering an index object has been added.

- Altering the index name
    - [ALTER INDEX name RENAME TO](../part-03-sql-manual/16-sql-references.md#1c016a1f45a446bc)

<a id="9b0b47ee37aa791c"></a>
##### Cluster System DDL

The following DDL altering a cluster system object has been added.

- Assigning an irrecoverable cluster member
    - [ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER](../part-03-sql-manual/16-sql-references.md#9f9987d2e2ba0d12)

<a id="f32da254c76efe86"></a>
##### System DCL

The following DCL controlling a system object has been added.

- Setting the reconnection of a session using GLOBAL CONNECTION
    - [ALTER SYSTEM RECONNECT GLOBAL CONNECTION](../part-03-sql-manual/16-sql-references.md#09f225f9ae90b003)

<a id="fc3217f12ea5bc03"></a>
### API

<a id="6f6cc68b12beec83"></a>
#### ODBC

<a id="cf2f448e934fdad6"></a>
##### odbc.ini

LOCATOR_SERVICE and  PACKET_COMPRESSION_THRESHOLD have been added to [odbc.ini file ](../part-05-developer-manual/25-odbc.md#bdc1948c0522f52f) as a data source name keyword.

ALTERNATE_LOCATORS and CONNECTION_TIMEOUT have been added as a location keyword.

<a id="68691c18059aebf5"></a>
##### GLOBAL CONNECTION

It supports [global connection](../part-05-developer-manual/25-odbc.md#7f0533e89f5e09e6).

<a id="5696d0c160e266c9"></a>
#### Statement Attributes

SQL_ATTR_FETCH_FAILOVER has been added to the statement property values.

<a id="6de6950d86b2c414"></a>
#### JDBC

<a id="8e000d78d95fef30"></a>
##### Connection Property

packet_compression_threshold has been added to [connection property](../part-05-developer-manual/26-jdbc.md#0342fbea344af6ed).

<a id="9cf9a083a4cd9f67"></a>
#### Embedded SQL

[EXEC SQL GET GROUPID INTO](../part-05-developer-manual/27-embedded-sql.md#92773049ec4eb75e) statement has been added.

<a id="a5309841fc5e5cee"></a>
#### PDO

[PDO](../part-05-developer-manual/28-pdo.md#b2017b736dcfdf85) driver which can access GOLDILOCKS from PDO has been added from Venus 3.2 version.

<a id="f04111db3eeb4a94"></a>
#### PyDBC

[PyDBC](../part-05-developer-manual/29-pydbc.md#b2cdf0a1c34ca612) which is API for python language is provided from Venus 3.2 version.

<a id="8a6c75af6e0dcd32"></a>
#### Ruby

[Ruby](#8a6c75af6e0dcd32) driver which is API for ruby language is provided from Venus 3.2 version.

<a id="01942fb1d78465a8"></a>
#### Hibernate

The source which can interwork with [hibernate](../part-05-developer-manual/30-hibernate.md#b4c603685b3709d8), Java ORM framework, is provided from Venus 3.2 version.

<a id="004041431a3d076f"></a>
### Utility

<a id="83de8138257a4466"></a>
#### gcreatedb

It has not been changed.

<a id="125b1c1bceed2fde"></a>
#### glsnr

It has not been changed.

<a id="cea5e55ce34155ec"></a>
#### gsql/gsqlnet

<a id="278e6d44b736e826"></a>
##### DDL Output of an Audit Policy Object

[`\ddl_audit_policy`](../part-06-utility-manual/33-gsql-gsqlnet-interactive-sql-tool.md#e187a7595fbe5445), an interactive command, has been added to output DDL of an audit object.

<a id="f1013e623f396444"></a>
##### SET HEADING {ON | OFF}

[`\set heading`](../part-06-utility-manual/33-gsql-gsqlnet-interactive-sql-tool.md#51148a17dbd631f0) has been added to set whether to output the header in the query result.

<a id="8fb3e956cc1ccbba"></a>
#### gloader/gloadernet

<a id="ed4fdf6882197346"></a>
##### WHERE Clause

The following conditional clauses can be set in an export (data download).

- [WHERE](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#33f2f40f4ccdc7b3)
- [--where](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#db2780dfb5eefa55)

<a id="004549247c73a5cb"></a>
##### --group-id

gloader command argument [--group-id](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#28e5b53099d6245b) has been added.

<a id="6c44b6676e8ed29e"></a>
##### --directio-size

gloader command argument [--directio-size](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#51f42bb5e33d7cbc) has been added.

<a id="844fd5b92dac4223"></a>
#### gdump

It has not been changed.

<a id="c5f22b7d8100f43b"></a>
#### tablediff

It has not been changed.

<a id="55cdc9815a524948"></a>
#### gsyncher

It has not been changed.

<a id="f90789eb7c03b40b"></a>
#### gmon

It has not been changed.

<a id="68baa4c8ab59238b"></a>
#### gtrclogger

It has not been changed.

<a id="d97b69ab28754560"></a>
#### glocator

<a id="8d0fb519985ef603"></a>
##### Configuration

[ALTERNATE_LOCATORS](../part-06-utility-manual/40-glocator.md#8c6db02941896095) has been added as a configuration keyword which is related to the replication.

<a id="8c3feb7f0f8bde66"></a>
##### Argument

--[sync](../part-06-utility-manual/40-glocator.md#b9e185ed83756d47) option has been added to an argument.

<a id="7270aaedfeab3865"></a>
#### gagent

<a id="70415c9ff42012f9"></a>
##### Configuration

[ALTERNATE_LOCATORS](../part-06-utility-manual/40-glocator.md#8c6db02941896095) has been added as a configuration keyword.

<a id="e82544c6d4d16fb3"></a>
#### gloctl

<a id="fc0ea9ea8df945bd"></a>
##### Configuration

[Configuration](../part-06-utility-manual/42-gloctl.md#e8e424fcc3f5e607) file which sets the driving environment of gloctl has been added.

[conf](../part-06-utility-manual/40-glocator.md#07efcb54971c16a2) option which assigns the configuration file has been added.

<a id="33c80732dc0b9fbf"></a>
##### --dsn

dsn option of when driving gloctl is deleted.

<a id="5de7deda7907f0c2"></a>
### Replication

<a id="370ce98d46181218"></a>
#### cyclone

[Recovery](../part-07-replication/44-cyclone.md#31d85f08e70598b8) function has been added.

[Operating CYCLONE in Cluster](../part-07-replication/44-cyclone.md#0376a1d9a1e16786) function has been added.

Database supporting the slave supports [ORACLE_DRIVER](../part-07-replication/44-cyclone.md#090514400ba1a240) as well as GOLDILOCKS.

[Executing options](../part-07-replication/44-cyclone.md#882734f64f5d2e44)of the standalone have been added.

Local [executing options](../part-07-replication/44-cyclone.md#882734f64f5d2e44) have been added.

<a id="c01da282d6d9e3f7"></a>
#### logmirror

It has not been changed.

<a id="bdbc0a3ea891302d"></a>
#### cymon

It has not been changed.

<a id="8066758dde3d3ef8"></a>
## Patch Notes

<a id="8b209540cc568ead"></a>
### 3.2.14 Patch Note

<a id="f74e00304209723c"></a>
#### <kbd>ISSUE-6253</kbd> It supports the property to use the normal page when it fails to allocate the shared memory using the large page.

<a id="c995973af7ec01e7"></a>
##### Description

It supports [USE_LARGE_PAGES](../part-02-administration-manual/10-server-property.md#5a65cc9ecf6f9b46) property. This property allows to use the normal page and the large page when allocating the shared memory. This property also allows to allocate the shared memory using the normal page when it fails to allocate the shared memory using the large page.

<a id="476d24ecfb842a14"></a>
##### Workaround

The patch is required.

<a id="7d0409dd46c6662e"></a>
### 3.2.13 Patch Note

<a id="a2aa1ebc9952e108"></a>
#### <kbd>ISSUE-5862</kbd> If the connection object is shared in the multi-thread program of JDBC, the deadlock occurs.

<a id="b4ea0fa8938bc395"></a>
##### Description

If the connection object is shared and used in the multi-thread program, the deadlock occurs.

<a id="aa300534a73532fc"></a>
##### Workaround

Create each different connection object per the thread, and use them.

<a id="46c3e792e7a2f46e"></a>
### 3.2.12 Patch Note

<a id="21b1bba8113f682f"></a>
#### <kbd>ISSUE-4362</kbd> It is abnormally terminated because cserver refers to the freed memory in the cluster.

<a id="068e2898af7f90ef"></a>
##### Description

If executing another dml after freeing the memory used in c server session when the remote member performs dml in the cluster, then it is abnormally terminated. It is because it uses the freed memory, and this is a bug, but this error has been fixed.

<a id="ddbb485584b1a457"></a>
### 3.2.11 Patch Note

<a id="a167b44fdb1f22d7"></a>
#### <kbd>ISSUE-3869</kbd> The result of row status is wrong when executing array fetch in ODBC.

<a id="deeb1a67f0bffbf8"></a>
##### Description

When executing array fetch in ODBC, the status value of the row can be seen after calling SQLFetch function. If the returned value of SQLFetch is not SQL_SUCCESS, then it is required to check the row status or the diagnostic.   
However, even when the returned value of SQLFetch is SQL_SUCCESS_WITH_INFO, the diagnostic message is seen but all row statuses are SQL_ROW_SUCCESS, which are wrong.

<a id="55815daa59ab7971"></a>
##### Symptom

The following is the string data which can not be converted to number.

```
CREATE TABLE T1 ( I1 VARCHAR(10) );
INSERT INTO T1 VALUES ( '1' );
INSERT INTO T1 VALUES ( '2A' );
INSERT INTO T1 VALUES ( '3' );
INSERT INTO T1 VALUES ( 'AB' );
COMMIT;
```

The following is a part of an example of executing array fetch after converting the data above to the numeric type.

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

The data can not be converted to number is included, but all row statuses are SQL_ROW_SUCCESS.

```
row status: 0
row status: 0
row status: 0
row status: 0
```

<a id="6dff3f926ff26368"></a>
##### Workaround

The patch is required.

<a id="7e86b9d18f449555"></a>
#### <kbd>ISSUE-3534</kbd> gagent does not shutdown the server, but the server is terminated by itself during the cluster failover process.

<a id="7d1d57058863c1c0"></a>
##### Description

If gagent receives the non-viability result during the cluster failover process, then gagent used to shutdown the server by executing SHUTDOWN ABORT. However it has been changed so the server is terminated by itself.

<a id="33defc4d36d988ae"></a>
#### <kbd>ISSUE-3534</kbd> glocator is changed to transfer the result only to gagent which enquired while processing the cluster failover.

<a id="c1f9e5ec9e01bf3d"></a>
##### Description

glocator transfers the failover result not only to gagent which enquired but also to another gagent which is a failover target, during the cluster failover process. However, in this case, gagent which is a failover target also transfers a query to glocator to process the cluster failover. Therefore, glocator is changed to transfer the result only to gagent which enquired.

<a id="266e626c93a1d716"></a>
#### <kbd>ISSUE-3314</kbd> When registerOutParameter() and set..() which are the method of CallableStatement in JDBC are used in the same parameter, then the normal value can not be get.

<a id="6c3e0748ac0c2c99"></a>
##### Description

A bind type is set to INPUT OUTPUT by using registerOutParameter() method and set...() method to get the out parameter value by calling the procedure whose bind type is not clear by using CallableStatement. Then, it does not return the normal value when calling get...() method to get the result value of the out parameter.

<a id="acd22e4b40b8a84b"></a>
##### Symptom

Create a table and a procedure as follows.

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

The following is a result of calling the procedure PROC_TEST_1 in gsql. The result value is stored in the out value of the second parameter.

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

The following is a part of the program code, calling procedure PROC_TEST_1.

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

When executing the program, then the out parameter value is stored in the first parameter as follows instead of the second parameter.

```
OUTPUT: 6, 0
```

<a id="f86b18f0125a72d8"></a>
##### Workaround

Make sure the input, output types as follows, and avoid using set method neither registerOutParameter method above, then the normal result is output.

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

<a id="a8b2a5286c7c0c33"></a>
#### <kbd>ISSUE-3302</kbd> An error occurs when executing getBytes() method which is the method of CallableStatement in JDBC.

<a id="9083484678476e12"></a>
##### Description

When the out parameter type in CallableStatement is either BINARY, VARBINARY or LONG VARBINARY, then using getBytes() method causes an error.

<a id="b0f516925b820bed"></a>
##### Symptom

The following is an example of registering the out parameter as Types.BINARY in CallableStatement.

```
CallableStatement sCStmt = aCon.prepareCall( "BEGIN ? := x'aaff'; END; " );
sCStmt.registerOutParameter(1, java.sql.Types.BINARY);
sCStmt.executeUpdate();
byte[] sValue = sCStmt.getBytes(1);
```

When executing the program containing the codes above, then an error occurs.

```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: -1
	at indep.jdbc.dt.RowCache.readBytes(RowCache.java:637)
	at indep.jdbc.dt.Column.getBytes(Column.java:589)
	at indep.jdbc.core.JdbcCallableStatement.getBytes(JdbcCallableStatement.java:316)
```

<a id="d2c2a796cbcc2bc3"></a>
##### Workaround

The patch is required.

<a id="47c1cf73a6846cc7"></a>
#### gloader command argument *--group-id* has been added.

<a id="18610dccd7584cc3"></a>
##### Description

[--group-id](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#28e5b53099d6245b) argument uploads the data in the sharded table by group in the cluster environment.

<a id="432a5c17932cd018"></a>
#### gloader command argument *--directio-size* has been added.

<a id="2afaf918a823f762"></a>
##### Description

[--directio-size](../part-06-utility-manual/34-gloader-gloadernet-upload-download-tool.md#51f42bb5e33d7cbc) argument is used to modify the direct IO size.

<a id="9462df1324e30c4b"></a>
### 3.2.10 Patch Note

<a id="8649cac67f7b6cbf"></a>
#### <kbd>ISSUE-3253</kbd> When recovering the offline tablespace during the service, then it does not recover the log written on the log buffer.

<a id="df279bb52adcdadf"></a>
##### Description

When switching the offline tablespace in GOLDILOCKS to online, it may requires the recovery or may not. The recovery is required when *IMMEDIATE* option is used in the offline statement, or when that tablespace was shifted to offline due to an error occurred in the data file during the operation. In this case, the log about that tablespace may remain in the buffer, but the recovery is performed only with the logs written on the log file, so the system can be abnormally terminated or the database becomes inconsistent.

<a id="5059d6ac01f26aba"></a>
##### Symptom

It creates the table T1 in the tablespace created by a user, then deletes the datafile and creates the checkpoint while the transaction TX1 updates T1. If the datafile does not exists while performing the checkpoint, then it shifts that tablespace to offline, then rolls back the transaction TX1. Moreover, if recovering the offline tablespace and shifting to online when the log in the log buffer is not written on the disk yet, then the it is abnormally terminated.

<a id="25fbdd05912b56f9"></a>
##### Workaround

The patch is required.

<a id="b3cf5ed2f754cd2f"></a>
#### <kbd>ISSUE-3222</kbd> When GOLDILOCKS system process in the cluster environment hangs up, then the entire system stops.

<a id="1f9e97edba4f8095"></a>
##### Description

If the GOLDILOCKS system process of the remote cluster member hangs up, so it can not transfer the respond when waiting for the response after transferring the protocol to the remote cluster member in the cluster environment, then not only the session waiting for the response but also the entire system stops. It happens because the query timeout or the session status is not checked for the protocol which should receive the respond within GOLDILOCKS. This error has been fixed by terminating the session which does not responds within the specified time or by making the remote cluster member which does not responds to be failover then proceeding the service.

When using the policy terminating the session, it waits for the time (seconds) specified in [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](../part-02-administration-manual/10-server-property.md#30569b05453f1dcd), then terminates the session. However, when using the failover policy, it waits for the time (seconds) specified in [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](../part-02-administration-manual/10-server-property.md#bc867ec7116a99bb), then it makes the remote cluster member which does not responds to be failover.

<a id="677d8d75c07d6016"></a>
##### Symptom

When committing in the session connected to G1N1 after making the commit server of G1N2 member in an 1 by 2 cluster which consists of G1N1, G1N2 to hang up, then the session can not receive the response so stops.

When performing *ALTER SYSTEM SWITCH LOGFILE* in the session connected to G1N1 after making the gmaster of G1N2 member to hangup, then the session can not receive the response and stops.

<a id="d08bac6e8d12ee59"></a>
##### Workaround

The patch is required.

<a id="00412600b03edaf9"></a>
#### <kbd>ISSUE-3175</kbd> gpec can not process the annotation in #define statement.

<a id="d5d6068c23916374"></a>
##### Description

If an annotation exists in #define statements, then gpec can not process it.

<a id="f68342fe77cff604"></a>
##### Symptom

The macro AA in the following gc file should be same, which is 1. However, gpec can not process the annotation in the macro, so it is processed wrong. If gpec processes the following gc file, then the warning message is output.

```
#define AA 1 /* comment */
#define AA 1
```

```
ERR-42000(41028): 'AA' macro is already defined at line 3, in file test.gc
```

<a id="665d69ca805e7ba7"></a>
##### Workaround

The patch is required.

<a id="90f81f5f2ea549ef"></a>
#### <kbd>ISSUE-3175</kbd> gpec can not process define statement normally in #if, #else.

<a id="533d9ec5e28e5724"></a>
##### Description

If #define is used between #if and #endif or between #else and #endif, the gpec can not normally process it.

<a id="b05cccf17fbe39aa"></a>
##### Symptom

If #define which belongs to the false condition exists between #if and #endif or between #else and #endif, the gpec should not process it, but it actually processes it.

gpec should not process *#define AA 2* which is the false condition in the following gc file, but actually gpec does not ignore it instead processes it so that an error occurs.

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

<a id="6ca3fb2643e97b2c"></a>
##### Workaround

The patch is required.

<a id="c9b018ac7c66c322"></a>
#### <kbd>ISSUE-3175</kbd> The number #define statements which are processed by gpec is fixed.

<a id="78c6421fa3a1e70d"></a>
##### Description

The number of #define statements managed by gpec is fixed into 256, and if it exceeds 256, then an error occurs.

<a id="1aa2ebfa27cd2bde"></a>
##### Symptom

If the number of each different #define statements in the gc file exceed 256, then the following error occurs.

```
ERR-42000(41000): syntax error at line 258, in file test.gc
ERR-42000(41027): too many 'define' macro (256)
```

<a id="1d2b499d6ccb6871"></a>
##### Workaround

The patch is required.

<a id="5efaa73fcaa33257"></a>
#### <kbd>ISSUE-3175</kbd> gpec can not process the empty bracket annotation normally.

<a id="dfa1eae31cf4357a"></a>
##### Description

If the bracket annotation containing any contents comes next to the empty bracket annotation such as */**/* , then gpec can not parsing it normally.

<a id="2fcf09a30a052832"></a>
##### Symptom

An empty bracket annotation and an ordinary bracket annotation are used together in the following gc file.

```
/**/
EXEC SQL BEGIN DECLARE SECTION;
int  value;
EXEC SQL END DECLARE SECTION;  

/* comment */

EXEC SQL SELECT 1 INTO :value FROM DUAL;
```

If gpec parses this gc file, then the following error occurs during the progress.

```
ERR-42000(41000): syntax error at line 8, in file a.gc: 
SELECT 1 INTO :value FROM DUAL;
                     ^  ^
Error at line 1
ERR-42000(41002): Host variable "value" not declared

ERR-42000(41006): Fatal error while doing embedded SQL precompiling
```

<a id="5c624dadf15797f7"></a>
##### Workaround

Do not use an empty bracket annotation.

<a id="a8df4eafe1ffdf1b"></a>
#### <kbd>ISSUE-3243</kbd> When glsnr receives the wrong protocol it is terminated.

<a id="9976db84f3e89b16"></a>
##### Description

When glsnr receives the wrong protocol, then it is terminated, and this error has been fixed. After the modification glsnr is not terminated though the following log message is output.

```
2020-01-15 17:57:51.835036 THREAD(27742,139777341413120)] 
[LISTENER] Invalid communication protocol : 192.168.0.123
```

<a id="f7c050eaea8e7466"></a>
##### Symptom

When glsnr receives the wrong protocol, glsnr outputs the following log message then is terminated.

```
[2020-01-15 11:14:28.738666 THREAD(5706,140285308184384)]
[LISTENER] abnormally terminated
ERR-08S01(24001): Invalid communication protocol
```

<a id="89f8b3918b34fb4c"></a>
##### Workaround

The patch is required.

<a id="e566907c541d6497"></a>
#### <kbd>ISSUE-3174</kbd> LOCALITY_GROUP_POLICY, LOCALITY_GROUP_PATH, LOCALITY_MEMBER_POLICY, LOCALITY_MEMBER_PATH have been added to ODBC properties.

<a id="b585853da147df82"></a>
##### Description

The followings have been added to ODBC properties.

- LOCALITY_GROUP_POLICY
- LOCALITY_GROUP_PATH
- LOCALITY_MEMBER_POLICY
- LOCALITY_MEMBER_PATH

<a id="44bb0dc04945016e"></a>
#### <kbd>ISSUE-3220</kbd> When multiple subquery conditions exists for more than three joins, some subquery conditions are omitted

<a id="740d63219f59d80a"></a>
##### Description

If two or more subquery conditions exist when joining three more more tables, then the location in which the subquery conditions are processes is determined. (push-down subquery filter)  
In this case, if the first subquery condition is placed at the lowest table, and the second subquery condition is placed at the upper join, then the first subquery condition is omitted.

<a id="fd3bf695730fb329"></a>
##### Symptom

Create the table and the data as follows.

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

If *EXISTS* condition exists like as the following query, then the result satisfying the condition does not exist.

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

However, if *AND NOT EXISTS* subquery condition is inserted to the query above as follows, then the wrong query result is created.

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

<a id="8307ef737ebc791b"></a>
##### Workaround

Insert *NO_PUSH_SUBQ* hint to *NOT EXISTS* subquery as follows, then the correct result is obtained.

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

<a id="08302aa518496b8b"></a>
#### <kbd>ISSUE-3199</kbd> It can not be processed normally when obtaining GroupId in array in EmbeddedSQL.

<a id="b726badd1960f1d8"></a>
##### Description

The program is abnormally terminated when obtaining GroupId in array then executing the cached SQL statement again.

<a id="3d514a5e84c5a6b9"></a>
##### Symptom

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

The program is abnormally terminated if performing the cached *INSERT INTO TEST_T1 VALUES( :sValue )* statement again.

<a id="87d9b9ca331a5d7e"></a>
##### Workaround

Do not use an array, otherwise alter the host variable not to use the cached SQL statement.

<a id="3d0a102a42197ffd"></a>
#### <kbd>ISSUE-3197</kbd> gpec can not process &lt; ... &gt; string normally.

<a id="fded2da14694c545"></a>
##### Description

If &lt; &gt; exists on the same line, then gpec can not parsing it normally.

<a id="e6998a45f5ed3a9b"></a>
##### Symptom

```
for( i = 0; i < 5; i++ ) { // > COMMENT
    sValue[i] = i;
}
```

It can not process *&lt; 5; i++ ) { // &gt;* string normally, so an error occurs when performing gpec.

<a id="b524f26a016ebcc7"></a>
##### Workaround

Write the gc file by relocating the bracket or the comment as follows.

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

<a id="7ecf839f226dba81"></a>
### 3.2.9 Patch Note

<a id="ba9993d9f6353307"></a>
#### <kbd>ISSUE-3188</kbd> set heading has been added in gsql.

<a id="3651dc19e62bd824"></a>
##### Description

It can be set whether to output the header in the query result by using *set heading {on|off}*.

<a id="3a1efc4e2b7d02e5"></a>
### 3.2.8 Patch Note

<a id="3ab9257b5e95d25a"></a>
#### <kbd>ISSUE-3175</kbd> gpec can not process a non-ascii character.

<a id="b6b41c99d30ed40d"></a>
##### Description

When gpec processes the preprocessor whose #if, #ifdef, #elif and #else are false groups, the contents in the group are converted into whitespaces. However, a non-ascii character in the false group is not converted into a whitespace.

<a id="2530633a863cf8b3"></a>
##### Symptom

```
#if 0
    EXEC SQL INSERT INTO TEST_T1 VALUES( :sC1, :sC2 );  -- 주석
#endif
```

When gpec processes the example above, then all contents should be converted into whitespaces, but a non-ascii character remains the same.

```
주석
```

<a id="54f42ad440d0f50e"></a>
##### Workaround

Process a non-ascii character in a form of c annotation.

<a id="0db7f105fa55aa3a"></a>
#### <kbd>ISSUE-2958</kbd> The group ID of the SQL statement can be obtained in the embedded SQL.

<a id="84981b7a78578726"></a>
##### Description

It obtains the the group ID of the delete/ insert/ select/ update statement in the table in which the shard key is set, in the cluster environment which uses the global connection. For more information, refer to [EXEC SQL GET GROUPID INTO](../part-05-developer-manual/27-embedded-sql.md#92773049ec4eb75e).

<a id="391aa5e9e5bc44d2"></a>
#### <kbd>ISSUE-3186</kbd> When two nodes are abnormally terminated at a time, then a hang may occur during the failover.

<a id="3be6da3a88c15ec5"></a>
##### Description

When a domain coordinator node and a global coordinator node are abnormally terminated at a time, then a hang may occur during the failover, and this error has been fixed.

<a id="8f394d49aab7cab5"></a>
##### Symptom

A hang may occur during the failover, then the online transaction service of the groups to which the abnormally terminated nodes belong may stop operating.

<a id="818551f5a0169a8c"></a>
##### Workaround

The patch is required.

<a id="96efd6106dcbc49a"></a>
### 3.2.7 Patch Note

<a id="139dd25c23c43d33"></a>
#### <kbd>ISSUE-3093</kbd> An error occurs while gpec parses the preprocessor #define.

<a id="b437c7f2803d348d"></a>
##### Description

An error occurs when C reserved word comes to the alternative string of the preprocessor #define.

<a id="74a5d2a7ce4d5f34"></a>
##### Symptom

```
#define SQLCA_STORAGE_CLASS extern
```

A parsing error occurs when executing gpec.

```
$ gpec test.gc

FileName: test.gc
Pre-compile test.gc -> test.c
ERR-42000(41000): syntax error at line 1, in file test.gc: 
#define SQLCA_STORAGE_CLASS extern
............................^
Error at line 1, in file test.gc
```

<a id="2ba7cd420192b1d0"></a>
##### Workaround

Define the keyword in an ordinary header file which does not execute gpec.

<a id="fde0b50115ffa404"></a>
### 3.2.6 Patch Note

<a id="16f48a56c854d499"></a>
#### <kbd>ISSUE-3149</kbd> gpec can not parse the file normally which uses a structure array in SELECT INTO statement.

<a id="a7395a908086aa94"></a>
##### Description

gpec can not process the gc file normally which uses a structure array as a host variable in SELECT INTO statement.

<a id="44fce39d013d13a9"></a>
##### Symptom

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

SELECT INTO statement in the example above is altered to the following incorrect statement.

```
sqlargs.sqlstmt = (char *)"SELECT c1,c2,c3,c4\n"
"    INTO  :sArr ?, ?FROM EMP\n"
```

<a id="32e0398c47532a74"></a>
##### Workaround

The patch is required.

<a id="ede3ed94f8ba7773"></a>
#### <kbd>ISSUE-3145</kbd> SSA is increasing due to allocating the new memory even though the available memory exists in the session.

<a id="b66ce8fcc526085e"></a>
##### Description

The memories used after the session is started can be reused, and it is managed into multiple levels according to its size for an efficient memory allocation for the memory fragment. However, the new memory chunk is allocated when reallocating the released memory instead of the memory which is available to be reallocated to minimize the fragment, then it continuously increases SSA, and this error has been fixed.

<a id="3d1c5af40d73120c"></a>
##### Symptom

When viewing V$SYSTEM_MEM_STAT while retrieving the table which includes LONG VARBINARY type, it can be viewed that VARIABLE_STATIC_ALLOC_SIZE is continuously increasing.

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

<a id="39cbf6ccadfe10c1"></a>
##### Workaround

The patch is required.

<a id="77de268675de084a"></a>
#### <kbd>ISSUE-3144</kbd> gloader can not import the data normally when the first character of the field delimiter and that of the line terminator are the same.

<a id="28c58fe14b445b63"></a>
##### Description

If the first character of the field delimiter and that of the line terminator are the same, then the data may be missing or gloader process may be abnormally terminated.

<a id="de0d4b257e6d6507"></a>
##### Symptom

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

The first character of the field delimiter and that of the line terminator are the same, which is ^. The correct result value of the column I3 when gloader imported the data is supposed to be 3456^S, but the actual value is an incorrect value in which ^ is missing.

<a id="45dc3935e7444964"></a>
##### Workaround

Use different characters for the first character of the field delimiter and that of the line terminator each other.

<a id="9dd0e9b2dc578a2b"></a>
### 3.2.5 Patch Note

<a id="dd410311a65f16c5"></a>
#### <kbd>ISSUE-3093</kbd> gpec can process #define and #undef only when they were declared in the declare section. Also, it does not alter the statement about the false value of *if group* such as #ifdef into a white space.

<a id="529d5a874b1b935a"></a>
##### Description

gpec processed #define and #undef which were declared in the declare section, so it can not process the macro in the if group such as #if, #ifdef. Also it does not alter the c code of the *if group* which corresponds to the false value into a white space, so preprocessor is not available in the middle of the c code or the SQL statement.

<a id="ad03d8c6c8a74102"></a>
##### Symptom

If preprocessors #define and #undef are not declared in the declare section, then gpec can not recognize the corresponding macro because it could not process #define and #undef. A user should repeatedly write the same contents because it can not use SQL the preprocessor corresponding to the *if group* in the middle of SQL.

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

> 1 It is false because _DEV_ is declared outside of the declare section.  
> 2 The preprocessor is not processed as a white space, so gpec processes it as a parsing error.  
> 3 An error occurs during parsing the SQL statement.

<a id="1e0e2fbab2248b7c"></a>
##### Workaround

Declare the preprocessors #define and #undef in the declare section, and do not use preprocessors in the middle of the c code and the SQL statement.

<a id="8ddf72efe51c6df7"></a>
#### <kbd>ISSUE-3075</kbd> An error occurs because the data type is changed when repeatedly executingPreparedStatement.setCharactertStream(int, Reader, int) method and PreparedStatement.addBatch() method in JDBC

<a id="857f79e5765d73b5"></a>
##### Description

The data type was determined by using the parameter length when executing PreparedStatement class method of JDBC such as setAsciiStream(), setBinaryStream(), setCharacterStream() methods, and it has been changed to use only the long data type.

<a id="f3f6d13ef83cf7a4"></a>
##### Symptom

When calling addBatch() method after setting the data of the length which was allowed for the VARCHAR type by setCharacterStream() method, and trying to set the data which exceeds the  length which was allowed for the VARCHAR by setCharacterStream() method, then the data type is changed from VARCHAR to LONG VARCHAR, which is an error.

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

<a id="312c15b134872448"></a>
##### Workaround

set Ascii/ Binary/ Character Stream() methods of PrepraredStatement class have two methods, which are the method with the parameter length and the method without the parameter length. Use the method without the parameter length among them.

<a id="43cbc93dc0579b4b"></a>
#### <kbd>ISSUE-3056</kbd> Characters which returns TRUE/ FALSE when performing ResultSet.getBoolean() in JDBC have been diversified.

<a id="c5713d70c12440d8"></a>
##### Description

Previously, only "true", "false" character strings could be converted into boolean type when ResultSet.getBoolean() in JDBC, but "t", "f", "y", "n", "yes", "no", "on", "off", "1" and "0" characters can also be converted into boolean type now.

<a id="a81ca9a4fc86f4d2"></a>
##### Symptom

When reading "0" and "1" with ResultSet.getBoolean(), then an error occurs.

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

<a id="21d5234fba9bb8de"></a>
##### Workaround

The patch is required.

<a id="a5831530ad59177a"></a>
#### <kbd>ISSUE-3055</kbd> Transferring an invalid character when connecting server and client whose character sets are different each other

<a id="1dcab326e9285c85"></a>
##### Description

It transfers an invalid character when connecting server and client whose character sets are different each other, and this error has been fixed.

<a id="8d2f373e87f71564"></a>
##### Symptom

The user "가" is created in Linux server.

```
gSQL> create user "가" identified by test;

User created.

gSQL> grant create session to "가";

Grant succeeded.

gSQL> commit;

Commit complete.
```

An error occurs when connecting from Windows client to Linux server.

```
D:\goldilocks_home\bin>gsqlnet.exe "가" test

ERR-28000(16004): invalid username/password; logon denied
```

It is operated normally when connecting from Linux client to Linux server.

```
% gsqlnet "가" test

gSQL>
```

<a id="f25fa33251c9e3fc"></a>
##### Workaround

Either set character sets in the server and that in the client same, or include only ASCII in a string which is used for the connection.

<a id="662418f033920580"></a>
#### <kbd>ISSUE-2359</kbd> cluster peer without a parent session

<a id="3bff79941b7b4b53"></a>
##### Description

A cluster peer without a parent session exists in a remote node, and this error has been fixed.

<a id="cd4148d13746aec7"></a>
##### Symptom

When an error occurs while altering password when a parent session tries to login, then a cluster peer without a parent session may exist in a remote node  
A cluster peer session may be created in a remote node while altering password, and if it fails to alter the password then the parent session is terminated without terminating the cluster peer session.

<a id="a96ff062d8c6f33d"></a>
##### Workaround

The patch is required.

<a id="a2c5d8c34ca3eda0"></a>
### 3.2.4 Patch Note

<a id="c5ad6c708b20ec12"></a>
#### <kbd>ISSUE-3026</kbd> Altering the location of AT statement when performing `\`ddl_tablespace in gsql

<a id="d464dfa4c99cac6c"></a>
##### Description

AT statement is located in a wrong position when performing `\`ddl_tablespace in gsql, and this error has been fixed.

<a id="f16eabd6829aa649"></a>
##### Symptom

An error occurs when perfroming SQL statement which is created with `\`ddl_tablespace.

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

<a id="9ef5dbdbf8004705"></a>
##### Workaround

Alter the location of AT statement in SQL which is created with `\`ddl_tablespace.

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

<a id="16448f17ff0f3bbf"></a>
#### <kbd>ISSUE-3023</kbd> BEGIN BACKUP AT DOMAIN error

<a id="90e9793c0b0b87d9"></a>
##### Description

It is not normally operated when using AT DOMAIN clause to backup only within a specific group or a member, and this error has been fixed.

<a id="214f74dcc2237486"></a>
##### Symptom

BEGIN BACKUP fails even when the member G1N2 is being operated with ARCHIVELOG as follows.

```
gSQL> SELECT ARCHIVELOG_MODE FROM V$ARCHIVELOG;

ARCHIVELOG_MODE
---------------
ARCHIVELOG     

1 row selected.

gSQL> ALTER DATABASE BEGIN BACKUP AT G1N2;

ERR-HY000(16247): MEMBER(G1N1): cannot BACKUP; noarchivelog mode
```

<a id="a257af7bba0326e2"></a>
##### Workaround

Perform BACKUP BEGIN/ END without using AT DOMAIN.

<a id="60f7c4ffdbcf0ff5"></a>
### 3.2.3 Patch Note

<a id="2763148394c311e2"></a>
#### <kbd>ISSUE-3006</kbd> A transaction is created when performing EXPLAIN PLAN ONLY

<a id="0413f35058dcfc79"></a>
##### Description

A transaction is created when performing EXPLAIN PLAN ONLY, and this error has been fixed.

<a id="ad648680ef455e9a"></a>
##### Symptom

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

<a id="40615049b4105e28"></a>
##### Workaround

The patch is required.

<a id="341985a74fb14268"></a>
### 3.2.2 Patch Note

<a id="0e22ca6ce3ce3b8f"></a>
#### <kbd>ISSUE-2947</kbd> The previous version data of a remote group which was executed in the same session is retrieved in cluster environment.

<a id="a1a2ff1dcba29bc3"></a>
##### Description

If selecting after executing a domain transaction which is updatable only in a specific remote group of a session, then the previous version data is retrieved, and this error has been fixed.

<a id="8df71b87ff6d0307"></a>
##### Symptom

Add a record to a shard in G1 after creating a sharded table in cluster groups G1, G2 as follows.

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

Delete a record (transaction T1) of group G1 in a session (session 1) connected to a member of group G2, then execute a global transaction (transaction T2) in another session (session 2) and commit. When committing T1 and retrieving the record of G1, while T2 is completed in group G1 and is not completed in G2, then the deleted recorded is retrieved.

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

<a id="f430188282e757f3"></a>
##### Workaround

When selecting after executing a domain transaction in the same session, execute it by replace SELECT statement with SELECT FOR UPDATE.

<a id="e7e51c0fc3a7a262"></a>
#### <kbd>ISSUE-2965</kbd> Data is missing when BigDecimal types is used as a parameter in JDBC

<a id="459ec1b17b69b2b2"></a>
##### Description

It the value exceeding the double type precision is used as a parameter in BigDecimal type, then the data is missing, and this error has been fixed.

<a id="14dff2a2455678ca"></a>
##### Symptom

The data is missing without the user's intention.

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

<a id="6c25e018079911a3"></a>
##### Workaround

Process it with a string instead of the BigDecimal type.

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

<a id="1f670ef1fce7dba8"></a>
#### <kbd>ISSUE-2955</kbd> gsqlnet can not consecutively execute cstartup or cshutdown in cluster environment.

<a id="85da7798e72cb8c0"></a>
##### Description

gsqlnet builds the connecting information of a location file and  glocator through ODBC.  
This information is built when executing cstartup or cshutdown for the first time.  
When executing cstartup or cshutdown for the second time, then it ignores the information construction process. However, the flag configuration is wrong, so an error occurs.

<a id="4561b584a496fa65"></a>
##### Symptom

An error occurs when gsqlnet process executes cstartup or cshutdown, then executes it again.

<a id="68ca244fe6998e11"></a>
##### Workaround

Restart gsqlnet session and execute cstartup or cshutdown.

<a id="95dd0f428726280d"></a>
#### <kbd>ISSUE-2943</kbd> agable scn does not increase when a query timeout occurs in cluster environment.

<a id="a566bb5cba44913f"></a>
##### Description

When processing DML in async in a cluster environment,  it sets the view scn information of remote members in a session. In this case, if an exception such as query timeout occurs when there is not anyremote member to whom  DML is successfully transferred, then the view scn information of remotemembers set in the session can not be initialized, and which is a bug. Therefore, the agable scn of the system does not increase while the session is connected even though the statement in progress does not exist in a system.

Therefore, it is fixed to initialize the view scn information of remote members when an exception occurs while processing an async to prevent an error.

<a id="85b1ce5cdd118e66"></a>
##### Symptom

agable scn stops after a query timeout occurs in cluster environment, so the undo, data segments become insufficient.

<a id="16c7e95d3df05b3b"></a>
##### Workaround

Terminate the session in which a query timeout occurred.

<a id="15c3e821c0edb3f4"></a>
#### <kbd>ISSUE-2927</kbd> Deadlock Due to the Lack of Transaction Slot

<a id="ac498e65147bbefb"></a>
##### Description

A hang may occur due to the lack of transaction slots when all server processes allocate transaction slots and the transactions do not release slots. It is fixed to make an error on the corresponding patch when the specified time passed.

<a id="f8fd9b04cca79a92"></a>
##### Symptom

A hang may occur due to the lack of transaction slots when multiple transactions simultaneously occur in multiple sessions.

<a id="4a86f7743069d18e"></a>
##### Workaround

The patch is required.

<a id="cad7e4087fc7ab69"></a>
#### <kbd>ISSUE-2922</kbd> Adding SQL_ATTR_FETCH_FAILOVER to statement attribute in ODBC

<a id="657befe4f2bc5d29"></a>
##### Description

SQL_ATTR_FETCH_FAILOVER has been added to statement attribute in ODBC, and the following values can be set.

- SQL_FETCH_FAILOVER_OFF
- SQL_FETCH_FAILOVER_ON

```
SQLSetStmtAttr( stmt, 
                SQL_ATTR_FETCH_FAILOVER,
                (SQLPOINTER)SQL_FETCH_FAILOVER_ON,
                0 )
```

<a id="60dd1493bab4d823"></a>
##### Symptom

There is not any symptom.

<a id="c0fed353391dd7d0"></a>
##### Workaround

The patch is required.

<a id="74d1dd62fa365c4c"></a>
#### <kbd>ISSUE-2513</kbd> EXEC SQL AT :sConn DISCONNECT can not detect VARCHAR type

<a id="47085058c8ee8666"></a>
##### Description

gpec detects VARCHAR type as char type in EXEC SQL AT clause.

<a id="8cc49e9b246b403c"></a>
##### Symptom

When using VARCHAR type variable in EXEC SQL AT clause, gpec does not process it as VARCHAR type but processes it as char type.

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

It processes VARCHAR type as char * type, so an error occurs when compiling a c file created by gpec.

<a id="2c26b6e58b9a2b85"></a>
##### Workaround

Use char type instead of VARCHAR type.

<a id="a070ae8fc73e265c"></a>
#### <kbd>ISSUE-2349</kbd> When gpec processes a preprocessor, __LINE__ macro indiates the wrong line.

<a id="4413409e8a87661b"></a>
##### Description

When gpec processes a preprocessor such as #if, __LINE__ macro indicates the wrong line.

<a id="e102b1867cf6640c"></a>
##### Symptom

When gpec processes a preprocessor such as #if, #ifdef, #ifndef, #else, #elif, a comment has been added so it leads to a wrong value unlike the intended __LINE__ macro value.

- Example gc file

```
#if 0
    printf("[%s:%d] if\n", __FILE__, __LINE__);
#else
    printf("[%s:%d] else\n", __FILE__, __LINE__);
#endif
    printf("[%s:%d] endif\n", __FILE__, __LINE__);
```

The following is a result of which gpec processes the code.

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

If gpec executes the created c file, then unexpected line is output.

```
$ ./pp_bug
[pp_bug.gc:9] else
[pp_bug.gc:11] endif
```

The following is a normal __LINE__ macro value.

```
$ ./pp_bug
[pp_bug.gc:7] else
[pp_bug.gc:9] endif
```

<a id="7b4d206af4a54a26"></a>
##### Workaround

The patch is required.

<a id="ef1680644a7843fd"></a>
### 3.2.1 Patch Note

<a id="e9bdfb181fc0486f"></a>
#### <kbd>ISSUE-2902</kbd> Deadlock When Referring to the Global Sequence Value in Cluster Environment

<a id="ee477ca7a9f6d8f8"></a>
##### Description

A deadlock occurs while acquiring the global sequence latch for the entire cluster member to get the next value because the cashed value in local members were run out when referring to the global sequence value in cluster environment.

<a id="d45370c0cd808708"></a>
##### Symptom

A hang occurs due to a deadlock when repeatedly performing a statement of which multiple sessions simultaneously refers to the global sequence.

<a id="4a988645e8a94be5"></a>
##### Workaround

The patch is required.

---

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
