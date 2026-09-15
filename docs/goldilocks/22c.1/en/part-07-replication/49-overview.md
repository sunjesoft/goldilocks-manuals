<a id="a8cd1175a6766bf7"></a>

# 49. Overview

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/a8cd1175a6766bf7)  
> Tag: `22c.1_10_tag`

[← 48. gloctl](../part-06-utility-manual/48-gloctl.md) · [Table of contents](../README.md) · [50. CYCLONE →](50-cyclone.md)

<a id="306a0bc3e3d7d9ec"></a>
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

<a id="9d96e8933c5b4570"></a>
## Characteristics

<a id="d6fbc65a847df3d0"></a>
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

<a id="8ea9dd030132798e"></a>
### LOGMIRROR

The followings are the characteristics of LOGMIRROR.

- It transfers and stores the redo logs of the original database to the remote machine without any loss.
- It interworks with CYCLONE and replicates without any loss of data. 
- Only one LOGMIRROR can be operated in a database.
- It is operated being divided into master and slave.

<a id="bfd99d04dd19826e"></a>
### CYFILE

The followings are features of CYFILE.

- It uses Change Data Capture (CDC) method.
- It recognizes and analyzes updates in the redo log file of the original database.
- It captures in the unit of table.
- The process is independently operated, so GOLDILOCKS is not affected even when an error occurs. 
- It supports standalone environment and cluster environment.

---

[← 48. gloctl](../part-06-utility-manual/48-gloctl.md) · [Table of contents](../README.md) · [50. CYCLONE →](50-cyclone.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
