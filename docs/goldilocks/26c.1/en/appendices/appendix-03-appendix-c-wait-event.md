<a id="990e0f08bfb12bf2"></a>

# Appendix C. Wait Event

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/990e0f08bfb12bf2)  
> Tag: `26c.1_0_tag`

[← Appendix B. Error Codes](appendix-02-appendix-b-error-codes.md) · [Table of contents](../README.md) · [Appendix D. Open Source License →](appendix-04-appendix-d-open-source-license.md)

<a id="19dcae941f402b00"></a>
## Wait Event

Performance views which is related to the wait event is as follows.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#4b12716a3b7eaf0b)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#8d5901ed500e22a4)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#0e5f0162635a2444)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#f19aa56bac54d208)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#2983344226a78f2f)

<a id="c04cc67fc6f18b30"></a>
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

<a id="d25354dda3d29241"></a>
## Item of Wait Event

<a id="a35de2f2aa88eab5"></a>
### ENQUEUE: GDISPATCHER REQUEST

It is the time a request waits in the queue when GDISPATCHER sends it to the shared server.  
Parameter: None

<a id="126b594cae752ce3"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

It is the time a response waits in the queue when the shared server sends it to GDISPATCHER.  
Parameter: None

<a id="6f6763baa1c0d3f0"></a>
### DEQUEUE: SHARED-SERVER REQUEST

It is the time a request waits in the queue when the shared server receives it from GDISPATCHER.  
Parameter: None

<a id="6ab702a7c4851e8f"></a>
### DEQUEUE: GDISPATCHER RESPONSE

It is the time a response waits in the queue when GDISPATCHER receives it from the shared server.  
Parameter: None

<a id="aa47566cbb5a6906"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

It is the time a dedicated server waits in the socket or IPC when sending a spooled response to the client.

**PARAMETER**

<a id="2a3a103ec5610ee7"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="63e3dbb8fdd3205d"></a>
### SEND: DEDICATE-SERVER RESPONSE

It is the time a dedicated server waits in the socket or IPC when sending a response to the client.

**Parameter**

<a id="377b9ca74c436631"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="a33563dc5d2242ff"></a>
### RECV: DEDICATE-SERVER REQUEST

It is the time a dedicated server waits in the socket or IPC when receiving a request from the client.  
Parameter: None

<a id="95d0aeb9c70e5377"></a>
### SEND: GDISPATCHER RESPONSE

It is the time GDISPATCHER waits in the socket when sending a response to the client.

**Parameter**

<a id="e966f4896cebc8dd"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="47c8f5899afae25e"></a>
### RECV: GDISPATCHER REQUEST

It is the time GDISPATCHER waits in the socket when receiving a request from the client.  
Parameter: None

<a id="5bc01606c3dea75c"></a>
### ENQUEUE: CLUSTER REQUEST

It is the time a request waits in the queue when sent remotely in a cluster.  
Parameter: None

<a id="2dae6f2f1f3ac61a"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

It is the time a broadcast request waits in the queue when sent remotely in a cluster.  
Parameter: None

<a id="0ab6b22b0eede846"></a>
### DEQUEUE: CLUSTER RESPONSE

It is the time a response waits in the queue when received remotely in a cluster.  
Parameter: None

<a id="08623f4617f639a7"></a>
### SEND: CDISPATCHER

It is the time CDISPATCHER waits in the socket when sending a message remotely.  
Parameter: None

<a id="a08d6ec9abae4663"></a>
### RECV: CDISPATCHER

It is the time CDISPATCHER waits in the socket when receiving a message remotely.  
Parameter: None

<a id="d00bbd2462b856f4"></a>
### WAIT TRANSACTION

It is the time spent waiting for a specific transaction to complete.

**Parameter**

<a id="f97882c377651cf2"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | Transaction id for which to wait |

<a id="330c1a83ec602f44"></a>
### WAIT OTHER TRANSACTION

It is the time spent waiting while another transaction holds a lock.   
For example, if transaction A is waiting for the completion of transaction B, it refers to the waiting time of A.

**Parameter**

