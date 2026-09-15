<a id="89c56419728deb44"></a>

# Appendix C. Wait Event

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/89c56419728deb44)  
> Tag: `22c.1_10_tag`

[← Appendix B. Error Codes](appendix-02-appendix-b-error-codes.md) · [Table of contents](../README.md) · [Appendix D. Open Source License →](appendix-04-appendix-d-open-source-license.md)

<a id="63d77dfdc4eddbba"></a>
## Wait Event

Performance views which is related to the wait event is as follows.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#57748d05ef24dc11)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#bfe55baaa77a2489)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#61f255d78318f2f4)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#640642d06a164c65)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#3f208b85eb34bb5e)

<a id="84ea4b630f5de4a7"></a>
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

<a id="fad38e5b7cb84bcd"></a>
## Item of Wait Event

<a id="7df85d44e45990ec"></a>
### ENQUEUE: GDISPATCHER REQUEST

It is the time of which GDISPATCHER enqueues a request in a shared mode.  
Parameter: None

<a id="a6a901670057fb5b"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

It is the time of which a shared server enqueues a response in a shared mode.  
Parameter: None

<a id="022e4e01a9057d6c"></a>
### DEQUEUE: SHARED-SERVER REQUEST

It is the time of which a shared server dequeues a request in a shared mode.  
Parameter: None

<a id="e1281a115916024d"></a>
### DEQUEUE: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER dequeues a response in a shared mode.  
Parameter: None

<a id="49ab4e535b0a373c"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

It is the time of which a dedicate server sends the spooled response to the client in a dedicate mode.

**PARAMETER**

<a id="51f4595b97203ea3"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="6a906869cb639786"></a>
### SEND: DEDICATE-SERVER RESPONSE

It is the time of which a dedicate server sends a response to the client in a dedicate mode.

**Parameter**

<a id="d4799796a19c3832"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="febbdf86c14e2453"></a>
### RECV: DEDICATE-SERVER REQUEST

It is the time of which a dedicate server receives a request from the client in a dedicate mode.  
Parameter: None

<a id="b39e919e4bf99926"></a>
### SEND: GDISPATCHER RESPONSE

It is the time of which GDISPATCHER sends a response to a client in a shared mode.

**Parameter**

<a id="5492e5ac5f0d25a8"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="fc3cef0a9590d010"></a>
### RECV: GDISPATCHER REQUEST

It is the time of which GDISPATCHER receives a request from a client in a shared mode.  
Parameter: None

<a id="749fa4a334a85a59"></a>
### ENQUEUE: CLUSTER REQUEST

It is the time of enqueuing a request of cluster.  
Parameter: None

<a id="26db3b790a8cc7cf"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

It is the time of enqueuing a broadcast request of cluster.  
Parameter: None

<a id="b09eaa7a2f6b2f6f"></a>
### DEQUEUE: CLUSTER RESPONSE

It is the time of dequeuing a response of cluster.  
Parameter: None

<a id="10b5ef7249c70a2b"></a>
### SEND: CDISPATCHER

It is the time of sending in cluster CDISPATCHER.  
Parameter: None

<a id="28a90c26ef2b86c0"></a>
### RECV: CDISPATCHER

It is the time of receiving in cluster CDISPATCHER.  
Parameter: None

<a id="f5b53bb0ccadc6a5"></a>
### GMASTER: ARCHIVE LOG

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="2835b6bf82eba05b"></a>
### GMASTER: CHECKPOINT

It is the time of processing checkpoints in gmaster.  
Parameter: None

<a id="ebfee14198d9a588"></a>
### GMASTER: IO SLAVE

It is the time of processing IO slave in gmaster.  
Parameter: None

<a id="1bccab8d1cf23a6d"></a>
### GMASTER: LOG FLUSH

It is the time of processing archive logs in gmaster.  
Parameter: None

<a id="2d95a08665b21355"></a>
### GMASTER: PAGE FLUSH

It is the time of processing page flush in gmaster.  
Parameter: None

<a id="091b8dacf3ed20fe"></a>
### WRITE: TRACE LOG

It is the time of writing trace logs.  
Parameter: None

<a id="d8c70c47eb15bc2b"></a>
### WRITE: COPY ARCHIVING LOG

It is the time of copying archiving logs.  
Parameter: None

<a id="2bfc44573400b66a"></a>
### WRITE: BACKUP CTRL FILE

It is the time of backing up control files.  
Parameter: None

<a id="13d2ee1f3eaefec5"></a>
### WRITE: RESTORE CTRL FILE

It is the time of restoring the control file.  
Parameter: None

