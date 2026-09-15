<a id="7e86445b896a561b"></a>

# 부록 B. Wait Event

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/7e86445b896a561b)  
> 태그: `21c.1_35_tag`

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<a id="0d54ba08239ac4a0"></a>
## Wait Event

Wait event와 관련된 performance view는 다음과 같다.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#94f9fe99e51cccfa)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#472514fc36931edc)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#d0d920c89aa52774)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#334acf3538552838)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#8ddf576a3b638b92)

<a id="46ceb705704861ee"></a>
## Wait Event의 Class

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

<a id="b074c7addbcda021"></a>
## Wait Event 항목

<a id="dbbd01b9430beb00"></a>
### ENQUEUE: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 request를 enqueue하는 시간이다.   
Parameter: None

<a id="fd37f5cefa4050d8"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="63a39219bfd7d6fc"></a>
### DEQUEUE: SHARED-SERVER REQUEST

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="fcc7e318eb42180b"></a>
### DEQUEUE: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 dequeue하는 시간이다.   
Parameter: None

<a id="5d77f559f1a6c38e"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

Dedicate mode에서 dedicate server가 spool 된 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="7a937c7dac6a1753"></a>
| Parameter | Description |
| --- | --- |
| send data size | Send 할 data byte |

<a id="cdadd0cd9e04159f"></a>
### SEND: DEDICATE-SERVER RESPONSE

Dedicate mode에서 dedicate server가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="f665d0fe1bf4ce0c"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="f603272d5aee93ee"></a>
### RECV: DEDICATE-SERVER REQUEST

Dedicate mode에서 dedicate server가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="0256a9f5c78ea6b7"></a>
### SEND: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="48383c1fcaf83147"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="7217a6c445380cfc"></a>
### RECV: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="27ce8d5a8f4dd921"></a>
### ENQUEUE: CLUSTER REQUEST

Cluster의 request를 enqueue하는 시간이다.  
Parameter: None

<a id="0e96fba7545ab381"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

Cluster의 broadcast request를 enqueue하는 시간이다.   
Parameter: None

<a id="9e0930084e3642d1"></a>
### DEQUEUE: CLUSTER RESPONSE

Cluster의 response를 dequeue하는 시간이다.   
Parameter: None

<a id="e2b229a25f26ebc1"></a>
### SEND: CDISPATCHER

Cluster CDISPATCHER에서 send하는 시간이다.   
Parameter: None

<a id="96b78093d9e46c4b"></a>
### RECV: CDISPATCHER

Cluster CDISPATCHER에서 receive 하는 시간이다.   
Parameter: None

<a id="054e0a1d812c94de"></a>
### GMASTER: ARCHIVE LOG

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="0e4ca427cf84442e"></a>
### GMASTER: CHECKPOINT

gmaster에서 checkpoint를 처리하는 시간이다.   
Parameter: None

<a id="071c2eb5b901dc1f"></a>
### GMASTER: IO SLAVE

gmaster에서 IO slave를 처리하는 시간이다.   
Parameter: None

<a id="ffaeb3a6e94fc217"></a>
### GMASTER: LOG FLUSH

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="67920cd43922ed6d"></a>
### GMASTER: PAGE FLUSH

gmaster에서 page flush를 처리하는 시간이다.   
Parameter: None

<a id="deff01ad1738bcf7"></a>
### WRITE: TRACE LOG

Trace log를 write하는 시간이다.   
Parameter: None

<a id="a591cb66874d2054"></a>
### WRITE: COPY ARCHIVING LOG

Archiving log를 복사하는 시간이다.   
Parameter: None

<a id="e5ff2c1f8649ddf8"></a>
### WRITE: BACKUP CTRL FILE

Control file을 백업하는 시간이다.   
Parameter: None

<a id="ba89f7107015991c"></a>
### WRITE: RESTORE CTRL FILE

Control file을 restore하는 시간이다.   
Parameter: None

<a id="50a9581fddf94a50"></a>
### READ: ARCHIVE LOG

Archive log file을 read하는 시간이다.   
Parameter: None

<a id="340c4f1a95601892"></a>
### READ: CTRL FILE

Control file을 read하는 시간이다.   
Parameter: None

<a id="141a79c4d8364574"></a>
### WRITE: LOG FILE

Log file을 write하는 시간이다.   
Parameter: None

<a id="3261c8bcfee7bab2"></a>
### WRITE: PAGE FILE

Page file을 write하는 시간이다.   
Parameter: None

<a id="68f298cc6044e518"></a>
### WRITE: CTRL FILE