<a id="63637d62c09bc019"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | ID of the waiting transaction |
| target transaction id | ID of the transaction to be terminated |

<a id="ca9e2ba827716d87"></a>
### WAIT ENABLE LOGGING

It is the time spent waiting until logging is allowed.  
Parameter: None

<a id="20cf58722d431c03"></a>
### WAIT LOG FLUSHER

It is the time the session waits until the log flusher writes the log to the disk.

**Parameter**

<a id="56c5f9a349a633fc"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="a4e304fd08c1e596"></a>
### WAIT XA CONTEXT

It is the time the session waits when the XA context is being used by another session.  
Parameter: None

<a id="04fc7ad9005faecd"></a>
### LATCH: LOG BUFFER

It is the time spent waiting to acquire the latch for the log buffer.

**Parameter**

<a id="40ab624b27d1f423"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9515d4ce7312ef82"></a>
### LATCH: PROCESS MANAGER

It is the time spent waiting to acquire the latch for the process manager.

**Parameter**

<a id="227eef0c71354726"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="31407a87fac7435b"></a>
### LATCH: ENV MGR

It is the time spent waiting to acquire the latch for the env manager.

**Parameter**

<a id="d03bd94400b5ca17"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7b1136b80138d603"></a>
### LATCH: SESSION ENV MGR

It is the time spent waiting to acquire the latch for the session env manager.

**Parameter**

<a id="94f9b12a1831270d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="361e9775b48d30ce"></a>
### LATCH: PCH

It is the time spent waiting to acquire the latch for the Page Control Header (PCH).

**Parameter**

<a id="9870b02d67448b18"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d15a44ca264bfe3f"></a>
### LATCH: PAGE

It is the time spent waiting to acquire the latch for the page layer.

**Parameter**

<a id="665c2e60be79af00"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a42c207c202d1ff0"></a>
### LATCH: PENDING LOG

It is the time spent waiting to write a log to the pending log buffer.

**PARAMETER**

<a id="9c40d02ca2cd7712"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bca179c8a155c965"></a>
### LATCH: ALLOC TRANS

It is the time spent waiting to allocate a transaction slot.

**PARAMETER**

<a id="d6592b88ccbc9ba3"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4c80b8b953690cf6"></a>
### LATCH: UNDO SEGMENT

It is the time spent waiting to acquire the latch for the undo segment.

**PARAMETER**

<a id="15ece0f9fe44839d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3b9750db4e039781"></a>
### LATCH: CLUSTER LOCATION

It is the time spent waiting to acquire the latch for the cluster location.

**PARAMETER**

<a id="187fdd7ba5957f05"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9f7a65db3e028004"></a>
### LATCH: DICT HASH ELEMENT AGING

It is the time spent waiting in the latch while aging a deleted dictionary cache.

**PARAMETER**

<a id="148fd8f966b3117e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b8689ab9dde7fea5"></a>
### LATCH: DICT HASH RELATED AGING

It is the time spent waiting in the latch while aging a deleted related dictionary cache.

**PARAMETER**

<a id="7c5f0edea26d86db"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="155a2b97a0ef9db8"></a>
### LATCH: FILE MANAGER

It is the time spent waiting to acquire the latch for the file manager.

**PARAMETER**

<a id="3a43197c02290199"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7b031baca88769f8"></a>
### LATCH: TRACE LOG

It is the time spent waiting to acquire the latch for the trace log.

**PARAMETER**

<a id="7647409ea82adcd2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a76bf12d55570baa"></a>
### LATCH: STATIC HASH

It is the time spent waiting to acquire the latch for the static hash.

**PARAMETER**

<a id="cdc9d5a0c49fd524"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ec557ae75d56e449"></a>
### LATCH: STATIC HASH BUCKET

It is the time spent waiting to acquire the bucket latch for the static hash.

**PARAMETER**

<a id="1c37244319e320f2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="23bbd6c9a32271fb"></a>
### LATCH: SQL HANDLE

It is the time spent waiting to acquire the latch for the SQL cache manager.

**PARAMETER**

