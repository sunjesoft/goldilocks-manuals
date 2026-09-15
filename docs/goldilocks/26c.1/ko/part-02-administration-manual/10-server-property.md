<a id="e95fbf953ce3e17d"></a>

# 10. Server Property

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/e95fbf953ce3e17d)  
> 태그: `26c.1_0_tag`

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="90d59830121ce116"></a>
## Server Property 정보

Property는 다음 SQL 구문으로 변경할 수 있다.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#d0c54353bc77cbe4) 
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#2a4ad434eedabea8)

Property 정보는 다음 view로 확인할 수 있다.

- [V$PROPERTY](9-database-information.md#2432f4ad05878988): 시스템 운영 도중이나 재시작 과정에서 변경할 수 있는 property list를 보여준다.
- [V$SPROPERTY](9-database-information.md#8f509aad7adf5f5b): Binary file에서 읽어 들여 설정된 property 이거나, binary file에 저장된 property list 이다.
- [V$DB_PROPERTY](9-database-information.md#b51644ad5d756018): 데이터베이스를 생성할 때만 변경할 수 있고, 이후에는 변경할 수 없는 read-only 속성을 갖는 property list 이다.

본 매뉴얼의 property 기본 정보 각 항에 대한 설명은 다음과 같다.

<a id="de0b47319d890b4c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | Property의 구분자이다. |
| 요약 | Property 요약 설명이다. |
| Data type | Property가 갖는 값의 데이터 타입이다. |
| 적용 단계 | ALTER SYSTEM 또는 ALTER SESSION으로 변경할 수 있는 startup phase에 적용할 수 있다 * NONE: 적용할 수 있는 단계가 없다. (만약 변경 가능하지만 적용 단계가 NONE인 경우에는 SCOPE = FILE을 이용해야 한다.) |
| 변경가능 여부 | Property를 변경할 수 있는지 여부이다. * 해당 값이 TRUE일 경우, 변경할 수 있다. * 해당 값이 FALSE일 경우, read-only만 가능하다. |
| ALTER SESSION 여부 | [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#2a4ad434eedabea8) 구문으로 변경할 수 있는지 여부이다. |
| ALTER SYSTEM 여부 | [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#d0c54353bc77cbe4) 구문으로 변경할 수 있는지 여부이다. * IMMEDIATE: 수행 즉시 모든 SESSION에 변경된 값이 반영된다. * DEFERRED: 수행된 이후에 접속한 SESSION에만 변경된 값이 반영된다. 이미 접속된 SESSION에는 반영되지 않는다. * FALSE: 운영 중에는 변경된 값이 반영되지 않으며 restart 이후에 변경된 값이 반영된다. SCOPE=FILE로만 수행할 수 있다. * NONE: 변경할 수 없다. |
| MIN | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최소값이다.  VARCHAR일 경우에는 N/A이다. |
| MAX | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최대값이다. VARCHAR일 경우에는 N/A이다. |
| 기본값 | 해당 property가 갖는 기본값이다. |

<a id="561f7e058ad3c8e6"></a>
## Property Alias 정보

Property alias 정보는 [V$PROPERTY_ALIAS](9-database-information.md#99c885211178e083) view를 통해 확인할 수 있다.

본 매뉴얼에 쓰인 property alias의 기본 정보는 다음과 같다.

<a id="5928847cba6a8eac"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | Property의 원본 구분자이다. |
| ALIAS | Property alias의 구분자이다. |

Property alias 목록은 [Property Alias](../part-01-getting-started/4-what-s-new.md#f6827c242fa41236)를 참조한다.

<a id="eab109c58ee99c16"></a>
### CDISPATCHER_THREADS

[CDISPATCHER_LOCKABLE_THREADS](#90f4635804480d8e)의 alias이다.

<a id="ec1fc7a8253ddcc6"></a>
### CLUSTER_COMMIT_SLAVES

[CLUSTER_COMMIT_SLAVE_CSERVERS](#f9eab795d94a2e32)의 alias이다.

<a id="c4d356685410c45b"></a>
### CLUSTER_SERVER_RESPONSE_ QUEUE_SIZE

[CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE](#e863ea26d4e81ba4)의 alias이다.

<a id="234b69b409a7bbb4"></a>
### CSERVER

[CLUSTER_LOCKABLE_CSERVERS](#6ed3923f99bf28ff)의 alias이다.

<a id="a555b52587552a56"></a>
### INCREMENTAL_CHECKPOINT_CRITERIA

[BUFFER_DIRTY_PAGE_LIMIT](#141a470d8d601f73)의 alias이다.

<a id="28b7a2ef380785db"></a>
### INDEX_LOGGING_THROTTLING

[REDO_LOGGING_THROTTLING](#c462a3db9feff284)의 alias이다.

<a id="8514dc3803fc90a6"></a>
### INST_TABLE_BLOCK_SIZE

[INST_TABLE_PAGE_SIZE](#b38e42dbc41377ae)의 alias이다.

<a id="47316bdc7c7d96d1"></a>
### LOCKLESS_CSERVERS

[CLUSTER_LOCKLESS_CSERVERS](#7e02c0ba1098756d)의 alias이다.

<a id="90a84bfae7d953f9"></a>
### MAXIMUM_JOURNAL_REPLAY_COUNT

[ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT](#fa65edf9db034833)의 alias이다.

<a id="46f53859caa3b572"></a>
### MEMORY_MERGE_RUN_COUNT

[INDEX_MERGE_RUN_COUNT](#78503664cefabfde)의 alias이다.

<a id="88f7d51b8b3ce744"></a>
### MEMORY_SORT_RUN_SIZE

[INDEX_SORT_RUN_SIZE](#a62d8d83d47c06c9)의 alias이다.

<a id="e62842c82d708977"></a>
### ONLINE_JOURNAL_REPLAY_THRESHOLD

[ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD](#39cb80c592e7815c)의 alias이다.

<a id="98e553f99018623b"></a>
### REBALANCE_BLOCK_READ_COUNT

[ONLINE_DDL_BLOCK_READ_COUNT](#3ecfa3edb0e08bb5)의 alias이다.

<a id="3137b14c38b962c3"></a>
### REBALANCE_SHARD_DIVISOR

[ONLINE_DDL_SCAN_PARTITION](#20196df5e431393d)의 alias이다.

<a id="fa2f69180ac78d48"></a>
### SYSTEM_LOGGER_DIR

[TRACE_SYSTEM_DIR](#b3e61846fa02f601)의 alias이다.

<a id="155d2236634cc4fa"></a>
## ADMIN_SESSION_POOL_INIT_SIZE

<a id="bd8b71f54626924a"></a>
### 기본 정보

<a id="59a23f8a3956cd14"></a>
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

<a id="22d43f1fbff854ff"></a>
### 설명

Admin session pool의 초기 메모리 크기를 설정한다.

<a id="71b4c4a12163eec9"></a>
## ADMIN_SESSION_POOL_NEXT_SIZE

<a id="37c9bdf14b76b220"></a>
### 기본 정보

<a id="183bd93cc554dbfd"></a>
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

<a id="5f113ffb8fb06850"></a>
### 설명

Admin session pool의 공간을 확장할 때 session pool 내부의 메모리 크기를 얼마나 확장할지 설정한다.  
ADMIN_SESSION_POOL_INIT_SIZE가 0보다 큰 경우에만 유효하다.

<a id="12c5754d97d3626b"></a>
## AGING_INTERVAL

<a id="8e82c996fa3d7828"></a>
### 기본 정보

<a id="e19d38d0e9cdafdd"></a>
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

<a id="051f8adb3c7d4eff"></a>
### 설명

MVCC 기반의 database에서 이전 버전의 데이터를 지우는 ager thread가 처리할 job이 없을 때의 유휴 시간 (초)을 설정한다.

<a id="057ca3b036d23605"></a>
## AGING_PLAN_INTERVAL

<a id="f6ba9506cbb616c1"></a>
### 기본 정보

<a id="d94fbea9b54ca538"></a>
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
| 기본값 | 3 |

<a id="ae1b26d427732aea"></a>
### 설명

AGING_PLAN_INTERVAL 보다 오래된 SQL plan이 aging 대상이 된다.

<a id="0dcd99b270ed698c"></a>
## ARCHIVE_LOG_THROTTLING

<a id="eb327aecce580fcb"></a>
### 기본 정보

<a id="58575e13d40e8865"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ARCHIVE_LOG_THROTTLING |
| 요약 | I/O throttling threshold for redo log archiving |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 |
| 기본값 | 0 |

<a id="51ec9379a80527dc"></a>
### 설명

Redo log를 archiving할 때 디스크 I/O 성능을 제어하기 위한 프로퍼티이다.   
대상 파일로 복사된 데이터 크기가 해당 프로퍼티 값보다 커질 때마다 한 번씩 sleep 을 수행한다.

<a id="cf2debdbd62c3548"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="23a7825f689e4610"></a>
### 기본 정보

<a id="95054465559930cf"></a>
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

<a id="daca0e12a5708a4c"></a>
### 설명

GOLDILOCKS 데이터베이스의 온라인 redo log file이 archive되는 디렉토리와 미디어 복구할 때 archive redo log file을 읽을 위치를 설정한다. 온라인 redo log file은 ARCHIVELOG_DIR_1에만 archive redo log file을 생성한다.

ARCHIVELOG_DIR_1은 시스템만 설정할 수 있고 ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10은 세션을 설정할 수 있다.

<a id="fdb43ca14d8602af"></a>
## ARCHIVELOG_FILE

<a id="6045c09e045e7a53"></a>
### 기본 정보

<a id="5489eb8102850820"></a>
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

<a id="ede455593badddcd"></a>
### 설명

온라인 redo log file을 archive 할 때 archive 디렉토리에 저장되는 목적 파일 이름의 prefix를 설정한다. Archive log file은 ARCHIVELOG_FILE에 설정된 prefix에 '_'와 파일 시퀀스, 'log' 확장자가 추가된 형태로 생성된다. 예를 들어, 파일 시퀀스가 0인 로그 파일은 'archive_0.log'으로 아카이빙된다.

<a id="4f26758a283bbab9"></a>
## ARCHIVELOG_MODE

<a id="9bcc6eca98388a17"></a>
### 기본 정보

<a id="61f06f96b959819f"></a>
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

<a id="ccacf6c10bf4aedd"></a>
### 설명

Database를 생성할 때 적용되는 속성으로써 archive log mode를 다음 중 하나의 값으로 설정할 수 있다.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

Database가 생성된 후 운용되는 동안에는 archive log mode에 영향을 미치지 않고 mount 단계에서 ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}로 archive log mode를 변경할 수 있다.

<a id="8cd80a375123c946"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="801b46e34ab0a878"></a>
### 기본 정보

<a id="4bc43308b9cc6b26"></a>
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

<a id="75af01abc5200edf"></a>
### 설명

증분 백업이 수행될 때 백업 파일이 생성되고 증분 백업을 이용하여 파일을 복원할 때 백업 파일이 읽혀질 디렉토리를 설정한다. 증분 백업은 BACKUP_DIR_1에 설정된 디렉토리에만 생성된다.

BACKUP_DIR_1은 시스템만 설정할 수 있고 BACKUP_DIR_2 ~ BACKUP_DIR_10은 세션을 설정할 수 있다.

<a id="3ec5dd43bd630ca9"></a>
## BLOCK_READ_COUNT

<a id="c989b1c9dd25fd81"></a>
### 기본 정보

<a id="357c6f55462b2b81"></a>
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

<a id="9c116e19bc42c5e2"></a>
### 설명

SQL 처리시 row의 묶음 단위인 BLOCK_READ_COUNT 단위로 row를 읽어 연산을 처리한다.   
BLOCK_READ_COUNT는 연산을 수행할 때 한 번에 처리할 row의 개수를 의미하며 SQL 질의 처리에 참여하는 실행 노드간의 pipe-lining 처리의 기본 단위이다.

BLOCK_READ_COUNT 값이 크면 연산 처리 성능은 향상되지만 메모리 자원을 많이 사용한다.  따라서 10 ~ 100 사이의 값을 권장한다. 그 이상의 값을 사용하는 경우 자원 사용량은 비례하여 증가하지만 성능은 비례하여 향상되지 않는다.

<a id="cf1b738c7aec34df"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="ec284fc935fa59ef"></a>
### 기본 정보

<a id="4365c11619930ce4"></a>
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

<a id="00318d4247da7ab7"></a>
### 설명

클러스터 환경에서 인덱스를 재구축할 때 여러 멤버에서 동시에 처리할지 여부를 설정한다.

<a id="fb07120e4f25d938"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="2d9f852c8c7308b5"></a>
### 기본 정보

<a id="c8a990620cefeed6"></a>
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

<a id="ce8c84fbae18eded"></a>
### 설명

클러스터 환경에서 테이블 리밸런스를 수행할 때 여러 멤버에서 동시에 처리할 수 있는 프로토콜을 동시 처리할지 여부를 설정한다.

<a id="e0636338226aa458"></a>
## BUFFER_CACHE_SIZE

<a id="45458545f8ed7e68"></a>
### 기본 정보

<a id="077dd14bbbb06ca1"></a>
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

<a id="00e38829f09e2f36"></a>
### 설명

디스크 테이블스페이스의 페이지를 caching하는 버퍼의 크기를 설정한다.

<a id="7f8146084c596372"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

> 21c.1 이후로 지원하지 않는다.

<a id="c5028e013dbbedfc"></a>
### 기본 정보

<a id="a8d92a4f0cba2d89"></a>
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

<a id="8e3c172dc931400e"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스의 페이지들이 갱신되었을 때 체크포인트 리스트에 연결된다. 각 체크포인트 리스트는 전용 flush thread에 의해 체크포인트 리스트에 연결된 갱신된 페이지를 디스크로 flush 하는데 BUFFER_CHECKPOINT_LIST_COUNT는 체크포인트 리스트의 개수와 flush thread의 개수를 설정한다.

<a id="141a470d8d601f73"></a>
## BUFFER_DIRTY_PAGE_LIMIT

<a id="22550a42fe26f5a3"></a>
### 기본 정보

<a id="7af1e4823ad06f58"></a>
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

<a id="405190f23e6867dc"></a>
### 설명

시스템의 버퍼 캐쉬에 갱신된 페이지들은 체크포인트 할 때 디스크에 반영되는데, 버퍼 캐쉬 크기가 크고 갱신된 페이지들이 많으면 체크포인트 시간이 길어져 서비스에 영향을 미칠 수 있다. GOLDILOCKS는 시스템에서 갱신된 페이지 수가 일정 숫자 이상이 되면 갱신된 페이지들을 디스크에 반영하는 증분 체크포인트를 수행하며 BUFFER_DIRTY_PAGE_LIMIT은 증분 체크포인트를 수행하는 기준을 설정한다.

예를 들어, 이 값이 1000으로 설정되면 시스템에서 갱신된 페이지가 1000 미만일 때는 디스크에 반영되지 않고 1000 이상이 되면 버퍼의 갱신된 페이지들을 디스크에 반영한다.

기본값은 0인데 이는 무한대를 의미하고, 버퍼에 캐싱된 페이지가 모두 갱신되더라도 증분 체크포인트를 수행하지 않는다.

BUFFER_DIRTY_PAGE_LIMIT와 [INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA](#956149aa76d033fb)의 값은 재시작 복구의 시간과 서비스에 미치는 영향을 고려하여 적정하게 설정한다.

<a id="a7307b8c8b982e64"></a>
### ALIAS

<a id="209a15f13d089ccc"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | BUFFER_DIRTY_PAGE_LIMIT |
| ALIAS | INCREMENTAL_CHECKPOINT_CRITERIA |

<a id="a57fb7c3a46068c0"></a>
## BUFFER_FLUSH_THREADS

> 21c.1 이후로 지원하지 않는다.

<a id="ea39956b3d355edf"></a>
### 기본 정보

<a id="223b29b2eec47254"></a>
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

<a id="572d3226adac7cac"></a>
### 설명

버퍼 lru list에서 갱신된 페이지를 caching한 bch를 재사용하려면 flush list에 연결하여 buffer flusher에 flush를 요청하게 되는데, 이 때 BUFFER_FLUSH_THREADS가 데이터베이스에서 사용할 buffer flusher와 flush list의 수를 설정한다.

<a id="e745618b16ecfe82"></a>
## BUFFER_FLUSHING_INTERVAL

> 21c.1 이후로 지원하지 않는다.

<a id="fe855f87f853d627"></a>
### 기본 정보

<a id="3b630b8a7969b0f8"></a>
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

<a id="92938664a7f7aeb4"></a>
### 설명

갱신된 디스크 테이블스페이스 페이지들을 디스크로 flush하는 버퍼 flusher가 처리할 job이 없을 때의 유휴 시간 (sec)을 설정한다.

<a id="451d6aaf03eea354"></a>
## BUFFER_FREE_LIST_COUNT

<a id="cdcc14a5b5c73923"></a>
### 기본 정보

<a id="1bfab16794ae830f"></a>
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

<a id="5664fa95be672e45"></a>
### 설명

버퍼 캐쉬에 즉시 사용 가능한 bch들을 연결하는 buffer free list의 수를 설정한다.

<a id="73c474bfae932a28"></a>
## BUFFER_HASH_BUCKETS

<a id="156a7995f83adb05"></a>
### 기본 정보

<a id="36f09f4bf7b12eae"></a>
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

<a id="6210e39591d1740a"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스 페이지를 위한 hash bucket의 개수를 설정한다. 0 부터 1073741824 까지 설정할 수 있으며 0은 BUFFER_CACHE_SIZE에 따라 설정된 버퍼에 caching 할 수 있는 페이지 수만큼의 hash bucket을 계산하여 설정한다. 만약 설정된 값보다 버퍼의 크기가 작으면 버퍼의 크기로 hash bucket 수를 조정한다.

<a id="93aabc57645d61a1"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="cd8e92ae5d904515"></a>
### 기본 정보

<a id="114e6c22962f2ce0"></a>
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

<a id="2c9801f7cebb71db"></a>
### 설명

버퍼 lru list에서 cold region에 존재하는 페이지를 hot region으로 옮기기 위한 touch count를 설정한다.

<a id="ee8bc0d2a20fbb6b"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="68052d9542e35921"></a>
### 기본 정보

<a id="390fe07d46a87ef1"></a>
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
| 기본값 | 50 |

<a id="99557aea3e9cb721"></a>
### 설명

버퍼 lru list에 존재하는 전체 페이지 중에 hot region의 페이지의 비율 (백분율)을 설정한다.

<a id="3c2b66f302093c2f"></a>
## BUFFER_LRU_LIST_COUNT

<a id="eae190e678c2b339"></a>
### 기본 정보

<a id="3ea7a65ff2989b9b"></a>
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

<a id="c3c5ea0469c415bd"></a>
### 설명

디스크 테이블스페이스 페이지를 caching 하기 위한 free buffer가 없을 때 caching하여 사용 중인 페이지들 중에 victim을 선정하기 위한 lru list의 수를 설정한다.

<a id="1cabedb4fd0fbd38"></a>
## BUFFER_LRU_SCAN_PERCENT

<a id="eda573cf46febd5b"></a>
### 기본 정보

<a id="787deb7ee6308431"></a>
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

<a id="b00baab0c06bb147"></a>
### 설명

시스템에서 즉시 사용 가능한 free 버퍼가 없을 때, 디스크 테이블스페이스 페이지를 버퍼에 캐싱하기 위해 lru list에서 재사용 가능한 버퍼를 구한다. Lru list에서 재사용 가능한 버퍼를 구하기 위해 검사하는 페이지 수를 결정하기 위해, BUFFER_LRU_SCAN_PERCENT는 [BUFFER_CACHE_SIZE](#e0636338226aa458)에 설정된 버퍼 페이지의 퍼센트를 설정한다.

<a id="ab69691b2057d271"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="aa6f4d11a46396a4"></a>
### 기본 정보

<a id="f0efb4d35a3aa4a7"></a>
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

<a id="0619a40343f996c7"></a>
### 설명

디스크 테이블을 full scan 할 때 한 번의 디스크 IO에 사용할 최대 페이지 수를 설정한다.

<a id="d57e81e66f62000b"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="6e16592b738f78ae"></a>
### 기본 정보

<a id="456378a503166e35"></a>
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
| 기본값 | 4 |

<a id="8e689d75d6e5b8a4"></a>
### 설명

버퍼에 존재하지 않는 디스크 테이블스페이스의 페이지에 접근할 때 한 번의 디스크 I/O로 프리 페치할 인접한 최대 페이지 수를 설정한다.

<a id="c719baa25205e611"></a>
## BULK_IO_PAGE_COUNT

<a id="7d2d5e6b6a50d049"></a>
### 기본 정보

<a id="977bd9120c893fb8"></a>
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

<a id="8dd2c7099008470c"></a>
### 설명

서버를 재시작할 때 데이터 파일에 IO READ가 발생할 경우나 데이터 파일을 생성할 때 IO WRITE가 발생할 경우에 사용된다.

서버를 재시작하거나 데이터 파일을 생성할 때 BULK_IO_PAGE_COUNT * 8192 크기만큼 heap 메모리가 할당되며 세션의 PRIVATE_STATIC_AREA_SIZE가 그 크기보다 작을 경우 메모리 부족 에러가 발생할 수 있다. 이 경우에는 PRIVATE_STATIC_AREA_SIZE를 늘려주어야 한다.

<a id="2b5598521b1db7f6"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="31479515217a8983"></a>
### 기본 정보

<a id="724a6d892c8374d1"></a>
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

<a id="644673f09ff2701a"></a>
### 설명

cdispatcher에서 dequeue 할 때 busy waiting 하는 시간이다. Micro second 단위이며 이 값을 크게 하면 CPU를 많이 사용하는 대신 사용자 응답 시간 (latency)은 줄어든다.  
기본값은 0 이고 busy waiting을 하지 않는다.

<a id="90f4635804480d8e"></a>
## CDISPATCHER_LOCKABLE_THREADS

<a id="3151175edcf2e512"></a>
### 기본 정보

<a id="0d88dba24800d9d5"></a>
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

<a id="d4b3280de2717195"></a>
### 설명

Lockable 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockless 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKLESS_THREADS](#f77acbc5a4a2b5bd)로 설정한다.

<a id="3b21cc8d7fd54368"></a>
### ALIAS

<a id="e4ee7567d21fd30e"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CDISPATCHER_LOCKABLE_THREADS |
| ALIAS | CDISPATCHER_THREADS |

<a id="f77acbc5a4a2b5bd"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="9e26b54ac0c30401"></a>
### 기본 정보

<a id="c5f6eae11723b473"></a>
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

<a id="11515611f4e9e46f"></a>
### 설명

Lockless 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockable 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKABLE_THREADS](#90f4635804480d8e)로 설정한다.

<a id="92fa4b505e408cc7"></a>
## CDISPATCHER_MAX_PACKET_BUFFER_SIZE

<a id="f813ad2a9de71d2d"></a>
### 기본 정보

<a id="5ed9039ba75506e5"></a>
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

<a id="d39a3b78f6e1b68b"></a>
### 설명

cdispatcher의 데이터 송수신자가 송신하거나 수신한 패킷을 저장하는 최대 버퍼 크기를 설정한다.

<a id="69770e79c3cee6b4"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="e1f5b4cbf68a8b7a"></a>
### 기본 정보

<a id="f54750b35af229cd"></a>
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

<a id="5074db4863aba4c7"></a>
### 설명

cdispatcher socket buffer (송신자, 수신자)의 크기이다.

<a id="62049caf34a15e12"></a>
## CDISPATCHER_SYNC_THREADS

<a id="381c7dcbb9e9d56e"></a>
### 기본 정보

<a id="3875816d78a73308"></a>
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

<a id="a307463b8b37dd8d"></a>
### 설명

cdispatcher sync thread의 개수이다.

<a id="0bcec625403ff79d"></a>
## CHANGE_TRACKING

<a id="13f2b29043d9b36c"></a>
### 기본 정보

<a id="bd88fd84ac4eaef1"></a>
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

<a id="f5f428ff14c274d8"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 변경된 페이지들을 tracking 할지 여부를 설정한다.

- NO: disable change tracking
- YES: enable change tracking

데이터베이스가 archivelog로 운용 중인 경우에만 mount 이상 단계에서 ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING 으로 change tracking을 enable 할 수 있다.

<a id="be1cff326f96d642"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="b4da8296b2eb934b"></a>
### 기본 정보

<a id="ff582ac2a72f3c1c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CHANGE_TRACKING_EXTENT_SIZE |
| 요약 | number of pages to track changed of incremental backup |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 32 |
| MAX | 512 |
| 기본값 | 32 |

<a id="f0c70941ac8592b0"></a>
### 설명

Change tracking 할 때 하나의 dirty flag로 표시할 페이지 수를 설정한다. 예를 들어, 32로 설정하면 32 페이지당 하나의 dirty flag를 사용하고, 128로 설정하면 128 페이지당 하나의 dirty flag를 사용한다.

<a id="4f436a868b271594"></a>
## CHANGE_TRACKING_FILE

<a id="6b78433b866095f5"></a>
### 기본 정보

<a id="3a32555369a90c5c"></a>
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

<a id="d726482e4b883c38"></a>
### 설명

Change tracking을 저장할 파일의 디렉토리와 파일 이름을 설정한다.

<a id="502c307b879b9ff8"></a>
## CHAR_LENGTH_UNITS

<a id="d02db039519492e4"></a>
### 기본 정보

<a id="90ae2f6ef406dae9"></a>
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

<a id="5d618eafbe3e35fa"></a>
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

<a id="136f16d5d32f730b"></a>
## CHARACTER_SET

<a id="d2fa7c213a2da638"></a>
### 기본 정보

<a id="754daafb308f7676"></a>
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

<a id="3b4aaf7c062293d9"></a>
### 설명

Database의 character set이다.  
Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값을 설정할 수 있다.

<a id="48fa146f36510241"></a>
| Character set | 설명 |
| --- | --- |
| SQL_ASCII | ASCII standard |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standard |

<a id="c019c99c2e329f93"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="7f2e4f5374f1f713"></a>
### 기본 정보

<a id="24487fc82b504f45"></a>
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

<a id="29b287589bf923b0"></a>
### 설명

C/S dedicate 환경에서 client가 접속을 강제로 종료했을 경우, 이를 검사하는 주기이다. Dedicate server (gserver)가 socket을 확인하여 끊어졌으면 종료한다. 기본값은 1,000 millisecond (1초)이다.

<a id="33c593b218cba9f5"></a>
## CHECKPOINT_LIST_COUNT_PER_IO_GROUP

<a id="c851508fd1dcb710"></a>
### 기본 정보

<a id="49df1ac8bb82f1a0"></a>
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

<a id="952cec22884748c6"></a>
### 설명

[PARALLEL_IO_FACTOR](#8e9574c0ee72da5d)에 의해 설정된 각 IO slave가 처리할 체크포인트 목록의 개수를 설정한다. 갱신된 페이지를 체크포인트 목록에 연결할 때 동시성을 효율적으로 처리하기 위해 적정한 값을 지정한다. 기본값은 0인데 이 경우 각 IO slave마다 CPU 개수만큼의 체크포인트 목록을 생성하여 처리한다.

<a id="b2fbc953301336ea"></a>
## CLIENT_MAX_COUNT

<a id="e8e7a8adc98c1d88"></a>
### 기본 정보

<a id="7e4852ce1ae77488"></a>
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

<a id="c590964016974c93"></a>
### 설명

접속할 수 있는 세션의 최대 개수를 설정한다.

<a id="5c46c3e1d91e1a95"></a>
## CLIENT_NUMA_POLICY

<a id="8b1132f7c0d84218"></a>
### 기본 정보

<a id="3ae290d3597ab0a2"></a>
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

<a id="a8a2a7145d60e206"></a>
### 설명

Client 프로세스들을 NUMA 노드들에 분배하기 위한 정책을 결정한다. CLIENT_NUMA_POLICY 프로퍼티는 NUMA 프로퍼티가 on 되어있을 때 동작한다.

- 0: 세션 ID를 모듈러 (modular)해서 연결할 NUMA 노드를 결정한다.
- 1: 통계정보를 바탕으로 가장 조금 연결되어 있는 NUMA 노드에 우선적으로 연결한다.
- 2: C/S client는 TCP_CLIENT_NUMA_NODE 프로퍼티에 의해서 결정되고, D/A client는 DA_CLIENT_ NUMA_NODE 프로퍼티에 의해서 결정된다.

<a id="13a28fb181980ad8"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="89d54c482d191ab0"></a>
### 기본 정보

<a id="86bb98baace49803"></a>
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

<a id="a69592589d6bd606"></a>
### 설명

매 실행 마지막에 PSM의 child 구문을 close 한다.

<a id="ab7778eb81fcfa1b"></a>
## CLUSTER_ASYNC_COMMIT

<a id="d8bde2d204e394cd"></a>
### 기본 정보

<a id="48bb967266ca841a"></a>
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

<a id="cef96d4b4e8f094f"></a>
### 설명

Cluster system에서 내부적으로 commit protocol을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 commit을 비동기 처리하기 때문에 일시적으로 노드별 consistency가 깨어질 수 있다. 반면에 이 프로퍼티가 꺼져 있으면 commit 할 때마다 동기화하기 때문에 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="5bc5210d9031ef3d"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="9be3536a5a56e653"></a>
### 기본 정보

<a id="81444b6089127efb"></a>
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

<a id="3e978936198a62db"></a>
### 설명

Cluster의 communication buffer 크기이다.

<a id="2adac62ae9e839ef"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="4b7ff63fe4166a69"></a>
### 기본 정보

<a id="49d0d31254cac2ce"></a>
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

<a id="531ea267a500184a"></a>
### 설명

Communication read block의 크기이다.

<a id="f9eab795d94a2e32"></a>
## CLUSTER_COMMIT_SLAVE_CSERVERS

<a id="13c6d67e8f0476cd"></a>
### 기본 정보

<a id="9b8b0aca005fcd2d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_COMMIT_SLAVE_CSERVERS |
| 요약 | number of commit slave cservers |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 8 |
| 기본값 | 0 |

<a id="c8a4572c434cf8f2"></a>
### 설명

Commit slave의 개수이다.

<a id="e63e8cd4ac1f1cf9"></a>
### ALIAS

<a id="35482a072b0c06a6"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_COMMIT_SLAVE_CSERVERS |
| ALIAS | CLUSTER_COMMIT_SLAVES |

<a id="bb665643d89ee406"></a>
## CLUSTER_CONNECTION

<a id="f1c804e1c573ab1c"></a>
### 기본 정보

<a id="0f15db70cc2367a8"></a>
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

<a id="c11d72ae2b8cbbf3"></a>
### 설명

Cluster의 connection mode이다. (socket: 0, rdma:1)

<a id="70f3e1878b8530a1"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="3b5a4addd6682abc"></a>
### 기본 정보

<a id="9646fbbdc378d6ef"></a>
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

<a id="93bd946a171deee6"></a>
### 설명

Cluster 멤버간 최초 연결시 사용되는 connection timeout 이다.

<a id="002ba72bdbd332b0"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="1bd98034fc7786be"></a>
### 기본 정보

<a id="d6fab69db34ea89d"></a>
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

<a id="4d8345a9bc7e4691"></a>
### 설명

Data synchronization server의 개수이다.

<a id="284a8099bd5e1cb0"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="b18d76e52ecfb488"></a>
### 기본 정보

<a id="87a576ea4f96b873"></a>
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

<a id="66f58c9589b9d563"></a>
### 설명

Cluster dispatcher in-queue의 크기이다.

<a id="7e767168e107497e"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="5fd146952d6d79fd"></a>
### 기본 정보

<a id="a291d3f9164e8c8f"></a>
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

<a id="eb463e3c9c58fdc1"></a>
### 설명

Cluster 디스패처들이 연결될 NUMA 노드를 결정한다. CLUSTER_DISPATCHER_NUMA_STREAM_MAP 프로퍼티는 NUMA 프로퍼티가 on되어 있을 때 동작한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고 1번 스트림은 NUMA 노드 1번에 연결하며 2번 스트림은 NUMA 노드 2번에 연결한다.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="06ab218da9b3a2ca"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="6823549b6ffa4cc9"></a>
### 기본 정보

<a id="cbf9b20ef3842cb1"></a>
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

<a id="1697a557a1b905d0"></a>
### 설명

Cluster dispatcher의 out-queue 크기이다.

<a id="6651e03e26279112"></a>
## CLUSTER_FETCH_ORDER

<a id="a4f1a3c93f1f6901"></a>
### 기본 정보

<a id="02c206c6ad544551"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_FETCH_ORDER |
| 요약 | fetch order in cluster |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 0 |
| MAX | 2 |
| 기본값 | 0 |

<a id="d98ee83a7db14cb0"></a>
### 설명

Cluster puller의 fetch 우선 순위를 설정한다.

값이 0인 경우, local 노드와 remote 노드 중 먼저 fetch가 가능한 노드에서 데이터를 fetch한다.  
값이 1인 경우, local 노드에서 먼저 fetch를 수행한 후 remote 노드에서 fetch를 진행한다.  
값이 2인 경우, remote 노드에서 먼저 fetch를 수행한 후 local 노드에서 fetch를 진행한다.

<a id="e863ea26d4e81ba4"></a>
## CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE

<a id="6f43dcbbae7a93c1"></a>
### 기본 정보

<a id="f1420980e7ece5f4"></a>
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

<a id="48139e64b214628a"></a>
### 설명

원격 서버로부터 응답을 받기 위한 queue의 최대 크기를 설정한다.

<a id="c4aa97e64842e46d"></a>
### ALIAS

<a id="d23ec1ef1200f719"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_GSERVER_RESPONSE_QUEUE_SIZE |
| ALIAS | CLUSTER_SERVER_RESPONSE_QUEUE_SIZE |

<a id="a3d49f1882e8aa1f"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="d4512f953c4667f8"></a>
### 기본 정보

<a id="eae77daa474b1e58"></a>
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

<a id="13d5cbc51772e632"></a>
### 설명

Cluster의 상태를 점검하는 주기 (초)이다. 0은 비활성화 상태를 의미한다.

<a id="b49883b250ed1aa5"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="0a195a5c32f2cd5d"></a>
### 기본 정보

<a id="a79814c00f8d01fe"></a>
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

<a id="0b8c7d2b029fc94b"></a>
### 설명

Cluster 상태 점검을 다시 시도하는 횟수이다.

<a id="e59e3c8651fd3c02"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="5d35df38aff0bcdb"></a>
### 기본 정보

<a id="de8e694682929bb3"></a>
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

<a id="1d9ab6f03409162d"></a>
### 설명

Cluster의 in-active 멤버를 무시한다.

<a id="55fb5df5b3c523af"></a>
## CLUSTER_KEEPALIVE_IDLE_TIME

<a id="c6a75b6580466aa6"></a>
### 기본 정보

<a id="4f8b88d1a7dac5e4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_KEEPALIVE_IDLE_TIME |
| 요약 | The number of seconds a cluster connection needs to be idle |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 16383 |
| 기본값 | 0 |

<a id="1d4d88ea94f5e7a0"></a>
### 설명

Keep alive packet을 송신하기 전에 cluster session과 cdispatcher 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, CLUSTER_KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 cdispatcher 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

기본값은 0 이며, 이 경우 keep alive 기능을 사용하지 않는다.

<a id="6ed3923f99bf28ff"></a>
## CLUSTER_LOCKABLE_CSERVERS

<a id="18e61ee8afdc6218"></a>
### 기본 정보

<a id="84531e7787680f70"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_LOCKABLE_CSERVERS |
| 요약 | number of lockable cserver processes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="643d3c71e5dda29f"></a>
### 설명

Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수는 [CLUSTER_LOCKLESS_CSERVERS](#7e02c0ba1098756d)로 설정한다.

<a id="50cbd5bf6cc6bfa4"></a>
### ALIAS

<a id="a8bfda21c4dda12e"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_LOCKABLE_CSERVERS |
| ALIAS | CSERVERS |

<a id="7e02c0ba1098756d"></a>
## CLUSTER_LOCKLESS_CSERVERS

<a id="13c476ac604049d1"></a>
### 기본 정보

<a id="8c1d5f00234623f1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_LOCKLESS_CSERVERS |
| 요약 | number of lockless cserver processes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="988b7a87c7918b2d"></a>
### 설명

Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수는 [CLUSTER_LOCKABLE_CSERVERS](#6ed3923f99bf28ff)로 설정한다.

<a id="53891e8b3337000e"></a>
### ALIAS

<a id="6ea7ee6bd4f0f3f5"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | CLUSTER_LOCKLESS_CSERVERS |
| ALIAS | LOCKLESS_CSERVERS |

<a id="31e3eb5e6aa8286c"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="ca3b0534f9b2595f"></a>
### 기본 정보

<a id="9fa558f858ed2a47"></a>
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

<a id="e6aaaffad75165c4"></a>
### 설명

원격 프로토콜이 한 번에 전송할 수 있는 패킷의 최대 크기를 결정한다. 원격으로 전송해야 하는 column의 크기가 CLUSTER_MAX_PACKET_SIZE 프로퍼티 크기를 초과할 경우, 해당 프로퍼티를 column 크기보다 크게 설정해야 한다.

<a id="542111a1250a11c2"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="76c667e223138437"></a>
### 기본 정보

<a id="b8a65498dbc51c77"></a>
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

<a id="ad45579e3402bf05"></a>
### 설명

원격으로 전송되는 클러스터 패킷은 여러 개의 piece로 나뉘어 전달될 수 있는데 CLUSTER_MAX_PAYLOAD_SIZE 프로퍼티는 하나의 piece에 저장할 수 있는 데이터의 최대 크기를 설정한다.

<a id="77f76dfe4a2a2a6a"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="f876205f54cc8a97"></a>
### 기본 정보

<a id="315c160a5316e2e4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CLUSTER_PACKET_ALLOCATION_TIMEOUT |
| 요약 | a time limit (sec) for how long statements will wait to allocate packet memory |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 100000000 |
| 기본값 | 3 |

<a id="3f04c8242ca357f1"></a>
### 설명

Cluster 패킷 구성에 필요한 메모리를 할당할 때 기다릴 수 있는 최대 시간 (초)을 설정한다.

<a id="aa7b0d6bf3026e5d"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="907ef5e1bea1fbb7"></a>
### 기본 정보

<a id="71c4a8912519345f"></a>
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

<a id="e62e5fba8dc71f9b"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Failover 시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, session을 종료시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#5dfb637b7c839ca6) property를 사용하여 제한 시간을 설정한다.

<a id="5dfb637b7c839ca6"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="4526c5e1de77b14e"></a>
### 기본 정보

<a id="d242a7305999c8a7"></a>
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

<a id="c8741271ab42f3b1"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Session을 종료시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, failover 시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#aa7b0d6bf3026e5d) property를 사용하여 제한 시간을 설정한다.

<a id="a64f5e37bc269a4d"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="90b51c25afb3cd00"></a>
### 기본 정보

<a id="dd17189036dfb32c"></a>
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

<a id="6524b9c097f51dc8"></a>
### 설명

Cluster session을 관리하기 위한 hash bucket의 개수를 설정한다.

<a id="5165de282789b915"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="da7cf50ca7c9f0fe"></a>
### 기본 정보

<a id="d50f1f1de6663e79"></a>
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

<a id="3695851a92f5516a"></a>
### 설명

Cluster system에서 split-brain 상황을 해결하기 위한 정책을 설정한다. 1 이상의 값으로 설정할 경우 해결 방안을 locator에게 질의한다.

> Locator에게 한 질의에 timeout이 발생하면 CLUSTER_SPLIT_BRAIN_RETRY_COUNT만큼 질의를 시도한다. 재시도에 실패하면 속성값이 1인 경우에는 failover를 강제로 진행하고 속성값이 2인 경우에는 fatal 종료한다.

<a id="4efadad9e0fc200e"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="5ef6a0a6f90a8975"></a>
### 기본 정보

<a id="76d665fb2c0f4a9d"></a>
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

<a id="7fa64a48ed11fdb8"></a>
### 설명

Cluster system에서 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 이상으로 설정되었을 경우에 사용된다. Locator에게 보낸 질의에 응답이 없을 경우, 질의를 다시 시도하는 횟수를 설정한다.

<a id="476a6d45a16d4345"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="550c91056e45c3ed"></a>
### 기본 정보

<a id="89c9b81b14bcf16b"></a>
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

<a id="beae77f47c52a6ee"></a>
### 설명

Commit cserver가 commit protocol 메시지를 읽기 위해 deque 할 때 busy waiting의 기준 시간 간격을 설정한다. 만약 1000000 (1초)로 설정할 경우, 이전 deque에 성공한 이후 다시 deque를 시도할 때까지 1 초를 경과하지 않았다면 deque에서의 대기시간 (timeout)을 0으로 설정하여 busy waiting 한다.

<a id="72b1dccfe8c6e8ce"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="fd289cc2ad9dd1ea"></a>
### 기본 정보

<a id="8198eb001770e084"></a>
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

<a id="9a51dcf4bba6f8f5"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화해야 하는데 이 때 각 control file이 저장될 디렉토리와 파일 이름을 설정한다.

<a id="1c24227d83a9884f"></a>
## CONTROL_FILE_COUNT

<a id="de942ef11c7e4e22"></a>
### 기본 정보

<a id="a1058cf8455b6a27"></a>
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

<a id="491419e2948bafc4"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화한다. CONTROL_FILE_COUNT는 control file의 다중화 개수를 설정하며 최소 두 개에서 최대 여덟 개까지 다중화할 수 있다.

<a id="a2700b39bdd7e097"></a>
## CONTROL_FILE_TEMP_NAME

> 26c.1 이후로 지원하지 않는다.

<a id="f06271699c417ac5"></a>
### 기본 정보

<a id="2cebdc08d9e10a11"></a>
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

<a id="69fed0e1607a36f3"></a>
### 설명

Database를 운용하는 중에 control file은 수시로 변경되고 필요할 경우 임시로 복사본을 만들 수도 있다. CONTROL_FILE_TEMP_NAME은 control file이 임시로 저장되는 디렉토리와 파일 이름을 설정한다.

<a id="b5fc46e47fd703cd"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="31474059e2e193bd"></a>
### 기본 정보

<a id="e97f4208e219c4dd"></a>
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

<a id="66d12db0c5bced04"></a>
### 설명

조정자 (coordinator)에 적용되는 commit write mode 이다. 만약 TRANSACTION_COMMIT_WRITE_MODE가 "no wait"이고 해당 프로퍼티가 "wait" 인 경우라면 조정자 노드는 "wait"으로 동작하고 그 외 노드들은 "no wait"으로 동작한다.

<a id="24e8a78fda8fbdbd"></a>
## DA_CLIENT_NUMA_NODE

<a id="3b788d83c0e4c31f"></a>
### 기본 정보

<a id="032b747065efba04"></a>
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

<a id="c43f0cacac40cbb1"></a>
### 설명

Direct Access (D/A) 세션이 바인드 될 NUMA 노드 ID를 설정한다. DA_CLIENT_NUMA_NODE는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="4d90e51f0ead51f5"></a>
## DATA_STORE_MODE

<a id="712df8382a63fb01"></a>
### 기본 정보

<a id="f3b55db8465c0ff5"></a>
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

<a id="60f66cb63dbafe7f"></a>
### 설명

Database의 저장 방식을 설정한다.

- 1: CDS 모드는 다중 사용자에 대한 동시성은 지원하지만 영속성은 보장하지 않는다. 즉, data 삽입/ 삭제/ 갱신을 비롯하여 database를 변경하는 모든 연산에 대한 로그를 기록하지 않기 때문에 장애가 발생할 경우 복구할 수도 없다.
- 2: TDS 모드는 다중 사용자에 대한 동시성 및 로그를 이용한 영속성을 보장한다.

<a id="034d1b5a7c4fdbec"></a>
## DATABASE_INSTANCE_NAME

<a id="1f7099a19f588691"></a>
### 기본 정보

<a id="68599b21ed930b2a"></a>
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

<a id="74fc49122a061138"></a>
### 설명

데이터베이스의 instance 이름이다.

<a id="4d26ef77988c6c4b"></a>
## DDL_AUTOCOMMIT

<a id="dae727e3ec148a51"></a>
### 기본 정보

<a id="594c647dea01b507"></a>
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

<a id="11f19931e02772dd"></a>
### 설명

Autocommit이 적용되지 않는 DDL에 대한 autocommit 여부를 설정한다. 예를 들어, table의 생성과 변경에는 autocommit이 적용되지 않기 때문에 DDL_AUTOCOMMIT이 '0'인 경우 rollback을 수행하여 table 생성과 변경을 철회할 수 있다. 이에 반해 DDL_AUTOCOMMIT을 '1'로 설정하면 autocommit이 적용되지 않는 DDL들이 즉시 commit 된다.

<a id="4cceb35f6411d58d"></a>
## DDL_LOCK_TIMEOUT

<a id="ddce8aa4a49c194e"></a>
### 기본 정보

<a id="20bd88c06b232b8b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DDL_LOCK_TIMEOUT |
| 요약 | a time limit (sec) for how long DDL statements will wait |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 100000000 |
| 기본값 | 0 |

<a id="e966305257777046"></a>
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

<a id="2bdee70d513b1be3"></a>
## DEADLOCK_PRIORITY

<a id="bb71e9354c8a5984"></a>
### 기본 정보

<a id="abe2960d2ead43f4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEADLOCK_PRIORITY |
| 요약 | importance to choose deadlock victim |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 9 |
| 기본값 | 5 |

<a id="5c93c744b5c52b2a"></a>
### 설명

다수의 트랜잭션을 동시에 수행하다가 deadlock이 발생할 경우, deadlock을 유발한 트랜잭션들 중에서 weight 값이 낮은 트랜잭션을 victim으로 선택하여 deadlock을 해결한다. 이 속성값이 상대적으로 높은 세션에서 시작된 트랜잭션과, 이 속성값이 더 낮은 세션에서 시작된 트랜잭션 사이에서 deadlock이 발생하면, 이 속성값이 더 낮은쪽 트랜잭션이 deadlock victim으로 선택된다. Deadlock이 발생했을 때 어느 트랜잭션을 우선적으로 처리할 것인가에 따라 이 속성값을 설정해야 한다.

이 속성값을 설정한 후에 트랜잭션을 시작해야 이 값이 해당 트랜잭션의 weight으로 적용되며, 트랜잭션이 시작된 후에는 이 값을 변경하더라도 트랜잭션의 weight는 변경되지 않음에 유의해야 한다.

<a id="e267ca9cbac98bef"></a>
## DEFAULT_ASC_NULLS_ORDER

<a id="c2726c2a2fc34c9c"></a>
### 기본 정보

<a id="6f2dff55128747eb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_ASC_NULLS_ORDER |
| 요약 | default nulls order for ascending sort (0:nulls_first, 1:nulls_last) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 1 |

<a id="f46566e8db278d73"></a>
### 설명

Sort order가 ascending이고 nulls order가 생략된 경우 기본 nulls order 값을 설정한다. 이 값이 0 이면 NULLS FIRST 이고, 1 이면 NULLS LAST 이다.

Property 값은 서버를 구동할 때 시스템에 적용된다.

Sort order가 ascending인 경우, DBMS별 Default Nulls Order는 다음과 같다.

- NULLS FIRST: MSSQL, MySQL, SQLite
- NULLS LAST (default): PostgreSQL, ORACLE, DB2

<a id="2393f609968f19d8"></a>
## DEFAULT_DESC_NULLS_ORDER

<a id="6d03cdd5c69d128b"></a>
### 기본 정보

<a id="330cf67840fb4880"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_DESC_NULLS_ORDER |
| 요약 | default nulls order for descending sort (0:nulls_first, 1:nulls_last) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 1 |

<a id="e24f816abb00d7f9"></a>
### 설명

Sort order가 descending이고 nulls order가 생략된 경우 기본 nulls order 값을 설정한다. 이 값이 0 이면 NULLS FIRST 이고, 1 이면 NULLS LAST 이다.

Property 값은 서버를 구동할 때 시스템에 적용된다.

Sort order가 descending인 경우, DBMS별 Default Nulls Order는 다음과 같다.

- NULLS FIRST: PostgreSQL, ORACLE, DB2
- NULLS LAST (default): MSSQL, MySQL, SQLite

<a id="c51bcdce7adcc3db"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="28381b165de3cacb"></a>
### 기본 정보

<a id="66873893f39735d3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION |
| 요약 | specifies whether or not create global secondary index at table creation |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 1 |
| 기본값 | YES |

<a id="b611aaa2c31d3e80"></a>
### 설명

Cluster system에서 테이블을 생성할 때 global secondary index를 생성할지 여부를 설정한다. Global secondary index를 생성하지 않은 테이블에 대한 non-deterministic 질의는 실패한다. NO로 설정한 상태에서 테이블을 생성한 후에 별도로 global secondary index를 생성할 수도 있다.

<a id="31409c1bdec8fa63"></a>
## DEFAULT_INDEX_LOGGING

> 3.2 이후로 지원하지 않는다.

<a id="39ed2304b3ba3c08"></a>
### 기본 정보

<a id="2a94fee75b9913db"></a>
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

<a id="bc90ee12a569e6aa"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 LOGGING 속성을 지정하지 않은 경우, LOGGING 속성은 DEFAULT_INDEX_LOGGING 프로퍼티 값으로 설정된다. 만약 인덱스가 LOGGING 테이블스페이스에 생성되면 반드시 LOGGING 속성이 설정되어야 한다.

<a id="a70319f95fa6c573"></a>
## DEFAULT_INDEX_PCTFREE

<a id="278af7d1a08856f4"></a>
### 기본 정보

<a id="0430fb8619880c4b"></a>
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

<a id="731ab2f765ec5327"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_INDEX_PCTFREE 프로퍼티 값으로 설정된다.

<a id="4b46ffe9ed49a55e"></a>
## DEFAULT_INITRANS

<a id="098a7ba83cca03a5"></a>
### 기본 정보

<a id="df90ba4429bc2700"></a>
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

<a id="592f6851df9237aa"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 INITRANS 구문을 지정하지 않은 경우 INITRANS는 DEFAULT_INITRANS 프로퍼티 값으로 설정된다.

<a id="38446e3a7bf4bd60"></a>
## DEFAULT_MAXTRANS

<a id="b373bdbc80fbc83e"></a>
### 기본 정보

<a id="a9d653fedf2f8596"></a>
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

<a id="6cacaf58c588fa39"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 MAXTRANS 구문을 지정하지 않은 경우 MAXTRANS는 DEFAULT_MAXTRANS 프로퍼티 값으로 설정된다.

<a id="6d97856e81b980b8"></a>
## DEFAULT_PCTFREE

<a id="f5c537bf98523139"></a>
### 기본 정보

<a id="4b6954ab7962d90c"></a>
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

<a id="e54369e3ff289a2e"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_PCTFREE 프로퍼티 값으로 설정된다.

<a id="213c6fa1427ed9d7"></a>
## DEFAULT_PCTUSED

<a id="adf04945b64d387f"></a>
### 기본 정보

<a id="1f68a0b19ebac15d"></a>
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

<a id="3c6c8582ef26fd9e"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTUSED 구문을 지정하지 않은 경우 PCTUSED는 DEFAULT_PCTUSED 프로퍼티 값으로 설정된다.

<a id="fcdbb849f5c36dc2"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="095d0785d76fdb55"></a>
### 기본 정보

<a id="eb431a0e9f4fd8be"></a>
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

<a id="790f6fd324e0c71e"></a>
### 설명

백업 목록을 삭제할 때 백업 파일을 삭제할지 여부를 지정한다.

<a id="da8225b734ea8612"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="d05f3961a0043411"></a>
### 기본 정보

<a id="c9ef8edee7936dc4"></a>
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

<a id="463bf95dba4f87cd"></a>
### 설명

INCREMENTAL BACKUP을 수행할 때 obsolete 된 이전 백업 목록의 삭제 여부를 설정한다.

<a id="1a409609d661f5ac"></a>
## DEFAULT_SHARDING

<a id="bafce037885a91e5"></a>
### 기본 정보

<a id="b063a342c73bb7b9"></a>
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

<a id="77be169fe4e4812b"></a>
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

<a id="6699008d62da0603"></a>
## DISABLE_DDL

<a id="1ca3dbba90d3d48f"></a>
### 기본 정보

<a id="d41ed3a79a9314ff"></a>
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

<a id="48e9daeff065a97b"></a>
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
ALTER DATABASE ADD LOGFILE GROUP                         
ALTER DATABASE ADD LOGFILE MEMBER                        
ALTER DATABASE ARCHIVELOG                                
ALTER DATABASE CLEAR AUDIT TRAIL                         
ALTER DATABASE CLEAR PASSWORD HISTORY                    
ALTER DATABASE DATAFILE AUTOEXTEND ..                    
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS             
ALTER DATABASE DROP LOGFILE GROUP                        
ALTER DATABASE DROP LOGFILE MEMBER                       
ALTER DATABASE NOARCHIVELOG                              
ALTER DATABASE RENAME CHANGE TRACKING                    
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE         
ALTER DATABASE RENAME LOGFILE                            
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                
ALTER FUNCTION                                           
ALTER INDEX .. DISABLE                                   
ALTER INDEX .. ENABLE                                    
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
ALTER TABLE .. DROP UNUSABLE SEGMENTS                    
ALTER TABLE .. MERGE SHARDS .. INTO ..                   
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..         
ALTER TABLE .. OFFLINE INACTIVE CLUSTER MEMBERS          
ALTER TABLE .. READ ONLY                                 
ALTER TABLE .. READ WRITE                                
ALTER TABLE .. REBALANCE ..                              
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX            
ALTER TABLE .. RENAME COLUMN                             
ALTER TABLE .. RENAME CONSTRAINT                         
ALTER TABLE .. RENAME SHARD .. TO ..                     
ALTER TABLE .. RENAME TO ..                              
ALTER TABLE .. REORGANIZE                                
ALTER TABLE .. SET TRIGGER ORDER ..                      
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
ALTER TRIGGER .. COMPILE                                 
ALTER TRIGGER .. DISABLE                                 
ALTER TRIGGER .. ENABLE                                  
ALTER TRIGGER .. RENAME TO ..                            
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
CREATE LIBRARY                                           
CREATE PACKAGE                                           
CREATE PACKAGE BODY                                      
CREATE PROCEDURE                                         
CREATE PROFILE                                           
CREATE ROLE                                              
CREATE SCHEMA                                            
CREATE SEQUENCE                                          
CREATE SYNONYM                                           
CREATE TABLE                                             
CREATE TABLE ... AS SELECT                               
CREATE TABLESPACE                                        
CREATE TRIGGER                                           
CREATE USER                                              
CREATE VIEW                                              
DROP AUDIT POLICY                                        
DROP CLUSTER GROUP                                       
DROP FUNCTION                                            
DROP INDEX                                               
DROP LIBRARY                                             
DROP PACKAGE                                             
DROP PROCEDURE                                           
DROP PROFILE                                             
DROP ROLE                                                
DROP SCHEMA                                              
DROP SEQUENCE                                            
DROP SYNONYM                                             
DROP TABLE                                               
DROP TABLESPACE                                          
DROP TRIGGER                                             
DROP USER                                                
DROP VIEW                                                
FLASHBACK TABLE                                          
GRANT .. ON DATABASE                                     
GRANT .. ON LIBRARY                                      
GRANT .. ON PACKAGE                                      
GRANT .. ON PROCEDURE                                    
GRANT .. ON SCHEMA                                       
GRANT .. ON TABLE                                        
GRANT .. ON TABLESPACE                                   
GRANT USAGE ON ..                                        
GRANT role TO                                            
NOAUDIT POLICY                                           
PURGE CONSTRAINT                                         
PURGE DBA_RECYCLEBIN                                     
PURGE INDEX                                              
PURGE RECYCLEBIN                                         
PURGE TABLE                                              
PURGE TABLESPACE                                         
PURGE TRIGGER                                            
REVOKE .. ON DATABASE                                    
REVOKE .. ON LIBRARY                                     
REVOKE .. ON PACKAGE                                     
REVOKE .. ON PROCEDURE                                   
REVOKE .. ON SCHEMA                                      
REVOKE .. ON TABLE                                       
REVOKE .. ON TABLESPACE                                  
REVOKE USAGE ON ..                                       
REVOKE role TO                                           
TRUNCATE TABLE                                           

149 rows selected.
```

<a id="7b4b33d6b19ca33f"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="5f104d0574921902"></a>
### 기본 정보

<a id="47033cf069ed71c6"></a>
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

<a id="4851ccb425629ec0"></a>
### 설명

CDC의 give up에 영향을 미치는 supplemental log 대상 테이블에 대한 DDL 수행을 금지한다.  
관련 DDL은 [DDL 구문에 따른 give up 발생 및 절차에 따른 허용 여부](../part-07-replication/55-cyclone.md#0c96c385c72c2d01)를 참조한다.

<a id="b384460d22688e8c"></a>
## DISABLE_SERIAL_DDL

<a id="4e72bb5b6ffda186"></a>
### 기본 정보

<a id="5477b14b2f593946"></a>
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

<a id="ab95f98fa52e3871"></a>
### 설명

Cluster 환경에서 DDL은 [Cluster의 DDL 처리](../part-03-sql-manual/12-sql-languages.md#146a58645f8d10c9)에 설명된 것처럼 모든 cluster member 들을 순차적으로 lock을 획득한 후 수행한다.    
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

COMMAND                                           IS_DDL CLUSTER_LOCK_MODE
------------------------------------------------- ------ -----------------
ALTER AUDIT POLICY                                YES    SERIAL           
ALTER DATABASE CLEAR AUDIT TRAIL                  YES    SERIAL           
ALTER DATABASE CLEAR PASSWORD HISTORY             YES    SERIAL           
ALTER DATABASE DATAFILE AUTOEXTEND ..             YES    SERIAL           
ALTER FUNCTION                                    YES    SERIAL           
ALTER INDEX .. DISABLE                            YES    SERIAL           
ALTER INDEX .. ENABLE                             YES    SERIAL           
ALTER INDEX .. REBUILD                            YES    SERIAL           
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
ALTER TABLE .. DROP UNUSABLE SEGMENTS             YES    SERIAL           
ALTER TABLE .. READ ONLY                          YES    SERIAL           
ALTER TABLE .. READ WRITE                         YES    SERIAL           
ALTER TABLE .. REBUILD GLOBAL SECONDARY INDEX     YES    SERIAL           
ALTER TABLE .. RENAME COLUMN                      YES    SERIAL           
ALTER TABLE .. RENAME CONSTRAINT                  YES    SERIAL           
ALTER TABLE .. RENAME SHARD .. TO ..              YES    SERIAL           
ALTER TABLE .. RENAME TO ..                       YES    SERIAL           
ALTER TABLE .. SET TRIGGER ORDER ..               YES    SERIAL           
ALTER TABLE .. SET UNUSED COLUMN                  YES    SERIAL           
ALTER TABLE .. STORAGE                            YES    SERIAL           
ALTER TABLESPACE .. ADD                           YES    SERIAL           
ALTER TABLESPACE .. DROP                          YES    SERIAL           
ALTER TABLESPACE .. OFFLINE                       YES    SERIAL           
ALTER TABLESPACE .. ONLINE                        YES    SERIAL           
ALTER TABLESPACE .. RENAME TO                     YES    SERIAL           
ALTER TABLESPACE .. RENAME { DATAFILE | MEMORY }  YES    SERIAL           
ALTER TRIGGER .. COMPILE                          YES    SERIAL           
ALTER TRIGGER .. DISABLE                          YES    SERIAL           
ALTER TRIGGER .. ENABLE                           YES    SERIAL           
ALTER TRIGGER .. RENAME TO ..                     YES    SERIAL           
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
CREATE LIBRARY                                    YES    SERIAL           
CREATE PACKAGE                                    YES    SERIAL           
CREATE PACKAGE BODY                               YES    SERIAL           
CREATE PROCEDURE                                  YES    SERIAL           
CREATE PROFILE                                    YES    SERIAL           
CREATE ROLE                                       YES    SERIAL           
CREATE SCHEMA                                     YES    SERIAL           
CREATE SEQUENCE                                   YES    SERIAL           
CREATE SYNONYM                                    YES    SERIAL           
CREATE TABLE                                      YES    SERIAL           
CREATE TABLE ... AS SELECT                        YES    SERIAL           
CREATE TABLESPACE                                 YES    SERIAL           
CREATE TRIGGER                                    YES    SERIAL           
CREATE USER                                       YES    SERIAL           
CREATE VIEW                                       YES    SERIAL           
DROP AUDIT POLICY                                 YES    SERIAL           
DROP FUNCTION                                     YES    SERIAL           
DROP INDEX                                        YES    SERIAL           
DROP LIBRARY                                      YES    SERIAL           
DROP PACKAGE                                      YES    SERIAL           
DROP PROCEDURE                                    YES    SERIAL           
DROP PROFILE                                      YES    SERIAL           
DROP ROLE                                         YES    SERIAL           
DROP SCHEMA                                       YES    SERIAL           
DROP SEQUENCE                                     YES    SERIAL           
DROP SYNONYM                                      YES    SERIAL           
DROP TABLE                                        YES    SERIAL           
DROP TABLESPACE                                   YES    SERIAL           
DROP TRIGGER                                      YES    SERIAL           
DROP USER                                         YES    SERIAL           
DROP VIEW                                         YES    SERIAL           
FLASHBACK TABLE                                   YES    SERIAL           
GRANT .. ON DATABASE                              YES    SERIAL           
GRANT .. ON LIBRARY                               YES    SERIAL           
GRANT .. ON PACKAGE                               YES    SERIAL           
GRANT .. ON PROCEDURE                             YES    SERIAL           
GRANT .. ON SCHEMA                                YES    SERIAL           
GRANT .. ON TABLE                                 YES    SERIAL           
GRANT .. ON TABLESPACE                            YES    SERIAL           
GRANT USAGE ON ..                                 YES    SERIAL           
GRANT role TO                                     YES    SERIAL           
NOAUDIT POLICY                                    YES    SERIAL           
PURGE CONSTRAINT                                  YES    SERIAL           
PURGE DBA_RECYCLEBIN                              YES    SERIAL           
PURGE INDEX                                       YES    SERIAL           
PURGE RECYCLEBIN                                  YES    SERIAL           
PURGE TABLE                                       YES    SERIAL           
PURGE TABLESPACE                                  YES    SERIAL           
PURGE TRIGGER                                     YES    SERIAL           
REVOKE .. ON DATABASE                             YES    SERIAL           
REVOKE .. ON LIBRARY                              YES    SERIAL           
REVOKE .. ON PACKAGE                              YES    SERIAL           
REVOKE .. ON PROCEDURE                            YES    SERIAL           
REVOKE .. ON SCHEMA                               YES    SERIAL           
REVOKE .. ON TABLE                                YES    SERIAL           
REVOKE .. ON TABLESPACE                           YES    SERIAL           
REVOKE USAGE ON ..                                YES    SERIAL           
REVOKE role TO                                    YES    SERIAL           
TRUNCATE TABLE                                    YES    SERIAL           

125 rows selected.
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
ALTER DATABASE ADD LOGFILE GROUP                          YES    NONE             
ALTER DATABASE ADD LOGFILE MEMBER                         YES    NONE             
ALTER DATABASE ARCHIVELOG                                 YES    NONE             
ALTER DATABASE DROP INACTIVE CLUSTER MEMBERS              YES    MANUAL           
ALTER DATABASE DROP LOGFILE GROUP                         YES    NONE             
ALTER DATABASE DROP LOGFILE MEMBER                        YES    NONE             
ALTER DATABASE NOARCHIVELOG                               YES    NONE             
ALTER DATABASE RENAME CHANGE TRACKING                     YES    NONE             
ALTER DATABASE RENAME GLOBAL TRANSACTION LOGFILE          YES    NONE             
ALTER DATABASE RENAME LOGFILE                             YES    NONE             
ALTER DATABASE RESET LOCAL CLUSTER MEMBER                 YES    NONE             
ALTER SEQUENCE .. SYNCHRONIZE                             YES    MANUAL           
ALTER SYSTEM SWITCH LOGFILE                               YES    NONE             
ALTER TABLE .. MERGE SHARDS .. INTO ..                    YES    MANUAL           
ALTER TABLE .. MOVE SHARD .. TO CLUSTER GROUP ..          YES    MANUAL           
ALTER TABLE .. OFFLINE INACTIVE CLUSTER MEMBERS           YES    MANUAL           
ALTER TABLE .. REBALANCE ..                               YES    MANUAL           
ALTER TABLE .. REORGANIZE                                 YES    MANUAL           
ALTER TABLE .. SPLIT SHARD .. INTO .. AT CLUSTER GROUP .. YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE ..                             YES    MANUAL           
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

24 rows selected.
```

<a id="b775fee01e3b2a48"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="0dc9bbac059ef45f"></a>
### 기본 정보

<a id="95ce3523be33074d"></a>
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

<a id="f40b58704fed5de7"></a>
### 설명

CDC give up을 유발한 UPDATE primary key를 비활성화 한다.

<a id="e4dcc9e115cada07"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="c29db5c69adffcaa"></a>
### 기본 정보

<a id="9d2693a40698e7dc"></a>
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

<a id="a0fd402e479b31d0"></a>
### 설명

TARGETTYPE protocol을 허용하지 않는다.

<a id="d1562f17ca6ba5f8"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="afd2be4bb229175f"></a>
### 기본 정보

<a id="e5e403c8217f23cb"></a>
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

<a id="3292a91a20be386a"></a>
### 설명

TARGETTYPE_WITH_ALL protocol을 허용하지 않는다.

<a id="ba55043dea200966"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="19db3c407473c5d1"></a>
### 기본 정보

<a id="8bd7181e1cf23011"></a>
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

<a id="22291d98e3c6a059"></a>
### 설명

TARGETTYPE_WITH_NAME protocol을 허용하지 않는다.

<a id="8ea1fbc41a34f73f"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="852cd5351edb8452"></a>
### 기본 정보

<a id="aab58b83ed0f8aa5"></a>
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

<a id="0640baccd0661f22"></a>
### 설명

Shared 모드에서 사용하는 전체 communication buffer 크기로써 Shared Static Area (SSA) 내에 할당되어 사용된다.

<a id="5ec011cf53180e75"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="3fb27fd066ce140d"></a>
### 기본 정보

<a id="27ba40afbb3b649e"></a>
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

<a id="2b5c783b6485f99b"></a>
### 설명

Shared 모드에서 dispatcher가 관리하는 unit의 크기이다. 이 크기가 크면 메모리가 낭비되고 이 크기가 작으면 성능이 저하될 수 있다.  
Shared 모드에서 통신 packet의 최대 크기로 설정된다.

<a id="47fd6ba48a2a65c5"></a>
## DISPATCHER_CONNECTIONS

<a id="047d806ff6a5e155"></a>
### 기본 정보

<a id="57b870008a21e627"></a>
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

<a id="723d81ff03d205ed"></a>
### 설명

Shared 모드에서 하나의 dispatcher가 관리할 수 있는 최대 connection (client)의 개수이다.  
시스템에서 지원하는 최대값이 설정값보다 작으면 내부적으로 시스템 최대값으로 설정된다.

<a id="67612afa85850539"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="7fe63a1c5a4f0ce7"></a>
### 기본 정보

<a id="422fe107bf10aabd"></a>
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

<a id="03138973ad487cdc"></a>
### 설명

Busy waiting에 대한 dispatcher dequeue 주기이다. (micro second)

<a id="118dc7a03c3436aa"></a>
## DISPATCHER_LOAD_BALANCING

<a id="00d0cb1934f5c16c"></a>
### 기본 정보

<a id="74ffe2cfab5fecf9"></a>
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

<a id="2ac3d0f8c7d70fda"></a>
### 설명

Shared 모드에서 client에 접속할 때 dispatcher를 할당하는 알고리즘이다.

- 0: 현재 연결된 client 수가 적은 dispatcher에 할당한다.
- 1: 순차적으로 dispatcher에 할당한다.

<a id="66c3a99c472db4df"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="235672cfaadaa6a6"></a>
### 기본 정보

<a id="83a4c102ce8083a5"></a>
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

<a id="c8983fddd51f982e"></a>
### 설명

디스패처들이 연결될 NUMA 노드를 결정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고, 1번 스트림은 NUMA 노드 1번에 연결하고, 2번 스트림은 NUMA 노드 2번에 연결한다.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="03a3866f024b2618"></a>
## DISPATCHER_QUEUE_SIZE

<a id="679dd8e77fd15752"></a>
### 기본 정보

<a id="286b998042099cdd"></a>
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

<a id="7216c279f5b16b3b"></a>
### 설명

Shared 모드에서 dispatcher와 shared-server 간의 통신을 위한 queue 크기를 설정한다.

<a id="f276656cb1a27559"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="0022020dd6e0306d"></a>
### 기본 정보

<a id="aff2b89cd31c6908"></a>
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

<a id="b4b4fd364152a3bb"></a>
### 설명

각 response queue의 mini queue 개수이다.

<a id="9b714d48a46cd94b"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="6a0e79228f7a4dd9"></a>
### 기본 정보

<a id="f93e07845d0a38ee"></a>
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

<a id="eccd7f452b8f9d24"></a>
### 설명

각 request queue의 mini queue 개수이다.

<a id="32050d911bfa3799"></a>
## DISPATCHERS

<a id="c6b4d54994e5317b"></a>
### 기본 정보

<a id="8bd1439a5ed98440"></a>
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

<a id="457e2ad08a6e5140"></a>
### 설명

Shared 모드를 사용할 때 dispatcher process 개수를 설정한다.  
Open 단계에서는 alter system을 사용하여 값을 줄일 수 없다.

<a id="3972a5c619054d4c"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="9e2e9ea7b0cad55f"></a>
### 기본 정보

<a id="d9f8c7d14cc02477"></a>
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

<a id="95ed4a38dcac5716"></a>
### 설명

instant hash table을 사용하는 질의에서 hash bucket을 확장하기 위한 메모리가 부족한 경우 질의를 실패한 것으로 처리할지 아니면 hash bucket을 확장하지 않고 질의를 수행할지 여부를 지정한다.

<a id="c69aeaed2a027c28"></a>
## EXTLIB_DIR

<a id="155468c741ed39f9"></a>
### 기본 정보

<a id="b6d995d7648d2bf9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | EXTLIB_DIR |
| 요약 | external library directory |
| Data type | VARCHAR |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | N/A |
| MAX | N/A |
| 기본값 | &lt;GOLDILOCKS_DATA&gt;/extlib |

<a id="72aecb05064d05c6"></a>
### 설명

외부 라이브러리 함수 호출을 위한 shared library 경로를 지정한다.

<a id="06e51f1f1dd0d3f8"></a>
## FETCH_FAILOVER

<a id="5540431fdfe8871b"></a>
### 기본 정보

<a id="87d6e7a6b0e66cf2"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | FETCH_FAILOVER |
| 요약 | enable fetch failover |
| Data type | BOOLEAN |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="6f3b9266fbfc0dc8"></a>
### 설명

Fetch failover를 활성화한다.

<a id="0aad276c305d59dd"></a>
## FULL_TABLE_SCAN_CACHING_THRESHOLD

<a id="40c4b5372e88b56f"></a>
### 기본 정보

<a id="05ade17ff21d1024"></a>
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

<a id="f4787bd59c56fea3"></a>
### 설명

디스크 테이블스페이스에 생성된 테이블을 전체 스캔할 때 버퍼 캐쉬에 캐싱할지 여부는 테이블 크기의 threshold에 따라 결정된다. FULL_TABLE_SCAN_CACHING_THRESHOLD는 바로 이 threshold 값을 설정한다. 기본값은 20이며, 이 경우 [BUFFER_CACHE_SIZE](#e0636338226aa458)의 2.0% 보다 작거나 같은 수의 페이지를 사용 중인 테이블들만 캐싱한다. 이 값이 1000 (100%)이면 전체 스캔을 수행할 때 모든 테이블을 버퍼에 캐싱한다.

예를 들어 BUFFER_CACHE_SIZE 값이 8192이고 FULL_TABLE_SCAN_CACHING_THRESHOLD 값이 509 (50.9%)인 경우, 사용 중인 페이지의 수가 4169 (8192의 50.9%)보다 작거나 같은 테이블들만 전체 스캔 시 버퍼에 캐싱된다.

<a id="98ff44ebcb1f810d"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="7f0e8fceb836b005"></a>
### 기본 정보

<a id="18ef307696bec1bd"></a>
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

<a id="4365821272c7d58d"></a>
### 설명

Global connection에서 session dependent한 정보를 포함한 질의 수행 지원 여부를 설정한다.

<a id="5d750379335628c9"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="2366ae563a168047"></a>
### 기본 정보

<a id="4f704bcf33f38ede"></a>
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

<a id="4c1cbeda19db835a"></a>
### 설명

Global journal의 buffer 크기이다.

<a id="d2bd254382f2033e"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="80f531bcb7bfa7c7"></a>
### 기본 정보

<a id="34425bb2c2ef9594"></a>
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

<a id="cc13ec1fcccc08a1"></a>
### 설명

Global journal buffer의 최대 사이즈의 합이다.

<a id="f73695ebaf90903a"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="cf2ed8ee5dc7d998"></a>
### 기본 정보

<a id="84c04ebfec0420a2"></a>
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

<a id="70267de900eaf73a"></a>
### 설명

Global property를 변경할 때 동시성을 제어하기 위해 lock 하는데 이 때 해당 lock 하기 위해 대기하는 시간을 설정한다.

<a id="743905806a1eba6f"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="cada3bf71441ac50"></a>
### 기본 정보

<a id="de887641f7807449"></a>
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

<a id="0438208cddb4d5d3"></a>
### 설명

Global transaction의 commit write mode를 변경하기 위한 프로퍼티이다. TRANSACTION_COMMIT_ WRITE_MODE는 모든 트랜잭션들에 적용되는 반면에 이 프로퍼티는 global transaction에만 적용된다. 만약 해당 프로퍼티가 2로 설정되면 TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

- 0: no wait
- 1: wait
- 2: TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

<a id="21fe968101698a45"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="691387ee16b9965f"></a>
### 기본 정보

<a id="e91f4e0529f793d0"></a>
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

<a id="8b8313d86abe1f7e"></a>
### 설명

Transaction이 두 개 이상의 cluster group에 걸쳐 데이터를 변경한 경우 이를 global transaction으로 처리할지 다수의 domain transaction으로 처리할지 결정하는 프로퍼티이다.

- 0: Global tranaction으로 처리
- 1: 다수의 domain transaction으로 처리

> 이 프로퍼티가 1인 경우에는 cluster group마다 독립적인 트랜잭션으로 commit하기 때문에 트랜잭션 원자성 (transaction atomicity)을 보장하지 않는다.

<a id="0c5e9ac0a13685cd"></a>
## GLOBAL_TRANSACTION_LOG_BLOCK_SIZE

<a id="7cbbf643c66b8fb5"></a>
### 기본 정보

<a id="cf0141f352b618de"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GLOBAL_TRANSACTION_LOG_BLOCK_SIZE |
| 요약 | block size of global transaction log file(byte) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 512 |
| MAX | 4096 |
| 기본값 | 512 |

<a id="f913cef58f21b6ad"></a>
### 설명

GLOBAL_TRANSACTION_LOG_BLOCK_SIZE는 global transaction 로그 파일의 블록 크기를 나타낸다. 그 값은 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="726ea4c3455dcc54"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="f87374861b05b6b2"></a>
### 기본 정보

<a id="0706fdc71e049290"></a>
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

<a id="2c0c46b7e4250716"></a>
### 설명

Global transaction log의 기본 directory 이다.

<a id="ba792b45bb339e9c"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="e6a037aa4a1f7d6a"></a>
### 기본 정보

<a id="e416a17add551fb7"></a>
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

<a id="7d7900871f991519"></a>
### 설명

Global transaction log의 file 크기이다.

<a id="2d52344243070fc0"></a>
## GMASTER_NUMA_NODE

<a id="03efa1f00f295c6a"></a>
### 기본 정보

<a id="a59a2370821f2942"></a>
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

<a id="1909272c8695e0f7"></a>
### 설명

gmaster 데몬이 사용할 NUMA node의 ID를 설정한다. GMASTER_NUMA_NODE 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="d4ff5dd7fc7176e9"></a>
## GMON_AUTOSTART

<a id="f0aac99f37e40149"></a>
### 기본 정보

<a id="8136a4e7b4e8b385"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | GMON_AUTOSTART |
| 요약 | Indicate whether gmon process automatically starts or not ( 0 \| 1 ) |
| Data type | BOOLEAN |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | 1 |

<a id="04d01c43de3e97b2"></a>
### 설명

gmon 프로세스를 자동으로 시작시킬지 여부를 설정한다.

<a id="c43339e41d788f8b"></a>
## HINT_ERROR

<a id="63396f964b653d36"></a>
### 기본 정보

<a id="a6b9d66579f3774e"></a>
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

<a id="66ea140549a1ceef"></a>
### 설명

Hint 구문에 대한 syntax error 및 validation error 체크 여부를 설정한다.

<a id="0646042872327a32"></a>
## HISTOGRAM_BALANCE_BUCKET_COUNT

<a id="927cea855d3e1aa8"></a>
### 기본 정보

<a id="f5edbc8102117bad"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HISTOGRAM_BALANCE_BUCKET_COUNT |
| 요약 | bucket count for height-balanced histogram when ANALYZE TABLE |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 0 |
| MAX | 1000 |
| 기본값 | 0 |

<a id="ecc4a1c2b163109b"></a>
### 설명

ANALYZE TABLE을 수행할 때 height-balanced histogram을 생성하기 위해 필요한 bucket의 개수이다.

권장값은 20 이다.

값이 5 이하일 경우 histogram 정보를 구축하지 않는다.

<a id="4e46aae7c1ded5d0"></a>
## HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT

<a id="3a471e0a966f0c46"></a>
### 기본 정보

<a id="9afc7c0f1893a52a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HISTOGRAM_BALANCE_MAX_SAMPLE_COUNT |
| 요약 | maximum sampling count for height-balanced histogram when ANALYZE TABLE |
| Data type | BIGINT |
| 적용단계 | OPEN 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 100000 |
| MAX | 1000000000 |
| 기본값 | 100000 |

<a id="2338b999948f879e"></a>
### 설명

Height-balanced histogram 정보 구축 시 sampling 할 data 의 최대 개수이다.

<a id="ef42f2f75da19f94"></a>
## HISTOGRAM_FREQUENCY_BUCKET_COUNT

<a id="4f5bb18efdb0c0dc"></a>
### 기본 정보

<a id="3cd961f62171df3b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HISTOGRAM_FREQUENCY_BUCKET_COUNT |
| 요약 | bucket count for frequency histogram when ANALYZE TABLE |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 0 |
| MAX | 1000 |
| 기본값 | 0 |

<a id="b8e6e852b7828422"></a>
### 설명

ANALYZE TABLE을 수행할 때 frequency histogram을 생성하기 위한 기준이 되는 bucket의 개수이다.

권장값은 20 이다.

값이 5 이하일 경우 histogram 정보를 구축하지 않는다.

생성해야 하는 frequency bucket의 개수가 HISTOGRAM_FREQUENCY_BUCKET_COUNT 프로퍼티 보다 클 경우, frequency histogram을 생성하지 않는다.

<a id="080fc4da28013069"></a>
## IDLE_TIMEOUT

<a id="f3c3271481de2f88"></a>
### 기본 정보

<a id="797c97315f5223c3"></a>
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

<a id="649cf7fd31479c0b"></a>
### 설명

C/S 세션에서 최대로 대기할 수 있는 IDLE 시간을 설정하며 해당 IDLE 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT이 발생하지 않는다.

<a id="ec48854ca32b38ee"></a>
## IN_DOUBT_DECISION

<a id="15ff63bdc1cc551a"></a>
### 기본 정보

<a id="c7e02aa5e2031aae"></a>
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

<a id="3072664eda15373a"></a>
### 설명

분산 트랜잭션의 in-doubt 트랜잭션을 commit 할지 rollback 할지 결정한다.

- 1: Commit
- 2: Rollback

<a id="a277cfe25833f5f6"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="83ba45857496307e"></a>
### 기본 정보

<a id="1cfc6b3d81ad27a3"></a>
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

<a id="2f3c08d3b1fe14db"></a>
### 설명

Array 기반의 in key range scan을 수행할 수 있는 in key range 대상 value들의 최대 개수이다.

- 다음과 같은 구문에 대해 array 기반 in key range scan을 수행하려면 IN_KEY_RANGE_ARRAY_COUNT가 3 이상이어야 한다.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

IN_KEY_RANGE_ARRAY_COUNT 값보다 in key range 대상 value들의 최대 개수가 더 많은 경우에는 instant table 기반으로 in key range scan을 수행한다.

<a id="4458261b7e66146c"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="80817553a8b3e2f0"></a>
### 기본 정보

<a id="56d17593831fce24"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE |
| 요약 | number of pages read in one I/O operation during an incremental backup |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 32 |

<a id="3427fcf813b30f95"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 한 번의 디스크 IO로 읽어들일 페이지의 수를 설정한다.

<a id="956149aa76d033fb"></a>
## INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA

<a id="b370e37312ff0d60"></a>
### 기본 정보

<a id="60c5681de0b28907"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INCREMENTAL_DATAFILE_HEADER_UPDATE_CRITERIA |
| 요약 | criteria for the number of flush page count to update datafile header |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1000 |
| MAX | 134217728 |
| 기본값 | 134217728 |

<a id="6f082df23079ba6c"></a>
### 설명

디스크 테이블스페이스의 데이터 파일 헤더를 갱신하는 기준을 설정한다. IO slave가 버퍼 캐쉬에서 갱신된 페이지를 디스크에 반영하는 동안 설정된 값만큼의 갱신된 페이지를 반영하였을 때 데이터 파일의 헤더에 복구를 시작할 LSN을 설정한다. 이렇게 하면 재시작 복구 시 디스크 IO를 줄일 수 있다.

<a id="9da6eb8635265063"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="eba4199f11abf3e1"></a>
### 기본 정보

<a id="e71bee16cadeabcc"></a>
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

<a id="98d6e0e795ce2686"></a>
### 설명

인덱스를 생성할 때 병렬화 개수 (parallel factor)를 지정한다.

- 0: 시스템의 코어 개수로 지정된다.

<a id="78503664cefabfde"></a>
## INDEX_MERGE_RUN_COUNT

<a id="fc8d7e1889b3de08"></a>
### 기본 정보

<a id="34b1bfc1ede06cdd"></a>
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

<a id="6b11e069efc5ad82"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (INDEX_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. INDEX_MERGE_RUN_COUNT는 한 번에 병합할 정렬된 block들의 개수를 설정한다.

<a id="5ba79a80a6fb77a6"></a>
### ALIAS

<a id="e565b425f9f990e4"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | INDEX_MERGE_RUN_COUNT |
| ALIAS | MEMORY_MERGE_RUN_COUNT |

<a id="ca307703d537c410"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="7fafa0e722db1b16"></a>
### 기본 정보

<a id="aa91346a24aa4ab1"></a>
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

<a id="1677c6b65921bdd8"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축 하는 도중에 DML이 수행되면 journal data가 저장된다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal data들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. INDEX_REBUILD_BLOCK_READ_COUNT는 이 과정에서 journal data를 얼마만큼 읽어들여 인덱스에 반영할지를 나타낸다.

<a id="29459539da2adf73"></a>
## INDEX_SELF_AGING_TRHESHOLD

<a id="6cd1ca766a27c5e1"></a>
### 기본 정보

<a id="e4f0b8e280945cd7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INDEX_SELF_AGING_THRESHOLD |
| 요약 | the threshold for processing empty nodes |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1048576 |
| 기본값 | 0 |

<a id="2a9938184c774720"></a>
### 설명

인덱스 페이지는 모든 키가 삭제되어도 인덱스에서 제거되지 않고 empty node로 관리된다. 이후 새로운 페이지가 필요할 때 empty node의 재사용 가능 여부를 판단하고, 재사용할 수 있는 경우 인덱스 세그먼트에 반납 (aging)한다.  
인덱스에 empty node가 존재하면 삭제된 키도 인덱스 스캔의 대상이 되므로 성능에 영향을 미친다.  
INDEX_SELF_AGING_THRESHOLD는 인덱스에서 키를 삭제할 때 empty node aging을 수행할 empty node의 개수를 설정한다. 즉, 키 삭제 시 INDEX_SELF_AGING_THRESHOLD 이상의 empty node가 존재하면 aging을 시도한다.

- 0: 키 삭제 시 empty node aging 을 수행하지 않는다.

> 키 삭제 시 self aging을 수행하기 위해 empty node의 aging 가능 여부를 판단한다. 그러나 aging 할 수 없는 경우에도 self aging 을 시도하면서 성능이 저하될 수 있다. 따라서 INDEX_SELF_AGING_THRESHOLD는 인덱스 스캔을 통해 대량의 레코드를 삭제하는 경우에 사용하는 것을 권장한다.

<a id="a62d8d83d47c06c9"></a>
## INDEX_SORT_RUN_SIZE

<a id="d33d7df84c314ef9"></a>
### 기본 정보

<a id="decbcff0716b5e4f"></a>
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
| MAX | 1048576 |
| 기본값 | 1048576 |

<a id="93cac7646c76ea29"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (INDEX_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. INDEX_SORT_RUN_SIZE는 정렬할 block 한 개의 크기를 설정한다.

<a id="d8e1fe0d42c7adc7"></a>
### ALIAS

<a id="e9c2f3ba22266c2f"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | INDEX_SORT_RUN_SIZE |
| ALIAS | MEMORY_SORT_RUN_SIZE |

<a id="7680e4bf52ede471"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="d763663af747f7ce"></a>
### 기본 정보

<a id="717a63df478bc4be"></a>
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

<a id="1e44e92544c5d0a2"></a>
### 설명

인덱스를 생성할 때 sub-tree를 합병하기 위한 병렬화 개수 (parallel factor)를 지정한다. 만약 해당 값이 INDEX_BUILD_PARALLEL_FACTOR 보다 큰 경우에는 INDEX_BUILD_PARALLEL_FACTOR를 사용한다.

- 0: INDEX_BUILD_PARALLEL_FACTOR를 따른다.

<a id="17342d74c06b6e7c"></a>
## INST_ALLOCATOR_COUNT

<a id="7fb482ce875f82c8"></a>
### 기본 정보

<a id="5e9fec3a1dc88761"></a>
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

<a id="e5401967bb4ab4a6"></a>
### 설명

인스턴트 블록을 할당 또는 삭제하는 연산의 병렬성을 높이기 위한 프로퍼티이다.

<a id="6fb8b231e1d09cef"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="cd7384ffa54ab9f0"></a>
### 기본 정보

<a id="9dc5436afec444d2"></a>
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

<a id="843948215d0aaa66"></a>
### 설명

Hash instant table의 예상 bucket count의 최대값을 설정한다.

<a id="b38e42dbc41377ae"></a>
## INST_TABLE_PAGE_SIZE

<a id="dfab94fed3964143"></a>
### 기본 정보

<a id="62fd5b45a6f34312"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INST_TABLE_PAGE_SIZE |
| 요약 | a page size of instant tables |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 8192 |
| MAX | 1048576 |
| 기본값 | 16384 |

<a id="81161ff33f8194f3"></a>
### 설명

인스턴트 테이블의 페이지 크기를 결정한다. 만약 인스턴트 레코드의 고정영역 크기가 인스턴트 블록의 크기를 초과하는 경우 다음과 같은 에러가 발생한다.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="d3e01ad1b7ce5002"></a>
### ALIAS

<a id="efe0910ee4d1dff4"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | INST_TABLE_PAGE_SIZE |
| ALIAS | INST_TABLE_BLOCK_SIZE |

<a id="f8c688afe0275310"></a>
## INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD

<a id="9408bd36a9721fca"></a>
### 기본 정보

<a id="94220bc6ef0b1558"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD |
| 요약 | threshold of the size to be stored as a reference column in an instant index |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 8192 |
| 기본값 | 64 |

<a id="0e91b7bf17e426ca"></a>
### 설명

인스턴트 인덱스에 column을 저장할 때 그 크기가 이 속성값보다 크거나 같은 column들은 참조 방식으로 저장한다.

인스턴트 인덱스의 키가 크기 제한 (16000 bytes)을 초과할 경우, 이 속성을 조정해 키 크기를 줄일 수 있다. Column을 참조 방식으로 저장하면 키의 크기를 줄여 인스턴트 인덱스의 크기를 줄일 수 있는 반면에 성능이 떨어진다.

```
gSQL> SELECT /*+ USE_GROUP_SORT */ * FROM T1 GROUP BY C1,C2,C3,C4,C5,C6,C7,C8;

ERR-RD000(14066): key size(16025) of the instant index exceeds the limit(16000)

gSQL> ALTER SESSION SET INSTANT_INDEX_REFERENCE_COLUMN_THRESHOLD = 64;

Session altered.

gSQL> SELECT /*+ USE_GROUP_SORT */ * FROM T1 GROUP BY C1,C2,C3,C4,C5,C6,C7,C8;

1 row selected.
```

<a id="9554881aefde43df"></a>
## INSTANT_WORK_AREA_SIZE

<a id="862cafcd90e50732"></a>
### 기본 정보

<a id="c7c2b5e134b3da14"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | INSTANT_WORK_AREA_SIZE |
| 요약 | memory area size for instant segment |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 ( 1 Terabytes ) |
| 기본값 | 65536 |

<a id="6ae70ed2f110e048"></a>
### 설명

ORDER BY와 같이 임시 적재 공간이 필요한 경우 instant table을 사용합니다. instant table에 적재할 때, 이 속성에 지정된 크기까지 메모리에 저장하다가, 더 많은 공간이 필요하면 TEMPORARY TABLESPACE로부터 공간을 할당받아 사용합니다.

> FIXED TABLE을 조회하기 위해 MOUNT 단계 이하까지 이 속성값이 무한대라고 가정한다.

<a id="01b6166a5c2d766b"></a>
## IPC_CHANNEL_COUNT

<a id="bf27d3b38a2f074d"></a>
### 기본 정보

<a id="02167dfe9ea6c20e"></a>
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

<a id="1dd9e651d813bfda"></a>
### 설명

IPC 통신을 위한 채널 개수를 지정한다.

<a id="dbefce26efecd811"></a>
## JOURNAL_TEMP_DIR

<a id="0210a32c2296f894"></a>
### 기본 정보

<a id="515cea16366fdb82"></a>
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

<a id="0140765e77fc3c92"></a>
### 설명

Journaling의 임시 디렉토리이다.

<a id="693a8aed654ece74"></a>
## KEEPALIVE_IDLE_TIME

<a id="18522d9a099077bd"></a>
### 기본 정보

<a id="319d11da9e961177"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 요약 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 16383 |
| 기본값 | 300 |

<a id="6383f27d4f026b6e"></a>
### 설명

Keep alive packet을 송신하기 전에 client와 server 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 server 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="caf2dacd79ca5bb0"></a>
## LOCAL_CLUSTER_MEMBER

<a id="10394e6d9019f0c1"></a>
### 기본 정보

<a id="45619822140e5397"></a>
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

<a id="dc108ebc05da5952"></a>
### 설명

Local cluster member의 이름이다.

<a id="5a740a29e1299c1c"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="4ca0e3a28b0462ba"></a>
### 기본 정보

<a id="d87e186c3a5da543"></a>
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

<a id="0aad8cc887e9459e"></a>
### 설명

Local cluster member의 host 이름이다.

<a id="c345eed26dbda71b"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="1ea8bee1fd7d6e20"></a>
### 기본 정보

<a id="4a86fbbbb25bc217"></a>
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

<a id="1992067cbf6ee338"></a>
### 설명

Local cluster member의 listen port 이다.

<a id="c8301c97281088a3"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="8658501d32f91f4a"></a>
### 기본 정보

<a id="8e03d2e0926693ef"></a>
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

<a id="7559c57ce9db98f6"></a>
### 설명

Local journal buffer의 크기이다.

<a id="579a841c05f539cc"></a>
## LOCATION_FILE

<a id="734b27519c4d2812"></a>
### 기본 정보

<a id="30d43091424a60fb"></a>
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

<a id="5f1a5bebe83c4303"></a>
### 설명

Location file의 이름이다.

<a id="286669eedd5ba8bb"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="17bcd74bf3013712"></a>
### 기본 정보

<a id="7b3f6670112a266e"></a>
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

<a id="5257cdec6be272e2"></a>
### 설명

Cluster system이 split-brain 상황에 대한 해결 방안을 locator에게 질의한 후에 응답을 기다리는 시간 (초)을 설정한다. CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY를 1 이상으로 설정했을 때만 사용할 수 있는 프로퍼티이다.

<a id="32e4e4fdfe48f0e7"></a>
## LOCK_HASH_TABLE_SIZE

<a id="df16bc9a2aad0b5c"></a>
### 기본 정보

<a id="1f2ec27458306197"></a>
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

<a id="c042c792043a26a1"></a>
### 설명

잠금 관리자 (lock manager)가 관리하는 hash table의 최대 크기를 설정한다.

<a id="6ea8fae775896cf8"></a>
## LOCKABLE_DISPATCHER_CM_BUFFER_COUNT

<a id="68892a7cf53d26ac"></a>
### 기본 정보

<a id="15eb64f41197adb4"></a>
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

<a id="2343f261f68a458f"></a>
### 설명

Cluster lockable dispatcher의 communication buffer 개수를 지정한다.

<a id="4ddbc6e597502b57"></a>
## LOCKLESS_DISPATCHER_CM_BUFFER_COUNT

<a id="053f1764220ca8b3"></a>
### 기본 정보

<a id="fc13563e6efea9af"></a>
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

<a id="4dca83dee18bbb76"></a>
### 설명

Cluster lockless dispatcher의 communication buffer 개수를 지정한다.

<a id="abf27fc10f61b70e"></a>
## LOG_BLOCK_SIZE

<a id="cf6f123187a56ae9"></a>
### 기본 정보

<a id="93b9572bf9d3069e"></a>
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

<a id="a878702efd48784e"></a>
### 설명

LOG_BLOCK_SIZE는 log buffer가 disk의 log file로 flush 되는 최소 크기이고 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="014af4031e5b2242"></a>
## LOG_BUFFER_SIZE

<a id="fc6f8628f9f0c728"></a>
### 기본 정보

<a id="28069062a96d641e"></a>
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

<a id="b0beda08ee481167"></a>
### 설명

Database에서 DML 및 DDL 연산을 수행하여 생성한 redo log들은 공유 메모리 공간인 log buffer에 저장되고, LOG_BUFFER_SIZE를 참조하여 log buffer의 메모리 크기를 설정한다.

<a id="4ef7aa88796173a5"></a>
## LOG_DIR

<a id="9eeea35d30793cd6"></a>
### 기본 정보

<a id="a22bd37f0a360969"></a>
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

<a id="1a17beea18b5aa06"></a>
### 설명

Log buffer에 기록된 log는 database의 영속성을 보장하기 위해 비휘발성 저장 장치에 존재하는 log file로 flush 되고, LOG_DIR은 log file의 경로를 설정한다.

<a id="20eb92d51fc1b07f"></a>
## LOG_FILE_SIZE

<a id="0ac08fffda4ff34a"></a>
### 기본 정보

<a id="5dc8b574ffe1266a"></a>
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

<a id="53612eb9aa7a29c6"></a>
### 설명

Database에서 사용되는 log file의 크기를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 log file size를 변경할 수 없다.

<a id="ac2066d1577ab221"></a>
## LOG_FLUSHER_HOT_POLICY_INTERVAL

<a id="223a5207edc9840d"></a>
### 기본 정보

<a id="14d859a9964f81c4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOG_FLUSHER_HOT_POLICY_INTERVAL |
| 요약 | log flushing interval for busy waiting(us) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 86400000000(1 day) |
| 기본값 | 0 |

<a id="30270dcd6bd5dca3"></a>
### 설명

gmaster 의 log flusher thread 가 event 를 기다릴 때 busy waiting 을 수행하는 시간이다.   
단위는 micro second 이며, 이 값을 크게 설정할수록 CPU 사용량은 증가하지만 로그 버퍼의 데이터를 디스크로 더 빠르게 기록할 수 있다.   
기본값은 0 이며, 이 경우 busy waiting을 수행하지 않는다.

<a id="3ea14d7527cd6f31"></a>
## LOG_GROUP_COUNT

<a id="493c97022ffe690e"></a>
### 기본 정보

<a id="d0475373322c0e58"></a>
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

<a id="2415e4e9d94f0988"></a>
### 설명

Database에서 사용되는 log group의 개수를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 영향을 미치지 않는다. Database를 생성한 후에 log group을 추가하거나 제거하는 기능은 별도의 구문으로 지원한다.

<a id="e38bb90f7911f458"></a>
## LOG_MIRROR_MODE

<a id="539fc1efcd353c32"></a>
### 기본 정보

<a id="1efc301e015813fc"></a>
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

<a id="2d57165785f59081"></a>
### 설명

데이터베이스를 시작할 때 redo log 복제 tool인 LogMirror를 운영할 때 필요한 shared memory를 구성하기 위한 프로퍼티이다.   
LogMirror를 수행하려면 반드시 enable 되어야 한다.  
Shared memory의 크기는 LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE 프로퍼티로 변경할 수 있다.

<a id="0b5cc85388b1bf30"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="7c87c027d8a7f6d2"></a>
### 기본 정보

<a id="95ffa32b852d1354"></a>
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

<a id="3c018a7ba51422c3"></a>
### 설명

Redo log 복제 tool인 LogMirror에 사용될 shared memory의 크기를 설정하는 프로퍼티이다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="c102b0c944ddf6b6"></a>
## LOG_MIRROR_TIMEOUT

<a id="413dab99c5eb1279"></a>
### 기본 정보

<a id="5eaf33faeb75ff23"></a>
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

<a id="dd55a918dda8a4a8"></a>
### 설명

LogMirror의 응답을 기다리는 시간이다.   
만약 0일 경우 무한정 대기하며 그렇지 않을 경우 설정한 값만큼 대기하다가 TIMEOUT이 발생하고 LogMirror service를 중단한다. 이 후 서버는 정상적으로 운영된다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="810eace2ed68cbcf"></a>
## LOG_SYNC_INTERVAL

<a id="44b5916bf89eb130"></a>
### 기본 정보

<a id="71a24368694c336f"></a>
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

<a id="5bdaa834693ca02d"></a>
### 설명

GOLDILOCKS의 log flusher는 log buffer의 내용을 disk log file로 flush하는 system thread이다. Log flusher가 유휴상태에서 깨어나면 flush 해야 할 log가 있는지 확인하여 있을 경우 flush를 수행한다. 이 때 LOG_SYNC_INTERVAL에 설정된 시간 내에 flush를 하지 않았다면 현재 log buffer의 마지막 block까지 flush를 수행하여 log buffer와 log file을 동기화한다.

<a id="491d73b5a9e381ea"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="2f8ecfd42c0fe78a"></a>
### 기본 정보

<a id="e1c097a9096567a6"></a>
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

<a id="71c31806f5901289"></a>
### 설명

Log를 동기화하는 millisecond 단위의 주기이다.

<a id="1e5168db98af38c1"></a>
## MAX_GROUP_COUNT

<a id="31c77ea8a8049a1d"></a>
### 기본 정보

<a id="e333ae910f0a12b9"></a>
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

<a id="a92ac1e5097302f6"></a>
### 설명

클러스터 시스템 내 최대 그룹 개수이다.

<a id="ba64c6c4ca033940"></a>
## MAX_GROUPING_SETS_COUNT

<a id="6128efb43548c88b"></a>
### 기본 정보

<a id="b0169f79197f2722"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_GROUPING_SETS_COUNT |
| 요약 | maximum grouping sets count |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 1 |
| MAX | 131072 |
| 기본값 | 4096 |

<a id="a193ad39d1719456"></a>
### 설명

Group by 구문에서 구성할 수 있는 grouping set의 최대 개수이다.

<a id="8966189602bcf57d"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="d49498e48f853c39"></a>
### 기본 정보

<a id="6deb6a68b43ce2c4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_JOURNAL_FILE_SIZE |
| 요약 | maximum journal file size |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 1099511627776 ( 1 Terabytes) |
| 기본값 | 0 (no limit) |

<a id="37e8dba4ad9cdd03"></a>
### 설명

Cluster system에서 journaling이 발생할 경우 내부적으로 journaling data를 저장할 global journaling file 의 최대 크기 (quota)를 설정한다.

<a id="c6614c37bb6c75db"></a>
## MAX_NODE_COUNT

<a id="bfe562ae4ab984ac"></a>
### 기본 정보

<a id="0a1f7a9e21b5b23b"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAX_NODE_COUNT |
| 요약 | maximum node count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 8192 |
| 기본값 | 64 |

<a id="957e5b8439a7bd76"></a>
### 설명

클러스터 시스템에 조인 가능한 노드 (instance)의 최대 개수이다.

<a id="da246abf0edba0d4"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="2eb4732217280b3e"></a>
### 기본 정보

<a id="58306b14b0594563"></a>
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

<a id="05bea7313db09ff4"></a>
### 설명

동시에 수행될 수 있는 statement 개수를 설정한다.

<a id="ad5bec6bee37ae11"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="68476e86a6374f4b"></a>
### 기본 정보

<a id="b19ebbe2acf03c78"></a>
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

<a id="a841406e9e3ceb52"></a>
### 설명

세션에서 사용 중인 파일 캐쉬의 최대 개수를 설정한다.

<a id="0e681799cc028993"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="2b07c6c6f4253b60"></a>
### 기본 정보

<a id="82cffd1d5fd9550c"></a>
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

<a id="8a525c5648ec1d95"></a>
### 설명

디스크 쓰기 연산 한 번으로 기록할 수 있는 최대 페이지 수를 설정한다. 디스크 테이블스페이스의 페이지가 버퍼에서 변경이 된 경우 IO thread가 이를 디스크에 기록한다. 디스크 쓰기 연산을 한 번 수행할 때 인접한 페이지들을 함께 기록하면 디스크 기록 횟수를 줄여 시스템 자원의 효율성을 높일 수 있다.

<a id="949df3467d9afa43"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="d6b0fdf40aa59cd7"></a>
### 기본 정보

<a id="bb96658d1ff204f1"></a>
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

<a id="8e096846fd05af40"></a>
### 설명

Log buffer의 내용을 disk의 log file에 flush 할 때 한 번의 write 연산으로 flush 할 log block의 최대 개수를 설정한다.

<a id="13765a88902e4073"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="56a83a172d6d69c7"></a>
### 기본 정보

<a id="a7816e4555a0289a"></a>
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

<a id="a25266c0d792edec"></a>
### 설명

GOLDILOCKS의 datafile은 checkpoint와 특정 DDL문에 의해 disk에 flush 된다. Datafile을 flush 하기 위해 한 번의 write 연산으로 flush 할 data page의 최대 개수를 설정한다.

<a id="33eb9921e0ea0b45"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="08282bafa7baf8c4"></a>
### 기본 정보

<a id="51e61d8c37eb858e"></a>
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

<a id="e3a48945a7b9725b"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하면 DML 수행과 병행하여 처리할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal log들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. Journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="4db11cd667b64bcd"></a>
## MAXIMUM_LOADED_LIBRARY_COUNT

<a id="48f8ff43a7993006"></a>
### 기본 정보

<a id="e3a2f93a84212e61"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MAXIMUM_LOADED_LIBRARY_COUNT |
| 요약 | maximum number of loaded library |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 128 |
| 기본값 | 16 |

<a id="10d450086e439761"></a>
### 설명

데이터베이스에서 외부 루틴 (external routine)을 실행할 때 동시에 로드할 수 있는 공유 라이브러리의 최대 개수를 제한한다. 이 프로퍼티는 데이터베이스 프로세스가 유지할 수 있는 동적 라이브러리 핸들의 총 개수에 상한선을 두어, 잘못된 외부 코드나 설정 오류로 인한 과도한 메모리 점유, 핸들 고갈, 성능 저하를 예방한다.

<a id="d061da65868d4d66"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="56920090956fd66a"></a>
### 기본 정보

<a id="2d56937a7694aae5"></a>
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

<a id="bd5fe0bf25c2326c"></a>
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

<a id="4c3833e8daa7e689"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="42598dfce24c342f"></a>
### 기본 정보

<a id="48bd3ee0137e0a32"></a>
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

<a id="2331c3786fac684a"></a>
### 설명

하나의 session 내에서 사용할 수 있는 package instance의 최대 개수이다.  
Package instance는 해당 session에서 stateful package를 사용할 때 생성된다.

<a id="8be3d60e6d14f7af"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="9d339427e6bf14f6"></a>
### 기본 정보

<a id="c129aecf0806e32f"></a>
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

<a id="48b5bc7129e797c6"></a>
### 설명

Shared mode로 접속한 하나의 session에서 사용 가능한 최대 buffer size를 설정한다.  
자세한 내용은 [DISPATCHER_CM_BUFFER_SIZE](#8ea1fbc41a34f73f)를 참조한다.

<a id="154b91a58d09ace1"></a>
## MEASURE_CLUSTER_LATENCY

<a id="c27192294f8c137e"></a>
### 기본 정보

<a id="90cf035e37dda8d8"></a>
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

<a id="87c36f4583a2fffe"></a>
### 설명

Measure cluster의 latency 이다.

<a id="254c80b8b5f8dc20"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="d18fa4c5745c3d08"></a>
### 기본 정보

<a id="3e2f5e9af001ea46"></a>
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

<a id="ac12d071beeeb9c9"></a>
### 설명

샘플링을 이용해서 [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#2c58b21ce5cb8f13)을 수행할 때의 최소 샘플링 row 건수이다.

<a id="20cbb23dd0fc942f"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="9bfb02e2a83325c4"></a>
### 기본 정보

<a id="b657eea36dc7b948"></a>
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

<a id="773e12568fb86015"></a>
### 설명

DML은 이전 image를 저장하기 위해 undo page를 사용한다. DML당 undo segment를 하나씩 사용하여 undo page를 소모하는데, 만약 할당받은 undo segment의 page를 모두 소진하였을 경우 다른 undo segment의 page를 가져와서 사용할 수 있다. MINIMUM_UNDO_PAGE_COUNT는 undo page가 부족할 때 page를 가져올 undo segment를 찾기 위한 최소 undo page 수이다. 즉, undo page가 부족할 때, MINIMUM_UNDO_PAGE_COUNT 보다 많은 page를 보유한 undo segment에서만 page를 가져올 수 있다.

<a id="c000e9380b059158"></a>
## NET_BUFFER_SIZE

<a id="17fe456f2643b6e8"></a>
### 기본 정보

<a id="3d49702522f8ab8c"></a>
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

<a id="d1021eb7049565b3"></a>
### 설명

TCP 통신 buffer size를 설정한다.  
Dedicated 모드에서는 통신 packet의 최대 크기로 설정된다.  
Shared 모드에서는 [DISPATCHER_CM_UNIT_SIZE](#5ec011cf53180e75)가 사용된다.

<a id="09118aefc816172d"></a>
## NLS_DATE_FORMAT

<a id="b6dcbbf7771f8e32"></a>
### 기본 정보

<a id="19c4028bec55f1bc"></a>
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

<a id="471bd73199d3470a"></a>
### 설명

NLS_DATE_FORMAT은 TO_CHAR와 TO_DATE 함수의 default date format을 지정한다.

<a id="d78680ceba6107a9"></a>
## NLS_TIME_FORMAT

<a id="e6a5ce7207ff6507"></a>
### 기본 정보

<a id="be34d4dbb0895830"></a>
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

<a id="048511c161428f5f"></a>
### 설명

NLS_TIME_FORMAT은 TO_CHAR와 TO_TIME 함수의 default time format을 지정한다.

<a id="d8ed241efdbfc8ee"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="38ddbff615dffc8f"></a>
### 기본 정보

<a id="89adc2682fa54130"></a>
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

<a id="444dfc7bc0af620a"></a>
### 설명

NLS_TIME_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIME_WITH_TIME_ZONE 함수의 default time with time zone format을 지정한다.

<a id="b83b0daa42003bc4"></a>
## NLS_TIMESTAMP_FORMAT

<a id="11a55fc7b66ad689"></a>
### 기본 정보

<a id="0b2ccee3ac7bf89f"></a>
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

<a id="7859f5bd0f74d091"></a>
### 설명

NLS_TIMESTAMP_FORMAT은 TO_CHAR와 TO_TIMESTAMP 함수의 default timestamp format을 지정한다.

<a id="8cf319a54a7fec34"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="0fb45de62082dc56"></a>
### 기본 정보

<a id="df5e24f8c2b29a0e"></a>
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

<a id="163e7c52bcd72d72"></a>
### 설명

NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIMESTAMP_WITH_TIME_ZONE 함수의 default timestamp with time zone format을 지정한다.

<a id="9ab02e3de5d2839a"></a>
## NUMA

<a id="23c7d2234a7a0bbf"></a>
### 기본 정보

<a id="688c0cf2722438b1"></a>
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

<a id="6e8e4736820f920a"></a>
### 설명

NUMA를 활성화/ 비활성화한다.

> AIX에서 NUMA 속성을 사용하기 위해서는 사용자 계정을 변경해야 한다. 다음 명령을 루트 사용자로 실행한다.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> 여기에서 &lt;username&gt;은 루트가 아닌 AIX 사용자 계정이다.  
> 변경 사항을 적용하려면 로그아웃한 후에 다시 로그인해야 한다.

<a id="b5576465670eb688"></a>
## NUMA_MAP

<a id="8cca806a6369a874"></a>
### 기본 정보

<a id="409d3e540dfbb050"></a>
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

<a id="43d885ef6676a3f8"></a>
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

<a id="58508b3c587155a0"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="f595ca75e0918f6b"></a>
### 기본 정보

<a id="61bd9417d73b036e"></a>
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

<a id="9cfbd8610c00ece6"></a>
### 설명

시스템의 백그라운드 프로세스 (gmaster)는 노드 장애에 따른 failover를 완료한 후에 장애 멤버를 자동으로 오프라인 시킨다.

만약 NO로 설정되어서 장애 멤버가 오프라인되지 않았다면 장애 멤버를 시스템에 다시 조인시키기 전에 다음 구문을 실행해야 한다.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="3ecfa3edb0e08bb5"></a>
## ONLINE_DDL_BLOCK_READ_COUNT

<a id="5a2a1565a8e6af81"></a>
### 기본 정보

<a id="9923ac5db8c7353c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_DDL_BLOCK_READ_COUNT |
| 요약 | block read count for online DDL |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1 |
| MAX | 65536 |
| 기본값 | 100 |

<a id="48d57942377fc822"></a>
### 설명

Online DDL 수행 시 block 의 크기를 결정한다.  
하나의 block 에는 프로퍼티 개수 만큼의 레코드가 저장되며, block 단위로 원격에 전송된다.

<a id="39cb80c592e7815c"></a>
## ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD

<a id="14d02a392c986de6"></a>
### 기본 정보

<a id="638896e6ed876c90"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_DDL_JOURNAL_REPLAY_THRESHOLD |
| 요약 | threshold bytes for replaying journals without table lock |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 10737418240 (10G) |
| 기본값 | 1048576 (1M) |

<a id="197bdbf361fcb325"></a>
### 설명

클러스터 환경에서 online DDL 은 수행 중 발생한 DML이 남긴 journal log를 여러 번에 걸쳐 반영한다. Journal log를 반영하는 최대 횟수는 ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT로 결정되지만, 남은 journal log의 양이 많지 않을 경우에는 최대 횟수만큼 반복하지 않고, 즉시 테이블에 EXCLUSIVE lock을 걸어 마지막 journal log를 반영하기 위한 threshold 값으로 사용한다.

<a id="fa65edf9db034833"></a>
## ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="35ba4b532c272cc4"></a>
### 기본 정보

<a id="6c7a42cd6af64d67"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_DDL_MAXIMUM_JOURNAL_REPLAY_COUNT |
| 요약 | maximum number of replaying journals for online DDL |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 2 |
| MAX | 1024 |
| 기본값 | 2 |

<a id="a9757cd2eb2893af"></a>
### 설명

클러스터 환경에서 online DDL은 DML과 병행하여 수행할 수 있으며, 이 때 DML은 변경된 내용을 journal log로 남긴다.   
Online DDL은 테이블을 동기화하는 동안 발생한 journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는 방식으로 처리한다.  
이와 같은 과정을 통해 최대 몇 차까지 journal log를 반영할 것인지 설정한다.

<a id="20196df5e431393d"></a>
## ONLINE_DDL_SCAN_PARTITION

<a id="965846396e92b3c7"></a>
### 기본 정보

<a id="ed5e8abc7a9946f0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ONLINE_DDL_SCAN_PARTITION |
| 요약 | partition factor of shard upon online DDL |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 1000 |
| 기본값 | 5 |

<a id="b0d2ae27668f3e47"></a>
### 설명

Online DDL 시 shard를 몇 개로 분할하여 동기화할지 설정한다.  
자세한 내용은 [ALTER TABLE name REBALANCE](../part-03-sql-manual/18-sql-references-a-b.md#4dcbc8cc43487ef2)를 참조한다.

<a id="c3efe0b6528eaa8b"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="c8b92952e604dcf7"></a>
### 기본 정보

<a id="2add1771ede34829"></a>
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

<a id="485e8614d6157510"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하는 동안 수행된 DML은 journal log를 남긴다. 인덱스 재구축이 마무리되는 단계에서 여러 차례에 걸쳐 journal이 인덱스에 반영되는데 이 때 journal log를 반영하는 최대 차수는 [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#33eb9921e0ea0b45)가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="97fa3605c52461e3"></a>
## OS_GROUP_ACCESS

<a id="60ae515a5e4ccf87"></a>
### 기본 정보

<a id="44007a5c4126bb00"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | OS_GROUP_ACCESS |
| 요약 | enable access database with OS group permission |
| Data type | BOOLEAN |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1 |
| 기본값 | NO |

<a id="b2adf335e0d374d9"></a>
### 설명

동일한 group의 다른 user가 D/A로 접속하려면 이 설정을 YES로 변경해야 한다. 또한 시스템 상의 umask도 0002로 변경해야 한다.

<a id="d9e92a36abc98645"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="728aa1f192cf9af5"></a>
### 기본 정보

<a id="8360327631fd3421"></a>
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

<a id="78aec788f0d03488"></a>
### 설명

클라이언트로 보낼 통신 데이터의 크기가 PACKET_COMPRESSION_THRESHOLD 보다 클 경우, 통신 데이터를 압축한다.

<a id="c863dc4362b040f4"></a>
## PAGE_CHECKSUM_TYPE

<a id="e7408a40a1a3521d"></a>
### 기본 정보

<a id="31905e0f0b9722fe"></a>
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

<a id="b13422504409a015"></a>
### 설명

Datafile의 각 page들에 대한 물리적 정합성을 보장하기 위해 checksum을 사용한다. GOLDILOCKS는 LSN, CRC 방식의 page checksum을 지원한다.

- 0: LSN
- 1: CRC

<a id="8e9574c0ee72da5d"></a>
## PARALLEL_IO_FACTOR

<a id="d46305c993db7dfe"></a>
### 기본 정보

<a id="ef1f80d32730403e"></a>
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

<a id="c76ae51375654f15"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일을 병렬 로딩하고 체크포인트 할 때 데이터 파일을 병렬 기록하기 위한 thread 개수를 설정한다.

<a id="354ec149a98fdf5c"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

> 22c.1 이후로 지원하지 않는다.

<a id="e1a17600a915b42c"></a>
### 기본 정보

<a id="0906c6bb6158ba1e"></a>
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

<a id="c141bc02b4d25b89"></a>
### 설명

Datafile의 병렬 IO를 위한 group directory를 설정한다. 즉, PARALLEL_IO_FACTOR 수만큼 group을 설정하여 각 group에 속한 datafile 별로 병렬 IO를 수행한다.

<a id="1b4b20346037b538"></a>
## PARALLEL_LOAD_FACTOR

<a id="1e5748a7092646b1"></a>
### 기본 정보

<a id="f95c02c24362ec54"></a>
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

<a id="4d1da9176b2933fa"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일의 메모리를 적재한 후에 병렬 작업을 위한 thread 개수를 설정한다.

<a id="f64c4bc97fc72011"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="d1e64639bab93920"></a>
### 기본 정보

<a id="dc4a98e170341729"></a>
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

<a id="795fa69d6e1683e4"></a>
### 설명

여러 트랜잭션이 동시에 실행될 경우 log buffer에 대한 경쟁을 줄이기 위해 pending log buffer를 사용하며, PENDING_LOG_BUFFER_COUNT는 동시에 사용할 수 있는 pending log buffer 개수를 설정한다.

<a id="e3eb93833964a2d1"></a>
## PLAN_CACHE

<a id="0e97f31a9418cdb4"></a>
### 기본 정보

<a id="5ed6a26e9aba8d99"></a>
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

<a id="309715d0672b575b"></a>
### 설명

Plan cache 사용 여부를 설정한다.

<a id="20b7c3ce69752590"></a>
## PLAN_CACHE_SIZE

<a id="7af8de28cee313e2"></a>
### 기본 정보

<a id="38e61e0ecff34230"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_CACHE_SIZE |
| 요약 | sql plan cache size(byte) |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | TRUE |
| MIN | 20971520 |
| MAX | 1099511627776 |
| 기본값 | 104857600 |

<a id="f9b22ada2a3e6aec"></a>
### 설명

Plan cache에 사용할 메모리 크기를 설정한다.

<a id="263059fd84a1af98"></a>
## PLAN_HISTORY

<a id="4803edb81c1bfa92"></a>
### 기본 정보

<a id="ee1efbf3c7199212"></a>
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

<a id="9d7d4484eff7e60d"></a>
### 설명

Plan history 사용 여부를 설정한다.

<a id="e8a49d80e6e88910"></a>
## PLAN_HISTORY_SIZE

<a id="46fa9e1113673ebc"></a>
### 기본 정보

<a id="fd8eb46c1a1ad29e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PLAN_HISTORY_SIZE |
| 요약 | plan history size |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 |
| MAX | 100000 |
| 기본값 | 0 |

<a id="0458ddf1c9e90291"></a>
### 설명

Plan history에 저장할 plan 개수를 설정한다.

<a id="1134f13e4b562942"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="d428a1730079c9a6"></a>
### 기본 정보

<a id="92489ce5242bd140"></a>
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

<a id="b1b0279127e49e2c"></a>
### 설명

세션이 사용할 heap 메모리의 최초 크기를 설정한다. 세션에서 사용되지 않는 메모리가 생기더라도 이 메모리들이 운영체제로 반환되지는 않는다.

<a id="7115ad7917ad14bc"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="f6cfd73ee2623c52"></a>
### 기본 정보

<a id="f0bb4c23d73c2a0d"></a>
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

<a id="05958fd88ae1a4e4"></a>
### 설명

세션에서 heap 메모리를 추가적으로 할당할 때, 확장될 메모리 크기를 설정한다.

<a id="6b116ce2df4b2561"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="369cccffbf36eca9"></a>
### 기본 정보

<a id="d760f8181ba787fd"></a>
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

<a id="b11b7c67a00cf6b2"></a>
### 설명

세션에서 사용하지 않는 heap 메모리가 생기더라도 이 크기만큼의 메모리를 유지하며 시스템에 반환하지 않고 세션 내에서 재사용한다.

PRIVATE_STATIC_AREA_INIT_SIZE보다 작게 설정하더라도 그 크기보다 작아지지 않는다.

<a id="ac29014e15c42d84"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="53a7ed2a81b3be2b"></a>
### 기본 정보

<a id="2b3928cea45fd9f4"></a>
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

<a id="a38c775e4c6815a4"></a>
### 설명

세션에서 할당할 수 있는 최대 heap 메모리 크기를 지정한다.

<a id="cdb7effa6ea2c6b6"></a>
## PROCESS_MAX_COUNT

<a id="557dbc28d6251fdd"></a>
### 기본 정보

<a id="24862d54e33eb033"></a>
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

<a id="29b3425a7c03208a"></a>
### 설명

시스템에서 사용할 수 있는 최대 프로세스 (thread) 개수를 지정한다.

시스템 프로세스 생성  
• D/A 또는 C/S dedicated 모드로 접속할 때마다 프로세스가 생성된다.  
• C/S shared 모드는 기본적인 balancer, dispatcher, shared-server가 프로세스이고 client에서 접속할   
&nbsp;&nbsp;때는 프로세스가 생성되지 않는다.

<a id="995edac2089cebe5"></a>
## QUERY_TIMEOUT

<a id="a09f91f7ace7e90d"></a>
### 기본 정보

<a id="7b51ea76c1fb43d1"></a>
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

<a id="83d166cc331145c0"></a>
### 설명

세션에서 받은 명령어를 처리할 수 있는 최대 시간을 지정하며 만약 해당 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT 에러가 발생하지 않는다.

<a id="2a75be98cd562dd9"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="69034197e6f14e84"></a>
### 기본 정보

<a id="fc37fc2f0456a956"></a>
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

<a id="4678cb7e36919f8b"></a>
### 설명

미디어 복구 시 archive redo log가 존재하는 디렉토리의 개수를 설정한다.

<a id="3c2142c8e7876aa3"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="7d78b850cc4c92c4"></a>
### 기본 정보

<a id="a05180bfc68c8441"></a>
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

<a id="3c46ed08a62ac515"></a>
### 설명

증분 백업을 이용하여 파일을 복원할 때 증분 백업이 존재하는 디렉토리의 개수를 설정한다.

<a id="5100b2e582456549"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> 3.1 이후로 지원하지 않는다.

<a id="f81fcc18a847e212"></a>
### 기본 정보

<a id="9bbacb2ed88b6453"></a>
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

<a id="75596ba2ce693aef"></a>
### 설명

Page count 변경에 의해 plan이 recompile 되었는지 여부를 체크하기 위해 minimum page count를 설정한다.

<a id="4db1cb40adf13994"></a>
## RECOMPILE_PAGE_PERCENT

> 3.1 이후로 지원하지 않는다.

<a id="9f2f7b43e11e5e67"></a>
### 기본 정보

<a id="eda7d22e5365717a"></a>
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

<a id="ba57b626cffd55f3"></a>
### 설명

Page count가 변경되어 plan을 recompile 할 때의 page percentage를 설정한다. 이 값이 0인 경우 page count 변경에 따른 recompile을 하지 않는다.

<a id="7e7a0a7ce180d296"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="6857a71c0d342643"></a>
### 기본 정보

<a id="449cad605009aadf"></a>
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

<a id="6872fcc6304bdd8f"></a>
### 설명

복구를 위한 기본 log buffer 크기이다.

<a id="0f33ffc599e55ae7"></a>
## RECOVERY_SLAVES

<a id="f7479ec4f5d70e41"></a>
### 기본 정보

<a id="97dc3a9c4cb2d66d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RECOVERY_SLAVES |
| 요약 | the number of slave threads to participate in instance or crash recovery |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 64 |
| 기본값 | 8 |

<a id="7d75e7e18c4997a8"></a>
### 설명

병렬 복구를 위한 slave thread의 개수를 설정한다. 해당 프로퍼티 값을 0으로 설정하면 slave thread 없이 master thread 만으로 복구를 수행한다.

<a id="e82f0eedda428e99"></a>
## RECYCLEBIN

<a id="b145c668659f0929"></a>
### 기본 정보

<a id="7d07a7de342e0c4a"></a>
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

<a id="3a6db55d55902aab"></a>
### 설명

휴지통 기능을 활성화할지 여부를 설정한다.

<a id="0800df3cd814daac"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="6af4f376501c12c0"></a>
### 기본 정보

<a id="909fe74870432f78"></a>
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

<a id="6714f803543a9aa2"></a>
### 설명

생성된 REDO LOG의 크기가 REDO_LOG_COMPRESSION_THRESHOLD 값보다 클 경우, REDO LOG를 압축한다.

<a id="c462a3db9feff284"></a>
## REDO_LOGGING_THROTTLING

<a id="f7133f9ff83a44d2"></a>
### 기본 정보

<a id="64efe4db924caf6c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REDO_LOGGING_THROTTLING |
| 요약 | The limit on the number of dirty blocks in the log buffer for large-scale redo logging |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 10737418240 |
| 기본값 | 10737418240 |

<a id="726ccf8a5128f566"></a>
### 설명

이 프로퍼티는 대량의 로그로 인한 시스템 과부하를 방지하고, 온라인 서비스에 미치는 영향을 최소화하기 위해 사용된다.

로깅할 때 로그 버퍼에 설정된 프로퍼티 값보다 많은 dirty block이 존재하면, dirty block이 디스크로 flush될 때까지 대기한다.

<a id="d559fe6106901820"></a>
### ALIAS

<a id="fd78b95db45edc34"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | REDO_LOGGING_THROTTLING |
| ALIAS | INDEX_LOGGING_THROTTLING |

<a id="cf00a7acd30a9f37"></a>
## REFINE_RELATION

<a id="7785a90138f904c8"></a>
### 기본 정보

<a id="fcdc26cd4a8e6b7d"></a>
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

<a id="2d4eece9f637481e"></a>
### 설명

이 속성을 NO로 하면 서버를 재시작할 때 REFINE RELATION 과정을 수행하지 않는다.

해당 프로퍼티는 REFINE RELATION 도중에 문제가 발생한 경우에 사용할 수 있으며 삭제되었지만 REFINE 하지 못한 RELATION (테이블이나 인덱스)들의 공간은 재사용할 수 없다. 문제를 해결한 이후 해당 프로퍼티를 YES로 설정하고 재시작하면 삭제하지 못했던 RELATION들에 대해 REFINE을 시도한다.

<a id="e870ce9df66fc2f2"></a>
## RESTORE_BUFFER_SIZE

<a id="ed877e1ee2b9aa94"></a>
### 기본 정보

<a id="f00b1a661fcca99e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RESTORE_BUFFER_SIZE |
| 요약 | buffer size for datafile retsore |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 1048576 |
| MAX | 1073741824 |
| 기본값 | 1048576 |

<a id="2cfc7d532423de15"></a>
### 설명

백업을 이용하여 디스크 테이블페이스를 [ALTER DATABASE RESTORE](../part-03-sql-manual/18-sql-references-a-b.md#60ea018060bd0c35) 할 때 디스크에서 한 번에 읽어 처리하는 버퍼 크기를 설정한다. 백업을 이용하여 디스크 테이블스페이스에 대해 [ALTER DATABASE RECOVER](../part-03-sql-manual/18-sql-references-a-b.md#233fbcf85decd22e)를 수행하는 경우에도 restore 과정에서 동일하게 적용된다.

<a id="1f174eb8af0095ae"></a>
## SESSION_FATAL_BEHAVIOR

<a id="84444ea289c65631"></a>
### 기본 정보

<a id="1cdf19329a1ad13c"></a>
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

<a id="cf2a80da2a7a2a79"></a>
### 설명

Session fatal이 발생할 때 fatal을 유발한 thread만 종료시킬지 아니면 프로세스 자체를 종료시킬지 결정한다.

- 0: Fatal을 유발한 thread만 종료한다.
- 1: 프로세스를 종료한다. 해당 프로세스 내에 다수의 세션이 동시에 수행되고 있다면 모든 세션들이 데이터베이스 사용을 끝낸 후에 프로세스를 종료한다.

<a id="9d01096d9cfaec26"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="522303dbeed6f946"></a>
### 기본 정보

<a id="2008c70015c84bde"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_MEMORY_INIT_SIZE |
| 요약 | initial memory size for dedicated sessions |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 524288 (512K) |

<a id="44d8e8b4e16cb656"></a>
### 설명

Dedicated session에서 사용할 메모리의 초기 크기를 설정한다.

<a id="876cfdccbee0f0b7"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="b8449ea4bda5015f"></a>
### 기본 정보

<a id="c6c14f28f851d620"></a>
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

<a id="edcc697581df9bfb"></a>
### 설명

세션에서 사용한 동적 공유 메모리를 해제할 때 세션에서 사용하지 않는 동적 공유 메모리를 시스템에 반납할지 여부를 판단하기 위한 경계값을 설정한다. 즉, 사용하지 않는 메모리 중 설정된 값보다 큰 크기의 메모리 청크가 있으면 시스템에 반납한다.

<a id="da54e5b328c8e8a9"></a>
## SESSION_POOL_INIT_SIZE

<a id="dbf4b96cd5b2fe02"></a>
### 기본 정보

<a id="759ad2489ecc20c2"></a>
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

<a id="179bafd0a0d913b3"></a>
### 설명

Session pool의 초기 메모리 크기를 설정한다.

각 세션들에 메모리가 필요한 경우 session pool에서 공간을 할당 받는데 session pool의 공간이 부족할 경우에는 SSA로부터 공간을 할당 받는다.  
Session pool은 세션에서 SSA로 빈번하게 접근하는 것을 방지하기 위해서 사용되는데 만약 "0"으로 설정할 경우 session pool 기능은 비활성화 된다.

<a id="432e9184bb5cc010"></a>
## SESSION_POOL_NEXT_SIZE

<a id="1066fc79769d9b91"></a>
### 기본 정보

<a id="613ddd47b8ffff2d"></a>
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

<a id="9d0dc0ed437928ae"></a>
### 설명

Session pool의 공간을 확장할 때 session pool 내부의 메모리 크기를 얼마나 확장할지 설정한다.  
SESSION_POOL_INIT_SIZE가 0보다 큰 경우에만 유효하다.

<a id="27e961b795d2dfb5"></a>
## SHARED_MEMORY_ADDRESS

<a id="18879c16c4456666"></a>
### 기본 정보

<a id="92a04d60cb6811fe"></a>
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

<a id="e3cf7ada7c07e247"></a>
### 설명

Shared Static Area (SSA)의 주소를 지정한다.

<a id="35ce92e943afa27c"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="52a679be77653d67"></a>
### 기본 정보

<a id="dcd5637015d8e250"></a>
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

<a id="7812a666e1734114"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory key 값을 지정한다.

<a id="4f093df7ab1c3b9f"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="1db319a4200d907b"></a>
### 기본 정보

<a id="68badcded128b0da"></a>
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

<a id="d7e7eef71ee8da60"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory name을 지정한다.

<a id="eadde14e86afa8c7"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="e5633cfa806505bc"></a>
### 기본 정보

<a id="36cc4754f5c7987c"></a>
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
| 기본값 | 838860800 (800M) |

<a id="90c60150f2523c48"></a>
### 설명

Shared Static Area (SSA)의 크기를 지정한다.

<a id="560333485e34f3e7"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="7133ce30e7e3f541"></a>
### 기본 정보

<a id="6ff2841b9fdfef09"></a>
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

<a id="9d40fb8a2b83e095"></a>
### 설명

Shared 모드의 dispatcher에서 shared-server로 요청하는 queue 개수를 설정한다. 여러 dispatcher가 사용자의 작업 요청을 shared-server에 할당할 때 사용하는 queue로써 일반적으로 load-balance를 위해 하나를 사용한다. 그러나 dispatcher와 shared-server가 많아지면 queue에 경합이 발생하여 성능이 저하될 수 있으므로 이 값을 늘려서 사용한다. 이 값이 커지면 load-balance가 비효율적으로 될 수 있고 dead-lock이 발생할 가능성이 커진다.

<a id="3f5f0e5fb86fd03e"></a>
## SHARED_SERVERS

<a id="d1ff82e961bb3914"></a>
### 기본 정보

<a id="60554b471b3a6932"></a>
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

<a id="2f6221d7a8d91c9d"></a>
### 설명

Shared 모드에서 shared-server process 개수를 설정한다.  
Open 단계에서는 alter system으로 값을 줄일 수 없다.

<a id="b4192347dae45357"></a>
## SHARED_SESSION

<a id="5e2d39c1496c014b"></a>
### 기본 정보

<a id="77b8c07bae1a2d62"></a>
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

<a id="cda2f2020cdbb1a9"></a>
### 설명

Shared 모드를 활성화할지 여부를 설정한다. 이 값을 NO로 설정하면 load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver)가 실행되지 않는다.

<a id="6a10fcab391aff45"></a>
## SHARED_SESSION_MEMORY_INIT_SIZE

<a id="ec7a1069e6258cf9"></a>
### 기본 정보

<a id="5b179694cc53d0a7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SHARED_SESSION_MEMORY_INIT_SIZE |
| 요약 | initial memory size for shared sessions |
| Data type | BIGINT |
| 적용단계 | NO MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 131072 (128K) |
| MAX | 1073741824 (1G) |
| 기본값 | 786432 (768K) |

<a id="d04022a70f25e05e"></a>
### 설명

공유 세션에서 사용할 메모리의 초기 크기를 설정한다.

<a id="ddc3e5e1f69bc16f"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="023e3c544ec91800"></a>
### 기본 정보

<a id="16d55afce8fb01f1"></a>
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

<a id="b881bb7ca0b2c51d"></a>
### 설명

Snapshot read가 필요로 하는 statement의 최대 유지 시간을 설정한다. 설정된 시간을 초과한 snapshot statement들에는 TIMEOUT 에러가 발생한다.

<a id="e98a7634442676d7"></a>
## SQL_HISTORY_SIZE

<a id="717f0f3cff1ced4f"></a>
### 기본 정보

<a id="3bdef4129e3aa473"></a>
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

<a id="33d7ae13ed5632e6"></a>
### 설명

SQLs의 이력 (history) 크기이다.

<a id="60e594bfba6ce057"></a>
## SQL_HISTORY_TYPE

<a id="1dbea82348158f0b"></a>
### 기본 정보

<a id="673507bbc92f729b"></a>
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

<a id="dc7620b1dae1bd91"></a>
### 설명

SQLs의 이력 (history) 타입이다.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="8f325c2202db88bb"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="a39af038a53104c4"></a>
### 기본 정보

<a id="76e960a83562c5a3"></a>
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

<a id="366df46d4581c350"></a>
### 설명

Database 내의 모든 변경 내용에 대한 supplemental log를 기록한다.

<a id="3e14bf273b75b9e8"></a>
## SYNC_DISPATCHER_CM_BUFFER_COUNT

<a id="dc7c3cb1fdaec96c"></a>
### 기본 정보

<a id="551401efd49290e7"></a>
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

<a id="03a8939b4b03699b"></a>
### 설명

Cluster synchronization dispatcher의 communication buffer 개수를 지정한다.

<a id="cf55d4d987b096b9"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="4f928caadad295ae"></a>
### 기본 정보

<a id="ea86428ce3451c3b"></a>
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

<a id="40177a1a3792d2ce"></a>
### 설명

데이터베이스를 생성할 때 초기 DISK_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="156f8d5c88f530b4"></a>
## SYSTEM_FILE_IO

<a id="0df9e26cfe6dd5b8"></a>
### 기본 정보

<a id="81db193dbae4c14d"></a>
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

<a id="85ee6e9572b9e463"></a>
### 설명

데이터 파일과 로그 파일을 제외한 데이터베이스 파일을 사용할 때 IO 타입을 설정한다.

<a id="896f6baf1337fc1e"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="8580c8719ccba0e3"></a>
### 기본 정보

<a id="e54c0afe03b9c4a5"></a>
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

<a id="21d9075f2f273bf3"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_AUX_TBS 테이블스페이스 크기를 결정한다.

<a id="84cf540b122a2747"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="b8a064d496fdcea2"></a>
### 기본 정보

<a id="c9970af6f6818261"></a>
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

<a id="ae9c30c27019fd19"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="2b76561b49e927aa"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="fc66fd47bd9c9df1"></a>
### 기본 정보

<a id="068740a44b3c45f8"></a>
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

<a id="032f7bc94d4932f7"></a>
### 설명

데이터베이스를 생성할 때 초기 DICTIONARY_TBS 테이블스페이스의 크기를 결정한다.

<a id="bfcfa7194429ad84"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="7dfeb0e4eb90e13c"></a>
### 기본 정보

<a id="3229887c30e2b194"></a>
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

<a id="41816c6c23a4aa95"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_TEMP_TBS 테이블스페이스의 크기를 결정한다.

<a id="51f4c56e7c21a3cb"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="995ad27c07f521d1"></a>
### 기본 정보

<a id="53b0d78b51d86352"></a>
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

<a id="a03a27e6ee4ddd3d"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_UNDO_TBS 테이블스페이스의 크기를 결정한다.

<a id="ec376b6168ad435d"></a>
## SYSTEM_TABLESPACE_DIR

<a id="45c5056397d985c9"></a>
### 기본 정보

<a id="9b129158451d2e06"></a>
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

<a id="845a2ad4a5673a12"></a>
### 설명

데이터베이스를 생성할 때 초기 시스템 테이블스페이스들이 저장되는 경로를 지정한다.

<a id="e89925794c22f514"></a>
## SYSTEM_UDS_DIR

<a id="ee9bf08afb2e827d"></a>
### 기본 정보

<a id="eb57d990f22804de"></a>
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

<a id="4cc43c5179505ae4"></a>
### 설명

Unix domain socket 파일이 생성되는 directory를 설정한다.  
DB system 이외에 glsnr 등과 같은 unix domain socket에 대한 디렉토리 설정은 별도의 configuration file에서 관리된다.  
최대 설정 크기는 60 byte이다. (Unix domain socket 파일의 절대 경로 (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.)

<a id="d2dcbd87077296c2"></a>
## TCP_CLIENT_NUMA_NODE

<a id="ec1f3c53834f5bd4"></a>
### 기본 정보

<a id="1868c0f163dc4c08"></a>
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

<a id="5f3db5183f5368af"></a>
### 설명

Client server 세션이 바인드 될 NUMA 노드 ID를 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="ee871a3db545a91d"></a>
## TCP_NODELAY

<a id="a3a136d31b8ce427"></a>
### 기본 정보

<a id="91ee5bf3bf75cef4"></a>
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

<a id="2688c2524ab24f00"></a>
### 설명

C/S 방식 (TCP socket)으로 client에 data를 전송할 때의 socket TCP_NODELAY 옵션을 설정한다.  
빠른 latency가 필요하지 않고 network 부하를 줄이고 싶은 경우에는 NO로 설정한다.

<a id="84f625f58bc56b82"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="507e782c2f918e25"></a>
### 기본 정보

<a id="45573e63aed25bf9"></a>
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

<a id="a0ef6869a2a08c22"></a>
### 설명

Global temporary table이나 global temporary index segment가 drop 될 때 tablespace에 반납하지 않고 session에서 caching 할 segment 개수를 지정한다. Segment cache에 존재하는 segment는 향후 global temporary table이나 global temporary index에서 재사용된다.

- 0: Session에서 global temporary table이나 global temporary index의 segment cache를 사용하지 않는다.
- 1 ~ 4294967295: Session에서 global temporary table이나 global temporary index의 segment cache를 주어진 개수만큼 유지한다.

<a id="d051cb46c0e94d3a"></a>
## TEMP_UNDO_ENABLED

<a id="8d2d78245a0358d9"></a>
### 기본 정보

<a id="baebe1d738cf935a"></a>
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

<a id="983bee4b873cb565"></a>
### 설명

Global temporary table에 대한 undo 레코드의 로깅 위치를 지정한다.

- 0 (FALSE): 데이터베이스의 기본 undo tablespace에 undo 레코드를 기록한다.
- 1 (TRUE): 데이터베이스의 기본 temporary tablespace에 undo 레코드를 기록한다.

<a id="b73832dfa73a430b"></a>
## TEMP_UNDO_SHRINK_THRESHOLD

<a id="a65f1fdfbb2209e3"></a>
### 기본 정보

<a id="8cc1193f62fc21f3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TEMP_UNDO_SHRINK_THRESHOLD |
| 요약 | threshold bytes to attempt to shrink temp undo segment ( byte ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1048576 |
| MAX | 107374182400 |
| 기본값 | 10485760 |

<a id="12c163281af02cdc"></a>
### 설명

세션에서 global temporary table 의 undo 레코드를 temp 테이블스페이스에 기록하는 경우, 완료된 트랜잭션이 사용한 undo 공간을 반납할 때 세션에 유지할 최소 공간을 설정한다. 이를 통해 undo 레코드 기록에 필요한 공간 할당 비용을 줄일 수 있다.

<a id="40f0de7f382d57f7"></a>
## TIMED_STATISTICS

<a id="fb1b4bb031bf3808"></a>
### 기본 정보

<a id="e41afbc3c62978b9"></a>
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

<a id="f02800dcb2bcf086"></a>
### 설명

Wait event를 측정하는지 여부이다.  
v$system_event, v$session_event, v$session_wait table에 wait event와 관련된 통계 기록을 남기고 싶은 경우에 설정한다.

- 0: 통계 기록을 남기지 않는다.
- 1: 통계 기록을 남긴다.
- 2: High precision timer를 이용하여 통계 기록을 남긴다.

<a id="98833ef747fb4e1b"></a>
## TIMER_INTERVAL

<a id="01d93ebfce288c3b"></a>
### 기본 정보

<a id="9cb3a70473509460"></a>
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

<a id="77251f83eeab5994"></a>
### 설명

타이머 thread가 시스템 시간을 설정할 수 있도록 시간 간격을 설정한다.

<a id="e5a8420441fa46e1"></a>
## TIMEZONE

<a id="135483e1370aa8d2"></a>
### 기본 정보

<a id="d5af6dbc23370bfd"></a>
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

<a id="28f561c8de1a8b13"></a>
### 설명

Database의 time zone 값이다.  
Database가 생성될 때 적용되는 속성으로써 -14:00 ~ +14:00 범위의 값을 사용할 수 있다.

<a id="dca051ef156256f4"></a>
## TRACE_ALTER_SYSTEM

<a id="1e6778f3c76ceb8e"></a>
### 기본 정보

<a id="d0ff906337d08484"></a>
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

<a id="bb46aa1239d2480e"></a>
### 설명

ALTER SYSTEM 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

시스템 변경에 대한 기록을 남기려면 TRACE_ALTER_SYSTEM 프로퍼티를 ON으로 설정한다.  

TRACE_ALTER_SYSTEM 프로퍼티는 SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="cee6761b96d13ea7"></a>
## TRACE_DDL

<a id="e15fa8ef6053444d"></a>
### 기본 정보

<a id="462b29b1a9a33696"></a>
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

<a id="5b6780622cd8f89b"></a>
### 설명

Data Definition Language (DDL) 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

테이블 생성, 삭제, 변경 등과 같은 SQL 문을 실행했을 때 이에 대한 기록을 남기려면 TRACE_DDL 프로퍼티를 ON으로 설정한다.  

TRACE_DDL 프로퍼티는 DDL 구문 수행에만 영향을 주며, SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="3afcdb7a99e99fc7"></a>
## TRACE_LOG_ID

<a id="3fd3d8ace9310210"></a>
### 기본 정보

<a id="1a90231db3796cbd"></a>
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

<a id="5a74dd7c91eb5f52"></a>
### 설명

질의를 수행할 때 해당 질의에 대한 실행 계획 정보와 기타 정보를 trace directory(&lt;GOLDILOCKS_DATA&gt;/trc/) 아래에 있는 trace file (opt_p[프로세스ID]_s[세션ID].trc)에 기록한다.

질의에 대한 SQL 구문과 실행 계획, 수행시간 등에 대한 기록을 남기려면 아래 표의 flag 정보를 조합하여 설정한다.

**TRACE_LOG_ID 의 flag 정보**

<a id="67e4de2f23f655d6"></a>
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

<a id="30596a9789bc4ec5"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="f21e2244a9865809"></a>
### 기본 정보

<a id="841bdb140d86fc43"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOG_MSGBUF_SIZE |
| 요약 | memory buffer size for trace log message |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 8192 |
| MAX | 10485760 |
| 기본값 | 24576 |

<a id="9052f696bd6d5e1f"></a>
### 설명

Trace logfile에 기록할 log message를 구성하는데 사용되는 heap memory buffer의 크기를 설정한다.

<a id="bc312de7e5b8cd1d"></a>
## TRACE_LOG_TIME_DETAIL

<a id="53bdae37a3ba0361"></a>
### 기본 정보

<a id="0a11f7aa61373147"></a>
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

<a id="febfd084fb5e1f21"></a>
### 설명

Trace log를 기록할 때 시간 정확도를 높일지 여부를 설정한다.  
이 값이 OFF로 설정된 경우, 10 ms의 정확도를 가지며, ON으로 설정된 경우 1 us의 정확도를 가진다.

<a id="ae6cea8b432b9fce"></a>
## TRACE_LOGGER

<a id="fbdd153a55b2ebbd"></a>
### 기본 정보

<a id="4284d480783b5cd5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER |
| 요약 | trace log type ( 1:file, 2:file & remote ) |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2 |
| 기본값 | 1 |

<a id="4e8e8f6e9f85633a"></a>
### 설명

Trace log를 기록할 대상을 설정한다.  
1이면 file에 기록하고 2이면 remote로 파일에 기록한다.  
Remote로 기록하면 gtrclogger에서 원격으로 trace log를 수집하여 파일에 기록한다.

<a id="09a801625fa6f527"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="e834278fa4331554"></a>
### 기본 정보

<a id="8476cf387f29da1d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER_REMOTE_HOST |
| 요약 | remote host for trace logger |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 0 |
| MAX | 255255255255 |
| 기본값 | 127000000001 |

<a id="573c361fe2181582"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 host를 설정한다.

<a id="db9c668cdf6330b6"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="1ad48bafe32be3cf"></a>
### 기본 정보

<a id="378296602c7f0f27"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRACE_LOGGER_REMOTE_PORT |
| 요약 | remote port for trace logger |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1024 |
| MAX | 49151 |
| 기본값 | 21470 |

<a id="8c2ccfc784eb4548"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 port를 설정한다.

<a id="9e34ea4f4be236e3"></a>
## TRACE_LOGIN

<a id="c41e1be43fb27e12"></a>
### 기본 정보

<a id="b72700f97fede714"></a>
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

<a id="51e0662c8faf52b8"></a>
### 설명

로그인 할 때 해당 접속 정보를 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc)에 기록한다.  
로그인 할 때 이에 대한 기록을 남기려면 TRACE_LOGIN 프로퍼티를 ON으로 설정한다.

<a id="50f8b0bc379ac3a1"></a>
## TRACE_LONG_RUN_CURSOR

<a id="c212ddf15b2e6052"></a>
### 기본 정보

<a id="32febbfbf2ff9068"></a>
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

<a id="e2008d52d2abf337"></a>
### 설명

Cursor의 lifetime이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#25cbf4dc5562ea4c) 프로퍼티를 사용한다.

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

<a id="07f05b1909ccb56b"></a>
## TRACE_LONG_RUN_SQL

<a id="1dcd5ceb381c00e8"></a>
### 기본 정보

<a id="339513a5cb670330"></a>
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

<a id="8e3ceb9dea360dba"></a>
### 설명

구문의 수행시간이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc) 에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#25cbf4dc5562ea4c) 프로퍼티를 사용한다.

- 수행시간이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="25cbf4dc5562ea4c"></a>
## TRACE_LONG_RUN_TIMER

<a id="63b49ef7bc03a409"></a>
### 기본 정보

<a id="5e39d1a200d55574"></a>
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

<a id="d9ba0dd57f8409c8"></a>
### 설명

다음 프로퍼티들을 이용하여 SQL 구문의 실행시간을 측정할 때 측정 정밀도를 제어한다.

- [TRACE_LONG_RUN_CURSOR](#50f8b0bc379ac3a1)
- [TRACE_LONG_RUN_SQL](#07f05b1909ccb56b)

- 값의 의미
    - 0: 10 millisecond의 interval을 가지는 timer thread를 사용한다.
    - 1: gettimeofday() 함수를 이용하여 시간을 측정한다. 정밀도는 높지만 system call로 인한 부하가 있다.

<a id="b3e61846fa02f601"></a>
## TRACE_SYSTEM_DIR

<a id="e7f7c52bceb7df30"></a>
### 기본 정보

<a id="f3a829cd08c6ffed"></a>
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

<a id="46c8469afe230258"></a>
### 설명

Trace 로그 메시지가 기록되는 디스크 경로를 지정한다.

<a id="85ead0ccec17551c"></a>
### ALIAS

<a id="ebae9e6570709a29"></a>
| 항목 | 설명 |
| --- | --- |
| 원본 이름 | TRACE_SYSTEM_DIR |
| ALIAS | SYSTEM_LOGGER_DIR |

<a id="181cfc8f91892c3b"></a>
## TRACE_XA

<a id="2987f052c21b029a"></a>
### 기본 정보

<a id="2f78e78a1084b9e3"></a>
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

<a id="1633d22bf809efc3"></a>
### 설명

XA 인터페이스를 사용할 때 추적 메시지를 출력할지 여부를 지정한다. 메시지는 'SYSTEM_LOGGER_DIR/xa.trc'에 출력된다.

<a id="78584ac42efdccf8"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="252cbf864af5fe14"></a>
### 기본 정보

<a id="e975493979a5960f"></a>
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

<a id="44e9495f3b9fed2f"></a>
### 설명

Transaction slot을 할당할 때의 최대 대기 시간이다.

대기 시간이 TRANSACTION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="ac89dc771d3d52e6"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="7d16e84e54bc5170"></a>
### 기본 정보

<a id="00924f9810379735"></a>
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

<a id="3001fa67544765d6"></a>
### 설명

TRANSACTION_COMMIT_WRITE_MODE는 트랜잭션이 완료될 때 트랜잭션이 생성한 log를 disk log file에 flush할지 여부를 설정한다. 즉, TRANSACTION_COMMIT_WRITE_MODE가 '1'이면 log를 트랜잭션 완료 시점에 disk log file에 flush해야 하고, 그렇지 않은 경우 log flush 여부와 관계없이 트랜잭션을 완료한다.

만약 TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정하여 시스템을 운용하는 경우에 트랜잭션을 COMMIT 한 후 log flush가 되지 않은 상태에서 GOLDILOCKS가 비정상적으로 종료되면 기록되지 않은 log로 인해 최신 data를 잃어버리게 된다.

따라서 모든 트랜잭션이 완료되었을 때 반드시 database에 남아 있어야 하는 경우 TRANSACTION_COMMIT_WRITE_MODE를 '1'로 설정하여 시스템을 운용하거나, TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정한 후 트랜잭션이 완료되는 시점에 명시적으로 'ALTER SYSTEM FLUSH LOGS' 문을 수행하여 log를 flush해야 한다.

- 0: no wait
- 1: wait

<a id="ec53960790e740e7"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="6c945a4f253d5a5a"></a>
### 기본 정보

<a id="ebd158a9dd0a570e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT |
| 요약 | 트랜잭션이 기록할 수 있는 최대 undo페이지 개수 |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 13107200 |
| 기본값 | 13107200 |

<a id="07505b94986dfb16"></a>
### 설명

트랜잭션이 기록할 수 있는 최대 undo 페이지 개수를 의미한다. 최소값은 1로 8 Kbyte이며, 최대값은 13107200으로 100 Gbyte이다.

<a id="e20fffefb153528b"></a>
## TRANSACTION_TABLE_SIZE

<a id="493a39c5abcc8ee8"></a>
### 기본 정보

<a id="a0c4780a5a19b83a"></a>
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

<a id="ae63881fe27c1c6f"></a>
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

<a id="5d2fd54f73660f73"></a>
## TRANSACTION_TIMEOUT

<a id="31bdcf9d0c3b8f43"></a>
### 기본 정보

<a id="a900bbfe2e551a8b"></a>
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

<a id="2bb93c32899a51b2"></a>
### 설명

Transaction이 활성화되어 있는 시간을 설정한다. Transaction이 장시간 활성화되어 있을 때 발생할 수 있는 부작용을 예방하기 위해 사용된다. 정해진 시간을 초과한 transaction이 있을 경우, gmaster 데몬이 해당 transaction을 소유한 세션을 자동으로 종료시킨다.

<a id="27b41071063b2d5f"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="aa1940cbe55cbbc6"></a>
### 기본 정보

<a id="d00404fd2b1263e8"></a>
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

<a id="b86a5a2f7d37caa7"></a>
### 설명

Undo relation을 할당할 때의 최대 대기 시간이다.

대기 시간이 UNDO_RELATION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="9722b537614d22f0"></a>
## UNDO_RELATION_COUNT

<a id="83ab6fad3ca7c8f8"></a>
### 기본 정보

<a id="160d25f6b4738ce1"></a>
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

<a id="82aeb545af8a960e"></a>
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

<a id="cac4b9fe16db8588"></a>
## UNDO_SHRINK_THRESHOLD

<a id="c985254192dbcde2"></a>
### 기본 정보

<a id="3ac66b15a427f72c"></a>
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

<a id="68e752f25963d18d"></a>
### 설명

Ager thread는 주기적으로 (10초) undo segment 공간을 검사하여 이 속성값보다 많은 공간을 차지하고 있을 경우, 재사용 가능한 공간을 테이블스페이스로 반환한다. Undo segment의 공간이 이 속성 (byte)만큼 남을 때까지 반환을 시도하다가 남은 undo page의 양이 MINIMUM_UNDO_PAGE_COUNT보다 작아지면 반환을 종료한다.

<a id="35d8eefa81d7d694"></a>
## USE_LARGE_PAGES

<a id="bc1bcf436c03335a"></a>
### 기본 정보

<a id="bda0eef4fd0af8a1"></a>
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

<a id="22d01a972c835c70"></a>
### 설명

HugePage를 사용한다. USE_LARGE_PAGES를 사용하려면 먼저 장비에 HugePage를 설정해야 한다.

- 0: Large page를 사용하지 않는다.
- 1: Large page를 사용한다. 만약 공유 메모리 할당에 실패할 경우에는 에러가 발생한다.
- 2: Large page를 사용하여 할당을 시도한다. 만약 공유 메모리 할당에 실패할 경우에는 regular page를 사용하여 메모리를 할당한다.

> 리눅스 커널 2.6.32-573 이상에서만 사용할 수 있다.

<a id="41cc3c3fbab12ffb"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="7effc8254078e048"></a>
### 기본 정보

<a id="cc3330e345f35572"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | USER_DATA_TABLESPACE_MEDIA_TYPE |
| 요약 | default media type of user data tablespace |
| Data type | BIGINT |
| 적용단계 | NO_MOUNT 이상 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | TRUE |
| ALTER SYSTEM 여부 | DEFERRED |
| MIN | 0 ( Memory ) |
| MAX | 1 ( Disk ) |
| 기본값 | 0 ( Memory ) |

<a id="b55164617263db74"></a>
### 설명

사용자 데이터 테이블스페이스를 생성할 때 테이블스페이스의 media 타입이 생략된 경우, default media 타입을 지정한다. 0은 memory, 1은 disk를 의미한다.

<a id="d1de56fb0f9fea7f"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="eadf671b6fc7a492"></a>
### 기본 정보

<a id="81b6b092bb5e38d7"></a>
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

<a id="1ba339dbbe349674"></a>
### 설명

사용자 데이터 테이블스페이스가 생성되거나 데이터 파일이 추가될 때 데이터 파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="b90b6eb5b52f00b0"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="c658e52ced233360"></a>
### 기본 정보

<a id="d7c1889ac73799ac"></a>
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

<a id="fade4deac5d21055"></a>
### 설명

사용자 디스크 데이터 테이블스페이스의 데이터파일이 확장되어야 할 때 확장할 크기가 설정되지 않은 경우, default 크기를 지정한다.

<a id="cb1e9c16ef5eb648"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="078ff77e07912a85"></a>
### 기본 정보

<a id="b15e6a2b061d0ed7"></a>
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

<a id="a1284b66536c56d0"></a>
### 설명

사용자 temp 테이블스페이스가 생성되거나 데이터파일이 추가될 때 데이터파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="5a7b7c7b08908129"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="61d0f5aaa38f6029"></a>
### 기본 정보

<a id="24536de0a55ace96"></a>
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

<a id="15eeddf120379a8a"></a>
### 설명

Xa transaction이 idle 상태 (XA가 시작된 후 다음 처리가 발생할 때까지 시간)로 대기할 수 있는 최대 시간이다. Idle 상태로 대기하다가 이 시간을 초과하면 xa transaction은 rollback 된다.

0으로 설정하면 XA가 idle 상태로 있더라도 무한 대기한다.

---

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
