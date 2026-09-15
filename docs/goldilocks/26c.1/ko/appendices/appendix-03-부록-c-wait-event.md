<a id="1a412fca34b671ba"></a>

# 부록 C. Wait Event

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/1a412fca34b671ba)  
> 태그: `26c.1_0_tag`

[← 부록 B. Error Codes](appendix-02-부록-b-error-codes.md) · [전체 목차](../README.md) · [부록 D. Open Source License →](appendix-04-부록-d-open-source-license.md)

<a id="5cfd239c155fbb49"></a>
## Wait Event

Wait event와 관련된 performance view는 다음과 같다.

- v$system_event [V$SYSTEM_EVENT](../part-02-administration-manual/9-database-information.md#3aeef7ff0e6515be)
- v$session_event [V$SESSION_EVENT](../part-02-administration-manual/9-database-information.md#86a28d80dde087fd)
- v$session_wait [V$SESSION_WAIT](../part-02-administration-manual/9-database-information.md#916f3c6bbc93eb7a)
- v$wait_event_name [V$WAIT_EVENT_NAME](../part-02-administration-manual/9-database-information.md#9f1a44a9403cd824)
- v$wait_event_class_name [V$WAIT_EVENT_CLASS_NAME](../part-02-administration-manual/9-database-information.md#f86a8ce21b44ac96)

<a id="887af32a98354fc7"></a>
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

<a id="997e4e8d5c36ae3f"></a>
## Wait Event 항목

<a id="3bdbcf9e4830b1b5"></a>
### ENQUEUE: GDISPATCHER REQUEST

GDISPATCHER가 shared server에게 request를 보낼 때 queue에서 대기하는 시간이다.  
Parameter: None

<a id="4f3391a314e376f4"></a>
### ENQUEUE: SHARED-SERVER RESPONSE

Shared server가 GDISPATCHER에게 response를 보낼 때 queue에서 대기하는 시간이다.   
Parameter: None

<a id="53de06be3d14090a"></a>
### DEQUEUE: SHARED-SERVER REQUEST

Shared server가 GDISPATCHER로부터 request를 받을 때 queue에서 대기하는 시간이다.   
Parameter: None

<a id="975f3c2a55e0f99f"></a>
### DEQUEUE: GDISPATCHER RESPONSE

GDISPATCHER가 shared server로부터 response를 받을 때 queue에서 대기하는 시간이다.   
Parameter: None

<a id="e078e24ee1ab7601"></a>
### SEND: DEDICATE-SERVER SPOOLED RESPONSE

Dedicate server가 spool 된 response를 client로 보낼 때 socket 또는 ipc에서 대기하는 시간이다.

**PARAMETER**

<a id="01a3c33ff11f1a48"></a>
| Parameter | Description |
| --- | --- |
| send data size | Send 할 data byte |

<a id="df837d4448e437a5"></a>
### SEND: DEDICATE-SERVER RESPONSE

Dedicate server가 response를 client로 보낼 때 socket 또는 ipc에서 대기하는 시간이다.

**PARAMETER**

<a id="71df14e41596b605"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="8b224452eb139664"></a>
### RECV: DEDICATE-SERVER REQUEST

Dedicate server가 client로부터 request를 받을 때 socket 또는 ipc에서 대기하는 시간이다.   
Parameter: None

<a id="f6b6c3b4329a2c84"></a>
### SEND: GDISPATCHER RESPONSE

GDISPATCHER가 client로 response를 보낼 때 socket에서 대기하는 시간이다.

**PARAMETER**

<a id="fcab32f18a5c4e04"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="bdba0424d445d9ed"></a>
### RECV: GDISPATCHER REQUEST

GDISPATCHER가 client로부터 request를 받을 때 socket에서 대기하는 시간이다.   
Parameter: None

<a id="3812653897260e1b"></a>
### ENQUEUE: CLUSTER REQUEST

Cluster에서 원격으로 request를 보낼 때 queue에서 대기하는 시간이다.  
Parameter: None

<a id="7f5c71c373af701d"></a>
### ENQUEUE: CLUSTER BROADCAST REQUEST

Cluster에서 원격으로 broadcast request를 보낼 때 queue에서 대기하는 시간이다.   
Parameter: None

<a id="a8105a71934594f8"></a>
### DEQUEUE: CLUSTER RESPONSE

Cluster에서 원격으로부터 response를 받을 때 queue에서 대기하는 시간이다.   
Parameter: None

<a id="1d648e32e3bf05d4"></a>
### SEND: CDISPATCHER

CDISPATCHER가 원격으로 메시지를 보낼 때 socket에서 대기하는 시간이다.   
Parameter: None

<a id="b41d97c060baa387"></a>
### RECV: CDISPATCHER

CDISPATCHER가 원격으로 메시지를 받을 때 socket에서 대기하는 시간이다.   
Parameter: None

<a id="31401588da5280c3"></a>
### WAIT TRANSACTION

특정 transaction이 종료하기를 기다리는 시간이다.

**PARAMETER**

<a id="31f8d55b5ca2f7ef"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다릴 transaction id |

<a id="04732e88c15d28bc"></a>
### WAIT OTHER TRANSACTION

다른 transaction이 lock 되어 있는 동안 기다리는 시간이다.   
예를 들어 A 트랜잭션이 B 트랜잭션의 종료를 기다릴 경우, A의 대기 시간을 의미한다.

**PARAMETER**

<a id="f900c718435f23ad"></a>
| Parameter | 설명 |
| --- | --- |
| wait transaction id | 기다리는 transaction id |
| target transaction id | 종료 대상 transaction id |

<a id="f86eaea98f076af2"></a>
### WAIT ENABLE LOGGING

Logging을 허용할 때까지 기다리는 시간이다.   
Parameter: None

<a id="75332f57bb78e8f0"></a>
### WAIT LOG FLUSHER

Log flusher가 log를 디스크에 기록할 때까지 세션이 대기하는 시간이다.

**PARAMETER**

<a id="4aa0ba1aeabe14a9"></a>
| Parameter | 설명 |
| --- | --- |
| send data size | Send 할 data byte |

<a id="89a0942065473d87"></a>
### WAIT XA CONTEXT

XA context를 다른 세션에서 사용 중일 때 세션이 대기하는 시간이다.   
Parameter: None

<a id="6484223c8eae835c"></a>
### LATCH: LOG BUFFER

Log buffer의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="ab5a27eb148e4cf5"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="28a1cc9894d7f433"></a>
### LATCH: PROCESS MANAGER

Process manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="69001cbe8d3ab26d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e062d8cb76f8c744"></a>
### LATCH: ENV MGR

Env manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="3e6f03b6f4f07733"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a6fa6793ee428515"></a>
### LATCH: SESSION ENV MGR

Session env manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="4c7e102111bc4421"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d9d2e96a44d10f11"></a>
### LATCH: PCH

Page Control Header (PCH)의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="ceb069eca54a80ce"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="321b2a87d6e00395"></a>
### LATCH: PAGE

Page layer의 latch를 획득하기 위해서 대기하는 시간이다.

**PARAMETER**

<a id="1f7ef560cffab79f"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b98e0b6ca0a3183d"></a>
### LATCH: PENDING LOG

Pending log buffer에 log를 기록하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="eeb6eb359a644316"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="75ae6d88d9054361"></a>
### LATCH: ALLOC TRANS

Transaction slot을 할당하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="45e98e9a09303fc9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f25142c1c0209c17"></a>
### LATCH: UNDO SEGMENT

Undo segment의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="bd679d7ba914220c"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="53faeb0ab11096e7"></a>
### LATCH: CLUSTER LOCATION

Cluster location의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="5a22d5bf2f2914ed"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="190e2071b8615dd3"></a>
### LATCH: DICT HASH ELEMENT AGING

삭제된 dictionary cache를 aging 할 때 latch에 대기하는 시간이다.

**PARAMETER**

<a id="18b6d3ec99208894"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f624d55607803ccd"></a>
### LATCH: DICT HASH RELATED AGING

삭제된 related dictionary cache를 aging 할 때 latch에 대기하는 시간이다.

**PARAMETER**

<a id="aef38059d81b17b6"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a43a8b0a12d8ee57"></a>
### LATCH: FILE MANAGER

File manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="1c85e02d6023ce4b"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="6d33018cff2f72d7"></a>
### LATCH: TRACE LOG

Trace log의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="53824f1fd6a12a57"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a1a7cd1df7d55c1f"></a>
### LATCH: STATIC HASH

Static hash의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="1a2bc048fd1bcb75"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="bd7471f29baa55ac"></a>
### LATCH: STATIC HASH BUCKET

Static hash의 bucket latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="bf7566cb492cf807"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="42ce605d50b46a2c"></a>
### LATCH: SQL HANDLE

SQL cache manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="fcde297ca1b53006"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="696f26eb21112413"></a>
### LATCH: XA CONTEXT HASH

Xa context hash의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="5cc90be23bc3b9e5"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="750e28a761fb09e0"></a>
### LATCH: PLAN CLOCK

SQL plan의 clock latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="36303a1aedc05193"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="979d48cece030538"></a>
### LATCH: XA CONTEXT

XA context의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="93172d8518036a7a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="47a8129b8ac5425f"></a>
### LATCH: MEM CONTROLLER

Memory controller의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="5596e68968bf1950"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="e0de3ec262b1bdaa"></a>
### LATCH: DYNAMIC MEM

Dynamic memory의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="c3a54a24e36141a3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="b3ff96ad6a55a6fe"></a>
### LATCH: PROPERTY

Property manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="98601cae1952978e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1a9fef7c18b3b955"></a>
### LATCH: ATTACH SHM

Shared memory segment의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="3d0f3625b2a2718e"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="533facdc82704347"></a>
### LATCH: BACKUP TBS

Tablespace backup manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="8c18c4f51de8dcb7"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="1b43d443bc00a7c1"></a>
### LATCH: DATAFILE COMPONENT

Datafile manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="ebd41089864c28cb"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="52396517548fc074"></a>
### LATCH: TABLESPACE

Tablespace의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="28f2f654e3940f9a"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="ad123f12a8ea78d3"></a>
### LATCH: BACKUP DATABASE

Database backup manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="65ccd0321fd710fd"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9697b57a3c6c0915"></a>
### LATCH: JOURNAL BUFFER

Journal buffer manager의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="411c438df49bdfa3"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="8ae94b972ac1651c"></a>
### LATCH: JOURNAL BUFFER ENTRY

Journal buffer entry의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="cf34db6936650576"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d749c7c19a90c77a"></a>
### LATCH: JOURNAL WRITE BUFFER

Journal write buffer의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="5143800b608d03e8"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="0521395169ee9458"></a>
### LATCH: LOCK ITEM

Lock item의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="541093d27d8139e1"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="880b9b52f624cbe1"></a>
### LATCH: RECORD HASH

Lock record hash의 bucket latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="23cca5f4d8ae72fc"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="2116e8de0a29c57c"></a>
### LATCH: SEQUENCE

Sequence object의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="1437951d02d498f6"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="56c654d1e28276e1"></a>
### LATCH: LOG FILE

Redo logfile의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="a28f4abdc9cb3a8d"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="a9a75b923caaab96"></a>
### LATCH: BUILD AGABLE SCN

Agable scn 구축을 위한 latch에 대기하는 시간이다.

**PARAMETER**

<a id="9e5fc89a05849b56"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="da4f7f5343f7bfa7"></a>
### LATCH: TRANSACTION TABLE

Transaction table의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="3eaf62b61d0ef141"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="413dda0e875764b6"></a>
### LATCH: SESSION LINK HASH

Session link hash의 bucket latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="968f76980911b798"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d66b4b6144757594"></a>
### LATCH: ALLOC XA CONTEXT

XA context를 할당하기 위해 latch에 대기하는 시간이다.

**PARAMETER**

<a id="efe109d7f3a9ca54"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="9fb8c7ef995833d6"></a>
### LATCH: SEQUENCE GLOBAL_X

Global sequence의 X latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="a3299da949f9abd4"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="925b080d6678eacd"></a>
### LATCH: SEQUENCE GLOBAL_Y

Global sequence의 Y latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="efc914b8a9c58981"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="d7ae8c4b64940997"></a>
### LATCH: TRANSACTION LOG FILE

Transaction logfile의 latch를 획득하기 위해 대기하는 시간이다.

**PARAMETER**

<a id="b3fa641fa88832e0"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="7d312554bb4d0982"></a>
### ASYNC RESPONSE

원격 노드로부터 비동기 명령어에 대한 응답을 기다리는 시간이다.  
Parameter: None

<a id="75dbe8f112c70bc5"></a>
### ASYNC TRANSACTION

원격 노드로부터 비동기 COMMIT 명령에 대한 응답을 기다리는 시간이다.  
Parameter: None

<a id="6abe06be6850bb9e"></a>
### LATCH: DISK BUFFER HASH BUCKET

Disk buffer cache를 위한 hash의 bucket latch에 대기하는 시간이다.

**PARAMETER**

<a id="1ddcd22e7243acc9"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="279f6b14a675ffb1"></a>
### WRITE: CHANGE TRACKING FILE

Change tracking file의 latch를 획득하기 위해 대기하는 시간이다.  
Parameter: None

<a id="5d4e829d2977fb05"></a>
### WAIT FREE BUFFER

Clean 상태의 disk buffer를 찾을 때까지 대기하는 시간이다.  
Parameter: None

<a id="434653f1b793185f"></a>
### GLOBAL SEQUENCE: LOCK AND QUERY

Global sequence 동기화에 대한 latch를 기다리는 시간이다.  
Parameter: None

<a id="c4f2a0004a2fcf36"></a>
### GLOBAL SEQUENCE: SYNC

Global sequence 동기화가 완료될 때까지 대기하는 시간이다.  
Parameter: None

<a id="a64bba7dd975ef5d"></a>
### LATCH: SEQUENCE GLOBAL NEXT

Sequence nextval에 대한 latch를 기다리는 시간이다.

**PARAMETER**

<a id="05af5671b71fb337"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="f74552137ded113d"></a>
### LATCH: BUFFER LRU LIST

Disk buffer의 LRU list에 대한 latch를 기다리는 시간이다.

**PARAMETER**

<a id="9dd051d3dde14917"></a>
| Parameter | 설명 |
| --- | --- |
| address | The address of the latch for which the process is waiting |
| tries | A count of the number of times the process tried to get the latch |

<a id="71307fa82eb0f36e"></a>
### WAIT DIRTY PAGE LIMIT

Disk buffer의 dirty page 수가 [BUFFER_DIRTY_PAGE_LIMIT](../part-02-administration-manual/10-server-property.md#141a470d8d601f73) 프로퍼티보다 작아질 때까지 대기하는 시간이다.   
Parameter: None

<a id="0bc75e3db885a35d"></a>
### WAIT BUFFER READ COMPLETE

Disk read 중인 disk buffer page에 접근할 때 read가 완료될 때까지 대기하는 시간이다.  
Parameter: None

<a id="0034d3344b49aeda"></a>
### WAIT ENV EVENT

Env event가 종료되기를 기다리는 시간이다.

**PARAMETER**

<a id="e6c061d7025c3b40"></a>
| Parameter | 설명 |
| --- | --- |
| event id | Event 아이디 |

<a id="d6eb3ed1ca26e6f0"></a>
### WAIT FREE APPEND EXTENT

Append insert를 위해 할당 받은 extent가 buffer에서 free 되기를 기다리는 시간이다.  
Parameter: None

---

[← 부록 B. Error Codes](appendix-02-부록-b-error-codes.md) · [전체 목차](../README.md) · [부록 D. Open Source License →](appendix-04-부록-d-open-source-license.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
