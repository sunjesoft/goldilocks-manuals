<a id="f88ef52e0a3a7613"></a>

# 30. Database Connection

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/f88ef52e0a3a7613)  
> Tag: `22c.1_10_tag`

[← 29. PSM SQL References](../part-04-psm-manual/29-psm-sql-references.md) · [Table of contents](../README.md) · [31. ODBC →](31-odbc.md)

<a id="068c32fb3f6382cb"></a>
## Features

<a id="c05a040310f73bd8"></a>
![GLOBAL CONNECTION](../assets/images/c322afaa7afd1eac.png)

Global connection feature is a method of optimizing transaction performance in consideration of data locality.  
A general connection is a connection with a single member, but global connection is a connection with all members. An application using the global connection makes the member with most data accessed by queries perform the query, so the performance is upgraded.   
Hash, range, list sharding method can use the global connection, and the application does not need to be altered at that moment.

When the online scale-out is performed, a user does not need to consider a new node but the the application automatically connects to a new node and operates it.

<a id="87b81d7939fa647c"></a>
![GLOBAL CONNECTION HA (high availability)](../assets/images/e8a20c9c85740f44.png)

If an error occurs on the selected node when performing SQL, then the SQL is performed through another node in the same group. If errors occur on all nodes in the selected group, then the SQL is performed through another group.    
When a node is recovered from an error, the it is automatically connected to the node again online. Moreover, a user can make an application connect again by using the following syntax.

```
ALTER SYSTEM RECONNECT GLOBAL CONNECTION
```

<a id="6d65ac6c5d8e5db7"></a>
## Selecting Execution Member

An execution member is selected per transaction. When DML query is first performed without a transaction, a group is selected according to the sharding key, and an execution member in the group is selected according to LOCALITY_MEMBER_POLICY property. Then, all queries are processed in the selected member until COMMIT or ROLLBACK. If the first query can not select the appropriate group according to a sharding key, then the group is selected according to LOCALITY_GROUP_POLICY property.

<a id="093d5a6a59f4b748"></a>
![Selecting a member](../assets/images/ea58d966fae6b746.png)

In case of transaction1 in the figure above, UPDATE query is performed in the group1 according to the sharding key, so all queries between COMMITs are performed in group1. In case of transaction2, UPDATE query is performed in group3, and all queries are performed in group3 before COMMIT even when further queries are not appropriate to perform in group3.

The read-only query (SELECT) without a transaction selects an execution member according to  a sharding key like as other queries, but further queries are not always performed in the previously selected member.   
In other words, all queries included in a transaction is performed only in a single member, but a query  irrelevant to a transaction selects a member per a member.

<a id="bcd46f908c936f9e"></a>
## Global Session

<a id="740632d65333771c"></a>
![Cluster session derived from global connection](../assets/images/461f30a3236066d0.png)

The session directly connected to an application is called as a driver session, and a session from a driver session to another member is called as a cluster session. Global connection creates a driver session in all members, and creates cluster sessions in another member when it is needed. Global connection can make multiple cluster sessions in a single member.

<a id="0d7d024290f27684"></a>
![Global session](../assets/images/08aec27d2baea3d3.png)

Global session is a feature for a cluster sessions created in the global connection shares a single session to improve the resource efficiency. When the global connection does not use a global session, then the cluster session increases according to increasing groups and members. However, when it uses the global session, then the cluster session does not increase even when groups and members increase.

The global session feature is available only in the global connection, but it is not available in the general connection.

<a id="832fbdb2d3876ebb"></a>
## Constraints

When using the global connection, a session dependent object is not available in SQL statement, a session dependent clause nor is a session dependent function available.

Also, if SQLs accessing to multiple cluster nodes exist in a single transaction, then SQLs in the transaction uses the cluster node in common which were selected by the sharding key of the first SQL.

The query in the global connection is performed in consideration of data locality only when it is performed with prepare execute. However, it is performed in an arbitrary node when it is performed with direct execute.

<a id="d0c3f5598a7ead43"></a>
### Session Dependent Object

When using a session dependent object in SQL statement, the global connection is not available.

- Global temporary table

<a id="5433a47e4e4f2150"></a>
### Session Dependent Clause

When using a session dependent clause in SQL statement, the global connection is not available.

- All @domain-related statements

<a id="d4a74a4fce1c8f3c"></a>
### Session Dependent Function and Pseudo Column

When using session dependent information in SQL statement, the global connection is not available.

- CURRVAL(sequence), sequence.CURRVAL
- UUID()
- VERSION()
- SESSION_ID()
- SESSION_SERIAL()
- USER_ID()
- LAST_IDENTITY_VALUE()
- STATEMENT_VIEW_SCN()
- STATEMENT_VIEW_SCN_GCN()
- STATEMENT_VIEW_SCN_DCN()
- STATEMENT_VIEW_SCN_LCN()
- LOCAL_GROUP_ID()
- LOCAL_MEMBER_ID()
- LOCAL_GROUP_NAME()
- LOCAL_MEMBER_NAME()
- CLUSTER_GROUP_ID
- CLUSTER_GROUP_NAME
- CLUSTER_MEMBER_ID
- CLUSTER_MEMBER_NAME
- CLUSTER_SHARD_ID

<a id="3a19341946ee83eb"></a>
### When Using Global Session

Data Definition Language (DDL) is not available in SQL statement.

<a id="d10a4f6480f5e9e7"></a>
## Settings

For more information, refer to the followings.

- [Setting global connection in ODBC ](31-odbc.md#7c9e8defdb7b38e1)
- [Setting global connection in JDBC ](32-jdbc.md#9559380de8fafad8)

---

[← 29. PSM SQL References](../part-04-psm-manual/29-psm-sql-references.md) · [Table of contents](../README.md) · [31. ODBC →](31-odbc.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