<a id="ea0432d0704ef8ab"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f3edc23f58eac983"></a>
### LATCH: XA CONTEXT HASH

It is the time spent waiting to acquire the latch for the XA context hash.

**PARAMETER**

<a id="3673b92c393569e8"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6bb10765f9fe21d6"></a>
### LATCH: PLAN CLOCK

It is the time spent waiting to acquire the clock latch for the SQL plan.

**PARAMETER**

<a id="a2332e6212797f8e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9fb34a890b4b97d5"></a>
### LATCH: XA CONTEXT

It is the time spent waiting to acquire the latch for the XA context.

**PARAMETER**

<a id="cdcd113eee9fea60"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a4fea44f727e60d7"></a>
### LATCH: MEM CONTROLLER

It is the time spent waiting to acquire the latch for the memory controller.

**PARAMETER**

<a id="cdbcb447572db9eb"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="68daca121060836a"></a>
### LATCH: DYNAMIC MEM

It is the time spent waiting to acquire the latch for dynamic memory.

**PARAMETER**

<a id="990f044885bdc01f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b1c4d2c38bc3d4ab"></a>
### LATCH: PROPERTY

It is the time spent waiting to acquire the latch for the property manager.

**PARAMETER**

<a id="6e1a06dcd96dbe32"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5636c6820d52c8ab"></a>
### LATCH: ATTACH SHM

It is the time spent waiting to acquire the latch for the shared memory segment.

**PARAMETER**

<a id="49f38871dc0f01ec"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8d279f3c1e555402"></a>
### LATCH: BACKUP TBS

It is the time spent waiting to acquire the latch for the tablespace backup manager.

**PARAMETER**

<a id="cce67c31b74b8141"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b84bd8f9ecc19817"></a>
### LATCH: DATABASE COMPONENT

It is the time spent waiting to acquire the latch for the datafile manager.

**PARAMETER**

<a id="005e844c6abb457d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ea8ec1ff032d7c36"></a>
### LATCH: TABLESPACE

It is the time spent waiting to acquire the latch for the tablespace.

**PARAMETER**

<a id="4d1d7799487a34e3"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2a2a4f16d0729c3a"></a>
### LATCH: BACKUP DATABASE

It is the time spent waiting to acquire the latch for the database backup manager.

**PARAMETER**

<a id="3bedd61e5f801677"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f90f4c0a9ed38133"></a>
### LATCH: JOURNAL BUFFER

It is the time spent waiting to acquire the latch for the journal buffer manager.

**PARAMETER**

<a id="cf455f0b0f03892b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6ad181e03e8f4c15"></a>
### LATCH: JOURNAL BUFFER ENTRY

It is the time spent waiting to acquire the latch for the journal buffer entry.

**PARAMETER**

<a id="92403a3f9e7e637e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="187cb2518f756228"></a>
### LATCH: JOURNAL WRITE BUFFER

It is the time spent waiting to acquire the latch for the journal write buffer.

**PARAMETER**

<a id="ea8a561cc0fe4c21"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="36647bbe9ebd1852"></a>
### LATCH: LOCK ITEM

It is the time spent waiting to acquire the latch for the lock item.

**PARAMETER**

<a id="f05b99f3fd4b5031"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="083d16c577441387"></a>
### LATCH: RECORD HASH

It is the time spent waiting to acquire the bucket latch for the lock record hash.

**PARAMETER**

<a id="8b80a05ebc6e56a8"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a79e336daf392ef1"></a>
### LATCH: SEQUENCE

It is the time spent waiting to acquire the latch for the sequence object.

**PARAMETER**

<a id="cbeeb2e486301c67"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a055721392e08a31"></a>
### LATCH: LOG FILE

It is the time spent waiting to acquire the latch for the redo logfile.

**PARAMETER**

<a id="f99449ee5a1152b9"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="21da113d09658814"></a>
### LATCH: BUILD AGABLE SCN

It is the time spent waiting for the latch to construct the agable SCN.

**PARAMETER**

<a id="12cbd739b4f7f807"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8253a04778a1423a"></a>
### LATCH: TRANSACTION TABLE

