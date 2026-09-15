<a id="68701c9504814bf4"></a>

# Appendix B. Wait Event

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/68701c9504814bf4)  
> Tag: `20c.1_30_tag`

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<a id="c39696cf626823a3"></a>
## Wait Event

Performance views which is related to the wait event is as follows.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#5eb4630598c0927e)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#b4fe4b32b4fe86c4)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#ad8d598a0fcca7f8)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#1407ca38ff6e0d2f)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#215d6de883bcc29c)

<a id="b7557b652c99e877"></a>
## Class of Wait Event

- Administrative: Waits resulting from DBA commands that cause users to wait (for example, an index rebuild)
- Application: Waits resulting from user application code (for example, lock waits caused by row level locking or explicit lock commands)
- Cluster: Waits related to cluster resources (for example, global cache resources )
- Commit: This wait class only comprises one wait event - wait for redo log write confirmation after a commit (that is, 'log file sync')
- Concurrency: Waits for internal database resources (for example, latches)
- Configuration: Waits caused by inadequate configuration of database or instance resources (for example, undersized log file sizes, shared pool size)
- Idle: Waits that signify the session is inactive, waiting for work (for example, 'gsql message from client')
- Network: Waits related to network messaging
- Other: Waits which should not typically occur on a system
- Scheduler: Resource manager related waits
- System IO: Waits for background process IO
- User IO: Waits for user IO

<a id="6f29b132b311c87e"></a>
## Item of Wait Event

<a id="8b4e0755c0beb646"></a>
### ENQUEUE: GDISPATCHER REQUEST

It is the time of which GDISPATCHER enqueues a request in a shared mode.  
Parameter: None

<a id="5d510a3c366e995e"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

It is the time of which a shared server enqueues a response in a shared mode.  
Parameter: None

<a id="cfa7bff375d6f50f"></a>
### DEQUEUE: SHARED-SERVER REQUEST

It is the time of which a shared server dequeues a request in a shared mode.  
Parameter: None

<a id="95f04cc05b7c3ed7"></a>
### DEQUEUE: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER dequeues a response in a shared mode.  
Parameter: None

<a id="0b0e85361a077d8a"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

It is the time of which a dedicate server sends the spooled response to the client in a dedicate mode.

**PARAMETER**

<a id="b9e51163fc240172"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="e45ec1d718df5bcb"></a>
### SEND: DEDICATE-SERVER RESPONSE

It is the time of which a dedicate server sends a response to the client in a dedicate mode.

**Parameter**

<a id="f3f89ad97cdcb431"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="75479a95e47b13fe"></a>
### RECV: DEDICATE-SERVER REQUEST

It is the time of which a dedicate server receives a request from the client in a dedicate mode.  
Parameter: None

<a id="c8d9298287683e4f"></a>
### SEND: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER sends a response to a client in a shared mode.

**Parameter**

<a id="2fadce74b046cc49"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="37f87571d14799e2"></a>
### RECV: GDISPATCHER REQUEST

It is the time of which GDISPATCHER receives a request from a client in a shared mode.  
Parameter: None

<a id="d4aeefbcd3cdf50a"></a>
### ENQUEUE: CLUSTER REQUEST

It is the time of enqueuing a request of cluster.  
Parameter: None

<a id="3f63a16fdc1a0dc9"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

It is the time of enqueuing a broadcast request of cluster.  
Parameter: None

<a id="7888095723658d6a"></a>
### DEQUEUE: CLUSTER RESPONSE

It is the time of dequeuing a response of cluster.  
Parameter: None

<a id="bc969dea52df6509"></a>
### SEND: CDISPATCHER

It is the time of sending in cluster CDISPATCHER.  
Parameter: None

<a id="6cee2bf2147238b2"></a>
### RECV: CDISPATCHER

It is the time of receiving in cluster CDISPATCHER.  
Parameter: None