Control file을 write하는 시간이다.   
Parameter: None

<a id="2eb1cf1b9a189364"></a>
### WRITE: REMOVE DATA FILE

Data file을 삭제하는 시간이다.   
Parameter: None

<a id="e7bb9a4197d91cdf"></a>
### WRITE: JOURNAL BUFFER

Journal buffer를 write하는 시간이다.   
Parameter: None

<a id="cb9ece282359c24f"></a>
### READ: JOURNAL BUFFER

Journal buffer를 read하는 시간이다.   
Parameter: None

<a id="64235b03f6c9fcdb"></a>
### WAIT TRANSACTION

Transaction을 wait하는 시간이다.

**PARAMETER**

<a id="5f69b32eb99cd6c4"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다릴 transaction id |

<a id="8ee0c598f8f64f2d"></a>
### WAIT OTHER TRANSACTION

다른 transaction이 종료되기를 wait하는 시간이다.

**PARAMETER**

<a id="4ad7fb137383e187"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다리는 transaction id |
| target transaction id | 종료 대상 transaction id |

<a id="4598cf063178cdb2"></a>
### WAIT ENABLE LOGGING

Logging이 가능할 때까지 wait하는 시간이다.   
Parameter: None

<a id="50f382163974185b"></a>
### WAIT LOG FLUSHER

Log flusher를 wait하는 시간이다.

**PARAMETER**

<a id="b41307fa2f0a2b7c"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="c3018f061cc963c8"></a>
### WAIT PAGE FLUSHER

Page flusher를 wait하는 시간이다.

**PARAMETER**

<a id="005982e40efe790e"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="ab89f3a2e6c5a28d"></a>
### WAIT XA CONTEXT

XA context를 wait하는 시간이다.   
Parameter: None

<a id="aca0ea0d0a3589a2"></a>
### LATCH: LOG BUFFER

Log buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="eaf743b5229ee471"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9a8b7370d114dd0f"></a>
### LATCH: PROCESS MANAGER

Process manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="0925ea81ce652d70"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bf92f3941ac0966a"></a>
### LATCH: ENV MGR

Env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="e7a1b5030492bc70"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c3a29e17baed8984"></a>
### LATCH: SESSION ENV MGR

Session env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="1cabe4310ef25dde"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="52d13419e5ad7cf2"></a>
### LATCH: PCH

Page Control Header (PCH) latch를 기다리는 시간이다.

**PARAMETER**

<a id="3e06e1ebe3637a8e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c7e8584929f2ee0b"></a>
### LATCH: PAGE

Page latch를 기다리는 시간이다.

**PARAMETER**

<a id="942a2fcdd667bfba"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e8bdbf468d37cb24"></a>
### LATCH: PENDING LOG

Pending log latch를 기다리는 시간이다.

**PARAMETER**

<a id="b2c03802383d1303"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d96b8af036c7967c"></a>
### LATCH: ALLOC TRANS

Allocate transaction latch를 기다리는 시간이다.

**PARAMETER**

<a id="a7f9e5473444039e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1702238135c54020"></a>
### LATCH: UNDO SEGMENT

Undo segment latch를 기다리는 시간이다.

**PARAMETER**

<a id="130c411391afd7f7"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b94a21d7097f5f16"></a>
### LATCH: CLUSTER LOCATION

Cluster location latch를 기다리는 시간이다.

**PARAMETER**

<a id="068aa8ea914670b8"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a0684984c2c948c5"></a>
### LATCH: DICT HASH ELEMENT AGING

Dict hash element aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="77d2ce493d3b0d71"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4dceb90cb6ea4c55"></a>
### LATCH: DICT HASH RELATED AGING

Dict hash related aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="5bc666f26a5cb955"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0196734de54fc8c3"></a>
### LATCH: FILE MANAGER

File manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="dec6a817ce6f3091"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="944319304e57e0ed"></a>
### LATCH: TRACE LOG

Trace log latch를 기다리는 시간이다.

**PARAMETER**

<a id="1d220c5bea23b5d4"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="353b06b6e2beeaa2"></a>
### LATCH: STATIC HASH

Static hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="cc5e8b0b40f2a36b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dbf17e1b1bcf5fab"></a>
### LATCH: STATIC HASH BUCKET

Static hash bucket latch를 기다리는 시간이다.

**PARAMETER**

<a id="a5c682871dc037e8"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="53b4daf3795cded0"></a>
### LATCH: SQL HANDLE

SQL handle latch를 기다리는 시간이다.

**PARAMETER**

