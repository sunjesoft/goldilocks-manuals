<a id="8cceb588ee312996"></a>

# Appendix B. Wait Event

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/8cceb588ee312996)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<a id="eb0579dc55240c03"></a>
## Wait Event

Performance views which is related to the wait event is as follows.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#b7b984cfc1731725)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#80e91c211204a7b6)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#f9bc7b650b276801)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#53df1e5560ed6393)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#e609fc9cdab47c32)

<a id="9283ab664c4c07e4"></a>
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

<a id="eb569b76f344e3af"></a>
## Item of Wait Event

<a id="a972d12547a22a83"></a>
### ENQUEUE: GDISPATCHER REQUEST

It is the time of which GDISPATCHER enqueues a request in a shared mode.  
Parameter: None

<a id="b8f05532c386f3a8"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

It is the time of which a shared server enqueues a response in a shared mode.  
Parameter: None

<a id="5cdf382d317593e5"></a>
### DEQUEUE: SHARED-SERVER REQUEST

It is the time of which a shared server dequeues a request in a shared mode.  
Parameter: None

<a id="a3b29d03f683ef58"></a>
### DEQUEUE: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER dequeues a response in a shared mode.  
Parameter: None

<a id="41a2017124e6316e"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

It is the time of which a dedicate server sends the spooled response to the client in a dedicate mode.

**PARAMETER**

<a id="f84dc0ba81e5d1d9"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="5e4593f8fa28666e"></a>
### SEND: DEDICATE-SERVER RESPONSE

It is the time of which a dedicate server sends a response to the client in a dedicate mode.

**Parameter**

<a id="08fdad609b7b5ee9"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="3dcff4148670f499"></a>
### RECV: DEDICATE-SERVER REQUEST

It is the time of which a dedicate server receives a request from the client in a dedicate mode.  
Parameter: None

<a id="93af0ea5257e6444"></a>
### SEND: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER sends a response to a client in a shared mode.

**Parameter**

<a id="426dbbe940fdc510"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="a3d70b35f69d24bf"></a>
### RECV: GDISPATCHER REQUEST

It is the time of which GDISPATCHER receives a request from a client in a shared mode.  
Parameter: None

<a id="d255263e920d30cc"></a>
### ENQUEUE: CLUSTER REQUEST

It is the time of enqueuing a request of cluster.  
Parameter: None

<a id="6b059e49c460da8b"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

It is the time of enqueuing a broadcast request of cluster.  
Parameter: None

<a id="9de1ba58ce20162d"></a>
### DEQUEUE: CLUSTER RESPONSE

It is the time of dequeuing a response of cluster.  
Parameter: None

<a id="bcec3e244feaeab9"></a>
### SEND: CDISPATCHER

It is the time of sending in cluster CDISPATCHER.  
Parameter: None

<a id="998bf69ce0aef657"></a>
### RECV: CDISPATCHER

It is the time of receiving in cluster CDISPATCHER.  
Parameter: None

<a id="65a40e64c1a5243f"></a>
### GMASTER: ARCHIVE LOG

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="dcae06960378b3d8"></a>
### GMASTER: CHECKPOINT

It is the time of processing checkpoints in gmaster.  
Parameter: None

<a id="cbd037cad4878a9f"></a>
### GMASTER: IO SLAVE

It is the time of processing IO slave in gmaster.  
Parameter: None

<a id="522c8f70e87c9719"></a>
### GMASTER: LOG FLUSH

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="a2592739057be7ff"></a>
### GMASTER: PAGE FLUSH

It is the time of processing page flush in gmaster.  
Parameter: None

<a id="4247e7508034d2c3"></a>
### WRITE: TRACE LOG

It is the time of writing trace logs.  
Parameter: None

<a id="e1de9b216b9ce404"></a>
### WRITE: COPY ARCHIVING LOG

It is the time of copying archiving logs.  
Parameter: None

<a id="b5ee1755839409f2"></a>
### WRITE: BACKUP CTRL FILE

It is the time of backing up control files.  
Parameter: None

<a id="7f124fdbf35b8da4"></a>
### WRITE: RESTORE CTRL FILE

It is the time of restoring the control file.  
Parameter: None

<a id="7b2e410b3a236a2a"></a>
### READ: ARCHIVE LOG

It is the time of reading archive log files.  
Parameter: None

<a id="6ae7874d045d2834"></a>
### READ: CTRL FILE

It is the time of reading the control file.  
Parameter: None

<a id="61bcd52779af1380"></a>
### WRITE: LOG FILE

It is the time of writing log files.  
Parameter: None

<a id="836a362298932645"></a>
### WRITE: PAGE FILE

It is the time of writing page files.  
Parameter: None

<a id="5f99fc442eb14e0f"></a>
### WRITE: CTRL FILE

It is the time of writing the control file.  
Parameter: None

<a id="9b43a228e98c4aba"></a>
### WRITE: REMOVE DATA FILE

