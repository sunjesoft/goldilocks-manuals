<a id="b4c90cb50eb63ca2"></a>

# 9. Database Information

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/b4c90cb50eb63ca2)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 8. GOLDILOCKS Database Replication](8-goldilocks-database-replication.md) · [Table of contents](../README.md) · [10. Server Property →](10-server-property.md)

<a id="94a1f2f476df37b4"></a>
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

<a id="72dbba22c4cb0354"></a>
### Views of ALL_family

It retrieves information about objects accessible by a current user.

<a id="ed89311b9808ccc8"></a>
#### ALL_ALL_TABLES

ALL_ALL_TABLES describes the object tables and relational tables accessible to the current user.

**Column information**

<a id="25ef583c46192bf8"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="f021ceb76223943a"></a>
#### ALL_ARGUMENTS

ALL_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="9676efb1e011a146"></a>
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

<a id="44ce00c745b03014"></a>
#### ALL_CATALOG

ALL_CATALOG displays the tables, views, synonyms, and sequences accessible to the current user.

**Column information**

<a id="bedc702678b66644"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_NAME | VARCHAR(128) | Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_TYPE | VARCHAR(32) | Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |

<a id="cd31ac4e60fd16b6"></a>
#### ALL_CLUSTER_TABLES

ALL_CLUSTER_TABLES describes all cluster tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="728a0cb9d45563eb"></a>
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

<a id="ff875cc84b4130bd"></a>
#### ALL_COL_COMMENTS

ALL_COL_COMMENTS displays comments on the columns of the tables and views accessible to the current user.

**Column information**

<a id="67c2d9c6a30a4065"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| COMMENTS | VARCHAR(1024) | Comment on the column |

<a id="af1aa3deeaaf7152"></a>
#### ALL_COL_PRIVS

ALL_COL_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="15bfdb7066cf3f06"></a>
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

<a id="59071239b875f4e3"></a>
#### ALL_COL_PRIVS_MADE

ALL_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner or grantor.

**Column information**

<a id="f6a61f9ca3e89474"></a>
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

<a id="a1f2bbe2e9aa7e55"></a>
#### ALL_COL_PRIVS_RECD

ALL_COL_PRIVS_RECD describes the column object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="9957b1727a58f43e"></a>
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

<a id="dd457202f184be04"></a>
#### ALL_CONSTRAINTS

ALL_CONSTRAINTS describes constraint definitions on tables accessible to the current user.

**Column information**

<a id="06e5e23aa2b99b55"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_TYPE</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;SEARCH_CONDITION</td><td align="left" valign="middle">&nbsp;LONG VARCHAR</td><td align="left" valign="middle">&nbsp;Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">&nbsp;R_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;R_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;R_CONSTRAINT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;DELETE_RULE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">&nbsp;UPDATE_RULE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">&nbsp;STATUS</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">&nbsp;DEFERRABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">&nbsp;DEFERRED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">&nbsp;VALIDATED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">&nbsp;GENERATED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">&nbsp;BAD</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">&nbsp;RELY</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_CHANGE</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INVALID</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="33d9299c37fcff0e"></a>
#### ALL_CONS_COLUMNS

ALL_CONS_COLUMNS describes columns that are accessible to the current user and that are specified in constraints.

**Column information**

<a id="d573c867a24d8b1f"></a>
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

<a id="698dbfe9a4162d7c"></a>
#### ALL_DB_PRIVS

ALL_DB_PRIVS describes the database grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="feee6010569941c0"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="f27a5304c75f334d"></a>
#### ALL_DB_PRIVS_MADE

ALL_DB_PRIVS_MADE describes the database grants for which the current user is the grantor.

**Column information**

<a id="ed14dd0d5c899ca2"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9010332ee0411620"></a>
#### ALL_DB_PRIVS_RECD

ALL_DB_PRIVS_RECD describes the database grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="fc1edbfcf0cb9c4c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="c6479d966387745c"></a>
#### ALL_DEPENDENCIES

ALL_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column information**

<a id="8e60e536de38de81"></a>
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

<a id="373812a70198333f"></a>
#### ALL_GLOBAL_SECONDARY_INDEXES

ALL_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables accessible to the current user.

> It is available only on a cluster.

**Column information**

<a id="3ecc392d0cae3f3f"></a>
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

<a id="badafc04f36d2a87"></a>
#### ALL_GSI_PLACE

ALL_GSI_PLACE describes node placement of all global secondary indexes on the tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="23b64df9e26af768"></a>
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
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="644f64106fa6b8a3"></a>
#### ALL_INDEXES

ALL_INDEXES describes the indexes on the tables accessible to the current user.

**Column information**

<a id="a9f659c1129304d4"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="328ec427f75ad49b"></a>
#### ALL_IND_COLUMNS

ALL_IND_COLUMNS describes the columns of indexes on all tables accessible to the current user.

**Column information**

<a id="3a16be5d98675a0c"></a>
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

<a id="dd6872271227a7af"></a>
#### ALL_IND_PLACE

ALL_IND_PLACE describes node placement of the indexes on the tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="22cc5998076547ec"></a>
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
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(2) WITHOUT TIME ZONE | (deprecated) |

<a id="6abe5cc0b7c011cc"></a>
#### ALL_NONSCHEMA_COMMENTS

ALL_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces) accessible to the current user.

**Column information**

<a id="d7182612411136a3"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OBJECT_NAME | VARCHAR(128) | Name of the non-schema object |
| OBJECT_TYPE | VARCHAR(32) | Type of the non-schema object: DATABASE, AUTHORIZATION, SCHEMA, TABLESPACE |
| COMMENTS | VARCHAR(1024) | Comments of the non-schema object |

<a id="05778f3954ad7a8b"></a>
#### ALL_OBJECTS

ALL_OBJECTS describes all objects accessible to the current user.

**Column information**

<a id="aad2a773a8020d34"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the object</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the object</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the object</td></tr><tr><td align="left" valign="middle">&nbsp;SUBOBJECT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_ID</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">&nbsp;DATA_OBJECT_ID</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_TYPE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">&nbsp;CREATED</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_DDL_TIME</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">&nbsp;TIMESTAMP</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">&nbsp;STATUS</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">&nbsp;TEMPORARY</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;GENERATED</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;* reserved<br>Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;SECONDARY</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;NAMESPACE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Namespace for the object</td></tr><tr><td align="left" valign="middle">&nbsp;EDITION_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="ed10e82ebda1900e"></a>
#### ALL_PROCEDURES

ALL_PROCEDURES lists all function, procedures or package

**Column information**

<a id="ba0a7a0d028e2a56"></a>
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

<a id="d4164618ef45a531"></a>
#### ALL_PROC_PRIVS

ALL_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="176b0f5bf0ac15c8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="c7aa00fe08b0617e"></a>
#### ALL_PROC_PRIVS_MADE

ALL_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column information**

<a id="f3df8bdb3a6c72a1"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="23bcabe25a2b14a1"></a>
#### ALL_PROC_PRIVS_RECD

ALL_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="95e5c87af916ef54"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="7750e5c841ff187b"></a>
#### ALL_SCHEMAS

ALL_SCHEMAS identifies the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column information**

<a id="7d50c76e53f20ff8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| CREATED_TIME | TIMESTAMP(2) WITHOUT TIME ZONE | Created time of the schema |
| MODIFIED_TIME | TIMESTAMP(2) WITHOUT TIME ZONE | Last modified time of the schema |
| COMMENTS | VARCHAR(1024) | Comments of the schema |

<a id="b47adc6162d131ac"></a>
#### ALL_SCHEMA_PATH

ALL_SCHEMA_PATH describes the schema search order of the current user and PUBLIC, for naming resolution of unqualified SQL schema objects.

**Column information**

<a id="dbf0a0fa68f4b033"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| AUTH_NAME | VARCHAR(128) | Name of the authorization |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| SEARCH_ORDER | NUMBER | Schema search order of the authorization |

<a id="81750441f335c256"></a>
#### ALL_SCHEMA_PRIVS

ALL_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="59f6b134a6629ffe"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| PRIVILEGE | VARCHAR(32) | Privilege on the schema |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9268c9d9ae4e21dc"></a>
#### ALL_SCHEMA_PRIVS_MADE

ALL_SCHEMA_PRIVS_MADE describes the schema grants, for which the current user is the grantor.

**Column information**

<a id="f217b0e8e206b6da"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="7a209af1944e4172"></a>
#### ALL_SCHEMA_PRIVS_RECD

ALL_SCHEMA_PRIVS_RECD describes the schema grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="d409a5320dcd9a73"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="8ff79c24458228a9"></a>
#### ALL_SEQUENCES

ALL_SEQUENCES describes all sequences accessible to the current user.

**Column information**

<a id="d7ddb36fbd1e532e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Sequence name</td></tr><tr><td align="left" valign="middle">&nbsp;MIN_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;MAX_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;INCREMENT_BY</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">&nbsp;CYCLE_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;ORDER_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;CACHE_SIZE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_NUMBER</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="dc968262dd69ee2f"></a>
#### ALL_SEQ_PRIVS

ALL_SEQ_PRIVS describes the sequence grants, for which the current user is the sequence owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="5ecefd86c50c6b42"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="6536692384603282"></a>
#### ALL_SEQ_PRIVS_MADE

ALL_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner or grantor.

**Column information**

<a id="c1dc15d2e8109b2b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="aa4e09341f68a6af"></a>
#### ALL_SEQ_PRIVS_RECD

ALL_SEQ_PRIVS_RECD describes the sequence grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="0b2b2db8d52d3bdf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="8161b82714901b27"></a>
#### ALL_SHARD_KEY_COLUMNS

ALL_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="8e45565fdc32a791"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="59af137efaa7f83c"></a>
#### ALL_SOURCE

ALL_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="9f992616f1066c90"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="9d0e92c651459eaf"></a>
#### ALL_SYNONYMS

ALL_SYNONYMS describes all synonyms.

**Column information**

<a id="36645d8bafb48aa0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="03f74eb28bdfc88b"></a>
#### ALL_TABLES

ALL_TABLES describes the relational tables accessible to the current user.

**Column information**

<a id="80806b83844bbf7b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="b79b3bd27601b302"></a>
#### ALL_TAB_COLS

ALL_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="1b8c41e5b75f4824"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="a47f61b9cc096959"></a>
#### ALL_TAB_COLUMNS

ALL_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="19f5f4464a5a806a"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="d90d7c149d6a6fec"></a>
#### ALL_TAB_COMMENTS

ALL_TAB_COMMENTS displays comments on the tables and views accessible to the current user.

**Column information**

<a id="e471337932774426"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="2ec3a5ffd9d609d9"></a>
#### ALL_TAB_IDENTITY_COLS

ALL_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="4c2db5c4595c2113"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="78b2f71fa82841ea"></a>
#### ALL_TAB_PLACE

ALL_TAB_PLACE describes node placement of all cluster tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="10180dc2a8719cfb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="518fba2d1495fd31"></a>
#### ALL_TAB_SHARDS

ALL_TAB_SHARDS describes shard information of sharded tables accessible to the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="3ce7b929ebdc315d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="bf101e8211cba6a8"></a>
#### ALL_TAB_PRIVS

ALL_TAB_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="f823c23248564b55"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="3ed04219e2f9c9b2"></a>
#### ALL_TAB_PRIVS_MADE

