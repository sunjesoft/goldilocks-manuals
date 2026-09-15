<a id="93c759381f4615e5"></a>

# Appendix B. Wait Event

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/93c759381f4615e5)  
> Tag: `21c.1_35_tag`

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<a id="5ba8457a6ae8d115"></a>
## Wait Event

Performance views which is related to the wait event is as follows.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#917f99ec3cf00787)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#26533c4fefcdfd22)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#8d8c0c579a9596a6)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#af4709c747da52b1)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#fb5b3a34243eee19)

<a id="7879c105dd82d240"></a>
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

<a id="db7bac8149456dea"></a>
## Item of Wait Event

<a id="a9b246d52f41c0dd"></a>
### ENQUEUE: GDISPATCHER REQUEST

It is the time of which GDISPATCHER enqueues a request in a shared mode.  
Parameter: None

<a id="5ea1f69c408fc0ca"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

It is the time of which a shared server enqueues a response in a shared mode.  
Parameter: None

<a id="5bbd87a6e5c9b2e6"></a>
### DEQUEUE: SHARED-SERVER REQUEST

It is the time of which a shared server dequeues a request in a shared mode.  
Parameter: None

<a id="acb2ffc8184ac66d"></a>
### DEQUEUE: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER dequeues a response in a shared mode.  
Parameter: None

<a id="11a57f6d729ac459"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

It is the time of which a dedicate server sends the spooled response to the client in a dedicate mode.

**PARAMETER**

<a id="39eef7b90a675eb9"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="d0e4d5664f400aca"></a>
### SEND: DEDICATE-SERVER RESPONSE

It is the time of which a dedicate server sends a response to the client in a dedicate mode.

**Parameter**

<a id="8be43bed8fa627e2"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="45835d5e334910ff"></a>
### RECV: DEDICATE-SERVER REQUEST

It is the time of which a dedicate server receives a request from the client in a dedicate mode.  
Parameter: None

<a id="8798e2c2449379e6"></a>
### SEND: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER sends a response to a client in a shared mode.

**Parameter**

<a id="d25942bce1e343ff"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="2c2b30ee37dedc38"></a>
### RECV: GDISPATCHER REQUEST

It is the time of which GDISPATCHER receives a request from a client in a shared mode.  
Parameter: None

<a id="26e3878f32a078a9"></a>
### ENQUEUE: CLUSTER REQUEST

It is the time of enqueuing a request of cluster.  
Parameter: None

<a id="9078a16f64c409b9"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

It is the time of enqueuing a broadcast request of cluster.  
Parameter: None

<a id="0d919acb4c0e3abb"></a>
### DEQUEUE: CLUSTER RESPONSE

It is the time of dequeuing a response of cluster.  
Parameter: None

<a id="faff96b501df71a3"></a>
### SEND: CDISPATCHER

It is the time of sending in cluster CDISPATCHER.  
Parameter: None

<a id="78573fa941bc06a5"></a>
### RECV: CDISPATCHER

It is the time of receiving in cluster CDISPATCHER.  
Parameter: None

<a id="373452080eef3e15"></a>
### GMASTER: ARCHIVE LOG

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="adad0c54d9cedac2"></a>
### GMASTER: CHECKPOINT

It is the time of processing checkpoints in gmaster.  
Parameter: None

<a id="86c02904203c9922"></a>
### GMASTER: IO SLAVE

It is the time of processing IO slave in gmaster.  
Parameter: None

<a id="5c355b97854b417f"></a>
### GMASTER: LOG FLUSH

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="84b653d44f638af1"></a>
### GMASTER: PAGE FLUSH

It is the time of processing page flush in gmaster.  
Parameter: None

<a id="fd1ccff90a5e6469"></a>
### WRITE: TRACE LOG

It is the time of writing trace logs.  
Parameter: None

<a id="094d4cbdc830c001"></a>
### WRITE: COPY ARCHIVING LOG

It is the time of copying archiving logs.  
Parameter: None

<a id="b9764fce3c4c220c"></a>
### WRITE: BACKUP CTRL FILE

It is the time of backing up control files.  
Parameter: None

<a id="658c588c21b33cbf"></a>
### WRITE: RESTORE CTRL FILE

It is the time of restoring the control file.  
Parameter: None

<a id="176b3acf0214b793"></a>
### READ: ARCHIVE LOG

It is the time of reading archive log files.  
Parameter: None

<a id="8c06e96f39cae13f"></a>
### READ: CTRL FILE

It is the time of reading the control file.  
Parameter: None

<a id="478c1a26725e15f5"></a>
### WRITE: LOG FILE

It is the time of writing log files.  
Parameter: None

<a id="d6403eefd510a05d"></a>
### WRITE: PAGE FILE

It is the time of writing page files.  
Parameter: None

<a id="aed8c7dc09a3e071"></a>
### WRITE: CTRL FILE

It is the time of writing the control file.  
Parameter: None

<a id="2a90f0e9135918d6"></a>
### WRITE: REMOVE DATA FILE