It is the time of removing the data file.  
Parameter: None

<a id="274d8381b22e174c"></a>
### WRITE: JOURNAL BUFFER

It is the time of writing journal buffers.  
Parameter: None

<a id="af419f372df35b35"></a>
### READ: JOURNAL BUFFER

It is the time of reading journal buffers.  
Parameter: None

<a id="3797c1d1857a7eb0"></a>
### WAIT TRANSACTION

It is the time of waiting for transactions.

**Parameter**

<a id="0edf3d7b29a21076"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | Transaction id for which to wait |

<a id="9dafef3f6551ccee"></a>
### WAIT OTHER TRANSACTION

It is the time of waiting for other transactions to be terminated.

**Parameter**

<a id="4f1c92e5bcbc7260"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | ID of the waiting transaction |
| target transaction id | ID of the transaction to be terminated |

<a id="0e4a21942a4a60f9"></a>
### WAIT ENABLE LOGGING

It is the time of waiting until when the logging is available.  
Parameter: None

<a id="bf3e2e2469ebfec2"></a>
### WAIT LOG FLUSHER

It is the time of waiting for the log flusher.

**Parameter**

<a id="6fa75c8825479aa7"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="8ead94d057e26097"></a>
### WAIT PAGE FLUSHER

It is the time of waiting for the page flusher.

**Parameter**

<a id="c97c4c4a9a383546"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="b17ba77d135ec4db"></a>
### WAIT XA CONTEXT

It is the time of waiting for the XA context.  
Parameter: None

<a id="a99bc7c5f65e824d"></a>
### LATCH: LOG BUFFER

It is the time of waiting for the log buffer latch.

**Parameter**

<a id="28aa09879f9fbf14"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5581a1c259ec0b48"></a>
### LATCH: PROCESS MANAGER

It is the time of waiting for the process manager latch.

**Parameter**

<a id="be77d83fecf93851"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="43acd5aaaa819590"></a>
### LATCH: ENV MGR

It is the time of waiting for the env manager latch.

**Parameter**

<a id="c73d4af30c136210"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="399a5e82662f9c37"></a>
### LATCH: SESSION ENV MGR

It is the time of waiting for the session env manager latch.

**Parameter**

<a id="bc15b4dab7d4b808"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="75be5ee0c49afc3f"></a>
### LATCH: PCH

It is the time of waiting for the Page Control Header (PCH) latch.

**Parameter**

<a id="fbd6a7f584010e26"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ef3a5d0ded0baf0a"></a>
### LATCH: PAGE

It is the time of waiting for the page latch.

**Parameter**

<a id="3344c4428ff08169"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0c2de63b2ee4e70c"></a>
### LATCH: PENDING LOG

It is the time of waiting for the pending log latch.

**PARAMETER**

<a id="d2e182966958e8fc"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="40d4852f8268898d"></a>
### LATCH: ALLOC TRANS

It is the time of waiting for the allocate transaction latch.

**PARAMETER**

<a id="20013613c11e7363"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bcfaad6caa8fe2a5"></a>
### LATCH: UNDO SEGMENT

It is the time of waiting for the undo segment latch.

**PARAMETER**

<a id="ccdd279b61994916"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="262e7942f9db6acc"></a>
### LATCH: CLUSTER LOCATION

It is the time of waiting for the cluster location latch.

**PARAMETER**

<a id="27f314065cf2a854"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d7b9863d3ddb18ff"></a>
### LATCH: DICT HASH ELEMENT AGING

It is the time of waiting for the dict hash element aging latch.

**PARAMETER**

<a id="c8d2251355e20c64"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ffebc83540952d43"></a>
### LATCH: DICT HASH RELATED AGING

It is the time of waiting for the dict hash related aging latch.

**PARAMETER**

<a id="285d8bf2c7b1e51d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0f5b869339986fc4"></a>
### LATCH: FILE MANAGER

It is the time of waiting for the file manager latch.

**PARAMETER**

<a id="d1439c2e6bd2cdcc"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="81c02e4f623f7634"></a>
### LATCH: TRACE LOG

It is the time of waiting for the trace log latch.

**PARAMETER**

<a id="c27728948cc5734b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2b2a047a5d5fcd28"></a>
### LATCH: STATIC HASH

It is the time of waiting for the static hash latch.

**PARAMETER**

<a id="93156a99ac31150d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cbf2f5243339ff90"></a>
### LATCH: STATIC HASH BUCKET

It is the time of waiting for the static hash bucket latch.

**PARAMETER**

<a id="3d4fc867d14e61c1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a02e81e8559368c0"></a>
### LATCH: SQL HANDLE

It is the time of waiting for SQL handle latch.

**PARAMETER**

<a id="a5c1193f0c3e25d8"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="33f91cfe6d14131a"></a>
### LATCH: XA CONTEXT HASH

It is the time of waiting for XA context hash latch.

**PARAMETER**