ALL_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner or grantor.

**Column information**

<a id="5180f0ab588a4c32"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="c7b332ff8d1630ce"></a>
#### ALL_TAB_PRIVS_RECD

ALL_TAB_PRIVS_RECD describes object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="a861d6264d8477e5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="924e1ac92c4aa58b"></a>
#### ALL_TBS_PRIVS

ALL_TBS_PRIVS describes the tablespace grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="2fc18319c0bdb26a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="7ae8273374c31003"></a>
#### ALL_TBS_PRIVS_MADE

ALL_TBS_PRIVS_MADE describes the tablespace grants for which the current user is the grantor.

**Column information**

<a id="260910846a03bbc0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2fd11e1979af8c28"></a>
#### ALL_TBS_PRIVS_RECD

ALL_TBS_PRIVS_RECD describes the tablespace grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="6bbb1a4d87bf261f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ab34bfe59dd878df"></a>
#### ALL_USERS

ALL_USERS lists all users of the database visible to the current user.

**Column information**

<a id="f096f17ab1e9e723"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">USERNAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">USER_ID</td><td align="left">NUMBER</td><td align="left">ID number of the user</td></tr><tr><td align="left">CREATED</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">User creation timestamp</td></tr></tbody></table>

<a id="65ef4295de5856aa"></a>
#### ALL_VIEWS

ALL_VIEWS describes the views accessible to the current user.

**Column information**

<a id="c496537e279f7be5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="becbc5eeef86ed4c"></a>
### Views of DBA_family

The current user has DBA privileges (ACCESS CONTROL ON DATABASE), and the user can retrieve information about all objects.

<a id="024a6996d14d0542"></a>
#### DBA_ALL_TABLES

DBA_ALL_TABLES describes all object tables and relational tables in the database.

**Column information**

<a id="640757d8d9a1ae58"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="dfad14da09baad34"></a>
#### DBA_ARGUMENTS

DBA_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="025e20edde975def"></a>
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

<a id="70a69f286ced3676"></a>
#### DBA_CATALOG

DBA_CATALOG lists all tables, views, synonyms, and sequences in the database.

**Column information**

<a id="7ffd8ce9ea22454a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="2e454976e81594fd"></a>
#### DBA_CLUSTER

DBA_CLUSTER describes all cluster members in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="c5faa30790489038"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GROUP_ID</td><td align="left">NUMBER</td><td align="left">Group identifier of the cluster member</td></tr><tr><td align="left">GROUP_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Group name of the cluster member</td></tr><tr><td align="left">MEMBER_ID</td><td align="left">NUMBER</td><td align="left">Member identifier of the cluster member</td></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Member name of the cluster member</td></tr><tr><td align="left">MEMBER_HOST</td><td align="left">VARCHAR(128)</td><td align="left">Host address of the cluster member</td></tr><tr><td align="left">MEMBER_PORT</td><td align="left">NUMBER</td><td align="left">Port number of the cluster member</td></tr></tbody></table>

<a id="78c5e9414da63f44"></a>
#### DBA_CLUSTER_COMMENTS

DBA_CLUSTER_COMMENTS displays comments on the cluster objects in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="bf220dacce043bce"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the cluster object</td></tr><tr><td align="left">OBJECT_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the cluster object: CLUSTER GROUP, CLUSTER MEMBER</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the cluster object</td></tr></tbody></table>

<a id="40ce105393159659"></a>
#### DBA_CLUSTER_TABLES

DBA_CLUSTER_TABLES describes all cluster tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="3b861ac0c3715a06"></a>
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

<a id="96160632f22e34fd"></a>
#### DBA_COL_COMMENTS

DBA_COL_COMMENTS displays comments on the columns of all tables and views in the database.

**Column information**

<a id="67fbc366f5178451"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="b0eb59ddd834019b"></a>
#### DBA_COL_PRIVS

DBA_COL_PRIVS describes all column object grants in the database.

**Column information**

<a id="a8e968f38214e465"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">CHARACTER VARYING(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">CHARACTER VARYING(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2813ee3808d1bed7"></a>
#### DBA_CONSTRAINTS

DBA_CONSTRAINTS describes all constraint definitions on all tables in the database.

**Column information**

<a id="c36a8631ee4deb36"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="c27f01225ebf2675"></a>
#### DBA_CONS_COLUMNS

DBA_CONS_COLUMNS describes all columns in the database that are specified in constraints.

**Column information**

<a id="08b83e095e4eaa78"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="936e4ebbfcedad74"></a>
#### DBA_DB_PRIVS

DBA_DB_PRIVS describes all database grants in the database.

**Column information**

<a id="7bcba642dd41348b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the database</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="c84483b78bf2e042"></a>
#### DBA_DEPENDENCIES

DBA_DEPENDENCIES describes all dependencies between objects in the database

**Column information**

<a id="b394d36d23848aa0"></a>
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

<a id="ee95af912d297db5"></a>
#### DBA_EXTENTS

DBA_EXTENTS describes the extents comprising the segments in all tablespaces in the database.

**Column information**

<a id="526ffa7c568ff99d"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Extent number in the segment</td></tr><tr><td align="left" valign="middle">FILE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;File identifier number of the file containing the extent</td></tr><tr><td align="left" valign="middle">BLOCK_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Starting block number of the extent</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr><tr><td align="left" valign="middle">RELATIVE_FNO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Relative file number of the first extent block</td></tr></tbody></table>

<a id="d3018ac308035142"></a>
#### DBA_GLOBAL_SECONDARY_INDEXES

DBA_GLOBAL_SECONDARY_INDEXES describes all global secondary indexes in the database.

> It is available only on a cluster.

**Column information**

<a id="4cd43e014a5ca137"></a>
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

<a id="5df5c5f1c9ca78c1"></a>
#### DBA_GSI_PLACE

DBA_GSI_PLACE describes node placement of all global secondary indexes in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="f647224c577a030c"></a>
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
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="aa344dd46980f172"></a>
#### DBA_INDEXES

DBA_INDEXES describes all indexes in the database.

**Column information**

<a id="291299743efeccb1"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="c7a23c19966275b3"></a>
#### DBA_IND_COLUMNS

DBA_IND_COLUMNS describes the columns of all the indexes on all tables and clusters in the database.

**Column information**

<a id="2707ca3ca72814ec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="5dd866522bcfa25c"></a>
#### DBA_IND_PLACE

DBA_IND_PLACE describes node placement of all indexes in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="13844a313837488e"></a>
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
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(2) WITHOUT TIME ZONE | (deprecated) |

<a id="034b7bfbaf20758c"></a>
#### DBA_NONSCHEMA_COMMENTS

DBA_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces).

**Column information**

<a id="707e5cd45ea80770"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the non-schema object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the non-schema object: DATABASE, PROFILE, AUTHORIZATION, SCHEMA, TABLESPACE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the non-schema object</td></tr></tbody></table>

<a id="404da49a00fd3122"></a>
#### DBA_OBJECTS

DBA_OBJECTS describes all objects in the database.

**Column information**

<a id="b3a497a882b5b554"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="72d173b87eecab16"></a>
#### DBA_PROCEDURES

DBA_PROCEDURES lists all function, procedures or package

**Column information**

<a id="040f7b65c43fee3c"></a>
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

<a id="dfb992d6994703fc"></a>
#### DBA_PROC_PRIVS

DBA_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="ba2ad2dd02d93ac8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="f2ea4eb44db12518"></a>
#### DBA_PROFILES

DBA_PROFILES displays all profiles and their limits.

**Column information**

<a id="15ccb78d86c8e4eb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROFILE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Profile name</td></tr><tr><td align="left" valign="middle">RESOURCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Resource name</td></tr><tr><td align="left" valign="middle">RESOURCE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the resource profile is a KERNEL or a PASSWORD parameter</td></tr><tr><td align="left" valign="middle">LIMIT_VALUE</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Limit placed on this resource for this profile</td></tr><tr><td align="left" valign="middle">COMMON</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether a given profile is common. (YES or NO)</td></tr></tbody></table>

<a id="aa28f4431879331b"></a>
#### DBA_SCHEMAS

Identify the schemata in the database.

**Column information**

<a id="e8b8f3f1756e39bd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="c304d4fbce6f788c"></a>
#### DBA_SCHEMA_PATH

DBA_SCHEMA_PATH describes the schema search order of all authorizations in the database.

**Column information**

<a id="b5d65eceac77f953"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the authorization</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the authorization</td></tr></tbody></table>

<a id="7e434df5a629551d"></a>
#### DBA_SCHEMA_PRIVS

DBA_SCHEMA_PRIVS describes all schema grants in the database.

**Column information**

<a id="e2dba5650a9edc52"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="7d5d825a5ff82dd8"></a>
#### DBA_SEQUENCES

DBA_SEQUENCES describes all sequences in the database.

**Column information**

<a id="96c77176eb63983d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="f01562dd89b9fd83"></a>
#### DBA_SEQ_PRIVS

DBA_SEQ_PRIVS describes all sequence grants in the database.

**Column information**

<a id="1abf56336c8b9262"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2541d6d65297a925"></a>
#### DBA_SHARD_KEY_COLUMNS

DBA_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="95b7870e6eeb8a72"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="56feae76236fb5e6"></a>
#### DBA_SOURCE

DBA_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="b023140d64b5709f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="fa75433c51e5a207"></a>
#### DBA_STAT_SYSTEM

DBA_STAT_SYSTEM describes analyzed system statistics.

**Column information**

<a id="2744786f4a07234c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CPU_OPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">OPS(operations per second) of CPU</td></tr><tr><td align="left" valign="middle">NETWORK_IOPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">IOPS(I/O operations per second) of Cluster NETWORK</td></tr><tr><td align="left" valign="middle">NETWORK_BUFSIZE</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">buffer size of Cluster NETWORK when analyzed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="d5e7d9b245b3de12"></a>
#### DBA_SYS_PRIVS

DBA_SYS_PRIVS describes all system (database, tablespace, schema) privileges in the database.

**Column information**

<a id="c9173f5c5b54c271"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the grantee</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="86321943d12c8cc4"></a>
#### DBA_SYNONYMS

DBA_SYNONYMS describes all synonyms in the database.

**Column information**

<a id="fc477fe9ae6b91ac"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="49a961e05ff0afa3"></a>
#### DBA_TABLES

DBA_TABLES describes all relational tables in the database.

**Column information**

<a id="d60d8a6ff77ab945"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="2378b643c2d5455a"></a>
#### DBA_TABLESPACES

DBA_TABLESPACES describes all tablespaces in the database.

**Column information**

<a id="ed6f8dd859b5c659"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">PLUGGED_IN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is plugged in (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="be0beb4f58ecf137"></a>
#### DBA_TAB_COLS

DBA_TAB_COLS describes the columns (including hidden columns) of all tables, views, and clusters in the database.

**Column information**

<a id="aef14d4c67ecee7c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="a6779bb6bff10c37"></a>
#### DBA_TAB_COLUMNS

DBA_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column information**

<a id="c0975d3f03a31eb0"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="a16cb4999a19ec18"></a>
#### DBA_TAB_COMMENTS

DBA_TAB_COMMENTS displays comments on all tables and views in the database.

**Column information**

<a id="f9ae9093b68242b1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="1d0d29dac5e7296b"></a>
#### DBA_TAB_IDENTITY_COLS

