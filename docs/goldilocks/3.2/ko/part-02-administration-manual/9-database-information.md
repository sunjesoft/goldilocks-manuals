<a id="86f373fa6f1f5339"></a>

# 9. Database Information

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/86f373fa6f1f5339)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 8. GOLDILOCKS 데이터베이스 이중화](8-goldilocks-데이터베이스-이중화.md) · [전체 목차](../README.md) · [10. Server Property →](10-server-property.md)

<a id="ef9643afcec18f44"></a>
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
    - USER_ 로 시작하는 이름을 가진 view
    - 현재 사용자가 소유한 객체에 대한 정보

<a id="d5ad856d0be4035b"></a>
### ALL 계열 View

현재 사용자가 접근 가능한 객체에 대한 정보를 얻을 수 있다.

<a id="88eb31a28589adaa"></a>
#### ALL_ALL_TABLES

ALL_ALL_TABLES describes the object tables and relational tables accessible to the current user.

**Column 정보**

<a id="1d31e6695f4deb06"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="d329f1ef96e30df5"></a>
#### ALL_ARGUMENTS

ALL_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="c239518060de3f36"></a>
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

<a id="6680fc64e0629366"></a>
#### ALL_CATALOG

ALL_CATALOG displays the tables, views, synonyms, and sequences accessible to the current user.

**Column 정보**

<a id="037a52014ade9f0d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_NAME | VARCHAR(128) | Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |
| TABLE_TYPE | VARCHAR(32) | Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED |

<a id="428e93d86a2d4c50"></a>
#### ALL_CLUSTER_TABLES

ALL_CLUSTER_TABLES describes all cluster tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="f105db77e4f86b75"></a>
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

<a id="23591c0883ff6fa0"></a>
#### ALL_COL_COMMENTS

ALL_COL_COMMENTS displays comments on the columns of the tables and views accessible to the current user.

**Column 정보**

<a id="99152fa2245ad1b7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the object |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the object |
| TABLE_NAME | VARCHAR(128) | Name of the object |
| COLUMN_NAME | VARCHAR(128) | Name of the column |
| COMMENTS | VARCHAR(1024) | Comment on the column |

<a id="795c0a2937ebbd0e"></a>
#### ALL_COL_PRIVS

ALL_COL_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="2d42b37a270e6668"></a>
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

<a id="298639d1e39f59c7"></a>
#### ALL_COL_PRIVS_MADE

ALL_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner or grantor.

**Column 정보**

<a id="2fd416514bc07156"></a>
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

<a id="791616b2208f8265"></a>
#### ALL_COL_PRIVS_RECD

ALL_COL_PRIVS_RECD describes the column object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="b28e1f75c0ce33e1"></a>
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

<a id="20001d1c31d2c9bf"></a>
#### ALL_CONSTRAINTS

ALL_CONSTRAINTS describes constraint definitions on tables accessible to the current user.

**Column 정보**

<a id="e9a1538c28de1774"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;CONSTRAINT_TYPE</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;TABLE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">&nbsp;SEARCH_CONDITION</td><td align="left" valign="middle">&nbsp;LONG VARCHAR</td><td align="left" valign="middle">&nbsp;Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">&nbsp;R_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;R_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;R_CONSTRAINT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">&nbsp;DELETE_RULE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">&nbsp;UPDATE_RULE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">&nbsp;STATUS</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">&nbsp;DEFERRABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">&nbsp;DEFERRED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">&nbsp;VALIDATED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">&nbsp;GENERATED</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">&nbsp;BAD</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">&nbsp;RELY</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_CHANGE</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INDEX_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">&nbsp;INVALID</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="05abb0b0bc2410a9"></a>
#### ALL_CONS_COLUMNS

ALL_CONS_COLUMNS describes columns that are accessible to the current user and that are specified in constraints.

**Column 정보**

<a id="de6a9339d9309363"></a>
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

<a id="70f239a552622843"></a>
#### ALL_DB_PRIVS

ALL_DB_PRIVS describes the database grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="4e7a1b872d57149b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="f63cef9b62fc9a35"></a>
#### ALL_DB_PRIVS_MADE

ALL_DB_PRIVS_MADE describes the database grants for which the current user is the grantor.

**Column 정보**

<a id="25e2d5b0d6cf08e4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="9e0501646a16bcaa"></a>
#### ALL_DB_PRIVS_RECD

ALL_DB_PRIVS_RECD describes the database grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="f04c7272b903f1d4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| PRIVILEGE | VARCHAR(32) | Privilege on the database |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="528675dc0fbedf60"></a>
#### ALL_DEPENDENCIES

ALL_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column 정보**

<a id="c736f41b3ee2e1d4"></a>
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

<a id="905c0ccf6530ae90"></a>
#### ALL_GLOBAL_SECONDARY_INDEXES

ALL_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables accessible to the current user.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="4500f2e9b3aa9799"></a>
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

<a id="7c8669e22ba75bb6"></a>
#### ALL_GSI_PLACE

ALL_GSI_PLACE describes node placement of all global secondary indexes on the tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="876a70afde60b86c"></a>
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

<a id="18fbbfd549f4e44c"></a>
#### ALL_INDEXES

ALL_INDEXES describes the indexes on the tables accessible to the current user.

**Column 정보**

<a id="0ebfc07c643dc060"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="3d6ae0d4536d599b"></a>
#### ALL_IND_COLUMNS

ALL_IND_COLUMNS describes the columns of indexes on all tables accessible to the current user.

**Column 정보**

<a id="41155f74e79c0b2c"></a>
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

<a id="d9170db0965d70b9"></a>
#### ALL_IND_PLACE

ALL_IND_PLACE describes node placement of the indexes on the tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="0b1bd1710193f273"></a>
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

<a id="b55f9bd1d016fc3e"></a>
#### ALL_NONSCHEMA_COMMENTS

ALL_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces) accessible to the current user.

**Column 정보**

<a id="f39744af0d2c86c7"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OBJECT_NAME | VARCHAR(128) | Name of the non-schema object |
| OBJECT_TYPE | VARCHAR(32) | Type of the non-schema object: DATABASE, AUTHORIZATION, SCHEMA, TABLESPACE |
| COMMENTS | VARCHAR(1024) | Comments of the non-schema object |

<a id="830bf35f7fe56f0c"></a>
#### ALL_OBJECTS

ALL_OBJECTS describes all objects accessible to the current user.

**Column 정보**

<a id="a7a3cd69d07773e3"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the object</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the object</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the object</td></tr><tr><td align="left" valign="middle">&nbsp;SUBOBJECT_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_ID</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">&nbsp;DATA_OBJECT_ID</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">&nbsp;OBJECT_TYPE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">&nbsp;CREATED</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_DDL_TIME</td><td align="left" valign="middle">&nbsp;TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">&nbsp;Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">&nbsp;TIMESTAMP</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">&nbsp;STATUS</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">&nbsp;TEMPORARY</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;GENERATED</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;* reserved<br>Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;SECONDARY</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;NAMESPACE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Namespace for the object</td></tr><tr><td align="left" valign="middle">&nbsp;EDITION_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="a69411d57c8688f6"></a>
#### ALL_PROCEDURES

ALL_PROCEDURES lists all function, procedures or package

**Column 정보**

<a id="34666a3f6081b9dc"></a>
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

<a id="01da6ba3721bc6b0"></a>
#### ALL_PROC_PRIVS

ALL_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="cb3e174ac5854cdf"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="22a910b59f190272"></a>
#### ALL_PROC_PRIVS_MADE

ALL_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column 정보**

<a id="af88f10c4a2878ea"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="1cdf40c4fe7eb2a8"></a>
#### ALL_PROC_PRIVS_RECD

ALL_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="e09923c770daed6a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="58c5838e344630d5"></a>
#### ALL_SCHEMAS

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column 정보**

<a id="5011031732e22d6e"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| CREATED_TIME | TIMESTAMP(2) WITHOUT TIME ZONE | Created time of the schema |
| MODIFIED_TIME | TIMESTAMP(2) WITHOUT TIME ZONE | Last modified time of the schema |
| COMMENTS | VARCHAR(1024) | Comments of the schema |

<a id="45799657d910e736"></a>
#### ALL_SCHEMA_PATH

ALL_SCHEMA_PATH describes the schema search order of the current user and PUBLIC, for naming resolution of unqualified SQL schema objects.

**Column 정보**

<a id="69ea4015df576b26"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| AUTH_NAME | VARCHAR(128) | Name of the authorization |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| SEARCH_ORDER | NUMBER | Schema search order of the authorization |

<a id="f1dbe918367b0085"></a>
#### ALL_SCHEMA_PRIVS

ALL_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="96244cae30cff554"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| OWNER | VARCHAR(128) | Owner of the schema |
| SCHEMA_NAME | VARCHAR(128) | Name of the schema |
| PRIVILEGE | VARCHAR(32) | Privilege on the schema |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="cbf27195e5e6857a"></a>
#### ALL_SCHEMA_PRIVS_MADE

ALL_SCHEMA_PRIVS_MADE describes the schema grants, for which the current user is the grantor.

**Column 정보**

<a id="9e57e64fc5113e7b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ab2f794abe2c743e"></a>
#### ALL_SCHEMA_PRIVS_RECD

ALL_SCHEMA_PRIVS_RECD describes the schema grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="bc4a4c3616d0a81c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;SCHEMA_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the schema</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the schema</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="719d67264a24fc6f"></a>
#### ALL_SEQUENCES

ALL_SEQUENCES describes all sequences accessible to the current user.

**Column 정보**

<a id="63ccb74ac32663de"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Sequence name</td></tr><tr><td align="left" valign="middle">&nbsp;MIN_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;MAX_VALUE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;INCREMENT_BY</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">&nbsp;CYCLE_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;ORDER_FLAG</td><td align="left" valign="middle">&nbsp;VARCHAR(1)</td><td align="left" valign="middle">&nbsp;Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">&nbsp;CACHE_SIZE</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">&nbsp;LAST_NUMBER</td><td align="left" valign="middle">&nbsp;NUMBER</td><td align="left" valign="middle">&nbsp;Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="2858149e890d19eb"></a>
#### ALL_SEQ_PRIVS

ALL_SEQ_PRIVS describes the sequence grants, for which the current user is the sequence owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="dea47a4c702faa0d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">&nbsp;GRANTOR</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTEE</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_OWNER</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Owner of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_SCHEMA</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Schema of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;SEQUENCE_NAME</td><td align="left" valign="middle">&nbsp;VARCHAR(128)</td><td align="left" valign="middle">&nbsp;Name of the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;PRIVILEGE</td><td align="left" valign="middle">&nbsp;VARCHAR(32)</td><td align="left" valign="middle">&nbsp;Privilege on the sequence</td></tr><tr><td align="left" valign="middle">&nbsp;GRANTABLE</td><td align="left" valign="middle">&nbsp;VARCHAR(3)</td><td align="left" valign="middle">&nbsp;Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="829943984587acb6"></a>
#### ALL_SEQ_PRIVS_MADE

ALL_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner or grantor.

**Column 정보**

<a id="3dcffc150ee2dc13"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="41332cf4354496c0"></a>
#### ALL_SEQ_PRIVS_RECD

ALL_SEQ_PRIVS_RECD describes the sequence grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="02ebf359ef998212"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f8973f8966c14537"></a>
#### ALL_SHARD_KEY_COLUMNS

ALL_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="2b474691ca0f7412"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="864a32e2c874f23b"></a>
#### ALL_SOURCE

ALL_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="d8709ef50a632897"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="377be549d8db1b64"></a>
#### ALL_SYNONYMS

ALL_SYNONYMS describes all synonyms.

**Column 정보**

<a id="66ac045953e8b8d4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="53430e5becb78994"></a>
#### ALL_TABLES

ALL_TABLES describes the relational tables accessible to the current user.

**Column 정보**

<a id="f3945208704963c6"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="21c2c06fe55617ed"></a>
#### ALL_TAB_COLS

ALL_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="62af1b7bfc6c4393"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="645746a59e673411"></a>
#### ALL_TAB_COLUMNS

ALL_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="a38db4c1504db90e"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="689b914ded7aaf5a"></a>
#### ALL_TAB_COMMENTS

ALL_TAB_COMMENTS displays comments on the tables and views accessible to the current user.

**Column 정보**

<a id="ce2c9213cab0a783"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="8395e2b764c84066"></a>
#### ALL_TAB_IDENTITY_COLS

ALL_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="142e5cf78e2eb2a2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="3f248eb6c8bfd0b8"></a>
#### ALL_TAB_PLACE

ALL_TAB_PLACE describes node placement of all cluster tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="6b58b9ed49a6d250"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="203365869b418007"></a>
#### ALL_TAB_SHARDS

ALL_TAB_SHARDS describes shard information of sharded tables accessible to the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="c88265958c1466a8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="4fb3c1b77f566d53"></a>
#### ALL_TAB_PRIVS

ALL_TAB_PRIVS describes the object grants, for which the current user is the object owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="ccc2eb57a4917ead"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="65cca915e90099a6"></a>
#### ALL_TAB_PRIVS_MADE

ALL_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner or grantor.

**Column 정보**

<a id="e6e2975e2623e614"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="0b1ebfdea11650ff"></a>
#### ALL_TAB_PRIVS_RECD

ALL_TAB_PRIVS_RECD describes object grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="1f4524d19b6224fd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a6144484b4286656"></a>
#### ALL_TBS_PRIVS

ALL_TBS_PRIVS describes the tablespace grants, for which the current user is the grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="d2260f4ed0ff0c2e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="436d94827e58a251"></a>
#### ALL_TBS_PRIVS_MADE

ALL_TBS_PRIVS_MADE describes the tablespace grants for which the current user is the grantor.

**Column 정보**

<a id="60c7bab0c82c8a18"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ad706e6a64e6c9d2"></a>
#### ALL_TBS_PRIVS_RECD

ALL_TBS_PRIVS_RECD describes the tablespace grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="5923fc87c7245095"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="df4f5288425fcd57"></a>
#### ALL_USERS

ALL_USERS lists all users of the database visible to the current user.

**Column 정보**

<a id="934e266f4040263c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">USERNAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">USER_ID</td><td align="left">NUMBER</td><td align="left">ID number of the user</td></tr><tr><td align="left">CREATED</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">User creation timestamp</td></tr></tbody></table>

<a id="063149f535b882dd"></a>
#### ALL_VIEWS

ALL_VIEWS describes the views accessible to the current user.

**Column 정보**

<a id="8971233541f9fd7e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="f77cf2ff2d4f5e08"></a>
### DBA 계열 View

DBA 권한 (ACCESS CONTROL ON DATABASE)을 가지고 있는 현재 사용자의 모든 객체에 대한 정보를 얻을 수 있다.

<a id="18552ab4c8d2defd"></a>
#### DBA_ALL_TABLES

DBA_ALL_TABLES describes all object tables and relational tables in the database.

**Column 정보**

<a id="52dee00bb63dd80b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="af8d7f63dbc0d3f5"></a>
#### DBA_ARGUMENTS

DBA_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="c73720258ae3e9b3"></a>
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

<a id="2664134e8b22a545"></a>
#### DBA_CATALOG

DBA_CATALOG lists all tables, views, synonyms, and sequences in the database.

**Column 정보**

<a id="4d70b7b48d779591"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="adfd2f34239fda8b"></a>
#### DBA_CLUSTER

DBA_CLUSTER describes all cluster members in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="aee7ace3a4926fc5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GROUP_ID</td><td align="left">NUMBER</td><td align="left">Group identifier of the cluster member</td></tr><tr><td align="left">GROUP_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Group name of the cluster member</td></tr><tr><td align="left">MEMBER_ID</td><td align="left">NUMBER</td><td align="left">Member identifier of the cluster member</td></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Member name of the cluster member</td></tr><tr><td align="left">MEMBER_HOST</td><td align="left">VARCHAR(128)</td><td align="left">Host address of the cluster member</td></tr><tr><td align="left">MEMBER_PORT</td><td align="left">NUMBER</td><td align="left">Port number of the cluster member</td></tr></tbody></table>

<a id="7f2c82be49e4623d"></a>
#### DBA_CLUSTER_COMMENTS

DBA_CLUSTER_COMMENTS displays comments on the cluster objects in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="b1d8091dbbbbf55d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the cluster object</td></tr><tr><td align="left">OBJECT_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the cluster object: CLUSTER GROUP, CLUSTER MEMBER</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the cluster object</td></tr></tbody></table>

