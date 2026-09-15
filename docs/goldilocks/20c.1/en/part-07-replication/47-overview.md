<a id="6a441da770703b9b"></a>

# 47. Overview

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/6a441da770703b9b)  
> Tag: `20c.1_30_tag`

[← 46. gloctl](../part-06-utility-manual/46-gloctl.md) · [Table of contents](../README.md) · [48. CYCLONE →](48-cyclone.md)

<a id="eca83fa4808ee5ad"></a>
## Overview of GOLDILOCKS Replication

Database replication efficiently and consistently distributes data for data recovery when an error occurs in the original database by using the remote database, so that it enables sustained service. It is also used to build multiple database with same data.

GOLDILOCKS replication supports CYCLONE, which is a tool using Change Data Capture (CDC) method.

> Change Data Capture (CDC)  
> This method captures and analyzes the redo log generated during the database operation, and performs the replication.   
> Only the asynchronous mode is supported because CYCLONE is available after the changes of the database are stored in the redo log file.

The interval may occur between the original database and the remote database of the replication because CDC method supports only the asynchronous mode. When the failure of original database or equipment occurs in the state of which the replication to the remote database is not completed, the remote database is in the state of which the interval is not reflected.

LOGMIRROR can be used to complement the data not reflected due to the interval of the asynchronous mode.

> LOGMIRROR is a tool which replicates the redo log files. It sends and stores the redo logs generated from the original database to the remote equipment without any loss of data. Therefore, using LOGMIRROR can prevent loss of data.

<a id="989d3457d89dc9a4"></a>
## Characteristics

<a id="8b3fc519c73462eb"></a>
### CYCLONE

The followings are the characteristics of CYCLONE.

- It is a replication tool which uses Change Data Capture (CDC) method.
- It recognizes, analyzes and applies the changes in redo log files of the original database. 
- It is operated being divided into master and slave.
- It supports active-active, active-standby.
- Replication is available in table unit.
- Several options can be set to improve the performance.
- It does not affect GOLDILOCKS in case of failure because it is operated as an independent process.
- Adding or changing the H/W is not required for operation. 
- It allows various replication topology 
- The operation between master and slave in standalone environment supports the relationship of 1 : 1 or N : N.
- The operation between master and slave in cluster environment supports the relationship of N : 1.

<a id="2f7561ddf42de5c8"></a>
### LOGMIRROR

The followings are the characteristics of LOGMIRROR.

- It transfers and stores the redo logs of the original database to the remote machine without any loss.
- It interworks with CYCLONE and replicates without any loss of data. 
- Only one LOGMIRROR can be operated in a database.
- It is operated being divided into master and slave.

---

[← 46. gloctl](../part-06-utility-manual/46-gloctl.md) · [Table of contents](../README.md) · [48. CYCLONE →](48-cyclone.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