DBA_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="2cf643a2133e119a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="center" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="center" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="center" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="7855bcef4ccdd77b"></a>
#### DBA_TAB_PLACE

DBA_TAB_PLACE describes node placement of all cluster tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="974f441d0d3d4b53"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="4a905ed95a27997e"></a>
#### DBA_TAB_PRIVS

DBA_TAB_PRIVS describes all object grants in the database.

**Column information**

<a id="bee9dcd303c46e37"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2216f21a11bad5d7"></a>
#### DBA_TAB_SHARDS

DBA_TAB_SHARDS describes shard information of all sharded tables in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="41f06d301d721964"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="e2c5a1add10aaba8"></a>
#### DBA_TBS_PRIVS

DBA_TBS_PRIVS describes all tablespace grants in the database.

**Column information**

<a id="7a95ec9f85e4c0da"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="bbdf5a61170fa6d2"></a>
#### DBA_USERS

DBA_USERS describes all users of the database.

**Column information**

<a id="bd2f47e7628e375d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">PASSWORD</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">encrypted password</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">FAILED_LOGIN_ATTEMPTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Consecutive failed login attempts count</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">PROFIL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">User resource profile name</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr><tr><td align="left" valign="middle">PASSWORD_VERSIONS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Shows the list of versions of the password hashes (verifiers).</td></tr><tr><td align="left" valign="middle">EDITIONS_ENABLED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether editions have been enabled for the corresponding user (Y) or not (N).</td></tr><tr><td align="left" valign="middle">AUTHENTICATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the authentication mechanism for the user.</td></tr></tbody></table>

<a id="aa3ae01dfc4b9bb9"></a>
#### DBA_VIEWS

DBA_VIEWS describes all views in the database.

**Column information**

<a id="bb7c75c1b037d2ab"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="69e83744acff1ef5"></a>
### Views of USER_family

It retrieves information about objects which are owned by current user.

<a id="2584269a20968044"></a>
#### USER_ALL_TABLES

USER_ALL_TABLES describes the object tables and relational tables owned by the current user.

**Column information**

<a id="3d0a733d8b3b7b48"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="403c26cfa34f3eb1"></a>
#### USER_ARGUMENTS

USER_ARGUMENTS lists all arguments of functions, procedures.

**Column information**

<a id="b573d1b69461a719"></a>
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

<a id="31cb830d51a239f4"></a>
#### USER_CATALOG

USER_CATALOG lists tables, views, synonyms, and sequences owned by the current user.

**Column information**

<a id="678293da96095d56"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="4dd4bd8aa8a5d496"></a>
#### USER_COL_COMMENTS

USER_COL_COMMENTS displays comments on the columns of the tables and views owned by the current user.

**Column information**

<a id="7c4a951cabc85045"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="4a22c4894367c71a"></a>
#### USER_CLUSTER_TABLES

USER_CLUSTER_TABLES describes all cluster tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="a1eac00822acab4a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| SHARD_STRATEGY | VARCHAR(32) | Sharding strategy of the table:  the value in (CLONED, HASH SHARDING, RANGE SHARDING, LIST SHARDING) |
| SHARD_PLACEMENT | VARCHAR(32) | Shard placement of the table:  the value in (AT CLUSTER WIDE or AT CLUSTER GROUP) |
| SHARD_COUNT | NUMBER | Shard count of the table (if cloned table, the value is null) |
| SHARD_KEY_COUNT | NUMBER | Shard key column count of the table (if cloned table, the value is null) |
| HAS_GSI | VARCHAR(3) | Indicate whether the table has global secondary index: (YES) or (NO) |

<a id="a97a3094ad724b75"></a>
#### USER_COL_PRIVS

USER_COL_PRIVS describes the column object grants for which the current user is the object owner, grantor, or grantee.

**Column information**

<a id="7d5d191ce767ccd7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="26f00d2e47cc2b74"></a>
#### USER_COL_PRIVS_MADE

USER_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner.

**Column information**

<a id="8a1a0056e301b972"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="dc2b331c8f034c95"></a>
#### USER_COL_PRIVS_RECD

USER_COL_PRIVS_RECD describes the column object grants for which the current user is the grantee.

**Column information**

<a id="25a104542dbcba7e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ef31f6775105ad0e"></a>
#### USER_CONSTRAINTS

USER_CONSTRAINTS describes all constraint definitions on tables owned by the current user.

**Column information**

<a id="d34ffc3152f5de95"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="7fbe8636a6760dbb"></a>
#### USER_CONS_COLUMNS

USER_CONS_COLUMNS describes columns that are owned by the current user and that are specified in constraint definitions.

**Column information**

<a id="26bb3da316355b39"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="c2075175067ada4d"></a>
#### USER_DEPENDENCIES

USER_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column information**

<a id="719e726c43507dcd"></a>
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

<a id="744d0d1709f3e78a"></a>
#### USER_EXTENTS

USER_EXTENTS describes the extents comprising the segments owned by the current user's objects.

**Column information**

<a id="67a17dbfa63dbf30"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Extent number in the segment</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr></tbody></table>

<a id="d13941ce4a27e2fd"></a>
#### USER_GLOBAL_SECONDARY_INDEXES

USER_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables owned by the current user.

> It is available only on a cluster.

**Column information**

<a id="5dc0c01095b7ad6f"></a>
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

<a id="ac948a5e7ed1eb5c"></a>
#### USER_GSI_PLACE

USER_GSI_PLACE describes node placement of all global secondary indexes on the tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="a7ca73dd7ca672d3"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the global secondary indexed object |
| TABLE_NAME | VARCHAR(128) | Name of the global secondary indexed object |
| GROUP_ID | NUMBER | Group identifier of the node where the global secondary index placed |
| GROUP_NAME | VARCHAR(128) | Group name of the node where the global secondary index placed |
| MEMBER_ID | NUMBER | Member identifier of the node where the global secondary index placed |
| MEMBER_NAME | VARCHAR(128) | Member name of the node where the global secondary index placed |
| MEMBER_OFFLINE | BOOLEAN | data of the cluster member is offline or not |
| BLOCKS | NUMBER | Number of used blocks of the node where the global secondary index placed |

<a id="b32c1acad70361b2"></a>
#### USER_INDEXES

USER_INDEXES describes indexes owned by the current user.

**Column information**

<a id="71be3a0c8fd2eca4"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">ndicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left">BLOCKS</td><td align="left">NUMBER</td><td align="left">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="b6cecc4ebe878654"></a>
#### USER_IND_COLUMNS

USER_IND_COLUMNS describes the columns of the indexes owned by the current user and columns of indexes on tables owned by the current user.

**Column information**

<a id="648af416ed96bb53"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="c273e8f22a65e178"></a>
#### USER_IND_PLACE

USER_IND_PLACE describes node placement of the indexes owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="87ab52174d5d60ea"></a>
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
| DISTINCT_KEYS | NUMBER | (deprecated) |
| SAMPLE_SIZE | NUMBER | (deprecated) |
| BLOCKS | NUMBER | Number of used blocks of the node where the index placed |
| LAST_ANALYZED | TIMESTAMP(2) WITHOUT TIME ZONE | (deprecated) |

<a id="2ac4de9dd8089ae5"></a>
#### USER_OBJECTS

USER_OBJECTS describes all objects owned by the current user.

**Column information**

<a id="30612d0026323bd5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="bf328f90f712cdff"></a>
#### USER_PROCEDURES

USER_PROCEDURES lists of procedures owned by the current user.

**Column information**

<a id="a6530a14db1c6908"></a>
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

<a id="155401cd0c1ad68f"></a>
#### USER_PROC_PRIVS

USER_PROC_PRIVS describes the procedure grants for which the current user is the procedure owner, grantor, or grantee.

**Column information**

<a id="0e9da1f867f38efa"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="764f8d575c3c167c"></a>
#### USER_PROC_PRIVS_MADE

USER_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column information**

<a id="07f5cee36cf5bc6c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9b1a825217c0072b"></a>
#### USER_PROC_PRIVS_RECD

USER_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column information**

<a id="66325013cde3507c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="4b736a03542cdd81"></a>
#### USER_SCHEMAS

USER_SCHEMAS identifies the schemata in a catalog that are owned by current user.

**Column information**

<a id="fd257375fac66b10"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="ca8cfc6df41892db"></a>
#### USER_SCHEMA_PATH

USER_SCHEMA_PATH describes the schema search order of the current user, for naming resolution of unqualified SQL schema objects.

**Column information**

<a id="f67ed243a63d67fb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the user</td></tr></tbody></table>

<a id="9cf4e427e410ccf7"></a>
#### USER_SCHEMA_PRIVS

USER_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee.

**Column information**

<a id="9235aaff11994131"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a656373b8a1f9a52"></a>
#### USER_SCHEMA_PRIVS_MADE

USER_SCHEMA_PRIVS_MADE describes the schema grants for which the current user is the schema owner.

**Column information**

<a id="fce35693f8ff6ba8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="c6daff905040c2ff"></a>
#### USER_SCHEMA_PRIVS_RECD

USER_SCHEMA_PRIVS_RECD describes the schema grants for which the current user is the grantee.

**Column information**

<a id="f07f589845763cf1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f1eb8d48c1554cdc"></a>
#### USER_SEQUENCES

USER_SEQUENCES describes all sequences owned by the current user.

**Column information**

<a id="eab29dd5e2bc9a5d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="2a7e65819955f2d7"></a>
#### USER_SEQ_PRIVS

USER_SEQ_PRIVS describes the sequence grants for which the current user is the sequence owner, grantor, or grantee.

**Column information**

<a id="da77dfe64edaa330"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="7fe949acaecb1cbf"></a>
#### USER_SEQ_PRIVS_MADE

USER_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner.

**Column information**

<a id="388ebb5178c39c44"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="fa394543418a8513"></a>
#### USER_SEQ_PRIVS_RECD

USER_SEQ_PRIVS_RECD describes the sequence grants for which the current user is the grantee.

**Column information**

<a id="dd3964eb60569ea6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="698e229fd0ca9e86"></a>
#### USER_SHARD_KEY_COLUMNS

USER_SHARD_KEY_COLUMNS describes shard key columns of shareded tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="d464cb787844687f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="27f76ee2063a9406"></a>
#### USER_SOURCE

USER_SOURCE describes the text source of the stored objects accessible to the current user.

**Column information**

<a id="714dcb22949d4a0f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="65e409423a991359"></a>
#### USER_SYNONYMS

USER_SYNONYMS describes all synonyms owned by the current user.

**Column information**

<a id="5b699d43a9474664"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="ff6d11e20625162d"></a>
#### USER_SYS_PRIVS

USER_SYS_PRIVS describes system (database, tablespace, schema) privileges granted to the current user or PUBLIC.

**Column information**

<a id="0ca106d990e5a2c0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user, or PUBLIC</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="fd802f6b3a795fa6"></a>
#### USER_TABLES

USER_TABLES describes the relational tables owned by the current user.

**Column information**

<a id="69bca4898cf028be"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="6870767566816192"></a>
#### USER_TABLESPACES

USER_TABLESPACES describes the tablespaces accessible to the current user.

**Column information**

<a id="06b6a08696147d71"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="281c2ffe620f8696"></a>
#### USER_TAB_COLS

USER_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters owned by the current user.

**Column information**

