<a id="67b2191de001eb2e"></a>

# 부록 C. Wait Event

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/67b2191de001eb2e)  
> 태그: `22c.1_10_tag`

[← 부록 B. Error Codes](appendix-02-부록-b-error-codes.md) · [전체 목차](../README.md) · [부록 D. Open Source License →](appendix-04-부록-d-open-source-license.md)

<a id="e3225e04df8f2cdc"></a>
## Wait Event

Wait event와 관련된 performance view는 다음과 같다.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#8e77ec82f5f66055)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#02fdf479273f9149)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#dc3837e90ab0be65)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#8f9015565637a29c)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#c020ace7ab77d45f)

<a id="532cd908556b4abf"></a>
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

<a id="82067e5492dd3c10"></a>
## Wait Event 항목

<a id="f7e3b5ec77696edc"></a>
### ENQUEUE: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 request를 enqueue하는 시간이다.   
Parameter: None

<a id="9bf2ab4990f1358b"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="7dd9ec0f5960fe6b"></a>
### DEQUEUE: SHARED-SERVER REQUEST

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="4d15cf144aa6ad82"></a>
### DEQUEUE: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 dequeue하는 시간이다.   
Parameter: None

<a id="a2baecc05ae3ac43"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

Dedicate mode에서 dedicate server가 spool 된 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="cfecce22ff77941b"></a>
| Parameter | Description |
| --- | --- |
| send data size | Send 할 data byte |

<a id="86d3ebd0b563161c"></a>
### SEND: DEDICATE-SERVER RESPONSE

Dedicate mode에서 dedicate server가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="da279b65383fd826"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="e1d86434d7dc6328"></a>
### RECV: DEDICATE-SERVER REQUEST

Dedicate mode에서 dedicate server가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="4bb8949cb4162497"></a>
### SEND: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="d956914655d988c5"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="83fd53adec33f77b"></a>
### RECV: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="282c87f6faad65b5"></a>
### ENQUEUE: CLUSTER REQUEST

Cluster의 request를 enqueue하는 시간이다.  
Parameter: None

<a id="230d038f7c5c20ab"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

Cluster의 broadcast request를 enqueue하는 시간이다.   
Parameter: None

<a id="9a65f79fd0322340"></a>
### DEQUEUE: CLUSTER RESPONSE

Cluster의 response를 dequeue하는 시간이다.   
Parameter: None

<a id="0332850a10760026"></a>
### SEND: CDISPATCHER

Cluster CDISPATCHER에서 send하는 시간이다.   
Parameter: None

<a id="b70f7af3d74100e1"></a>
### RECV: CDISPATCHER

Cluster CDISPATCHER에서 receive 하는 시간이다.   
Parameter: None

<a id="483a24c1f4fc538b"></a>
### GMASTER: ARCHIVE LOG

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="8e30f7bb3f373b18"></a>
### GMASTER: CHECKPOINT

gmaster에서 checkpoint를 처리하는 시간이다.   
Parameter: None

<a id="1c627640bccb44fe"></a>
### GMASTER: IO SLAVE

gmaster에서 IO slave를 처리하는 시간이다.   
Parameter: None

<a id="40e7a061ba055e8b"></a>
### GMASTER: LOG FLUSH

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="c773282b6d7acaa5"></a>
### GMASTER: PAGE FLUSH

gmaster에서 page flush를 처리하는 시간이다.   
Parameter: None

<a id="6ab15da90384a44a"></a>
### WRITE: TRACE LOG

Trace log를 write하는 시간이다.   
Parameter: None

<a id="414d56f058c993a2"></a>
### WRITE: COPY ARCHIVING LOG

Archiving log를 복사하는 시간이다.   
Parameter: None

<a id="7f6db8103819697a"></a>
### WRITE: BACKUP CTRL FILE

Control file을 백업하는 시간이다.   
Parameter: None

<a id="3144f191a4838986"></a>
### WRITE: RESTORE CTRL FILE

Control file을 restore하는 시간이다.   
Parameter: None

<a id="03da6192cb74125e"></a>
### READ: ARCHIVE LOG

Archive log file을 read하는 시간이다.   
Parameter: None

<a id="c53a5e9edbcb1885"></a>
### READ: CTRL FILE

Control file을 read하는 시간이다.   
Parameter: None

