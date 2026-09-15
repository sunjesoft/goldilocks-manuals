<a id="2cabfa49a0322098"></a>

# 부록 B. Wait Event

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/2cabfa49a0322098)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<a id="1903d249327abca6"></a>
## Wait Event

Wait event와 관련된 performance view는 다음과 같다.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#0b225c107903b9d9)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#7b861b651db03450)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#8fe8aa04bdd6de62)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#90930114d7a2f958)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#b2cfca320c875842)

<a id="d1f1e514db01259b"></a>
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

<a id="bf2cf3f216545b58"></a>
## Wait Event 항목

<a id="6f8feb3df6f0f394"></a>
### ENQUEUE: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 request를 enqueue하는 시간이다.  
Parameter: None

<a id="279cf85bda56d5cd"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

Shared mode에서 shared server가 request를 dequeue하는 시간이다.  
Parameter: None

<a id="c512ff1e90b089cc"></a>
### DEQUEUE: SHARED-SERVER REQUEST

Shared mode에서 shared server가 request를 dequeue하는 시간이다.  
Parameter: None

<a id="b509f00c29e844d1"></a>
### DEQUEUE: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 dequeue하는 시간이다.  
Parameter: None

<a id="ee59ac137c3ea8c6"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

Dedicate mode에서 dedicate server가 spool 된 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="99021eed12ef0236"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="fe9cf402aeee9301"></a>
### SEND: DEDICATE-SERVER RESPONSE

Dedicate mode에서 dedicate server가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="0c48392145ddb786"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="a9a0e79fc2bccae6"></a>
### RECV: DEDICATE-SERVER REQUEST

Dedicate mode에서 dedicate server가 client의 request를 receive하는 시간이다.  
Parameter: None

<a id="e181fa4093aa9d5e"></a>
### SEND: GDISPATCHER RESPONSE

Shared mode에서 GDISPATCHER가 response를 client로 send하는 시간이다.

**PARAMETER**

<a id="3504a043c182f128"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="382bfc8f84529612"></a>
### RECV: GDISPATCHER REQUEST

Shared mode에서 GDISPATCHER가 client의 request를 receive하는 시간이다.  
Parameter: None

<a id="b21597bb18914b74"></a>
### ENQUEUE: CLUSTER REQUEST

Cluster의 request를 enqueue하는 시간이다.  
Parameter: None

<a id="3bf5de9871b7930f"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

Cluster의 broadcast request를 enqueue하는 시간이다.  
Parameter: None

<a id="4d2b927a9780bf5a"></a>
### DEQUEUE: CLUSTER RESPONSE

Cluster의 response를 dequeue하는 시간이다.  
Parameter: None

<a id="05013bbdfffbbd45"></a>
### SEND: CDISPATCHER

Cluster CDISPATCHER에서 send하는 시간이다.  
Parameter: None

<a id="2c2a5d2367c62129"></a>
### RECV: CDISPATCHER

Cluster CDISPATCHER에서 receive 하는 시간이다.  
Parameter: None

<a id="d03a82f3294e5c0a"></a>
### GMASTER: ARCHIVE LOG

gmaster에서 archive log를 처리하는 시간이다.  
Parameter: None

<a id="c3678b557b60fd5a"></a>
### GMASTER: CHECKPOINT

gmaster에서 checkpoint를 처리하는 시간이다.  
Parameter: None

<a id="4d3a1fc798233899"></a>
### GMASTER: IO SLAVE

gmaster에서 IO slave를 처리하는 시간이다.  
Parameter: None

<a id="59632845f592c101"></a>
### GMASTER: LOG FLUSH

gmaster에서 archive log를 처리하는 시간이다.  
Parameter: None

<a id="d7db0988dbf9edeb"></a>
### GMASTER: PAGE FLUSH

gmaster에서 page flush를 처리하는 시간이다.  
Parameter: None

<a id="8998bd9e596f094d"></a>
### WRITE: TRACE LOG

Trace log를 write하는 시간이다.  
Parameter: None

<a id="efbb7ece78399a5b"></a>
### WRITE: COPY ARCHIVING LOG

Archiving log를 복사하는 시간이다.  
Parameter: None

<a id="2f1cc076be4b792f"></a>
### WRITE: BACKUP CTRL FILE

Control file을 백업하는 시간이다.  
Parameter: None

<a id="7652f84b69519e8d"></a>
### WRITE: RESTORE CTRL FILE

Control file을 restore하는 시간이다.  
Parameter: None

<a id="ede9ad34fb138713"></a>
### READ: ARCHIVE LOG

Archive log file을 read하는 시간이다.  
Parameter: None

<a id="28322c0b1d8a7f38"></a>
### READ: CTRL FILE

Control file을 read하는 시간이다.  
Parameter: None

<a id="b694442cacae46b8"></a>
### WRITE: LOG FILE

Log file을 write하는 시간이다.  
Parameter: None

