<a id="f3a65f9f655ee5d5"></a>

# 부록 B. Wait Event

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/f3a65f9f655ee5d5)  
> 태그: `20c.1_30_tag`

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<a id="9920a315cbf960cd"></a>
## Wait Event

Wait event와 관련된 performance view는 다음과 같다.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#7b4f41981d816b02)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#97cb17270406b3c4)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#1930895093ecae52)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#01f11275e2a37135)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#13f8bec17d4e8182)

<a id="30414d47981b864e"></a>
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

<a id="d3d8880601e26020"></a>
## Wait Event 항목

<a id="512e6943c972fbff"></a>
### ENQUEUE: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 request를 enqueue하는 시간이다.   
Parameter: None

<a id="4b09fa24efb87ba4"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="3b61cce572960636"></a>
### DEQUEUE: SHARED-SERVER REQUEST

Shared mode에서 shared server가 request를 dequeue하는 시간이다.   
Parameter: None

<a id="05756061c2cb1eea"></a>
### DEQUEUE: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 dequeue하는 시간이다.   
Parameter: None

<a id="9d617d0dcccf73ea"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

Dedicate mode에서 dedicate server가 spool 된 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="abcbca83fc41fb36"></a>
| Parameter | Description |
| --- | --- |
| send data size | Send 할 data byte |

<a id="f7f1e1f70c88062d"></a>
### SEND: DEDICATE-SERVER RESPONSE

Dedicate mode에서 dedicate server가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="e75566ae0737c109"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="47664faa9caa6ffd"></a>
### RECV: DEDICATE-SERVER REQUEST

Dedicate mode에서 dedicate server가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="ec4b83f320340b31"></a>
### SEND: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="13b177fc07c9d810"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="15ed208ac8aa7dc0"></a>
### RECV: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 client의 request를 receive하는 시간이다.   
Parameter: None

<a id="a6759a1ad51051d3"></a>
### ENQUEUE: CLUSTER REQUEST

Cluster의 request를 enqueue하는 시간이다.  
Parameter: None

<a id="98c8886f8327637e"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

Cluster의 broadcast request를 enqueue하는 시간이다.   
Parameter: None

<a id="05dedccdbecf0d08"></a>
### DEQUEUE: CLUSTER RESPONSE

Cluster의 response를 dequeue하는 시간이다.   
Parameter: None

<a id="55b26eb5e2003052"></a>
### SEND: CDISPATCHER

Cluster CDISPATCHER에서 send하는 시간이다.   
Parameter: None

<a id="a10d4a3d76d2abdd"></a>
### RECV: CDISPATCHER

Cluster CDISPATCHER에서 receive 하는 시간이다.   
Parameter: None

<a id="7fdb2a279b0a03f7"></a>
### GMASTER: ARCHIVE LOG

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="fe5c32b2ba4d6c22"></a>
### GMASTER: CHECKPOINT

gmaster에서 checkpoint를 처리하는 시간이다.   
Parameter: None

<a id="d263d139a5ca1b11"></a>
### GMASTER: IO SLAVE

gmaster에서 IO slave를 처리하는 시간이다.   
Parameter: None

<a id="5ab715e0683819ca"></a>
### GMASTER: LOG FLUSH

gmaster에서 archive log를 처리하는 시간이다.   
Parameter: None

<a id="99b1a3a3b5553fe8"></a>
### GMASTER: PAGE FLUSH

gmaster에서 page flush를 처리하는 시간이다.   
Parameter: None

<a id="3dcd9f06e22d2416"></a>
### WRITE: TRACE LOG

Trace log를 write하는 시간이다.   
Parameter: None

<a id="0bf27b080bde6ab1"></a>
### WRITE: COPY ARCHIVING LOG

Archiving log를 복사하는 시간이다.   
Parameter: None

<a id="83ec6510fd1e2c4b"></a>
### WRITE: BACKUP CTRL FILE

Control file을 백업하는 시간이다.   
Parameter: None

<a id="673b7947aeb087a8"></a>
### WRITE: RESTORE CTRL FILE

Control file을 restore하는 시간이다.   
Parameter: None

<a id="b3347fa455041388"></a>
### READ: ARCHIVE LOG

Archive log file을 read하는 시간이다.   
Parameter: None

<a id="4c1bef6f5b30110f"></a>
### READ: CTRL FILE

Control file을 read하는 시간이다.   
Parameter: None

<a id="2c606fec4e3d5da2"></a>
### WRITE: LOG FILE

Log file을 write하는 시간이다.   
Parameter: None

<a id="fa0eec8a780d3cdd"></a>
### WRITE: PAGE FILE