It is the time spent waiting to acquire the latch for the transaction table.

**PARAMETER**

<a id="eb14c2735defba93"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9f13ccfa172725ee"></a>
### LATCH: SESSION LINK HASH

It is the time spent waiting to acquire the bucket latch for the session link hash.

**PARAMETER**

<a id="8973a7ac5bf83f8f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2450f8ff85a31012"></a>
### LATCH: ALLOC XA CONTEXT

It is the time spent waiting in the latch to allocate the XA context.

**PARAMETER**

<a id="379401ba0542d20f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="80deabcbe3ee0d92"></a>
### LATCH: SEQUENCE GLOBAL_X

It is the time spent waiting to acquire the X latch for the global sequence.

**PARAMETER**

<a id="7607c24891f49032"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c45baf00c9b9c979"></a>
### LATCH: SEQUENCE GLOBAL_Y

It is the time spent waiting to acquire the Y latch for the global sequence.

**PARAMETER**

<a id="8bff1eede2ce1585"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ae53cfd39559d96d"></a>
### LATCH: TRANSACTION LOG FILE

It is the time spent waiting to acquire the latch for the transaction logfile.

**PARAMETER**

<a id="c902e7c22fb673c2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ddc67648aa24e0e2"></a>
### ASYNC RESPONSE

It is the time spent waiting for a response to an asynchronous command from a remote node.  
Parameter: None

<a id="5fe8c93e76679cb9"></a>
### ASYNC TRANSACTION

It is the time spent waiting for a response to an asynchronous COMMIT command from a remote node.  
Parameter: None

<a id="1aa74a30a005db90"></a>
### LATCH: DISK BUFFER HASH BUCKET

It is the time spent waiting for the bucket latch for the hash of the disk buffer cache.

**PARAMETER**

<a id="4fad31b9a0f9302a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="47d747956afbd183"></a>
### WRITE: CHANGE TRACKING FILE

It is the time spent waiting to acquire the latch for the change tracking file.  
Parameter: None

<a id="1cad959942fcfa03"></a>
### WAIT FREE BUFFER

It is the time spent waiting to find a clean disk buffer.  
Parameter: None

<a id="64199fbbd9045f21"></a>
### GLOBAL SEQUENCE: LOCK AND QUERY

It is the time spent waiting for the latch for global sequence synchronization.  
Parameter: None

<a id="c7e7ed891b80713a"></a>
### GLOBAL SEQUENCE: SYNC

It is the time spent waiting for the completion of global sequence synchronization.  
Parameter: None

<a id="e08048544eb9013a"></a>
### LATCH: SEQUENCE GLOBAL NEXT

It is the time spent waiting for the latch for sequence nextval.

**PARAMETER**

<a id="c643e5bf6868250c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="27d8684a8a77a676"></a>
### LATCH: BUFFER LRU LIST

It is the time spent waiting for the latch for the LRU list of the disk buffer.

**PARAMETER**

<a id="9735ed407c82e6dd"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="10c25ad4dcdb2622"></a>
### WAIT DIRTY PAGE LIMIT

It is the time spent waiting until the number of dirty pages in the disk buffer is reduced below the  [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#5c88ba27554a8c6b) property.   
Parameter: None

<a id="970c191396a9fb1c"></a>
### WAIT BUFFER READ COMPLETE

It is the time spent waiting for the read to complete when accessing a disk buffer page that is currently being read.  
Parameter: None

<a id="27263c1cb8b6b5cb"></a>
### WAIT ENV EVENT

It is the time spent waiting for the completion of the env event.

**PARAMETER**

<a id="932ff3d68b51dccf"></a>
| Parameter | Description |
| --- | --- |
| event id | Event ID |

<a id="105da9c174c4511d"></a>
### WAIT FREE APPEND EXTENT

It is the time spent waiting for the extent allocated for append insert to be freed in the buffer.  
Parameter: None

---

[← Appendix B. Error Codes](appendix-02-appendix-b-error-codes.md) · [Table of contents](../README.md) · [Appendix D. Open Source License →](appendix-04-appendix-d-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