<a id="05789cecfec96e4e"></a>
#### DBA_CLUSTER_TABLES

DBA_CLUSTER_TABLES describes all cluster tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="f27f54800f8a329c"></a>
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

<a id="f848d253bb13fd12"></a>
#### DBA_COL_COMMENTS

DBA_COL_COMMENTS displays comments on the columns of all tables and views in the database.

**Column 정보**

<a id="9b7fab8d068f4c33"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="adecacf96246ce2e"></a>
#### DBA_COL_PRIVS

DBA_COL_PRIVS describes all column object grants in the database.

**Column 정보**

<a id="ebf156aacf6d21ea"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">CHARACTER VARYING(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">CHARACTER VARYING(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">CHARACTER VARYING(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="0dcb1d8e417a4957"></a>
#### DBA_CONSTRAINTS

DBA_CONSTRAINTS describes all constraint definitions on all tables in the database.

**Column 정보**

<a id="b3a6f38ca2de34c2"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="94a4310b4f8cbc93"></a>
#### DBA_CONS_COLUMNS

DBA_CONS_COLUMNS describes all columns in the database that are specified in constraints.

**Column 정보**

<a id="0cecbdd3fb35b06c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="4adc9a8f53d72c83"></a>
#### DBA_DB_PRIVS

DBA_DB_PRIVS describes all database grants in the database.

**Column 정보**

<a id="fc64ad4470dc69f0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the database</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="6bc78c929619e3fe"></a>
#### DBA_DEPENDENCIES

DBA_DEPENDENCIES describes all dependencies between objects in the database

**Column 정보**

<a id="25cff074972ee93e"></a>
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

<a id="64be8605b0c8d2ef"></a>
#### DBA_EXTENTS

DBA_EXTENTS describes the extents comprising the segments in all tablespaces in the database.

**Column 정보**

<a id="654b28d5069367d3"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Extent number in the segment</td></tr><tr><td align="left" valign="middle">FILE_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;File identifier number of the file containing the extent</td></tr><tr><td align="left" valign="middle">BLOCK_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Starting block number of the extent</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr><tr><td align="left" valign="middle">RELATIVE_FNO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Relative file number of the first extent block</td></tr></tbody></table>

<a id="5262b9c5bade4eab"></a>
#### DBA_GLOBAL_SECONDARY_INDEXES

DBA_GLOBAL_SECONDARY_INDEXES describes all global secondary indexes in the database.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="479d3a0c8867e4d4"></a>
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

<a id="4d9f6c6f0aac0152"></a>
#### DBA_GSI_PLACE

DBA_GSI_PLACE describes node placement of all global secondary indexes in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="bb09a442a9436fde"></a>
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

<a id="e265ef9735c7983c"></a>
#### DBA_INDEXES

DBA_INDEXES describes all indexes in the database.

**Column 정보**

<a id="08a0b14e1503c46c"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="1a5947eea507c974"></a>
#### DBA_IND_COLUMNS

DBA_IND_COLUMNS describes the columns of all the indexes on all tables and clusters in the database.

**Column 정보**

<a id="f500f5c9ec8e13b8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="b965ac4490dc100b"></a>
#### DBA_IND_PLACE

DBA_IND_PLACE describes node placement of all indexes in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="7263ef76b21cf0a1"></a>
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

<a id="15cc7a26d9c610ad"></a>
#### DBA_NONSCHEMA_COMMENTS

DBA_NONSCHEMA_COMMENTS displays comments on all non-schema objects (database, authorizations, schemas, tablespaces).

**Column 정보**

<a id="6af820f94e43c7a8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the non-schema object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the non-schema object: DATABASE, PROFILE, AUTHORIZATION, SCHEMA, TABLESPACE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the non-schema object</td></tr></tbody></table>

<a id="d780e29c55c087ba"></a>
#### DBA_OBJECTS

DBA_OBJECTS describes all objects in the database.

**Column 정보**

<a id="1e2f19719658006e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="1f07b06e48243dc4"></a>
#### DBA_PROCEDURES

DBA_PROCEDURES lists all function, procedures or package

**Column 정보**

<a id="8232112269bbdf73"></a>
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

<a id="38af7f7e000fe5b2"></a>
#### DBA_PROC_PRIVS

DBA_PROC_PRIVS describes the procedure grants, for which the current user is the procedure owner, grantor, or grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="9432dbfae4a5e43b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="8782afbbe822c2ae"></a>
#### DBA_PROFILES

DBA_PROFILES displays all profiles and their limits.

**Column 정보**

<a id="0be5e58baa830d97"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROFILE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Profile name</td></tr><tr><td align="left" valign="middle">RESOURCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Resource name</td></tr><tr><td align="left" valign="middle">RESOURCE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the resource profile is a KERNEL or a PASSWORD parameter</td></tr><tr><td align="left" valign="middle">LIMIT_VALUE</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Limit placed on this resource for this profile</td></tr><tr><td align="left" valign="middle">COMMON</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether a given profile is common. (YES or NO)</td></tr></tbody></table>

<a id="13d55ffa771dc4f0"></a>
#### DBA_SCHEMAS

Identify the schemata in the database.

**Column 정보**

<a id="c19be5336ae715d8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="47bfa26cb8002387"></a>
#### DBA_SCHEMA_PATH

DBA_SCHEMA_PATH describes the schema search order of all authorizations in the database.

**Column 정보**

<a id="fd114fd9391a3e7f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the authorization</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the authorization</td></tr></tbody></table>

<a id="174f6c7459d22d2a"></a>
#### DBA_SCHEMA_PRIVS

DBA_SCHEMA_PRIVS describes all schema grants in the database.

**Column 정보**

<a id="99cc3cbc58d1d022"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="08629af0ea6299cc"></a>
#### DBA_SEQUENCES

DBA_SEQUENCES describes all sequences in the database.

**Column 정보**

<a id="a864b11cded0ce0f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="8eb42a5128a233b1"></a>
#### DBA_SEQ_PRIVS

DBA_SEQ_PRIVS describes all sequence grants in the database.

**Column 정보**

<a id="aff61ab0fd365088"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a4537366269d32fa"></a>
#### DBA_SHARD_KEY_COLUMNS

DBA_SHARD_KEY_COLUMNS describes shard key columns of all shareded tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="2ef1d1a77b0d577b"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of the table |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="a8de36bf3be217b3"></a>
#### DBA_SOURCE

DBA_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="90d65cdd135e9eeb"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| OWNER | VARCHAR(128) | Owner of object |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="2f0a2bb23e634e8c"></a>
#### DBA_STAT_SYSTEM

DBA_STAT_SYSTEM describes analyzed system statistics.

**Column 정보**

<a id="20e428f7047e1660"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CPU_OPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">OPS(operations per second) of CPU</td></tr><tr><td align="left" valign="middle">NETWORK_IOPS</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">IOPS(I/O operations per second) of Cluster NETWORK</td></tr><tr><td align="left" valign="middle">NETWORK_BUFSIZE</td><td align="left" valign="middle">NATIVE_BIGINT</td><td align="left" valign="middle">buffer size of Cluster NETWORK when analyzed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="70372beb78ed90c1"></a>
#### DBA_SYS_PRIVS

DBA_SYS_PRIVS describes all system (database, tablespace, schema) privileges in the database.

**Column 정보**

<a id="b215f2565a479c0e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the grantee</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="e3c2e3840218caef"></a>
#### DBA_SYNONYMS

DBA_SYNONYMS describes all synonyms in the database.

**Column 정보**

<a id="3c66e6c15ebc330c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="9ff8da3f82ce6d6b"></a>
#### DBA_TABLES

DBA_TABLES describes all relational tables in the database.

**Column 정보**

<a id="c0888f5c848943da"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="003f21f082cf1bc3"></a>
#### DBA_TABLESPACES

DBA_TABLESPACES describes all tablespaces in the database.

**Column 정보**

<a id="5a715bde2345112f"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">PLUGGED_IN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is plugged in (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="b3dfb24ebb5446d5"></a>
#### DBA_TAB_COLS

DBA_TAB_COLS describes the columns (including hidden columns) of all tables, views, and clusters in the database.

**Column 정보**

<a id="76f47e101ee6c80e"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="666b7b1136dbf006"></a>
#### DBA_TAB_COLUMNS

DBA_TAB_COLUMNS describes the columns of the tables, views, and clusters accessible to the current user.

**Column 정보**

<a id="322f6cf10fd78b9f"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="bd6c5e1b58675fb4"></a>
#### DBA_TAB_COMMENTS

DBA_TAB_COMMENTS displays comments on all tables and views in the database.

**Column 정보**

<a id="aac4934158381e6b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the object</td></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="eb1eca408592a7ca"></a>
#### DBA_TAB_IDENTITY_COLS

DBA_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="a5cf487bc70cd18e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="6697c2c51fc98a6a"></a>
#### DBA_TAB_PLACE

DBA_TAB_PLACE describes node placement of all cluster tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="02884a7884dbd15c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="780a36f58f932743"></a>
#### DBA_TAB_PRIVS

DBA_TAB_PRIVS describes all object grants in the database.

**Column 정보**

<a id="da163b2f01a3bca4"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="e68b35385fceca5f"></a>
#### DBA_TAB_SHARDS

DBA_TAB_SHARDS describes shard information of all sharded tables in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="dfa703c2f945c06f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="0a1fbbd23b70a938"></a>
#### DBA_TBS_PRIVS

DBA_TBS_PRIVS describes all tablespace grants in the database.

**Column 정보**

<a id="129b8d2e29ec4ecb"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the tablespace</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="ffcd5fbaad72a2dd"></a>
#### DBA_USERS

DBA_USERS describes all users of the database.

**Column 정보**

<a id="2a326258aafeaef8"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">PASSWORD</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">encrypted password</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">FAILED_LOGIN_ATTEMPTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Consecutive failed login attempts count</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">PROFIL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">User resource profile name</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr><tr><td align="left" valign="middle">PASSWORD_VERSIONS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Shows the list of versions of the password hashes (verifiers).</td></tr><tr><td align="left" valign="middle">EDITIONS_ENABLED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether editions have been enabled for the corresponding user (Y) or not (N).</td></tr><tr><td align="left" valign="middle">AUTHENTICATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the authentication mechanism for the user.</td></tr></tbody></table>

<a id="d78a4c2ab46bcbd1"></a>
#### DBA_VIEWS

DBA_VIEWS describes all views in the database.

**Column 정보**

<a id="a4b16db3ab06869c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the view</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="9fb73ae679fb5e65"></a>
### USER 계열 View

현재 사용자가 소유한 객체에 대한 정보를 얻을 수 있다.

<a id="594443caed92723f"></a>
#### USER_ALL_TABLES

USER_ALL_TABLES describes the object tables and relational tables owned by the current user.

**Column 정보**

<a id="d1ab1551a4c9c165"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">OBJECT_ID_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the object ID (OID) is USER-DEFINED or SYSTEM GENERATED</td></tr><tr><td align="left" valign="middle">TABLE_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, owner of the type from which the table is created</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If an object table, type of the table</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr></tbody></table>

<a id="51752ceaa27d7558"></a>
#### USER_ARGUMENTS

USER_ARGUMENTS lists all arguments of functions, procedures.

**Column 정보**

<a id="3087b4903327762f"></a>
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

<a id="d00c5b24b9d57e2c"></a>
#### USER_CATALOG

USER_CATALOG lists tables, views, synonyms, and sequences owned by the current user.

**Column 정보**

<a id="d081eb50c081c2a9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the TABLE, VIEW, SYNONYM, SEQUENCE, or UNDEFINED</td></tr></tbody></table>

<a id="49fd03ec7fb8f1a0"></a>
#### USER_COL_COMMENTS

USER_COL_COMMENTS displays comments on the columns of the tables and views owned by the current user.

**Column 정보**

<a id="4bfa2c94b8745a22"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the column</td></tr></tbody></table>

<a id="f9b7c0b04455db32"></a>
#### USER_CLUSTER_TABLES

USER_CLUSTER_TABLES describes all cluster tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="b6b18c398d1308ac"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| SHARD_STRATEGY | VARCHAR(32) | Sharding strategy of the table:  the value in (CLONED, HASH SHARDING, RANGE SHARDING, LIST SHARDING) |
| SHARD_PLACEMENT | VARCHAR(32) | Shard placement of the table:  the value in (AT CLUSTER WIDE or AT CLUSTER GROUP) |
| SHARD_COUNT | NUMBER | Shard count of the table (if cloned table, the value is null) |
| SHARD_KEY_COUNT | NUMBER | Shard key column count of the table (if cloned table, the value is null) |
| HAS_GSI | VARCHAR(3) | Indicate whether the table has global secondary index: (YES) or (NO) |

<a id="5d50cf42eef50c7d"></a>
#### USER_COL_PRIVS

USER_COL_PRIVS describes the column object grants for which the current user is the object owner, grantor, or grantee.

**Column 정보**

<a id="59d01a7d63803192"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="5f197023b5655d00"></a>
#### USER_COL_PRIVS_MADE

USER_COL_PRIVS_MADE describes the column object grants for which the current user is the object owner.

**Column 정보**

<a id="3b5e41fcdd67c901"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="1d535f48d34d0111"></a>
#### USER_COL_PRIVS_RECD

USER_COL_PRIVS_RECD describes the column object grants for which the current user is the grantee.

**Column 정보**

<a id="301704fbf78976a6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the column</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="0e3c1b326b378dbc"></a>
#### USER_CONSTRAINTS

USER_CONSTRAINTS describes all constraint definitions on tables owned by the current user.

**Column 정보**

<a id="d45fe17344701fee"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Type of the constraint definition: the value in ( C: check constraint, P: Primary key, U: Unique Key, R: Referential intgrity )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table (or view) associated with the constraint definition</td></tr><tr><td align="left" valign="middle">SEARCH_CONDITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Text of search condition for a check constraint</td></tr><tr><td align="left" valign="middle">R_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">R_CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the unique constraint definition for the referenced table</td></tr><tr><td align="left" valign="middle">DELETE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Delete rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">UPDATE_RULE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Update rule for a referential constraint: the value in ( NO ACTION, RESTRICT, CASCADE, SET NULL, SET DEFAULT )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Enforcement status of the constraint: the value in ( ENABLED, DISABLE )</td></tr><tr><td align="left" valign="middle">DEFERRABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is deferrable (DEFERRABLE) or not (NOT DEFERRABLE)</td></tr><tr><td align="left" valign="middle">DEFERRED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint was initially deferred (DEFERRED) or not (IMMEDIATE)</td></tr><tr><td align="left" valign="middle">VALIDATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether all data may obey the constraint or not: the value in ( VALIDATED, NOT VALIDATED )</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the name of the constraint is user-generated (USER NAME) or system-generated (GENERATED NAME)</td></tr><tr><td align="left" valign="middle">BAD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether this constraint specifies a century in an ambiguous manner (BAD) or not (NULL)</td></tr><tr><td align="left" valign="middle">RELY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;When NOT VALIDATED, indicates whether the constraint is to be taken into account for query rewrite (RELY) or not (NULL)</td></tr><tr><td align="left" valign="middle">LAST_CHANGE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">When the constraint was last enabled or disabled</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index associated with the key constraint</td></tr><tr><td align="left" valign="middle">INVALID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the constraint is invalid (INVALID) or not (NULL)</td></tr><tr><td align="left" valign="middle">VIEW_RELATED</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether the constraint depends on a view (DEPEND ON VIEW) or not (NULL)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the constraint definition</td></tr></tbody></table>

<a id="e0a5214567a9c5e1"></a>
#### USER_CONS_COLUMNS

USER_CONS_COLUMNS describes columns that are owned by the current user and that are specified in constraint definitions.

**Column 정보**

<a id="5b07607eaf9d5ed7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the constraint definition</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table with the constraint definition</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the column or attribute of the object type column specified in the constraint definition</td></tr><tr><td align="left" valign="middle">POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Original position of the column or attribute in the definition of the object</td></tr></tbody></table>

<a id="009cb0d029f92a8e"></a>
#### USER_DEPENDENCIES

USER_DEPENDENCIES describes dependencies between objects accessible to the current user

**Column 정보**

<a id="b5e17d3c32023317"></a>
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

<a id="21ab6db3a2fc360a"></a>
#### USER_EXTENTS

USER_EXTENTS describes the extents comprising the segments owned by the current user's objects.

**Column 정보**

<a id="4f56fe278ce6b15c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEGMENT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">SEGMENT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the segment associated with the extent</td></tr><tr><td align="left" valign="middle">PARTITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Object Partition Name (Set to NULL for non-partitioned objects)</td></tr><tr><td align="left" valign="middle">SEGMENT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the segment: TABLE, INDEX</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the extent</td></tr><tr><td align="left" valign="middle">EXTENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Extent number in the segment</td></tr><tr><td align="left" valign="middle">BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in bytes</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the extent in Oracle blocks</td></tr></tbody></table>

<a id="f83cb6810fd16ad4"></a>
#### USER_GLOBAL_SECONDARY_INDEXES

USER_GLOBAL_SECONDARY_INDEXES describes the global secondary indexes on the tables owned by the current user.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="3d48cce91a752d75"></a>
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

<a id="9fc90844bcbb9d2e"></a>
#### USER_GSI_PLACE

USER_GSI_PLACE describes node placement of all global secondary indexes on the tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="5022fd0399ae6c75"></a>
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

<a id="8954cee23120ce4a"></a>
#### USER_INDEXES

USER_INDEXES describes indexes owned by the current user.

**Column 정보**

<a id="5aca52c5d0b3bf34"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">INDEX_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the index: the value in ( NORMAL, NORMAL/REV, BITMAP, FUNCTION-BASED NORMAL, FUNCTION-BASED NORMAL/REV, FUNCTION-BASED BITMAP, IOT - TOP, DOMAIN )</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the indexed object</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the indexed object: the value in ( NEXT OBJECT, INDEX, TABLE, VIEW, SYNONYM, SEQUENCE )</td></tr><tr><td align="left" valign="middle">UNIQUENESS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the index is unique (UNIQUE) or nonunique (NONUNIQUE)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether index compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">PREFIX_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of columns in the prefix of the compression key</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the index</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">PCT_THRESHOLD</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Threshold percentage of block space allowed per index entry</td></tr><tr><td align="left" valign="middle">INCLUDE_COLUMN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Column ID of the last column to be included in index-organized table primary key (non-overflow) index</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to this segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to this segment</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">ndicates whether or not changes to the index are logged: (YES) or (NO)</td></tr><tr><td align="left">BLOCKS</td><td align="left">NUMBER</td><td align="left">Number of used blocks in the index</td></tr><tr><td align="left" valign="middle">BLEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;B-Tree level (depth of the index from its root block to its leaf blocks)</td></tr><tr><td align="left" valign="middle">LEAF_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of leaf blocks in the index</td></tr><tr><td align="left" valign="middle">DISTINCT_KEYS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct indexed values.</td></tr><tr><td align="left" valign="middle">AVG_LEAF_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of leaf blocks in which each distinct value in the index appears, rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">AVG_DATA_BLOCKS_PER_KEY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average number of data blocks in the table that are pointed to by a distinct value in the index rounded to the nearest integer</td></tr><tr><td align="left" valign="middle">CLUSTERING_FACTOR</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the amount of order of the rows in the table based on the values of the index</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether a nonpartitioned index is VALID or UNUSABLE</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the index</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the sample used to analyze the index</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this index was most recently analyzed</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the index, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the indexes to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the index is on a temporary table (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of the index is system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a secondary object created by the method of the Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for index blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for index blocks</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">PCT_DIRECT_ACCESS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a secondary index on an index-organized table, the percentage of rows with VALID guess</td></tr><tr><td align="left" valign="middle">ITYP_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the owner of the indextype</td></tr><tr><td align="left" valign="middle">ITYP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the name of the indextype</td></tr><tr><td align="left" valign="middle">PARAMETERS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For a domain index, the parameter string</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned indexes, indicates whether statistics were collected by analyzing the index as a whole (YES) or were estimated from statistics on underlying index partitions and subpartitions (NO)</td></tr><tr><td align="left" valign="middle">DOMIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a domain index</td></tr><tr><td align="left" valign="middle">DOMIDX_OPSTATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of the operation on a domain index</td></tr><tr><td align="left" valign="middle">FUNCIDX_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Status of a function-based index</td></tr><tr><td align="left" valign="middle">JOIN_INDEX</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is a join index (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_REDUNDANT_PKEY_ELIM</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether redundant primary key columns are eliminated from secondary indexes on index-organized tables (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VISIBILITY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the index is VISIBLE or INVISIBLE to the optimizer</td></tr><tr><td align="left" valign="middle">DOMIDX_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If this is a domain index, indicates whether the domain index is system-managed (SYSTEM_MANAGED) or user-managed (USER_MANAGED)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the index segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the index</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of empty blocks in the index</td></tr></tbody></table>

<a id="df7431ff331a73ae"></a>
#### USER_IND_COLUMNS

USER_IND_COLUMNS describes the columns of the indexes owned by the current user and columns of indexes on tables owned by the current user.

**Column 정보**

<a id="1f32fc5b6601682a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the index</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table or cluster</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table or cluster</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name or attribute of the object type column</td></tr><tr><td align="left" valign="middle">COLUMN_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Position of the column or attribute within the index</td></tr><tr><td align="left" valign="middle">COLUMN_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Indexed length of the column</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Maximum codepoint length of the column</td></tr><tr><td align="left" valign="middle">DESCEND</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the column is sorted in descending order (DESC) or ascending order (ASC)</td></tr><tr><td align="left" valign="middle">NULL_ORDER</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether the null value of the column is sorted in nulls first order (NULLS FIRST) or nulls last order (NULLS LAST)</td></tr></tbody></table>

<a id="ac1b65c2ac8f721d"></a>
#### USER_IND_PLACE

USER_IND_PLACE describes node placement of the indexes owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="acde70ab35e53df4"></a>
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

<a id="4f4f7992313dad3c"></a>
#### USER_OBJECTS

USER_OBJECTS describes all objects owned by the current user.

**Column 정보**

<a id="24224cba4550a29f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUBOBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the subobject (for example, partition)</td></tr><tr><td align="left" valign="middle">OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the object</td></tr><tr><td align="left" valign="middle">DATA_OBJECT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Dictionary object number of the segment that contains the object</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Type of the object (such as TABLE, INDEX)</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the creation of the object</td></tr><tr><td align="left" valign="middle">LAST_DDL_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp for the last modification of the object resulting from a DDL statement</td></tr><tr><td align="left" valign="middle">TIMESTAMP</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Timestamp for the specification of the object (character data)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Status of the object: the value in ( VALID, INVALID, N/A )</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the object is temporary (the current session can see only data that it placed in this object itself) (Y) or not (N)</td></tr><tr><td align="left" valign="middle">GENERATED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the name of this object was system-generated (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether this is a secondary object created by the ODCIIndexCreate method of the Oracle Data Cartridge (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NAMESPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Namespace for the object</td></tr><tr><td align="left" valign="middle">EDITION_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the edition in which the object is actual</td></tr></tbody></table>

<a id="738d4070bf0e189e"></a>
#### USER_PROCEDURES

USER_PROCEDURES lists of procedures owned by the current user.

**Column 정보**

<a id="9fa36041b2019b32"></a>
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

<a id="e7651bd3b2bc77bc"></a>
#### USER_PROC_PRIVS

USER_PROC_PRIVS describes the procedure grants for which the current user is the procedure owner, grantor, or grantee.

**Column 정보**

<a id="950a1a56e5a67bb4"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="d39f8f5796b1dd6b"></a>
#### USER_PROC_PRIVS_MADE

USER_PROC_PRIVS_MADE describes the procedure grants for which the current user is the procedure owner or grantor.

**Column 정보**

<a id="0fd39d6f97164c6a"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="99e8a12a3bf3dd2b"></a>
#### USER_PROC_PRIVS_RECD

USER_PROC_PRIVS_RECD describes the procedure grants, for which the current user is the grantee, or for which an enabled role or PUBLIC is the grantee.

**Column 정보**

<a id="e676990019da38f6"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| GRANTOR | VARCHAR(128) | Name of the user who performed the grant |
| GRANTEE | VARCHAR(128) | Name of the user or role to whom access was granted |
| PROCEDURE_OWNER | VARCHAR(128) | Owner of the procedure, function or package |
| PROCEDURE_SCHEMA | VARCHAR(128) | Schema of the procedure, function or package |
| PROCEDURE_NAME | VARCHAR(128) | Name of the procedure, function or package |
| PRIVILEGE | VARCHAR(32) | Privilege on the procedure, function or package |
| GRANTABLE | VARCHAR(3) | Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO) |

<a id="18eaf4c9f691f07c"></a>
#### USER_SCHEMAS

Identify the schemata in a catalog that are owned by current user.

**Column 정보**

<a id="1e35bb5be3b569cd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCHEMA_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the schema</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">CREATED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Created time of the schema</td></tr><tr><td align="left">MODIFIED_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">Last modified time of the schema</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comments of the schema</td></tr></tbody></table>

<a id="d8adfe3073d40426"></a>
#### USER_SCHEMA_PATH

USER_SCHEMA_PATH describes the schema search order of the current user, for naming resolution of unqualified SQL schema objects.

**Column 정보**

<a id="936ae4ad793a02f2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">AUTH_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the user</td></tr><tr><td align="left">SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the schema</td></tr><tr><td align="left">SEARCH_ORDER</td><td align="left">NUMBER</td><td align="left">Schema search order of the user</td></tr></tbody></table>

<a id="a58749c53a1169ea"></a>
#### USER_SCHEMA_PRIVS

USER_SCHEMA_PRIVS describes the schema grants, for which the current user is the schema owner, grantor, or grantee.

**Column 정보**

<a id="71623654765e0f24"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="a5047b0a9de98e24"></a>
#### USER_SCHEMA_PRIVS_MADE

USER_SCHEMA_PRIVS_MADE describes the schema grants for which the current user is the schema owner.

**Column 정보**

<a id="1b9357360f415bce"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="f5827721c26a61f0"></a>
#### USER_SCHEMA_PRIVS_RECD

USER_SCHEMA_PRIVS_RECD describes the schema grants for which the current user is the grantee.

**Column 정보**

<a id="433d274ebe931245"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the schema</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the schema</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="863de1ba71fc8a17"></a>
#### USER_SEQUENCES

USER_SEQUENCES describes all sequences owned by the current user.

**Column 정보**

<a id="ce117ddab0cc8ece"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Sequence name</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum value of the sequence</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum value of the sequence</td></tr><tr><td align="left" valign="middle">INCREMENT_BY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value by which sequence is incremented</td></tr><tr><td align="left" valign="middle">CYCLE_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the sequence wraps around on reaching the limit (Y) or not (N)</td></tr><tr><td align="left" valign="middle">ORDER_FLAG</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>Indicates whether sequence numbers are generated in order (Y) or not (N)</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">LAST_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Last sequence number written to database. If a sequence uses caching, the number written to database is the last number placed in the sequence cache.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Comments of the sequence</td></tr></tbody></table>

<a id="414abf1833bd59d5"></a>
#### USER_SEQ_PRIVS

USER_SEQ_PRIVS describes the sequence grants for which the current user is the sequence owner, grantor, or grantee.

**Column 정보**

<a id="cfe29aa2724ab950"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="2531c2e59d2f9ce2"></a>
#### USER_SEQ_PRIVS_MADE

USER_SEQ_PRIVS_MADE describes the sequence grants for which the current user is the sequence owner.

**Column 정보**

<a id="8e6bd21c3ac69961"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="800f49dd3172d0ab"></a>
#### USER_SEQ_PRIVS_RECD

USER_SEQ_PRIVS_RECD describes the sequence grants for which the current user is the grantee.

**Column 정보**

<a id="7d2d2fa74460e899"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the sequence</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the sequence</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="aa7f42cabffe0ef8"></a>
#### USER_SHARD_KEY_COLUMNS

USER_SHARD_KEY_COLUMNS describes shard key columns of shareded tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="c2c6962f7c338068"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| TABLE_SCHEMA | VARCHAR(128) | Schema of the table |
| TABLE_NAME | VARCHAR(128) | Name of the table |
| COLUMN_NAME | VARCHAR(128) | Column name of the shard key |
| COLUMN_POSITION | NUMBER | Position of the column within the shard key |

<a id="b6a811de9c708452"></a>
#### USER_SOURCE

USER_SOURCE describes the text source of the stored objects accessible to the current user.

**Column 정보**

<a id="b7b21140543f214d"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| SCHEMA_NAME | VARCHAR(128) | Schema Name of object |
| NAME | VARCHAR(128) | Name of object |
| TYPE | VARCHAR(32) | Type of object: FUNCTION, PROCEDURE, PACKAGE, PACKAGE BODY, TRIGGER |
| LINE | NUMBER | Line number of this line of source |
| TEXT | LONG VARCHAR | Text source of the strored object |
| ORIGIN_CON_ID | VARCHAR(256) | ID of the container where the data originates |

<a id="fa75b14b390f2873"></a>
#### USER_SYNONYMS

USER_SYNONYMS describes all synonyms owned by the current user.

**Column 정보**

<a id="c220c61e3f112e10"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SYNONYM_OWNER</td><td align="left">VARCHAR(128)</td><td align="left">Owner of the synonym</td></tr><tr><td align="left">SYNONYM_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the synonym</td></tr><tr><td align="left">SYNONYM_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Synonym name</td></tr><tr><td align="left">OBJECT_SCHEMA_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object schema name</td></tr><tr><td align="left">OBJECT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Object name</td></tr><tr><td align="left">DB_LINK</td><td align="left">VARCHAR(128)</td><td align="left">Reserved for future use</td></tr></tbody></table>

<a id="9ff916c1b96e00ba"></a>
#### USER_SYS_PRIVS

USER_SYS_PRIVS describes system (database, tablespace, schema) privileges granted to the current user or PUBLIC.

**Column 정보**

<a id="b90cc472ee0d9c92"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user, or PUBLIC</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(256)</td><td align="left" valign="middle">System(database, tablespace, schema) privilege</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">ADMIN_OPTION</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">equal to GRANTABLE column</td></tr></tbody></table>

<a id="7039cc74ff97328c"></a>
#### USER_TABLES

USER_TABLES describes the relational tables owned by the current user.

**Column 정보**

<a id="a9570a1eac49c92b"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace containing the table</td></tr><tr><td align="left" valign="middle">CLUSTER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the cluster</td></tr><tr><td align="left" valign="middle">IOT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the index-organized table</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a previous DROP TABLE operation failed, indicates whether the table is unusable (UNUSABLE) or valid (VALID)</td></tr><tr><td align="left" valign="middle">PCT_FREE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of free space in a block</td></tr><tr><td align="left" valign="middle">PCT_USED</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum percentage of used space in a block</td></tr><tr><td align="left" valign="middle">INI_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Initial number of transactions</td></tr><tr><td align="left" valign="middle">MAX_TRANS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of transactions</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of the initial extent (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Size of secondary extents (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Minimum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Maximum number of extents allowed in the segment</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Percentage increase in extent size</td></tr><tr><td align="left" valign="middle">FREELISTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of process freelists allocated to the segment</td></tr><tr><td align="left" valign="middle">FREELIST_GROUPS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of freelist groups allocated to the segment</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether or not changes to the table are logged</td></tr><tr><td align="left" valign="middle">BACKED_UP</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been backed up since the last modification (Y) or not (N)</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks in the table</td></tr><tr><td align="left" valign="middle">EMPTY_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of empty (never used) blocks in the table</td></tr><tr><td align="left" valign="middle">AVG_SPACE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average available free space in the table</td></tr><tr><td align="left" valign="middle">CHAIN_CNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of rows in the table that are chained from one data block to another or that have migrated to a new block, requiring a link to preserve the old rowid</td></tr><tr><td align="left" valign="middle">AVG_ROW_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average row length, including row overhead</td></tr><tr><td align="left" valign="middle">AVG_SPACE_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Average freespace of all blocks on a freelist</td></tr><tr><td align="left" valign="middle">NUM_FREELIST_BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of blocks on the freelist</td></tr><tr><td align="left" valign="middle">DEGREE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of threads per instance for scanning the table, or DEFAULT</td></tr><tr><td align="left" valign="middle">INSTANCES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of instances across which the table is to be scanned, or DEFAULT</td></tr><tr><td align="left" valign="middle">CACHE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is to be cached in the buffer cache (Y) or not (N)</td></tr><tr><td align="left" valign="middle">TABLE_LOCK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Indicates whether table locking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing the table</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr><tr><td align="left" valign="middle">PARTITIONED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is partitioned (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IOT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If the table is an index-organized table, then IOT_TYPE is IOT, IOT_OVERFLOW, or IOT_MAPPING.</td></tr><tr><td align="left" valign="middle">TEMPORARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the table is temporary (Y) or not (N)</td></tr><tr><td align="left" valign="middle">SECONDARY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a secondary object created by cartridge</td></tr><tr><td align="left" valign="middle">NESTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table is a nested table (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">BUFFER_POOL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Buffer pool to be used for table blocks</td></tr><tr><td align="left" valign="middle">FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Database Smart Flash Cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">CELL_FLASH_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Cell flash cache hint to be used for table blocks</td></tr><tr><td align="left" valign="middle">ROW_MOVEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a partitioned table, indicates whether row movement is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether statistics for the table as a whole (global statistics) are accurate (YES)</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DURATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates the duration of a temporary table</td></tr><tr><td align="left" valign="middle">SKIP_CORRUPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether Database ignores blocks marked corrupt during table and index scans (ENABLED) or raises an error (DISABLED)</td></tr><tr><td align="left" valign="middle">MONITORING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has the MONITORING attribute set (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CLUSTER_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the cluster, if any</td></tr><tr><td align="left" valign="middle">DEPENDENCIES</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether row-level dependency tracking is enabled (ENABLED) or disabled (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default compression for what kind of operations</td></tr><tr><td align="left" valign="middle">DROPPED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the table has been dropped and is in the recycle bin (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table IS READ-ONLY (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_CREATED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the table segment has been created (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">RESULT_CACHE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Result cache mode annotation for the table: the value in ( NULL, DEFAULT, FORCE, MANUAL )</td></tr></tbody></table>

<a id="33f7b309a26bbf21"></a>
#### USER_TABLESPACES

USER_TABLESPACES describes the tablespaces accessible to the current user.

**Column 정보**

<a id="5f0cc042cec4e603"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the tablespace</td></tr><tr><td align="left" valign="middle">BLOCK_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Tablespace block size</td></tr><tr><td align="left" valign="middle">INITIAL_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default initial extent size (in bytes)</td></tr><tr><td align="left" valign="middle">NEXT_EXTENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default incremental extent size (in bytes)</td></tr><tr><td align="left" valign="middle">MIN_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default minimum number of extents</td></tr><tr><td align="left" valign="middle">MAX_EXTENTS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum number of extents</td></tr><tr><td align="left" valign="middle">MAX_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default maximum size of segments</td></tr><tr><td align="left" valign="middle">PCT_INCREASE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Default percent increase for extent size</td></tr><tr><td align="left" valign="middle">MIN_EXTLEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Minimum extent size for this tablespace (in bytes)</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace status: the value in ( ONLINE, OFFLINE, READ ONLY )</td></tr><tr><td align="left" valign="middle">CONTENTS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Tablespace contents: the value in ( SYSTEM, DATA, TEMPORARY, UNDO )</td></tr><tr><td align="left" valign="middle">LOGGING</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Default logging attribute: LOGGING, NOLOGGING</td></tr><tr><td align="left" valign="middle">FORCE_LOGGING</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is under force logging mode (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">EXTENT_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the extents in the tablespace are dictionary managed (DICTIONARY) or locally managed (LOCAL)</td></tr><tr><td align="left" valign="middle">ALLOCATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of extent allocation in effect for the tablespace: the value in ( SYSTEM, UNIFORM, USER )</td></tr><tr><td align="left" valign="middle">SEGMENT_SPACE_MANAGEMENT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the free and used segment space in the tablespace is managed using free lists (MANUAL) or bitmaps (AUTO)</td></tr><tr><td align="left" valign="middle">DEF_TAB_COMPRESSION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether default table compression is enabled (ENABLED) or not (DISABLED)</td></tr><tr><td align="left" valign="middle">RETENTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Undo tablespace retention: the value in ( GUARANTEE, NOGUARANTEE, NOT APPLY )</td></tr><tr><td align="left" valign="middle">BIGFILE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is a bigfile tablespace (YES) or a smallfile tablespace (NO)</td></tr><tr><td align="left" valign="middle">PREDICATE_EVALUATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether predicates are evaluated by host (HOST) or by storage (STORAGE)</td></tr><tr><td align="left" valign="middle">ENCRYPTED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">COMPRESS_FOR</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the tablespace is encrypted (YES) or not (NO)</td></tr></tbody></table>

<a id="669e4623bd602f78"></a>
#### USER_TAB_COLS

USER_TAB_COLS describes the columns (including hidden columns) of the tables, views, and clusters owned by the current user.

**Column 정보**

<a id="e22ae09d46649e62"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIDDEN_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the column is a hidden column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">VIRTUAL_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column is a virtual column (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">SEGMENT_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column in the segment</td></tr><tr><td align="left" valign="middle">INTERNAL_COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Internal sequence number of the column</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">QUALIFIED_COL_NAME</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle">Qualified column name</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="6ee1783068257382"></a>
#### USER_TAB_COLUMNS

USER_TAB_COLUMNS describes the columns of the tables, views, and clusters owned by the current user.

**Column 정보**

<a id="b8db76a33d41c22f"></a>
<table><thead><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr></thead><tbody><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Column name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_MOD</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Datatype modifier of the column</td></tr><tr><td align="left" valign="middle">DATA_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the datatype of the column</td></tr><tr><td align="left" valign="middle">DATA_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Decimal precision for NUMBER datatype; binary precision for FLOAT datatype; NULL for all other datatypes</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Digits to the right of the decimal point in a number</td></tr><tr><td align="left" valign="middle">NULLABLE</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether a column allows NULLs.</td></tr><tr><td align="left" valign="middle">COLUMN_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sequence number of the column as created</td></tr><tr><td align="left" valign="middle">DEFAULT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the default value for the column</td></tr><tr><td align="left" valign="middle">DATA_DEFAULT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Default value for the column</td></tr><tr><td align="left" valign="middle">NUM_DISTINCT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of distinct values in the column</td></tr><tr><td align="left" valign="middle">LOW_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">Low value in the column</td></tr><tr><td align="left" valign="middle">HIGH_VALUE</td><td align="left" valign="middle">VARBINARY(32)</td><td align="left" valign="middle">High value in the column</td></tr><tr><td align="left" valign="middle">DENSITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;If a histogram is available on COLUMN_NAME, then this column displays the selectivity of a value that spans fewer than 2 endpoints in the histogram.</td></tr><tr><td align="left" valign="middle">NUM_NULLS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of NULLs in the column</td></tr><tr><td align="left" valign="middle">NUM_BUCKETS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Number of buckets in the histogram for the column</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which this column was most recently analyzed</td></tr><tr><td align="left" valign="middle">SAMPLE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Sample size used in analyzing this column</td></tr><tr><td align="left" valign="middle">CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the character set</td></tr><tr><td align="left" valign="middle">CHAR_COL_DECL_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Declaration length of the character type column</td></tr><tr><td align="left" valign="middle">GLOBAL_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;For partitioned tables, indicates whether column statistics were collected for the table</td></tr><tr><td align="left" valign="middle">USER_STATS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether statistics were entered directly by the user (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">AVG_COL_LEN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Average length of the column (in bytes)</td></tr><tr><td align="left" valign="middle">CHAR_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Displays the length of the column in characters.</td></tr><tr><td align="left" valign="middle">CHAR_USED</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates that the column uses BYTE length semantics (B) or CHAR length semantics (C)</td></tr><tr><td align="left" valign="middle">V80_FMT_IMAGE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data is in release older image format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">DATA_UPGRADED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates whether the column data has been upgraded to the latest type version format (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HISTOGRAM</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Indicates existence/type of histogram</td></tr><tr><td align="left" valign="middle">IDENTITY_COLUMN</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether this is an identity column (YES) or not (NO)</td></tr></tbody></table>

<a id="3fb01b14bacac529"></a>
#### USER_TAB_COMMENTS

USER_TAB_COMMENTS displays comments on the tables and views owned by the current user.

**Column 정보**

<a id="ce39a7eac5f3981c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object</td></tr><tr><td align="left">TABLE_TYPE</td><td align="left">VARCHAR(32)</td><td align="left">Type of the object</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Comment on the object</td></tr></tbody></table>

<a id="a69f1e034e7f4e3f"></a>
#### USER_TAB_IDENTITY_COLS

USER_TAB_IDENTITY_COLS describes all table identity columns.

**Column 정보**

<a id="ca42820743632619"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the identity column</td></tr><tr><td align="left" valign="middle">GENERATION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Generation type of the identity column. Possible values are ALWAYS or BY DEFAULT</td></tr><tr><td align="left" valign="middle">IDENTITY_OPTIONS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Options for the identity column sequence generator</td></tr></tbody></table>

<a id="0ea57017d08c124a"></a>
#### USER_TAB_PLACE

USER_TAB_PLACE describes node placement of cluster tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="552363d33947edd1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Member identifier of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Member name of the node where the table placed</td></tr><tr><td align="left" valign="middle">MEMBER_OFFLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">data of the cluster member is offline or not</td></tr><tr><td align="left" valign="middle">SCN</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">table scn of the node where the table placed</td></tr><tr><td align="left" valign="middle">NUM_ROWS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of rows in the table</td></tr><tr><td align="left" valign="middle">BLOCKS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Number of used blocks of the node where the table placed</td></tr><tr><td align="left" valign="middle">LAST_ANALYZED</td><td align="left" valign="middle">TIMESTAMP(6) WITHOUT TIME ZONE</td><td align="left" valign="middle">Date on which the table was most recently analyzed</td></tr></tbody></table>

<a id="8cc3243c0db7092c"></a>
#### USER_TAB_PRIVS

USER_TAB_PRIVS describes the object grants for which the current user is the object owner, grantor, or grantee.

**Column 정보**

<a id="b54bc9b77b92507e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="49bd80cbd638d2fe"></a>
#### USER_TAB_PRIVS_MADE

USER_TAB_PRIVS_MADE describes the object grants for which the current user is the object owner.

**Column 정보**

<a id="cfb3850756adc39e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user or role to whom access was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="e0b8f0748577e246"></a>
#### USER_TAB_PRIVS_RECD

USER_TAB_PRIVS_RECD describes the object grants for which the current user is the grantee.

**Column 정보**

<a id="cc26448567009f22"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Owner of the object</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user who performed the grant</td></tr><tr><td align="left" valign="middle">PRIVILEGE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Privilege on the object</td></tr><tr><td align="left" valign="middle">GRANTABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the GRANT OPTION (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">HIERARCHY</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">Indicates whether the privilege was granted with the HIERARCHY OPTION (YES) or not (NO)</td></tr></tbody></table>

<a id="eb950951d383e1b7"></a>
#### USER_TAB_SHARDS

USER_TAB_SHARDS describes shard information of sharded tables owned by the current user in the cluster system.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="93c762e83e6f9945"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the table</td></tr><tr><td align="left" valign="middle">SHARD_STRATEGY</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Sharding strategy of the table:<br>the value in (HASH SHARDING, RANGE SHARDING, LIST SHARDING)</td></tr><tr><td align="left" valign="middle">SHARD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Shard name</td></tr><tr><td align="left" valign="middle">SHARD_NUMBER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Shard number</td></tr><tr><td align="left" valign="middle">SHARD_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">Shard definition (if hash sharded, the value is null)</td></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Group identifier where the shard placed</td></tr><tr><td align="left" valign="middle">GROUP_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Group Name where the shard placed</td></tr></tbody></table>

<a id="b45b0f21998cd775"></a>
#### USER_USERS

USER_USERS describes the current user.

**Column 정보**

<a id="0dc94bc59b485d52"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">USERNAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the user</td></tr><tr><td align="left" valign="middle">USER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID number of the user</td></tr><tr><td align="left" valign="middle">ACCOUNT_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Account status: the value in ( OPEN, EXPIRED, EXPIRED(GRACE), LOCKED(TIMED), LOCKED, EXPIRED &amp; LOCKED(TIMED), EXPIRED(GRACE) &amp; LOCKED(TIMED), EXPIRED &amp; LOCKED, EXPIRED(GRACE) &amp; LOCKED )</td></tr><tr><td align="left" valign="middle">LOCK_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp the account was locked if account status was LOCKED</td></tr><tr><td align="left" valign="middle">EXPIRY_DATE</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">Timestamp of expiration of the account</td></tr><tr><td align="left" valign="middle">DEFAULT_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for data</td></tr><tr><td align="left" valign="middle">TEMPORARY_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the default tablespace for temporary tables or the name of a tablespace group</td></tr><tr><td align="left" valign="middle">INDEX_TABLESPACE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Default tablespace for index</td></tr><tr><td align="left" valign="middle">CREATED</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">User creation timestamp</td></tr><tr><td align="left" valign="middle">INITIAL_RSRC_CONSUMER_GROUP</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Initial resource consumer group for the user</td></tr><tr><td align="left" valign="middle">EXTERNAL_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;User external name</td></tr></tbody></table>

<a id="b9d9185f2ebe50e6"></a>
#### USER_VIEWS

USER_VIEWS describes the views owned by the current user.

**Column 정보**

<a id="8c66e0c43278c240"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the view</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the view</td></tr><tr><td align="left" valign="middle">TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Length of the view text</td></tr><tr><td align="left" valign="middle">TEXT</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">View text</td></tr><tr><td align="left" valign="middle">TYPE_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the type clause of the typed view</td></tr><tr><td align="left" valign="middle">TYPE_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Length of the WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">OID_TEXT</td><td align="left" valign="middle">VARCHAR(4000)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;WITH OID clause of the typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Owner of the type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">VIEW_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Type of the view if the view is a typed view</td></tr><tr><td align="left" valign="middle">SUPERVIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle"><ul><li>reserved</li></ul>&nbsp;Name of the superview</td></tr><tr><td align="left" valign="middle">EDITIONING_VIEW</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Reserved for future use</td></tr><tr><td align="left" valign="middle">READ_ONLY</td><td align="left" valign="middle">VARCHAR(1)</td><td align="left" valign="middle">Indicates whether the view is read-only (Y) or not (N)</td></tr></tbody></table>

<a id="6d7101b7ff15bcb0"></a>
### 기타 View

ALL 계열이나 DBA 계열, USER 계열이 아닌 view나 테이블이다.

<a id="2aed231f5a379c46"></a>
#### AUDIT_POLICIES

AUDIT_POLICIES contains one row for each audit policy.

**Column 정보**

<a id="205fc7a76d254f32"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enabled (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the audit policy</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the audit policy</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the audit policy</td></tr></tbody></table>

<a id="513c1853a2e073df"></a>
#### AUDIT_POLICY_OPTIONS

AUDIT_POLICY_OPTIONS describes all audit policies created in the database.

**Column 정보**

<a id="70a37f7f92043135"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">auditing option defined in the audit policy</td></tr><tr><td align="left" valign="middle">AUDIT_OPTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">The values of AUDIT_OPTION_TYPE_NAME in ( 'DATABASE PRIVILEGE', 'SYSTEM ACTION', 'OBJECT ACTION' )</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name, for an object-specific auditing option</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">object type name, for an object-specific auditing option</td></tr></tbody></table>

<a id="e60b8c262c2a23c3"></a>
#### AUDIT_POLICY_ENABLED

AUDIT_POLICY_ENABLE describes all the audit policies that are enable in the database.

**Column 정보**

<a id="2fab4a4189df443e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">audit policy name</td></tr><tr><td align="left" valign="middle">ENABLED_OPT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">enable option of the audit policy, the possible values are BY, EXCEPT</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name for whom the audit policy is enable</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="2eb922e8e06a1b57"></a>
#### AUDIT_TRAIL

AUDIT_TRAIL displays audit records from the audit trail.

**Column 정보**

<a id="6d7fb3783e9b4d90"></a>
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

<a id="d8fa12f92a86dba7"></a>
#### DATABASE_PROPERTIES

DATABASE_PROPERTIES lists permanent database properties.

**Column 정보**

<a id="a312591004126ea5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;PROPERTY_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Property name</td></tr><tr><td align="left">&nbsp;PROPERTY_VALUE</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property value</td></tr><tr><td align="left">&nbsp;DESCRIPTION</td><td align="left">&nbsp;VARCHAR(4000)</td><td align="left">&nbsp;Property description</td></tr></tbody></table>

<a id="63a9d3fbbd65d89b"></a>
#### DBC_TABLE_TYPE_INFO

Identify the ODBC/JDBC table types available in this database.

**Column 정보**

<a id="fbfa138c56061b1e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE_ID</td><td align="left">&nbsp;NUMBER</td><td align="left">&nbsp;number identifier of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;DBC_TABLE_TYPE</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;name of the table type in ODBC/JDBC</td></tr><tr><td align="left">&nbsp;IS_SUPPORTED</td><td align="left">&nbsp;BOOLEAN</td><td align="left">&nbsp;is supported feature</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;comments of the table type</td></tr></tbody></table>

<a id="1cbaa523a139c7e7"></a>
#### DICTIONARY

DICTIONARY contains descriptions of data dictionary tables and views.

**Column 정보**

<a id="682028c715371bd5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">&nbsp;TABLE_SCHEMA</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Schema of the object</td></tr><tr><td align="left">&nbsp;TABLE_NAME</td><td align="left">&nbsp;VARCHAR(128)</td><td align="left">&nbsp;Name of the object</td></tr><tr><td align="left">&nbsp;COMMENTS</td><td align="left">&nbsp;VARCHAR(1024)</td><td align="left">&nbsp;Text comment on the object</td></tr></tbody></table>

<a id="ef194c2bd171af11"></a>
#### DICT_COLUMNS

DICT_COLUMNS contains descriptions of columns in data dictionary tables and views.

**Column 정보**

<a id="30fbaf14308bf474"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_SCHEMA</td><td align="left">VARCHAR(128)</td><td align="left">Schema of the object that contains the column</td></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the object that contains the column</td></tr><tr><td align="left">COLUMN_NAME</td><td align="left">VARCHAR(128)</td><td align="left">Name of the column</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">Text comment on the column</td></tr></tbody></table>

<a id="f385f780256a6877"></a>
#### IMPLEMENTATION_INFO

IMPLEMENTATION_INFO contains information about various aspects that are left implementation-defined.

**Column 정보**

<a id="d44b265accf28eff"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">identifier of the implementation item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="331165070d612adf"></a>
#### IMPLEMENTATION_INFO_BASE

The IMPLEMENTATION_INFO_BASE table has one row for each implementation information item.

**Column 정보**

<a id="8c18f0504299aae9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation item</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">SUB_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation item</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if the implementation item is supported, FALSE if not</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">Value of the implementation item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation item</td></tr></tbody></table>

<a id="c64e6c7389e58e94"></a>
#### JDBC_CLIENT_PROPS

JDBC_CLIENT_PROPS is the set of jdbc client properties.

**Column 정보**

<a id="a41a2a699502b9c6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">property name</td></tr><tr><td align="left">MAX_LEN</td><td align="left">NATIVE_INTEGER</td><td align="left">max length of a value</td></tr><tr><td align="left">DEFAULT_VALUE</td><td align="left">VARCHAR(128)</td><td align="left">default value</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(256)</td><td align="left">descrption on that property</td></tr></tbody></table>

<a id="6eb35c6e9cc2712f"></a>
#### PRODUCT

PRODUCT is about the product name, version for ODBC, JDBC interface.

**Column 정보**

<a id="1384848a5d70da11"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(32)</td><td align="left">the product name</td></tr><tr><td align="left">VERSION</td><td align="left">VARCHAR(128)</td><td align="left">product full version information</td></tr><tr><td align="left">PRODUCT_VERSION</td><td align="left">NUMBER</td><td align="left">product version</td></tr><tr><td align="left">MAJOR_VERSION</td><td align="left">NUMBER</td><td align="left">major version</td></tr><tr><td align="left">MINOR_VERSION</td><td align="left">NUMBER</td><td align="left">minor version</td></tr><tr><td align="left">PATCH_VERSION</td><td align="left">NUMBER</td><td align="left">patch version</td></tr></tbody></table>

<a id="cc3ef135b349186f"></a>
#### SESSION_PRIVS

SESSION_PRIVS describes the privileges that are currently available to the user.

**Column 정보**

<a id="83c5a3d0b17dc63e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE</td><td align="left">VARCHAR(256)</td><td align="left">Name of the privilege</td></tr></tbody></table>

<a id="0f171b20a67bda25"></a>
#### SUPPLEMENTAL_LOG_TABLE_INFO

SUPPLEMENTAL_LOG_TABLE_INFO describes table-level supplemental logging status.

**Column 정보**

<a id="93176c0a9616be05"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Schema of the object</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">Name of the object</td></tr><tr><td align="left" valign="middle">SUPPLEMENTAL_LOG_DATA_PK</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Status of table-level PRIMARY KEY COLUMNS supplemental logging: IMPLICIT, EXPLICIT, NO</td></tr></tbody></table>

<a id="8072af73d6669adf"></a>
### Aliased Synonym

DICTIONARY_SCHEMA 내의 view나 테이블을 가리키는 public synonym이다.

<a id="f3b46c42cdb77f37"></a>
#### COLS

COLS is a public synonym for USER_TAB_COLUMNS.

<a id="58c5f9652cf7cc94"></a>
#### DICT

DICT is a public synonym for DICTIONARY.

<a id="5f86e818ba1d2a0d"></a>
#### IND

IND is a public synonym for USER_INDEXES.

<a id="42baf3485ab70d10"></a>
#### OBJ

OBJ is a public synonym for USER_OBJECTS.

<a id="020f72fd8446a9e7"></a>
#### SEQ

SEQ is a public synonym for USER_SEQUENCES.

<a id="496da48cd5fdd77b"></a>
#### TABS

TABS is a public synonym for USER_TABLES.

<a id="ac6101a002bac098"></a>
## INFORMATION_SCHEMA

INFORMATION_SCHEMA 스키마의 view들은 SQL 표준에서 정의한 INFORMATION_SCHEMA의 view들과 동일한 정보를 제공한다.

해당 view들을 사용하려면 다음과 같이 InformationSchema.sql 을 실행해야 한다.

- Standalone의 경우

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/standalone/InformationSchema.sql
```

- Cluster의 경우

```
% gsql sys gliese --as sysdba --import  $GOLDILOCKS_HOME/admin/cluster/InformationSchema.sql
```

> INFORMATION_SCHEMA의 view와 테이블들은 open 단계부터 조회할 수 있다.

<a id="0f02c91112b610ac"></a>
### COLUMNS

Identify the columns of tables defined in this catalog that are accessible to given user or role.

**Column 정보**

<a id="d9ea47527ec0978c"></a>
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

<a id="4aeed2956255af81"></a>
### COLUMN_PRIVILEGES

Identify the privileges on columns of tables defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="21829ece62cb6166"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted column privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the column privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name of the column on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( SELECT, INSERT, UPDATE, REFERENCES )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="92e3030b77b1b565"></a>
### CONSTRAINT_COLUMN_USAGE

Identify the columns used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column 정보**

<a id="87c5c7a470202861"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="3c4c1892d671fcb1"></a>
### CONSTRAINT_TABLE_USAGE

Identify the tables that are used by referential constraints, unique constraints, check constraints, and assertions defined in this catalog and owned by a given user or role.

**Column 정보**

<a id="0ed934fe64be56ae"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr></tbody></table>

<a id="e79a0420e0165fea"></a>
### INFORMATION_SCHEMA_CATALOG_NAME

Identify the catalog that contains the Information Schema.

**Column 정보**

<a id="5a807c5d65d0a83b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CATALOG_NAME</td><td align="left">VARCHAR(128)</td><td align="left">the name of catalog in which this Information Schema resides</td></tr></tbody></table>

<a id="33d3801eba122bb6"></a>
### KEY_COLUMN_USAGE

Identify the columns defined in this catalog that are constrained as keys and that are accessible by a given user or role.

**Column 정보**

<a id="9622cb635fba0cd6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the column that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the constraint being described</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position of the specific column in the constraint being described. If the constraint described is a key of cardinality 1 (one), then the value of ORDINAL_POSITION is always 1 (one).</td></tr><tr><td align="left" valign="middle">POSITION_IN_UNIQUE_CONSTRAINT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the constraint being described is a foreign key constraint, then the value of POSITION_IN_UNIQUE_CONSTRAINT is the ordinal position of the referenced column corresponding to the referencing column being described, in the corresponding unique key constraint.</td></tr></tbody></table>

<a id="a98b52f73aada557"></a>
### PARAMETERS

Identify the SQL parameters of SQL-invoked routines defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="3291770cb52daff1"></a>
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

<a id="b1f9db648392de94"></a>
### REFERENTIAL_CONSTRAINTS

Identify the referential constraints defined on tables in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="512a0c1a9c138bed"></a>
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

<a id="f64133e59afa66f0"></a>
### ROUTINES

Identify the SQL-invoked routines in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="d96588a0fb30f9ec"></a>
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

<a id="5bf351df5e562b25"></a>
### ROUTINE_PRIVILEGES

Identify the privileges on SQL-invoked routines defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="26b0ccd93a087596"></a>
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

<a id="47cab32daf80699f"></a>
### ROUTINE_ROUTINE_USAGE

Identify each SQL-invoked routine owned by a given user or role on which an SQL routine defined in this catalog is dependent.

**Column 정보**

<a id="4adc0348e41b8f06"></a>
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

<a id="0e2fe946f5be3edb"></a>
### ROUTINE_SEQUENCE_USAGE

Identify each external sequence generator owned by a given user or role on which some SQL routine defined in this catalog is dependent.

**Column 정보**

<a id="57b2ce4645371a84"></a>
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

<a id="38232dba5a3b906a"></a>
### ROUTINE_TABLE_USAGE

Identify the tables owned by a given user or role on which SQL routines defined in this catalog are dependent.

**Column 정보**

<a id="92c8c45122d2d249"></a>
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

<a id="250d1971fe8cf78c"></a>
### SCHEMATA

Identify the schemata in a catalog that are owned by given user or accessible to given user or role.

**Column 정보**

<a id="8dd3919e22113812"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CATALOG_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the schema</td></tr><tr><td align="left" valign="middle">SCHEMA_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name</td></tr><tr><td align="left" valign="middle">SCHEMA_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the schema</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">DEFAULT_CHARACTER_SET_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">character set name of the default character set for columns and domains in the schemata</td></tr><tr><td align="left" valign="middle">SQL_PATH</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">character representation of schema path specification</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the schema</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the schema</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the schema</td></tr></tbody></table>

<a id="950463cce27a5e06"></a>
### SEQUENCES

Identify the external sequence generators defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="60844d34d884832b"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SEQUENCE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the sequence</td></tr><tr><td align="left" valign="middle">SEQUENCE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">sequence name</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the standard name of the data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_PRECISION_RADIX</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the radix ( 2 or 10 ) of the precision of the numerical data type</td></tr><tr><td align="left" valign="middle">NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the numeric scale of the exact numerical data type</td></tr><tr><td align="left" valign="middle">START_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the start value of the sequence generator</td></tr><tr><td align="left" valign="middle">MINIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the minimum value of the sequence generator</td></tr><tr><td align="left" valign="middle">MAXIMUM_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the maximum value of the sequence generator</td></tr><tr><td align="left" valign="middle">INCREMENT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the increment of the sequence generator</td></tr><tr><td align="left" valign="middle">CYCLE_OPTION</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">cycle option</td></tr><tr><td align="left" valign="middle">CACHE_SIZE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">number of sequence numbers to cache</td></tr><tr><td align="left" valign="middle">DECLARED_DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DECLARED_NUMERIC_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the sequence generator</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the sequence generator</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the sequence generator</td></tr></tbody></table>

<a id="d5fb0178296c8785"></a>
### SQL_FEATURES

List the features and subfeatures of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="3cf2c138ddadf0cf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">SUB_FEATURE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the subfeature, or a single space if not a subfeature</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="8d13475b4b7db6ac"></a>
### SQL_IMPLEMENTATION_INFO

List the SQL-implementation information items defined in this ISO/IEC 9075 standard and, for each of these, indicate the value supported by the SQL-implementation.

**Column 정보**

<a id="37a3312e67623597"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the implementation information item</td></tr><tr><td align="left" valign="middle">IMPLEMENTATION_INFO_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the implementation information item</td></tr><tr><td align="left" valign="middle">INTEGER_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column CHARACTER_VALUE</td></tr><tr><td align="left" valign="middle">CHARACTER_VALUE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">value of the implementation information item, or null if the value is contained in the column INTEGER_VALUE</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the implementation information item</td></tr></tbody></table>

<a id="0fe14a17832f31f2"></a>
### SQL_PACKAGES

List the packages of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="3d934ed4deed6043"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="d3799e4bccae3c1d"></a>
### SQL_PARTS

List the parts of this ISO/IEC 9075 standard, and indicate which of these the SQL-implementation supports.

**Column 정보**

<a id="12e89e69bacaa826"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ID</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">identifier string of the conformance element</td></tr><tr><td align="left" valign="middle">NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the conformance element</td></tr><tr><td align="left" valign="middle">IS_SUPPORTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">TRUE if an SQL-implementation fully supports that conformance element described when SQL-data in the identified catalog is accessed through that implementation, FALSE if not</td></tr><tr><td align="left" valign="middle">IS_VERIFIED_BY</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">If full support for the conformance element described has been verified by testing, then the IS_VERIFIED_BY column shall contain information identifying the conformance test used to verify the conformance claim; otherwise, IS_VERIFIED_BY shall be the null value</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the conformance element</td></tr></tbody></table>

<a id="4d256a4ebc418e1a"></a>
### SQL_SIZING

List the sizing items of this ISO/IEC 9075 standard, for each of these, indicate the size supported by the SQL-implementation.

**Column 정보**

<a id="ec90d64aedaed16f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SIZING_ID</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">identifier of the sizing item</td></tr><tr><td align="left" valign="middle">SIZING_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">descriptive name of the sizing item</td></tr><tr><td align="left" valign="middle">SUPPORTED_VALUE</td><td align="left" valign="middle">NATIVE_INTEGER</td><td align="left" valign="middle">value of the sizing item, or 0 if the size is unlimited or cannot be determined, or null if the features for which the sizing item is applicable are not supported</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">possibly a comment pertaining to the sizing item</td></tr></tbody></table>

<a id="c2caccf08ff3bcf4"></a>
### STATISTICS

Provide a list of statistics about a single table and the indexes associated with the table that are accessible to a given user or role.

**Column 정보**

<a id="8124d00c3ed1b2d3"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">STAT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">statistics type: the value in ( TABLE STAT, INDEX CLUSTERED, INDEX HASHED, INDEX OTHER )</td></tr><tr><td align="left" valign="middle">NON_UNIQUE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the index does not allow duplicate values</td></tr><tr><td align="left" valign="middle">INDEX_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the index</td></tr><tr><td align="left" valign="middle">INDEX_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the index</td></tr><tr><td align="left" valign="middle">INDEX_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the index</td></tr><tr><td align="left" valign="middle">INDEX_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the index</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name that participates in the index</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ordinal position of the specific column in the index described</td></tr><tr><td align="left" valign="middle">IS_ASCENDING_ORDER</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">index key column being described is sorted in ASCENDING(TRUE) or DESCENDING(FALSE) order</td></tr><tr><td align="left" valign="middle">IS_NULLS_FIRST</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">the null values of the key column are sorted before(TRUE) or after(FALSE) non-null values</td></tr><tr><td align="left" valign="middle">CARDINALITY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of rows in the table; otherwise, it is the number of unique values in the index</td></tr><tr><td align="left" valign="middle">PAGES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the number of pages used for the table; otherwise, it is the number of pages used for the current index.</td></tr><tr><td align="left" valign="middle">FILTER_CONDITION</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">filter condition, if any.</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">if STAT_TYPE is (TABLE TYPE), then this is the table comments; otherwise, it is the index comments.</td></tr></tbody></table>

<a id="10a77b9e373a4fb4"></a>
### TABLES

Identify the tables defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="b789527fc9f3f17e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table</td></tr><tr><td align="left" valign="middle">TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( BASE TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM VERSIONED, FIXED TABLE, DUMP TABLE )</td></tr><tr><td align="left" valign="middle">DBC_TABLE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">ODBC/JDBC table type: the value is in ( TABLE, VIEW, GLOBAL TEMPORARY, LOCAL TEMPORARY, SYSTEM TABLE, ALIAS, SYNONYM )</td></tr><tr><td align="left" valign="middle">TABLESPACE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name of the table, NULL if view</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_START_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version start column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_END_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a system-versioned table, then the name of the system-version end column of the table</td></tr><tr><td align="left" valign="middle">SYSTEM_VERSION_RETENTION_PERIOD</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a system-versioned table, then the character representation of the value of the retention period of the table</td></tr><tr><td align="left" valign="middle">SELF_REFERENCING_COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table is a typed table, then the name of the self-referencing column of the table</td></tr><tr><td align="left" valign="middle">REFERENCE_GENERATION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table has a self-referencing column, the value is in ( SYSTEM GENERATED, USER GENERATED, DERIVED )</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the catalog name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the schema name of the structured type</td></tr><tr><td align="left" valign="middle">USER_DEFINED_TYPE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">if the table being described is a table of a structured type, the name of the structured type</td></tr><tr><td align="left" valign="middle">IS_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable-into table</td></tr><tr><td align="left" valign="middle">IS_TYPED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a typed table</td></tr><tr><td align="left" valign="middle">COMMIT_ACTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">if the table is a temporary table, the value is in ( DELETE, PRESERVE )</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the table</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the table</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the table</td></tr></tbody></table>

<a id="8a75ba82edf9d716"></a>
### TABLE_CONSTRAINTS

Identify the table constraints defined on tables in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="80bc3dd163cce205"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">CONSTRAINT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the constraint</td></tr><tr><td align="left" valign="middle">CONSTRAINT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the constraint being described</td></tr><tr><td align="left" valign="middle">CONSTRAINT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">constraint name</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name who owns the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of the table to to which the table constraint being described applies</td></tr><tr><td align="left" valign="middle">CONSTRAINT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( PRIMARY KEY, UNIQUE, FOREIGN KEY, NOT NULL, CHECK )</td></tr><tr><td align="left" valign="middle">IS_DEFERRABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is a deferrable constraint</td></tr><tr><td align="left" valign="middle">INITIALLY_DEFERRED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an initially deferred constraint</td></tr><tr><td align="left" valign="middle">ENFORCED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an enforced constraint</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">created time of the constraint</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">last modified time of the constraint</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the constraint</td></tr></tbody></table>

<a id="0b4e38778d9a5d51"></a>
### TABLE_PRIVILEGES

Identify the privileges on tables defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="8656e98e13395484"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted table privileges</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of some user or role, or PUBLIC to indicate all users, to whom the table privilege being described is granted</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table owner name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the table on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CONTROL, SELECT, INSERT, UPDATE, DELETE, REFERENCES, LOCK, INDEX, ALTER )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr><tr><td align="left" valign="middle">WITH_HIERARCHY</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the privilege was granted WITH HIERARCHY OPTION or not</td></tr></tbody></table>

<a id="6173fc594d90a01a"></a>
### USAGE_PRIVILEGES

Identify the USAGE privileges on objects defined in this catalog that are available to or granted by a given user or role.

**Column 정보**

<a id="cacb6f3fc29dac3f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GRANTOR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization name of the user who granted usage privileges, on the object of the type identified by OBJECT_TYPE</td></tr><tr><td align="left" valign="middle">GRANTEE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">authorization identifier of some user or role, or PUBLIC to indicate all users, to whom the usage privilege being described is granted</td></tr><tr><td align="left" valign="middle">OBJECT_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the object of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">object name of the type identified by OBJECT_TYPE on which the privilege being described was granted</td></tr><tr><td align="left" valign="middle">OBJECT_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( DOMAIN, CHARACTER SET, COLLATION, TRANSLATION, SEQUENCE )</td></tr><tr><td align="left" valign="middle">PRIVILEGE_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( USAGE )</td></tr><tr><td align="left" valign="middle">IS_GRANTABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is grantable</td></tr></tbody></table>

<a id="fa0e11a19e94d64c"></a>
### VIEWS

Identify the viewed tables defined in this catalog that are accessible to a given user or role.

**Column 정보**

<a id="1a60049855b7d72c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_DEFINITION</td><td align="left" valign="middle">LONG VARCHAR</td><td align="left" valign="middle">the character representation of the user-specified query expression contained in the corresponding view descriptor</td></tr><tr><td align="left" valign="middle">CHECK_OPTION</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the value is in ( CASCADED, LOCAL, NONE )</td></tr><tr><td align="left" valign="middle">IS_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an updatable view</td></tr><tr><td align="left" valign="middle">INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">is an insertable view</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_UPDATABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an update INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_DELETABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether a delete INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_TRIGGER_INSERTABLE_INTO</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether an insert INSTEAD OF trigger is defined on the view or not</td></tr><tr><td align="left" valign="middle">IS_COMPILED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is compiled or not</td></tr><tr><td align="left" valign="middle">IS_AFFECTED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">whether the view is affected by modification of underlying object or not</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the view</td></tr></tbody></table>

<a id="6abd4f3c5e410d7e"></a>
### VIEW_ROUTINE_USAGE

Identify each routine owned by a given user or role on which a view defined in this catalog is dependent.

**Column 정보**

<a id="6fd21c02e9894355"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">SPECIFIC_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific catalog name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific owner name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific schema name of a routine contained in the query expression of the view being described</td></tr><tr><td align="left" valign="middle">SPECIFIC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">specific name of a routine contained in the query expression of the view being described</td></tr></tbody></table>

<a id="6522a57a6314e93e"></a>
### VIEW_TABLE_USAGE

Identify the tables on which viewed tables defined in this catalog and owned by a given user or role are dependent.

**Column 정보**

<a id="af317d47e0c7b398"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">VIEW_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the viewed table</td></tr><tr><td align="left" valign="middle">VIEW_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">view name of the viewed table</td></tr><tr><td align="left" valign="middle">TABLE_CATALOG</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">catalog name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">table name of a table that is explicitly or implicitly referenced in the original query expression of the compiled view being described</td></tr></tbody></table>

<a id="be3a2988882eafa4"></a>
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
각각의 view를 어떤 시작 단계에서 조회할 수 있는지는 다음과 같은 질의를 통해 확인할 수 있다.

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

<a id="a2f2f6a006ab8b75"></a>
### GV$ Global View

Cluster에서는 거의 모든 V$ view에 대응하는 GV$ view를 제공한다.  
V$ view가 현재 접속한 서버의 정보를 조회하는 반면에 GV$ view는 모든 서버의 정보를 조회한다.  
GV$ view는 V$ view의 모든 column 정보를 포함하는데 이에 추가로 데이터를 획득한 서버 (cluster member)를 의미하는 ORIGIN_MEMBER_NAME column을 갖는다.

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

위의 예에서 ORIGIN_MEMBER_NAME 정보는 각 트랜잭션 정보를 G1N1, G2N1, G1N2, G2N2에 해당하는 cluster member로부터 획득했음을 알 수 있다.

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

<a id="e4f5de6bd4b50beb"></a>
### V$AGABLE_INFO

The V$AGABLE_INFO displays the system agable information.

**Column 정보**

<a id="15e16df8a3ade879"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SCN</td><td align="left">VARCHAR(32)</td><td align="left">system scn</td></tr><tr><td align="left">AGABLE_SCN</td><td align="left">VARCHAR(32)</td><td align="left">system agable scn</td></tr><tr><td align="left">AGABLE_SCN_GAP</td><td align="left">VARCHAR(32)</td><td align="left">gap between system scn and agable scn</td></tr><tr><td align="left">OLDEST_SESSION_ID</td><td align="left">NUMBER</td><td align="left">identifier of session blocking aging</td></tr></tbody></table>

<a id="055a278e38b82fda"></a>
### V$ARCHIVELOG

The V$ARCHIVELOG displays information of log archiving.

**Column 정보**

<a id="3a732819fca57586"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">ARCHIVELOG_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database log mode: the value in ( NOARCHIVELOG, ARCHIVELOG )</td></tr><tr><td align="left" valign="middle">LAST_ARCHIVED_LOG</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">sequence number of last archived log file</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_DIR</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">archive destination path</td></tr><tr><td align="left" valign="middle">ARCHIVELOG_FILE_PREFIX</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">file prefix name of the archived log</td></tr></tbody></table>

<a id="d46668d49037a36a"></a>
### V$AUDITABLE_DB_PRIVILEGES

The V$AUDITABLE_DB_PRIVILEGES displays auditable database privileges.

**Column 정보**

<a id="7c33be5582cd79e6"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PRIVILEGE_ID</td><td align="left">NUMBER</td><td align="left">database privilege identifier</td></tr><tr><td align="left">PRIVILEGE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">database privilege name</td></tr></tbody></table>

<a id="b41cc53cda66f791"></a>
### V$AUDITABLE_SYSTEM_ACTIONS

The V$AUDITABLE_SYSTEM_ACTIONS displays auditable system actions.

**Column 정보**

<a id="c50cc8fcefb89f6d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ACTION_ID</td><td align="left">NUMBER</td><td align="left">auditable system action identifier</td></tr><tr><td align="left">ACTION_NAME</td><td align="left">VARCHAR(128)</td><td align="left">auditable system action name</td></tr></tbody></table>

<a id="13960bf496a54a73"></a>
### V$BACKUP

The V$BACKUP displays information of backup.

**Column 정보**

<a id="eb14c7327e982919"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">BACKUP_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">indicates whether the tablespace begin backup ( ACTIVE ) or not ( INACTIVE )</td></tr><tr><td align="left" valign="middle">BACKUP_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the last checkpoint lsn of tablespace when backup started</td></tr></tbody></table>

<a id="17705c6c024acb45"></a>
### V$BALANCER

The V$BALANCER displays information of balancer.

**Column 정보**

<a id="16a2de0efe796182"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">balancer process identifier</td></tr><tr><td align="left">CUR_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">current number of connections</td></tr><tr><td align="left">CONNECTIONS</td><td align="left">NUMBER</td><td align="left">total number of connections</td></tr><tr><td align="left">CONNECTIONS_HIGHWATER</td><td align="left">NUMBER</td><td align="left">highest number of connections</td></tr><tr><td align="left">MAX_CONNECTIONS</td><td align="left">NUMBER</td><td align="left">maximum connections</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">status</td></tr></tbody></table>

<a id="5f287b6fdce5a779"></a>
### V$CLUSTER_DISPATCHER

The V$CLUSTER_DISPATCHER displays cluster dispatcher information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="154866bcc30e895f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">DISPATCHER_ID</td><td align="left">NUMBER</td><td align="left">dispatcher identifier</td></tr><tr><td align="left">IS_SYNC</td><td align="left">BOOLEAN</td><td align="left">whether the dispatcher is sync or not</td></tr><tr><td align="left">RX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has received through the dispatcher</td></tr><tr><td align="left">TX_BYTES</td><td align="left">NUMBER</td><td align="left">total amount of data that has transmitted through the dispatcher</td></tr><tr><td align="left">RX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs received</td></tr><tr><td align="left">TX_JOBS</td><td align="left">NUMBER</td><td align="left">the total number of jobs transmitted</td></tr></tbody></table>

<a id="2d0e4d63e9de55ce"></a>
### V$CLUSTER_LOCATION

The V$CLUSTER_LOCATION displays cluster location information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="7f1f8e4c92892750"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">MEMBER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">member name</td></tr><tr><td align="left">HOST</td><td align="left">VARCHAR(128)</td><td align="left">host address of a member</td></tr><tr><td align="left">PORT</td><td align="left">NUMBER</td><td align="left">host port of a member</td></tr></tbody></table>

<a id="7955a89d3bc88f7b"></a>
### V$CLUSTER_MEMBER

The V$CLUSTER_MEMBER displays cluster member information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="43fc03d92d67742c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">MEMBER_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member identifier</td></tr><tr><td align="left" valign="middle">MEMBER_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">member position</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">status of the member: the value in ( ACTIVE, INACTIVE )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is global coordnator (TRUE) or not (FALSE)</td></tr><tr><td align="left" valign="middle">IS_GROUP_COORD</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether a member is group coordnator (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="1ce72a5b1789abb2"></a>
### V$COLUMNS

The V$COLUMNS has one row for each column of all the performance views (views beginning with V$).

V$COLUMNS를 사용할 수 없는 nomount와 mount 단계에서 performance view의 column 정보를 조회하려면 아래 예제와 같이 `\`desc를 사용한다.

```
gSQL> \desc V$INSTANCE

COLUMN_NAME     TYPE                           IS_NULLABLE
--------------- ------------------------------ -----------
RELEASE_VERSION VARCHAR(64)          FALSE      
STARTUP_TIME    TIMESTAMP(2) WITHOUT TIME ZONE FALSE      
INSTANCE_STATUS VARCHAR(16)          FALSE
```

**Column 정보**

<a id="983934df613fe792"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">COLUMN_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">column name</td></tr><tr><td align="left" valign="middle">ORDINAL_POSITION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the ordinal position (&gt; 0) of the column in the performance view</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">the data type name that a user declared</td></tr><tr><td align="left" valign="middle">DATA_PRECISION</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the precision value that a user declared</td></tr><tr><td align="left" valign="middle">DATA_SCALE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">the scale value that a user declared</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">comments of the column</td></tr></tbody></table>

<a id="33fbc15a07d0f419"></a>
### V$CONTROLFILE

This view displays information about GOLDILOCKS control files.

**Column 정보**

<a id="1ead4a0c950b1014"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(16)</td><td align="left">control file status ( VALID, CORRUPTED )</td></tr><tr><td align="left">CONTROLFILE_NAME</td><td align="left">VARCHAR(1152)</td><td align="left">control file name ( absolute path )</td></tr><tr><td align="left">LAST_CHECKPOINT_LSN</td><td align="left">NATIVE_BIGINT</td><td align="left">the last checkpoint lsn</td></tr><tr><td align="left">IS_PRIMARY</td><td align="left">BOLLEAN</td><td align="left">indicates whether the control file is primary</td></tr></tbody></table>

<a id="fdec5d65c77714f0"></a>
### V$DATAFILE

The V$DATAFILE displays information of all datafiles.

**Column 정보**

<a id="c8df5f357d5cad65"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">DATAFILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">datafile name ( absolute path )</td></tr><tr><td align="left" valign="middle">CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">LSN at last checkpoint ( null if temporary tablespace )</td></tr><tr><td align="left" valign="middle">CREATION_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">timestamp of the datafile creation</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">datafile size ( in bytes )</td></tr><tr><td align="left" valign="middle">LOADED_CHECKPOINT_LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">checkpoint LSN of the datafile loaded in memory</td></tr><tr><td align="left" valign="middle">CORRUPT_PAGE_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">number of corrupt pages in the datafile</td></tr></tbody></table>

<a id="fa24d442284c6770"></a>
### V$DB_FILE

The V$DB_FILE displays a list of all files using in database.

**Column 정보**

<a id="2cb16442385c846a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">FILE_NAME</td><td align="left">VARCHAR(1024)</td><td align="left">file name</td></tr><tr><td align="left">FILE_TYPE</td><td align="left">VARCHAR(16)</td><td align="left">file type</td></tr></tbody></table>

<a id="abad2f63f48f64d7"></a>
### V$DISPATCHER

The V$DISPATCHER displays information of dispatchers.

**Column 정보**

<a id="da348a59f2ace41e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">dispatcher process identifier</td></tr><tr><td align="left" valign="middle">RESPONSE_JOB_COUNT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">response job count</td></tr><tr><td align="left" valign="middle">ACCEPT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">indicates whether this dispatcher is accepting new connections</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">process start time</td></tr><tr><td align="left" valign="middle">CUR_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">current number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total number of connections</td></tr><tr><td align="left" valign="middle">CONNECTIONS_HIGHWATER</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">highest number of connections</td></tr><tr><td align="left" valign="middle">MAX_CONNECTIONS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum connections</td></tr><tr><td align="left" valign="middle">RECV_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">receive status</td></tr><tr><td align="left" valign="middle">RECV_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of received</td></tr><tr><td align="left" valign="middle">RECV_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of received</td></tr><tr><td align="left" valign="middle">RECV_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">RECV_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of receive (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">send status</td></tr><tr><td align="left" valign="middle">SEND_BYTES</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total bytes of sent</td></tr><tr><td align="left" valign="middle">SEND_UNITS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total units of sent</td></tr><tr><td align="left" valign="middle">SEND_IDLE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total idle time of send (1/100 second)</td></tr><tr><td align="left" valign="middle">SEND_BUSY</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">total busy time of send (1/100 second)</td></tr></tbody></table>

<a id="e74a25b50fd9e83a"></a>
### V$ERROR_CODE

The V$ERROR_CODE displays a list of all GOLDILOCKS error codes.

**Column 정보**

<a id="9269e18c30e71c13"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">ERROR_CODE</td><td align="left">NUMBER</td><td align="left">GOLDILOCKS error code</td></tr><tr><td align="left">SQL_STATE</td><td align="left">VARCHAR(32)</td><td align="left">standard SQLSTATE code</td></tr><tr><td align="left">ERROR_MESSAGE</td><td align="left">VARCHAR(1024)</td><td align="left">error message</td></tr></tbody></table>

<a id="7d394788810b7015"></a>
### V$GLOBAL_TRANSACTION

The V$GLOBAL_TRANSACTION displays information on the currently active global transactions.

**Column 정보**

<a id="2c07335de3bfaa47"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">global transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">GLOBAL_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the global transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the global transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">global transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the global transaction is repreparable</td></tr></tbody></table>

<a id="b3d9141fbbea5bcd"></a>
### V$INCREMENTAL_BACKUP

The V$INCREMENTAL_BACKUP displays information about control files and datafiles in backup sets from the control file.

**Column 정보**

<a id="9ea85e7e6a243098"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">BACKUP_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">backup file name ( absolute path )</td></tr><tr><td align="left" valign="middle">BACKUP_SCOPE</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">incremental backup scope: the value in ( database, tablespace, control )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_LEVEL</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">incremental backup level: the value in ( 0, 1, 2, 3, 4 )</td></tr><tr><td align="left" valign="middle">INCREMENTAL_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">incremental backup type: the value in ( DIFFERENTIAL, CUMULATIVE )</td></tr><tr><td align="left" valign="middle">LSN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">all changes up to checkpoint LSN are included in this backup</td></tr><tr><td align="left" valign="middle">BEGIN_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup beginning time</td></tr><tr><td align="left" valign="middle">COMPLETION_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">incremental backup completion time</td></tr></tbody></table>

<a id="7f7269ae94612f2e"></a>
### V$INSTANCE

This view displays the state of the current instance.

> 데이터베이스가 open 단계로 전이될 때 READ ONLY나 READ WRITE를 선택할 수 있는데, 만약 생략할 경우 DATABASE_ACCESS_MODE 프로퍼티에 설정된 값을 이용하여 DATA_ACCESS_MODE를 결정한다. 따라서 DATA_ACCESS_MODE는 nomount나 mount 단계에서 NONE으로 표시된다.

**Column 정보**

<a id="4c7a32352f5adf18"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">RELEASE_VERSION</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">release version</td></tr><tr><td align="left" valign="middle">STARTUP_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">time when the instance was started</td></tr><tr><td align="left" valign="middle">INSTANCE_STATUS</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">status of the instance: the value in ( STARTED, MOUNTED, OPEN )</td></tr><tr><td align="left" valign="middle">DATA_ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(16)</td><td align="left" valign="middle">data access mode of the instance: the value in ( NONE, READ_ONLY, READ_WRITE )</td></tr></tbody></table>

<a id="fceaa2945420cda9"></a>
### V$JOURNALING

The V$JOURNALING displays journaling information.

> Cluster에서만 사용할 수 있다.

**Column 정보**

<a id="b26859c43b85207a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TABLE_NAME</td><td align="left">VARCHAR(128)</td><td align="left">table name</td></tr><tr><td align="left">SHARD_ID</td><td align="left">NUMBER</td><td align="left">shard identifier</td></tr><tr><td align="left">RECORD_COUNT</td><td align="left">NUMBER</td><td align="left">journaled record count</td></tr><tr><td align="left">TOTAL_SIZE</td><td align="left">NUMBER</td><td align="left">total size of journaled records (byte)</td></tr></tbody></table>

<a id="e519aa54d5f8822e"></a>
### V$KEYWORDS

The V$KEYWORDS displays a list of all SQL keywords.

**Column 정보**

<a id="7b87a46e9f931b0d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">KEYWORD_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of keyword</td></tr><tr><td align="left" valign="middle">KEYWORD_LENGTH</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">length of the keyword</td></tr><tr><td align="left" valign="middle">IS_RESERVED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the keyword cannot be used as an identifier (TRUE) or whether the keyword is not reserved (FALSE)</td></tr></tbody></table>

<a id="184fc27c84c321fc"></a>
### V$LATCH

The V$LATCH shows latch information.

**Column 정보**

<a id="3f1cba4068e5e2c2"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">LATCH_DESCRIPTION</td><td align="left">VARCHAR(64)</td><td align="left">latch description</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">reference count</td></tr><tr><td align="left">SPIN_LOCK</td><td align="left">VARCHAR(3)</td><td align="left">indicates whether the spin lock is locked ( YES ) or not ( NO )</td></tr><tr><td align="left">WAIT_COUNT</td><td align="left">NUMBER</td><td align="left">wait count</td></tr><tr><td align="left">CURRENT_MODE</td><td align="left">VARCHAR(32)</td><td align="left">current latch mode: the value in ( INITIAL, SHARED, EXCLUSIVE )</td></tr></tbody></table>

<a id="553c0b7b68c41997"></a>
### V$LOGFILE

The V$LOGFILE displays information of all redo log members.

**Column 정보**

<a id="2a567a60bd156eff"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">GROUP_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">redo log group identifier</td></tr><tr><td align="left" valign="middle">FILE_NAME</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">name of the log member</td></tr><tr><td align="left" valign="middle">GROUP_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the log group: the value in ( UNUSED, ACTIVE, CURRENT, INACTIVE )</td></tr><tr><td align="left" valign="middle">FILE_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file sequence number of the log member</td></tr><tr><td align="left" valign="middle">FILE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">file size of the log member ( in bytes )</td></tr></tbody></table>

<a id="c5ccd107a383cd75"></a>
### V$LOCK_WAIT

This view lists the locks currently held and outstanding requests for a lock.

**Column 정보**

<a id="fe91af3734f9b64f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">GRANT_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that holds the lock</td></tr><tr><td align="left">REQUEST_TRANS_ID</td><td align="left">NUMBER</td><td align="left">transaction identifier that requests the lock</td></tr></tbody></table>

<a id="7140098b467e3ca4"></a>
### V$PROCESS_STAT

The V$PROCESS_STAT displays goldilocks process statistics.

**Column 정보**

<a id="d7879d26b6891cd9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="3e0d25df58575dca"></a>
### V$PROCESS_MEM_STAT

The V$PROCESS_MEM_STAT displays goldilocks process memory statistics.

**Column 정보**

<a id="38e358bd05ce3c5f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="75ec97826a8d5dcc"></a>
### V$PROCESS_SQL_STAT

The V$PROCESS_SQL_STAT displays goldilocks process SQL statistics.

**Column 정보**

<a id="1ef9a865159400f5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">PROC_ID</td><td align="left">NUMBER</td><td align="left">goldilocks process identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="d29f6a2a0b856835"></a>
### V$PROPERTY

The V$PROPERTY displays a list of all properties at current session. Otherwise, the instance-wide value.

**Column 정보**

<a id="a53af807410b0d16"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value for the session. otherwise, the instance-wide value</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the session</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr></tbody></table>

<a id="7d9460b7c0de5785"></a>
### V$PSM_RESERVED_WORDS

The V$PSM_RESERVED_WORDS displays a list of all PSM reserved keywords. Reserved words cannot be used in variable name or procedure name.

**Column 정보**

<a id="d3a02f0a97bae9e8"></a>
| Column name | Data type | Description |
| --- | --- | --- |
| KEYWORD_NAME | VARCHAR(128) | name of keyword |
| KEYWORD_LENGTH | NUMBER | length of the keyword |

<a id="5f38dad949e34483"></a>
### V$QUEUE

The V$QUEUE displays information of queue.

**Column 정보**

<a id="bfec70a081d25bfd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TYPE</td><td align="left">NUMBER</td><td align="left">queue type ( COMMON or DISPATCHER )</td></tr><tr><td align="left">INDEX</td><td align="left">NUMBER</td><td align="left">index</td></tr><tr><td align="left">QUEUED</td><td align="left">NUMBER</td><td align="left">number of items in the queue</td></tr><tr><td align="left">WAIT</td><td align="left">NUMBER</td><td align="left">total time that all items in this queue have waited (1/100 second)</td></tr><tr><td align="left">TOTALQ</td><td align="left">VARCHAR(128)</td><td align="left">total number of items that have ever been in the queue</td></tr></tbody></table>

<a id="cdfe387213bbdd08"></a>
### V$RESERVED_WORDS

The V$RESERVED_WORDS displays a list of all SQL reserved keywords. Reserved words cannot be used in table name or column name.

**Column 정보**

<a id="bebac312b3c4916f"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">KEYWORD_NAME</td><td align="left">VARCHAR(128)</td><td align="left">name of keyword</td></tr><tr><td align="left">KEYWORD_LENGTH</td><td align="left">NUMBER</td><td align="left">length of the keyword</td></tr></tbody></table>

<a id="3e37cc93cfc1c720"></a>
### V$SESSION

The V$SESSION displays session information for each current session.

**Column 정보**

<a id="ad5c2c8e282f5c33"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier ( -1 if inactive transaction )</td></tr><tr><td align="left" valign="middle">CONNECTION_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">connection type: the value in ( DA, TCP )</td></tr><tr><td align="left" valign="middle">USER_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">user name</td></tr><tr><td align="left" valign="middle">SESSION_STATUS</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">status of the session: the value in ( CONNECTED, SIGNALED, SNIPED, DEAD )</td></tr><tr><td align="left" valign="middle">SERVER_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">server type: the value in ( DEDICATED, SHARED )</td></tr><tr><td align="left" valign="middle">PROCESS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client process identifier</td></tr><tr><td align="left" valign="middle">LOGON_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">logon time</td></tr><tr><td align="left" valign="middle">PROGRAM_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">program name</td></tr><tr><td align="left" valign="middle">CLIENT_ADDRESS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">client address ( null if DA )</td></tr><tr><td align="left" valign="middle">CLIENT_PORT</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">client port ( 0 if DA )</td></tr><tr><td align="left" valign="middle">FAILOVER_TYPE</td><td align="left" valign="middle">VARCHAR(13)</td><td align="left" valign="middle">indicates whether and to what extent transparent application failover (TAF) is enabled for the session ( NONE, SESSION )</td></tr><tr><td align="left" valign="middle">FAILED_OVER</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is running in failover mode and failover has occurred (YES) or not (NO)</td></tr><tr><td align="left" valign="middle">IS_AUDITED</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the session is audited (YES) or not (NO)</td></tr></tbody></table>

<a id="e561500a066acd6b"></a>
### V$SESSION_AUDIT

The V$SESSION_AUDIT displays audited session information.

**Column 정보**

<a id="1bac7bb984c8bc38"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">SERIAL_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session serial number</td></tr><tr><td align="left" valign="middle">POLICY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">active audit policy name</td></tr><tr><td align="left" valign="middle">WHEN_SUCCESS</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing successful events or not</td></tr><tr><td align="left" valign="middle">WHEN_FAILURE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">indicates whether the audit policy is enable for auditing unsuccessful events or not</td></tr></tbody></table>

<a id="3a93cb1ca752a1bc"></a>
### V$SESSION_CONNECT_INFO

The V$SESSION_CONNECT_INFO displays information about network connections for the current session.

**Column 정보**

<a id="b915123fff96d216"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">SERIAL_NO</td><td align="left">NUMBER</td><td align="left">session serial number</td></tr><tr><td align="left">CLIENT_CHARSET</td><td align="left">VARCHAR(40)</td><td align="left">client character set</td></tr></tbody></table>

<a id="7b861b651db03450"></a>
### V$SESSION_EVENT

The V$SESSION_EVENT displays information on waits for an event by a session.

**Column 정보**

<a id="76dfcaeb4949e899"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">ID of the session</td></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">MAX_WAIT</td><td align="left">NUMBER</td><td align="left">Maximum time waited for the event by the session (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="6239d0ad46a06a93"></a>
### V$SESSION_STAT

The V$SESSION_STAT displays session statistics.

**Column 정보**

<a id="ee1fc7b46f526864"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="ea8a4cf88b41edc4"></a>
### V$SESSION_MEM_STAT

The V$SESSION_MEM_STAT displays session memory statistics.

**Column 정보**

<a id="c1b4fe74fd23096c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="7ffae79b4275d59c"></a>
### V$SESSION_SQL_STAT

The V$SESSION_SQL_STAT displays session SQL statistics.

**Column 정보**

<a id="7c05ca89ad79575a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">SESS_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr></tbody></table>

<a id="8fe8aa04bdd6de62"></a>
### V$SESSION_WAIT

The V$SESSION_WAIT displays the current or last wait for each session.

**Column 정보**

<a id="ad8ca3588973bc46"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">ID of the session</td></tr><tr><td align="left" valign="middle">SEQ_NO</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Identifier of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Name of the wait event</td></tr><tr><td align="left" valign="middle">WAIT_EVENT_NAME</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">A number that uniquely identifies the current or last wait (incremented for each wait)</td></tr><tr><td align="left" valign="middle">P1TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the first parameter for the wait event</td></tr><tr><td align="left" valign="middle">P1</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">First wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P1HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">First wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P2TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the second parameter for the wait event</td></tr><tr><td align="left" valign="middle">P2</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Second wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P2HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Second wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">P3TEXT</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Description of the third parameter for the wait event</td></tr><tr><td align="left" valign="middle">P3</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">Third wait event parameter (in decimal)</td></tr><tr><td align="left" valign="middle">P3HEX</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">Third wait event parameter (in hex)</td></tr><tr><td align="left" valign="middle">STATE</td><td align="left" valign="middle">VARCHAR(64)</td><td align="left" valign="middle">Wait state</td></tr><tr><td align="left" valign="middle">WAIT_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">If the session is currently waiting, then the value is time waited for the current wait. If the session is not in a wait, then the value is the duration of the last wait (in microseconds)</td></tr><tr><td align="left">TIME_SINCE_LAST_WAIT</td><td align="left">NUMBER</td><td align="left">Time elapsed since the end of the last wait (in microseconds). If the session is currently in a wait, then the value is 0.</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="0c690ccef913d3b2"></a>
### V$SHARED_MODE

The V$SHARED_MODE displays information of shared mode.

**Column 정보**

<a id="3a3f13866f88ccec"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(128)</td><td align="left">name</td></tr><tr><td align="left">VALUE</td><td align="left">VARCHAR(128)</td><td align="left">value</td></tr></tbody></table>

<a id="2184f032a485462e"></a>
### V$SHARED_SERVER

The V$SHARED_SERVER displays information of shared servers.

**Column 정보**

<a id="bedfcc9e5ccc38c1"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">PROCESS_ID</td><td align="left">NUMBER</td><td align="left">shared server process identifier</td></tr><tr><td align="left">PROCESSED_JOB_COUNT</td><td align="left">NUMBER</td><td align="left">processed job count</td></tr><tr><td align="left">STATUS</td><td align="left">VARCHAR(128)</td><td align="left">status</td></tr><tr><td align="left">IDLE</td><td align="left">NUMBER</td><td align="left">total idle time (1/100 second)</td></tr><tr><td align="left">BUSY</td><td align="left">NUMBER</td><td align="left">total busy time (1/100 second)</td></tr></tbody></table>

<a id="deb7245077c3b1b6"></a>
### V$SHM_SEGMENT

The V$SHM_SEGMENT displays a list of all shared memory segments.

**Column 정보**

<a id="26017e95b458dcc5"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SHM_NAME</td><td align="left">VARCHAR(32)</td><td align="left">shared memory segment name</td></tr><tr><td align="left">SHM_ID</td><td align="left">NUMBER</td><td align="left">shared memory segment identifier</td></tr><tr><td align="left">SHM_SIZE</td><td align="left">NUMBER</td><td align="left">shared memory segment size ( in bytes )</td></tr><tr><td align="left">SHM_KEY</td><td align="left">NUMBER</td><td align="left">shared memory segment key</td></tr><tr><td align="left">SHM_SEQ</td><td align="left">NUMBER</td><td align="left">shared memory segment sequence</td></tr><tr><td align="left">SHM_ADDR</td><td align="left">VARCHAR(32)</td><td align="left">start address of the shared memory segment</td></tr></tbody></table>

<a id="f62651b0f5405fe9"></a>
### V$SPROPERTY

The V$SPROPERTY displays a list of Properties. This is store a binary property file.

**Column 정보**

<a id="fc3851e7fe49cc8d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">PROPERTY_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the property</td></tr><tr><td align="left" valign="middle">DESCRIPTION</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">description of the property</td></tr><tr><td align="left" valign="middle">DATA_TYPE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">data type of the property</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">modifiable startup-phase: the value IN ( NO MOUNT / MOUNT / OPEN &amp; [BELOW|ABOVE] )</td></tr><tr><td align="left" valign="middle">VALUE_UNIT</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">unit of the property value: the value in ( NONE, BYTE, MS(milisec) )</td></tr><tr><td align="left" valign="middle">PROPERTY_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property value stored in the binary property file</td></tr><tr><td align="left" valign="middle">PROPERTY_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property value: the value is BINARY_FILE</td></tr><tr><td align="left" valign="middle">INIT_VALUE</td><td align="left" valign="middle">VARCHAR(2048)</td><td align="left" valign="middle">property init value for the system</td></tr><tr><td align="left" valign="middle">INIT_SOURCE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">source of the current property INIT_VALUE: the value IN ( USER, DEFAULT, ENV_VAR, BINARY_FILE, FILE, SYSTEM )</td></tr><tr><td align="left" valign="middle">MIN_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">MAX_VALUE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum value for property. null if type is varchar</td></tr><tr><td align="left" valign="middle">SES_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SESSION or not: the value in ( TRUE, FALSE )</td></tr><tr><td align="left" valign="middle">SYS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed with ALTER SYSTEM and when the change takes effect: the value in ( NONE, FALSE, IMMEDIATE, DEFERRED )</td></tr><tr><td align="left" valign="middle">IS_MODIFIABLE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">property can be changed or not: the value in ( TRUE, FALSE )</td></tr></tbody></table>

<a id="548ee753524a6325"></a>
### V$SQLFN_METADATA

The V$SQLFN_METADATA contains metadata about operators and built-in functions.

**Column 정보**

<a id="4da940bc08ce6448"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">FUNC_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the built-in function</td></tr><tr><td align="left" valign="middle">MINARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">minimum number of arguments for the function</td></tr><tr><td align="left" valign="middle">MAXARGS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">maximum number of arguments for the function</td></tr><tr><td align="left" valign="middle">IS_AGGREGATE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the function is an aggregate function (TRUE) or not (FALSE)</td></tr></tbody></table>

<a id="5f30e34ed523e507"></a>
### V$SQL_CACHE

The V$SQL_CACHE lists statistics of shared SQL plan.

**Column 정보**

<a id="2089f7efecf778c0"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SQL_HANDLE</td><td align="left">NUMBER</td><td align="left">SQL handle</td></tr><tr><td align="left">HASH_VALUE</td><td align="left">NUMBER</td><td align="left">hash value of the SQL statement</td></tr><tr><td align="left">REF_COUNT</td><td align="left">NUMBER</td><td align="left">count of prepared statements referencing the statement</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">CLOCK_ID</td><td align="left">NUMBER</td><td align="left">clock identifier</td></tr><tr><td align="left">PLAN_AGE</td><td align="left">NUMBER</td><td align="left">plan age</td></tr><tr><td align="left">USER_NAME</td><td align="left">VARCHAR(128)</td><td align="left">user name</td></tr><tr><td align="left">BIND_PARAM_COUNT</td><td align="left">NUMBER</td><td align="left">count of bind parameters</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">SQL full text</td></tr><tr><td align="left">PLAN_COUNT</td><td align="left">NUMBER</td><td align="left">physical plan count of the SQL statement</td></tr><tr><td align="left">PLAN_ID</td><td align="left">NUMBER</td><td align="left">plan identifier</td></tr><tr><td align="left">PLAN_SIZE</td><td align="left">NUMBER</td><td align="left">the total plan size of the SQL statement ( in bytes )</td></tr><tr><td align="left">PLAN_IS_ATOMIC</td><td align="left">BOOLEAN</td><td align="left">plan is atomic array insert or not</td></tr><tr><td align="left">PLAN_TEXT</td><td align="left">LONG VARCHAR</td><td align="left">plan text for SQL statement</td></tr></tbody></table>

<a id="6165b1024d56a016"></a>
### V$SQL_COMMAND

The V$SQL_COMMAND lists attribute information of each SQL command.

**Column 정보**

<a id="6212850822d2fbcf"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">COMMAND</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">SQL command</td></tr><tr><td align="left" valign="middle">FROM_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable from start-up phase</td></tr><tr><td align="left" valign="middle">UNTIL_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">executable until start-up phase</td></tr><tr><td align="left" valign="middle">ACCESS_MODE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">database access mode: values in (NONE, READ &amp; WRITE, READ, READ &amp; LOCK)</td></tr><tr><td align="left" valign="middle">NEED_FETCH</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">the command is a query which has result set and need fetch</td></tr><tr><td align="left" valign="middle">IS_DDL</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is a DDL(Data Defintion Language) or not</td></tr><tr><td align="left" valign="middle">AUTO_COMMIT</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is auto-commit or not</td></tr><tr><td align="left" valign="middle">IS_CACHEABLE</td><td align="left" valign="middle">VARCHAR(3)</td><td align="left" valign="middle">the command is plan-cacheable or not</td></tr><tr><td align="left" valign="middle">AUDIT_ACTION</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">auditiable action name for the SQL command</td></tr></tbody></table>

<a id="2b59f64f5776e21c"></a>
### V$SQL_HISTORY

The V$SQL_HISTORY displays information of SQLs.

**Column 정보**

<a id="69d9834fafca4e55"></a>
<table><tbody><tr><th align="center" valign="middle">Column name</th><th align="center" valign="middle">Data type</th><th align="center" valign="middle">Description</th></tr><tr><td align="left" valign="middle">DRIVER_MEMBER_POS</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">driver member position</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">statement start time</td></tr><tr><td align="left" valign="middle">EXEC_TIME</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">execution time(us)</td></tr><tr><td align="left" valign="middle">PREPARED</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is prepared ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">SUCCESS</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the statement is success ( YES )<br>or not ( NO )</td></tr><tr><td align="left" valign="middle">STATUS</td><td align="left" valign="middle">CHARACTER VARYING(16)</td><td align="left" valign="middle">status of the statement: the value in<br>( RUNNING, DONE )</td></tr><tr><td align="left" valign="middle">SQL_TEXT</td><td align="left" valign="middle">CHARACTER VARYING(1024)</td><td align="left" valign="middle">first 1024 bytes of the SQL text for the statement</td></tr></tbody></table>

<a id="115f96ee4621729b"></a>
### V$STATEMENT

The V$STATEMENT lists all statements.

**Column 정보**

<a id="cc1eaac5c7e91bfd"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">SESSION_ID</td><td align="left">NUMBER</td><td align="left">session identifier</td></tr><tr><td align="left">STMT_ID</td><td align="left">NUMBER</td><td align="left">statement identifier in a session</td></tr><tr><td align="left">STMT_VIEW_SCN</td><td align="left">NUMBER</td><td align="left">statement view scn</td></tr><tr><td align="left">SQL_TEXT</td><td align="left">VARCHAR(1024)</td><td align="left">first 1024 bytes of the SQL text for the statement</td></tr><tr><td align="left">START_TIME</td><td align="left">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left">statement start time</td></tr></tbody></table>

<a id="0b225c107903b9d9"></a>
### V$SYSTEM_EVENT

The V$SYSTEM_EVENT displays information on total waits for an event.

**Column 정보**

<a id="8a85da755b7494d7"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">WAIT_EVENT_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">WAIT_EVENT_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">TOTAL_WAITS</td><td align="left">NUMBER</td><td align="left">Total number of waits for the event</td></tr><tr><td align="left">TOTAL_TIMEOUTS</td><td align="left">NUMBER</td><td align="left">Total number of timeouts for the event</td></tr><tr><td align="left">TIME_WAITED</td><td align="left">NUMBER</td><td align="left">Total amount of time waited for the event (microsecond)</td></tr><tr><td align="left">AVERAGE_WAIT</td><td align="left">NUMBER</td><td align="left">Average amount of time waited for the event (microsecond)</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="8cc7487d22f76726"></a>
### V$SYSTEM_STAT

The V$SYSTEM_STAT displays system statistics.

**Column 정보**

<a id="8cac58f4966b3554"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="8cdd226d90e86257"></a>
### V$SYSTEM_MEM_STAT

The V$SYSTEM_MEM_STAT displays system memory statistics.

**Column 정보**

<a id="78146f4384208c2d"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="d56e0ecb3e628d4b"></a>
### V$SYSTEM_SQL_STAT

The V$SYSTEM_SQL_STAT displays system SQL statistics.

**Column 정보**

<a id="7a54d1fc758e863a"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">STAT_NAME</td><td align="left">VARCHAR(128)</td><td align="left">statistic name</td></tr><tr><td align="left">STAT_VALUE</td><td align="left">NUMBER</td><td align="left">statistic value</td></tr><tr><td align="left">COMMENTS</td><td align="left">VARCHAR(1024)</td><td align="left">comments</td></tr></tbody></table>

<a id="755e69d0261dfb76"></a>
### V$TABLES

The V$TABLES contains the definitions of all the performance views (views beginning with V$).

**Column 정보**

<a id="7d835a4d119d596e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TABLE_OWNER</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">owner name who owns the performance view</td></tr><tr><td align="left" valign="middle">TABLE_SCHEMA</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">schema name of the performance view</td></tr><tr><td align="left" valign="middle">TABLE_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">name of the performance view</td></tr><tr><td align="left" valign="middle">STARTUP_PHASE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">visible startup phase of the performance view</td></tr><tr><td align="left" valign="middle">CREATED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>created time of the performance view</td></tr><tr><td align="left" valign="middle">MODIFIED_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>modified time of the performance view</td></tr><tr><td align="left" valign="middle">COMMENTS</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle"><ul><li>available only in OPEN phase</li></ul>comments of the performance view</td></tr></tbody></table>

<a id="67e4fce274c45987"></a>
### V$TABLESPACE

This view displays tablespace information.

**Column 정보**

<a id="65cb697431f62481"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TBS_NAME</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace name</td></tr><tr><td align="left" valign="middle">TBS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">tablespace identifier</td></tr><tr><td align="left" valign="middle">TBS_ATTR</td><td align="left" valign="middle">VARCHAR(128)</td><td align="left" valign="middle">tablespace attribute: the value in ( device attribute (MEMORY) | temporary attribute (TEMPORARY, PERSISTENT) | usage attribute(DICT, UNDO, DATA, TEMPORARY) )</td></tr><tr><td align="left" valign="middle">IS_LOGGING</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is a logging tablespace ( YES ) or not ( NO )</td></tr><tr><td align="left" valign="middle">IS_ONLINE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the tablespace is ONLINE ( YES ) or OFFLINE ( NO )</td></tr><tr><td align="left" valign="middle">OFFLINE_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">indicates whether the tablespace can be taken online normally ( CONSISTENT ) or not ( INCONSISTENT ). null if the tablespace is ONLINE</td></tr><tr><td align="left" valign="middle">EXTENT_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">extent size of the tablespace ( in bytes )</td></tr><tr><td align="left" valign="middle">PAGE_SIZE</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">page size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="41eaf3fcca987ef3"></a>
### V$TABLESPACE_STAT

This view displays tablespace statistical information.

**Column 정보**

<a id="f424a765ac8ac719"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">TBS_NAME</td><td align="left">VARCHAR(128)</td><td align="left">tablespace name</td></tr><tr><td align="left">TBS_ID</td><td align="left">NUMBER</td><td align="left">tablespace identifier</td></tr><tr><td align="left">TOTAL_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">total extent count of the tablespace</td></tr><tr><td align="left">USED_META_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">meta extent count currently used on the tablespace</td></tr><tr><td align="left">USED_DATA_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">data extent count currently used on the tablespace</td></tr><tr><td align="left">FREE_EXT_COUNT</td><td align="left">NUMBER</td><td align="left">free extent count of the tablespace</td></tr><tr><td align="left">EXTENT_SIZE</td><td align="left">NUMBER</td><td align="left">extent size of the tablespace ( in bytes )</td></tr></tbody></table>

<a id="0c16c63fd381c3f4"></a>
### V$TRANSACTION

The V$TRANSACTION lists the active transactions in the system.

**Column 정보**

<a id="e396425d5094e65e"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction identifier</td></tr><tr><td align="left" valign="middle">SESSION_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">session identifier ( null if the global transaction is unassociated</td></tr><tr><td align="left" valign="middle">TRANS_SLOT_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction slot identifier</td></tr><tr><td align="left" valign="middle">PHYSICAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">physical transaction identifier</td></tr><tr><td align="left" valign="middle">TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction state: the value in ( ACTIVE, BLOCK, PREPARE, COMMIT, ROLLBACK, IDLE, PRECOMMIT )</td></tr><tr><td align="left" valign="middle">IS_GLOBAL</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the transaction is global or not</td></tr><tr><td align="left" valign="middle">TRANS_ATTRIBUTE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction attribute: the value in ( READ_ONLY, UPDATABLE, LOCKABLE, UPDATABLE | LOCKABLE )</td></tr><tr><td align="left" valign="middle">ISOLATION_LEVEL</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">transaction isolation level: the value in ( READ COMMITTED, SERIALIZABLE )</td></tr><tr><td align="left" valign="middle">TRANS_VIEW_SCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction view scn</td></tr><tr><td align="left" valign="middle">TCN</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction change number</td></tr><tr><td align="left" valign="middle">TRANS_SEQ</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">transaction sequence number</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">transaction start time</td></tr></tbody></table>

<a id="b2cfca320c875842"></a>
### V$WAIT_EVENT_CLASS_NAME

The V$WAIT_EVENT_CLASS_NAME displays information about Class of wait event.

**Column 정보**

<a id="5d91502c84032979"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the class of the wait event</td></tr></tbody></table>

<a id="90930114d7a2f958"></a>
### V$WAIT_EVENT_NAME

The V$WAIT_EVENT_NAME displays information about wait events.

**Column 정보**

<a id="3dc37db077fd774c"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the wait event</td></tr><tr><td align="left">NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the wait event</td></tr><tr><td align="left">DESCRIPTION</td><td align="left">VARCHAR(128)</td><td align="left">Description of the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the first parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the second parameter for the wait event</td></tr><tr><td align="left">PARAMETER1</td><td align="left">NUMBER</td><td align="left">Description of the third parameter for the wait event</td></tr><tr><td align="left">CLASS_ID</td><td align="left">NUMBER</td><td align="left">Identifier of the class of the wait event</td></tr><tr><td align="left">CLASS_NAME</td><td align="left">VARCHAR(64)</td><td align="left">Name of the class of the wait event</td></tr></tbody></table>

<a id="6299d103553443d7"></a>
### V$XA_TRANSACTION

The V$XA_TRANSACTION displays information on the currently active XA transactions.

**Column 정보**

<a id="31f0197c182472f9"></a>
<table><tbody><tr><th align="center">Column name</th><th align="center">Data type</th><th align="center">Description</th></tr><tr><td align="left" valign="middle">XA_TRANS_ID</td><td align="left" valign="middle">VARCHAR(1024)</td><td align="left" valign="middle">XA transaction identifier</td></tr><tr><td align="left" valign="middle">LOCAL_TRANS_ID</td><td align="left" valign="middle">NUMBER</td><td align="left" valign="middle">local transaction identifier</td></tr><tr><td align="left" valign="middle">XA_TRANS_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">state of the XA transaction: the value in ( NOTR, ACTIVE, IDLE, PREPARED, ROLLBACK_ONLY, HEURISTIC_COMPLETED )</td></tr><tr><td align="left" valign="middle">ASSO_STATE</td><td align="left" valign="middle">VARCHAR(32)</td><td align="left" valign="middle">associate state of the XA transaction: the value in ( NOT_ASSOCIATED, ASSOCIATED, ASSOCIATION_SUSPENDED )</td></tr><tr><td align="left" valign="middle">START_TIME</td><td align="left" valign="middle">TIMESTAMP(2) WITHOUT TIME ZONE</td><td align="left" valign="middle">XA transaction start time</td></tr><tr><td align="left" valign="middle">IS_REPREPARABLE</td><td align="left" valign="middle">BOOLEAN</td><td align="left" valign="middle">indicates whether the XA transaction is repreparable</td></tr></tbody></table>

---

[← 8. GOLDILOCKS 데이터베이스 이중화](8-goldilocks-데이터베이스-이중화.md) · [전체 목차](../README.md) · [10. Server Property →](10-server-property.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