Page file을 write하는 시간이다.   
Parameter: None

<a id="4aa8b3a6e3a45da4"></a>
### WRITE: CTRL FILE

Control file을 write하는 시간이다.   
Parameter: None

<a id="5f9db185ba402d3d"></a>
### WRITE: REMOVE DATA FILE

Data file을 삭제하는 시간이다.   
Parameter: None

<a id="153b6df6bb4fe4b9"></a>
### WRITE: JOURNAL BUFFER

Journal buffer를 write하는 시간이다.   
Parameter: None

<a id="7bd4f21046cfe272"></a>
### READ: JOURNAL BUFFER

Journal buffer를 read하는 시간이다.   
Parameter: None

<a id="1cc95ec73ecb26f2"></a>
### WAIT TRANSACTION

Transaction을 wait하는 시간이다.

**PARAMETER**

<a id="50b51a321351048c"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다릴 transaction id |

<a id="2cb72bec9cdce8e2"></a>
### WAIT OTHER TRANSACTION

다른 transaction이 종료되기를 wait하는 시간이다.

**PARAMETER**

<a id="c53de39279ad370b"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다리는 transaction id |
| target transaction id | 종료 대상 transaction id |

<a id="361aab87a06e3180"></a>
### WAIT ENABLE LOGGING

Logging이 가능할 때까지 wait하는 시간이다.   
Parameter: None

<a id="48c2b16ce322715f"></a>
### WAIT LOG FLUSHER

Log flusher를 wait하는 시간이다.

**PARAMETER**

<a id="a04a86279a2fa833"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="ffd48ee290a81809"></a>
### WAIT PAGE FLUSHER

Page flusher를 wait하는 시간이다.

**PARAMETER**

<a id="eb68d270fcd6a015"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="7e2db07c2cba7cb0"></a>
### WAIT XA CONTEXT

XA context를 wait하는 시간이다.   
Parameter: None

<a id="8139c7b21a54f7fd"></a>
### LATCH: LOG BUFFER

Log buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="bc7d91e5a1e4e10b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2d0ff1a41a4ab460"></a>
### LATCH: PROCESS MANAGER

Process manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="b6f631af455753b0"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="589b6297c9b5f0c0"></a>
### LATCH: ENV MGR

Env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="1388cbdf18fa3329"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="16aa44201d6c7b97"></a>
### LATCH: SESSION ENV MGR

Session env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="7f2f2e68af833b2d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="10ec35e41f2593ae"></a>
### LATCH: PCH

Page Control Header (PCH) latch를 기다리는 시간이다.

**PARAMETER**

<a id="95bdbf7d63639639"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ef453d0463849268"></a>
### LATCH: PAGE

Page latch를 기다리는 시간이다.

**PARAMETER**

<a id="487db3b8de532586"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ef566284b1e8a9e4"></a>
### LATCH: PENDING LOG

Pending log latch를 기다리는 시간이다.

**PARAMETER**

<a id="a856eff550d221cd"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8554240ea969fd3a"></a>
### LATCH: ALLOC TRANS

Allocate transaction latch를 기다리는 시간이다.

**PARAMETER**

<a id="3ff985f52e6a70b3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c579dd178586b344"></a>
### LATCH: UNDO SEGMENT

Undo segment latch를 기다리는 시간이다.

**PARAMETER**

<a id="65dcd6cce96e39db"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a835dbae9059e24a"></a>
### LATCH: CLUSTER LOCATION

Cluster location latch를 기다리는 시간이다.

**PARAMETER**

<a id="b784e206087edad2"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f78d09abeabcf6bd"></a>
### LATCH: DICT HASH ELEMENT AGING

Dict hash element aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="13468c1d28a8a0fc"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ad60d8c369752373"></a>
### LATCH: DICT HASH RELATED AGING

Dict hash related aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="f40fefb8229be0ae"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4509be6ab98771c4"></a>
### LATCH: FILE MANAGER

File manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="64a98e66a323e914"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a6fd87e099bb9cdd"></a>
### LATCH: TRACE LOG

Trace log latch를 기다리는 시간이다.

**PARAMETER**

<a id="c9d0ab40c30a9f1f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e7396aca1fec92c2"></a>
### LATCH: STATIC HASH

Static hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="08b4ba8ac8dcb751"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="74a1d16191249b73"></a>
### LATCH: STATIC HASH BUCKET

Static hash bucket latch를 기다리는 시간이다.

**PARAMETER**

<a id="31e7e5864f26cb4f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="742687eeade966ff"></a>
### LATCH: SQL HANDLE

SQL handle latch를 기다리는 시간이다.

**PARAMETER**