<a id="167bb74935d4d33c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="3865788061a47f37"></a>
#### USER_TAB_COLUMNS

USER_TAB_COLUMNS describes the columns of the tables, views, and clusters owned by the current user.

**Column information**

<a id="93f4066f956883cc"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="349c2845adf5e0f8"></a>
#### USER_TAB_COMMENTS

USER_TAB_COMMENTS displays comments on the tables and views owned by the current user.

**Column information**

<a id="c432e66ac207432e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="b6cd4ad2b087d8e3"></a>
#### USER_TAB_IDENTITY_COLS

USER_TAB_IDENTITY_COLS describes all table identity columns.

**Column information**

<a id="8e681b6c16f94221"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="117d945fca2fdc74"></a>
#### USER_TAB_PLACE

USER_TAB_PLACE describes node placement of cluster tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="5bbe09b60032cf86"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="7d2a3a1a7d53af09"></a>
#### USER_TAB_PRIVS

USER_TAB_PRIVS describes the object grants for which the current user is the object owner, grantor, or grantee.

**Column information**

<a id="9fd34ae0903d81a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="3b143fbbc2bcf453"></a>
#### USER_TAB_PRIVS_MADE

USER_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner.

**Column information**

<a id="93fc680d700bfd09"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="219318494a428013"></a>
#### USER_TAB_PRIVS_RECD

USER_TAB_PRIVS_RECD describes the object grants for which the current user is the grantee.

**Column information**

<a id="eb444ae5fd3de013"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="0ce67f24a6acdcfb"></a>
#### USER_TAB_SHARDS

USER_TAB_SHARDS describes shard information of sharded tables owned by the current user in the cluster system.

> It is available only on a cluster.

**Column information**

<a id="8cf26733dcf0a209"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="3e1b8d302a735ca3"></a>
#### USER_USERS

USER_USERS describes the current user.

**Column information**

<a id="cf0e4965e1f7eb03"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr></tbody></table>

<a id="735ee47f50fed522"></a>
#### USER_VIEWS

USER_VIEWS describes the views owned by the current user.

**Column information**

<a id="6988281cfc8bddad"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="7ebdd3c2d6fcc6e7"></a>
### Other Views

There are other views or tables which are none of All-family, DBA-family or USER-family.

<a id="ead3d16d2bd20d7e"></a>
#### AUDIT_POLICIES

AUDIT_POLICIES contains one row for each audit policy.

**Column information**

<a id="23c936ba5f819ae3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enabled (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the audit policy</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the audit policy</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the audit policy</td></tr></tbody></table>

<a id="d838aa0749749ad8"></a>
#### AUDIT_POLICY_OPTIONS

AUDIT_POLICY_OPTIONS describes all audit policies created in the database.

**Column information**

<a id="8b002c47a06823a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">auditing option defined in the audit policy</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">The values of AUDIT_OPTION_TYPE_NAME in ( 'DATABASE PRIVILEGE', 'SYSTEM ACTION', 'OBJECT ACTION' )</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">object type name, for an object-specific auditing option</td></tr></tbody></table>

<a id="a5e3ef0be7883956"></a>
#### AUDIT_POLICY_ENABLED

AUDIT_POLICY_ENABLE describes all the audit policies that are enable in the database.

**Column information**

<a id="92221dd2b7df826e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED_OPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">enable option of the audit policy, the possible values are BY, EXCEPT</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name for whom the audit policy is enable</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="e4782a986661d5a6"></a>
#### AUDIT_TRAIL

AUDIT_TRAIL displays audit records from the audit trail.

**Column information**

<a id="38bab7d9fbac1fa3"></a>
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
| EVENT_TIMESTAMP | TIMESTAMP(2) WITHOUT TIME ZONE | timestamp of the creation of the audit trail entry in local time zone |
| POLICY_NAME | VARCHAR(128) | audit policy name that caused the current audit record |
| PRIVILEGE_USED | VARCHAR(32) | database privilege used to execute the action |
| ACTION_NAME | VARCHAR(32) | action name executed by the user |
| OBJECT_TYPE | VARCHAR(32) | object type of object affected by the action |
| OBJECT_SCHEMA | VARCHAR(128) | schema name of object affected by the action |
| OBJECT_NAME | VARCHAR(128) | object name of object affected by the action |

<a id="43f77833e04fbd88"></a>
#### DATABASE_PROPERTIES

DATABASE_PROPERTIES lists permanent database properties.

**Column information**

<a id="fcb7495d7e4965de"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;PROPERTY_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Property name</td></tr><tr><td align="left">&nbsp;PROPERTY_VALUE</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property value</td></tr><tr><td align="left">&nbsp;DESCRIPTION</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property description</td></tr></tbody></table>

<a id="5cdfbc27266fc923"></a>
#### DBC_TABLE_TYPE_INFO

Identify the ODBC/JDBC table types available in this database.

**Column information**

<a id="00b5ac386e173437"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE_ID</td><td align="left">&nbsp;NUMBER</td><td align="left">&nbsp;number identifier of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;name of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;IS_SUPPORTED</td><td align="left">&nbsp;BOOLEAN</td><td align="left">&nbsp;is supported feature</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;comments of the table type</td></tr></tbody></table>

<a id="05655342ad1cf5c9"></a>
#### DICTIONARY

DICTIONARY contains descriptions of data dictionary tables and views.

**Column information**

<a id="3cd674970dd422a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;TABLE_SCHEMA</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Schema of the object</td></tr><tr><td align="left">&nbsp;TABLE_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Name of the object</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;Text comment on the object</td></tr></tbody></table>

<a id="fc5be8d1abb44b1e"></a>
#### DICT_COLUMNS

DICT_COLUMNS contains descriptions of columns in data dictionary tables and views.

**Column information**

<a id="77f09cadafcc2e70"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object that contains the column</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object that contains the column</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Text comment on the column</td></tr></tbody></table>

<a id="8ae6488828d29440"></a>
#### IMPLEMENTATION_INFO

IMPLEMENTATION_INFO contains information about various aspects that are left implementation-defined.

**Column information**

<a id="d627885037c5bd85"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">identifier of the implementation item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="be5d24d9818fd6ed"></a>
#### IMPLEMENTATION_INFO_BASE

The IMPLEMENTATION_INFO_BASE table has one row for each implementation information item.

**Column information**

<a id="5ef21b22093afeb5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if the implementation item is supported, FALSE if not</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="c3fc2038b257a6fb"></a>
#### JDBC_CLIENT_PROPS

JDBC_CLIENT_PROPS is the set of jdbc client properties.

**Column information**

<a id="8b8056d78d99fcd4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">property name</td></tr><tr><td align="left">MAX_LEN</td><td align="left">NATIVE_INTEGER</td><td align="left">max length of a value</td></tr><tr><td align="left">DEFAULT_VALUE</td><td align="left">VARCHAR(128)</td><td align="left">default value</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(256)</td><td align="left">descrption on that property</td></tr></tbody></table>

<a id="3ea8ed9c760277bd"></a>
#### PRODUCT

PRODUCT is about the product name, version for ODBC, JDBC interface.

**Column information**

<a id="2b9d02abb6858bd3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(32)</td><td align="left">the product name</td></tr><tr><td align="left">VERSION</td><td align="left">VARCHAR(128)</td><td align="left">product full version information</td></tr><tr><td align="left">PRODUCT_VERSION</td><td align="left">NUMBER</td><td align="left">product version</td></tr><tr><td align="left">MAJOR_VERSION</td><td align="left">NUMBER</td><td align="left">major version</td></tr><tr><td align="left">MINOR_VERSION</td><td align="left">NUMBER</td><td align="left">minor version</td></tr><tr><td align="left">PATCH_VERSION</td><td align="left">NUMBER</td><td align="left">patch version</td></tr></tbody></table>

<a id="cf80c126a42e1c51"></a>
#### SESSION_PRIVS

SESSION_PRIVS describes the privileges that are currently available to the user.

**Column information**

<a id="d081f9699bd53701"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE</td><td align="left">VARCHAR(256)</td><td align="left">Name of the privilege</td></tr></tbody></table>

<a id="f30e73df10f8de6a"></a>
#### SUPPLEMENTAL_LOG_TABLE_INFO

SUPPLEMENTAL_LOG_TABLE_INFO describes table-level supplemental logging status.

**Column information**

<a id="eaf1fd8f0eb62d58"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUPPLEMENTAL_LOG_DATA_PK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of table-level PRIMARY KEY COLUMNS supplemental logging: IMPLICIT, EXPLICIT, NO</td></tr></tbody></table>

<a id="7b30fb8527644609"></a>
### Aliased Synonym

It is the public synonym which indicates the view or table in DICTIONARY_SCHEMA.

<a id="f32597e3e7042326"></a>
#### COLS

COLS is a public synonym for USER_TAB_COLUMNS.

<a id="ad967db8801d6ec9"></a>
#### DICT

DICT is a public synonym for DICTIONARY.

<a id="4b48b2a58ab8d54d"></a>
#### IND

IND is a public synonym for USER_INDEXES.

<a id="683b525136ba2ba9"></a>
#### OBJ

OBJ is a public synonym for USER_OBJECTS.

<a id="f61cf3ec9fd02659"></a>
#### SEQ

SEQ is a public synonym for USER_SEQUENCES.

<a id="dbfc90dffe6c25a9"></a>
#### TABS

TABS is a public synonym for USER_TABLES.

<a id="b8da4c669200f987"></a>
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

> Views and tables of INFORMATION_SCHEMA can be retrieved from OPEN phase.

<a id="95f49f67c0d8dcd5"></a>
### COLUMNS

Identify the columns of tables defined in this catalog that are accessible to given user or role.

**Column information**

<a id="a7a58c3278e3b96b"></a>
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

<a id="1e5cc7fb618f9b7b"></a>
### COLUMN_PRIVILEGES

Identify the privileges on columns of tables defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="48caa9c3a536f2cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted column privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the column privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( SELECT, INSERT, UPDATE, REFERENCES )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="bd8d2116a31e7345"></a>
### CONSTRAINT_COLUMN_USAGE

Identify the columns used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column information**

<a id="2512a711252d4c6a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="6c8b02ec0449d20b"></a>
### CONSTRAINT_TABLE_USAGE

Identify the tables that are used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column information**

<a id="69147a5e5ffb1784"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="e569303fab0197e1"></a>
### INFORMATION_SCHEMA_CATALOG_NAME

Identify the catalog that contains the Information Schema

**Column information**

<a id="488416ad610701ec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CATALOG_NAME</td><td align="left">VARCHAR(128)</td><td align="left">the name of catalog in which this Information Schema resides</td></tr></tbody></table>

<a id="2cebfb61d5c89150"></a>
### KEY_COLUMN_USAGE

Identify the columns defined in this catalog that are constrained as keys and that are accessible by a given user or role.

**Column information**

<a id="fcc71efe073b6558"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position of the specific column in the constraint being described. If the constraint described is a key of cardinality 1 (one), then the value of ORDINAL_POSITION is always 1 (one).</td></tr><tr><td align="left" valign="middle">POSITION_IN_UNIQUE_CONSTRAINT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the constraint being described is a foreign key constraint, then the value of POSITION_IN_UNIQUE_CONSTRAINT is the ordinal position of the referenced column corresponding to the referencing column being described, in the corresponding unique key constraint.</td></tr></tbody></table>