<a id="58c1c8c193594264"></a>
### GMASTER: ARCHIVE LOG

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="5ad929692944e382"></a>
### GMASTER: CHECKPOINT

It is the time of processing checkpoints in gmaster.  
Parameter: None

<a id="58f25529492c1c18"></a>
### GMASTER: IO SLAVE

It is the time of processing IO slave in gmaster.  
Parameter: None

<a id="e41ce9398c4eb8ae"></a>
### GMASTER: LOG FLUSH

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="e3630debd9e21ce2"></a>
### GMASTER: PAGE FLUSH

It is the time of processing page flush in gmaster.  
Parameter: None

<a id="615f02bf00c8fb00"></a>
### WRITE: TRACE LOG

It is the time of writing trace logs.  
Parameter: None

<a id="2fe7fea1493b9a72"></a>
### WRITE: COPY ARCHIVING LOG

It is the time of copying archiving logs.  
Parameter: None

<a id="fc096b51344ccdd2"></a>
### WRITE: BACKUP CTRL FILE

It is the time of backing up control files.  
Parameter: None

<a id="686f98f954cd20e8"></a>
### WRITE: RESTORE CTRL FILE

It is the time of restoring the control file.  
Parameter: None

<a id="b1cff461cdd9d148"></a>
### READ: ARCHIVE LOG

It is the time of reading archive log files.  
Parameter: None

<a id="480f70e1a2cd9a79"></a>
### READ: CTRL FILE

It is the time of reading the control file.  
Parameter: None

<a id="a9778f879aae35e7"></a>
### WRITE: LOG FILE

It is the time of writing log files.  
Parameter: None

<a id="c2b183e444c54f81"></a>
### WRITE: PAGE FILE

It is the time of writing page files.  
Parameter: None

<a id="b742b442c73a60be"></a>
### WRITE: CTRL FILE

It is the time of writing the control file.  
Parameter: None

<a id="129e8621c6d4acf6"></a>
### WRITE: REMOVE DATA FILE

It is the time of removing the data file.  
Parameter: None

<a id="b5c36e9e65e88b4a"></a>
### WRITE: JOURNAL BUFFER

It is the time of writing journal buffers.  
Parameter: None

<a id="0c64f77b176fe3da"></a>
### READ: JOURNAL BUFFER

It is the time of reading journal buffers.  
Parameter: None

<a id="37b240f008a4ca50"></a>
### WAIT TRANSACTION

It is the time of waiting for transactions.

**Parameter**

<a id="a5bd7d43d0384ecc"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | Transaction id for which to wait |

<a id="18f0fd9f3f8d8af5"></a>
### WAIT OTHER TRANSACTION

It is the time of waiting for other transactions to be terminated.

**Parameter**

<a id="201e52c7c82e9fb1"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | ID of the waiting transaction |
| target transaction id | ID of the transaction to be terminated |

<a id="286f54c4a0c219d4"></a>
### WAIT ENABLE LOGGING

It is the time of waiting until when the logging is available.  
Parameter: None

<a id="3e102ea80a1c342d"></a>
### WAIT LOG FLUSHER

It is the time of waiting for the log flusher.

**Parameter**

<a id="5596251a129b4335"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="91a9e8f7e7ba6057"></a>
### WAIT PAGE FLUSHER

It is the time of waiting for the page flusher.

**Parameter**

<a id="2e762cc14fba00ee"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="3d1ebb058e4ae8f1"></a>
### WAIT XA CONTEXT

It is the time of waiting for the XA context.  
Parameter: None

<a id="b43115e392c93aa7"></a>
### LATCH: LOG BUFFER

It is the time of waiting for the log buffer latch.

**Parameter**

<a id="98fc3b115e503f68"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e5da68ed8301399b"></a>
### LATCH: PROCESS MANAGER

It is the time of waiting for the process manager latch.

**Parameter**

<a id="722f1e5286a1ad66"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c5fb26404f7c5fd0"></a>
### LATCH: ENV MGR

