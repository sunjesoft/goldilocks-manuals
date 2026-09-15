<a id="d20afce9d2025bfe"></a>

# 9. Database Information

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/d20afce9d2025bfe)  
> 태그: `26c.1_0_tag`

[← 8. GOLDILOCKS 데이터베이스 이중화](8-goldilocks-데이터베이스-이중화.md) · [전체 목차](../README.md) · [10. Server Property →](10-server-property.md)

<a id="72c0cc66453855b4"></a>
## DICTIONARY_SCHEMA

DICTIONARY_SCHEMA 스키마는 시스템 내의 SQL 객체와 이와 관련된 정보를 얻기 위한 view나 테이블을 포함하고 있다.

> DICTIONARY_SCHEMA의 view와 테이블들은 open 단계부터 조회할 수 있다.

해당 view들을 사용하려면 다음과 같이 DictionarySchema.sql을 실행해야 한다.

- Standalone의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/DictionarySchema.sql
```

- Cluster의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/DictionarySchema.sql
```

View나 테이블의 이름에 따라 다음과 같은 정보를 얻을 수 있다.

- ALL 계열 view
    - ALL_로 시작하는 이름을 가진 view
    - 현재 사용자가 접근 가능한 객체에 대한 정보
- DBA 계열 view
    - DBA_로 시작하는 이름을 가진 view
    - DBA 권한 (ACCESS CONTROL ON DATABASE)을 가지고 있는 현재 사용자의 모든 객체에 대한 정보
- USER 계열 view
    - USER_로 시작하는 이름을 가진 view
    - 현재 사용자가 소유한 객체에 대한 정보

<a id="ffb8201653d4ce0a"></a>
### ALL 계열 View

현재 사용자가 접근 가능한 객체에 대한 정보를 얻을 수 있다.

<a id="dc565e7fcadcbd4c"></a>
#### ALL_ALL_TABLES

ALL_ALL_TABLES describes the object tables and relational tables accessible to the current user.

**Column 정보**

<a id="4d61033d45433010"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="f5fb8e730f20eaed"></a>
#### ALL_ARGUMENTS

ALL_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="2513639975069d6e"></a>
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
| DATA_TYPE | VARCHAR(128) | Data Type of the argument |
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

<a id="aa2e74896010d145"></a>
#### ALL_CATALOG

ALL_CATALOG displays the tables, views, synonyms, and sequences accessible to the current user.

**Column 정보**

<a id="0a88eec95db54eca"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_NAME | VARCHAR(128) | Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_TYPE | VARCHAR(32) | Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |

<a id="9a65c1aae94a7159"></a>
#### ALL_CLUSTER_TABLES

ALL_CLUSTER_TABLES describes all cluster tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="a7a3cbaed36ac9e1"></a>
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

<a id="ff557ebf665a49fb"></a>
#### ALL_COL_COMMENTS

ALL_COL_COMMENTS displays comments on the columns of the tables and views accessible to the current user.

**Column 정보**

<a id="023f25f9c102852b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| COMMENTS | VARCHAR(1024) | Comment on the column |

<a id="15332b2b242e0769"></a>
#### ALL_COL_PRIVS

ALL_COL_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="877e000fe19bd300"></a>
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

<a id="9159e112df77170a"></a>
#### ALL_COL_PRIVS_MADE

ALL_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner or grantor.

**Column 정보**

<a id="54ca7864fd14b043"></a>
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

<a id="df74a52c4b90a300"></a>
#### ALL_COL_PRIVS_RECD

ALL_COL_PRIVS_RECD describes the column object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="8a7c5f7d256556b9"></a>
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

<a id="3ae785a09e4fae66"></a>
#### ALL_CONSTRAINTS

ALL_CONSTRAINTS describes constraint definitions on tables accessible to the current user.

**Column 정보**

<a id="29f9aa9974baabae"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="c02a278e388d9880"></a>
#### ALL_CONS_COLUMNS

ALL_CONS_COLUMNS describes columns that are accessible to the current user and that are specified in constraints.

**Column 정보**

<a id="a2909556baf8363d"></a>
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

<a id="61a310d4e33b8e32"></a>
#### ALL_DB_PRIVS

ALL_DB_PRIVS describes the database grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="1e0ea0d04ad25ca6"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="cbcc08828938a5d2"></a>
#### ALL_DB_PRIVS_MADE

ALL_DB_PRIVS_MADE describes the database grants for which the current user is the grantor.

**Column 정보**

<a id="2ddcb8ceedeadfe9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="88628013b7184da3"></a>
#### ALL_DB_PRIVS_RECD

ALL_DB_PRIVS_RECD describes the database grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="0c5ce7c302abb764"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="3a2d49f5e51a4954"></a>
#### ALL_DEPENDENCIES

ALL_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column 정보**

<a id="6ee0190c864b6cc9"></a>
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

<a id="06dd4dd336b21820"></a>
#### ALL_GLOBAL_SECONDARY_INDEXES

ALL_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables accessible to the current user.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="daddc171eb1bad7f"></a>
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

<a id="570217f7cd3f740d"></a>
#### ALL_GSI_PLACE

ALL_GSI_PLACE describes node placement of all global secondary indexes on the tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="dc29ffd19e0ff0e8"></a>
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

<a id="b7f4d01b2a94e713"></a>
#### ALL_HISTOGRAM_BALANCE

ALL_HISTOGRAM_BALANCE describes each height-balanced histogram bucket accessible to the current user.

**Column 정보**

<a id="43b11f104100af7d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of height-balanced histogram |
| BUCKET_ACCU_HEIGHT | NUMBER | Accumulated height of the height-balanced histogram bucket |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="dad9ef0d72ca81dd"></a>
#### ALL_HISTOGRAM_FREQUENCY

ALL_HISTOGRAM_FREQUENCY describes each frequency histogram bucket accessible to the current user.

**Column 정보**

<a id="31f9be3f020ee154"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of frequency histogram |
| BUCKET_HEIGHT | NUMBER | Bucket height of the frequency histogram bucket |
| SAMPLE_COUNT | NUMBER | Sample count of frequency histogram |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="d1fd272774a3b73a"></a>
#### ALL_INDEXES

ALL_INDEXES describes the indexes on the tables accessible to the current user.

**Column 정보**

<a id="59b8a8bfa04c7666"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or DISABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="6434c96b3ab834d5"></a>
#### ALL_IND_COLUMNS

ALL_IND_COLUMNS describes the columns of indexes on all tables accessible to the current user.

**Column 정보**

<a id="d7725a184eceef19"></a>
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

<a id="0cfa92ed07146ea0"></a>
#### ALL_IND_PLACE

ALL_IND_PLACE describes node placement of the indexes on the tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="1a8a6b3a4ede393c"></a>
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

<a id="d98055987666e009"></a>
#### ALL_LIBRARIES

ALL_LIBRARIES describes the libraries accessible to the current user.

**Column 정보**

<a id="1cb400963bf4340c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of Library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema Name of Library |
| LIBRARY_NAME | VARCHAR(128) | Name of Library |
| FILE_SPEC | LONG VARCHAR | Operating system file specification associated with the library |
| DYNAMIC | VARCHAR(1) | Indicates whether the library is dynamically loadable (Y) or not (N) |
| STATUS | VARCHAR(32) | Status of the library : the value in ( VALID, INVALID, N/A ) |
| AGENT | VARCHAR(128) | Agent of the library |
| LEAF_FILENAME | VARCHAR(4000) | Leaf filename of the library |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |
| COMMENTS | VARCHAR(1024) | Comment on the library |

<a id="ecc689fec6b9a03d"></a>
#### ALL_LIBRARY_PRIVS

ALL_LIBRARY_PRIVS describes the library grants, for which the current user is the library owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="db3ce88d926c4338"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="dbe2595e1791998b"></a>
#### ALL_LIBRARY_PRIVS_MADE

ALL_LIBRARY_PRIVS_MADE describes the library grants for which the current user is the library owner or grantor.

**Column 정보**

<a id="e8602ce1bb15b9e3"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="3c76a7b72dfc2ce6"></a>
#### ALL_LIBRARY_PRIVS_RECD

ALL_LIBRARY_PRIVS_RECD describes the library grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="d3c8e6a648d8f5a8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="1d6dad84e8b15dfe"></a>
#### ALL_NONSCHEMA_COMMENTS

ALL_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces) accessible to the current user.

**Column 정보**

<a id="91ba2d83602759b6"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OBJECT_NAME | VARCHAR(128) | Name of the non-schema object |
| OBJECT_TYPE | VARCHAR(32) | Type of the non-schema object: DATABASE, AUTHORIZATION, SCHEMA, TABLESPACE |
| COMMENTS | VARCHAR(1024) | Comments of the non-schema object |

<a id="ccbbe24816949e2e"></a>
#### ALL_OBJECTS

ALL_OBJECTS describes all objects accessible to the current user.

**Column 정보**

<a id="b51b4c92ea087b0c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="c3c7638b7d5fde20"></a>
#### ALL_PACKAGE_PRIVS

ALL_PACKAGE_PRIVS describes the package grants, for which the current user is the package owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="32c1e44a3cd09e48"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="53f2df90a2789754"></a>
#### ALL_PACKAGE_PRIVS_MADE

ALL_PACKAGE_PRIVS_MADE describes the package grants for which the current user is the package owner or grantor.

**Column 정보**

<a id="9cf8d659271c3d2f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="68b2c6f78e54b428"></a>
#### ALL_PACKAGE_PRIVS_RECD

ALL_PACKAGE_PRIVS_RECD describes the package grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="4f3e2b2474f2b66f"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="e7131befcd6a9436"></a>
#### ALL_PROCEDURES

ALL_PROCEDURES lists all function, procedures or package

**Column 정보**

<a id="b38dcb3a0b63e2cf"></a>
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

<a id="252044aa24074c61"></a>
#### ALL_PROC_PRIVS

ALL_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="1189cb79cd0136b7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="f3ffec0643c44342"></a>
#### ALL_PROC_PRIVS_MADE

ALL_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column 정보**

<a id="52018c636ea5360e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="c4ffee247f8b3452"></a>
#### ALL_PROC_PRIVS_RECD

ALL_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="1c5bcb268d817266"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="298934d4b94c08e6"></a>
#### ALL_SCHEMAS

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column 정보**

<a id="199bc467db35023d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| CREATED_TIME | TIMESTAMP(6) WITHOUT TIME ZONE | Created time of the schema |
| MODIFIED_TIME | TIMESTAMP(6) WITHOUT TIME ZONE | Last modified time of the schema |
| COMMENTS | VARCHAR(1024) | Comments of the schema |

<a id="0d8f802467fdbe89"></a>
#### ALL_SCHEMA_PATH

ALL_SCHEMA_PATH describes the schema search order of the current user and PUBLIC, for naming resolution of unqualified SQL schema objects.

**Column 정보**

<a id="4f7184fd77c92ef6"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| AUTH_NAME | VARCHAR(128) | Name of the authorization |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| SEARCH_ORDER | NUMBER | Schema search order of the authorization |

<a id="d4ad359f8cdc7602"></a>
#### ALL_SCHEMA_PRIVS

ALL_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="8554fe36aad2c2e7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| PRIVILEGE | VARCHAR(32) | Privilege on the schema |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="b0d4d36aca23f9c1"></a>
#### ALL_SCHEMA_PRIVS_MADE

ALL_SCHEMA_PRIVS_MADE describes the schema grants, for which the current user is the grantor.

**Column 정보**

<a id="3b340a3750f3c208"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="dc8710f678ec439a"></a>
#### ALL_SCHEMA_PRIVS_RECD

ALL_SCHEMA_PRIVS_RECD describes the schema grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="750350eaf2431b8a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f474cdc8f1ea5ed2"></a>
#### ALL_SEQUENCES

ALL_SEQUENCES describes all sequences accessible to the current user.

**Column 정보**

<a id="4189d850cf9f483b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Sequence name</td></tr><tr><td align="left" valign="middle">&nbsp;MIN_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;MAX_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;INCREMENT_BY</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">&nbsp;CYCLE_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;ORDER_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;CACHE_SIZE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_NUMBER</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="ca8af6c12e250b6f"></a>
#### ALL_SEQ_PRIVS

ALL_SEQ_PRIVS describes the sequence grants, for which the current user is the sequence owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="afe2945464797d95"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="792b971a0f3d669f"></a>
#### ALL_SEQ_PRIVS_MADE

ALL_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner or grantor.

**Column 정보**

<a id="52233f2cf3498932"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="c0d89a274452967e"></a>
#### ALL_SEQ_PRIVS_RECD

ALL_SEQ_PRIVS_RECD describes the sequence grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="a1d1e73d1b5632f6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ba23c7745a176b8a"></a>
#### ALL_SHARD_KEY_COLUMNS

ALL_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="b766a50d72416bf0"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="6886cacab277e385"></a>
#### ALL_SOURCE

ALL_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="907df8af973669be"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="46dab8b8f2fb45ad"></a>
#### ALL_STAT_COLUMN_GROUP

ALL_STAT_COLUMN_GROUP describes each column group statistics accessible to the current user.

**Column 정보**

<a id="b3c8d8ad5c94931c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| STAT_NAME | VARCHAR(128) | Statistics name |
| COLUMN_GROUPS | VARCHAR(1024) | Column names of the column group statistics |
| NUM_DISTINCT | NUMBER | Number of distinct values in the column group statistics |
| SAMPLE_SIZE | NUMBER | Sample size used in analyzing this column group statistics |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | Date on which this column group statistics was most recently analyzed |

<a id="90424165915ee36f"></a>
#### ALL_SYNONYMS

ALL_SYNONYMS describes all synonyms.

**Column 정보**

<a id="c629b4e224da0d7e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="bf27c90f06aa7c46"></a>
#### ALL_TABLES

ALL_TABLES describes the relational tables accessible to the current user.

**Column 정보**

<a id="0e8aee0795e58edc"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="216d7c326e937526"></a>
#### ALL_TAB_COLS

ALL_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="dacc8ff9829650a1"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="2a47031b2fd0c4b8"></a>
#### ALL_TAB_COLUMNS

ALL_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="f6683592e832e3b3"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="56d1b254b90e03d9"></a>
#### ALL_TAB_COMMENTS

ALL_TAB_COMMENTS displays comments on the tables and views accessible to the current user.

**Column 정보**

<a id="a2bc21a58e4debd5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="4b2b39b23c249cd8"></a>
#### ALL_TAB_IDENTITY_COLS

ALL_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="b009c4a53e754f23"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="08c1ae3b580b99da"></a>
#### ALL_TAB_PLACE

ALL_TAB_PLACE describes node placement of all cluster tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="7816b4d3b3af182e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td>MEMBER_POSITION</td><td>NUMBER</td><td>Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td>IS_UPDATE_MASTER</td><td>BOOLEAN</td><td>whether the cluster member is update master or not</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="df0ae14c10ea3b7a"></a>
#### ALL_TAB_SHARDS

ALL_TAB_SHARDS describes shard information of sharded tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="778ee53927d9187b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="7f2d1a1080e946dd"></a>
#### ALL_TAB_PRIVS

ALL_TAB_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="9068d01b14fb8f58"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="07a4248638ea8f7d"></a>
#### ALL_TAB_PRIVS_MADE

ALL_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner or grantor.

**Column 정보**

<a id="e5ea04a2dbc92713"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="402a1c8be296e247"></a>
#### ALL_TAB_PRIVS_RECD

ALL_TAB_PRIVS_RECD describes object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="cab9ce7bff2348fa"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="79f2f67ea1cd87f1"></a>
#### ALL_TBS_PRIVS

ALL_TBS_PRIVS describes the tablespace grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="0f6fe9f8c9269984"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="79042e3ca49b7096"></a>
#### ALL_TBS_PRIVS_MADE

ALL_TBS_PRIVS_MADE describes the tablespace grants for which the current user is the grantor.

**Column 정보**

<a id="7e68fe524b305d91"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="b4dfa871ef5ef515"></a>
#### ALL_TBS_PRIVS_RECD

ALL_TBS_PRIVS_RECD describes the tablespace grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="63efb4a8b9198594"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="4411cc85725f6776"></a>
#### ALL_TRIGGERS

ALL_TRIGGERS describes the triggers on tables accessible to the current user.

**Column 정보**

<a id="c20a1e1f219a4a77"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the trigger</td></tr><tr><td valign="middle">TRIGGER_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">When the trigger fires: the value in ( BEFORE STATEMENT, BEFORE EACH ROW, AFTER STATEMENT, AFTER EACH ROW, INSTEAD OF, COMPOUND )</td></tr><tr><td valign="middle">TRIGGERING_EVENT</td><td valign="middle">VARCHAR(32)</td><td valign="middle">DML, DDL, or database event that fires the trigger</td></tr><tr><td valign="middle">TABLE_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the table on which the trigger is defined</td></tr><tr><td valign="middle">TABLE_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the table on which the trigger is defined</td></tr><tr><td valign="middle">BASE_OBJECT_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Base object on which the trigger is defined: the value in ( TABLE, VIEW, SCHEMA, DATABASE )</td></tr><tr><td valign="middle">TABLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">If the base object type of the trigger is SCHEMA or DATABASE, then this column is NULL; if the base object type of the trigger is TABLE or VIEW then this column indicates the table or view name on which the trigger is defined</td></tr><tr><td valign="middle">COLUMN_NAME</td><td valign="middle">VARCHAR(4000)</td><td valign="middle">Name of the nested table column (if a nested table trigger), else NULL</td></tr><tr><td valign="middle">REFERENCING_NAMES</td><td valign="middle">VARCHAR(1024)</td><td valign="middle">Names used for referencing OLD and NEW column values from within the trigger</td></tr><tr><td valign="middle">WHEN_CLAUSE</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Must evaluate to TRUE for TRIGGER_BODY to execute</td></tr><tr><td valign="middle">STATUS</td><td valign="middle">VARCHAR(8)</td><td valign="middle">Indicates whether the trigger is enabled (ENABLED) or disabled (DISABLED); a disabled trigger will not fire</td></tr><tr><td valign="middle">DESCRIPTION</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Trigger description; useful for re-creating a trigger creation statement</td></tr><tr><td valign="middle">ACTION_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Action type of the trigger body: the value in ( CALL, PSM BLOCK )</td></tr><tr><td valign="middle">TRIGGER_BODY</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Statements executed by the trigger when it fires</td></tr><tr><td valign="middle">CROSSEDITION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Type of crossedition trigger: the value in ( FORWARD, REVERSE, NO )</td></tr><tr><td valign="middle">BEFORE_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">BEFORE_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">INSTEAD_OF_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an INSTEAD OF section (YES) or not (NO)</td></tr><tr><td valign="middle">FIRE_ONCE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will fire only for user processes making changes (YES) or whether the trigger will also fire for Replication Apply or SQL Apply processes (NO)</td></tr><tr><td valign="middle">APPLY_SERVER_ONLY</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will only fire for a Replication Apply or SQL Apply process (YES) or not (NO). If set to YES, then the setting of FIRE_ONCE does not matter</td></tr><tr><td>COMMENTS</td><td>VARCHAR(1024)</td><td>Comment on the trigger</td></tr></tbody></table>

<a id="c9ebeb24cb4c390e"></a>
#### ALL_USERS

ALL_USERS lists all users of the database visible to the current user.

**Column 정보**

<a id="83378373ae02181c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">USERNAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">USER_ID</td><td align="left">NUMBER</td><td align="left">ID number of the user</td></tr><tr><td align="left">CREATED</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">User creation timestamp</td></tr></tbody></table>

<a id="590899e52ec43687"></a>
#### ALL_VIEWS

ALL_VIEWS describes the views accessible to the current user.

**Column 정보**

<a id="494f9ba1b33dd406"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="dd309963fe70929f"></a>
### DBA 계열 View

DBA 권한 (ACCESS CONTROL ON DATABASE)을 가지고 있는 현재 사용자의 모든 객체에 대한 정보를 얻을 수 있다.

<a id="088661857590d830"></a>
#### DBA_ALL_TABLES

DBA_ALL_TABLES describes all object tables and relational tables in the database.

**Column 정보**

<a id="74430f7deaab2369"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="4b893a592dadfc92"></a>
#### DBA_ARGUMENTS

DBA_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="f14b0534c5f30749"></a>
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
| DATA_TYPE | VARCHAR(128) | Data Type of the argument |
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

<a id="57f050cdba4d2a80"></a>
#### DBA_CATALOG

DBA_CATALOG lists all tables, views, synonyms, and sequences in the database.

**Column 정보**

<a id="92fb3425c6712e51"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="34859817c75d1b71"></a>
#### DBA_CLUSTER

DBA_CLUSTER describes all cluster members in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="1d25cd41661e04d4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GROUP_ID</td><td align="left">NUMBER</td><td align="left">Group identifier of the cluster member</td></tr><tr><td align="left">GROUP_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Group name of the cluster member</td></tr><tr><td align="left">MEMBER_ID</td><td align="left">NUMBER</td><td align="left">Member identifier of the cluster member</td></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Member name of the cluster member</td></tr><tr><td align="left">MEMBER_HOST</td><td align="left">VARCHAR(256)</td><td align="left">Host name or IP address of the cluster member</td></tr><tr><td align="left">MEMBER_PORT</td><td align="left">NUMBER</td><td align="left">Port number of the cluster member</td></tr><tr><td>MEMBER_POSITION</td><td>NUMBER</td><td>Member position number of the cluster member</td></tr></tbody></table>