<a id="967316578cc16ab1"></a>
### READ: ARCHIVE LOG

It is the time of reading archive log files.  
Parameter: None

<a id="dd2362437935ac02"></a>
### READ: CTRL FILE

It is the time of reading the control file.  
Parameter: None

<a id="8ab5a787ea641fe0"></a>
### WRITE: LOG FILE

It is the time of writing log files.  
Parameter: None

<a id="2ba24a690d7b38a2"></a>
### WRITE: PAGE FILE

It is the time of writing page files.  
Parameter: None

<a id="690f87f858230392"></a>
### WRITE: CTRL FILE

It is the time of writing the control file.  
Parameter: None

<a id="7852471a2cabd0c2"></a>
### WRITE: REMOVE DATA FILE

It is the time of removing the data file.  
Parameter: None

<a id="306cdbaafc3a878f"></a>
### WRITE: JOURNAL BUFFER

It is the time of writing journal buffers.  
Parameter: None

<a id="f39f12bc96347c02"></a>
### READ: JOURNAL BUFFER

It is the time of reading journal buffers.  
Parameter: None

<a id="11d7fe9ca8829a45"></a>
### WAIT TRANSACTION

It is the time of waiting for transactions.

**Parameter**

<a id="97d7ffef22eec365"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | Transaction id for which to wait |

<a id="8d36b606cf43f84a"></a>
### WAIT OTHER TRANSACTION

It is the time of waiting for other transactions to be terminated.

**Parameter**

<a id="5a957925000cacd1"></a>
| Parameter | Description |
| --- | --- |
| wait transaction id | ID of the waiting transaction |
| target transaction id | ID of the transaction to be terminated |

<a id="7a5cbccfe45c4fd9"></a>
### WAIT ENABLE LOGGING

It is the time of waiting until when the logging is available.  
Parameter: None

<a id="7b2264731db6995b"></a>
### WAIT LOG FLUSHER

It is the time of waiting for the log flusher.

**Parameter**

<a id="0dce5af22fa286b3"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="579235af33be07c7"></a>
### WAIT PAGE FLUSHER

It is the time of waiting for the page flusher.

**Parameter**

<a id="4e41a5e1a0f632d0"></a>
| Parameter | Description |
| --- | --- |
| send data size | Bytes of the data to be sent |

<a id="2bbbaf2842a7c531"></a>
### WAIT XA CONTEXT

It is the time of waiting for the XA context.  
Parameter: None

<a id="ba5f9594c4970bcc"></a>
### LATCH: LOG BUFFER

It is the time of waiting for the log buffer latch.

**Parameter**

<a id="3c948eb214bae0fa"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3ef44ea6383e1cf6"></a>
### LATCH: PROCESS MANAGER

It is the time of waiting for the process manager latch.

**Parameter**

<a id="235ac0758679f61f"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a02b2e8571319d3a"></a>
### LATCH: ENV MGR

It is the time of waiting for the env manager latch.

**Parameter**

<a id="45bac173d1f76e17"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7db00ac73ddfa81e"></a>
### LATCH: SESSION ENV MGR

It is the time of waiting for the session env manager latch.

**Parameter**

<a id="dd3203cab4fd2f3b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6e97ac3178c05bad"></a>
### LATCH: PCH

It is the time of waiting for the Page Control Header (PCH) latch.

**Parameter**

<a id="9ca923ea625e68a7"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2397d4f7c0db7141"></a>
### LATCH: PAGE

It is the time of waiting for the page latch.

**Parameter**

<a id="c93b93227679eae5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="44ac873062290a94"></a>
### LATCH: PENDING LOG

It is the time of waiting for the pending log latch.

**PARAMETER**

<a id="26d897d65bb6353a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f8846287b2d2ff7a"></a>
### LATCH: ALLOC TRANS

It is the time of waiting for the allocate transaction latch.

**PARAMETER**

<a id="fb8b95ff0cfa1cf0"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c9f7fcaa1137618d"></a>
### LATCH: UNDO SEGMENT

It is the time of waiting for the undo segment latch.

**PARAMETER**

<a id="e0413dbe73edfcb4"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8620e58080eeb832"></a>
### LATCH: CLUSTER LOCATION

It is the time of waiting for the cluster location latch.

**PARAMETER**

<a id="9348188271b07f11"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a70afb1f5604ea0d"></a>
### LATCH: DICT HASH ELEMENT AGING

It is the time of waiting for the dict hash element aging latch.

**PARAMETER**

<a id="ac96738c9cddadc6"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f55ae5a1ef3ed16b"></a>
### LATCH: DICT HASH RELATED AGING