It is the time of waiting for the env manager latch.

**Parameter**

<a id="56818f80b198a8af"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e278e111f447d06a"></a>
### LATCH: SESSION ENV MGR

It is the time of waiting for the session env manager latch.

**Parameter**

<a id="38cf48f78ed147a0"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="78ae86a3781aa37b"></a>
### LATCH: PCH

It is the time of waiting for the Page Control Header (PCH) latch.

**Parameter**

<a id="0f58fb00ddeda51c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e5d276c8d327a64e"></a>
### LATCH: PAGE

It is the time of waiting for the page latch.

**Parameter**

<a id="8157b45cfa31f5f4"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="eae319b033fecef9"></a>
### LATCH: PENDING LOG

It is the time of waiting for the pending log latch.

**PARAMETER**

<a id="e201f31f8fea7f02"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1a719aa3073d9189"></a>
### LATCH: ALLOC TRANS

It is the time of waiting for the allocate transaction latch.

**PARAMETER**

<a id="11b9bd374532ba14"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5b858f8c8efe381e"></a>
### LATCH: UNDO SEGMENT

It is the time of waiting for the undo segment latch.

**PARAMETER**

<a id="e2ecf41f480faa88"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="744c0263c94d57ea"></a>
### LATCH: CLUSTER LOCATION

It is the time of waiting for the cluster location latch.

**PARAMETER**

<a id="187060eca1dbe5d1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ba612cf8ff12f865"></a>
### LATCH: DICT HASH ELEMENT AGING

It is the time of waiting for the dict hash element aging latch.

**PARAMETER**

<a id="61a99bd75b7a4f57"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="90881aab37784707"></a>
### LATCH: DICT HASH RELATED AGING

It is the time of waiting for the dict hash related aging latch.

**PARAMETER**

<a id="ceb0edd52fe2c212"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="10661b0c5d88a97a"></a>
### LATCH: FILE MANAGER

It is the time of waiting for the file manager latch.

**PARAMETER**

<a id="5d5c1d0a22149bf0"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cf790928b2c5b3da"></a>
### LATCH: TRACE LOG

It is the time of waiting for the trace log latch.

**PARAMETER**

<a id="06c32abecb267053"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a5699525c2913014"></a>
### LATCH: STATIC HASH

It is the time of waiting for the static hash latch.

**PARAMETER**

<a id="277d76b296cba792"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="764c5f7ad44393b0"></a>
### LATCH: STATIC HASH BUCKET

It is the time of waiting for the static hash bucket latch.

**PARAMETER**

<a id="a83daa1076e0959c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="70b81c783b34e187"></a>
### LATCH: SQL HANDLE

It is the time of waiting for SQL handle latch.

**PARAMETER**

<a id="0379452e2147ce2c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6566aac6e1373273"></a>
### LATCH: XA CONTEXT HASH

It is the time of waiting for XA context hash latch.

**PARAMETER**

<a id="3ccd59caa96d2f8a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ebbf0677b708342a"></a>
### LATCH: PLAN CLOCK

It is the time of waiting for the plan clock latch.

**PARAMETER**

<a id="70fef9879f11c9ec"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b9d46b7346a4509c"></a>
### LATCH: XA CONTEXT

It is the time of waiting for XA context latch.

**PARAMETER**

<a id="3ffc7bbb257b2064"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dd5eda2ea3534565"></a>
### LATCH: MEM CONTROLLER

It is the time of waiting for the memory controller latch.

**PARAMETER**

<a id="c80be53a32bce204"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="34a3500bd3303d2c"></a>
### LATCH: DYNAMIC MEM

It is the time of waiting for the dynamic memory latch.

**PARAMETER**

<a id="d1f4727788ef783d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3489eb29ed2198b5"></a>
### LATCH: PROPERTY

It is the time of waiting for the property latch.

**PARAMETER**