<a id="c167900434693573"></a>
### PARAMETERS

Identify the SQL parameters of SQL-invoked routines defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="11ee994528eed2f0"></a>
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

<a id="e3de5e19d753044c"></a>
### REFERENTIAL_CONSTRAINTS

Identify the referential constraints defined on tables in this catalog that are accessible to a given user or role.

**Column information**

<a id="17f3c596b20ece24"></a>
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

<a id="0e3e91e04690028c"></a>
### ROUTINES

Identify the SQL-invoked routines in this catalog that are accessible to a given user or role.

**Column information**

<a id="69d4a3d6be95b19d"></a>
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
| CREATED | TIMESTAMP(2) WITHOUT TIME ZONE | creation time of the routine |
| LAST_ALTERED | TIMESTAMP(2) WITHOUT TIME ZONE | most lately altered time of the routine |
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

<a id="74d114fe68da6dcd"></a>
### ROUTINE_PRIVILEGES

Identify the privileges on SQL-invoked routines defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="7500e06eecd814d0"></a>
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

<a id="d532641bccefe2c1"></a>
### ROUTINE_ROUTINE_USAGE

Identify each SQL-invoked routine owned by a given user or role on which an SQL routine defined in this catalog is dependent.

**Column information**

<a id="60fca87aa0ad9cf3"></a>
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

<a id="0255ce9b74f14b99"></a>
### ROUTINE_SEQUENCE_USAGE

Identify each external sequence generator owned by a given user or role on which some SQL routine defined in this catalog is dependent.

**Column information**

<a id="f4252ed53fa80b8e"></a>
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

<a id="6ea3201b39e35273"></a>
### ROUTINE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column information**

<a id="c90f68fa872c7968"></a>
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

<a id="e14c77607e569970"></a>
### SCHEMATA

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column information**

<a id="7fe619d344c6bf9e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CATALOG_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name</td></tr><tr><td align="left" valign="middle">SCHEMA_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the schema</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">character set name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">SQL_PATH</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">character representation of schema path specification</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the schema</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the schema</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the schema</td></tr></tbody></table>

<a id="2070bc7fbee0865b"></a>
### SEQUENCES

Identify the external sequence generators defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="7df7b48f2ee83f0c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the standard name of the data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION_RADIX</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the radix ( 2 or 10 ) of the precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric scale of the exact numerical data type</td></tr><tr><td align="left" valign="middle">START_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the start value of the sequence generator</td></tr><tr><td align="left" valign="middle">MINIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the minimum value of the sequence generator</td></tr><tr><td align="left" valign="middle">MAXIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the maximum value of the sequence generator</td></tr><tr><td align="left" valign="middle">INCREMENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the increment of the sequence generator</td></tr><tr><td align="left" valign="middle">CYCLE_OPTION</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">cycle option</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">DECLARED_DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the sequence generator</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the sequence generator</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the sequence generator</td></tr></tbody></table>

<a id="ecfce4415896e63f"></a>
### SQL_FEATURES

List the features and subfeatures of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="2fe392b99983096c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="9ecc2786db352228"></a>
### SQL_IMPLEMENTATION_INFO

List the SQL-implementation information items defined in this ISO/IEC 9075 standard and, for each of these, indicate the value supported by the SQL-implementation.

**Column information**

<a id="81e7e96c42dc0ba2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation information item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation information item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation information item</td></tr></tbody></table>

<a id="7632595a09edd746"></a>
### SQL_PACKAGES

List the packages of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="ab58aad36ba4a03f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="c84fd8134de26cc1"></a>
### SQL_PARTS

List the parts of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column information**

<a id="4bb89eae107b0412"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="ad16098d2410050a"></a>
### SQL_SIZING

List the sizing items of this ISO/IEC 9075 standard, for each of these, indicate the size supported by the SQL-implementation.

**Column information**

<a id="9d3b3db5ff52ca8a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SIZING_ID</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">identifier of the sizing item</td></tr><tr><td align="left" valign="middle">SIZING_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the sizing item</td></tr><tr><td align="left" valign="middle">SUPPORTED_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the sizing item, or 0 if the size is unlimited or cannot be determined, or null if the features for which the sizing item is applicable are not supported</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the sizing item</td></tr></tbody></table>

<a id="9b1d70fc9dba8d1e"></a>
### STATISTICS

Provide a list of statistics about a single table and the indexes associated with the table that are accessible to a given user or role.

**Column information**

<a id="c5d81730aff00257"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">STAT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">statistics type: the value in ( TABLE STAT, INDEX CLUSTERED, INDEX HASHED, INDEX OTHER )</td></tr><tr><td align="left" valign="middle">NON_UNIQUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the index does not allow duplicate values</td></tr><tr><td align="left" valign="middle">INDEX_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the index</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the index</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the index</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ordinal position of the specific column in the index described</td></tr><tr><td align="left" valign="middle">IS_ASCENDING_ORDER</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">index key column being described is sorted in ASCENDING(TRUE) or DESCENDING(FALSE) order</td></tr><tr><td align="left" valign="middle">IS_NULLS_FIRST</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">the null values of the key column are sorted before(TRUE) or after(FALSE) non-null values</td></tr><tr><td align="left" valign="middle">CARDINALITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of rows in the table; otherwise, it is the number of unique values in the index</td></tr><tr><td align="left" valign="middle">PAGES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of pages used for the table; otherwise, it is the number of pages used for the current index.</td></tr><tr><td align="left" valign="middle">FILTER_CONDITION</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">filter condition, if any.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the table comments; otherwise, it is the index comments.</td></tr></tbody></table>

<a id="7a2a0253cb65d31a"></a>
### TABLES

Identify the tables defined in this catalog that are accessible to a given user or role

**Column information**

<a id="efc3763d0d189eeb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( BASE TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM VERSIONED, FIXED TABLE, DUMP TABLE )</td></tr><tr><td align="left" valign="middle">DBC_TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">ODBC/JDBC table type: the value is in ( TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM TABLE, ALIAS, SYNONYM )</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name of the table, NULL if view</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_START_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version start column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_END_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version end column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_RETENTION_PERIOD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a system-versioned table, then the character representation of the value of the retention period of the table</td></tr><tr><td align="left" valign="middle">SELF_REFERENCING_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a typed table, then the name of the self-referencing column of the table</td></tr><tr><td align="left" valign="middle">REFERENCE_GENERATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table has a self-referencing column, the value is in ( SYSTEM GENERATED, USER GENERATED, DERIVED )</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the catalog name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the schema name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the name of the structured type</td></tr><tr><td align="left" valign="middle">IS_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable-into table</td></tr><tr><td align="left" valign="middle">IS_TYPED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a typed table</td></tr><tr><td align="left" valign="middle">COMMIT_ACTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a temporary table, the value is in ( DELETE, PRESERVE )</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the table</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the table</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the table</td></tr></tbody></table>

<a id="3f378e4a582aee05"></a>
### TABLE_CONSTRAINTS

Identify the table constraints defined on tables in this catalog that are accessible to a given user or role

**Column information**

<a id="d07c833db32021b0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( PRIMARY KEY, UNIQUE, FOREIGN KEY, NOT NULL, CHECK )</td></tr><tr><td align="left" valign="middle">IS_DEFERRABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a deferrable constraint</td></tr><tr><td align="left" valign="middle">INITIALLY_DEFERRED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an initially deferred constraint</td></tr><tr><td align="left" valign="middle">ENFORCED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an enforced constraint</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the constraint</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the constraint</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the constraint</td></tr></tbody></table>

<a id="30d422c1f3aed193"></a>
### TABLE_PRIVILEGES

Identify the privileges on tables of tables defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="e9bf8369a752c8c3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted table privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the table privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CONTROL, SELECT, INSERT, UPDATE, DELETE, REFERENCES, LOCK, INDEX, ALTER )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr><tr><td align="left" valign="middle">WITH_HIERARCHY</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the privilege was granted WITH HIERARCHY OPTION or not</td></tr></tbody></table>

<a id="4c35bef32e55abbb"></a>
### USAGE_PRIVILEGES

Identify the USAGE privileges on objects defined in this catalog that are available to or granted by a given user or role.

**Column information**

<a id="93a419312256f5aa"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted usage privileges, on the object of the type identified by OBJECT_TYPE</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization identifier of some user or role, or PUBLIC to indicate all users, to whom the usage privilege being described is granted</td></tr><tr><td align="left" valign="middle">OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( DOMAIN, CHARACTER SET, COLLATION, TRANSLATION, SEQUENCE )</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( USAGE )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="c949d877dacaff11"></a>
### VIEWS

Identify the viewed tables defined in this catalog that are accessible to a given user or role.

**Column information**

<a id="60181e215c905c7a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">the character representation of the user-specified query expression contained in the corresponding view descriptor</td></tr><tr><td align="left" valign="middle">CHECK_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CASCADED, LOCAL, NONE )</td></tr><tr><td align="left" valign="middle">IS_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an updatable view</td></tr><tr><td align="left" valign="middle">INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable view</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an update INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_DELETABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether a delete INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an insert INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_COMPILED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is compiled or not</td></tr><tr><td align="left" valign="middle">IS_AFFECTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is affected by modification of underlying object or not</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the view</td></tr></tbody></table>

<a id="c8f8aee0da8e5300"></a>
### VIEW_ROUTINE_USAGE

Identify each routine owned by a given user or role on which a view defined in this catalog is dependent.

**Column information**

<a id="d58515c92348aa36"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">SPECIFIC_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific catalog name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific owner name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific schema name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific name of a routine contained in the query expression of the view being described</td></tr></tbody></table>

<a id="93d9c18a4fca56ce"></a>
### VIEW_TABLE_USAGE

Identify the tables on which viewed tables defined in this catalog and owned by a given user or role are dependent.

**Column information**

<a id="e22310344e77a8c5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr></tbody></table>

<a id="460e2e65c6636029"></a>
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

The retrievable Information of PERFORMANCE_VIEW_SCHEMA views vary upon its phase of the startup. (nomount, mount, open)  
Execute the followings to figure out the startup phase in which each views are retrieved.

```
gSQL> select table_name, startup_phase from v$tables order by 1;

TABLE_NAME           STARTUP_PHASE
-------------------- -------------
V$AGABLE_INFO        OPEN         
V$ARCHIVELOG         MOUNT        
V$BACKUP             MOUNT        
V$BALANCER           OPEN         
V$COLUMNS            OPEN         
V$CONTROLFILE        MOUNT        
V$DATAFILE           MOUNT        
V$DB_FILE            MOUNT        
V$DISPATCHER         OPEN         
V$ERROR_CODE         NO_MOUNT     
V$INCREMENTAL_BACKUP MOUNT        
V$INSTANCE           NO_MOUNT     
V$KEYWORDS           NO_MOUNT     
V$LATCH              NO_MOUNT     
V$LOCK_WAIT          OPEN         
V$LOGFILE            MOUNT        
V$PROCESS_MEM_STAT   NO_MOUNT     
V$PROCESS_SQL_STAT   NO_MOUNT     
V$PROCESS_STAT       NO_MOUNT     
V$PROPERTY           NO_MOUNT     

TABLE_NAME             STARTUP_PHASE
---------------------- -------------
V$PSM_RESERVED_WORDS   NO_MOUNT     
V$QUEUE                OPEN         
V$RESERVED_WORDS       NO_MOUNT     
V$SESSION              NO_MOUNT     
V$SESSION_CONNECT_INFO NO_MOUNT     
V$SESSION_EVENT        OPEN         
V$SESSION_MEM_STAT     NO_MOUNT     
V$SESSION_SQL_STAT     NO_MOUNT     
V$SESSION_STAT         NO_MOUNT     
V$SESSION_WAIT         OPEN         
V$SHARED_MODE          OPEN         
V$SHARED_SERVER        OPEN         
V$SHM_SEGMENT          NO_MOUNT     
V$SPROPERTY            NO_MOUNT     
V$SQLFN_METADATA       NO_MOUNT     
V$SQL_CACHE            NO_MOUNT     
V$SQL_COMMAND          OPEN         
V$SQL_HISTORY          NO_MOUNT     
V$STATEMENT            NO_MOUNT     
V$SYSTEM_EVENT         OPEN         

TABLE_NAME              STARTUP_PHASE
----------------------- -------------
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

50 rows selected.
```

