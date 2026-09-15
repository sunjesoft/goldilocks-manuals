<a id="9f07a05c50b7a826"></a>

# 16. SQL References

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/9f07a05c50b7a826)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Overview of PSM →](../part-04-psm-manual/17-overview-of-psm.md)

<a id="41e688c628dec27b"></a>
## ALTER AUDIT POLICY

<a id="3d33c31ef4efb480"></a>
### Function

It adds an auditing target to an audit policy object, or drops an auditing target from an audit policy object.

<a id="57de7a3be9981fde"></a>
### Syntax

```
<alter audit policy statement> ::= 
    ALTER AUDIT POLICY policy_name
    { <add_audit_option> | <drop_audit_option> }
    ;

<add_audit_option> ::=
    ADD { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }

<drop_audit_option> ::=
    DROP { <privilege_audit_clause> |  <action_audit_clause> | <privilege_audit_clause> <action_audit_clause> }


<privilege_audit_clause> ::=
    PRIVILEGES <database_privilege> [, ...]

<action_audit_clause> ::=
    ACTIONS { <object_action_audit> | <system_action_audit> } [, ...]

<object_action_audit> ::=
      ALL ON [schema_name.]object_name
    | <object_action> ON [schema_name.]object_name

<system_action_audit> ::=
      ALL
    | <system_action>
```

<a id="048c970d54feeb10"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;alter audit policy statement&gt;.

<a id="7885e6cb630a85fb"></a>
### Syntax Rules and Parameters

<a id="26e86a8b99d1963c"></a>
#### policy_name

It is the name of an audit policy object to be altered.

<a id="69574a65f33e4622"></a>
#### &lt;add_audit_option&gt;

It adds an auditing target to an audit policy.

<a id="d7d317e15adc4c16"></a>
#### &lt;drop_audit_option&gt;

It drops an auditing target from an audit policy.

<a id="1f3981fe82edaad0"></a>
#### &lt;privilege_audit_clause&gt;

For more information, refer to [CREATE AUDIT POLICY](#6be201c413853041).

<a id="afea814206bc86fa"></a>
#### &lt;action_audit_clause&gt;

For more information, refer to [CREATE AUDIT POLICY](#6be201c413853041).

<a id="f7a18911b32ffce3"></a>
### Description

It can alter an audit policy which is already activated, and it does not effect the existing session but it effects only the newly created session.

> When dropping ALL option as follows, not all actions are dropped, but only the corresponding ALL option is dropped.

```
CREATE AUDIT POLICY p1
       ACTIONS ALL ON u1.t1,
               SELECT ON u1.t1;

ALTER AUDIT POLICY p1 DROP
      ACTIONS ALL ON u1.t1;
```

<a id="23d7c564e6047fe7"></a>
### Examples

The following is an example of adding a new audit option to an audit policy.

```
ALTER AUDIT POLICY policy_dml
      ADD ACTIONS SELECT ON u1.t1;
```

The following is an example of dropping an audit option from an audit policy.

```
ALTER AUDIT POLICY policy_dml
      DROP ACTIONS SELECT ON u1.t1;
```

<a id="68c1d495f5615590"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="70dcf3bd1d6cf2dd"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy 
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Enquiring audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Dropping audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="0f86518c60487e59"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="43d259f08661fc4b"></a>
### Function

It adds a cluster member to a cluster group.

<a id="32cc6cbeac1de115"></a>
### Syntax

```
<alter cluster group add member statement> ::=
    ALTER CLUSTER GROUP group_name ADD
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute>

<connection attribute> ::
    HOST 'address' PORT port_no
```

<a id="0e094e9a3561f989"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster group add member statement&gt;.

<a id="38476a11d3ecf88a"></a>
### Syntax Rules and Parameters

<a id="238c5b176990543a"></a>
#### group_name

It is the cluster group name.

<a id="a34e6d4ff39ffba9"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group may include maximum 32 cluster members.

<a id="aa88a52bd644e953"></a>
#### member_name

It is the name of a cluster member.  
The cluster member name should be as same as the member name which was defined when the database of that cluster member was created.  
There should not be the same cluster group, nor the same cluster member.  
The length of the name should be shorter than 128 bytes.  
The start-up phase for the cluster member should be OPEN.

<a id="1054b959fc09f216"></a>
#### &lt;connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
&lt;connection attribute&gt; should be as same as the HOST and PORT which were defined when the database of that cluster member was created.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST 'address' uses ip v4 type. 
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="da610c1021d5ebdd"></a>
### Description

&lt;alter cluster group add member statement&gt; statement does not rebalance shards in the tables.  
The following statement should be performed to rebalance shards on the added cluster member.

- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="b15669605b82cfc0"></a>
### Examples

The following is an example of adding two cluster members to a cluster group.

```
gSQL>
ALTER CLUSTER GROUP g1 ADD
    CLUSTER MEMBER g1n3 HOST '192.168.0.13' PORT 10130,
    CLUSTER MEMBER g1n4 HOST '192.168.0.14' PORT 10140
;

Cluster Group altered.
```

<a id="29b0366b6e360f81"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="fc09dda1cedcb6c2"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [DROP CLUSTER GROUP](#7335700144f62a07)
- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="f8eaa3124c5d9541"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="b4b0cc980d218b25"></a>
### Function

It sets a cluster member of the cluster group to offline.

<a id="f9603cc653d2af98"></a>
### Syntax

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE
        <cluster member definition>
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name
    ;
```

<a id="2d1a0aeaedc761b8"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster group offline member statement&gt;.

<a id="60d86a6779fa2d75"></a>
### Syntax Rules and Parameters

<a id="0a647e3cfb0bbc75"></a>
#### group_name

It is the cluster group name.

<a id="21b1050d629dd413"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group may include maximum 32 cluster members.

<a id="3967b25cbdf2f641"></a>
#### member_name

It is the name of a cluster member.  
The cluster member name should be as same as the member name which was defined when the database of that cluster member was created.  
There should not be the same cluster group, nor the same cluster member.  
The length of the name should be shorter than 128 bytes.  
The start-up phase for the cluster member should be OPEN.

<a id="a45813425fdcaabb"></a>
### Description

&lt;alter cluster group offline member statement&gt; statement does not rebalance shards in the tables.

<a id="3b1ac36bcc4df10d"></a>
### Examples

The following is an example of setting a specific cluster member to offline.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE
    CLUSTER MEMBER g1n3
;
Cluster Group altered.
```

<a id="3e7aac735259fce9"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="df225d42ac26e0f6"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [DROP CLUSTER GROUP](#7335700144f62a07)
- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="ca28514ab71c220c"></a>
## ALTER CLUSTER LOCATION

<a id="1fd75a8e46cb879d"></a>
### Function

It alters a cluster location information.

<a id="9df5ad66e93b00d5"></a>
### Syntax

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="3bcb87f26b611bc6"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster location statement&gt;.

<a id="3d080d2f98484ded"></a>
### Syntax Rules and Parameters

<a id="f84a3fa3b2fd49ac"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should exist in the registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="e55ff57075660f6f"></a>
#### &lt;cluster connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST 'address' uses ip v4 type. 
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="6bcd5362e41c977f"></a>
### Description

If the connection information of the cluster location is altered, the cluster member does not need to be dropped or recreated, but the connection information can be altered by using [ALTER CLUSTER LOCATION](#ca28514ab71c220c).

<a id="daf29e80a20e7f14"></a>
### Examples

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="ec6eedc64eb4fb4e"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="c3203d37ee4d1761"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER LOCATION](#648735809e94071b)
- [DROP CLUSTER LOCATION](#7866e0152d6dec9e)

<a id="38b37f71079e8858"></a>
## ALTER DATABASE ADD LOGFILE

<a id="9fef18bb637a74f6"></a>
### Function

It adds log file groups or log file members to the database.

<a id="9b1227212e6f620e"></a>
### Syntax

```
<alter database add logfile statement> ::=
      <add logfile member statement> 
    | <add logfile group statement>
    ;

<add logfile member statement> ::=
    ALTER DATABASE ADD LOGFILE MEMBER <add logfile clause> [, ...] TO 
        <group clause>

<add logfile group statement> ::=
    ALTER DATABASE ADD LOGFILE <group clause> ( 'logfile_name' [, ...] ) 
        <size clause> [ REUSE ]

<group clause> ::=
    GROUP integer

<add logfile clause> ::=
    'logfile_name' [ REUSE ]

<size clause> ::=
    integer [ M | G ]
```

<a id="a0197462c7928ce2"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database add logfile statement&gt;.

<a id="593005b56568a964"></a>
### Syntax Rules and Parameters

<a id="5b551cf5e34a6f24"></a>
#### &lt;alter database add logfile statement&gt;

The database should be in MOUNT phase.

<a id="1a6d889902b88fb8"></a>
#### &lt;add logfile member statement&gt;

The log member is added to an existing log file group.

- &lt;add logfile clause&gt; 
    - 'logfile_name' is the file name of logfile member to be added to the log file group.
    - If the file does not exist, a new file is created.
    - The length of the logfile_name should be shorter than 1024 bytes.
- &lt;group clause&gt; 
    - It specifies the identifier of the logfile group to be added to the database.
    - Integer should be an identifier of the existing logfile group. 
    - If an identifier for the integer does not exist, an error occurs.

<a id="8cb13534c3dd3be4"></a>
#### &lt;add logfile group statement&gt;

It adds a new log file group.

- It is added as the next group of the CURRENT log file group.
- &lt;group clause&gt; 
    - It specifies the identifier of the logfile group to be added to the database.
    - Integer should be an identifier of the unexisting logfile group.
    - If an identifier for the integer exists, an error occurs.
- &lt;size clause&gt; 
    - The file size can be specified minimum of 10 MB to maximum of 10 GB.
    - The file size should be bigger than the sum of redo log buffer size and pending log buffer size.
- When logfile_name already exists, and the REUSE option is used, if the file size is as same as another group member, then the existing log file is reused.

<a id="e29c7c7b4e3349ad"></a>
### Description

It is recommended to back up the control file just in case for the file damage because the newly added log file groups and log members are stored in the control file.

<a id="49136cb4c8b32b3b"></a>
### Examples

The following is an example of adding two log file members to an existing log file group 3.

```
ALTER DATABASE ADD LOGFILE MEMBER 'logfile1.log', 'logfile2.log' TO GROUP 3;
```

The following is an example of adding a new log file group 4 to database. The size of log file group 4 is 100 M, and the log file name is 'logfile1.log'.

```
ALTER DATABASE ADD LOGFILE GROUP 4 ( 'logfile1.log' ) SIZE 100M;
```

> When adding a log group, a single log file should be used, and multiple log files can be added to an existing group as a member.

<a id="1a63f95329004e7e"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="61511f75f517252a"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE ADD LOGFILE](#38b37f71079e8858)
- [ALTER DATABASE DROP LOGFILE](#e2d7196e622dc75a)
- [ALTER DATABASE RENAME LOGFILE](#62e2fd8e2cb97810)

<a id="e208fd454f3edee3"></a>
## ALTER DATABASE ARCHIVELOG

<a id="4ec9efcca31305be"></a>
### Function

It alters an archive setting of the online log file in the database.

<a id="450bfa6435262403"></a>
### Syntax

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="de9e2d01f84f5b68"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database archivelog statement&gt;.

<a id="3e60115b4b849c50"></a>
### Syntax Rules and Parameters

<a id="8c5593530bee852a"></a>
#### &lt;alter database archivelog statement&gt;

- The database should be in MOUNT phase.
- ARCHIVELOG
    - It archives the online log file.
- NOARCHIVELOG
    - It does not archive the online log file.

<a id="6fe5a72c7fd3dad9"></a>
### Description

For the database backup and the media recovery using the backup, the system should be operated in ARCHIVELOG mode.

<a id="965e748d423fb6e4"></a>
### Example

The following is an example of how to set up a database to archive mode.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="794e49519575a665"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="4a857049b3ed7d78"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#8d346919c26ef35f)
- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)

<a id="8d346919c26ef35f"></a>
## ALTER DATABASE BACKUP

<a id="8db8ce7153220acb"></a>
### Function

The backup state is set to ACTIVE or INACTIVE to perform a full backup of the database. Then, the incremental database backup and control file backup are performed.

<a id="6b086f41712ba9ba"></a>
### Syntax

```
<alter database backup statement> ::=
      <database begin backup statement>
    | <database end backup statement>
    | <database incremental backup statement>
    | <database controlfile backup statement>
    ;

<database begin backup statement> ::=
    ALTER DATABASE BEGIN BACKUP [ AT <domain name> ]
    ;

<database end backup statement> ::=
    ALTER DATABASE END BACKUP [ AT <domain name> ]
    ;

<database incremental backup statement> ::=
    ALTER DATABASE BACKUP INCREMENTAL
        <incremental backup option> [ AT <domain name> ]    ;

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]

<database controlfile backup statement> ::=
    ALTER DATABASE BACKUP CONTROLFILE TO 'target_name'
        [ AT <domain name> ]    ;
```

<a id="7d65baeb69d3d1b3"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database backup statement&gt;.

<a id="a0fe24c40723d194"></a>
### Syntax Rules and Parameters

<a id="71add125f447bcd0"></a>
#### &lt;database begin backup clause&gt;

The database is set to the state which the full backup is available.

- All tablespaces in ONLINE state, which are created and used in the database, are set to the state of which the full backup is available. 
- The database should be OPEN state and operated in ARCHIVELOG mode.
- After starting BEGIN BACKUP, the following operations which require writing to the data file can not be performed.
    - SHUTDOWN NORMAL
    - OFFLINE / DROP TABLESPACE
    - ADD / DROP DATAFILE
- It may require media recovery on restart when a full backup is ACTIVE state and the instance is abnormally terminated.

<a id="3802d137bc8e9f8b"></a>
#### &lt;database end backup clause&gt;

The database is set to the state which the full backup is not available.

- All tablespaces in ONLINE state, which are created and used in the database, are set to the state which the full backup is not available. 
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

<a id="f6bbb06a1dc74c38"></a>
#### &lt;database incremental backup statement&gt;

- An incremental backup is performed for the database.
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

<a id="761df841446146a3"></a>
#### &lt;incremental backup option&gt;

- 'integer' can be specified from 0 to 4. 
- LEVEL 0 can not specify CUMULATIVE or DIFFERENTIAL.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n-1. 
    - DIFFERENTIAL
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n. 
    - If it is omitted, DIFFERENTIAL is specified by default.

<a id="ee504d736e30c201"></a>
#### &lt;database controlfile backup statement&gt;

- The control file is backed up. 
    - The length of 'target_name' should be shorter than 1024 bytes.
    - If 'target_name' already exists, the operation fails.
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

> The maximum length of the 'target_name' managed by GOLDILOCKS is 1024 bytes. However, the maximum lengths of the file name varies depending on the OS, so the actual length of 'target_name' which is available to be created can be shorter than 1024 bytes.

<a id="9e649de1dceba88f"></a>
#### &lt;domain name&gt;

- It is a name of a member or a group for which the statement is performed.
- If it is omitted, it is performed for all groups.

<a id="deba39931ca0e7f0"></a>
### Description

It backs up data files and control files in the database. A full backup of the database begins with BEGIN BACKUP, and copies the datafiles using OS file copy, then ends with END BACKUP. The incremental backup file is created in the path set by the BACKUP_DIR 1 property using a single statement.

<a id="2005ec9e8233f93f"></a>
### Examples

The following is an example of setting the entire backup state to ACTIVE.

```
ALTER SYSTEM BEGIN BACkUP;
```

The following is an example of setting the entire backup state to INACTIVE.

```
ALTER SYSTEM END BACkUP;
```

The following is an example to create the incremental backup of LEVEL 1 by using DIFFERENTIAL.

```
ALTER DATABASE BACKUP INCREMENTAL LEVEL 1 DIFFERENTIAL;
```

The following is an example to create the 'controlfile.bak' backup file for the control file. If the absolute path is not included, a backup file is created in the path set by the LOG_DIR property.

```
ALTER DATABASE BACKUP CONTROLFILE TO 'controlfile.bak';
```

<a id="83fef6c090edcfb0"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="dfd66bbe0151d233"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)
- [ALTER DATABASE RECOVER](#24aaa87abb398f65)

<a id="4bae50ba8bf61053"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="a6f25d5940fb7469"></a>
### Function

It purges audit records which are accumulated when applying an audit policy.

<a id="82315901dac8d7e9"></a>
### Syntax

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="053c86e59c5e72c0"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;clear audit trail statement&gt;.

<a id="4273130be9b60994"></a>
### Description

If an audit policy is activated, an audit trails is getting longer as time goes by.  
Tables configuring an audit trail are stored in MEM_AUX_TBS tablespace, and a user should be cautious not to let the audit trail keep increasing.

<a id="be330b289e55ee09"></a>
### Storing Audit Trail

A user should purge an audit trail after storing it according to the following procedure to store an audit trail when it is necessary.

- When performing it for the first time

```
CREATE TABLE backup_audit_trail AS SELECT * FROM AUDIT_TRAIL;
COMMIT;
```

- When repeatedly performing it

```
INSERT INTO backup_audit_trail SELECT * FROM AUDIT_TRAIL;
COMMIT;
```

- When purging an audit trail

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="bb19ede685ebbbc3"></a>
### Examples

Purge an audit trail by using the following statement.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="8b785ec3f7e7ac0d"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="f5c249bea04efc7f"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy 
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Enquiring audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Dropping audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="b1c83484159e9548"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="85d752d242561d68"></a>
### Function

It deletes the user's password change history which is accumulated due by applying the profile.

<a id="a3e70b08c50c799a"></a>
### Syntax

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="ad16ad098ca767e4"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;clear password history statement&gt;.

<a id="9f13cabb1e28cec0"></a>
### Description

When a profile is applied to a user, the user's password change history is accumulated according to the PASSWORD_REUSE_MAX and PASSWORD_REUSE_TIME policies.

**Managing the change history**

<a id="9918029bf55e886f"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | Managing the change history |
| --- | --- | --- |
| value | value | It manages only the change history within the value range, and the change history out of the value range is automatically deleted. |
| value | UNLIMITED | It accumulates all change history and it does not delete any change history because all change history should be checked. |
| UNLIMITED | value | It accumulates all change history and it does not delete any change history because all change history should be checked. |
| UNLIMITED | UNLIMITED | It does not manage the change history because the change history is not checked. |

&lt;Clear password history statement&gt; deletes the accumulated user's password change history.

<a id="31150c01d9ac32b2"></a>
### Examples

The following is an example of executing &lt;clear password history statement&gt; statement.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="ca735f0dbedb1420"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="7716b9f5f84c6b10"></a>
### For More Information

Refer to the followings.

- [CREATE PROFILE](#b8608593e7c730f3)
- [CREATE USER](#524780362f90ebc8)

<a id="822f8c4efbba0bdc"></a>
## ALTER DATABASE DELETE BACKUP

<a id="7e7be778847a5ce3"></a>
### Function

It deletes the backup file and the backup information of incremental backup. It can delete all incremental backup of the database or no longer usable obsolete backup.

<a id="fc89458e06bf0c52"></a>
### Syntax

```
<alter database delete backup statement> ::=
    ALTER DATABASE DELETE <delete backup list option> 
        BACKUP LIST [ <including backup file option> ]
    ;

<delete backup list option> ::=
      OBSOLETE
    | ALL

<including backup file option> ::=
    INCLUDING BACKUP FILES
```

<a id="2820ed519dfa5cdf"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database delete backup statement&gt;.

<a id="6b73a640531378b4"></a>
### Syntax Rules and Parameters

<a id="6d91ad246b25b35a"></a>
#### &lt;alter database delete backup statement&gt;

The database should be in MOUNT or OPEN phase.

<a id="59356fb95d1e8b3b"></a>
#### &lt;delete backup list option&gt;

It selects the backups to be deleted among the existing incremental backups.

- OBSOLETE: It selects backups of database or tablespaces to be deleted, which was backed up before the most recent database LEVEL 0 backup. 
- ALL: It selects all incremental backups to be deleted.

<a id="01b6ad5c05a8a6b5"></a>
#### &lt;including backup file option&gt;

- If it is omitted, it deletes only the backup information from the control file.
- It also deletes not only backup information but also the backup files.

<a id="986eb8569f6ca509"></a>
### Description

Deletion of the OBSOLETE incremental backup deletes the incremental backup of which is before the most recent LEVEL 0 database backup. When non-LEVEL 0 incremental backup is performed, it is not deleted even if it includes the previously performed incremental backup. It is because it can be used when performing the incomplete recovery by using the incremental backups.

> Be cautious of deleting the backup file together when an incremental backup is deleted. It can not be recovered even by using the control file which has incremental backup information.

<a id="03317a616905dd3f"></a>
### Example

The following is an example to delete the backup information and backup files of all existing incremental backups.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="399a04d762921fab"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="3153e1c534e86fb2"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)
- [ALTER DATABASE RECOVER](#24aaa87abb398f65)

<a id="e511a40b370e1420"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="ca233da0a7b45ba4"></a>
### Function

It drops the entire inactive cluster member.

<a id="fa502970cfe485c5"></a>
### Syntax

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS
    ;
```

<a id="cb89cb9eda98b68e"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database drop inactive cluster members statement&gt;.

<a id="702e45b871a67c00"></a>
### Description

It drops the entire inactive cluster member.

The inactive state of a cluster member means that it is not connected to the cluster system, and it occurs in the following cases.

- An error occurs on a cluster member in an operating cluster system.
- Trying to start-up the cluster system without driving the cluster member.

However, if the table shard is lost while dropping the cluster member, then an inactive cluster member can not be dropped.

It is recommended to use &lt;alter database drop inactive members statement&gt; when an inactive cluster member can not be included in the cluster system any more.

<a id="5a7727fe10460cee"></a>
### Examples

The following is an example of executing &lt;alter database drop inactive members statement&gt;.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="907c0cebf8d89eea"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="e2aa4ffe41290012"></a>
### For More Information

Refer to [ALTER SYSTEM JOIN DATABASE](#93365f06a2e0defc).

<a id="e2d7196e622dc75a"></a>
## ALTER DATABASE DROP LOGFILE

<a id="fb64ccf15f7f9574"></a>
### Function

It drops a log file group or a member which exists in the database.

<a id="94a3a05861235b90"></a>
### Syntax

```
<alter database drop logfile statement> ::=
      <drop logfile group statement>
    | <drop logfile member statement>
    ;

<drop logfile group statement> ::=
    ALTER DATABASE DROP LOGFILE <group clause>

<group clause> ::=
    GROUP integer

<drop logfile member statement> ::=
    ALTER DATABASE DROP LOGFILE MEMBER <logfile_list>

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="5a68e52389c66676"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database drop logfile statement&gt;.

<a id="ee5a227c9aaf448d"></a>
### Syntax Rules and Parameters

<a id="393552c291ffb213"></a>
#### &lt;alter database drop logfile statement&gt;

The database should be in MOUNT phase.  
An error occurs when the log file to be deleted is in CURRENT or ACTIVE stage.  
At least four log file groups should be remained after dropping.

<a id="28378c5820406107"></a>
#### &lt;drop logfile group statement&gt;

It drops the existing log file group.

- &lt;group clause&gt; 
    - It specifies the log file group to be dropped.
    - An integer should be an identifier of the existing log file.
    - An error occurs if the integer does not exist.

<a id="70918beefd65473d"></a>
#### &lt;drop logfile member statement&gt;

It drops the existing log file members.

- &lt;logfile_list&gt;
    - It is the list of the log file members to be dropped.
    - 'logfile_name' should be an existing name. 
    - An error occurs if 'logfile_name' does not exist.

<a id="47b42e5899ee9ffa"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="15aa86d5f0ad68cf"></a>
### Examples

The following is an example of dropping the existing log file GROUP 3.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

The following is an example of dropping logfile1.log and logfile2.log from the existing logfile GROUP 3.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="deba1cbb39985a2b"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="a8bbd62f574a146e"></a>
### For More Information

Refer to the respective syntax rules, and the followings.

- [ALTER DATABASE ADD LOGFILE](#38b37f71079e8858)
- [ALTER DATABASE RENAME LOGFILE](#62e2fd8e2cb97810)

<a id="5e14870d019b823b"></a>
## ALTER DATABASE MOVE SHARD

<a id="dcb8d5b81e1c6006"></a>
### Function

It rebalances shard of all tables in a specific cluster group to another cluster group.

<a id="c30171477811a142"></a>
### Syntax

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ];
```

<a id="0bca9de7e2b9ba3a"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database move shard statement&gt;.

<a id="5fb21e8676ee887b"></a>
### Syntax Rules and Parameters

<a id="60f6ad3506188df5"></a>
#### src_cluster_group

It is a cluster group to which the table shard is moved.

<a id="d390c9d208803c6d"></a>
#### dest_cluster_group

It is a target cluster group to which the table shard is moved.

<a id="c495aefd66b6bea4"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="0a8ee6b67f28e2c8"></a>
### Description

When adding a cluster member and a cluster group using the following statements, the table shard is not rebalanced.

- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0f86518c60487e59)

Perform &lt;alter database rebalance statement&gt; to rebalance the shard of the entire table which was not rebalanced when adding a cluster group and a cluster member.

&lt;alter database move shard statement&gt; is performed as the following concepts for tables which did not rebalance the shard.

```
ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
ALTER TABLE t2 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
ALTER TABLE t3 MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
...
...
ALTER TABLE t_n MOVE SHARD FROM CLUSTER GROUP src_group TO CLUSTER GROUP dest_group;
COMMIT;
```

The &lt;alter database move shard statement&gt; is proceeded even when the rebalancing the shard of a specific table fails. It does not rollback the table which succeeded in rebalancing the shard.

Therefore, when performing &lt;alter database move shard statement&gt; again after appropriately processed an error, then it rebalances only the shard for the table requiring the rebalancing. In this case, the table which succeeded in rebalancing the shard is not included in a target of the rebalancing.

<a id="7ab1819cd4e73a8a"></a>
### Examples

The following is an example of performing &lt;alter database move shard statement&gt;.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="9ffee095688a6dff"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="fa24406886148b7e"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name MOVE SHARD](#acf74aaf4961edaa)
- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0f86518c60487e59)

<a id="57c11d42fb324dc7"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="e2dad20b9593ea82"></a>
### Function

It sets the entire inactive cluster member to offline. In other words, it sets the shard map for the cluster member to offline.

<a id="925d4052e053644d"></a>
### Syntax

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="360f1f64d39846b0"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database offline inactive cluster members statement&gt;.

<a id="07d85bd3300e9344"></a>
### Syntax Rules and Parameters

It sets the entire inactive cluster member to offline.  
The inactive state of a cluster member means that it is not connected to the cluster system, and it occurs in the following cases.

- An error occurs on a cluster member in an operating cluster system.
- Trying to start-up the cluster system without driving the cluster member.

<a id="7704b27e1e4ac5c0"></a>
### Description

It is recommended to use &lt;alter database offline inactive members statement&gt; when an inactive cluster member can not be included in the cluster system any more.

If an inactive cluster member can participate in a cluster system, then perform [ALTER SYSTEM JOIN DATABASE](#93365f06a2e0defc) to include it in a cluster system.

The cluster member which is set to offline can be shifted to online again by using the following statements after the join.

- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="051baf419a0006bb"></a>
### Examples

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="78260447a3904eac"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="df8dd1140aefa0de"></a>
### For More Information

Refer to the followings.

- [ALTER SYSTEM JOIN DATABASE](#93365f06a2e0defc)
- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="6bf45492d225c752"></a>
## ALTER DATABASE REBALANCE

<a id="d11dbbed9afbf405"></a>
### Function

It rebalances shard of all tables.

<a id="a53bdfe478fe73db"></a>
### Syntax

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE [ ONLINE | OFFLINE ];
```

<a id="81546d26daa9c77b"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database rebalance statement&gt;.

<a id="36200f46e77ddb56"></a>
### Syntax Rules and Parameters

<a id="9ac1221e9ef58b6d"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="42ef71da0a8d3244"></a>
### Description

When adding a cluster member and a cluster group using the following statements, the table shard is not rebalanced.

- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0f86518c60487e59)

Perform &lt;alter database rebalance statement&gt; to rebalance the shard of the entire table which was not rebalanced when adding a cluster group and a cluster member.

&lt;alter database rebalance statement&gt; is performed as the following concepts for tables which did not rebalance the shard.

```
ALTER TABLE t1 REBALANCE;
COMMIT;
ALTER TABLE t2 REBALANCE;
COMMIT;
ALTER TABLE t3 REBALANCE;
COMMIT;
...
...
ALTER TABLE t_n REBALANCE;
COMMIT;
```

The &lt;alter database rebalance statement&gt; is proceeded even when the rebalancing the shard of a specific table fails. It does not rollback the table which succeeded in rebalancing the shard.

Therefore, when performing &lt;alter database rebalance statement&gt; again after appropriately processed an error, then it rebalances only the shard for the table requiring the rebalancing. In this case, the table which succeeded in rebalancing the shard is not included in a target of the rebalancing.

<a id="12d9427776fabe07"></a>
### Examples

The following is an example of performing &lt;alter database rebalance statement&gt;.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="198228a7e731a609"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="519906ae1e419eca"></a>
### For More Information

Refer to [ALTER TABLE name REBALANCE](#467720ee446849be).

<a id="d73ac151e73a973a"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="582f9718b8f20839"></a>
### Function

It rebalances shard of all tables excluding shards of a specific cluster group.

<a id="59422054f9edce43"></a>
### Syntax

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name [ ONLINE | OFFLINE ];
```

<a id="985a00f4426dfa68"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database rebalance exclude cluster group statement&gt;.

<a id="94aef435c9bab9d4"></a>
### Syntax Rules and Parameters

<a id="2eccd3d6d64fa90a"></a>
#### cluster_group_name

It is a name of the cluster group excluding a shard of the table.  
If the specified cluster group is the only cluster group, then the statement can not be performed.

<a id="ba8fefdcd7874f69"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="fca2f9923b5c9b1a"></a>
### Description

To drop a cluster group by using [DROP CLUSTER GROUP](#7335700144f62a07), there should not be a shard in the cluster group.

Perform &lt;alter database rebalance exclude cluster group statement&gt; to exclude a shard from the cluster group. &lt;alter database rebalance exclude cluster group statement&gt; is performed as the following concepts for tables which include a shard in the cluster group.

```
ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
ALTER TABLE t2 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
ALTER TABLE t3 REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
...
...
ALTER TABLE t_n REBALANCE EXCLUDE CLUSTER GROUP g3;
COMMIT;
```

If  the &lt;alter database rebalance exclude cluster group statement&gt; fails due to the lack of storage space, it does not rollback the table which succeed in excluding a shard.

Therefore, when performing &lt;alter database rebalance exclude cluster group statement&gt; again after appropriately processed an error, then it excludes and rebalances only the shard for the table requiring the rebalancing. In this case, the table which succeeded in excluding the shard is not included in a target of the rebalancing.

<a id="09ee7f5e32ff10e0"></a>
### Examples

The following is an example of performing &lt;alter database rebalance exclude cluster group statement&gt;.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="6352b05ccb8bc186"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="cc77fd1b640bfc4a"></a>
### For More Information

Refer to the followings.

- [DROP CLUSTER GROUP](#7335700144f62a07)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#7591488dbf1f1cba)

<a id="62e2fd8e2cb97810"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="7a63293bdd2938fa"></a>
### Function

It renames the logfile in the database.

<a id="21267d14552f544d"></a>
### Syntax

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="351c35884eb7c3fb"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required for performing &lt;alter database rename logfile statement&gt;.

<a id="340d71aea347a1d2"></a>
### Syntax Rules and Parameters

<a id="f9a3f0fb15e22355"></a>
#### &lt;alter database rename logfile statement&gt;

- The database should be in MOUNT phase. 
- FROM &lt;logfile_list&gt;
    - The name list of the logfiles to modify in the database.
- TO &lt;logfile_list&gt;
    - The name list of the logfiles to be modified in the database.
    - &lt;logfile_list&gt; should be an existing file.
    - An error occurs if the file does not exist.

<a id="300bbcae4391c739"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="e50e59ca807f7ce6"></a>
### Example

The following is an example of modifying the existing 'logfile.log' logfile to 'newlogfile.log'.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="32f079ebbff7cbd8"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="d5ec6021988ccf7b"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE ADD LOGFILE](#38b37f71079e8858)
- [ALTER DATABASE DROP LOGFILE](#e2d7196e622dc75a)

<a id="24aaa87abb398f65"></a>
## ALTER DATABASE RECOVER

<a id="f06c44fee34a237b"></a>
### Function

It recovers the entire data file or part of the data files in the database by using the online and archive log files.

<a id="8e4449c54f971d6f"></a>
### Syntax

```
<alter database recover statement> ::=
      <complete database recover statement>
    | <datafile recover statement>
    | <complete tablespace recover statement>
    | <incomplete database recover statement>
    ;

<complete database recover statement> ::=
    ALTER DATABASE RECOVER

<datafile recover statement> ::=
    ALTER DATABASE RECOVER DATAFILE <datafile recovery clause>

<datafile recovery clause> ::=
    <datafile recovery object> [, ...]

<datafile recovery object> ::=
    'datafile_name' [<recovery using backup option>] [recovery corruption option>]

<recovery using backup option> ::=
    USING BACKUP 'backup_datafile_name'

<recovery corruption option> ::=
    CORRUPTION

<complete tablespace recover statement> ::=
    ALTER DATABASE RECOVER TABLESPACE tablespace_name

<incomplete database recover statement> ::=
      <batch incomplete recovery statement>
    | <interactive incomplete recovery statement>
    ;

<batch incomplete recovery statement> ::=
    ALTER DATABASE RECOVER <until clause> [<using backup controlfile option>]
    
<until clause> ::=
      UNTIL CHANGE integer

<using backup controlfile option> ::=
    USING BACKUP CONTROLFILE

<interactive incomplete recovery statement> ::=
    ALTER DATABASE <incomplete recovery option> [<using backup controlfile option>]

<incomplete recovery option> ::=
      BEGIN INCOMPLETE RECOVERY
    | END INCOMPLETE RECOVERY
    | RECOVER 'logfile name'
    | RECOVER AUTOMATICALLY
    | RECOVER SUGGESTION
    ;
```

<a id="1fcbb5c65f82af96"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database recover statement&gt;.

<a id="b706b98156827fde"></a>
### Syntax Rules and Parameters

<a id="37957de16c27de69"></a>
#### &lt;complete database recover statement&gt;

The data files of the database are recovered up to date by using the online and archive log files.

- The recovery is performed for all tablespaces in the ONLINE state.
- The database should be in MOUNT phase and in ARCHIVELOG mode. 
- If the required archived log file does not exist, it fails.

<a id="bbb77f30a95d3426"></a>
#### &lt;datafile recover statement&gt;

It recovers the backuped datafile, the datafile of the tablespace which requires the recovery by using the archive logfile due to an error during the backup, or the datafile of the tablespace which was set to offline by an immediate option, to the latest status.

- Datafile can be recovered on MOUNT phase or OPEN phase.
- The datafile of the tablespace which is in OFFLINE state can be recovered on OPEN phase, and datafile which is either in ONLINE/OFFLINE state can be recovered in MOUNT phase.
- If the required archive logfile does not exist, then the recovery fails.
- &lt;datafile recovery clause&gt;
    - It specifies one or more datafile object list which is a target of the recovery.
- &lt;datafile recovery object&gt;
    - It sets the name of datafile which is a target of the recovery, and the recovery option.
- &lt;recovery using backup option&gt;
    - It sets the name of backup datafile of the datafile which is a target of the recovery.
- &lt;recovery corruption option&gt;
    - It determines whether to recover only the pages corrupted from the datafile which is a target of the recovery.

<a id="1a697aee6d0b14b7"></a>
#### &lt;complete tablespace recover statement&gt;

The data files of the tablespace is recovered up to date.

- Tablespace recovery should be performed when the database is in MOUNT or OPEN phase. 
- The recovery in the OPEN phase can only be performed when the tablespaces is in the OFFLINE stage, and the recovery in MOUNT phase can be performed when the tablespace is either in ONLINE/ OFFLINE stage. 
- If the required archive log file does not exist, it fails.
- The following is the case which requires the tablespace recovery operation.
    - The tablespace became OFFLINE by IMMEDIATE. 
    - The backed up data file is used.
    - A failure occurred during the entire backup.

<a id="7ca4b830e330f3ac"></a>
#### &lt;incomplete database recover statement&gt;

<a id="f0b2cab99f62cfb2"></a>
##### &lt;batch incomplete database recover statement&gt;

The datafiles in the database are recovered in a batch up to a specific point of time by using the online and archive logfile.

- The recovery is performed for all tablespaces in the ONLINE stage.
- The database should be in MOUNT phase and in ARCHIVELOG mode.
- It fails if using the data file containing data which is after the time of the incomplete recovery.
- The database should be OPEN by using RESETLOGS after completion of incomplete recovery.
- &lt;until clause&gt; 
    - A specific point of time for incomplete recovery
    - UNTIL CHANGE: The point of time is specified for incomplete recovery in log units
- &lt;using backup controlfile&gt; 
    - Deprecated

<a id="e9b97bcaf630c715"></a>
##### &lt;interactive incomplete database recover statement&gt;

The data files in the database are interactively recovered with a user up to a specific point of time by using online and archive log file.

- The recovery is performed for all tablespaces in the ONLINE stage.
- The database should be in MOUNT phase and in ARCHIVELOG mode.
- It fails if using the data file containing data which is after the time of the incomplete recovery.
- The database should be OPEN by using RESETLOGS after completion of incomplete recovery.
- &lt;incomplete recovery option&gt;
    - It is an option to perform an interactive incomplete recovery in log units.
    - BEGIN INCOMPLETE RECOVERY: It starts an incomplete recovery. 
    - END INCOMPLETE RECOVERY: It ends an incomplete recovery. 
    - RECOVER 'logfile name': A user directly specifies the log file performing the recovery. 
    - RECOVER AUTOMATICALLY: All recoverable archive log files are recovered. 
    - RECOVER SUGGESTION: It recovers archive log files which are required for the recovery and recommended by the system.
- &lt;using backup controlfile&gt;
    - Deprecated.

<a id="c5ca2f8c1788cc81"></a>
### Description

Incomplete recovery of the database is not easy to find a recovery completion point at a time. Therefore, the desired recovery point is found by performing it several times.  
However, it becomes a new database if the database is started up with RESETLOGS option after an incomplete recovery. Therefore, the incomplete recovery should be performed several times after creating a copy of the archived log files and online redo log files.

<a id="b0cbd3d7e1ec663b"></a>
### Examples

The following is an example of a complete recovery for entire database.

```
ALTER DATABASE RECOVER;
```

The following is an example of a datafile recovery.

```
ALTER DATABASE RECOVER DATAFILE 'test.dbf';
```

The following is an example of a tablespace recovery.

```
ALTER DATABASE RECOVER TABLESPACE test_tbs;
```

The following is an example of incomplete recovery for the entire database until LSN is 11123.

```
ALTER DATABASE RECOVER UNTIL CHANGE 11123;
```

The following is an example of interactive incomplete recovery until the recoverable archive log files.

```
ALTER DATABASE BEGIN INCOMPLETE RECOVERY;
ALTER DATABASE RECOVER AUTOMATICALLY;
ALTER DATABASE END INCOMPLETE RECOVERY;
```

<a id="534e3beee79bb701"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="79750cf7126193f3"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#8d346919c26ef35f)
- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#e5a37a0f857e01cd)

<a id="5dfb401870695b11"></a>
## ALTER DATABASE REGISTER

<a id="8176d8774c600476"></a>
### Function

It registers unrecoverable segments in the database.

<a id="e97e43290a1200f4"></a>
### Syntax

```
<alter database register statement> ::=
    ALTER DATABASE REGISTER IRRECOVERALBE SEGMENT 
        <segment physical identifier list>
    ;

<segment physical identifier list> ::=
      integer
    | <segment physical identifier list> , integer
```

<a id="2c5ed15efbdcba7f"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database register statement&gt;.

<a id="a97beba864651dc0"></a>
### Syntax Rules and Parameters

<a id="871137afe5032369"></a>
#### &lt;alter database register statement&gt;

It registers the unrecoverable segments in the database. The statement can be used on the assumption that the segment is not used any more, when the database is not recoverable and the backup does not exist.

- The database should be in MOUNT phase. 
- The registered segment identifier list is initialized at restart.
- If a server restart is successful, the registered segment becomes 'UNUSABLE' state, and that segments should be deleted.

<a id="09c951f21ceca9f9"></a>
#### &lt;segment physical identifier list&gt;

The list of unrecoverable segment identifier  
• Integer: 8 bytes integer segment identifier

<a id="cb0a14fa61b57682"></a>
### Description

When a server restarts after abnormal termination, the database performs the recovery process. During this process, it executes pages again by using the REDO log to recover pages which was not reflected in the disk in the previous service stage.

If an unexpected failure occurs during execution of the REDO operation, that statement can be used to ignore the failure and to execute the recovery.

<a id="867297f343f953a0"></a>
### Example

The following is an example of giving up the recovery of the segment whose identifier is 4028679323648.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="900b03c80a2dac37"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="9873370c4eb3b51f"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)
- [ALTER DATABASE RECOVER](#24aaa87abb398f65)

<a id="dc9924209ee5d22d"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="444e7b35df56e847"></a>
### Function

It resets the local cluster member except for the tablespace object to the time of creating the database.

<a id="6c7d57d9a686517a"></a>
### Syntax

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="059e6d3d1a97e7e3"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

The start-up phase should be LOCAL OPEN.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database reset local cluster member statement&gt;.

<a id="8c1a437ce29b6c8d"></a>
### Description

It resets the local cluster member except for the tablespace object to the time of creating the database. It drops all objects created by a user except for the tablespace object.

&lt;alter database reset local cluster member statement&gt; statement resets an inactive cluster member, and makes the new cluster member to participate in a cluster system.  
An inactive cluster member which is disconnected from the cluster system is processed as follows.

- If it can join in a cluster system again, then use JOIN statement to make it join. 
    - [ALTER SYSTEM JOIN DATABASE](#93365f06a2e0defc)
- If it can not join in a cluster system again, then use DROP statement to exclude it. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#e511a40b370e1420)

In this case, the device corresponding to the cluster member which is excluded from a cluster system can be used again by using the following two methods.

- Method 1: Recreate the database of the local cluster member. 
- Method 2: Reset the local cluster member by using &lt;alter database reset local cluster member statement&gt;.

The method 2 reduces the cost of recreating the tablespace comparing to the method 1.

<a id="ee577230a3fbd14d"></a>
### Examples

The following is an example of a reset by using &lt;alter database reset local cluster member statement&gt; after driving the local cluster member, which is excluded from the cluster system, up to LOCAL OPEN phase.

```
gSQL> \startup nomount

Startup success


gSQL> ALTER SYSTEM MOUNT DATABASE;

System altered.


gSQL> ALTER SYSTEM OPEN LOCAL DATABASE;

System altered.

gSQL> ALTER DATABASE RESET LOCAL CLUSTER MEMBER;

Database altered.
```

<a id="d1c5af30ee874d02"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="222d7776ac158fa1"></a>
### For More Information

Refer to the followings.

- [ALTER SYSTEM JOIN DATABASE](#93365f06a2e0defc)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#e511a40b370e1420)

<a id="70b329814c7e841f"></a>
## ALTER DATABASE RESTORE

<a id="b8029215edff5379"></a>
### Function

It restores the data files in the database or tablespace by using the incremental backup.

<a id="b7293333c749d861"></a>
### Syntax

```
<alter database restore statement> ::=
      <database restore statement>
    | <tablespace restore statement>
    | <controlfile restore statement>
    ;

<database restore statement> ::=
    ALTER DATABASE RESTORE [ <until clause> ]

<until clause> ::=
    UNTIL CHANGE integer

<tablespace restore statement> ::=
    ALTER DATABASE RESTORE TABLESPACE tablespace_name

<controlfile restore statement> ::=
    ALTER DATABASE RESTORE CONTROLFILE FROM 'file_name'
```

<a id="78ffcaa2d6a79095"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database restore statement&gt;.

<a id="9a8cb9316b6b6eb2"></a>
### Syntax Rules and Parameters

<a id="720b5bfc2774da00"></a>
#### &lt;database restore statement&gt;

It restores the data files in the database by using the incremental backup.   
The database should be in MOUNT phase.

<a id="4675ada7edab2325"></a>
#### &lt;tablespace restore statement&gt;

It restores the data files in the tablespace by using the incremental backup.

- The database should be in MOUNT or OPEN phase.
- The recovery in OPEN state can be performed only for the tablespaces in OFFLINE state. The recovery in MOUNT phase can be performed for the tablespace is either in ONLINE state or OFFLINE state.

<a id="5bda7aca2e24ab5c"></a>
#### &lt;controlfile restore statement&gt;

The control file is recovered using 'file_name'.

- The database should be in NOMOUNT phase.
- The absolute path is recommended for 'file_name' but if relative path is described, then &lt;GOLDILOCKS_HOME&gt;/wal/'file_name' is used.

<a id="4254b0648db62512"></a>
### Description

The data recovery using full backup uses OS copy command to directly copy the backup file to the data file path. The data recovery using incremental backup restores only the deleted data files or old data files.

<a id="daa8e8affae0299b"></a>
### Examples

The following is an example of recovering the database by using the incremental backup.

```
ALTER DATABASE RESTORE;
```

The following is an example of recovering the tablespace by using the incremental backup.

```
ALTER DATABASE RESTORE TABLESPACE test_tbs;
```

The following is an example of recovering the database by using only the incremental backup whose LSN is smaller than 11123.

```
ALTER DATABASE RESTORE UNTIL CHANGE 11123;
```

The following is an example of recovering the control file by using controlfile.bak.

```
ALTER DATABASE RESTORE CONTROLFILE FROM 'controlfile.bak'
```

<a id="85c352a6d72552de"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="7b53255598362a99"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#8d346919c26ef35f)
- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)
- [ALTER DATABASE RECOVER](#24aaa87abb398f65)

<a id="1bdd55fdd17ecc95"></a>
## ALTER INDEX

<a id="9a5ddf9d3375c14c"></a>
### Function

It alters the index definition.

<a id="4a542bd14b1b7faa"></a>
### Syntax

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    ;
```

<a id="8f6f38a8cfd377a5"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="06761b2f98432514"></a>
### Syntax Rules and Parameters

<a id="a38da94f1044d2c6"></a>
#### &lt;alter index physical attribute statement&gt;

It alters physical attributes of the index.  
For more information, refer to [ALTER INDEX name STORAGE](#f11f2cc5c5cc3859).

<a id="3390275a51474836"></a>
#### &lt;rename index statement&gt;

It alters the index name.  
For more information, refer to [ALTER INDEX name RENAME TO](#1c016a1f45a446bc).

<a id="71eea8ffeaa0aa5e"></a>
#### &lt;aging statement&gt;

It deletes the empty page of the index.  
For more information, refer to [ALTER INDEX name AGING](#90501d78604fb0db).

<a id="aae7762eea88ae8c"></a>
### Description

Refer to the descriptions of each detailed statement.

<a id="732e3f926d6de9f2"></a>
### Examples

Refer to the examples of each detailed statement.

<a id="5fc87269bb8c121b"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="90501d78604fb0db"></a>
## ALTER INDEX name AGING

<a id="6ce881d870fe4436"></a>
### Function

It deletes an empty page of the index.

<a id="cbf570a5e73f3943"></a>
### Syntax

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="8dc002ee649a6769"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;aging index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="85b5c2bd8f924095"></a>
### Syntax Rules and Parameters

<a id="f70bb5a806566339"></a>
#### index_name

It is the name of the target index.

<a id="fac73d5ec9535b46"></a>
### Description

This syntax returns pages whose all keys are deleted among index pages to a segment. Aging is processed in two steps which are logical deletion and physical deletion. A logical deletion is disconnection of index page, and it is performed when SCN of when deleting the last key of a page is smaller than the agable SCN of the system. Then the physical deletion is performed when the SCN of the logical deletion is smaller then the agable SCN of the system.

> If the agable SCN of the system does not increase, then the empty page may not be deleted even though the index AGING statement succeeded.

<a id="a64622f89f2a4217"></a>
### Examples

The following is an example of aging the index.

```
gSQL> select index_name, empty_blocks from user_indexes where index_name = 'T1X';

INDEX_NAME EMPTY_BLOCKS
---------- ------------
T1X                   2

1 row selected.

gSQL> alter index t1x aging;

Index altered.

gSQL> select index_name, empty_blocks from user_indexes where index_name = 'T1X';

INDEX_NAME EMPTY_BLOCKS
---------- ------------
T1X                   0

1 row selected.
```

<a id="b70db6239e532e03"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="9d40a45e7f1a33b7"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](#11cedda99c2339bc)
- [ALTER INDEX](#1bdd55fdd17ecc95)
- [DROP INDEX](#9fbe418d2e4cd17c)

<a id="f11f2cc5c5cc3859"></a>
## ALTER INDEX name STORAGE

<a id="395ddd4354bbc7cb"></a>
### Function

It alters the physical attributes of the index.

<a id="0684c303f7fcb7b0"></a>
### Syntax

```
<alter index physical attribute statement> ::=
    ALTER INDEX index_name
    | <physical attribute clause>
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

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
```

<a id="ec53ad4a9e99c2ff"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter index physical attribute statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="0040be896e1240d7"></a>
### Syntax Rules and Parameters

<a id="59520e039930df91"></a>
#### index_name

It is the target index name.

<a id="e8eec3d2124fbb86"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of the index.

- PCTFREE integer 
    - Definition 
        - The reserved space to adjust the frequency of page splits caused by inserting the key in the page.
        - It is applied only when the index bottom-up build.
    - It can use of the value from 0 to 99.
    - If it is omitted, the value set in DEFAULT_INDEX_PCTFREE property is used by default.

- INITRANS integer 
    - Definition 
        - The initial number of transactions simultaneously accessing the page.
        - If the number of users accessing the index is small, then INITRANS is set low. If the number of users simultaneously accessing the index is big, then INITRANS is set high.
        - If necessary, it is automatically increased to the specified MAXTRANS.
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions simultaneously accessing the page.
    - It can use the value from 1 to 32. 
    - If it is omitted, the default value is 8.

<a id="efdbff9aa8cbe5b1"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of physical storage space which is initially allocated when creating the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually operated as 8192 bytes.)
        - The size (aligned to the EXTENT size of TABLESPACE) should be equal to or bigger than MINEXTENTS, or it should be equal to or less than MAXEXTENTS.
        - It is applied only when the index bottom-up build.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is omitted, the default value is one EXTENT size of TABLESPACE to which the table belongs.

- NEXT integer
    - Definition
        - It specifies the physical space size to be allocated when adding the space to the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually operated as 8192 bytes.)
        - NEXT operates as follows depending on the remaining space size of the currently available index. (Obtained by subtracting the amount of currently used space from the MAXEXTENTS size)  
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
    - If it is omitted, the default value is EXTENT size * 2147483647(The maximum positive integer of INT32).

<a id="83e74863bfb1463b"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="991584921d9ed638"></a>
### Description

Refer to the syntax rules of each statement.

<a id="ff1916a45620e54e"></a>
### Examples

The following is an example of altering the physical attributes of the index.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="b46286d337e51d30"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="ae789a926382815c"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](#11cedda99c2339bc)
- [ALTER INDEX](#1bdd55fdd17ecc95)
- [DROP INDEX](#9fbe418d2e4cd17c)

<a id="1c016a1f45a446bc"></a>
## ALTER INDEX name RENAME TO

<a id="a842e1029c60d081"></a>
### Function

It alters the index name.

<a id="ddde54241cc68788"></a>
### Syntax

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="cf6cd0db49e2ac79"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="5078b83e5312f1f6"></a>
### Syntax Rules and Parameters

<a id="176de506a08df44e"></a>
#### index_name

It is the name of the target index.  
The schema name can not be described and it has the same schema name as same as that of the existing index.

<a id="bdcc6976d366ebfd"></a>
#### new_index_name

It is the name of the new index, and it should be a unique index name within the schema.

<a id="f00c62a654c1941d"></a>
### Description

Refer to the syntax rules of each statement.

<a id="be646243fcecc9f2"></a>
### Examples

The following is an example of altering the index name.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="f55f4e1c7a20a311"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="d5a243f6a9e46424"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](#11cedda99c2339bc)
- [ALTER INDEX](#1bdd55fdd17ecc95)
- [DROP INDEX](#9fbe418d2e4cd17c)

<a id="da7815275847e190"></a>
## ALTER PROFILE

<a id="33a7d6c9d3080c3d"></a>
### Function

It alters the password management method.

<a id="ab1b7bfafb739275"></a>
### Syntax

```
<alter profile statement> ::= 
    ALTER PROFILE profile_name LIMIT 
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

<a id="237bafbb63426e36"></a>
### Invocation and Access Rules

ALTER PROFILE ON DATABASE privilege is required to perform &lt;alter profile statement&gt;.

<a id="5acb1a2acb7f95a2"></a>
### Syntax Rules and Parameters

<a id="8ceb2b2931548ad2"></a>
#### profile_name

It is a profile name to be altered.

<a id="b91c5cfb0a770687"></a>
#### FAILED_LOGIN_ATTEMPTS

It sets the number of consecutive login attempts allowed to fail.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="57403f1663aa1e4b"></a>
#### PASSWORD_LOCK_TIME

It sets an account lockout duration (day) after the consecutive login failures.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="12fb6a1ea7516060"></a>
#### PASSWORD_LIFE_TIME

It sets the password lifetime (day).  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="2dfb6d82cb06877f"></a>
#### PASSWORD_GRACE_TIME

It sets a password expiration grace period when log in after PASSWORD_LIFE_TIME.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="c510e368658aca7c"></a>
#### PASSWORD_REUSE_MAX

It specifies the number of the recent passwords which can not be reused when a user wants to reuse the old password.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="d7210eb2ecd3ac91"></a>
#### PASSWORD_REUSE_TIME

It specifies the duration which the password can not be reused when a user wants to reuse the old password.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="3fca7c7dcd82b371"></a>
#### PASSWORD_VERIFY_FUNCTION

It sets the password complexity verification method.  
For more information, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="412df008e88f0129"></a>
### Examples

The following is an example of changing the profile to control the account lockout.

```
gSQL> ALTER PROFILE prof1 LIMIT
        FAILED_LOGIN_ATTEMPTS 3
        PASSWORD_LOCK_TIME 3;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of changing the profile to control the password lifetime.

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_LIFE_TIME 90 
        PASSWORD_GRACE_TIME 7;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of changing the profile to control the password reusability.

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_REUSE_MAX  DEFAULT
        PASSWORD_REUSE_TIME DEFAULT;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of changing the profile to control the password complexity verification.

```
gSQL> ALTER PROFILE prof1 LIMIT
        PASSWORD_VERIFY_FUNCTION KISA_VERIFY_FUNCTION;

Profile altered.

gSQL> COMMIT;

Commit complete.
```

<a id="d76acc9801cb2930"></a>
### Compatibility

The SQL standard does not define the concepts of the profile.

<a id="99b2be9a4335ee9f"></a>
### For More Information

Refer to [DROP PROFILE](#a176f22a83621a33).

<a id="b01c09c114935817"></a>
## ALTER SEQUENCE

<a id="29df24f5d4331271"></a>
### Function

It alters the sequence.

<a id="4ccaa5ab45a69c3a"></a>
### Syntax

```
<alter sequence generator statement> ::=
    ALTER SEQUENCE sequence_name <alter sequence generator options>
    ;

<alter sequence generator options> ::=
    <alter sequence generator option> [, ...]

<alter sequence generator option> ::=
      <alter sequence generator restart option>
    | <basic sequence generator option>

<alter sequence generator restart option> ::=
    RESTART [ WITH integer ]

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

<a id="de38364bf425e7e2"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter sequence generator statement&gt;.

- The owner of that sequence 
- (ALTER SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence belongs
- ALTER ANY SEQUENCE ON DATABASE

<a id="0843bdfee418edef"></a>
### Syntax Rules and Parameters

<a id="1b59593294aa6ca2"></a>
#### sequence_name

It is the sequence name to be altered.  
It can define schema to which the sequence belongs such as schema_name.sequence_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="7b8bfdf2eb1e8261"></a>
#### &lt;alter sequence generator restart option&gt;

It sets NEXT VALUE of the sequence.  
However, it does not change the value of START WITH which is defined in [CREATE SEQUENCE](#f57ec80975339322) statement.

- RESTART 
    - If the value is not specified, the value of START WITH defined in &lt;sequence generator definition&gt; is set as the next value of the sequence.
- RESTART WITH integer 
    - It sets an integer value as the next value of the sequence.
    - The integer value should be between MINVALUE and MAXVALUE.

If &lt;alter sequence generator restart option&gt; clause is not specified, it changes the sequence attributes based on the current sequence value.

<a id="8d09adc66b513aa1"></a>
#### &lt;sequence generator increment by option&gt;

It changes the interval of the sequence number.  
The constraints and characteristics are as follows.

- A positive or negative value can be used, but 0 can not be used.
- The absolute value of the interval should be smaller than the difference between MINVALUE and MAXVALUE.
- If it is a positive value, it an ascending sequence. If it is a negative value, it is a descending sequence.

<a id="30e2ec799baa193f"></a>
#### &lt;sequence generator maxvalue option&gt;

It changes the maximum value which the sequence can generate.  
However, the MAXVALUE should not be smaller than the current sequence value.

- MAXVALUE integer 
    - The maximum value is in the range between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of 64 bit integer.
    - It should be equal to or bigger than the value of START WITH, and bigger than the value of MINVALUE.
- NO MAXVALUE | NOMAXVALUE 
    - It changes the maximum value as follows.
        - If it is an ascending sequence, it is the maximum value (+9,223,372,036,854,775,807) of the 64 bit integer.
        - If it is a descending sequence, the value is -1.
        - NO MAXVALUE (SQL standard) and NOMAXVALUE are the reserved words with the same meaning, and either of them can be used.

<a id="5736f5043e107760"></a>
#### &lt;sequence generator minvalue option&gt;

It changes the minimum value which the sequence can generate.  
However, the MINVALUE should not be bigger than the current sequence value.

- MINVALUE integer 
    - The minimum value is in the range between the minimum (-9,223,372,036,854,775,808) and the maximum (+9,223,372,036,854,775,807) of 64bit integer.
    - It should be equal to or smaller than the value of START WITH, and smaller than the value of MAXVALUE.
- NO MINVALUE | NOMINVALUE 
    - It changes the minimum value as follows.
        - If it is an ascending sequence, the value is 1.
        - If it is a descending sequence, it is the minimum value (−9,223,372,036,854,775,808) of the 64bit integer.
    - NO MINVALUE (SQL standard) and NOMINVALUE are the reserved words with the same meaning, and either of them can be used.

<a id="181d6beb744dba4a"></a>
#### &lt;sequence generator cycle option&gt;

It changes whether to continue generating a value when the sequence value becomes the maximum or minimum value.

- CYCLE 
    - If an ascending sequence becomes the maximum value, it generates the value again from the minimum value.
    - If a descending sequence becomes the minimum value, it generates the value again from the maximum value.
- NO CYCLE | NOCYCLE 
    - It can not generate the value sequence when it becomes the maximum value or the minimum value.
    - NO CYCLE (SQL standard) and NOCYCLE are the reserved words with the same meaning, and either of them can be used.

<a id="5fd456d05ba6baba"></a>
#### &lt;sequence generator cache option&gt;

For quick access of a sequence, it defines the number of sequence values to be pre-loaded on the memory.  
When restarting the database, the sequence value loaded on the memory is lost, and it starts from the value after loading.

- CACHE integer 
    - The CACHE value should be equal to or bigger than 2.
    - If CYCLE exists, the CACHE value should not be bigger than the length of CYCLE.
        - The length of CYCLE: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - It does not pre-load the sequence value in memory.

<a id="a3e55a534318a401"></a>
### Description

It can not change START WITH which is one of the sequence attributes defined in [CREATE SEQUENCE](#f57ec80975339322) statement. To change START WITH attribute, it should be re-created by performing [CREATE SEQUENCE](#f57ec80975339322) statement after performing [DROP SEQUENCE](#98127fac6b27272b) statement.

<a id="f269e8e72332ac5a"></a>
### Examples

The following is an example of restating the sequence value by using RESTART option, then assigning a new ID.

```
gSQL> SELECT id, name FROM t1 ORDER BY 1;

 ID NAME  
--- ------
 10 leekmo
 42 mkkim 
 51 jhkim 
172 ehpark

4 rows selected.


gSQL> ALTER SEQUENCE seq1 RESTART;

Sequence altered.


gSQL> UPDATE t1 SET id = seq1.NEXTVAL;

4 rows updated.


gSQL> SELECT id, name FROM t1 ORDER BY 1;

ID NAME  
-- ------
 1 leekmo
 2 mkkim 
 3 jhkim 
 4 ehpark

4 rows selected.
```

<a id="f242831bc6b80d1c"></a>
### Compatibility

The SQL standard does not define CACHE/ NO CACHE statement.

**SQL standard compatibility**

<a id="db7ba1aa150d2a72"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="efeb8f75ea26743d"></a>
### For More Information

Refer to the followings.

- [CREATE SEQUENCE](#f57ec80975339322)
- [DROP SEQUENCE](#98127fac6b27272b)

<a id="71b5ddbfb9400441"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="5e70cdecb79bff5d"></a>
### Function

It returns all segments which were caught to be reused in a session to tablespaces.

<a id="37d5ecfdf1bbfa15"></a>
### Syntax

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="a1fddcfc2baed7ac"></a>
### Description

It cleans up only the segments of a segment cache in the performed session.

<a id="49205336567b30d2"></a>
### Examples

The following is an example of cleaning up the segment cache of the session.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="37e4bc0af7489c3b"></a>
### Compatibility

The SQL standard does not define the concepts of the segment cache of a global temporary table and a global temporary index.

<a id="629bb41db9c4ccc9"></a>
### For More Information

Refer to [Global Temporary Table](13-sql-objects.md#d74235a3a28eef92).

<a id="c7a0e93656726619"></a>
## ALTER SESSION SET property_name

<a id="7637d3fa1d9c0c64"></a>
### Function

It sets the property value of the session.

<a id="269355d415a27989"></a>
### Syntax

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="d2781ab3efa38060"></a>
### Syntax Rules and Parameters

<a id="01c549d132c5878c"></a>
#### &lt;property name&gt;

It is the property name to be set.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#6c2d42da1f4f968c) in an administration manual.

<a id="f8f1efb59c660c4a"></a>
#### &lt;property value&gt;

It is the property value to be set.

<a id="eb0f15653c399876"></a>
#### TO DEFAULT

It sets the session property value as a system property value.

<a id="7117089c862d9fd0"></a>
### Description

For more information about property, refer to [Server Property](../part-02-administration-manual/10-server-property.md#6c2d42da1f4f968c) in an administration manual.

<a id="8e84ac25e4a0cd04"></a>
### Examples

The following is an example of an error when setting ERROR HINT property so the hint clause includes an error.

```
gSQL> ALTER SESSION SET HINT_ERROR = ON;

Session altered.

gSQL> SELECT /*+ INDEX( t1, invalid_index ) */ name FROM t1 WHERE id = 1;

ERR-42000(16058): not applicable hint : 
SELECT /*+ INDEX( t1, invalid_index ) */ name FROM t1 WHERE id = 1
           *
ERROR at line 1:
```

The following is an example of setting the session property value as the system property value.

```
gSQL> ALTER SESSION SET HINT_ERROR TO DEFAULT;

Session altered.
```

<a id="4b4e6d5359820046"></a>
### Compatibility

The SQL standard does not define the concepts of the session property.

<a id="53e520bc49562300"></a>
### For More Information

Refer to [ALTER SESSION SET property_name](#c7a0e93656726619).

<a id="19612bdf5baa61ea"></a>
## ALTER SYSTEM CHECKPOINT

<a id="471789498aa7d321"></a>
### Function

It performs CHECKPOINT.

<a id="238fb068c9793acf"></a>
### Syntax

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="5cad76a49a862309"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system checkpoint statement&gt;.

<a id="d7814ab2ea926ba7"></a>
### Syntax Rules and Parameters

<a id="5a106bbf2a446a95"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT is an operation to ensure that all altered data by the committed transactions are written to disk.

- The database should be in OPEN phase. 
- The database should be in TDS mode.
- When a full backup is in progress, the altered pages are not recorded in the data file, but only the REDO logs and control files are written to the disk. If the server is abnormally terminated in this situation, a media recovery should be performed.

<a id="63a6501d217dfdb7"></a>
#### &lt;domain name&gt;

- It is a name of a member or a group for which the statement is performed.
- If it is omitted, it is performed for all groups.

<a id="06da572dd8c78aef"></a>
### Description

The checkpoint operation records all changes by the committed transactions to disk, so it enables a rapid recovery at system error.

<a id="1fd5105056be6f32"></a>
### Example

The following is an example of performing CHECKPOINT.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="a03551ee4f036482"></a>
### Compatibility

The SQL standard does not define the concepts of CHECKPOINT.

<a id="12d5fa59477220e9"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="9aa3a09a882c57ea"></a>
### Function

It cleans up all SQL plans.

<a id="fb4218bd8d01563d"></a>
### Syntax

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="6ca6861792ee2a37"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system cleanup plan statement&gt;.

<a id="d0dc473aab428e26"></a>
### Syntax Rules and Parameters

<a id="767d379d39e79301"></a>
#### &lt;alter system cleanup plan statement&gt;

There is not any syntax rules or parameters for &lt;alter system cleanup plan statement&gt;.

<a id="10ff7cc79539eb31"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="f70204a2034086df"></a>
### Description

It cleans up all of the cached SQL plan. However, the plan whose V$SQL CACHE.REF COUNT is bigger than 0 (the plan referenced by the prepared statement) is excluded from cleanup.

<a id="53a358db42ba05e8"></a>
### Examples

The following is an example of executing CLEANUP PLAN.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="7fb62cbf36cc9cb1"></a>
### Compatibility

The SQL standard does not define the concepts of CLEANUP PLAN.

<a id="9f9987d2e2ba0d12"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="89fd3d94c963a24b"></a>
### Function

It specifies an irrecoverable cluster member.

<a id="57227504b56d937e"></a>
### Syntax

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="e35a6a0c42b0b7f1"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system irrecoverable cluster member statement&gt;.

<a id="0e7d5fc5d3610a79"></a>
### Syntax Rules and Parameters

<a id="3b614b8651d84230"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

There is not any syntax rules or parameters for &lt;alter system irrecoverable cluster member statement&gt;.

<a id="910558349221bd88"></a>
#### &lt;domain name&gt;

It is a name of an irrecoverable member.   
It is not allowed to specify all members in a group as an irrecoverable member.

<a id="dad74e6218522d61"></a>
### Description

It is used to restart the system excluding the corresponding member if the cluster failed to restart due to an irrecoverable member. The corresponding member should be dropped by using [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#e511a40b370e1420) after the system succeeded to restart.

<a id="0127816e7433e1ae"></a>
### Examples

The following is an example of executing IRRECOVERABLE CLUSTER MEMBER.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="b62465cb16353cf1"></a>
### Compatibility

The SQL standard does not define the concepts of IRRECOVERABLE CLUSTER MEMBER.

<a id="93365f06a2e0defc"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="c9a1ecb5a19a9db7"></a>
### Function

It includes a specific inactive cluster member in a cluster system again.

<a id="8b5870bea9731fc3"></a>
### Syntax

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="be6798e39ed06e0d"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter system join database statement&gt;.

<a id="2acd9f251ef38fe2"></a>
### Description

The inactive state of a cluster member means that it is not connected to the cluster system, and it occurs in the following cases.

- An error occurs on a cluster member in an operating cluster system.
- Trying to start-up the cluster system without driving the cluster member included in the cluster system.

If a specific cluster member is inactive, then the member can be included in a cluster system again according to the following procedure.

- Start-up the unstarted cluster member to the local open phase.

```
$ gsql sys gliese --as sysdba --dsn=G3N2
gSQL> \startup
```

- Include it in a cluster system by using &lt;alter system join database statement&gt;.

```
$ gsql sys gliese --as sysdba --dsn=G3N2
gSQL> ALTER SYSTEM JOIN DATABASE;
```

Use &lt;alter system join database statement&gt; to make an inactive cluster member which is started up to the local open phase to participate in the cluster system without shutting it down.

To make the inactive cluster member to participate in the cluster system again, the database state of the cluster system and that of the inactive cluster member should be same.

The inactive cluster member can not participate in the cluster system again after the transaction altering the database in the cluster system completed.

To operate the cluster system normally the inactive cluster members should be dropped according to the following procedure when multiple inactive cluster members exist.

1. JOIN inactive cluster members which can participate in the cluster system.

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

2. DROP inactive cluster members which can not participate in the cluster system.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;
```

All inactive cluster members which can participate in the cluster system should be included in the cluster system before dropping because all inactive cluster members are dropped from the cluster system when performing &lt;alter database drop inactive cluster member statement&gt;.

<a id="ca1782f3bfdcc999"></a>
### Examples

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="aab3b7182c9d57c2"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="9a04d23e3258a8f8"></a>
### For More Information

Refer to [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#e511a40b370e1420).

<a id="e5a37a0f857e01cd"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="66a3a651a2dcb2e5"></a>
### Function

It mounts the database on system, or alters the database to the state which is available for the service.

<a id="364244dfda12943e"></a>
### Syntax

```
<alter system database statement> ::=
    ALTER SYSTEM <alter system database clause>
    ;

<alter system database clause> ::= 
      MOUNT DATABASE
    | OPEN [ <database_scope> ] DATABASE [ <open_database_option> ]

<open_database_option> ::=
      READ WRITE [ NORESETLOGS | RESETLOGS ]
    | READ ONLY

<database_scope> ::=
	  LOCAL
    | GLOBAL
```

<a id="e8425ad85ebaa22a"></a>
### Invocation and Access Rules

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter system database statement&gt;.

<a id="415c6dea5e1ee0b2"></a>
### Syntax Rules and Parameters

<a id="adc293f9d9857567"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - It mounts the database on the system.
- OPEN DATABASE
    - It changes the database to the state which is available for the service.

<a id="8eda82928dd803c2"></a>
#### &lt;open database option&gt;

- READ ONLY / READ WRITE
    - It specifies the read/write mode and drives the database.
    - If it is omitted, it is driven in READ WRITE.
- RESETLOGS / NORESETLOGS
    - It determines whether to keep the online redo logs after recovering the database.
    - NORESETLOGS maintains the existing redo log, but RESETLOGS initializes it.
    - RESETLOGS should be specified when the database is incompletely recovered.
    - If it is omitted, NORESETLOGS is specified by default.

<a id="42cb561da2f04da6"></a>
#### &lt;database_scope&gt;

- LOCAL
    - It starts up the LOCAL server to the OPEN phase.
- GLOBAL
    - It starts up the GLOBAL server, the entire server, to the OPEN phase.
- If it is omitted in a cluster environment, it starts up the GLOBAL server.

<a id="d4995d67d3c8cf46"></a>
### Examples

The following is an example of driving the database in read only.

```
ALTER SYSTEM OPEN DATABASE READ ONLY;
```

The following is an example of driving the database in read/write, and initializing the online redo logs.

```
ALTER SYSTEM OPEN DATABASE READ WRITE RESETLOGS;
```

<a id="a9cfa3c7eb2db6b6"></a>
### Compatibility

The SQL standard does not define the concepts of MOUNT or OPEN in the database.

<a id="1035ad07d73fac82"></a>
### For More Information

Refer to [ALTER DATABASE RECOVER](#24aaa87abb398f65).

<a id="1676380aa453fb44"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="cf67c1a8a324632f"></a>
### Function

It terminates a session.

<a id="05beeeb5f17e9135"></a>
### Syntax

```
<alter system end session statement> ::=
      ALTER SYSTEM DISCONNECT SESSION [<member_position>,] <session_id>,
           <serial#> [<disconnect_option>] [AT <domain name>]
    |  ALTER SYSTEM KILL SESSION [<member_position>,]
           <session_id>, <serial#> [AT <domain name>]
    ;
<disconnect_option> ::=
      POST_TRANSACTION
    | IMMEDIATE
```

<a id="0330c29a114c8d59"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system end session statement&gt;.

<a id="a298377a3bfe4a31"></a>
### Syntax Rules and Parameters

<a id="694062056ddfa5aa"></a>
#### &lt;member_position&gt;

It is a member position of a session which is a disconnect/kill target in a cluster environment.

<a id="dd34c35834fd0259"></a>
#### &lt;session_id&gt;

It is the session ID.

<a id="8994da8c14e2bbf6"></a>
#### &lt;serial#&gt;

It is the SERIAL NUMBER of the session.

<a id="fcd106e5b653aeed"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: The session is terminated after completion of the transaction.
- IMMEDIATE: The session is immediately terminated without waiting for the completion of the transaction.

If &lt;disconnect_option&gt; is not used, then it is operated in IMMEDIATE.

<a id="c7231b41c8408ef9"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="c4b2b59ad42c80c9"></a>
### Description

DISCONNECT SESSION can specify the options such as POST TRANSACTION and IMMEDIATE.   
POST TRANSACTION terminates the session after the currently running transaction is completed. IMMEDIATE terminates the session after immediately cleaning up the currently running transaction.

KILL SESSION terminates the abnormal session which remains on the system without its process.

<a id="0b0e6978c90af9de"></a>
### Example

```
gSQL> SELECT USER_NAME, SESSION_ID, SERIAL_NO, SESSION_STATUS, PROGRAM_NAME FROM V$SESSION WHERE USER_NAME = 'TEST';

USER_NAME SESSION_ID SERIAL_NO SESSION_STATUS PROGRAM_NAME
--------- ---------- --------- -------------- ------------
TEST              62        49 CONNECTED      gsql        
TEST              65       109 CONNECTED      gsqlnet     
TEST              66       130 CONNECTED      gsql        

3 rows selected.

gSQL> ALTER SYSTEM DISCONNECT SESSION 65, 109;

System altered.
```

<a id="9eadb0fd75c7851f"></a>
### Compatibility

The SQL standard does not define it.

<a id="09f225f9ae90b003"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="7ac42a5d4ef48fd4"></a>
### Function

It determines whether to reconnect to the session which is connected in GLOBAL CONNECTION form.

<a id="1d83aff62a8147eb"></a>
### Syntax

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="d1251d69e6b6a509"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system reconnect global connection statement&gt;.

<a id="8b619398014d9a48"></a>
### Description

Whether the GLOBAL CONNECTION client reconnects is determined by comparing SCN of a system object acquired from a server at the first connection and SCN of current server system object. This statement leads the client to reconnect by increasing SCN of the system object.

The client does not necessarily reconnect immediately after this statement is performed. The client reconnects by comparing SCN when the client executes a command in a server, and it does not try to reconnect if connections to all members from a client are valid.

<a id="50b1c3c27c96d1a8"></a>
### Examples

The following is an example of executing the statement.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="6a666318b2df9487"></a>
### Compatibility

The SQL standard does not define the concepts of GLOBAL CONNECTION.

<a id="8369550130177ff2"></a>
## ALTER SYSTEM RESET property_name

<a id="e6dbd1e60af2a0db"></a>
### Function

It removes a property value from the property file.

<a id="f3a2418556b3479d"></a>
### Syntax

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="352b203cdcaa5e2b"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system reset statement&gt;.

<a id="0082e4c3ceb687d7"></a>
### Syntax Rules and Parameters

<a id="8b507ece8b6839db"></a>
#### { RESET | UNSET }

RESET and UNSET are the reserved words with the same meaning, so either of them can be used.

<a id="18d5e3c7f94a9d9e"></a>
#### &lt;property name&gt;

It is the property name to be removed.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#6c2d42da1f4f968c) in an administration manual.

<a id="70002c8eaa885787"></a>
#### [ SCOPE = { FILE | SPFILE } ]

It removes the property from a property file, so only SCOPE=FILE/SPFILE can be used.

- SCOPE = FILE 
    - FILE and SPFILE are the reserved words with the same meaning, so either of them can be used. 
    - A property is removed from FILE, and is not applied to the current state.
    - When restarting the database, the changes are applied.

If SCOPE clause is not specified, the default value is SCOPE = FILE.

<a id="bcd3810e455de257"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="1a8f19d61bfced98"></a>
### Description

If a property is altered by using SCOPE=FILE/SPFILE, the updated property value is stored in the property file, and it is applied when restarting the database.

When executing RESET, the updated property value is removed from the property file and the default value is used when restarting the database.

<a id="b3c422bbeb6a3ca2"></a>
### Examples

The following is an example of altering the property by using SCOPE=FILE.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

System altered.

gSQL> alter system set DEFAULT_INDEX_LOGGING=YES scope=FILE;

System altered.
```

The following is an example of removing the property altered above.

```
gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT SCOPE=FILE;

System altered.

gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT SCOPE=SPFILE;

System altered.

gSQL> ALTER SYSTEM RESET PROCESS_MAX_COUNT;

System altered.

gSQL> ALTER SYSTEM RESET DEFAULT_INDEX_LOGGING;

System altered.

gSQL> ALTER SYSTEM UNSET DEFAULT_INDEX_LOGGING;

System altered.
```

<a id="ec3c4ad2550ea2ec"></a>
### Compatibility

The SQL standard does not define the concepts of the system property.

<a id="3024d70431e25b61"></a>
### For More Information

Refer to [ALTER SYSTEM SET property_name](#d5748a5f89f15f32).

<a id="d5748a5f89f15f32"></a>
## ALTER SYSTEM SET property_name

<a id="301a89ef18861bec"></a>
### Function

It sets the system property value.

<a id="4d186d368f1a65d7"></a>
### Syntax

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="62af1384d560dd84"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system set statement&gt;.

<a id="2c732bf083b375ae"></a>
### Syntax Rules and Parameters

<a id="646c0ce10d0caa33"></a>
#### &lt;property name&gt;

It is the property name to be set.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#6c2d42da1f4f968c) in an administration manual.

<a id="dec5d700cad5b10d"></a>
#### &lt;property value&gt;

It is the property value to be set.

<a id="7fa33d92c5b3500a"></a>
#### TO DEFAULT

It sets the system property value as the initial value of system driving.

<a id="1dc8303492b02939"></a>
#### [ DEFERRED ]

It defines the point of time to apply the altered property.

- DEFERRED 
    - It does not effect the current SESSION, but it is applied to the newly generated SESSION.
    - It can be applied when ISSYS_MODIFIABL property value is IMMEDIATE/DEFERRED. It should be explicitly specified. 
    - It is not applicable when the SYS_MODIFIABLE property value is FALSE.

If SYS_MODIFIABLE property value is IMMEDIATE, and DEFERRED is not explicitly specified, then it is immediately applied to all sessions.

<a id="2ac5343aa5d59bf7"></a>
#### [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]

It specifies the range which is affected by the property changes of the system.

- SCOPE = MEMORY 
    - The changes are applied only to the current state, and the value is lost when restarting the database.
- SCOPE = FILE 
    - FILE and SPFILE are the reserved words with the same meaning, so either of them can be used. 
    - The changes are stored in FILE, and not applied to the current state.
    - The changes are applied when restarting the database.
- SCOPE = BOTH 
    - The changes are stored in FILE, and applied to the current state.

If SCOPE clause is omitted, the default value is SCOPE = MEMORY.  
If SYS_MODIFIABLE property value is FALSE, it should be specified as SCOPE=FILE/SPFILE.

<a id="e2fedc30b353317d"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="0fe9b9c0f5e43bb7"></a>
### Description

For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#6c2d42da1f4f968c) in an administration manual.

<a id="557b65e15c05bb1c"></a>
### Examples

The following is an example of changing the property whose SYS_MODIFIABLE property is DEFERRED.

```
gSQL> ALTER SYSTEM SET HINT_ERROR = ON;

ERR-22000(13019): Invalid property modify mode.(HINT_ERROR)

gSQL> ALTER SYSTEM SET HINT_ERROR = ON DEFERRED;

System altered.
```

The following is an example of changing the property whose SYS_MODIFIABLE property is FALSE.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128;

ERR-22000(13018): Specified property cannot be modified with this SCOPE option.(PROCESS_MAX_COUNT)

gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

System altered.
```

The following is an example of changing the altered property to the default value of when the session was connected.

```
gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE=0;

System altered.

gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE TO DEFAULT;

System altered.

gSQL> ALTER SYSTEM SET TRANSACTION_COMMIT_WRITE_MODE TO DEFAULT DEFERRED;

System altered.
```

<a id="747311f6bd7838eb"></a>
### Compatibility

The SQL standard does not define the concepts of the system property.

<a id="05038ff5b1eb5fb5"></a>
### For More Information

Refer to [ALTER SYSTEM RESET property_name](#8369550130177ff2).

<a id="860138cb583a47fd"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="9098a61c39b9054f"></a>
### Function

It alters the log files in CURRENT state to ACTIVE state in database.

<a id="b9de0edfc2420ce3"></a>
### Syntax

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="e7721b508acd0b30"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system switch logfile statement&gt;.

<a id="81a421d72b4578d6"></a>
### Syntax Rules and Parameters

<a id="334c35d91073d974"></a>
#### &lt;alter system switch logfile statement&gt;

The database should be in MOUNT or OPEN phase.

<a id="d60f69000d4b7bc4"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="0878995e0d153837"></a>
### Description

Basically, if the log file in CURRENT state is filled, the log switch automatically occurs. That statement is used to forcibly execute log switch in special circumstances.

<a id="07fb5608eb104765"></a>
### Example

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="55cbe16b68ebe08d"></a>
### Compatibility

The SQL standard does not define the concepts of the LOGFILE.

<a id="259e3616ce69efd3"></a>
### For More Information

Refer to [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#e5a37a0f857e01cd).

<a id="90e40a320994005d"></a>
## ALTER TABLE

<a id="4c83c8629aa3c2e4"></a>
### Function

It alters the table definition.

<a id="86dfb4395712b6e0"></a>
### Syntax

```
<alter table statement> ::=
      <alter table physical attribute statement>
    | <rename table statement>
    | <add column definition>
    | <drop column definition>
    | <alter column definition>
    | <rename column statement>
    | <add table constraint definition>
    | <drop table constraint definition>
    | <alter table constraint definition>
    | <add table supplemental log statement>
    | <drop table supplemental log statement>
    | <rebalance statement>
    | <move shard statement>
    | <split shard statement>
    ;
```

<a id="5587a336b9cedd81"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for the table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="782363da8ff00226"></a>
### Syntax Rules and Parameters

<a id="6c712cec7c89b9f3"></a>
#### &lt;alter table physical attribute statement&gt;

It alters physical attributes of a table.  
For more information, refer to [ALTER TABLE name STORAGE](#4dd7d18d5dcf2174).

<a id="19ec1fa5d2f4f2f7"></a>
#### &lt;rename table statement&gt;

It renames the table.  
For more information, refer to [ALTER TABLE name RENAME TO](#49b7a9e000ac5b20).

<a id="5b565dd92010815f"></a>
#### &lt;add column definition&gt;

It adds columns to the table.  
For more information, refer to [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16).

<a id="b5394d4c5f988b7f"></a>
#### &lt;drop column definition&gt;

It drops a column from the table.  
For more information, refer to [ALTER TABLE name SET UNUSED COLUMN](#d1bfb6824c4855f9).

<a id="9a369d2adc32d572"></a>
#### &lt;alter column definition&gt;

It alters the column definition in the table.  
For more information, refer to [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b).

<a id="a3925a49e026b7ff"></a>
#### &lt;rename column statement&gt;

It renames the column in the table.  
For more information, refer to [ALTER TABLE name RENAME COLUMN](#3cd0fd960aabac66).

<a id="9e8fd0ea9b1d03ae"></a>
#### &lt;add table constraint definition&gt;

It adds constraints to the table.  
For more information, refer to [ALTER TABLE name ADD CONSTRAINT](#65400a8940d0436c).

<a id="bc1aa27073502b07"></a>
#### &lt;drop table constraint definition&gt;

It drops the constraints of the table.  
For more information, refer to [ALTER TABLE name DROP CONSTRAINT](#5f73b4ecf07ae833).

<a id="683d17274b5353bf"></a>
#### &lt;alter table constraint definition&gt;

It alters the constraints of the table.  
For more information, refer to [ALTER TABLE name ALTER CONSTRAINT](#dbba103b11769053).

<a id="62da6e90c9486a63"></a>
#### &lt;rename table constraint statement&gt;

It renames the constraints of the table.  
For more information, refer to [ALTER TABLE name RENAME CONSTRAINT](#fdce17f8e7a2137b).

<a id="c2cfee6cdaf13365"></a>
#### &lt;add table supplemental log statement&gt;

It sets to add information to the redo log when the data is altered in the table.  
For more information, refer to  [ALTER TABLE name ADD SUPPLEMENTAL LOG](#057d2a978c3e044c).

<a id="3b5c133d7e4c071f"></a>
#### &lt;drop table supplemental log statement&gt;

It sets not to add information to the redo log when the data is altered in the table.   
For more information, refer to [ALTER TABLE name DROP SUPPLEMENTAL LOG](#1fe2b729e647576f).

<a id="a38cb750807844b5"></a>
#### &lt;rebalance statement&gt;

It restores consistency by rebalancing the shard of the table or by synchronizing the broken shard in a cluster environment.   
For more information, refer to [ALTER TABLE name REBALANCE](#467720ee446849be).

<a id="4e11f013a8fb3a9f"></a>
#### &lt;move shard statement&gt;

It rebalances a specific shard of a table on a specific cluster group in a cluster environment.  
For more information, refer to [ALTER TABLE name MOVE SHARD](#acf74aaf4961edaa).

<a id="73b82e6299922916"></a>
#### &lt;split shard statement&gt;

It rebalances a specific shard of a table on a specific cluster group by splitting the shard in a cluster environment.  
For more information, refer to [ALTER TABLE name SPLIT SHARD](#b959c469127f77b7).

<a id="f1c0fdcf8ebc296d"></a>
#### &lt;rename shard statement&gt;

It renames a specific shard of a table in cluster environment.   
For more information, refer to [ALTER TABLE name RENAME SHARD](#c7ea8d74ec6bdc02).

<a id="4fcf80de2f2ee837"></a>
#### &lt;read { only | write } statement&gt;

It sets READ ( only | write } to a table.  
For more information, refer to [ALTER TABLE name READ { ONLY | WRITE }](#7ec007f109a6e713).

<a id="cf2637c7c3a2c5a6"></a>
### Description

For more information, refer to the description of each detailed statement.

<a id="a08bc0115f042a56"></a>
### Example

Refer to the examples of each detailed statement.

<a id="aa388a08cebd1083"></a>
### Compatibility

The SQL standard does not define the following statements.

- &lt;alter table physical attribute statement&gt; 
- &lt;rename table statement&gt; 
- &lt;rename column statement&gt; 
- &lt;rename table constraint statement&gt;
- &lt;add table supplemental log statement&gt; 
- &lt;drop table supplemental log statement&gt;
- &lt;rebalance statement&gt;
- &lt;move shard statement&gt;
- &lt;split shard statement&gt;
- &lt;rename shard statement&gt;
- &lt;read { only | write } statement&gt;

<a id="d350cd62e4767b16"></a>
## ALTER TABLE name ADD COLUMN

<a id="9fb7b0dd8adc0b91"></a>
### Function

It adds a column to the table.

<a id="92ffbc96011857ca"></a>
### Syntax

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="567b79a3c7f9ac66"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;add column definition&gt;.

- At least one of the following privileges is required to alter the table.
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE

- If the constraints are specified with the added columns, the conditions should be satisfied to generate the constraints as follows.
    - One of the following privileges is required for the schema in which constraints are to be generated. 
        - (ADD CONSTRAINT or CONTROL SCHEMA) ON SCHEMA for the schema
        - ALTER ANY TABLE ON DATABASE 
    - If the key constraint is to be generated, one of the following privileges is required for the tablespace in which an index is to be created. 
        - CREATE OBJECT ON TABLESPACE for the tablespace
        - USAGE TABLESPACE ON DATABASE

- The table owner has the following privileges for the added columns.
    - Privileges on all added columns 
        - SELECT(columns) ON TABLE WITH GRANT OPTION 
        - INSERT(columns) ON TABLE WITH GRANT OPTION 
        - UPDATE(columns) ON TABLE WITH GRANT OPTION 
        - REFERENCES(columns) ON TABLE WITH GRANT OPTION 
    - Privilege on the constraint generated together
        - The owner of that constraint 
        - The index owner generated together with the constraint

<a id="e5b9923e607e370e"></a>
### Syntax Rules and Parameters

<a id="7525b8cecdf1c8d6"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="0493a284b7814376"></a>
#### ADD [ COLUMN ]

The reserved word COLUMN can be omitted.

<a id="643fd92856f7c4d7"></a>
#### &lt;column definition&gt;

It defines the column to be added. For more information, refer to [&lt;column definition&gt;](#33f0fb077cded0d9) clause of [CREATE TABLE](#72507f5467c281c9) statement.  
There should not be columns with the same name in a table.

If DEFAULT clause is specified when defining the column, the default value of all rows are stored in the added column.  
If &lt;identity column specification&gt; clause is specified when defining the column, each automatically generated value of all rows is stored in the added column.  
If NOT NULL constraint is specified when defining the column, the table should be empty or it should be specified together with DEFAULT or &lt;identity column specification&gt; clause.

<a id="88ff2994905b9c51"></a>
#### ( &lt;column definition&gt; [, ...] )

It adds multiple columns.  
It lists multiple &lt;column definition&gt; inside the parentheses.

<a id="89b8c128e2f5e948"></a>
### Description

The added column is positioned at the end of the existing columns.  
When specifying DEFAULT or &lt;identity column specification&gt; clause, the processing time is increased in proportion to the number of the rows in the table.

<a id="809b0e0c8f651319"></a>
### Examples

The following is an example of adding a column.

```
gSQL> ALTER TABLE region ADD COLUMN r_new_comment VARCHAR(152);

Table altered.
```

The following is an example of adding multiple columns.

```
gSQL> ALTER TABLE partsupp ADD COLUMN ( 
   ps_retailprice NUMERIC(12,2), 
   ps_acctbal NUMERIC(12,2), ps_mktsegment  CHAR(10) );

Table altered.
```

The following is an example of adding the identity column and the column including DEFAULT clause.

```
gSQL> ALTER TABLE region ADD COLUMN ( 
    r_regionkey INTEGER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    r_comment   VARCHAR(152) DEFAULT 'N/A' );

Table altered.

gSQL> SELECT r_regionkey, r_name, r_comment FROM region;

R_REGIONKEY R_NAME                    R_COMMENT
----------- ------------------------- ---------
          1 AFRICA                    N/A      
          2 AMERICA                   N/A      
          3 ASIA                      N/A      
          4 EUROPE                    N/A      
          5 MIDDLE EAST               N/A      

5 rows selected.
```

The following is an example of adding the column including the deferrable constraint.

```
gSQL> ALTER TABLE t1 ADD COLUMN ( id INTEGER CONSTRAINT t1_uk UNIQUE DEFERRABLE );

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="63715df424ddaa41"></a>
### Compatibility

The SQL standard does not define of adding multiple column definitions.

<a id="b887b4e10d165344"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name SET UNUSED COLUMN](#d1bfb6824c4855f9)
- [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b)
- [ALTER TABLE name RENAME COLUMN](#3cd0fd960aabac66)

<a id="d1bfb6824c4855f9"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="a65263a6a422723e"></a>
### Function

It drops a table column.

<a id="08b411a4c572935f"></a>
### Syntax

```
<drop column definition> ::=
    ALTER TABLE table_name <drop column clause>
    ;

<drop column clause> ::=
      SET UNUSED [ COLUMN ] <column_name_list> [ <drop behavior> ]

<column name list> ::=
      column_name
    | ( column_name [, ...] )

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="d5076625920a0ce7"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop column definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="14e8c0b4140f0498"></a>
### Syntax Rules and Parameters

<a id="756ce02a6b330058"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="13f4c0e5c2f2f00f"></a>
#### SET UNUSED [ COLUMN ]

It sets the column not to be used.

<a id="71498c9c1f5aa526"></a>
#### column_name_list

One or more column names to be dropped.

- e.g. ALTER TABLE t1 SET UNUSED COLUMN c1 
- e.g. ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="98acec55263f1e2f"></a>
#### column_name

It is the column name to be dropped.  
It also drops the constraints and indexes which use the column.

<a id="57932dc1ea3026b0"></a>
#### drop behavior

When it is omitted, the default value is RESTRICT.  
Currently, RESTRICT/CASCADE is operated in the same way.

<a id="152b8824ef0d1d9c"></a>
### Description

SET UNUSED COLUMN does not delete the data physically, so it ensures consistent performance regardless of the number of the rows.

<a id="6da6ba91b8d2089d"></a>
### Example

The following is an example of setting the column not to be used.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="22f0d4fc2827d0e7"></a>
### Compatibility

The SQL standard does not define the following clauses.  

• SET UNUSED   
• CASCADE CONSTRAINTS   
• Listing multiple columns

**SQL standard compatibility**

<a id="244c66568a869a38"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="a8330c76e49fd134"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16)
- [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b)
- [ALTER TABLE name RENAME COLUMN](#3cd0fd960aabac66)

<a id="6df8140b35bd2d2b"></a>
## ALTER TABLE name ALTER COLUMN

<a id="652f8877ae0eeba1"></a>
### Function

It alters the column definition.

<a id="a9422754a9657cab"></a>
### Syntax

```
<alter column definition> ::=
    ALTER TABLE table_name 
        ALTER [ COLUMN ] column_name <alter column action>

<alter column action> ::=

      <set column default clause>
    | <drop column default clause>
    | <set column not null clause>
    | <drop column not null clause>
    | <alter column data type clause>
    | <alter identity column specification>
    | <drop identity property clause>    
    ;

<set column default clause> ::=
    SET DEFAULT <default option>

<drop column default clause> ::=
    DROP DEFAULT

<set column not null clause> ::=
    SET [ CONSTRAINT constraint_name ] NOT NULL [ <constraint characteristics> ]


<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ]
    | <constraint check time> [ [ NOT ] DEFERRABLE ]

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE

<drop column not null clause> ::=
    DROP NOT NULL

<alter column data type clause> ::=
    SET DATA TYPE <data type> 

<alter identity column specification> ::=
     <set identity column generation clause> [ <alter identity column option> ... ]
   | <alter identity column option> ...

<set identity column generation clause> ::=
   SET GENERATED { ALWAYS | BY DEFAULT }

<alter identity column option> ::=
     <alter sequence generator restart option>
   | [ SET ] <basic sequence generator option>

<alter sequence generator restart option> ::=
    RESTART [ WITH integer ]

<basic sequence generator option> ::=
      <sequence generator increment by option>
    | <sequence generator maxvalue option>
    | <sequence generator minvalue option>
    | <sequence generator cycle option>
    | <sequence generator cache option>

<drop identity property clause> ::=
    DROP IDENTITY
```

<a id="2dd9ddeba6ade30c"></a>
### Invocation and Access Rules

One of the following privileges is required to performing &lt;alter column definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="d6bae467930bcbfe"></a>
### Syntax Rules and Parameters

<a id="44eba44d301d54e0"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="d3877609dee3a55a"></a>
#### ALTER [ COLUMN ]

The reserved word COLUMN can be omitted.

<a id="5c8ca4f474b4e0bc"></a>
#### column_name

It is the column name to be altered.

<a id="fb0aeafe5a80e13b"></a>
#### &lt;set column default clause&gt;

It sets the default value of the column.  
It should not be an identity column.

The default value set when using the DEFAULT clause is used in INSERT statement later.

The data type of DEFAULT expression should be compatible with the data type of the column.  
If there is insufficient space or the data type is not compatible, an error occurs when using DEFAULT  in INSERT, UPDATE statements.

For more information, refer to [&lt;default clause&gt;](#77b8ab635fda06de) of [CREATE TABLE](#72507f5467c281c9) statement.

<a id="f2eed952a15c674d"></a>
#### &lt;drop column default clause&gt;

It drops the default value of the column.  
It should not be an identity column.  
If the default value is dropped, NULL is set when using DEFAULT clause in INSERT statement.

<a id="b276b4b3b3174331"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - It sets NOT NULL constraint on the column.
    - NULL is not allowed as the column value.
    - NULL should not exist in the column.

- If [CONSTRAINT constraint_name] is omitted, the constraint name is automatically given. 
- If &lt;constraint characteristics&gt; is omitted, it has NOT DEFERRABLE INITIALLY IMMEDIATE property. 
- The Identity column can not have DEFERRABLE property.

For more information about the DEFERRABLE constraint, refer to [SET CONSTRAINTS](#8337ae2c011b78f5).

<a id="0ccf23382f6334b2"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - It drops NOT NULL constraint from the column.

<a id="d1d235380dc3280c"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - It changes the data type of the column.

> SET DATA TYPE is a DDL statement which is automatically committed.

The type conversion can be executed among the same family, and it should satisfy the following conditions.

**Conversion of character string type**

<a id="4a651eb2848a9701"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

The conversion of char length unit should satisfy the following condition.

**Conversion of character length unit**

<a id="1b64e03c65754c6d"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**Conversion of binary string type**

<a id="a73d3e8af5daa3be"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**Conversion of numeric type**

<a id="a92a9e776b746b4b"></a>
| from \ to | SMALLINT | INTEGER | BIGINT | NUMERIC | NUMERIC(q) | NUMERIC(q,t) | NUMBER(q) | NUMBER(q,t) | REAL | DOUBLE PRECISION | FLOAT | FLOAT(q) | NUMBER |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SMALLINT | O | O | O | O | q >= 5 | q >= 5  t >= 0  (q-t) >= 5 | q >= 5 | q >= 5  t >= 0  (q-t) >= 5 | O | O | O | ddc(q) >= 5 | O |
| INTEGER | X | O | O | O | q >= 10 | q >= 10  t >= 0  (q-t) >= 10 | q >= 10 | q >= 10  t >= 0  (q-t) >= 10 | X | O | O | ddc(q) >= 10 | O |
| BIGINT | X | X | O | O | q >= 19 | q >= 19  t >= 0  (q-t) >= 19 | q >= 19 | q >= 19  t >= 0  (q-t) >= 19 | X | X | O | ddc(q) >= 19 | O |
| NUMERIC | X | X | X | O | q == 38 | q == 38  t == 0 | q == 38 | q == 38  t == 0 | X | X | O | ddc(q) == 38 | O |
| NUMERIC(p) | 5 >= p | 10 >= p | 19 >= p | O | q >= p | q >= p  t >= 0  (q-t) >= p | q >= p | q >= p  t >= 0  (q-t) >= p | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMERIC(p,s) | 5 >= p  0 >= s  5 >= (p-s) | 10 >= p  0 >= s  10 >= (p-s) | 19 >= p  0 >= s 19 >= (p-s) | 38 >= p  0 >= s  38 >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMBER(p) | 5 >= p | 10 >= p | 19 >= p | O | q >= p | q >= p  t >= 0  (q-t) >= p | q >= p | q >= p  t >= 0 (q-t) >= p | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| NUMBER(p,s) | 5 >= p  0 >= s  5 >= (p-s) | 10 >= p 0 >= s 10 >= (p-s) | 19 >= p  0 >= s  19 >= (p-s) | 38 >= p  0 >= s 3 8 >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s  (q-t) >= (p-s) | q >= p  0 >= s  q >= (p-s) | q >= p  t >= s (q-t) >= (p-s) | 8 >= p | 16 >= p | O | ddc(q) >= p | O |
| REAL | X | X | X | X | X | X | X | X | O | O | O | ddc(q) >= 8 | O |
| DOUBLE PRECISION | X | X | X | X | X | X | X | X | X | O | O | ddc(q) >= 16 | O |
| FLOAT | X | X | X | X | X | X | X | X | X | X | O | ddc(q) == 38 | O |
| FLOAT(p) | X | X | X | X | X | X | X | X | 8 >= ddc(p) | 16 >= ddc(p) | O | ddc(q) >= ddc(p) | O |
| NUMBER | X | X | X | X | X | X | X | X | X | - | O | ddc(q) == 38 | O |

Decimal digit count (ddc) value for the FLOAT (p) is as follows.

**Decimal digit count (ddc) value**

<a id="114861a4e0f3f80e"></a>
| FLOAT(p) | ddc(p) |
| --- | --- |
| 1 ~ 3 | 1 |
| 4 ~ 6 | 2 |
| 7 ~ 9 | 3 |
| 10 ~ 13 | 4 |
| 14 ~ 16 | 5 |
| 17 ~ 19 | 6 |
| 20 ~ 23 | 7 |
| 24 ~ 26 | 8 |
| 27 ~ 29 | 9 |
| 30 ~ 33 | 10 |
| 34 ~ 36 | 11 |
| 37 ~ 39 | 12 |
| 40 ~ 43 | 13 |
| 44 ~ 46 | 14 |
| 47 ~ 49 | 15 |
| 50 ~ 53 | 16 |
| 54 ~ 56 | 17 |
| 57 ~ 59 | 18 |
| 60 ~ 63 | 19 |
| 64 ~ 66 | 20 |
| 67 ~ 69 | 21 |
| 70 ~ 73 | 22 |
| 74 ~ 76 | 23 |
| 77 ~ 79 | 24 |
| 80 ~ 83 | 25 |
| 84 ~ 86 | 26 |
| 87 ~ 89 | 27 |
| 90 ~ 93 | 28 |
| 94 ~ 96 | 29 |
| 97 ~ 99 | 30 |
| 100 ~ 103 | 31 |
| 104 ~ 106 | 32 |
| 107 ~ 109 | 33 |
| 110 ~ 113 | 34 |
| 114 ~ 116 | 35 |
| 117 ~ 119 | 36 |
| 120 ~ 123 | 37 |
| 124 ~ 126 | 38 |

All numeric types are managed in the same structure, and each numeric type is as same as the following NUMBER (p, s) expression.

**NUMBER expressions of the numeric types**

<a id="61165d784f40fc3a"></a>
| Numeric type | NUMBER(p,s) expression |
| --- | --- |
| SMALLINT | NUMBER(5,0) |
| INTEGER | NUMBER(10,0) |
| BIGINT | NUMBER(19,0) |
| NUMERIC | NUMBER(38,0) |
| NUMERIC(p) | NUMBER(p,0) |
| NUMERIC(p,s) | NUMBER(p,s) |
| NUMBER(p) | NUMBER(p,0) |
| NUMBER(p,s) | NUMBER(p,s) |
| REAL | NUMBER(8,N/A) <= FLOAT(24) |
| DOUBLE PRECISION | NUMBER(16,N/A) <= FLOAT(53) |
| FLOAT | NUMBER(38,N/A) <= FLOAT(126) |
| FLOAT(p) | NUMBER( ddc(p), N/A ) |
| NUMBER | NUMBER(38, N/A ) |

Native numeric type is as same with as C language numeric type, and it can not be converted to another type.

**Conversion of native numeric type**

<a id="1b621d400f026e8e"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Conversion of boolean type**

<a id="490ee9832e59786e"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Conversion of date/time type (TZ: WITH TIME ZONE)**

<a id="c5fa116e7e056e5d"></a>
| from \ to | DATE | TIME | TIME(g) | TIME TZ | TIME(g) TZ | TIMESTAMP | TIMESTAMP(g) | TIMESTAMP TZ | TIMESTAMP(g) TZ |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DATE | O | X | X | X | X | X | X | X | X |
| TIME | X | O | g >= 6 | X | X | X | X | X | X |
| TIME(f) | X | 6 >= f | g >= f | X | X | X | X | X | X |
| TIME TZ | X | X | X | O | g >= 6 | X | X | X | X |
| TIME(f) TZ | X | X | X | 6 >= f | g >= f | X | X | X | X |
| TIMESTAMP | X | X | X | X | X | O | g >= 6 | X | X |
| TIMESTAMP(f) | X | X | X | X | X | 6 >= f | g >= f | X | X |
| TIMESTAMP TZ | X | X | X | X | X | X | X | O | g >= 6 |
| TIMESTAMP(f) TZ | X | X | X | X | X | X | X | 6 >= f | g >= f |

**Type conversion of INTERVAL YEAR TO MONTH family (If p,q are omitted, then it is 2.)**

<a id="b05d662eec8075ab"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**Type conversion of INTERVAL DAY TO TIME family (If p,q are omitted, then it is 2.) (If f,g are omitted, then it is 6.)**

<a id="eed9142097c1b774"></a>
| from \ to | DAY(q) | HOUR(q) | MINUTE(q) | SECOND(q,g) | DAY(q) TO HOUR | DAY(q) TO MINUTE | DAY(q) TO SECOND(g) | HOUR(q) TO MINUTE | HOUR(q) TO SECOND(g) | MINUTE(q) TO SECOND(g) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DAY(p) | q >= p | X | X | X | X | X | X | X | X | X |
| HOUR(p) | X | q >= p | X | X | X | X | X | X | X | X |
| MINUTE(p) | X | X | q >= p | X | X | X | X | X | X | X |
| SECOND(p,f) | X | X | X | q >= p  g >= f | X | X | X | X | X | X |
| DAY(p) TO HOUR | X | X | X | X | q >= p | X | X | X | X | X |
| DAY(p) TO MINUTE | X | X | X | X | X | q >= p | X | X | X | X |
| DAY(p) TO SECOND(f) | X | X | X | X | X | X | q >= p g >= f | X | X | X |
| HOUR(p) TO MINUTE | X | X | X | X | X | X | X | q >= p | X | X |
| HOUR(p) TO SECOND(f) | X | X | X | X | X | X | X | X | q >= p  g >= f | X |
| MINUTE(p) TO SECOND(f) | X | X | X | X | X | X | X | X | X | q >= p  g >= f |

**Conversion of ROWID type**

<a id="74366247482b75ce"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="bf886d93386114be"></a>
#### &lt;alter identity column specification&gt;

It alters the identity property of the column.  
The column should be an identity column.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - It changes the method of generating the identity column.
    - For more information, refer to [&lt;identity column specification&gt;](#bb2126450b9efec0) of [CREATE TABLE](#72507f5467c281c9) statement. 
- &lt;alter sequence generator restart option&gt; 
    - It changes NEXT VALUE of the identity column.
    - For more information, refer to [&lt;alter sequence generator restart option&gt;](#7b8bfdf2eb1e8261) clause of [ALTER SEQUENCE](#b01c09c114935817) statement. 
- &lt;basic sequence generator option&gt; 
    - It changes the property of the identity column. 
    - In SQL standard, it is defined to be described in the form of SET &lt;basic sequence generator option&gt;, but it can be omitted. 
    - For more information, refer to [ALTER SEQUENCE](#b01c09c114935817) statement.

<a id="1ada8dc13e68b74f"></a>
#### &lt;drop identity property clause&gt;

It drops the identity property of the column.  
The column should be the identity column.

<a id="53cce8b84a1abacc"></a>
### Description

SET NOT NULL clause requires the time for checking null in proportion to the number of table rows.

The following columns do not allow NULL values. In other words, even if DROP NOT NULL clause is performed, NULL is not allowed in the following cases.

- A column which includes NOT NULL constraint
- A column which is included in primary key constraint
- An identity column

The change of the default value using SET DEFAULT clause and the change of the identity property using &lt;alter identity column specification&gt; clause, is applied to INSERT or UPDATE statement which is performed later.

<a id="5502e29f9b06d5ad"></a>
### Examples

The following is an example of setting DEFAULT property to the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment SET DEFAULT 'N/A';

Table altered.
```

The following is an example of dropping DEFAULT property from the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment DROP DEFAULT;

Table altered.
```

The following is an example of setting NOT NULL constraint to the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey SET NOT NULL;

Table altered.
```

The following is an example of dropping the NOT NULL constraint from the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey DROP NOT NULL;

Table altered.
```

The following is an example of extending the data type size of the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_comment SET DATA TYPE VARCHAR(512);

Table altered.
```

The following is an example of restarting the next value of the identity column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey RESTART;

Table altered.
```

The following is an example of dropping the identity property from the column.

```
gSQL> ALTER TABLE region ALTER COLUMN r_regionkey DROP IDENTITY;

Table altered.
```

<a id="ddb2b5c4d4637d78"></a>
### Compatibility

**The SQL satndards compatibility**

<a id="e76204f03d42e393"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | X |
| F382 | Alter column data type | O |
| F383 | Set column not null clause | O |
| F384 | Drop identity property value | O |
| F385 | Drop column generation expression clause | X |
| F386 | Set identity column generation clause | O |
| S043 | Enhanced reference types | X |
| T174 | Identity columns | O |
| T178 | Identity columns: simple restart option | O |

<a id="7f2947f98f724b6e"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16)
- [ALTER TABLE name SET UNUSED COLUMN](#d1bfb6824c4855f9)
- [ALTER TABLE name RENAME COLUMN](#3cd0fd960aabac66)

<a id="3cd0fd960aabac66"></a>
## ALTER TABLE name RENAME COLUMN

<a id="6f0a76b26ba00528"></a>
### Function

It renames the table column.

<a id="a6274137841bad2f"></a>
### Syntax

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="d888c2df775a5c5d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename column statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="5c83db92da3fc2f9"></a>
### Syntax Rules and Parameters

<a id="e39068c3842d70ee"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="5a16756fc604056a"></a>
#### old_column_name

It is the old column name to be altered.

<a id="5763afa62247ecbe"></a>
#### new_column_name

It is the new column name to be altered.  
The same column name should not exist in a table.

<a id="bebcc1a817edfb7a"></a>
### Description

Even when the column name is altered it does not require the object change such as index, constraint which is generated based on the previous column.

<a id="6994f4e281e26d6c"></a>
### Example

The following is an example of exchanging the names of two columns, col_1 and col_2.

```
gSQL> ALTER TABLE t1 RENAME COLUMN col_1 TO col_temp;

Table altered.

gSQL> ALTER TABLE t1 RENAME COLUMN col_2 TO col_1;

Table altered.

gSQL> ALTER TABLE t1 RENAME COLUMN col_temp TO col_2;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="a527d138845da6ef"></a>
### Compatibility

The SQL standard does not define &lt;rename column statement&gt;.

<a id="f5ca06216120568f"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16)
- [ALTER TABLE name SET UNUSED COLUMN](#d1bfb6824c4855f9)
- [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b)

<a id="65400a8940d0436c"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="6c5bac53746d67b1"></a>
### Function

It adds a table constraint.

<a id="f62bc95009edb70f"></a>
### Syntax

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="07fd52330c2f28e7"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;add table constraint definition&gt; clause.

- One of the following privileges is required on the table to create the constraint.
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE

- One of the following privileges is required on the schema to create the constraint.
    - (ADD CONSTRAINT or CONTROL SCHEMA) ON SCHEMA for the schema
    - ALTER ANY TABLE ON DATABASE

- One of the following privileges is required for the tablespace in which the index is to be created to create the key constraint
    - CREATE OBJECT ON TABLESPACE for the tablespace
    - USAGE TABLESPACE ON DATABASE

- The owner of the created constraint is determined as follows.
    - The owner of the schema to which the constraint belongs. 
    - If the schema to which the constraint belongs is PUBLIC, then it is the user who executed the statement.

> Constraints of PRIMARY KEY, UNIQUE in a cluster system should include all sharding keys.

<a id="a479e03760473377"></a>
### Syntax Rules and Parameters

<a id="ab8b63c7d532c984"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="c2372be14281398d"></a>
#### &lt;table constraint definition&gt;

It defines the constraint to be added.  
NOT NULL constraint can not be added by using ALTER TABLE .. ADD CONSTRAINT statement, and it can be defined by using [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b) statement as follows.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

For more information, refer to [&lt;table constraint definition&gt;](#ea4e41ed20bb4738) clause of [CREATE TABLE](#72507f5467c281c9) statement.

<a id="115b75d9caedf1c9"></a>
### Description

When adding the key constraints such as primary key, unique key, the index is automatically created for them.

<a id="f893dae202089e20"></a>
### Examples

The following is an example of adding the primary key constraint to the table.

```
gSQL> ALTER TABLE t1 ADD PRIMARY KEY ( id );

Table altered.
```

The following is an example of specifying the constraint name when adding a primary key constraint to the table.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT t1_pk PRIMARY KEY ( id );

Table altered.
```

The following is an example of adding a DEFERRABLE constraint.

```
gSQL> ALTER TABLE t1 ADD CONSTRAINT t1_uk UNIQUE ( id ) DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="28ec10bba7dd6713"></a>
### Compatibility

**SQL standard compatibility**

<a id="1a7098db4caf47c5"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="8d0a4372f08bb8e4"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#72507f5467c281c9)
- [CREATE INDEX](#11cedda99c2339bc)
- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name DROP CONSTRAINT](#5f73b4ecf07ae833)

<a id="5f73b4ecf07ae833"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="56f8070844ac9329"></a>
### Function

It drops a table constraint.

<a id="1cb5a0db3c5b7f42"></a>
### Syntax

```
<drop table constraint definition> ::=
    ALTER TABLE table_name 
        DROP <constraint object>
        [ <drop behavior> ]
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] ) 

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="142f7f12bff77fc8"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table constraint definition&gt;.

- The owner of that constraint
- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="d1664a2b8f65a36d"></a>
### Syntax Rules and Parameters

<a id="59ad27fb5e2cf98b"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="0ceaf1df4077555d"></a>
#### CONSTRAINT constraint_name

It is the constraint name to be dropped.

<a id="3a61a3ddaf198f92"></a>
#### PRIMARY KEY

It is the primary key constraint for the table.

<a id="0139e06345f7cdbe"></a>
#### UNIQUE( column_name [, ...] )

It is the unique constraint for the columns.

<a id="3e31c7796892ecbb"></a>
#### &lt;drop behavior&gt;

When it is omitted, the default value is RESTRICT.  
Currently, RESTRICT/CASCADE is operated in the same way.

<a id="33c75bca4d25c247"></a>
### Description

[&lt;drop column not null clause&gt;](#0ccf23382f6334b2) of [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b) is used to drop NOT NULL constraint without using the constraint name.

<a id="fec0d186c816857e"></a>
### Examples

The following is an example of dropping a primary key constraint from the table.

```
gSQL> ALTER TABLE t1 DROP PRIMARY KEY;

Table altered.
```

The following is an example of dropping the table constraint by specifying the constraint name.

```
gSQL> ALTER TABLE t1 DROP CONSTRAINT t1_pk;

Table altered.
```

<a id="e1734cc737be98c7"></a>
### Compatibility

The SQL standard does not define the following clauses.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL standard compatibility**

<a id="d9bf0f5df2995ed6"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="8a705a6798fa770f"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name ADD CONSTRAINT](#65400a8940d0436c)
- [DROP INDEX](#9fbe418d2e4cd17c)

<a id="dbba103b11769053"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="547b0fc3fcc1e48f"></a>
### Function

It alters the characteristics of the table constraint.

<a id="59df0afecb4911e9"></a>
### Syntax

```
<alter table constraint definition> ::=
    ALTER TABLE table_name 
        ALTER <constraint object> <constraint characteristics>
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] ) 

<constraint characteristics> ::=
      [ NOT ] DEFERRABLE [ <constraint check time> ] 
    | <constraint check time> [ [ NOT ] DEFERRABLE ] 

<constraint check time> ::=
      INITIALLY DEFERRED 
    | INITIALLY IMMEDIATE
```

<a id="efe44c1a85e5605e"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table constraint definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

> Cluster does not support the deferrable constraints.

<a id="88b544aea37519a8"></a>
### Syntax Rules and Parameters

<a id="8e63ff8e832b7d59"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="f6a60542d2dcf6b1"></a>
#### &lt;constraint object&gt;

The constraint to be altered is specified as follows.

- CONSTRAINT constraint_name
    - The constraint name to be altered.
- PRIMARY KEY 
    - PRIMARY KEY constraint of the table
- UNIQUE( column [,...] ) 
    - UNIQUE constraint which satisfies the column list.

<a id="3767bfd32e966601"></a>
#### DEFERRABLE | NOT DEFERRABLE

It alters whether the constraint state is deferrable.

- DEFERRABLE
    - The constraint is altered to be deferrable. 
- NOT DEFERRABLE 
    - The constraint is altered not to be deferrable.

<a id="52e57ead5eb57d9e"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

It alters an initial value of the check point for the constraint.

- INITIALLY IMMEDIATE 
    - It checks the constraints at the time of DML.
- INITIALLY DEFERRED 
    - It checks the constraints at the time of COMMIT.

The constraints defined as NOT DEFERRABLE can not be altered to INITIALLY DEFERRED.

<a id="7d89a9a2a1c2c934"></a>
### Description

For more information about the deferrable constraints, refer to [SET CONSTRAINTS](#8337ae2c011b78f5).

<a id="783c56d7f7401104"></a>
### Example

The following is an example that the constraint t1_uk is set as deferrable and its checking time is set as DEFERRED.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="89c37ed626d1dacf"></a>
### Compatibility

The SQL standard does not define the following clauses.

- ALTER PRIMARY KEY clause
- ALTER UNIQUE(column [,...]) clause

**SQL standard compatibility**

<a id="cef5c098fe9a0d44"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="fdce17f8e7a2137b"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="fe4dc1e0693b195c"></a>
### Function

It renames the table constraints.

<a id="d0cb73533a08a18b"></a>
### Syntax

```
<rename table constraint statement> ::=
    ALTER TABLE table_name 
        RENAME <constraint object> TO new_constraint_name
    ;

<constraint object> ::=
      CONSTRAINT constraint_name
    | PRIMARY KEY 
    | UNIQUE ( column_name [, ...] )
```

<a id="2425a1db31d3ccf8"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename table constraint statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="43743e8e1e38614e"></a>
### Syntax Rules and Parameters

<a id="fe39478b6e7280f4"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="ffc31a754c597d48"></a>
#### &lt;constraint object&gt;

The existing name of the constraint to be altered is specified as follows.

- CONSTRAINT constraint_name
    - The constraint name to be altered
- PRIMARY KEY
    - PRIMARY KEY constraint of the table
- UNIQUE( column [,...] )
    - UNIQUE constraint which satisfies the column list

<a id="7250d414a83614c8"></a>
#### new_column_name

It is the new name of a constraint to be altered.

<a id="325b105fbabcf3bd"></a>
### Description

The index name which was automatically created with a key constraint such as primary key, unique key is not altered. Use [ALTER INDEX name RENAME TO](#1c016a1f45a446bc) statement to rename the index.

<a id="b488dfd1f8652216"></a>
### Examples

The following is an example of renaming the primary key constraint of the table.

```
gSQL> ALTER TABLE t1 RENAME PRIMARY KEY TO pk_t1;

Table altered.
```

The following is an example of renaming the table constraint by specifying the constraint name.

```
gSQL> ALTER TABLE t1 RENAME CONSTRAINT pk_t1 TO t1_pk;

Table altered.
```

<a id="52291eb29b6e3030"></a>
### Compatibility

The SQL standard does not define the &lt;rename table constraint statement&gt; statement.

<a id="ec624adf71f7c7df"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name ADD CONSTRAINT](#65400a8940d0436c)
- [ALTER TABLE name DROP CONSTRAINT](#5f73b4ecf07ae833)
- [ALTER TABLE name ALTER CONSTRAINT](#dbba103b11769053)

<a id="a391d93da4c7cda3"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="2dada7f50b16ca92"></a>
### Function

It creates a global secondary index in a table.

<a id="e88e082373df5911"></a>
### Syntax

```
<alter table add global secondary index definition> ::=
    ALTER TABLE table_name 
        ADD GLOBAL SECONDARY INDEX
        [ <index attributes> [...] ] [ TABLESPACE tablespace_name ]
    ;

<index attributes> ::=
      <physical attribute clause>
    | STORAGE ( <segment attr clause> [...] )
    | <logging clause> 
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

<logging clause> ::=
      LOGGING
    | NOLOGGING

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="3d772a73ba3620b9"></a>
### Invocation and Access Rules

&lt;alter table add global secondary index definition&gt; can be defined in a cluster system, and a user should satisfy the following conditions.

- At least one of the following privileges for a table in which the index is to be created is required.
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs.
    - ALTER ANY TABLE ON DATABASE

- At least one of the following privileges for a tablespace in which the index is to be created is required.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

<a id="8193b00343492cad"></a>
### Syntax Rules and Parameters

<a id="75d04a532c99d6ec"></a>
#### table_name

It is the name of a table in which the index is to be created.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="7213c711e19381c6"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of the index.

- PCTFREE integer 
    - Definition 
        - The reserved space to adjust the frequency of page splits caused by inserting the key in the page.
        - It is applied only when the index bottom-up build.
    - It can use of the value from 0 to 99.
    - If it is omitted, the value set in DEFAULT_INDEX_PCTFREE property is used by default.

- INITRANS integer 
    - Definition 
        - The initial number of transactions simultaneously accessing the page.
        - If the number of users accessing the index is small, then INITRANS is set low. If the number of users simultaneously accessing the index is big, then INITRANS is set high.
        - If necessary, it is automatically increased to the specified MAXTRANS.
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions simultaneously accessing the page.
    - It can use the value from 1 to 32. 
    - If it is omitted, the default value is 8.

<a id="ed0543e3652a34c1"></a>
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
    - If it is omitted, the default value is EXTENT size * 2147483647(The maximum positive integer of INT32).

<a id="be0f1530ae7312c0"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="128728cf802b17a0"></a>
#### LOGGING | NOLOGGING

It specifies whether to redo log the index.  
If it is omitted, the default value is NOLOGGING.

<a id="de4b70cf15c23a6f"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used when building an index.

- NOPARALLEL 
    - It does not build an index in parallel.
- PARALLEL [integer] 
    - It builds an index in parallel.
    - If an integer is omitted or set as 0, then it follows the property (INDEX_BUILD_PARALLEL_FACTOR). 
    - The minimum value of an integer is 0 and the maximum value is 16. 
    - If the property value is 0, then the system determines the optimal value.
- If it is omitted, the default value is PARALLEL.

<a id="7254c68e20ed942a"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be stored.

- If it specifies tablespace_name
    - The tablespace_name of LOGGING index should be a data tablespace. 
    - The tablespace_name of NOLOGGING index should be a temporary tablespace or a nologging tablespace.

- If it omits TABLESPACE clause
    - If INDEX TABLESPACE tablespace_name of USER is specified
        - The defined tablespace is used.
    - If INDEX TABLESPACE of USER is NULL
        - LOGGING index uses the user's default data tablespace.
        - NOLOGGING index uses the user's default temporary tablespace.

<a id="f9d5b13407daa7b8"></a>
### Description

A non-deterministic query requires the global secondary index. LOGGING index and NOLOGGING index have the following trade-offs.

- LOGGING index
    - Advantage: It does not separately build an index because the index is automatically restored by using the log when starting up the system.
    - Disadvantage: A disk I/O occurs because the changes on the index are recorded on the log when altering the row.
- NOLOGGING index
    - Advantage: A disk I/O does not occur for the changes on the index when altering the row.
    - Disadvantage: It automatically rebuilds the index when starting up the system because the log information of the index does not exist.

<a id="be7727776474841a"></a>
### Examples

The following is an example of adding a global secondary index to the table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a global secondary index with a  logging option on the tablespace USER_DATA_TBS of table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX LOGGING TABLESPACE USER_DATA_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a global secondary index with a nologging option on the tablespace USER_TEMP_TBS of table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX NOLOGGING TABLESPACE USER_TEMP_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="2639bbf1ece2f352"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="04366e74a53b67b6"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#099238b02dbd2f4d)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#8204dcffccd1aa15)
- [CREATE TABLE](#72507f5467c281c9)

<a id="099238b02dbd2f4d"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="296f4a091777cc35"></a>
### Function

It drops a global secondary index from the table.

<a id="5c635979fdc413e7"></a>
### Syntax

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="e36988d3cdce3bc3"></a>
### Invocation and Access Rules

&lt;alter table drop global secondary index definition&gt; statement can be defined in a cluster system, and the user should satisfy the following conditions.

- The following privilege for the table from which the index is to be dropped is required 
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE

<a id="481f73bd50223910"></a>
### Syntax Rules and Parameters

<a id="13d70aa5f541685e"></a>
#### table_name

It is the name of a table from which the index is to be dropped.

<a id="8888303dd8ef1e6d"></a>
### Description

A global secondary index is required to enquire a non-deterministic query.

<a id="0927ee9ad00a1182"></a>
### Examples

It drops a global secondary index from the table T1.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="fc1071b8bb02c6db"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="ed197903deb9466e"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#a391d93da4c7cda3)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#8204dcffccd1aa15)

<a id="8204dcffccd1aa15"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="4484e7cd2dbc21e7"></a>
### Function

It alters the physical attributes of the global secondary index in the table.

<a id="b28d548441b3c0a6"></a>
### Syntax

```
<alter table alter global secondary index storage statement> ::=
    ALTER TABLE table_name ALTER GLOBAL SECONDARY INDEX
      <physical attribute clause>
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

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
```

<a id="85c056479edea57a"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table alter global secondary index storage statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="d1d4d6497077f0ba"></a>
### Syntax Rules and Parameters

<a id="aa44831efb547223"></a>
#### table_name

It is the name of a table in which the index is to be created.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="717d511495ce1287"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of the index.

- PCTFREE integer 
    - Definition 
        - The reserved space to adjust the frequency of page splits caused by inserting the key in the page.
        - It is applied only when the index bottom-up build.
    - It can use of the value from 0 to 99.
    - If it is omitted, the value set in DEFAULT_INDEX_PCTFREE property is used by default.

- INITRANS integer 
    - Definition 
        - The initial number of transactions simultaneously accessing the page.
        - If the number of users accessing the index is small, then INITRANS is set low. If the number of users simultaneously accessing the index is big, then INITRANS is set high.
        - If necessary, it is automatically increased to the specified MAXTRANS.
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is 4.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions simultaneously accessing the page.
    - It can use the value from 1 to 32. 
    - If it is omitted, the default value is 8.

<a id="bf99ce0bb1925fca"></a>
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
    - If it is omitted, the default value is EXTENT size * 2147483647(The maximum positive integer of INT32).

<a id="c9bddc0601639b4a"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="cdcaedfe08aac1fe"></a>
### Description

A global secondary index is required to enquire a non-deterministic query.

<a id="24092d79949c88d6"></a>
### Examples

It alters the maximum available size to be used by a global secondary index in the table T1 to 100 MBytes.

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX STORAGE( MAXSIZE 100M );

Table altered.

gSQL> COMMIT;

Commit complete.
```

It alters the INITRANS value and the MAXTRANS value to 2 and 4 each which are to be used by a global secondary index in the table T1

```
gSQL> ALTER TABLE T1 ALTER GLOBAL SECONDARY INDEX INITRANS 2 MAXTRANS 4;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="5a4f3874356dc94f"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="9a89dd7665e0b6a5"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#a391d93da4c7cda3)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#099238b02dbd2f4d)

<a id="acf74aaf4961edaa"></a>
## ALTER TABLE name MOVE SHARD

<a id="e57f4836ebd4a872"></a>
### Function

It rebalances a specific shard of a table, or the entire shard in a specific cluster group to a specific cluster group.

<a id="cde432c16ebf9bd5"></a>
### Syntax

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ]
    ;
```

<a id="a15c9676e9d7b452"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table move shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="d187d18490754842"></a>
### Syntax Rules and Parameters

<a id="28bc125822803ce8"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster group specific table.

<a id="e264a08f5c870844"></a>
#### shard_name_list

It is the shard name list to be rebalanced.  
If the shard does not exist in that table, then the statement can not be performed.

<a id="a7174234d95e8511"></a>
#### src_cluster_group

It is the name of a specific cluster group to be rebalanced.

<a id="9e99c4e8f2cfc149"></a>
#### dest_cluster_group

It is the name of a target cluster group on which the shard of the table is to be rebalanced.  
If the shard of the table already exists in the specified cluster group, the statement cannot be performed.

<a id="78c065feb5743c6e"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="59679015b5383dc7"></a>
### Description

It rebalances a specific shard of the table from a specific cluster group to another cluster group.

To drop a specific cluster group, rebalance the shard of the table then  perform the [DROP CLUSTER GROUP](#7335700144f62a07) statement.

To move shards of all tables from a specific cluster group to another cluster group, then perform the ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP statement.

<a id="3ae8a3908e5c340b"></a>
### Examples

The following is an example of executing the &lt;alter table move shard statement&gt; statement.

```
gSQL> ALTER TABLE t1 MOVE SHARD shard1, shard2 TO CLUSTER GROUP g3;

Table altered.

gSQL> ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

Table altered.
```

<a id="069941039c83ced5"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="006a1381c80cd848"></a>
### For More Information

Refer to [ALTER DATABASE MOVE SHARD](#5e14870d019b823b).

<a id="467720ee446849be"></a>
## ALTER TABLE name REBALANCE

<a id="c945a3ab135b91ac"></a>
### Function

It rebalances the shard in a table.

<a id="0cdf745c003221c3"></a>
### Syntax

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE [ ONLINE | OFFLINE ]
    ;
```

<a id="dc68100a60547788"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rebalance statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="d25d6c0ddb3487aa"></a>
### Syntax Rules and Parameters

<a id="e676421fb1df93f6"></a>
#### table_name

It is the table name.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="a2a12abd7bf10f09"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="adba8988a13028b3"></a>
### Description

It does not rebalance shards in a table when adding a cluster member or a cluster group by using the following statements.

- [CREATE CLUSTER GROUP](#f8131b333b91edb7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0f86518c60487e59)

To rebalance the shards of a table in the added cluster group and the cluster member, perform the &lt;alter table rebalance statement&gt; statement. The operation succeeds without a separate rebalancing if the shard of the table is already rebalanced.

To rebalance shards in all tables, perform the [ALTER DATABASE REBALANCE](#6bf45492d225c752) statement.

<a id="bd0bfaac19f20590"></a>
### Examples

The following is an example of executing the &lt;alter table rebalance statement&gt; statement.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="5cbc0137994e4a5b"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="7591488dbf1f1cba"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="49627c47d885b078"></a>
### Function

It rebalances the shard of the table not to include a shard in a specific cluster group.

<a id="83f494c17af426e3"></a>
### Syntax

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list [ ONLINE | OFFLINE ]
    ;
```

<a id="8f0733d677cddb46"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rebalance exclude cluster group statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="be4a63a80f050df2"></a>
### Syntax Rules and Parameters

<a id="3a9593d1003e1f87"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster-wide table.

<a id="6669952891bcc55b"></a>
#### cluster_group_list

It is a list of the cluster group which does not include a shard of a table.  
If the cluster group to be excluded from the rebalancing is the entire group, the statement can not be performed.

<a id="8c242dc6360abaa2"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="3645d6629733c3fb"></a>
### Description

It excludes a specific cluster group and rebalances the shard of the table.  
If the shard of the table does not exist in that cluster group, the operation succeeds without a separate rebalancing.   
It rebalances the shard based on the cluster group in which the shard of the table is located.

To drop a specific cluster group, rebalance the shard of the table and perform  [DROP CLUSTER GROUP](#7335700144f62a07) statement.  
To rebalance the shard excluding a cluster group from all tables, perform the  [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#d73ac151e73a973a) statement.

<a id="d95db6364559b61a"></a>
### Examples

The following is an example of executing the &lt;alter table rebalance exclude cluster group statement&gt; statement.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="cbe21de23f369b8e"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="b959c469127f77b7"></a>
## ALTER TABLE name SPLIT SHARD

<a id="fd8455f2d6f0deeb"></a>
### Function

It rebalances a specific shard of a table by splitting it in a cluster environment.

<a id="8ea76d20a26fdd01"></a>
### Syntax

```
<alter table split shard statement> ::=
    ALTER TABLE table_name SPLIT SHARD source_shard_name
        INTO ( <split shard placement> [, ...] )
    ;

<split shard placement> ::=
    <split shard bound def> AT CLUSTER GROUP dest_group_name

<split shard bound def> ::=
    <split list shard def>
  | <split range shard def>

<split list shard def> :=
    SHARD dest_shard_name VALUES IN ( <split list value clause> )

<split list value clause> :=
    <split list value> [, ...]

<split list value> :=
    constant
  | NULL

<split range shard def> :=
    SHARD dest_shard_name VALUES LESS THAN ( <split range value clause> )

<split range value clause> :=
    <split range value> [, ...]

<split range value> :=
    constant
```

<a id="822c61b5de46775c"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table split shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="eea940733fd9e552"></a>
### Syntax Rules and Parameters

<a id="a77ffddce23d8200"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster group specific table, and when the shard is a list shard or a range shard.

<a id="50cf6f5ec115921d"></a>
#### source_shard_name

It is the name of an original shard to be split.   
If the shard does not exist in that table, the statement can not be performed.

<a id="830dc870338b273a"></a>
#### &lt;split shard placement&gt;

It defines the target shard to which the original shard is rebalanced by splitting.

<a id="58609f999f61fb2f"></a>
#### &lt;split shard bound def&gt;

It defines the bound of a target shard to be split.

It can be defined as one of two following bound defs.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="d994c4a10054cffd"></a>
##### &lt;split list shard def&gt;

It defines a split shard bound for a list shard.

- dest_shard_name
    - It is the name of a target shard.

- &lt;split list value clause&gt;
    - &lt;split list value&gt; should be an integer.
    - &lt;split list value&gt; can not be NULL.
    - &lt;split list value&gt; can not be DEFAULT.
    - S1 : ( 1, 11, 21, 31, NULL ) SPLIT SHARD S1 INTO ( &lt;split list value clause&gt; .. )
        - (O) SHARD S11 VALUES IN ( 1 )
        - (O) SHARD S11 VALUES IN ( 1, NULL ) 
        - (O) SHARD S11 VALUES IN ( 1, 11, 21, 31 ) 
        - (X) SHARD S11 VALUES IN ( 2 ) 
        - (X) SHARD S11 VALUES IN ( DEFAULT ) 
        - (X) SHARD S11 VALUES IN ( 1, 11, 21, 31, NULL )

<a id="b07ae42b47076402"></a>
##### &lt;split range shard def&gt;

It defines a split shard bound for a range shard.

- &lt;split range value clause&gt;
    - &lt;split list value&gt; should be an integer.
    - &lt;split list value&gt; can not be NULL.
    - &lt;split list value&gt; can not be MAXVALUE.
    - S1 : ( 100, 100 ), S2 : ( 50, 50 ) SPLIT SHARD S1 INTO ( &lt;split range value clause&gt; .. )
        - (O) SHARD S11 VALUES IN ( 50, 100 )
        - (O) SHARD S11 VALUES IN ( 100, 50 )
        - (O) SHARD S11 VALUES IN ( 60, 60 )
        - (X) SHARD S11 VALUES IN ( 50, NULL )
        - (X) SHARD S11 VALUES IN ( 50, 50 )
        - (X) SHARD S11 VALUES IN ( 100, 100 )
        - (X) SHARD S11 VALUES IN ( 100, 110 )
        - (X) SHARD S11 VALUES IN ( MAXVALUE, 100 )

<a id="c58d9f5d105c66b6"></a>
#### dest_group_name

It is the name of a cluster group in which the split shard is to be rebalanced.

<a id="79d91616671eb501"></a>
### Description

It splits a specific shard of a specific table and rebalances it to a random cluster group.  
This is used to distribute records and loads by splitting the shards when records corresponding to a specific shard is too much or when a specific group member is overloaded.

<a id="0325d06f2fd2d08f"></a>
### Examples

The following is an example of executing the &lt;alter table split shard statement&gt; statement.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="b501710e6fb285d6"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="a8fede8e3b14440f"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name REBALANCE](#467720ee446849be)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#7591488dbf1f1cba)
- [ALTER TABLE name MOVE SHARD](#acf74aaf4961edaa)

<a id="c7ea8d74ec6bdc02"></a>
## ALTER TABLE name RENAME SHARD

<a id="1264fb59176005f3"></a>
### Function

It renames a specific shard of a table in cluster environment.

<a id="39ccf31d8c13f67d"></a>
### Syntax

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="6c2b3c0e060bdb43"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rename shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="c5b618d59ffedf23"></a>
### Syntax Rules and Parameters

<a id="5f2cc9200c0ee58c"></a>
#### table_name

It is the table name to be altered.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="4f57611c79556604"></a>
#### shard_name

It is the existing name of a shard to be altered.  
If the shard does not exist in that table, then the statement can not be performed.

<a id="f5f7a197b23f6bbc"></a>
#### new_shard_name

It is the new name of a shard to be altered.   
The same shard name should not exist in the table.

<a id="1be798ea162b62ee"></a>
### Description

It alters the name of a specific shard of a hash, a range, or a list table. This statement can not be performed for a cloned table.

<a id="80b5a684bd200c85"></a>
### Examples

The following is an example of executing &lt;alter table rename shard statement&gt; statement.

```
gSQL> ALTER TABLE t_range RENAME SHARD r_01 TO r_new_01;

Table altered.

gSQL> ALTER TABLE t_list RENAME SHARD l_01 TO l_new_01;

Table altered.

gSQL> ALTER TABLE t_hash RENAME SHARD shard_000000 TO h_new_00;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="02d8a8e9d1b8db84"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="f90b577445bd5df7"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#90e40a320994005d)
- [ALTER TABLE name MOVE SHARD](#acf74aaf4961edaa)
- [ALTER TABLE name SPLIT SHARD](#b959c469127f77b7)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="7ec007f109a6e713"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="f11e3713ce3ca22b"></a>
### Function

It sets READ { ONLY | WRITE } in a table.

<a id="60174139499c2dfc"></a>
### Syntax

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="3767e6ff0173db43"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table read { only | write } statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="929aa7c4d7f169b9"></a>
### Syntax Rules and Parameters

<a id="1f5f4c11e218ada8"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="54c925bfe926a991"></a>
### Description

It sets table property to READ { ONLY | WRITE }.

If it is set to READ ONLY, neither SELECT .. FOR UPDATE statement, nor DML/ DDL statement which updates table data can be used. However, DDL statement which does not update the table data is allowed.

> Disallowed SQL statements when it is set to READ ONLY  
> • INSERT, UPDATE, DELETE  
> • TRUNCATE  
> • SELECT .. FOR UPDATE  
> • ALTER TABLE RENAME/DROP COLUMN  
> • ALTER TABLE SET COLUMN UNUSED  
>   
> Allowed SQL statements when it is set to READ ONLY  
> • SELECT  
> • CREATE/ALTER/DROP INDEX  
> • ALTER TABLE ADD/ALTER COLUMN  
> • ALTER TABLE ADD/ALTER/RENAME/DROP CONSTRAINT  
> • ALTER TABLE for physical property changes  
> • ALTER TABLE DROP UNUSED COLUMNS  
> • ALTER TABLE RENAME TO  
> • DROP TABLE  
> • ALTER TABLE ADD/DROP SUPPLEMENTAL LOG  
> • LOCK TABLE

<a id="77a1f2ade4ecdbe2"></a>
### Examples

The following is an example of executing &lt;alter table read { only | write } statement&gt;.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="4e3680669c1365a9"></a>
### Compatibility

The SQL standard does not define &lt;alter table read { only | write } statement&gt;.

<a id="d00751d23541b83e"></a>
### For More Information

Refer to [ALTER TABLE](#90e40a320994005d).

<a id="49b7a9e000ac5b20"></a>
## ALTER TABLE name RENAME TO

<a id="c62ea94a898665a9"></a>
### Function

It renames the table.

<a id="08f463cbdd1108df"></a>
### Syntax

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="33088d5b23cf9994"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename table statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="2168b4b6bbcefa0d"></a>
### Syntax Rules and Parameters

<a id="8028e50819967d4b"></a>
#### table_name

It is the existing name of the table.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="ad04e290791d0521"></a>
#### new_table_name

It is a new name of the table.  
The same table name should not exist in the schema.

<a id="a5218642f2d92e03"></a>
### Description

Even when the table is renamed, the object referring to the table such as index, constraint does not need to be renamed.

<a id="d80595e070518d13"></a>
### Example

The following is an example of exchanging the name of the two tables t1, t2.

```
gSQL> ALTER TABLE t1 RENAME TO t_temp;

Table altered.

gSQL> ALTER TABLE t2 RENAME TO t1;

Table altered.

gSQL> ALTER TABLE t_temp RENAME TO t2;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="8fccace9a3c18334"></a>
### Compatibility

The SQL standard does not define &lt;rename table statement&gt;.

<a id="a5be0527da0ccb71"></a>
### For More Information

Refer to [ALTER TABLE](#90e40a320994005d).

<a id="4dd7d18d5dcf2174"></a>
## ALTER TABLE name STORAGE

<a id="30c336ce7d099762"></a>
### Function

It alters physical attributes of a table.

<a id="13bc25cf60392079"></a>
### Syntax

```
<alter table physical attribute statement> ::=
    ALTER TABLE table_name 
      [ <physical attribute clause> ]
    | [ STORAGE ( <segment attr clause> [...] ) ]
    ;

<physical attribute clause> ::=
      PCTFREE integer
    | PCTUSED integer
    | INITRANS integer
    | MAXTRANS integer

<segment attr clause> ::=
    NEXT <size_clause>
    | MINSIZE <size_clause>
    | MAXSIZE <size_clause>

<size clause> ::=
      integer [ K | M | G | T ]
```

<a id="972b1ff1cc80893f"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table physical attribute statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="0a543d54b20d884d"></a>
### Syntax Rules and Parameters

<a id="ad516de2335c6ac2"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="d71cc632ea5278dd"></a>
#### &lt;physical attribute clause&gt;

It alters the physical attribute of a page which configures the table.  
It is not applied to the already allocated page, but is applied to the newly allocated page.  
For more information, refer to [&lt;table physical attribute clause&gt;](#1861b0eebcd90804) of [CREATE TABLE](#72507f5467c281c9).

<a id="dfb26673c2addd64"></a>
#### &lt;segment attr clause&gt;

It alters the physical attribute of the extent configuring the segment. It is not applied to the already allocated extent but is applied to the newly allocated extent.

- MAXSIZE integer 
    - It alters the space size of the segment which can be allocated.
    - If the newly allocated space is smaller than the already allocated space, the MAXSIZE is altered to the currently allocated space size.

<a id="00039cde3e69278a"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="37c36c589020ada3"></a>
### Example

The following is an example of changing the physical attribute of the table.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="7aa6df8706c425c2"></a>
### Compatibility

The SQL standard does not define the physical attribute of a table.

<a id="bf5ec636c0c31cac"></a>
### For More Information

Refer to [ALTER TABLE](#90e40a320994005d).

<a id="057d2a978c3e044c"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="674adaa7a4440934"></a>
### Function

If the primary key exists in the table when table data is altered, it sets to add the primary key value to redo log.

<a id="d5f9b88ad32483e3"></a>
### Syntax

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="dd723c7d1c765dfb"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;add table supplemental log statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="946c95b68a8be2bd"></a>
### Syntax Rules and Parameters

<a id="35e1b2021f6419b8"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

Even when the primary key does not exist in the table, the statement can be executed.

<a id="27fe712c7b411c95"></a>
### Description

It additionally records SUPPLEMENTAL LOG when executing UPDATE/DELETE on the corresponding TABLE. The recorded SUPPLEMENTAL LOG is used to analyze logs or tools such as CDC.

To record SUPPLEMENTAL LOG of every TABLE, set the property as *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES*.

<a id="925d4d6ee0530d17"></a>
### Example

The following is an example of setting to additionally add a primary key value to the redo log when changing the data in the table.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="061016c3ac91cedd"></a>
### Compatibility

The SQL standard does not cover &lt;add table supplemental log statement&gt;.

<a id="1ffad164d686817d"></a>
### For More Information

Refer to [ALTER TABLE name DROP SUPPLEMENTAL LOG](#1fe2b729e647576f).

<a id="1fe2b729e647576f"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="8398aaaf27b00aa7"></a>
### Function

It sets not to leave the primary key information on the redo log when changing the data in the table.

<a id="2be8dba5aaace2c1"></a>
### Syntax

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="fd84942a2d979b92"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table supplemental log statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="31fd13d92bd99103"></a>
### Syntax Rules and Parameters

<a id="aea1877da2d180d9"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
It should have been set by using [ALTER TABLE name ADD SUPPLEMENTAL LOG](#057d2a978c3e044c) statement.

<a id="07775cc2f8c9ee65"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="028e3ed5bb399ff5"></a>
### Example

The following is an example of setting not to leave the primary key information on the redo log when changing the data in the table.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="701de8cd2c59423d"></a>
### Compatibility

The SQL standard does not cover &lt;drop table supplemental log statement&gt;.

<a id="fb4ccb735469fcaa"></a>
## ALTER TABLESPACE

<a id="3a7993cd2a4670b1"></a>
### Function

It alters the tablespace definition.

<a id="b3736058dc6a7f11"></a>
### Syntax

```
<alter tablespace statement> ::=
      <rename tablespace statement>
    | <backup tablespace statement>
    | <on/offline tablespace statement>
    | <add file statement>
    | <drop file statement>
    | <rename datafile statement>
    ;
```

<a id="dc7316a6eddbcaed"></a>
### Invocation and Access Rules

ALTER TABLESPACE privilege is required to perform &lt;alter tablespace statement&gt;.

<a id="481bf6494a8a6088"></a>
### Syntax Rules and Parameters

<a id="720847ccfcd96cfc"></a>
#### &lt;rename tablespace statement&gt;

It renames the tablespace.  
For more information, refer to [ALTER TABLESPACE name RENAME TO](#c983eeb63ef48220) statement.

<a id="f36c309b8e76d15f"></a>
#### &lt;backup tablespace statement&gt;

It backs up the tablespace.  
For more information, refer to [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec) statement.

<a id="b8f0e7e42a555ad1"></a>
#### &lt;on-offline tablespace statement&gt;

It changes all files in the tablespace to the online state or offline state.  
For more information, refer to [ALTER TABLESPACE name [ONLINE|OFFLINE]](#4e161d8fc4785fea) statement.

<a id="9460ee0511d044eb"></a>
#### &lt;add file statement&gt;

It adds a file to the tablespace.  
For more information, refer to [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#07af513836ecc0d6) statement.

<a id="0c1bd0127c60caa3"></a>
#### &lt;drop file statement&gt;

It drops a file from the tablespace.  
For more information, refer to [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#1a3749fb33ec627a) statement.

<a id="a6e8c98f08258f1e"></a>
#### &lt;rename datafile statement&gt;

It renames the datafile in the data tablespace.   
For more information, refer to [ALTER TABLESPACE name RENAME DATAFILE](#8b0b8578d9225bfe) statement.

<a id="db0502d0ed864ec9"></a>
### Description

Unlike other Data Definition Language (DDL), ALTER TABLESPACE statement is not allowed to ROLLBACK, and its transaction is automatically committed after executing the statement.

<a id="50d700842ddfde2e"></a>
### Example

Refer to the examples of each detailed statement.

<a id="0ae8db178af662d3"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="fc01c5ad4663fc43"></a>
### For More Information

Refer to the followings.

- [CREATE TABLESPACE](#4fb45716ef9fbe7b)
- [DROP TABLESPACE](#ee3406f353c996e6)

<a id="c983eeb63ef48220"></a>
## ALTER TABLESPACE name RENAME TO

<a id="83c0408c9e109c51"></a>
### Function

It renames the tablespace.

<a id="58ab79bb9cc5d165"></a>
### Syntax

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="bfd10ef11dfc30cc"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege required to perform &lt;rename space statement&gt;.

<a id="d6eaf175ce1bfb5a"></a>
### Syntax Rules and Parameters

<a id="c4215ac38c155caa"></a>
#### tablespace_name

It is a name of the old tablespace.

- The built-in tablespace can not be renamed.
- The OFFLINE tablespace can not be renamed.

<a id="ed2a34b2c5b6d3e3"></a>
#### new_tablespace_name

It is a name of the new tablespace.

<a id="24a861a840511a62"></a>
### Description

Even when the tablespace is renamed, the table or index which was already created in the existing tablespace does not need to be renamed.

<a id="758eb4d2e0915b6d"></a>
### Example

The following is an example of renaming the tablespace.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="85486b074bafaeff"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="11246906ad83d50e"></a>
### For More Information

Refer to [ALTER TABLESPACE](#fb4ccb735469fcaa).

<a id="d42abe0527e5ecec"></a>
## ALTER TABLESPACE name BACKUP

<a id="788648db94f27213"></a>
### Function

It switches the tablespace to backup enabled state and backup disabled state to perform backup.

<a id="6d5d8c4cdfb43f97"></a>
### Syntax

```
<backup tablespace statement> ::=
      <tablespace begin backup statement>
    | <tablespace end backup statement>
    | <tablespace incremental backup statement>    
    ;

<tablespace begin backup statement> ::=
    ALTER TABLESPACE tablespace_name BEGIN BACKUP [AT <domain_name>]
    ;

<tablespace end backup statement> ::=
    ALTER TABLESPACE tablespace_name END BACKUP [AT <domain_name>]
    ;

<tablesapce incremental backup statement> ::=
    ALTER TABLESPACE tablespace_name
        BACKUP INCREMENTAL <incremental backup option> [AT <domain_name>]    ;

<incremental backup option> ::=
      LEVEL integer [ CUMULATIVE | DIFFERENTIAL ]
```

<a id="ad3a904e898da47f"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;backup space statement&gt;.

<a id="ea7c98eb0a68c3c5"></a>
### Syntax Rules and Parameters

<a id="06a1140545879076"></a>
#### &lt;tablespace begin backup statement&gt;

It sets the tablespace to the backup enabled state.

- The tablespace being used is set to the backup enabled state.
- The backup state of the tablespace such as OFFLINE/ temporary can not be switched.

<a id="1364f617323aeab2"></a>
#### tablespace_name

It is the tablespace name whose backup state is to be switched.

<a id="a124d1239f9d9a19"></a>
#### &lt;tablespace end backup statement&gt;

It sets the tablespace to the backup disabled state.

<a id="ec1ab471caebc088"></a>
#### &lt;tablesapce incremental backup statement&gt;

It performs the incremental backup of the tablespace.  
The database is in OPEN phase and it should be operated in ARCHIVELOG mode.

<a id="6f425724a14cf6c9"></a>
#### &lt;incremental backup option&gt;

- An 'Integer' can be specified from 0 to 4. 
- 'LEVEL 0' can not specify CUMULATIVE or DIFFERENTIAL.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n-1. 
    - DIFFERENTIAL
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n.
    - If it is omitted, DIFFERENTIAL is specified by default.

<a id="cf4f92cac1e8ec6b"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="e84425cefcf0a41f"></a>
### Description

It backs up the datafiles which are created in the tablespace. A full backup of the tablespace begins with BEGIN BACKUP, and copies the datafiles by OS file copy and ends with END BACKUP. The incremental backup file is created in the path set by BACKUP_DIR 1 property using a single statement.

<a id="9da67504d7821168"></a>
### Examples

The following is an example of setting the full backup state to 'ACTIVE' for the tablespace DICTIONARY_TBS.

```
ALTER TABLESPACE DICTIONARY_TBS BEGIN BACKUP;
```

The following is an example of setting the full backup state to 'INACTIVE' for the tablespace DICTIONARY_TBS.

```
ALTER TABLESPACE DICTIONARY_TBS END BACKUP;
```

The following is an example of generating the LEVEL 0 incremental backup of the tablespace DICTIONARY_TBS.

```
ALTER TABLESPACE DICTIONARY_TBS BACKUP INCREMENTAL LEVEL 0;
```

<a id="a2b315617d63d21a"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="65db871eaba50c87"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#4e161d8fc4785fea)

<a id="4e161d8fc4785fea"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="b87d3f0da8977ace"></a>
### Function

It alters the tablespace status.

<a id="183007d9e88b80ae"></a>
### Syntax

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="a4552800359b458f"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;on/off tablespace statement&gt;.

<a id="5a23d415fee8f19b"></a>
### Syntax Rules and Parameters

<a id="b1e5e6ef8797b707"></a>
#### ONLINE

It alters the tablespace status in OFFLINE state to ONLINE state.

<a id="0940f319ca56b21d"></a>
#### OFFLINE NORMAL

It alters the tablespace status in ONLINE state to OFFLINE state.

The media recovery is not required in ONLINE state because the tablespace which was altered to OFFLINE state is in consistent state.

> OFFLINE NORMAL is not allowed in MOUNT phase.  
> (However, if the previous instance is terminated by `\`SHUTDOWN NORMAL, OFFLINE NORMAL is allowed.)

<a id="072623842359f1ac"></a>
#### OFFLINE IMMEDIATE

It alters the tablespace status in ONLINE state to OFFLINE state.

The media recovery is required in ONLINE state because the tablespace which was altered to OFFLINE state is in inconsistent state.

> The SYSTEM tablespace can not be altered to OFFLINE state.   
> OFFLINE IMMEDIATE requires the media recovery, so it can be performed only in ARCHIVELOG mode.

<a id="4283b3729f05cf52"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="0c31df333dc972e4"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="9e71940a366cb561"></a>
### Examples

The following is an example of setting the tablespace to OFFLINE.

```
gSQL> ALTER TABLESPACE space1 OFFLINE;

Tablespace altered.
```

The following is an example of that OFFLINE NORMAL for the tablespace fails in MOUNT phase.

```
gSQL> ALTER TABLESPACE space1 OFFLINE;

ERR-42000(16290): OFFLINE NORMAL is only allowed if the database is in OPEN phase : 
ALTER TABLESPACE space1 OFFLINE
                 *
ERROR at line 1:

gSQL> ALTER TABLESPACE space1 OFFLINE NORMAL;

ERR-42000(16290): OFFLINE NORMAL is only allowed if the database is in OPEN phase : 
ALTER TABLESPACE space1 OFFLINE NORMAL
                 *
ERROR at line 1:
```

<a id="9b7f46bccf0adc7f"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="bd7fc139e24dfcd1"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- [ALTER TABLESPACE name BACKUP](#d42abe0527e5ecec)

<a id="07af513836ecc0d6"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="3327dc840107818d"></a>
### Function

It extends the space of the tablespace.

<a id="1c4a81a19bd30d92"></a>
### Syntax

```
<add space statement> ::=
    ALTER TABLESPACE tablespace_name ADD <space specification>
        [AT <domain name>]
    ;

<space specification> ::=
      MEMORY <memory clause> [, ...]
    | DATAFILE <add datafile clause> [, ...]

<size clause> ::=
    integer [ K | M | G | T ]

<memory clause> 
     'memory_name' { SIZE <size clause> }

<add datafile clause> ::=
     'filename' 
        { SIZE <size clause> | REUSE | SIZE <size clause> REUSE }
```

<a id="91d2d38a2dd91694"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;add space statement&gt;.

<a id="4744107dc47b782c"></a>
### Syntax Rules and Parameters

<a id="d031d3c052eb2437"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="cea826aa844db429"></a>
#### &lt;file specification&gt;

The following syntax should be used according to the tablespace type.

- Memory data tablespace
    - DATAFILE &lt;add datafile clause&gt;
- Memory temporary tablespace
    - MEMORY &lt;memory clause&gt;

<a id="c3ac5d96ebcf90ad"></a>
#### &lt;add datafile clause&gt;

It defines the memory datafile to be added.

- 'filename' 
    - It is the file name to store and manage the data.
    - It is the space to store the checkpoint image for the memory data. 
    - The filename can be either the new file or existing file. 
    - The length of filename should be shorter than 1024 bytes.

- SIZE &lt;size clause&gt; 
    - For the new file, the initial size is specified by using SIZE clause.
    - An error occurs if the file exists.
    - The file size can be specified from 1M to 30G.

- REUSE 
    - If the file exists, it uses REUSE clause.
    - If the file does not exist, a new file is created. 
    - The size of newly created file 
        - For the data tablespace, it is determined by MEMORY_DATA_TABLESPACE_SIZE property.
        - For the temporary table space, it is determined by MEMORY_TEMP_TABLESPACE_SIZE property.

- SIZE &lt;size clause&gt; REUSE 
    - If both of SIZE clause and REUSE clause are specified, it is operated as follows based on the presence of the filename.
        - For the new filename, the initial file size is specified by using SIZE clause.
        - For the existing filename, it is adjusted to the SIZE clause value by using the existing file.

<a id="4e457411d0d07e14"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - It defines the memory to be added.

For more information, refer to  [&lt;memory clause&gt;](#4781565a80069d9a) of [CREATE MEMORY TEMPORARY TABLESPACE](#3ddf803b50db6f27) statement.

<a id="7d48f3854cf101a7"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="529443828a98f04b"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="e61fadcfae6fdc28"></a>
### Example

The following is an example of adding datafile to the tablespace.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="ea44120f9dffbc90"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="706c3360ab7a0af5"></a>
### For More Information

Refer to the followings.

- [CREATE MEMORY DATA TABLESPACE](#b0ee56c9e33dadf5)
- [CREATE MEMORY TEMPORARY TABLESPACE](#3ddf803b50db6f27)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)

<a id="1a3749fb33ec627a"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="414db54747eaf231"></a>
### Function

It reduces the space of the tablespace.

<a id="2c3bef2a37dd18bb"></a>
### Syntax

```
<drop space statement> ::=
    ALTER TABLESPACE tablespace_name DROP <file specification>
    [ AT <domain name> ]
    ;

<file specification> ::=
      DATAFILE 'filename' 
    | MEMORY 'memory_name'
```

<a id="0c34a46c81f1a226"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;drop space statement&gt;.

<a id="f61a00337bb9bc27"></a>
### Syntax Rules and Parameters

<a id="c2affb06caedf385"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="0d9adc1d13f1de22"></a>
#### &lt;file specification&gt;

The following syntax should be used according to the tablespace type.

- Memory data tablespace
    - DATAFILE 'filename' 
- Memory temporary tablespace
    - MEMORY 'memory_name'

> The file of OFFLINE tablespace can not be dropped.   
> The first file of the tablespace can not be dropped.   
> The data file which has been used once can not be dropped.

<a id="d4a687237a023fdd"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="44888142b9af93e5"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="05c40c28e021e24e"></a>
### Example

The following is an example of dropping the file from the tablespace.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="b221101bfd07af90"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="4603e58bc5e7ef87"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#07af513836ecc0d6)
- [ALTER TABLESPACE name RENAME DATAFILE](#8b0b8578d9225bfe)

<a id="8b0b8578d9225bfe"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="fb405e68deccbe63"></a>
### Function

It renames the datafiles that configure the tablespace.

<a id="f37e8afe12f13fc0"></a>
### Syntax

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [, ...]
```

<a id="779121672d2e8604"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;rename datafile statement&gt;.

> ONLINE tablespace file can not be altered when it is in TDS mode and the database is in OPEN phase. (Except for the temporary memory tablespace.)   
> The file should exist even after the alteration.

<a id="10f688eda345b580"></a>
### Syntax Rules and Parameters

<a id="23964900b7d94bbb"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="2bd2048cb973c47b"></a>
#### 'filename'

The memory temporary tablespace is 'memory_name' and the other kinds of tablespace is 'filename'.

<a id="164c7f4cc4631868"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="ef35997c5290a3af"></a>
### Description

The tablespace status determines whether the operation can be performed.

- OFFLINE: It can be performed in MOUNT or OPEN phase.
- ONLINE: It can be performed only in MOUNT phase.

<a id="c19bfd7cf084233a"></a>
### Example

The following is an example of renaming 'test.dbf' to 'test1.dbf'.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="c9ef4a10e81f19b0"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="79f093e72e8a8bd9"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#07af513836ecc0d6)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#1a3749fb33ec627a)

<a id="ed40a6862d9c8f12"></a>
## ALTER USER

<a id="ecaabfb5bac637c4"></a>
### Function

It alters the user definition of the database.

<a id="9e56eb0a728c2157"></a>
### Syntax

```
<alter user statement> ::=
      ALTER USER user_identifier <alter user action>
    | ALTER USER PUBLIC <alter schema path>
    ;

<alter user action> ::=
      <alter password>
    | <alter profile>
    | <password expire>
    | <account lock>
    | <alter default tablespace>
    | <alter temporary tablespace>
    | <alter schema path>

<alter password> ::=
    IDENTIFIED BY new_password [ REPLACE old_password ]

<alter profile> ::=
    PROFILE { profile_name | DEFAULT | NULL }

<password expire> ::=
    PASSWORD EXPIRE

<account lock> ::=
    ACCOUNT { LOCK | UNLOCK }

<alter default tablespace> ::=
    DEFAULT TABLESPACE tablespace_name

<alter temporary tablespace> ::=
    TEMPORARY TABLESPACE tablespace_name

<alter schema path> ::=
    SCHEMA PATH ( { schema_name | CURRENT PATH } [, ...] )
```

<a id="d0ce3901e62550e2"></a>
### Invocation and Access Rules

ALTER USER ON DATABASE privilege is required to perform &lt;alter user statement&gt;.  
However, &lt;alter password&gt; can be performed without any privilege, when the user and user_identifier are identical.

<a id="0b8b296e36bbda40"></a>
### Syntax Rules and Parameters

<a id="6985b68a7be98abe"></a>
#### user_identifier

It is the username to be altered.

<a id="f96f3b8cdb636662"></a>
#### &lt;alter password&gt;

It alters the user's password.

- IDENTIFIED BY new_password 
    - The new password is encrypted and stored. 
    - The length of the password should be shorter than 128 bytes. 
    - The password is case sensitive.

- REPLACE old_password 
    - It can be omitted when ALTER USER ON DATABASE privilege is given.
    - It can not be omitted when ALTER USER ON DATABASE privilege is not given.
        - The user and the user_identifier should be identical.

<a id="156744f4b5848b09"></a>
#### &lt;alter profile&gt;

It alters the profile for the password management policy.

- PROFILE profile_name
    - It allocates profile_name which is created by a user.
- PROFILE DEFAULT
    - It allocates "DEFAULT" which is the default profile.
- PROFILE NULL
    - It does not allocate the profile.

<a id="db8e685005192e32"></a>
#### &lt;password expire&gt;

It expires the user's password.

<a id="47d6c79949f4f046"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - It locks the user account. 
- ACCOUNT UNLOCK
    - It unlocks the user account.

<a id="5e8109f98dd5c993"></a>
#### &lt;alter default tablespace&gt;

It alters the user's default tablespace.  
The tablespace_name should be a data tablespace.

<a id="42b443eedc823bf4"></a>
#### &lt;alter temporary tablespace&gt;

It alters the user's temporary tablespace.  
The tablespace_name should be a temporary tablespace.

<a id="ca9cb1af1a3f31ff"></a>
#### &lt;alter index tablespace&gt;

It alters an index tablespace of the user.

- It specifies INDEX TABLESPACE tablespace_name.
    - If the data tablespace is specified, then it should be a LOGGING index.
    - If the temporary tablespace is specified, then it should be a NOLOGGING index.
- INDEX TABLESPACE NULL
    - It does not specify an index tablespace.

<a id="923e7963d4a49bea"></a>
#### &lt;alter schema path&gt;

It alters the user's schema access path.  
If the schema is not specified in user's SQL statement, the schema access path is determined in the schema order for the naming resolution of the object.

If the schema name is as same as another schema which is previously listed, it is not applied.

The following is an example of objects existing in a schema when performing *ALTER USER u1 SCHEMA PATH ( u1, s2, public );*  statement.

<a id="8cbb94ce4b29edd8"></a>
| Schema name | u1 | s2 | public |
| --- | --- | --- | --- |
| - | t1 | - | t1 |
| - | - | t2 | - |
| - | - | - | t3 |

The object name whose schema name is not specified when the user u1 executes the schema is interpreted by the SCHEMA PATH as follows.

- CREATE statement 
    - CREATE TABLE t1 ( c1 INTEGER ); 
        - Error: CREATE TABLE u1.t1 ( c1 INTEGER ); 
    - CREATE TABLE t2 ( c1 INTEGER ); 
        - Execution: CREATE TABLE u1.t2 ( c1 INTEGER );

- SELECT statement
    - SELECT * FROM t1; 
        - Execution: SELECT * FROM u1.t1; 
    - SELECT * FROM t2; 
        - Execution: SELECT * FROM s2.t2; 
    - SELECT * FROM t3; 
        - Execution: SELECT * FROM public.t3;

<a id="0e2a3e1d8303bd3f"></a>
#### CURRENT PATH

It is the current user's schema path.

A new schema path can be added using CURRENT PATH maintaining the existing schema path as follows.

- The u1's current schema path 
    - (u1, public) 
- The statement execution
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- The u1's schema path is altered as follows.
    - (s1, u1, public, s2)

<a id="ce3af2117c4a911c"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

It alters the schema path of PUBLIC account.  
The schema path of PUBLIC account is included in every user's schema path.

The initial schema path which is allocated to PUBLIC account is as follows.

- DICTIONARY_SCHEMA
- INFORMATION_SCHEMA
- DEFINITION_SCHEMA
- PERFORMANCE_VIEW_SCHEMA
- FIXED_TABLE_SCHEMA

<a id="631b0c0edb8b9fc9"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="7b97707d252dbde0"></a>
### Examples

The following is an example of altering the user's password.

```
gSQL> ALTER USER u1 IDENTIFIED BY new_password;

User altered.
```

The following is an example of allocating the profile to the user.

```
gSQL> ALTER USER u1 PROFILE prof1;

User altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of dropping the user's profile.

```
gSQL> ALTER USER u1 PROFILE NULL;

User altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of expiring the user's password.

```
gSQL> ALTER USER u1 PASSWORD EXPIRE;

User altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of unlocking the user's account.

```
gSQL> ALTER USER u1 ACCOUNT UNLOCK;

User altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of altering the user's DEFAULT TABLESPACE.

```
gSQL> ALTER USER u1 DEFAULT TABLESPACE mem_data_tbs;

User altered.
```

The following is an example of altering the user's TEMPORARY TABLESPACE.

```
gSQL> ALTER USER u1 TEMPORARY TABLESPACE mem_temp_tbs;

User altered.
```

The following is an example of altering the user's INDEX TABLESPACE.

```
gSQL> ALTER USER u1 INDEX TABLESPACE mem_temp_tbs;

User altered.
```

The following is an example of altering the user's schema path.

```
gSQL> ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH );

User altered.
```

<a id="5e9e56e067da83d5"></a>
### Compatibility

SQL standard covers the concepts of a user, but it does not define the SQL statements associated with creating, altering, dropping a user.

<a id="5bd2afc72b277659"></a>
### For More Information

Refer to the followings.

- [CREATE USER](#524780362f90ebc8)
- [DROP USER](#75a505d0fbae98f3)

<a id="062be61ee2ec0848"></a>
## ALTER VIEW

<a id="be2920615433d2bf"></a>
### Function

It alters the view definition.

<a id="1ec6837f975f840d"></a>
### Syntax

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="3680e1fe1c3fd8c9"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter view statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for the view
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
- ALTER ANY TABLE ON DATABASE

<a id="8c2358b23659d6c2"></a>
### Syntax Rules and Parameters

<a id="ee5813d9f53db22a"></a>
#### view_name

It is the view name to be altered.  
It can define the schema to which the view belongs, such as schema_name.view_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="c698b2de1a154818"></a>
#### COMPILE

It compiles the view again.  
COMMENT which is given to the view column is initialized.

<a id="cddbb648268e84a8"></a>
### Description

When the table or the view which is referenced by the view is altered or dropped, then it affects that view.

This information can be retrieved from INFORMATION_SCHEMA.VIEWS.

- IS_COMPILED column
    - TRUE: The view was successfully created. 
    - FALSE: The view was created with FORCE option when an error exists.

- IS_AFFECTED column
    - TRUE: The table and the view which was referenced by the view was altered.
    - FALSE: After creation and compilation of a view, the table and the view which was referenced by the view was not altered.

<a id="328e32a51d1379da"></a>
### Example

The following is an example of compiling the view which is affected by the table change referenced by that view.

```
gSQL> SELECT TABLE_NAME, IS_AFFECTED 
        FROM INFORMATION_SCHEMA.VIEWS 
       WHERE TABLE_SCHEMA = 'PUBLIC'
         AND TABLE_NAME = 'V1';

TABLE_NAME IS_AFFECTED
---------- -----------
V1         TRUE       

1 row selected.


gSQL> ALTER VIEW v1 COMPILE;

View altered.

COMMIT;

Commit complete.

gSQL> SELECT TABLE_NAME, IS_AFFECTED 
        FROM INFORMATION_SCHEMA.VIEWS 
       WHERE TABLE_SCHEMA = 'PUBLIC'
         AND TABLE_NAME = 'V1';

TABLE_NAME IS_AFFECTED
---------- -----------
V1         FALSE      

1 row selected.
```

<a id="87c03a76c35167e4"></a>
### Compatibility

The SQL standard does not define &lt;alter view statement&gt;.

<a id="52ea43ee93ac474c"></a>
### For More Information

Refer to the followings.

- [CREATE VIEW](#ae5c14874ae12b2e)
- [DROP VIEW](#c3d4597ac53c944b)

<a id="6b688bf452d42be5"></a>
## ANALYZE SYSTEM

<a id="e01d0786a9e43f37"></a>
### Function

It controls the statistics information of the system.

<a id="7718e6f48dd37ced"></a>
### Syntax

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="3ca1fcc1d3ac89a4"></a>
### Invocation and Access Rules

ANALYZE ANY ON DATABASE privilege is required to perform &lt;analyze system statement&gt;.

<a id="1f5096679b09d562"></a>
### Syntax Rules and Parameters

<a id="995999496d3ef7db"></a>
#### &lt;analyze action&gt;

When it is omitted, the default value is COMPUTE STATISTICS.

<a id="e3b2fd36289e2200"></a>
#### COMPUTE STATISTICS

It builds the following statistics information related to the system.

- CPU_OPS (Operations Per Second) 
    - It is the number of operations of which the CPU can process per second.

- NETWORK_IOPS (I/O operations Per Second) 
    - It is valid for the cluster. 
    - It is the number of the network I/O which can be processed per second.

<a id="0b183c2f0edc1c8d"></a>
#### DELETE STATISTICS

It deletes the statistics information of the system.

<a id="d55f5bfeed4be4fc"></a>
### Description

The built statistics information of the system is used to calculate the cost of optimization for the query process.

<a id="d63179cade611c1a"></a>
### Examples

The following is an example of building the statistics information of the system by using the &lt;analyze system statement&gt; statement.

```
gSQL> ANALYZE SYSTEM COMPUTE STATISTICS;

analyzed.
```

The following is an example of retrieving the built statistics information of the system.

```
gSQL> 
SELECT * FROM DBA_STAT_SYSTEM;

 CPU_OPS NETWORK_IOPS NETWORK_BUFSIZE LAST_ANALYZED             
-------- ------------ --------------- --------------------------
53000412         2914           65536 2017-03-30 16:49:42.200000

1 row selected.
```

<a id="b19526ea0b6fbe42"></a>
### Compatibility

The SQL standard does not define the concepts of the statistics information.

<a id="c25a3c5a7f805ef5"></a>
### For More Information

Refer to [ANALYZE TABLE](#7a194a6cfef8c726).

<a id="7a194a6cfef8c726"></a>
## ANALYZE TABLE

<a id="a51441cddca11a50"></a>
### Function

It controls the statistics information of the table.

<a id="3d46a01a70a64034"></a>
### Syntax

```
<analyze table statement> ::=
    ANALYZE TABLE table_name
    [ <parallel clause> ]
    [ <analyze action> ]
    ;

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [thread_count]

<analyze action> ::=
      COMPUTE STATISTICS [ <for_clause> ]
    | ESTIMATE STATISTICS <sample_clause> [ <for_clause> ]
    | DELETE STATISTICS

<sample_clause>
      SAMPLE row_count ROWS
    | SAMPLE percentage PERCENT

<for_clause>
      FOR ALL COLUMNS
    | FOR ALL INDEXED COLUMNS
    | FOR COLUMNS column_name [, ...]
    | FOR ALL INDEXES
    | FOR INDEXES index_name [, ...]
```

<a id="190734854b931db3"></a>
### Invocation and Access Rules

ANALYZE ANY ON DATABASE privilege is required to perform &lt;analyze table statement&gt;.

<a id="3902126438042b3c"></a>
### Syntax Rules and Parameters

<a id="e908939941040ede"></a>
#### table_name

It is the table name.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="5bca319d6cd38343"></a>
#### &lt;parallel clause&gt;

It specifies the number of threads to be used in a analyzing process.  
If it is not specified, the default value is PARALLEL.

- NOPARALLEL
    - It does not analyze in parallel.

- PARALLEL [thread_count]
    - It analyzes in parallel.
    - The minimum value of the thread_count is 0, and the maximum value is 64.
    - If the thread_count value is 0 or it is omitted, then it is determined by the number of CPUs in the system.

<a id="e17e6a30b00f1cfe"></a>
#### &lt;analyze action&gt;

When it is omitted, the default value is COMPUTE STATISTICS.

<a id="3c1d25c8fb543a6b"></a>
#### COMPUTE STATISTICS

It builds the following statistics information related to the table through the all inspection.

- The table statistics information
    - Row count 
- The statistics information of each column
    - The number of different values
    - The number of NULL values 
    - The average length of the value 
    - The minimum value
    - The maximum value 
- The statistics information of an index 
    - The number of different keys

The statistics information which is built according to the data type of the column is as follows.

**Statistics information built according to the data type**

<a id="87c7a329cb04dae1"></a>
| Data type | NUM_DISTINCT | NUM_NULLS | AVG_LENGTH | MIN/MAX |
| --- | --- | --- | --- | --- |
| BOOLEAN | O | O | O | X |
| NATIVE_SMALLINT | O | O | O | O |
| NATIVE_INTEGER | O | O | O | O |
| NATIVE_BIGINT | O | O | O | O |
| NATIVE_REAL | O | O | O | O |
| NATIVE_DOUBLE | O | O | O | O |
| NUMBER | O | O | O | O |
| NUMERIC | O | O | O | O |
| FLOAT | O | O | O | O |
| CHAR(n) | O | O | O | It is built when it is 64 bytes or smaller. |
| VARCHAR(n) | O | O | O | It is built when it is 64 bytes or smaller. |
| LONG VARCHAR | X | X | X | X |
| BINARY | O | O | O | X |
| VARBINARY | O | O | O | X |
| LONG VARBINARY | X | X | X | X |
| DATE | O | O | O | O |
| TIME | O | O | O | O |
| TIMESTAMP | O | O | O | O |
| INTERVAL | O | O | O | O |
| ROWID | O | O | O | X |

<a id="ad49449022038ef0"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

It builds the statistics information of the column and the index by using as many samples as the specified &lt;sample_clause&gt;.

- SAMPLE row_count ROWS 
    - It uses as many samples as the specified number of rows.
    - row_count is a positive integer bigger than 0. 
- SAMPLE percentage PERCENT 
    - It uses as many samples as the specified ratio.
    - The percentage is a positive integer in the range between 1 and 99.

If the number of the sampling rows is smaller than the value of [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#43c982a68399a772) property, then it follows the property value.

<a id="b575355dfca68320"></a>
#### &lt;for_clause&gt;

If it is omitted, it builds the statistics information of all possible columns and indexes.

<a id="91ef0491c89092f0"></a>
#### FOR ALL COLUMNS

It builds the statistics information of all possible columns.  
It does not build the statistics information of an index.

<a id="645737846fd3730b"></a>
#### FOR ALL INDEXED COLUMNS

It builds the statistics information of all columns included in an index.  
It does not build the statistics information of other columns.  
It does not build the statistics information of an index.

<a id="9b892f7771b0d85d"></a>
#### FOR COLUMNS column_name [, ...]

It builds the statistics information of the listed columns.  
It does not build the statistics information of unlisted columns.  
It does not build the statistics information of an index.

<a id="e9e32acf34f9e9e3"></a>
#### FOR ALL INDEXES

It builds the statistics information of all indexes.  
It does not build the statistics information of columns.

<a id="7aee32304de6afdf"></a>
#### FOR INDEXES index_name [, ...]

It builds the statistics information of the listed indexes.  
It does not build the statistics information of unlisted indexes.  
It does not build the statistics information of a column.

<a id="4ed7fd45fb1b853a"></a>
#### DELETE STATISTICS

It deletes the statistics information of the table.

<a id="4310faf61847801a"></a>
### Description

The statistics information of the table affects the query optimization, so it is very important information.

The time to build the statistics information is increased in proportion to the data volumes in a table. Therefore, when the data volume is big, then it is recommended to build the statistics information by using the sampling or to build only the statistics of major information which affects the query.

- The following is an example of building the statistics information by using the sampling.

```
ANALYZE TABLE lineitem ESTIMATE STATISTICS SAMPLE 10 PERCENT;
```

- The following is an example of building the statistics information only of major columns and the index.

```
ANALYZE TABLE lineitem COMPUTE STATISTICS FOR ALL INDEXED COLUMNS;
ANALYZE TABLE lineitem COMPUTE STATISTICS FOR ALL INDEXES;
```

<a id="57248c0e4d8ea897"></a>
### Examples

The following is an example of building the statistics information through the all inspection.

```
gSQL> ANALYZE TABLE orders;

Table analyzed.
```

The following is an example of retrieving the built statistics information of the table.

```
gSQL>
SELECT 
       TABLE_NAME
     , NUM_ROWS
  FROM
       DICTIONARY_SCHEMA.USER_TABLES
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME NUM_ROWS
---------- --------
ORDERS      1500000

1 row selected.


gSQL>
SELECT 
       TABLE_NAME
     , COLUMN_NAME
     , NUM_DISTINCT
     , NUM_NULLS
     , LOW_VALUE
     , HIGH_VALUE
  FROM
       DICTIONARY_SCHEMA.USER_TAB_COLUMNS
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME COLUMN_NAME     NUM_DISTINCT NUM_NULLS LOW_VALUE           HIGH_VALUE         
---------- --------------- ------------ --------- ------------------- -------------------
ORDERS     O_ORDERKEY           1500000         0 1                   6000000            
ORDERS     O_CUSTKEY              99996         0 1                   149999             
ORDERS     O_ORDERSTATUS              3         0 F                   P                  
ORDERS     O_TOTALPRICE         1464556         0 857.71              555285.16          
ORDERS     O_ORDERDATE             2406         0 1992-01-01 00:00:00 1998-08-02 00:00:00
ORDERS     O_ORDERPRIORITY            5         0 1-URGENT            5-LOW              
ORDERS     O_CLERK                 1000         0 Clerk#000000001     Clerk#000001000    
ORDERS     O_SHIPPRIORITY             1         0 0                   0                  
ORDERS     O_COMMENT            1482071         0 null                null               

9 rows selected.

gSQL>
SELECT 
       TABLE_NAME
     , INDEX_NAME
     , DISTINCT_KEYS
  FROM
       DICTIONARY_SCHEMA.USER_INDEXES
 WHERE
       TABLE_SCHEMA = 'PUBLIC'
   AND TABLE_NAME   = 'ORDERS'
;

TABLE_NAME INDEX_NAME        DISTINCT_KEYS
---------- ----------------- -------------
ORDERS     ORDERS_PK_INDEX         1500000
ORDERS     ORDERS_CUSTKEY_FK         99996

2 rows selected.
```

<a id="a3646955b6026bdb"></a>
### Compatibility

The SQL standard does not define the concepts of the statistics information.

<a id="57a5a41ca5291e01"></a>
### For More Information

Refer to [ANALYZE SYSTEM](#6b688bf452d42be5).

<a id="7207b4f12e0bf6f6"></a>
## AUDIT POLICY

<a id="d9c2aa4d786db07e"></a>
### Function

It activates the audit policy.

<a id="59eb65b15bc5c5bd"></a>
### Syntax

```
<audit policy statement> ::= 
    AUDIT POLICY policy_name
    [ <specified_user_option> ]
    [ <specified_success_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
    | EXCEPT user_name [, ...]

<specified_success_option> ::=
      WHENEVER SUCCESSFUL
    | WHENEVER NOT SUCCESSFUL
```

<a id="c260087155687ab8"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;audit policy statement&gt;.

<a id="0434f607918d9bc8"></a>
### Syntax Rules and Parameters

<a id="8fd2784243566a01"></a>
#### policy_name

It is the name of the audit policy object to be activated.  
The activated audit policy does not effect on the existing session, and it effects only on the newly created session.

<a id="f2cea1319945dcca"></a>
#### &lt;specified_user_option&gt;

It specifies the user to be audited.  
If omitted, all users are audited.

BY clause and EXCEPT clause can not be used together for the same audit policy.

- BY user_list: If the user to be audited is specified, then use BY clause.
- EXCEPT user_list: If other users excluding a specific user is to be audited, use EXCEPT clause.

<a id="759d3602052444c3"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - If an action succeeds, then the audit record is created.
- WHENEVER NOT SUCCESSFUL
    - If an action fails, then the audit record is created.
- If omitted, both when an action succeeds and fails, the audit record is created.

<a id="ef25ad178c010c11"></a>
### Description

Activating the audit policy does not affect the existing session, but it starts to audit the newly created session.

<a id="239e98745d34a80d"></a>
#### Retrieving Audit Record

The audit record is created when it corresponds to the audit policy, and it can be retrieved through DICTIONARY_SCHEMA.AUDIT_TRAIL view as follows.

```
SELECT logon_user
     , event_timestamp
     , action_name
     , object_name 
     , sql_text
  FROM audit_trail
 WHERE policy_name = 'P1'
;
```

SELECT privilege should be given to an ordinary user to retrieve AUDIT_TRAIL.

```
GRANT SELECT ON DICTIONARY_SCHEMA.AUDTI_TRAIL TO user_name;
```

<a id="eba17510752178f2"></a>
#### Retrieving Audit Policy Information

The information about the audit policy object can be retrieved through DICTIONARY_SCHEMA.AUDIT_POLICY_OPTIONS view.

```
SELECT policy_name
     , audit_option
     , object_schema
     , object_name
  FROM audit_policy_options
;
```

The information about whether the audit policy object is activated can be retrieved through DICTIONARY_SCHEMA.AUDIT_POLICY_ENABLED view.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
;
```

<a id="f0ef2c1106db3f52"></a>
#### Cautions When Using BY and EXCEPT Clauses

Activate the users group if multiple AUDIT POLICY BY clauses are used for the same audit policy.  
In other words, the following two examples have the same meaning.

- Example 1: It activates the p1 audit policy for u1 and u2.

```
AUDIT POLICY p1 BY u1;
AUDIT POLICY p1 BY u2;
```

- Example 2: It activates the p1 audit policy for u1 and u2.

```
AUDIT POLICY p1 BY u1, u2;
```

If multiple AUDIT POLICY EXCEPT clauses are used for the same audit policy, only the last AUDIT POLICY clause is valid.  
In other words, the following two examples have different meanings.

- Example 1: Only the last clause is valid, and activates the p1 audit policy excluding u2.

```
AUDIT POLICY p1 EXCEPT u1;
AUDIT POLICY p1 EXCEPT u2;
```

- Example 2: It activates the p1 audit policy excluding u1 and u2.

```
AUDIT POLICY p1 EXCEPT u1, u2;
```

BY and EXCEPT can not be used together for the same policy.

- If the audit policy is activated with BY clause, then only BY clause can be used afterwards.

```
AUDIT POLICY p1 BY u1;
```

    - Error

```
AUDIT POLICY p1 EXCEPT u2;
```

- If the audit policy is activated with EXCEPT clause, then only EXCEPT clause can be used afterwards.

```
AUDIT POLICY p1 EXCEPT u1;
```

    - Error: It corresponds to *by all users*.

```
AUDIT POLICY p1;
```

If a user wants to convert the audit policy activated with BY to EXCEPT or to convert the audit policy activated with EXCEPT to BY, the activated audit policy should be deactivated first, then it can be converted.

Deactivate the audit policy with NOAUDIT POLICY statement as follows.

- AUDIT POLICY p1 BY u1, u2;
    - NOAUDIT POLICY p1 BY u1, u2;
- AUDIT POLICY p1;
    - NOAUDIT POLICY p1;
- AUDIT POLICY p1 EXCEPT u1, u2;
    - NOAUDIT POLICY p1;
    - NOAUDIT POLICY statement does not have an EXCEPT option.

WHENEVER clause which is used together with BY clause is accumulated.

The following two examples have the same meaning.

- Example 1: It creates the audit record regardless of success/ failure.

```
AUDIT POLICY p1 BY u1 WHENEVER SUCCESSFUL;
AUDIT POLICY p1 BY u1 WHENEVER NOT SUCCESSFUL;
```

- Example 2: It creates the audit record regardless of success/ failure.

```
AUDIT POLICY p1 BY u1;
```

If WHENEVER clauses are used together with EXCEPT clause, only the last WHENEVER clause is valid.

The following two examples have different meanings.

- Example 1: It creates the audit record when it fails.

```
AUDIT POLICY p1 EXCEPT u1 WHENEVER SUCCESSFUL;
AUDIT POLICY p1 EXCEPT u1 WHENEVER NOT SUCCESSFUL;
```

- Example 2: It creates the audit record regardless of success/ failure.

```
AUDIT POLICY p1 EXCEPT u1;
```

<a id="49d913a08a6452f5"></a>
### Examples

The following is an example of activating the audit policy for all users.

```
AUDIT POLICY table_pol;
```

The information about activation can be viewed through the following query.

```
SELECT policy_name
     , enabled_opt
     , user_name
  FROM audit_policy_enabled
 WHERE policy_name = 'TABLE_POL';

POLICY_NAME  ENABLED_OPT  USER_NAME
-----------  -----------  ---------
TABLE_POL    BY           ALL USERS
```

The following is an example of activating the audit policy by defining specific users.

```
AUDIT POLICY dml_pol BY u1, u2;
```

The following is an example of activating the audit policy by excluding a specific user.

```
AUDIT POLICY read_seq_pol EXCEPT sys;
```

The following is an example of auditing the failure of SQL statement by a specific user.

```
AUDIT POLICY delete_pol BY u1 WHENEVER NOT SUCCESSFUL;
```

<a id="9f9de11c71a238e1"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="644c8bb450afd18a"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Viewing audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="8094485dc3cb5ea5"></a>
## CLOSE cursor_name

<a id="1d6c7101dfd415fa"></a>
### Function

It closes a cursor.

<a id="1e015fa4ea9e94bd"></a>
### Syntax

```
<close statement> ::=
    CLOSE cursor_name
    ;
```

<a id="db6fdf1832366930"></a>
### Syntax Rules and Parameters

<a id="0f32afd29f6a54ff"></a>
#### cursor_name

The cursor should be open.  
The cursor should be declared with [DECLARE cursor_name](#9826eadcd321de1b) statement in the session.

<a id="9844fa290a1f4f3d"></a>
### Description

The cursor is an object which exists in the session and it does not affect the cursor in a different session.

<a id="ed92cfbcf4c84380"></a>
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

<a id="3b775a30be663b1b"></a>
### Compatibility

**SQL standard compatibility**

<a id="95dbf43fc832a7e6"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="6a17c8ddca71e153"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)
- [FETCH cursor_name](#8b90e7e7e6e0c963)

<a id="a048c7c7e79657ee"></a>
## COMMENT ON name IS

<a id="58ad89be6a4b38b9"></a>
### Function

It stores the comments about the object in the dictionary.

<a id="f177158f81a6a30f"></a>
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

<a id="4ded54f051669cd2"></a>
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

<a id="1718fce6974c5b5d"></a>
### Syntax Rules and Parameters

<a id="3f3455b55a073fe2"></a>
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

If schema_name for the schema object is not specified, the schema name is determined by [Schema Path](13-sql-objects.md#4c6da900c6be2852) of the user performing the statement.

```
COMMENT ON TABLE test_table IS 'test comment'; 
→ COMMENT ON TABLE user_default_schema.test_table IS 'test comment';
```

<a id="d1712ab924d251f8"></a>
#### 'comment string'

It describes the comments to be stored.  
Use the empty string ('') to delete the comments as follows.

```
COMMENT ON TABLE test_table IS '';
```

The length of the comment string can not exceed 1024 bytes.

<a id="67dcdec53f033aad"></a>
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

For more information about the detailed description of each view, refer to [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#94a1f2f476df37b4).

<a id="e58df7ad0253e35e"></a>
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

<a id="ed74fc57d6224efb"></a>
### Compatibility

&lt;comment statement&gt; does not exist in SQL standard.

<a id="97c03faa5a24c67f"></a>
## COMMIT

<a id="4c0fe1fbb3dc5116"></a>
### Function

It terminates the current transaction and makes all changes permanent.

<a id="5912f61aba071d89"></a>
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

<a id="dc30e31ca88e5af0"></a>
### Syntax Rules and Parameters

<a id="8075d1e8758d6a83"></a>
#### WORK

It is the reserved word which does not affect the operation.

<a id="ca0d754d30b4c597"></a>
#### &lt;commit comment clause&gt;

- COMMENT 'comment_string'
    - It specifies the comment to the transaction when committing the transaction.

<a id="7e54788b765ab820"></a>
#### &lt;commit write clause&gt;

It determines whether to wait until the redo logs generated by the commit operation are written on the redo log file.

- WAIT
    - It waits until the redo logs generated by the commit operation are written to the redo log file, and then the operation is terminated. 
- NOWAIT
    - The operation is terminated when the redo logs generated by the commit operation are written to the redo log buffer.
- If it is not specified, it follows the property.

<a id="ac96b984f3fcb438"></a>
#### &lt;commit force clause&gt;

It is used to manually commit a distributed transaction.

- FORCE 'xid_string'
    - It commits the distributed transaction 'xid_string'.
    - 'xid_string' consists of *'format_id.transaction_id.branch_id'*.

<a id="d2683e379edbb882"></a>
### Description

COMMIT statement completes the following statements which were executed in a transaction.

- Data Manipulation Language (DML) statement
    - It is the statement which changes data, such as INSERT, UPDATE, DELETE. 
- Data Definition Language (DDL) statement
    - It is the statement which changes the structure and definition of the objects, such as CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE.

Exceptionally, the following DDL statements which manage the OS resources or change the DATA TYPE are automatically committed.

- [CREATE TABLESPACE](#4fb45716ef9fbe7b)
- [DROP TABLESPACE](#ee3406f353c996e6)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](#d1d235380dc3280c)

When performing COMMIT, the cursor opened by WITHOUT HOLD option is automatically closed. For more information about cursors, refer to the following cursor related statements.

- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)

If the transaction violates the DEFERRED constraint, the COMMIT statement fails and the transaction is rolled back. For more information about DEFERRED constraint, refer to [SET CONSTRAINTS](#8337ae2c011b78f5).

<a id="a4393108ae97f0ed"></a>
### Example

The following is an example of performing COMMIT after executing INSERT statement.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> COMMIT WORK COMMENT 'INSERT T1';

Commit complete.
```

<a id="cb0a703f8f08b6ce"></a>
### Compatibility

**SQL standard compatibility**

<a id="37f98322d1250f2d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T261 | Chained transactions | X |

<a id="036172084b79b5a4"></a>
### For More Information

Refer to the followings.

- [ROLLBACK](#30d00b80c704d186)
- [SAVEPOINT savepoint_specifier](#bf9e53dc119286d7)

<a id="6be201c413853041"></a>
## CREATE AUDIT POLICY

<a id="dbe9971083690012"></a>
### Function

It creates an audit policy object.  
AUDIT POLICY should be performed to activate the created audit policy object.

<a id="e40d5cb2357d3ed3"></a>
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

<a id="f0441c698e9ef8d0"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;audit policy definition&gt;.

<a id="99b91217845cdcb6"></a>
### Syntax Rules and Parameters

<a id="45f9e92e4640a229"></a>
#### policy_name

It is the name of the audit policy to be created.

<a id="377743085c4f9a99"></a>
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

<a id="c833e4556051d657"></a>
#### &lt;action_audit_clause&gt;

It audits an action for a specific object and an action for the entire database.

<a id="7dc8dee705721bbd"></a>
#### &lt;object_action_audit&gt;

<a id="310275d905ed4afd"></a>
##### ALL ON object_name

It means all actions which can list objects corresponding to object_name.

The following table describes audit actions of which each object type can audit.

**Audit action per object type**

<a id="d6b95b2bf8ce882e"></a>
| Object type | Action |
| --- | --- |
| Table | ALTER, COMMENT, DELETE, GRANT, INDEX, INSERT, LOCK, RENAME, SELECT, UPDATE |
| View | ALTER, COMMENT, GRANT, SELECT |
| Sequence | ALTER, COMMENT, GRANT, SELECT |
| Stored Function/Procedure | ALTER, COMMENT, EXECUTE, GRANT |

<a id="40f454b55a220050"></a>
##### &lt;object_action&gt; ON object_name

Each separate action per a specific object should be listed by specifying ON clause as follows.

```
CREATE AUDIT POLICY p1
       ACTIONS INSERT ON u1.t1
             , DELETE ON u1.t1
             , UPDATE ON u1.t1
;
```

<a id="b786224dc8b4b828"></a>
##### Caution of EXECUTE action

Auditing the success or the failure of stored function or stored procedure is determined only based on whether it is executable at the time of execution.

- WHENEVER NOT SUCCESSFUL creates the audit record when neither the stored function nor procedure is executable.
- WHENEVER SUCCESSFUL creates the audit record even though an error occurs while executing SQL statement within the stored function or the procedure 
- If an auditing for the failure of SQL statement within the stored function or the procedure is required, then the audit target should include the corresponding SQL statement.

<a id="63235d16fa409981"></a>
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

<a id="0b2a29469bfbeac6"></a>
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

<a id="071575551f5adb9c"></a>
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

<a id="bbf106ef4efff475"></a>
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

<a id="386939830cca1388"></a>
### Compatibility

The audit policy does not exist in SQL standard.

<a id="957da05ccc4dc61e"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Retrieving audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="f8131b333b91edb7"></a>
## CREATE CLUSTER GROUP

<a id="09bc1184f2ef690d"></a>
### Function

It creates a cluster group which is to participate in a cluster system.

<a id="06a986a18858e458"></a>
### Syntax

```
<cluster group definition> ::=
    CREATE CLUSTER GROUP group_name 
        <cluster member definition> [, ...]
    ;

<cluster member definition> ::=
    CLUSTER MEMBER member_name <connection attribute>

<connection attribute> ::
    HOST 'address' PORT port_no
```

<a id="877f4ed12ba78df4"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  

ADMINISTRATION ON DATABASE privilege is required to perform &lt;cluster group definition&gt;.

<a id="778e3c8bf34b623a"></a>
### Syntax Rules and Parameters

<a id="282f0500958a8eac"></a>
#### group_name

It is the name of a cluster group.  
An identical cluster group name or a cluster member name should not exist.  
The name length should be shorter than 128 bytes.

<a id="6356c5113c6103e8"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group can include maximum 32 cluster members.  
A cluster group which is created first in a cluster system can define only one cluster member, and should include itself as a cluster member.

<a id="a7aedf0ddce7cb01"></a>
#### member_name

It is the name of a cluster member.  
The name of a cluster member should be same as the name of the member which was defined when creating the database of that member.  
An identical cluster group name or a cluster member name should not exist.  
The name length should be shorter than 128 bytes.

The start-up phase of the cluster member should be the OPEN phase.

<a id="919cd762eafb10e4"></a>
#### &lt;connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
&lt;connection attribute&gt; should be as same as the HOST and PORT which were defined when the database of that cluster member was created.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST address uses ip v4 type.
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="3c46195c42085ddb"></a>
### Description

&lt;cluster group definition&gt; statement does not rebalance the shard of tables.

Perform the following statements to rebalance the shard to an added cluster group.

- [ALTER DATABASE REBALANCE](#6bf45492d225c752)
- [ALTER TABLE name REBALANCE](#467720ee446849be)

<a id="78c6671507836c30"></a>
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

<a id="f95b8923ee2a9478"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="8bf4564ddd875524"></a>
### For More Information

Refer to the followings.

- [DROP CLUSTER GROUP](#7335700144f62a07)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0f86518c60487e59)

<a id="648735809e94071b"></a>
## CREATE CLUSTER LOCATION

<a id="2afaf0d72f399506"></a>
### Function

It creates the connection information of a cluster member.

<a id="08024ec1e13ad994"></a>
### Syntax

```
<cluster location definition> ::=
    CREATE CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="628e0ac7e179763c"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;cluster location definition&gt;.

<a id="940e294323aaf8d8"></a>
### Syntax Rules and Parameters

<a id="1d42dedd31b43cd5"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should not exist in the registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="d478c18b89db9418"></a>
#### &lt;cluster connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST address uses ip v4 type.
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="e9928ff46f4dbc1c"></a>
### Description

Generally, the information of the cluster location is automatically created by using the connection information provided when creating the cluster group or adding the cluster member. The created information is deleted together when deleting the cluster member and the cluster group.

If the information of the cluster location is modified, then the connection information can be modified by using [ALTER CLUSTER LOCATION](#ca28514ab71c220c) without deleting or recreating the cluster member.

<a id="13f813882b8152f5"></a>
### Examples

```
gSQL> 
CREATE CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120,
;

Created
```

<a id="1fa99ac95fd494ea"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="0e835a9eaa0d0e4d"></a>
### For More Information

Refer to [DROP CLUSTER LOCATION](#7866e0152d6dec9e).

<a id="11cedda99c2339bc"></a>
## CREATE INDEX

<a id="4af6d3e4f071befb"></a>
### Function

It creates an index.

<a id="ff284271e5d30ba9"></a>
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
    | <logging clause> 
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

<logging clause> ::=
      LOGGING
    | NOLOGGING

<parallel clause> ::=
      NOPARALLEL
    | PARALLEL [ integer ]
```

<a id="1dfd08e7f35cd95a"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;index definition&gt;.

- One of the following privileges is required to create an index on the table.
    - (INDEX or CONTROL TABLE ON) TABLE for that table
    - CONTROL SCHEMA ON SCHEMA for the schema to which the table belongs
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the schema on which the index to be created.
    - (CREATE INDEX or CONTROL SCHEMA) ON SCHEMA for the schema
    - CREATE ANY INDEX ON DATABASE

- One of the following privileges is required for the tablespace on which the index to be created.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

- The owner of the index is determined as follows.
    - The owner of the schema to which the index belongs. 
    - If the schema to which the index belongs is PUBLIC, then it is the user who executed the statement.

> Unique indexes in a cluster system should include all sharding keys.

<a id="de1efcafd5382d2a"></a>
### Syntax Rules and Parameters

<a id="adb1374c32658fcc"></a>
#### UNIQUE

It does not allow duplicate values for the columns of the index.

<a id="31b872607e3ba3d3"></a>
#### index_name

It is the index name to be created and it should be a unique name within the schema.  
If the schema name is omitted, the index is created in the schema to which the referring table belongs.  
The length of the index name should be shorter than 128 bytes.

<a id="9f0fd1e4cc4e5907"></a>
#### table_name

It is the table name which creates the index.  
The schema to which a table belongs, such as schema_name.table_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="8834e9d8ffda3d28"></a>
#### column_name

It is the column name to be used as an index key.  
One or more columns should be defined, and maximum 32 columns can be used as an index key.

The following constraints can occur depending on the implementation.

- If the column data type included in an index is LONG CHARACTER VARYING, LONG BINARY VARYING, an index can not be created.
- An index is created only when the sum of the column precisions is less than half of the page size.

<a id="aa2a251f7b298faa"></a>
#### ASC | DESC

It specifies the sort order of a column.

- ASC: It is sorted in ascending order.
- DESC: It is sorted in descending order.
- If not specified, the default value is ASC.

<a id="47d138441581580c"></a>
#### NULLS FIRST | NULLS LAST

It specifies the sort order of the NULL value.

- NULLS FIRST: It precedes the non-NULL values.
- NULLS LAST: It is behind the non-NULL values.
- If not specified, the default value is NULLS LAST.

<a id="4e3a5504a69cd153"></a>
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

<a id="ba5ca529587564e5"></a>
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

<a id="e5c25df80f014e68"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes.(If the unit is omitted, the default value is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="da44362e6a073591"></a>
#### LOGGING | NOLOGGING

It specifies whether the index performs redo logging.  
If not specified, the default value is NOLOGGING.

<a id="5452d0fe5b16aa4b"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used when building an index.

- NOPARALLEL 
    - It does not build an index in parallel.
- PARALLEL [integer] 
    - It builds an index in parallel.
    - If an integer is omitted or set as 0, then it follows the property (INDEX_BUILD_PARALLEL_FACTOR). 
    - The minimum value of an integer is 0 and the maximum value is 16. 
    - If the property value is 0, then the system determines the optimal value.
- If it is omitted, the default value is PARALLEL.

<a id="a38df68b69f1634c"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be stored.

- If it specifies tablespace_name
    - The tablespace_name of LOGGING index should be a data tablespace. 
    - The tablespace_name of NOLOGGING index should be a temporary tablespace or a nologging tablespace.

- If it omits TABLESPACE clause
    - If INDEX TABLESPACE tablespace_name of USER is specified
        - The defined tablespace is used.
    - If INDEX TABLESPACE of USER is NULL
        - LOGGING index uses the user's default data tablespace.
        - NOLOGGING index uses the user's default temporary tablespace.

<a id="e2033dea7ca7cce6"></a>
### Description

LOGGING index and NOLOGGING index have the following trade-offs.

- LOGGING index
    - Advantage: It does not separately build an index because the index is automatically restored by using the log when starting up the system.
    - Disadvantage: A disk I/O occur because the changes on the index is recorded on the log when altering the row.
- NOLOGGING index
    - Advantage: A disk I/O does not occur for the changes on the index when altering the row.
    - Disadvantage: It automatically rebuilds the index when starting up the system because the log information of the index does not exist.

<a id="8f6838087ceaf0bb"></a>
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
gSQL> CREATE INDEX idx_t1_id ON t1( id ) LOGGING;

Index created.
```

The following is an example of creating the index with parallel option.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) PARALLEL;

Index created.
```

The following is an example of specifying the tablespace when creating an index.

```
gSQL> CREATE INDEX idx_t1_name ON t1( name ) NOLOGGING TABLESPACE mem_temp_tbs;

Index created.
```

<a id="5b32d5f6a4f53437"></a>
### Compatibility

The SQL standard does not cover the concepts of the index.

<a id="f3e5fae729041c96"></a>
### For more information

Refer to [DROP INDEX](#9fbe418d2e4cd17c).

<a id="b8608593e7c730f3"></a>
## CREATE PROFILE

<a id="489349467179157e"></a>
### Function

It is the statement which creates the profile, and it sets the password management method.   
When a profile is allocated to a user, the user's password is managed in the way defined in the profile.

<a id="f1b70aff4da41857"></a>
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

<a id="1816a44e393acc31"></a>
### Invocation and Access Rules

CREATE PROFILE ON DATABASE privilege is required to perform &lt;profile definition&gt;.

<a id="f04b4eaf44b840c2"></a>
### Syntax Rules and Parameters

<a id="dc89185f8a86bcb7"></a>
#### profile_name

It specifies the profile name to be created.

<a id="5e66dfc6ad24d5db"></a>
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

<a id="b63f02d94b014b61"></a>
#### FAILED_LOGIN_ATTEMPTS

It sets the number of consecutive login attempts allowed to fail.  
If the failed attempts exceed the specified number, the account is locked.

- FAILED_LOGIN_ATTEMPTS integer
    - The value range should be a positive integer bigger than 0.
- FAILED_LOGIN_ATTEMPTS UNLIMITED
    - Account lockout which is due to a login failure does not occur.
- FAILED_LOGIN_ATTEMPTS DEFAULT
    - It follows the "DEFAULT" profile policy.

<a id="105439782ad45e99"></a>
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

<a id="f18f3308295bab67"></a>
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

<a id="42a8e5bfa68b2fab"></a>
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

<a id="0fec782a0f8ad603"></a>
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

<a id="a4f0409e93a84e97"></a>
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

<a id="0fa06f57a3ad38fd"></a>
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

<a id="5ed1d17d44a36049"></a>
##### KISA_VERIFY_FUNCTION

It is the password verification method of KISA (Korea Internet & Security Agency).

- 8 or more letters
- One or more characters
- One or more numbers
- One or more special characters

<a id="a31265b98c75cf6f"></a>
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

<a id="404a12ef99682f36"></a>
##### ORA12C_STRONG_VERIFY_FUNCTION

It is the password verification method of Oracle, ORA12C_STRONG_VERIFY_FUNCTION.

- 9 or more letters
- 2 or more uppercases 
- 2 or more lowercases
- 2 or more numbers
- 2 or more special characters
- At least 4 characters of the new password should be different from the old password.

<a id="345553fca814945a"></a>
##### VERIFY_FUNCTION_11G

It is the password verification method of Oracle, VERIFY_FUNCTION_11G.

- 8 or more letters
- 1 or more characters 
- 1 or more numbers 
- The username should not be included. 
- At least 3 characters of the new password should be different from the old password.

<a id="000c0d038334f1f3"></a>
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

<a id="7714e0c3e21f7114"></a>
### Description

<a id="40138f727c4fe9d9"></a>
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

<a id="67ac38985b4450aa"></a>
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

<a id="42f84b44affcca5e"></a>
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

<a id="87082d5b2a01f768"></a>
#### Password Reusability

The followings are the parameters affecting the password reusability.

- PASSWORD_REUSE_MAX
- PASSWORD_REUSE_TIME

The password reusability of the two parameters above is determined according to the following table.

**Conditions for the password reusability**

<a id="39348c61a126116f"></a>
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

<a id="017269223cb8aac6"></a>
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

<a id="bb7d5fb0ffd96ed8"></a>
#### DEFAULT profile

When creating the database, the following "DEFAULT" profile is automatically created. The password parameters of the "DEFAULT" profile are as follows.

**Configuration of DEFAULT profile**

<a id="75df97e034324b0d"></a>
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

<a id="d3519e8b5c6ca057"></a>
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

<a id="5b351aa0587a8eea"></a>
### Compatibility

The SQL standard does not cover the concepts of the profile.

<a id="e6f5f5587b8735d5"></a>
### For More Information

Refer to the followings.

- [DROP PROFILE](#a176f22a83621a33)
- [ALTER PROFILE](#da7815275847e190)
- [CREATE USER](#524780362f90ebc8)
- [ALTER USER](#ed40a6862d9c8f12)
- [ALTER DATABASE CLEAR PASSWORD HISTORY](#b1c83484159e9548)

<a id="671a916eb0910614"></a>
## CREATE SCHEMA

<a id="71b69c2145e3818e"></a>
### Function

It defines the schema.

<a id="b3051e4e1ada4c21"></a>
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

<a id="461d0804f75beeea"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;schema definition&gt;.

- CREATE SCHEMA ON DATABASE privilege is required to create the schema.

- If &lt;schema element&gt; exists, the privilege to perform each &lt;schema element&gt; is required.  
  For more information about the access privilege, refer to *invocation and access rules* in the following statements.
    - [CREATE TABLE](#72507f5467c281c9)
    - [CREATE VIEW](#ae5c14874ae12b2e)
    - [CREATE INDEX](#11cedda99c2339bc)
    - [CREATE SEQUENCE](#f57ec80975339322)
    - [GRANT privileges TO](#5969f471eb288b39)
    - [COMMENT ON name IS](#a048c7c7e79657ee)

- The user who is user_identifier has the following privileges for the created schema.
    - The owner of the created schema, which is schema_name
    - The owner of the object which is created by &lt;schema element&gt; clause

- An appropriate privilege for the schema is required to create an object because a separate privilege on the created schema is not granted.  
  For more information about schema privilege types, refer to [&lt;schema privilege&gt;](#f992ce28766780dd) of GRANT privileges TO statement.  
  For more information about usage example, refer to [Examples](#934e0bec0913b6a4) of CREATE USER statement.

<a id="93fd118d16b6bbda"></a>
### Syntax Rules and Parameters

<a id="24762e42b6bb69c7"></a>
#### schema_name

It is the schema name to be created.  
An identical schema name should not exist in the database.  
The length of the schema name should be shorter than 128 bytes.

<a id="9c74718ab5b91c15"></a>
#### AUTHORIZATION user_identifier

If the schema name is omitted, a schema with the same name as the user_identifier is created.  
If the AUTHORIZATION is not specified, the user_identifier of the user performing the statement is used.

<a id="d3f9dd9eee59c30c"></a>
#### schema_name AUTHORIZATION user_identifier

It specifies the schema name and schema owner to be created.  
The owner can not be a role or PUBLIC.

<a id="fee1c2c0a8572057"></a>
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

<a id="fa2b744aa94d3d8f"></a>
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

<a id="ad851340b86e00d6"></a>
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

<a id="1d0d85bc1c147e30"></a>
### Compatibility

**SQL standard compatibility**

<a id="d586ca0c0ff3628d"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S071 | SQL paths in function and type name resolution | X |
| F461 | Named character sets | X |
| F171 | Multiple schemas per user | O |
| T332 | Extended roles | X |

<a id="0d12ee72466018e2"></a>
### For More Information

Refer to the followings.

- [DROP SCHEMA](#406abccf7b931f83)
- [CREATE USER](#524780362f90ebc8)
- [CREATE TABLE](#72507f5467c281c9)
- [CREATE VIEW](#ae5c14874ae12b2e)
- [CREATE INDEX](#11cedda99c2339bc)
- [CREATE SEQUENCE](#f57ec80975339322)
- [GRANT privileges TO](#5969f471eb288b39)
- [COMMENT ON name IS](#a048c7c7e79657ee)

<a id="f57ec80975339322"></a>
## CREATE SEQUENCE

<a id="e775436fc963ff2f"></a>
### Function

It creates a sequence.

<a id="57fc6e59b528a767"></a>
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

<a id="85c0f85f2bc18753"></a>
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

<a id="79ec3567b53c6404"></a>
### Syntax Rules and Parameters

<a id="d4eea2d6879c8dbd"></a>
#### sequence_name

It is the sequence name to be created, and it should be a unique name within the schema.  
The schema to which the sequence belongs, such as schema_name.sequence_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the sequence name should be shorter than 128 bytes.

<a id="64e4fa99fa1b748e"></a>
#### &lt;sequence generator option&gt;

If any of &lt;sequence generator option&gt; is not used, the following two statements have the same meaning.

- CREATE SEQUENCE test_seq; 
- CREATE SEQUENCE test_seq START WITH 1 INCREMENT BY 1 NO MINVALUE NO MAXVALUE NO CYCLE CACHE 20;

<a id="7f9ac7a9b1543115"></a>
#### &lt;sequence generator start with option&gt;

It defines the first sequence number to be generated.  
Depending on the ascending or the descending order, it has the following features.

- Ascending sequence (INCREMENT BY a positive number)
    - It is used when starting the sequence with bigger sequence value than the minimum value.
    - If START WITH clause is omitted, the default value is the minimum value (MINVALUE value).
- Descending sequence (INCREMENT BY a negative number)
    - It is used when starting the sequence with smaller sequence value than the maximum value.
    - If START WITH clause is omitted, the default value is the maximum value (MAXVALUE value).

<a id="735d0101b3352a1b"></a>
#### &lt;sequence generator increment by option&gt;

It defines the interval of sequence numbers.  
The constraints and features are as follows.

- A positive number or a negative number is allowed, but 0 is not allowed.
- The absolute value of the interval should be smaller than the difference between MINVALUE and MAXVALUE.
- The ascending sequence is generated if it is a positive number, and the descending sequence is generated if it is a negative number.
- If INCREMENT BY clause is omitted, the default is a positive number 1.

<a id="82b95d2615ad8a4d"></a>
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

<a id="5094407fa31799ed"></a>
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

<a id="abc897e37c8184f7"></a>
#### &lt;sequence generator cycle option&gt;

It specifies whether to continue generating a value when the sequence value becomes the maximum value or the minimum value.

- CYCLE 
    - When the ascending sequence becomes the maximum value, it generates the value again from the minimum value. 
    - When the descending sequence becomes the minimum value, it generates the value again from the maximum value. 
- NO CYCLE | NOCYCLE 
    - When the sequence value becomes the maximum value or the minimum value, it does not generate a sequence value. 
    - NO CYCLE(SQL standard) and NOCYCLE are the reserved words with the same meaning, so either of them can be used.
- If CYCLE and NO CYCLE are not specified, the default value is NO CYCLE.

<a id="414a2e0986794da7"></a>
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

<a id="11b8b2f9d2c22194"></a>
### Description

The sequence values of the created sequence objects are used by using [NEXTVAL](11-sql-elements.md#39329e8ee5b2fa13) and [CURRVAL](11-sql-elements.md#564199c8f133c07b) functions.

The sequence value does not have a transaction property. The sequence value maintains the most recent value, even when an error occurs in the SQL statement in which the sequence function is used or when explicit ROLLBACK is performed.

CURRVAL function returns NEXTVAL value from the most recent call by a session.   
Therefore, using this feature, the sequence value obtained by NEXTVAL can still be usable in the other SQL statements. However, when the session does not call NEXTVAL, using CURRVAL function generates an error.

<a id="50968a76d928f8fc"></a>
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

<a id="d76d83a9330f5427"></a>
### Compatibility

The SQL standard does not define &lt;sequence generator cache option&gt; clause.

**SQL standard compatibility**

<a id="226b43f66d967ec1"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="5803ed85b6e98691"></a>
### For More Information

Refer to the followings.

- [DROP SEQUENCE](#98127fac6b27272b)
- [ALTER SEQUENCE](#b01c09c114935817)
- [NEXTVAL](11-sql-elements.md#39329e8ee5b2fa13)
- [CURRVAL](11-sql-elements.md#564199c8f133c07b)

<a id="9e6f02e8285e67d1"></a>
## CREATE SYNONYM

<a id="c7e82458071d423c"></a>
### Function

It creates a synonym. A synonym is an alternative name for a table, view, sequence, or another synonym, and it can be used in the following statements.

- DML: SELECT, INSERT, UPDATE, DELETE, LOCK TABLE, CALL
- DDL: GRANT, REVOKE, COMMENT

<a id="41f6427e5948fe1a"></a>
### Syntax

```
<table definition> ::=    
    CREATE [OR REPLACE] [PUBLIC] SYNONYM [schema_name.]synonym_name 
    FOR [schema_name.]object_name
    ;
```

<a id="11ae5523af9f17a3"></a>
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

<a id="ffe5eda7e2cbae1a"></a>
### Syntax Rules and Parameters

<a id="6ad88ba80827c9b3"></a>
#### [ OR REPLACE ]

It replaces the existing synonym if the synonym already exists.

<a id="a0430c1ac664a476"></a>
#### [ PUBLIC ]

It is specified when creating public synonym.  
If it is omitted, private synonym is created.

<a id="12a7122bbc79f782"></a>
#### synonym_name

It is the synonym name to be created, and it should be a unique name within the schema.  
The schema to which the synonym belongs, such as schema_name.synonym_name, can be defined. If schema_name is omitted, default schema name of the user performing the statement is used.  
The length of the synonym name should be shorter than 128 bytes.  
Public synonym is a non-schema object. Therefore, a schema name can not be specified when creating public synonym by explicitly specifying PUBLIC.

<a id="7062bdfdbe2c3a49"></a>
#### object_name

The schema to which the object belongs, such as schema_name.object_name, can be defined. If schema_name is omitted, default schema name of the user performing the statement is used.

The object types which can specify the object_name are as follows.

- Table
- View
- Sequence
- Another synonym

Existence of the target object, cycle check and privilege check are performed when executing the statement using the synonym.

<a id="5c4ba2fc60cb4d64"></a>
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

<a id="e59291a71f5c5550"></a>
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

<a id="57c1aaa9327ca1f0"></a>
### Compatibility

The SQL standard does not define the CREATE SYNONYM statement.

<a id="cb12f721c1426b9e"></a>
### For More Information

Refer to [DROP SYNONYM](#1c07c24ac96a8b62).

<a id="72507f5467c281c9"></a>
## CREATE TABLE

<a id="f09e25131f245a3c"></a>
### Function

It defines a table.

<a id="5f0d90183a76c875"></a>
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
    | <logging clause>


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

<logging clause> ::=
      LOGGING
    | NOLOGGING


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

<a id="3aeb1dcdeccbed2a"></a>
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

<a id="ed2873dcad48c8ad"></a>
### Syntax Rules and Parameters

<a id="67a923a89b775405"></a>
#### table_name

It is the table name to be created and it should be a unique name within the schema.  
The schema to which the table belongs, such as schema_name.table_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the table name should be shorter than 128 bytes.

<a id="33f0fb077cded0d9"></a>
#### &lt;column definition&gt;

It defines the columns which configure the table.  
The table should include one or more column definitions.   
It can specify the column data type, default value, automatically generated value, and constraints.

<a id="08e09927b639220e"></a>
#### column_name

It is name of the column which configures a table and each column should have a unique name within the table.  
The length of the column name should be shorter than 128 bytes.

<a id="9415bec4d378d8e5"></a>
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
For more information about data types, refer to [Data Type](11-sql-elements.md#9ebaf6ccb06f475d).

<a id="058d9b77400ac369"></a>
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

<a id="9451ae3531d2b6a9"></a>
#### [ &lt;default clause&gt; | &lt;identity column specification&gt; ]

It specifies the default value of a column.  
&lt;default clause&gt; and &lt;identity column specification&gt; can not be used together.  
When both of them are omitted, the default value is NULL.

<a id="77b8ab635fda06de"></a>
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

If the data type is not compatible or the space is insufficient, an error occurs when using DEFAULT in INSERT, UPDATE statements.

- CREATE TABLE t1 ( user_name VARCHAR(1) DEFAULT CURRENT_USER );
- e.g. error: INSERT INTO t1 VALUES (DEFAULT);
- e.g. error: UPDATE t1 SET user_name = DEFAULT;

DEFAULT expression can use any built-in functions but it can not use the followings.

- Logical operators (AND, OR, NOT), comparison operators (=,>, ...)
- Stored function
- Column name
- Subquery expression

<a id="bb2126450b9efec0"></a>
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

For more information about &lt;common sequence generator option&gt; and &lt;basic sequence generator option&gt;, which are options to create an identity column, refer to [CREATE SEQUENCE](#f57ec80975339322).

<a id="0cf1823c600193f5"></a>
#### &lt;column constraint definition&gt;

It defines the following constraints for a column.

- NOT NULL constraints
- UNIQUE constraints
- PRIMARY KEY constraints

<a id="9bc9b32756efd8be"></a>
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

<a id="346cbeb206168fc3"></a>
#### NOT NULL Constraint

NULL is not allowed for the column value.

<a id="38312bf7f459c495"></a>
#### UNIQUE Constraint

The identical value is not allowed for the column value, but NULL is allowed.

<a id="af4eb5dbe99276e7"></a>
#### PRIMARY KEY Constraint

NULL or the identical value is not allowed as the column value. A single PRIMARY KEY constraint can be defined on a single table.

<a id="c16cf2332ce53081"></a>
#### &lt;index name clause&gt;

It defines the index name to be created when defining UNIQUE constraint and PRIMARY KEY constraint.

- INDEX index_name 
    - It defines the index name for the constraint.
    - It can not be used together with a schema name and it is created in the same schema where the constraint is created.

When defining UNIQUE constraint and PRIMARY KEY constraint, if INDEX clause is omitted, an index which satisfies the constraints is automatically created.  
"constraint_name" + "INDEX" is added to the name of index which is automatically generated.

- &lt;index attributes&gt; 
    - It specifies the physical attributes of the index to be created.
    - For more information, refer to [CREATE INDEX](#11cedda99c2339bc).
- TABLESPACE index_tablespace_name 
    - It specifies the tablespace where the index is to be created.
    - For more information, refer to [CREATE INDEX](#11cedda99c2339bc).

<a id="ea4e41ed20bb4738"></a>
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

<a id="d5e40ee1ff095c68"></a>
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

<a id="1632ea8e08ded2ae"></a>
#### &lt;table sharding strategy&gt;

It defines the sharding strategy of a table.  
It can be defined as one of the four following strategies.

- &lt;cloned strategy&gt; 
- &lt;hash sharding strategy&gt; 
- &lt;range sharding strategy&gt; 
- &lt;list sharding strategy&gt;

If it is omitted, it is determined by [DEFAULT_SHARDING](../part-02-administration-manual/10-server-property.md#30cbcb4f35b1117e) property value.

- If DEFAULT_SHARDING value is 0
    - &lt;cloned strategy&gt;
- If DEFAULT_SHARDING value is 1 
    - &lt;hash sharding strategy&gt;

<a id="ec2651303443ec75"></a>
#### &lt;cloned strategy&gt;

It clones all data in a table.

<a id="ef8d89a9c5e9bfb8"></a>
#### &lt;clone placement&gt;

It defines the placement strategy of a clone.

- AT CLUSTER WIDE 
    - It places clones in all cluster members of all cluster groups in a cluster system.
    - A clone can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster group and a cluster member.
- AT CLUSTER GROUP group_list 
    - It places clones in all cluster members of a specified cluster groups.
    - A clone can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster member in a specified cluster group.
    - Adding a cluster group does not affect the relocation of the clone.
- When it is omitted, the default value is AT CLUSTER WIDE.

<a id="98bd79ff8afaaa54"></a>
#### &lt;hash sharding strategy&gt;

It shards the table data according to the hash value of the sharding key.

<a id="4e7a2c0abcfc5180"></a>
#### SHARDING BY [HASH] ( column_list )

It defines a sharding key for a hash sharding.

- It can list maximum 32 columns. 
- It can not use a duplicate column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="838ca97380e4be95"></a>
#### &lt;hash shard count&gt;

It defines the number of the hash shards to be sharded.  
The number of shards can be defined from 1 to 512.  
If it is omitted, the default value is 24.

<a id="287ee8d536fbaeae"></a>
#### &lt;hash shard placement&gt;

It defines the placement strategy of a hash shard.

- AT CLUSTER WIDE 
    - It places shards in all cluster members of all cluster groups in a cluster system.
    - A shard can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster group and a cluster member.
- AT CLUSTER GROUP group_list 
    - It places hash shards in all cluster members of a specified cluster groups.
    - The number of group_list should be equal to or smaller than the value of &lt;hash shard count&gt;.
    - Unlike a range shard and a list shard, the cluster group on which the specific hash shard is to be located can not be specified, but the system automatically determines a cluster group on which the shard is to be located.
    - A shard can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster member in a specified cluster group.
    - Adding a cluster group does not affect the relocation of the hash shard.
- When it is omitted, the default value is AT CLUSTER WIDE.

<a id="af7f0d3286b335d4"></a>
#### &lt;range sharding strategy&gt;

It shards the table data according to the range value of the sharding key.

<a id="e8178e542fd23991"></a>
#### SHARDING BY RANGE ( column_list )

It defines a sharding key for the range sharding.

- It can list maximum 32 columns. 
- It can not use a duplicate column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="c7f7c0ee6f4523bf"></a>
#### &lt;cluster-wide range shard placement&gt;

It automatically places range shards in all cluster groups of a cluster system.  
AT CLUSTER WIDE statement is described before describing &lt;range shard definition&gt;.  
Shards can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster group and a cluster member.

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

<a id="b744f6ce20ff3771"></a>
#### &lt;group-specific range shard placement&gt;

It places range shards in a specified cluster group.  
It describes AT CLUSTER GROUP group_name statement which places that shard together with &lt;range shard definition&gt;.  
Shards can be automatically relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster member to a specified cluster group.  
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

<a id="26286eb6d599e56e"></a>
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

<a id="702e6b2cfd61358f"></a>
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

If a sharding key is defined by using multiple columns, a MAX shard which is listed with MAXVALUE for its all values like as the SHARD s3 below should exist.

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

<a id="d94aa50ea6ecea9a"></a>
#### &lt;list sharding strategy&gt;

It shards the table data according to the listed value of the sharding key.

<a id="3a674458deefe5d9"></a>
#### SHARDING BY LIST ( column_name )

It defines a sharding key for a list sharding.

- It can use only one column. 
- It can not use a LONG VARCHAR type column or a LONG VARBINARY type column.

<a id="ec06066b8bd76ab0"></a>
#### &lt;cluster-wide list shard placement&gt;

It automatically places list shards in all cluster groups of a cluster system.  
AT CLUSTER WIDE statement is described before describing &lt;range shard definition&gt;.  
Shards can be relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster group and a cluster member.

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

<a id="a9d3c9cd04cdb471"></a>
#### &lt;group-specific list shard placement&gt;

It places list shards in a specified cluster group.  
It describes AT CLUSTER GROUP group_name statement which places that shard together with &lt;list shard definition&gt;.  
Shards can be automatically relocated by using [ALTER TABLE name REBALANCE](#467720ee446849be) statement when adding a cluster member to a specified cluster group.  
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

<a id="c2b3d9de88531e8c"></a>
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

<a id="e0128bc27ff527e3"></a>
#### &lt;list value clause&gt;

&lt;list value&gt; should be a constant.  
NULL or DEFAULT can be used as &lt;list value&gt;.

- (O) SHARD s1 VALUES IN ( 1, 1 + 1, 3, 4 ) 
- (O) SHARD s2 VALUES IN ( 5, 6, 7, NULL ) 
- (O) SHARD s3 VALUES IN ( DEFAULT ) 
- (X) SHARD s4 VALUES IN ( DEFAULT, 8, 9, 10 ) 
- (X) SHARD s5 VALUES IN ( current_timestamp, systimestamp ) 
- (X) SHARD s6 VALUES IN ( c1, c2 )

<a id="1861b0eebcd90804"></a>
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

<a id="3219da3240931da4"></a>
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

<a id="7d9233898642c6f4"></a>
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

<a id="403830b28cd2754a"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="777c55b99ed5b667"></a>
#### TABLESPACE tablespace_name

It specifies the tablespace name in which a table is to be stored.  
If TABLESPACE clause is omitted, the default tablespace_name of the user performing the statement is used.

<a id="207bbcefe7276b57"></a>
#### LOGGING | NOLOGGING

It specifies whether to perform redo logging of the index.  
If not specified, the default value is NOLOGGING.

<a id="a416e29c91ae502a"></a>
#### TABLESPACE index_tablespace_name

It specifies the tablespace name in which an index is to be stored.  
If the TABLESPACE clause is omitted, LOGGING index uses the user's default data tablespace and NOLOGGING index uses the user's default temporary tablespace.

<a id="bce77acecf480a5e"></a>
#### &lt;constraint characteristics&gt;

It defines characteristics of the constraint.  
When defining constraints, the following characteristics can be set.

- DEFERRABLE | NOT DEFERRABLE
- &lt;constraint check time&gt;

If &lt;constraint characteristics&gt; is omitted, it is set to NOT DEFERRABLE INITIALLY IMMEDIATE.

<a id="c861ed70738a8ac6"></a>
#### DEFERRABLE | NOT DEFERRABLE

It sets whether the constraints checking is deferrable so that the constraints can be checked when executing COMMIT without checking when executing DML statements.

The checking time of the deferrable constraint is controlled by [SET CONSTRAINTS](#8337ae2c011b78f5).

- NOT DEFERRABLE
    - The checking point is not deferrable, and the constraints are checked when executing INSERT/DELETE/UPDATE statements. 
- DEFERRABLE
    - The checking point can be controlled by [SET CONSTRAINTS](#8337ae2c011b78f5) statement.
    - SET CONSTRAINTS constraint_name IMMEDIATE
        - The constraint is checked when executing DML statement. 
    - SET CONSTRAINTS constraint_name DEFERRED
        - The constraint is checked when executing COMMIT statement. 
- If not specified, the default value is determined in accordance with the &lt;constraint check time&gt;.
    - If INITIALLY IMMEDIATE is specified, the constraint check time is NOT DEFERRABLE.
    - If INITIALLY DEFERRED is specified, the constraint check time is DEFERRABLE.
    - If &lt;constraint check time&gt; is not specified, the constraint check time is NOT DEFERRABLE.

<a id="7fc6a5701b6d243d"></a>
#### &lt;constraint check time&gt;

If the constraints are DEFERRABLE, it sets an initial value for the checking time.

- INITIALLY IMMEDIATE
    - The constraint is checked when executing the DML statements. 
- INITIALLY DEFERRED
    - The constraint is checked when executing the COMMIT statements. 
    - It can not be used together with NOT DEFERRABLE.
- If not specified, the default value is INITIALLY IMMEDIATE.

For more information about the deferrable constraints, refer to [SET CONSTRAINTS](#8337ae2c011b78f5).

<a id="452fd4a3c81d224b"></a>
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

<a id="82a5d7cbba073fe7"></a>
### Description

<a id="1e1cc2d71676eb86"></a>
#### Constraint Characteristics

GOLDILOCKS automatically creates an index to check the uniqueness when generating key constraints.

The following columns do not allow NULL value.

- A column including NOT NULL constraint
- A column which is included in primary key constraints
- An identity column

<a id="58d9875ae3416277"></a>
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

<a id="fc011517e0962ab1"></a>
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

A global secondary index of table T1 is created in a tablespace USER_DATA_TBS with a logging option after creating a table T1.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      LOGGING TABLESPACE USER_DATA_TBS;

Table created.
```

A global secondary index of table T1 is created in a tablespace USER_TEMP_TBS with a nologging option after creating a table T1.

```
gSQL> CREATE TABLE T1 ( I1 INTEGER, I1 CHAR(32) ) 
      WITH GLOBAL SECONDARY INDEX
      NOLOGGING TABLESPACE USER_TEMP_TBS;

Table created.
```

<a id="58e4f6f99c14631e"></a>
### Compatibility

The SQL standard does not define the following clauses.

- The physical concepts of TABLESPACE clause and &lt;physical attribute clause&gt; clause. 
- The SQL standard does not allow an operation in DEFAULT clause.

**SQL standard compatibility**

<a id="a2d396db44869cb5"></a>
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

<a id="3300b1020b125fd7"></a>
### For More Information

Refer to the followings.

- [DROP TABLE](#b8225899a85c66e7)
- [ALTER TABLE](#90e40a320994005d)
- [CREATE TABLESPACE](#4fb45716ef9fbe7b)
- [CREATE SCHEMA](#671a916eb0910614)
- [CREATE INDEX](#11cedda99c2339bc)
- [CREATE SEQUENCE](#f57ec80975339322)
- [SET CONSTRAINTS](#8337ae2c011b78f5)
- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#a391d93da4c7cda3)

<a id="2908776ae1fc3e96"></a>
## CREATE TABLE AS SELECT

<a id="4d2778487ae93fd2"></a>
### Function

It creates a new table from the query result.

<a id="6561348829b8b319"></a>
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

<a id="eb6c3b7be39f84bc"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;table definition:AS query expression&gt;statement.

- Table creation privilege
    - Refer to the access privilege in [CREATE TABLE](#72507f5467c281c9).
- SELECT access privilege 
    - Refer to the access privilege in [SELECT](#1117040fd802dbd4).

<a id="c2cdd2f604e1097d"></a>
### Syntax Rules and Parameters

<a id="1d76e6b23ddc75aa"></a>
#### table_name

It is the table name to be created.  
For more information, refer to [table_name](#67a923a89b775405).

<a id="c6ea8af2fbe5cf9b"></a>
#### column_name_list

These are the names of the columns that configure the table, and it should be unique names within the table.  
The number of columns should be as same as the number of result columns in SELECT clause.  
If not specified, the column names of SELECT clause in &lt;query expression&gt; are used.

However, if an expression (such as a function, operation, or subquery) is used instead of a column in SELECT clause, the alias or column name should be specified.

The length of the column name should be shorter than 128 bytes.

<a id="6e0b649d6aa699a1"></a>
#### WITH [NO] DATA

If WITH DATA is specified, the result of SELECT clause is inserted to the table to be created.  
If WITH NO DATA is specified, the result of SELECT clause is not inserted to the table to be created.   
If not specified, it is operated as same as when WITH DATA is specified.

<a id="74b8e85a21652e9b"></a>
#### Other Syntax

For more information about other syntaxes, refer to the syntax in [CREATE TABLE](#72507f5467c281c9) statement.

<a id="7b66b1e0a0567fe0"></a>
### Description

When executing CREATE TABLE AS SELECT, if a column including a  NOT NULL constraint is specified in SELECT list, the NOT NULL constraint is also created in the new table.  
However, if the NOT NULL constraint is deferrable, then NOT NULL constraint is not created in the new table.

On the other hand, the NOT NULL constraint is not created in the new table if NOT NULL constraint was not explicitly created but there is NOT NULL property such as primary key column or identity column.

<a id="795ffd42e3ce3d46"></a>
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

<a id="89c397dad4ab9e8f"></a>
### Compatibility

CREATE TABLE AS SELECT statement follows SQL standard. However, the following is an extension of SQL standard.

- SQL standard requires parentheses outside SELECT clause, but it is optional in GOLDILOCKS. 
- SQL standard requires WITH [NO] DATA clause, but it is optional in GOLDILOCKS. 
- The concepts of tablespace in GOLDILOCKS is an extended concept, and it is not supported in SQL standard.

**SQL standard compatibility**

<a id="1962d60d890842d0"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T172 | AS subquery clause in table definition | O |

<a id="4853b70782b3ccc4"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#72507f5467c281c9)
- [SELECT](#1117040fd802dbd4)

<a id="5d245a0d6b896d4d"></a>
## CREATE GLOBAL TEMPORARY TABLE

<a id="77ffd667bf5fa029"></a>
### Function

It creates a new global temporary table.

<a id="221a86deea020e66"></a>
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

> The definition of &lt;table element&gt; is as same as those in &lt;table_definition&gt;.  
> For more information, refer to [CREATE TABLE](#72507f5467c281c9).

<a id="05f20ecbe235a7c5"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;global temporary table definition&gt; statement.

- Table creation privilege
    - Refer to the access privilege in [CREATE TABLE](#72507f5467c281c9).
- SELECT access privilege 
    - Refer to the access privilege in [SELECT](#1117040fd802dbd4).

<a id="8a8a7a22c57ce36f"></a>
### Syntax Rules and Parameters

<a id="d5e7e8b02cc6f3f6"></a>
#### table_name

It is the table name to be created.  
For more information, refer to [table_name](#67a923a89b775405).

<a id="62d33305732c5f1d"></a>
#### other syntax

For more information about other syntaxes, refer to the syntax in [CREATE TABLE](#72507f5467c281c9) and in [CREATE TABLE AS SELECT](#2908776ae1fc3e96) statement.

<a id="29da65287dc0a2e7"></a>
### Description

GLOBAL TEMPORARY TABLE is used to store the data which is maintained while a transaction or a session is performed.   
It is used for the purpose as same as that of the variable of which a developer temporarily stores the mid-data of the operation when developing an application.

The global temporary table has the following features.

- The definition of the global temporary table can be viewed in every session. 
- The physical segment is not allocated when defining the global temporary table, but the segment subordinated to that session is allocated when it is inserted for the first time.
- The data of the global temporary table can be viewed in a session or a transaction which was inserted.
- The tablespace to store the data of the global temporary table is determined as follows.

<a id="9b7fe32b4e693214"></a>
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

<a id="4c53c28abdb8118b"></a>
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

<a id="46688e1c51eda833"></a>
| TEMP_UNDO_ENABLED value | Description |
| --- | --- |
| TRUE | The undo log is recorded in the default temporary tablespace of the database system. |
| FALSE | The undo log is recorded in the undo tablespace of the database system. |

- TRUNCATE command for the global temporary table truncates only the segment of the corresponding session.
- If the session is terminated, all segments are TRUNCATEd and then returned.

<a id="4bfac807e8084baf"></a>
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

<a id="5100764f0c9e6992"></a>
### Compatibility

CREATE GLOBAL TEMPORARY TABLE and CREATE GLOBAL TEMPORARY TABLE AS SELECT statements follow the definition of SQL standard &lt;table definition&gt;. However, the following is an extension of SQL standard.

- SQL standard requires parentheses outside SELECT clause, but it is optional in GOLDILOCKS.
- SQL standard requires WITH [NO] DATA clause, but it is optional in GOLDILOCKS.
- The concepts of tablespace in GOLDILOCKS is an extended concept, and it is not supported in SQL standard.

**SQL standard compatibility**

<a id="5baeccda8ce3628b"></a>
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

<a id="9886c9a6c24d914e"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](#72507f5467c281c9)
- [CREATE TABLE AS SELECT](#2908776ae1fc3e96)

<a id="4fb45716ef9fbe7b"></a>
## CREATE TABLESPACE

<a id="45155654b49d7f78"></a>
### Function

It creates a tablespace.

<a id="a42003ae67955d2b"></a>
### Syntax

```
<create tablespace statement> ::=
      <memory data tablespace statement>
    | <memory temporary tablespace statement>
    ;
```

<a id="b62bbb7c0fe29db0"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;create tablespace statement&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="b66ab90c473eaa96"></a>
### Syntax Rules and Parameters

<a id="eacdaa850d754249"></a>
#### &lt;memory data tablespace statement&gt;

- [ MEMORY ] TEMPORARY

It is a memory temporary tablespace to store the no logging indexes or the temporary objects such as intermediate results which are generated during the query processing.  
The reserved word MEMORY can be omitted.

<a id="d5f7f4edaaf956b6"></a>
#### &lt;memory data tablespace clause&gt;

It defines a memory data tablespace.  
For more information, refer to [CREATE MEMORY DATA TABLESPACE](#b0ee56c9e33dadf5).

<a id="c7aa87b50cbee1c6"></a>
#### &lt;memory temporary tablespace definition&gt;

It defines a memory temporary tablespace.  
For more information, refer to [CREATE MEMORY TEMPORARY TABLESPACE](#3ddf803b50db6f27).

<a id="bcbf8b487b9e9fb3"></a>
### Description

For more information, refer to the description of each detailed statement.

<a id="616bc63cb6a82597"></a>
### Example

For more information, refer to usage example of each detailed statement.

<a id="561b49235967b8d2"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="8f1fea6118715a2e"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#ee3406f353c996e6)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)

<a id="b0ee56c9e33dadf5"></a>
## CREATE MEMORY DATA TABLESPACE

<a id="02671893d00becae"></a>
### Function

It defines a memory data tablespace.

<a id="8783afb81877dc85"></a>
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

<a id="31a13354e16ef6d4"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;memory data tablespace definition&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="9927f4e8f4e907ff"></a>
### Syntax Rules and Parameters

<a id="2748cf4dab8a57b6"></a>
#### [ MEMORY ] [ DATA ]

It is a memory tablespace to store the permanent objects such as tables, indexes, etc.  
The reserved words, MEMORY and DATA, can be omitted.

<a id="3805f3f06dc2f223"></a>
#### tablespace_name

It is the tablespace name to be created.  
The length of the tablespace name should be shorter than 128 bytes.

<a id="a8d022de19a5a5fd"></a>
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
        - determined by MEMORY_DATA_TABLESPACE_SIZE property in case of the data tablespace.
        - determined by MEMORY_TEMP_TABLESPACE_SIZE property in case of the temporary tablespace.

- SIZE &lt;size clause&gt; REUSE 
    - If both SIZE clause and REUSE clause are specified, it is operated as follows according to the presence of the filename.
        - For the new filename, the initial file size is assigned by using the SIZE clause.
        - For the existing filename, the size is adjusted to the value of SIZE clause by using the existing file.

<a id="5e133a8e6f5ffac6"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0f51be9413978283"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="af14d59d42d0b199"></a>
#### ONLINE | OFFLINE

It sets ONLINE or OFFLINE of the tablespace.

- ONLINE is the state which a tablespace can be used as soon as it is created.
- OFFLINE is the state which a tablespace is unable to be used, it can be used after switching to ONLINE state.

<a id="1aee7bff17a70769"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies extent size of the tablespace.

- The extent size is specified in bytes, and one of the five (64K, 128K, 256K, 512K, 1M) is selected.
- If the extent size is defined as a value between 64K ~ 128K, 128K is set. If the extent size is defined as 1M or bigger, 1M is set.

<a id="54d6342f197ed324"></a>
### Description

The data tablespace is an object which provides the physical space to store the SQL schema object such as a table, an index (with LOGGING option).

<a id="b427e19b44798ef3"></a>
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

<a id="99596b5a1eb1cc0f"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="d22b2d547f6e1311"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#ee3406f353c996e6)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)

<a id="3ddf803b50db6f27"></a>
## CREATE MEMORY TEMPORARY TABLESPACE

<a id="f9b88a66055205e3"></a>
### Function

It defines a memory temporary tablespace.

<a id="82fb3ccc5f5d41d6"></a>
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

<a id="ef7c198fa1f96931"></a>
### Invocation and Access Rules

CREATE TABLESPACE ON DATABASE privilege is required to perform &lt;memory temporary tablespace definition&gt;.

The user who performed the statement has CREATE OBJECT ON TABLESPACE privilege on the created tablespace.

One of the following privileges is required to create the objects on the created tablespace.

- CREATE OBJECT ON TABLESPACE for the tablespace.
- USAGE TABLESPACE ON DATABASE

<a id="07507d118f09ae2b"></a>
### Syntax Rules and Parameters

<a id="dcc9bf47a0275663"></a>
#### [ MEMORY ] TEMPORARY

It is a memory temporary tablespace to store the no logging indexes or the temporary objects such as intermediate results which are generated during the query processing.  
The reserved word, MEMORY, can be omitted.

<a id="56f727ff6388461c"></a>
#### tablespace_name

It is the tablespace name to be created.  
The length of the tablespace name should be shorter than 128 bytes.

<a id="4781565a80069d9a"></a>
#### &lt;memory clause&gt;

- 'memory_name' 
    - It is a memory name to store the temporary data.
    - memory_name should be guaranteed to be unique within the tablespace.
    - The length of the memory_name should be shorter than 1024 bytes.
- SIZE &lt;size clause&gt; 
    - It specifies the initial size.
    - It can be specified between minimum 1M and maximum 30G.

<a id="ec7b37c6df8aae5e"></a>
#### &lt;size clause&gt;

It specifies the size of shared memory space in bytes.(If it is omitted, the default unit is bytes.)  
The image is not managed as a file in case of the temporary memory data.

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="fc1b8e50a949f0d4"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="521e04d262b1be5d"></a>
#### EXTSIZE &lt;size clause&gt;

It specifies extent size of the tablespace.

- The extent size is specified in bytes, and one of the five (64K, 128K, 256K, 512K, 1M) is selected.
- If the extent size is defined as a value between 64K ~ 128K, 128K is set. If the extent size is defined as 1M or bigger, 1M is set.

<a id="b0362f8ff027b999"></a>
### Description

The temporary tablespace is an object which provides the physical space to store the SQL schema object such as an index (with NOLOGGING option), and to store the intermediate results for sorting, hashing during the query processing.

<a id="9baa27ce892de171"></a>
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

<a id="68429a05b6fbabc9"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="2c1ba9a0b85aef3b"></a>
### For More Information

Refer to the followings.

- [DROP TABLESPACE](#ee3406f353c996e6)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)

<a id="524780362f90ebc8"></a>
## CREATE USER

<a id="2bff7d3bfddd6f66"></a>
### Function

It defines a database user.

<a id="b120f8cc77beecee"></a>
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

<a id="c94944e434336246"></a>
### Invocation and Access Rules

CREATE USER ON DATABASE privilege is required to perform &lt;user definition&gt;.

The created user, user_identifier, has the privilege, which is the owner the schema created by using &lt;schema clause&gt;.

> A separate privilege is not granted to the created user_identifier.   
> The appropriate privileges should be granted to user_identifier to access and perform SQL statements.

<a id="ec25c7621f53f9d0"></a>
### Syntax Rules and Parameters

<a id="f0417eeea879affb"></a>
#### user_identifier

It is the username to be created.  
The identical username (user identifier) or role (role name) should not exist.  
The length of user_identifier should be shorter than 128 bytes.

<a id="b3838f0a5e914d91"></a>
#### password

It is the user's password to be created. It is encrypted and stored.  
The length of password should be shorter than 128 bytes.  
The password should start with an alphabetic character, and it can include alphabetic characters, numbers, underscore (_), and $.   
The other special characters should be enclosed in double quotes (").

<a id="3ac3b17b7d8ca871"></a>
#### PROFILE { profile_name | DEFAULT | NULL }

The profile for password management policy is assigned.

- PROFILE profile_name
    - It allocates the profile_name which is created by a user. 
- PROFILE DEFAULT
    - It allocates the default profile "DEFAULT". 
- PROFILE NULL
    - It does not allocate the profile.

If PROFILE clause is omitted, it is as same as PROFILE NULL, and the profile is not applied.  
For more information about the password management policy, refer to [CREATE PROFILE](#b8608593e7c730f3).

<a id="d15598de26c6ec09"></a>
#### PASSWORD EXPIRE

It expires the user's password.  
It is used when a user attempts to change the password by force before login.

<a id="c58824694e352bce"></a>
#### ACCOUNT { LOCK | UNLOCK }

- ACCOUNT LOCK
    - It locks the user account. 
- ACCOUNT UNLOCK
    - It unlocks the user account.

<a id="7ddfbb8e427315b8"></a>
#### DEFAULT TABLESPACE tablespace_name

It specifies the default TABLESPACE to store objects such as the table created by the user, the indexes (with NOLOGGING option).  
If DEFAULT TABLESPACE clause is omitted, default data tablespace(MEM_DATA_TBS) is specified, which was defined when creating DATABASE.

<a id="81993aecdfb51775"></a>
#### TEMPORARY TABLESPACE tablespace_name

It specifies the TABLESPACE which stores the temporary tables created by a user, indexes (NO LOGGING), and the intermediate results generated by the query processing.  
If TEMPORARY TABLESPACE clause is omitted, default temporary tablespace (MEM_TEMP_TBS) is specified, which was defined when creating DATABASE.

<a id="33bdca3a624ef5e9"></a>
#### INDEX TABLESPACE { tablespace_name | NULL }

It specifies the default TABLESPACE which stores the index objects created by a user.

- Specifying INDEX TABLESPACE tablespace_name
    - If it specifies the data tablespace, then it should be the LOGGING index.
    - If it specifies the temporary tablespace,then it should be the NOLOGGING index.

- INDEX TABLESPACE NULL
    - It does not specify the index tablespace.

If INDEX TABLESPACE clause is omitted, then it is INDEX TABLESPACE NULL.

<a id="b6f686c4200c63df"></a>
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
The schema to be owned by the user can be additionally created by using [CREATE SCHEMA](#671a916eb0910614) statement.

<a id="9e0818dc60230038"></a>
### Description

A user is an authorization object which consists of a set of privileges.

When &lt;user definition&gt; statement is executed for the first time, a user without any privilege is created, and the appropriate privileges should be granted as follows.

In GOLDILOCKS, the relationship between user and schema is 1 : N.  
In other words, a user does not own any schema, or a user can own multiple schemas.

The SQL standard does not explicitly define the relationship of the non-schema objects such as a user, a schema, or a database. Each DBMS defines the relationship of non-schema objects in different concept as follows.

> The relationship between user and schema in other DBMS.  
>   
> • Oracle  
>  ° User : schema = 1 : 1.  
>   
> • DB2   
>  ° It is as same as the OS user.  
>  ° The separate SQL statements which creates or deletes a user do not exist.  
>   
> • Postgres   
>  ° User : schema = 1 : N.   
>   
> • MySQL   
>  ° Database : schema = 1 : 1.  
>  ° User is a subordinate object of database (schema).

<a id="934e0bec0913b6a4"></a>
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

<a id="a3abc3c1ee5a3b8b"></a>
### Compatibility

The SQL standard covers the concepts of the user, but it does not define the SQL statements associated with the creation and deletion of user.

<a id="580d12eb94936b3f"></a>
### For More Information

Refer to the followings.

- [DROP USER](#75a505d0fbae98f3)
- [ALTER USER](#ed40a6862d9c8f12)
- [CREATE SCHEMA](#671a916eb0910614)

<a id="ae5c14874ae12b2e"></a>
## CREATE VIEW

<a id="a7b5248d99637058"></a>
### Function

It defines a view.

<a id="022c40043f47c8ff"></a>
### Syntax

```
<view definition> ::=
    CREATE [ OR REPLACE ] [ FORCE | NO FORCE ] 
        VIEW view_name [ ( column_name [, ...] ) ]
        AS <query expression>
    ;
```

<a id="93144e97e3c6d3b3"></a>
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

<a id="c56d7f578857af38"></a>
### Syntax Rules and Parameters

<a id="0a765e7c72097c0f"></a>
#### [ OR REPLACE ]

It replaces the existing view when a view already exists.

<a id="8065db009dca92cf"></a>
#### [ FORCE | NO FORCE ]

- FORCE 
    - A view is created regardless of the validity of &lt;query expression&gt;.
- NO FORCE 
    - A view is created when &lt;Query expression&gt; is valid.
- The default value is NO FORCE.

<a id="53549ae836a23549"></a>
#### view_name

It is the view name to be created, and it should be a unique name within the schema.  
The schema to which the view belongs, such as schema_name.view_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The length of the view name must be shorter than 128 bytes.

<a id="3df151fcf342f7b6"></a>
#### [ ( column_name [, ...] ) ]

It defines a column name which will configure the view.  
Each column name should be unique within the view.

The number of columns should be as same as the number of result columns in SELECT clause.

If the list of column names is omitted, the column names of SELECT clause in &lt;query expression&gt; are used.

<a id="ddd11abbe5d21123"></a>
##### AS &lt;query expression&gt;

It is the [SELECT](#1117040fd802dbd4) query which will create a view.

&lt;query expression&gt; can not include the following variables.

- Host parameter 
- SQL parameter 
- Dynamic parameter 
- Embedded variable 
- SEQUENCE object

<a id="b727068aaabbceac"></a>
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

<a id="0085c405c2545f5a"></a>
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

<a id="29197019dea2eb82"></a>
### Compatibility

The SQL standard does not define the following clauses.

- [ OR REPLACE ] clause 
- [ FORCE | NO FORCE ] clause

**SQL standard compatibility**

<a id="a8c9a27b041dd5fd"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T131 | Recursive query | X |
| F751 | View CHECK enhancements | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F859 | Top-level &lt;fetch first clause&gt; in views | O |
| S081 | Subtables | X |

<a id="886f1effc98ba9f4"></a>
### For More Information

Refer to the followings.

- [DROP VIEW](#c3d4597ac53c944b)
- [ALTER VIEW](#062be61ee2ec0848)
- [SELECT](#1117040fd802dbd4)

<a id="9826eadcd321de1b"></a>
## DECLARE cursor_name

<a id="ca8c5b3d45fcbb86"></a>
### Function

It declares a cursor.

<a id="30d572f84dd78468"></a>
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

<a id="b5767b7addceaf83"></a>
### Invocation and Access Rules

The dynamic cursor which uses statement_name can be used in an embedded SQL.

An appropriate access privilege is required depending on &lt;cursor query&gt; types.  
For more information about the access privileges, refer to the followings.

- The access privilege of a [SELECT](#1117040fd802dbd4) statement
- The access privilege of a [SELECT .. FOR UPDATE](#f7fb3657b7896855) statement
- The access privilege of a [INSERT INTO name RETURNING](#6e07672cf5aedd6b)statement
- The access privilege of a [UPDATE name RETURNING](#247a80e4d8b5ad3d)statement
- The access privilege of a [DELETE FROM name RETURNING](#6806f9f54690d5b6)statement

<a id="6ebf8b3a6669fc10"></a>
### Syntax Rules and Parameters

<a id="4e42ad8a11c15b5d"></a>
#### cursor_name

It is the cursor name to be declared.  
It should be a unique name within the session.  
The length of cursor name should be shorter than 128 bytes.

<a id="81b110be407f589e"></a>
#### { FOR | IS }

Either FOR or IS is used as a syntax keyword in SQL standard.

<a id="ce5e4fbeae909093"></a>
#### &lt;cursor properties&gt;

It defines the cursor properties.

- If &lt;cursor sensitivity&gt; is not specified, the default value is INSENSITIVE. 
- If &lt;cursor scrollability&gt; is not specified, the default value is NO SCROLL. 
- If &lt;cursor holdability&gt; is not specified, the default value is determined by &lt;cursor updatability&gt;.

<a id="93d5ae05cf34903e"></a>
#### updatable query

To use a cursor property such as SENSITIVE or FOR UPDATE, a query of the cursor should identify changes in rows of the base table, or it should be the updatable query which can acquire a lock on the row.

The updatable query should satisfy all of the following conditions.

- DISTINCT should not exist at the top level query.
    - (X) SELECT DISTINCT * FROM t1;
- GROUP BY, HAVING, aggregation function should not exist at the top level query.
    - (X) SELECT MAX(c1) FROM t1;
- A returning query should not exist. 
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

<a id="38f70c13ded9da2f"></a>
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

<a id="e40ba2043461ec2b"></a>
#### &lt;cursor scrollability&gt;

It specifies whether the result set of the cursor can be fetched sequentially or non-sequentially.

- NO SCROLL 
    - Only sequential FETCH (FETCH NEXT) is possible. 
- SCROLL 
    - Non-sequential FETCH is possible.
- If not specified, the default value is NO SCROLL.

<a id="d12dcf895a4f8b79"></a>
#### &lt;cursor holdability&gt;

It determines whether the cursor is maintained after the cursor is OPEN and the transaction is committed.

- WITH HOLD 
    - The cursor is maintained after the transaction is committed.
    - It can not be used together with FOR UPDATE statement.
    - It can not be used together with [INSERT INTO name RETURNING](#6e07672cf5aedd6b) statement. 
    - It can not be used together with [UPDATE name RETURNING](#247a80e4d8b5ad3d) statement. 
    - It can not be used together with [DELETE FROM name RETURNING](#6806f9f54690d5b6) statement.

- WITHOUT HOLD 
    - When the transaction is committed or rolled back, the cursor is closed.

- Rollback and cursor
    - It closes a cursor included in a transaction when rolling back the transaction.
    - It closes a cursor created since the savepoint when rolling back up to the savepoint.

- If not specified, the default value of &lt;cursor holdability&gt; is determined by &lt;cursor updatability&gt;.
    - If it is FOR READ ONLY or &lt;cursor updatability&gt; is not specified, the default value is WITH HOLD. 
    - If it is used together with FOR UPDATE statement, the default value is WITHOUT HOLD.

<a id="5a4d4a7b16455442"></a>
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

<a id="372bfd9d7bbd70b4"></a>
| Updatability | Query type | Sensitivity |
| --- | --- | --- |
| FOR UPDATE | Updatable query | SENSITIVE |
| FOR UPDATE | Non-updatable query | Query error |
| FOR READ ONLY | Any query | INSENSITIVE |
| N/A | Updatable query | SENSITIVE |
| N/A | Non-updatable query | INSENSITIVE |

<a id="a6dbbeb2d6a06f20"></a>
#### &lt;cursor specification&gt;

It defines a query which is a target of the cursor.  
If statement_name is used, a dynamic cursor whose query has not been defined is declared.  
If &lt;cursor query&gt; is used, a standing cursor whose query is defined is declared.

<a id="1e00f7be96736421"></a>
#### statement_name

It is a statement_name to be referenced by the cursor, and it can be used in an embedded SQL.

statement_name should exist before performing &lt;declare cursor&gt; statement, and the SQL statement referenced by statement_name should be the query prepared by [PREPARE statement_name](#897dbc4fb97ab869) statement.

If it is not a query, an error occurs when executing [OPEN cursor_name](#503dadf63d95d09e) statement.

<a id="0c5a221463cc610d"></a>
#### &lt;cursor query&gt;

For more information about available query types in the cursor, refer to the followings.

- [SELECT](#1117040fd802dbd4)
- [SELECT .. FOR UPDATE](#f7fb3657b7896855)
- [INSERT INTO name RETURNING](#6e07672cf5aedd6b)
- [UPDATE name RETURNING](#247a80e4d8b5ad3d)
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)

<a id="f79295e16e679fcc"></a>
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

<a id="416c9c94fbc78e9c"></a>
#### FOR UPDATE OF …

It lists the columns associated with the lock obtaining when OPENing the cursor.

- If it is the columns listed in FOR UPDATE OF statement
    - It should be an updatable column of the table listed in FROM clause of &lt;select statement&gt;.
    - It acquires the lock for the table of listed columns. 
- If only FOR UPDATE statement is used
    - It is the same meaning as listing all updatable columns of the table in FROM clause of &lt;select statement&gt;.
    - It acquires the lock for the table of all columns.

<a id="48f259714f793f7e"></a>
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

<a id="aedae8408e15c463"></a>
### Description

When controlling the query property, using DECLARE CURSOR, OPEN, FETCH, CLOSE statements have the performance burden compared to using the cursor with the ODBC or JDBC statements. It is because using DECLARE CURSOR, OPEN, FETCH, CLOSE statements control the cursor of the server.

Before executing the query, the cursor property can be controlled by ODBC statement and JDBC statement. The SQL cursor property control method by DECLARE CURSOR statement, and cursor property control method by the ODBC standard and the JDBC standard are as follows.

<a id="2c5c5b9ef9531b74"></a>
<table class="table column_count_4"><caption>Controlling the cursor property of ODBC/ JDBC</caption><thead><tr><th class="to_center to_middle"><div>Property</div></th><th class="to_center to_middle"><div>GOLDILOCKS 
cursor property</div></th><th class="to_center to_middle"><div>ODBC standard cursor property</div></th><th class="to_center to_middle"><div>JDBC standard cursor property</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>Sensitivity</div></td><td class="to_left to_middle"><div>INSENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_INSENSITIVE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>SENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_SENSITIVE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>ASENSITIVE</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SENSITIVITY, SQL_UNSPECIFIED, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Scrollability</div></td><td class="to_left to_middle"><div>NO SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_NONSCROLLABLE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle"><div>SCROLL</div></td><td class="to_left to_middle"><div>SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_SCROLLABLE, SQL_SCROLLABLE, len)</div></td><td class="to_left to_middle"><div>It can not be set.</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>Holdability</div></td><td class="to_left to_middle"><div>WITHOUT HOLD</div></td><td class="to_left to_middle"><div>It can not be set.</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.CLOSE_CURSORS_AT_COMMIT )</div></td></tr><tr><td class="to_left to_middle"><div>WITH HOLD</div></td><td class="to_left to_middle"><div>It can not be set.</div></td><td class="to_left to_middle"><div>java.sql.Connection::prepareStatement( query, type, conc, ResultSet.HOLD_CURSORS_OVER_COMMIT )</div></td></tr></tbody></table>

SQL cursor declaration corresponding to ODBC cursor type is as follows.

**SQL cursor declaration corresponding to ODBC cursor type**

<a id="eb923ada30280015"></a>
| ODBC cursor type | SQL cursor declaration |
| --- | --- |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, len) | NO SCROLL CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, len) | STATIC CURSOR |
| SQLSetStmtAttr(stmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, len) | KEYSET CURSOR |

SQL cursor declaration corresponding to JDBC cursor type is as follows.

**SQL cursor declaration corresponding to JDBC cursor type**

<a id="40e25ebd5feec466"></a>
| JDBC cursor type | SQL cursor declaration |
| --- | --- |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_FORWARD_ONLY, conc, hold ) | INSENSITIVE NO SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_INSENSITIVE, conc, hold ) | INSENSITIVE SCROLL CURSOR |
| java.sql.Connection::prepareStatement( query, ResultSet.TYPE_SCROLL_SENSITIVE, conc, hold ) | KEYSET CURSOR |

<a id="d704a8311e0cc907"></a>
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

<a id="9117fd090d652523"></a>
### Compatibility

&lt;declare cursor&gt; statement has the following differences compared to the SQL standard.

- In SQL standard, the default value of &lt;cursor sensitivity&gt; is ASENSITIVE, but in GOLDILOCKS, the default value is INSENSITIVE.
- The SQL standard does not cover the following &lt;odbc cursor type&gt;.
    - STATIC CURSOR 
    - KEYSET CURSOR 
- In SQL standard, the default value of &lt;cursor holdability&gt; is WITHOUT HOLD, but in GOLDILOCKS, the default value depends on &lt;cursor updatability&gt;.
- SQL standard can use only &lt;select statement&gt; as &lt;cursor query&gt;, but GOLDILOCKS can use the returning query as follows.
    - [INSERT INTO name RETURNING](#6e07672cf5aedd6b)
    - [UPDATE name RETURNING](#247a80e4d8b5ad3d)
    - [DELETE FROM name RETURNING](#6806f9f54690d5b6)
- In SQL standard, the default value of &lt;cursor updatability&gt; is determined by &lt;select statement&gt;, but in GOLDILOCKS the default value is FOR READ ONLY.
- In SQL standard, &lt;lock wait mode&gt; statement does not exist.

**SQL standard compatibility**

<a id="7c46a7957d6255e3"></a>
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

<a id="6aaa072864caf116"></a>
### For More Information

Refer to the followings.

- [OPEN cursor_name](#503dadf63d95d09e)
- [FETCH cursor_name](#8b90e7e7e6e0c963)
- [CLOSE cursor_name](#8094485dc3cb5ea5)
- [PREPARE statement_name](#897dbc4fb97ab869)
- [SELECT](#1117040fd802dbd4)
- [SELECT .. FOR UPDATE](#f7fb3657b7896855)
- [INSERT INTO name RETURNING](#6e07672cf5aedd6b)
- [UPDATE name RETURNING](#247a80e4d8b5ad3d)
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)

<a id="c496862da559967a"></a>
## DELETE FROM

<a id="5019375c4fd7c3e2"></a>
### Function

It deletes rows in a table.

<a id="a78c262f38bd5e77"></a>
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

<a id="6c4818c20c0cf89e"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;delete statement: searched&gt;.

- (DELETE or CONTROL TABLE) ON TABLE for the table
- (DELETE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DELETE ANY TABLE ON DATABASE

<a id="2efeb22056b631e9"></a>
### Syntax Rules and Parameters

<a id="d3b3327eaafe4fa4"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.  
It defines the schema to which the table belongs such as schema_name.table_name.   
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="d2a970e84c6041d8"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="d28b7065c7a7fdd1"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
If WHERE condition is omitted, it deletes all rows.  
For more information about WHERE condition, refer to [where clause](#12ec541722ce6e3e) of [SELECT](#1117040fd802dbd4) statement.

<a id="0a625bd394123e36"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [offset limit clause](#a7e3de58d6de6bbb) of [SELECT](#1117040fd802dbd4) statement.

<a id="66bcf11bd87e110f"></a>
#### &lt;fetch limit clause&gt;

The following two ways are used to specify the number of rows to be fetched.

- &lt;fetch first clause&gt;
    - It specifies the number of rows to be fetched. 
    - For more information, refer to [&lt;fetch first clause&gt;](#89f9ac4af34ef519) of [SELECT](#1117040fd802dbd4) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.
    - For more information, refer to [&lt;limit clause&gt;](#765d5e71a89c2751) of [SELECT](#1117040fd802dbd4) statement.

<a id="b04499b176ae2ff9"></a>
### Description

<a id="e042b264c1a9c06f"></a>
#### Differences among DELETE-related Statements

- [DELETE FROM](#c496862da559967a)
    - It deletes multiple rows which satisfy conditions. 
    - e.g. DELETE FROM t1 WHERE c1 = 0; 
- [DELETE FROM name WHERE CURRENT OF cursor_name](#557c797ddb6c8af5)
    - It deletes the row which the current cursor indicates.
    - e.g. DELETE FROM t1 WHERE CURRENT OF cursor; 
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)
    - It deletes multiple rows which satisfy the conditions, and the deleted rows can be retrieved in the same way as [SELECT](#1117040fd802dbd4) statement (API such as SQLFetch ()).
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2; 
- [DELETE FROM name RETURNING .. INTO](#1a665c9644be2b50)
    - It deletes row equal to or less than one, and if one row is deleted, the value is obtained into the host variable of RETURNING INTO clause.
    - e.g. DELETE FROM t1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="1e47e055fb9a7616"></a>
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

<a id="ec269dac656ca9c4"></a>
### Compatibility

The SQL standard does not define the following clauses of DELETE statement.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL standard compatibility**

<a id="b82278fcad562f06"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="1af683c19b9f4d49"></a>
### For More Information

Refer to the followings.

- [DELETE FROM name WHERE CURRENT OF cursor_name](#557c797ddb6c8af5)
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)
- [DELETE FROM name RETURNING .. INTO](#1a665c9644be2b50)
- [SELECT](#1117040fd802dbd4)

<a id="6806f9f54690d5b6"></a>
## DELETE FROM name RETURNING

<a id="00bb95a38a02a60c"></a>
### Function

It deletes rows of the table, and retrieves the deleted rows.

<a id="abf8a2e1b2bf1fc7"></a>
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

<a id="b0e691d4239b99ef"></a>
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

<a id="9cc88f901597b3e8"></a>
### Syntax Rules and Parameters

<a id="d7886b3212cf8680"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="b120b684d322ce6c"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="b0f4320f9fb9e224"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="01a2ecd791df9ae0"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="9cea9956fb57d28a"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="f95e589baed899a6"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="15d22c977d0bacb9"></a>
#### &lt;returning clause&gt;

It sets the deleted rows as a result set, and it specifies the columns to be searched from the set.

- RETURNING clause returns the rows deleted by DELETE statement as a result set.
- &lt;value expression&gt; 
    - It is as same as &lt;select list&gt; of SELECT statement, but it can not use aggregation.
- [[AS] alias_name] 
    - It can give the name to the value expression by using AS clause.

The keywords RETURNING and RETURN have the same meaning.

<a id="509260aab1559f32"></a>
### Description

For more information, refer to [Differences among DELETE-related Statements](#e042b264c1a9c06f).

<a id="09bae0da8dce63ec"></a>
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

<a id="8b169fc9b120aaa7"></a>
### Compatibility

The SQL standard does not cover &lt;delete returning query statement&gt;.

<a id="c95abf606f16d872"></a>
### For More Information

Refer to the followings.

- [DELETE FROM](#c496862da559967a)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#557c797ddb6c8af5)
- [DELETE FROM name RETURNING .. INTO](#1a665c9644be2b50)
- [SELECT](#1117040fd802dbd4)

<a id="1a665c9644be2b50"></a>
## DELETE FROM name RETURNING .. INTO

<a id="38530236f4a8bb6d"></a>
### Function

It deletes a single row from the table, and the value of the deleted row is obtained into the host variable.

<a id="b08e5c10ad60021c"></a>
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

<a id="777dd458c7b1d898"></a>
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

<a id="987a73ab7d9413c1"></a>
### Syntax Rules and Parameters

<a id="473f4110ac6ff9ea"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="f25273a17461046a"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="ec9f9910101517f0"></a>
#### WHERE &lt;search condition&gt;

It deletes the rows which satisfy WHERE condition.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="0f963fe337003b3f"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to be skipped among the query result.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="953bdb169f238fba"></a>
#### &lt;fetch first clause&gt;

It specifies the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="c7673ea87e1425ec"></a>
#### &lt;limit clause&gt;

It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.  
For more information, refer to [DELETE FROM](#c496862da559967a) statement.

<a id="a5c04fb5ef43651a"></a>
#### &lt;returning into clause&gt;

- RETURNING .. AS ..
    - For more information, refer to &lt;returning clause&gt; of [DELETE FROM name RETURNING](#6806f9f54690d5b6) statement.
- INTO variable_name [, ...]
    - The number of variables specified in INTO clause should be equal to the number of the expressions specified in RETURNING clause.

<a id="7c07a69b6b18e95e"></a>
### Description

The number of rows to be deleted should be equal to or less than one.  
If two or more rows are deleted, then an error occurs.

For more information, refer to [Differences among DELETE-related Statements](#e042b264c1a9c06f).

<a id="052a7a42c02413ab"></a>
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

<a id="5efaee1b6c10a413"></a>
### Compatibility

The SQL standard does not cover &lt;delete returning into statement&gt;.

<a id="41729ae314bd42ee"></a>
### For More Information

Refer to the followings.

- [DELETE FROM](#c496862da559967a)
- [DELETE FROM name WHERE CURRENT OF cursor_name](#557c797ddb6c8af5)
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)
- [SELECT](#1117040fd802dbd4)

<a id="557c797ddb6c8af5"></a>
## DELETE FROM name WHERE CURRENT OF cursor_name

<a id="bc65f8257a337343"></a>
### Function

It deletes a single row which the cursor indicates.

<a id="66d40773055cb643"></a>
### Syntax

```
<delete statement: positioned> ::=
    DELETE [ FROM ] table_name [ [ AS ] alias_name ]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="eba4b89fbf9fbab7"></a>
### Invocation and Access Rules

The privilege to perform [DELETE FROM](#c496862da559967a) statement is required to perform &lt;delete statement: positioned&gt;.

<a id="fdc03eacd1bcd356"></a>
### Syntax Rules and Parameters

<a id="549f8448fa31d881"></a>
#### table_name

It is the name of a target table whose rows are to be deleted.

<a id="7bac7ba91a7c6b83"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="7312ac7b6e3de32d"></a>
#### cursor_name

The cursor corresponding to cursor_name should satisfy the following conditions.

- The cursor should be OPEN. (Refer to [OPEN cursor_name](#503dadf63d95d09e).) 
- Fetched rows by using the cursor should exist. (Refer to [FETCH cursor_name](#8b90e7e7e6e0c963).) 
- The query used for the cursor should identify table_name. (Refer to [DECLARE cursor_name](#9826eadcd321de1b).) 
- The cursor should be updatable for table_name. (Refer to [DECLARE cursor_name](#9826eadcd321de1b).)

<a id="7a0dc025f647580c"></a>
### Description

For more information, refer to [Differences among DELETE-related Statements](#e042b264c1a9c06f).

<a id="86b82d996d1ab9e3"></a>
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

<a id="ff6b76132d8556ba"></a>
### Compatibility

**SQL standard compatibility**

<a id="514b417d9c72cba4"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S111 | ONLY in query expressions | X |
| B031 | Basic dynamic SQL | O |

<a id="d04c1382bd62df94"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)
- [FETCH cursor_name](#8b90e7e7e6e0c963)
- [DELETE FROM](#c496862da559967a)
- [DELETE FROM name RETURNING](#6806f9f54690d5b6)
- [DELETE FROM name RETURNING .. INTO](#1a665c9644be2b50)

<a id="bd602160c2b9fd00"></a>
## DROP AUDIT POLICY

<a id="0da5441eaf299c4a"></a>
### Function

It drops an audit policy.

<a id="c179623696347861"></a>
### Syntax

```
<drop audit policy statement> ::= 
    DROP AUDIT POLICY [ IF EXISTS ] policy_name
;
```

<a id="f16db253524c47f7"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;drop audit policy statement&gt;.

<a id="bc564ec670698df7"></a>
### Syntax Rules and Parameters

<a id="d79323701768a209"></a>
#### IF EXISTS

An error does not occur even when a policy_name does not exist.

<a id="b6177e7427601560"></a>
#### policy_name

It is the name of an audit policy object to be dropped.

<a id="81d4c836f1a25f25"></a>
### Description

The audit policy object which is already activated can not be dropped. In this case, the audit policy should be deactivated by using NOAUDIT POLICY statement.

<a id="764fc8d1d30fdcb7"></a>
### Examples

The following is an example of dropping an audit policy.

```
DROP AUDIT POLICY policy_table;
```

<a id="fc6415941568a329"></a>
### Compatibility

In the SQL standard, an audit policy does not exist.

<a id="f7c9ea445a5414d8"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Retrieving audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="7335700144f62a07"></a>
## DROP CLUSTER GROUP

<a id="5e722acf84697a1c"></a>
### Function

It drops a cluster group from a cluster system.

<a id="e7a851a5f28628a6"></a>
### Syntax

```
<drop cluster group statement> ::=
    DROP CLUSTER GROUP [IF EXISTS] group_name
    ;
```

<a id="dc3ce4780b947570"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  
ADMINISTRATION ON DATABASE privilege is required to perform &lt;drop cluster group statement&gt;.

<a id="670b6b85ef8025c4"></a>
### Syntax Rules and Parameters

<a id="9af417f05556c648"></a>
#### [IF EXISTS]

An error does not occur even when a cluster group does not exist.

<a id="5b66beeeb277b5c7"></a>
#### group_name

It is the name of a cluster group.  
A cluster group without any shard can be dropped.

<a id="d5096c52c3d17902"></a>
### Description

A cluster group can be dropped only when dropping the cluster group does not cause the data loss.

<a id="4370caaad27b8c6c"></a>
### Examples

The following is an example of dropping a cluster group.

```
gSQL> DROP CLUSTER GROUP g3;

Cluster Group dropped.
```

<a id="d63156c9c608826d"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="c147c5750d861ac8"></a>
### For More Information

Refer to [CREATE CLUSTER GROUP](#f8131b333b91edb7).

<a id="7866e0152d6dec9e"></a>
## DROP CLUSTER LOCATION

<a id="1af9d98828d00820"></a>
### Function

It drops the access information of a cluster member.

<a id="312e2fddf58bbb0c"></a>
### Syntax

```
<drop cluster location statement> ::=
    DROP CLUSTER LOCATION member_name 
    ;
```

<a id="cb60c352d244a607"></a>
### Invocation and Access Rules

It can be performed in a cluster system.  
ADMINISTRATION ON DATABASE privilege is required to perform &lt;drop cluster location statement&gt;.

<a id="3ae9bf0467f0d91f"></a>
### Syntax Rules and Parameters

<a id="ec6c27dd2dcb5d40"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should exist in a registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="78c3e02337b10aab"></a>
### Description

Generally, the information of the cluster location is automatically created by using the connection information provided when creating the cluster group or adding the cluster member. The created information is deleted together when deleting the cluster member and the cluster group.

If the access information of the cluster location is modified, then the connection information can be modified by using [ALTER CLUSTER LOCATION](#ca28514ab71c220c) without deleting or recreating the cluster member.

<a id="2d9032307aedb31c"></a>
### Example

```
gSQL> 
DROP CLUSTER LOCATION g1n2
;

Created
```

<a id="b5f6e01dadb1acaf"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="a160a6a9d37aa80b"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER LOCATION](#648735809e94071b)
- [ALTER CLUSTER LOCATION](#ca28514ab71c220c)

<a id="9fbe418d2e4cd17c"></a>
## DROP INDEX

<a id="6bfe6439b64bde89"></a>
### Function

It drops an index.

<a id="3b1f2ee6bb7ecb88"></a>
### Syntax

```
<drop index statement> ::=
    DROP INDEX [ IF EXISTS ] index_name
    ;
```

<a id="c122b3a2111aff6a"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs
- (DROP INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- DROP ANY INDEX ON DATABASE

<a id="15ca57537df05028"></a>
### Syntax Rules and Parameters

<a id="af860711af6fc3ab"></a>
#### IF EXISTS

Even when the index does not exist, an error does not occur.

<a id="445a544201db7da6"></a>
#### index_name

It is the index name to be dropped.  
It can define schema to which the index belongs such as schema_name.index_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

The indexes created for UNIQUE constraint, PRIMARY KEY constraint can not be dropped.  
To drop the indexes created for the constraints above, the constraints should be removed through [ALTER TABLE name DROP CONSTRAINT](#5f73b4ecf07ae833) statement.

<a id="bf07ded85bad6790"></a>
### Description

Data Definition Language (DDL) statement such as DROP INDEX can be rolled back if it is before when the transaction is committed.

<a id="f7d15f8a61340664"></a>
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

<a id="7396ea692bb750fb"></a>
### Compatibility

The SQL standard does not cover the concepts of the index.

<a id="322a67f4bac5ee34"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](#11cedda99c2339bc)
- [DROP TABLE](#b8225899a85c66e7)
- [ALTER TABLE name DROP CONSTRAINT](#5f73b4ecf07ae833)

<a id="a176f22a83621a33"></a>
## DROP PROFILE

<a id="9770b9f20f015c03"></a>
### Function

It drops a profile.

<a id="58a4431a0030e16d"></a>
### Syntax

```
<drop profile statement> ::= 
    DROP PROFILE [ IF EXISTS ] profile_name [ CASCADE ] ;
```

<a id="77e2038b2a11718b"></a>
### Invocation and Access Rules

DROP PROFILE ON DATABASE privilege is required to perform &lt;drop profile statement&gt;.

<a id="23d6fd6dfb134fd9"></a>
### Syntax Rules and Parameters

<a id="1833640eb1dd73f7"></a>
#### IF EXISTS

Even when the profile does not exist, an error does not occur.

<a id="20eb6bdc4d254f16"></a>
#### profile_name

It specifies the profile name to be dropped.  
It can not drop the DEFAULT profile.

<a id="5deb1d9aa95a0cdb"></a>
#### CASCADE

If the profile has already been assigned to users, CASCADE clause should be explicitly specified to drop the profile.  
The profile which is assigned to users and to be dropped is changed to DEFAULT profile.

<a id="e05bd65c3a88a648"></a>
### Example

The following is an example of dropping a profile by using CASCADE statement.

```
gSQL> DROP PROFILE prof CASCADE;

Profile dropped.

gSQL> COMMIT;

Commit complete.
```

<a id="09a144a337ed551f"></a>
### Compatibility

The SQL standard does not cover the concepts of the profile.

<a id="8a8b687b9cc85819"></a>
### For More Information

Refer to the followings.

- [CREATE PROFILE](#b8608593e7c730f3)
- [ALTER PROFILE](#da7815275847e190)

<a id="406abccf7b931f83"></a>
## DROP SCHEMA

<a id="ac30f8f26df6f3d9"></a>
### Function

It drops a schema.

<a id="5be16a39bbcb7692"></a>
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

<a id="aeb2d1d852e764c0"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop schema statement&gt;.

- The owner of that schema
- CONTROL SCHEMA ON SCHEMA for the schema
- DROP SCHEMA ON DATABASE

<a id="a03e6a23fa35cf08"></a>
### Syntax Rules and Parameters

<a id="21ec5ebd6a19b888"></a>
#### IF EXISTS

Even when the schema does not exist, an error does not occur.

<a id="c8a2619fff572be4"></a>
#### schema_name

It is the schema name to be dropped.  
However, it can not drop the built-in schema such as "DICTIONARY_SCHEMA", "INFORMATION_SCHEMA" and "PUBLIC" which are automatically created when creating the database.

<a id="5e183de4c04f2ab7"></a>
#### &lt;drop behavior&gt;

- When it is RESTRICT 
    - Objects should not exist within the schema.
- When it is CASCADE 
    - It drops all objects in the schema together.
- When it is omitted, the default value is RESTRICT.

<a id="d96512c940fed6e1"></a>
### Description

Data Definition Language (DDL) statement such as DROP SCHEMA can be rolled back if it is before when the transaction is committed.

<a id="ac0adff110d2dafb"></a>
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

<a id="a7ed589e992cb44f"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="74baf3714470a01a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |
| F381 | Extended schema manipulation | O |

<a id="1a9a89e66c1c0d07"></a>
### For More Information

Refer to [CREATE SCHEMA](#671a916eb0910614).

<a id="98127fac6b27272b"></a>
## DROP SEQUENCE

<a id="eeef67bb069e0d91"></a>
### Function

It drops a sequence.

<a id="02ce0f10e2e0d73f"></a>
### Syntax

```
<drop sequence generator statement> ::=
    DROP SEQUENCE [ IF EXISTS ] [schema_name.] sequence_name 
    ;
```

<a id="3d08e6bb8ae38722"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop sequence generator statement&gt;.

- The owner of that sequence
- (DROP SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence belongs
- DROP ANY SEQUENCE ON DATABASE

<a id="d674fdc0b9cf3bc2"></a>
### Syntax Rules and Parameters

<a id="6a19be3c93a2b919"></a>
#### IF EXISTS

Even when the sequence does not exist, an error does not occur.

<a id="8a46b98aa4839652"></a>
#### sequence_name

It is the sequence name to be dropped.  
It can define schema to which the sequence belongs such as schema_name.sequence_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3977d419bf6affb9"></a>
### Description

Data Definition Language (DDL) statement such as DROP SEQUENCE can be rolled back if it is before when the transaction is committed.

<a id="3c90bbdae5087f1c"></a>
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

<a id="a325bac19ff79ae3"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="0b215fe033338ac3"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |

<a id="84554a3fca6acf89"></a>
### For More Information

Refer to the followings.

- [CREATE SEQUENCE](#f57ec80975339322)
- [ALTER SEQUENCE](#b01c09c114935817)

<a id="1c07c24ac96a8b62"></a>
## DROP SYNONYM

<a id="29464b80b5e3d951"></a>
### Function

It drops a synonym.

<a id="3d8754b57c0d68db"></a>
### Syntax

```
<drop synonym statement> ::=
    DROP [ PUBLIC ] SYNONYM [ IF EXISTS ] [schema_name.]synonym_name
    ;
```

<a id="92ab4ec798748592"></a>
### Invocation and Access Rules

DROP PUBLIC SYNONYM ON DATABASE privilege is required to drop a public synonym by specifying PUBLIC.

One of the following privileges is required to drop a private synonym.

- The owner of that synonym
- (DROP SYNONYM or CONTROL SCHEMA) ON SCHEMA for the schema to which the synonym belongs
- DROP ANY SYNONYM ON DATABASE

<a id="3233314f384ccc24"></a>
### Syntax Rules and Parameters

<a id="0effda71c139d28a"></a>
#### [ PUBLIC ]

It is specified when dropping the public synonym.  
If this clause is omitted, the private synonym is dropped.

<a id="3019e8157212db25"></a>
#### IF EXISTS

Even when the synonym does not exist, an error does not occur.

<a id="2f19c0be69005372"></a>
#### synonym_name

It is the synonym name to be dropped.  
It can define schema to which the synonym belongs such as schema_name.synonym_name and if schema_name is omitted, the default schema name of the user performing the statement is used.  
If PUBLIC is explicitly specified, the schema name can not be specified.

<a id="5e5216c97d96ab50"></a>
### Description

Data Definition Language (DDL) statement such as DROP SYNONYM can be rolled back if it is before when the transaction is committed.

<a id="cdd661fc3d5a944d"></a>
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

<a id="69ca19cdf1dad1a2"></a>
### Compatibility

The SQL standard does not define DROP SYNONYM statement.

<a id="24ed80c9b879fb63"></a>
### For More Information

Refer to [CREATE SYNONYM](#9e6f02e8285e67d1).

<a id="b8225899a85c66e7"></a>
## DROP TABLE

<a id="88ee483672dd4bf5"></a>
### Function

It drops a table.

<a id="9ffde157cacf4876"></a>
### Syntax

```
<drop table statement> ::=
    DROP TABLE [ IF EXISTS ] table_name
    [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="1f41082a77404307"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table statement&gt;.

- The owner of that table 
- CONTROL TABLE ON TABLE for that table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="697ba97f7a6e9d85"></a>
### Syntax Rules and Parameters

<a id="886a847b5dc14a44"></a>
#### IF EXISTS

Even when the table does not exist, an error does not occur.

<a id="5acd88c43eea0dbc"></a>
#### table_name

It is the table name to be dropped.  
It can define schema to which the table belongs such as schema_name.table_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

The following tables which are automatically created during creating the database, can not be dropped.

- The tables in "DEFINITION_SCHEMA" schema
- The tables in "FIXED_TABLE_SCHEMA" schema

It also drops constraints and indexes created in the table.

<a id="b2e5ed360e46bcc5"></a>
#### drop behavior

Currently, both RESTRICT and CASCADE are operated same.  
When it is omitted, the default value is RESTRICT.

<a id="794e0c42f47a8918"></a>
### Description

Data Definition Language (DDL) statement such as DROP TABLE can be rolled back if it is before when the transaction is committed.

<a id="81bd1784afc72915"></a>
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

<a id="d2a7be19284e1d11"></a>
### Compatibility

The SQL standard does not define the following clauses.

- IF EXISTS 
- CASCADE CONSTRAINTS

**SQL standard compatibility**

<a id="971b8d9e7f9cd12c"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | O |

<a id="49a0d234c29eeace"></a>
### For More Information

Refer to [CREATE TABLE](#72507f5467c281c9).

<a id="ee3406f353c996e6"></a>
## DROP TABLESPACE

<a id="91af75c214048fc7"></a>
### Function

It drops a tablespace.

<a id="aecabb644da16974"></a>
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

<a id="f5ed7898873aeafe"></a>
### Invocation and Access Rules

DROP TABLESPACE ON DATABASE privilege is required to perform &lt;drop tablespace definition&gt;.

<a id="07d291f9e58d47bb"></a>
### Syntax Rules and Parameters

<a id="fa53d12cfabf5e4b"></a>
#### IF EXISTS

Even when the tablespace does not exist, an error does not occur.

<a id="8654ba7c6e3438b7"></a>
#### tablespace_name

It is the tablespace name to be dropped.  

The following system tablespaces which are automatically created during creating the database, can not be dropped.

- DICTIONARY_TBS: system tablespace for dictionary management
- MEM_UNDO_TBS: system tablespace for default undo tablespace
- MEM_DATA_TBS: system tablespace for default user data tablespace
- MEM_TEMP_TBS: system tablespace for default temporary tablespace

> If tablespace_name was used as a default tablespace of a user, the space for the objects can not be allocated after dropping the tablespace.  
> After dropping the tablespace, the default tablespace should be changed by using [ALTER USER](#ed40a6862d9c8f12) statement.

<a id="97db65f4b46e19d1"></a>
#### INCLUDING CONTENTS

It drops objects (table, index, key constraint) which belong to the tablespace. If the index or key constraint which refers to the table which belongs to the tablespace exists outside of the tablespace, then it is also dropped.

If INCLUDING CONTENTS clause is not used, then any object which belongs to the tablespace should not exist.

<a id="dd2caf0368036ed6"></a>
#### [ { AND | KEEP } DATAFILES ]

It specifies whether to drop the datafiles which configure the tablespace together.  
The datafiles are not in the memory temporary tablespace, so the clause is ignored.

- AND DATAFILES 
    - It drops the datafiles together. 
- KEEP DATAFILES 
    - It does not drop the datafiles, but keeps them.
- If it is not specified, the default value is KEEP DATAFILES.

<a id="d57bc81bff472d44"></a>
#### drop behavior

Currently, both RESTRICT and CASCADE are operated same.  
When it is omitted, the default value is RESTRICT.

<a id="27b23fddbd6c81a9"></a>
### Description

Unlike other Data Definition Language (DDL), DROP TABLESPACE statement can not be rolled back and the executed transaction is automatically committed.

<a id="1b1b2f473e26c667"></a>
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

<a id="fb727835a1a5dbe8"></a>
### Compatibility

The SQL standard does not cover the concepts of the tablespace.

<a id="c4933a92abd87647"></a>
### For More Information

Refer to the followings.

- [CREATE MEMORY DATA TABLESPACE](#b0ee56c9e33dadf5)
- [CREATE MEMORY TEMPORARY TABLESPACE](#3ddf803b50db6f27)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)

<a id="75a505d0fbae98f3"></a>
## DROP USER

<a id="6f9fa33cf8b415d1"></a>
### Function

It drops a database user.

<a id="d08559e4c0d7521b"></a>
### Syntax

```
<drop user statement> ::=
    DROP USER [ IF EXISTS ] user_identifier [ <drop behavior> ]
    ;

<drop behavior> ::=
      RESTRICT
    | CASCADE
```

<a id="4316aa73ccd477a4"></a>
### Invocation and Access Rules

DROP USER ON DATABASE privilege is required to perform &lt;drop user statement&gt;.

> The schema owned by user_identifier should not exist.  
> For more information about dropping the schema, refer to [DROP SCHEMA](#406abccf7b931f83).

<a id="c1ab028259ae8a0c"></a>
### Syntax Rules and Parameters

<a id="955835d81dbf5e66"></a>
#### IF EXISTS

Even when the user does not exist, an error does not occur.

<a id="fd9a82a6e3ab0dcd"></a>
#### user_identifier

It is the database username to be dropped.  
However, the user which is automatically created during creating the database such as "SYS", can not be dropped.

It does not drop the object which is created by user_identifier but is not an owner as follows.

- Role 
- Tablespace

<a id="8b248a46867bb992"></a>
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

<a id="84592c9a5b500715"></a>
### Description

In GOLDILOCKS, relationship between the user and the schema is 1 : N. A user does not own a schema, or the user can have multiple schemas.

To drop a user, all schema owned by the user should be dropped.

<a id="340c93a74dd11de2"></a>
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

<a id="4642c716f53754ea"></a>
### Compatibility

SQL standard cover the concepts of the user, but they do not define the SQL statements related to creating or dropping a user.

<a id="912f3eb43ae81f76"></a>
### For More Information

Refer to the followings.

- [CREATE USER](#524780362f90ebc8)
- [ALTER USER](#ed40a6862d9c8f12)
- [DROP SCHEMA](#406abccf7b931f83)

<a id="c3d4597ac53c944b"></a>
## DROP VIEW

<a id="98b57a2364e83c84"></a>
### Function

It drops a view.

<a id="8ea40b1b27e4a291"></a>
### Syntax

```
<drop view statement> ::=
    DROP VIEW [ IF EXISTS ] view_name
    ;
```

<a id="f3be3608c093f1b7"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop view statement&gt;.

- The owner of that view 
- CONTROL TABLE ON TABLE for that view
- (DROP VIEW or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
- DROP ANY VIEW ON DATABASE

<a id="31f3b5705f5f932e"></a>
### Syntax Rules and Parameters

<a id="23a6393b0e01b233"></a>
#### IF EXISTS

Even when the view does not exist, an error does not occur.

<a id="080a69445c7378a8"></a>
#### view_name

It is the view name to be dropped.  
The schema to which the table belongs, such as schema_name.view_name, can be defined. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="5ac73fcdc09a6cea"></a>
### Description

Data Definition Language (DDL) statement such as DROP VIEW can be rolled back if it is before when the transaction is committed.

<a id="a5657778254717f9"></a>
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

<a id="9cef370eccedb420"></a>
### Compatibility

The SQL standard does not define IF EXISTS clause.

**SQL standard compatibility**

<a id="92c7bde971722adf"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F032 | CASCADE drop behavior | X |

<a id="01e0fee6d77323df"></a>
### For More Information

Refer to the followings.

- [CREATE VIEW](#ae5c14874ae12b2e)
- [ALTER VIEW](#062be61ee2ec0848)

<a id="ca4c1dbcc096bbdd"></a>
## EXECUTE statement_name

<a id="518198fbcd083017"></a>
### Function

It executes the prepared statement.

<a id="e5df3d2f042e338c"></a>
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

<a id="d81502339514dc4a"></a>
### Invocation and Access Rules

It can be used in an embedded SQL.  
An appropriate privilege according to the type of a dynamic SQL statement is required.

<a id="e4a3dce84a4c1f7c"></a>
### Syntax Rules and Parameters

<a id="a5499de624ae3cf5"></a>
#### statement_name

It is the name of a prepared statement.  
Statement_name should be prepared by using [PREPARE statement_name](#897dbc4fb97ab869).

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

- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)
- [FETCH cursor_name](#8b90e7e7e6e0c963)
- [CLOSE cursor_name](#8094485dc3cb5ea5)

If there is not any query result, it is completed as NO DATA.

<a id="3f9775ce4df0cd8b"></a>
#### [ &lt;parameter using clause&gt; ] [ &lt;result into clause&gt; ]

&lt;parameter using clause&gt; and &lt;result into clause&gt; can be specified in any order, but they should not be repeated.

<a id="bfe1b73673043336"></a>
#### &lt;parameter using clause&gt;

If any parameter exists in a dynamic SQL statement referenced by statement_name, the parameter information is specified with &lt;using parameter arguments&gt; clause.

<a id="c3520e61339e9f2d"></a>
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

<a id="1d77558792e0c11c"></a>
#### &lt;result into clause&gt;

If the dynamic SQL statement referenced by statement_name is a query, the information about the result columns is specified with &lt;into result arguments&gt; clause.

If the result is null and INDICATOR is not specified, [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error occurs.

<a id="99713864bc8be691"></a>
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

<a id="4a73a03c72f12e9d"></a>
### Description

Statement_name is an identifier which informs the precompiler the statement in an embedded SQL source code.  
A separate type or declaration is not required because statement_name is not a host variable. EXECUTE statement_name should be written after PREPARE statement_name.

For more information, refer to [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926).

<a id="ab7bda071dadd975"></a>
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

The full source code in which EXECUTE statement_name was used can be viewed in [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#3f9d137d2500f1fa).

<a id="a339ee49791073b0"></a>
### Compatibility

**SQL standard compatibility**

<a id="d496bc223e8fe1f8"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B032 | Extended dynamic SQL | X |

<a id="56ce9bc00a7a8f93"></a>
### For More Information

Refer to the followings.

- [PREPARE statement_name](#897dbc4fb97ab869)
- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)
- [FETCH cursor_name](#8b90e7e7e6e0c963)
- [CLOSE cursor_name](#8094485dc3cb5ea5)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926)

<a id="1eacad0a6072f76a"></a>
## EXECUTE IMMEDIATE 'sql_string'

<a id="5891cbabcfad9733"></a>
### Function

It executes a dynamic SQL statement which was not defined when writing a program.

<a id="9c61f86d530c7279"></a>
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

<a id="0ebd634ebbeaa2af"></a>
### Invocation and Access Rules

It can be used in an embedded SQL.  
An appropriate privilege according to the type of a dynamic SQL statement is required.

<a id="ddaa02112151b7ec"></a>
### Syntax Rules and Parameters

<a id="95264143fccd7b1b"></a>
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

<a id="304624f078d54069"></a>
#### variable_name

The type corresponding to the variable_name should be a character string.  
The dynamic SQL statement defined in the variable_name should be valid.

<a id="c092f059f6bfa9fa"></a>
#### sql statement

The dynamic SQL statement defined in the sql statement should be valid.

<a id="84ba7f020d13121f"></a>
### Description

EXECUTE IMMEDIATE 'sql_string' statement can be used as the non-query SQL without a host variable in dynamic embedded SQL application. It is appropriate to execute DDL, DML as one-off because it does not require separate preparation procedure.

For more information, refer to  [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926).

<a id="6a4cdebb1c5d710c"></a>
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

The full source code in which EXECUTE IMMEDIATE 'sql_string' was used can be viewed in [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#3f9d137d2500f1fa).

<a id="82f124f502462ced"></a>
### Compatibility

**SQL standard compatibility**

<a id="18bb7777d2ae95af"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="a01bd42f7b5e9fb4"></a>
### For More Information

Refer to the followings.

- [PREPARE statement_name](#897dbc4fb97ab869)
- [EXECUTE statement_name](#ca4c1dbcc096bbdd)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926)

<a id="8b90e7e7e6e0c963"></a>
## FETCH cursor_name

<a id="b857a98bf943b226"></a>
### Function

It locates the cursor on a specific row of result set, and obtains the value of that row to a host variable.

<a id="01507943167f7e30"></a>
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

<a id="19bf8a82476f2117"></a>
### Syntax Rules and Parameters

<a id="4d8571fecd4f2869"></a>
#### [ FROM ] cursor_name

It should be an open cursor in a session.  
FROM can be omitted.

<a id="7cf0a5a52deb5e18"></a>
#### &lt;fetch orientation&gt;

To use &lt;fetch orientation&gt; other than FETCH NEXT, a scrollable cursor should be used.  
If &lt;fetch orientation&gt; is omitted, the default value is NEXT.

The open cursor has the cursor position information for the result set as follows.

<a id="c5c3067cb82a79fe"></a>
![The position of cursor](../assets/images/23f25310e182e3eb.png)

**The position of cursor**

<a id="d1dd76901a7a35cc"></a>
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

<a id="a6101d444f309d8a"></a>
#### &lt;result into clause&gt;

The variable information to obtain the result column is specified by using &lt;into result arguments&gt;.

If the result is null and INDICATOR is not specified, [DATA EXCEPTION, NULL VALUE, NO INDICATOR PARAMETER] error occurs.

<a id="591ad3affd19be60"></a>
#### &lt;into result arguments&gt;

The number of variables in INTO clause should be as same as the number of columns in the result set of the cursor.

<a id="a7fd5a4dec9ff936"></a>
### Description

If the cursor is BEFORE THE FIRST ROW or AFTER THE LAST ROW after performing FETCH, it is positioned at the same position regardless of the entered position in &lt;fetch orientation&gt;.

<a id="6309bd0af8ece259"></a>
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

<a id="85bdd892299d399e"></a>
### Compatibility

The SQL standard does not define CURRENT among &lt;fetch orientation&gt;.

**SQL standard compatibility**

<a id="cb1324e6accef692"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F431 | Read-only scrollable cursors | O |
| B031 | Basic dynamic SQL | O |

<a id="b594c12d471520e8"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#9826eadcd321de1b)
- [OPEN cursor_name](#503dadf63d95d09e)
- [CLOSE cursor_name](#8094485dc3cb5ea5)

<a id="5969f471eb288b39"></a>
## GRANT privileges TO

<a id="1be205682a27fe82"></a>
### Function

It grants privileges to a user.

<a id="635e27d30aeab27a"></a>
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
```

<a id="b32575a58e445c3f"></a>
### Syntax Rules and Parameters

<a id="620814a55971ee71"></a>
#### &lt;grantee&gt;

It is the user to be granted the privileges.

- user_identifier 
    - It grants the privilege to a user. 
- PUBLIC 
    - It is an authorization object which means all users.

<a id="7a61e3d557d18afd"></a>
#### WITH GRANT OPTION

It allows the grantee to grant the privilege to other users.

When the same &lt;privilege&gt; is granted as follows, WITH GRANT OPTION is maintained.

- GRANT SELECT ON t1 TO u1 WITH GRANT OPTION; 
- GRANT SELECT ON t1 TO u1;

<a id="0fbd8cc7ad66e02f"></a>
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

<a id="6cf78e61b1abff46"></a>
#### &lt;database privilege&gt;

It is the privilege for the database objects.  
[ON DATABASE] statement can be omitted.

The database action which can be defined with the database privilege is as follows.

- ALL [ PRIVILEGES ] [ON DATABASE] 
    - All privileges for the database which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Database privilege**

<a id="3347b8d7c7a5a195"></a>
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

<a id="7be6b901f0ac9d48"></a>
#### &lt;tablespace privilege&gt;

It is the privilege for the tablespace objects.

The tablespace action which can be defined with the tablespace privilege is as follows.

- ALL [ PRIVILEGES ] ON TABLESPACE tablespace_name 
    - All privileges for the tablespace which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Tablespace privilege**

<a id="3c51d12666667242"></a>
| &lt;tablespace action&gt; | Description |
| --- | --- |
| CREATE OBJECT | Privilege for creating objects in the tablespace |

<a id="f992ce28766780dd"></a>
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

<a id="d1e87ca0f75aec2b"></a>
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

<a id="95da501d1083dbb2"></a>
#### &lt;table privilege&gt;

It is the privilege for the table object or the view object.  
[TABLE] statement can be omitted.

The table action which can be defined with the table privilege is as follows.

- ALL [ PRIVILEGES ] ON [TABLE] table_name 
    - All privileges for the table which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Table privilege**

<a id="d056b14a814ffd07"></a>
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

<a id="3b4c834f85ebdb02"></a>
| &lt;column action&gt; | Description |
| --- | --- |
| SELECT (columns) | Privilege for querying that columns |
| INSERT (columns) | Privilege for creating rows including that columns |
| UPDATE (columns) | Privilege for updating that columns |
| REFERENCES (columns) | Privilege for creating referential constraints which refers to that columns |

<a id="ae119827fbf28a16"></a>
#### &lt;sequence privilege&gt;

It is the privilege for the sequence object.

The sequence action which can be defined with the sequence privilege is as follows.

- ALL [ PRIVILEGES ] ON SEQUENCE sequence_name 
    - All privileges for the sequence which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION.

**Sequence privilege**

<a id="b093083f0552a067"></a>
| &lt;sequence action&gt; | Description |
| --- | --- |
| USAGE | Privilege for using the sequence |

<a id="ca2bcf48ce5ee10f"></a>
#### &lt;procedure privilege&gt;

It is the privilege for the procedure/ function object.

The action which can be defined with the procedure privilege is as follows.

- ALL [ PRIVILEGES ] ON PROCEDURE procedure_name 
    - All privileges for the procedure/ function which the grantor (the user who performs the statement) owns by using WITH GRANT OPTION

**Procedure privilege**

<a id="77427e2020dd5a02"></a>
| &lt;procedure action&gt; | Description |
| --- | --- |
| EXECUTE | Privilege for executing the procedure/function |

<a id="57f6d683a99d6719"></a>
### Description

Data Definition Language (DDL) such as GRANT privilege can be rolled back if it is before when the transaction is committed.

The owner who created SQL schema object, such as table, sequence, has certain privileges without being granted any separate privilege for the object.    
For more information, refer to the following CREATE statements.

- [CREATE TABLE](#72507f5467c281c9)
- [CREATE VIEW](#ae5c14874ae12b2e)
- [CREATE SEQUENCE](#f57ec80975339322)
- [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16) 
- [CREATE FUNCTION](../part-04-psm-manual/24-psm-sql-references.md#21b6c80060dfcc44)
- [CREATE PROCEDURE](../part-04-psm-manual/24-psm-sql-references.md#730491b1fd9dfcc3)

The owner who created non-schema object such as schema, tablespace, does not automatically have any privilege for the object. Therefore, the privilege should be separately granted.   
For more information, refer to the following CREATE statements.

- [CREATE SCHEMA](#671a916eb0910614)
- [CREATE TABLESPACE](#4fb45716ef9fbe7b)
- [CREATE USER](#524780362f90ebc8)

<a id="cdcfa3cded82309b"></a>
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

<a id="26928165ba7966cc"></a>
### Compatibility

The SQL standard does not define the following privileges.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

**SQL standard compatibility**

<a id="d19a960a3e78f9f8"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S081 | Subtables | X |
| T211 | Basic trigger capability | X |
| T281 | SELECT privilege with column granularity | O |
| T332 | Extended Roles | X |
| F731 | INSERT column privileges | O |

<a id="5d89ba100e920f65"></a>
### For More Information

Refer to the followings.

- [REVOKE privileges FROM](#1e240fa22ac10351)
- [CREATE USER](#524780362f90ebc8)
- [DROP USER](#75a505d0fbae98f3)
- [ALTER USER](#ed40a6862d9c8f12)

<a id="db825a2bf01d54dd"></a>
## INSERT INTO

<a id="3b8158228e667d10"></a>
### Function

It creates new rows in a table.

<a id="9c5028f2de168461"></a>
### Syntax

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES
```

<a id="c9f22118676a8f0c"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;Insert statement&gt;.

- One of the following privileges is required to perform the INSERT statement.
    - INSERT(columns) ON TABLE for all columns which are targets of insert 
    - (INSERT or CONTROL TABLE) ON TABLE for the table
    - (INSERT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - INSERT ANY TABLE ON DATABASE

- One of the following privileges is required for all tables used in &lt;from subquery&gt;.
    - SELECT(columns) ON TABLE for all columns of tables which were used in the statement
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="099653294bb018e7"></a>
### Syntax Rules and Parameters

<a id="f91ea92028e2306d"></a>
#### table_name

It is the name of a target table in which the row is to be created.  
It can define schema to which the table belongs such as schema_name.table_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="9827cbbb8059f4e7"></a>
#### [ ( column_name [, ...] ) ]

It is the column name of a table.  
The column list can be omitted.  
The number of columns and the number of  &lt;insert source&gt; values should be same, and DEFAULT value is assigned to the omitted column.

<a id="b025c0eac63552f5"></a>
#### &lt;values clause&gt;

It is the list of values to be assigned to the corresponding columns.

- &lt;value expression&gt; 
    - It is the value or expression to be assigned to the corresponding column. 
- DEFAULT 
    - The value of corresponding column will use the default value which were defined through [CREATE TABLE](#72507f5467c281c9).
    - If it is not defined, NULL will be assigned.

Multiple rows can be created as follows.

```
INSERT INTO table_name VALUES ( 1, 'A' ), ( 2, 'B' ), ( 3, 'C' )
```

<a id="b90f7eb57c80e145"></a>
#### &lt;from subquery&gt;

It is the query to create rows.  
For more information, refer to [query expression](#1d9bd840c91d26e4) clause of [SELECT](#1117040fd802dbd4) statement.

<a id="74c31290afa45291"></a>
#### DEFAULT VALUES

It fills every column with default value.

DEFAULT VALUES clause means as same as the following.

```
VALUES ( DEFAULT, DEFAULT, ..., DEFAULT )
```

<a id="f4063a6daeb06a3f"></a>
### Description

<a id="39e20efc68e148b6"></a>
#### Differences among INSERT-related Statements

- [INSERT INTO](#db825a2bf01d54dd)
    - It creates one or multiple rows into the table. 
    - e.g. INSERT INTO t1 SELECT * FROM t1; 
- [INSERT INTO name RETURNING](#6e07672cf5aedd6b)
    - It creates one or multiple rows into the table, then the created rows can be retrieved in the same way as SELECT statement(API such as SQLFetch()).
    - e.g. INSERT INTO t1 SELECT * FROM t1 RETURNING c1; 
- [INSERT INTO name RETURNING .. INTO](#be8a8f852c974819)
    - It creates one or less row, and if a single row is created, it obtains the value to the host variable of RETURNING INTO clause.
    - e.g. INSERT INTO t1 DEFAULT VALUES RETURNING c1 INTO :v1;

<a id="6e6fdb7e2da55eb7"></a>
### Examples

The following is an example of creating a single row by using INSERT statement.

```
gSQL> INSERT INTO region VALUES ( 0, 'AFRICA' );

1 row created.
```

The following is an example of using the DEFAULT value or identity value of the column in INSERT statement.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

• DEFAULT is inserted into all columns.

```
gSQL> INSERT INTO region DEFAULT VALUES;

1 row created.
```

• DEFAULT is inserted into all columns.

```
gSQL> INSERT INTO region VALUES (DEFAULT, DEFAULT);

1 row created.
```

• If a column is omitted, the DEFAULT value of r_name column is used.

```
gSQL> INSERT INTO region(r_regionkey) VALUES (-100);

1 row created.
```

• If a column is omitted, the identity value of r_regionkey column is used.

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA');

1 row created.


gSQL> SELECT * FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      
          2 N/A                      
       -100 N/A                      
          3 ASIA                     

4 rows selected.
```

The following is an example of creating multiple rows by describing them in VALUES clause.

```
gSQL> INSERT INTO region
       VALUES ( 1, 'AFRICA' ),
              ( 2, 'ASIA'   ),
              ( 3, 'EUROPE' );

3 rows created.
```

The following is an example of creating multiple rows by using a subquery.

```
gSQL> INSERT INTO region SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3;

3 rows created.
```

<a id="2cd4ea9719d1d7c6"></a>
### Compatibility

**SQL standard compatibility**

<a id="1bd1bc1ffb716b96"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| F222 | INSERT statement: DEFAULT VALUES clause | O |
| S204 | Enhanced structured types | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="c859ffbcec9d8fd1"></a>
### For More Information

Refer to the followings.

- [SELECT](#1117040fd802dbd4)
- [INSERT INTO name RETURNING](#6e07672cf5aedd6b)
- [INSERT INTO name RETURNING .. INTO](#be8a8f852c974819)

<a id="6e07672cf5aedd6b"></a>
## INSERT INTO name RETURNING

<a id="1d8a0b9558fa25bc"></a>
### Function

It creates new rows in the table, and retrieves them.

<a id="8ab986edee1429f3"></a>
### Syntax

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning clause>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...]
```

<a id="0b9f83c70101c364"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;insert returning query statement&gt;.

- One of the following privileges is required to perform INSERT statement.
    - INSERT(columns) ON TABLE for all columns which are targets of insert
    - (INSERT or CONTROL TABLE) ON TABLE for the table
    - (INSERT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - INSERT ANY TABLE ON DATABASE

- One of the following privileges is required for all tables used in &lt;from subquery&gt;.
    - SELECT(columns) ON TABLE for all columns of tables which were used in the statement
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

- One of the following privileges is required for all columns used in RETURNING clause.
    - SELECT(columns) ON TABLE for all columns which were used in RETURNING clause. 
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="688bb2e0101de450"></a>
### Syntax Rules and Parameters

<a id="a7c7df854ec12bbc"></a>
#### table_name

It is the name of a target table in which the row is to be created.

<a id="2c56de488a705445"></a>
#### [ ( column_name [, ...] ) ]

It is the column name of a table.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="e162c293d430520b"></a>
#### &lt;values clause&gt;

It is the list of values to be assigned to the corresponding columns.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="ecfa535075c6f3bc"></a>
#### &lt;from subquery&gt;

It is the query to create rows.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="42811cf4a2549377"></a>
#### DEFAULT VALUES

It fills every column with default value.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="ccadee531a3b0262"></a>
#### &lt;returning clause&gt;

It returns the inserted rows.

- It sets the inserted rows as a result set, and specifies the rows to be retrieved.
    - RETURNING clause returns the rows which were inserted by INSERT statement, and which is a result set. 
    - &lt;value expression&gt; 
        - It is as same as &lt;select list&gt; in SELECT statement, but it can not use the aggregation.
    - [[AS] alias_name] 
        - It can name a value expression by using AS clause.

The keywords RETURNING and RETURN have the same meaning.

<a id="2dd4bc06441c9352"></a>
### Description

For more information, refer to [Differences among INSERT-related Statements](#39e20efc68e148b6).

<a id="08522a94c87a4f18"></a>
### Examples

The following is an example of retrieving the column values created by using INSERT statement.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- The following is an example of returning the created DEFAULT value (RETURNING).

```
gSQL> INSERT INTO region VALUES ( DEFAULT, DEFAULT ) RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      

1 row created.
```

- The following is an example of returning the omitted column value (RETURNING).

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA') RETURNING r_regionkey;

R_REGIONKEY
-----------
          2

1 row created.
```

The following is an example of retrieving the rows created by using the subquery.

```
gSQL> INSERT INTO region 
      SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3 
      RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     

3 rows created.
```

<a id="672c93c1ed1a0d0e"></a>
### Compatibility

The SQL standard does not define &lt;insert returning query statement&gt;.

<a id="b4913c03a30638f1"></a>
### For More Information

Refer to the followings.

- [INSERT INTO](#db825a2bf01d54dd)
- [INSERT INTO name RETURNING .. INTO](#be8a8f852c974819)

<a id="be8a8f852c974819"></a>
## INSERT INTO name RETURNING .. INTO

<a id="88e8fb5ffe49e179"></a>
### Function

It creates a single row in a table, and obtains the value of the created row as a host variable.

<a id="e9f70ae987336ba4"></a>
### Syntax

```
<insert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning into clause>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning into clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="16abb35eca381028"></a>
### Invocation and Access Rules

A user should satisfy the following conditions to perform &lt;insert returning into statement&gt;.

- One of the following privileges is required to perform INSERT statement.
    - INSERT(columns) ON TABLE for all columns which are targets of insert.
    - (INSERT or CONTROL TABLE) ON TABLE for the table 
    - (INSERT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - INSERT ANY TABLE ON DATABASE

- One of the following privileges is required for all tables used in &lt;from subquery&gt;.
    - SELECT(columns) ON TABLE for all columns of tables which were used in the statement
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

- One of the following privileges is required for all columns used in RETURNING clause.
    - SELECT(columns) ON TABLE for all columns which were used in RETURNING clause
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="d4eda2d314c55f67"></a>
### Syntax Rules and Parameters

<a id="60121c1df6ee9809"></a>
#### table_name

It is the name of a target table in which the row is to be created.

<a id="9b5ee34ac9d878ec"></a>
#### [ ( column_name [, ...] ) ]

It is the column name of a table.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="7b638f3c146a8928"></a>
#### &lt;values clause&gt;

It is the list of values to be assigned to the corresponding columns.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="1e1aced5b84aefab"></a>
#### &lt;from subquery&gt;

It is the query to create rows.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="b1573f7a22227243"></a>
#### DEFAULT VALUES

It fills every column with default value.  
For more information, refer to [INSERT INTO](#db825a2bf01d54dd).

<a id="3ffd8a1172fe84b9"></a>
#### &lt;returning clause&gt;

It returns the inserted rows.  
For more information, refer to [&lt;returning clause&gt;](#ccadee531a3b0262) in [INSERT INTO name RETURNING](#6e07672cf5aedd6b) statement.

<a id="3003c9fd06b7a8ef"></a>
##### INTO variable_name [, ...]

The number of variables in INTO clause should be equal to the number of the expressions in RETURNING clause.  
The row to be created should be one or less. If two or more rows are created, an error occurs.

<a id="246969c8b559687d"></a>
### Description

For more information, refer to [Differences among INSERT-related Statements](#39e20efc68e148b6).

<a id="2d872174a563dd5a"></a>
### Example

The following is an example of obtaining the value of the created row as a host variable.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

• The host variables are declared.

```
\VAR v_key  BIGINT
\VAR v_name VARCHAR(128)
```

• The created DEFAULT values are obtained as the host variables.

```
gSQL> INSERT INTO region 
      VALUES ( DEFAULT, DEFAULT ) 
      RETURNING r_regionkey, r_name 
      INTO :v_key, :v_name;

V_KEY V_NAME                   
----- -------------------------
    1 N/A                      

1 row created.
```

• The omitted column value is obtained as the host variable.

```
gSQL> INSERT INTO region(r_name) 
      VALUES ('ASIA') 
      RETURNING r_regionkey 
      INTO :v_key;

V_KEY
-----
    2

1 row created.
```

<a id="7c553f53f722fb10"></a>
### Compatibility

The SQL standard does not define &lt;insert returning into statement&gt;.

<a id="7c5528e175597751"></a>
### For More Information

Refer to the followings.

- [INSERT INTO](#db825a2bf01d54dd)
- [INSERT INTO name RETURNING](#6e07672cf5aedd6b)

<a id="64e196a787076509"></a>
## LOCK TABLE

<a id="4940aedd7b239fb3"></a>
### Function

It locks one or more tables.

<a id="4657dafc35f80613"></a>
### Syntax

```
<lock table statement> ::=
    LOCK TABLE lock target [, ...] 
    IN <lock mode> MODE [<wait clause>]
    ;

<lock mode> ::=
    SHARE
    | EXCLUSIVE
    | ROW SHARE
    | ROW EXCLUSIVE
    | SHARE ROW EXCLUSIVE


<wait clause> ::=
    NOWAIT
    | WAIT time
```

<a id="db6a29432829dc85"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;lock table statement&gt;.

- (LOCK or CONTROL TABLE) ON TABLE for the table
- (LOCK TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- LOCK ANY TABLE ON DATABASE

<a id="589e5b6d9f117b26"></a>
### Syntax Rules and Parameters

<a id="45d13ca1a2605e66"></a>
#### &lt;lock target&gt;

It specifies the target table to be locked.

<a id="e73f0de191332c4d"></a>
#### &lt;lock mode&gt;

It specifies the LOCK mode.

- SHARE 
    - It allows concurrent queries for the locked table, but prohibits updating the table.
- EXCLUSIVE 
    - It allows exclusive queries for the locked table. 
- ROW SHARE 
    - It allows concurrent access to the locked table, but prohibits locking the entire table for exclusive access. 
- ROW EXCLUSIVE 
    - It allows concurrent access to the locked table, but prohibits locking the entire table for exclusive access. 
    - If ROW EXCLUSIVE mode is set, it prohibits locking in SHARE mode. 
    - ROW EXCLUSIVE mode is automatically obtained when updating, inserting, deleting. 
- SHARE ROW EXCLUSIVE 
    - It is used to search for the entire table or to make other users search for the rows in the table.
    - It prohibits other users from accessing the locked tables in SHARE mode or accessing the rows being updated.

<a id="83bd6cacdb33dc49"></a>
#### &lt;wait clause&gt;

It specifies the waiting time to acquire the lock.

- NOWAIT 
    - It immediately acquires the lock contol for the object.
    - If the lock is already set by another user, the control is immediately handed over.
        - In this case, the database generates a message. 
- WAIT time 
    - It sets the waiting time for acquiring the lock.
    - It is specified in seconds, and its value is from 0 to 1,000,000,000.
- If it is not specified, it waits indefinitely until acquiring the lock.

<a id="cdc32d90e252ee3e"></a>
### Description

If the transaction is committed or rolled back all acquired locks are automatically released. When using ROLLBACK TO SAVEPOINT statement, all locks acquired since that savepoint are released.

<a id="7b78810811e9ddb7"></a>
### Examples

The following is an example of locking the TABLE t1 to prevent any updating operation by another transaction.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE;

Table locked.
```

The following is an example of performing LOCK statement for multiple tables.

```
gSQL> LOCK TABLE t1, t2 IN EXCLUSIVE MODE;

Table locked.
```

The following is an example of acquiring SHARE ROW EXCLUSIVE lock for the TABLE t1.

```
gSQL> LOCK TABLE t1 IN SHARE ROW EXCLUSIVE MODE;

Table locked.
```

The following statement is performed only when the lock can be immediately acquired for the table. If the lock can not be acquired, an error occurs.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE NOWAIT;

Table locked.
```

The following is an example of waiting 10 seconds to acquire the lock.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE WAIT 10;

Table locked.
```

<a id="ac050679e1844124"></a>
### Compatibility

The SQL standard does not cover the concepts of the lock table.

<a id="d0c36e6956e09289"></a>
### For More Information

Refer to the followings.

- [COMMIT](#97c03faa5a24c67f)
- [ROLLBACK](#30d00b80c704d186)

<a id="bd9d827360468b68"></a>
## NOAUDIT POLICY

<a id="ff93bc54229f1512"></a>
### Function

It deactivates the audit policy.

<a id="6f10fa915d753470"></a>
### Syntax

```
<noaudit policy statement> ::= 
    NOAUDIT POLICY policy_name
    [ <specified_user_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
```

<a id="71322c628899f1e6"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;noaudit policy statement&gt;.

<a id="e78e7b6fc6d4e793"></a>
### Syntax Rules and Parameters

<a id="264b5b620d8238af"></a>
#### policy_name

It is the name of the audit policy object to be deactivated.  
The deactivated audit policy does not effect on the existing session, and it effects only on the newly created session.

<a id="c3f33ca99e95d493"></a>
#### &lt;specified_user_option&gt;

It specifies the user to be excluded from the auditing target.

Unlike AUDIT POLICY statement, NOAUDIT POLICY does not have EXCEPT option.

If AUDIT POLICY name BY clause is used, NOAUDIT POLICY name BY statement should be used to deactivate it.  
If AUDIT POLICY name EXCEPT clause is used, NOAUDIT POLICY name statement without BY clause should be used to deactivate it.

NOAUDIT POLICY statement should be used as follows according to the usage of AUDIT POLICY statement to deactivate it.

**Activating/ deactivating audit policy**

<a id="18d8dc85607c7eb6"></a>
| Type | AUDIT POLICY statement | NOAUDIT POLICY statement |
| --- | --- | --- |
| All users | AUDIT POLICY p1 | NOAUDIT POLICY p1 |
| Using BY | AUDIT POLICY p1 BY u1 | NOAUDIT POLICY p1 BY u1 |
| Using EXCEPT | AUDIT POLICY p1 EXCEPT u1 | NOAUDIT POLICY p1 |

When deactivating all activated users, the audit policy object is completely deactivated.

<a id="c6a2debec72cba47"></a>
### Description

The activation information of an audit policy object can be queried as follows.

```
SELECT policy_name
     , enabled_opt
     , user_name
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';
```

NOAUDIT POLICY statement deletes each created information about activationaccording to the AUDIT POLICY specifying method.  
If the information activated through the query above does not exist, then the audit policy is completely deactivated.

If all users are activated as follows, NOAUDIT POLICY BY clause does not does not affect it.

```
AUDIT POLICY p1;
```

- It does not have any effect.

```
NOAUDIT POLICY p1 BY u1;
```

- It should be deactivated as follows.

```
NOAUDIT POLICY p1;
```

If one or more users are separately activated, use NOAUDIT POLICY statement according to the AUDIT POLICY specifying method.

<a id="3c85525ddc6e58cc"></a>
#### When Activated by Using BY

If the audit policy is activated as follows,

```
AUDIT POLICY p1 WHENEVER NOT SUCCESSFUL;
AUDIT POLICY p1 BY u1;
AUDIT POLICY p1 BY u2;
```

the information about activation is as follows.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS  WHEN_FAILURE
-----------  -----------  ---------    ------------  ------------
P1           BY           ALL USERS    NO            YES
P1           BY           U1           YES           YES
P1           BY           U2           YES           YES
```

The following is an example of performing NOAUDIT statement and the information about activation.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           BY           U1           YES             YES
P1           BY           U2           YES             YES
```

The auditing for a failure for ALL USERS is deactivated, but the auditing for user u1, u2 is still activated.

If NOAUDIT POLICY statement is additionally used through BY option as follows, then audit policy p1 is completely deactivated.

```
NOAUDIT POLICY p1 BY u1, u2;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

<a id="1e181973eca778e0"></a>
#### When Activated by Using EXCEPT

If the audit policy is activated as follows,

```
AUDIT POLICY p1 EXCEPT u1, sys;
```

the information about activation is as follows.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           EXCEPT       U1           YES             YES
P1           EXCEPT       SYS          YES             YES
```

Unlike AUDIT POLICY statement, NOAUDIT POLICY does not have EXCEPT option, so execute the statement without an option as follows.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

In other words, if the audit policy is activated by using EXCEPT option, each user can not be deactivated again by using NOAUDIT POLICY statement.

<a id="944d3122114cb0f4"></a>
### Examples

The following is an example of deactivating all users.

```
NOAUDIT POLICY table_pol;
```

The following is an example of deactivating a specific activated user by using BY.

```
NOAUDIT POLICY table_pol BY u1;
```

<a id="ee41e320e6487995"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="db7ff928b439246a"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](#6be201c413853041)
    - [DROP AUDIT POLICY](#bd602160c2b9fd00)
    - [ALTER AUDIT POLICY](#41e688c628dec27b)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](#7207b4f12e0bf6f6)
    - [NOAUDIT POLICY](#bd9d827360468b68)

- Viewing audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#e4782a986661d5a6)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#4bae50ba8bf61053)

<a id="503dadf63d95d09e"></a>
## OPEN cursor_name

<a id="f4b8df7ada0007ce"></a>
### Function

It opens a cursor.

<a id="6dc8e9f271cefe4d"></a>
### Syntax

```
<open statement> ::=
    OPEN cursor_name [ <parameter using clause> ]
    ;

<parameter using clause> ::=
      <using parameter arguments>

<using parameter arguments> ::=
    USING variable_name [, ...]
```

<a id="676321d916900713"></a>
### Invocation and Access Rules

If cursor_name is a dynamic cursor which is declared by using [PREPARE statement_name](#897dbc4fb97ab869) and [DECLARE cursor_name](#9826eadcd321de1b), it can be used in an embedded SQL.

It is same with the privilege of [&lt;cursor query&gt;](#0c5a221463cc610d) included in [DECLARE cursor_name](#9826eadcd321de1b) which declared cursor_name.

<a id="4154f20662ed7b43"></a>
### Syntax Rules and Parameters

<a id="f115de55bb2fb352"></a>
#### cursor_name

It should be a cursor declared with [DECLARE cursor_name](#9826eadcd321de1b) within the session.

<a id="9e25d3324c81afa7"></a>
#### &lt;parameter using clause&gt;

It can be used in an embedded SQL.

When &lt;parameter using clause&gt; is used, cursor_name should be a dynamic cursor declared by using [PREPARE statement_name](#897dbc4fb97ab869) and [DECLARE cursor_name](#9826eadcd321de1b).

<a id="b1a9671d72bf6dd9"></a>
#### &lt;using parameter arguments&gt;

When &lt;using parameter arguments&gt; is used, the number of variable_name should be equal to the number of the parameter included in a query which is referenced by [PREPARE statement_name](#897dbc4fb97ab869).

The listed variable_name corresponds to the dynamic parameter in an order of its description.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT c1, c2 FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL DECLARE cur1 CURSOR FOR stmt1;
    EXEC SQL OPEN cur1 USING :sValue1, :sValue2, :sValue3;
    ...
    EXEC SQL WHENEVER NOT FOUND DO break;
    for(;;)
    {
        EXEC SQL FETCH cur1 INTO :sC1, :sC2;    
    }
    EXEC SQL WHENEVER NOT FOUND CONTINUE;
    ...
    EXEC SQL CLOSE cur1;    
    ... 
}
```

<a id="0f82459e9a890e22"></a>
### Description

The cursor is a distinguishable object in a session. The cursor being used in the current session has nothing to do with the cursor being used in another session.

To use OPEN cursor_name statement, it should be a cursor declared with [DECLARE cursor_name](#9826eadcd321de1b), and it should be a closed cursor.

<a id="03bfd36cb10e5315"></a>
### Examples

The following is an example of declaring a cursor and using OPEN cursor statement in an interactive SQL (gsql).

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

<a id="51834e57bd768d2c"></a>
### Compatibility

**SQL standard compatibility**

<a id="e992640cf5327184"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |

<a id="d9bc305e14472fa0"></a>
### For More Information

Refer to the followings.

- [DECLARE cursor_name](#9826eadcd321de1b)
- [FETCH cursor_name](#8b90e7e7e6e0c963)
- [CLOSE cursor_name](#8094485dc3cb5ea5)
- [PREPARE statement_name](#897dbc4fb97ab869)

<a id="897dbc4fb97ab869"></a>
## PREPARE statement_name

<a id="ba8eb5f8c37e8445"></a>
### Function

It prepares a dynamic SQL statement for a repeated execution.

<a id="0bb5a0e7633eedb3"></a>
### Syntax

```
<prepare statement> ::=
    PREPARE statement_name FROM <SQL statement variable>
    ;

<SQL statement variable> ::=
      variable_name
    | 'sql statement'
    | "sql statement"
    | sql statement
```

<a id="29042e1eb533e180"></a>
### Invocation and Access Rules

It can be used in an embedded SQL.  
An appropriate privilege according to the type of a dynamic SQL statement is required.

<a id="5f7a3404ec1383c2"></a>
### Syntax Rules and Parameters

<a id="b0e74b715452d373"></a>
#### statement_name

It is the name of the statement to be prepared.  
The length of the statement name should be shorter than 128 bytes.  
[EXECUTE statement_name](#ca4c1dbcc096bbdd) and [DECLARE cursor_name](#9826eadcd321de1b), which are to be performed later, refers to the statement_name.  
If the same statement_name exists, the previously prepared dynamic SQL is dropped.

```
{
    ...

    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1';
    ...
    EXEC SQL PREPARE stmt1 FROM 'UPDATE t1 SET c1 = c1 + 10';
    ...
}
```

<a id="64b61cb2a2c14803"></a>
#### &lt;SQL statement variable&gt;

&lt;SQL statement variable&gt; can be used as following four types.

- variable_name: It is a variable in which an SQL statement is stored. 
- 'sql statement': It is an SQL statement which is enclosed with single quote ('). 
- "sql statement": It is an SQL statement which is enclosed with double quotes ("). 
- sql statement: It is an SQL statement without quote.

The single quote (') is used twice as follows to represent string data within single-quoted string.

```
{
    ...
    PREPARE stmt_name FROM 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

The dynamic SQL statement referenced by &lt;SQL statement variable&gt; can use a host variable (:var) or parameter marker (?).   
However, if the unquoted SQL statement is used, the parameter marker (?) can not be used.

Depending on the characteristics of the referenced dynamic SQL statements, the variable can be either input or output dynamic parameter.   
The dynamic parameter described in the dynamic SQL statement does not have a meaning for the variable name, and it is identified by the specified order regardless of its type.

- Example 1

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 BETWEEN ? AND ?';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;   
    ...
}
```

- All parameter markers are the input dynamic parameters.
- The order to identify
    - No. 1 - BETWEEN ? 
        - Input dynamic parameter 
        - It uses the value of :sValue1. 
    - No. 2 - AND ? 
        - Input dynamic parameter 
        - It uses the value of :sValue2.

- Example 2

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT SUM(c2) INTO :v1 FROM t1 WHERE c1 > :v2';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;
    ...
}
```

- The input dynamic parameter and the output dynamic parameter exist.
- The order to identify 
    - No. 1 - :v1 
        - Output dynamic parameter 
        - It stores the value in :sValue1. 
    - No. 2 - :v2 
        - Input dynamic parameter 
        - It uses the value of :sValue2.

<a id="d32d40dc8e0404bb"></a>
#### variable_name

The type corresponding to variable_name should be a character string.  
The dynamic SQL statement defined in variable_name should be valid.

<a id="c9debd99fafe8fd9"></a>
#### sql statement

The dynamic SQL statement defined in the sql statement should be valid.

<a id="f07abfdb7b68f44f"></a>
### Description

PREPARE statement_name FROM sql_string statement analyzes SQL statement to use EXECUTE or cursor statement. Statement_name is an identifier which informs the precompiler the statement in an embedded SQL source code. A separate type or declaration is not required because statement_name is not a host variable.

For more information, refer to [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926).

<a id="55f4c9165af87d49"></a>
### Example

The following is an example of using PREPARE statement_name in an embedded SQL source code.

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

The full source code in which PREPARE statement_name was used can be viewed in [Dynamic Embedded SQL Example Program](../part-05-developer-manual/27-embedded-sql.md#3f9d137d2500f1fa).

<a id="17673d18f6f3704b"></a>
### Compatibility

**SQL standard compatibility**

<a id="eff856bee5431eea"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B034 | Dynamic specification of cursor attributes | X |

<a id="383593eb05e0f797"></a>
### For More Information

Refer to the followings.

- [EXECUTE statement_name](#ca4c1dbcc096bbdd)
- [DECLARE cursor_name](#9826eadcd321de1b)
- [EXECUTE IMMEDIATE 'sql_string'](#1eacad0a6072f76a)
- [Embedded Dynamic SQL](../part-05-developer-manual/27-embedded-sql.md#1462dee3f6bfd926)

<a id="065ee3ea308cf161"></a>
## RELEASE SAVEPOINT savepoint_specifier

<a id="b164d94a9142262d"></a>
### Function

It releases a savepoint.

<a id="c9aa5f7b5c60fdea"></a>
### Syntax

```
<release savepoint statement> ::=
    RELEASE SAVEPOINT savepoint_name 
    ;
```

<a id="eb5c188f9b5c11ad"></a>
### Syntax Rules and Parameters

<a id="c67c7a3316a2dc52"></a>
#### savepoint_name

It is a name of the savepoint, and it should exist.   
The length of the savepoint name should be shorter than 128 bytes.

<a id="343eab0dc34fbd66"></a>
### Description

If multiple savepoints are defined and RELEASE SAVEPOINT savepoint_name statement is performed, all savepoints defined since the savepoint_name are also released.

<a id="e7923db4c4d3bace"></a>
### Example

The following is an example of releasing a savepoint.

```
gSQL> RELEASE SAVEPOINT sp2;

Savepoint dropped.
```

<a id="1115da4e81cddfca"></a>
### Compatibility

**SQL standard compatibility**

<a id="7ef16d7de434ecfb"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="27f1effc0915ffff"></a>
### For More Information

Refer to the followings.

- [COMMIT](#97c03faa5a24c67f)
- [ROLLBACK](#30d00b80c704d186)
- [SAVEPOINT savepoint_specifier](#bf9e53dc119286d7)

<a id="1e240fa22ac10351"></a>
## REVOKE privileges FROM

<a id="e9f7394905d75e17"></a>
### Function

It revokes the granted privilege from a user.

<a id="66aa654d2a11c3d4"></a>
### Syntax

```
<revoke privilege statement> ::=
    REVOKE [ <revoke option extention> ] <privilege>
      FROM <grantee> [, ...]
      [ <revoke behavior> ]
    ;

<revoke option extention> ::=
      GRANT OPTION FOR

<revoke behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="8008b8ba70aa6f28"></a>
### Syntax Rules and Parameters

<a id="3468d61e1b60edaa"></a>
#### &lt;privilege&gt;

It is a privilege which is to be revoked from the revokee (the user whose privilege is to be revoked).

The revoker (the user who performs the statement) should satisfy one of the following conditions.

- If it is &lt;privilege&gt; which the revoker grants to the revokee.
    - Only the &lt;privilege&gt; which the revoker grants to the revokee is revoked. 
- If the revoker owns ACCESS CONTROL ON DATABASE privilege. 
    - The &lt;privilege&gt; which other grantors grant to the revokee is revoked.

When using ALL [PRIVILEGES], it succeeds even when the satisfying &lt;privilege&gt; does not exist.

For more information about the types of &lt;privilege&gt;, refer to [&lt;privilege&gt;](#0fbd8cc7ad66e02f) clause of [GRANT privileges TO](#5969f471eb288b39) statement.

<a id="1f0ebfade0018907"></a>
#### &lt;grantee&gt;

It is a user whose privilege is to be revoked.

- user_identifier 
    - It revokes the privilege of that user.
- PUBLIC 
    - They are authorization objects which mean all users.

<a id="a488e3cd4c02caa1"></a>
#### GRANT OPTION FOR

It revokes WITH GRANT OPTION included in the privilege.   
It also revokes WITH GRANT OPTION of the dependent privilege.

The privilege is maintained.

<a id="ab270d25391053ef"></a>
#### &lt;revoke behavior&gt;

- Dependent privilege: It is as same as the &lt;privilege&gt; which was granted to the revokee by using WITH GRANT OPTION and granted to another user by the revokee. 
- RESTRICT 
    - If the dependent privilege exists, it can not be revoked. 
- CASCADE 
    - The dependent privilege should also be revoked.
- CASCADE CONSTRAINTS 
    - The dependent privilege should also be revoked.
- If it is omitted, the default value is CASCADE.

<a id="0c04cfc71702e506"></a>
### Description

Data Definition Language (DDL) such as REVOKE privilege can be rolled back if it is before when the transaction is committed.

When performing the following DROP statement, all privilege information related to the object is revoked even without performing any separate REVOKE statement.

- DROP statement related to SQL schema object
    - [DROP TABLE](#b8225899a85c66e7)
    - [DROP VIEW](#c3d4597ac53c944b)
    - [DROP SEQUENCE](#98127fac6b27272b)
    - [ALTER TABLE name SET UNUSED COLUMN](#d1bfb6824c4855f9)
    - [DROP FUNCTION](../part-04-psm-manual/24-psm-sql-references.md#aec5d4c01f2a2c6d)
    - [DROP PROCEDURE](../part-04-psm-manual/24-psm-sql-references.md#8c112cc6728145b1)

- DROP statement related to non-schema object 
    - [DROP SCHEMA](#406abccf7b931f83)
    - [DROP TABLESPACE](#ee3406f353c996e6)
    - [DROP USER](#75a505d0fbae98f3)

<a id="ff92f68023b40f22"></a>
### Examples

The following is an example of revoking multiple privileges for the table t1.

```
gSQL> REVOKE INSERT, UPDATE, DELETE, LOCK, ALTER, INDEX ON t1 FROM u1;

Revoke succeeded.
```

The following is an example of revoking SELECT ON TABLE t1 privilege granted to the PUBLIC account, which means all users. However, only the privilege for PUBLIC account is revoked, and SELECT ON TABLE t1 privilege which was explicitly granted to a specific user is not revoked.

```
gSQL> REVOKE SELECT ON t1 FROM PUBLIC;

Revoke succeeded.
```

The following is an example that SELECT ON TABLE t1 privilege granted to user u1 is remained, and only REVOKE GRANT OPTION which can grant the privilege to another user is revoked.

```
gSQL> REVOKE GRANT OPTION FOR SELECT ON t1 FROM u1;

Revoke succeeded.
```

The following is an example that an error occurs when the privilege granted to the user u1 is revoked by using RESTRICT option and the user u1 grants it to another user. CASCADE option is used to revoke these dependent privileges as well.

```
gSQL> REVOKE SELECT ON t1 FROM u1 RESTRICT;

ERR-2B000(16235): dependent privilege descriptors still exist

gSQL> REVOKE SELECT ON t1 FROM u1 CASCADE;

Revoke succeeded.
```

<a id="cc840aff8f423ba5"></a>
### Compatibility

The SQL standard does not define the following privileges.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

&lt;revoke behavior&gt; of the SQL standard has the following differences.

- The default value of the SQL standard is RESTRICT.
- The SQL standard does not cover CASCADE CONSTRAINTS.

**SQL standard compatibility**

<a id="3584ae1656d74959"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T311 | Basic roles | X |
| F034 | Extended REVOKE statement | X |
| S081 | Subtables | X |

<a id="8b66038b0e9fbe20"></a>
### For More Information

Refer to the followings.

- [GRANT privileges TO](#5969f471eb288b39)
- [&lt;database privilege&gt;](#6cf78e61b1abff46)
- [&lt;tablespace privilege&gt;](#7be6b901f0ac9d48)
- [&lt;schema privilege&gt;](#f992ce28766780dd)
- [&lt;table privilege&gt;](#95da501d1083dbb2)
- [Column privilege](#3b4c834f85ebdb02)
- [&lt;sequence privilege&gt;](#ae119827fbf28a16)

<a id="30d00b80c704d186"></a>
## ROLLBACK

<a id="4740b1ba755f59b7"></a>
### Function

It rolls back a transaction, or the operation after the savepoint.

<a id="ef3cc2a998b42028"></a>
### Syntax

```
<rollback statement> ::=
    ROLLBACK [ WORK ] [ <rollback force clause> | <savepoint clause> ]
    ;

<rollback force clause> ::=
    FORCE 'xid_string' [ COMMENT 'comment_string' ]

<savepoint clause> ::=
    TO SAVEPOINT savepoint_name
```

<a id="38dfdf016f9ab6c2"></a>
### Syntax Rules and Parameters

<a id="d5ebd55773c41701"></a>
#### WORK

It is a reserved word which does not affect the operation.

<a id="0066ff32d864b9a3"></a>
#### &lt;rollback force clause&gt;

It is used to manually rollback the distributed transaction.

- FORCE 'xid_string'
    - It rolls back the distributed transaction corresponding to 'xid_string'.
    - 'xid_string' consists of 'format_id.transaction_id.branch_id'.
- COMMENT 'comment_string'
    - It specifies the comment on a transaction when rolling back the distributed transaction.

<a id="41a8458f16dce380"></a>
#### &lt;savepoint clause&gt;

It specifies the rollback scope of the current transaction.

- If it is omitted 
    - It undoes all operations of the current transaction. 
    - It ends the transaction. 
    - It deletes all savepoints. 
    - It releases all transaction locks.

- TO SAVEPOINT savepoint_name 
    - It undoes the operations of the current transaction since savepoint_name.
    - It does not end the transaction. 
    - It deletes all savepoints since savepoint_name. 
    - It releases all transaction locks acquired since savepoint_name.

<a id="df61f90f11969c3c"></a>
### Description

ROLLBACK statement undoes the following statements performed in the transaction.

- Data Manipulation Language (DML) statement
    - The statements to update data, such as INSERT, UPDATE and DELETE
- Data Definition Language (DDL) statement 
    - The statements to alter the structure and definition of the object such as CREATE, DROP, ALTER, TRUNCATE, GRANT and REVOKE

Exceptionally, the following statements of DDL which deals with OS resources or alters the DATA TYPE can not be rolled back, but are automatically committed when executing the statement.

- [CREATE TABLESPACE](#4fb45716ef9fbe7b)
- [DROP TABLESPACE](#ee3406f353c996e6)
- [ALTER TABLESPACE](#fb4ccb735469fcaa)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](#d1d235380dc3280c)

<a id="4a65966f723384c4"></a>
### Examples

The following is an example of rolling back the INSERT statement.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

The following is an example of ROLLBACK after performing the DROP TABLE statement.

```
gSQL> DROP TABLE t1;

Table dropped.

gSQL> SELECT * FROM t1;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM t1
              *
ERROR at line 1:

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.
```

<a id="2cc99549caaa6433"></a>
### Compatibility

**SQL standard compatibility**

<a id="a2f82c79a86090dd"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T271 | Savepoints | O |
| T261 | Chained transactions | X |

<a id="45b6156dea732792"></a>
### For More Information

Refer to the followings.

- [COMMIT](#97c03faa5a24c67f)
- [SAVEPOINT savepoint_specifier](#bf9e53dc119286d7)

<a id="bf9e53dc119286d7"></a>
## SAVEPOINT savepoint_specifier

<a id="a26fd3730b9492e2"></a>
### Function

It defines a savepoint.

<a id="7215f5c2b4dd3df5"></a>
### Syntax

```
<savepoint statement> ::=
    SAVEPOINT savepoint_name 
    ;
```

<a id="81ca22d121cd8440"></a>
### Syntax Rules and Parameters

<a id="6fd129226dc3826f"></a>
#### savepoint_name

It is a name of the savepoint.  
If the savepoint name is as same as the existing savepoint name, then the existing savepoint is deleted.  
The length of the savepoint name should be shorter than 128 bytes.

<a id="d803178ecabc359f"></a>
### Description

The defined savepoint is used by ROLLBACK TO SAVEPOINT statement (refer to [ROLLBACK](#30d00b80c704d186).), and DML or DDL statement which has been performed up to the savepoint is rolled back. Then the locks acquired by using that statement are released, too.

The defined savepoint is automatically deleted when the transaction is committed or rolled back, or it can be explicitly deleted by using [RELEASE SAVEPOINT savepoint_specifier](#065ee3ea308cf161).

<a id="f34ea42886340c25"></a>
### Example

The following is an example of defining the savepoint and using ROLLBACK TO SAVEPOINT statement.

```
gSQL> SAVEPOINT sp1;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SAVEPOINT sp2;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 2, 'someone' );

1 row created.

gSQL> SAVEPOINT sp3;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 3, 'anyone' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  
 3 anyone   

3 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp3;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  

2 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp2;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK TO SAVEPOINT sp1;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

<a id="f4fd13b4ed4c9b77"></a>
### Compatibility

**SQL standard compatibility**

<a id="eed58c1cff6f66d6"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="42a48fb2bdcb61b6"></a>
### For More Information

Refer to the followings.

- [COMMIT](#97c03faa5a24c67f)
- [ROLLBACK](#30d00b80c704d186)
- [RELEASE SAVEPOINT savepoint_specifier](#065ee3ea308cf161)

<a id="1117040fd802dbd4"></a>
## SELECT

<a id="1d9bd840c91d26e4"></a>
### query expression

<a id="21410c85121cd8e0"></a>
#### Function

It retrieves desired rows from one or more tables or views.

<a id="a82f97705cea2325"></a>
#### Syntax

```
<query expression> ::=
    <query expression body> [ <order by clause> ] [ <offset limit clause> ]

<query expression body> ::=
      <query term>
    | <set operator>

<query term> ::=
      <query specification>
    | <left paren> <query expression body> [ <order by clause> ] [ <offset limit clause> ] <right paren>
```

<a id="4b17c254285e50e2"></a>
#### Invocation and Access Rules

One of the following privileges for all tables used in the statement is required for a user to perform &lt;query expression&gt;.

- SELECT(columns) ON TABLE for all used columns of table in the statement 
- (SELECT or CONTROL TABLE) ON TABLE for the table
- (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- SELECT ANY TABLE ON DATABASE

<a id="eb7fc109b70e2ed3"></a>
#### Syntax Rules and Parameters

<a id="76d0625de926a509"></a>
##### &lt;set operator&gt;

It performs a set operation among the subqueries.  
For more information, refer to [set operator](#ab0a1ea34982332b).

<a id="9086592d836dfc6f"></a>
##### &lt;query specification&gt;

It specifies a single subquery.   
For more information, refer to [&lt;query specification&gt;](#9086592d836dfc6f).

<a id="8e29237c4d202cce"></a>
##### &lt;order by clause&gt;

It specifies sorting information of a query result.   
For more information, refer to [order by clause](#b9310b0f0bbe10c9).

<a id="6f6ecb2992a5d11a"></a>
##### &lt;offset limit clause&gt;

It specifies the number of rows to skip and the number of rows to fetch from the query result set.   
For more information, refer to [offset limit clause](#a7e3de58d6de6bbb).

<a id="66f502657bc0cd5f"></a>
#### Description

It is specifying SELECT statement, and &lt;order by clause&gt;, &lt;offset limit clause&gt; can be omitted and two or more subqueries can be specified through &lt;set operator&gt;.

<a id="87fc55bced2e541f"></a>
#### Examples

The following is an example of SELECT statement.

```
gSQL> SELECT s_name, s_nation FROM supplier;

S_NAME                    S_NATION     
------------------------- -------------
Supplier#1                FRANCE       
Supplier#2                KOREA        
Supplier#3                GERMANY      
Supplier#4                UNITED STATES
Supplier#5                CANADA       

5 rows selected.
```

The following is an example of the SELECT statement which uses &lt;order by clause&gt;.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

The following is an example of the SELECT statement which uses &lt;offset limit clause&gt;.

```
gSQL> SELECT s_name, s_nation FROM supplier OFFSET 1;

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT s_name, s_nation FROM supplier LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#1                FRANCE  

1 row selected.
```

The following is an example of the SELECT statement which uses &lt;order by clause&gt; and &lt;offset limit clause&gt;.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC OFFSET 3 LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA   

1 row selected.
```

<a id="0354f084ca7bfabe"></a>
#### Compatibility

**SQL standard compatibility**

<a id="8111f199584b820e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T121 | WITH(excluding RECURSIVE) in query expression | X |
| T122 | WITH(excluding RECURSIVE) in subquery | X |
| T131 | Recursive query | X |
| T132 | Recursive query in subquery | X |
| F661 | Simple tables | O |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING in query expressions | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | X |
| F851 | &lt;order by clause&gt; in subqueries | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F856 | Nested &lt;fetch first clause&gt; in &lt;query expression&gt; | X |
| F857 | Top-level &lt;fetch first clause&gt; in &lt;query expression&gt; | X |
| F858 | &lt;fetch first clause&gt; in subqueries | X |
| F860 | dynamic &lt;fetch first row count&gt; in &lt;fetch first clause&gt; | X |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt; in subqueries | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F865 | dynamic &lt;offset row count&gt; in &lt;result offset clause&gt; | X |
| F866 | FETCH FIRST clause: PERCENT option | X |
| F867 | FETCH FIRST clause: WITH TIES option | X |

<a id="3ec5b3395d1f51b6"></a>
### query specification

<a id="4ea8c77c30d4dd62"></a>
#### Function

It specifies the table which is derived from the result of &lt;table expression&gt;.

<a id="8c9c3dd31952b3bf"></a>
#### Syntax

```
<query specification> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list> <table expression>

<set quantifier> ::=
      ALL
    | DISTINCT

<table expression> ::=
      <from clause> [ <where clause> ] [ <group by clause> ] [ <having clause> ]
```

<a id="6bc2e0ca9c3887e0"></a>
#### Invocation and Access Rules

The use should satisfy one of the following conditions to perform &lt;query specification&gt;.

- The owner of that table 
- SELECT privilege for the table
- The user owns one of SELECT TABLE, CONTROL TABLE, CONTROL privileges for the schema to which the table belongs
- The user owns the SELECT TABLE privilege for the database

<a id="4c3c4a96487eeb7d"></a>
#### Syntax Rules and Parameters

<a id="9be565ee0e2185e1"></a>
##### &lt;hint clause&gt;

It specifies the hint for query execution.   
For more information, refer to [hint clause](#ad0ef76d32e7f521).

<a id="fe5abeaa22cb12d5"></a>
##### &lt;set quantifier&gt;

It specifies whether to remove a duplicate of the query result.   
If it is omitted, it operates in the same way as ALL.

<a id="0b70d0783e28ac36"></a>
##### &lt;select list&gt;

It specifies the expression to be output among query results.   
For more information, refer to [select list](#bd334f359dc73b47).

<a id="e41e502865243193"></a>
##### &lt;from clause&gt;

It specifies the tables to be retrieved.  
For more information, refer to [from clause](#15851b1e9d806918).

<a id="5ce48a51f4eeaee5"></a>
##### &lt;where clause&gt;

It specifies conditions for retrieving.  
For more information, refer to [where clause](#12ec541722ce6e3e).

<a id="c56ebbcbf9dffdcb"></a>
##### &lt;group by clause&gt;

It specifies grouping of the query result.  
For more information, refer to [group by clause](#2a27f113f4d9b2c1).

<a id="5bc85c52d748ad0b"></a>
##### &lt;having clause&gt;

It specifies conditions for the grouping result.  
For more information, refer to [having clause](#7fdb727a180a0ee5).

<a id="6883aeaccc91432e"></a>
#### Description

<a id="ca91f04770c56e2b"></a>
##### &lt;hint clause&gt;

&lt;hint clause&gt; is a statement that the user commands an optimizer to perform the better execution plan than the plan selected by an optimizer, if exist.

The optimizer of GOLDILOCKS preferentially applies &lt;hint clause&gt; specified by a user. If it is not applicable, the optimizer selects the best execution plan through the cost calculation.

Even when a syntactic error occurs in &lt;hint clause&gt;, GOLDILOCKS is set to ignore and perform it by default. Set "HINT_ERROR" property to *on*, then execute the query to check if a syntactic error exist in &lt;hint clause&gt;.

<a id="bfe2772ced502972"></a>
##### &lt;set quantifier&gt;

&lt;set quantifier&gt; sets whether to remove duplicates for each row consisting of the expressions specified in &lt;select list&gt;. The meaning of each set quantifier is as follows.

- ALL: It does not remove the duplicates from the result set. 
- DISTINCT: It removes the duplicates from the result set.

&lt;set quantifier&gt; can be omitted. If it is omitted, it is operated by default which is as same as ALL.

<a id="1e9463d4d574c48d"></a>
##### &lt;select list&gt;

&lt;select list&gt; specifies the expression list to be returned from each row of the result set.   
They are listed by separating by a comma (,).   
An asterisk (*) is used to specify all columns in &lt;from clause&gt;.

<a id="ec236f123e61918d"></a>
##### &lt;from clause&gt;

&lt;from clause&gt; specifies the tables or views to be retrieved.

<a id="aa963e764f8a7376"></a>
##### &lt;where clause&gt;

&lt;where clause&gt; specifies the conditions to get only the desired results from the result obtained from &lt;table expression&gt;.

<a id="fd01cdcd1d52fe3b"></a>
##### &lt;group by clause&gt;

&lt;group by clause&gt; specifies the grouping method for the result set acquired from &lt;table expression&gt;.

When &lt;group by clause&gt; is specified, only the group key determining the group, or aggregation function for the data belonging to the group can be used in &lt;select list&gt;.

<a id="10c14b54fe7dbc72"></a>
##### &lt;having clause&gt;

&lt;having clause&gt; specifies the retrieving condition for the group to get only the desired results from the grouped result set.  
It is generally used together with &lt;group by clause&gt;. When it is used without &lt;group by clause&gt;, the result set returned from &lt;table expression&gt; operates as same as when &lt;group by clause&gt;, a single group, is specified.

<a id="4ab7f47f51c2a663"></a>
#### Examples

The following is an example of SELECT statement which uses &lt;hint clause&gt;.

```
gSQL> SELECT /*+ INDEX_DESC(supplier, supplier_pk_index) */ s_name, s_nation FROM supplier;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

The following is an example of SELECT statement which uses &lt;set quantifier&gt;.

```
gSQL> SELECT ALL p_type FROM part;

P_TYPE
------
COPPER
NICKEL
STEEL
NICKEL
STEEL

5 rows selected.

gSQL> SELECT DISTINCT p_type FROM part;

P_TYPE
------
COPPER
STEEL
NICKEL

3 rows selected.
```

The following is an example of SELECT statement which uses &lt;where clause&gt;.

```
gSQL> SELECT p_name, p_brand, p_type, p_size FROM part where p_size < 10;

P_NAME P_BRAND    P_TYPE P_SIZE
------ ---------- ------ ------
Part#1 Brand#1    COPPER      7
Part#2 Brand#1    NICKEL      1

2 rows selected.
```

The following is an example of SELECT statement which uses &lt;group by clause&gt;.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         2             8025
         3            13864
         4            11564
         5             8744

5 rows selected.
```

The following is an example of SELECT statement which uses &lt;having clause&gt;.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey having SUM(ps_availqty) > 10000;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         3            13864
         4            11564

3 rows selected.
```

<a id="676cd319fb4d6fd8"></a>
#### Compatibility

**SQL standard compatibility**

<a id="ad3cab993e249b9e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F801 | Full set function | X |
| T051 | Row types | X |
| T301 | Functional dependencies | X |
| T325 | Qualified SQL parameter references | X |
| T053 | Explicit aliases for all-fields reference | O |
| T285 | Enhanced derived column names | O |

<a id="cb038f8c481bdc4a"></a>
#### For More Information

Refer to [query expression](#1d9bd840c91d26e4).

<a id="bd334f359dc73b47"></a>
### select list

<a id="597e5158faf047ce"></a>
#### Function

It specifies the columns to be retrieved from the query result.

<a id="ad00e2a5461f1815"></a>
#### Syntax

```
<select list> ::=
      <asterisk>
    | <select sublist> [ { <comma> <select sublist> } ... ]

<select sublist> ::=
      <derived column>
    | <qualified asterisk>

<qualified asterisk> ::=
      <asterisked identifier chain> <period> <asterisk>

<asterisked identifier chain> ::=
    <asterisked identifier> [ { <period> <asterisked identifier> } ... ]

<derived column> ::=
    <value expression> [ <as clause> ]

<as clause> ::=
    [ AS ] <column name>
```

<a id="9553071abc1b32a8"></a>
#### Invocation and Access Rules

If columns or subqueries exist in &lt;select list&gt; statement, to perform &lt;select list&gt;, a user should have the access privileges for the columns and the access privileges for the table and columns of the subqueries.

<a id="564b74f56ba2dbaa"></a>
#### Syntax Rules and Parameters

<a id="7e0ad904f9dd83e9"></a>
##### &lt;select list&gt;

It has &lt;asterisk&gt; or &lt;select sublist&gt;.   
&lt;asterisk&gt; can be used in &lt;select list&gt; only when it is alone. In other words, it can not specify &lt;select sublist&gt;.  
If two or more &lt;select sublist&gt; are specified, each &lt;select sublist&gt; should be separated by a comma(,).

<a id="2d25ef6b54f036d2"></a>
##### &lt;select sublist&gt;

It has &lt;derived column&gt; or &lt;qualified asterisk&gt;.   
A single table can have only one &lt;quantified asterisk&gt;.  
&lt;derived column&gt; can change the output name by using *AS*, and *AS* can be omitted.

<a id="1d0ba324f390fe11"></a>
#### Description

<a id="2b587411aac5f5ad"></a>
##### &lt;select list&gt;

&lt;select list&gt; specifies the columns to be included in the result set. If &lt;asterisk&gt; is specified in &lt;select list&gt;, all columns in &lt;from clause&gt; are specified as a select list, and &lt;select sublist&gt; can not be additionally specified.

<a id="8f88b6238e2ad79e"></a>
##### &lt;select sublist&gt;

&lt;select sublist&gt; has &lt;derived column&gt; or &lt;qualified asterisk&gt;. If two or more &lt;select sublist&gt; are specified, they should be separated by a comma (',').

For &lt;qualified asterisk&gt;, all columns belonging to a particular table or view are set as a select list. For &lt;derived column&gt;, the column can be directly specified, or &lt;value expression&gt; can be specified.

&lt;derived column&gt; can change the column name by using &lt;as clause&gt;, and *AS* can be omitted.

<a id="33d7af5dcdc51650"></a>
##### Names to Be Set in select list

- When &lt;column name&gt; is specified in &lt;derived column&gt;, the name is set as a select list name.
- When &lt;column name&gt; is not specified in &lt;derived column&gt;, the select list name is specified as follows.
    - If &lt;derived column&gt; is a single column reference, the column name of a single column is set to a select list name.
    - If &lt;derived column&gt; is SQL parameter reference, &lt;SQL parameter name&gt; of SQL parameter is set as a select list name.
    - Otherwise, the column name of &lt;derived column&gt; is not set. 
- When two or more tables exist in &lt;from clause&gt; and the columns with the same name are included in these tables, the table name or table alias should be specified to refer to these columns.

<a id="f001f657670253f9"></a>
#### Examples

The following is an example of SELECT statement which uses &lt;asterisk&gt;.

```
gSQL> SELECT * FROM supplier;

S_SUPPKEY S_NAME                    S_NATION      S_PHONE
--------- ------------------------- ------------- ---------------
        1 Supplier#1                FRANCE        27-918-335-1736
        2 Supplier#2                KOREA         15-679-861-2259
        3 Supplier#3                GERMANY       11-383-516-1199
        4 Supplier#4                UNITED STATES 25-843-787-7479
        5 Supplier#5                CANADA        21-151-690-3663

5 rows selected.
```

The following is an example of SELECT statement which uses &lt;select sublist&gt;.

```
gSQL> SELECT revenue.* FROM revenue;

SUPPLIER_NO TOTAL_REVENUE
----------- -------------
          1      11978.64
          2       20321.5
          3      41844.68

3 rows selected.

gSQL> SELECT supplier_no suppno, total_revenue AS TOTAL FROM revenue;

SUPPNO    TOTAL
------ --------
     1 11978.64
     2  20321.5
     3 41844.68

3 rows selected.

gSQL> SELECT 1, revenue.*, CAST( total_revenue AS NATIVE_INTEGER ) TOTAL FROM revenue;

1 SUPPLIER_NO TOTAL_REVENUE TOTAL
- ----------- ------------- -----
1           1      11978.64 11979
1           2       20321.5 20322
1           3      41844.68 41845

3 rows selected.
```

<a id="691382f49a9cc4fe"></a>
#### Compatibility

Unlike &lt;select list&gt;, the SQL standard supports &lt;all fields reference&gt;.

<a id="8404ffdef2af2e08"></a>
#### For More Information

Refer to [query specification](#3ec5b3395d1f51b6).

<a id="15851b1e9d806918"></a>
### from clause

<a id="b68360d3263b60e7"></a>
#### Function

It specifies the table which is derived from one or more tables.

<a id="9f81a6bfd588b449"></a>
#### Syntax

```
<from clause> ::=
    FROM <table reference list>

<table reference list> ::=
    <table reference> [ { , <table reference> } ... ]

<table reference> ::=
      <table factor>
    | <joined table>

<table factor> ::=
    <table primary>

<table primary> ::=
      <table name> [ <cluster domain> ] [ [ AS ] <correlation name> ]
    | <derived table> [ <cluster domain> ] [ [ AS ] <correlation name> [ <left paren> <derived column list> <right paren> ] ]
    | <parenthesized joined table>

<derived table> ::=
    <table subquery>

<parenthesized joined table> ::=
      <left paren> <parenthesized joined table> <right paren>
    | <left paren> <joined table> <right paren>

<derived column list> ::=
    <column name list>

<cluster domain> ::=
    @ <cluster domain name>

<cluster domain name> ::=
      GLOBAL
    | LOCAL
    | LOCAL_OFFLINE
    | <identifier>
```

<a id="1601bb020233d091"></a>
#### Invocation and Access Rules

The access privilege for the table or view specified in &lt;table reference list&gt; is required.

<a id="060238be0b56c346"></a>
#### Syntax Rules and Parameters

<a id="f9c730b298201906"></a>
##### &lt;table reference list&gt;

- One or more tables can be specified in &lt;table reference list&gt; by using a comma (,).
- When two or more tables are specified 
    - The evaluation order for the tables is from left to right.
    - When * is specified in &lt;select list&gt;, the columns are sequentially mapped in &lt;select list&gt; from the left table to the right table.

<a id="2099d59c800fe31d"></a>
##### &lt;table primary&gt;

An alias name can be specified by using &lt;correlation name&gt;.

&lt;table subquery&gt; is in &lt;derived table&gt;, and an alias name can be specified by using &lt;correlation name&gt;.  
&lt;derived column list&gt; can be specified in &lt;derived table&gt;, and the number of &lt;column name&gt; in &lt;derived column list&gt; should be same as the number of the target of &lt;select list&gt; specified in &lt;table subquery&gt;.

If &lt;derived column list&gt; is specified in &lt;derived table&gt;, then it is sequentially mapped one to one with targets of &lt;select list&gt; specified in &lt;table subquery&gt;.   
If &lt;derived column list&gt; is specified in &lt;derived table&gt;, &lt;column name&gt; in &lt;derived column list&gt; should be used to refer to &lt;select list&gt; of &lt;table subquery&gt; in &lt;derived table&gt;.

<a id="b35041cbd0c8a583"></a>
##### &lt;correlation name&gt;

The same &lt;correlation name&gt; should not exist two or more in &lt;table reference list&gt;.

When &lt;correlation name&gt; is specified in &lt;table name&gt; or &lt;derived table&gt;, &lt;correlation name&gt; should be used to refer to &lt;table name&gt; or &lt;derived table&gt;.

*AS* which is specified in front of &lt;correlation name&gt; can be omitted.

<a id="21e083e078ce4c5e"></a>
##### &lt;derived column list&gt;

The same &lt;column name&gt; should not exist two or more in &lt;derived column list&gt;.

<a id="4740582645f05008"></a>
##### &lt;cluster domain&gt;

- &lt;cluster domain&gt; may be a table, a view, or a table subquery, but a joined table in parentheses can not be &lt;cluster domain&gt;.
- &lt;cluster domain&gt; can not be specified in a table or a view whose structure or data is to be altered.
    - However, "@LOCAL" is specified in a target table for a data altering query created by [Processing SELECT in Cluster](12-sql-languages.md#10ffb2e825d49396).

<a id="5bb9b1a139e8e9f1"></a>
##### &lt;cluster domain name&gt;

Only a cluster group name or a cluster member name can be &lt;identifier&gt; of &lt;cluster domain name&gt;.

<a id="f007f35d80fc28ae"></a>
#### Description

<a id="f4289033e3418c8c"></a>
##### &lt;table reference list&gt;

Two or more tables can be specified in &lt;table reference list&gt; by using a comma (,). When specifying two or more tables, it operates in the same way as cross join each table from left to right. If the conditions to join two tables exist in &lt;where clause&gt;, the two tables operate in the same way as inner join which has &lt;where clause&gt; as a join condition.  
If outer join operator (+) is used in &lt;where clause&gt;, it operats in the same way as outer join.

For more information about outer join operator (+), refer to outer join operator specification of [joined table](#3b5e0afecad154e6).

<a id="c6a0015b6b52a269"></a>
##### &lt;table reference&gt;

A single table, or view, table subquery, joined table can be &lt;table reference&gt;. They can have a correlation name except for the joined table.

For more information about joined table, refer to [joined table](#3b5e0afecad154e6).

<a id="b3e9d21b4427033c"></a>
##### &lt;table primary&gt;

The tables, views, table subqueries and joined tables in parentheses can be &lt;table primary&gt;. The table, view, table subquery can have a correlation name, and 'AS' can be omitted. If the correlation name is specified, it should be used in everywhere referring to the table, view, table subquery such as &lt;select list&gt;, &lt;where clause&gt;.

The table subquery can specify &lt;derived column list&gt; by using parentheses. The name specified in &lt;derived column list&gt; should be used in everywhere referring to table subquery column like as correlation name. To use &lt;derived column list&gt; in the table subquery, the correlation name should be specified.

The joined table enclosed with parentheses specifies the logical join order for the table participating in the join operation. At this time, if all join operations for the tables enclosed with parentheses are cross join, inner join, the join order can be changed by an optimizer.

<a id="377ea845f717b872"></a>
##### &lt;cluster domain&gt;

When &lt;cluster domain&gt; is omitted, it means the same as using GLOBAL as &lt;cluster domain name&gt;.

<a id="4bcf4aa5273733fb"></a>
##### &lt;cluster domain name&gt;

The reserved words defined in &lt;cluster domain name&gt; mean as follows.

- GLOBAL
    - It selects all cluster groups as a cluster domain.
- LOCAL
    - It selects only the server performing the user query as a cluster domain.
- LOCAL_OFFLINE
    - If the table to which the domain is to be applied is offline, it selects only the server performing the user query as a cluster domain.
    - If LOCAL_OFFLINE domain is specified in an online table, then an error occurs.

If &lt;identifier&gt; is specified in &lt;cluster domain name&gt;, a cluster group or a cluster member with the corresponding name is selected as [Cluster Domain](12-sql-languages.md#e5a0136e74d8f68c).

<a id="af206c675a86189c"></a>
#### Examples

The following is an example of SELECT statement to query a single table by using &lt;table name&gt;.

```
gSQL> SELECT c_name, c_nation FROM customer;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

The following is an example of SELECT statement which uses &lt;derived table&gt;.

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.


gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer) AS CUST ("CUSTOMER_NAME", "CUSTOMER_NATION");

CUSTOMER_NAME CUSTOMER_NATION
------------- ---------------
Customer#1    KOREA          
Customer#2    CANADA         
Customer#3    KOREA          
Customer#4    GERMANY        
Customer#5    UNITED STATES  

5 rows selected.
```

The following is an example of SELECT statement for a joined table which uses parentheses.

```
gSQL> SELECT customer.c_name, o_totalprice FROM (customer INNER JOIN orders ON customer.c_custkey = orders.o_custkey);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

The following is an example of SELECT statement which uses two table separated by a comma (,).

```
gSQL> SELECT c_name, o_totalprice FROM customer, orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

The following is an example of SELECT statement which uses &lt;cluster domain&gt;.

- Using the reserved word GLOBAL

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@GLOBAL);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

- Using the reserved word LOCAL

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer)@LOCAL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- Using the cluster group name G1

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G1);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- Using the cluster member name G2N1

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G2N1);

C_NAME     C_NATION
---------- -------------
Customer#3 KOREA
Customer#4 GERMANY

2 rows selected.
```

<a id="ef16a5e040071627"></a>
#### Compatibility

The SQL standard has the following differences compared to GOLDILOCKS.

- It supports &lt;sample clause&gt; in &lt;table factor&gt;. 
- It supports &lt;lateral derived table&gt;, &lt;collection derived table&gt;, &lt;table function derived table&gt;, &lt;only spec&gt;, &lt;data change delta table&gt; in &lt;table primary&gt;.
    - &lt;lateral derived table&gt; allows &lt;from clause&gt; to refer to the left tables of the corresponding statement within subquery of &lt;lateral derived table&gt;. (e.g. select * from dual a,(select * from dual b where a.dummy = b.dummy);)
    - &lt;only spec&gt; does not allow the results of the subview to be included if the view of &lt;from clause&gt; is a hierarchical view.
- It supports system-versioned table in &lt;table primary&gt;. 
- It supports &lt;derived column list&gt; in &lt;table primary&gt;. 
- It supports &lt;transition table name&gt; and &lt;query name&gt; in &lt;table primary&gt;.
- &lt;correlation name&gt; should exist for &lt;derived table&gt;.

<a id="6e300e16a6487e2a"></a>
#### For More Information

Refer to [subquery](#831b79067708258d).

<a id="3b5e0afecad154e6"></a>
### joined table

<a id="65c8ab327472366e"></a>
#### Function

It specifies the table derived from a cartesian product, inner join, outer join.

<a id="a3076ba2f90980f8"></a>
#### Syntax

```
<joined table> ::=
      <cross join>
    | <qualified join>
    | <natural join>

<cross join> ::=
    <table reference> CROSS JOIN <table factor>

<qualified join> ::=
    <table reference> [ <join type> ] JOIN <table reference> <join specification>

<natural join> ::=
    <table reference> NATURAL [ <join type> ] JOIN <table factor>

<join specification> ::=
      <join condition>
    | <named columns join>

<join condition> ::=
    ON <search condition>

<named columns join> ::=
    USING ( <join column list> )

<join type> ::=
      INNER
    | { LEFT | RIGHT | FULL } [ OUTER ]

<join column list> ::=
    <column name list>
```

<a id="b607abbc99bed600"></a>
#### Invocation and Access Rules

The access privilege for all tables and views specified in a joined table is required.

<a id="d5d10bfaa03acac0"></a>
#### Syntax Rules and Parameters

<a id="052d399f7a229c32"></a>
##### &lt;cross join&gt;

&lt;join specification&gt; does not appear, and a single table, &lt;table subquery&gt; or &lt;joined table&gt; in parentheses can appear on the right.

<a id="cd5057579481b568"></a>
##### &lt;qualified join&gt;

- &lt;join specification&gt; should be specified.
- &lt;join type&gt; can be omitted. When it is omitted, it performs INNER.
- OUTER can be omitted in &lt;join type&gt;.
- If &lt;join type&gt; is OUTER JOIN, only &lt;join condition&gt; can appear in &lt;join specification&gt;. (If &lt;named columns join&gt; appears, an error occurs.)

<a id="76a6c3a83d6ed378"></a>
##### &lt;natural join&gt;

- &lt;join specification&gt; does not appear and a single table, &lt;table subquery&gt; or &lt;joined table&gt; in parentheses can appear on the right.
- &lt;join type&gt; can be omitted. When it is omitted, it performs INNER.
- It does not support OUTER in &lt;join type&gt;.
- If the same &lt;column name&gt; does not exist between the left row and right row of NATURAL JOIN, it performs &lt;cross join&gt;.
- If the same &lt;column name&gt; exists between the left row and right row of NATURAL JOIN, it is treated in the same way specified with USING clause.
- If comparison operation does not exist for the two corresponding columns, an error occurs.

<a id="f905faf6f314805f"></a>
##### &lt;join specification&gt;

- Only one of &lt;join condition&gt; or &lt;named columns join&gt; can be specified.
- When &lt;named columns join&gt; is specified
    - One or more column name should be specified in &lt;join column list&gt;.
    - The column name can not be specified such as &lt;table name&gt;.&lt;column name&gt;.
    - The listed columns in &lt;join column list&gt; should be on the left row and right row of JOIN, and they should be able to be compared.
    - If * is used in &lt;select list&gt;, the display column names of listed columns in &lt;join column list&gt; are corresponding column names, and those columns are excluded from the left row and right row of JOIN.
    - If * is used in &lt;select list&gt;, the display order of target is the listed columns in &lt;join column list&gt;, followed by the columns which does not correspond to &lt;join column list&gt; on the left row, then followed by the columns which does not correspond to &lt;join column list&gt; on the right row.
    - The columns corresponding to the left row and right row of the columns specified in &lt;join column list&gt; of the JOIN statement can not be referenced. (In other words, &lt;column name&gt; specified in &lt;join column list&gt; can not be referenced such as &lt;table name&gt;.&lt;column name&gt;, but only &lt;column name&gt; can be referenced.)
    - If the listed columns in &lt;join column list&gt; are treated using a join condition, the condition &lt;left table name&gt;.&lt;column name&gt; = &lt;right table name&gt;.&lt;column name&gt; is generated for each &lt;column name&gt;, and the conditions to treat each &lt;column name&gt; condition using AND are generated and processed.
    - It can not use '&lt;table name&gt;.*' phrase which returns all the row for a particular table to &lt;select list&gt;.
    - If comparison operation does not exist for the two corresponding columns, an error occurs.

<a id="1a90b445c84c3339"></a>
#### Description

<a id="f620a59b61e4281d"></a>
##### &lt;cross join&gt;

&lt;cross join&gt; returns a result which combines all of each left row with each right rows.

The explicit join condition can not be specified in &lt;cross join&gt;, but the join condition for the two tables can be specified in &lt;where clause&gt;. In this case, it performs inner join.

<a id="12e97a96f1cc3642"></a>
##### &lt;qualified join&gt;

&lt;qualified join&gt; returns results which satisfy the join condition in combinations of all right rows for each left row. If &lt;where clause&gt; exists, the conditions of &lt;where clause&gt; are applied to the result rows to which the join condition is applied when executing join statement.

The result is same, even when inner join treats the conditions in &lt;where clause&gt; in the same way as the join conditions. But result differs when outer join treats the conditions in &lt;where clause&gt; in the same way as the join conditions.

Left outer join returns combined results of rows when right rows satisfying the condition for the left rows exist. If right rows satisfying the condition for the left rows do not exist, then it keep the value of left rows and fill the value of right rows with NULL and return them as a result.

Right outer join is operated exactly contrary to the left outer join.

Full outer join returns the result of left outer join, and rows whose values of the left rows are filled with NULL for all right rows which do not satisfy the join condition.

<a id="d9d994d81dfdf09c"></a>
##### &lt;natural join&gt;

&lt;natural join&gt; joins all columns with same names in two tables participating in join as equal. In other words, it is as same as specifying all columns with same names in two tables participating in join in USING clause of inner join.

<a id="90572bc1a20e568b"></a>
##### &lt;join specification&gt;

&lt;join condition&gt; specifies the condition for joining left rows and right rows of a join statement. &lt;named columns join&gt; specifies the join condition by listing that &lt;column name&gt;, if the same &lt;column name&gt; exist in left rows and right rows.

<a id="1538823490b36267"></a>
#### Examples

The following is an example of SELECT statement which uses &lt;cross join&gt;.

```
gSQL> SELECT c_name, o_totalprice FROM customer CROSS JOIN orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

The following is an example of SELECT statement which uses inner join.

```
gSQL> SELECT c_name, o_totalprice FROM customer INNER JOIN orders ON c_custkey = o_custkey;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

The following is an example of SELECT statement which uses outer join.

```
gSQL> SELECT c_name, o_totalprice FROM customer LEFT OUTER JOIN orders ON c_custkey = o_custkey AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4    193846.25
Customer#5     144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer RIGHT OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
null           46929.18
null          193846.25
Customer#3     32151.78
null           144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer FULL OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA' AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4         null
Customer#5         null
null          173665.47
null           46929.18
null          193846.25
null           144659.2

9 rows selected.
```

The following is an example of SELECT statement which uses natural join.

```
gSQL> SELECT c_name, o_totalprice FROM (SELECT c_custkey custkey, c_name FROM customer) NATURAL JOIN (SELECT o_custkey custkey, o_totalprice FROM orders);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

<a id="8017a95013bbb52e"></a>
#### Compatibility

The SQL standard has the following differences compared to GOLDILOCKS.

- It supports &lt;partitioned join table&gt; for &lt;qualified join&gt; and &lt;natural join&gt;.
- It supports USING clause for the outer join.
- It supports the type for outer join as &lt;join type&gt; of &lt;natural join&gt;.
- It supports &lt;set function specification&gt; in &lt;join condition&gt;.

**SQL standard compatibility**

<a id="26ffc87c75fce322"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F401 | Extended joined table | O |
| F402 | Named column joins for LOBs, arrays, and multisets | X |
| F403 | Partitioned join tables | X |

<a id="576afed03c6563e0"></a>
#### For More Information

Refer to [from clause](#15851b1e9d806918).

<a id="12ec541722ce6e3e"></a>
### where clause

<a id="3a5e3b11a6ba8661"></a>
#### Function

It applies &lt;search condition&gt; to the result of &lt;from clause&gt;.

<a id="83f166de083b9252"></a>
#### Syntax

```
<where clause> ::=
    WHERE <search condition>
```

<a id="b11cf0ec8c6168e1"></a>
#### Syntax Rules and Parameters

<a id="3ba2155e12ae7478"></a>
##### &lt;where clause&gt;

&lt;search condition&gt; which returns a boolean type is required after WHERE keyword.

<a id="f3cd9264e4fcceeb"></a>
#### Description

For more information about &lt;where clause&gt;, refer to [Conditions](11-sql-elements.md#35320a70860f96ff).

<a id="3caface05593d57e"></a>
#### Example

The following is an example of SELECT statement which uses &lt;where clause&gt;.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation = 'KOREA';

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA

1 row selected.

gSQL> SELECT s_name, ps_availqty, ps_supplycost FROM supplier, partsupp WHERE s_nation = 'KOREA' AND s_suppkey = ps_suppkey;

S_NAME                    PS_AVAILQTY PS_SUPPLYCOST
------------------------- ----------- -------------
Supplier#2                       8076        993.49
Supplier#2                       4069        357.84

2 rows selected.
```

<a id="7cd694361f0a26a4"></a>
#### Compatibility

**SQL standard compatibility**

<a id="e4118961764f9245"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F441 | Extended set function support | O |

<a id="c9404a77c4a57787"></a>
#### For More Information

Refer to [query specification](#3ec5b3395d1f51b6).

<a id="2a27f113f4d9b2c1"></a>
### group by clause

<a id="42762148b99b0edb"></a>
#### Function

It specifies the grouped table of which &lt;group by clause&gt; was applied to the result processed by the previous statements.

<a id="87a51c21b3aef0de"></a>
#### Syntax

```
<group by clause> ::=
    GROUP BY <grouping element list>

<grouping element list> ::=
    <grouping element> [ { , <grouping element> } ... ]

<grouping element> ::=
      <ordinary grouping set>
    | <empty grouping set>

<ordinary grouping set> ::=
      <grouping column reference>

<grouping column reference> ::=
    <column reference>
    | <value_expression>

<empty grouping set> ::=
    <left paren> <right paren>
```

<a id="3c4e1f59977ba5ba"></a>
#### Invocation and Access Rules

Any separate access privilege is not required for a user to perform &lt;group by clause&gt;.

<a id="ad109413fdf282f0"></a>
#### Syntax Rules and Parameters

<a id="84c3c065277ba344"></a>
##### &lt;ordinary grouping set&gt;

It consists of one or more &lt;grouping column reference&gt;.  
It does not support LONG type.

<a id="eeb7cd22fd3ff726"></a>
##### &lt;empty grouping set&gt;

It can be specified by using only parentheses, and any expression should not be used within the parentheses.

<a id="41689f515f7447b8"></a>
#### Description

<a id="2233687c4d368526"></a>
##### &lt;grouping element list&gt;

&lt;grouping element&gt; in &lt;group by clause&gt; is grouped sequentially into a GROUPING SET. At this time, if all values of &lt;grouping element&gt; in GROUPING SET are matched sequentially, it is processed as the same group.

When &lt;group by clause&gt; is specified, the column in &lt;group by clause&gt; or the column, not in &lt;group by clause&gt; but in aggregate functions, can appear in &lt;select list&gt;.

<a id="34b37853d287eb95"></a>
##### &lt;grouping column reference&gt;

&lt;column reference&gt; or &lt;value expression&gt; can appear in &lt;grouping column reference&gt;.

For &lt;column reference&gt;, only the columns belong to &lt;from clause&gt; of &lt;query specification&gt; can be referenced. If columns with a same name exist, the column name should be explicitly specified by using the table name.

&lt;value expression&gt; consists of expressions which include or do not include &lt;column reference&gt;. The former can be divided into several groups by &lt;column reference&gt;, but all records of the latter are configured into a single group because all values of &lt;value expression&gt; is an identical constant value.

If NULL is specified in &lt;value expression&gt;, all NULL values are treated as the same value. Therefore, all records with NULL values are configured into a single group.

<a id="f02ccfcaf7912aa6"></a>
##### &lt;empty grouping set&gt;

&lt;empty grouping set&gt; specifies that the grouping target column does not exist. Therefore, all records are configured into a single group.

<a id="9bb15e6b3425ee47"></a>
#### Example

The following is an example of SELECT statement which uses GROUP BY clause.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation;

C_NATION      COUNT(C_NAME)
------------- -------------
UNITED STATES             1
CANADA                    1
KOREA                     2
GERMANY                   1

4 rows selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY NULL;

COUNT(C_NAME)
-------------
            5

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY ();

COUNT(C_NAME)
-------------
            5

1 row selected.
```

<a id="1c925ecafee87161"></a>
#### Compatibility

**SQL standard compatibility**

<a id="ce2f01249c7f69d9"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T431 | Extended grouping capabilities | X |
| T432 | Nested and concatenated GROUPING SETS | X |
| T434 | GROUP BY DISTINCT | X |

<a id="bd7f8bc7f851f07b"></a>
#### For More Information

Refer to the followings.

- [having clause](#7fdb727a180a0ee5)
- [query specification](#3ec5b3395d1f51b6)

<a id="7fdb727a180a0ee5"></a>
### having clause

<a id="59223d9d1f5bc234"></a>
#### Function

It specifies grouped tables having removed groups which do not satisfy &lt;search condition&gt;.

<a id="7835c1f17eb6e283"></a>
#### Syntax

```
<having clause> ::=
    HAVING <search condition>
```

<a id="f54df19c262d471b"></a>
#### Invocation and Access Rules

Any separate access privilege is not required for a user to perform &lt;having clause&gt;.

<a id="faa94086c6186d9e"></a>
#### Syntax Rules and Parameters

<a id="e94e6b13dbedbb8e"></a>
##### &lt;having clause&gt;

The columns which can be used without aggregate functions in &lt;search condition&gt; is only the columns specified in &lt;group by clause&gt;.  
The columns which are not specified in &lt;group by clause&gt; can be specified by using aggregate functions.

<a id="c85d425c2b0b736c"></a>
#### Description

<a id="160660640a150cdd"></a>
##### &lt;having clause&gt;

&lt;having clause&gt; specifies search conditions for the grouped data. Generally, it is used together with &lt;group by clause&gt;. When &lt;having clause&gt; is used without &lt;group by clause&gt;, it is considered as if "GROUP BY ()" exists.

Other columns can not be specified alone in &lt;having clause&gt; but only the columns specified in &lt;group by clause&gt; can be specified. Other columns can be used only when using aggregate functions.

<a id="3cebaf83bfffe2a2"></a>
#### Example

The following is an example of SELECT statement which uses &lt;having clause&gt;.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation HAVING COUNT(c_name) > 1;

C_NATION COUNT(C_NAME)
-------- -------------
KOREA                2

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer HAVING COUNT(c_name) > 1;

COUNT(C_NAME)
-------------
            5

1 row selected.
```

<a id="435b881d5caed20d"></a>
#### Compatibility

**SQL standard compatibility**

<a id="3f1366d8c3d8a2f2"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T301 | Functional dependencies | O |

<a id="28d3a93a340905e9"></a>
#### For More Information

Refer to the followings.

- [group by clause](#2a27f113f4d9b2c1)
- [Conditions](11-sql-elements.md#35320a70860f96ff)

<a id="b9310b0f0bbe10c9"></a>
### order by clause

<a id="cc5acf273eec86e3"></a>
#### Function

It specifies the sorting order of the query results.

<a id="a23c6266194c7b02"></a>
#### Syntax

```
<order by clause> ::=
    ORDER BY <sort specification list>

<sort specification list> ::=
    <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
    <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
    <value expression>

<ordering specification> ::=
      ASC
    | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST
```

<a id="fdac2ed2cc979714"></a>
#### Invocation and Access Rules

The access privilege for a column is required if the column exist in a sort key specified for sorting.

<a id="6db6cb76617d8853"></a>
#### Syntax Rules and Parameters

<a id="ca1c5c7057b153b6"></a>
##### &lt;order by clause&gt;

- When the column not used in &lt;select list&gt; of &lt;query specification&gt; is used as &lt;sort key&gt;, &lt;set quantifier&gt; DISTINCT or one or more &lt;set function specification&gt; can not be specified.
- However, the specified DISTINCT clause can be omitted in the followings, so the constraint above is not applied to them.
    - When &lt;group by clause&gt; or &lt;having clause&gt; is not specified, and one or more &lt;set function specification&gt; are specified.
    - When one or more nested &lt;set function specification&gt; are specified.
- If &lt;order by clause&gt; is specified in &lt;set operator&gt;, &lt;sort key&gt; is analysed based on the firstly specified &lt;query specification&gt;.

<a id="2b230b0e58befcd2"></a>
##### &lt;sort specification list&gt;

If &lt;ordering specification&gt; is not specified, the default value is ASC.   
If &lt;null ordering&gt; is not specified, the default value is NULLS LAST.

<a id="a0b9a4a294466f3e"></a>
##### &lt;sort key&gt;

- If &lt;value expression&gt; of &lt;sort key&gt; is the positive integer value whose scale is zero, the value is used as a sort key index.
    - The i-th &lt;select sublist&gt; of &lt;query specification&gt; which corresponds to the value is used as a sort key.
    - If the i-th &lt;select sublist&gt; of &lt;query specification&gt; which corresponds to the value does not exist, it returns an error.
- A row subquery or relation subquery is not supported as &lt;value expression&gt;.
- Other &lt;value expression&gt; are used as sort keys.

<a id="41c103b5143c5aa3"></a>
#### Description

<a id="74b5e0a118bf1b26"></a>
##### &lt;order by clause&gt;

&lt;order by clause&gt; specifies a method to sort the query results. &lt;sort key&gt; can be listed in &lt;order by clause&gt; by using a comma (,), and &lt;sort key&gt; of each records are compared and listed in order.

&lt;ordering specification&gt; can specify a sorting by an ascending or by a descending order in &lt;sort key&gt;. If it is omitted, it is regarded as a sorting by an ascending order.   
Also, &lt;null ordering&gt; specifies an order between the non-NULL values and NULL values in &lt;sort key&gt;. If it is omitted, it is regarded as NULLS LAST.

If a constant value is specified in &lt;sort key&gt;, the expression positioned in the location corresponding to its value in &lt;select list&gt; is regarded as &lt;sort key&gt;. In this case, the constant value should be equal to or smaller than the total number of expression in &lt;select list&gt;, and its scale should be 0.

LONG type can not be specified in &lt;sort key&gt;.

<a id="dfecef0bec319f2e"></a>
##### Comparison of Null Value

- The comparison between null values is regarded as the same value.
- The comparison between non-null value and null value is subject to the following rules.
    - When it is NULLS FIRST and ASC: null value < not null value
    - When it is NULLS LAST and ASC: null value > not null value
    - When it is NULLS FIRST and DESC: null value > not null value
    - When it is NULLS LAST and DESC: null value < not null value
- If the comparison result between null values is UNKNOWN, it is sorted according to the scan order.

<a id="68f677dd4426a2c2"></a>
##### Sorting Rows Which Have Same Sort Key Value

Peers are rows which can not be distinguished by a sort key, and the peers are sorted according to the scan order.

<a id="74c5332464cff881"></a>
##### &lt;aggregation function&gt; Which Is Used As &lt;sort key&gt;

If &lt;aggregation function&gt; is used in &lt;query specification&gt;, or &lt;group by clause&gt; is specified, &lt;aggregation function&gt; can be used as &lt;sort key&gt;. However, the nested aggregation function can be used as &lt;sort key&gt; only when &lt;group by clause&gt; is specified.

<a id="803360ba292b770b"></a>
#### Example

The following is an example of SELECT statement which uses ORDER BY clause.

```
gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#4 GERMANY
Customer#1 KOREA
Customer#3 KOREA
Customer#5 UNITED STATES

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation DESC;

C_NAME     C_NATION
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA
Customer#3 KOREA
Customer#4 GERMANY
Customer#2 CANADA

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY 2 DESC;

C_NAME     C_NATION     
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA        
Customer#3 KOREA        
Customer#4 GERMANY      
Customer#2 CANADA       

5 rows selected.
```

<a id="8ce8b843b3902bad"></a>
#### Compatibility

&lt;order by clause&gt; has the following differences compared to the SQL standard.

- The SQL standard supports only &lt;column reference&gt; as &lt;value expression&gt; of &lt;sort key&gt;.
- The SQL standard does not use &lt;value expression&gt; of &lt;sort key&gt; as a sort key index.

**SQL standard compatibility**

<a id="e654337e884dcc6b"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | X |
| F851 | &lt;order by clause&gt; in subqueries | O |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |

<a id="c1071c2c04a643f0"></a>
#### For More Information

Refer to [query expression](#1d9bd840c91d26e4).

<a id="a7e3de58d6de6bbb"></a>
### offset limit clause

<a id="995ce3076904d166"></a>
#### Function

It specifies the number of rows to skip and the number of rows to fetch from the query results.

<a id="370454c3b7b24791"></a>
#### Syntax

```
<offset limit clause> ::=
      <result offset clause>
    | <fetch limit clause>
    | <result offset clause> <fetch limit clause>

<result offset clause> ::=
    OFFSET <offset row count> [ { ROW | ROWS } ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ <fetch row count> ] [ ROW ONLY | ROWS ONLY ]

<limit clause> ::=
    LIMIT { <fetch row count> | <offset row count> , <fetch row count> | ALL }
```

<a id="c611b5788204a661"></a>
#### Invocation and Access Rules

The access privilege for &lt;offset limit clause&gt; is not required.

<a id="2e614b49808fd154"></a>
#### Syntax Rules and Parameters

<a id="bee49c088d0c944c"></a>
##### &lt;result offset clause&gt;

- &lt;offset row count&gt; value should be a positive integer which is equal to or bigger than zero.
- ROW and ROWS are keywords with the same meaning and they can be omitted.
- If the statement is omitted, it means as same as *OFFSET 0 ROWS*.

<a id="3a35a25181872759"></a>
##### &lt;fetch limit clause&gt;

- It specifies the number of rows to skip in the query result.
- If the statement is omitted, it means as same as *LIMIT ALL*.

<a id="89f9ac4af34ef519"></a>
##### &lt;fetch first clause&gt;

- It specifies the number of rows to fetch from the query result.
- It can not be used together with &lt;limit clause&gt;.
- FIRST and NEXT are keywords with the same meaning and they can be omitted.
- The value of &lt;fetch row count&gt; should be a positive integer which is bigger than zero.
- ROW ONLY and ROWS ONLY are keywords with the same meaning and they can be omitted.
- &lt;fetch row count&gt; can be omitted and if it is omitted, its value is one.

<a id="765d5e71a89c2751"></a>
##### &lt;limit clause&gt;

- It specifies the number of rows to fetch or, it specifies the number of rows to fetch and the number of rows to be skipped in query results together.
- It can not be used together with &lt;fetch first clause&gt;.
- When it is used as LIMIT &lt;fetch row count&gt;
    - &lt;fetch row count&gt; should be a positive integer which is bigger than zero.
    - The statement means as same as *FETCH FIRST &lt;fetch row count&gt; ROWS ONLY*.
- When it is used as LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;
    - It can not be used together with &lt;result offset clause&gt;.
    - &lt;offset row count&gt; should be a positive integer which is equal to or bigger than zero.
    - &lt;fetch row count&gt; should be a positive integer which is bigger than zero.
    - The statement means as same as *OFFSET &lt;offset row count&gt; ROWS FETCH FIRST &lt;fetch row count&gt; ROWS ONLY*.
- When it is used as LIMIT ALL
    - It does not limit the number of rows to fetch.

<a id="6d89df39f79a28ac"></a>
#### Description

<a id="6ca42c66d1b6209f"></a>
##### &lt;result offset clause&gt;

It returns rows starting from the &lt;offset row count&gt; th of the query results to a user. If &lt;offset row count&gt; is equal to or greater than the number of rows of query results, the returned result to a user is zero.

<a id="b36b440fb04fccc0"></a>
##### &lt;fetch first clause&gt;

It returns the query results to a user as many as the number of &lt;fetch row count&gt;.

<a id="86f26e9ffc975abd"></a>
##### &lt;limit clause&gt;

When it is used as LIMIT &lt;fetch_row_count&gt;, it returns the query results to a user as many as the number of &lt;fetch row count&gt;.

When it is used as LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;, it returns the query results to a user as many as the number of &lt;fetch row count&gt; from the &lt;offset row count&gt;th row.

When it is used as LIMIT ALL, it returns the query results to a user without limit of the number.

<a id="6f58e89d8dc8f71a"></a>
#### Examples

The following is an example of SELECT statement which uses &lt;result offset clause&gt;.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

4 rows selected.
```

The following is an example of SELECT statement which uses &lt;fetch first clause&gt;.

```
gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST 2 ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

The following is an example of SELECT statement which uses &lt;limit clause&gt;.

```
gSQL> SELECT c_name, c_nation FROM customer LIMIT 1;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT 1, 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT ALL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

The following is an example of SELECT statement which uses &lt;result offset clause&gt; and &lt;fetch limit clause&gt;.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 FETCH 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 LIMIT 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.
```

<a id="45ad7e2ea64f99ac"></a>
#### Compatibility

The SQL standard has the following differences compared to GOLDILOCKS.

- ROW or ROWS can not be omitted.
- FIRST or NEXT can not be omitted.
- It supports &lt;fetch first percentage&gt; in &lt;fetch first clause&gt;.
    - &lt;simple value specification&gt; can be any numeric in &lt;fetch first percentage&gt;. (In other words, a number below decimal point is also allowed.)
    - When &lt;fetch first percentage&gt; is specified, the value is converted to &lt;fetch row count&gt;. The conversion formula is as follows.
        - FRC = CEILING( FFP * LOCT / 100.0E0 )
        - FFP: The value of &lt;simple value specification&gt;
        - LOCT: The number of rows in the query results
        - FRC: The value which is converted to &lt;fetch row count&gt;
- It supports WITH TIES in &lt;fetch first clause&gt;
    - When using &lt;fetch first clause&gt; which specified WITH TIES, &lt;order by clause&gt; should exist.
    - When WITH TIES is specified, a sort key of &lt;order by clause&gt; returns the peers as many as the number of &lt;fetch row count&gt; based on the peers. The peers are units of rows whose sort keys are same.

> OFFSET and LIMIT syntax
> 
> - The SQL standard defines OFFSET .. FETCH {FIRST|NEXT} ... syntax. 
> - IBM DB2 and Postgres provide the same syntax as the SQL standard.
> - Postgres and MySQL provide OFFSET .. LIMIT syntax. 
> - Oracle performs a similar function through ROWNUM column.
> 

**SQL standard compatibility**

<a id="8152d5ebddc220fd"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt; in subqueries | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F865 | dynamic &lt;offset row count&gt; in &lt;result offset clause&gt; | X |

<a id="ab0a1ea34982332b"></a>
### set operator

<a id="4139074597fbb9eb"></a>
#### Function

It performs a set operation for results of the subquery.

<a id="82d1257e0c488e58"></a>
#### Syntax

```
<set operator> ::=
      <set operator term>
    | <query expression body> UNION [ ALL | DISTINCT ] <set operator term>
    | <query expression body> EXCEPT [ ALL | DISTINCT ] <set operator term>
    | <query expression body> MINUS [ ALL | DISTINCT ] <set operator term>

<set operator term> ::=
      <query term>
    | <set operator term> INTERSECT [ ALL | DISTINCT ] <set operator term>
```

<a id="ae68c18983fab43d"></a>
#### Invocation and Access Rules

All access privileges for the &lt;query expression&gt; in each &lt;set operator term&gt; are required for using &lt;set operator&gt; statement.

<a id="c0eb90283e3afceb"></a>
#### Syntax Rules and Parameters

<a id="04789246e05cbcb6"></a>
##### &lt;set operator&gt;

- It specifies the set operations among the subqueries.
- The number of the target in &lt;select list&gt; of each subquery should be same, and all matched targets should belong to the same data type group.
- The representative name of the result target of &lt;set operator&gt; is the target name of &lt;select list&gt; of the first subquery.
- If the processing order is not explicitly specified by using parentheses it processes by evaluating specified subqueries from the left to the the right.
- The meaning of each operator in &lt;set operator&gt; is as follows.
    - UNION
        - UNION ALL: It is a union of all subquery results without removing the duplicates.
        - UNION DISTINCT: It is a union of all subquery results, which removed the duplicates.
        - If at least one of ALL and DISTINCT is not specified, it is operated as same as when DISTINCT is specified.
    - EXCEPT
        - EXCEPT ALL: It returns the difference of all rows for the subquery result including all duplicates.
        - EXCEPT DISTINCT: It returns the difference of all rows for the subquery result excluding all duplicates.
        - If at least one of ALL and DISTINCT is not specified, it is operated as same as when DISTINCT is specified.
    - MINUS
        - It is an alias of EXCEPT and, it is operated as same as EXCEPT.
    - INTERSECT
        - INTERSECT ALL: It is a intersection of all subquery results without removing the duplicates.
        - INTERSECT DISTINCT: It is a intersection of all subquery results, which removed the duplicates.
        - If at least one of ALL and DISTINCT is not specified, it is operated as same as when DISTINCT is specified.

<a id="9901d4c11a1736d7"></a>
##### &lt;query term&gt;

It specifies the single subquery.  
For more information, refer to [query expression](#1d9bd840c91d26e4).

<a id="708bd5c53cdb4c1e"></a>
#### Description

<a id="57e3296f9a8d5679"></a>
##### The Differences between ALL and DISTINCT in &lt;set operator&gt;

For example, if the data of the table R1 and R2 is given as follows, the result of each &lt;set operator &gt; is as follows.

- TABLE data
    - R1 TABLE = {1, 1, 1, 2, 2, 2, 3, 4, 4, 5}
    - R2 TABLE = {1, 1, 3, 3, 4}
- SELECT * FROM R1 UNION ALL SELECT * FROM R2;
    - result = {1, 1, 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5}
- SELECT * FROM R1 UNION DISTINCT SELECT * FROM R2;
    - result = {1, 2, 3, 4, 5}
- SELECT * FROM R1 MINUS ALL SELECT * FROM R2;
    - result = {1, 2, 2, 2, 4, 5}
- SELECT * FROM R1 MINUS DISTINCT SELECT * FROM R2;
    - result = {2, 5}
- SELECT * FROM R1 INTERSECT ALL SELECT * FROM R2;
    - result = {1, 1, 3, 4}
- SELECT * FROM R1 INTERSECT DISTINCT SELECT * FROM R2;
    - result = {1, 3, 4}

<a id="297328629eb2fb74"></a>
![SET operation results](../assets/images/ee0bb0da1a2351f8.png)

<a id="e63922efd9e24995"></a>
##### Operator Precedence

The operator precedence of &lt;set operator&gt; is as follows.

- Parentheses ( ) has a priority.
- INTERSECT has a priority.
- For UNION and EXCEPT, the precedence is according to an order listed from left to right within an expression.

<a id="e47177c7aa293719"></a>
##### The Result Type of &lt;set operator&gt;

The i-th column of all subqueries in &lt;set operator&gt; should be a data type of the same family, and its result type is determined by  [Result Type Combination Rule](11-sql-elements.md#7b9ef315990930de).  
However, LONG VARCHAR and LONG VARBINARY types can only use UNION ALL.

<a id="1eedc13994a263ab"></a>
##### ORDER BY Clause

When &lt;set operator&gt; is used together with ORDER BY, and the column names are different among subqueries, then it can be used as follows.

- ORDER BY indicator
    - It specifies the order of result columns.  
      SELECT c1 FROM t1  
      UNION ALL  
      SELECT c2 FROM t2  
      ORDER BY 1;
- ORDER BY left_column_name
    - It specifies the column name of the first subquery.  
      SELECT c1 FROM t1  
      UNION ALL  
      SELECT c2 FROM t2  
      ORDER BY c1;

<a id="6b8854041c80dde3"></a>
#### Examples

The following is an example of SELECT statement which uses UNION operator.

```
gSQL> SELECT s_nation nation FROM supplier UNION ALL SELECT c_nation FROM customer;

NATION
-------------
FRANCE
KOREA
GERMANY
UNITED STATES
CANADA
KOREA
CANADA
KOREA
GERMANY
UNITED STATES

10 rows selected.

gSQL> SELECT s_nation nation FROM supplier UNION DISTINCT SELECT c_nation FROM customer;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY
FRANCE

5 rows selected.
```

The following is an example of SELECT statement which uses EXCEPT operator.

```
gSQL> SELECT c_nation nation FROM customer EXCEPT ALL SELECT s_nation FROM supplier;

NATION
------
KOREA

1 row selected.

gSQL> SELECT c_nation nation FROM customer EXCEPT DISTINCT SELECT s_nation FROM supplier;

no rows selected.
```

The following is an example of SELECT statement which uses INTERSECT operator.

```
gSQL> SELECT c_nation nation FROM customer INTERSECT ALL SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.

gSQL> SELECT c_nation nation FROM customer INTERSECT DISTINCT SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.
```

<a id="05d02d2b7de3aa6d"></a>
#### Compatibility

&lt;set operator&gt; has the following differences compared to the SQL standard.

- The SQL standard does not support MINUS.
- In the SQL standard, &lt;set operator&gt; can not be used together with ORDER BY indicator.
- In the SQL standard, if ORDER BY column_name is used together with &lt;set operator&gt;, it should be identical to the column name of all subqueries.

**SQL standard compatibility**

<a id="444cce94d79d933e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |

<a id="0f701b72ff865d61"></a>
#### For More Information

Refer to [query expression](#1d9bd840c91d26e4).

<a id="831b79067708258d"></a>
### subquery

<a id="fe6d201476792352"></a>
#### Function

It specifies the scalar value, row, table which are derived from &lt;query expression&gt;.

<a id="2bff9d1ccb9ae606"></a>
#### Syntax

```
<scalar subquery> ::=
    <subquery>

<row subquery> ::=
    <subquery>

<table subquery> ::=
    <subquery>

<subquery> ::=
    ( <query expression> )
```

<a id="6ea9dd642241a6e0"></a>
#### Invocation and Access Rules

The access privilege for &lt;query expression&gt; in &lt;subquery&gt; is required.

<a id="ebcb401779309a51"></a>
#### Syntax Rules and Parameters

<a id="ad4a6c02e0e070b8"></a>
##### &lt;scalar subquery&gt;

- The number of targets in &lt;query expression&gt; should be one.
- The result value according to the number of rows returned from &lt;query expression&gt; is as follows.
    - If the number of returned rows is zero, the result value is NULL.
    - If the number of returned rows is one, the result value is a value contained in the row.
    - If the number of returned rows is two or more, an exception error occurs.

<a id="14d73737e1233d3f"></a>
##### &lt;row subquery&gt;

- The number of target in &lt;query expression&gt; should be two or more.
- The result value according to the number of rows returned from &lt;query expression&gt; is as follows.
    - If the number of returned rows is zero, the result value is a row all of whose columns are NULL.
    - If the number of returned rows is one, the result value is that row.
    - If the number of returned rows is two or more, an exception error occurs.

<a id="fab66151ae05e9f7"></a>
##### &lt;table subquery&gt;

- The number of target in &lt;query expression&gt; should be one or more.
- The result according to the number of rows returned from &lt;query expression&gt; is as follows. 
    - If the number of returned rows is zero, the result value is *no rows*.
    - If the number of returned rows is one or more, the result value is that row.

<a id="236dfdad765b13f6"></a>
#### Description

<a id="e6cddad9669048f8"></a>
##### &lt;scalar subquery&gt;

&lt;scalar subquery&gt; returns one row which has one column as a result. The target of &lt;scalar subquery&gt; should be only one, and the result data type depends on the data type of the target.

&lt;scalar subquery&gt; can be used alone in the target of &lt;select list&gt;, and it can be used in the operator which has a single column.

<a id="5d4c04e3b4febc0a"></a>
##### &lt;row subquery&gt;

&lt;row subquery&gt; returns one row which has two or more columns as a result. The targets of &lt;row subquery&gt; should be two or more, and the result data type depends on the data type of each target.

&lt;row subquery&gt; can not be used alone in the target of &lt;select list&gt;, and it can only be used in the row operator which has two or more columns.

<a id="9d1bc0477d1e4e6c"></a>
##### &lt;table subquery&gt;

&lt;table subquery&gt; returns one or more rows which have one or more columns as a result. The targets of &lt;table subquery&gt; should be one or more, and the result data type depends on the data type of each target.

&lt;table subquery&gt; can not be used alone in the target of &lt;select list&gt;, but it can be used in the operators such as IN, NOT IN, EXISTS, NOT EXISTS, quantify operator.

<a id="3dda84da9b045414"></a>
#### Examples

The following is an example of SELECT statement which uses &lt;scalar subquery&gt;.

```
gSQL> SELECT (SELECT c_name FROM dual)  FROM customer;

(SELECT C_NAME FROM DUAL)
-------------------------
Customer#1
Customer#2
Customer#3
Customer#4
Customer#5

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer WHERE c_nation = (SELECT 'CANADA' FROM dual);

C_NAME     C_NATION
---------- --------
Customer#2 CANADA

1 row selected.
```

The following is an example of SELECT statement which uses &lt;row subquery&gt;.

```
gSQL> SELECT p_name, p_brand, p_type FROM part WHERE (p_brand, p_type) = (SELECT 'Brand#1', 'NICKEL' FROM dual);

P_NAME P_BRAND    P_TYPE
------ ---------- ------
Part#2 Brand#1    NICKEL

1 row selected.
```

The following is an example of SELECT statement which uses &lt;table subquery&gt;.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation IN (SELECT c_nation FROM customer);

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT * FROM (SELECT s_name, s_nation FROM supplier);

S_NAME                    S_NATION
------------------------- -------------
Supplier#1                FRANCE
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

5 rows selected.
```

<a id="8cffad0976e71b56"></a>
#### Compatibility

**SQL standard compatibility**

<a id="ad2054b7919d3f44"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F471 | Scalar subquery values | O |
| F641 | Row and table constructors | X |
| T501 | Enhanced EXISTS predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-12 | Correlated subqueries | O |

<a id="a6b30c9c3d5b2425"></a>
#### For More Information

Refer to the followings.

- [from clause](#15851b1e9d806918)
- [where clause](#12ec541722ce6e3e)

<a id="ad0ef76d32e7f521"></a>
### hint clause

<a id="295a150d5fc6aece"></a>
#### Function

It specifies a hint to be used for a query execution.

<a id="a1db7cbc95199d51"></a>
#### Syntax

```
<hint clause> ::=
    /*+ <hint element> [ comment ] [ [ , ] <hint element> [ comment ] ] */

<hint element> ::=
      <access path hints>
    | <join order hints>
    | <join operation hints>
    | <query transformation hints>
    | <other hints>

<access_path_hints> ::=
      FULL( table_name )
    | INDEX( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | NO_INDEX( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_ASC( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_DESC( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | INDEX_COMBINE( table_name [ , ] [ index_name [ [ , ] index_name ] ] )
    | ROWID( table_name )

<join order hints> ::=
      ORDERED
    | ORDERING( table_name [ LEFT | RIGHT ] [ , table_name [ LEFT | RIGHT ] ]
    | LEADING( table_name [ [ , ] table_name ] )

<join operation hints> ::=
      USE_HASH( table_name [ [ , ] table_name ] )
    | NO_USE_HASH( table_name [ [ , ] table_name ] )
    | USE_MERGE( table_name [ [ , ] table_name ] )
    | NO_USE_MERGE( table_name [ [ , ] table_name ] )
    | USE_NL( table_name [ [ , ] table_name ] )
    | NO_USE_NL( table_name [ [ , ] table_name ] )
    | USE_INL( table_name [ [ , ] table_name ] )
    | NO_USE_INL( table_name [ [ , ] table_name ] )

<query transformation hints> ::=
      UNNEST
    | NO_UNNEST
    | NL_SJ
    | NL_ISJ
    | MERGE_SJ
    | HASH_SJ
    | HASH_ISJ
    | HASH_AJ
    | TRANSITIVE_CLOSURE
    | NO_TRANSITIVE_CLOSURE
    | MERGE( view_name ) 
    | NO_MERGE( view_name ) 
    | NO_QUERY_TRANSFORMATION

<other hints> ::=
      PUSH_SUBQ
    | NO_PUSH_SUBQ
```

<a id="2c266873404cce70"></a>
#### Invocation and Access Rules

The privilege for query execution is required to perform &lt;hint clause&gt;.

<a id="371d0f462389f24a"></a>
#### Syntax Rules and Parameters

The basic syntax rules for &lt;hint clause&gt; are as follows.

- &lt;hint clause&gt; can be specify multiple &lt;hint element&gt; by using a space or ','.
- If two or more &lt;hint element&gt; for the same object exist and they are not applicable simultaneously, only the firstly specified &lt;hint element&gt; is applied. 
- When a syntax error occurs for &lt;hint element&gt;, it is ignored by default. If "hint_error" property is set to *on*, &lt;hint clause&gt; is treated as a validation error.
- When a table name is specified in &lt;hint clause&gt;, it should be identical to one of the table names (or the alias name if an alias name is specified in the table) in &lt;from clause&gt;.
- The table name can not be specified together with a schema name.
- Even when &lt;hint element&gt; is correctly specified, if it is not applicable, the optimizer ignores the &lt;hint element&gt;.

<a id="bf5e44a318c1c6d9"></a>
##### &lt;access_path_hints&gt;

<a id="cd67b94d58d8ebca"></a>
###### **FULL**

It instructs an optimizer to perform table full scan for the specified table. When this hint is specified, the optimizer does not take into account the optimization which uses the index scan, rowid scan, index combine.

When specifying FULL hint, the table name is required, and only a single table name should be specified. The specified table name should exist in &lt;from clause&gt;.

The following is an example of applying a hint to perform table full scan for the table T1.

• Type 1: The table name is specified in &lt;from clause&gt;.

```
SELECT /*+ FULL(T1) */ I1
  FROM T1;
```

• Type 2: The alias name is specified in &lt;from clause&gt;.

```
SELECT /*+ FULL(T1_ALIAS) */ I1
  FROM T1 T1_ALIAS;
```

<a id="87d29b7bd35ea4fb"></a>
###### **INDEX**

It instructs an optimizer to perform index scan for the specified table. When this hint is specified, the optimizer does not take into account the optimization which uses the table scan, index scan by another index, rowid scan, index combine.

When specifying INDEX hint, the table name should exist in &lt;from clause&gt;, and the index name should be the name of an index which exists in the table.

One or more index names can be specified or an index name can be omitted. If the index name is omitted, all indexes in the table are targeted.

If two or more index names are specified or an index name for the table with two or more indexes is omitted, an optimizer calculates scan cost of each index and selects the best index scan method.

The following is an example of applying a hint to perform index scan for the table T1.

• Type 1: Only one index name is specified.

```
SELECT /*+ INDEX(T1, T1_PK_INDEX) */ I1
  FROM T1;
```

• Type 2: Two or more index names are specified.

```
SELECT /*+ INDEX(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1;
```

• Type 3: The index name is omitted.

```
SELECT /*+ INDEX(T1) */ I1
  FROM T1;
```

<a id="86a17c65e884cded"></a>
###### **NO_INDEX**

It instructs an optimizer not to perform index scan for indexes corresponding to the index name in the specified table. When this hint is specified, the optimizer does not take into account the optimization which uses the index scan for the specifies indexes in the table.

When specifying NO_INDEX hint, the table name should exist in &lt;from clause&gt;, and the index name should be the name of an index which exists in the table.

One or more index names can be specified or an index name can be omitted. If the index name is omitted, an optimizer does not take into account the index scan for the table.

If indexes which are not specified in NO_INDEX hint exist, an optimizer calculates index scan cost for the indexes and selects the best scan method including table scan cost and rowid scan cost.

The following is an example of applying NO_INDEX hint to the table T1.

• Type 1: Only one index name is specified.

```
SELECT /*+ NO_INDEX(T1, T1_PK_INDEX) */ I1
  FROM T1;
```

• Type 2: Two or more index names are specified.

```
SELECT /*+ NO_INDEX(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1;
```

• Type 3: The index name is omitted.

```
SELECT /*+ NO_INDEX(T1) */ I1
  FROM T1;
```

<a id="bf10daf81c4484bd"></a>
###### **INDEX_ASC**

It instructs an optimizer to perform ascending index scan for the specified table. When this hint is specified, the optimizer does not take into account the optimization which uses the table scan, index scan by another index, rowid scan, index combine.

If the index of the selected index scan consists of ascending (descending) order, it scans the index in ascending (descending) order.

The syntax rule for INDEX_ASC hint is as same as the syntax rule for INDEX hint.

<a id="9d0ff1abd4a2cabe"></a>
###### **INDEX_DESC**

It instructs an optimizer to perform descending index scan for the specified table. When this hint is specified, the optimizer does not take into account the optimization which uses the table scan, index scan by another index, rowid scan, index combine.

If the index of the selected index scan consists of ascending (descending) order, it scans the index in ascending (descending) order.

The syntax rule for INDEX_ DESC hint is as same as the syntax rule for INDEX hint.

<a id="94207253cd1ef9fd"></a>
###### **INDEX_COMBINE**

It instructs an optimizer to separate OR statements and perform index scan for the specified table then to combine the results. When this hint is specified, the optimizer firstly takes into account the optimization which uses the index combine. If index combine is not available, it calculates the cost of table scan , index scan or rowid scan, and selects the best scan method.

When specifying INDEX_COMBINE hint, the table name should exist in &lt;from clause&gt;, and the index name should be the name of an index which exists in the table.

One or more index names can be specified or an index name can be omitted. If the index name is omitted, all indexes in the table are targeted.

OR statements should exist in the condition to scan the table to perform INDEX_COMBINE hint. If OR statement does not exist, an optimizer ignores the hint and it calculates the cost of the table scan, index scan or rowid scan, and chooses the best scan method.

If two or more index names are specified or an index name for the table with two or more indexes is omitted, an optimizer calculates index scan cost of each index in each OR statement, then selects the best index scan method. Therefore, it can selects an index scan which uses each different index for conditions separated by OR statements.

The following is an example of applying a hint to perform the index combine for the table T1.

• Type 1: Only one index name is specified.

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX) */ I1
  FROM T1
 WHERE I1 = 1
    OR I1 = 2;
```

• Type 2: Two or more index names are specified.

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX T1_UNIQUE_INDEX) */ I1
  FROM T1
 WHERE I1 = 1
    OR I2 = 2;
```

• Type 3: The index name is omitted.

```
SELECT /*+ INDEX_COMBINE(T1) */ I1
  FROM T1
 WHERE I1 = 1
    OR I2 = 2;
```

• Type 4: INDEX_COMBINE hint is not applicable. (An OR statement does not exist.)

```
SELECT /*+ INDEX_COMBINE(T1, T1_PK_INDEX) */ I1
  FROM T1
 WHERE I1 = 1;
```

<a id="0462ba479c82f981"></a>
###### **ROWID**

It instructs an optimizer to perform rowid scan for the specified table. When this hint is specified, the optimizer takes into account the optimization which uses the rowid scan firstly. If rowid scan is not available, it calculates the cost of table scan, index scan, index combine, and selects the best index scan method.

When specifying ROWID hint, the table name is required, and only a single table name should be specified. The specified table name should exist in &lt;from clause&gt;.

To perform ROWID hint, EQUAL condition using ROWID should exist in the condition to scan the table. If the EQUAL condition does not exist, an optimizer ignores the hint and it calculates the cost of table scan, index scan, index combine, and selects the best scan method.

The following is an example of applying a hint to perform ROWID scan for the table T1.

• Type 1: The table name is specified in &lt;from clause&gt;.

```
SELECT /*+ ROWID(T1) */ I1
  FROM T1
 WHERE ROWID = 'AAAAAAAAADXAACAAAGAlAAA';
```

• Type 2: The alias name is specified in &lt;from clause&gt;.

```
SELECT /*+ ROWID(T1_ALIAS) */ I1
  FROM T1 T1_ALIAS
 WHERE ROWID = 'AAAAAAAAADXAACAAAGAlAAA';
```

• Type 3: ROWID hint is not applicable. (A rowid condition does not exist.)

```
SELECT /*+ ROWID(T1) */ I1
  FROM T1
 WHERE I1 = 1;
```

<a id="9a4bbf30414b2af4"></a>
##### &lt;join_order_hints&gt;

<a id="5878a1dcd762a9c7"></a>
###### **ORDERED**

It instructs an optimizer to perform join in an order specified in &lt;from clause&gt; for the tables. This hint is applicable only when tables which are separated by ',' are specified in &lt;from clause&gt; or the tables are specified by inner join.

The following is an example of applying ORDERED hint for joining the tables T1 and T2.

• Type 1: The tables separated by ',' are specified in &lt;from clause&gt;.

```
SELECT /*+ ORDERED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: The tables are specified as inner join in &lt;from clause&gt;.

```
SELECT /*+ ORDERED */ *
  FROM T1 INNER JOIN T2 ON T1.I1 = T2.I1;
```

• Type 3: ORDERED hint is not applicable. (It is outer join.)

```
SELECT /*+ ORDERED */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

<a id="1af4bbe34aea17d8"></a>
###### **ORDERING**

It instructs an optimizer to perform join in an order of specified tables in this hint. This hint is applicable only when tables which are separated by ',' are specified in &lt;from clause&gt; or the tables are specified by inner join.

ORDERING hint can specify a positioning option for each table. The positioning option can not be specified for the first and second tables but it can be specified since the third table. The position for the first and second tables can be specified according to the order specified in the ORDERING hint.   
The positioning options are LEFT or RIGHT. LEFT locates a table to the left node (outer node) of join, and RIGHT locates a table to the right node (inner node) of join.

When the positioning option is specified in the table, the table executes join at the fixed position specified by the option. When the positioning option is not specified in the table, the optimizer calculates cost of positioning the table in the left node(outer node) and right node(inner node), and selects the best join order.

The following is an example of applying ORDERING hint for joining the tables T1, T2, T3.

• Type 1: The tables separated by ',' are specified in &lt;from clause&gt;.

```
SELECT /*+ ORDERING(T2, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

• Type 2: The tables are specified as inner join in &lt;from clause&gt;.

```
SELECT /*+ ORDERING(T2, T3, T1) */ *
  FROM (T1 INNER JOIN T2 ON T1.I1 = T2.I1) INNER JOIN T3 ON T2.I2 = T3.I2;
```

• Type 3: The positioning option is specified in ORDERING hint.

```
SELECT /*+ ORDERING(T2, T3, T1 LEFT) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

• Type 4: ORDERING hint is not applicable. (It is outer join.)

```
SELECT /*+ ORDERING(T1, T2) */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

• Type 5: The positioning option is misused in the ORDERING hint. (It is used in the first table.)

```
SELECT /*+ ORDERING(T2 RIGHT, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

<a id="6a042878734a97db"></a>
###### **LEADING**

It instructs an optimizer to perform join in an order of specified tables in this hint. This hint is applicable only when tables which are separated by ',' are specified in &lt;from clause&gt; or the tables are specified by inner join.

LEADING hint can not specify the position, unlike ORDERING hint, but it can specify the order of the table participating in join operation. Therefore, the first and second table is determined to be placed in the left node (outer node) and the right node (inner node) each according to the order.  
From the third table, the optimizer calculates cost of positioning the table in the left node (outer node) and right node(inner node), and selects a better position.

The following is an example of applying LEADING hint to join the tables T1, T2, T3.

• Type 1: The tables separated by ',' are specified in &lt;from clause&gt;.

```
SELECT /*+ LEADING(T2, T3, T1) */ *
  FROM T1, T2, T3
 WHERE T1.I1 = T2.I1
   AND T2.I2 = T3.I2;
```

• Type 2: The tables are specified as inner join in &lt;from clause&gt;.

```
SELECT /*+ LEADING(T2, T3, T1) */ *
  FROM (T1 INNER JOIN T2 ON T1.I1 = T2.I1) INNER JOIN T3 ON T2.I2 = T3.I2;
```

• Type 3: LEADING hint is not applicable. (It is outer join.)

```
SELECT /*+ LEADING(T1, T2) */ *
  FROM T1 LEFT OUTER JOIN T2 ON T1.I1 = T2.I1;
```

<a id="3140b84a021740cf"></a>
##### &lt;join operation_hints&gt;

<a id="54434c358824aa01"></a>
###### **USE_HASH**

It instructs an optimizer to perform join by using the hash join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

USE_HASH hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in USE_HASH hint are not allowed to be specified in USE_MERGE, USE_NL, USE_INL.   
When it is specified, if "hint_error" property is set to *on*, it is treated as a validation error.  If "hint_error" property is set to *off* the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node(outer node) is firstly applied.

When the table specified in USE_HASH hint participates in join, the condition which can hash join should exist in join condition. (The column should be comparable and it should be equi-join) If the condition does not exist, an optimizer ignores the hint and selects the best join operation according to the cost calculation.

The following is an example of applying USE_HASH hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ USE_HASH(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.           
&nbsp;(The order is determined according to ORDERED hint, and the join operation hint (USE_HASH) for   
&nbsp;&nbsp;the table T1 in the left node (outer node) is applied.)

```
SELECT /*+ ORDERED USE_HASH(T1) USE_MERGE(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 3: USE_HASH hint is not applicable. (A hash join condition does not exist.)

```
SELECT /*+ USE_HASH(T1, T2) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="2304cc60cd42979d"></a>
###### **NO_USE_HASH**

It instructs an optimizer to perform join by selecting one of the methods except for the hash join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

NO_USE_HASH hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in NO_USE_HASH hint are allowed to be specified in any other join operation hint except for USE_HASH hint.   
When the table specified in this hint is specified in USE_HASH hint, if "hint_error" property is set to on, it is treated as a validation error.  If "hint_error" property is set to off the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node (outer node) is firstly applied.

When tables specified in NO_USE_HASH hint participates in join, an optimizer calculates the cost of other join operations except for hash join, and selects the best join operation.

The following is an example of applying NO_USE_HASH hint to join of the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ NO_USE_HASH(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint specified in table T2 is applied, so the merge join is applied.)

```
SELECT /*+ NO_USE_HASH(T1) USE_MERGE(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="ca5b674f53425097"></a>
###### **USE_MERGE**

It instructs an optimizer to perform join by using a merge join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

USE_MERGE hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in USE_MERGE hint are not allowed to be specified in USE_HASH, USE_NL, USE_INL.   
When it is specified, if "hint_error" property is set to *on*, it is treated as a validation error.  If "hint_error" property is set to *off*, the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node(outer node) is firstly applied.

When the table specified in USE_MERGE hint participates in join, the condition which can merge join should exist in join condition. (The column should be comparable and it should be equi-join) If the condition does not exist, an optimizer ignores the hint and selects the best join operation according to the cost calculation.

The following is an example of applying USE_MERGE hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ USE_MERGE(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The order is determined according to ORDERED hint, and the join operation hint   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(USE_MERGE) is applied for the table T1 in the left node(outer node))

```
SELECT /*+ ORDERED USE_MERGE(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 3: USE_MERGE hint is not applicable. (A hash join condition does not exist.)

```
SELECT /*+ USE_MERGE(T1, T2) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="3b738790dcee2abb"></a>
###### **NO_USE_MERGE**

It instructs an optimizer to perform join by selecting one of the methods except for the merge join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

NO_USE_MERGE hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in NO_USE_MERGE hint are allowed to be specified in any other  join operation hint except for USE_MERGE hint.   
When the table specified in this hint is specified in USE_MERGE hint, if "hint_error" property is set to on, it is treated as a validation error.  If "hint_error" property is set to off the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node(outer node) is firstly applied.

When tables specified in NO_USE_MERGE hint participates in join, an optimizer calculates the cost of other join operations except for merge join, and selects the best join operation.

The following is an example of applying NO_USE_MERGE hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ NO_USE_MERGE(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint specified in table T2 is applied, so the hash join is applied.)

```
SELECT /*+ NO_USE_MERGE(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="46bafc130b952c38"></a>
###### **USE_NL**

It instructs an optimizer to perform join by using a nested loops join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

USE_NL hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in USE_NL hint are not allowed to be specified in USE_HASH, USE_MERGE, USE_INL.   
When it is specified, if "hint_error" property is set to *on*, it is treated as a validation error. If "hint_error" property is set to *off* the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node(outer node) is firstly applied.

The nested loops join, unlike the hash join and the merge join, can perform join without any constraints.

The following is an example of applying USE_NL hint to join of the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The order is determined according to ORDERED hint, and the join operation hint   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(USE_NL) is applied for the table T1 in the left node (outer node))

```
SELECT /*+ ORDERED USE_NL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="42542f2a8376651b"></a>
###### **NO_USE_NL**

It instructs an optimizer to perform join by selecting one of the methods except for the nested loops join method if the table specified in this hint is included when performing join. This hint is applicable to all join types.

NO_USE_NL hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in NO_USE_NL hint are allowed to be specified in any other join operation hint except for USE_NL hint.  
When the table specified in this hint is specified in USE_NL hint, if "hint_error" property is set to *on*, it is treated as a validation error. If "hint_error" property is set to *off* the firstly specified hint is applied.  
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node (outer node) is firstly applied.

When tables specified in NO_USE_NL hint participates in join, an optimizer calculates the cost of other join operations except for nested loops join, and selects the best join operation.   
However, if other join operations can not be used because of constraints, the optimizer ignores the hint, and selects the nested loops join.

The following is an example of applying NO_USE_NL hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ NO_USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint specified in table T2 is applied, so the hash join is applied.)

```
SELECT /*+ NO_USE_NL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 3:  NO_USE_NL hint is specified but the join operation such as hash join can not be applied   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;because of constraints.   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(A nested loops join is applied.)

```
SELECT /*+ NO_USE_NL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 < T2.I1;
```

<a id="0fa109b07c79c35b"></a>
###### **USE_INL**

It instructs an optimizer to perform join by using a nested loops join method which uses a sort instant if the table specified in this hint is included when performing join.   
This hint is applicable only when tables which are separated by ',' are specified in &lt;from clause&gt; or the tables are specified by inner join.

USE_INL hint should specifies one or more tables, and it can not specify identical tables more than two. The tables specified in USE_INL hint are not allowed to be specified in USE_HASH, USE_MERGE, USE_NL.   
When it is specified, if "hint_error" property is set to *on*, it is treated as a validation error. If "hint_error" property is set to *off*, the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node (outer node) is firstly applied.

The nested loops join using a sort instant creates a sort instance whose sort key is expressions satisfying the join condition for the table in the right node (inner node), and performs  join using it. In this case, the sort key should be a type which can perform key compare.   
If all expressions satisfying the join condition are a type which can not perform key compare, this method can not be applied. In this case, an optimizer calculates the cost of other join operations and selects the best join operation.

The following is an example of applying USE_INL hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ USE_INL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The order is determined according to ORDERED hint, and the join operation hint   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(USE_INL) is applied for the table T1 in the left node (outer node))

```
SELECT /*+ ORDERED USE_INL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="b20367d29daa4a20"></a>
###### **NO_USE_INL**

It instructs an optimizer to perform join by selecting one of the methods except for the nested loops join method which uses a sort instant if the table specified in this hint is included when performing join. This hint is applicable to all join types.

NO_USE_INL hint should specify one or more tables, and it can not specify identical tables more than two. The tables specified in NO_USE_INL hint are allowed to be specified in any other  join operation hint except for USE_INL hint.   
When the table specified in this hint is specified in USE_INL hint, if "hint_error" property is set to *on*, it is treated as a validation error.  If "hint_error" property is set to *off* the firstly specified hint is applied.   
Also, if each different join operation hints are specified for two tables participating in join, the hint specified in the left node(outer node) is firstly applied.

When tables specified in NO_USE_INL hint participates in join, an optimizer calculates the cost of other join operations except for the nested loops join method which uses a sort instant, and selects the best join operation..

The following is an example of applying NO_USE_INL hint to join the tables T1, T2.

• Type 1: The join operation hint is specified only for a single table.

```
SELECT /*+ NO_USE_INL(T1) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

• Type 2: Each different join operation hints are specified for two tables.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint specified in table T2 is applied, so the hash join is applied.)

```
SELECT /*+ NO_USE_INL(T1) USE_HASH(T2) */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1;
```

<a id="19c46915111cbf21"></a>
##### &lt;query_transformation_hints&gt;

<a id="d9be4134559ece49"></a>
###### **UNNEST**

It instructs an optimizer to change subqueries to the join statement which guarantees the same results. Therefore, it does not repeatedly perform subqueries by using the method to treat the join with the upper-level query instead of separately performing a subquery.

The UNNEST hint can be specified only in &lt;hint clause&gt; of the subquery. It is applied only to the subquery, and is not applied to subordinate subqueries.   
To unnest all subqueries when multiple subqueries exist, the UNNEST hints should be specified for all subqueries. To unnest a subquery which exist within a subquery, the UNNEST hints should be specified for that subquery.

If UNNEST hint is specified together with NO_QUERY_TRANSFORMATION hint, UNNEST hint is ignored due to NO_QUERY_TRANSFORMATION hint.

UNNEST hint can not be used simultaneously with the NO_UNNEST hint. If they are used simultaneously and "hint_error" property is set to *on*, it is treated as a validation error. If "hint_error" property is set to *off* the firstly specified hint is applied.

The following is an example of applying unnesting to a subquery by using UNNEST hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST */ I1
                 FROM T2 );
```

• Type 2: UNNEST hint and NO_QUERY_TRANSFORMATION hint are specified.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The subquery is not unnested due to NO_QUERY_TRANSFORMATION hint.)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST NO_QUERY_TRANSFORMATION */ I1
                 FROM T2 );
```

<a id="b1bb2cf030d6de06"></a>
###### **NO_UNNEST**

It instructs an optimizer to process a subquery as a filter instead of unnesting. This performs subquery whenever in need.

NO_UNNEST hint can be specified only in &lt;hint clause&gt; of a subquery. It is applied only to the subquery, and is not applied to subordinate subqueries.   
Not to unnest all subqueries when multiple subqueries exist, the NO_UNNEST hints should be specified for all subqueries. Not to unnest a subquery which exist within a subquery, the NO_UNNEST hints should be specified for that subquery.

If NO_UNNEST hint is specified together with NO_QUERY_TRANSFORMATION hint, NO_UNNEST hint is ignored due to NO_QUERY_TRANSFORMATION hint.

NO_UNNEST hint can not be used simultaneously with UNNEST hint. If they are used simultaneously and "hint_error" property is set to *on*, it is treated as a validation error. If "hint_error" property is set to *off*, the firstly specified hint is applied.

The following is an example of applying no unnesting to a subquery by using NO_UNNEST hint.

- It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NO_UNNEST */ I1
                 FROM T2 );
```

<a id="dd7087d376aec62f"></a>
###### **NL_SJ**

It instructs an optimizer to process a subquery by using nested loops semi join. This method changes the subquery to a semi join form which has the same result.

NL_SJ hint can be used in EXISTS, IN, ANY quantify operator and it can not be used in NOT EXISTS, NOT IN, ALL quantify operator.

The optimizer ignores NL_SJ hint when it is specified in a subquery which can be changed only to anti-semi join form because NL_SJ hint changes the subquery to semi join form.

The following is an example of changing a subquery to a join form by using NL_SJ hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NL_SJ */ I1
                 FROM T2 );
```

• Type 2: It is used in EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ NL_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 < ANY ( SELECT /*+ NL_SJ */ I1
                    FROM T2 );
```

• Type 4: It is used in NOT IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to anti-semi join)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ NL_SJ */ I1
                     FROM T2 );
```

<a id="1f45467878fec6d6"></a>
###### **NL_ISJ**

It instructs an optimizer to process a subquery by using nested loops inverted semi join. This method changes the subquery to a inverted semi join form which has the same result.

Inverted semi join creates a sort instant which has a key for a semi join as a unique sort key on the right node (inner node). Then it reversely searches for a record which is identical to the corresponding key from the left node (outer node).

NL_ISJ hint is more advantageous in case when there are many duplicate right nodes (inner nodes) for keys of semi join and the key in the left node (outer node) can perform the index scan.   
The optimizer ignores the hint when the index scan can not be performed in the left node (outer node) for the key of semi join. Also, the optimizer ignores the hint when the key compare for the key of semi join can not be performed.

NL_ISJ hint can be used in EXISTS, IN, = ANY quantify operator, and it can not be used in NOT EXISTS, NOT IN, ALL quantify operator, and ANY quantify operator except for =ANY.

The optimizer ignores NL_ISJ hint when it is specified in a subquery which can be changed only to anti-semi join form because NL_ISJ hint changes the subquery to semi join.

The following is an example of changing a subquery to a join form by using NL_ISJ hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NL_ISJ */ I1
                 FROM T2 );
```

• Type 2: It is used in EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ NL_ISJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ NL_ISJ */ I1
                    FROM T2 );
```

• Type 4: It is used in NOT IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to anti-semi join)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ NL_ISJ */ I1
                     FROM T2 );
```

<a id="77dd39569aeb849d"></a>
###### **MERGE_SJ**

It instructs an optimizer to process a subquery by using merge semi join. This method changes the subquery to a semi join form which has the same result.

MERGE_SJ hint can be used in EXISTS, IN, = ANY quantify operator, and it can not be used in NOT EXISTS, NOT IN, ALL quantify operator, and ANY quantify operator except for =ANY.

The optimizer ignores MERGE_SJ hint when it is specified in a subquery which can be changed only to anti-semi join form because MERGE_SJ hint changes the subquery to semi join. Also, the optimizer ignores the hint when the key compare for the key of merge semi join can not be performed.

The following is an example of changing a subquery to a join form by using MERGE_SJ hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ MERGE_SJ */ I1
                 FROM T2 );
```

• Type 2: It is used in EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ MERGE_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ MERGE_SJ */ I1
                    FROM T2 );
```

• Type 4: It is used in NOT IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to anti-semi join)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ MERGE_SJ */ I1
                     FROM T2 );
```

<a id="558cc0fa1cf6bff3"></a>
###### **HASH_SJ**

It instructs an optimizer to process a subquery by using hash semi join. This method changes the subquery to a semi join form which has the same result.

HASH_SJ hint can be used in EXISTS, IN, = ANY quantify operator, and it can not be used in NOT EXISTS, NOT IN, ALL quantify operator, ANY quantify operator except for = ANY.

The optimizer ignores HASH_SJ hint when it is specified in a subquery which can be changed only to anti-semi join form because HASH_SJ hint changes the subquery to semi join. Also, the optimizer ignores the hint when the key compare for the key of hash semi join can not be performed.

The following is an example of changing a subquery to a join form by using HASH_SJ hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_SJ */ I1
                 FROM T2 );
```

• Type 2: It is used in EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ HASH_SJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ HASH_SJ */ I1
                    FROM T2 );
```

• Type 4: It is used in NOT IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to anti-semi join)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_SJ */ I1
                     FROM T2 );
```

<a id="4fedef042e4421a0"></a>
###### **HASH_ISJ**

It instructs an optimizer to process a subquery by using hash inverted semi join. This method changes the subquery to a inverted semi join form which has the same result.

HASH_ISJ hint is more advantageous in the case that the number of rows of the left node (outer node) is small, whereas the number of rows of the right node (inner node) is large. The optimizer ignores the hint when the key compare for the key of semi join can not be performed.

HASH_ISJ hint can be used in EXISTS, IN, = ANY quantify operator, and it can not be used in NOT EXISTS, NOT IN, ALL quantify operator, ANY quantify operator except for = ANY.

The optimizer ignores HASH_ISJ hint when it is specified in a subquery which can be changed only to anti-semi join form because HASH_ISJ hint changes the subquery to semi join. Also, the optimizer ignores the hint when the key compare for the key of hash semi join can not be performed.

The following is an example of changing a subquery to a join form by using HASH_ISJ hint.

• Type 1: It is used in IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_ISJ */ I1
                 FROM T2 );
```

• Type 2: It is used in EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE EXISTS ( SELECT /*+ HASH_ISJ */ I1
                  FROM T2
                 WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 = ANY ( SELECT /*+ HASH_ISJ */ I1
                    FROM T2 );
```

• Type 4: It is used in NOT IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to anti-semi join)

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_ISJ */ I1
                     FROM T2 );
```

<a id="1e085f71f5651036"></a>
###### **HASH_AJ**

It instructs an optimizer to process a subquery by using hash anti-semi join. This method changes the subquery to a anti-semi join form which has the same result.

HASH_AJ hint can be used in NOT EXISTS, NOT IN, != ALL quantify operator, and it can not be used in EXISTS, IN, ANY quantify operator, ALL quantify operator except for != ALL.

The optimizer ignores HASH_AJ hint when it is specified in a subquery which can be changed only to semi join form because HASH_AJ hint changes the subquery to anti-semi join. Also, the optimizer ignores the hint when the key compare for the key of hash semi join can not be performed.

The following is an example of changing a subquery to a join form by using HASH_AJ hint.

• Type 1: It is used in NOT IN subquery.

```
SELECT *
  FROM T1
 WHERE I1 NOT IN ( SELECT /*+ HASH_AJ */ I1
                     FROM T2 );
```

• Type 2: It is used in NOT EXISTS subquery.

```
SELECT *
  FROM T1
 WHERE NOT EXISTS ( SELECT /*+ HASH_AJ */ I1
                      FROM T2
                     WHERE T1.I1 = T2.I1 );
```

• Type 3: It is used in the subquery of a quantify operator.

```
SELECT *
  FROM T1
 WHERE I1 != ALL ( SELECT /*+ HASH_AJ */ I1
                     FROM T2 );
```

• Type 4: It is used in IN subquery.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The hint is ignored because it is an operator which can be changed to semi join)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ HASH_AJ */ I1
                 FROM T2 );
```

<a id="ff1348d41992d8ce"></a>
###### **TRANSITIVE_CLOSURE**

If A=B and B = C, then A=C. The relation like this is applied to a join predicate.

• 'T1.i1 = T2.i1' and 'T2.i1 = T3.i1' create 'T1.i1 = T3.i1' predicate.   
&nbsp;&nbsp;&nbsp;However, if it is not used in a join ordering, then it will be automatically deleted.

```
SELECT *
  FROM T1, T2, T3
 WHERE T1.i1 = T2.i1 AND T2.i1 = T3.i1;
```

In the example above, if the join ordering is ((t1 ⋈ t2) ⋈ t3), then only one predicate with higher selectivity is selected between 'T2.i1 = T3.i1' and 'T1.i1 = T3.i1'. If the  join ordering is ((t1 ⋈ t3) ⋈ t2), then only one predicate with higher selectivity is selected between 'T1.i1 = T2.i1' and 'T2.i1 = T3.i1'.

<a id="fda93d89fdfb6ce2"></a>
###### **NO_TRANSITIVE_CLOSURE**

It does not apply the join transitive closure to a join predicate.

• 'T1.i1 = T2.i1' and 'T2.i1 = T3.i1' does not create 'T1.i1 = T3.i1' predicate.

```
SELECT *
  FROM T1, T2, T3
 WHERE T1.i1 = T2.i1 AND T2.i1 = T3.i1;
```

The join transitive closure is not applied, so 'T1.i1 = T3.i1' predicate= does not exist. Therefore, the join ordering such as ((t1 ⋈ t3) ⋈ t2) can not occur.

<a id="ea5f77a665775d03"></a>
###### **MERGE**

It instructs an optimizer to apply a simple view merging to the specified view when it is possible. This hint should be specified in superordinate query block which includes the specified view.

If MERGE hint is used together with &lt;join order hints&gt;, &lt;join operation hints&gt;, &lt;other hints&gt;, TRANSITIVE_CLOSURE/NO_TRANSITIVE hint, NO MERGE hint, then the processing is ambiguous.

Therefore, if these hints are used together with MERGE hint, and "hint_error" property is set to *on* it is treated as a validation error. If "hint_error" property is set to *off*, the firstly specified hint is applied.

The following is an example of applying simple view merging by using MERGE hint.

• Type 1: If MERGE hint is specified in a single view, then a simple view merging is performed for v1.

```
SELECT /*+ MERGE(v1) */ *
  FROM ( SELECT * FROM t1 ) v1;
```

• Type 2: If MERGE hint is specified in multiple views, then a simple view merging is performed for   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;v1 and v2, but it is not applied to v3.

```
SELECT /*+ MERGE(v1) MERGE(v2) NO_MERGE(v3) */ *
  FROM ( SELECT i1 FROM t1 ) v1, 
       ( SELECT i1 FROM t2 ) v2,     
       ( SELECT i1 FROM t3 ) v3
 WHERE v1.i1 = v2.i1 AND v2.i1 = v3.i1;
```

• Type 3: If the simple view merging is performed when the hint is specified together with <join   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;order hints>, then the application order and direction between t3 and t4 is ambiguous.   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Therefore, the firstly specified hint is applied only, and the simple view merging is not   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;performed.

```
SELECT /*+ ORDERING( t1, t2, v1 RIGHT ) MERGE(v1) */ *
  FROM t1, 
       t2,
       ( SELECT * FROM t3, t4 WHERE t3.i1 = t4.i1 ) v1
 WHERE t1.i1 = t2.i1 AND t2.i1 = v1.i1;
→
```

• Type 4: If the simple view merging is performed when the hint is specified together with <join   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;operation hints>, then the view which is a target of hashing disappears. Therefore, the firstly   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;specified hint is applied only, and the simple view merging is not performed.

```
SELECT /*+ USE_HASH(v1) MERGE(v1) */ *
  FROM t1, 
       t2,
       ( SELECT * FROM t3, t4 WHERE t3.i1 = t4.i1 ) v1
 WHERE t1.i1 = t2.i1 AND t2.i1 = v1.i1;
```

• Type 5: If the simple view merging is performed when the hint is specified together with <other   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hints>, then other hints between the view and the superordinate query conflicts. Therefore,   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the firstly specified hint is applied only, and the simple view merging is not performed.

```
SELECT /*+ PUSH_PRED MERGE(v1) */ *
  FROM ( SELECT /*+ NO_PUSH_PRED */ * FROM t1 WHERE t1.i1 = 1 ) v1
 WHERE v1.i1 = 1;
```

• Type 6: If the simple view merging is performed when the hint is specified together with TRANSITIV  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;E CLOSUE hint, then other hints between the view and the superordinate query conflicts.   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Therefore, the firstly specified hint is applied only, and the simple view merging is not   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;performed.

```
SELECT /*+ TRANSITIVE_CLOSURE MERGE(v1) */ *
  FROM ( SELECT /*+ NO_TRANSITIVE_CLOSURE */ * 
           FROM t1, t2, t3
          WHERE t1.i1 = t2.i1 AND t2.i1 = t3.i1 ) v1;
```

<a id="2a5cdf14be0dec53"></a>
###### **NO_MERGE**

It instructs an optimizer not to apply a simple view merging to the specified view even when it is possible. This hint should be specified in superordinate query block which includes the specified view.

If NO_MERGE hint is used together with &lt;join order hints&gt;, &lt;join operation hints&gt;, &lt;other hints&gt;, TRANSITIVE_CLOSURE/NO_TRANSITIVE hint, MERGE hint, then the processing is ambiguous.

Therefore, if these hints are used together with NO_MERGE hint, and "hint_error" property is set to *on* it is treated as a validation error. If "hint_error" property is set to *off*, the firstly specified hint is applied.

The following is an example of not applying simple view merging by using NO_MERGE hint.

• Type 1: If NO_MERGE hint is specified in a single view, then a simple view merging is not performed for v1.

```
SELECT /*+ NO_MERGE(v1) */ *
  FROM ( SELECT * FROM t1 ) v1;
```

• Type 2: If NO_MERGE hint is specified in multiple views, then a simple view merging is performed   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for v1 and v2, but it is not applied to v3.

```
SELECT /*+ MERGE(v1) MERGE(v2) NO_MERGE(v3) */ *
  FROM ( SELECT i1 FROM t1 ) v1, 
       ( SELECT i1 FROM t2 ) v2,     
       ( SELECT i1 FROM t3 ) v3
 WHERE v1.i1 = v2.i1 AND v2.i1 = v3.i1;
```

<a id="257be93d818e89ae"></a>
###### **NO_QUERY_TRANSFORMATION**

It instructs an optimizer not to change anything for a query. This hint does not perform the process of which a heuristic optimizer and cost based optimizer changes the query for the best performance.

NO_QUERY_TRANSFORMATION hint can be specified in the top-level query and subquery, and it is applied to the specified query and all its subordinate subqueries.

The following is an example of preventing a query being changed by using NO_QUERY_TRANSFORMATION.

• Type 1: NO_QUERY_TRANSFORMATION hint is used in the subquery.                          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Only the query in the subquery is not changed.)

```
SELECT *
  FROM T1
 WHERE I1 IN ( SELECT /*+ NO_QUERY_TRANSFORMATION */ I1
                 FROM T2 );
```

• Type 2: NO_QUERY_TRANSFORMATION hint is used in the top-level query.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(All queries in the top-level query and its subquery are not changed.)

```
SELECT /*+ NO_QUERY_TRANSFORMATION */ *
  FROM T1
 WHERE I1 IN ( SELECT I1
                 FROM T2 );
```

• Type 3: NO_QUERY_TRANSFORMATION hint is used in the top-level query, and the UNNEST   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hint is used in the subquery.   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The UNNEST hint for the subquery is ignored.)

```
SELECT /*+ NO_QUERY_TRANSFORMATION */ *
  FROM T1
 WHERE I1 IN ( SELECT /*+ UNNEST */ I1
                 FROM T2 );
```

<a id="9d1b59522265171b"></a>
##### &lt;other_hints&gt;

<a id="94ee6c7ad33ee6be"></a>
###### **PUSH_PRED**

It instructs an optimizer to push filters which are applicable to a single table. The hint pushes filters of the select statement to a single table to which the filters are applicable, then preprocess it.  
The hint can be respectively specified to subqueries starting with SELECT, and it is applied only within a block of each query, but it is not spreaded to a subordinate subquery.

The hint can be independently specified in each subqueries.   
If it is not specified, the default value is applied. The default value is PUSH_PRED.

The following is an example of pushing a subquery by using PUSH_PRED hint.

• It pushes T1.i1 = 1 to table T1.

```
SELECT /*+ PUSH_PRED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 = 1;
```

<a id="3e3905d2abc459c6"></a>
###### **NO_PUSH_PRED**

It instructs an optimizer not to push filters which are applicable to a single table. The hint prevents pushing filters of the select statement to a single table to which the filters are applicable, so that it is not to be preprocessed.  
The hint can be respectively specified to subqueries starting with SELECT, and it is applied only within a block of each query, but it is not spreaded to a subordinate subquery.

The hint can be independently specified in each subqueries.   
If it is not specified, the default value is applied. The default value is PUSH_PRED.

If the hint is specified, and a join exists in a from statement, then it is processed at the lowest join among joins which can process the filter. In other words, it prevents preprocessing in a single table which can processes the filter.   
If the hint is specified, and a view exists in the from statement, then the filter is not pushed to the low-level of the view.

The following is an example of pushing a filter by using NO_PUSH_PRED hint.

• Type 1: It performs T1.i1 = 1 after joining T1 and T2.

```
SELECT /*+ NO_PUSH_PRED */ *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 = 1;
```

• Type 2: It performs A.i1 = 1 after processing view A.

```
SELECT /*+ NO_PUSH_PRED */ *
  FROM (SELECT I1 FROM T1) AS A
 WHERE A.I1 = 1;
```

<a id="2bc672c6e8afa043"></a>
###### **PUSH_SUBQ**

It instructs an optimizer to push a subquery to the lowest applicable node. When the upper level query of the subquery consists of join, this hint scans a structure of the join nodes, from the top to the bottom, to find a node which can process the subquery. Then it processes the subquery from the lowest node which can push the subquery.

PUSH_SUBQ hint can be specified only in the subquery. When multiple subqueries exist, PUSH_SUBQ hint should be respectively specified in each subquery.

If the PUSH_SUBQ hint is not specified, the optimizer calculates the cost and pushes the subquery to the node of the best cost.

The following is an example of pushing a subquery by using PUSH_SUBQ hint.

• Type 1: A subquery is pushed to the table T1.

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ PUSH_SUBQ */ I1
                    FROM T3 );
```

• Type 2: The subquery can be processed only in the top node.      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(The subquery can not be pushed to the subordinate node.)

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ PUSH_SUBQ */ I1
                    FROM T3
                   WHERE T3.I2 = T1.I2
                     AND T3.I3 = T2.I3 );
```

<a id="4064a25f2d652386"></a>
###### **NO_PUSH_SUBQ**

It instructs the optimizer not to push the subquery to a subordinate node. When a superordinate query of the subquery consists of join, this hint processes the subquery at the top node of the join node.

NO_PUSH_SUBQ hint can be specified only in the subquery. When multiple subqueries exist, NO_PUSH_SUBQ hint should be respectively specified in each subquery.

If NO_PUSH_SUBQ hint is not specified, the optimizer calculates the cost and pushes the subquery to the node of the best cost.

The following is an example of pushing a subquery by using NO_PUSH_SUBQ hint.

• NO_PUSH_SUBQ hint is used for the subquery which can be processed in the table T1.      
&nbsp;&nbsp;(After joining the tables T1 and T2, the subquery is processed.)

```
SELECT *
  FROM T1, T2
 WHERE T1.I1 = T2.I1
   AND T1.I1 IN ( SELECT /*+ NO_PUSH_SUBQ */ I1
                    FROM T3 );
```

<a id="c7cee1e16e9bfa61"></a>
###### **USE_GROUP_HASH**

When group by clause exists, it instructs an optimizer to use a hash instant for grouping.

USE_GROUP_HASH hint can be specified only in group by clause. When multiple subqueries exist, USE_GROUP_HASH hint should be respectively specified in each subquery.

If USE_GROUP_HASH hint is not used and group keys for grouping are sorted from a subordinate node, a method using the group node is considered.

The following is an example of using USE_GROUP_HASH hint.

• USE_GROUP_HASH is used when the index consisting of group keys in the table T1 exists.

```
SELECT /*+ USE_GROUP_HASH */ *
  FROM T1
 GROUP BY I1;
```

<a id="379dcb081b8fc5f7"></a>
###### **USE_DISTINCT_HASH**

When distinct clause exist, it instructs an optimizer to use a hash instant to perform distinct.

USE_DISTINCT_HASH hint can be specified only in a statement with distinct clause. When multiple subqueries exist, USE_DISTINCT_HASH hint should be respectively specified in each subquery.

If USE_DISTINCT_HASH hint is not used and distinct keys are sorted from a subordinate node, a method using the group node is considered.

The following is an example of using USE_DISTINCT_HASH hint.

• USE_DISTINCT_HASH is used when the index consisting of distinct keys is in the table T1 exists.

```
SELECT /*+ USE_DISTINCT_HASH */ I1, I2
  FROM T1;
```

<a id="ec3f48f3faca8372"></a>
#### Description

A hint is a comment which a user directly instructs how to perform an SQL statement to the GOLDILOCKS optimizer. When GOLDILOCKS optimizer does not determine an appropriate execution plan, the user can select the execution plan using the hint.

The GOLDILOCKS optimizer preferentially selects the user defined hints to determine an execution plan. If the user defined hint is not available, the GOLDILOCKS optimizer determines the execution plan.

GOLDILOCKS optimizer operates based on the user defined hint as possible when the user uses a hint. Therefore, it is recommended to use the hint only when it is determined that the execution plan of GOLDILOCKS optimizer is wrong while the user performs the SQL statement.

Especially, GOLDILOCKS optimizer performs the execution plan according to the user defined hint when repeatedly using the same SQL statement by a hint. Therefore, be cautious that the table or view included in the SQL statement is updated, and the performance of another execution plan may be degraded.

In GOLDILOCKS, the hint can be used in SELECT, INSERT SELECT, DELETE, UPDATE statements. The hint can be specified after the keyword of each statement and it is specified between the keywords '/ * + ' and '* / '.

If a wrong hint is specified, or if hints conflict because two or more hints for the same execution plan are specified, the hint is ignored or the first hint is applied. To check if the hint is wrong, use the hint after setting HINT_ERROR property to *on* by using ALTER statement.

<a id="c05905440d3a8b57"></a>
#### Examples

The following is an example of using &lt;hint clause&gt; in INSERT SELECT, DELETE, UPDATE, SELECT statements.

• It is used in INSERT SELECT statement.

```
gSQL> INSERT INTO T1 SELECT /*+ INDEX(T1, T1_IDX) */ * FROM T1;

1 row created.
```

• It is used in SELECT statement.

```
gSQL> SELECT /*+ INDEX(T1, T1_IDX) */ * FROM T1;

I1
--
 1
 1

2 rows selected.
```

• It is used in UPDATE statement.

```
gSQL> UPDATE /*+ INDEX(T1, T1_IDX) */ T1 SET I1 = 2;

2 rows updated.
```

• It is used in DELETE statement.

```
gSQL> DELETE /*+ INDEX(T1, T1_IDX) */ T1 WHERE I1 = 2;

2 rows deleted.
```

The following is an example of using a wrong hint when HINT_ERROR property is set to *on* by using ALTER statement.

```
gSQL> ALTER SESSION SET HINT_ERROR = ON;

Session altered.

gSQL> SELECT /*+ INDEX(T2, T1_IDX) */ * FROM T1;

ERR-42000(16058): not applicable hint :
SELECT /*+ INDEX(T2, T1_IDX) */ * FROM T1
           *
ERROR at line 1:
```

<a id="352fb45a262aec31"></a>
#### Compatibility

The SQL standard does not define a hint, and the other vendors, such as Oracle support a hint in their own forms.

Most hints of GOLDILOCKS are compatible with hints of Oracle, and the hints of GOLDILOCKS which are as same as the hints of Oracle are operated in Oracle in the same way. However, Oracle has a different meaning for the INDEX_COMBINE hint, and Oracle does not support the ORDERING hint.

<a id="18f4c8bbd6e59b25"></a>
#### For More Information

Refer to [query specification](#3ec5b3395d1f51b6).

<a id="f7fb3657b7896855"></a>
## SELECT .. FOR UPDATE

<a id="8623596064f8f232"></a>
### Function

It sets whether or not to update the result set of SELECT statement.

<a id="cdb0581717bb14ef"></a>
### Syntax

```
<select for update statement> ::=
    <query expression>  <updatability clause>
    ;

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="00ce591e97eca9ec"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;select for update statement&gt;.

- One of the following privileges for all tables used in the statement is required for a user to perform &lt;query expression&gt;.
    - SELECT(columns) ON TABLE for all columns used in the statement among the table columns
    - (SELECT or CONTROL TABLE) ON TABLE for that table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

- If FOR UPDATE clause is used, one of the following privileges for the tables to be locked is required.
    - (LOCK or CONTROL TABLE) ON TABLE for that table
    - (LOCK TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - LOCK ANY TABLE ON DATABASE

<a id="fb6dd926c571926f"></a>
### Syntax Rules and Parameters

<a id="7d8e568d4b81d1ca"></a>
#### &lt;query expression&gt;

INTO clause should not exist in SELECT statement.

To use FOR UPDATE, the query should identify the row updates of the base table, or it should be an updatable query which can acquire the lock into the row.

The updatable query should satisfy all of following conditions.

- DISTINCT should not exist in the top-level query. 
    - (X) SELECT DISTINCT * FROM t1; 
- GROUP BY, HAVING, aggregation function should not exist in the top-level query. 
    - (X) SELECT MAX(c1) FROM t1; 
- Set operators should not exist. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- There should be at least one updatable column in the table listed in FROM clause. 
    - The column of the table which is not for cross join among the tables included in join is not an updatable column.
        - OUTER JOIN is not the cross join. 
        - NATURAL JOIN is not the cross join. 
        - If USING clause is is used in INNER JOIN, it is not the cross join. 
    - The column of the following tables is not an updatable column.
        - Dictionary table, fixed table, performance view 
    - The column of a view is not an updatable table.

For more information about SELECT statement, refer to [query expression](#1d9bd840c91d26e4).

<a id="8c67579ddaab0aa9"></a>
#### &lt;updatability clause&gt;

It specifies whether or not to update the row for the result set.

- FOR READ ONLY 
    - The read-only query is declared.
- FOR UPDATE 
    - The writable query is declared. 
    - x lock is acquired for the rows until the end of the transaction to prevent other transactions from updating the rows when executing the query.
    - &lt;query expression&gt; should be an updatable query.

<a id="21bec0f848a4a610"></a>
#### FOR UPDATE OF …

It lists the columns relating to acquiring lock when executing the query.

- The column listed in FOR UPDATE OF statement. 
    - It should be updatable columns of the table listed in the FROM clause of &lt;query expression&gt;.
    - It acquires a lock for the table of the listed column.
- Only FOR UPDATE is used 
    - It means the same as listing all updatable columns of the table in FROM clause of &lt;query expression&gt;.
    - It acquires a lock for the table of all columns.

<a id="197e8a95c2f7db24"></a>
#### &lt;lock wait mode&gt;

It is used together with FOR UPDATE statement, and it specifies the lock acquisition method.

- WAIT 
    - It acquires a lock for all rows of the query result before obtaining the query result.
    - It waits until acquiring a lock.
- WAIT second 
    - It acquires a lock for all rows of the query result before acquiring the query result.
    - If the lock is not acquired for a specified time, an error occurs.
    - The wait time is in seconds and it can use the value between 0 and 1,000,000,000.
- NOWAIT 
    - It acquires a lock for all rows of the query result before acquiring the query result.
    - If the lock is not immediately acquired, an error occurs.
- If it is not specified, the default value is WAIT.

<a id="9826679040edcb38"></a>
### Description

SELECT statement keep fetching the rows regardless of whether the transaction ends. However, SELECT .. FOR UPDATE statement can not fetch the rows when the transaction ends because the statement acquires the lock for the rows.

> Cursor holdability  
> 
> 
> - WITH HOLD
>     - It can keep fetching regardless of whether the transaction ends. 
>     - It is also known as fetch across commit.
> 
> 
> 
> - WITHOUT HOLD
>     - When the transaction ends, it can not fetch.
> 

<a id="7b9c752d4b924860"></a>
### Examples

The following is an example of acquiring a lock for the row by using FOR UPDATE statement.

```
gSQL> SELECT id, data FROM t1 WHERE id = 3 FOR UPDATE;

ID DATA  
-- ------
 3 data_3

1 row selected.
```

The following uses join and ORDER BY clause but it is an updatable query, so FOR UPDATE statement can be used.

```
gSQL> SELECT t1.id, t1.name, t2.addr 
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    
 2 anyone  anywhere     
 3 unknown N/A          
 4 leekmo  leekmo's home
 5 mkkim   seoul        

5 rows selected.
```

The following is a non-updatable query, so FOR UPDATE statement can not be used.

```
gSQL> SELECT id, COUNT(*)
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="5aea41a4ef56839a"></a>
### Compatibility

In the SQL standard, &lt;select for update statement&gt; is not defined, but it can be defined by using [DECLARE cursor_name](#9826eadcd321de1b) statement.

<a id="3a7d31ba115517c4"></a>
## SELECT .. INTO

<a id="c1136c17d2c815b2"></a>
### Function

It retrieves a single row by using a query, then obtains the value of retrieved row into the host variable.

<a id="0418914a2b8a3f2d"></a>
### Syntax

```
<select statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>
    ;

<select target list> ::=
    variable_name [, ...]
```

<a id="13022f859c7c3cef"></a>
### Invocation and Access Rules

One of the following privileges for all tables used in the statement is required for a user to perform &lt;select statement: single row&gt;.

- SELECT(columns) ON TABLE for all columns used in the statement among the table columns
- (SELECT or CONTROL TABLE) ON TABLE for that table
- (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- SELECT ANY TABLE ON DATABASE

<a id="b69a57a6fcf66de9"></a>
### Syntax Rules and Parameters

<a id="6cc4f3454c58ccc1"></a>
#### &lt;hint clause&gt;

It specifies hints for query execution.  
For more information, refer to [hint clause](#ad0ef76d32e7f521) of [SELECT](#1117040fd802dbd4) statement.

<a id="7167e4e53555961c"></a>
#### &lt;set quantifier&gt;

It specifies whether to remove duplicates from the query result.  
For more information, refer to [query specification](#3ec5b3395d1f51b6) clause.

<a id="8aabbd11e4483f02"></a>
#### &lt;select list&gt;

It specifies the columns to be retrieved from the query result.  
For more information, refer to [select list](#bd334f359dc73b47) clause.

<a id="4e03535b78232123"></a>
#### INTO &lt;select target list&gt;

The number of the variable specified in INTO clause should be equal to the number of the expression specified in &lt;select list&gt;.

<a id="634997eba5346c03"></a>
#### &lt;table expression&gt;

It specifies the query information such as a search condition.  
For more information, refer to [query specification](#3ec5b3395d1f51b6) clause.

<a id="265e1b074d12df7f"></a>
### Description

The rows to be retrieved should be one or less.  
If two or more rows are retrieved, an error occurs.

<a id="ad76bebf47ea95d3"></a>
#### Differences among SELECT-related Statements

- &lt;select statement&gt;
    - It retrieves multiple rows which satisfy the condition, and the retrieved rows can be retrieved by using API such as SQLFetch ().
    - e.g. SELECT c1 FROM t1 WHERE c1 > 0; 
- &lt;select statement: single row&gt;
    - It can retrieve one or less row which satisfies the condition, then obtains the value into the host variable in INTO clause when the retrieved row is a single row. 
    - e.g. SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0;

<a id="2c112ed1c6da1d9f"></a>
### Example

The following is an example of obtaining the value into the host variable by using interactive SQL (gsql).

```
gSQL> \var v_id   INTEGER
gSLQ> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

<a id="5ef29f0c327f68ca"></a>
## SELECT .. INTO .. FOR UPDATE

<a id="f34f677a4b4248bd"></a>
### Function

It sets whether to update the row by retrieving a single row through the query, then obtains the value of retrieved row into the host variable.

<a id="531ad5cc177e6feb"></a>
### Syntax

```
<select for update statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>  <updatability clause>
    ;

<select target list> ::=
    variable_name [, ...]

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="eee8b383391b1e19"></a>
### Invocation and Access Rules

One of the following privileges for all tables used in the statement is required for a user to perform &lt;select statement: single row&gt;.

- SELECT(columns) ON TABLE for all columns used in the statement among the table columns
- (SELECT or CONTROL TABLE) ON TABLE for that table
- (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- SELECT ANY TABLE ON DATABASE

If FOR UPDATE clause is used, one of the following privileges for the tables to be locked is required.

- (LOCK or CONTROL TABLE) ON TABLE for that table
- (LOCK TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- LOCK ANY TABLE ON DATABASE

<a id="e6013e393cbd3af4"></a>
### Syntax Rules and Parameters

<a id="effc497b583d1ac1"></a>
#### &lt;select for update statement: single row&gt;

To use FOR UPDATE, the query should identify the row updates of the base table, or it should be an updatable query which can acquire the lock into the row.

The updatable query should satisfy all of following conditions.

- DISTINCT should not exist in the top-level query. 
    - (X) SELECT DISTINCT * FROM t1; 
- GROUP BY, HAVING, aggregation function should not exist in the top-level query. 
    - (X) SELECT MAX(c1) FROM t1; 
- Set operators should not exist. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- There should be at least one updatable column in the table listed in FROM clause. 
    - The column of the table which is not for cross join among the tables included in join is not an updatable column.
        - FULL OUTER JOIN is not the cross join. 
        - NATURAL JOIN is not the cross join. 
        - If USING clause is is used in INNER JOIN, it is not the cross join. 
    - The column of the following tables is not an updatable column.
        - Dictionary table, fixed table, performance view 
    - The column of a view is not an updatable table.

<a id="9f748a44b66f3cbb"></a>
#### &lt;updatability clause&gt;

It specifies whether or not to update the row for the result set.

- FOR READ ONLY 
    - The read-only query is declared.
- FOR UPDATE 
    - The writable query is declared. 
    - x lock is acquired for the rows until the end of the transaction to prevent other transactions from updating the rows when executing the query.
    - &lt;query expression&gt; should be an updatable query.

<a id="9840ac033d808b3c"></a>
#### FOR UPDATE OF …

It lists the columns relating to acquiring lock when executing the query.

- The column listed in FOR UPDATE OF statement. 
    - It should be updatable columns of the table listed in the FROM clause of &lt;query expression&gt;.
    - It acquires a lock for the table of the listed column.
- Only FOR UPDATE is used 
    - It means the same as listing all updatable columns of the table in FROM clause of &lt;query expression&gt;.
    - It acquires a lock for the table of all columns.

<a id="ea4e1d60bd0e8af8"></a>
#### &lt;lock wait mode&gt;

It is used together with FOR UPDATE statement, and it specifies the lock acquisition method.

- WAIT 
    - It acquires a lock for all rows of the query result before obtaining the query result.
    - It waits until acquiring a lock.
- WAIT second 
    - It acquires a lock for all rows of the query result before acquiring the query result.
    - If the lock is not acquired for a specified time, an error occurs.
    - The wait time is in seconds and it can use the value between 0 and 1,000,000,000.
- NOWAIT 
    - It acquires a lock for all rows of the query result before acquiring the query result.
    - If the lock is not immediately acquired, an error occurs.
- If it is not specified, the default value is WAIT.

<a id="029e9d8cb22d8b3a"></a>
#### &lt;hint clause&gt;

It specifies hints for query execution.  
For more information, refer to [hint clause](#ad0ef76d32e7f521) of [SELECT](#1117040fd802dbd4) statement.

<a id="1aae77b9f0dcd397"></a>
#### &lt;set quantifier&gt;

It specifies whether to remove duplicates from the query result.  
For more information, refer to [query specification](#3ec5b3395d1f51b6) clause.

<a id="0759060e46eee7cd"></a>
#### &lt;select list&gt;

It specifies the columns to be retrieved from the query result.  
For more information, refer to [select list](#bd334f359dc73b47) clause.

<a id="8be4d0ab3cf4b747"></a>
#### INTO &lt;select target list&gt;

The number of the variable specified in INTO clause should be equal to the number of the expression specified in &lt;select list&gt;.

<a id="88cd1f567de2add6"></a>
#### &lt;table expression&gt;

It specifies the query information such as a search condition.  
For more information, refer to [query specification](#3ec5b3395d1f51b6) clause.

<a id="9ef9add39cca68f6"></a>
### Description

The rows to be retrieved should be one or less.  
If two or more rows are retrieved, an error occurs.

SELECT statement keep fetching the rows regardless of whether the transaction ends. However, SELECT .. FOR UPDATE statement can not fetch the rows when the transaction ends because the statement acquires the lock for the rows.

> Cursor holdability  
>   
> • WITH HOLD  
> ° It can keep fetching regardless of whether the transaction ends.   
> ° It is also known as fetch across commit.  
>   
>  • WITHOUT HOLD  
> ° When the transaction ends, it can not fetch.

<a id="e9d74142b21e7d6c"></a>
#### Differences among SELECT-related Statements

- &lt;select for update statement&gt;
    - It retrieves multiple rows which satisfy the condition, sets whether to update them and the retrieved rows can be retrieved by using API such as SQLFetch ().
    - e.g. SELECT c1 FROM t1 WHERE c1 > 0 FOR UPDATE; 
- &lt;select for update statement: single row&gt;
    - It can retrieve one or less row which satisfies the condition, sets whether to update them then obtains the value into the host variable in INTO clause when the retrieved row is a single row. 
    - e.g. SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0 FOR UPDATE;

<a id="caaf8bc560f6c04a"></a>
### Examples

The following is an example of acquiring a lock for the row by using FOR UPDATE statement, and obtaining the value into the host variable by using interactive SQL (gsql).

```
gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3 FOR UPDATE;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

The following uses join and ORDER BY clause but it is an updatable query, so FOR UPDATE statement can be used.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_name VARCHAR(128)
gSQL> \var v_addr VARCHAR(128)


gSQL> SELECT t1.id, t1.name, t2.addr 
        INTO :v_id, :v_name, :v_addr
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
       LIMIT 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    

1 row selected.
```

The following is a non-updatable query, so FOR UPDATE statement can not be used.

```
gSQL> \var v_id    INTEGER
gSQL> \var v_count INTEGER

gSQL> SELECT id, COUNT(*)
        INTO :v_id, :v_count
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="0b7ea47ed9dec395"></a>
### For More Information

Refer to the followings.

- [SELECT .. FOR UPDATE](#f7fb3657b7896855)
- [SELECT .. INTO](#3a7d31ba115517c4)

<a id="8337ae2c011b78f5"></a>
## SET CONSTRAINTS

<a id="ef33e9471f1af627"></a>
### Function

It sets the check point of deferrable constraint in a transaction to IMMEDIATE or DEFERRED.

<a id="79b7a239a6424b3d"></a>
### Syntax

```
<set constraints mode statement> ::=
    SET { CONSTRAINT | CONSTRAINTS } <constraint name list> { DEFERRED | IMMEDIATE }
    ;

<constraint name list> ::=
      ALL
    | <constraint name> [, ...]
```

<a id="b71624c925e73541"></a>
### Invocation and Access Rules

Any separate access privilege is not required for a user to perform SET CONSTRAINTS.

> It is not supported in the cluster system.

<a id="609e16f454a619e2"></a>
### Syntax Rules and Parameters

<a id="ad9cec4904f494a8"></a>
#### CONSTRAINT | CONSTRAINTS

CONSTRAINT and CONSTRAINTS are the keywords of the same meaning, and the SQL standard uses CONSTRAINTS.

<a id="dbb9f7f0ca3e1a5d"></a>
#### &lt;constraint name list&gt;

It specifies the list of constraint names, or specifies ALL to set all deferrable constraints.  
When specifying &lt;constraint name&gt;, it should be the name of the deferrable constraint.  
ALL means all deferrable constraints.

<a id="a87f52988ca75e45"></a>
#### DEFERRED | IMMEDIATE

It sets the check point of specified deferrable constraints.

- IMMEDIATE
    - It checks the specified constraints when executing the DML statement. 
    - If the transaction violates the constraints, then an error occurs.
- DEFERRED
    - It checks the specified constraints when the transaction is committed.

If the transaction is in progress, the check point of the constraint is set in the current transaction. If the transaction is not in progress, it is set in the next transaction.  
After the transaction ends, it does not affect the next transaction.

<a id="fd573fcad61ca135"></a>
### Description

<a id="be155beef59a1c89"></a>
#### Deferrable Constraint

DEFERRABLE constraint can change its check point.  
The following is an example of creating a table with a deferrable constraint, and inserting data to the table.

```
gSQL> CREATE TABLE t1 
( 
    id   INTEGER, 
    name VARCHAR(128) CONSTRAINT t1_uk UNIQUE 
                      DEFERRABLE INITIALLY IMMEDIATE
);

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' );

1 row created.

gSQL> COMMIT;

Commit complete.
```

In the example above, UNIQUE constraint which is deferrable is created on a name column, and the initial check point is set as INITIALLY IMMEDIATE. Therefore, the constraint is checked whenever DML statement is executed.

In this case, if the user tries to exchange the name value of two rows as follows, it violates the constraint because the check point is IMMEDIATE.

```
gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated
```

If the check point is changed to DEFERRED as follows, the operation as same as above succeeds because the constraint is checked when the transaction is committed.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

1 row updated.

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

1 row updated.

gSQL> COMMIT;

Commit complete.
```

If the check point is set to DEFERRED, then the constraint is checked when the transaction is committed. Therefore, if the transaction is committed when the constraint is violated, then the transaction fails and it is rolled back as follows.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> COMMIT;

ERR-40002(16291): transaction rollback: integrity constraint violation : PUBLIC.T1_UK(1)
```

<a id="23ab3760e3bb5ce4"></a>
#### Violation of a Deferred Constraint

Executing the following statements when the transaction violates the constraints set to DEFFFERED, then an error occurs as follows.

- COMMIT
    - An error occurs and the transaction is rolled back.
- SET CONSTRAINTS ALL IMMEDIATE
    - An syntax error occurs. 
- DDL
    - An syntax error occurs.

An unexpected ROLLBACK can occur when COMMIT, it is necessary to ensure whether the transaction violates the constraint by using SET CONSTRAINTS ALL IMMEDIATE statement.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

ERR-23000(16038): integrity constraint violation : PUBLIC.T1_UK(1)

gSQL> SELECT * FROM t1 ORDER BY id;

ID NAME  
-- ------
 1 mkkim 
 2 leekmo
 3 leekmo

3 rows selected.

gSQL> UPDATE t1 SET name = 'xcom73' WHERE id = 3;

1 row updated.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.

gSQL> COMMIT;

Commit complete.
```

<a id="de9c48cb612a1fde"></a>
#### Transaction Control Language

SET CONSTRAINTS statement is a transaction control language which is used when the transaction is in progress such as [SAVEPOINT savepoint_specifier](#bf9e53dc119286d7).  
The transaction control such as COMMIT, ROLLBACK, ROLLBACK TO SAVEPOINT statement is applied to SET CONSTRAINTS statement.

The following is an example of a table with multiple deferrable constraints.

```
CREATE TABLE t1
(
   id1 INTEGER CONSTRAINT t1_uk1 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id2 INTEGER CONSTRAINT t1_uk2 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id3 INTEGER CONSTRAINT t1_uk3 UNIQUE DEFERRABLE INITIALLY IMMEDIATE
);
```

If &lt;set constraints mode statement&gt; statement is performed when the transaction is in progress, the check point of deferrable constraints is changed depending on each point as follows.

- result: success

```
INSERT INTO t1 VALUES ( 1, 1, 1 );

1 row created.

COMMIT;

Commit complete.
```

- result: success

```
SAVEPOINT sp1;

Savepoint created.
```

- result: success
- t1_uk1 constraint is DEFERRED

```
SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp2;

Savepoint created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
SET CONSTRAINTS t1_uk2 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp3;

Savepoint created.
```

- result: success
- ALL constraints are DEFERRED

```
SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp4;

Savepoint created.
```

- result: success
- ALL constraints are IMMEDIATE

```
SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.
```

When the transaction is partially rolled back by using ROLLBACK TO SAVEPOINT statement as follows, SET CONSTRAINTS statement is also partially rolled back and the check point is changed.

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp4;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

1 row created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp3;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1 constraint is DEFERRED

```
ROLLBACK TO SAVEPOINT sp2;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- all constraint are IMMEDIATE

```
ROLLBACK TO SAVEPOINT sp1;

Rollback complete.
```

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: 1 row
- 1 1 1

```
SELECT * FROM t1;

ID1 ID2 ID3
--- --- ---
  1   1   1

1 row selected.
```

When the transaction is committed or rolled back, the effects of SET CONSTRAINTS statement is also terminated, and all deferrable constraints follows the constraints property which is INITIALLY IMMEDIATE or INITIALLY DEFERRED value.

<a id="77cac31c8819a783"></a>
### Examples

The following is an example of changing the check point by specifying the constraint name.

```
gSQL> SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

The following is an example of changing the check point of all deferrable constraints.

```
gSQL> SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

<a id="46199f56e55b3c49"></a>
### Compatibility

The SQL standard does not define CONSTRAINT keyword clause.

**SQL standard compatibility**

<a id="295f9256fc77a78a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F721 | Deferrable constraints | O |

<a id="96818ea83d624c76"></a>
### For More Information

Refer to the followings.

- Adding constraints
    - [CREATE TABLE](#72507f5467c281c9)
    - [ALTER TABLE name ADD CONSTRAINT](#65400a8940d0436c)
    - [ALTER TABLE name ADD COLUMN](#d350cd62e4767b16)
    - [ALTER TABLE name ALTER COLUMN](#6df8140b35bd2d2b)

- Altering constraints: [ALTER TABLE name ALTER CONSTRAINT](#dbba103b11769053)

- Controlling the check point of constraints: [SET CONSTRAINTS](#8337ae2c011b78f5)

<a id="271bb49251e35732"></a>
## SET SESSION AUTHORIZATION user_identifier

<a id="00c1e3537e5433c7"></a>
### Function

It sets the session user and current user.

<a id="7d7d09ede0d9f813"></a>
### Syntax

```
<set session user identifier statement> ::=
    SET SESSION AUTHORIZATION user_identifier
    ;
```

<a id="fb7a57f1c4a8e8f7"></a>
### Invocation and Access Rules

ACCESS CONTROL ON DATABASE privilege is required for a logon user to perform &lt;set session user identifier statement&gt;.

The user information is managed in three types as follows.

- Logon user
    - It is a user who performed login, and it is maintained until the connection is closed.
- Session user
    - It is as same as the first logon user, but it can be changed using the SET SESSION AUTHORIZATION statement.
- Current user
    - It is generally as same as the session user, but it is temporarily changed internally in system to control access when using the PSM or view.
    - The session user and current user is similar to the difference between the unix system's real user and the effective user.

<a id="c1627f3311f40e12"></a>
### Syntax Rules and Parameters

<a id="5631ad8ab7238f8f"></a>
#### user_identifier

It is the username to be altered.

<a id="bf8e3be93fbafc63"></a>
### Description

After performing SET SESSION AUTHORIZATION statement, all statements is performed based on the session user. Therefore, the privilege for the session user is checked and the owner of when creating objects also is the session user.

<a id="0f3642da99742990"></a>
### Example

The following is an example that the user test with ACCESS CONTROL ON DATABASE privilege sets the user u1 to the session user.

```
gSQL> SET SESSION AUTHORIZATION u1;

Session set.

gSQL> SELECT LOGON_USER(), SESSION_USER(), CURRENT_USER FROM dual;

LOGON_USER() SESSION_USER() CURRENT_USER
------------ -------------- ------------
TEST         U1             U1          

1 row selected.
```

<a id="892b9b0b0971610d"></a>
### Compatibility

**SQL standard compatibility**

<a id="c7f96130f53c9f1a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F321 | User authorization | O |

<a id="0f518ee0bd0d6a1a"></a>
## SET SESSION CHARACTERISTICS AS transaction_mode

<a id="04313a8e8efc9eb9"></a>
### Function

It sets the transaction property of a session.

<a id="3b4344051c12c4aa"></a>
### Syntax

```
<set session characteristics statement> ::=
    SET SESSION CHARACTERISTICS AS TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="5541c1635311eea5"></a>
### Syntax Rules and Parameters

<a id="267ba320a5d84414"></a>
#### &lt;transaction_access_mode&gt;

It is ACCESS MODE of the following transactions.

- READ ONLY 
- READ WRITE

<a id="c3d0148dd5f3629a"></a>
#### &lt;isolation_level&gt;

It is ISOLATION LEVEL of the following transactions.

- READ COMMITTED 
- SERIALIZABLE

<a id="c582fc61b78e0fbf"></a>
### Description

SET SESSION CHARACTERISTICS sets the transaction property of a session. In other words, properties of all transactions created within the session follows these properties.

However, [SET TRANSACTION transaction_mode](#3ee5dd4ad5b9c02b) statement sets only the property of a single transaction which is performed next.

<a id="a0ba32cdfa521b7f"></a>
### Examples

The following is an example that all transactions to be created within the session are set to READ ONLY.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION READ ONLY;

Session set.
```

The following is an example that the isolation level of all transactions to be created within the session is set to READ COMMITTED.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL READ COMMITTED;

Session set.
```

<a id="967b6e279b3eeabb"></a>
### Compatibility

**SQL standard compatibility**

<a id="1650409dc36e13b1"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F761 | Session management | O |

<a id="2937a7bae3612c87"></a>
### For More Information

Refer to [SET TRANSACTION transaction_mode](#3ee5dd4ad5b9c02b).

<a id="b5ef99e1c983e928"></a>
## SET TIME ZONE

<a id="c7510f88335b7927"></a>
### Function

It sets the TIMEZONE of a session.

<a id="49252cd5a0be2ee1"></a>
### Syntax

```
<set local time zone statement> ::=
    SET TIME ZONE <set time zone value>
    ;

<set time zone value> ::= 
    { '[+|-]hh:mm' | LOCAL }
```

<a id="6091b28e7af7c171"></a>
### Syntax Rules and Parameters

<a id="0a1cc3e476d48eda"></a>
#### &lt;set time zone value&gt;

It is the TIMEZONE value to be set.

- hh:mm: It is a GMT OFFSET of the TIMEZONE to be set.
    - The range of the offset value is '-14:00' ~ '+14:00' .
- LOCAL: It is the TIME ZONE at the time of session creation.
    - TIME ZONE at the time of session creation is set to TIME ZONE of the client OS.

<a id="8a6d589170a249bb"></a>
### Description

Altering the time zone of the session affects the result value of function such as [CURRENT_TIME](11-sql-elements.md#406eee865fb2c767), [CURRENT_TIMESTAMP](11-sql-elements.md#cf40f2352a534e8c).

<a id="39a5b386ac68a405"></a>
### Example

The following is an example of altering the session time zone to '+09: 00'.

```
gSQL> SET TIME ZONE '+09:00';

Session set.
```

<a id="9351dfcc351bbaeb"></a>
### Compatibility

**SQL standard compatibility**

<a id="9b65ea1e180d7d41"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F411 | Time zone specifications | O |

<a id="3ee5dd4ad5b9c02b"></a>
## SET TRANSACTION transaction_mode

<a id="d08cd6bce22c0549"></a>
### Function

It sets the transaction property.

<a id="a2113e403b53a477"></a>
### Syntax

```
<set transaction statement> ::=
    SET TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="03af0eecd5750833"></a>
### Syntax Rules and Parameters

<a id="47302b7af8c04b6a"></a>
#### &lt;transaction_access_mode&gt;

It is ACCESS MODE of the following transactions.

- READ ONLY 
- READ WRITE

<a id="ece7a5ec2bea1897"></a>
#### &lt;isolation_level&gt;

It is ISOLATION LEVEL of the following transactions.

- READ COMMITTED 
- SERIALIZABLE

<a id="41646086888124c3"></a>
### Description

SET TRANSACTION sets property of the next transaction, and the property is reset to the default value after the next transaction ends.

<a id="060060fd8fbe783b"></a>
### Example

The following is an example of setting the next transaction to READ ONLY.

```
gSQL> SET TRANSACTION READ ONLY;

Transaction set.
```

<a id="2179d301cca215ba"></a>
### Compatibility

**SQL standard compatibility**

<a id="6193ae6b72000e2c"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T251 | SET TRANSACTION statement: LOCAL option | X |

<a id="0cf80c03670c24b8"></a>
### For More Information

Refer to [SET SESSION CHARACTERISTICS AS transaction_mode](#0f518ee0bd0d6a1a).

<a id="39eff80c142b3feb"></a>
## TRUNCATE TABLE

<a id="49b56e44aeccf866"></a>
### Function

It truncates all rows from a table.

<a id="32870572e43fcbce"></a>
### Syntax

```
<truncate table statement> ::= 
    TRUNCATE TABLE table_name 
        [ RESTART IDENTITY | CONTINUE IDENTITY ] 
        [ DROP STORAGE | DROP ALL STORAGE ] 
    ;
```

<a id="ede214d31fb54ef2"></a>
### Invocation and Access Rules

One of the following privileges is required for a user to perform &lt;truncate table statement&gt;.

- The owner of that table 
- CONTROL TABLE ON TABLE for the table
- (DROP TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- DROP ANY TABLE ON DATABASE

<a id="46102a338d06a1a1"></a>
### Syntax Rules and Parameters

<a id="ae9c69a2fb0519c0"></a>
#### table_name

It is the name of a target table whose rows are to be truncated.  
It can define schema to which the table belongs such as schema_name.table_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="ddc679358e516e30"></a>
#### [ RESTART IDENTITY | CONTINUE IDENTITY ]

- RESTART IDENTITY 
    - If an identity column which has auto created value in that table exists, it automatically restarts value.
- CONTINUE IDENTITY 
    - If an identity column which has auto created value in that table exists, it does not change the existing value.
- If it is not specified, the default value is CONTINUE IDENTITY.

<a id="38af0af7c64cc754"></a>
#### [ DROP STORAGE | DROP ALL STORAGE ]

- DROP STORAGE 
    - It drops allocated extents from the the table excluding the space of MINSIZE.
- DROP ALL STORAGE 
    - It drops all extents allocated to the table.
- If it is not specified, the default value is DROP STORAGE.

<a id="73208d46acdafe32"></a>
### Description

Data Definition Language (DDL) statement such as TRUNCATE TABLE can be rolled back if it is before when the transaction is committed.

<a id="d5387e7229ebaaf3"></a>
### Examples

The following is an example of performing TRUNCATE TABLE statement.

```
gSQL> TRUNCATE TABLE t1;

Table truncated.
```

The following is an example of restarting the value of the identity column when performing TRUNCATE TABLE.

```
TRUNCATE TABLE t1 RESTART IDENTITY;

Table truncated.
```

<a id="adcb7ce1a2b39ed6"></a>
### Compatibility

The SQL standard does not define [ DROP STORAGE | DROP ALL STORAGE ] clause.

**SQL standard compatibility**

<a id="30210fd69aef85d4"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F200 | TRUNCATE TABLE statement | O |
| F202 | TRUNCATE TABLE: identity column restart option | O |

<a id="607eb6ad25aa2ec3"></a>
## UPDATE

<a id="58b1cb69d858554e"></a>
### Function

It updates rows in a table.

<a id="8419bdcb5a599d1c"></a>
### Syntax

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
    ;

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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

<a id="e7b671ebc5af2cd6"></a>
### Invocation and Access Rules

One of the following privileges is required for a user to perform &lt;update statement: searched&gt;.

- UPDATE(columns) ON TABLE for all columns which are targets to be updated
- (UPDATE or CONTROL TABLE) ON TABLE for the table
- (UPDATE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- UPDATE ANY TABLE ON DATABASE

<a id="cd228d9b1efde796"></a>
### Syntax Rules and Parameters

<a id="6288e80e0fe14f9c"></a>
#### table_name

It is the name of a target table whose rows are to be updated.  
It can define schema to which the table belongs such as schema_name.table_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="04f4b87b9ca46d3e"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="5de18e1efa4f64b9"></a>
#### &lt;set clause&gt;

It defines the columns to be updated and its values to be assigned. The number of columns in &lt;set clause&gt; should be as same as the number of values.

It can be defined as follows.

- column_name = { &lt;value expression&gt; | DEFAULT }

```
UPDATE table_name 
   SET column1 = value1, column2 = value2, column3 = value3
```

- ( column_name [, ...] ) = ( { &lt;value expression&gt; | DEFAULT } [, ...] )

```
UPDATE table_name 
   SET ( column1, column2, column3 ) = ( value1, value2, value3 )
```

- ( column_name [, ...] ) = ( &lt;query expression&gt; )

```
UPDATE table_name 
   SET column1 = ( SELECT max(value1) FROM other_table_name )
```

&lt;query expression&gt; should be a query which creates a single row.

If DEFAULT is defined as a column value, the default values (refer to [&lt;default clause&gt;](#77b8ab635fda06de)) defined when executing [CREATE TABLE](#72507f5467c281c9) is used. If it is not defined, NULL value is assigned.

<a id="1bccec0a69d3210c"></a>
#### WHERE &lt;search condition&gt;

It updates the rows which satisfy WHERE condition.  
If WHERE condition is not specified, all rows are updated.  
For more information about WHERE condition, refer to [where clause](#12ec541722ce6e3e) of [SELECT](#1117040fd802dbd4).

<a id="9f2b4565ddd45a39"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip from the query result.  
For more information, refer to [&lt;result offset clause&gt;](#bee49c088d0c944c) of [SELECT](#1117040fd802dbd4).

<a id="4e2d85b32196493b"></a>
#### &lt;fetch limit clause&gt;

It specifies the number of rows to fetch in two ways, which are &lt;fetch first clause&gt; and &lt;limit clause&gt;.

- &lt;fetch first clause&gt;
    - It specifies the number of rows to be fetched. 
    - For more information, refer to [&lt;fetch first clause&gt;](#89f9ac4af34ef519) of [SELECT](#1117040fd802dbd4) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.
    - For more information, refer to [&lt;limit clause&gt;](#765d5e71a89c2751) of [SELECT](#1117040fd802dbd4) statement.

<a id="cd79c50c40c3a2f3"></a>
### Description

<a id="fa49f838ec451841"></a>
#### Differences among UPDATE-related Statements

- [UPDATE](#607eb6ad25aa2ec3)
    - It updates multiple rows which satisfy the condition.
    - e.g. UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0; 
- [UPDATE name WHERE CURRENT OF cursor_name](#b16d585b333e86ee)
    - It updates the row which the current cursor indicates.
    - e.g. UPDATE t1 WHERE CURRENT OF cursor; 
- [UPDATE name RETURNING](#247a80e4d8b5ad3d)
    - It updates multiple rows which satisfy the conditions, and the updated rows can be retrieved in the same way as [SELECT](#1117040fd802dbd4) statement (API such as SQLFetch ()).
    - e.g. UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0 RETURNING c2; 
- [UPDATE name RETURNING .. INTO](#0d90d25d49a050ed)
    - It updates row equal to or less than one, and if a single row is updated, it obtains the value to the host variable of RETURNING INTO clause.
    - e.g. UPDATE t1 SET c2 = c2 + 1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="6e1d9350cd0f1686"></a>
### Examples

The following is an example of updating multiple rows which satisfy the condition.

```
gSQL> UPDATE lineitem
         SET l_shipdate = CURRENT_DATE
       WHERE l_returnflag = 'R';

5 rows updated.
```

The following is an example of updating the value of multiple columns.

```
gSQL> UPDATE lineitem
         SET l_shipdate   = CURRENT_DATE
           , l_returnflag = 'A'
       WHERE l_returnflag = 'R';

5 rows updated.
```

The following is an example of updating multiple columns by enclosing them with parentheses.

```
gSQL> UPDATE lineitem
         SET ( l_shipdate  , l_returnflag )
           = ( CURRENT_DATE, 'A' )
       WHERE l_returnflag = 'R';

5 rows updated.
```

The following is an example of updating the column value by using the subquery.

```
gSQL> UPDATE lineitem
         SET l_discount = ( SELECT MAX(l_discount) + 0.01 FROM lineitem )
       WHERE l_returnflag = 'R';

5 rows updated.
```

The following is an example of updating part of the rows which satisfy the condition by using OFFSET and FETCH clauses.

```
gSQL> UPDATE lineitem
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
      OFFSET 3
      FETCH 2;

2 rows updated.
```

<a id="f4742cff767cb0c3"></a>
### Compatibility

The SQL standard does not define the following clauses in UPDATE statement.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL standard compatibility**

<a id="a53e98414b18bf45"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="247a80e4d8b5ad3d"></a>
## UPDATE name RETURNING

<a id="8af26533038ec5ea"></a>
### Function

It updates rows in a table, and retrieves the rows of before or after the update.

<a id="8d2e68414b76c375"></a>
### Syntax

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning clause>

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] }
```

<a id="d2e808aba1a94556"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;update returning query statement&gt;.

- One of the following privileges is required to perform UPDATE statement.
    - UPDATE(columns) ON TABLE for all columns which are targets to be updated
    - (UPDATE or CONTROL TABLE) ON TABLE for the table
    - (UPDATE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - UPDATE ANY TABLE ON DATABASE

- One of the following privileges for all columns used in RETURNING clause is required.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause 
    - (SELECT or CONTROL TABLE) ON TABLE for the table
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="dd0c43071ffb0ee5"></a>
### Syntax Rules and Parameters

<a id="673b5e4763d8a70d"></a>
#### table_name

It is the name of a target table whose rows are to be updated.

<a id="7cbd470e00d23e4d"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="84788d58b035138a"></a>
#### &lt;set clause&gt;

It defines the columns to be updated and its values to be assigned. The number of columns in &lt;set clause&gt; should be as same as the number of values.  
For more information, refer to [UPDATE](#607eb6ad25aa2ec3).

<a id="fa9a731cfadb0044"></a>
#### WHERE &lt;search condition&gt;

It updates the rows which satisfy WHERE condition.  
If WHERE condition is not specified, all rows are updated.  
For more information about WHERE condition, refer to [where clause](#12ec541722ce6e3e) of [SELECT](#1117040fd802dbd4).

<a id="0c7f6e97c60fd08a"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip from the query result.  
For more information, refer to [&lt;result offset clause&gt;](#bee49c088d0c944c) of [SELECT](#1117040fd802dbd4).

<a id="edbdebc02fac7a6f"></a>
#### &lt;fetch limit clause&gt;

It specifies the number of rows to fetch in two ways, which are &lt;fetch first clause&gt; and &lt;limit clause&gt;.

- &lt;fetch first clause&gt;
    - It specifies the number of rows to be fetched. 
    - For more information, refer to [&lt;fetch first clause&gt;](#89f9ac4af34ef519) of [SELECT](#1117040fd802dbd4) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.
    - For more information, refer to [&lt;limit clause&gt;](#765d5e71a89c2751) of [SELECT](#1117040fd802dbd4) statement.

<a id="f108034b80604e1d"></a>
#### &lt;returning clause&gt;

It defines the updated rows as a result set, and specifies columns to be retrieved from the result set.

- RETURN and RETURNING are the keywords with the same meaning. 
- NEW | OLD 
    - NEW: It searches for updated rows based on the row after the update.
    - OLD: It searches for updated rows based on the row before the update.
    - If it is omitted, the default value is NEW. 
- &lt;value expression&gt; 
    - It is as same as &lt;select list&gt; in SELECT statement, but aggregation can not be used.
- [ [AS] alias_name] 
    - It can name &lt;value expression&gt; by using AS clause.

<a id="91fc4c490ecd3874"></a>
### Description

For more information, refer to [Differences among UPDATE-related Statements](#fa49f838ec451841).

<a id="1f9567ac14fb5125"></a>
### Examples

The following is an example of obtaining values of the updated rows by using RETURNING clause.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .07
         9            2        .11
        12            5        .05
        15            1        .03
        16            2        .08

5 rows updated.
```

The following is an example of obtaining values before the update for the updated rows by using RETURNING OLD clause.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING OLD l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .06
         9            2         .1
        12            5        .04
        15            1        .02
        16            2        .07

5 rows updated.
```

<a id="d9e05e3fa9566cd6"></a>
### Compatibility

The SQL standard does not define &lt;update returning query statement&gt;.

<a id="0d90d25d49a050ed"></a>
## UPDATE name RETURNING .. INTO

<a id="4df18f4979afb43f"></a>
### Function

It updates a single row of a table, and the updated value is obtained into the host variable.

<a id="56bdcc47a0774d72"></a>
### Syntax

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning into clause>
    ;


<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


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
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO variable_name [, ...]
```

<a id="8e85e5461fc20442"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;update returning query statement&gt;.

- One of the following privileges is required to perform UPDATE statement.
    - UPDATE(columns) ON TABLE for all columns which are targets to be updated
    - (UPDATE or CONTROL TABLE) ON TABLE for the table
    - (UPDATE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - UPDATE ANY TABLE ON DATABASE

- One of the following privileges for all columns used in RETURNING clause is required.
    - SELECT(columns) ON TABLE for all columns used in RETURNING clause
    - (SELECT or CONTROL TABLE) ON TABLE for the table 
    - (SELECT TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - SELECT ANY TABLE ON DATABASE

<a id="e299018fb9100869"></a>
### Syntax Rules and Parameters

<a id="91bcd93d9ecdc55e"></a>
#### table_name

It is the name of a target table whose rows are to be updated.

<a id="0808820451ed94f4"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="305c1e3a7e15ce55"></a>
#### &lt;set clause&gt;

It defines the columns to be updated and its values to be assigned. The number of columns in &lt;set clause&gt; should be as same as the number of values.  
For more information, refer to [UPDATE](#607eb6ad25aa2ec3).

<a id="e85c4f567f04610f"></a>
#### WHERE &lt;search condition&gt;

It updates the rows which satisfy WHERE condition.  
If WHERE condition is not specified, all rows are updated.  
For more information about WHERE condition, refer to [where clause](#12ec541722ce6e3e) of [SELECT](#1117040fd802dbd4).

<a id="4903727d60e91371"></a>
#### &lt;result offset clause&gt;

It specifies the number of rows to skip in the query result.  
For more information, refer to [&lt;result offset clause&gt;](#bee49c088d0c944c) of [SELECT](#1117040fd802dbd4).

<a id="2f065462b856bf62"></a>
#### &lt;fetch limit clause&gt;

It specifies the number of rows to fetch in two ways, which are &lt;fetch first clause&gt; and &lt;limit clause&gt;.

- &lt;fetch first clause&gt;
    - It specifies the number of rows to be fetched. 
    - For more information, refer to [&lt;fetch first clause&gt;](#89f9ac4af34ef519) of [SELECT](#1117040fd802dbd4) statement.
- &lt;limit clause&gt;
    - It specifies the number of rows to be fetched, or it simultaneously specifies both the number of rows to be skipped and the number of rows to be fetched.
    - For more information, refer to [&lt;limit clause&gt;](#765d5e71a89c2751) of [SELECT](#1117040fd802dbd4) statement.

<a id="4dabe48eb5436f9b"></a>
#### RETURNING .. AS ..

It defines the updated rows as a result set, and specifies columns to be retrieved from the result set.  
For more information, refer to [&lt;returning clause&gt;](#f108034b80604e1d) of  [UPDATE name RETURNING](#247a80e4d8b5ad3d).

<a id="ed8e3c1104726107"></a>
#### INTO variable_name [, ...]

The number of variables specified in INTO clause should be equal to the number of the expressions specified in RETURNING clause.  
The row to be updated should be one or less. If two or more rows are updated, an error occurs.

<a id="be84337a9127afa8"></a>
### Description

For more information, refer to [Differences among UPDATE-related Statements](#fa49f838ec451841).

<a id="5b29aae3a74b3756"></a>
### Example

The following is an example of obtaining column values of the updated rows into the host variables.

• Declare the host variable.

```
gSQL> \VAR v_discount NUMBER

gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_orderkey = 12 AND l_linenumber = 5
   RETURNING l_discount INTO :v_discount;

V_DISCOUNT
----------
       .05

1 row updated.
```

<a id="4847b93c35774709"></a>
### Compatibility

In the SQL standard, &lt;update returning into statement&gt; statement does not exist.

<a id="b16d585b333e86ee"></a>
## UPDATE name WHERE CURRENT OF cursor_name

<a id="ee99bc8f3642fbdf"></a>
### Function

It updates a single row which the current cursor indicates.

<a id="8ef8578eeef39757"></a>
### Syntax

```
<update statement: positioned> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="87dac470ac8b11c0"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;update statement: positioned&gt;.

- One of the following privileges is required to perform UPDATE statement.
    - UPDATE(columns) ON TABLE for all columns which are targets to be updated
    - (UPDATE or CONTROL TABLE) ON TABLE for the table
    - (UPDATE TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - UPDATE ANY TABLE ON DATABASE

<a id="e1a3bd3920419dd8"></a>
### Syntax Rules and Parameters

<a id="ba24e4c92ee27805"></a>
#### table_name

It is the name of a table whose rows are to be updated.

<a id="6f50d017c037fc16"></a>
#### [ AS alias_name ]

It is the alias of table_name.

<a id="c97440db18e924e1"></a>
#### &lt;set clause&gt;

It defines the columns to be updated and its values to be assigned. The number of columns in &lt;set clause&gt; should be as same as the number of values.  
For more information, refer to [UPDATE](#607eb6ad25aa2ec3).

<a id="deb209e790fba1ec"></a>
#### cursor_name

The cursor corresponding to cursor_name should satisfy the following conditions.

- The cursor should be OPEN. (Refer to [OPEN cursor_name](#503dadf63d95d09e).) 
- Fetched rows by using the cursor should exist. (Refer to [FETCH cursor_name](#8b90e7e7e6e0c963).) 
- The query used for the cursor should identify table_name. (Refer to [DECLARE cursor_name](#9826eadcd321de1b).) 
- The cursor should be updatable for table_name. (Refer to [DECLARE cursor_name](#9826eadcd321de1b).)

<a id="97fb6fbecabcc763"></a>
### Description

For more information, refer to [Differences among UPDATE-related Statements](#fa49f838ec451841).

<a id="1fca39d734389cea"></a>
### Examples

The following is an example that &lt;update statement: positioned&gt; is performed in interactive SQL (gsql) using the cursor.

- Declare the host variable.

```
gSQL> \VAR v_discount NUMBER
```

- Declare the cursor.

```
gSQL> DECLARE update_cursor CURSOR FOR 
        SELECT l_discount
          FROM lineitem
         WHERE l_orderkey = 8 AND l_linenumber = 1
           FOR UPDATE;

Cursor declared.
```

- Open the cursor.

```
gSQL> OPEN update_cursor;

Cursor is open.
```

- Fetch the row.

```
gSQL> FETCH update_cursor INTO :v_discount;

V_DISCOUNT
----------
       .06

1 row fetched.
```

- Update the current row.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01 
       WHERE CURRENT OF update_cursor;

1 row updated.
```

- Close the cursor.

```
gSQL> CLOSE update_cursor;

Cursor closed.

gSQL> COMMIT;

Commit complete.
```

The following is an example of performing &lt;update statement: positioned&gt; by using the cursor in embedded SQL program.

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
        ...    
        double v_discount;  
        ...   
    EXEC SQL END DECLARE SECTION;
    ...
    EXEC SQL DECLARE update_cursor CURSOR FOR
              SELECT l_discount
                FROM lineitem
               WHERE l_orderkey = 8 AND l_linenumber = 1
                 FOR UPDATE;
    ...
    EXEC SQL OPEN update_cursor;
    ...
    EXEC SQL FETCH NEXT update_cursor INTO :v_discount;
    ...
    EXEC SQL UPDATE lineitem 
                SET l_discount = l_discount + 0.01 
              WHERE CURRENT OF update_cursor;
    ...
    EXEC SQL CLOSE update_cursor;
    ...
    EXEC SQL COMMIT WORK;
    ...
}
```

<a id="86d4a91ee1f1cd32"></a>
### Compatibility

**SQL standard compatibility**

<a id="f2a3757c7234b42a"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F831 | Full cursor update | O |
| B031 | Basic dynamic SQL | O |

<a id="4eb2eebed10822cf"></a>
### For More Information

Refer to [CLOSE cursor_name](#8094485dc3cb5ea5).

---

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Overview of PSM →](../part-04-psm-manual/17-overview-of-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