It is the time of waiting for the dict hash related aging latch.

**PARAMETER**

<a id="0fba3462422cd2e7"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d22ab5fcea662ebd"></a>
### LATCH: FILE MANAGER

It is the time of waiting for the file manager latch.

**PARAMETER**

<a id="2357f35c2cb693f4"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b4df39c331118154"></a>
### LATCH: TRACE LOG

It is the time of waiting for the trace log latch.

**PARAMETER**

<a id="8269d4d1710fcf96"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b85f9dfcd589957f"></a>
### LATCH: STATIC HASH

It is the time of waiting for the static hash latch.

**PARAMETER**

<a id="29a8a6a3e91b2727"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1cfa2a0b991bd4bf"></a>
### LATCH: STATIC HASH BUCKET

It is the time of waiting for the static hash bucket latch.

**PARAMETER**

<a id="de4e70b271e07dca"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="06644992949ca706"></a>
### LATCH: SQL HANDLE

It is the time of waiting for SQL handle latch.

**PARAMETER**

<a id="ef11061cfc3cb676"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="257700da02d69021"></a>
### LATCH: XA CONTEXT HASH

It is the time of waiting for XA context hash latch.

**PARAMETER**

<a id="38a53d323f934a58"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e015da70d51a3d90"></a>
### LATCH: PLAN CLOCK

It is the time of waiting for the plan clock latch.

**PARAMETER**

<a id="9d63039f1b54565e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dec1b10cc3aa23ee"></a>
### LATCH: XA CONTEXT

It is the time of waiting for XA context latch.

**PARAMETER**

<a id="353e443e34bb193b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5d80f9ed9ec4d384"></a>
### LATCH: MEM CONTROLLER

It is the time of waiting for the memory controller latch.

**PARAMETER**

<a id="3e8156e41e29cad5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="08eaff5e5b6070b5"></a>
### LATCH: DYNAMIC MEM

It is the time of waiting for the dynamic memory latch.

**PARAMETER**

<a id="8ecf082755959e42"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="13954c0f5443a099"></a>
### LATCH: PROPERTY

It is the time of waiting for the property latch.

**PARAMETER**

<a id="4aaba70fe66fff16"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="68807df3761c16ac"></a>
### LATCH: ATTACH SHM

It is the time of waiting for the attack shared memory latch.

**PARAMETER**

<a id="216f2b706c479041"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d12f8cb03753cf19"></a>
### LATCH: BACKUP TBS

It is the time of waiting for the backup tablespace latch.

**PARAMETER**

<a id="6b7c70841d2b3ac8"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="24216fdbd8817118"></a>
### LATCH: DATABASE COMPONENT

It is the time of waiting for the database component latch.

**PARAMETER**

<a id="7bb305f1bf9753b4"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="000b39c4c32c87b7"></a>
### LATCH: TABLESPACE

It is the time of waiting for the tablespace latch.

**PARAMETER**

<a id="865d5065219e318d"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8b2e18ad676c2a49"></a>
### LATCH: BACKUP DATABASE

It is the time of waiting for the backup database latch.

**PARAMETER**

<a id="6ca41de31ab12e5a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="df8231f05387afe6"></a>
### LATCH: JOURNAL BUFFER

It is the time of waiting for the journal buffer latch.

**PARAMETER**

<a id="4ef62a0f6ab73ee2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4b1360525c4f8feb"></a>
### LATCH: JOURNAL BUFFER ENTRY

It is the time of waiting for the journal buffer entry latch.

**PARAMETER**

<a id="1a331603d41d70b2"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2de1ab103a516801"></a>
### LATCH: JOURNAL WRITE BUFFER

It is the time of waiting for the journal write buffer latch.

**PARAMETER**

<a id="9eb43afc7179cd5b"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="52fa74a34d3bca96"></a>
### LATCH: LOCK ITEM

It is the time of waiting for the lock item latch.

**PARAMETER**

<a id="c526ebd2cfbf7e11"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="12c1fd3ec56b0f3f"></a>
### LATCH: RECORD HASH

It is the time of waiting for the record hash latch.

**PARAMETER**

<a id="c4d084535a831756"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f2bd0d390228cc8b"></a>
### LATCH: DEADLOCK

It is the time of waiting for the deadlock latch.

**PARAMETER**

<a id="621a79441c2903ac"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="959fa78fd9e52877"></a>
### LATCH: SEQUENCE

It is the time of waiting for the sequence latch.

**PARAMETER**

<a id="36e7896ee4aea3ea"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c16cbaa2435529a9"></a>
### LATCH: LOG STREAM