<a id="d9c49ab318fc6008"></a>
#### DBA_CLUSTER_COMMENTS

DBA_CLUSTER_COMMENTS displays comments on the cluster objects in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="19a391744f7bd7b4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the cluster object</td></tr><tr><td align="left">OBJECT_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the cluster object: CLUSTER GROUP, CLUSTER MEMBER</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the cluster object</td></tr></tbody></table>

<a id="8d4a3611a47b21fd"></a>
#### DBA_CLUSTER_TABLES

DBA_CLUSTER_TABLES describes all cluster tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="24d7efd3c0db4129"></a>
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

<a id="1065ef2d2eb85000"></a>
#### DBA_COL_COMMENTS

DBA_COL_COMMENTS displays comments on the columns of all tables and views in the database.

**Column 정보**

<a id="d1be45bc07914686"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="4d405df025d9c048"></a>
#### DBA_COL_PRIVS

DBA_COL_PRIVS describes all column object grants in the database.

**Column 정보**

<a id="c947b42bf982dd60"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">CHARACTER VARYING(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">CHARACTER VARYING(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="15c248dc7cba08c8"></a>
#### DBA_CONSTRAINTS

DBA_CONSTRAINTS describes all constraint definitions on all tables in the database.

**Column 정보**

<a id="5cc3e20d23352627"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td valign="middle">DROPPED</td><td valign="middle">VARCHAR(3)</td><td>Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="9a0786de534b2011"></a>
#### DBA_CONS_COLUMNS

DBA_CONS_COLUMNS describes all columns in the database that are specified in constraints.

**Column 정보**

<a id="6f2721d8b2d671c0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="cfa629575bc9f5af"></a>
#### DBA_DB_PRIVS

DBA_DB_PRIVS describes all database grants in the database.

**Column 정보**

<a id="349a107cf66bb0d0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the database</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="18b46084a111d309"></a>
#### DBA_DEPENDENCIES

DBA_DEPENDENCIES describes all dependencies between objects in the database

**Column 정보**

<a id="0a4c0dc278a54331"></a>
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

<a id="3ab0f1e5c449a3e5"></a>
#### DBA_EXTENTS

DBA_EXTENTS describes the extents comprising the segments in all tablespaces in the database.

**Column 정보**

<a id="efa35a471e780e9e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Extent number in the segment</td></tr><tr><td align="left" valign="middle">FILE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;File identifier number of the file containing the extent</td></tr><tr><td align="left" valign="middle">BLOCK_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Starting block number of the extent</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr><tr><td align="left" valign="middle">RELATIVE_FNO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Relative file number of the first extent block</td></tr></tbody></table>

<a id="833e7aca5fd6e05f"></a>
#### DBA_GLOBAL_SECONDARY_INDEXES

DBA_GLOBAL_SECONDARY_INDEXES describes all global secondary indexes in the database.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="49ef71c5d3c08d6e"></a>
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

<a id="b4b86cf251cfbfa0"></a>
#### DBA_GSI_PLACE

DBA_GSI_PLACE describes node placement of all global secondary indexes in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="af64303e4f316174"></a>
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

<a id="09c3d6ca433f6967"></a>
#### DBA_HISTOGRAM_BALANCE

DBA_HISTOGRAM_BALANCE describes each height-balanced histogram bucket.

**Column 정보**

<a id="7b33b38ee650ae58"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of height-balanced histogram |
| BUCKET_ACCU_HEIGHT | NUMBER | Accumulated height of the height-balanced histogram bucket |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="dff4e7fbc504613c"></a>
#### DBA_HISTOGRAM_FREQUENCY

DBA_HISTOGRAM_FREQUENCY describes each frequency histogram bucket.

**Column 정보**

<a id="92760ba8549a487c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of frequency histogram |
| BUCKET_HEIGHT | NUMBER | Bucket height of the frequency histogram bucket |
| SAMPLE_COUNT | NUMBER | Sample count of frequency histogram |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="ed5aaba4a0d4ea61"></a>
#### DBA_INDEXES

DBA_INDEXES describes all indexes in the database.

**Column 정보**

<a id="b94cdb6d8bbb0e0b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or DISABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="0a65b8b42534a0ff"></a>
#### DBA_IND_COLUMNS

DBA_IND_COLUMNS describes the columns of all the indexes on all tables and clusters in the database.

**Column 정보**

<a id="d272499201da809e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="881c38b1051a6602"></a>
#### DBA_IND_PLACE

DBA_IND_PLACE describes node placement of all indexes in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="1c1072b241f3dbee"></a>
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

<a id="fe133756d9523ec8"></a>
#### DBA_LIBRARIES

DBA_LIBRARIES describes all libraries in the database.

**Column 정보**

<a id="10268233e42e084a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of Library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema Name of Library |
| LIBRARY_NAME | VARCHAR(128) | Name of Library |
| FILE_SPEC | LONG VARCHAR | Operating system file specification associated with the library |
| DYNAMIC | VARCHAR(1) | Indicates whether the library is dynamically loadable (Y) or not (N) |
| STATUS | VARCHAR(32) | Status of the library : the value in ( VALID, INVALID, N/A ) |
| AGENT | VARCHAR(128) | Agent of the library |
| LEAF_FILENAME | VARCHAR(4000) | Leaf filename of the library |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |
| COMMENTS | VARCHAR(1024) | Comment on the library |

<a id="c45ee9ed4bd8719b"></a>
#### DBA_LIBRARY_PRIVS

DBA_LIBRARY_PRIVS describes all library grants in the database.

**Column 정보**

<a id="42e7ebb46a393d3a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="d8ae3fe6779c1bf5"></a>
#### DBA_NONSCHEMA_COMMENTS

DBA_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces).

**Column 정보**

<a id="fda4496ac6c93906"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the non-schema object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the non-schema object: DATABASE, PROFILE, AUTHORIZATION, SCHEMA, TABLESPACE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the non-schema object</td></tr></tbody></table>

<a id="e37b2b65f0cd7723"></a>
#### DBA_OBJECTS

DBA_OBJECTS describes all objects in the database.

**Column 정보**

<a id="89822680b99c0321"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the edition in which the object is actual</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="2141e701f688f02e"></a>
#### DBA_PACKAGE_PRIVS

DBA_PACKAGE_PRIVS describes all packages grants in the database.

**Column 정보**

<a id="860c3c11ed99ca43"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="69419c086f5ebac5"></a>
#### DBA_PROCEDURES

DBA_PROCEDURES lists all function, procedures or package

**Column 정보**

<a id="090c77579ca2d0cc"></a>
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

<a id="ab66aa2a233c418b"></a>
#### DBA_PROC_PRIVS

DBA_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="06813b4307f61053"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="74bb0ea3a7701c39"></a>
#### DBA_PROFILES

DBA_PROFILES displays all profiles and their limits.

**Column 정보**

<a id="72347894379350cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROFILE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Profile name</td></tr><tr><td align="left" valign="middle">RESOURCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Resource name</td></tr><tr><td align="left" valign="middle">RESOURCE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the resource profile is a KERNEL or a PASSWORD parameter</td></tr><tr><td align="left" valign="middle">LIMIT_VALUE</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Limit placed on this resource for this profile</td></tr><tr><td align="left" valign="middle">COMMON</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether a given profile is common. (YES or NO)</td></tr></tbody></table>

<a id="61b59006802a5dc5"></a>
#### DBA_RECYCLEBIN

DBA_RECYCLEBIN describes all recycle bins in the database.

**Column 정보**

<a id="653eff52e38e5217"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema name of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">ORIGINAL_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Original name of the object</td></tr><tr><td align="left" valign="middle">OPERATION</td><td valign="middle">VARCHAR(4)</td><td valign="middle">Operation carried out on the object</td></tr><tr><td valign="middle">OBJECT_TYPE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Type of the object</td></tr><tr><td valign="middle">TABLESPACE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the tablespace containing the object</td></tr><tr><td valign="middle">CREATED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Created time of the object</td></tr><tr><td valign="middle">DROPPED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Dropped time of the object</td></tr><tr><td valign="middle">DROP_SCN</td><td valign="middle">VARCHAR(128)</td><td valign="middle">System change number (SCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_GCN</td><td valign="middle">NUMBER</td><td valign="middle">Global change number (GCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_DCN</td><td valign="middle">NUMBER</td><td valign="middle">Domain change number (DCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_LCN</td><td valign="middle">NUMBER</td><td valign="middle">Local change number (LCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">CAN_UNDROP</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be undropped (YES) or not (NO)</td></tr><tr><td valign="middle">CAN_PURGE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be purged (YES) or not (NO)</td></tr><tr><td valign="middle">BASE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number of the base object</td></tr><tr><td valign="middle">PURGE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number for the object which gets purged</td></tr></tbody></table>

<a id="18c475b2ae70e7f4"></a>
#### DBA_ROLES

DBA_ROLES describes all roles in the database.

**Column 정보**

<a id="d27d5987d77506bb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">ROLE_ID</td><td valign="middle">NUMBER</td><td valign="middle">ID number of the role</td></tr><tr><td valign="middle">PASSWORD_REQUIRED</td><td valign="middle">VARCHAR(8)</td><td valign="middle">This column is deprecated in favor of the AUTHENTICATION_TYPE column</td></tr><tr><td valign="middle">AUTHENTICATION_TYPE</td><td valign="middle">VARCHAR(4)</td><td valign="middle">Indicates the authentication mechanism for the role</td></tr><tr><td valign="middle">COMMON</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether a given role is common. (YES or NO)</td></tr><tr><td valign="middle">IS_BUILTIN</td><td valign="middle">VARCHAR(1)</td><td valign="middle">Denotes whether the role was created, and is maintained, by GOLDILOCKS.</td></tr><tr><td valign="middle">INHERITED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role was inherited from another container (YES) or not (NO)</td></tr><tr><td valign="middle">IMPLICIT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role is a common role created by an implicit application (YES) or not (NO)</td></tr><tr><td valign="middle">EXTERNAL_NAME</td><td valign="middle">VARCHAR(4000)</td><td valign="middle">For a global role, the external name refers to the DN of a group from a directory service that is mapped to the global role. This is not applicable to a local role.</td></tr></tbody></table>

<a id="73ae5fee2af31c6b"></a>
#### DBA_ROLE_PRIVS

DBA_ROLE_PRIVS describes the roles granted to all users and roles in the database.

**Column 정보**

<a id="fd54f17b55af4c13"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">GRANTEE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the user or role receiving the grant</td></tr><tr><td valign="middle">GRANTED_ROLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Granted role name</td></tr><tr><td valign="middle">ADMIN_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the ADMIN OPTION (YES) or not (NO)</td></tr><tr><td valign="middle">DELEGATE_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the DELEGATE OPTION (YES) or not (NO)</td></tr><tr><td valign="middle">DEFAULT_ROLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role is designated as a DEFAULT ROLE for the user (YES) or not (NO)</td></tr><tr><td valign="middle">COMMON</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates how the grant was made. (YES or NO)</td></tr><tr><td valign="middle">INHERITED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role grant was inherited from another container (YES) or not (NO)</td></tr></tbody></table>

<a id="ad04940da4040f07"></a>
#### DBA_SCHEMAS

Identify the schemata in the database.

**Column 정보**

<a id="d5d9e5fcf4b8783c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="444bef24262ea72e"></a>
#### DBA_SCHEMA_PATH

DBA_SCHEMA_PATH describes the schema search order of all authorizations in the database.

**Column 정보**

<a id="442a06a8fe811530"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the authorization</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the authorization</td></tr></tbody></table>

<a id="0fd1bbdabd3e3cae"></a>
#### DBA_SCHEMA_PRIVS

DBA_SCHEMA_PRIVS describes all schema grants in the database.

**Column 정보**

<a id="766f66cbec8ef9be"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="239feaeeb5409f9a"></a>
#### DBA_SEQUENCES

DBA_SEQUENCES describes all sequences in the database.

**Column 정보**

<a id="9351beb20bd5deaf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="18051f3feff82f28"></a>
#### DBA_SEQ_PRIVS

DBA_SEQ_PRIVS describes all sequence grants in the database.

**Column 정보**

<a id="e6e81f7ae00af126"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="8ce9e7b854067a4e"></a>
#### DBA_SHARD_KEY_COLUMNS

DBA_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="0c9b923d21285821"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="ae46dec62eb2e1f2"></a>
#### DBA_SOURCE

DBA_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="598e86cba4ab822c"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="6caac999753f88dc"></a>
#### DBA_STAT_COLUMN_GROUP

DBA_STAT_COLUMN_GROUP describes each column group statistics.

**Column 정보**

<a id="bcb1f01313f51f37"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| STAT_NAME | VARCHAR(128) | Statistics name |
| COLUMN_GROUPS | VARCHAR(1024) | Column names of the column group statistics |
| NUM_DISTINCT | NUMBER | Number of distinct values in the column group statistics |
| SAMPLE_SIZE | NUMBER | Sample size used in analyzing this column group statistics |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | Date on which this column group statistics was most recently analyzed |

<a id="da80dc1b28a36974"></a>
#### DBA_STAT_SYSTEM

DBA_STAT_SYSTEM describes analyzed system statistics.

**Column 정보**

<a id="c009423a8785f018"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CPU_OPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">OPS(operations per second) of CPU</td></tr><tr><td align="left" valign="middle">NETWORK_IOPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">IOPS(I/O operations per second) of Cluster NETWORK</td></tr><tr><td align="left" valign="middle">NETWORK_BUFSIZE</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">buffer size of Cluster NETWORK when analyzed</td></tr><tr><td valign="middle">BUFFER_MISS_PERCENT</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">disk buffer miss percent</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="0f896a3393720dd2"></a>
#### DBA_SYS_PRIVS

DBA_SYS_PRIVS describes all system (database, tablespace, schema) privileges in the database.

**Column 정보**

<a id="d860e2e3328c45c8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the grantee</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="3b2326d15cdf01f0"></a>
#### DBA_SYNONYMS

DBA_SYNONYMS describes all synonyms in the database.

**Column 정보**

<a id="f1e2c4ddb9c44fe4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="35efdb8e7ddeb700"></a>
#### DBA_TABLES

DBA_TABLES describes all relational tables in the database.

**Column 정보**

<a id="cf1d18489a26b00b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="2bea4d928c8a3a09"></a>
#### DBA_TABLESPACES

DBA_TABLESPACES describes all tablespaces in the database.

**Column 정보**

