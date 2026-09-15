<a id="cde56a0de7f1ec68"></a>

# 9. Database Information

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/cde56a0de7f1ec68)  
> Tag: `22c.1_10_tag`

[← 8. GOLDILOCKS Database Replication](8-goldilocks-database-replication.md) · [Table of contents](../README.md) · [10. Server Property →](10-server-property.md)

<a id="fd116a7f066a7767"></a>
## DICTIONARY_SCHEMA

DICTIONARY_SCHEMA contains views or tables to get SQL objects and their information in the system.

> The views and tables in DICTIONARY_SCHEMA can be retrieved from the open phase.

Execute *DictionarySchema.sql* as follows to use the views.

- For standalone

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
```

- For cluster

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
```

Information is retrieved as follows according to the names of views or tables.

- ALL-family view
    - The view name begins with ALL_ 
    - Information about accessible objects by a current user
- DBA-family view
    - The view name begins with DBA_ 
    - Information about all objects whose current user has DBA privileges (ACCESS CONTROL ON DATABASE).
- USER-family view
    - The view name begins with USER_ 
    - Information about objects which are owned by the current user

<a id="f4aeb4ed5c4771df"></a>
### Views of ALL_family

It retrieves information about objects accessible by a current user.

<a id="fa172bfe0b739f0a"></a>
#### ALL_ALL_TABLES

ALL_ALL_TABLES describes the object tables and relational tables accessible to the current user.

**Column information**

<a id="27a8c4eed9f629a1"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="d2c6ff7f27bd6f9a"></a>
#### ALL_ARGUMENTS

ALL_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="88a592b6c662fc15"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of function, procedures or package |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures |
| PACKAGE_NAME | VARCHAR(128) | Package Name of function, procedures |
| OBJECT_ID | NUMBER | ID of a function, procedures |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| ARGUMENT_NAME | VARCHAR(128) | Name of argument or attribute name of record type argument |
| POSITION | NUMBER | Position of argument or position of attribute in record type |
| SEQUENCE | NUMBER | Sequential order of argument and its attributes |
| DATA_LEVEL | NUMBER | Nesting depth of the argument for composite types |
| DATA_TYPE | VARCHAR(128) | Data type of the argument |
| DEFAULTED | VARCHAR(1) | Whether or not the argument is defaulted |
| DEFAULT_VALUE | VARCHAR(1) | Reserved for future use |
| DEFAULT_LENGTH | VARCHAR(1) | Reserved for future use |
| IN_OUT | VARCHAR(32) | Direction of the argument (IN, OUT, IN/OUT) |
| DATA_LENGTH | NUMBER | Length of the column(in bytes) |
| DATA_PRECISION | NUMBER | Length in decimal digits(NUMBER) or binary digits(FLOAT) |
| DATA_SCALE | NUMBER | Digits to the right of the decimal point in a number |
| RADIX | NUMBER | Argument radix for a number |
| CHARACTER_SET_NAME | VARCHAR(128) | Character set name for the argument |
| TYPE_OWNER | VARCHAR(128) | Owner of the type of the argument |
| TYPE_NAME | VARCHAR(128) | Name of the type of the argument |
| TYPE_SUBNAME | VARCHAR(128) | Name of the type of the argument declared in package |
| TYPE_LINK | VARCHAR(128) | Name of the type of the argument declared in a remote package |
| PLS_TYPE | VARCHAR(128) | Name of the type of the argument at PSM |
| CHAR_LENGTH | NUMBER | Character limit for string datatypes |
| CHAR_USED | VARCHAR(1) | Whether the byte limit(B) or char limit(C) is official for the string |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="eabb6b65d6c6ffcf"></a>
#### ALL_CATALOG

ALL_CATALOG displays the tables, views, synonyms, and sequences accessible to the current user.

**Column information**

<a id="350d874ba9f4c1b5"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_NAME | VARCHAR(128) | Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_TYPE | VARCHAR(32) | Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |

<a id="91c7d8e7b165cd13"></a>
#### ALL_CLUSTER_TABLES

ALL_CLUSTER_TABLES describes all cluster tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="34c67dbbc7f90103"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| SHARD_STRATEGY | VARCHAR(32) | Sharding strategy of the table:  the value in (CLONED, HASH SHARDING, RANGE SHARDING, LIST SHARDING) |
| SHARD_PLACEMENT | VARCHAR(32) | Shard placement of the table:  the value in (AT CLUSTER WIDE or AT CLUSTER GROUP) |
| SHARD_COUNT | NUMBER | Shard count of the table (if cloned table, the value is null) |
| SHARD_KEY_COUNT | NUMBER | Shard key column count of the table (if cloned table, the value is null) |
| HAS_GSI | VARCHAR(3) | Indicate whether the table has global secondary index: (YES) or (NO) |
| DROPPED | VARCHAR(3) | Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="ec9d741ede48fc12"></a>
#### ALL_COL_COMMENTS

ALL_COL_COMMENTS displays comments on the columns of the tables and views accessible to the current user.

**Column information**

<a id="eac96cfe4a1919d7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| COMMENTS | VARCHAR(1024) | Comment on the column |

<a id="3d4d5b9e5d68536b"></a>
#### ALL_COL_PRIVS

ALL_COL_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="d8d74432d9704929"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| PRIVILEGE | VARCHAR(32) | Privilege on the column |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="b38e234cfbee6a80"></a>
#### ALL_COL_PRIVS_MADE

ALL_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner or grantor.

**Column information**

<a id="b348caf4b5dd9ee4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the column |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9e1b606cfc119b2a"></a>
#### ALL_COL_PRIVS_RECD

ALL_COL_PRIVS_RECD describes the column object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="5032d423f62e9f08"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the column |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="2826ab105a4aeabd"></a>
#### ALL_CONSTRAINTS

ALL_CONSTRAINTS describes constraint definitions on tables accessible to the current user.

**Column information**

<a id="a34fea4600cbcad1"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="e222eb63c18b72be"></a>
#### ALL_CONS_COLUMNS

ALL_CONS_COLUMNS describes columns that are accessible to the current user and that are specified in constraints.

**Column information**

<a id="51c7404ccc26c73d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the constraint definition |
| CONSTRAINT_SCHEMA | VARCHAR(128) | Schema of the constraint definition |
| CONSTRAINT_NAME | VARCHAR(128) | Name of the constraint definition |
| TABLE_OWNER | VARCHAR(128) | Owner of the table with the constraint definition |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table with the constraint definition |
| TABLE_NAME | VARCHAR(128) | Name of the table with the constraint definition |
| COLUMN_NAME | VARCHAR(128) | Name of the column or attribute of the object type column specified in the constraint definition |
| POSITION | NUMBER | Original position of the column or attribute in the definition of the object |

<a id="4f4545437d435e5d"></a>
#### ALL_DB_PRIVS

ALL_DB_PRIVS describes the database grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="134e43aa86b7ac27"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="88aeba0642cc2e2f"></a>
#### ALL_DB_PRIVS_MADE

ALL_DB_PRIVS_MADE describes the database grants for which the current user is the grantor.

**Column information**

<a id="5811c390ddb8f675"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9dbe5936c19b66ac"></a>
#### ALL_DB_PRIVS_RECD

ALL_DB_PRIVS_RECD describes the database grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="03a1f1d91c002b6a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="4756b7463d7564a8"></a>
#### ALL_DEPENDENCIES

ALL_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column information**

<a id="df848716ad2bc1f9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, VIEW, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_OWNER | VARCHAR(128) | Owner of the referenced object |
| REFERENCED_SCHEMA_NAME | VARCHAR(128) | Schema Name of the referenced object |
| REFERENCED_TYPE | VARCHAR(32) | Type of the referenced object: FUNCTION, PROCEDURE, TABLE, VIEW, SEQUENCE, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_LINK_NAME | VARCHAR(128) | Name of the link to the parent object |
| REFERENCED_NAME | VARCHAR(128) | Name of the referenced object |
| DEPENDENCY_TYPE | VARCHAR(32) | Indicates whether the dependency is a REF dependency (REF) or not (HARD) |

<a id="3c405f9eb4878efd"></a>
#### ALL_GLOBAL_SECONDARY_INDEXES

ALL_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables accessible to the current user.

> It is available only on a cluster.

**Column information**

<a id="bae71efbc607590a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_OWNER | VARCHAR(128) | Owner of the global secondary indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| TABLESPACE_NAME | VARCHAR(128) | Name of the tablespace containing the global secondary index |
| INI_TRANS | NUMBER | Initial number of transactions |
| MAX_TRANS | NUMBER | Maximum number of transactions |
| INITIAL_EXTENT | NUMBER | Size of the initial extent |
| NEXT_EXTENT | NUMBER | Size of secondary extents |
| MIN_EXTENTS | NUMBER | Minimum number of extents allowed in the segment |
| MAX_EXTENTS | NUMBER | Maximum number of extents allowed in the segment |
| PCT_FREE | NUMBER | Minimum percentage of free space in a block |
| LOGGING | VARCHAR(3) | Indicates whether or not changes to the global secondary index are logged: (YES) or (NO) |
| BLOCKS | NUMBER | Number of used blocks in the global secondary index |
| EMPTY_BLOCKS | NUMBER | Number of empty blocks in the global secondary index |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="1136123bdbe5d9eb"></a>
#### ALL_GSI_PLACE

ALL_GSI_PLACE describes node placement of all global secondary indexes on the tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="0610b2d5a503ba17"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_OWNER | VARCHAR(128) | Owner of the global secondary indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the global secondary index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the global secondary index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the global secondary index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the global secondary index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="fc7a4d13da011291"></a>
#### ALL_INDEXES

ALL_INDEXES describes the indexes on the tables accessible to the current user.

**Column information**

<a id="58bcf936a3140708"></a>
<table><thead><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="204902c3172a050b"></a>
#### ALL_IND_COLUMNS

ALL_IND_COLUMNS describes the columns of indexes on all tables accessible to the current user.

**Column information**

<a id="c840778694470251"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| INDEX_OWNER | VARCHAR(128) | Owner of the index |
| INDEX_SCHEMA | VARCHAR(128) | Schema of the index |
| INDEX_NAME | VARCHAR(128) | Name of the index |
| TABLE_OWNER | VARCHAR(128) | Owner of the table or cluster |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table or cluster |
| TABLE_NAME | VARCHAR(128) | Name of the table or cluster |
| COLUMN_NAME | VARCHAR(128) | Column name or attribute of the object type column |
| COLUMN_POSITION | NUMBER | Position of the column or attribute within the index |
| COLUMN_LENGTH | NUMBER | Indexed length of the column |
| CHAR_LENGTH | NUMBER | Maximum codepoint length of the column |
| DESCEND | VARCHAR(32) | Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC) |
| NULL_ORDER | VARCHAR(32) | Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST) |

<a id="a4ed6f28d1311e00"></a>
#### ALL_IND_PLACE

ALL_IND_PLACE describes node placement of the indexes on the tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="dd887bd8617bd0e7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the index |
| INDEX_SCHEMA | VARCHAR(128) | Schema of the index |
| INDEX_NAME | VARCHAR(128) | Name of the index |
| TABLE_OWNER | VARCHAR(128) | Owner of the indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO) |
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | (deprecated) |

<a id="2ef7214dc7ea7a48"></a>
#### ALL_NONSCHEMA_COMMENTS

ALL_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces) accessible to the current user.

**Column information**

<a id="5db4765770eebe57"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OBJECT_NAME | VARCHAR(128) | Name of the non-schema object |
| OBJECT_TYPE | VARCHAR(32) | Type of the non-schema object: DATABASE, AUTHORIZATION, SCHEMA, TABLESPACE |
| COMMENTS | VARCHAR(1024) | Comments of the non-schema object |

<a id="47e9b779d037b2d0"></a>
#### ALL_OBJECTS

ALL_OBJECTS describes all objects accessible to the current user.

**Column information**

<a id="19d07147267c2ae6"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="74280e86e4d2c586"></a>
#### ALL_PACKAGE_PRIVS

ALL_PACKAGE_PRIVS describes the package grants, for which the current user is the package owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="617b7f94ddaa1d16"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="626365fb987d0080"></a>
#### ALL_PACKAGE_PRIVS_MADE

ALL_PACKAGE_PRIVS_MADE describes the package grants for which the current user is the package owner or grantor.

**Column information**

<a id="7a7b82d80d2044cb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="3fc3b35dc9c968c6"></a>
#### ALL_PACKAGE_PRIVS_RECD

ALL_PACKAGE_PRIVS_RECD describes the package grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="dda148f6b9075bc0"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9414a849ae5452f3"></a>
#### ALL_PROCEDURES

ALL_PROCEDURES lists all function, procedures or package

**Column information**

<a id="20d2d5962c0e9260"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of function, procedures or package |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures or package |
| PROCEDURE_NAME | VARCHAR(128) | Name when a procedures in package |
| OBJECT_ID | NUMBER | ID of a function, procedures or package |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| OVERLOAD | VARCHAR(32) | ID of overloading procedure in package |
| OBJECT_TYPE | VARCHAR(32) | Type of function, procedures or package |
| AGGREGATE | VARCHAR(3) | Indicate whether the procedure is an aggreage function(YES) or not(NO) |
| PIPELINED | VARCHAR(3) | Indicate whether the procedure is a pipelined table function(YES) or not(NO) |
| IMPLTYPEOWNER | VARCHAR(128) | Name of the owner of the implementation type, if any |
| IMPLTYPENAME | VARCHAR(128) | Name of the implementation type, if any |
| PARALLEL | VARCHAR(3) | Indicates whether the procedure or function is parallel-enabled (YES) or not (NO) |
| INTERFACE | VARCHAR(3) | YES, if the procedure/function is a table function implemented using the SQLCLI interface; otherwise NO |
| DETERMINISTIC | VARCHAR(3) | YES, if the procedure/function is declared to be deterministic; otherwise NO |
| AUTHID | VARCHAR(32) | Indicates whether the procedure/function is declared to execute as DEFINER or CURRENT_USER (invoker) |

<a id="f305b17a9da6244e"></a>
#### ALL_PROC_PRIVS

ALL_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="ac5938fd0c8d1239"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="a88c39e3f8e9b202"></a>
#### ALL_PROC_PRIVS_MADE

ALL_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column information**

<a id="967aa652d1450baf"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="777e35e9585ca6c0"></a>
#### ALL_PROC_PRIVS_RECD

ALL_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="c4b3bd1133b62852"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="92e220a4701e88da"></a>
#### ALL_SCHEMAS

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column information**

<a id="02b795daac37e00d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| CREATED_TIME | TIMESTAMP(6) WITHOUT TIME ZONE | Created time of the schema |
| MODIFIED_TIME | TIMESTAMP(6) WITHOUT TIME ZONE | Last modified time of the schema |
| COMMENTS | VARCHAR(1024) | Comments of the schema |

<a id="4a54a4178690af49"></a>
#### ALL_SCHEMA_PATH

ALL_SCHEMA_PATH describes the schema search order of the current user and PUBLIC, for naming resolution of unqualified SQL schema objects.

**Column information**

<a id="b411b4ad6b0f4403"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| AUTH_NAME | VARCHAR(128) | Name of the authorization |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| SEARCH_ORDER | NUMBER | Schema search order of the authorization |

<a id="7dfdc31ad16631a2"></a>
#### ALL_SCHEMA_PRIVS

ALL_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="48eabf12341ec61e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| PRIVILEGE | VARCHAR(32) | Privilege on the schema |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="3c0433340596d70e"></a>
#### ALL_SCHEMA_PRIVS_MADE

ALL_SCHEMA_PRIVS_MADE describes the schema grants, for which the current user is the grantor.

**Column information**

<a id="524b1336766c1327"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f79b97044adb6e22"></a>
#### ALL_SCHEMA_PRIVS_RECD

ALL_SCHEMA_PRIVS_RECD describes the schema grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="7d20c8255cd321b4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="1e065ebb0e38aa3c"></a>
#### ALL_SEQUENCES

ALL_SEQUENCES describes all sequences accessible to the current user.

**Column information**

<a id="11e15908d08b8cb4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Sequence name</td></tr><tr><td align="left" valign="middle">&nbsp;MIN_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;MAX_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;INCREMENT_BY</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">&nbsp;CYCLE_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;ORDER_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;CACHE_SIZE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_NUMBER</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="a14a1174bda7889c"></a>
#### ALL_SEQ_PRIVS

ALL_SEQ_PRIVS describes the sequence grants, for which the current user is the sequence owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="270f20de13ce5c0e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b93fb3203c15effd"></a>
#### ALL_SEQ_PRIVS_MADE

ALL_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner or grantor.

**Column information**

<a id="7c43b41325d22088"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="755f0e6b68fa220f"></a>
#### ALL_SEQ_PRIVS_RECD

ALL_SEQ_PRIVS_RECD describes the sequence grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="ce4313c86345395d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="15f521dccf394061"></a>
#### ALL_SHARD_KEY_COLUMNS

ALL_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="83dbaac9fa147cfc"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="c13aeb08c66010e6"></a>
#### ALL_SOURCE

ALL_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="2cf79ba77012e9ce"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="a3cb5f1dc2555b23"></a>
#### ALL_SYNONYMS

ALL_SYNONYMS describes all synonyms.

**Column information**

<a id="be892127ad9f6430"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="bedf19a877d482bb"></a>
#### ALL_TABLES

ALL_TABLES describes the relational tables accessible to the current user.

**Column information**

<a id="712ceef50f60d45e"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="d96c8e722e9c5b55"></a>
#### ALL_TAB_COLS

ALL_TAB_COLS describes the columns(including hidden columns) of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="4d42c8baec2a9def"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="eeae0a821d5eb30b"></a>
#### ALL_TAB_COLUMNS

ALL_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="55e65d0321fc3f9d"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="675a2ce61b15ba74"></a>
#### ALL_TAB_COMMENTS

ALL_TAB_COMMENTS displays comments on the tables and views accessible to the current user.

**Column information**

<a id="4732eed923a76fc1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="6ab51f64b75e0761"></a>
#### ALL_TAB_IDENTITY_COLS

ALL_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="8c7262ad39e55f1e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="50045795e344458c"></a>
#### ALL_TAB_PLACE

ALL_TAB_PLACE describes node placement of all cluster tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="e540cecce1dded4c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td valign="middle">MEMBER_POSITION</td><td valign="middle">NUMBER</td><td valign="middle">Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td valign="middle">IS_UPDATE_MASTER</td><td valign="middle">BOOLEAN</td><td valign="middle">whether the cluster member is update master or not</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="74b66d63ac0ae641"></a>
#### ALL_TAB_SHARDS

ALL_TAB_SHARDS describes shard information of sharded tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="b596bbb94beb0770"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="5cd44bf55a14cfa7"></a>
#### ALL_TAB_PRIVS

ALL_TAB_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="6dfbd891e15db296"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="d0730513885b7f3b"></a>
#### ALL_TAB_PRIVS_MADE

ALL_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner or grantor.

**Column information**

<a id="5d16e36db4c9bb55"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="502da6a35b708977"></a>
#### ALL_TAB_PRIVS_RECD

ALL_TAB_PRIVS_RECD describes object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="2f8cdce5775f53f0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2051a6aead24a2d3"></a>
#### ALL_TBS_PRIVS

ALL_TBS_PRIVS describes the tablespace grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="6555795eef07b5c5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="66d4dd67696c866a"></a>
#### ALL_TBS_PRIVS_MADE

ALL_TBS_PRIVS_MADE describes the tablespace grants for which the current user is the grantor.

**Column information**

<a id="bff2fabb1c300411"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="848956e01273912c"></a>
#### ALL_TBS_PRIVS_RECD

ALL_TBS_PRIVS_RECD describes the tablespace grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="8e7f8b211b740f4c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b77a1d1382eaaca1"></a>
#### ALL_USERS

ALL_USERS lists all users of the database visible to the current user.

**Column information**

<a id="dd646e176a6367e0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">USERNAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">USER_ID</td><td align="left">NUMBER</td><td align="left">ID number of the user</td></tr><tr><td align="left">CREATED</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">User creation timestamp</td></tr></tbody></table>

