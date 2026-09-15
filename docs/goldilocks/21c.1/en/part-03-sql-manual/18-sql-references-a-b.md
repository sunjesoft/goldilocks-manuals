<a id="111809c594826c45"></a>

# 18. SQL References (A~B)

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/111809c594826c45)  
> Tag: `21c.1_35_tag`

[← 17. Built-in Function References](17-built-in-function-references.md) · [Table of contents](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<a id="53347c6092b6e054"></a>
## ALTER AUDIT POLICY

<a id="8d700fac6d15e0ac"></a>
### Function

It adds an auditing target to an audit policy object, or drops an auditing target from an audit policy object.

<a id="5766253d63a18e0a"></a>
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

<a id="b0c52e0541a4a5dd"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;alter audit policy statement&gt;.

<a id="fd6f608e68834c09"></a>
### Syntax Rules and Parameters

<a id="6755a0bad9d32bd9"></a>
#### policy_name

It is the name of an audit policy object to be altered.

<a id="e2e63b5f58392a88"></a>
#### &lt;add_audit_option&gt;

It adds an auditing target to an audit policy.

<a id="9b52e45297b91ead"></a>
#### &lt;drop_audit_option&gt;

It drops an auditing target from an audit policy.

<a id="7581d2a06faf1fdf"></a>
#### &lt;privilege_audit_clause&gt;

For more information, refer to [CREATE AUDIT POLICY](19-sql-references-c-g.md#4f95ec95d004a1b2).

<a id="47fd542580045ce6"></a>
#### &lt;action_audit_clause&gt;

For more information, refer to [CREATE AUDIT POLICY](19-sql-references-c-g.md#4f95ec95d004a1b2).

<a id="be447842441b074f"></a>
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

<a id="a4bfe25db2be8012"></a>
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

<a id="502b5a841f9de33b"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="d5457576d890651e"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#4f95ec95d004a1b2)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#74a07e0949274daf)
    - [ALTER AUDIT POLICY](#53347c6092b6e054)

- Activating/ deactivating audit policy 
    - [AUDIT POLICY](#9289801d878dbdc2)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#1d87c2f21b970bb9)

- Enquiring audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#c239152842953eb8)

- Dropping audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#783e2ba71672a2fa)

<a id="0a6879be2602f377"></a>
## ALTER CLUSTER GROUP name ADD MEMBER

<a id="41bc85b60c1206af"></a>
### Function

It adds a cluster member to a cluster group.

<a id="d9842a39f24a08a1"></a>
### Syntax

```
<alter cluster group add member statement> ::=
    ALTER CLUSTER GROUP group_name ADD
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

<a id="9efa3398511e23ea"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster group add member statement&gt;.

<a id="d8d8eca30f817ce8"></a>
### Syntax Rules and Parameters

<a id="7419e376e1373ffd"></a>
#### group_name

It is the cluster group name.

<a id="52659f0df094f6c3"></a>
#### &lt;cluster member definition&gt;

It defines a cluster member to be included in a cluster group.  
A cluster group may include maximum 32 cluster members.

<a id="2b2b12bd9f85759c"></a>
#### member_name

It is the name of a cluster member.  
The cluster member name should be as same as the member name which was defined when the database of that cluster member was created.  
There should not be the same cluster group, nor the same cluster member.  
The length of the name should be shorter than 128 bytes.

The start-up phase for the cluster member should be GLOBAL OPEN.

<a id="3bc3565001e90201"></a>
#### &lt;connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
&lt;connection attribute&gt; should be as same as the HOST and PORT which were defined when the database of that cluster member was created.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST 'address' uses ip v4 type. 
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="7a223a0767ebc549"></a>
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

<a id="2cc1c9057605eed3"></a>
### Description

&lt;alter cluster group add member statement&gt; statement does not rebalance shards in the tables.  
The following statement should be performed to rebalance shards on the added cluster member.

- [ALTER DATABASE REBALANCE](#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="72910fe57b7c4a85"></a>
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

The following is an example of designating the empty member position as a cluster member position.

```
ALTER CLUSTER GROUP g2 ADD
    CLUSTER MEMBER g2n1 HOST '192.168.0.21' PORT 10210 POSITION 4
;
```

<a id="bee050e2d234c639"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="bd4a458264b9e850"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13)
- [ALTER DATABASE REBALANCE](#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="09ca7c14c479f510"></a>
## ALTER CLUSTER GROUP name OFFLINE MEMBER

<a id="bb035ac5639b807a"></a>
### Function

It sets a cluster member of the cluster group to offline.

<a id="ec385c86aa1775c3"></a>
### Syntax

```
<alter cluster group offline member statement> ::=
    ALTER CLUSTER GROUP group_name OFFLINE CLUSTER MEMBER member_name
    ;
```

<a id="fc98d9a2ed99cf17"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster group offline member statement&gt;.

<a id="021b90d78a20038d"></a>
### Syntax Rules and Parameters

<a id="85f44a2d7d09e9ac"></a>
#### group_name

It is the cluster group name.

<a id="d9454c4c197dda67"></a>
#### member_name

It is the name of a cluster member.  
The cluster member should be included in the cluster group of group_name.  
The cluster member should be inactive.

<a id="4488961081ecccbc"></a>
### Description

It sets the inactive cluster member to offline.

&lt;alter cluster group offline member statement&gt; statement does not rebalance shards in the tables.

<a id="88bda7413f768141"></a>
### Examples

If trying to set the cluster member which is not inactive to offline, then the following error occurs.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE CLUSTER MEMBER g1n2;

ERR-42000(16417): active member 'G1N2' cannot be offlined
```

The following is an example of setting a specific cluster member to offline.

```
gSQL>

ALTER CLUSTER GROUP g1 OFFLINE
    CLUSTER MEMBER g1n3
;
Cluster Group altered.
```

<a id="96f12230536bfe10"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="db6dc904ebff6c63"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13)
- [ALTER DATABASE REBALANCE](#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="68afa63d36875d46"></a>
## ALTER CLUSTER LOCATION

<a id="d6e3683b23dd5126"></a>
### Function

It alters a cluster location information.

<a id="b9698a9a2ebc1d2e"></a>
### Syntax

```
<alter cluster location statement> ::=
    ALTER CLUSTER LOCATION member_name 
    <cluster connection attribute>
    ;

<cluster connection attribute> ::
       HOST 'address' PORT port_no
```

<a id="cd5130da9ee82dcd"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter cluster location statement&gt;.

<a id="2bf601bff4fd0119"></a>
### Syntax Rules and Parameters

<a id="28046bd6cf177119"></a>
#### member_name

It is the name of a cluster member.  
The same cluster member name should exist in the registered cluster location information.  
The length of the name should be shorter than 128 bytes.

<a id="089c1b479afb9bc5"></a>
#### &lt;cluster connection attribute&gt;

It defines the connection information for the communication between the cluster members.  
The combination of HOST and PORT should be unique in the cluster system.

- HOST 'address' uses ip v4 type. 
- PORT port_no should be in the range between 1024 ~ 49151.

<a id="5a50e9ce8a493f4e"></a>
### Description

If the connection information of the cluster location is altered, the cluster member does not need to be dropped or recreated, but the connection information can be altered by using [ALTER CLUSTER LOCATION](#68afa63d36875d46).

<a id="cd1483220bb457e2"></a>
### Examples

```
gSQL> 
ALTER CLUSTER LOCATION g1n2
    HOST '192.168.0.12' PORT 10120
;

altered.
```

<a id="c86a3f7cac5adc59"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="82e0de7700777bfe"></a>
### For More Information

Refer to the followings.

- [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#67ef6e090f63d08d)
- [DROP CLUSTER LOCATION](19-sql-references-c-g.md#351e9009d382090f)

<a id="e61d8380d28bd181"></a>
## ALTER DATABASE ADD LOGFILE

<a id="b5024ddc86b53920"></a>
### Function

It adds log file groups or log file members to the database.

<a id="60bdc5547ea2fe71"></a>
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

<a id="5918cebeb6080cf7"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database add logfile statement&gt;.

<a id="79ece378f9b0c86e"></a>
### Syntax Rules and Parameters

<a id="cbcf84caf4c43feb"></a>
#### &lt;alter database add logfile statement&gt;

The database should be in MOUNT phase.

<a id="8604e8cc2a0e24ab"></a>
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

<a id="88209763044da3b9"></a>
#### &lt;add logfile group statement&gt;

It adds a new log file group.

- It is added as the next group of the CURRENT log file group.
- &lt;group clause&gt; 
    - It specifies the identifier of the logfile group to be added to the database.
    - Integer should be an identifier of the unexisting logfile group.
    - If an identifier for the integer exists, an error occurs.
- &lt;size clause&gt; 
    - The file size can be specified minimum of 20 MB to maximum of 120 GB.
    - The file size should be bigger than the sum of redo log buffer size and pending log buffer size.
- When logfile_name already exists, and the REUSE option is used, if the file size is as same as another group member, then the existing log file is reused.

<a id="2ba285f2d5f64479"></a>
### Description

It is recommended to back up the control file just in case for the file damage because the newly added log file groups and log members are stored in the control file.

<a id="61273b1c0f02d08d"></a>
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

<a id="7e4f503999767f37"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="c244316f546c7ed3"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE ADD LOGFILE](#e61d8380d28bd181)
- [ALTER DATABASE DROP LOGFILE](#8d6a8c5cd906742d)
- [ALTER DATABASE RENAME LOGFILE](#ea9453261d58be3a)

<a id="ba215547bc1143dc"></a>
## ALTER DATABASE ARCHIVELOG

<a id="4e87943d70afd6f6"></a>
### Function

It alters an archive setting of the online log file in the database.

<a id="1bc12327f64e10d0"></a>
### Syntax

```
<alter database archivelog statement> ::=
    ALTER DATABASE { ARCHIVELOG | NOARCHIVELOG }
    ;
```

<a id="0498c4d906bffedd"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database archivelog statement&gt;.

<a id="a1183aaf72e5a28d"></a>
### Syntax Rules and Parameters

<a id="c008b2dfa3487b57"></a>
#### &lt;alter database archivelog statement&gt;

- The database should be in MOUNT phase.
- ARCHIVELOG
    - It archives the online log file.
- NOARCHIVELOG
    - It does not archive the online log file.

<a id="18fd81a9a17f6da7"></a>
### Description

For the database backup and the media recovery using the backup, the system should be operated in ARCHIVELOG mode.

<a id="428283e31cd6a8ab"></a>
### Example

The following is an example of how to set up a database to archive mode.

```
ALTER DATABASE ARCHIVELOG;
```

<a id="b1006a7b3b57e10d"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="8ccb7ebfbe6e941b"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#ad2eeebfaa732bca)
- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)

<a id="ad2eeebfaa732bca"></a>
## ALTER DATABASE BACKUP

<a id="e2fcff53b1c4d7ab"></a>
### Function

The backup state is set to ACTIVE or INACTIVE to perform a full backup of the database. Then, the incremental database backup and control file backup are performed.

<a id="12045f41d807e293"></a>
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

<a id="069db0925a41a64f"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database backup statement&gt;.

<a id="f48c466560327e2c"></a>
### Syntax Rules and Parameters

<a id="b5846fdd52242721"></a>
#### &lt;database begin backup clause&gt;

The database is set to the state which the full backup is available.

- All tablespaces in ONLINE state, which are created and used in the database, are set to the state of which the full backup is available. 
- The database should be OPEN state and operated in ARCHIVELOG mode.
- After starting BEGIN BACKUP, the following operations which require writing to the data file can not be performed.
    - SHUTDOWN NORMAL
    - OFFLINE / DROP TABLESPACE
    - ADD / DROP DATAFILE
- It may require media recovery on restart when a full backup is ACTIVE state and the instance is abnormally terminated.

<a id="f9f920e902f22e3c"></a>
#### &lt;database end backup clause&gt;

The database is set to the state which the full backup is not available.

- All tablespaces in ONLINE state, which are created and used in the database, are set to the state which the full backup is not available. 
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

<a id="0bcd4d22e7026c99"></a>
#### &lt;database incremental backup statement&gt;

- An incremental backup is performed for the database.
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

<a id="045a8004f333f55d"></a>
#### &lt;incremental backup option&gt;

- 'integer' can be specified from 0 to 4. 
- LEVEL 0 can not specify CUMULATIVE or DIFFERENTIAL.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n-1. 
    - DIFFERENTIAL
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n. 
    - If it is omitted, DIFFERENTIAL is specified by default.

<a id="29b0edd68607f2cb"></a>
#### &lt;database controlfile backup statement&gt;

- The control file is backed up. 
    - The length of 'target_name' should be shorter than 1024 bytes.
    - If 'target_name' already exists, the operation fails.
- The database should be in OPEN phase and operated in ARCHIVELOG mode.

> The maximum length of the 'target_name' managed by GOLDILOCKS is 1024 bytes. However, the maximum lengths of the file name varies depending on the OS, so the actual length of 'target_name' which is available to be created can be shorter than 1024 bytes.

<a id="5b4b951c336203d7"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="84b0288f37b2eba0"></a>
### Description

It backs up data files and control files in the database. A full backup of the database begins with BEGIN BACKUP, and copies the datafiles using OS file copy, then ends with END BACKUP. The incremental backup file is created in the path set by the BACKUP_DIR 1 property using a single statement.

<a id="945630ff1623ab39"></a>
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

<a id="ae54b6b4a057fcf6"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="9950f8c01c5c281a"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)
- [ALTER DATABASE RECOVER](#3fa18e0049bd27dd)

<a id="783e2ba71672a2fa"></a>
## ALTER DATABASE CLEAR AUDIT TRAIL

<a id="2fc412da11ba22fe"></a>
### Function

It purges audit records which are accumulated when applying an audit policy.

<a id="ed430716a3922ab5"></a>
### Syntax

```
<clear audit trail statement> ::= 
    ALTER DATABASE CLEAR AUDIT TRAIL
;
```

<a id="1658015853ad5cba"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;clear audit trail statement&gt;.

<a id="9b1b96cab92ca810"></a>
### Description

If an audit policy is activated, an audit trails is getting longer as time goes by.  
Tables configuring an audit trail are stored in MEM_AUX_TBS tablespace, and a user should be cautious not to let the audit trail keep increasing.

<a id="1844a6173151305f"></a>
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

<a id="852488693ad8c9e3"></a>
### Examples

Purge an audit trail by using the following statement.

```
ALTER DATABASE CLEAR AUDIT TRAIL;
```

<a id="e4ca9dcfd07d71ed"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="3e8c489a8ff6920a"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#4f95ec95d004a1b2)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#74a07e0949274daf)
    - [ALTER AUDIT POLICY](#53347c6092b6e054)

- Activating/ deactivating audit policy 
    - [AUDIT POLICY](#9289801d878dbdc2)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#1d87c2f21b970bb9)

- Enquiring audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#c239152842953eb8)

- Dropping audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#783e2ba71672a2fa)

<a id="45533ba352d57e4b"></a>
## ALTER DATABASE CLEAR PASSWORD HISTORY

<a id="cf85ccfb6aaa4ea0"></a>
### Function

It deletes the user's password change history which is accumulated due by applying the profile.

<a id="c2550d9de2d0618d"></a>
### Syntax

```
<clear password history statement> ::= 
    ALTER DATABASE CLEAR PASSWORD HISTORY
    ;
```

<a id="f3df0377de262e00"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;clear password history statement&gt;.

<a id="2935d57d2dfd0d2a"></a>
### Description

When a profile is applied to a user, the user's password change history is accumulated according to the PASSWORD_REUSE_MAX and PASSWORD_REUSE_TIME policies.

**Managing the change history**

<a id="2d1e21acd65ff103"></a>
| PASSWORD_REUSE_MAX | PASSWORD_REUSE_TIME | Managing the change history |
| --- | --- | --- |
| value | value | It manages only the change history within the value range, and the change history out of the value range is automatically deleted. |
| value | UNLIMITED | It accumulates all change history and it does not delete any change history because all change history should be checked. |
| UNLIMITED | value | It accumulates all change history and it does not delete any change history because all change history should be checked. |
| UNLIMITED | UNLIMITED | It does not manage the change history because the change history is not checked. |

&lt;Clear password history statement&gt; deletes the accumulated user's password change history.

<a id="cf178d676e134faf"></a>
### Examples

The following is an example of executing &lt;clear password history statement&gt; statement.

```
gSQL> ALTER DATABASE CLEAR PASSWORD HISTORY;

Database altered.

gSQL> COMMIT;

Commit complete.
```

<a id="1f6db32c6adbb5a7"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="8a71f735c003dceb"></a>
### For More Information

Refer to the followings.

- [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024)
- [CREATE USER](19-sql-references-c-g.md#67d566d84adb0376)

<a id="fbe5739ba301ebcf"></a>
## ALTER DATABASE DATAFILE AUTOEXTEND

<a id="38996dd0487e8d78"></a>
### Function

It alters the property to automatically extend disk tablespace data file. If the property is ON, then the size to be extended and the maximum size of the data file also can be altered.

<a id="d6c2dd5ee9c6a8eb"></a>
### Syntax

```
<alter database datafile autoextend statement> ::= 
    ALTER DATABASE DATAFILE datafile_name <autoextend clause>
        [ AT <domain name> ]
    ;

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }
```

<a id="9d897ae40a5674b1"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database datafile autoextend statement&gt;.

The datafile automatic expand property can alter the property of disk tablespace only.

<a id="9402569c57af60c9"></a>
#### datafile_name

It specifies the name of the data file to be altered.

<a id="d83b8ec575242d52"></a>
#### &lt;autoextend clause&gt;

It sets the automatic expand property to ON or OFF. If it is set to ON, then it can specify the automatic expanded size and the maximum size of the data file.

<a id="7b7052d1cbc73a09"></a>
#### &lt;next size clause&gt;

It specifies the size to be extended when the data file in use does not have available space.

<a id="d761529820bc5be1"></a>
#### &lt;max size clause&gt;

It specifies the maximum expanded size of the data file.

<a id="228bc3f11aba618b"></a>
### Description

Refer to the syntax rules of each statement.

<a id="61817530dedd8762"></a>
### Examples

The following is an example of altering the automatic expand property of the datafile, the automatic expanded size, and datafile size.

```
gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND OFF;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON NEXT 20M;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON MAXSIZE 1G;

Database altered.

gSQL> ALTER DATABASE DATAFILE 'DISK_TBS.dbf' AUTOEXTEND ON 20M MAXSIZE 1G;

Database altered.
```

<a id="c978c3171804f920"></a>
### Compatibility

The SQL standard does not define the concepts of the datafile.

<a id="c328cd415851a5ce"></a>
### For More Information

Refer to [CREATE DISK DATA TABLESPACE](19-sql-references-c-g.md#f9c7eb32cc7ffaf4).

<a id="e90cdf82964500a1"></a>
## ALTER DATABASE DELETE BACKUP

<a id="56e2e422eed9e669"></a>
### Function

It deletes the backup file and the backup information of incremental backup. It can delete all incremental backup of the database or no longer usable obsolete backup.

<a id="35b44653cd20f1d8"></a>
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

<a id="a26350d40e900361"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database delete backup statement&gt;.

<a id="5c8ce2985749a792"></a>
### Syntax Rules and Parameters

<a id="eda570264adaf62a"></a>
#### &lt;alter database delete backup statement&gt;

The database should be in MOUNT or OPEN phase.

<a id="56dc324912ab6a2b"></a>
#### &lt;delete backup list option&gt;

It selects the backups to be deleted among the existing incremental backups.

- OBSOLETE: It selects backups of database or tablespaces to be deleted, which was backed up before the most recent database LEVEL 0 backup. 
- ALL: It selects all incremental backups to be deleted.

<a id="42d53b085829c863"></a>
#### &lt;including backup file option&gt;

- If it is omitted, it deletes only the backup information from the control file.
- It also deletes not only backup information but also the backup files.

<a id="0ff486fb6b458a85"></a>
### Description

Deletion of the OBSOLETE incremental backup deletes the incremental backup of which is before the most recent LEVEL 0 database backup. When non-LEVEL 0 incremental backup is performed, it is not deleted even if it includes the previously performed incremental backup. It is because it can be used when performing the incomplete recovery by using the incremental backups.

> Be cautious of deleting the backup file together when an incremental backup is deleted. It can not be recovered even by using the control file which has incremental backup information.

<a id="09f992fbcc13a13b"></a>
### Example

The following is an example to delete the backup information and backup files of all existing incremental backups.

```
ALTER DATABASE DELETE ALL BACKUP LIST INCLUING BACKUP FILES;
```

<a id="a4291010485d6447"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="6e02506f2621dcd5"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)
- [ALTER DATABASE RECOVER](#3fa18e0049bd27dd)

<a id="63f811ebc15cf737"></a>
## ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS

<a id="07d2e523084c39f9"></a>
### Function

It drops the entire inactive cluster member.

<a id="63b83978133b8e30"></a>
### Syntax

```
<alter database drop inactive members statement> ::=
    ALTER DATABASE DROP [ FORCE | NO FORCE ] INACTIVE CLUSTER MEMBERS
    ;
```

<a id="11e79e523b2d19cc"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database drop inactive cluster members statement&gt;.

<a id="c2739783d77bbcf4"></a>
### Syntax Rules and Parameters

<a id="73ff26b7e3e13827"></a>
#### [ FORCE | NO FORCE ]

- FORCE
    - It drops an inactive cluster member even when there is a possibility of data loss.
- NO FORCE
    - It can not drop an inactive cluster member if there is a possibility of data loss.
- The default value is NO FORCE.

<a id="972e73301ca7cb50"></a>
### Description

It drops the entire inactive cluster member.

The inactive state of a cluster member means that it is not connected to the cluster system, and it occurs in the following cases.

- An error occurs on a cluster member in an operating cluster system.
- Trying to start-up the cluster system without driving the cluster member.

However, if the table shard is lost while dropping the cluster member, then an inactive cluster member can not be dropped.

Also, if there is a possibility of data loss when dropping the cluster member, then an inactive cluster member can not be dropped. The data is not lost when it is guaranteed that the data in replica of the table or the shard which belongs the inactive cluster member to be dropped is not latest comparing to that in the members of that cluster group. Therefore, an inactive cluster member can be dropped when at least one online member exists in the same cluster group in case for the sharded table, and in the entire cluster in case for the cloned table.

However, if an online cluster member does not exist in the cluster group and the service is not available due to an inactive cluster member, then the inactive cluster member can be dropped by using FORCE option despite of the possibility of the data loss.

It is recommended to use &lt;alter database drop inactive members statement&gt; when an inactive cluster member can not be included in the cluster system any more.

<a id="77c2628f3938f17e"></a>
### Examples

The following is an example of executing &lt;alter database drop inactive members statement&gt;.

```
gSQL> ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="918782d8d4e42468"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="d911b33e624e3d4f"></a>
### For More Information

Refer to [ALTER SYSTEM JOIN DATABASE](#389b6cddb5c2c458).

<a id="8d6a8c5cd906742d"></a>
## ALTER DATABASE DROP LOGFILE

<a id="30a0f342b1850a3f"></a>
### Function

It drops a log file group or a member which exists in the database.

<a id="3795b1f8209b65b0"></a>
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

<a id="e27a63e03aaf8dc7"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database drop logfile statement&gt;.

<a id="42f63a242c95e28a"></a>
### Syntax Rules and Parameters

<a id="da36004292fc8c84"></a>
#### &lt;alter database drop logfile statement&gt;

The database should be in MOUNT phase.  
An error occurs when the log file to be deleted is in CURRENT or ACTIVE stage.  
At least four log file groups should be remained after dropping.

<a id="104de39129dfb4e2"></a>
#### &lt;drop logfile group statement&gt;

It drops the existing log file group.

- &lt;group clause&gt; 
    - It specifies the log file group to be dropped.
    - An integer should be an identifier of the existing log file.
    - An error occurs if the integer does not exist.

<a id="52d2aa77b73fadde"></a>
#### &lt;drop logfile member statement&gt;

It drops the existing log file members.

- &lt;logfile_list&gt;
    - It is the list of the log file members to be dropped.
    - 'logfile_name' should be an existing name. 
    - An error occurs if 'logfile_name' does not exist.

<a id="cfc80b71161818f0"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="f7b5da7c0c97742b"></a>
### Examples

The following is an example of dropping the existing log file GROUP 3.

```
ALTER DATABASE DROP LOGFILE GROUP 3;
```

The following is an example of dropping logfile1.log and logfile2.log from the existing logfile GROUP 3.

```
ALTER DATABASE DROP LOGFILE MEMBER 'logfile1.log', 'logfile2.log';
```

<a id="ed4890b16c30364b"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="f95e5b4c62e5cccb"></a>
### For More Information

Refer to the respective syntax rules, and the followings.

- [ALTER DATABASE ADD LOGFILE](#e61d8380d28bd181)
- [ALTER DATABASE RENAME LOGFILE](#ea9453261d58be3a)

<a id="2539c44d7da42e34"></a>
## ALTER DATABASE MOVE SHARD

<a id="6200927208403c61"></a>
### Function

It rebalances shard of all tables in a specific cluster group to another cluster group.

<a id="3685e2be4aee2830"></a>
### Syntax

```
<alter database move shard statement> ::=
    ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP src_cluster_group
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ];
```

<a id="c2c134050d1ee28f"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database move shard statement&gt;.

<a id="6515405d1a79bac5"></a>
### Syntax Rules and Parameters

<a id="9e2b9db7982a2184"></a>
#### src_cluster_group

It is a cluster group to which the table shard is moved.

<a id="95fb48b2fc733098"></a>
#### dest_cluster_group

It is a target cluster group to which the table shard is moved.

<a id="49c216ff621a4deb"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="4b2d905ed72993b7"></a>
### Description

When adding a cluster member and a cluster group using the following statements, the table shard is not rebalanced.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0a6879be2602f377)

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

It is performed as above for all tables except for a CLONED table and a CLUSTER WIDE table. The &lt;alter database move shard statement&gt; is proceeded even when the rebalancing the shard of a specific table fails. It does not rollback the table which succeeded in rebalancing the shard.

Therefore, when performing &lt;alter database move shard statement&gt; again after appropriately processed an error, then it rebalances only the shard for the table requiring the rebalancing. In this case, the table which succeeded in rebalancing the shard is not included in a target of the rebalancing.

<a id="4d5d0ddedea43d3e"></a>
### Examples

The following is an example of performing &lt;alter database move shard statement&gt;.

```
gSQL> ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP G1 TO CLUSTER GROUP G2;

Database altered.
```

<a id="87d6e323491766e3"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="b5bfabb18ee97cbd"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name MOVE SHARD](#ce282f55c7c9877b)
- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0a6879be2602f377)

<a id="6cdf673e33168368"></a>
## ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS

<a id="2df8f1b35e0d35a4"></a>
### Function

It sets the entire inactive cluster member to offline. In other words, it sets the shard map for the cluster member to offline.

<a id="fd6005fb54c1e41d"></a>
### Syntax

```
<alter database offline inactive cluster members statement> ::=
    ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS
    ;
```

<a id="252f109c59a70c5f"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database offline inactive cluster members statement&gt;.

<a id="ddab695d42f8d23a"></a>
### Syntax Rules and Parameters

It sets the entire inactive cluster member to offline.  
The inactive state of a cluster member means that it is not connected to the cluster system, and it occurs in the following cases.

- An error occurs on a cluster member in an operating cluster system.
- Trying to start-up the cluster system without driving the cluster member.

<a id="c59eeb1b95b4715a"></a>
### Description

It is recommended to use &lt;alter database offline inactive members statement&gt; when an inactive cluster member can not be included in the cluster system any more.

If an inactive cluster member can participate in a cluster system, then perform [ALTER SYSTEM JOIN DATABASE](#389b6cddb5c2c458) to include it in a cluster system.

The cluster member which is set to offline can be shifted to online again by using the following statements after the join.

- [ALTER DATABASE REBALANCE](#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="e2bf9ef091f2f42e"></a>
### Examples

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;
```

<a id="40d96ca9e0265c59"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="960c663415a39880"></a>
### For More Information

Refer to the followings.

- [ALTER SYSTEM JOIN DATABASE](#389b6cddb5c2c458)
- [ALTER DATABASE REBALANCE](#218ad4f730bea674)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="218ad4f730bea674"></a>
## ALTER DATABASE REBALANCE

<a id="879f2de60e3720d5"></a>
### Function

It rebalances shard of all tables.

<a id="2482068884157e77"></a>
### Syntax

```
<alter database rebalance statement> ::=
    ALTER DATABASE REBALANCE [ ONLINE | OFFLINE ];
```

<a id="3825e747e9385c1f"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database rebalance statement&gt;.

<a id="1070c99d7c78c91d"></a>
### Syntax Rules and Parameters

<a id="31d5e48febf848c9"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="669f43e0968ae9c6"></a>
### Description

When adding a cluster member and a cluster group using the following statements, the table shard is not rebalanced.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0a6879be2602f377)

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

<a id="dea3aeda597345a9"></a>
### Examples

The following is an example of performing &lt;alter database rebalance statement&gt;.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="5868fa47e6cef2cf"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="cda81b6aa0a2faa1"></a>
### For More Information

Refer to [ALTER TABLE name REBALANCE](#f7d09b5058d6293a).

<a id="ddaf56ae2c345c2c"></a>
## ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP

<a id="8ebf4c41ae3eb2ac"></a>
### Function

It rebalances shard of all tables excluding shards of a specific cluster group.

<a id="2fd4341efdf60b39"></a>
### Syntax

```
<alter database rebalance exclude cluster group statement> ::=
    ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP cluster_group_name [ ONLINE | OFFLINE ];
```

<a id="1f0dee1a9acd1f52"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database rebalance exclude cluster group statement&gt;.

<a id="3ea606f324c62431"></a>
### Syntax Rules and Parameters

<a id="0daa6d2c296a82e1"></a>
#### cluster_group_name

It is a name of the cluster group excluding a shard of the table.  
If the specified cluster group is the only cluster group, then the statement can not be performed.

<a id="b51f0690c5f4be4e"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="85470c7957da9aad"></a>
### Description

To drop a cluster group by using [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13), there should not be a shard in the cluster group.

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

<a id="db9ea08a92808c34"></a>
### Examples

The following is an example of performing &lt;alter database rebalance exclude cluster group statement&gt;.

```
gSQL> ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP g3;

Database altered.
```

<a id="9a90998077c24a54"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="bb51f022d8fe88af"></a>
### For More Information

Refer to the followings.

- [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#f003b5733529d1e0)

<a id="3fa18e0049bd27dd"></a>
## ALTER DATABASE RECOVER

<a id="b45ea6118abb98ac"></a>
### Function

It recovers the entire data file or part of the data files in the database by using the online and archive log files.

<a id="5fcfc44da734a0b9"></a>
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

<a id="c5dff3ffd9d2fd76"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database recover statement&gt;.

<a id="cb7f68e8dc8956aa"></a>
### Syntax Rules and Parameters

<a id="ee912b12a75c0bfe"></a>
#### &lt;complete database recover statement&gt;

The data files of the database are recovered up to date by using the online and archive log files.

- The recovery is performed for all tablespaces in the ONLINE state.
- The database should be in MOUNT phase and in ARCHIVELOG mode. 
- If the required archived log file does not exist, it fails.

<a id="b58137fec6ae02ee"></a>
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

<a id="a125cf42584d900e"></a>
#### &lt;complete tablespace recover statement&gt;

The data files of the tablespace is recovered up to date.

- Tablespace recovery should be performed when the database is in MOUNT or OPEN phase. 
- The recovery in the OPEN phase can only be performed when the tablespaces is in the OFFLINE stage, and the recovery in MOUNT phase can be performed when the tablespace is either in ONLINE/ OFFLINE stage. 
- If the required archive log file does not exist, it fails.
- The following is the case which requires the tablespace recovery operation.
    - The tablespace became OFFLINE by IMMEDIATE. 
    - The backed up data file is used.
    - A failure occurred during the entire backup.

<a id="2e378b986704937d"></a>
#### &lt;incomplete database recover statement&gt;

<a id="90f05189ae70d907"></a>
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

<a id="b6319f48e9762498"></a>
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

<a id="8187e2515068024f"></a>
### Description

Incomplete recovery of the database is not easy to find a recovery completion point at a time. Therefore, the desired recovery point is found by performing it several times.  
However, it becomes a new database if the database is started up with RESETLOGS option after an incomplete recovery. Therefore, the incomplete recovery should be performed several times after creating a copy of the archived log files and online redo log files.

<a id="eae70288363c958e"></a>
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

<a id="29a57f7c0169fc11"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="0cf2be2a70c81d59"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#ad2eeebfaa732bca)
- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)
- [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#54011886eee6d8dd)

<a id="f1c48ce65f4ddd31"></a>
## ALTER DATABASE REGISTER

<a id="ee7458546c604730"></a>
### Function

It registers unrecoverable segments in the database.

<a id="ba05fb46139388d9"></a>
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

<a id="134076b9b2e08fc7"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database register statement&gt;.

<a id="7126e0d5599af582"></a>
### Syntax Rules and Parameters

<a id="99ebbc99fcab25d1"></a>
#### &lt;alter database register statement&gt;

It registers the unrecoverable segments in the database. The statement can be used on the assumption that the segment is not used any more, when the database is not recoverable and the backup does not exist.

- The database should be in MOUNT phase. 
- The registered segment identifier list is initialized at restart.
- If a server restart is successful, the registered segment becomes 'UNUSABLE' state, and that segments should be deleted.

<a id="973304637f3c80c1"></a>
#### &lt;segment physical identifier list&gt;

The list of unrecoverable segment identifier  
• Integer: 8 bytes integer segment identifier

<a id="76dd78e521435944"></a>
### Description

When a server restarts after abnormal termination, the database performs the recovery process. During this process, it executes pages again by using the REDO log to recover pages which was not reflected in the disk in the previous service stage.

If an unexpected failure occurs during execution of the REDO operation, that statement can be used to ignore the failure and to execute the recovery.

<a id="3cfc74c735d32a38"></a>
### Example

The following is an example of giving up the recovery of the segment whose identifier is 4028679323648.

```
ALTER DATABASE REGISTER IRRECOVERABLE SEGMENT 4028679323648;
```

<a id="fc6455fd735fe2a2"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="b79ff629561f68ac"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)
- [ALTER DATABASE RECOVER](#3fa18e0049bd27dd)

<a id="ea9453261d58be3a"></a>
## ALTER DATABASE RENAME LOGFILE

<a id="72a3f2fd2fc96e30"></a>
### Function

It renames the logfile in the database.

<a id="5586fc0a0dd49dc4"></a>
### Syntax

```
<alter database rename logfile statement> ::=
    ALTER DATABASE RENAME LOGFILE <logfile_list> TO <logfile_list>
    ;

<logfile_list> ::=
      'logfile_name'
    | <logfile_list> , 'logfile_name'
```

<a id="cd683b4a69503585"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required for performing &lt;alter database rename logfile statement&gt;.

<a id="ebaadb0a1dd2e4ac"></a>
### Syntax Rules and Parameters

<a id="44da4d19d4d43261"></a>
#### &lt;alter database rename logfile statement&gt;

- The database should be in MOUNT phase. 
- FROM &lt;logfile_list&gt;
    - The name list of the logfiles to modify in the database.
- TO &lt;logfile_list&gt;
    - The name list of the logfiles to be modified in the database.
    - &lt;logfile_list&gt; should be an existing file.
    - An error occurs if the file does not exist.

<a id="8c8f7d0001f9f745"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="257703f9b80ec42b"></a>
### Example

The following is an example of modifying the existing 'logfile.log' logfile to 'newlogfile.log'.

```
ALTER DATABASE RENAME LOGFILE 'logfile.log' TO 'newlogfile.log';
```

<a id="0bd1aa75c6082d16"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="9194c4c74f73e104"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE ADD LOGFILE](#e61d8380d28bd181)
- [ALTER DATABASE DROP LOGFILE](#8d6a8c5cd906742d)

<a id="ebfd1a9a53aef514"></a>
## ALTER DATABASE RESET LOCAL CLUSTER MEMBER

<a id="deae6b469235185b"></a>
### Function

It resets the local cluster member except for the tablespace object to the time of creating the database.

<a id="911a258849c58ec3"></a>
### Syntax

```
<alter database reset local cluster member statement> ::=
    ALTER DATABASE RESET LOCAL CLUSTER MEMBER
    ;
```

<a id="3f1413a7044e0caa"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

The start-up phase should be LOCAL OPEN.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter database reset local cluster member statement&gt;.

<a id="bb020acf090cec4a"></a>
### Description

It resets the local cluster member except for the tablespace object to the time of creating the database. It drops all objects created by a user except for the tablespace object.

&lt;alter database reset local cluster member statement&gt; statement resets an inactive cluster member, and makes the new cluster member to participate in a cluster system.  
An inactive cluster member which is disconnected from the cluster system is processed as follows.

- If it can join in a cluster system again, then use JOIN statement to make it join. 
    - [ALTER SYSTEM JOIN DATABASE](#389b6cddb5c2c458)
- If it can not join in a cluster system again, then use DROP statement to exclude it. 
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#63f811ebc15cf737)

In this case, the device corresponding to the cluster member which is excluded from a cluster system can be used again by using the following two methods.

- Method 1: Recreate the database of the local cluster member. 
- Method 2: Reset the local cluster member by using &lt;alter database reset local cluster member statement&gt;.

The method 2 reduces the cost of recreating the tablespace comparing to the method 1.

<a id="c7d04dcc81d236a9"></a>
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

<a id="ed7f224d6a08cbb8"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="92afa1b900d5df89"></a>
### For More Information

Refer to the followings.

- [ALTER SYSTEM JOIN DATABASE](#389b6cddb5c2c458)
- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#63f811ebc15cf737)

<a id="85fee9c048422d86"></a>
## ALTER DATABASE RESTORE

<a id="0930c09c372680b9"></a>
### Function

It restores the data files in the database or tablespace by using the incremental backup.

<a id="5ac00333aedec775"></a>
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

<a id="6db556b97cc3e4e1"></a>
### Invocation and Access Rules

ALTER DATABASE ON DATABASE privilege is required to perform &lt;alter database restore statement&gt;.

<a id="1ea1b245d31bbb95"></a>
### Syntax Rules and Parameters

<a id="71e43c8f01cc923c"></a>
#### &lt;database restore statement&gt;

It restores the data files in the database by using the incremental backup.   
The database should be in MOUNT phase.

<a id="0df8b5a05febaefd"></a>
#### &lt;tablespace restore statement&gt;

It restores the data files in the tablespace by using the incremental backup.

- The database should be in MOUNT or OPEN phase.
- The recovery in OPEN state can be performed only for the tablespaces in OFFLINE state. The recovery in MOUNT phase can be performed for the tablespace is either in ONLINE state or OFFLINE state.

<a id="3cb88d2c2844d11d"></a>
#### &lt;controlfile restore statement&gt;

The control file is recovered using 'file_name'.

- The database should be in NOMOUNT phase.
- The absolute path is recommended for 'file_name' but if relative path is described, then &lt;GOLDILOCKS_HOME&gt;/wal/'file_name' is used.

<a id="5136f2574ab2f0d6"></a>
### Description

The data recovery using full backup uses OS copy command to directly copy the backup file to the data file path. The data recovery using incremental backup restores only the deleted data files or old data files.

<a id="5956d6304ac7d575"></a>
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

<a id="47da6ca36b6562e7"></a>
### Compatibility

The SQL standard does not define ALTER DATABASE statement.

<a id="901f7dc31862584c"></a>
### For More Information

Refer to the followings.

- [ALTER DATABASE BACKUP](#ad2eeebfaa732bca)
- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)
- [ALTER DATABASE RECOVER](#3fa18e0049bd27dd)

<a id="48553e0933068af5"></a>
## ALTER INDEX

<a id="602a9a9ef2fc6972"></a>
### Function

It alters the index definition.

<a id="1de556d446d89f86"></a>
### Syntax

```
<alter index statement> ::=
      <alter index physical attribute statement>
    | <rename index statement>
    | <aging index statement>
    | <rebuild statement>
    ;
```

<a id="535313812f3b8d7b"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="4cd951ccae0feb03"></a>
### Syntax Rules and Parameters

<a id="b9a625ac65d1b341"></a>
#### &lt;alter index physical attribute statement&gt;

It alters physical attributes of the index.  
For more information, refer to [ALTER INDEX name STORAGE](#15c9d7666e8ad651).

<a id="e913908bd95d4a37"></a>
#### &lt;rename index statement&gt;

It alters the index name.  
For more information, refer to [ALTER INDEX name RENAME TO](#a7fb743218a1f203).

<a id="8c8a79bbd2ca7142"></a>
#### &lt;aging statement&gt;

It deletes the empty page of the index.  
For more information, refer to [ALTER INDEX name AGING](#1e08b0a563c14569).

<a id="bb37be4a350018d6"></a>
#### &lt;rebuild statement&gt;

It rebuilds the index.  
For more information, refer to [ALTER INDEX name REBUILD](#0df5754f2a0050c1).

<a id="9faf1a614da7846a"></a>
### Description

Refer to the descriptions of each detailed statement.

<a id="d15e5e5f1742eb77"></a>
### Examples

Refer to the examples of each detailed statement.

<a id="580126efdead73d6"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="1e08b0a563c14569"></a>
## ALTER INDEX name AGING

<a id="2345e280b5b3ade9"></a>
### Function

It deletes an empty page of the index.

<a id="f2892d3d5bf5e7d8"></a>
### Syntax

```
<aging index statement> ::=
    ALTER INDEX index_name AGING
    ;
```

<a id="a84ef00a76ef3286"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;aging index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="12f2398210593c8a"></a>
### Syntax Rules and Parameters

<a id="34d5120cd01e2d32"></a>
#### index_name

It is the name of the target index.

<a id="eea2ea9da3b6fc1c"></a>
### Description

This syntax returns pages whose all keys are deleted among index pages to a segment. Aging is processed in two steps which are logical deletion and physical deletion. A logical deletion is disconnection of index page, and it is performed when SCN of when deleting the last key of a page is smaller than the agable SCN of the system. Then the physical deletion is performed when the SCN of the logical deletion is smaller then the agable SCN of the system.

> If the agable SCN of the system does not increase, then the empty page may not be deleted even though the index AGING statement succeeded.

<a id="6d2f15c897cbb7bd"></a>
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

<a id="482caaeafcf48cde"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="c435a69bbbc0a5f7"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](19-sql-references-c-g.md#d54e994b20c1da1b)
- [ALTER INDEX](#48553e0933068af5)
- [DROP INDEX](19-sql-references-c-g.md#fcb6f064d90f791d)

<a id="0df5754f2a0050c1"></a>
## ALTER INDEX name REBUILD

<a id="3fa35cff418bdb17"></a>
### Function

It rebuilds an index.

<a id="d1cbde8547328c16"></a>
### Syntax

```
<rebuild index statement> ::=
    ALTER INDEX index_name REBUILD
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
    ;

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

<a id="356debf384fe8858"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;rebuild index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

At least one of the following privileges for a tablespace in which the index is to be created is required.

- CREATE OBJECT ON TABLESPACE for that tablespace
- USAGE TABLESPACE ON DATABASE

<a id="a3dfa5147320be8b"></a>
### Syntax Rules and Parameters

<a id="a02ae5f47589f7b8"></a>
#### index_name

It is the name of the target index.  
The schema name can be specified, and the user's default schema name is used when it is omitted.

<a id="2329cf7d6e437dc9"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML on the table when rebuilding the index.

- ONLINE
    - It allows INSERT, UPDATE, and DELETE.
- OFFLINE
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="61aca7a376509b6e"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of an index.

- PCTFREE integer 
    - Definition
        - It is the reserved space for adjusting the page split frequency caused by the key inserted in the page.
    - It can use the value from 0 to 99.
    - If it is omitted, the default value is the value set in the existing index.

- INITRANS integer 
    - Definition 
        - It specifies the initial number of transactions which can simultaneously access the page. 
        - If the number of users who access the index is small, INITRANS is set to low, and if the number of users who simultaneously access the index is big, INITRANS is set to high. 
        - If necessary, it is automatically increased to the specified MAXTRANS. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is the value set in the existing index.

- MAXTRANS integer 
    - Definition 
        - It specifies the maximum number of transactions which can simultaneously access the page. 
    - It can use the value from 1 to 32.
    - If it is omitted, the default value is the value set in the existing index.

<a id="f2f496c55bfcd66d"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of physical storage space which is initially allocated when creating the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually operated as 8192 bytes.)
        - The size (aligned to the EXTENT size of TABLESPACE) should be equal to or bigger than MINEXTENTS, or it should be equal to or less than MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is omitted, the default value is the value set in the existing index.

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
    - If it is omitted, the default value is the value set in the existing index.

- MINSIZE integer
    - Definition
        - It is the minimum space size of the index.
        - The value should smaller than or equal to MAXSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it is specified to the size of two EXTENT.
    - If it is omitted, the default value is the value set in the existing index.

- MAXSIZE integer
    - Definition
        - It is the maximum space size of the index.
        - The value should be equal to or bigger than MINSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is omitted, the default value is the value set in the existing index.

<a id="808e64db1742ebab"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If the unit is omitted, the default value is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="58f8ade46f059201"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used when rebuilding an index.

- NOPARALLEL 
    - It does not rebuild an index in parallel.
- PARALLEL [integer] 
    - It rebuilds an index in parallel.
    - If an integer is omitted or set as 0, then it follows INDEX_BUILD_PARALLEL_FACTOR property. 
    - The minimum value of an integer is 0 and the maximum value is 64. 
    - If the integer or the property value is 0, then the system determines the optimal value.
- If it is omitted, the default value is NOPARALLEL.

<a id="63e5b901b33c1d69"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be rebuilt.

- When it specifies tablespace_name
    - if tablespace_name is data tablespace, then it is rebuilt as a LOGGING index.
    - if tablespace_name is temporary tablespace or nologging tablespace, then it is rebuilt as a NOLOGGING index.
- When TABLESPACE clause is omitted, then it is set to the tablespace of the existing index.

<a id="01d8a5e75f7994d5"></a>
### Description

- Dropping the index fragmentation
    - The fragmentation may occur on the index page, when DML is frequently performed in the index. If the tree becomes too big comparing to the valid data, then the index volume becomes larger and the performance is degraded. In this case, rebuilding the index can solve the index fragmentation issue so that the index volume is reduced and the index performance is recovered.
- Altering the tablespace in the index
    - The tablespace in the previously created index can be altered.
    - However, LOGGING should be set properly according to whether the tablespace is TEMPORARY or not.
- Altering LOGGING setting in the index 
    - The data tablespace should be set in TABLESPACE option to switch to the LOGGING index.
    - The temporary tablespace or the nologging tablespace should be set in TABLESPACE option to switch to the NOLOGGING index.

<a id="178333dd76c39447"></a>
### Examples

The following is an example of altering the index logging setting and the tablespace.

```
gsql> SELECT INDEX_NAME, TABLESPACE_NAME FROM INDEXES AS IDX, TABLESPACES AS TBS WHERE IDX.TABLESPACE_ID = TBS.TABLESPACE_ID AND IDX.INDEX_NAME = 'T1X';

INDEX_NAME TABLESPACE_NAME
---------- ---------------
T1X        MEM_TEMP_TBS   

1 row selected.

gsql> ALTER INDEX T1X REBUILD TABLESPACE MEM_DATA_TBS;

SELECT INDEX_NAME, TABLESPACE_NAME FROM INDEXES AS IDX, TABLESPACES AS TBS WHERE IDX.TABLESPACE_ID = TBS.TABLESPACE_ID AND IDX.INDEX_NAME = 'T1X';

INDEX_NAME TABLESPACE_NAME
---------- ---------------
T1X        MEM_DATA_TBS   

1 row selected.
```

<a id="158340121ed4dfc1"></a>
### Compatibility

The SQL standard does not cover the concepts of the index.

<a id="be624b9bda92c677"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](19-sql-references-c-g.md#d54e994b20c1da1b)
- [ALTER INDEX](#48553e0933068af5)
- [DROP INDEX](19-sql-references-c-g.md#fcb6f064d90f791d)

<a id="a7fb743218a1f203"></a>
## ALTER INDEX name RENAME TO

<a id="7882969a0c530f89"></a>
### Function

It alters the index name.

<a id="1f34bd87b541d1c7"></a>
### Syntax

```
<rename index statement> ::=
    ALTER INDEX index_name
        RENAME TO new_index_name
    ;
```

<a id="4cdb87e803848b47"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename index statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="3c76f0706fd794a4"></a>
### Syntax Rules and Parameters

<a id="68c57e0fcadd9126"></a>
#### index_name

It is the name of the target index.  
The schema name can not be described and it has the same schema name as same as that of the existing index.

<a id="dbbf92d2c014ac28"></a>
#### new_index_name

It is the name of the new index, and it should be a unique index name within the schema.

<a id="b483987054b195dc"></a>
### Description

Refer to the syntax rules of each statement.

<a id="ed7d010c2955adc6"></a>
### Examples

The following is an example of altering the index name.

```
gSQL> ALTER INDEX t1_idx1 RENAME TO idx_t1_id;

Index altered.
```

<a id="63499a5a74b4a6be"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="e6e5d1bf7f7612fb"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](19-sql-references-c-g.md#d54e994b20c1da1b)
- [ALTER INDEX](#48553e0933068af5)
- [DROP INDEX](19-sql-references-c-g.md#fcb6f064d90f791d)

<a id="15c9d7666e8ad651"></a>
## ALTER INDEX name STORAGE

<a id="e2546e822e8b9512"></a>
### Function

It alters the physical attributes of the index.

<a id="ff4746b330c97c15"></a>
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

<a id="f6f2e1299f9b82b1"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter index physical attribute statement&gt;.

- The owner of that index 
- The owner of the table to which the index belongs
- CONTROL TABLE ON TABLE for the table to which the index belongs.
- (ALTER INDEX or CONTROL SCHEMA) ON SCHEMA for the schema to which the index belongs
- ALTER ANY INDEX ON DATABASE

<a id="079fa84bf3e003eb"></a>
### Syntax Rules and Parameters

<a id="c6a437ccf6f40333"></a>
#### index_name

It is the target index name.

<a id="495c79d244cc0593"></a>
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

<a id="57b07be952122916"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of physical storage space which is initially allocated when creating the index.
        - This size is aligned to the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually operated as 8192 bytes.)
        - The size (aligned to the EXTENT size of TABLESPACE) should be equal to or bigger than MINEXTENTS, or it should be equal to or less than MAXEXTENTS.
        - It is applied only when the index bottom-up build.
    - The minimum value is 1, and the maximum value depends on the system environment.

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

- MINSIZE integer
    - Definition
        - It is the minimum space size of the index.
        - The value should smaller than or equal to MAXSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it is specified to the size of two EXTENT.

- MAXSIZE integer
    - Definition
        - It is the maximum space size of the index.
        - The value should be equal to or bigger than MINSIZE.
    - This size is aligned to the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If it is omitted, the default value is EXTENT size * 2147483647(The maximum positive integer of INT32).

<a id="670c0d9d54be677d"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="ec651287d165aa4e"></a>
### Description

Refer to the syntax rules of each statement.

<a id="d34cebb011d046dc"></a>
### Examples

The following is an example of altering the physical attributes of the index.

```
gSQL> ALTER INDEX idx_t1_id PCTFREE 10 INITRANS 4 MAXTRANS 8;

Index altered.
```

<a id="b82fdb423b2a3ee7"></a>
### Compatibility

The SQL standard does not define the concepts of the index.

<a id="a7b1b6aee689b0f9"></a>
### For More Information

Refer to the followings.

- [CREATE INDEX](19-sql-references-c-g.md#d54e994b20c1da1b)
- [ALTER INDEX](#48553e0933068af5)
- [DROP INDEX](19-sql-references-c-g.md#fcb6f064d90f791d)

<a id="328cee336239afe4"></a>
## ALTER PROFILE

<a id="5fe5e561c7aab500"></a>
### Function

It alters the password management method.

<a id="8cded532232ab389"></a>
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

<a id="e361949ea8938f53"></a>
### Invocation and Access Rules

ALTER PROFILE ON DATABASE privilege is required to perform &lt;alter profile statement&gt;.

<a id="1a3403a77ea1b1e3"></a>
### Syntax Rules and Parameters

<a id="8217b00424246a72"></a>
#### profile_name

It is a profile name to be altered.

<a id="d8046a15c0cdf0ef"></a>
#### FAILED_LOGIN_ATTEMPTS

It sets the number of consecutive login attempts allowed to fail.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="08bd4fdda2d41853"></a>
#### PASSWORD_LOCK_TIME

It sets an account lockout duration (day) after the consecutive login failures.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="0915893dc68a427b"></a>
#### PASSWORD_LIFE_TIME

It sets the password lifetime (day).  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="2a1dce34462f1900"></a>
#### PASSWORD_GRACE_TIME

It sets a password expiration grace period when log in after PASSWORD_LIFE_TIME.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="eb4743af08c2a495"></a>
#### PASSWORD_REUSE_MAX

It specifies the number of the recent passwords which can not be reused when a user wants to reuse the old password.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="565b53c604feda0b"></a>
#### PASSWORD_REUSE_TIME

It specifies the duration which the password can not be reused when a user wants to reuse the old password.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="ce7ccdfb0259e475"></a>
#### PASSWORD_VERIFY_FUNCTION

It sets the password complexity verification method.  
For more information, refer to [CREATE PROFILE](19-sql-references-c-g.md#fa2854762beb7024).

<a id="7c84ad964426cb7c"></a>
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

<a id="b71b5a55c73911a7"></a>
### Compatibility

The SQL standard does not define the concepts of the profile.

<a id="6c418e074be9047e"></a>
### For More Information

Refer to [DROP PROFILE](19-sql-references-c-g.md#235532c683a06591).

<a id="c19ab51ee6e2aea4"></a>
## ALTER SEQUENCE

<a id="fc9febceb7295bce"></a>
### Function

It alters the sequence.

<a id="6b30a39607f9aeac"></a>
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

<a id="b5f7eec22f58a5c8"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter sequence generator statement&gt;.

- The owner of that sequence 
- (ALTER SEQUENCE or CONTROL SCHEMA) ON SCHEMA for the schema to which the sequence belongs
- ALTER ANY SEQUENCE ON DATABASE

<a id="df87aa26ffba3fb7"></a>
### Syntax Rules and Parameters

<a id="4f5686419eedaf18"></a>
#### sequence_name

It is the sequence name to be altered.  
It can define schema to which the sequence belongs such as schema_name.sequence_name and if schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="a70516d3b0723faa"></a>
#### &lt;alter sequence generator restart option&gt;

It sets NEXT VALUE of the sequence.  
However, it does not change the value of START WITH which is defined in [CREATE SEQUENCE](19-sql-references-c-g.md#11cfe1f314df4ce6) statement.

- RESTART 
    - If the value is not specified, the value of START WITH defined in &lt;sequence generator definition&gt; is set as the next value of the sequence.
- RESTART WITH integer 
    - It sets an integer value as the next value of the sequence.
    - The integer value should be between MINVALUE and MAXVALUE.

If &lt;alter sequence generator restart option&gt; clause is not specified, it changes the sequence attributes based on the current sequence value.

<a id="464ae7b3141470f6"></a>
#### &lt;sequence generator increment by option&gt;

It changes the interval of the sequence number.  
The constraints and characteristics are as follows.

- A positive or negative value can be used, but 0 can not be used.
- The absolute value of the interval should be smaller than the difference between MINVALUE and MAXVALUE.
- If it is a positive value, it an ascending sequence. If it is a negative value, it is a descending sequence.

<a id="3ac1e57e3269ae83"></a>
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

<a id="a8ed0a6d57216af7"></a>
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

<a id="ab4897eb298cdbc7"></a>
#### &lt;sequence generator cycle option&gt;

It changes whether to continue generating a value when the sequence value becomes the maximum or minimum value.

- CYCLE 
    - If an ascending sequence becomes the maximum value, it generates the value again from the minimum value.
    - If a descending sequence becomes the minimum value, it generates the value again from the maximum value.
- NO CYCLE | NOCYCLE 
    - It can not generate the value sequence when it becomes the maximum value or the minimum value.
    - NO CYCLE (SQL standard) and NOCYCLE are the reserved words with the same meaning, and either of them can be used.

<a id="94d82b87488a91b8"></a>
#### &lt;sequence generator cache option&gt;

For quick access of a sequence, it defines the number of sequence values to be pre-loaded on the memory.  
When restarting the database, the sequence value loaded on the memory is lost, and it starts from the value after loading.

- CACHE integer 
    - The CACHE value should be equal to or bigger than 2.
    - If CYCLE exists, the CACHE value should not be bigger than the length of CYCLE.
        - The length of CYCLE: CEIL(MAXVALUE - MINVALUE) / ABS(INCREMENT) 
- NO CACHE | NOCACHE 
    - It does not pre-load the sequence value in memory.

<a id="5f362735855b5dbe"></a>
### Description

It can not change START WITH which is one of the sequence attributes defined in [CREATE SEQUENCE](19-sql-references-c-g.md#11cfe1f314df4ce6) statement. To change START WITH attribute, it should be re-created by performing [CREATE SEQUENCE](19-sql-references-c-g.md#11cfe1f314df4ce6) statement after performing [DROP SEQUENCE](19-sql-references-c-g.md#61c1cea96080ef41) statement.

<a id="9be7c25493a98fdb"></a>
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

<a id="8c0e143bdff0b29c"></a>
### Compatibility

The SQL standard does not define CACHE/ NO CACHE statement.

**SQL standard compatibility**

<a id="6a5c9566172e34b5"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| T176 | Sequence generator support | O |
| T177 | Sequence generator support: simple restart option | O |

<a id="72c3cbda0b351d18"></a>
### For More Information

Refer to the followings.

- [CREATE SEQUENCE](19-sql-references-c-g.md#11cfe1f314df4ce6)
- [DROP SEQUENCE](19-sql-references-c-g.md#61c1cea96080ef41)

<a id="66cbf9bec6135a60"></a>
## ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

<a id="453951eaa7220cbf"></a>
### Function

It returns all segments which were caught to be reused in a session to tablespaces.

<a id="f36b36f9ad094701"></a>
### Syntax

```
<alter session cleanup global temporary segment pool statement> ::=
    ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL
    ;
```

<a id="0115c8627d9f25fe"></a>
### Description

It cleans up only the segments of a segment cache in the performed session.

<a id="4896e84e088b1578"></a>
### Examples

The following is an example of cleaning up the segment cache of the session.

```
gSQL> ALTER SESSION CLEANUP GLOBAL TEMPORARY SEGMENT POOL;

Session altered.
```

<a id="ce981d1647295ad7"></a>
### Compatibility

The SQL standard does not define the concepts of the segment cache of a global temporary table and a global temporary index.

<a id="826ec95204771bbe"></a>
### For More Information

Refer to [Global Temporary Table](13-sql-objects.md#85749c383118bd40).

<a id="9478b0e9e0d1d5e2"></a>
## ALTER SESSION SET property_name

<a id="63626bfc6059a037"></a>
### Function

It sets the property value of the session.

<a id="a5b748a6f1a8cec1"></a>
### Syntax

```
<alter session set statement> ::=
    ALTER SESSION SET <property name> { = <property value> | TO DEFAULT }
    ;
```

<a id="56fe27c12cab7e87"></a>
### Syntax Rules and Parameters

<a id="8993492e59de378a"></a>
#### &lt;property name&gt;

It is the property name to be set.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#5d474603dd66e8e7) in an administration manual.

<a id="ff3fbcd4624b6e14"></a>
#### &lt;property value&gt;

It is the property value to be set.

<a id="eecb95b76f370ebb"></a>
#### TO DEFAULT

It sets the session property value as a system property value.

<a id="0a2d825df7ad25d7"></a>
### Description

For more information about property, refer to [Server Property](../part-02-administration-manual/10-server-property.md#5d474603dd66e8e7) in an administration manual.

<a id="6e313255e58b16b8"></a>
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

<a id="4920642ca264533e"></a>
### Compatibility

The SQL standard does not define the concepts of the session property.

<a id="f1ce091f2f4edd91"></a>
### For More Information

Refer to [ALTER SESSION SET property_name](#9478b0e9e0d1d5e2).

<a id="22987caefdea5e8d"></a>
## ALTER SYSTEM CHECKPOINT

<a id="20ce75c4d5829fe1"></a>
### Function

It performs CHECKPOINT.

<a id="cd7e317254ccd8c6"></a>
### Syntax

```
<alter system checkpoint statement> ::=
    ALTER SYSTEM CHECKPOINT
    [ AT <domain name> ]
    ;
```

<a id="44fcc1253c0c0edd"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system checkpoint statement&gt;.

<a id="4c42af2a14fa24ff"></a>
### Syntax Rules and Parameters

<a id="140e741a9691e28b"></a>
#### &lt;alter system checkpoint statement&gt;

CHECKPOINT is an operation to ensure that all altered data by the committed transactions are written to disk.

- The database should be in OPEN phase. 
- The database should be in TDS mode.
- When a full backup is in progress, the altered pages are not recorded in the data file, but only the REDO logs and control files are written to the disk. If the server is abnormally terminated in this situation, a media recovery should be performed.

<a id="009b886adb49a9de"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="5c31ed0af644d068"></a>
### Description

The checkpoint operation records all changes by the committed transactions to disk, so it enables a rapid recovery at system error.

<a id="e5396e4b73b1bc27"></a>
### Example

The following is an example of performing CHECKPOINT.

```
ALTER SYSTEM CHECKPOINT;
```

<a id="69b507629d6aa985"></a>
### Compatibility

The SQL standard does not define the concepts of CHECKPOINT.

<a id="4d5d1798edbb3e18"></a>
## ALTER SYSTEM CLEANUP BUFFER_CACHE

<a id="7b0d117c6eca8fdb"></a>
### Function

It clears all buffer pages which can be free from the buffer cache.

<a id="770456f2eb70c76d"></a>
### Syntax

```
<alter system cleanup buffer_cache statement> ::=
    ALTER SYSTEM CLEANUP BUFFER_CACHE
    [ AT <domain name> ]
    ;
```

<a id="88e1e8a285e0fff2"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system cleanup buffer_cache statement&gt;.

<a id="f70e1342581de80b"></a>
### Syntax Rules and Parameters

<a id="c4a7b349fb5f894d"></a>
#### &lt;alter system cleanup buffer_cache statement&gt;

Syntax rules and parameters do not exist for &lt;alter system cleanup buffer_cache statement&gt;.

<a id="365c8c7d67b3e931"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="cd025683d4c91225"></a>
### Description

It flushes and frees all free buffer pages cached in the buffer.

> It should be used to clear the buffer cache before the performance measuring.  
> If it is used on the operating server, then it could have fatal effect for the performance.

<a id="55529f4e0e6d8d4d"></a>
### Example

The following is an example of performing CLEANUP BUFFER_CACHE.

```
ALTER SYSTEM CLEANUP BUFFER_CACHE;
```

<a id="4b59df074f0dfaab"></a>
### Compatibility

The SQL standard does not define the concepts of CLEANUP BUFFER_CACHE.

<a id="2001d11aba7e2fa7"></a>
## ALTER SYSTEM CLEANUP PLAN

<a id="4b5b9b1975931f30"></a>
### Function

It cleans up all SQL plans.

<a id="d715ac23cb954d1e"></a>
### Syntax

```
<alter system cleanup plan statement> ::=
    ALTER SYSTEM CLEANUP PLAN
    [ AT <domain name> ]
    ;
```

<a id="8d0bcc39c7db418e"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system cleanup plan statement&gt;.

<a id="9d6dd2a8c099c8c7"></a>
### Syntax Rules and Parameters

<a id="625af4bf08012cb0"></a>
#### &lt;alter system cleanup plan statement&gt;

There is not any syntax rules or parameters for &lt;alter system cleanup plan statement&gt;.

<a id="946835536491e4b4"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="9c18a38c3e95d5f9"></a>
### Description

It cleans up all of the cached SQL plan. However, the plan whose V$SQL CACHE.REF COUNT is bigger than 0 (the plan referenced by the prepared statement) is excluded from cleanup.

<a id="fabe87f8712ff158"></a>
### Examples

The following is an example of executing CLEANUP PLAN.

```
ALTER SYSTEM CLEANUP PLAN;
```

<a id="f974f5a844903abb"></a>
### Compatibility

The SQL standard does not define the concepts of CLEANUP PLAN.

<a id="b6ab36baa68456a8"></a>
## ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER

<a id="8b5f0bb7c70a9030"></a>
### Function

It specifies an irrecoverable cluster member.

<a id="076cc694d888844a"></a>
### Syntax

```
<alter system irrecoverable cluster member statement> ::=
    ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER <domain name>
    ;
```

<a id="ad1eeb07d6e4cc09"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system irrecoverable cluster member statement&gt;.

<a id="e679d22170ee4b14"></a>
### Syntax Rules and Parameters

<a id="975e6601bff100b8"></a>
#### &lt;alter system irrecoverable cluster member statement&gt;

There is not any syntax rules or parameters for &lt;alter system irrecoverable cluster member statement&gt;.

<a id="bba6d05d816de031"></a>
#### &lt;domain name&gt;

It is a name of an irrecoverable member.   
It is not allowed to specify all members in a group as an irrecoverable member.

<a id="cf977f5463894ef8"></a>
### Description

It is used to restart the system excluding the corresponding member if the cluster failed to restart due to an irrecoverable member. The corresponding member should be dropped by using [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#63f811ebc15cf737) after the system succeeded to restart.

<a id="e5fe9660b10d6ce8"></a>
### Examples

The following is an example of executing IRRECOVERABLE CLUSTER MEMBER.

```
gSQL> ALTER SYSTEM IRRECOVERABLE CLUSTER MEMBER g1n1;
```

<a id="e3ddad0ac47b0401"></a>
### Compatibility

The SQL standard does not define the concepts of IRRECOVERABLE CLUSTER MEMBER.

<a id="389b6cddb5c2c458"></a>
## ALTER SYSTEM JOIN DATABASE

<a id="7fafbf6e9209d8bc"></a>
### Function

It includes a specific inactive cluster member in a cluster system again.

<a id="6d641fa01f2d4207"></a>
### Syntax

```
<alter system join database statement> ::=
    ALTER SYSTEM JOIN DATABASE 
    ;
```

<a id="60d6f551d59ada55"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter system join database statement&gt;.

<a id="8c0f68995e0cd168"></a>
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

<a id="219b8a286d897664"></a>
### Examples

```
gSQL> ALTER SYSTEM JOIN DATABASE;
```

<a id="5e60275467dcc130"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="c2aa50d25b4f66bd"></a>
### For More Information

Refer to [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](#63f811ebc15cf737).

<a id="38e96a269836e35e"></a>
## ALTER SYSTEM [KILL | DISCONNECT] SESSION

<a id="eff4cc70f8395051"></a>
### Function

It terminates a session.

<a id="77a6c60953bdd930"></a>
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

<a id="d5b1881c9ef6bfb3"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system end session statement&gt;.

<a id="f0d1180640181db1"></a>
### Syntax Rules and Parameters

<a id="cff75760fad6ac21"></a>
#### &lt;member_position&gt;

It is a member position of a session which is a disconnect/kill target in a cluster environment.

<a id="45e9a2b7158f06e9"></a>
#### &lt;session_id&gt;

It is the session ID.

<a id="89fd5f7e4b9fa5b5"></a>
#### &lt;serial#&gt;

It is the SERIAL NUMBER of the session.

<a id="4e942881958295c3"></a>
#### &lt;disconnect_option&gt;

- POST_TRANSACTION: The session is terminated after completion of the transaction.
- IMMEDIATE: The session is immediately terminated without waiting for the completion of the transaction.

If &lt;disconnect_option&gt; is not used, then it is operated in IMMEDIATE.

<a id="29491e114ccde207"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="731cf2a23203accc"></a>
### Description

DISCONNECT SESSION can specify the options such as POST TRANSACTION and IMMEDIATE.   
POST TRANSACTION terminates the session after the currently running transaction is completed. IMMEDIATE terminates the session after immediately cleaning up the currently running transaction.

KILL SESSION terminates the abnormal session which remains on the system without its process.

<a id="67c7ae44e0e191c1"></a>
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

<a id="212400e68e58a435"></a>
### Compatibility

The SQL standard does not define it.

<a id="54011886eee6d8dd"></a>
## ALTER SYSTEM {MOUNT | OPEN} DATABASE

<a id="5441073bbf28cf9c"></a>
### Function

It mounts the database on system, or alters the database to the state which is available for the service.

<a id="739a3ce9ad52fc44"></a>
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

<a id="6c0af36b4dfb3486"></a>
### Invocation and Access Rules

ADMINISTRATION ON DATABASE privilege is required to perform &lt;alter system database statement&gt;.

<a id="1f2d0db468926aaf"></a>
### Syntax Rules and Parameters

<a id="717219b07521d995"></a>
#### &lt;alter system database clause&gt;

- MOUNT DATATABASE
    - It mounts the database on the system.
- OPEN DATABASE
    - It changes the database to the state which is available for the service.

<a id="3ae924d8763d2d11"></a>
#### &lt;open database option&gt;

- READ ONLY / READ WRITE
    - It specifies the read/write mode and drives the database.
    - If it is omitted, it is driven in READ WRITE.
- RESETLOGS / NORESETLOGS
    - It determines whether to keep the online redo logs after recovering the database.
    - NORESETLOGS maintains the existing redo log, but RESETLOGS initializes it.
    - RESETLOGS should be specified when the database is incompletely recovered.
    - If it is omitted, NORESETLOGS is specified by default.

<a id="90e3afc9227de54b"></a>
#### &lt;database_scope&gt;

- LOCAL
    - It starts up the LOCAL server to the OPEN phase.
- GLOBAL
    - It starts up the GLOBAL server, the entire server, to the OPEN phase.
- If it is omitted in a cluster environment, it starts up the GLOBAL server.

<a id="31c3f5c5c201e64c"></a>
### Examples

The following is an example of driving the database in read only.

```
ALTER SYSTEM OPEN DATABASE READ ONLY;
```

The following is an example of driving the database in read/write, and initializing the online redo logs.

```
ALTER SYSTEM OPEN DATABASE READ WRITE RESETLOGS;
```

<a id="d1497997a3406dff"></a>
### Compatibility

The SQL standard does not define the concepts of MOUNT or OPEN in the database.

<a id="60a4c8395dbdcc2f"></a>
### For More Information

Refer to [ALTER DATABASE RECOVER](#3fa18e0049bd27dd).

<a id="0d864b8eb7156cfd"></a>
## ALTER SYSTEM RECONNECT GLOBAL CONNECTION

<a id="244ff3045d7a651a"></a>
### Function

It determines whether to reconnect to the session which is connected in GLOBAL CONNECTION form.

<a id="fcfe07e6776138cf"></a>
### Syntax

```
<alter system reconnect global connection statement> ::=
    ALTER SYSTEM RECONNECT GLOBAL CONNECTION
    ;
```

<a id="46c3db4217cb0239"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system reconnect global connection statement&gt;.

<a id="61ed99f292d22739"></a>
### Description

Whether the GLOBAL CONNECTION client reconnects is determined by comparing SCN of a system object acquired from a server at the first connection and SCN of current server system object. This statement leads the client to reconnect by increasing SCN of the system object.

The client does not necessarily reconnect immediately after this statement is performed. The client reconnects by comparing SCN when the client executes a command in a server, and it does not try to reconnect if connections to all members from a client are valid.

<a id="2174492f98d35ff3"></a>
### Examples

The following is an example of executing the statement.

```
gSQL> ALTER SYSTEM RECONNECT GLOBAL CONNECTION;

System altered.
```

<a id="80078c9a0135ec28"></a>
### Compatibility

The SQL standard does not define the concepts of GLOBAL CONNECTION.

<a id="8c8b1bcebb15cd54"></a>
## ALTER SYSTEM RESET property_name

<a id="f8d8057ab53c0cd8"></a>
### Function

It removes a property value from the property file.

<a id="9a5ca0e2a4c0be71"></a>
### Syntax

```
<alter system reset statement> ::=
    ALTER SYSTEM { RESET | UNSET } <property name>
        [ SCOPE = { FILE | SPFILE } ]
        [ AT <domain name>]
    ;
```

<a id="66431825e0c78e6c"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system reset statement&gt;.

<a id="3397653cc145892c"></a>
### Syntax Rules and Parameters

<a id="8f6fd9ca4857a9c1"></a>
#### { RESET | UNSET }

RESET and UNSET are the reserved words with the same meaning, so either of them can be used.

<a id="1c8fbad13c9844c3"></a>
#### &lt;property name&gt;

It is the property name to be removed.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#5d474603dd66e8e7) in an administration manual.

<a id="31777bbe7f8fa008"></a>
#### [ SCOPE = { FILE | SPFILE } ]

It removes the property from a property file, so only SCOPE=FILE/SPFILE can be used.

- SCOPE = FILE 
    - FILE and SPFILE are the reserved words with the same meaning, so either of them can be used. 
    - A property is removed from FILE, and is not applied to the current state.
    - When restarting the database, the changes are applied.

If SCOPE clause is not specified, the default value is SCOPE = FILE.

<a id="0472ba8f2caebbbf"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="d0b477a0bb9e7cae"></a>
### Description

If a property is altered by using SCOPE=FILE/SPFILE, the updated property value is stored in the property file, and it is applied when restarting the database.

When executing RESET, the updated property value is removed from the property file and the default value is used when restarting the database.

<a id="df0d990c6235c71b"></a>
### Examples

The following is an example of altering the property by using SCOPE=FILE.

```
gSQL> ALTER SYSTEM SET PROCESS_MAX_COUNT=128 SCOPE=FILE;

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

gSQL> ALTER SYSTEM UNSET PROCESS_MAX_COUNT;

System altered.
```

<a id="328f53ef1e6b90d1"></a>
### Compatibility

The SQL standard does not define the concepts of the system property.

<a id="da548c4270fd5d12"></a>
### For More Information

Refer to [ALTER SYSTEM SET property_name](#8524798b9d7f6a03).

<a id="8524798b9d7f6a03"></a>
## ALTER SYSTEM SET property_name

<a id="184c079ddeda3d46"></a>
### Function

It sets the system property value.

<a id="1fa78bc0ae9d79b2"></a>
### Syntax

```
<alter system set statement> ::=
    ALTER SYSTEM SET <property name> { = <property value> | TO DEFAULT }
        [ DEFERRED ]
        [ SCOPE = [ MEMORY | { FILE | SPFILE } | BOTH ] ]
    [AT <domain name>]
    ;
```

<a id="ae312c57821eef11"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system set statement&gt;.

<a id="75904cfa74aae23c"></a>
### Syntax Rules and Parameters

<a id="5fd4ce3fe63f0c7c"></a>
#### &lt;property name&gt;

It is the property name to be set.  
For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#5d474603dd66e8e7) in an administration manual.

<a id="6cb5c6e01789a3a0"></a>
#### &lt;property value&gt;

It is the property value to be set.

<a id="ae45e93dd47fee7f"></a>
#### TO DEFAULT

It sets the system property value as the initial value of system driving.

<a id="5f0f6843632ecfd8"></a>
#### [ DEFERRED ]

It defines the point of time to apply the altered property.

- DEFERRED 
    - It does not effect the current SESSION, but it is applied to the newly generated SESSION.
    - It can be applied when ISSYS_MODIFIABL property value is IMMEDIATE/DEFERRED. It should be explicitly specified. 
    - It is not applicable when the SYS_MODIFIABLE property value is FALSE.

If SYS_MODIFIABLE property value is IMMEDIATE, and DEFERRED is not explicitly specified, then it is immediately applied to all sessions.

<a id="2e5581575205d607"></a>
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

<a id="0415c05035cf95c5"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="79417781f81183e0"></a>
### Description

For more information, refer to [Server Property](../part-02-administration-manual/10-server-property.md#5d474603dd66e8e7) in an administration manual.

<a id="1aa321f3b8dec471"></a>
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

<a id="15228d2cad50ac72"></a>
### Compatibility

The SQL standard does not define the concepts of the system property.

<a id="a310db917332c1fc"></a>
### For More Information

Refer to [ALTER SYSTEM RESET property_name](#8c8b1bcebb15cd54).

<a id="cad24f3df58ddc03"></a>
## ALTER SYSTEM SWITCH LOGFILE

<a id="997a9e9e922c7c44"></a>
### Function

It alters the log files in CURRENT state to ACTIVE state in database.

<a id="22f1a724abf23ba5"></a>
### Syntax

```
<alter system switch logfile statement> ::=
    ALTER SYSTEM SWITCH LOGFILE
    [ AT <domain name> ]
    ;
```

<a id="44af78a4f0b5cfd3"></a>
### Invocation and Access Rules

ALTER SYSTEM ON DATABASE privilege is required to perform &lt;alter system switch logfile statement&gt;.

<a id="836df0fbd82d62db"></a>
### Syntax Rules and Parameters

<a id="69245e55cbe43577"></a>
#### &lt;alter system switch logfile statement&gt;

The database should be in MOUNT or OPEN phase.

<a id="8ad1b771d83ed41e"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="a6413f2ae4599993"></a>
### Description

Basically, if the log file in CURRENT state is filled, the log switch automatically occurs. That statement is used to forcibly execute log switch in special circumstances.

<a id="8b92f46a01c0999a"></a>
### Example

```
ALTER SYSTEM SWITCH LOGFILE;
```

<a id="420893c02916161d"></a>
### Compatibility

The SQL standard does not define the concepts of the LOGFILE.

<a id="06f5647fbcbfd2d9"></a>
### For More Information

Refer to [ALTER SYSTEM {MOUNT | OPEN} DATABASE](#54011886eee6d8dd).

<a id="8d2122be368c72be"></a>
## ALTER TABLE

<a id="cee041144ec37c86"></a>
### Function

It alters the table definition.

<a id="9b16032ea63db49c"></a>
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
    | <rename table constraint statement>
    | <add table supplemental log statement>
    | <drop table supplemental log statement>
    | <rebalance statement>
    | <move shard statement>
    | <merge shards statement>
    | <split shard statement>
    | <rename shard statement>
    | <read { only | write } statement>
    ;
```

<a id="542843c2077ed9cc"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for the table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="4615e2e6bbdf9c1f"></a>
### Syntax Rules and Parameters

<a id="622b2a176e756785"></a>
#### &lt;alter table physical attribute statement&gt;

It alters physical attributes of a table.  
For more information, refer to [ALTER TABLE name STORAGE](#71c41b55b638caef).

<a id="c9c8c9e0435da8f5"></a>
#### &lt;rename table statement&gt;

It renames the table.  
For more information, refer to [ALTER TABLE name RENAME TO](#b4f871c5e3e593ce).

<a id="04114c3fb48a45d6"></a>
#### &lt;add column definition&gt;

It adds columns to the table.  
For more information, refer to [ALTER TABLE name ADD COLUMN](#9e97702c72f6ffbe).

<a id="ae65f774c46e4cdc"></a>
#### &lt;drop column definition&gt;

It drops a column from the table.  
For more information, refer to [ALTER TABLE name SET UNUSED COLUMN](#9e4d9a9c6969a42e).

<a id="35dc3977ab87c68a"></a>
#### &lt;alter column definition&gt;

It alters the column definition in the table.  
For more information, refer to [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4).

<a id="eaefdb0ad0b5d770"></a>
#### &lt;rename column statement&gt;

It renames the column in the table.  
For more information, refer to [ALTER TABLE name RENAME COLUMN](#fc0bfc6460f62c7c).

<a id="578a087dbcc6ae46"></a>
#### &lt;add table constraint definition&gt;

It adds constraints to the table.  
For more information, refer to [ALTER TABLE name ADD CONSTRAINT](#44f4ae4ef49e26ef).

<a id="52345156a08117a4"></a>
#### &lt;drop table constraint definition&gt;

It drops the constraints of the table.  
For more information, refer to [ALTER TABLE name DROP CONSTRAINT](#5dc66d99183e1a21).

<a id="70586fd87d15f651"></a>
#### &lt;alter table constraint definition&gt;

It alters the constraints of the table.  
For more information, refer to [ALTER TABLE name ALTER CONSTRAINT](#72353def66d0d589).

<a id="7d8718b42f39c641"></a>
#### &lt;rename table constraint statement&gt;

It renames the constraints of the table.  
For more information, refer to [ALTER TABLE name RENAME CONSTRAINT](#c40e89f12d33bad6).

<a id="38cdbd789dd00468"></a>
#### &lt;add table supplemental log statement&gt;

It sets to add information to the redo log when the data is altered in the table.  
For more information, refer to  [ALTER TABLE name ADD SUPPLEMENTAL LOG](#3b4859472868cccf).

<a id="361a0476221303ee"></a>
#### &lt;drop table supplemental log statement&gt;

It sets not to add information to the redo log when the data is altered in the table.   
For more information, refer to [ALTER TABLE name DROP SUPPLEMENTAL LOG](#a9449ce3dc7482ff) .

<a id="f66fab116a426848"></a>
#### &lt;rebalance statement&gt;

It restores consistency by rebalancing the shard of the table or by synchronizing the broken shard in a cluster environment.   
For more information, refer to [ALTER TABLE name REBALANCE](#f7d09b5058d6293a).

<a id="817b73a84c880e1b"></a>
#### &lt;move shard statement&gt;

It rebalances a specific shard of a table on a specific cluster group in a cluster environment.  
For more information, refer to [ALTER TABLE name MOVE SHARD](#ce282f55c7c9877b) .

<a id="77925611593c35f7"></a>
#### &lt;merge shards statement&gt;

It merges specific shards in a table in a cluster environment, then rebalances them.  
For more information, refer to  [ALTER TABLE name MERGE SHARDS](#2e12e025295d1acb).

<a id="51e23063082bbd23"></a>
#### &lt;split shard statement&gt;

It rebalances a specific shard of a table on a specific cluster group by splitting the shard in a cluster environment.  
For more information, refer to [ALTER TABLE name SPLIT SHARD](#942e6b10f519010e).

<a id="45051bb56575c2f7"></a>
#### &lt;rename shard statement&gt;

It renames a specific shard of a table in cluster environment.   
For more information, refer to [ALTER TABLE name RENAME SHARD](#2640bc3e8d297ee4).

<a id="12202cce565b7884"></a>
#### &lt;read { only | write } statement&gt;

It sets READ ( only | write } to a table.  
For more information, refer to [ALTER TABLE name READ { ONLY | WRITE }](#35ffe6d74914caca).

<a id="d64a0a937ba79e9a"></a>
### Description

For more information, refer to the description of each detailed statement.

<a id="feba71e077379135"></a>
### Example

Refer to the examples of each detailed statement.

<a id="da2a08d58df30ebd"></a>
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

<a id="9e97702c72f6ffbe"></a>
## ALTER TABLE name ADD COLUMN

<a id="944d852c3ff07f8d"></a>
### Function

It adds a column to the table.

<a id="c4a793ab7135be3e"></a>
### Syntax

```
<add column definition> ::=
      ALTER TABLE table_name ADD [ COLUMN ] <column definition>
    | ALTER TABLE table_name ADD [ COLUMN ] ( <column definition> [, ...] )
    ;
```

<a id="99086c70826db7d9"></a>
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

<a id="8f905d6fc1022394"></a>
### Syntax Rules and Parameters

<a id="747c664facc18910"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="0fc1bbffabb946ee"></a>
#### ADD [ COLUMN ]

The reserved word COLUMN can be omitted.

<a id="fa8403aff90a7c20"></a>
#### &lt;column definition&gt;

It defines the column to be added. For more information, refer to [&lt;column definition&gt;](19-sql-references-c-g.md#3c38e65e466d65e2) clause of [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d) statement.  
There should not be columns with the same name in a table.

If DEFAULT clause is specified when defining the column, the default value of all rows are stored in the added column.  
If &lt;identity column specification&gt; clause is specified when defining the column, each automatically generated value of all rows is stored in the added column.  
If NOT NULL constraint is specified when defining the column, the table should be empty or it should be specified together with DEFAULT or &lt;identity column specification&gt; clause.

<a id="0ea391095f922be4"></a>
#### ( &lt;column definition&gt; [, ...] )

It adds multiple columns.  
It lists multiple &lt;column definition&gt; inside the parentheses.

<a id="1a73a00c62fd1b19"></a>
### Description

The added column is positioned at the end of the existing columns.  
When specifying DEFAULT or &lt;identity column specification&gt; clause, the processing time is increased in proportion to the number of the rows in the table.

<a id="2bcbc52ce971952d"></a>
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

<a id="ae69660ac72f9a5b"></a>
### Compatibility

The SQL standard does not define of adding multiple column definitions.

<a id="8ea22eaa2501963e"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name SET UNUSED COLUMN](#9e4d9a9c6969a42e)
- [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4)
- [ALTER TABLE name RENAME COLUMN](#fc0bfc6460f62c7c)

<a id="44f4ae4ef49e26ef"></a>
## ALTER TABLE name ADD CONSTRAINT

<a id="6256544a862d16e3"></a>
### Function

It adds a table constraint.

<a id="8edc155d50187973"></a>
### Syntax

```
<add table constraint definition> ::=
    ALTER TABLE table_name 
        ADD <table constraint definition>
    ;
```

<a id="d5ab3cf8d10d3330"></a>
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

<a id="bc02ac9a857c2008"></a>
### Syntax Rules and Parameters

<a id="daa46c1e131f661f"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="a9fdefc4f52d0b5c"></a>
#### &lt;table constraint definition&gt;

It defines the constraint to be added.  
NOT NULL constraint can not be added by using ALTER TABLE .. ADD CONSTRAINT statement, and it can be defined by using [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4) statement as follows.

```
ALTER TABLE t1 ALTER COLUMN c1 SET NOT NULL;
```

For more information, refer to [&lt;table constraint definition&gt;](19-sql-references-c-g.md#2f2688dbb20b72dc) clause of [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d) statement.

<a id="a55fb198a375e24e"></a>
### Description

When adding the key constraints such as primary key, unique key, the index is automatically created for them.

<a id="5ecb68032e15dec5"></a>
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

<a id="a5607103501a205e"></a>
### Compatibility

**SQL standard compatibility**

<a id="9621c0bb35e9d288"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="f75a87ae88cd5ead"></a>
### For More Information

Refer to the followings.

- [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d)
- [CREATE INDEX](19-sql-references-c-g.md#d54e994b20c1da1b)
- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name DROP CONSTRAINT](#5dc66d99183e1a21)

<a id="35909868f7689aed"></a>
## ALTER TABLE name ADD GLOBAL SECONDARY INDEX

<a id="99dee43ba8d8dcfd"></a>
### Function

It creates a global secondary index in a table.

<a id="f824408b70ff28d0"></a>
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

<a id="75e4dfb6bff67d32"></a>
### Invocation and Access Rules

&lt;alter table add global secondary index definition&gt; can be defined in a cluster system, and a user should satisfy the following conditions.

- At least one of the following privileges for a table in which the index is to be created is required.
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs.
    - ALTER ANY TABLE ON DATABASE

- At least one of the following privileges for a tablespace in which the index is to be created is required.
    - CREATE OBJECT ON TABLESPACE for that tablespace
    - USAGE TABLESPACE ON DATABASE

<a id="a4c7e3d67b372d78"></a>
### Syntax Rules and Parameters

<a id="995b15f317b0580d"></a>
#### table_name

It is the name of a table in which the index is to be created.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="f66f36011d92d0db"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of the index.

- PCTFREE integer
    - Definition
        - The reserved space to adjust the frequency of page splits caused by key insertion within the page
        - This is applied only during the index bottom-up build.
    - The value can range from 0 to 99.
    - If omitted, the value set in the DEFAULT_INDEX_PCTFREE property will be used by default.

- INITRANS integer
    - Definition
        - The initial number of transactions that can simultaneously access the page
        - If the number of users accessing the index is small, INITRANS is set to a low value. If the number of users simultaneously accessing the index is large, INITRANS is set to a high value.
        - If necessary, INITRANS will be automatically increased up to the specified MAXTRANS.
    - The value can range from 1 to 32.
    - If omitted, the default value will be 4.

- MAXTRANS integer
    - Definition
        - The maximum number of transactions that can simultaneously access the page
    - The value can range from 1 to 32.
    - If omitted, the default value will be 8.

<a id="3849869d1ec9e352"></a>
#### &lt;segment attr clause&gt;

It specifies the information about the storage space where the index will be stored.

- INITIAL integer
    - Definition
        - It specifies the size of the physical storage space initially allocated when creating the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually treated as 8192 bytes.)
        - The size (aligned with the EXTENT size of the TABLESPACE) must be greater than or equal to MINEXTENTS, or less than or equal to MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be one EXTENT size of the TABLESPACE to which the index belongs.

- NEXT integer
    - Definition
        - It specifies the size of the physical storage space to be allocated when adding space to the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually treated as 8192 bytes.)
        - The allocation of space for NEXT works as follows, depending on the remaining available space in the index (calculated by subtracting the amount of space currently used from the MAXEXTENTS size).  
      - If the remaining space size is 0, space cannot be extended.  
      - If the remaining space size is greater than 0 but smaller than NEXT, the space will be allocated as large as the remaining space.  
      - If the remaining space size is greater than NEXT, the space will be allocated as large as the NEXT size.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be one EXTENT size of the TABLESPACE to which the index belongs.

- MINSIZE integer
    - Definition
        - It specifies the minimum space size for the index.
        - The value must be less than or equal to MAXSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it will be set to the size of two EXTENT.
    - If omitted, the default value will be the size of two EXTENT.

- MAXSIZE integer
    - Definition
        - It specifies the maximum space size for the index.
        - The value must be greater than or equal to MINSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1 and the maximum value depends on the system environment.
    - If omitted, the default value will be the EXTENT size * 2147483647 (The maximum positive integer of INT32).

<a id="8cd4a4e281a1903b"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0f935cbf1f00e3b6"></a>
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

<a id="d1c22c2952694c18"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be stored.

- If it specifies tablespace_name
    - tablespace_name should be a data tablespace to switch to the LOGGING index. 
    - tablespace_name should be a temporary tablespace or a nologging tablespace to switch to the NOLOGGING index

- If it omits TABLESPACE clause, then it follows the settings of the existing index.

<a id="f05eb8d151d63476"></a>
### Description

A non-deterministic query requires the global secondary index. LOGGING index and NOLOGGING index have the following trade-offs.

- LOGGING index
    - Advantage: It does not separately build an index because the index is automatically restored by using the log when starting up the system.
    - Disadvantage: A disk I/O occur because the changes on the index is recorded on the log when altering the row.
- NOLOGGING index
    - Advantage: A disk I/O does not occur for the changes on the index when altering the row.
    - Disadvantage: It automatically rebuilds the index when starting up the system because the log information of the index does not exist.

<a id="8905aac1e5bc5662"></a>
### Examples

The following is an example of adding a global secondary index to the table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a global secondary index as a logging index on the tablespace USER_DATA_TBS of table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX LOGGING TABLESPACE USER_DATA_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

The following is an example of creating a global secondary index as a nologging index on the tablespace USER_TEMP_TBS of table T1.

```
gSQL> ALTER TABLE T1 ADD GLOBAL SECONDARY INDEX NOLOGGING TABLESPACE USER_TEMP_TBS;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="023babc01f992e84"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="be19f13a029945c9"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#6a4810ca2588350f)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#60f7aeca8914e724)
- [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d)

<a id="3b4859472868cccf"></a>
## ALTER TABLE name ADD SUPPLEMENTAL LOG

<a id="3c61cfcde32e1d38"></a>
### Function

If the primary key exists in the table when table data is altered, it sets to add the primary key value to redo log.

<a id="93376abaf5fb35b4"></a>
### Syntax

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="c4e5865580716739"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;add table supplemental log statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="0418e4d187bea1c4"></a>
### Syntax Rules and Parameters

<a id="e9a04c55e82871c7"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

Even when the primary key does not exist in the table, the statement can be executed.

<a id="169cdff643d13654"></a>
### Description

It additionally records SUPPLEMENTAL LOG when executing UPDATE/DELETE on the corresponding TABLE. The recorded SUPPLEMENTAL LOG is used to analyze logs or tools such as CDC.

To record SUPPLEMENTAL LOG of every TABLE, set the property as *SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY = YES*.

<a id="41636ce41533f06a"></a>
### Example

The following is an example of setting to additionally add a primary key value to the redo log when changing the data in the table.

```
gSQL> ALTER TABLE t1 ADD SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="65001a7ef6d611eb"></a>
### Compatibility

The SQL standard does not cover &lt;add table supplemental log statement&gt;.

<a id="536328aa83f47127"></a>
### For More Information

Refer to [ALTER TABLE name DROP SUPPLEMENTAL LOG](#a9449ce3dc7482ff).

<a id="22fe007bdb09fad4"></a>
## ALTER TABLE name ALTER COLUMN

<a id="ef2124d8f7df725c"></a>
### Function

It alters the column definition.

<a id="38aa20cea3ed95dc"></a>
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

<a id="cd436cada36e2945"></a>
### Invocation and Access Rules

One of the following privileges is required to performing &lt;alter column definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="a1daa0ddaeaca592"></a>
### Syntax Rules and Parameters

<a id="7999f338cea7f5c9"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="6071d521c814a764"></a>
#### ALTER [ COLUMN ]

The reserved word COLUMN can be omitted.

<a id="563a70ed4fd71c15"></a>
#### column_name

It is the column name to be altered.

<a id="cc8c1fe41655e48f"></a>
#### &lt;set column default clause&gt;

It sets the default value of the column.  
It should not be an identity column.

The default value set when using the DEFAULT clause is used in INSERT statement later.

The data type of DEFAULT expression should be compatible with the data type of the column.  
If the data type is not compatible or the expression is not valid, an error occurs.

For more information, refer to [&lt;default clause&gt;](19-sql-references-c-g.md#ac3e45cb05f9c6b5) of [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d) statement.

<a id="7626075f5014db81"></a>
#### &lt;drop column default clause&gt;

It drops the default value of the column.  
It should not be an identity column.  
If the default value is dropped, NULL is set when using DEFAULT clause in INSERT statement.

<a id="88cb5ebc6152bc22"></a>
#### &lt;set column not null clause&gt;

- SET [CONSTRAINT constraint_name] NOT NULL [ &lt;constraint characteristics&gt; ]
    - It sets NOT NULL constraint on the column.
    - NULL is not allowed as the column value.
    - NULL should not exist in the column.

- If [CONSTRAINT constraint_name] is omitted, the constraint name is automatically given. 
- If &lt;constraint characteristics&gt; is omitted, it has NOT DEFERRABLE INITIALLY IMMEDIATE property. 
- The Identity column can not have DEFERRABLE property.

For more information about the DEFERRABLE constraint, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

<a id="bac0502adb0405aa"></a>
#### &lt;drop column not null clause&gt;

- DROP NOT NULL
    - It drops NOT NULL constraint from the column.

<a id="19a6d7b58dfd96ca"></a>
#### &lt;alter column data type clause&gt;

- SET DATA TYPE &lt;data type&gt;
    - It changes the data type of the column.

> SET DATA TYPE is a DDL statement which is automatically committed.

The type conversion can be executed among the same family, and it should satisfy the following conditions.

**Conversion of character string type**

<a id="d8e12bf914c877c2"></a>
| from \ to | CHAR(n) | VARHCAR(n) | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR(m) | X | X | X |
| VARCHAR(m) | X | n >= m | X |
| LONG VARCHAR | X | X | O |

The conversion of char length unit should satisfy the following condition.

**Conversion of character length unit**

<a id="60fbe56b51b7aff0"></a>
| from \ to | OCTETS | CHARACTERS |
| --- | --- | --- |
| OCTETS | O | O |
| CHARACTERS | X | O |

**Conversion of binary string type**

<a id="b1c47e0959d0eb3c"></a>
| from \ to | BINARY(n) | VARBINARY(n) | LONG VARBINARY |
| --- | --- | --- | --- |
| BINARY(m) | X | X | X |
| VARBINARY(m) | X | n >= m | X |
| LONG VARBINARY | X | X | O |

**Conversion of numeric type**

<a id="471932d7a44ae8b3"></a>
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

<a id="504aeedd4890f68a"></a>
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

<a id="48bceb378431a0c0"></a>
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

<a id="36796b56a90f76a3"></a>
| from \ to | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| NATIVE_SMALLINT | O | X | X | X | X |
| NATIVE_INTEGER | X | O | X | X | X |
| NATIVE_BIGINT | X | X | O | X | X |
| NATIVE_REAL | X | X | X | O | X |
| NATIVE_DOUBLE | X | X | X | X | O |

**Conversion of boolean type**

<a id="62ff5f1fd8ced66a"></a>
| from \ to | BOOLEAN |
| --- | --- |
| BOOLEAN | O |

**Conversion of date/time type (TZ: WITH TIME ZONE)**

<a id="2398a59a4343f63d"></a>
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

<a id="322d3b36e8576469"></a>
| from \ to | YEAR(q) | MONTH(q) | YEAR(q) TO MONTH |
| --- | --- | --- | --- |
| YEAR(p) | q >= p | X | X |
| MONTH(p) | X | q >= p | X |
| YEAR(p) TO MONTH | X | X | q >= p |

**Type conversion of INTERVAL DAY TO TIME family (If p,q are omitted, then it is 2.) (If f,g are omitted, then it is 6.)**

<a id="2a529c4814931251"></a>
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

<a id="ffa66200b4f1a0da"></a>
| from \ to | ROWID |
| --- | --- |
| ROWID | O |

<a id="8958bfba7dd2d6f1"></a>
#### &lt;alter identity column specification&gt;

It alters the identity property of the column.  
The column should be an identity column.

- SET GENERATED [ ALWAYS | BY DEFAULT ]
    - It changes the method of generating the identity column.
    - For more information, refer to [&lt;identity column specification&gt;](19-sql-references-c-g.md#7072b711465819ee) of [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d) statement. 
- &lt;alter sequence generator restart option&gt; 
    - It changes NEXT VALUE of the identity column.
    - For more information, refer to [&lt;alter sequence generator restart option&gt;](#a70516d3b0723faa) clause of [ALTER SEQUENCE](#c19ab51ee6e2aea4) statement. 
- &lt;basic sequence generator option&gt; 
    - It changes the property of the identity column. 
    - In SQL standard, it is defined to be described in the form of SET &lt;basic sequence generator option&gt;, but it can be omitted. 
    - For more information, refer to [ALTER SEQUENCE](#c19ab51ee6e2aea4) statement.

<a id="3528e68a3dd3235b"></a>
#### &lt;drop identity property clause&gt;

It drops the identity property of the column.  
The column should be the identity column.

<a id="5363df2e6c7c1eed"></a>
### Description

SET NOT NULL clause requires the time for checking null in proportion to the number of table rows.

The following columns do not allow NULL values. In other words, even if DROP NOT NULL clause is performed, NULL is not allowed in the following cases.

- A column which includes NOT NULL constraint
- A column which is included in primary key constraint
- An identity column

The change of the default value using SET DEFAULT clause and the change of the identity property using &lt;alter identity column specification&gt; clause, is applied to INSERT or UPDATE statement which is performed later.

<a id="4331de06e0c8f6ad"></a>
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

<a id="53fa6a3b3fe4f0e9"></a>
### Compatibility

**The SQL satndards compatibility**

<a id="12a86dc37f727bc8"></a>
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

<a id="10e26e8c20244b92"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name ADD COLUMN](#9e97702c72f6ffbe)
- [ALTER TABLE name SET UNUSED COLUMN](#9e4d9a9c6969a42e)
- [ALTER TABLE name RENAME COLUMN](#fc0bfc6460f62c7c)

<a id="72353def66d0d589"></a>
## ALTER TABLE name ALTER CONSTRAINT

<a id="8ffba9f7df56d130"></a>
### Function

It alters the characteristics of the table constraint.

<a id="274f09dd225e2436"></a>
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

<a id="b38545eddac814ee"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table constraint definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

> Cluster does not support the deferrable constraints.

<a id="d67f5fcbd6ba7076"></a>
### Syntax Rules and Parameters

<a id="1a0bd99c53eecabb"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="f04cce625bf40614"></a>
#### &lt;constraint object&gt;

The constraint to be altered is specified as follows.

- CONSTRAINT constraint_name
    - The constraint name to be altered.
- PRIMARY KEY 
    - PRIMARY KEY constraint of the table
- UNIQUE( column [,...] ) 
    - UNIQUE constraint which satisfies the column list.

<a id="0ad0c80aac408875"></a>
#### DEFERRABLE | NOT DEFERRABLE

It alters whether the constraint state is deferrable.

- DEFERRABLE
    - The constraint is altered to be deferrable. 
- NOT DEFERRABLE 
    - The constraint is altered not to be deferrable.

For more information about the deferrable constraints, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

<a id="3b5abe8ff4e1241a"></a>
#### INITIALLY IMMEDIATE | INITIALLY DEFERRED

It alters an initial value of the check point for the constraint.

- INITIALLY IMMEDIATE 
    - It checks the constraints at the time of DML.
- INITIALLY DEFERRED 
    - It checks the constraints at the time of COMMIT.

The constraints defined as NOT DEFERRABLE can not be altered to INITIALLY DEFERRED.

<a id="5c0c467ca2759646"></a>
### Description

For more information about the deferrable constraints, refer to [SET CONSTRAINTS](20-sql-references-h-z.md#0465632935b629b3).

<a id="b2f45f44e90f56cc"></a>
### Example

The following is an example that the constraint t1_uk is set as deferrable and its checking time is set as DEFERRED.

```
gSQL> ALTER TABLE t1 ALTER CONSTRAINT t1_uk DEFERRABLE INITIALLY DEFERRED;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="d33a84b94982ac5c"></a>
### Compatibility

The SQL standard does not define the following clauses.

- ALTER PRIMARY KEY clause
- ALTER UNIQUE(column [,...]) clause

**SQL standard compatibility**

<a id="38ef304751f36a6b"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F492 | Optional table constraint enforcement | X |

<a id="60f7aeca8914e724"></a>
## ALTER TABLE name ALTER GLOBAL SECONDARY INDEX

<a id="b87d64ce95d420e3"></a>
### Function

It alters the physical attributes of the global secondary index in the table.

<a id="0f858774bdd441e6"></a>
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

<a id="e625ad6680d99120"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table alter global secondary index storage statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="5c0c1772020c096a"></a>
### Syntax Rules and Parameters

<a id="63c3e4fc4fcd5acb"></a>
#### table_name

It is the name of a table in which the index is to be created.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="e67f2a3d0e3bde8c"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of the index.

- PCTFREE integer
    - Definition
        - The reserved space to adjust the frequency of page splits caused by key insertion within the page
    - The value can range from 0 to 99.
    - If omitted, the existing index settings will be used.

- INITRANS integer
    - Definition
        - The initial number of transactions that can simultaneously access the page
        - If the number of users accessing the index is small, INITRANS is set to a low value. If the number of users simultaneously accessing the index is large, INITRANS is set to a high value.
        - If necessary, INITRANS is automatically increased up to the specified MAXTRANS.
    - The value can range from 1 to 32.
    - If omitted, the existing index settings will be used.

- MAXTRANS integer
    - Definition
        - The maximum number of transactions that can simultaneously access the page
    - The value can range from 1 to 32.
    - If omitted, the existing index settings will be used.

<a id="a1ec2407aa70351a"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of the physical storage space initially allocated when creating the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually treated as 8192 bytes.)
        - The size (aligned with the EXTENT size of the TABLESPACE) must be greater than or equal to MINEXTENTS, or less than or equal to MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

- NEXT integer
    - Definition
        - It specifies the size of the physical storage space to be allocated when adding space to the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually treated as 8192 bytes.)
        - The allocation of space for NEXT works as follows, depending on the remaining available space in the index (calculated by subtracting the amount of space currently used from the MAXEXTENTS size).  
      - If the remaining space size is 0, space cannot be extended.  
      - If the remaining space size is greater than 0 but smaller than NEXT, the space will be allocated as large as the remaining space.  
      - If the remaining space size is greater than NEXT, the space will be allocated as large as the NEXT size.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

- MINSIZE integer
    - Definition
        - It specifies the minimum space size for the index.
        - The value must be less than or equal to MAXSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it will be set to the size of two EXTENT.
    - If omitted, the default value will be the one set in the existing index.

- MAXSIZE integer
    - Definition
        - It specifies the maximum space size for the index.
        - The value must be greater than or equal to MINSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

<a id="86476095efb8f658"></a>
#### &lt;size clause&gt;

It specifies the file size in byte. (If it is omitted, the default unit is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="e9819b7432feccf6"></a>
### Description

A global secondary index is required to enquire a non-deterministic query.

<a id="2374f7aa50e5f7d1"></a>
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

<a id="9dec02f865a76030"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="4f4acdcc76549cdc"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#35909868f7689aed)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#6a4810ca2588350f)

<a id="5dc66d99183e1a21"></a>
## ALTER TABLE name DROP CONSTRAINT

<a id="4b8a1e7e61c4b17e"></a>
### Function

It drops a table constraint.

<a id="0d7d57fcd7ea20ce"></a>
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

<a id="9020b2701bc7d704"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table constraint definition&gt;.

- The owner of that constraint
- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="df984d8079ebad23"></a>
### Syntax Rules and Parameters

<a id="3f035ad385bedab7"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="e08ef73c16dbf4cd"></a>
#### CONSTRAINT constraint_name

It is the constraint name to be dropped.

<a id="092ffbf92087651e"></a>
#### PRIMARY KEY

It is the primary key constraint for the table.

<a id="e276526f1a7b0c6d"></a>
#### UNIQUE( column_name [, ...] )

It is the unique constraint for the columns.

<a id="1b8f9bb51523c663"></a>
#### &lt;drop behavior&gt;

When it is omitted, the default value is RESTRICT.  
Currently, RESTRICT/CASCADE is operated in the same way.

<a id="66d59525a466ccfc"></a>
### Description

[&lt;drop column not null clause&gt;](#bac0502adb0405aa) of [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4) is used to drop NOT NULL constraint without using the constraint name.

<a id="96e9c0c115c5d4db"></a>
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

<a id="1b1f857ca9fe358b"></a>
### Compatibility

The SQL standard does not define the following clauses.

- DROP PRIMARY KEY 
- DROP UNIQUE ( column_name [, ...] ) 
- CASCADE CONSTRAINTS

**SQL standard compatibility**

<a id="0499f7a834210cf9"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F381 | Extended schema manipulation | O |

<a id="906137b309e19488"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name ADD CONSTRAINT](#44f4ae4ef49e26ef)
- [DROP INDEX](19-sql-references-c-g.md#fcb6f064d90f791d)

<a id="6a4810ca2588350f"></a>
## ALTER TABLE name DROP GLOBAL SECONDARY INDEX

<a id="c64f8ebcf13ec128"></a>
### Function

It drops a global secondary index from the table.

<a id="f1952c8406ef7def"></a>
### Syntax

```
<alter table drop global secondary index definition> ::=
    ALTER TABLE table_name 
        DROP GLOBAL SECONDARY INDEX
    ;
```

<a id="25871dd48c3d0015"></a>
### Invocation and Access Rules

&lt;alter table drop global secondary index definition&gt; statement can be defined in a cluster system, and the user should satisfy the following conditions.

- The following privilege for the table from which the index is to be dropped is required 
    - (ALTER or CONTROL TABLE) ON TABLE for that table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE

<a id="25eed1533a1eb638"></a>
### Syntax Rules and Parameters

<a id="11124a0466cb2780"></a>
#### table_name

It is the name of a table from which the index is to be dropped.

<a id="0d2ebbc834631e9a"></a>
### Description

A global secondary index is required to enquire a non-deterministic query.

<a id="897b50f9e60a38c0"></a>
### Examples

It drops a global secondary index from the table T1.

```
gSQL> ALTER TABLE T1 DROP GLOBAL SECONDARY INDEX;

Table altered.

gSQL> COMMIT;

Commit complete.
```

<a id="f3192372f8667902"></a>
### Compatibility

The SQL standard does not define the concepts of the global secondary index.

<a id="3f4adabf40792f76"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#35909868f7689aed)
- [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](#60f7aeca8914e724)

<a id="a9449ce3dc7482ff"></a>
## ALTER TABLE name DROP SUPPLEMENTAL LOG

<a id="865fe44e738b5062"></a>
### Function

It sets not to leave the primary key information on the redo log when changing the data in the table.

<a id="52883ae8f390e1a1"></a>
### Syntax

```
<add table supplemental log statement> ::=
    ALTER TABLE table_name 
        DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS
    ;
```

<a id="9d26fde1465760f2"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop table supplemental log statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="6764e70506c190ed"></a>
### Syntax Rules and Parameters

<a id="72753650e0698e5e"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
It should have been set by using [ALTER TABLE name ADD SUPPLEMENTAL LOG](#3b4859472868cccf) statement.

<a id="0f9b0e0752dceff9"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="b66e542018eb1a1a"></a>
### Example

The following is an example of setting not to leave the primary key information on the redo log when changing the data in the table.

```
gSQL> ALTER TABLE t1 DROP SUPPLEMENTAL LOG DATA ( PRIMARY KEY ) COLUMNS;

Table altered.
```

<a id="bbbb8e553c140e53"></a>
### Compatibility

The SQL standard does not cover &lt;drop table supplemental log statement&gt;.

<a id="2e12e025295d1acb"></a>
## ALTER TABLE name MERGE SHARDS

<a id="9d3d790fa7055266"></a>
### Function

It merges specific shards in a table in a cluster environment, and rebalances them.

<a id="16f7ebd305fcf1be"></a>
### Syntax

```
<alter table merge shards statement> ::=
    ALTER TABLE table_name MERGE SHARDS <source shard list> 
       INTO dest_shard_name [ <dest shard placement> ]
    ;

<source shard list> ::= 
    source_shard_name [, ...]
  | start_shard_name TO end_shard_name

<dest shard placement> ::=
    AT CLUSTER GROUP dest_group_name
```

<a id="5dd288dfafbfa529"></a>
### Invocation and Access Rules

It can be performed in the cluster system.

One of the following privileges is required to perform &lt;alter table merge shards statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="6e707bbce4b235b5"></a>
### Syntax Rules and Parameters

<a id="cdb727cfe6a32318"></a>
#### table_name

It is the name of a table.  
It can define a schema to which the table belongs such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when the table is a cluster-specific, and a list shard or a range shard.

<a id="6f78954139110bfd"></a>
#### &lt;source shard list&gt;

It is the list of original shards to be merged.  
The shard specified by a list should exist in the table.

<a id="053ff1179beaf42d"></a>
#### source_shard_name

It is the name of an original shard to be merged.  
If the shard does not exist in the table, then the statement can not be performed.

<a id="756c1f42945ea78a"></a>
#### start_shard_name

It is the name of the first shard in the range of merging.   
It is used only in a range shard.

<a id="f693dc510a99e217"></a>
#### end_shard_name

It is the name of the last shard in the range of merging.   
It is used only in a range shard.

<a id="c20f1b881fa54483"></a>
#### dest_shard_name

It is the name of a target shard.

<a id="2ba1a11ee19aefa4"></a>
#### &lt;dest shard placement&gt;

It is the name of a cluster group in which the target shard is to be placed.  
If the corresponding clause is omitted, *dest_shard_name* should be included in &lt;source shard list&gt;.

<a id="a3a0cd235a84ecfe"></a>
### Description

It merges specific shards in a specific table, then places them in an arbitrary cluster group.

- It can not be performed in a standalone database.
- It can not be performed in a hash sharded table nor in a cloned table.
- It can not be performed in a table created as cluster wide.
- DML can not be performed for source shards while merging is in progress. 
- If it is a range shard, the beginning and ending original shards to be merged can be defined.
- Original shards to be merged can be listed in a range shard or a list shard.  
  In this case, shards listed in a range shard should be the neighboring shard.

The following is an error which occurred when merging shards which are not neighboring in a range sharded table in a way of listing.

```
CREATE TABLE t1( i1 INTEGER ) 
    SHARDING BY RANGE (i1)
    SHARD shard1 VALUES LESS THAN ( 200 )      AT CLUSTER GROUP G1,
    SHARD shard2 VALUES LESS THAN ( 400 )      AT CLUSTER GROUP G2,
    SHARD shard3 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP G3
;

Table created.

ALTER TABLE t1 MERGE SHARDS shard1, shard3 INTO shard4 AT CLUSTER GROUP G2;

ERR-42000(16488): shards being merged are not adjacent : 
ALTER TABLE t1 MERGE SHARDS shard1, shard3 INTO shard4 AT CLUSTER GROUP G2
                                    *
ERROR at line 1:
```

<a id="f5654bc20cdab7f2"></a>
### Examples

The following is an example of merging shards in a way of listing.

```
gSQL> ALTER TABLE t1 MERGE SHARDS shard1, shard2, shard3 INTO shard4 AT CLUSTER GROUP G2;

Table altered
```

The following is an example of merging shards in a way of ranging.

```
gSQL> ALTER TABLE t1 MERGE SHARDS shard1 TO shard3 INTO shard4 AT CLUSTER GROUP G2;

Table altered
```

<a id="b05f3d3e541320ac"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="e13603af1a518848"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name MOVE SHARD](#ce282f55c7c9877b)
- [ALTER TABLE name SPLIT SHARD](#942e6b10f519010e)

<a id="ce282f55c7c9877b"></a>
## ALTER TABLE name MOVE SHARD

<a id="1a56528871bf8e8c"></a>
### Function

It rebalances a specific shard of a table, or the entire shard in a specific cluster group to a specific cluster group.

<a id="d6270dc5c66e9870"></a>
### Syntax

```
<alter table move shard statement> ::=
    ALTER TABLE table_name MOVE SHARD
        { shard_name_list | FROM CLUSTER GROUP src_cluster_group }
        TO CLUSTER GROUP dest_cluster_group [ ONLINE | OFFLINE ]
    ;
```

<a id="48d9530a49b4cdee"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table move shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="2b401c5a469e4edc"></a>
### Syntax Rules and Parameters

<a id="7747b8d179c01fd9"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster group specific table.

<a id="c0a4172364765081"></a>
#### shard_name_list

It is the shard name list to be rebalanced.  
If the shard does not exist in that table, then the statement can not be performed.

<a id="54617f38e4453804"></a>
#### src_cluster_group

It is the name of a specific cluster group to be rebalanced.

<a id="e7aff9213b690e3c"></a>
#### dest_cluster_group

It is the name of a target cluster group on which the shard of the table is to be rebalanced.  
If the shard of the table already exists in the specified cluster group, the statement cannot be performed.

<a id="2205a91064e48033"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="0b4fa66d777b895d"></a>
### Description

It rebalances a specific shard of the table from a specific cluster group to another cluster group.

To drop a specific cluster group, rebalance the shard of the table then  perform the [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13) statement.

To move shards of all tables from a specific cluster group to another cluster group, then perform the ALTER DATABASE MOVE SHARD FROM CLUSTER GROUP TO CLUSTER GROUP statement.

If it is a CLONED table or a CLUSTER WIDE table, then an error occurs and it fails.

<a id="fdacdb4c6dce39d4"></a>
### Examples

The following is an example of executing the &lt;alter table move shard statement&gt; statement.

```
gSQL> ALTER TABLE t1 MOVE SHARD shard1, shard2 TO CLUSTER GROUP g3;

Table altered.

gSQL> ALTER TABLE t1 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

Table altered.
```

The following is an example of which a CLONED table and a CLUSTER WIDE table fails to move shard.

```
gSQL> CREATE TABLE T1 ( C1 INTEGER ) SHARDING BY RANGE (C1)
         AT CLUSTER WIDE
         SHARD s1 VALUES LESS THAN (10),                                      
         SHARD s2 VALUES LESS THAN (MAXVALUE);

Table created.

gSQL> ALTER TABLE T1 MOVE SHARD s1 TO CLUSTER GROUP g2;

ERR-42000(16440): cannot execute on cluster wide sharded tables

gSQL> CREATE TABLE T2 ( C1 INTEGER ) CLONED AT CLUSTER GROUP g1, g2;

Table created.

gSQL> ALTER TABLE T2 MOVE SHARD FROM CLUSTER GROUP g1 TO CLUSTER GROUP g3;

ERR-42000(16437): cannot execute on cloned tables
```

<a id="3b8e9d4893716d20"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="e1a28950f6302b62"></a>
### For More Information

Refer to [ALTER DATABASE MOVE SHARD](#2539c44d7da42e34).

<a id="35ffe6d74914caca"></a>
## ALTER TABLE name READ { ONLY | WRITE }

<a id="0cf79337a9817dfc"></a>
### Function

It sets READ { ONLY | WRITE } in a table.

<a id="5cc9e469de84d869"></a>
### Syntax

```
<alter table read { only | write } statement> :==
     ALTER TABLE table_name
         READ { ONLY | WRITE }
     ;
```

<a id="769b5f3a0eb2b221"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table read { only | write } statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="fdaff7e7ef79169a"></a>
### Syntax Rules and Parameters

<a id="c9715c43a04d7747"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="ca7618296e5e3438"></a>
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

<a id="cd0ccaf3d91dca4e"></a>
### Examples

The following is an example of executing &lt;alter table read { only | write } statement&gt;.

```
gSQL> ALTER TABLE t1 READ ONLY;

Table altered.

gSQL> ALTER TABLE t1 READ WRITE;

Table altered.
```

<a id="4b7a96295e19eec8"></a>
### Compatibility

The SQL standard does not define &lt;alter table read { only | write } statement&gt;.

<a id="820793cf6b10bff4"></a>
### For More Information

Refer to [ALTER TABLE](#8d2122be368c72be).

<a id="f7d09b5058d6293a"></a>
## ALTER TABLE name REBALANCE

<a id="3af21de1b213ecb3"></a>
### Function

It rebalances the shard in a table.

<a id="4f67eb0e3451ac2e"></a>
### Syntax

```
<alter table rebalance statement> ::=
    ALTER TABLE table_name REBALANCE [ ONLINE | OFFLINE ]
    ;
```

<a id="8f3841f5ece375f2"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rebalance statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="6d504d965f7fea2d"></a>
### Syntax Rules and Parameters

<a id="3e6942e07574a784"></a>
#### table_name

It is the table name.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="608a52a818274cd7"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="78afac591c7e214e"></a>
### Description

It does not rebalance shards in a table when adding a cluster member or a cluster group by using the following statements.

- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#3f7a6957233a40f7)
- [ALTER CLUSTER GROUP name ADD MEMBER](#0a6879be2602f377)

To rebalance the shards of a table in the added cluster group and the cluster member, perform the &lt;alter table rebalance statement&gt; statement. The operation succeeds without a separate rebalancing if the shard of the table is already rebalanced.

To rebalance shards in all tables, perform the [ALTER DATABASE REBALANCE](#218ad4f730bea674) statement.

<a id="29061bf6b9f61a14"></a>
### Examples

The following is an example of executing the &lt;alter table rebalance statement&gt; statement.

```
gSQL> ALTER TABLE t1 REBALANCE;

Table altered.
```

<a id="9efeb69f2675c89a"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="f003b5733529d1e0"></a>
## ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list

<a id="229057b50e98f8c6"></a>
### Function

It rebalances the shard of the table not to include a shard in a specific cluster group.

<a id="3f7d2972f137e574"></a>
### Syntax

```
<alter table rebalance exclude cluster group statement> ::=
    ALTER TABLE table_name REBALANCE 
        EXCLUDE CLUSTER GROUP cluster_group_list [ ONLINE | OFFLINE ]
    ;
```

<a id="d0ab60a6a0ac43df"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rebalance exclude cluster group statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="4a4f8e97eac14d56"></a>
### Syntax Rules and Parameters

<a id="17a191738bf8a08a"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster-wide table.

<a id="ad234f20ea7d3d69"></a>
#### cluster_group_list

It is a list of the cluster group which does not include a shard of a table.  
If the cluster group to be excluded from the rebalancing is the entire group, the statement can not be performed.

<a id="7ac077c66dad47b8"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML when rebalancing table shard.

- ONLINE 
    - It allows INSERT, UPDATE, and DELETE. 
- OFFLINE 
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="fe00ec385006d42b"></a>
### Description

It excludes a specific cluster group and rebalances the shard of the table.  
If the shard of the table does not exist in that cluster group, the operation succeeds without a separate rebalancing.   
It rebalances the shard based on the cluster group in which the shard of the table is located.

To drop a specific cluster group, rebalance the shard of the table and perform  [DROP CLUSTER GROUP](19-sql-references-c-g.md#76a15fea6a02da13) statement.  
To rebalance the shard excluding a cluster group from all tables, perform the  [ALTER DATABASE REBALANCE EXCLUDE CLUSTER GROUP](#ddaf56ae2c345c2c) statement.

<a id="c7c428466b31c73e"></a>
### Examples

The following is an example of executing the &lt;alter table rebalance exclude cluster group statement&gt; statement.

```
gSQL> ALTER TABLE t1 REBALANCE EXCLUDE CLUSTER GROUP g3;

Table altered.
```

<a id="e8790d798dc4dc0a"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="3ddd26732c40c3bf"></a>
## ALTER TABLE name REBUILD GLOBAL SECONDARY INDEX

<a id="7de7ab1b441952ab"></a>
### Function

It rebuilds a global secondary index

<a id="f7042288d1b64def"></a>
### Syntax

```
<rebuild global secondary index statement> ::=
    ALTER TABLE table_name REBUILD GLOBAL SECONDARY INDEX
        [ ONLINE | OFFLINE ]
        [ <index attributes> [...] ]
        [ TABLESPACE tablespace_name ]
    ;

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

<a id="9c121b13a039b094"></a>
### Invocation and Access Rules

The user should satisfy the following conditions to perform &lt;rebuild global secondary index statement&gt;.

- One of the following privileges is required for the table on which the index is to be rebuilt.
    - (ALTER or CONTROL TABLE) ON TABLE for the table
    - (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
    - ALTER ANY TABLE ON DATABASE

- One of the following privileges is required for the tablespace on which the index is to be rebuilt.
    - CREATE OBJECT ON TABLESPACE for the tablespace
    - USAGE TABLESPACE ON DATABASE

<a id="be532f1b3cbf0c66"></a>
### Syntax Rules and Parameters

<a id="85b623e7e20e2883"></a>
#### table_name

It is the table name on which the index is to be rebuilt.   
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="e73c3d3d0f3ec253"></a>
#### [ ONLINE | OFFLINE ]

It determines whether to allow DML on the table when rebuilding the index.

- ONLINE
    - It allows INSERT, UPDATE, and DELETE.
- OFFLINE
    - It does not allow INSERT, UPDATE, DELETE.
- When it is omitted, the default value is ONLINE.

<a id="614e2488251ae23d"></a>
#### &lt;physical attribute clause&gt;

It defines the physical attribute information of an index.

- PCTFREE integer
    - Definition
        - The reserved space to adjust the frequency of page splits caused by key insertion within the page
    - It can use the value from 0 to 99.
    - If omitted, the default value will be the one set in the existing index.

- INITRANS integer
    - Definition
        - The initial number of transactions that can simultaneously access the page
        - If the number of users accessing the index is small, INITRANS is set to a low value. If the number of users simultaneously accessing the index is large, INITRANS is set to a high value.
        - If necessary, INITRANS will be automatically increased up to the specified MAXTRANS.
    - The value can range from 1 to 32.
    - If omitted, the default value will be the one set in the existing index.

- MAXTRANS integer
    - Definition
        - The maximum number of transactions that can simultaneously access the page
    - The value can range from 1 to 32.
    - If omitted, the default value will be the one set in the existing index.

<a id="aa33c0207bf90eb7"></a>
#### &lt;segment attr clause&gt;

It specifies the information for the index storage space.

- INITIAL integer
    - Definition
        - It specifies the size of the physical storage space initially allocated when creating the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'INITIAL 100' is actually treated as 8192 bytes.)
        - The size (aligned with the EXTENT size of the TABLESPACE) must be greater than or equal to MINEXTENTS, or less than or equal to MAXEXTENTS.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

- NEXT integer
    - Definition
        - It specifies the size of the physical storage space to be allocated when adding space to the index.
        - This size is aligned with the EXTENT size of the TABLESPACE to which the table belongs. (e.g. If the EXT size is 8192 bytes, 'NEXT 100' is actually treated as 8192 bytes.)
        - The allocation of space for NEXT works as follows, depending on the remaining available space in the index (calculated by subtracting the amount of space currently used from the MAXEXTENTS size).  
      - If the remaining space size is 0, space cannot be extended.  
      - If the remaining space size is greater than 0 but smaller than NEXT, the space will be allocated as large as the remaining space.  
      - If the remaining space size is greater than NEXT, the space will be allocated as large as the NEXT size.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

- MINSIZE integer
    - Definition
        - It specifies the minimum space size for the index.
        - The value must be less than or equal to MAXSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If it is smaller than the size of two EXTENT, it will be set to the size of two EXTENT.
    - If omitted, the default value will be the one set in the existing index.

- MAXSIZE integer
    - Definition
        - It specifies the maximum space size for the index.
        - The value must be greater than or equal to MINSIZE.
    - This size is aligned with the EXTENT size of the TABLESPACE to which the index belongs.
    - The minimum value is 1, and the maximum value depends on the system environment.
    - If omitted, the default value will be the one set in the existing index.

<a id="9214be907977bb45"></a>
#### &lt;size clause&gt;

It specifies the file size in bytes. (If the unit is omitted, the default value is bytes.)

- K: Kilobytes 
- M: Megabytes 
- G: Gigabytes 
- T: Terabytes

<a id="0c020700445fef1b"></a>
#### NOPARALLEL | PARALLEL [ integer ]

It specifies the number of threads to be used when rebuilding an index.

- NOPARALLEL 
    - It does not rebuild an index in parallel.
- PARALLEL [integer] 
    - It rebuilds an index in parallel.
    - If an integer is omitted or set as 0, then it follows INDEX_BUILD_PARALLEL_FACTOR property. 
    - The minimum value of an integer is 0 and the maximum value is 64. 
    - If the integer or the property value is 0, then the system determines the optimal value.
- If it is omitted, the default value is NOPARALLEL.

<a id="5437d0982f4cd893"></a>
#### TABLESPACE tablespace_name

It specifies the name of the tablespace in which the index is to be rebuilt.

- When it specifies tablespace_name
    - if tablespace_name is data tablespace, then it is rebuilt as a LOGGING index.
    - if tablespace_name is temporary tablespace or nologging tablespace, then it is rebuilt as a NOLOGGING index.
- When TABLESPACE clause is omitted, then it is set to the tablespace of the existing index.

<a id="aba4fc39343f1b73"></a>
### Description

- Dropping the index fragmentation
    - The fragmentation may occur on the index page, when update DML is frequently performed in the index. If the tree becomes too big comparing to the valid data, then the index volume becomes larger and the performance is degraded. In this case, rebuilding the index can solve the index fragmentation issue so that the index volume is reduced and the index performance is recovered.
- Altering the tablespace in the index
    - The tablespace in the previously created index can be altered.
    - However, LOGGING should be set properly according to whether the tablespace is TEMPORARY or not.
- Altering LOGGING setting in the index 
    - The LOGGING setting in the previously created index can be altered by using TABLESPACE option.
    - The data tablespace should be set in TABLESPACE option to switch to the LOGGING index.
    - The temporary tablespace or the nologging tablespace should be set in TABLESPACE option to switch to the NOLOGGING index.

<a id="628d89486a63c5cc"></a>
### Examples

Rebuild the global secondary index in the table T1.

```
gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX;
```

Alter the tablespace and logging settings of the global secondary index in the table T1.

```
gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX TABLESPACE MEM_DATA_TBS;

gSQL> ALTER TABLE T1 REBUILD GLOBAL SECONDARY INDEX TABLESPACE MEM_TEMP_TBS;
```

<a id="08221c2864277cc3"></a>
### Compatibility

The SQL standard does not cover the concepts of the global secondary index.

<a id="4b97db69ba60ec1f"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](#35909868f7689aed)
- [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](#6a4810ca2588350f)
- [ALTER INDEX name REBUILD](#0df5754f2a0050c1)

<a id="fc0bfc6460f62c7c"></a>
## ALTER TABLE name RENAME COLUMN

<a id="5d3d8c3ac35e5614"></a>
### Function

It renames the table column.

<a id="27c878a3fea45589"></a>
### Syntax

```
<rename column statement> ::=
    ALTER TABLE table_name 
        RENAME COLUMN old_column_name TO new_column_name
    ;
```

<a id="4eaf39c5a37a14e9"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename column statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="b842572f35a86354"></a>
### Syntax Rules and Parameters

<a id="1e93a89359dee2d8"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="94436a0cff12e339"></a>
#### old_column_name

It is the old column name to be altered.

<a id="177af3c77dd229ae"></a>
#### new_column_name

It is the new column name to be altered.  
The same column name should not exist in a table.

<a id="12c726fa71205420"></a>
### Description

Even when the column name is altered it does not require the object change such as index, constraint which is generated based on the previous column.

<a id="ad79aeb5323aad75"></a>
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

<a id="5fa9aa20a9d42936"></a>
### Compatibility

The SQL standard does not define &lt;rename column statement&gt;.

<a id="ea105bdcdab6c533"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name ADD COLUMN](#9e97702c72f6ffbe)
- [ALTER TABLE name SET UNUSED COLUMN](#9e4d9a9c6969a42e)
- [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4)

<a id="c40e89f12d33bad6"></a>
## ALTER TABLE name RENAME CONSTRAINT

<a id="638aff6d4aa7fed7"></a>
### Function

It renames the table constraints.

<a id="c0de08dea4c772d4"></a>
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

<a id="c3fbfc9929a08730"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename table constraint statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="f108fa1cd7f01b2d"></a>
### Syntax Rules and Parameters

<a id="584ac143f403a48d"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="3ba5cc9583b56a81"></a>
#### &lt;constraint object&gt;

The existing name of the constraint to be altered is specified as follows.

- CONSTRAINT constraint_name
    - The constraint name to be altered
- PRIMARY KEY
    - PRIMARY KEY constraint of the table
- UNIQUE( column [,...] )
    - UNIQUE constraint which satisfies the column list

<a id="8375f378aba79458"></a>
#### new_column_name

It is the new name of a constraint to be altered.

<a id="b06209ec02739dec"></a>
### Description

The index name which was automatically created with a key constraint such as primary key, unique key is not altered. Use [ALTER INDEX name RENAME TO](#a7fb743218a1f203) statement to rename the index.

<a id="71a9da2630580abb"></a>
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

<a id="9883725d77c16065"></a>
### Compatibility

The SQL standard does not define the &lt;rename table constraint statement&gt; statement.

<a id="f4a6d07d183553b9"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name ADD CONSTRAINT](#44f4ae4ef49e26ef)
- [ALTER TABLE name DROP CONSTRAINT](#5dc66d99183e1a21)
- [ALTER TABLE name ALTER CONSTRAINT](#72353def66d0d589)

<a id="2640bc3e8d297ee4"></a>
## ALTER TABLE name RENAME SHARD

<a id="220beb40ef057586"></a>
### Function

It renames a specific shard of a table in cluster environment.

<a id="7c8cdeac6c8baa77"></a>
### Syntax

```
<alter table rename shard statement> ::=
    ALTER TABLE table_name 
        RENAME SHARD shard_name TO new_shard_name
    ;
```

<a id="c1a3122f3843b7da"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table rename shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="10641638fba76d84"></a>
### Syntax Rules and Parameters

<a id="c1c60d2b341c9fa3"></a>
#### table_name

It is the table name to be altered.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="b970d550cbd7cf68"></a>
#### shard_name

It is the existing name of a shard to be altered.  
If the shard does not exist in that table, then the statement can not be performed.

<a id="0a0a0a448dd5d28d"></a>
#### new_shard_name

It is the new name of a shard to be altered.   
The same shard name should not exist in the table.

<a id="033ec81269eb7062"></a>
### Description

It alters the name of a specific shard of a hash, a range, or a list table. This statement can not be performed for a cloned table.

<a id="ffa059be6f132dd3"></a>
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

<a id="0913e1acbfddd0e6"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="12e7a87758eb89ce"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name MOVE SHARD](#ce282f55c7c9877b)
- [ALTER TABLE name SPLIT SHARD](#942e6b10f519010e)
- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)

<a id="b4f871c5e3e593ce"></a>
## ALTER TABLE name RENAME TO

<a id="2671b7b8a044fa74"></a>
### Function

It renames the table.

<a id="0a280182b0c08d3f"></a>
### Syntax

```
<rename table statement> ::=
    ALTER TABLE table_name 
        RENAME TO new_table_name
    ;
```

<a id="cf99a78130d2e863"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;rename table statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="72c94b5d9784b4c0"></a>
### Syntax Rules and Parameters

<a id="45400ebef5e6e40a"></a>
#### table_name

It is the existing name of the table.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="b02724e1755f3b38"></a>
#### new_table_name

It is a new name of the table.  
The same table name should not exist in the schema.

<a id="ebcab1e16a771317"></a>
### Description

Even when the table is renamed, the object referring to the table such as index, constraint does not need to be renamed.

<a id="54fd8e783cf24612"></a>
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

<a id="10a77fa4224b4209"></a>
### Compatibility

The SQL standard does not define &lt;rename table statement&gt;.

<a id="b67ef089833bf5a7"></a>
### For More Information

Refer to [ALTER TABLE](#8d2122be368c72be).

<a id="9e4d9a9c6969a42e"></a>
## ALTER TABLE name SET UNUSED COLUMN

<a id="63e6730a3dc01453"></a>
### Function

It drops a table column.

<a id="5ecb038be3d2736c"></a>
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

<a id="8ff4cb25d0c8b663"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;drop column definition&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="78462527709ba595"></a>
### Syntax Rules and Parameters

<a id="c732d7f6ac819687"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="73e336400f35ab57"></a>
#### SET UNUSED [ COLUMN ]

It sets the column not to be used.

<a id="87e1bd9cbc07ef9a"></a>
#### column_name_list

One or more column names to be dropped.

- e.g. ALTER TABLE t1 SET UNUSED COLUMN c1 
- e.g. ALTER TABLE t1 SET UNUSED COLUMN (c1, c2)

<a id="ad996ee63e77f54f"></a>
#### column_name

It is the column name to be dropped.  
It also drops the constraints and indexes which use the column.

<a id="ab3b93f79b60ac93"></a>
#### drop behavior

When it is omitted, the default value is RESTRICT.  
Currently, RESTRICT/CASCADE is operated in the same way.

<a id="32b3eda5db47e9dd"></a>
### Description

SET UNUSED COLUMN does not delete the data physically, so it ensures consistent performance regardless of the number of the rows.

<a id="87393d49b26dabeb"></a>
### Example

The following is an example of setting the column not to be used.

```
gSQL> ALTER TABLE t1 SET UNUSED COLUMN ( addr );

Table altered.
```

<a id="b6875b0434b848af"></a>
### Compatibility

The SQL standard does not define the following clauses.

- SET UNUSED
- CASCADE CONSTRAINTS
- Listing multiple columns

**SQL standard compatibility**

<a id="c2e0e8348f6c1e7e"></a>
| Feature ID | Description | Compatibility |
| --- | --- | --- |
| F033 | ALTER TABLE statement: DROP COLUMN clause | X |

<a id="1a920eabd8ee3205"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE](#8d2122be368c72be)
- [ALTER TABLE name ADD COLUMN](#9e97702c72f6ffbe)
- [ALTER TABLE name ALTER COLUMN](#22fe007bdb09fad4)
- [ALTER TABLE name RENAME COLUMN](#fc0bfc6460f62c7c)

<a id="942e6b10f519010e"></a>
## ALTER TABLE name SPLIT SHARD

<a id="a3df111a98915929"></a>
### Function

It rebalances a specific shard of a table by splitting it in a cluster environment.

<a id="c90c85385e80f49b"></a>
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

<a id="5f4dd00c1851189e"></a>
### Invocation and Access Rules

It can be performed in a cluster system.

One of the following privileges is required to perform &lt;alter table split shard statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="da7484ca767a7857"></a>
### Syntax Rules and Parameters

<a id="c67f6447a51d7660"></a>
#### table_name

It is the table name.  
It can define a schema to which the table belongs such as schema_name.table_name.  
If schema_name is omitted, the default schema name of the user performing the statement is used.  
The statement can be performed only when that table is a cluster group specific table, and when the shard is a list shard or a range shard.

<a id="83bcd96a93c9a8a2"></a>
#### source_shard_name

It is the name of an original shard to be split.   
If the shard does not exist in that table, the statement can not be performed.

<a id="1b34146b3b7104ba"></a>
#### &lt;split shard placement&gt;

It defines the target shard to which the original shard is rebalanced by splitting.

<a id="b4935ecf7a05d40d"></a>
#### &lt;split shard bound def&gt;

It defines the bound of a target shard to be split.

It can be defined as one of two following bound defs.

- &lt;split list shard def&gt;
- &lt;split range shard def&gt;

<a id="da7f7cc50b0d2448"></a>
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

<a id="23e1614932259eea"></a>
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

<a id="15b47389155f69d9"></a>
#### dest_group_name

It is the name of a cluster group in which the split shard is to be rebalanced.

<a id="a44296047e460e4a"></a>
### Description

It splits a specific shard of a specific table and rebalances it to a random cluster group.  
This is used to distribute records and loads by splitting the shards when records corresponding to a specific shard is too much or when a specific group member is overloaded.

<a id="7737f27d348da629"></a>
### Examples

The following is an example of executing the &lt;alter table split shard statement&gt; statement.

```
gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES IN ( 11 ) AT CLUSTER GROUP G2 );

Table altered.

gSQL> ALTER TABLE t1 SPLIT SHARD shard1 INTO ( SHARD shard11 VALUES LESS THAN ( 11 ) AT CLUSTER GROUP G2 );


Table altered.
```

<a id="f1d1a1c5428e476a"></a>
### Compatibility

The SQL standard does not define the concepts of the cluster.

<a id="42d2849d5839fb1e"></a>
### For More Information

Refer to the followings.

- [ALTER TABLE name REBALANCE](#f7d09b5058d6293a)
- [ALTER TABLE name REBALANCE EXCLUDE CLUSTER GROUP cluster_group_list](#f003b5733529d1e0)
- [ALTER TABLE name MOVE SHARD](#ce282f55c7c9877b)
- [ALTER TABLE name MERGE SHARDS](#2e12e025295d1acb)

<a id="71c41b55b638caef"></a>
## ALTER TABLE name STORAGE

<a id="8fe8deeec20e7d24"></a>
### Function

It alters physical attributes of a table.

<a id="7717bd81acc5ac90"></a>
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

<a id="a1fef946e6cfeac3"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter table physical attribute statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for that table
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the table belongs
- ALTER ANY TABLE ON DATABASE

<a id="2788c1518312d84f"></a>
### Syntax Rules and Parameters

<a id="cc9097a9049569cb"></a>
#### table_name

It is the table name to be altered.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="e18d25ffe877d96f"></a>
#### &lt;physical attribute clause&gt;

It alters the physical attribute of a page which configures the table.  
It is not applied to the already allocated page, but is applied to the newly allocated page.  
For more information, refer to [&lt;table physical attribute clause&gt;](19-sql-references-c-g.md#f51c022e96ec3285) of [CREATE TABLE](19-sql-references-c-g.md#4c3b06d433f75b3d).

<a id="edd68d66406a9eaf"></a>
#### &lt;segment attr clause&gt;

It alters the physical attribute of the extent configuring the segment. It is not applied to the already allocated extent but is applied to the newly allocated extent.

- MAXSIZE integer 
    - It alters the space size of the segment which can be allocated.
    - If the newly allocated space is smaller than the already allocated space, the MAXSIZE is altered to the currently allocated space size.

<a id="004b531652a04147"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="7dab7cce00f25dbd"></a>
### Example

The following is an example of changing the physical attribute of the table.

```
gSQL> ALTER TABLE t1 PCTFREE 10 PCTUSED 40 STORAGE ( NEXT 10M  MAXSIZE  100M );

Table altered.
```

<a id="2f3117c35afeecab"></a>
### Compatibility

The SQL standard does not define the physical property of a table.

<a id="34a328efdbaae1e3"></a>
### For More Information

Refer to [ALTER TABLE](#8d2122be368c72be).

<a id="b3042281f058c1cb"></a>
## ALTER TABLESPACE

<a id="e37879404a7521d6"></a>
### Function

It alters the tablespace definition.

<a id="b69d65611325f514"></a>
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

<a id="8ec83a81904d9a0c"></a>
### Invocation and Access Rules

ALTER TABLESPACE privilege is required to perform &lt;alter tablespace statement&gt;.

<a id="a435917f126bef15"></a>
### Syntax Rules and Parameters

<a id="d3bc8c8831e23305"></a>
#### &lt;rename tablespace statement&gt;

It renames the tablespace.  
For more information, refer to [ALTER TABLESPACE name RENAME TO](#a85bf45f67da2c65) statement.

<a id="574501440b68ff71"></a>
#### &lt;backup tablespace statement&gt;

It backs up the tablespace.  
For more information, refer to [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957) statement.

<a id="cbee3b3762e99f8f"></a>
#### &lt;on-offline tablespace statement&gt;

It changes all files in the tablespace to the online state or offline state.  
For more information, refer to [ALTER TABLESPACE name [ONLINE|OFFLINE]](#03c54bf99c431d45) statement.

<a id="45caf2d187b61dd8"></a>
#### &lt;add file statement&gt;

It adds a file to the tablespace.  
For more information, refer to [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#e6c60d7941ea0eca) statement.

<a id="60b06f55fde640f1"></a>
#### &lt;drop file statement&gt;

It drops a file from the tablespace.  
For more information, refer to [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#50070746325da70d) statement.

<a id="fb9cab4f064085f6"></a>
#### &lt;rename datafile statement&gt;

It renames the datafile in the data tablespace.   
For more information, refer to [ALTER TABLESPACE name RENAME DATAFILE](#c37c6f99c21bcc51) statement.

<a id="2bfe9b993ae3b8fc"></a>
### Description

Unlike other Data Definition Language (DDL), ALTER TABLESPACE statement is not allowed to ROLLBACK, and its transaction is automatically committed after executing the statement.

<a id="71e6f76639db5f32"></a>
### Example

Refer to the examples of each detailed statement.

<a id="7bbcde7624372756"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="18ef63f318668533"></a>
### For More Information

Refer to the followings.

- [CREATE TABLESPACE](19-sql-references-c-g.md#cfdf7d2f50958860)
- [DROP TABLESPACE](19-sql-references-c-g.md#a9171e5695f3e4e0)

<a id="e6c60d7941ea0eca"></a>
## ALTER TABLESPACE name ADD [DATAFILE|MEMORY]

<a id="c12c352baa85a48f"></a>
### Function

It extends the space of the tablespace.

<a id="6f94207ad9c5de81"></a>
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
        [ <autoextend clause> ]

<autoextend clause>
    AUTOEXTEND { ON [ <next size clause> ] [ <max size clause> ] | OFF }

<next size clause>
    NEXT <size clause>

<max size clause>
    MAXSIZE { <size clause> | UNLIMITED }
```

<a id="a7d71671b8113a4c"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;add space statement&gt;.

<a id="d3befcc3ef619d11"></a>
### Syntax Rules and Parameters

<a id="b31d64dcb2e1bab9"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="7153b929d8475833"></a>
#### &lt;file specification&gt;

The following syntax should be used according to the tablespace type.

- Memory data tablespace
    - DATAFILE &lt;add datafile clause&gt;
- Memory temporary tablespace
    - MEMORY &lt;memory clause&gt;

<a id="843071c48df726da"></a>
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

<a id="1d0d7d7a94009233"></a>
#### &lt;memory clause&gt;

- &lt;size clause&gt;
    - It defines the memory to be added.

For more information, refer to  [&lt;memory clause&gt;](19-sql-references-c-g.md#19e55aea320f5684) of [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#504552ef753c144a) statement.

<a id="ad486c5a86fe5f84"></a>
#### &lt;autoextend clause&gt;

It sets the automatic extending property when adding the data file of the disk tablespace. Set the automatic extending property to *ON* or *OFF*. If it is set to *ON*, then it can define the size of the automatic extending and the maximum size of the data file.

<a id="f8ca9b4b1e37104f"></a>
#### &lt;next size clause&gt;

It defines the space size to be extended when there is not any space available in the current data file in use.

<a id="6d8a7045014c7f16"></a>
#### &lt;max size clause&gt;

It defines the maximum size of the data file which can be extended.

<a id="2a77f2906c79d2d3"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="473ef58baf1f4783"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="67f7e4b99f6447b6"></a>
### Example

The following is an example of adding datafile to the tablespace.

```
gSQL> ALTER TABLESPACE space1 ADD DATAFILE 'test_file_a2.dbf' SIZE 10M REUSE;

Tablespace altered.
```

<a id="4a0b79adf0e82623"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="974bf58a6fcbc65a"></a>
### For More Information

Refer to the followings.

- [CREATE MEMORY DATA TABLESPACE](19-sql-references-c-g.md#9831f431f182fce6)
- [CREATE MEMORY TEMPORARY TABLESPACE](19-sql-references-c-g.md#504552ef753c144a)
- [ALTER TABLESPACE](#b3042281f058c1cb)

<a id="bedd10e0f3e72957"></a>
## ALTER TABLESPACE name BACKUP

<a id="1d78ad4eb651074a"></a>
### Function

It switches the tablespace to backup enabled state and backup disabled state to perform backup.

<a id="f24a227759bff1e8"></a>
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

<a id="bd2e43abb194f4f8"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;backup space statement&gt;.

<a id="7fc93576e88163d7"></a>
### Syntax Rules and Parameters

<a id="3db23baf4975d95a"></a>
#### &lt;tablespace begin backup statement&gt;

It sets the tablespace to the backup enabled state.

- The tablespace being used is set to the backup enabled state.
- The backup state of the tablespace such as OFFLINE/ temporary can not be switched.

<a id="38776b36945f8618"></a>
#### tablespace_name

It is the tablespace name whose backup state is to be switched.

<a id="c39c793a41ee7c74"></a>
#### &lt;tablespace end backup statement&gt;

It sets the tablespace to the backup disabled state.

<a id="f9c6c9b24936017e"></a>
#### &lt;tablesapce incremental backup statement&gt;

It performs the incremental backup of the tablespace.  
The database is in OPEN phase and it should be operated in ARCHIVELOG mode.

<a id="8e86b90d4a9823f9"></a>
#### &lt;incremental backup option&gt;

- An 'Integer' can be specified from 0 to 4. 
- 'LEVEL 0' can not specify CUMULATIVE or DIFFERENTIAL.
- CUMULATIVE | DIFFERENTIAL
    - CUMULATIVE
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n-1. 
    - DIFFERENTIAL
        - If 'integer' is n, it backs up all pages which are altered after the most recent backups of LEVEL 0 ~ LEVEL n.
    - If it is omitted, DIFFERENTIAL is specified by default.

<a id="d4c94bcd7183bde2"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="56f1dc6ee72a679d"></a>
### Description

It backs up the datafiles which are created in the tablespace. A full backup of the tablespace begins with BEGIN BACKUP, and copies the datafiles by OS file copy and ends with END BACKUP. The incremental backup file is created in the path set by BACKUP_DIR 1 property using a single statement.

<a id="a4a373efe9a35658"></a>
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

<a id="452a8f4db4e0f09f"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="3120b9b677f3e434"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#b3042281f058c1cb)
- [ALTER TABLESPACE name [ONLINE|OFFLINE]](#03c54bf99c431d45)

<a id="50070746325da70d"></a>
## ALTER TABLESPACE name DROP [DATAFILE|MEMORY]

<a id="3e73536873a6e1b1"></a>
### Function

It reduces the space of the tablespace.

<a id="f4ee91c28dee1986"></a>
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

<a id="a7241074342e9ae1"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;drop space statement&gt;.

<a id="25c5f2b7bf8dc94b"></a>
### Syntax Rules and Parameters

<a id="04353f5c4c5478ee"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="34e2525f834bd74c"></a>
#### &lt;file specification&gt;

The following syntax should be used according to the tablespace type.

- Memory data tablespace
    - DATAFILE 'filename' 
- Memory temporary tablespace
    - MEMORY 'memory_name'

> The file of OFFLINE tablespace can not be dropped.   
> The first file of the tablespace can not be dropped.   
> The data file which has been used once can not be dropped.

<a id="65f8356274fe314c"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="47d5f43cf0ecfd37"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="bb1f106a164bb407"></a>
### Example

The following is an example of dropping the file from the tablespace.

```
gSQL> ALTER TABLESPACE space1 DROP DATAFILE 'test_file_f2.dbf';

Tablespace altered.
```

<a id="07cf6a484276e709"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="ab8235efeee6a1f4"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#b3042281f058c1cb)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#e6c60d7941ea0eca)
- [ALTER TABLESPACE name RENAME DATAFILE](#c37c6f99c21bcc51)

<a id="03c54bf99c431d45"></a>
## ALTER TABLESPACE name [ONLINE|OFFLINE]

<a id="0fdada5e7eec719d"></a>
### Function

It alters the tablespace status.

<a id="0891ba7806ddb07e"></a>
### Syntax

```
<on/off tablespace statement> ::=
    ALTER TABLESPACE tablespace_name { ONLINE | OFFLINE [ NORMAL | IMMEIDATE ] }
    [ AT <domain name> ]
    ;
```

<a id="705b11c454ee4bcd"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;on/off tablespace statement&gt;.

<a id="f79177e03c7ed04d"></a>
### Syntax Rules and Parameters

<a id="72daf2d6169adbf2"></a>
#### ONLINE

It alters the tablespace status in OFFLINE state to ONLINE state.

<a id="896ec687a5bfaa9b"></a>
#### OFFLINE NORMAL

It alters the tablespace status in ONLINE state to OFFLINE state.

The media recovery is not required in ONLINE state because the tablespace which was altered to OFFLINE state is in consistent state.

> OFFLINE NORMAL is not allowed in MOUNT phase.  
> (However, if the previous instance is terminated by `\`SHUTDOWN NORMAL, OFFLINE NORMAL is allowed.)

<a id="f91991d61565d992"></a>
#### OFFLINE IMMEDIATE

It alters the tablespace status in ONLINE state to OFFLINE state.

The media recovery is required in ONLINE state because the tablespace which was altered to OFFLINE state is in inconsistent state.

> The SYSTEM tablespace can not be altered to OFFLINE state.   
> OFFLINE IMMEDIATE requires the media recovery, so it can be performed only in ARCHIVELOG mode.

<a id="02c1deb71a9ba00e"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="1762971255d9b7c9"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="303a1b7b94abeeb3"></a>
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

<a id="b66874812d5196fa"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="39138d37ed3ba586"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#b3042281f058c1cb)
- [ALTER TABLESPACE name BACKUP](#bedd10e0f3e72957)

<a id="c37c6f99c21bcc51"></a>
## ALTER TABLESPACE name RENAME DATAFILE

<a id="8b2aa0ff7d559edd"></a>
### Function

It renames the datafiles that configure the tablespace.

<a id="8bfc84e77fd8ca84"></a>
### Syntax

```
<rename datafile statement> ::=
    ALTER TABLESPACE tablespace_name RENAME DATAFILE <filename_list> TO <filename_list>
    ;

    <filename_list> ::= 
        'filename' [, ...]
```

<a id="0f214c67d0289cc0"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege is required to perform &lt;rename datafile statement&gt;.

> ONLINE tablespace file can not be altered when it is in TDS mode and the database is in OPEN phase. (Except for the temporary memory tablespace.)   
> The file should exist even after the alteration.

<a id="f9971e13b5a954ba"></a>
### Syntax Rules and Parameters

<a id="5cdc46ccd77f486a"></a>
#### tablespace_name

It is the tablespace name to be altered.

<a id="8f52cc6a63cf87d0"></a>
#### 'filename'

The memory temporary tablespace is 'memory_name' and the other kinds of tablespace is 'filename'.

<a id="8059136712b5947a"></a>
#### &lt;domain name&gt;

It is a name of a member or a group for which the statement is performed.  
If it is omitted, it is performed for all groups.

<a id="22b02e39685d5b8a"></a>
### Description

The tablespace status determines whether the operation can be performed.

- OFFLINE: It can be performed in MOUNT or OPEN phase.
- ONLINE: It can be performed only in MOUNT phase.

<a id="4a0e5c8780ad03de"></a>
### Example

The following is an example of renaming 'test.dbf' to 'test1.dbf'.

```
gSQL> ALTER TABLESPACE TEST_TBS RENAME DATAFILE 'test.dbf' TO 'test1.dbf';

Tablespace altered.
```

<a id="08efdeed11df5951"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="4e0ead7c585d2ee0"></a>
### For More Information

Refer to the followings.

- [ALTER TABLESPACE](#b3042281f058c1cb)
- [ALTER TABLESPACE name ADD [DATAFILE|MEMORY]](#e6c60d7941ea0eca)
- [ALTER TABLESPACE name DROP [DATAFILE|MEMORY]](#50070746325da70d)

<a id="a85bf45f67da2c65"></a>
## ALTER TABLESPACE name RENAME TO

<a id="5a275cd07beae0c4"></a>
### Function

It renames the tablespace.

<a id="5ccec94cb447bb3b"></a>
### Syntax

```
<rename tablespace statement> ::=
    ALTER TABLESPACE tablespace_name RENAME TO <new_tablespace_name>
    ;
```

<a id="790317cfb248e32c"></a>
### Invocation and Access Rules

ALTER TABLESPACE ON DATABASE privilege required to perform &lt;rename space statement&gt;.

<a id="e7348008e23bcf1a"></a>
### Syntax Rules and Parameters

<a id="f171658dd383d1a3"></a>
#### tablespace_name

It is a name of the old tablespace.

- The built-in tablespace can not be renamed.
- The OFFLINE tablespace can not be renamed.

<a id="59b43778e84f6902"></a>
#### new_tablespace_name

It is a name of the new tablespace.

<a id="c5e25bb525527298"></a>
### Description

Even when the tablespace is renamed, the table or index which was already created in the existing tablespace does not need to be renamed.

<a id="467abd1c1a63c15d"></a>
### Example

The following is an example of renaming the tablespace.

```
gSQL> ALTER TABLESPACE space1 RENAME TO space2;

Tablespace altered.
```

<a id="0e6b503a8aa6caef"></a>
### Compatibility

The SQL standard does not define the concepts of the tablespace.

<a id="3e6330f78c2c54fa"></a>
### For More Information

Refer to [ALTER TABLESPACE](#b3042281f058c1cb).

<a id="270d91f0c78160b6"></a>
## ALTER USER

<a id="aeb6b71e0584fc97"></a>
### Function

It alters the user definition of the database.

<a id="470319424277a775"></a>
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

<a id="ec75cccb89fb36be"></a>
### Invocation and Access Rules

ALTER USER ON DATABASE privilege is required to perform &lt;alter user statement&gt;.  
However, &lt;alter password&gt; can be performed without any privilege, when the user and user_identifier are identical.

<a id="d3ca8f559e5dcb6f"></a>
### Syntax Rules and Parameters

<a id="30c32216ec97db66"></a>
#### user_identifier

It is the username to be altered.

<a id="7cfcc99578ec2465"></a>
#### &lt;alter password&gt;

It alters the user's password.

- IDENTIFIED BY new_password 
    - The new password is encrypted and stored. 
    - The length of the password should be shorter than 128 byte. 
    - The password is case sensitive.

- REPLACE old_password 
    - It can be omitted when ALTER USER ON DATABASE privilege is given.
    - It can not be omitted when ALTER USER ON DATABASE privilege is not given.
        - The user and the user_identifier should be identical.

<a id="51693a2363cb5f3b"></a>
#### &lt;alter profile&gt;

It alters the profile for the password management policy.

- PROFILE profile_name
    - It allocates profile_name which is created by a user.
- PROFILE DEFAULT
    - It allocates "DEFAULT" which is the default profile.
- PROFILE NULL
    - It does not allocate the profile.

<a id="f3f767cef129a2ba"></a>
#### &lt;password expire&gt;

It expires the user's password.

<a id="b71c946124ab2b15"></a>
#### &lt;account lock&gt;

- ACCOUNT LOCK
    - It locks the user account. 
- ACCOUNT UNLOCK
    - It unlocks the user account.

<a id="f932731a7889d21e"></a>
#### &lt;alter default tablespace&gt;

It alters the user's default tablespace.  
The tablespace_name should be a data tablespace.

<a id="2d7c2e4cca531a8c"></a>
#### &lt;alter temporary tablespace&gt;

It alters the user's temporary tablespace.  
The tablespace_name should be a temporary tablespace.

<a id="47166087fa6fa7a6"></a>
#### &lt;alter index tablespace&gt;

It alters an index tablespace of the user.

- It specifies INDEX TABLESPACE tablespace_name.
    - If the data tablespace is specified, then it becomes a LOGGING index.
    - If the temporary tablespace is specified, then it becomes a NOLOGGING index.
- INDEX TABLESPACE NULL
    - It does not specify an index tablespace.

<a id="65f8ba7aa2d24169"></a>
#### &lt;alter schema path&gt;

It alters the user's schema access path.  
If the schema is not specified in user's SQL statement, the schema access path is determined in the schema order for the naming resolution of the object.

If the schema name is as same as another schema which is previously listed, it is not applied.

The following is an example of objects existing in a schema when performing *ALTER USER u1 SCHEMA PATH ( u1, s2, public );*  statement.

<a id="37fd3081d7cee4e0"></a>
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

<a id="bd2c6425271195e7"></a>
#### CURRENT PATH

It is the current user's schema path.

A new schema path can be added using CURRENT PATH maintaining the existing schema path as follows.

- The u1's current schema path 
    - (u1, public) 
- The statement execution
    - ALTER USER u1 SCHEMA PATH ( s1, CURRENT PATH, s2 ); 
- The u1's schema path is altered as follows.
    - (s1, u1, public, s2)

<a id="9247ab89fd3b215d"></a>
#### ALTER USER PUBLIC &lt;alter schema path&gt;

It alters the schema path of PUBLIC account.  
The schema path of PUBLIC account is included in every user's schema path.

The initial schema path which is allocated to PUBLIC account is as follows.

- DICTIONARY_SCHEMA
- INFORMATION_SCHEMA
- DEFINITION_SCHEMA
- PERFORMANCE_VIEW_SCHEMA
- FIXED_TABLE_SCHEMA

<a id="b5cbd8a0648afffc"></a>
### Description

For more information, refer to the rules for each syntax.

<a id="62ac923b4c2bbb1d"></a>
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

<a id="d89cb7dd781f656a"></a>
### Compatibility

SQL standard covers the concepts of a user, but it does not define the SQL statements associated with creating, altering, dropping a user.

<a id="522d115e24ea7dcd"></a>
### For More Information

Refer to the followings.

- [CREATE USER](19-sql-references-c-g.md#67d566d84adb0376)
- [DROP USER](19-sql-references-c-g.md#f64464bae416acc8)

<a id="766aa99e0f4c4f78"></a>
## ALTER VIEW

<a id="31a982087112c75b"></a>
### Function

It alters the view definition.

<a id="215b0900c8bf10fd"></a>
### Syntax

```
<alter view statement> ::=
    ALTER VIEW view_name <alter view action>
    ;

<alter view action> ::=
    COMPILE
```

<a id="ef61e018a33f658d"></a>
### Invocation and Access Rules

One of the following privileges is required to perform &lt;alter view statement&gt;.

- (ALTER or CONTROL TABLE) ON TABLE for the view
- (ALTER TABLE or CONTROL SCHEMA) ON SCHEMA for the schema to which the view belongs
- ALTER ANY TABLE ON DATABASE

<a id="76955024250cadf3"></a>
### Syntax Rules and Parameters

<a id="b4d2556ad74f0b7c"></a>
#### view_name

It is the view name to be altered.  
It can define the schema to which the view belongs, such as schema_name.view_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="d4743527c082fb6b"></a>
#### COMPILE

It compiles the view again.  
COMMENT which is given to the view column is initialized.

<a id="1ed4eb96e56dac33"></a>
### Description

When the table or the view which is referenced by the view is altered or dropped, then it affects that view.

This information can be retrieved from INFORMATION_SCHEMA.VIEWS.

- IS_COMPILED column
    - TRUE: The view was successfully created. 
    - FALSE: The view was created with FORCE option when an error exists.

- IS_AFFECTED column
    - TRUE: The table and the view which was referenced by the view was altered.
    - FALSE: After creation and compilation of a view, the table and the view which was referenced by the view was not altered.

<a id="5f9409479eda2327"></a>
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

<a id="68a66e34b440f0eb"></a>
### Compatibility

The SQL standard does not define &lt;alter view statement&gt;.

<a id="9676c30a17633b47"></a>
### For More Information

Refer to the followings.

- [CREATE VIEW](19-sql-references-c-g.md#b82ddec42cccf582)
- [DROP VIEW](19-sql-references-c-g.md#34f6b0ced02ffeeb)

<a id="7788adc1bfa02cb3"></a>
## ANALYZE SYSTEM

<a id="e7f738d37ff2d11a"></a>
### Function

It controls the statistics information of the system.

<a id="58659c969216d98e"></a>
### Syntax

```
<analyze system statement> ::=
    ANALYZE SYSTEM [ <analyze action> ]
    ;

<analyze action> ::=
      COMPUTE STATISTICS
    | DELETE STATISTICS
```

<a id="048b62e870ee83d9"></a>
### Invocation and Access Rules

ANALYZE ANY ON DATABASE privilege is required to perform &lt;analyze system statement&gt;.

<a id="879abd77b0168765"></a>
### Syntax Rules and Parameters

<a id="7feb3f2ed157334c"></a>
#### &lt;analyze action&gt;

When it is omitted, the default value is COMPUTE STATISTICS.

<a id="4d0a0ada4df93bb9"></a>
#### COMPUTE STATISTICS

It builds the following statistics information related to the system.

- CPU_OPS (Operations Per Second) 
    - It is the number of operations of which the CPU can process per second.

- NETWORK_IOPS (I/O operations Per Second) 
    - It is valid for the cluster. 
    - It is the number of the network I/O which can be processed per second.

<a id="a2002b216f92cf2c"></a>
#### DELETE STATISTICS

It deletes the statistics information of the system.

<a id="98ade56096bae30b"></a>
### Description

The built statistics information of the system is used to calculate the cost of optimization for the query process.

<a id="1885547137d420eb"></a>
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

<a id="0624c3cf6932b87c"></a>
### Compatibility

The SQL standard does not define the concepts of the statistics information.

<a id="6635bcb78a736093"></a>
### For More Information

Refer to [ANALYZE TABLE](#30fc30b6cd667055).

<a id="30fc30b6cd667055"></a>
## ANALYZE TABLE

<a id="4eb992c106cfee1d"></a>
### Function

It controls the statistics information of the table.

<a id="b789b9f011e916d0"></a>
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

<a id="efe58f23202d775f"></a>
### Invocation and Access Rules

ANALYZE ANY ON DATABASE privilege is required to perform &lt;analyze table statement&gt;.

<a id="510b76f269344eca"></a>
### Syntax Rules and Parameters

<a id="9f0e29ca8020f013"></a>
#### table_name

It is the table name.  
It can define the schema to which the table belongs, such as schema_name.table_name. If schema_name is omitted, the default schema name of the user performing the statement is used.

<a id="5982130f2227c197"></a>
#### &lt;parallel clause&gt;

It specifies the number of threads to be used in a analyzing process.  
If it is not specified, the default value is PARALLEL.

- NOPARALLEL
    - It does not analyze in parallel.

- PARALLEL [thread_count]
    - It analyzes in parallel.
    - The minimum value of the thread_count is 0, and the maximum value is 64.
    - If the thread_count value is 0 or it is omitted, then it is determined by the number of CPUs in the system.

<a id="fc9b5d4f6333d4df"></a>
#### &lt;analyze action&gt;

When it is omitted, the default value is COMPUTE STATISTICS.

<a id="ca509d6d6a4796d7"></a>
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

<a id="f5fa48d45a37825a"></a>
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

<a id="929ea5a64678da33"></a>
#### ESTIMATE STATISTICS &lt;sample_clause&gt;

It builds the statistics information of the column and the index by using as many samples as the specified &lt;sample_clause&gt;.

- SAMPLE row_count ROWS 
    - It uses as many samples as the specified number of rows.
    - row_count is a positive integer bigger than 0. 
- SAMPLE percentage PERCENT 
    - It uses as many samples as the specified ratio.
    - The percentage is a positive integer in the range between 1 and 99.

If the number of the sampling rows is smaller than the value of [MIN_SAMPLE_ROW_COUNT](../part-02-administration-manual/10-server-property.md#b04be52f7248ccb2) property, then it follows the property value.

<a id="9602bd012c8f9f3c"></a>
#### &lt;for_clause&gt;

If it is omitted, it builds the statistics information of all possible columns and indexes.

<a id="699fb9e92d07c850"></a>
#### FOR ALL COLUMNS

It builds the statistics information of all possible columns.  
It does not build the statistics information of an index.

<a id="fadc53dbfffafd19"></a>
#### FOR ALL INDEXED COLUMNS

It builds the statistics information of all columns included in an index.  
It does not build the statistics information of other columns.  
It does not build the statistics information of an index.

<a id="203effc047c1b8f8"></a>
#### FOR COLUMNS column_name [, ...]

It builds the statistics information of the listed columns.  
It does not build the statistics information of unlisted columns.  
It does not build the statistics information of an index.

<a id="caeb7370c5798ff1"></a>
#### FOR ALL INDEXES

It builds the statistics information of all indexes.  
It does not build the statistics information of columns.

<a id="4cc6cbd6505eb428"></a>
#### FOR INDEXES index_name [, ...]

It builds the statistics information of the listed indexes.  
It does not build the statistics information of unlisted indexes.  
It does not build the statistics information of a column.

<a id="fbde242dfad25670"></a>
#### DELETE STATISTICS

It deletes the statistics information of the table.

<a id="98cf9057515f1d74"></a>
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

<a id="ea1f3e34a0b0d048"></a>
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

<a id="be7d6dd690693835"></a>
### Compatibility

The SQL standard does not define the concepts of the statistics information.

<a id="79cff4fa0067a2ed"></a>
### For More Information

Refer to [ANALYZE SYSTEM](#7788adc1bfa02cb3).

<a id="9289801d878dbdc2"></a>
## AUDIT POLICY

<a id="aaa25a6a78862915"></a>
### Function

It activates the audit policy.

<a id="505ca2b6d4ff62fd"></a>
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

<a id="a35659537139180c"></a>
### Invocation and Access Rules

AUDIT SYSTEM ON DATABASE privilege is required to perform &lt;audit policy statement&gt;.

<a id="6d83bc26b501155c"></a>
### Syntax Rules and Parameters

<a id="1a445e08a3580b03"></a>
#### policy_name

It is the name of the audit policy object to be activated.  
The activated audit policy does not effect on the existing session, and it effects only on the newly created session.

<a id="f9ca8fdaa85da71d"></a>
#### &lt;specified_user_option&gt;

It specifies the user to be audited.  
If omitted, all users are audited.

BY clause and EXCEPT clause can not be used together for the same audit policy.

- BY user_list: If the user to be audited is specified, then use BY clause.
- EXCEPT user_list: If other users excluding a specific user is to be audited, use EXCEPT clause.

<a id="c9aca1b6ad0fe3e8"></a>
#### &lt;specified_success_option&gt;

- WHENEVER SUCCESSFUL
    - If an action succeeds, then the audit record is created.
- WHENEVER NOT SUCCESSFUL
    - If an action fails, then the audit record is created.
- If omitted, both when an action succeeds and fails, the audit record is created.

<a id="24e006e02ae13121"></a>
### Description

Activating the audit policy does not affect the existing session, but it starts to audit the newly created session.

<a id="c457631b2f4cf0e0"></a>
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

<a id="8774953c25786b09"></a>
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

<a id="37ff849bd1ba8711"></a>
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

<a id="487416b55fe45d12"></a>
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

<a id="1947d3bec11a2cca"></a>
### Compatibility

The SQL standard does not have the audit policy.

<a id="2a4daca134770762"></a>
### For More Information

Refer to the followings.

- Managing audit policy object
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#4f95ec95d004a1b2)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#74a07e0949274daf)
    - [ALTER AUDIT POLICY](#53347c6092b6e054)

- Activating/ deactivating audit policy
    - [AUDIT POLICY](#9289801d878dbdc2)
    - [NOAUDIT POLICY](20-sql-references-h-z.md#1d87c2f21b970bb9)

- Viewing audit trail: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#c239152842953eb8)

- Clearing audit trail: [ALTER DATABASE CLEAR AUDIT TRAIL](#783e2ba71672a2fa)

---

[← 17. Built-in Function References](17-built-in-function-references.md) · [Table of contents](../README.md) · [19. SQL References (C~G) →](19-sql-references-c-g.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