<a id="28372c81f5166ca7"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5af980e3a4a29763"></a>
### LATCH: ATTACH SHM

It is the time of waiting for the attack shared memory latch.

**PARAMETER**

<a id="fbc864453e3e69d5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="44d13056d17912bb"></a>
### LATCH: BACKUP TBS

It is the time of waiting for the backup tablespace latch.

**PARAMETER**

<a id="eccb2339bb3c587f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4c12621e644cf99c"></a>
### LATCH: DATABASE COMPONENT

It is the time of waiting for the database component latch.

**PARAMETER**

<a id="d9cc5ed4081bad55"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="10e6ef39fa34f926"></a>
### LATCH: TABLESPACE

It is the time of waiting for the tablespace latch.

**PARAMETER**

<a id="64535dcc053c28af"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dc7e87aaa574b2ed"></a>
### LATCH: BACKUP DATABASE

It is the time of waiting for the backup database latch.

**PARAMETER**

<a id="c312fddec30aedae"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ff12351aedfa3113"></a>
### LATCH: JOURNAL BUFFER

It is the time of waiting for the journal buffer latch.

**PARAMETER**

<a id="61ef27fd60826e65"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cea52d7159d4da0c"></a>
### LATCH: JOURNAL BUFFER ENTRY

It is the time of waiting for the journal buffer entry latch.

**PARAMETER**

<a id="039ed5dd121c7653"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="be9a6682746ca676"></a>
### LATCH: JOURNAL WRITE BUFFER

It is the time of waiting for the journal write buffer latch.

**PARAMETER**

<a id="8a306032fd1a7246"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="34b2f689501e5c87"></a>
### LATCH: LOCK ITEM

It is the time of waiting for the lock item latch.

**PARAMETER**

<a id="a314435e1f04e6b2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a3f78eee6cd1352b"></a>
### LATCH: RECORD HASH

It is the time of waiting for the record hash latch.

**PARAMETER**

<a id="ca3deb31d59e1233"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="259eb88744003d9f"></a>
### LATCH: DEADLOCK

It is the time of waiting for the deadlock latch.

**PARAMETER**

<a id="246cc204661c6960"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="60c3043f02a35d3d"></a>
### LATCH: SEQUENCE

It is the time of waiting for the sequence latch.

**PARAMETER**

<a id="5bf64a2b1cc77250"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8f54ae92fe768fc7"></a>
### LATCH: LOG STREAM

It is the time of waiting for the log stream latch.

**PARAMETER**

<a id="03eab1ecdb458a3c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8838b186a633f256"></a>
### LATCH: BUILD AGABLE SCN

It is the time of waiting for the build agable SCN latch.

**PARAMETER**

<a id="4ca7be4ef8a827b3"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c42222b442057d9b"></a>
### LATCH: TRANSACTION TABLE

It is the time of waiting for the transaction table latch.

**PARAMETER**

<a id="5a6d2b0f0e5cac94"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="752858cd0aa56779"></a>
### LATCH: SESSION LINK HASH

It is the time of waiting for the session link hash latch.

**PARAMETER**

<a id="5fabe49df5ec40b5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="82601b5e9d94e1d4"></a>
### LATCH: ALLOC XA CONTEXT

It is the time of waiting for the allocate XA context latch.

**PARAMETER**

<a id="29676befd4f6ad3b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="17ed976cec518a0b"></a>
### LATCH: SEQUENCE GLOBALX

It is the time of waiting for the sequence global latch X.

**PARAMETER**

<a id="0cb4460e11633a2d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="fe1fe70a75eecd9b"></a>
### LATCH: SEQUENCE GLOBALY

It is the time of waiting for the sequence global latch Y.

**PARAMETER**

<a id="3ed3e20f3a576a61"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a58a01d17af3d4de"></a>
### LATCH: TRANSACTION LOG FILE

It is the time of waiting for the transaction logfile latch.

**PARAMETER**

<a id="88f01515aee8879d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