<a id="cbf6ac6de8a5a898"></a>
#### ALL_VIEWS

ALL_VIEWS describes the views accessible to the current user.

**Column information**

<a id="23485b64ef064513"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="0814c9e3a93706b8"></a>
### Views of DBA_family

The current user has DBA privileges (ACCESS CONTROL ON DATABASE), and the user can retrieve information about all objects.

<a id="59ae6b75e0189060"></a>
#### DBA_ALL_TABLES

DBA_ALL_TABLES describes all object tables and relational tables in the database.

**Column information**

<a id="9341bac67680102c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="822bb96b4b02c94c"></a>
#### DBA_ARGUMENTS

DBA_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="86a2ec3a3bdc15a9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of function, procedures or package |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures |
| PACKAGE_NAME | VARCHAR(128) | Package Name of function, procedures |
| OBJECT_ID | NUMBER | ID of a function, procedures |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| ARGUMENT_NAME | VARCHAR(128) | Name of argument or attribute name of record type argument |
| POSITION | NUMBER | Position of argument or position of attribute in record type |
| SEQUENCE | NUMBER | Sequential order of argument and its attributes |
| DATA_LEVEL | NUMBER | Nesting depth of the argument for composite types |
| DATA_TYPE | VARCHAR(128) | Data type of the argument |
| DEFAULTED | VARCHAR(1) | Whether or not the argument is defaulted |
| DEFAULT_VALUE | VARCHAR(1) | Reserved for future use |
| DEFAULT_LENGTH | VARCHAR(1) | Reserved for future use |
| IN_OUT | VARCHAR(32) | Direction of the argument (IN, OUT, IN/OUT) |
| DATA_LENGTH | NUMBER | Length of the column(in bytes) |
| DATA_PRECISION | NUMBER | Length in decimal digits(NUMBER) or binary digits(FLOAT) |
| DATA_SCALE | NUMBER | Digits to the right of the decimal point in a number |
| RADIX | NUMBER | Argument radix for a number |
| CHARACTER_SET_NAME | VARCHAR(128) | Character set name for the argument |
| TYPE_OWNER | VARCHAR(128) | Owner of the type of the argument |
| TYPE_NAME | VARCHAR(128) | Name of the type of the argument |
| TYPE_SUBNAME | VARCHAR(128) | Name of the type of the argument declared in package |
| TYPE_LINK | VARCHAR(128) | Name of the type of the argument declared in a remote package |
| PLS_TYPE | VARCHAR(128) | Name of the type of the argument at PSM |
| CHAR_LENGTH | NUMBER | Character limit for string datatypes |
| CHAR_USED | VARCHAR(1) | Whether the byte limit(B) or char limit(C) is official for the string |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="bcb788acbd820cfd"></a>
#### DBA_CATALOG

DBA_CATALOG lists all tables, views, synonyms, and sequences in the database.

**Column information**

<a id="820a6db76d23cdc2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="c944365990fbf691"></a>
#### DBA_CLUSTER

DBA_CLUSTER describes all cluster members in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="94b6d3927e5a8222"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GROUP_ID</td><td align="left">NUMBER</td><td align="left">Group identifier of the cluster member</td></tr><tr><td align="left">GROUP_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Group name of the cluster member</td></tr><tr><td align="left">MEMBER_ID</td><td align="left">NUMBER</td><td align="left">Member identifier of the cluster member</td></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Member name of the cluster member</td></tr><tr><td align="left">MEMBER_HOST</td><td align="left">VARCHAR(256)</td><td align="left">Host name or IP address of the cluster member</td></tr><tr><td align="left">MEMBER_PORT</td><td align="left">NUMBER</td><td align="left">Port number of the cluster member</td></tr><tr><td>MEMBER_POSITION</td><td>NUMBER</td><td>Member position number of the cluster member</td></tr></tbody></table>

<a id="7ec8d9a1539c5557"></a>
#### DBA_CLUSTER_COMMENTS

DBA_CLUSTER_COMMENTS displays comments on the cluster objects in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="575394df7d3bc4e4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the cluster object</td></tr><tr><td align="left">OBJECT_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the cluster object: CLUSTER GROUP, CLUSTER MEMBER</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the cluster object</td></tr></tbody></table>

<a id="146c6e783cb4e3f8"></a>
#### DBA_CLUSTER_TABLES

DBA_CLUSTER_TABLES describes all cluster tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="2a7c3b04caa0c64d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| SHARD_STRATEGY | VARCHAR(32) | Sharding strategy of the table:  the value in (CLONED, HASH SHARDING, RANGE SHARDING, LIST SHARDING) |
| SHARD_PLACEMENT | VARCHAR(32) | Shard placement of the table:  the value in (AT CLUSTER WIDE or AT CLUSTER GROUP) |
| SHARD_COUNT | NUMBER | Shard count of the table (if cloned table, the value is null) |
| SHARD_KEY_COUNT | NUMBER | Shard key column count of the table (if cloned table, the value is null) |
| HAS_GSI | VARCHAR(3) | Indicate whether the table has global secondary index: (YES) or (NO) |
| DROPPED | VARCHAR(3) | Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="1308091fb27cdf4e"></a>
#### DBA_COL_COMMENTS

DBA_COL_COMMENTS displays comments on the columns of all tables and views in the database.

**Column information**

<a id="fb505402f42acd9f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="54387031724a6b81"></a>
#### DBA_COL_PRIVS

DBA_COL_PRIVS describes all column object grants in the database.

**Column information**

<a id="56b31ef9f7297b44"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">CHARACTER VARYING(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">CHARACTER VARYING(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="dd5b53e3bd4356e7"></a>
#### DBA_CONSTRAINTS

DBA_CONSTRAINTS describes all constraint definitions on all tables in the database.

**Column information**

<a id="cfff09303243d1c4"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="941762fe0c8defb2"></a>
#### DBA_CONS_COLUMNS

DBA_CONS_COLUMNS describes all columns in the database that are specified in constraints.

**Column information**

<a id="b93b995e7faca5ac"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="52f051b46464387d"></a>
#### DBA_DB_PRIVS

DBA_DB_PRIVS describes all database grants in the database.

**Column information**

<a id="0426cf6ac0ead5d2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the database</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f8f5ee5b7f0e8d82"></a>
#### DBA_DEPENDENCIES

DBA_DEPENDENCIES describes all dependencies between objects in the database

**Column information**

<a id="89143d447fd0d330"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, VIEW, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_OWNER | VARCHAR(128) | Owner of the referenced object |
| REFERENCED_SCHEMA_NAME | VARCHAR(128) | Schema Name of the referenced object |
| REFERENCED_TYPE | VARCHAR(32) | Type of the referenced object: FUNCTION, PROCEDURE, TABLE, VIEW, SEQUENCE, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_LINK_NAME | VARCHAR(128) | Name of the link to the parent object |
| REFERENCED_NAME | VARCHAR(128) | Name of the referenced object |
| DEPENDENCY_TYPE | VARCHAR(32) | Indicates whether the dependency is a REF dependency (REF) or not (HARD) |

<a id="65e92f312ce99153"></a>
#### DBA_EXTENTS

DBA_EXTENTS describes the extents comprising the segments in all tablespaces in the database.

**Column information**

<a id="da85244b36e76d5b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Extent number in the segment</td></tr><tr><td align="left" valign="middle">FILE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;File identifier number of the file containing the extent</td></tr><tr><td align="left" valign="middle">BLOCK_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Starting block number of the extent</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr><tr><td align="left" valign="middle">RELATIVE_FNO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Relative file number of the first extent block</td></tr></tbody></table>

<a id="507a8568ab2c63ae"></a>
#### DBA_GLOBAL_SECONDARY_INDEXES

DBA_GLOBAL_SECONDARY_INDEXES describes all global secondary indexes in the database.

> It is available only on a cluster.

**Column information**

<a id="a68a1141897782f4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_OWNER | VARCHAR(128) | Owner of the global secondary indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| TABLESPACE_NAME | VARCHAR(128) | Name of the tablespace containing the global secondary index |
| INI_TRANS | NUMBER | Initial number of transactions |
| MAX_TRANS | NUMBER | Maximum number of transactions |
| INITIAL_EXTENT | NUMBER | Size of the initial extent |
| NEXT_EXTENT | NUMBER | Size of secondary extents |
| MIN_EXTENTS | NUMBER | Minimum number of extents allowed in the segment |
| MAX_EXTENTS | NUMBER | Maximum number of extents allowed in the segment |
| PCT_FREE | NUMBER | Minimum percentage of free space in a block |
| LOGGING | VARCHAR(3) | Indicates whether or not changes to the global secondary index are logged: (YES) or (NO) |
| BLOCKS | NUMBER | Number of used blocks in the global secondary index |
| EMPTY_BLOCKS | NUMBER | Number of empty blocks in the global secondary index |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="9391a0a0a516e215"></a>
#### DBA_GSI_PLACE

DBA_GSI_PLACE describes node placement of all global secondary indexes in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="3a2513da46fac3bf"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_OWNER | VARCHAR(128) | Owner of the global secondary indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the global secondary index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the global secondary index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the global secondary index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the global secondary index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="f9793dea5365c94a"></a>
#### DBA_INDEXES

DBA_INDEXES describes all indexes in the database.

**Column information**

<a id="e8085a4f8ab63b33"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="e3306f4a319c8f75"></a>
#### DBA_IND_COLUMNS

DBA_IND_COLUMNS describes the columns of all the indexes on all tables and clusters in the database.

**Column information**

<a id="33e3573d3a8f1996"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="80d7eda6ef4fd0f5"></a>
#### DBA_IND_PLACE

DBA_IND_PLACE describes node placement of all indexes in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="b111c87719113b9e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the index |
| INDEX_SCHEMA | VARCHAR(128) | Schema of the index |
| INDEX_NAME | VARCHAR(128) | Name of the index |
| TABLE_OWNER | VARCHAR(128) | Owner of the indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO) |
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | (deprecated) |

<a id="f1de8287fd06f6bc"></a>
#### DBA_NONSCHEMA_COMMENTS

DBA_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces).

**Column information**

<a id="8fe02a0b170c0ed3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the non-schema object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the non-schema object: DATABASE, PROFILE, AUTHORIZATION, SCHEMA, TABLESPACE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the non-schema object</td></tr></tbody></table>

<a id="497024429c1c9b59"></a>
#### DBA_OBJECTS

DBA_OBJECTS describes all objects in the database.

**Column information**

<a id="05dba3e79a56e9d0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the edition in which the object is actual</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="f5984257e01dee9f"></a>
#### DBA_PACKAGE_PRIVS

DBA_PACKAGE_PRIVS describes all packages grants in the database.

**Column information**

<a id="ead0e8b1e21bab6a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="ed33a7c96223df35"></a>
#### DBA_PROCEDURES

DBA_PROCEDURES lists all function, procedures or package

**Column information**

<a id="abbfe262037f7f97"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of function, procedures or package |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures or package |
| PROCEDURE_NAME | VARCHAR(128) | Name when a procedures in package |
| OBJECT_ID | NUMBER | ID of a function, procedures or package |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| OVERLOAD | VARCHAR(32) | ID of overloading procedure in package |
| OBJECT_TYPE | VARCHAR(32) | Type of function, procedures or package |
| AGGREGATE | VARCHAR(3) | Indicate whether the procedure is an aggreage function(YES) or not(NO) |
| PIPELINED | VARCHAR(3) | Indicate whether the procedure is a pipelined table function(YES) or not(NO) |
| IMPLTYPEOWNER | VARCHAR(128) | Name of the owner of the implementation type, if any |
| IMPLTYPENAME | VARCHAR(128) | Name of the implementation type, if any |
| PARALLEL | VARCHAR(3) | Indicates whether the procedure or function is parallel-enabled (YES) or not (NO) |
| INTERFACE | VARCHAR(3) | YES, if the procedure/function is a table function implemented using the SQLCLI interface; otherwise NO |
| DETERMINISTIC | VARCHAR(3) | YES, if the procedure/function is declared to be deterministic; otherwise NO |
| AUTHID | VARCHAR(32) | Indicates whether the procedure/function is declared to execute as DEFINER or CURRENT_USER (invoker) |

<a id="96af0ed84c1ac294"></a>
#### DBA_PROC_PRIVS

DBA_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="649f4425eb172781"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="acacc03940f1aec3"></a>
#### DBA_PROFILES

DBA_PROFILES displays all profiles and their limits.

**Column information**

<a id="6c5ec0c3d3203bab"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROFILE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Profile name</td></tr><tr><td align="left" valign="middle">RESOURCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Resource name</td></tr><tr><td align="left" valign="middle">RESOURCE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the resource profile is a KERNEL or a PASSWORD parameter</td></tr><tr><td align="left" valign="middle">LIMIT_VALUE</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Limit placed on this resource for this profile</td></tr><tr><td align="left" valign="middle">COMMON</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether a given profile is common. (YES or NO)</td></tr></tbody></table>

<a id="a9df4ab7d086ae40"></a>
#### DBA_RECYCLEBIN

DBA_RECYCLEBIN describes all recycle bins in the database.

**Column information**