<a id="40aaaaefc1cc705e"></a>
### WRITE: LOG FILE

Log file을 write하는 시간이다.   
Parameter: None

<a id="187f064c8987610f"></a>
### WRITE: PAGE FILE

Page file을 write하는 시간이다.   
Parameter: None

<a id="37060bb22fad2cc6"></a>
### WRITE: CTRL FILE

Control file을 write하는 시간이다.   
Parameter: None

<a id="4004ba48c0626815"></a>
### WRITE: REMOVE DATA FILE

Data file을 삭제하는 시간이다.   
Parameter: None

<a id="922b5bb90d74f923"></a>
### WRITE: JOURNAL BUFFER

Journal buffer를 write하는 시간이다.   
Parameter: None

<a id="a6532374b819e303"></a>
### READ: JOURNAL BUFFER

Journal buffer를 read하는 시간이다.   
Parameter: None

<a id="52d5c0d655636ec4"></a>
### WAIT TRANSACTION

Transaction을 wait하는 시간이다.

**PARAMETER**

<a id="0e70d9af20ce6d6a"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다릴 transaction id |

<a id="b68770f74589a06d"></a>
### WAIT OTHER TRANSACTION

다른 transaction이 종료되기를 wait하는 시간이다.

**PARAMETER**

<a id="f05d078b12c4d68a"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다리는 transaction id |
| target transaction id | 종료 대상 transaction id |

<a id="694670296415df03"></a>
### WAIT ENABLE LOGGING

Logging이 가능할 때까지 wait하는 시간이다.   
Parameter: None

<a id="1ebecec76321904c"></a>
### WAIT LOG FLUSHER

Log flusher를 wait하는 시간이다.

**PARAMETER**

<a id="0d3006d3ae9e6a9c"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="63ad234efecad0b9"></a>
### WAIT PAGE FLUSHER

Page flusher를 wait하는 시간이다.

**PARAMETER**

<a id="ec4bda13b0627d35"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="754ab0ab50ca98c2"></a>
### WAIT XA CONTEXT

XA context를 wait하는 시간이다.   
Parameter: None

<a id="9fb7a43b88d8dbaa"></a>
### LATCH: LOG BUFFER

Log buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="080f6e481ce882e5"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="101c1d186bd8e4ca"></a>
### LATCH: PROCESS MANAGER

Process manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="9c39f5c749a0c538"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1805a90925d0a6c7"></a>
### LATCH: ENV MGR

Env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="5d38afda57ee704b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8135dbe4f864cb06"></a>
### LATCH: SESSION ENV MGR

Session env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="71d102696ef9605f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="13888fb736aff509"></a>
### LATCH: PCH

Page Control Header (PCH) latch를 기다리는 시간이다.

**PARAMETER**

<a id="db6145d40fe4a466"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3e20036d66ad99ea"></a>
### LATCH: PAGE

Page latch를 기다리는 시간이다.

**PARAMETER**

<a id="27137505e85b7b67"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="750845e4b27d47d2"></a>
### LATCH: PENDING LOG

Pending log latch를 기다리는 시간이다.

**PARAMETER**

<a id="5eb1cefcc4fb692a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="02b5731a15ff1717"></a>
### LATCH: ALLOC TRANS

Allocate transaction latch를 기다리는 시간이다.

**PARAMETER**

<a id="929a7e6b9e81b502"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f4bf0cb8c7f37475"></a>
### LATCH: UNDO SEGMENT

Undo segment latch를 기다리는 시간이다.

**PARAMETER**

<a id="4055589e6d53710f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a988eac0b2ce69a6"></a>
### LATCH: CLUSTER LOCATION

Cluster location latch를 기다리는 시간이다.

**PARAMETER**

<a id="b11c8b5ed473a39d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9c2092594ee840ca"></a>
### LATCH: DICT HASH ELEMENT AGING

Dict hash element aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="b83cb3b854d8d70d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="438d4b7af4459822"></a>
### LATCH: DICT HASH RELATED AGING

Dict hash related aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="7655dc5512dc32c3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="326ec4d6bf43324e"></a>
### LATCH: FILE MANAGER

File manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="f763492b7e9cc438"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="16a18441810a5b79"></a>
### LATCH: TRACE LOG

Trace log latch를 기다리는 시간이다.

**PARAMETER**

