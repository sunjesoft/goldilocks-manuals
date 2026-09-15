<a id="06a4113c431f8e11"></a>

# 4. What's New

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/06a4113c431f8e11)  
> Tag: `20c.1_30_tag`

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<a id="92652eeeae3039ad"></a>
## Feature Matrix

This chapter briefly describes the features added to each major version.

<a id="426002b83ef7e20d"></a>
### Architecture

<a id="13043afb9ca1fe4d"></a>
#### System Architecture

The following is a feature matrix for system architecture.

**Feature matrix for system architecture**

<a id="a1f6332468840cfe"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| Shared Nothing Cluster | X | X | O | O | O |
| DA (Direct Attach) | O | O | O | O | O |
| JDBC DA (Direct Attach) | X | X | O | O | O |
| C/S (Client/Server) Dedicated | X | O | O | O | O |
| C/S (Client/Server) Shared | X | O | O | O | O |
| multi-process applications | O | O | O | O | O |
| multi-threaded applications | O | O | O | O | O |
| Linux platform | O | O | O | O | O |
| HP platform | X | O | O | O | O |
| AIX platform | X | O | O | O | O |
| Windows Client Platform | X | O | O | O | O |
| CDC(Change Data Capture) replication | X | O | O | O | O |
| CDC replication with log mirror | X | O | O | O | O |
| multi-level start up | X | O | O | O | O |
| parallel database loading | O | O | O | O | O |
| parallel index build | X | O | O | O | O |
| SQL plan cache | X | O | O | O | O |

<a id="8c7adaa3acca956b"></a>
#### Storage Internal

The following is a feature matrix for storage internal.

**Feature matrix for storage internal**

<a id="7efd252a47d28992"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| memory dictionary tablespace | O | O | O | O | O |
| memory data tablespace | O | O | O | O | O |
| memory undo tablespace | O | O | O | O | O |
| memory temporary tablespace | X | O | O | O | O |
| memory bitmap data segment | O | O | O | O | O |
| memory bitmap undo segment | O | O | O | O | O |
| memory bitmap instant segment | X | O | O | O | O |
| memory heap table | O | O | O | O | O |
| memory instant table | X | O | O | O | O |
| memory B-tree index | O | O | O | O | O |
| memory instant B-tree | X | O | O | O | O |
| memory instant hash | X | O | O | O | O |
| global secondary index | X | X | O | O | O |
| disk data tablespace | X | X | X | X | O |
| disk bitmap data segment | X | X | X | X | O |
| disk B-tree index | X | X | X | X | O |
| disk global secondary index | X | X | X | X | O |

<a id="aa28a14ca99a034b"></a>
#### Transaction Control

The following is a feature matrix for transaction control.

**Feature matrix for transaction control**

<a id="06e4aba577fca9ff"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| CDS(Concurrency Data Store) database mode | O | O | O | O | O |
| TDS(Transactional Data Store) database mode | O | O | O | O | O |
| read-only database | X | O | O | O | O |
| read/write database | O | O | O | O | O |
| flat transaction | O | O | O | O | O |
| distributed transaction | X | O | O | O | O |
| read-only transaction | X | O | O | O | O |
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
| logging group | X | O | O | O | O |
| supplemental logging | X | O | O | O | O |
| mirrored logging | X | O | O | O | O |
| synchronous commit | O | O | O | O | O |
| asynchronous commit | O | O | O | O | O |
| grouped commit | O | O | O | O | O |
| total rollback | O | O | O | O | O |
| implicit statement rollback | O | O | O | O | O |
| savepoint management | X | O | O | O | O |

<a id="16fb0f9682a7700c"></a>
#### Backup & Recovery

The following is a feature matrix for backup & recovery.

**Feature matrix for backup & recovery**

<a id="0bf16bdcc1c7e19d"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| off-line backup | O | O | O | O | O |
| on-line backup | X | O | O | O | O |
| full backup | X | O | O | O | O |
| incremental backup | X | O | O | O | O |
| complete recovery | O | O | O | O | O |
| incomplete recovery | X | O | O | O | O |
| auto instance recovery | O | O | O | O | O |
| tablespace recovery | X | O | O | O | O |
| file recovery | X | O | O | O | O |
| change tracking | X | X | X | X | O |

<a id="4ae57234e50f39cd"></a>
#### Database Information

<a id="26a2facbad882b0e"></a>
##### DICTIONARY_SCHEMA Schema

The following is a feature matrix for DICTIONARY_SCHEMA schema.

<a id="37ae4cc48fc37299"></a>
<table class="table column_count_7"><caption>Feature matrix for DICTIONARY_SCHEMA schema </caption><thead><tr><th class="to_center"><div>Family</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="56"><div>Views of ALL_family</div></td><td><div>ALL_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>ALL_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PACKAGE_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_PROC_PRIV_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_TBS_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALL_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left to_middle" rowspan="48"><div>Views of DBA_family</div></td><td><div>DBA_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>DBA_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_NONSCHEMA_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>DBA_PROFILES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_STAT_SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_TBS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBA_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="53"><div>Views of USER_family</div></td><td><div>USER_ALL_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ARGUMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CATALOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CLUSTER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>USER_COL_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_COL_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_CONS_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_DEPENDENCIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_EXTENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GLOBAL_SECONDARY_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_GSI_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_INDEXES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_IND_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_OBJECTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PACKAGE_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROCEDURES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PROC_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMAS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SCHEMA_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQUENCES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SEQ_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SHARD_KEY_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SOURCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYNONYMS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_SYS_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TABLESPACES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_COMMENTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_IDENTITY_COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PLACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_MADE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_PRIVS_RECD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_TAB_SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_USERS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_VIEWS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="15"><div>Other views</div></td><td><div>AUDIT_POLICIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_ENABLED</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_POLICY_OPTIONS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT_TRAIL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATABASE_PROPERTIES</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DBC_TABLE_TYPE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICTIONARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT_COLUMNS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DUAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IMPLEMENTATION_INFO_BASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>JDBC_CLIENT_PROPS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PRODUCT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SESSION_PRIVS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SUPPLEMENTAL_LOG_TABLE_INFO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>Aliased synonym</div></td><td><div>COLS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DICT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>IND</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>OBJ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RECYCLEBIN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SEQ</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TABS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="62914bcad8e1d9dc"></a>
##### INFORMATION_SCHEMA Schema

The following is a feature matrix for INFORMATION_SCHEMA schema.

**Feature matrix for INFORMATION_SCHEMA schema**

<a id="2f2ec383a70d8eeb"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| COLUMNS | X | O | O | O | O |
| COLUMN_PRIVILEGES | X | O | O | O | O |
| CONSTRAINT_COLUMN_USAGE | X | O | O | O | O |
| CONSTRAINT_TABLE_USAGE | X | O | O | O | O |
| INFORMATION_SCHEMA_CATALOG_NAME | X | O | O | O | O |
| KEY_COLUMN_USAGE | X | O | O | O | O |
| MODULES | X | X | X | X | O |
| MODULE_BODY | X | X | X | X | O |
| MODULE_BODY_MODULE_USAGE | X | X | X | X | O |
| MODULE_BODY_ROUTINE_USAGE | X | X | X | X | O |
| MODULE_BODY_SEQUENCE_USAGE | X | X | X | X | O |
| MODULEBODY_TABLE_USAGE | X | X | X | X | O |
| MODULE_MODULE_USAGE | X | X | X | X | O |
| MODULE_PRIVILEGES | X | X | X | X | O |
| MODULE_ROUTINE_USAGE | X | X | X | X | O |
| MODULE_SEQUENCE_USAGE | X | X | X | X | O |
| MODULE_TABLE_USAGE | X | X | X | X | O |
| PARAMETERS | X | X | O | O | O |
| REFERENTIAL_CONSTRAINTS | X | O | O | O | O |
| ROUTINES | X | X | O | O | O |
| ROUTINE_MODULE_USAGE | X | X | X | X | O |
| ROUTINE_PRIVILEGES | X | X | O | O | O |
| ROUTINE_ROUTINE_USAGE | X | X | O | O | O |
| ROUTINE_SEQUENCE_USAGE | X | X | O | O | O |
| ROUTINE_TABLE_USAGE | X | X | O | O | O |
| SCHEMATA | X | O | O | O | O |
| SEQUENCES | X | O | O | O | O |
| SQL_FEATURES | X | O | O | O | O |
| SQL_IMPLEMENTATION_INFO | X | O | O | O | O |
| SQL_PACKAGES | X | O | O | O | O |
| SQL_PARTS | X | O | O | O | O |
| SQL_SIZING | X | O | O | O | O |
| STATISTICS | X | O | O | O | O |
| TABLES | X | O | O | O | O |
| TABLE_CONSTRAINTS | X | O | O | O | O |
| TABLE_PRIVILEGES | X | O | O | O | O |
| USAGE_PRIVILEGES | X | O | O | O | O |
| VIEWS | X | O | O | O | O |
| VIEW_MODULE_USAGE | X | X | X | X | O |
| VIEW_ROUTINE_USAGE | X | X | O | O | O |
| VIEW_TABLE_USAGE | X | O | O | O | O |

<a id="320b4cb8f10f4e7e"></a>
##### PERFORMANCE_VIEW_SCHEMA Schema

The following is a feature matrix for PERFORMANCE_VIEW_SCHEMA schema.

**Feature matrix for PERFORMANCE_VIEW_SCHEMA schema**

<a id="cf421d65c4f8abc2"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| GV$____ | X | X | O | O | O |
| V$AGABLE_INFO | X | X | O | O | O |
| V$ARCHIVELOG | X | O | O | O | O |
| V$AUDITABLE_DB_PRIVILEGES | X | X | X | O | O |
| V$AUDITABLE_SYSTEM_ACTIONS | X | X | X | O | O |
| V$BACKUP | X | O | O | O | O |
| V$BALANCER | X | O | O | O | O |
| V$BCH | X | X | X | X | O |
| V$BUFFER_STAT | X | X | X | X | O |
| V$CLUSTER_DISPATCHER | X | X | O | O | O |
| V$CLUSTER_LOCATION | X | X | O | O | O |
| V$CLUSTER_MEMBER | X | X | O | O | O |
| V$COLUMNS | X | O | O | O | O |
| V$CONTROLFILE | X | O | O | O | O |
| V$DATAFILE | X | O | O | O | O |
| V$DB_CHANGE_TRACKING | X | X | X | X | O |
| V$DB_FILE | X | O | O | O | O |
| V$DISPATCHER | X | O | O | O | O |
| V$ERROR_CODE | X | O | O | O | O |
| V$GLOBAL_TRANSACTION | X | O | O | O | O |
| V$JOURNALING | X | X | O | O | O |
| V$INCREMENTAL_BACKUP | X | O | O | O | O |
| V$INSTANCE | X | O | O | O | O |
| V$KEYWORDS | X | O | O | O | O |
| V$LATCH | X | O | O | O | O |
| V$LOCK_WAIT | X | O | O | O | O |
| V$LOCKED_OBJECT | X | X | X | X | O |
| V$LOGFILE | X | O | O | O | O |
| V$PROCESS_MEM_STAT | X | O | O | O | O |
| V$PROCESS_SQL_STAT | X | O | O | O | O |
| V$PROCESS_STAT | X | O | O | O | O |
| V$PROPERTY | X | O | O | O | O |
| V$PSM_RESERVED_WORDS | X | X | O | O | O |
| V$QUEUE | X | O | O | O | O |
| V$RESERVED_WORDS | X | O | O | O | O |
| V$SESSION | X | O | O | O | O |
| V$SESSION_AUDIT | X | X | X | O | O |
| V$SESSION_CONNECT_INFO | X | O | O | O | O |
| V$SESSION_EVENT | X | X | O | O | O |
| V$SESSION_MEM_STAT | X | O | O | O | O |
| V$SESSION_SQL_STAT | X | O | O | O | O |
| V$SESSION_STAT | X | O | O | O | O |
| V$SESSION_WAIT | X | X | O | O | O |
| V$SHARED_MODE | X | O | O | O | O |
| V$SHARED_SERVER | X | O | O | O | O |
| V$SHM_SEGMENT | X | O | O | O | O |
| V$SPROPERTY | X | O | O | O | O |
| V$SQLFN_METADATA | X | O | O | O | O |
| V$SQL_CACHE | X | O | O | O | O |
| V$SQL_COMMAND | X | X | O | O | O |
| V$SQL_HISTORY | X | X | O | O | O |
| V$STATEMENT | X | O | O | O | O |
| V$SYSTEM_EVENT | X | X | O | O | O |
| V$SYSTEM_MEM_STAT | X | O | O | O | O |
| V$SYSTEM_SQL_STAT | X | O | O | O | O |
| V$SYSTEM_STAT | X | O | O | O | O |
| V$TABLES | X | O | O | O | O |
| V$TABLESPACE | X | O | O | O | O |
| V$TABLESPACE_STAT | X | X | O | O | O |
| V$TRANSACTION | X | O | O | O | O |
| V$WAIT_EVENT_CLASS_NAME | X | X | O | O | O |
| V$WAIT_EVENT_NAME | X | X | O | O | O |
| V$XA_TRANSATION | X | X | O | O | O |

<a id="50fe0fdea0a2bc72"></a>
#### Server Property

The following is a feature matrix for server property.

**Feature matrix for server property**

<a id="b38cae5aca46fdcf"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| AGING_INTERVAL | O | O | O | O | O |
| AGING_PLAN_INTERVAL | X | O | O | O | O |
| ARCHIVELOG_DIR | O | O | X | X | X |
| ARCHIVELOG_DIR_1 ~ DIR_10 | X | O | O | O | O |
| ARCHIVELOG_FILE | X | O | O | O | O |
| ARCHIVELOG_MODE | X | O | O | O | O |
| BACKUP_DIR_1 ~ DIR_10 | X | O | O | O | O |
| BLOCK_READ_COUNT | O | O | O | O | O |
| BROADCAST_INDEX_REBUILD_PROTOCOL | X | X | X | X | O |
| BROADCAST_REBALANCE_PROTOCOL | X | X | X | X | O |
| BUFFER_CACHE_SIZE | X | X | X | X | O |
| BUFFER_CHECKPOINT_LIST_COUNT | X | X | X | X | O |
| BUFFER_FLUSH_THREADS | X | X | X | X | O |
| BUFFER_FLUSHING_INTERVAL | X | X | X | X | O |
| BUFFER_FREE_LIST_COUNT | X | X | X | X | O |
| BUFFER_HASH_BUCKETS | X | X | X | X | O |
| BUFFER_HOT_REGION_CRITERIA | X | X | X | X | O |
| BUFFER_HOT_REGION_PERCENT | X | X | X | X | O |
| BUFFER_LRU_LIST_COUNT | X | X | X | X | O |
| BUFFER_MULTIPAGE_READ_COUNT | X | X | X | X | O |
| BULK_IO_PAGE_COUNT | X | O | O | O | O |
| CDISPATCHER_HOT_POLICY_INTERVAL | X | X | O | O | O |
| CDISPATCHER_LOCKLESS_THREADS | X | X | X | X | O |
| CDISPATCHER_SOCKET_BUFFER_SIZE | X | X | O | O | O |
| CDISPATCHER_THREADS | X | X | O | O | O |
| CHANGE_TRACKING | X | X | X | X | O |
| CHANGE_TRACKING_EXTENT_SIZE | X | X | X | X | O |
| CHANGE_TRACKING_FILE | X | X | X | X | O |
| CHAR_LENGTH_UNITS | X | O | O | O | O |
| CHARACTER_SET | X | O | O | O | O |
| CHECK_DEDICATE_CONNECTION_INTERVAL | X | X | O | O | O |
| CHECK_DEDICATE_SOCKET | X | X | O | X | X |
| CLIENT_MAX_COUNT | O | O | O | O | O |
| CLIENT_NUMA_POLICY | X | X | O | O | O |
| CLOSE_PSM_CHILD_STMTS | X | X | O | O | O |
| CLUSTER_ASYNC_COMMIT | X | X | O | O | O |
| CLUSTER_ASYNC_REPLICATION | X | X | O | O | O |
| CLUSTER_CM_BUFFER_COUNT | X | X | O | O | O |
| CLUSTER_CM_BUFFER_SIZE | X | X | O | O | O |
| CLUSTER_CM_READ_BUFFER_SIZE | X | X | O | O | O |
| CLUSTER_COMMIT_SLAVES | X | X | O | O | O |
| CLUSTER_COMMIT_STREAM_ISOLATION | X | X | O | O | O |
| CLUSTER_CONNECTION | X | X | O | O | O |
| CLUSTER_CONNECTION_TIMEOUT_SEC | X | X | O | O | O |
| CLUSTER_DATA_SYNC_SERVERS | X | X | O | O | O |
| CLUSTER_DEADLOCK_TIMEOUT | X | X | X | X | O |
| CLUSTER_DISPATCHER_IN_QUEUE_SIZE | X | X | O | O | O |
| CLUSTER_DISPATCHER_NUMA_STREAM_MAP | X | X | O | O | O |
| CLUSTER_DISPATCHER_OUT_QUEUE_SIZE | X | X | O | O | O |
| CLUSTER_HEARTBEAT_INTERVAL | X | X | O | O | O |
| CLUSTER_HEARTBEAT_RETRY_COUNT | X | X | O | O | O |
| CLUSTER_IGNORE_INACTIVE_MEMBER | X | X | O | O | O |
| CLUSTER_MAX_PACKET_SIZE | X | X | O | O | O |
| CLUSTER_MAX_PAYLOAD_SIZE | X | X | O | O | O |
| CLUSTER_PACKET_ALLOCATION_TIMEOUT | X | X | O | O | O |
| CLUSTER_SERVER_RESPONSE_QUEUE_SIZE | X | X | O | O | O |
| CLUSTER_SESSION_HASH_BUCKETS | X | X | X | X | O |
| CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY | X | X | O | O | O |
| CLUSTER_SPLIT_BRAIN_RETRY_COUNT | X | X | O | O | O |
| COMMITTER_HOT_POLICY_INTERVAL | X | X | O | O | O |
| CONTROL_FILE_0 ~ FILE_7 | X | O | O | O | O |
| CONTROL_FILE_COUNT | X | O | O | O | O |
| CONTROL_FILE_TEMP_NAME | X | O | O | O | O |
| COORDINATOR_COMMIT_WRITE_MODE | X | X | O | O | O |
| CSERVERS | X | X | O | O | O |
| DA_CLIENT_NUMA_MODE | X | X | O | O | O |
| DATA_STORE_MODE | O | O | O | O | O |
| DATABASE_ACCESS_MODE | X | O | O | O | O |
| DATABASE_INSTANCE_NAME | X | X | O | O | O |
| DDL_AUTOCOMMIT | X | O | O | O | O |
| DDL_LOCK_TIMEOUT | O | O | O | O | O |
| DEADLOCK_PRIORITY | X | X | X | X | O |
| DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION | X | X | O | O | O |
| DEFAULT_INDEX_LOGGING | X | O | O | O | X |
| DEFAULT_INDEX_PCTFREE | X | X | O | O | O |
| DEFAULT_INITRANS | O | O | O | O | O |
| DEFAULT_MAXTRANS | O | O | O | O | O |
| DEFAULT_PCTFREE | O | O | O | O | O |
| DEFAULT_PCTUSED | O | O | O | O | O |
| DEFAULT_REMOVAL_BACKUP_FILE | X | O | O | O | O |
| DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST | X | O | O | O | O |
| DEFAULT_SHARDING | X | X | O | O | O |
| DISABLE_DDL_CDC_GIVEUP | X | O | O | O | O |
| DISABLE_UPDATE_PK_CDC_GIVEUP | X | O | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE | X | X | O | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL | X | X | X | O | O |
| DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME | X | X | O | O | O |
| DISPATCHERS | X | O | O | O | O |
| DISPATCHER_CM_BUFFER_SIZE | X | O | O | O | O |
| DISPATCHER_CM_UNIT_SIZE | X | O | O | O | O |
| DISPATCHER_CONNECTIONS | X | O | O | O | O |
| DISPATCHER_HOT_POLICY_INTERVAL | X | X | O | O | O |
| DISPATCHER_LOAD_BALANCING | X | X | O | O | O |
| DISPATCHER_NUMA_STREAM_MAP | X | X | O | O | O |
| DISPATCHER_QUEUE_SIZE | X | O | O | O | O |
| DISPATCHER_REQUEST_MINI_QUEUE_COUNT | X | X | O | O | O |
| DISPATCHER_RESPONSE_MINI_QUEUE_COUNT | X | X | O | O | O |
| FETCH_FAILOVER | X | X | O | O | O |
| GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY | X | X | X | O | O |
| GLOBAL_JOURNAL_BUFFER_SIZE | X | X | O | O | O |
| GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE | X | X | O | O | O |
| GLOBAL_PROPERTY_LOCK_TIMEOUT | X | X | O | O | O |
| GLOBAL_TRANSACTION_COMMIT_WRITE_MODE | X | X | O | O | O |
| GLOBAL_TRANSACTION_ISOLATION_SCOPE | X | X | O | O | O |
| GLOBAL_TRANSACTION_LOG_DIR | X | X | O | O | O |
| GLOBAL_TRANSACTION_LOG_FILE_SIZE | X | X | O | O | O |
| GMASTER_NUMA_NODE | X | X | O | O | O |
| GMON_AUTOSTART | X | X | O | O | O |
| HINT_ERROR | X | O | O | O | O |
| IDLE_TIMEOUT | O | O | O | O | O |
| IN_DOUBT_DECISION | X | O | O | O | O |
| IN_KEY_RANGE_ARRAY_COUNT | X | X | X | X | O |
| INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE | X | X | X | X | O |
| INDEX_BUILD_PARALLEL_FACTOR | X | O | O | O | O |
| INDEX_REBUILD_BLOCK_READ_COUNT | X | X | X | X | O |
| INDEX_TREE_MERGE_PARALLEL_FACTOR | X | X | O | O | O |
| INST_ALLOCATOR_COUNT | X | X | O | O | O |
| INST_TABLE_BLOCK_SIZE | X | X | O | O | O |
| JOURNAL_TEMP_DIR | X | X | O | O | O |
| KEEPALIVE_IDLE_TIME | X | O | O | O | O |
| LOCAL_CLUSTER_MEMBER | X | X | O | O | O |
| LOCAL_CLUSTER_MEMBER_HOST | X | X | O | O | O |
| LOCAL_CLUSTER_MEMBER_PORT | X | X | O | O | O |
| LOCAL_JOURNAL_BUFFER_SIZE | X | X | O | O | O |
| LOCATION_FILE | X | X | O | O | O |
| LOCATOR_QUERY_TIMEOUT | X | X | O | O | O |
| LOCK_HASH_TABLE_SIZE | X | O | O | O | O |
| LOCKLESS_CSERVERS | X | X | X | X | O |
| LOG_BLOCK_SIZE | O | O | O | O | O |
| LOG_BUFFER_SIZE | O | O | O | O | O |
| LOG_DIR | O | O | O | O | O |
| LOG_FILE_SIZE | O | O | O | O | O |
| LOG_GROUP_COUNT | O | O | O | O | O |
| LOG_MIRROR_MODE | X | O | O | O | O |
| LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE | X | O | O | O | O |
| LOG_MIRROR_TIMEOUT | X | O | O | O | O |
| LOG_SYNC_INTERVAL | X | O | O | O | O |
| LOG_SYNC_INTERVAL_MSEC | X | X | O | O | O |
| MAX_GROUP_COUNT | X | X | O | O | O |
| MAX_JOURNAL_FILE_SIZE | X | X | O | O | O |
| MAX_NODE_COUNT | X | X | O | O | O |
| MAXIMUM_CONCURRENT_ACTIVITIES | X | O | O | O | O |
| MAXIMUM_FLANGE_COUNT | X | X | O | O | O |
| MAXIMUM_FLUSH_LOG_BLOCK_COUNT | O | O | O | O | O |
| MAXIMUM_FLUSH_PAGE_COUNT | O | O | O | O | O |
| MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT | X | X | X | X | O |
| MAXIMUM_JOURNAL_REPLAY_COUNT | X | X | X | O | O |
| MAXIMUM_NAMED_CURSOR_COUNT | X | O | O | O | O |
| MAXIMUM_SESSION_CM_BUFFER_SIZE | X | O | O | O | O |
| MEASURE_CLUSTER_LATENCY | X | X | O | O | O |
| MEDIA_RECOVERY_LOG_BUFFER_SIZE | X | O | X | X | X |
| MEMORY_MERGE_RUN_COUNT | X | O | O | O | O |
| MEMORY_SORT_RUN_SIZE | X | O | O | O | O |
| MIN_SAMPLE_ROW_COUNT | X | X | O | O | O |
| MINIMUM_UNDO_PAGE_COUNT | O | O | O | O | O |
| NET_BUFFER_SIZE | X | O | O | O | O |
| NLS_DATE_FORMAT | X | O | O | O | O |
| NLS_TIME_FORMAT | X | O | O | O | O |
| NLS_TIME_WITH_TIME_ZONE_FORMAT | X | O | O | O | O |
| NLS_TIMESTAMP_FORMAT | X | O | O | O | O |
| NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT | X | O | O | O | O |
| NUMA | X | X | O | O | O |
| NUMA_MAP | X | X | O | O | O |
| OFFLINE_MEMBER_AFTER_FAILOVER | X | X | O | O | O |
| ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD | X | X | X | X | O |
| ONLINE_JOURNAL_REPLAY_THRESHOLD | X | X | X | O | O |
| OS_GROUP_ACCESS | X | X | O | O | O |
| PACKET_COMPRESSION_THRESHOLD | X | X | X | X | O |
| PAGE_CHECKSUM_TYPE | X | O | O | O | O |
| PARALLEL_IO_FACTOR | O | O | O | O | O |
| PARALLEL_IO_GROUP_1 ~ GROUP_16 | O | O | O | O | O |
| PARALLEL_LOAD_FACTOR | O | O | O | O | O |
| PENDING_LOG_BUFFER_COUNT | O | O | O | O | O |
| PLAN_CACHE | X | O | O | O | O |
| PLAN_CACHE_SIZE | X | O | O | O | O |
| PRIVATE_STATIC_AREA_INIT_SIZE | X | X | X | X | O |
| PRIVATE_STATIC_AREA_NEXT_SIZE | X | X | X | X | O |
| PRIVATE_STATIC_AREA_SHRINK_THRESHOLD | X | X | X | X | O |
| PRIVATE_STATIC_AREA_SIZE | X | O | O | O | O |
| PROCESS_MAX_COUNT | O | O | O | O | O |
| QUERY_TIMEOUT | O | O | O | O | O |
| READABLE_ARCHIVELOG_DIR_COUNT | X | O | O | O | O |
| READABLE_BACKUP_DIR_COUNT | X | O | O | O | O |
| REBALANCE_BLOCK_READ_COUNT | X | X | O | O | O |
| RECOMPILE_CHECK_MINIMUM_PAGE_COUNT | X | O | O | X | X |
| RECOMPILE_PAGE_PERCENT | X | O | O | X | X |
| RECOVERY_LOG_BUFFER_SIZE | X | X | O | O | O |
| RECYCLEBIN | X | X | X | X | O |
| REDO_LOG_COMPRESSION_THRESHOLD | X | X | X | O | O |
| REFINE_RELATION | X | O | O | O | O |
| SESSION_FATAL_BEHAVIOR | X | O | O | O | O |
| SESSION_MEMORY_INIT_SIZE | X | X | X | O | O |
| SESSION_MEMORY_SHRINK_THRESHOLD | X | X | X | O | O |
| SHARED_MEMORY_ADDRESS | O | O | O | O | O |
| SHARED_MEMORY_STATIC_KEY | O | O | O | O | O |
| SHARED_MEMORY_STATIC_NAME | O | O | O | O | O |
| SHARED_MEMORY_STATIC_SIZE | O | O | O | O | O |
| SHARED_REQUEST_QUEUE_COUNT | X | O | O | O | O |
| SHARED_SERVERS | X | O | O | O | O |
| SHARED_SESSION | X | O | O | O | O |
| SNAPSHOT_STATEMENT_TIMEOUT | X | O | O | O | O |
| SQL_HISTORY_SIZE | X | X | O | O | O |
| SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY | X | O | O | O | O |
| SYSTEM_DISK_DATA_TABLESPACE_SIZE | X | X | X | X | O |
| SYSTEM_FILE_IO | X | O | O | O | O |
| SYSTEM_LOGGER_DIR | X | O | O | O | O |
| SYSTEM_MEMORY_AUX_TABLESPACE_SIZE | X | X | X | O | O |
| SYSTEM_MEMORY_DATA_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_DICT_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE | O | O | O | O | O |
| SYSTEM_TABLESPACE_DIR | O | O | O | O | O |
| SYSTEM_UDS_DIR | X | X | O | O | O |
| TCP_NODELAY | X | X | O | O | O |
| TEMP_SEGMENT_CACHE_SIZE | X | X | X | O | O |
| TEMP_UNDO_ENABLED | X | X | X | O | O |
| TIMED_STATISTICS | X | X | O | O | O |
| TIMER_INTERVAL | O | O | X | X | X |
| TIMEZONE | X | O | O | O | O |
| TRACE_ALTER_SYSTEM | X | O | O | O | O |
| TRACE_DDL | O | O | O | O | O |
| TRACE_LOG_ID | X | O | O | O | O |
| TRACE_LOG_MSGBUG_SIZE | X | X | O | O | O |
| TRACE_LOG_TIME_DETAIL | X | O | O | O | O |
| TRACE_LOGGER | X | X | O | O | O |
| TRACE_LOGGER_REMOTE_HOST | X | X | O | O | O |
| TRACE_LOGGER_REMOTE_PORT | X | X | O | O | O |
| TRACE_LOGIN | X | O | O | O | O |
| TRACE_LONG_RUN_CURSOR | X | O | O | O | O |
| TRACE_LONG_RUN_SQL | X | O | O | O | O |
| TRACE_LONG_RUN_TIMER | X | X | X | X | O |
| TRACE_XA | X | O | O | O | O |
| TRANSACTION_ALLOCATION_TIMEOUT | X | X | X | O | O |
| TRANSACTION_COMMIT_WRITE_MODE | O | O | O | O | O |
| TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT | X | O | O | O | O |
| TRANSACTION_TABLE_SIZE | O | O | O | O | O |
| TRANSACTION_TIMEOUT | X | X | O | O | O |
| UNDO_RELATION_ALLOCATION_TIMEOUT | X | X | X | O | O |
| UNDO_RELATION_COUNT | O | O | O | O | O |
| UNDO_SHRINK_THRESHOLD | X | O | O | O | O |
| USE_LARGE_PAGES | X | X | X | X | O |
| USER_DATA_TABLESPACE_MEDIA_TYPE | X | X | X | X | O |
| USER_DATA_TABLESPACE_SIZE | X | X | X | X | O |
| USER_DISK_DATA_TABLESPACE_NEXTSIZE | X | X | X | X | O |
| USER_TEMP_TABLESPACE_SIZE | O | O | O | O | O |
| XA_TRANSACTION_IDLE_TIMEOUT | X | X | X | X | O |

