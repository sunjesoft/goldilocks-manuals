<a id="eb2050e20eb39a08"></a>

# 14. Cluster Objects

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/eb2050e20eb39a08)  
> Tag: `22c.1_10_tag`

[← 13. SQL Objects](13-sql-objects.md) · [Table of contents](../README.md) · [15. SQL Tuning →](15-sql-tuning.md)

<a id="5ddda09b70f4933f"></a>
## Cluster System

<a id="727acc970a3e8ff4"></a>
### Cluster System Related Statements

For more information, refer to the followings.

- Expanding a cluster system
    - [CREATE CLUSTER GROUP](19-sql-references-c-g.md#57c6f6ae1e01e560)
    - [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03)

- Controlling an inactive cluster member
    - [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](18-sql-references-a-b.md#1f2538cb978d9370)
    - [ALTER SYSTEM JOIN DATABASE](18-sql-references-a-b.md#7a98f890a10933e4)

- Rebalancing data
    - [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#e579543f77dce467)
    - [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b)

Information which is related to a cluster system can be retrieved through the following views.

<a id="1aa5dab0b27fb69e"></a>
<table class="table column_count_3"><caption>Cluster system related information</caption><thead><tr><th class="to_center"><div>Schema</div></th><th class="to_center"><div>View</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>DICTIONARY_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#c944365990fbf691">DBA_CLUSTER</a></div></td><td class="to_middle"><div>Object information of a cluster group and a cluster member which configure a cluster</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#7ec8d9a1539c5557">DBA_CLUSTER_COMMENTS</a></div></td><td class="to_middle"><div>Comment information of a cluster group and a cluster member</div></td></tr><tr><td class="to_middle"><div>PERFORMANCE_VIEW_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#fffe98e088d63f51">V$CLUSTER_MEMBER</a></div></td><td class="to_middle"><div>Status information of a cluster member</div></td></tr></tbody></table>

<a id="2e282a2820dc91f1"></a>
### Concepts of Cluster System

GOLDILOCKS cluster system manages data of a single database by sharding or duplicating the data into several servers. Applications can be run on every server configuring a cluster system, and run in the same way as using a single database system regardless of a system configuration or a connected server.

GOLDILOCKS cluster system consists of one or more cluster groups, and a cluster group consists of one or more cluster members. It does not require a separate application server or a meta server, but applications are connected to a cluster member corresponding to a data server, and run.

<a id="7e0c59aa2b2cbe3d"></a>
![3 x 2 cluster system](../assets/images/1ecc70e395b155ff.png)

The figure above is a 3x2 cluster system which consists of two cluster members consisting of three cluster groups and a single cluster group. In the figure above, the cluster system consists of cluster groups (G1, G2, G3), and the cluster group G1 consists of cluster members (G1N1, G1N2), the cluster group G2 consists of cluster members (G2N1 and G2N2), and the cluster group G3 consists of cluster members (G3N1, G3N2). Applications can access any of those six cluster members and it is run as same as using a single database.

The table data is sharded and placed in each cluster group, and cluster members in a cluster group maintain the replications same. The figure below describes the concepts of the table data placement in a 3x2 cluster.

<a id="6315ac1a6a7098ad"></a>
![Concepts of sharding and duplicating by the cluster](../assets/images/04bb7f3491bb1ca3.png)

The table data is sharded and placed in each cluster group according to the sharding strategy defined by a user. (According to the ID column in the figure above) The placed data in a cluster group maintains the replication of a cluster member in a cluster group.

<a id="ee17ef1497265af1"></a>
### Availability of Cluster System

Cluster continues to provide service even when a specific server is broken or the network is cut. Cluster members configuring each cluster group maintain the same data replications, so the service does not stop even when a single cluster member is broken. In other words, unless the data is lost due to the malfunction of all cluster members in a cluster group, the service continues to be provided.

The cluster continues to provide service even when three devices are broken in the 3x2 cluster as follows.

<a id="5ac632e1fa070822"></a>
![Cluster availability](../assets/images/4539ef4716b9eb74.png)

If additional errors occur in G1N1, G2N2, G3N1 in the situation above, then the data loss occurs and the service can not be provided any more. Therefore, a user should make the broken device to participate in a cluster system, or add a new cluster member before an additional error occurs.

- [ALTER SYSTEM JOIN DATABASE](18-sql-references-a-b.md#7a98f890a10933e4) statement is used to make the broken cluster member to participate in a cluster system again.

- [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](18-sql-references-a-b.md#1f2538cb978d9370) statement is used to drop the broken cluster member from the cluster system.

- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03) statement is used to add a cluster member to a cluster group for the high availability.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#e579543f77dce467) statement and [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b) statement are used to rebalance data to a newly added cluster member.

<a id="f5f7553495a793d1"></a>
### Expanding Cluster System

The cluster can be expanded by adding a new server without stopping the service.

Cluster is expanded by adding a cluster member or a cluster group and by rebalancing the data to an created server.

The following is an example of expanding a 2x1 cluster to a 3x2 cluster.

<a id="84cc3c1ffd4d9b27"></a>
![Expanding cluster system](../assets/images/ed47cfe58d141b20.png)

Add a cluster group and a cluster member by using the following statements to expand a cluster.

- [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03)
- [CREATE CLUSTER GROUP](19-sql-references-c-g.md#57c6f6ae1e01e560)

To add a new cluster member to the cluster system, tablespaces in the cluster member and those in the cluster system should be same. In other words, tablespaces as same as all tablespaces in the cluster system should be created in the cluster member.

The following is an example of adding a cluster group and a cluster member of the 3x2 cluster to the 2x1 cluster. Add the member G1N2 to the group G1, and add the member G2N2 to the group G2. Then, create the group G3 including the members (G3N1, G3N2).

- Add the member G1N2 to the group G1.

```
gSQL> 
ALTER CLUSTER GROUP G1 
      ADD CLUSTER MEMBER G1N2 HOST '192.168.0.12' PORT 10120;

Cluster Group altered.
```

- Add the member G2N2 to the group G2.

```
gSQL> 
ALTER CLUSTER GROUP G2 
      ADD CLUSTER MEMBER G2N2 HOST '192.168.0.22' PORT 10220;

Cluster Group altered.
```

- Create the group G3.

```
gSQL>
CREATE CLUSTER GROUP G3 
       CLUSTER MEMBER G3N1 HOST '192.168.0.31' PORT 10310,
       CLUSTER MEMBER G3N2 HOST '192.168.0.32' PORT 10320;

Cluster Group created.
```

The cluster group and the cluster member which are newly added to the cluster system can provide the service by synchronizing the dictionary information of the SQL object. However, the data is not yet placed in the added cluster member, so the availability can not be increased nor can the load balancing be expected. Therefore, the data should be rebalanced to the created cluster member for the high availability and the load balancing.

Use the following statements sequentially to rebalance the data.

- [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#e579543f77dce467)
- [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b)

The following is an example of rebalancing data to all tables in the database.

```
gSQL> ALTER DATABASE REBALANCE;

Database altered.
```

<a id="f5ebdd4895e74e15"></a>
## Cluster Group

<a id="6ddbf2e91ef6b748"></a>
### Cluster Group Related Statements

For more information about creating, dropping, and altering a cluster group, refer to the followings.

- Creating a cluster group: [CREATE CLUSTER GROUP](19-sql-references-c-g.md#57c6f6ae1e01e560)
- Dropping a cluster group: [DROP CLUSTER GROUP](19-sql-references-c-g.md#05c49f429ff9e7a5)
- Altering a cluster group: [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03)

Information which is related to a cluster group can be retrieved through the following views.

<a id="8630dce9a6eb6ce7"></a>
<table class="table column_count_3"><caption>Cluster group related information</caption><thead><tr><th class="to_center"><div>Schema</div></th><th class="to_center"><div>View</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>DICTIONARY_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#c944365990fbf691">DBA_CLUSTER</a></div></td><td class="to_middle"><div>Object information of a cluster group and a cluster member which configure the cluster</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#7ec8d9a1539c5557">DBA_CLUSTER_COMMENTS</a></div></td><td class="to_middle"><div>Comment information of a cluster group and a cluster member</div></td></tr></tbody></table>

<a id="9ae68b1d10b2a359"></a>
### Concepts of Cluster Group

At least one cluster group should be created to run the cluster system.

<a id="4c2258352d6e0f22"></a>
#### Creating Cluster Group

The first created cluster group should include itself as a cluster member. For more information about creating a cluster group, refer to [CREATE CLUSTER GROUP](19-sql-references-c-g.md#57c6f6ae1e01e560).

A cluster member is a physical concept meaning the data server, but a cluster group is a logical concept consisting of one or more cluster members.

The availability and load balancing of the cluster system depend on the configuration of the cluster group. The more cluster members the cluster group includes the higher the availability. The more the number of the cluster groups the bigger the throughput of the cluster system because the data is distributed.

All cluster members in a cluster group maintain the same data replications, so it can continuously provides the service unless an error occurs in all cluster members configuring a cluster group. It is recommended to configure the cluster group with two or more cluster members to maintain the availability of the cluster system.

The table data is sharded according to the sharding strategy, and it is stored and managed in each different cluster group according to the shard placement strategy. An appropriate table sharding strategy and the placement strategy according to the service feature determines the entire system performance. Each transaction and query is processed focusing on a cluster group in which the data is stored, so the performance is improved if the referenced data exist in the same cluster group.

<a id="baada89f133e7313"></a>
#### Dropping Cluster Group

The cluster group participating in a cluster system and providing a service can be dropped for various reasons. For more information about dropping the cluster group, refer to [DROP CLUSTER GROUP](19-sql-references-c-g.md#05c49f429ff9e7a5).

To drop the cluster group, all shards in a sharded table which is created in that cluster group should be transferred to another cluster group. It should be transferred separately according to cluster-wide, group-specific table.

<a id="382c2e039592e9f2"></a>
## Cluster Member

<a id="abff00a72294d593"></a>
### Cluster Member Related Statements

For more information, refer to the followings.

- Adding a cluster member: [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03)
- Dropping a cluster member: [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](18-sql-references-a-b.md#1f2538cb978d9370)
- Controlling a cluster member
    - [ALTER SYSTEM JOIN DATABASE](18-sql-references-a-b.md#7a98f890a10933e4)
    - [ALTER CLUSTER GROUP name OFFLINE MEMBER](18-sql-references-a-b.md#a9c296754fea8365)
    - [ALTER DATABASE RESET LOCAL CLUSTER MEMBER](18-sql-references-a-b.md#9d3ecfe5ef494e70)

Information which is related to a cluster member can be retrieved through the following views.

<a id="d6ee9fc89b461e67"></a>
<table class="table column_count_3"><caption>Cluster member related information</caption><thead><tr><th class="to_center"><div>Schema</div></th><th class="to_center"><div>View</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="2"><div>DICTIONARY_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#c944365990fbf691">DBA_CLUSTER</a></div></td><td class="to_middle"><div>Object information of a cluster group and a cluster member which configure a cluster</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#7ec8d9a1539c5557">DBA_CLUSTER_COMMENTS</a></div></td><td class="to_middle"><div>Comment information of a cluster group and a cluster member</div></td></tr><tr><td class="to_middle"><div>PERFORMANCE_VIEW_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#fffe98e088d63f51">V$CLUSTER_MEMBER</a></div></td><td class="to_middle"><div>Status information of a cluster member</div></td></tr></tbody></table>

<a id="f552d1c0128676cb"></a>
### Concepts of Cluster Member

The cluster member is a server configuring a cluster system, and it maintains the replications as same as those of cluster member in a cluster group.

The cluster member is a data server storing a part of the cluster database data, and it is also an application server processing the connection and request of an application. Moreover, it is a meta server duplicating and managing the meta information. In other words, GOLDILOCKS cluster does not require any data server, application server, or meta server.

Cluster members which belong to the same cluster group have the same data replications. Therefore, an error in a specific cluster member does not cause an error in the entire system. It is recommended to include two or more cluster members in each cluster group for the high availability of the system. A single cluster group can be configured with maximum 32 cluster members.

Perform [ALTER CLUSTER GROUP name ADD MEMBER](18-sql-references-a-b.md#7aeb1944a8c55e03) statement to add a new cluster member to a cluster group.

The added cluster member maintains the meta information of the SQL object as same as that in the cluster system, so it can process the connection and request of the application. However, the data is not placed, so adding a cluster member does not guarantee the high availability of the cluster group.

Perform the following statements to place the data after adding a cluster member.

- For rebalancing the entire data: Refer to [ALTER DATABASE REBALANCE](18-sql-references-a-b.md#e579543f77dce467).
- For rebalancing only a part of the table: Refer to [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b).

When an error occurs on a cluster member, service is continously provided but DDL can not be performed. For a normal service operation, an appropriate action should be taken for the cluster member with an error.

To make the cluster member with an error to participate in the cluster system again, then perform [ALTER SYSTEM JOIN DATABASE](18-sql-references-a-b.md#7a98f890a10933e4) statement after connecting to the cluster member and driving up to the LOCAL OPEN phase.

Even when a part of cluster members are not driven or the cluster system is driven while the network is disconnected, perform [ALTER SYSTEM JOIN DATABASE](18-sql-references-a-b.md#7a98f890a10933e4) statement after driving up the cluster member to the LOCAL OPEN phase.

If the cluster member device with an error can not be restored, then drop that cluster member by performing [ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS](18-sql-references-a-b.md#1f2538cb978d9370) statement in the cluster system.

The cluster member dropped from the cluster system still includes the previous information, and it can not participate in the cluster system again. Perform [ALTER DATABASE RESET LOCAL CLUSTER MEMBER](18-sql-references-a-b.md#9d3ecfe5ef494e70) statement to reset the cluster member to when it is before participating in the cluster system.

The statement above is different from newly creating the database of the cluster member because it maintains the tablespace information. Therefore, it can shorten the time to create the tablespace when adding a new cluster member to the cluster system.

<a id="f1a779d179af9a83"></a>
## Cluster Location

<a id="f528f3275f2993a6"></a>
### Cluster Location Related Statements

For more information about creating, dropping, and altering a cluster location, refer to the followings.

- Creating a cluster location: [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#f90d35ca160e7aaf)
- Dropping a cluster location: [DROP CLUSTER LOCATION](19-sql-references-c-g.md#5ee74e721fcc4b5b)
- Altering a cluster location: [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#8898b9d2fa2187e2)

Information which is related to a cluster location can be retrieved through the following views.

**Cluster location related information**

<a id="e2c5efa9f33d0184"></a>
| Schema | View | Description |
| --- | --- | --- |
| PERFORMANCE_VIEW_SCHEMA | [V$CLUSTER_LOCATION](../part-02-administration-manual/9-database-information.md#423135d4ca5ad1c9) | Information of cluster location |

<a id="841702eaf14ee1cb"></a>
### Concepts of Cluster Location

Cluster location is a connection information to connect the internal cluster networks of each cluster member registered on the cluster system. Each cluster members use the cluster-exclusive tcp network to transfer and receive various protocols such as the transaction processing and the exchanging the management information. In this case, the member name, host ip address, and port are used for the connection and they are called as a cluster location by the lump.

A unique cluster location information should be specified for each member, and if the information is duplicate, then the cluster network connection fails and the cluster system does not operate normally.

Cluster location information is automatically added or deleted when adding or dropping a cluster member, so a user rarely need to directly and solely add or delete the location information. However, DDL statement related to the cluster location can be used in the following case.

- When the cluster location information is lost due to the deleted location control file: [CREATE CLUSTER LOCATION](19-sql-references-c-g.md#f90d35ca160e7aaf)
- When the previously registered connection information of the cluster member is altered, which means that the hardware or the connected ip and port is altered: [ALTER CLUSTER LOCATION](18-sql-references-a-b.md#8898b9d2fa2187e2)

<a id="fc09584b2becfda9"></a>
## Cluster Table and Shard

<a id="b48a377421c07fd3"></a>
### Shard Related Statements

For more information about definition and rebalance of the shard, refer to the followings.

- Definition of a shard: &lt;table sharding strategy&gt; clause of [CREATE TABLE](19-sql-references-c-g.md#78614830d4f324f4).
- Rebalancing a shard: [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b)

Information which is related to a shard in a cluster table can be retrieved through the following views.

<a id="4b4b3f718fdb1139"></a>
<table class="table column_count_3"><caption>Shard in a cluster table related information </caption><thead><tr><th class="to_center"><div>Schema</div></th><th class="to_center"><div>View</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="8"><div>DICTIONARY_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#91c7d8e7b165cd13">ALL_CLUSTER_TABLES</a></div></td><td class="to_middle"><div>Information of user accessible cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#15f521dccf394061">ALL_SHARD_KEY_COLUMNS</a></div></td><td class="to_middle"><div>Shard key column information of user accessible cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#50045795e344458c">ALL_TAB_PLACE</a></div></td><td class="to_middle"><div>Placement information of user accessible cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#74b66d63ac0ae641">ALL_TAB_SHARDS</a></div></td><td class="to_middle"><div>Shard information of user accessible cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#7a6a63782540de1d">USER_CLUSTER_TABLES</a></div></td><td class="to_middle"><div>Information of user owned cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#9a9b25398e64dad7">USER_SHARD_KEY_COLUMNS</a></div></td><td class="to_middle"><div>Shard key column information of user owned cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#9ab464e8ab5dc8eb">USER_TAB_PLACE</a></div></td><td class="to_middle"><div>Placement information of user owned cluster table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#3e8fb597d4d1b321">USER_TAB_SHARDS</a></div></td><td class="to_middle"><div>Shard information of user owned cluster table</div></td></tr></tbody></table>

<a id="c77acc38826f059c"></a>
### Cluster Table Type

A table which is created by a user in a cluster environment is one of the followings.

- Cloned table: Equally duplicating the table data and managing it
- Sharded table: Horizontally sharding the table data and managing it

A cloned table is appropriate for a table such as a product list or a provider list whose data is relatively small and is not often altered, because a cloned table duplicates all table data and manages it. When inserting, deleting, updating data to the cloned table, they are applied same to all cluster members to which the cloned table is placed.

A sharded table is appropriate for a table such as a transaction history or a call history whose data is big so required to be sharded. They are classifed according to three sharding strategies as follows.

- Hash sharded table 
    - It divides the table data into several shards based on the hash value of a sharding key, then places them in the cluster system.
- Range sharded table
    - It divides the table data into several shards based on the range value of a sharding key, then places them in the cluster system.
- List sharded table
    - It divides the table data into several shards based on the list value of a sharding key, then places them in the cluster system.

A sharded table horizontally divides rows and manages them in shard unit, the sharding strategy is defined by using the SHARDING BY clause in [CREATE TABLE](19-sql-references-c-g.md#78614830d4f324f4) statement. The row set classified by the sharding strategy is called as shard.

Each shard is placed in a cluster group according to the placement strategy defined by a user. A shard can automatically be placed by using AT CLUSTER WIDE of [CREATE TABLE](19-sql-references-c-g.md#78614830d4f324f4), or a cluster group to place a shard can be specified by using AT CLUSTER GROUP clause. When a shard is automatically placed by using AT CLUSTER WIDE, [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b) is performed after creating the cluster group by using [CREATE CLUSTER GROUP](19-sql-references-c-g.md#57c6f6ae1e01e560). However, when specifying a cluster group to allocate a shard using AT CLUSTER GROUP, the shard is not placed in the newly created cluster group.

The following is an example of creating a table according to the cluster table type and placing the data in the 3x2 cluster environment.

<a id="174c27a8cc778297"></a>
### Cloned Table

A cloned table equally duplicates the table data and manages it.

The following is an example of creating a cluster-wide cloned table. All table data is equally duplicated and placed in 3x2 cluster members.

```
CREATE TABLE t1 ( id INTEGER )
   CLONED
   AT CLUSTER WIDE
;
```

<a id="82008809451b5099"></a>
![Cluster-wide cloned table](../assets/images/33ccf33db629628c.png)

The following is an example of creating a group-specific cloned table. All table data is equally duplicated and managed, but the duplicated table data exists only in cluster members of group g1 and g2 which are specified by a user, but it does not exist in a group g3.

```
CREATE TABLE t1 ( id INTEGER )
   CLONED
   AT CLUSTER GROUP g1, g2
;
```

<a id="95960b4310e9f41e"></a>
![Group-specific cloned table](../assets/images/43bb4d52bfedd781.png)

<a id="177d116ee98e287f"></a>
### Hash-sharded table

A hash-sharded table divides the table data into several shards based on the hash value of a sharding key, then places them in the cluster system.

The following is an example of creating the cluster-wide hash-sharded table. When adding data to a table, the hash value is created based on the ID column value, and the shard to place row is selected among five shards by using the hash value. Each shard is automatically placed. All rows with the same ID column value are included in the same shard, and placed in the same cluster group.

```
CREATE TABLE t1 ( id INTEGER )
   SHARDING BY HASH(id)
   SHARD COUNT 5
   AT CLUSTER WIDE
;
```

<a id="82c26da55ab85d4c"></a>
![Cluster-wide hash-sharded table](../assets/images/9bb52379a072c265.png)

The following is an example of creating the group-specific hash-sharded table. The hash value of an ID column determines the shard, but each shard is placed only in the cluster group g1 and g2 which are specified by a user.

```
CREATE TABLE t1 ( id INTEGER )
   SHARDING BY HASH(id)
   SHARD COUNT 5
   AT CLUSTER GROUP g1, g2
;
```

<a id="a8947b8462638e77"></a>
![Group-specific hash-sharded table](../assets/images/19e1f1ee62be53a1.png)

<a id="18372f50454e1f20"></a>
### Range-sharded Table

A range-sharded table divides the table data into several shards based on the range value of a sharding key, then places them in the cluster system.

The following is an example of creating the cluster-wide range-sharded table. When adding data to a table, the shard to place row is selected among five shards based on the range value of the ID column. Each shard is automatically placed. All rows of the ID column within the same range are included in the same shard, and placed in the same cluster group.

```
CREATE TABLE t1 ( id INTEGER )
   SHARDING BY RANGE(id)
   AT CLUSTER WIDE
       SHARD s1 VALUES LESS THAN ( 20 ),
       SHARD s2 VALUES LESS THAN ( 40 ),
       SHARD s3 VALUES LESS THAN ( 60 ),
       SHARD s4 VALUES LESS THAN ( 80 ),
       SHARD s5 VALUES LESS THAN ( MAXVALUE )
;
```

<a id="a9ba69d20911bb61"></a>
![Cluster-wide range-sharded table](../assets/images/f1001a3562e43bb1.png)

The following is an example of creating the group-specific range-sharded table. The range value of the ID column defines the shard, but each shard is placed in a cluster group specified by a user.

```
CREATE TABLE t1 ( id INTEGER )
   SHARDING BY RANGE(id)
       SHARD s1 VALUES LESS THAN ( 20 )       AT CLUSTER GROUP g1,
       SHARD s2 VALUES LESS THAN ( 40 )       AT CLUSTER GROUP g2,
       SHARD s3 VALUES LESS THAN ( 60 )       AT CLUSTER GROUP g1,
       SHARD s4 VALUES LESS THAN ( 80 )       AT CLUSTER GROUP g2,
       SHARD s5 VALUES LESS THAN ( MAXVALUE ) AT CLUSTER GROUP g3
;
```

<a id="0aeff9863ee39ab8"></a>
![Group-specific range-sharded table](../assets/images/0a01761263790019.png)

<a id="554a6051e02360a2"></a>
### List-sharded Table

A list-sharded table divides the table data into several shards based on the list value of a sharding key, then places them in the cluster system.

The following is an example of creating the cluster-wide list-sharded table. When adding data to a table, rows are placed in a shard with the list value as same as the CITY column value. Each shard is automatically placed.

```
CREATE TABLE t1 ( city VARCHAR(128) ) 
   SHARDING BY LIST (city)
      AT CLUSTER WIDE
      SHARD s1 VALUES IN ( 'seoul' ),
      SHARD s2 VALUES IN ( 'busan', 'ulsan' ),
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ),
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ),
      SHARD s5 VALUES IN ( DEFAULT )            
;
```

<a id="5fde91d7333f230c"></a>
![Cluster-wide list-sharded table](../assets/images/f747f6f785399227.png)

The following is an example of creating the group-specific list-sharded table. The shard is selected by the list value of the CITY column, but each shard is placed in the cluster group specified by a user.

```
CREATE TABLE t1 ( city VARCHAR(128) ) 
   SHARDING BY LIST (city)
      SHARD s1 VALUES IN ( 'seoul' )                  AT CLUSTER GROUP g1,
      SHARD s2 VALUES IN ( 'busan', 'ulsan' )         AT CLUSTER GROUP g2,
      SHARD s3 VALUES IN ( 'suwon', 'ansan', 'osan' ) AT CLUSTER GROUP g1,
      SHARD s4 VALUES IN ( 'goyang', 'paju', 'guri' ) AT CLUSTER GROUP g2,
      SHARD s5 VALUES IN ( DEFAULT )                  AT CLUSTER GROUP g3
;
```

<a id="00fc92636f9b6331"></a>
![Group-specific list-sharded table](../assets/images/1065dee5bc0e801f.png)

<a id="23f6c797402f073d"></a>
### Rebalancing Cluster Table

Rebalance the data of the cluster table by using [ALTER TABLE name REBALANCE](18-sql-references-a-b.md#a5e30678f94e116b) statement.

Data of the cluster table is rebalanced in the following unit.

- Cloned table: The entire table 
- Sharded table: shard unit

If the table is specified as AT CLUSTER WIDE, the shard is automatically rebalanced to the created cluster group, but if the cluster group to place the shard is specified by AT CLUSTER GROUP, the shard is not rebalanced to the created cluster group.

- When automatically rebalancing by using AT CLUSTER WIDE, then the data can be rebalanced to a new cluster group and a new cluster member.

```
CREATE TABLE region
(
    r_regionkey   INTEGER
  , r_name        CHAR(25)
  , r_comment     VARCHAR(152)
)
CLONED
AT CLUSTER WIDE;
```

<a id="17ae17cf94ae3232"></a>
![Rebalancing the region table defined by AT CLUSTER WIDE](../assets/images/1e8222bf752f26bc.png)

- When specifying the location to place the shard by using AT CLUSTER GROUP
    - The data is not rebalanced on the new cluster group.
    - The data can be rebalanced on the new cluster member which is added to the specified cluster group.

```
CREATE TABLE nation
(
    n_nationkey   INTEGER
  , n_name        CHAR(25)
  , n_regionkey   INTEGER
  , n_comment     VARCHAR(152)
)
CLONED
AT CLUSTER GROUP g1, g2;
```

<a id="2a797f75298c48d8"></a>
![Rebalancing the nation table defined by AT CLUSTER GROUP](../assets/images/81c052d38b200153.png)

Information about the table placement can be retrieved through the following views.

- [USER_TAB_PLACE](../part-02-administration-manual/9-database-information.md#9ab464e8ab5dc8eb)
- [ALL_TAB_PLACE](../part-02-administration-manual/9-database-information.md#50045795e344458c)

```
gSQL> 
SELECT group_name, member_name 
  FROM user_tab_place 
 WHERE table_name = 'REGION';

GROUP_NAME MEMBER_NAME
---------- -----------
G1         G1N1       
G1         G1N2       
G2         G2N1       
G2         G2N2       
G3         G3N1       
G3         G3N2       

6 rows selected.
```

The sharded table is rebalanced in shard unit, and rebalancing shards due to the increase of groups is as follows.

```
CREATE TABLE orders
(
    o_orderkey     INTEGER
  , o_custkey      INTEGER
  , o_orderstatus  CHAR(1)
  , o_totalprice   NUMERIC(12,2)
  , o_orderdate     DATE
  , o_orderpriority CHAR(15)
  , o_clerk        CHAR(15)
  , o_shippriority INTEGER
  , o_comment      VARCHAR(79)
)
SHARDING BY HASH( o_orderkey )
SHARD COUNT 24
AT CLUSTER WIDE
;
```

<a id="183bae8828f04051"></a>
![Rebalancing shards due to the increase of groups](../assets/images/92232aba7692d257.png)

In the example above, the data of orders table is divided into 24 shards and placed. All shards are placed in a single group of 1x cluster which has only one group. 12 shards are placed in each group of 2x cluster which has two groups.

When expanding 2x cluster to 3x cluster, shards are transferred from an old group to the new group, but the number of shards in each group is same (8). When expanding 3x cluster to 4x cluster, then each G1, G2, G3 rebalances two shards to the newly created group G4.

In other words, the shard rebalancing minimizes the movement when shards are transferred from an old group to the new group, then data is equally rebalanced maintaining the same number of shards in each group.

Information about the shard placement of the sharded table can be retrieved through the following views.

- [USER_TAB_SHARDS](../part-02-administration-manual/9-database-information.md#3e8fb597d4d1b321)
- [ALL_TAB_SHARDS](../part-02-administration-manual/9-database-information.md#74b66d63ac0ae641)

```
gSQL> 
SELECT shard_name, group_name 
  FROM user_tab_shards 
 WHERE table_name = 'ORDERS';

SHARD_NAME   GROUP_NAME
------------ ----------
SHARD_000000 G1        
SHARD_000001 G1        
SHARD_000002 G1        
SHARD_000003 G1        
SHARD_000004 G1        
SHARD_000005 G1        
SHARD_000006 G1        
SHARD_000007 G1        
SHARD_000008 G3        
SHARD_000009 G3        
SHARD_000010 G3        
SHARD_000011 G3        
SHARD_000012 G2        
SHARD_000013 G2        
SHARD_000014 G2        
SHARD_000015 G2        
SHARD_000016 G2        
SHARD_000017 G2        
SHARD_000018 G2        
SHARD_000019 G2        
SHARD_000020 G3        
SHARD_000021 G3        
SHARD_000022 G3        
SHARD_000023 G3        

24 rows selected.
```

When tables which have the same &lt;sharding strategy&gt; are completely rebalanced as follows, then the shard placement result is same. Rows with the same shard key are guaranteed to be placed in the same shard and the same group even when the tables are different.

- Table t1
    - It is created in the 2x cluster.
    - CREATE TABLE t1 ( c1 INTEGER ) SHARDING BY (c1);
    - It is rebalanced in the 4x cluster.
    - ALTER TABLE t1 REBALANCE:
- Table t2
    - It is created in the 3x cluster.
    - CREATE TABLE t2 ( a1 INTEGER ) SHARDING BY (a1);
    - It is rebalanced in the 4x cluster.
    - ALTER TABLE t2 REBALANCE:
- Table t3
    - It is created in the 4x cluster.
    - CREATE TABLE t3 ( i1 INTEGER ) SHARDING BY (i1);

In other words, the following query can access only to a single cluster member and process it.

```
SELECT COUNT(*)
  FROM t1, t2, t3
 WHERE t1.c1 = t2.a1
   AND t2.a1 = t3.i1
   AND t1.c1 = 1;
```

<a id="4ff66200d323c646"></a>
## Global Secondary Index

<a id="10c5bd38f6cb9219"></a>
### Global Secondary Index Related Statements

For more information about creating, dropping, and altering a global secondary index, refer to the followings.

- Creating a global secondary index: [ALTER TABLE name ADD GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#df41543d1fc55bb7)
- Dropping a global secondary index: [ALTER TABLE name DROP GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#ad40f305fca523f9)
- Altering a global secondary index: [ALTER TABLE name ALTER GLOBAL SECONDARY INDEX](18-sql-references-a-b.md#b06a5fa817400a3b)

Information related to a global secondary index can be retrieved through the following views.

<a id="8b8dae82884b974b"></a>
<table class="table column_count_3"><caption>Global secondary index related information</caption><thead><tr><th class="to_center"><div>Schema</div></th><th class="to_center"><div>View</div></th><th class="to_center"><div>Description</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="6"><div>DICTIONARY_SCHEMA</div></td><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#91c7d8e7b165cd13">ALL_CLUSTER_TABLES</a></div></td><td class="to_middle"><div>Existence of a global secondary index in user accessible table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#3c405f9eb4878efd">ALL_GLOBAL_SECONDARY_INDEXES</a></div></td><td class="to_middle"><div>Object information of user accessible global secondary index</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#1136123bdbe5d9eb">ALL_GSI_PLACE</a></div></td><td class="to_middle"><div>Placement information of user accessible global secondary index</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#7a6a63782540de1d">USER_CLUSTER_TABLES</a></div></td><td class="to_middle"><div>Existence of a global secondary index in user owned table</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#1df448488581026a">USER_GLOBAL_SECONDARY_INDEXES</a></div></td><td class="to_middle"><div>Object information of user owned global secondary index</div></td></tr><tr><td class="to_middle"><div><a class="reference" href="../part-02-administration-manual/9-database-information.md#8e8194788b369838">USER_GSI_PLACE</a></div></td><td class="to_middle"><div>Placement information of user owned global secondary index</div></td></tr></tbody></table>

<a id="604ffc4db9884f90"></a>
### Concepts of Global Secondary Index

A global secondary index is a B-Tree index which configures the GRID (global row identifier) value as a key in each cluster member of the cluster environment.

Tables in the cluster environment are duplicated to all members in a group and the same records are applied and retrieved when performing DML or select. GRID is a unique value identifying the same records in cluster members, and it is allocated when the record is inserted for the first time, and it is spread over all members in a group, then stored together with the record.

When creating a table in a cluster environment, a global secondary index may or may not be created, and it can be separately created or deleted after the table is created. A table may not have a global secondary index, or it may have maximum one global secondary index.

<a id="51163a1d93e79d7f"></a>
![Structure of a global secondary index](../assets/images/d2c5bc4d857a8437.png)

A global secondary index is required to perform a non-deterministic query for a table. If the table does not have a global secondary index, then the non-deterministic query fails as follows.

```
gSQL> DELETE FROM T1 LIMIT 1;

ERR-42000(16423): does not support non-deterministic DML in the cluster system : global secondary index expected
```

Refer to the dictionary such as ALL_GSI_PLACE, DBA_GSI_PLACE, and USER_GSI_PLACE to check if a table has a global secondary index.

---

[← 13. SQL Objects](13-sql-objects.md) · [Table of contents](../README.md) · [15. SQL Tuning →](15-sql-tuning.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