<a id="4596ac0a4ba9fea9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e26d50a7b0b339fb"></a>
### LATCH: STATIC HASH

Static hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="260509cd8a9e8808"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="87179d0cfd04f366"></a>
### LATCH: STATIC HASH BUCKET

Static hash bucket latch를 기다리는 시간이다.

**PARAMETER**

<a id="b23ecb4e5d7c01ba"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6cba0af8c33786ee"></a>
### LATCH: SQL HANDLE

SQL handle latch를 기다리는 시간이다.

**PARAMETER**

<a id="95e2b1a3e880a8de"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ea79e47e25721952"></a>
### LATCH: XA CONTEXT HASH

XA context hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="2919bfbd0ca4cbce"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="23de0cdaf0018ed0"></a>
### LATCH: PLAN CLOCK

Plan clock latch를 기다리는 시간이다.

**PARAMETER**

<a id="504014c5d376a83e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="67989d607b907674"></a>
### LATCH: XA CONTEXT

XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="4d0e2190dbfbc4a5"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e3dc1c2a4ba332db"></a>
### LATCH: MEM CONTROLLER

Memory controller latch를 기다리는 시간이다.

**PARAMETER**

<a id="5ca8cb3fe1453c8a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="acbbdd21f59a2c29"></a>
### LATCH: DYNAMIC MEM

Dynamic memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="822c5b212946dba7"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="715273b02b235dbd"></a>
### LATCH: PROPERTY

Property latch를 기다리는 시간이다.

**PARAMETER**

<a id="1498b1f95a056c37"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7f5771ff50649522"></a>
### LATCH: ATTACH SHM

Attack shared memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="ff8b72ca01cf9ab1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="590a7d7f580da24d"></a>
### LATCH: BACKUP TBS

Backup tablespacce latch를 기다리는 시간이다.

**PARAMETER**

<a id="552691177f87dbca"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4cced97abc81a4ff"></a>
### LATCH: DATABASE COMPONENT

Database component latch를 기다리는 시간이다.

**PARAMETER**

<a id="6f2ade5644396012"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ba9a8f0db9fc7845"></a>
### LATCH: TABLESPACE

Tablespace latch를 기다리는 시간이다.

**PARAMETER**

<a id="84c4338ded0bee3e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4a13bf5baf7f02f4"></a>
### LATCH: BACKUP DATABASE

Backup database latch를 기다리는 시간이다.

**PARAMETER**

<a id="df2c6a43aeaebee9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3f03d8ef472d9be2"></a>
### LATCH: JOURNAL BUFFER

Journal buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="2e2fe88b83be81f9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4d36b4b6056d254e"></a>
### LATCH: JOURNAL BUFFER ENTRY

Journal buffer entry latch를 기다리는 시간이다.

**PARAMETER**

<a id="fd12709b29261d28"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="59d9447f1a08b874"></a>
### LATCH: JOURNAL WRITE BUFFER

Journal write buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="09fd6f1bb749993f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="caa61fb786a6ad46"></a>
### LATCH: LOCK ITEM

Lock item latch를 기다리는 시간이다.

**PARAMETER**

<a id="48b25cc6dce622ff"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3ecbe74747cd8672"></a>
### LATCH: RECORD HASH

Record hash latch를 기다리는 시간

**PARAMETER**

<a id="b46d592168be504e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3470b1a64ccd0202"></a>
### LATCH: DEADLOCK

Deadlock latch를 기다리는 시간이다.

**PARAMETER**

<a id="ecc4c3aa6ab9bb6c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="50e2e4c72a756e5c"></a>
### LATCH: SEQUENCE

Sequence latch를 기다리는 시간이다.

**PARAMETER**

<a id="90e661a1540e6881"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4676b0e8d4be31b7"></a>
### LATCH: LOG STREAM

Log stream latch를 기다리는 시간이다.

**PARAMETER**

<a id="16d7b9bee367b97c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c4d5cda9cde1c36e"></a>
### LATCH: BUILD AGABLE SCN

Build agable SCN latch를 기다리는 시간이다.

**PARAMETER**

<a id="7db1794f8b1e274f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="78703a9600b4abd0"></a>
### LATCH: TRANSACTION TABLE

Transaction table latch를 기다리는 시간이다.

**PARAMETER**