<a id="10f001d9e378b132"></a>
### SQL

<a id="0c67e60ad89cefef"></a>
#### SQL Element

<a id="2151595b1e079567"></a>
##### Data Type

The following is a feature matrix for data type.

<a id="f41186aa48a59b5e"></a>
<table class="table column_count_7"><caption>Feature matrix for data type</caption><thead><tr><th class="to_center"><div>Type</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>Character string type</div></td><td><div>CHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARCHAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Binary string type</div></td><td><div>BINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>VARBINARY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LONG VARBINARY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Decimal number type</div></td><td><div>SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMERIC</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DECIMAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NUMBER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DOUBLE PRECISION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLOAT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Binary number type</div></td><td><div>NATIVE_SMALLINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_INTEGER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_BIGINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_REAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NATIVE_DOUBLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>BOOLEAN type</div></td><td><div>BOOLEAN</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Date/ time type</div></td><td><div>DATE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIME WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>INTERVAL type</div></td><td><div>INTERVAL YEAR TO MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MONTH</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ROWID type</div></td><td><div>ROWID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="05aa54f961bf0888"></a>
##### Function

The following is a feature matrix for function.

**Feature matrix for function**

<a id="328642a00f2ca833"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| expr1 * expr2 | O | O | O | O | O |
| expr1 + expr2 | O | O | O | O | O |
| datetime + interval | X | O | O | O | O |
| ＋ expr | O | O | O | O | O |
| expr1 - expr2 | O | O | O | O | O |
| datetime - interval | X | O | O | O | O |
| - expr | O | O | O | O | O |
| expr1 / expr2 | O | O | O | O | O |
| str1 \|\| str2 | O | O | O | O | O |
| expr &lt;comp&gt; expr | O | O | O | O | O |
| expr &lt;comp&gt; ( subquery ) | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; expr | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( subquery ) | X | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( expr, ... ) | X | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; ( subquery ) | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; ( expr, ... ) | X | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | X | O | O | O | O |
| expr &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr, ... ) | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | X | O | O | O | O |
| ( expr, ... ) &lt;comp&gt; {ALL\|ANY\|SOME} ( subquery ) | X | O | O | O | O |
| ( subquery ) &lt;comp&gt; {ALL\|ANY\|SOME} ( expr_list, ... ) | X | O | O | O | O |
| ABS( num ) | O | O | O | O | O |
| ACOS( num ) | O | O | O | O | O |
| ADDDATE( date, interval ) | X | O | O | O | O |
| ADDDATE( expr, days ) | X | O | O | O | O |
| ADDTIME( expr1, expr2 ) | X | O | O | O | O |
| ADD_MONTHS( date, number ) | X | O | O | O | O |
| AND | O | O | O | O | O |
| ASCII( char ) | X | X | O | O | O |
| ASIN( num ) | O | O | O | O | O |
| ATAN( num ) | O | O | O | O | O |
| ATAN2( num1, num2 ) | O | O | O | O | O |
| AVG( num ) | X | O | O | O | O |
| expr1 [NOT] BETWEEN [ASYMMETRIC\|SYMMETRIC] expr2 AND expr3 | X | O | O | O | O |
| BITAND( num1, num2 ) | O | O | O | O | O |
| BITNOT( num ) | O | O | O | O | O |
| BITOR( num1, num2 ) | O | O | O | O | O |
| BITXOR( num1, num2 ) | O | O | O | O | O |
| BIT_LENGTH( str ) | O | O | O | O | O |
| BYTE_LENGTH( str ) | O | O | O | O | O |
| CASE .. WHEN .. THEN .. ELSE .. END | X | O | O | O | O |
| CASE2( condition, result, ... ) | X | O | O | O | O |
| CAST( expr AS datatype ) | O | O | O | O | O |
| CBRT( num ) | O | O | O | O | O |
| CEIL( num ) | O | O | O | O | O |
| CEILING( num ) | O | O | O | O | O |
| CHAR_LENGTH( str ) | O | O | O | O | O |
| CHARACTER_LENGTH( str ) | O | O | O | O | O |
| CHR( num ) | X | X | O | O | O |
| CLOCK_DATE() | O | O | O | O | O |
| CLOCK_LOCALTIME() | O | O | O | O | O |
| CLOCK_LOCALTIMESTAMP() | O | O | O | O | O |
| CLOCK_TIME() | O | O | O | O | O |
| CLOCK_TIMESTAMP() | O | O | O | O | O |
| COALESCE( expr1, ..., exprN ) | X | O | O | O | O |
| CONCAT( str1, str2 ) | O | O | O | O | O |
| CONCATENATE( str1, str2 ) | O | O | O | O | O |
| COS( num ) | O | O | O | O | O |
| COT( num ) | O | O | O | O | O |
| COUNT( expr ) | X | O | O | O | O |
| COUNT(*) | X | O | O | O | O |
| CURRENT_CATALOG | O | O | O | O | O |
| CURRENT_DATE | O | O | O | O | O |
| CURRENT_SCHEMA | O | O | O | O | O |
| CURRENT_TIME | O | O | O | O | O |
| CURRENT_TIMESTAMP | O | O | O | O | O |
| CURRENT_USER | O | O | O | O | O |
| seq.CURRVAL | O | O | O | O | O |
| CURRVAL( seq ) | O | O | O | O | O |
| DATEADD( datepart, number, date ) | O | O | O | O | O |
| DATEDIFF( datepart, startdate, enddate ) | X | O | O | O | O |
| DATE_ADD( date, interval ) | X | O | O | O | O |
| DATE_PART( field, datetime ) | X | O | O | O | O |
| DECODE( expr, comparison, result, ... ) | X | O | O | O | O |
| DEGREES( radians ) | O | O | O | O | O |
| DIGEST ( data, type ) | X | X | O | O | O |
| DUMP( expr ) | X | O | O | O | O |
| EXISTS( subquery ) | X | O | O | O | O |
| EXP( num ) | O | O | O | O | O |
| EXTRACT( field FROM datetime ) | X | O | O | O | O |
| FACTORIAL( num ) | O | O | O | O | O |
| FLOOR( num ) | O | O | O | O | O |
| FROM_BASE64( str ) | X | X | O | O | O |
| GREATEST( expr, ... ) | X | O | O | O | O |
| HEX( str ) | X | X | O | O | O |
| expr1 [NOT] IN ( expr, ... ) | X | O | O | O | O |
| expr1 [NOT] IN ( subquery ) | X | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt; ) | X | O | O | O | O |
| subquery [NOT] IN ( subquery ) | X | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( &lt;expr_list&gt;, ... ) | X | O | O | O | O |
| &lt;expr_list&gt; [NOT] IN ( subquery ) | X | O | O | O | O |
| subquery [NOT] IN ( &lt;expr_list&gt;, ... ) | X | O | O | O | O |
| INITCAP( str ) | X | O | O | O | O |
| INSTR( str, substr, ... ) | X | O | O | O | O |
| IS NOT NULL | O | O | O | O | O |
| IS NULL | O | O | O | O | O |
| LAST_DAY( date ) | X | O | O | O | O |
| LAST_IDENTITY_VALUE() | X | X | O | O | O |
| LEAST( expr, ... ) | X | O | O | O | O |
| LENGTH( str ) | O | O | O | O | O |
| LENGTHB( str ) | O | O | O | O | O |
| string [NOT] LIKE pattern ESCAPE escape_char | X | O | O | O | O |
| LN( num ) | O | O | O | O | O |
| LNNVL( expr ) | X | X | X | X | O |
| LOCALTIME | O | O | O | O | O |
| LOCALTIMESTAMP | O | O | O | O | O |
| LOCAL_GROUP_ID() | X | X | O | O | O |
| LOCAL_GROUP_NAME() | X | X | O | O | O |
| LOCAL_MEMBER_ID() | X | X | O | O | O |
| LOCAL_MEMBER_NAME() | X | X | O | O | O |
| LOG( num2 ) | O | O | O | O | O |
| LOG( num1, num2 ) | O | O | O | O | O |
| LOGON_USER() | X | O | O | O | O |
| LOWER( str ) | O | O | O | O | O |
| LPAD( str, length, fill ) | X | O | O | O | O |
| LTRIM( str, [ str ] ) | X | O | O | O | O |
| MAX( expr ) | X | O | O | O | O |
| MIN( expr ) | X | O | O | O | O |
| MOD( num1, num2 ) | O | O | O | O | O |
| MONTHS_BETWEEN( date1, date2 ) | X | X | X | O | O |
| NEXT_DAY( date, day ) | X | X | O | O | O |
| seq.NEXTVAL | O | O | O | O | O |
| NEXTVAL( seq ) | O | O | O | O | O |
| NEXT VALUE FOR seq | O | O | O | O | O |
| NOT | X | O | O | O | O |
| NULLIF( expr1, expr2 ) | X | O | O | O | O |
| NUMTODSINTERVAL( num, interval_indicator ) | X | X | X | X | O |
| NUMTODSINTERVAL( num, interval_indicator ) | X | X | X | X | O |
| NVL( expr1, expr2 ) | X | O | O | O | O |
| NVL2( expr1, expr2, expr3 ) | X | O | O | O | O |
| OCTET_LENGTH( str ) | O | O | O | O | O |
| OVERLAY( str1 PLACING str2 FROM start FOR length ) | X | O | O | O | O |
| OR | X | O | O | O | O |
| PHYSICAL_LENGTH( expr ) | X | X | X | X | O |
| PI() | O | O | O | O | O |
| POSITION( str1 IN str2 ) | O | O | O | O | O |
| POWER( num1, num2 ) | O | O | O | O | O |
| RADIANS( degrees ) | O | O | O | O | O |
| RANDOM( min, max ) | O | O | O | O | O |
| REPEAT( str, num ) | X | O | O | O | O |
| REPLACE( str, from, to ) | X | O | O | O | O |
| REVERSE( str ) | X | X | X | O | O |
| ROUND( num ) | X | O | O | O | O |
| ROUND( date, fmt ) | X | O | O | O | O |
| ROWID_GRID_BLOCK_ID( rowid ) | X | X | O | O | O |
| ROWID_GRID_BLOCK_SEQ( rowid ) | X | X | O | O | O |
| ROWID_MEMBER_ID( rowid ) | X | X | O | O | O |
| ROWID_OBJECT_ID( rowid ) | X | O | O | O | O |
| ROWID_PAGE_ID( rowid ) | X | O | O | O | O |
| ROWID_ROW_NUMBER( rowid ) | X | O | O | O | O |
| ROWID_SHARD_ID( rowid ) | X | X | O | O | O |
| ROWID_TABLESPACE_ID( rowid ) | X | O | O | O | O |
| ROWNUM | X | X | O | O | O |
| RPAD( str, length, fill ) | X | O | O | O | O |
| RTRIM( str, [ str ] ) | X | O | O | O | O |
| SESSION_ID() | X | O | O | O | O |
| SESSION_SERIAL() | X | O | O | O | O |
| SESSION_USER | X | O | O | O | O |
| SHARD_GROUP_ID( table, expr ) | X | X | O | O | O |
| SHARD_GROUP_NAME( table_name, shard_key_value [, ...] ) | X | X | O | O | O |
| SHARD_ID( table, expr ) | X | X | O | O | O |
| SHARD_NAME( table_name, shard_key_value [, ...] ) | X | X | O | O | O |
| SHIFT_LEFT( num, cnt ) | O | O | O | O | O |
| SHIFT_RIGHT( num, cnt ) | O | O | O | O | O |
| SIGN( num ) | O | O | O | O | O |
| SIN( num ) | O | O | O | O | O |
| SPLIT_PART( str, delimiter, field ) | X | O | O | O | O |
| SQRT( num ) | O | O | O | O | O |
| STATEMENT_DATE() | O | O | O | O | O |
| STATEMENT_LOCALTIME() | O | O | O | O | O |
| STATEMENT_LOCALTIMESTAMP() | O | O | O | O | O |
| STATEMENT_TIME() | O | O | O | O | O |
| STATEMENT_TIMESTAMP() | O | O | O | O | O |
| STATEMENT_VIEW_SCN() | X | O | O | O | O |
| STATEMENT_VIEW_SCN_DCN() | X | X | O | O | O |
| STATEMENT_VIEW_SCN_GCN() | X | X | O | O | O |
| STATEMENT_VIEW_SCN_LCN() | X | X | O | O | O |
| STDDEV( [ ALL \| DISTINCT ] expr ) | X | X | X | O | O |
| STDDEV_POP( expr ) | X | X | X | O | O |
| STDDEV_SAMP( expr ) | X | X | X | O | O |
| SUBSTR( str FROM start FOR length ) | X | O | O | O | O |
| SUBSTR( str, start, length ) | X | O | O | O | O |
| SUBSTRB( str, start, length ) | X | O | O | O | O |
| SUBSTRING( str FROM start FOR length ) | X | O | O | O | O |
| SUBSTRING( str, start, length ) | X | O | O | O | O |
| SUM( expr ) | X | O | O | O | O |
| SYSDATE | O | O | O | O | O |
| SYS_EXTRACT_UTC( datetime_with_timezone ) | X | X | O | O | O |
| SYSTIME | O | O | O | O | O |
| SYSTIMESTAMP | O | O | O | O | O |
| TAN( num ) | O | O | O | O | O |
| TO_CHAR( datetime, fmt ) | X | O | O | O | O |
| TO_CHAR( number, fmt ) | X | O | O | O | O |
| TO_BASE64( str ) | X | X | O | O | O |
| TO_DATE( str, fmt ) | X | O | O | O | O |
| TO_NATIVE_BIGNIT( str, fmt ) | X | X | X | X | O |
| TO_NATIVE_DOUBLE( str, fmt ) | X | O | O | O | O |
| TO_NATIVE_INTEGER( str, fmt ) | X | X | X | X | O |
| TO_NATIVE_REAL( str, fmt ) | X | O | O | O | O |
| TO_NATIVE_SMALLINT( str, fmt ) | X | X | X | X | O |
| TO_NUMBER( num, fmt ) | X | O | O | O | O |
| TO_TIME( str, fmt ) | X | O | O | O | O |
| TO_TIME_TZ( str, fmt ) | X | O | O | O | O |
| TO_TIME_WITH_TIME_ZONE( str, fmt ) | X | O | O | O | O |
| TO_TIMESTAMP( str, fmt ) | X | O | O | O | O |
| TO_TIMESTAMP_TZ( str, fmt ) | X | O | O | O | O |
| TO_TIMESTAMP_WITH_TIME_ZONE( str, fmt ) | X | O | O | O | O |
| TRANSACTION_DATE() | O | O | O | O | O |
| TRANSACTION_LOCALTIME() | O | O | O | O | O |
| TRANSACTION_LOCALTIMESTAMP() | O | O | O | O | O |
| TRANSACTION_TIME() | O | O | O | O | O |
| TRANSACTION_TIMESTAMP() | O | O | O | O | O |
| TRANSLATE( str, from, to ) | X | O | O | O | O |
| TRIM( LEADING\|TRAILING\|BOTH trim_char FROM source ) | O | O | O | O | O |
| TRUNC( num, scale ) | X | O | O | O | O |
| TRUNC( date, fmt ) | X | O | O | O | O |
| UPPER( str ) | O | O | O | O | O |
| UNHEX( str ) | X | X | O | O | O |
| UNHEX_TO_CHARSTR( str ) | X | X | O | O | O |
| USER_ID() | O | O | O | O | O |
| UUID() | X | X | O | O | O |
| VAR_POP( expr ) | X | X | X | O | O |
| VAR_SAMP( expr ) | X | X | X | O | O |
| VARIANCE( [ ALL \| DISTINCT ] expr ) | X | X | X | O | O |
| VERSION() | O | O | O | O | O |
| WIDTH_BUCKET( num, min, max, cnt ) | O | O | O | O | O |

<a id="f38087fd4e1c528d"></a>
#### Object

<a id="3305437838c2cc81"></a>
##### SQL Object

The following is a feature matrix for DDL which creates/ drops/ alters an SQL object.