<a id="3c20e44fe305af09"></a>
### WRITE: PAGE FILE

Page file을 write하는 시간이다.  
Parameter: None

<a id="07aacf9951b29ab5"></a>
### WRITE: CTRL FILE

Control file을 write하는 시간이다.  
Parameter: None

<a id="9fd3fa3b3c94dfc5"></a>
### WRITE: REMOVE DATA FILE

Data file을 삭제하는 시간이다.  
Parameter: None

<a id="82721c59aa795cad"></a>
### WRITE: JOURNAL BUFFER

Journal buffer를 write하는 시간이다.  
Parameter: None

<a id="1dc9f24369f957d4"></a>
### READ: JOURNAL BUFFER

Journal buffer를 read하는 시간이다.  
Parameter: None

<a id="39930c8f43805b48"></a>
### WAIT TRANSACTION

Transaction을 wait하는 시간이다.

**PARAMETER**

<a id="09a1052a3903c57f"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다릴 transaction id |

<a id="4ce731ef4c8352b7"></a>
### WAIT OTHER TRANSACTION

다른 transaction이 종료되기를 wait하는 시간이다.

**PARAMETER**

<a id="9521404bd06f9ad5"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다리는 transaction id |
| target transaction id | 종료 대상 transaction id |

<a id="a4e1acb10979e26d"></a>
### WAIT ENABLE LOGGING

Logging이 가능할 때까지 wait하는 시간이다.  
Parameter: None

<a id="3dafac0b6f2b7e06"></a>
### WAIT LOG FLUSHER

Log flusher를 wait하는 시간이다.

**PARAMETER**

<a id="26e644e51f4d83e4"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="2c5439235e8810d9"></a>
### WAIT PAGE FLUSHER

Page flusher를 wait하는 시간이다.

**PARAMETER**

<a id="7bdb9480c47d9298"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="0307ececbf900259"></a>
### WAIT XA CONTEXT

XA context를 wait하는 시간이다.  
Parameter: None

<a id="244f89b5317aac80"></a>
### LATCH: LOG BUFFER

Log buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="047860b87eff5f7f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3491962de6ff9551"></a>
### LATCH: PROCESS MANAGER

Process manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="a9108c265aba9d8d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c045f5660444c1cc"></a>
### LATCH: ENV MGR

Env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="356d0d688165d772"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="056907b17344fd69"></a>
### LATCH: SESSION ENV MGR

Session env manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="c4962f4a9e3c664e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="72a62bcc382e07a7"></a>
### LATCH: PCH

Page Control Header (PCH) latch를 기다리는 시간이다.

**PARAMETER**

<a id="a32bf62aa6df3747"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f611b0ae02133e73"></a>
### LATCH: PAGE

Page latch를 기다리는 시간이다.

**PARAMETER**

<a id="2982c2740649d6ce"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7a68831bb4468199"></a>
### LATCH: PENDING LOG

Pending log latch를 기다리는 시간이다.

**PARAMETER**

<a id="f8bbfc1eb0347eef"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="96b32db2920e602f"></a>
### LATCH: ALLOC TRANS

Allocate transaction latch를 기다리는 시간이다.

**PARAMETER**

<a id="b9f783eb0a332cdd"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a555ec33bf614ca5"></a>
### LATCH: UNDO SEGMENT

Undo segment latch를 기다리는 시간이다.

**PARAMETER**

<a id="eef49552cbe21545"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f846a67b187540fd"></a>
### LATCH: CLUSTER LOCATION

Cluster location latch를 기다리는 시간이다.

**PARAMETER**

<a id="630fbe5b388310d1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e77b2dfd016d938e"></a>
### LATCH: DICT HASH ELEMENT AGING

Dict hash element aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="a9027797df8ffbe1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8c732ddd59a98407"></a>
### LATCH: DICT HASH RELATED AGING

Dict hash related aging latch를 기다리는 시간이다.

**PARAMETER**

<a id="44e877de0cb97f96"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bd7a823d235b1f1d"></a>
### LATCH: FILE MANAGER

File manager latch를 기다리는 시간이다.

**PARAMETER**

<a id="11bef5d6bbcfb113"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="dc71b742eb1283e4"></a>
### LATCH: TRACE LOG

Trace log latch를 기다리는 시간이다.

**PARAMETER**

<a id="713220e550f31c22"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2099b85d08732e1e"></a>
### LATCH: STATIC HASH

Static hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="a53c4c27fc07b6a8"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="644cb16295cad5b1"></a>
### LATCH: STATIC HASH BUCKET

Static hash bucket latch를 기다리는 시간이다.

**PARAMETER**

<a id="962d2fddcb2f2a6e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="37968afd127e8a82"></a>
### LATCH: SQL HANDLE

SQL handle latch를 기다리는 시간이다.

**PARAMETER**

<a id="00b330580207dd05"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="3bd7a154ed273cc8"></a>
### LATCH: XA CONTEXT HASH