<a id="3e098f6528498622"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f0c612a19d3ee6a4"></a>
### LATCH: PLAN CLOCK

It is the time of waiting for the plan clock latch.

**PARAMETER**

<a id="b980c6a6f3340215"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6da1980fdfcf89dc"></a>
### LATCH: XA CONTEXT

It is the time of waiting for XA context latch.

**PARAMETER**

<a id="f8bd44ef34d603a9"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9abb3d7294302c8a"></a>
### LATCH: MEM CONTROLLER

It is the time of waiting for the memory controller latch.

**PARAMETER**

<a id="9eed419f0aa69c1b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="27a3ba3764f51e9b"></a>
### LATCH: DYNAMIC MEM

It is the time of waiting for the dynamic memory latch.

**PARAMETER**

<a id="b1b48fe6eaca6a98"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4005f54277b9ae4c"></a>
### LATCH: PROPERTY

It is the time of waiting for the property latch.

**PARAMETER**

<a id="f81a5d7b221875da"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ffcdc35a73af2f17"></a>
### LATCH: ATTACH SHM

It is the time of waiting for the attack shared memory latch.

**PARAMETER**

<a id="ecf381301b741620"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c2d9b2aaa0d7de97"></a>
### LATCH: BACKUP TBS

It is the time of waiting for the backup tablespace latch.

**PARAMETER**

<a id="fc05a78316342319"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="80c8180f971cdb6b"></a>
### LATCH: DATABASE COMPONENT

It is the time of waiting for the database component latch.

**PARAMETER**

<a id="c33d90e37962615f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f17abe84bc1c81a6"></a>
### LATCH: TABLESPACE

It is the time of waiting for the tablespace latch.

**PARAMETER**

<a id="913854e68204ab44"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4df4e613732bead1"></a>
### LATCH: BACKUP DATABASE

It is the time of waiting for the backup database latch.

**PARAMETER**

<a id="59b243ea2e538a8e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6edfe3b2e98dbab9"></a>
### LATCH: JOURNAL BUFFER

It is the time of waiting for the journal buffer latch.

**PARAMETER**

<a id="0feafa6c03372cec"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b639301ffdfc6130"></a>
### LATCH: JOURNAL BUFFER ENTRY

It is the time of waiting for the journal buffer entry latch.

**PARAMETER**

<a id="05babd9a212fc339"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="67d6a9bffb59ad95"></a>
### LATCH: JOURNAL WRITE BUFFER

It is the time of waiting for the journal write buffer latch.

**PARAMETER**

<a id="8ed2bdc5e1927d6a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b71959e608f33e02"></a>
### LATCH: LOCK ITEM

It is the time of waiting for the lock item latch.

**PARAMETER**

<a id="a9baf29969fb851a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6ae047caa33e8f6e"></a>
### LATCH: RECORD HASH

It is the time of waiting for the record hash latch.

**PARAMETER**

<a id="669e881cdd7930fa"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="31d35aea61cdd561"></a>
### LATCH: DEADLOCK

It is the time of waiting for the deadlock latch.

**PARAMETER**

<a id="6fed2b8f95265159"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f40b887f9359fb29"></a>
### LATCH: SEQUENCE

It is the time of waiting for the sequence latch.

**PARAMETER**

<a id="a44d9ed5ba635c74"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="150e50b46c485362"></a>
### LATCH: LOG STREAM

It is the time of waiting for the log stream latch.

**PARAMETER**

<a id="b8fa2ed6be8836bd"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4e812a8fdfac2067"></a>
### LATCH: BUILD AGABLE SCN

It is the time of waiting for the build agable SCN latch.

**PARAMETER**

<a id="f0c7f2e1c08235d9"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5496b8e2c8e1f634"></a>
### LATCH: TRANSACTION TABLE

It is the time of waiting for the transaction table latch.

**PARAMETER**

<a id="674f48b3300a74c5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3103199f8751125c"></a>
### LATCH: SESSION LINK HASH

It is the time of waiting for the session link hash latch.

**PARAMETER**

<a id="1a7b18ce8b389b54"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="880fb7d0eaae6d58"></a>
### LATCH: ALLOC XA CONTEXT

It is the time of waiting for the allocate XA context latch.

**PARAMETER**

<a id="8fd2e94b9ff861f1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="638b2d84c2d09c84"></a>
### LATCH: SEQUENCE GLOBALX

It is the time of waiting for the sequence global latch X.

**PARAMETER**

<a id="d14fb626cf5e0400"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4a3135fdf8390a0a"></a>
### LATCH: SEQUENCE GLOBALY

It is the time of waiting for the sequence global latch Y.

**PARAMETER**

<a id="5b22d246ef9255e4"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e58ebf5d7d49ea25"></a>
### LATCH: TRANSACTION LOG FILE

It is the time of waiting for the transaction logfile latch.

**PARAMETER**

<a id="85378ec8d2f3a292"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
