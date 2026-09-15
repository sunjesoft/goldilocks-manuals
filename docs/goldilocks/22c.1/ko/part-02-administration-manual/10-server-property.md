<a id="5c4ff2359a15b769"></a>

# 10. Server Property

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/5c4ff2359a15b769)  
> 태그: `22c.1_10_tag`

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="77691ed5e972acea"></a>
## Server Property 정보

Property는 다음 SQL 구문으로 변경할 수 있다.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#677a2c760cc67fbc) 
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#4923f8bcbf518f9e)

Property 정보는 다음 view로 확인할 수 있다.

- [V$PROPERTY](9-database-information.md#8e14932731e251fa): 시스템 운영 도중이나 재시작 과정에서 변경할 수 있는 property list를 보여준다.
- [V$SPROPERTY](9-database-information.md#2221a72b31f18fb5): Binary file에서 읽어 들여 설정된 property 이거나, binary file에 저장된 property list 이다.
- [V$DB_PROPERTY](9-database-information.md#b4b40238a392b16f) : 데이터베이스를 생성할 때만 변경할 수 있고, 이후에는 변경할 수 없는 read-only 속성을 갖는 property list 이다.

본 매뉴얼의 property 기본 정보 각 항에 대한 설명은 다음과 같다.

<a id="434e7cf721e9abb2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | Property의 구분자이다. |
| 요약 | Property 요약 설명이다. |
| Data type | Property가 갖는 값의 데이터 타입이다. |
| 적용 단계 | ALTER SYSTEM 또는 ALTER SESSION으로 변경할 수 있는 startup phase에 적용할 수 있다 * NONE: 적용할 수 있는 단계가 없다. (만약 변경 가능하지만 적용 단계가 NONE인 경우에는 SCOPE = FILE을 이용해야 한다.) |
| 변경가능 여부 | Property를 변경할 수 있는지 여부이다. * 해당 값이 TRUE일 경우, 변경할 수 있다. * 해당 값이 FALSE일 경우, read-only만 가능하다. |
| ALTER SESSION 여부 | [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#4923f8bcbf518f9e) 구문으로 변경할 수 있는지 여부이다. |
| ALTER SYSTEM 여부 | [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#677a2c760cc67fbc) 구문으로 변경할 수 있는지 여부이다. * IMMEDIATE: 수행 즉시 모든 SESSION에 변경된 값이 반영된다. * DEFERRED: 수행된 이후에 접속한 SESSION에만 변경된 값이 반영된다. 이미 접속된 SESSION에는 반영되지 않는다. * FALSE: 운영 중에는 변경된 값이 반영되지 않으며 restart 이후에 변경된 값이 반영된다. SCOPE=FILE로만 수행할 수 있다. * NONE: 변경할 수 없다. |
| MIN | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최소값이다.  VARCHAR일 경우에는 N/A이다. |
| MAX | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최대값이다. VARCHAR일 경우에는 N/A이다. |
| 기본값 | 해당 property가 갖는 기본값이다. |

<a id="de9cbe489f1a4134"></a>
## Property Alias 정보

Property alias 정보는 [V$PROPERTY_ALIAS](9-database-information.md#d3f8dde944bb64df) view를 통해 확인할 수 있다.

본 매뉴얼에 쓰인 property alias의 기본 정보는 다음과 같다.

<a id="7cb4aa665a38d71c"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | Property의 원본 구분자이다. |
| ALIAS | Property alias 구분자이다. |

Property alias 목록은 [Property Alias](../part-01-getting-started/4-what-s-new.md#ff5543ba546a3184)를 참조한다.

<a id="1afa9ee3d8d4ed58"></a>
### CDISPATCHER_THREADS

[CDISPATCHER_LOCKABLE_THREADS](#c8bfd353e9c35721)의 alias이다.

<a id="16089d743fa0c945"></a>
### CLUSTER_COMMIT_SLAVES

[CLUSTER_COMMIT_SLAVE_CSERVERS](#d228d737f7944d63)의 alias이다.

<a id="c914d146e83ca310"></a>
### CLUSTER_SERVER_RESPONSE_ QUEUE_SIZE

[CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE](#540a7313e72f614b)의 alias이다.

<a id="fbcf6282fb5fd10f"></a>
### CSERVER

[CLUSTER_LOCKABLE_CSERVERS](#3fa9eef22b15e015)의 alias이다.

<a id="66250c2ed0500529"></a>
### INCREMENTAL_CHECKPOINT_CRITERIA

[BUFFER_DIRTY_PAGE_LIMIT](#f27cdd06cf3054f4)의 alias이다.

<a id="6c552a601ac84957"></a>
### LOCKLESS_CSERVERS

[CLUSTER_LOCKLESS_CSERVERS](#531e53de52255f11)의 alias이다.

<a id="7c3f66a5f96aa83a"></a>
### MEMORY_MERGE_RUN_COUNT

[INDEX_MERGE_RUN_COUNT](#1fda90fc5c7d93a9)의 alias이다.

<a id="8affb465ef70490b"></a>
### MEMORY_SORT_RUN_SIZE

[INDEX_SORT_RUN_SIZE](#3a3a8e2b59bb5329)의 alias이다.

<a id="cb74a1ba9b3815ea"></a>
### SYSTEM_LOGGER_DIR

[TRACE_SYSTEM_DIR](#9082de9a7be5d382)의 alias이다.

<a id="bd597ee2b6a74bc7"></a>
## ADMIN_SESSION_POOL_INIT_SIZE

<a id="22f2f4d01d95135d"></a>
### 기본 정보

<a id="5a8ee88aa4850129"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ADMIN_SESSION_POOL_INIT_SIZE |
| 요약 | initial memory size for admin session pool |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1099511627776 (1T) |
| 기본값 | 10485760 (10M) |

<a id="0339eb70b1adba04"></a>
### 설명

Admin session pool의 초기 메모리 크기를 설정한다.

<a id="b59402fc3e1016bf"></a>
## ADMIN_SESSION_POOL_NEXT_SIZE

<a id="6ed2e91d40e4c2dd"></a>
### 기본 정보

<a id="f78eab9959821935"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ADMIN_SESSION_POOL_NEXT_SIZE |
| 요약 | memory size to be expanded in admin session pool |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 1048576 (1M) |

<a id="e86eee70d104237e"></a>
### 설명

Admin session pool의 공간을 확장할 때 session pool 내부의 메모리 크기를 얼마나 확장할지 설정한다.  
ADMIN_SESSION_POOL_INIT_SIZE가 0보다 큰 경우에만 유효하다.

<a id="814e141ef6228853"></a>
## AGING_INTERVAL

<a id="6be01687eab61b8e"></a>
### 기본 정보

<a id="2f114a4b366152b1"></a>
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

<a id="83daffca588e62a0"></a>
### 설명

MVCC 기반의 database에서 이전 버전의 데이터를 지우는 ager thread가 처리할 job이 없을 때의 유휴 시간 (초)을 설정한다.

<a id="3704034ce6ae3015"></a>
## AGING_PLAN_INTERVAL

<a id="feddaccdbd234c27"></a>
### 기본 정보

<a id="1e47b911ac39d68e"></a>
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

<a id="8d29c2b540144677"></a>
### 설명

AGING_PLAN_INTERVAL 보다 오래된 SQL plan이 aging 대상이 된다.

<a id="55fb22f483f6cfdc"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="79f83b41294c2ff2"></a>
### 기본 정보

<a id="90c630d60a320622"></a>
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

<a id="fb1bd34db5249440"></a>
### 설명

GOLDILOCKS 데이터베이스의 온라인 redo log file이 archive되는 디렉토리와 미디어 복구할 때 archive redo log file을 읽을 위치를 설정한다. 온라인 redo log file은 ARCHIVELOG_DIR_1에만 archive redo log file을 생성한다.

ARCHIVELOG_DIR_1은 시스템만 설정할 수 있고 ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10은 세션을 설정할 수 있다.

<a id="00d25ec0585e7d59"></a>
## ARCHIVELOG_FILE

<a id="88ae7708ceb152a6"></a>
### 기본 정보

<a id="1100b83fdb6ce053"></a>
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

<a id="c65b11de3a5be421"></a>
### 설명

온라인 redo log file을 archive 할 때 archive 디렉토리에 저장되는 목적 파일 이름의 prefix를 설정한다. Archive log file은 ARCHIVELOG_FILE에 설정된 prefix에 '_'와 파일 시퀀스, 'log' 확장자가 추가된 형태로 생성된다. 예를 들어, 파일 시퀀스가 0인 로그 파일은 'archive_0.log'으로 아카이빙된다.

<a id="1ce60185b4db7326"></a>
## ARCHIVELOG_MODE

<a id="c0cc315f6d0028f7"></a>
### 기본 정보

<a id="dce97b4db438eb31"></a>
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

<a id="276a30a516c6cb81"></a>
### 설명

Database를 생성할 때 적용되는 속성으로써 archive log mode를 다음 중 하나의 값으로 설정할 수 있다.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

Database가 생성된 후 운용되는 동안에는 archive log mode에 영향을 미치지 않고 mount 단계에서 ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}로 archive log mode를 변경할 수 있다.

<a id="ed50eb3b85411970"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="2895a422e812e859"></a>
### 기본 정보

<a id="6b786a983cb655b2"></a>
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

<a id="d8b089fac4859ae5"></a>
### 설명

증분 백업이 수행될 때 백업 파일이 생성되고 증분 백업을 이용하여 파일을 복원할 때 백업 파일이 읽혀질 디렉토리를 설정한다. 증분 백업은 BACKUP_DIR_1에 설정된 디렉토리에만 생성된다.

BACKUP_DIR_1은 시스템만 설정할 수 있고 BACKUP_DIR_2 ~ BACKUP_DIR_10은 세션을 설정할 수 있다.

<a id="5039758aa935395a"></a>
## BLOCK_READ_COUNT

<a id="29f615c06214bc53"></a>
### 기본 정보

<a id="cca46a9056c44366"></a>
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

<a id="247dd0eb41ec45e4"></a>
### 설명

SQL 처리시 row의 묶음 단위인 BLOCK_READ_COUNT 단위로 row를 읽어 연산을 처리한다.   
BLOCK_READ_COUNT는 연산을 수행할 때 한 번에 처리할 row의 개수를 의미하며 SQL 질의 처리에 참여하는 실행 노드간의 pipe-lining 처리의 기본 단위이다.

BLOCK_READ_COUNT 값이 크면 연산 처리 성능은 향상되지만 메모리 자원을 많이 사용한다.  따라서 10 ~ 100 사이의 값을 권장한다. 그 이상의 값을 사용하는 경우 자원 사용량은 비례하여 증가하지만 성능은 비례하여 향상되지 않는다.

<a id="177ed4639f442790"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="7262f915b45ac69d"></a>
### 기본 정보

<a id="75e631e8f24b412c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BROADCAST_INDEX_REBUILD_PROTOCOL |
| 요약 | broadcast index rebuild protocol |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="8fcbd449a75cbdee"></a>
### 설명

클러스터 환경에서 인덱스를 재구축할 때 여러 멤버에서 동시에 처리할지 여부를 설정한다.

<a id="b94aaf14c0427824"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="e1afc617e3995cb1"></a>
### 기본 정보

<a id="e57a1e1ce9f9e452"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BROADCAST_REBALANCE_PROTOCOL |
| 요약 | broadcast rebalance protocol |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="990147c1620ea76c"></a>
### 설명

클러스터 환경에서 테이블 리밸런스를 수행할 때 여러 멤버에서 동시에 처리할 수 있는 프로토콜을 동시 처리할지 여부를 설정한다.

<a id="258d891c7bd4cbf0"></a>
## BUFFER_CACHE_SIZE

<a id="a06e370ee8c47e3f"></a>
### 기본 정보

<a id="aa6d8e7842c6a16a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_CACHE_SIZE |
| 요약 | buffer cache size ( byte ) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 MB |
| MAX | 1 TB |
| 기본값 | 64 MB |

<a id="679ff1e36dab2e6f"></a>
### 설명

디스크 테이블스페이스의 페이지를 caching하는 버퍼의 크기를 설정한다.

<a id="1739a98c2e1ddee9"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="39daac6adcb30151"></a>
### 기본 정보

<a id="9d05a54783e03a49"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_CHECKPOINT_LIST_COUNT |
| 요약 | number of buffer checkpoint lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 36 |
| 기본값 | 1 |

<a id="6bf21aa1afcd5124"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스의 페이지들이 갱신되었을 때 체크포인트 리스트에 연결된다. 각 체크포인트 리스트는 전용 flush thread에 의해 체크포인트 리스트에 연결된 갱신된 페이지를 디스크로 flush 하는데 BUFFER_CHECKPOINT_LIST_COUNT는 체크포인트 리스트의 개수와 flush thread의 개수를 설정한다.

<a id="f27cdd06cf3054f4"></a>
## BUFFER_DIRTY_PAGE_LIMIT

<a id="35f5c20bb5bdeb4a"></a>
### 기본 정보

<a id="329a5318def3e57e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_DIRTY_PAGE_LIMIT |
| 요약 | a limit on the number of dirty pages in the buffer cache |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 134217728 |
| 기본값 | 0 |

<a id="e00d394910118762"></a>
### 설명

시스템의 버퍼 캐쉬에 갱신된 페이지들은 체크포인트 할 때 디스크에 반영되는데, 버퍼 캐쉬 크기가 크고 갱신된 페이지들이 많으면 체크포인트 시간이 길어져 서비스에 영향을 미칠 수 있다. GOLDILOCKS는 시스템에서 갱신된 페이지 수가 일정 숫자 이상이 되면 갱신된 페이지들을 디스크에 반영하는 증분 체크포인트를 수행하며 BUFFER_DIRTY_PAGE_LIMIT은 증분 체크포인트를 수행하는 기준을 설정한다.

예를 들어, 이 값이 1000으로 설정되면 시스템에서 갱신된 페이지가 1000 미만일 때는 디스크에 반영되지 않고 1000 이상이 되면 버퍼의 갱신된 페이지들을 디스크에 반영한다.

기본값은 0인데 이는 무한대를 의미하고, 버퍼에 캐싱된 페이지가 모두 갱신되더라도 증분 체크포인트를 수행하지 않는다.

BUFFER_DIRTY_PAGE_LIMIT와 [INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA](#1a0b0151961245b4)의 값은 재시작 복구의 시간과 서비스에 미치는 영향을 고려하여 적정하게 설정한다.

<a id="04ead527d7feea7e"></a>
### ALIAS

<a id="11a5d3c427648122"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | BUFFER_DIRTY_PAGE_LIMIT |
| ALIAS | INCREMENTAL_CHECKPOINT_CRITERIA |

<a id="ea40de00c72a1597"></a>
## BUFFER_FLUSH_THREADS

<a id="ec6eedeedf2a4b21"></a>
### 기본 정보

<a id="1ed9d5375f0c4d90"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_FLUSH_THREADS |
| 요약 | number of buffer flush threads |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 36 |
| 기본값 | 1 |

<a id="937b892f97314f84"></a>
### 설명

버퍼 lru list에서 갱신된 페이지를 caching한 bch를 재사용하려면 flush list에 연결하여 buffer flusher에 flush를 요청하게 되는데, 이 때 BUFFER_FLUSH_THREADS가 데이터베이스에서 사용할 buffer flusher와 flush list의 수를 설정한다.

<a id="0a5ce5debe33272a"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="b27350fcb49177dc"></a>
### 기본 정보

<a id="5c3b7c3b8bef44c8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_FLUSHING_INTERVAL |
| 요약 | buffer flushing interval time (sec) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 86400 (1 day) |
| 기본값 | 3 |

<a id="b2211f28a2e256b9"></a>
### 설명

갱신된 디스크 테이블스페이스 페이지들을 디스크로 flush하는 버퍼 flusher가 처리할 job이 없을 때의 유휴 시간 (sec)을 설정한다.

<a id="75bc73d1a85c847f"></a>
## BUFFER_FREE_LIST_COUNT

<a id="8bb4a1805f953484"></a>
### 기본 정보

<a id="0b88fd28b2488fa5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_FREE_LIST_COUNT |
| 요약 | number of buffer free lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 64 |
| 기본값 | 16 |

<a id="4e18b919e054f174"></a>
### 설명

버퍼 캐쉬에 즉시 사용 가능한 bch들을 연결하는 buffer free list의 수를 설정한다.

<a id="9072b99254ea1378"></a>
## BUFFER_HASH_BUCKETS

<a id="bdeca34666660963"></a>
### 기본 정보

<a id="5abff4900c7db78e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_HASH_BUCKETS |
| 요약 | number of buffer hash buckets |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1073741824 |
| 기본값 | 0 |

<a id="779af9cc746909b1"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스 페이지를 위한 hash bucket의 개수를 설정한다. 0 부터 1073741824 까지 설정할 수 있으며 0은 BUFFER_CACHE_SIZE에 따라 설정된 버퍼에 caching 할 수 있는 페이지 수만큼의 hash bucket을 계산하여 설정한다. 만약 설정된 값보다 버퍼의 크기가 작으면 버퍼의 크기로 hash bucket 수를 조정한다.

<a id="7e61009abd6da56e"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="369ad36378b4bd20"></a>
### 기본 정보

<a id="6ae38143c00aa79b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_HOT_REGION_CRITERIA |
| 요약 | threshold touch count of hot region in the buffer lru list |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 100 |
| 기본값 | 2 |

<a id="1e00ba61448f7400"></a>
### 설명

버퍼 lru list에서 cold region에 존재하는 페이지를 hot region으로 옮기기 위한 touch count를 설정한다.

<a id="ffd5a96100fc23dc"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="77d5f4c16d907ad4"></a>
### 기본 정보

<a id="07349f896664f906"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_HOT_REGION_PERCENT |
| 요약 | the percentage of hot region in the buffer lru list |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 80 |
| 기본값 | 20 |

<a id="aef73bd43a056531"></a>
### 설명

버퍼 lru list에 존재하는 전체 페이지 중에 hot region의 페이지의 비율 (백분율)을 설정한다.

<a id="4444b857c45fb3fa"></a>
## BUFFER_LRU_LIST_COUNT

<a id="1fbdfe66755d593b"></a>
### 기본 정보

<a id="d8a676fb38ca093b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_LRU_LIST_COUNT |
| 요약 | number of buffer LRU lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 64 |
| 기본값 | 16 |

<a id="c2d381965219e7d4"></a>
### 설명

디스크 테이블스페이스 페이지를 caching 하기 위한 free buffer가 없을 때 caching하여 사용 중인 페이지들 중에 victim을 선정하기 위한 lru list의 수를 설정한다.

<a id="7fa83b9ff039b574"></a>
## BUFFER_LRU_SCAN_PERCENT

<a id="c28b39853a38405b"></a>
### 기본 정보

<a id="34ce712b8bd9d8cc"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_LRU_SCAN_PERCENT |
| 요약 | the percentage of buffers to inspect when looking for free |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10 |
| MAX | 100 |
| 기본값 | 40 |

<a id="e80da9d4108d7a57"></a>
### 설명

시스템에서 즉시 사용 가능한 free 버퍼가 없을 때, 디스크 테이블스페이스 페이지를 버퍼에 캐싱하기 위해 lru list에서 재사용 가능한 버퍼를 구한다. Lru list에서 재사용 가능한 버퍼를 구하기 위해 검사하는 페이지 수를 결정하기 위해, BUFFER_LRU_SCAN_PERCENT는 [BUFFER_CACHE_SIZE](#258d891c7bd4cbf0)에 설정된 버퍼 페이지의 퍼센트를 설정한다.

<a id="814f9308869e08a6"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="955441258a1488ff"></a>
### 기본 정보

<a id="afff7991502be8d4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_MULTIPAGE_READ_COUNT |
| 요약 | maximum number of pages read in one I/O operation during a full scan |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 32 |

<a id="d6ac29023c24814d"></a>
### 설명

디스크 테이블을 full scan 할 때 한 번의 디스크 IO에 사용할 최대 페이지 수를 설정한다.

<a id="ccc42a15b2f278ca"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="b5ce47c1bae9daae"></a>
### 기본 정보

<a id="d92037ff6b5774cb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_PREFETCH_PAGE_COUNT |
| 요약 | the maximum number of pages to be prefetched to the buffer per I/O operation |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 32 |

<a id="fa5e2be970a7b063"></a>
### 설명

버퍼에 존재하지 않는 디스크 테이블스페이스의 페이지에 접근할 때 한 번의 디스크 I/O로 프리 페치할 인접한 최대 페이지 수를 설정한다.

<a id="32f9ffaecb31e34e"></a>
## BULK_IO_PAGE_COUNT

<a id="79831e3456e9a475"></a>
### 기본 정보

<a id="d4c58ada17fe4e9b"></a>
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

<a id="87e8623bfecb970e"></a>
### 설명

서버를 재시작할 때 데이터 파일에 IO READ가 발생할 경우나 데이터 파일을 생성할 때 IO WRITE가 발생할 경우에 사용된다.

서버를 재시작하거나 데이터 파일을 생성할 때 BULK_IO_PAGE_COUNT * 8192 크기만큼 heap 메모리가 할당되며 세션의 PRIVATE_STATIC_AREA_SIZE가 그 크기보다 작을 경우 메모리 부족 에러가 발생할 수 있다. 이 경우에는 PRIVATE_STATIC_AREA_SIZE를 늘려주어야 한다.

<a id="1bc259ebf338d35b"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="59a71f2fe9e950be"></a>
### 기본 정보

<a id="699bea51e00b2ca4"></a>
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
| 기본값 | 0 |

<a id="8f4907a2d3d5c107"></a>
### 설명

cdispatcher에서 dequeue 할 때 busy waiting 하는 시간이다. Micro second 단위이며 이 값을 크게 하면 CPU를 많이 사용하는 대신 사용자 응답 시간 (latency)은 줄어든다.  
기본값은 0 이고 busy waiting을 하지 않는다.

<a id="c8bfd353e9c35721"></a>
## CDISPATCHER_LOCKABLE_THREADS

<a id="d03eb8783bff811d"></a>
### 기본 정보

<a id="84595d096cf794e7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_LOCKABLE_THREADS |
| 요약 | cdispatcher lockable sender, receiver thread count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 30 |
| 기본값 | 1 |

<a id="240cf412d5841825"></a>
### 설명

Lockable 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockless 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKLESS_THREADS](#0824cbab94b2bfa0)로 설정한다.

<a id="5d888b5a94de99a7"></a>
### ALIAS

<a id="bb02822fe72af58f"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CDISPATCHER_LOCKABLE_THREADS |
| ALIAS | CDISPATCHER_THREADS |

<a id="0824cbab94b2bfa0"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="d539a7e3e4c1331d"></a>
### 기본 정보

<a id="3ab6fa6bebc2a617"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_LOCKLESS_THREADS |
| 요약 | cdispatcher lockless sender, receiver thread count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 30 |
| 기본값 | 1 |

<a id="b689bf23652e2a53"></a>
### 설명

Lockless 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockable 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKABLE_THREADS](#c8bfd353e9c35721)로 설정한다.

<a id="d94302eecd74ed77"></a>
## CDISPATCHER_MAX_PACKET_BUFFER_SIZE

<a id="e20abdf1f5ea4dff"></a>
### 기본 정보

<a id="aabb4c902a9f84bc"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_MAX_PACKET_BUFFER_SIZE |
| 요약 | maximum packet buffer size for cdipatcher sender and receiver threads |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10 Mega |
| MAX | 32 Giga |
| 기본값 | 1 Giga |

<a id="e7078691d991bfd3"></a>
### 설명

cdispatcher의 데이터 송수신자가 송신하거나 수신한 패킷을 저장하는 최대 버퍼 크기를 설정한다.

<a id="4e35f7ad2e4a0ff9"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="b9d5d525e0fd8a9e"></a>
### 기본 정보

<a id="f4b4afc6d23abf18"></a>
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

<a id="55008ff1fe64c316"></a>
### 설명

cdispatcher socket buffer (송신자, 수신자)의 크기이다.

<a id="707c2883008e5609"></a>
## CDISPATCHER_SYNC_THREADS

<a id="f2869a3f5f5f49fc"></a>
### 기본 정보

<a id="7d94fcd826ef987f"></a>
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
| MAX | 30 |
| 기본값 | 1 |

<a id="f32f8284e053022e"></a>
### 설명

cdispatcher sync thread의 개수이다.

<a id="94f7d8ed4cec9cd8"></a>
## CHANGE_TRACKING

<a id="5a5c0a43e16df7e0"></a>
### 기본 정보

<a id="54368232516c3c2b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHANGE_TRACKING |
| 요약 | enable change tracking for incremental backup |
| Data type | BOOLEAN |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="2a1abb31b7d2e5c9"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 변경된 페이지들을 tracking 할지 여부를 설정한다.

- NO: disable change tracking
- YES: enable change tracking

데이터베이스가 archivelog로 운용 중인 경우에만 mount 이상 단계에서 ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING 으로 change tracking을 enable 할 수 있다.

<a id="d1e11165dc6a8dd2"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="22cc8adb5775680c"></a>
### 기본 정보

<a id="d85bc1d6f9dd0dd0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHANGE_TRACKING_EXTENT_SIZE |
| 요약 | number of pages to track changed of incremental backup |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 16 |
| MAX | 128 |
| 기본값 | 32 |

<a id="b92263affc95514f"></a>
### 설명

Change tracking 할 때 하나의 dirty flag로 표시할 페이지 수를 설정한다. 예를 들어, 32로 설정하면 32 페이지당 하나의 dirty flag를 사용하고, 128로 설정하면 128 페이지당 하나의 dirty flag를 사용한다.

<a id="0c3a4f7c8eb7f939"></a>
## CHANGE_TRACKING_FILE

<a id="7b6eb1e399b18947"></a>
### 기본 정보

<a id="175ef2aa8488f459"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHANGE_TRACKING_FILE |
| 요약 | default change tracking file |
| Data type | VARCHAR |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/backup/gl_change_tracking_file.ctf |

<a id="1b3db500d2eb9ec9"></a>
### 설명

Change tracking을 저장할 파일의 디렉토리와 파일 이름을 설정한다.

<a id="4f053a478d278f9f"></a>
## CHAR_LENGTH_UNITS

<a id="4ce50ff3d0d755f1"></a>
### 기본 정보

<a id="b8cf57a492b31499"></a>
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

<a id="4b1b3c55f106b869"></a>
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

Database를 생성할 때 적용되는 속성으로 OCTETS나 CHARACTERS 중 하나의 값을 설정할 수 있다. OCTETS는 byte 수를 의미하고 CHARACTERS는 문자의 개수를 의미한다.

> SQL 표준은 기본값을 CHARACTERS로 정의하고 있으며 타 DBMS 들의 char length unit 기본값은 다음과 같다.
> 
> - Oracle과 DB2는 OCTETS를 사용한다. 
> - MS-SQL, MySQL, PostgreSQL는 CHARACTERS를 사용한다.
> 

<a id="38891a7d14cc44ed"></a>
## CHARACTER_SET

<a id="ce35f18e04485a43"></a>
### 기본 정보

<a id="dffdeca984592dd6"></a>
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

<a id="6e8649106bc895c8"></a>
### 설명

Database의 character set이다.  
Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값을 설정할 수 있다.

<a id="caa7dfc690d07a19"></a>
| Character set | 설명 |
| --- | --- |
| SQL_ASCII | ASCII standard |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standard |

<a id="c1cc98de4afe8d8a"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="a7b7b30ea8785463"></a>
### 기본 정보

<a id="089d1172f9961401"></a>
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

<a id="7bc26ef62a8a8421"></a>
### 설명

C/S dedicate 환경에서 client가 접속을 강제로 종료했을 경우, 이를 검사하는 주기이다. Dedicate server (gserver)가 socket을 확인하여 끊어졌으면 종료한다. 기본값은 1,000 millisecond (1초)이다.

<a id="64b94d60fb8b7d36"></a>
## CHECKPOINT_LIST_COUNT_PER_IO_GROUP

<a id="4833b148b4477fec"></a>
### 기본 정보

<a id="9019dd9438cb057b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHECKPOINT_LIST_COUNT_PER_IO_GROUP |
| 요약 | number of checkpoint lists per each io group |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 8192 |
| 기본값 | 0 |

<a id="f2bf0496a27e541b"></a>
### 설명

[PARALLEL_IO_FACTOR](#471ad4dfae4507b6)에 의해 설정된 각 IO slave가 처리할 체크포인트 목록의 개수를 설정한다. 갱신된 페이지를 체크포인트 목록에 연결할 때 동시성을 효율적으로 처리하기 위해 적정한 값을 지정한다. 기본값은 0인데 이 경우 각 IO slave마다 CPU 개수만큼의 체크포인트 목록을 생성하여 처리한다.

<a id="815bf970bdbf5bc0"></a>
## CLIENT_MAX_COUNT

<a id="4cb5aca6af1a91ae"></a>
### 기본 정보

<a id="9b06d8bc1cb6a6ab"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLIENT_MAX_COUNT |
| 요약 | Maximum Session Count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 12 |
| MAX | 65535 |
| 기본값 | 128 |

<a id="e049ee1542e2c78b"></a>
### 설명

접속할 수 있는 세션의 최대 개수를 설정한다.

<a id="81617cb2623fa706"></a>
## CLIENT_NUMA_POLICY

<a id="4c20717806568786"></a>
### 기본 정보

<a id="80f6390082a258d4"></a>
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

<a id="8db95e11885bfbda"></a>
### 설명

Client 프로세스들을 NUMA 노드들에 분배하기 위한 정책을 결정한다. CLIENT_NUMA_POLICY 프로퍼티는 NUMA 프로퍼티가 on 되어있을 때 동작한다.

- 0: 세션 ID를 모듈러 (modular)해서 연결할 NUMA 노드를 결정한다.
- 1: 통계정보를 바탕으로 가장 조금 연결되어 있는 NUMA 노드에 우선적으로 연결한다.
- 2: C/S client는 TCP_CLIENT_NUMA_NODE 프로퍼티에 의해서 결정되고, D/A client는 DA_CLIENT_ NUMA_NODE 프로퍼티에 의해서 결정된다.

<a id="2ca8dd9c63eef2dd"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="07c6a4a3e6f1ef79"></a>
### 기본 정보

<a id="3e8fd30d79b1ac5b"></a>
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

<a id="ecda0c55ca6bfd18"></a>
### 설명

매 실행 마지막에 PSM의 child 구문을 close 한다.

<a id="ed077bb903e171b4"></a>
## CLUSTER_ASYNC_COMMIT

<a id="79c18fee3ea04633"></a>
### 기본 정보

<a id="4050058d79b2c2be"></a>
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

<a id="a453d5a1a6982235"></a>
### 설명

Cluster system에서 내부적으로 commit protocol을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 commit을 비동기 처리하기 때문에 일시적으로 노드별 consistency가 깨어질 수 있다. 반면에 이 프로퍼티가 꺼져 있으면 commit 할 때마다 동기화하기 때문에 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="82b5f4147f7f8b3c"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="146b5f43f7b8cd25"></a>
### 기본 정보

<a id="5fe7e27fc5346c8d"></a>
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

<a id="6c82e0dc56f33d83"></a>
### 설명

Cluster의 communication buffer 크기이다.

<a id="ab85dae9755c9048"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="7665ccc66afb4885"></a>
### 기본 정보

<a id="a13cbefa6a7c523e"></a>
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

<a id="5d4f0543831e6e0f"></a>
### 설명

Communication read block의 크기이다.

<a id="d228d737f7944d63"></a>
## CLUSTER_COMMIT_SLAVE_CSERVERS

<a id="fc5d27f7dfd2bc53"></a>
### 기본 정보

<a id="ca5d56d2648ea861"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_COMMIT_SLAVE_CSERVERS |
| 요약 | number of commit slave cservers |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 8 |
| 기본값 | 0 |

<a id="7abfe1f2aa8d763e"></a>
### 설명

Commit slave의 개수이다.

<a id="cbd72b790bfa150b"></a>
### ALIAS

<a id="61853905252d2224"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_COMMIT_SLAVE_CSERVERS |
| ALIAS | CLUSTER_COMMIT_SLAVES |

<a id="ff54b0ae4b7738a6"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="1fe5ee14ccb344d5"></a>
### 기본 정보

<a id="cb79cd2dee67a40a"></a>
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

<a id="bdd254a895daa3a7"></a>
### 설명

Cluster system에서 내부적으로 commit 처리 흐름을 다른 protocol 처리와 분리하여 수행할 것인지 여부를 설정한다. 시스템 환경에 따라 commit 처리를 분리할 경우 성능이 향상될 수 있다.

<a id="268a248a0897a191"></a>
## CLUSTER_CONNECTION

<a id="26c44f550dbef89e"></a>
### 기본 정보

<a id="2eab72e0c0efeb0e"></a>
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
| 기본값 | 0 : socket |

<a id="2014475d5a766585"></a>
### 설명

Cluster의 connection mode이다. (socket: 0, rdma:1)

<a id="9e1e902620c502c0"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="1568c772cb36e6d2"></a>
### 기본 정보

<a id="88025fe7b09e68b4"></a>
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
| 기본값 | 10 |

<a id="0de904dcb54ec012"></a>
### 설명

Cluster의 connection timeout 이다.

<a id="6889a8f121d57c22"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="b48c2003c561c3b7"></a>
### 기본 정보

<a id="479121ca7081f20f"></a>
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

<a id="0ac3b8d0acc9aa2b"></a>
### 설명

Data synchronization server의 개수이다.

<a id="681ba2aad2ad2199"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="a83ecb8fe3696cf1"></a>
### 기본 정보

<a id="16850b7fba5cd89e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_DEADLOCK_TIMEOUT |
| 요약 | a time limit (sec) for resolving cluster deadlock |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 3600 (1 hour) |
| 기본값 | 3600 (1 hour) |

<a id="60172f5bfda334cd"></a>
### 설명

Lockable cluster server 부족 등으로 인해 cluster server를 점유하려는 경합이 심해지면 cluster deadlock이 발생할 수 있다. Cluster deadlock이 발생하면 이 프로퍼티에 설정된 시간만큼 deadlock이 해결되기를 기다리는데 해결되지 않을 경우에는 CLUSTER_DEADLOCK_TIMEOUT 에러가 발생한다.

<a id="4852d4ec952eae91"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="ce2b52514bb36c3b"></a>
### 기본 정보

<a id="8e81b9cf4ed43571"></a>
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

<a id="9fdcc72131cff449"></a>
### 설명

Cluster dispatcher in-queue의 크기이다.

<a id="e061aa3147d95181"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="1263ebee111b18f1"></a>
### 기본 정보

<a id="a9efb693b374e460"></a>
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
| 기본값 | 'x' : no binding |

<a id="f830b87890bc57c4"></a>
### 설명

Cluster 디스패처들이 연결될 NUMA 노드를 결정한다. CLUSTER_DISPATCHER_NUMA_STREAM_MAP 프로퍼티는 NUMA 프로퍼티가 on되어 있을 때 동작한다.

> 만약 CLUSTER_COMMIT_STREAM_ISOLATION 프로퍼티가 on 되어 있다면 0번 스트림은 commit stream의 NUMA 노드로 설정된다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고 1번 스트림은 NUMA 노드 1번에 연결하며 2번 스트림은 NUMA 노드 2번에 연결한다.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="6036a0118dc578ba"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="feef6f948549e3d8"></a>
### 기본 정보

<a id="ab431dad5e858e0b"></a>
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

<a id="66ad4839a8004e4f"></a>
### 설명

Cluster dispatcher의 out-queue 크기이다.

<a id="540a7313e72f614b"></a>
## CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE

<a id="10fb57ff101b1df1"></a>
### 기본 정보

<a id="c66d8f5e1ef954bf"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| 요약 | response queue size for cluster server |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 30 |
| MAX | 32768 |
| 기본값 | 30 |

<a id="e34e5f05987203f6"></a>
### 설명

원격 서버로부터 응답을 받기 위한 queue의 최대 크기를 설정한다.

<a id="bfd8bc5310a1df11"></a>
### ALIAS

<a id="e0ba99b9f1a8370c"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| ALIAS | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |

<a id="80a285fcfe6a5faf"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="bb40a390033c5d2b"></a>
### 기본 정보

<a id="de7dddfcc2e37f6a"></a>
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

<a id="3b269393a6069f13"></a>
### 설명

Cluster의 상태를 점검하는 주기 (초)이다. 0은 비활성화 상태를 의미한다.

<a id="7ca2a7293d299f4c"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="3d198b61edfed9ff"></a>
### 기본 정보

<a id="73c6c621a27cbafb"></a>
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

<a id="a9a1b2972c264870"></a>
### 설명

Cluster 상태 점검을 다시 시도하는 횟수이다.

<a id="71cd315130709014"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="8a84e64bf30eeac8"></a>
### 기본 정보

<a id="338e35c72a7694e4"></a>
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

<a id="29788c6e30847985"></a>
### 설명

Cluster의 in-active 멤버를 무시한다.

<a id="13bc96509e4cab50"></a>
## CLUSTER_KEEPALIVE_IDLE_TIME

<a id="597e089bfe76853c"></a>
### 기본 정보

<a id="5d3fb915b4c5d87f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_KEEPALIVE_IDLE_TIME |
| 요약 | The number of seconds a cluster connection needs to be idle |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 16383 |
| 기본값 | 0 |

<a id="01ee2e4022074d58"></a>
### 설명

Keep alive packet을 송신하기 전에 cluster session과 cdispatcher 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, CLUSTER_KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 cdispatcher 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

기본값은 0 이며, 이 경우 keep alive 기능을 사용하지 않는다.

<a id="3fa9eef22b15e015"></a>
## CLUSTER_LOCKABLE_CSERVERS

<a id="b6f5641d26fdb799"></a>
### 기본 정보

<a id="5d6668b7378852a6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_LOCKABLE_CSERVERS |
| 요약 | number of lockable cserver processes |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="76661b66c1d2fa3e"></a>
### 설명

Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수는 [CLUSTER_LOCKLESS_CSERVERS](#531e53de52255f11)로 설정한다.

<a id="ace0153d7f785395"></a>
### ALIAS

<a id="ce3ba49e9e92907d"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_LOCKABLE_CSERVERS |
| ALIAS | CSERVERS |

<a id="531e53de52255f11"></a>
## CLUSTER_LOCKLESS_CSERVERS

<a id="d96125a493aef6a0"></a>
### 기본 정보

<a id="bbc9cb7ccde3e76d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_LOCKLESS_CSERVERS |
| 요약 | number of lockless cserver processes |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="6bf0a6562f8d1702"></a>
### 설명

Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수는 [CLUSTER_LOCKABLE_CSERVERS](#3fa9eef22b15e015)로 설정한다.

<a id="a392d41e0af1db26"></a>
### ALIAS

<a id="07c1d2bdc26986bc"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_LOCKLESS_CSERVERS |
| ALIAS | LOCKLESS_CSERVERS |

<a id="d234ce4cb6ada97a"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="5cf9054c1396a3cd"></a>
### 기본 정보

<a id="ac0163151f66d366"></a>
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

<a id="c342301cd242ce1a"></a>
### 설명

원격 프로토콜이 한 번에 전송할 수 있는 패킷의 최대 크기를 결정한다. 원격으로 전송해야 하는 column의 크기가 CLUSTER_MAX_PACKET_SIZE 프로퍼티 크기를 초과할 경우, 해당 프로퍼티를 column 크기보다 크게 설정해야 한다.

<a id="f9a29c06a6a9ef47"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="14951e3951760bdb"></a>
### 기본 정보

<a id="c3036becd948e186"></a>
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

<a id="f6da06d4bef0d446"></a>
### 설명

원격으로 전송되는 클러스터 패킷은 여러 개의 piece로 나뉘어 전달될 수 있는데 CLUSTER_MAX_PAYLOAD_SIZE 프로퍼티는 하나의 piece에 저장할 수 있는 데이터의 최대 크기를 설정한다.

<a id="1d4ad079bc3596a6"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="f2fa61c33b1d74c0"></a>
### 기본 정보

<a id="4fbd3838adf10c30"></a>
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

<a id="7be9b986dbb71c90"></a>
### 설명

Cluster 패킷 구성에 필요한 메모리를 할당할 때 기다릴 수 있는 최대 시간 (초)을 설정한다.

<a id="20e9e2272ceec3a7"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="1950fb3cc17b8844"></a>
### 기본 정보

<a id="87e51a79d34064d0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT |
| 요약 | a time limit of failover policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="8bbafc424a51ade1"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Failover 시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, session을 종료시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#b47715248d4067f3) property를 사용하여 제한 시간을 설정한다.

<a id="b47715248d4067f3"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="37200ce50950c164"></a>
### 기본 정보

<a id="b99392a6005af7c1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT |
| 요약 | a time limit of session fatal policy to wait for a response from the cluster protocol |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="93e5e8bef98ebba5"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Session을 종료시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, failover 시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#20e9e2272ceec3a7) property를 사용하여 제한 시간을 설정한다.

<a id="a5335cd87bc0bd43"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="7374af0cfa83cd21"></a>
### 기본 정보

<a id="a71eee4d71041530"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_SESSION_HASH_BUCKETS |
| 요약 | Number of hash buckets for cluster sessions |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 127 |
| MAX | 1073741824 |
| 기본값 | 127 |

<a id="a571b8081ebceef5"></a>
### 설명

Cluster session을 관리하기 위한 hash bucket의 개수를 설정한다.

<a id="5952b20d977ac530"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="ffb1cb3bbeba4ff0"></a>
### 기본 정보

<a id="231a119535f60557"></a>
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

<a id="d1a8f4544bafe63a"></a>
### 설명

Cluster system에서 split-brain 상황을 해결하기 위한 정책을 설정한다. 1 이상의 값으로 설정할 경우 해결 방안을 locator에게 질의한다.

> Locator에게 한 질의에 timeout이 발생하면 CLUSTER_SPLIT_BRAIN_RETRY_COUNT만큼 질의를 시도한다. 재시도에 실패하면 속성값이 1인 경우에는 failover를 강제로 진행하고 속성값이 2인 경우에는 fatal 종료한다.

<a id="f9b740dd4e63870e"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="bda8d5f47222ef12"></a>
### 기본 정보

<a id="5b4e49c78225d74b"></a>
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
| 기본값 | 1 |

<a id="b02c1c2d57ad56ec"></a>
### 설명

Cluster system에서 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 이상으로 설정되었을 경우에 사용된다. Locator에게 보낸 질의에 응답이 없을 경우, 질의를 다시 시도하는 횟수를 설정한다.

<a id="902f61f8d96a3706"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="54de418c92ae9918"></a>
### 기본 정보

<a id="c956081e6a376346"></a>
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

<a id="6618e765a4b5eaaf"></a>
### 설명

Commit cserver가 commit protocol 메시지를 읽기 위해 deque 할 때 busy waiting의 기준 시간 간격을 설정한다. 만약 1000000 (1초)로 설정할 경우, 이전 deque에 성공한 이후 다시 deque를 시도할 때까지 1 초를 경과하지 않았다면 deque에서의 대기시간 (timeout)을 0으로 설정하여 busy waiting 한다.

<a id="c60de01978dc482f"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="25cb6e3322a88a7a"></a>
### 기본 정보

<a id="c6a54bc07bf5008c"></a>
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

<a id="4e608fa86d8751c5"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화해야 하는데 이 때 각 control file이 저장될 디렉토리와 파일 이름을 설정한다.

<a id="bc411bac9d6e9a57"></a>
## CONTROL_FILE_COUNT

<a id="1d7be977ef9a60f7"></a>
### 기본 정보

<a id="cd9eb82db90ca499"></a>
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

<a id="a9ca56f50cbd7f44"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화한다. CONTROL_FILE_COUNT는 control file의 다중화 개수를 설정하며 최소 두 개에서 최대 여덟 개까지 다중화할 수 있다.

<a id="6d388580b59e4bde"></a>
## CONTROL_FILE_TEMP_NAME

<a id="4cce9ef804c11234"></a>
### 기본 정보

<a id="01b3ae82448d7c85"></a>
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

<a id="c0e05d0207c0504b"></a>
### 설명

Database를 운용하는 중에 control file은 수시로 변경되고 필요할 경우 임시로 복사본을 만들 수도 있다. CONTROL_FILE_TEMP_NAME은 control file이 임시로 저장되는 디렉토리와 파일 이름을 설정한다.

<a id="bf981a50d28bafa0"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="28c55b22c21fb716"></a>
### 기본 정보

<a id="f391ffe53a463eb7"></a>
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

<a id="8cb0448864a85d0c"></a>
### 설명

조정자 (coordinator)에 적용되는 commit write mode 이다. 만약 TRANSACTION_COMMIT_WRITE_MODE가 "no wait"이고 해당 프로퍼티가 "wait" 인 경우라면 조정자 노드는 "wait"으로 동작하고 그 외 노드들은 "no wait"으로 동작한다.

<a id="a9467bcb7ee6c10c"></a>
## DA_CLIENT_NUMA_NODE

<a id="9e58da611fa63cca"></a>
### 기본 정보

<a id="05823e3710b39301"></a>
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

<a id="8fe807acc6c3207b"></a>
### 설명

Direct Access (D/A) 세션이 바인드 될 NUMA 노드 ID를 설정한다. DA_CLIENT_NUMA_NODE는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="96180655986b8b03"></a>
## DATA_STORE_MODE

<a id="79d97e11f6609a89"></a>
### 기본 정보

<a id="8397a656de0702b5"></a>
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

<a id="544edeac7a294756"></a>
### 설명

Database의 저장 방식을 설정한다.

- 1: CDS 모드는 다중 사용자에 대한 동시성은 지원하지만 영속성은 보장하지 않는다. 즉, data 삽입/ 삭제/ 갱신을 비롯하여 database를 변경하는 모든 연산에 대한 로그를 기록하지 않기 때문에 장애가 발생할 경우 복구할 수도 없다.
- 2: TDS 모드는 다중 사용자에 대한 동시성 및 로그를 이용한 영속성을 보장한다.

<a id="354f9a42121e023d"></a>
## DATABASE_INSTANCE_NAME

<a id="d63c97770396a7dc"></a>
### 기본 정보

<a id="de0e8c8068a20194"></a>
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

<a id="61d638b32698f7e5"></a>
### 설명

데이터베이스의 instance 이름이다.

<a id="ef2e2169108dac16"></a>
## DDL_AUTOCOMMIT

<a id="b329ef44230f9d37"></a>
### 기본 정보

<a id="bf73d334232443ed"></a>
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

<a id="c8c68ffaf779d795"></a>
### 설명

Autocommit이 적용되지 않는 DDL에 대한 autocommit 여부를 설정한다. 예를 들어, table의 생성과 변경에는 autocommit이 적용되지 않기 때문에 DDL_AUTOCOMMIT이 '0'인 경우 rollback을 수행하여 table 생성과 변경을 철회할 수 있다. 이에 반해 DDL_AUTOCOMMIT을 '1'로 설정하면 autocommit이 적용되지 않는 DDL들이 즉시 commit 된다.

<a id="929934270e7cc773"></a>
## DDL_LOCK_TIMEOUT

<a id="a3c2a9106665ebdd"></a>
### 기본 정보

<a id="a5113ceecb292eb6"></a>
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

<a id="366cd66ea04b8120"></a>
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

<a id="e61019b8a53ad4d1"></a>
## DEADLOCK_PRIORITY

<a id="bfdb2efe04587a0e"></a>
### 기본 정보

<a id="2ff10b72396023f7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEADLOCK_PRIORITY |
| 요약 | importance to choose deadlock victim |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 9 |
| 기본값 | 5 |

<a id="c92d17ccf0875bf0"></a>
### 설명

다수의 트랜잭션을 동시에 수행하다가 deadlock이 발생할 경우, deadlock을 유발한 트랜잭션들 중에서 weight 값이 낮은 트랜잭션을 victim으로 선택하여 deadlock을 해결한다. 이 속성값이 상대적으로 높은 세션에서 시작된 트랜잭션과, 이 속성값이 더 낮은 세션에서 시작된 트랜잭션 사이에서 deadlock이 발생하면, 이 속성값이 더 낮은쪽 트랜잭션이 deadlock victim으로 선택된다. Deadlock이 발생했을 때 어느 트랜잭션을 우선적으로 처리할 것인가에 따라 이 속성값을 설정해야 한다.

이 속성값을 설정한 후에 트랜잭션을 시작해야 이 값이 해당 트랜잭션의 weight으로 적용되며, 트랜잭션이 시작된 후에는 이 값을 변경하더라도 트랜잭션의 weight는 변경되지 않음에 유의해야 한다.

<a id="b6388dd75d11789a"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="b759779fedb0666e"></a>
### 기본 정보

<a id="3180822101c64fe9"></a>
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

<a id="f88cd64fc430300e"></a>
### 설명

Cluster system에서 테이블을 생성할 때 global secondary index를 생성할지 여부를 설정한다. Global secondary index를 생성하지 않은 테이블에 대한 non-deterministic 질의는 실패한다. NO로 설정한 상태에서 테이블을 생성한 후에 별도로 global secondary index를 생성할 수도 있다.

<a id="47e868a612cf06ef"></a>
## DEFAULT_INDEX_LOGGING

> 3.2 이후로 지원하지 않는다.

<a id="783bdd9d901f1369"></a>
### 기본 정보

<a id="d071ef2caf91b4a4"></a>
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

<a id="c49cd3e432ccabf4"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 LOGGING 속성을 지정하지 않은 경우, LOGGING 속성은 DEFAULT_INDEX_LOGGING 프로퍼티 값으로 설정된다. 만약 인덱스가 LOGGING 테이블스페이스에 생성되면 반드시 LOGGING 속성이 설정되어야 한다.

<a id="27b5f38a51f795ff"></a>
## DEFAULT_INDEX_PCTFREE

<a id="675539a20ea4e296"></a>
### 기본 정보

<a id="ef7a2fd1c88496e6"></a>
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
| 기본값 | 10 |

<a id="771582ca1c80d7c0"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_INDEX_PCTFREE 프로퍼티 값으로 설정된다.

<a id="32bfc27020e800b7"></a>
## DEFAULT_INITRANS

<a id="d88239cdcccbadbc"></a>
### 기본 정보

<a id="277386e72da27f5d"></a>
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

<a id="223bf1cfa6b440fb"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 INITRANS 구문을 지정하지 않은 경우 INITRANS는 DEFAULT_INITRANS 프로퍼티 값으로 설정된다.

<a id="2234f2bb86cf064c"></a>
## DEFAULT_MAXTRANS

<a id="34b1267775ac2cc8"></a>
### 기본 정보

<a id="5d554f244b8beebd"></a>
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
| 기본값 | 32 |

<a id="698cb63587a2abb5"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 MAXTRANS 구문을 지정하지 않은 경우 MAXTRANS는 DEFAULT_MAXTRANS 프로퍼티 값으로 설정된다.

<a id="d23ff70a89f76cca"></a>
## DEFAULT_PCTFREE

<a id="b55b594e3b7e0b4a"></a>
### 기본 정보

<a id="cdcd2de69db1b238"></a>
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

<a id="002840d051415c8c"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_PCTFREE 프로퍼티 값으로 설정된다.

<a id="80e54870150f426f"></a>
## DEFAULT_PCTUSED

<a id="b70cd1dd776ed198"></a>
### 기본 정보

<a id="963df2b87d40c65f"></a>
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

<a id="fdc46d76407eeefd"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTUSED 구문을 지정하지 않은 경우 PCTUSED는 DEFAULT_PCTUSED 프로퍼티 값으로 설정된다.

<a id="ac3e0ee6c1b6755e"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="8668c65b4b131301"></a>
### 기본 정보

<a id="db75d47b4e5b397e"></a>
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

<a id="947bf0ec20207226"></a>
### 설명

백업 목록을 삭제할 때 백업 파일을 삭제할지 여부를 지정한다.

<a id="da41d7862cb4fbb4"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="aaa0908d8236c1d0"></a>
### 기본 정보

<a id="9475f3488d5b06c8"></a>
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

<a id="d1b5a723b07926d0"></a>
### 설명

INCREMENTAL BACKUP을 수행할 때 obsolete 된 이전 백업 목록의 삭제 여부를 설정한다.

<a id="e967b037fd858e4a"></a>
## DEFAULT_SHARDING

<a id="b4f0da7f083d2d3e"></a>
### 기본 정보

<a id="90dc0f466ac2131d"></a>
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

<a id="6c8534253e13bb6a"></a>
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

DEFAULT_SHARDING 값이 1 (hash sharding) 이고 &lt;table sharding strategy&gt;를 기술하지 않은 경우 다음과 같은 순서로 hash sharding key를 결정한다.

1. PRIMARY KEY 제약 조건을 정의한 경우, primary key를 sharding key로 사용한다.

- 원본

CREATE TABLE t1 ( id INTEGER PRIMARY KEY, name VARCHAR(128) );

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

<a id="3e43dc6b31373561"></a>
## DISABLE_DDL

<a id="137c7d0a4457e2bb"></a>
### 기본 정보

<a id="ea324b9c64e0ee1d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISABLE_DDL |
| 요약 | disable All DDL |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="97ee1b055215ff81"></a>
### 설명

모든 DDL 수행을 금지한다.

DISABLE_DDL의 적용을 받는 SQL 구문은 다음과 같이 조회한다.

```
gSQL>
SELECT command
  FROM v$sql_command
 WHERE is_ddl = 'YES'
 ORDER BY 1
;

COMMAND                                                  
---------------------------------------------------------
ALTER AUDIT POLICY                                       
ALTER CLUSTER GROUP .. ADD CLUSTER MEMBER                
ALTER CLUSTER GROUP .. OFFLINE CLUSTER MEMBER            
ALTER DATABASE ADD LOGFILE GROUP                         
ALTER DATABASE ADD LOGFILE MEMBER                        
ALTER DATABASE ARCHIVELOG                                
ALTER DATABASE CLEAR PASSWORD HISTORY                    
ALTER DATABASE DATAFILE AUTOEXTEND ..                    
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS             
ALTER DATABASE DROP LOGFILE GROUP                        
ALTER DATABASE DROP LOGFILE MEMBER                       
ALTER DATABASE NOARCHIVELOG                              
ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS          
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE         
ALTER DATABASE RENAME LOGFILE                            
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                
ALTER FUNCTION                                           
ALTER INDEX .. REBUILD                                   
ALTER INDEX .. RENAME                                    
ALTER INDEX .. STORAGE                                   
ALTER INDEX AGING                                        
ALTER PACKAGE                                            
ALTER PROCEDURE                                          
ALTER PROFILE                                            
ALTER SEQUENCE                                           
ALTER SEQUENCE .. SYNCHRONIZE                            
ALTER SYSTEM SWITCH LOGFILE                              
ALTER TABLE .. ADD COLUMN                                
ALTER TABLE .. ADD CONSTRAINT                            
ALTER TABLE .. ADD GLOBAL SECONDARY INDEX                
ALTER TABLE .. ADD SUPPLEMENTAL LOG                      
ALTER TABLE .. ALTER COLUMN .. AS IDENTITY               
ALTER TABLE .. ALTER COLUMN .. DROP DEFAULT              
ALTER TABLE .. ALTER COLUMN .. DROP IDENTITY             
ALTER TABLE .. ALTER COLUMN .. DROP NOT NULL             
ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE             
ALTER TABLE .. ALTER COLUMN .. SET DEFAULT               
ALTER TABLE .. ALTER COLUMN .. SET NOT NULL              
ALTER TABLE .. ALTER CONSTRAINT                          
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX              
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX AGING        
ALTER TABLE .. DROP CONSTRAINT                           
ALTER TABLE .. DROP GLOBAL SECONDARY INDEX               
ALTER TABLE .. DROP OFFLINE SEGMENTS                     
ALTER TABLE .. DROP SUPPLEMENTAL LOG                     
ALTER TABLE .. MERGE SHARDS .. INTO ..                   
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..         
ALTER TABLE .. READ ONLY                                 
ALTER TABLE .. READ WRITE                                
ALTER TABLE .. REBALANCE ..                              
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX            
ALTER TABLE .. RENAME COLUMN                             
ALTER TABLE .. RENAME CONSTRAINT                         
ALTER TABLE .. RENAME SHARD .. TO ..                     
ALTER TABLE .. RENAME TO ..                              
ALTER TABLE .. SET UNUSED COLUMN                         
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP ..
ALTER TABLE .. STORAGE                                   
ALTER TABLE .. SYNCHRONIZE ..                            
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN               
ALTER TABLESPACE .. ADD                                  
ALTER TABLESPACE .. DROP                                 
ALTER TABLESPACE .. OFFLINE                              
ALTER TABLESPACE .. ONLINE                               
ALTER TABLESPACE .. RENAME TO                            
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }         
ALTER USER                                               
ALTER USER .. IDENTIFIED BY                              
ALTER VIEW                                               
ANALYZE SYSTEM COMPUTE STATISTICS                        
ANALYZE SYSTEM DELETE STATISTICS                         
ANALYZE TABLE .. DELETE STATISTICS                       
ANALYZE TABLE .. [COMPUTE|ESTIMATE] STATISTICS           
AUDIT POLICY                                             
COMMENT ON .. IS                                         
CREATE AUDIT POLICY                                      
CREATE CLUSTER GROUP                                     
CREATE FUNCTION                                          
CREATE INDEX                                             
CREATE PACKAGE                                           
CREATE PACKAGE BODY                                      
CREATE PROCEDURE                                         
CREATE PROFILE                                           
CREATE SCHEMA                                            
CREATE SEQUENCE                                          
CREATE SYNONYM                                           
CREATE TABLE                                             
CREATE TABLE ... AS SELECT                               
CREATE TABLESPACE                                        
CREATE USER                                              
CREATE VIEW                                              
DROP AUDIT POLICY                                        
DROP CLUSTER GROUP                                       
DROP FUNCTION                                            
DROP INDEX                                               
DROP PACKAGE                                             
DROP PROCEDURE                                           
DROP PROFILE                                             
DROP SCHEMA                                              
DROP SEQUENCE                                            
DROP SYNONYM                                             
DROP TABLE                                               
DROP TABLESPACE                                          
DROP USER                                                
DROP VIEW                                                
FLASHBACK TABLE                                          
GRANT .. ON DATABASE                                     
GRANT .. ON PACKAGE                                      
GRANT .. ON PROCEDURE                                    
GRANT .. ON SCHEMA                                       
GRANT .. ON TABLE                                        
GRANT .. ON TABLESPACE                                   
GRANT USAGE ON ..                                        
NOAUDIT POLICY                                           
PURGE CONSTRAINT                                         
PURGE DBA_RECYCLEBIN                                     
PURGE INDEX                                              
PURGE RECYCLEBIN                                         
PURGE TABLE                                              
PURGE TABLESPACE                                         
REVOKE .. ON DATABASE                                    
REVOKE .. ON PACKAGE                                     
REVOKE .. ON PROCEDURE                                   
REVOKE .. ON SCHEMA                                      
REVOKE .. ON TABLE                                       
REVOKE .. ON TABLESPACE                                  
REVOKE USAGE ON ..                                       
TRUNCATE TABLE                                           

128 rows selected.
```

<a id="be3c0447764c3bfb"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="a94c02f7e822669a"></a>
### 기본 정보

<a id="e1cf1ed8373743be"></a>
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

<a id="ef9e904ebe2b90dc"></a>
### 설명

CDC의 give up에 영향을 미치는 supplemental log 대상 테이블에 대한 DDL 수행을 금지한다.  
관련 DDL은 [DDL 구문에 따른 give up 발생 및 절차에 따른 허용 여부](../part-07-replication/50-cyclone.md#aeeaad848e48138c)를 참조한다.

<a id="05573d9dab7732e0"></a>
## DISABLE_SERIAL_DDL

<a id="b3127e3343f5d864"></a>
### 기본 정보

<a id="533305c5b463f675"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DISABLE_SERIAL_DDL |
| 요약 | disable Serial DDL |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="8caff37891206fef"></a>
### 설명

Cluster 환경에서 DDL은 [Cluster의 DDL 처리](../part-03-sql-manual/12-sql-languages.md#284f96e2eecfe9fc)에 설명된 것처럼 모든 cluster member 들을 순차적으로 lock을 획득한 후 수행한다.    
이와 같이 serial lock 방식으로 수행하는 DDL을 serial DDL 이라 한다.

DISABLE_SERIAL_DDL의 적용을 받는 DDL 구문은 다음과 같이 조회하는데, 대부분의 schema DDL이 이에 해당한다.

```
gSQL>
SELECT command
     , is_ddl
     , cluster_lock_mode
  FROM v$sql_command
 WHERE is_ddl = 'YES'
   AND cluster_lock_mode = 'SERIAL'
 ORDER BY 1
;

SELECT command
     , is_ddl
     , cluster_lock_mode
  FROM v$sql_command
 WHERE is_ddl = 'YES'
   AND cluster_lock_mode = 'SERIAL'
 ORDER BY 1
;

COMMAND                                           IS_DDL CLUSTER_LOCK_MODE
------------------------------------------------- ------ -----------------
ALTER AUDIT POLICY                                YES    SERIAL           
ALTER DATABASE CLEAR PASSWORD HISTORY             YES    SERIAL           
ALTER DATABASE DATAFILE AUTOEXTEND ..             YES    SERIAL           
ALTER FUNCTION                                    YES    SERIAL           
ALTER INDEX .. RENAME                             YES    SERIAL           
ALTER INDEX .. STORAGE                            YES    SERIAL           
ALTER INDEX AGING                                 YES    SERIAL           
ALTER PACKAGE                                     YES    SERIAL           
ALTER PROCEDURE                                   YES    SERIAL           
ALTER PROFILE                                     YES    SERIAL           
ALTER SEQUENCE                                    YES    SERIAL           
ALTER TABLE .. ADD COLUMN                         YES    SERIAL           
ALTER TABLE .. ADD CONSTRAINT                     YES    SERIAL           
ALTER TABLE .. ADD GLOBAL SECONDARY INDEX         YES    SERIAL           
ALTER TABLE .. ADD SUPPLEMENTAL LOG               YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. AS IDENTITY        YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP DEFAULT       YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP IDENTITY      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. DROP NOT NULL      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE      YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET DEFAULT        YES    SERIAL           
ALTER TABLE .. ALTER COLUMN .. SET NOT NULL       YES    SERIAL           
ALTER TABLE .. ALTER CONSTRAINT                   YES    SERIAL           
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX       YES    SERIAL           
ALTER TABLE .. ALTER GLOBAL SECONDARY INDEX AGING YES    SERIAL           
ALTER TABLE .. DROP CONSTRAINT                    YES    SERIAL           
ALTER TABLE .. DROP GLOBAL SECONDARY INDEX        YES    SERIAL           
ALTER TABLE .. DROP OFFLINE SEGMENTS              YES    SERIAL           
ALTER TABLE .. DROP SUPPLEMENTAL LOG              YES    SERIAL           
ALTER TABLE .. READ ONLY                          YES    SERIAL           
ALTER TABLE .. READ WRITE                         YES    SERIAL           
ALTER TABLE .. RENAME COLUMN                      YES    SERIAL           
ALTER TABLE .. RENAME CONSTRAINT                  YES    SERIAL           
ALTER TABLE .. RENAME SHARD .. TO ..              YES    SERIAL           
ALTER TABLE .. RENAME TO ..                       YES    SERIAL           
ALTER TABLE .. SET UNUSED COLUMN                  YES    SERIAL           
ALTER TABLE .. STORAGE                            YES    SERIAL           
ALTER TABLESPACE .. ADD                           YES    SERIAL           
ALTER TABLESPACE .. DROP                          YES    SERIAL           
ALTER TABLESPACE .. OFFLINE                       YES    SERIAL           
ALTER TABLESPACE .. ONLINE                        YES    SERIAL           
ALTER TABLESPACE .. RENAME TO                     YES    SERIAL           
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }  YES    SERIAL           
ALTER USER                                        YES    SERIAL           
ALTER USER .. IDENTIFIED BY                       YES    SERIAL           
ALTER VIEW                                        YES    SERIAL           
ANALYZE SYSTEM COMPUTE STATISTICS                 YES    SERIAL           
ANALYZE SYSTEM DELETE STATISTICS                  YES    SERIAL           
ANALYZE TABLE .. DELETE STATISTICS                YES    SERIAL           
ANALYZE TABLE .. [COMPUTE|ESTIMATE] STATISTICS    YES    SERIAL           
AUDIT POLICY                                      YES    SERIAL           
COMMENT ON .. IS                                  YES    SERIAL           
CREATE AUDIT POLICY                               YES    SERIAL           
CREATE FUNCTION                                   YES    SERIAL           
CREATE INDEX                                      YES    SERIAL           
CREATE PACKAGE                                    YES    SERIAL           
CREATE PACKAGE BODY                               YES    SERIAL           
CREATE PROCEDURE                                  YES    SERIAL           
CREATE PROFILE                                    YES    SERIAL           
CREATE SCHEMA                                     YES    SERIAL           
CREATE SEQUENCE                                   YES    SERIAL           
CREATE SYNONYM                                    YES    SERIAL           
CREATE TABLE                                      YES    SERIAL           
CREATE TABLE ... AS SELECT                        YES    SERIAL           
CREATE TABLESPACE                                 YES    SERIAL           
CREATE USER                                       YES    SERIAL           
CREATE VIEW                                       YES    SERIAL           
DROP AUDIT POLICY                                 YES    SERIAL           
DROP FUNCTION                                     YES    SERIAL           
DROP INDEX                                        YES    SERIAL           
DROP PACKAGE                                      YES    SERIAL           
DROP PROCEDURE                                    YES    SERIAL           
DROP PROFILE                                      YES    SERIAL           
DROP SCHEMA                                       YES    SERIAL           
DROP SEQUENCE                                     YES    SERIAL           
DROP SYNONYM                                      YES    SERIAL           
DROP TABLE                                        YES    SERIAL           
DROP TABLESPACE                                   YES    SERIAL           
DROP USER                                         YES    SERIAL           
DROP VIEW                                         YES    SERIAL           
FLASHBACK TABLE                                   YES    SERIAL           
GRANT .. ON DATABASE                              YES    SERIAL           
GRANT .. ON PACKAGE                               YES    SERIAL           
GRANT .. ON PROCEDURE                             YES    SERIAL           
GRANT .. ON SCHEMA                                YES    SERIAL           
GRANT .. ON TABLE                                 YES    SERIAL           
GRANT .. ON TABLESPACE                            YES    SERIAL           
GRANT USAGE ON ..                                 YES    SERIAL           
NOAUDIT POLICY                                    YES    SERIAL           
PURGE CONSTRAINT                                  YES    SERIAL           
PURGE DBA_RECYCLEBIN                              YES    SERIAL           
PURGE INDEX                                       YES    SERIAL           
PURGE RECYCLEBIN                                  YES    SERIAL           
PURGE TABLE                                       YES    SERIAL           
PURGE TABLESPACE                                  YES    SERIAL           
REVOKE .. ON DATABASE                             YES    SERIAL           
REVOKE .. ON PACKAGE                              YES    SERIAL           
REVOKE .. ON PROCEDURE                            YES    SERIAL           
REVOKE .. ON SCHEMA                               YES    SERIAL           
REVOKE .. ON TABLE                                YES    SERIAL           
REVOKE .. ON TABLESPACE                           YES    SERIAL           
REVOKE USAGE ON ..                                YES    SERIAL           
TRUNCATE TABLE                                    YES    SERIAL           

103 rows selected.
```

DISABLE_SERIAL_DDL의 적용을 받지 않는 DDL 구문은 다음과 같이 조회하는데, 대부분의 cluster DDL이 이에 해당한다.

```
gSQL>
SELECT command
     , is_ddl
     , cluster_lock_mode
  FROM v$sql_command
 WHERE is_ddl = 'YES'
   AND cluster_lock_mode <> 'SERIAL'
 ORDER BY 1
;

COMMAND                                                   IS_DDL CLUSTER_LOCK_MODE
--------------------------------------------------------- ------ -----------------
ALTER CLUSTER GROUP .. ADD CLUSTER MEMBER                 YES    MANUAL           
ALTER CLUSTER GROUP .. OFFLINE CLUSTER MEMBER             YES    MANUAL           
ALTER DATABASE ADD LOGFILE GROUP                          YES    NONE             
ALTER DATABASE ADD LOGFILE MEMBER                         YES    NONE             
ALTER DATABASE ARCHIVELOG                                 YES    NONE             
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS              YES    MANUAL           
ALTER DATABASE DROP LOGFILE GROUP                         YES    NONE             
ALTER DATABASE DROP LOGFILE MEMBER                        YES    NONE             
ALTER DATABASE NOARCHIVELOG                               YES    NONE             
ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS           YES    MANUAL           
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE          YES    NONE             
ALTER DATABASE RENAME LOGFILE                             YES    NONE             
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                 YES    NONE             
ALTER INDEX .. REBUILD                                    YES    MANUAL           
ALTER SEQUENCE .. SYNCHRONIZE                             YES    MANUAL           
ALTER SYSTEM SWITCH LOGFILE                               YES    NONE             
ALTER TABLE .. MERGE SHARDS .. INTO ..                    YES    MANUAL           
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..          YES    MANUAL           
ALTER TABLE .. REBALANCE ..                               YES    MANUAL           
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX             YES    MANUAL           
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP .. YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE ..                             YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

25 rows selected.
```

<a id="0fd7ff95d30ddb7c"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="152fd4a21a22ef34"></a>
### 기본 정보

<a id="0bac6caf6366fe34"></a>
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

<a id="7911bd7686e4456b"></a>
### 설명

CDC give up을 유발한 UPDATE primary key를 비활성화 한다.

<a id="a122306b4fd5546b"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="b33ef33e16c89559"></a>
### 기본 정보

<a id="3834fdeec36194a0"></a>
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

<a id="11a22d74bce86010"></a>
### 설명

TARGETTYPE protocol을 허용하지 않는다.

<a id="112bfd058733ad37"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="32e66b9065db556c"></a>
### 기본 정보

<a id="49f28604898ce943"></a>
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

<a id="601cc18dea746f4c"></a>
### 설명

TARGETTYPE_WITH_ALL protocol을 허용하지 않는다.

<a id="be15263a35d355d9"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="0b28478668e5c8e9"></a>
### 기본 정보

<a id="bfa8143280adea0b"></a>
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

<a id="02ec25d3ccf6a744"></a>
### 설명

TARGETTYPE_WITH_NAME protocol을 허용하지 않는다.

<a id="42d313969647fe76"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="c794166234244fc5"></a>
### 기본 정보

<a id="a72b98bba39e2b4e"></a>
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

<a id="e541ad752373e6f3"></a>
### 설명

Shared 모드에서 사용하는 전체 communication buffer 크기로써 Shared Static Area (SSA) 내에 할당되어 사용된다.

<a id="1bc78f9b2aa8ae49"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="c2f525af7291c082"></a>
### 기본 정보

<a id="7f4364106202e24b"></a>
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

<a id="f7ff927def4cecf6"></a>
### 설명

Shared 모드에서 dispatcher가 관리하는 unit의 크기이다. 이 크기가 크면 메모리가 낭비되고 이 크기가 작으면 성능이 저하될 수 있다.  
Shared 모드에서 통신 packet의 최대 크기로 설정된다.

<a id="9acdb0a8cfe0252c"></a>
## DISPATCHER_CONNECTIONS

<a id="f00eb2934f0f8560"></a>
### 기본 정보

<a id="abb5c258923dc6d5"></a>
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

<a id="5eb7c607caa1ced2"></a>
### 설명

Shared 모드에서 하나의 dispatcher가 관리할 수 있는 최대 connection (client)의 개수이다.  
시스템에서 지원하는 최대값이 설정값보다 작으면 내부적으로 시스템 최대값으로 설정된다.

<a id="9e1d086a75e9517a"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="486494d31ca1e291"></a>
### 기본 정보

<a id="f8582081af3fe67b"></a>
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
| MAX | 86400000000 : 1day |
| 기본값 | 100000 : 0.1 second |

<a id="fcf3f7b0a7f9d428"></a>
### 설명

Busy waiting에 대한 dispatcher dequeue 주기이다. (micro second)

<a id="83c660d44edc2321"></a>
## DISPATCHER_LOAD_BALANCING

<a id="bca1ef9b0cf532f1"></a>
### 기본 정보

<a id="5aa6036943196e98"></a>
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

<a id="21599df6375b5492"></a>
### 설명

Shared 모드에서 client에 접속할 때 dispatcher를 할당하는 알고리즘이다.

- 0: 현재 연결된 client 수가 적은 dispatcher에 할당한다.
- 1: 순차적으로 dispatcher에 할당한다.

<a id="21affd4ee265d761"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="bbb6c98d4e5526c0"></a>
### 기본 정보

<a id="67a8cae6ff56e223"></a>
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
| 기본값 | 'x' : no binding |

<a id="af394b3c13814083"></a>
### 설명

디스패처들이 연결될 NUMA 노드를 결정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고, 1번 스트림은 NUMA 노드 1번에 연결하고, 2번 스트림은 NUMA 노드 2번에 연결한다.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="61bd166bb2d97ee4"></a>
## DISPATCHER_QUEUE_SIZE

<a id="e38bd83ee772854f"></a>
### 기본 정보

<a id="6f895afeb3ab07f8"></a>
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

<a id="b045baa6d067be6b"></a>
### 설명

Shared 모드에서 dispatcher와 shared-server 간의 통신을 위한 queue 크기를 설정한다.

<a id="4a8a88311164f65b"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="820e024f7afdd663"></a>
### 기본 정보

<a id="ce0b947c4026a0cf"></a>
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

<a id="1258069cf008e45e"></a>
### 설명

각 response queue의 mini queue 개수이다.

<a id="31e22b104efcb586"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="a6b797daa99e8e49"></a>
### 기본 정보

<a id="edfc7c044c3d9613"></a>
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

<a id="e73d1663df17b136"></a>
### 설명

각 request queue의 mini queue 개수이다.

<a id="74716bc3d9717a20"></a>
## DISPATCHERS

<a id="40f05d772a88e56f"></a>
### 기본 정보

<a id="8ed678748677fa3d"></a>
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

<a id="0ffea69f0ab1e938"></a>
### 설명

Shared 모드를 사용할 때 dispatcher process 개수를 설정한다.  
Open 단계에서는 alter system을 사용하여 값을 줄일 수 없다.

<a id="764193a7a070a155"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="420a72abbb4863eb"></a>
### 기본 정보

<a id="4050f52f441b5862"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY |
| 요약 | execute instant hash table using available memory even if not enough |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="64271918c4d055ad"></a>
### 설명

instant hash table을 사용하는 질의에서 hash bucket을 확장하기 위한 메모리가 부족한 경우 질의를 실패한 것으로 처리할지 아니면 hash bucket을 확장하지 않고 질의를 수행할지 여부를 지정한다.

<a id="f81d28295ac1acab"></a>
## FETCH_FAILOVER

<a id="4b9a94de514daa17"></a>
### 기본 정보

<a id="af52467a768d0247"></a>
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

<a id="47893007fd0b0dcb"></a>
### 설명

Fetch failover를 활성화한다.

<a id="19cf338782b55190"></a>
## FULL_TABLE_SCAN_CACHING_THRESHOLD

<a id="232758cb3ad0f983"></a>
### 기본 정보

<a id="c70d8e0a7aadc837"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | FULL_TABLE_SCAN_CACHING_THRESHOLD |
| 요약 | upper threshold of table size for buffer caching while full scan |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1000 |
| 기본값 | 20 |

<a id="6df42b45c80633fc"></a>
### 설명

디스크 테이블스페이스에 생성된 테이블을 전체 스캔할 때 버퍼 캐쉬에 캐싱할지 여부는 테이블 크기의 threshold에 따라 결정된다. FULL_TABLE_SCAN_CACHING_THRESHOLD는 바로 이 threshold 값을 설정한다. 기본값은 20이며, 이 경우 [BUFFER_CACHE_SIZE](#258d891c7bd4cbf0)의 2.0% 보다 작거나 같은 수의 페이지를 사용 중인 테이블들만 캐싱한다. 이 값이 1000 (100%)이면 전체 스캔을 수행할 때 모든 테이블을 버퍼에 캐싱한다.

예를 들어 BUFFER_CACHE_SIZE 값이 8192이고 FULL_TABLE_SCAN_CACHING_THRESHOLD 값이 509 (50.9%)인 경우, 사용 중인 페이지의 수가 4169 (8192의 50.9%)보다 작거나 같은 테이블들만 전체 스캔 시 버퍼에 캐싱된다.

<a id="3819bf4b99a658fd"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="3f0c543e617c47ed"></a>
### 기본 정보

<a id="ffb1af74bd61bf23"></a>
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

<a id="c834dcf660036594"></a>
### 설명

Global connection에서 session dependent한 정보를 포함한 질의 수행 지원 여부를 설정한다.

<a id="9fe99dd25caad0b9"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="b2d55c537a8a42d4"></a>
### 기본 정보

<a id="1db91061db73996a"></a>
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

<a id="33d1c044f1e7672b"></a>
### 설명

Global journal의 buffer 크기이다.

<a id="0a31b18c64f0d44d"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="49353568827d1de9"></a>
### 기본 정보

<a id="72b15f7baa7d3660"></a>
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

<a id="35db7774c3641776"></a>
### 설명

Global journal buffer의 최대 사이즈의 합이다.

<a id="009d4fab746b1391"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="8be07930dbd33bed"></a>
### 기본 정보

<a id="97668737a58afbd9"></a>
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

<a id="54b954122694fd70"></a>
### 설명

Global property를 변경할 때 동시성을 제어하기 위해 lock 하는데 이 때 해당 lock 하기 위해 대기하는 시간을 설정한다.

<a id="b77fafc1c4feb877"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="caeec81a70e92788"></a>
### 기본 정보

<a id="c55bd80973236922"></a>
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

<a id="aaa02f7a4cedc5e3"></a>
### 설명

Global transaction의 commit write mode를 변경하기 위한 프로퍼티이다. TRANSACTION_COMMIT_ WRITE_MODE는 모든 트랜잭션들에 적용되는 반면에 이 프로퍼티는 global transaction에만 적용된다. 만약 해당 프로퍼티가 2로 설정되면 TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

- 0: no wait
- 1: wait
- 2: TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

<a id="7cd8ecef47732723"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="5153a92eef5a35c5"></a>
### 기본 정보

<a id="577a0a8b5c7fca7d"></a>
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

<a id="92dd7e4b2a8b3591"></a>
### 설명

Transaction이 두 개 이상의 cluster group에 걸쳐 데이터를 변경한 경우 이를 global transaction으로 처리할지 다수의 domain transaction으로 처리할지 결정하는 프로퍼티이다.

- 0: Global tranaction으로 처리
- 1: 다수의 domain transaction으로 처리

> 이 프로퍼티가 1인 경우에는 cluster group마다 독립적인 트랜잭션으로 commit하기 때문에 트랜잭션 원자성 (transaction atomicity)을 보장하지 않는다.

<a id="f9a7f320478dd07a"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="998a367cf4cef852"></a>
### 기본 정보

<a id="354a4a4bc9ec78a2"></a>
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

<a id="e20cf1555c6df34b"></a>
### 설명

Global transaction log의 기본 directory 이다.

<a id="430c6603b9b60f7b"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="619c6c9ce2b7c7e4"></a>
### 기본 정보

<a id="427fd468ddb34b7c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_LOG_FILE_SIZE |
| 요약 | global transaction log file size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20 Mega |
| MAX | 10 Giga |
| 기본값 | 100 Mega |

<a id="d3d0e5f52ee44282"></a>
### 설명

Global transaction log의 file 크기이다.

<a id="0ae78c55ff68bcad"></a>
## GMASTER_NUMA_NODE

<a id="3ea8ec4794836005"></a>
### 기본 정보

<a id="025243ced556bb73"></a>
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

<a id="9bd4a034a1e33982"></a>
### 설명

gmaster 데몬이 사용할 NUMA node의 ID를 설정한다. GMASTER_NUMA_NODE 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="7d58a6afe78df58e"></a>
## GMON_AUTOSTART

<a id="6c4f16880cfdb941"></a>
### 기본 정보

<a id="4a742cca01d63886"></a>
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

<a id="ed755713167edf95"></a>
### 설명

gmon 프로세스를 자동으로 시작시킬지 여부를 설정한다.

<a id="4413c16821b072a7"></a>
## HINT_ERROR

<a id="26feb3277b05a803"></a>
### 기본 정보

<a id="2c8a43532f072b99"></a>
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

<a id="2fee4a8ddc505c36"></a>
### 설명

Hint 구문에 대한 syntax error 및 validation error 체크 여부를 설정한다.

<a id="0e2a57b4fe8e0533"></a>
## IDLE_TIMEOUT

<a id="725168fbfcbe8833"></a>
### 기본 정보

<a id="5818db4d1d1880c4"></a>
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

<a id="ac785451daaa90a9"></a>
### 설명

C/S 세션에서 최대로 대기할 수 있는 IDLE 시간을 설정하며 해당 IDLE 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT이 발생하지 않는다.

<a id="1870bd2415901fa8"></a>
## IN_DOUBT_DECISION

<a id="3c80d96d0e2def49"></a>
### 기본 정보

<a id="753410780a35d628"></a>
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

<a id="cb8508468acd6ffc"></a>
### 설명

분산 트랜잭션의 in-doubt 트랜잭션을 commit 할지 rollback 할지 결정한다.

- 1: Commit
- 2: Rollback

<a id="2b981beaa0427eda"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="50e0d65f0577a52d"></a>
### 기본 정보

<a id="05ec5349581e8321"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | IN_KEY_RANGE_ARRAY_COUNT |
| 요약 | array count for in key range scan |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 20 |

<a id="eb339558b84448ea"></a>
### 설명

Array 기반의 in key range scan을 수행할 수 있는 in key range 대상 value들의 최대 개수이다.

- 다음과 같은 구문에 대해 array 기반 in key range scan을 수행하려면 IN_KEY_RANGE_ARRAY_COUNT가 3 이상이어야 한다.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

IN_KEY_RANGE_ARRAY_COUNT 값보다 in key range 대상 value들의 최대 개수가 더 많은 경우에는 instant table 기반으로 in key range scan을 수행한다.

<a id="13f478ab05d41b23"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="88eabea779d0e650"></a>
### 기본 정보

<a id="aaa91d6bd048255d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE |
| 요약 | number of pages read in one I/O operation during an incremental backup |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 32 |

<a id="b865d7d3759c376e"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 한 번의 디스크 IO로 읽어들일 페이지의 수를 설정한다.

<a id="1a0b0151961245b4"></a>
## INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA

<a id="860dfcb44f1b7bba"></a>
### 기본 정보

<a id="394d87b663b28821"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA |
| 요약 | criteria for the number of flush page count to update datafile header |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 134217728 |
| 기본값 | 134217728 |

<a id="78dec3bc47efd1bb"></a>
### 설명

디스크 테이블스페이스의 데이터 파일 헤더를 갱신하는 기준을 설정한다. IO slave가 버퍼 캐쉬에서 갱신된 페이지를 디스크에 반영하는 동안 설정된 값만큼의 갱신된 페이지를 반영하였을 때 데이터 파일의 헤더에 복구를 시작할 LSN을 설정한다. 이렇게 하면 재시작 복구 시 디스크 IO를 줄일 수 있다.

<a id="c1b0ff41fc5e19a3"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="ae2eaee2936999c2"></a>
### 기본 정보

<a id="f35f02b9aee21c38"></a>
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

<a id="2f955973e0331b54"></a>
### 설명

인덱스를 생성할 때 병렬화 개수 (parallel factor)를 지정한다.

- 0: 시스템의 코어 개수로 지정된다.

<a id="7bf6de118a3fa6de"></a>
## INDEX_LOGGING_THROTTLING

<a id="8bb89c586e3b9207"></a>
### 기본 정보

<a id="9d5004559abb2ee5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_LOGGING_THROTTLING |
| 요약 | The limit on the number of dirty blocks in the log buffer during index building or rebuilding |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| 기본값 | 10737418240 |

<a id="47d0817101ea5b0a"></a>
### 설명

해당 프로퍼티는 인덱스 구축 및 재구축 시 발생하는 대량의 로그로 인해 시스템에 과부하가 걸리는 것을 방지하며 온라인 서비스에 영향을 주지 않기 위해 사용한다.

인덱스 로깅 시 로그 버퍼에 주어진 프로퍼티 값보다 많은 양의 dirty block 이 있으면 dirty block이 디스크로 flush 될 때까지 대기한다.

<a id="1fda90fc5c7d93a9"></a>
## INDEX_MERGE_RUN_COUNT

<a id="c805c849666f9ddf"></a>
### 기본 정보

<a id="a2296ff38888ff96"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_MERGE_RUN_COUNT |
| 요약 | merge run count for memory index |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 64 |
| 기본값 | 32 |

<a id="5d35404fbd87530c"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (INDEX_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. INDEX_MERGE_RUN_COUNT는 한 번에 병합할 정렬된 block들의 개수를 설정한다.

<a id="cf4c0758eb8b6e90"></a>
### ALIAS

<a id="bc71136a01de8c87"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | INDEX_MERGE_RUN_COUNT |
| ALIAS | MEMORY_MERGE_RUN_COUNT |

<a id="33a5c5019d4bc8b5"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="401afce6a2ad9de8"></a>
### 기본 정보

<a id="ab67d58eaa4067d0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_REBUILD_BLOCK_READ_COUNT |
| 요약 | value count for a block read for index rebuild |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 100 |

<a id="aa902d0d34f35c8f"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축 하는 도중에 DML이 수행되면 journal data가 저장된다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal data들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. INDEX_REBUILD_BLOCK_READ_COUNT는 이 과정에서 journal data를 얼마만큼 읽어들여 인덱스에 반영할지를 나타낸다.

<a id="3a3a8e2b59bb5329"></a>
## INDEX_SORT_RUN_SIZE

<a id="598f39281d21f30f"></a>
### 기본 정보

<a id="f6bf1f6ca959fdb6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_SORT_RUN_SIZE |
| 요약 | sort run size for memory index(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8192 |
| MAX | 32768 |
| 기본값 | 8192 |

<a id="733cfd5a0862bd1d"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (INDEX_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. INDEX_SORT_RUN_SIZE는 정렬할 block 한 개의 크기를 설정한다.

<a id="fd6c6d0066b71dc1"></a>
### ALIAS

<a id="31be6f5d9fce389e"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | INDEX_SORT_RUN_SIZE |
| ALIAS | MEMORY_SORT_RUN_SIZE |

<a id="5826cb666a22a0a9"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="d1f6a0a12588e0a6"></a>
### 기본 정보

<a id="fdf4e931f41ed783"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_TREE_MERGE_PARALLEL_FACTOR |
| 요약 | parallel factor for merging sub-trees |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| 기본값 | 0 |

<a id="c76afaaa5e0651a6"></a>
### 설명

인덱스를 생성할 때 sub-tree를 합병하기 위한 병렬화 개수 (parallel factor)를 지정한다. 만약 해당 값이 INDEX_BUILD_PARALLEL_FACTOR 보다 큰 경우에는 INDEX_BUILD_PARALLEL_FACTOR를 사용한다.

- 0: INDEX_BUILD_PARALLEL_FACTOR를 따른다.

<a id="42411aafc9a8e321"></a>
## INST_ALLOCATOR_COUNT

<a id="c3ad2ed81df602fc"></a>
### 기본 정보

<a id="f0ea3d0ce30f4edf"></a>
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

<a id="f1186f0c29bbf8cd"></a>
### 설명

인스턴트 블록을 할당 또는 삭제하는 연산의 병렬성을 높이기 위한 프로퍼티이다.

<a id="097f27d8b9f9ca78"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="57dc7a4b00efbb50"></a>
### 기본 정보

<a id="36eeb6afe0822208"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INST_HASH_TABLE_BUCKET_MAX_COUNT |
| 요약 | instant hash table bucket max count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 4294967295 |
| 기본값 | 0 |

<a id="8a90266af654a216"></a>
### 설명

Hash instant table의 예상 bucket count의 최대값을 설정한다.

<a id="8050dbc0fe761f36"></a>
## INST_TABLE_BLOCK_SIZE

<a id="bf3072cf1f76a7d9"></a>
### 기본 정보

<a id="18f5dc38e9b1c694"></a>
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

<a id="9861f2dfeb3d914d"></a>
### 설명

인스턴트 블록의 크기를 결정한다. 만약 인스턴트 레코드의 고정영역 크기가 인스턴트 블록의 크기를 초과하는 경우 다음과 같은 에러가 발생한다.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="6965649539ce1bea"></a>
## IPC_CHANNEL_COUNT

<a id="6a64d6f7704f5bd4"></a>
### 기본 정보

<a id="5ae953fbf002be39"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | IPC_CHANNEL_COUNT |
| 요약 | IPC Channel Count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 2048 |
| 기본값 | 0 |

<a id="e9429ec4044c04b1"></a>
### 설명

IPC 통신을 위한 채널 개수를 지정한다.

<a id="c59426db08e3a642"></a>
## JOURNAL_TEMP_DIR

<a id="53728b1af984c5bc"></a>
### 기본 정보

<a id="4215e95bdd364b98"></a>
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

<a id="49974bf0cf41d763"></a>
### 설명

Journaling의 임시 디렉토리이다.

<a id="44fdf5fc323476d0"></a>
## KEEPALIVE_IDLE_TIME

<a id="50c3fd60ae79eeb3"></a>
### 기본 정보

<a id="0deaa01e6d018a04"></a>
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

<a id="7ccee8478d35c75f"></a>
### 설명

Keep alive packet을 송신하기 전에 client와 server 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 server 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="f20a51008ddcc37a"></a>
## LOCAL_CLUSTER_MEMBER

<a id="6862c7013f3153aa"></a>
### 기본 정보

<a id="5846fa8ff09e2339"></a>
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

<a id="d3ce7e7e90b14aea"></a>
### 설명

Local cluster member의 이름이다.

<a id="75d07c77fd17d83c"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="b4e3b885988fd2c8"></a>
### 기본 정보

<a id="2b36a3f338685f75"></a>
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

<a id="196ccc6b7c2acb67"></a>
### 설명

Local cluster member의 host 이름이다.

<a id="5729ecd30ff4810c"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="10c876635d77fd94"></a>
### 기본 정보

<a id="b9c7e48109c58319"></a>
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

<a id="e894870cde3ddddd"></a>
### 설명

Local cluster member의 listen port 이다.

<a id="164f7408535661d7"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="33b8c1eb45d7c870"></a>
### 기본 정보

<a id="bb8ef2872425f528"></a>
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

<a id="b11477779511fca1"></a>
### 설명

Local journal buffer의 크기이다.

<a id="97dbdf4a04277ab2"></a>
## LOCATION_FILE

<a id="49632a944fa4c52c"></a>
### 기본 정보

<a id="9e6a7d529d09ad2c"></a>
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

<a id="39e5b455d95d8760"></a>
### 설명

Location file의 이름이다.

<a id="899241c2601698b3"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="d8eb46ad8f2041f9"></a>
### 기본 정보

<a id="040aa797184c3ce2"></a>
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
| 기본값 | 3 |

<a id="c5761a5e38ff9c88"></a>
### 설명

Cluster system이 split-brain 상황에 대한 해결 방안을 locator에게 질의한 후에 응답을 기다리는 시간 (초)을 설정한다. CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY를 1 이상으로 설정했을 때만 사용할 수 있는 프로퍼티이다.

<a id="ec577381c232d110"></a>
## LOCK_HASH_TABLE_SIZE

<a id="9aa4e4a8e151736e"></a>
### 기본 정보

<a id="8a808d25f5a2c199"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCK_HASH_TABLE_SIZE |
| 요약 | lock manager hash table size ( bucket 개수 ) |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 1000000 |
| 기본값 | 65519 |

<a id="04d076c3d1e7a2c0"></a>
### 설명

잠금 관리자 (lock manager)가 관리하는 hash table의 최대 크기를 설정한다.

<a id="eebec07b2adc98c5"></a>
## LOCKABLE_DISPATCHER_CM_BUFFER_COUNT

<a id="b1a30edd2321f59c"></a>
### 기본 정보

<a id="28d330170d44f9b7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCKABLE_DISPATCHER_CM_BUFFER_COUNT |
| 요약 | communication buffer count for lockable dispatcher |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 1 |

<a id="e2877de56c84bed2"></a>
### 설명

Cluster lockable dispatcher의 communication buffer 개수를 지정한다.

<a id="4a41ec8105158e4d"></a>
## LOCKLESS_DISPATCHER_CM_BUFFER_COUNT

<a id="43cc6fa8ad65e258"></a>
### 기본 정보

<a id="b52762bc050863f2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCKLESS_DISPATCHER_CM_BUFFER_COUNT |
| 요약 | communication buffer count for lockless dispatcher |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 1 |

<a id="ac80f24d69fa61dc"></a>
### 설명

Cluster lockless dispatcher의 communication buffer 개수를 지정한다.

<a id="48b6e1eacbccb722"></a>
## LOG_BLOCK_SIZE

<a id="b9d0c509d0f4b856"></a>
### 기본 정보

<a id="0f322d7274e22578"></a>
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

<a id="acc0c324e467ec54"></a>
### 설명

LOG_BLOCK_SIZE는 log buffer가 disk의 log file로 flush 되는 최소 크기이고 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="ff1cd1d615847302"></a>
## LOG_BUFFER_SIZE

<a id="4fb0a5031737fe80"></a>
### 기본 정보

<a id="dfca60d29881b286"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_BUFFER_SIZE |
| 요약 | default log buffer size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1048576 |
| MAX | 10737418240 |
| 기본값 | 10485760 |

<a id="de4bb1de5c5d924d"></a>
### 설명

Database에서 DML 및 DDL 연산을 수행하여 생성한 redo log들은 공유 메모리 공간인 log buffer에 저장되고, LOG_BUFFER_SIZE를 참조하여 log buffer의 메모리 크기를 설정한다.

<a id="0e2f546dcc35c21a"></a>
## LOG_DIR

<a id="a2b7fbf1fee67f8d"></a>
### 기본 정보

<a id="7eccff42e434801c"></a>
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

<a id="f5ec02351a9144dd"></a>
### 설명

Log buffer에 기록된 log는 database의 영속성을 보장하기 위해 비휘발성 저장 장치에 존재하는 log file로 flush 되고, LOG_DIR은 log file의 경로를 설정한다.

<a id="5926f5d03a9b7e4d"></a>
## LOG_FILE_SIZE

<a id="f1aaf569b4e3faee"></a>
### 기본 정보

<a id="c4d02aded287da98"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_FILE_SIZE |
| 요약 | log file size(byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20 Mbyte |
| MAX | 120 Gbyte |
| 기본값 | 100 Mbyte |

<a id="9c396fb6dabe453d"></a>
### 설명

Database에서 사용되는 log file의 크기를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 log file size를 변경할 수 없다.

<a id="07624567a8845988"></a>
## LOG_GROUP_COUNT

<a id="2c5da0bb3a57d9b3"></a>
### 기본 정보

<a id="ff1e304f31253c13"></a>
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

<a id="a6e019ed44607533"></a>
### 설명

Database에서 사용되는 log group의 개수를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 영향을 미치지 않는다. Database를 생성한 후에 log group을 추가하거나 제거하는 기능은 별도의 구문으로 지원한다.

<a id="60ed27c94087bc25"></a>
## LOG_MIRROR_MODE

<a id="452579c4977cfbb1"></a>
### 기본 정보

<a id="83d84dfa16a28a35"></a>
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

<a id="b64d76f6f1221d02"></a>
### 설명

데이터베이스를 시작할 때 redo log 복제 tool인 LogMirror를 운영할 때 필요한 shared memory를 구성하기 위한 프로퍼티이다.   
LogMirror를 수행하려면 반드시 enable 되어야 한다.  
Shared memory의 크기는 LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE 프로퍼티로 변경할 수 있다.

<a id="c850a6456dfbe9c8"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="ff27f9e70226249c"></a>
### 기본 정보

<a id="25b4fc75dc8e0250"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE |
| 요약 | shared memory size for LogMirror(byte) |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10485760 (10M) |
| MAX | 1073741824 (1G) |
| 기본값 | 104857600 (100M) |

<a id="c4d40d43ff1150ce"></a>
### 설명

Redo log 복제 tool인 LogMirror에 사용될 shared memory의 크기를 설정하는 프로퍼티이다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="642338177e109025"></a>
## LOG_MIRROR_TIMEOUT

<a id="dddf30254fe7a92b"></a>
### 기본 정보

<a id="69897a257129b571"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_MIRROR_TIMEOUT |
| 요약 | logmirror retry timeout(sec) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="0661f39842f841f5"></a>
### 설명

LogMirror의 응답을 기다리는 시간이다.   
만약 0일 경우 무한정 대기하며 그렇지 않을 경우 설정한 값만큼 대기하다가 TIMEOUT이 발생하고 LogMirror service를 중단한다. 이 후 서버는 정상적으로 운영된다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="5493e82137cddfe6"></a>
## LOG_SYNC_INTERVAL

<a id="86bbef20ee7b21d9"></a>
### 기본 정보

<a id="cb255d1a007e0614"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_SYNC_INTERVAL |
| 요약 | interval for synchronize log(s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 10000 |
| 기본값 | 3 |

<a id="2d91cc60c98c4bd5"></a>
### 설명

GOLDILOCKS의 log flusher는 log buffer의 내용을 disk log file로 flush하는 system thread이다. Log flusher가 유휴상태에서 깨어나면 flush 해야 할 log가 있는지 확인하여 있을 경우 flush를 수행한다. 이 때 LOG_SYNC_INTERVAL에 설정된 시간 내에 flush를 하지 않았다면 현재 log buffer의 마지막 block까지 flush를 수행하여 log buffer와 log file을 동기화한다.

<a id="80130a02dc724441"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="30b5bfb37b858764"></a>
### 기본 정보

<a id="b8543aea5ac8cd25"></a>
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

<a id="4be2ce18a4547788"></a>
### 설명

Log를 동기화하는 millisecond 단위의 주기이다.

<a id="ade5b00d98706f4a"></a>
## MAX_GROUP_COUNT

<a id="b9e5c2d0080abc0d"></a>
### 기본 정보

<a id="726fd04be4ea8af2"></a>
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

<a id="36c30396ffffa4fb"></a>
### 설명

클러스터 시스템 내 최대 그룹 개수이다.

<a id="d49f8ce6aa9ac147"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="63f4019a70bc1b49"></a>
### 기본 정보

<a id="58a193b66d47570a"></a>
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

<a id="c88c38a18c6a6791"></a>
### 설명

Cluster system에서 journaling이 발생할 경우 내부적으로 journaling data를 저장할 global journaling file 의 최대 크기 (quota)를 설정한다.

<a id="78ab874b580c9a98"></a>
## MAX_NODE_COUNT

<a id="4676daa9e92bce5b"></a>
### 기본 정보

<a id="d080c0418393a5b4"></a>
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

<a id="3f3c609c05b08735"></a>
### 설명

클러스터 시스템에 조인 가능한 노드 (instance)의 최대 개수이다.

<a id="577e637e88d9ffdf"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="b044ed42834697cd"></a>
### 기본 정보

<a id="ddc62ae16a8ca7e3"></a>
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

<a id="6781dc61c5222ac7"></a>
### 설명

동시에 수행될 수 있는 statement 개수를 설정한다.

<a id="4463a53b087aa0f2"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="b4b6c9aefd4124e1"></a>
### 기본 정보

<a id="0186c48e6c38a30e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_FILE_CACHE_SIZE |
| 요약 | the limit of file descriptor cache |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 16 |
| MAX | 32768 |
| 기본값 | 128 |

<a id="8546f5639d3906d2"></a>
### 설명

세션에서 사용 중인 파일 캐쉬의 최대 개수를 설정한다.

<a id="2a4d3358764a45dd"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="4ff3cf90c83a7152"></a>
### 기본 정보

<a id="dff191501cb3c902"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_FLUSH_BUFFER_PAGE_COUNT |
| 요약 | maximum number of buffer page count to be flushing |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 64 |

<a id="9d50af11fa29046c"></a>
### 설명

디스크 쓰기 연산 한 번으로 기록할 수 있는 최대 페이지 수를 설정한다. 디스크 테이블스페이스의 페이지가 버퍼에서 변경이 된 경우 IO thread가 이를 디스크에 기록한다. 디스크 쓰기 연산을 한 번 수행할 때 인접한 페이지들을 함께 기록하면 디스크 기록 횟수를 줄여 시스템 자원의 효율성을 높일 수 있다.

<a id="0dc32eaa49f8190f"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="d2e2ef266d63e505"></a>
### 기본 정보

<a id="3f3b26d6ba6aba11"></a>
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

<a id="ca3d5b8cfa2e7d7a"></a>
### 설명

Log buffer의 내용을 disk의 log file에 flush 할 때 한 번의 write 연산으로 flush 할 log block의 최대 개수를 설정한다.

<a id="77215a65fc8d40de"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="797ec1cb76f94af0"></a>
### 기본 정보

<a id="1ac4551183e201c9"></a>
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

<a id="d110e01f2a13db0c"></a>
### 설명

GOLDILOCKS의 datafile은 checkpoint와 특정 DDL문에 의해 disk에 flush 된다. Datafile을 flush 하기 위해 한 번의 write 연산으로 flush 할 data page의 최대 개수를 설정한다.

<a id="7e3ba1c10642baa4"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="8ebbc1dc3cffc7a5"></a>
### 기본 정보

<a id="80aa4fc274ebbd48"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT |
| 요약 | maximum number of replaying journals for rebuild index |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| 기본값 | 2 |

<a id="f5f0e0b6a55141cb"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하면 DML 수행과 병행하여 처리할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal log들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. Journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="dce8e523ec19c482"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="881a73a36c022c87"></a>
### 기본 정보

<a id="9131919b442ffc24"></a>
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

<a id="d187c9b3f5b91b54"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스를 DML과 병행하여 수행할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 테이블 리밸런스는 테이블을 동기화하는 동안 발생한 journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="9c7f9b957e17e863"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="1f5d0a52f3bd0b91"></a>
### 기본 정보

<a id="8a34df993c59a000"></a>
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

<a id="f26f8e7d63b8c554"></a>
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

- Embedded SQL 에서 DECLARE cursor FOR UPDATE 구문을 사용한 경우

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

> Embedded SQL에서는 다음과 같이 FOR UPDATE가 없는 DECLARE CURSOR 구문은 session에 named cursor를 생성하지 않는다.

```
{
    ...
    EXEC SQL DECLARE my_cursor CURSOR FOR SELECT col_name FROM tab_name;
    ...
}
```

<a id="a94046021edba0f3"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="95d6aa1588c045e6"></a>
### 기본 정보

<a id="a2c232a516f0c2f3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_PACKAGE_INSTANCE_COUNT |
| 요약 | maximum number of package instance that the driver can support for a connection |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 100000 |
| 기본값 | 128 |

<a id="cf5093383ce3c574"></a>
### 설명

하나의 session 내에서 사용할 수 있는 package instance의 최대 개수이다.  
Package instance는 해당 session에서 stateful package를 사용할 때 생성된다.

<a id="5b411827309c10e7"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="c437f3e9ff5dd034"></a>
### 기본 정보

<a id="d7b8dc081e67a4d7"></a>
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

<a id="d5fb9e4f20b63311"></a>
### 설명

Shared mode로 접속한 하나의 session에서 사용 가능한 최대 buffer size를 설정한다.  
자세한 내용은 [DISPATCHER_CM_BUFFER_SIZE](#42d313969647fe76)를 참조한다.

<a id="6877e302b38e1c3e"></a>
## MEASURE_CLUSTER_LATENCY

<a id="c0fb0082324572b9"></a>
### 기본 정보

<a id="f510f56889d4faf7"></a>
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

<a id="ffdf1577b510b6c0"></a>
### 설명

Measure cluster의 latency 이다.

<a id="257deba70585568a"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="f7c1d911be8934c9"></a>
### 기본 정보

<a id="18089e3d1bc40032"></a>
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

<a id="d399856e31b4bac9"></a>
### 설명

샘플링을 이용해서 [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#1513e1fe777d56bb)을 수행할 때의 최소 샘플링 row 건수이다.

<a id="ed6ef32099e6a2c9"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="85023437c9bed932"></a>
### 기본 정보

<a id="3d345a1b6d943f61"></a>
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

<a id="9e321f173fb89523"></a>
### 설명

DML은 이전 image를 저장하기 위해 undo page를 사용한다. DML당 undo segment를 하나씩 사용하여 undo page를 소모하는데, 만약 할당받은 undo segment의 page를 모두 소진하였을 경우 다른 undo segment의 page를 가져와서 사용할 수 있다. MINIMUM_UNDO_PAGE_COUNT는 undo page가 부족할 때 page를 가져올 undo segment를 찾기 위한 최소 undo page 수이다. 즉, undo page가 부족할 때, MINIMUM_UNDO_PAGE_COUNT 보다 많은 page를 보유한 undo segment에서만 page를 가져올 수 있다.

<a id="0b417b6d59bdf10c"></a>
## NET_BUFFER_SIZE

<a id="b896f3e010849de7"></a>
### 기본 정보

<a id="87e57fc92d9c1204"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | NET_BUFFER_SIZE |
| 요약 | TCP network buffer size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1024 |
| MAX | 1073741824 |
| 기본값 | 32768 |

<a id="30dd630dd0e66ea7"></a>
### 설명

TCP 통신 buffer size를 설정한다.  
Dedicated 모드에서는 통신 packet의 최대 크기로 설정된다.  
Shared 모드에서는 [DISPATCHER_CM_UNIT_SIZE](#1bc78f9b2aa8ae49)가 사용된다.

<a id="c4633f85f0eaaed9"></a>
## NLS_DATE_FORMAT

<a id="3d17bd95b1586a60"></a>
### 기본 정보

<a id="0e440e9d7f105514"></a>
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

<a id="6fac97b722e2a910"></a>
### 설명

NLS_DATE_FORMAT은 TO_CHAR와 TO_DATE 함수의 default date format을 지정한다.

<a id="87c4cf7cbfe4f6d9"></a>
## NLS_TIME_FORMAT

<a id="cf74bb207a44f7f4"></a>
### 기본 정보

<a id="94cb7a8936d613b2"></a>
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

<a id="5aa6057f44028246"></a>
### 설명

NLS_TIME_FORMAT은 TO_CHAR와 TO_TIME 함수의 default time format을 지정한다.

<a id="ff631fe160c25550"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="ee6186c2507a7f98"></a>
### 기본 정보

<a id="3fea45388e391956"></a>
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

<a id="796d5e42bd83d69d"></a>
### 설명

NLS_TIME_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIME_WITH_TIME_ZONE 함수의 default time with time zone format을 지정한다.

<a id="75b47cb73b3a190a"></a>
## NLS_TIMESTAMP_FORMAT

<a id="cff865ee34b80398"></a>
### 기본 정보

<a id="ec6ab77bf1c33661"></a>
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

<a id="f4c11495d60aaa31"></a>
### 설명

NLS_TIMESTAMP_FORMAT은 TO_CHAR와 TO_TIMESTAMP 함수의 default timestamp format을 지정한다.

<a id="f2873b18cb78ac0d"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="eb3edd796975be27"></a>
### 기본 정보

<a id="707f2d6b3f3f7700"></a>
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

<a id="4dfe331bf3f9c49a"></a>
### 설명

NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIMESTAMP_WITH_TIME_ZONE 함수의 default timestamp with time zone format을 지정한다.

<a id="6e457ccdc672d024"></a>
## NUMA

<a id="2fdce2415d95ae63"></a>
### 기본 정보

<a id="b41db861f118137e"></a>
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

<a id="0a246f7cd09f11c1"></a>
### 설명

NUMA를 활성화/ 비활성화한다.

> AIX에서 NUMA 속성을 사용하기 위해서는 사용자 계정을 변경해야 한다. 다음 명령을 루트 사용자로 실행한다.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> 여기에서 &lt;username&gt;은 루트가 아닌 AIX 사용자 계정이다.  
> 변경 사항을 적용하려면 로그아웃한 후에 다시 로그인해야 한다.

<a id="4f078b0ea2982b8e"></a>
## NUMA_MAP

<a id="6cbb35346eaecdfd"></a>
### 기본 정보

<a id="3769244edc26cc5b"></a>
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
| 기본값 | 'x' : no binding |

<a id="bb8c283fe6b6e8b4"></a>
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

<a id="1a82892a8ffa1124"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="bc5bff525411d76d"></a>
### 기본 정보

<a id="8f8d36000dc7c825"></a>
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

<a id="ead4a28de79e3eea"></a>
### 설명

시스템의 백그라운드 프로세스 (gmaster)는 노드 장애에 따른 failover를 완료한 후에 장애 멤버를 자동으로 오프라인 시킨다.

만약 NO로 설정되어서 장애 멤버가 오프라인되지 않았다면 장애 멤버를 시스템에 다시 조인시키기 전에 다음 구문을 실행해야 한다.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="e294a8cc503962ea"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="60a2daa6d1edc273"></a>
### 기본 정보

<a id="125fdf4c04e18fed"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD |
| 요약 | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 |
| 기본값 | 1048576 |

<a id="78322aabbd924c6e"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하는 동안 수행된 DML은 journal log를 남긴다. 인덱스 재구축이 마무리되는 단계에서 여러 차례에 걸쳐 journal이 인덱스에 반영되는데 이 때 journal log를 반영하는 최대 차수는 [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#7e3ba1c10642baa4)가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="107346a1eddec13f"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="6bc21378732bdcfc"></a>
### 기본 정보

<a id="dfdd2f70790142c3"></a>
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

<a id="1c9cfceab187d144"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스는 수행 중에 발생한 DML이 남긴 journal log를 여러 번에 걸쳐 반영한다. Journal log를 반영하는 최대 차수는 MAXIMUM_JOURNAL_REPLAY_COUNT가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="91fb02ce9a0448ff"></a>
## OS_GROUP_ACCESS

<a id="e28b11cf834a5733"></a>
### 기본 정보

<a id="9379765beb81e097"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | OS_GROUP_ACCESS |
| 요약 | enable access database with OS group permission |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="c589f657c894c935"></a>
### 설명

동일한 group의 다른 user가 D/A로 접속하려면 이 설정을 YES로 변경해야 한다. 또한 시스템 상의 umask도 0002로 변경해야 한다.

<a id="41ba950b4356694a"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="7b60d55bd6b4ef0f"></a>
### 기본 정보

<a id="2ec5692b69524911"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PACKET_COMPRESSION_THRESHOLD |
| 요약 | The size limit at which packets are compressed(bytes) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 32 |
| MAX | 2113929216 |
| 기본값 | 2113929216 |

<a id="b62e667d0e1ed298"></a>
### 설명

클라이언트로 보낼 통신 데이터의 크기가 PACKET_COMPRESSION_THRESHOLD 보다 클 경우, 통신 데이터를 압축한다.

<a id="44c7e91dd61aa94f"></a>
## PAGE_CHECKSUM_TYPE

<a id="fadd305d028db773"></a>
### 기본 정보

<a id="a5384ffa61005d06"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PAGE_CHECKSUM_TYPE |
| 요약 | page checksum type (0:LSN, 1:CRC) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="0a23450e612d9088"></a>
### 설명

Datafile의 각 page들에 대한 물리적 정합성을 보장하기 위해 checksum을 사용한다. GOLDILOCKS는 LSN, CRC 방식의 page checksum을 지원한다.

- 0: LSN
- 1: CRC

<a id="471ad4dfae4507b6"></a>
## PARALLEL_IO_FACTOR

<a id="10eb88b1f4a26b86"></a>
### 기본 정보

<a id="c2ce33e486727b24"></a>
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

<a id="96cbbac5d195a172"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일을 병렬 로딩하고 체크포인트 할 때 데이터 파일을 병렬 기록하기 위한 thread 개수를 설정한다.

<a id="eac2fca9e52129e6"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="5dd0dbe5acf2b389"></a>
### 기본 정보

<a id="78cb36972a963e9f"></a>
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

<a id="f914f0eee35c1066"></a>
### 설명

Datafile의 병렬 IO를 위한 group directory를 설정한다. 즉, PARALLEL_IO_FACTOR 수만큼 group을 설정하여 각 group에 속한 datafile 별로 병렬 IO를 수행한다.

<a id="0baf9509e6259cdf"></a>
## PARALLEL_LOAD_FACTOR

<a id="bd876d7e591886b3"></a>
### 기본 정보

<a id="f249528611bfc866"></a>
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

<a id="947c06fa3b8f6918"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일의 메모리를 적재한 후에 병렬 작업을 위한 thread 개수를 설정한다.

<a id="e05c1bc4f17dff69"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="5474ef42c4340b56"></a>
### 기본 정보

<a id="391b46409d80b66b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PENDING_LOG_BUFFER_COUNT |
| 요약 | default pending log buffer count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 32 |
| 기본값 | 4 |

<a id="d724e98e4189456f"></a>
### 설명

여러 트랜잭션이 동시에 실행될 경우 log buffer에 대한 경쟁을 줄이기 위해 pending log buffer를 사용하며, PENDING_LOG_BUFFER_COUNT는 동시에 사용할 수 있는 pending log buffer 개수를 설정한다.

<a id="5aa340218b8e5a9a"></a>
## PLAN_CACHE

<a id="d6ac43900874f3c4"></a>
### 기본 정보

<a id="5848a2ce1fb6df1a"></a>
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

<a id="f4399444e5b92bba"></a>
### 설명

Plan cache 사용 여부를 설정한다.

<a id="211c5592125ca84f"></a>
## PLAN_CACHE_SIZE

<a id="1ea19b82a4dee307"></a>
### 기본 정보

<a id="e0e83abdb88c5d6a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_CACHE_SIZE |
| 요약 | sql plan cache size(byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 20971520 |
| MAX | 1099511627776 |
| 기본값 | 104857600 |

<a id="5c456df7576d93e4"></a>
### 설명

Plan cache에 사용할 메모리 크기를 설정한다.

<a id="10275b68c5c037af"></a>
## PLAN_HISTORY

<a id="0cfc65095f5f086b"></a>
### 기본 정보

<a id="8359bd1c3efd151f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_HISTORY |
| 요약 | plan history for SQLs |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="2d08f018441844a1"></a>
### 설명

Plan history 사용 여부를 설정한다.

<a id="0425f8ed370b3a24"></a>
## PLAN_HISTORY_SIZE

<a id="36c8a0f28480e219"></a>
### 기본 정보

<a id="b3b847bf1b0a7580"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_HISTORY_SIZE |
| 요약 | plan history size |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| 기본값 | 0 |

<a id="cd2d61796781dade"></a>
### 설명

Plan history에 저장할 plan 개수를 설정한다.

<a id="c28c4ac9364a4bf2"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="d1a79e0282a09934"></a>
### 기본 정보

<a id="175c5ebce4722cf1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PRIVATE_STATIC_AREA_INIT_SIZE |
| 요약 | Initial size of Private Static Area (byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 34359738368 |
| 기본값 | 10485760 |

<a id="9c6a49bb8c6e45a5"></a>
### 설명

세션이 사용할 heap 메모리의 최초 크기를 설정한다. 세션에서 사용되지 않는 메모리가 생기더라도 이 메모리들이 운영체제로 반환되지는 않는다.

<a id="14d6443e6f5c843c"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="85a9bf91f2d9bb53"></a>
### 기본 정보

<a id="713b384dcb0dfc38"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PRIVATE_STATIC_AREA_NEXT_SIZE |
| 요약 | Next size of Private Static Area (byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1024 |
| MAX | 34359738368 |
| 기본값 | 10485760 |

<a id="1970a27fdba65d9e"></a>
### 설명

세션에서 heap 메모리를 추가적으로 할당할 때, 확장될 메모리 크기를 설정한다.

<a id="05e3d3245b4f31d6"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="3619ddcc92a48508"></a>
### 기본 정보

<a id="3687489c609d39b4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PRIVATE_STATIC_AREA_SHRINK_THRESHOLD |
| 요약 | Threshold bytes to attempt to shrink private static area(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 34359738368 |
| 기본값 | 10485760 |

<a id="4f870867efb22eec"></a>
### 설명

세션에서 사용하지 않는 heap 메모리가 생기더라도 이 크기만큼의 메모리를 유지하며 시스템에 반환하지 않고 세션 내에서 재사용한다.

PRIVATE_STATIC_AREA_INIT_SIZE보다 작게 설정하더라도 그 크기보다 작아지지 않는다.

<a id="4e8d13e352a7d20d"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="03ad169bea966061"></a>
### 기본 정보

<a id="c0056f05ef607622"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PRIVATE_STATIC_AREA_SIZE |
| 요약 | Private Static Area Size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 104857600 |
| MAX | 34359738368 |
| 기본값 | 104857600 |

<a id="7f6b8d0b587d6502"></a>
### 설명

세션에서 할당할 수 있는 최대 heap 메모리 크기를 지정한다.

<a id="8fc37eb8ba5c6486"></a>
## PROCESS_MAX_COUNT

<a id="a4005a925813ccc7"></a>
### 기본 정보

<a id="b53c20d15abcf52d"></a>
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

<a id="660556c628e54e7c"></a>
### 설명

시스템에서 사용할 수 있는 최대 프로세스 (thread) 개수를 지정한다.

시스템 프로세스 생성  
• D/A 또는 C/S dedicated 모드로 접속할 때마다 프로세스가 생성된다.  
• C/S shared 모드는 기본적인 balancer, dispatcher, shared-server가 프로세스이고 client에서 접속할   
&nbsp;&nbsp;때는 프로세스가 생성되지 않는다.

<a id="30db74c17ba7b790"></a>
## QUERY_TIMEOUT

<a id="6978436cec142f73"></a>
### 기본 정보

<a id="13ee0149a62529ea"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | QUERY_TIMEOUT |
| 요약 | query timeout(s) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10000000 |
| 기본값 | 0 |

<a id="e613e5e1400395d1"></a>
### 설명

세션에서 받은 명령어를 처리할 수 있는 최대 시간을 지정하며 만약 해당 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT 에러가 발생하지 않는다.

<a id="50e795f1a5c0f658"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="95c0a3a782d081c8"></a>
### 기본 정보

<a id="52eef876caaa7a33"></a>
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

<a id="9831847084009bcb"></a>
### 설명

미디어 복구 시 archive redo log가 존재하는 디렉토리의 개수를 설정한다.

<a id="04bbde44289ddbf4"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="5d35b5d10e172a7c"></a>
### 기본 정보

<a id="3450df85ab21c102"></a>
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

<a id="b2d80596a7390213"></a>
### 설명

증분 백업을 이용하여 파일을 복원할 때 증분 백업이 존재하는 디렉토리의 개수를 설정한다.

<a id="82e02498db222303"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="e5e15cd8aebb7036"></a>
### 기본 정보

<a id="8d0d284f927c1c90"></a>
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

<a id="356421b8bf496660"></a>
### 설명

Rebalance 하기 위해 block을 읽어들이는 횟수이다.

<a id="094180606b5040d1"></a>
## REBALANCE_SHARD_DIVISOR

<a id="7bd12b86a11942fb"></a>
### 기본 정보

<a id="2c7dcd8493db6da0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REBALANCE_SHARD_DIVISOR |
| 요약 | partition factor of shard upon rebalance |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 1000 |
| 기본값 | 1 |

<a id="a7caa09db8e42bf6"></a>
### 설명

테이블을 rebalance 하고 synchronize 할 때 사용되는 shard를 몇 개로 분할할지 설정한다.  
자세한 내용은 [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#149294331f00fde7)를 참조한다.

<a id="e8c1fdef49ed452b"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> 3.1 이후로 지원하지 않는다.

<a id="def1afd7a383ff0a"></a>
### 기본 정보

<a id="e9df5fdfda87d044"></a>
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

<a id="73cd710b02fceb44"></a>
### 설명

Page count 변경에 의해 plan이 recompile 되었는지 여부를 체크하기 위해 minimum page count를 설정한다.

<a id="8b8ad09806ce53ec"></a>
## RECOMPILE_PAGE_PERCENT

> 3.1 이후로 지원하지 않는다.

<a id="d2d7b8c2fc7dc54f"></a>
### 기본 정보

<a id="8b8165ca702ef1ca"></a>
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

<a id="7940162b69c0aaab"></a>
### 설명

Page count가 변경되어 plan을 recompile 할 때의 page percentage를 설정한다. 이 값이 0인 경우 page count 변경에 따른 recompile을 하지 않는다.

<a id="ead320049a59f9df"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="799e03f10b3f67c6"></a>
### 기본 정보

<a id="31824969eeb6f027"></a>
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

<a id="49acd8eaccece4cb"></a>
### 설명

복구를 위한 기본 log buffer 크기이다.

<a id="45c4cec31d8bbda5"></a>
## RECYCLEBIN

<a id="c2753073a3f25577"></a>
### 기본 정보

<a id="84b8eddf85a67a9d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RECYCLEBIN |
| 요약 | enable or disable recyclebin feature |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="0ee5112c4bfc15f0"></a>
### 설명

휴지통 기능을 활성화할지 여부를 설정한다.

<a id="caf36514c5c8f012"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="7a318f2122290565"></a>
### 기본 정보

<a id="53ed74d03eb0a669"></a>
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
| 기본값 | 2113929216 |

<a id="bd0fd1ca66df7bd2"></a>
### 설명

생성된 REDO LOG의 크기가 REDO_LOG_COMPRESSION_THRESHOLD 값보다 클 경우, REDO LOG를 압축한다.

<a id="be65317b42b5e37a"></a>
## REFINE_RELATION

<a id="afd9dd143a5a3fa5"></a>
### 기본 정보

<a id="2d3f1c85c0f57631"></a>
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

<a id="27c63e6a304abd51"></a>
### 설명

이 속성을 NO로 하면 서버를 재시작할 때 REFINE RELATION 과정을 수행하지 않는다.

해당 프로퍼티는 REFINE RELATION 도중에 문제가 발생한 경우에 사용할 수 있으며 삭제되었지만 REFINE 하지 못한 RELATION (테이블이나 인덱스)들의 공간은 재사용할 수 없다. 문제를 해결한 이후 해당 프로퍼티를 YES로 설정하고 재시작하면 삭제하지 못했던 RELATION들에 대해 REFINE을 시도한다.

<a id="d26fbd33f3c2f813"></a>
## SESSION_FATAL_BEHAVIOR

<a id="622e2162b87ac844"></a>
### 기본 정보

<a id="3c46b4274c8902f4"></a>
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

<a id="f87d78025390de14"></a>
### 설명

Session fatal이 발생할 때 fatal을 유발한 thread만 종료시킬지 아니면 프로세스 자체를 종료시킬지 결정한다.

- 0: Fatal을 유발한 thread만 종료한다.
- 1: 프로세스를 종료한다. 해당 프로세스 내에 다수의 세션이 동시에 수행되고 있다면 모든 세션들이 데이터베이스 사용을 끝낸 후에 프로세스를 종료한다.

<a id="ccea85f51503b3b3"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="827f57c6bf1a8c34"></a>
### 기본 정보

<a id="5779711deb1fdfd1"></a>
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

<a id="2169e4562c1aba3b"></a>
### 설명

세션에서 사용할 공유 메모리를 미리 할당할 크기를 설정한다.

<a id="d634130b621cf350"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="4419bc0b4df24ea0"></a>
### 기본 정보

<a id="15c34813eab5c435"></a>
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

<a id="8ad6660ca437cb89"></a>
### 설명

세션에서 사용한 동적 공유 메모리를 해제할 때 세션에서 사용하지 않는 동적 공유 메모리를 시스템에 반납할지 여부를 판단하기 위한 경계값을 설정한다. 즉, 사용하지 않는 메모리 중 설정된 값보다 큰 크기의 메모리 청크가 있으면 시스템에 반납한다.

<a id="9b2d649fa0590efa"></a>
## SESSION_POOL_INIT_SIZE

<a id="d8cf9579323c42ce"></a>
### 기본 정보

<a id="f95af31bbd2333f3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_POOL_INIT_SIZE |
| 요약 | initial memory size for session pool |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1099511627776 (1T) |
| 기본값 | 0 |

<a id="6bc585fbb4859e1c"></a>
### 설명

Session pool의 초기 메모리 크기를 설정한다.

각 세션들에 메모리가 필요한 경우 session pool에서 공간을 할당 받는데 session pool의 공간이 부족할 경우에는 SSA로부터 공간을 할당 받는다.  
Session pool은 세션에서 SSA로 빈번하게 접근하는 것을 방지하기 위해서 사용되는데 만약 "0"으로 설정할 경우 session pool 기능은 비활성화 된다.

<a id="7e53a73467a11870"></a>
## SESSION_POOL_NEXT_SIZE

<a id="8bb281eaceca9b07"></a>
### 기본 정보

<a id="85105672c729e35d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_POOL_NEXT_SIZE |
| 요약 | memory size to be expanded in session pool |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 1048576 (1M) |

<a id="5957532afc372c3d"></a>
### 설명

Session pool의 공간을 확장할 때 session pool 내부의 메모리 크기를 얼마나 확장할지 설정한다.  
SESSION_POOL_INIT_SIZE가 0보다 큰 경우에만 유효하다.

<a id="301d98a994f57b6d"></a>
## SHARED_MEMORY_ADDRESS

<a id="7ac25ba4ee0c7358"></a>
### 기본 정보

<a id="eaa51b4981a1a77f"></a>
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

<a id="d870c63e6748c66e"></a>
### 설명

Shared Static Area (SSA)의 주소를 지정한다.

<a id="528d7298ab9c5c40"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="195a741421c140f2"></a>
### 기본 정보

<a id="88e7f30041fe9b5c"></a>
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

<a id="812ab84b9c7750d2"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory key 값을 지정한다.

<a id="066fcf845a3acf8e"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="3ddb41f99d2d4690"></a>
### 기본 정보

<a id="702c915551a701dd"></a>
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

<a id="cb24c9b6b1862ad5"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory name을 지정한다.

<a id="2bf816f7170df461"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="b31c319d0b76984b"></a>
### 기본 정보

<a id="72a27720ad8c5f86"></a>
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

<a id="f9e1edf14cd908ab"></a>
### 설명

Shared Static Area (SSA)의 크기를 지정한다.

<a id="b36aacdfa3d5e1ca"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="167eb74d4e26a11a"></a>
### 기본 정보

<a id="8191ac4d8d6e9786"></a>
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

<a id="f8fbc29929ff070e"></a>
### 설명

Shared 모드의 dispatcher에서 shared-server로 요청하는 queue 개수를 설정한다. 여러 dispatcher가 사용자의 작업 요청을 shared-server에 할당할 때 사용하는 queue로써 일반적으로 load-balance를 위해 하나를 사용한다. 그러나 dispatcher와 shared-server가 많아지면 queue에 경합이 발생하여 성능이 저하될 수 있으므로 이 값을 늘려서 사용한다. 이 값이 커지면 load-balance가 비효율적으로 될 수 있고 dead-lock이 발생할 가능성이 커진다.

<a id="021eec4715ad44e7"></a>
## SHARED_SERVERS

<a id="d9079fe069b3f127"></a>
### 기본 정보

<a id="fac3d1f6738bd5ec"></a>
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

<a id="d630eb57f45de5df"></a>
### 설명

Shared 모드에서 shared-server process 개수를 설정한다.  
Open 단계에서는 alter system으로 값을 줄일 수 없다.

<a id="56c3dbb635ea88f2"></a>
## SHARED_SESSION

<a id="22fa236975918f49"></a>
### 기본 정보

<a id="f77c04d2eaf78e10"></a>
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

<a id="3abb2eb7acb44325"></a>
### 설명

Shared 모드를 활성화할지 여부를 설정한다. 이 값을 NO로 설정하면 load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver)가 실행되지 않는다.

<a id="684030daa6f1292e"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="786be5c2d6004583"></a>
### 기본 정보

<a id="f89797f291ff2150"></a>
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

<a id="5322656ad35c5530"></a>
### 설명

Snapshot read가 필요로 하는 statement의 최대 유지 시간을 설정한다. 설정된 시간을 초과한 snapshot statement들에는 TIMEOUT 에러가 발생한다.

<a id="09f21fa131954110"></a>
## SQL_HISTORY_SIZE

<a id="626ce3395856a50f"></a>
### 기본 정보

<a id="28a05288839511cd"></a>
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

<a id="c86c97b243d7057e"></a>
### 설명

SQLs의 이력 (history) 크기이다.

<a id="befccb31452f3629"></a>
## SQL_HISTORY_TYPE

<a id="e1fa918b5ad13e67"></a>
### 기본 정보

<a id="5ab2e2e8b704728c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SQL_HISTORY_TYPE |
| 요약 | history type for SQLs |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="ea9d928b1ab03a52"></a>
### 설명

SQLs의 이력 (history) 타입이다.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="928c613e12620d64"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="2e224bef0a169a91"></a>
### 기본 정보

<a id="af55c6ac9afae926"></a>
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

<a id="0c39a14b94537a90"></a>
### 설명

Database 내의 모든 변경 내용에 대한 supplemental log를 기록한다.

<a id="81fa17bd408ab6a5"></a>
## SYNC_DISPATCHER_CM_BUFFER_COUNT

<a id="ff43b0d4237fe07b"></a>
### 기본 정보

<a id="5d2e9615a8b12542"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYNC_DISPATCHER_CM_BUFFER_COUNT |
| 요약 | communication buffer count for synchronization dispatcher |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 1 |

<a id="b13bc8de6c636f31"></a>
### 설명

Cluster synchronization dispatcher의 communication buffer 개수를 지정한다.

<a id="cc1563ffff3f67a2"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="abbc25f492f3b603"></a>
### 기본 정보

<a id="726ae2a62fb68800"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_DISK_DATA_TABLESPACE_SIZE |
| 요약 | default system disk data tablespace size(byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | NONE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 200 Mega |

<a id="39d2c56e754d9f55"></a>
### 설명

데이터베이스를 생성할 때 초기 DISK_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="eb789a5693add577"></a>
## SYSTEM_FILE_IO

<a id="917f48fd4e7bf7d1"></a>
### 기본 정보

<a id="18b7dc6835d43fd9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_FILE_IO |
| 요약 | i/o type for system file ( 0: direct io, 1: buffered io ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="1ae875cef66ec4b4"></a>
### 설명

데이터 파일과 로그 파일을 제외한 데이터베이스 파일을 사용할 때 IO 타입을 설정한다.

<a id="b128f7f19cf57c0f"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="1fcb133e54c6380f"></a>
### 기본 정보

<a id="44c28abf54e0fa5d"></a>
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

<a id="ab019f08836082e7"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_AUX_TBS 테이블스페이스 크기를 결정한다.

<a id="56a21827c8078153"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="d8753f85278d9649"></a>
### 기본 정보

<a id="d01e32f16015ee48"></a>
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

<a id="f279fca885f99cc6"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="1ea354340e2e4148"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="ac2178a168900344"></a>
### 기본 정보

<a id="ceba7ecb288d8a35"></a>
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

<a id="fe09e6aad825e722"></a>
### 설명

데이터베이스를 생성할 때 초기 DICTIONARY_TBS 테이블스페이스의 크기를 결정한다.

<a id="19062829f829a47f"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="1d9f6cc6ec5b036d"></a>
### 기본 정보

<a id="b785d41c46a39728"></a>
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

<a id="017badfc30cc2a3b"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_TEMP_TBS 테이블스페이스의 크기를 결정한다.

<a id="9a695b142c119386"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="354365f5d1e7449f"></a>
### 기본 정보

<a id="8e183f17eea8fd68"></a>
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

<a id="e06f764aa83618fa"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_UNDO_TBS 테이블스페이스의 크기를 결정한다.

<a id="192e7498b53b1609"></a>
## SYSTEM_TABLESPACE_DIR

<a id="8a824f8d0f8daf7d"></a>
### 기본 정보

<a id="725060a0681f695b"></a>
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

<a id="8a87af67e111a104"></a>
### 설명

데이터베이스를 생성할 때 초기 시스템 테이블스페이스들이 저장되는 경로를 지정한다.

<a id="8469ede8b8f1abbc"></a>
## SYSTEM_UDS_DIR

<a id="cc3c49dabf7271ca"></a>
### 기본 정보

<a id="acb3e52af576a3d5"></a>
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

<a id="d4d52e8044906d1d"></a>
### 설명

Unix domain socket 파일이 생성되는 directory를 설정한다.  
DB system 이외에 glsnr 등과 같은 unix domain socket에 대한 디렉토리 설정은 별도의 configuration file에서 관리된다.  
최대 설정 크기는 60 byte이다. (Unix domain socket 파일의 절대 경로 (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.)

<a id="905f902a720feca5"></a>
## TCP_CLIENT_NUMA_NODE

<a id="becaf6c7c7796812"></a>
### 기본 정보

<a id="293e4e09a6d527b0"></a>
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

<a id="e19d820c87aee77e"></a>
### 설명

Client server 세션이 바인드 될 NUMA 노드 ID를 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="9092f4c2648cca6f"></a>
## TCP_NODELAY

<a id="f2cce570f4b571d1"></a>
### 기본 정보

<a id="d9ae768291bd0b1b"></a>
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

<a id="680ac00c6ffa4abc"></a>
### 설명

C/S 방식 (TCP socket)으로 client에 data를 전송할 때의 socket TCP_NODELAY 옵션을 설정한다.  
빠른 latency가 필요하지 않고 network 부하를 줄이고 싶은 경우에는 NO로 설정한다.

<a id="b13c41d1a791dffe"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="2b3e3b3218fb2065"></a>
### 기본 정보

<a id="4ec2f836f1d3dcc1"></a>
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

<a id="b73f292893936ce4"></a>
### 설명

Global temporary table이나 global temporary index segment가 drop 될 때 tablespace에 반납하지 않고 session에서 caching 할 segment 개수를 지정한다. Segment cache에 존재하는 segment는 향후 global temporary table이나 global temporary index에서 재사용된다.

- 0: Session에서 global temporary table이나 global temporary index의 segment cache를 사용하지 않는다.
- 1 ~ 4294967295: Session에서 global temporary table이나 global temporary index의 segment cache를 주어진 개수만큼 유지한다.

<a id="22a6f96b0a0ba9de"></a>
## TEMP_UNDO_ENABLED

<a id="1e5618357aeca343"></a>
### 기본 정보

<a id="e21502f8020a8c77"></a>
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

<a id="f27331b55860f92f"></a>
### 설명

Global temporary table에 대한 undo 레코드의 로깅 위치를 지정한다.

- 0 (FALSE): 데이터베이스의 기본 undo tablespace에 undo 레코드를 기록한다.
- 1 (TRUE): 데이터베이스의 기본 temporary tablespace에 undo 레코드를 기록한다.

<a id="2a51292bf46624b9"></a>
## TIMED_STATISTICS

<a id="1d4497dd688e8dcf"></a>
### 기본 정보

<a id="6f54e549458ee4ec"></a>
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

<a id="d7d7418f9f1aa849"></a>
### 설명

Wait event를 측정하는지 여부이다.  
v$system_event, v$session_event, v$session_wait table에 wait event와 관련된 통계 기록을 남기고 싶은 경우에 설정한다.

- 0: 통계 기록을 남기지 않는다.
- 1: 통계 기록을 남긴다.
- 2: High precision timer를 이용하여 통계 기록을 남긴다.

<a id="63c6489a6a82b299"></a>
## TIMER_INTERVAL

<a id="3fabe6c1cfe61ec6"></a>
### 기본 정보

<a id="e3b807aaa0104c73"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TIMER_INTERVAL |
| 요약 | timer interval time(us) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 10 |
| MAX | 100000 |
| 기본값 | 10000 |

<a id="01d5f97eecf8bdae"></a>
### 설명

타이머 thread가 시스템 시간을 설정할 수 있도록 시간 간격을 설정한다.

<a id="5525e5bf3452dfa7"></a>
## TIMEZONE

<a id="76407973af266c41"></a>
### 기본 정보

<a id="96a83f82bfb37984"></a>
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

<a id="11851538a505a0c8"></a>
### 설명

Database의 time zone 값이다.  
Database가 생성될 때 적용되는 속성으로써 -14:00 ~ +14:00 범위의 값을 사용할 수 있다.

<a id="18193aa2f7063bc3"></a>
## TRACE_ALTER_SYSTEM

<a id="29a0c28eb2887130"></a>
### 기본 정보

<a id="0fca57a3568fc802"></a>
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
| 기본값 | YES |

<a id="81c2590cec845bf1"></a>
### 설명

ALTER SYSTEM 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

시스템 변경에 대한 기록을 남기려면 TRACE_ALTER_SYSTEM 프로퍼티를 ON으로 설정한다.  

TRACE_ALTER_SYSTEM 프로퍼티는 SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="eb3cb94bca96473b"></a>
## TRACE_DDL

<a id="abc434cae7d26f36"></a>
### 기본 정보

<a id="0be47bff44e684f0"></a>
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
| 기본값 | YES |

<a id="50a4bc22d2fd3632"></a>
### 설명

Data Definition Language (DDL) 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

테이블 생성, 삭제, 변경 등과 같은 SQL 문을 실행했을 때 이에 대한 기록을 남기려면 TRACE_DDL 프로퍼티를 ON으로 설정한다.  

TRACE_DDL 프로퍼티는 DDL 구문 수행에만 영향을 주며, SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="c38f8a5307fde56c"></a>
## TRACE_LOG_ID

<a id="44ac7d0ec2099ddf"></a>
### 기본 정보

<a id="3e586ba6b7659296"></a>
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

<a id="a76fcc6c20d63373"></a>
### 설명

질의를 수행할 때 해당 질의에 대한 실행 계획 정보와 기타 정보를 trace directory(&lt;GOLDILOCKS_DATA&gt;/trc/) 아래에 있는 trace file (opt_p[프로세스ID]_s[세션ID].trc)에 기록한다.

질의에 대한 SQL 구문과 실행 계획, 수행시간 등에 대한 기록을 남기려면 아래 표의 flag 정보를 조합하여 설정한다.

**TRACE_LOG_ID에 대한 flag 정보**

<a id="87768946dd550c32"></a>
| 정보 | Flag(on) | Flag(off) |
| --- | --- | --- |
| PSM (procedure/function) 호출 흐름 출력 여부 | 1000000 | 0 |
| 성공한 SQL 질의 출력 여부 | 100000 | 0 |
| 실패한 SQL 질의 출력 여부 | 10000 | 0 |
| 실행 계획 출력 여부 | 1000 | 0 |
| 실행 형태 (direct/prepare) 출력 여부 | 100 | 0 |
| Bind 값 출력 여부 | 10 | 0 |
| 구간별 수행시간 출력 여부 | 1 | 0 |

만약 "성공한 SQL 질의 출력" + "실행 계획 출력" + "Bind 값 출력" 하려면 TRACE_LOG_ID 값을 101010으로 설정한다.

<a id="1767ab06efd54603"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="a496cda1e1bb272b"></a>
### 기본 정보

<a id="2f10c3aab0cf018d"></a>
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
| 기본값 | 24576 |

<a id="ece78b00a2dd75b3"></a>
### 설명

Trace logfile에 기록할 log message를 구성하는데 사용되는 heap memory buffer의 크기를 설정한다.

<a id="1fe1a61bc34b0a36"></a>
## TRACE_LOG_TIME_DETAIL

<a id="781cd8b0cf0a1ae1"></a>
### 기본 정보

<a id="77ae2a588620ff44"></a>
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

<a id="666e7ecba3892517"></a>
### 설명

Trace log를 기록할 때 시간 정확도를 높일지 여부를 설정한다.  
이 값이 OFF로 설정된 경우, 10 ms의 정확도를 가지며, ON으로 설정된 경우 1 us의 정확도를 가진다.

<a id="c7d79ce99697156b"></a>
## TRACE_LOGGER

<a id="525f90a2146c0b4c"></a>
### 기본 정보

<a id="51817a1df2eddb73"></a>
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

<a id="bff3a3f48a3546ed"></a>
### 설명

Trace log를 기록할 대상을 설정한다.  
1이면 file에 기록하고 2이면 remote로 파일에 기록한다.  
Remote로 기록하면 gtrclogger에서 원격으로 trace log를 수집하여 파일에 기록한다.

<a id="09c925d3e70266a7"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="8b95d2b045cdb76e"></a>
### 기본 정보

<a id="bf664de798590426"></a>
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

<a id="70434ac996b7d16e"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 host를 설정한다.

<a id="08bc0dc9635e548d"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="1e7c3e8c8413e839"></a>
### 기본 정보

<a id="587951eef3242bee"></a>
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

<a id="7b44eda2b0f8cc29"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 port를 설정한다.

<a id="510897d222e4ce2b"></a>
## TRACE_LOGIN

<a id="c8b763ed1192725f"></a>
### 기본 정보

<a id="76828f4174a0f01e"></a>
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

<a id="66eaa6f83cef2e03"></a>
### 설명

로그인 할 때 해당 접속 정보를 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc)에 기록한다.  
로그인 할 때 이에 대한 기록을 남기려면 TRACE_LOGIN 프로퍼티를 ON으로 설정한다.

<a id="8c17017f1037f69f"></a>
## TRACE_LONG_RUN_CURSOR

<a id="64d7e8096a1127ba"></a>
### 기본 정보

<a id="77d2c9d00dd76fd8"></a>
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

<a id="d37ec308c08509d8"></a>
### 설명

Cursor의 lifetime이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#7784a1e0d76e38c0) 프로퍼티를 사용한다.

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
   ...
   long_run_user_logic( s_name ); ❶ 사용자 logic으로 인해 ager가 오랜 시간 자원을 정리하지 못한다.
   ...
   EXEC SQL CLOSE cur1;
   ...
}
```

<a id="d002ad14375e6203"></a>
## TRACE_LONG_RUN_SQL

<a id="2422572f39e05fe3"></a>
### 기본 정보

<a id="571d4911f7c7ac95"></a>
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

<a id="91f2811a3066dbb7"></a>
### 설명

구문의 수행시간이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) 에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#7784a1e0d76e38c0) 프로퍼티를 사용한다.

- 수행시간이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="7784a1e0d76e38c0"></a>
## TRACE_LONG_RUN_TIMER

<a id="d0f11b33bf6e0d14"></a>
### 기본 정보

<a id="71c63516956d54c1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LONG_RUN_TIMER |
| 요약 | trace long-run timer resolution ( 0: timer thread(10 ms interval), 1: gettimeofday() ) |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 0 |

<a id="4f9bd3db3633caa3"></a>
### 설명

다음 프로퍼티들을 이용하여 SQL 구문의 실행시간을 측정할 때 측정 정밀도를 제어한다.

- [TRACE_LONG_RUN_CURSOR](#8c17017f1037f69f)
- [TRACE_LONG_RUN_SQL](#d002ad14375e6203)

- 값의 의미
    - 0: 10 millisecond의 interval을 가지는 timer thread를 사용한다.
    - 1: gettimeofday() 함수를 이용하여 시간을 측정한다. 정밀도는 높지만 system call로 인한 부하가 있다.

<a id="9082de9a7be5d382"></a>
## TRACE_SYSTEM_DIR

<a id="4d9d2af76f9459b9"></a>
### 기본 정보

<a id="3c1ba08c13793193"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_SYSTEM_DIR |
| 요약 | system logger directory |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/trc |

<a id="8782c5cf6a097f98"></a>
### 설명

Trace 로그 메시지가 기록되는 디스크 경로를 지정한다.

<a id="92b0e95cff626bbf"></a>
### ALIAS

<a id="32b0d23ed7dfb886"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | TRACE_SYSTEM_DIR |
| ALIAS | SYSTEM_LOGGER_DIR |

<a id="d94724dfd1b1b7f0"></a>
## TRACE_XA

<a id="739a7f4c4a00db92"></a>
### 기본 정보

<a id="a683479499cac740"></a>
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

<a id="b614ac937a72f629"></a>
### 설명

XA 인터페이스를 사용할 때 추적 메세지를 출력할지 여부를 지정한다. 메세지는 'SYSTEM_LOGGER_DIR/xa.trc'에 출력된다.

<a id="c5305c9b4bc5977f"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="54551c86654a028b"></a>
### 기본 정보

<a id="ee77665b4c01ac76"></a>
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

<a id="9bc77d6667feed27"></a>
### 설명

Transaction slot을 할당할 때의 최대 대기 시간이다.

대기 시간이 TRANSACTION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="fa0db3260da44b1a"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="ef56cfb4b03572cc"></a>
### 기본 정보

<a id="1f165a7cd09176a1"></a>
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

<a id="2e3555e7b1f644f4"></a>
### 설명

TRANSACTION_COMMIT_WRITE_MODE는 트랜잭션이 완료될 때 트랜잭션이 생성한 log를 disk log file에 flush할지 여부를 설정한다. 즉, TRANSACTION_COMMIT_WRITE_MODE가 '1'이면 log를 트랜잭션 완료 시점에 disk log file에 flush해야 하고, 그렇지 않은 경우 log flush 여부와 관계없이 트랜잭션을 완료한다.

만약 TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정하여 시스템을 운용하는 경우에 트랜잭션을 COMMIT 한 후 log flush가 되지 않은 상태에서 GOLDILOCKS가 비정상적으로 종료되면 기록되지 않은 log로 인해 최신 data를 잃어버리게 된다.

따라서 모든 트랜잭션이 완료되었을 때 반드시 database에 남아 있어야 하는 경우 TRANSACTION_COMMIT_WRITE_MODE를 '1'로 설정하여 시스템을 운용하거나, TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정한 후 트랜잭션이 완료되는 시점에 명시적으로 'ALTER SYSTEM FLUSH LOGS' 문을 수행하여 log를 flush해야 한다.

- 0: no wait
- 1: wait

<a id="4e14ccaec342add1"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="286610ba8e4f6352"></a>
### 기본 정보

<a id="27fab9c37faa2565"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT |
| 요약 | 트랜잭션이 기록할 수 있는 최대 undo페이지 개수 |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 13107200 |
| 기본값 | 13107200 |

<a id="35298e1a232bb52a"></a>
### 설명

트랜잭션이 기록할 수 있는 최대 undo 페이지 개수를 의미한다. 최소값은 1로 8 Kbyte이며, 최대값은 13107200으로 100 Gbyte이다.

<a id="7b861ee8d3fb7f1d"></a>
## TRANSACTION_TABLE_SIZE

<a id="e51b7cf26061d8e0"></a>
### 기본 정보

<a id="dfd067f3743cd910"></a>
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

<a id="c884535da650b23f"></a>
### 설명

Database에서 수행되는 최대 트랜잭션 테이블의 수를 설정한다. 트랜잭션 테이블의 수를 변경하려면 database를 재시작해야 하는데, 변경되는 값이 이전에 설정된 값보다 더 큰 경우에는 항상 변경 가능하다. 그러나 이전 값보다 작은 값으로 변경할 경우, 재시작 복구 후 prepare된 트랜잭션들이 사용한 트랜잭션 slot 식별자의 최대값보다 작거나 같으면 재시작에 실패한다.

예를 들어, 1024로 설정된 값을 512로 변경하고, 재시작 시 prepare된 트랜잭션들이 사용한 트랜잭션 slot 식별자의 최대값이 512인 경우, 다음과 같이 재시작에 실패한다. 이 경우, 512보다 큰 수로 설정하면 재시작에 성공한다.

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

ERR-HY000(14118): TRANSACTION_TABLE_SIZE property value must be equal to or greater than '513'

gSQL> ALTER SYSTEM SET TRANSACTION_TABLE_SIZE = 513 SCOPE = FILE;

System altered.

gSQL> \SHUTDOWN

Shutdown success

gSQL> \STARTUP

Startup success
```

> Cluster 환경에서 TRANSACTION_TABLE_SIZE는 모든 cluster member에서 동일해야 하기 때문에, TRANSACTION_TABLE_SIZE를 변경하려면 모든 cluster member를 재시작해야 한다.

<a id="28232ac9852c6def"></a>
## TRANSACTION_TIMEOUT

<a id="5a6f6705d18cb2e8"></a>
### 기본 정보

<a id="2f2d551d76643db0"></a>
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

<a id="83d6128734f22082"></a>
### 설명

Transaction이 활성화되어 있는 시간을 설정한다. Transaction이 장시간 활성화되어 있을 때 발생할 수 있는 부작용을 예방하기 위해 사용된다. 정해진 시간을 초과한 transaction이 있을 경우, gmaster 데몬이 해당 transaction을 소유한 세션을 자동으로 종료시킨다.

<a id="3ccb650e4649fce5"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="cd6efe2aba5f6c42"></a>
### 기본 정보

<a id="749b3121f6d857e2"></a>
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

<a id="8e594f236943df7e"></a>
### 설명

Undo relation을 할당할 때의 최대 대기 시간이다.

대기 시간이 UNDO_RELATION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="e9b0bf8ce2d70aa1"></a>
## UNDO_RELATION_COUNT

<a id="3facbf393e0e5fae"></a>
### 기본 정보

<a id="a09829b665427453"></a>
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

<a id="be067d0c846b9b9e"></a>
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

<a id="0e592ae5cf4b4ee1"></a>
## UNDO_SHRINK_THRESHOLD

<a id="031729737a3c0fbc"></a>
### 기본 정보

<a id="cc0bcf57038df254"></a>
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

<a id="fb5b96fa27bf9038"></a>
### 설명

Ager thread는 주기적으로 (10초) undo segment 공간을 검사하여 이 속성값보다 많은 공간을 차지하고 있을 경우, 재사용 가능한 공간을 테이블스페이스로 반환한다. Undo segment의 공간이 이 속성 (byte)만큼 남을 때까지 반환을 시도하다가 남은 undo page의 양이 MINIMUM_UNDO_PAGE_COUNT보다 작아지면 반환을 종료한다.

<a id="8bc9a84d7f230545"></a>
## USE_LARGE_PAGES

<a id="ed7b817db51a1114"></a>
### 기본 정보

<a id="0771ef3c494ddbd4"></a>
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

<a id="826af02084787808"></a>
### 설명

HugePage를 사용한다. USE_LARGE_PAGES를 사용하려면 먼저 장비에 HugePage를 설정해야 한다.

- 0: Large page를 사용하지 않는다.
- 1: Large page를 사용한다. 만약 공유 메모리 할당에 실패할 경우에는 에러가 발생한다.
- 2: Large page를 사용하여 할당을 시도한다. 만약 공유 메모리 할당에 실패할 경우에는 regular page를 사용하여 메모리를 할당한다.

> 리눅스 커널 2.6.32-573 이상에서만 사용할 수 있다.

<a id="1a29c6036e367ee4"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="7491165088d57fd9"></a>
### 기본 정보

<a id="d2a7fe0a411503c6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USER_DATA_TABLESPACE_MEDIA_TYPE |
| 요약 | default media type of user data tablespace |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 ( Memory ) |
| MAX | 1 ( Disk ) |
| 기본값 | 0 ( Memory ) |

<a id="0aefc38924a39453"></a>
### 설명

사용자 데이터 테이블스페이스를 생성할 때 테이블스페이스의 media 타입이 생략된 경우, default media 타입을 지정한다. 0은 memory, 1은 disk를 의미한다.

<a id="c69241dfb3f4664b"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="c35ec33d64f68346"></a>
### 기본 정보

<a id="1a3c2e17b665f906"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USER_DATA_TABLESPACE_SIZE |
| 요약 | default user data tablespace size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 32 Mega |

<a id="e6003dd3eecd346d"></a>
### 설명

사용자 데이터 테이블스페이스가 생성되거나 데이터 파일이 추가될 때 데이터 파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="cbd2e5d78539ac3b"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="505d2767a2fb13d5"></a>
### 기본 정보

<a id="4c88b97236d27a47"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USER_DISK_DATA_TABLESPACE_NEXTSIZE |
| 요약 | default next size of user data tablespace |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 3554432 Byte |
| MAX | 30 Giga |
| 기본값 | 10 Mega |

<a id="eb86065a22eeba78"></a>
### 설명

사용자 디스크 데이터 테이블스페이스의 데이터파일이 확장되어야 할 때 확장할 크기가 설정되지 않은 경우, default 크기를 지정한다.

<a id="4f2b1bf454908164"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="637dc41770826bff"></a>
### 기본 정보

<a id="1fe83050024d6c05"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USER_TEMP_TABLESPACE_SIZE |
| 요약 | default user temp tablespace size(byte) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 32 Mega |
| MAX | 30 Giga |
| 기본값 | 32 Mega |

<a id="471270fedcc7d43b"></a>
### 설명

사용자 temp 테이블스페이스가 생성되거나 데이터파일이 추가될 때 데이터파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="2e431b20b4b13b80"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="b064799062ab5834"></a>
### 기본 정보

<a id="0cf728ecc185ae39"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | XA_TRANSACTION_IDLE_TIMEOUT |
| 요약 | idle timeout for xa transaction |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 ( no limit ) |
| MAX | 10000000 |
| 기본값 | 60 |

<a id="663669b214f35137"></a>
### 설명

Xa transaction이 idle 상태 (XA가 시작된 후 다음 처리가 발생할 때까지 시간)로 대기할 수 있는 최대 시간이다. Idle 상태로 대기하다가 이 시간을 초과하면 xa transaction은 rollback 된다.

0으로 설정하면 XA가 idle 상태로 있더라도 무한 대기한다.

---

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