<a id="f7c4c6dad4201efd"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b72a4c30890f7c40"></a>
### LATCH: XA CONTEXT HASH

XA context hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="a77099b3a4753874"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9ee0d5c19229b1f1"></a>
### LATCH: PLAN CLOCK

Plan clock latch를 기다리는 시간이다.

**PARAMETER**

<a id="a802597fcfb303ea"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="fad08d1e83ffe7ff"></a>
### LATCH: XA CONTEXT

XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="29dc4cab29331453"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2b24db574da29c45"></a>
### LATCH: MEM CONTROLLER

Memory controller latch를 기다리는 시간이다.

**PARAMETER**

<a id="40ef227dbcd09f6d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="566fd74365843678"></a>
### LATCH: DYNAMIC MEM

Dynamic memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="b75bdb123c670f06"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1cf6810e839c3042"></a>
### LATCH: PROPERTY

Property latch를 기다리는 시간이다.

**PARAMETER**

<a id="0068676096aa3fc3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ae4f4121fa7d7735"></a>
### LATCH: ATTACH SHM

Attack shared memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="82ed01dc7c2bad13"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0ae72094869daa77"></a>
### LATCH: BACKUP TBS

Backup tablespacce latch를 기다리는 시간이다.

**PARAMETER**

<a id="a06268b5d090993f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0e64115896717900"></a>
### LATCH: DATABASE COMPONENT

Database component latch를 기다리는 시간이다.

**PARAMETER**

<a id="ba4e0687d728d605"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d6b8bd29e05f4548"></a>
### LATCH: TABLESPACE

Tablespace latch를 기다리는 시간이다.

**PARAMETER**

<a id="a137076be7a315af"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b1c9342a2e6d2256"></a>
### LATCH: BACKUP DATABASE

Backup database latch를 기다리는 시간이다.

**PARAMETER**

<a id="3c69aa6cb2333f9b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e3369fab4005143c"></a>
### LATCH: JOURNAL BUFFER

Journal buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="39cf932027283141"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a001154bdbbbfcf7"></a>
### LATCH: JOURNAL BUFFER ENTRY

Journal buffer entry latch를 기다리는 시간이다.

**PARAMETER**

<a id="326e0d363e300023"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d8aa5cdb146a057f"></a>
### LATCH: JOURNAL WRITE BUFFER

Journal write buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="5f66f318635b4fe3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cc71d0b7744dd70b"></a>
### LATCH: LOCK ITEM

Lock item latch를 기다리는 시간이다.

**PARAMETER**

<a id="36ab80d4780bfd5f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5bff2a4fbfc3a532"></a>
### LATCH: RECORD HASH

Record hash latch를 기다리는 시간

**PARAMETER**

<a id="2061970776d08719"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a1f496c297aeb27d"></a>
### LATCH: DEADLOCK

Deadlock latch를 기다리는 시간이다.

**PARAMETER**

<a id="18ba960868534da9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="18a642da3bb8dbaa"></a>
### LATCH: SEQUENCE

Sequence latch를 기다리는 시간이다.

**PARAMETER**

<a id="1d5d2882270f3c57"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="5c4343e6087bf802"></a>
### LATCH: LOG STREAM

Log stream latch를 기다리는 시간이다.

**PARAMETER**

<a id="551f64c910db9067"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="486af59712177294"></a>
### LATCH: BUILD AGABLE SCN

Build agable SCN latch를 기다리는 시간이다.

**PARAMETER**

<a id="b13462f4b603e9f3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7b73819b3b52d0b2"></a>
### LATCH: TRANSACTION TABLE

Transaction table latch를 기다리는 시간이다.

**PARAMETER**

<a id="22d7b7ab7c7aa2ee"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="120db04696e95f23"></a>
### LATCH: SESSION LINK HASH

Session link hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="d8be2274a88f989c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9d22a6b147924a0a"></a>
### LATCH: ALLOC XA CONTEXT

Allocate XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="0e7d5e4ca6528b5e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2dcae42f4af9c376"></a>
### LATCH: SEQUENCE GLOBALX

Sequence global latch X를 기다리는 시간이다.

**PARAMETER**

<a id="5b69cc640bde6689"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bccc24754d1116ed"></a>
### LATCH: SEQUENCE GLOBALY

Sequence global latch Y를 기다리는 시간이다.

**PARAMETER**

<a id="71284d5df02051b7"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="caa23fcb0a5a1304"></a>
### LATCH: TRANSACTION LOG FILE

Transaction logfile latch를 기다리는 시간이다.

**PARAMETER**

<a id="aee3cb74fc19f029"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