XA context hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="bd01868be4e7d43e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="73029f10acdd4d77"></a>
### LATCH: PLAN CLOCK

Plan clock latch를 기다리는 시간이다.

**PARAMETER**

<a id="9e5798969f55af0f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d9b7f0648ce98d7b"></a>
### LATCH: XA CONTEXT

XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="a67bf1e8fb09170d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0b97f8eeddc1ef15"></a>
### LATCH: MEM CONTROLLER

Memory controller latch를 기다리는 시간이다.

**PARAMETER**

<a id="337a43cc6a9f9650"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="64c859a53596a96f"></a>
### LATCH: DYNAMIC MEM

Dynamic memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="8cb1519978e9327c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9fc356d5539a3f84"></a>
### LATCH: PROPERTY

Property latch를 기다리는 시간이다.

**PARAMETER**

<a id="eefe857376c3a5b9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="c3037943e2b9a4c7"></a>
### LATCH: ATTACH SHM

Attack shared memory latch를 기다리는 시간이다.

**PARAMETER**

<a id="92d8d95ee5150a95"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="81b67aab36ab12d4"></a>
### LATCH: BACKUP TBS

Backup tablespace latch를 기다리는 시간이다.

**PARAMETER**

<a id="d257e023434aa18a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="00622ee1cf1a8ac9"></a>
### LATCH: DATABASE COMPONENT

Database component latch를 기다리는 시간이다.

**PARAMETER**

<a id="ef1cde2348c3bca2"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="613f37fb3509b77f"></a>
### LATCH: TABLESPACE

Tablespace latch를 기다리는 시간이다.

**PARAMETER**

<a id="fd6f939b61d4caaa"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="350aaeb7450666cf"></a>
### LATCH: BACKUP DATABASE

Backup database latch를 기다리는 시간이다.

**PARAMETER**

<a id="5afc60492194fe98"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d39a799a8d1106d5"></a>
### LATCH: JOURNAL BUFFER

Journal buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="3c1cb9c7af2862a9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="aeacd919cf7569c8"></a>
### LATCH: JOURNAL BUFFER ENTRY

Journal buffer entry latch를 기다리는 시간이다.

**PARAMETER**

<a id="e39db7c9b6618299"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b214fe98aaa94ca4"></a>
### LATCH: JOURNAL WRITE BUFFER

Journal write buffer latch를 기다리는 시간이다.

**PARAMETER**

<a id="df85924052c8564a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bb5f5308e2fc07b3"></a>
### LATCH: LOCK ITEM

Lock item latch를 기다리는 시간이다.

**PARAMETER**

<a id="1909cb408cc58a4b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1f4bc770671b2adb"></a>
### LATCH: RECORD HASH

Record hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="a61a211e46405f1f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6e89cf2c0fe218a1"></a>
### LATCH: DEADLOCK

Deadlock latch를 기다리는 시간이다.

**PARAMETER**

<a id="5bcfebd9f06009d1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0c6752c6e9d72269"></a>
### LATCH: SEQUENCE

Sequence latch를 기다리는 시간이다.

**PARAMETER**

<a id="0c09ef0329fdc6c1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="767efe92fa332c15"></a>
### LATCH: LOG STREAM

Log stream latch를 기다리는 시간이다.

**PARAMETER**

<a id="b1e1fe9a6cc8d617"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9eed672449b2ad67"></a>
### LATCH: BUILD AGABLE SCN

Build agable SCN latch를 기다리는 시간이다.

**PARAMETER**

<a id="d057ae15a3a89266"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="55ab0087ca4015ae"></a>
### LATCH: TRANSACTION TABLE

Transaction table latch를 기다리는 시간이다.

**PARAMETER**

<a id="bde80231e8fb772b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b8b3dff105c6c778"></a>
### LATCH: SESSION LINK HASH

Session link hash latch를 기다리는 시간이다.

**PARAMETER**

<a id="813da0cabe174339"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8e6f279606de92cd"></a>
### LATCH: ALLOC XA CONTEXT

Allocate XA context latch를 기다리는 시간이다.

**PARAMETER**

<a id="f93fbae37064e3ec"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="80cdc026f7ace08d"></a>
### LATCH: SEQUENCE GLOBALX

Sequence global latch X를 기다리는 시간이다.

**PARAMETER**

<a id="edc09408823a3b25"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="035970b4f021f54e"></a>
### LATCH: SEQUENCE GLOBALY

Sequence global latch Y를 기다리는 시간이다.

**PARAMETER**

<a id="cd2faab55a541ce8"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2f829daf9d5dca44"></a>
### LATCH: TRANSACTION LOG FILE

Transaction logfile latch를 기다리는 시간이다.

**PARAMETER**

<a id="110a359a5bf074bc"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

---

[← 부록 A. Error Codes](appendix-01-부록-a-error-codes.md) · [전체 목차](../README.md) · [부록 C. Open Source License →](appendix-03-부록-c-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
