<a id="4752291cb768d51a"></a>

# 10. Server Property

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/4752291cb768d51a)  
> 태그: `21c.1_35_tag`

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="e2d4a0a855db668d"></a>
## Server Property 정보

Property는 다음 SQL 구문으로 변경할 수 있다.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#af037c637cf5ed8e) 
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#a0d698a8bdefa8ba)

Property 정보는 다음 view로 확인할 수 있다.

- [V$PROPERTY](9-database-information.md#0b34777589cc694d)
- [V$SPROPERTY](9-database-information.md#6b645a6cf042e8a2)

본 매뉴얼의 property 기본 정보 각 항에 대한 설명은 다음과 같다.

<a id="0db97649fed1ee94"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | Property의 구분자이다. |
| 요약 | Property 요약 설명이다. |
| Data type | Property가 갖는 값의 데이터 타입이다. |
| 적용 단계 | ALTER SYSTEM 또는 ALTER SESSION으로 변경할 수 있는 startup phase에 적용할 수 있다 * NONE: 적용할 수 있는 단계가 없다. (만약 변경 가능하지만 적용 단계가 NONE인 경우에는 SCOPE = FILE을 이용해야 한다.) |
| 변경가능 여부 | Property를 변경할 수 있는지 여부이다. * 해당 값이 TRUE일 경우, 변경할 수 있다. * 해당 값이 FALSE일 경우, read-only만 가능하다. |
| ALTER SESSION 여부 | [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#a0d698a8bdefa8ba) 구문으로 변경할 수 있는지 여부이다. |
| ALTER SYSTEM 여부 | [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#af037c637cf5ed8e) 구문으로 변경할 수 있는지 여부이다. * IMMEDIATE: 수행 즉시 모든 SESSION에 변경된 값이 반영된다. * DEFERRED: 수행된 이후에 접속한 SESSION에만 변경된 값이 반영된다. 이미 접속된 SESSION에는 반영되지 않는다. * FALSE: 운영 중에는 변경된 값이 반영되지 않으며 restart 이후에 변경된 값이 반영된다. SCOPE=FILE로만 수행할 수 있다. * NONE: 변경할 수 없다. |
| MIN | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최소값이다.  VARCHAR일 경우에는 N/A이다. |
| MAX | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최대값이다. VARCHAR일 경우에는 N/A이다. |
| 기본값 | 해당 property가 갖는 기본값이다. |

<a id="11826f5332bbb858"></a>
## AGING_INTERVAL

<a id="ae78e77dbd812302"></a>
### 기본 정보

<a id="ae1bad8629f49527"></a>
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

<a id="bd52f4bf236704c6"></a>
### 설명

MVCC 기반의 database에서 이전 버전의 데이터를 지우는 ager thread가 처리할 job이 없을 때의 유휴 시간 (초)을 설정한다.

<a id="5594ff30c03e69ba"></a>
## AGING_PLAN_INTERVAL

<a id="f0aa9c08aac148bc"></a>
### 기본 정보

<a id="85bf9b1a6f451030"></a>
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

<a id="0644ceddb675f195"></a>
### 설명

AGING_PLAN_INTERVAL 보다 오래된 SQL plan이 aging 대상이 된다.

<a id="453ac01cb35a1161"></a>
## ARCHIVE_LOG_THROTTLING

<a id="b2700642a66b2db2"></a>
### 기본 정보

<a id="796618d1bcec8b42"></a>
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

<a id="5ae4470c9badfd31"></a>
### 설명

Redo log를 archiving할 때 디스크 I/O 성능을 제어하기 위한 프로퍼티이다.   
대상 파일로 복사된 데이터 크기가 해당 프로퍼티 값보다 커질 때마다 한 번씩 sleep 을 수행한다.

<a id="c33cd94f38935a55"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="3611c54f72132710"></a>
### 기본 정보

<a id="936d9f26d1ab0982"></a>
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

<a id="8169c6878db53e88"></a>
### 설명

GOLDILOCKS 데이터베이스의 온라인 redo log file이 archive되는 디렉토리와 미디어 복구할 때 archive redo log file을 읽을 위치를 설정한다. 온라인 redo log file은 ARCHIVELOG_DIR_1에만 archive redo log file을 생성한다.

ARCHIVELOG_DIR_1은 시스템만 설정할 수 있고 ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10은 세션을 설정할 수 있다.

<a id="430ed855f0c209ce"></a>
## ARCHIVELOG_FILE

<a id="efdf72f82352bcf2"></a>
### 기본 정보

<a id="c61a1ed75b7b0b2f"></a>
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

<a id="7b56c63536c1e66a"></a>
### 설명

온라인 redo log file을 archive 할 때 archive 디렉토리에 저장되는 목적 파일 이름의 prefix를 설정한다. Archive log file은 ARCHIVELOG_FILE에 설정된 prefix에 '_'와 파일 시퀀스, 'log' 확장자가 추가된 형태로 생성된다. 예를 들어, 파일 시퀀스가 0인 로그 파일은 'archive_0.log'으로 아카이빙된다.

<a id="99ef54757baa17e2"></a>
## ARCHIVELOG_MODE

<a id="61dd1a8892320c03"></a>
### 기본 정보

<a id="7dca4e8f47ddeeae"></a>
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

<a id="12ad98ff420205d8"></a>
### 설명

Database를 생성할 때 적용되는 속성으로써 archive log mode를 다음 중 하나의 값으로 설정할 수 있다.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

Database가 생성된 후 운용되는 동안에는 archive log mode에 영향을 미치지 않고 mount 단계에서 ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}로 archive log mode를 변경할 수 있다.

<a id="1c86068e772f40dc"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="5c906c22a4f6132b"></a>
### 기본 정보

<a id="ce045d4f0fd79781"></a>
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

<a id="bf664cbfac400a8a"></a>
### 설명

증분 백업이 수행될 때 백업 파일이 생성되고 증분 백업을 이용하여 파일을 복원할 때 백업 파일이 읽혀질 디렉토리를 설정한다. 증분 백업은 BACKUP_DIR_1에 설정된 디렉토리에만 생성된다.

BACKUP_DIR_1은 시스템만 설정할 수 있고 BACKUP_DIR_2 ~ BACKUP_DIR_10은 세션을 설정할 수 있다.

<a id="1914cfbbe1e0332b"></a>
## BLOCK_READ_COUNT

<a id="091f192ebf2cf38e"></a>
### 기본 정보

<a id="9870adf0beb038b5"></a>
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

<a id="6206b1900f857136"></a>
### 설명

SQL 처리시 row의 묶음 단위인 BLOCK_READ_COUNT 단위로 row를 읽어 연산을 처리한다.   
BLOCK_READ_COUNT는 연산을 수행할 때 한 번에 처리할 row의 개수를 의미하며 SQL 질의 처리에 참여하는 실행 노드간의 pipe-lining 처리의 기본 단위이다.

BLOCK_READ_COUNT 값이 크면 연산 처리 성능은 향상되지만 메모리 자원을 많이 사용한다.  따라서 10 ~ 100 사이의 값을 권장한다. 그 이상의 값을 사용하는 경우 자원 사용량은 비례하여 증가하지만 성능은 비례하여 향상되지 않는다.

<a id="b70c377d862562f2"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="79d20344fffd50c7"></a>
### 기본 정보

<a id="699cb7c2f38f2b5a"></a>
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

<a id="94786d744ca59dd7"></a>
### 설명

클러스터 환경에서 인덱스를 재구축할 때 여러 멤버에서 동시에 처리할지 여부를 설정한다.

<a id="7ec0536410bd3683"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="9bf839aca38c1f00"></a>
### 기본 정보

<a id="0e3903b49758b553"></a>
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

<a id="4f076fb73a4e2fb4"></a>
### 설명

클러스터 환경에서 테이블 리밸런스를 수행할 때 여러 멤버에서 동시에 처리할 수 있는 프로토콜을 동시 처리할지 여부를 설정한다.

<a id="af23e99f2a820376"></a>
## BUFFER_CACHE_SIZE

<a id="ebd82756a681248f"></a>
### 기본 정보

<a id="4eed7ccd92b9e352"></a>
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

<a id="e3641c8a153c7a12"></a>
### 설명

디스크 테이블스페이스의 페이지를 caching하는 버퍼의 크기를 설정한다.

<a id="3d8cf206ce26d0af"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="f78389e75ba860fe"></a>
### 기본 정보

<a id="d6f30880f7dc9835"></a>
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

<a id="99a23ea6b9af4b25"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스의 페이지들이 갱신되었을 때 체크포인트 리스트에 연결된다. 각 체크포인트 리스트는 전용 flush thread에 의해 체크포인트 리스트에 연결된 갱신된 페이지를 디스크로 flush 하는데 BUFFER_CHECKPOINT_LIST_COUNT는 체크포인트 리스트의 개수와 flush thread의 개수를 설정한다.

<a id="befce2de61e6c6c1"></a>
## BUFFER_FLUSH_THREADS

<a id="8765f2f4bfb71948"></a>
### 기본 정보

<a id="5c7679e284c2b418"></a>
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

<a id="52ec483da1e69e73"></a>
### 설명

버퍼 lru list에서 갱신된 페이지를 caching한 bch를 재사용하려면 flush list에 연결하여 buffer flusher에 flush를 요청하게 되는데, 이 때 BUFFER_FLUSH_THREADS가 데이터베이스에서 사용할 buffer flusher와 flush list의 수를 설정한다.

<a id="eb4b7289d36f75e9"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="338a2622bf6ee56e"></a>
### 기본 정보

<a id="a8160b16f530fd9d"></a>
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

<a id="b9fd64abf1f02d95"></a>
### 설명

갱신된 디스크 테이블스페이스 페이지들을 디스크로 flush하는 버퍼 flusher가 처리할 job이 없을 때의 유휴 시간 (sec)을 설정한다.

<a id="38dac921a46c21bb"></a>
## BUFFER_FREE_LIST_COUNT

<a id="d0ac772df814f673"></a>
### 기본 정보

<a id="8e98ac80a556b311"></a>
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

<a id="3399ab12404bf089"></a>
### 설명

버퍼 캐쉬에 즉시 사용 가능한 bch들을 연결하는 buffer free list의 수를 설정한다.

<a id="b3b2d5003f2527d3"></a>
## BUFFER_HASH_BUCKETS

<a id="bcf53b2347a36346"></a>
### 기본 정보

<a id="56e242670014d7ac"></a>
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

<a id="68ac081061ea3eac"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스 페이지를 위한 hash bucket의 개수를 설정한다. 0 부터 1073741824 까지 설정할 수 있으며 0은 BUFFER_CACHE_SIZE에 따라 설정된 버퍼에 caching 할 수 있는 페이지 수만큼의 hash bucket을 계산하여 설정한다. 만약 설정된 값보다 버퍼의 크기가 작으면 버퍼의 크기로 hash bucket 수를 조정한다.

<a id="003129e5e4ca7c3f"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="c242d36637e5943c"></a>
### 기본 정보

<a id="de7690be04bd6403"></a>
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

<a id="b620a421c0fc6e00"></a>
### 설명

버퍼 lru list에서 cold region에 존재하는 페이지를 hot region으로 옮기기 위한 touch count를 설정한다.

<a id="baff3957de2c84ff"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="66710ca7b9894016"></a>
### 기본 정보

<a id="459bfdfe27876922"></a>
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

<a id="cd66918a8028542e"></a>
### 설명

버퍼 lru list에 존재하는 전체 페이지 중에 hot region의 페이지의 비율 (백분율)을 설정한다.

<a id="c718c59538b5e3f5"></a>
## BUFFER_LRU_LIST_COUNT

<a id="d01a27d82ec5c9a0"></a>
### 기본 정보

<a id="f8045548130a55b8"></a>
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

<a id="4e936698ac0a23f8"></a>
### 설명

디스크 테이블스페이스 페이지를 caching 하기 위한 free buffer가 없을 때 caching하여 사용 중인 페이지들 중에 victim을 선정하기 위한 lru list의 수를 설정한다.

<a id="1a37cbb8adb079ee"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="5fda0dd2ebaad727"></a>
### 기본 정보

<a id="e40250c2f93abea6"></a>
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

<a id="7e3b309fe33a51f3"></a>
### 설명

디스크 테이블을 full scan 할 때 한 번의 디스크 IO에 사용할 최대 페이지 수를 설정한다.

<a id="0ccb362b42900cce"></a>
## BUFFER_PREFETCH_PAGE_COUNT

<a id="59024e3d2e51a09e"></a>
### 기본 정보

<a id="4f1bd75b0666c65a"></a>
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

<a id="1f85c92a3fc647e2"></a>
### 설명

버퍼에 존재하지 않는 디스크 테이블스페이스의 페이지에 접근할 때 한 번의 디스크 I/O로 프리 페치할 인접한 최대 페이지 수를 설정한다.

<a id="501a823fe67aed05"></a>
## BULK_IO_PAGE_COUNT

<a id="9a777eede313762e"></a>
### 기본 정보

<a id="7e6b23200c6f5f00"></a>
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

<a id="c3eb3dd213c69cc6"></a>
### 설명

서버를 재시작할 때 데이터 파일에 IO READ가 발생할 경우나 데이터 파일을 생성할 때 IO WRITE가 발생할 경우에 사용된다.

서버를 재시작하거나 데이터 파일을 생성할 때 BULK_IO_PAGE_COUNT * 8192 크기만큼 heap 메모리가 할당되며 세션의 PRIVATE_STATIC_AREA_SIZE가 그 크기보다 작을 경우 메모리 부족 에러가 발생할 수 있다. 이 경우에는 PRIVATE_STATIC_AREA_SIZE를 늘려주어야 한다.

<a id="a5902e8ebdccaed9"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="849d139047e32bba"></a>
### 기본 정보

<a id="92a5772f8c21e7e4"></a>
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

<a id="60d30119551542a2"></a>
### 설명

cdispatcher에서 dequeue 할 때 busy waiting 하는 시간이다. Micro second 단위이며 이 값을 크게 하면 CPU를 많이 사용하는 대신 사용자 응답 시간 (latency)은 줄어든다.  
기본값은 0 이고 busy waiting 을 하지 않는다.

<a id="0a64a72404cc4aed"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="416aab71bbabbc8a"></a>
### 기본 정보

<a id="1a34b22a0c994c4b"></a>
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

<a id="d78ff8f1d866ac4f"></a>
### 설명

Lockless 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockable 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_THREADS](#e75668d124fb6778)로 설정한다.

<a id="b623b3db3ed8f6c8"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="28fdac9a0689d623"></a>
### 기본 정보

<a id="0a3d7570f2424862"></a>
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

<a id="957bc57bbd4f627d"></a>
### 설명

cdispatcher socket buffer (송신자, 수신자)의 크기이다.

<a id="867c097e423a6539"></a>
## CDISPATCHER_SYNC_THREADS

<a id="3a5b60ae9898639a"></a>
### 기본 정보

<a id="47c99d95ca62f035"></a>
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

<a id="5aef20fe1b1bc883"></a>
### 설명

cdispatcher sync thread의 개수이다.

<a id="e75668d124fb6778"></a>
## CDISPATCHER_THREADS

<a id="6e6ba0f7ab663e79"></a>
### 기본 정보

<a id="d65e666e5a34b4c9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CDISPATCHER_THREADS |
| 요약 | cdispatcher lockable sender, receiver thread count |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 30 |
| 기본값 | 1 |

<a id="e24bb38e3f082d21"></a>
### 설명

Lockable 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockless 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKLESS_THREADS](#0a64a72404cc4aed)로 설정한다.

<a id="b764c42af6457346"></a>
## CHANGE_TRACKING

<a id="4350aec75f164134"></a>
### 기본 정보

<a id="a098578367857271"></a>
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

<a id="d2182c1ee2e20ae3"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 변경된 페이지들을 tracking 할지 여부를 설정한다.

- NO: disable change tracking
- YES: enable change tracking

데이터베이스가 archivelog로 운용 중인 경우에만 mount 이상 단계에서 ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING 으로 change tracking을 enable 할 수 있다.

<a id="60668b034f85e125"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="928be07b7819b5df"></a>
### 기본 정보

<a id="f54b977135ad915a"></a>
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

<a id="4014c381142d1c76"></a>
### 설명

Change tracking 할 때 하나의 dirty flag로 표시할 페이지 수를 설정한다. 예를 들어, 32로 설정하면 32 페이지당 하나의 dirty flag를 사용하고, 128로 설정하면 128 페이지당 하나의 dirty flag를 사용한다.

<a id="2f915b69e41d9b2c"></a>
## CHANGE_TRACKING_FILE

<a id="423069f4daa7a2ec"></a>
### 기본 정보

<a id="cd38d707456533e9"></a>
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

<a id="90dc2034b6004aa3"></a>
### 설명

Change tracking을 저장할 파일의 디렉토리와 파일 이름을 설정한다.

<a id="b205bdf9941e1ed4"></a>
## CHAR_LENGTH_UNITS

<a id="8928cb35e438beed"></a>
### 기본 정보

<a id="e1043bb7cc7d9ce6"></a>
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

<a id="66ccb6da44ec6236"></a>
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

<a id="752cf14717dffe5e"></a>
## CHARACTER_SET

<a id="c634cefe0d29c790"></a>
### 기본 정보

<a id="5292e8a2ee478917"></a>
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

<a id="d01ac4133a82d7db"></a>
### 설명

Database의 character set이다.  
Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값을 설정할 수 있다.

<a id="e79a6eeb4c2ea1ec"></a>
| Character set | 설명 |
| --- | --- |
| SQL_ASCII | ASCII standard |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standard |

<a id="f43afba9727e1ce1"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="0cb28dbd96e53dad"></a>
### 기본 정보

<a id="54c21294f2673c48"></a>
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

<a id="a217b307c4aeef9c"></a>
### 설명

C/S dedicate 환경에서 client가 접속을 강제로 종료했을 경우, 이를 검사하는 주기이다. Dedicate server (gserver)가 socket을 확인하여 끊어졌으면 종료한다. 기본값은 1,000 millisecond (1초)이다.

<a id="feb92027c7bd9205"></a>
## CLIENT_MAX_COUNT

<a id="052b772ca2f04899"></a>
### 기본 정보

<a id="1091c0f5d301c6f9"></a>
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

<a id="cee57818ce7bebfb"></a>
### 설명

접속할 수 있는 세션의 최대 개수를 설정한다.

<a id="58a25c6a27ae4066"></a>
## CLIENT_NUMA_POLICY

<a id="f30e6103c45bbf05"></a>
### 기본 정보

<a id="438f6d821d3851ac"></a>
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

<a id="5a0b58b7b0665b2c"></a>
### 설명

Client 프로세스들을 NUMA 노드들에 분배하기 위한 정책을 결정한다. CLIENT_NUMA_POLICY 프로퍼티는 NUMA 프로퍼티가 on 되어있을 때 동작한다.

- 0: 세션 ID를 모듈러 (modular)해서 연결할 NUMA 노드를 결정한다.
- 1: 통계정보를 바탕으로 가장 조금 연결되어 있는 NUMA 노드에 우선적으로 연결한다.
- 2: C/S client는 TCP_CLIENT_NUMA_NODE 프로퍼티에 의해서 결정되고, D/A client는 DA_CLIENT_ NUMA_NODE 프로퍼티에 의해서 결정된다.

<a id="dba1af2f83ec9b8c"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="a9a10bb0511b2f77"></a>
### 기본 정보

<a id="bb5c7231d99b2cbc"></a>
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

<a id="5cb095a22a2744e3"></a>
### 설명

매 실행 마지막에 PSM의 child 구문을 close 한다.

<a id="d6c3a346f4080fd4"></a>
## CLUSTER_ASYNC_COMMIT

<a id="4841e513470ef073"></a>
### 기본 정보

<a id="e1d58c4ab92a16dd"></a>
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

<a id="2dfc9b7c0491c8ce"></a>
### 설명

Cluster system에서 내부적으로 commit protocol을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 commit을 비동기 처리하기 때문에 일시적으로 노드별 consistency가 깨어질 수 있다. 반면에 이 프로퍼티가 꺼져 있으면 commit 할 때마다 동기화하기 때문에 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="d743a95184734953"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="8a9cf089b3a3a667"></a>
### 기본 정보

<a id="94e8d5a371b8aa21"></a>
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

<a id="e31e6dacfda087ef"></a>
### 설명

Cluster system에서 내부적으로 replication을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 데이터를 비동기적으로 반영하기 때문에 어떤 노드에 접속하여 작업을 수행하는지에 따라 응답시간이 차이난다. 반면에 이 프로퍼티가 꺼져 있으면 데이터를 변경할 때마다 동기화하기 때문에 전체 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="b0c7c8683e3f60f0"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="daafb82f68762694"></a>
### 기본 정보

<a id="729ffedffe4e0a99"></a>
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

<a id="59146ad4e31ca501"></a>
### 설명

Cluster의 communication buffer 개수이다.

<a id="aca316a3d80f8a7c"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="90da98086ef98e56"></a>
### 기본 정보

<a id="98d42bbf59be394e"></a>
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

<a id="50a50baae94432d8"></a>
### 설명

Cluster의 communication buffer 크기이다.

<a id="740d96edb10d6187"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="09025dee9a75b654"></a>
### 기본 정보

<a id="db1b2061100da324"></a>
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

<a id="86d83c1768fe6b35"></a>
### 설명

Communication read block의 크기이다.

<a id="d516906f2cad611f"></a>
## CLUSTER_COMMIT_SLAVES

<a id="b9fd8adf5007afe6"></a>
### 기본 정보

<a id="be86e50af92d43d6"></a>
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

<a id="b95c935dfa5d2fb0"></a>
### 설명

Commit slave의 번호이다.

<a id="15f8b5437d12b41e"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="271b2ada8aeacaab"></a>
### 기본 정보

<a id="e46f36e56e3d1d21"></a>
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

<a id="4b706140e7969044"></a>
### 설명

Cluster system에서 내부적으로 commit 처리 흐름을 다른 protocol 처리와 분리하여 수행할 것인지 여부를 설정한다. 시스템 환경에 따라 commit 처리를 분리할 경우 성능이 향상될 수 있다.

<a id="442abf3deceaaf13"></a>
## CLUSTER_CONNECTION

<a id="1958d8bf901c285e"></a>
### 기본 정보

<a id="c4e8f8fa35983e82"></a>
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

<a id="7395f4c611b53d61"></a>
### 설명

Cluster의 connection mode이다. (socket: 0, rdma:1)

<a id="4905eaefcd761478"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="95285b87e65647f2"></a>
### 기본 정보

<a id="23cffe8a1171231c"></a>
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

<a id="5183ba240ec8d4a5"></a>
### 설명

Cluster의 connection timeout 이다.

<a id="347e0608ca765ce8"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="efe95a295784ff1e"></a>
### 기본 정보

<a id="cb1eb5b677edb806"></a>
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

<a id="4223aea6fa72ad9a"></a>
### 설명

Data synchronization server의 개수이다.

<a id="00e2d5e83b8865c8"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="8a5e4118bf2e39d5"></a>
### 기본 정보

<a id="82baf2a83fa1476e"></a>
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

<a id="ed07c948d07c1f9f"></a>
### 설명

Lockable cluster server 부족 등으로 인해 cluster server를 점유하려는 경합이 심해지면 cluster deadlock이 발생할 수 있다. Cluster deadlock이 발생하면 이 프로퍼티에 설정된 시간만큼 deadlock이 해결되기를 기다리는데 해결되지 않을 경우에는 CLUSTER_DEADLOCK_TIMEOUT 에러가 발생한다.

<a id="54cb47f5421fc050"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="7d9dab437dac81b8"></a>
### 기본 정보

<a id="99b63b01b76b6b48"></a>
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

<a id="b759b9ee5d2cc4e0"></a>
### 설명

Cluster dispatcher in-queue의 크기이다.

<a id="117b958af4274e52"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="b109358e1f24f5b4"></a>
### 기본 정보

<a id="6ac2dd8594683f7e"></a>
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

<a id="9bafe38a4ab1670b"></a>
### 설명

Cluster 디스패처들이 연결될 NUMA 노드를 결정한다. CLUSTER_DISPATCHER_NUMA_STREAM_MAP 프로퍼티는 NUMA 프로퍼티가 on되어 있을 때 동작한다.

> 만약 CLUSTER_COMMIT_STREAM_ISOLATION 프로퍼티가 on 되어 있다면 0번 스트림은 commit stream의 NUMA 노드로 설정된다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고 1번 스트림은 NUMA 노드 1번에 연결하며 2번 스트림은 NUMA 노드 2번에 연결한다.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="8a5477d8b8e01ada"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="6528335d8e98c5af"></a>
### 기본 정보

<a id="f7395487fcd0febc"></a>
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

<a id="1d3eceab794b628a"></a>
### 설명

Cluster dispatcher의 out-queue 크기이다.

<a id="95fc44bc900e37e3"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="a090cde7730daf5b"></a>
### 기본 정보

<a id="f0c73a16fbbb1138"></a>
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

<a id="81d011be9f105fe8"></a>
### 설명

Cluster의 상태를 점검하는 주기 (초)이다. 0은 비활성화 상태를 의미한다.

<a id="e3992b6945e6c1b8"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="83d89a29f8039361"></a>
### 기본 정보

<a id="602e2472d8d617a8"></a>
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

<a id="19dd90fc1ca59af3"></a>
### 설명

Cluster 상태 점검을 다시 시도하는 횟수이다.

<a id="b820a93ca23bfc7c"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="95646b09c9630aa5"></a>
### 기본 정보

<a id="cd556f3665f6145b"></a>
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

<a id="38b903ee4873a068"></a>
### 설명

Cluster의 in-active 멤버를 무시한다.

<a id="65e2f04d14084ec9"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="2f55cced34b86684"></a>
### 기본 정보

<a id="8969ac5a958790be"></a>
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

<a id="1c66d12467c0399e"></a>
### 설명

원격 프로토콜이 한 번에 전송할 수 있는 패킷의 최대 크기를 결정한다. 원격으로 전송해야 하는 column의 크기가 CLUSTER_MAX_PACKET_SIZE 프로퍼티 크기를 초과할 경우, 해당 프로퍼티를 column 크기보다 크게 설정해야 한다.

<a id="1b00d9d7fcf8facf"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="4ce8e25faa25b2ac"></a>
### 기본 정보

<a id="a42cae3c4ff7da7c"></a>
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

<a id="20c88f640ea35ce8"></a>
### 설명

원격으로 전송되는 클러스터 패킷은 여러 개의 piece로 나뉘어 전달될 수 있는데 CLUSTER_MAX_PAYLOAD_SIZE 프로퍼티는 하나의 piece에 저장할 수 있는 데이터의 최대 크기를 설정한다.

<a id="2106ddaa1da9648d"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="5e731b084fde0960"></a>
### 기본 정보

<a id="1bd14c44ee019a9b"></a>
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

<a id="0797ae75196bdd1b"></a>
### 설명

Cluster 패킷 구성에 필요한 메모리를 할당할 때 기다릴 수 있는 최대 시간 (초)을 설정한다.

<a id="54575aaf64b0f077"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="b1773ccb46e83763"></a>
### 기본 정보

<a id="f944888cfbea64de"></a>
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

<a id="0ad39eecb7c3f5cd"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Failover 시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, session을 종료시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#cca33b61c502ca13) property를 사용하여 제한 시간을 설정한다.

<a id="cca33b61c502ca13"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="119858903f90278b"></a>
### 기본 정보

<a id="c482ccfb6455705e"></a>
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

<a id="2c930129fcdb4e6c"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Session을 종료시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, failover 시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#54575aaf64b0f077) property를 사용하여 제한 시간을 설정한다.

<a id="cfad175e0322fe77"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="fa50b9e0f261c93c"></a>
### 기본 정보

<a id="35a335150a92648f"></a>
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

<a id="a5d6d7051db00f72"></a>
### 설명

원격 서버로부터 응답을 받기 위한 queue의 최대 크기를 설정한다.

<a id="bb414ddebf4ccb10"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="1af79dc13b7d8103"></a>
### 기본 정보

<a id="6e75ed6d4f43e57e"></a>
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

<a id="eae0431f88a2b0f4"></a>
### 설명

Cluster session을 관리하기 위한 hash bucket의 개수를 설정한다.

<a id="b0f8ad4bc44dbe18"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="a5f7a43ea5611018"></a>
### 기본 정보

<a id="c517ac847e3186a2"></a>
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

<a id="9c02f364c50d5f3a"></a>
### 설명

Cluster system에서 split-brain 상황을 해결하기 위한 정책을 설정한다. 1 이상의 값으로 설정할 경우 해결 방안을 locator에게 질의한다.

> Locator에게 한 질의에 timeout이 발생하면 CLUSTER_SPLIT_BRAIN_RETRY_COUNT만큼 질의를 시도한다. 재시도에 실패하면 속성값이 1인 경우에는 failover를 강제로 진행하고 속성값이 2인 경우에는 fatal 종료한다.

<a id="a1df217a5b6ac36a"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="977a475942a8369b"></a>
### 기본 정보

<a id="69ed62fa4b5f6f57"></a>
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

<a id="363c35b4da6db983"></a>
### 설명

Cluster system에서 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 이상으로 설정되었을 경우에 사용된다. Locator에게 보낸 질의에 응답이 없을 경우, 질의를 다시 시도하는 횟수를 설정한다.

<a id="feb81babc3b16c95"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="4e7c85ac4c73f0f8"></a>
### 기본 정보

<a id="79fc3456d5ca04c5"></a>
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

<a id="5e1bce2bc6b52ecb"></a>
### 설명

Commit cserver가 commit protocol 메시지를 읽기 위해 deque 할 때 busy waiting의 기준 시간 간격을 설정한다. 만약 1000000 (1초)로 설정할 경우, 이전 deque에 성공한 이후 다시 deque를 시도할 때까지 1 초를 경과하지 않았다면 deque에서의 대기시간 (timeout)을 0으로 설정하여 busy waiting 한다.

<a id="8922a1a3170bb345"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="d069313789515fa5"></a>
### 기본 정보

<a id="86e23288b2166368"></a>
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

<a id="6da2849ecef08f51"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화해야 하는데 이 때 각 control file이 저장될 디렉토리와 파일 이름을 설정한다.

<a id="c6a63242ec96a7e4"></a>
## CONTROL_FILE_COUNT

<a id="b6884d28cc423c43"></a>
### 기본 정보

<a id="96de4b557efafb64"></a>
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

<a id="a4866d1c87dbf48e"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화한다. CONTROL_FILE_COUNT는 control file의 다중화 개수를 설정하며 최소 두 개에서 최대 여덟 개까지 다중화할 수 있다.

<a id="cc8b36e95e55be09"></a>
## CONTROL_FILE_TEMP_NAME

<a id="ebe655f13618e006"></a>
### 기본 정보

<a id="0d99cb88f6a7d4e3"></a>
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

<a id="62b72ae7d86ac674"></a>
### 설명

Database를 운용하는 중에 control file은 수시로 변경되고 필요할 경우 임시로 복사본을 만들 수도 있다. CONTROL_FILE_TEMP_NAME은 control file이 임시로 저장되는 디렉토리와 파일 이름을 설정한다.

<a id="bdd3aebe5d6ffb80"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="5afb4066ab914471"></a>
### 기본 정보

<a id="ab308a02bbed2c3e"></a>
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

<a id="2503481f18b2efe2"></a>
### 설명

조정자 (coordinator)에 적용되는 commit write mode 이다. 만약 TRANSACTION_COMMIT_WRITE_MODE가 "no wait"이고 해당 프로퍼티가 "wait" 인 경우라면 조정자 노드는 "wait"으로 동작하고 그 외 노드들은 "no wait"으로 동작한다.

<a id="36844f309ae95eb4"></a>
## CSERVERS

<a id="cc935e44b5bc884b"></a>
### 기본 정보

<a id="916c41029f6729b6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | CSERVERS |
| 요약 | number of lockable cserver processes |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="28bd2f9835405d82"></a>
### 설명

Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수는 [LOCKLESS_CSERVERS](#7c7297d4a9299dbb)로 설정한다.

<a id="be7865a6b5c96a46"></a>
## DA_CLIENT_NUMA_NODE

<a id="728f2906f40d9b27"></a>
### 기본 정보

<a id="4f1305a0affcbf59"></a>
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

<a id="4af39c784006158c"></a>
### 설명

Direct Access (D/A) 세션이 바인드 될 NUMA 노드 ID를 설정한다. DA_CLIENT_NUMA_NODE는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="a64b61f774427c94"></a>
## DATA_STORE_MODE

<a id="60b4dc5203a32213"></a>
### 기본 정보

<a id="42cc4a7c4572ad1e"></a>
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

<a id="5f888a4c11931556"></a>
### 설명

Database의 저장 방식을 설정한다.

- 1: CDS 모드는 다중 사용자에 대한 동시성은 지원하지만 영속성은 보장하지 않는다. 즉, data 삽입/ 삭제/ 갱신을 비롯하여 database를 변경하는 모든 연산에 대한 로그를 기록하지 않기 때문에 장애가 발생할 경우 복구할 수도 없다.
- 2: TDS 모드는 다중 사용자에 대한 동시성 및 로그를 이용한 영속성을 보장한다.

<a id="d1af6a1cff0e065b"></a>
## DATABASE_ACCESS_MODE

<a id="80d389e653860cbb"></a>
### 기본 정보

<a id="34fd58363901947a"></a>
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

<a id="c796c2f12906e344"></a>
### 설명

Database를 시작할 때 접근 모드를 설정한다.

- 0: Database 조회만 할 수 있고 삽입/ 갱신/ 삭제는 불가능하다.
- 1: Database를 조회/ 삽입/ 삭제/ 갱신할 수 있다.

<a id="7db22d96548e91dd"></a>
## DATABASE_INSTANCE_NAME

<a id="9e821534812a6a24"></a>
### 기본 정보

<a id="ab76170d97c31c70"></a>
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

<a id="39d704c9ff805139"></a>
### 설명

데이터베이스의 instance 이름이다.

<a id="5722e58565e1b336"></a>
## DDL_AUTOCOMMIT

<a id="ac282d88713fb0e8"></a>
### 기본 정보

<a id="d41a07639a85d346"></a>
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

<a id="f19e0370067acdb6"></a>
### 설명

Autocommit이 적용되지 않는 DDL에 대한 autocommit 여부를 설정한다. 예를 들어, table의 생성과 변경에는 autocommit이 적용되지 않기 때문에 DDL_AUTOCOMMIT이 '0'인 경우 rollback을 수행하여 table 생성과 변경을 철회할 수 있다. 이에 반해 DDL_AUTOCOMMIT을 '1'로 설정하면 autocommit이 적용되지 않는 DDL들이 즉시 commit 된다.

<a id="fb8cdc2baeace047"></a>
## DDL_LOCK_TIMEOUT

<a id="ccdd76dfe592cdb7"></a>
### 기본 정보

<a id="1e146ea2aa04ed4b"></a>
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

<a id="a01c67b8a6c208b6"></a>
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

<a id="23666d50c68bd487"></a>
## DEADLOCK_PRIORITY

<a id="ae9ed8b872c594ae"></a>
### 기본 정보

<a id="11a0a03045c9b01c"></a>
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

<a id="932539e07e8e1314"></a>
### 설명

다수의 트랜잭션을 동시에 수행하다가 deadlock이 발생할 경우, deadlock을 유발한 트랜잭션들 중에서 weight 값이 낮은 트랜잭션을 victim으로 선택하여 deadlock을 해결한다. 이 속성값이 상대적으로 높은 세션에서 시작된 트랜잭션과, 이 속성값이 더 낮은 세션에서 시작된 트랜잭션 사이에서 deadlock이 발생하면, 이 속성값이 더 낮은쪽 트랜잭션이 deadlock victim으로 선택된다. Deadlock이 발생했을 때 어느 트랜잭션을 우선적으로 처리할 것인가에 따라 이 속성값을 설정해야 한다.

이 속성값을 설정한 후에 트랜잭션을 시작해야 이 값이 해당 트랜잭션의 weight으로 적용되며, 트랜잭션이 시작된 후에는 이 값을 변경하더라도 트랜잭션의 weight는 변경되지 않음에 유의해야 한다.

<a id="05d6a1b33cff8671"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="3b7b00324dfa1e47"></a>
### 기본 정보

<a id="7abde4c36d43a9ce"></a>
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

<a id="1a2a42db2cd86211"></a>
### 설명

Cluster system에서 테이블을 생성할 때 global secondary index를 생성할지 여부를 설정한다. Global secondary index를 생성하지 않은 테이블에 대한 non-deterministic 질의는 실패한다. NO로 설정한 상태에서 테이블을 생성한 후에 별도로 global secondary index를 생성할 수도 있다.

<a id="8e2feaf104d9ae59"></a>
## DEFAULT_INDEX_LOGGING

> 3.2 이후로 지원하지 않는다.

<a id="e44592b4eacd1aa2"></a>
### 기본 정보

<a id="d9494f31535f1a48"></a>
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

<a id="11f0a449b97cda89"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 LOGGING 속성을 지정하지 않은 경우, LOGGING 속성은 DEFAULT_INDEX_LOGGING 프로퍼티 값으로 설정된다. 만약 인덱스가 LOGGING 테이블스페이스에 생성되면 반드시 LOGGING 속성이 설정되어야 한다.

<a id="222c05a8df683df0"></a>
## DEFAULT_INDEX_PCTFREE

<a id="cd4c529c6fec499c"></a>
### 기본 정보

<a id="0c7407dac702fcc7"></a>
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

<a id="9869cb2ac9841461"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_INDEX_PCTFREE 프로퍼티 값으로 설정된다.

<a id="113ea426431f70ad"></a>
## DEFAULT_INITRANS

<a id="551afbd2504ea594"></a>
### 기본 정보

<a id="46221a26a3035568"></a>
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

<a id="6f69d45e35a0c0c6"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 INITRANS 구문을 지정하지 않은 경우 INITRANS는 DEFAULT_INITRANS 프로퍼티 값으로 설정된다.

<a id="9d86fd050489a563"></a>
## DEFAULT_MAXTRANS

<a id="aa385fd7b8b7c2b8"></a>
### 기본 정보

<a id="4bb904e827f8d696"></a>
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

<a id="e11606cb20eec329"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 MAXTRANS 구문을 지정하지 않은 경우 MAXTRANS는 DEFAULT_MAXTRANS 프로퍼티 값으로 설정된다.

<a id="87d3f16cefeffa66"></a>
## DEFAULT_PCTFREE

<a id="3e3b22d8f9cb11cd"></a>
### 기본 정보

<a id="5b394f7bdfa986a1"></a>
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

<a id="576f81d8d874aa86"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_PCTFREE 프로퍼티 값으로 설정된다.

<a id="f5e64301c00a709c"></a>
## DEFAULT_PCTUSED

<a id="b5db8d0f1173e719"></a>
### 기본 정보

<a id="54dc5616759433b9"></a>
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

<a id="85615419496024a0"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTUSED 구문을 지정하지 않은 경우 PCTUSED는 DEFAULT_PCTUSED 프로퍼티 값으로 설정된다.

<a id="35c5e9c55054902f"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="5c69a3d341b1ab0c"></a>
### 기본 정보

<a id="fd3b0064df920f8e"></a>
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

<a id="a0011ff756b3167e"></a>
### 설명

백업 목록을 삭제할 때 백업 파일을 삭제할지 여부를 지정한다.

<a id="24595d1d603941f2"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="d639ab4e2c67e9d6"></a>
### 기본 정보

<a id="6700836b505199a3"></a>
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

<a id="526e77923b8dfc3d"></a>
### 설명

INCREMENTAL BACKUP을 수행할 때 obsolete 된 이전 백업 목록의 삭제 여부를 설정한다.

<a id="23503fafcc828415"></a>
## DEFAULT_SHARDING

<a id="481c38fcd0384116"></a>
### 기본 정보

<a id="6c26b30c7ac06bac"></a>
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

<a id="5a73640a7202c2c8"></a>
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

<a id="5304e2d2d318a2c8"></a>
## DISABLE_DDL

<a id="412871c9b6fa9d18"></a>
### 기본 정보

<a id="cf30ad9f6f5db0cd"></a>
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

<a id="8c3326a7a2198834"></a>
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

125 rows selected.
```

<a id="6f92112033620276"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="4ceb2e3556356dbf"></a>
### 기본 정보

<a id="3e1b2b3d82364071"></a>
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

<a id="e5b5f79e87260cb2"></a>
### 설명

CDC의 give up에 영향을 미치는 supplemental log 대상 테이블에 대한 DDL 수행을 금지한다.  
관련 DDL은 [DDL 구문에 따른 give-up 발생 및 절차에 따른 허용 여부](../part-07-replication/50-cyclone.md#85f345e9fde1d288)를 참조한다.

<a id="877f3ecf2a376572"></a>
## DISABLE_SERIAL_DDL

<a id="67ee5540c90242ee"></a>
### 기본 정보

<a id="a5b9c54ffab2499f"></a>
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

<a id="a8f9bde9fe42e7fe"></a>
### 설명

Cluster 환경에서 DDL은 [Cluster의 DDL 처리](../part-03-sql-manual/12-sql-languages.md#4a767afd56c90dc3)에 설명된 것처럼 모든 cluster member 들을 순차적으로 lock을 획득한 후 수행한다.    
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

102 rows selected.
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
ALTER TABLE .. SYNCHRONIZE IDENTITY COLUMN                YES    MANUAL           
CREATE CLUSTER GROUP                                      YES    MANUAL           
DROP CLUSTER GROUP                                        YES    MANUAL           

23 rows selected.
```

<a id="cd17713f26634775"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="3a66bc71b8635d3f"></a>
### 기본 정보

<a id="6b2cb94a9e680caa"></a>
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

<a id="a93346f1f9f7ddcd"></a>
### 설명

CDC give up을 유발한 UPDATE primary key를 비활성화 한다.

<a id="eece3c2856267955"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="5b7567e1ace54709"></a>
### 기본 정보

<a id="3a595d3cd25e31d3"></a>
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

<a id="eec2847a782dcae7"></a>
### 설명

TARGETTYPE protocol을 허용하지 않는다.

<a id="dc47c95a37ba3cc7"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="21074295821a5121"></a>
### 기본 정보

<a id="77fbc31a76fdb9e5"></a>
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

<a id="66597390ff02a381"></a>
### 설명

TARGETTYPE_WITH_ALL protocol을 허용하지 않는다.

<a id="b3fa1d94af659a13"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="6f048d23a277f46d"></a>
### 기본 정보

<a id="c732389e3d6bfefb"></a>
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

<a id="145d95aea6e7eb40"></a>
### 설명

TARGETTYPE_WITH_NAME protocol을 허용하지 않는다.

<a id="f6b825d933a96153"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="42528ef10b69e1f6"></a>
### 기본 정보

<a id="66dd637cc270f412"></a>
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

<a id="efb1ad448f1dd4eb"></a>
### 설명

Shared 모드에서 사용하는 전체 communication buffer 크기로써 Shared Static Area (SSA) 내에 할당되어 사용된다.

<a id="56c88e6c67db5a48"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="f243689fb188cb62"></a>
### 기본 정보

<a id="8e35dfd2f6f7bacd"></a>
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

<a id="069d5be02ae40bcf"></a>
### 설명

Shared 모드에서 dispatcher가 관리하는 unit의 크기이다. 이 크기가 크면 메모리가 낭비되고 이 크기가 작으면 성능이 저하될 수 있다.  
Shared 모드에서 통신 packet의 최대 크기로 설정된다.

<a id="7bd7451c3c983151"></a>
## DISPATCHER_CONNECTIONS

<a id="6314894a5c9b8e61"></a>
### 기본 정보

<a id="a5b785022f2927fa"></a>
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

<a id="44b399972f5a4e74"></a>
### 설명

Shared 모드에서 하나의 dispatcher가 관리할 수 있는 최대 connection (client)의 개수이다.  
시스템에서 지원하는 최대값이 설정값보다 작으면 내부적으로 시스템 최대값으로 설정된다.

<a id="ac6e2f3fce006f95"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="a384a39f50fb86a9"></a>
### 기본 정보

<a id="ee589874a4d7bf3e"></a>
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

<a id="c3dfcd2e58dfb1c0"></a>
### 설명

Busy waiting에 대한 dispatcher dequeue 주기이다. (micro second)

<a id="998860c89600afd6"></a>
## DISPATCHER_LOAD_BALANCING

<a id="3dfb9595862d2bc9"></a>
### 기본 정보

<a id="9006bf8760210b47"></a>
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

<a id="9e3298600768a1f9"></a>
### 설명

Shared 모드에서 client에 접속할 때 dispatcher를 할당하는 알고리즘이다.

- 0: 현재 연결된 client 수가 적은 dispatcher에 할당한다.
- 1: 순차적으로 dispatcher에 할당한다.

<a id="06075af92fd94702"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="4d1d0af7697dc3c6"></a>
### 기본 정보

<a id="8a79bee23ba2c538"></a>
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

<a id="ff2e5b55190063eb"></a>
### 설명

디스패처들이 연결될 NUMA 노드를 결정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고, 1번 스트림은 NUMA 노드 1번에 연결하고, 2번 스트림은 NUMA 노드 2번에 연결한다.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="eb05edd43f208d53"></a>
## DISPATCHER_QUEUE_SIZE

<a id="d278a536d52cd831"></a>
### 기본 정보

<a id="5aff0ca25756f2aa"></a>
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

<a id="eccd82368c840aeb"></a>
### 설명

Shared 모드에서 dispatcher와 shared-server 간의 통신을 위한 queue 크기를 설정한다.

<a id="ad2870a1a0ff4237"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="cddcdcb53d401d87"></a>
### 기본 정보

<a id="cf7d9b079ee4fc7e"></a>
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

<a id="9757693fee868551"></a>
### 설명

각 response queue의 mini queue 개수이다.

<a id="ec3277b1a10cc92e"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="0abfb5e00c8c1d86"></a>
### 기본 정보

<a id="6c89c31d7503e24a"></a>
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

<a id="e4351b627a4f65e1"></a>
### 설명

각 request queue의 mini queue 개수이다.

<a id="f6f834815cee0abb"></a>
## DISPATCHERS

<a id="703dfc3f78a298f4"></a>
### 기본 정보

<a id="00344c478cd5241f"></a>
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

<a id="cea54a99c21040bd"></a>
### 설명

Shared 모드를 사용할 때 dispatcher process 개수를 설정한다.  
Open 단계에서는 alter system을 사용하여 값을 줄일 수 없다.

<a id="3b100ef98fca39c2"></a>
## EXECUTE_INST_HASH_TABLE_USING_AVAILABLE_MEMORY

<a id="c41f1ec5da438131"></a>
### 기본 정보

<a id="5dfc286a653aceb4"></a>
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

<a id="7efd349e702be7e1"></a>
### 설명

instant hash table을 사용하는 질의에서 hash bucket을 확장하기 위한 메모리가 부족한 경우 질의를 실패한 것으로 처리할지 아니면 hash bucket을 확장하지 않고 질의를 수행할지 여부를 지정한다.

<a id="8fdc709fb1357461"></a>
## FETCH_FAILOVER

<a id="013a7dbd48d2b50e"></a>
### 기본 정보

<a id="eb17c7177849b9ad"></a>
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

<a id="6e93b972beeea762"></a>
### 설명

Fetch failover를 활성화한다.

<a id="433868e649ffc321"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="2b9e266998b804fe"></a>
### 기본 정보

<a id="e02472a8ddc1b121"></a>
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

<a id="d2f723bf0092a2ea"></a>
### 설명

Global connection에서 session dependent한 정보를 포함한 질의 수행 지원 여부를 설정한다.

<a id="27013698a801bc19"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="87b3b7403f84f68f"></a>
### 기본 정보

<a id="481026deb5f38efc"></a>
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

<a id="1441ff7b759bbe38"></a>
### 설명

Global journal의 buffer 크기이다.

<a id="96a1cdee5d8daaff"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="55090158dab30754"></a>
### 기본 정보

<a id="427e02fa2b90012b"></a>
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

<a id="1cd1584cd9331178"></a>
### 설명

Global journal buffer의 최대 사이즈의 합이다.

<a id="311b6e63cbffa84e"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="17f50db1744606b5"></a>
### 기본 정보

<a id="4a12196894573a71"></a>
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

<a id="0866a955042a1e1f"></a>
### 설명

Global property를 변경할 때 동시성을 제어하기 위해 lock 하는데 이 때 해당 lock 하기 위해 대기하는 시간을 설정한다.

<a id="20515868ee56f9cb"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="dd7dde8f542b61ca"></a>
### 기본 정보

<a id="f088aee330858d6a"></a>
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

<a id="09e77759e83d6ea0"></a>
### 설명

Global transaction의 commit write mode를 변경하기 위한 프로퍼티이다. TRANSACTION_COMMIT_ WRITE_MODE는 모든 트랜잭션들에 적용되는 반면에 이 프로퍼티는 global transaction에만 적용된다. 만약 해당 프로퍼티가 2로 설정되면 TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

- 0: no wait
- 1: wait
- 2: TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

<a id="04966765ffc4efd0"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="55dad4379dacca97"></a>
### 기본 정보

<a id="460a826a8a0c9556"></a>
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

<a id="530f28ff142d2212"></a>
### 설명

Transaction이 두 개 이상의 cluster group에 걸쳐 데이터를 변경한 경우 이를 global transaction으로 처리할지 다수의 domain transaction으로 처리할지 결정하는 프로퍼티이다.

- 0: Global tranaction으로 처리
- 1: 다수의 domain transaction으로 처리

> 이 프로퍼티가 1인 경우에는 cluster group마다 독립적인 트랜잭션으로 commit하기 때문에 트랜잭션 원자성 (transaction atomicity)을 보장하지 않는다.

<a id="124e3333af6bd020"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="d88c29c03dbaf3ef"></a>
### 기본 정보

<a id="88a64c6c71e5f376"></a>
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

<a id="99617961968af021"></a>
### 설명

Global transaction log의 기본 directory 이다.

<a id="fdb14a52022fb427"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="a742c2070406eb7f"></a>
### 기본 정보

<a id="2b7a194e78abda3f"></a>
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

<a id="dac61c9d3fbaa401"></a>
### 설명

Global transaction log의 file 크기이다.

<a id="5c8b183fb6a9aebf"></a>
## GMASTER_NUMA_NODE

<a id="25e871f1ef5cfef7"></a>
### 기본 정보

<a id="d5151b4106574170"></a>
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

<a id="c1c4952f6ba9e60a"></a>
### 설명

gmaster 데몬이 사용할 NUMA node의 ID를 설정한다. GMASTER_NUMA_NODE 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="ffa7f2269986d1e3"></a>
## GMON_AUTOSTART

<a id="d39af7484c3fcf39"></a>
### 기본 정보

<a id="b6cedcc4f6bb8f99"></a>
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

<a id="8ab8699e67eda03d"></a>
### 설명

gmon 프로세스를 자동으로 시작시킬지 여부를 설정한다.

<a id="951721fc39fd2f9a"></a>
## HINT_ERROR

<a id="06a7ca3c7cd796ca"></a>
### 기본 정보

<a id="7d2a66d3be3c6fbd"></a>
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

<a id="95146732c018ed20"></a>
### 설명

Hint 구문에 대한 syntax error 및 validation error 체크 여부를 설정한다.

<a id="46eddc77caec904b"></a>
## IDLE_TIMEOUT

<a id="d9adf4b4c4d06876"></a>
### 기본 정보

<a id="ec3404026a2f9042"></a>
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

<a id="959f26896f5377af"></a>
### 설명

C/S 세션에서 최대로 대기할 수 있는 IDLE 시간을 설정하며 해당 IDLE 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT이 발생하지 않는다.

<a id="5206c1274a0f9678"></a>
## IN_DOUBT_DECISION

<a id="1b4403efcc507ac3"></a>
### 기본 정보

<a id="b04030d12a4007aa"></a>
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

<a id="679de0c876e31cbb"></a>
### 설명

분산 트랜잭션의 in-doubt 트랜잭션을 commit 할지 rollback 할지 결정한다.

- 1: Commit
- 2: Rollback

<a id="bddb4cc4b4cda17c"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="0a87be82747db627"></a>
### 기본 정보

<a id="7e3a61c7090f8a56"></a>
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

<a id="d0cc43fa683d25b3"></a>
### 설명

Array 기반의 in key range scan을 수행할 수 있는 in key range 대상 value들의 최대 개수이다.

- 다음과 같은 구문에 대해 array 기반 in key range scan을 수행하려면 IN_KEY_RANGE_ARRAY_COUNT가 3 이상이어야 한다.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

IN_KEY_RANGE_ARRAY_COUNT 값보다 in key range 대상 value들의 최대 개수가 더 많은 경우에는 instant table 기반으로 in key range scan을 수행한다.

<a id="03bb24993299dff4"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="90f5b2f3f8782fd7"></a>
### 기본 정보

<a id="fccb4510aac7da12"></a>
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

<a id="d9ab7d06f4547411"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 한 번의 디스크 IO로 읽어들일 페이지의 수를 설정한다.

<a id="e9d12a9c191c812f"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="5f0665dc19b293ce"></a>
### 기본 정보

<a id="8cff397a5eea4af0"></a>
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

<a id="9a30d31f2769315c"></a>
### 설명

인덱스를 생성할 때 병렬화 개수 (parallel factor)를 지정한다.

- 0: 시스템의 코어 개수로 지정된다.

<a id="e613f53aef76fcfb"></a>
## INDEX_LOGGING_THROTTLING

<a id="1318112db8745eed"></a>
### 기본 정보

<a id="51a2a005fe1db2ac"></a>
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

<a id="c9b07d9ec90cd151"></a>
### 설명

해당 프로퍼티는 인덱스 구축 및 재구축 시 발생하는 대량의 로그로 인해 시스템에 과부하가 걸리는 것을 방지하며 온라인 서비스에 영향을 주지 않기 위해 사용한다.

인덱스 로깅 시 로그 버퍼에 주어진 프로퍼티 값보다 많은 양의 dirty block 이 있으면 dirty block이 디스크로 flush 될 때까지 대기한다.

<a id="f243ae4477f7338f"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="8921ebf9d87464a7"></a>
### 기본 정보

<a id="0c1840235e544fca"></a>
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

<a id="c1398f8873ffb7f1"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축 하는 도중에 DML이 수행되면 journal data가 저장된다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal data들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. INDEX_REBUILD_BLOCK_READ_COUNT는 이 과정에서 journal data를 얼마만큼 읽어들여 인덱스에 반영할지를 나타낸다.

<a id="c9816356937d2d96"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="d12fc201e2d38ee0"></a>
### 기본 정보

<a id="901a621cc5b58b36"></a>
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

<a id="a07b78f224f253b8"></a>
### 설명

인덱스를 생성할 때 sub-tree를 합병하기 위한 병렬화 개수 (parallel factor)를 지정한다. 만약 해당 값이 INDEX_BUILD_PARALLEL_FACTOR 보다 큰 경우에는 INDEX_BUILD_PARALLEL_FACTOR를 사용한다.

- 0: INDEX_BUILD_PARALLEL_FACTOR를 따른다.

<a id="0dcebd7f05a5d081"></a>
## INST_ALLOCATOR_COUNT

<a id="b255d28e65a56ad9"></a>
### 기본 정보

<a id="d66edc2c260da289"></a>
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

<a id="d9cdc1ecef3c8410"></a>
### 설명

인스턴트 블록을 할당 또는 삭제하는 연산의 병렬성을 높이기 위한 프로퍼티이다.

<a id="ffcbb52c42b37a79"></a>
## INST_HASH_TABLE_BUCKET_MAX_COUNT

<a id="7ebcc78597ed0788"></a>
### 기본 정보

<a id="0ade9f923f41a81e"></a>
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

<a id="cc09e799697d09bf"></a>
### 설명

Hash instant table의 예상 bucket count의 최대값을 설정한다.

<a id="3927f6bda8b460db"></a>
## INST_TABLE_BLOCK_SIZE

<a id="07f6a145363ab6e0"></a>
### 기본 정보

<a id="9b8522d006819414"></a>
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

<a id="14292c048ef92a53"></a>
### 설명

인스턴트 블록의 크기를 결정한다. 만약 인스턴트 레코드의 고정영역 크기가 인스턴트 블록의 크기를 초과하는 경우 다음과 같은 에러가 발생한다.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="dc51e6fe9115863a"></a>
## IPC_CHANNEL_COUNT

<a id="0d4846077d4e2015"></a>
### 기본 정보

<a id="ac04de1e206db8f6"></a>
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

<a id="9f146641b5fcae68"></a>
### 설명

IPC 통신을 위한 채널 개수를 지정한다.

<a id="b04c43b34b278b63"></a>
## JOURNAL_TEMP_DIR

<a id="ea0cd8047d98dac5"></a>
### 기본 정보

<a id="e3bd1fda21113f76"></a>
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

<a id="4a0451e12e0f788f"></a>
### 설명

Journaling의 임시 디렉토리이다.

<a id="f8050650ad2e683f"></a>
## KEEPALIVE_IDLE_TIME

<a id="33cd4b0961ac31cb"></a>
### 기본 정보

<a id="6f19917faa4ba595"></a>
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

<a id="8b6b65ec65060a1a"></a>
### 설명

Keep alive packet을 송신하기 전에 client와 server 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 server 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="719c6f25e7ea0a09"></a>
## LOCAL_CLUSTER_MEMBER

<a id="d48188496d6be7cf"></a>
### 기본 정보

<a id="fb64eda63fb1ae75"></a>
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

<a id="b283b362d5a58000"></a>
### 설명

Local cluster member의 이름이다.

<a id="001bb0dc95cf5c17"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="8154078f0ec0a7e3"></a>
### 기본 정보

<a id="9f08639adad5e4bc"></a>
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

<a id="20bb814182cc7fc2"></a>
### 설명

Local cluster member의 host 이름이다.

<a id="ead42f91272467b6"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="0d965e909f976be2"></a>
### 기본 정보

<a id="e096a8dd2a1372fa"></a>
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

<a id="1b91baec47be65fc"></a>
### 설명

Local cluster member의 listen port 이다.

<a id="595c5285e4fd67fe"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="3e9cb54405a43322"></a>
### 기본 정보

<a id="5de63f14d0eb3011"></a>
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

<a id="21f57512f9597f01"></a>
### 설명

Local journal buffer의 크기이다.

<a id="d885d556c648dd3c"></a>
## LOCATION_FILE

<a id="a3457b6d8b2ed35d"></a>
### 기본 정보

<a id="3f855d9d461faa79"></a>
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

<a id="9074463e4ddfdf52"></a>
### 설명

Location file의 이름이다.

<a id="8d44bdd2f47e6621"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="99b6d024a9da144f"></a>
### 기본 정보

<a id="ba7f30f3b577cbad"></a>
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

<a id="f025dd6b65e652fb"></a>
### 설명

Cluster system이 split-brain 상황에 대한 해결 방안을 locator에게 질의한 후에 응답을 기다리는 시간 (초)을 설정한다. CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY를 1 이상으로 설정했을 때만 사용할 수 있는 프로퍼티이다.

<a id="620b921ab54635e6"></a>
## LOCK_HASH_TABLE_SIZE

<a id="a88f986f1df64d54"></a>
### 기본 정보

<a id="d7fdc52e92efa4ba"></a>
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

<a id="72db5c6764eb4150"></a>
### 설명

잠금 관리자 (lock manager)가 관리하는 hash table의 최대 크기를 설정한다.

<a id="7c7297d4a9299dbb"></a>
## LOCKLESS_CSERVERS

<a id="f9aad7e489fc755f"></a>
### 기본 정보

<a id="0cc0182ab7d164ff"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCKLESS_CSERVERS |
| 요약 | number of lockless cserver processes |
| Data type | BIGINT |
| 적용단계 | MOUNT 이하 |
| 변경가능 여부 | TRUE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | IMMEDIATE |
| MIN | 1 |
| MAX | 2048 |
| 기본값 | 5 |

<a id="635de51dd757eb88"></a>
### 설명

Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수는 [CSERVERS](#36844f309ae95eb4)로 설정한다.

<a id="b49f40689ed87470"></a>
## LOG_BLOCK_SIZE

<a id="8931b0b656c96d67"></a>
### 기본 정보

<a id="b1f147d4a5c29596"></a>
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

<a id="0f1c752a04576e31"></a>
### 설명

LOG_BLOCK_SIZE는 log buffer가 disk의 log file로 flush 되는 최소 크기이고 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="0388200617dbdb36"></a>
## LOG_BUFFER_SIZE

<a id="f86cbbada18f14f7"></a>
### 기본 정보

<a id="5de189693630ca93"></a>
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

<a id="d43f3ba3640201fd"></a>
### 설명

Database에서 DML 및 DDL 연산을 수행하여 생성한 redo log들은 공유 메모리 공간인 log buffer에 저장되고, LOG_BUFFER_SIZE를 참조하여 log buffer의 메모리 크기를 설정한다.

<a id="4cf2308aa9e634a7"></a>
## LOG_DIR

<a id="e98c0f5accf49908"></a>
### 기본 정보

<a id="caac6cc7ac37a54d"></a>
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

<a id="ee9b15ef73b193bd"></a>
### 설명

Log buffer에 기록된 log는 database의 영속성을 보장하기 위해 비휘발성 저장 장치에 존재하는 log file로 flush 되고, LOG_DIR은 log file의 경로를 설정한다.

<a id="23e5eaa33c2af146"></a>
## LOG_FILE_SIZE

<a id="60869b4535970d19"></a>
### 기본 정보

<a id="75dfd43407efa685"></a>
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

<a id="af5ba61167d339f9"></a>
### 설명

Database에서 사용되는 log file의 크기를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 log file size를 변경할 수 없다.

<a id="86e1cbc577827156"></a>
## LOG_GROUP_COUNT

<a id="c6dc1a6f5a083bc4"></a>
### 기본 정보

<a id="ce8ee38e09989a06"></a>
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

<a id="a497475c98e70fed"></a>
### 설명

Database에서 사용되는 log group의 개수를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 영향을 미치지 않는다. Database를 생성한 후에 log group을 추가하거나 제거하는 기능은 별도의 구문으로 지원한다.

<a id="547b03eb8dd4f480"></a>
## LOG_MIRROR_MODE

<a id="4e61b541f18db6d6"></a>
### 기본 정보

<a id="0908a937b0e689c2"></a>
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

<a id="39513bb1b1b8790c"></a>
### 설명

데이터베이스를 시작할 때 redo log 복제 tool인 LogMirror를 운영할 때 필요한 shared memory를 구성하기 위한 프로퍼티이다.   
LogMirror를 수행하려면 반드시 enable 되어야 한다.  
Shared memory의 크기는 LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE 프로퍼티로 변경할 수 있다.

<a id="e86c10711d54c346"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="d15d19a3710545fc"></a>
### 기본 정보

<a id="6523090117fc43bd"></a>
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

<a id="d605907298653c89"></a>
### 설명

Redo log 복제 tool인 LogMirror에 사용될 shared memory의 크기를 설정하는 프로퍼티이다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="cdcabd3780917e28"></a>
## LOG_MIRROR_TIMEOUT

<a id="92ecc97f99eca246"></a>
### 기본 정보

<a id="ecd3b9ec9b983a4f"></a>
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

<a id="918172410d7b3525"></a>
### 설명

LogMirror의 응답을 기다리는 시간이다.   
만약 0일 경우 무한정 대기하며 그렇지 않을 경우 설정한 값만큼 대기하다가 TIMEOUT이 발생하고 LogMirror service를 중단한다. 이 후 서버는 정상적으로 운영된다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="82b9c1169d1f6986"></a>
## LOG_SYNC_INTERVAL

<a id="fe440ace4a7577b4"></a>
### 기본 정보

<a id="ed096b38e2dca695"></a>
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

<a id="84e0ef076524dcc8"></a>
### 설명

GOLDILOCKS의 log flusher는 log buffer의 내용을 disk log file로 flush하는 system thread이다. Log flusher가 유휴상태에서 깨어나면 flush 해야 할 log가 있는지 확인하여 있을 경우 flush를 수행한다. 이 때 LOG_SYNC_INTERVAL에 설정된 시간 내에 flush를 하지 않았다면 현재 log buffer의 마지막 block까지 flush를 수행하여 log buffer와 log file을 동기화한다.

<a id="0e078fee5b18a093"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="10b6b45b5fc90bb6"></a>
### 기본 정보

<a id="60eff6885a9a6fcc"></a>
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

<a id="9d9bc6cba5f91473"></a>
### 설명

Log를 동기화하는 millisecond 단위의 주기이다.

<a id="e03338fb7d3c6afd"></a>
## MAX_GROUP_COUNT

<a id="7951793c9cbf6e59"></a>
### 기본 정보

<a id="bde8229af78a19e2"></a>
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

<a id="6fd91a57cf033c8e"></a>
### 설명

클러스터 시스템 내 최대 그룹 개수이다.

<a id="be367892340be0d3"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="d5bb3abd47c28ce7"></a>
### 기본 정보

<a id="5f4262bff29be7ba"></a>
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

<a id="3aeb2019f25f6277"></a>
### 설명

Cluster system에서 journaling이 발생할 경우 내부적으로 journaling data를 저장할 global journaling file 의 최대 크기 (quota)를 설정한다.

<a id="f666b22ac9337662"></a>
## MAX_NODE_COUNT

<a id="bb09e21ea099abd2"></a>
### 기본 정보

<a id="e0eca2ff67e11c56"></a>
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

<a id="881f5c130cc4baf9"></a>
### 설명

클러스터 시스템에 조인 가능한 노드 (instance)의 최대 개수이다.

<a id="ac5c202f1a6fe4e7"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="132723fc4a548aaa"></a>
### 기본 정보

<a id="8f68a89a13cfd9ea"></a>
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

<a id="3b07cd58b9786d0a"></a>
### 설명

동시에 수행될 수 있는 statement 개수를 설정한다.

<a id="dd076383d1e9db22"></a>
## MAXIMUM_FILE_CACHE_SIZE

<a id="4b7d713d2b2fb8a1"></a>
### 기본 정보

<a id="1a7a08db807c91df"></a>
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

<a id="7618d40e556e1cb2"></a>
### 설명

세션에서 사용 중인 파일 캐쉬의 최대 개수를 설정한다.

<a id="ec997a314b9b3c23"></a>
## MAXIMUM_FLANGE_COUNT

<a id="fb3ff7ddce7ae71e"></a>
### 기본 정보

<a id="2405759922dd61f6"></a>
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

<a id="baaa1b3bfeb1e994"></a>
### 설명

Plan clock에서 확장될 수 있는 flange의 최대 개수이다.

<a id="01e975f1c939c3b7"></a>
## MAXIMUM_FLUSH_BUFFER_PAGE_COUNT

<a id="7c1ca448400bec60"></a>
### 기본 정보

<a id="5a49855c1d83c58b"></a>
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

<a id="dc0c2b55f061ab59"></a>
### 설명

디스크 쓰기 연산 한 번으로 기록할 수 있는 최대 페이지 수를 설정한다. 디스크 테이블스페이스의 페이지가 버퍼에서 변경이 된 경우 IO thread가 이를 디스크에 기록한다. 디스크 쓰기 연산을 한 번 수행할 때 인접한 페이지들을 함께 기록하면 디스크 기록 횟수를 줄여 시스템 자원의 효율성을 높일 수 있다.

<a id="43e20b5505f82e0a"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="a3c0e2e67401d977"></a>
### 기본 정보

<a id="7b2a874c533cd88c"></a>
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

<a id="9c12e8406145832e"></a>
### 설명

Log buffer의 내용을 disk의 log file에 flush 할 때 한 번의 write 연산으로 flush 할 log block의 최대 개수를 설정한다.

<a id="b7b2bd52b305328a"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="313cfdb307b481ce"></a>
### 기본 정보

<a id="8ee16d361b444105"></a>
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

<a id="a8b1d4c1a7cb24d8"></a>
### 설명

GOLDILOCKS의 datafile은 checkpoint와 특정 DDL문에 의해 disk에 flush 된다. Datafile을 flush 하기 위해 한 번의 write 연산으로 flush 할 data page의 최대 개수를 설정한다.

<a id="e81f8f584c850a93"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="b18fc489996e907c"></a>
### 기본 정보

<a id="7659093d845c66da"></a>
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

<a id="d1070186256d62a7"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하면 DML 수행과 병행하여 처리할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal log들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. Journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="79b56e76825fd6bd"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="1f289f8f49b144a9"></a>
### 기본 정보

<a id="96f13fe40aba082d"></a>
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

<a id="a0dd6ef00cebb52d"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스를 DML과 병행하여 수행할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 테이블 리밸런스는 테이블을 동기화하는 동안 발생한 journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="dd321d58a237d8c9"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="06699d5b18674d5c"></a>
### 기본 정보

<a id="d42e45bb1225c8fc"></a>
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

<a id="844675d412527c02"></a>
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

<a id="f7501c03d2e338e0"></a>
## MAXIMUM_PACKAGE_INSTANCE_COUNT

<a id="88056792b7b4d4ff"></a>
### 기본 정보

<a id="3dc41aaf2ab77d5c"></a>
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

<a id="7876bf3213010d91"></a>
### 설명

하나의 session 내에서 사용할 수 있는 package instance의 최대 개수이다.  
Package instance는 해당 session에서 stateful package를 사용할 때 생성된다.

<a id="9954b8fd30b20b41"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="3ae94de837270ec6"></a>
### 기본 정보

<a id="16e561fd2988a534"></a>
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

<a id="ade481832475109b"></a>
### 설명

Shared mode로 접속한 하나의 session에서 사용 가능한 최대 buffer size를 설정한다.  
자세한 내용은 [DISPATCHER_CM_BUFFER_SIZE](#f6b825d933a96153)를 참조한다.

<a id="e04f0fbcb56a34bb"></a>
## MEASURE_CLUSTER_LATENCY

<a id="701cd92785d99133"></a>
### 기본 정보

<a id="21aa27f1598c00cd"></a>
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

<a id="576ca788d70fd059"></a>
### 설명

Measure cluster의 latency 이다.

<a id="e677e32f0a6e8115"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="0279c758f1c0b058"></a>
### 기본 정보

<a id="e2b06be9f1d73c1d"></a>
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

<a id="8a17db8cb5f78201"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_MERGE_RUN_COUNT는 한 번에 병합할 정렬된 block들의 개수를 설정한다.

<a id="ef68ccd75bf75d75"></a>
## MEMORY_SORT_RUN_SIZE

<a id="1fcac2ec2286cfa3"></a>
### 기본 정보

<a id="5d6cf8c28f7024ad"></a>
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

<a id="4f393d920774f719"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_SORT_RUN_SIZE는 정렬할 block 한 개의 크기를 설정한다.

<a id="6ae84702cb5ce557"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="435478a0ffe1b7ae"></a>
### 기본 정보

<a id="59a4664b9d702bb2"></a>
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

<a id="d2ed98d0bef38cb8"></a>
### 설명

샘플링을 이용해서 [ANALYZE TABLE](../part-03-sql-manual/18-sql-references-a-b.md#327c57ea5d5cc931)을 수행할 때의 최소 샘플링 row 건수이다.

<a id="cd3077cebad3b7fc"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="f09ab1a2470831bc"></a>
### 기본 정보

<a id="05a40a94ed309d0a"></a>
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

<a id="096b6bfc959d949c"></a>
### 설명

DML은 이전 image를 저장하기 위해 undo page를 사용한다. DML당 undo segment를 하나씩 사용하여 undo page를 소모하는데, 만약 할당받은 undo segment의 page를 모두 소진하였을 경우 다른 undo segment의 page를 가져와서 사용할 수 있다. MINIMUM_UNDO_PAGE_COUNT는 undo page가 부족할 때 page를 가져올 undo segment를 찾기 위한 최소 undo page 수이다. 즉, undo page가 부족할 때, MINIMUM_UNDO_PAGE_COUNT 보다 많은 page를 보유한 undo segment에서만 page를 가져올 수 있다.

<a id="78679f0edce2146a"></a>
## NET_BUFFER_SIZE

<a id="885380026854ec34"></a>
### 기본 정보

<a id="5cfa343e7853f678"></a>
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

<a id="be7657790bf005db"></a>
### 설명

TCP 통신 buffer size를 설정한다.  
Dedicated 모드에서는 통신 packet의 최대 크기로 설정된다.  
Shared 모드에서는 [DISPATCHER_CM_UNIT_SIZE](#56c88e6c67db5a48)가 사용된다.

<a id="3743e60c126ee1e1"></a>
## NLS_DATE_FORMAT

<a id="4b79bbb12f7c43a5"></a>
### 기본 정보

<a id="d5c3af2203dab1d8"></a>
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

<a id="74d389150974d347"></a>
### 설명

NLS_DATE_FORMAT은 TO_CHAR와 TO_DATE 함수의 default date format을 지정한다.

<a id="94b62e1d8e627da5"></a>
## NLS_TIME_FORMAT

<a id="17c6114d9e14c91f"></a>
### 기본 정보

<a id="9411fefe96871d53"></a>
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

<a id="1eb303d60db89991"></a>
### 설명

NLS_TIME_FORMAT은 TO_CHAR와 TO_TIME 함수의 default time format을 지정한다.

<a id="4446f2d6ee237e50"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="96d1b8a2da84dae7"></a>
### 기본 정보

<a id="7e9b04e3d444b5d8"></a>
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

<a id="5ecf3c640cbe253a"></a>
### 설명

NLS_TIME_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIME_WITH_TIME_ZONE 함수의 default time with time zone format을 지정한다.

<a id="02892516d7d97f96"></a>
## NLS_TIMESTAMP_FORMAT

<a id="a2d584287dbdeeb1"></a>
### 기본 정보

<a id="008e3909566ad040"></a>
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

<a id="c286d81d379b1d81"></a>
### 설명

NLS_TIMESTAMP_FORMAT은 TO_CHAR와 TO_TIMESTAMP 함수의 default timestamp format을 지정한다.

<a id="0cecf8f45a110468"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="13edd6609f6c993c"></a>
### 기본 정보

<a id="046ccba73c725e3c"></a>
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

<a id="8500f4c18aae82b0"></a>
### 설명

NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIMESTAMP_WITH_TIME_ZONE 함수의 default timestamp with time zone format을 지정한다.

<a id="93a77840a17b3ea0"></a>
## NUMA

<a id="94994dfae2a69319"></a>
### 기본 정보

<a id="9764f809aaf45fce"></a>
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

<a id="a4c6997d80767808"></a>
### 설명

NUMA를 활성화/ 비활성화한다.

> AIX에서 NUMA 속성을 사용하기 위해서는 사용자 계정을 변경해야 한다. 다음 명령을 루트 사용자로 실행한다.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> 여기에서 &lt;username&gt;은 루트가 아닌 AIX 사용자 계정이다.  
> 변경 사항을 적용하려면 로그아웃한 후에 다시 로그인해야 한다.

<a id="b6eeb301d31bc1d5"></a>
## NUMA_MAP

<a id="e5cfac9d2c77ba0a"></a>
### 기본 정보

<a id="4aff1704bc1f5c92"></a>
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

<a id="4fd8700e5dd7676d"></a>
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

<a id="6cdeee1d926f6c14"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="722df07bc1ad7242"></a>
### 기본 정보

<a id="85b41624c46225d1"></a>
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

<a id="3ba1c4168bb27e14"></a>
### 설명

시스템의 백그라운드 프로세스 (gmaster)는 노드 장애에 따른 failover를 완료한 후에 장애 멤버를 자동으로 오프라인 시킨다.

만약 NO로 설정되어서 장애 멤버가 오프라인되지 않았다면 장애 멤버를 시스템에 다시 조인시키기 전에 다음 구문을 실행해야 한다.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="e4fb8ed31ba216c7"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="2d429a02b638a450"></a>
### 기본 정보

<a id="d7b4981595f3dc4a"></a>
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

<a id="a634aa8adc0bcdca"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하는 동안 수행된 DML은 journal log를 남긴다. 인덱스 재구축이 마무리되는 단계에서 여러 차례에 걸쳐 journal이 인덱스에 반영되는데 이 때 journal log를 반영하는 최대 차수는 [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#e81f8f584c850a93)가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="86c86c7a549e7780"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="333f2b1c78b58709"></a>
### 기본 정보

<a id="4f6c986e67af4112"></a>
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

<a id="5997d18ce6928b29"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스는 수행 중에 발생한 DML이 남긴 journal log를 여러 번에 걸쳐 반영한다. Journal log를 반영하는 최대 차수는 MAXIMUM_JOURNAL_REPLAY_COUNT가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="961ba365d59ed4f7"></a>
## OS_GROUP_ACCESS

<a id="88f1b136ed94dc67"></a>
### 기본 정보

<a id="0c1a276b000247d1"></a>
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

<a id="1255d0f97cbb1019"></a>
### 설명

동일한 group의 다른 user가 D/A로 접속하려면 이 설정을 YES로 변경해야 한다. 또한 시스템 상의 umask도 0002로 변경해야 한다.

<a id="d76b12bb19fc0fab"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="5d3e4a14a23f8dd1"></a>
### 기본 정보

<a id="aa1b8fc54b7294ed"></a>
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

<a id="e895f0f0ed8aa3f6"></a>
### 설명

클라이언트로 보낼 통신 데이터의 크기가 PACKET_COMPRESSION_THRESHOLD 보다 클 경우, 통신 데이터를 압축한다.

<a id="f280f24d30552558"></a>
## PAGE_CHECKSUM_TYPE

<a id="6cf1485fba00d761"></a>
### 기본 정보

<a id="385e70b01127fb06"></a>
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

<a id="d8dbc4be873e59a6"></a>
### 설명

Datafile의 각 page들에 대한 물리적 정합성을 보장하기 위해 checksum을 사용한다. GOLDILOCKS는 LSN, CRC 방식의 page checksum을 지원한다.

- 0: LSN
- 1: CRC

<a id="5da76f1104e4a963"></a>
## PARALLEL_IO_FACTOR

<a id="1ed82662ccde65a4"></a>
### 기본 정보

<a id="62873efc9d74a2c2"></a>
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

<a id="17b41059d73b164f"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일을 병렬 로딩하고 체크포인트 할 때 데이터 파일을 병렬 기록하기 위한 thread 개수를 설정한다.

<a id="db6d9ab3af867552"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="e6265ff0e745f43a"></a>
### 기본 정보

<a id="eef520b0d8561e4b"></a>
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

<a id="3c08497203fc72f6"></a>
### 설명

Datafile의 병렬 IO를 위한 group directory를 설정한다. 즉, PARALLEL_IO_FACTOR 수만큼 group을 설정하여 각 group에 속한 datafile 별로 병렬 IO를 수행한다.

<a id="72922128fab77823"></a>
## PARALLEL_LOAD_FACTOR

<a id="d0fca1bf3586abcb"></a>
### 기본 정보

<a id="ae1f2f1aa5b0a362"></a>
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

<a id="28b24d4e013fb28d"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일의 메모리를 적재한 후에 병렬 작업을 위한 thread 개수를 설정한다.

<a id="c8ec5fa1e4f87157"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="20412bbe6ea02386"></a>
### 기본 정보

<a id="a9cd24615e4cc01c"></a>
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

<a id="841f97c560fa0597"></a>
### 설명

여러 트랜잭션이 동시에 실행될 경우 log buffer에 대한 경쟁을 줄이기 위해 pending log buffer를 사용하며, PENDING_LOG_BUFFER_COUNT는 동시에 사용할 수 있는 pending log buffer 개수를 설정한다.

<a id="0e8d6709940861e6"></a>
## PLAN_CACHE

<a id="f5b6599d14032787"></a>
### 기본 정보

<a id="eef103413c3afc41"></a>
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

<a id="6ead6371fb265a3f"></a>
### 설명

Plan cache 사용 여부를 설정한다.

<a id="1d6342b2149d5b23"></a>
## PLAN_CACHE_SIZE

<a id="ba32bebee70c1b31"></a>
### 기본 정보

<a id="2696fae82a6b1c12"></a>
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

<a id="ffbdecb79e5536ab"></a>
### 설명

Plan cache에 사용할 메모리 크기를 설정한다.

<a id="ded1a20f3222603b"></a>
## PLAN_HISTORY

<a id="a0407eea8c8170db"></a>
### 기본 정보

<a id="d95ff8dbdfdfe48d"></a>
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

<a id="663b8b81b1118e71"></a>
### 설명

Plan history 사용 여부를 설정한다.

<a id="1348bca7461d1635"></a>
## PLAN_HISTORY_SIZE

<a id="d2e5b54216e2308a"></a>
### 기본 정보

<a id="2a0e4f5375394b9b"></a>
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

<a id="9fb22dd342846e5d"></a>
### 설명

Plan history에 저장할 plan 개수를 설정한다.

<a id="ce6a022d9118a86b"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="639e87241807b51b"></a>
### 기본 정보

<a id="8ce8a59c77089724"></a>
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

<a id="bd23da1131996295"></a>
### 설명

세션이 사용할 heap 메모리의 최초 크기를 설정한다. 세션에서 사용되지 않는 메모리가 생기더라도 이 메모리들이 운영체제로 반환되지는 않는다.

<a id="ac1459eb387ba3d3"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="7b5f08167cc3ee3a"></a>
### 기본 정보

<a id="2f77b87bbcd5d8c1"></a>
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

<a id="95aef3410a5d6c66"></a>
### 설명

세션에서 heap 메모리를 추가적으로 할당할 때, 확장될 메모리 크기를 설정한다.

<a id="478d358f51c73545"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="3d6b625e486d16a7"></a>
### 기본 정보

<a id="bfc31219fe92ba71"></a>
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

<a id="6d618138f584f2bc"></a>
### 설명

세션에서 사용하지 않는 heap 메모리가 생기더라도 이 크기만큼의 메모리를 유지하며 시스템에 반환하지 않고 세션 내에서 재사용한다.

PRIVATE_STATIC_AREA_INIT_SIZE보다 작게 설정하더라도 그 크기보다 작아지지 않는다.

<a id="2e968749fa90fd86"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="9e2c6cf18e9e2fab"></a>
### 기본 정보

<a id="fb328567567ab4cf"></a>
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

<a id="9c372112eefb7950"></a>
### 설명

세션에서 할당할 수 있는 최대 heap 메모리 크기를 지정한다.

<a id="0cf328c455d9a018"></a>
## PROCESS_MAX_COUNT

<a id="669e17dde2349221"></a>
### 기본 정보

<a id="d3b51d693c2474ce"></a>
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

<a id="11d1d9f864771628"></a>
### 설명

시스템에서 사용할 수 있는 최대 프로세스 (thread) 개수를 지정한다.

시스템 프로세스 생성  
• D/A 또는 C/S dedicated 모드로 접속할 때마다 프로세스가 생성된다.  
• C/S shared 모드는 기본적인 balancer, dispatcher, shared-server가 프로세스이고 client에서 접속할   
&nbsp;&nbsp;때는 프로세스가 생성되지 않는다.

<a id="13ef7d14bfcff08c"></a>
## QUERY_TIMEOUT

<a id="23eccbf26a8fcfd7"></a>
### 기본 정보

<a id="7db9ab1578aba120"></a>
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

<a id="cba19a13b0dc8ce0"></a>
### 설명

세션에서 받은 명령어를 처리할 수 있는 최대 시간을 지정하며 만약 해당 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT 에러가 발생하지 않는다.

<a id="d4bda0aab0189bb3"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="7c85bd9988f51998"></a>
### 기본 정보

<a id="5b7f8df264feff52"></a>
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

<a id="5546b2fcd272f41d"></a>
### 설명

미디어 복구 시 archive redo log가 존재하는 디렉토리의 개수를 설정한다.

<a id="e0ed4505abec8781"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="0de7bd70304c7165"></a>
### 기본 정보

<a id="afaf474e1b97bcbe"></a>
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

<a id="d6ce82aaf11bb5d4"></a>
### 설명

증분 백업을 이용하여 파일을 복원할 때 증분 백업이 존재하는 디렉토리의 개수를 설정한다.

<a id="02009559d8b838ad"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="6a76ad7e0f16009f"></a>
### 기본 정보

<a id="40503154cf01c893"></a>
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

<a id="9a225528728c85fe"></a>
### 설명

Rebalance 하기 위해 block을 읽어들이는 횟수이다.

<a id="217e832b024921bd"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> 3.1 이후로 지원하지 않는다.

<a id="dfd386dc82c68334"></a>
### 기본 정보

<a id="864d298ba6dff17d"></a>
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

<a id="7b54eb54fdc774fc"></a>
### 설명

Page count 변경에 의해 plan이 recompile 되었는지 여부를 체크하기 위해 minimum page count를 설정한다.

<a id="7d00f2f808b976c2"></a>
## RECOMPILE_PAGE_PERCENT

> 3.1 이후로 지원하지 않는다.

<a id="50aed651ae1576cb"></a>
### 기본 정보

<a id="bc397d5ac921809b"></a>
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

<a id="bc77ab0be034aa15"></a>
### 설명

Page count가 변경되어 plan을 recompile 할 때의 page percentage를 설정한다. 이 값이 0인 경우 page count 변경에 따른 recompile을 하지 않는다.

<a id="ab1030b2c1c6389c"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="aa466f2ac2ca2f1d"></a>
### 기본 정보

<a id="5cea7449326244ae"></a>
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

<a id="7380cc831bf5bd9e"></a>
### 설명

복구를 위한 기본 log buffer 크기이다.

<a id="6a01f4fc7f8b92da"></a>
## RECYCLEBIN

<a id="cac92d3593c3ed9b"></a>
### 기본 정보

<a id="48c0cee5161bc9e2"></a>
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

<a id="5c450ce755fbf2ab"></a>
### 설명

휴지통 기능을 활성화할지 여부를 설정한다.

<a id="6face03211668970"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="510457fa19288bd5"></a>
### 기본 정보

<a id="edd8bb37d8c31c7a"></a>
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

<a id="9af7be7b808e2fcc"></a>
### 설명

생성된 REDO LOG의 크기가 REDO_LOG_COMPRESSION_THRESHOLD 값보다 클 경우, REDO LOG를 압축한다.

<a id="ce8d8034b7b9c26a"></a>
## REFINE_RELATION

<a id="4f66c8d029b02aa5"></a>
### 기본 정보

<a id="26b349eb7709ad9c"></a>
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

<a id="11eb5fbf55bad061"></a>
### 설명

이 속성을 NO로 하면 서버를 재시작할 때 REFINE RELATION 과정을 수행하지 않는다.

해당 프로퍼티는 REFINE RELATION 도중에 문제가 발생한 경우에 사용할 수 있으며 삭제되었지만 REFINE 하지 못한 RELATION (테이블이나 인덱스)들의 공간은 재사용할 수 없다. 문제를 해결한 이후 해당 프로퍼티를 YES로 설정하고 재시작하면 삭제하지 못했던 RELATION들에 대해 REFINE을 시도한다.

<a id="7135d41c76eec404"></a>
## SESSION_FATAL_BEHAVIOR

<a id="2a3e770dfc22949f"></a>
### 기본 정보

<a id="5f11009f83af553f"></a>
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

<a id="957dea57c5a858a3"></a>
### 설명

Session fatal이 발생할 때 fatal을 유발한 thread만 종료시킬지 아니면 프로세스 자체를 종료시킬지 결정한다.

- 0: Fatal을 유발한 thread만 종료한다.
- 1: 프로세스를 종료한다. 해당 프로세스 내에 다수의 세션이 동시에 수행되고 있다면 모든 세션들이 데이터베이스 사용을 끝낸 후에 프로세스를 종료한다.

<a id="3af9dd17fe038e6b"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="87711635bfdaf430"></a>
### 기본 정보

<a id="c91df260c3a12331"></a>
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

<a id="9fcb2dc079ce49d8"></a>
### 설명

세션에서 사용할 공유 메모리를 미리 할당할 크기를 설정한다.

<a id="a97b48f4d0567713"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="bd553ae71152b3dd"></a>
### 기본 정보

<a id="32fa4237c35d9730"></a>
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

<a id="f228665779389607"></a>
### 설명

세션에서 사용한 동적 공유 메모리를 해제할 때 세션에서 사용하지 않는 동적 공유 메모리를 시스템에 반납할지 여부를 판단하기 위한 경계값을 설정한다. 즉, 사용하지 않는 메모리 중 설정된 값보다 큰 크기의 메모리 청크가 있으면 시스템에 반납한다.

<a id="22f17de3709e893e"></a>
## SHARED_MEMORY_ADDRESS

<a id="a91d78b06c3cb55e"></a>
### 기본 정보

<a id="9440afae85607e0f"></a>
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

<a id="7e56cdd430ac9e14"></a>
### 설명

Shared Static Area (SSA)의 주소를 지정한다.

<a id="22cc76f6ad1ae23a"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="ea6d979e4ac868f9"></a>
### 기본 정보

<a id="a47c786bb4715b95"></a>
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

<a id="a5f0769d4295f4a2"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory key 값을 지정한다.

<a id="ef95e1ba3a5b05d6"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="e0363b0a9701ea9d"></a>
### 기본 정보

<a id="65bbb1a0b1cdda0a"></a>
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

<a id="4eceb779d834fdea"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory name을 지정한다.

<a id="bd61a081d00ad5fe"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="b884788c8148778e"></a>
### 기본 정보

<a id="8d456b600d66b8f5"></a>
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
| 기본값 | 763363328 |

<a id="605993d273daac97"></a>
### 설명

Shared Static Area (SSA)의 크기를 지정한다.

<a id="05cac9a77ae10c3c"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="832fe926c560f5df"></a>
### 기본 정보

<a id="99dc2e4e62fbea69"></a>
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

<a id="84fd221f2f8765ad"></a>
### 설명

Shared 모드의 dispatcher에서 shared-server로 요청하는 queue 개수를 설정한다. 여러 dispatcher가 사용자의 작업 요청을 shared-server에 할당할 때 사용하는 queue로써 일반적으로 load-balance를 위해 하나를 사용한다. 그러나 dispatcher와 shared-server가 많아지면 queue에 경합이 발생하여 성능이 저하될 수 있으므로 이 값을 늘려서 사용한다. 이 값이 커지면 load-balance가 비효율적으로 될 수 있고 dead-lock이 발생할 가능성이 커진다.

<a id="da6f29734c81f290"></a>
## SHARED_SERVERS

<a id="470adc92b8b379df"></a>
### 기본 정보

<a id="23aff9d77714c121"></a>
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

<a id="1e87692c2e84b3d6"></a>
### 설명

Shared 모드에서 shared-server process 개수를 설정한다.  
Open 단계에서는 alter system으로 값을 줄일 수 없다.

<a id="16469163b048f0db"></a>
## SHARED_SESSION

<a id="182f9dcd9b22de8e"></a>
### 기본 정보

<a id="53f065319c5b26b2"></a>
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

<a id="dd687c2194227e1d"></a>
### 설명

Shared 모드를 활성화할지 여부를 설정한다. 이 값을 NO로 설정하면 load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver)가 실행되지 않는다.

<a id="a0179647ae350ac0"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="e1a0508c93a606f8"></a>
### 기본 정보

<a id="67e3acb314f65af5"></a>
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

<a id="c146918ed8f924e0"></a>
### 설명

Snapshot read가 필요로 하는 statement의 최대 유지 시간을 설정한다. 설정된 시간을 초과한 snapshot statement들에는 TIMEOUT 에러가 발생한다.

<a id="ebc7165797734e33"></a>
## SQL_HISTORY_SIZE

<a id="122f8fe15e240e5c"></a>
### 기본 정보

<a id="791cfdbe3ce2c138"></a>
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

<a id="bea1dce652312ab6"></a>
### 설명

SQLs의 이력 (history) 크기이다.

<a id="eb082c6e9796db6a"></a>
## SQL_HISTORY_TYPE

<a id="5305a312c31c043b"></a>
### 기본 정보

<a id="622cf5effb46e7ed"></a>
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

<a id="2f483e19ef0aabbc"></a>
### 설명

SQLs의 이력 (history) 타입이다.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="b528c8d9dedee3ed"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="38d30ffb4ba57059"></a>
### 기본 정보

<a id="43233719c61d5cb6"></a>
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

<a id="cfd51b5c1e76084e"></a>
### 설명

Database 내의 모든 변경 내용에 대한 supplemental log를 기록한다.

<a id="e649aa01dc7ea5cd"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="6fb864bd853077ab"></a>
### 기본 정보

<a id="b9f6feb5492294ce"></a>
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

<a id="0ce5c383b9b1112b"></a>
### 설명

데이터베이스를 생성할 때 초기 DISK_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="9f9d1d3ea81b1d88"></a>
## SYSTEM_FILE_IO

<a id="c3d9cc49d9ca57c9"></a>
### 기본 정보

<a id="3e1f47335fd9970c"></a>
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

<a id="47f3657e33f8ba7d"></a>
### 설명

데이터 파일과 로그 파일을 제외한 데이터베이스 파일을 사용할 때 IO 타입을 설정한다.

<a id="a9708fdbf5d4561d"></a>
## SYSTEM_LOGGER_DIR

<a id="82c202e37504a5e8"></a>
### 기본 정보

<a id="d85dbdd31c5103e7"></a>
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

<a id="931eebbdc3f373e5"></a>
### 설명

Trace 로그 메시지가 기록되는 디스크 경로를 지정한다.

<a id="d5041c0b6ca45a15"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="771dbe21b1190d32"></a>
### 기본 정보

<a id="742b84d1abec3e31"></a>
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

<a id="b8ec61ffba35b8fe"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_AUX_TBS 테이블스페이스 크기를 결정한다.

<a id="00013513bc371202"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="e5fd32b93b9c3085"></a>
### 기본 정보

<a id="397bbb049c3db711"></a>
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

<a id="4729ab9f93429a0f"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="8dc9f809974de6a2"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="4f3b5a7d8164a66c"></a>
### 기본 정보

<a id="c032fd9e9acb38ef"></a>
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

<a id="de66796e07cc5ec5"></a>
### 설명

데이터베이스를 생성할 때 초기 DICTIONARY_TBS 테이블스페이스의 크기를 결정한다.

<a id="3180f117c82b9040"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="18c3304d8c90e8b9"></a>
### 기본 정보

<a id="b98f1665c6121eec"></a>
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

<a id="5daebb075aaeac25"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_TEMP_TBS 테이블스페이스의 크기를 결정한다.

<a id="d1a6eb648b4e5c44"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="caa60e4fc2641bcc"></a>
### 기본 정보

<a id="f01412e97c0ef387"></a>
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

<a id="b7bedcda016e61d6"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_UNDO_TBS 테이블스페이스의 크기를 결정한다.

<a id="f7c01b1c0fd09b10"></a>
## SYSTEM_TABLESPACE_DIR

<a id="bfb86c9dec2b7482"></a>
### 기본 정보

<a id="56f05806c65cce15"></a>
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

<a id="1ee4a2b0ace4a78e"></a>
### 설명

데이터베이스를 생성할 때 초기 시스템 테이블스페이스들이 저장되는 경로를 지정한다.

<a id="bebeb4eb1ccefcaf"></a>
## SYSTEM_UDS_DIR

<a id="afc725807b0e0429"></a>
### 기본 정보

<a id="8d66e34ca788d0ac"></a>
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

<a id="b7d62760cb65435f"></a>
### 설명

Unix domain socket 파일이 생성되는 directory를 설정한다.  
DB system 이외에 glsnr 등과 같은 unix domain socket에 대한 디렉토리 설정은 별도의 configuration file에서 관리된다.  
최대 설정 크기는 60 byte이다. (Unix domain socket 파일의 절대 경로 (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.)

<a id="f7b01f8e342be39a"></a>
## TCP_CLIENT_NUMA_NODE

<a id="7c7698b898dd6ca1"></a>
### 기본 정보

<a id="5b04b8c83ccee5e9"></a>
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

<a id="1584fb688994951e"></a>
### 설명

Client server 세션이 바인드 될 NUMA 노드 ID를 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="6609542d056dcee6"></a>
## TCP_NODELAY

<a id="72ee16e4ebc70dd5"></a>
### 기본 정보

<a id="b27e0db65e4f84dc"></a>
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

<a id="abb091146bce8851"></a>
### 설명

C/S 방식 (TCP socket)으로 client에 data를 전송할 때의 socket TCP_NODELAY 옵션을 설정한다.  
빠른 latency가 필요하지 않고 network 부하를 줄이고 싶은 경우에는 NO로 설정한다.

<a id="8820763c95c708c3"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="c8e1e98b718f3cf8"></a>
### 기본 정보

<a id="ca772e3566194b03"></a>
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

<a id="87e0140c6c39ef85"></a>
### 설명

Global temporary table이나 global temporary index segment가 drop 될 때 tablespace에 반납하지 않고 session에서 caching 할 segment 개수를 지정한다. Segment cache에 존재하는 segment는 향후 global temporary table이나 global temporary index에서 재사용된다.

- 0: Session에서 global temporary table이나 global temporary index의 segment cache를 사용하지 않는다.
- 1 ~ 4294967295: Session에서 global temporary table이나 global temporary index의 segment cache를 주어진 개수만큼 유지한다.

<a id="fdd3614480464ba9"></a>
## TEMP_UNDO_ENABLED

<a id="b33b677d034ef6d4"></a>
### 기본 정보

<a id="3cbe7aa16d942735"></a>
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

<a id="e51ff90685213838"></a>
### 설명

Global temporary table에 대한 undo 레코드의 로깅 위치를 지정한다.

- 0 (FALSE): 데이터베이스의 기본 undo tablespace에 undo 레코드를 기록한다.
- 1 (TRUE): 데이터베이스의 기본 temporary tablespace에 undo 레코드를 기록한다.

<a id="f855d08c3cc25333"></a>
## TIMED_STATISTICS

<a id="9699f24a68425967"></a>
### 기본 정보

<a id="dc1b9f433398d71f"></a>
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

<a id="04e89e484ad62f61"></a>
### 설명

Wait event를 측정하는지 여부이다.  
v$system_event, v$session_event, v$session_wait table에 wait event와 관련된 통계 기록을 남기고 싶은 경우에 설정한다.

- 0: 통계 기록을 남기지 않는다.
- 1: 통계 기록을 남긴다.
- 2: High precision timer를 이용하여 통계 기록을 남긴다.

<a id="64210712883ef70a"></a>
## TIMER_INTERVAL

<a id="5b78b7d8b97d982d"></a>
### 기본 정보

<a id="bdfc77bab18d4ab9"></a>
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

<a id="8efa189fceefbd0f"></a>
### 설명

타이머 thread가 시스템 시간을 설정할 수 있도록 시간 간격을 설정한다.

<a id="f49a6d4b79974d75"></a>
## TIMEZONE

<a id="e75993c495bfc9f5"></a>
### 기본 정보

<a id="b336744cb8d9c985"></a>
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

<a id="43ad978aa2f3fcf4"></a>
### 설명

Database의 time zone 값이다.  
Database가 생성될 때 적용되는 속성으로써 -14:00 ~ +14:00 범위의 값을 사용할 수 있다.

<a id="a501b161a4b2389a"></a>
## TRACE_ALTER_SYSTEM

<a id="32a003e5665d859e"></a>
### 기본 정보

<a id="18a68c3f6964978f"></a>
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

<a id="2c70899e8eb2348f"></a>
### 설명

ALTER SYSTEM 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

시스템 변경에 대한 기록을 남기려면 TRACE_ALTER_SYSTEM 프로퍼티를 ON으로 설정한다.  

TRACE_ALTER_SYSTEM 프로퍼티는 SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="1559c7de1c08221a"></a>
## TRACE_DDL

<a id="c0351f0239da61ec"></a>
### 기본 정보

<a id="3049bd375337a0f0"></a>
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

<a id="88b7c2c834933e1d"></a>
### 설명

Data Definition Language (DDL) 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

테이블 생성, 삭제, 변경 등과 같은 SQL 문을 실행했을 때 이에 대한 기록을 남기려면 TRACE_DDL 프로퍼티를 ON으로 설정한다.  

TRACE_DDL 프로퍼티는 DDL 구문 수행에만 영향을 주며, SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="6e98c3f94fbd0997"></a>
## TRACE_LOG_ID

<a id="7976e3a7c97a034c"></a>
### 기본 정보

<a id="405d99bd871aa989"></a>
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

<a id="48e0890554db068f"></a>
### 설명

질의를 수행할 때 해당 질의에 대한 실행 계획 정보와 기타 정보를 trace directory(&lt;GOLDILOCKS_DATA&gt;/trc/) 아래에 있는 trace file (opt_p[프로세스ID]_s[세션ID].trc)에 기록한다.

질의에 대한 SQL 구문과 실행 계획, 수행시간 등에 대한 기록을 남기려면 아래 표의 flag 정보를 조합하여 설정한다.

**TRACE_LOG_ID에 대한 flag 정보**

<a id="c09888d0690daa3f"></a>
| 정보 | Flag(on) | Flag(off) |
| --- | --- | --- |
| 성공한 SQL 질의 출력 여부 | 100000 | 0 |
| 실패한 SQL 질의 출력 여부 | 10000 | 0 |
| 실행 계획 출력 여부 | 1000 | 0 |
| 실행 형태 (direct/prepare) 출력 여부 | 100 | 0 |
| Bind 값 출력 여부 | 10 | 0 |
| 구간별 수행시간 출력 여부 | 1 | 0 |

만약 "성공한 SQL 질의 출력" + "실행 계획 출력" + "Bind 값 출력" 하려면 TRACE_LOG_ID 값을 101010으로 설정한다.

<a id="8e7a48875885b46c"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="90522adf7d0be457"></a>
### 기본 정보

<a id="2760936429a5a029"></a>
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

<a id="9e6310929c54addf"></a>
### 설명

Trace logfile에 기록할 log message를 구성하는데 사용되는 heap memory buffer의 크기를 설정한다.

<a id="c3ad783b286a47d8"></a>
## TRACE_LOG_TIME_DETAIL

<a id="5f182bab776a517d"></a>
### 기본 정보

<a id="03efd30ee8d44429"></a>
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

<a id="0c2ac12b3150b2d7"></a>
### 설명

Trace log를 기록할 때 시간 정확도를 높일지 여부를 설정한다.  
이 값이 OFF로 설정된 경우, 10 ms의 정확도를 가지며, ON으로 설정된 경우 1 us의 정확도를 가진다.

<a id="aa5107b527bf9f27"></a>
## TRACE_LOGGER

<a id="a15195ea5ebb1391"></a>
### 기본 정보

<a id="05bc67db8667b10e"></a>
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

<a id="4ab6becdfa7e5315"></a>
### 설명

Trace log를 기록할 대상을 설정한다.  
1이면 file에 기록하고 2이면 remote로 파일에 기록한다.  
Remote로 기록하면 gtrclogger에서 원격으로 trace log를 수집하여 파일에 기록한다.

<a id="98ddefbe78cb58ad"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="553faf667681734d"></a>
### 기본 정보

<a id="86df9a997e85fe38"></a>
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

<a id="26e5f67b44b4c57a"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 host를 설정한다.

<a id="ac554ae6a8498676"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="10531b82c7bdd044"></a>
### 기본 정보

<a id="eaaa50d371523f5f"></a>
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

<a id="05b9368c6530f942"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 port를 설정한다.

<a id="6c69a8e357c92302"></a>
## TRACE_LOGIN

<a id="1bda7b022a31f107"></a>
### 기본 정보

<a id="39c5e47b5db8ae29"></a>
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

<a id="9bc65e19937a9517"></a>
### 설명

로그인 할 때 해당 접속 정보를 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc)에 기록한다.  
로그인 할 때 이에 대한 기록을 남기려면 TRACE_LOGIN 프로퍼티를 ON으로 설정한다.

<a id="1f7170daea2629dd"></a>
## TRACE_LONG_RUN_CURSOR

<a id="550b7e25de1cf0b8"></a>
### 기본 정보

<a id="36a14eed9ab3d0ed"></a>
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

<a id="8cc2a6209fd7fec6"></a>
### 설명

Cursor의 lifetime이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#7c7e38f2fbfcc990) 프로퍼티를 사용한다.

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

<a id="c7b4c19ea5a0321d"></a>
## TRACE_LONG_RUN_SQL

<a id="151fca5b7c7442d7"></a>
### 기본 정보

<a id="d8ea9a3e3fc0d743"></a>
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

<a id="408a606d9d978ba2"></a>
### 설명

구문의 수행시간이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 높은 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#7c7e38f2fbfcc990) 프로퍼티를 사용한다.

- 수행시간이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="7c7e38f2fbfcc990"></a>
## TRACE_LONG_RUN_TIMER

<a id="74586fd42bb8ed6b"></a>
### 기본 정보

<a id="e56ed7d968e55170"></a>
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

<a id="3696ccc6f689dd2f"></a>
### 설명

다음 프로퍼티들을 이용하여 SQL 구문의 실행시간을 측정할 때 측정 정밀도를 제어한다.

- [TRACE_LONG_RUN_CURSOR](#1f7170daea2629dd)
- [TRACE_LONG_RUN_SQL](#c7b4c19ea5a0321d)

- 값의 의미
    - 0: 10 millisecond의 interval을 가지는 timer thread를 사용한다.
    - 1: gettimeofday() 함수를 이용하여 시간을 측정한다. 정밀도는 높지만 system call로 인한 부하가 있다.

<a id="05191f7c36b586c2"></a>
## TRACE_XA

<a id="8f4e0bd350c7f3f9"></a>
### 기본 정보

<a id="1febdc67a40420ee"></a>
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

<a id="cdc9c61644769db5"></a>
### 설명

XA 인터페이스를 사용할 때 추적 메세지를 출력할지 여부를 지정한다. 메세지는 'SYSTEM_LOGGER_DIR/xa.trc'에 출력된다.

<a id="e475ca1c49b28a10"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="fa08b0e5aee4f17c"></a>
### 기본 정보

<a id="8791f458613169ff"></a>
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

<a id="07c9c52e5fd70f32"></a>
### 설명

Transaction slot을 할당할 때의 최대 대기 시간이다.

대기 시간이 TRANSACTION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="aca188a1407a04ef"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="28e2e422e1893a1a"></a>
### 기본 정보

<a id="bfde951e5d20bc9b"></a>
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

<a id="e05000f791687cbb"></a>
### 설명

TRANSACTION_COMMIT_WRITE_MODE는 트랜잭션이 완료될 때 트랜잭션이 생성한 log를 disk log file에 flush할지 여부를 설정한다. 즉, TRANSACTION_COMMIT_WRITE_MODE가 '1'이면 log를 트랜잭션 완료 시점에 disk log file에 flush해야 하고, 그렇지 않은 경우 log flush 여부와 관계없이 트랜잭션을 완료한다.

만약 TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정하여 시스템을 운용하는 경우에 트랜잭션을 COMMIT 한 후 log flush가 되지 않은 상태에서 GOLDILOCKS가 비정상적으로 종료되면 기록되지 않은 log로 인해 최신 data를 잃어버리게 된다.

따라서 모든 트랜잭션이 완료되었을 때 반드시 database에 남아 있어야 하는 경우 TRANSACTION_COMMIT_WRITE_MODE를 '1'로 설정하여 시스템을 운용하거나, TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정한 후 트랜잭션이 완료되는 시점에 명시적으로 'ALTER SYSTEM FLUSH LOGS' 문을 수행하여 log를 flush해야 한다.

- 0: no wait
- 1: wait

<a id="c7c9de6d3c903123"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="cdefbe0e2f1f87da"></a>
### 기본 정보

<a id="c9de9e84d14082fc"></a>
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

<a id="4bf8aa6ce21de8b8"></a>
### 설명

트랜잭션이 기록할 수 있는 최대 undo 페이지 개수를 의미한다. 최소값은 1로 8 Kbyte이며, 최대값은 13107200으로 100 Gbyte이다.

<a id="7ec7d83414e6673c"></a>
## TRANSACTION_TABLE_SIZE

<a id="cb172b2cdc8feed3"></a>
### 기본 정보

<a id="0599a379cd007793"></a>
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

<a id="6410c6066b22c520"></a>
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

<a id="953f8dd654a0d615"></a>
## TRANSACTION_TIMEOUT

<a id="af21694e1011256d"></a>
### 기본 정보

<a id="8050ebb0a4063d4a"></a>
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

<a id="51d2a8b14c60922a"></a>
### 설명

Transaction이 활성화되어 있는 시간을 설정한다. Transaction이 장시간 활성화되어 있을 때 발생할 수 있는 부작용을 예방하기 위해 사용된다. 정해진 시간을 초과한 transaction이 있을 경우, gmaster 데몬이 해당 transaction을 소유한 세션을 자동으로 종료시킨다.

<a id="d58c60376f74c330"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="df9d1c315bc8181d"></a>
### 기본 정보

<a id="e655c8abb0d0155e"></a>
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

<a id="271ca90a1144e8f2"></a>
### 설명

Undo relation을 할당할 때의 최대 대기 시간이다.

대기 시간이 UNDO_RELATION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="af0b2c19e7f6c064"></a>
## UNDO_RELATION_COUNT

<a id="9793cde20d1d91f7"></a>
### 기본 정보

<a id="e368c1dc63bf2c52"></a>
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

<a id="67d722acfaf7aecb"></a>
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

<a id="34f13237187e6e54"></a>
## UNDO_SHRINK_THRESHOLD

<a id="b098bc8dee2c2cf7"></a>
### 기본 정보

<a id="3ba8266050500566"></a>
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

<a id="f503aec0e1d96af2"></a>
### 설명

Ager thread는 주기적으로 (10초) undo segment 공간을 검사하여 이 속성값보다 많은 공간을 차지하고 있을 경우, 재사용 가능한 공간을 테이블스페이스로 반환한다. Undo segment의 공간이 이 속성 (byte)만큼 남을 때까지 반환을 시도하다가 남은 undo page의 양이 MINIMUM_UNDO_PAGE_COUNT보다 작아지면 반환을 종료한다.

<a id="51f9068c33c263be"></a>
## USE_LARGE_PAGES

<a id="c8d2a7aa06b21381"></a>
### 기본 정보

<a id="c8da995d36e7d01a"></a>
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

<a id="458cd4a7bbe59bf0"></a>
### 설명

HugePage를 사용한다. USE_LARGE_PAGES를 사용하려면 먼저 장비에 HugePage를 설정해야 한다.

- 0: Large page를 사용하지 않는다.
- 1: Large page를 사용한다. 만약 공유 메모리 할당에 실패할 경우에는 에러가 발생한다.
- 2: Large page를 사용하여 할당을 시도한다. 만약 공유 메모리 할당에 실패할 경우에는 regular page를 사용하여 메모리를 할당한다.

> 리눅스 커널 2.6.32-573 이상에서만 사용할 수 있다.

<a id="d75aeea9a40a4358"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="b2ec508e63d46844"></a>
### 기본 정보

<a id="3e126cacc6dfd875"></a>
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

<a id="380bde125efb1dcd"></a>
### 설명

사용자 데이터 테이블스페이스를 생성할 때 테이블스페이스의 media 타입이 생략된 경우, default media 타입을 지정한다. 0은 memory, 1은 disk를 의미한다.

<a id="00d23afed1c001a6"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="d5d700d3b6bcf370"></a>
### 기본 정보

<a id="e880b7a7bbf7e81a"></a>
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

<a id="d461ce12ee6aa2a7"></a>
### 설명

사용자 데이터 테이블스페이스가 생성되거나 데이터 파일이 추가될 때 데이터 파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="7f26827b400bd5e0"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="4220c9f2924b3066"></a>
### 기본 정보

<a id="72c536cf1ecc8d17"></a>
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

<a id="6f122d17e654c786"></a>
### 설명

사용자 디스크 데이터 테이블스페이스의 데이터파일이 확장되어야 할 때 확장할 크기가 설정되지 않은 경우, default 크기를 지정한다.

<a id="5020fb65cf781126"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="c69e79810ff0b381"></a>
### 기본 정보

<a id="8fe6aa5d8c9f851d"></a>
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

<a id="5770978615847dd1"></a>
### 설명

사용자 temp 테이블스페이스가 생성되거나 데이터파일이 추가될 때 데이터파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="6323920b5647c1c3"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="c2dd97a590fa4dad"></a>
### 기본 정보

<a id="2088beedd3c0e5f8"></a>
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

<a id="0ccedeff1d871faa"></a>
### 설명

Xa transaction이 idle 상태 (XA가 시작된 후 다음 처리가 발생할 때까지 시간)로 대기할 수 있는 최대 시간이다. Idle 상태로 대기하다가 이 시간을 초과하면 xa transaction은 rollback 된다.

0으로 설정하면 XA가 idle 상태로 있더라도 무한 대기한다.

---

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