<a id="0ca7610a48feef95"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="be41a94406b62af4"></a>
### LATCH: SESSION LINK HASH

Session link hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="f2b0062363b3a179"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f5f084ebe49236ec"></a>
### LATCH: ALLOC XA CONTEXT

Allocate XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="00e38509f8916b51"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a02af701e63172a7"></a>
### LATCH: SEQUENCE GLOBALX

Sequence global latch X를 기다리는 시간이다.

**PARAMETER**

<a id="d6d71c39d75cd8d0"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6575e959385a3398"></a>
### LATCH: SEQUENCE GLOBALY

Sequence global latch Y를 기다리는 시간이다.

**PARAMETER**

<a id="6bac46d68ac633ff"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="23e85f7a96baa3c3"></a>
### LATCH: TRANSACTION LOG FILE

Transaction logfile latch를 기다리는 시간이다.

**PARAMETER**

<a id="fbcea435acbd94a1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4ea432ea889c9ef2"></a>
### ASYNC RESPONSE

클러스터 환경에서 원격 노드로부터 응답을 기다리는 시간이다.  
Parameter: None

<a id="6a2243f7575fda8f"></a>
### ASYNC TRANSACTION

클러스터 환경에서 원격 노드로부터 ASYNC TRANSACTION의 COMMIT 응답을 기다리는 시간이다.  
Parameter: None

<a id="c03c339b7ebfb6f8"></a>
### ASYNC COMMIT

N/A

<a id="41f2dd27fdd36b9e"></a>
### GMASTER: BUFFER FLUSH

gmaster의 io slave가 buffer flush를 수행한 시간이다.  
Parameter: None

<a id="56722d5b9f6027ed"></a>
### LATCH: BUFFER HASH BUCKET

버퍼 해쉬 버킷의 latch를 기다리는 시간이다.

**PARAMETER**

<a id="7f3944603f13d5ab"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b566ad81e8096c1d"></a>
### READ: PAGE FILE

디스크 테이블스페이스의 페이지를 읽기 위해 디스크로부터 페이지를 read 한 시간이다.  
Parameter: None

<a id="8df9a58d298dd935"></a>
### LATCH: BUFFER CHECKPOINT LIST

N/A

<a id="9e3b1257a8783415"></a>
### WRITE: CHANGE TRACKING FILE

디스크 테이블스페이스의 change tracking file을 write 한 시간이다.  
Parameter: None

<a id="a5643a283116b681"></a>
### WAIT FREE BUFFER

디스크 테이블스페이스의 페이지를 읽기 위해 free buffer를 기다리는 시간이다.  
Parameter: None

<a id="d4273390fd663fb0"></a>
### GLOBAL SEQUENCE: LOCK AND QUERY

클러스터에서 global sequence를 동기화 하기 위해 모든 멤버에서 global latch를 기다린 시간과 global sequnce의 최신정보를 얻기 위해 기다린 시간이다.  
Parameter: None

<a id="a23cc7e4f05bfe27"></a>
### GLOBAL SEQUENCE: SYNC

클러스터에서 global sequence 동기화를 수행한 시간이다.  
Parameter: None

<a id="2f7c80f7cd172707"></a>
### LATCH: SEQUENCE GLOBAL NEXT

클러스터에서 sequence global next latch를 기다리는 시간이다.

**PARAMETER**

<a id="27b98cf5b3e95b5d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9b541afc05d0dd7e"></a>
### LATCH: BUFFER LRU LIST

버퍼 lru list latch를 기다리는 시간이다.

**PARAMETER**

<a id="8752349e5d1cfbd1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e6046ac49b9aa4df"></a>
### WAIT DIRTY PAGE LIMIT

버퍼에 캐싱된 페이지에 접근하기 위해 시스템의 dirty page 수가 [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#f27cdd06cf3054f4)보다 작아질 때까지 기다리는 시간이다.  
Parameter: None

<a id="f610342362664a74"></a>
### WAIT BUFFER READ COMPLETE

디스크 테이블스페이스의 페이지를 접근하기 위해 disk read가 완료될 때까지 기다리는 시간이다.  
Parameter: None

---

[← 부록 B. Error Codes](appendix-02-부록-b-error-codes.md) · [전체 목차](../README.md) · [부록 D. Open Source License →](appendix-04-부록-d-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