<a id="f0dae5642fd55e8e"></a>
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

<a id="c4510e141f9f963a"></a>
### V$AGABLE_INFO

The V$AGABLE_INFO displays the system agable information.

**Column information**

<a id="ce54f81e701c3f66"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCN</td><td align="left">VARCHAR(32)</td><td align="left">system scn</td></tr><tr><td align="left">AGABLE_SCN</td><td align="left">VARCHAR(32)</td><td align="left">system agable scn</td></tr><tr><td align="left">AGABLE_SCN_GAP</td><td align="left">VARCHAR(32)</td><td align="left">gap between system scn and agable scn</td></tr><tr><td align="left">OLDEST_SESSION_ID</td><td align="left">NUMBER</td><td align="left">identifier of session blocking aging</td></tr></tbody></table>

<a id="2e76f1d6333f7163"></a>
### V$ARCHIVELOG

The V$ARCHIVELOG displays information of log archiving.

**Column information**

<a id="d386906536ff4399"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ARCHIVELOG_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database log mode: the value in ( NOARCHIVELOG, ARCHIVELOG )</td></tr><tr><td align="left" valign="middle">LAST_ARCHIVED_LOG</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence number of last archived log file</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_DIR</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">archive destination path</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_FILE_PREFIX</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">file prefix name of the archived log</td></tr></tbody></table>

<a id="fb0895b2ad2050fa"></a>
### V$AUDITABLE_DB_PRIVILEGES

The V$AUDITABLE_DB_PRIVILEGES displays auditable database privileges.

**Column information**

<a id="f79cc52ecd38a8f7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE_ID</td><td align="left">NUMBER</td><td align="left">database privilege identifier</td></tr><tr><td align="left">PRIVILEGE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">database privilege name</td></tr></tbody></table>

<a id="d057b6861f9678f8"></a>
### V$AUDITABLE_SYSTEM_ACTIONS

The V$AUDITABLE_SYSTEM_ACTIONS displays auditable system actions.

**Column information**

<a id="5c1740e611f8c95b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ACTION_ID</td><td align="left">NUMBER</td><td align="left">auditable system action identifier</td></tr><tr><td align="left">ACTION_NAME</td><td align="left">VARCHAR(128)</td><td align="left">auditable system action name</td></tr></tbody></table>

<a id="d430e1a30dd1bc9d"></a>
### V$BACKUP

The V$BACKUP displays information of backup.

**Column information**

<a id="50da086069ce6383"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">BACKUP_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">indicates whether the tablespace begin backup ( ACTIVE ) or not ( INACTIVE )</td></tr><tr><td align="left" valign="middle">BACKUP_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the last checkpoint lsn of tablespace when backup started</td></tr></tbody></table>

<a id="81f486588fd8cd3d"></a>
### V$BALANCER

The V$BALANCER displays information of balancer.

**Column information**

<a id="c2f948fcf26e4056"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">balancer process identifier</td></tr><tr><td align="left">CUR_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">current number of connections</td></tr><tr><td align="left">CONNECTIONS</td><td align="left">NUMBER</td><td align="left">total number of connections</td></tr><tr><td align="left">CONNECTIONS_HIGHWATER</td><td align="left">NUMBER</td><td align="left">highest number of connections</td></tr><tr><td align="left">MAX_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">maximum connections</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">status</td></tr></tbody></table>

<a id="1df303ae690a6b71"></a>
### V$CLUSTER_DISPATCHER

The V$CLUSTER_DISPATCHER displays cluster dispatcher information.

> It is available only on a cluster.

**Column information**

<a id="707bfaeba43b043a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">DISPATCHER_ID</td><td align="left">NUMBER</td><td align="left">dispatcher identifier</td></tr><tr><td align="left">IS_SYNC</td><td align="left">BOOLEAN</td><td align="left">whether the dispatcher is sync or not</td></tr><tr><td align="left">RX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has received through the dispatcher</td></tr><tr><td align="left">TX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has transmitted through the dispatcher</td></tr><tr><td align="left">RX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs received</td></tr><tr><td align="left">TX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs transmitted</td></tr></tbody></table>

<a id="450b610303917bc0"></a>
### V$CLUSTER_LOCATION

The V$CLUSTER_LOCATION displays cluster location information.

> It is available only on a cluster.

**Column information**

<a id="7f28902c87c748f2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">member name</td></tr><tr><td align="left">HOST</td><td align="left">VARCHAR(128)</td><td align="left">host address of a member</td></tr><tr><td align="left">PORT</td><td align="left">NUMBER</td><td align="left">host port of a member</td></tr></tbody></table>

<a id="007dfbfed60d6971"></a>
### V$CLUSTER_MEMBER

The V$CLUSTER_MEMBER displays cluster member information.

> It is available only on a cluster.

**Column information**

