<a id="5debfb33dc9cdf97"></a>

# 10. Server Property

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/5debfb33dc9cdf97)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="f0fac7360e5d4996"></a>
## Server Property 정보

Property는 다음 SQL 구문으로 변경할 수 있다.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/16-sql-references.md#6e2b8dbddba3fab3) 
- [ALTER SESSION SET property_name](../part-03-sql-manual/16-sql-references.md#824f5c01b1aa6faa)

Property 정보는 다음 view로 확인할 수 있다.

- [V$PROPERTY](9-database-information.md#d29f6a2a0b856835)
- [V$SPROPERTY](9-database-information.md#f62651b0f5405fe9)

본 매뉴얼의 property 기본 정보 각 항에 대한 설명은 다음과 같다.

<a id="605cc22bdf3f67e9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | Property의 구분자이다. |
| 요약 | Property 요약 설명이다. |
| Data type | Property가 갖는 값의 데이터 타입이다. |
| 적용단계 | ALTER SYSTEM 또는 ALTER SESSION으로 변경할 수 있는 startup phase에 적용할 수 있다. * NONE: 적용할 수 있는 단계가 없다. (만약 변경 가능하지만 적용단계가 NONE인 경우에는 SCOPE = FILE 을 이용해야 한다.) |
| 변경가능 여부 | Property를 변경할 수 있는지 여부이다. * 해당 값이 TRUE일 경우, 변경 가능하다. * 해당 값이 FALSE일 경우, read-only만 가능하다. |
| ALTER SESSION 여부 | [ALTER SESSION SET property_name](../part-03-sql-manual/16-sql-references.md#824f5c01b1aa6faa) 구문으로 변경할 수 있는지 여부이다. |
| ALTER SYSTEM 여부 | [ALTER SYSTEM SET property_name](../part-03-sql-manual/16-sql-references.md#6e2b8dbddba3fab3) 구문으로 변경할 수 있는지 여부이다. * IMMEDIATE: 수행 즉시 모든 SESSION에 변경된 값이 반영된다. * DEFERRED: 수행된 이후에 접속한 SESSION에만 변경된 값이 반영된다. 이미 접속된 SESSION에는 반영되지 않는다. * FALSE: 운영 중에는 변경된 값이 반영되지 않으며 restart 이후에 변경된 값이 반영된다. SCOPE=FILE로만 수행할 수 있다. * NONE: 변경할 수 없다. |
| MIN | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최소값이다.  VARCHAR일 경우에는 N/A이다. |
| MAX | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최대값이다. VARCHAR일 경우에는 N/A이다. |
| 기본값 | 해당 property가 갖는 기본값이다. |

<a id="e86da35d4a1a8ed9"></a>
## AGING_INTERVAL

<a id="a6fb421cf06986a5"></a>
### 기본 정보

<a id="21c007c861a8eb2a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | AGING_INTERVAL |
| 요약 | aging interval time(ms) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| 기본값 | 10 |

<a id="156eaf138ce81586"></a>
### 설명

MVCC 기반의 database에서 이전 버전의 데이터를 지우는 ager thread가 처리할 job이 없을 때의 유휴 시간 (초)을 설정한다.

<a id="5c2c72ff4322cabe"></a>
## AGING_PLAN_INTERVAL

<a id="63178e19b69c5103"></a>
### 기본 정보

<a id="23747ea413f6f9f2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | AGING_PLAN_INTERVAL |
| 요약 | aging plan interval time(s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 31536000 |
| 기본값 | 0 |

<a id="905e3aa2428ec87e"></a>
### 설명

AGING_PLAN_INTERVAL 보다 오래된 SQL plan이 aging 대상이 된다.

<a id="3ee06b99755e80a9"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="19ea25e242cdcded"></a>
### 기본 정보

<a id="78bf530afe07398b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10 |
| 요약 | archive log directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE(ARCHIVELOG_DIR_1), TRUE(ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10) |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/archive_log |

<a id="f1456cb57ff679f2"></a>
### 설명

GOLDILOCKS 데이터베이스의 온라인 redo log file이 archive되는 디렉토리와 미디어 복구할 때 archive redo log file을 읽을 위치를 설정한다. 온라인 redo log file은 ARCHIVELOG_DIR_1에만 archive redo log file을 생성한다.

ARCHIVELOG_DIR_1은 시스템만 설정할 수 있고 ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10은 세션을 설정할 수 있다.

<a id="eadcea5c6ff71d43"></a>
## ARCHIVELOG_FILE

<a id="f6752dc7202e8010"></a>
### 기본 정보

<a id="8764a77601ced24b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ARCHIVELOG_FILE |
| 요약 | default archive log file |
| Data type | VARCHAR |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | archive |

<a id="03def94b8e8609cb"></a>
### 설명

온라인 redo log file을 archive 할 때 archive 디렉토리에 저장되는 목적 파일 이름의 prefix를 설정한다. Archive log file은 ARCHIVELOG_FILE에 설정된 prefix에 '_'와 파일 시퀀스, 'log' 확장자가 추가된 형태로 생성된다. 예를 들어, 파일 시퀀스가 0인 로그 파일은 'archive_0.log'으로 아카이빙된다.

<a id="f81e8737e1219d5a"></a>
## ARCHIVELOG_MODE

<a id="ce1575313ee3e236"></a>
### 기본 정보

<a id="3818a8ee264cc15f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ARCHIVELOG_MODE |
| 요약 | archive log mode(0:disable, 1:enable) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="5f7ceebbed6a3346"></a>
### 설명

Database를 생성할 때 적용되는 속성으로써 archive log mode를 다음 중 하나의 값으로 설정할 수 있다.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

Database가 생성된 후 운용되는 동안에는 archive log mode에 영향을 미치지 않고 mount 단계에서 ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}로 archive log mode를 변경할 수 있다.

<a id="7badcad52522ac6a"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="8bcf04c75b988cec"></a>
### 기본 정보

<a id="1602ee5ac143e8c4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BACKUP_DIR_1 ~ BACKUP_DIR_10 |
| 요약 | backup directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE(BACKUP_DIR_1), TRUE(BACKUP_DIR_2 ~ BACKUP_DIR_10) |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/backup |

<a id="93a0531701032638"></a>
### 설명

증분 백업이 수행될 때 백업 파일이 생성되고 증분 백업을 이용하여 파일을 복원할 때 백업 파일이 읽혀질 디렉토리를 설정한다. 증분 백업은 BACKUP_DIR_1에 설정된 디렉토리에만 생성된다.

BACKUP_DIR_1은 시스템만 설정할 수 있고 BACKUP_DIR_2 ~ BACKUP_DIR_10은 세션을 설정할 수 있다.

<a id="f8b12a32c20ecd5a"></a>
## BLOCK_READ_COUNT

<a id="4d71e7d106ce1ba2"></a>
### 기본 정보

<a id="571024f513944913"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BLOCK_READ_COUNT |
| 요약 | value count for a block read |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 20 |

<a id="68333eddeb1992e9"></a>
### 설명

SQL을 처리할 때 row의 묶음 단위인 BLOCK_READ_COUNT 단위로 row를 읽어 연산을 처리한다.   
BLOCK_READ_COUNT는 연산을 수행할 때 한 번에 처리할 row의 개수를 의미하며 SQL 질의 처리에 참여하는 실행 노드간의 pipe-lining 처리의 기본 단위이다.

BLOCK_READ_COUNT 값이 크면 연산 처리 성능은 향상되지만 메모리 자원을 많이 사용한다. 따라서 10 ~ 100 사이의 값을 권장한다. 그 이상의 값을 사용하는 경우 자원 사용량은 비례하여 증가하지만 성능은 비례하여 향상되지 않는다.

<a id="56b23998675161c0"></a>
## BULK_IO_PAGE_COUNT

<a id="0bec7edbd280d4e1"></a>
### 기본 정보

<a id="78ea050ec5d9f886"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BULK_IO_PAGE_COUNT |
| 요약 | page count for bulk IO operation |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 128 |
| MAX | 131072 |
| 기본값 | 3840 |

<a id="71f8c214edd546f3"></a>
### 설명

서버를 재시작할 때 데이터 파일에 IO READ가 발생할 경우나 데이터 파일을 생성할 때 IO WRITE가 발생할 경우에 사용된다.

서버를 재시작하거나 데이터 파일을 생성할 때 BULK_IO_PAGE_COUNT * 8192 크기만큼 heap 메모리가 할당되며 세션의 PRIVATE_STATIC_AREA_SIZE가 그 크기보다 작을 경우 메모리 부족 에러가 발생할 수 있다. 이 경우에는 PRIVATE_STATIC_AREA_SIZE를 늘려주어야 한다.

<a id="8bdc8a4b681592f4"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="edec5aebd2cc5e0d"></a>
### 기본 정보

<a id="ed5b4435649b3932"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_HOT_POLICY_INTERVAL |
| 요약 | cdispatcher dequeue interval for busy waiting ( micro second ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000 (1day) |
| 기본값 | 100000 |

<a id="17a231d0a8ae64cc"></a>
### 설명

cdispatcher에서 dequeue 할 때 busy waiting하는 시간이다. Micro second 단위이며 이 값을 크게 하면 CPU를 많이 사용하는 대신 사용자 응답 시간 (latency)은 줄어든다.

<a id="a15a3003ab8e8f44"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="780380fe1bfc1cea"></a>
### 기본 정보

<a id="5cc95c5c1c450a5f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_SOCKET_BUFFER_SIZE |
| 요약 | cdispatcher socket buffer(sender, receiver) size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 64 |
| MAX | 100 Mega |
| 기본값 | 32768 |

<a id="5ca5e67aa4c2eb83"></a>
### 설명

cdispatcher socket buffer (송신자, 수신자)의 크기이다.

<a id="2c766d6cdcf2dcdd"></a>
## CDISPATCHER_SYNC_THREADS

<a id="7494aaad133bc73b"></a>
### 기본 정보

<a id="ff66467b1cbc50bf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_SYNC_THREADS |
| 요약 | cdispatcher sync thread count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 32 |
| 기본값 | 1 |

<a id="516624c399acfa1b"></a>
### 설명

cdispatcher sync thread의 개수이다.

<a id="404ec844f8d33858"></a>
## CDISPATCHER_THREADS

<a id="784f96bf433631d6"></a>
### 기본 정보

<a id="ad3308c45d26bd33"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_THREADS |
| 요약 | cdispatcher sender, receiver thread count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 32 |
| 기본값 | 1 |

<a id="d6ec2b1de48df792"></a>
### 설명

cdispatcher 송수신자의 thread 개수이다.

<a id="ca2b51aaf579786d"></a>
## CHARACTER_SET

<a id="4aec60c716d9de2e"></a>
### 기본 정보

<a id="abe6aeff209a355f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHARACTER_SET |
| 요약 | character set |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | UTF8 |

<a id="43f072f83724eba0"></a>
### 설명

Database의 character set이다.  
Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값을 설정할 수 있다.

**Character set**

<a id="7d701fbb4b01b9dc"></a>
| Character set | 설명 |
| --- | --- |
| SQL_ASCII | ASCII standard |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standard |

<a id="aac7ec44c5e984a8"></a>
## CHAR_LENGTH_UNITS

<a id="bcb891468f99e7af"></a>
### 기본 정보

<a id="57fecc28c0bee404"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHAR_LENGTH_UNITS |
| 요약 | char length units |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | OCTETS |

<a id="593858ba5bf3ddff"></a>
### 설명

CHAR, VARCHAR와 같은 문자열 column을 정의하면서 다음과 같이 char length unit을 생략할 경우에 사용되는 char length units 값이다.

```
CREATE TABLE t1 
(
   id   CHAR( 10 OCTETS ),          
   name VARCHAR( 128 CHARACTERS ),  
   addr VARCHAR( 128 )            
);
```

- id CHAR( 10 OCTETS )는 10 bytes를 의미한다. 
- name VARCHAR( 128 CHARACTERS )는 128 글자를 의미한다.
- addr VARCHAR( 128 )는 char length unit이 생략된 경우에 참조하는 프로퍼티 값이다.

Database 생성시 적용되는 속성으로 OCTETS나 CHARACTERS 중 하나의 값을 설정할 수 있다. OCTETS는 byte 수를 의미하고 CHARACTERS는 문자의 개수를 의미한다.

> SQL 표준은 기본값을 CHARACTERS로 정의하고 있으며 타 DBMS 들의 char length unit 기본값은 다음과 같다.
> 
> - Oracle과 DB2는 OCTETS를 사용한다. 
> - MS-SQL, MySQL, PostgreSQL는 CHARACTERS를 사용한다.
> 

<a id="4f047051e0dd9e21"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="1cf7cd728b88d1f7"></a>
### 기본 정보

<a id="aa2cc1e87b3a965f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHECK_DEDICATE_CONNECTION_INTERVAL |
| 요약 | check dedicate socket |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000 |
| 기본값 | 1000 |

<a id="fe33614aa67a9376"></a>
### 설명

C/S dedicate 환경에서 client가 접속을 강제로 종료했을 경우, 이를 검사하는 주기이다. Dedicate server (gserver)가 socket을 확인하여 끊어졌으면 종료한다. 기본값은 1,000 millisecond (1초)이다.

<a id="5e62c6e4d5c861a0"></a>
## CLIENT_MAX_COUNT

<a id="cfb84b85dc3a92db"></a>
### 기본 정보

<a id="cb957363a3752800"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLIENT_MAX_COUNT |
| 요약 | Maximum session count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 12 |
| MAX | 65535 |
| 기본값 | 128 |

<a id="af26b4637c3ee1d7"></a>
### 설명

접속할 수 있는 세션의 최대 개수를 설정한다.

<a id="094cd5213b50d000"></a>
## CLIENT_NUMA_POLICY

<a id="bff8dac1216746d5"></a>
### 기본 정보

<a id="fda544a8de776ecb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLIENT_NUMA_POLICY |
| 요약 | client numa policy( 0: by modualar, 1: by statistics , 2: by manunal ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="71c34f027121777d"></a>
### 설명

Client 프로세스들을 NUMA 노드들에 분배하기 위한 정책을 결정한다. CLIENT_NUMA_POLICY 프로퍼티는 NUMA 프로퍼티가 on 되어있을 때 동작한다.

- 0: 세션 ID를 모듈러 (modular)해서 연결할 NUMA 노드를 결정한다.
- 1: 통계정보를 바탕으로 가장 조금 연결되어 있는 NUMA 노드에 우선적으로 연결한다.
- 2: C/S client는 TCP_CLIENT_NUMA_NODE 프로퍼티에 의해서 결정되고, D/A client는 DA_CLIENT_ NUMA_NODE 프로퍼티에 의해서 결정된다.

<a id="7fead8108add95df"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="58ff36e7d1ba5d3c"></a>
### 기본 정보

<a id="df78b37e5ce83061"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLOSE_PSM_CHILD_STMTS |
| 요약 | close child statements of PSM at the end of each execution |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="2cdf79941e6e3f71"></a>
### 설명

매 실행 마지막에 PSM의 child 구문을 close 한다.

<a id="22c4439ee496a28d"></a>
## CLUSTER_ASYNC_COMMIT

<a id="9030f55bb945f19a"></a>
### 기본 정보

<a id="dd60fa4b065e6750"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_ASYNC_COMMIT |
| 요약 | enable asynchronous commit in cluster system |
| Data type | BOOLEAN |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="34f6c2e64de0b77c"></a>
### 설명

Cluster system에서 내부적으로 commit protocol을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 commit을 비동기 처리하기 때문에 일시적으로 노드별 consistency가 깨어질 수 있다. 반면에 이 프로퍼티가 꺼져 있으면 commit 할 때마다 동기화하기 때문에 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="b000521e6fe631c8"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="caf263e7894e1e34"></a>
### 기본 정보

<a id="4cfd250d04e1bae3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_ASYNC_REPLICATION |
| 요약 | enable asynchronous replication |
| Data type | BOOLEAN |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="a6b95aa2ea13ffb8"></a>
### 설명

Cluster system에서 내부적으로 replication을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 데이터를 비동기적으로 반영하기 때문에 어떤 노드에 접속하여 작업을 수행하는지에 따라 응답시간이 차이난다. 반면에 이 프로퍼티가 꺼져 있으면 데이터를 변경할 때마다 동기화하기 때문에 전체 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="6c70261eec051c55"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="cc27c370eda0160f"></a>
### 기본 정보

<a id="8e493c7b8fd7d226"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_CM_BUFFER_COUNT |
| 요약 | communication buffer count for cluster |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 256 |
| 기본값 | 4 |

<a id="6af7af99c1b48ef6"></a>
### 설명

Cluster의 communication buffer 개수이다.

<a id="39026c83ded7cbe4"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="57a11b1323c8234f"></a>
### 기본 정보

<a id="5a619a41743103c3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_CM_BUFFER_SIZE |
| 요약 | communication buffer size for cluster |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| 기본값 | 10 Mega |

<a id="95e1a2a05a554e85"></a>
### 설명

Cluster의 communication buffer 크기이다.

<a id="ebfcd97f92c3fc20"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="0fa3f5c11564f3be"></a>
### 기본 정보

<a id="214405a952d59ab3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_CM_READ_BUFFER_SIZE |
| 요약 | communication read block size |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8192 |
| MAX | 10485760 |
| 기본값 | 65536 |

<a id="9ff9c1f25ed61c5c"></a>
### 설명

Communication read block의 크기이다.

<a id="4cdd0947a62f65c2"></a>
## CLUSTER_COMMIT_SLAVES

<a id="f70abedbd14d9d14"></a>
### 기본 정보

<a id="b0940b90fae25fa5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_COMMIT_SLAVES |
| 요약 | number of commit slaves |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 8 |
| 기본값 | 1 |

<a id="98165741fb9d5247"></a>
### 설명

Commit slave의 번호이다.

<a id="ca313faae2fdecc7"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="2aa4eb5d99d38786"></a>
### 기본 정보

<a id="dd61907da33aa08a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_COMMIT_STREAM_ISOLATION |
| 요약 | isolate cluster dispatcher stream for commit protocol |
| Data type | BOOLEAN |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="c352b05c9ecd4939"></a>
### 설명

Cluster system에서 내부적으로 commit 처리 흐름을 다른 protocol 처리와 분리하여 수행할 것인지 여부를 설정한다. 시스템 환경에 따라 commit 처리를 분리할 경우 성능이 향상될 수 있다.

<a id="271c3ab80eb29de1"></a>
## CLUSTER_CONNECTION

<a id="6c99ed533b4d809b"></a>
### 기본 정보

<a id="2ce9892549e4ad68"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_CONNECTION |
| 요약 | connection mode for cluster ( socket:0, rdma:1 ) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0: socket |

<a id="fe3a1f6b368e951b"></a>
### 설명

Cluster의 connection mode이다. (socket: 0, rdma:1)

<a id="1c820923ac8bd99b"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="533477ec66b85c7c"></a>
### 기본 정보

<a id="168184a3361e2d79"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_CONNECTION_TIMEOUT_SEC |
| 요약 | connection timeout for cluster |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400 |
| 기본값 | 5 |

<a id="6a9bef320d0eef1e"></a>
### 설명

Cluster의 connection timeout 이다.

<a id="ef74a626bebc4261"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="19ae262df422b199"></a>
### 기본 정보

<a id="04ca642254c564ba"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_DATA_SYNC_SERVERS |
| 요약 | count of data synchronization server |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 3 |

<a id="4d58d57d925a473c"></a>
### 설명

Data synchronization server의 개수이다.

<a id="09bebc11b93514bf"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="a47e1e9f31b43731"></a>
### 기본 정보

<a id="64f52a36fada8974"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_DISPATCHER_IN_QUEUE_SIZE |
| 요약 | in-queue size for cluster dispatcher |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1024 |
| MAX | 32768 |
| 기본값 | 1024 |

<a id="95cd222005438976"></a>
### 설명

Cluster dispatcher in-queue의 크기이다.

<a id="4409d86a484d3b05"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="330a5c1e5d749beb"></a>
### 기본 정보

<a id="7ed147ffac3b48d4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_DISPATCHER_NUMA_STREAM_MAP |
| 요약 | numa stream map for cluster dispatcher |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 'x': no binding |

<a id="ebc4b1b6aaf18324"></a>
### 설명

Cluster 디스패처들이 연결될 NUMA 노드를 결정한다. CLUSTER_DISPATCHER_NUMA_STREAM_MAP 프로퍼티는 NUMA 프로퍼티가 on되어 있을 때 동작한다.

> 만약 CLUSTER_COMMIT_STREAM_ISOLATION 프로퍼티가 on 되어 있다면 0번 스트림은 commit stream의 NUMA 노드로 설정된다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고 1번 스트림은 NUMA 노드 1번에 연결하며 2번 스트림은 NUMA 노드 2번에 연결한다.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="743f1db417c4fbc4"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="3f4c1a3dd2c21df3"></a>
### 기본 정보

<a id="586a721e0decb2d5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_DISPATCHER_OUT_QUEUE_SIZE |
| 요약 | out-queue size for cluster dispatcher |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1024 |
| MAX | 32768 |
| 기본값 | 1024 |

<a id="f776e838150bc58e"></a>
### 설명

Cluster dispatcher의 out-queue 크기이다.

<a id="544b8021dcfbc62a"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="d3fa7dd86794f33e"></a>
### 기본 정보

<a id="a04241e4956b8942"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_HEARTBEAT_INTERVAL |
| 요약 | interval seconds for health checking of cluster |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400 |
| 기본값 | 3 |

<a id="0c29ed40df5eba81"></a>
### 설명

Cluster의 상태를 점검하는 주기 (초)이다. 0은 비활성화 상태를 의미한다.

<a id="3cf27aa32b03c4ae"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="f836a050c02e1fbb"></a>
### 기본 정보

<a id="3985d6a745ee16eb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_HEARTBEAT_RETRY_COUNT |
| 요약 | retry count for health checking of cluster |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 5 |

<a id="185c4a7081821fa5"></a>
### 설명

Cluster 상태 점검을 다시 시도하는 횟수이다.

<a id="5d0249ded5dfae12"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="675db70ce9726b10"></a>
### 기본 정보

<a id="e8b2669eb3ca0754"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_IGNORE_INACTIVE_MEMBER |
| 요약 | ignore in-active member for cluster |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="08f2cf5849751383"></a>
### 설명

Cluster의 in-active 멤버를 무시한다.

<a id="44a5b0687dccf2b6"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="b1fc646b9d20ebe1"></a>
### 기본 정보

<a id="02fd6ca6b126c4b1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_MAX_PACKET_SIZE |
| 요약 | maximum packet size for cluster session |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| 기본값 | 100 Mega |

<a id="1a961fcb651a3b41"></a>
### 설명

원격 프로토콜이 한 번에 전송할 수 있는 패킷의 최대 크기를 결정한다. 원격으로 전송해야 하는 column의 크기가 CLUSTER_MAX_PACKET_SIZE 프로퍼티 크기를 초과할 경우, 해당 프로퍼티를 column 크기보다 크게 설정해야 한다.

<a id="94c23ea106d75e0f"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="cff4c971d5e0a74d"></a>
### 기본 정보

<a id="742c01368b8ff5bf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_MAX_PAYLOAD_SIZE |
| 요약 | maximum packet payload size for cluster session (byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 524288 |
| MAX | 33554432 |
| 기본값 | 524288 |

<a id="dabec854b5fb53f4"></a>
### 설명

원격으로 전송되는 클러스터 패킷은 여러 개의 piece로 나뉘어 전달될 수 있는데 CLUSTER_MAX_PAYLOAD_SIZE 프로퍼티는 하나의 piece에 저장할 수 있는 데이터의 최대 크기를 설정한다.

<a id="7eadd0cffd31cafe"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="0067a37ecb7431c7"></a>
### 기본 정보

<a id="01589c91ca293607"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PACKET_ALLOCATION_TIMEOUT |
| 요약 | a time limit (sec) for how long statemets will wait to allocate packet memory |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| 기본값 | 3 |

<a id="904f093e68930437"></a>
### 설명

Cluster 패킷 구성에 필요한 메모리를 할당할 때 기다릴 수 있는 최대 시간 (초)을 설정한다.

<a id="d21aab50c1233764"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="b9c23310dc9274d8"></a>
### 기본 정보

<a id="adedc68467a96058"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT |
| 요약 | a time limit of session fatal policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="0f32922886baf7b1"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Session을 종료시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, failover 시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#c153389143e691b5) property를 사용하여 제한 시간을 설정한다.

<a id="c153389143e691b5"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="1f4ca7784957b957"></a>
### 기본 정보

<a id="69fd2381b90e9887"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT |
| 요약 | a time limit of failover policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="8850c5f08352bd6b"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Failover 시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, session을 종료시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#d21aab50c1233764) property를 사용하여 제한 시간을 설정한다.

<a id="031351e864ea2adb"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="be23e41f7f4e77bf"></a>
### 기본 정보

<a id="02308871c4979990"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |
| 요약 | response queue size for cluster server |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 30 |
| MAX | 32768 |
| 기본값 | 30 |

<a id="e987f20c36fabb3e"></a>
### 설명

원격 서버로부터 응답을 받기 위한 queue의 최대 크기를 설정한다.

<a id="dfa017b50ad92f75"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="f45ec5ad31adc997"></a>
### 기본 정보

<a id="5b99cdcee1aa18f4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY |
| 요약 | split brain resolution policy for cluster system |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="244faed03d1d0fda"></a>
### 설명

Cluster system에서 split-brain 상황을 해결하기 위한 정책을 설정한다. 1 이상의 값으로 설정할 경우 해결 방안을 locator에게 질의한다.

> Locator에게 한 질의에 timeout이 발생하면 CLUSTER_SPLIT_BRAIN_RETRY_COUNT만큼 질의를 시도한다. 재시도에 실패하면 속성값이 1인 경우에는 failover를 강제로 진행하고 속성값이 2인 경우에는 fatal 종료한다.

<a id="1881fd494bdea437"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="1e1ff18e51d6e512"></a>
### 기본 정보

<a id="d84e415d0b13c9eb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_SPLIT_BRAIN_RETRY_COUNT |
| 요약 | retry count for split brain resolution policy(1 ~ 65536) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 4 |

<a id="e38d0b1def08f005"></a>
### 설명

Cluster system에서 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 이상으로 설정되었을 경우에 사용된다. Locator에게 보낸 질의에 응답이 없을 경우, 질의를 다시 시도하는 횟수를 설정한다.

<a id="fe1b65e3c4b9bae7"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="3cc055d547b11780"></a>
### 기본 정보

<a id="3af32f0dc2e8a9d3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | COMMITTER_HOT_POLICY_INTERVAL |
| 요약 | committer deque interval for busy waiting |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000 (1 day) |
| 기본값 | 0 (cold 정책) |

<a id="0c1de25108edc864"></a>
### 설명

Commit cserver가 commit protocol 메시지를 읽기 위해 deque 할 때 busy waiting의 기준 시간 간격을 설정한다. 만약 1000000 (1초)로 설정할 경우, 이전 deque에 성공한 이후 다시 deque를 시도할 때까지 1 초를 경과하지 않았다면 deque에서의 대기시간 (timeout)을 0으로 설정하여 busy waiting 한다.

<a id="b06f583584d38597"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="06c4589982b3c943"></a>
### 기본 정보

<a id="b3fb6d9f722e20c8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CONTROL_FILE_0 |
| 요약 | control file name |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/wal/control_0.ctl |

<a id="4fbcb5bbd1ac9f3c"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화해야 하는데 이 때 각 control file이 저장될 디렉토리와 파일 이름을 설정한다.

<a id="dc70609db9a1d50d"></a>
## CONTROL_FILE_COUNT

<a id="dbafd62977a8c2b2"></a>
### 기본 정보

<a id="09a2b99f27ca6987"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CONTROL_FILE_COUNT |
| 요약 | control file count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 2 |
| MAX | 8 |
| 기본값 | 2 |

<a id="746c2e33f07eac66"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화한다. CONTROL_FILE_COUNT는 control file의 다중화 개수를 설정하며 최소 두 개에서 최대 여덟 개까지 다중화할 수 있다.

<a id="5ffb51e16678a4a5"></a>
## CONTROL_FILE_TEMP_NAME

<a id="a16d11e545458af7"></a>
### 기본 정보

<a id="84139714fbcfda71"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CONTROL_FILE_TEMP_NAME |
| 요약 | temporary file name for control file |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/backup/control.tmp |

<a id="a2e772251265bd3c"></a>
### 설명

Database를 운용하는 중에 control file은 수시로 변경되고 필요할 경우 임시로 복사본을 만들 수도 있다. CONTROL_FILE_TEMP_NAME은 control file이 임시로 저장되는 디렉토리와 파일 이름을 설정한다.

<a id="aa390a27bb935d1c"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="bd8edcb70b4e82de"></a>
### 기본 정보

<a id="079288b77dd7db10"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | COORDINATOR_COMMIT_WRITE_MODE |
| 요약 | coordinator commit write mode(0:disable, 1:wait mode) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="4e21cbd940556718"></a>
### 설명

조정자 (coordinator)에 적용되는 commit write mode 이다. 만약 TRANSACTION_COMMIT_WRITE_MODE가 "no wait"이고 해당 프로퍼티가 "wait" 인 경우라면 조정자 노드는 "wait"으로 동작하고 그 외 노드들은 "no wait"으로 동작한다.

<a id="7e7e4f38d89fd0f8"></a>
## CSERVERS

<a id="6e03e24ca9a38242"></a>
### 기본 정보

<a id="798ee0cfef1d346a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CSERVERS |
| 요약 | number of cserver processes |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 512 |
| 기본값 | 10 |

<a id="58c5feb9382828b1"></a>
### 설명

cserver 프로세스의 번호이다.

<a id="24828e1296e52045"></a>
## DATABASE_ACCESS_MODE

<a id="d2e8209a41f80b93"></a>
### 기본 정보

<a id="b2fdc6fe4aad0ce6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DATABASE_ACCESS_MODE |
| 요약 | database access mode ( 0: read only, 1: read write ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 1 |

<a id="e980ceb9a0140f2d"></a>
### 설명

Database를 시작할 때 접근 모드를 설정한다.

- 0: Database 조회만 할 수 있고 삽입/ 갱신/ 삭제는 불가능하다.
- 1: Database를 조회/ 삽입/ 삭제/ 갱신할 수 있다.

<a id="88887e6cab834647"></a>
## DATABASE_INSTANCE_NAME

<a id="36b6a379c6cef140"></a>
### 기본 정보

<a id="f81949746f3d2046"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DATABASE_INSTANCE_NAME |
| 요약 | database instance name |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | GOLDILOCKS |

<a id="f8bfca5aa3794631"></a>
### 설명

데이터베이스의 instance 이름이다.

<a id="60bf37c12c36968f"></a>
## DATA_STORE_MODE

<a id="b75a5fbcd41f72bc"></a>
### 기본 정보

<a id="a544fd978c29682b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DATA_STORE_MODE |
| 요약 | Data store mode(cds:1,tds:2) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 2 |
| 기본값 | 2 |

<a id="784b818a2591594c"></a>
### 설명

Database의 저장 방식을 설정한다.

- 1: CDS 모드는 다중 사용자에 대한 동시성은 지원하지만 영속성은 보장하지 않는다. 즉, data 삽입/ 삭제/ 갱신을 비롯하여 database를 변경하는 모든 연산에 대한 로그를 기록하지 않기 때문에 장애가 발생할 경우 복구할 수도 없다.
- 2: TDS 모드는 다중 사용자에 대한 동시성 및 로그를 이용한 영속성을 보장한다.

<a id="ab7511cf1a834931"></a>
## DA_CLIENT_NUMA_NODE

<a id="c2b8f9d59491c784"></a>
### 기본 정보

<a id="4b2226e44b67b278"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DA_CLIENT_NUMA_NODE |
| 요약 | numa node for DA clients |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | -1 |
| MAX | 63 |
| 기본값 | -1 |

<a id="4cf0772eddcd4c05"></a>
### 설명

Direct Access (D/A) 세션이 바인드 될 NUMA 노드 ID를 설정한다. DA_CLIENT_NUMA_NODE는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="d35729c9ebe5c65b"></a>
## DDL_AUTOCOMMIT

<a id="40771607061866df"></a>
### 기본 정보

<a id="171a3faa2dde49b8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DDL_AUTOCOMMIT |
| 요약 | DDL auto commit |
| Data type | BOOL |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="c2f31057b840e44f"></a>
### 설명

Autocommit이 적용되지 않는 DDL에 대한 autocommit 여부를 설정한다. 예를 들어, table의 생성과 변경에는 autocommit이 적용되지 않기 때문에 DDL_AUTOCOMMIT이 '0'인 경우 rollback을 수행하여 table 생성과 변경을 철회할 수 있다. 이에 반해 DDL_AUTOCOMMIT을 '1'로 설정하면 autocommit이 적용되지 않는 DDL들이 즉시 commit 된다.

<a id="68a23f1cee137963"></a>
## DDL_LOCK_TIMEOUT

<a id="7d7969f7ee524860"></a>
### 기본 정보

<a id="d3502699bf0d2888"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DDL_LOCK_TIMEOUT |
| 요약 | a time limit (sec) for how long DDL statemets will wait |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="906549ec12052e9c"></a>
### 설명

동일한 객체에 대해 동시에 DDL이 발생했을 때의 lock 대기 시간을 의미한다.  
기본값은 0 sec로써 DDL이 발생했을 때 lock을 기다리지 않는다.

다음과 같이 테이블에 대한 구조 변경 작업이 동시에 발생할 경우 다른 트랜잭션이 종료될 때까지 대기하지 않고 DDL_LOCK_TIMEOUT 시간만큼만 대기한다.

- Transaction A

```
ALTER TABLE t1 ADD COLUMN ( new_column NUMBER );
```

- Transaction B

```
TRUNCATE TABLE t1;
```

대기 시간이 DDL_LOCK_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> TRUNCATE TABLE t1;

ERR-HYT00(14026): resource busy or timeout expired
```

<a id="d2b66b992e0706c3"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="2596f0df5d38ab86"></a>
### 기본 정보

<a id="4fd5e92763834aac"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION |
| 요약 | specifies whether or not create global secondary index at table creation |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="78ec0e69d7f6dc0b"></a>
### 설명

Cluster system에서 테이블을 생성할 때 global secondary index를 생성할지 여부를 설정한다. Global secondary index를 생성하지 않은 테이블에 대한 non-deterministic 질의는 실패한다. NO로 설정한 상태에서 테이블을 생성한 후에 별도로 global secondary index를 생성할 수도 있다.

<a id="05051866db9894e2"></a>
## DEFAULT_INDEX_LOGGING

<a id="7174adfe63958e88"></a>
### 기본 정보

<a id="df223363df45e584"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_INDEX_LOGGING |
| 요약 | default logging flag of indexes |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="e0ad39e91fa56720"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 LOGGING 속성을 지정하지 않은 경우, LOGGING 속성은 DEFAULT_INDEX_LOGGING 프로퍼티 값으로 설정된다. 만약 인덱스가 LOGGING 테이블스페이스에 생성되면 반드시 LOGGING 속성이 설정되어야 한다

<a id="33f195ae745819d1"></a>
## DEFAULT_INDEX_PCTFREE

<a id="fece2b6bab859b75"></a>
### 기본 정보

<a id="750663ae2024faa9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_INDEX_PCTFREE |
| 요약 | default pctfree value of indexes ( % ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| 기본값 | 0 |

<a id="78222cbce0451338"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_INDEX_PCTFREE 프로퍼티 값으로 설정된다.

<a id="2c8d025479f60bf7"></a>
## DEFAULT_INITRANS

<a id="6d4193c197e013fb"></a>
### 기본 정보

<a id="f5a86d074adca6e1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_INITRANS |
| 요약 | default initrans value of tables |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 32 |
| 기본값 | 4 |

<a id="233d6b78c8b1b565"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 INITRANS 구문을 지정하지 않은 경우 INITRANS는 DEFAULT_INITRANS 프로퍼티 값으로 설정된다.

<a id="0522f24386679c10"></a>
## DEFAULT_MAXTRANS

<a id="e363a851ffa27540"></a>
### 기본 정보

<a id="d57e65d2c4b78ec7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_MAXTRANS |
| 요약 | default maxtrans value of tables |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 32 |
| 기본값 | 8 |

<a id="1521a4c7f77c7399"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 MAXTRANS 구문을 지정하지 않은 경우 MAXTRANS는 DEFAULT_MAXTRANS 프로퍼티 값으로 설정된다.

<a id="d97dd53835582379"></a>
## DEFAULT_PCTFREE

<a id="f589e29f3614a3b7"></a>
### 기본 정보

<a id="b3305ced4a42821d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_PCTFREE |
| 요약 | default pctfree value of tables ( % ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| 기본값 | 10 |

<a id="c93dae57110c2eaf"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_PCTFREE 프로퍼티 값으로 설정된다.

<a id="e5dc822e991ed2d2"></a>
## DEFAULT_PCTUSED

<a id="dd3a6e366cbdcfa1"></a>
### 기본 정보

<a id="0c3195bfbeb42451"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_PCTUSED |
| 요약 | default pctused value of tables ( % ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 99 |
| 기본값 | 60 |

<a id="5fe06f726e201313"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTUSED 구문을 지정하지 않은 경우 PCTUSED는 DEFAULT_PCTUSED 프로퍼티 값으로 설정된다.

<a id="015b2f80200e2115"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="1644c00109b73be3"></a>
### 기본 정보

<a id="5f5ddf042d69213f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_REMOVAL_BACKUP_FILE |
| 요약 | default removal flag of incremental backup files |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="c91d6ff8e71cae2e"></a>
### 설명

백업 목록을 삭제할 때 백업 파일을 삭제할지 여부를 지정한다.

<a id="c994aa2a07fe9264"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="8fcacd80b967ac0e"></a>
### 기본 정보

<a id="269779fbab130923"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST |
| 요약 | default removal flag of obsolete incremental backup lists |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="f51108a8a1e680b3"></a>
### 설명

INCREMENTAL BACKUP을 수행할 때 obsolete 된 이전 백업 목록의 삭제 여부를 설정한다.

<a id="df566c03eeccec67"></a>
## DEFAULT_SHARDING

<a id="ef5f43d2e95b009b"></a>
### 기본 정보

<a id="fdcf08c190a7138f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_SHARDING |
| 요약 | default sharding strategy (0: cloned, 1: hash sharding) |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="4a5799d96fcb9335"></a>
### 설명

테이블을 생성할 때 sharding strategy를 정의하지 않을 경우 사용할 기본 sharding strategy를 설정한다.

다음은 CREATE TABLE 구문을 수행하는 예이다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
);
```

DEFAULT_SHARDING 값이 0 (cloned) 인 경우, 테이블을 다음과 같은 개념의 cloned table로 생성한다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
)
CLONED
AT CLUSTER WIDE
;
```

DEFAULT_SHARDING 값이 1 (hash sharding) 인 경우, 테이블을 다음과 같은 개념의 hash-sharded table 로 생성한다.

```
CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128)
)
SHARDING BY HASH (id)
    SHARD COUNT 24
    AT CLUSTER WIDE
;
```

DEFAULT_SHARDING 값이 1 (hash sharding) 이고 &lt;table sharding strategy&gt;를 기술하지 않은 경우, 다음과 같은 순서로 hash sharding key를 결정한다.

1. PRIMARY KEY 제약 조건을 정의한 경우, primary key를 sharding key로 사용한다.

- 원본

```
CREATE TABLE t1 ( id INTEGER PRIMARY KEY, name VARCHAR(128) );
```

- 해석

```
CREATE TABLE t1 ( id INTEGER PRIMARY KEY, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

2. UNIQUE 제약 조건을 정의한 경우, 첫 번째로 기술한 UNIQUE 제약 조건을 sharding key로 사용한다.

- 원본

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) UNIQUE );
```

- 해석

```
CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) UNIQUE )
    SHARDING BY HASH(name)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

3. Key 제약 조건이 없는 경우, 다음과 같은 data type이 아닌 첫 번째 column을 sharding key로 사용한다.
** 제외되는 data type: LONG VARCHAR, LONG VARBINARY, BOOLEAN

- 원본

```
CREATE TABLE t1 ( is_man BOOLEAN, id INTEGER, name VARCHAR(128) );
```

- 해석

```
CREATE TABLE t1 ( is_man BOOLEAN, id INTEGER, name VARCHAR(128) )
    SHARDING BY HASH(id)
    SHARD COUNT 24
    AT CLUSTER WIDE;
```

<a id="9785cdcccce1120f"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="e7a6692f0bd4681d"></a>
### 기본 정보

<a id="61d1def32b8fa3e4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISABLE_DDL_CDC_GIVEUP |
| 요약 | disable DDL which caused CDC give-up |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="7413902552430c9e"></a>
### 설명

CDC의 give up에 영향을 미치는 supplemental log 대상 테이블에 대한 DDL 수행을 금지한다.  
관련 DDL은 [DDL 구문에 따른 Give-up 발생 및 절차에 따른 허용 여부](../part-07-replication/44-cyclone.md#cc3ac8f41cae7c0b)를 참조한다.

<a id="361849a3696f934a"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="4877f3a0af031436"></a>
### 기본 정보

<a id="c42663ee6aa40c57"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISABLE_UPDATE_PK_CDC_GIVEUP |
| 요약 | disable UPDATE primary key which caused CDC give-up |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="ce0a50d8538fd153"></a>
### 설명

CDC give up을 유발한 UPDATE primary key를 비활성화 한다.

<a id="e3faa5d2e64c442e"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="0bc478b5412ecbac"></a>
### 기본 정보

<a id="e38bd5f735366439"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISALLOWED_PROTOCOL_TARGETTYPE |
| 요약 | disallowed TARGETTYPE protocol |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="5204eff3846f9c8a"></a>
### 설명

TARGETTYPE protocol을 허용하지 않는다.

<a id="e1aa9a9011a744c8"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="150d2ec002a79dec"></a>
### 기본 정보

<a id="44d55f6f0f79e43d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL |
| 요약 | disallowed TARGETTYPE_WITH_ALL protocol |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="2d1bdb5a3e9f3aad"></a>
### 설명

TARGETTYPE_WITH_ALL protocol을 허용하지 않는다.

<a id="0df0e63fdbeba90f"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="923878dfbeec23bd"></a>
### 기본 정보

<a id="c240bea4d1ddd572"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME |
| 요약 | disallowed TARGETTYPE_WITH_NAME protocol |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="9ae6f06c9601dc91"></a>
### 설명

TARGETTYPE_WITH_NAME protocol을 허용하지 않는다.

<a id="2b8e9fc41ad20eba"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="aa4fac3b1af3a092"></a>
### 기본 정보

<a id="edfda69177a4496d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_CM_BUFFER_SIZE |
| 요약 | communication buffer size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 10485760 |
| MAX | 34359738368 |
| 기본값 | 31457280 |

<a id="de2586651f87a000"></a>
### 설명

Shared 모드에서 사용하는 전체 communication buffer 크기로써 Shared Static Area (SSA) 내에 할당되어 사용된다.

<a id="cc5f06f8cb3b1846"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="82259a606b54b63a"></a>
### 기본 정보

<a id="d0464226ece62b3e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_CM_UNIT_SIZE |
| 요약 | communication unit size |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1024 |
| MAX | 10485760 |
| 기본값 | 1024 |

<a id="6b752d2655737c44"></a>
### 설명

Shared 모드에서 dispatcher가 관리하는 unit의 크기이다. 이 크기가 크면 메모리가 낭비되고 이 크기가 작으면 성능이 저하될 수 있다.  
Shared 모드에서 통신 packet의 최대 크기로 설정된다.

<a id="953ad7bcf8e8ec56"></a>
## DISPATCHER_CONNECTIONS

<a id="ea07539e3fcf684b"></a>
### 기본 정보

<a id="3e7e19793b755436"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_CONNECTIONS |
| 요약 | maximum number of connections for each dispatcher |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10 |
| MAX | 32768 |
| 기본값 | 950 |

<a id="e26b8ea62322c603"></a>
### 설명

Shared 모드에서 하나의 dispatcher가 관리할 수 있는 최대 connection (client)의 개수이다.  
시스템에서 지원하는 최대값이 설정값보다 작으면 내부적으로 시스템 최대값으로 설정된다.

<a id="584c9dcb963fc253"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="ce2f3847d642d6dc"></a>
### 기본 정보

<a id="8f9bbcaa782ce638"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_HOT_POLICY_INTERVAL |
| 요약 | dispatcher dequeue interval for busy waiting |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000: 1day |
| 기본값 | 100000: 0.1 second |

<a id="0e07279e7d0dfd3e"></a>
### 설명

Busy waiting에 대한 dispatcher dequeue 주기이다. (micro second)

<a id="d634d7e13aaa9a89"></a>
## DISPATCHER_LOAD_BALANCING

<a id="79be0d4693a41b26"></a>
### 기본 정보

<a id="99c2f6be004fda63"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_LOAD_BALANCING |
| 요약 | load balancing algorithm for shared mode (0: number of clients, 1: round robin) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="ebe0733c97c19b71"></a>
### 설명

Shared 모드에서 client에 접속할 때 dispatcher를 할당하는 알고리즘이다.

- 0: 현재 연결된 client 수가 적은 dispatcher에 할당한다.
- 1: 순차적으로 dispatcher에 할당한다.

<a id="583332ef603ab566"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="9811e38e76ccf67b"></a>
### 기본 정보

<a id="ebecb15579ce8339"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_NUMA_STREAM_MAP |
| 요약 | numa stream map for dispatcher |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 'x': no binding |

<a id="d49e0cd92078446d"></a>
### 설명

디스패처들이 연결될 NUMA 노드를 결정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고, 1번 스트림은 NUMA 노드 1번에 연결하고, 2번 스트림은 NUMA 노드 2번에 연결한다.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="2dad907fb8b68942"></a>
## DISPATCHER_QUEUE_SIZE

<a id="b2a1960df02409bb"></a>
### 기본 정보

<a id="8c7ac1eed0b6b5c4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_QUEUE_SIZE |
| 요약 | dispatcher queue size |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1024 |
| MAX | 32768 |
| 기본값 | 1024 |

<a id="dea4c31af88c6205"></a>
### 설명

Shared 모드에서 dispatcher와 shared-server 간의 통신을 위한 queue 크기를 설정한다.

<a id="adddf1669c37f966"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="6913560c6bac95fd"></a>
### 기본 정보

<a id="6d83dcbe564917bb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_REQUEST_MINI_QUEUE_COUNT |
| 요약 | count of mini queue per request queue |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 16 |
| 기본값 | 4 |

<a id="03af5dd40ef5cfa5"></a>
### 설명

각 request queue의 mini queue 개수이다.

<a id="240c3e2ca2924adf"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="36b5487ec0851839"></a>
### 기본 정보

<a id="23c6f3ed8d4dd166"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHER_RESPONSE_MINI_QUEUE_COUNT |
| 요약 | count of mini queue per response queue |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 16 |
| 기본값 | 4 |

<a id="627ab12b00054e94"></a>
### 설명

각 response queue의 mini queue 개수이다.

<a id="e30ab878bba5e908"></a>
## DISPATCHERS

<a id="2f6abe0649090dfc"></a>
### 기본 정보

<a id="8ebd2283f3d4bc7e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISPATCHERS |
| 요약 | number of dispatcher processes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 256 |
| 기본값 | 2 |

<a id="a30d0fcc17f7d857"></a>
### 설명

Shared 모드를 사용할 때 dispatcher process 개수를 설정한다.  
Open 단계에서는 alter system을 사용하여 값을 줄일 수 없다.

<a id="6a4ca0a5ee7fc764"></a>
## FETCH_FAILOVER

<a id="adf4e4888b4a792b"></a>
### 기본 정보

<a id="b1936bea42d88797"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | FETCH_FAILOVER |
| 요약 | enable fetch failover |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="74b646986fb21a60"></a>
### 설명

Fetch failover를 활성화한다.

<a id="b927ce35c4411222"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="c133de077645c150"></a>
### 기본 정보

<a id="12b65ac041dbd018"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY |
| 요약 | allowed session dependent features in global connection |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="9f117c6926169d65"></a>
### 설명

Global connection에서 session dependent한 정보를 포함한 질의 수행 지원 여부를 설정한다.

<a id="8eb4eae48eb567e4"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="c95fcb99c6fb5666"></a>
### 기본 정보

<a id="95a22af4aad874e9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_JOURNAL_BUFFER_SIZE |
| 요약 | global journal buffer size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1024 |
| MAX | 10 Giga |
| 기본값 | 1 Mega |

<a id="ad7fc3f267916b65"></a>
### 설명

Global journal의 buffer 크기이다.

<a id="3351f818d59f0f2d"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="c51ef4ba7f186526"></a>
### 기본 정보

<a id="a2ae75c85d674172"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE |
| 요약 | global journal buffer total max size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 Mega |
| MAX | 100 Giga |
| 기본값 | 64 Mega |

<a id="b90ff47d6f67297a"></a>
### 설명

Global journal buffer의 최대 사이즈의 합이다.

<a id="defb9e511e4af77d"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="4518576265498b4a"></a>
### 기본 정보

<a id="257914a12eb66a0c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_PROPERTY_LOCK_TIMEOUT |
| 요약 | a time limit(second) for how long global property lock statements will wait |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 (infinite) |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="d67e1829f89abdad"></a>
### 설명

Global property를 변경할 때 동시성을 제어하기 위해 lock 하는데 이 때 해당 lock 하기 위해 대기하는 시간을 설정한다.

<a id="ce5798ae727ae370"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="b3682b9f4acb76b2"></a>
### 기본 정보

<a id="cf377706b402f3f6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_COMMIT_WRITE_MODE |
| 요약 | global transaction commit write mode(0:no_wait, 1:wait, 2:disable) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 2 |

<a id="0666fceba18d13c6"></a>
### 설명

Global transaction의 commit write mode를 변경하기 위한 프로퍼티이다. TRANSACTION_COMMIT_ WRITE_MODE는 모든 트랜잭션들에 적용되는 반면에 이 프로퍼티는 global transaction에만 적용된다. 만약 해당 프로퍼티가 2로 설정되면 TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

- 0: no wait
- 1: wait
- 2: TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

<a id="ee0f97294369576f"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="486faa7977a7b06b"></a>
### 기본 정보

<a id="4bfd11c62eff1694"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_ISOLATION_SCOPE |
| 요약 | isolation scope for global transaction(0:system, 1:group) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="4610f1e3671ab02b"></a>
### 설명

Transaction이 두 개 이상의 cluster group에 걸쳐 데이터를 변경한 경우 이를 global transaction으로 처리할지 아니면 다수의 domain transaction으로 처리할지 결정하는 프로퍼티이다.

- 0: Global tranaction으로 처리
- 1: 다수의 domain transaction으로 처리

> 이 프로퍼티가 1인 경우에는 cluster group마다 독립적인 트랜잭션으로 commit하기 때문에 트랜잭션 원자성 (transaction atomicity)을 보장하지 않는다.

<a id="81375b4ed9015d58"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="490aacab766fe68c"></a>
### 기본 정보

<a id="3dba0f1648d2d089"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_LOG_DIR |
| 요약 | default global transaction log directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/wal |

<a id="419d1cdc9edce9f7"></a>
### 설명

Global transaction log의 기본 directory 이다.

<a id="4533f1948d06db7c"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="b5a919f88e6a9905"></a>
### 기본 정보

<a id="be85ec0614a710b2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_LOG_FILE_SIZE |
| 요약 | global transaction log file size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20 Mega |
| MAX | 10 Giga |
| 기본값 | 100 Mega |

<a id="f757b83c25393f8a"></a>
### 설명

Global transaction log의 file 크기이다.

<a id="0a6de8abbd18d63b"></a>
## GMASTER_NUMA_NODE

<a id="71d36f8a294824d2"></a>
### 기본 정보

<a id="93d63dd1d552b7e6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GMASTER_NUMA_NODE |
| 요약 | numa node for gmaster process |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | -1 |
| MAX | 63 |
| 기본값 | -1 |

<a id="51ae8a3a002f4a22"></a>
### 설명

gmaster 데몬이 사용할 NUMA node의 ID를 설정한다. GMASTER_NUMA_NODE 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="d61d98483ca995e1"></a>
## GMON_AUTOSTART

<a id="ba480408a7d91587"></a>
### 기본 정보

<a id="8afd0761e44a31ef"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GMON_AUTOSTART |
| 요약 | Indicate whether gmon process automatically starts or not ( 0 \| 1 ) |
| Data type | BOOLEAN |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 1 |

<a id="d1a6f550db2b11f3"></a>
### 설명

gmon 프로세스를 자동으로 시작시킬지 여부를 설정한다.

<a id="e2b337eab1814398"></a>
## HINT_ERROR

<a id="62075ed225d0dff0"></a>
### 기본 정보

<a id="fc0cd320355e0b8b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HINT_ERROR |
| 요약 | enable hint error |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="ea4f0cbe3f00e70a"></a>
### 설명

Hint 구문에 대한 syntax 에러 및 validation 에러 체크 여부를 설정한다.

<a id="2361590702636c72"></a>
## IDLE_TIMEOUT

<a id="720b377150fbdf40"></a>
### 기본 정보

<a id="a09fab635177c33a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | IDLE_TIMEOUT |
| 요약 | idle timeout(s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="0a6c9957dfc7e1db"></a>
### 설명

C/S 세션에서 최대로 대기할 수 있는 IDLE 시간을 설정하며 해당 IDLE 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT이 발생하지 않는다.

<a id="d57928b487dd684e"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="2e899eb2273decb7"></a>
### 기본 정보

<a id="f6fe91cdb8faec53"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_BUILD_PARALLEL_FACTOR |
| 요약 | index build parallel factor |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| 기본값 | 0 |

<a id="f86e7e891a6a5ef8"></a>
### 설명

인덱스를 생성할 때 병렬화 개수 (parallel factor)를 지정한다.

- 0: 시스템의 코어 개수로 지정된다.

<a id="3bbfec597f98a1bc"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="0174c1523cf11363"></a>
### 기본 정보

<a id="17e801cc2391842a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_BUILD_PARALLEL_FACTOR |
| 요약 | parallel factor for merging sub-trees |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| 기본값 | 0 |

<a id="42d99608f5e131ee"></a>
### 설명

인덱스를 생성할 때 sub-tree를 합병하기 위한 병렬화 개수 (parallel factor)를 지정한다. 만약 해당 값이 INDEX_BUILD_PARALLEL_FACTOR 보다 큰 경우에는 INDEX_BUILD_PARALLEL_FACTOR를 사용한다.

- 0: INDEX_BUILD_PARALLEL_FACTOR를 따른다.

<a id="9bb02c29cb70cde0"></a>
## INST_ALLOCATOR_COUNT

<a id="3a16559c1e51aaa0"></a>
### 기본 정보

<a id="2e424f57a816df6a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INST_ALLOCATOR_COUNT |
| 요약 | memory allocator count for instant tables or indexes |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 3 |
| MAX | 128 |
| 기본값 | 3 |

<a id="04f9d7357814cb40"></a>
### 설명

인스턴트 블록을 할당 또는 삭제하는 연산의 병렬성을 높이기 위한 프로퍼티이다.

<a id="7ade876c4f6826ff"></a>
## INST_TABLE_BLOCK_SIZE

<a id="565950093f7f042c"></a>
### 기본 정보

<a id="d3d0bcba8eec2bef"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INST_TABLE_BLOCK_SIZE |
| 요약 | a block size of instant tables or indexes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8192 |
| MAX | 1048576 |
| 기본값 | 16384 |

<a id="e53bd19cc033b93c"></a>
### 설명

인스턴트 블록의 크기를 결정한다. 만약 인스턴트 레코드의 고정영역 크기가 인스턴트 블록의 크기를 초과하는 경우 다음과 같은 에러가 발생한다.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="3cfbac85b9326b37"></a>
## IN_DOUBT_DECISION

<a id="5da0c4b088c0bc9e"></a>
### 기본 정보

<a id="635a1ec76c4e6822"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | IN_DOUBT_DECISION |
| 요약 | decision for in-doubt transaction |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| 기본값 | 2 |

<a id="f0b2f78ea557c475"></a>
### 설명

분산 트랜잭션의 in-doubt 트랜잭션을 commit 할지 rollback 할지 결정한다.

- 1: Commit
- 2: Rollback

<a id="3a1ee053caf7affe"></a>
## JOURNAL_TEMP_DIR

<a id="f3a60f0b960b36c0"></a>
### 기본 정보

<a id="9f8a5d8d3a19be7b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | JOURNAL_TEMP_DIR |
| 요약 | journaling temporary directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/journal |

<a id="4f0f4360b3acd0a5"></a>
### 설명

Journaling의 임시 디렉토리이다.

<a id="9e58c5872cacd303"></a>
## KEEPALIVE_IDLE_TIME

<a id="3be60413444b169f"></a>
### 기본 정보

<a id="ac4a0a1bbd6baa6c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 요약 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 16383 |
| 기본값 | 300 |

<a id="d3db229cf1246e83"></a>
### 설명

Keep alive packet을 송신하기 전에 client와 server 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 server 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="11eaf487224538f7"></a>
## LOCAL_CLUSTER_MEMBER

<a id="58f028879f7a65f8"></a>
### 기본 정보

<a id="e20850788e0ca83a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCAL_CLUSTER_MEMBER |
| 요약 | local cluster member name |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 'G1N1' |

<a id="f9ad79cfd1ada69d"></a>
### 설명

Local cluster member의 이름이다.

<a id="4463524a96178da4"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="cda859f0583dcf65"></a>
### 기본 정보

<a id="5137cc07adfb9f02"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCAL_CLUSTER_MEMBER_HOST |
| 요약 | host name of local cluster member |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | '127.0.0.1' |

<a id="c006cffdaca63d33"></a>
### 설명

Local cluster member의 host 이름이다.

<a id="3002f7ebe4f5cc0f"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="7ddfd321cd430ab6"></a>
### 기본 정보

<a id="b4d19efabc33aa9a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCAL_CLUSTER_MEMBER_PORT |
| 요약 | listen port of local cluster member |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 1024 |
| MAX | 49151 |
| 기본값 | 10101 |

<a id="69d1ce3b9165b364"></a>
### 설명

Local cluster member의 listen port 이다.

<a id="7f4b603ae221ab7e"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="4732d0ab4881fd9d"></a>
### 기본 정보

<a id="cf47cab1fd3e72e6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCAL_JOURNAL_BUFFER_SIZE |
| 요약 | local journal buffer size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1024 |
| MAX | 10737418240 (10 Giga) |
| 기본값 | 65536 |

<a id="7e81b613ad7a4e39"></a>
### 설명

Local journal buffer의 크기이다.

<a id="bcd53228747136cc"></a>
## LOCATION_FILE

<a id="bb34e02c5df69dc4"></a>
### 기본 정보

<a id="979cdfa36c277b3a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE |
| 요약 | location file name |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/wal/location.ctl |

<a id="fbbcfdbb4904364f"></a>
### 설명

Location file의 이름이다.

<a id="3feb1002b148a346"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="fa1f9428cef4808e"></a>
### 기본 정보

<a id="9b1d896569150f2d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_QUERY_TIMEOUT |
| 요약 | timeout for waiting locator response (sec) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 20 |

<a id="819c6308d907e8c6"></a>
### 설명

Cluster system이 split-brain 상황에 대한 해결 방안을 locator에게 질의한 후에 응답을 기다리는 시간 (초)을 설정한다. CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY를 1 이상으로 설정했을 때만 사용할 수 있는 프로퍼티이다.

<a id="b8dfdf88a3682b3c"></a>
## LOCK_HASH_TABLE_SIZE

<a id="8ac115fe225a14de"></a>
### 기본 정보

<a id="b8763b5c51497f2c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCK_HASH_TABLE_SIZE |
| 요약 | lock manager hash table size (bucket 개수) |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 1000000 |
| 기본값 | 65519 |

<a id="b1cb34fa791ad2bb"></a>
### 설명

잠금 관리자 (lock manager)가 관리하는 hash table의 최대 크기를 설정한다.

<a id="a2c31cb3ebf6f135"></a>
## LOG_BLOCK_SIZE

<a id="e50410e7e7def3f6"></a>
### 기본 정보

<a id="aa14358a33145f90"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_BLOCK_SIZE |
| 요약 | log block size(byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 512 |
| MAX | 4096 |
| 기본값 | 512 |

<a id="1cdc001aec8218f4"></a>
### 설명

LOG_BLOCK_SIZE는 log buffer가 disk의 log file로 flush 되는 최소 크기이고 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="e3bf78799c97e4bf"></a>
## LOG_BUFFER_SIZE

<a id="2784d6b4ed8152fb"></a>
### 기본 정보

<a id="ea7ed3c429a5d2e7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_BUFFER_SIZE |
| 요약 | default log buffer size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| 기본값 | 10485760 |

<a id="c8aa8186689a7ecf"></a>
### 설명

Database에서 DML 및 DDL 연산을 수행하여 생성한 redo log들은 공유 메모리 공간인 log buffer에 저장되고, LOG_BUFFER_SIZE를 참조하여 log buffer의 메모리 크기를 설정한다.

<a id="4dec26d49bae7eaf"></a>
## LOG_DIR

<a id="c402b7ccc0796ae0"></a>
### 기본 정보

<a id="d4073c1d938339ba"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_DIR |
| 요약 | default log directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/wal |

<a id="cfc03f7d74a36a48"></a>
### 설명

Log buffer에 기록된 log는 database의 영속성을 보장하기 위해 비휘발성 저장 장치에 있는 log file로 flush 되고 LOG_DIR은 log file의 경로를 설정한다.

<a id="4da07a5818e8f976"></a>
## LOG_FILE_SIZE

<a id="db085af6c11174d8"></a>
### 기본 정보

<a id="ea01d2cd4f44e5a0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_FILE_SIZE |
| 요약 | log file size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20 Mbyte |
| MAX | 60 Gbyte |
| 기본값 | 100 Mbyte |

<a id="5514c5960020aaea"></a>
### 설명

Database에서 사용되는 log file의 크기를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 log file size를 변경할 수 없다.

<a id="086644eb4ef0a0b9"></a>
## LOG_GROUP_COUNT

<a id="88fab1f2087e4da9"></a>
### 기본 정보

<a id="a0c091c936f14632"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_GROUP_COUNT |
| 요약 | initial count of log group |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 4 |
| MAX | 254 |
| 기본값 | 4 |

<a id="133fc57a8cb39ef1"></a>
### 설명

Database에서 사용되는 log group의 개수를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 영향을 미치지 않는다. Database를 생성한 후에 log group을 추가하거나 제거하는 기능은 별도의 구문으로 지원한다.

<a id="b9069d225dac1cba"></a>
## LOG_MIRROR_MODE

<a id="911100c56f9e74cd"></a>
### 기본 정보

<a id="1f293d2ccf0faedd"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_MIRROR_MODE |
| 요약 | LogMirror Mode (1:Enable, 0:Disable) |
| Data type | BOOLEAN |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="6d14391f02e30a37"></a>
### 설명

데이터베이스를 시작할 때 redo log 복제 tool인 LogMirror를 운영할 때 필요한 shared memory를 구성하기 위한 프로퍼티이다.   
LogMirror를 수행하려면 반드시 enable 되어야 한다.  
Shared memory의 크기는 LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE 프로퍼티로 변경할 수 있다.

<a id="0789dfd3864ab9f3"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="b2b1bdee4fedc5e7"></a>
### 기본 정보

<a id="483a3f50d8ba8c9d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE |
| 요약 | shared memory size for LogMirror (byte) |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10485760 (10M) |
| MAX | 1073741824 (1G) |
| 기본값 | 104857600 (100M) |

<a id="5184ec88797dad6c"></a>
### 설명

Redo log 복제 tool인 LogMirror에 사용될 shared memory의 크기를 설정하는 프로퍼티이다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="7a61dc6d6a9eeb8f"></a>
## LOG_MIRROR_TIMEOUT

<a id="49820bac8f809439"></a>
### 기본 정보

<a id="58e5abb2935ec29f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_MIRROR_TIMEOUT |
| 요약 | logmirror retry timeout (sec) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="4ce035b712e63b52"></a>
### 설명

LogMirror의 응답을 기다리는 시간이다.   
만약 0일 경우 무한정 대기하며 그렇지 않을 경우 설정한 값만큼 대기하다가 TIMEOUT이 발생하고 LogMirror service를 중단한다. 이 후 서버는 정상적으로 운영된다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="0164610597a2a16d"></a>
## LOG_SYNC_INTERVAL

<a id="91498ac9ceb169f2"></a>
### 기본 정보

<a id="a6c0c765f660ed95"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_SYNC_INTERVAL |
| 요약 | interval for synchronize log (s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 10000 |
| 기본값 | 3 |

<a id="e61067d53e6280b9"></a>
### 설명

GOLDILOCKS의 log flusher는 log buffer의 내용을 disk log file로 flush하는 system thread이다. Log flusher가 유휴상태에서 깨어나면 flush해야 할 log가 있는지 확인하여 있을 경우 flush를 수행한다. 이 때 LOG_SYNC_INTERVAL에 설정된 시간 내에 flush를 하지 않았다면 현재 log buffer의 마지막 block까지 flush를 수행하여 log buffer와 log file을 동기화한다.

<a id="6cbb0e9d931868b2"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="f1bed7ab8cddebf8"></a>
### 기본 정보

<a id="11ed03a479573d12"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_SYNC_INTERVAL_MSEC |
| 요약 | milli-second interval for synchronize log |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="a2fdb292eaa7797f"></a>
### 설명

Log를 동기화하는 millisecond 단위의 주기이다.

<a id="d825c680166cab65"></a>
## MAX_GROUP_COUNT

<a id="9a9383e3a117932e"></a>
### 기본 정보

<a id="7a95d11a9ab73ebd"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_GROUP_COUNT |
| 요약 | maximum group count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 32 |

<a id="1e4092b007df0fab"></a>
### 설명

그룹의 최대 개수이다.

<a id="6b69f6a5ba02eda5"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="aa889bc989207a7a"></a>
### 기본 정보

<a id="7a360ce65a254e48"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_JOURNAL_FILE_SIZE |
| 요약 | maximum journal file size |
| Data type | BIGINT |
| 적용단계 | MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 ( 1 Terabytes) |
| 기본값 | 0 (no limit) |

<a id="f602b4675c6a343e"></a>
### 설명

Cluster system에서 journaling이 발생할 경우 내부적으로 journaling data를 저장할 global journaling file 의 최대 크기 (quota)를 설정한다.

<a id="9518ea4c9e1496a4"></a>
## MAX_NODE_COUNT

<a id="7797e2173d6f17bd"></a>
### 기본 정보

<a id="06f822ef7ff9d056"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_NODE_COUNT |
| 요약 | maximum node count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 64 |

<a id="3748a600e2861af8"></a>
### 설명

최대 노드 개수이다.

<a id="0e4eea59054046c1"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="2fa78675ba31d3f3"></a>
### 기본 정보

<a id="73cc765494f1e0d3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_CONCURRENT_ACTIVITIES |
| 요약 | maximum number of active statements that the driver can support for a connection |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65535 |
| 기본값 | 1024 |

<a id="1f074fd66c6aa262"></a>
### 설명

동시에 수행 가능한 statement 개수를 설정한다.

<a id="5bd915d3d8353bcf"></a>
## MAXIMUM_FLANGE_COUNT

<a id="3fccb822d065f295"></a>
### 기본 정보

<a id="05b3e74b5d038cd5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_FLANGE_COUNT |
| 요약 | maximum flange count in a plan clock |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 128 |
| MAX | 65535 |
| 기본값 | 1024 |

<a id="1dd37c5bf5c4e0c6"></a>
### 설명

Plan clock에서 확장할 수 있는 flange의 최대 개수이다.

<a id="0cc6d55ff866fa3f"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="9f23252ae5470e6f"></a>
### 기본 정보

<a id="61b15aceb35f31e2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_FLUSH_LOG_BLOCK_COUNT |
| 요약 | maximum number of log block count to be flushing |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1000 |
| MAX | 2000000 |
| 기본값 | 100000 |

<a id="bf7d00081b7f5984"></a>
### 설명

Log buffer의 내용을 disk의 log file에 flush 할 때 한 번의 write 연산으로 flush 할 log block의 최대 개수를 설정한다.

<a id="dd0830348e1617d4"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="d62fbebf28439f30"></a>
### 기본 정보

<a id="e83f3010fa21a99a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_FLUSH_PAGE_COUNT |
| 요약 | maximum number of page count to be flushing |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 1024 |

<a id="f73df72c23e93623"></a>
### 설명

GOLDILOCKS의 datafile은 checkpoint와 특정 DDL문에 의해 disk에 flush 된다. Datafile을 flush 하기 위해 한 번의 write 연산으로 flush 할 data page의 최대 개수를 설정한다.

<a id="278301240c158b3a"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="d5ffecca3fc754c6"></a>
### 기본 정보

<a id="6f17394861c7db42"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_JOURNAL_REPLAY_COUNT |
| 요약 | maximum number of replaying journals for rebalance table |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| 기본값 | 2 |

<a id="cc2144ebbadfbe98"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스를 DML과 병행하여 수행할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 테이블 리밸런스는 테이블을 동기화하는 동안 발생한 journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="1aa69631421503ab"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="bdff353a4cc086c1"></a>
### 기본 정보

<a id="5c9a5103edab9d72"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_NAMED_CURSOR_COUNT |
| 요약 | maximum number of named cursor that the driver can support for a connection |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 100000 |
| 기본값 | 128 |

<a id="479b56d9c608315a"></a>
### 설명

하나의 session 내에서 사용할 수 있는 named cursor의 최대 개수이다.  
다음과 같은 경우에 named cursor가 생성된다.

- SQLSetCursorName(), SQLGetCursorName() 함수 등을 이용해 named cursor를 선언한 경우

```
{
    ...
    SQLSetCursorName( stmt,
                      "my_cursor",
                      SQL_NTS );
    ...
}
```

- SQLExecDirect(), SQLPrepare() 함수 등에서 DECLARE cursor 구문을 사용한 경우

```
{
    ...
    SQLExecDirect( stmt,
                   "DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name",
                   SQL_NTS );
    ...
}
```

- Embedded SQL에서 DECLARE cursor FOR UPDATE 구문을 사용한 경우

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name FOR UPDATE;
    ...
    EXEC SQL OPEN my_cursor;
    ...
    EXEC SQL FETCH my_cursor INTO :data;
    EXEC SQL DELETE FROM tab_name WHERE CURRENT OF my_cursor;
    ...
    EXEC SQL CLOSE my_cursor;
}
```

> Embedded SQL에서 다음과 같이 FOR UPDATE가 없는 DECLARE CURSOR 구문은 session에 named cursor를 생성하지 않는다.

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name;
    ...
}
```

<a id="184b997851581a83"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="f4adf09aa58bcb31"></a>
### 기본 정보

<a id="1a92b7d26e0eae0f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_SESSION_CM_BUFFER_SIZE |
| 요약 | maximum communication bytes per shared mode session |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 1073741824 |
| 기본값 | 20971520 |

<a id="0072a1bf9e006c4d"></a>
### 설명

Shared mode로 접속한 하나의 session에서 사용 가능한 최대 buffer size를 설정한다.  
자세한 내용은 [DISPATCHER_CM_BUFFER_SIZE](#2b8e9fc41ad20eba)를 참조한다.

<a id="3fdb78c3ca8745f8"></a>
## MEASURE_CLUSTER_LATENCY

<a id="11f503f219adf056"></a>
### 기본 정보

<a id="f445439ffdd48055"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MEASURE_CLUSTER_LATENCY |
| 요약 | measure cluster latency |
| Data type | BOOL |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="6f9b8a61d4883492"></a>
### 설명

Measure cluster의 latency 이다.

<a id="269985f56e9e9c31"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="16f38e43aca768ad"></a>
### 기본 정보

<a id="cf4715745f671d6e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MEMORY_MERGE_RUN_COUNT |
| 요약 | merge run count for memory index |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 64 |
| 기본값 | 32 |

<a id="a1caf47deae90e87"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_MERGE_RUN_COUNT는 한 번에 병합할 정렬된 block들의 개수를 설정한다.

<a id="7f26c55aa242db78"></a>
## MEMORY_SORT_RUN_SIZE

<a id="adead81d6469dadf"></a>
### 기본 정보

<a id="1f13dc4be4d4b5ae"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MEMORY_SORT_RUN_SIZE |
| 요약 | sort run size for memory index(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8192 |
| MAX | 32768 |
| 기본값 | 8192 |

<a id="91d0db416a17f201"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_SORT_RUN_SIZE는 정렬할 block 한 개의 크기를 설정한다.

<a id="3d53b2a05477c7e4"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="ead4cc8b598d9eb2"></a>
### 기본 정보

<a id="51763c7dc3b244ad"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MINIMUM_UNDO_PAGE_COUNT |
| 요약 | minimum undo page count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 16 |
| MAX | 1048576 |
| 기본값 | 16 |

<a id="749fa8053e1225d2"></a>
### 설명

DML은 이전 image를 저장하기 위해 undo page를 사용한다. DML당 undo segment를 하나씩 사용하여 undo page를 소모하는데, 만약 할당받은 undo segment의 page를 모두 소진하였을 경우 다른 undo segment의 page를 가져와서 사용할 수 있다. MINIMUM_UNDO_PAGE_COUNT는 undo page가 부족할 때 page를 가져올 undo segment를 찾기 위한 최소 undo page 수이다. 즉, undo page가 부족할 때, MINIMUM_UNDO_PAGE_COUNT 보다 많은 page를 보유한 undo segment에서만 page를 가져올 수 있다.

<a id="ed54cddaf1645a39"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="c497a82b262e9c34"></a>
### 기본 정보

<a id="8262cf9ec79399e6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MIN_SAMPLE_ROW_COUNT |
| 요약 | minimum sampling row count for analyze table |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 9223372036854775807 (INT64_MAX) |
| 기본값 | 100000 |

<a id="c5facd55d429d951"></a>
### 설명

샘플링을 이용해서 [ANALYZE TABLE](../part-03-sql-manual/16-sql-references.md#313298c58633e794)을 수행할 때의 최소 샘플링 row 건수이다.

<a id="604927467caca382"></a>
## NET_BUFFER_SIZE

<a id="2c11a62d67ee7086"></a>
### 기본 정보

<a id="06ed6865349cba2a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NET_BUFFER_SIZE |
| 요약 | TCP network buffer size (byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1024 |
| MAX | 1073741824 |
| 기본값 | 32768 |

<a id="5e642caa60f3bf7a"></a>
### 설명

TCP 통신 buffer size를 설정한다.  
Dedicated 모드에서는 통신 packet의 최대 크기로 설정된다.  
Shared 모드에서는 [DISPATCHER_CM_UNIT_SIZE](#cc5f06f8cb3b1846)가 사용된다.

<a id="39cb46c447575199"></a>
## NLS_DATE_FORMAT

<a id="72242f3d60204480"></a>
### 기본 정보

<a id="1f876d208a0d1d09"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NLS_DATE_FORMAT |
| 요약 | nls date format |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | YYYY-MM-DD |

<a id="8ae80ee85ee68f0a"></a>
### 설명

NLS_DATE_FORMAT은 TO_CHAR와 TO_DATE 함수의 default date format을 지정한다.

<a id="2524063f770de1b8"></a>
## NLS_TIME_FORMAT

<a id="aa05f827d0bb72e0"></a>
### 기본 정보

<a id="823df879e3e042b1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NLS_TIME_FORMAT |
| 요약 | nls time format |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | HH24:MI:SS.FF6 |

<a id="e30e20ab735521c1"></a>
### 설명

NLS_TIME_FORMAT은 TO_CHAR와 TO_TIME 함수의 default time format을 지정한다.

<a id="838ff7f06a1cc0ac"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="1b23129dd9c82128"></a>
### 기본 정보

<a id="342d464f99245ef3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NLS_TIME_WITH_TIME_ZONE_FORMAT |
| 요약 | nls time with time zone format |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | HH24:MI:SS.FF6 TZH:TZM |

<a id="fc232d63c16b446a"></a>
### 설명

NLS_TIME_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIME_WITH_TIME_ZONE 함수의 default time with time zone format을 지정한다.

<a id="db86968fe3d06d6e"></a>
## NLS_TIMESTAMP_FORMAT

<a id="8a03648283714e97"></a>
### 기본 정보

<a id="1fac50d9f8d9f85b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NLS_TIMESTAMP_FORMAT |
| 요약 | nls timestamp format |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | YYYY-MM-DD HH24:MI:SS.FF6 |

<a id="f46003becdcafbc7"></a>
### 설명

NLS_TIMESTAMP_FORMAT은 TO_CHAR와 TO_TIMESTAMP 함수의 default timestamp format을 지정한다.

<a id="3356e96838139b8a"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="ba5143403b7114fd"></a>
### 기본 정보

<a id="c597bcf5ea86f2ef"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT |
| 요약 | nls timestamp with time zone format |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM |

<a id="f3972ace8b61f870"></a>
### 설명

NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIMESTAMP_WITH_TIME_ZONE 함수의 default timestamp with time zone format을 지정한다.

<a id="d5ad0f9fa74fb9d7"></a>
## NUMA

<a id="8ece582439a61b6e"></a>
### 기본 정보

<a id="382e3d87b1d8d7a6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NUMA |
| 요약 | enable numa |
| Data type | BOOLEAN |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="a631b073b2c1d581"></a>
### 설명

NUMA를 활성화/ 비활성화한다.

> AIX에서 NUMA 속성을 사용하려면 사용자 계정을 변경해야 한다. 다음 명령을 루트 사용자로 실행한다.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> 여기에서 &lt;username&gt;은 루트가 아닌 AIX 사용자 계정이다.  
> 변경 사항을 적용하려면 로그아웃한 후에 다시 로그인해야 한다.

<a id="308b0fcb7b76c764"></a>
## NUMA_MAP

<a id="db88c16e31fc8477"></a>
### 기본 정보

<a id="2f789bfd6921ad21"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NUMA_MAP |
| 요약 | numa node map |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 'x': no binding |

<a id="e4a340696b5549b5"></a>
### 설명

시스템의 CPU core들을 NUMA 노드에 연결하기 위한 map을 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 시스템의 core가 네 개인 경우의 예이다.

- 0과 1은 NUMA 노드 0번에 연결하고, core 2와 3은 NUMA 노드 1번에 연결한다.

```
NUMA_MAP = '0:0:1:1' # core
```

- 0과 1은 NUMA 노드 0번에 연결하고, core 2와 3은 NUMA 노드 1번, core 1과 3을 NUMA 노드 2번에 연결한다.

```
NUMA_MAP = '0:0,2:1:1,2' # core
```

<a id="9ea26d44f73066b7"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="6e91cd0a328916ef"></a>
### 기본 정보

<a id="189b49806e9b6af5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | OFFLINE_MEMBER_AFTER_FAILOVER |
| 요약 | Aromatically offline member after failover |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="daac1234bfaff3aa"></a>
### 설명

시스템의 백그라운드 프로세스 (gmaster)는 노드 장애에 따른 failover를 완료한 후에 장애 멤버를 자동으로 오프라인시킨다.

만약 NO로 설정되어서 장애 멤버가 오프라인되지 않았다면 장애 멤버를 시스템에 다시 조인시키기 전에 다음 구문을 실행해야 한다.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="fe9af156152592be"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="05609b9407365e82"></a>
### 기본 정보

<a id="390a143c15d95c47"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_JOURNAL_REPLAY_THRESHOLD |
| 요약 | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 (10G) |
| 기본값 | 1048576 (1M) |

<a id="557dfa56f7010786"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스는 수행 중에 발생한 DML이 남긴 journal log를 여러 번에 걸쳐 반영한다. Journal log를 반영하는 최대 차수는 MAXIMUM_JOURNAL_REPLAY_COUNT가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="c79995ae50cd6528"></a>
## OS_GROUP_ACCESS

<a id="6f3c04b67c8b139f"></a>
### 기본 정보

<a id="90bb263ddea72310"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | OS_GROUP_ACCESS |
| 요약 | enable access database with OS group permission |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="90b4d779dcb9d133"></a>
### 설명

동일한 group의 다른 user가 D/A로 접속하려면 이 설정을 YES로 변경해야 한다. 또한 시스템 상의 umask도 0002로 변경해야 한다.

<a id="9f68af2aa947bbca"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="820e21487e724293"></a>
### 기본 정보

<a id="6fcd70a70be76613"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PACKET_COMPRESSION_THRESHOLD |
| 요약 | The size limit at which packets are compressed(bytes) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMNEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| 기본값 | 2113929216 |

<a id="c62695629da10124"></a>
### 설명

클라이언트로 보낼 통신 데이터의 크기가 PACKET_COMPRESSION_THRESHOLD 보다 클 경우, 통신 데이터를 압축한다.

<a id="ea356c4b40f2448d"></a>
## PAGE_CHECKSUM_TYPE

<a id="14f2cac9576a8f25"></a>
### 기본 정보

<a id="db9e03fbbfa5f06c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PAGE_CHECKSUM_TYPE |
| 요약 | page checksum type (0:LSN, 1:CRC) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMNEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="ee75f4943823e9d9"></a>
### 설명

Datafile의 각 page들에 대한 물리적 정합성을 보장하기 위해 checksum을 사용한다. GOLDILOCKS는 LSN, CRC 방식의 page checksum을 지원한다.

- 0: LSN
- 1: CRC

<a id="e33148a7324cac4b"></a>
## PARALLEL_IO_FACTOR

<a id="af90ca0969b1d09d"></a>
### 기본 정보

<a id="f0ef683b50622d67"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PARALLEL_IO_FACTOR |
| 요약 | parallel load factor |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 16 |
| 기본값 | 1 |

<a id="33eb2ca77235c6a2"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일을 병렬 로딩하고 체크포인트 할 때 데이터 파일을 병렬 기록하기 위한 thread 개수를 설정한다.

<a id="83dec9e4f88fa43f"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="4c971e4b029f527a"></a>
### 기본 정보

<a id="6a3fca038bd0385f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PARALLEL_IO_GROUP_1 |
| 요약 | parallel load group 1 |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/db |

<a id="708a57e8a3dff929"></a>
### 설명

Datafile의 병렬 IO를 위한 group directory를 설정한다. 즉, PARALLEL_IO_FACTOR 수만큼 group을 설정하여 각 group에 속한 datafile 별로 병렬 IO를 수행한다.

<a id="08bd14ac53f5a017"></a>
## PARALLEL_LOAD_FACTOR

<a id="98b489f388cd3dac"></a>
### 기본 정보

<a id="ed00dee46cd6d7d5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PARALLEL_LOAD_FACTOR |
| 요약 | parallel load factor |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 64 |
| 기본값 | 1 |

<a id="ed3c5ba55d28e59f"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일의 메모리를 적재한 후에 병렬 작업을 위한 thread 개수를 설정한다.

<a id="a97f349a03dd8363"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="bb2eb1bd6d9276f8"></a>
### 기본 정보

<a id="cb4e08d89de47a36"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PENDING_LOG_BUFFER_COUNT |
| 요약 | default pending log buffer count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 32 |
| 기본값 | 4 |

<a id="1e7b37820d989469"></a>
### 설명

여러 트랜잭션이 동시에 실행될 경우 log buffer에 대한 경쟁을 줄이기 위해 pending log buffer를 사용하며, PENDING_LOG_BUFFER_COUNT는 동시에 사용할 수 있는 pending log buffer 개수를 설정한다.

<a id="93566cb6d7281466"></a>
## PLAN_CACHE

<a id="fb7757106bce1744"></a>
### 기본 정보

<a id="aa9a52a2da596a58"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_CACHE |
| 요약 | caching sql plan |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="a88f0fefd0a9d68b"></a>
### 설명

Plan cache 사용 여부를 설정한다.

<a id="ba2ca642fafc04cc"></a>
## PLAN_CACHE_SIZE

<a id="53d4c61227b33fe1"></a>
### 기본 정보

<a id="d681ef2d72c529ba"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_CACHE_SIZE |
| 요약 | sql plan cache size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20971520 |
| MAX | 1099511627776 |
| 기본값 | 104857600 |

<a id="be078ea2f81b203b"></a>
### 설명

Plan cache에 사용할 메모리 크기를 설정한다.

<a id="538a0f4594590119"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="10f6424db27849b3"></a>
### 기본 정보

<a id="4bbe504b76693b16"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PRIVATE_STATIC_AREA_SIZE |
| 요약 | Private Static Area Size (byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 104857600 |
| MAX | 34359738368 |
| 기본값 | 104857600 |

<a id="1ef2bdbfc69f58b7"></a>
### 설명

세션에서 할당할 수 있는 최대 heap 메모리 크기를 지정한다.

<a id="930b2541fdbec46e"></a>
## PROCESS_MAX_COUNT

<a id="fd742cffb817fa98"></a>
### 기본 정보

<a id="e8456a3b5974c048"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PROCESS_MAX_COUNT |
| 요약 | Process Max Count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 12 |
| MAX | 65535 |
| 기본값 | 128 |

<a id="9839a8ab85b0128b"></a>
### 설명

시스템에서 사용할 수 있는 최대 프로세스 (thread) 개수를 지정한다.

시스템 프로세스 생성  

• D/A 또는 C/S dedicated 모드로 접속할 때마다 프로세스가 생성된다.  
• C/S shared 모드는 기본적인 balancer, dispatcher, shared-server가 프로세스이고 client에서 접속할   
&nbsp;&nbsp;때는 프로세스가 생성되지 않는다.

<a id="1c19e3cae486b41a"></a>
## QUERY_TIMEOUT

<a id="e0f570c7ebbd13fe"></a>
### 기본 정보

<a id="b4d841fcc9d6ee25"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | QUERY_TIMEOUT |
| 요약 | query timeout (s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="d201b8ab4d6e15b8"></a>
### 설명

세션에서 받은 명령어를 처리할 수 있는 최대 시간을 지정하며 만약 해당 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT 에러가 발생하지 않는다.

<a id="1222c7e0940d3f2f"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="4f3ad309bffda7d1"></a>
### 기본 정보

<a id="b6dc9705772224ae"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | READABLE_ARCHIVELOG_DIR_COUNT |
| 요약 | readable archive log directory count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 10 |
| 기본값 | 1 |

<a id="35f06633c41b0f78"></a>
### 설명

미디어 복구 시 archive redo log가 존재하는 디렉토리의 개수를 설정한다.

<a id="95fe899e16add867"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="e2bbdcdace2c9789"></a>
### 기본 정보

<a id="a384afeb1452ab97"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | READABLE_BACKUP_DIR_COUNT |
| 요약 | readable backup directory count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 10 |
| 기본값 | 1 |

<a id="064acd02bfb1529b"></a>
### 설명

증분 백업을 이용하여 파일을 복원할 때 증분 백업이 존재하는 디렉토리의 개수를 설정한다.

<a id="aecf1b152a4653fa"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="a0889a9dca0b4c86"></a>
### 기본 정보

<a id="5c45c370cf300355"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REBALANCE_BLOCK_READ_COUNT |
| 요약 | block read count for rebalance |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 100 |

<a id="48acc879eb207b2d"></a>
### 설명

Rebalance 하기 위해 block을 읽어들이는 횟수이다.

<a id="b7d56d90a78c778e"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> 3.1 이후로 지원하지 않는다.

<a id="aa64571d4ce662bf"></a>
### 기본 정보

<a id="79adeff438fc864a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RECOMPILE_CHECK_MINIMUM_PAGE_COUNT |
| 요약 | minimum page count for recompile check |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 10000 |
| 기본값 | 64 |

<a id="eac8f4f306bd4874"></a>
### 설명

Page count 변경에 의해 plan이 recompile 되었는지 여부를 체크하기 위해 minimum page count를 설정한다.

<a id="a6e4a785a58f7242"></a>
## RECOMPILE_PAGE_PERCENT

> 3.1 이후로 지원하지 않는다.

<a id="2d5b9d766a15a08c"></a>
### 기본 정보

<a id="ad7aedb3529ffe4f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RECOMPILE_PAGE_PERCENT |
| 요약 | recompile page percent |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1000 |
| 기본값 | 30 |

<a id="8d18479978eed37b"></a>
### 설명

Page count가 변경되어 plan을 recompile 할 때의 page percentage를 설정한다. 이 값이 0인 경우 page count 변경에 따른 recompile을 하지 않는다.

<a id="c2d9fc890cb79364"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="fb90b21677966b57"></a>
### 기본 정보

<a id="ea194bded7686576"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RECOVERY_LOG_BUFFER_SIZE |
| 요약 | default log buffer size for recovery |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 786432 |
| MAX | 32 Mega |
| 기본값 | 10 Mega |

<a id="e275af118611e2fa"></a>
### 설명

복구를 위한 기본 log buffer 크기이다.

<a id="9d0b6c8dcc448227"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="c37702b57332c08f"></a>
### 기본 정보

<a id="069f22d5c0f73827"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REDO_LOG_COMPRESSION_THRESHOLD |
| 요약 | The size limit at which redo log are compressed(bytes) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| 기본값 | 256 |

<a id="ae9ce27845660aeb"></a>
### 설명

생성된 REDO LOG 의 크기가 REDO_LOG_COMPRESSION_THRESHOLD 값보다 클 경우, REDO LOG를 압축한다.

<a id="aa97c82a7d8e903d"></a>
## REFINE_RELATION

<a id="f44b3e3f214ccbd1"></a>
### 기본 정보

<a id="6c3d4e0e7206b2ff"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REFINE_RELATION |
| 요약 | refine aged relations |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="fe2adf3007e677e2"></a>
### 설명

이 속성을 NO로 하면 서버를 재시작할 때 REFINE RELATION 과정을 수행하지 않는다.

해당 프로퍼티는 REFINE RELATION 도중에 문제가 발생한 경우에 사용할 수 있으며 삭제되었지만 REFINE 하지 못한 RELATION (테이블이나 인덱스)들의 공간은 재사용할 수 없다. 문제를 해결한 이후 해당 프로퍼티를 YES로 설정하고 재시작하면 삭제하지 못했던 RELATION들에 대해 REFINE을 시도한다.

<a id="e3fdfa80422c69a8"></a>
## SESSION_FATAL_BEHAVIOR

<a id="aa956c7c18f325be"></a>
### 기본 정보

<a id="376a19cacc4c8c34"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_FATAL_BEHAVIOR |
| 요약 | session fatal behavior |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="a48d5eba04303101"></a>
### 설명

Session fatal이 발생할 때 fatal을 유발한 thread만 종료시킬지 아니면 프로세스 자체를 종료시킬지 결정한다.

- 0: Fatal을 유발한 thread만 종료한다.
- 1: 프로세스를 종료한다. 해당 프로세스 내에 다수의 세션이 동시에 수행되고 있다면 모든 세션들이 데이터베이스 사용을 끝낸 후에 프로세스를 종료한다.

<a id="6c4dff6cd7423d95"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="53833370f7c1d71e"></a>
### 기본 정보

<a id="ba0432d60069dddf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_MEMORY_INIT_SIZE |
| 요약 | initial memory size for session |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 131072 (128K) |

<a id="d016bd5638f8f022"></a>
### 설명

세션에서 사용할 공유 메모리를 미리 할당할 크기를 설정한다.

<a id="7a10e7eb96b13996"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="159f5fd134a95277"></a>
### 기본 정보

<a id="43d05d4b035e5128"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_MEMORY_SHRINK_THRESHOLD |
| 요약 | threshold bytes to attempt to shrink session memory allocator ( byte ) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 131072 (128K) |

<a id="69e3b8074f7f3a3c"></a>
### 설명

세션에서 사용한 동적 공유 메모리를 해제할 때 세션에서 사용하지 않는 동적 공유 메모리를 시스템에 반납할지 여부를 판단하기 위한 경계값을 설정한다. 즉, 사용하지 않는 메모리 중 설정된 값보다 큰 크기의 메모리 청크가 있으면 시스템에 반납한다.

<a id="db25fac0e95424bc"></a>
## SHARED_MEMORY_ADDRESS

<a id="91064430d956c42f"></a>
### 기본 정보

<a id="061ae1f848e2d0da"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_MEMORY_ADDRESS |
| 요약 | shared memory address |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 1610612736 |

<a id="f7d2d82f8a67d31e"></a>
### 설명

Shared Static Area (SSA)의 주소를 지정한다.

<a id="d06298cb5e1ddcb7"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="3bdfc0293a5cca2a"></a>
### 기본 정보

<a id="145abfa65bd5b4d5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_MEMORY_STATIC_KEY |
| 요약 | Shared Memory Static KEY |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | 542353 |

<a id="3f996a9364dca72f"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory key 값을 지정한다.

<a id="ab18534da39f89b5"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="df8193b8918dde2d"></a>
### 기본 정보

<a id="f54dbe86aaa7fc36"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_MEMORY_STATIC_NAME |
| 요약 | Shared Memory Static Name |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | _STATIC |

<a id="10f44a4e3705eeaa"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory name을 지정한다.

<a id="a10dff42df0680c0"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="6f2da83a96efb6cb"></a>
### 기본 정보

<a id="788d8d3170e6a6ab"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_MEMORY_STATIC_SIZE |
| 요약 | Shared Memory Static Size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 104857600 |
| MAX | 1099511627776 |
| 기본값 | 629145600 |

<a id="fca40ec82dc10d3f"></a>
### 설명

Shared Static Area (SSA)의 크기를 지정한다.

<a id="4586d2ee6651c913"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="3c48beea9ca79b64"></a>
### 기본 정보

<a id="4327fe05688d647a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_REQUEST_QUEUE_COUNT |
| 요약 | count of global request queue |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 16 |
| 기본값 | 1 |

<a id="c242f55bce6803ce"></a>
### 설명

Shared 모드의 dispatcher에서 shared-server로 요청하는 queue 개수를 설정한다. 여러 dispatcher가 사용자의 작업 요청을 shared-server에 할당할 때 사용하는 queue로써 일반적으로 load-balance를 위해 하나를 사용한다. 그러나 dispatcher와 shared-server가 많아지면 queue에 경합이 발생하여 성능이 저하될 수 있으므로 이 값을 늘려서 사용한다. 이 값이 커지면 load-balance가 비효율적으로 될 수 있고 dead-lock이 발생할 가능성이 커진다.

<a id="b00edefc530d394a"></a>
## SHARED_SERVERS

<a id="0add370d739e0d6f"></a>
### 기본 정보

<a id="2cbaea40d23fde89"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_SERVERS |
| 요약 | number of shared-server processes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 10 |

<a id="ca2e6b7fa16b2a0a"></a>
### 설명

Shared 모드에서 shared-server process 개수를 설정한다.  
Open 단계에서는 alter system으로 값을 줄일 수 없다.

<a id="4104b1330694709f"></a>
## SHARED_SESSION

<a id="91feaed440fdc171"></a>
### 기본 정보

<a id="36b8bb8238fc6d86"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_SESSION |
| 요약 | to enable shared session |
| Data type | BOOL |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="c403694cb9dda34c"></a>
### 설명

Shared 모드를 활성화할지 여부를 설정한다. 이 값을 NO로 설정하면 load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver)가 실행되지 않는다.

<a id="3c4b915d9e19c568"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="565c0a7bb260bc9a"></a>
### 기본 정보

<a id="a93baf0e27038abd"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SNAPSHOT_STATEMENT_TIMEOUT |
| 요약 | snapshot statement timeout (s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 22118400 ( 1 year ) |
| 기본값 | 22118400 ( 1 year ) |

<a id="da4a955cb75937fd"></a>
### 설명

Snapshot read가 필요로 하는 statement의 최대 유지 시간을 설정한다. 설정된 시간을 초과한 snapshot statement들에는 TIMEOUT 에러가 발생한다.

<a id="b032c2f903a907e0"></a>
## SQL_HISTORY_SIZE

<a id="2e8b0ce103b94aa9"></a>
### 기본 정보

<a id="7633b802a39b856a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SQL_HISTORY_SIZE |
| 요약 | history size for SQLs |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| 기본값 | 0 |

<a id="94fa81c3b935508d"></a>
### 설명

SQLs의 이력 (history) 크기이다.

<a id="7eadd416b7168234"></a>
## SQL_HISTORY_TYPE

<a id="c37a495947ba36f3"></a>
### 기본 정보

<a id="8a8e02f2b99cedcb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SQL_HISTORY_TYPE |
| 요약 | history type for SQLs |
| Data Type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="595c43fdafd80f23"></a>
### 설명

SQLs의 이력 (history) 타입이다.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="a10662f9c76a1337"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="e73ae3519232d79a"></a>
### 기본 정보

<a id="7ec8cc158104624f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY |
| 요약 | supplemental log data of primary key columns be logged in redo log files |
| Data type | BOOLEAN |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="16bcb4e32c85ac2a"></a>
### 설명

Database 내의 모든 변경 내용에 대한 supplemental log를 기록한다.

<a id="43b927dd7275223b"></a>
## SYSTEM_LOGGER_DIR

<a id="788139ecf9f94261"></a>
### 기본 정보

<a id="ea9299f7e7355a79"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 요약 | system logger directory |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/trc |

<a id="6cd15d4d432d6711"></a>
### 설명

Trace 로그 메시지가 기록되는 디스크 경로를 지정한다.

<a id="4792ffa5a1cd100e"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="72e090d7bf4276e6"></a>
### 기본 정보

<a id="9ba70466e246a803"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_MEMORY_AUX_TABLESPACE_SIZE |
| 요약 | default system memory auxiliary tablespace size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 200 Mega |

<a id="5f76344abfa12bc2"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_AUX_TBS 테이블스페이스 크기를 결정한다.

<a id="b7619105a0e51dba"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="c3c3b778fc639681"></a>
### 기본 정보

<a id="75ee3e85dfe75906"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_MEMORY_DATA_TABLESPACE_SIZE |
| 요약 | default system memory data tablespace size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 200 Mega |

<a id="2edd208f6c33cd97"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="3c68a0d9aadc0736"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="66d0ed309e398755"></a>
### 기본 정보

<a id="c842dd16cab685d8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_MEMORY_DICT_TABLESPACE_SIZE |
| 요약 | default dictionary tablespace size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 256 Mega |
| MAX | 30 Giga |
| 기본값 | 256 Mega |

<a id="e25b75a7086e7426"></a>
### 설명

데이터베이스를 생성할 때 초기 DICTIONARY_TBS 테이블스페이스의 크기를 결정한다.

<a id="0078a4c8958fce47"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="8d5bb366b1b8374d"></a>
### 기본 정보

<a id="97779f610a0828a4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE |
| 요약 | default system memory temporary tablespace size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 200 Mega |

<a id="1fd909bd4cbed355"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_TEMP_TBS 테이블스페이스의 크기를 결정한다.

<a id="8bd40bc42ea2c1e3"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="8b7e19da2c52211e"></a>
### 기본 정보

<a id="4badc239943286c0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE |
| 요약 | default system memory undo tablespace size (byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 32 Mega |

<a id="4cd0fb6617f4d709"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_UNDO_TBS 테이블스페이스의 크기를 결정한다.

<a id="2dff147c9a8ca0f8"></a>
## SYSTEM_TABLESPACE_DIR

<a id="f30580ea73811ffd"></a>
### 기본 정보

<a id="00e3ba5b31d1d093"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_TABLESPACE_DIR |
| 요약 | system tablespace directory |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/db |

<a id="6ac3706d0275ec8b"></a>
### 설명

데이터베이스를 생성할 때 초기 시스템 테이블스페이스들이 저장되는 경로를 지정한다.

<a id="8149a246bb4b2da7"></a>
## SYSTEM_UDS_DIR

<a id="d64a820527ee415d"></a>
### 기본 정보

<a id="784de8ad62faea09"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 요약 | system unix domain socket directory |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | '/tmp' |

<a id="8f35187c4d6ecf77"></a>
### 설명

Unix domain socket 파일이 생성되는 directory를 설정한다.  
DB system 이외에 glsnr 등과 같은 unix domain socket에 대한 디렉토리 설정은 별도의 configuration file에서 관리된다.  
최대 설정 크기는 60 byte이다. (Unix domain socket 파일의 절대 경로 (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.)

<a id="a8787206663155e2"></a>
## TCP_CLIENT_NUMA_NODE

<a id="0deb048f4686d3ff"></a>
### 기본 정보

<a id="74bf39e8d1a0cebf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_CLIENT_NUMA_NODE |
| 요약 | numa node for TCP clients |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | -1 |
| MAX | 63 |
| 기본값 | -1 |

<a id="2c1b24671c178ad6"></a>
### 설명

Client server 세션이 바인드 될 NUMA 노드 ID를 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="88a451460c77f0e1"></a>
## TCP_NODELAY

<a id="689e2d44aa87dbf6"></a>
### 기본 정보

<a id="2b13e32218d7a1cc"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TCP_NODELAY |
| 요약 | no delays in buffer flushing within the TCP/IP protocol stack |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="fa648a9e61a23850"></a>
### 설명

C/S 방식 (TCP socket)으로 client에 data 전송할 때의 socket TCP_NODELAY 옵션을 설정한다.  
빠른 latency가 필요하지 않고 network 부하를 줄이고 싶은 경우에는 NO로 설정한다.

<a id="56e88319bfcad81c"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="0760656ea1ba55e9"></a>
### 기본 정보

<a id="641fcc3a5f168830"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TEMP_SEGMENT_CACHE_SIZE |
| 요약 | the number of segments to be cached for global temporary tables and indexes in each session |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 4294967295 |
| 기본값 | 3 |

<a id="ae0a490c1063bd2d"></a>
### 설명

Global temporary table이나 global temporary index segment가 drop 될 때 tablespace에 반납하지 않고 session에서 caching 할 segment 개수를 지정한다. Segment cache에 존재하는 segment는 향후 global temporary table이나 global temporary index에서 재사용된다.

- 0: Session에서 global temporary table이나 global temporary index의 segment cache를 사용하지 않는다.
- 1 ~ 4294967295: Session에서 global temporary table이나 global temporary index의 segment cache를 주어진 개수만큼 유지한다.

<a id="7c831a78045be60a"></a>
## TEMP_UNDO_ENABLED

<a id="810d033f44485c6b"></a>
### 기본 정보

<a id="657cd371caec642d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TEMP_UNDO_ENABLED |
| 요약 | enables writing undo records of global temporary tables to the temp tablespace |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="ab58982bf6304e28"></a>
### 설명

Global temporary table에 대한 undo 레코드의 로깅 위치를 지정한다.

- 0 (FALSE): 데이터베이스의 기본 undo tablespace에 undo 레코드를 기록한다.
- 1 (TRUE): 데이터베이스의 기본 temporary tablespace에 undo 레코드를 기록한다.

<a id="491fa1f14e74100c"></a>
## TIMED_STATISTICS

<a id="fd39fb515a84f538"></a>
### 기본 정보

<a id="4c8dc56b7adbab01"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TIMED_STATISTICS |
| 요약 | timed statistics |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="0f913a7a1bfeb39b"></a>
### 설명

Wait event를 측정하는지 여부이다.  
v$system_event, v$session_event, v$session_wait table에 wait event와 관련된 통계 기록을 남기고 싶은 경우 설정한다.

- 0: 통계 기록을 남기지 않는다.
- 1: 통계 기록을 남긴다.
- 2: High precision timer를 이용하여 통계 기록을 남긴다.

<a id="25790eccd6d36471"></a>
## TIMEZONE

<a id="d2dfc31ae22f205f"></a>
### 기본 정보

<a id="b2dc876f1b7b52a7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TIMEZONE |
| 요약 | timezone |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | +09:00 |

<a id="440e49463ed2ec1c"></a>
### 설명

Database의 time zone 값이다.  
Database가 생성될 때 적용되는 속성으로써 -14:00 ~ +14:00 범위의 값을 사용할 수 있다.

<a id="ad666b46e581dfd7"></a>
## TRACE_ALTER_SYSTEM

<a id="d26149172128013f"></a>
### 기본 정보

<a id="3a20864fb7da38c1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_ALTER_SYSTEM |
| 요약 | write trace messages for ALTER SYSTEM |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="68f9a34675444274"></a>
### 설명

ALTER SYSTEM 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

시스템 변경에 대한 기록을 남기려면 TRACE_ALTER_SYSTEM 프로퍼티를 ON으로 설정한다.  

TRACE_ALTER_SYSTEM 프로퍼티는 SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="a968095053191bbd"></a>
## TRACE_DDL

<a id="4b0b6c2e92fc87d0"></a>
### 기본 정보

<a id="1a1b9eb9b95d99f1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_DDL |
| 요약 | write trace messages for DDL |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="1a4f73305aecdd60"></a>
### 설명

Data Definition Language (DDL) 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

테이블 생성, 삭제, 변경 등과 같은 SQL 문을 실행했을 때 이에 대한 기록을 남기려면 TRACE_DDL 프로퍼티를 ON으로 설정한다.  

TRACE_DDL 프로퍼티는 DDL 구문 수행에만 영향을 주며, SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="6ea871bf73c92847"></a>
## TRACE_LOG_ID

<a id="7402aa9b65acad77"></a>
### 기본 정보

<a id="7d84d3b76a5f2294"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOG_ID |
| 요약 | trace log ID |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="4e9fa2bc09fe634e"></a>
### 설명

질의를 수행할 때 해당 질의에 대한 실행 계획 정보와 기타 정보를 trace directory (&lt;GOLDILOCKS_DATA&gt;/trc/) 아래에 있는 trace file (opt_p[프로세스ID]_s[세션ID].trc)에 기록한다.

질의에 대한 SQL 구문과 실행 계획, 수행시간 등에 대한 기록을 남기려면 아래 표의 flag 정보를 조합하여 설정한다.

**TRACE_LOG_ID에 대한 flag 정보**

<a id="4f0c9100e9c21638"></a>
| 정보 | Flag(on) | Flag(off) |
| --- | --- | --- |
| 성공한 SQL 질의 출력 여부 | 100000 | 0 |
| 실패한 SQL 질의 출력 여부 | 10000 | 0 |
| 실행 계획 출력 여부 | 1000 | 0 |
| 실행 형태 (direct/prepare) 출력 여부 | 100 | 0 |
| Bind 값 출력 여부 | 10 | 0 |
| 구간별 수행시간 출력 여부 | 1 | 0 |

"성공한 SQL 질의 출력" + "실행 계획 출력" + "Bind 값 출력" 하려면 TRACE_LOG_ID 값을 101010으로 설정한다.

<a id="86bdaa0fadb69a52"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="e5f56fcf78dccc8c"></a>
### 기본 정보

<a id="834d3abc250f5676"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOG_MSGBUF_SIZE |
| 요약 | memory buffer size for trace log message |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 8192 |
| MAX | 10485760 |
| 기본값 | 8192 |

<a id="ccae965f87867abd"></a>
### 설명

Trace logfile에 기록할 log message를 구성하는데 사용되는 heap memory buffer의 크기를 설정한다.

<a id="804237767640b1e5"></a>
## TRACE_LOG_TIME_DETAIL

<a id="037238fa2bf77a9f"></a>
### 기본 정보

<a id="3d54ac2455b1844d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOG_TIME_DETAIL |
| 요약 | detail trace log time |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="3e3da5d86603c1f8"></a>
### 설명

Trace log를 기록할 때 시간 정확도를 높일지 여부를 설정한다.  
이 값이 OFF로 설정된 경우, 10 ms의 정확도를 가지며, ON으로 설정된 경우 1 us의 정확도를 가진다.

<a id="78ca140f888ef806"></a>
## TRACE_LOGGER

<a id="735d1650a8bdd8b9"></a>
### 기본 정보

<a id="7b95876e993a6e7a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER |
| 요약 | trace log type ( 1:file, 2:file & remote ) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| 기본값 | 1 |

<a id="f7cbbd281b1d5788"></a>
### 설명

Trace log를 기록할 대상을 설정한다.  
1이면 file에 기록하고 2이면 remote로 파일에 기록한다.  
Remote로 기록하면 gtrclogger에서 원격으로 trace log를 수집하여 파일에 기록한다.

<a id="d2ec4e0c03824711"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="463fb3a38169f0dd"></a>
### 기본 정보

<a id="f59a4c8131324039"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER_REMOTE_HOST |
| 요약 | remote host for trace logger |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 255255255255 |
| 기본값 | 127000000001 |

<a id="a438291b6f063f12"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 host를 설정한다.

<a id="50e03c1fe950f00e"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="9deabe1a06952ddd"></a>
### 기본 정보

<a id="7a00a725c8c72ae2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER_REMOTE_PORT |
| 요약 | remote port for trace logger |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1024 |
| MAX | 49151 |
| 기본값 | 21470 |

<a id="204280da66b1bec7"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 port를 설정한다.

<a id="cf4671f13d11cce3"></a>
## TRACE_LOGIN

<a id="4b4877353be3dddf"></a>
### 기본 정보

<a id="c0e533a1628611a2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGIN |
| 요약 | write login trace messages for user |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="c2c9e7a131a92fef"></a>
### 설명

로그인 할 때 해당 접속 정보를 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc)에 기록한다.  
로그인 할 때 이에 대한 기록을 남기려면 TRACE_LOGIN 프로퍼티를 ON으로 설정한다.

<a id="9dcfe1f23aece94d"></a>
## TRACE_LONG_RUN_CURSOR

<a id="6b5cbb6c73cebf11"></a>
### 기본 정보

<a id="cd01363f2df43f7e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LONG_RUN_CURSOR |
| 요약 | write trace SQL for cursor life-time over specific time (mili-sec. 0 ~ 10000000) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="a6ed3db0dde73cc3"></a>
### 설명

Cursor의 lifetime이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.

- 커서의 lifetime이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_CURSOR TO DEFAULT;
```

다음과 같이 커서를 오래 유지하는 사용자 프로그램을 추적하기 위해 사용한다.

```
int main()
{
   ...
   EXEC SQL DECLARE cur1 CURSOR FOR SELECT name FROM t1 WHERE pk = :s_id;
   EXEC SQL OPEN cur1
   EXEC SQL FETCH cur1 INTO :s_name;
```

- 사용자 logic으로 인해 ager가 오랜 시간 자원을 정리하지 못한다.

```
long_run_user_logic( s_name );

   EXEC SQL CLOSE cur1;
   ...
}
```

<a id="9e855e62e7b696bd"></a>
## TRACE_LONG_RUN_SQL

<a id="a4e85803680e180f"></a>
### 기본 정보

<a id="7a88de1ba0b2bcf2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LONG_RUN_SQL |
| 요약 | write trace for long-run SQL over specific execution time (mili-sec. 0 ~ 10000000) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="aa026efc5ecf13e3"></a>
### 설명

구문의 수행시간이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.

- 수행시간이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="5333666515f68492"></a>
## TRACE_XA

<a id="2083293fb115ef9d"></a>
### 기본 정보

<a id="dbede164735b3430"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_XA |
| 요약 | logging trace log for xa interfaces |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="864732e2e57fb164"></a>
### 설명

XA 인터페이스를 사용할 때 추적 메세지를 출력할지 여부를 지정한다. 메세지는 'SYSTEM_LOGGER_DIR/xa.trc'에 출력된다.

<a id="6230d69821e35411"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="f6f1008ba74a34a8"></a>
### 기본 정보

<a id="c2e1094823564b62"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_ALLOCATION_TIMEOUT |
| 요약 | a time limit (sec) for allocating transaction slot |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 3 |

<a id="fbf9aef129988f3d"></a>
### 설명

Transaction slot을 할당할 때의 최대 대기 시간이다.

대기 시간이 TRANSACTION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="720f606b7425c7a5"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="190f5c3631e5f093"></a>
### 기본 정보

<a id="70d7fa44be7a4bec"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_COMMIT_WRITE_MODE |
| 요약 | transaction commit write mode (0:no_wait, 1:wait) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="c17911c91a75579a"></a>
### 설명

TRANSACTION_COMMIT_WRITE_MODE는 트랜잭션이 완료될 때 트랜잭션이 생성한 log를 disk log file에 flush할지 여부를 설정한다. 즉, TRANSACTION_COMMIT_WRITE_MODE가 '1'이면 log를 트랜잭션 완료 시점에 disk log file에 flush해야 하고, 그렇지 않은 경우 log flush 여부와 관계없이 트랜잭션을 완료한다.

만약 TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정하여 시스템을 운용하는 경우에 트랜잭션을 COMMIT 한 후 log flush가 되지 않은 상태에서 GOLDILOCKS가 비정상적으로 종료되면 기록되지 않은 log로 인해 최신 data를 잃어버리게 된다.

따라서 모든 트랜잭션이 완료되었을 때 반드시 database에 남아 있어야 하는 경우 TRANSACTION_COMMIT_WRITE_MODE를 '1'로 설정하여 시스템을 운용하거나, TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정한 후 트랜잭션이 완료되는 시점에 명시적으로 'ALTER SYSTEM FLUSH LOGS'문을 수행하여 log를 flush해야 한다.

- 0: no wait
- 1: wait

<a id="055782ea275adf16"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="ee37e502b57c7115"></a>
### 기본 정보

<a id="319b9da910557dea"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT |
| 요약 | 트랜잭션이 기록할 수 있는 최대 undo 페이지 개수 |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 838860800 |
| 기본값 | 838860800 |

<a id="1c563c8e431f13ca"></a>
### 설명

트랜잭션이 기록할 수 있는 최대 undo 페이지 개수를 의미한다. 최소값은 1로 8 Kbyte이며 최대값은 838860800으로 100 Gbyte이다.

<a id="f23b6b2864c8e1d5"></a>
## TRANSACTION_TABLE_SIZE

<a id="4838177b42a39a84"></a>
### 기본 정보

<a id="b248f98052dfed67"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_TABLE_SIZE |
| 요약 | transaction table size |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 64 |
| MAX | 10240 |
| 기본값 | 1024 |

<a id="7cc24a6404ca234a"></a>
### 설명

Database에서 수행되는 최대 트랜잭션 테이블의 수를 설정한다. Database를 갱신할 때 트랜잭션의 ACID를 보장하기 위해 트랜잭션 테이블을 할당한다. 트랜잭션 테이블의 수를 변경하려면 database를 재시작해야 하며, 이전에 설정된 값보다 더 큰 수로만 변경할 수 있다.

더 작은 수로 변경하면 재시작에 실패하는데 예를 들어, 1024로 설정된 값을 512로 변경하면 다음과 같이 재시작에 실패한다. 이 경우 1024보다 크거나 같은 수로 설정하면 재시작에 성공한다.

```
gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 512 SCOPE = FILE;

System altered.

gSQL> \CONNECT sys gliese as sysdba
gSQL> \SHUTDOWN

Shutdown success
```

- 재시작 실패

```
gSQL> \STARTUP

ERR-HY000(14118): TRANSACTION_TABLE_SIZE property value must be equal to or greater than '1024'

gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 1024 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

<a id="5bb5a43a2d96907d"></a>
## TRANSACTION_TIMEOUT

<a id="0188a6c82c757a0d"></a>
### 기본 정보

<a id="c52355e88008d98a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_TIMEOUT |
| 요약 | transaction timeout(s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="2f822547f9724805"></a>
### 설명

Transaction이 활성화되어 있는 시간을 설정한다. Transaction이 장시간 활성화되어 있을 때 발생할 수 있는 부작용을 방지하기 위해 사용한다. Transaction이 정해진 시간을 초과할 경우, gmaster 데몬이 해당 transaction을 소유한 세션을 자동으로 종료시킨다.

<a id="32a59b43d67d3df9"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="e0e1838443207cc9"></a>
### 기본 정보

<a id="5512af1e2878f44f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UNDO_RELATION_ALLOCATION_TIMEOUT |
| 요약 | a time limit (sec) for allocating undo relation |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 3 |

<a id="49eaff5692fa1a8f"></a>
### 설명

Undo relation을 할당할 때의 최대 대기 시간이다.

대기 시간이 UNDO_RELATION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="a51b2f96e4f660b7"></a>
## UNDO_RELATION_COUNT

<a id="d7a0d23935532cb1"></a>
### 기본 정보

<a id="951688ce89d16a52"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UNDO_RELATION_COUNT |
| 요약 | undo relation count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8 |
| MAX | 10240 |
| 기본값 | 128 |

<a id="61a3f3924de552fa"></a>
### 설명

Database에서 사용할 undo relation의 수를 설정한다. Undo relation은 DML을 수행하는 트랜잭션이 undo segment를 사용하도록 하기 위해 할당한다. Undo relation의 수를 변경하기 위해서는 database를 재시작해야 하며 이전에 설정된 값보다 더 큰 수로만 변경할 수 있다.

더 작은 수로 변경하면 재시작에 실패하는데 예를 들어, 128로 설정된 값을 64로 변경하면 다음과 같이 재시작에 실패한다. 이 경우 128보다 크거나 같은 수로 설정하면 재시작에 성공한다.

```
gSQL> ALTER SYSTEM SET UNDO_RELATION_COUNT = 64 SCOPE = FILE;

System altered.

gSQL> \CONNECT sys gliese as sysdba
gSQL> \SHUTDOWN

Shutdown success
```

- 재시작 실패

```
gSQL> \STARTUP

ERR-HY000(14119): UNDO_RELATION_COUNT property value must be equal to or greater than '128'

gSQL> ALTER SYSTEM SET UNDO_RELATION_COUNT = 128 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

<a id="5a84fd09ad5a260c"></a>
## UNDO_SHRINK_THRESHOLD

<a id="b370c5d1b8450b91"></a>
### 기본 정보

<a id="b0edee42f383682c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UNDO_SHRINK_THRESHOLD |
| 요약 | threshold bytes to attempt to shrink undo segment(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 107374182400 |
| 기본값 | 10485760 |

<a id="0a36c13e2b6d1519"></a>
### 설명

Ager thread는 주기적으로 (10초) undo segment의 공간을 검사하여 공간을 많이 차지하고 있을 경우, 일부분을 테이블스페이스로 반환한다. 이 프로퍼티는 한 번에 반환해야 할 바이트 단위의 크기를 의미한다.

<a id="4f5b19b609458ab0"></a>
## USE_LARGE_PAGES

<a id="6a4ab6c570c439b9"></a>
### 기본 정보

<a id="783792364dfe24d0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USE_LARGE_PAGES |
| 요약 | use large pages |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="1b6b2f2acd58447a"></a>
### 설명

HugePage를 사용한다. USE_LARGE_PAGES를 사용하려면 먼저 장비에 HugePage를 설정해야 한다.

- 0: Large page를 사용하지 않는다.
- 1: Large page를 사용한다. 만약 공유 메모리 할당에 실패할 경우에는 에러가 발생한다.
- 2: Large page를 사용하여 할당을 시도한다. 만약 공유 메모리 할당에 실패할 경우에는 regular page를 사용하여 메모리를 할당한다.

> 리눅스 커널 2.6.32-573 이상에서만 사용할 수 있다.

---

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