<a id="55445f2298fc852e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4beb4a1854b1ecf0"></a>
### LATCH: XA CONTEXT HASH

XA context hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="19d0089cb7da67ca"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="110869e00b587570"></a>
### LATCH: PLAN CLOCK

Plan clock latch를 기다리는 시간이다.

**PARAMETER**

<a id="46595d98e438a58d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="962d22edc3593585"></a>
### LATCH: XA CONTEXT

XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="5c42baa3db9cf17c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="fb9a7f905d885de0"></a>
### LATCH: MEM CONTROLLER

Memory controller latch를 기다리는 시간이다.

**PARAMETER**

<a id="206c8d5e0444978b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8e839a73da223f2c"></a>
### LATCH: DYNAMIC MEM

Dynamic memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="2500b8f6c18a734a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e5a000495afddcfd"></a>
### LATCH: PROPERTY

Property latch를 기다리는 시간이다.

**PARAMETER**

<a id="df314d0969f12d37"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d804b864e1aee8e0"></a>
### LATCH: ATTACH SHM

Attack shared memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="bfff5dfb1cf8988f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4693284e94cd211b"></a>
### LATCH: BACKUP TBS

Backup tablespacce latch를 기다리는 시간이다.

**PARAMETER**

<a id="e945e594971a7167"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cf096266c4e2458b"></a>
### LATCH: DATABASE COMPONENT

Database component latch를 기다리는 시간이다.

**PARAMETER**

<a id="ff11e8c11c38da76"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="91f02f46cfa532ed"></a>
### LATCH: TABLESPACE

Tablespace latch를 기다리는 시간이다.

**PARAMETER**

<a id="1abd60d5c2abb649"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8adbc6773c6adcff"></a>
### LATCH: BACKUP DATABASE

Backup database latch를 기다리는 시간이다.

**PARAMETER**

<a id="fc57cf448317ee0b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0eafecc57a037757"></a>
### LATCH: JOURNAL BUFFER

Journal buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="02744e9800ec22b4"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7614aef71aa348a1"></a>
### LATCH: JOURNAL BUFFER ENTRY

Journal buffer entry latch를 기다리는 시간이다.

**PARAMETER**

<a id="3b614e3b6889428e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="cbb50f402c9e507f"></a>
### LATCH: JOURNAL WRITE BUFFER

Journal write buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="de25af24a7ed966b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c9bb3e6c9292db22"></a>
### LATCH: LOCK ITEM

Lock item latch를 기다리는 시간이다.

**PARAMETER**

<a id="af714ae057999b1b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="35c92a0ec9d5ad3e"></a>
### LATCH: RECORD HASH

Record hash latch를 기다리는 시간

**PARAMETER**

<a id="93f1cd75d1b47bcd"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="205ba97c5c695859"></a>
### LATCH: DEADLOCK

Deadlock latch를 기다리는 시간이다.

**PARAMETER**

<a id="dba71a1554051774"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="609a254f06e42c46"></a>
### LATCH: SEQUENCE

Sequence latch를 기다리는 시간이다.

**PARAMETER**

<a id="7ec011f852850586"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ab63d3ec3abeac36"></a>
### LATCH: LOG STREAM

Log stream latch를 기다리는 시간이다.

**PARAMETER**

<a id="97e1e9ee99e6e2c4"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c5cc1de2c57edf27"></a>
### LATCH: BUILD AGABLE SCN

Build agable SCN latch를 기다리는 시간이다.

**PARAMETER**

<a id="0255d8527226b240"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a1036008af5c0ce1"></a>
### LATCH: TRANSACTION TABLE

Transaction table latch를 기다리는 시간이다.

**PARAMETER**

<a id="fb7a58210cb2ba96"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="faec4e6ca9fe977d"></a>
### LATCH: SESSION LINK HASH

Session link hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="af914a7156a7d297"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d61a1da39ffbd228"></a>
### LATCH: ALLOC XA CONTEXT

Allocate XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="0f3f5119ca6a2a1e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="503d7a8b706d52e4"></a>
### LATCH: SEQUENCE GLOBALX

Sequence global latch X를 기다리는 시간이다.

**PARAMETER**

<a id="41d37af0b77d50f6"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="4db2254f64a91072"></a>
### LATCH: SEQUENCE GLOBALY

Sequence global latch Y를 기다리는 시간이다.

**PARAMETER**

<a id="809b78bdb33be852"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="998f5af58ea2ca37"></a>
### LATCH: TRANSACTION LOG FILE

Transaction logfile latch를 기다리는 시간이다.

**PARAMETER**

<a id="4ec61a8774e8c052"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