It is the time of removing the data file.  
Parameter: None

<a id="6bca3247c3c7f5d1"></a>
### WRITE: JOURNAL BUFFER

It is the time of writing journal buffers.  
Parameter: None

<a id="38a13392a87d4a2c"></a>
### READ: JOURNAL BUFFER

It is the time of reading journal buffers.  
Parameter: None

<a id="714f70c2cb54aec8"></a>
### WAIT TRANSACTION

It is the time of waiting for transactions.

**Parameter**

<a id="4c37d4e922e12135"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | Transaction id for which to wait |

<a id="c89ad680d7f52e9a"></a>
### WAIT OTHER TRANSACTION

It is the time of waiting for other transactions to be terminated.

**Parameter**

<a id="655eca067281cc31"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | ID of the waiting transaction |
| target transaction id | ID of the transaction to be terminated |

<a id="19b054807ca0ca85"></a>
### WAIT ENABLE LOGGING

It is the time of waiting until when the logging is available.  
Parameter: None

<a id="7591ba63da7cc82d"></a>
### WAIT LOG FLUSHER

It is the time of waiting for the log flusher.

**Parameter**

<a id="85bf7c6170575d3e"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="0959771fd819a088"></a>
### WAIT PAGE FLUSHER

It is the time of waiting for the page flusher.

**Parameter**

<a id="8b2017c6a54b2db7"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="7e1182aff252ab3e"></a>
### WAIT XA CONTEXT

It is the time of waiting for the XA context.  
Parameter: None

<a id="0843395a6826f901"></a>
### LATCH: LOG BUFFER

It is the time of waiting for the log buffer latch.

**Parameter**

<a id="ad34f48ec9ea0281"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f6d151ea838aac72"></a>
### LATCH: PROCESS MANAGER

It is the time of waiting for the process manager latch.

**Parameter**

<a id="676596c8b464f4ae"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a7a6473fd433b4c0"></a>
### LATCH: ENV MGR

It is the time of waiting for the env manager latch.

**Parameter**

<a id="a2dfc012fd255642"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="31379041532ffd99"></a>
### LATCH: SESSION ENV MGR

It is the time of waiting for the session env manager latch.

**Parameter**

<a id="eab9e7d353dc72a5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="063a400ea04a9e8d"></a>
### LATCH: PCH

It is the time of waiting for the Page Control Header (PCH) latch.

**Parameter**

<a id="07028a1e8c2cf9cd"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9969042a8f1067ce"></a>
### LATCH: PAGE

It is the time of waiting for the page latch.

**Parameter**

<a id="0edeb8dd436e1c41"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6712c732f4de9106"></a>
### LATCH: PENDING LOG

It is the time of waiting for the pending log latch.

**PARAMETER**

<a id="dff69b6d5970aed3"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ae0e25c83d5ad7cf"></a>
### LATCH: ALLOC TRANS

It is the time of waiting for the allocate transaction latch.

**PARAMETER**

<a id="32752252ebdce738"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b7eed7eed72a0a86"></a>
### LATCH: UNDO SEGMENT

It is the time of waiting for the undo segment latch.

**PARAMETER**

<a id="fde58033d4968e55"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="41339b4c4f8c7bb4"></a>
### LATCH: CLUSTER LOCATION

It is the time of waiting for the cluster location latch.

**PARAMETER**

<a id="9933307a2d4d252a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3902bc1e77ee5a64"></a>
### LATCH: DICT HASH ELEMENT AGING

It is the time of waiting for the dict hash element aging latch.

**PARAMETER**

<a id="8f6f1513971e4d62"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d965b7903afa9843"></a>
### LATCH: DICT HASH RELATED AGING

It is the time of waiting for the dict hash related aging latch.

**PARAMETER**

<a id="10da62ae18660ddf"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="86bf4ef9e7ba1215"></a>
### LATCH: FILE MANAGER

It is the time of waiting for the file manager latch.

**PARAMETER**

<a id="cf394f4c88906d2f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="347870f250891b95"></a>
### LATCH: TRACE LOG

It is the time of waiting for the trace log latch.

**PARAMETER**

<a id="890e166363761b27"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="25778f72fce92b0e"></a>
### LATCH: STATIC HASH

It is the time of waiting for the static hash latch.

**PARAMETER**

<a id="94734fd010bef1be"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f9d0acba9040a8a9"></a>
### LATCH: STATIC HASH BUCKET

It is the time of waiting for the static hash bucket latch.

**PARAMETER**

<a id="5bbe171c7dd6def6"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="520e3c6b9578f210"></a>
### LATCH: SQL HANDLE

It is the time of waiting for SQL handle latch.

**PARAMETER**

<a id="e228bc0175e2b465"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="088357fe5eada29d"></a>
### LATCH: XA CONTEXT HASH

It is the time of waiting for XA context hash latch.

**PARAMETER**

<a id="d56b7ecde8ab2dfa"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d26d97918e29ab07"></a>
### LATCH: PLAN CLOCK