<a id="8a5affb58ebc4fbc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema name of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">ORIGINAL_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Original name of the object</td></tr><tr><td align="left" valign="middle">OPERATION</td><td valign="middle">VARCHAR(4)</td><td valign="middle">Operation carried out on the object</td></tr><tr><td valign="middle">OBJECT_TYPE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Type of the object</td></tr><tr><td valign="middle">TABLESPACE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the tablespace containing the object</td></tr><tr><td valign="middle">CREATED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Created time of the object</td></tr><tr><td valign="middle">DROPPED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Dropped time of the object</td></tr><tr><td valign="middle">DROP_SCN</td><td valign="middle">VARCHAR(128)</td><td valign="middle">System change number (SCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_GCN</td><td valign="middle">NUMBER</td><td valign="middle">Global change number (GCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_DCN</td><td valign="middle">NUMBER</td><td valign="middle">Domain change number (DCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_LCN</td><td valign="middle">NUMBER</td><td valign="middle">Local change number (LCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">CAN_UNDROP</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be undropped (YES) or not (NO)</td></tr><tr><td valign="middle">CAN_PURGE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be purged (YES) or not (NO)</td></tr><tr><td valign="middle">BASE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number of the base object</td></tr><tr><td valign="middle">PURGE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number for the object which gets purged</td></tr></tbody></table>

<a id="e99593c6c7ac4a73"></a>
#### DBA_SCHEMAS

Identify the schemata in the database.

**Column information**

<a id="fd2ef76633c5bdd0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="a6c265fb230db73c"></a>
#### DBA_SCHEMA_PATH

DBA_SCHEMA_PATH describes the schema search order of all authorizations in the database.

**Column information**

<a id="403ae23a3db42d67"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the authorization</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the authorization</td></tr></tbody></table>

<a id="daa86a4baa2da962"></a>
#### DBA_SCHEMA_PRIVS

DBA_SCHEMA_PRIVS describes all schema grants in the database.

**Column information**

<a id="c2e9d71700485d23"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="96ca1d814ff79a79"></a>
#### DBA_SEQUENCES

DBA_SEQUENCES describes all sequences in the database.

**Column information**

<a id="ac9d2816b7304eda"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="0769222d676af254"></a>
#### DBA_SEQ_PRIVS

DBA_SEQ_PRIVS describes all sequence grants in the database.

**Column information**

<a id="60c24a3037849694"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b1561d03a6325d86"></a>
#### DBA_SHARD_KEY_COLUMNS

DBA_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="9eb6df73794f61e4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="495235a59ae69e64"></a>
#### DBA_SOURCE

DBA_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="5b145b3d6bf2e993"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="864adf1ed0b85e8d"></a>
#### DBA_STAT_SYSTEM

DBA_STAT_SYSTEM describes analyzed system statistics.

**Column information**

<a id="7956d05afce37a4b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CPU_OPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">OPS(operations per second) of CPU</td></tr><tr><td align="left" valign="middle">NETWORK_IOPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">IOPS(I/O operations per second) of Cluster NETWORK</td></tr><tr><td align="left" valign="middle">NETWORK_BUFSIZE</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">buffer size of Cluster NETWORK when analyzed</td></tr><tr><td valign="middle">BUFFER_MISS_PERCENT</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">disk buffer miss percent</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="7d59717cfb30bde6"></a>
#### DBA_SYS_PRIVS

DBA_SYS_PRIVS describes all system (database, tablespace, schema) privileges in the database.

**Column information**

<a id="28b27e7762aa4324"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the grantee</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="bf4c7fd510e5ed2c"></a>
#### DBA_SYNONYMS

DBA_SYNONYMS describes all synonyms in the database.

**Column information**

<a id="c44d0776b5640874"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="f1387ba16a271919"></a>
#### DBA_TABLES

DBA_TABLES describes all relational tables in the database.

**Column information**

<a id="792e6ad99df8a3a3"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="f51118eada7e83a5"></a>
#### DBA_TABLESPACES

DBA_TABLESPACES describes all tablespaces in the database.

**Column information**

<a id="dcb5798dac84c20d"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">PLUGGED_IN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is plugged in (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="8ec4cb5e6f13aa66"></a>
#### DBA_TAB_COLS

DBA_TAB_COLS describes the columns (including hidden columns) of all tables, views, and clusters in the database.

**Column information**

<a id="f947eed0f36483c8"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="a3618f854e82348e"></a>
#### DBA_TAB_COLUMNS

DBA_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="9fa4ccd172d2cfba"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="4e15d7e450bf2921"></a>
#### DBA_TAB_COMMENTS

DBA_TAB_COMMENTS displays comments on all tables and views in the database.

**Column information**

<a id="0ef86fa018a4ad39"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="ec534d07595ba95a"></a>
#### DBA_TAB_IDENTITY_COLS

DBA_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="304c1faf04f4eb9f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="center" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="center" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="cac1f4392fa25969"></a>
#### DBA_TAB_PLACE

DBA_TAB_PLACE describes node placement of all cluster tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="28965c4469eefbab"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td valign="middle">MEMBER_POSITION</td><td valign="middle">NUMBER</td><td valign="middle">Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td valign="middle">IS_UPDATE_MASTER</td><td valign="middle">BOOLEAN</td><td valign="middle">whether the cluster member is update master or not</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="1e6114e010b2b815"></a>
#### DBA_TAB_PRIVS

DBA_TAB_PRIVS describes all object grants in the database.

**Column information**

<a id="e5550d1a02d8b0ef"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="607fd41f8faf2627"></a>
#### DBA_TAB_SHARDS

DBA_TAB_SHARDS describes shard information of all sharded tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="6d552d1c9cb194cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="b22a15931fd4a77e"></a>
#### DBA_TBS_PRIVS

DBA_TBS_PRIVS describes all tablespace grants in the database.

**Column information**

<a id="b0bfa2a4ccbb916e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="4a81883c92f13198"></a>
#### DBA_USERS

DBA_USERS describes all users of the database.

**Column information**

<a id="00d013f3092cb556"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">PASSWORD</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">encrypted password</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">FAILED_LOGIN_ATTEMPTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Consecutive failed login attempts count</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">PROFIL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">User resource profile name</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr><tr><td align="left" valign="middle">PASSWORD_VERSIONS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Shows the list of versions of the password hashes (verifiers).</td></tr><tr><td align="left" valign="middle">EDITIONS_ENABLED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether editions have been enabled for the corresponding user (Y) or not (N).</td></tr><tr><td align="left" valign="middle">AUTHENTICATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the authentication mechanism for the user.</td></tr></tbody></table>

<a id="d9846c491023a6c7"></a>
#### DBA_VIEWS

DBA_VIEWS describes all views in the database.

**Column information**

<a id="f6e97a931949b9b7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="69068fb5285a5fda"></a>
### Views of USER_family

It retrieves information about objects which are owned by current user.

<a id="1438fd7fa7bc3061"></a>
#### USER_ALL_TABLES

USER_ALL_TABLES describes the object tables and relational tables owned by the current user.

**Column information**

<a id="02fc1d95b1663595"></a>
<table><thead><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="4f969b3f2fca8509"></a>
#### USER_ARGUMENTS

USER_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="4492dba739cc8325"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures |
| PACKAGE_NAME | VARCHAR(128) | Package Name of function, procedures |
| OBJECT_ID | NUMBER | ID of a function, procedures |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| ARGUMENT_NAME | VARCHAR(128) | Name of argument or attribute name of record type argument |
| POSITION | NUMBER | Position of argument or position of attribute in record type |
| SEQUENCE | NUMBER | Sequential order of argument and its attributes |
| DATA_LEVEL | NUMBER | Nesting depth of the argument for composite types |
| DATA_TYPE | VARCHAR(128) | Data type of the argument |
| DEFAULTED | VARCHAR(1) | Whether or not the argument is defaulted |
| DEFAULT_VALUE | VARCHAR(1) | Reserved for future use |
| DEFAULT_LENGTH | VARCHAR(1) | Reserved for future use |
| IN_OUT | VARCHAR(32) | Direction of the argument (IN, OUT, IN/OUT) |
| DATA_LENGTH | NUMBER | Length of the column(in bytes) |
| DATA_PRECISION | NUMBER | Length in decimal digits(NUMBER) or binary digits(FLOAT) |
| DATA_SCALE | NUMBER | Digits to the right of the decimal point in a number |
| RADIX | NUMBER | Argument radix for a number |
| CHARACTER_SET_NAME | VARCHAR(128) | Character set name for the argument |
| TYPE_OWNER | VARCHAR(128) | Owner of the type of the argument |
| TYPE_NAME | VARCHAR(128) | Name of the type of the argument |
| TYPE_SUBNAME | VARCHAR(128) | Name of the type of the argument declared in package |
| TYPE_LINK | VARCHAR(128) | Name of the type of the argument declared in a remote package |
| PLS_TYPE | VARCHAR(128) | Name of the type of the argument at PSM |
| CHAR_LENGTH | NUMBER | Character limit for string datatypes |
| CHAR_USED | VARCHAR(1) | Whether the byte limit(B) or char limit(C) is official for the string |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="0f6d2f2f8b16051c"></a>
#### USER_CATALOG

USER_CATALOG lists tables, views, synonyms, and sequences owned by the current user.

**Column information**

<a id="1f19cfcadba07dc2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="06a2915a6f4251f5"></a>
#### USER_COL_COMMENTS

USER_COL_COMMENTS displays comments on the columns of the tables and views owned by the current user.

**Column information**

<a id="593b12c732117a52"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="7a6a63782540de1d"></a>
#### USER_CLUSTER_TABLES

USER_CLUSTER_TABLES describes all cluster tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="ba90e73c86b927f5"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| SHARD_STRATEGY | VARCHAR(32) | Sharding strategy of the table:  the value in (CLONED, HASH SHARDING, RANGE SHARDING, LIST SHARDING) |
| SHARD_PLACEMENT | VARCHAR(32) | Shard placement of the table:  the value in (AT CLUSTER WIDE or AT CLUSTER GROUP) |
| SHARD_COUNT | NUMBER | Shard count of the table (if cloned table, the value is null) |
| SHARD_KEY_COUNT | NUMBER | Shard key column count of the table (if cloned table, the value is null) |
| HAS_GSI | VARCHAR(3) | Indicate whether the table has global secondary index: (YES) or (NO) |
| DROPPED | VARCHAR(3) | Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="b11bf359f4c02759"></a>
#### USER_COL_PRIVS

USER_COL_PRIVS describes the column object grants for which the current user is the object owner, grantor, or grantee.

**Column information**

<a id="f86e1fa13456cbf0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="9fa9497214b1f48a"></a>
#### USER_COL_PRIVS_MADE

USER_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner.

**Column information**

<a id="8afc9d0a76771eb0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b25ad58c537dae08"></a>
#### USER_COL_PRIVS_RECD

USER_COL_PRIVS_RECD describes the column object grants for which the current user is the grantee.

**Column information**

<a id="7f27b19bbf482154"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="49a3cdf0558f4f22"></a>
#### USER_CONSTRAINTS

USER_CONSTRAINTS describes all constraint definitions on tables owned by the current user.

**Column information**

<a id="2d0696754e158824"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="1acf36057e8255a2"></a>
#### USER_CONS_COLUMNS

USER_CONS_COLUMNS describes columns that are owned by the current user and that are specified in constraint definitions.

**Column information**

<a id="4fbe5b807aed92e8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="cfd3e93bcaee4b08"></a>
#### USER_DEPENDENCIES

USER_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column information**

<a id="478b6596856ae71e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, VIEW, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_OWNER | VARCHAR(128) | Owner of the referenced object |
| REFERENCED_SCHEMA_NAME | VARCHAR(128) | Schema Name of the referenced object |
| REFERENCED_TYPE | VARCHAR(32) | Type of the referenced object: FUNCTION, PROCEDURE, TABLE, VIEW, SEQUENCE, PACKAGE, PACKAGE BODY, TRIGGER |
| REFERENCED_LINK_NAME | VARCHAR(128) | Name of the link to the parent object |
| REFERENCED_NAME | VARCHAR(128) | Name of the referenced object |
| DEPENDENCY_TYPE | VARCHAR(32) | Indicates whether the dependency is a REF dependency (REF) or not (HARD) |

<a id="7f2907ccb7ecd908"></a>
#### USER_EXTENTS

USER_EXTENTS describes the extents comprising the segments owned by the current user's objects.

**Column information**

<a id="a30c1b826fa7127b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Extent number in the segment</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr></tbody></table>

<a id="1df448488581026a"></a>
#### USER_GLOBAL_SECONDARY_INDEXES

USER_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables owned by the current user.

> It is available only on a cluster.

**Column information**

<a id="1c8fe6d39f2e8e50"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| TABLESPACE_NAME | VARCHAR(128) | Name of the tablespace containing the global secondary index |
| INI_TRANS | NUMBER | Initial number of transactions |
| MAX_TRANS | NUMBER | Maximum number of transactions |
| INITIAL_EXTENT | NUMBER | Size of the initial extent |
| NEXT_EXTENT | NUMBER | Size of secondary extents |
| MIN_EXTENTS | NUMBER | Minimum number of extents allowed in the segment |
| MAX_EXTENTS | NUMBER | Maximum number of extents allowed in the segment |
| PCT_FREE | NUMBER | Minimum percentage of free space in a block |
| LOGGING | VARCHAR(3) | Indicates whether or not changes to the global secondary index are logged: (YES) or (NO) |
| BLOCKS | NUMBER | Number of used blocks in the global secondary index |
| EMPTY_BLOCKS | NUMBER | Number of empty blocks in the global secondary index |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |

<a id="8e8194788b369838"></a>
#### USER_GSI_PLACE

USER_GSI_PLACE describes node placement of all global secondary indexes on the tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="dcdc0eb4b7340510"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the global secondary index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the global secondary index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the global secondary index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the global secondary index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the global secondary index has been dropped and is in the recycle bin (YES) or not (NO) |
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="7647f6502f2a1110"></a>
#### USER_INDEXES

USER_INDEXES describes indexes owned by the current user.

**Column information**

<a id="e0bed8b94ec70201"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">ndicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="f3a38f32b1b180c7"></a>
#### USER_IND_COLUMNS

USER_IND_COLUMNS describes the columns of the indexes owned by the current user and columns of indexes on tables owned by the current user.

**Column information**

<a id="6dc0a03e7d5e48fc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="cedaaba10d63ec2f"></a>
#### USER_IND_PLACE

USER_IND_PLACE describes node placement of the indexes owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="afe9567d5ce5bc84"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| INDEX_SCHEMA | VARCHAR(128) | Schema of the index |
| INDEX_NAME | VARCHAR(128) | Name of the index |
| TABLE_OWNER | VARCHAR(128) | Owner of the indexed object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| DROPPED | VARCHAR(3) | Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO) |
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | (deprecated) |

<a id="f204b0b065e9afd8"></a>
#### USER_OBJECTS

USER_OBJECTS describes all objects owned by the current user.

**Column information**

<a id="9282549dffabcebd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="473be5a21f5824eb"></a>
#### USER_PACKAGE_PRIVS

USER_PACKAGE_PRIVS describes the package grants for which the current user is the package owner, grantor, or grantee.

**Column information**

<a id="0c22a1e370fbd6f7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="cca69e792bcc5384"></a>
#### USER_PACKAGE_PRIVS_MADE

USER_PACKAGE_PRIVS_MADE describes the package grants for which the current user is the package owner.

**Column information**

<a id="8b23b6a4a93fbe64"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="56cffc703ae94bea"></a>
#### USER_PACKAGE_PRIVS_RECD

USER_PACKAGE_PRIVS_RECD describes the package grants for which the current user is the grantee.

**Column information**

<a id="30144e8550237744"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="d4176987d553dd9c"></a>
#### USER_PROCEDURES

USER_PROCEDURES lists of procedures owned by the current user.

**Column information**

<a id="f1002bfbe4e12ec1"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of function, procedures or package |
| OBJECT_NAME | VARCHAR(128) | Name of function, procedures or package |
| PROCEDURE_NAME | VARCHAR(128) | Name when a procedures in package |
| OBJECT_ID | NUMBER | ID of a function, procedures or package |
| SUBPROGRAM_ID | NUMBER | ID of procedures in package |
| OVERLOAD | VARCHAR(32) | ID of overloading procedure in package |
| OBJECT_TYPE | VARCHAR(32) | Type of function, procedures or package |
| AGGREGATE | VARCHAR(3) | Indicate whether the procedure is an aggreage function(YES) or not(NO) |
| PIPELINED | VARCHAR(3) | Indicate whether the procedure is a pipelined table function(YES) or not(NO) |
| IMPLTYPEOWNER | VARCHAR(128) | Name of the owner of the implementation type, if any |
| IMPLTYPENAME | VARCHAR(128) | Name of the implementation type, if any |
| PARALLEL | VARCHAR(3) | Indicates whether the procedure or function is parallel-enabled (YES) or not (NO) |
| INTERFACE | VARCHAR(3) | YES, if the procedure/function is a table function implemented using the SQLCLI interface; otherwise NO |
| DETERMINISTIC | VARCHAR(3) | YES, if the procedure/function is declared to be deterministic; otherwise NO |
| AUTHID | VARCHAR(32) | Indicates whether the procedure/function is declared to execute as DEFINER or CURRENT_USER (invoker) |

<a id="19cd9be379541181"></a>
#### USER_PROC_PRIVS

USER_PROC_PRIVS describes the procedure grants for which the current user is the procedure owner, grantor, or grantee.

**Column information**

<a id="a59c7ffdf946350a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="bf9883b1f509220d"></a>
#### USER_PROC_PRIVS_MADE

USER_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column information**

<a id="d5bc4e7cb8e919f5"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="500cec8a704a0383"></a>
#### USER_PROC_PRIVS_RECD

USER_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="b62f9f8771682d04"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="f297b21f35a65701"></a>
#### USER_RECYCLEBIN

USER_RECYCLEBIN describes recycle bins owned by the current user.

**Column information**

<a id="0bb4d470421c2e0b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema name of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">ORIGINAL_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Original name of the object</td></tr><tr><td align="left" valign="middle">OPERATION</td><td valign="middle">VARCHAR(4)</td><td valign="middle">Operation carried out on the object</td></tr><tr><td valign="middle">OBJECT_TYPE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Type of the object</td></tr><tr><td valign="middle">TABLESPACE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the tablespace containing the object</td></tr><tr><td valign="middle">CREATED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Created time of the object</td></tr><tr><td valign="middle">DROPPED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Dropped time of the object</td></tr><tr><td valign="middle">DROP_SCN</td><td valign="middle">VARCHAR(128)</td><td valign="middle">System change number (SCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_GCN</td><td valign="middle">NUMBER</td><td valign="middle">Global change number (GCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_DCN</td><td valign="middle">NUMBER</td><td valign="middle">Domain change number (DCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_LCN</td><td valign="middle">NUMBER</td><td valign="middle">Local change number (LCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">CAN_UNDROP</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be undropped (YES) or not (NO)</td></tr><tr><td valign="middle">CAN_PURGE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be purged (YES) or not (NO)</td></tr><tr><td valign="middle">BASE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number of the base object</td></tr><tr><td valign="middle">PURGE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number for the object which gets purged</td></tr></tbody></table>

<a id="5610dfcb544783d8"></a>
#### USER_SCHEMAS

Identify the schemata in a catalog that are owned by current user.

**Column information**

<a id="f3b947773a15f551"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="853d53bf3852ec25"></a>
#### USER_SCHEMA_PATH

USER_SCHEMA_PATH describes the schema search order of the current user, for naming resolution of unqualified SQL schema objects.

**Column information**

<a id="6b32c21559aa2f9f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the user</td></tr></tbody></table>

<a id="42e569ffc08eaa7e"></a>
#### USER_SCHEMA_PRIVS

USER_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee.

**Column information**

<a id="0662084cbca9bba1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="9189cdd215a3f6c9"></a>
#### USER_SCHEMA_PRIVS_MADE

USER_SCHEMA_PRIVS_MADE describes the schema grants for which the current user is the schema owner.

**Column information**

<a id="99e5f628b6d61ff2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b9a938c458b2086c"></a>
#### USER_SCHEMA_PRIVS_RECD

USER_SCHEMA_PRIVS_RECD describes the schema grants for which the current user is the grantee.

**Column information**

<a id="09dbca53dbaaea78"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="161db83b8d0a0a6c"></a>
#### USER_SEQUENCES

USER_SEQUENCES describes all sequences owned by the current user.

**Column information**

<a id="d79ee04b0bb1296b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="05a47278a7aa4854"></a>
#### USER_SEQ_PRIVS

USER_SEQ_PRIVS describes the sequence grants for which the current user is the sequence owner, grantor, or grantee.

**Column information**

<a id="6a916d1471cc30e1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="bcb51f0f18a223bc"></a>
#### USER_SEQ_PRIVS_MADE

USER_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner.

**Column information**

<a id="1fe6d305094f2be3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="eecc8b3c5684b9e5"></a>
#### USER_SEQ_PRIVS_RECD

USER_SEQ_PRIVS_RECD describes the sequence grants for which the current user is the grantee.

**Column information**

<a id="2a5f01cd8f76181d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="9a9b25398e64dad7"></a>
#### USER_SHARD_KEY_COLUMNS

USER_SHARD_KEY_COLUMNS describes shard key columns of shareded tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="8c3b02d612a7c1ca"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="e53a45a11f69a70e"></a>
#### USER_SOURCE

USER_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="b2391b8862e87a2c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="80bcb28d89c77d97"></a>
#### USER_SYNONYMS

USER_SYNONYMS describes all synonyms owned by the current user.

**Column information**

<a id="24c368ebfb36e393"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="fdd8a2b2ae106800"></a>
#### USER_SYS_PRIVS

USER_SYS_PRIVS describes system (database, tablespace, schema) privileges granted to the current user or PUBLIC.

**Column information**

<a id="5311d72a7e0f9a07"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user, or PUBLIC</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="c8ea3eff0e79a43f"></a>
#### USER_TABLES

USER_TABLES describes the relational tables owned by the current user.

**Column information**

<a id="00b8c5ca9cca3430"></a>
<table><thead><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="cc1952b80fe375fa"></a>
#### USER_TABLESPACES

USER_TABLESPACES describes the tablespaces accessible to the current user.

**Column information**

<a id="9490a24b1e157f50"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="b173312f6dda49b5"></a>
#### USER_TAB_COLS

USER_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters owned by the current user.

**Column information**

<a id="9ea5c2e643c5d66c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="d251e708aecf7293"></a>
#### USER_TAB_COLUMNS

USER_TAB_COLUMNS describes the columns of the tables, views, and clusters owned by the current user.

**Column information**

<a id="f524b0a12dfe9f4e"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="1d20b67d42725db2"></a>
#### USER_TAB_COMMENTS

USER_TAB_COMMENTS displays comments on the tables and views owned by the current user.

**Column information**

<a id="57e7f5fe5e117bbf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="a5d76c720ade3719"></a>
#### USER_TAB_IDENTITY_COLS

USER_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="caf4692584e99e24"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="9ab464e8ab5dc8eb"></a>
#### USER_TAB_PLACE

USER_TAB_PLACE describes node placement of cluster tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="620f84eb122ba39f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td valign="middle">MEMBER_POSITION</td><td valign="middle">NUMBER</td><td valign="middle">Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td valign="middle">IS_UPDATE_MASTER</td><td valign="middle">BOOLEAN</td><td valign="middle">whether the cluster member is update master or not</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="a526df8a4548ccb9"></a>
#### USER_TAB_PRIVS

USER_TAB_PRIVS describes the object grants for which the current user is the object owner, grantor, or grantee.

**Column information**

<a id="402b9e6590b94287"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f75594eacee1c89a"></a>
#### USER_TAB_PRIVS_MADE

USER_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner.

**Column information**

<a id="fc42ca720ce2beff"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="8872650cc9a65964"></a>
#### USER_TAB_PRIVS_RECD

USER_TAB_PRIVS_RECD describes the object grants for which the current user is the grantee.

**Column information**

<a id="3f0fc7b9c953712e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="3e8fb597d4d1b321"></a>
#### USER_TAB_SHARDS

USER_TAB_SHARDS describes shard information of sharded tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="7dd011eafe34d9e2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="1b5ac7b711072e71"></a>
#### USER_USERS

USER_USERS describes the current user.

**Column information**

<a id="bbc96bd478deb0e1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr></tbody></table>

<a id="e012a67b85430c2d"></a>
#### USER_VIEWS

USER_VIEWS describes the views owned by the current user.

**Column information**

<a id="78100cbf4cdd3c6e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="4f11d27f4882c67f"></a>
### Other Views

There are other views or tables which are none of All-family, DBA-family or USER-family.

<a id="19c870a8e5ca2150"></a>
#### AUDIT_POLICIES

AUDIT_POLICIES contains one row for each audit policy.

**Column information**

<a id="fa403a7e1160dc7e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enabled (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the audit policy</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the audit policy</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the audit policy</td></tr></tbody></table>

<a id="f21689304f8cd82e"></a>
#### AUDIT_POLICY_OPTIONS

AUDIT_POLICY_OPTIONS describes all audit policies created in the database.

**Column information**

<a id="3ee97529db7470b9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">auditing option defined in the audit policy</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">The values of AUDIT_OPTION_TYPE_NAME in ( 'DATABASE PRIVILEGE', 'SYSTEM ACTION', 'OBJECT ACTION' )</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">object type name, for an object-specific auditing option</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="a319eb60b822016b"></a>
#### AUDIT_POLICY_ENABLED

AUDIT_POLICY_ENABLE describes all the audit policies that are enable in the database.

**Column information**

<a id="a9cd5cca35914a01"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED_OPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">enable option of the audit policy, the possible values are BY, EXCEPT</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name for whom the audit policy is enable</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="55a6aed1582db32b"></a>
#### AUDIT_TRAIL

AUDIT_TRAIL displays audit records from the audit trail.

**Column information**

<a id="25b3133627a03a23"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MEMBER_NAME | VARCHAR(128) | cluster member name |
| SESSION_ID | NUMBER | session identifier |
| SESSION_SERIAL | NUMBER | session serial number |
| LOGON_USERNAME | VARCHAR(128) | logon user name of the user whose actions were audited |
| CURRENT_USERNAME | VARCHAR(128) | effective user for the statement execution |
| SERVER_PROCESS | NUMBER | server process identifer for the session |
| CLIENT_PROGRAM_NAME | VARCHAR(128) | client program used for session |
| CLIENT_USERNAME | VARCHAR(128) | client operating system user name for the session |
| CLIENT_PROCESS | NUMBER | client process identifer for the session |
| CLIENT_HOST | VARCHAR(128) | client host ip address for the session |
| CLIENT_PORT | NUMBER | client port number for the session |
| CLIENT_TERMINAL | VARCHAR(128) | client terminal name for the session |
| TRANSACTION_ID | NUMBER | transaction identifier |
| SCN | VARCHAR(128) | system change number (SCN) string of the query at the time of the event |
| GCN | NUMBER | global change number (GCN) of the query at the time of the event |
| DCN | NUMBER | domain change number (DCN) of the query at the time of the event |
| LCN | NUMBER | local change number (LCN) of the query at the time of the event |
| STMT_NO | NUMBER | numeric number for each statement run in a session |
| SQL_TEXT | LONG VARCHAR | SQL associated with the event |
| SQL_BINDS | LONG VARCHAR | list of bind variables, if any, associated with SQL_TEXT |
| RETURN_CODE | NUMBER | error code generated by the action, zero if the action succeeded |
| ERROR_MESSAGE | VARCHAR(1024) | error message generated by the action, null if the action succeeded |
| ENTRY_ID | NUMBER | audit trail entry identifier in the session |
| EVENT_TIMESTAMP | TIMESTAMP(6) WITHOUT TIME ZONE | timestamp of the creation of the audit trail entry in local time zone |
| POLICY_NAME | VARCHAR(128) | audit policy name that caused the current audit record |
| PRIVILEGE_USED | VARCHAR(32) | database privilege used to execute the action |
| ACTION_NAME | VARCHAR(32) | action name executed by the user |
| OBJECT_TYPE | VARCHAR(32) | object type of object affected by the action |
| OBJECT_SCHEMA | VARCHAR(128) | schema name of object affected by the action |
| OBJECT_NAME | VARCHAR(128) | object name of object affected by the action |

<a id="40d20d05a0dec131"></a>
#### DATABASE_PROPERTIES

DATABASE_PROPERTIES lists permanent database properties.

**Column information**

<a id="a84ff01af34af06e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;PROPERTY_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Property name</td></tr><tr><td align="left">&nbsp;PROPERTY_VALUE</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property value</td></tr><tr><td align="left">&nbsp;DESCRIPTION</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property description</td></tr></tbody></table>

<a id="aa80408e2df2efc2"></a>
#### DBC_TABLE_TYPE_INFO

Identify the ODBC/JDBC table types available in this database.

**Column information**

<a id="cbfbcb2383ce0391"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE_ID</td><td align="left">&nbsp;NUMBER</td><td align="left">&nbsp;number identifier of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;name of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;IS_SUPPORTED</td><td align="left">&nbsp;BOOLEAN</td><td align="left">&nbsp;is supported feature</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;comments of the table type</td></tr></tbody></table>

<a id="60de923717c920b5"></a>
#### DICTIONARY

DICTIONARY contains descriptions of data dictionary tables and views.

**Column information**

<a id="658b63fe8bd80750"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;TABLE_SCHEMA</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Schema of the object</td></tr><tr><td align="left">&nbsp;TABLE_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Name of the object</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;Text comment on the object</td></tr></tbody></table>

<a id="01c5f638fecda3be"></a>
#### DICT_COLUMNS

DICT_COLUMNS contains descriptions of columns in data dictionary tables and views.

**Column information**

<a id="73f14b8a61991dec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object that contains the column</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object that contains the column</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Text comment on the column</td></tr></tbody></table>

<a id="7ab7758d90960848"></a>
#### IMPLEMENTATION_INFO

IMPLEMENTATION_INFO contains information about various aspects that are left implementation-defined.

**Column information**

<a id="7ae59b71072cd7bc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">identifier of the implementation item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="b1ef4f4f99e831cb"></a>
#### IMPLEMENTATION_INFO_BASE

The IMPLEMENTATION_INFO_BASE table has one row for each implementation information item.

**Column information**

<a id="ada0f86bcc201540"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if the implementation item is supported, FALSE if not</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="a1e74545aa879f54"></a>
#### JDBC_CLIENT_PROPS

JDBC_CLIENT_PROPS is the set of jdbc client properties.

**Column information**

<a id="3d0a66c17acad1d6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">property name</td></tr><tr><td align="left">MAX_LEN</td><td align="left">NATIVE_INTEGER</td><td align="left">max length of a value</td></tr><tr><td align="left">DEFAULT_VALUE</td><td align="left">VARCHAR(128)</td><td align="left">default value</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(256)</td><td align="left">descrption on that property</td></tr></tbody></table>

<a id="e7ded90959b41417"></a>
#### PRODUCT

PRODUCT is about the product name, version for ODBC, JDBC interface.

**Column information**

<a id="ebc29645c16c8473"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(32)</td><td align="left">the product name</td></tr><tr><td align="left">VERSION</td><td align="left">VARCHAR(128)</td><td align="left">product full version information</td></tr><tr><td align="left">PRODUCT_VERSION</td><td align="left">NUMBER</td><td align="left">product version</td></tr><tr><td align="left">MAJOR_VERSION</td><td align="left">NUMBER</td><td align="left">major version</td></tr><tr><td align="left">MINOR_VERSION</td><td align="left">NUMBER</td><td align="left">minor version</td></tr><tr><td align="left">PATCH_VERSION</td><td align="left">NUMBER</td><td align="left">patch version</td></tr></tbody></table>

<a id="a18b53ec7d4b77ef"></a>
#### SESSION_PRIVS

SESSION_PRIVS describes the privileges that are currently available to the user.

**Column information**

<a id="71d7e94420d6fc93"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE</td><td align="left">VARCHAR(256)</td><td align="left">Name of the privilege</td></tr></tbody></table>

<a id="b6f9d6f1292bdcd0"></a>
#### SUPPLEMENTAL_LOG_TABLE_INFO

SUPPLEMENTAL_LOG_TABLE_INFO describes table-level supplemental logging status.

**Column information**

<a id="458f6c813ed72bcb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUPPLEMENTAL_LOG_DATA_PK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of table-level PRIMARY KEY COLUMNS supplemental logging: IMPLICIT, EXPLICIT, NO</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="25450c6716b8667d"></a>
### Aliased Synonym

It is the public synonym which indicates the view or table in DICTIONARY_SCHEMA.

<a id="ac8bac064c67f7ef"></a>
#### COLS

COLS is a public synonym for USER_TAB_COLUMNS.

<a id="f0607259da4b3e30"></a>
#### DICT

DICT is a public synonym for DICTIONARY.

<a id="756bd9fad9385c64"></a>
#### IND

IND is a public synonym for USER_INDEXES.

<a id="407073ed93ff88fb"></a>
#### OBJ

OBJ is a public synonym for USER_OBJECTS.

<a id="37eac94b2a9bc5e8"></a>
#### SEQ

SEQ is a public synonym for USER_SEQUENCES.

<a id="d35458389d5b0686"></a>
#### TABS

TABS is a public synonym for USER_TABLES.

<a id="88fb6d4686319b4f"></a>
#### RECYCLEBIN

RECYCLEBIN is a public synonym for USER_RECYCLEBIN.

<a id="ee5a1a28f6ab5db9"></a>
## INFORMATION_SCHEMA

Views of INFORMATION_SCHEMA schema provides the same information as those defined in the SQL standard.

Execute *InformationSchema.sql* as follows to use the views.

- For standalone

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/standalone/InformationSchema.sql
```

- For cluster

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
```


> 
> - Views and tables of INFORMATION_SCHEMA can be retrieved from OPEN phase.
> - Objects stored in the recyclebin can not be retrieved in the view of INFORMATION_SCHEMA.
> 

<a id="862158c05fd113c1"></a>
### COLUMNS

Identify the columns of tables defined in this catalog that are accessible to given user or role.

**Column information**

<a id="376b063c4ca5f20f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the column |
| TABLE_OWNER | VARCHAR(128) | owner name of the column |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the column |
| TABLE_NAME | VARCHAR(128) | table name of the column |
| COLUMN_NAME | VARCHAR(128) | column name |
| ORDINAL_POSITION | NUMBER | the ordinal position (> 0) of the column in the table |
| COLUMN_DEFAULT | LONG VARCHAR | the default for the column |
| IS_NULLABLE | BOOLEAN | is nullable of the column |
| DATA_TYPE | VARCHAR(128) | the standard name of the data type |
| CHARACTER_MAXIMUM_LENGTH | NUMBER | the maximum length in characters |
| CHARACTER_OCTET_LENGTH | NUMBER | the maximum length in octets |
| NUMERIC_PRECISION | NUMBER | the numeric precision of the numerical Data type |
| NUMERIC_PRECISION_RADIX | NUMBER | the radix ( 2 or 10 ) of the precision of the numerical data type |
| NUMERIC_SCALE | NUMBER | the numeric scale of the exact numerical data type |
| DATETIME_PRECISION | NUMBER | for a datetime or interval type, the value is the fractional seconds precision |
| INTERVAL_TYPE | VARCHAR(32) | for a interval type, the value is in ( YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, YEAR TO MONTH, DAY TO HOUR, DAY TO MINUTE, DAY TO SECOND, HOUR TO MINUTE, HOUR TO SECOND, MINUTE TO SECOND ) |
| INTERVAL_PRECISION | NUMBER | for a interval type, the value is the leading precision |
| CHARACTER_SET_CATALOG | VARCHAR(128) | catalog name of the character set if is is a character string type |
| CHARACTER_SET_SCHEMA | VARCHAR(128) | schema name of the character set if is is a character string type |
| CHARACTER_SET_NAME | VARCHAR(128) | character set name of the character set if is is a character string type |
| COLLATION_CATALOG | VARCHAR(128) | catalog name of the applicable collation if is is a character string type |
| COLLATION_SCHEMA | VARCHAR(128) | schema name of the applicable collation if is is a character string type |
| COLLATION_NAME | VARCHAR(128) | collation name of the applicable collation if is is a character string type |
| DOMAIN_CATALOG | VARCHAR(128) | catalog name of the domain used by the column being described |
| DOMAIN_SCHEMA | VARCHAR(128) | schema name of the domain used by the column being described |
| DOMAIN_NAME | VARCHAR(128) | domain name of the domain used by the column being described |
| UDT_CATALOG | VARCHAR(128) | catalog name of the user-defined type of the data type being described |
| UDT_SCHEMA | VARCHAR(128) | schema name of the user-defined type of the data type being described |
| UDT_NAME | VARCHAR(128) | user-defined type name of the user-defined type of the data type being described |
| SCOPE_CATALOG | VARCHAR(128) | catalog name of the referenceable table if DATA_TYPE is REF |
| SCOPE_SCHEMA | VARCHAR(128) | schema name of the referenceable table if DATA_TYPE is REF |
| SCOPE_NAME | VARCHAR(128) | scope name of the referenceable table if DATA_TYPE is REF |
| MAXIMUM_CARDINALITY | NUMBER | maximum cardinality if DATA_TYPE is ARRAY |
| DTD_IDENTIFIER | NUMBER | data type descriptor identifier |
| IS_SELF_REFERENCING | BOOLEAN | is a self-referencing column |
| IS_IDENTITY | BOOLEAN | is an identity column |
| IDENTITY_GENERATION | VARCHAR(32) | for an identity column, the value is in ( ALWAYS, BY DEFAULT ) |
| IDENTITY_START | NUMBER | for an identity column, the start value of the identity column |
| IDENTITY_INCREMENT | NUMBER | for an identity column, the increment of the identity column |
| IDENTITY_MAXIMUM | NUMBER | for an identity column, the maximum value of the identity column |
| IDENTITY_MINIMUM | NUMBER | for an identity column, the minimum value of the identity column |
| IDENTITY_CYCLE | BOOLEAN | for an identity column, the cycle option |
| IS_GENERATED | BOOLEAN | is a generated column |
| GENERATION_EXPRESSION | VARCHAR(128) | for a generated column, the text of the generation expression |
| IS_SYSTEM_VERSION_START | BOOLEAN | is a system-version start column |
| IS_SYSTEM_VERSION_END | BOOLEAN | is a system-version end column |
| SYSTEM_VERSION_TIMESTAMP_GENERATION | VARCHAR(32) | for a system-version column, the value is ALWAYS |
| IS_UPDATABLE | BOOLEAN | is an updatable column |
| DECLARED_DATA_TYPE | VARCHAR(128) | the data type name that a user declared |
| DECLARED_NUMERIC_PRECISION | NUMBER | the precision value that a user declared |
| DECLARED_NUMERIC_SCALE | NUMBER | the scale value that a user declared |
| COMMENTS | VARCHAR(1024) | comments of the column |

<a id="3513f10a82eaacfc"></a>
### COLUMN_PRIVILEGES

Identify the privileges on columns of tables defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="a4c40d14d807675c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted column privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the column privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( SELECT, INSERT, UPDATE, REFERENCES )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="6d09d6d00df7e2a4"></a>
### CONSTRAINT_COLUMN_USAGE

Identify the columns used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column information**

<a id="31a7c8417ba50210"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="8e59d5218afb4e36"></a>
### CONSTRAINT_TABLE_USAGE

Identify the tables that are used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column information**

<a id="ae75d7da50a780a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="f48e861c743a5493"></a>
### INFORMATION_SCHEMA_CATALOG_NAME

Identify the catalog that contains the Information Schema

**Column information**

<a id="7a87c9e36c29db18"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CATALOG_NAME</td><td align="left">VARCHAR(128)</td><td align="left">the name of catalog in which this Information Schema resides</td></tr></tbody></table>

<a id="49ea1b984e8b0096"></a>
### KEY_COLUMN_USAGE

Identify the columns defined in this catalog that are constrained as keys and that are accessible by a given user or role.

**Column information**

<a id="f1dfac143d853de4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position of the specific column in the constraint being described. If the constraint described is a key of cardinality 1 (one), then the value of ORDINAL_POSITION is always 1 (one).</td></tr><tr><td align="left" valign="middle">POSITION_IN_UNIQUE_CONSTRAINT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the constraint being described is a foreign key constraint, then the value of POSITION_IN_UNIQUE_CONSTRAINT is the ordinal position of the referenced column corresponding to the referencing column being described, in the corresponding unique key constraint.</td></tr></tbody></table>

<a id="d08a4f2e2cafe21c"></a>
### MODULES

Identify the SQL-server modules in this catalog that are accessible to a given user or role.

**Column information**

<a id="69ee30909a921daa"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| DEFAULT_CHARACTER_SET_CATALOG | VARCHAR(128) | default character set catalog name of the SQL-server module |
| DEFAULT_CHARACTER_SET_SCHEMA | VARCHAR(128) | default character set schema name of the SQL-server module |
| DEFAULT_CHARACTER_SET | VARCHAR(128) | default character set name of the SQL-server module |
| DEFAULT_SCHEMA_CATALOG | VARCHAR(128) | catalog name of default schema of SQL-server module |
| DEFAULT_SCHEMA_NAME | VARCHAR(128) | default scheam name of the SQL-server module |
| MODULE_DEFINITION | LONG VARCHAR | definition of the SQL-server module |
| MODULE_AUTHORIZATION | VARCHAR(32) | authorization of the SQL-server module(DEFINER/INVOKER) |
| SQL_PATH | VARCHAR(1024) | described SQL PATH when the SQL-server module is defined |
| CREATED | TIMESTAMP(6) WITHOUT TIME ZONE | creation time of the SQL-server module |
| LAST_ALTERED | TIMESTAMP(6) WITHOUT TIME ZONE | most lately altered time of the SQL-server module |

<a id="e7c70d52f16d78b1"></a>
### MODULE_BODY

Identify the SQL-server module bodies in this catalog that are accessible to a given user or role.

**Column information**

<a id="33abdd245e98e991"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module' |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| MODULE_DEFINITION | LONG VARCHAR | definition of the SQL-server module body |
| CREATED | TIMESTAMP(6) WITHOUT TIME ZONE | creation time of the SQL-server module body |
| LAST_ALTERED | TIMESTAMP(6) WITHOUT TIME ZONE | most lately altered time of the SQL-server module body |

<a id="883bccb6f8be8f3b"></a>
### MODULE_BODY_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column information**

<a id="184f1362ffdd7937"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| REF_MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module of contained in definition text of the SQL-server module body |
| REF_MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module of contained in definition text of the SQL-server module body |
| REF_MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module of contained in definition text of the SQL-server module body |
| REF_MODULE_NAME | VARCHAR(128) | SQL-server module name of contained in definition text of the SQL-server module body |

<a id="99db489aa34445fc"></a>
### MODULE_BODY_ROUTINE_USAGE

Identify the SQL-invoked routines owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column information**

<a id="aa0fbe88294db4c8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| ROUTINE_CATALOG | VARCHAR(128) | catalog name of the SQL-invoked routine of contained in definition text of the SQL-server module body |
| ROUTINE_OWNER | VARCHAR(128) | owner name of the SQL-invoked routine of contained in definition text of the SQL-server module body |
| ROUTINE_SCHEMA | VARCHAR(128) | schema name of the SQL-invoked routine of contained in definition text of the SQL-server module body |
| ROUTINE_NAME | VARCHAR(128) | SQL-invoked routine name of contained in definition text of the SQL-server module body |

<a id="d417a02fa7b99dd2"></a>
### MODULE_BODY_SEQUENCE_USAGE

Identify the sequences owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column information**

<a id="bb3fc4adeaa406af"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| SEQUENCE_CATALOG | VARCHAR(128) | catalog name of the sequence of contained in definition text of the SQL-server module body |
| SEQUENCE_OWNER | VARCHAR(128) | owner name of the sequence of contained in definition text of the SQL-server module body |
| SEQUENCE_SCHEMA | VARCHAR(128) | schema name of the sequence of contained in definition text of the SQL-server module body |
| SEQUENCE_NAME | VARCHAR(128) | sequence name of contained in definition text of the SQL-server module body |

<a id="1f5d75ce654ebbc8"></a>
### MODULE_BODY_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column information**

<a id="4746e0e2799657e7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the table of contained in definition text of the SQL-server module body |
| TABLE_OWNER | VARCHAR(128) | owner name of the table of contained in definition text of the SQL-server module body |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the table of contained in definition text of the SQL-server module body |
| TABLE_NAME | VARCHAR(128) | table name of contained in definition text of the SQL-server module body |

<a id="dab1607e0125db59"></a>
### MODULE_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column information**

<a id="4923dd3cd61f3279"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| REF_MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module of contained in definition text of the SQL-server module |
| REF_MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module of contained in definition text of the SQL-server module |
| REF_MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module of contained in definition text of the SQL-server module |
| REF_MODULE_NAME | VARCHAR(128) | SQL-server module name of contained in definition text of the SQL-server module |

<a id="c166a2d6a380465f"></a>
### MODULE_PRIVILEGES

Identify the privileges on SQL-server modules defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="3741bc88a755cacd"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted SQL-server module privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the SQL-server module privilege being described is granted |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module on which the privilege being described was granted |
| MODULE_OWNER | VARCHAR(128) | owner name of the the SQL-server module on which the privilege being described was granted |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the the SQL-server module on which the privilege being described was granted |
| MODULE_NAME | VARCHAR(128) | name of the the SQL-server module on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="b27933ead88ef462"></a>
### MODULE_ROUTINE_USAGE

Identify the SQL-invoked routines owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column information**

<a id="85e251e66ae505bb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| ROUTINE_CATALOG | VARCHAR(128) | catalog name of the SQL-invoked routine of contained in definition text of the SQL-server module |
| ROUTINE_OWNER | VARCHAR(128) | owner name of the SQL-invoked routine of contained in definition text of the SQL-server module |
| ROUTINE_SCHEMA | VARCHAR(128) | schema name of the SQL-invoked routine of contained in definition text of the SQL-server module |
| ROUTINE_NAME | VARCHAR(128) | SQL-invoked routine name of contained in definition text of the SQL-server module |

<a id="2e3506dd75687d9a"></a>
### MODULE_SEQUENCE_USAGE

Identify the sequences owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column information**

<a id="e65d122f8a2ef8ee"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| SEQUENCE_CATALOG | VARCHAR(128) | catalog name of the sequence of contained in definition text of the SQL-server module |
| SEQUENCE_OWNER | VARCHAR(128) | owner name of the sequence of contained in definition text of the SQL-server module |
| SEQUENCE_SCHEMA | VARCHAR(128) | schema name of the sequence of contained in definition text of the SQL-server module |
| SEQUENCE_NAME | VARCHAR(128) | sequence name of contained in definition text of the SQL-server module |

<a id="72378676024bd0e6"></a>
### MODULE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column information**

<a id="e7f1d9a2ee4d54cb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the table of contained in definition text of the SQL-server module |
| TABLE_OWNER | VARCHAR(128) | owner name of the table of contained in definition text of the SQL-server module |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the table of contained in definition text of the SQL-server module |
| TABLE_NAME | VARCHAR(128) | table name of contained in definition text of the SQL-server module |

<a id="99f0ac33886a3993"></a>
### PARAMETERS

Identify the SQL parameters of SQL-invoked routines defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="ab69827244d5facf"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | catalog name of the specific name of the SQL- invoked routine that contains the SQL parameter being described |
| SPECIFIC_OWNER | VARCHAR(128) | owner name of the specific name of the SQL- invoked routine that contains the SQL parameter being described |
| SPECIFIC_SCHEMA | VARCHAR(128) | schema name of the specific name of the SQL- invoked routine that contains the SQL parameter being described |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the SQL- invoked routine that contains the SQL parameter being described |
| ORDINAL_POSITION | NUMBER | ordinal position of the SQL- invoked routine that contains the SQL parameter being described |
| PARAMETER_MODE | VARCHAR(32) | parameter mode of the SQL parameter being described |
| IS_RESULT | BOOLEAN | the parameter is RESULT parameter of type-preserving function |
| AS_LOCATOR | BOOLEAN | the parameter is passed as locator |
| PARAMETER_NAME | VARCHAR(128) | name of the SQL parameter being descaibed |
| FROM_SQL_SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the from-sql routine for the input parameter being described |
| FROM_SQL_SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the from-sql routine for the input parameter being described |
| FROM_SQL_SPECIFIC_NAME | VARCHAR(128) | specific name of the from-sql routine for the input parameter being described |
| TO_SQL_SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the to-sql routine for the input parameter being described |
| TO_SQL_SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the to-sql routine for the input parameter being described |
| TO_SQL_SPECIFIC_NAME | VARCHAR(128) | specific name of the to-sql routine for the input parameter being described |
| DATA_TYPE | VARCHAR(128) | data type of the SQL parameter being described |
| CHARACTER_MAXIMUM_LENGTH | NUMBER | maximum length of the SQL parameter being described |
| CHARACTER_OCTET_LENGTH | NUMBER | maximum length in octets of the SQL parameter being described |
| CHARACTER_SET_CATALOG | VARCHAR(128) | character set catalog name of the data type of the SQL parameter being described |
| CHARACTER_SET_SCHEMA | VARCHAR(128) | character set schema name of the data type of the SQL parameter being described |
| CHARACTER_SET_NAME | VARCHAR(128) | character set name of the data type of the SQL parameter being described |
| COLLATION_CATALOG | VARCHAR(128) | collation catalog name of the data type of the SQL parameter being described |
| COLLATION_SCHEMA | VARCHAR(128) | collation schema name of the data type of the SQL parameter being described |
| COLLATION_NAME | VARCHAR(128) | collation name of the data type of the SQL parameter being described |
| NUMERIC_PRECISION | NUMBER | precision of the data type of the SQL parameter being described |
| NUMERIC_PRECISION_RADIX | NUMBER | precision radix of the data type of the SQL parameter being described |
| NUMERIC_SCALE | NUMBER | scale of the data type of the SQL parameter being described |
| DATETIME_PRECISION | NUMBER | fractional second precisions of the data type of the SQL parameter being described |
| INTERVAL_TYPE | VARCHAR(32) | interval qualifier of the data type of the SQL parameter being described |
| INTERVAL_PRECISION | NUMBER | interval precision of the data type of the SQL parameter being described |
| UDT_CATALOG | VARCHAR(128) | catalog name of UDT of the data type of the SQL parameter being described |
| UDT_SCHEMA | VARCHAR(128) | schema name of UDT of the data type of the SQL parameter being described |
| UDT_NAME | VARCHAR(128) | name of UDT of the data type of the SQL parameter being described |
| SCOPE_CATALOG | VARCHAR(128) | catalog name of referenceable tables of the data type of the SQL parameter being described |
| SCOPE_SCHEMA | VARCHAR(128) | schema name of referenceable tables of the data type of the SQL parameter being described |
| SCOPE_NAME | VARCHAR(128) | name of referenceable tables of the data type of the SQL parameter being described |
| MAXIMUM_CARDINALITY | NUMBER | maximum cardinality of the data type of the SQL parameter being described |
| DTD_IDENTIFIER | NUMBER | dtd identifier of the data type of the SQL parameter being described |
| DECLARED_DATA_TYPE | VARCHAR(128) | declared data type of the SQL parameter being described |
| DECLARED_NUMERIC_PRECISION | NUMBER | precision of declared data type of the SQL parameter being described |
| DECLARED_NUMERIC_SCALE | NUMBER | scale of declared data type of the SQL parameter being described |
| PARAMETER_DEFAULT | LONG VARCHAR | default value of the SQL parameter being described |

<a id="f559226f2f473d62"></a>
### REFERENTIAL_CONSTRAINTS

Identify the referential constraints defined on tables in this catalog that are accessible to a given user or role.

**Column information**

<a id="5093d84867a1de5f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| CONSTRAINT_CATALOG | VARCHAR(128) | catalog name of the referential constraint |
| CONSTRAINT_OWNER | VARCHAR(128) | owner name who owns the referential constraint |
| CONSTRAINT_SCHEMA | VARCHAR(128) | schema name of the referential constraint being described |
| CONSTRAINT_NAME | VARCHAR(128) | referential constraint name |
| CONSTRAINT_TABLE_NAME | VARCHAR(128) | name of the table to which the referential constraint being described applies |
| CONSTRAINT_COLUMN_NAME | VARCHAR(128) | column name of the table to which the referential constraint being described applies |
| ORDINAL_POSITION | NUMBER | the ordinal position of the specific column in the referentail constraint being described. |
| UNIQUE_CONSTRAINT_CATALOG | VARCHAR(128) | catalog name of the unique or primary key constraint applied to the referenced column list being described |
| UNIQUE_CONSTRAINT_OWNER | VARCHAR(128) | owner name of the unique or primary key constraint applied to the referenced column list being described |
| UNIQUE_CONSTRAINT_SCHEMA | VARCHAR(128) | schema name of the unique or primary key constraint applied to the referenced column list being described |
| UNIQUE_CONSTRAINT_NAME | VARCHAR(128) | constraint name of the unique or primary key constraint applied to the referenced column list being described |
| UNIQUE_CONSTRAINT_TABLE_NAME | VARCHAR(128) | table name of the unique or primary key constraint applied to the referenced column list being described |
| UNIQUE_CONSTRAINT_COLUMN_NAME | VARCHAR(128) | column name of the unique or primary key constraint applied to the referenced column list being described |
| IS_PRIMARY_KEY | BOOLEAN | whether the constraint applied to the referenced column list being described, is primary key or not |
| MATCH_OPTION | VARCHAR(32) | the referential constraint that has a match option: the value in ( SIMPLE, PARTIAL, FULL ) |
| UPDATE_RULE | VARCHAR(32) | the referential constraint that has an update rule: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT ) |
| DELETE_RULE | VARCHAR(32) | the referential constraint that has a delete rule: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT ) |
| IS_DEFERRABLE | BOOLEAN | is a deferrable constraint |
| INITIALLY_DEFERRED | BOOLEAN | is an initially deferred constraint |

<a id="2ede67988561424a"></a>
### ROUTINES

Identify the SQL-invoked routines in this catalog that are accessible to a given user or role.

**Column information**

<a id="59c368dc7174d387"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the routine |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the routine |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the routine |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the routine |
| ROUTINE_CATALOG | VARCHAR(128) | catalog name of the routine |
| ROUTINE_OWNER | VARCHAR(128) | owner name of the routine |
| ROUTINE_SCHEMA | VARCHAR(128) | schema name of the routine |
| ROUTINE_NAME | VARCHAR(128) | null |
| ROUTINE_TYPE | VARCHAR(128) | name of the routine |
| MODULE_CATALOG | VARCHAR(128) | module name of the routine |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the module in which the routine is defined |
| MODULE_NAME | VARCHAR(128) | name of the module in which the routine is defined |
| UDT_CATALOG | VARCHAR(128) | catalog name of the user-defined data type which defined the routine as a method function |
| UDT_SCHEMA | VARCHAR(128) | schema name of the user-defined data type which defined the routine as a method function |
| UDT_NAME | VARCHAR(128) | name of the user-defined data type which defined the routine as a method function |
| DATA_TYPE | VARCHAR(128) | data type the routine returns |
| CHARACTER_MAXIMUM_LENGTH | NUMBER | maximum character length of data type the routine returns |
| CHARACTER_OCTET_LENGTH | NUMBER | maximum character length in octets of data type the routine returns |
| CHARACTER_SET_CATALOG | VARCHAR(128) | character set catalog name of data type the routine returns |
| CHARACTER_SET_SCHEMA | VARCHAR(128) | character set schema name of data type the routine returns |
| CHARACTER_SET_NAME | VARCHAR(128) | character set name of data type the routine returns |
| COLLATION_CATALOG | VARCHAR(128) | collation catalog name of data type the routine returns |
| COLLATION_SCHEMA | VARCHAR(128) | collation schema name of data type the routine returns |
| COLLATION_NAME | VARCHAR(128) | collation name of data type the routine returns |
| NUMERIC_PRECISION | NUMBER | precision of data type the routine returns |
| NUMERIC_PRECISION_RADIX | NUMBER | precision radix of data type the routine returns |
| NUMERIC_SCALE | NUMBER | scale of data type the routine returns |
| DATETIME_PRECISION | NUMBER | fractional seconds precision of data type the routine returns |
| INTERVAL_TYPE | VARCHAR(32) | interval qualifier for data type the routine returns |
| INTERVAL_PRECISION | NUMBER | interval leading field precision of data type the routine returns |
| TYPE_UDT_CATALOG | VARCHAR(128) | catalog name of the user-defined data type, which is the data type the routine returns |
| TYPE_UDT_SCHEMA | VARCHAR(128) | schema name of the user-defined data type, which is the data type the routine returns |
| TYPE_UDT_NAME | VARCHAR(128) | name of the user-defined data type, which is the data type the routine returns |
| SCOPE_CATALOG | VARCHAR(128) | catalog name of referenceable table |
| SCOPE_SCHEMA | VARCHAR(128) | schema name of referenceable table |
| SCOPE_NAME | VARCHAR(128) | name of referenceable table |
| MAXIMUM_CARDINALITY | NUMBER | maximum cardinality of data type the routine returns |
| DTD_IDENTIFIER | NUMBER | dtd ientifier of data type the routine returns |
| ROUTINE_BODY | VARCHAR(32) | type of the routine body |
| ROUTINE_DEFINITION | LONG VARCHAR | catalog name of the routine |
| EXTERNAL_NAME | VARCHAR(128) | external name of the external routine |
| EXTERNAL_LANGUAGE | VARCHAR(32) | language of the external routine |
| PARAMETER_STYLE | VARCHAR(32) | SQL parameter passing style of the external routine |
| IS_DETERMINISTIC | BOOLEAN | the routine is deterministic or not |
| SQL_DATA_ACCESS | VARCHAR(32) | routine possibly contains SQL or access data |
| IS_NULL_CALL | BOOLEAN | routine returns NULL if any of parameter values are NULL |
| SQL_PATH | VARCHAR(1024) | described SQL PATH when the routine is defined |
| SCHEMA_LEVEL_ROUTINE | BOOLEAN | the routine is schema-level routine |
| MAX_DYNAMIC_RESULT_SETS | NUMBER | max result set count of the routine |
| IS_USER_DEFINED_CAST | BOOLEAN | the routine is a function that is a user-defined cast function |
| IS_IMPLICITLY_INVOCABLE | BOOLEAN | the user-defined cast function is implicitly invocable |
| SECURITY_TYPE | VARCHAR(32) | security type of the routine(DEFINER/INVOKER) |
| TO_SQL_SPECIFIC_CATALOG | VARCHAR(128) | catalog name of the to-sql routine of the result type of routine |
| TO_SQL_SPECIFIC_SCHEMA | VARCHAR(128) | schema name of the to-sql routine of the result type of routine |
| TO_SQL_SPECIFIC_NAME | VARCHAR(128) | name of the to-sql routine of the result type of routine |
| AS_LOCATOR | BOOLEAN | return value of the routine is passed as locator |
| CREATED | TIMESTAMP(6) WITHOUT TIME ZONE | creation time of the routine |
| LAST_ALTERED | TIMESTAMP(6) WITHOUT TIME ZONE | most lately altered time of the routine |
| NEW_SAVEPOINT_LEVEL | BOOLEAN | specifiy new savepoint level or not |
| IS_UDT_DEPENDENT | BOOLEAN | routine is dependent |
| RESULT_CAST_FROM_DATA_TYPE | VARCHAR(128) | data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_AS_LOCATOR | BOOLEAN | locator indication which is specificed in result cast clause of the routine definition |
| RESULT_CAST_CHAR_MAX_LENGTH | NUMBER | maximum character length of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_CHAR_OCTET_LENGTH | NUMBER | maximum character length in octets of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_CHAR_SET_CATALOG | VARCHAR(128) | character set catalog name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_CHAR_SET_SCHEMA | VARCHAR(128) | character set schema name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_CHARACTER_SET_NAME | VARCHAR(128) | character set name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_COLLATION_CATALOG | VARCHAR(128) | collation catalog name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_COLLATION_SCHEMA | VARCHAR(128) | collation schema name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_COLLATION_NAME | VARCHAR(128) | collation name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_NUMERIC_PRECISION | NUMBER | precision of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_NUMERIC_RADIX | NUMBER | precision radix of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_NUMERIC_SCALE | NUMBER | scale of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_DATETIME_PRECISION | NUMBER | fractional seconds precision of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_INTERVAL_TYPE | VARCHAR(32) | interval qualifier of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_INTERVAL_PRECISION | NUMBER | interval precision of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_TYPE_UDT_CATALOG | VARCHAR(128) | UDT catalog name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_TYPE_UDT_SCHEMA | VARCHAR(128) | UDT schema name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_TYPE_UDT_NAME | VARCHAR(128) | UDT name of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_SCOPE_CATALOG | VARCHAR(128) | catalog name of referenceable table described in result cast clause of the routine definition |
| RESULT_CAST_SCOPE_SCHEMA | VARCHAR(128) | schema name of referenceable table described in result cast clause of the routine definition |
| RESULT_CAST_SCOPE_NAME | VARCHAR(128) | name of referenceable table described in result cast clause of the routine definition |
| RESULT_CAST_MAX_CARDINALITY | NUMBER | maximum cardinality of data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_DTD_IDENTIFIER | NUMBER | dtd identifier of data type which is specificed in result cast clause of the routine definition |
| DECLARED_DATA_TYPE | VARCHAR(128) | declared data type of the routine returns |
| DECLARED_NUMERIC_PRECISION | NUMBER | declared data type precision of the routine returns |
| DECLARED_NUMERIC_SCALE | NUMBER | declared data type scale of the routine returns |
| RESULT_CAST_FROM_DECLARED_DATA_TYPE | VARCHAR(128) | declared data type which is specificed in result cast clause of the routine definition |
| RESULT_CAST_DECLARED_NUMERIC_PRECISION | NUMBER | declared data type precision which is specificed in result cast clause of the routine definition |
| RESULT_CAST_DECLARED_NUMERIC_SCALE | NUMBER | declared data type scale which is specificed in result cast clause of the routine definition |

<a id="238c8531721434a8"></a>
### ROUTINE_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column information**

<a id="118c922fcc1a3953"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the routine |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the routine |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the routine |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the routine |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module of contained in routine body of the SQL-invoked routine |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module of contained in routine body of the SQL-invoked routine |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module of contained in routine body of the SQL-invoked routine |
| MODULE_NAME | VARCHAR(128) | SQL-server module name of contained in routine body of the SQL-invoked routine |

<a id="5d500865f3435e72"></a>
### ROUTINE_PRIVILEGES

Identify the privileges on SQL-invoked routines defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="b1c7a032ada57077"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted routine privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the routine privilege being described is granted |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_CATALOG | VARCHAR(128) | routine catalog name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_OWNER | VARCHAR(128) | null |
| ROUTINE_SCHEMA | VARCHAR(128) | routine schema name of the the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_NAME | VARCHAR(128) | routine name of the the SQL-invoked routine on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="7b4d79fe875a531b"></a>
### ROUTINE_ROUTINE_USAGE

Identify each SQL-invoked routine owned by a given user or role on which an SQL routine defined in this catalog is dependent.

**Column information**

<a id="c34df9e2e98b5c11"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the routine |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the routine |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the routine |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the routine |
| ROUTINE_CATALOG | VARCHAR(128) | routine catalog name of a routine contained in routine body of the SQL-invoked routine |
| ROUTINE_OWNER | VARCHAR(128) | routine owner name of a routine contained in routine body of the SQL-invoked routine |
| ROUTINE_SCHEMA | VARCHAR(128) | routine schema name of a routine contained in routine body of the SQL-invoked routine |
| ROUTINE_NAME | VARCHAR(128) | routine name of a routine contained in routine body of the SQL-invoked routine |

<a id="66f5a0e0bf39b757"></a>
### ROUTINE_SEQUENCE_USAGE

Identify each external sequence generator owned by a given user or role on which some SQL routine defined in this catalog is dependent.

**Column information**

<a id="f357c193c5892bdb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the routine |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the routine |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the routine |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the routine |
| SEQUENCE_CATALOG | VARCHAR(128) | catalog name of the sequence of contained in routine body of the SQL-invoked routine |
| SEQUENCE_OWNER | VARCHAR(128) | owner name of the sequence of contained in routine body of the SQL-invoked routine |
| SEQUENCE_SCHEMA | VARCHAR(128) | schema name of the sequence of contained in routine body of the SQL-invoked routine |
| SEQUENCE_NAME | VARCHAR(128) | sequence name of contained in routine body of the SQL-invoked routine |

<a id="1fdd736d83082ae4"></a>
### ROUTINE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column information**

<a id="265e6027070b6051"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the routine |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the routine |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the routine |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the routine |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the table of contained in routine body of the SQL-invoked routine |
| TABLE_OWNER | VARCHAR(128) | owner name of the table of contained in routine body of the SQL-invoked routine |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the table of contained in routine body of the SQL-invoked routine |
| TABLE_NAME | VARCHAR(128) | table name of contained in routine body of the SQL-invoked routine |

<a id="173534c19b31da0e"></a>
### SCHEMATA

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column information**

<a id="2aa7e8e70b651fea"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CATALOG_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name</td></tr><tr><td align="left" valign="middle">SCHEMA_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the schema</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">character set name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">SQL_PATH</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">character representation of schema path specification</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the schema</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the schema</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the schema</td></tr></tbody></table>

<a id="51d84c1c169adb6e"></a>
### SEQUENCES

Identify the external sequence generators defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="122719e89274a458"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the standard name of the data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION_RADIX</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the radix ( 2 or 10 ) of the precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric scale of the exact numerical data type</td></tr><tr><td align="left" valign="middle">START_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the start value of the sequence generator</td></tr><tr><td align="left" valign="middle">MINIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the minimum value of the sequence generator</td></tr><tr><td align="left" valign="middle">MAXIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the maximum value of the sequence generator</td></tr><tr><td align="left" valign="middle">INCREMENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the increment of the sequence generator</td></tr><tr><td align="left" valign="middle">CYCLE_OPTION</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">cycle option</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">DECLARED_DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the sequence generator</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the sequence generator</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the sequence generator</td></tr></tbody></table>

<a id="488404d71e73aadd"></a>
### SQL_FEATURES

List the features and subfeatures of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="98e4e1034169f08c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="67f0df2e641bb425"></a>
### SQL_IMPLEMENTATION_INFO

List the SQL-implementation information items defined in this ISO/IEC 9075 standard and, for each of these, indicate the value supported by the SQL-implementation.

**Column information**

<a id="cea3d28c08c3f72d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation information item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation information item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation information item</td></tr></tbody></table>

<a id="9601a3f8d0a1398d"></a>
### SQL_PACKAGES

List the packages of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="920ee7fa5c213afc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="8693a5797f6babe7"></a>
### SQL_PARTS

List the parts of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="e1a97ac4ba718414"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="305dd1e5c2661008"></a>
### SQL_SIZING

List the sizing items of this ISO/IEC 9075 standard, for each of these, indicate the size supported by the SQL-implementation.

**Column information**

<a id="4e96f0285b14cf7a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SIZING_ID</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">identifier of the sizing item</td></tr><tr><td align="left" valign="middle">SIZING_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the sizing item</td></tr><tr><td align="left" valign="middle">SUPPORTED_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the sizing item, or 0 if the size is unlimited or cannot be determined, or null if the features for which the sizing item is applicable are not supported</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the sizing item</td></tr></tbody></table>

<a id="cfa149df4197ca3c"></a>
### STATISTICS

Provide a list of statistics about a single table and the indexes associated with the table that are accessible to a given user or role.

**Column information**

<a id="2cfaaf074792c286"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">STAT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">statistics type: the value in ( TABLE STAT, INDEX CLUSTERED, INDEX HASHED, INDEX OTHER )</td></tr><tr><td align="left" valign="middle">NON_UNIQUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the index does not allow duplicate values</td></tr><tr><td align="left" valign="middle">INDEX_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the index</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the index</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the index</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ordinal position of the specific column in the index described</td></tr><tr><td align="left" valign="middle">IS_ASCENDING_ORDER</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">index key column being described is sorted in ASCENDING(TRUE) or DESCENDING(FALSE) order</td></tr><tr><td align="left" valign="middle">IS_NULLS_FIRST</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">the null values of the key column are sorted before(TRUE) or after(FALSE) non-null values</td></tr><tr><td align="left" valign="middle">CARDINALITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of rows in the table; otherwise, it is the number of unique values in the index</td></tr><tr><td align="left" valign="middle">PAGES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of pages used for the table; otherwise, it is the number of pages used for the current index.</td></tr><tr><td align="left" valign="middle">FILTER_CONDITION</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">filter condition, if any.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the table comments; otherwise, it is the index comments.</td></tr></tbody></table>

<a id="f020a030ee0fda34"></a>
### TABLES

Identify the tables defined in this catalog that are accessible to a given user or role

**Column information**

<a id="bb2a18b251343a48"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( BASE TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM VERSIONED, FIXED TABLE, DUMP TABLE )</td></tr><tr><td align="left" valign="middle">DBC_TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">ODBC/JDBC table type: the value is in ( TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, IMMUTABLE TABLE, SYSTEM TABLE, ALIAS, SYNONYM )</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name of the table, NULL if view</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_START_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version start column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_END_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version end column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_RETENTION_PERIOD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a system-versioned table, then the character representation of the value of the retention period of the table</td></tr><tr><td align="left" valign="middle">SELF_REFERENCING_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a typed table, then the name of the self-referencing column of the table</td></tr><tr><td align="left" valign="middle">REFERENCE_GENERATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table has a self-referencing column, the value is in ( SYSTEM GENERATED, USER GENERATED, DERIVED )</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the catalog name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the schema name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the name of the structured type</td></tr><tr><td align="left" valign="middle">IS_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable-into table</td></tr><tr><td align="left" valign="middle">IS_TYPED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a typed table</td></tr><tr><td align="left" valign="middle">COMMIT_ACTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a temporary table, the value is in ( DELETE, PRESERVE )</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the table</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the table</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the table</td></tr></tbody></table>

<a id="bd2c1cb9cf9012d3"></a>
### TABLE_CONSTRAINTS

Identify the table constraints defined on tables in this catalog that are accessible to a given user or role

**Column information**

<a id="2c120c2a3b67e9eb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( PRIMARY KEY, UNIQUE, FOREIGN KEY, NOT NULL, CHECK )</td></tr><tr><td align="left" valign="middle">IS_DEFERRABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a deferrable constraint</td></tr><tr><td align="left" valign="middle">INITIALLY_DEFERRED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an initially deferred constraint</td></tr><tr><td align="left" valign="middle">ENFORCED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an enforced constraint</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the constraint</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the constraint</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the constraint</td></tr></tbody></table>

<a id="1297d86cbd2a60f7"></a>
### TABLE_PRIVILEGES

Identify the privileges on tables of tables defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="53b02a7951986042"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted table privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the table privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CONTROL, SELECT, INSERT, UPDATE, DELETE, REFERENCES, LOCK, INDEX, ALTER )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr><tr><td align="left" valign="middle">WITH_HIERARCHY</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the privilege was granted WITH HIERARCHY OPTION or not</td></tr></tbody></table>

<a id="7b66867d8b957bd0"></a>
### USAGE_PRIVILEGES

Identify the USAGE privileges on objects defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="1df8721e70e7364b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted usage privileges, on the object of the type identified by OBJECT_TYPE</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization identifier of some user or role, or PUBLIC to indicate all users, to whom the usage privilege being described is granted</td></tr><tr><td align="left" valign="middle">OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( DOMAIN, CHARACTER SET, COLLATION, TRANSLATION, SEQUENCE )</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( USAGE )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="5a15cafa65c593ba"></a>
### VIEWS

Identify the viewed tables defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="807ce4dbc1ca06dd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">the character representation of the user-specified query expression contained in the corresponding view descriptor</td></tr><tr><td align="left" valign="middle">CHECK_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CASCADED, LOCAL, NONE )</td></tr><tr><td align="left" valign="middle">IS_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an updatable view</td></tr><tr><td align="left" valign="middle">INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable view</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an update INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_DELETABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether a delete INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an insert INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_COMPILED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is compiled or not</td></tr><tr><td align="left" valign="middle">IS_AFFECTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is affected by modification of underlying object or not</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the view</td></tr></tbody></table>

<a id="118bba2fac25f3a0"></a>
### VIEW_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which views defined in this catalog are dependent.

**Column information**

<a id="9b34a721e2483b40"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">MODULE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td>catalog name of the SQL-server module of contained in definition text of the view</td></tr><tr><td align="left" valign="middle">MODULE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td>owner name of the SQL-server module of contained in definition text of the view</td></tr><tr><td align="left" valign="middle">MODULE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td>schema name of the SQL-server module of contained in definition text of the view'</td></tr><tr><td align="left" valign="middle">MODULE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td>SQL-server module name of contained in definition text of the view</td></tr></tbody></table>

<a id="f5f734cce74edca7"></a>
### VIEW_ROUTINE_USAGE

Identify each routine owned by a given user or role on which a view defined in this catalog is dependent.

**Column information**

<a id="9ba154134a62612c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">SPECIFIC_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific catalog name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific owner name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific schema name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific name of a routine contained in the query expression of the view being described</td></tr></tbody></table>

<a id="0b26f99e1e845ded"></a>
### VIEW_TABLE_USAGE

Identify the tables on which viewed tables defined in this catalog and owned by a given user or role are dependent.

**Column information**

<a id="9d0121c7514eb9ec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr></tbody></table>

<a id="000c698afd5185ee"></a>
## PERFORMANCE_VIEW_SCHEMA

PERFORMANCE_VIEW_SCHEMA schema consists of views which can retrieve the current state of the system.

Execute *PerformanceViewSchema.sql* as follows to use the views.

- For standalone

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/PerformanceViewSchema.sql
```

- For cluster

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

The retrievable information of PERFORMANCE_VIEW_SCHEMA views vary upon its phase of the startup. (nomount, mount, open)  
Execute the followings to figure out the startup phase in which each views are retrieved.

```
gSQL> select table_name, startup_phase from v$tables order by 1;

TABLE_NAME                 STARTUP_PHASE
-------------------------- -------------
V$AGABLE_INFO              OPEN         
V$ARCHIVELOG               MOUNT        
V$AUDITABLE_DB_PRIVILEGES  NO_MOUNT     
V$AUDITABLE_SYSTEM_ACTIONS NO_MOUNT     
V$BACKUP                   MOUNT        
V$BALANCER                 OPEN         
V$BCH                      MOUNT        
V$BUFFER_STAT              MOUNT        
V$COLUMNS                  OPEN         
V$CONTROLFILE              MOUNT        
V$DATAFILE                 MOUNT        
V$DB_CHANGE_TRACKING       MOUNT        
V$DB_FILE                  MOUNT
V$DB_PROPERTY              OPEN        
V$DISPATCHER               OPEN         
V$ERROR_CODE               NO_MOUNT     
V$INCREMENTAL_BACKUP       MOUNT        
V$INSTANCE                 NO_MOUNT     
V$KEYWORDS                 NO_MOUNT     
V$LATCH                    NO_MOUNT     
V$LOCK_WAIT                OPEN         

TABLE_NAME             STARTUP_PHASE
---------------------- -------------
V$LOGFILE              MOUNT        
V$OPEN_CURSOR          NO_MOUNT     
V$PLAN_HISTORY         OPEN         
V$PLAN_HISTORY_LATEST  OPEN         
V$PROCESS_MEM_STAT     NO_MOUNT     
V$PROCESS_SQL_STAT     NO_MOUNT     
V$PROCESS_STAT         NO_MOUNT     
V$PROPERTY             NO_MOUNT
V$PROPERTY_ALIAS       NO_MOUNT      
V$PSM_RESERVED_WORDS   NO_MOUNT     
V$QUEUE                OPEN         
V$RESERVED_WORDS       NO_MOUNT     
V$SEQUENCE             OPEN         
V$SESSION              NO_MOUNT     
V$SESSION_AUDIT        OPEN         
V$SESSION_CONNECT_INFO NO_MOUNT     
V$SESSION_EVENT        OPEN         
V$SESSION_MEM_STAT     NO_MOUNT     
V$SESSION_SQL_STAT     NO_MOUNT     
V$SESSION_STAT         NO_MOUNT     
V$SESSION_WAIT         OPEN         

TABLE_NAME              STARTUP_PHASE
----------------------- -------------
V$SHARED_MODE           OPEN         
V$SHARED_SERVER         OPEN         
V$SHM_SEGMENT           NO_MOUNT     
V$SPROPERTY             NO_MOUNT     
V$SQLFN_METADATA        NO_MOUNT     
V$SQL_CACHE             NO_MOUNT     
V$SQL_COMMAND           NO_MOUNT     
V$SQL_HISTORY           NO_MOUNT     
V$STATEMENT             NO_MOUNT     
V$SYSTEM_EVENT          OPEN         
V$SYSTEM_MEM_STAT       NO_MOUNT     
V$SYSTEM_SQL_STAT       NO_MOUNT     
V$SYSTEM_STAT           NO_MOUNT     
V$TABLES                NO_MOUNT     
V$TABLESPACE            MOUNT        
V$TABLESPACE_STAT       OPEN         
V$TRANSACTION           OPEN         
V$WAIT_EVENT_CLASS_NAME OPEN         
V$WAIT_EVENT_NAME       OPEN         
V$XA_TRANSACTION        OPEN         

62 rows selected.
```

<a id="d58c9bb212f7071d"></a>
### GV$ Global View

The cluster provides GV$ view corresponding to almost every V$ views.  
V$ view retrieves the information of the currently connected server, but GV$ view retrieves the information of all servers.   
GV$ view includes all column information of V$ view, and it additionally has ORIGIN_MEMBER_NAME column which is a server having acquired the data (cluster member).

> It is available only on a cluster.

For example, V$TRANSACTION information retrieves the transaction information of the currently connected server as follows.

```
gSQL> SELECT TRANS_ID, SESSION_ID, TRANS_VIEW_SCN, START_TIME FROM V$TRANSACTION;

TRANS_ID SESSION_ID TRANS_VIEW_SCN START_TIME                
-------- ---------- -------------- --------------------------
40501296         48 1098.1.26      2017-04-07 17:14:01.912637
```

On the other hand, GV$TRANSACTION information retrieves the transaction information of all servers as follows.

```
gSQL> SELECT ORIGIN_MEMBER_NAME, TRANS_ID, SESSION_ID, TRANS_VIEW_SCN, START_TIME FROM GV$TRANSACTION;

ORIGIN_MEMBER_NAME TRANS_ID SESSION_ID TRANS_VIEW_SCN START_TIME                
------------------ -------- ---------- -------------- --------------------------
G1N1               40501296         48 1098.1.26      2017-04-07 17:14:01.912637
G2N2               40304688         48 1098.0.888     2017-04-07 17:14:55.134015
G2N1               42205232         48 1098.0.888     2017-04-07 17:14:55.135996
G1N2               40435760         48 1098.1.889     2017-04-07 17:14:01.910138
```

In the example above, the ORIGIN_MEMBER_NAME information indicates that the transaction information were obtained from the cluster members corresponding to G1N1, G2N1, G1N2, G2N2 each.

The information of a specific remote server can be retrieved by using the condition for ORIGIN_MEMBER_NAME column as follows.

```
gSQL> 
SELECT ORIGIN_MEMBER_NAME, TRANS_ID, SESSION_ID, TRANS_VIEW_SCN, START_TIME 
  FROM GV$TRANSACTION 
WHERE ORIGIN_MEMBER_NAME IN ( 'G2N1', 'G3N2' );

ORIGIN_MEMBER_NAME TRANS_ID SESSION_ID TRANS_VIEW_SCN START_TIME                
------------------ -------- ---------- -------------- --------------------------
G3N2               32178224         48 1099.0.888     2017-04-07 17:33:10.934752
G2N1               42270768         48 1099.0.888     2017-04-07 17:31:14.726007

2 rows selected.
```

<a id="a80dfcdff8fc4161"></a>
### V$AGABLE_INFO

The V$AGABLE_INFO displays the system agable information.

**Column information**

<a id="2e029238e3bd8e5b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCN</td><td align="left">VARCHAR(32)</td><td align="left">system scn</td></tr><tr><td align="left">AGABLE_SCN</td><td align="left">VARCHAR(32)</td><td align="left">system agable scn</td></tr><tr><td align="left">AGABLE_SCN_GAP</td><td align="left">VARCHAR(32)</td><td align="left">gap between system scn and agable scn</td></tr><tr><td align="left">OLDEST_SESSION_ID</td><td align="left">NUMBER</td><td align="left">identifier of session blocking aging</td></tr></tbody></table>

<a id="868cdcb7e99a1d9f"></a>
### V$ARCHIVELOG

The V$ARCHIVELOG displays information of log archiving.

**Column information**

<a id="313cf7e95c4a3b1f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ARCHIVELOG_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database log mode: the value in ( NOARCHIVELOG, ARCHIVELOG )</td></tr><tr><td align="left" valign="middle">LAST_ARCHIVED_LOG</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence number of last archived log file</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_DIR</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">archive destination path</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_FILE_PREFIX</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">file prefix name of the archived log</td></tr></tbody></table>

<a id="a0b81cc34bbc71b2"></a>
### V$AUDITABLE_DB_PRIVILEGES

The V$AUDITABLE_DB_PRIVILEGES displays auditable database privileges.

**Column information**

<a id="9f6ec89f8ed49e63"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE_ID</td><td align="left">NUMBER</td><td align="left">database privilege identifier</td></tr><tr><td align="left">PRIVILEGE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">database privilege name</td></tr></tbody></table>

<a id="024e0bb4861f3976"></a>
### V$AUDITABLE_SYSTEM_ACTIONS

The V$AUDITABLE_SYSTEM_ACTIONS displays auditable system actions.

**Column information**

<a id="36717f4d3d3081df"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ACTION_ID</td><td align="left">NUMBER</td><td align="left">auditable system action identifier</td></tr><tr><td align="left">ACTION_NAME</td><td align="left">VARCHAR(128)</td><td align="left">auditable system action name</td></tr></tbody></table>

<a id="763108e650cb91a5"></a>
### V$BACKUP

The V$BACKUP displays information of backup.

**Column information**

<a id="50ae0c7cbfed3c1a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">BACKUP_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">indicates whether the tablespace begin backup ( ACTIVE ) or not ( INACTIVE )</td></tr><tr><td align="left" valign="middle">BACKUP_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the last checkpoint lsn of tablespace when backup started</td></tr></tbody></table>

<a id="5f7c739b2d3022b8"></a>
### V$BALANCER

The V$BALANCER displays information of balancer.

**Column information**

<a id="cd2ffd7eced62470"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">balancer process identifier</td></tr><tr><td align="left">CUR_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">current number of connections</td></tr><tr><td align="left">CONNECTIONS</td><td align="left">NUMBER</td><td align="left">total number of connections</td></tr><tr><td align="left">CONNECTIONS_HIGHWATER</td><td align="left">NUMBER</td><td align="left">highest number of connections</td></tr><tr><td align="left">MAX_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">maximum connections</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">status</td></tr></tbody></table>

<a id="b2e6f5f03921af00"></a>
### V$BCH

The V$BCH displays information of database buffer control header array.

**Column information**

<a id="f36747b38a44eeda"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BCH_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">bch sequence</td></tr><tr><td align="left" valign="middle">TABLESPACE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier of the page cached in the frame of bch</td></tr><tr><td align="left" valign="middle">PAGE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page identifier of the page cached in the frame of bch</td></tr><tr><td valign="middle">LOGICAL_ADDRESS</td><td valign="middle">VARCHAR(18)</td><td valign="middle">logical address of the frame of bch</td></tr><tr><td valign="middle">DIRTY</td><td valign="middle">BOOLEAN</td><td valign="middle">dirty state of the page cached in the frame of bch</td></tr><tr><td valign="middle">PGAE_TYPE</td><td valign="middle">VARCHAR(20)</td><td valign="middle">page type of the page cached in the frame of bch</td></tr><tr><td valign="middle">FIRST_DIRTY_LSN</td><td valign="middle">NUMBER</td><td valign="middle">first dirty lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">RECOVERY_LSN</td><td valign="middle">NUMBER</td><td valign="middle">recovery lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">LAST_FLUSHED_LSN</td><td valign="middle">NUMBER</td><td valign="middle">last flushed lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">FIXED_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">fixed count of the page cached in the frame of bch</td></tr><tr><td valign="middle">TOUCHED_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">touched count of the page cached in the frame of bch</td></tr><tr><td valign="middle">RECENT_TOUCH_COUNT_INCREASED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">timestamp that touch count of the page cached in the frame of bch increased most recently</td></tr><tr><td valign="middle">BCH_LIST_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">list type to which the bch belongs</td></tr><tr><td valign="middle">BCH_STATE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">bch state</td></tr></tbody></table>

<a id="d1da52e764099878"></a>
### V$BUFFER_STAT

The V$BUFFER_STAT displays database buffer statistics.

**Column information**

<a id="715b5d553d4e522b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BUFFER_POOL_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total buffer frame size ( page count )</td></tr><tr><td align="left" valign="middle">HASH_BUCKET_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">buffer hash bucket count</td></tr><tr><td align="left" valign="middle">LRU_LIST_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">buffer lru list count</td></tr><tr><td valign="middle">HOT_REGION_PERCENTAGE</td><td valign="middle">NUMBER</td><td valign="middle">percentage of lru hot region</td></tr><tr><td valign="middle">HOT_REGION_CRITERIA</td><td valign="middle">NUMBER</td><td valign="middle">touch count criteria of lru hot region</td></tr><tr><td valign="middle">CHECKPOINT_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer checkpoint list count</td></tr><tr><td valign="middle">FLUSH_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer flush list count</td></tr><tr><td valign="middle">FREE_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer free list count</td></tr><tr><td valign="middle">FREE_BUFFER_WAIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of waiting for free list</td></tr><tr><td valign="middle">READ_COMPLETE_WAIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of waiting for read page complete</td></tr><tr><td valign="middle">BUFFER_LOOKUPS</td><td valign="middle">NUMBER</td><td valign="middle">total number of lookups in the buffer for requested pages</td></tr><tr><td valign="middle">BUFFER_HIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of hits in the buffer for requested pages</td></tr><tr><td valign="middle">BUFFER_MISS</td><td valign="middle">NUMBER</td><td valign="middle">total number of misses in the buffer for requested pages</td></tr><tr><td valign="middle">TOTAL_WRITES</td><td valign="middle">NUMBER</td><td valign="middle">total number of physical writes</td></tr><tr><td valign="middle">TOTAL_READS</td><td valign="middle">NUMBER</td><td valign="middle">total number of physical reads</td></tr><tr><td valign="middle">FLUSH_PER_SECOND</td><td valign="middle">NUMBER</td><td valign="middle">total number of disk writes per one second</td></tr><tr><td valign="middle">READ_PER_SECOND</td><td valign="middle">NUMBER</td><td valign="middle">total number of disk reads per one second</td></tr><tr><td valign="middle">AVERAGE_WRITE_LATENCY</td><td valign="middle">NUMBER</td><td valign="middle">average latency of disk writes</td></tr><tr><td valign="middle">AVERAGE_READ_LATENCY</td><td valign="middle">NUMBER</td><td valign="middle">average latency of disk reads</td></tr></tbody></table>

<a id="e586bbdf9a988b34"></a>
### V$CLUSTER_DISPATCHER

The V$CLUSTER_DISPATCHER displays cluster dispatcher information.

> It is available only on a cluster.

**Column information**

<a id="f691eb0826fdcaf2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">DISPATCHER_ID</td><td align="left">NUMBER</td><td align="left">dispatcher identifier</td></tr><tr><td align="left">IS_SYNC</td><td align="left">BOOLEAN</td><td align="left">whether the dispatcher is sync or not</td></tr><tr><td align="left">RX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has received through the dispatcher</td></tr><tr><td align="left">TX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has transmitted through the dispatcher</td></tr><tr><td align="left">RX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs received</td></tr><tr><td align="left">TX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs transmitted</td></tr></tbody></table>

<a id="423135d4ca5ad1c9"></a>
### V$CLUSTER_LOCATION

The V$CLUSTER_LOCATION displays cluster location information.

> It is available only on a cluster.

**Column information**

<a id="8269700c42ce7481"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">member name</td></tr><tr><td align="left">HOST</td><td align="left">VARCHAR(128)</td><td align="left">host name or IP address of a member</td></tr><tr><td align="left">PORT</td><td align="left">NUMBER</td><td align="left">host port of a member</td></tr></tbody></table>

<a id="fffe98e088d63f51"></a>
### V$CLUSTER_MEMBER

The V$CLUSTER_MEMBER displays cluster member information.

> It is available only on a cluster.

**Column information**

<a id="58f85f0d5d2ca7c4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member identifier</td></tr><tr><td align="left" valign="middle">MEMBER_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">status of the member: the value in ( ACTIVE, INACTIVE )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is global coordnator (TRUE) or not (FALSE)</td></tr><tr><td align="left" valign="middle">IS_GROUP_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is group coordnator (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="d6dff34dc75cc9f4"></a>
### V$COLUMNS

The V$COLUMNS has one row for each column of all the performance views (views beginning with V$).

Execute `\`desc as follows to retrieve the column information of performance view in nomount or mount phase in which V$COLUMNS is not available.

```
gSQL> \desc V$INSTANCE

COLUMN_NAME     TYPE                           IS_NULLABLE
--------------- ------------------------------ -----------
RELEASE_VERSION VARCHAR(64)          FALSE      
STARTUP_TIME    TIMESTAMP(6) WITHOUT TIME ZONE FALSE      
INSTANCE_STATUS VARCHAR(16)          FALSE
```

**Column information**

<a id="7eae09215cb2756b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position (&gt; 0) of the column in the performance view</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the column</td></tr></tbody></table>

<a id="a52e7a6f8281cfe4"></a>
### V$CONTROLFILE

This view displays information about GOLDILOCKS control files.

**Column information**

<a id="821bde152a245b5c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">control file status ( VALID, CORRUPTED )</td></tr><tr><td align="left">CONTROLFILE_NAME</td><td align="left">VARCHAR(1152)</td><td align="left">control file name ( absolute path )</td></tr><tr><td align="left">LAST_CHECKPOINT_LSN</td><td align="left">NATIVE_BIGINT</td><td align="left">the last checkpoint lsn</td></tr><tr><td align="left">IS_PRIMARY</td><td align="left">BOLLEAN</td><td align="left">indicates whether the control file is primary</td></tr></tbody></table>

<a id="8bbcf44ca7b9fdce"></a>
### V$DATAFILE

The V$DATAFILE displays information of all datafiles.

**Column information**

<a id="2556acbe02a748ce"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">DATAFILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">datafile name ( absolute path )</td></tr><tr><td align="left" valign="middle">CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">LSN at last checkpoint ( null if temporary tablespace )</td></tr><tr><td align="left" valign="middle">CREATION_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">timestamp of the datafile creation</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">datafile size ( in bytes )</td></tr><tr><td align="left" valign="middle">LOADED_CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">checkpoint LSN of the datafile loaded in memory</td></tr><tr><td align="left" valign="middle">CORRUPT_PAGE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">number of corrupt pages in the datafile</td></tr></tbody></table>

<a id="8362ecb7ffec5aad"></a>
### V$DB_CHANGE_TRACKING

The V$DB_CHANGE_TRACKING displays information of database change tracking.

**Column information**

<a id="375c78094581fd65"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLESPACE_ID</td><td align="left">NUMBER</td><td align="left">tablespage identifier</td></tr><tr><td align="left">DATAFILE_ID</td><td>NUMBER</td><td align="left">datafile identifier</td></tr><tr><td>CHANGE_TRACKING_STATE</td><td>VARCHAR(32)</td><td>state of dtafile change tracking</td></tr><tr><td>CHANGE_TRACKING_CHUNK_SEQ</td><td>NUMBER</td><td>sequence of change tracking chunk for datafile</td></tr><tr><td>MAX_SIZE</td><td>NUMBER</td><td>maximum size of datafile (byte)</td></tr><tr><td>BITMAP_BLOCK_COUNT</td><td>NUMBER</td><td>bitmap block count of change tracking chunk</td></tr><tr><td>LAST_PAGE_SEQ</td><td>NUMBER</td><td>the last page sequence of change tracking chunk</td></tr></tbody></table>

<a id="fa8b7c486a41ffb5"></a>
### V$DB_FILE

The V$DB_FILE displays a list of all files using in database.

**Column information**

<a id="c2fbbf6a7cbdf2c8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">FILE_NAME</td><td align="left">VARCHAR(1024)</td><td align="left">file name</td></tr><tr><td align="left">FILE_TYPE</td><td align="left">VARCHAR(16)</td><td align="left">file type</td></tr></tbody></table>

<a id="65585230f1401eab"></a>
### V$DB_PROPERTY

The V$DB_PROPERTY displays a list of permanent property.

**Column information**

<a id="ce708f31e6caa638"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr><tr><td valign="middle">IS_DEPRECATED</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property is deprecated or not: the value in (TRUE, FALSE)</td></tr><tr><td valign="middle">IS_GLOBAL</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property scope is global or not: the value in (TRUE, FALSE)</td></tr></tbody></table>

<a id="445052756750e122"></a>
### V$DISPATCHER

The V$DISPATCHER displays information of dispatchers.

**Column information**

<a id="a498712ec3aed65a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher process identifier</td></tr><tr><td align="left" valign="middle">RESPONSE_JOB_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">response job count</td></tr><tr><td align="left" valign="middle">ACCEPT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">indicates whether this dispatcher is accepting new connections</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">process start time</td></tr><tr><td align="left" valign="middle">CUR_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS_HIGHWATER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">highest number of connections</td></tr><tr><td align="left" valign="middle">MAX_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum connections</td></tr><tr><td align="left" valign="middle">RECV_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">receive status</td></tr><tr><td align="left" valign="middle">RECV_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of received</td></tr><tr><td align="left" valign="middle">RECV_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of received</td></tr><tr><td align="left" valign="middle">RECV_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">RECV_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">send status</td></tr><tr><td align="left" valign="middle">SEND_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of sent</td></tr><tr><td align="left" valign="middle">SEND_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of sent</td></tr><tr><td align="left" valign="middle">SEND_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of send (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of send (1/100 second)</td></tr></tbody></table>

<a id="1d8b9882b683bd3b"></a>
### V$ERROR_CODE

The V$ERROR_CODE displays a list of all GOLDILOCKS error codes.

**Column information**

<a id="0b8919dee141be90"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ERROR_CODE</td><td align="left">NUMBER</td><td align="left">GOLDILOCKS error code</td></tr><tr><td align="left">SQL_STATE</td><td align="left">VARCHAR(32)</td><td align="left">standard SQLSTATE code</td></tr><tr><td align="left">ERROR_MESSAGE</td><td align="left">VARCHAR(1024)</td><td align="left">error message</td></tr></tbody></table>

<a id="3c45d1757862abaf"></a>
### V$GLOBAL_TRANSACTION

The V$GLOBAL_TRANSACTION displays information on the currently active global transactions.

**Column information**

<a id="3247fc77f48fffb8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">global transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the global transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the global transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">global transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the global transaction is repreparable</td></tr></tbody></table>

<a id="a9d8eb2694e9e1bb"></a>
### V$INCREMENTAL_BACKUP

The V$INCREMENTAL_BACKUP displays information about control files and datafiles in backup sets from the control file.

**Column information**

<a id="03c9a5d775406c51"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BACKUP_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">backup file name ( absolute path )</td></tr><tr><td align="left" valign="middle">BACKUP_SCOPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">incremental backup scope: the value in ( database, tablespace, control )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_LEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">incremental backup level: the value in ( 0, 1, 2, 3, 4 )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">incremental backup type: the value in ( DIFFERENTIAL, CUMULATIVE )</td></tr><tr><td align="left" valign="middle">LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">all changes up to checkpoint LSN are included in this backup</td></tr><tr><td align="left" valign="middle">BEGIN_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup beginning time</td></tr><tr><td align="left" valign="middle">COMPLETION_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup completion time</td></tr></tbody></table>

<a id="1e2acc67b4840530"></a>
### V$INSTANCE

This view displays the state of the current instance.

**Column information**

<a id="c28c8b53ec21c7d1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">RELEASE_VERSION</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">release version</td></tr><tr><td align="left" valign="middle">STARTUP_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">time when the instance was started</td></tr><tr><td align="left" valign="middle">INSTANCE_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">status of the instance: the value in ( STARTED, MOUNTED, OPEN )</td></tr></tbody></table>

<a id="93dc56ef4512c4fe"></a>
### V$JOURNALING

The V$JOURNALING displays journaling information.

> It is available only on a cluster.

**Column information**

<a id="cba368d3dfe3adda"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">table name</td></tr><tr><td align="left">SHARD_ID</td><td align="left">NUMBER</td><td align="left">shard identifier</td></tr><tr><td align="left">RECORD_COUNT</td><td align="left">NUMBER</td><td align="left">journaled record count</td></tr><tr><td align="left">TOTAL_SIZE</td><td align="left">NUMBER</td><td align="left">total size of journaled records (byte)</td></tr></tbody></table>

<a id="67f0fb12c1cb72b7"></a>
### V$KEYWORDS

The V$KEYWORDS displays a list of all SQL keywords.

**Column information**

<a id="3e09298ae9a4c333"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">KEYWORD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of keyword</td></tr><tr><td align="left" valign="middle">KEYWORD_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">length of the keyword</td></tr><tr><td align="left" valign="middle">IS_RESERVED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the keyword cannot be used as an identifier (TRUE) or whether the keyword is not reserved (FALSE)</td></tr></tbody></table>

<a id="362c10450502fe27"></a>
### V$LATCH

The V$LATCH shows latch information.

**Column information**

<a id="452f9a27a08a6a18"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">LATCH_DESCRIPTION</td><td align="left">VARCHAR(64)</td><td align="left">latch description</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">reference count</td></tr><tr><td align="left">SPIN_LOCK</td><td align="left">VARCHAR(3)</td><td align="left">indicates whether the spin lock is locked ( YES ) or not ( NO )</td></tr><tr><td align="left">WAIT_COUNT</td><td align="left">NUMBER</td><td align="left">wait count</td></tr><tr><td align="left">CURRENT_MODE</td><td align="left">VARCHAR(32)</td><td align="left">current latch mode: the value in ( INITIAL, SHARED, EXCLUSIVE )</td></tr></tbody></table>

<a id="9a6fce93212c7758"></a>
### V$LICENSE

The V$LICENSE displays information of current license.

**Column information**

<a id="7653a58130305880"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>LICENSE_TYPE</td><td align="left">VARCHAR(8)</td><td>license type</td></tr><tr><td>START_DATE</td><td>DATE</td><td>start date of the license</td></tr><tr><td>EXPIRE_DATE</td><td>DATE</td><td>expire date of the license</td></tr></tbody></table>

<a id="95becc1aef220e54"></a>
### V$LOGFILE

The V$LOGFILE displays information of all redo log members.

**Column information**

<a id="7e930170cd0f9d41"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">redo log group identifier</td></tr><tr><td align="left" valign="middle">FILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">name of the log member</td></tr><tr><td align="left" valign="middle">GROUP_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the log group: the value in ( UNUSED, ACTIVE, CURRENT, INACTIVE )</td></tr><tr><td align="left" valign="middle">FILE_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file sequence number of the log member</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file size of the log member ( in bytes )</td></tr></tbody></table>

<a id="d238b39d25175bf5"></a>
### V$LOCK_WAIT

This view lists the locks currently held and outstanding requests for a lock.

**Column information**

<a id="0de186dc7e58b044"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GRANT_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that holds the lock</td></tr><tr><td align="left">REQUEST_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that requests the lock</td></tr></tbody></table>

<a id="6712cab30aa68384"></a>
### V$LOCKED_OBJECT

This view shows locked object information.

**Column information**

<a id="1a9cf28f7e8fcb82"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">LOCK_SLOT_ID</td><td align="left">NUMBER</td><td align="left">lock slot identifier</td></tr><tr><td>TABLE_OWNER</td><td>VARCHAR(128)</td><td>owner name who owns the locked table</td></tr><tr><td>TABLE_SCHEMA</td><td>VARCHAR(128)</td><td>schema of the locked table</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">locked table name</td></tr><tr><td>LOCK_MODE</td><td>VARCHAR(8)</td><td>granted lock mode (IS, IX, S, X, SIX)</td></tr></tbody></table>

<a id="9b263a9b95471ca5"></a>
### V$OPEN_CURSOR

The view lists display cursor status information for each current session.

**Column information**

<a id="54639ff609f29499"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td>ID of the session</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td>NAME of the user</td></tr><tr><td align="left">CURSOR_NAME</td><td align="left">VARCHAR(128)</td><td>NAME of the cursor</td></tr><tr><td align="left">PSM_CURSOR_ID</td><td align="left">NUMBER</td><td>ID of the PSM cursor</td></tr><tr><td>SQL_TEXT</td><td>LONG VARCHAR</td><td>SQL text for the cursor</td></tr><tr><td>IS_PSM_CURSOR</td><td>BOOLEAN</td><td>is PSM cursor</td></tr><tr><td>IS_OPEN</td><td>BOOLEAN</td><td>is open</td></tr><tr><td>OPEN_TIME</td><td>TIMESTAMP(6) WITHOUT TIME ZONE</td><td>cursor open time</td></tr><tr><td>LAST_EXEC_TIME</td><td>NATIVE_BIGINT</td><td>last execution time(us)</td></tr><tr><td>IS_SENSITIVE</td><td>BOOLEAN</td><td>is sensitive</td></tr><tr><td>IS_SCROLLABLE</td><td>BOOLEAN</td><td>is scrollable</td></tr><tr><td>IS_HOLDABLE</td><td>BOOLEAN</td><td>is holdable</td></tr><tr><td>IS_UPDATABLE</td><td>BOOLEAN</td><td>is updatable</td></tr></tbody></table>

<a id="64b23a8871a87bb2"></a>
### V$PLAN_HISTORY

The V$PLAN_HISTORY displays information of SQL plans.

**Column information**

<a id="2fa8a28eedecfb65"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">DRIVER_SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver session identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">STMT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement identifier in a session</td></tr><tr><td align="left" valign="middle">CL_STMT_ID</td><td>NUMBER</td><td>cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">DRIVER_CL_STMT_ID</td><td>NUMBER</td><td>driver cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_POS</td><td>NUMBER</td><td align="left" valign="middle">plan history position</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_ID</td><td>NUMBER</td><td>plan history identifier</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">SQL text for the statement</td></tr><tr><td align="left" valign="middle">PLAN_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">plan text for the statement</td></tr><tr><td align="left" valign="middle">LAST_EXEC_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement last execution time</td></tr></tbody></table>

<a id="a463d1c7d379dc2a"></a>
### V$PLAN_HISTORY_LATEST

The V$PLAN_HISTORY_LATEST displays information of the latest SQL plan.

**Column information**

<a id="61001474f7a4f83c"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">DRIVER_SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver session identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">STMT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement identifier in a session</td></tr><tr><td align="left" valign="middle">CL_STMT_ID</td><td>NUMBER</td><td>cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">DRIVER_CL_STMT_ID</td><td>NUMBER</td><td>driver cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_POS</td><td>NUMBER</td><td align="left" valign="middle">plan history position</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_ID</td><td>NUMBER</td><td>plan history identifier</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">SQL text for the statement</td></tr><tr><td align="left" valign="middle">PLAN_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">plan text for the statement</td></tr><tr><td align="left" valign="middle">LAST_EXEC_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement last execution time</td></tr></tbody></table>

<a id="8e0a3ac5159b62d3"></a>
### V$PROCESS_STAT

The V$PROCESS_STAT displays goldilocks process statistics.

**Column information**

<a id="9ef886acc12cbecc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="d0dc696c29bed7bd"></a>
### V$PROCESS_MEM_STAT

The V$PROCESS_MEM_STAT displays goldilocks process memory statistics.

**Column information**

<a id="b214f397a8d4799f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="f8da9dc38270e60b"></a>
### V$PROCESS_SQL_STAT

The V$PROCESS_SQL_STAT displays goldilocks process SQL statistics.

**Column information**

<a id="2300d044c5361ccd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="293ee5f5b7377b02"></a>
### V$PROPERTY

The V$PROPERTY displays a list of all properties at current session. Otherwise, the instance-wide value.

**Column information**

<a id="5ae8362c76f0240c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the session</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr><tr><td valign="middle">IS_DEPRECATED</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property is deprecated or not: the value in (TRUE, FALSE)</td></tr><tr><td valign="middle">IS_GLOBAL</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property scope is global or not: the value in (TRUE, FALSE)</td></tr></tbody></table>

<a id="6b38901dc4eaec7c"></a>
### V$PROPERTY_ALIAS

The V$PROPERTY_ALIAS displays a list of all properties alias.

**Column information**

<a id="50deb30178b5ca72"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">original name of the property</td></tr><tr><td align="left" valign="middle">PROPERTY_ALIAS</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">alias name of the property</td></tr></tbody></table>

<a id="ad66ee2e20afa9ac"></a>
### V$PSM_RESERVED_WORDS

The V$PSM_RESERVED_WORDS displays a list of all PSM reserved keywords. Reserved words cannot be used in variable name or procedure name.

**Column information**

<a id="d61e5424e916b620"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| KEYWORD_NAME | VARCHAR(128) | name of keyword |
| KEYWORD_LENGTH | NUMBER | length of the keyword |

<a id="dfeff9c4f505488e"></a>
### V$QUEUE

The V$QUEUE displays information of queue.

**Column information**

<a id="417a2290fda89a11"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TYPE</td><td align="left">NUMBER</td><td align="left">queue type ( COMMON or DISPATCHER )</td></tr><tr><td align="left">INDEX</td><td align="left">NUMBER</td><td align="left">index</td></tr><tr><td align="left">QUEUED</td><td align="left">NUMBER</td><td align="left">number of items in the queue</td></tr><tr><td align="left">WAIT</td><td align="left">NUMBER</td><td align="left">total time that all items in this queue have waited (1/100 second)</td></tr><tr><td align="left">TOTALQ</td><td align="left">VARCHAR(128)</td><td align="left">total number of items that have ever been in the queue</td></tr></tbody></table>

<a id="d58140da46e78771"></a>
### V$RESERVED_WORDS

The V$RESERVED_WORDS displays a list of all SQL reserved keywords. Reserved words cannot be used in table name or column name.

**Column information**

<a id="a504a99b6500daea"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">KEYWORD_NAME</td><td align="left">VARCHAR(128)</td><td align="left">name of keyword</td></tr><tr><td align="left">KEYWORD_LENGTH</td><td align="left">NUMBER</td><td align="left">length of the keyword</td></tr></tbody></table>

<a id="9f3b4d81f2540177"></a>
### V$SEQUENCE

The V$SEQUENCE displays information of sequences

**Column information**

<a id="45b9227172a6527a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">PHYSICAL_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence physical identifier</td></tr><tr><td align="left" valign="middle">START_WITH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">start with value</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">increment value</td></tr><tr><td align="left" valign="middle">MAXVALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value</td></tr><tr><td align="left" valign="middle">MINVALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">cache size</td></tr><tr><td align="left" valign="middle">LOCAL_NEXT_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local next value</td></tr><tr><td align="left" valign="middle">LOCAL_CURR_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local current value</td></tr><tr><td align="left" valign="middle">RESTART_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">restart value</td></tr><tr><td align="left" valign="middle">CYCLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">allow cycle</td></tr><tr><td align="left" valign="middle">USE_LAST_VALUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">use last value or not</td></tr><tr><td align="left" valign="middle">LOCAL_CACHE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current local cache count</td></tr><tr><td align="left" valign="middle">GLOBAL_NEXT_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">global next cache chunk start value</td></tr><tr><td align="left" valign="middle">SYNC_COMPARE_SN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">serial number for global sequence synchronization</td></tr><tr><td>GLOBAL_LATCH_SESSION_ID</td><td>NUMBER</td><td>identifier of the session acquiring the global latch ( -1 if the latch is not acquired )</td></tr><tr><td>GLOBAL_LATCH_SESSION_SERIAL</td><td>NUMBER</td><td>serial number of the session acquiring the global latch ( -1 if the latch is not acquired )</td></tr><tr><td>DDL_LATCH_SESSION_ID</td><td>NUMBER</td><td>identifier of the session acquiring the ddl latch ( -1 if the latch is not acquired )</td></tr><tr><td>DDL_LATCH_SESSION_SERIAL</td><td>NUMBER</td><td>serial number of the session acquiring the ddl latch ( -1 if the latch is not acquired )</td></tr><tr><td>LOCAL_LATCH_SESSION_ID</td><td>NUMBER</td><td>identifier of the session acquiring the local latch ( -1 if the latch is not acquired )</td></tr><tr><td>LOCAL_LATCH_SESSION_SERIAL</td><td>NUMBER</td><td>serial number of the session acquiring the local latch ( -1 if the latch is not acquired )</td></tr><tr><td>IS_ONLINE</td><td>BOOLEAN</td><td>is online</td></tr><tr><td valign="middle">LAST_SYNC_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">last time the sequence was synchronized</td></tr></tbody></table>

<a id="e5ac415663cd356e"></a>
### V$SESSION

The V$SESSION displays session information for each current session.

**Column information**

<a id="9d6b1286b8c9e8f9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier ( -1 if inactive transaction )</td></tr><tr><td align="left" valign="middle">CONNECTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">connection type: the value in ( DA, TCP )</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name</td></tr><tr><td align="left" valign="middle">SESSION_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">status of the session: the value in ( CONNECTED, SIGNALED, SNIPED, DEAD )</td></tr><tr><td align="left" valign="middle">SERVER_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">server type: the value in ( DEDICATED, SHARED )</td></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client process identifier</td></tr><tr><td align="left" valign="middle">LOGON_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">logon time</td></tr><tr><td align="left" valign="middle">PROGRAM_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">program name</td></tr><tr><td align="left" valign="middle">CLIENT_ADDRESS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">client address ( null if DA )</td></tr><tr><td align="left" valign="middle">CLIENT_PORT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client port ( 0 if DA )</td></tr><tr><td align="left" valign="middle">FAILOVER_TYPE</td><td align="left" valign="middle">VARCHAR(13)</td><td align="left" valign="middle">indicates whether and to what extent transparent application failover (TAF) is enabled for the session ( NONE, SESSION )</td></tr><tr><td align="left" valign="middle">FAILED_OVER</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is running in failover mode and failover has occurred (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IS_AUDITED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is audited (YES) or not (NO)</td></tr></tbody></table>

<a id="4051c6ed46df4f24"></a>
### V$SESSION_AUDIT

The V$SESSION_AUDIT displays audited session information.

**Column information**

<a id="cbf4695da966a143"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">active audit policy name</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="be035ba941e8b818"></a>
### V$SESSION_CONNECT_INFO

The V$SESSION_CONNECT_INFO displays information about network connections for the current session.

**Column information**

<a id="2c4fd49e68c798dd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">SERIAL_NO</td><td align="left">NUMBER</td><td align="left">session serial number</td></tr><tr><td align="left">CLIENT_CHARSET</td><td align="left">VARCHAR(40)</td><td align="left">client character set</td></tr></tbody></table>

<a id="bfe55baaa77a2489"></a>
### V$SESSION_EVENT

The V$SESSION_EVENT displays information on waits for an event by a session.

**Column information**

<a id="f3c94c2196f50dc8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">ID of the session</td></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">MAX_WAIT</td><td align="left">NUMBER</td><td align="left">Maximum time waited for the event by the session (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="f48f0f805d5fdeaa"></a>
### V$SESSION_STAT

The V$SESSION_STAT displays session statistics.

**Column information**

<a id="14841b05dd9248ff"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="24e8a0a4664c799f"></a>
### V$SESSION_MEM_STAT

The V$SESSION_MEM_STAT displays session memory statistics.

**Column information**

<a id="1a90f61414663d6d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="a90c6f7498e1c41f"></a>
### V$SESSION_MEM_USAGE

The V$SESSION_MEM_USAGE displays session memory usage for each session.

**Column information**

<a id="2bb9578c22fca86d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">ALLOCATOR_ID</td><td align="left">NUMBER</td><td align="left">memory allocator identifier</td></tr><tr><td align="left">ALLOCATOR_TYPE</td><td align="left">VARCHAR(7)</td><td align="left">memory allocator type ( REGION or DYNAMIC )</td></tr><tr><td>MEMORY_TYPE</td><td>VARCHAR(4)</td><td>memory type ( HEAP, SHM )</td></tr><tr><td>TOTAL_SIZE</td><td>NUMBER</td><td>total memory size</td></tr></tbody></table>

<a id="09966f39a26ce1ec"></a>
### V$SESSION_SQL_STAT

The V$SESSION_SQL_STAT displays session SQL statistics.

**Column information**

<a id="1623f0b5dce014be"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="61f255d78318f2f4"></a>
### V$SESSION_WAIT

The V$SESSION_WAIT displays the current or last wait for each session.

**Column information**

<a id="a305059f9a450698"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID of the session</td></tr><tr><td align="left" valign="middle">SEQ_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Identifier of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Name of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">A number that uniquely identifies the current or last wait (incremented for each wait)</td></tr><tr><td align="left" valign="middle">P1TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the first parameter for the wait event</td></tr><tr><td align="left" valign="middle">P1</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">First wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P1HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">First wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P2TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the second parameter for the wait event</td></tr><tr><td align="left" valign="middle">P2</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Second wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P2HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Second wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P3TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the third parameter for the wait event</td></tr><tr><td align="left" valign="middle">P3</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Third wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P3HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Third wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">STATE</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Wait state</td></tr><tr><td align="left" valign="middle">WAIT_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the session is currently waiting, then the value is time waited for the current wait. If the session is not in a wait, then the value is the duration of the last wait (in microseconds)</td></tr><tr><td align="left">TIME_SINCE_LAST_WAIT</td><td align="left">NUMBER</td><td align="left">Time elapsed since the end of the last wait (in microseconds). If the session is currently in a wait, then the value is 0.</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="e70708d78cfb602b"></a>
### V$SHARED_MODE

The V$SHARED_MODE displays information of shared mode.

**Column information**

<a id="9e1bfe5f03d1af43"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">name</td></tr><tr><td align="left">VALUE</td><td align="left">VARCHAR(128)</td><td align="left">value</td></tr></tbody></table>

<a id="ea304a978e40da35"></a>
### V$SHARED_SERVER

The V$SHARED_SERVER displays information of shared servers.

**Column information**

<a id="74c287090dd00a86"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">shared server process identifier</td></tr><tr><td align="left">PROCESSED_JOB_COUNT</td><td align="left">NUMBER</td><td align="left">processed job count</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(128)</td><td align="left">status</td></tr><tr><td align="left">IDLE</td><td align="left">NUMBER</td><td align="left">total idle time (1/100 second)</td></tr><tr><td align="left">BUSY</td><td align="left">NUMBER</td><td align="left">total busy time (1/100 second)</td></tr></tbody></table>

<a id="5d946c8df54b9074"></a>
### V$SHM_SEGMENT

The V$SHM_SEGMENT displays a list of all shared memory segments.

**Column information**

<a id="582b4cc4dbf59da0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SHM_NAME</td><td align="left">VARCHAR(32)</td><td align="left">shared memory segment name</td></tr><tr><td align="left">SHM_ID</td><td align="left">NUMBER</td><td align="left">shared memory segment identifier</td></tr><tr><td align="left">SHM_SIZE</td><td align="left">NUMBER</td><td align="left">shared memory segment size ( in bytes )</td></tr><tr><td align="left">SHM_KEY</td><td align="left">NUMBER</td><td align="left">shared memory segment key</td></tr><tr><td align="left">SHM_SEQ</td><td align="left">NUMBER</td><td align="left">shared memory segment sequence</td></tr><tr><td align="left">SHM_ADDR</td><td align="left">VARCHAR(32)</td><td align="left">start address of the shared memory segment</td></tr><tr><td>LARGE_PAGES</td><td>BOOLEAN</td><td>indicates whether the shared memory segment use large pages</td></tr></tbody></table>

<a id="4227ee95f859e378"></a>
### V$SPROPERTY

The V$SPROPERTY displays a list of Properties. This is store a binary property file.

**Column information**

<a id="f4c11d2153a0371e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value stored in the binary property file</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value is BINARY_FILE</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the system</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr></tbody></table>

<a id="e2e489f949f8a0cb"></a>
### V$SQLFN_METADATA

The V$SQLFN_METADATA contains metadata about operators and built-in functions

**Column information**

<a id="10fc3eb052ca68d1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FUNC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the built-in function</td></tr><tr><td align="left" valign="middle">MINARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum number of arguments for the function</td></tr><tr><td align="left" valign="middle">MAXARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum number of arguments for the function</td></tr><tr><td align="left" valign="middle">IS_AGGREGATE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the function is an aggregate function (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="1c66f69bff4c2fb0"></a>
### V$SQL_CACHE

The V$SQL_CACHE lists statistics of shared SQL plan.

**Column information**

<a id="a9205e703ea31280"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SQL_HANDLE</td><td align="left">NUMBER</td><td align="left">SQL handle</td></tr><tr><td align="left">HASH_VALUE</td><td align="left">NUMBER</td><td align="left">hash value of the SQL statement</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">count of prepared statements referencing the statement</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">CLOCK_ID</td><td align="left">NUMBER</td><td align="left">clock identifier</td></tr><tr><td align="left">PLAN_AGE</td><td align="left">NUMBER</td><td align="left">plan age</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">user name</td></tr><tr><td align="left">BIND_PARAM_COUNT</td><td align="left">NUMBER</td><td align="left">count of bind parameters</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">SQL full text</td></tr><tr><td align="left">PLAN_COUNT</td><td align="left">NUMBER</td><td align="left">physical plan count of the SQL statement</td></tr><tr><td align="left">PLAN_ID</td><td align="left">NUMBER</td><td align="left">plan identifier</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">PLAN_IS_ATOMIC</td><td align="left">BOOLEAN</td><td align="left">plan is atomic array insert or not</td></tr><tr><td align="left">PLAN_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">plan text for SQL statement</td></tr></tbody></table>

<a id="cf58585cd193795c"></a>
### V$SQL_COMMAND

The V$SQL_COMMAND lists attribute information of each SQL command.

**Column information**

<a id="f0c1b491bebd9adf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">COMMAND</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">SQL command</td></tr><tr><td align="left" valign="middle">FROM_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable from start-up phase</td></tr><tr><td align="left" valign="middle">UNTIL_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable until start-up phase</td></tr><tr><td align="left" valign="middle">ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database access mode: values in (NONE, READ &amp; WRITE, READ, READ &amp; LOCK)</td></tr><tr><td align="left" valign="middle">NEED_FETCH</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the command is a query which has result set and need fetch</td></tr><tr><td align="left" valign="middle">IS_DDL</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is a DDL(Data Defintion Language) or not</td></tr><tr><td valign="middle">CLUSTER_LOCK_MODE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">cluster lock mode: values in (NONE, SERIAL, MANUAL)</td></tr><tr><td align="left" valign="middle">AUTO_COMMIT</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is auto-commit or not</td></tr><tr><td align="left" valign="middle">IS_CACHEABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is plan-cacheable or not</td></tr><tr><td align="left" valign="middle">AUDIT_ACTION</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">auditiable action name for the SQL command</td></tr></tbody></table>

<a id="9b30b7f777ec3076"></a>
### V$SQL_HISTORY

The V$SQL_HISTORY displays information of SQLs.

**Column information**

<a id="655758e88007ad23"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement start time</td></tr><tr><td align="left" valign="middle">EXEC_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">execution time(us)</td></tr><tr><td align="left" valign="middle">PREPARED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is prepared ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">SUCCESS</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is success ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">CHARACTER VARYING(16)</td><td align="left" valign="middle">status of the statement: the value in<br>( RUNNING, DONE )</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">CHARACTER VARYING(1024)</td><td align="left" valign="middle">first 1024 bytes of the SQL text for the statement</td></tr></tbody></table>

<a id="585966ef9e09020b"></a>
### V$STATEMENT

The V$STATEMENT lists all statements.

**Column information**

<a id="98e355873510b911"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STMT_ID</td><td align="left">NUMBER</td><td align="left">statement identifier in a session</td></tr><tr><td align="left">STMT_VIEW_SCN</td><td align="left">NUMBER</td><td align="left">statement view scn</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">VARCHAR(1024)</td><td align="left">first 1024 bytes of the SQL text for the statement</td></tr><tr><td align="left">START_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">statement start time</td></tr><tr><td>TOTAL_EXEC_TIME</td><td>NATIVE_BIGINT</td><td>total execution time(us)</td></tr><tr><td>LAST_EXEC_TIME</td><td>NATIVE_BIGINT</td><td>last execution time(us)</td></tr><tr><td>EXECUTIONS</td><td>NATIVE_BIGINT</td><td>number of executions</td></tr></tbody></table>

<a id="57748d05ef24dc11"></a>
### V$SYSTEM_EVENT

The V$SYSTEM_EVENT displays information on total waits for an event.

**Column information**

<a id="51c59feb39065f84"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="a06528b97d70f039"></a>
### V$SYSTEM_STAT

The V$SYSTEM_STAT displays system statistics.

**Column information**

<a id="1c7e85db59811c01"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="f6b2fdecae200157"></a>
### V$SYSTEM_MEM_STAT

The V$SYSTEM_MEM_STAT displays system memory statistics.

**Column information**

<a id="27f0ab53dcead1d8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="66cf60ee82ff7ad0"></a>
### V$SYSTEM_SQL_STAT

The V$SYSTEM_SQL_STAT displays system SQL statistics.

**Column information**

<a id="9a176fc7449549ee"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="f0ea44639a18c880"></a>
### V$TABLES

The V$TABLES contains the definitions of all the performance views (views beginning with V$).

**Column information**

<a id="d5c0215409c5bd50"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">visible startup phase of the performance view</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>created time of the performance view</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>modified time of the performance view</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>comments of the performance view</td></tr></tbody></table>

<a id="5cd037d10b152ae6"></a>
### V$TABLESPACE

This view displays tablespace information.

**Column information**

<a id="4a77666a1192a520"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">TBS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier</td></tr><tr><td align="left" valign="middle">TBS_ATTR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace attribute: the value in ( device attribute (MEMORY) | temporary attribute (TEMPORARY, PERSISTENT) | usage attribute(DICT, UNDO, DATA, TEMPORARY) )</td></tr><tr><td align="left" valign="middle">IS_LOGGING</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is a logging tablespace ( YES ) or not ( NO )</td></tr><tr><td align="left" valign="middle">IS_ONLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is ONLINE ( YES ) or OFFLINE ( NO )</td></tr><tr><td align="left" valign="middle">OFFLINE_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">indicates whether the tablespace can be taken online normally ( CONSISTENT ) or not ( INCONSISTENT ). null if the tablespace is ONLINE</td></tr><tr><td align="left" valign="middle">EXTENT_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">extent size of the tablespace ( in bytes )</td></tr><tr><td align="left" valign="middle">PAGE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="c0814d8b00c32448"></a>
### V$TABLESPACE_STAT

This view displays tablespace statistical information.

**Column information**

<a id="bda50e7a47b2ff34"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TBS_NAME</td><td align="left">VARCHAR(128)</td><td align="left">tablespace name</td></tr><tr><td align="left">TBS_ID</td><td align="left">NUMBER</td><td align="left">tablespace identifier</td></tr><tr><td align="left">TOTAL_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">total extent count of the tablespace</td></tr><tr><td align="left">USED_META_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">meta extent count currently used on the tablespace</td></tr><tr><td align="left">USED_DATA_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">data extent count currently used on the tablespace</td></tr><tr><td align="left">FREE_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">free extent count of the tablespace</td></tr><tr><td align="left">EXTENT_SIZE</td><td align="left">NUMBER</td><td align="left">extent size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="3ebb20187a7497bc"></a>
### V$TRANSACTION

The V$TRANSACTION lists the active transactions in the system.

**Column information**

<a id="48043433591777c6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier ( null if the global transaction is unassociated</td></tr><tr><td align="left" valign="middle">TRANS_SLOT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction slot identifier</td></tr><tr><td align="left" valign="middle">PHYSICAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">physical transaction identifier</td></tr><tr><td align="left" valign="middle">TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction state: the value in ( ACTIVE, BLOCK, PREPARE, COMMIT, ROLLBACK, IDLE, PRECOMMIT )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the transaction is global or not</td></tr><tr><td align="left" valign="middle">TRANS_ATTRIBUTE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction attribute: the value in ( READ_ONLY, UPDATABLE, LOCKABLE, UPDATABLE | LOCKABLE )</td></tr><tr><td align="left" valign="middle">ISOLATION_LEVEL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction isolation level: the value in ( READ COMMITTED, SERIALIZABLE )</td></tr><tr><td align="left" valign="middle">TRANS_VIEW_SCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction view scn</td></tr><tr><td align="left" valign="middle">TCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction change number</td></tr><tr><td align="left" valign="middle">TRANS_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction sequence number</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">transaction start time</td></tr><tr><td valign="middle">UNDO_SEGMENT_ID</td><td valign="middle">NUMBER</td><td valign="middle">undo segment identifier</td></tr></tbody></table>

<a id="3f208b85eb34bb5e"></a>
### V$WAIT_EVENT_CLASS_NAME

The V$WAIT_EVENT_CLASS_NAME displays information about Class of wait event.

**Column information**

<a id="bfb6ffc8beabef6e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the class of the wait event</td></tr></tbody></table>

<a id="640642d06a164c65"></a>
### V$WAIT_EVENT_NAME

The V$WAIT_EVENT_NAME displays information about wait events.

**Column information**

<a id="c985ee772c9a30d5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the first parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the second parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the third parameter for the wait event</td></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="ac81102078be2a85"></a>
### V$XA_TRANSACTION

The V$XA_TRANSACTION displays information on the currently active XA transactions.

**Column information**

<a id="524d9570a197d40a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">XA_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">XA transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td valign="middle">DRIVER_TRANS_ID</td><td valign="middle">NUMBER</td><td valign="middle">driver transaction identifier</td></tr><tr><td valign="middle">DRIVER_MEMBER_POS</td><td valign="middle">NUMBER</td><td valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">XA_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the XA transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the XA transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">XA transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the XA transaction is repreparable</td></tr></tbody></table>

---

[← 8. GOLDILOCKS Database Replication](8-goldilocks-database-replication.md) · [Table of contents](../README.md) · [10. Server Property →](10-server-property.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