<a id="1bb0bd2c12e1142b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member identifier</td></tr><tr><td align="left" valign="middle">MEMBER_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">status of the member: the value in ( ACTIVE, INACTIVE )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is global coordnator (TRUE) or not (FALSE)</td></tr><tr><td align="left" valign="middle">IS_GROUP_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is group coordnator (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="e193731f3072bb40"></a>
### V$COLUMNS

The V$COLUMNS has one row for each column of all the performance views (views beginning with V$).

Execute `\`desc as follows to retrieve the column information of performance view in nomount or mount phase in which V$COLUMNS is not available.

```
gSQL> \desc V$INSTANCE

COLUMN_NAME     TYPE                           IS_NULLABLE
--------------- ------------------------------ -----------
RELEASE_VERSION VARCHAR(64)          FALSE      
STARTUP_TIME    TIMESTAMP(2) WITHOUT TIME ZONE FALSE      
INSTANCE_STATUS VARCHAR(16)          FALSE
```

**Column information**

<a id="19bc4582f2d4d1ea"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position (&gt; 0) of the column in the performance view</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the column</td></tr></tbody></table>

<a id="dd8d33ae3dd5af56"></a>
### V$CONTROLFILE

This view displays information about GOLDILOCKS control files.

**Column information**

<a id="ff8937c87ad50c91"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">control file status ( VALID, CORRUPTED )</td></tr><tr><td align="left">CONTROLFILE_NAME</td><td align="left">VARCHAR(1152)</td><td align="left">control file name ( absolute path )</td></tr><tr><td align="left">LAST_CHECKPOINT_LSN</td><td align="left">NATIVE_BIGINT</td><td align="left">the last checkpoint lsn</td></tr><tr><td align="left">IS_PRIMARY</td><td align="left">BOLLEAN</td><td align="left">indicates whether the control file is primary</td></tr></tbody></table>

<a id="79c3673feec2f180"></a>
### V$DATAFILE

The V$DATAFILE displays information of all datafiles.

**Column information**

<a id="96e9c68756c0e3cf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">DATAFILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">datafile name ( absolute path )</td></tr><tr><td align="left" valign="middle">CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">LSN at last checkpoint ( null if temporary tablespace )</td></tr><tr><td align="left" valign="middle">CREATION_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">timestamp of the datafile creation</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">datafile size ( in bytes )</td></tr><tr><td align="left" valign="middle">LOADED_CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">checkpoint LSN of the datafile loaded in memory</td></tr><tr><td align="left" valign="middle">CORRUPT_PAGE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">number of corrupt pages in the datafile</td></tr></tbody></table>

<a id="d5629f60226b3030"></a>
### V$DB_FILE

The V$DB_FILE displays a list of all files using in database.

**Column information**

<a id="e5afc20669dac44c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">FILE_NAME</td><td align="left">VARCHAR(1024)</td><td align="left">file name</td></tr><tr><td align="left">FILE_TYPE</td><td align="left">VARCHAR(16)</td><td align="left">file type</td></tr></tbody></table>

<a id="975bccf11bf3438f"></a>
### V$DISPATCHER

The V$DISPATCHER displays information of dispatchers.

**Column information**

<a id="578de6566bf8bded"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher process identifier</td></tr><tr><td align="left" valign="middle">RESPONSE_JOB_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">response job count</td></tr><tr><td align="left" valign="middle">ACCEPT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">indicates whether this dispatcher is accepting new connections</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">process start time</td></tr><tr><td align="left" valign="middle">CUR_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS_HIGHWATER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">highest number of connections</td></tr><tr><td align="left" valign="middle">MAX_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum connections</td></tr><tr><td align="left" valign="middle">RECV_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">receive status</td></tr><tr><td align="left" valign="middle">RECV_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of received</td></tr><tr><td align="left" valign="middle">RECV_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of received</td></tr><tr><td align="left" valign="middle">RECV_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">RECV_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">send status</td></tr><tr><td align="left" valign="middle">SEND_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of sent</td></tr><tr><td align="left" valign="middle">SEND_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of sent</td></tr><tr><td align="left" valign="middle">SEND_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of send (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of send (1/100 second)</td></tr></tbody></table>

<a id="f733591483a03b84"></a>
### V$ERROR_CODE

The V$ERROR_CODE displays a list of all GOLDILOCKS error codes.

**Column information**

<a id="f94efc39aaf144f3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ERROR_CODE</td><td align="left">NUMBER</td><td align="left">GOLDILOCKS error code</td></tr><tr><td align="left">SQL_STATE</td><td align="left">VARCHAR(32)</td><td align="left">standard SQLSTATE code</td></tr><tr><td align="left">ERROR_MESSAGE</td><td align="left">VARCHAR(1024)</td><td align="left">error message</td></tr></tbody></table>

<a id="2f84fe1b550d38f7"></a>
### V$GLOBAL_TRANSACTION

The V$GLOBAL_TRANSACTION displays information on the currently active global transactions.

**Column information**

<a id="4894d871441440c5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">global transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the global transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the global transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">global transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the global transaction is repreparable</td></tr></tbody></table>

<a id="e64900f51a6a1977"></a>
### V$INCREMENTAL_BACKUP

The V$INCREMENTAL_BACKUP displays information about control files and datafiles in backup sets from the control file.

**Column information**

<a id="c0f21e636841afbc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BACKUP_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">backup file name ( absolute path )</td></tr><tr><td align="left" valign="middle">BACKUP_SCOPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">incremental backup scope: the value in ( database, tablespace, control )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_LEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">incremental backup level: the value in ( 0, 1, 2, 3, 4 )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">incremental backup type: the value in ( DIFFERENTIAL, CUMULATIVE )</td></tr><tr><td align="left" valign="middle">LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">all changes up to checkpoint LSN are included in this backup</td></tr><tr><td align="left" valign="middle">BEGIN_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup beginning time</td></tr><tr><td align="left" valign="middle">COMPLETION_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup completion time</td></tr></tbody></table>

<a id="581a2407b615670b"></a>
### V$INSTANCE

This view displays the state of the current instance.

> When database is transited to open phase, it is possible to select *READ ONLY* or *READ WRITE*. If not selected, DATA_ACCESS_MODE is determined by the value of DATABASE_ACCESS_MODE property. DATA_ACCESS_MODE is displayed as *NONE* in nomount or mount phase.

**Column information**

<a id="99b5ca843e91b34d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">RELEASE_VERSION</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">release version</td></tr><tr><td align="left" valign="middle">STARTUP_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">time when the instance was started</td></tr><tr><td align="left" valign="middle">INSTANCE_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">status of the instance: the value in ( STARTED, MOUNTED, OPEN )</td></tr><tr><td align="left" valign="middle">DATA_ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">data access mode of the instance: the value in ( NONE, READ_ONLY, READ_WRITE )</td></tr></tbody></table>

<a id="8dafec4e9891c06d"></a>
### V$JOURNALING

The V$JOURNALING displays journaling information.

> It is available only on a cluster.

**Column information**

<a id="33bec149c15d8b60"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">table name</td></tr><tr><td align="left">SHARD_ID</td><td align="left">NUMBER</td><td align="left">shard identifier</td></tr><tr><td align="left">RECORD_COUNT</td><td align="left">NUMBER</td><td align="left">journaled record count</td></tr><tr><td align="left">TOTAL_SIZE</td><td align="left">NUMBER</td><td align="left">total size of journaled records (byte)</td></tr></tbody></table>

<a id="1080ad52fff7eced"></a>
### V$KEYWORDS

The V$KEYWORDS displays a list of all SQL keywords.

**Column information**

<a id="0ed410d86314fa9c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">KEYWORD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of keyword</td></tr><tr><td align="left" valign="middle">KEYWORD_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">length of the keyword</td></tr><tr><td align="left" valign="middle">IS_RESERVED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the keyword cannot be used as an identifier (TRUE) or whether the keyword is not reserved (FALSE)</td></tr></tbody></table>

<a id="2155ad2a7bf94014"></a>
### V$LATCH

The V$LATCH shows latch information.

**Column information**

<a id="e5b59d20ec50b3af"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">LATCH_DESCRIPTION</td><td align="left">VARCHAR(64)</td><td align="left">latch description</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">reference count</td></tr><tr><td align="left">SPIN_LOCK</td><td align="left">VARCHAR(3)</td><td align="left">indicates whether the spin lock is locked ( YES ) or not ( NO )</td></tr><tr><td align="left">WAIT_COUNT</td><td align="left">NUMBER</td><td align="left">wait count</td></tr><tr><td align="left">CURRENT_MODE</td><td align="left">VARCHAR(32)</td><td align="left">current latch mode: the value in ( INITIAL, SHARED, EXCLUSIVE )</td></tr></tbody></table>

<a id="ce9f65e969e6d20f"></a>
### V$LOGFILE

The V$LOGFILE displays information of all redo log members.

**Column information**

<a id="3ca9544f48063a18"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">redo log group identifier</td></tr><tr><td align="left" valign="middle">FILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">name of the log member</td></tr><tr><td align="left" valign="middle">GROUP_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the log group: the value in ( UNUSED, ACTIVE, CURRENT, INACTIVE )</td></tr><tr><td align="left" valign="middle">FILE_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file sequence number of the log member</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file size of the log member ( in bytes )</td></tr></tbody></table>

<a id="ea122e1e779aa3ec"></a>
### V$LOCK_WAIT

This view lists the locks currently held and outstanding requests for a lock.

**Column information**

<a id="ecca277b293bc7a3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GRANT_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that holds the lock</td></tr><tr><td align="left">REQUEST_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that requests the lock</td></tr></tbody></table>

<a id="ea6b63bcc1b5f4de"></a>
### V$PROCESS_STAT

The V$PROCESS_STAT displays goldilocks process statistics.

**Column information**

<a id="60148b94a0eb977a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="350d60c91bfb5ad7"></a>
### V$PROCESS_MEM_STAT

The V$PROCESS_MEM_STAT displays goldilocks process memory statistics.

**Column information**

<a id="e539fc083cfd75ab"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="f18f32929348783e"></a>
### V$PROCESS_SQL_STAT

The V$PROCESS_SQL_STAT displays goldilocks process SQL statistics.

**Column information**

<a id="2ff85b5dfebfd03e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="6460f1d2e272099c"></a>
### V$PROPERTY

The V$PROPERTY displays a list of all properties at current session. Otherwise, the instance-wide value.

**Column information**

<a id="812aefc76476b4a1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the session</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr></tbody></table>

<a id="a7399e9764512204"></a>
### V$PSM_RESERVED_WORDS

The V$PSM_RESERVED_WORDS displays a list of all PSM reserved keywords. Reserved words cannot be used in variable name or procedure name.

**Column information**

<a id="78ad94e51462e331"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| KEYWORD_NAME | VARCHAR(128) | name of keyword |
| KEYWORD_LENGTH | NUMBER | length of the keyword |

<a id="1f71a4fa757ff5eb"></a>
### V$QUEUE

The V$QUEUE displays information of queue.

**Column information**

<a id="10b8e862df15f7ff"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TYPE</td><td align="left">NUMBER</td><td align="left">queue type ( COMMON or DISPATCHER )</td></tr><tr><td align="left">INDEX</td><td align="left">NUMBER</td><td align="left">index</td></tr><tr><td align="left">QUEUED</td><td align="left">NUMBER</td><td align="left">number of items in the queue</td></tr><tr><td align="left">WAIT</td><td align="left">NUMBER</td><td align="left">total time that all items in this queue have waited (1/100 second)</td></tr><tr><td align="left">TOTALQ</td><td align="left">VARCHAR(128)</td><td align="left">total number of items that have ever been in the queue</td></tr></tbody></table>

<a id="5c6b10f7f13abfbf"></a>
### V$RESERVED_WORDS

The V$RESERVED_WORDS displays a list of all SQL reserved keywords. Reserved words cannot be used in table name or column name.

**Column information**

<a id="91f67c4f902be37f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">KEYWORD_NAME</td><td align="left">VARCHAR(128)</td><td align="left">name of keyword</td></tr><tr><td align="left">KEYWORD_LENGTH</td><td align="left">NUMBER</td><td align="left">length of the keyword</td></tr></tbody></table>

<a id="69bbe37a03c35781"></a>
### V$SESSION

The V$SESSION displays session information for each current session.

**Column information**

<a id="e1cd68744d7a8c0b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier ( -1 if inactive transaction )</td></tr><tr><td align="left" valign="middle">CONNECTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">connection type: the value in ( DA, TCP )</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name</td></tr><tr><td align="left" valign="middle">SESSION_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">status of the session: the value in ( CONNECTED, SIGNALED, SNIPED, DEAD )</td></tr><tr><td align="left" valign="middle">SERVER_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">server type: the value in ( DEDICATED, SHARED )</td></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client process identifier</td></tr><tr><td align="left" valign="middle">LOGON_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">logon time</td></tr><tr><td align="left" valign="middle">PROGRAM_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">program name</td></tr><tr><td align="left" valign="middle">CLIENT_ADDRESS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">client address ( null if DA )</td></tr><tr><td align="left" valign="middle">CLIENT_PORT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client port ( 0 if DA )</td></tr><tr><td align="left" valign="middle">FAILOVER_TYPE</td><td align="left" valign="middle">VARCHAR(13)</td><td align="left" valign="middle">indicates whether and to what extent transparent application failover (TAF) is enabled for the session ( NONE, SESSION )</td></tr><tr><td align="left" valign="middle">FAILED_OVER</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is running in failover mode and failover has occurred (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IS_AUDITED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is audited (YES) or not (NO)</td></tr></tbody></table>

<a id="5aec2842d674fa7f"></a>
### V$SESSION_AUDIT

The V$SESSION_AUDIT displays audited session information.

**Column information**

<a id="782de73367d5e619"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">active audit policy name</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="cc047cdb1f972c65"></a>
### V$SESSION_CONNECT_INFO

The V$SESSION_CONNECT_INFO displays information about network connections for the current session.

**Column information**

<a id="b1579d0716cb1362"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">SERIAL_NO</td><td align="left">NUMBER</td><td align="left">session serial number</td></tr><tr><td align="left">CLIENT_CHARSET</td><td align="left">VARCHAR(40)</td><td align="left">client character set</td></tr></tbody></table>

<a id="80e91c211204a7b6"></a>
### V$SESSION_EVENT

The V$SESSION_EVENT displays information on waits for an event by a session.

**Column information**

<a id="a6232dd78e5d9df0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">ID of the session</td></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">MAX_WAIT</td><td align="left">NUMBER</td><td align="left">Maximum time waited for the event by the session (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="3f17210f3f8cf18a"></a>
### V$SESSION_STAT

The V$SESSION_STAT displays session statistics.

**Column information**

<a id="f5949b5da7fa3c1c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="0fde94933b6ecb7f"></a>
### V$SESSION_MEM_STAT

The V$SESSION_MEM_STAT displays session memory statistics.

**Column information**

<a id="cdde65340cf95d67"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="67d17c06f74c7b2a"></a>
### V$SESSION_SQL_STAT

The V$SESSION_SQL_STAT displays session SQL statistics.

**Column information**

<a id="19e510b8998322b3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="f9bc7b650b276801"></a>
### V$SESSION_WAIT

The V$SESSION_WAIT displays the current or last wait for each session.

**Column information**

<a id="218059a86d00591e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID of the session</td></tr><tr><td align="left" valign="middle">SEQ_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Identifier of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Name of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">A number that uniquely identifies the current or last wait (incremented for each wait)</td></tr><tr><td align="left" valign="middle">P1TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the first parameter for the wait event</td></tr><tr><td align="left" valign="middle">P1</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">First wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P1HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">First wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P2TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the second parameter for the wait event</td></tr><tr><td align="left" valign="middle">P2</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Second wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P2HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Second wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P3TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the third parameter for the wait event</td></tr><tr><td align="left" valign="middle">P3</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Third wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P3HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Third wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">STATE</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Wait state</td></tr><tr><td align="left" valign="middle">WAIT_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the session is currently waiting, then the value is time waited for the current wait. If the session is not in a wait, then the value is the duration of the last wait (in microseconds)</td></tr><tr><td align="left">TIME_SINCE_LAST_WAIT</td><td align="left">NUMBER</td><td align="left">Time elapsed since the end of the last wait (in microseconds). If the session is currently in a wait, then the value is 0.</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="7c462422a68a2b62"></a>
### V$SHARED_MODE

The V$SHARED_MODE displays information of shared mode.

**Column information**

<a id="b93f90eb61655a1c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">name</td></tr><tr><td align="left">VALUE</td><td align="left">VARCHAR(128)</td><td align="left">value</td></tr></tbody></table>

<a id="69cfd22f600f649c"></a>
### V$SHARED_SERVER

The V$SHARED_SERVER displays information of shared servers.

**Column information**

<a id="c33634e19dec0654"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">shared server process identifier</td></tr><tr><td align="left">PROCESSED_JOB_COUNT</td><td align="left">NUMBER</td><td align="left">processed job count</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(128)</td><td align="left">status</td></tr><tr><td align="left">IDLE</td><td align="left">NUMBER</td><td align="left">total idle time (1/100 second)</td></tr><tr><td align="left">BUSY</td><td align="left">NUMBER</td><td align="left">total busy time (1/100 second)</td></tr></tbody></table>

<a id="d8afef344e2dbfd6"></a>
### V$SHM_SEGMENT

The V$SHM_SEGMENT displays a list of all shared memory segments.

**Column information**

<a id="5fd56a16378d06c7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SHM_NAME</td><td align="left">VARCHAR(32)</td><td align="left">shared memory segment name</td></tr><tr><td align="left">SHM_ID</td><td align="left">NUMBER</td><td align="left">shared memory segment identifier</td></tr><tr><td align="left">SHM_SIZE</td><td align="left">NUMBER</td><td align="left">shared memory segment size ( in bytes )</td></tr><tr><td align="left">SHM_KEY</td><td align="left">NUMBER</td><td align="left">shared memory segment key</td></tr><tr><td align="left">SHM_SEQ</td><td align="left">NUMBER</td><td align="left">shared memory segment sequence</td></tr><tr><td align="left">SHM_ADDR</td><td align="left">VARCHAR(32)</td><td align="left">start address of the shared memory segment</td></tr></tbody></table>

<a id="880f62d4ee4b6161"></a>
### V$SPROPERTY

The V$SPROPERTY displays a list of Properties. This is store a binary property file.

**Column information**

<a id="cd22a08cae119c13"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value stored in the binary property file</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value is BINARY_FILE</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the system</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr></tbody></table>

<a id="3f003d35cd9a3077"></a>
### V$SQLFN_METADATA

The V$SQLFN_METADATA contains metadata about operators and built-in functions

**Column information**

<a id="029e463234d5ea06"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FUNC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the built-in function</td></tr><tr><td align="left" valign="middle">MINARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum number of arguments for the function</td></tr><tr><td align="left" valign="middle">MAXARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum number of arguments for the function</td></tr><tr><td align="left" valign="middle">IS_AGGREGATE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the function is an aggregate function (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="7c2a2043779754ab"></a>
### V$SQL_CACHE

The V$SQL_CACHE lists statistics of shared SQL plan.

**Column information**

<a id="652574183fa6324b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SQL_HANDLE</td><td align="left">NUMBER</td><td align="left">SQL handle</td></tr><tr><td align="left">HASH_VALUE</td><td align="left">NUMBER</td><td align="left">hash value of the SQL statement</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">count of prepared statements referencing the statement</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">CLOCK_ID</td><td align="left">NUMBER</td><td align="left">clock identifier</td></tr><tr><td align="left">PLAN_AGE</td><td align="left">NUMBER</td><td align="left">plan age</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">user name</td></tr><tr><td align="left">BIND_PARAM_COUNT</td><td align="left">NUMBER</td><td align="left">count of bind parameters</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">SQL full text</td></tr><tr><td align="left">PLAN_COUNT</td><td align="left">NUMBER</td><td align="left">physical plan count of the SQL statement</td></tr><tr><td align="left">PLAN_ID</td><td align="left">NUMBER</td><td align="left">plan identifier</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">PLAN_IS_ATOMIC</td><td align="left">BOOLEAN</td><td align="left">plan is atomic array insert or not</td></tr><tr><td align="left">PLAN_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">plan text for SQL statement</td></tr></tbody></table>

<a id="d3f875d0d2cc9ccc"></a>
### V$SQL_COMMAND

The V$SQL_COMMAND lists attribute information of each SQL command.

**Column information**

<a id="0519ebb7da118fcd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">COMMAND</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">SQL command</td></tr><tr><td align="left" valign="middle">FROM_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable from start-up phase</td></tr><tr><td align="left" valign="middle">UNTIL_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable until start-up phase</td></tr><tr><td align="left" valign="middle">ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database access mode: values in (NONE, READ &amp; WRITE, READ, READ &amp; LOCK)</td></tr><tr><td align="left" valign="middle">NEED_FETCH</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the command is a query which has result set and need fetch</td></tr><tr><td align="left" valign="middle">IS_DDL</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is a DDL(Data Defintion Language) or not</td></tr><tr><td align="left" valign="middle">AUTO_COMMIT</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is auto-commit or not</td></tr><tr><td align="left" valign="middle">IS_CACHEABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is plan-cacheable or not</td></tr><tr><td align="left" valign="middle">AUDIT_ACTION</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">auditiable action name for the SQL command</td></tr></tbody></table>

<a id="a41f94b74e83a242"></a>
### V$SQL_HISTORY

The V$SQL_HISTORY displays information of SQLs.

**Column information**

<a id="8ba5c7cbf760a333"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement start time</td></tr><tr><td align="left" valign="middle">EXEC_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">execution time(us)</td></tr><tr><td align="left" valign="middle">PREPARED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is prepared ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">SUCCESS</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is success ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">CHARACTER VARYING(16)</td><td align="left" valign="middle">status of the statement: the value in<br>( RUNNING, DONE )</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">CHARACTER VARYING(1024)</td><td align="left" valign="middle">first 1024 bytes of the SQL text for the statement</td></tr></tbody></table>

<a id="cffdddb884541e19"></a>
### V$STATEMENT

The V$STATEMENT lists all statements.

**Column information**

<a id="afdd3af3d068458f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STMT_ID</td><td align="left">NUMBER</td><td align="left">statement identifier in a session</td></tr><tr><td align="left">STMT_VIEW_SCN</td><td align="left">NUMBER</td><td align="left">statement view scn</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">VARCHAR(1024)</td><td align="left">first 1024 bytes of the SQL text for the statement</td></tr><tr><td align="left">START_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">statement start time</td></tr></tbody></table>

<a id="b7b984cfc1731725"></a>
### V$SYSTEM_EVENT

The V$SYSTEM_EVENT displays information on total waits for an event.

**Column information**

<a id="5a7e4ab159c665da"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="991d7cc84066b7bc"></a>
### V$SYSTEM_STAT

The V$SYSTEM_STAT displays system statistics.

**Column information**

<a id="460b81ab275afb4a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="b5ba8c7debe46aa8"></a>
### V$SYSTEM_MEM_STAT

The V$SYSTEM_MEM_STAT displays system memory statistics.

**Column information**

<a id="b203a27255aca56a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="089cc5881e05e6c9"></a>
### V$SYSTEM_SQL_STAT

The V$SYSTEM_SQL_STAT displays system SQL statistics.

**Column information**

<a id="34d132aa4e0b29f2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="3350fad34fb6e76b"></a>
### V$TABLES

The V$TABLES contains the definitions of all the performance views (views beginning with V$).

**Column information**

<a id="f227fb63f2a9a0da"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">visible startup phase of the performance view</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>created time of the performance view</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>modified time of the performance view</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>comments of the performance view</td></tr></tbody></table>

<a id="be1e643546f2fb41"></a>
### V$TABLESPACE

This view displays tablespace information.

**Column information**

<a id="d4a0b6f012e6b250"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">TBS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier</td></tr><tr><td align="left" valign="middle">TBS_ATTR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace attribute: the value in ( device attribute (MEMORY) | temporary attribute (TEMPORARY, PERSISTENT) | usage attribute(DICT, UNDO, DATA, TEMPORARY) )</td></tr><tr><td align="left" valign="middle">IS_LOGGING</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is a logging tablespace ( YES ) or not ( NO )</td></tr><tr><td align="left" valign="middle">IS_ONLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is ONLINE ( YES ) or OFFLINE ( NO )</td></tr><tr><td align="left" valign="middle">OFFLINE_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">indicates whether the tablespace can be taken online normally ( CONSISTENT ) or not ( INCONSISTENT ). null if the tablespace is ONLINE</td></tr><tr><td align="left" valign="middle">EXTENT_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">extent size of the tablespace ( in bytes )</td></tr><tr><td align="left" valign="middle">PAGE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="c66effa4ede0e952"></a>
### V$TABLESPACE_STAT

This view displays tablespace statistical information.

**Column information**

<a id="d6c7492820844056"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TBS_NAME</td><td align="left">VARCHAR(128)</td><td align="left">tablespace name</td></tr><tr><td align="left">TBS_ID</td><td align="left">NUMBER</td><td align="left">tablespace identifier</td></tr><tr><td align="left">TOTAL_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">total extent count of the tablespace</td></tr><tr><td align="left">USED_META_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">meta extent count currently used on the tablespace</td></tr><tr><td align="left">USED_DATA_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">data extent count currently used on the tablespace</td></tr><tr><td align="left">FREE_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">free extent count of the tablespace</td></tr><tr><td align="left">EXTENT_SIZE</td><td align="left">NUMBER</td><td align="left">extent size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="89876a17b9e59ca0"></a>
### V$TRANSACTION

The V$TRANSACTION lists the active transactions in the system.

**Column information**

<a id="b42f31a344577d42"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier ( null if the global transaction is unassociated</td></tr><tr><td align="left" valign="middle">TRANS_SLOT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction slot identifier</td></tr><tr><td align="left" valign="middle">PHYSICAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">physical transaction identifier</td></tr><tr><td align="left" valign="middle">TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction state: the value in ( ACTIVE, BLOCK, PREPARE, COMMIT, ROLLBACK, IDLE, PRECOMMIT )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the transaction is global or not</td></tr><tr><td align="left" valign="middle">TRANS_ATTRIBUTE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction attribute: the value in ( READ_ONLY, UPDATABLE, LOCKABLE, UPDATABLE | LOCKABLE )</td></tr><tr><td align="left" valign="middle">ISOLATION_LEVEL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction isolation level: the value in ( READ COMMITTED, SERIALIZABLE )</td></tr><tr><td align="left" valign="middle">TRANS_VIEW_SCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction view scn</td></tr><tr><td align="left" valign="middle">TCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction change number</td></tr><tr><td align="left" valign="middle">TRANS_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction sequence number</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">transaction start time</td></tr></tbody></table>

<a id="e609fc9cdab47c32"></a>
### V$WAIT_EVENT_CLASS_NAME

The V$WAIT_EVENT_CLASS_NAME displays information about Class of wait event.

**Column information**

<a id="7b280d226e95dbbd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the class of the wait event</td></tr></tbody></table>

<a id="53df1e5560ed6393"></a>
### V$WAIT_EVENT_NAME

The V$WAIT_EVENT_NAME displays information about wait events.

**Column information**

<a id="2b39b9fe336779c8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the first parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the second parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the third parameter for the wait event</td></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="9f7740f692116732"></a>
### V$XA_TRANSACTION

The V$XA_TRANSACTION displays information on the currently active XA transactions.

**Column information**

<a id="5a7fc477bb29c720"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">XA_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">XA transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">XA_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the XA transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the XA transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">XA transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the XA transaction is repreparable</td></tr></tbody></table>

---

[← 8. GOLDILOCKS Database Replication](8-goldilocks-database-replication.md) · [Table of contents](../README.md) · [10. Server Property →](10-server-property.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
