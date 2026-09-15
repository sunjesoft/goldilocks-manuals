<a id="d67bce1008c3a9d5"></a>

# 19. SQL References (C~G)

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/d67bce1008c3a9d5)  
> Tag: `26c.1_0_tag`

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [Table of contents](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<a id="a47858c9b07fa0f3"></a>
## CLOSE cursor_name

<a id="147e5d7fc84eda1c"></a>
### Function

It closes the cursor.

<a id="774e596191162bc1"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="d64c6b4d7df0a437"></a>
### Syntax Rules and Parameters

<a id="54d7afb0a248afab"></a>
#### cursor_name

The cursor must be open.  
It should be declared within the session using the [DECLARE cursor_name](#ccb6dc5ecb7cf850) statement.

<a id="83ed47a1c154f577"></a>
### Description

A cursor is an object that exists within a session and does not affect cursors in other sessions.

<a id="6c30df2c44552371"></a>
### Example

The following is an example of DECLARE, OPEN, FETCH, and CLOSE of a cursor using the interactive SQL tool, gsql.

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

<a id="902a76933f53d109"></a>
### Compatibility

**SQL standard compatibility**

<a id="495365966559022e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="f1513570e0aac534"></a>
### For More Information

Refer to the following.

- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [FETCH cursor_name](#b4d62d5536bcdf22)

<a id="a14777a330bd6a71"></a>
## COMMENT ON name IS

<a id="f4f964f4cabc6d78"></a>
### Function

It stores comments about the object in the dictionary.

<a id="549b9419379448b9"></a>
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
    | AUDIT POLICY policy_name
    | AUTHORIZATION user_name
    | TABLESPACE tablespace_name
    | SCHEMA schema_name
    | TABLE [schema_name].table_name
    | COLUMN [schema_name].table_name.column_name
    | INDEX [schema_name].index_name
    | SEQUENCE [schema_name].sequence_name
    | CONSTRAINT [schema_name].constraint_name
    | LIBRARY [schema_name].library_name
    | PROCEDURE [schema_name].procedure_name
    | PACKAGE [schema_name].package_name
    | TRIGGER [schema_name].trigger_name
```

<a id="836ca479d3374289"></a>
### Invocation and Access Rules

The privileges on each object must be altered as follows to execute the &lt;COMMENT&gt; statement.

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
- LIBRARY
    - The owner of the library
    - CONTROL SCHEMA ON SCHEMA for the schema to which the library belongs
- PROCEDURE
    - The owner of the stored procedure/function
    - CONTROL SCHEMA ON SCHEMA for the schema to which the stored procedure/function belongs
    - ALTER ANY PROCEDURE ON DATABASE
- PACKAGE
    - The owner of the package
    - CONTROL SCHEMA ON SCHEMA for the schema to which the package belongs
    - ALTER ANY PACKAGE ON DATABASE
- TRIGGER
    - The owner of the trigger
    - CONTROL SCHEMA ON SCHEMA for the schema to which the trigger belongs
    - ALTER ANY TRIGGER ON DATABASE

<a id="bf2821068c8963b6"></a>
### Syntax Rules and Parameters

<a id="01db3974053a37d4"></a>
#### &lt;comment object&gt;

It is an object where comments are stored. Comments for the following database objects are stored.

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
    - LIBRARY
    - PROCEDURE or FUNCTION
    - PACKAGE
    - TRIGGER

If the schema_name for the schema object is not specified, the schema name is determined by the [Schema Path](13-sql-objects.md#99f767e717d501b2) of the user executing the statement.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="11fc15c09a613523"></a>
#### 'comment string'

It describes the comments to be stored.  
Use an empty string ('') to delete the comments as shown below.

```
COMMENT ON TABLE test_table IS '';
```

The length of the comment string must not exceed 1024 bytes.

<a id="33868361dac4ed6b"></a>
### Description

Information by object type can be found in the COMMENTS column of the following dictionary views.

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
    - LIBRARY
        - DICTIONARY_SCHEMA.USER_LIBRARIES view
        - DICTIONARY_SCHEMA.ALL_LIBRARIES view
        - DICTIONARY_SCHEMA.DBA_LIBRARIES view
    - PROCEDURE & FUNCTION
        - DICTIONARY_SCHEMA.USER_PROCEDURES view
        - DICTIONARY_SCHEMA.ALL_PROCEDURES view
        - DICTIONARY_SCHEMA.DBA_PROCEDURES view
        - INFORMATION_SCHEMA.ROUTINES view
    - PACKAGE
        - INFORMATION_SCHEMA.MODULES view
    - TRIGGER
        - DICTIONARY_SCHEMA.USER_TRIGGERS view
        - DICTIONARY_SCHEMA.ALL_TRIGGERS view
        - DICTIONARY_SCHEMA.DBA_TRIGGERS view
        - INFORMATION_SCHEMA.TRIGGERS view

For more information about each view, refer to the [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#7b4ef74c9b03cbc2).

<a id="75d156215ff46ada"></a>
### Examples

The following is an example of creating a comment on a table.

```
gSQL> COMMENT ON TABLE t1 IS 'test comment on table t1';

Comment created.
```

The following is an example of creating a comment on a column.

```
gSQL> COMMENT ON COLUMN t1.id IS 'test comment on column t1.id';

Comment created.
```

The following is an example of creating a comment on a schema.

```
gSQL> COMMENT ON SCHEMA s1 IS 'test comment on schema s1';

Comment created.
```

<a id="f8926363315b9c1a"></a>
### Compatibility

&lt;comment statement&gt; is not part of the SQL standard.

<a id="3beee453ea244831"></a>
## COMMIT

<a id="16f53ced983cbe5d"></a>
### Function

It terminates the current transaction and commits all changes permanently.

<a id="479d39f19f48ea5e"></a>
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

<a id="6b8bbc79613f7a55"></a>
### Syntax Rules and Parameters

<a id="23ffeec67ebd3f5a"></a>
#### WORK

It is a reserved word that does not affect the operation.

<a id="dbc3fa367b8d72b4"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - It specifies the comment for the transaction when committing the transaction.

<a id="b792bdab3b7113e4"></a>
#### &lt;commit write clause&gt;

It determines whether to wait until the redo logs generated by the commit operation are written to the redo log file.

- WAIT
    - It waits until the redo logs generated by the commit operation are written to the redo log file, and then the operation is terminated. 
- NOWAIT
    - The operation is terminated once the redo logs generated by the commit operation are written to the redo log buffer.
- If not specified, the default property is used.

<a id="0894ec559b2fc271"></a>
#### &lt;commit force clause&gt;

It is used to manually commit a distributed transaction.

- FORCE 'xid_string'
    - It commits the distributed transaction corresponding to 'xid_string'.
    - The 'xid_string' is composed of *'format_id.transaction_id.branch_id'*.

<a id="ae76a7a2aceee739"></a>
### Description

The COMMIT statement completes the following statements executed within a transaction.

- Data Manipulation Language (DML) statement
    - It is a statement that alters data, such as INSERT, UPDATE, and DELETE. 
- Data Definition Language (DDL) statement
    - It is a statement that alters the structure and definition of objects, such as CREATE, DROP, ALTER, TRUNCATE, GRANT, and REVOKE.

Exceptionally, the following DDL statements, which manage OS resources or alter the DATA TYPE, are automatically committed.

- [CREATE TABLESPACE](#8ab1dca3b8dad438)
- [DROP TABLESPACE](#9b31e9a7a77c3aed)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](18-sql-references-a-b.md#ccd11b5a7e1a1306)

When performing a COMMIT, the cursor opened with the WITHOUT HOLD option is automatically closed. For more information about cursors, refer to the following cursor-related statements.

- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)

If a transaction violates a DEFERRED constraint, the COMMIT statement will fail and the transaction will be rolled back. For more information about DEFERRED constraints, refer to the [SET CONSTRAINTS](20-sql-references-h-z.md#99b7c8cb97aff1bd).

<a id="430e6bb7e29286d8"></a>
### Example

The following is an example of performing a COMMIT after executing an INSERT statement.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="471533f2c7f366bc"></a>
### Compatibility

**SQL standard compatibility**

<a id="39555367b2929f79"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="4ac293f264c3f1b8"></a>
### For More Information

Refer to the following.

- [ROLLBACK](20-sql-references-h-z.md#a7f186a4dca1588e)
- [SAVEPOINT savepoint_specifier](20-sql-references-h-z.md#79cec2425d42b60f)

<a id="9b9979f490f84f42"></a>
## CREATE AUDIT POLICY

<a id="5a966711c37ced79"></a>
### Function

This creates an audit policy object.  
To activate the created audit policy, the AUDIT POLICY statement must be executed.

<a id="199d0c882c3079d6"></a>
### Syntax

```
<audit policy definition> ::= 
    CREATE AUDIT POLICY policy_name
    { <privilege_audit_clause> | <role_audit_clause> | <action_audit_clause> }  [, ...]
    ; 

<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<role_audit_clause> ::=
    ROLES <role_name> [, ...]


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

<a id="eb136c321dc85f60"></a>
### Invocation and Access Rules

The AUDIT SYSTEM ON DATABASE privilege is required to execute the &lt;audit policy definition&gt;.

<a id="7f516e2c3eafd209"></a>
### Syntax Rules and Parameters

<a id="18191a7c6591b11e"></a>
#### policy_name

It is the name of the audit policy to be created.

<a id="3c3f2c04f9912faa"></a>
#### &lt;privilege_audit_clause&gt;

Privilege auditing audits cases where SQL statements are successfully executed using database privileges. It can audit specific users who execute SQL statements using such privileges, but does not record audit logs for the SYS user, who is the owner of the database.

The following is an example of granting the SELECT ANY TABLE privilege to user u1 and enabling the audit policy.

```
CREATE AUDIT POLICY p1 
       PRIVILEGES SELECT ANY TABLE;

AUDIT POLICY p1;
```

If user u1 executes the following SQL statement, the privilege audit operates differently.

- SELECT * FROM u1.t1;
    - No audit record is created when the SQL statement is executed with the owner privilege on the table u1.t1.
- SELECT * FROM u2.t1;
    - An audit record is created when the SQL statement is executed with the SELECT ANY TABLE privilege.

The &lt;database_privilege&gt; that can be described in the privilege audit can be viewed with the following query.

```
SELECT PRIVILEGE_NAME FROM V$AUDITABLE_DB_PRIVILEGES;
```

<a id="6c9f34fc393f06e8"></a>
#### &lt;role_audit_clause&gt;

Role auditing monitors the execution of SQL statements using a specific role.   
The following is an example of granting the dba role privilege to user u1 and activating the audit policy.

```
gSQL> GRANT dba TO u1;
gSQL> CREATE AUDIT POLICY p1 ROLES dba;
gSQL> AUDIT POLICY p1;
```

The privilege audit operates differently when user u1 executes the following SQL statement.

- u1> SELECT * FROM u1.t1;
    - The SQL statement is performed using the privilege of the u1.t1 table's owner, and no audit record is generated.
- u1> SELECT * FROM u2.t1;
    - The SQL statement is performed using the dba role privilege, and an audit record is generated.

<a id="bb22f04139a06c35"></a>
#### &lt;action_audit_clause&gt;

It audits actions on specific objects as well as actions across the entire database.

<a id="fc3c926aebb5e6e5"></a>
#### &lt;object_action_audit&gt;

<a id="c9c98d2a0df30c93"></a>
##### ALL ON object_name

It refers to all actions that can list objects corresponding to the object_name.

The following table describes the audit actions that can be audited for each object type.

**Audit action per object type**

<a id="977c1e997f282b40"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored Function/Procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="3d5c89bd2224075d"></a>
##### &lt;object_action&gt; ON object_name

Each separate action for a specific object must be listed by specifying the ON clause as follows.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="59f850b194a8e85d"></a>
##### Caution of EXECUTE action

Auditing the success or failure of a stored function or stored procedure is determined solely by whether it is executable at the time of execution.

- WHENEVER NOT SUCCESSFUL creates an audit record when neither the stored function nor the procedure is executable.
- WHENEVER SUCCESSFUL creates an audit record even if an error occurs while executing an SQL statement within the stored function or procedure 
- If auditing the failure of an SQL statement within the stored function or procedure is required, the audit target must include the corresponding SQL statement.

<a id="af35d53477f2a474"></a>
#### &lt;system_action_audit&gt;

It audits system actions that occur in the database, regardless of a specific object.

- &lt;system_action&gt;

The valid system actions can be retrieved using the following query.

```
SELECT ACTION_NAME FROM V$AUDITABLE_SYSTEM_ACTIONS;
```

- ALL

It refers to all system actions.

- DDL

It refers to all Data Definition Language (DDL) statements.

<a id="81864714491086df"></a>
### Description

An audit policy object is an object that defines auditing targets.    
Execute the AUDIT POLICY statement to activate the audit policy.

Although it is possible to define and activate multiple audit policies, it is recommended to maintain a limited number of audit policies.    
It is also recommended to group multiple small policies into a smaller number of policy groups.

Information about an option of the created audit policy object can be retrieved through the AUDIT_POLICY_OPTIONS view as shown below.

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

<a id="3355bac9bb3c2515"></a>
#### Creating Audit Record

If an action corresponding to multiple audit policies occurs, one or more audit records will be created.

If similar audit options are listed as shown below, one audit record will be created.

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

If two different audit options are listed as shown below, two audit records will be created.

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

If multiple audit policies are activated for the same action as shown below, two audit records will be created.

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

<a id="ee200b4d10d84392"></a>
### Examples

The following is an example of defining an audit policy that audits a privilege.

```
CREATE AUDIT POLICY policy_table
       PRIVILEGES CREATE ANY TABLE
                , DROP ANY TABLE
;
```

The following is an example of defining an audit policy to track a specific action on an object.

```
CREATE AUDIT POLICY policy_dml
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
             , ALL    ON u1.t2
;
```

The following is an example of defining an audit policy to track a system action.

```
CREATE AUDIT POLICY policy_drop
       ACTIONS DROP TABLE, TRUNCATE TABLE
;
```

The following is an example of defining an audit policy that combines all examples above.

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

<a id="131655038fffc8dd"></a>
### Compatibility

The audit policy is not part of the SQL standard.

<a id="be8887ef629ed815"></a>
### For More Information

Refer to the following.

- Managing audit policy objects
    - [CREATE AUDIT POLICY](#9b9979f490f84f42)
    - [DROP AUDIT POLICY](#230511362f0d7d5e)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#1ee1c2c985e74ad3)

- Activating/ deactivating an audit policy
    - [AUDIT POLICY](18-sql-references-a-b.md#28ecab768bc8d18a)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#237307d91350ad0b)

- Retrieving the audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#79d9233c8fc99c99)

- Clearing the audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#a4524ffa1dc98eef)

<a id="6ad165b04482545a"></a>
## CREATE CLUSTER GROUP

<a id="48d3c05ea669f217"></a>
### Function

It creates a cluster group to participate in the cluster system.

<a id="11bbbc210dc48b25"></a>
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

<a id="e3584212d97a0cbe"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

The ADMINISTRATION ON DATABASE privilege is required to execute the &lt;cluster group definition&gt;.

<a id="595a2d4f5e0390c1"></a>
### Syntax Rules and Parameters

<a id="04e3ac6bf97e6dbe"></a>
#### group_name

It is the name of a cluster group.  
An identical cluster group name or cluster member name must not exist.  
The name length must be shorter than 128 bytes.

<a id="6ad2861ee8dd3ebf"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group can include up to 32 cluster members.  
The first  cluster group created in a cluster system can define only one cluster member, and it must include itself as the member.

<a id="cac37bbda9b718a0"></a>
#### member_name

It is the name of a cluster member.  
The name must be the same as the member name defined when creating the database for that member.  
No duplicate names are allowed among cluster groups or cluster members.  
The name must be shorter than 128 bytes.

The start-up phase of the cluster member must be GLOBAL OPEN.

<a id="80074038328db33d"></a>
#### &lt;connection attribute&gt;

It defines the connection information used for communication between cluster members.  
The &lt;connection attribute&gt; must match the HOST and PORT specified when the database for that cluster member was created.  
The combination of HOST and PORT must be unique within the cluster system.

- HOST 'address' uses either a host name or an IPv4 address. If a host name is used, the system uses the first available IPv4 address.
- PORT port_no must be in the range of 1024 to 49151.

<a id="d39357ff43d8cfec"></a>
#### &lt;member position&gt;

It assigns the position number to the cluster member.

- POSITION DEFAULT
    - The system automatically assigns the position number.
- POSITION MAX
    - The system assigns a new member position number even if an empty position number exists.
    - It assigns a value greater than the highest existing member position.
- POSITION number
    - The system assigns the position number corresponding to the specified number.
    - The position number must be unique within the cluster system.
    - The position number must be an empty position number and should be equal to or smaller than the highest existing position number.
- If omitted, the default value is POSITION DEFAULT.

The member_position information of the cluster member can be retrieved through the DBA_CLUSTER view.

```
SELECT member_name, member_id, member_position FROM dba_cluster;
```

If the following position numbers are being used,

- G1N1: 0
- G1N2: 1
- G2N2: 3
- G3N2: 5

The following values are assigned according to the selected option.

- POSITION DEFAULT
    - It assigns 2, which represents an empty value.
- POSITION MAX
    - It assigns 6, which is the value for a new position number.
- POSITION 3
    - It is duplicated, so an error occurs.
- POSITION 4
    - It assigns position number 4.

<a id="8a7b70076d9f2989"></a>
### Description

The &lt;cluster group definition&gt; statement does not rebalance table shards.

Perform the following statements to rebalance shards to the newly added cluster group.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#eba0a85e4ceddd6e)
- [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242)

<a id="dfc105f93509ec1d"></a>
### Examples

The following is an example of how to create a cluster group consisting of two cluster members.

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

<a id="5e21a28d1328d0be"></a>
### Compatibility

The SQL standard does not define the concept of a cluster.

<a id="33ab321a9f82bf74"></a>
### For More Information

Refer to the following.

- [DROP CLUSTER GROUP](#cf6da303c45334dc)
- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#587d989b6ad2040a)

<a id="1e6f444e1a43b4b5"></a>
## CREATE CLUSTER LOCATION

<a id="b2c5a8af6aec7a24"></a>
### Function

It creates the connection information for a cluster member.

<a id="4e1f92a25767d1f2"></a>
### Syntax

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
        <cluster connection attribute>
        [ AT <domain name> ]
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="643f49296f93aeb4"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

The ADMINISTRATION ON DATABASE privilege is required to execute the &lt;cluster location definition&gt;.

<a id="ddbca34ba0f2582f"></a>
### Syntax Rules and Parameters

<a id="117e3333b5b94e4a"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name must not exist in the registered cluster location information.  
The name length must be shorter than 128 bytes.

<a id="e69132e807bcab68"></a>
#### &lt;cluster connection attribute&gt;

It defines the connection information for communication between cluster members.  
The combination of HOST and PORT must be unique within the cluster system.

- The HOST 'address' can be specified using either the host name or the IPv4 address. If a host name is used, the system will use the first IPv4 address associated with it.
- The PORT port_no must be within the range of 1024 to 49151.

<a id="83b13da893469a3e"></a>
#### &lt;domain name&gt;

It is the name of the member or group on which the statement is performed.  
If not specified, the statement is performed on all groups.

<a id="558c6647a0b9536c"></a>
### Description

The cluster location information is typically created automatically using the connection details provided during the creation of a cluster group or the addition of a cluster member. This information is deleted when the cluster member and group are deleted.

If the cluster location information is modified, the connection details can be updated using [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#b1673f7439fc39e9) without deleting or recreating the cluster member.

<a id="cf6ce40b55c91fcf"></a>
### Examples

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="ee3390e0f980d318"></a>
### Compatibility

The SQL standard does not define the concept of a cluster.

<a id="45811f537db14391"></a>
### For More Information

Refer to [DROP CLUSTER LOCATION](#9a30ad97763681d1) .

<a id="89eb5cb801251c20"></a>
## CREATE DISK DATA TABLESPACE

<a id="c322290217a90f47"></a>
### Function

It defines the disk data tablespace.

<a id="2800a74a5afe100e"></a>
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

<a id="3919ccac4352d75f"></a>
### Invocation and Access Rules

The CREATE TABLESPACE ON DATABASE privilege is required to execute the &lt;disk data tablespace definition&gt;.

The user who executed the statement has the CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

The following privileges are required to create an object in the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace
- USAGE TABLESPACE ON DATABASE

<a id="3563efaf7a0b2fbf"></a>
### Syntax Rules and Parameters

<a id="07373095ae095be9"></a>
#### tablespace_name

It is the name of the tablespace to be created.  
The length of the tablespace name must be shorter than 128 bytes.

<a id="9a1188c0e1cf5c1a"></a>
#### &lt;disk datafile clause&gt;

- 'filename' 
    - It is the name of the file used to store and manage data.
    - It serves as the storage space for table and index pages created in the disk tablespace.
    - filename can refer to either a new file or an existing one. 
    - The filename length must be shorter than 1024 bytes.

- SIZE &lt;size clause&gt; 
    - If the file is new, the initial size is specified using the SIZE clause.
    - If the file already exists, an error occurs. 
    - The file size can be specified in the range from 1 M to 30 G.

- REUSE 
    - If the file exists, use the REUSE clause.
    - If the file does not exist, a new file is created.
    - The size of the newly created file is set based on the USER_DATA_TABLESPACE_SIZE property.

- SIZE &lt;size clause&gt; REUSE 
    - If both the SIZE and REUSE clauses are specified, the operation depends on whether the filename already exists. 
        - If the filename is new, the SIZE clause specifies the initial file size. 
        - If the filename already exists, the file size is adjusted to the value specified in the SIZE clause.

<a id="c9edfe8891d14c86"></a>
#### &lt;autoextend clause&gt;

It sets the auto-expand property to either ON or OFF. When set to ON, the auto-extend size and the maximum size of the data file can be specified.

<a id="3b65db3a97c2448f"></a>
#### &lt;next size clause&gt;

It specifies the size to extend when the current data file runs out of available space.

<a id="a9465b6f76e5e757"></a>
#### &lt;max size clause&gt;

It specifies the maximum size to which the data file can be extended.

<a id="25d665515bf1f365"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If omitted, bytes are used by default.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0abe1c9770c29c06"></a>
#### &lt;domain_name&gt;

It is the name of the member or group that executes the statement.  
If omitted, it is executed for all groups.

<a id="a539423d17605bdc"></a>
#### ONLINE | OFFLINE

It sets the tablespace to ONLINE or OFFLINE.

- If set to ONLINE, the tablespace becomes available immediately upon creation.
- If set to OFFLINE, it is not available until it is explicitly switched to ONLINE.

<a id="104173c940cc0c4e"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies the extent size of the tablespace.

- The extent size is specified in bytes, and one of the following six values must be selected: 64 K, 128 K, 256 K, 512 K, 1 M, or 2 M.
- If the extent size is specified between 64 K and 128 K, it is set to 128 K. If the specified size exceeds 2 M, it is adjusted to 2 M.

<a id="95bf47d9146973b2"></a>
### Description

A data tablespace is an object that provides physical storage for SQL schema objects such as tables and indexes (LOGGING).

<a id="878fd2e80719848b"></a>
### Examples

The following is an example of how to create a disk data tablespace.

```
gSQL> CREATE DISK TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

The following is an example of how to create a tablespace that consists of multiple data files.

```
gSQL> CREATE DISK TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="c842f7fca18b7061"></a>
### Compatibility

The SQL standard does not define the concept of tablespaces.

<a id="c3dff9d123f4fc76"></a>
### For More Information

Refer to the following.

- [DROP TABLESPACE](#9b31e9a7a77c3aed)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)
- [ALTER DATABASE DATAFILE AUTOEXTEND](18-sql-references-a-b.md#c38f4ab693cfd2c4)

<a id="66b0fbe98e273ebf"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="ecbcac2a8725f9e5"></a>
### Function

It creates a new global temporary table.

<a id="0f540c42d224176b"></a>
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

> The definition of &lt;table element&gt; is the same as that of &lt;table_definition&gt;.  
> For more information, refer to [CREATE TABLE](#47f3ce328094503e).

<a id="2f9b108f1a1e3ab1"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute a &lt;global temporary table definition&gt; statement.

- Table creation privilege
    - Refer to the access privilege for the [CREATE TABLE](#47f3ce328094503e) statement.
- SELECT privilege 
    - Refer to the access privilege for the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="9c86789a2c8df1bb"></a>
### Syntax Rules and Parameters

<a id="500d349877456aa5"></a>
#### table_name

It is the table name to be created.  
For more information, refer to [table_name](#5b5d4adf46c16d6b).

<a id="6f684219189a374e"></a>
#### other syntax

For more information about other syntax rules, refer to the syntax of the [CREATE TABLE](#47f3ce328094503e) and [CREATE TABLE AS SELECT](#13b906a980351a1f) statements.

<a id="c54f5a56b357f221"></a>
### Description

A GLOBAL TEMPORARY TABLE is a temporary table used to store data that is preserved during the execution of a transaction or session.  
It is typically used in a similar way to a variable that temporarily holds intermediate data during application development.

The global temporary table has the following characteristics.

- The definition of a global temporary table is visible to all sessions.
- When a global temporary table is defined, no physical storage is allocated. A session-specific segment is allocated when data is inserted for the first time.
- Data in a global temporary table is visible only within the session or transaction that inserted it.
- The tablespace used to store data in a global temporary table is determined as follows.

<a id="5352abb316594a69"></a>
| Whether to specify tablespace | The tablespace where the table is created |
| --- | --- |
| A tablespace is explicitly specified. | The table is created in the specified tablespace. |
| No tablespace is specified. | The table is created in the current session user's default temporary tablespace. |

- The index for a global temporary table is subordinate to the same session as the corresponding table, and its lifetime is also the same as that of the table. 
- A view can be defined on a global temporary table.
- The &lt;table sharding strategy&gt; and &lt;table global secondary index clause&gt; clauses, that describe cluster-related features of the table for a global temporary table, cannot be specified.
- The &lt;table attribute clause&gt;, which defines the physical attributes of a table, and the &lt;index attribute clause&gt;, which defines the physical attributes of an index, cannot be specified for a global temporary table.
- The &lt;index attribute clause&gt;, which defines the physical attributes of an index, cannot be specified for indexes created on a global temporary table used as a base table.
- When a transaction is terminated by the &lt;table commit action clause&gt;, it is possible to determine how the remaining data is handled.

<a id="8bea330bdb3ea371"></a>
| Table commit action | Description |
| --- | --- |
| ON COMMIT PRESERVE ROWS | It retains the data in the table even after a COMMIT or ROLLBACK. |
| ON COMMIT DELETE ROWS (default) | It deletes all the data remaining in the table at the time of COMMIT or ROLLBACK (TRUNCATE). |

- It supports most DDLs for a regular table, including ALTER and TRUNCATE.
    - It does not support CLUSTER-related statements (such as SHARD and global secondary index-related statements).
    - DDL for a global temporary table that is currently in use in its own session or another session will result in an error.
    - DDL operations are allowed only after all segment used by TRUNCATE TABLE or COMMIT in all active sessions have been removed.
- It supports all DML operations and select statements for a regular table. 
- Any modifications to a global temporary table (DML) do not generate redo logs.
- Any modifications to a global temporary table (DML) generate undo logs, with the location of the undo log determined by the TEMP_UNDO_ENABLED property.

<a id="c5619e29e8f44a32"></a>
| TEMP_UNDO_ENABLED value | Description |
| --- | --- |
| TRUE | The undo log is recorded in the default temporary tablespace of the database system. |
| FALSE | The undo log is recorded in the undo tablespace of the database system. |

- The TRUNCATE command on a global temporary table truncates only the segment of the corresponding session.
- If the session is terminated, all segments are TRUNCATEd and then returned.

<a id="2bfe363424c9cd60"></a>
### Examples

The following is an example of executing the CREATE GLOBAL TEMPORARY TABLE statement.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE1(
        COL1    CHAR(10)
       ,COL2    VARCHAR2(20)
       ,COL3    NUMBER(10)
)   ON  COMMIT  DELETE ROWS;

Table created.
```

The following is an example of executing the CREATE GLOBAL TEMPORARY TABLE ... AS SELECT statement.

```
gSQL> CREATE  GLOBAL TEMPORARY TABLE SESSION_TABLE2
    ON  COMMIT  PRESERVE ROWS
    AS  SELECT  *
          FROM  EMPLOYEES;

Table created.
```

<a id="b93e1f4e695ec1e0"></a>
### Compatibility

The CREATE GLOBAL TEMPORARY TABLE and CREATE GLOBAL TEMPORARY TABLE AS SELECT statements follow the definition of &lt;table definition&gt; as specified in the SQL standard.  

However, the following is an extension of the standard.

- The SQL standard requires parentheses around the SELECT clause, but this is optional in GOLDILOCKS.
- The SQL standard also requires the WITH [NO] DATA clause, but this is optional in GOLDILOCKS.
- The concept of tablespaces in GOLDILOCKS is an extended feature that is not part of the SQL standard.

**SQL standard compatibility**

<a id="2054cd8639aed648"></a>
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

<a id="789b8ff9bcde530e"></a>
### For More Information

Refer to the following.

- [CREATE TABLE](#47f3ce328094503e)
- [CREATE TABLE AS SELECT](#13b906a980351a1f)

<a id="223284d287163f99"></a>
## CREATE IMMUTABLE TABLE

<a id="5fdd79233a679cd9"></a>
### Function

It creates a new immutable table.

<a id="cc668c16e7a94617"></a>
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

> The definitions of &lt;table element&gt;, &lt;table sharding strategy&gt;, &lt;table attribute clause&gt;, and &lt;table global secondary index clause&gt; are the same as those in &lt;table_definition&gt;. For more information, refer to the [CREATE TABLE](#47f3ce328094503e).

<a id="d93e23f4f7756343"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute a &lt;immutable table definition&gt; statement.

- Table creation privilege 
    - Refer to the access privilege for the [CREATE TABLE](#47f3ce328094503e) statement.
- SELECT privilege
    - Refer to the access privilege for the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="b3765eac8d25b39f"></a>
### Syntax Rules and Parameters

<a id="71fd05a010391cfd"></a>
#### table_name

It is the name of the table to be created, and it must be unique within the schema.  
The schema to which the table belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.  
The length of the table name must be less than 128 bytes.

<a id="345f195b2875270b"></a>
#### Other Syntax

For other syntaxes, refer to the syntax for [CREATE TABLE](#47f3ce328094503e) and [CREATE TABLE AS SELECT](#13b906a980351a1f).

<a id="1cd1757aaeeb57a0"></a>
### Description

An immutable table is used when it is necessary to prevent the records stored in the table from being altered or deleted, as well as to prevent the table from being dropped.

> An immutable table can be dropped when the user, schema, tablespace or cluster group is dropped.

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

<a id="8bf7f2fb56860d5c"></a>
### Examples

The following is an example of executing the CREATE IMMUTABLE TABLE statement.

```
gSQL> CREATE IMMUTABLE TABLE t1
(
    id INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

The following is an example of executing the CREATE IMMUTABLE TABLE ... AS SELECT statement.

```
gSQL> CREATE IMMUTABLE TABLE T2
       AS SELECT *
             FROM T1;

Table created.
```

<a id="5e08aa02b1b62579"></a>
### Compatibility

The SQL standard does not define the concepts of the CREATE IMMUTABLE TABLE and CREATE IMMUTABLE TABLE AS SELECT statements.

<a id="428922e5094570fe"></a>
### For More Information

Refer to the following.

- [CREATE TABLE](#47f3ce328094503e)
- [CREATE TABLE AS SELECT](#13b906a980351a1f)

<a id="c758c010adf913ce"></a>
## CREATE INDEX

<a id="f9a65cd9e7a22d45"></a>
### Function

It creates an index.

<a id="dc8fcebe6c57827a"></a>
### Syntax

```
<index definition> ::=
    CREATE [ UNIQUE ] INDEX index_name
        ON table_name ( <index column element> [, ...] )
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
        [ <index enforcement> ]
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

<size clause> ::=
      integer [ K | M | G | T ]

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]

<index enforcement> ::=
      { ENABLE | ENFORCED }
    | { DISABLE | NOT ENFORCED }
```

<a id="3b79e326335dd7bd"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute the &lt;index definition&gt;.

- One of the following privileges is required to create an index on the table.
    - (INDEX or CONTROL TABLE ON) TABLE for the table
    - CONTROL SCHEMA ON SCHEMA for the schema to which the table belongs
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the schema in which the index is to be created.
    - (CREATE INDEX or CONTROL SCHEMA) ON SCHEMA for the schema
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the tablespace in which the index is to be created.
    - CREATE OBJECT ON TABLESPACE for the tablespace
    - USAGE TABLESPACE ON DATABASE

- The owner of the index is determined as follows.
    - The owner of the schema to which the index belongs. 
    - If the schema to which the index belongs is PUBLIC, the user who executed the statement will be the owner.

> Unique indexes in a cluster system must include all sharding keys.

<a id="7a264e287c5f2d67"></a>
### Syntax Rules and Parameters

<a id="9a0ad07f2d3e9548"></a>
#### UNIQUE

Duplicate values are not allowed in the columns that make up the index.

<a id="1d9e2e2ced156d9f"></a>
#### index_name

It is the name of the index to be created, and it must be unique within the schema.  
If the schema name is omitted, the index is created in the schema of the referenced table.  
The length of the index name must be less than 128 bytes.

<a id="26437f203815d3c7"></a>
#### table_name

It is the name of the table on which the index will be created.  
The schema to which the table belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

<a id="a7be5eaead28e271"></a>
#### column_name

It is the name of the column to be used as an index key.  
At least one column must be defined, and up to 32 columns can be used as index keys.

The following constraints may arise depending on the implementation.

- If the column data type included in an index is LONG CHARACTER VARYING or LONG BINARY VARYING, an index can not be created.
- An index can only be created when the sum of the column precisions is less than 1200 bytes.

<a id="9f09c385f8c8275a"></a>
#### ASC | DESC

It specifies the sort order of a column.

- ASC: The column is sorted in ascending order.
- DESC: The column is sorted in descending order.
- If not specified, ASC is used by default.

<a id="6d0e148aa5173041"></a>
#### NULLS FIRST | NULLS LAST

It specifies the sort order of NULL values.

- NULLS FIRST: NULL values appear before non-NULL values.
- NULLS LAST: NULL values appear after non-NULL values.
- If not specified, the default is NULLS LAST.

<a id="e98b870b5e043e98"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attributes of the index.

- PCTFREE integer 
    - Definition 
        - The percentage of space reserved to control the frequency of page splits caused by key insertions within a page.
        - This setting applies only during bottom-up index builds.
    - Values can range from 0 to 99.
    - If omitted, the value defined in the DEFAULT_INDEX_PCTFREE property is used.

- INITRANS integer 
    - Definition 
        - It specifies the initial number of concurrent transactions that can access a page. 
        - If the number of users accessing the index is low, a smaller INITRANS value is recommended. For higher concurrency, a larger value should be used. 
        - If needed, the number can automatically increase up to the value specified by MAXTRANS.
    - Values can range from 1 to 32.
    - If omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of concurrent transactions that can access a page. 
    - Values can range from 1 to 32.
    - If omitted, the default value is 8.

<a id="9e486506d709b5ca"></a>
#### &lt;segment attr clause&gt;

It specifies the information regarding the storage space for the index.

- INITIAL integer
    - Definition
        - It specifies the size of the physical storage space initially allocated when creating the index.
        - If the integer value is less than or equal to two EXTENTs, it is set to the size of two EXTENTs.
        - If the integer value is greater than two EXTENTs, it is aligned to the TABLESPACE’s EXTENT size.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value is the size of two EXTENTs of the TABLESPACE to which the table belongs.

- NEXT integer
    - Definition
        - It specifies the size of the physical storage space to be allocated when adding space to the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually treated as 8192 bytes.)
        - The allocation of space for NEXT works as follows, depending on the remaining available space in the index (calculated by subtracting the amount of space currently used from the MAXEXTENTS size).  
      - If the remaining space size is 0, space cannot be extended.  
      - If the remaining space size is greater than 0 but smaller than NEXT, the space will be allocated as large as the remaining space.  
      - If the remaining space size is greater than NEXT, the space will be allocated as large as the NEXT size.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value is one EXTENT size of the TABLESPACE to which the index belongs.

<a id="c1ecf79557296399"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If omitted, bytes are used by default.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="a2889209a0138c0a"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used during the index creation process.

- NOPARALLEL 
    - The index is not built in parallel.
- PARALLEL [integer] 
    - The index is built in parallel.
    - If the integer is omitted or set to 0, it defaults to the INDEX_BUILD_PARALLEL_FACTOR property.
    - The integer value ranges from a minimum of 0 to a maximum of 16.
    - If the property value is 0, the system determines the optimal value.
- If omitted, the default value is PARALLEL.

<a id="3f44fc90f336d358"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace where the index will be stored.

- When the tablespace_name is specified
    - if tablespace_name is a data tablespace, a LOGGING index is created.
    - if tablespace_name is a temporary tablespace or nologging tablespace, a NOLOGGING index is created.

- When the TABLESPACE clause is omitted
    - If the USER's INDEX TABLESPACE tablespace_name is specified
        - The defined tablespace is used.
    - If the USER's INDEX TABLESPACE is NULL
        - The index of a DISK table uses the user's default data tablespace.
        - The index of a MEMORY table uses the user's default temporary tablespace.

<a id="7afa49f135872a23"></a>
#### &lt;index enforcement&gt;

If omitted, the default value is ENABLE.

ENABLE and ENFORCED have the same meaning.  
DISABLE and NOT ENFORCED have the same meaning.

- ENABLE
    - It enables the index.
- DISABLE
    - It disables the index.
    - Only the index object is created; the index itself is not built.
    - The index is not used for DML or SELECT operations.

<a id="45c272f2b085123c"></a>
### Description

LOGGING and NOLOGGING indexes each have the following trade-offs:

- LOGGING index
    - Advantage: The index does not need to be rebuilt separately, as it is automatically restored using the log during system startup.
    - Disadvantage: Disk I/O occurs because changes to the index are recorded in the log when a row is modified.
- NOLOGGING index
    - Advantage: Disk I/O does not occur for index changes when a row is modified.
    - Disadvantage: The index must be automatically rebuilt during system startup, as no log information is available for recovery.

<a id="5f66e70f03489d9e"></a>
### Examples

The following is an example of creating a unique index.

```
gSQL> CREATE UNIQUE INDEX idx_t1_id ON t1( id );

Index created.
```

The following is an example of creating an index for multiple columns.

```
gSQL> CREATE INDEX idx_t1_id_name ON t1( id, name );

Index created.
```

The following is an example of specifying the sort order of an index column.

```
gSQL> CREATE INDEX idx_t1_dept_id ON t1( dept_id DESC );

Index created.
```

The following is an example of specifying the sort order for NULL values in the index column.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name NULLS FIRST );

Index created.
```

The following is an example of setting the information about the space where the index is stored.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id )
             STORAGE ( INITIAL 10M NEXT 1M );

Index created.
```

The following is an example of creating redo logging for the index.

```
gSQL> CREATE INDEX idx_t1_id ON t1( id );

Index created.
```

The following is an example of creating an index with the parallel option.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) PARALLEL;

Index created.
```

The following is an example of specifying the tablespace when creating an index.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) TABLESPACE mem_temp_tbs;

Index created.
```

<a id="059edb8d63374761"></a>
### Compatibility

The SQL standard does not define the concept of the index.

<a id="071b4dc6970cb38e"></a>
### For more information

Refer to [DROP INDEX](#0d535b079ff2f022).

<a id="8f6b0a901e93d0d4"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="6950eda73df6c7aa"></a>
### Function

It defines a tablespace for memory data.

<a id="71b13c25f5aa7bde"></a>
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

<a id="2fb47074b2515c3f"></a>
### Invocation and Access Rules

The CREATE TABLESPACE ON DATABASE privilege is required to execute the &lt;memory data tablespace definition&gt;.

The user who executed the statement has the CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create objects in the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace
- USAGE TABLESPACE ON DATABASE

<a id="890794c1e18edb2a"></a>
### Syntax Rules and Parameters

<a id="e5042731485f7640"></a>
#### [ MEMORY ] [ DATA ]

It is a memory tablespace used to store permanent objects such as tables, indexes, and more.  
The reserved words MEMORY and DATA may be omitted.

<a id="13bc609d18607d09"></a>
#### tablespace_name

It is the name of the tablespace to be created.  
The length of the tablespace name must be less than 128 bytes.

<a id="7901181a874b6fb0"></a>
#### &lt;memory datafile clause&gt;

- 'filename' 
    - It specifies the name of the file used to store and manage data.
    - It is the storage location for checkpoint images of memory data. 
    - filename can refer to either a new file or an existing one.
    - The length of filename must be less than 1024 bytes.

- SIZE &lt;size clause&gt; 
    - The initial size of a new file is specified using the SIZE clause.
    - An error occurs if the file already exists.
    - The file size can be specified between a minimum of 1M and a maximum of 30G.

- REUSE 
    - If the file already exists, the REUSE clause is used. 
    - If the file does not exist, a new file is created. 
    - The size of the newly created file is determined as follows: 
        - By the USER_DATA_TABLESPACE_SIZE property in the case of a data tablespace.
        - By the USER_TEMP_TABLESPACE_SIZE property in the case of a temporary tablespace.

- SIZE &lt;size clause&gt; REUSE 
    - If both the SIZE clause and the REUSE clause are specified, the operation proceeds as follows based on the presence of the filename.
        - For a new filename, the initial file size is assigned using the SIZE clause.
        - For an existing filename, the file size is adjusted to the value specified in the SIZE clause, using the existing file.

<a id="c23aa3defdc42be8"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If omitted, bytes are used by default.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="77d6b0e40c3e387c"></a>
#### &lt;domain name&gt;

It is the name of the member or group on which the statement is performed.  
If not specified, the statement is performed on all groups.

<a id="82885de590fc20f3"></a>
#### ONLINE | OFFLINE

It sets the tablespace to ONLINE or OFFLINE.

- If set to ONLINE, the tablespace becomes available immediately upon creation.
- If set to OFFLINE, it is not available until it is explicitly switched to ONLINE.

<a id="3eaebdb47fada5b1"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies the extent size of the tablespace.

- The extent size is specified in bytes, and must be one of the following values: 64K, 128K, 256K, 512K, 1M, or 2M.
- If a value between 64K and 128K is specified, it is rounded up to 128K. If a value of 2M or greater is specified, it is set to 2M.

<a id="b3d52e4bdec40d4a"></a>
### Description

A data tablespace is an object that provides the physical storage space for SQL schema objects such as tables and indexes (LOGGING).

<a id="6cac340a63a0aef3"></a>
### Examples

The following is an example of how to create a memory data tablespace.

```
gSQL> CREATE TABLESPACE space1 DATAFILE 'test_file_1.dbf' SIZE 10M REUSE;

Tablespace created.
```

The following is an example of how to create a tablespace that consists of multiple data files.

```
gSQL> CREATE TABLESPACE space1 
             DATAFILE 'test_file_3_1.dbf' SIZE 10M REUSE,
                      'test_file_3_2.dbf' SIZE 10M REUSE;

Tablespace created.
```

<a id="18cb413ffefd0430"></a>
### Compatibility

The SQL standard does not define the concept of tablespaces.

<a id="617a204ec7cfb602"></a>
### For More Information

Refer to the following.

- [DROP TABLESPACE](#9b31e9a7a77c3aed)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)

<a id="a09ab566de521b1a"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="65d8c9db3c7e8dfc"></a>
### Function

It defines a memory temporary tablespace.

<a id="fa988573ad1a26f9"></a>
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

<a id="bac800c734bb2034"></a>
### Invocation and Access Rules

The CREATE TABLESPACE ON DATABASE privilege is required to execute the &lt;memory temporary tablespace definition&gt;.

The user who executed the statement has the CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create objects in the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace.
- USAGE TABLESPACE ON DATABASE

<a id="af400a39e99908f5"></a>
### Syntax Rules and Parameters

<a id="94e1791a4cd02e47"></a>
#### [ MEMORY ] TEMPORARY

It is a memory temporary tablespace used to store no-logging indexes or temporary objects, such as intermediate results generated during query processing.  
The reserved word MEMORY can be omitted.

<a id="6f97aa6e7da53bd2"></a>
#### tablespace_name

It is the name of the tablespace to be created.  
The name must be less than 128 bytes in length.

<a id="57cf1f88427afa39"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - It is the name of the memory used to store temporary data.
    - The memory_name must be unique within the tablespace.
    - Its length must be shorter than 1024 bytes.
- SIZE &lt;size clause&gt; 
    - It specifies the initial size.
    - The size must be between 1M and 30G.

<a id="53919728a1aee6fa"></a>
#### &lt;size clause&gt;

It specifies the size of the shared memory space in bytes. (If omitted, bytes are used by default.)  
For temporary memory data, the image is not managed as a file.

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ab50d3bb621f90db"></a>
#### &lt;domain name&gt;

It is the name of a member or group on which the statement is executed.  
If not specified, the statement is performed on all groups.

<a id="d07dd0e0ed926158"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies the extent size of the tablespace.

- The extent size is specified in bytes and must be one of the following values: 64K, 128K, 256K, 512K, 1M, or 2M.
- If a value between 64K and 128K is specified, it is rounded up to 128K. If a value equal to or greater than 2M is specified, it is set to 2M.

<a id="3fcf40aa74d8dde3"></a>
### Description

A temporary tablespace is an object that provides the physical storage space for SQL schema objects such as indexes (NOLOGGING), as well as for intermediate results used in operations like sorting and hashing during query processing.

<a id="3abb612d1f341fc5"></a>
### Examples

The following is an example of how to create a temporary tablespace.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 MEMORY 'test_memory_1' SIZE 10M;

Tablespace created.
```

The following is an example of how to create a temporary tablespace that includes multiple memory spaces.

```
gSQL> CREATE TEMPORARY TABLESPACE temp_space1 
             MEMORY 'test_memory_3_1' SIZE 10M,
                    'test_memory_3_2' SIZE 10M;

Tablespace created.
```

<a id="d691b05fd83ff22b"></a>
### Compatibility

The SQL standard does not define the concept of tablespaces.

<a id="116cbae48e1a42b8"></a>
### For More Information

Refer to the following.

- [DROP TABLESPACE](#9b31e9a7a77c3aed)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)

<a id="98c2f8112f164605"></a>
## CREATE PROFILE

<a id="ac1d92b29efe41b1"></a>
### Function

This statement creates the profile and sets the password management method.   
When a profile is assigned to a user, the user's password is managed according to the method defined in the profile.

<a id="548678fb46262978"></a>
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

<a id="a9ad69551950bb63"></a>
### Invocation and Access Rules

The CREATE PROFILE ON DATABASE privilege is required to execute the &lt;profile definition&gt;.

<a id="efbfda09962ed1f3"></a>
### Syntax Rules and Parameters

<a id="a71a3d6d7e7737c1"></a>
#### profile_name

It specifies the name of the profile to be created.

<a id="ab455b2f0c54d3f1"></a>
#### password_parameters

It sets the parameters for password management.

- The following parameters can be set. 
    - FAILED_LOGIN_ATTEMPTS
    - PASSWORD_LOCK_TIME
    - PASSWORD_LIFE_TIME
    - PASSWORD_GRACE_TIME
    - PASSWORD_REUSE_MAX
    - PASSWORD_REUSE_TIME
    - PASSWORD_VERIFY_FUNCTION

Omitted parameters default to the "DEFAULT" profile policy.

<a id="95e720204cf636dc"></a>
#### FAILED_LOGIN_ATTEMPTS

It sets the number of consecutive failed login attempts allowed.  
If the number of failed attempts exceeds the specified value, the account is locked.

- FAILED_LOGIN_ATTEMPTS integer
    - The value must be a positive integer greater than 0.
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - Failed login attempts do not result in account lockout.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.

<a id="4ae53bd6b96ea5a6"></a>
#### PASSWORD_LOCK_TIME

It sets the duration (in days) for which the account remains locked after consecutive failed login attempts.

- PASSWORD_LOCK_TIME constant_expression
    - It specifies the duration (in days) for which an account remains locked.
    - The default unit is days.
    - For testing purposes, shorter duration can be specified using fractional values such as n/24 for hours, n/1,440 for minutes, or n/86,400 for seconds.
    - Valid range: 1 second (1/86400) to 100,000 days
- PASSWORD_LOCK_TIME UNLIMITED
    - If the account is locked, it will remain locked until the ALTER USER user_name ACCOUNT UNLOCK statement is executed.
- PASSWORD_LOCK_TIME DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.

<a id="824ffd63d923646b"></a>
#### PASSWORD_LIFE_TIME

It sets the password lifetime (in days).

- PASSWORD_LIFE_TIME constant_expression 
    - It specifies the lifetime of a password (in days).
    - The default unit is days.
    - For testing purposes, shorter duration can be specified using fractional values such as n/24 for hours, n/1,440 for minutes, or n/86,400 for seconds.
    - Valid range: 1 second (1/86400) to 100,000 days
- PASSWORD_LIFE_TIME UNLIMITED 
    - The password does not expire.
- PASSWORD_LIFE_TIME DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.

<a id="7af7baf41e16359f"></a>
#### PASSWORD_GRACE_TIME

It defines the grace period during which users can still log in after the password expires as specified by PASSWORD_LIFE_TIME.

- PASSWORD_GRACE_TIME constant_expression 
    - It specifies the grace period after password expiration (in days)
    - The default unit is days.
    - For testing purposes, shorter duration can be specified using fractional values such as n/24 for hours, n/1,440 for minutes, or n/86,400 for seconds.
    - Valid range: 1 second (1/86400) to 100,000 days
- PASSWORD_GRACE_TIME UNLIMITED 
    - Password expiration is deferred indefinitely. 
- PASSWORD_GRACE_TIME DEFAULT 
    - It follows the policy defined in the "DEFAULT" profile.

PASSWORD_GRACE_TIME begins at the first login attempt after the password validity period has passed. If the password is not changed during this period, it will expire.

<a id="f23244506e107548"></a>
#### PASSWORD_REUSE_MAX

It sets the number of the recent passwords that cannot be reused when a user attempts to use a previously used password.

PASSWORD_REUSE_MAX must be used together with PASSWORD_REUSE_TIME.

- PASSWORD_REUSE_MAX integer
    - The value must be a positive integer greater than 0.
- PASSWORD_REUSE_MAX UNLIMITED
    - If PASSWORD_REUSE_TIME is set to UNLIMITED, all previously used passwords can be reused.
    - If PASSWORD_REUSE_TIME is not UNLIMITED, no previously used passwords can be reused.
- PASSWORD_REUSE_MAX DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.

<a id="3ff6ecdf3017ff13"></a>
#### PASSWORD_REUSE_TIME

It sets the duration for which a previously used password is prohibited from being reused when a user attempts to reuse it.

PASSWORD_REUSE_TIME must be used together with PASSWORD_REUSE_MAX.

- PASSWORD_REUSE_TIME constant_expression 
    - It is the period during which the password cannot be reused. (in days)
    - The default unit is days.
    - For testing purposes, shorter duration can be specified using fractional values such as n/24 for hours, n/1,440 for minutes, or n/86,400 for seconds.
    - Valid range: 1 second (1/86400) to 100,000 days
- PASSWORD_REUSE_TIME UNLIMITED
    - If PASSWORD_REUSE_MAX is set to UNLIMITED, all previously used passwords can be reused.
    - If PASSWORD_REUSE_MAX is not UNLIMITED, no previously used passwords can be reused.
- PASSWORD_REUSE_TIME DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.

<a id="7e5f125023d95c42"></a>
#### PASSWORD_VERIFY_FUNCTION

It specifies the methods for verifying password complexity.

- PASSWORD_VERIFY_FUNCTION null
    - Password complexity verification is not performed.
- PASSWORD_VERIFY_FUNCTION DEFAULT
    - It follows the policy defined in the "DEFAULT" profile.
- PASSWORD_VERIFY_FUNCTION &lt;verify policy&gt;
    - It specifies the password complexity verification methods, which can be one of the following:
        - KISA_VERIFY_FUNCTION
        - ORA12C_VERIFY_FUNCTION
        - ORA12C_STRONG_VERIFY_FUNCTION
        - VERIFY_FUNCTION_11G 
        - VERIFY_FUNCTION

<a id="ed47a1082397ef1b"></a>
##### KISA_VERIFY_FUNCTION

It is the password verification method defined by KISA (Korea Internet & Security Agency).

- At least 8 characters, including:
- At least one letter
- At least one number
- At least one special character

<a id="580f1eb9f464a0c3"></a>
##### ORA12C_VERIFY_FUNCTION

It is the password verification method used by Oracle's ORA12C_VERIFY_FUNCTION.

- At least 8 characters, including:
- At least one letter
- At least one number
- Must not contain the database name
- Must not contain the username or the reversed username
- Must not contain the word *goldilocks*
- Must not contain the word *oracle*
- The following simple passwords are not allowed:
    - welcome1, database1, account1, user1234, password1, oracle123, computer1, abcdefg1, change_on_install 
- The new password must differ from the previous password by at least 3 characters.

<a id="c8d8d3b2740d0bde"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

It is the password verification method used by Oracle's ORA12C_STRONG_VERIFY_FUNCTION.

- At least 9 characters, including:
- At least 2 uppercase letters 
- At least 2 lowercase letters
- At least 2 numbers
- At least 2 special characters
- The new password must differ from the previous password by at least 4 characters.

<a id="2c2363408d3fc8c5"></a>
##### VERIFY_FUNCTION_11G

It is the password verification method used by Oracle's VERIFY_FUNCTION_11G.

- At least 8 characters, including:
- At least one letter
- At least one number
- Must not contain the username
- The new password must differ from the previous password by at least 3 characters.

<a id="c9b7839edd213d39"></a>
##### VERIFY_FUNCTION

It is the password verification method used by Oracle's VERIFY_FUNCTION.

- Password must differ from the username.
- At least 4 characters, including:
- At least one letter
- At least one number
- At least one special character
- The following simple passwords are not allowed:
    - welcome, database, account, user, password, oracle, computer, abcd
- The new password must differ from the previous password by at least 3 characters.

<a id="78b72664aabaa3e9"></a>
### Description

<a id="f6af1b16f6d62ef8"></a>
#### Account Lockout

The following parameters affect account lockout.

- FAILED_LOGIN_ATTEMPTS
- PASSWORD_LOCK_TIME

For example, when creating the following profile and user:

```
CREATE PROFILE prof LIMIT
    FAILED_LOGIN_ATTEMPTS 4
    PASSWORD_LOCK_TIME 30;

ALTER USER u1 PROFILE prof;
```

If user u1 fails to log in more than four times, the account is locked for 30 days and will be automatically unlocked afterward.

If PASSWORD_LOCK_TIME is set to UNLIMITED, the account lockout must be manually released using the ALTER USER statement.

```
ALTER USER user1 ACCOUNT UNLOCK;
```

<a id="5edd4334a32ab629"></a>
#### Password Expiration

The following parameters affect password expiration.

- PASSWORD_LIFE_TIME
- PASSWORD_GRACE_TIME

The password expires according to the following sequence.

1. Password is set.
** The password expiration time is defined as the period elapsed since the password was last changed, based on PASSWORD_LIFE_TIME.
** When the password expiration status is OPEN, normal login is allowed.

2. When a user logs in after the password has expired,
** The login is successful, but the password expiration status changes to EXPIRED (GRACE). The following warnings will be displayed:
*** ERR-28000(16310): The password will expire in n days
*** ERR-28000(16311): The password will expire soon
*** The SQL standard does not define the concept of password expiration.
*** 28000 is the authentication warning or the SQL standard status code of an error. 16310, 16311 are the GOLDILOCKS error codes.
** The password expiration time is reset based on the time elapsed since the user logged in, according to PASSWORD_GRACE_TIME.

3. When a user logs in after the grace period,
** The password expiration status changes to EXPIRED, and the user will not be able to log in. The following error occurs:
*** ERR-28000(16312): The password has expired
*** The SQL standard does not define the concept of password expiration.
*** 28000 is the authentication warning or SQL standard status code of an error. 16312 is the GOLDILOCKS error code.
*** The GOLDILOCKS internal error code 16312 should be used to control password re-entry through the program.

**Password expiration state transition**

<a id="94075ebce7e7b895"></a>
| Step | Timing | Login result | Password status |
| --- | --- | --- | --- |
| 1 | Password is changed | Success | OPEN |
| 2 | After PASSWORD_LIFE_TIME | Success with warning | EXPIRED(GRACE) |
| 3 | After PASSWORD_GRACE_TIME | Error | EXPIRED |

Refer to the following example.

```
CREATE PROFILE prof LIMIT
   PASSWORD_LIFE_TIME 90
   PASSWORD_GRACE_TIME 3;

ALTER USER u1 PROFILE prof;
```

In the above example, user u1 successfully logs in after 90 days, but receives a warning message that the password will expire in three days.

If the password is not changed within three days, it will expire.  
Once the password has expired, a message prompting the user to enter a new password is displayed at login, and access to the account is denied.

<a id="d33d6d181b895c0a"></a>
#### Password Reusability

The following are the parameters affecting password reusability.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

The password reusability of the two parameters above is determined according to the following table.

**Conditions for password reusability**

<a id="b5bb11db108f52e7"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | Conditions for password reusability |
| --- | --- | --- |
| value | value | Both PASSWORD_REUSE_TIME and PASSWORD_REUSE_MAX conditions must be met. |
| value | UNLIMITED | Always prohibited |
| UNLIMITED | value | Always prohibited |
| UNLIMITED | UNLIMITED | Always permitted |

If a profile is created as follows:

```
CREATE PROFILE prof LIMIT
   PASSWORD_REUSE_MAX 5
   PASSWORD_REUSE_TIME 3;
```

the last five passwords and any password changed within the past three days cannot be reused.

The following is an example of user u1's password change history. If the current password is P#_000007 and today's date is 2015-08-08, the reusability of previous passwords is as follows:

**Example of password reusability**

<a id="45b981dcd69cc2eb"></a>
| Password | Password_date | Password reusability status |
| --- | --- | --- |
| P#_000001 | 2015-08-01 | Possible |
| P#_000002 | 2015-08-02 | Possible |
| P#_000003 | 2015-08-03 | Violation of  REUSE_MAX |
| P#_000004 | 2015-08-04 | Violation of  REUSE_MAX |
| P#_000005 | 2015-08-05 | Violation of REUSE_MAX, REUSE_TIME |
| P#_000006 | 2015-08-06 | Violation of  REUSE_MAX, REUSE_TIME |
| P#_000007 | 2015-08-07 | Violation of  REUSE_MAX, REUSE_TIME |

The accumulated password change history used to check password reusability can be deleted using the following statement.

```
ALTER DATABASE CLEAR PASSWORD HISTORY;
```

<a id="b9616dd0d1bf89ec"></a>
#### DEFAULT profile

When the database is created, the following 'DEFAULT' profile is automatically generated. The password parameters of the 'DEFAULT' profile are as follows.

**Configuration of the DEFAULT profile**

<a id="73416f6ec3112f01"></a>
| Parameter | Value |
| --- | --- |
| FAILED_LOGIN_ATTEMPTS | 10 |
| PASSWORD_LOCK_TIME | 1 |
| PASSWORD_LIFE_TIME | 180 |
| PASSWORD_GRACE_TIME | 7 |
| PASSWORD_REUSE_MAX | UNLIMITED |
| PASSWORD_REUSE_TIME | UNLIMITED |
| PASSWORD_VERIFY_FUNCTION | NULL |

The default values of the "DEFAULT" profile have the following characteristics.

- Account lockout
    - If a user fails to log in 10 consecutive times (as specified by FAILED_LOGIN_ATTEMPTS), the account will be locked for 1 day (PASSWORD_LOCK_TIME).
- Password expiration
    - After 180 days (PASSWORD_LIFE_TIME) and following a 7-day (PASSWORD_GRACE_TIME) grace period, the password is considered expired. 
- Password reusability
    - Previous passwords can be reused. 
- Password complexity verification
    - No complexity check is performed.

The DEFAULT profile can not be dropped, but it can be altered as follows:

```
ALTER PROFILE DEFAULT LIMIT ...
```

<a id="d56ccae146b3ace0"></a>
### Examples

The following is an example of creating a profile to control account lockout. The account is locked for three days after three consecutive login failures.

```
gSQL> CREATE PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a profile to control password expiration. The password lifetime is 90 days, and the grace period is seven days.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a profile to control password reusability. This example does not require verifying the old password when changing the password.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a profile to enforce password complexity requirements.

```
gSQL> CREATE PROFILE prof1 LIMIT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile created.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a profile by setting all parameters.

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

<a id="7dadda6f383ffce1"></a>
### Compatibility

The SQL standard does not define the concept of the profile.

<a id="dcb8add42fd7e2a9"></a>
### For More Information

Refer to the following.

- [DROP PROFILE](#0c97ae81d474b49a)
- [ALTER PROFILE](18-sql-references-a-b.md#1107682b7d496cfb)
- [CREATE USER](#409f34806636a0ff)
- [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](18-sql-references-a-b.md#8cf16ad46dc69f8b)

<a id="635504efdc11b072"></a>
## CREATE ROLE

<a id="12284a667e6563a6"></a>
### Function

It defines the role.

<a id="ce12c070a200a97a"></a>
### Syntax

```
<role definition> ::=
    CREATE ROLE <role_name> [ WITHOUT GRANT ]
    ;
```

<a id="8a59525599b1cad2"></a>
### Invocation and Access Rules

The CREATE ROLE ON DATABASE privilege is required to execute the &lt;role definition&gt;.

> No additional privileges are granted to the created &lt;role_name&gt;.  
> By default, the user who creates the &lt;role_name&gt; is automatically granted the &lt;role_name&gt;.  
> Appropriate privileges must be granted to &lt;role_name&gt; to enable users assigned this &lt;role_name&gt; to access sessions and execute SQL statements.

<a id="1ed6b14040f597a8"></a>
### Syntax Rules and Parameters

<a id="8fcea54d8ad08ee2"></a>
#### &lt;role_name&gt;

It is the name of the role to be defined.  
There should be no existing user or role with the same name.   
The length of the &lt;role_name&gt; must be less than 128 bytes.

<a id="295b4096d997124f"></a>
#### WITHOUT GRANT

It does not grant the &lt;role_name&gt; to the user who created it.

<a id="2c79ae7cff198e22"></a>
### Description

The role is an authorization object that consists of a set of privileges.  
When performing a &lt;role definition&gt;, the role is defined without any privileges.  
Appropriate privileges should be granted to the role after it is defined.

By default, the user who creates a role is automatically granted that role.  
To avoid being granted the created role, define it using the WITHOUT GRANT option.

<a id="fc7328f3d14c8583"></a>
### Examples

A role can be defined by a user who has the CREATE ROLE ON DATABASE privilege.

- The following is an example of a user who has the CREATE ROLE ON DATABASE privilege.

```
gSQL> GRANT CREATE ROLE ON DATABASE TO u1;

Grant succeeded.

gSQL> commit;

Commit complete.

gSQL> \connect u1 u1

gSQL> CREATE ROLE role1;

Role created.
```

- The following is an example of a user who does not have the CREATE ROLE ON DATABASE privilege.

```
gSQL> \connect u2 u2

gSQL> CREATE ROLE role2;

ERR-42000(16210): lacks privilege (CREATE ROLE ON DATABASE)
```

By default, the created role is granted to the user who created it.  
If a role is created with the WITHOUT GRANT option, the created role is not granted to the creator.

- The following is an example of granting a role to the user who created it.

```
\connect u1 u1

gSQL> CREATE ROLE role1;

Role created.

gSQL> SELECT role_name
        FROM dba_roles 
       WHERE role_name = 'ROLE1';

ROLE_NAME
---------
ROLE1    

1 row selected.

gSQL> SELECT username , granted_role, admin_option
        FROM user_role_privs
       WHERE granted_role = 'ROLE1';

USERNAME GRANTED_ROLE ADMIN_OPTION
-------- ------------ ------------
U1       ROLE1        YES         

1 row selected.
```

- The following is an example of not granting a role to the user who created it.

```
\connect u1 u1

gSQL> CREATE ROLE role2 WITHOUT GRANT;

Role created.

gSQL> SELECT role_name
        FROM dba_roles 
       WHERE role_name = 'ROLE2';

ROLE_NAME
---------
ROLE2    

1 row selected.

gSQL> SELECT username , granted_role, admin_option
        FROM user_role_privs
       WHERE granted_role = 'ROLE2'; 

no rows selected.
```

Create an object under the role and grant it data manipulation privileges.  
Then, grant the role, which has privileges to create objects and perform data manipulation, to the user.  
The following is an example of a user who has been granted the role, creating an object and manipulating data.

```
gSQL> GRANT CREATE ANY TABLE, INSERT ANY TABLE ON DATABASE to role1;

Grant succeeded.

gSQL> GRANT create object on tablespace "MEM_DATA_TBS" to role1;

Grant succeeded.

gSQL> GRANT role1 TO u1;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee IN ( 'U1' , 'ROLE1' );

GRANTEE PRIVILEGE                                  
------- -------------------------------------------
ROLE1   CREATE ANY TABLE ON DATABASE               
ROLE1   INSERT ANY TABLE ON DATABASE               
ROLE1   CREATE OBJECT ON TABLESPACE "MEM_DATA_TBS" 
U1      CREATE SESSION ON DATABASE                 

4 rows selected.

gSQL> SELECT grantee, granted_role 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

GRANTEE GRANTED_ROLE
------- ------------
U1      ROLE1       

1 rows selected.

\connect u1 u1

gSQL> CREATE TABLE t1( c1 INTEGER , c2 INTEGER );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 , 2 );

1 row created.
```

<a id="7ecdaecfbf98932d"></a>
### Compatibility

**SQL standard compatibility**

<a id="43d16b0fed50dd15"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |

<a id="474a60053210b73c"></a>
### For More Information

Refer to [DROP ROLE](#9c173c3287657d63).

<a id="0173622cce38fc3c"></a>
## CREATE SCHEMA

<a id="26d04b099b9deeb1"></a>
### Function

It defines the schema.

<a id="5c9c4422656a9f13"></a>
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

<a id="6f7629824b074bbd"></a>
### Invocation and Access Rules

The user must satisfy the following conditions to perform &lt;schema definition&gt;.

- The CREATE SCHEMA ON DATABASE privilege is required to execute the schema.

- If a &lt;schema element&gt; exists, the privilege to perform each &lt;schema element&gt; is required.  
  For more information about access privileges, refer to the *invocation and access rules* in the following statements.
    - [CREATE TABLE](#47f3ce328094503e)
    - [CREATE VIEW](#5d56559b64b8b9ae)
    - [CREATE INDEX](#c758c010adf913ce)
    - [CREATE SEQUENCE](#630728df3a71a28b)
    - [GRANT privileges TO](#bd0f6497073f3a8e)
    - [COMMENT ON name IS](#a14777a330bd6a71)

- The user identified by user_identifier has the following privileges on the created schema:
    - The owner of the created schema schema_name
    - The owner of the objects created using the &lt;schema element&gt; clause

- Since no separate privileges are granted on the created schema, appropriate schema privileges must be granted in order to create objects.  
  For more information about the types of schema privileges, refer to [&lt;schema privilege&gt;](#9a864bad100ca61f) in the GRANT privileges TO statement.  
  For usage examples, refer to the [Examples](#d3c8a5d0abf0a0e7) provided in the CREATE USER statement.

<a id="c09f989090bdcf85"></a>
### Syntax Rules and Parameters

<a id="a95eac3cb62f1b5c"></a>
#### schema_name

It is the name of the schema to be created.  
An identical schema name must not already exist in the database.  
The length of the schema name must be less than 128 bytes.

<a id="265e7d387667af98"></a>
#### AUTHORIZATION user_identifier

If the schema name is omitted, a schema with the same name as the user_identifier is created.  
If AUTHORIZATION is not specified, the user_identifier of the user executing the statement is used.

<a id="b2e9e96c40d3bd60"></a>
#### schema_name AUTHORIZATION user_identifier

It specifies the schema name and the owner of the schema to be created.  
The owner can not be a role or PUBLIC.

<a id="40586fafb74816a7"></a>
#### &lt;schema element&gt;

It defines the objects to be created within the schema together with the schema at the time of schema creation.  
The schema_elements are executed in the specified order and are separated by whitespace, not commas.  
Objects cannot be defined under a schema with a name different from the schema being created.

- The &lt;grant privilege statement&gt; can be specified only for the following privileges:
    - &lt;schema privilege&gt;
    - &lt;table privilege&gt;
    - &lt;sequence privilege&gt;

- The &lt;comment statement&gt; can be specified only for the following objects:
    - SCHEMA schema_name
    - TABLE [schema_name].table_name
    - COLUMN [schema_name].table_name.column_name
    - INDEX [schema_name].index_name
    - SEQUENCE [schema_name].sequence_name
    - CONSTRAINT [schema_name].constraint_name

<a id="59034dd4ab1c65ee"></a>
### Description

A schema is an object that logically classifies SQL schema objects such as tables, views, indexes, sequences, and constraints.

In GOLDILOCKS, the relationship between a user and schemas is 1:N. In other words, a user may own no schemas at all, or may own multiple schemas.

The SQL standard does not clearly define the relationships among non-schema objects such as users, schemas, and databases, and each DBMS defines the relationships between these non-schema objects differently, as shown below.

> The relationship between users and schemas in other DBMSs  
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
>     - A user is a subordinate object of a database (or schema).
> 

<a id="6419136f658b3b34"></a>
### Examples

The following is an example of creating a schema.

```
gSQL> CREATE SCHEMA s1;

Schema created.
```

The following is an example of creating a schema and assigning its owner.

```
gSQL> CREATE SCHEMA s1 AUTHORIZATION test;

Schema created.
```

The following is an example of creating a schema along with the objects that belong to it.

```
gSQL> CREATE SCHEMA s1 
             CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) )
             CREATE INDEX idx_t1_id ON t1 ( id )
             COMMENT ON TABLE t1 IS 'comment on s1.t1'
;

Schema created.
```

<a id="5a4ec761a656a25f"></a>
### Compatibility

**SQL standard compatibility**

<a id="3780a383434ef23f"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="a8f614b213f12388"></a>
### For More Information

Refer to the following.

- [DROP SCHEMA](#2fd59a238a864111)
- [CREATE USER](#409f34806636a0ff)
- [CREATE TABLE](#47f3ce328094503e)
- [CREATE VIEW](#5d56559b64b8b9ae)
- [CREATE INDEX](#c758c010adf913ce)
- [CREATE SEQUENCE](#630728df3a71a28b)
- [GRANT privileges TO](#bd0f6497073f3a8e)
- [COMMENT ON name IS](#a14777a330bd6a71)

<a id="630728df3a71a28b"></a>
## CREATE SEQUENCE

<a id="9732524d75a2fd04"></a>
### Function

It creates a sequence.

<a id="603bd59e5b148113"></a>
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

<a id="5c2bd442018133b7"></a>
### Invocation and Access Rules

The user must have one of the following privileges to execute a &lt;sequence generator definition&gt; statement:  
• (CREATE SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence   
&nbsp;&nbsp;&nbsp;belongs  
• CREATE ANY SEQUENCE ON DATABASE

The sequence owner is determined as follows:  
• The owner of the schema to which the sequence belongs  
• If the schema to which the sequence belongs is PUBLIC, the owner is the user who executed the statement

The sequence owner has the USAGE ON SEQUENCE WITH GRANT OPTION privilege.

One of the following privileges is required to use the created sequence:  
• USAGE ON SEQUENCE for the sequence  
• (USAGE SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence   
&nbsp;&nbsp;&nbsp;belongs  
• USAGE ANY SEQUENCE ON DATABASE

<a id="8aa4a571fbf90ffc"></a>
### Syntax Rules and Parameters

<a id="8d71b7196ddace6c"></a>
#### sequence_name

It is the name of the sequence to be created, and it must be unique within the schema.  
The schema to which the sequence belongs can be specified using the format schema_name.sequence_name. If schema_name is omitted, the default schema of the user executing the statement is used.  
The length of the sequence name must be less than 128 bytes.

<a id="9fa3e373ae8d9abc"></a>
#### &lt;sequence generator option&gt;

If none of the &lt;sequence generator options&gt; are used, the following two statements have the same meaning.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="5e2520c8e5e49815"></a>
#### &lt;sequence generator start with option&gt;

It defines the first sequence number to be generated.  
Depending on whether the sequence is ascending or descending, it has the following characteristics.

- Ascending sequence (INCREMENT BY a positive number)
    - It is used when starting the sequence with a value greater than the minimum value.
    - If the START WITH clause is omitted, the default value is the minimum value (MINVALUE).
- Descending sequence (INCREMENT BY a negative number)
    - It is used when starting the sequence with a value smaller than the maximum value.
    - If the START WITH clause is omitted, the default value is the maximum value (MAXVALUE).

<a id="e50a54201fdff5d9"></a>
#### &lt;sequence generator increment by option&gt;

It defines the interval between sequence numbers.  
The constraints and characteristics are as follows.

- A positive or negative number is allowed, but 0 is not permitted.
- The absolute value of the interval must be smaller than the difference between MINVALUE and MAXVALUE.
- If the number is positive, an ascending sequence is generated; if negative, a descending sequence is generated.
- If the INCREMENT BY clause is omitted, the default is 1 (a positive number).

<a id="d1da86ae60157bc5"></a>
#### &lt;sequence generator maxvalue option&gt;

It defines the maximum value that can be generated by the sequence.

- MAXVALUE integer 
    - The maximum value range is between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of a 64-bit integer.
    - It must be greater than or equal to the START WITH value and greater than the MINVALUE value.
- NO MAXVALUE | NOMAXVALUE 
    - The maximum value is defined as follows:
        - For an ascending sequence, it is the maximum value (+9,223,372,036,854,775,807) of a 64-bit integer.
        - For a descending sequence, it is -1.
    - The reserved words NO MAXVALUE (SQL standard) and NOMAXVALUE have the same meaning, so either can be used.
- If neither MAXVALUE nor NO MAXVALUE is specified, the default is NO MAXVALUE.

<a id="feb20bb03e6b7966"></a>
#### &lt;sequence generator minvalue option&gt;

It defines the minimum value that can be generated by the sequence.

- MINVALUE integer 
    - The minimum value range is between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of a 64-bit integer. 
    - It must be less than or equal to the START WITH value, and less than the MAXVALUE value. 
- NO MINVALUE | NOMINVALUE 
    - The minimum value is defined as follows:
        - For an ascending sequence, it is 1. 
        - For a descending sequence, it is the minimum value (-9,223,372,036,854,775,808) of a 64-bit integer. 
    - The reserved words NO MINVALUE (SQL standard) and NOMINVALUE have the same meaning, so either can be used.
- If neither MINVALUE nor NO MINVALUE is specified, the default is NO MINVALUE.

<a id="c4453dbd512cbb54"></a>
#### &lt;sequence generator cycle option&gt;

It specifies whether to continue generating values when the sequence reaches its maximum or minimum value.

- CYCLE 
    - When an ascending sequence reaches its maximum value, it starts generating values again from the minimum value. 
    - When a descending sequence reaches its minimum value, it starts generating values again from the maximum value. 
- NO CYCLE | NOCYCLE 
    - When the sequence reaches its maximum or minimum value, it stops generating further sequence values. 
    - The reserved words NO CYCLE (SQL standard) and NOCYCLE have the same meaning, so either can be used.
- If neither CYCLE nor NO CYCLE is specified, the default is NO CYCLE.

<a id="f50ef72493d10ef6"></a>
#### &lt;sequence generator cache option&gt;

It defines the number of sequence values to preload into memory for faster access.  
When the database is restarted, the preloaded sequence values in memory are lost, and the sequence resumes from the next value after the last loaded one.

- CACHE integer 
    - The CACHE value must be greater than or equal to 2.
    - If CYCLE is specified, the CACHE value must not exceed the cycle length.
        - CYCLE length: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - Sequence values are not preloaded into memory.
- If neither CACHE nor NO CACHE is specified, the default is CACHE 20.

<a id="931ce86cc4f483aa"></a>
### Description

The created sequence object uses sequence values through the [NEXTVAL](17-built-in-function-references.md#bc1e3ceed22e9e15) and [CURRVAL](17-built-in-function-references.md#a9f13cbd9fea3680) functions.

The sequence value does not have transactional properties. The sequence retains the most recent value even if an error occurs in the SQL statement using the sequence function or if an explicit ROLLBACK is performed.

The CURRVAL function returns the most recent NEXTVAL value called within the session.  
By utilizing this feature, you can continue using the sequence value obtained by NEXTVAL in subsequent SQL statements. However, if NEXTVAL has not been called in the session, using CURRVAL will result in an error.

<a id="5b26b4d7840caefe"></a>
### Examples

The sequence object seq1, created without explicitly defining sequence options, is an ascending sequence by default. This means it behaves identically to the sequence object seq2 in the following example:

```
gSQL> CREATE SEQUENCE seq1;

Sequence created.


gSQL> CREATE SEQUENCE seq2 START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

Sequence created.
```

The following is an example of a sequence that generates an odd value.

```
gSQL> CREATE SEQUENCE seq1 START WITH 1 INCREMENT BY 2;

Sequence created.
```

The following is an example of creating a sequence that repeatedly generates even numbers starting from 0 up to 1000.

```
gSQL> CREATE SEQUENCE seq1 START WITH 0 MINVALUE 0 MAXVALUE 1000 INCREMENT BY 2 CYCLE;

Sequence created.
```

The following is an example of generating a descending sequence starting from -1.

```
gSQL> CREATE SEQUENCE seq1 INCREMENT BY -1;

Sequence created.
```

<a id="83e59d1bf400cd74"></a>
### Compatibility

The SQL standard does not define the &lt;sequence generator cache option&gt; clause.

**SQL standard compatibility**

<a id="f8b47df0f539dbb9"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="6102beb06cd82b63"></a>
### For More Information

Refer to the following.

- [DROP SEQUENCE](#125ff61843f5e7f3)
- [ALTER SEQUENCE](18-sql-references-a-b.md#59da3d9f8e5621cf)
- [NEXTVAL](17-built-in-function-references.md#bc1e3ceed22e9e15)
- [CURRVAL](17-built-in-function-references.md#a9f13cbd9fea3680)

<a id="3632eb462786e0cb"></a>
## CREATE SYNONYM

<a id="f87390678e0f2b54"></a>
### Function

It creates a synonym. A synonym is an alternative name for a table, view, sequence, or another synonym, and it can be used in the following statements.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="309e2ca3631a3dbb"></a>
### Syntax

```
<synonym definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="5a91082c0ad1ddb4"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute the &lt;synonym definition&gt; statement.

- The CREATE PUBLIC SYNONYM ON DATABASE privilege is required to create a public synonym by explicitly specifying PUBLIC.

- The owner of a public synonym is PUBLIC. The user who created the synonym does not have any privileges on it.

- One of the following privileges is required to create a private synonym.
    - (CREATE SYNONYM or CONTROL SCHEMA) ON SCHEMA for that schema
    - CREATE ANY SYNONYM ON DATABASE

- The owner of a private synonym is determined as follows:
    - The owner of the schema to which the private synonym belongs
    - If the schema to which the private synonym belongs is PUBLIC, then the owner is the user who executed the statement.

- If the user does not have privileges on the base object, the user is not allowed to execute statements using its synonym, even if the user created the synonym.

- Additionally, be cautious when granting privileges on a synonym, because doing so grants privileges on the base object that the synonym refers to.

<a id="5931556e00aa69ba"></a>
### Syntax Rules and Parameters

<a id="2b9132fee705e8a5"></a>
#### [ OR REPLACE ]

It replaces the existing synonym if the synonym already exists.

<a id="028b881a8fbbbd3d"></a>
#### [ PUBLIC ]

It is specified when creating a public synonym.  
If omitted, a private synonym is created.

<a id="edf6918eccc27da5"></a>
#### synonym_name

It is the name of the synonym to be created, and it must be unique within the schema.  
The schema to which the synonym belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.   
The length of the synonym name must be less than 128 bytes.  
A public synonym is a non-schema object; therefore, a schema name cannot be specified when creating a public synonym using the PUBLIC keyword.

<a id="06bfd0e3b7a66f43"></a>
#### object_name

The schema to which the object belongs can be defined using the format schema_name.table_name.  
If schema_name is omitted, the default schema of the user executing the statement will be used.

The object types for which object_name can be specified are as follows.

- Table
- View
- Sequence
- Another synonym

When a statement using a synonym is executed, checks are performed for object existence, cycles, and privileges.

<a id="f81a37f944db47a7"></a>
### Description

A synonym is an alternative name for a table, view, sequence, or another synonym.

If a synonym is created, applications do not need to be modified even when the underlying object changes; only the synonym needs to be redefined. This makes it convenient to manage changes.  
In addition, database security is improved by hiding the real names and schemas of objects, and usability is enhanced by allowing long object names to be replaced with shorter, more user-friendly names.

Since a synonym is literally an alternative name, creating it does not mean that the object can be accessed through the synonym. Appropriate privileges on the underlying object are required to access it.

When a statement is executed using a synonym, the object access procedure is as follows:

1. Look for a table with the specified name.
2. If the table does not exist, search for a private synonym with that name.
3. If no private synonym is found, search for a public synonym with that name.

```
gSQL> CREATE PUBLIC SYNONYM syn1 FOR u1.t1;

Synonym created.

gSQL> CREATE PUBLIC SYNONYM syn2 FOR syn1;

Synonym created.

gSQL> SELECT * FROM syn2;
```

The following describes the object access sequence in the above SELECT statement example:

1. It searched for the table syn2, but it does not exist. 
2. It searched for the private synonym syn2, but it does not exist. 
3. It searched for the public synonym syn2, and it exists. 
    1. It searched for the table syn1, but it does not exist. 
    2. It searched for the private synonym syn1, but it does not exist. 
    3. It searched for the public synonym syn2, and it exists. 
        1. It searched for the table u1.t1, and it exists.

<a id="fe7662a44cac5f3e"></a>
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

<a id="ed521f3b2adc6e04"></a>
### Compatibility

The SQL standard does not define the CREATE SYNONYM statement.

<a id="b566a88384f9a592"></a>
### For More Information

Refer to [DROP SYNONYM](#cc44cfa07d635430).

<a id="47f3ce328094503e"></a>
## CREATE TABLE

<a id="f58ca339a2ca2e1d"></a>
### Function

It defines a table.

<a id="2869233d737341d6"></a>
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
    | <references specification> [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]
    | <check constraint definition> 

<index name clause> ::=
    INDEX index_name

<index attributes> ::=
      <index physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )


<table constraint definition> ::=
    [ CONSTRAINT constraint_name ] <table constraint> [ <constraint characteristics> ]

<table constraint> ::=
      <unique constraint definition> [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]
    | <referential constraint definition> [ <index name clause> [ <index attributes> ] [ TABLESPACE index_tablespace_name ] ]
    | <check constraint definition>

<unique constraint definition> ::=
    { UNIQUE | PRIMARY KEY } ( <key column element> [, ...] )

<check constraint definition> ::= 
    CHECK ( search_condition ) 

<referential constraint definition> ::= 
    FOREIGN KEY ( <referencing column list> ) <references specification> [ <key constraint index option> ]

<references specification> ::=  
    REFERENCES <referenced table and columns> [ MATCH SIMPLE ] [ <referential triggered action> ] 

<referencing column list> ::=   
    <key column element> [, <key column element> ... ]   

<referenced table and columns> ::= 
    <table name> [ ( <referenced column list> ) ] 

<referenced column list> ::=  
    <column name list>         

<referential triggered action> ::=     
      <update rule> [ <delete rule> ]  
    | <delete rule> [ <update rule> ]  

<update rule> ::=       
    ON UPDATE <referential action>  

<delete rule> ::=     
    ON DELETE <referential action>  

<referential action> ::=      
      CASCADE 
    | SET NULL      
    | SET DEFAULT    
    | RESTRICT      
    | NO ACTION      

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
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]


<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ] [ <constraint enforcement> ] 
    | <constraint check time> [ [ NOT ] DEFERRABLE ] [ <constraint enforcement> ]
    | <constraint enforcement> 

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<constraint enforcement> ::=  
    [ NOT ] ENFORCED 

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="2cd4be2857b401a0"></a>
### Invocation and Access Rules

The differences between a stand-alone database and a cluster database are as follows:

- Stand-alone
    - It can not define a &lt;table sharding strategy&gt;.
    - It can not define a &lt;table global secondary index clause&gt;.
- Cluster
    - PRIMARY KEY and UNIQUE constraints must include all sharding keys.
    - It can not define deferrable constraints.

The user must satisfy the following conditions to execute a &lt;table definition&gt; statement.

- One of the following privileges is required on the schema where the table will be created.
    - (CREATE TABLE or CONTROL SCHEMA) ON SCHEMA for that schema
    - CREATE ANY TABLE ON DATABASE

- One of the following privileges is required on the tablespace where the table will be created.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- If constraints are created together with the table, one of the following privileges is required on the schema where the constraints will be created.
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for that schema
    - ALTER ANY TABLE ON DATABASE

- If the created constraint is a key constraint, one of the following privileges is required on the tablespace where the index will be created.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- To define a referential constraint, one of the following privileges is required:
    - REFERENCES on the referenced table
    - REFERENCES for each referenced column
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA on the schema to which the referenced table belongs
    - ALTER ANY TABLE ON DATABASE

- The owner of the table is determined as follows.
    - The owner of the schema to which the table belongs
    - If the schema to which the table belongs is PUBLIC, the owner is the user who executed the statement.

- The table owner has the following privileges for the created table.
    - The privileges for the table 
        - SELECT ON TABLE WITH GRANT OPTION 
        - INSERT ON TABLE WITH GRANT OPTION 
        - UPDATE ON TABLE WITH GRANT OPTION 
        - DELETE ON TABLE WITH GRANT OPTION 
        - TRIGGER ON TABLE WITH GRANT OPTION 
        - REFERENCES ON TABLE WITH GRANT OPTION 
        - LOCK ON TABLE WITH GRANT OPTION 
        - INDEX ON TABLE WITH GRANT OPTION 
        - ALTER ON TABLE WITH GRANT OPTION 
    - The privileges for all columns in the table. 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - The privileges for the constraint that was created together
        - The owner of that constraint
        - The owner of the index that was created together with the constraint

&lt;table sharding strategy&gt; statement can be used in a cluster system.

<a id="3d9278d124e86195"></a>
### Syntax Rules and Parameters

<a id="5b5d4adf46c16d6b"></a>
#### table_name

It is the table name to be created, and it must be unique within the schema.  
The schema to which the table belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.  
The length of the table name must be less than 128 bytes.

<a id="9a0d2edb45ff78e2"></a>
#### &lt;column definition&gt;

It defines the columns that configure the table.  
The table must include one or more column definitions.   
The column definition can include the data type, default value, automatically generated value, and constraints.

<a id="2e36f5fd75fe5667"></a>
#### column_name

It is name of the column that configures the table, and each column must have a unique name within the table.  
The length of the column name must be less than 128 bytes.

<a id="3afa8d27d216a04b"></a>
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
When defining a column with automatically generated values (&lt;identity column specification&gt;), its data type must be one of SMALLINT, INTEGER or BIGINT.  
For more information about data types, refer to [Data Type](11-sql-elements.md#d31560e2b64a41fa).

<a id="96c26b0c91be65d7"></a>
#### &lt;character length units&gt;

It specifies the length unit per character for character data types.

- CHARACTERS/CHAR assigns the maximum number of bytes required for a single character as its length unit. Therefore, a multi-byte character such as Hangul is treated as having a length of 1.
- OCTETS/BYTE assigns 1 byte as the length unit for a single character. As a result, a multi-byte character such as Hangul is treated as having a length equal to its actual byte size.
- If omitted, the setting defaults to the CHAR_LENGTH_UNITS property specified at the time the database was created.

The SQL standard defines CHARACTERS as the default value.

> The default value of the char length unit in other DBMSs is as follows:
> 
> - Oracle, DB2: OCTETS
> - MS-SQL, MySQL, PostgreSQL: CHARACTERS
> 

<a id="2c0fb4c27c2a4e12"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

It specifies the default value of a column.  
The &lt;default clause&gt; and &lt;identity column specification&gt; can not be used together.  
If both are omitted, the default value is NULL.

<a id="d666eeb539c786e2"></a>
#### &lt;default clause&gt;

The DEFAULT clause specifies the default value to be used when DEFAULT is explicitly stated in INSERT or UPDATE statements, or when the corresponding column name is omitted.

- When the DEFAULT clause is used 
    - e.g. CREATE TABLE t1 ( id INTEGER, name VARCHAR(32) DEFAULT 'anonymous' ); 
    - When a column is omitted 
        - INSERT INTO t1(id) VALUES ( 1 ); 
        - INSERT INTO t1(id) SELECT id FROM other_table; 
    - When a DEFAULT is specified 
        - INSERT INTO t1 DEFAULT VALUES; 
        - INSERT INTO t1 VALUES ( 2, DEFAULT ); 
        - UPDATE t1 SET name = DEFAULT;

The data type of the DEFAULT expression must be compatible with the column's data type.  
If it is not compatible, or if the expression is invalid, an error will occur.

```
--# result: error
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 0 );

ERR-22012(12122): divisor is equal to zero


--# result: success
CREATE TABLE t1 ( c1 INTEGER DEFAULT 1 / 1 );

Table created.
```

A DEFAULT expression can use any built-in functions, except for the following.

- Logical operators (AND, OR, NOT), comparison operators (=,>, ...)
- Stored function
- Column name
- Subquery expression

<a id="98890fd94ddb7e32"></a>
#### &lt;identity column specification&gt;

It defines a column with values that are automatically generated.

A table can have only one identity column.  
Even if the NOT NULL constraint is not explicitly specified, the identity column is treated as a not null column.

The &lt;identity column specification&gt; clause can not be used together with the DEFAULT clause. The &lt;identity column specification&gt; clause, like the DEFAULT clause, provides a default value in INSERT and UPDATE statements, or defines the default value to be used when the column name is omitted.

The method for generating values is defined as follows.

- GENERATED BY DEFAULT AS IDENTITY   
  When a user-defined value is provided, it is used. However, if a default value is required—similar to the DEFAULT clause—a value is automatically generated.
    - CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) );
    - (O) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS');
        - The user-defined value (12345) is inserted.
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS');
        - An automatically generated value is inserted into the id column.
    - (O) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - A user-defined value is inserted.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - An automatically generated value is inserted into the id column.
    - (O) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - A user-defined value is inserted.
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - An automatically generated value is inserted into the id column.

- GENERATED ALWAYS AS IDENTITY   
  A user-defined value is not allowed, and a default value should be generated automatically, as with the DEFAULT clause.
    - CREATE TABLE t1 ( id INTEGER GENERATED ALWAYS AS IDENTITY, name VARCHAR(32) ); 
    - (X) INSERT INTO t1 VALUES ( 12345, 'GOLDILOCKS'); 
        - Error: A user-defined value cannot be specified.
    - (O) INSERT INTO t1(name) VALUES ( 'GOLDILOCKS' ); 
        - An automatically generated value is inserted into the id column.
    - (X) INSERT INTO t1(id, name) SELECT other_id, other_name FROM other_table;
        - Error: A user-defined value cannot be specified.
    - (O) INSERT INTO t1(name) SELECT other_name FROM other_table;
        - An automatically generated value is inserted into the id column.
    - (X) UPDATE t1 SET id = 10000 WHERE id = 12345;
        - Error: A user-defined value cannot be specified.
    - (O) UPDATE t1 SET id = DEFAULT WHERE id = 12345;
        - An automatically generated value is inserted into the id column.

For more information about &lt;common sequence generator option&gt; and &lt;basic sequence generator option&gt;, which are options for creating an identity column, refer to [CREATE SEQUENCE](#630728df3a71a28b).

<a id="70ef153fb7aa294e"></a>
#### &lt;column constraint definition&gt;

It defines the following constraints for the column.

- NOT NULL constraints
- CHECK constraints
- UNIQUE constraints
- PRIMARY KEY constraints
- FOREIGN KEY constraints

<a id="7562f58f1074fedc"></a>
#### constraint_name

It is the name of the constraint and can be omitted.

If constraint_name is omitted, it will be automatically generated as follows.  
If the automatically generated name conflicts with an existing one, the constraint_name must be explicitly specified.

- NOT NULL constraints
    - "table_name" + "_" + "NOT_NULL" + "_" + "column_name"
- CHECK constraints
    - "table_name" + "_" + "CHECK" + "_" + "column_name"
- UNIQUE constraints
    - "table_name" + "_" + "UNIQUE" + "_" + "column_name"
- PRIMARY KEY constraints
    - "table_name" + "_" + "PRIMARY_KEY"
- FOREIGN KEY constraints
    - "table_name" + "_" + "FOREIGN_KEY" + "referencing_column_name" + "REFERENCES" + "_" + "referenced_table_name" + "_" + "referenced_column_name"

The length of the constraint name must be less than 128 bytes.

<a id="0107d684db0f4bf9"></a>
#### NOT NULL Constraint

NULL values are not allowed for the column.

<a id="acfcee22d5012787"></a>
#### CHECK Constraint

A CHECK constraint defines a condition that each row must satisfy.

The &lt;search_condition&gt; specified in the CHECK constraint must be a logical expression that returns a BOOLEAN value.

- (X) : CHECK( c1 + c2 )
- (O) : CHECK( c1 < c2 )

The constraint is considered satisfied when the result of &lt;search_condition&gt; is TRUE or UNKNOWN. If the result is FALSE, the constraint is violated.

When defining a CHECK constraint, the following restrictions must be observed:

- Subqueries are not allowed.
- References to other objects are not allowed.
    - (e.g., other tables, views, stored functions, sequences, etc.)
- Non-deterministic expressions are not allowed.
    - e.g., SYSDATE, CURRENT_DATE, CURRENT_USER, RANDOM(start, end), ...
- Pseudo columns are not allowed.
    - e.g., CURRVAL, NEXTVAL, ROWID, ROWNUM, LEVEL, ...
- A maximum of 32 columns can be used in a &lt;search_condition&gt;.
- Be cautious when using DATE/TIME literals, as their interpretation may vary depending on the format.
    - Examples of improper usage:
        - CHECK ( order_date > '2014-10-11' )
        - If the NLS_DATE_FORMAT is 'YYYY-MM-DD', it will be interpreted differently than if it is 'YYYY-DD-MM'.
        - CHECK ( order_date > TO_DATE( '14-10-11', 'RRRR-MM-DD' )
        - Using format strings like 'RR' or 'RRRR' can lead to ambiguous interpretation depending on the current year: e.g., interpreted as 1914 if before 1950, or 2014 if after 1950.
    - Recommended usage:
        - Use expressions that are not affected by NLS_DATE_FORMAT, such as:
        - CHECK ( order_date > DATE'2014-10-11' )
        - CHECK ( order_date > TO_DATE( '2014-10-11', 'YYYY-MM-DD' ) )

There is no priority among multiple CHECK constraints, and the system does not check for logical contradictions between them. Therefore, care must be taken when defining multiple CHECK constraints to ensure they do not conflict with each other.

```
CREATE TABLE t1 
(
   value1 INTEGER,
   value2 INTEGER,
   CONSTRAINT t1_check_1 CHECK ( value1 > value2 ),
   CONSTRAINT t1_check_2 CHECK ( value1 < 0 ),
   CONSTRAINT t1_check_3 CHECK ( value2 > 0 )
);
```

A CHECK constraint can only be dropped by using its constraint name.

```
ALTER TABLE t1 DROP CONSTRAINT t1_check_1;
```

<a id="a1b6ae970e491c4e"></a>
#### UNIQUE Constraint

Duplicate values are not allowed for the column, but NULL values are permitted.

<a id="7e6c71109593ea01"></a>
#### PRIMARY KEY Constraint

NULL values and duplicate values are not allowed in the column.  
Only one PRIMARY KEY constraint can be defined per table.

<a id="5ad53eb3db4e69ec"></a>
#### FOREIGN KEY Constraint

A FOREIGN KEY constraint, also known as a referential constraint, defines a relationship between a FOREIGN KEY column and a column that has a PRIMARY KEY or UNIQUE constraint.

The value in the FOREIGN KEY column must match a value in the referenced column that has a PRIMARY KEY or UNIQUE constraint.

However, if the FOREIGN KEY column contains a NULL value, the constraint is considered satisfied regardless of whether a matching value exists in the referenced column.

The table that defines the referential constraint is called the referencing table or child table. This table must be a base table; temp tables and views are not allowed.

<a id="fe2fee49f6ba4f10"></a>
##### &lt;referential constraint definition&gt;

A &lt;referential constraint definition&gt; is used to define a referential constraint.

When defining a referential constraint, the associated index is automatically created based on the &lt;referencing column list&gt; and the &lt;key constraint index option&gt;.

<a id="ae0f52b59588e9dc"></a>
##### &lt;referencing column list&gt;

The columns of the referencing table identified by the &lt;referencing column list&gt; are called referencing columns.

- Duplicate columns cannot be specified as referencing columns.
    - (X) FOREIGN KEY ( fk1, fk1 ) REFERENCES parent(pk1, pk2)
- Columns of type long varchar and long varbinary cannot be used as referencing columns.
- Even if the composition of the referencing columns is the same, it is possible to define multiple distinct referential constraints.
    - (O) FOREIGN KEY (fk1) REFERENCES parent1 (pk1)
    - (O) FOREIGN KEY (fk1) REFERENCES parent2 (pk2)

<a id="d9dace091039a3dd"></a>
##### &lt;references specification&gt;

When defining a FOREIGN KEY constraint as a column constraint, it must be specified using &lt;references specification&gt;. When defining it as a table constraint, it must be specified using &lt;referential constraint definition&gt;.

- When defining a FOREIGN KEY as a column constraint:

```
CREATE TABLE child ( fk1 INTEGER REFERENCES parent(pk) );
```

- When defining a FOREIGN KEY as a table constraint:

```
CREATE TABLE child ( fk1 INTEGER,
                     FOREIGN KEY (fk1) REFERENCES parent(pk) );
```

<a id="8d186b6fef12cac2"></a>
##### &lt;referenced table and columns&gt;

The table referenced by a referential constraint is called the referenced table or parent table.

- If the referencing table is a base table, the referenced table must also be a base table.
    - (X) FOREIGN KEY (fk1) REFERENCES viewed_table
- When the referenced table and the referencing table are the same, it is called a self-referencing relationship.
    - CREATE TABLE t1 ( pk INTEGER PRIMARY KEY, fk INTEGER REFERECNES t1(pk) );
- If only the parent table is specified, it must have a primary key.
    - CREATE TABLE parent1( pk INTEGER PRIMARY KEY );
    - CREATE TABLE parent2( uk INTEGER UNIQUE );
    - (O) CREATE TABLE child1 ( fk INTEGER REFERENCES parent1 );
    - (X) CREATE TABLE child2 ( fk INTEGER REFERENCES parent2 );

<a id="666443fa7883aa1e"></a>
##### &lt;referenced column list&gt;

The columns of the referenced table identified by the &lt;referenced column list&gt; are called referenced columns.

- The number of columns in the &lt;referencing column list&gt; and the &lt;referenced column list&gt; must be exactly the same.
    - (X) FOREIGN KEY (fk1) REFERENCES parent( pk1, pk2 )
- The n-th referencing column in the &lt;referenced column list&gt; refers to the n-th &lt;referencing column list&gt; in the referenced table.
    - FOREIGN KEY(fk1, fk2) REFERENCES parent( pk1, pk2)
        - fk1 -> pk1
        - fk2 -> pk2
    - FOREIGN KEY(fk1, fk2) REFERENCES parent( pk2, pk1)
        - fk1 -> pk2
        - fk2 -> pk1
- Referenced columns must be key columns that belong to a single primary constraint or unique constraint, ensuring that each row in the referenced table has a unique combination of values.
    - CREATE TABLE parent ( pk INTEGER PRIMARY KEY, c1 INTEGER );
    - (O) CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) );
    - (X) CREATE TABLE child ( fk INTEGER REFERENCES parent(c1) );
- The primary or unique constraint associated with the &lt;referenced column list&gt; must not be deferrable.
    - CREATE TABLE parent ( pk INTEGER PRIMARY KEY DEFERRABLE );
    - (X) CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) );
- Referenced columns cannot consist of key columns that are included in a unique index but are not part of any primary key or unique constraint.
    - CREATE TABLE parent ( c1 INTEGER );
    - CREATE UNIQUE INDEX parent_uk ON parent(c1);
    - (X) CREATE TABLE child ( fk INTEGER REFERENCES parent(c1) ); 
- Duplicate columns cannot be specified in the referenced column list.
    - (X) CREATE TABLE child ( fk1 INTEGER, fk2 INTEGER, FOREIGN KEY(fk1, fk2) REFERENCES parent(pk, pk) );
- If the &lt;referenced column list&gt; is omitted, the entire key defined by the primary constraint of the referenced table is used as the referenced columns.
    - In this case, the n-th referencing column of &lt;referenced column list&gt; refers to the n-th primary key of the referenced table.
    - CREATE TABLE parent( pk1 INTEGER, pk2 INTEGER, PRIMARY KEY(pk1,pk2) );
    - CREATE TABLE child ( fk1 INTEGER, fk2 INTEGER, FOREIGN KEY (fk1, fk2) REFERENCES parent );
        - fk1 -> pk1
        - fk2 -> pk2
- Even if the composition of referenced columns is the same, it is possible to define multiple distinct referential constraints.
    - (O) CREATE TABLE child ( fk1 INTEGER RERFERENCES parent(pk), fk2 INTEGER REFERENCES parent(pk) );
- The associated referencing and referenced columns must have compatible data types in terms of result type compatibility.
    - However, references between CHAR and VARCHAR types or between BINARY and VARBINARY types are not allowed.
    - CREATE TABLE parent( c1 CHAR(10) UNIQUE, c2 VARCHAR(10) UNIQUE);
    - (X) CREATE TABLE child ( fk VARCHAR(10) REFERENCES parent(c1) );
    - (O) CREATE TABLE child ( fk VARCHAR(10) REFERENCES parent(c2) );

<a id="64c4abb846ed63ee"></a>
##### &lt;referential triggered action&gt;

A &lt;referential triggered action&gt; consists of a referential update action and a referential delete action.

- The &lt;update rule&gt; specifies the referential update action,
- and the &lt;delete rule&gt; specifies the referential delete action.

Referential update actions and referential delete actions are collectively referred to as referential actions.

Referential actions are executed before the referential constraint is checked.

If an &lt;update rule&gt; is not specified in the &lt;referential constraint definition&gt;, the default &lt;referential action&gt; for the &lt;update rule&gt; is NO ACTION.

If a &lt;delete rule&gt; is not specified in the &lt;referential constraint definition&gt;, the default &lt;referential action&gt; for the &lt;delete rule&gt; is also NO ACTION.

<a id="6e08fe10f120838f"></a>
##### ON UPDATE CASCADE

When a referenced column in the referenced table is updated, the corresponding referencing column in the matching row of the referencing table is also updated accordingly.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON UPDATE CASCADE );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> UPDATE parent SET pk = 2 WHERE pk = 1;
1 row updated.

gSQL> SELECT * FROM child;
FK
--
 2
1 row selected.
```

<a id="392c5e77f8fa4a9a"></a>
##### ON UPDATE SET NULL

When a referenced column in the referenced table is updated, the corresponding referencing column in the matching row of the referencing table is updated to NULL.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON UPDATE SET NULL );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> UPDATE parent SET pk = 2 WHERE pk = 1;
1 row updated.

gSQL> SELECT * FROM child;
  FK
----
null
1 row selected.
```

<a id="272acda2197bda32"></a>
##### ON UPDATE SET DEFAULT

When a referenced column in the referenced table is updated, the corresponding referencing column in the matching row of the referencing table is updated to the default value.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER DEFAULT 0 REFERENCES parent(pk) ON UPDATE SET DEFAULT );
INSERT INTO parent VALUES ( 0 ), ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> UPDATE parent SET pk = 2 WHERE pk = 1;
1 row updated.

gSQL> SELECT * FROM child;
FK
--
 0
1 row selected.
```

<a id="795cbabe2c075973"></a>
##### ON UPDATE RESTRICT

If a matching row exists in the referencing table, the referenced column in the referenced table cannot be updated.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON UPDATE RESTRICT );
INSERT INTO parent VALUES (-1),(1);
INSERT INTO child  VALUES (-1),(1);
COMMIT;

gSQL> UPDATE parent SET pk = -pk;
ERR-23001(16660): referential constraint "PUBLIC"."CHILD_FOREIGN_KEY_FK_REFERENCES_PARENT_PK" restriction violated : can not delete or update parent row
```

ON UPDATE RESTRICT represents a stricter constraint than ON UPDATE NO ACTION.

- ON UPDATE RESTRICT: If a matching row exists, the update on the referenced row is immediately prohibited.
- ON UPDATE NO ACTION: Constraint checking is deferred until all updates are completed.

The difference between ON UPDATE RESTRICT and ON UPDATE NO ACTION can be summarized as follows.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) );
INSERT INTO parent VALUES (-1),(1);
INSERT INTO child  VALUES (-1),(1);
COMMIT;

gSQL> UPDATE parent SET pk = -pk;
2 rows updated.
```

<a id="375a99976da102ef"></a>
##### ON UPDATE NO ACTION

Only referential constraint checking is performed without any referential update action.

<a id="161747bd0f975b10"></a>
##### ON DELETE CASCADE

When a referenced row in the referenced table is deleted, all matching rows in the referencing table are also deleted.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON DELETE CASCADE );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> DELETE FROM parent WHERE pk = 1;
1 row deleted.

gSQL> SELECT * FROM child;
no rows selected.
```

<a id="f32b45d2c0cfd04b"></a>
##### ON DELETE SET NULL

When a referenced row in the referenced table is deleted, the corresponding referencing column in the matching row of the referencing table is updated to NULL.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON DELETE SET NULL );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> DELETE FROM parent WHERE pk = 1;
1 row deleted.

gSQL> SELECT * FROM child;
  FK
----
null
1 row selected.
```

<a id="4b3090a80a5d6778"></a>
##### ON DELETE SET DEFAULT

When a referenced row in the referenced table is deleted, the corresponding referencing column in the matching row of the referencing table is updated to the default value.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER DEFAULT 0 REFERENCES parent(pk) ON DELETE SET DEFAULT );
INSERT INTO parent VALUES ( 0 ), ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> DELETE FROM parent WHERE pk = 1;
1 row deleted.

gSQL> SELECT * FROM child;
FK
--
 0
1 row selected.
```

<a id="c43c13ae26d95caa"></a>
##### ON DELETE RESTRICT

If a matching row exists in the referencing table, the referenced row in the referenced table cannot be deleted.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER REFERENCES parent(pk) ON DELETE RESTRICT );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> DELETE FROM parent WHERE pk = 1;
ERR-23001(16660): referential constraint "PUBLIC"."CHILD_FOREIGN_KEY_FK_REFERENCES_PARENT_PK" restriction violated : can not delete or update parent row
```

ON DELETE RESTRICT represents a stricter constraint than ON DELETE NO ACTION.

- ON DELETE RESTRICT: If a matching row exists, the delete on the referenced row is immediately prohibited.
- ON DELETE NO ACTION: Constraint checking is deferred until all deletes are completed.

<a id="a9c2730fdf52f302"></a>
##### ON DELETE NO ACTION

Only referential constraint checking is performed without any referential delete action.

<a id="8347b7d423ac78ff"></a>
##### Usage Restrictions on &lt;referential triggered action&gt;

If a referencing column is a generated column, the following &lt;referential triggered action&gt; cannot be specified.

- UPDATE CASCADE
- UPDATE SET NULL
- UPDATE SET DEFAULT
- DELETE SET NULL
- DELETE SET DEFAULT

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );

gSQL>
CREATE TABLE child ( fk INTEGER GENERATED BY DEFAULT AS IDENTITY
                     REFERENCES parent(pk) ON DELETE SET NULL );
ERR-42000(16637): for referencing generated column, delete rule shall not specify SET NULL or SET DEFAULT : 
                     REFERENCES parent(pk) ON DELETE SET NULL )
                                                     *
ERROR at line 2:
```

<a id="bc27dcde4b9a6a15"></a>
#### &lt;index name clause&gt;

It specifies the index name to be created when a UNIQUE or PRIMARY KEY constraint is defined.

- INDEX index_name 
    - It defines the index name for the constraint.
    - A schema name cannot be used with it, and the index is created in the same schema as the constraint.

When a UNIQUE or PRIMARY KEY constraint is defined and the INDEX clause is omitted, an index that satisfies the constraint is automatically created.  
The automatically generated index name is assigned as "constraint_name" + "_INDEX".

- &lt;index attributes&gt; 
    - It specifies the physical attributes of the index to be created.
    - For more information, refer to [CREATE INDEX](#c758c010adf913ce).
- TABLESPACE index_tablespace_name 
    - It specifies the tablespace where the index will be created.
    - For more information, refer to [CREATE INDEX](#c758c010adf913ce).

<a id="ed1351cd864ccea3"></a>
#### &lt;table constraint definition&gt;

&lt;unique constraint definition&gt;

- When defining a table, constraints can be classified into two types based on their position in the statement.
    - The &lt;column constraint definition&gt; can be used when defining a column to specify a constraint on that individual column.
    - In contrast, the &lt;table constraint definition&gt; can be written separately from the column definitions and allows you to specify constraints on one or more columns.

Table constraint definitions differ from column constraint definitions in the following ways, syntactically.

- NOT NULL constraint 
    - It can not be specified using the table constraint definition.
- Unlike the column constraint definition, it must explicitly specify the column. 
    - UNIQUE constraint &lt;unique constraint definition&gt; 
        - UNIQUE ( column_name [, ...] ) 
    - PRIMARY KEY CONSTRAINT &lt;unique constraint definition&gt; 
        - PRIMARY KEY ( column_name [, ...] )

<a id="7d769dc3f124a0d1"></a>
#### key column element

It specifies the column that will be the target of the key.

- column name 
    - It is the name of the column that creates the key. 
- ASC | DESC 
    - ASC: The column is sorted in ascending order. 
    - DESC: The column is sorted in descending order. 
    - If not specified, the default value is ASC.
- NULLS FIRST | NULLS LAST 
    - NULLS FIRST: NULL values are placed before non-NULL values.
    - NULLS LAST: NULL values are placed after non-NULL values.
    - If not specified, the default value is NULLS LAST.

<a id="6992151ae8142273"></a>
#### &lt;table sharding strategy&gt;

It defines the sharding strategy for the table.  
One of the following four strategies can be specified.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

If omitted, the value is determined by the [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#b42b1ed9a19b2182) property.

- If the value of DEFAULT_SHARDING is 0
    - &lt;cloned strategy&gt;
- If the value of DEFAULT_SHARDING is 1
    - &lt;hash sharding strategy&gt;

<a id="64c8c8a37779dafd"></a>
#### &lt;cloned strategy&gt;

All data in the table is replicated to each shard.

<a id="bda3350ccefe521c"></a>
#### &lt;clone placement&gt;

It defines the placement strategy for a clone.

- AT CLUSTER WIDE 
    - Clones are placed on all cluster members across all cluster groups within the cluster system.
    - When a cluster group or cluster member is added, clones can be relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.
- AT CLUSTER GROUP group_list 
    - Clones are placed on all cluster members within the specified cluster group(s).
    - When a cluster member is added to the specified group(s), clones can be relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.
    - Adding a new cluster group does not affect the relocation of the clone.
- If omitted, the default value is AT CLUSTER WIDE.

<a id="8370d40ad06dcb90"></a>
#### &lt;hash sharding strategy&gt;

It shards the table data based on the hash value of the sharding key.

<a id="a8c00beaf9e1bfd9"></a>
#### SHARDING BY [HASH] ( column_list )

It defines the sharding key used for hash sharding.

- A maximum of 32 columns can be listed. 
- Duplicate columns are not allowed. 
- Columns of type LONG VARCHAR or LONG VARBINARY cannot be used.

<a id="d78d5dc00ccf258b"></a>
#### &lt;hash shard count&gt;

It defines the number of hash shards to be partitioned.  
The number of shards can be defined from 1 to 512.  
If omitted, the default value is 24.

<a id="79b30d9f6f1dce9c"></a>
#### &lt;hash shard placement&gt;

It defines the placement strategy for a hash shard.

- AT CLUSTER WIDE 
    - Shards are placed on all cluster members across all cluster groups within the cluster system.
    - When a cluster group or cluster member is added, shards can be relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.
- AT CLUSTER GROUP group_list 
    - Hash shards are placed on all cluster members within the specified cluster group(s).
    - The number of specified groups (group_list) must be less than or equal to the value of &lt;hash shard count&gt;.
    - Unlike range or list shards, a specific cluster group for a hash shard can not be specified. Instead, the system automatically determines which cluster group the shard will be placed in.
    - When a cluster member is added to the specified group(s), shards can be relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.
    - Adding a new cluster group does not affect the relocation of existing hash shards.
- If omitted, the default value is AT CLUSTER WIDE.

<a id="3e9d3e8b0947b393"></a>
#### &lt;range sharding strategy&gt;

It shards the table data based on the range of the sharding key values.

<a id="ff7a3ebf3ba11798"></a>
#### SHARDING BY RANGE ( column_list )

It defines the sharding key for range sharding.

- A maximum of 32 columns can be listed.
- Duplicate columns are not allowed.
- Columns of type LONG VARCHAR or LONG VARBINARY cannot be used.

<a id="d5f3485659bd12b4"></a>
#### &lt;cluster-wide range shard placement&gt;

Range shards are automatically distributed across all cluster groups in the cluster system.  
The AT CLUSTER WIDE clause must be specified before the &lt;range shard definition&gt;.  
When a cluster group or cluster member is added, shards can be automatically rebalanced using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.

- Create a range-sharded table.
- Distribute six shards across the existing cluster groups (g1, g2, and g3).

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

- Relocate the range shards.
- Distribute six shards across the cluster groups g1, g2, g3, and the newly added g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="38310b0d38cba270"></a>
#### &lt;group-specific range shard placement&gt;

Range shards are placed in the specified cluster group.  
The AT CLUSTER GROUP group_name clause is used along with the &lt;range shard definition&gt; to specify where the shard should be placed.  
When a cluster member is added to the specified cluster group, shards can be automatically relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.  
Adding a new cluster group does not affect the relocation of existing range shards.

- Create a range-sharded table.
- Place each range shard in the specified cluster group.

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

- Add a new cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate a range shard.
- The shard is not placed in the newly created cluster group, g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="7f0133a3aa580724"></a>
#### &lt;range shard definition&gt;

The SHARD range_name must be unique within a table

Up to 512 &lt;range shard definition&gt; can be defined.

The listed &lt;range shard definition&gt; are sorted in the order of their &lt;range value clause&gt;, and each must use a different &lt;range value clause&gt;.

The &lt;range shard definition&gt; in which all values are defined as MAXVALUE is called the MAX shard.  
A MAX shard must exist, and there must be only one.

- It must include a MAX shard.

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

- If a MAX shard is not include, an error will occur.

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

<a id="faa2e8f59ab8447c"></a>
#### &lt;range value clause&gt;

&lt;range value&gt; must be a constant or MAXVALUE (the maximum value).

NULL can not be used as a &lt;range value&gt;.

- (O) SHARD s1 VALUES LESS THAN ( 1 ) 
- (O) SHARD s2 VALUES LESS THAN ( 1 + 1 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE ) 
- (X) SHARD s4 VALUES LESS THAN ( SYSDATE ) 
- (X) SHARD s5 VALUES LESS THAN ( NULL )

MAXVALUE is always greater than any other value, including NULL.

If there are multiple sharding keys, only MAXVALUE can be specified after a MAXVALUE.

- (O) SHARD s1 VALUES LESS THAN ( 100, MAXVALUE ) 
- (X) SHARD s2 VALUES LESS THAN ( MAXVALUE, 100 ) 
- (O) SHARD s3 VALUES LESS THAN ( MAXVALUE, MAXVALUE )

If a sharding key is defined using multiple columns, there must be a single MAX shard that specifies MAXVALUE for all columns, as shown in SHARD s3 below.

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

<a id="96460f689f46332a"></a>
#### &lt;list sharding strategy&gt;

It shards the table data based on the list of the sharding key values.

<a id="78e102dd658e002c"></a>
#### SHARDING BY LIST ( column_name )

It defines the sharding key for list sharding.

- Only one column can be used. 
- Columns of type LONG VARCHAR or LONG VARBINARY cannot be used.

<a id="b4d476a5b2bd6802"></a>
#### &lt;cluster-wide list shard placement&gt;

List shards are automatically distributed across all cluster groups in the cluster system.  
The AT CLUSTER WIDE clause must be specified before the &lt;range shard definition&gt;.  
When a cluster group or cluster member is added, shards can be automatically rebalanced using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.

- Create a list-sharded table.
- Distribute five shards across the existing cluster groups (g1, g2, and g3).

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

- Relocate the list shards.
- Distribute five shards across the cluster groups g1, g2, g3, and the newly added g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="1aed860555a8a8c2"></a>
#### &lt;group-specific list shard placement&gt;

List shards are placed in the specified cluster group.  
The AT CLUSTER GROUP group_name clause is used along with the &lt;list shard definition&gt; to specify where the shard should be placed.  
When a cluster member is added to the specified cluster group, shards can be automatically relocated using the [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#f207258645781242) statement.  
Adding a new cluster group does not affect the relocation of existing list shards.

- Create a list-sharded table.
- Place each list shard in the specified cluster group.

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

- Add a new cluster group.

```
CREATE CLUSTER GROUP g4 
       CLUSTER MEMBER g4n1 HOST '192.168.0.41' PORT 10401
;
```

- Relocate a list shard.
- The shard is not placed in the newly added cluster group, g4.

```
ALTER TABLE t1 REBALANCE;
```

<a id="e801cf709a59b8d3"></a>
#### &lt;list shard definition&gt;

The LIST list_name must be unique within a table.

Up to 512 &lt;list shard definition&gt; can be defined.   
All &lt;list value&gt; in the listed &lt;list shard definition&gt; must be distinct.

DFFAULT refers to all values not included in the listed &lt;list value&gt;.  
DFFAULT can not be specified together with any other value.  
A shard that includes DEFAULT is called the DEFAULT shard.

A MAX shard must exist, and there must be only one.

- It must include a DEFAULT shard.

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

- If a DEFAULT shard is not included, an error will occur.

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

<a id="a5f28b5498f44555"></a>
#### &lt;list value clause&gt;

&lt;list value&gt; must be a constant.

NULL or DEFAULT can be used as a &lt;list value&gt;.

- (O) SHARD s1 VALUES IN ( 1, 1 + 1, 3, 4 ) 
- (O) SHARD s2 VALUES IN ( 5, 6, 7, NULL ) 
- (O) SHARD s3 VALUES IN ( DEFAULT ) 
- (X) SHARD s4 VALUES IN ( DEFAULT, 8, 9, 10 ) 
- (X) SHARD s5 VALUES IN ( current_timestamp, systimestamp ) 
- (X) SHARD s6 VALUES IN ( c1, c2 )

<a id="6b68c9f909f34928"></a>
#### &lt;table physical attribute clause&gt;

It defines the physical attributes of the table.

- PCTFREE integer 
    - Definition 
        - It specifies the reserved space on a page to accommodate potential increases in row size during updates or modifications
        - Initially, data is inserted excluding this reserved space.
        - If the reserved space defined by PCTFREE is insufficient, ROW MIGRATION may occur when data is updated or modified.
    - Valid values range from 0 to 99.
    - If omitted, the default value is 10.

- PCTUSED integer 
    - Definition 
        - It specifies the minimum percentage of a page that can be used for row data and overhead before a new row can be added to the page.
        - In other words, if the space usage on a page falls below the PCTUSED value due to updates or deletions, that page becomes eligible for new row inserts.
    - Valid values range from 0 to 99.
    - If omitted, the default value is 40.

- INITRANS integer 
    - Definition 
        - It specifies the initial number of concurrent transactions that can access a page simultaneously. 
        - If the number of users accessing the index is low, set INITRANS to a lower value; if there are many concurrent users, set it higher.
        - The value can automatically increase up to the configured MAXTRANS if needed.
    - Valid values range from 1 to 32.
    - If omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of concurrent transactions that can access a page. 
    - Valid values range from 1 to 32.
    - If omitted, the default value is 8.

<a id="f3f0bda246debae5"></a>
#### &lt;index physical attribute clause&gt;

It defines the physical attributes of the index.

- PCTFREE integer 
    - Definition
        - It specifies the amount of space reserved on a page to control the frequency of page splits caused by key insertions.
        - This applies only during index bottom-up builds.
    - Valid values range from 0 to 99.
    - If omitted, the value set in the DEFAULT_INDEX_PCTFREE property is used.
- INITRANS integer 
    - It is the same as INITRANS in the &lt;table physical attribute clause&gt;. 
- MAXTRANS integer 
    - It is the same as MAXTRANS in the &lt;table physical attribute clause&gt;.

<a id="4caa5da842e6fc27"></a>
#### &lt;segment attr clause&gt;

It describes the storage information for the table.

- INITIAL integer 
    - Definition 
        - It specifies the size of the physical space initially allocated when the table is created.
        - If the integer value is less than or equal to two EXTENTs, it is set to the size of two EXTENTs.
        - If the integer value is greater than two EXTENTs, it is aligned to the TABLESPACE’s EXTENT size.
    - The minimum value is 1, and the maximum value depends on the system environment. 
    - If omitted, the default value is the size of two EXTENTs of the TABLESPACE to which the table belongs.

- NEXT integer 
    - Definition 
        - It specifies the size of physical space to be allocated when additional space is needed for the table.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' will be treated as 8192 bytes.)
        - The behavior of NEXT depends on the remaining available space, calculated as the difference between MAXEXTENTS and the space currently used by the table:  
      - If the remaining space is 0, no further space can be allocated.  
      - If the remaining space is greater than 0 but less than NEXT, only the remaining space is allocated.  
      - If the remaining space is greater than or equal to NEXT, space equal to NEXT is allocated.
    - The minimum value is 1, and the maximum depends on the system environment. 
    - If omitted, the default is the size of a single EXTENT in the table’s TABLESPACE.

- MAXSIZE integer 
    - Definition 
        - It specifies the maximum amount of space that can be allocated to the table.
        - If the integer value is less than or equal to two EXTENTs, it is set to the size of two EXTENTs.
        - If the integer value is greater than two EXTENTs, it is aligned to the TABLESPACE’s EXTENT size.
    - The minimum value is 1, and the maximum depends on the system environment. 
    - If omitted, the default value is 32 terabytes (35,184,372,088,832).
    - If a value greater than 32 terabytes is specified, it will be automatically adjusted to 32 terabytes.

<a id="cc86132775cdbf56"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If omitted, bytes are used by default.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ce897f684c521f38"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace where the table will be stored.  
If the TABLESPACE clause is omitted, the default tablespace_name of the user executing the statement is used.

<a id="e41e75f2683ebc4c"></a>
#### TABLESPACE index_tablespace_name

It specifies the name of the tablespace where the index will be stored.  
If the TABLESPACE clause is omitted, the user's index tablespace is used.  
If the user's index tablespace is NULL, DISK tables use the user's default data tablespace, and MEMORY tables use the user's default temporary tablespace.

<a id="f539b339b9be68a3"></a>
#### &lt;constraint characteristics&gt;

It defines the characteristics of a constraint.  
The following characteristics can be specified when defining a constraint.

- DEFERRABLE | NOT DEFERRABLE
- &lt;constraint check time&gt;
- ENFORCED | NOT ENFORCED

If &lt;constraint characteristics&gt; is omitted, it is set to NOT DEFERRABLE INITIALLY IMMEDIATE ENFORCED.

<a id="76ed64edeec20432"></a>
#### DEFERRABLE | NOT DEFERRABLE

It specifies whether constraint checking is deferrable, allowing constraints to be checked at COMMIT time instead of during DML statement execution.

The checking time of deferrable constraints is controlled by the [SET CONSTRAINTS](20-sql-references-h-z.md#99b7c8cb97aff1bd) statement.

- NOT DEFERRABLE
    - The constraint checking time can not be deferred; constraints are checked when executing INSERT, DELETE, or UPDATE statements. 
- DEFERRABLE
    - The constraint checking time can be controlled using the [SET CONSTRAINTS](20-sql-references-h-z.md#99b7c8cb97aff1bd) statement.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - Checks the constraint during DML execution. 
    - SET CONSTRAINTS constraint_name DEFERRED
        - Checks the constraint at COMMIT time. 
- If not explicitly specified, the default depends on &lt;constraint check time&gt;:
    - Specifying INITIALLY IMMEDIATE means the constraint checking time is NOT DEFERRABLE.
    - Specifying INITIALLY DEFERRED means the constraint checking time is DEFERRABLE.
    - If &lt;constraint check time&gt; is not specified, the constraint checking time is NOT DEFERRABLE by default.

<a id="166a0ed4d9dc65a8"></a>
#### &lt;constraint check time&gt;

If the constraint is DEFERRABLE, it sets the initial timing for when the constraint is checked.

- INITIALLY IMMEDIATE
    - The constraint is checked at the time the DML statement is executed. 
- INITIALLY DEFERRED
    - The constraint is checked at the time the COMMIT statement is executed.
    - This option cannot be used with NOT DEFERRABLE.
- If not specified, the default is INITIALLY IMMEDIATE.

For more information about deferrable constraints, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#99b7c8cb97aff1bd).

<a id="8a739365261d82a9"></a>
#### &lt;constraint enforcement&gt;

It specifies whether the constraint is enabled or disabled.

- NOT ENFORCED: Disabled
- ENFORCED: Enabled

If not specified, the default is ENFORCED.

<a id="36abcc6c0ed84fde"></a>
#### &lt;table global secondary index clause&gt;

It defines a global secondary index for the table.

- WITH GLOBAL SECONDARY INDEX [ &lt;index attributes&gt; [...] ] [ TABLESPACE tablespace_name ]
    - It creates a global secondary index when the table is created in a cluster system environment. 
    - &lt;index attribute&gt;
        - It sets an index attribute of the global secondary index.
    - TABLESPACE tablespace_name
        - It specifies the tablespace in which to create the global secondary index.
- WITHOUT GLOBAL SECONDARY INDEX
    - It prevents the creation of a global secondary index when creating a table in a cluster system environment.

<a id="58293569fb6bb261"></a>
### Description

<a id="b8fbaafde8ac224f"></a>
#### Constraint Characteristics

GOLDILOCKS automatically creates an index to enforce uniqueness when creating key constraints.

The following types of columns do not allow NULL values:

- Columns with a NOT NULL constraint
- Columns that are part of a primary key constraint
- Identity columns

<a id="89d1f17f58011628"></a>
#### Cluster Table

In a cluster environment, a table manages data using one of the following sharding strategies:

- Cloned table
    - It replicates all table data and places it across the cluster system.
- Hash-sharded table
    - It distributes table data into multiple shards based on the hash value of a sharding key, and stores them across the cluster system.
- Range-sharded table
    - It distributes table data into multiple shards based on value ranges of a sharding key, and stores them across the cluster system.
- List-sharded table
    - It distributes table data into multiple shards based on specific list values of a sharding key, and stores them across the cluster system.

The sharding strategy is determined based on the following factors when creating a table. In a cluster system, tables are classified as code tables or fact tables according to their characteristics.

- Code table 
    - A code table refers to a table such as a product list or a provider list, where the amount of data is relatively small and infrequently updated
    - This type of table is often referenced together with a fact table. 
- Fact table 
    - A fact table refers to a table such as a transaction history or a call history, where the amount of data is relatively large and frequently updated. 
    - Because the data volume is large, sharding is required.

The &lt;cloned strategy&gt; is suitable for code tables. For fact tables, an appropriate &lt;table sharding strategy&gt; should be selected based on the table's access pattern.

<a id="60eec938e00a9c8f"></a>
### Examples

The following is an example of creating a regular table.

```
gSQL> CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
);

Table created.
```

The following is an example of defining constraints on columns when creating a table.

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

The following is an example of specifying a constraint that includes multiple columns when creating a table.

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

The following is an example of specifying a column with an automatically generated values and a default value when creating a table.

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

The following is an example of specifying the tablespace in which the table will be stored when creating it.

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

The following is an example of defining a cluster-wide cloned table. The table data is duplicated and distributed across the entire cluster system.

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

The following is an example of defining a group-specific cloned table. The table data is duplicated and placed in the cluster groups g1 and g2 as specified by the user.

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

The following is an example of defining a cluster-wide hash-sharded table. The table data is divided into 24 shards based on the hash value of the ps_partkey column, and each shard is automatically distributed across the entire the cluster system.

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

The following is an example of defining a group-specific hash-sharded table. The table data is divided into 24 shards based on the hash value of the ps_partkey column, and each shard is automatically placed in the specified cluster groups g2 and g3.

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

The following is an example of defining a cluster-wide range-sharded table. The table data is divided into 24 shards based on the range values of the D_ID column, and each shard is automatically distributed across the entire cluster system.

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

The following is an example of defining a group-specific range-sharded table. The table data is divided into three ranges based on the range values of the NO_D_ID column, and shard s1 is assigned to cluster group g1, shard s2 to cluster group g2, and shard s3 to cluster group g3, respectively

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

The following is an example of defining a cluster-wide list-sharded table. The table data is divided into five list shards based on the city column, and each shard is automatically distributed across the entire cluster system.

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

The following is an example of defining a group-specific list-sharded table. The table data is divided into five list shards based on the city column, and each shard is placed in a specified cluster group.

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

The table T1 is created without defining a global secondary index.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITHOUT GLOBAL SECONDARY INDEX;

Table created.
```

After creating table T1, a global secondary index is created on it.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) )  WITH GLOBAL SECONDARY INDEX;

Table created.
```

After creating table T1, a global secondary index on T1 is created in the USER_DATA_TBS tablespace as a logging index.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_DATA_TBS;

Table created.
```

After creating table T1, a global secondary index on T1 is created in the USER_TEMP_TBS tablespace as a nologging index.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      TABLESPACE USER_TEMP_TBS;

Table created.
```

<a id="dd4ef1de7fc4c415"></a>
### Compatibility

The SQL standard does not define the following clauses.

- Physical concepts such as the TABLESPACE clause and the &lt;physical attribute clause&gt;. 
- The SQL standard does not allow operations in the DEFAULT clause.

**&lt;table definition&gt;**

<a id="9baf3d883e665b88"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T171 | LIKE clause in table definition | X |
| F531 | Temporary tables | X |
| S051 | Create table of type | X |
| S043 | Enhanced reference types | X |
| S081 | Subtables | X |
| T172 | AS subquery clause in table definition | O |
| T173 | Extended LIKE clause in table definition | X |
| T180 | System-versioned tables | X |
| T181 | Application-time period tables | X |

**&lt;column definition&gt;**

<a id="f3465f329b5e513a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F692 | Extended collation support | X |
| T174 | Identity columns | O |
| T175 | Generated columns | X |
| T180 | System-versioned tables | X |

**&lt;default clause&gt;**

<a id="9ef0f03a9a50ff18"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F321 | User authorization | O |
| T322 | Extended roles | X |
| F762 | CURRENT_CATALOG | O |
| F763 | CURRENT_SCHEMA | O |

**&lt;unique constraint definition&gt;**

<a id="609709e7c50735fa"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S291 | Unique constraint on entire row | X |
| T591 | UNIQUE constraints of possibly null columns | O |
| T181 | Application-time period tables | X |
| F292 | UNIQUE null treatment | X |

**&lt;referential constraint definition&gt;**

<a id="8cf02849643b9a75"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T191 | Referential action RESTRICT | O |
| F741 | Referential MATCH types | X |
| F191 | Referential delete actions | O |
| F701 | Referential update actions | O |
| T201 | Comparable data types for referential constraints | O |
| T181 | Application-time period tables | X |

**&lt;check constraint definition&gt;**

<a id="b0f06fb8256a4d10"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F671 | Subqueries in CHECK constraints | X |
| F672 | Retrospective CHECK constraints | O |
| F673 | Reads SQL-data routine invocations in CHECK constraints | X |

<a id="b2584f89c9c0ffde"></a>
### For More Information

Refer to the following.

- [DROP TABLE](#5324bfcd0073e53b)
- [ALTER TABLE](18-sql-references-a-b.md#c0fe1090ab6b3bb1)
- [CREATE TABLESPACE](#8ab1dca3b8dad438)
- [CREATE SCHEMA](#0173622cce38fc3c)
- [CREATE INDEX](#c758c010adf913ce)
- [CREATE SEQUENCE](#630728df3a71a28b)
- [SET CONSTRAINTS](20-sql-references-h-z.md#99b7c8cb97aff1bd)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#c0be2a6bcfa14f9c)

<a id="13b906a980351a1f"></a>
## CREATE TABLE AS SELECT

<a id="e32be8cd58ec011b"></a>
### Function

It creates a new table from the query result.

<a id="3d87c99806c62f60"></a>
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
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]

<table global secondary index clause> ::=
      WITH GLOBAL SECONDARY INDEX [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    |  WITHOUT GLOBAL SECONDARY INDEX
```

<a id="cbf77228cf4f31a5"></a>
### Invocation and Access Rules

A user must meet the following conditions to execute a &lt;table definition:AS query expression&gt; statement.

- Table creation privilege
    - Refer to the access privileges for the [CREATE TABLE](#47f3ce328094503e) statement
- SELECT privilege 
    - Refer to the access privileges for the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="907c41481214390d"></a>
### Syntax Rules and Parameters

<a id="9775fc2809f60ec0"></a>
#### table_name

It is the name of the table to be created.  
For more information, refer to the [table_name](#5b5d4adf46c16d6b) clause.

<a id="4c980292f4e5cdfd"></a>
#### column_name_list

These are the names of the columns that make up the table. Each name must be unique within the table, and the number of columns must match the number of result columns in the SELECT clause.  
If not specified, the column names from the SELECT clause in the &lt;query expression&gt; are used.

However, if an expression (such as a function, operation, or subquery) is used instead of a column in the SELECT clause, an alias or column name must be explicitly specified.

The column name must be less than 128 bytes in length.

<a id="d9dbfdc12faa5d30"></a>
#### WITH [NO] DATA

If WITH DATA is specified, the result of the SELECT clause is inserted into the table being created.  
If WITH NO DATA is specified, the result of the SELECT clause is not inserted into the table.  
If omitted, it behaves as if WITH DATA were specified.

<a id="0317e4e8fc9c21ab"></a>
#### Other Syntax

For more information about other syntaxes, refer to the syntax of the [CREATE TABLE](#47f3ce328094503e) statement.

<a id="05f9dea3b7a6cd10"></a>
### Description

When executing the CREATE TABLE AS SELECT statement, if a column with a NOT NULL constraint is specified in the SELECT list, the NOT NULL constraint is also created in the new table. However, if the NOT NULL constraint is deferrable, it is not created in the new table.

However, if the NOT NULL constraint was not explicitly created, but the column has a NOT NULL property such as being a primary key or an identity column, the NOT NULL constraint is not created in the new table.

<a id="3ae4230607e2ebb5"></a>
### Examples

The following is an example of executing the CREATE TABLE AS SELECT statement.

```
gSQL> CREATE TABLE recent_orders 
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

The following is an example of specifying column names.

```
gSQL> CREATE TABLE recent_orders ( order_id, order_item, order_date )
                AS SELECT order_id, order_item, order_date
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
Table created.
```

The following is an example of using a function in the SELECT list.

```
gSQL> CREATE TABLE recent_orders ( order_date, order_count )
                AS SELECT order_date, COUNT(*) 
                   FROM orders 
                   WHERE order_date >= '2015-03-03'
                   GROUP BY order_date;
Table created.
```

The following is an example of a statement that includes WITH DATA.

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

The following is an example of a statement that includes WITH NO DATA.

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

<a id="28b41e80a1c91df1"></a>
### Compatibility

The CREATE TABLE AS SELECT statement follows the SQL standard. However, the following is an extension beyond the standard.

- The SQL standard requires parentheses around the SELECT clause; however, in GOLDILOCKS, they are optional.
- Similarly, the SQL standard mandates the use of the WITH [NO] DATA clause, but this is also optional in GOLDILOCKS.
- The tablespace concept in GOLDILOCKS is an extended feature that is not part of the SQL standard.

**SQL standard compatibility**

<a id="dbf91523e99fd8b1"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="09f8b8420ca0b4fc"></a>
### For More Information

Refer to the following.

- [CREATE TABLE](#47f3ce328094503e)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)

<a id="8ab1dca3b8dad438"></a>
## CREATE TABLESPACE

<a id="d51f3b012d47d9d2"></a>
### Function

It creates a tablespace.

<a id="75fda44e88057ac3"></a>
### Syntax

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="c0fdb8984e0dfe3b"></a>
### Invocation and Access Rules

The CREATE TABLESPACE ON DATABASE privilege is required to execute the &lt;create tablespace statement&gt;.

The user who executes the statement is granted the CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="60f7c41e9bc3f2f4"></a>
### Syntax Rules and Parameters

<a id="eb5345b7fba4d718"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

This is a memory temporary tablespace used to store no-logging indexes or temporary objects, such as intermediate results generated during query processing.  
The reserved word MEMORY can be omitted.

<a id="259c9cd3b69ebf0d"></a>
#### &lt;memory data tablespace clause&gt;

It defines a memory data tablespace.  
For more information, refer to the [CREATE MEMORY DATA TABLESPACE](#8f6b0a901e93d0d4) statement.

<a id="a93eaba38d50e5c3"></a>
#### &lt;memory temporary tablespace definition&gt;

It defines a memory temporary tablespace.  
For more information, refer to the [CREATE MEMORY TEMPORARY TABLESPACE](#a09ab566de521b1a) statement.

<a id="7f5b4976b998163d"></a>
### Description

For more information, refer to the description of each detailed clause.

<a id="cf1e2bdca1c4bd0d"></a>
### Example

For more information, refer to the usage examples for each detailed clause.

<a id="9fa366febbcdeccd"></a>
### Compatibility

The SQL standard does not define the concept of the tablespace.

<a id="a33b4f475e9e2b7b"></a>
### For More Information

Refer to the following.

- [DROP TABLESPACE](#9b31e9a7a77c3aed)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)

<a id="409f34806636a0ff"></a>
## CREATE USER

<a id="4f82055303b20319"></a>
### Function

It defines a database user.

<a id="97855d413e08b5cc"></a>
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

<a id="36ef61bc06f934fe"></a>
### Invocation and Access Rules

The CREATE USER ON DATABASE privilege is required to execute the &lt;user definition&gt;.

The created user, user_identifier, has ownership privileges for the schema created with the &lt;schema&gt; clause.

> No separate privileges are granted to the created user_identifier.  
> Appropriate privileges must be granted to user_identifier to allow access and execution of SQL statements.

<a id="cbf5ea05631dc428"></a>
### Syntax Rules and Parameters

<a id="c75adc4221f09ad0"></a>
#### user_identifier

It is the username to be created.  
An identical username (user identifier) or role (role name) must not already exist.  
The length of the user_identifier must be less than 128 bytes.

<a id="7cba056d3634f5ca"></a>
#### password

It is the user's password to be created. It is encrypted and stored.  
The password length must be less than 128 bytes.  
The password is case-sensitive.  
It must start with an alphabetic character and can include alphabetic characters, numbers, underscores (_), and dollar signs ($).  
Other special characters must be enclosed in double quotes (").

<a id="3353898d5f909278"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

The profile for the password management policy is assigned as follows:

- PROFILE profile_name
    - It assigns the profile_name created by a user.
- PROFILE DEFAULT
    - It assigns the default profile named DEFAULT.
- PROFILE NULL
    - It does not assign any profile.

If the PROFILE clause is omitted, it is treated as PROFILE NULL, and no profile is applied.  
For more information about password management policies, refer to the [CREATE PROFILE](#98c2f8112f164605) statement.

<a id="4b61f82efadc5b61"></a>
#### PASSWORD EXPIRE

It expires the user's password.  
It is used to force the user to change their password before logging in.

<a id="9c4bc4ec6a9bf729"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - It locks the user account. 
- ACCOUNT UNLOCK
    - It unlocks the user account.

<a id="f8d5b0f1917aa3ce"></a>
#### DEFAULT TABLESPACE tablespace_name

It specifies the default TABLESPACE where objects created by the user, such as tables and indexes (LOGGING), are stored.  
If the DEFAULT TABLESPACE clause is omitted, the default data tablespace (MEM_DATA_TBS) defined at DATABASE creation is assigned.

<a id="9ad32259ee18e524"></a>
#### TEMPORARY TABLESPACE tablespace_name

It specifies the TABLESPACE to store temporary tables created by the user, indexes (NOLOGGING), and intermediate results generated during query processing.  
If the TEMPORARY TABLESPACE clause is omitted, the default temporary tablespace (MEM_TEMP_TBS) defined at database creation is assigned.

<a id="5da1788c2c055d32"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

It specifies the default TABLESPACE to store index objects created by the user.

- Specifying INDEX TABLESPACE tablespace_name
    - If a data tablespace is specified, the index becomes a LOGGING index.
    - If a temporary tablespace is specified, the index becomes a NOLOGGING index.

- INDEX TABLESPACE NULL
    - It does not specify an index tablespace.

If the INDEX TABLESPACE clause is omitted, it defaults to INDEX TABLESPACE NULL.

<a id="6a68b7470555f963"></a>
#### &lt;schema clause&gt;

It creates the default schema for the user.  
The schema name must be unique within the database

- WITH SCHEMA [schema_name] 
    - If schema_name is not specified, a schema with the same name as user_identifier is created.
    - The user's SCHEMA PATH is set as schema_name.
- WITHOUT SCHEMA 
    - It does not create a schema to be owned by the user.
    - The user's SCHEMA PATH is set to PUBLIC.

If the &lt;schema clause&gt; is not specified, the default is WITH SCHEMA, and a schema with the same name as user_identifier is created.  
A schema to be owned by the user can also be created separately using the [CREATE SCHEMA](#0173622cce38fc3c) statement.

<a id="036a3bd82108b096"></a>
### Description

A user is an authorization object that consists of a set of privileges.

When the &lt;user definition&gt; statement is executed for the first time, a user is created without any privileges. Appropriate privileges must be granted afterward, as needed.

In GOLDILOCKS, the relationship between a user and schemas is 1 : N.  
In other words, a user may own multiple schemas or none at all.

The SQL standard does not explicitly define the relationship between non-schema objects such as users, schemas, and databases.  
On the other hand, each DBMS defines the relationships between non-schema objects differently, as shown below.

> Relationship Between User and Schema in Other DBMSs  
> 
> 
> - Oracle
>     - User : schema = 1 : 1.
> 
> 
> 
> - DB2 
>     - Users are identical to OS users.
>     - There are no separate SQL statements to create or drop users.
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
>     - A user is considered a subordinate object of a database (schema).
> 

<a id="d3c8a5d0abf0a0e7"></a>
### Examples

To allow creating a user and enabling that user to create objects and manipulate data, the following privileges must be granted.

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
GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE 
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

The following is an example of object creation by a user.

• It requires the CREATE SESSION ON DATABASE privilege.

```
gSQL> \connect u1 u1_password
```

• It requires the CREATE TABLE ON SCHEMA u1 privilege.   
• It requires the CREATE OBJECT ON TABLESPACE mem_data_tbs privilege.

```
gSQL> CREATE TABLE u1.t1 ( c1 INTEGER, c2 INTEGER ) TABLESPACE mem_data_tbs;

Table created.

gSQL> COMMIT;
```

• It requires the CREATE INDEX ON SCHEMA u1 privilege.   
• It requires the CREATE OBJECT ON TABLESPACE mem_temp_tbs privilege.

```
gSQL> CREATE INDEX u1.idx ON t1 (c2) TABLESPACE mem_temp_tbs;

Index created.

gSQL> COMMIT;
```

• It requires the CREATE SEQUENCE ON SCHEMA u1 privilege.

```
gSQL> CREATE SEQUENCE u1.seq;

Sequence created.

gSQL> COMMIT;

gSQL> INSERT INTO u1.t1 VALUES ( u1.seq.NEXTVAL, u1.seq.NEXTVAL );

1 row created

gSQL> COMMIT;
```

<a id="34f44eca5216c662"></a>
### Compatibility

While the SQL standard covers the concept of a user, it does not specify the SQL statements for user creation and deletion.

<a id="1d5ecfa2300d8f57"></a>
### For More Information

Refer to the following.

- [DROP USER](#7979783b911846c2)
- [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2)
- [CREATE SCHEMA](#0173622cce38fc3c)

<a id="5d56559b64b8b9ae"></a>
## CREATE VIEW

<a id="120273a0d3c5ec45"></a>
### Function

It defines a view.

<a id="1fb9e91b5aa94a3c"></a>
### Syntax

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="49aa8a0443c78527"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute a &lt;view definition&gt; statement.

- One of the following privileges is required to create a view.
    - (CREATE VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
    - CREATE ANY VIEW ON DATABASE

- When using the OR REPLACE clause, if the view already exists, one of the following privileges is required to replace the existing view.
    - The owner of that view
    - CONTROL TABLE ON TABLE for that view.
    - (DROP VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
    - DROP ANY VIEW ON DATABASE

- For every table referenced in the &lt;query expression&gt; clause, one of the following privileges is required.
    - SELECT(columns) ON TABLE on all columns used in the statement
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

- The owner of the created view is determined as follows.
    - The owner of the schema to which the view belongs. 
    - If the schema to which the view belongs is PUBLIC, then it is the user who executed the statement.

- The owner of a view has the following privileges on the created view.
    - SELECT ON TABLE WITH GRANT OPTION 
    - INSERT ON TABLE WITH GRANT OPTION 
    - UPDATE ON TABLE WITH GRANT OPTION 
    - DELETE ON TABLE WITH GRANT OPTION 
    - TRIGGER ON TABLE 
    - LOCK ON TABLE WITH GRANT OPTION 
    - ALTER ON TABLE WITH GRANT OPTION

<a id="ff71a94f66c07a3e"></a>
### Syntax Rules and Parameters

<a id="51981fce58750ace"></a>
#### [ OR REPLACE ]

It replaces the existing view if the view already exists.

<a id="e6c144f3ae872361"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - A view is created regardless of whether the &lt;query expression&gt; is valid.
- NO FORCE 
    - A view is created only if &lt;Query expression&gt; is valid.
- The default setting is NO FORCE.

<a id="7636f28f650edb6f"></a>
#### view_name

It is the name of the view to be created, and it must be unique within the schema.  
The schema to which the view belongs can be defined using the format schema_name.view_name. If schema_name is omitted, the default schema name of the user executing the statement is used.  
The length of the view name must be less than 128 bytes.

<a id="cc6c683d58f317a7"></a>
#### [ ( column_name [, ...] ) ]

It defines the names of the columns that make up the view.  
Each column name must be unique within the view.

The number of columns must match the number of columns returned by the SELECT clause.

If the list of column names is omitted, the column names from the SELECT clause in the query expression are used.

<a id="d059b573e9f16195"></a>
##### AS &lt;query expression&gt;

It is the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) query used to create the view.

The &lt;query expression&gt; must not include the following variables.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE object

<a id="8984896295c466cf"></a>
### Description

A view is an object that assigns a name to a query and is used in a similar way to a table.

When a query that includes a view is executed, the view is interpreted as the query defined in the view definition.  
As in the following example, if a table referenced by the view is modified, elements such as an asterisk (*) in the view definition are automatically reinterpreted according to the updated structure of the table.

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

A view may be affected if it is created using the FORCE option while the query contains errors, or if the tables or views it references are modified or deleted.

This information can be retrieved from the INFORMATION_SCHEMA.VIEWS.

- IS_COMPILED column
    - TRUE: The view was successfully created without errors. 
    - FALSE: The view was created with existing errors using the FORCE option.
- IS_AFFECTED column
    - TRUE : A table or view referenced by this view has been modified.
    - FALSE: Since the view was created and compiled, none of the referenced tables or views have been modified.

There is no limit to the number of views that can be created or the number of columns within a view. Therefore, as long as there is sufficient storage space, views can continue to be created without restriction.

<a id="12a4bb23761ffbff"></a>
### Examples

The following is an example of creating a view.

```
gSQL> CREATE VIEW v1 AS SELECT * FROM t1 WHERE dept_id = 101;

View created.
```

The following is an example of defining column names while creating a view.

```
gSQL> CREATE VIEW v1 ( v_id, v_name )
          AS SELECT id, name FROM t1 WHERE dept_id = 101;

View created.
```

The following is an example of dropping an existing view and creating a new one using the REPLACE option.

```
gSQL> CREATE OR REPLACE VIEW v1(id, name) 
             AS SELECT id, name FROM t1;

View created.
```

The following is an example of forcing the creation of a view using the FORCE option, even when the objects referenced by the view do not exist.

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

<a id="2ffe9c22e2ac40b4"></a>
### Compatibility

The SQL standard does not define the following clauses.

- [ OR REPLACE ] clause 
- [ FORCE | NO FORCE ] clause

**SQL standard compatibility**

<a id="5f6c34d1b10b6efa"></a>
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

<a id="8ea84a6252d880b2"></a>
### For More Information

Refer to the following.

- [DROP VIEW](#5a1fec21848fd68b)
- [ALTER VIEW](18-sql-references-a-b.md#119e4fa9e88f98df)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)

<a id="ccb6dc5ecb7cf850"></a>
## DECLARE cursor_name

<a id="12df7cec0925d7aa"></a>
### Function

It declares a cursor.

<a id="1a864300f6b3a278"></a>
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

<a id="780ad5b71fe37d59"></a>
### Invocation and Access Rules

A dynamic cursor that uses a statement_name can be used in embedded SQL.

Appropriate access privileges are required depending on the type of the &lt;cursor query&gt;.  
For more information about access privileges, refer to the following:

- Access privileges for a [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement
- Access privileges for a [SELECT .. FOR UPDATE](20-sql-references-h-z.md#1cd99ab297830a3f) statement
- Access privileges for a [INSERT INTO name RETURNING](20-sql-references-h-z.md#9b221e074482cce0) statement
- Access privileges for a [UPDATE name RETURNING](20-sql-references-h-z.md#f9a91742fa4c7945) statement
- Access privileges for a [DELETE FROM name RETURNING](#43d479588fc6bc18) statement

<a id="e6441d41af88d9ab"></a>
### Syntax Rules and Parameters

<a id="82c01f24e27c2e95"></a>
#### cursor_name

It specifies the name of the cursor to be declared.  
The name must be unique within the session.  
The length of the cursor name must be less than 128 bytes.

<a id="8455caceb5893edd"></a>
#### { FOR | IS }

According to the SQL standard, either FOR or IS is used as a syntax keyword.

<a id="38077b6eee5f875d"></a>
#### &lt;cursor properties&gt;

It defines the properties of the cursor.

- If &lt;cursor sensitivity&gt; is not specified, the default is INSENSITIVE. 
- If &lt;cursor scrollability&gt; is not specified, the default is NO SCROLL. 
- If &lt;cursor holdability&gt; is not specified, the default is determined by &lt;cursor updatability&gt;.

<a id="4a98be2081bc0a30"></a>
#### updatable query

To use a cursor property such as SENSITIVE or FOR UPDATE, a query of the cursor should identify changes in rows of the base table, or it should be the updatable query which can acquire a lock on the row.

An updatable query must satisfy all of the following conditions:

- The top-level query must not contain DISTINCT.
    - (X) SELECT DISTINCT * FROM t1;
- The top-level query must not contain GROUP BY, HAVING, or any aggregate functions.
    - (X) SELECT MAX(c1) FROM t1;
- The query must not be a returning query.
    - (X) DELETE FROM t1 RETURNING c1;
- Set operators must not be used
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2;
- At least one updatable column must exist in the tables listed in the FROM clause.
    - Columns from tables involved in join operations (excluding cross joins) are not considered updatable.
        - FULL OUTER JOIN is not a cross join.
        - NATURAL JOIN is not a cross join.
        - INNER JOIN using the USING phrase is not a cross join.
    - Columns from the following types of tables are not updatable.
        - Dictionary tables, fixed tables, performance views
    - Columns in a view are not updatable.

<a id="34eb32df88dff7ad"></a>
#### &lt;cursor sensitivity&gt;

It determines whether data changes that affect the query results can be detected while operating the cursor.

- INSENSITIVE 
    - It does not detect data changes that occur during cursor operation. 
- SENSITIVE 
    - The &lt;cursor query&gt; must be an updatable query.
    - It detects data that is updated (UPDATE) or deleted (DELETE) within the same transaction as the cursor. 
    - It also detects data that is updated or deleted by other transactions after they are committed. 
- ASENSITIVE 
    - Whether the cursor is INSENSITIVE or SENSITIVE depends on the type of &lt;cursor query&gt;.
        - If the query is updatable, it is considered SENSITIVE. 
        - If the query is not updatable, it is considered INSENSITIVE.
- If not explicitly specified, the default is INSENSITIVE.

<a id="dbcf0eecd32bcf92"></a>
#### &lt;cursor scrollability&gt;

It specifies whether the result set of the cursor can be fetched sequentially or non-sequentially.

- NO SCROLL 
    - Only sequential FETCH (FETCH NEXT) is allowed. 
- SCROLL 
    - Non-sequential FETCH is allowed.
- If not explicitly specified, the default is NO SCROLL.

<a id="ec9732d6305b4b75"></a>
#### &lt;cursor holdability&gt;

It specifies whether the cursor remains open after a transaction is committed.

- WITH HOLD 
    - The cursor remains open even after a COMMIT.
    - It can not be used with the FOR UPDATE clause.
    - It can not be used with the [INSERT INTO name RETURNING](20-sql-references-h-z.md#9b221e074482cce0) statement. 
    - It can not be used with the [UPDATE name RETURNING](20-sql-references-h-z.md#f9a91742fa4c7945) statement. 
    - It can not be used with the [DELETE FROM name RETURNING](#43d479588fc6bc18) statement.
    - It can not be used in queries that include a global temporary table with a table commit action of ON COMMIT DELETE ROWS.

- WITHOUT HOLD 
    - The cursor is closed when the transaction is COMMITTED or ROLLED BACK.

- Rollback and cursors
    - When a transaction is rolled back, all cursors opened within the transaction are closed.
    - If rolled back to a savepoint, cursors created after that savepoint are closed.

- If not explicitly specified, the default value of &lt;cursor holdability&gt; is determined by &lt;cursor updatability&gt;:
    - If the cursor is FOR READ ONLY or &lt;cursor updatability&gt; is not specified, the default is WITH HOLD.
    - If the cursor is used with FOR UPDATE clause, the default is WITHOUT HOLD.

<a id="e472210cf9fdbf24"></a>
#### &lt;odbc cursor type&gt;

This cursor type is defined in the ODBC standard and supports the SCROLL property.

- STATIC CURSOR 
    - This cursor type is equivalent to INSENSITIVE SCROLL in the SQL standard.
    - Non-sequential FETCH operations are supported.
    - In the ODBC standard, this corresponds to the static scroll cursor.
- KEYSET CURSOR 
    - This cursor type is equivalent to ASENSITIVE SCROLL in the SQL standard.
    - It corresponds to the keyset-driven scroll cursor in the ODBC standard.
    - The sensitivity of a cursor is determined by the following characteristics:

**Determining sensitivity based on FOR [UPDATE / READ ONLY] clause and query type**

<a id="c30ffc396db4555c"></a>
| Updatability | Query type | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="483d3bc30e01a1b8"></a>
#### &lt;cursor specification&gt;

It defines the query to be targeted by the cursor.  
When statement_name is used, a dynamic cursor is declared, meaning the query is not yet defined.  
When &lt;cursor query&gt; is used, a standing cursor is declared, meaning the query is already defined.

<a id="5e8b0ec09ac4b8fc"></a>
#### statement_name

It is a statement_name referenced by the cursor and can be used in embedded SQL.

The statement_name must exist before executing the &lt;declare cursor&gt; statement, and the SQL statement referenced by statement_name must be a query prepared using the [PREPARE statement_name](20-sql-references-h-z.md#ff813c116e09eff4) statement.

If it is not a query, an error will occur when the [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3) statement is executed.

<a id="8da2984ae500d2e9"></a>
#### &lt;cursor query&gt;

For more information about the types of queries that can be used with a cursor, refer to the following.

- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#1cd99ab297830a3f)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#9b221e074482cce0)
- [UPDATE name RETURNING](20-sql-references-h-z.md#f9a91742fa4c7945)
- [DELETE FROM name RETURNING](#43d479588fc6bc18)

<a id="1ea3837b1321aef1"></a>
#### &lt;updatability clause&gt;

It specifies whether to modify rows using the cursor.

- FOR READ ONLY 
    - It declares a read-only cursor.
- FOR UPDATE 
    - It declares a writable cursor. 
    - When the cursor is opened, an X lock is acquired on the corresponding rows to prevent changes by other transactions until the transaction ends.
    - It can not be used together with the WITH HOLD clause.
    - The &lt;cursor query&gt; must be an updatable query.
- If not specified, the default is FOR READ ONLY.

<a id="5f8fc838cb4dc24d"></a>
#### FOR UPDATE OF …

It lists the columns related to lock acquisition when opening the cursor.

- For columns listed in the FOR UPDATE OF clause:
    - Each column must be updatable and belong to a table specified in the FROM clause of the &lt;SELECT statement&gt;.
    - Locks are acquired on the tables that contain the listed columns. 
- If only FOR UPDATE is used (without specifying columns):
    - It has the same effect as listing all updatable columns of the tables in the FROM clause of the &lt;SELECT statement&gt;.
    - Locks are acquired on all tables containing updatable columns.

<a id="6b7e7a09917d85f6"></a>
#### &lt;lock wait mode&gt;

It is used with the FOR UPDATE clause to specify the lock acquisition behavior.

- WAIT 
    - Locks are acquired for all rows in the query result when the cursor is opened.
    - The operation waits until the locks can be acquired.
- WAIT second 
    - Locks are acquired for all rows in the query result when the cursor is opened.
    - If the locks cannot be acquired within the specified time, an error is raised.
    - The value is in seconds and can range from 0 to 1,000,000,000.
- NOWAIT 
    - Locks are acquired for all rows in the query result when the cursor is opened.
    - If the locks cannot be acquired immediately, an error is raised.
- If not specified, the default is WAIT.

<a id="d453cc9ad1d20ca0"></a>
### Description

When controlling query properties, using the DECLARE CURSOR, OPEN, FETCH, and CLOSE statements may impose a greater performance overhead compared to using cursors through ODBC or JDBC.  
This is because these SQL statements manage server-side cursors directly.

Before executing a query, cursor properties can be controlled using ODBC and JDBC statements.  
The method of controlling SQL cursor properties using the DECLARE CURSOR statement, along with the corresponding cursor property control methods in the ODBC and JDBC standards, is as follows.

<a id="60bed383329726b5"></a>
<table class="table column_count_4"><caption>Cursor property control in ODBC/ JDBC</caption><thead><tr><th class="to_center to_middle"><div>Property</div></th><th class="to_center to_middle"><div>GOLDILOCKS 
cursor property</div></th><th class="to_center to_middle"><div>ODBC standard cursor property</div></th><th class="to_center to_middle"><div>JDBC standard cursor property</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>Not configurable</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>Not configurable</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>Not configurable</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>Not configurable</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>Not configurable</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>Not configurable</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>Not configurable</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

The SQL cursor declarations corresponding to ODBC cursor types are as follows.

**SQL cursor declaration corresponding to ODBC cursor types**

<a id="f560da12ea63afb0"></a>
| ODBC cursor type | SQL cursor declaration |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

The SQL cursor declarations corresponding to JDBC cursor types are as follows.

**SQL cursor declaration corresponding to JDBC cursor types**

<a id="a260e210e8550561"></a>
| JDBC cursor type | SQL cursor declaration |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | KEYSET CURSOR |

<a id="ec140cf3249f48e5"></a>
### Examples

The following is an example of declaring and using a cursor with interactive SQL (gsql).

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

The following is an example of declaring a KEYSET cursor, performing sequential fetches, completing the transaction for UPDATE and DELETE statements, and then fetching in the reverse direction.

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

The following is an example of declaring a SCROLL cursor and using it with fetch orientations.

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

<a id="af4cc0d8b0f612a5"></a>
### Compatibility

The &lt;declare cursor&gt; statement differs from the SQL standard in the following ways:

- In the SQL standard, the default value for &lt;cursor sensitivity&gt; is ASENSITIVE, whereas in GOLDILOCKS, the default is INSENSITIVE.
- The following &lt;odbc cursor type&gt; are not defined in the SQL standard.
    - STATIC CURSOR 
    - KEYSET CURSOR 
- In the SQL standard, the default for &lt;cursor holdability&gt; is WITHOUT HOLD, but in GOLDILOCKS, the default varies depending on the &lt;cursor updatability&gt;.
- The SQL standard only allows a &lt;select statement&gt; as a &lt;cursor query&gt;. However, GOLDILOCKS also supports the following returning queries.
    - [INSERT INTO name RETURNING](20-sql-references-h-z.md#9b221e074482cce0)
    - [UPDATE name RETURNING](20-sql-references-h-z.md#f9a91742fa4c7945)
    - [DELETE FROM name RETURNING](#43d479588fc6bc18)
- In the SQL standard, the default value for &lt;cursor updatability&gt; is determined by the &lt;select statement&gt;. In GOLDILOCKS, the default is FOR READ ONLY.
- The SQL standard does not include syntax for &lt;lock wait mode&gt;.

**SQL standard compatibility**

<a id="25f7efcd98ff3f85"></a>
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

<a id="a8fea00001504032"></a>
### For More Information

Refer to the following.

- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [FETCH cursor_name](#b4d62d5536bcdf22)
- [CLOSE cursor_name](#a47858c9b07fa0f3)
- [PREPARE statement_name](20-sql-references-h-z.md#ff813c116e09eff4)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)
- [SELECT .. FOR UPDATE](20-sql-references-h-z.md#1cd99ab297830a3f)
- [INSERT INTO name RETURNING](20-sql-references-h-z.md#9b221e074482cce0)
- [UPDATE name RETURNING](20-sql-references-h-z.md#f9a91742fa4c7945)
- [DELETE FROM name RETURNING](#43d479588fc6bc18)

<a id="49b395482c2c6438"></a>
## DELETE FROM

<a id="4d7fdf394a88fada"></a>
### Function

It deletes rows from a table.

<a id="ccde3004a02053f6"></a>
### Syntax

```
<delete statement: searched> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        [ WHERE <search condition> ]
        { [ <result offset clause> ] [ <fetch limit clause> ] | [ <local shard limit clause> ] }
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

<local shard limit clause>
    LOCAL SHARD LIMIT limit_row_count [ ROWS ]
```

<a id="46aa0d44cc7249fb"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;delete statement: searched&gt;.

- (DELETE or CONTROL TABLE) ON TABLE for the table
- (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DELETE ANY TABLE ON DATABASE

<a id="9ce2e1e27bc3f278"></a>
### Syntax Rules and Parameters

<a id="1c8d1b1ba734b730"></a>
#### table_name

It is the name of the target table from which rows will be deleted.  
The schema to which the table belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

<a id="f78b6412ec944c55"></a>
#### [ AS alias_name ]

It is an alias for the table_name.

<a id="76107a93249d7be3"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows that satisfy the WHERE condition.  
If the WHERE condition is omitted, all rows in the table are deleted.  
For more information about the WHERE condition, refer to the [where clause](20-sql-references-h-z.md#9476446413c73f97) of the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="eb7b251a0e72a99a"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip in the query result.  
For more information, refer to the [offset limit clause](20-sql-references-h-z.md#0980c29c08cd8fe9) in the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="852a415e1825e17d"></a>
#### &lt;fetch limit clause&gt;

There are two ways to specify the number of rows to be fetched:

- &lt;fetch first clause&gt;
    - It specifies the number of rows to fetch. 
    - For more information, refer to the [&lt;fetch first clause&gt;](20-sql-references-h-z.md#796fff4d231b1d3a) of the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to fetch, or both the number of rows to skip and the number of rows to fetch.
    - For more information, refer to the [&lt;limit clause&gt;](20-sql-references-h-z.md#e948a1cc4ca56f3d) of the [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.

<a id="59f650a785d26d85"></a>
#### &lt;local shard limit clause&gt;

It provides data switchover for sharded tables in a cluster environment.

It deletes up to limit_row_count records from the local group of a sharded table.

- When this clause is specified, DELETE is supported only for sharded tables.
- The value of limit_row_count must be a positive integer.
- This clause cannot be used together with the &lt;result offset clause&gt; or the &lt;fetch limit clause&gt;.

<a id="b71ef6960cec9188"></a>
### Description

<a id="9ffcd1f9b9b7ff0c"></a>
#### Differences Between DELETE Statements

- [DELETE FROM](#49b395482c2c6438)
    - It deletes multiple rows that match the condition. 
    - e.g. DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#6203e76a3fa030ee)
    - It deletes the row currently pointed to by the cursor.
    - e.g. DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#43d479588fc6bc18)
    - It deletes multiple rows that match the condition, and allows retrieving the deleted rows using APISs such as SQLFetch(), similar to a [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f) statement.
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#58b0c6a8f037a99b)
    - It deletes at most one row. If exactly one row is deleted, its values are assigned to host variables specified in the RETURNING INTO clause.
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="8d5a99e8ccb818b0"></a>
### Examples

The following is an example of a DELETE statement.

```
gSQL> DELETE FROM t1 WHERE id > 3;

2 rows deleted.
```

The following example demonstrates how to skip a certain number of rows (two rows) and delete a specific number of rows (two rows) from the result set that meets the condition, using the &lt;result offset clause&gt; and &lt;fetch first clause&gt;.

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

The following is an example of using &lt;local group limit&gt; to delete only the records in the local group of the current target sharded table.

```
gSQL> SELECT cluster_group_name, id, data FROM t_shard ORDER BY 1, 2;

CLUSTER_GROUP_NAME ID DATA  
------------------ -- ------
G1                  1 data_1
G2                  2 data_2

2 rows selected.

--# The local group is G1.
gSQL> SELECT local_group_name() FROM dual;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.

--# Although the DELETE statement specifies a limit of two rows, only one row in the local group (G1) is deleted because it is the only row in the local group.
gSQL> DELETE FROM t_shard LOCAL SHARD LIMIT 2;

1 row deleted.

--# The row in the other local group is not deleted and remains unchanged.
gSQL> SELECT cluster_group_name, id, data FROM t_shard ORDER BY 1, 2;

CLUSTER_GROUP_NAME ID DATA  
------------------ -- ------
G2                  2 data_2

1 row selected.
```

The following is an example of performing data switchover for a sharded table by configuring an anonymous PL block that uses a DELETE statement with the &lt;local group limit&gt; clause.

- Example of the bulk_delete.sql file configuration

```
--# Deletes all records in the lineitem table where l_commitdate is earlier than '1997-08-28'.
--# Deletes target records in batches of 50,000 and repeatedly performs COMMIT.

BEGIN
    LOOP
        DELETE FROM lineitem WHERE l_commitdate < date '1997-08-28' LOCAL SHARD LIMIT 50000;
        
        IF SQL%ROWCOUNT = 0 THEN
            EXIT;
        ELSE
            COMMIT;
        END IF;
    END LOOP;
END;
/
```

- Example of executing the bulk_delete.sql file

```
[shell]> gsqlnet test test --dsn=G1N1 --import bulk_delete.sql
```

It is recommended to execute the data switchover query in parallel on the master server of each group where sharded table records are distributed.

```
[shell]> gsqlnet test test --dsn=G1N1 --import bulk_delete.sql &
[shell]> gsqlnet test test --dsn=G2N1 --import bulk_delete.sql &
[shell]> gsqlnet test test --dsn=G3N1 --import bulk_delete.sql &
```

<a id="3197db8b2c7efc1b"></a>
### Compatibility

The SQL standard does not define the following clauses in the DELETE statement.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;
- &lt;local shard limit clause&gt;

**SQL standard compatibility**

<a id="b377e6e49ec1bcda"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="1532fac9cc52215e"></a>
### For More Information

Refer to the following.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#6203e76a3fa030ee)
- [DELETE FROM name RETURNING](#43d479588fc6bc18)
- [DELETE FROM name RETURNING .. INTO](#58b0c6a8f037a99b)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)

<a id="43d479588fc6bc18"></a>
## DELETE FROM name RETURNING

<a id="e2388a7ca8f49982"></a>
### Function

It deletes rows from the table and retrieves the deleted rows.

<a id="b62aac1f963b83f2"></a>
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

<a id="b0a1ec50000a161f"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute a &lt;delete returning query statement&gt;.

- One of the following privileges is required to execute the DELETE statement.
    - (DELETE or CONTROL TABLE) ON TABLE for the table
    - (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - DELETE ANY TABLE ON DATABASE

- One of the following privileges is required for all columns used in the RETURNING clause.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause. 
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="4aae4f1977c890dc"></a>
### Syntax Rules and Parameters

<a id="94de14631be920ef"></a>
#### table_name

It is the name of the target table from which rows will be deleted.

<a id="0db8016b78c0b8d9"></a>
#### [ AS alias_name ]

It is an alias for the table_name.

<a id="d30d592570d47b0c"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows that satisfy the WHERE condition.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="1db2fe3ccd662f13"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip in the query result.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="ba954608f2fd5dc6"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to fetch.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="e4d94077a1bd1ec1"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to fetch, or both the number of rows to skip and the number of rows to fetch.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="7f1ee6fbd3623dbb"></a>
#### &lt;returning clause&gt;

It specifies the columns to retrieve from the result set of deleted rows.

- The RETURNING clause returns a result set consisting of the rows deleted by the DELETE statement.
- &lt;value expression&gt; 
    - Functions like the &lt;select list&gt; in a SELECT statement, but does not support aggregation functions or similar operations.
- [[AS] alias_name] 
    - It assigns an alias to a value expression using the optional AS clause.

RETURN and RETURNING are keywords with the same meaning and can be used interchangeably.

<a id="4de39f408dc57603"></a>
### Description

For more information, refer to [Differences Between DELETE Statements](#9ffcd1f9b9b7ff0c).

<a id="84c57ee5bc61d0ad"></a>
### Examples

The following is an example of deleting rows that satisfy a condition and retrieving the deleted rows.

```
gSQL> DELETE FROM t1 WHERE id > 3 RETURNING *;

ID DATA  
-- ------
 4 data_4
 5 data_5

2 rows deleted.
```

The following is an example of using expressions in the RETURNING clause to retrieve information about the deleted rows.

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

<a id="1edbb8206d2471b5"></a>
### Compatibility

The &lt;delete returning query statement&gt; is not defined in the SQL standard.

<a id="bfeecc7928dca1ec"></a>
### For More Information

Refer to the following.

- [DELETE FROM](#49b395482c2c6438)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#6203e76a3fa030ee)
- [DELETE FROM name RETURNING .. INTO](#58b0c6a8f037a99b)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)

<a id="58b0c6a8f037a99b"></a>
## DELETE FROM name RETURNING .. INTO

<a id="bd99a6a985db642d"></a>
### Function

It deletes a single row from the table and retrieves the value of the deleted row into a host variable.

<a id="e28206e6fcd5ad88"></a>
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

<a id="f8c2c3e31b5dc2d1"></a>
### Invocation and Access Rules

The user must meet the following conditions to execute a &lt;delete returning into statement&gt;.

- One of the following privileges is required to execute the DELETE statement.
    - (DELETE or CONTROL TABLE) ON TABLE for the table
    - (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - DELETE ANY TABLE ON DATABASE

- One of the following privileges is required for all columns used in the RETURNING clause.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="a09f11f78c4b992f"></a>
### Syntax Rules and Parameters

<a id="6950ec2df8bb2b5f"></a>
#### table_name

It is the name of the target table from which rows will be deleted.

<a id="a60511c2208ff768"></a>
#### [ AS alias_name ]

It is an alias for the table_name.

<a id="ce31d5e370201dad"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows that satisfy the WHERE condition.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="dc69a3cfc777c02d"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip in the query result.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="a2a54da48e705fa3"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to fetch.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="38608f4cf4ff3945"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to fetch, or both the number of rows to skip and the number of rows to fetch.  
For more information, refer to the [DELETE FROM](#49b395482c2c6438) statement.

<a id="65d6de3c38fbd19f"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - For more information, refer to the &lt;returning clause&gt; of the [DELETE FROM name RETURNING](#43d479588fc6bc18) statement.
- INTO variable_name [, ...]
    - The number of variables specified in the INTO clause must match the number of the expressions specified in the RETURNING clause.

<a id="4d7755c36ff99a17"></a>
### Description

The number of rows to be deleted must be less than or equal to one.  
If two or more rows are deleted, an error will occur.

For more information, refer to [Differences Between DELETE Statements](#9ffcd1f9b9b7ff0c).

<a id="55d0b0754965df53"></a>
### Example

The following is an example of deleting a row and retrieving the values of the deleted row into host variables in interactive SQL (gsql).

```
gSQL> \var v_id    INTEGER
gSQL> \var v_data  VARCHAR(128)

gSQL> DELETE FROM t1 WHERE id = 3 RETURNING id, data INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row deleted.
```

<a id="302ee84f66d5efb5"></a>
### Compatibility

The &lt;delete returning into statement&gt; is not defined in the SQL standard.

<a id="f4d1aa2aff07f1b4"></a>
### For More Information

Refer to the following.

- [DELETE FROM](#49b395482c2c6438)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#6203e76a3fa030ee)
- [DELETE FROM name RETURNING](#43d479588fc6bc18)
- [SELECT](20-sql-references-h-z.md#d7ebf6af3421bb2f)

<a id="6203e76a3fa030ee"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="ab58bb38a0277f94"></a>
### Function

It deletes a single row pointed to by the cursor.

<a id="26f7c89ddad022af"></a>
### Syntax

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="44c9e4bc2d4b6307"></a>
### Invocation and Access Rules

The privilege to execute a [DELETE FROM](#49b395482c2c6438) statement is required to perform a &lt;delete statement: positioned&gt; operation.

<a id="d808d478493f3726"></a>
### Syntax Rules and Parameters

<a id="ea99c48440ea99dd"></a>
#### table_name

It is the name of the target table from which rows will be deleted.

<a id="c8f66fcfa22372b7"></a>
#### [ AS alias_name ]

It is an alias for the table_name.

<a id="3a519fa24c73d143"></a>
#### cursor_name

The cursor corresponding to cursor_name must satisfy the following conditions:

- The cursor must be OPEN. (Refer to [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3).) 
- A row must have been fetched using the cursor. (Refer to [FETCH cursor_name](#b4d62d5536bcdf22).) 
- The query used for the cursor must be able to identify the table_name. (Refer to [DECLARE cursor_name](#ccb6dc5ecb7cf850).) 
- The cursor must be updatable for the specified table_name. (Refer to [DECLARE cursor_name](#ccb6dc5ecb7cf850).)

<a id="ff333f28b3dd8464"></a>
### Description

For more information, refer to [Differences among DELETE-related Statements](#9ffcd1f9b9b7ff0c).

<a id="500622de93339c20"></a>
### Example

The following is an example of how to declare a FOR UPDATE cursor and delete rows using the cursor in interactive SQL (gsql).

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

<a id="5416232c1a7fc811"></a>
### Compatibility

**SQL standard compatibility**

<a id="256a9a336269e85c"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="2ddacd6f7022b054"></a>
### For More Information

Refer to the following.

- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [FETCH cursor_name](#b4d62d5536bcdf22)
- [DELETE FROM](#49b395482c2c6438)
- [DELETE FROM name RETURNING](#43d479588fc6bc18)
- [DELETE FROM name RETURNING .. INTO](#58b0c6a8f037a99b)

<a id="230511362f0d7d5e"></a>
## DROP AUDIT POLICY

<a id="d2482aeb85f74c82"></a>
### Function

It drops an audit policy.

<a id="617f713360d8b86e"></a>
### Syntax

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="27218fcb6040682e"></a>
### Invocation and Access Rules

The AUDIT SYSTEM ON DATABASE privilege is required to execute the &lt;drop audit policy statement&gt;.

<a id="d9785f2f5b1ad466"></a>
### Syntax Rules and Parameters

<a id="d939b439df56ff26"></a>
#### IF EXISTS

No error is raised even if the specified policy_name does not exist.

<a id="1810fb782c7514e1"></a>
#### policy_name

It is the name of the audit policy object to be dropped.

<a id="1f0fdfd39ae955eb"></a>
### Description

An audit policy object that is currently active cannot be dropped. In such cases, the policy must first be deactivated using the NOAUDIT POLICY statement.

<a id="791d78190a22b1de"></a>
### Examples

The following is an example of dropping an audit policy.

```
DROP AUDIT POLICY policy_table;
```

<a id="0f72e245717bb08c"></a>
### Compatibility

The SQL standard does not define audit policies.

<a id="2c4a4b276a7fa88c"></a>
### For More Information

Refer to the following.

- Managing audit policy objects
    - [CREATE AUDIT POLICY](#9b9979f490f84f42)
    - [DROP AUDIT POLICY](#230511362f0d7d5e)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#1ee1c2c985e74ad3)

- Activating/ deactivating audit policies
    - [AUDIT POLICY](18-sql-references-a-b.md#28ecab768bc8d18a)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#237307d91350ad0b)

- Retrieving the audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#79d9233c8fc99c99)

- Clearing the audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#a4524ffa1dc98eef)

<a id="cf6da303c45334dc"></a>
## DROP CLUSTER GROUP

<a id="656904cb4468f785"></a>
### Function

It drops a cluster group from a cluster system.

<a id="bd899a1f7b0c6b86"></a>
### Syntax

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="ef76e2a8e4c26646"></a>
### Invocation and Access Rules

It can only be executed in a cluster system.  
The ADMINISTRATION ON DATABASE privilege is required to execute the &lt;drop cluster group statement&gt;.

<a id="7ed0acba991b1198"></a>
### Syntax Rules and Parameters

<a id="bec280cf1298ca2d"></a>
#### [IF EXISTS]

No error is raised even if the specified cluster group does not exist.

<a id="995838bf19484074"></a>
#### group_name

It is the name of the cluster group.  
Only cluster groups that do not contain any shards can be dropped.

<a id="8a7c807691b21a29"></a>
### Description

A cluster group can be dropped only if its removal does not result in data loss.

> All members of the target cluster group must be inactive.  
>  Otherwise, the following error will occur.

```
gSQL> DROP CLUSTER GROUP g3;

ERR-42000(16582): there are active cluster members in the target cluster group 'G3'
```

<a id="308148f173a1b7af"></a>
### Examples

The following is an example of dropping a cluster group.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="7e37011df93afab7"></a>
### Compatibility

The SQL standard does not define the concept of a cluster.

<a id="9b901611efd6256f"></a>
### For More Information

Refer to [CREATE CLUSTER GROUP](#6ad165b04482545a).

<a id="9a30ad97763681d1"></a>
## DROP CLUSTER LOCATION

<a id="ff0662523cda2e56"></a>
### Function

It drops the access information of a cluster member.

<a id="74c9078421cd6d58"></a>
### Syntax

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
        [ AT <domain name> ]
    ;
```

<a id="8451a6cf5d7edeb9"></a>
### Invocation and Access Rules

It can be executed only in a cluster system.  
The ADMINISTRATION ON DATABASE privilege is required to execute the &lt;drop cluster location statement&gt;.

<a id="27042e26abab2c3e"></a>
### Syntax Rules and Parameters

<a id="6477813b62487f77"></a>
#### member_name

It is the name of the cluster member.  
The specified name must exist in the registered cluster location information.  
The name must be less than 128 bytes in length.

<a id="51e8792de45727b8"></a>
#### &lt;domain name&gt;

It is the name of the member or group on which the statement is performed.  
If not specified, the statement is performed on all groups.

<a id="12b5df51fa74c809"></a>
### Description

By default, cluster location information is automatically created using the access details provided when creating a cluster group or adding a cluster member.  
This information is automatically removed when the associated cluster member or group is deleted.

If the access information of a cluster location changes, it is not necessary to delete or recreate the cluster member. Instead, use the [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#b1673f7439fc39e9) statement to update the access information.

<a id="487cd67fe6e0276c"></a>
### Example

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="1ec2f39d4aead1a9"></a>
### Compatibility

The SQL standard does not define the concept of a cluster.

<a id="dd0aa1db45d9df60"></a>
### For More Information

Refer to the following.

- [CREATE CLUSTER LOCATION](#1e6f444e1a43b4b5)
- [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#b1673f7439fc39e9)

<a id="0d535b079ff2f022"></a>
## DROP INDEX

<a id="73c05e7caa4e81d6"></a>
### Function

It drops an index.

<a id="68d65349d136f1d6"></a>
### Syntax

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="25997d3bd7484647"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;drop index statement&gt;.

- The owner of the index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs
- (DROP INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- DROP ANY INDEX ON DATABASE

<a id="85cadbb3295444b1"></a>
### Syntax Rules and Parameters

<a id="87c065ee6454d5ed"></a>
#### IF EXISTS

No error is raised even if the specified index does not exist.

<a id="10485167af7d65df"></a>
#### index_name

It is the name of the index to be dropped.  
The schema to which the index belongs  can be defined using the format schema_name.index_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

Indexes created for UNIQUE or PRIMARY KEY constraints can not be dropped directly.  
To drop such indexes, the associated constraints must first be dropped using the [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#76321198b633d720) statement.

<a id="ded55c30ab913e64"></a>
### Description

Even Data Definition Language (DDL) statements such as DROP INDEX can be rolled back, as long as the transaction has not been committed.

<a id="9b0ed4d566fde525"></a>
### Examples

The following is an example of dropping an index.

```
gSQL> DROP INDEX idx_t1_id;

Index dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified index does not exist.

```
gSQL> DROP INDEX IF EXISTS not_exist_index;

Index dropped.
```

<a id="d7a5046ed60caf60"></a>
### Compatibility

The SQL standard does not define the concept of the index.

<a id="84fc1fc2834c75a0"></a>
### For More Information

Refer to the following.

- [CREATE INDEX](#c758c010adf913ce)
- [DROP TABLE](#5324bfcd0073e53b)
- [ALTER TABLE name DROP CONSTRAINT](18-sql-references-a-b.md#76321198b633d720)

<a id="0c97ae81d474b49a"></a>
## DROP PROFILE

<a id="92f50eea7a8f9ead"></a>
### Function

It drops a profile.

<a id="8738400a39322496"></a>
### Syntax

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="71bf9ef5264ac490"></a>
### Invocation and Access Rules

The DROP PROFILE ON DATABASE privilege is required to execute the &lt;drop profile statement&gt;.

<a id="b38973e3921e2fb0"></a>
### Syntax Rules and Parameters

<a id="407cadc8ae704b00"></a>
#### IF EXISTS

No error is raised even if the specified profile does not exist.

<a id="60022bbc845a3388"></a>
#### profile_name

It is the name of the profile to be dropped.  
The DEFAULT profile cannot be dropped.

<a id="6e830c5c51d0a1aa"></a>
#### CASCADE

The CASCADE clause must be specified if there are users currently assigned to the profile being dropped.  
When a profile is dropped with CASCADE, all users assigned to that profile are automatically reassigned to the DEFAULT profile.

<a id="27b80b57ca2c30f1"></a>
### Example

The following is an example of dropping a profile using the CASCADE clause.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="3a991ed35f2ebf0f"></a>
### Compatibility

The SQL standard does not define the concept of the profile.

<a id="ba0e1ea235f85481"></a>
### For More Information

Refer to the following.

- [CREATE PROFILE](#98c2f8112f164605)
- [ALTER PROFILE](18-sql-references-a-b.md#1107682b7d496cfb)

<a id="9c173c3287657d63"></a>
## DROP ROLE

<a id="b20cf2b767b70d4f"></a>
### Function

It drops a role.

<a id="b09ea52a9a895769"></a>
### Syntax

```
<drop role statement> ::=
    DROP ROLE [ IF EXISTS ] <role_name>
    ;
```

<a id="23ba7925755c641f"></a>
### Invocation and Access Rules

One of the following conditions must be satisfied to execute a &lt;drop role statement&gt;.

- The user must have the DROP ROLE ON DATABASE privilege.
- The WITH ADMIN OPTION for &lt;role_name&gt; must have been granted.

<a id="436e1cc2bdd617a5"></a>
### Syntax Rules and Parameters

<a id="29e1ceadd0709448"></a>
#### IF EXISTS

No error is raised even if the specified role does not exist.

<a id="7c47c50fbe31b92c"></a>
#### &lt;role_name&gt;

It is the name of the role to be dropped.  
Built-in roles such as ADMIN, SYSDBA, and DBA can not be dropped.

<a id="439c9cdf704bfa25"></a>
### Description

It drops the role.

<a id="0484544b54adc3b8"></a>
### Examples

The following is an example of dropping a role by a user who has the DROP ROLE ON DATABASE privilege.

```
gSQL> GRANT DROP ROLE ON DATABASE TO u1;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 
U1      DROP ROLE ON DATABASE      

2 rows selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

no rows selected.

gSQL> \connect u1 u1

gSQL> DROP ROLE role1;

Role dropped.
```

The following is an example of dropping a role by a user who has the WITH ADMIN OPTION privilege.

```
gSQL> GRANT role1 TO u1 WITH ADMIN OPTION;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 

1 row selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

GRANTEE GRANTED_ROLE ADMIN_OPTION
------- ------------ ------------
U1      ROLE1        YES         

1 row selected.

gSQL> \connect u1 u1

gSQL> DROP ROLE role1;

Role dropped.
```

<a id="40c415be078798c6"></a>
### Compatibility

The SQL standard does not define the IF EXISTS clause.

**SQL standard compatibility**

<a id="61a09d439184a906"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |

<a id="1fe4a90d7735ba23"></a>
### For More Information

Refer to [CREATE ROLE](#635504efdc11b072).

<a id="2fd59a238a864111"></a>
## DROP SCHEMA

<a id="d072e2da5aa7f279"></a>
### Function

It drops a schema.

<a id="9afa9bedbf72e08a"></a>
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

<a id="ece6a9fc6330e832"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;drop schema statement&gt;.

- The owner of the schema
- CONTROL SCHEMA ON SCHEMA for the schema
- DROP SCHEMA ON DATABASE

<a id="dec50fc568cc49af"></a>
### Syntax Rules and Parameters

<a id="344295abea80a715"></a>
#### IF EXISTS

No error is raised even if the specified schema does not exist.

<a id="b43db25c51c0b698"></a>
#### schema_name

It is the name of the schema to be dropped.  
However, built-in schemas such as DICTIONARY_SCHEMA, INFORMATION_SCHEMA, and PUBLIC, which are automatically created when the database is created, cannot be dropped.

<a id="a2b1e3c68ad2c462"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - The schema can only be dropped if it contains no objects.
- CASCADE 
    - All objects within the schema are dropped along with the schema itself.
    - The FOREIGN KEYs in other schemas that reference the PRIMARY KEY or UNIQUE objects within the schema are also dropped.
- If omitted, the default behavior is RESTRICT.

<a id="99d07610c30bd7f6"></a>
### Description

It drops a schema. Any recycle bin objects contained in the schema are also dropped.

<a id="e6fbd7fde53ebc4e"></a>
### Examples

The following is an example of dropping a schema along with all its contained objects.

```
gSQL> DROP SCHEMA s1 CASCADE;

Schema dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified schema does not exist.

```
gSQL> DROP SCHEMA IF EXISTS not_exist_schema;

Schema dropped.
```

<a id="e93675af639e6701"></a>
### Compatibility

The SQL standard does not define the IF EXISTS clause.

**SQL standard compatibility**

<a id="79ea905b4887e523"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="480687aac174180a"></a>
### For More Information

Refer to [CREATE SCHEMA](#0173622cce38fc3c).

<a id="125ff61843f5e7f3"></a>
## DROP SEQUENCE

<a id="8e3c5e43b46767c0"></a>
### Function

It drops a sequence.

<a id="8a6054c307b60b21"></a>
### Syntax

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="380a00c88474fd34"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;drop sequence generator statement&gt;.

- The owner of the sequence
- (DROP SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence belongs
- DROP ANY SEQUENCE ON DATABASE

<a id="58488c586800153b"></a>
### Syntax Rules and Parameters

<a id="81a5309d77d8ad27"></a>
#### IF EXISTS

No error is raised even if the specified sequence does not exist.

<a id="d5b3f2b8f878795c"></a>
#### sequence_name

It is the name of the sequence to be dropped.  
The schema to which the sequence belongs can be defined using the format schema_name.sequence_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

<a id="71412c3e3fca7154"></a>
### Description

Even Data Definition Language (DDL) statements such as DROP SEQUENCE can be rolled back, as long as the transaction has not been committed.

<a id="c6b1732ae48f6d88"></a>
### Examples

The following is an example of dropping a sequence.

```
gSQL> DROP SEQUENCE seq1;

Sequence dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified sequence does not exist.

```
gSQL> DROP SEQUENCE invalid_sequence;

ERR-42000(16044): sequence does not exist : 
DROP SEQUENCE invalid_sequence
              *
ERROR at line 1:


gSQL> DROP SEQUENCE IF EXISTS invalid_sequence;

Sequence dropped.
```

<a id="8cefd65cb2561acd"></a>
### Compatibility

The SQL standard does not define the IF EXISTS clause.

**SQL standard compatibility**

<a id="3fd597b1206be322"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="138d50665556cba8"></a>
### For More Information

Refer to the following.

- [CREATE SEQUENCE](#630728df3a71a28b)
- [ALTER SEQUENCE](18-sql-references-a-b.md#59da3d9f8e5621cf)

<a id="cc44cfa07d635430"></a>
## DROP SYNONYM

<a id="cd4ee6605f05feb3"></a>
### Function

It drops a synonym.

<a id="6744ecbc1af22479"></a>
### Syntax

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="1aa762f50c7162e0"></a>
### Invocation and Access Rules

To drop a public synonym with the PUBLIC keyword explicitly specified, the user must have the DROP PUBLIC SYNONYM ON DATABASE privilege.

To drop a private synonym, the user must have one of the following privileges.

- The owner of the synonym
- (DROP SYNONYM or CONTROL SCHEMA) ON SCHEMA for the schema to which the synonym belongs
- DROP ANY SYNONYM ON DATABASE

<a id="a0858520dd6beeaf"></a>
### Syntax Rules and Parameters

<a id="bd401a654263d07c"></a>
#### [ PUBLIC ]

This clause is specified when dropping a public synonym.  
If omitted, a private synonym is dropped instead.

<a id="b4fa8480875e6a85"></a>
#### IF EXISTS

No error is raised even if the specified synonym does not exist.

<a id="870efda4fa654c6d"></a>
#### synonym_name

It is the name of the synonym to be dropped.  
It can define schema to which the synonym belongs using the format schema_name.synonym_name. If schema_name is omitted, the default schema of the user executing the statement will be used.  
When the PUBLIC keyword is specified, a schema name must not be provided.

<a id="0471b03ebd944c38"></a>
### Description

Even Data Definition Language (DDL) statements such as DROP SYNONYM can be rolled back, as long as the transaction has not been committed.

<a id="b290ad4dc077fdb7"></a>
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

<a id="357f9c872cd455fc"></a>
### Compatibility

The SQL standard does not define the DROP SYNONYM statement.

<a id="4cc3af469e545f00"></a>
### For More Information

Refer to [CREATE SYNONYM](#3632eb462786e0cb).

<a id="5324bfcd0073e53b"></a>
## DROP TABLE

<a id="a7142e33ef3a1ebe"></a>
### Function

It drops a table.

> If the recycle bin feature is enabled, the table is not immediately dropped but instead moved to the recycle bin.

<a id="f04a913e968bd2e4"></a>
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

<a id="f67f9f45a382fd85"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;drop table statement&gt;.

- The owner of the table 
- CONTROL TABLE ON TABLE for that table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="3cf748150e1eeba4"></a>
### Syntax Rules and Parameters

<a id="38a8d9edbd923779"></a>
#### IF EXISTS

No error is raised even if the specified table does not exist.

<a id="5b8686b1c7d753cc"></a>
#### table_name

It is the name of the table to be dropped.  
It can define schema to which the table belongs using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

The following tables, which are automatically created when the database is created, cannot be dropped.

- Tables in the DEFINITION_SCHEMA schema
- Tables in the FIXED_TABLE_SCHEMA schema

Constraints and indexes created on the table are also dropped together.

<a id="f37be3c113f9e8a3"></a>
#### drop behavior

When omitted, the default value is RESTRICT.

CASCADE and CASCADE CONSTRAINTS have the same meaning.

If there are referencing tables that refer to the table with a FOREIGN KEY, the CASCADE CONSTRAINTS clause must be specified.

<a id="43f438ea60c6419a"></a>
#### purge

When the recycle bin feature is enabled, using PURGE causes the table to be dropped immediately without being moved to the recycle bin.

<a id="dac6f3e7dd784cb4"></a>
### Description

Even Data Definition Language (DDL) statements such as DROP TABLE can be rolled back, as long as the transaction has not been committed.

<a id="64f428e4790d9b16"></a>
### Examples

The following is an example of dropping a regular table.

```
gSQL> DROP TABLE region;

Table dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified table does not exist.

```
gSQL> DROP TABLE IF EXISTS invalid_table;

Table dropped.
```

The following is an example of rolling back a dropped table.

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

<a id="38acfcb254a35984"></a>
### Compatibility

The SQL standard does not define the following clauses.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL standard compatibility**

<a id="e2a54e93916f4c8d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="adcb6af426be4315"></a>
### For More Information

Refer to [CREATE TABLE](#47f3ce328094503e).

<a id="9b31e9a7a77c3aed"></a>
## DROP TABLESPACE

<a id="22eca953bd7f1fe5"></a>
### Function

It drops a tablespace.

<a id="ab6edcd4979b2b44"></a>
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

<a id="08442580a60092fe"></a>
### Invocation and Access Rules

The DROP TABLESPACE ON DATABASE privilege is required to execute the &lt;drop tablespace definition&gt;.

<a id="a1073ad4a3e10c93"></a>
### Syntax Rules and Parameters

<a id="444bddbef310a485"></a>
#### IF EXISTS

No error is raised even if the specified tablespace does not exist.

<a id="c0dca9d1a34d61d5"></a>
#### tablespace_name

It is the name of the tablespace to be dropped.

The following system tablespaces, which are automatically created when the database is created, cannot be dropped.

- DICTIONARY_TBS: system tablespace for dictionary management
- MEM_UNDO_TBS: system tablespace for default undo tablespace
- MEM_DATA_TBS: system tablespace for default user data tablespace
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> If the tablespace_name was used as the default tablespace for users, space cannot be allocated for objects once the tablespace is dropped. Therefore, after dropping the tablespace, the users' default tablespace must be changed using the [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2) statement.

<a id="47b6ca534dee94a1"></a>
#### INCLUDING CONTENTS

It drops objects (such as tables, indexes, and key constraints) that belong to the tablespace. If an index or key constraint references a table in the tablespace  but exists outside of it, that index or constraint will also be dropped.

If the INCLUDING CONTENTS clause is not used, then no objects should exist within the tablespace.

<a id="5c7d8230817f2017"></a>
#### [ { AND | KEEP } DATAFILES ]

It specifies whether to drop the datafiles that make up the tablespace.  
For memory temporary tablespaces, datafiles do not exist, so this clause is ignored.

- AND DATAFILES 
    - It drops the datafiles along with the tablespace. 
- KEEP DATAFILES 
    - It does not drop the datafiles; they are retained.
- If not specified, the default is KEEP DATAFILES.

<a id="3722f74cdae6cc29"></a>
#### drop behavior

When omitted, the default value is RESTRICT.

CASCADE and CASCADE CONSTRAINTS have the same meaning.

If a FOREIGN KEY in a different tablespace refers to a PRIMARY KEY or UNIQUE constraint that is being dropped together with the corresponding tablespace, the CASCADE CONSTRAINTS clause must be specified.

<a id="58bdc8bc974d7723"></a>
### Description

Unlike other Data Definition Language (DDL) operations, the DROP TABLESPACE statement cannot be rolled back, and the transaction is automatically committed upon execution.  
If the tablespace being dropped contains recycle bin objects, those objects are also permanently dropped.

<a id="1698ebb7d48c5e56"></a>
### Examples

The following is an example of dropping a tablespace along with all objects contained in it, as well as all datafiles that make up the tablespace:

```
gSQL> DROP TABLESPACE space1 INCLUDING CONTENTS AND DATAFILES CASCADE CONSTRAINTS;

Tablespace dropped.
```

The following is an example of how to avoid an error when the specified tablespace does not exist by using the IF EXISTS clause:

```
gSQL> DROP TABLESPACE IF EXISTS not_exist_tablespace;

Tablespace dropped.
```

<a id="17380491a55a9085"></a>
### Compatibility

The SQL standard does not define the concept of a tablespace.

<a id="b161cc6ea86a36bf"></a>
### For More Information

Refer to the following.

- [CREATE MEMORY DATA TABLESPACE](#8f6b0a901e93d0d4)
- [CREATE MEMORY TEMPORARY TABLESPACE](#a09ab566de521b1a)
- [ALTER TABLESPACE](18-sql-references-a-b.md#4e7cd5f52e3f3a17)

<a id="7979783b911846c2"></a>
## DROP USER

<a id="89397e00ac5a58fd"></a>
### Function

It drops a database user.

<a id="519cda650226c914"></a>
### Syntax

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="f048dc9389401105"></a>
### Invocation and Access Rules

The DROP USER ON DATABASE privilege is required to execute the &lt;drop user statement&gt;.

> The schema owned by user_identifier must not exist.  
> For more information about dropping a schema, refer to the [DROP SCHEMA](#2fd59a238a864111) statement.

<a id="866b618ddabe8885"></a>
### Syntax Rules and Parameters

<a id="39ab2492e772f04a"></a>
#### IF EXISTS

No error is raised even if the specified user does not exist.

<a id="62eb1fb7f59b6d06"></a>
#### user_identifier

It is the username of the database to be dropped.  
However, the user which is automatically created when the database is created, such as "SYS", cannot be dropped.

The following types of objects are not dropped if they were created by user_identifier but are not owned by it.

- Role 
- Tablespace

<a id="3fc5bb937c048579"></a>
#### &lt;drop behavior&gt;

- RESTRICT 
    - The following SQL schema objects owned by the user must not exist:
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint 
- CASCADE 
    - All of the following SQL schema objects owned by the user are dropped:
        - Table, view 
        - Index 
        - Sequence 
        - Table constraint
    - The FOREIGN KEYs of other users that reference the PRIMARY KEY and UNIQUE objects owned by the user are also dropped. 
- If omitted, the default is RESTRICT.

> User and Schema Relationships in Other DBMSs   
> 
> 
> - Oracle
>     - User : schema = 1 : 1.
>     - When using CASCADE, the schema is also dropped.
> 
> 
> 
> - DB2 
>     - A database user is equivalent to an OS user.
>     - There are no separate SQL statements for creating or dropping users.
> 
> 
> 
> - Postgres 
>     - User : schema = 1 : N. 
>     - CASCADE is not supported. A user can be dropped only after all owned objects are dropped and all granted privileges are revoked.
> 
> 
> 
> - MySQL 
>     - Database : schema = 1 : 1.
>     - Users are subordinate to databases (schemas). CASCADE is not supported.
> 

<a id="675ee50f1cdb0455"></a>
### Description

In GOLDILOCKS, the relationship between a user and schemas is 1:N.  
In other words, a user may not own any schemas, or may own multiple schemas.

To drop a user, all schemas owned by the user must first be dropped.  
During this process, any recycle bin objects belonging to the user are also removed.

<a id="a6743413da6689bb"></a>
### Examples

The following is an example of dropping all schemas owned by a user, followed by dropping the user:

```
gSQL> DROP SCHEMA u1 CASCADE;

Schema dropped.

gSQL> DROP USER u1 CASCADE;

User dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified user does not exist.

```
gSQL> DROP USER IF EXISTS not_exist_user;

User dropped.
```

<a id="cd2a5cb9e3ed3518"></a>
### Compatibility

The SQL standard defines the concept of a user but does not specify SQL statements for creating or dropping users.

<a id="7d5f5d9aac611e3b"></a>
### For More Information

Refer to the following.

- [CREATE USER](#409f34806636a0ff)
- [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2)
- [DROP SCHEMA](#2fd59a238a864111)

<a id="5a1fec21848fd68b"></a>
## DROP VIEW

<a id="93f68edf5bcd327d"></a>
### Function

It drops a view.

<a id="f8b1d3e013349f6a"></a>
### Syntax

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="7f901f1acd46c453"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;drop view statement&gt;.

- The owner of the view 
- CONTROL TABLE ON TABLE for the view
- (DROP VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
- DROP ANY VIEW ON DATABASE

<a id="39ba9677785ce5d4"></a>
### Syntax Rules and Parameters

<a id="617f5048d3f79d88"></a>
#### IF EXISTS

No error is raised even if the specified view does not exist.

<a id="b9b2bcd82efb1d9a"></a>
#### view_name

It is the name of the view to be dropped.  
The schema to which the table belongs can be defined using the format schema_name.view_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

<a id="874fc0121cffbeca"></a>
### Description

Even Data Definition Language (DDL) statements such as DROP VIEW can be rolled back, as long as the transaction has not been committed.

<a id="cde643924ab5c876"></a>
### Examples

The following is an example of dropping a view.

```
gSQL> DROP VIEW v1;

View dropped.
```

The following example uses the IF EXISTS clause to avoid raising an error if the specified view does not exist.

```
gSQL> DROP VIEW IF EXISTS not_exist_view;

View dropped.
```

<a id="9d61b2deecac2dd2"></a>
### Compatibility

The SQL standard does not define the IF EXISTS clause.

**SQL standard compatibility**

<a id="8648b0ffddf2fe89"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="c96e6b2624d2a794"></a>
### For More Information

Refer to the following.

- [CREATE VIEW](#5d56559b64b8b9ae)
- [ALTER VIEW](18-sql-references-a-b.md#119e4fa9e88f98df)

<a id="dda14e1000da63d4"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="64fd6a0919931e05"></a>
### Function

It executes a dynamic SQL statement that was not defined at the time of writing the program.

<a id="4b8890f796ea2087"></a>
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

<a id="6ed117c4d61e9322"></a>
### Invocation and Access Rules

It can be used in embedded SQL.  
The appropriate execution privileges for the type of dynamic SQL statement must be granted.

<a id="0072ca12a6c20eb6"></a>
### Syntax Rules and Parameters

<a id="7afade701fb77b71"></a>
#### &lt;SQL statement variable&gt;

A dynamic SQL statement referenced by a &lt;SQL statement variable&gt; cannot use host variables (:var) or parameter markers (?).

The following four types of &lt;SQL statement variable&gt; can be used.

- variable_name: It is a variable that contains the SQL statement. 
- 'sql statement': It is an SQL statement enclosed in single quotes ('). 
- "sql statement": It is an SQL statement enclosed in double quotes ("). 
- sql statement: It is an SQL statement without any quotes.

To represent string data within a single-quoted string, two single quotes ('') must be used as follows.

```
{
    ...
    EXEC SQL EXECUTE IMMEDIATE 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

If the SQL statement is a query that produces a result set, it will execute successfully, but the result cannot be retrieved.

<a id="ec5565a0792d135c"></a>
#### variable_name

The type corresponding to variable_name must be a character string.  
The dynamic SQL statement defined in variable_name must be valid.

<a id="52326c5cf55edf70"></a>
#### sql statement

The dynamic SQL statement defined in the sql statement must be valid.

<a id="48c2e110a2896447"></a>
### Description

The EXECUTE IMMEDIATE 'sql_string' statement can be used for non-query SQL operations that do not include host variables in a dynamic embedded SQL application.  
It is suitable for executing one-off DDL or DML statements, as it does not require a separate preparation step.

For more information, refer to  [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#125731fd5648b0c7).

<a id="daa9576f55ead2cc"></a>
### Example

The following is an example of using EXECUTE IMMEDIATE 'sql_string' in embedded SQL source code.

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

The full source code that uses EXECUTE IMMEDIATE 'sql_string' can be found in the [Dynamic Embedded SQL Example Program](../part-05-developer-manual/36-embedded-sql.md#9e34f0e2b9235743).

<a id="bff3a04e85be6d07"></a>
### Compatibility

**SQL standard compatibility**

<a id="71dd2393684cdadd"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="459681b712cd2b42"></a>
### For More Information

Refer to the following.

- [PREPARE statement_name](20-sql-references-h-z.md#ff813c116e09eff4)
- [EXECUTE statement_name](#69d4b817b99bec5b)
- [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#125731fd5648b0c7)

<a id="69d4b817b99bec5b"></a>
## EXECUTE statement_name

<a id="ec2293581bdd9257"></a>
### Function

It executes a prepared statement.

<a id="a3242b48879528be"></a>
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

<a id="7fbb33a27ecbbb9e"></a>
### Invocation and Access Rules

It can be used in embedded SQL.  
Appropriate execution privileges must be granted for the type of dynamic SQL statement.

<a id="87ba25b2a688679a"></a>
### Syntax Rules and Parameters

<a id="d22adc29a90ef4f0"></a>
#### statement_name

It is the name of the prepared statement.  
statement_name must be prepared in advance using the [PREPARE statement_name](20-sql-references-h-z.md#ff813c116e09eff4) syntax.

If the dynamic SQL statement referenced by statement_name includes dynamic parameters, a &lt;parameter using clause&gt; must be specified.

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

If the dynamic SQL statement referenced by statement_name is a query or a stored function that returns a result, a &lt;result into clause&gt; must be specified.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT COUNT(*) FROM t1';
    EXEC SQL EXECUTE stmt1 INTO :sValue;
    ...
}
```

If multiple queries are executed, they run normally, but only the result of the first statement can be retrieved.  
To retrieve multiple rows, cursor-related statements must be used as follows:

- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [FETCH cursor_name](#b4d62d5536bcdf22)
- [CLOSE cursor_name](#a47858c9b07fa0f3)

If the query produces no result, the operation completes with NO DATA.

<a id="d638dd895b8fed41"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

The &lt;parameter using clause&gt; and &lt;result into clause&gt; can be specified in any order, but must not be used more than once.

<a id="3902f607377f0811"></a>
#### &lt;parameter using clause&gt;

If the dynamic SQL statement referenced by statement_name contains parameters, information about those parameters must be provided using the &lt;using parameter arguments&gt; clause.

<a id="6cb173b96d9294f9"></a>
#### &lt;using parameter arguments&gt;

When the &lt;using parameter arguments&gt; clause is used, the number of variable_name entries must match the number of parameters in the dynamic SQL statement referenced by statement_name.

The listed variable_names correspond to the dynamic parameters in the order in which they appear.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2, :sValue3;
    ... 
}
```

<a id="9272ff9f11f4238d"></a>
#### &lt;result into clause&gt;

If the dynamic SQL statement referenced by statement_name is a query, information about the result columns must be specified using the &lt;into result arguments&gt; clause.

If a result value is null and no INDICATOR variable is specified, a [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error will occur.

<a id="b78b6dac48c4a172"></a>
#### &lt;into result arguments&gt;

When the &lt;into result arguments&gt; clause is used, the number of variable_names must match the number of result columns in the dynamic SQL statement referenced by statement_name.

The listed variable_name corresponds to the dynamic parameter in the order of its description.

```
{

    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT MIN(salary), MAX(salary), AVG(salary) FROM employee';
    EXEC SQL EXECUTE stmt1 INTO :sMinValue, :sMaxValue, :sAvgValue;
    ... 
}
```

<a id="e29c79bd664f47a8"></a>
### Description

statement_name is an identifier that informs the precompiler of the statement in the embedded SQL source code.  
A separate type or declaration is not required, as statement_name is not a host variable.  
The EXECUTE statement_name must be written after the PREPARE statement_name.

For more information, refer to [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#125731fd5648b0c7).

<a id="dc6dd97accc3e412"></a>
### Example

The following is an example of using EXECUTE statement_name in embedded SQL source code.

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

The full source code that uses EXECUTE statement_name can be found in the [Dynamic Embedded SQL Example Program](../part-05-developer-manual/36-embedded-sql.md#9e34f0e2b9235743).

<a id="e39eb3371f3f4db5"></a>
### Compatibility

**SQL standard compatibility**

<a id="885c083dea15227c"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="e9dcb9505a2cce00"></a>
### For More Information

Refer to the following.

- [PREPARE statement_name](20-sql-references-h-z.md#ff813c116e09eff4)
- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [FETCH cursor_name](#b4d62d5536bcdf22)
- [CLOSE cursor_name](#a47858c9b07fa0f3)
- [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#125731fd5648b0c7)

<a id="b4d62d5536bcdf22"></a>
## FETCH cursor_name

<a id="303fd8f74ef89824"></a>
### Function

It positions the cursor on a specific row of the result set and retrieves the values of that row into host variables.

<a id="656042414fb6a6f4"></a>
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

<a id="87cdc624c3f639c1"></a>
### Syntax Rules and Parameters

<a id="eb5596e44608540f"></a>
#### [ FROM ] cursor_name

It must be a cursor that is open within the session.  
The FROM clause can be omitted.

<a id="338a11656059d5ee"></a>
#### &lt;fetch orientation&gt;

To use a &lt;fetch orientation&gt; other than FETCH NEXT, a scrollable cursor must be used.  
If &lt;fetch orientation&gt; is omitted, the default is NEXT.

An open cursor maintains position information for the result set as shown below.

<a id="ff6a840c093ed782"></a>
![Cursor position information](../assets/images/04550d3d3a9e3f0f.png)

**Cursor position**

<a id="f46309879d5152e4"></a>
| Position | Description |
| --- | --- |
| BEFORE THE FIRST ROW | The cursor is positioned before the first row of the result set. This is also the initial position when the cursor is opened. |
| ON A CERTAIN ROW | The cursor is positioned on a specific row of the result set by a FETCH operation. |
| AFTER THE LAST ROW | The cursor is positioned after the last row of the result set. |

The behavior of &lt;fetch orientation&gt; based on the cursor position is as follows.

- NEXT: It retrieves the row following the current cursor position. 
- PRIOR: It retrieves the row preceding the current cursor position. 
- FIRST: It retrieves the first row of the result set.
- LAST: It retrieves the last row of the result set.
- CURRENT: It retrieves the row at the current cursor position.
- ABSOLUTE position 
    - It retrieves the row at the specified absolute position in the result set. 
    - If the position is negative, the row is counted backward from AFTER THE LAST ROW.
- RELATIVE position 
    - It retrieves the row located the specified number of rows away from the current cursor position.

<a id="6b625255dfab9759"></a>
#### &lt;result into clause&gt;

The variables to receive the result columns are specified using &lt;into result arguments&gt;.

If a result value is null and no INDICATOR variable is specified, a [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error will occur.

<a id="529aa0c350029f85"></a>
#### &lt;into result arguments&gt;

The number of variables specified in the INTO clause must be the same as the number of columns in the cursor's result set.

<a id="37b606bfa9bf3e8f"></a>
### Description

If the cursor is positioned BEFORE THE FIRST ROW or AFTER THE LAST ROW after performing a FETCH, it remains at that position regardless of the value specified in &lt;fetch orientation&gt;.

<a id="9c403fe76f2d9112"></a>
### Example

The following is an example of declaring a SCROLL cursor using interactive SQL (gsql) and demonstrating the behavior of various &lt;fetch orientation&gt; options.

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

<a id="414110236c4275b9"></a>
### Compatibility

The SQL standard does not define CURRENT among &lt;fetch orientation&gt; options.

**SQL standard compatibility**

<a id="f1b6a4d1dc2d4fdd"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="84d5d6c03fd319c9"></a>
### For More Information

Refer to the following.

- [DECLARE cursor_name](#ccb6dc5ecb7cf850)
- [OPEN cursor_name](20-sql-references-h-z.md#f2fc3f30b9aedce3)
- [CLOSE cursor_name](#a47858c9b07fa0f3)

<a id="69b2f9ab182ec9e2"></a>
## FLASHBACK TABLE

<a id="d60f34948648aca5"></a>
### Function

It restores the table object that was stored in the recycle bin.

<a id="67e4a1aae9a5422f"></a>
### Syntax

```
<flashback table statement> ::=
    FLASHBACK TABLE table_name
    TO BEFORE DROP [ RENAME TO new_table_name ]
    ;
```

<a id="aac811ffbe1a5a37"></a>
### Invocation and Access Rules

One of the following privileges is required to execute the &lt;flashback table statement&gt;.

- The owner of the table
- CONTROL TABLE ON TABLE for that table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="539dda9a5f024629"></a>
### Syntax Rules and Parameters

<a id="578cd32a13e01b9e"></a>
#### table_name

It is the name of the object stored in the recycle bin, or the name of the dropped table.  
The schema to which the dropped table belongs can be defined using the format schema_name.table_name. If schema_name is omitted, the default schema of the user executing the statement will be used.

<a id="b0db731256ff931a"></a>
#### new_table_name

This is the new name of the table to be restored.  
There must not be another table with the same name within the schema.

<a id="02b1fd1fc2578b4c"></a>
### Description

It restores a table object stored in the recycle bin using either the object name in the recycle bin or the original name of the dropped table. If multiple tables with the same name exist in the recycle bin, the most recently dropped table is restored.

If a table with the same name as the one being restored already exists in the schema, an error occurs. In this case, the table can be restored under a new name using the RENAME TO clause.  
Constraints and indexes are restored with their original names. However, if a constraint or index with the original name already exists, they are restored with the names they had in the recycle bin.

Unlike other Data Definition Language (DDL) operations, the FLASHBACK TABLE statement cannot be rolled back, and the transaction is automatically committed upon execution.

<a id="734c681364135a23"></a>
### Example

The following is an example of restoring a table using the object name stored in the recycle bin.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

1 row selected.

gSQL> FLASHBACK TABLE "BIN$106A4F90165D11EA9C5C835D3E4BBBF7" TO BEFORE DROP;

Flashback complete.
```

The following is an example of restoring a table from the recycle bin using its original name before it was dropped.

```
gSQL> SELECT SCHEMA_NAME, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

SCHEMA_NAME OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE
----------- ------------------------------------ ------------- -----------
PUBLIC      BIN$106A4F90165D11EA9C5C835D3E4BBBF7 T1            TABLE      

gSQL> FLASHBACK TABLE T1 TO BEFORE DROP;

Flashback complete.
```

<a id="a7eef021df844dec"></a>
### Compatibility

The SQL standard does not define the &lt;flashback table statement&gt;.

<a id="5f40c3dfb2159b45"></a>
### For More Information

Refer to the following.

- [Managing Recycle Bin of Table](13-sql-objects.md#a69c745bde09025b)
- [PURGE](20-sql-references-h-z.md#5574787c1a0b3492)

<a id="bd0f6497073f3a8e"></a>
## GRANT privileges TO

<a id="c60666c74b5f5010"></a>
### Function

It grants privileges to a user or role.

<a id="04d3ae1f8778802b"></a>
### Syntax

```
<grant privilege statement> ::=
    GRANT <privilege> TO <grantee> [, ...]
        [ WITH GRANT OPTION ]
    ;

<grantee> ::=
      PUBLIC
    | user_identifier
    | role_name
    
<privilege> ::=
      <database privilege>
    | <tablespace privilege>
    | <schema privilege>
    | <table privilege>
    | <sequence privilege>
    | <procedure privilege>
    | <package privilege>
    | <library privilege>

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
    | GRANT ROLE
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
    | CREATE ANY LIBRARY
    | DROP ANY LIBRARY
    | EXECUTE ANY LIBRARY
    | CREATE ANY TRIGGER
    | ALTER ANY TRIGGER
    | DROP ANY TRIGGER
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
    | CREATE LIBRARY
    | DROP LIBRARY
    | EXECUTE LIBRARY
    | CREATE TRIGGER
    | ALTER TRIGGER
    | DROP TRIGGER

<table privilege> ::=
      ALL [ PRIVILEGES ] ON [TABLE] table_name
    | { <table action> | <column action> } [, ...] ON [TABLE] table_name

<table action> ::=
      CONTROL TABLE
    | SELECT
    | INSERT
    | UPDATE
    | DELETE
    | TRIGGER
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

<library privilege> ::=
      ALL [ PRIVILEGES ] ON LIBRARY library_name
    | <library action> ON LIBRARY library_name

<library action> ::=
      EXECUTE
```

<a id="b39e7b980a9d2ca0"></a>
### Syntax Rules and Parameters

<a id="c606487b95376aa4"></a>
#### &lt;grantee&gt;

It is the user or role to which the privileges are to be granted.

- user_identifier 
    - It grants the privilege to a specific user.
- role_name
    - It grants the privilege to a specific role.
- PUBLIC 
    - It is an authorization object that represents all users and roles.

<a id="b7cb55e1e61f2c6a"></a>
#### WITH GRANT OPTION

It allows the grantee to grant the privilege to other users.  
The WITH GRANT OPTION is permitted only when the grantee is a user.

When the same &lt;privilege&gt; is granted as follows, the WITH GRANT OPTION is retained.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="79c5b74234fe6d04"></a>
#### &lt;privilege&gt;

It is a privilege to be granted to a grantee (the user or role receiving the privilege).

The grantor (the user executing the statement) must meet one of the following conditions:

- The grantor owns the &lt;privilege&gt; with the WITH GRANT OPTION.
    - The grantor is the user who executes the statement.
- The grantor owns the ACCESS CONTROL ON DATABASE privilege.
    - The grantor is the owner of the object. 
        - &lt;database privilege&gt;: _SYSTEM account
        - &lt;tablespace privilege&gt;: _SYSTEM account 
        - &lt;schema privilege&gt;: _SYSTEM account
        - &lt;table privilege&gt;: Owner of the table 
        - &lt;sequence privilege&gt;: Owner of the sequence
        - &lt;procedure privilege&gt;: Owner of the procedure/function
        - &lt;package privilege&gt;: Owner of the package
        - &lt;library privilege&gt;: Owner of the library

<a id="134b53c6ac691c87"></a>
#### &lt;database privilege&gt;

It is the privilege for database objects.  
The [ON DATABASE] clause can be omitted.

The database actions that can be defined with a database privilege are as follows:

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - All privileges on the specified database that the grantor (the user executing the statement) owns by using WITH GRANT OPTION.

**Database privilege**

<a id="271a027f3a820a6d"></a>
| &lt;database action&gt; | Description |
| --- | --- |
| ADMINISTRATION | Privilege to start or shut down the server |
| ALTER DATABASE | Privilege to execute the ALTER DATABASE statement |
| ALTER SYSTEM | Privilege to execute the ALTER SYSTEM statement |
| AUDIT SYSTEM | Privilege to manage audit policies |
| ACCESS CONTROL | Privilege to control all database privileges |
| CREATE SESSION | Privilege to connect to the database |
| CREATE PROFILE | Privilege to create profiles in the database |
| ALTER PROFILE | Privilege to alter any profile in the database |
| DROP PROFILE | Privilege to drop any profile in the database |
| CREATE USER | Privilege to create users in the database |
| ALTER USER | Privilege to alter any user in the database |
| DROP USER | Privilege to drop any user in the database |
| CREATE ROLE | Privilege to create roles in the database |
| ALTER ROLE | Privilege to alter any role in the database |
| DROP ROLE | Privilege to drop any role in the database |
| GRANT ROLE | Privilege to grant any role in the database |
| CREATE TABLESPACE | Privilege to create tablespaces in the database |
| ALTER TABLESPACE | Privilege to alter any tablespace in the database |
| DROP TABLESPACE | Privilege to drop any tablespace in the database |
| USAGE TABLESPACE | Privilege to use any tablespace in the database |
| CREATE SCHEMA | Privilege to create schemas in the database |
| ALTER SCHEMA | Privilege to alter any schema in the database |
| DROP SCHEMA | Privilege to drop any schema in the database |
| CREATE PUBLIC SYNONYM | Privilege to create public synonyms in the database |
| DROP PUBLIC SYNONYM | Privilege to drop any public synonym in the database |
| CREATE ANY TABLE | Privilege to create tables in any schema of the database |
| ALTER ANY TABLE | Privilege to alter any table in the database |
| DROP ANY TABLE | Privilege to drop any table in the database |
| SELECT ANY TABLE | Privilege to query rows from any table in the database |
| INSERT ANY TABLE | Privilege to insert rows into any table in the database |
| DELETE ANY TABLE | Privilege to delete rows from any table in the database |
| UPDATE ANY TABLE | Privilege to update rows in any table in the database |
| LOCK ANY TABLE | Privilege to lock any table in the database |
| CREATE ANY VIEW | Privilege to create views in any schema of the database |
| DROP ANY VIEW | Privilege to drop any view in the database |
| CREATE ANY SEQUENCE | Privilege to create sequences in any schema of the database |
| ALTER ANY SEQUENCE | Privilege to alter any sequence in the database |
| DROP ANY SEQUENCE | Privilege to drop any sequence in the database |
| USAGE ANY SEQUENCE | Privilege to use any sequence in the database |
| CREATE ANY INDEX | Privilege to create indexes in any schema of the database |
| ALTER ANY INDEX | Privilege to alter any index in the database |
| DROP ANY INDEX | Privilege to drop any index in the database |
| CREATE ANY SYNONYM | Privilege to create synonyms in any schema of the database |
| DROP ANY SYNONYM | Privilege to drop any synonym in the database |
| CREATE ANY PROCEDURE | Privilege to create procedures or functions in any schema of the database |
| ALTER ANY PROCEDURE | Privilege to alter any procedure or function in the database |
| DROP ANY PROCEDURE | Privilege to drop any procedure or function in the database |
| EXECUTE ANY PROCEDURE | Privilege to execute any procedure or function in the database |
| CREATE ANY PACKAGE | Privilege to create packages in any schema of the database |
| ALTER ANY PACKAGE | Privilege to alter any package in the database |
| DROP ANY PACKAGE | Privilege to drop any package in the database |
| EXECUTE ANY PACKAGE | Privilege to execute any package of the database |
| CREATE ANY LIBRARY | Privilege to create libraries in any schema of  the database |
| DROP ANY LIBRARY | Privilege to drop any library in the database |
| EXECUTE ANY LIBRARY | Privilege to execute any library in the database |
| CREATE ANY TRIGGER | Privilege to create triggers in any schema of the database |
| ALTER ANY TRIGGER | Privilege to alter any trigger in the database |
| DROP ANY TRIGGER | Privilege to drop any trigger in the database |
| PURGE DBA_RECYCLEBIN | Privilege to purge the entire recycle bin in the database |

<a id="4bbeb7157db79704"></a>
#### &lt;tablespace privilege&gt;

It is the privilege for tablespace objects.

The tablespace actions that can be defined with a tablespace privilege are as follows:

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - All privileges on the specified tablespace that the grantor (the user executing the statement) owns by using WITH GRANT OPTION.

**Tablespace privilege**

<a id="be0d75db8be2ef22"></a>
| &lt;tablespace action&gt; | Description |
| --- | --- |
| CREATE OBJECT | Privilege to create objects in the tablespace |

<a id="9a864bad100ca61f"></a>
#### &lt;schema privilege&gt;

It is the privilege for schema objects.

- Omission of [ON SCHEMA schema_name]
    - If there are multiple &lt;grantee&gt; values, the [ON SCHEMA schema_name] clause must not be omitted.
    - If ALL [PRIVILEGES] is specified, the [ON SCHEMA schema_name] clause must not be omitted.
    - If the [ON SCHEMA schema_name] clause is omitted, only one user_identifier can be specified as &lt;grantee&gt;, and the privilege is granted on the first schema in the grantee's schema search path.

The schema actions that can be defined with a schema privilege are as follows:

- ALL [ PRIVILEGES ] ON SCHEMA schema_name 
    - All privileges on the specified schema that the grantor (the user executing the statement) owns by using WITH GRANT OPTION.

**Schema privilege**

<a id="9fa9b0fded32ede5"></a>
| &lt;schema action&gt; | Description |
| --- | --- |
| CONTROL SCHEMA | All privileges on the schema |
| CREATE TABLE | Privilege to create tables in the schema |
| ALTER TABLE | Privilege to alter any table in the schema |
| DROP TABLE | Privilege to drop any table in the schema |
| SELECT TABLE | Privilege to query rows of any table in the schema |
| INSERT TABLE | Privilege to insert rows into any table in the schema |
| DELETE TABLE | Privilege to delete rows from any table in the schema |
| UPDATE TABLE | Privilege to update rows of any table in the schema |
| LOCK TABLE | Privilege to lock any table in the schema |
| CREATE VIEW | Privilege to create views in the schema |
| DROP VIEW | Privilege to drop any view in the schema |
| CREATE SEQUENCE | Privilege to create sequences in the schema |
| ALTER SEQUENCE | Privilege to alter any sequence in the schema |
| DROP SEQUENCE | Privilege to drop any sequence in the schema |
| USAGE SEQUENCE | Privilege to use any sequence in the schema |
| CREATE INDEX | Privilege to create indexes in the schema |
| ALTER INDEX | Privilege to alter any index in the schema |
| DROP INDEX | Privilege to drop any index in the schema |
| CREATE SYNONYM | Privilege to create synonyms in the schema |
| DROP SYNONYM | Privilege to drop any synonym in the schema |
| CREATE PROCEDURE | Privilege to create procedures/functions in the schema |
| ALTER PROCEDURE | Privilege to alter any procedure/function in the schema |
| DROP PROCEDURE | Privilege to drop any procedure/function in the schema |
| EXECUTE PROCEDURE | Privilege to execute any procedure/function in the schema |
| CREATE PACKAGE | Privilege to create packages in the schema |
| ALTER PACKAGE | Privilege to alter any package in the schema |
| DROP PACKAGE | Privilege to drop any package in the schema |
| EXECUTE PACKAGE | Privilege to execute any package in the schema |
| CREATE LIBRARY | Privilege to create libraries in the schema |
| DROP LIBRARY | Privilege to drop any library in the schema |
| EXECUTE LIBRARY | Privilege to execute any library in the schema |
| CREATE TRIGGER | Privilege to create triggers in the schema |
| ALTER TRIGGER | Privilege to alter any trigger in the schema |
| DROP TRIGGER | Privilege to drop any trigger in the schema |

<a id="4eabcc60112d6ca3"></a>
#### &lt;table privilege&gt;

It is the privilege for table objects or view objects.  
The [TABLE] clause can be omitted.

The table actions that can be defined with the table privilege are as follows:

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - All privileges on the specified table that the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Table privilege**

<a id="3eaee320d4927f49"></a>
| &lt;table action&gt; | Description |
| --- | --- |
| CONTROL TABLE | All privileges on the specified table |
| SELECT | Privilege to query rows from the table |
| INSERT | Privilege to insert rows into the table |
| UPDATE | Privilege to update rows in the table |
| DELETE | Privilege to delete rows from the table |
| TRIGGER | Privilege to create triggers on the table |
| REFERENCES | Privilege to create referential constraints that reference the table |
| LOCK | Privilege to lock the table |
| INDEX | Privilege to create indexes on the table |
| ALTER | Privilege to alter the table |

For SELECT, INSERT, UPDATE, and REFERENCES, additional privileges are granted on all columns of the table.

The column actions that can be defined with the table privilege are as follows.  
Note that column actions apply only to base tables.

**Column privilege**

<a id="509b64b774e41232"></a>
| &lt;column action&gt; | Description |
| --- | --- |
| SELECT (columns) | Privilege to query the specified columns |
| INSERT (columns) | Privilege to insert rows including the specified columns |
| UPDATE (columns) | Privilege to update the specified columns |
| REFERENCES (columns) | Privilege to create referential constraints that reference the specified columns |

<a id="4beeb8e028d05f6d"></a>
#### &lt;sequence privilege&gt;

It is the privilege for sequence objects.

The sequence actions that can be defined with the sequence privilege are as follows:

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - All privileges on the specified sequence that the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Sequence privilege**

<a id="e73b08693d592f13"></a>
| &lt;sequence action&gt; | Description |
| --- | --- |
| USAGE | Privilege to use the sequence |

<a id="a50cb5669c4497c3"></a>
#### &lt;procedure privilege&gt;

It is the privilege for procedures/ function objects.

The actions that can be defined with the procedure privilege are as follows:

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - All privileges on the specified procedure/ function that the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Procedure privilege**

<a id="16b54d7ff7ad65f8"></a>
| &lt;procedure action&gt; | Description |
| --- | --- |
| EXECUTE | Privilege to execute the procedure/function |

<a id="cc24ebd33928dcc0"></a>
#### &lt;package privilege&gt;

It is the privilege for package objects.

The actions that can be defined with the package privilege are as follows:

- ALL [ PRIVILEGES ] ON PACKAGE package_name
    - All privileges on the specified package that the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Package privilege**

<a id="a52dbc5a92206461"></a>
| &lt;package action&gt; | Description |
| --- | --- |
| EXECUTE | Privilege to execute the package |

<a id="cc854a72b97a0018"></a>
#### &lt;library privilege&gt;

It is the privilege for library objects.

The actions that can be defined with the library privilege are as follows.

- ALL [ PRIVILEGES ] ON LIBRARY library_name
    - All privileges on the specified library that the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Library privilege**

<a id="b3b521e29ba557c0"></a>
| &lt;package action&gt; | Privilege for executing the package |
| --- | --- |
| EXECUTE | Privilege to execute the library |

<a id="db34538f6fb2039c"></a>
### Description

Data Definition Language (DDL) such as GRANT privileges can be rolled back as long as the transaction has not been committed.

An owner who creates a SQL schema object—such as a table or sequence—automatically receives certain privileges on that object without requiring explicit privilege grants.  
For more information, refer to the following CREATE statements:

- [CREATE TABLE](#47f3ce328094503e)
- [CREATE VIEW](#5d56559b64b8b9ae)
- [CREATE SEQUENCE](#630728df3a71a28b)
- [ALTER TABLE name ADD COLUMN](18-sql-references-a-b.md#a075befc84515f66) 
- [CREATE FUNCTION](../part-04-sql-psm-manual/31-psm-sql-references.md#8343c001bfba29fc)
- [CREATE PROCEDURE](../part-04-sql-psm-manual/31-psm-sql-references.md#d439613cbc283235)
- [CREATE PACKAGE](../part-04-sql-psm-manual/31-psm-sql-references.md#d67c80375fa9e3c8)
- [CREATE LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#d3c4a1abc483c544)
- [CREATE TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#44e30f425949fd8e)

However, for non-schema objects—such as schemas or tablespaces—the creator (owner) does not automatically receive any privileges on the object. Therefore, explicit privilege grants are required.  
For more information, refer to the following CREATE statements:

- [CREATE SCHEMA](#0173622cce38fc3c)
- [CREATE TABLESPACE](#8ab1dca3b8dad438)
- [CREATE USER](#409f34806636a0ff)

<a id="8f2c71b027bd8e78"></a>
### Examples

The following is an example of granting the SELECT ON TABLE t1 privilege to user u1.

```
gSQL> GRANT SELECT ON t1 TO u1;

Grant succeeded.
```

The following is an example of granting the SELECT ON TABLE t1 privilege to the PUBLIC account, which refers to all authorizations (users and roles).

```
gSQL> GRANT SELECT ON t1 TO PUBLIC;

Grant succeeded.
```

The following is an example of user u1 granting this privilege to other users using the WITH GRANT OPTION.

```
gSQL> GRANT SELECT ON t1 TO u1 WITH GRANT OPTION;

Grant succeeded.
```

The following is an example of the user executing the statement granting all privileges they own on TABLE t1 to user u1 using the WITH GRANT OPTION.

```
gSQL> GRANT ALL PRIVILEGES ON TABLE t1 TO u1;

Grant succeeded.
```

The following is an example of granting the CREATE SESSION ON DATABASE privilege, which allows a user to connect to the database.

```
gSQL> GRANT CREATE SESSION ON DATABASE TO u1;

Grant succeeded.
```

The following is an example of granting multiple privileges to user u1 for creating objects such as tables, views, indexes, and sequences in SCHEMA s1.

```
gSQL> GRANT CREATE TABLE, CREATE VIEW, CREATE INDEX, CREATE SEQUENCE ON SCHEMA s1 TO u1;

Grant succeeded.
```

The following is an example of granting the privilege to create objects in TABLESPACE mem_data_tbs to user u1.

```
gSQL> GRANT CREATE OBJECT ON TABLESPACE mem_data_tbs TO u1;

Grant succeeded.
```

The following is an example of granting user u1 the privilege to query specific columns in TABLE t1.

```
gSQL> GRANT SELECT( id, name ) ON TABLE t1 TO u1;

Grant succeeded.
```

The following is an example of granting user u1 the privilege to use the NEXTVAL() and CURRVAL() functions on SEQUENCE seq1.

```
gSQL> GRANT USAGE ON SEQUENCE seq1 TO u1;
Grant succeeded.
```

The following is an example of granting the SELECT ON TABLE t1 privilege to role1.

```
gSQL> GRANT SELECT ON t1 TO role1;  

Grant succeeded.
```

<a id="9263bf86c083662a"></a>
### Compatibility

The SQL standard does not define the following privileges.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL standard compatibility**

<a id="fd17ed5697bd5ef1"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | O |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="e99406714c050886"></a>
### For More Information

Refer to the following.

- [REVOKE privileges FROM](20-sql-references-h-z.md#6f3292517bedb93d)
- [CREATE USER](#409f34806636a0ff)
- [DROP USER](#7979783b911846c2)
- [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2)
- [CREATE ROLE](#635504efdc11b072)
- [DROP ROLE](#9c173c3287657d63)

<a id="08d2b8947feab7b4"></a>
## GRANT role TO

<a id="6b80f7525a0a5510"></a>
### Function

It grants the role to a user or another role.

<a id="2e6822299551022a"></a>
### Syntax

```
<grant role statement> ::=
    GRANT <role granted> [ , ... ] TO <grantee> [ , ... ]
        [ WITH ADMIN OPTION ]
    ;

<role granted> ::=
    <role_name>

<grantee> ::=
      PUBLIC
    | <user_identifier>
    | <role_name>
```

<a id="0bae0e500ccf2270"></a>
### Invocation and Access Rules

One of the following conditions must be satisfied to execute a &lt;grant role statement&gt;.

- The user should have GRANT ROLE ON DATABASE privilege.
- WITH ADMIN OPTION should be granted for &lt;role_name&gt;.

<a id="59ef7f849d98ab59"></a>
### Syntax Rules and Parameters

<a id="134d69b789e2fbe4"></a>
#### &lt;role granted&gt;

It is the name of the role to be granted.

<a id="fbcad610446dc4a7"></a>
#### &lt;grantee&gt;

It is the user or role that is to be granted the role.

- &lt;user_identifier&gt;
    - It grants the role to a user.
- &lt;role_name&gt;
    - It grants the role to another role.
- PUBLIC 
    - It is an authorization object that represents all users and roles.

<a id="390ddafa8de4e9ff"></a>
#### WITH ADMIN OPTION

It allows the grantee (the user or role receiving the role) to grant the role to other users or roles.

When the same &lt;role granted&gt; is granted multiple times as shown below, the WITH ADMIN OPTION is preserved:

- GRANT role1 TO u1 WITH ADMIN OPTION;
- GRANT role1 TO u1;

<a id="39973e351d7dd9e8"></a>
### Description

It grants the role to another user or role.  
Data Definition Language (DDL) statements such as GRANT role can be rolled back if the transaction has not yet been committed.

When a user creates a role, the role is automatically granted to that user with the WITH ADMIN OPTION, even if it is not explicitly granted.   
For more information, refer to the [CREATE ROLE](#635504efdc11b072) statement.

<a id="a8302bcbd1f44351"></a>
### Examples

The following is an example of a user with the GRANT ROLE ON DATABASE privilege granting a role.

```
gSQL> GRANT GRANT ROLE ON DATABASE TO u1;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 
U1      GRANT ROLE ON DATABASE     

2 rows selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

no rows selected.

gSQL> \connect u1 u1

gSQL> GRANT role1 TO role2;

Grant succeeded.
```

The following is an example of a user with the WITH ADMIN OPTION for a role granting that role.

```
gSQL> GRANT role1 TO u1 WITH ADMIN OPTION;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 

1 row selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

GRANTEE GRANTED_ROLE ADMIN_OPTION
------- ------------ ------------
U1      ROLE1        YES         

1 row selected.

gSQL> \connect u1 u1

gSQL> GRANT role1 TO role2;

Grant succeeded.
```

<a id="ca4d17e9b4039e6a"></a>
### Compatibility

**SQL standard compatibility**

<a id="2bc6831085e93006"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |

<a id="d1ab56281ceb2216"></a>
### For More Information

Refer to the following.

- [REVOKE role FROM](20-sql-references-h-z.md#56d94492714e9b12)
- [CREATE USER](#409f34806636a0ff)
- [DROP USER](#7979783b911846c2)
- [ALTER USER](18-sql-references-a-b.md#0cc4292dd9d412b2)
- [CREATE ROLE](#635504efdc11b072)
- [DROP ROLE](#9c173c3287657d63)

---

[← 18. SQL References (A~B)](18-sql-references-a-b.md) · [Table of contents](../README.md) · [20. SQL References (H~Z) →](20-sql-references-h-z.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