<a id="c8db0e333733e286"></a>
<table class="table column_count_7"><caption>Feature matrix for SQL object DDL</caption><thead><tr><th class="to_center"><div>Object</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="11"><div>Database 
object</div></td><td><div>ALTER DATABASE ARCHIVELOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE ADD LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE DROP LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RENAME LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RECOVER TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE REGISTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER DATABASE RESTORE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE SYSTEM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMENT ON object IS ..</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Profile 
object</div></td><td><div>CREATE PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Audit policy 
object</div></td><td><div>CREATE AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>AUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>NOAUDIT POLICY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Authorization 
object</div></td><td><div>CREATE USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER USER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GRANT privileges TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>REVOKE privileges FROM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Schema 
object</div></td><td><div>CREATE SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SCHEMA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="9"><div>Tablespace 
object</div></td><td><div>CREATE MEMORY DATA TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE MEMORY TEMPORARY TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLESPACE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. BEGIN/END BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. ADD [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLESPACE .. DROP [DATAFILE|MEMORY]</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. RENAME DATAFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLESPACE .. { ONLINE | OFFLINE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="24"><div>Table 
object</div></td><td><div>CREATE TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE GLOBAL TEMPORARY TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CREATE GLOBAL TEMPORARY TABLE AS SELECT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE IMMUTABLE TABLE AS SELECT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP TABLE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRUNCATE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME TO</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. SET UNUSED COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME COLUMN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. RENAME CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ALTER CONSTRAINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. ADD SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. DROP SUPPLEMENTAL LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER TABLE .. READ { ONLY | WRITE }</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ANALYZE TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>FLASHBACK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PURGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>View 
object</div></td><td><div>CREATE VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER VIEW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>Index 
object</div></td><td><div>CREATE INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP INDEX</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. AGING</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. STORAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. RENAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER INDEX .. REBUILD</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Sequence 
object</div></td><td><div>CREATE SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SEQUENCE</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SEQUENCE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Synonym 
object</div></td><td><div>CREATE SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PUBLIC SYNONYM</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored procedure 
object</div></td><td><div>CREATE PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PROCEDURE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Stored function 
object</div></td><td><div>CREATE FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER FUNCTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Package object</div></td><td><div>CREATE PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CREATE PACKAGE BODY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DROP PACKAGE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="4388452b3a22a670"></a>
##### Cluster Object

The following is a feature matrix for DDL which creates/ drops/ alters a cluster object.

<a id="bf8baea2437d63ce"></a>
<table class="table column_count_7"><caption>Feature matrix for cluster object DDL </caption><thead><tr><th class="to_center to_middle"><div>Object</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>1.x</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.1</div></th><th class="to_center to_middle"><div>3.2</div></th><th class="to_center to_middle"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>Cluster system 
object</div></td><td class="to_middle"><div>ALTER DATABASE REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>Cluster group 
object</div></td><td class="to_middle"><div>CREATE CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER GROUP</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster member 
object</div></td><td class="to_middle"><div>ALTER CLUSTER GROUP name ADD MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER GROUP name OFFLINE MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER DATABASE RESET LOCAL CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM JOIN DATABASE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>Cluster location 
object</div></td><td class="to_middle"><div>CREATE CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DROP CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER CLUSTER LOCATION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Cluster table and shard object</div></td><td class="to_middle"><div>ALTER TABLE name REBALANCE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER TABLE name MERGE SHARDS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name MOVE SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name SPLIT SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name RENAME SHARD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Global secondary index
object</div></td><td class="to_middle"><div>ALTER TABLE name ADD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name DROP GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name ALTER GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="21c62ec9a8f6da40"></a>
#### SQL Language

<a id="8383dda83de0b6bf"></a>
##### DML

The following is a feature matrix for DML which manipulates data.

**Feature matrix for DML**

<a id="83c8d6a07a0a1009"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| INSERT INTO .. | O | O | O | O | O |
| INSERT INTO .. RETURNING query | X | O | O | O | O |
| INSERT INTO .. RETURNING .. INTO .. | X | O | O | O | O |
| DELETE FROM .. | O | O | O | O | O |
| DELETE FROM .. RETURNING query | X | O | O | O | O |
| DELETE FROM .. RETURNING .. INTO .. | X | O | O | O | O |
| DELETE FROM .. WHERE CURRENT OF cursor | X | O | O | O | O |
| UPDATE .. | O | O | O | O | O |
| UPDATE .. RETURNING query | X | O | O | O | O |
| UPDATE .. RETURNING .. INTO .. | X | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | X | O | O | O | O |
| CALL proc_name | X | X | O | O | O |

<a id="a2692b6ee04ce7a0"></a>
##### Query

The following is a feature matrix for SELECT statement which enquires data.

**Feature matrix for SELECT**

<a id="b543e1692f433738"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| &lt;query expression&gt; | O | O | O | O | O |
| &lt;query specification&gt; | O | O | O | O | O |
| &lt;select list&gt; | O | O | O | O | O |
| &lt;from clause&gt; | O | O | O | O | O |
| &lt;joined table&gt; | X | O | O | O | O |
| &lt;where clause&gt; | O | O | O | O | O |
| &lt;group by clause&gt; | X | O | O | O | O |
| &lt;order by clause&gt; | X | O | O | O | O |
| &lt;offset limit clause&gt; | O | O | O | O | O |
| &lt;set operator&gt; | X | O | O | O | O |
| &lt;subquery&gt; | X | O | O | O | O |
| &lt;hint clause&gt; | X | O | O | O | O |

<a id="5d552548fe853265"></a>
##### Control Language

The following is a feature matrix for control statement.

<a id="8c13ca857fcd4eeb"></a>
<table class="table column_count_7"><caption>Feature matrix for control statement</caption><thead><tr><th class="to_center to_middle"><div>Control statement</div></th><th class="to_center to_middle"><div>Feature</div></th><th class="to_center to_middle"><div>1.x</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.1</div></th><th class="to_center to_middle"><div>3.2</div></th><th class="to_center to_middle"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>Transaction</div></td><td><div>COMMIT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ROLLBACK</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>RELEASE SAVEPOINT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOCK TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET CONSTRAINTS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TRANSACTION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Session</div></td><td><div>SET SESSION CHARACTERISTICS AS</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET SESSION AUTHORIZATION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SET TIME ZONE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SESSION SET property</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>System</div></td><td><div>ALTER SYSTEM {OPEN|MOUNT} DATABASE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM CHECKPOINT</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM KILL SESSION</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>ALTER SYSTEM RECONNECT GLOBAL CONNECTION</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SWITCH LOGFILE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM SET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ALTER SYSTEM RESET property</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="2c7bf7d108326e9a"></a>
#### PSM Language

The following is a feature matrix for Persistent Stored Module (PSM) language element.

**Feature matrix for Persistent Stored Module (PSM) language element**

<a id="2c313fae77626dab"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| Assignment Statement | X | X | O | O | O |
| Basic LOOP Statement | X | X | O | O | O |
| Block (BEGIN .. END) | X | X | O | O | O |
| CASE Statement | X | X | O | O | O |
| CLOSE Statement | X | X | O | O | O |
| Collection Method Invocation | X | X | O | O | O |
| Collection Variable Declaration | X | X | O | O | O |
| CONTINUE Statement | X | X | O | O | O |
| Cursor FOR LOOP Statement | X | X | O | O | O |
| Cursor Variable Declaration | X | X | O | O | O |
| DELETE Statement Extension | X | X | O | O | O |
| EXCEPTION_INIT Pragma | X | X | O | O | O |
| Exception Declaration | X | X | O | O | O |
| Exception Handler | X | X | O | O | O |
| EXECUTE IMMEDIATE Statement | X | X | O | O | O |
| EXIT Statement | X | X | O | O | O |
| Explicit Cursor Declaration and Definition | X | X | O | O | O |
| FETCH Statement | X | X | O | O | O |
| FOR LOOP Statement | X | X | O | O | O |
| GOTO Statement | X | X | O | O | O |
| IF Statement | X | X | O | O | O |
| Implicit Cursor Attribute | X | X | O | O | O |
| INSERT Statement Extension | X | X | O | O | O |
| Named Cursor Attribute | X | X | O | O | O |
| NULL Statement | X | X | O | O | O |
| OPEN Statement | X | X | O | O | O |
| OPEN FOR Statement | X | X | O | O | O |
| Procedure Call | X | X | O | O | O |
| Procedure Declaration and Definition | X | X | O | O | O |
| RAISE Statement | X | X | O | O | O |
| Record Variable Declaration | X | X | O | O | O |
| RETURN Statement | X | X | O | O | O |
| RETURNING INTO clause | X | X | O | O | O |
| %ROWTYPE Attribute | X | X | O | O | O |
| Scalar Variable Declaration | X | X | O | O | O |
| SELECT INTO Statement | X | X | O | O | O |
| SQLCODE Function | X | X | O | O | O |
| SQLERRM Function | X | X | O | O | O |
| %TYPE Attribute | X | X | O | O | O |
| UPDATE Statement Extension | X | X | O | O | O |
| WHILE LOOP Statement | X | X | O | O | O |

The following is a feature matrix for the Built-In Package.

<a id="fe2777e2d7639b65"></a>
<table class="table column_count_7"><caption>Feature matrix for Built-in Package</caption><thead><tr><th class="to_center to_middle"><div>Package</div></th><th class="to_center to_middle"><div>Sub Routine</div></th><th class="to_center to_middle"><div>1.x</div></th><th class="to_center to_middle"><div>2.x</div></th><th class="to_center to_middle"><div>3.1</div></th><th class="to_center to_middle"><div>3.2</div></th><th class="to_center to_middle"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DBMS_LOCK</div></td><td class="to_middle"><div>SLEEP()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="7"><div>DBMS_OUTPUT</div></td><td class="to_middle"><div>DISABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>ENABLE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>GET_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>NEW_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td><div>PUT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td><div>PUT_LINE()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td><div>SET_LOG()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DBMS_SQL</div></td><td class="to_middle"><div>RETURN_RESULT()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>DBMS_STANDARD</div></td><td><div>RAISE_APPLICATION_ERROR()</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="ae1362c606a9cc37"></a>
### API

<a id="d739ba04f25e8286"></a>
#### ODBC

The following is a feature matrix for the ODBC standard API.

**Feature matrix for the ODBC standard API**

<a id="85f11061283c4f14"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| SQLAllocHandle() | O | O | O | O | O |
| SQLBindCol() | O | O | O | O | O |
| SQLBindParameter() | O | O | O | O | O |
| SQLCloseCursor() | O | O | O | O | O |
| SQLColAttribute() | X | O | O | O | O |
| SQLColumnPrivileges() | X | O | O | O | O |
| SQLColumns() | X | O | O | O | O |
| SQLConnect() | O | O | O | O | O |
| SQLDescribeCol() | O | O | O | O | O |
| SQLDescribeParam() | O | O | O | O | O |
| SQLDisconnect() | O | O | O | O | O |
| SQLDriverConnect() | X | O | O | O | O |
| SQLEndTran() | O | O | O | O | O |
| SQLExecDirect() | O | O | O | O | O |
| SQLExecute() | O | O | O | O | O |
| SQLExtendedFetch() | X | O | O | O | O |
| SQLFetch() | O | O | O | O | O |
| SQLFetchScroll() | X | O | O | O | O |
| SQLForeignKeys() | X | O | O | O | O |
| SQLFreeHandle() | O | O | O | O | O |
| SQLFreeStmt() | O | O | O | O | O |
| SQLGetConnectAttr() | O | O | O | O | O |
| SQLGetCursorName() | X | O | O | O | O |
| SQLGetData() | X | O | O | O | O |
| SQLGetDescField() | O | O | O | O | O |
| SQLGetDescRec() | O | O | O | O | O |
| SQLGetDiagField() | O | O | O | O | O |
| SQLGetDiagRec() | O | O | O | O | O |
| SQLGetEnvAttr() | O | O | O | O | O |
| SQLGetFunctions() | O | O | O | O | O |
| SQLGetInfo() | X | O | O | O | O |
| SQLGetStmtAttr() | O | O | O | O | O |
| SQLGetTypeInfo() | X | O | O | O | O |
| SQLMoreResults() | X | O | O | O | O |
| SQLNumParams() | O | O | O | O | O |
| SQLNumResultCols() | O | O | O | O | O |
| SQLParamData() | X | O | O | O | O |
| SQLPrepare() | O | O | O | O | O |
| SQLPrimaryKeys() | X | O | O | O | O |
| SQLProcedureColumns() | X | O | O | O | O |
| SQLProcedures() | X | O | O | O | O |
| SQLPutData() | X | O | O | O | O |
| SQLRowCount() | O | O | O | O | O |
| SQLSetConnectAttr() | O | O | O | O | O |
| SQLSetCursorName() | X | O | O | O | O |
| SQLSetDescField() | O | O | O | O | O |
| SQLSetDescRec() | O | O | O | O | O |
| SQLSetEnvAttr() | O | O | O | O | O |
| SQLSetPos() | X | O | O | O | O |
| SQLSetStmtAttr() | O | O | O | O | O |
| SQLSpecialColumns() | X | O | O | O | O |
| SQLStatistics() | X | O | O | O | O |
| SQLTablePrivileges() | X | O | O | O | O |
| SQLTables() | X | O | O | O | O |

The following is a feature matrix for API other than the ODBC standard API.

**Feature matrix for API other than the ODBC standard**

<a id="987c7f8ac779b2ee"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| xa_open | X | O | O | O | O |
| xa_close | X | O | O | O | O |
| xa_start | X | O | O | O | O |
| xa_end | X | O | O | O | O |
| xa_rollback | X | O | O | O | O |
| xa_prepare | X | O | O | O | O |
| xa_commit | X | O | O | O | O |
| xa_recover | X | O | O | O | O |
| xa_forget | X | O | O | O | O |
| SQLGetXaSwitch | X | O | O | O | O |
| SQLGetXaConnectionHandle | X | O | O | O | O |
| SQLGetGroupCount | X | X | X | O | O |
| SQLGetGroupIDs | X | X | X | O | O |
| SQLGetGroupName | X | X | X | O | O |
| SQLGetSuitableGroupID | X | X | X | O | O |

<a id="8b99a61ba513f4e1"></a>
#### JDBC

The following is a class feature matrix for JDBC.

**Class feature matrix for JDBC**

<a id="316a2878302ee518"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| CallableStatement | X | X | O | O | O |
| CommonDataSource | X | O | O | O | O |
| Connection | X | O | O | O | O |
| ConnectionPoolDataSource | X | O | O | O | O |
| DatabaseMetaData | X | O | O | O | O |
| DataSource | X | O | O | O | O |
| Driver | X | O | O | O | O |
| ParameterMetaData | X | O | O | O | O |
| PooledConnection | X | O | O | O | O |
| PreparedStatement | X | O | O | O | O |
| ResultSet | X | O | O | O | O |
| ResultSetMetaData | X | O | O | O | O |
| RowId | X | O | O | O | O |
| Savepoint | X | O | O | O | O |
| Statement | X | O | O | O | O |
| XAConnection | X | O | O | O | O |
| XADataSource | X | O | O | O | O |
| XAResource | X | O | O | O | O |
| GoldilocksInterval | X | O | O | O | O |
| GoldilocksTypes | X | O | O | O | O |

<a id="18ef5647b8bd1821"></a>
#### Embedded SQL

<a id="4e356b8c52bab241"></a>
##### Precompiler Option

The following is a feature matrix for precompiler option.

**Feature matrix for precompiler option**

<a id="b6981ccf13a9fcc6"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | X | O | O | O | O |
| --include-path | X | O | O | O | O |
| --no-prompt | X | O | O | O | O |
| --output | X | O | O | O | O |
| --unsafe-null | X | O | O | O | O |
| --version | X | O | O | O | O |
| --no-lineinfo | X | X | X | O | O |
| --char_map | X | X | X | O | O |
| --cumulative | X | X | X | X | O |
| --parse | X | X | X | X | O |

<a id="08b7bb1cf0d700f9"></a>
##### Embedded SQL-only Syntax

The following is a feature matrix of embedded SQL-only syntax.

**Feature matrix for embedded SQL-only syntax**

<a id="cf34468f1c8657fa"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| EXEC SQL AT | X | O | O | O | O |
| EXEC SQL ATOMIC INSERT | X | O | O | O | O |
| EXEC SQL AUTOCOMMIT | X | O | O | O | O |
| EXEC SQL BEGIN DECLARE SECTION | X | O | O | O | O |
| EXEC SQL COMMIT RELEASE | X | O | O | O | O |
| EXEC SQL CONNECT | X | O | O | O | O |
| EXEC SQL CONTEXT ALLOCATE | X | O | O | O | O |
| EXEC SQL CONTEXT FREE | X | O | O | O | O |
| EXEC SQL CONTEXT USE | X | O | O | O | O |
| EXEC SQL DISCONNECT | X | O | O | O | O |
| EXEC SQL END DECLARE SECTION | X | O | O | O | O |
| EXEC SQL FOR | X | O | O | O | O |
| EXEC SQL GET GROUPID | X | X | X | O | O |
| EXEC SQL INCLUDE | X | O | O | O | O |
| EXEC SQL INCLUDE SQLCA | X | O | O | O | O |
| EXEC SQL OPTION | X | O | O | O | O |
| EXEC SQL ROLLBACK RELEASE | X | O | O | O | O |
| EXEC SQL WHENEVER | X | O | O | O | O |

<a id="fa2dfce3b64e72f1"></a>
##### Host Variable Data Type

The following is a feature matrix for embedded SQL data type which can be used for HOST variables.

**Feature matrix for host variable data type**

<a id="5e2e23eafc5d4d25"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| C native type | X | O | O | O | O |
| struct, union | X | O | O | O | O |
| typedef | X | O | O | O | O |
| VARCHAR | X | O | O | O | O |
| LONG VARCHAR | X | O | O | O | O |
| BINARY | X | O | O | O | O |
| LONG VARBINARY | X | O | O | O | O |
| BOOLEAN | X | O | O | O | O |
| NUMBER | X | O | O | O | O |
| DATE | X | O | O | O | O |
| TIME | X | O | O | O | O |
| TIME WITH TIMEZONE | X | O | O | O | O |
| TIMESTAMP | X | O | O | O | O |
| TIMESTAMP WITH TIMEZONE | X | O | O | O | O |
| INTERVAL YEAR | X | O | O | O | O |
| INTERVAL MONTH | X | O | O | O | O |
| INTERVAL DAY | X | O | O | O | O |
| INTERVAL HOUR | X | O | O | O | O |
| INTERVAL MINUTE | X | O | O | O | O |
| INTERVAL SECOND | X | O | O | O | O |
| INTERVAL YEAR TO MONTH | X | O | O | O | O |
| INTERVAL DAY TO HOUR | X | O | O | O | O |
| INTERVAL DAY TO MINUTE | X | O | O | O | O |
| INTERVAL DAY TO SECOND | X | O | O | O | O |
| INTERVAL HOUR TO MINUTE | X | O | O | O | O |
| INTERVAL HOUR TO SECOND | X | O | O | O | O |
| INTERVAL MINUTE TO SECOND | X | O | O | O | O |

<a id="1cc9f7d743fe2d21"></a>
##### Dynamic SQL

The following is a feature matrix for dynamic SQL.

**Feature matrix for dynamic SQL**

<a id="ca36d0dc11953599"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| SELECT .. INTO | X | O | O | O | O |
| EXECUTE IMMEDIATE sql | X | O | O | O | O |
| PREPARE stmt | X | O | O | O | O |
| EXECUTE stmt | X | O | O | O | O |
| DECLARE cursor FOR sql | X | O | O | O | O |
| DECLARE cursor FOR stmt | X | O | O | O | O |
| OPEN cursor | X | O | O | O | O |
| OPEN cursor USING | X | O | O | O | O |
| FETCH cursor INTO | X | O | O | O | O |
| CLOSE cursor | X | O | O | O | O |
| DELETE .. WHERE CURRENT OF cursor | X | O | O | O | O |
| UPDATE .. WHERE CURRENT OF cursor | X | O | O | O | O |

<a id="93bb9a632c48a138"></a>
#### PyDBC

<a id="1e7bd1e1bb3df372"></a>
##### Module

The following is a method feature matrix for pygoldilocks provided by PyDBC.

**Feature matrix for pygoldilock method**

<a id="b6f7762e69039491"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| connect | X | X | X | O | O |
| Date | X | X | X | O | O |
| Time | X | X | X | O | O |
| Timestamp | X | X | X | O | O |
| DateFromTicks | X | X | X | O | O |
| TimeFromTicks | X | X | X | O | O |
| TimestampFromTicks | X | X | X | O | O |
| Binary | X | X | X | O | O |
| STRING | X | X | X | O | O |
| BINARY | X | X | X | O | O |
| NUMBER | X | X | X | O | O |
| DATETIME | X | X | X | O | O |
| ROWID | X | X | X | O | O |
| getDecimalSeparator | X | X | X | O | O |
| setDecimalSeparator | X | X | X | O | O |

The following is an attribute feature matrix for pygoldilocks module.

**Feature matrix for pygoldilock attribute**

<a id="402fc8b775c323b1"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| apilevel | X | X | X | O | O |
| threadsafety | X | X | X | O | O |
| paramstyle | X | X | X | O | O |
| version | X | X | X | O | O |
| lowercase | X | X | X | O | O |

<a id="c4226ec44d5ce59e"></a>
##### Connection

The following is a method feature matrix for connection object.

**Feature matrix for connection method**

<a id="b34cfb7119d89f26"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor | X | X | X | O | O |
| commit | X | X | X | O | O |
| rollback | X | X | X | O | O |
| close | X | X | X | O | O |
| getinfo | X | X | X | O | O |
| execute | X | X | X | O | O |
| set_attr | X | X | X | O | O |

The following is an attribute feature matrix for connection object.

**Feature matrix for connection attribute**

<a id="9050ecc31bbe476f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| autocommit | X | X | X | O | O |
| searchescape | X | X | X | O | O |
| timeout | X | X | X | O | O |

<a id="35ed11f65bf68663"></a>
##### Cursor

The following is a method feature matrix for cursor object.

**Feature matrix for cursor method**

<a id="40e443678c9f6484"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| excute | X | X | X | O | O |
| executemany | X | X | X | O | O |
| fetchone | X | X | X | O | O |
| fetchall | X | X | X | O | O |
| fetchmany | X | X | X | O | O |
| commit | X | X | X | O | O |
| rollback | X | X | X | O | O |
| skip | X | X | X | O | O |
| nextset | X | X | X | O | O |
| close | X | X | X | O | O |
| setinputsizes | X | X | X | O | O |
| setoutputsize | X | X | X | O | O |
| callproc | X | X | X | O | O |
| callfunc | X | X | X | O | O |
| tables | X | X | X | O | O |
| columns | X | X | X | O | O |
| statistics | X | X | X | O | O |
| rowIdColumns | X | X | X | O | O |
| rowVerColumns | X | X | X | O | O |
| primaryKeys | X | X | X | O | O |
| foreignKeys | X | X | X | O | O |
| procedures | X | X | X | O | O |
| getTypeInfo | X | X | X | O | O |

The following is an attribute feature matrix for cursor object.

**Feature matrix for cursor attribute**

<a id="dcceba835545f1a1"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| Description | X | X | X | O | O |
| rowcount | X | X | X | O | O |
| arraysize | X | X | X | O | O |
| connection | X | X | X | O | O |
| fast_executemany | X | X | X | O | O |

<a id="a5014683a280eb04"></a>
##### Row

The following is an attribute feature matrix for row object.

**Feature matrix for row attribute**

<a id="c45da6222b57c33c"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| cursor_description | X | X | X | O | O |

<a id="0ae13a216b3ac892"></a>
### Utility

<a id="0e9b9a5fcdc64898"></a>
#### gcreatedb

<a id="7929899b038f1dff"></a>
##### Command Usage

The following is a feature matrix for command usage of gcreatedb.

**Feature matrix for command usage of gcreatedb**

<a id="f6db6f1cbfe52c3b"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --character_set | O | O | O | O | O |
| --char_length_units | X | O | O | O | O |
| --cluster | X | X | O | O | O |
| --db_comment | O | O | O | O | O |
| --help | O | O | O | O | O |
| --host | X | X | O | O | O |
| --member | X | X | O | O | O |
| --port | X | X | O | O | O |
| --silent | O | O | O | O | O |
| --timezone | X | O | O | O | O |

<a id="0d5b9cfd1119ba9b"></a>
#### glsnr

<a id="7165128163598407"></a>
##### Command Usage

The following is a feature matrix for command usage of glsnr.

**Feature matrix for command usage of glsnr**

<a id="1dbe6bb1c4f2dc5f"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --help | X | O | O | O | O |
| --home | X | X | O | O | O |
| --silent | X | O | O | O | O |
| --start | X | O | O | O | O |
| --status | X | O | O | O | O |
| --stop | X | O | O | O | O |

<a id="aa1f810b2b7a8761"></a>
##### Configuration File

The following is a feature matrix for configuration of glsnr.

**Feature matrix for configuration of glsnr**

<a id="539be38c49409227"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| BACKLOG | X | O | O | O | O |
| DEFAULT_CS_MODE | X | O | O | O | O |
| LISTENER_LOG_DIR | X | X | O | O | O |
| LISTEN_PORT | X | O | O | O | O |
| TCP_EXCLUDED | X | O | O | O | O |
| TCP_INVITED | X | O | O | O | O |
| TCP_HOST | X | O | O | O | O |
| TCP_VALIDNODE_CHECKING | X | O | O | O | O |
| TIMEOUT | X | O | O | O | O |
| USR_DIR | X | X | O | O | O |

<a id="3d4f65680e11d09f"></a>
#### gsql/ gsqlnet

<a id="d5e195992bd07189"></a>
##### Command Usage

The following is a feature matrix for command usage of gsql.

**Feature matrix for command usage of gsql**

<a id="c71c5d85781920c6"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| username password | O | O | O | O | O |
| --as {SYSDBA\|ADMIN} | X | O | O | O | O |
| --conn-string | X | O | O | O | O |
| --dsn | X | O | O | O | O |
| --enable-color | O | O | O | O | O |
| --help | O | O | O | O | O |
| --import | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --prompt | O | O | O | O | O |
| --silent | O | O | O | O | O |
| --version | O | O | O | O | O |

<a id="da07fa95fa955be0"></a>
##### Interactive gsql Command

The following is a feature matrix for interactive gsql command which is used in gsql prompt state.

**Feature matrix for interactive gsql command**

<a id="31f2d8474e8a1d16"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| `\\` | O | O | O | O | O |
| `\connect userid password [as sysdba] ` | X | O | O | O | O |
| `\cshutdown` | X | X | O | O | O |
| `\cstartup` | X | X | O | O | O |
| `\ddl_cluster` | X | X | O | O | O |
| `\ddl_db` | X | O | O | O | O |
| `\ddl_tablespace` | X | O | O | O | O |
| `\ddl_profile` | X | O | O | O | O |
| `\ddl_audit_policy` | X | X | X | O | O |
| `\ddl_auth` | X | O | O | O | O |
| `\ddl_schema` | X | O | O | O | O |
| `\ddl_public_synonym` | X | O | O | O | O |
| `\ddl_table` | X | O | O | O | O |
| `\ddl_constraint` | X | O | O | O | O |
| `\ddl_index` | X | O | O | O | O |
| `\ddl_view` | X | O | O | O | O |
| `\ddl_sequence` | X | O | O | O | O |
| `\ddl_synonym` | X | O | O | O | O |
| `\ddl_procedure` | X | X | O | O | O |
| `\ddl_package` | X | X | X | O | O |
| `\desc ` | O | O | O | O | O |
| `\dynamic sql :var ` | X | O | O | O | O |
| `\exec ` | O | O | O | O | O |
| `\exec :var := :value` | O | O | O | O | O |
| `\exec sql ` | O | O | O | O | O |
| `\explain plan [on\|only] ` | O | O | O | O | O |
| `\help ` | O | O | O | O | O |
| `\history` | O | O | O | O | O |
| `\host {os_command}` | X | X | O | O | O |
| `\import` | O | O | O | O | O |
| `\idesc ` | O | O | O | O | O |
| `\{n} ` | O | O | O | O | O |
| `\prepare sql ` | O | O | O | O | O |
| `\print ` | O | O | O | O | O |
| `\quit` | O | O | O | O | O |
| `\set autocommit ` | O | O | O | O | O |
| `\set color ` | O | O | O | O | O |
| `\set colsize ` | X | O | O | O | O |
| `\set ddlsize` | X | O | O | O | O |
| `\set error ` | O | O | O | O | O |
| `\set history ` | O | O | O | O | O |
| `\set linesize ` | O | O | O | O | O |
| `\set numsize ` | X | O | O | O | O |
| `\set pagesize ` | O | O | O | O | O |
| `\set timing ` | O | O | O | O | O |
| `\set vertical ` | O | O | O | O | O |
| `\shutdown {abort\|immediate\|transactional\|normal}` | X | O | O | O | O |
| `\startup {nomount\|mount\|open} ` | X | O | O | O | O |
| `\var ` | O | O | O | O | O |

<a id="0e04214319c73895"></a>
#### gloader/ gloadernet

<a id="ec85301cdec4ce45"></a>
##### Command Usage

The following is a feature matrix for command usage of gloader.

**Feature matrix for command usage of gloader**

<a id="3195912218ccad90"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| username password | O | O | O | O | O |
| --array | O | O | O | O | O |
| --atomic | O | O | O | O | O |
| --bad | O | O | O | O | O |
| --buffered | X | O | O | O | O |
| --commit | O | O | O | O | O |
| --control | O | O | O | O | O |
| --data | O | O | O | O | O |
| --dsn | X | O | O | O | O |
| --errors | X | O | O | O | O |
| --export | O | O | O | O | O |
| --fieldterm | X | X | O | O | O |
| --filesize | X | O | O | O | O |
| --format | X | O | O | O | O |
| --help | O | O | O | O | O |
| --import | O | O | O | O | O |
| --lineterm | X | X | O | O | O |
| --log | O | O | O | O | O |
| --no-prompt | O | O | O | O | O |
| --parallel | O | O | O | O | O |
| --propagation | X | O | O | O | O |
| --qualifier | X | X | O | O | O |
| --silent | O | O | O | O | O |
| --AsTIMESTAMP | X | O | O | O | O |
| --where | X | X | X | O | O |
| --group-id | X | X | X | O | O |
| --directio-size | X | X | X | O | O |

<a id="fa9b464dcc567a76"></a>
##### Control File Syntax

The following is a feature matrix for control file syntax of gloader.

**Feature matrix for control file syntax of gloader**

<a id="169b657de2d3088c"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| CHARACTERSET | X | O | O | O | O |
| FIELDS TERMINATED BY | O | O | O | O | O |
| OPTIONALLY ENCLOSED BY | O | O | O | O | O |
| TABLE table_name | O | O | O | O | O |
| TABLE schema_name.table_name | X | O | O | O | O |
| LTRIM | X | X | O | O | O |
| RTRIM | X | X | O | O | O |
| LINES TERMINATED BY | X | X | O | O | O |
| WHERE | X | X | X | O | O |

<a id="803cb358c631389f"></a>
#### gdump

<a id="67eb9c68aa030bd6"></a>
##### Command Usage

The following is a feature matrix for command usage of gdump.

<a id="a970454a5ac155e1"></a>
<table class="table column_count_7"><caption>Feature matrix for command usage of gdump</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle"><div>Common arguments</div></td><td><div>--silent</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>File type</div></td><td><div>BACKUP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>COMMIT_LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CONTROL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DATA</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PEND_BUFFER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPERTY</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>BACKUP file arguments</div></td><td><div>--body</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--tbs</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle"><div>CONTROL file arguments</div></td><td><div>--section</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="3"><div>DATA file arguments</div></td><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>LOG file arguments</div></td><td><div>--all</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--fetch</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--header</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--number</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>--offset</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="1fc2b031a433f72d"></a>
#### tablediff

<a id="937e07753cbf1ae1"></a>
##### Configuration File

The following is a feature matrix for configuration file of tablediff.

<a id="b8044cf66b62c40c"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of tablediff</caption><thead><tr><th class="to_center"><div>Item</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="5"><div>Source table</div></td><td class="to_middle"><div>SOURCE_PASSWORD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_SCHEMA</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_URL</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_USER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="5"><div>Target table</div></td><td class="to_middle"><div>TARGET_PASSWORD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_SCHEMA</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_TABLE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_URL</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_USER</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="4"><div>Sync operation</div></td><td class="to_middle"><div>TARGET_INSERT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_UPDATE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>TARGET_DELETE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SOURCE_INSERT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle" rowspan="13"><div>Operation options</div></td><td class="to_middle"><div>DIFF_BIN_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DIFF_OUT_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_CALL_STACK</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>DISPLAY_ROW_UNIT</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>EXCLUDE_COLUMNS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_DIFF</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>LOGGING_ON_SUCCESS</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_QUEUE_SIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_THREAD</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>JOB_UNIT_SIZE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>PARTITION_RANGE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>SYNC_OUT_FILE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>WHERE_CLAUSE</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr></tbody></table>

<a id="c0665c9dbcaa8ef5"></a>
#### gsyncher

<a id="42b8752e2bc01a85"></a>
##### Command Usage

The following is a feature matrix for command usage of gsyncher.

**Feature matrix for command usage of gsyncher**

<a id="04066faef2e766ca"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --log | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --home | X | X | O | O | O |
| --copy-right | X | O | O | O | O |
| --backup-path | X | O | O | O | O |
| --help | X | O | O | O | O |

<a id="3783b0e8a0e274eb"></a>
#### gmon

<a id="d0efe7e41372fa40"></a>
##### Command Usage

The following is a feature matrix for command usage of gmon.

**Feature matrix for command usage of gmon**

<a id="370757623a0d8075"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | X | X | O | O | O |
| --stop | X | X | O | O | O |
| --status | X | X | O | O | O |
| --home | X | X | O | O | O |
| --uds_dir | X | X | X | X | O |
| --silent | X | X | O | O | O |
| --no-copyright | X | X | O | O | O |
| --help | X | X | O | O | O |

<a id="d6d9d8173a039665"></a>
#### gtrclogger

<a id="62a106ff44c85f65"></a>
##### Command Usage

The following is a feature matrix for command usage of gtrclogger.

**Feature matrix for command usage of gtrclogger**

<a id="e8a2709e2e2ac552"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --dir | X | X | O | O | O |
| --help | X | X | O | O | O |
| --port | X | X | O | O | O |
| --start | X | X | O | O | O |
| --stop | X | X | O | O | O |

<a id="f29247604ffa002d"></a>
#### glocator

<a id="b93f682592b6aacd"></a>
##### Command Usage

The following is a feature matrix for command usage of glocator.

**Feature matrix for command usage of glocator**

<a id="3edef621ddac801b"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --create | X | X | O | O | O |
| --start | X | X | O | O | O |
| --stop | X | X | O | O | O |
| --conf | X | X | O | O | O |
| --status | X | X | O | O | O |
| --sync | X | X | X | O | O |
| --silent | X | X | O | O | O |
| --no-copyright | X | X | O | O | O |
| --help | X | X | O | O | O |

<a id="bd7fea7902908ac7"></a>
##### Configuration File

The following is a feature matrix for configuration file of glocator.

**Feature matrix for configuration file of glocator**

<a id="c4fdc24dce4f2e09"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | X | O | O | O |
| WORKER_COUNT | X | X | O | O | O |
| SESSION_QUEUE_SIZE | X | X | O | O | O |
| SESSION_ALLOCATOR_SIZE | X | X | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | X | O | O | O |
| SYSTEM_LOGGER_DIR | X | X | O | O | O |
| SYSTEM_UDS_DIR | X | X | O | O | O |
| LOCATION_FILE_DIR | X | X | O | O | O |
| LOCATION_FILE_SIZE | X | X | O | O | O |
| LOCATION_FILE_MAX_SIZE | X | X | O | O | O |
| SESSION_TIMEOUT | X | X | O | O | O |
| FAILOVER_TIMEOUT | X | X | O | O | O |
| ALTERNATE_LOCATORS | X | X | X | O | O |
| SYNC_RETRY_COUNT | X | X | X | O | O |
| SYNC_RESPONSE_TIMEOUT | X | X | X | O | O |

<a id="bce5e3891fd46878"></a>
#### gagent

<a id="50b58b48dcac8857"></a>
##### Command Usage

The following is a feature matrix for command usage of gagent.

**Feature matrix for command usage of gagent**

<a id="84b73c291231deb0"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --start | X | X | O | O | O |
| --stop | X | X | O | O | O |
| --conf | X | X | O | O | O |
| --status | X | X | O | O | O |
| --home | X | X | O | O | O |
| --silent | X | X | O | O | O |
| --no-copyright | X | X | O | O | O |
| --help | X | X | O | O | O |

<a id="99e5554a7649f6d4"></a>
##### Configuration File

The following is a feature matrix for configuration file of gagent.

**Feature matrix for configuration file of gagent**

<a id="131bb699bc1ca310"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | X | O | O | O |
| LOCATOR_HOST | X | X | O | O | O |
| LOCATOR_PORT | X | X | O | O | O |
| COMMAND_QUEUE_SIZE | X | X | O | O | O |
| COMMAND_ALLOCATOR_SIZE | X | X | O | O | O |
| PACKET_ALLOCATOR_SIZE | X | X | O | O | O |
| SYSTEM_LOGGER_DIR | X | X | O | O | O |
| SESSION_TIMEOUT | X | X | O | O | O |
| UPDATE_LOCATION_TIME | X | X | O | O | O |
| ALTERNATE_LOCATORS | X | X | X | O | O |

<a id="d2c610159b977213"></a>
#### gloctl

<a id="ef833d2d03c6e975"></a>
##### Command Usage

The following is a feature matrix for command usage of gloctl.

**Feature matrix for command usage of gloctl**

<a id="0160c9d5b194476e"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --dsn | X | X | O | X | X |
| --conf | X | X | X | O | O |
| --ip | X | X | O | O | O |
| --port | X | X | O | O | O |
| --import | X | X | O | O | O |
| --silent | X | X | O | O | O |
| --no-copyright | X | X | O | O | O |
| --help | X | X | O | O | O |

<a id="40a9e349449d32d7"></a>
##### Configuration File

The following is a feature matrix for configuration file of gloctl.

**Feature matrix for configuration file of gloctl**

<a id="22c044bdc8048188"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| PORT | X | X | X | O | O |
| LOCATOR_HOST | X | X | X | O | O |
| LOCATOR_PORT | X | X | X | O | O |

<a id="49f33c025663f647"></a>
### Replication

<a id="a27f2e72d9a3aad0"></a>
#### cyclone

<a id="5eb717c4c201958e"></a>
##### Command Usage

The following is a feature matrix for command usage of cyclone.

**Feature matrix for command usage of cyclone**

<a id="62c28de47c9f4ca3"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | X | O | O | O | O |
| --encrypt | X | X | O | O | O |
| --group | X | O | O | O | O |
| --help | X | O | O | O | O |
| --key | X | X | O | O | O |
| --master | X | O | O | O | O |
| --reset | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --slave | X | O | O | O | O |
| --start | X | O | O | O | O |
| --status | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --sync | X | O | O | O | O |
| --stand-alone | X | X | X | O | O |
| --recovery | X | X | X | O | O |
| --local | X | X | X | O | O |
| --info | X | O | O | O | O |

<a id="3c581ae4d5212d87"></a>
##### Configuration File

The following is a feature matrix for configuration file of cyclone.

<a id="c14d70fcb7d56b50"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of cyclone</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="12"><div>Common configuration</div></td><td><div>COMM_CHUNK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ENCRYPT_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GROUP_NAME</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_EXTERNAL_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_left"><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HEARTBEAT_TIMEOUT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="11"><div>MASTER configuration</div></td><td><div>CAPTURE_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>READ_LOG_BLOCK_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_SORT_AREA_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>TRANS_FILE_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNCHER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SYNC_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>GIVEUP_INTERVAL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>SKIP_COMMENT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_1</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>LOG_CAPTURE_INTERVAL_2</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="8"><div>SLAVE configuration</div></td><td><div>APPLIER_COUNT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_ARRAY_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td></tr><tr><td><div>APPLY_COMMIT_SIZE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>APPLY_TABLE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROPAGATE_MODE</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>CLUSTER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>ORACLE_DRIVER</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="58b76b0ed4653db8"></a>
#### logmirror

<a id="2ad1559c81563dbf"></a>
##### Command Usage

The following is a feature matrix for command usage of logmirror.

**Feature matrix for command usage of logmirror**

<a id="a38ea5aa74bb7ff7"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | X | O | O | O | O |
| --help | X | O | O | O | O |
| --infiniband | X | O | O | O | O |
| --master | X | O | O | O | O |
| --silent | X | O | O | O | O |
| --slave | X | O | O | O | O |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |

<a id="417bca6a3b19c1f6"></a>
##### Configuration File

The following is a feature matrix for configuration file of logmirror.

<a id="1a1235873997690f"></a>
<table class="table column_count_7"><caption>Feature matrix for configuration file of logmirror</caption><thead><tr><th class="to_center"><div>Configuration</div></th><th class="to_center"><div>Feature</div></th><th class="to_center"><div>1.x</div></th><th class="to_center"><div>2.x</div></th><th class="to_center"><div>3.1</div></th><th class="to_center"><div>3.2</div></th><th class="to_center"><div>20c.1</div></th></tr></thead><tbody><tr><td><div>Common configuration</div></td><td><div>PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="6"><div>MASTER configuration</div></td><td><div>DSN</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>HOST_PORT</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>PROTOCOL</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_ID</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>USER_PW</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td class="to_middle" rowspan="2"><div>SLAVE configuration</div></td><td><div>LOG_PATH</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr><tr><td><div>MASTER_IP</div></td><td class="to_center"><div>X</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td><td class="to_center"><div>O</div></td></tr></tbody></table>

<a id="5f27e073da7bacad"></a>
#### cymon

<a id="2683086ea3393e5c"></a>
##### Command Usage

The following is a feature matrix for command usage of cymon.

**Feature matrix for command usage of cymon**

<a id="a675516eae4dfe1c"></a>
| Feature | 1.x | 2.x | 3.1 | 3.2 | 20c.1 |
| --- | --- | --- | --- | --- | --- |
| --conf | X | O | O | O | O |
| --help | X | O | O | O | O |
| --cycle | X | O | O | O | O |
| --key | X | X | O | O | O |
| --start | X | O | O | O | O |
| --stop | X | O | O | O | O |
| --status | X | O | O | O | O |

<a id="cfbbc7cb9e8f8d01"></a>
#### cyfile

<a id="e6db45cef68768dd"></a>
##### Command Usage

The following is a feature matrix for command usage of cyfile.

**Feature matrix for command usage of cyfile**

<a id="428001ca8d116860"></a>
| Feature | 2.x | 3.1 | 3.2 | 20c.1 | Trunk |
| --- | --- | --- | --- | --- | --- |
| --conf | X | X | X | O | O |
| --help | X | X | X | O | O |
| --reset | X | X | X | O | O |
| --key | X | X | X | O | O |
| --silent | X | X | X | O | O |
| --info | X | X | X | O | O |
| --start | X | X | X | O | O |
| --stop | X | X | X | O | O |
| --group | X | X | X | O | O |
| --encrypt | X | X | X | O | O |
| --status | X | X | X | O | O |

<a id="872216ec877ef11c"></a>
##### Configuration File

The following is a feature matrix for configuration file of cyfile.

**Feature matrix for configuration file of cyfile**

<a id="3f666c5eebb66061"></a>
| Feature | 2.x | 3.1 | 3.2 | 20c.1 | Trunk |
| --- | --- | --- | --- | --- | --- |
| DSN | X | X | X | O | O |
| HOST_IP | X | X | X | O | O |
| HOST_PORT | X | X | X | O | O |
| PROTOCOL | X | X | X | O | O |
| USER_ID | X | X | X | O | O |
| USER_PW | X | X | X | O | O |
| GROUP_NAME | X | X | X | O | O |
| USER_ENCRYPT_PW | X | X | X | O | O |
| CAPTURE_TABLE | X | X | X | O | O |
| READ_LOG_BLOCK_COUNT | X | X | X | O | O |
| TRANS_SORT_AREA_SIZE | X | X | X | O | O |
| TRANS_FILE_PATH | X | X | X | O | O |
| LOG_CAPTURE_INTERVAL_1 | X | X | X | O | O |
| LOG_CAPTURE_INTERVAL_2 | X | X | X | O | O |
| DATA_FILE_PATH | X | X | X | O | O |
| DATA_FILE_PREFIX | X | X | X | O | O |
| DATA_FILE_SIZE | X | X | X | O | O |
| UPDATE_BEFORE_VALUE | X | X | X | O | O |

<a id="fff271c7529f539b"></a>
## What's New in GOLDILOCKS 20c.1

This chapter briefly describes the features added to GOLDILOCKS 20c.1.

<a id="c10d6b098130d969"></a>
### Architecture

<a id="1ce05a63afbee368"></a>
#### System Architecture

The available platform has been changed.

- [linux-powerpc-64](2-tutorial.md#fec0e4faecf8ffe5) has been added.
- [aix6-powerpc-64](2-tutorial.md#fec0e4faecf8ffe5) has been deleted.
- [aix7-powerpc-64](2-tutorial.md#fec0e4faecf8ffe5) has been added.

<a id="a21bdbd8f80777ae"></a>
#### Storage Internal

Tables and indexes can be stored in the disk tablespace. Pages in the disk tablespace should be read by using s separate memory space, so the buffer cache feature also has been added for that.

Also, the incremental backup for the disk tablespace is determined after scanning the entire data file looking for updated pages after the previous backup. Therefore, if the data file size is big, then the backup speed is slow even when the number of updated pages is small. Therefore, change tracking feature has been added to fix the problem of the incremental backup for the disk tablespace.

<a id="daff87a5b0c5140e"></a>
#### Transaction Control

It has not been changed.

<a id="bdeb52c96130ca18"></a>
#### Backup & Recovery

It has not been changed.

<a id="f0ec5de56ad1fd38"></a>
#### Database Information

<a id="d4bce354493c6bf3"></a>
##### DICTIONARY_SCHEMA

The following views have been added to retrieve the recyclebin object information.

- [DBA_RECYCLEBIN](../part-02-administration-manual/9-database-information.md#0399befaa3a7a6e4)
- [USER_RECYCLEBIN](../part-02-administration-manual/9-database-information.md#5a7ffc8c6fdbb148)
- [RECYCLEBIN](../part-02-administration-manual/9-database-information.md#5bf06cdb9ed20ff7)

The following views have been added to retrieve the PSM package object information.

- [ALL_PACKAGE_PRIVS](../part-02-administration-manual/9-database-information.md#dde8cf0bc056c184)
- [ALL_PACKAGE_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#abdc8ade55dad425)
- [ALL_PACKAGE_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#47b6111e7b0dff6c)
- [DBA_PACKAGE_PRIVS](../part-02-administration-manual/9-database-information.md#f2948fde085c4d91)
- [USER_PACKAGE_PRIVS](../part-02-administration-manual/9-database-information.md#18f2a50e7a7e0ea8)
- [USER_PACKAGE_PRIVS_MADE](../part-02-administration-manual/9-database-information.md#fd8d64a0628966c8)
- [USER_PACKAGE_PRIVS_RECD](../part-02-administration-manual/9-database-information.md#9eeb6efa8ddaf503)

<a id="195c49fb2a187cbe"></a>
##### INFORMATION_SCHEMA

The following views have been added to retrieve the PSM package object information.

- [MODULES](../part-02-administration-manual/9-database-information.md#e2e3ad11d02a8507)
- [MODULE_BODY](../part-02-administration-manual/9-database-information.md#e1b232a2167277d0)
- [MODULE_BODY_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#70ed94c476b8296f)
- [MODULE_BODY_ROUTINE_USAGE](../part-02-administration-manual/9-database-information.md#cc749b84601d1e49)
- [MODULE_BODY_SEQUENCE_USAGE](../part-02-administration-manual/9-database-information.md#4e9e9b09c00ba657)
- [MODULE_BODY_TABLE_USAGE](../part-02-administration-manual/9-database-information.md#d18ec651f4765cbe)
- [MODULE_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#fe7973c0d3b2cd0b)
- [MODULE_PRIVILEGES](../part-02-administration-manual/9-database-information.md#bc7b373d2aaf2997)
- [MODULE_ROUTINE_USAGE](../part-02-administration-manual/9-database-information.md#d09409ee15a91dea)
- [MODULE_SEQUENCE_USAGE](../part-02-administration-manual/9-database-information.md#c7cd783de795c62c)
- [MODULE_TABLE_USAGE](../part-02-administration-manual/9-database-information.md#717b1c4560f26f50)
- [ROUTINE_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#f1337052e0bfd70f)
- [VIEW_MODULE_USAGE](../part-02-administration-manual/9-database-information.md#d245e449895227ff)

<a id="73b0dab095a0443b"></a>
##### PERFORMANCE_VIEW_SCHEMA

The following views have been added to retrieve the statistics information about the buffer cache and to retrieve all page frames of the buffer cache for caching the disk tablespace pages.

- [V$BCH](../part-02-administration-manual/9-database-information.md#d3a5a314a1fde361)
- [V$BUFFER_STAT](../part-02-administration-manual/9-database-information.md#b9ba0f4dd820c464)

[V$DB_CHANGE_TRACKING](../part-02-administration-manual/9-database-information.md#a6e54411676230d7) has been added to retrieve the change tracking information which is used for the disk tablespace incremental backup.

<a id="c8fdcd565e0c3909"></a>
#### Server Property

<a id="dc52ba4ce84afd2b"></a>
##### The property for the recyclebin

[RECYCLEBIN](../part-02-administration-manual/10-server-property.md#66227b4a108abd8d) property has been added to activate the recyclebin feature.

<a id="6124923c5ec4cc29"></a>
##### CLUSTER_SESSION_HASH_BUCKETS

[CLUSTER_SESSION_HASH_BUCKETS](../part-02-administration-manual/10-server-property.md#5001e0a508492aa3) property has been added to control the number of hash buckets of the cluster session.

<a id="f64694010e1007da"></a>
##### DEADLOCK_PRIORITY

[DEADLOCK_PRIORITY](../part-02-administration-manual/10-server-property.md#661ef139ef73c8cf) property has been added to select a specific transaction as a victim for resolving the deadlock which occurred while simultaneously processing multiple transactions.

<a id="7d1344c934013fcd"></a>
##### USE_LARGE_PAGES

[USE_LARGE_PAGES](../part-02-administration-manual/10-server-property.md#f838d6d20a8a1377) property has been added to use HugePage.

<a id="003616b7cbc23b62"></a>
##### BUFFER_CACHE_SIZE

[BUFFER_CACHE_SIZE](../part-02-administration-manual/10-server-property.md#d438f35f7fc39b51) property has been added to set the size of the buffer cache which cashes the disk tablespace.

<a id="cfcd71a6a60a6d98"></a>
##### BUFFER_CHECKPOINT_LIST_COUNT

[BUFFER_CHECKPOINT_LIST_COUNT](../part-02-administration-manual/10-server-property.md#005d4e68f933e38a) property has been added to set the number of checkpoint lists to link for flushing the updated pages in the buffer cache to the disk when performing the checkpoint.

<a id="8247ac0a94d8d01e"></a>
##### BUFFER_FLUSH_THREADS

[BUFFER_FLUSH_THREADS](../part-02-administration-manual/10-server-property.md#4c54e6675f656479) property has been added to set the number of threads which flushes the database system buffers.

<a id="238a7f9e860e3492"></a>
##### BUFFER_FLUSHING_INTERVAL

[BUFFER_FLUSHING_INTERVAL](../part-02-administration-manual/10-server-property.md#0ee83d428c6c0d54) property has been added to set the idle time of when the buffer flush thread does not have any task to process.

<a id="c3f4077acf958d22"></a>
##### BUFFER_FREE_LIST_COUNT

[BUFFER_FREE_LIST_COUNT](../part-02-administration-manual/10-server-property.md#5c2850ace46ec79c) property has been added to set the number of lists linking bch which is instantly available in the buffer cache.

<a id="ecab441289022dba"></a>
##### BUFFER_HASH_BUCKETS

[BUFFER_HASH_BUCKETS](../part-02-administration-manual/10-server-property.md#22df381968cc09ab) property has been added to set the number of hash buckets to lookup the pages cached in the buffer cache.

<a id="83a9557c923eb6d5"></a>
##### BUFFER_HOT_REGION_CRITERIA

[BUFFER_HOT_REGION_CRITERIA](../part-02-administration-manual/10-server-property.md#e0e997271e9e7970) property has been added to set *touch count* to transfer pages to the hot region in buffer lru list.

<a id="2695a63247ed794a"></a>
##### BUFFER_HOT_REGION_PERCENT

[BUFFER_HOT_REGION_PERCENT](../part-02-administration-manual/10-server-property.md#0116b509d070906f) property has been added to set the proportion (percentage) of pages to leave in hot region to the entire page in the buffer lru list.

<a id="67875ad7086cab3e"></a>
##### BUFFER_LRU_LIST_COUNT

[BUFFER_LRU_LIST_COUNT](../part-02-administration-manual/10-server-property.md#58313b5de02bdcbb) property has been added to set the number of buffer lru lists to be used in the database system.

<a id="83ee7e03a955556a"></a>
##### BUFFER_MULTIPAGE_READ_COUNT

[BUFFER_MULTIPAGE_READ_COUNT](../part-02-administration-manual/10-server-property.md#21c7fc13eb798f14) property has been added to set the maximum number of pages to be used for one time disk IO when full scanning the disk table.

<a id="e8af7125c5edc7e8"></a>
##### CHANGE_TRACKING

[CHANGE_TRACKING](../part-02-administration-manual/10-server-property.md#99b038a7da685780) property has been added to set whether to track the updated pages to perform the incremental backup of disk tablespace.

<a id="36ef8dad13f0d84f"></a>
##### CHANGE_TRACKING_EXTENT_SIZE

[CHANGE_TRACKING_EXTENT_SIZE](../part-02-administration-manual/10-server-property.md#417b6dfe23b70666) property has been added to set the number of pages to be included in one extent when performing change tracking.

<a id="0448d4c1cf107290"></a>
##### CHANGE_TRACKING_FILE

[CHANGE_TRACKING_FILE](../part-02-administration-manual/10-server-property.md#c72973af494b6dce) property has been added to set the file directory which stores the change tracking, and the file name.

<a id="c517fdd684803e6c"></a>
##### INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

[INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE](../part-02-administration-manual/10-server-property.md#d82fc4412501b069) property has been added to set the maximum number of pages to be read by one time disk IO when performing the incremental backup of disk tablespace.

<a id="be9252f7f14237db"></a>
##### REDO_LOG_COMPRESSION_THRESHOLD

[REDO_LOG_COMPRESSION_THRESHOLD](../part-02-administration-manual/10-server-property.md#7d7c66aade580fc0) property has been added to set the threshold size when compressing the log.

<a id="f8f790e6147738d9"></a>
##### SYSTEM_DISK_DATA_TABLESPACE_SIZE

[SYSTEM_DISK_DATA_TABLESPACE_SIZE](../part-02-administration-manual/10-server-property.md#97522be350b538cc) property has been added to set DISK_DATA_TBS tablespace size when creating the database.

<a id="2fd7aef6cd59d3ef"></a>
##### USER_DATA_TABLESPACE_MEDIA_TYPE

[USER_DATA_TABLESPACE_MEDIA_TYPE](../part-02-administration-manual/10-server-property.md#79aa027e79a7b50d) property has been added to set the default media type to use if the tablespace media type is omitted when creating the user data tablespace.

<a id="17cfc563aa165529"></a>
##### USER_DATA_TABLESPACE_SIZE

[USER_DATA_TABLESPACE_SIZE](../part-02-administration-manual/10-server-property.md#e3542e99dbc097cf) property has been added to set the default size to use if the data file size is omitted when creating the user data tablespace or adding the data file.

<a id="6526ffcd50d6eed2"></a>
##### USER_DISK_DATA_TABLESPACE_NEXTSIZE

[USER_DISK_DATA_TABLESPACE_NEXTSIZE](../part-02-administration-manual/10-server-property.md#0175e393e2c1b58e) property has been added to set the default size to use if the size to be extended is not set when it is required to extend the data file of the user disk data tablespace.

<a id="5987edf5a3b1ec0d"></a>
##### USER_TEMP_TABLESPACE_SIZE

[USER_TEMP_TABLESPACE_SIZE](../part-02-administration-manual/10-server-property.md#0f5a0f4a8b6edf18) property has been added to set the default size to use if the data file size is omitted when creating the user temp tablespace or adding the data file.

<a id="d200f3a83879ac1f"></a>
##### IN_KEY_RANGE_ARRAY_COUNT

[IN_KEY_RANGE_ARRAY_COUNT](../part-02-administration-manual/10-server-property.md#4656d2ae248373f8) property has been added to set the array size of the in key range scan based on array.

<a id="1516026d68b625a6"></a>
##### BROADCAST_INDEX_REBUILD_PROTOCOL

[BROADCAST_INDEX_REBUILD_PROTOCOL](../part-02-administration-manual/10-server-property.md#4c6034f9c28ad9e5) property has been added to set whether to simultaneously rebuild the indexes on all members when rebuilding the index in cluster environment.

<a id="527181db76bfe6e1"></a>
### SQL

<a id="e15b219467848602"></a>
#### Improved Cluster Query Performance

The performance of processing the complex query in cluster has been improved.

The performance is changed as follows according to the increase of cluster groups per each query in TPC-H(scale factor 10) test.

The following is a graph of version 20c.1.   
The response time of most queries are decreased when cluster groups increase.

<a id="07c12026d1a1c49c"></a>
![The response time per each query when cluster groups of TPC-H SF10 increase in version 20c.1](../assets/images/a9da7d3c6845d138.png)

For more information about query processing in cluster environment, refer to the followings.

- [Processing SELECT in Cluster](../part-03-sql-manual/12-sql-languages.md#347ab311664c018e)
- [SQL Tuning](../part-03-sql-manual/15-sql-tuning.md#08796d297b669e37)

<a id="672c79569f4f1ff6"></a>
#### SQL Element

<a id="059465e5066db849"></a>
##### Data Type

It has not been changed.

<a id="87c49cb614852d87"></a>
##### Function

The following formatting functions have been added.

- [NUMTODSINTERVAL](../part-03-sql-manual/17-built-in-function-references.md#178b15afb662f3e7)
- [NUMTOYMINTERVAL](../part-03-sql-manual/17-built-in-function-references.md#65a06975c0f29f33)
- [TO_NATIVE_SMALLINT](../part-03-sql-manual/17-built-in-function-references.md#c3d517a3792a9ee9)
- [TO_NATIVE_INTEGER](../part-03-sql-manual/17-built-in-function-references.md#8c40f9722a4badbe)
- [TO_NATIVE_BIGINT](../part-03-sql-manual/17-built-in-function-references.md#4ca029a562131b56)

[PHYSICAL_LENGTH](../part-03-sql-manual/17-built-in-function-references.md#a772f0c90f1e1f39) function has been added.

[LNNVL](../part-03-sql-manual/17-built-in-function-references.md#03e7bd17010092b5) function has been added.

<a id="efd06e77e558b4c5"></a>
##### Pseudo Column

[CLUSTER_SHARD_ID Pseudo Column](../part-03-sql-manual/11-sql-elements.md#a091401135dada3b) has been added.

<a id="80cc0a03a4970fab"></a>
#### Object

<a id="8e98490329cc184b"></a>
##### Package Object

The PSM package object has been added.

<a id="665e84bfcb3cffa7"></a>
#### SQL Language

<a id="f08dfdea3668cd0c"></a>
##### Table DDL

The recyclebin feature has been added to the table.

- Restoring an object stored in the recyclebin.
    - [FLASHBACK TABLE](../part-03-sql-manual/18-sql-references.md#8ffa53ef8c83bb07)
- Dropping an object stored in the recyclebin.
    - [PURGE](../part-03-sql-manual/18-sql-references.md#b23bd710e90b06b9)

[ALTER TABLE name MERGE SHARDS](../part-03-sql-manual/18-sql-references.md#a19816c91dffcb2e) has been added to merge shards.

[REBUILD GLOBAL SECONDARY INDEX](../part-03-sql-manual/18-sql-references.md#a99b0c18851a218a) has been added to rebuild the global secondary index.

<a id="f8fd6af06d4e099f"></a>
##### Index DDL

[ALTER INDEX name REBUILD](../part-03-sql-manual/18-sql-references.md#acfab393b8ed037d) has been added to rebuild the index.

<a id="c3241bbb74154ddd"></a>
##### Immutable Table

The feature which prevents the record stored in the table from being altered or deleted and prevents the table from being dropped has been added.

<a id="f50d539838428c65"></a>
##### Assigning position When Performing ADD MEMBER

The statement assigning the member position when adding the cluster member has been added.

- &lt;member position&gt; in [ALTER CLUSTER GROUP name ADD MEMBER](../part-03-sql-manual/18-sql-references.md#619c417c530cdf9a)
- &lt;member position&gt; in [CREATE CLUSTER GROUP](../part-03-sql-manual/18-sql-references.md#77c1869df568145d)

<a id="adab89c642a6fb22"></a>
##### PSM Package-related DDL

DDLs to create or drop PSM package have been added.

- [ALTER PACKAGE](../part-04-psm-manual/27-psm-sql-references.md#d764dcd97c314905)
- [CREATE PACKAGE](../part-04-psm-manual/27-psm-sql-references.md#1703e698a9990747)
- [CREATE PACKAGE BODY](../part-04-psm-manual/27-psm-sql-references.md#8cd428de365c3d39)
- [DROP PACKAGE](../part-04-psm-manual/27-psm-sql-references.md#275183c395e46b67)

<a id="e5c98fb540cafd06"></a>
##### Performance Measuring

[ALTER SYSTEM CLEANUP BUFFER_CACHE](../part-03-sql-manual/18-sql-references.md#40ca457d69aff6a3) has been added to clear buffer pages in the disk buffer cache.

<a id="4643f15d36282ead"></a>
### API

<a id="9e00d541236cde3d"></a>
#### ODBC

DOT_NET_FOR_ODBC has been added to [Keywords in the data source specification section](../part-05-developer-manual/29-odbc.md#1c85f9f5822cc739).

<a id="3c3a598c28847aaf"></a>
##### Data Source Configuration

trace, tracefile and include_synonyms have been added to [data source configuration](../part-05-developer-manual/29-odbc.md#bd6b4a774ef02591).

<a id="1157c685c2d0307c"></a>
#### JDBC

[Statement Pooling](../part-05-developer-manual/30-jdbc.md#cb7afb5ed5dcd283) feature has been added.

The [getNetworkTimeout()](../part-05-developer-manual/30-jdbc.md#3b41ef42070a23a3) and [setNetworkTimeout()](../part-05-developer-manual/30-jdbc.md#6810626dcc1e1e17) methods of the [Connection](../part-05-developer-manual/30-jdbc.md#fe504e4779c3c33a) class are supported.

<a id="a53a11202a0a3641"></a>
##### Connection Property

tcp_nodelay, login_timeout and include_synonyms have been added to [connection property](../part-05-developer-manual/30-jdbc.md#0991228d1eae1556).

<a id="97fc9f974a514b09"></a>
#### Embedded SQL

<a id="34575fb3ea558b01"></a>
##### Precompiler(gpec)

[--cumulative](../part-05-developer-manual/31-embedded-sql.md#274a5089d2d237b8) option has been added.

The [--parse](../part-05-developer-manual/31-embedded-sql.md#02ae95a8ac72f9cf) option has been added to gpec.

<a id="f072487719d66b4b"></a>
#### PDO

It has not been changed.

<a id="6561cc17a87ec07f"></a>
#### PyDBC

It has not been changed.

<a id="29e1d8d9490fa1a3"></a>
#### Ruby

It has not been changed.

<a id="24a4e9dc2baffb0e"></a>
#### Hibernate

It has not been changed.

<a id="d96839ba17b377b6"></a>
### Utility

<a id="92c535fbbd991aeb"></a>
#### gcreatedb

It has not been changed.

<a id="11bdc70b0501d567"></a>
#### glsnr

It has not been changed.

<a id="bd4991a917bd247c"></a>
#### gsql/gsqlnet

[`\ddl_package`](../part-06-utility-manual/37-gsql-gsqlnet-interactive-sql-tool.md#090d6800c4ac0e99) feature has been added to export DDL statement of the package objects.

<a id="f8a3523d18b27b62"></a>
#### gloader/gloadernet

It has not been changed.

<a id="c31dbaf5859c42bc"></a>
#### gdump

It has not been changed.

<a id="9773539783f91e33"></a>
#### tablediff

It has not been changed.

<a id="94e9bd5e9a53aaca"></a>
#### gsyncher

It has not been changed.

<a id="7d27464b4a731a52"></a>
#### gmon

It has not been changed.

<a id="d96c4c9002affc02"></a>
#### gtrclogger

It has not been changed.

<a id="e00b3729b74822c0"></a>
#### glocator

The method to communicate with gagent is changed to TCP.

FAILOVER_TIMEOUT is deleted from configure file.

[MAX_NODE_COUNT](../part-06-utility-manual/44-glocator.md#a673f5ae08659002) has been added to configure file.

[KEEPALIVE_IDLE_TIME](../part-06-utility-manual/44-glocator.md#8bcd2af50f4dbe8c), [KEEPALIVE_COUNT](../part-06-utility-manual/44-glocator.md#9f0fe87f8e18f998), [KEEPALIVE_INTERVAL](../part-06-utility-manual/44-glocator.md#b21f5a4a10e1193a) have been added to configure file.

<a id="88d27d264641970d"></a>
#### gagent

The method to communicate with glocator is changed to TCP.

COMMAND_QUEUE_SIZE is deleted from configure file.

COMMAND_ALLOCATOR_SIZE is deleted from configure file.

PACKET_ALLOCATOR_SIZE is deleted from configure file.

UPDATE_LOCATION_TIME is deleted from configure file.

SESSION_TIMEOUT is deleted from configure file.

[SYSTEM_UDS_DIR](../part-06-utility-manual/45-gagent.md#76eac818aa66fe84) has been added to configure file.

PORT is deleted, and [REQUEST_PORT](../part-06-utility-manual/45-gagent.md#7fea5e1cff83b5b1), [RESPONSE_PORT](../part-06-utility-manual/45-gagent.md#d82b88c2b34342a6) have been added to configure file.

[KEEPALIVE_IDLE_TIME](../part-06-utility-manual/45-gagent.md#040494b7131e1a40), [KEEPALIVE_COUNT](../part-06-utility-manual/45-gagent.md#0b60133bb81cd215), [KEEPALIVE_INTERVAL](../part-06-utility-manual/45-gagent.md#d593d7d38d6ba6d3) have been added to configure file.

<a id="28c71a8444002772"></a>
#### gloctl

It has not been changed.

<a id="c9bb62bc64a8940c"></a>
### Replication

<a id="55735089e2a961d5"></a>
#### cyclone

It has not been changed.

<a id="031ea46a393cb26a"></a>
#### logmirror

It has not been changed.

<a id="a95da2eb15bc1520"></a>
#### cymon

It has not been changed.

<a id="d0d7bc6678cb610a"></a>
#### cyfile

A tool which uses CDC method to store/ record the transaction of the original database in CSV format file has been added.

<a id="6dfefa71309d766b"></a>
## Patch Notes

<a id="84331ee1d5b0156d"></a>
### 20c.1.30 Patch Notes

<a id="4a957c95b77683ce"></a>
#### <kbd>ISSUE-4478</kbd> The setNetworkTimeout behavior of the JDBC connection class has been changed from asynchronous to synchronous.

<a id="a7d7ac79cef1edda"></a>
##### Description

The internal setNetworkTimeout() behavior of of the Connection class has been changed from asynchronous to synchronous.

<a id="ad8d581c92ee2310"></a>
##### Symptom

In the previous asynchronous implementation, requests to configure the network timeout returned immediately, while the actual timeout configuration was performed in a separate thread.  
As a result, SQL statements executed immediately after calling setNetworkTimeout() could run before the new timeout value was applied. Consequently, the timeout might not behave as expected, and the timing of the timeout configuration could be inconsistent.

<a id="bd65962ba62a38ab"></a>
##### Workaround

Wait for a certain period of time after calling setNetworkTimeout(), or execute SQL statements only after the timeout setting is expected to be applied.

<a id="1da1432fa11e679f"></a>
#### <kbd>ISSUE-8272</kbd> During view projection pruning, aggregations referenced by other targets were incorrectly removed when unused columns were pruned from a view, and this issue has been fixed.

<a id="a4808d681bda5060"></a>
##### Description

During view projection pruning, aggregations referenced by other targets were incorrectly removed when unused columns were pruned from a view.

<a id="f141de832c53e1f0"></a>
##### Symptom

Executing the following query causes an abnormal termination.

```
DROP VIEW IF EXISTS v1;

CREATE VIEW v1( sum1, sum2 )
AS
SELECT
  SUM(c2),
  SUM(c2) - SUM(c2)
FROM ( SELECT 1, 2 FROM dual 
       UNION ALL 
       SELECT 1, 2 FROM dual ) as v2( c1, c2 )
GROUP BY c1
ORDER BY c1;
COMMIT;

--# Query that causes an abnormal termination
SELECT sum2 FROM v1;
```

After the fix, the above query executes successfully and returns the following result.

```
DROP VIEW IF EXISTS v1;

CREATE VIEW v1( sum1, sum2 )
AS
SELECT
  SUM(c2),
  SUM(c2) - SUM(c2)
FROM ( SELECT 1, 2 FROM dual 
       UNION ALL 
       SELECT 1, 2 FROM dual ) as v2( c1, c2 )
GROUP BY c1
ORDER BY c1;
COMMIT;

SELECT sum2 FROM v1;

SUM2
----
   0

1 row selected.
```

<a id="d0f1fde2097b936e"></a>
##### Workaround

The patch is required.

<a id="88bd98ec175a5ef2"></a>
### 20c.1.29 Patch Notes

<a id="e6485819518c3741"></a>
#### <kbd>ISSUE-4478</kbd> The getNetworkTimeout and setNetworkTimeout methods of the JDBC connection class are supported.

<a id="0b2e76cefc1ac277"></a>
##### Description

The getNetworkTimeout and setNetworkTimeout methods of the connection class are supported.

<a id="2334811b09a2a23e"></a>
##### Symptom

N/A

<a id="ad4e9a495be601e8"></a>
##### Workaround

The patch is required.

<a id="c9c00f7ded88038a"></a>
#### <kbd>ISSUE-8058</kbd> The pthread_yield compatibility issue in glibc 2.34 has been fixed.

<a id="81b79c80e5d4e29f"></a>
##### Description

In the glibc 2.34 environment, referencing pthread_yield() caused a compatibility issue that could lead to a link failure of the GOLDILOCKS shared library. To address this, the thread yield implementation has been modified to preferentially use the standard sched_yield() API, ensuring build compatibility with glibc 2.34-based systems.

<a id="615c7eabf2ee9047"></a>
##### Symptom

When building an application in a glibc 2.34 environment, the final linking stage could fail because the GOLDILOCKS shared library was unable to resolve the pthread_yield symbol. A representative error message is shown below:  
• `undefined reference to 'pthread_yield'`

<a id="3b8190801f925e80"></a>
##### Workaround

Use an environment with a glibc version earlier than 2.34.

<a id="b428fa5e24704638"></a>
#### <kbd>ISSUE-7805</kbd> The issue where memory allocated during the handling of the ODBC LONG VARCHAR and LONG VARBINARY types was not properly released has been fixed.

<a id="d64de6c0da40f5ff"></a>
##### Description

A memory leak occurred for LONG VARCHAR and LONG VARBINARY columns during metadata reconstruction when the table schema was altered during a FETCH and another FETCH was performed on the same table.

<a id="dbd6fca9c54edffa"></a>
##### Symptom

In a client-server (CS) environment, when querying data through ODBC, altering the table schema via an ALTER statement during a FETCH operation triggers metadata reconstruction. If the table contains LONG VARCHAR or LONG VARBINARY columns, memory dynamically allocated for those column types was not released properly, resulting in a memory leak.

<a id="dd082dd33a2624a3"></a>
##### Workaround

Before this issue was fixed, the safest approach was to avoid altering the table schema during a FETCH operation. If altering the schema was unavoidable, the affected SQLHSTMT handle had to be reallocated by calling SQLFreeHandle followed by SQLAllocHandle.

<a id="ac05bcf4106d48c9"></a>
#### <kbd>ISSUE-7782</kbd> A parse option has been added to gpec.

<a id="86979bfa39712969"></a>
##### Description

The parse option has been added to gpec to control source parsing. The option can be set to none or partial, and if not specified, the default value is partial.

<a id="a1e9875985c62898"></a>
##### Symptom

N/A

<a id="0963fb92de23e8fb"></a>
##### Workaround

The patch is required.

<a id="f771f3db9a768e4f"></a>
#### <kbd>ISSUE-7782</kbd> The code handling behavior of the gpec preprocessor has been modified.

<a id="b77ff45d029ea0ac"></a>
##### Description

The gpec preprocessor has been updated to change how it handles code in branches that evaluate to false (#if, #elif, #else, #ifdef, #ifndef).  
Before this update, code in false branches was removed from the output. It now remains intact and is included in the output.

<a id="4dc0844844d42ca1"></a>
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

<a id="7c78e7106e4ddd17"></a>
##### Workaround

Preprocessor conditions and macros used in gc files should be defined within header files included using EXEC SQL INCLUDE.

<a id="97f3f0dd03af1459"></a>
#### <kbd>ISSUE-7743</kbd> An issue that occurred while processing nested #if / #endif directives in the gpec preprocessor has been fixed.

<a id="d2d3351273b078cd"></a>
##### Description

When processing #if preprocessor directives, the gpec preprocessor removes (replaces with empty strings) all statements up to the corresponding #endif directive if the condition is evaluated as false.  
However, when #if / #endif directives were used in a nested structure, some statements within the inner preprocessor blocks were not removed correctly. This issue has been identified and fixed.  
This fix applies not only to #if directives but also to all conditional preprocessor directives, including #elif, #else, #ifdef, and #ifndef.

<a id="3da01747b17b4788"></a>
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

<a id="68fceefd8af69a08"></a>
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

<a id="5751e501c8f68721"></a>
#### <kbd>ISSUE-7353</kbd> Fixed missing data issue when changing array size during ODBC fetch

<a id="1522e8c8d315d624"></a>
##### Description

An issue was identified in the ODBC client-server environment where changing the array size dynamically during data fetch caused data retrieval to fail. This issue has been resolved.

<a id="dddbcf7fa75c81b1"></a>
##### Symptom

When retrieving data using ODBC in a client-server (CS) environment, an issue occurred where data could not be fetched correctly if the array size was changed during the fetch operation. This problem commonly appeared when using the SQLExtendedFetch, SQLFetch, and SQLFetchScroll functions, and was particularly noticeable when the fetch started with a small array size (e.g., 1 row) and was later changed to a larger array size (e.g., 100 rows).

As a specific symptom, after changing the SQL_ROWSET_SIZE or SQL_ATTR_ROW_ARRAY_SIZE attribute, SQL_NO_DATA was returned prematurely, resulting in only a subset of the data being retrieved even though more data was actually available.

<a id="3f7c1d0f3e6019dc"></a>
##### Workaround

Prior to applying the patch for this issue, the most reliable approach was to keep the array size fixed rather than changing it. If changing the array size was unavoidable, the recommended method was to close the current cursor using the SQLCloseCursor function and then re-execute the query so that the fetch would begin with the new array size. When stability was more important than performance, the array size could be set to 1 to fetch data one row at a time.

<a id="661e277e62caa095"></a>
#### <kbd>ISSUE-6575</kbd> An error occurs when only the fields of a record type variable are specified in the INTO clause of a FETCH statement.

<a id="db0cdcd6e0264be2"></a>
##### Description

An error occurs if fields of a record type variable are specified, even when the number of targets of the cursor in the FETCH statement matches the number of targets in the INTO clause.

<a id="ab705dac2fc001f1"></a>
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

<a id="dcbe9e709d338b0c"></a>
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

<a id="72cab9e23364656a"></a>
#### <kbd>ISSUE-6574</kbd> The boundary of the member info array may be violated during the GSI REBUILD process.

<a id="492879f0957ff9c7"></a>
##### Description

If rebuilding the GSI after dropping a cluster member, the system may terminate abnormally.

<a id="3070890816340785"></a>
##### Symptom

Clearing the cluster member and rebuilding the GSI after dropping one or more cluster nodes as follows below may cause the system to terminate abnormally.

```
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;
Database altered.

ALTER TABLE T1 REBALANCE;
Table altered.

ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX;
```

<a id="4a4cf60ee1299063"></a>
##### Workaround

The patch is required.

<a id="15f2e9845ff3435a"></a>
#### <kbd>ISSUE-6557</kbd> When using an outer join, if functions such as DECODE, stored functions, or CONCAT that include columns from the right table are in the WHERE clause, it can lead to incorrect results.

<a id="6bcf4a621e1ef831"></a>
##### Description

When functions such as DECODE, stored functions, or CONCAT that include columns from the right table exist in the WHERE clause, the following outer join operation elimination should not be applied; however, it was actually applied, resulting in an error.

- The left outer join was transformed into an inner join.
- The full outer join was transformed into a left outer join.

<a id="990c6dcf60da7c18"></a>
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

<a id="ce6d24f7a0d2fb76"></a>
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

<a id="606207cf09967647"></a>
#### <kbd>ISSUE-4334</kbd> It fails to join the node due to the SCN difference when ascending to Global Open.

<a id="18fbb0acf30ac2e0"></a>
##### Description

It fails to join a cluster because the scn of a specific member is smaller than a maximum scn of the cluster, and this error has been fixed.

<a id="023fe2dc59f2e4d9"></a>
##### Symptom

It can not ascend to Global Open with the following error.

```
gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

ERR-42000(16410): Startup driver node must have the latest data - a suitable startup driver node is 'G1N1' member
```

<a id="cbda8a8aeb1755c4"></a>
##### Workaround

The patch is required.

<a id="941cfd8b2c72b5eb"></a>
#### <kbd>ISSUE-6129</kbd> When executing *prepare/execute* on the global connection, a valid plan cache may be dropped.

<a id="473c98ffcd405376"></a>
##### Description

It has been occurred from version 20c.1.12.

When executing prepare/execute on the global connection, a valid plan cache is dropped at the first execute and the new plan cache is created, and this error has been fixed.

<a id="999f23b6e2ff89c9"></a>
##### Symptom

Execute prepare/execute with multiple gsqlnet in the global connection environment as follows.

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1111

gSQL> \prepare sql SELECT * FROM t1 WHERE sk = :v1;

SQL prepared.

gSQL> \exec

  SK
----
1111

1 row selected.
```

Then, enquire the status of the plan cache to find the dropped plan cache as follows.

```
SELECT COUNT(*) FROM x$sql_cache WHERE dropped IS TRUE;

COUNT(*)
--------
       2

1 row selected.
```

<a id="bf0ae6c62205d204"></a>
##### Workaround

The patch is required.

<a id="461bcc7a2c12e79a"></a>
#### <kbd>ISSUE-4575</kbd> The identical SQL statement is redundantly cached in the embedded SQL.

<a id="20a2efe24d57d521"></a>
##### Description

The embedded SQL reuses the identical SQL by caching DML and the query statement when using the identical SQL. If char pointer is used as a host variable, then the identical SQL statement is redundantly cached.

<a id="5ba3e45f74658dbb"></a>
##### Symptom

If a char pointer is used as a host variable and the string length of this char pointer changes as follows, then a new SQL statement is created.

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

<a id="cac56fa95503fce3"></a>
##### Workaround

Use a char array instead of using the char pointer as a host variable.

<a id="619a63e99c857ff7"></a>
### 20c.1.28 Patch Notes

<a id="91f2ebe95c6ff2aa"></a>
#### <kbd>ISSUE-5828</kbd> The join query including ROWNUM should not be sent to the remote node, but sometimes it is sent.

<a id="6e83356eb853f428"></a>
##### Description

The join query including ROWNUM should not be sent to the remote node. If each node stores data in a different order then the result may be wrong even though it is a clone table.

<a id="65b28a8fffd00b67"></a>
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

<a id="3efc5ca89db71fc3"></a>
##### Workaround

Use */*+ LOCAL_JOIN(Y) */* hint.

<a id="3eaf9d7ae92ea535"></a>
#### <kbd>ISSUE-5665</kbd> If the join including three or more tables is performed by using the instant nested loop join method, then the result may be wrong.

<a id="47bb8c19f55cd004"></a>
##### Description

If the join including three or more tables is performed by using the instant nested loop join method, then the result may be wrong.

<a id="9929c98caef449a4"></a>
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

<a id="0f62e963135b6826"></a>
##### Workaround

Use a hint other than USE_INL(t1). For example, use USE_NL(t1), USE_HASH(t1) or USE_MERGE(t1).

<a id="f85eb3843b13efa5"></a>
#### <kbd>ISSUE-4863</kbd> The lock is not switched to the optimistic mode after REBALANCE.

<a id="f53196264b6fa225"></a>
##### Description

The lock which is switched to the pessimistic mode during ALTER TABLE REBALANCE, is not switched to the optimistic mode, and it may downgrade the performance.

<a id="283524157309ef4c"></a>
##### Symptom

If performing ALTER TABLE REBALANCE ONLINE when DML occurs, then it may downgrade the performance.

<a id="87cfeb65bc4eca80"></a>
##### Workaround

The patch is required.

<a id="ea3ce5fea276904f"></a>
### 20c.1.27 Patch Notes

<a id="e3b61ad3d204765c"></a>
#### <kbd>ISSUE-4334</kbd> It fails to join the node due to the SCN difference when ascending to Global Open.

<a id="46695746eede14f1"></a>
##### Description

It fails to join a cluster because the scn of a specific member is smaller than a maximum scn of the cluster, and this error has been fixed.

<a id="2fa24941aed9f5c0"></a>
##### Symptom

It can not ascend to Global Open with the following error.

```
gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

ERR-42000(16410): Startup driver node must have the latest data - a suitable startup driver node is 'G1N1' member
```

<a id="2170f2febfea62d2"></a>
##### Workaround

The patch is required.

<a id="c795d898c351635e"></a>
#### <kbd>ISSUE-5505</kbd> If the access method for leftmost table in the join is the unique index access, and only part of key columns in the group by belong to the unique index, then the result may be wrong.

<a id="fcc6d485eec57c79"></a>
##### Description

If the access method for leftmost table in the join is the unique index access, and only part of key columns in the group by belong to the unique index, then the result may be wrong.

<a id="e2c43c5331e4be0e"></a>
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

<a id="ff5e87acdd955c42"></a>
##### Workaround

Use */*+ USE_GROUP_HASH */* hint.

<a id="ced4b4da1ec17c20"></a>
#### <kbd>ISSUE-5353</kbd> When connecting and disconnecting by using the window ODBC, then the number of program handles increase and this error has been fixed.

<a id="36f9c05ab05ff437"></a>
##### Description

When repeatedly connecting and disconnecting by using the window ODBC, then the number of entire program handles increase and this error has been fixed.

<a id="523c954ae42f7ed4"></a>
##### Symptom

When repeatedly connecting and disconnecting by using the window ODBC, then the number of entire program handles increase.

<a id="7b97fd60363fd539"></a>
##### Workaround

The patch is required.

<a id="c52831e81dc942f2"></a>
#### <kbd>ISSUE-5367</kbd> Statement pooling feature has been added in JDBC.

<a id="63a484129bcb2bd1"></a>
##### Description

It supports the statement pooling feature.

<a id="58a6a62378c45118"></a>
##### Symptom

N/A

<a id="6af601c8efed9331"></a>
##### Workaround

The patch is required.

<a id="aa674cc6679245ea"></a>
#### <kbd>ISSUE-5344</kbd> When performing view projection pruning it deletes the column used in the upper block.

<a id="f4dd89bdd498215c"></a>
##### Description

If the following conditions are satisfied, the server may be abnormally terminated due to improperly performed view projection pruning.

- *group by* or *order by* exists within a view.
- expr to be deleted from the view's select list is an argument of another function expression.

<a id="f0c43a17fb22a4e0"></a>
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

<a id="65b183d1a77be466"></a>
##### Workaround

The patch is required.

<a id="aeaecd9d7c4aa210"></a>
#### <kbd>ISSUE-4234</kbd> When performing PSM DDL after ADD MEMBER, then a dictionary integrity constraint violation occurs for the ROUTINE primary key.

<a id="925b9c77995d2c5b"></a>
##### Description

When performing PSM DDL after ADD MEMBER, then a dictionary integrity constraint violation occurs for the ROUTINE primary key, and this error has been fixed.

<a id="d24a401f28e90cfe"></a>
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

<a id="6c1a134e5747b6a6"></a>
##### Workaround

The patch is required.

<a id="5924ce720ad3ed3b"></a>
#### <kbd>ISSUE-5162</kbd> Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC, it may wait longer than the settings, and this error has been fixed.

<a id="e6156f244ab49f46"></a>
##### Description

Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC to detect the network disconnection, it may wait longer than the given timeout setting, and this error has been fixed.

<a id="f3e3767107c362d8"></a>
##### Symptom

Even when SQL_ATTR_CONNECTION_TIMEOUT is set in ODBC, it can not detect the network disconnection in a specific situation, so it keeps waiting for the server's response in ODBC.

<a id="51fd28f1d1652eb7"></a>
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

<a id="0282878196a837fe"></a>
#### <kbd>ISSUE-5124</kbd> If it fails to allocating dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="9f3b1d8084e3e29d"></a>
##### Description

If it fails to allocating dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="c0ddd48d8ea1d1ec"></a>
##### Symptom

If it fails while multiple threads allocate a single dynamic memory, then it may kill the server due to the simultaneity issue.

<a id="d288df4f126dbc71"></a>
##### Workaround

The patch is required.

<a id="741a260e6b2d80fd"></a>
### 20c.1.26 Patch Notes

<a id="81c364c7129f50d7"></a>
#### <kbd>ISSUE-4933</kbd> If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client.

<a id="ff98f06fc536b5ae"></a>
##### Description

If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client.

<a id="0279b8ba1988f630"></a>
##### Symptom

If the server becomes unavailable while using JDBC XA, then it should transfer XA error to the client. However, in reality, it does not transfer XA error and it is operated as if it succeeds.

<a id="b90deab9956c5738"></a>
##### Workaround

The patch is required.

<a id="dcba383285a8c027"></a>
#### <kbd>ISSUE-4873</kbd> It supports XA rollback feature for XA transaction which is not dissociated from the session.

<a id="b23b803e470b551f"></a>
##### Description

XA transaction is associated with the session until performing xa end, and to commit or rollback the XA transaction, it should be dissociated from the session. However, other DBMS support the rollback feature even when the transaction is not dissociated from the session. Therefore, it has been improved to support the same feature.

<a id="4788afa05a0419d5"></a>
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

<a id="856b37b8a27e0511"></a>
##### Workaround

The patch is required.

<a id="0df2cad6404e598a"></a>
#### <kbd>ISSUE-4753</kbd> When enquiring USER_TABLES, the global temporary table is not viewed.

<a id="586e86b453df0d4d"></a>
##### Description

When enquiring the dictionary view such as USER_TABLES, ALL_TABLES and DBA_TABLES, the global temporary table is not viewed.

<a id="0f652b8ac518421f"></a>
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

<a id="c85d1369a10e728d"></a>
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

<a id="7133c852c93fc990"></a>
#### <kbd>ISSUE-4709</kbd> Query execution for the local node may fail on local open phase.

<a id="d066fb478980bcb4"></a>
##### Description

If enquiring the table by connecting to the node on local open phase in cluster environment, then an error occurs.

<a id="72b185efd0eee230"></a>
##### Symptom

If the connected node is on local open phase, then it can not access the remote node but it can access the local node. However, if it determines that the node on local open phase can not access the local node, then the query fails.

The following is an example of an error occurred when executing the query on G1N1 on local open phase.

```
gSQL> SELECT * FROM v$datafile;

ERR-HY000(16354): connection of member 'G1N1' is broken
```

It determines whether the current node can access a specific node based on the connection information. However, if it can not refer to the connection information in case when it is on local open phase, then it may determine that it can not access the current node either.

It is modified to determine that it can access the current node even when it can not refer to the connection information.

<a id="e34df7fdc7b0775c"></a>
##### Workaround

The patch is required.

<a id="213a832c30a82e8f"></a>
#### <kbd>ISSUE-4696</kbd> View columns have been added to view the update master information of the cluster table.

<a id="626311be67c66a77"></a>
##### Description

The update master in the cluster table is a member node where DML is first performed when DML occurs in the table.

The followings affect determining the update master of each cluster table.

- Positioning cluster table
- Position of members in the cluster group
- Whether it is online/ offline
- Whether to perform rebalance

IS_UPDATE_MASTER column has been added to the following dictionary views to easily view the update master information which is subject to change during the operation.

- [DBA_TAB_PLACE](../part-02-administration-manual/9-database-information.md#bc911a2bb2214059)
- [ALL_TAB_PLACE](../part-02-administration-manual/9-database-information.md#61d5ecd55404bcaa)
- [USER_TAB_PLACE](../part-02-administration-manual/9-database-information.md#989f5b17033d74c8)

<a id="6ee1d571d99980a2"></a>
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

<a id="28c9668ce07fe0d5"></a>
##### Workaround

The patch is required.

<a id="4d8926563614cd3d"></a>
#### <kbd>ISSUE-4609</kbd> When using two or more subquery expressions including a join combine, then a segment fault occurs.

<a id="dbad76111bde28f5"></a>
##### Description

When referring to the information of the subquery expression in the statement in which two or more subquery expressions including a join combine are used, then a segment fault occurs.

The error occurred in the following clauses.

- TARGET clause
- WHERE clause
- HAVING clause
- ORDER BY clause

<a id="3a4e070e5beaf07d"></a>
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

<a id="e613834405e287eb"></a>
##### Workaround

The patch is required.

<a id="d51199cf6b429247"></a>
#### <kbd>ISSUE-4589</kbd> Complex view merging was executed even though SELECT FOR UPDATE, UPDATE, DELETE does not support the complex view merging.

<a id="9ec94dd5dd1d6a57"></a>
##### Description

Complex view merging was executed even though SELECT FOR UPDATE, UPDATE, DELETE does not support the complex view merging.

<a id="1d8213f0a749f490"></a>
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

<a id="1a1f8e3c83f2d1ac"></a>
##### Workaround

The patch is required.

<a id="c59bddd576d4832b"></a>
#### <kbd>ISSUE-4566</kbd> It can not process the overflow even when the number of digits increased after the rounding off while converting the numeric type to NUMBER type.

<a id="7d02dcb67790c4e6"></a>
##### Description

It can not process the overflow even when the number of digits increased after the rounding off while converting the numeric type to NUMBER type.

<a id="b77cd52413f2755b"></a>
##### Symptom

The following query was supposed to cause an overflow error.

```
gSQL> SELECT CAST( 9999999999.9 AS NUMBER(10,0)) FROM dual;

CAST( 9999999999.9 AS NUMBER(10,0))
-----------------------------------
                        10000000000

1 row selected.
```

<a id="9c073c1a615c7242"></a>
##### Workaround

Convert it to NUMBER type after convert it to the character type.

```
gSQL> SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual;

ERR-22003(12060): data is outside the range of the data type to which the number is being converted : 
SELECT CAST( TO_CHAR( 9999999999.9 ) AS NUMBER(10,0) ) FROM dual
       *
ERROR at line 1:
```

<a id="3293f6edaec2f2bb"></a>
#### <kbd>ISSUE-4559</kbd> The trace log is output as TRACE_LONG_RUN_CURSOR even when the cursor does not exist in SELECT INTO statement.

<a id="b1c1e6dc342f464b"></a>
##### Description

TRACE_LONG_RUN_CURSOR property records the long run cursor which exceeds the specified time on the trace log. However, the trace log is output as TRACE_LONG_RUN_CURSOR even though SELECT INTO statement does not require the cursor, and this error has been fixed.

<a id="aad816c4c9a40b54"></a>
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

<a id="d70108492813739c"></a>
##### Workaround

The patch is required.

<a id="f9809e659e95227b"></a>
#### <kbd>ISSUE-4537</kbd> When performing ADD MEMBER after the incorrect DROP TABLESPACE statement succeeds, then the new member is abnormally terminated.

<a id="04e54d0b99d76f28"></a>
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

<a id="804b67ce89e5045b"></a>
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

<a id="550e8a16abb94796"></a>
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

<a id="0f0070fe7bf7dadc"></a>
#### <kbd>ISSUE-4500</kbd> If performing the index scan by using another OR condition when the join condition includes OR condition, then the query waits infinitely.

<a id="cd5a6fb851b68ef7"></a>
##### Description

When the join combine method is selected by the join condition including OR condition, and the column included in the join combine is referenced in the relation to which another join belongs, then it waits infinitely.

<a id="cd3343e86c66b5b2"></a>
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

<a id="afaa86fe61e9e08f"></a>
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

<a id="22b0ddad19489282"></a>
#### <kbd>ISSUE-4480</kbd> When defining %TYPE which refers to the column whose reserved word is the column name, then an error occurs.

<a id="fb21acf85c7fed18"></a>
##### Description

When defining %TYPE which refers to the column whose reserved word is the column name, then an error occurs.

<a id="49a4c3bd50a1f205"></a>
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

<a id="24a4ff91995a2c0e"></a>
##### Workaround

The patch is required.

<a id="710bcd04a8c474fc"></a>
#### <kbd>ISSUE-4472</kbd> When outputting DDL_DB, the schema privilege DDL is not output.

<a id="1409edce3b9978ba"></a>
##### Description

If outputting DDL_DB when two or more schema are created, then only part of them are output and other are not output.

<a id="38249625dd8767cd"></a>
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

<a id="544110f439ea7212"></a>
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

<a id="544649748289edbd"></a>
#### <kbd>ISSUE-4471</kbd> When creating TABLESPACE with DISK TABLESPACE statement which was output with DDL_DB command, then a syntax error occurs.

<a id="77607fa6394dd286"></a>
##### Description

When creating TABLESPACE with CREATE DISK TABLESPACE statement which was output with DDL_DB command, then a syntax error occurs.

<a id="c4aa14ccb321c63e"></a>
##### Symptom

1. Create the tablespace.

```
gSQL> CREATE DISK DATA TABLESPACE disk_test_01 DATAFILE 'DISK_TEST_01.dbf' SIZE 100M;
COMMIT;
```

2. Input *\ddl_db*.

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

3. Input tablespace DDL statement which was output by executing *\ddl_db* command in step 2.

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

<a id="ef6adeacd588d6f5"></a>
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

<a id="db685c582018f1c3"></a>
#### <kbd>ISSUE-4454</kbd> When TRACE_LOG_ID = xxxxx1 is set, the performance time of the query per section is not output on the trace log.

<a id="7804efed3a268f29"></a>
##### Description

When TRACE_LOG_ID = xxxxx1 is set, the performance time of the query per section is not output on the trace log. The ones place in TRACE_LOG_ID is the flag which determines whether to output the performance time per section, and it outputs the time when the value is 1.

<a id="f82aabeeab2f99ce"></a>
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

<a id="59f58d1ad34a64af"></a>
##### Workaround

The patch is required.

<a id="9c9d293d6ce5b949"></a>
#### <kbd>ISSUE-4317</kbd> It supports SQL_ATTR_CONNECTION_TIMEOUT property.

<a id="55b2ad43451917b7"></a>
##### Description

If the network is unstable, then the client can not receive the response and stays in blocking status, after sending a query to the server. Therefore, it supports SQL_ATTR_CONNECTION_TIMEOUT property of SQLSetConnectAttr() to solve this problem.

If SQL_ATTR_CONNECTION_TIMEOUT value is set, then the client sends a query to the server and waits for the response as long as the set time. If it can not get the response for the set time, then the client cuts the connection to the server and returns *HYT01 Connection timeout expired* error.

<a id="fb9af87647aab64e"></a>
##### Symptom

If the network is unstable, then the client waits for the set time after requesting the response to the server.

<a id="931f64f001555f4f"></a>
##### Workaround

Alter the kernel property value as follows, so that it can quickly detects whether the connection between the client and the server has an error.

```
net.ipv4.tcp_keepalive_time = 3
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.tcp_keepalive_intvl = 3
net.ipv4.tcp_retries2 = 5
```

<a id="ffb07ad92da05d5f"></a>
#### <kbd>ISSUE-4031</kbd> The column name of the table is not properly displayed in .Net Framework.

<a id="8a0615218f2c44f0"></a>
##### Description

When querying the column name in SQLColAttribute() and SQLGetDescField(), SQL_DESC_LABEL property, SQL_DESC_NAME property or SQL_DESC_BASE_COLUMN_NAME property is used. SQL_DESC_LABEL returns the label, when the column has a label. SQL_DESC_NAME returns an alias when the column has an alias. And, SQL_DESC_BASE_COLUMN_NAME returns the column name.

.Net Framework, data provider for ODBC, uses SQL_DESC_NAME when querying the column name, and the column name is unintentionally retrieved when the label is given to the column. Therefore, DOT_NET_FOR_ODBC, the connection property, has been added for Net Framework to solve this problem.

<a id="7079d30761330346"></a>
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

<a id="4e1ac2e06cb4a439"></a>
##### Workaround

The patch is required.

<a id="2eb020938bc04d70"></a>
#### <kbd>ISSUE-4254</kbd> When executing a subquery containing DISTINCT in the cluster system, then a syntax error occurs in the remote server.

<a id="ee9d68700320ca7c"></a>
##### Description

If configuring a cluster query by using the query and executing it when the subquery containing DISTINCT is described and the subquery target which is not referenced exists in the cluster system, then a syntax error occurs in the remote server.  
It is because the number of target expressions in the created cluster query and that of view column names do not match.

<a id="190aaa172471d1f8"></a>
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

<a id="868a754d00f62f81"></a>
##### Workaround

Convert DISTINCT statement into GROUP BY statement.

If GROUP BY is not described within the query in which DISTINCT is described, then define all DISTINCT targets by using GROUP BY and omit DISTINCT.

```
gSQL> SELECT v1.i1 FROM ( SELECT i1, i2 FROM t1 GROUP BY i1, i2 ) v1;

no rows selected.
```

<a id="42f29e5a5ad877b9"></a>
### 20c.1.25 Patch Notes

<a id="8789146f2d6972a1"></a>
#### <kbd>ISSUE-4246</kbd> When using AT clause in EXEC SQL AUTOCOMMIT statement, then an error occurs.

<a id="931003a89b280320"></a>
##### Description

AT clause is not recognizable in *EXEC SQL AT :db_name AUTOCOMMIT* statement, so *INVALID HANDLE* error occurs.

<a id="2a572ba674662143"></a>
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

<a id="f77eca99f2058227"></a>
##### Workaround

The patch is required.

<a id="86c75543186b6eb7"></a>
#### <kbd>ISSUE-4215</kbd> If the variable of using clause in EXECUTE IMMEDIATE is IN OUT type, then an error occurs.

<a id="ce6703a2bbba5dcf"></a>
##### Description

If the variable bind type of using clause in EXECUTE IMMEDIATE is IN OUT type, then an error occurs.

<a id="95e88a5142905aa8"></a>
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

<a id="a9a0a76729aee706"></a>
##### Workaround

The patch is required.

<a id="dbba13caaec6a17f"></a>
#### <kbd>ISSUE-4189</kbd> If creating the procedure whose parameter is consisted in an order of ref cursor, DB type, and executing it, then an error occurs.

<a id="358ccad90057537e"></a>
##### Description

If creating the procedure whose parameter is consisted in an order of ref cursor, DB type, and executing it, then an error occurs.

<a id="7dff2cd07b4e62c5"></a>
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

<a id="0211c8f01b98817e"></a>
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

<a id="73d8ed7027b46ae1"></a>
### 20c.1.24 Patch Notes

<a id="d7335c8fa6df8ab8"></a>
#### <kbd>ISSUE-4178</kbd> DBMS_OUTPUT.PUT_LINE() is output twice.

<a id="cc9fde0218ae6c84"></a>
##### Description

When DBMS_OUTPUT.PUT_LINE() calls a function including an actual parameter, DBMS_OUTPUT.PUT_LINE(), then the contents of the function are output twice.

<a id="1ba7d1c48e71f8c4"></a>
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

<a id="c3a267a67b578c5b"></a>
##### Workaround

The patch is required.

<a id="a85fe40a4188b13d"></a>
#### <kbd>ISSUE-4135</kbd> When a socket error occurs in cluster environment, then the system hangs.

<a id="2af0f21962790a4d"></a>
##### Description

When a socket error occurs on a sender thread in cluster environment, then it can not send the message to the remote member, so the entire system hangs. It has been modified to failover the remote member when a socket error occurs on a sender/ receiver thread to solve this problem.

<a id="e4f78a4dbf4526f6"></a>
##### Symptom

When a network error occurs in cluster, then it checks the heartbeat and failover occurs. In this case, if an error occurs only in a specific socket which is not a heartbeat among threads sending and receiving message with the remote member, then it can not receive the response, so the entire system hangs.

<a id="27e59794a4c0f5b5"></a>
##### Workaround

The patch is required.

<a id="5228c81eb73a1d1a"></a>
#### <kbd>ISSUE-4174</kbd> The performance of when the local caches of the global sequence are run out has been improved.

<a id="212a68cc7948f971"></a>
##### Description

The performance was severely downgraded when the local cache of the global sequence were run out, and this problem has been solved.

<a id="cc08b11591580004"></a>
##### Symptom

All servers using sequences proceed the operations to secure local caches from the global cache when the local caches are run out. In this case, they try to competitively secure the remote cserver, so it may downgrade the performance severely.

<a id="8733b9260bb3f69b"></a>
##### Workaround

The patch is required.

<a id="cce9893e4a7188bd"></a>
#### <kbd>ISSUE-4182</kbd> When restarting cyfile, the recovery may not be operated normally.

<a id="f3c0bcc1cc05d9c4"></a>
##### Description

If stopping and restarting cyfile while multiple transactions are simultaneously being processed, then the recovery may not be operated normally, and this problem has been solved.

<a id="098d41a40921efde"></a>
##### Symptom

If stopping and restarting cyfile while transactions are being processed in multiple sessions, then it causes a trouble because the previously stored transaction is stored again in the data file.

<a id="8ba55fa3ea4cd668"></a>
##### Workaround

The patch is required.

<a id="d6da14de44019670"></a>
### 20c.1.23 Patch Notes

<a id="e93bf6d8268227d7"></a>
#### <kbd>ISSUE-4088</kbd> If the user explicitly performs OUT binding the bind parameter in the function including an out parameter in ODBC or JDBC, then an error occurs.

<a id="fee68b33fe8fd26a"></a>
##### Description

If the user explicitly performs OUT binding the bind parameter in the function including an out parameter in ODBC or JDBC, then an error occurs.

<a id="35dfbe926e3ec1bb"></a>
##### Symptom

Though the function parameter is an out type and the user explicitly performed OUT binding the bind parameter according to the parameter type in ODBC program, but an error occurs.

```
CREATE OR REPLACE FUNCTION func1( a1 OUT INTEGER )
RETURN INTEGER
IS
BEGIN
  a1 := 110;
  RETURN 10;
END;
/
```

```
sRet = SQLPrepare( sStmt1,
                   (SQLCHAR*)"CALL FUNC1(?) INTO ?",
                   SQL_NTS );  
        
sRet = SQLBindParameter( sStmt1,
                         1,  
                         SQL_PARAM_OUTPUT,
                         SQL_C_SLONG,
                         SQL_INTEGER,
                         0,  
                         0,  
                         &sV1,
                         0,  
                         &sV1Ind );

sRet = SQLBindParameter( sStmt1,
                         2,  
                         SQL_PARAM_OUTPUT,
                         SQL_C_SLONG,
                         SQL_INTEGER,
                         0,
                         0,
                         &sV2,
                         0,
                         &sV2Ind ) );

sRet = SQLExecute( sStmt1 );
```

<a id="da713fdee6278d3b"></a>
##### Workaround

The patch is required.

<a id="4997fd3f28144df6"></a>
#### <kbd>ISSUE-4078</kbd> If the type with the default value is defined in the package field and another PSM object refers to it, then an error occurs.

<a id="4309fed0089c54f6"></a>
##### Description

If TYPE with the field including the default value is defined in the package and another PSM object refers to it, then an error occurs.

<a id="4d37cab0a7e9d511"></a>
##### Symptom

The following is an example of defining the type with the field including the default value in the package. If a procedure refers to it, then the syntax error occurs.

```
CREATE OR REPLACE PACKAGE pkg1 AS
  TYPE rec IS RECORD( f1 VARCHAR(10) := 'abcde' );
  v_rec rec;
  v_int INTEGER;
END;
/ 
Package created.

CREATE OR REPLACE PROCEDURE proc1( p1 IN pkg1.rec ) AS
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'p1 : ' || p1.f1 );
END;
/

ERR-42000(16062): syntax error : 
RETURN RETURN 'abcde' 
       ^    ^
Error at line 1
```

<a id="6b52c30d7a3dc4cc"></a>
##### Workaround

The patch is required.

<a id="0a0afd1ead290eda"></a>
#### <kbd>ISSUE-4081</kbd> TRACE_LONG_RUN_TIMER property has been added.

<a id="21cdce06758e6888"></a>
##### Description

[TRACE_LONG_RUN_TIMER](../part-02-administration-manual/10-server-property.md#e838aee7eaff0357) property has been added, and it controls the precision of the execution when using the following properties.

- TRACE_LONG_RUN_CURSOR
- TRACE_LONG_RUN_SQL

<a id="95861d8979c6d05a"></a>
##### Symptom

N/A

<a id="d0091cb3dd7b57c4"></a>
##### Workaround

The patch is required.

<a id="65517432b0e67168"></a>
#### <kbd>ISSUE-4045</kbd> BROADCAST_INDEX_REBUILD_PROTOCOL property has been added.

<a id="40c62520fc31848a"></a>
##### Description

[BROADCAST_INDEX_REBUILD_PROTOCOL](../part-02-administration-manual/10-server-property.md#4c6034f9c28ad9e5) property has been added, and it sets whether to simultaneously rebuild the indexes on all members when rebuilding the index in cluster environment.

<a id="2fa8cec3112eccc2"></a>
##### Symptom

N/A

<a id="59ffef8a04fd7418"></a>
##### Workaround

The patch is required.

<a id="efed53062be23b96"></a>
### 20c.1.22 Patch Notes

<a id="a1788e13282441fa"></a>
#### <kbd>ISSUE-4062</kbd> If an actual parameter does not exist when the formal parameter is %TYPE and has the default value, then an error occurs.

<a id="9922df49f629e07c"></a>
##### Description

If the actual parameter is not specified when executing PSM object whose formal parameter datatype is %TYPE and which has the default value, then an error occurs.

<a id="3ec70853a3ff6721"></a>
##### Symptom

When omitting the actual parameter as follows, then *wrong number of parameters* error occurs.

```
CREATE TABLE t1( c1 INTEGER, c2 INTEGER );

Table created.

CREATE OR REPLACE FUNCTION func1( p1 IN t1.c1%type default 100,
                                  p2 IN t1.c2%type default 200 )
RETURN INTEGER AS
BEGIN
  RETURN p1 + p2;
END;
/

Function created.

SELECT func1( 10 ) FROM DUAL;
```

<a id="4569b5e34f67b89d"></a>
##### Workaround

The patch is required.

<a id="14255ca89ef3866a"></a>
### 20c.1.21 Patch Notes

<a id="d6cdd62756ceabc9"></a>
#### <kbd>ISSUE-4049</kbd> When an error occurs over the entire CYCLONE slave group in cluster environment, then the data error occurs.

<a id="75b9921247f8b454"></a>
##### Description

The data error occurs when two or more groups exist in cluster environment. If manipulating the data in the group whose sharding table is terminated while the partial service is available because all members in the specific group are terminated, then the query fails while CYCLONE is normally operated.

<a id="d9614c0503f49350"></a>
##### Symptom

If *ERR-42000(16357) : must be accessible to at least one member of group 'GX'* error occurs on slave side, then CYCLONE is normally operated instead of being terminated, so the data error may occur.

<a id="e148e424b50f1cc1"></a>
##### Workaround

The patch is required.

<a id="29b51ba6e6a72026"></a>
### 20c.1.20 Patch Notes

<a id="620893e4d66ed05e"></a>
#### <kbd>ISSUE-4039</kbd> It rounds up the result of the operation which uses PSM variable in Cursor For Loop, then returns it.

<a id="26e4ea5806335dcf"></a>
##### Description

It rounds up the result of the operation which uses PSM variable in SELECT statement of Cursor For Loop, then returns it.

<a id="0d5265ab2d23f7d9"></a>
##### Symptom

It rounds up the result of the operation which uses PSM variable in SELECT statement of Cursor For Loop, then returns it as follows.

```
DECLARE
  v1 NUMBER;
  v2 NUMBER;
BEGIN
  v1 := 5.02;
  v2 := 5.01;

  FOR tmp IN ( SELECT v1 + v2 res FROM DUAL ) LOOP
    DBMS_OUTPUT.PUT_LINE( tmp.res );
  END LOOP;
END;
/

10
Anonymous PL block executed.
```

<a id="fe8ab01270987644"></a>
##### Workaround

Specify DATA TYPE by using CAST function in PSM variable.

```
DECLARE
  v1 NUMBER;
  v2 NUMBER;
BEGIN
  v1 := 5.02;
  v2 := 5.01;

  FOR tmp IN ( SELECT CASE(v1 as NUMBER) + v2 res FROM DUAL ) LOOP
    DBMS_OUTPUT.PUT_LINE( tmp.res );
  END LOOP;
END;
/

10.03
Anonymous PL block executed.
```

<a id="ff1ee92bbe68587c"></a>
#### <kbd>ISSUE-4042</kbd> If performing commit statement while performing Cursor For Loop statement, then an error occurs.

<a id="a672a4980ccd649e"></a>
##### Description

If performing commit statement while performing Cursor For Loop statement, then *cursor not open* error occurs.

<a id="e24caf9f29cf442f"></a>
##### Symptom

It closes the open cursor to perform commit, then commits it. Then, if closing the used cursor when terminating *cursor for loop* statement, *cursor is not open* error occurs because the cursor already has been closed beforehand.

```
BEGIN
  FOR cur1 IN ( SELECT r_c1 FROM r FOR UPDATE ) LOOP
    IF ( cur1.r_c1 = 2 ) THEN
      COMMIT;
      RETURN;
    END IF;
  END LOOP;
END;
/
```

<a id="0c3fc3f0efa23042"></a>
##### Workaround

Specify commit after *cursor for loop* statement is completed.

```
BEGIN
  FOR cur1 IN ( SELECT r_c1 FROM r FOR UPDATE ) LOOP
    IF ( cur1.r_c1 = 2 ) THEN
      RETURN;
    END IF;
  END LOOP;

  COMMIT;
END;
/
```

<a id="5a2a3024389c4a54"></a>
#### <kbd>ISSUE-4040</kbd> When using sequence after performing ALTER SEQUENCE in PSM, then the SELECT statement waits infinitely.

<a id="40fc4c68c13b2de8"></a>
##### Description

When using sequence after performing ALTER SEQUENCE in PSM in cluster environment, then the SELECT statement which uses the sequence waits infinitely.

<a id="d8eb40d58be23458"></a>
##### Symptom

When using sequence after performing ALTER SEQUENCE by using EXECUTE IMMEDIATE statement in PSM in cluster environment as follows, then the SELECT statement which uses the sequence waits infinitely.

```
DECLARE
    curr_val INTEGER;
BEGIN
    EXECUTE IMMEDIATE 'ALTER SEQUENCE seq CACHE 100';
    EXECUTE IMMEDIATE 'SELECT seq.nextval FROM DUAL' INTO curr_val; 
END;
/
```

<a id="ea7a210a53cacc64"></a>
##### Workaround

Specify COMMIT as follows after performing ALTER SEQUENCE statement.

```
DECLARE
    curr_val INTEGER;
BEGIN
    EXECUTE IMMEDIATE 'ALTER SEQUENCE seq CACHE 100';
    COMMIT;
    EXECUTE IMMEDIATE 'SELECT seq.nextval FROM DUAL' INTO curr_val; 
END;
/
```

<a id="e4788a31941aca6d"></a>
### 20c.1.19 Patch Notes

<a id="2a02051cc1fc6773"></a>
#### <kbd>ISSUE-4024</kbd> Savepoint hang may occur when an error occurs at the remote member in cluster.

<a id="274f547d6017c91f"></a>
##### Description

The savepoint statement may hang in a specific situation of cluster.

<a id="7717306c5c2b3693"></a>
##### Symptom

If the savepoint statement is performed after a specific member accessed by a transaction is abnormally terminated, then a hang may occur.

<a id="430f592d63dbcd7d"></a>
##### Workaround

The patch is required.

<a id="5e29501a4ab7dfe7"></a>
### 20c.1.18 Patch Notes

<a id="fd9384ca24a4e8dc"></a>
#### <kbd>ISSUE-4021</kbd> The program is abnormally terminated during the fetch cursor in the embedded SQL.

<a id="9eb7446b38e48e4b"></a>
##### Description

If the array size becomes bigger in FETCH CURSOR when reusing STANDING CURSOR in the embedded SQL, then the client program is abnormally terminated.

<a id="5e0b5c30ad3dd092"></a>
##### Symptom

If the array size becomes bigger during fetching the cursor when reusing the cursor as the following sample code, then the program is abnormally terminated.

```
int OpenCursor()
{
    printf( "DECLARE CRS_ ... \n");
    EXEC SQL DECLARE CRS_ CURSOR FOR
        SELECT ename FROM emp;
    if( sqlca.sqlcode != 0 )
        goto FINISH_LABEL;

    printf( "OPEN CRS_ ... \n");
    EXEC SQL OPEN CRS_;
    if( sqlca.sqlcode != 0 )
        goto FINISH_LABEL;

    return 0;

    FINISH_LABEL:

    return -1;
}

int FetchCursor()
{
    EXEC SQL BEGIN DECLARE SECTION;
    char  name[100];
    EXEC SQL END DECLARE SECTION;
    int  count = 0;

    printf( "ARRAY SIZE: 1\n" );
    printf( "FETCH CRS_ ... \n");

    while( 1 )
    {
        EXEC SQL FETCH CRS_ INTO :name;
        if( sqlca.sqlcode == 100 )
        {
            break;
        }

        if( sqlca.sqlcode != 0 )
            goto FINISH_LABEL;
        count++;
    }

    printf( "%d fetched.\n", count );
    
    printf( "CLOSE CRS_ ... \n\n");
    EXEC SQL CLOSE CRS_;
    if( sqlca.sqlcode != 0 )
        goto FINISH_LABEL;
    
    return 0;

    FINISH_LABEL:

    return -1;
}


int FetchCursorArray()
{
    EXEC SQL BEGIN DECLARE SECTION;
    char  name[20][100];
    EXEC SQL END DECLARE SECTION;
    int  count = 0;

    printf( "ARRAY SIZE: 20\n" );
    printf( "FETCH CRS_ ... \n");

    while( 1 )
    {
        EXEC SQL FETCH CRS_ INTO :name;
        if( sqlca.sqlcode == 100 )
        {
            break;
        }

        if( sqlca.sqlcode != 0 )
            goto FINISH_LABEL;
        count += sqlca.sqlerrd[2];
    }

    printf( "%d fetched.\n", count );
    
    printf( "CLOSE CRS_ ... \n\n");
    EXEC SQL CLOSE CRS_;
    if( sqlca.sqlcode != 0 )
        goto FINISH_LABEL;
    
    return 0;

    FINISH_LABEL:

    return -1;
}

int DoJob()
{
    if( OpenCursor() == -1 ) goto FINISH_LABEL;
    if( FetchCursor() == -1 ) goto FINISH_LABEL;

    if( OpenCursor() == -1 ) goto FINISH_LABEL;
    if( FetchCursorArray() == -1 ) goto FINISH_LABEL;
	return 0;
    FINISH_LABEL:
    return -1;
}
```

<a id="04d3eb0227f95029"></a>
##### Workaround

Set the size of the host variable used in FETCH CURSOR same when reusing the standing cursor.

<a id="f86b291951dec7bb"></a>
#### <kbd>ISSUE-4017</kbd> Idle timeout feature for XA transaction has been added.

<a id="73329c0baebbbb68"></a>
##### Description

XA_TRANSACTION_IDLE_TIMEOUT property has been added. It is the maximum idle time after the transaction is processed in XA, and the default value is 60 seconds.

<a id="c97f88943f4b4d48"></a>
##### Symptom

If the session is terminated when XA transaction has not been committed nor is rolled back, then it may infinitely waits because it is unable to return the resources in the transaction.

<a id="6433eda1994ac7d9"></a>
##### Workaround

The patch is required.

<a id="e9142f220eb56713"></a>
### 20c.1.17 Patch Notes

<a id="bff42a1abce77771"></a>
#### <kbd>ISSUE-3994</kbd> The options for sqlca.sqlerrd[2] value in an embedded SQL are added.

<a id="7e65657e04605c1f"></a>
##### Description

The number of rows which were executed just before are stored as sqlca.sqlerrd[2] value in the embedded SQL. However, the value can be selected between the accumulated total of rows or the number of fetched rows in FETCH CURSOR statement. For more information, refer to [--cumulative](../part-05-developer-manual/31-embedded-sql.md#274a5089d2d237b8) of the precompiler gpec option.

<a id="a92ccdfab02b4edd"></a>
##### Symptom

N/A

<a id="44188884396a4b18"></a>
##### Workaround

The patch is required.

<a id="823f618847343697"></a>
#### <kbd>ISSUE-3981</kbd> include_synonyms property has been added in ODBC and JDBC.

<a id="8eb0d859b8493e9c"></a>
##### Description

include_synonyms property has been added, and this property sets whether to include the synonym object in SQLColumns() of ODBC and DatabaseMetaData.getColumns() of JDBC.

<a id="c995cbb9a89f326a"></a>
##### Symptom

The synonym object information is not included in SQLColumns() of ODBC neither is included in DatabaseMetaData.getColumns() of JDBC.

<a id="d833a9a50ca3df34"></a>
##### Workaround

The patch is required.

<a id="cb130c50b4de6f7a"></a>
#### <kbd>ISSUE-3900</kbd> The uniqueness has been deleted from the cursor name in gpec.

<a id="6ab9895b7801ec50"></a>
##### Description

When using gpec, there is a constraint that the cursor name in a single gc file should be unique. gpec processes the gc file as an error with "The cursor name is already declared" message if the gc file declared multiple cursors with the same name. This creates useless codes and reduces the productivity, so the uniqueness has been deleted from the cursor name.

<a id="7e9fb42f08afd675"></a>
##### Symptom

When trying to declare a cursor selectively by using the conditional statement as follows, then gpec processes it as an error.

```
if( isTrue == 1 )
{
    EXEC SQL DECLARE CURSOR CUR1 FOR 
SELECT I1 FROM T1;
}
else
{
    EXEC SQL DECLARE CURSOR CUR1 FOR
SELECT C1 FROM T2;
}
```

When trying to select a cursor by using the conditional statement like as the example, then the cursor name should be declared different and the additional conditional statement should be added to the subordinate code.

```
if( isTrue == 1 )
{
    EXEC SQL DECLARE CURSOR CUR1 FOR 
SELECT I1 FROM T1;
}
else
{
    EXEC SQL DECLARE CURSOR CUR2 FOR
SELECT C1 FROM T2;
}

if( isTrue == 1 )
{
    EXEC SQL OPEN CUR1;
}
else
{
    EXEC SQL OPEN CUR2;
}
```

<a id="1263c3aa86cfc64e"></a>
##### Workaround

The patch is required.

<a id="a0837c825313627f"></a>
#### <kbd>ISSUE-3679</kbd> ODBC API trace feature has been added.

<a id="f13af0efcfde5972"></a>
##### Description

The feature to trace ODBC API has been added, so TRACE and TRACEFILE are also added to the connection property.

<a id="93d88c852bd2009c"></a>
##### Symptom

N/A

<a id="9e12876177611c54"></a>
##### Workaround

The patch is required.

<a id="58af5fa6cd6c2050"></a>
### 20c.1.16 Patch Notes

<a id="d0f2eb3b207886f3"></a>
#### <kbd>ISSUE-3958</kbd> SYNONYM information is not found in SQLTables() of ODBC nor in DatabaseMetaData.getTables() of JDBC.

<a id="a2800f02cee049e8"></a>
##### Description

The information about TABLE, VIEW and SYNONYM should be found in both SQLTables() of ODBC and in DatabaseMetaData.getTables() of JDBC, but currently the SYNONYM information is not found. The SYNONYM information can be found through each function.

<a id="3d7bc3f94df44df4"></a>
##### Symptom

When calling SQLTables() of ODBC or DatabaseMetaData.getTables() of JDBC, the information about TABLE and VIEW are found, but the SYNONYM information is not found.

<a id="db087f887877399d"></a>
##### Workaround

Use the following SQL statement to find the SYNONYM information.

```
gSQL> SELECT * FROM DICTIONARY_SCHEMA.ALL_SYNONYMS;
```

<a id="f04f769c050fc99c"></a>
#### <kbd>ISSUE-3954</kbd> When using SELECT INTO ARRAY clause in an embedded SQL, the result is wrong.

<a id="50e74f556b691da2"></a>
##### Description

The result value varies upon the number of FETCHED ROW when using SELECT INTO ARRAY clause.

<a id="080d443f7f5ffeff"></a>
##### Symptom

The following is a code which uses SELECT INTO ARRAY clause with the array size 3.

```
EXEC SQL BEGIN DECLARE SECTION;
int  sI1[3];
char sI2[3][10];
EXEC SQL END DECLARE SECTION;

SELECT I1, I2 INTO :sI1, :sI2 FROM TEST;
printf( "Fetched Count: %d\n", sqlca.sqlerrd[2] );
if( sqlca.sqlcode != 0 )
{
    printf( "SQLCODE: %d\n SQLSTATE: %s\n ERROR MSG: %s\n\n",
             sqlca.sqlcode, SQLSTATE, sqlca.sqlerrm.sqlerrmc );
}
```

If the total number of the entire ROW is one, then sqlca.sqlcode value should have been 0, but the actual sqlca.sqlcode value is -23034, and "SELECT INTO returns too many rows" error occurs.

<a id="0d0eb864cc112eb2"></a>
##### Workaround

The patch is required.

<a id="0a4243480249aa38"></a>
#### <kbd>ISSUE-3950</kbd> If performing an unsupported PSM query to the user by using JDBC/ ODBC, then the server is abnormally terminated.

<a id="341d39175d34334d"></a>
##### Description

If performing a PSM query which is registered in the plan cache though but is not supported through JDBC/ ODBC to the user, then an error occurs, and this error has been fixed so that those queries are not performed.

<a id="52243f47108a1d41"></a>
##### Symptom

If performing the query registered in the plan cache through ODBC as follows, then the server is abnormally terminated.

```
sRet = SQLExecDirect( sStmt,
                     (SQLCHAR*)"PROCEDURE \"PUBLIC\".\"PROC1\"  AS BEGIN NULL; END;",
                     SQL_NTS ) 
       == STL_SUCCESS );
```

If performing the query registered in the plan cache through JDBC as follows, then the server is abnormally terminated.

```
Statement sStmt = aCon.createStatement();
sStmt.execute("PROCEDURE \"PUBLIC\".\"PROC1\"  AS BEGIN NULL; END;);
```

<a id="aca081d71f3727b2"></a>
##### Workaround

Perform the correct query through ODBC as follows.

```
sRet = SQLExecDirect( sStmt,
                     (SQLCHAR*)"CALL PROC1;",
                     SQL_NTS ) 
       == STL_SUCCESS );
```

Perform the correct query through JDBC as follows.

```
Statement sStmt = aCon.createStatement();
sStmt.execute("CALL PROC1");
```

<a id="97be3ab7c4b846c2"></a>
#### <kbd>ISSUE-3959</kbd> An access to the deleted handle occurs while synchronizing the global sequence.

<a id="d1eb36e63917d24b"></a>
##### Description

An access to the deleted statement handle occurs while it waits for the response from the protocol of the previously used executors as a preliminary work before synchronizing the global sequence.

<a id="2fb18b9e2f198327"></a>
##### Symptom

The server is abnormally terminated while trying to access the deleted statement handle.

<a id="a693fde488108ad1"></a>
##### Workaround

The patch is required.

<a id="112c182dd475e7bc"></a>
### 20c.1.15 Patch Notes

<a id="8e3b85dc16cb46b7"></a>
#### <kbd>ISSUE-3923</kbd> The server is abnormally terminated when using the stored function in group by clause in SELECT statement.

<a id="13cdebdb1185c0a7"></a>
##### Description

An error occurs when using the stored function in *group by* clause in SELECT statement, and this error has been fixed.

<a id="0869dbf952d57edb"></a>
##### Symptom

The server is abnormally terminated when using the stored function in group by clause in SELECT statement as follows.

```
gSQL> 
SELECT func1( r_c1, r_c2 )
     , SUM( r_c1 )
  FROM r
 GROUP BY func1( r_c1, r_c2 );
```

<a id="0fa021d7c1ff1db7"></a>
##### Workaround

The patch is required.

<a id="01ee32a649f546f8"></a>
### 20c.1.14 Patch Notes

<a id="4413fc3eac2d9d60"></a>
#### <kbd>ISSUE-3909</kbd> Features which correspond to the national strategic item are not supported.

<a id="fcb3d963c2b0350f"></a>
##### Description

The following functions are not supported due to the restriction according to the policy for the national strategic item.

- ENCRYPT_STR() 
- DECRYPT_STR()

<a id="fdc077a154a86c39"></a>
##### Symptom

N/A

<a id="332ead34aa0287aa"></a>
##### Workaround

The patch is required.

<a id="99757455988ce0db"></a>
#### <kbd>ISSUE-3917</kbd> An error occurs when executing a procedure in XA environment.

<a id="17785204b01da4ec"></a>
##### Description

A procedure or an anonymous block is not executable in XA environment, and this error has been fixed.

<a id="a214c48434addc6f"></a>
##### Symptom

The following error occurs when executing a procedure in XA environment.

```
gSQL> CALL proc1();

ERR-42000(18009): The command cannot be executed when global transaction is in the ACTIVE state
```

<a id="884df4bee1a81641"></a>
##### Workaround

The patch is required.

<a id="2534c2a121c42695"></a>
#### <kbd>ISSUE-3913</kbd> An option which can specify the permission in DBMS_OUTPUT.SET_LOG() procedure has been added.

<a id="41673b02f0a81d7f"></a>
##### Description

It is enabled to specify the permission in DBMS_OUTPUT.SET_LOG() procedure.

```
gSQL> CALL DBMS_OUTPUT.SET_LOG('a.txt', 640);

Procedure Call complete.
```

<a id="af7147987e873e6e"></a>
##### Symptom

N/A

<a id="54519434952c486c"></a>
##### Workaround

The patch is required.

<a id="f3b576f31e5a1607"></a>
### 20c.1.13 Patch Notes

<a id="f24eb45688808f6c"></a>
#### <kbd>ISSUE-3884</kbd> When repeatedly executing connect in a process while using JDBC, then fd keeps increasing.

<a id="46cc33c1ba91c9ba"></a>
##### Description

When repeatedly executing connect in a process while using JDBC, then pipe and eventpoll fd keep increasing so "can not open files"  error occurs.

<a id="cb23fb7c3f9bc413"></a>
##### Symptom

fd is increased when repeatedly executing connect as follows, and it can be seen through lsof.

```
while (true)
{
    Connection con = DriverManager.getConnection("jdbc:goldilocks://127.0.0.1:11100/test", "TEST", "test");

    ...

    con.close();
    con = null;
}
```

```
% lsof -p 359414 | awk '{print $9}' | sort | uniq -c | sort -rn
    192 pipe
     96 [eventpoll]
     65 type=STREAM
     ...
```

```
% lsof -p 359414 | awk '{print $9}' | sort | uniq -c | sort -rn
    224 pipe
    112 [eventpoll]
     81 type=STREAM
     ...
```

<a id="0602b76831d54e67"></a>
##### Workaround

The patch is required.

<a id="da1f31e6677ccd1a"></a>
#### <kbd>ISSUE-3869</kbd> The result of row status is wrong when executing array fetch in ODBC.

<a id="c28764762ae3a22c"></a>
##### Description

When executing array fetch in ODBC, the status value of the row can be seen after calling SQLFetch function. If the returned value of SQLFetch is not SQL_SUCCESS, then it is required to check the row status or the diagnostic.   
However, even when the returned value of SQLFetch is SQL_SUCCESS_WITH_INFO, the diagnostic message is seen but all row statuses are SQL_ROW_SUCCESS, which are wrong.

<a id="5511e18aa58f3034"></a>
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

<a id="21c3a519ca647f01"></a>
##### Workaround

The patch is required.

<a id="dd699cd3b845cd68"></a>
### 20c.1.12 Patch Notes

<a id="2a012d567fde9c8e"></a>
#### <kbd>ISSUE-3859</kbd> If the size of an array is smaller than the number of records when using an array in an embedded SQL, SELECT INTO clause, then it should be processed as an error.

<a id="ae68acb49ee32226"></a>
##### Description

Currently, if the size of an array is smaller than the number of fetched records when using an array in SELECT INTO statement of an embedded SQL, no further action is taken. In this case, if the size of an array is smaller than the number of records, then the application can not recognize whether additional records exist. Therefore, if the size of an array is smaller than the number of fetched records, it should be processed as an error.

<a id="861be8105e26ed93"></a>
##### Symptom

```
gSQL> SELECT COUNT(*) FROM TEST;

COUNT(*)
--------
      20

1 row selected.
```

```
EXEC SQL BEGIN DECLARE SECTION;
int c1[10];
EXEC SQL END DECLARE SECTION;

EXEC SQL SELECT C1 INTO :c1 FROM TEST;
printf( "SQLCODE: %d\n", sqlca.sqlcode );
```

When the size of an array is smaller than the number of fetched records as above, then sqlca.sqlcode is normally processed, which is 0.

<a id="f5ad23d46b1cf8ce"></a>
##### Workaround

The patch is required.

<a id="e80783940883eae8"></a>
#### <kbd>ISSUE-3846</kbd> Core occurs if the property values between members are different in cluster environment when restarting.

<a id="52f536f16568ea40"></a>
##### Description

Some property values should be same between all members in the cluster environment. If those property values are different between members when restarting, then cserver dies.

<a id="b1831fb18b60e643"></a>
##### Symptom

It compares the property values which are supposed to be same between all members when restarting members in the cluster environment, and if there is a member with the different property value, then cserver dies.

The properties to have same values in the cluster environment are as follows.

```
gSQL> SELECT PROPERTY_NAME FROM X$PROPERTY@LOCAL WHERE CLUSTER_SCOPE = 'GLOBAL';

PROPERTY_NAME                          
---------------------------------------
TRANSACTION_TABLE_SIZE                 
NLS_DATE_FORMAT                        
NLS_TIME_FORMAT                        
NLS_TIME_WITH_TIME_ZONE_FORMAT         
NLS_TIMESTAMP_FORMAT                   
NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT    
DISABLE_DDL_CDC_GIVEUP                 
DISABLE_UPDATE_PK_CDC_GIVEUP           
DATABASE_ACCESS_MODE                   
IN_DOUBT_DECISION                      
DATABASE_TEST_OPTION                   
DDL_AUTOCOMMIT                         
SHARED_REQUEST_QUEUE_COUNT             
CLUSTER_CONNECTION                     
CDISPATCHER_THREADS                    
MAX_NODE_COUNT                         
MAX_GROUP_COUNT                        
CLUSTER_COMMIT_STREAM_ISOLATION        
DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION
TRACE_LOG_MSGBUF_SIZE                  

PROPERTY_NAME                           
----------------------------------------
DEFAULT_SHARDING                        
LOCATOR_QUERY_TIMEOUT                   
DISALLOWED_PROTOCOL_TARGETTYPE          
DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME
DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL 
FAILOVER_DRIVER_MEMBER                  
CDISPATCHER_SYNC_THREADS                
CLUSTER_SPLIT_BRAIN_RETRY_COUNT         
CLUSTER_TEST_SBR_POLICY                 
COORDINATOR_COMMIT_WRITE_MODE           
OFFLINE_MEMBER_AFTER_FAILOVER           
RECYCLEBIN                              
CDISPATCHER_LOCKLESS_THREADS            

33 rows selected.
```

<a id="d55f8c30620a9aae"></a>
##### Workaround

Modify property values of members to be same, then restart it.

<a id="6c5b5c9cd530037b"></a>
#### <kbd>ISSUE-3842</kbd> gpec omits EXEC SQL WHENEVER NOT FOUND statement in a specific DML statement.

<a id="c1fb1c942a1377cb"></a>
##### Description

Processing WHENEVER EXCEPTION should be applied to all DML statements when gpec converts the embedded SQL code to C code. However, actually it is applied only to SELECT INTO clause and FETCH clause.

<a id="05d917447b0c0f72"></a>
##### Symptom

gc file before transcoding

```
EXEC SQL WHENEVER SQLERROR DO callErrorLog( param->param, 0, sqlca.sqlcode, sqlca.sqlerrd[2] );

EXEC SQL WHENEVER NOT FOUND DO callLog( param->param, 0, sqlca.sqlcode, sqlca.sqlerrd[2] );

EXEC SQL DELETE FROM TEST
    WHERE ENUMBER = :in.enumber
        AND ENAME = :in.ename;
```

c file after transcoding

```
DBESQL_Execute(NULL, &sqlargs);

if(sqlca.sqlcode < 0) callErrorLog(param->param, 0, sqlca.sqlcode, sqlca.sqlerrd[2]);
```

The code is created without an action code for NOT FOUND.

<a id="2f6a12d47ff453f3"></a>
##### Workaround

Directly write NOT FOUND processing in gc file as follows.

```
EXEC SQL DELETE FROM TEST
    WHERE ENUMBER = :in.enumber
        AND ENAME = :in.ename;
if(sqlca.sqlcode == 0) callLog( ... );
```

<a id="9e6d54d4d6764f2c"></a>
#### <kbd>ISSUE-3830</kbd> XA connection is not available as a default context in embedded SQL.

<a id="067369eb83fc9d4a"></a>
##### Description

Use the default context or create the named context to use XA in the embedded SQL.

If executing xa open without the connection name while any connection is not created in the default context when using XA with the default context, then XA connection is supposed to be connected to the default context. However, in practice, it is not connected to the default context.

<a id="d2804045c53e5599"></a>
##### Symptom

If creating xa connection without the connection name while any connection does not exist in the default context as follows, then XA connection is supposed to be connected to the default context. Also, it should be able to execute SQL statement with the default context.

```
int main( int argc, char** argv)
{
	xa_switch_t * sXaSwitch;

    sXaSwitch = SQLGetXaSwitch();

    if( (sXaSwitch->xa_open_entry)( "DSN=GOLDILOCKS;UID=test;PWD=test", 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    EXEC SQL DROP TABLE IF EXISTS DEPOSIT;

    ... /* Ellipsis */

}
```

When executing the program created with the code above, then invalid handle error occurs.

```
[ERROR] SQL ERROR -
SQLCODE : -2
SQLSTATE : HY000
ERROR MSG : Invalid handle
```

<a id="84329058bba1e7e0"></a>
##### Workaround

Create the named context, and use it.

<a id="190aa4a37f9e08b1"></a>
### 20c.1.11 Patch Notes

<a id="544279557052312d"></a>
#### <kbd>ISSUE-3371</kbd> Xa transaction is supported in cluster environment.

<a id="477bee8212a18b94"></a>
##### Description

It supports Xa transaction in cluster environment.

<a id="346ccb66ba8c1313"></a>
##### Symptom

N/A

<a id="dee5899ac499a233"></a>
##### Workaround

The patch is required.

<a id="55ed0ac00d2bc671"></a>
#### <kbd>ISSUE-3821</kbd> If it fails to use the large page when allocating the shared segment, then the feature to use the normal page is required.

<a id="eff136c36e69595c"></a>
##### Description

USE_LARGE_PAGES property supports 0 and 1. When it is set to 0, it does not use the large page, and when it is set to 1, then it uses the large page. If it fails to allocate the shared memory when it is set to 1, then an error occurs.

Therefore, the feature to use the normal page when it fails to allocate the shared memory in the large page has been added.

<a id="7910043b50655434"></a>
##### Symptom

When USE_LARGE_PAGE is set to 2, then it tries to allocate the shared memory in the large page first, and if it fails, then it allocates the shared memory in the normal page.

```
gSQL> alter tablespace mem_data_tbs add datafile 'test1.dbf' size 5G;

ERR-HY000(11042): Not enough memory : sthCreate() returned errno(12)

gSQL> alter system set use_large_pages = 2;

System altered.

gSQL> alter tablespace mem_data_tbs add datafile 'test1.dbf' size 5G;

Tablespace altered.
```

<a id="067ea7ccbfee0a1c"></a>
##### Workaround

The patch is required.

<a id="084a5050e076ed3c"></a>
#### <kbd>ISSUE-3798</kbd> When performing DML with protocol method by using synonym in cluster, the system is abnormally terminated or the query processing is infinitely repeated.

<a id="1d1bf9cf4b27ba4f"></a>
##### Description

If processing DML by a using synonym when the synonym is defined in a schema which is different from the target object in cluster, then the system is abnormally terminated or the query processing is infinitely repeated.

<a id="68a7b1f65b698464"></a>
##### Symptom

When performing *insert* through a synonym after defining the table and the synonym as follows, then the query processing is infinitely repeated.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1;

User created.

gSQL> GRANT ALL PRIVILEGES TO u1;

Grant succeeded.

gSQL> CREATE USER u2 IDENTIFIED BY u2;

User created.

gSQL> GRANT ALL PRIVILEGES TO u2;

Grant succeeded.

gSQL> \CONNECT u2 u2
gSQL> CREATE TABLE u1.t_cloned ( c1 NUMBER ) CLONED;

Table created.

gSQL> CREATE SYNONYM u2.syn FOR u1.t_cloned;

Synonym created.


--# hang
gSQL> INSERT INTO u2.syn VALUES( 1 );
```

<a id="93926de63c224d96"></a>
##### Workaround

Do not use a synonym when performing DML.

```
INSERT INTO u1.t_cloned VALUES( 2 );
```

Or, execute DML based on a query complying with the following constraints in case for *delete*, *update* and *select for update* except for insert.

- Do not include a subquery expression nor a non-deterministic expression.
- Do not use OFFSET/ LIMIT statement.
- Do not use ROWNUM.
- Limit UPDATE for a sharding key.

<a id="9e2547f808381041"></a>
### 20c.1.10 Patch Notes

<a id="9fa6ec280f4772d6"></a>
#### <kbd>ISSUE-3768</kbd> Executing IN function during prepare/ execution, then the system is intermittently and abnormally terminated.

<a id="cc2f0a3330f27e9d"></a>
##### Description

When executing the query two or more times after preparing during preparing/ executing the query whose number of the value part of IN function is 10 or more, then the system is intermittently and abnormally terminated.

<a id="e7094fc8c11ae63f"></a>
##### Symptom

When executing the query two or more times after preparing it when the table was created as follows, then the system is intermittently and abnormally terminated.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER, c2 VARCHAR(1) );

Table created.

gSQL> INSERT INTO t1 VALUES ( 1, 'A' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 2, 'B' );

1 row created.

gSQL> CREATE INDEX idx_t1 ON t1 ( c1 );

Index created.

gSQL> \var v1 INTEGER
gSQL> \prepare sql
SELECT *
  FROM t1
 WHERE c1 = :v1
   AND c2 IN ( 'P','T','X','C','W','B','L','M','H','J','Z','G','D' );
    2     3     4     5 
SQL prepared.

gSQL> \exec

no rows selected.

gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       2

1 row selected.

gSQL> \exec

no rows selected.

gSQL> \exec :v1 := 2
gSQL> \exec

C1 C2
-- --
 2 B 

1 row selected.

gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       2

1 row selected.
```

- When repeatedly executing exec, then the system is abnormally terminated.  
  The location of exec error is not fixed.

```
gSQL> \exec

C1 C2
-- --
 2 B 

1 row selected.
```

<a id="7e7f6d5778e67893"></a>
##### Workaround

Configure the number of values in value part of IN function less than 10 to prevent IN_HASH from applying.

```
\prepare sql
SELECT *
  FROM t1
 WHERE c1 = :v1
   AND c2 IN ( 'P','T','X','C','W','B','L','M','H','J','Z','G','D' );
```

When number of values in value part of IN function is more than 10 as above, then divide IN functions and bind it with OR.

```
\prepare sql
SELECT *
  FROM t1
 WHERE c1 = :v1
   AND ( 
         c2 IN ( 'P','T','X','C','W','B' ) 
         OR
         c2 IN ( 'L','M','H','J','Z','G','D' ) 
       );
```

<a id="30e71a420e69fcb6"></a>
#### <kbd>ISSUE-3766</kbd> When checking the availability of the remote method of ROWNUM, then checking for the subquery filter is omitted.

<a id="19fd53b3627a7352"></a>
##### Description

The query result may have an error because the subquery filter is dropped in the following query.

```
SELECT r_sk
     , r_nk
  FROM r
 WHERE r_sk = 202
   AND r_nk = ( SELECT r_nk + 999 FROM dual )
   AND ROWNUM < 5
```

When all of the following conditions exist as in the query above, then the subquery filter disappears.

- r_sk = 202 
    - The sharding key condition which determines a single remote server 
- r_nk = ( SELECT r_nk + 999 FROM dual )
    - The subquery condition which can not be unnested
- ROWNUM < 5
    - The ROWNUM condition which limits the number

<a id="bf374e86c0885eaa"></a>
##### Symptom

The query result is supposed not to exist after building the table as follows, but actually the query result is created because the subquery filter was dropped.

```
CREATE TABLE r
(
    r_sk INTEGER,
    r_nk INTEGER
) SHARDING BY RANGE(r_sk)
  SHARD s1 VALUES LESS THAN ( 200      ) AT CLUSTER GROUP g1,
  SHARD s2 VALUES LESS THAN ( 300      ) AT CLUSTER GROUP g2,
  SHARD s3 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g3
;

INSERT INTO r VALUES ( 101, 101 );
INSERT INTO r VALUES ( 202, 202 );
INSERT INTO r VALUES ( 303, 303 );
COMMIT;
```

- The query result should not exist.

```
\explain plan
SELECT r_sk
     , r_nk
  FROM r
 WHERE r_sk = 202
   AND r_nk = ( SELECT r_nk + 999 FROM dual )
   AND ROWNUM < 5
;   

R_SK R_NK
---- ----
 202  202

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      PLAN BASED CLUSTER                                      | REMOTE ONLY           1 |
|    3  |        COUNT                                                 |                       0 |
|    4  |          TABLE ACCESS ("R")                                  |                       0 |
==================================================================================================

     1  -  TARGET : R.R_SK, R.R_NK
     2  -  SQL : SELECT /*+ FULL( _A1 ) */ "_A1"."R_SK", "_A1"."R_NK" FROM "PUBLIC"."R"@LOCAL AS "_A1" WHERE "_A1"."R_SK" = :_V0 AND ROWNUM < :_V1
           TARGET DOMAIN : G2(G2N1,G2N2) 1 rows
     3  -  STOP KEY FILTER : ROWNUM < 5
     4  -  RANGE SHARD ( # 3 ) 
           READ COLUMN : R.R_SK, R.R_NK
             PHYSICAL FILTER : R.R_SK = 202

<<<  end print plan
```

<a id="4b29bb50f5c952d4"></a>
##### Workaround

Change ROWNUM condition to LIMIT condition as follows.

```
\explain plan
SELECT r_sk
     , r_nk
  FROM r
 WHERE r_sk = 202
   AND r_nk = ( SELECT r_nk + 999 FROM dual )
 LIMIT 4
;   

no rows selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       0 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       0 |
|    2  |      PLAN BASED CLUSTER                                      | REMOTE ONLY           0 |
|    3  |        TABLE ACCESS ("R")                                    |                       0 |
|    4  |      SUB QUERY LIST                                          |                         |
|    5  |        INLINE_VIEW ("$V5")                                   |                       1 |
|    6  |          QUERY BLOCK ("$QB_IDX_6")                           |                       1 |
|    7  |            FAST DUAL ACCESS ("DUAL")                         |                       1 |
==================================================================================================

     1  -  TARGET : R.R_SK, R.R_NK
     2  -  SQL : SELECT /*+ FULL( _A1 ) */ "_A1"."R_SK", "_A1"."R_NK" FROM "PUBLIC"."R"@LOCAL AS "_A1" WHERE "_A1"."R_SK" = :_V0
           TARGET DOMAIN : G2(G2N1,G2N2) 1 rows
             POST FILTER : R.R_NK = $V5.$C0
     3  -  RANGE SHARD ( # 3 ) 
           READ COLUMN : R.R_SK, R.R_NK
             PHYSICAL FILTER : R.R_SK = 202
     5  -  COLUMN : {R.R_NK} + 999 AS $C0
     6  -  TARGET : {R.R_NK} + 999
     7  -  READ COLUMN : NOTHING

<<<  end print plan
```

<a id="6306286369455d97"></a>
#### <kbd>ISSUE-3751</kbd> When prepare/ execution, the accumulated information about rows of plans under the cluster puller is output.

<a id="b678eef3a4138454"></a>
##### Description

When prepare/ execute the query including the cluster puller plan, then the number of result rows for the cluster puller and its subordinate nodes are accumulated whenever it is executed, and output.

It is the matter related to counting result rows, and it does not affect the query execution.

<a id="9d10d44d28f0c6ea"></a>
##### Symptom

When executing the query two times or more after creating the following table and preparing the query, then the wrong result is output.

```
gSQL> CREATE TABLE T1 ( SK INT, C1 INT ) SHARDING BY HASH ( SK );

Table created.

gSQL> INSERT INTO T1 VALUES ( 1, 10 );

1 row created.

gSQL> \SET AUTOTRACE ON
gSQL> \PREPARE SQL SELECT SUM( SK ) FROM T1 GROUP BY C1;

SQL prepared.

gSQL> \EXEC

SUM( SK )
---------
        1

1 row selected.

>>>  start print plan

< Execution Plan >
=========================================================================
|  IDX  |  NODE DESCRIPTION                          |             ROWS |
-------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                          |                1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")               |                1 |
|    2  |      SINGLE CLUSTER                        | LOCAL/REMOTE   1 |
|    3  |        SELECT STATEMENT                    |                1 |
|    4  |          QUERY BLOCK ("$QB_IDX_2")         |                1 |
|    5  |            GROUP HASH INSTANT              |                1 |
|    6  |              TABLE ACCESS ("T1" AS _A1)    |                1 |
=========================================================================

     1  -  TARGET : SUM( T1.SK )
     2  -  SQL : SELECT /*+ USE_GROUP_HASH(10) FULL( _A1 ) */ "_A1"."C1", SUM( "_A1"."SK" ) FROM "PUBLIC"."T1"@LOCAL AS "_A1" GROUP BY "_A1"."C1"
           TARGET DOMAIN : G1(G1N1) 1 rows, G2(G2N1) 0 rows, G3(G3N1) 0 rows
           RE-GROUPING
             GROUP KEY : T1.C1
             AGGREGATION : SUM( SUM( T1.SK ) )
     4  -  TARGET : _A1.C1, SUM( _A1.SK )
     5  -  GROUP KEY : _A1.C1
           RECORD COLUMN : SUM( _A1.SK )
           READ KEY COLUMN : _A1.C1
           READ RECORD COLUMN : SUM( _A1.SK )
     6  -  HASH SHARD ( # 3 ) 
           READ COLUMN : _A1.SK, _A1.C1

<<<  end print plan


gSQL> \EXEC

SUM( SK )
---------
        1

1 row selected.

>>>  start print plan

< Execution Plan >
=========================================================================
|  IDX  |  NODE DESCRIPTION                          |             ROWS |
-------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                          |                1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")               |                1 |
|    2  |      SINGLE CLUSTER                        | LOCAL/REMOTE   1 |
|    3  |        SELECT STATEMENT                    |                2 |
|    4  |          QUERY BLOCK ("$QB_IDX_2")         |                2 |
|    5  |            GROUP HASH INSTANT              |                2 |
|    6  |              TABLE ACCESS ("T1" AS _A1)    |                2 |
=========================================================================

     1  -  TARGET : SUM( T1.SK )
     2  -  SQL : SELECT /*+ USE_GROUP_HASH(10) FULL( _A1 ) */ "_A1"."C1", SUM( "_A1"."SK" ) FROM "PUBLIC"."T1"@LOCAL AS "_A1" GROUP BY "_A1"."C1"
           TARGET DOMAIN : G1(G1N1) 1 rows, G2(G2N1) 0 rows, G3(G3N1) 0 rows
           RE-GROUPING
             GROUP KEY : T1.C1
             AGGREGATION : SUM( SUM( T1.SK ) )
     4  -  TARGET : _A1.C1, SUM( _A1.SK )
     5  -  GROUP KEY : _A1.C1
           RECORD COLUMN : SUM( _A1.SK )
           READ KEY COLUMN : _A1.C1
           READ RECORD COLUMN : SUM( _A1.SK )
     6  -  HASH SHARD ( # 3 ) 
           READ COLUMN : _A1.SK, _A1.C1

<<<  end print plan
```

<a id="984e190fce6a2f6e"></a>
##### Workaround

The patch is required.

<a id="c9194df62b8ce84a"></a>
### 20c.1.9 Patch Notes

<a id="925cb518f0eb690a"></a>
#### <kbd>ISSUE-3752</kbd> If the targets of the query are not all groups but are some groups when using the global connection, then the client may be abnormally terminated.

<a id="61ec47c11e0252a7"></a>
##### Description

When using the global connection, the shard information only about groups used in the query are transferred but not about all groups. Therefore, it may refer to the wrong memory when only part of information about the group is transferred. In this case, the client may be abnormally terminated.

> When this patch is applied, then the client should be rebuilt.

<a id="28b52e1cf8c4cfa1"></a>
##### Symptom

When performing the query in the global connection environment after creating the following table, then the client is abnormally terminated.

```
gSQL> create table t1 ( i1 integer ) sharding by (i1);

Table created.

gSQL> insert into t1 values (1),(2),(3),(4),(5),(6),(7),(8),(9),(10),(11),(12),(13),(14),(15),(16),(17),(18),(19),(20),(21),(22),(23),(24);

24 rows created.

gSQL> commit;

Commit complete.

gSQL> select * from t1@g2;

I1
--
12
13
14
15
16
17
18
19

8 rows selected.

gSQL> select * from t1@g3;

I1
--
 8
 9
10
11
20
21
22
23

8 rows selected.
```

```
gSQL> \var v1 integer;
gSQL> \exec :v1 := 8
gSQL> \prepare sql select * from t1 where i1 = :v1 and i1 in (8,12);

SQL prepared.
```

- Client is abnormally terminated.

```
gSQL> \exec
```

<a id="3728c31b56b8a2e7"></a>
##### Workaround

Do not use the global connection.

<a id="a4be349f5c16adb2"></a>
### 20c.1.8 Patch Notes

<a id="5b6ce45fbf7eb09b"></a>
#### <kbd>ISSUE-3726</kbd> When repeatedly calling Statement.getUpdateCount() in JDBC, the update count should be initialized.

<a id="20df01af632652c9"></a>
##### Description

Statement.getUpdateCount() in JDBC can be called only once per a result as quoted below.


> 
> 1. Retrieves the current result as an update count; if the result is a ResultSet object or there are no more results, -1 is returned. This method should be called only once per result.
> 

When repeatedly calling Statement.getUpdateCount(), then it returns -1.

<a id="14ac8207b912de5b"></a>
##### Symptom

When repeatedly calling Statement.getUpdateCount(), then it keeps returning the same values.

<a id="ca38d809fef994ab"></a>
##### Workaround

The patch is required.

<a id="bc5c58095668db09"></a>
### 20c.1.7 Patch Notes

<a id="4afe94777f37d847"></a>
#### <kbd>ISSUE-3716</kbd> Performing view merging when a sequence exists in the superordinate query and order by exists within a view leads to the wrong result.

<a id="ed73b8111f5f2628"></a>
##### Description

view merging should not be performed when a sequence exists in the superordinate query, but view merging is performed in reality, and it leads to the wrong result.

<a id="27beb43212a4ecdc"></a>
##### Symptom

Performing the following query leads to the wrong result.

```
CREATE SEQUENCE seq1;
CREATE TABLE t1 ( col1 INTEGER, col2 INTEGER );
INSERT INTO t1 VALUES(1,1);
INSERT INTO t1 VALUES(2,2);
INSERT INTO t1 VALUES(3,3);


\EXPLAIN PLAN
SELECT seq1.nextval
  FROM ( SELECT * 
           FROM t1 
         ORDER BY col1 )v1;

NEXTVAL
-------
   NULL
   NULL
   NULL

3 rows selected.
```

<a id="9bf692e1ebf442e1"></a>
##### Workaround

Add NO_MERGE( view_name) hint.

```
\EXPLAIN PLAN
SELECT /*+ NO_MERGE(v1) */
       seq1.nextval
  FROM ( SELECT * 
           FROM t1 )v1;

NEXTVAL
-------
      1
      2
      3

3 rows selected.

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      INLINE_VIEW ("V1")                                      |
|    3  |        QUERY BLOCK ("$QB_IDX_5")                             |
|    4  |          SORT INSTANT                                        |
|    5  |            TABLE ACCESS ("T1")                               |
========================================================================

     1  -  TARGET : NEXTVAL(SEQ1)
     2  -  COLUMN : V1.DUMMY_COL AS DUMMY_COL
     3  -  TARGET : NOTHING
     4  -  SORT KEY : "T1.COL1 ASC NULLS LAST"
     5  -  READ COLUMN : T1.COL1

<<<  end print plan
```

<a id="8b43df89e0c79b91"></a>
#### <kbd>ISSUE-3707</kbd> The process is abnormally terminated when a target view of the simple view merging is on the right side of the left outer join, and only one constant exists in the select list of that view.

<a id="e164e0ffaa40b833"></a>
##### Description

The process is abnormally terminated when the following conditions are satisfied.

- A left outer join exists within a view.
- The right side of the left outer join is a view again, and only one constant exists in the select list of that view.

<a id="fec85d33feb57903"></a>
##### Symptom

The process is abnormally terminated when processing the following query.

```
\EXPLAIN PLAN 
SELECT COUNT(*)
  FROM ( SELECT t1.col1
           FROM t1 LEFT OUTER JOIN ( SELECT 1 as col1 FROM dual ) v1
                ON v1.col1 = t1.col1
      ) AAA;
```

<a id="3644548a71843f43"></a>
##### Workaround

Add NO_MERGE( view_name) hint.

```
\EXPLAIN PLAN 
SELECT COUNT(*)
  FROM ( SELECT /*+ NO_MERGE(v1) */ t1.col1
           FROM t1 LEFT OUTER JOIN ( SELECT 1 as col1 FROM dual ) v1
                ON v1.col1 = t1.col1
      ) AAA;
```

<a id="7cfb61c235056b3a"></a>
#### <kbd>ISSUE-3699</kbd> Recovery fails due to the lack of the space when restarting the database.

<a id="c13913dc8c8c37a7"></a>
##### Description

The information about transactions of the record and the key is stored in RTS space in table data pages and the index leaf pages. If multiple transactions simultaneously update a single page, then RTS can be expanded. The page compaction is performed to reuse the space of dropped records, and RTS is reduced at this moment when it is possible.

The error occurs when the space is not expanded because it does not satisfy the condition to reduce RTS at the recovery though the space was made by reducing RTS when compacting pages during the service.

<a id="9cc03483758711c1"></a>
##### Symptom

The recovery fails due to the lack of the page space when restarting the database.

<a id="914237eaf5265961"></a>
##### Workaround

The patch is required.

<a id="5d65f87d0d7dd127"></a>
#### <kbd>ISSUE-3705</kbd> Wrong transitive predicate is created.

<a id="e82c5da6fd0db7f2"></a>
##### Description

When LIKE, NOT LIKE predicate appears after the transitive predicate was created, then the wrong transitive predicate is created.

<a id="9aaab7dae74529cc"></a>
##### Symptom

The following is an example of SQL which causes an error.

```
\EXPLAIN PLAN
SELECT r_c1, s_c1
  FROM r, s
 WHERE r_c1 = 'A'     ❶ The filter creating the transitive predicate is                     
                          described beforehand. 
   AND s_c2 LIKE '99%'  ❷ LIKE or NOT LIKE function exists
   AND r_c1 = s_c1      ❸ A equi join condition exists. 
;

no rows selected.

>>>  start print plan

< Execution Plan >
========================================================================
|  IDX  |  NODE DESCRIPTION                                            |
------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |
|    2  |      NESTED JOIN (INNER JOIN)                                |
|    3  |        INDEX ACCESS ("S", "S_PRIMARY_KEY_INDEX")             |
|    4  |        INDEX ACCESS ("R", "IDX_R_C1")                        |
========================================================================

     1  -  TARGET : R.R_C1, S.S_C1
     2  -  JOINED COLUMN : R.R_C1, S.S_C1
     3  -  READ INDEX COLUMN : S.S_C1
           READ TABLE COLUMN : S.S_C2
             MIN RANGE : S.S_C1 = 'A' AND S.S_C1 LIKE '99%'
             MAX RANGE : S.S_C1 = 'A' AND S.S_C1 LIKE '99%'
             LOGICAL KEY FILTER : S.S_C1 LIKE '99%'
             LOGICAL TABLE FILTER : S.S_C2 LIKE '99%'
           FETCH ONE ROW
     4  -  READ INDEX COLUMN : R.R_C1
             MIN RANGE : R.R_C1 = {S.S_C1} AND R.R_C1 = 'A'
             MAX RANGE : R.R_C1 = {S.S_C1} AND R.R_C1 = 'A'

<<<  end print plan
```

<a id="0ef844586cb662ba"></a>
##### Workaround

Describe the predicate which includes LIKE, NOT LIKE functions beforehand as follows.

```
\EXPLAIN PLAN
SELECT r_c1, s_c1
  FROM r, s
 WHERE s_c2 LIKE '99%' 
   AND r_c1 = 'A'    
   AND r_c1 = s_c1    
;


R_C1 S_C1
---- ----
A    A

1 row selected.
```

<a id="d89654ae5f64271a"></a>
#### <kbd>ISSUE-3697</kbd> Type qualifier is not output in gpec.

<a id="e07da514003386b4"></a>
##### Description

When gpec converts gc file which uses the storage class or the type qualifier in front of the embedded SQL pseudo type into c file, then the storage class and the type qualifier are omitted.

<a id="76bd936aa3487f01"></a>
##### Symptom

The following is a part of gc file.

```
EXEC SQL BEGIN DECLARE SECTION;
static VARCHAR gUid[10];
static char    gPwd[10];
EXEC SQL END DECLARE SECTION;
```

The following is a part of c file which was converted by gpec from gc file created above.

```
/* EXEC SQL BEGIN DECLARE SECTION; */
#line 16 "test.gc"

/* static VARCHAR gUid[10]; */
struct { int len; char arr[10]; } gUid;
#line 17 "test.gc"

static char    gPwd[10];
/* EXEC SQL END DECLARE SECTION; */
#line 19 "test.gc"
```

The static operator is dropped because *static Varchar gUid[10*] code is converted into C code.

<a id="0076be3d52bf15ca"></a>
##### Workaround

The patch is required.

<a id="c30c15a0aa2e7b33"></a>
#### <kbd>ISSUE-3698</kbd> getUpdateCount of JDBC statement class returns an abnormal value.

<a id="9521bcb61941398e"></a>
##### Description

When executing INSERT INTO statement which used QUERY, then it returns 0 as the result value of getUpdateCount().

<a id="b6e79dbd034b0e6d"></a>
##### Symptom

```
Statement stmt = conn.createStatement();
stmt.executeUpdate( "CREATE TABLE TEST ( I1 INTEGER )" );
stmt.executeUpdate( "INSERT INTO TEST VALUES ( 1 ) );
stmt.executeUpdate( "INSERT INTO TEST SELECT I1 FROM TEST" );

int count = stmt.getUpdateCount();
```

It returns 0 as getUpdateCount() value.

<a id="e5d6dded23d4fb00"></a>
##### Workaround

The patch is required.

<a id="0f76a6b33281f824"></a>
### 20c.1.6 Patch Notes

<a id="fc4067ca7cdd9465"></a>
#### <kbd>ISSUE-3690</kbd> When the file path is entered in JDBC URL in Windows, the file is unreadable.

<a id="5584ba540d898450"></a>
##### Description

Even when the correct file path is entered in URL by using / delimiter in Windows, but the file is unreadable in JDBC.

<a id="a021c605b2adc778"></a>
##### Symptom

Unreadable File error occurs.

<a id="9597d25dce04acac"></a>
##### Workaround

The patch is required.

<a id="95414886a0e4d47a"></a>
#### <kbd>ISSUE-3687</kbd> When executing transaction retransmission, it stores the transaction whose size exceeds the sorting block size in a block.

<a id="498f1fee76ce74eb"></a>
##### Description

While configuring a sorting block for the transaction retransmission when the coordinator failover occurred, it stores the transaction whose size exceeds the block size, then sorts it, so it invades the unallocated memory area.

<a id="7acc16a5a570e860"></a>
##### Symptom

It is abnormally terminated as SEGV while the coordinator server executes the coordinator failover.

<a id="ba428761467e1097"></a>
##### Workaround

The patch is required.

<a id="6bba5d587bb746a5"></a>
### 20c.1.5 Patch Notes

<a id="98ff2a85bc3c630b"></a>
#### <kbd>ISSUE-3678</kbd> JDBC connection property login_timeout is added.

<a id="63d9cbdce391fa0b"></a>
##### Description

Previously, login timeout can be set by setLoginTimeout method of DriverManager/DataSource class. However, setLoginTimeout method may not be called in a certain situation such as WAS. Therefore, the connection property login_timeout has been added.

<a id="600a5a4ae3f3545b"></a>
##### Symptom

When connecting to the server in JDBC with the wrong IP or the wrong PORT, it indefinitely waits instead of causing an error.

<a id="d5375883d9902041"></a>
##### Workaround

The patch is required.

<a id="639cc6bc81016dad"></a>
### 20c.1.4 Patch Notes

<a id="ad4c8c2b38cbc215"></a>
#### <kbd>ISSUE-3669</kbd> When failover occurs by the heartbeat, the aging information is not reset.

<a id="3ee8e951fc5fbb18"></a>
##### Description

While processing the failover, the aging information of dead nodes managed by active nodes are supposed to be reset, but it is not reset in fact.

<a id="36b1a4895cd002e3"></a>
##### Symptom

If active nodes do not reset the aging information of dead nodes, UNDO tablespace may be insufficient.

<a id="649148c03b4decf5"></a>
##### Workaround

The patch is required.

<a id="5d92f72039358100"></a>
### 20c.1.3 Patch Notes

<a id="77d1565e971dde51"></a>
#### <kbd>ISSUE-3655</kbd> Rebalance protocols are simultaneously performed on multiple members.

<a id="83ca4a0f8ca0f499"></a>
##### Description

When performing table rebalancing, if sequentially transferring protocols to remote members and receiving responses, then the delay occurs. Therefore, BROADCAST_REBALANCE_PROTOCOL property which broadcasts protocols to remote members and simultaneously processes them is added when the protocols can be processes at the same time, so the delay is reduced.

<a id="08983291ff9d9b62"></a>
##### Symptom

When performing table rebalancing, the processing time is delayed as much as the number of target members while locking, or sequentially transferring rebalancing starting protocols to remote members, and receiving responses.

<a id="eb86c61eb8d3173c"></a>
##### Workaround

The patch is required.

<a id="31e0c69b8eefc7ec"></a>
#### <kbd>ISSUE-3649</kbd> Cluster server which is exclusive for lockless protocols is required

<a id="be6a90181eaa30b7"></a>
##### Description

A query which does not need a lock such as SELECT waits because it can not reserve the cluster server.

<a id="941663308c4f0a2c"></a>
##### Symptom

The cluster server using shared connection method may wait in the lock status while the server is reserved when lock wait frequently occurs. Even a query which does not need a lock such as SELECT waits because it can not reserve the cluster server.

<a id="04604b5233e21e1f"></a>
##### Workaround

The patch is required.

<a id="7314029e50e5a745"></a>
#### <kbd>ISSUE-3663</kbd> If cluster deadlock timeout occurs when performing DML, then the query is performed again.

<a id="a51c57336d270882"></a>
##### Description

The cluster deadlock timeout which occurred when performing DML is not a deadlock due to the competition between transactions. so it does not need to be terminated as a query failure. Therefore, it performs the query again after rollback.

<a id="7a6a7d9f4b00126b"></a>
##### Symptom

The cluster deadlock may occur due to the lack of lockable cluster servers. The deadlock is not resolved even after the waiting for the time set in [CLUSTER_DEADLOCK_TIMEOUT](../part-02-administration-manual/10-server-property.md#bcc389ceff77f7bf), then CLUSTER_DEADLOCK_TIMEOUT error occurs.

However, if is DML query, then the query is performed again after the rollback when CLUSTER DEADLOCK TIMEOUT occurs.

<a id="6ece8bfe90b74e2e"></a>
##### Workaround

The patch is required.

<a id="f4c0d1cb243016ed"></a>
### 20c.1.2 Patch Notes

<a id="7694fce8514f9b57"></a>
#### <kbd>ISSUE-3648</kbd> Incorrect result packet of transaction retransmission when failover

<a id="d0024092210671d7"></a>
##### Description

It is supposed to ignore the committed transactions when performing the transaction retransmission during the failover, but it actually configures incorrect response packet and transfers it to the client.

<a id="f7881e72abe8118a"></a>
##### Symptom

The server is abnormally terminated when it accesses to the result packet, and it occurs for the case of triplication or over.

<a id="873a703c7a691b95"></a>
##### Workaround

The patch is required.

<a id="f2e1f8ec6d203cd6"></a>
### 20c.1.1 Patch Notes

<a id="5c84afca47932394"></a>
#### <kbd>ISSUE-3621</kbd> MERGE_DISTINCT hint is added.

<a id="2209ee8e2cb4a451"></a>
##### Description

MERGE_DISTINCT hint has been added.

This hint is available when performing distinct clause in the cluster environment, and it is available when it satisfies the following conditions.

- A distinct clause exists.
- It can be performed with remote distinct.
- The intermediate result ascends from the subordinate node of the distinct node in a state that the order for the distinct key column is guaranteed.

<a id="92deec578e69f146"></a>
##### Symptom

The following is an example of using MERGE_DISTINCT hint.

```
\EXPLAIN PLAN
SELECT /*+ MERGE_DISTINCT */
       DISTINCT o_custkey
  FROM orders
 WHERE o_custkey > 0
ORDER BY o_custkey;

O_CUSTKEY
---------
        1
        2
        4
      ...

99996 rows selected.

>>>  start print plan

< Execution Plan >
==========================================================================
|IDX|  NODE DESCRIPTION                                                  |
--------------------------------------------------------------------------
| 0 |  SELECT STATEMENT                                                  |
| 1 |    QUERY BLOCK ("$QB_IDX_2")                                       |
| 2 |      MULTIPLE CLUSTER                                              |
| 3 |        SELECT STATEMENT                                            |
| 4 |          QUERY BLOCK ("$QB_IDX_2")                                 |
| 5 |            GROUP                                                   |
| 6 |              INDEX ACCESS ("ORDERS" AS _A1, "ORDERS_CUSTKEY_FK")   |
==========================================================================

     1  -  TARGET : ORDERS.O_CUSTKEY
     2  -  SQL : SELECT /*+ INDEX( _A1, "PUBLIC"."ORDERS_CUSTKEY_FK" ) */
                        DISTINCT "_A1"."O_CUSTKEY" 
                   FROM "PUBLIC"."ORDERS"@LOCAL AS "_A1" 
                  WHERE "_A1"."O_CUSTKEY" > :_V0 
               ORDER BY "_A1"."O_CUSTKEY" ASC NULLS LAST
           TARGET DOMAIN : G1(G1N1,G1N2) 98218 rows, 
                           G2(G2N1,G2N2) 98174 rows,
                           G3(G3N1,G3N2) 98138 rows
           MERGE GROUPING
             SORT KEY : ORDERS.O_CUSTKEY
             GROUP KEY : ORDERS.O_CUSTKEY
     4  -  TARGET : _A1.O_CUSTKEY
     5  -  GROUP KEY : _A1.O_CUSTKEY
     6  -  HASH SHARD ( # 3 ) 
           READ INDEX COLUMN : _A1.O_CUSTKEY
             MIN RANGE : _A1.O_CUSTKEY > :_V0
             MAX RANGE : _A1.O_CUSTKEY IS NOT NULL

<<<  end print plan
```

In the execution plan above, *MULTIPLE CLUSTER(IDX:2)* keeps the order for o_custkey. Therefore, SORT node for ORDER BY is useless, so it is dropped.

<a id="73a74a70127e582b"></a>
##### Workaround

The patch is required.

<a id="265647414b281aa6"></a>
#### <kbd>ISSUE-3619</kbd> Performance of Sampling ANALYZE is improved.

<a id="890162fe09dd5d1e"></a>
##### Description

Performance of Sampling ANALYZE for an indexed column in the cluster environment is improved.

<a id="830208d888243de8"></a>
##### Symptom

Sampling ANALYZE for an indexed column is processed in proportion to the entire number of row as follows.

```
ANALYZE TABLE large_shard_table ESTIMATE STATISTICS 
        SAMPLE 1000000 ROWS FOR COLUMNS indexed_column;
```

It is modified to process the query above to be processes in proportion to the user-defined SAMPLE n ROWS so that the performance is improved.

<a id="3f719f450f66742f"></a>
##### Workaround

The patch is required.

---

[← 3. Cluster Tutorial](3-cluster-tutorial.md) · [Table of contents](../README.md) · [5. Basic Management of GOLDILOCKS Database →](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