<a id="e3e983d86064e80b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">PLUGGED_IN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is plugged in (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="4623d8ca747d2d34"></a>
#### DBA_TAB_COLS

DBA_TAB_COLS describes the columns (including hidden columns) of all tables, views, and clusters in the database.

**Column 정보**

<a id="c59299e687ecc851"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="3817d436751014ef"></a>
#### DBA_TAB_COLUMNS

DBA_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="f61738f2d4dcbb3c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="03869debcb0323bb"></a>
#### DBA_TAB_COMMENTS

DBA_TAB_COMMENTS displays comments on all tables and views in the database.

**Column 정보**

<a id="010c363f69d6d3c9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="877ac16662d4885e"></a>
#### DBA_TAB_IDENTITY_COLS

DBA_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="950a09021e8e2acd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="baba25ebffca026c"></a>
#### DBA_TAB_PLACE

DBA_TAB_PLACE describes node placement of all cluster tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="b1ccbbc7213e189c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td valign="middle">MEMBER_POSITION</td><td valign="middle">NUMBER</td><td valign="middle">Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td valign="middle">IS_UPDATE_MASTER</td><td valign="middle">BOOLEAN</td><td valign="middle">whether the cluster member is update master or not</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="57adebf2b7d0814a"></a>
#### DBA_TAB_PRIVS

DBA_TAB_PRIVS describes all object grants in the database.

**Column 정보**

<a id="fe0c55ba37463309"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="57af98e528aae36a"></a>
#### DBA_TAB_SHARDS

DBA_TAB_SHARDS describes shard information of all sharded tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="c5cd84bdb0f4e009"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="c60cd336895d3b3b"></a>
#### DBA_TBS_PRIVS

DBA_TBS_PRIVS describes all tablespace grants in the database.

**Column 정보**

<a id="bb77ea6668a7c4c6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2faa31e61f2379f1"></a>
#### DBA_TRIGGERS

DBA_TRIGGERS describes all triggers in the database.

**Column 정보**

<a id="a6791014ccd067da"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the trigger</td></tr><tr><td valign="middle">TRIGGER_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">When the trigger fires: the value in ( BEFORE STATEMENT, BEFORE EACH ROW, AFTER STATEMENT, AFTER EACH ROW, INSTEAD OF, COMPOUND )</td></tr><tr><td valign="middle">TRIGGERING_EVENT</td><td valign="middle">VARCHAR(32)</td><td valign="middle">DML, DDL, or database event that fires the trigger</td></tr><tr><td valign="middle">TABLE_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the table on which the trigger is defined</td></tr><tr><td valign="middle">TABLE_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the table on which the trigger is defined</td></tr><tr><td valign="middle">BASE_OBJECT_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Base object on which the trigger is defined: the value in ( TABLE, VIEW, SCHEMA, DATABASE )</td></tr><tr><td valign="middle">TABLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">If the base object type of the trigger is SCHEMA or DATABASE, then this column is NULL; if the base object type of the trigger is TABLE or VIEW then this column indicates the table or view name on which the trigger is defined</td></tr><tr><td valign="middle">COLUMN_NAME</td><td valign="middle">VARCHAR(4000)</td><td valign="middle">Name of the nested table column (if a nested table trigger), else NULL</td></tr><tr><td valign="middle">REFERENCING_NAMES</td><td valign="middle">VARCHAR(1024)</td><td valign="middle">Names used for referencing OLD and NEW column values from within the trigger</td></tr><tr><td valign="middle">WHEN_CLAUSE</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Must evaluate to TRUE for TRIGGER_BODY to execute</td></tr><tr><td valign="middle">STATUS</td><td valign="middle">VARCHAR(8)</td><td valign="middle">Indicates whether the trigger is enabled (ENABLED) or disabled (DISABLED); a disabled trigger will not fire</td></tr><tr><td valign="middle">DESCRIPTION</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Trigger description; useful for re-creating a trigger creation statement</td></tr><tr><td valign="middle">ACTION_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Action type of the trigger body: the value in ( CALL, PSM BLOCK )</td></tr><tr><td valign="middle">TRIGGER_BODY</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Statements executed by the trigger when it fires</td></tr><tr><td valign="middle">CROSSEDITION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Type of crossedition trigger: the value in ( FORWARD, REVERSE, NO )</td></tr><tr><td valign="middle">BEFORE_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">BEFORE_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">INSTEAD_OF_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an INSTEAD OF section (YES) or not (NO)</td></tr><tr><td valign="middle">FIRE_ONCE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will fire only for user processes making changes (YES) or whether the trigger will also fire for Replication Apply or SQL Apply processes (NO)</td></tr><tr><td valign="middle">APPLY_SERVER_ONLY</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will only fire for a Replication Apply or SQL Apply process (YES) or not (NO). If set to YES, then the setting of FIRE_ONCE does not matter</td></tr><tr><td>COMMENTS</td><td>VARCHAR(1024)</td><td>Comment on the trigger</td></tr></tbody></table>

<a id="0f18c3f66c6e6cc3"></a>
#### DBA_USERS

DBA_USERS describes all users of the database.

**Column 정보**

<a id="adb0d14eec183b22"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">PASSWORD</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">encrypted password</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">FAILED_LOGIN_ATTEMPTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Consecutive failed login attempts count</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">PROFIL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">User resource profile name</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr><tr><td align="left" valign="middle">PASSWORD_VERSIONS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Shows the list of versions of the password hashes (verifiers).</td></tr><tr><td align="left" valign="middle">EDITIONS_ENABLED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether editions have been enabled for the corresponding user (Y) or not (N).</td></tr><tr><td align="left" valign="middle">AUTHENTICATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the authentication mechanism for the user.</td></tr></tbody></table>

<a id="ca2c6a20f9ebdf95"></a>
#### DBA_VIEWS

DBA_VIEWS describes all views in the database.

**Column 정보**

<a id="120eeafec6839b75"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="e92aa813ffe83928"></a>
### USER 계열 View

현재 사용자가 소유한 객체에 대한 정보를 얻을 수 있다.

<a id="e6e23cf6219e0431"></a>
#### USER_ALL_TABLES

USER_ALL_TABLES describes the object tables and relational tables owned by the current user.

**Column 정보**

<a id="b89b1c9858c63f68"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="7ec640710c7cae83"></a>
#### USER_ARGUMENTS

USER_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="d8f0e5b718f60ee7"></a>
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
| DATA_TYPE | VARCHAR(128) | Data Type of the argument |
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

<a id="38bf5731a76c748e"></a>
#### USER_CATALOG

USER_CATALOG lists tables, views, synonyms, and sequences owned by the current user.

**Column 정보**

<a id="f8b77775a4249d87"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="944c54436ef0dc0a"></a>
#### USER_COL_COMMENTS

USER_COL_COMMENTS displays comments on the columns of the tables and views owned by the current user.

**Column 정보**

<a id="07bfd25cb71a526f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="d1b5fa7839ebaa04"></a>
#### USER_CLUSTER_TABLES

USER_CLUSTER_TABLES describes all cluster tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="54c7eba83179574c"></a>
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

<a id="0bc364a2e15941c0"></a>
#### USER_COL_PRIVS

USER_COL_PRIVS describes the column object grants for which the current user is the object owner, grantor, or grantee.

**Column 정보**

<a id="eb0b1b9080d73866"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a07ce15aa176f8e5"></a>
#### USER_COL_PRIVS_MADE

USER_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner.

**Column 정보**

<a id="8131c2c395c48fd6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="8a84bb532f3dce16"></a>
#### USER_COL_PRIVS_RECD

USER_COL_PRIVS_RECD describes the column object grants for which the current user is the grantee.

**Column 정보**

<a id="d6fce4681ca93e7e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="13d5969d5f1a63cb"></a>
#### USER_CONSTRAINTS

USER_CONSTRAINTS describes all constraint definitions on tables owned by the current user.

**Column 정보**

<a id="125c90db388f90d5"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the constraint has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="a2ca9175a2f78f0d"></a>
#### USER_CONS_COLUMNS

USER_CONS_COLUMNS describes columns that are owned by the current user and that are specified in constraint definitions.

**Column 정보**

<a id="eb5069c8b61b60ab"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="0a2af32e1b1e4f2f"></a>
#### USER_DEPENDENCIES

USER_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column 정보**

<a id="07f9d41c868b3d4a"></a>
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

<a id="a193b1ed79a70d4b"></a>
#### USER_EXTENTS

USER_EXTENTS describes the extents comprising the segments owned by the current user's objects.

**Column 정보**

<a id="e24a136a9dc2dacf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Extent number in the segment</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr></tbody></table>

<a id="0b82bd1aa969c893"></a>
#### USER_GLOBAL_SECONDARY_INDEXES

USER_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables owned by the current user.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="58acf06bf6774cd2"></a>
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

<a id="5593d434701072ba"></a>
#### USER_GSI_PLACE

USER_GSI_PLACE describes node placement of all global secondary indexes on the tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="c5be7b070025bab5"></a>
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

<a id="267df225b64b2f0d"></a>
#### USER_HISTOGRAM_BALANCE

USER_HISTOGRAM_BALANCE describes each height-balanced histogram bucket owned by the current user.

**Column 정보**

<a id="5a623cb13e909dd9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of height-balanced histogram |
| BUCKET_ACCU_HEIGHT | NUMBER | Accumulated height of the height-balanced histogram bucket |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="c1c6f648a3e9c3c4"></a>
#### USER_HISTOGRAM_FREQUENCY

USER_HISTOGRAM_FREQUENCY describes each frequency histogram bucket owned by the current user.

**Column 정보**

<a id="f76d0aeb43abe435"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARACHAR(128) | Column name |
| BUCKET_NUMBER | NUMBER | Bucket number of frequency histogram |
| BUCKET_HEIGHT | NUMBER | Bucket height of the frequency histogram bucket |
| SAMPLE_COUNT | NUMBER | Sample count of frequency histogram |
| BUCKET_VALUE | VARCHAR(128) | Bucket value |

<a id="ddf11c72dd2b4f2b"></a>
#### USER_INDEXES

USER_INDEXES describes indexes owned by the current user.

**Column 정보**

<a id="7cea3da160cf29f1"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">ndicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the index when most recently analyzed</td></tr><tr><td valign="middle">EMPTY_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of empty blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or DISABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="eeb10ac356a7cd09"></a>
#### USER_IND_COLUMNS

USER_IND_COLUMNS describes the columns of the indexes owned by the current user and columns of indexes on tables owned by the current user.

**Column 정보**

<a id="c0cf82521bd0fcb2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="db2ad3eea4d9e043"></a>
#### USER_IND_PLACE

USER_IND_PLACE describes node placement of the indexes owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="095a2eb8d99a9de1"></a>
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

<a id="68259f0728c9d8db"></a>
#### USER_LIBRARIES

USER_LIBRARIES describes the libraries owned by the current user.

**Column 정보**

<a id="7cd9714bb097d7c9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema Name of Library |
| LIBRARY_NAME | VARCHAR(128) | Name of Library |
| FILE_SPEC | LONG VARCHAR | Operating system file specification associated with the library |
| DYNAMIC | VARCHAR(1) | Indicates whether the library is dynamically loadable (Y) or not (N) |
| STATUS | VARCHAR(32) | Status of the library : the value in ( VALID, INVALID, N/A ) |
| AGENT | VARCHAR(128) | Agent of the library |
| LEAF_FILENAME | VARCHAR(4000) | Leaf filename of the library |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |
| COMMENTS | VARCHAR(1024) | Comment on the library |

<a id="011adb422490cceb"></a>
#### USER_LIBRARY_PRIVS

USER_LIBRARY_PRIVS describes the library grants for which the current user is the library owner, grantor, or grantee.

**Column 정보**

<a id="48ed918a3b9289ae"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="64751101e6ed0d23"></a>
#### USER_LIBRARY_PRIVS_MADE

USER_LIBRARY_PRIVS_MADE describes the library grants for which the current user is the library owner.

**Column 정보**

<a id="120ddb3f9b3d02ae"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="2159518323a3b7fa"></a>
#### USER_LIBRARY_PRIVS_RECD

USER_LIBRARY_PRIVS_RECD describes the library grants for which the current user is the grantee.

**Column 정보**

<a id="c8a37e974e266994"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| LIBRARY_OWNER | VARCHAR(128) | Owner of the library |
| LIBRARY_SCHEMA | VARCHAR(128) | Schema of the library |
| LIBRARY_NAME | VARCHAR(128) | Name of the library |
| PRIVILEGE | VARCHAR(32) | Privilege on the library |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="57cf3544374b0397"></a>
#### USER_OBJECTS

USER_OBJECTS describes all objects owned by the current user.

**Column 정보**

<a id="29a265e901b6f9ae"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="09b24ba1c7e135c3"></a>
#### USER_PACKAGE_PRIVS

USER_PACKAGE_PRIVS describes the package grants for which the current user is the package owner, grantor, or grantee.

**Column 정보**

<a id="8f0509ff58203dd3"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="da5391bbec901d8e"></a>
#### USER_PACKAGE_PRIVS_MADE

USER_PACKAGE_PRIVS_MADE describes the package grants for which the current user is the package owner.

**Column 정보**

<a id="43ca8aa6b2413784"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="5385c5c430363670"></a>
#### USER_PACKAGE_PRIVS_RECD

USER_PACKAGE_PRIVS_RECD describes the package grants for which the current user is the grantee.

**Column 정보**

<a id="5475be83fe18ceb9"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the package |
| PRIVILEGE | VARCHAR(32) | Privilege on the package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="e86fb98ed061563f"></a>
#### USER_PROCEDURES

USER_PROCEDURES lists of procedures owned by the current user.

**Column 정보**

<a id="55b415edd5b7acf1"></a>
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

<a id="7ef104867e0394d2"></a>
#### USER_PROC_PRIVS

USER_PROC_PRIVS describes the procedure grants for which the current user is the procedure owner, grantor, or grantee.

**Column 정보**

<a id="01562701c4c293be"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="b1f674966d1ffa0a"></a>
#### USER_PROC_PRIVS_MADE

USER_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column 정보**

<a id="f830485f1a53566d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="1d9fc955816e537a"></a>
#### USER_PROC_PRIVS_RECD

USER_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="09b8ba6e741dd249"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure and function |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure and function |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure and function |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure and function |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="11646427cdb17e1a"></a>
#### USER_RECYCLEBIN

USER_RECYCLEBIN describes recycle bins owned by the current user.

**Column 정보**

<a id="34abc2777ea841cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema name of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">ORIGINAL_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Original name of the object</td></tr><tr><td align="left" valign="middle">OPERATION</td><td valign="middle">VARCHAR(4)</td><td valign="middle">Operation carried out on the object</td></tr><tr><td valign="middle">OBJECT_TYPE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Type of the object</td></tr><tr><td valign="middle">TABLESPACE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the tablespace containing the object</td></tr><tr><td valign="middle">CREATED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Created time of the object</td></tr><tr><td valign="middle">DROPPED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">Dropped time of the object</td></tr><tr><td valign="middle">DROP_SCN</td><td valign="middle">VARCHAR(128)</td><td valign="middle">System change number (SCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_GCN</td><td valign="middle">NUMBER</td><td valign="middle">Global change number (GCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_DCN</td><td valign="middle">NUMBER</td><td valign="middle">Domain change number (DCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">DROP_LCN</td><td valign="middle">NUMBER</td><td valign="middle">Local change number (LCN) of the transaction which moved the object to the recycle bin</td></tr><tr><td valign="middle">CAN_UNDROP</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be undropped (YES) or not (NO)</td></tr><tr><td valign="middle">CAN_PURGE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the object can be purged (YES) or not (NO)</td></tr><tr><td valign="middle">BASE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number of the base object</td></tr><tr><td valign="middle">PURGE_OBJECT</td><td valign="middle">NUMBER</td><td valign="middle">Object number for the object which gets purged</td></tr></tbody></table>

<a id="f5acc6f79a1ec982"></a>
#### USER_ROLE_PRIVS

USER_ROLE_PRIVS describes the roles granted to the current user.

**Column 정보**

<a id="749ebdff234c887e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">USERNAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the user, or PUBLIC</td></tr><tr><td valign="middle">GRANTED_ROLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role granted to the user</td></tr><tr><td valign="middle">ADMIN_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the ADMIN OPTION (YES) or not (NO)</td></tr><tr><td valign="middle">DELEGATE_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the DELEGATE OPTION (YES) or not (NO)</td></tr><tr><td valign="middle">DEFAULT_ROLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role is designated as a DEFAULT ROLE for the user (YES) or not (NO)</td></tr><tr><td valign="middle">OS_GRANTED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role was granted by the operating system (YES) or not (NO); occurs if the OS_ROLES initialization parameter is true</td></tr><tr><td valign="middle">COMMON</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates how the grant was made. (YES or NO)</td></tr><tr><td valign="middle">INHERITED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role grant was inherited from another container (YES) or not (NO)</td></tr></tbody></table>

<a id="ca406172d39cecd5"></a>
#### USER_SCHEMAS

Identify the schemata in a catalog that are owned by current user.

**Column 정보**

<a id="d9d29e36773dac58"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="daf7825280e49c87"></a>
#### USER_SCHEMA_PATH

USER_SCHEMA_PATH describes the schema search order of the current user, for naming resolution of unqualified SQL schema objects.

**Column 정보**

<a id="10c2f01f2b8ae63c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the user</td></tr></tbody></table>

<a id="df14c72d989fbfbe"></a>
#### USER_SCHEMA_PRIVS

USER_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee.

**Column 정보**

<a id="d73dec37f097b4f5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="72e0a5b716fd2369"></a>
#### USER_SCHEMA_PRIVS_MADE

USER_SCHEMA_PRIVS_MADE describes the schema grants for which the current user is the schema owner.

**Column 정보**

<a id="7101bd8de9db222f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="d73c26e9d1209f62"></a>
#### USER_SCHEMA_PRIVS_RECD

USER_SCHEMA_PRIVS_RECD describes the schema grants for which the current user is the grantee.

**Column 정보**

<a id="dbf41433bebf5516"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ef722d1d917f3872"></a>
#### USER_SEQUENCES

USER_SEQUENCES describes all sequences owned by the current user.

**Column 정보**

<a id="785147d360a93c00"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="292fa980ccc13df8"></a>
#### USER_SEQ_PRIVS

USER_SEQ_PRIVS describes the sequence grants for which the current user is the sequence owner, grantor, or grantee.

**Column 정보**

<a id="3141b34a73f3ce10"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="7c30f643f5fdf632"></a>
#### USER_SEQ_PRIVS_MADE

USER_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner.

**Column 정보**

<a id="0124c83790800897"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a75b08c54d3aea5c"></a>
#### USER_SEQ_PRIVS_RECD

USER_SEQ_PRIVS_RECD describes the sequence grants for which the current user is the grantee.

**Column 정보**

<a id="647860618fc88585"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="e8e0d8570ab61ce8"></a>
#### USER_SHARD_KEY_COLUMNS

USER_SHARD_KEY_COLUMNS describes shard key columns of shareded tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="be69b76c04a5f832"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="1e6fe98e39d570ce"></a>
#### USER_SOURCE

USER_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="baa230dc2219156d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="727b6bec662b5d50"></a>
#### USER_STAT_COLUMN_GROUP

USER_STAT_COLUMN_GROUP describes each column group statistics owned by the current user.

**Column 정보**

<a id="a300aaf176733b7e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| STAT_NAME | VARCHAR(128) | Statistics name |
| COLUMN_GROUPS | VARCHAR(1024) | Column names of the column group statistics |
| NUM_DISTINCT | NUMBER | Number of distinct values in the column group statistics |
| SAMPLE_SIZE | NUMBER | Sample size used in analyzing this column group statistics |
| LAST_ANALYZED | TIMESTAMP(6) WITHOUT TIME ZONE | Date on which this column group statistics was most recently analyzed |

<a id="00329453f6e68e9a"></a>
#### USER_SYNONYMS

USER_SYNONYMS describes all synonyms owned by the current user.

**Column 정보**

<a id="ca63fbd317c4fd26"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="6092b9d904f01e02"></a>
#### USER_SYS_PRIVS

USER_SYS_PRIVS describes system (database, tablespace, schema) privileges granted to the current user or PUBLIC.

**Column 정보**

<a id="c00eee69340ca9b4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user, or PUBLIC</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="8bb75376c97a3a2c"></a>
#### USER_TABLES

USER_TABLES describes the relational tables owned by the current user.

**Column 정보**

<a id="5308bdd23190da5c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td valign="middle">ANAL_BLOCKS</td><td valign="middle">NUMBER</td><td valign="middle">Number of used blocks in the table when most recently analyzed</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td>Indicates the duration of a temporary table, the value is in ( TRANSACTION, SESSION )</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td valign="middle">IS_IMMUTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the table IS IMMUTABLE (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="0cddbb87c26f11d0"></a>
#### USER_TABLESPACES

USER_TABLESPACES describes the tablespaces accessible to the current user.

**Column 정보**

<a id="afd9e88be2ce1004"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="9764f65d709e5b40"></a>
#### USER_TAB_COLS

USER_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters owned by the current user.

**Column 정보**

<a id="4ad51d41297bfc48"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="0ab36400f75b86cc"></a>
#### USER_TAB_COLUMNS

USER_TAB_COLUMNS describes the columns of the tables, views, and clusters owned by the current user.

**Column 정보**

<a id="f8de9d103faf14e0"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="6c39a1284d5d78aa"></a>
#### USER_TAB_COMMENTS

USER_TAB_COMMENTS displays comments on the tables and views owned by the current user.

**Column 정보**

<a id="364e7617adb56775"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="e3806fc6fe054b34"></a>
#### USER_TAB_IDENTITY_COLS

USER_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="13b43fee8682a4f6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="b67aa92422af69df"></a>
#### USER_TAB_PLACE

USER_TAB_PLACE describes node placement of cluster tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="e77ed3da804e730e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td valign="middle">MEMBER_POSITION</td><td valign="middle">NUMBER</td><td valign="middle">Member position of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td valign="middle">IS_UPDATE_MASTER</td><td valign="middle">BOOLEAN</td><td valign="middle">whether the cluster member is update master or not</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="2d8c275e39bc5dbd"></a>
#### USER_TAB_PRIVS

USER_TAB_PRIVS describes the object grants for which the current user is the object owner, grantor, or grantee.

**Column 정보**

<a id="622fdcb16a3631f6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="c3207957b4096eda"></a>
#### USER_TAB_PRIVS_MADE

USER_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner.

**Column 정보**

<a id="27f3bac543e8ccf3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="d4c68fabc3d8342f"></a>
#### USER_TAB_PRIVS_RECD

USER_TAB_PRIVS_RECD describes the object grants for which the current user is the grantee.

**Column 정보**

<a id="3f2a7db73a9c4445"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a63f133713822434"></a>
#### USER_TAB_SHARDS

USER_TAB_SHARDS describes shard information of sharded tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="81d9a013e1134517"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="da4c6f4ef1c163db"></a>
#### USER_TRIGGERS

USER_TRIGGERS describes the triggers owned by the current user.

**Column 정보**

<a id="67458839a663f1bd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">TRIGGER_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the trigger</td></tr><tr><td valign="middle">TRIGGER_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">When the trigger fires: the value in ( BEFORE STATEMENT, BEFORE EACH ROW, AFTER STATEMENT, AFTER EACH ROW, INSTEAD OF, COMPOUND )</td></tr><tr><td valign="middle">TRIGGERING_EVENT</td><td valign="middle">VARCHAR(32)</td><td valign="middle">DML, DDL, or database event that fires the trigger</td></tr><tr><td valign="middle">TABLE_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the table on which the trigger is defined</td></tr><tr><td valign="middle">TABLE_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema Name of the table on which the trigger is defined</td></tr><tr><td valign="middle">BASE_OBJECT_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Base object on which the trigger is defined: the value in ( TABLE, VIEW, SCHEMA, DATABASE )</td></tr><tr><td valign="middle">TABLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">If the base object type of the trigger is SCHEMA or DATABASE, then this column is NULL; if the base object type of the trigger is TABLE or VIEW then this column indicates the table or view name on which the trigger is defined</td></tr><tr><td valign="middle">COLUMN_NAME</td><td valign="middle">VARCHAR(4000)</td><td valign="middle">Name of the nested table column (if a nested table trigger), else NULL</td></tr><tr><td valign="middle">REFERENCING_NAMES</td><td valign="middle">VARCHAR(1024)</td><td valign="middle">Names used for referencing OLD and NEW column values from within the trigger</td></tr><tr><td valign="middle">WHEN_CLAUSE</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Must evaluate to TRUE for TRIGGER_BODY to execute</td></tr><tr><td valign="middle">STATUS</td><td valign="middle">VARCHAR(8)</td><td valign="middle">Indicates whether the trigger is enabled (ENABLED) or disabled (DISABLED); a disabled trigger will not fire</td></tr><tr><td valign="middle">DESCRIPTION</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Trigger description; useful for re-creating a trigger creation statement</td></tr><tr><td valign="middle">ACTION_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">Action type of the trigger body: the value in ( CALL, PSM BLOCK )</td></tr><tr><td valign="middle">TRIGGER_BODY</td><td valign="middle">LONG VARCHAR</td><td valign="middle">Statements executed by the trigger when it fires</td></tr><tr><td valign="middle">CROSSEDITION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Type of crossedition trigger: the value in ( FORWARD, REVERSE, NO )</td></tr><tr><td valign="middle">BEFORE_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">BEFORE_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has a BEFORE EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER EACH ROW section (YES) or not (NO)</td></tr><tr><td valign="middle">AFTER_STATEMENT</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an AFTER STATEMENT section (YES) or not (NO)</td></tr><tr><td valign="middle">INSTEAD_OF_ROW</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger has an INSTEAD OF section (YES) or not (NO)</td></tr><tr><td valign="middle">FIRE_ONCE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will fire only for user processes making changes (YES) or whether the trigger will also fire for Replication Apply or SQL Apply processes (NO)</td></tr><tr><td valign="middle">APPLY_SERVER_ONLY</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the trigger will only fire for a Replication Apply or SQL Apply process (YES) or not (NO). If set to YES, then the setting of FIRE_ONCE does not matter</td></tr><tr><td>COMMENTS</td><td>VARCHAR(1024)</td><td>Comment on the trigger</td></tr></tbody></table>

<a id="6cc56912e3a2f8fb"></a>
#### USER_USERS

USER_USERS describes the current user.

**Column 정보**

<a id="41ad7769bc3e3552"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr></tbody></table>

<a id="868da788f00d7653"></a>
#### USER_VIEWS

USER_VIEWS describes the views owned by the current user.

**Column 정보**

<a id="1ab15958187f57ac"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="344552816857df3b"></a>
### 기타 View

ALL 계열이나 DBA 계열, USER 계열이 아닌 view나 테이블이다.

<a id="bcc03d54474ebf70"></a>
#### AUDIT_POLICIES

AUDIT_POLICIES contains one row for each audit policy.

**Column 정보**

<a id="ca3daf710b9814c8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enabled (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the audit policy</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the audit policy</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the audit policy</td></tr></tbody></table>

<a id="24211623ebe3ca8c"></a>
#### AUDIT_POLICY_OPTIONS

AUDIT_POLICY_OPTIONS describes all audit policies created in the database.

**Column 정보**

<a id="55a6518f5b9be1f7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">auditing option defined in the audit policy</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">The values of AUDIT_OPTION_TYPE_NAME in ( 'DATABASE PRIVILEGE', 'SYSTEM ACTION', 'OBJECT ACTION' )</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">object type name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="a0b1425590db4566"></a>
#### AUDIT_POLICY_ENABLED

AUDIT_POLICY_ENABLE describes all the audit policies that are enable in the database.

**Column 정보**

<a id="1ae32c0a09546c2f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED_OPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">enable option of the audit policy, the possible values are BY, EXCEPT</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name for whom the audit policy is enable</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="28a87ad95b910b03"></a>
#### AUDIT_TRAIL

AUDIT_TRAIL displays audit records from the audit trail.

**Column 정보**

<a id="8c96260685c2d0aa"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MEMBER_NAME | VARCHAR(128) | cluster member name |
| SESSION_ID | NUMBER | session identifier |
| SESSION_SERIAL | NUMBER | session serial number |
| LOGON_USERNAME | VARCHAR(128) | logon user name of the user whose actions were audited |
| CURRENT_USERNAME | VARCHAR(128) | effective user for the statement execution |
| SERVER_PROCESS | NUMBER | server process identifier for the session |
| CLIENT_PROGRAM_NAME | VARCHAR(128) | client program used for session |
| CLIENT_USERNAME | VARCHAR(128) | client operating system user name for the session |
| CLIENT_PROCESS | NUMBER | client process identifier for the session |
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

<a id="eb7ff0d15b0bb013"></a>
#### DATABASE_PROPERTIES

DATABASE_PROPERTIES lists permanent database properties.

**Column 정보**

<a id="0834130d1c862783"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;PROPERTY_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Property name</td></tr><tr><td align="left">&nbsp;PROPERTY_VALUE</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property value</td></tr><tr><td align="left">&nbsp;DESCRIPTION</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property description</td></tr></tbody></table>

<a id="714cdd5270ca71cb"></a>
#### DBC_TABLE_TYPE_INFO

Identify the ODBC/JDBC table types available in this database.

**Column 정보**

<a id="d752d78522cfd493"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE_ID</td><td align="left">&nbsp;NUMBER</td><td align="left">&nbsp;number identifier of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;name of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;IS_SUPPORTED</td><td align="left">&nbsp;BOOLEAN</td><td align="left">&nbsp;is supported feature</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;comments of the table type</td></tr></tbody></table>

<a id="0d52195dbbfec410"></a>
#### DICTIONARY

DICTIONARY contains descriptions of data dictionary tables and views.

**Column 정보**

<a id="c373720c1be3e721"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;TABLE_SCHEMA</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Schema of the object</td></tr><tr><td align="left">&nbsp;TABLE_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Name of the object</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;Text comment on the object</td></tr></tbody></table>

<a id="2d2f6ce882a83be8"></a>
#### DICT_COLUMNS

DICT_COLUMNS contains descriptions of columns in data dictionary tables and views.

**Column 정보**

<a id="40292449c2158c9f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object that contains the column</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object that contains the column</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Text comment on the column</td></tr></tbody></table>

<a id="ba51407c95171b0c"></a>
#### DUAL

DUAL returns one row and one column.

**Column 정보**

<a id="fd5616e0862fc117"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| DUMMY | VARCHAR(1) | Dummy column |

<a id="5b8b001f0e7cc32b"></a>
#### GLOBAL_DUAL

GLOBAL_DUAL returns one row and one column in cluster environment.

**Column 정보**

<a id="1523994e82873904"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| DUMMY | VARCHAR(1) | Dummy column |

<a id="a037f6c2d14b02a0"></a>
#### IMPLEMENTATION_INFO

IMPLEMENTATION_INFO contains information about various aspects that are left implementation-defined.

**Column 정보**

<a id="492227c5d28c20e9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">identifier of the implementation item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="e64d3e19020f3b20"></a>
#### IMPLEMENTATION_INFO_BASE

The IMPLEMENTATION_INFO_BASE table has one row for each implementation information item.

**Column 정보**

<a id="acb2664796766ebd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if the implementation item is supported, FALSE if not</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="826ab3ec8e4c4df3"></a>
#### JDBC_CLIENT_PROPS

JDBC_CLIENT_PROPS is the set of jdbc client properties.

**Column 정보**

<a id="70f9fddad0d64ade"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">property name</td></tr><tr><td align="left">MAX_LEN</td><td align="left">NATIVE_INTEGER</td><td align="left">max length of a value</td></tr><tr><td align="left">DEFAULT_VALUE</td><td align="left">VARCHAR(128)</td><td align="left">default value</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(256)</td><td align="left">descrption on that property</td></tr></tbody></table>

<a id="b41ef9135422a705"></a>
#### PRODUCT

PRODUCT is about the product name, version for ODBC, JDBC interface.

**Column 정보**

<a id="50fa51add66766fe"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(32)</td><td align="left">the product name</td></tr><tr><td align="left">VERSION</td><td align="left">VARCHAR(128)</td><td align="left">product full version information</td></tr><tr><td align="left">PRODUCT_VERSION</td><td align="left">NUMBER</td><td align="left">product version</td></tr><tr><td align="left">MAJOR_VERSION</td><td align="left">NUMBER</td><td align="left">major version</td></tr><tr><td align="left">MINOR_VERSION</td><td align="left">NUMBER</td><td align="left">minor version</td></tr><tr><td align="left">PATCH_VERSION</td><td align="left">NUMBER</td><td align="left">patch version</td></tr></tbody></table>

<a id="cb971b9e672523a4"></a>
#### ROLE_COL_PRIVS

ROLE_COL_PRIVS describes column privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="104f60171a310849"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>ROLE_NAME</td><td>VARCHAR(128)</td><td>Name of the role</td></tr><tr><td>TABLE_OWNER</td><td>VARCHAR(128)</td><td>Owner of the table</td></tr><tr><td>TABLE_SCHEMA</td><td>VARCHAR(128)</td><td>Schema of the table</td></tr><tr><td>TABLE_NAME</td><td>VARCHAR(128)</td><td>Name of the table</td></tr><tr><td>COLUMN_NAME</td><td>VARCHAR(128)</td><td>Name of the column</td></tr><tr><td>PRIVILEGE</td><td>VARCHAR(32)</td><td>Column privilege granted to the role</td></tr><tr><td>GRANTABLE</td><td>VARCHAR(3)</td><td>YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="acb5f5769893d030"></a>
#### ROLE_DB_PRIVS

ROLE_DB_PRIVS describes database privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="67efd355940776cc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Database privilege granted to the role</td></tr><tr><td valign="middle">GRANT_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the GRANT option (YES) or not (NO)</td></tr></tbody></table>

<a id="bd0a54d96c906072"></a>
#### ROLE_LIBRARY_PRIVS

ROLE_LIBRARY_PRIVS describes library privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="7fa56d5a9181e7eb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>ROLE_NAME</td><td>VARCHAR(128)</td><td>Name of the role</td></tr><tr><td>LIBRARY_OWNER</td><td>VARCHAR(128)</td><td>Owner of the library</td></tr><tr><td>LIBRARY_SCHEMA</td><td>VARCHAR(128)</td><td>Schema of the library</td></tr><tr><td>LIBRARY_NAME</td><td>VARCHAR(128)</td><td>Name of the library</td></tr><tr><td>PRIVILEGE</td><td>VARCHAR(32)</td><td>library privilege granted to the role</td></tr><tr><td>GRANTABLE</td><td>VARCHAR(3)</td><td>YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="dc87b0d3eaab2580"></a>
#### ROLE_PACKAGE_PRIVS

ROLE_PACKAGE_PRIVS describes package privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="7e2e18e5bdea1bd5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>ROLE_NAME</td><td>VARCHAR(128)</td><td>Name of the role</td></tr><tr><td>PACKAGE_OWNER</td><td>VARCHAR(128)</td><td>Owner of the package</td></tr><tr><td>PACKAGE_SCHEMA</td><td>VARCHAR(128)</td><td>Schema of the package</td></tr><tr><td>PACKAGE_NAME</td><td>VARCHAR(128)</td><td>Name of the package</td></tr><tr><td>PRIVILEGE</td><td>VARCHAR(32)</td><td>Package privilege granted to the role</td></tr><tr><td>GRANTABLE</td><td>VARCHAR(3)</td><td>YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="09d06287320caea3"></a>
#### ROLE_PROC_PRIVS

ROLE_PROC_PRIVS describes routine privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="2cf4bd5039363bec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">PROCEDURE_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the routine</td></tr><tr><td valign="middle">PROCEDURE_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema of the routine</td></tr><tr><td valign="middle">PROCEDURE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the routine</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Routine privilege granted to the role</td></tr><tr><td valign="middle">GRANTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="2404a08308b1e2c0"></a>
#### ROLE_ROLE_PRIVS

ROLE_ROLE_PRIVS describes the roles granted to other roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="2050e41119a38ee5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">GRANTED_ROLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Role that was granted</td></tr><tr><td valign="middle">ADMIN_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Signifies that the role was granted with ADMIN option</td></tr><tr><td valign="middle">COMMON</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates how the grant was made. (YES or NO)</td></tr><tr><td valign="middle">INHERITED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role grant was inherited from another container (YES) or not (NO)</td></tr></tbody></table>

<a id="f989b2154a832373"></a>
#### ROLE_SCHEMA_PRIVS

ROLE_SCHEMA_PRIVS describes schema privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="3995cc3b464c3be1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Schema privilege granted to the role</td></tr><tr><td valign="middle">SCHEMA_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the schema</td></tr><tr><td valign="middle">SCHEMA_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the schema</td></tr><tr><td valign="middle">GRANT_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the GRANT option (YES) or not (NO)</td></tr></tbody></table>

<a id="5f7e282867bb459c"></a>
#### ROLE_SEQ_PRIVS

ROLE_SEQ_PRIVS describes sequence privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="3efa63129647890b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">SEQUENCE_OWNER</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Owner of the sequence</td></tr><tr><td valign="middle">SEQUENCE_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Schema of the sequence</td></tr><tr><td valign="middle">SEQUENCE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the sequence</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Sequence privilege granted to the role</td></tr><tr><td valign="middle">GRANTABLE</td><td valign="middle">VARCHAR(3)</td><td valign="middle">YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="418c8aa9b1d53846"></a>
#### ROLE_SYS_PRIVS

ROLE_SYS_PRIVS describes all system(database, tablespace, schema) privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="c8dfe0848f27a83d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(256)</td><td valign="middle">all system(database, tablespace, schema) privilege granted to the role</td></tr><tr><td valign="middle">GRANT_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the GRANT option (YES) or not (NO)</td></tr><tr><td valign="middle">COMMON</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates how the grant was made. (YES or NO)</td></tr><tr><td valign="middle">INHERITED</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the role grant was inherited from another container (YES) or not (NO)</td></tr></tbody></table>

<a id="25e9323ff840e05c"></a>
#### ROLE_TAB_PRIVS

ROLE_TAB_PRIVS describes table privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="31cf648952aa12ac"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>ROLE_NAME</td><td>VARCHAR(128)</td><td>Name of the role</td></tr><tr><td>TABLE_OWNER</td><td>VARCHAR(128)</td><td>Owner of the table</td></tr><tr><td>TABLE_SCHEMA</td><td>VARCHAR(128)</td><td>Schema of the table</td></tr><tr><td>TABLE_NAME</td><td>VARCHAR(128)</td><td>Name of the table</td></tr><tr><td>PRIVILEGE</td><td>VARCHAR(32)</td><td>Table privilege granted to the role</td></tr><tr><td>GRANTABLE</td><td>VARCHAR(3)</td><td>YES if the role was granted with GRANT OPTION; otherwise NO</td></tr></tbody></table>

<a id="462dc6980831d98c"></a>
#### ROLE_TBS_PRIVS

ROLE_TBS_PRIVS describes tablespace privileges granted to roles. Information is provided only about roles to which the user has access.

**Column 정보**

<a id="d34e28d362c7fded"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td valign="middle">ROLE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the role</td></tr><tr><td valign="middle">PRIVILEGE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">Tablespace privilege granted to the role</td></tr><tr><td valign="middle">TABLESPACE_NAME</td><td valign="middle">VARCHAR(128)</td><td valign="middle">Name of the tablespace</td></tr><tr><td valign="middle">GRANT_OPTION</td><td valign="middle">VARCHAR(3)</td><td valign="middle">Indicates whether the grant was with the GRANT option (YES) or not (NO)</td></tr></tbody></table>

<a id="4bcf38569b8bfc42"></a>
#### SESSION_PRIVS

SESSION_PRIVS describes the privileges that are currently available to the user.

**Column 정보**

<a id="fceeb8c7b30e1f4b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE</td><td align="left">VARCHAR(256)</td><td align="left">Name of the privilege</td></tr></tbody></table>

<a id="dcbd0ed855449050"></a>
#### SESSION_ROLES

SESSION_ROLES describes the roles currently enabled for the current session.

**Column 정보**

<a id="16bf00e3007de59b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>ROLE_NAME</td><td>VARCHAR(128)</td><td>Name of the role</td></tr></tbody></table>

<a id="20cb9f04676fb2c6"></a>
#### SUPPLEMENTAL_LOG_TABLE_INFO

SUPPLEMENTAL_LOG_TABLE_INFO describes table-level supplemental logging status.

**Column 정보**

<a id="fffc3f7754d3b7e1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUPPLEMENTAL_LOG_DATA_PK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of table-level PRIMARY KEY COLUMNS supplemental logging: IMPLICIT, EXPLICIT, NO</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td>Indicates whether the object has been dropped and is in the recycle bin (YES) or not (NO)</td></tr></tbody></table>

<a id="f8e0d33e2c151686"></a>
### Aliased Synonym

DICTIONARY_SCHEMA 내의 view나 테이블을 가리키는 public synonym이다.

<a id="ebc0cc76ed3ed37b"></a>
#### COLS

COLS is a public synonym for USER_TAB_COLUMNS.

<a id="a6442d05c609526f"></a>
#### DICT

DICT is a public synonym for DICTIONARY.

<a id="a7479c687d01a1c2"></a>
#### IND

IND is a public synonym for USER_INDEXES.

<a id="06fff78d6d056e9a"></a>
#### OBJ

OBJ is a public synonym for USER_OBJECTS.

<a id="9017f006da2a232d"></a>
#### SEQ

SEQ is a public synonym for USER_SEQUENCES.

<a id="556c9918412e6c77"></a>
#### TABS

TABS is a public synonym for USER_TABLES.

<a id="80cfc11fa8140b5d"></a>
#### RECYCLEBIN

RECYCLEBIN is a public synonym for USER_RECYCLEBIN.

<a id="83a1c3ba584ee938"></a>
## INFORMATION_SCHEMA

INFORMATION_SCHEMA 스키마의 view들은 SQL 표준에서 정의한 INFORMATION_SCHEMA의 view들과 동일한 정보를 제공한다.

해당 view들을 사용하려면 다음과 같이 InformationSchema.sql을 실행해야 한다.

- Standalone의 경우

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/standalone/InformationSchema.sql
```

- Cluster의 경우

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
```


> 
> - INFORMATION_SCHEMA의 view와 테이블들은 open 단계부터 조회할 수 있다.
> - 휴지통에 보관된 객체들은 INFORMATION_SCHEMA의 view에서 조회할 수 없다.
> 

<a id="b79db007a27dc6cf"></a>
### ADMINISTRABLE_ROLE_AUTHORIZATIONS

Identify role authorizations for which the current user or role has WITH ADMIN OPTION

**Column 정보**

<a id="d4e5d8fef0b2e2ac"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | grantee name |
| ROLE_NAME | VARCHAR(128) | role name |
| IS_GRANTABLE | BOOLEAN | is grantable or not |

<a id="bd47c46100f17655"></a>
### APPLICABLE_ROLES

Identify the applicable roles for current SQL-session

**Column 정보**

<a id="cb147decffa89bcf"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | grantee name |
| ROLE_NAME | VARCHAR(128) | role name |
| IS_GRANTABLE | BOOLEAN | is grantable or not |

<a id="ac3225f1a6a74612"></a>
### CHECK_CONSTRAINTS

Identify the check constraints defined in this catalog that are owned by a given user or role.

**Column 정보**

<a id="99c7baa86b66fbec"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| CONSTRAINT_CATALOG | VARCHAR(128) | catalog name of the constraint |
| CONSTRAINT_OWNER | VARCHAR(128) | authorization name who owns the constraint |
| CONSTRAINT_SCHEMA | VARCHAR(128) | schema name of the constraint being described |
| CONSTRAINT_TABLE | VARCHAR(128) | table name of the constraint being described |
| CONSTRAINT_NAME | VARCHAR(128) | constraint name |
| CHECK_CLAUSE | LONG VARCHAR | search condition of CHECK constraint, null for NOT NULL constraint |

<a id="3cfe57f67565febd"></a>
### COLUMNS

Identify the columns of tables defined in this catalog that are accessible to given user or role.

**Column 정보**

<a id="02e80fb3ca8214df"></a>
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
| CHARACTER_SET_CATALOG | VARCHAR(128) | catalog name of the character set if it is a character string type |
| CHARACTER_SET_SCHEMA | VARCHAR(128) | schema name of the character set if it is a character string type |
| CHARACTER_SET_NAME | VARCHAR(128) | character set name of the character set if it is a character string type |
| COLLATION_CATALOG | VARCHAR(128) | catalog name of the applicable collation if it is a character string type |
| COLLATION_SCHEMA | VARCHAR(128) | schema name of the applicable collation if it is a character string type |
| COLLATION_NAME | VARCHAR(128) | collation name of the applicable collation if it is a character string type |
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

<a id="59562e81a335ac33"></a>
### COLUMN_PRIVILEGES

Identify the privileges on columns of tables defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="a0149dca2b35cb44"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted column privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the column privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( SELECT, INSERT, UPDATE, REFERENCES )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="52b7b9c0a58e93d8"></a>
### CONSTRAINT_COLUMN_USAGE

Identify the columns used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column 정보**

<a id="829ee391a7905291"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="f8d3eb95d004ce72"></a>
### CONSTRAINT_TABLE_USAGE

Identify the tables that are used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column 정보**

<a id="446e0b83e35319f3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="1a74c1aceda9783b"></a>
### ENABLED_ROLES

Identify the enabled roles for current SQL-session

**Column 정보**

<a id="a10d9830e38dcb3b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| ROLE_NAME | VARCHAR(128) | role name |

<a id="3634eaae939205b5"></a>
### INFORMATION_SCHEMA_CATALOG_NAME

Identify the catalog that contains the Information Schema.

**Column 정보**

<a id="e78641bb727736af"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CATALOG_NAME</td><td align="left">VARCHAR(128)</td><td align="left">the name of catalog in which this Information Schema resides</td></tr></tbody></table>

<a id="3aad55059a768926"></a>
### KEY_COLUMN_USAGE

Identify the columns defined in this catalog that are constrained as keys and that are accessible by a given user or role.

**Column 정보**

<a id="9ff830ed3c0fb84d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position of the specific column in the constraint being described. If the constraint described is a key of cardinality 1 (one), then the value of ORDINAL_POSITION is always 1 (one).</td></tr><tr><td align="left" valign="middle">POSITION_IN_UNIQUE_CONSTRAINT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the constraint being described is a foreign key constraint, then the value of POSITION_IN_UNIQUE_CONSTRAINT is the ordinal position of the referenced column corresponding to the referencing column being described, in the corresponding unique key constraint.</td></tr></tbody></table>

<a id="aaf7ad7cdbe69f1d"></a>
### MODULES

Identify the SQL-server modules in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="dd0966d63b432490"></a>
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
| DEFAULT_SCHEMA_NAME | VARCHAR(128) | default schema name of the SQL-server module |
| MODULE_DEFINITION | LONG VARCHAR | definition of the SQL-server module |
| MODULE_AUTHORIZATION | VARCHAR(32) | authorization of the SQL-server module(DEFINER/INVOKER) |
| SQL_PATH | VARCHAR(1024) | described SQL PATH when the SQL-server module is defined |
| CREATED | TIMESTAMP(6) WITHOUT TIME ZONE | creation time of the SQL-server module |
| LAST_ALTERED | TIMESTAMP(6) WITHOUT TIME ZONE | most lately altered time of the SQL-server module |
| COMMENTS | VARCHAR(1024) | comment on the SQL-server module |

<a id="31bc2a12d6a11d4c"></a>
### MODULE_BODY

Identify the SQL-server module bodies in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="e2ef3b9ad65c54eb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module' |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module |
| MODULE_DEFINITION | LONG VARCHAR | definition of the SQL-server module body |
| CREATED | TIMESTAMP(6) WITHOUT TIME ZONE | creation time of the SQL-server module body |
| LAST_ALTERED | TIMESTAMP(6) WITHOUT TIME ZONE | most lately altered time of the SQL-server module body |

<a id="27b446d2b4d278aa"></a>
### MODULE_BODY_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column 정보**

<a id="118278d8cee38112"></a>
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

<a id="2b910b6853e0a405"></a>
### MODULE_BODY_ROUTINE_USAGE

Identify the SQL-invoked routines owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column 정보**

<a id="44210c12037fe4bf"></a>
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

<a id="30aab53e2446bfef"></a>
### MODULE_BODY_SEQUENCE_USAGE

Identify the sequences owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column 정보**

<a id="3a4689419e271f60"></a>
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

<a id="392e033c0d4f4f52"></a>
### MODULE_BODY_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL-server module bodies defined in this catalog are dependent.

**Column 정보**

<a id="db02a134a4c26626"></a>
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

<a id="8b07f3fd637e56a5"></a>
### MODULE_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column 정보**

<a id="d4a41fa413e7cf56"></a>
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

<a id="445aa91bbee77289"></a>
### MODULE_PRIVILEGES

Identify the privileges on SQL-server modules defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="f7686ef77e0f7494"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted SQL-server module privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the SQL-server module privilege being described is granted |
| MODULE_CATALOG | VARCHAR(128) | catalog name of the SQL-server module on which the privilege being described was granted |
| MODULE_OWNER | VARCHAR(128) | owner name of the SQL-server module on which the privilege being described was granted |
| MODULE_SCHEMA | VARCHAR(128) | schema name of the SQL-server module on which the privilege being described was granted |
| MODULE_NAME | VARCHAR(128) | name of the SQL-server module on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="6183a810e8fef33b"></a>
### MODULE_ROUTINE_USAGE

Identify the SQL-invoked routines owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column 정보**

<a id="b025ce35e4eec975"></a>
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

<a id="1217dc973bebedb1"></a>
### MODULE_SEQUENCE_USAGE

Identify the sequences owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column 정보**

<a id="a5713954eb692e36"></a>
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

<a id="8eec24659fd7ea0d"></a>
### MODULE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL-server modules defined in this catalog are dependent.

**Column 정보**

<a id="3286bb47f58c3a14"></a>
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

<a id="998fdaedd0d0e2dd"></a>
### PARAMETERS

Identify the SQL parameters of SQL-invoked routines defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="824d3df8bd98e29e"></a>
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

<a id="641d01b1ec5bf079"></a>
### REFERENTIAL_CONSTRAINTS

Identify the referential constraints defined on tables in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="420b21ec0e2524cd"></a>
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

<a id="3d2b11ed66218115"></a>
### ROLE_COLUMN_GRANTS

Identify the privileges on columns defined in this catalog that are available to or granted by the currently enabled roles.

**Column 정보**

<a id="17dea1caa534c41b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted column privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the column privilege being described is granted |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the column on which the privilege being described was granted |
| TABLE_OWNER | VARCHAR(128) | table owner name of the column on which the privilege being described was granted |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the column on which the privilege being described was granted |
| TABLE_NAME | VARCHAR(128) | table name of the column on which the privilege being described was granted |
| COLUMN_NAME | VARCHAR(128) | column name of the column on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( SELECT, INSERT, UPDATE, REFERENCES ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="2c8b0992131aaabd"></a>
### ROLE_MODULE_GRANTS

Identify the privileges on SQL-server modules defined in this catalog that are available to or granted by the currently enabled roles.

**Column 정보**

<a id="7f2ab8a44f0d4c11"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted SQL-server module privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the SQL-server module privilege being described is granted |
| MODULE_CATALOG | VARCHAR(128) | specific catalog name of the SQL-server module on which the privilege being described was granted |
| MODULE_OWNER | VARCHAR(128) | specific owner name of the SQL-server module on which the privilege being described was granted |
| MODULE_SCHEMA | VARCHAR(128) | specific schema name of the SQL-server module on which the privilege being described was granted |
| MODULE_NAME | VARCHAR(128) | specific name of the SQL-server module on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="9619508606d2776e"></a>
### ROLE_ROUTINE_GRANTS

Identify the privileges on SQL-invoked routines defined in this catalog that are available to or granted by the currently enabled roles.

**Column 정보**

<a id="a5b554b9c72b6566"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted routine privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the routine privilege being described is granted |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_CATALOG | VARCHAR(128) | routine catalog name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_OWNER | VARCHAR(128) | routine owner name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_SCHEMA | VARCHAR(128) | routine schema name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_NAME | VARCHAR(128) | routine name of the SQL-invoked routine on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="fc8b32800e452fd1"></a>
### ROLE_TABLE_GRANTS

Identify the privileges on tables defined in this catalog that are available to or granted by the currently enabled roles.

**Column 정보**

<a id="6f907c8ae3f20027"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted table privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the table privilege being described is granted |
| TABLE_CATALOG | VARCHAR(128) | catalog name of the table on which the privilege being described was granted |
| TABLE_OWNER | VARCHAR(128) | table owner name of the table on which the privilege being described was granted |
| TABLE_SCHEMA | VARCHAR(128) | schema name of the table on which the privilege being described was granted |
| TABLE_NAME | VARCHAR(128) | table name on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( CONTROL, SELECT, INSERT, UPDATE, DELETE, REFERENCES, LOCK, INDEX, ALTER ) |
| IS_GRANTABLE | BOOLEAN | is grantable |
| WITH_HIERARCHY | BOOLEAN | whether the privilege was granted WITH HIERARCHY OPTION or not |

<a id="7955d1c7839ad3b9"></a>
### ROLE_USAGE_GRANTS

Identify the USAGE privileges on objects defined in this catalog that are available to or granted by the currently enabled roles.

**Column 정보**

<a id="d3b2313e9ba4cd25"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted usage privileges, on the object of the type identified by OBJECT_TYPE |
| GRANTEE | VARCHAR(128) | authorization identifier of some user or role, or PUBLIC to indicate all users, to whom the usage privilege being described is granted |
| OBJECT_CATALOG | VARCHAR(128) | catalog name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted |
| OBJECT_OWNER | VARCHAR(128) | owner name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted |
| OBJECT_SCHEMA | VARCHAR(128) | schema name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted |
| OBJECT_NAME | VARCHAR(128) | object name of the type identified by OBJECT_TYPE on which the privilege being described was granted |
| OBJECT_TYPE | VARCHAR(32) | the value is in ( DOMAIN, CHARACTER SET, COLLATION, TRANSLATION, SEQUENCE ) |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( USAGE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="78ef3c3234db2c9b"></a>
### ROUTINES

Identify the SQL-invoked routines in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="e2aa3bcd941dfdab"></a>
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
| EXTERNAL_C_FUNCTION | LONG VARCHAR | external C function prototype of the SQL-invoked routine |
| EXTERNAL_LANGUAGE | VARCHAR(32) | language of the external routine |
| LIBRARY_SCHEMA | VARCHAR(128) | library schema name which associated with an operating-system shared library |
| LIBRARY_NAME | VARCHAR(128) | library name which associated with an operating-system shared library |
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
| COMMENTS | VARCHAR(1024) | comment on the routine |

<a id="b18f91b27680bc3a"></a>
### ROUTINE_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column 정보**

<a id="066eb09c9ec571b6"></a>
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

<a id="e4030493f02bdbe7"></a>
### ROUTINE_PRIVILEGES

Identify the privileges on SQL-invoked routines defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="f4f483636c1ebe29"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | authorization name of the user who granted routine privileges |
| GRANTEE | VARCHAR(128) | authorization name of some user or role, or PUBLIC to indicate all users, to whom the routine privilege being described is granted |
| SPECIFIC_CATALOG | VARCHAR(128) | specific catalog name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_OWNER | VARCHAR(128) | specific owner name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_SCHEMA | VARCHAR(128) | specific schema name of the SQL-invoked routine on which the privilege being described was granted |
| SPECIFIC_NAME | VARCHAR(128) | specific name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_CATALOG | VARCHAR(128) | routine catalog name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_OWNER | VARCHAR(128) | null |
| ROUTINE_SCHEMA | VARCHAR(128) | routine schema name of the SQL-invoked routine on which the privilege being described was granted |
| ROUTINE_NAME | VARCHAR(128) | routine name of the SQL-invoked routine on which the privilege being described was granted |
| PRIVILEGE_TYPE | VARCHAR(32) | the value is in ( EXECUTE ) |
| IS_GRANTABLE | BOOLEAN | is grantable |

<a id="623e6157b0a1df87"></a>
### ROUTINE_ROUTINE_USAGE

Identify each SQL-invoked routine owned by a given user or role on which an SQL routine defined in this catalog is dependent.

**Column 정보**

<a id="cd1292f1620c24bf"></a>
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

<a id="0f058cd608fd4e5a"></a>
### ROUTINE_SEQUENCE_USAGE

Identify each external sequence generator owned by a given user or role on which some SQL routine defined in this catalog is dependent.

**Column 정보**

<a id="811e179fd72c2c2a"></a>
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

<a id="13771f5b770f6fd7"></a>
### ROUTINE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column 정보**

<a id="9bcdde6326d1702d"></a>
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

<a id="3c40d87c8bc1d23c"></a>
### SCHEMATA

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column 정보**

<a id="7486314b5ba32e2c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CATALOG_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name</td></tr><tr><td align="left" valign="middle">SCHEMA_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the schema</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">character set name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">SQL_PATH</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">character representation of schema path specification</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the schema</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the schema</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the schema</td></tr></tbody></table>

<a id="751d08bedae5a927"></a>
### SEQUENCES

Identify the external sequence generators defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="26b049c605ef13b8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the standard name of the data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION_RADIX</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the radix ( 2 or 10 ) of the precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric scale of the exact numerical data type</td></tr><tr><td align="left" valign="middle">START_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the start value of the sequence generator</td></tr><tr><td align="left" valign="middle">MINIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the minimum value of the sequence generator</td></tr><tr><td align="left" valign="middle">MAXIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the maximum value of the sequence generator</td></tr><tr><td align="left" valign="middle">INCREMENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the increment of the sequence generator</td></tr><tr><td align="left" valign="middle">CYCLE_OPTION</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">cycle option</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">DECLARED_DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the sequence generator</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the sequence generator</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the sequence generator</td></tr></tbody></table>

<a id="53018e31a0639e42"></a>
### SQL_FEATURES

List the features and subfeatures of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="35325dd1f78e65cb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="25750f2b0cd049c6"></a>
### SQL_IMPLEMENTATION_INFO

List the SQL-implementation information items defined in this ISO/IEC 9075 standard and, for each of these, indicate the value supported by the SQL-implementation.

**Column 정보**

<a id="fc1bbdfc934f62f1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation information item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation information item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation information item</td></tr></tbody></table>

<a id="ca72bcbd4f322384"></a>
### SQL_PACKAGES

List the packages of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="af966277457705fd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="c212dae7493c2f9e"></a>
### SQL_PARTS

List the parts of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="5d9c9930dcd9ee08"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="a390569b57f3aa55"></a>
### SQL_SIZING

List the sizing items of this ISO/IEC 9075 standard, for each of these, indicate the size supported by the SQL-implementation.

**Column 정보**

<a id="53196ef411450a13"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SIZING_ID</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">identifier of the sizing item</td></tr><tr><td align="left" valign="middle">SIZING_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the sizing item</td></tr><tr><td align="left" valign="middle">SUPPORTED_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the sizing item, or 0 if the size is unlimited or cannot be determined, or null if the features for which the sizing item is applicable are not supported</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the sizing item</td></tr></tbody></table>

<a id="d99bacdf71dd99eb"></a>
### STATISTICS

Provide a list of statistics about a single table and the indexes associated with the table that are accessible to a given user or role.

**Column 정보**

<a id="fe795358fb0531d7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">STAT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">statistics type: the value in ( TABLE STAT, INDEX CLUSTERED, INDEX HASHED, INDEX OTHER )</td></tr><tr><td align="left" valign="middle">NON_UNIQUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the index does not allow duplicate values</td></tr><tr><td align="left" valign="middle">INDEX_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the index</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the index</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the index</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ordinal position of the specific column in the index described</td></tr><tr><td align="left" valign="middle">IS_ASCENDING_ORDER</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">index key column being described is sorted in ASCENDING(TRUE) or DESCENDING(FALSE) order</td></tr><tr><td align="left" valign="middle">IS_NULLS_FIRST</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">the null values of the key column are sorted before(TRUE) or after(FALSE) non-null values</td></tr><tr><td align="left" valign="middle">CARDINALITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of rows in the table; otherwise, it is the number of unique values in the index</td></tr><tr><td align="left" valign="middle">PAGES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of pages used for the table; otherwise, it is the number of pages used for the current index.</td></tr><tr><td align="left" valign="middle">FILTER_CONDITION</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">filter condition, if any.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the table comments; otherwise, it is the index comments.</td></tr></tbody></table>

<a id="1d331d4bc01ad39c"></a>
### TABLES

Identify the tables defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="85e53d0155df1c90"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( BASE TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM VERSIONED, FIXED TABLE, DUMP TABLE )</td></tr><tr><td align="left" valign="middle">DBC_TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">ODBC/JDBC table type: the value is in ( TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, IMMUTABLE TABLE, SYSTEM TABLE, ALIAS, SYNONYM )</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name of the table, NULL if view</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_START_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version start column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_END_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version end column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_RETENTION_PERIOD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a system-versioned table, then the character representation of the value of the retention period of the table</td></tr><tr><td align="left" valign="middle">SELF_REFERENCING_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a typed table, then the name of the self-referencing column of the table</td></tr><tr><td align="left" valign="middle">REFERENCE_GENERATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table has a self-referencing column, the value is in ( SYSTEM GENERATED, USER GENERATED, DERIVED )</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the catalog name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the schema name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the name of the structured type</td></tr><tr><td align="left" valign="middle">IS_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable-into table</td></tr><tr><td align="left" valign="middle">IS_TYPED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a typed table</td></tr><tr><td align="left" valign="middle">COMMIT_ACTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a temporary table, the value is in ( DELETE, PRESERVE )</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the table</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the table</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the table</td></tr></tbody></table>

<a id="6047874bb63329e2"></a>
### TABLE_CONSTRAINTS

Identify the table constraints defined on tables in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="671f79874bd73cc1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( PRIMARY KEY, UNIQUE, FOREIGN KEY, NOT NULL, CHECK )</td></tr><tr><td align="left" valign="middle">IS_DEFERRABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a deferrable constraint</td></tr><tr><td align="left" valign="middle">INITIALLY_DEFERRED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an initially deferred constraint</td></tr><tr><td align="left" valign="middle">ENFORCED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an enforced constraint</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the constraint</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the constraint</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the constraint</td></tr></tbody></table>

<a id="a5e27e85777c8eaf"></a>
### TABLE_PRIVILEGES

Identify the privileges on tables defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="0e98379b49f14f0e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted table privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the table privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CONTROL, SELECT, INSERT, UPDATE, DELETE, REFERENCES, LOCK, INDEX, ALTER )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr><tr><td align="left" valign="middle">WITH_HIERARCHY</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the privilege was granted WITH HIERARCHY OPTION or not</td></tr></tbody></table>

<a id="7a2acb29cb1714e9"></a>
### TRIGGER_EVENT_ORDER

Identify trigger event order in the list of triggers with the same EVENT_OBJECT_SCHEMA, EVENT_OBJECT_TABLE, ACTION_TIMING, ACTION_ORIENTATION, and EVENT_MANIPULATION.

**Column 정보**

<a id="c3cf6278632a5719"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">EVENT_OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_TABLE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">ACTION_TIMING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">action timing, the value is in ( 'BEFORE', 'AFTER', 'INSTEAD OF' )</td></tr><tr><td align="left" valign="middle">ACTION_ORIENTATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">action orientation, the value is in ( 'ROW', 'STATEMENT' )</td></tr><tr><td align="left" valign="middle">EVENT_MANIPULATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">trigger event, the value is in ( 'INSERT', 'UPDATE', 'DELETE' )</td></tr><tr><td align="left" valign="middle">ACTION_ORDER</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">the ordinal position of the trigger in the list of triggers with the same EVENT_OBJECT_SCHEMA, EVENT_OBJECT_TABLE, ACTION_TIMING, ACTION_ORIENTATION, and EVENT_MANIPULATION</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td>TRIGGER_SCHEMA</td><td>VARCHAR(128)</td><td>schema name of the trigger</td></tr><tr><td>TRIGGER_NAME</td><td>VARCHAR(128)</td><td>trigger name</td></tr></tbody></table>

<a id="d4fcbd71fb7e1511"></a>
### TRIGGER_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which some trigger defined in this catalog is dependent.

**Column 정보**

<a id="f64ce4346e8c4dbe"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">MODULE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the SQL-server module identified in the trigger</td></tr><tr><td align="left" valign="middle">MODULE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the SQL-server module identified in the trigger</td></tr><tr><td align="left" valign="middle">MODULE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the SQL-server module identified in the trigger</td></tr><tr><td align="left" valign="middle">MODULE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">module name of the SQL-server module identified in the trigger</td></tr></tbody></table>

<a id="c645c53788b61e17"></a>
### TRIGGER_ROUTINE_USAGE

Identify each SQL-invoked routine owned by a given user or role on which some trigger defined in this catalog is dependent.

**Column 정보**

<a id="d8b274441655fcee"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">SPECIFIC_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific catalog name of the routine identified in the trigger</td></tr><tr><td align="left" valign="middle">SPECIFIC_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific owner name of the routine identified in the trigger</td></tr><tr><td align="left" valign="middle">SPECIFIC_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific schema name of the routine identified in the trigger</td></tr><tr><td align="left" valign="middle">SPECIFIC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific name of the routine identified in the trigger</td></tr></tbody></table>

<a id="bc3e28cc394151cd"></a>
### TRIGGER_SEQUENCE_USAGE

Identify each external sequence generator owned by a given user or role on which some trigger defined in this catalog is dependent.

**Column 정보**

<a id="6748632e91ff04aa"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">SEQUENCE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the sequence identified in the trigger</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the sequence identified in the trigger</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the sequence identified in the trigger</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name identified in the trigger</td></tr></tbody></table>

<a id="5408701b0cf2b9e9"></a>
### TRIGGER_TABLE_USAGE

Identify the tables on which triggers defined in this catalog and owned by a given user or role are dependent.

**Column 정보**

<a id="4644760f232ed974"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table identified in the trigger</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table identified in the trigger</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table identified in the trigger</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name identified in the trigger</td></tr></tbody></table>

<a id="b05f349928e40ed8"></a>
### TRIGGERED_UPDATE_COLUMNS

Identify the columns in this catalog that are identified by the explicit UPDATE trigger event columns of a trigger defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="8530c5ba258190b3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_TABLE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the subject table of the trigger</td></tr><tr><td>EVENT_OBJECT_COLUMN</td><td>VARCHAR(128)</td><td>column name of the subject table of the trigger</td></tr></tbody></table>

<a id="e81a9859de741ee3"></a>
### TRIGGERS

Identify the triggers defined on tables in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="1c39b5726aca5769"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRIGGER_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the trigger</td></tr><tr><td align="left" valign="middle">TRIGGER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">trigger name</td></tr><tr><td align="left" valign="middle">EVENT_MANIPULATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">trigger event, the value is in ( 'INSERT', 'UPDATE', 'INSERT OR UPDATE', 'DELETE', 'INSERT OR DELETE', 'UPDATE OR DELETE', 'INSERT OR UPDATE OR DELETE' )</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">EVENT_OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the subject table of the trigger</td></tr><tr><td valign="middle">EVENT_OBJECT_SCHEMA</td><td valign="middle">VARCHAR(128)</td><td valign="middle">schema name of the subject table of the trigger</td></tr><tr><td valign="middle">EVENT_OBJECT_TABLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">table name of the subject table of the trigger</td></tr><tr><td align="left" valign="middle">ACTION_ORDER</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">the ordinal position of the trigger in the list of triggers with the same EVENT_OBJECT_CATALOG, EVENT_OBJECT_SCHEMA, EVENT_OBJECT_TABLE, ACTION_TIMING, and ACTION_ORIENTATION</td></tr><tr><td valign="middle">ACTION_CONDITION</td><td valign="middle">LONG VARCHAR</td><td valign="middle">action condition is a character representation of the &lt;search condition&gt; in the &lt;triggered action&gt; of the trigger</td></tr><tr><td valign="middle">ACTION_STATEMENT</td><td valign="middle">LONG VARCHAR</td><td valign="middle">action statement is a character representation of the &lt;triggered SQL statement&gt; in the &lt;triggered action&gt; of the trigger</td></tr><tr><td valign="middle">ACTION_ORIENTATION</td><td valign="middle">VARCHAR(32)</td><td valign="middle">action orientation, the value is in ( 'ROW', 'STATEMENT' )</td></tr><tr><td valign="middle">ACTION_TIMING</td><td valign="middle">VARCHAR(32)</td><td valign="middle">action timing, the value is in ( 'BEFORE', 'AFTER', 'INSTEAD OF' )</td></tr><tr><td valign="middle">ACTION_REFERENCE_OLD_TABLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">the &lt;old transition table name&gt; of the trigger</td></tr><tr><td valign="middle">ACTION_REFERENCE_NEW_TABLE</td><td valign="middle">VARCHAR(128)</td><td valign="middle">the &lt;new transition table name&gt; of the trigger</td></tr><tr><td valign="middle">ACTION_REFERENCE_OLD_ROW</td><td valign="middle">VARCHAR(128)</td><td valign="middle">the &lt;old transition variable name&gt; of the trigger</td></tr><tr><td valign="middle">ACTION_REFERENCE_NEW_ROW</td><td valign="middle">VARCHAR(128)</td><td valign="middle">the &lt;new transition variable name&gt; of the trigger</td></tr><tr><td valign="middle">CREATED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">created time of the trigger</td></tr><tr><td valign="middle">MODIFIED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">last modified time of the trigger</td></tr><tr><td valign="middle">COMMENTS</td><td valign="middle">VARCHAR(1024)</td><td valign="middle">comments of the trigger</td></tr></tbody></table>

<a id="be51cf9010ec9360"></a>
### USAGE_PRIVILEGES

Identify the USAGE privileges on objects defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="26626b19d71a877c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted usage privileges, on the object of the type identified by OBJECT_TYPE</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization identifier of some user or role, or PUBLIC to indicate all users, to whom the usage privilege being described is granted</td></tr><tr><td align="left" valign="middle">OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( DOMAIN, CHARACTER SET, COLLATION, TRANSLATION, SEQUENCE )</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( USAGE )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="373d058e03d3aabe"></a>
### VIEWS

Identify the viewed tables defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="9a13f64675ebd7e1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">the character representation of the user-specified query expression contained in the corresponding view descriptor</td></tr><tr><td align="left" valign="middle">CHECK_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CASCADED, LOCAL, NONE )</td></tr><tr><td align="left" valign="middle">IS_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an updatable view</td></tr><tr><td align="left" valign="middle">INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable view</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an update INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_DELETABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether a delete INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an insert INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_COMPILED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is compiled or not</td></tr><tr><td align="left" valign="middle">IS_AFFECTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is affected by modification of underlying object or not</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the view</td></tr></tbody></table>

<a id="e6810598b1810d0a"></a>
### VIEW_MODULE_USAGE

Identify the SQL-server modules owned by a given user or role on which views defined in this catalog are dependent.

**Column 정보**

<a id="c2c03c1a92a1177f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">MODULE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td>catalog name of the SQL-server module of contained in definition text of the view</td></tr><tr><td align="left" valign="middle">MODULE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td>owner name of the SQL-server module of contained in definition text of the view</td></tr><tr><td align="left" valign="middle">MODULE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td>schema name of the SQL-server module of contained in definition text of the view'</td></tr><tr><td align="left" valign="middle">MODULE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td>SQL-server module name of contained in definition text of the view</td></tr></tbody></table>

<a id="3004b97ae0d544d8"></a>
### VIEW_ROUTINE_USAGE

Identify each routine owned by a given user or role on which a view defined in this catalog is dependent.

**Column 정보**

<a id="06abc76bb73cc757"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">SPECIFIC_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific catalog name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific owner name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific schema name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific name of a routine contained in the query expression of the view being described</td></tr></tbody></table>

<a id="32e6b7bb5a158983"></a>
### VIEW_TABLE_USAGE

Identify the tables on which viewed tables defined in this catalog and owned by a given user or role are dependent.

**Column 정보**

<a id="0993aa639e3ad6eb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr></tbody></table>

<a id="5691092c2fc94b72"></a>
## PERFORMANCE_VIEW_SCHEMA

PERFORMANCE_VIEW_SCHEMA 스키마는 시스템의 현재 상태 정보를 조회할 수 있는 view들로 구성되어 있다.

해당 view들을 사용하려면 다음과 같이 PerformanceViewSchema.sql을 실행해야 한다.

- Standalone의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/standalone/PerformanceViewSchema.sql
```

- Cluster의 경우

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/cluster/PerformanceViewSchema.sql
```

PERFORMANCE_VIEW_SCHEMA의 view들은 startup 단계 (nomount, mount, open)별로 조회할 수 있는 정보가 다르다.  
각 view를 어떤 시작 단계에서 조회할 수 있는지는 다음과 같은 질의를 통해 확인할 수 있다.

```
gSQL> select table_name, startup_phase from v$tables order by 1;

TABLE_NAME                 STARTUP_PHASE
-------------------------- -------------
V$AGABLE_INFO              OPEN         
V$ALLOCATOR                NO_MOUNT     
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

TABLE_NAME            STARTUP_PHASE
--------------------- -------------
V$LATCH               NO_MOUNT     
V$LICENSE             OPEN         
V$LOCKED_OBJECT       OPEN         
V$LOCK_WAIT           OPEN         
V$LOGFILE             MOUNT        
V$OPEN_CURSOR         NO_MOUNT     
V$PLAN_HISTORY        OPEN         
V$PLAN_HISTORY_LATEST OPEN         
V$PROCESS_MEM_STAT    NO_MOUNT     
V$PROCESS_SQL_STAT    NO_MOUNT     
V$PROCESS_STAT        NO_MOUNT     
V$PROPERTY            NO_MOUNT     
V$PROPERTY_ALIAS      NO_MOUNT     
V$PSM_RESERVED_WORDS  NO_MOUNT     
V$QUEUE               OPEN         
V$RELATION            OPEN         
V$RESERVED_WORDS      NO_MOUNT     
V$SEQUENCE            OPEN         
V$SESSION             NO_MOUNT     
V$SESSION_AUDIT       OPEN         

TABLE_NAME             STARTUP_PHASE
---------------------- -------------
V$SESSION_CONNECT_INFO NO_MOUNT     
V$SESSION_EVENT        OPEN         
V$SESSION_MEM_STAT     NO_MOUNT     
V$SESSION_MEM_USAGE    NO_MOUNT     
V$SESSION_SQL_STAT     NO_MOUNT     
V$SESSION_STAT         NO_MOUNT     
V$SESSION_WAIT         OPEN         
V$SHARED_MODE          OPEN         
V$SHARED_SERVER        OPEN         
V$SHM_SEGMENT          NO_MOUNT     
V$SPROPERTY            NO_MOUNT     
V$SQLFN_METADATA       NO_MOUNT     
V$SQL_CACHE            NO_MOUNT     
V$SQL_COMMAND          NO_MOUNT     
V$SQL_HISTORY          NO_MOUNT     
V$STATEMENT            NO_MOUNT     
V$SYSTEM_EVENT         OPEN         
V$SYSTEM_MEM_STAT      NO_MOUNT     
V$SYSTEM_SQL_STAT      NO_MOUNT     
V$SYSTEM_STAT          NO_MOUNT     

TABLE_NAME              STARTUP_PHASE
----------------------- -------------
V$TABLES                NO_MOUNT     
V$TABLESPACE            MOUNT        
V$TABLESPACE_STAT       OPEN         
V$TCL_LOGFILE           MOUNT        
V$TRANSACTION           OPEN         
V$UNDO_SEGMENT          OPEN         
V$WAIT_EVENT_CLASS_NAME OPEN         
V$WAIT_EVENT_NAME       OPEN         
V$XA_TRANSACTION        OPEN         

69 rows selected.
```

<a id="12a1a8bb8a7c61d1"></a>
### GV$ Global View

Cluster에서는 대부분의 V$ view에 대응하는 GV$ view를 제공한다. V$ view는 현재 접속한 cluster member의 정보를 조회하는 반면, GV$ view는 일반적으로 활성화된 모든 cluster member 정보를 조회한다.

일반적인 GV$ view는 대응하는 V$ view의 모든 column을 포함하며, 각 행을 제공한 cluster member를 나타내는 ORIGIN_MEMBER_NAME column을 추가로 제공한다.

다만, 클러스터 공통 정보나 메타데이터를 제공하거나 뷰 자체가 클러스터 전체 정보를 나타내는 다음 GV$ view는 ORIGIN_MEMBER_NAME column을 제공하지 않으며, 대응하는 V$ view와 동일한 column 구성을 갖는다.

- GV$CLUSTER_MEMBER
- GV$ERROR_CODE
- GV$KEYWORDS
- GV$PSM_RESERVED_WORDS
- GV$RESERVED_WORDS
- GV$SQLFN_METADATA
- GV$TABLES

각 GV$ view의 column 구성은 **\DESC GV$view_name** 명령으로 확인할 수 있다.

> Cluster에서만 사용할 수 있다.

예를 들어, V$TRANSACTION 정보는 다음과 같이 현재 접속한 서버의 트랜잭션 정보를 보여준다.

```
gSQL> SELECT TRANS_ID, SESSION_ID, TRANS_VIEW_SCN, START_TIME FROM V$TRANSACTION;

TRANS_ID SESSION_ID TRANS_VIEW_SCN START_TIME                
-------- ---------- -------------- --------------------------
40501296         48 1098.1.26      2017-04-07 17:14:01.912637
```

이에 반해, GV$TRANSACTION 정보는 다음과 같이 모든 서버의 트랜잭션 정보를 보여준다.

```
gSQL> SELECT ORIGIN_MEMBER_NAME, TRANS_ID, SESSION_ID, TRANS_VIEW_SCN, START_TIME FROM GV$TRANSACTION;

ORIGIN_MEMBER_NAME TRANS_ID SESSION_ID TRANS_VIEW_SCN START_TIME                
------------------ -------- ---------- -------------- --------------------------
G1N1               40501296         48 1098.1.26      2017-04-07 17:14:01.912637
G2N2               40304688         48 1098.0.888     2017-04-07 17:14:55.134015
G2N1               42205232         48 1098.0.888     2017-04-07 17:14:55.135996
G1N2               40435760         48 1098.1.889     2017-04-07 17:14:01.910138
```

위의 예에서 ORIGIN_MEMBER_NAME 정보는 각 트랜잭션 정보가 G1N1, G2N1, G1N2, G2N2에 해당하는 클러스터 멤버로부터 획득되었음을 보여준다.

특정 원격 서버에 대한 정보는 다음과 같이 ORIGIN_MEMBER_NAME column에 대한 조건을 사용하여 조회할 수 있다.

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

<a id="eeaba056944fb80a"></a>
### V$AGABLE_INFO

The V$AGABLE_INFO displays the system agable information.

**Column 정보**

<a id="33bcb4ce81d9f13c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCN</td><td align="left">VARCHAR(32)</td><td align="left">system scn</td></tr><tr><td align="left">AGABLE_SCN</td><td align="left">VARCHAR(32)</td><td align="left">system agable scn</td></tr><tr><td align="left">AGABLE_SCN_GAP</td><td align="left">VARCHAR(32)</td><td align="left">gap between system scn and agable scn</td></tr><tr><td align="left">OLDEST_SESSION_ID</td><td align="left">NUMBER</td><td align="left">identifier of session blocking aging</td></tr></tbody></table>

<a id="71b3c73a3fd79d8d"></a>
### V$ALLOCATOR

The V$ALLOCATOR shows descriptions of all memory allocators.

**Column 정보**

<a id="ee748c37cc5be55d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ID</td><td align="left">NUMBER</td><td align="left">allocator identifier</td></tr><tr><td align="left">TYPE</td><td align="left">VARCHAR(8)</td><td align="left">allocator type: the value in ( REGION, DYNAMIC, ARRAY )</td></tr><tr><td align="left">MINIMUM_FRAGMENT_SIZE</td><td align="left">NUMBER</td><td align="left">minimum size of free block</td></tr><tr><td align="left">DESC</td><td align="left">VARCHAR(64)</td><td align="left">description of memory allocator</td></tr></tbody></table>

<a id="064824c498caa0a6"></a>
### V$ARCHIVELOG

The V$ARCHIVELOG displays information of log archiving.

**Column 정보**

<a id="7a5895dc370de5d0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ARCHIVELOG_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database log mode: the value in ( NOARCHIVELOG, ARCHIVELOG )</td></tr><tr><td align="left" valign="middle">LAST_ARCHIVED_LOG</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence number of last archived log file</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_DIR</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">archive destination path</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_FILE_PREFIX</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">file prefix name of the archived log</td></tr></tbody></table>

<a id="aee8355ea24895a3"></a>
### V$AUDITABLE_DB_PRIVILEGES

The V$AUDITABLE_DB_PRIVILEGES displays auditable database privileges.

**Column 정보**

<a id="ab83720a9a4572a1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE_ID</td><td align="left">NUMBER</td><td align="left">database privilege identifier</td></tr><tr><td align="left">PRIVILEGE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">database privilege name</td></tr></tbody></table>

<a id="55b95c4332da3e3d"></a>
### V$AUDITABLE_SYSTEM_ACTIONS

The V$AUDITABLE_SYSTEM_ACTIONS displays auditable system actions.

**Column 정보**

<a id="771cd7f217134443"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ACTION_ID</td><td align="left">NUMBER</td><td align="left">auditable system action identifier</td></tr><tr><td align="left">ACTION_NAME</td><td align="left">VARCHAR(128)</td><td align="left">auditable system action name</td></tr></tbody></table>

<a id="69a3b1ef5f81a076"></a>
### V$BACKUP

The V$BACKUP displays information of backup.

**Column 정보**

<a id="3100fc42db84bd45"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">BACKUP_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">indicates whether the tablespace begin backup ( ACTIVE ) or not ( INACTIVE )</td></tr><tr><td align="left" valign="middle">BACKUP_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the last checkpoint lsn of tablespace when backup started</td></tr></tbody></table>

<a id="432fead40dc70be1"></a>
### V$BALANCER

The V$BALANCER displays information of balancer.

**Column 정보**

<a id="a96a9f2f541ecadd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">balancer process identifier</td></tr><tr><td align="left">CUR_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">current number of connections</td></tr><tr><td align="left">CONNECTIONS</td><td align="left">NUMBER</td><td align="left">total number of connections</td></tr><tr><td align="left">CONNECTIONS_HIGHWATER</td><td align="left">NUMBER</td><td align="left">highest number of connections</td></tr><tr><td align="left">MAX_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">maximum connections</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">status</td></tr></tbody></table>

<a id="59dfbf4b571cd344"></a>
### V$BCH

The V$BCH displays information of database buffer control header array.

**Column 정보**

<a id="53f3769d5119ef0b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BCH_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">bch sequence</td></tr><tr><td align="left" valign="middle">TABLESPACE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier of the page cached in the frame of bch</td></tr><tr><td align="left" valign="middle">PAGE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page identifier of the page cached in the frame of bch</td></tr><tr><td valign="middle">LOGICAL_ADDRESS</td><td valign="middle">VARCHAR(18)</td><td valign="middle">logical address of the frame of bch</td></tr><tr><td valign="middle">DIRTY</td><td valign="middle">BOOLEAN</td><td valign="middle">dirty state of the page cached in the frame of bch</td></tr><tr><td valign="middle">PGAE_TYPE</td><td valign="middle">VARCHAR(20)</td><td valign="middle">page type of the page cached in the frame of bch</td></tr><tr><td valign="middle">FIRST_DIRTY_LSN</td><td valign="middle">NUMBER</td><td valign="middle">first dirty lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">RECOVERY_LSN</td><td valign="middle">NUMBER</td><td valign="middle">recovery lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">LAST_FLUSHED_LSN</td><td valign="middle">NUMBER</td><td valign="middle">last flushed lsn of the page cached in the frame of bch</td></tr><tr><td valign="middle">FIXED_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">fixed count of the page cached in the frame of bch</td></tr><tr><td valign="middle">TOUCHED_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">touched count of the page cached in the frame of bch</td></tr><tr><td valign="middle">RECENT_TOUCH_COUNT_INCREASED_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">timestamp that touch count of the page cached in the frame of bch increased most recently</td></tr><tr><td valign="middle">BCH_LIST_TYPE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">list type to which the bch belongs</td></tr><tr><td valign="middle">BCH_STATE</td><td valign="middle">VARCHAR(16)</td><td valign="middle">bch state</td></tr></tbody></table>

<a id="1c71f0f7d8fa0976"></a>
### V$BUFFER_STAT

The V$BUFFER_STAT displays database buffer statistics.

**Column 정보**

<a id="20d6c31b83416796"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BUFFER_POOL_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total buffer frame size ( page count )</td></tr><tr><td align="left" valign="middle">HASH_BUCKET_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">buffer hash bucket count</td></tr><tr><td align="left" valign="middle">LRU_LIST_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">buffer lru list count</td></tr><tr><td valign="middle">HOT_REGION_PERCENTAGE</td><td valign="middle">NUMBER</td><td valign="middle">percentage of lru hot region</td></tr><tr><td valign="middle">HOT_REGION_CRITERIA</td><td valign="middle">NUMBER</td><td valign="middle">touch count criteria of lru hot region</td></tr><tr><td valign="middle">CHECKPOINT_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer checkpoint list count</td></tr><tr><td valign="middle">FLUSH_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer flush list count</td></tr><tr><td valign="middle">FREE_LIST_COUNT</td><td valign="middle">NUMBER</td><td valign="middle">buffer free list count</td></tr><tr><td valign="middle">FREE_BUFFER_WAIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of waiting for free list</td></tr><tr><td valign="middle">READ_COMPLETE_WAIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of waiting for read page complete</td></tr><tr><td valign="middle">BUFFER_LOOKUPS</td><td valign="middle">NUMBER</td><td valign="middle">total number of lookups in the buffer for requested pages</td></tr><tr><td valign="middle">BUFFER_HIT</td><td valign="middle">NUMBER</td><td valign="middle">total number of hits in the buffer for requested pages</td></tr><tr><td valign="middle">BUFFER_MISS</td><td valign="middle">NUMBER</td><td valign="middle">total number of misses in the buffer for requested pages</td></tr><tr><td valign="middle">TOTAL_WRITES</td><td valign="middle">NUMBER</td><td valign="middle">total number of physical writes</td></tr><tr><td valign="middle">TOTAL_READS</td><td valign="middle">NUMBER</td><td valign="middle">total number of physical reads</td></tr><tr><td valign="middle">FLUSH_PER_SECOND</td><td valign="middle">NUMBER</td><td valign="middle">total number of disk writes per one second</td></tr><tr><td valign="middle">READ_PER_SECOND</td><td valign="middle">NUMBER</td><td valign="middle">total number of disk reads per one second</td></tr><tr><td valign="middle">AVERAGE_WRITE_LATENCY</td><td valign="middle">NUMBER</td><td valign="middle">average latency of disk writes</td></tr><tr><td valign="middle">AVERAGE_READ_LATENCY</td><td valign="middle">NUMBER</td><td valign="middle">average latency of disk reads</td></tr></tbody></table>

<a id="73139863bbefb273"></a>
### V$CLUSTER_COMMAND

The V$CLUSTER_COMMAND lists statistics information of each cluster command.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="027c9ed7155e0148"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">COMMAND</td><td align="left">VARCHAR(128)</td><td align="left">command name</td></tr><tr><td align="left">SEND_COUNT</td><td align="left">NUMBER</td><td align="left">send count</td></tr><tr><td align="left">ELAPSED_TIME</td><td align="left">NUMBER</td><td align="left">average elapsed time for command requests</td></tr><tr><td align="left">RECEIVE_COUNT</td><td align="left">NUMBER</td><td align="left">receive count</td></tr></tbody></table>

<a id="9237f1978b67a40a"></a>
### V$CLUSTER_CONNECTION

The V$CLUSTER_CONNECTION displays a list of all cluster connections.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="4ae57e430866afdc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">DISPATCHER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher identifier</td></tr><tr><td align="left" valign="middle">IS_SENDER</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the connection is owned by the sender (TRUE) or not (FALSE)</td></tr><tr><td align="left" valign="middle">LOCAL_PORT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">port number of connected local socket</td></tr><tr><td align="left" valign="middle">PEER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position of connected peer</td></tr><tr><td valign="middle">PEER_ADDR</td><td valign="middle">VARCHAR(1024)</td><td valign="middle">ip address of connected peer socket</td></tr><tr><td valign="middle">PEER_PORT</td><td valign="middle">NUMBER</td><td valign="middle">port number of connected peer socket</td></tr></tbody></table>

<a id="d2b23c79ecd3a287"></a>
### V$CLUSTER_DISPATCHER

The V$CLUSTER_DISPATCHER displays cluster dispatcher information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="50e0ee54769bb643"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">DISPATCHER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher identifier</td></tr><tr><td valign="middle">TYPE</td><td valign="middle">VARCHAR(64)</td><td valign="middle">dispatcher type: the value in ( commit, heartbeat, lockable, lockless, sync, urgent )</td></tr><tr><td align="left" valign="middle">RX_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total amount of data that has received through the dispatcher</td></tr><tr><td align="left" valign="middle">TX_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total amount of data that has transmitted through the dispatcher</td></tr><tr><td align="left" valign="middle">RX_JOBS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the total number of jobs received</td></tr><tr><td align="left" valign="middle">TX_JOBS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the total number of jobs transmitted</td></tr></tbody></table>

<a id="4229d8c893b08fad"></a>
### V$CLUSTER_LOCATION

The V$CLUSTER_LOCATION displays cluster location information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="310a68397a7edaf3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">member name</td></tr><tr><td align="left">HOST</td><td align="left">VARCHAR(256)</td><td align="left">host name or IP address of a member</td></tr><tr><td align="left">PORT</td><td align="left">NUMBER</td><td align="left">host port of a member</td></tr></tbody></table>

<a id="955698ee0a3944ce"></a>
### V$CLUSTER_MEMBER

The V$CLUSTER_MEMBER displays cluster member information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="704c459d0b247ee6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member identifier</td></tr><tr><td align="left" valign="middle">MEMBER_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">status of the member: the value in ( ACTIVE, INACTIVE )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is global coordnator (TRUE) or not (FALSE)</td></tr><tr><td align="left" valign="middle">IS_GROUP_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is group coordnator (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="cb1d377a01eb9832"></a>
### V$CLUSTER_QUEUE

The V$CLUSTER_QUEUE displays a list of all cluster queues.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="3dfae082e3f5522f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the name of the queue</td></tr><tr><td align="left" valign="middle">QUEUED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the number of items currently enqueued</td></tr><tr><td align="left" valign="middle">QUEUE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">size of queue</td></tr><tr><td align="left" valign="middle">TOTAL_QUEUED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of enqueued items</td></tr></tbody></table>

<a id="34f1288631a81e2b"></a>
### V$CLUSTER_SERVER

The V$CLUSTER_SERVER displays a list of all cluster servers.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="0150f4a0a0d23970"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the cluster server</td></tr><tr><td align="left" valign="middle">OS_PROC_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">process identifier of the cluster server in the operating system</td></tr><tr><td align="left" valign="middle">PROCESSED_JOBS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of jobs processed</td></tr><tr><td>STATUS</td><td>VARCHAR(16)</td><td>status of cluster server: the value in( NONE, WAIT, SUSPEND, RUN )</td></tr><tr><td align="left" valign="middle">DRIVER_SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">identifier of the session that orginated the job</td></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position from which the job orginated</td></tr><tr><td>WAIT_EVENT_ID</td><td>NUMBER</td><td>identifier of the wait event (valid only if STATUS is SUSPEND)</td></tr></tbody></table>

<a id="567301c2378df87a"></a>
### V$COLUMNS

The V$COLUMNS has one row for each column of all the performance views (views beginning with V$).

V$COLUMNS를 사용할 수 없는 nomount와 mount 단계에서 performance view의 column 정보를 조회하려면 아래 예제와 같이 `\`desc를 사용한다.

```
gSQL> \desc V$INSTANCE

COLUMN_NAME     TYPE                           IS_NULLABLE
--------------- ------------------------------ -----------
RELEASE_VERSION VARCHAR(64)          FALSE      
STARTUP_TIME    TIMESTAMP(6) WITHOUT TIME ZONE FALSE      
INSTANCE_STATUS VARCHAR(16)          FALSE
```

**Column 정보**

<a id="8c4aa152b6967a43"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position (&gt; 0) of the column in the performance view</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the column</td></tr></tbody></table>

<a id="18bdc552731c31d6"></a>
### V$CONTROLFILE

This view displays information about GOLDILOCKS control files.

**Column 정보**

<a id="f2498c988bcd5cbf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">control file status ( VALID, CORRUPTED )</td></tr><tr><td align="left" valign="middle">CONTROLFILE_NAME</td><td align="left" valign="middle">VARCHAR(1152)</td><td align="left" valign="middle">control file name ( absolute path )</td></tr><tr><td align="left" valign="middle">LAST_CHECKPOINT_LSN</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">the last checkpoint lsn</td></tr><tr><td valign="middle">ON_DISK_LSN</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">the minimum lsn of the most recent log that must be contained in the logfile to complete recovery</td></tr><tr><td align="left" valign="middle">IS_PRIMARY</td><td align="left" valign="middle">BOLLEAN</td><td align="left" valign="middle">indicates whether the control file is primary</td></tr></tbody></table>

<a id="c361e3507a9b133f"></a>
### V$DATAFILE

The V$DATAFILE displays information of all datafiles.

**Column 정보**

<a id="a9ed2937458ac63a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">DATAFILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">datafile name ( absolute path )</td></tr><tr><td align="left" valign="middle">CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">LSN at last checkpoint ( null if temporary tablespace )</td></tr><tr><td align="left" valign="middle">CREATION_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">timestamp of the datafile creation</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">datafile size ( in bytes )</td></tr><tr><td align="left" valign="middle">LOADED_CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">checkpoint LSN of the datafile loaded in memory</td></tr><tr><td align="left" valign="middle">CORRUPT_PAGE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">number of corrupt pages in the datafile</td></tr></tbody></table>

<a id="2e9dac6b6b53181a"></a>
### V$DB_CHANGE_TRACKING

The V$DB_CHANGE_TRACKING displays information of database change tracking.

**Column 정보**

<a id="331570b01e75fd2e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLESPACE_ID</td><td align="left">NUMBER</td><td align="left">tablespage identifier</td></tr><tr><td align="left">DATAFILE_ID</td><td>NUMBER</td><td align="left">datafile identifier</td></tr><tr><td>CHANGE_TRACKING_STATE</td><td>VARCHAR(32)</td><td>state of datafile change tracking</td></tr></tbody></table>

<a id="8c7c50b66a2a20eb"></a>
### V$DB_FILE

The V$DB_FILE displays a list of all files using in database.

**Column 정보**

<a id="83ebd3f46db084f1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">FILE_NAME</td><td align="left">VARCHAR(1024)</td><td align="left">file name</td></tr><tr><td align="left">FILE_TYPE</td><td align="left">VARCHAR(16)</td><td align="left">file type</td></tr></tbody></table>

<a id="b51644ad5d756018"></a>
### V$DB_PROPERTY

The V$DB_PROPERTY displays a list of permanent property.

**Column 정보**

<a id="4d3608d9f4d5156d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr><tr><td valign="middle">IS_DEPRECATED</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property is deprecated or not: the value in (TRUE, FALSE)</td></tr><tr><td valign="middle">IS_GLOBAL</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property scope is global or not: the value in (TRUE, FALSE)</td></tr></tbody></table>

<a id="e23c6b6dcb02af8b"></a>
### V$DISPATCHER

The V$DISPATCHER displays information of dispatchers.

**Column 정보**

<a id="9443ca0b4436bcd8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher process identifier</td></tr><tr><td align="left" valign="middle">RESPONSE_JOB_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">response job count</td></tr><tr><td align="left" valign="middle">ACCEPT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">indicates whether this dispatcher is accepting new connections</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">process start time</td></tr><tr><td align="left" valign="middle">CUR_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS_HIGHWATER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">highest number of connections</td></tr><tr><td align="left" valign="middle">MAX_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum connections</td></tr><tr><td align="left" valign="middle">RECV_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">receive status</td></tr><tr><td align="left" valign="middle">RECV_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of received</td></tr><tr><td align="left" valign="middle">RECV_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of received</td></tr><tr><td align="left" valign="middle">RECV_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">RECV_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">send status</td></tr><tr><td align="left" valign="middle">SEND_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of sent</td></tr><tr><td align="left" valign="middle">SEND_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of sent</td></tr><tr><td align="left" valign="middle">SEND_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of send (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of send (1/100 second)</td></tr></tbody></table>

<a id="43658edbe7f84cd6"></a>
### V$ERROR_CODE

The V$ERROR_CODE displays a list of all GOLDILOCKS error codes.

**Column 정보**

<a id="4628f6a5d3dc7976"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ERROR_CODE</td><td align="left">NUMBER</td><td align="left">GOLDILOCKS error code</td></tr><tr><td align="left">SQL_STATE</td><td align="left">VARCHAR(32)</td><td align="left">standard SQLSTATE code</td></tr><tr><td align="left">ERROR_MESSAGE</td><td align="left">VARCHAR(1024)</td><td align="left">error message</td></tr></tbody></table>

<a id="19cc3797a499541a"></a>
### V$GLOBAL_TRANSACTION

The V$GLOBAL_TRANSACTION displays information on the currently active global transactions.

**Column 정보**

<a id="439010daf47b1a4b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">global transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the global transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the global transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">global transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the global transaction is repreparable</td></tr></tbody></table>

<a id="c75f642b2f1c558a"></a>
### V$INCREMENTAL_BACKUP

The V$INCREMENTAL_BACKUP displays information about control files and datafiles in backup sets from the control file.

**Column 정보**

<a id="f07e23ee1ba457f3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BACKUP_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">backup file name ( absolute path )</td></tr><tr><td align="left" valign="middle">BACKUP_SCOPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">incremental backup scope: the value in ( database, tablespace, control )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_LEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">incremental backup level: the value in ( 0, 1, 2, 3, 4 )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">incremental backup type: the value in ( DIFFERENTIAL, CUMULATIVE )</td></tr><tr><td align="left" valign="middle">LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">all changes up to checkpoint LSN are included in this backup</td></tr><tr><td align="left" valign="middle">BEGIN_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup beginning time</td></tr><tr><td align="left" valign="middle">COMPLETION_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup completion time</td></tr></tbody></table>

<a id="9cedd68d40772aa2"></a>
### V$INSTANCE

This view displays the state of the current instance.

**Column 정보**

<a id="f5a7696dccb975fc"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">RELEASE_VERSION</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">release version</td></tr><tr><td align="left" valign="middle">STARTUP_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">time when the instance was started</td></tr><tr><td align="left" valign="middle">INSTANCE_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">status of the instance: the value in ( STARTED, MOUNTED, OPEN )</td></tr></tbody></table>

<a id="62f7b27a3558c852"></a>
### V$JOURNALING

The V$JOURNALING displays journaling information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="1e17ddc5caebe8dd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">table name</td></tr><tr><td align="left">SHARD_ID</td><td align="left">NUMBER</td><td align="left">shard identifier</td></tr><tr><td align="left">RECORD_COUNT</td><td align="left">NUMBER</td><td align="left">journaled record count</td></tr><tr><td align="left">TOTAL_SIZE</td><td align="left">NUMBER</td><td align="left">total size of journaled records (byte)</td></tr></tbody></table>

<a id="439efe20f50404cf"></a>
### V$KEYWORDS

The V$KEYWORDS displays a list of all SQL keywords.

**Column 정보**

<a id="dbf309f9569723f6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">KEYWORD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of keyword</td></tr><tr><td align="left" valign="middle">KEYWORD_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">length of the keyword</td></tr><tr><td align="left" valign="middle">IS_RESERVED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the keyword cannot be used as an identifier (TRUE) or whether the keyword is not reserved (FALSE)</td></tr></tbody></table>

<a id="ed7103f33d8ddfb1"></a>
### V$LATCH

The V$LATCH shows latch information.

**Column 정보**

<a id="c689d45405748224"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">LATCH_DESCRIPTION</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">latch description</td></tr><tr><td align="left" valign="middle">REF_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">reference count</td></tr><tr><td align="left" valign="middle">SPIN_LOCK</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the spin lock is locked ( YES ) or not ( NO )</td></tr><tr><td align="left" valign="middle">WAIT_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">wait count</td></tr><tr><td align="left" valign="middle">CURRENT_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">current latch mode: the value in ( INITIAL, SHARED, EXCLUSIVE )</td></tr></tbody></table>

<a id="53035315feb0ad0c"></a>
### V$LICENSE

The V$LICENSE displays information of current license.

**Column 정보**

<a id="b72696c76b0e85f8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td>LICENSE_TYPE</td><td align="left">VARCHAR(8)</td><td>license type</td></tr><tr><td>START_DATE</td><td>DATE</td><td>start date of the license</td></tr><tr><td>EXPIRE_DATE</td><td>DATE</td><td>expire date of the license</td></tr></tbody></table>

<a id="526855f30ad5a017"></a>
### V$LOGFILE

The V$LOGFILE displays information of all redo log members.

**Column 정보**

<a id="e9e164b5eb93fddb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">redo log group identifier</td></tr><tr><td align="left" valign="middle">FILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">name of the log member</td></tr><tr><td align="left" valign="middle">GROUP_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the log group: the value in ( UNUSED, ACTIVE, CURRENT, INACTIVE )</td></tr><tr><td align="left" valign="middle">FILE_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file sequence number of the log member</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file size of the log member ( in bytes )</td></tr></tbody></table>

<a id="c270548a9fba5427"></a>
### V$LOCK_WAIT

This view lists the locks currently held and outstanding requests for a lock.

**Column 정보**

<a id="65b2f36d7dcb4686"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GRANT_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that holds the lock</td></tr><tr><td align="left">REQUEST_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that requests the lock</td></tr></tbody></table>

<a id="3f3fee4ed0e3e325"></a>
### V$LOCKED_OBJECT

This view shows locked object information.

**Column 정보**

<a id="b9b83c4b79ab234d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">LOCK_SLOT_ID</td><td align="left">NUMBER</td><td align="left">lock slot identifier</td></tr><tr><td align="left">TABLE_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">owner name who owns the locked table</td></tr><tr><td>TABLE_SCHEMA</td><td>VARCHAR(128)</td><td align="left">schema of the locked table</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">locked table name</td></tr><tr><td>LOCK_MODE</td><td>VARCHAR(8)</td><td>granted lock mode (IS, IX, S, X, SIX)</td></tr></tbody></table>

<a id="c3b87f037d9a936e"></a>
### V$OPEN_CURSOR

The view lists display cursor status information for each current session.

**Column 정보**

<a id="9014a67584f0a23c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td>ID of the session</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td>NAME of the user</td></tr><tr><td align="left">CURSOR_NAME</td><td align="left">VARCHAR(128)</td><td>NAME of the cursor</td></tr><tr><td align="left">PSM_CURSOR_ID</td><td align="left">NUMBER</td><td>ID of the PSM cursor</td></tr><tr><td>SQL_TEXT</td><td>LONG VARCHAR</td><td>SQL text for the cursor</td></tr><tr><td>IS_PSM_CURSOR</td><td>BOOLEAN</td><td>is PSM cursor</td></tr><tr><td>IS_OPEN</td><td>BOOLEAN</td><td>is open</td></tr><tr><td>OPEN_TIME</td><td>TIMESTAMP(6) WITHOUT TIME ZONE</td><td>cursor open time</td></tr><tr><td>LAST_EXEC_TIME</td><td>NATIVE_BIGINT</td><td>last execution time(us)</td></tr><tr><td>IS_SENSITIVE</td><td>BOOLEAN</td><td>is sensitive</td></tr><tr><td>IS_SCROLLABLE</td><td>BOOLEAN</td><td>is scrollable</td></tr><tr><td>IS_HOLDABLE</td><td>BOOLEAN</td><td>is holdable</td></tr><tr><td>IS_UPDATABLE</td><td>BOOLEAN</td><td>is updatable</td></tr></tbody></table>

<a id="393099f4d5ef70ef"></a>
### V$PLAN_HISTORY

The V$PLAN_HISTORY displays information of SQL plans.

**Column 정보**

<a id="913a19c5111bf6ad"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">DRIVER_SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver session identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">STMT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement identifier in a session</td></tr><tr><td align="left" valign="middle">CL_STMT_ID</td><td>NUMBER</td><td>cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">DRIVER_CL_STMT_ID</td><td>NUMBER</td><td>driver cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_POS</td><td>NUMBER</td><td align="left" valign="middle">plan history position</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_ID</td><td>NUMBER</td><td>plan history identifier</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">SQL text for the statement</td></tr><tr><td align="left" valign="middle">PLAN_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">plan text for the statement</td></tr><tr><td align="left" valign="middle">LAST_EXEC_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement last execution time</td></tr></tbody></table>

<a id="a1012ed8d3bc99bd"></a>
### V$PLAN_HISTORY_LATEST

The V$PLAN_HISTORY_LATEST displays information of the latest SQL plan.

**Column 정보**

<a id="da4eb16b8543879f"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">DRIVER_SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver session identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">STMT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement identifier in a session</td></tr><tr><td align="left" valign="middle">CL_STMT_ID</td><td>NUMBER</td><td>cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">DRIVER_CL_STMT_ID</td><td>NUMBER</td><td>driver cluster statement identifier in a session</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_POS</td><td>NUMBER</td><td align="left" valign="middle">plan history position</td></tr><tr><td align="left" valign="middle">PLAN_HISTORY_ID</td><td>NUMBER</td><td>plan history identifier</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">SQL text for the statement</td></tr><tr><td align="left" valign="middle">PLAN_TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">plan text for the statement</td></tr><tr><td align="left" valign="middle">LAST_EXEC_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement last execution time</td></tr></tbody></table>

<a id="68d6afd926f9af6d"></a>
### V$PROCESS_STAT

The V$PROCESS_STAT displays goldilocks process statistics.

**Column 정보**

<a id="f50e3dab3ea3bc1a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="c86c5fe63372881a"></a>
### V$PROCESS_MEM_STAT

The V$PROCESS_MEM_STAT displays goldilocks process memory statistics.

**Column 정보**

<a id="e0bf47bf6efb8bb0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="e010d661c36f0ccb"></a>
### V$PROCESS_SQL_STAT

The V$PROCESS_SQL_STAT displays goldilocks process SQL statistics.

**Column 정보**

<a id="94d6ff57c2abe238"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="2432f4ad05878988"></a>
### V$PROPERTY

The V$PROPERTY displays a list of all properties at current session. Otherwise, the instance-wide value.

**Column 정보**

<a id="8f68e78e174f36b3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the session</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr><tr><td valign="middle">IS_DEPRECATED</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property is deprecated or not: the value in (TRUE, FALSE)</td></tr><tr><td valign="middle">IS_GLOBAL</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property scope is global or not: the value in (TRUE, FALSE)</td></tr></tbody></table>

<a id="99c885211178e083"></a>
### V$PROPERTY_ALIAS

The V$PROPERTY_ALIAS displays a list of all properties alias.

**Column 정보**

<a id="663ef49c831f73a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">original name of the property</td></tr><tr><td align="left" valign="middle">PROPERTY_ALIAS</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">alias name of the property</td></tr></tbody></table>

<a id="abdb28833e567315"></a>
### V$PSM_RESERVED_WORDS

The V$PSM_RESERVED_WORDS displays a list of all PSM reserved keywords. Reserved words cannot be used in variable name or procedure name.

**Column 정보**

<a id="a2f7b2dc23ed6361"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| KEYWORD_NAME | VARCHAR(128) | name of keyword |
| KEYWORD_LENGTH | NUMBER | length of the keyword |

<a id="0bcfa3540ec25f3e"></a>
### V$QUEUE

The V$QUEUE displays information of queue.

**Column 정보**

<a id="05b808a50a3af4ed"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TYPE</td><td align="left">NUMBER</td><td align="left">queue type ( COMMON or DISPATCHER )</td></tr><tr><td align="left">INDEX</td><td align="left">NUMBER</td><td align="left">index</td></tr><tr><td align="left">QUEUED</td><td align="left">NUMBER</td><td align="left">number of items in the queue</td></tr><tr><td align="left">WAIT</td><td align="left">NUMBER</td><td align="left">total time that all items in this queue have waited (1/100 second)</td></tr><tr><td align="left">TOTALQ</td><td align="left">VARCHAR(128)</td><td align="left">total number of items that have ever been in the queue</td></tr></tbody></table>

<a id="968718f4c44e1f4a"></a>
### V$RELATION

The V$RELATION displays information of all relations

**Column 정보**

<a id="8761e2e40087baf2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the relation</td></tr><tr><td align="left" valign="middle">TBS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier</td></tr><tr><td valign="middle">PHYSICAL_ID</td><td valign="middle">NUMBER</td><td valign="middle">physical identifier of the relation</td></tr><tr><td align="left" valign="middle">TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">type of the relation: values in ( TABLE, BTREE INDEX, GLOBAL SECONDARY INDEX )</td></tr><tr><td valign="middle">USABLE</td><td valign="middle">BOOLEAN</td><td valign="middle">indicates whether the relation is usable or not</td></tr><tr><td align="left" valign="middle">ALLOC_PAGE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">number of pages currently allocated</td></tr><tr><td align="left" valign="middle">GLOBAL_SCN</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">global scn of the relation: only available for the TABLE type</td></tr></tbody></table>

<a id="ebd95a0e07bb165b"></a>
### V$RESERVED_WORDS

The V$RESERVED_WORDS displays a list of all SQL reserved keywords. Reserved words cannot be used in table name or column name.

**Column 정보**

<a id="7211802e6d4396dd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">KEYWORD_NAME</td><td align="left">VARCHAR(128)</td><td align="left">name of keyword</td></tr><tr><td align="left">KEYWORD_LENGTH</td><td align="left">NUMBER</td><td align="left">length of the keyword</td></tr></tbody></table>

<a id="c8410885b14eee59"></a>
### V$SEQUENCE

The V$SEQUENCE displays information of sequences

**Column 정보**

<a id="4c4991a4c0373e12"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">PHYSICAL_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence physical identifier</td></tr><tr><td align="left" valign="middle">START_WITH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">start with value</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">increment value</td></tr><tr><td align="left" valign="middle">MAXVALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value</td></tr><tr><td align="left" valign="middle">MINVALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">cache size</td></tr><tr><td align="left" valign="middle">LOCAL_NEXT_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local next value</td></tr><tr><td align="left" valign="middle">LOCAL_CURR_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local current value</td></tr><tr><td align="left" valign="middle">RESTART_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">restart value</td></tr><tr><td align="left" valign="middle">CYCLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">allow cycle</td></tr><tr><td align="left" valign="middle">USE_LAST_VALUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">use last value or not</td></tr><tr><td align="left" valign="middle">LOCAL_CACHE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current local cache count</td></tr><tr><td align="left" valign="middle">GLOBAL_NEXT_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">global next cache chunk start value</td></tr><tr><td align="left" valign="middle">SYNC_COMPARE_SN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">serial number for global sequence synchronization</td></tr><tr><td valign="middle">IS_ONLINE</td><td valign="middle">BOOLEAN</td><td valign="middle">is online</td></tr><tr><td valign="middle">LAST_SYNC_TIME</td><td valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td valign="middle">last time the sequence was synchronized</td></tr></tbody></table>

<a id="9096d5ab0a597825"></a>
### V$SESSION

The V$SESSION displays session information for each current session.

**Column 정보**

<a id="a16a27c90aa3bc4a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier ( -1 if inactive transaction )</td></tr><tr><td align="left" valign="middle">CONNECTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">connection type: the value in ( DA, TCP )</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name</td></tr><tr><td align="left" valign="middle">SESSION_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">status of the session: the value in ( CONNECTED, SIGNALED, SNIPED, DEAD )</td></tr><tr><td align="left" valign="middle">SERVER_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">server type: the value in ( DEDICATED, SHARED )</td></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client process identifier</td></tr><tr><td align="left" valign="middle">LOGON_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">logon time</td></tr><tr><td align="left" valign="middle">PROGRAM_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">program name</td></tr><tr><td align="left" valign="middle">CLIENT_ADDRESS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">client address ( null if DA )</td></tr><tr><td align="left" valign="middle">CLIENT_PORT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client port ( 0 if DA )</td></tr><tr><td align="left" valign="middle">FAILOVER_TYPE</td><td align="left" valign="middle">VARCHAR(13)</td><td align="left" valign="middle">indicates whether and to what extent transparent application failover (TAF) is enabled for the session ( NONE, SESSION )</td></tr><tr><td align="left" valign="middle">FAILED_OVER</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is running in failover mode and failover has occurred (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IS_AUDITED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is audited (YES) or not (NO)</td></tr></tbody></table>

<a id="e622453afb4651f0"></a>
### V$SESSION_AUDIT

The V$SESSION_AUDIT displays audited session information.

**Column 정보**

<a id="fb65bb68924a81f6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">active audit policy name</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="f293550e886558a0"></a>
### V$SESSION_CONNECT_INFO

The V$SESSION_CONNECT_INFO displays information about network connections for the current session.

**Column 정보**

<a id="9ede840336ed930c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">SERIAL_NO</td><td align="left">NUMBER</td><td align="left">session serial number</td></tr><tr><td align="left">CLIENT_CHARSET</td><td align="left">VARCHAR(40)</td><td align="left">client character set</td></tr></tbody></table>

<a id="86a28d80dde087fd"></a>
### V$SESSION_EVENT

The V$SESSION_EVENT displays information on waits for an event by a session.

**Column 정보**

<a id="dbd0a77e89b8dcda"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID of the session</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Identifier of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Name of the wait event</td></tr><tr><td align="left" valign="middle">TOTAL_WAITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Total number of waits for the event</td></tr><tr><td align="left" valign="middle">TOTAL_TIMEOUTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Total number of timeouts for the event</td></tr><tr><td align="left" valign="middle">TIME_WAITED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left" valign="middle">AVERAGE_WAIT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left" valign="middle">MAX_WAIT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum time waited for the event by the session (microsecond)</td></tr><tr><td align="left" valign="middle">CLASS_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Name of the class of the wait event</td></tr></tbody></table>

<a id="ffc97c53e841a4ec"></a>
### V$SESSION_STAT

The V$SESSION_STAT displays session statistics.

**Column 정보**

<a id="ad79ee566d748930"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="622e1801ba146da2"></a>
### V$SESSION_MEM_STAT

The V$SESSION_MEM_STAT displays session memory statistics.

**Column 정보**

<a id="5b94ebbbe3fbb5a5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="64567f02bc7c9d4a"></a>
### V$SESSION_MEM_USAGE

The V$SESSION_MEM_USAGE displays session memory usage for each session.

**Column 정보**

<a id="690cbd592b309543"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">ALLOCATOR_ID</td><td align="left">NUMBER</td><td align="left">memory allocator identifier</td></tr><tr><td>PARENT_ALLOCATOR_ID</td><td>NUMBER</td><td>parent memory allocator identifier</td></tr><tr><td align="left">ALLOCATOR_TYPE</td><td align="left">VARCHAR(7)</td><td align="left">memory allocator type ( REGION or DYNAMIC )</td></tr><tr><td>MEMORY_TYPE</td><td>VARCHAR(4)</td><td>memory type ( HEAP, SHM )</td></tr><tr><td>TOTAL_SIZE</td><td>NUMBER</td><td>total memory size</td></tr><tr><td>USED_SIZE</td><td>NUMBER</td><td>used memory size</td></tr></tbody></table>

<a id="cad8de6476008d04"></a>
### V$SESSION_SQL_STAT

The V$SESSION_SQL_STAT displays session SQL statistics.

**Column 정보**

<a id="a6c2e00dc0353247"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="916f3c6bbc93eb7a"></a>
### V$SESSION_WAIT

The V$SESSION_WAIT displays the current or last wait for each session.

**Column 정보**

<a id="bbf8701612d8f9cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID of the session</td></tr><tr><td align="left" valign="middle">SEQ_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Identifier of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Name of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">A number that uniquely identifies the current or last wait (incremented for each wait)</td></tr><tr><td align="left" valign="middle">P1TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the first parameter for the wait event</td></tr><tr><td align="left" valign="middle">P1</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">First wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P1HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">First wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P2TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the second parameter for the wait event</td></tr><tr><td align="left" valign="middle">P2</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Second wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P2HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Second wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P3TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the third parameter for the wait event</td></tr><tr><td align="left" valign="middle">P3</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Third wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P3HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Third wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">STATE</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Wait state</td></tr><tr><td align="left" valign="middle">WAIT_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the session is currently waiting, then the value is time waited for the current wait. If the session is not in a wait, then the value is the duration of the last wait (in microseconds)</td></tr><tr><td align="left" valign="middle">TIME_SINCE_LAST_WAIT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Time elapsed since the end of the last wait (in microseconds). If the session is currently in a wait, then the value is 0.</td></tr><tr><td align="left" valign="middle">CLASS_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Name of the class of the wait event</td></tr></tbody></table>

<a id="bed6d58e3f4fdbc2"></a>
### V$SHARED_MODE

The V$SHARED_MODE displays information of shared mode.

**Column 정보**

<a id="a70124eabe0c00d6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">name</td></tr><tr><td align="left">VALUE</td><td align="left">VARCHAR(128)</td><td align="left">value</td></tr></tbody></table>

<a id="f49bdc1ffaa700e1"></a>
### V$SHARED_SERVER

The V$SHARED_SERVER displays information of shared servers.

**Column 정보**

<a id="02abc0155a16e760"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">shared server process identifier</td></tr><tr><td align="left" valign="middle">PROCESSED_JOB_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">processed job count</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">status</td></tr><tr><td align="left" valign="middle">IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time (1/100 second)</td></tr><tr><td align="left" valign="middle">BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time (1/100 second)</td></tr><tr><td valign="middle">REQUEST_GROUP_ID</td><td valign="middle">NUMBER</td><td valign="middle">indicates which shared group the shared server belongs to</td></tr><tr><td valign="middle">WAIT_EVENT_ID</td><td valign="middle">NUMBER</td><td valign="middle">identifier of the wait event (valid only if STATUS is SUSPEND)</td></tr></tbody></table>

<a id="31c64f4833196b90"></a>
### V$SHM_SEGMENT

The V$SHM_SEGMENT displays a list of all shared memory segments.

**Column 정보**

<a id="e59c72b521a04b41"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SHM_NAME</td><td align="left">VARCHAR(32)</td><td align="left">shared memory segment name</td></tr><tr><td align="left">SHM_ID</td><td align="left">NUMBER</td><td align="left">shared memory segment identifier</td></tr><tr><td align="left">SHM_SIZE</td><td align="left">NUMBER</td><td align="left">shared memory segment size ( in bytes )</td></tr><tr><td align="left">SHM_KEY</td><td align="left">NUMBER</td><td align="left">shared memory segment key</td></tr><tr><td align="left">SHM_SEQ</td><td align="left">NUMBER</td><td align="left">shared memory segment sequence</td></tr><tr><td align="left">SHM_ADDR</td><td align="left">VARCHAR(32)</td><td align="left">start address of the shared memory segment</td></tr><tr><td>LARGE_PAGES</td><td>BOOLEAN</td><td>indicates whether the shared memory segment use large pages</td></tr></tbody></table>

<a id="8f509aad7adf5f5b"></a>
### V$SPROPERTY

The V$SPROPERTY displays a list of Properties. This is store a binary property file.

**Column 정보**

<a id="10221e995cf09d80"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value stored in the binary property file</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value is BINARY_FILE</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the system</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr><tr><td valign="middle">IS_DEPRECATED</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property is deprecated or not: the value in (TRUE, FALSE)</td></tr><tr><td valign="middle">IS_GLOBAL</td><td valign="middle">VARCHAR(32)</td><td valign="middle">whether a property scope is global or not: the value in (TRUE, FALSE)</td></tr></tbody></table>

<a id="943f74e153aae95f"></a>
### V$SQLFN_METADATA

The V$SQLFN_METADATA contains metadata about operators and built-in functions.

**Column 정보**

<a id="98c7abc866a4acd3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FUNC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the built-in function</td></tr><tr><td align="left" valign="middle">MINARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum number of arguments for the function</td></tr><tr><td align="left" valign="middle">MAXARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum number of arguments for the function</td></tr><tr><td align="left" valign="middle">IS_AGGREGATE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the function is an aggregate function (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="752ef279734cff3f"></a>
### V$SQL_CACHE

The V$SQL_CACHE lists statistics of shared SQL plan.

**Column 정보**

<a id="9461fd45a621d829"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SQL_HANDLE</td><td align="left">NUMBER</td><td align="left">SQL handle</td></tr><tr><td align="left">HASH_VALUE</td><td align="left">NUMBER</td><td align="left">hash value of the SQL statement</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">CLOCK_ID</td><td align="left">NUMBER</td><td align="left">clock identifier</td></tr><tr><td align="left">PLAN_AGE</td><td align="left">NUMBER</td><td align="left">plan age</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">user name</td></tr><tr><td align="left">BIND_PARAM_COUNT</td><td align="left">NUMBER</td><td align="left">count of bind parameters</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">SQL full text</td></tr><tr><td align="left">PLAN_COUNT</td><td align="left">NUMBER</td><td align="left">plan count of the SQL statement</td></tr><tr><td align="left">PLAN_ID</td><td align="left">NUMBER</td><td align="left">plan identifier</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">PLAN_IS_ATOMIC</td><td align="left">BOOLEAN</td><td align="left">plan is atomic array insert or not</td></tr><tr><td align="left">PLAN_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">plan text for SQL statement</td></tr></tbody></table>

<a id="06a20c22eb22471a"></a>
### V$SQL_COMMAND

The V$SQL_COMMAND lists attribute information of each SQL command.

**Column 정보**

<a id="81f2db1c8798be9e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">COMMAND</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">SQL command</td></tr><tr><td align="left" valign="middle">FROM_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable from start-up phase</td></tr><tr><td align="left" valign="middle">UNTIL_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable until start-up phase</td></tr><tr><td align="left" valign="middle">ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database access mode: values in (NONE, READ &amp; WRITE, READ, READ &amp; LOCK)</td></tr><tr><td align="left" valign="middle">NEED_FETCH</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the command is a query which has result set and need fetch</td></tr><tr><td align="left" valign="middle">IS_DDL</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is a DDL(Data Definition Language) or not</td></tr><tr><td valign="middle">CLUSTER_LOCK_MODE</td><td valign="middle">VARCHAR(32)</td><td valign="middle">cluster lock mode: values in (NONE, SERIAL, MANUAL)</td></tr><tr><td align="left" valign="middle">AUTO_COMMIT</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is auto-commit or not</td></tr><tr><td align="left" valign="middle">IS_CACHEABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is plan-cacheable or not</td></tr><tr><td align="left" valign="middle">AUDIT_ACTION</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">auditiable action name for the SQL command</td></tr></tbody></table>

<a id="b43b389d38fa0c9b"></a>
### V$SQL_HISTORY

The V$SQL_HISTORY displays information of SQLs.

**Column 정보**

<a id="053848cf7c005092"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement start time</td></tr><tr><td align="left" valign="middle">EXEC_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">execution time(us)</td></tr><tr><td align="left" valign="middle">PREPARED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is prepared ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">SUCCESS</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is success ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">CHARACTER VARYING(16)</td><td align="left" valign="middle">status of the statement: the value in<br>( RUNNING, DONE )</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">CHARACTER VARYING(1024)</td><td align="left" valign="middle">first 1024 bytes of the SQL text for the statement</td></tr></tbody></table>

<a id="b49784483d3afdaf"></a>
### V$STATEMENT

The V$STATEMENT lists all statements.

**Column 정보**

<a id="49065a11f9d3aa82"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">STMT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement identifier in a session</td></tr><tr><td align="left" valign="middle">STMT_VIEW_SCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">statement view scn</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">first 1024 bytes of the SQL text for the statement</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement start time</td></tr><tr><td valign="middle">TOTAL_EXEC_TIME</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">total execution time(us)</td></tr><tr><td valign="middle">LAST_EXEC_TIME</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">last execution time(us)</td></tr><tr><td valign="middle">EXECUTIONS</td><td valign="middle">NATIVE_BIGINT</td><td valign="middle">number of executions</td></tr></tbody></table>

<a id="3aeef7ff0e6515be"></a>
### V$SYSTEM_EVENT

The V$SYSTEM_EVENT displays information on total waits for an event.

**Column 정보**

<a id="fea0b96fd24fa215"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="ed8419eb87ee3806"></a>
### V$SYSTEM_STAT

The V$SYSTEM_STAT displays system statistics.

**Column 정보**

<a id="010763a6b6c64a51"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="6908e31e3c19645e"></a>
### V$SYSTEM_MEM_STAT

The V$SYSTEM_MEM_STAT displays system memory statistics.

**Column 정보**

<a id="81f0b1d3a46721ee"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="8bcd9e213eee5184"></a>
### V$SYSTEM_SQL_STAT

The V$SYSTEM_SQL_STAT displays system SQL statistics.

**Column 정보**

<a id="ae127f20f07f1588"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="a6db4681b39b773f"></a>
### V$TABLES

The V$TABLES contains the definitions of all the performance views (views beginning with V$).

**Column 정보**

<a id="12342734a623a4bd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">visible startup phase of the performance view</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>created time of the performance view</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>modified time of the performance view</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>comments of the performance view</td></tr></tbody></table>

<a id="c33cd02ea5b4e280"></a>
### V$TABLESPACE

This view displays tablespace information.

**Column 정보**

<a id="c3d0dd3dbb7a76a7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">TBS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier</td></tr><tr><td align="left" valign="middle">TBS_ATTR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace attribute: the value in ( device attribute (MEMORY) | temporary attribute (TEMPORARY, PERSISTENT) | usage attribute(DICT, UNDO, DATA, TEMPORARY) )</td></tr><tr><td align="left" valign="middle">IS_LOGGING</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is a logging tablespace ( YES ) or not ( NO )</td></tr><tr><td align="left" valign="middle">IS_ONLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is ONLINE ( YES ) or OFFLINE ( NO )</td></tr><tr><td align="left" valign="middle">OFFLINE_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">indicates whether the tablespace can be taken online normally ( CONSISTENT ) or not ( INCONSISTENT ). null if the tablespace is ONLINE</td></tr><tr><td align="left" valign="middle">EXTENT_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">extent size of the tablespace ( in bytes )</td></tr><tr><td align="left" valign="middle">PAGE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="a61c7f85a77129b6"></a>
### V$TABLESPACE_STAT

This view displays tablespace statistical information.

**Column 정보**

<a id="3099d57e96fa9b65"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TBS_NAME</td><td align="left">VARCHAR(128)</td><td align="left">tablespace name</td></tr><tr><td align="left">TBS_ID</td><td align="left">NUMBER</td><td align="left">tablespace identifier</td></tr><tr><td align="left">TOTAL_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">total extent count of the tablespace</td></tr><tr><td align="left">USED_META_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">meta extent count currently used on the tablespace</td></tr><tr><td align="left">USED_DATA_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">data extent count currently used on the tablespace</td></tr><tr><td align="left">FREE_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">free extent count of the tablespace</td></tr><tr><td align="left">EXTENT_SIZE</td><td align="left">NUMBER</td><td align="left">extent size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="0970c7bb710b15d4"></a>
### V$TCL_LOGFILE

The V$TCL_LOGFILE displays information of all TCL(tranaction commit log) members.

**Column 정보**

<a id="e4b7622732c5e546"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">group identifier of the TCL member</td></tr><tr><td align="left" valign="middle">FILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">file path of the TCL member</td></tr><tr><td align="left" valign="middle">GROUP_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the TCL group: the value in ( UNUSED, ACTIVE, CURRENT, INACTIVE )</td></tr><tr><td align="left" valign="middle">FILE_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file sequence number of the TCL member</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file size of the TCL member ( in bytes )</td></tr></tbody></table>

<a id="32b24d3b64fcb10b"></a>
### V$TRANSACTION

The V$TRANSACTION lists the active transactions in the system.

**Column 정보**

<a id="eea6b2512ad5fd19"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier ( null if the global transaction is unassociated )</td></tr><tr><td align="left" valign="middle">TRANS_SLOT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction slot identifier</td></tr><tr><td align="left" valign="middle">PHYSICAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">physical transaction identifier</td></tr><tr><td align="left" valign="middle">TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction state: the value in ( ACTIVE, BLOCK, PREPARE, COMMIT, ROLLBACK, IDLE, PRECOMMIT )</td></tr><tr><td>IS_XA</td><td align="left" valign="middle">BOOLEAN</td><td>indicates whether the transaction is xa transaction or not</td></tr><tr><td align="left" valign="middle">TRANS_ATTRIBUTE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction attribute: the value in ( READ_ONLY, UPDATABLE, LOCKABLE, UPDATABLE | LOCKABLE )</td></tr><tr><td align="left" valign="middle">ISOLATION_LEVEL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction isolation level: the value in ( READ COMMITTED, SERIALIZABLE )</td></tr><tr><td align="left" valign="middle">TRANS_VIEW_SCN</td><td>VARCHAR(32)</td><td align="left" valign="middle">transaction view scn</td></tr><tr><td align="left" valign="middle">TCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction change number</td></tr><tr><td align="left" valign="middle">TRANS_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction sequence number</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">transaction start time</td></tr><tr><td valign="middle">UNDO_SEGMENT_ID</td><td valign="middle">NUMBER</td><td valign="middle">undo segment identifier</td></tr></tbody></table>

<a id="426d35a70c53845c"></a>
### V$UNDO_SEGMENT

The V$UNDO_SEGMENT displays a list of all undo segments.

**Column 정보**

<a id="f4fd1d76e2b0f911"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ID</td><td align="left">NUMBER</td><td align="left">logical identifier of undo segment</td></tr><tr><td align="left">PHYSICAL_ID</td><td align="left">NUMBER</td><td align="left">physical identifier of undo segment</td></tr><tr><td align="left">PAGES</td><td align="left">NUMBER</td><td align="left">total number of allocated pages</td></tr><tr><td>AGABLE_PAGES</td><td>NUMBER</td><td>total number of agable pages</td></tr></tbody></table>

<a id="f86a8ce21b44ac96"></a>
### V$WAIT_EVENT_CLASS_NAME

The V$WAIT_EVENT_CLASS_NAME displays information about Class of wait event.

**Column 정보**

<a id="a3f12c14aea1c416"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the class of the wait event</td></tr></tbody></table>

<a id="9f1a44a9403cd824"></a>
### V$WAIT_EVENT_NAME

The V$WAIT_EVENT_NAME displays information about wait events.

**Column 정보**

<a id="b54bb5943b209f8f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the first parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the second parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the third parameter for the wait event</td></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="6aa3b1129f860b99"></a>
### V$XA_TRANSACTION

The V$XA_TRANSACTION displays information on the currently active XA transactions.

**Column 정보**

<a id="76f8f629c8a51666"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">XA_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">XA transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td valign="middle">DRIVER_TRANS_ID</td><td valign="middle">NUMBER</td><td valign="middle">driver transaction identifier</td></tr><tr><td valign="middle">DRIVER_MEMBER_POS</td><td valign="middle">NUMBER</td><td valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">XA_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the XA transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the XA transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">XA transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the XA transaction is repreparable</td></tr></tbody></table>

---

[← 8. GOLDILOCKS 데이터베이스 이중화](8-goldilocks-데이터베이스-이중화.md) · [전체 목차](../README.md) · [10. Server Property →](10-server-property.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