It is the time of waiting for the plan clock latch.

**PARAMETER**

<a id="e832729089d276f5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="db802f973c86bab6"></a>
### LATCH: XA CONTEXT

It is the time of waiting for XA context latch.

**PARAMETER**

<a id="1e0f1e02069d57a8"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cbc242d4efea3f97"></a>
### LATCH: MEM CONTROLLER

It is the time of waiting for the memory controller latch.

**PARAMETER**

<a id="9c193aedb64ec0cf"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3d38f5064550d943"></a>
### LATCH: DYNAMIC MEM

It is the time of waiting for the dynamic memory latch.

**PARAMETER**

<a id="79868fc9a4a41211"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0a91c24c20273ecd"></a>
### LATCH: PROPERTY

It is the time of waiting for the property latch.

**PARAMETER**

<a id="edc3381ee37c7f1f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f9be02351a234bc6"></a>
### LATCH: ATTACH SHM

It is the time of waiting for the attack shared memory latch.

**PARAMETER**

<a id="d82350cf55517e57"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cc0bb0347fa62160"></a>
### LATCH: BACKUP TBS

It is the time of waiting for the backup tablespace latch.

**PARAMETER**

<a id="2b8a25dc972f3e93"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="22924cfcc07b222e"></a>
### LATCH: DATABASE COMPONENT

It is the time of waiting for the database component latch.

**PARAMETER**

<a id="9800b0c13abcf7e1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="497f4c517f2e9cfd"></a>
### LATCH: TABLESPACE

It is the time of waiting for the tablespace latch.

**PARAMETER**

<a id="56534b78b697f2d1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0478f7297366d9ec"></a>
### LATCH: BACKUP DATABASE

It is the time of waiting for the backup database latch.

**PARAMETER**

<a id="3b8883727c6c6d51"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4c28d4564dd5bad8"></a>
### LATCH: JOURNAL BUFFER

It is the time of waiting for the journal buffer latch.

**PARAMETER**

<a id="4dbdd0dece7e59ef"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="725e3fcf32b5d7ee"></a>
### LATCH: JOURNAL BUFFER ENTRY

It is the time of waiting for the journal buffer entry latch.

**PARAMETER**

<a id="c2b2528df1d46a79"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dd2b7ca1e3930891"></a>
### LATCH: JOURNAL WRITE BUFFER

It is the time of waiting for the journal write buffer latch.

**PARAMETER**

<a id="9ec5f7a97d440f36"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="def5960f25096352"></a>
### LATCH: LOCK ITEM

It is the time of waiting for the lock item latch.

**PARAMETER**

<a id="e0e1fa84eef5957b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5e3f5c2294a35042"></a>
### LATCH: RECORD HASH

It is the time of waiting for the record hash latch.

**PARAMETER**

<a id="d148db6ee301dd80"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b218a6cbd4bc1331"></a>
### LATCH: DEADLOCK

It is the time of waiting for the deadlock latch.

**PARAMETER**

<a id="5bb9c5a06bf2d4f0"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="626eba51f166a369"></a>
### LATCH: SEQUENCE

It is the time of waiting for the sequence latch.

**PARAMETER**

<a id="a57167a6fb8c4ed7"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="82fe513096a1e968"></a>
### LATCH: LOG STREAM

It is the time of waiting for the log stream latch.

**PARAMETER**

<a id="a4028381cb80e2ed"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b29bf9d4a13e857a"></a>
### LATCH: BUILD AGABLE SCN

It is the time of waiting for the build agable SCN latch.

**PARAMETER**

<a id="848db95731742d5f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="812dd61c054bacf3"></a>
### LATCH: TRANSACTION TABLE

It is the time of waiting for the transaction table latch.

**PARAMETER**

<a id="81286179a7b1131f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ff5d44dfb9234f80"></a>
### LATCH: SESSION LINK HASH

It is the time of waiting for the session link hash latch.

**PARAMETER**

<a id="77a5f01d411deaca"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="421a900c8b6dc493"></a>
### LATCH: ALLOC XA CONTEXT

It is the time of waiting for the allocate XA context latch.

**PARAMETER**

<a id="e1df03629b37fcf3"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c1b687d3e075ec06"></a>
### LATCH: SEQUENCE GLOBALX

It is the time of waiting for the sequence global latch X.

**PARAMETER**

<a id="146d36030cb6332e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3453287515f80795"></a>
### LATCH: SEQUENCE GLOBALY

It is the time of waiting for the sequence global latch Y.

**PARAMETER**

<a id="533409ce7329b896"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e2c171ed7b9f0ad1"></a>
### LATCH: TRANSACTION LOG FILE

It is the time of waiting for the transaction logfile latch.

**PARAMETER**

<a id="71f298c66fcbc8ad"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← Appendix A. Error Codes](appendix-01-appendix-a-error-codes.md) · [Table of contents](../README.md) · [Appendix C. Open Source License →](appendix-03-appendix-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
