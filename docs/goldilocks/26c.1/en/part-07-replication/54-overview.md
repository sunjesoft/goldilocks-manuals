<a id="2718c1f7abb2c5a3"></a>

# 54. Overview

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/2718c1f7abb2c5a3)  
> Tag: `26c.1_0_tag`

[← 53. gloctl](../part-06-utility-manual/53-gloctl.md) · [Table of contents](../README.md) · [55. CYCLONE →](55-cyclone.md)

<a id="fba76bf8bbb1a3af"></a>
## Overview of GOLDILOCKS Replication

Database replication efficiently and consistently distributes data for data recovery when an error occurs in the original database by using the remote database, so that it enables sustained service. It is also used to build multiple database with same data.

GOLDILOCKS replication supports CYCLONE, which is a tool using Change Data Capture (CDC) method.

> Change Data Capture (CDC)  
> This method captures and analyzes the redo log generated during the database operation, and performs the replication.   
> Only the asynchronous mode is supported because CYCLONE is available after the changes of the database are stored in the redo log file.

The interval may occur between the original database and the remote database of the replication because CDC method supports only the asynchronous mode. When the failure of original database or equipment occurs in the state of which the replication to the remote database is not completed, the remote database is in the state of which the interval is not reflected.

LOGMIRROR can be used to complement the data not reflected due to the interval of the asynchronous mode.

> LOGMIRROR is a tool which replicates the redo log files. It sends and stores the redo logs generated from the original database to the remote equipment without any loss of data. Therefore, using LOGMIRROR can prevent loss of data.

It provides CYFILE tool storing the transaction data which was processed and committed in the database in Comma-Separated Values (CSV) format file by using CDC method. A user can directly process the data by using the stored file or converts the data according to its purpose.

> CYFILE directly captures the redo log file by using CDC method and analyzes the transaction in real time, then stores the contents in CSV format file.

<a id="4484183e26315b1c"></a>
## Characteristics

<a id="b48e0a9a01819c38"></a>
### CYCLONE

The following are the characteristics of CYCLONE.

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

<a id="6eac8cd8ba5133ac"></a>
### LOGMIRROR

The following are the characteristics of LOGMIRROR.

- It transfers and stores the redo logs of the original database to the remote machine without any loss.
- It interworks with CYCLONE and replicates without any loss of data. 
- Only one LOGMIRROR can be operated in a database.
- It is operated being divided into master and slave.

<a id="487fcb57dcf760f8"></a>
### CYFILE

The following are features of CYFILE.

- It uses Change Data Capture (CDC) method.
- It recognizes and analyzes updates in the redo log file of the original database.
- It captures in the unit of table.
- The process is independently operated, so GOLDILOCKS is not affected even when an error occurs. 
- It supports standalone environment and cluster environment.

---

[← 53. gloctl](../part-06-utility-manual/53-gloctl.md) · [Table of contents](../README.md) · [55. CYCLONE →](55-cyclone.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
