<a id="550b15dd9167e3da"></a>

# 19. SQL References (C~G)

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/550b15dd9167e3da)  
> Tag: `21c.1_35_tag`

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [Table of contents](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<a id="a7de81e9ff1d1b99"></a>
## CLOSE cursor_name

<a id="881cbbdc3846cdd8"></a>
### Function

It closes a cursor.

<a id="3b3912bb8f946081"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="410fcaa4c539ec96"></a>
### Syntax Rules and Parameters

<a id="7f7f1900ad66f689"></a>
#### cursor_name

The cursor should be open.  
The cursor should be declared with [DECLARE cursor_name](#d5d4c37681027dd4) statement in the session.

<a id="af65e92d8f0b1e9c"></a>
### Description

The cursor is an object which exists in the session and it does not affect the cursor in a different session.

<a id="6f603eb0f9da2461"></a>
### Example

The following is an example of DECLARE, OPEN, FETCH, and CLOSE the cursor by using gsql (interactive SQL tool).

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

<a id="d390e39e22522fd7"></a>
### Compatibility

**SQL standard compatibility**

<a id="ff2a94d9d9b394be"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="eef3bc9e18590025"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [FETCH cursor_name](#fcce02e780b87a86)

<a id="ab6593b2744b2d0f"></a>
## COMMENT ON name IS

<a id="4bb3b9a311c5c449"></a>
### Function

It stores the comments about the object in the dictionary.

<a id="ecef90e6ed9a49af"></a>
### Syntax

```
<comment statement> ::=
    COMMENT ON <comment object> IS 'comment string'
    ;

<comment object> ::=
      CLUSTER GROUP group_name
    | CLUSTER MEMBER member_name
    | DATABASE
    | PROFILE profile_name
    | AUTHORIZATION user_name
    | TABLESPACE tablespace_name
    | SCHEMA schema_name
    | TABLE [schema_name].table_name
    | COLUMN [schema_name].table_name.column_name
    | INDEX [schema_name].index_name
    | SEQUENCE [schema_name].sequence_name
    | CONSTRAINT [schema_name].constraint_name
    | PROCEDURE [schema_name].procedure_name
```

<a id="c6660439f98f177f"></a>
### Invocation and Access Rules

The altering privileges on each object are required to perform &lt;comment statement&gt; as follows.

- CLUSTER GROUP
    - ALTER SYSTEM ON DATABASE
- CLUSTER MEMBER
    - ALTER SYSTEM ON DATABASE
- DATABASE 
    - ALTER DATABASE ON DATABASE 
- PROFILE
    - ALTER PROFILE ON DATABASE
- AUDIT POLICY
    - AUDIT SYSTEM ON DATABASE
- AUTHORIZATION (user) 
    - ALTER USER ON DATABASE 
- AUTHORIZATION (role) 
    - ALTER ROLE ON DATABASE 
- TABLESPACE 
    - ALTER TABLESPACE ON DATABASE 
- SCHEMA: One of the following privileges is required. 
    - The owner of the schema 
    - CONTROL SCHEMA ON SCHEMA for the schema
    - ALTER SCHEMA ON DATABASE
- TABLE: One of the following privileges is required. 
    - The owner of the table 
    - CONTROL TABLE ON TABLE for the table
    - CONTROL SCHEMA ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE 
- COLUMN: One of the following privileges is required. 
    - The owner of the table to which the column belongs 
    - CONTROL TABLE ON TABLE for the table to which the column belongs 
    - CONTROL SCHEMA ON SCHEMA for the schema of the table to which the column belongs
    - ALTER ANY TABLE ON DATABASE 
- INDEX: One of the following privileges is required. 
    - The owner of the index
    - CONTROL SCHEMA ON SCHEMA for the schema to which the index belongs
    - ALTER ANY INDEX ON DATABASE 
- SEQUENCE 
    - The owner of the sequence 
    - CONTROL SCHEMA ON SCHEMA for the schema to which the sequence belongs
    - ALTER ANY SEQUENCE ON DATABASE 
- CONSTRAINT 
    - The owner of that constraint 
    - CONTROL SCHEMA ON SCHEMA for the schema to which the constraint belongs 
    - ALTER ANY TABLE ON DATABASE
- PROCEDURE
    - The owner of the stored procedure/function
    - CONTROL SCHEMA ON SCHEMA for the schema to which the stored procedure/function belongs
    - ALTER ANY PROCEDURE ON DATABASE

<a id="8b556ccc67d24917"></a>
### Syntax Rules and Parameters

<a id="9ce91f3891641cea"></a>
#### &lt;comment object&gt;

It is an object in which the comments are to be stored. The comments for the following database objects are stored.

- Cluster object
    - CLUSTER GROUP
    - CLUSTER MEMBER 
- Non-schema object 
    - DATABASE 
    - PROFILE
    - AUDIT POLICY
    - AUTHORIZATION (User or role) 
    - TABLESPACE 
    - SCHEMA 
- Schema object 
    - TABLE or VIEW 
    - COLUMN 
    - INDEX 
    - SEQUENCE 
    - CONSTRAINT
    - PROCEDURE or FUNCTION

If schema_name for the schema object is not specified, the schema name is determined by [Schema Path](13-sql-objects.md#1fd540af769e321f) of the user performing the statement.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="ec720177adfca7a6"></a>
#### 'comment string'

It describes the comments to be stored.  
Use the empty string ('') to delete the comments as follows.

```
COMMENT ON TABLE test_table IS '';
```

The length of the comment string can not exceed 1024 bytes.

<a id="f75ca3514480ae2e"></a>
### Description

The information can be retrieved from the COMMENTS column of the following dictionary view per each object type.

- Cluster objects
    - CLUSTER GROUP & CLUSTER MEMBER
        - DICTIONARY_SCHEMA.DBA_CLUSTER_COMMENTS view
- Non-schema objects
    - DATABASE
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - PROFILE
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - AUDIT POLICY
        - DICTIONARY_SCHEMA.AUDIT_POLICIES view
    - USER
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - TABLESPACE
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
    - SCHEMA
        - DICTIONARY_SCHEMA.ALL_NONSCHEMA_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_NONSCHEMA_COMMENTS view
- SQL schema objects
    - TABLE
        - DICTIONARY_SCHEMA.USER_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_TAB_COMMENTS view
    - VIEW
        - DICTIONARY_SCHEMA.USER_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_TAB_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_TAB_COMMENTS view
    - COLUMN
        - DICTIONARY_SCHEMA.USER_COL_COMMENTS view
        - DICTIONARY_SCHEMA.ALL_COL_COMMENTS view
        - DICTIONARY_SCHEMA.DBA_COL_COMMENTS view
    - INDEX
        - DICTIONARY_SCHEMA.USER_INDEXES view
        - DICTIONARY_SCHEMA.ALL_INDEXES view
        - DICTIONARY_SCHEMA.DBA_INDEXES view
    - SEQUENCE
        - DICTIONARY_SCHEMA.USER_SEQUENCES view
        - DICTIONARY_SCHEMA.ALL_SEQUENCES view
        - DICTIONARY_SCHEMA.DBA_SEQUENCES view
    - CONSTRAINT
        - DICTIONARY_SCHEMA.USER_CONSTRAINTS view
        - DICTIONARY_SCHEMA.ALL_CONSTRAINTS view
        - DICTIONARY_SCHEMA.DBA_CONSTRAINTS view
    - PROCEDURE & FUNCTION
        - DICTIONARY_SCHEMA.USER_PROCEDURES view
        - DICTIONARY_SCHEMA.ALL_PROCEDURES view
        - DICTIONARY_SCHEMA.DBA_PROCEDURES view

For more information about the detailed description of each view, refer to [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#f76942ec1e209b30).

<a id="7c758137e8efdc0f"></a>
### Examples

The following is an example of creating the comment on the table.

```
gSQL> COMMENT ON TABLE t1 IS 'test comment on table t1';

Comment created.
```

The following is an example of creating the comment on the column.

```
gSQL> COMMENT ON COLUMN t1.id IS 'test comment on column t1.id';

Comment created.
```

The following is an example of creating the comment on the schema.

```
gSQL> COMMENT ON SCHEMA s1 IS 'test comment on schema s1';

Comment created.
```

<a id="cb03b3e0430d6ada"></a>
### Compatibility

&lt;comment statement&gt; does not exist in SQL standard.

<a id="c2b7ad9d96c93c7b"></a>
## COMMIT

<a id="7600aa18aefc1bd7"></a>
### Function

It terminates the current transaction and makes all changes permanent.

<a id="b3c6881ae8c19fdd"></a>
### Syntax

```
<commit statement> ::=
    COMMIT [ WORK ] 
       [ [ <commit comment clause> ] [ <commit write clause> ] |
         [ <commit force clause> ] [ <commit comment clause> ] ]
    ;

<commit comment clause> ::=
      COMMENT 'comment_string'

<commit write clause> ::=
      WRITE [ WAIT | NOWAIT ]

<commit force clause> ::=
    FORCE 'xid_string'
```

<a id="0b152aac2dc56612"></a>
### Syntax Rules and Parameters

<a id="071247b5ef93cb18"></a>
#### WORK

It is the reserved word which does not affect the operation.

<a id="52af81d40d5a5428"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - It specifies the comment to the transaction when committing the transaction.

<a id="991ff494fb231e16"></a>
#### &lt;commit write clause&gt;

It determines whether to wait until the redo logs generated by the commit operation are written on the redo log file.

- WAIT
    - It waits until the redo logs generated by the commit operation are written to the redo log file, and then the operation is terminated. 
- NOWAIT
    - The operation is terminated when the redo logs generated by the commit operation are written to the redo log buffer.
- If it is not specified, it follows the property.

<a id="c31a186d0b1b9322"></a>
#### &lt;commit force clause&gt;

It is used to manually commit a distributed transaction.

- FORCE 'xid_string'
    - It commits the distributed transaction 'xid_string'.
    - 'xid_string' consists of *'format_id.transaction_id.branch_id'*.

<a id="02d5e418d18bbe1b"></a>
### Description

COMMIT statement completes the following statements which were executed in a transaction.

- Data Manipulation Language (DML) statement
    - It is the statement which changes data, such as INSERT, UPDATE, DELETE. 
- Data Definition Language (DDL) statement
    - It is the statement which changes the structure and definition of the objects, such as CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE.

Exceptionally, the following DDL statements which manage the OS resources or change the DATA TYPE are automatically committed.

- [CREATE TABLESPACE](#cfdf7d2f50958860)
- [DROP TABLESPACE](#a9171e5695f3e4e0)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](18-sql-references-a-b.md#19a6d7b58dfd96ca)

When performing COMMIT, the cursor opened by WITHOUT HOLD option is automatically closed. For more information about cursors, refer to the following cursor related statements.

- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)

If the transaction violates the DEFERRED constraint, the COMMIT statement fails and the transaction is rolled back. For more information about DEFERRED constraint, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

<a id="27bd4520905a3867"></a>
### Example

The following is an example of performing COMMIT after executing INSERT statement.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="d189d06b2f7da562"></a>
### Compatibility

**SQL standard compatibility**

<a id="5c08b816d7b0b2b1"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="e8c3febf88e246d2"></a>
### For More Information

Refer to the followings.

- [ROLLBACK](20-sql-references-h-z.md#1c726f64ce2dea9c)
- [SAVEPOINT savepoint_specifier](20-sql-references-h-z.md#723785c99b199c7c)

<a id="4f95ec95d004a1b2"></a>
## CREATE AUDIT POLICY

<a id="697e8b14527fe0f8"></a>
### Function

It creates an audit policy object.  
AUDIT POLICY should be performed to activate the created audit policy object.

<a id="18540fd0d36ed8da"></a>
### Syntax

```
<audit policy definition> ::= 
    CREATE AUDIT POLICY policy_name
    { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }
    ; 

<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<action_audit_clause> ::=
    ACTIONS { <object_action_audit> | <system_action_audit> } [, ...]

<object_action_audit> ::=
      ALL ON [schema_name.]object_name
    | <object_action> ON [schema_name.]object_name

<system_action_audit> ::=
      ALL
    | DDL
    | <system_action>
```

<a id="a37d73dcc1f16efe"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;audit policy definition&gt;.

<a id="7c1f156d3df68e67"></a>
### Syntax Rules and Parameters

<a id="4d17c6d187c4dc37"></a>
#### policy_name

It is the name of the audit policy to be created.

<a id="a620d115ea140a09"></a>
#### &lt;privilege_audit_clause&gt;

The privilege audit is auditing when the SQL statement is successfully performed by using the database privilege.  
It can audit a specific user performing SQL statement by using the database privilege, and it does not record the privilege audit for SYS user who is the owner of the database.

The following is an example of granting SELECT ANY TABLE privilege to user u1 and activating the audit policy.

```
CREATE AUDIT POLICY p1 
       PRIVILEGES SELECT ANY TABLE;

AUDIT POLICY p1;
```

If the user u1 performs the following SQL statement, the privilege audit differently operates.

- SELECT * FROM u1.t1;
    - It does not create the audit record by performing SQL statement with the privilege as an owner of table u1.t1.
- SELECT * FROM u2.t1;
    - It creates the audit record by performing SQL statement with SELECT ANY TABLE privilege.

&lt;database_privilege&gt; which can be described in the privilege audit can be viewed with the following query.

```
SELECT PRIVILEGE_NAME FROM V$AUDITABLE_DB_PRIVILEGES;
```

<a id="b6b7f85e1e89dbb8"></a>
#### &lt;action_audit_clause&gt;

It audits an action for a specific object and an action for the entire database.

<a id="289bf2f0966caaed"></a>
#### &lt;object_action_audit&gt;

<a id="ce6cd06f2ef086a0"></a>
##### ALL ON object_name

It means all actions which can list objects corresponding to object_name.

The following table describes audit actions of which each object type can audit.

**Audit action per object type**

<a id="4b49be6d18abd6f4"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored Function/Procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="f73c5ba0ad80f6fa"></a>
##### &lt;object_action&gt; ON object_name

Each separate action per a specific object should be listed by specifying ON clause as follows.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="68e6b4a895d34386"></a>
##### Caution of EXECUTE action

Auditing the success or the failure of stored function or stored procedure is determined only based on whether it is executable at the time of execution.

- WHENEVER NOT SUCCESSFUL creates the audit record when neither the stored function nor procedure is executable.
- WHENEVER SUCCESSFUL creates the audit record even though an error occurs while executing SQL statement within the stored function or the procedure 
- If an auditing for the failure of SQL statement within the stored function or the procedure is required, then the audit target should include the corresponding SQL statement.

<a id="8dfec52e3fac0018"></a>
#### &lt;system_action_audit&gt;

It audits the system action which occurs in the database regardless of a specific object.

- &lt;system_action&gt;

The valid system action can be retrieved by using the following query.

```
SELECT ACTION_NAME FROM V$AUDITABLE_SYSTEM_ACTIONS;
```

- ALL

It means all system actions.

- DDL

It means all Data Definition Language (DDL).

<a id="be98a59beedbc32f"></a>
### Description

An audit policy object is an object which defines auditing targets.    
Perform AUDIT POLICY statement to activate an audit policy.

Though it is possible to define and activate multiple audit policies, but it is recommended to maintain certain number of audit policies.    
It is also recommended to bind multiple small pieces of policies into a small number of groups.

The information about an option of the created audit policy object can be retrieved through AUDIT_POLICY_OPTIONS view as follows.

```
SELECT audit_option
     , audit_option_type
     , object_schema
     , object_name
  FROM audit_policy_options
 WHERE policy_name = 'P1'
;

AUDIT_OPTION AUDIT_OPTION_TYPE OBJECT_SCHEMA  OBJECT_NAME
------------ ----------------- -------------- ------------
DELETE	     OBJECT ACTION     U1	      T1
INSERT	     OBJECT ACTION     U1	      T1
UPDATE	     OBJECT ACTION     U1	      T1
```

<a id="2f8a82ae3b95df98"></a>
#### Creating Audit Record

If an action corresponding to multiple audit policies occurs, then one or more audit records are created.

If similar audit options are listed as follows, then one audit record is created.

- Defining an audit policy

```
CREATE AUDIT POLICY p1
       PRIVILEGES SELECT ANY TABLE
       ACTIONS SELECT;

AUDIT POLICY p1;
```

- Performing an audit action

```
SELECT * FROM other_user.t1;
```

If two different audit options are listed as follows, then two audit records are created.

- Defining an audit policy

```
CREATE AUDIT POLICY p1
       ACTIONS SELECT ON u1.t1
             , SELECT ON u2.t2;

AUDIT POLICY p1;
```

- Performing an audit action

```
SELECT COUNT(*) FROM u1.t1 A, u2.t2 B WHERE A.id = B.id;
```

If multiple audit policies are activated for the same action as follows, then two audit records are created.

- Defining an audit policy

```
CREATE AUDIT POLICY p1
       PRIVILEGES SELECT ANY TABLE;
AUDIT POLICY p1;

CREATE AUDIT POLICY p2
       ACTIONS SELECT;
AUDIT POLICY p2;
```

- Performing an audit action

```
SELECT * FROM other.t1;
```

<a id="b84d2231218fdd58"></a>
### Examples

The following is an example of defining an audit policy which audits an privilege.

```
CREATE AUDIT POLICY policy_table
       PRIVILEGES CREATE ANY TABLE
                , DROP ANY TABLE
;
```

The following is an example of defining an audit policy which audits an action for an object.

```
CREATE AUDIT POLICY policy_dml
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
             , ALL    ON u1.t2
;
```

The following is an example of defining an audit policy which audits the system action.

```
CREATE AUDIT POLICY policy_drop
       ACTIONS DROP TABLE, TRUNCATE TABLE
;
```

The following is an example of defining an audit policy which combines all examples above.

```
CREATE AUDIT POLICY policy_group
       PRIVILEGES CREATE ANY TABLE
                , DROP ANY TABLE
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
             , ALL    ON u1.t2
             , DROP TABLE
             , TRUNCATE TABLE
;
```

<a id="e2e99cdfd6af9d3d"></a>
### Compatibility

The audit policy does not exist in SQL standard.

<a id="3078ab653bdd8f27"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#4f95ec95d004a1b2)
    - [DROP AUDIT POLICY](#74a07e0949274daf)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#53347c6092b6e054)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](18-sql-references-a-b.md#9289801d878dbdc2)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#1d87c2f21b970bb9)

- Retrieving audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#c239152842953eb8)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#783e2ba71672a2fa)

<a id="3f7a6957233a40f7"></a>
## CREATE CLUSTER GROUP

<a id="cf6cd7889d4c0a25"></a>
### Function

It creates a cluster group which is to participate in a cluster system.

<a id="ee708ae3ad9358bb"></a>
### Syntax

```
<cluster group definition> ::=
    CREATE CLUSTER GROUP group_name 
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute> [<member position>]

<connection attribute> ::=
    HOST 'address' PORT port_no

<member position> ::=
    POSITION DEFAULT
  | POSITION MAX
  | POSITION number
```

<a id="f8b308df0e40354e"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  

ADMINISTRATION ON DATABASE privilege is required to perform &lt;cluster group definition&gt;.

<a id="d10b45383a41898d"></a>
### Syntax Rules and Parameters

<a id="902e039b670cc628"></a>
#### group_name

It is the name of a cluster group.  
An identical cluster group name or a cluster member name should not exist.  
The name length should be shorter than 128 bytes.

<a id="2605322276edf316"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group can include maximum 32 cluster members.  
A cluster group which is created first in a cluster system can define only one cluster member, and should include itself as a cluster member.

<a id="5124136bc7cb0e02"></a>
#### member_name

It is the name of a cluster member.  
The name of a cluster member should be same as the name of the member which was defined when creating the database of that member.  
An identical cluster group name or a cluster member name should not exist.  
The name length should be shorter than 128 bytes.

The start-up phase of the cluster member should be the GLOBAL OPEN phase.

<a id="1ebfc63856323437"></a>
#### &lt;connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
&lt;connection attribute&gt; should be as same as the HOST and PORT which were defined when the database of that cluster member was created.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST address uses ip v4 type.
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="d1b2f5ec4642dd14"></a>
#### &lt;member position&gt;

It assigns the position number of the cluster member.

- POSITION DEFAULT
    - The system automatically assigns the position number.
- POSITION MAX
    - It assigns the new member position number even when an empty position number exists.
    - It assigns the value bigger than the biggest member position.
- POSITION number
    - It assigns the position number corresponding to the number
    - The position number should be unique in the cluster system.
    - The position number should be an empty position number, and it should be same or smaller than the biggest position number.
- If it is omitted, the default value is POSITION DEFAULT.

The member_position information of the cluster member can be retrieved through DBA_CLUSTER view.

```
SELECT member_name, member_id, member_position FROM dba_cluster;
```

If the following position numbers are being used,

- G1N1: 0
- G1N2: 1
- G2N2: 3
- G3N2: 5

The following values are assigned according to each option.

- POSITION DEFAULT
    - It assigns 2 which is an empty value.
- POSITION MAX
    - It assigns 6 which is a value of a new position number.
- POSITION 3
    - It is duplicated, so it is an error.
- POSITION 4
    - It assigns 4 which is a position number.

<a id="f3121e9dd621ccaa"></a>
### Description

&lt;cluster group definition&gt; statement does not rebalance the shard of tables.

Perform the following statements to rebalance the shard to an added cluster group.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a)

<a id="262b9f85c8b3facd"></a>
### Examples

The following is an example of creating a cluster group which consists of two cluster members.

```
gSQL> 
CREATE CLUSTER GROUP g1
    CLUSTER MEMBER g1n1 HOST '192.168.0.11' PORT 10110
;

Cluster Group created.

gSQL>
ALTER CLUSTER GROUP g1
    ADD CLUSTER MEMBER g1n2 HOST '192.168.0.12' PORT 10120
;

Cluster Group altered.

gSQL> 
CREATE CLUSTER GROUP g2
    CLUSTER MEMBER g2n1 HOST '192.168.0.21' PORT 10210,
    CLUSTER MEMBER g2n2 HOST '192.168.0.22' PORT 10220
;

Cluster Group created.
```

<a id="8e85b486d50a8c62"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="7c930e8b113d5a3f"></a>
### For More Information

Refer to the followings.

- [DROP CLUSTER GROUP](#76a15fea6a02da13)
- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#0a6879be2602f377)

<a id="67ef6e090f63d08d"></a>
## CREATE CLUSTER LOCATION

<a id="cd79a495dbaaca33"></a>
### Function

It creates the connection information of a cluster member.

<a id="390857a8ba7685ea"></a>
### Syntax

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="190ab53f7bbc8b53"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;cluster location definition&gt;.

<a id="f56f4215f22ae765"></a>
### Syntax Rules and Parameters

<a id="9f40ff047312d1de"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should not exist in the registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="a2e0855a5067d05e"></a>
#### &lt;cluster connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST address uses ip v4 type.
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="1cc3bc18be7d9ac1"></a>
### Description

Generally, the information of the cluster location is automatically created by using the connection information provided when creating the cluster group or adding the cluster member. The created information is deleted together when deleting the cluster member and the cluster group.

If the information of the cluster location is modified, then the connection information can be modified by using [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#68afa63d36875d46) without deleting or recreating the cluster member.

<a id="627173216587b631"></a>
### Examples

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="cf98c5819a7b91ae"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="bcc779b770b884b0"></a>
### For More Information

Refer to [DROP CLUSTER LOCATION](#351e9009d382090f) .

<a id="f9c7eb32cc7ffaf4"></a>
## CREATE DISK DATA TABLESPACE

<a id="3957f0f0febfa463"></a>
### Function

It defines the disk data tablespace.

<a id="bf343741d9a90938"></a>
### Syntax

```
<disk data tablespace statement> ::=
    CREATE DISK [ DATA ] TABLESPACE tablespace_name
        DATAFILE <disk datafile clause> [, ...]
        [ <data tablespace management clause> [, ...] ]

<disk datafile clause> ::=
     'filename' 
        [ SIZE <size clause> | REUSE | SIZE <size clause> REUSE ]
        [ <autoextend clause> ]
        [ AT <domain_name> ]

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }

<size clause> ::=
    integer [ K | M | G | T ]

<data tablespace management clause> ::=
      { ONLINE | OFFLINE }
    | EXTSIZE <size clause>
```

<a id="a0124c1c327fcc5c"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;disk data tablespace definition&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege for the created tablespace.

The following privileges are required to create an object on the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace
- USAGE TABLESPACE ON DATABASE

<a id="780bdf32fc6e4044"></a>
### Syntax Rules and Parameters

<a id="6d13fa8995981b5d"></a>
#### tablespace_name

It is the name of the tablespace to be created.  
The length of the tablespace name should be shorter than 128 bytes.

<a id="e71f02b94e3f8b1c"></a>
#### &lt;disk datafile clause&gt;

- 'filename' 
    - It is the name of the file which stores and manages the data.
    - It is the space to store tables and index pages which were created in the disk tablespace.
    - filename is either a new file or an existing file. 
    - filename length should be shorter than 1024 bytes.

- SIZE &lt;size clause&gt; 
    - If it is a new file, then it specifies the initial size by using SIZE clause. 
    - If a file exists, then an error occurs. 
    - The file size can be in the range between 1 M ~ maximum 30 G.

- REUSE 
    - If it is an existing file, then it uses REUSE clause. 
    - If a file does not exist, then it creates a new file.
    - The size of the newly created files is determined by USER_DATA_TABLESPACE_SIZE property.

- SIZE &lt;size clause&gt; REUSE 
    - If both SIZE clause and REUSE clause are specified, then it is operated according to the existence of filename as follows. 
        - If it is a new filename, then it specifies the initial file size by using SIZE clause. 
        - If it is an existing filename, then it adjust the size to the value in SIZE clause.

<a id="043b6c64eb031836"></a>
#### &lt;autoextend clause&gt;

It sets the automatic expand property to ON or OFF. If it is set to ON, then it can specify the automatic expanded size and the maximum size of the data file.

<a id="f9806506eb260d6f"></a>
#### &lt;next size clause&gt;

It specifies the size to be extended when the data file in use does not have available space.

<a id="f40387a41757dc12"></a>
#### &lt;max size clause&gt;

It specifies the maximum expanded size of the data file.

<a id="b2e08bcc73b49e60"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="f6b866d88ee60488"></a>
#### &lt;domain_name&gt;

It is the name of member or the group to performs the statement.  
If it is omitted, then it is performed for all groups.

<a id="e9dc8a0834929d23"></a>
#### ONLINE | OFFLINE

It determines whether to ONLINE/ OFFLINE the tablespace.

- If it is set to ONLINE, then the tablespace is available as soon as it is created.
- If it is set to OFFLINE, it is not available until it is explicitly switched to ONLINE.

<a id="64edb436cd52da1e"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies the extent size of the tablespace.

- The extent size is specified in byte, and one of the fives (64 K, 128 K, 256 K, 512 K, 1 M) are selected.
- If the extent size is specified between 64 K ~ 128 K, then it is set to 128 K, and if it is specified bigger than 1 M, then it is set to 1 M.

<a id="b68773b83e49d8ff"></a>
### Description

The data tablespace is an object which provides a physical storage to store SQL schema objects such as a table, and index (LOGGING).

<a id="a9b5b5fa5a523ca1"></a>
### Examples

The following is an example of creating the disk data tablespace.

```
gSQL> CREATE DISK TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

The following is an example of creating the tablespace which consists of multiple data files.

```
gSQL> CREATE DISK TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="69ab4e4101943fab"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="517431e845cffc33"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#a9171e5695f3e4e0)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)
- [ALTER DATABASE DATAFILE AUTOEXTEND](18-sql-references-a-b.md#fbe5739ba301ebcf)

<a id="2ed5e588dcaef93e"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="15093a1024eda137"></a>
### Function

It creates a new global temporary table.

<a id="277e4ffb531254d3"></a>
### Syntax

```
<global temporary table definition> ::=
    CREATE GLOBAL TEMPORARY TABLE table_name
        ( <table element> [, ...] )
        [ <table commit action clause> ]
        [ TABLESPACE tablespace_name ]
    ;

<global temporary table definition: AS query expression> ::=
    CREATE GLOBAL TEMPORARY TABLE table_name 
        [ TABLESPACE tablespace_name ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;

<table commit action clause> ::=
    ON COMMIT { PRESERVE | DELETE } ROWS
```

> The definition of &lt;table element&gt; is as same as that of &lt;table_definition&gt;.  
> For more information, refer to [CREATE TABLE](#4c3b06d433f75b3d).

<a id="3f99cf4cd3b6d1d7"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;global temporary table definition&gt; statement.

- Table creation privilege
    - Refer to the access privilege in [CREATE TABLE](#4c3b06d433f75b3d).
- SELECT access privilege 
    - Refer to the access privilege in [SELECT](20-sql-references-h-z.md#94be89d31f330d61).

<a id="11ddf01bdcda3734"></a>
### Syntax Rules and Parameters

<a id="cfe315c8139970d0"></a>
#### table_name

It is the table name to be created.  
For more information, refer to [table_name](#0ca0ee5b6120fae6).

<a id="30cc9513274450d4"></a>
#### other syntax

For more information about other syntaxes, refer to the syntax in [CREATE TABLE](#4c3b06d433f75b3d) and in [CREATE TABLE AS SELECT](#c4998a213dbc93e2) statement.

<a id="e4743d34fadf6699"></a>
### Description

GLOBAL TEMPORARY TABLE is used to store the data which is maintained while a transaction or a session is performed.   
It is used for the purpose as same as that of the variable of which a developer temporarily stores the mid-data of the operation when developing an application.

The global temporary table has the following features.

- The definition of the global temporary table can be viewed in every session. 
- The physical segment is not allocated when defining the global temporary table, but the segment subordinated to that session is allocated when it is inserted for the first time.
- The data of the global temporary table can be viewed in a session or a transaction which was inserted.
- The tablespace to store the data of the global temporary table is determined as follows.

<a id="24c480b3a5566aeb"></a>
| Whether to specify tablespace | The tablespace in which the table is created |
| --- | --- |
| It specifies the tablespace. | It is created in the specified tablespace. |
| It does not specify the tablespace. | It is created in the default temporary tablespace of the current session user. |

- The index for the global temporary table is subordinate to the same session of the corresponding table, and the time duration is as same as that of the table. 
- It can define the view for the global temporary table.
- It can not specify &lt;table sharding strategy&gt; statement which describe the cluster-related features of the table for the global temporary table, nor &lt;table global secondary index clause&gt; statement. 
- It can not specify &lt;table attribute clause&gt; which describes the physical attributes of the table for the global temporary table, nor &lt;index attribute clause&gt; which describes the physical attributes of the index. 
- &lt;index attribute clause&gt; which describes the physical attributes of the index can not be specified for the index which is created based on the global temporary table. 
- If a transaction is terminated by &lt;table commit action clause&gt;, it can determine how to process the remaining data.

<a id="1ba7363540a99359"></a>
| Table commit action | Description |
| --- | --- |
| ON COMMIT PRESERVE ROWS | It maintains the data remained in a table even after COMMIT or ROLLBACK. |
| ON COMMIT DELETE ROWS (default) | It deletes all data remained in a table at the time of COMMIT or ROLLBACK (TRUNCATE). |

- It supports most of DDLs for an ordinary table. (Including ALTER and TRUNCATE)
    - It does not support CLUSTER-related statement (SHARD and global secondary index-related statement).
    - DDL for the global temporary table which is currently used in its own session or in another session causes an error.
    - DDL is available after removing all segments which is used as TRUNCATE TABLE or COMMIT in all sessions in use.
- It supports all DMLs and select statements for an ordinary table. 
- All alteration for the global temporary table (DML) do not leave the redo log.
- All alteration for the global temporary table (DML) leaves the undo log, the location of the undo log is determined according to TEMP_UNDO_ENABLED property.

<a id="e1cabba5166e022f"></a>
| TEMP_UNDO_ENABLED value | Description |
| --- | --- |
| TRUE | The undo log is recorded in the default temporary tablespace of the database system. |
| FALSE | The undo log is recorded in the undo tablespace of the database system. |

- TRUNCATE command for the global temporary table truncates only the segment of the corresponding session.
- If the session is terminated, all segments are TRUNCATEd and then returned.

<a id="fc437963c9b815d6"></a>
### Examples

The following is an example of performing CREATE GLOBAL TEMPORARY TABLE statement.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE1(
        COL1    CHAR(10)
       ,COL2    VARCHAR2(20)
       ,COL3    NUMBER(10)
)   ON  COMMIT  DELETE ROWS;

Table created.
```

The following is an example of performing CREATE GLOBAL TEMPORARY TABLE ... AS SELECT statement.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE2
    ON  COMMIT  PRESERVE ROWS
    AS  SELECT  *
          FROM  EMPLOYEES;

Table created.
```

<a id="d974c10d7842e701"></a>
### Compatibility

CREATE GLOBAL TEMPORARY TABLE and CREATE GLOBAL TEMPORARY TABLE AS SELECT statements follow the definition of SQL standard &lt;table definition&gt;. However, the following is an extension of SQL standard.

- SQL standard requires parentheses outside SELECT clause, but it is optional in GOLDILOCKS.
- SQL standard requires WITH [NO] DATA clause, but it is optional in GOLDILOCKS.
- The concepts of tablespace in GOLDILOCKS is an extended concept, and it is not supported in SQL standard.

**SQL standard compatibility**

<a id="a974003f76e7a0f5"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T171 | LIKE clause in table definition | X |
| T172 | AS subquery clause in table definition | O |
| F531 | Temporary tables | X |
| S051 | Create table of type | X |
| S043 | Enhanced reference types | X |
| S081 | Subtables | X |
| T173 | Extended LIKE clause in table definition | X |
| T180 | System-versioned tables | X |
| F692 | Extended collation support | X |
| T174 | Identity columns | O |
| T175 | Generated columns | X |
| S071 | SQL paths in function and type name resolution | X |
| F321 | User authorization | O |
| T322 | Extended roles | X |
| F762 | CURRENT_CATALOG | O |
| F763 | CURRENT_SCHEMA | O |

<a id="4d9ce51e22e0d015"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#4c3b06d433f75b3d)
- [CREATE TABLE AS SELECT](#c4998a213dbc93e2)

<a id="22283cabebb44fe8"></a>
## CREATE IMMUTABLE TABLE

<a id="93a498230507f258"></a>
### Function

It creates a new immutable table.

<a id="a9eada5bd76b4b4c"></a>
### Syntax

```
<immutable table definition> ::=
    CREATE IMMUTABLE TABLE table_name
        ( <table element> [, ...] )
        [ <table sharding strategy> ]
        [ <table attribute clause> [...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
    ;

<immutable table definition: AS query expression> ::=
    CREATE IMMUTABLE TABLE table_name
        [ ( column_name [, ...] ) ]
        [ <table sharding strategy> ]
        [ <table attribute clause> [, ...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;
```

> The definition for &lt;table element&gt;, &lt;table sharding strategy&gt;, &lt;table attribute clause&gt; and &lt;table global secondary index clause&gt; are as same as those in &lt;table_definition&gt;. For more information, refer to [CREATE TABLE](#4c3b06d433f75b3d).

<a id="5c906f1438740c46"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;immutable table definition&gt;.

- The privilege to create the table 
    - Refer to the access rules for [CREATE TABLE](#4c3b06d433f75b3d) statement.
- The privilege for SELECT to access 
    - Refer to the access rules for [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement.

<a id="743384d211a83e69"></a>
### Syntax Rules and Parameters

<a id="300c0a408ef7d551"></a>
#### table_name

It is the table name to be created and it should be unique in the schema.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the table name should be shorter than 128 bytes.

<a id="ad7ff21060c1f2a1"></a>
#### Other Syntax

For other syntaxes, refer to the syntaxes for [CREATE TABLE](#4c3b06d433f75b3d) and [CREATE TABLE AS SELECT](#c4998a213dbc93e2).

<a id="96bbb21e51968a2b"></a>
### Description

An immutable table is used when it is required to prevent the record stored in the table from being altered or deleted and to prevent the table from being dropped.

> An immutable table can be dropped when a user, a schema, a tablespace and a cluster group are dropped.

> The following SQL statements are not allowed for an immutable table.
> 
> - UPDATE
> - DELETE
> - ALTER TABLE RENAME/DROP COLUMN
> - ALTER TABLE SET UNUSED COLUMN
> - ALTER TABLE DROP UNUSED COLUMNS
> - ALTER TABLE RENAME TO
> - TRUNCATE TABLE
> - DROP TABLE
> 
>   
> The following SQL statements are allowed for an immutable table.
> 
> - INSERT
> - SELECT
> - SELECT .. FOR UPDATE
> - CREATE/ALTER/DROP INDEX
> - ALTER TABLE ADD/ALTER COLUMN
> - ALTER TABLE ADD/ALTER/RENAME/DROP CONSTRAINT
> - ALTER TABLE for physical property changes
> - ALTER TABLE ADD/DROP SUPPLEMENTAL LOG
> - LOCK TABLE
> - ALTER TABLE .. ADD/ALTER/DROP GLOBAL SECONDARY INDEX
> - ALTER DATABASE MOVE SHARD
> - ALTER TABLE .. MOVE SHARD
> - ALTER TABLE .. SPLIT SHARD
> - ALTER TABLE .. MERGE SHARD
> - DROP TABLESPACE
> - DROP SCHEMA
> - DROP USER
> - DROP CLUSTER GROUP
> 

<a id="b6f2f913c44aed46"></a>
### Examples

The following is an example of executing CREATE IMMUTABLE TABLE statement.

```
gSQL> CREATE IMMUTABLE TABLE t1
(
    id INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

The following is an example of executing CREATE IMMUTABLE TABLE ... AS SELECT statement.

```
gSQL> CREATE IMMUTABLE TABLE T2
       AS SELECT *
             FROM T1;

Table created.
```

<a id="ea09bfad12b49278"></a>
### Compatibility

The SQL standard does not cover CREATE IMMUTABLE TABLE and CREATE IMMUTABLE TABLE AS SELECT statements.

<a id="57c792886a48d621"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#4c3b06d433f75b3d)
- [CREATE TABLE AS SELECT](#c4998a213dbc93e2)

<a id="d54e994b20c1da1b"></a>
## CREATE INDEX

<a id="914f05196f851845"></a>
### Function

It creates an index.

<a id="4ab2ed951fa07cf8"></a>
### Syntax

```
<index definition> ::=
    CREATE [ UNIQUE ] INDEX index_name
        ON table_name ( <index column element> [, ...] )
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
    ;

<index column element> ::=
    column_name [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]

<index attributes> ::=
      <physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )
    | <parallel clause> 

<physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="b0bd56127070310e"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;index definition&gt;.

- One of the following privileges is required to create an index on the table.
    - (INDEX or CONTROL TABLE ON) TABLE for that table
    - CONTROL SCHEMA ON SCHEMA for the schema to which the table belongs
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the schema on which the index is to be created.
    - (CREATE INDEX or CONTROL SCHEMA) ON SCHEMA for the schema
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the tablespace on which the index is to be created.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- The owner of the index is determined as follows.
    - The owner of the schema to which the index belongs. 
    - If the schema to which the index belongs is PUBLIC, then it is the user who executed the statement.

> Unique indexes in a cluster system should include all sharding keys.

<a id="aa3e734891fa2136"></a>
### Syntax Rules and Parameters

<a id="aa4f88325fb132ab"></a>
#### UNIQUE

It does not allow duplicate values for the columns of the index.

<a id="b2fc53459174f030"></a>
#### index_name

It is the index name to be created and it should be a unique name within the schema.  
If the schema name is omitted, the index is created in the schema to which the referring table belongs.  
The length of the index name should be shorter than 128 bytes.

<a id="40ac1f4e69261210"></a>
#### table_name

It is the table name which creates the index.  
The schema to which a table belongs, such as schema_name.table_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="2e7e6adcc7ef583c"></a>
#### column_name

It is the column name to be used as an index key.  
One or more columns should be defined, and maximum 32 columns can be used as an index key.

The following constraints can occur depending on the implementation.

- If the column data type included in an index is LONG CHARACTER VARYING, LONG BINARY VARYING, an index can not be created.
- An index is created only when the sum of the column precisions is less than 1200 bytes.

<a id="a58260574e35b677"></a>
#### ASC | DESC

It specifies the sort order of a column.

- ASC: It is sorted in ascending order.
- DESC: It is sorted in descending order.
- If not specified, the default value is ASC.

<a id="220c82f9394bc8ac"></a>
#### NULLS FIRST | NULLS LAST

It specifies the sort order of the NULL value.

- NULLS FIRST: It precedes the non-NULL values.
- NULLS LAST: It is behind the non-NULL values.
- If not specified, the default value is NULLS LAST.

<a id="1c557733960895c5"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute of the index.

- PCTFREE integer 
    - Definition 
        - It is the reserved space for adjusting the page split frequency caused by the key inserted in the page.
        - It applies only to the index bottom-up build.
    - It can use the value from 0 to 99.
    - If it is omitted, the default value is the value set in DEFAULT_INDEX_PCTFREE property.

- INITRANS integer 
    - Definition 
        - It specifies the initial number of transactions which can simultaneously access the page. 
        - If the number of users who access the index is small, INITRANS is set to low, and if the number of users who simultaneously access the index is big, INITRANS is set to high. 
        - If necessary, it is automatically increased to the specified MAXTRANS. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions which can simultaneously access the page. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 8.

<a id="9a0becc1dbca2380"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of physical storage space which is initially allocated when creating the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually operated as 8192 bytes.)
        - The size (aligned to the EXTENT size of TABLESPACE) should be equal to or bigger than MINEXTENTS, or it should be equal to or less than MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is omitted, the default value is one EXTENT size of TABLESPACE to which the table belongs.

- NEXT integer
    - Definition
        - It specifies the physical space size to be allocated when adding the space to the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually operated as 8192 bytes.)
        - NEXT operates as follows, depending on the remaining space size of the index available currently. (Obtained by subtracting the amount of currently used space from the MAXEXTENTS size)  
      - If the remaining space size is 0, then it can not extend the space.  
      - If the remaining space size is bigger than 0, but smaller than NEXT, then it allocates the  
      space as big as the remaining space.  
      - If the remaining space size is bigger than NEXT, then it allocates the space as big as the NEXT.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is omitted, the default value is one EXTENT size of TABLESPACE to which the index belongs.

- MINSIZE integer
    - Definition
        - It is the minimum space size of the index.
        - The value should be equal to or smaller than MAXSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it is specified to the size of two EXTENT.
    - If it is omitted, the default value is the size of two EXTENT.

- MAXSIZE integer
    - Definition
        - It is the maximum space size of the index.
        - The value should be equal to or bigger than MINSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is omitted, the default value is EXTENT size * 2147483647 (The maximum positive integer of INT32).

<a id="b94d78c8c4bc04cf"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If the unit is omitted, the default value is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ff96f839880cdae1"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used when building an index.

- NOPARALLEL 
    - It does not build an index in parallel.
- PARALLEL [integer] 
    - It builds an index in parallel.
    - If an integer is omitted or set as 0, then it follows INDEX_BUILD_PARALLEL_FACTOR property. 
    - The minimum value of an integer is 0 and the maximum value is 16. 
    - If the property value is 0, then the system determines the optimal value.
- If it is omitted, the default value is PARALLEL.

<a id="a08e1b760546af22"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be stored.

- When it specifies tablespace_name
    - if tablespace_name is data tablespace, then a LOGGING index is created.
    - if tablespace_name is temporary tablespace or nologging tablespace, then a NOLOGGING index is created.

- When it omits TABLESPACE clause
    - If INDEX TABLESPACE tablespace_name of USER is specified
        - The defined tablespace is used.
    - If INDEX TABLESPACE of USER is NULL
        - The index of the DISK table uses the user's default data tablespace.
        - The index of the MEMORY table uses the user's default temporary tablespace.

<a id="4de99dd831a733e5"></a>
### Description

LOGGING index and NOLOGGING index have the following trade-offs.

- LOGGING index
    - Advantage: It does not separately build an index because the index is automatically restored by using the log when starting up the system.
    - Disadvantage: A disk I/O occurs because the changes on the index are recorded on the log when altering the row.
- NOLOGGING index
    - Advantage: A disk I/O does not occur for the changes on the index when altering the row.
    - Disadvantage: It automatically rebuilds the index when starting up the system because the log information of the index does not exist.

<a id="af3e1166d9a27ce0"></a>
### Examples

The following is an example of creating the unique index.

```
gSQL> CREATE UNIQUE INDEX idx_t1_id ON t1( id );

Index created.
```

The following is an example of creating an index for multiple columns.

```
gSQL> CREATE INDEX idx_t1_id_name ON t1( id, name );

Index created.
```

The following is an example of specifying the sort order of the index column.

```
gSQL> CREATE INDEX idx_t1_dept_id ON t1( dept_id DESC );

Index created.
```

The following is an example of specifying the sort order of NULL value of the index column.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name NULLS FIRST );

Index created.
```

The following is an example of setting information about the space in which index is stored.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id )
             STORAGE ( INITIAL 10M NEXT 1M MINSIZE 10M MAXSIZE 100M );

Index created.
```

The following is an example of creating the redo logging for the index.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id );

Index created.
```

The following is an example of creating the index with parallel option.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) PARALLEL;

Index created.
```

The following is an example of specifying the tablespace when creating an index.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) TABLESPACE mem_temp_tbs;

Index created.
```

<a id="dde42f6bbd80e199"></a>
### Compatibility

The SQL standard does not cover the concepts of the index.

<a id="9d564d9afc6372be"></a>
### For more information

Refer to [DROP INDEX](#fcb6f064d90f791d).

<a id="9831f431f182fce6"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="022e9378bd86adc6"></a>
### Function

It defines a memory data tablespace.

<a id="10a5776133bad857"></a>
### Syntax

```
<memory data tablespace statement> ::=
    CREATE [ MEMORY ] [ DATA ] TABLESPACE tablespace_name
        DATAFILE <memory datafile clause> [, ...]
        [ <data tablespace management clause> [, ...] ]

<memory datafile clause> ::=
     'filename' 
        [ SIZE <size clause> | REUSE | SIZE <size clause> REUSE ]
        [ AT <domain_name> ]
<size clause> ::=
    integer [ K | M | G | T ]

<data tablespace management clause> ::=
      { ONLINE | OFFLINE }
    | EXTSIZE <size clause>
```

<a id="a75202c8b50abe23"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;memory data tablespace definition&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="f98885659db8a741"></a>
### Syntax Rules and Parameters

<a id="fb9c135c56c7770d"></a>
#### [ MEMORY ] [ DATA ]

It is a memory tablespace to store the permanent objects such as tables, indexes, etc.  
The reserved words, MEMORY and DATA, can be omitted.

<a id="0e74bbe4ca80d4ce"></a>
#### tablespace_name

It is the tablespace name to be created.  
The length of the tablespace name should be shorter than 128 bytes.

<a id="3fd24d3cf6a720b0"></a>
#### &lt;memory datafile clause&gt;

- 'filename' 
    - It is the file name to store and manage the data.
    - It is the space to store the checkpoint image for the memory data. 
    - filename can be either a new file or an already existing file.
    - The length of the filename should be shorter than 1024 bytes.

- SIZE &lt;size clause&gt; 
    - The initial size is assigned for a new file by using the SIZE clause.
    - An error occurs if the file already exists.
    - The file size can be specified between minimum 1M and maximum 30G.

- REUSE 
    - If the file already exists, REUSE clause is used. 
    - If the file does not exist, a new file is created. 
    - The newly created file size is 
        - determined by USER_DATA_TABLESPACE_SIZE property in case of the data tablespace.
        - determined by USER_TEMP_TABLESPACE_SIZE property in case of the temporary tablespace.

- SIZE &lt;size clause&gt; REUSE 
    - If both SIZE clause and REUSE clause are specified, it is operated as follows according to the presence of the filename.
        - For the new filename, the initial file size is assigned by using the SIZE clause.
        - For the existing filename, the size is adjusted to the value of SIZE clause by using the existing file.

<a id="188e6902b51a6094"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="d663eabd2836834e"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="f5ad410b6ab73deb"></a>
#### ONLINE | OFFLINE

It sets ONLINE or OFFLINE of the tablespace.

- ONLINE is the state which a tablespace can be used as soon as it is created.
- OFFLINE is the state which a tablespace is unable to be used, it can be used after switching to ONLINE state.

<a id="f69497281eb6d692"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies extent size of the tablespace.

- The extent size is specified in bytes, and one of the five (64K, 128K, 256K, 512K, 1M) is selected.
- If the extent size is defined as a value between 64K ~ 128K, 128K is set. If the extent size is defined as 1M or bigger, 1M is set.

<a id="5a937c9b9407cc47"></a>
### Description

The data tablespace is an object which provides the physical space to store the SQL schema object such as a table, an index (LOGGING).

<a id="eb09e348934339b0"></a>
### Examples

The following is an example of creating a memory data tablespace.

```
gSQL> CREATE TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

The following is an example of creating a tablespace which consists of multiple data files.

```
gSQL> CREATE TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="ecde4700410cd2e6"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="26d7a0e2f87621cf"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#a9171e5695f3e4e0)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)

<a id="504552ef753c144a"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="033cc25d7e368255"></a>
### Function

It defines a memory temporary tablespace.

<a id="1ae118d2468b907b"></a>
### Syntax

```
<memory temporary tablespace statement> ::=
    CREATE [ MEMORY ] TEMPORARY TABLESPACE tablespace_name
        MEMORY <memory clause> [, ...]
        <temporary tablespace management clause>

<memory clause> 
     'memory_name' { SIZE <size clause> } [ AT <domain_name> ]

<temporary tablespace management clause> ::=
    EXTSIZE <size clause>
```

<a id="839c876f1913eb32"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;memory temporary tablespace definition&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace.
- USAGE TABLESPACE ON DATABASE

<a id="8be0558adb89e19b"></a>
### Syntax Rules and Parameters

<a id="7dc7be5d18bd7b1f"></a>
#### [ MEMORY ] TEMPORARY

It is a memory temporary tablespace to store the no logging indexes or the temporary objects such as intermediate results which are generated during the query processing.  
The reserved word, MEMORY, can be omitted.

<a id="f01411c04b60353c"></a>
#### tablespace_name

It is the tablespace name to be created.  
The length of the tablespace name should be shorter than 128 bytes.

<a id="19e55aea320f5684"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - It is a memory name to store the temporary data.
    - memory_name should be guaranteed to be unique within the tablespace.
    - The length of the memory_name should be shorter than 1024 bytes.
- SIZE &lt;size clause&gt; 
    - It specifies the initial size.
    - It can be specified between minimum 1M and maximum 30G.

<a id="3d223b2e397ee4f0"></a>
#### &lt;size clause&gt;

It specifies the size of shared memory space in bytes.(If it is omitted, the default unit is bytes.)  
The image is not managed as a file in case of the temporary memory data.

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="75c869d4b85faec4"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="d1dc2fb4e41b3747"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies extent size of the tablespace.

- The extent size is specified in bytes, and one of the five (64K, 128K, 256K, 512K, 1M) is selected.
- If the extent size is defined as a value between 64K ~ 128K, 128K is set. If the extent size is defined as 1M or bigger, 1M is set.

<a id="11ff8ff71a2c434b"></a>
### Description

The temporary tablespace is an object which provides the physical space to store the SQL schema object such as an index (NOLOGGING), and to store the intermediate results for sorting, hashing during the query processing.

<a id="fa12a649c711777c"></a>
### Examples

The following is an example of creating a temporary tablespace.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 MEMORY 'test_memory_1' SIZE 10M;

Tablespace created.
```

The following is an example of creating a temporary tablespace which includes multiple memory spaces.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 
             MEMORY 'test_memory_3_1' SIZE 10M,
                    'test_memory_3_2' SIZE 10M;

Tablespace created.
```

<a id="19fc7cceaefd85f1"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="23cdcef7de306863"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#a9171e5695f3e4e0)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)

<a id="fa2854762beb7024"></a>
## CREATE PROFILE

<a id="ffe659a21187e7f1"></a>
### Function

It is the statement which creates the profile, and it sets the password management method.   
When a profile is allocated to a user, the user's password is managed in the way defined in the profile.

<a id="0a55843d1aae20c0"></a>
### Syntax

```
<profile definition> ::=

    CREATE PROFILE profile_name LIMIT 
    { <password_parameters>, ...}
    ; 

<password parameters> ::= 
      FAILED_LOGIN_ATTEMPTS { integer | UNLIMITED | DEFAULT }
    | PASSWORD_LOCK_TIME  { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_LIFE_TIME  { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_GRACE_TIME { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_REUSE_MAX  { integer | UNLIMITED | DEFAULT }
    | PASSWORD_REUSE_TIME { password_parameter_number_interval | UNLIMITED | DEFAULT }
    | PASSWORD_VERIFY_FUNCTION { <verify_policy> | NULL | DEFAULT }

<verify_policy> ::= 
      KISA_VERIFY_FUNCTION
    | ORA12C_VERIFY_FUNCTION
    | ORA12C_STRONG_VERIFY_FUNCTION
    | VERIFY_FUNCTION_11G 
    | VERIFY_FUNCTION

<password_parameter_number_interval> ::=
   integer 
 | integer / integer
```

<a id="36a7fa150144c1e2"></a>
### Invocation and Access Rules

CREATE PROFILE ON DATABASE privilege is required to perform &lt;profile definition&gt;.

<a id="71439df7227a9ac2"></a>
### Syntax Rules and Parameters

<a id="b063942e9957da79"></a>
#### profile_name

It specifies the profile name to be created.

<a id="ffcffffa5aa058b0"></a>
#### password_parameters

It sets the parameters for password management.

- The following parameters are to be set. 
    - FAILED_LOGIN_ATTEMPTS
    - PASSWORD_LOCK_TIME
    - PASSWORD_LIFE_TIME
    - PASSWORD_GRACE_TIME
    - PASSWORD_REUSE_MAX
    - PASSWORD_REUSE_TIME
    - PASSWORD_VERIFY_FUNCTION

The omitted parameters follow the "DEFAULT" profile policy.

<a id="c149725e50c87916"></a>
#### FAILED_LOGIN_ATTEMPTS

It sets the number of consecutive login attempts allowed to fail.  
If the failed attempts exceed the specified number, the account is locked.

- FAILED_LOGIN_ATTEMPTS integer
    - The value range should be a positive integer bigger than 0.
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - Account lockout which is due to a login failure does not occur.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="c3e9778c4167bf5b"></a>
#### PASSWORD_LOCK_TIME

It sets the period (days) which the account is locked after consecutive login failure.

- PASSWORD_LOCK_TIME constant_expression
    - It is the lock duration (day).
    - The default unit is a day.
    - Hours(n/24), minutes (n/1440), seconds (n/86400) can be specified for testing.
    - The value range is from one second (1/86400) to 100,000 days.
- PASSWORD_LOCK_TIME UNLIMITED
    - If an account lockout occurs, the lock is not release until performing ALTER USER user_name ACCOUNT UNLOCK statement.
- PASSWORD_LOCK_TIME DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="ea8fa340b8180fc1"></a>
#### PASSWORD_LIFE_TIME

It sets the life time of the password (day).

- PASSWORD_LIFE_TIME constant_expression 
    - It is the life time of the password (day).
    - The default unit is a day.
    - Hours(n/24), minutes (n/1440), seconds (n/86400) can be specified for testing.
    - The value range is from one second (1/86400) to 100,000 days.
- PASSWORD_LIFE_TIME UNLIMITED 
    - The password does not have the expiration date.
- PASSWORD_LIFE_TIME DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="5622c48474cc4a9c"></a>
#### PASSWORD_GRACE_TIME

It sets the grace period of password expiration when logging in after PASSWORD_LIFE_TIME.

- PASSWORD_GRACE_TIME constant_expression 
    - The grace period for password expiration (day)
    - The default unit is a day.
    - Hours (n/24), minutes (n/1440), seconds (n/86400) can be specified for testing.
    - The value range is from one second (1/86400) to 100,000 days.
- PASSWORD_GRACE_TIME UNLIMITED 
    - It continues to defer the password expiration. 
- PASSWORD_GRACE_TIME DEFAULT 
    - It follows the "DEFAULT" profile policy.

PASSWORD_GRACE_TIME starts at first login trial after the password life time. If the password is not altered during the grace period, the password expires.

<a id="7255a09299224b0f"></a>
#### PASSWORD_REUSE_MAX

It sets the number of the recent passwords which can not be reused when the user wants to reuse the old password.

PASSWORD_REUSE_MAX should be used together with PASSWORD_REUSE_TIME.

- PASSWORD_REUSE_MAX integer
    - The value range should be a positive integer bigger than 0.
- PASSWORD_REUSE_MAX UNLIMITED
    - If PASSWORD_REUSE_TIME is UNLIMITED, all old passwords can be reused.
    - If PASSWORD_REUSE_TIME is not UNLIMITED, any old password can not be reused.
- PASSWORD_REUSE_MAX DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="852635fd7c327b09"></a>
#### PASSWORD_REUSE_TIME

It sets the duration which the password can not be reused when the user wants to reuse the old password.

PASSWORD_REUSE_TIME should be used together with PASSWORD_REUSE_MAX.

- PASSWORD_REUSE_TIME constant_expression 
    - It is the duration which the password can not be reused. (day)
    - The default unit is a day.
    - Hours(n/24), minutes (n/1440), seconds (n/86400) can be specified for testing.
    - The value range is from one second (1/86400) to 100,000 days.
- PASSWORD_REUSE_TIME UNLIMITED
    - If PASSWORD_REUSE_MAX is UNLIMITED, all old passwords can be reused.
    - If PASSWORD_REUSE_MAX is not UNLIMITED, any old password can not be reused.
- PASSWORD_REUSE_TIME DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="dab17d2684a093f9"></a>
#### PASSWORD_VERIFY_FUNCTION

It sets the password complexity verification methods.

- PASSWORD_VERIFY_FUNCTION null
    - The password complexity verification is not performed.
- PASSWORD_VERIFY_FUNCTION DEFAULT
    - It follows the "DEFAULT" profile policy.
- PASSWORD_VERIFY_FUNCTION &lt;verify policy&gt;
    - The password complexity verification methods can be specified as follows.
        - KISA_VERIFY_FUNCTION
        - ORA12C_VERIFY_FUNCTION
        - ORA12C_STRONG_VERIFY_FUNCTION
        - VERIFY_FUNCTION_11G 
        - VERIFY_FUNCTION

<a id="18c13e98e322c7b4"></a>
##### KISA_VERIFY_FUNCTION

It is the password verification method of KISA (Korea Internet & Security Agency).

- 8 or more letters
- One or more characters
- One or more numbers
- One or more special characters

<a id="e7ee40729e7380c8"></a>
##### ORA12C_VERIFY_FUNCTION

It is the password verification method of Oracle, ORA12C_VERIFY_FUNCTION.

- 8 or more letters
- 1 or more characters
- 1 or more numbers
- The database name should not be included. 
- The username or the reversed username should not be included. 
- *goldilocks* should not be included. 
- *oracle* should not be included. 
- The following simple passwords are not allowed. 
    - welcome1, database1, account1, user1234, password1, oracle123, computer1, abcdefg1, change_on_intall 
- At least 3 characters of the new password should be different from the old password.

<a id="d6d4917a97692e60"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

It is the password verification method of Oracle, ORA12C_STRONG_VERIFY_FUNCTION.

- 9 or more letters
- 2 or more uppercases 
- 2 or more lowercases
- 2 or more numbers
- 2 or more special characters
- At least 4 characters of the new password should be different from the old password.

<a id="c3c0be39e91759b3"></a>
##### VERIFY_FUNCTION_11G

It is the password verification method of Oracle, VERIFY_FUNCTION_11G.

- 8 or more letters
- 1 or more characters 
- 1 or more numbers 
- The username should not be included. 
- At least 3 characters of the new password should be different from the old password.

<a id="80e4ecf4977f6711"></a>
##### VERIFY_FUNCTION

It is the password verification method of Oracle, VERIFY_FUNCTION.

- It should not be as same as the username.
- 4 or more letters 
- 1 or more characters
- 1 or more numbers 
- 1 or more special characters 
- The following simple passwords are not allowed. 
    - welcome, database, account, user, password, oracle, computer, abcd
- At least 3 characters of the new password should be different from the old password.

<a id="5294781e8533fcd5"></a>
### Description

<a id="b8a143ae640bb26f"></a>
#### Account Lockout

The followings are the parameters affecting the account lockout.

- FAILED_LOGIN_ATTEMPTS
- PASSWORD_LOCK_TIME

For example, when a user and a profile are created as follows.

```
CREATE PROFILE prof LIMIT
    FAILED_LOGIN_ATTEMPTS 4
    PASSWORD_LOCK_TIME 30;

ALTER USER u1 PROFILE prof;
```

If the user u1 fails to log in more than four times, the account is locked for 30 days. Then the account lockout is released after 30 days.

If PASSWORD_LOCK_TIME is UNLIMITED, the account lockout should be explicitly released by using ALTER USER statement.

```
ALTER USER user1 ACCOUNT UNLOCK;
```

<a id="87651164b71a7b8b"></a>
#### Password Expiration

The followings are the parameters affecting the password expiration.

- PASSWORD_LIFE_TIME
- PASSWORD_GRACE_TIME

The password is expired in the following order.

1. The password is set.
** The time of the password expiration is set to the time elapsed as much as PASSWORD_LIFE_TIME since when a password is altered.
** The password expiration status is OPEN, and it allows a normal login.

2. When a user logs in after the password expiration 
** The login succeeds but the password expiration status becomes EXPIRED (GRACE) and the following warnings occur.
*** ERR-28000(16310): The password will expire in n days
*** ERR-28000(16311): The password will expire soon
*** The SQL standard does not cover the concepts of password expiration.
*** 28000 is the authentication warning or SQL standard status code of an error. 16310, 16311 are the GOLDILOCKS error code.
** The time of the password expiration is reset to the time elapsed as much as PASSWORD_GRACE_TIME since when a user logged in.

3. When a user logs in after the grace time
** The password expiration status becomes EXPIRED, the user can not log in, and the following error occurs.
*** ERR-28000(16312): The password has expired
*** The SQL standard does not cover the concepts of password expiration.
*** 28000 is the authentication warning or SQL standard status code of an error. 16312 is the GOLDILOCKS error code.
*** GOLDILOCKS internal error code of 16312 should be used to control password reentering using program.

**Password expiration status transition**

<a id="6799d6d091375661"></a>
| Step | Point of time | login | Status |
| --- | --- | --- | --- |
| 1 | The password is changed. | Success | OPEN |
| 2 | PASSWORD_LIFE_TIME is elapsed. | Success with warning | EXPIRED(GRACE) |
| 3 | PASSWORD_GRACE_TIME is elapsed. | Error | EXPIRED |

The following is another example.

```
CREATE PROFILE prof LIMIT
   PASSWORD_LIFE_TIME 90
   PASSWORD_GRACE_TIME 3;

ALTER USER u1 PROFILE prof;
```

The example above describes that the user u1 succeeds in login after 90 days of password expiration. However, the user receives a warning that the password expires in three days.

If the password is not changed within three days, the password expires.  
Once the password expires, it reminds that the new password should be entered when logging in, and the account access is denied.

<a id="f438b114f3d86f79"></a>
#### Password Reusability

The followings are the parameters affecting the password reusability.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

The password reusability of the two parameters above is determined according to the following table.

**Conditions for the password reusability**

<a id="21cab2d8dfca9681"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | Reusable condition |
| --- | --- | --- |
| value | value | It can be reused when both conditions of PASSWORD_REUSE_TIME and PASSWORD_REUSE_MAX are satisfied. |
| value | UNLIMITED | It can not be reused. |
| UNLIMITED | value | It can not be reused. |
| UNLIMITED | UNLIMITED | It can always be reused. |

If a profile is created as follows,

```
CREATE PROFILE prof LIMIT
   PASSWORD_REUSE_MAX 5
   PASSWORD_REUSE_TIME 3;
```

the password can not be reused if it is the five recent passwords or the password changed within three days.

The following is an example of the user u1's password change history. If the current password is P # _000007 and the current date is 2015-08-08, the reusability of existing passwords is as follows.

**Examples of password reusability**

<a id="ce82d3687707d25f"></a>
| Password | Password_date | Password reusability |
| --- | --- | --- |
| P#_000001 | 2015-08-01 | It can be reused. |
| P#_000002 | 2015-08-02 | It can be reused. |
| P#_000003 | 2015-08-03 | It violates REUSE_MAX. |
| P#_000004 | 2015-08-04 | It violates REUSE_MAX. |
| P#_000005 | 2015-08-05 | It violates REUSE_MAX, REUSE_TIME. |
| P#_000006 | 2015-08-06 | It violates REUSE_MAX, REUSE_TIME. |
| P#_000007 | 2015-08-07 | It violates REUSE_MAX, REUSE_TIME. |

The password change history accumulated for checking the password reusability can be deleted by using the following statement.

```
ALTER DATABASE CLEAR PASSWORD HISTORY;
```

<a id="483ea63b5041020d"></a>
#### DEFAULT profile

When creating the database, the following "DEFAULT" profile is automatically created. The password parameters of the "DEFAULT" profile are as follows.

**Configuration of DEFAULT profile**

<a id="2afb960d82cd210a"></a>
| Parameter | Value |
| --- | --- |
| FAILED_LOGIN_ATTEMPTS | 10 |
| PASSWORD_LOCK_TIME | 1 |
| PASSWORD_LIFE_TIME | 180 |
| PASSWORD_GRACE_TIME | 7 |
| PASSWORD_REUSE_MAX | UNLIMITED |
| PASSWORD_REUSE_TIME | UNLIMITED |
| PASSWORD_VERIFY_FUNCTION | NULL |

The default values of "DEFAULT" profile have the following characteristics.

- Account lockout
    - The account is locked for one day (PASSWORD_LOCK_TIME) after ten consecutive login failure (FAILED_LOGIN_ATTEMPTS).
- Password expiration
    - The password expires after the grace period of seven days (PASSWORD_GRACE_TIME) after 180 days (PASSWORD_LIFE_TIME) are exceeded. 
- Password reusability
    - The old password can be reused. 
- Password complexity verification
    - It is not performed.

DEFAULT profile can not be dropped but it can be altered as follows.

```
ALTER PROFILE DEFAULT LIMIT ...
```

<a id="d9b23765238262bd"></a>
### Examples

The following is an example of creating the profile to control the account lockout. The account is locked for three days after three consecutive login failures.

```
gSQL> CREATE PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating the profile to control the password expiration. The life time of the password is 90 days, and the grace time of the password is seven days.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating the profile to control whether the password is reusable. The following example does not verify the old password when changing the password.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating the profile to control the password complexity check.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating the profile by setting all parameter.

```
gSQL> CREATE PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile created.

gSQL> COMMIT;

Commit complete.
```

<a id="036a88687a234864"></a>
### Compatibility

The SQL standard does not cover the concepts of the profile.

<a id="efd0adf8708c2263"></a>
### For More Information

Refer to the followings.

- [DROP PROFILE](#235532c683a06591)
- [ALTER PROFILE](18-sql-references-a-b.md#328cee336239afe4)
- [CREATE USER](#67d566d84adb0376)
- [ALTER USER](18-sql-references-a-b.md#270d91f0c78160b6)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](18-sql-references-a-b.md#45533ba352d57e4b)

<a id="f7ea7ef79efa639b"></a>
## CREATE SCHEMA

<a id="2c041c9b5c50a63a"></a>
### Function

It defines the schema.

<a id="ce4e5afdb0acecc0"></a>
### Syntax

```
<schema definition> ::=
    CREATE SCHEMA <schema name clause>
        [ <schema element> [...] ]
    ;

<schema name clause> ::=
      schema_name
    | AUTHORIZATION user_identifier
    | schema_name AUTHORIZATION user_identifier

<schema element> ::=
      <table definition>
    | <view definition>
    | <index definition>
    | <sequence generator definition>
    | <grant privilege statement>
    | <comment statement>
```

<a id="56763a1944ca9de4"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;schema definition&gt;.

- CREATE SCHEMA ON DATABASE privilege is required to create the schema.

- If &lt;schema element&gt; exists, the privilege to perform each &lt;schema element&gt; is required.  
  For more information about the access privilege, refer to *invocation and access rules* in the following statements.
    - [CREATE TABLE](#4c3b06d433f75b3d)
    - [CREATE VIEW](#b82ddec42cccf582)
    - [CREATE INDEX](#d54e994b20c1da1b)
    - [CREATE SEQUENCE](#11cfe1f314df4ce6)
    - [GRANT privileges TO](#c7985df8e45cc984)
    - [COMMENT ON name IS](#ab6593b2744b2d0f)

- The user who is user_identifier has the following privileges for the created schema.
    - The owner of the created schema, which is schema_name
    - The owner of the object which is created by &lt;schema element&gt; clause

- An appropriate privilege for the schema is required to create an object because a separate privilege on the created schema is not granted.  
  For more information about schema privilege types, refer to [&lt;schema privilege&gt;](#53309e4011b33e74) of GRANT privileges TO statement.  
  For more information about usage example, refer to [Examples](#322aee49fff9fbe6) of CREATE USER statement.

<a id="6dbaffc7e7752f19"></a>
### Syntax Rules and Parameters

<a id="8e3a2b51d517627e"></a>
#### schema_name

It is the schema name to be created.  
An identical schema name should not exist in the database.  
The length of the schema name should be shorter than 128 bytes.

<a id="9c4196ea072e4fb9"></a>
#### AUTHORIZATION user_identifier

If the schema name is omitted, a schema with the same name as the user_identifier is created.  
If the AUTHORIZATION is not specified, the user_identifier of the user performing the statement is used.

<a id="da8ee8dd214215e3"></a>
#### schema_name AUTHORIZATION user_identifier

It specifies the schema name and schema owner to be created.  
The owner can not be a role or PUBLIC.

<a id="63a59cd2c37ea67e"></a>
#### &lt;schema element&gt;

It defines the objects to be created in the schema along with the schema creation.  
The schema_element is executed in the listed order, and they are separated by a white space without a comma (,).   
The object can not be defined in a schema which has different name from the schema to be created.

- The &lt;grant privilege statement&gt; can be specified only for the following privileges.
    - &lt;schema privilege&gt;
    - &lt;table privilege&gt;
    - &lt;sequence privilege&gt;

- The &lt;comment statement&gt; can be specified only for the following objects.
    - SCHEMA schema_name
    - TABLE [schema_name].table_name
    - COLUMN [schema_name].table_name.column_name
    - INDEX [schema_name].index_name
    - SEQUENCE [schema_name].sequence_name
    - CONSTRAINT [schema_name].constraint_name

<a id="4467e0f8cc3b8a3a"></a>
### Description

A schema is an object which logically classifies SQL schema objects such as table, view, index, sequence and constraint.

In GOLDILOCKS, the relationship between the user and the schema is 1 : N. In other words, the schema owned by a user may not exist, or the user may own multiple schemas.

The SQL standard does not explicitly define the relationship of the non-schema objects such as user, schema, database, but each DBMS defines the relationship between the non-schema objects as a different concept. Refer to the following note.

> The relationship between user and schema in other DBMS   
> 
> 
> - Oracle
>     - User : schema = 1 : 1 
> 
> 
> 
> - DB2 
>     - User : schema = 1 : N 
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1 
>     - User is a subordinate object of a database (schema).
> 

<a id="e597e498ad301689"></a>
### Examples

The following is an example of creating a schema.

```
gSQL> CREATE SCHEMA s1;

Schema created.
```

The following is an example of creating a schema and assigning the schema owner.

```
gSQL> CREATE SCHEMA s1 AUTHORIZATION test;

Schema created.
```

The following is an example of creating a schema together with the objects which belong to the schema.

```
gSQL> CREATE SCHEMA s1 
             CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
             CREATE INDEX idx_t1_id ON t1 ( id )
             COMMENT ON TABLE t1 IS 'comment on s1.t1'
;

Schema created.
```

<a id="eee53b67a1e1e226"></a>
### Compatibility

**SQL standard compatibility**

<a id="e1da5bdc30e0fe79"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="1802628b3f5508ad"></a>
### For More Information

Refer to the followings.

- [DROP SCHEMA](#3057681bb2ca4423)
- [CREATE USER](#67d566d84adb0376)
- [CREATE TABLE](#4c3b06d433f75b3d)
- [CREATE VIEW](#b82ddec42cccf582)
- [CREATE INDEX](#d54e994b20c1da1b)
- [CREATE SEQUENCE](#11cfe1f314df4ce6)
- [GRANT privileges TO](#c7985df8e45cc984)
- [COMMENT ON name IS](#ab6593b2744b2d0f)

<a id="11cfe1f314df4ce6"></a>
## CREATE SEQUENCE

<a id="457d5d0a332d23bf"></a>
### Function

It creates a sequence.

<a id="07c983fa0ed5af04"></a>
### Syntax

```
<sequence generator definition> ::=
    CREATE SEQUENCE [schema_name.] sequence_name 
        [ <sequence generator option> [, ...] ]
    ;

<sequence generator option> ::=
      <sequence generator start with option> 
    | <basic sequence generator option>

<sequence generator start with option> ::=
    START WITH integer

<basic sequence generator option> ::=
      <sequence generator increment by option>
    | <sequence generator maxvalue option>
    | <sequence generator minvalue option>
    | <sequence generator cycle option>
    | <sequence generator cache option>

<sequence generator increment by option> ::=
    INCREMENT BY integer

<sequence generator maxvalue option> ::=
      MAXVALUE integer
    | (NO MAXVALUE | NOMAXVALUE)

<sequence generator minvalue option> ::=
      MINVALUE integer
    | (NO MINVALUE | NOMINVALUE)

<sequence generator cycle option> ::=
      CYCLE 
    | (NO CYCLE | NOCYCLE)

<sequence generator cache option> ::=
      CACHE integer
    | (NO CACHE | NOCACHE)
```

<a id="bc67ff60fe7ecc98"></a>
### Invocation and Access Rules

The user should have one of the following privileges to perform &lt;sequence generator definition&gt; statement.  
• (CREATE SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence   
&nbsp;&nbsp;&nbsp;belongs  
• CREATE ANY SEQUENCE ON DATABASE

The sequence owner is determined as follows.  
• The owner of the schema to which the sequence belongs  
• If the schema to which the sequence belongs is PUBLIC, then it is the user who executed the statement.

The sequence owner has USAGE ON SEQUENCE WITH GRANT OPTION privilege.

One of the following privileges is required to use the created sequence.  
• USAGE ON SEQUENCE for the sequence  
• (USAGE SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence   
&nbsp;&nbsp;&nbsp;belongs  
• USAGE ANY SEQUENCE ON DATABASE

<a id="105c4d514c6e066e"></a>
### Syntax Rules and Parameters

<a id="bb89752bd29343aa"></a>
#### sequence_name

It is the sequence name to be created, and it should be a unique name within the schema.  
The schema to which the sequence belongs, such as schema_name.sequence_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the sequence name should be shorter than 128 bytes.

<a id="939a3207b3136dd1"></a>
#### &lt;sequence generator option&gt;

If any of &lt;sequence generator option&gt; is not used, the following two statements have the same meaning.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="1096c2cdfb8a0300"></a>
#### &lt;sequence generator start with option&gt;

It defines the first sequence number to be generated.  
Depending on the ascending or the descending order, it has the following features.

- Ascending sequence (INCREMENT BY a positive number)
    - It is used when starting the sequence with bigger sequence value than the minimum value.
    - If START WITH clause is omitted, the default value is the minimum value (MINVALUE value).
- Descending sequence (INCREMENT BY a negative number)
    - It is used when starting the sequence with smaller sequence value than the maximum value.
    - If START WITH clause is omitted, the default value is the maximum value (MAXVALUE value).

<a id="14ca204383daab85"></a>
#### &lt;sequence generator increment by option&gt;

It defines the interval of sequence numbers.  
The constraints and features are as follows.

- A positive number or a negative number is allowed, but 0 is not allowed.
- The absolute value of the interval should be smaller than the difference between MINVALUE and MAXVALUE.
- The ascending sequence is generated if it is a positive number, and the descending sequence is generated if it is a negative number.
- If INCREMENT BY clause is omitted, the default is a positive number 1.

<a id="58b40538aeb9ac0d"></a>
#### &lt;sequence generator maxvalue option&gt;

It defines the maximum value of which the sequence can generate.

- MAXVALUE integer 
    - The maximum value range is between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of the 64 bit integer.
    - It should be equal to or bigger than START WITH value, and bigger than MINVALUE value.
- NO MAXVALUE | NOMAXVALUE 
    - The maximum value is defined as follows.
        - If it is an ascending sequence, it is the maximum value (+9,223,372,036,854,775,807) of the 64 bit integer. 
        - If it is a descending sequence, it is -1.
    - NO MAXVALUE(SQL standard) and NOMAXVALUE are the reserved words with the same meaning, so either of them can be used. 
- If MAXVALUE and NO MAXVALUE are not specified, the default value is NO MAXVALUE.

<a id="588402c629619c5d"></a>
#### &lt;sequence generator minvalue option&gt;

It defines the minimum value of which the sequence can generate.

- MINVALUE integer 
    - The minimum value range is between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of the 64 bit integer. 
    - It should be equal to or smaller than START WITH value, and smaller than MAXVALUE. 
- NO MINVALUE | NOMINVALUE 
    - The minimum value is defined as follows.
        - If it is an ascending sequence, it is 1. 
        - If it is a descending sequence, it is the minimum value (-9,223,372,036,854,775,808) of the 64 bit integer. 
    - NO MINVALUE(SQL standard) and NOMINVALUE are the reserved words with the same meaning, so either of them can be used.
- If MINVALUE and NO MINVALUE are not specified, the default value is NO MINVALUE.

<a id="dadd46631db6f199"></a>
#### &lt;sequence generator cycle option&gt;

It specifies whether to continue generating a value when the sequence value becomes the maximum value or the minimum value.

- CYCLE 
    - When the ascending sequence becomes the maximum value, it generates the value again from the minimum value. 
    - When the descending sequence becomes the minimum value, it generates the value again from the maximum value. 
- NO CYCLE | NOCYCLE 
    - When the sequence value becomes the maximum value or the minimum value, it does not generate a sequence value. 
    - NO CYCLE(SQL standard) and NOCYCLE are the reserved words with the same meaning, so either of them can be used.
- If CYCLE and NO CYCLE are not specified, the default value is NO CYCLE.

<a id="104b5014fadfb096"></a>
#### &lt;sequence generator cache option&gt;

For quick access of a sequence, it defines the number of the sequence values to be preloaded in memory.  
When restarting database, the sequence values loaded in memory are lost, and it starts from the value since being loaded.

- CACHE integer 
    - CACHE value should be equal to or bigger than 2. 
    - CACHE value should not be bigger than CYCLE length, if CYCLE exists.
        - CYCLE length: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - The sequence values are not preloaded in memory.
- If CACHE and NO CACHE are not specified, the default value is CACHE 20.

<a id="a52aaedaa84ab5a0"></a>
### Description

The sequence values of the created sequence objects are used by using [NEXTVAL](17-built-in-function-references.md#09b72a3c73f75661) and [CURRVAL](17-built-in-function-references.md#e0d30993727500e4) functions.

The sequence value does not have a transaction property. The sequence value maintains the most recent value, even when an error occurs in the SQL statement in which the sequence function is used or when explicit ROLLBACK is performed.

CURRVAL function returns NEXTVAL value from the most recent call by a session.   
Therefore, using this feature, the sequence value obtained by NEXTVAL can still be usable in the other SQL statements. However, when the session does not call NEXTVAL, using CURRVAL function generates an error.

<a id="21b0985217d95cbf"></a>
### Examples

The object seq1 without the defined sequence options is an ascending sequence of the same meanings as the object seq2 in the following example.

```
gSQL> CREATE SEQUENCE seq1;

Sequence created.


gSQL> CREATE SEQUENCE seq2 START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

Sequence created.
```

The following is an example of a sequence which generates an odd value.

```
gSQL> CREATE SEQUENCE seq1 START WITH 1 INCREMENT BY 2;

Sequence created.
```

The following is an example of generating sequence which repeatedly generates an even number starting from 0 to 1000.

```
gSQL> CREATE SEQUENCE seq1 START WITH 0 MINVALUE 0 MAXVALUE 1000 INCREMENT BY 2 CYCLE;

Sequence created.
```

The following is an example of generating a descending sequence starting from -1.

```
gSQL> CREATE SEQUENCE seq1 INCREMENT BY -1;

Sequence created.
```

<a id="d8ced9608edd4a5a"></a>
### Compatibility

The SQL standard does not define &lt;sequence generator cache option&gt; clause.

**SQL standard compatibility**

<a id="dd2956503594adb4"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="5c19bb74d0d1228c"></a>
### For More Information

Refer to the followings.

- [DROP SEQUENCE](#61c1cea96080ef41)
- [ALTER SEQUENCE](18-sql-references-a-b.md#c19ab51ee6e2aea4)
- [NEXTVAL](17-built-in-function-references.md#09b72a3c73f75661)
- [CURRVAL](17-built-in-function-references.md#e0d30993727500e4)

<a id="fbdbe1b73f80a473"></a>
## CREATE SYNONYM

<a id="7f08851b106d82ba"></a>
### Function

It creates a synonym. A synonym is an alternative name for a table, view, sequence, or another synonym, and it can be used in the following statements.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="cf8eb3e6b1f294a8"></a>
### Syntax

```
<table definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="caadd588e906ea58"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;synonym definition&gt; statement.

- CREATE PUBLIC SYNONYM ON DATABASE privilege is required to create public synonym by explicitly specifying PUBLIC.

- The owner of public synonym is PUBLIC. The user who created the synonym does not have any privilege.

- One of the following privileges is required to create the private synonym.
    - (CREATE SYNONYM or CONTROL SCHEMA) ON SCHEMA for that schema
    - CREATE ANY SYNONYM ON DATABASE

- The private synonym owner is determined as follows.
    - The owner of the schema to which the private synonym belongs
    - If the schema to which the private synonym belongs is PUBLIC, then it is the user who executed the statement.

- If the user does not have privilege on the base object, the user is not allowed to execute the statement using its synonym even when the user created the synonym.

- Be cautious when allowing the privilege on the synonym because it means allowing privilege on the base object to which the synonym indicates.

<a id="a8c83e38ea0376b1"></a>
### Syntax Rules and Parameters

<a id="3be9e6be4eaf9d94"></a>
#### [ OR REPLACE ]

It replaces the existing synonym if the synonym already exists.

<a id="bf7e0db378d4f99a"></a>
#### [ PUBLIC ]

It is specified when creating public synonym.  
If it is omitted, private synonym is created.

<a id="f742a1dde97984ff"></a>
#### synonym_name

It is the synonym name to be created, and it should be a unique name within the schema.  
The schema to which the synonym belongs, such as schema_name.synonym_name, can be defined. If schema_name is omitted, default schema name of the user performing the statement is used.  
The length of the synonym name should be shorter than 128 bytes.  
Public synonym is a non-schema object. Therefore, a schema name can not be specified when creating public synonym by explicitly specifying PUBLIC.

<a id="584c35291db721be"></a>
#### object_name

The schema to which the object belongs, such as schema_name.object_name, can be defined. If schema_name is omitted, default schema name of the user performing the statement is used.

The object types which can specify the object_name are as follows.

- Table
- View
- Sequence
- Another synonym

Existence of the target object, cycle check and privilege check are performed when executing the statement using the synonym.

<a id="e25dd56c82984238"></a>
### Description

A synonym is an alternative name for a table, view, sequence, or another synonym.

If synonym is created, the applications do not need to be modified even when the base object is changed instead only the synonyms should be redefined. Therefore, it is convenient.   
Also, the database security is improved by hiding the objects' real names and their schemas, and the usability is enhanced by changing the object's long name to a shorter name.

The synonym is literally an alternative name so creating the synonym does not mean that the synonym can be used to access the object. The proper privilege is required to access the object.

When executing the statement using the synonym, the object access procedure is as follows.

1. Find a table of the corresponding name.
2. If the table does not exist, find the private synonym of the corresponding name.
3. If the private synonym does not exist, find the public synonym of the corresponding name.

```
gSQL> CREATE PUBLIC SYNONYM syn1 FOR u1.t1;

Synonym created.

gSQL> CREATE PUBLIC SYNONYM syn2 FOR syn1;

Synonym created.

gSQL> SELECT * FROM syn2;
```

The example above is the object access procedure in SELECT statement.

1. It searched for the table syn2, but it does not exist. 
2. It searched for the private synonym syn2, but it does not exist. 
3. It searched for the public synonym syn2, and it exists. 
    1. It searched for the table syn1, but it does not exist. 
    2. It searched for the private synonym syn1, but it does not exist. 
    3. It searched for the public synonym syn2, and it exists. 
        1. It searched for the table u1.t1, and it exists.

<a id="cbf2dcabc31eb6ae"></a>
### Examples

The following is an example of creating a private synonym.

```
gSQL> CREATE SYNONYM MyEmp FOR branch.Employee;

Synonym created.


gSQL> SELECT * FROM MyEmp;
```

The following is an example of creating a public synonym.

```
gSQL> CREATE PUBLIC SYNONYM MainEmp FOR main.Employee;

Synonym created.


gSQL> SELECT * FROM MainEmp;
```

<a id="438d05c85cbbee2e"></a>
### Compatibility

The SQL standard does not define the CREATE SYNONYM statement.

<a id="b5248f876ec6a924"></a>
### For More Information

Refer to [DROP SYNONYM](#b3cdccf874ce9683).

<a id="4c3b06d433f75b3d"></a>
## CREATE TABLE

<a id="d45eaefa740d4150"></a>
### Function

It defines a table.

<a id="84be21cfe9e8d2cf"></a>
### Syntax

```
<table definition> ::=
    CREATE TABLE table_name
        ( <table element> [, ...] )
        [ <table sharding strategy> ]
        [ <table attribute clause> [...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
    ;

<table element> ::=
      <column definition>
    | <table constraint definition>

<column definition> ::=
    column_name <data type> 
        [ <default clause> | <identity column specification> ]
        [ <column constraint definition> ]

<data type> ::=
      <character string type>
    | <binary string type>
    | <numeric type>
    | <boolean type>
    | <datetime type>
    | <interval type>

<character string type> ::=
      CHARACTER [ ( integer [ <character length units> ] ) ]
    | CHAR [ ( integer [ <character length units> ] ) ]
    | CHARACTER VARYING ( integer [ <character length units> ] )
    | CHAR VARYING ( integer [ <character length units> ] )
    | VARCHAR ( integer [ <character length units> ] )
    | CHARACTER LONG VARYING
    | LONG VARCHAR
  
<character length units> ::=
      CHARACTERS
    | CHAR
    | OCTETS
    | BYTE

<binary string type> ::=
      BINARY [ ( length ) ]
    | BINARY VARYING ( length )
    | VARBINARY ( length )
    | LONG BINARY VARYING
    | LONG VARBINARY

<numeric type> ::=
      <exact numeric type>
    | <approximate numeric type>
    | <native numeric type>

<exact numeric type> ::=
      NUMERIC [ ( precision [, scale ] ) ]
    | SMALLINT
    | INTEGER
    | INT
    | BIGINT

<approximate numeric type> ::=
    | FLOAT [ ( precision ) ]
    | REAL
    | DOUBLE PRECISION

<native numeric type> ::=
      NATIVE_SMALLINT
    | NATIVE_INTEGER
    | NATIVE_BIGINT
    | NATIVE_REAL
    | NATIVE_DOUBLE

<boolean type> ::=
    BOOLEAN

<datetime type> ::=
      DATE
    | TIME [ ( time_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
    | TIMESTAMP [ ( timestamp_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]

<interval type> ::=
    INTERVAL <interval qualifier>

<interval qualifier> ::=
      <non-second primary datetime field> [ ( interval_leading_field_precision ) ]
          TO { <non-second primary datetime field> | SECOND [ ( interval_fractional_seconds_precision ) ] }
    | <non-second primary datetime field> [ ( interval_leading_field_precision ) ]
    | SECOND [ ( interval_leading_field_precision [, interval_fractional_seconds_precision ] ) ]

<non-second primary datetime field> ::=
      YEAR
    | MONTH
    | DAY
    | HOUR
    | MINUTE

<default clause> ::=
    DEFAULT <default option>

<default option> ::=
      constant
    | NULL
    | expression

<identity column specification> ::=
    GENERATED { ALWAYS | BY DEFAULT } AS IDENTITY 
    [ ( <common sequence generator option> [, ...] ) ]

<common sequence generator option> ::=
      START WITH integer_constant
    | <basic sequence generator option>

<basic sequence generator option> ::=
      INCREMENT BY integer_constant 
    | { MAXVALUE integer_constant | NO MAXVALUE }
    | { MINVALUE integer_constant | NO MINVALUE }
    | { CYCLE | NO CYCLE }
    | { CACHE integer_constant | NO CACHE }

<column constraint definition> ::=
    [ CONSTRAINT constraint_name ] <column constraint> [ <constraint characteristics> ]

<column constraint> ::=
      NOT NULL
    | { UNIQUE | PRIMARY KEY } [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]

<index name clause> ::=
    INDEX index_name

<index attributes> ::=
      <index physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )


<table constraint definition> ::=
    [ CONSTRAINT constraint_name ] <table constraint> [ <constraint characteristics> ]

<table constraint> ::=
      <unique constraint definition> [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]

<unique constraint definition> ::=
    { UNIQUE | PRIMARY KEY } ( <key column element> [, ...] )

<key column element> ::=
    column_name [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]


<table sharding strategy> ::=
      <cloned strategy>
    | <hash sharding strategy>
    | <range sharding strategy>
    | <list sharding strategy>

<cloned strategy> ::=
    CLONED [ <clone placement> ]

<clone placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<hash sharding strategy> ::=
    SHARDING BY [HASH] ( column_list )
    [ <hash shard count> ]
    [ <hash shard placement> ]

<hash shard count> ::=
    SHARD COUNT integer

<hash shard placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<range sharding strategy> ::=
    SHARDING BY RANGE ( column_list )
    { <cluster-wide range shard placement> | <group-specific range shard placement> }

<cluster-wide range shard placement> ::=
    AT CLUSTER WIDE
    <range shard definition> [, ...]

<group-specific range shard placement> ::=
    <group-specific range shard definition> [, ...]

<group-specific range shard definition> ::=
    <range shard definition> AT CLUSTER GROUP group_name

<range shard definition> ::=
    SHARD range_name VALUES LESS THAN ( <range value clause> )

<range value clause> ::=
    <range value> [, ...]

<range value> ::=
      constant
    | MAXVALUE

<list sharding strategy> ::=
    SHARDING BY LIST ( column_name )
    { <cluster-wide list shard placement> | <group-specific list shard placement> }

<cluster-wide list shard placement> ::=
    AT CLUSTER WIDE
    <list shard definition> [, ...]

<group-specific list shard placement> ::=
    <group-specific list shard definition> [, ...]

<group-specific list shard definition> ::=
    <list shard definition> AT CLUSTER GROUP group_name

<list shard definition> ::=
      SHARD shard_name VALUES IN ( <list value clause> )

<list value clause> ::=
    <list value> [, ...]

<list value> ::=
      constant
    | NULL
    | DEFAULT


<table attribute clause> ::=
      [ <table physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]

<table physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<index physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]


<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ]

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="3302eacc08f6e61f"></a>
### Invocation and Access Rules

The differences between the stand-alone database and the cluster database are as follows.

- Stand-alone
    - It can not define &lt;table sharding strategy&gt;.
    - It can not define &lt;table global secondary index clause&gt;.
- Cluster
    - Constraints of PRIMARY KEY, UNIQUE should include all sharding keys.
    - It can not define the deferrable constraints.

The user should satisfy the following conditions to perform &lt;table definition&gt; statement.

- One of the following privileges is required for the schema in which a table is to be created.
    - (CREATE TABLE or CONTROL SCHEMA) ON SCHEMA for that schema
    - CREATE ANY TABLE ON DATABASE

- One of the following privileges is required for the tablespace in which a table is to be created.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- One of the following privileges is required for the schema in which the constraints are to be created when the constraints exists which were created together.
    - (ADD CONSTRAINT or CONTROL SCHEMA) ON SCHEMA for that schema
    - ALTER ANY TABLE ON DATABASE

- One of the following privileges is required for the tablespace in which the index is to be created when the key constraint is created together.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- The owner of the table is determined as follows.
    - The owner of the schema to which the table belongs
    - If the schema to which the table belongs is PUBLIC, then it is the user who executed the statement.

- The table owner has the following privileges for the created table.
    - The privilege for the table 
        - SELECT ON TABLE WITH GRANT OPTION 
        - INSERT ON TABLE WITH GRANT OPTION 
        - UPDATE ON TABLE WITH GRANT OPTION 
        - DELETE ON TABLE WITH GRANT OPTION 
        - TRIGGER ON TABLE WITH GRANT OPTION 
        - REFERENCES ON TABLE WITH GRANT OPTION 
        - LOCK ON TABLE WITH GRANT OPTION 
        - INDEX ON TABLE WITH GRANT OPTION 
        - ALTER ON TABLE WITH GRANT OPTION 
    - The privilege for all columns in the table. 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - The privilege for the constraint which was generated together
        - The owner of that constraint
        - The owner of the index which was generated together with the constraint

&lt;table sharding strategy&gt; statement can be used in a cluster system.

<a id="a0d1cd530e123cf7"></a>
### Syntax Rules and Parameters

<a id="0ca0ee5b6120fae6"></a>
#### table_name

It is the table name to be created and it should be a unique name within the schema.  
The schema to which the table belongs, such as schema_name.table_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the table name should be shorter than 128 bytes.

<a id="3c38e65e466d65e2"></a>
#### &lt;column definition&gt;

It defines the columns which configure the table.  
The table should include one or more column definitions.   
It can specify the column data type, default value, automatically generated value, and constraints.

<a id="2954bfeea93c781d"></a>
#### column_name

It is name of the column which configures a table and each column should have a unique name within the table.  
The length of the column name should be shorter than 128 bytes.

<a id="76443fbbed872e4f"></a>
#### &lt;data type&gt;

- &lt;character string type&gt; 
- &lt;binary string type&gt; 
- &lt;numeric type&gt; 
- &lt;exact numeric type&gt; 
- &lt;approximate numeric type&gt; 
- &lt;boolean type&gt; 
- &lt;datetime type&gt; 
- &lt;interval type&gt; 
- &lt;interval qualifier&gt; 
- &lt;non-second primary datetime field&gt;

It defines the data type of the column.  
When defining the column including automatically generated values(&lt;identity column specification&gt;), its data type should be one of SMALLINT, INTEGER or BIGINT.  
For more information about data types, refer to [Data Type](11-sql-elements.md#0bcfff149f5e9259).

<a id="355d5de543c2d369"></a>
#### &lt;character length units&gt;

It specifies the length unit of a single character for the character type.

- CHARACTERS/ CHAR assigns the maximum bytes of a single character as the length of a single character. Therefore, the length of multi-bytes single character such as Hangul is 1.
- OCTETS/ BYTE assigns one byte for the length of a single character. Therefore, the length of multi-bytes single character such as Hangul is multi-bytes.
- If it is omitted, it follows CHAR_LENGTH UNITS property which is used when creating the database.

The SQL standard defines CHARACTERS as a default value.

> The default value of the char length unit in other DBMS are as follows.
> 
> - Oracle, DB2: OCTETS
> - MS-SQL, MySQL, PostgreSQL: CHARACTERS
> 

<a id="fd1f3584f048c43c"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

It specifies the default value of a column.  
&lt;default clause&gt; and &lt;identity column specification&gt; can not be used together.  
When both of them are omitted, the default value is NULL.

<a id="ac3e45cb05f9c6b5"></a>
#### &lt;default clause&gt;

The DEFAULT clause defines the default value to be used when DEFAULT is specified in INSERT, UPDATE statements or the corresponding column name is omitted.

- When DEFAULT clause is used 
    - e.g. CREATE TABLE t1 ( id INTEGER, name VARCHAR(32) DEFAULT 'anonymous' ); 
    - When the column is omitted 
        - INSERT INTO t1(id) VALUES ( 1 ); 
        - INSERT INTO t1(id) SELECT id FROM other_table; 
    - When the DEFAULT is specified 
        - INSERT INTO t1 DEFAULT VALUES; 
        - INSERT INTO t1 VALUES ( 2, DEFAULT ); 
        - UPDATE t1 SET name = DEFAULT;

The data type of DEFAULT expression should be compatible with the data type of the column.  
If the data type is not compatible or the expression is not valid, an error occurs.

```
--# result: error
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

ERR-22012(12122): divisor is equal to zero


--# result: success
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 1 );

Table created.
```

DEFAULT expression can use any built-in functions but it can not use the followings.

- Logical operators (AND, OR, NOT), comparison operators (=,>, ...)
- Stored function
- Column name
- Subquery expression

<a id="7072b711465819ee"></a>
#### &lt;identity column specification&gt;

It defines a column which has automatically generated values.

The table can have only one identity column.  
The identity column becomes *not nullable* column even though NOT NULL constraint is not specified.

&lt;identity column specification&gt; clause can not be specified together with DEFAULT clause.  
&lt;identity column specification&gt; clause, like as DEFAULT clause, specifies DEFAULT in INSERT, UPDATE statements or it defines the default value to be used when the column name is omitted.

The generation method is defined as follows.

- GENERATED BY DEFAULT AS IDENTITY   
  A user defined value is applied if defined, but the value is automatically generated, like as DEFAULT clause, when the default value should be used.
    - CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) );
    - (O) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS');
        - It inserts the user defined value (12345).
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS');
        - It inserts the automatically generated value in an id column.
    - (O) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - It inserts the user defined value.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - It inserts the automatically generated value in an id column.
    - (O) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - It inserts the user defined value
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - It inserts the automatically generated value in an id column.

- GENERATED ALWAYS AS IDENTITY   
  A user can not define the value and the default value should be generated like as DEFAULT clause.
    - CREATE TABLE t1 ( id INTEGER GENERATED ALWAYS AS IDENTITY, name VARCHAR(32) ); 
    - (X) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS'); 
        - Error, a user can not define the value.
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS' ); 
        - It inserts the automatically generated value in an id column.
    - (X) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - Error, a user can not define the value.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - It inserts the automatically generated value in an id column.
    - (X) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - Error, a user can not define the value.
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - It inserts the automatically generated value in an id column.

For more information about &lt;common sequence generator option&gt; and &lt;basic sequence generator option&gt;, which are options to create an identity column, refer to [CREATE SEQUENCE](#11cfe1f314df4ce6).

<a id="ebe69ea3d2586d5e"></a>
#### &lt;column constraint definition&gt;

It defines the following constraints for a column.

- NOT NULL constraints
- UNIQUE constraints
- PRIMARY KEY constraints

<a id="4a9e97c4a634bc47"></a>
#### constraint_name

It is the constraint name and it can be omitted.

If the constraint_name is omitted, it is automatically set as follows.  
If the automatically generated name is duplicated, the constraint_name should be explicitly specified.

- NOT NULL constraints
    - "table_name" + "_" + "NOT_NULL" + "_" + "column_name" 
- UNIQUE constraints
    - "table_name" + "_" + "UNIQUE" + "_" + "column_name" 
- PRIMARY KEY constraints
    - "table_name" + "_" + "PRIMARY_KEY"

The length of the constraint name should be shorter than 128 bytes.

<a id="f8f677701b11d309"></a>
#### NOT NULL Constraint

NULL is not allowed for the column value.

<a id="b2033b40cd121394"></a>
#### UNIQUE Constraint

The identical value is not allowed for the column value, but NULL is allowed.

<a id="0ed294bac629af36"></a>
#### PRIMARY KEY Constraint

NULL or the identical value is not allowed as the column value. A single PRIMARY KEY constraint can be defined on a single table.

<a id="dacb2fc498cf2556"></a>
#### &lt;index name clause&gt;

It defines the index name to be created when defining UNIQUE constraint and PRIMARY KEY constraint.

- INDEX index_name 
    - It defines the index name for the constraint.
    - It can not be used together with a schema name and it is created in the same schema where the constraint is created.

When defining UNIQUE constraint and PRIMARY KEY constraint, if INDEX clause is omitted, an index which satisfies the constraints is automatically created.  
"constraint_name" + "INDEX" is added to the name of index which is automatically generated.

- &lt;index attributes&gt; 
    - It specifies the physical attributes of the index to be created.
    - For more information, refer to [CREATE INDEX](#d54e994b20c1da1b).
- TABLESPACE index_tablespace_name 
    - It specifies the tablespace where the index is to be created.
    - For more information, refer to [CREATE INDEX](#d54e994b20c1da1b).

<a id="2f2688dbb20b72dc"></a>
#### &lt;table constraint definition&gt;

&lt;unique constraint definition&gt;

- When defining a table, the constraints can be classified in two ways depending on the location in the statement.
    - When defining a column, column constraints can be specified by using &lt;column constraint definition&gt;.
    - On the other hand, the table constraint definition clause, &lt;table constraint definition&gt;, can be specified separately from the column definition and the constraints on one or more columns can be specified.

The table constraint definition has the following syntactic difference compared to the column constraint definition.

- NOT NULL constraint 
    - It can not be specified by using the table constraint definition.
- It should explicitly specify the column unlike the column constraint definition. 
    - UNIQUE constraint &lt;unique constraint definition&gt; 
        - UNIQUE ( column_name [, ...] ) 
    - PRIMARY KEY CONSTRAINT &lt;unique constraint definition&gt; 
        - PRIMARY KEY ( column_name [, ...] )

<a id="e7393f136740c124"></a>
#### key column element

It specifies the column to be a target of the key.

- column name 
    - It is name of the column which creates the key. 
- ASC | DESC 
    - ASC: It is sorted in an ascending order. 
    - DESC: It is sorted in a descending order. 
    - If not specified, the default value is ASC. 
- NULLS FIRST | NULLS LAST 
    - NULLS FIRST: It is located before non-NULL values. 
    - NULLS LAST: It is located after non-NULL values. 
    - If not specified, the default value is NULLS LAST.

<a id="789a6a7e7933b76d"></a>
#### &lt;table sharding strategy&gt;

It defines the sharding strategy of a table.  
It can be defined as one of the four following strategies.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

If it is omitted, it is determined by [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#538c33a1508d31f9) property value.

- If DEFAULT_SHARDING value is 0
    - &lt;cloned strategy&gt;
- If DEFAULT_SHARDING value is 1 
    - &lt;hash sharding strategy&gt;

<a id="a42a3a673f45e368"></a>
#### &lt;cloned strategy&gt;

It clones all data in a table.

<a id="00879e459c2d508e"></a>
#### &lt;clone placement&gt;

It defines the placement strategy of a clone.

- AT CLUSTER WIDE 
    - It places clones in all cluster members of all cluster groups in a cluster system.
    - A clone can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster group and a cluster member.
- AT CLUSTER GROUP group_list 
    - It places clones in all cluster members of a specified cluster groups.
    - A clone can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster member in a specified cluster group.
    - Adding a cluster group does not affect the relocation of the clone.
- When it is omitted, the default value is AT CLUSTER WIDE.

<a id="61e381cb95be2e43"></a>
#### &lt;hash sharding strategy&gt;

It shards the table data according to the hash value of the sharding key.

<a id="291f75e80c467b73"></a>
#### SHARDING BY [HASH] ( column_list )

It defines a sharding key for a hash sharding.

- It can list maximum 32 columns. 
- It can not use a duplicate column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="79be4fa4072d33b0"></a>
#### &lt;hash shard count&gt;

It defines the number of the hash shards to be sharded.  
The number of shards can be defined from 1 to 512.  
If it is omitted, the default value is 24.

<a id="039362b5c8e0de22"></a>
#### &lt;hash shard placement&gt;

It defines the placement strategy of a hash shard.

- AT CLUSTER WIDE 
    - It places shards in all cluster members of all cluster groups in a cluster system.
    - A shard can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster group and a cluster member.
- AT CLUSTER GROUP group_list 
    - It places hash shards in all cluster members of a specified cluster groups.
    - The number of group_list should be equal to or smaller than the value of &lt;hash shard count&gt;.
    - Unlike a range shard and a list shard, the cluster group on which the specific hash shard is to be located can not be specified, but the system automatically determines a cluster group on which the shard is to be located.
    - A shard can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster member in a specified cluster group.
    - Adding a cluster group does not affect the relocation of the hash shard.
- When it is omitted, the default value is AT CLUSTER WIDE.

<a id="a45b0a069f78b2cb"></a>
#### &lt;range sharding strategy&gt;

It shards the table data according to the range value of the sharding key.

<a id="4d63afc0c1e09625"></a>
#### SHARDING BY RANGE ( column_list )

It defines a sharding key for the range sharding.

- It can list maximum 32 columns. 
- It can not use a duplicate column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="74eba3c78b7d5ab0"></a>
#### &lt;cluster-wide range shard placement&gt;

It automatically places range shards in all cluster groups of a cluster system.  
AT CLUSTER WIDE statement is described before describing &lt;range shard definition&gt;.  
Shards can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster group and a cluster member.

- Create a range sharded table.
- Place six shards in the existing cluster groups (g1, g2, g3).

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    AT CLUSTER WIDE
    SHARD s1 VALUES LESS THAN ( 200000 ),
    SHARD s2 VALUES LESS THAN ( 400000 ),
    SHARD s3 VALUES LESS THAN ( 500000 ),
    SHARD s4 VALUES LESS THAN ( 600000 ),
    SHARD s5 VALUES LESS THAN ( 800000 ),
    SHARD s6 VALUES LESS THAN ( MAXVALUE )
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate the range shard.
- Place six shards in the cluster groups (g1, g2, g3, g4) including the added g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="1413c4bd2261d7b0"></a>
#### &lt;group-specific range shard placement&gt;

It places range shards in a specified cluster group.  
It describes AT CLUSTER GROUP group_name statement which places that shard together with &lt;range shard definition&gt;.  
Shards can be automatically relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster member to a specified cluster group.  
Adding a cluster group does not affect the relocation of the range shard.

- Create a range sharded table.
- Place each range shard in a specified cluster group.

```
CREATE TABLE t1 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
    SHARD s1 VALUES LESS THAN ( 200000 )   AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( 400000 )   AT CLUSTER GROUP g2,
    SHARD s3 VALUES LESS THAN ( 500000 )   AT CLUSTER GROUP g3,
    SHARD s4 VALUES LESS THAN ( 600000 )   AT CLUSTER GROUP g2,
    SHARD s5 VALUES LESS THAN ( 800000 )   AT CLUSTER GROUP g3,
    SHARD s6 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g1
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate a range shard.
- The shard is not placed in a newly created cluster group g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="5544cb57e15e2fb5"></a>
#### &lt;range shard definition&gt;

SHARD range_name should be unique in a table.

It can define maximum 512 of &lt;range shard definition&gt;.

The listed &lt;range shard definition&gt; is sorted in an order of &lt;range value clause&gt;, and it should use each different &lt;range value clause&gt;.

The &lt;range shard definition&gt; whose all values are define as MAXVALUE is a MAX shard.  
MAX shard should exist, and it should be a single one.

- It should include a MAX shard.

```
gSQL>
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000 ),
   SHARD s2 VALUES LESS THAN ( 200000 ),
   SHARD s3 VALUES LESS THAN ( MAXVALUE )
;

Table created.
```

- If it does not include a MAX shard, then an error occurs.

```
gSQL>
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000 ),
   SHARD s2 VALUES LESS THAN ( 200000 ),
   SHARD s3 VALUES LESS THAN ( 300000 )
;

ERR-42000(16377): MAX shard not defined : 
   SHARD s3 VALUES LESS THAN ( 300000 )
   *
ERROR at line 10:
```

<a id="251008606b79e7d7"></a>
#### &lt;range value clause&gt;

&lt;range value&gt; should be a constant or a MAXVALUE (a maximum value).  

NULL can not be used as &lt;range value&gt;.

- (O) SHARD s1 VALUES LESS THAN ( 1 ) 
- (O) SHARD s2 VALUES LESS THAN ( 1 + 1 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE ) 
- (X) SHARD s4 VALUES LESS THAN ( SYSDATE ) 
- (X) SHARD s5 VALUES LESS THAN ( NULL )

MAXVALUE is always bigger than any other value, and it includes null.

If there are multiple sharding keys, only a MAXVALUE can be specified after the MAXVALUE.

- (O) SHARD s1 VALUES LESS THAN ( 100, MAXVALUE ) 
- (X) SHARD s2 VALUES LESS THAN ( MAXVALUE, 100 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE, MAXVALUE )

If a sharding key is defined by using multiple columns, a MAX shard which is listed with MAXVALUE for its all values as like the SHARD s3 below should exist.

```
CREATE TABLE t1 
(
   id INTEGER,
   name VARCHAR(32)
)
SHARDING BY RANGE (id, name)
   AT CLUSTER WIDE
   SHARD s1 VALUES LESS THAN ( 100000, MAXVALUE ),
   SHARD s2 VALUES LESS THAN ( 200000, 20000 ),
   SHARD s3 VALUES LESS THAN ( MAXVALUE, MAXVALUE )
;
```

<a id="f44bdab84b0dee6b"></a>
#### &lt;list sharding strategy&gt;

It shards the table data according to the listed value of the sharding key.

<a id="f02f0b2457150a97"></a>
#### SHARDING BY LIST ( column_name )

It defines a sharding key for a list sharding.

- It can use only one column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="f58f518968309844"></a>
#### &lt;cluster-wide list shard placement&gt;

It automatically places list shards in all cluster groups of a cluster system.  
AT CLUSTER WIDE statement is described before describing &lt;range shard definition&gt;.  
Shards can be relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster group and a cluster member.

- Create a list sharded table.
- Place five shards in the existing cluster groups (g1, g2, g3).

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    AT CLUSTER WIDE
    SHARD s1 VALUES IN ( 'SEOUL' ),
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ),
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' ),
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' ),
    SHARD s5 VALUES IN ( DEFAULT )
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate a list shard.
- Place five shards in the cluster groups (g1, g2, g3, g4) including the added g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="f6f838031fb6d463"></a>
#### &lt;group-specific list shard placement&gt;

It places list shards in a specified cluster group.  
It describes AT CLUSTER GROUP group_name statement which places that shard together with &lt;list shard definition&gt;.  
Shards can be automatically relocated by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f7d09b5058d6293a) statement when adding a cluster member to a specified cluster group.  
Adding a cluster group does not affect the relocation of the list shard.

- Create a list sharded table.
- Place each list shard in a specified cluster group.

```
CREATE TABLE city 
(
   id   INTEGER,
   name VARCHAR(32)
)
SHARDING BY LIST (name)
    SHARD s1 VALUES IN ( 'SEOUL' )                   AT CLUSTER GROUP g1,
    SHARD s2 VALUES IN ( 'PUSAN', 'ULSAN', 'DAEGU' ) AT CLUSTER GROUP g2,
    SHARD s3 VALUES IN ( 'DAEJEON', 'GWANGJU' )      AT CLUSTER GROUP g3,
    SHARD s4 VALUES IN ( 'ANSAN', 'GOYANG' )         AT CLUSTER GROUP g2,
    SHARD s5 VALUES IN ( DEFAULT )                   AT CLUSTER GROUP g1
;
```

- Add a cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate a list shard.
- The shard is not placed in a newly added cluster group g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="bb0ff2228a2cbcef"></a>
#### &lt;list shard definition&gt;

LIST list_name should be unique in a table.

It can define maximum 512 of &lt;list shard definition&gt;.  
All &lt;list value&gt; of the listed &lt;list shard definition&gt; should be different each other.

DFFAULT are other values which is not the listed &lt;list value&gt;.  
DFFAULT can not be defined together with another value.  
A shard including DEFAULT is a DEFAULT shard.

MAX shard should exist, and it should be a single one.

- It should include a DEFAULT shard.

```
gSQL>
CREATE TABLE t1 
(
   category INTEGER,
   name     VARCHAR(32)
)
SHARDING BY LIST (category)
   AT CLUSTER WIDE
   SHARD s1 VALUES IN ( 1, 3, 5, 7 ),
   SHARD s2 VALUES IN ( 2, 4, 6, 8 ),
   SHARD s3 VALUES IN ( DEFAULT )
;

Table created.
```

- If it does not include a DEFAULT shard, then an error occurs.

```
gSQL>

CREATE TABLE t1 
(
   category INTEGER,
   name     VARCHAR(32)
)
SHARDING BY LIST (category)
   AT CLUSTER WIDE
   SHARD s1 VALUES IN ( 1, 3, 5, 7 ),
   SHARD s2 VALUES IN ( 2, 4, 6, 8 ),
   SHARD s3 VALUES IN ( 9, 10 )
;

ERR-42000(16385): DEFAULT shard not defined : 
   SHARD s3 VALUES IN ( 9, 10 )
   *
ERROR at line 10:
```

<a id="13ad8fb80d72fa56"></a>
#### &lt;list value clause&gt;

&lt;list value&gt; should be a constant.  
NULL or DEFAULT can be used as &lt;list value&gt;.

- (O) SHARD s1 VALUES IN ( 1, 1 + 1, 3, 4 ) 
- (O) SHARD s2 VALUES IN ( 5, 6, 7, NULL ) 
- (O) SHARD s3 VALUES IN ( DEFAULT ) 
- (X) SHARD s4 VALUES IN ( DEFAULT, 8, 9, 10 ) 
- (X) SHARD s5 VALUES IN ( current_timestamp, systimestamp ) 
- (X) SHARD s6 VALUES IN ( c1, c2 )

<a id="f51c022e96ec3285"></a>
#### &lt;table physical attribute clause&gt;

It defines the physical attribute information of the table.

- PCTFREE integer 
    - Definition 
        - The reserved space in case the row size is increased when altering or updating a row in a page.
        - The initial input is input in other space except for this reserved space.
        - If PCTFREE is not enough ROW MIGRATION occurs when altering or updating the data.
    - It can use of the value from 0 to 99.
    - If it is omitted, the default value is 10.

- PCTUSED integer 
    - Definition 
        - It is the minimum percentage which can be used for the row data and overhead before adding a new row to a page. 
        - It can be input only on this page when the value got smaller than PCTUSED due to alteration or deletion of the existing data. 
    - It can use of the value from 0 to 99.
    - If it is omitted, the default value is 40.

- INITRANS integer 
    - Definition 
        - It specifies the initial number of transactions which can simultaneously access the page. 
        - If the number of users who access the index is small, INITRANS is set to low, and if the number of users who simultaneously access the index is big, INITRANS is set to high. 
        - If necessary, it is automatically increased to the specified MAXTRANS. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions which can simultaneously access the page. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 8.

<a id="c2c4a604a850c08d"></a>
#### &lt;index physical attribute clause&gt;

It defines the physical attributes of the index.

- PCTFREE integer 
    - Definition
        - It is a reserved space for adjusting the frequency of page splits caused by the key insertion in the page.
        - It is applied only to the index bottom-up build.
    - It can use the value from 0 to 99. 
    - If it is omitted, the value set in DEFAULT_INDEX_PCTFREE property is used.
- INITRANS integer 
    - It is as same as INITRANS in &lt;table physical attribute clause&gt;. 
- MAXTRANS integer 
    - It is as same as MAXTRANS in &lt;table physical attribute clause&gt;.

<a id="139c7e675c98b948"></a>
#### &lt;segment attr clause&gt;

It describes the information about the space in which the table is stored.

- INITIAL integer 
    - Definition 
        - It specifies the size of physical storage space which is initially allocated when creating the table.
        - The size is aligned to the EXTENT size of TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' actually operates as 8192 bytes.)
        - The size (aligned to the size of TABLESPACE EXTENT) should be equal to or bigger than the size of MINEXTENTS, and it should be equal to or smaller than the size of the MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment. 
    - If it is omitted, the default value is a single EXTENT size of TABLESPACE where the table belongs.

- NEXT integer 
    - Definition 
        - It specifies the physical space size to be allocated when adding the space to the table.
        - The size is aligned to EXTENT size of TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' actually operates as 8192 bytes.)
        - NEXT is operated as follows according to the size of the remaining space of the currently available table. (The size of subtracting the currently used space from the size of MAXEXTENTS.)  
      - If the remaining space size is 0, then it can not extend the space.  
      - If the remaining space size is bigger than 0, but smaller than NEXT, then it allocates the  
      space as big as the remaining space.  
      - If the remaining space size is bigger than NEXT, then it allocates the space as big as the NEXT.
    - The minimum value is 1, and the maximum value depends on the system environment. 
    - If it is omitted, the default value is a single EXTENT size of TABLESPACE to which the table belongs.

- MINSIZE integer 
    - Definition 
        - It is the minimum space size which the table should maintain. 
        - It should be equal to or smaller than the value of MAXSIZE.
    - It is aligned to the EXTENT size of TABLESPACE to which the table belongs.
    - The minimum value is 1, and the maximum value depends on the system environment. 
    - If it is smaller than the size of two EXTENT, the size of two EXTENT is allocated.
    - If it is omitted, the default value is the size of two EXTENT.

- MAXSIZE integer 
    - Definition 
        - It is the maximum space size which can be allocated to a table.
        - It should be equal to or bigger than the value of MINSIZE.
    - This size is aligned to the EXTENT size of TABLESPACE to which the table belongs.
    - The minimum value is 1, and the maximum value depends on the system environment. 
    - If it is omitted, the default value is EXTENT size * 2147483647 (The maximum positive integer of INT32).

<a id="8ade2c6b3ba18f00"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="c175dde41c7a6b85"></a>
#### TABLESPACE tablespace_name

It specifies the tablespace name in which a table is to be stored.  
If TABLESPACE clause is omitted, the default tablespace_name of the user performing the statement is used.

<a id="7f104bd967c971d7"></a>
#### TABLESPACE index_tablespace_name

It specifies the tablespace name in which an index is to be stored.  
If TABLESPACE clause is omitted, then it uses the index tablespace of the user.   
If the index tablespace of the user is NULL, then the DISK table uses the user's data tablespace and the MEMORY table uses the user's default temporary tablespace.

<a id="9b16b26826aa044b"></a>
#### &lt;constraint characteristics&gt;

It defines characteristics of the constraint.  
When defining constraints, the following characteristics can be set.

- DEFERRABLE | NOT DEFERRABLE
- &lt;constraint check time&gt;

If &lt;constraint characteristics&gt; is omitted, it is set to NOT DEFERRABLE INITIALLY IMMEDIATE.

<a id="8b7dd2c609607ef9"></a>
#### DEFERRABLE | NOT DEFERRABLE

It sets whether the constraints checking is deferrable so that the constraints can be checked when executing COMMIT without checking when executing DML statements.

The checking time of the deferrable constraint is controlled by [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

- NOT DEFERRABLE
    - The checking point is not deferrable, and the constraints are checked when executing INSERT/DELETE/UPDATE statements. 
- DEFERRABLE
    - The checking point can be controlled by [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3) statement.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - The constraint is checked when executing DML statement. 
    - SET CONSTRAINTS constraint_name DEFERRED
        - The constraint is checked when executing COMMIT statement. 
- If not specified, the default value is determined in accordance with the &lt;constraint check time&gt;.
    - If INITIALLY IMMEDIATE is specified, the constraint check time is NOT DEFERRABLE.
    - If INITIALLY DEFERRED is specified, the constraint check time is DEFERRABLE.
    - If &lt;constraint check time&gt; is not specified, the constraint check time is NOT DEFERRABLE.

<a id="688a0064625c7c89"></a>
#### &lt;constraint check time&gt;

If the constraints are DEFERRABLE, it sets an initial value for the checking time.

- INITIALLY IMMEDIATE
    - The constraint is checked when executing the DML statements. 
- INITIALLY DEFERRED
    - The constraint is checked when executing the COMMIT statements. 
    - It can not be used together with NOT DEFERRABLE.
- If not specified, the default value is INITIALLY IMMEDIATE.

For more information about the deferrable constraints, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

<a id="85344e34acf4e13f"></a>
#### &lt;table global secondary index clause&gt;

It defines a global secondary index of the table.

- WITH GLOBAL SECONDARY INDEX [ &lt;index attributes&gt; [...] ] [ TABLESPACE tablespace_name ]
    - It creates a global secondary index when creating a table in a cluster system environment. 
    - &lt;index attribute&gt;
        - It sets an index attribute of a global secondary index.
    - TABLESPACE tablespace_name
        - It specifies a tablespace to create a global secondary index.
- WITHOUT GLOBAL SECONDARY INDEX
    - It does not create a global secondary index when creating a table in a cluster system environment.

<a id="55e0f8fcfa48c195"></a>
### Description

<a id="9c24cee53eea0c2f"></a>
#### Constraint Characteristics

GOLDILOCKS automatically creates an index to check the uniqueness when generating key constraints.

The following columns do not allow NULL value.

- A column including NOT NULL constraint
- A column which is included in primary key constraints
- An identity column

<a id="34c89a07a239684c"></a>
#### Cluster Table

A table manages data using one of the following sharding strategies in a cluster environment.

- Cloned table
    - It duplicates all table data and places them in a cluster system.
- Hash sharded table
    - It divides the table data into several shards based on the hash value of a sharding key, then places them in the cluster system.
- Range sharded table
    - It divides the table data into several shards based on the range value of a sharding key, then places them in the cluster system.
- List sharded table
    - It divides the table data into several shards based on the list value of a sharding key, then places them in the cluster system.

The sharding strategy is determined considering the followings when creating a table. Tables operated in a cluster system are specified as a code table and a fact table based on its features.

- Code table 
    - It is a table such as a product list or a provider list whose data is relatively small and is not often altered
    - This table is referenced often together with a fact table. 
- Fact table 
    - It is a table such as a transaction history or a call history whose data is relatively big and is often altered. 
    - Its data is big so required to be sharded.

&lt;cloned strategy&gt; is appropriate for a code table, and an appropriate &lt;table sharding strategy&gt; should be determined according to the table access pattern in case of a fact table.

<a id="d073effc67514b54"></a>
### Examples

The following is an example of generating an ordinary table.

```
gSQL> CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
);

Table created.
```

The following is an example of specifying the constraints on the columns when creating a table.

```
gSQL> CREATE TABLE supplier
(
    s_suppkey     INTEGER PRIMARY KEY
  , s_name        CHAR(25) NOT NULL
  , s_address     VARCHAR(40)
  , s_nationkey   INTEGER
  , s_phone       CHAR(15)
  , s_acctbal     NUMERIC(12,2)
  , s_comment     VARCHAR(101)
);

Table created.
```

The following is an example of specifying the constraint which includes multiple columns when creating a table.

```
gSQL> CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
  , CONSTRAINT ps_unique_key UNIQUE(ps_partkey, ps_suppkey)
);

Table created.
```

The following is an example of specifying whether constraints are deferrable when creating a table.

```
gSQL> CREATE TABLE t1 
( 
    id     NUMBER        PRIMARY KEY 
                         NOT DEFERRABLE INITIALLY IMMEDIATE
  , name   VARCHAR(128)  CONSTRAINT t1_nn NOT NULL 
                         DEFERRABLE INITIALLY IMMEDIATE
  , addr   VARCHAR(1024) 
  , CONSTRAINT t1_uk UNIQUE ( id, name ) 
                     DEFERRABLE INITIALLY DEFERRED
);

Table created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of specifying a column including automatically generated values and the default value when creating a table.

```
CREATE TABLE customer
(
    c_custkey     INTEGER   GENERATED BY DEFAULT AS IDENTITY
  , c_name        VARCHAR(25)
  , c_address     VARCHAR(40) DEFAULT 'N/A'
  , c_nationkey   INTEGER
  , c_phone       CHAR(15)
  , c_acctbal     NUMERIC(12,2)
  , c_mktsegment  CHAR(10)
  , c_comment     VARCHAR(117)
);

Table created.
```

The following is an example of specifying the tablespace which is to be stored when creating a table.

```
gSQL> CREATE TABLE lineitem
(
    l_orderkey      INTEGER
  , l_partkey       INTEGER
  , l_suppkey       INTEGER
  , l_linenumber    INTEGER
  , l_quantity      NUMERIC(12,2)
  , l_extendedprice NUMERIC(12,2)
  , l_discount      NUMERIC(12,2)
  , l_tax           NUMERIC(12,2)
  , l_returnflag    CHAR(1)
  , l_linestatus    CHAR(1)
  , l_shipdate      DATE
  , l_commitdate    DATE
  , l_receiptdate   DATE
  , l_shipinstruct  CHAR(25)
  , l_shipmode      CHAR(10)
  , l_comment       VARCHAR(44)
  , PRIMARY KEY (l_orderkey, l_linenumber) INDEX lineitem_pk_idx TABLESPACE mem_temp_tbs
) TABLESPACE mem_data_tbs;

Table created.
```

The following is an example of defining a cluster-wide cloned table. The table data is copied and placed all over the cluster system.

```
gSQL>
CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
)
CLONED
AT CLUSTER WIDE
;

Table created.
```

The following is an example of defining a group-specific cloned table. The table data is copied and placed in a cluster group g1 and g2 specified by a user.

```
gSQL> 
CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
)
CLONED
AT CLUSTER GROUP g1, g2
;

Table created.
```

The following is an example of defining a cluster-wide hash sharded table. The table data is divided into 24 shards based on the hash value of a ps_partkey column, and each shard is automatically placed all over the cluster system.

```
gSQL>
CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
)
SHARDING BY HASH ( ps_partkey )
SHARD COUNT 24
AT CLUSTER WIDE
;

Table created.
```

The following is an example of defining a group-specific hash sharded table. The table data is divided into 24 shards based on the hash value of a ps_partkey column, and each shard is automatically placed in the specified cluster groups g2 and g3.

```
gSQL>
CREATE TABLE partsupp
(
    ps_partkey    INTEGER
  , ps_suppkey    INTEGER
  , ps_availqty   INTEGER
  , ps_supplycost NUMERIC(12,2)    
  , ps_comment    VARCHAR(199)
)
SHARDING BY HASH ( ps_partkey )
SHARD COUNT 24
AT CLUSTER GROUP g2, g3
;

Table created.
```

The following is an example of defining a cluster-wide range sharded table. The table data is divided into 24 shards based on the range value of D_ID column, and each shard is automatically placed all over the cluster system.

```
gSQL>
CREATE TABLE DISTRICT (
    D_ID        INTEGER, 
    D_W_ID      INTEGER, 
    D_NAME      VARCHAR(10), 
    D_STREET_1  VARCHAR(20), 
    D_STREET_2  VARCHAR(20), 
    D_CITY      VARCHAR(20), 
    D_STATE     CHAR(2), 
    D_ZIP       CHAR(9), 
    D_TAX       NUMERIC(4,4), 
    D_YTD       NUMERIC(15,2), 
    D_NEXT_O_ID INTEGER,

    PRIMARY KEY (D_W_ID, D_ID) INDEX DISTRICT_PK_IDX
) 
    SHARDING BY RANGE (D_ID)
    AT CLUSTER WIDE
    SHARD s1 VALUES LESS THAN ( 100 ),
    SHARD s2 VALUES LESS THAN ( 200 ),
    SHARD s3 VALUES LESS THAN ( 300 ),
    SHARD s4 VALUES LESS THAN ( 400 ),
    SHARD s5 VALUES LESS THAN ( 500 ),
    SHARD s6 VALUES LESS THAN ( 600 ),
    SHARD s7 VALUES LESS THAN ( 700 ),
    SHARD s8 VALUES LESS THAN ( MAXVALUE );
;

Table created.
```

The following is an example of defining a group-specific range sharded table. The table data is divided into three range values based on the range value of a NO_D_ID column, and a shard s1 is placed in a cluster group g1, a shard s2 is placed in a cluster group g2, a shard s3 is placed in a cluster group g3.

```
gSQL>
CREATE TABLE NEW_ORDER
(
    NO_O_ID INTEGER,
    NO_D_ID INTEGER,
    NO_W_ID INTEGER,

    PRIMARY KEY(NO_W_ID, NO_D_ID, NO_O_ID) INDEX NEW_ORDER_PK_IDX
) 
    SHARDING BY RANGE (NO_D_ID)
    SHARD s1 VALUES LESS THAN ( 5 )        AT CLUSTER GROUP g1,
    SHARD s2 VALUES LESS THAN ( 8 )        AT CLUSTER GROUP g2,
    SHARD s3 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g3
;

Table created.
```

The following is an example of defining a cluster-wide list sharded table. A list shard is divided into five based on a city column, and each shard is automatically placed all over the cluster system.

```
gSQL>
CREATE TABLE t1 
(
    id   INTEGER
  , name VARCHAR(32)
  , city VARCHAR(128) 
) 
   SHARDING BY LIST (city)
      AT CLUSTER WIDE
      SHARD s1 VALUES IN ( 'seoul' ),
      SHARD s2 VALUES IN ( 'busan', 'ulsan' ),
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ),
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ),
      SHARD s5 VALUES IN ( DEFAULT )            
;

Table created.
```

The following is an example of defining a group-specific list sharded table. A list shard is divided into five based on a city column, and each shard is placed in a specified cluster group.

```
gSQL>
CREATE TABLE t1 
(
    id   INTEGER
  , name VARCHAR(32)
  , city VARCHAR(128) 
) 
   SHARDING BY LIST (city)
      SHARD s1 VALUES IN ( 'seoul' )                  AT CLUSTER GROUP g1,
      SHARD s2 VALUES IN ( 'busan', 'ulsan' )         AT CLUSTER GROUP g2,
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ) AT CLUSTER GROUP g1,
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ) AT CLUSTER GROUP g2,
      SHARD s5 VALUES IN ( DEFAULT )                  AT CLUSTER GROUP g3
;

Table created.
```

A table T1 is created without a global secondary index.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITHOUT GLOBAL SECONDARY INDEX;

Table created.
```

A global secondary index is created after creating a table T1.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITH GLOBAL SECONDARY INDEX;

Table created.
```

A global secondary index of table T1 is created in a tablespace USER_DATA_TBS as a logging index after creating a table T1.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_DATA_TBS;

Table created.
```

A global secondary index of table T1 is created in a tablespace USER_TEMP_TBS as a nologging  index after creating a table T1.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_TEMP_TBS;

Table created.
```

<a id="e053eb9660a61df0"></a>
### Compatibility

The SQL standard does not define the following clauses.

- The physical concepts of TABLESPACE clause and &lt;physical attribute clause&gt; clause. 
- The SQL standard does not allow an operation in DEFAULT clause.

**SQL standard compatibility**

<a id="7c18519fa773be34"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T171 | LIKE clause in table definition | X |
| F531 | Temporary tables | X |
| S051 | Create table of type | X |
| S043 | Enhanced reference types | X |
| S081 | Subtables | X |
| T173 | Extended LIKE clause in table definition | X |
| T180 | System-versioned tables | X |
| F692 | Extended collation support | X |
| T174 | Identity columns | O |
| T175 | Generated columns | X |
| S071 | SQL paths in function and type name resolution | X |
| F321 | User authorization | O |
| T322 | Extended roles | X |
| F762 | CURRENT_CATALOG | O |
| F763 | CURRENT_SCHEMA | O |

<a id="b84de9eededc0a3f"></a>
### For More Information

Refer to the followings.

- [DROP TABLE](#99cce8728f930322)
- [ALTER TABLE](18-sql-references-a-b.md#8d2122be368c72be)
- [CREATE TABLESPACE](#cfdf7d2f50958860)
- [CREATE SCHEMA](#f7ea7ef79efa639b)
- [CREATE INDEX](#d54e994b20c1da1b)
- [CREATE SEQUENCE](#11cfe1f314df4ce6)
- [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#35909868f7689aed)

<a id="c4998a213dbc93e2"></a>
## CREATE TABLE AS SELECT

<a id="1a72a169d1f5eb92"></a>
### Function

It creates a new table from the query result.

<a id="df5014ae58d1f6f7"></a>
### Syntax

```
<table definition: AS query expression> ::=
    CREATE TABLE table_name 
        [ ( column_name [, ...] ) ]
        [ <table sharding strategy> ]
        [ <table attribute clause> [, ...] ]
        [ TABLESPACE tablespace_name ]
        [ <table global secondary index clause> ]
        AS <query expression> [ WITH [ NO ] DATA ]
    ;

<table sharding strategy> ::=
      <cloned strategy>
    | <hash sharding strategy>
    | <range sharding strategy>
    | <list sharding strategy>

<cloned strategy> ::=
    CLONED [ <clone placement> ]

<clone placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<hash sharding strategy> ::=
    SHARDING BY [HASH] ( column_list )
    [ <hash shard count> ]
    [ <hash shard placement> ]

<hash shard count> ::=
    SHARD COUNT integer

<hash shard placement> ::=
      AT CLUSTER WIDE
    | AT CLUSTER GROUP group_list

<range sharding strategy> ::=
    SHARDING BY RANGE ( column_list )
    { <cluster-wide range shard placement> | <group-specific range shard placement> }

<cluster-wide range shard placement> ::=
    AT CLUSTER WIDE
    <range shard definition> [, ...]

<group-specific range shard placement> ::=
    <group-specific range shard definition> [, ...]

<group-specific range shard definition> ::=
    <range shard definition> AT CLUSTER GROUP group_name

<range shard definition> ::=
    SHARD range_name VALUES LESS THAN ( <range value clause> )

<range value clause> ::=
    <range value> [, ...]

<range value> ::=
      constant
    | MAXVALUE

<list sharding strategy> ::=
    SHARDING BY LIST ( column_name )
    { <cluster-wide list shard placement> | <group-specific list shard placement> }

<cluster-wide list shard placement> ::=
    AT CLUSTER WIDE
    <list shard definition> [, ...]

<group-specific list shard placement> ::=
    <group-specific list shard definition> [, ...]

<group-specific list shard definition> ::=
    <list shard definition> AT CLUSTER GROUP group_name

<list shard definition> ::=
      SHARD shard_name VALUES IN ( <list value clause> )

<list value clause> ::=
    <list value> [, ...]

<list value> ::=
      constant
    | NULL
    | DEFAULT


<table attribute clause> ::=
      [ <table physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]

<table physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<index physical attribute clause> ::=
      PCTFREE integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
      INITIAL <size_clause>
    | NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="10f42f30e5641cab"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;table definition:AS query expression&gt;statement.

- Table creation privilege
    - Refer to the access privilege in [CREATE TABLE](#4c3b06d433f75b3d).
- SELECT access privilege 
    - Refer to the access privilege in [SELECT](20-sql-references-h-z.md#94be89d31f330d61).

<a id="6d860dcad9d964ac"></a>
### Syntax Rules and Parameters

<a id="d4973082c4d9a06a"></a>
#### table_name

It is the table name to be created.  
For more information, refer to [table_name](#0ca0ee5b6120fae6).

<a id="5b4de98bd1cae8ca"></a>
#### column_name_list

These are the names of the columns that configure the table, and it should be unique names within the table.  
The number of columns should be as same as the number of result columns in SELECT clause.  
If not specified, the column names of SELECT clause in &lt;query expression&gt; are used.

However, if an expression (such as a function, operation, or subquery) is used instead of a column in SELECT clause, the alias or column name should be specified.

The length of the column name should be shorter than 128 bytes.

<a id="505200f7a36152dd"></a>
#### WITH [NO] DATA

If WITH DATA is specified, the result of SELECT clause is inserted to the table to be created.  
If WITH NO DATA is specified, the result of SELECT clause is not inserted to the table to be created.   
If not specified, it is operated as same as when WITH DATA is specified.

<a id="766303b2f7e721ff"></a>
#### Other Syntax

For more information about other syntaxes, refer to the syntax in [CREATE TABLE](#4c3b06d433f75b3d) statement.

<a id="337e80d02361966b"></a>
### Description

When executing CREATE TABLE AS SELECT, if a column including a  NOT NULL constraint is specified in SELECT list, the NOT NULL constraint is also created in the new table.  
However, if the NOT NULL constraint is deferrable, then NOT NULL constraint is not created in the new table.

On the other hand, the NOT NULL constraint is not created in the new table if NOT NULL constraint was not explicitly created but there is NOT NULL property such as primary key column or identity column.

<a id="990beba8345b03cb"></a>
### Examples

The following is an example of executing CREATE TABLE AS SELECT statement.

```
gSQL> CREATE TABLE recent_orders 
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

The following is an example of specifying the column name.

```
gSQL> CREATE TABLE recent_orders ( order_id, order_item, order_date )
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

The following is an example of a function in SELECT list.

```
gSQL> CREATE TABLE recent_orders ( order_date, order_count )
                AS SELECT order_date, COUNT(*) 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
                   GROUP BY order_date;
Table created.
```

The following is an example of the statement including WITH DATA.

```
gSQL>CREATE TABLE orders 
( 
    order_id   NUMBER        
  , order_item VARCHAR(128)  
  , order_date DATE
);
gSQL> COMMIT;
gSQL> INSERT INTO orders VALUES ( 1, 'Pen', '2010-01-01' );
gSQL> INSERT INTO orders VALUES ( 2, 'Book', '2015-03-03' );
gSQL> COMMIT;
gSQL> CREATE TABLE recent_orders
                AS SELECT order_id, order_item, order_date 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
      WITH DATA;
Table created.
gSQL> SELECT COUNT(*) FROM recent_orders;

COUNT(*)
--------
       1

1 row selected.
```

The following is an example of the statement including WITH NO DATA.

```
gSQL>CREATE TABLE orders 
( 
    order_id   NUMBER        
  , order_item VARCHAR(128)  
  , order_date DATE
);
gSQL> COMMIT;
gSQL> INSERT INTO orders VALUES ( 1, 'Pen', '2010-01-01' );
gSQL> INSERT INTO orders VALUES ( 2, 'Book', '2015-03-03' );
gSQL> COMMIT;
gSQL> CREATE TABLE recent_orders
                AS SELECT order_id, order_item, order_date 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
      WITH NO DATA;
Table created.
gSQL> SELECT COUNT(*) FROM recent_orders;

COUNT(*)
--------
       0

1 row selected.
```

<a id="1e3b2fcd1141b545"></a>
### Compatibility

CREATE TABLE AS SELECT statement follows SQL standard. However, the following is an extension of SQL standard.

- SQL standard requires parentheses outside SELECT clause, but it is optional in GOLDILOCKS. 
- SQL standard requires WITH [NO] DATA clause, but it is optional in GOLDILOCKS. 
- The concepts of tablespace in GOLDILOCKS is an extended concept, and it is not supported in SQL standard.

**SQL standard compatibility**

<a id="5d99dc30e0d00a50"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="2fc2131d88491c5a"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#4c3b06d433f75b3d)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)

<a id="cfdf7d2f50958860"></a>
## CREATE TABLESPACE

<a id="22717eb4777246aa"></a>
### Function

It creates a tablespace.

<a id="26a4588979b3f4e4"></a>
### Syntax

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="cb7f11733fd49f6b"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;create tablespace statement&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="adfb0a4e3be008c1"></a>
### Syntax Rules and Parameters

<a id="837ffc7b7126f58d"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

It is a memory temporary tablespace to store the no logging indexes or the temporary objects such as intermediate results which are generated during the query processing.  
The reserved word MEMORY can be omitted.

<a id="96c76cd44ad194ab"></a>
#### &lt;memory data tablespace clause&gt;

It defines a memory data tablespace.  
For more information, refer to [CREATE MEMORY DATA TABLESPACE](#9831f431f182fce6).

<a id="0df7653490d24bd4"></a>
#### &lt;memory temporary tablespace definition&gt;

It defines a memory temporary tablespace.  
For more information, refer to [CREATE MEMORY TEMPORARY TABLESPACE](#504552ef753c144a).

<a id="a1ccd7e80baec33d"></a>
### Description

For more information, refer to the description of each detailed statement.

<a id="7f1b02c1cf6394ef"></a>
### Example

For more information, refer to usage example of each detailed statement.

<a id="1f7f5fa3fd235712"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="02145dd61ca9e502"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#a9171e5695f3e4e0)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)

<a id="67d566d84adb0376"></a>
## CREATE USER

<a id="7d51b958dcbc21e6"></a>
### Function

It defines a database user.

<a id="cac3160922261328"></a>
### Syntax

```
<user definition> ::=
    CREATE USER user_identifier IDENTIFIED BY password
    [ PROFILE { profile_name | DEFAULT | NULL } ]
    [ PASSWORD EXPIRE ]
    [ ACCOUNT { LOCK | UNLOCK } ]
    [ DEFAULT TABLESPACE tablespace_name ]
    [ TEMPORARY TABLESPACE tablespace_name ]
    [ INDEX TABLESPACE { tablespace_name | NULL } ]
    [ <schema clause> ]
    ;

<schema clause> ::=
      WITH SCHEMA [schema_name]
    | WITHOUT SCHEMA
```

<a id="94c5668906a05d5b"></a>
### Invocation and Access Rules

CREATE USER ON DATABASE privilege is required to perform &lt;user definition&gt;.

The created user, user_identifier, has the privilege, which is the owner the schema created by using &lt;schema clause&gt;.

> A separate privilege is not granted to the created user_identifier.   
> The appropriate privileges should be granted to user_identifier to access and perform SQL statements.

<a id="208ff6b55f896918"></a>
### Syntax Rules and Parameters

<a id="3f8f841b88209dcb"></a>
#### user_identifier

It is the username to be created.  
The identical username (user identifier) or role (role name) should not exist.  
The length of user_identifier should be shorter than 128 bytes.

<a id="a5fa71daa67b6233"></a>
#### password

It is the user's password to be created. It is encrypted and stored.  
The length of password should be shorter than 128 bytes.  
The password is case sensitive.  
The password should start with an alphabetic character, and it can include alphabetic characters, numbers, underscore (_), and $.   
The other special characters should be enclosed in double quotes (").

<a id="c94b6939a2d928d5"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

The profile for password management policy is assigned.

- PROFILE profile_name
    - It allocates the profile_name which is created by a user. 
- PROFILE DEFAULT
    - It allocates the default profile "DEFAULT". 
- PROFILE NULL
    - It does not allocate the profile.

If PROFILE clause is omitted, it is as same as PROFILE NULL, and the profile is not applied.  
For more information about the password management policy, refer to [CREATE PROFILE](#fa2854762beb7024).

<a id="9554a822549ad3c2"></a>
#### PASSWORD EXPIRE

It expires the user's password.  
It is used when a user attempts to change the password by force before login.

<a id="665aaf98097103ea"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - It locks the user account. 
- ACCOUNT UNLOCK
    - It unlocks the user account.

<a id="4a1f68a9b8a51ff1"></a>
#### DEFAULT TABLESPACE tablespace_name

It specifies the default TABLESPACE to store objects such as the table created by the user, the indexes (with NOLOGGING option).  
If DEFAULT TABLESPACE clause is omitted, default data tablespace(MEM_DATA_TBS) is specified, which was defined when creating DATABASE.

<a id="abba81b6ece44197"></a>
#### TEMPORARY TABLESPACE tablespace_name

It specifies the TABLESPACE which stores the temporary tables created by a user, indexes (NO LOGGING), and the intermediate results generated by the query processing.  
If TEMPORARY TABLESPACE clause is omitted, default temporary tablespace (MEM_TEMP_TBS) is specified, which was defined when creating DATABASE.

<a id="775df3dee63ac836"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

It specifies the default TABLESPACE which stores the index objects created by a user.

- Specifying INDEX TABLESPACE tablespace_name
    - If it specifies the data tablespace, then it becomes the LOGGING index.
    - If it specifies the temporary tablespace, then it becomes the NOLOGGING index.

- INDEX TABLESPACE NULL
    - It does not specify the index tablespace.

If INDEX TABLESPACE clause is omitted, then it is INDEX TABLESPACE NULL.

<a id="8d11071e5d32cf04"></a>
#### &lt;schema clause&gt;

It creates a schema which a user uses by default.  
The schema name should be unique in the database.

- WITH SCHEMA [schema_name] 
    - If schema_name is not assigned, the schema is created whose name is as same as user_identifier.
    - SCHEMA PATH of the user is set as follows.
        - schema_name, PUBLIC 
- WITHOUT SCHEMA 
    - It does not create the schema which is to be owned by a user.
    - SCHEMA PATH of the user is set as PUBLIC.

If &lt;schema clause&gt; is not specified, the default value is WITH SCHEMA and the schema is created whose name is as same as user_identifier.  
The schema to be owned by the user can be additionally created by using [CREATE SCHEMA](#f7ea7ef79efa639b) statement.

<a id="2125ab5e65c5336b"></a>
### Description

A user is an authorization object which consists of a set of privileges.

When &lt;user definition&gt; statement is executed for the first time, a user without any privilege is created, and the appropriate privileges should be granted as follows.

In GOLDILOCKS, the relationship between user and schema is 1 : N.  
In other words, a user does not own any schema, or a user can own multiple schemas.

The SQL standard does not explicitly define the relationship of the non-schema objects such as a user, a schema, or a database. Each DBMS defines the relationship of non-schema objects in different concept as follows.

> The relationship between user and schema in other DBMS.  
> 
> 
> - Oracle
>     - User : schema = 1 : 1.
> 
> 
> 
> - DB2 
>     - It is as same as the OS user.
>     - The separate SQL statements which creates or deletes a user do not exist.
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N. 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1.
>     - User is a subordinate object of database (schema).
> 

<a id="322aee49fff9fbe6"></a>
### Examples

At least the following privileges should be granted to create a user, and for the created user to create the objects, manipulate data.

The following is an example of creating a user and granting privileges.

• Create a user.

```
gSQL> CREATE USER u1 IDENTIFIED BY u1_password
             DEFAULT   TABLESPACE mem_data_tbs
             TEMPORARY TABLESPACE mem_temp_tbs
             INDEX TABLESPACE NULL;

User created.

gSQL> COMMIT;

Commit complete.
```

• Grant database privileges.

```
gSQL> GRANT CREATE SESSION ON DATABASE TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

• Grant schema privileges.

```
GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE, ADD CONSTRAINT 
      ON SCHEMA u1 TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

• Grant tablespace privileges.

```
GRANT CREATE OBJECT ON TABLESPACE mem_data_tbs TO u1;

Grant succeeded.

GRANT CREATE OBJECT ON TABLESPACE mem_temp_tbs TO u1;

Grant succeeded.

COMMIT;

Commit complete.
```

The following is an example of creating objects by the user.

• It needs CREATE SESSION ON DATABASE.

```
gSQL> \connect u1 u1_password
```

• It needs CREATE TABLE ON SCHEMA u1.   
• It needs CREATE OBJECT ON TABLESPACE mem_data_tbs.

```
gSQL> CREATE TABLE u1.t1 ( c1 INTEGER, c2 INTEGER ) TABLESPACE mem_data_tbs;

Table created.

gSQL> COMMIT;
```

• It needs CREATE INDEX ON SCHEMA u1.   
• It needs CREATE OBJECT ON TABLESPACE mem_temp_tbs.

```
gSQL> CREATE INDEX u1.idx ON t1 (c2) TABLESPACE mem_temp_tbs;

Index created.

gSQL> COMMIT;
```

• It needs ADD CONSTRAINT ON SCHEMA u1.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT u1.t1_pk PRIMARY KEY (c1) ;

Table altered.

gSQL> COMMIT;
```

• It needs CREATE SEQUENCE ON SCHEMA u1.

```
gSQL> CREATE SEQUENCE u1.seq;

Sequence created.

gSQL> COMMIT;

gSQL> INSERT INTO u1.t1 VALUES ( u1.seq.NEXTVAL, u1.seq.NEXTVAL );

1 row created

gSQL> COMMIT;
```

<a id="144c35cee41e265b"></a>
### Compatibility

The SQL standard covers the concepts of the user, but it does not define the SQL statements associated with the creation and deletion of user.

<a id="36032ec03ed08e6d"></a>
### For More Information

Refer to the followings.

- [DROP USER](#f64464bae416acc8)
- [ALTER USER](18-sql-references-a-b.md#270d91f0c78160b6)
- [CREATE SCHEMA](#f7ea7ef79efa639b)

<a id="b82ddec42cccf582"></a>
## CREATE VIEW

<a id="8156b664ba859ca8"></a>
### Function

It defines a view.

<a id="ab4dd444728198d7"></a>
### Syntax

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="1230be7fbb308ea9"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;view definition&gt; statement.

- One of the following privileges is required to create a view.
    - (CREATE VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
    - CREATE ANY VIEW ON DATABASE

- When using OR REPLACE clause, if a view already exists, then one of the following privileges is required to remove the existing view.
    - The owner of that view
    - CONTROL TABLE ON TABLE for that view.
    - (DROP VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
    - DROP ANY VIEW ON DATABASE

- One of the following privileges is required for all tables used in &lt;Query expression&gt;.
    - SELECT(columns) ON TABLE for all columns used in the statement among table columns
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

- The owner of the created view is determined as follows.
    - The owner of the schema to which the view belongs. 
    - If the schema to which the view belongs is PUBLIC, then it is the user who executed the statement.

- The owner of the view has the following privileges for the created view.
    - SELECT ON TABLE WITH GRANT OPTION 
    - INSERT ON TABLE WITH GRANT OPTION 
    - UPDATE ON TABLE WITH GRANT OPTION 
    - DELETE ON TABLE WITH GRANT OPTION 
    - TRIGGER ON TABLE 
    - LOCK ON TABLE WITH GRANT OPTION 
    - ALTER ON TABLE WITH GRANT OPTION

<a id="70e7de6dedc9519c"></a>
### Syntax Rules and Parameters

<a id="23f100afb06333d7"></a>
#### [ OR REPLACE ]

It replaces the existing view when a view already exists.

<a id="3757df9245114193"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - A view is created regardless of the validity of &lt;query expression&gt;.
- NO FORCE 
    - A view is created when &lt;Query expression&gt; is valid.
- The default value is NO FORCE.

<a id="2f0b072e962e6ec4"></a>
#### view_name

It is the view name to be created, and it should be a unique name within the schema.  
The schema to which the view belongs, such as schema_name.view_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the view name must be shorter than 128 bytes.

<a id="c79409e60c6cb20b"></a>
#### [ ( column_name [, ...] ) ]

It defines a column name which will configure the view.  
Each column name should be unique within the view.

The number of columns should be as same as the number of result columns in SELECT clause.

If the list of column names is omitted, the column names of SELECT clause in &lt;query expression&gt; are used.

<a id="7324ac3835650b68"></a>
##### AS &lt;query expression&gt;

It is the [SELECT](20-sql-references-h-z.md#94be89d31f330d61) query which will create a view.

&lt;query expression&gt; can not include the following variables.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE object

<a id="55ff061847a1e776"></a>
### Description

A view is the object which gave a name to the query, and it is used in the similar way of a table.

When executing a query including the view, that view is interpreted as the query included in the view definition. If the table referenced by the view is altered, as the following example, the asterisk (*) included in the view definition is automatically interpreted based on the altered table information.

```
gSQL> CREATE VIEW v1 AS SELECT * FROM t1;
gSQL> COMMIT;
gSQL> SELECT * FROM v1;

ID NAME     
-- ---------
 1 leekmo   
 2 mkkim    
 3 egonspace

3 rows selected.

gSQL> ALTER TABLE t1 ADD COLUMN ( dept_id  INTEGER,  addr  VARCHAR(1024) );
gSQL> COMMIT;

gSQL> select * from v1;

ID NAME      DEPT_ID ADDR
-- --------- ------- ----
 1 leekmo       null null
 2 mkkim        null null
 3 egonspace    null null

3 rows selected.
```

The view is affected if the view is created on the query including errors by using FORCE option, the tables referred by the view, or views are altered or deleted.

This information can be retrieved from INFORMATION_SCHEMA.VIEWS information.

- IS_COMPILED column
    - TRUE: The view is normally created. 
    - FALSE: The view is created having an error by using FORCE option.
- IS_AFFECTED column
    - TRUE : The referenced tables by a view or view is altered.
    - FALSE: After a view is created and compiled, the referenced tables or views are not altered.

The maximum number of creating views and the maximum number of columns to be created within a view is not limited. Therefore, they can be created as many as the storage space is available.

<a id="b014f9bab6924a97"></a>
### Examples

The following is an example of creating a view.

```
gSQL> CREATE VIEW v1 AS SELECT * FROM t1 WHERE dept_id = 101;

View created.
```

The following is an example of defining the column names when defining a view.

```
gSQL> CREATE VIEW v1 ( v_id, v_name )
          AS SELECT id, name FROM t1 WHERE dept_id = 101;

View created.
```

The following is an example of removing the existing view and creating a new view by using REPLACE option.

```
gSQL> CREATE OR REPLACE VIEW v1(id, name) 
             AS SELECT id, name FROM t1;

View created.
```

The following is an example of forcing to create a view by using FORCE option even when the referenced object by the view does not exist.

```
gSQL> CREATE FORCE VIEW v1 
          AS SELECT * FROM t1 WHERE dept_id = 101;

ERR-01000(16243): Warning: View created with compilation errors
ERR-42000(16040): table or view does not exist : 
    AS SELECT * FROM t1 WHERE dept_id = 101
                     *
ERROR at line 2:

View created.
```

<a id="e9d340f65b724bd2"></a>
### Compatibility

The SQL standard does not define the following clauses.

- [ OR REPLACE ] clause 
- [ FORCE | NO FORCE ] clause

**SQL standard compatibility**

<a id="7e3f99128fd60e4d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T131 | Recursive query | O |
| F751 | View CHECK enhancements | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F859 | Top-level &lt;fetch first clause&gt; in views | O |
| S081 | Subtables | X |

<a id="a19edd409df44a75"></a>
### For More Information

Refer to the followings.

- [DROP VIEW](#34f6b0ced02ffeeb)
- [ALTER VIEW](18-sql-references-a-b.md#766aa99e0f4c4f78)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)

<a id="d5d4c37681027dd4"></a>
## DECLARE cursor_name

<a id="6b67513d5e4fa782"></a>
### Function

It declares a cursor.

<a id="f7746408b9c9ba23"></a>
### Syntax

```
<declare cursor> ::=
    DECLARE cursor_name <cursor properties> { FOR | IS } <cursor specification>
    ;

<cursor properties> ::=
      [ <cursor sensitivity> ] [ <cursor scrollability>] ] CURSOR [ <cursor holdability> ] 
    | [ <odbc cursor type] CURSOR [ <cursor holdability> ] 

<cursor sensitivity> ::=
      INSENSITIVE
    | SENSITIVE
    | ASENSITIVE

<cursor scrollability> ::=
      NO SCROLL
    | SCROLL

<cursor holdability> ::=
      WITH HOLD
    | WITHOUT HOLD

<odbc cursor type> ::=
      STATIC
    | KEYSET

<cursor specification> ::=
      statement_name
    | <cursor query>  [ <updatability clause> ]

<cursor query> ::=
      <select statement>
    | <insert returning query statement>
    | <update returning query statement>
    | <delete returning query statement>

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="6ca67ba7b624ea45"></a>
### Invocation and Access Rules

The dynamic cursor which uses statement_name can be used in an embedded SQL.

An appropriate access privilege is required depending on &lt;cursor query&gt; types.  
For more information about the access privileges, refer to the followings.

- The access privilege of a [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement
- The access privilege of a [SELECT .. FOR UPDATE](20-sql-references-h-z.md#444c1075ec03498c) statement
- The access privilege of a [INSERT INTO name RETURNING](20-sql-references-h-z.md#6a81cf659499eec4) statement
- The access privilege of a [UPDATE name RETURNING](20-sql-references-h-z.md#926e12086d39dc4d) statement
- The access privilege of a [DELETE FROM name RETURNING](#5363553d184a14da) statement

<a id="5fb31d0cfbbb3577"></a>
### Syntax Rules and Parameters

<a id="061ee728202425e3"></a>
#### cursor_name

It is the cursor name to be declared.  
It should be a unique name within the session.  
The length of cursor name should be shorter than 128 bytes.

<a id="f10ab2cbb1396ffc"></a>
#### { FOR | IS }

Either FOR or IS is used as a syntax keyword in SQL standard.

<a id="9c316320701126a0"></a>
#### &lt;cursor properties&gt;

It defines the cursor properties.

- If &lt;cursor sensitivity&gt; is not specified, the default value is INSENSITIVE. 
- If &lt;cursor scrollability&gt; is not specified, the default value is NO SCROLL. 
- If &lt;cursor holdability&gt; is not specified, the default value is determined by &lt;cursor updatability&gt;.

<a id="255025501ebd3a25"></a>
#### updatable query

To use a cursor property such as SENSITIVE or FOR UPDATE, a query of the cursor should identify changes in rows of the base table, or it should be the updatable query which can acquire a lock on the row.

The updatable query should satisfy all of the following conditions.

- DISTINCT should not exist at the top level query.
    - (X) SELECT DISTINCT * FROM t1;
- GROUP BY, HAVING, aggregation function should not exist at the top level query.
    - (X) SELECT MAX(c1) FROM t1;
- It should not be a returning query. 
    - (X) DELETE FROM t1 RETURNING c1;
- Set operator should not exist. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2;
- At least one updatable column is required on the listed tables in FROM clause.
    - The columns of the tables, which are included in join operations and are not used in the cross join, are not the updatable columns.
        - FULL OUTER JOIN is not cross join.
        - NATURAL JOIN is not cross join.
        - If INNER JOIN uses USING phrase, it is not cross join.
    - The columns of the following tables are not the updatable columns.
        - Dictionary table, fixed table, performance view
    - The columns of the view are not updatable tables.

<a id="548c0df2c11f429a"></a>
#### &lt;cursor sensitivity&gt;

It determines whether the following data changes that affect the query results can be queried when operating the cursor.

- INSENSITIVE 
    - It can not detect the data updated during the cursor operation. 
- SENSITIVE 
    - &lt;cursor query&gt; should be an updatable query. 
    - It detects the updated and deleted data in the transaction as same as that of the cursor. 
    - It detects the data updated and deleted through COMMIT of other transactions. 
- ASENSITIVE 
    - INSENSITIVE or SENSITIVE is determined depending on the type of &lt;cursor query&gt;.
        - For the updatable query, it is SENSITIVE. 
        - For no updatable query, it is INSENSITIVE.
- If it is not specified, the default value is INSENSITIVE.

<a id="bdfbfffd79e68fe5"></a>
#### &lt;cursor scrollability&gt;

It specifies whether the result set of the cursor can be fetched sequentially or non-sequentially.

- NO SCROLL 
    - Only sequential FETCH (FETCH NEXT) is possible. 
- SCROLL 
    - Non-sequential FETCH is possible.
- If not specified, the default value is NO SCROLL.

<a id="57d6fe50f9e3959d"></a>
#### &lt;cursor holdability&gt;

It determines whether the cursor is maintained after the cursor is OPEN and the transaction is committed.

- WITH HOLD 
    - The cursor is maintained after the transaction is committed.
    - It can not be used together with FOR UPDATE statement.
    - It can not be used together with [INSERT INTO name RETURNING](20-sql-references-h-z.md#6a81cf659499eec4) statement. 
    - It can not be used together with [UPDATE name RETURNING](20-sql-references-h-z.md#926e12086d39dc4d) statement. 
    - It can not be used together with [DELETE FROM name RETURNING](#5363553d184a14da) statement.
    - It can not be used in the query including the global temporary table whose table commit action is ON COMMIT DELETE ROWS.

- WITHOUT HOLD 
    - When the transaction is committed or rolled back, the cursor is closed.

- Rollback and cursor
    - It closes a cursor included in a transaction when rolling back the transaction.
    - It closes a cursor created since the savepoint when rolling back up to the savepoint.

- If not specified, the default value of &lt;cursor holdability&gt; is determined by &lt;cursor updatability&gt;.
    - If it is FOR READ ONLY or &lt;cursor updatability&gt; is not specified, the default value is WITH HOLD. 
    - If it is used together with FOR UPDATE statement, the default value is WITHOUT HOLD.

<a id="64ac053ff87f7466"></a>
#### &lt;odbc cursor type&gt;

It is the cursor type in the ODBC standard, and it has the SCROLL property.

- STATIC CURSOR 
    - It is as same as INSENSITIVE SCROLL in SQL standard.
    - Non-sequential FETCH is possible. 
    - It is the static scroll cursor in the ODBC standard. 
- KEYSET CURSOR 
    - It is as same as ASENSITIVE SCROLL in SQL standard.
    - It is the keyset-driven scroll cursor in the ODBC standard.
    - The property of sensitivity is determined according to the following characteristics.

**Sensitivity according to FOR [UPDATE / READ ONLY] statement and the query type**

<a id="a293e2e6248ff3f9"></a>
| Updatability | Query type | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="76c92b9082b2de31"></a>
#### &lt;cursor specification&gt;

It defines a query which is a target of the cursor.  
If statement_name is used, a dynamic cursor whose query has not been defined is declared.  
If &lt;cursor query&gt; is used, a standing cursor whose query is defined is declared.

<a id="6383a295b5212cf8"></a>
#### statement_name

It is a statement_name to be referenced by the cursor, and it can be used in an embedded SQL.

statement_name should exist before performing &lt;declare cursor&gt; statement, and the SQL statement referenced by statement_name should be the query prepared by [PREPARE statement_name](20-sql-references-h-z.md#fe0135540bee6aee) statement.

If it is not a query, an error occurs when executing [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121) statement.

<a id="8bb0e559d3f3d79c"></a>
#### &lt;cursor query&gt;

For more information about available query types in the cursor, refer to the followings.

- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#444c1075ec03498c)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#6a81cf659499eec4)
- [UPDATE name RETURNING](20-sql-references-h-z.md#926e12086d39dc4d)
- [DELETE FROM name RETURNING](#5363553d184a14da)

<a id="5248d62d5c7550f5"></a>
#### &lt;updatability clause&gt;

It specifies whether to change rows by using the cursor.

- FOR READ ONLY 
    - It declares a read-only cursor.
- FOR UPDATE 
    - It declares a writable cursor. 
    - When opening the cursor, the x lock for the corresponding rows is acquired to prevent the change by other transactions until the transaction is completed. 
    - It can not be used together with WITH HOLD statement. 
    - &lt;cursor query&gt; should be an updatable query.
- If not specified, the default value is FOR READ ONLY.

<a id="b7d193fb1d2cb991"></a>
#### FOR UPDATE OF …

It lists the columns associated with the lock obtaining when OPENing the cursor.

- If it is the columns listed in FOR UPDATE OF statement
    - It should be an updatable column of the table listed in FROM clause of &lt;select statement&gt;.
    - It acquires the lock for the table of listed columns. 
- If only FOR UPDATE statement is used
    - It is the same meaning as listing all updatable columns of the table in FROM clause of &lt;select statement&gt;.
    - It acquires the lock for the table of all columns.

<a id="159d51baeb1a1da0"></a>
#### &lt;lock wait mode&gt;

It is used together with FOR UPDATE clause, and it specifies the lock acquisition method.

- WAIT 
    - It acquires the lock for all rows of the query result when OPENing the cursor.
    - It waits until acquiring the lock. 
- WAIT second 
    - It acquires the lock for all rows of the query result when OPENing the cursor.
    - An error occurs if the lock is not acquired within the specified time. 
    - The wait time is in seconds, and it can use the value between 0 and 1000000000.
- NOWAIT 
    - It acquires the lock for all rows of the query result when OPENing the cursor.
    - An error occurs if the lock is not immediately acquired.
- If not specified, the default value is WAIT.

<a id="cb364b21031bb6fd"></a>
### Description

When controlling the query property, using DECLARE CURSOR, OPEN, FETCH, CLOSE statements have the performance burden compared to using the cursor with the ODBC or JDBC statements. It is because using DECLARE CURSOR, OPEN, FETCH, CLOSE statements control the cursor of the server.

Before executing the query, the cursor property can be controlled by ODBC statement and JDBC statement. The SQL cursor property control method by DECLARE CURSOR statement, and cursor property control method by the ODBC standard and the JDBC standard are as follows.

<a id="d2d0f2c5050b9f4d"></a>
<table class="table column_count_4"><caption>Controlling the cursor property of ODBC/ JDBC</caption><thead><tr><th class="to_center to_middle"><div>Property</div></th><th class="to_center to_middle"><div>GOLDILOCKS 
cursor property</div></th><th class="to_center to_middle"><div>ODBC standard cursor property</div></th><th class="to_center to_middle"><div>JDBC standard cursor property</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>It can not be set.</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>It can not be set.</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

SQL cursor declaration corresponding to ODBC cursor type is as follows.

**SQL cursor declaration corresponding to ODBC cursor type**

<a id="11edf199728fd3b8"></a>
| ODBC cursor type | SQL cursor declaration |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

SQL cursor declaration corresponding to JDBC cursor type is as follows.

**SQL cursor declaration corresponding to JDBC cursor type**

<a id="aafa8aaf7e4b2bd2"></a>
| JDBC cursor type | SQL cursor declaration |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | KEYSET CURSOR |

<a id="af13854ac2d750f1"></a>
### Examples

The following is an example of declaring the cursor by using interactive SQL (gsql), and using it.

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

The following is an example of declaring KEYSET cursor, sequentially searching, then completing the transaction of UPDATE, DELETE statements, and searching for it in the reverse direction.

```
gSQL> DECLARE cur_keyset KEYSET CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_keyset;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH NEXT cur_keyset INTO :v_id, :v_data;

no rows fetched.

gSQL> UPDATE t1 SET data = 'new data_2' WHERE id = 2;

1 row updated.

gSQL> COMMIT;

Commit complete.

gSQL> DELETE FROM t1 WHERE id = 4;

1 row deleted.

gSQL> COMMIT;

Commit complete.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.


gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

no rows fetched.


gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA    
---- ----------
   2 new data_2

1 row fetched.

gSQL> FETCH PRIOR cur_keyset INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> CLOSE cur_keyset;

Cursor closed.
```

The following is an example of declaring SCROLL cursor, and using the cursor through the fetch orientation.

```
gSQL> DECLARE cur_scroll SCROLL CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_scroll;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;
V_ID V_DATA
---- ------
   5 data_5

1 row fetched.


gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.


gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.


gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.


gSQL> FETCH RELATIVE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.


gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> CLOSE cur_scroll;

Cursor closed.
```

<a id="d0d3842676123100"></a>
### Compatibility

&lt;declare cursor&gt; statement has the following differences compared to the SQL standard.

- In SQL standard, the default value of &lt;cursor sensitivity&gt; is ASENSITIVE, but in GOLDILOCKS, the default value is INSENSITIVE.
- The SQL standard does not cover the following &lt;odbc cursor type&gt;.
    - STATIC CURSOR 
    - KEYSET CURSOR 
- In SQL standard, the default value of &lt;cursor holdability&gt; is WITHOUT HOLD, but in GOLDILOCKS, the default value depends on &lt;cursor updatability&gt;.
- SQL standard can use only &lt;select statement&gt; as &lt;cursor query&gt;, but GOLDILOCKS can use the returning query as follows.
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#6a81cf659499eec4)
    - [UPDATE name RETURNING](20-sql-references-h-z.md#926e12086d39dc4d)
    - [DELETE FROM name RETURNING](#5363553d184a14da)
- In SQL standard, the default value of &lt;cursor updatability&gt; is determined by &lt;select statement&gt;, but in GOLDILOCKS the default value is FOR READ ONLY.
- In SQL standard, &lt;lock wait mode&gt; statement does not exist.

**SQL standard compatibility**

<a id="da8775d729f3543f"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F831 | Full cursor update | O |
| T231 | Sensitive cursors | O |
| F791 | Insensitive cursors | O |
| F431 | Read-only scrollable cursors | O |
| T471 | Result sets return value | X |
| T551 | Optional key words for default syntax | O |
| T111 | Updatable joins, unions, and columns | X |
| B031 | Basic dynamic SQL | O |

<a id="3ec2f545bd8e2331"></a>
### For More Information

Refer to the followings.

- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [FETCH cursor_name](#fcce02e780b87a86)
- [CLOSE cursor_name](#a7de81e9ff1d1b99)
- [PREPARE statement_name](20-sql-references-h-z.md#fe0135540bee6aee)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#444c1075ec03498c)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#6a81cf659499eec4)
- [UPDATE name RETURNING](20-sql-references-h-z.md#926e12086d39dc4d)
- [DELETE FROM name RETURNING](#5363553d184a14da)

<a id="66917622c0a305db"></a>
## DELETE FROM

<a id="0a6371392588d076"></a>
### Function

It deletes rows in a table.

<a id="66769f6249148b3d"></a>
### Syntax

```
<delete statement: searched> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
    ;

<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]

<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }
```

<a id="ce41f6a3bd00f7f8"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;delete statement: searched&gt;.

- (DELETE or CONTROL TABLE) ON TABLE for the table
- (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DELETE ANY TABLE ON DATABASE

<a id="a305ffa318576398"></a>
### Syntax Rules and Parameters

<a id="f7db74139b034251"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.  
It defines the schema to which the table belongs such as schema_name.table_name.   
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="633a6b2204f55513"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="f989ec6d4d22ec97"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
If WHERE condition is omitted, it deletes all rows.  
For more information about WHERE condition, refer to [where clause](20-sql-references-h-z.md#ef64355a6e859971) of [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement.

<a id="408029ea05e26f1f"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [offset limit clause](20-sql-references-h-z.md#ba0c692a791aafab) of [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement.

<a id="41db9c3e1746b593"></a>
#### &lt;fetch limit clause&gt;

The following two ways are used to specify the number of rows to be fetched.

- &lt;fetch first clause&gt;
    - It specifies the number of rows to be fetched. 
    - For more information, refer to [&lt;fetch first clause&gt;](20-sql-references-h-z.md#11fa929dab5b723e) of [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.
    - For more information, refer to [&lt;limit clause&gt;](20-sql-references-h-z.md#dbfd045ecbd16de8) of [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement.

<a id="d98fc65742b90167"></a>
### Description

<a id="18addbab8f6784bd"></a>
#### Differences among DELETE-related Statements

- [DELETE FROM](#66917622c0a305db)
    - It deletes multiple rows which satisfy conditions. 
    - e.g. DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#41d060c0d86599cc)
    - It deletes the row which the current cursor indicates.
    - e.g. DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#5363553d184a14da)
    - It deletes multiple rows which satisfy the conditions, and the deleted rows can be retrieved in the same way as [SELECT](20-sql-references-h-z.md#94be89d31f330d61) statement (API such as SQLFetch ()).
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#134bdaa5055cd709)
    - It deletes row equal to or less than one, and if one row is deleted, the value is obtained into the host variable of RETURNING INTO clause.
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="fb762d4e08d997ec"></a>
### Examples

The following is an example of DELETE statement.

```
gSQL> DELETE FROM t1 WHERE id > 3;

2 rows deleted.
```

The following is an example of skipping some rows (two rows) and deleting some rows (two rows) among the rows which satisfy the conditions by using &lt;result offset clause&gt; and &lt;fetch first clause&gt; clauses.

```
gSQL> DELETE FROM t1 OFFSET 2 FETCH 2;

2 rows deleted.


gSQL> SELECT * FROM t1 ORDER BY 1;

ID DATA  
-- ------
 1 data_1
 2 data_2
 5 data_5

3 rows selected.
```

<a id="937d3982dadeffe9"></a>
### Compatibility

The SQL standard does not define the following clauses of DELETE statement.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL standard compatibility**

<a id="844442f2e1288fab"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="d52dc0c726d68857"></a>
### For More Information

Refer to the followings.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#41d060c0d86599cc)
- [DELETE FROM name RETURNING](#5363553d184a14da)
- [DELETE FROM name RETURNING .. INTO](#134bdaa5055cd709)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)

<a id="5363553d184a14da"></a>
## DELETE FROM name RETURNING

<a id="a3bebb2383738d2a"></a>
### Function

It deletes rows of the table, and retrieves the deleted rows.

<a id="61d5c5bda6679014"></a>
### Syntax

```
<delete returning query statement> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning clause>
    ;

<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]

<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }

<returning clause> ::=
    { RETURN | RETURNING } { * | { <value expression> [ [AS] alias_name] } [, ...] }
```

<a id="38be0fe90b4af8be"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;delete returning query statement&gt;.

- One of the following privileges is required to perform DELETE statement.
    - (DELETE or CONTROL TABLE) ON TABLE for the table
    - (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - DELETE ANY TABLE ON DATABASE

- One of the following privileges is required for all the columns used in RETURNING clause.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause. 
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="1352fcde7289ab02"></a>
### Syntax Rules and Parameters

<a id="91af940760a7dc81"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="a7427b42a05756f7"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="f66af18397010c75"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="8cdf703875b0597e"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="9e662f2765eeb6cd"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="84d8cf8730199b01"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="bd79cb1d34b1257d"></a>
#### &lt;returning clause&gt;

It sets the deleted rows as a result set, and it specifies the columns to be searched from the set.

- RETURNING clause returns the rows deleted by DELETE statement as a result set.
- &lt;value expression&gt; 
    - It is as same as &lt;select list&gt; of SELECT statement, but it can not use aggregation.
- [[AS] alias_name] 
    - It can give the name to the value expression by using AS clause.

The keywords RETURNING and RETURN have the same meaning.

<a id="6b0d5ddcd45dba86"></a>
### Description

For more information, refer to [Differences among DELETE-related Statements](#18addbab8f6784bd).

<a id="ad33ff3141985257"></a>
### Examples

The following is an example of deleting rows which satisfy the condition, and searching for the deleted rows.

```
gSQL> DELETE FROM t1 WHERE id > 3 RETURNING *;

ID DATA  
-- ------
 4 data_4
 5 data_5

2 rows deleted.
```

The following is an example of querying information of the deleted rows by using operation in RETURNING clause.

```
gSQL> DELETE FROM t1 
             WHERE id > 3 
             RETURNING 'ID: ' || id || ', DATA: ' || data AS id_data;

ID_DATA            
-------------------
ID: 4, DATA: data_4
ID: 5, DATA: data_5

2 rows deleted.
```

<a id="d44170c15716c83b"></a>
### Compatibility

The SQL standard does not cover &lt;delete returning query statement&gt;.

<a id="e677f9aaf45b4f19"></a>
### For More Information

Refer to the followings.

- [DELETE FROM](#66917622c0a305db)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#41d060c0d86599cc)
- [DELETE FROM name RETURNING .. INTO](#134bdaa5055cd709)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)

<a id="134bdaa5055cd709"></a>
## DELETE FROM name RETURNING .. INTO

<a id="67f5242b8be9d5a5"></a>
### Function

It deletes a single row from the table, and the value of the deleted row is obtained into the host variable.

<a id="576c24e2df19e603"></a>
### Syntax

```
<delete returning query statement> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning into clause>
    ;

<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]


<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>


<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]


<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }


<returning into clause> ::=
    { RETURN | RETURNING } { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO variable_name [, ...]
```

<a id="431d8675798f2b47"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;delete returning into statement&gt;.

- One of the following privileges is required to perform DELETE statement.
    - (DELETE or CONTROL TABLE) ON TABLE for the table
    - (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - DELETE ANY TABLE ON DATABASE

- One of the following privileges is required for all columns used in RETURNING clause.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="804ce4030a08b1ba"></a>
### Syntax Rules and Parameters

<a id="503a9110a18b7720"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="5d61a5c52f260f70"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="d65ca184017cc1b7"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="9e803a7ce42edda4"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="025fb7d29b236272"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="b0b79356a36bf482"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#66917622c0a305db) statement.

<a id="c0ddf00b87e052d9"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - For more information, refer to &lt;returning clause&gt; of [DELETE FROM name RETURNING](#5363553d184a14da) statement.
- INTO variable_name [, ...]
    - The number of variables specified in INTO clause should be equal to the number of the expressions specified in RETURNING clause.

<a id="f031e62fa4d52a91"></a>
### Description

The number of rows to be deleted should be equal to or less than one.  
If two or more rows are deleted, then an error occurs.

For more information, refer to [Differences among DELETE-related Statements](#18addbab8f6784bd).

<a id="99bfb530dd132d53"></a>
### Example

The following is an example of deleting rows and obtaining the value of deleted rows into the host variable in an interactive SQL (gsql).

```
gSQL> \var v_id    INTEGER
gSQL> \var v_data  VARCHAR(128)

gSQL> DELETE FROM t1 WHERE id = 3 RETURNING id, data INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row deleted.
```

<a id="ac64153512c74a42"></a>
### Compatibility

The SQL standard does not cover &lt;delete returning into statement&gt;.

<a id="a2034e054139bc87"></a>
### For More Information

Refer to the followings.

- [DELETE FROM](#66917622c0a305db)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#41d060c0d86599cc)
- [DELETE FROM name RETURNING](#5363553d184a14da)
- [SELECT](20-sql-references-h-z.md#94be89d31f330d61)

<a id="41d060c0d86599cc"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="28163f82cd15a235"></a>
### Function

It deletes a single row which the cursor indicates.

<a id="d831189e134016e8"></a>
### Syntax

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="3d6a296bad443d88"></a>
### Invocation and Access Rules

The privilege to perform [DELETE FROM](#66917622c0a305db) statement is required to perform &lt;delete statement: positioned&gt;.

<a id="973892e828cd0e25"></a>
### Syntax Rules and Parameters

<a id="27e6f150a417af16"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="725d355a7b327585"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="2e20898925b2a401"></a>
#### cursor_name

The cursor corresponding to cursor_name should satisfy the following conditions.

- The cursor should be OPEN. (Refer to [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121).) 
- Fetched rows by using the cursor should exist. (Refer to [FETCH cursor_name](#fcce02e780b87a86).) 
- The query used for the cursor should identify table_name. (Refer to [DECLARE cursor_name](#d5d4c37681027dd4).) 
- The cursor should be updatable for table_name. (Refer to [DECLARE cursor_name](#d5d4c37681027dd4).)

<a id="13359144f2128a11"></a>
### Description

For more information, refer to [Differences among DELETE-related Statements](#18addbab8f6784bd).

<a id="9c938504f87f2453"></a>
### Example

The following is an example of declaring the FOR UPDATE cursor, and deleting rows by using the cursor in interactive SQL (gsql).

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1 FOR UPDATE;

Cursor declared.


gSQL> OPEN cur1;

Cursor is open.


gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> DELETE FROM t1 WHERE CURRENT OF cur1;

1 row deleted.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> DELETE FROM t1 WHERE CURRENT OF cur1;

1 row deleted.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.

gSQL> SELECT id, data FROM t1 ORDER BY 1;

ID DATA  
-- ------
 1 data_1
 3 data_3
 5 data_5

3 rows selected.
```

<a id="df72e6c5dffaa99e"></a>
### Compatibility

**SQL standard compatibility**

<a id="798b5b0005240a76"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="d82f3865e203f15e"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [FETCH cursor_name](#fcce02e780b87a86)
- [DELETE FROM](#66917622c0a305db)
- [DELETE FROM name RETURNING](#5363553d184a14da)
- [DELETE FROM name RETURNING .. INTO](#134bdaa5055cd709)

<a id="74a07e0949274daf"></a>
## DROP AUDIT POLICY

<a id="13e250664e1702de"></a>
### Function

It drops an audit policy.

<a id="f04b07f4512570a7"></a>
### Syntax

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="66c1ebe5e9a24d9d"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;drop audit policy statement&gt;.

<a id="ef4465af17f807ca"></a>
### Syntax Rules and Parameters

<a id="6d478781e82b92a1"></a>
#### IF EXISTS

An error does not occur even when a policy_name does not exist.

<a id="e845e34d00fcc311"></a>
#### policy_name

It is the name of an audit policy object to be dropped.

<a id="3e902c47b4b746d7"></a>
### Description

The audit policy object which is already activated can not be dropped. In this case, the audit policy should be deactivated by using NOAUDIT POLICY statement.

<a id="e6cb7e00c6e7261e"></a>
### Examples

The following is an example of dropping an audit policy.

```
DROP AUDIT POLICY policy_table;
```

<a id="2c0c5196997d35b9"></a>
### Compatibility

In the SQL standard, an audit policy does not exist.

<a id="a017bbeadc4731eb"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#4f95ec95d004a1b2)
    - [DROP AUDIT POLICY](#74a07e0949274daf)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#53347c6092b6e054)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](18-sql-references-a-b.md#9289801d878dbdc2)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#1d87c2f21b970bb9)

- Retrieving audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#c239152842953eb8)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#783e2ba71672a2fa)

<a id="76a15fea6a02da13"></a>
## DROP CLUSTER GROUP

<a id="7fb1ac4c89dbb467"></a>
### Function

It drops a cluster group from a cluster system.

<a id="5b3a17c57b29efe2"></a>
### Syntax

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="9d17bfa3539a9127"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  
ADMINISTRATION ON DATABASE privilege is required to perform &lt;drop cluster group statement&gt;.

<a id="d635f75ff758bab3"></a>
### Syntax Rules and Parameters

<a id="9daa0c8b5a39b875"></a>
#### [IF EXISTS]

An error does not occur even when a cluster group does not exist.

<a id="219b76a785861427"></a>
#### group_name

It is the name of a cluster group.  
A cluster group without any shard can be dropped.

<a id="680a4333209dbf61"></a>
### Description

A cluster group can be dropped only when dropping the cluster group does not cause the data loss.  
However, an error may occur when trying to drop a group including the global coordinator.

<a id="ae6f242ca1459a35"></a>
### Examples

The following is an example of dropping a cluster group.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="124803bbdef4fc4f"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="ded28d8080e8f2c7"></a>
### For More Information

Refer to [CREATE CLUSTER GROUP](#3f7a6957233a40f7).

<a id="351e9009d382090f"></a>
## DROP CLUSTER LOCATION

<a id="b18320dc4281fd45"></a>
### Function

It drops the access information of a cluster member.

<a id="36be94e7811ec996"></a>
### Syntax

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="76ab9b9e4bff02b7"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  
ADMINISTRATION ON DATABASE privilege is required to perform &lt;drop cluster location statement&gt;.

<a id="397c88dad4fc1171"></a>
### Syntax Rules and Parameters

<a id="360ba8bb567a48a3"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should exist in a registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="e02eaa32ba31e3de"></a>
### Description

Generally, the information of the cluster location is automatically created by using the connection information provided when creating the cluster group or adding the cluster member. The created information is deleted together when deleting the cluster member and the cluster group.

If the access information of the cluster location is modified, then the connection information can be modified by using [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#68afa63d36875d46) without deleting or recreating the cluster member.

<a id="a254a7c8652a2a79"></a>
### Example

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="060d8db1ecd38ace"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="0860a25ba7d96153"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER LOCATION](#67ef6e090f63d08d)
- [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#68afa63d36875d46)

<a id="fcb6f064d90f791d"></a>
## DROP INDEX

<a id="22f72e8d04631f30"></a>
### Function

It drops an index.

<a id="955d95d2b59f71e2"></a>
### Syntax

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="c885e9f7fca6b8b3"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs
- (DROP INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- DROP ANY INDEX ON DATABASE

<a id="30c6553131bee51f"></a>
### Syntax Rules and Parameters

<a id="d26503f82fca16df"></a>
#### IF EXISTS

Even when the index does not exist, an error does not occur.

<a id="61989bf33e6d52b5"></a>
#### index_name

It is the index name to be dropped.  
It can define schema to which the index belongs such as schema_name.index_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

The indexes created for UNIQUE constraint, PRIMARY KEY constraint can not be dropped.  
To drop the indexes created for the constraints above, the constraints should be removed through [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#5dc66d99183e1a21) statement.

<a id="24634b175f68379b"></a>
### Description

Data Definition Language (DDL) statement such as DROP INDEX can be rolled back if it is before when the transaction is committed.

<a id="960a0681caac494a"></a>
### Examples

The following is an example of dropping an index.

```
gSQL> DROP INDEX idx_t1_id;

Index dropped.
```

The following is an example of preventing an error even when the index does not exist by using IF EXISTS statement.

```
gSQL> DROP INDEX IF EXISTS not_exist_index;

Index dropped.
```

<a id="1ff1dd66f4c6120f"></a>
### Compatibility

The SQL standard does not cover the concepts of the index.

<a id="de57faeee8f23b1e"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](#d54e994b20c1da1b)
- [DROP TABLE](#99cce8728f930322)
- [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#5dc66d99183e1a21)

<a id="235532c683a06591"></a>
## DROP PROFILE

<a id="1c0e6bde14c67214"></a>
### Function

It drops a profile.

<a id="7840075f77f0f21d"></a>
### Syntax

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="42af8fe514b9c4a8"></a>
### Invocation and Access Rules

DROP PROFILE ON DATABASE privilege is required to perform &lt;drop profile statement&gt;.

<a id="43496aa2f534f46a"></a>
### Syntax Rules and Parameters

<a id="4587307e0fecddc7"></a>
#### IF EXISTS

Even when the profile does not exist, an error does not occur.

<a id="c4bc2305a68591de"></a>
#### profile_name

It specifies the profile name to be dropped.  
It can not drop the DEFAULT profile.

<a id="de9b474510dade76"></a>
#### CASCADE

If the profile has already been assigned to users, CASCADE clause should be explicitly specified to drop the profile.  
The profile which is assigned to users and to be dropped is changed to DEFAULT profile.

<a id="ed080590b82257ee"></a>
### Example

The following is an example of dropping a profile by using CASCADE statement.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="f9b44763b7fb861b"></a>
### Compatibility

The SQL standard does not cover the concepts of the profile.

<a id="06084d303e3d7b65"></a>
### For More Information

Refer to the followings.

- [CREATE PROFILE](#fa2854762beb7024)
- [ALTER PROFILE](18-sql-references-a-b.md#328cee336239afe4)

<a id="3057681bb2ca4423"></a>
## DROP SCHEMA

<a id="44bcfd5d571655cd"></a>
### Function

It drops a schema.

<a id="cee1151f253cd522"></a>
### Syntax

```
<drop schema statement> ::=
    DROP SCHEMA [ IF EXISTS ] schema_name
        [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="98205ed66b456880"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop schema statement&gt;.

- The owner of that schema
- CONTROL SCHEMA ON SCHEMA for the schema
- DROP SCHEMA ON DATABASE

<a id="b02bf905e3b20631"></a>
### Syntax Rules and Parameters

<a id="afffce00b3f7ed1e"></a>
#### IF EXISTS

Even when the schema does not exist, an error does not occur.

<a id="1e5a5f03b25e065b"></a>
#### schema_name

It is the schema name to be dropped.  
However, it can not drop the built-in schema such as "DICTIONARY_SCHEMA", "INFORMATION_SCHEMA" and "PUBLIC" which are automatically created when creating the database.

<a id="9dcc23905a29fc4a"></a>
#### &lt;drop behavior&gt;

- When it is RESTRICT 
    - Objects should not exist within the schema.
- When it is CASCADE 
    - It drops all objects in the schema together.
- When it is omitted, the default value is RESTRICT.

<a id="c07758ba0bda0611"></a>
### Description

Data Definition Language (DDL) statement such as DROP SCHEMA can be rolled back if it is before when the transaction is committed. In this case, recycle bin objects which are included in the schema to be dropped are also dropped.

<a id="4f0c4347e77eac3a"></a>
### Examples

The following is an example of dropping a schema and all objects which exist within the schema.

```
gSQL> DROP SCHEMA s1 CASCADE;

Schema dropped.
```

The following is an example of preventing an error even when the schema does not exist by using IF EXISTS statement.

```
gSQL> DROP SCHEMA IF EXISTS not_exist_schema;

Schema dropped.
```

<a id="6a74c9feedda0c7c"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="c0fe23b2cfa7f305"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="ec6c972aca4b547f"></a>
### For More Information

Refer to [CREATE SCHEMA](#f7ea7ef79efa639b).

<a id="61c1cea96080ef41"></a>
## DROP SEQUENCE

<a id="fdc612fa87aba805"></a>
### Function

It drops a sequence.

<a id="184237877e0c4165"></a>
### Syntax

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="21a1fade9e0d5d43"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop sequence generator statement&gt;.

- The owner of that sequence
- (DROP SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence belongs
- DROP ANY SEQUENCE ON DATABASE

<a id="9a11ebde74db7bac"></a>
### Syntax Rules and Parameters

<a id="5295e567b1b1915b"></a>
#### IF EXISTS

Even when the sequence does not exist, an error does not occur.

<a id="58f8b37748e09c2b"></a>
#### sequence_name

It is the sequence name to be dropped.  
It can define schema to which the sequence belongs such as schema_name.sequence_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="290b96a171db118c"></a>
### Description

Data Definition Language (DDL) statement such as DROP SEQUENCE can be rolled back if it is before when the transaction is committed.

<a id="70c2ec3822e004c8"></a>
### Examples

The following is an example of dropping a sequence.

```
gSQL> DROP SEQUENCE seq1;

Sequence dropped.
```

The following is an example of preventing an error even when the sequence does not exist by using IF EXISTS statement.

```
gSQL> DROP SEQUENCE invalid_sequence;

ERR-42000(16044): sequence does not exist : 
DROP SEQUENCE invalid_sequence
              *
ERROR at line 1:


gSQL> DROP SEQUENCE IF EXISTS invalid_sequence;

Sequence dropped.
```

<a id="2c8af7397f0f63be"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="ae37f0fdb9752a84"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="7e1317ecde04e57e"></a>
### For More Information

Refer to the followings.

- [CREATE SEQUENCE](#11cfe1f314df4ce6)
- [ALTER SEQUENCE](18-sql-references-a-b.md#c19ab51ee6e2aea4)

<a id="b3cdccf874ce9683"></a>
## DROP SYNONYM

<a id="cb1b6e06c6241db1"></a>
### Function

It drops a synonym.

<a id="b7ad6a741338c379"></a>
### Syntax

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="f5f8f88dfd9f8adb"></a>
### Invocation and Access Rules

DROP PUBLIC SYNONYM ON DATABASE privilege is required to drop a public synonym by specifying PUBLIC.

One of the following privileges is required to drop a private synonym.

- The owner of that synonym
- (DROP SYNONYM or CONTROL SCHEMA) ON SCHEMA for the schema to which the synonym belongs
- DROP ANY SYNONYM ON DATABASE

<a id="c1c9a4f2adba5185"></a>
### Syntax Rules and Parameters

<a id="cc399cde953664e5"></a>
#### [ PUBLIC ]

It is specified when dropping the public synonym.  
If this clause is omitted, the private synonym is dropped.

<a id="24a7799260d27938"></a>
#### IF EXISTS

Even when the synonym does not exist, an error does not occur.

<a id="19ed358276a795ae"></a>
#### synonym_name

It is the synonym name to be dropped.  
It can define schema to which the synonym belongs such as schema_name.synonym_name and if schema_name is omitted, the default schema name of the user performing the statement is used.  
If PUBLIC is explicitly specified, the schema name can not be specified.

<a id="af4f4d1038cecbfb"></a>
### Description

Data Definition Language (DDL) statement such as DROP SYNONYM can be rolled back if it is before when the transaction is committed.

<a id="06fb79a78f627584"></a>
### Examples

The following is an example of dropping a private synonym.

```
gSQL> DROP SYNONYM MyEmp;

Synonym dropped.
```

The following is an example of dropping a public synonym.

```
gSQL> DROP PUBLIC SYNONYM MainEmp;

Synonym dropped.
```

<a id="b465e10ff9eb7777"></a>
### Compatibility

The SQL standard does not define DROP SYNONYM statement.

<a id="c7111db820b996c1"></a>
### For More Information

Refer to [CREATE SYNONYM](#fbdbe1b73f80a473).

<a id="99cce8728f930322"></a>
## DROP TABLE

<a id="60b9a2749cfaa1c1"></a>
### Function

It drops a table.

> If the recycle bin feature is activated, the table is not completely dropped but it is stored in the recycle bin.

<a id="eb9aa1a2a109cd06"></a>
### Syntax

```
<drop table statement> ::=
    DROP TABLE [ IF EXISTS ] table_name
    [ <drop behavior> ]
    [ PURGE ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="ed3aef8f3192e7a6"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table statement&gt;.

- The owner of that table 
- CONTROL TABLE ON TABLE for that table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="1341441cf0c0fff1"></a>
### Syntax Rules and Parameters

<a id="5d4fd015cfbd9870"></a>
#### IF EXISTS

Even when the table does not exist, an error does not occur.

<a id="5481ea95e09b0c32"></a>
#### table_name

It is the table name to be dropped.  
It can define schema to which the table belongs such as schema_name.table_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

The following tables which are automatically created during creating the database, can not be dropped.

- The tables in "DEFINITION_SCHEMA" schema
- The tables in "FIXED_TABLE_SCHEMA" schema

It also drops constraints and indexes created in the table.

<a id="6c67e3c1de94ab89"></a>
#### drop behavior

Currently, both RESTRICT and CASCADE are operated same.  
When it is omitted, the default value is RESTRICT.

<a id="8f1ba1c6448e39b0"></a>
#### purge

It immediately drops a table instead of storing it in the recycle bin even when the recycle bin feature is activated.

<a id="818d67cb543d2887"></a>
### Description

Data Definition Language (DDL) statement such as DROP TABLE can be rolled back if it is before when the transaction is committed.

<a id="7b7faca388a5068d"></a>
### Examples

The following is an example of dropping an ordinary table.

```
gSQL> DROP TABLE region;

Table dropped.
```

The following is an example of preventing an error even when the table does not exist by using IF EXISTS statement.

```
gSQL> DROP TABLE IF EXISTS invalid_table;

Table dropped.
```

The following is an example of rolling back the dropped table.

```
gSQL> SELECT r_regionkey, r_name FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     
          3 EUROPE                   
          4 MIDDLE EAST              

5 rows selected.


gSQL> DROP TABLE region;

Table dropped.


gSQL> SELECT r_regionkey, r_name FROM region;

ERR-42000(16040): table or view does not exist : 
SELECT r_regionkey, r_name FROM region
                                *
ERROR at line 1:


gSQL> ROLLBACK;

Rollback complete.


gSQL> SELECT r_regionkey, r_name FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     
          3 EUROPE                   
          4 MIDDLE EAST              

5 rows selected.
```

<a id="ec6db618649d8560"></a>
### Compatibility

The SQL standard does not define the following clauses.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL standard compatibility**

<a id="fff8936ad28e448d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="e6d5dda811bec990"></a>
### For More Information

Refer to [CREATE TABLE](#4c3b06d433f75b3d).

<a id="a9171e5695f3e4e0"></a>
## DROP TABLESPACE

<a id="c88146188f246e6a"></a>
### Function

It drops a tablespace.

<a id="91552f805551fa36"></a>
### Syntax

```
<drop tablespace statement> ::=
    DROP TABLESPACE [ IF EXISTS ] tablespace_name
        [ INCLUDING CONTENTS ]
        [ { AND | KEEP } DATAFILES ]
        [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="01c067cd7db8963d"></a>
### Invocation and Access Rules

DROP TABLESPACE ON DATABASE privilege is required to perform &lt;drop tablespace definition&gt;.

<a id="804ab9cf5304faca"></a>
### Syntax Rules and Parameters

<a id="3f26cff91ea20ad7"></a>
#### IF EXISTS

Even when the tablespace does not exist, an error does not occur.

<a id="3f779d013ed1e315"></a>
#### tablespace_name

It is the tablespace name to be dropped.  

The following system tablespaces which are automatically created during creating the database, can not be dropped.

- DICTIONARY_TBS: system tablespace for dictionary management
- MEM_UNDO_TBS: system tablespace for default undo tablespace
- MEM_DATA_TBS: system tablespace for default user data tablespace
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> If tablespace_name was used as a default tablespace of a user, the space for the objects can not be allocated after dropping the tablespace.  
> After dropping the tablespace, the default tablespace should be changed by using [ALTER USER](18-sql-references-a-b.md#270d91f0c78160b6) statement.

<a id="47eb24b3ea7ddc1e"></a>
#### INCLUDING CONTENTS

It drops objects (table, index, key constraint) which belong to the tablespace. If the index or key constraint which refers to the table which belongs to the tablespace exists outside of the tablespace, then it is also dropped.

If INCLUDING CONTENTS clause is not used, then any object which belongs to the tablespace should not exist.

<a id="222c7beaf5e686bb"></a>
#### [ { AND | KEEP } DATAFILES ]

It specifies whether to drop the datafiles which configure the tablespace together.  
The datafiles are not in the memory temporary tablespace, so the clause is ignored.

- AND DATAFILES 
    - It drops the datafiles together. 
- KEEP DATAFILES 
    - It does not drop the datafiles, but keeps them.
- If it is not specified, the default value is KEEP DATAFILES.

<a id="8e0fe3ce614da839"></a>
#### drop behavior

Currently, both RESTRICT and CASCADE are operated same.  
When it is omitted, the default value is RESTRICT.

<a id="310a0f7ee5347cd6"></a>
### Description

Unlike other Data Definition Language (DDL), DROP TABLESPACE statement can not be rolled back and the executed transaction is automatically committed. In this case, recycle bin objects which are included in the tablespace to be dropped are also dropped.

<a id="e50e6c746aa4ca02"></a>
### Examples

The following is an example of dropping a tablespace together with all objects in the tablespace and datafiles which configure the tablespace.

```
gSQL> DROP TABLESPACE space1 INCLUDING CONTENTS AND DATAFILES CASCADE CONSTRAINTS;

Tablespace dropped.
```

The following is an example of preventing an error even when the tablespace does not exist by using IF EXISTS statement.

```
gSQL> DROP TABLESPACE IF EXISTS not_exist_tablespace;

Tablespace dropped.
```

<a id="cce6e19eb1a49acf"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="880acf8473704c45"></a>
### For More Information

Refer to the followings.

- [CREATE MEMORY DATA TABLESPACE](#9831f431f182fce6)
- [CREATE MEMORY TEMPORARY TABLESPACE](#504552ef753c144a)
- [ALTER TABLESPACE](18-sql-references-a-b.md#b3042281f058c1cb)

<a id="f64464bae416acc8"></a>
## DROP USER

<a id="3b5fb3ed420259af"></a>
### Function

It drops a database user.

<a id="ee56562495093ca9"></a>
### Syntax

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="2826343a74ad32cd"></a>
### Invocation and Access Rules

DROP USER ON DATABASE privilege is required to perform &lt;drop user statement&gt;.

> The schema owned by user_identifier should not exist.  
> For more information about dropping the schema, refer to [DROP SCHEMA](#3057681bb2ca4423).

<a id="99a2e8328ff785b5"></a>
### Syntax Rules and Parameters

<a id="b269906ba987641a"></a>
#### IF EXISTS

Even when the user does not exist, an error does not occur.

<a id="d7436c127b22a107"></a>
#### user_identifier

It is the database username to be dropped.  
However, the user which is automatically created during creating the database such as "SYS", can not be dropped.

It does not drop the object which is created by user_identifier but is not an owner as follows.

- Role 
- Tablespace

<a id="7fe0520e14815a66"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - There should not be the following user owned SQL schema objects.
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint 
- CASCADE 
    - It drops all the following user owned SQL schema objects.
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint 
- When it is omitted, the default value is RESTRICT.

> The relationship between user and schema in other DBMS   
> 
> 
> - Oracle
>     - User : schema = 1 : 1.
>     - When CASCADE, the schema is also dropped. 
> 
> 
> 
> - DB2 
>     - It is as same as the OS user.
>     - The separate SQL statements which create or delete a user do not exist.
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N. 
>     - It does not support CASCADE option, and a user can be dropped after dropping all the objects owned by the user and all the privileges granted to other users. 
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1.
>     - User is a subordinate object of database (schema), and it does not support CASCADE option.
> 

<a id="8a22875fc6dfda6d"></a>
### Description

In GOLDILOCKS, relationship between the user and the schema is 1 : N. A user does not own a schema, or the user can have multiple schemas.

To drop a user, all schema owned by the user should be dropped. In this case, recycle bin objects of the user to be dropped are also dropped.

<a id="895948cdffbe02ea"></a>
### Examples

The following is an example of dropping all schema owned by the user and then dropping the user.

```
gSQL> DROP SCHEMA u1 CASCADE;

Schema dropped.

gSQL> DROP USER u1 CASCADE;

User dropped.
```

The following is an example of preventing an error even when the user does not exist by using IF EXISTS statement.

```
gSQL> DROP USER IF EXISTS not_exist_user;

User dropped.
```

<a id="0f0a4cc773d9085c"></a>
### Compatibility

SQL standard cover the concepts of the user, but they do not define the SQL statements related to creating or dropping a user.

<a id="bd78d6e59748deff"></a>
### For More Information

Refer to the followings.

- [CREATE USER](#67d566d84adb0376)
- [ALTER USER](18-sql-references-a-b.md#270d91f0c78160b6)
- [DROP SCHEMA](#3057681bb2ca4423)

<a id="34f6b0ced02ffeeb"></a>
## DROP VIEW

<a id="956b22d50a978d86"></a>
### Function

It drops a view.

<a id="b847c718bb95c6e9"></a>
### Syntax

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="ded623cf2f100e6d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop view statement&gt;.

- The owner of that view 
- CONTROL TABLE ON TABLE for that view
- (DROP VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
- DROP ANY VIEW ON DATABASE

<a id="1a01505fd9dc2243"></a>
### Syntax Rules and Parameters

<a id="98bbbbc5c1e62d58"></a>
#### IF EXISTS

Even when the view does not exist, an error does not occur.

<a id="4fed130f7515b708"></a>
#### view_name

It is the view name to be dropped.  
The schema to which the table belongs, such as schema_name.view_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3c54492cfea63b6c"></a>
### Description

Data Definition Language (DDL) statement such as DROP VIEW can be rolled back if it is before when the transaction is committed.

<a id="3d72b260ba3f35ef"></a>
### Examples

The following is an example of dropping a view.

```
gSQL> DROP VIEW v1;

View dropped.
```

The following is an example of preventing an error even when the view does not exist by using IF EXISTS statement.

```
gSQL> DROP VIEW IF EXISTS not_exist_view;

View dropped.
```

<a id="d63c1c8eea4f4aa3"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="968b72283e27adfe"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="1c67fdc02814ece5"></a>
### For More Information

Refer to the followings.

- [CREATE VIEW](#b82ddec42cccf582)
- [ALTER VIEW](18-sql-references-a-b.md#766aa99e0f4c4f78)

<a id="512d2b2288401131"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="e51dbe97561ab6c7"></a>
### Function

It executes a dynamic SQL statement which was not defined when writing a program.

<a id="2c86a40ade183f99"></a>
### Syntax

```
<execute immediate statement> ::=
    EXECUTE IMMEDIATE <SQL statement variable>
    ;

<SQL statement variable> ::=
      variable_name
    | 'sql statement'
    | "sql statement"
    | sql statement
```

<a id="0badb4aef60c5e78"></a>
### Invocation and Access Rules

It can be used in an embedded SQL.  
An appropriate privilege according to the type of a dynamic SQL statement is required.

<a id="ff7936d79f3fcaee"></a>
### Syntax Rules and Parameters

<a id="303dde0a64453f2e"></a>
#### &lt;SQL statement variable&gt;

The dynamic SQL statement referenced by &lt;SQL statement variable&gt; can not use a host variable (:var) or parameter marker (?).

The following four types of &lt;SQL statement variable&gt; can be used.

- variable_name: It is a variable in which an SQL statement is stored. 
- 'sql statement': It is an SQL statement which is enclosed with a single quote ('). 
- "sql statement": It is an SQL statement which is enclosed with double quotes ("). 
- sql statement: It is an SQL statement without quote.

The single quote (') is used twice as follows to represent string data within a single-quoted string.

```
{
    ...
    EXEC SQL EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

If the SQL statement is a query including a query result, it is successfully executed, but the result can not be obtained.

<a id="c2c109a9438e65de"></a>
#### variable_name

The type corresponding to the variable_name should be a character string.  
The dynamic SQL statement defined in the variable_name should be valid.

<a id="7530240eb7774252"></a>
#### sql statement

The dynamic SQL statement defined in the sql statement should be valid.

<a id="e14efe5b69dffa22"></a>
### Description

EXECUTE IMMEDIATE 'sql_string' statement can be used as the non-query SQL without a host variable in dynamic embedded SQL application. It is appropriate to execute DDL, DML as one-off because it does not require separate preparation procedure.

For more information, refer to  [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#b15442af59f50813).

<a id="4e004bc080935710"></a>
### Example

The following is an example of using EXECUTE IMMEDIATE 'sql_string' in the embedded SQL source code.

```
{
    ...
    sprintf(sSqlStmt, "INSERT INTO EMP_RND\n"
            "SELECT *\n"
            "FROM   EMP\n"
            "WHERE  JOB = 'RND'\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    ...
}
```

The full source code in which EXECUTE IMMEDIATE 'sql_string' was used can be viewed in [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#fe744f57cdd760c6).

<a id="57228a5ec000d10b"></a>
### Compatibility

**SQL standard compatibility**

<a id="28473eb9e2a311f0"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="3137f7b288800dd6"></a>
### For More Information

Refer to the followings.

- [PREPARE statement_name](20-sql-references-h-z.md#fe0135540bee6aee)
- [EXECUTE statement_name](#e4c1bc28bb314674)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#b15442af59f50813)

<a id="e4c1bc28bb314674"></a>
## EXECUTE statement_name

<a id="31dccc3b37c3c043"></a>
### Function

It executes the prepared statement.

<a id="9c020237d3c1488e"></a>
### Syntax

```
<execute statement> ::=
    EXECUTE statement_name [ <parameter using clause> ] [ <result into clause> ]
    ;

<parameter using clause> ::=
      <using parameter arguments>

<using parameter arguments> ::=
    USING variable_name [, ...]

<result into clause> ::=
      <into result arguments>

<into result arguments> ::=
    INTO variable_name [, ...]
```

<a id="11b1f432c1a8bf78"></a>
### Invocation and Access Rules

It can be used in an embedded SQL.  
An appropriate privilege according to the type of a dynamic SQL statement is required.

<a id="596c7e3f373a0351"></a>
### Syntax Rules and Parameters

<a id="7d8183a585bc621f"></a>
#### statement_name

It is the name of a prepared statement.  
Statement_name should be prepared by using [PREPARE statement_name](20-sql-references-h-z.md#fe0135540bee6aee).

If the dynamic SQL statement referenced by statement_name contains a dynamic parameter, &lt;parameter using clause&gt; should explicitly be specified.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 > ?';
    EXEC SQL EXECUTE stmt1 USING :sValue;
    ...
}
```

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT COUNT(*) INTO :v1 FROM t1';
    EXEC SQL EXECUTE stmt1 USING :sValue;
    ...
}
```

If the dynamic SQL statement referenced by statement_name is a query or a stored function including the result, &lt;result into clause&gt; should explicitly be specified.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT COUNT(*) FROM t1';
    EXEC SQL EXECUTE stmt1 INTO :sValue;
    ...
}
```

If there are multiple queries they are normally executed, but only the first query can get the result.  
To get multiple results, the following statements related to the cursor should be used.

- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [FETCH cursor_name](#fcce02e780b87a86)
- [CLOSE cursor_name](#a7de81e9ff1d1b99)

If there is not any query result, it is completed as NO DATA.

<a id="41bdad2aebec41d4"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt; and &lt;result into clause&gt; can be specified in any order, but they should not be repeated.

<a id="fa8e641eef9a14e9"></a>
#### &lt;parameter using clause&gt;

If any parameter exists in a dynamic SQL statement referenced by statement_name, the parameter information is specified with &lt;using parameter arguments&gt; clause.

<a id="bccf82081f004461"></a>
#### &lt;using parameter arguments&gt;

If &lt;using parameter arguments&gt; statement is used, the number of variable_name should be equal to the number of the parameter included in the dynamic SQL statement referenced by statement_name.

The listed variable_name corresponds to the dynamic parameter in an order of its description.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2, :sValue3;
    ... 
}
```

<a id="7c3d085637ae9831"></a>
#### &lt;result into clause&gt;

If the dynamic SQL statement referenced by statement_name is a query, the information about the result columns is specified with &lt;into result arguments&gt; clause.

If the result is null and INDICATOR is not specified, [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error occurs.

<a id="2356a6b70e41e196"></a>
#### &lt;into result arguments&gt;

If &lt;into result arguments&gt; clause is used, the number of variable_name should be equal to the number of the result column in the dynamic SQL statement referenced by statement_name.

The listed variable_name corresponds to the dynamic parameter in an order of its description.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT MIN(salary), MAX(salary), AVG(salary) FROM employee';
    EXEC SQL EXECUTE stmt1 INTO :sMinValue, :sMaxValue, :sAvgValue;
    ... 
}
```

<a id="72da5d809839c3f0"></a>
### Description

Statement_name is an identifier which informs the precompiler the statement in an embedded SQL source code.  
A separate type or declaration is not required because statement_name is not a host variable. EXECUTE statement_name should be written after PREPARE statement_name.

For more information, refer to [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#b15442af59f50813).

<a id="1728c491034de9ff"></a>
### Example

The following is an example of using EXECUTE statement_name in an embedded SQL source code.

```
{
    ...
    sprintf( sUpdateSql, "UPDATE EMP SET sal = sal * :v1 WHERE JOB = 'SALES'");
    EXEC SQL PREPARE UPDATE_STMT FROM :sUpdateSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    sRatio = 1.1;
    EXEC SQL EXECUTE UPDATE_STMT USING :sRatio;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    ...
}
```

The full source code in which EXECUTE statement_name was used can be viewed in [Dynamic Embedded SQL Example Program](../part-05-developer-manual/33-embedded-sql.md#fe744f57cdd760c6).

<a id="d8db96eedb0b4088"></a>
### Compatibility

**SQL standard compatibility**

<a id="9ad78fca2586f50f"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="c7146a3713c5861a"></a>
### For More Information

Refer to the followings.

- [PREPARE statement_name](20-sql-references-h-z.md#fe0135540bee6aee)
- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [FETCH cursor_name](#fcce02e780b87a86)
- [CLOSE cursor_name](#a7de81e9ff1d1b99)
- [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#b15442af59f50813)

<a id="fcce02e780b87a86"></a>
## FETCH cursor_name

<a id="e33ad6f62ebda6c1"></a>
### Function

It locates the cursor on a specific row of result set, and obtains the value of that row to a host variable.

<a id="ba3f9a32df59a1f2"></a>
### Syntax

```
<fetch statement> ::=
    FETCH [ <fetch orientation> ] [ FROM ] cursor_name 
        <result into clause>
    ;

<fetch orientation> ::=
      NEXT
    | PRIOR
    | FIRST
    | LAST
    | CURRENT
    | ABSOLUTE position
    | RELATIVE position

<result into clause> ::=
      <into result arguments>

<into result arguments> ::=
    INTO variable_name [, ...]
```

<a id="37aea871cbe0e69e"></a>
### Syntax Rules and Parameters

<a id="b9b4c89c6d29c322"></a>
#### [ FROM ] cursor_name

It should be an open cursor in a session.  
FROM can be omitted.

<a id="11b6b96df78462b3"></a>
#### &lt;fetch orientation&gt;

To use &lt;fetch orientation&gt; other than FETCH NEXT, a scrollable cursor should be used.  
If &lt;fetch orientation&gt; is omitted, the default value is NEXT.

The open cursor has the cursor position information for the result set as follows.

<a id="8fd2d7bf8cf99dec"></a>
![The position of cursor](../assets/images/1233846ef1eeb18c.png)

**The position of cursor**

<a id="8efd1d6fe478de86"></a>
| Cursor position | Description |
| --- | --- |
| BEFORE THE FIRST ROW | The cursor is positioned before the first row of the result set. It is also the cursor position when opening it. |
| ON A CERTAIN ROW | The cursor is positioned on a certain row of the result set through FETCH. |
| AFTER THE LAST ROW | The cursor is positioned after the last row of the result set. |

Each &lt;fetch orientation&gt; operates based on the cursor position as follows.

- NEXT: It searches for the row next to the current position. 
- PRIOR: It searches for the row prior to the current position. 
- FIRST: It searches for the first row of the result set.
- LAST: It searches for the last row of the result set.
- CURRENT: It searches for the row in the current position.
- ABSOLUTE position 
    - It searches for the row corresponding to the position from the result set. 
    - If the position value is negative, it searches for the row at previous position from AFTER THE LAST ROW.
- RELATIVE position 
    - It searches for the row apart as much as position from the current position.

<a id="4576c7e3c3cebf84"></a>
#### &lt;result into clause&gt;

The variable information to obtain the result column is specified by using &lt;into result arguments&gt;.

If the result is null and INDICATOR is not specified, [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error occurs.

<a id="d5252b58f06687d1"></a>
#### &lt;into result arguments&gt;

The number of variables in INTO clause should be as same as the number of columns in the result set of the cursor.

<a id="6ed1f815eaac7aef"></a>
### Description

If the cursor is BEFORE THE FIRST ROW or AFTER THE LAST ROW after performing FETCH, it is positioned at the same position regardless of the entered position in &lt;fetch orientation&gt;.

<a id="fb1b973df9bb89e7"></a>
### Example

The following is an example of declaring SCROLL cursor by using the interactive SQL (gsql), then operating the various &lt;fetch orientation&gt;.

```
gSQL> DECLARE cur_scroll SCROLL CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur_scroll;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH NEXT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH NEXT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH PRIOR cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH FIRST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH LAST cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH CURRENT cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH ABSOLUTE 1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH ABSOLUTE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH ABSOLUTE 6 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH ABSOLUTE -6 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH ABSOLUTE 3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH ABSOLUTE -3 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH RELATIVE 1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH RELATIVE -1 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH RELATIVE 5 cur_scroll INTO :v_id, :v_data;

no rows fetched.

gSQL> FETCH RELATIVE -5 cur_scroll INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> CLOSE cur_scroll;

Cursor closed.
```

<a id="2a5f780d2126cff9"></a>
### Compatibility

The SQL standard does not define CURRENT among &lt;fetch orientation&gt;.

**SQL standard compatibility**

<a id="41617624176f1545"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="0865a2d63c963809"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#d5d4c37681027dd4)
- [OPEN cursor_name](20-sql-references-h-z.md#5c3a8ed73a7b2121)
- [CLOSE cursor_name](#a7de81e9ff1d1b99)

<a id="f4810a75ede2bf94"></a>
## FLASHBACK TABLE

<a id="0a8c6479775b65b5"></a>
### Function

It restores the table object which is stored in the recycle bin.

<a id="e8e1835289310099"></a>
### Syntax

```
<flashback table statement> ::=
    FLASHBACK TABLE table_name
    TO BEFORE DROP [ RENAME TO new_table_name ]
    ;
```

<a id="227732c81194c332"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;flashback table statement&gt;.

- The owner of that table
- CONTROL TABLE ON TABLE for that table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="a37e9ed5dc08185e"></a>
### Syntax Rules and Parameters

<a id="704846599fb044e7"></a>
#### table_name

It is the name of the object stored or of the dropped table in the recycle bin.  
It can define the schema to which the table belongs in the dropped table name, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="b296f2ee6c0d490a"></a>
#### new_table_name

It is a new name of the table to be restored.  
The duplicate table name should not exist within a single schema.

<a id="60b3cbabd2339acb"></a>
### Description

It restores the table object which is stored in the recycle bin by using the object name or the dropped table name stored in the recycle bin. If the name which is as same as that of the dropped table exists, then the newest table object is restored.

If the name which is as same as that of the table object to be restored exists, then an error occurs, but it can be restored with the new name by using RENAME TO clause. The constraints and the indexes of the restored tables are restored in its name of when before they were dropped. However, if their names of when before the constraints and the indexes were dropped already exist, then the object is restored in the name of when it is stored in the recycle bin.

Unlike other Data Definition Language (DDL), FLASHBACK TABLE statement can not be rolled back and the executed transaction is automatically committed.

<a id="0cc0f64bd5983e7e"></a>
### Example

The following is an example of restoring a table with the name of the object stored in the recycle bin.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

1 row selected.

gSQL> FLASHBACK TABLE "BIN$106A4F90165D11EA9C5C835D3E4BBBF7" TO BEFORE DROP;

Flashback complete.
```

The following is an example of restoring the table from the recycle bin in the name of when before it is dropped.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

gSQL> FLASHBACK TABLE T1 TO BEFORE DROP;

Flashback complete.
```

<a id="7763db70670f2932"></a>
### Compatibility

The SQL standard does not define &lt;flashback table statement&gt;.

<a id="45438a601bd3b169"></a>
### For More Information

Refer to the followings.

- [Managing Recycle Bin of Table](13-sql-objects.md#2e2d5a2f0f131f9c)
- [PURGE](20-sql-references-h-z.md#e690b6c4c32c9e70)

<a id="c7985df8e45cc984"></a>
## GRANT privileges TO

<a id="054e7462f2b7dd2a"></a>
### Function

It grants privileges to a user.

<a id="c547415c5c63d379"></a>
### Syntax

```
<grant privilege statement> ::=
    GRANT <privilege> TO <grantee> [, ...]
        [ WITH GRANT OPTION ]
    ;

<grantee> ::=
      PUBLIC
    | user_identifier
    ;
    
<privilege> ::=
      <database privilege>
    | <tablespace privilege>
    | <schema privilege>
    | <table privilege>
    | <sequence privilege>
    | <procedure privilege>

<database privilege> ::=
      ALL [ PRIVILEGES ] [ON DATABASE]
    | <database action> [, ...] [ON DATABASE]

<database action> ::=
      ADMINISTRATION
    | ANALYZE ANY 
    | ALTER DATABASE
    | ALTER SYSTEM
    | AUDIT SYSTEM
    | ACCESS CONTROL
    | CREATE SESSION
    | CREATE PROFILE
    | ALTER PROFILE
    | DROP PROFILE 
    | CREATE USER
    | ALTER USER
    | DROP USER 
    | CREATE ROLE
    | ALTER ROLE
    | DROP ROLE
    | CREATE TABLESPACE
    | ALTER TABLESPACE
    | DROP TABLESPACE
    | USAGE TABLESPACE
    | CREATE SCHEMA
    | ALTER SCHEMA
    | DROP SCHEMA
    | CREATE PUBLIC SYNONYM
    | DROP PUBLIC SYNONYM
    | CREATE ANY TABLE
    | ALTER ANY TABLE
    | DROP ANY TABLE
    | SELECT ANY TABLE
    | INSERT ANY TABLE
    | DELETE ANY TABLE
    | UPDATE ANY TABLE
    | LOCK ANY TABLE
    | CREATE ANY VIEW
    | DROP ANY VIEW
    | CREATE ANY SEQUENCE
    | ALTER ANY SEQUENCE
    | DROP ANY SEQUENCE
    | USAGE ANY SEQUENCE
    | CREATE ANY INDEX
    | ALTER ANY INDEX
    | DROP ANY INDEX
    | CREATE ANY SYNONYM
    | DROP ANY SYNONYM
    | CREATE ANY PROCEDURE
    | ALTER ANY PROCEDURE
    | DROP ANY PROCEDURE
    | EXECUTE ANY PROCEDURE
    | CREATE ANY PACKAGE
    | ALTER ANY PACKAGE
    | DROP ANY PACKAGE
    | EXECUTE ANY PACKAGE
    | PURGE DBA_RECYCLEBIN

<tablespace privilege> ::=
      ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name
    | <tablespace action> [, ...] ON TABLESPACE tablespace_name

<tablespace action> ::=
    CREATE OBJECT

<schema privilege> ::=
      ALL [ PRIVILEGES ] ON SCHEMA schema_name
    | <schema action> [, ...] [ON SCHEMA schema_name]

<schema action> ::=
      CONTROL SCHEMA
    | CREATE TABLE
    | ALTER TABLE 
    | DROP TABLE
    | SELECT TABLE
    | INSERT TABLE
    | DELETE TABLE
    | UPDATE TABLE
    | LOCK TABLE
    | CREATE VIEW
    | DROP VIEW
    | CREATE SEQUENCE
    | ALTER SEQUENCE
    | DROP SEQUENCE
    | USAGE SEQUENCE
    | CREATE INDEX
    | ALTER INDEX
    | DROP INDEX
    | ADD CONSTRAINT
    | CREATE SYNONYM
    | DROP SYNONYM
    | CREATE PROCEDURE
    | ALTER PROCEDURE
    | DROP PROCEDURE
    | EXECUTE PROCEDURE
    | CREATE PACKAGE
    | ALTER PACKAGE
    | DROP PACKAGE
    | EXECUTE PACKAGE

<table privilege> ::=
      ALL [ PRIVILEGES ] ON [TABLE] table_name
    | { <table action> | <column action> } [, ...] ON [TABLE] table_name

<table action> ::=
      CONTROL TABLE
    | SELECT
    | INSERT
    | UPDATE
    | DELETE
    | REFERENCES
    | LOCK
    | INDEX
    | ALTER

<column action> ::=
      SELECT ( column_name [, ...] )
    | INSERT ( column_name [, ...] )
    | UPDATE ( column_name [, ...] )
    | REFERENCES ( column_name [, ...] )

<sequence privilege> ::=
      ALL [ PRIVILEGES ] ON SEQUENCE sequence_name
    | <sequence action> ON SEQUENCE sequence_name

<sequence action> ::=
    USAGE

<procedure privilege> ::=
      ALL [ PRIVILEGES ] ON PROCEDURE procedure_name
    | <procedure action> ON PROCEDURE procedure_name

<procedure action> ::=
    EXECUTE

<package privilege> ::=
      ALL [ PRIVILEGES ] ON PACKAGE package_name
    | <package action> ON PACKAGE package_name

<package action> ::=
    EXECUTE
```

<a id="a721ccc7104078e4"></a>
### Syntax Rules and Parameters

<a id="fb6cce1491de14f4"></a>
#### &lt;grantee&gt;

It is the user to be granted the privileges.

- user_identifier 
    - It grants the privilege to a user. 
- PUBLIC 
    - It is an authorization object which means all users.

<a id="62f531df89bb3ed7"></a>
#### WITH GRANT OPTION

It allows the grantee to grant the privilege to other users.

When the same &lt;privilege&gt; is granted as follows, WITH GRANT OPTION is maintained.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="8849412473ffb388"></a>
#### &lt;privilege&gt;

It is a privilege which is to be granted to a grantee (the user to be granted the privilege).

The grantor (the user to perform the statement) should satisfy one of the following conditions.

- The grantor owns that &lt;privilege&gt; by using WITH GRANT OPTION. 
    - The grantor is the user who performs the statement.
- The grantor owns the ACCESS CONTROL ON DATABASE privilege.
    - The grantor is the object owner. 
        - &lt;database privilege&gt;: _SYSTEM account
        - &lt;tablespace privilege&gt;: _SYSTEM account 
        - &lt;schema privilege&gt;: _SYSTEM account
        - &lt;table privilege&gt;: The owner of the table 
        - &lt;sequence privilege&gt;: The owner of the sequence
        - &lt;procedure privilege&gt;: The owner of the procedure/function
        - &lt;package privilege&gt;: The owner of the package

<a id="c2ff68daf26914e5"></a>
#### &lt;database privilege&gt;

It is the privilege for the database objects.  
[ON DATABASE] statement can be omitted.

The database action which can be defined with the database privilege is as follows.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - All privileges for the database which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Database privilege**

<a id="212bfe043ef6e877"></a>
| &lt;database action&gt; | Description |
| --- | --- |
| ADMINISTRATION | Privilege for starting or terminating the server |
| ALTER DATABASE | Privilege for executing ALTER DATABASE |
| ALTER SYSTEM | Privilege for executing ALTER SYSTEM |
| AUDIT SYSTEM | Privilege for controlling the audit policy |
| ACCESS CONTROL | Privilege for controlling all the privileges |
| CREATE SESSION | Privilege for connecting to the database |
| CREATE PROFILE | Privilege for creating profiles in the database |
| ALTER PROFILE | Privilege for altering any profile in the database |
| DROP PROFILE | Privilege for dropping any profile in the database |
| CREATE USER | Privilege for creating users in the database |
| ALTER USER | Privilege for altering any user in the database |
| DROP USER | Privilege for dropping any user in the database |
| CREATE ROLE | Privilege for creating roles in the database |
| ALTER ROLE | Privilege for altering any role in the database |
| DROP ROLE | Privilege for dropping any role in the database |
| CREATE TABLESPACE | Privilege for creating tablespaces in the database |
| ALTER TABLESPACE | Privilege for altering any tablespace in the database |
| DROP TABLESPACE | Privilege for dropping any tablespace in the database |
| USAGE TABLESPACE | Privilege for using any tablespace in the database |
| CREATE SCHEMA | Privilege for creating schemas in the database |
| ALTER SCHEMA | Privilege for altering any schema in the database |
| DROP SCHEMA | Privilege for dropping any schema in the database |
| CREATE PUBLIC SYNONYM | Privilege for creating public synonyms in the database |
| DROP PUBLIC SYNONYM | Privilege for dropping any public synonym in the database |
| CREATE ANY TABLE | Privilege for creating tables in any schema of the database |
| ALTER ANY TABLE | Privilege for altering any table in the database |
| DROP ANY TABLE | Privilege for dropping any table in the database |
| SELECT ANY TABLE | Privilege for querying rows of any table in the database |
| INSERT ANY TABLE | Privilege for creating rows of any table in the database |
| DELETE ANY TABLE | Privilege for deleting rows of any table in the database |
| UPDATE ANY TABLE | Privilege for updating rows of any table in the database |
| LOCK ANY TABLE | Privilege for locking any table in the database |
| CREATE ANY VIEW | Privilege for creating views in any schema of the database |
| DROP ANY VIEW | Privilege for dropping any view in the database |
| CREATE ANY SEQUENCE | Privilege for creating sequences in any schema of the database |
| ALTER ANY SEQUENCE | Privilege for altering any sequence of the database |
| DROP ANY SEQUENCE | Privilege for dropping any sequence of the database |
| USAGE ANY SEQUENCE | Privilege for using any sequence of the database |
| CREATE ANY INDEX | Privilege for creating indexes in any schema of the database |
| ALTER ANY INDEX | Privilege for altering any index in the database |
| DROP ANY INDEX | Privilege for dropping any index in the database |
| CREATE ANY SYNONYM | Privilege for creating synonyms in the database |
| DROP ANY SYNONYM | Privilege for dropping any synonym in the database |
| CREATE ANY PROCEDURE | Privilege for creating any procedure/function in any schema of the database |
| ALTER ANY PROCEDURE | Privilege for altering any procedure/function in the database |
| DROP ANY PROCEDURE | Privilege for dropping any procedure/function in the database |
| EXECUTE ANY PROCEDURE | Privilege for executing any procedure/function in the database |
| CREATE ANY PACKAGE | Privilege for creating any package in any schema of the database |
| ALTER ANY PACKAGE | Privilege for altering any package in the database |
| DROP ANY PACKAGE | Privilege for dropping any package in the database |
| EXECUTE ANY PACKAGE | Privilege for executing any package in the database |
| PURGE DBA_RECYCLEBIN | Privilege for dropping any package in the database |

<a id="49c8be3a098c28d8"></a>
#### &lt;tablespace privilege&gt;

It is the privilege for the tablespace objects.

The tablespace action which can be defined with the tablespace privilege is as follows.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - All privileges for the tablespace which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Tablespace privilege**

<a id="e12cf12c4171047a"></a>
| &lt;tablespace action&gt; | Description |
| --- | --- |
| CREATE OBJECT | Privilege for creating objects in the tablespace |

<a id="53309e4011b33e74"></a>
#### &lt;schema privilege&gt;

It is the privilege for the schema objects.

- Whether to omit [ON SCHEMA schema_name]
    - If multiple &lt;grantee&gt; exist, [ON SCHEMA schema_name] statement can not be omitted. 
    - If ALL [PRIVILEGES] is used, [ON SCHEMA schema_name] statement can not be omitted. 
    - If [ON SCHEMA schema_name] statement is omitted, &lt;grantee&gt; can use only one user_identifier, and the privilege on the first schema in the schema search path of &lt;grantee&gt; is granted.

The schema action which can be defined with the schema privilege is as follows.

- ALL [ PRIVILEGES ] ON SCHEMA schema_name 
    - All privileges for the schema which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Schema privilege**

<a id="ae59fe06132b5796"></a>
| &lt;schema action&gt; | Description |
| --- | --- |
| CONTROL SCHEMA | All privileges for that schema |
| CREATE TABLE | Privilege for creating tables in the schema |
| ALTER TABLE | Privilege for altering any table in the schema |
| DROP TABLE | Privilege for dropping any table in the schema |
| SELECT TABLE | Privilege for querying rows of any table in the schema |
| INSERT TABLE | Privilege for creating rows of any table in the schema |
| DELETE TABLE | Privilege for deleting rows of any table in the schema |
| UPDATE TABLE | Privilege for updating rows of any table in the schema |
| LOCK TABLE | Privilege for locking any table of the schema |
| CREATE VIEW | Privilege for creating views in the schema |
| DROP VIEW | Privilege for dropping any view of the schema |
| CREATE SEQUENCE | Privilege for creating sequences in the schema |
| ALTER SEQUENCE | Privilege for altering any sequence of the schema |
| DROP SEQUENCE | Privilege for dropping any sequence of the schema |
| USAGE SEQUENCE | Privilege for using any sequence of the schema |
| CREATE INDEX | Privilege for creating indexes in the schema |
| ALTER INDEX | Privilege for altering any index in the schema |
| DROP INDEX | Privilege for dropping any index in the schema |
| ADD CONSTRAINT | Privilege for creating constraints in the schema |
| CREATE SYNONYM | Privilege for creating synonyms in the schema |
| DROP SYNONYM | Privilege for dropping any synonym of the schema |
| CREATE PROCEDURE | Privilege for creating any procedure/function in the schema |
| ALTER PROCEDURE | Privilege for altering any procedure/function in the schema |
| DROP PROCEDURE | Privilege for dropping any procedure/function in the schema |
| EXECUTE PROCEDURE | Privilege for executing any procedure/function in the schema |
| CREATE PACKAGE | Privilege for creating any package in the schema |
| ALTER PACKAGE | Privilege for altering any package in the schema |
| DROP PACKAGE | Privilege for dropping any package in the schema |
| EXECUTE PACKAGE | Privilege for executing any package in the schema |

<a id="dd26ea186f7b0adb"></a>
#### &lt;table privilege&gt;

It is the privilege for the table object or the view object.  
[TABLE] statement can be omitted.

The table action which can be defined with the table privilege is as follows.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - All privileges for the table which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Table privilege**

<a id="0ba723fe93253c3f"></a>
| &lt;table action&gt; | Description |
| --- | --- |
| CONTROL TABLE | All privileges for that table |
| SELECT | Privilege for querying rows of the table |
| INSERT | Privilege for creating rows into the table |
| UPDATE | Privilege for updating rows in the table |
| DELETE | Privilege for deleting rows from the table |
| REFERENCES | Privilege for creating referential constraints which refers to the table |
| LOCK | Privilege for locking the table |
| INDEX | Privilege for creating indexes in the table |
| ALTER | Privilege for altering the table |

For SELECT, INSERT, UPDATE, REFERENCES, additional privileges are granted to all columns of the table.

The column action which can be defined with the table privilege is as follows. However, the column action is applicable only to the base table.

**Column privilege**

<a id="229a457d7b78a658"></a>
| &lt;column action&gt; | Description |
| --- | --- |
| SELECT (columns) | Privilege for querying that columns |
| INSERT (columns) | Privilege for creating rows including that columns |
| UPDATE (columns) | Privilege for updating that columns |
| REFERENCES (columns) | Privilege for creating referential constraints which refers to that columns |

<a id="b730f2432dfa5a90"></a>
#### &lt;sequence privilege&gt;

It is the privilege for the sequence object.

The sequence action which can be defined with the sequence privilege is as follows.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - All privileges for the sequence which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Sequence privilege**

<a id="37e34829dad79788"></a>
| &lt;sequence action&gt; | Description |
| --- | --- |
| USAGE | Privilege for using the sequence |

<a id="9c7b23397649717c"></a>
#### &lt;procedure privilege&gt;

It is the privilege for the procedure/ function object.

The action which can be defined with the procedure privilege is as follows.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - All privileges for the procedure/ function which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Procedure privilege**

<a id="ef97ac0a0ae6e41f"></a>
| &lt;procedure action&gt; | Description |
| --- | --- |
| EXECUTE | Privilege for executing the procedure/function |

<a id="8c65c318403a73f0"></a>
#### &lt;package privilege&gt;

It is the privilege for the package object.

The action which can be defined with the package privilege is as follows.

- ALL [ PRIVILEGES ] ON PACKAGE package_name
    - All privileges for the package which is given to the grantor (the user who performs the statement) by using WITH GRANT OPTION

**Package privilege**

<a id="0ad189b7ee1d743b"></a>
| &lt;package action&gt; | Description |
| --- | --- |
| EXECUTE | Privilege for executing the package |

<a id="48520695ddd006b0"></a>
### Description

Data Definition Language (DDL) such as GRANT privilege can be rolled back if it is before when the transaction is committed.

The owner who created SQL schema object, such as table, sequence, has certain privileges without being granted any separate privilege for the object.    
For more information, refer to the following CREATE statements.

- [CREATE TABLE](#4c3b06d433f75b3d)
- [CREATE VIEW](#b82ddec42cccf582)
- [CREATE SEQUENCE](#11cfe1f314df4ce6)
- [ALTER TABLE name ADD COLUMN](18-sql-references-a-b.md#9e97702c72f6ffbe) 
- [CREATE FUNCTION](../part-04-psm-manual/29-psm-sql-references.md#7acaf940b774cb75)
- [CREATE PROCEDURE](../part-04-psm-manual/29-psm-sql-references.md#c4195b7175b4b1f4)
- [CREATE PACKAGE](../part-04-psm-manual/29-psm-sql-references.md#14a6f29743ca8dc2)

The owner who created non-schema object such as schema, tablespace, does not automatically have any privilege for the object. Therefore, the privilege should be separately granted.   
For more information, refer to the following CREATE statements.

- [CREATE SCHEMA](#f7ea7ef79efa639b)
- [CREATE TABLESPACE](#cfdf7d2f50958860)
- [CREATE USER](#67d566d84adb0376)

<a id="a7a2393a345d0fb9"></a>
### Examples

The following is an example of granting SELECT ON TABLE t1 privilege to the user u1.

```
gSQL> GRANT SELECT ON t1 TO u1;

Grant succeeded.
```

The following is an example of granting SELECT ON TABLE t1 privilege to the PUBLIC account (all users).

```
gSQL> GRANT SELECT ON t1 TO PUBLIC;

Grant succeeded.
```

The following is an example that the user u1 grants the privilege to the other user by using WITH GRANT OPTION.

```
gSQL> GRANT SELECT ON t1 TO u1 WITH GRANT OPTION;

Grant succeeded.
```

The following is the example that the user executing the statement grants all privileges on the TABLE t1 to user u1 by using WITH GRANT OPTION.

```
gSQL> GRANT ALL PRIVILEGES ON TABLE t1 TO u1;

Grant succeeded.
```

The following is an example of granting CREATE SESSION ON DATABASE privilege which is a privilege for connecting to the database.

```
gSQL> GRANT CREATE SESSION ON DATABASE TO u1;

Grant succeeded.
```

The following is an example of granting multiple privileges for creating objects such as the table, view, index, sequence, constraint in the SCHEMA s1 to the user u1.

```
gSQL> GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE, ADD CONSTRAINT ON SCHEMA s1 TO u1;

Grant succeeded.
```

The following is an example of granting the privileges for creating objects in TABLESPACE mem_data_tbs to the user u1.

```
gSQL> GRANT CREATE OBJECT ON TABLESPACE mem_data_tbs TO u1;

Grant succeeded.
```

The following is an example of granting the privilege for querying some columns in the TABLE t1 to the user u1.

```
gSQL> GRANT SELECT( id, name ) ON TABLE t1 TO u1;

Grant succeeded.
```

The following is an example of granting the privilege to the user u1 for using NEXTVAL(), CURRVAL() functions in the SEQUENCE seq1.

```
gSQL> GRANT USAGE ON SEQUENCE seq1 TO u1;
Grant succeeded.
```

<a id="ff24568dff6495fb"></a>
### Compatibility

The SQL standard does not define the following privileges.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL standard compatibility**

<a id="5b86531f18b64578"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="b96c2454a637c0c4"></a>
### For More Information

Refer to the followings.

- [REVOKE privileges FROM](20-sql-references-h-z.md#11e3eda7800214e7)
- [CREATE USER](#67d566d84adb0376)
- [DROP USER](#f64464bae416acc8)
- [ALTER USER](18-sql-references-a-b.md#270d91f0c78160b6)

---

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [Table of contents](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