It is the time of waiting for the log stream latch.

**PARAMETER**

<a id="5d892f6f71db505c"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cbc951c5b9a12337"></a>
### LATCH: BUILD AGABLE SCN

It is the time of waiting for the build agable SCN latch.

**PARAMETER**

<a id="bc547fef9bcb7cf0"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="94fbd1d3a4a6c8c1"></a>
### LATCH: TRANSACTION TABLE

It is the time of waiting for the transaction table latch.

**PARAMETER**

<a id="f70c015e5d3c00a5"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e6def6d0178fd2e8"></a>
### LATCH: SESSION LINK HASH

It is the time of waiting for the session link hash latch.

**PARAMETER**

<a id="9f46fce8936d4146"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="49e79317fbdc4d44"></a>
### LATCH: ALLOC XA CONTEXT

It is the time of waiting for the allocate XA context latch.

**PARAMETER**

<a id="c2ee90f6920f3f25"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dd8a7592db2d25fa"></a>
### LATCH: SEQUENCE GLOBALX

It is the time of waiting for the sequence global latch X.

**PARAMETER**

<a id="e40d0736dacce76a"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a67f8b6406649b11"></a>
### LATCH: SEQUENCE GLOBALY

It is the time of waiting for the sequence global latch Y.

**PARAMETER**

<a id="f3086ec394368fca"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="31f55353fead7044"></a>
### LATCH: TRANSACTION LOG FILE

It is the time of waiting for the transaction logfile latch.

**PARAMETER**

<a id="46a8c7542ba04056"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f986b87ff85cd6f1"></a>
### ASYNC RESPONSE

It is the time of waiting for the response from the remote node in the cluster environment.  
Parameter: None

<a id="4baaa25b1527ad00"></a>
### ASYNC TRANSACTION

It is the time of waiting for the response for the ASYNC TRANSACTION's COMMIT from the remote node in the cluster environment.  
Parameter: None

<a id="b191e33466a91705"></a>
### ASYNC COMMIT

N/A

<a id="2a742c20f99272c4"></a>
### GMASTER: BUFFER FLUSH

It is the time of executing the buffer flush by the io slave of gmaster.  
Parameter: None

<a id="0cbfa7cffb3f4bc1"></a>
### LATCH: BUFFER HASH BUCKET

It is the time of waiting for the buffer hash bucket's latch.

**PARAMETER**

<a id="60d62991ab49230e"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="33215d9f3d714811"></a>
### READ: PAGE FILE

It is the time of reading pages from the disk to read the disk tablespace's pages.  
Parameter: None

<a id="38b8fce01eb6e2d7"></a>
### LATCH: BUFFER CHECKPOINT LIST

N/A

<a id="3de68529111480c2"></a>
### WRITE: CHANGE TRACKING FILE

It is the time of writing the disk tablespace's change tracking file.  
Parameter: None

<a id="ed71caafd229e24b"></a>
### WAIT FREE BUFFER

It is the time of waiting for the free buffer, to read the pages in the disk tablespace.  
Parameter: None

<a id="34b5122aeec13cd3"></a>
### GLOBAL SEQUENCE: LOCK AND QUERY

It is the time of waiting for the global latch by all members to synchronize the global sequence in cluster, and the time of waiting to get the latest information of the global sequence.  
Parameter: None

<a id="a0a809771f8976a2"></a>
### GLOBAL SEQUENCE: SYNC

It is the time of synchronizing the global sequence in cluster.  
Parameter: None

<a id="01b44d47d897ff81"></a>
### LATCH: SEQUENCE GLOBAL NEXT

It is the time of waiting for the sequence global next latch in cluster.

**PARAMETER**

<a id="8498bee43ad8c399"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1c784d12064b9e79"></a>
### LATCH: BUFFER LRU LIST

It is the time of waiting for the buffer lru list latch.

**PARAMETER**

<a id="37e29b87b7896ad1"></a>
| Parameter | Description |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2adfba0d706dfa19"></a>
### WAIT DIRTY PAGE LIMIT

It is the time of waiting until the number of dirty pages in the system becomes smaller than [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#9a788e0a29630941) to access the pages cached in the buffer.   
Parameter: None

<a id="3e8760983fb49502"></a>
### WAIT BUFFER READ COMPLETE

It is the time of waiting for the disk read to be completed to access the page of the disk tablespace.  
Parameter: None

---

[← Appendix B. Error Codes](appendix-02-appendix-b-error-codes.md) · [Table of contents](../README.md) · [Appendix D. Open Source License →](appendix-04-appendix-d-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
