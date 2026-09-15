<a id="5892e8fc0b188208"></a>

# 10. Server Property

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/5892e8fc0b188208)  
> 태그: `20c.1_30_tag`

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<a id="6b25d87f32e874d8"></a>
## Server Property 정보

Property는 다음 SQL 구문으로 변경할 수 있다.

- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references.md#daca16c30923690a) 
- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references.md#4b18743f121b279d)

Property 정보는 다음 view로 확인할 수 있다.

- [V$PROPERTY](9-database-information.md#b2746c8b95b1e0ef)
- [V$SPROPERTY](9-database-information.md#f54634170391e18f)

본 매뉴얼의 property 기본 정보 각 항에 대한 설명은 다음과 같다.

<a id="a21d3710e245e5d5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | Property의 구분자이다. |
| 요약 | Property 요약 설명이다. |
| Data type | Property가 갖는 값의 데이터 타입이다. |
| 적용 단계 | ALTER SYSTEM 또는 ALTER SESSION으로 변경할 수 있는 startup phase에 적용할 수 있다 * NONE: 적용할 수 있는 단계가 없다. (만약 변경 가능하지만 적용 단계가 NONE인 경우에는 SCOPE = FILE을 이용해야 한다.) |
| 변경가능 여부 | Property를 변경할 수 있는지 여부이다. * 해당 값이 TRUE일 경우, 변경할 수 있다. * 해당 값이 FALSE일 경우, read-only만 가능하다. |
| ALTER SESSION 여부 | [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references.md#4b18743f121b279d) 구문으로 변경할 수 있는지 여부이다. |
| ALTER SYSTEM 여부 | [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references.md#daca16c30923690a) 구문으로 변경할 수 있는지 여부이다. * IMMEDIATE: 수행 즉시 모든 SESSION에 변경된 값이 반영된다. * DEFERRED: 수행된 이후에 접속한 SESSION에만 변경된 값이 반영된다. 이미 접속된 SESSION에는 반영되지 않는다. * FALSE: 운영 중에는 변경된 값이 반영되지 않으며 restart 이후에 변경된 값이 반영된다. SCOPE=FILE로만 수행할 수 있다. * NONE: 변경할 수 없다. |
| MIN | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최소값이다.  VARCHAR일 경우에는 N/A이다. |
| MAX | 데이터 타입이 BIGINT인 경우, property가 가질 수 있는 최대값이다. VARCHAR일 경우에는 N/A이다. |
| 기본값 | 해당 property가 갖는 기본값이다. |

<a id="ee42452f0aeedd6d"></a>
## AGING_INTERVAL

<a id="5fbf179781886d30"></a>
### 기본 정보

<a id="8385a2a432c06526"></a>
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

<a id="c3fcf29be19de706"></a>
### 설명

MVCC 기반의 database에서 이전 버전의 데이터를 지우는 ager thread가 처리할 job이 없을 때의 유휴 시간 (초)을 설정한다.

<a id="f7fbfdbbae9253f7"></a>
## AGING_PLAN_INTERVAL

<a id="9a508a6ff7f6e0be"></a>
### 기본 정보

<a id="339aa561a2fb3485"></a>
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

<a id="69205912d3d86bd7"></a>
### 설명

AGING_PLAN_INTERVAL 보다 오래된 SQL plan이 aging 대상이 된다.

<a id="95b2b07b5280b62d"></a>
## ARCHIVELOG_DIR_1 ~ ARCHIVELOG_DIR_10

<a id="c8532b4f80a92b32"></a>
### 기본 정보

<a id="c5c500c5fd1621a5"></a>
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

<a id="4b1f678a754d4515"></a>
### 설명

GOLDILOCKS 데이터베이스의 온라인 redo log file이 archive되는 디렉토리와 미디어 복구할 때 archive redo log file을 읽을 위치를 설정한다. 온라인 redo log file은 ARCHIVELOG_DIR_1에만 archive redo log file을 생성한다.

ARCHIVELOG_DIR_1은 시스템만 설정할 수 있고 ARCHIVELOG_DIR_2 ~ ARCHIVELOG_DIR_10은 세션을 설정할 수 있다.

<a id="176faa207bdd3530"></a>
## ARCHIVELOG_FILE

<a id="6dd7ad4f31ae9902"></a>
### 기본 정보

<a id="c6d5d609538454e5"></a>
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

<a id="a430a64ee7f133c1"></a>
### 설명

온라인 redo log file을 archive 할 때 archive 디렉토리에 저장되는 목적 파일 이름의 prefix를 설정한다. Archive log file은 ARCHIVELOG_FILE에 설정된 prefix에 '_'와 파일 시퀀스, 'log' 확장자가 추가된 형태로 생성된다. 예를 들어, 파일 시퀀스가 0인 로그 파일은 'archive_0.log'으로 아카이빙된다.

<a id="4b4d8b65da05d2cc"></a>
## ARCHIVELOG_MODE

<a id="34082165bad81797"></a>
### 기본 정보

<a id="30e559d758d2a764"></a>
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

<a id="962c38c07343884b"></a>
### 설명

Database를 생성할 때 적용되는 속성으로써 archive log mode를 다음 중 하나의 값으로 설정할 수 있다.

- 0: NOARCHIVELOG
- 1: ARCHIVELOG

Database가 생성된 후 운용되는 동안에는 archive log mode에 영향을 미치지 않고 mount 단계에서 ALTER DATABASE {ARCHIVELOG | NOARCHIVELOG}로 archive log mode를 변경할 수 있다.

<a id="ca70cb69286d4a6c"></a>
## BACKUP_DIR_1 ~ BACKUP_DIR_10

<a id="37ba3a01f495b4a6"></a>
### 기본 정보

<a id="b51470b8a55e055c"></a>
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

<a id="2706a793f811c53c"></a>
### 설명

증분 백업이 수행될 때 백업 파일이 생성되고 증분 백업을 이용하여 파일을 복원할 때 백업 파일이 읽혀질 디렉토리를 설정한다. 증분 백업은 BACKUP_DIR_1에 설정된 디렉토리에만 생성된다.

BACKUP_DIR_1은 시스템만 설정할 수 있고 BACKUP_DIR_2 ~ BACKUP_DIR_10은 세션을 설정할 수 있다.

<a id="29c7a32340e47489"></a>
## BLOCK_READ_COUNT

<a id="636475ee87307212"></a>
### 기본 정보

<a id="fce51657953fc556"></a>
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

<a id="7983b72c82ca5165"></a>
### 설명

SQL 처리시 row의 묶음 단위인 BLOCK_READ_COUNT 단위로 row를 읽어 연산을 처리한다.   
BLOCK_READ_COUNT는 연산을 수행할 때 한 번에 처리할 row의 개수를 의미하며 SQL 질의 처리에 참여하는 실행 노드간의 pipe-lining 처리의 기본 단위이다.

BLOCK_READ_COUNT 값이 크면 연산 처리 성능은 향상되지만 메모리 자원을 많이 사용한다.  따라서 10 ~ 100 사이의 값을 권장한다. 그 이상의 값을 사용하는 경우 자원 사용량은 비례하여 증가하지만 성능은 비례하여 향상되지 않는다.

<a id="1f5b674b7f44f688"></a>
## BROADCAST_INDEX_REBUILD_PROTOCOL

<a id="5c4356512c82878d"></a>
### 기본 정보

<a id="ff0d02ce7c83b33d"></a>
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

<a id="67877dd20c2c380f"></a>
### 설명

클러스터 환경에서 인덱스를 재구축할 때 여러 멤버에서 동시에 처리할지 여부를 설정한다.

<a id="84257c087c067419"></a>
## BROADCAST_REBALANCE_PROTOCOL

<a id="3891b62de2242be4"></a>
### 기본 정보

<a id="e8502583047655f8"></a>
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

<a id="42ada17e94c1f6c9"></a>
### 설명

클러스터 환경에서 테이블 리밸런스 수행 시 여러 멤버에서 동시 처리가 가능한 프로토콜의 경우 동시 처리를 수행할지 여부를 설정한다.

<a id="a5dee0c6da72e54b"></a>
## BUFFER_CACHE_SIZE

<a id="9f613e937cb80837"></a>
### 기본 정보

<a id="18489a22deb846e0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_CACHE_SIZE |
| 요약 | buffer cache size ( byte ) |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 MB |
| MAX | 1 TB |
| 기본값 | 64 MB |

<a id="e04642b3d0f0f567"></a>
### 설명

디스크 테이블스페이스의 페이지를 caching하는 버퍼의 크기를 설정한다.

<a id="4bfcc335a472ab8d"></a>
## BUFFER_CHECKPOINT_LIST_COUNT

<a id="621d252949867310"></a>
### 기본 정보

<a id="5a9916780e81e699"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_CHECKPOINT_LIST_COUNT |
| 요약 | number of buffer checkpoint lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 36 |
| 기본값 | 1 |

<a id="fc0365125ef8b9ab"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스의 페이지들이 갱신되었을 때 체크포인트 리스트에 연결된다. 각 체크포인트 리스트는 전용 flush thread에 의해 체크포인트 리스트에 연결된 갱신된 페이지를 디스크로 flush 하는데 BUFFER_CHECKPOINT_LIST_COUNT는 체크포인트 리스트의 개수와 flush thread의 개수를 설정한다.

<a id="af5aad728aafedc5"></a>
## BUFFER_FLUSH_THREADS

<a id="6a4077ea4d3b6929"></a>
### 기본 정보

<a id="c28e00fc81b625a5"></a>
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

<a id="01ad38521bb1af67"></a>
### 설명

버퍼 lru list에서 갱신된 페이지를 caching한 bch를 재사용하려면 flush list에 연결하여 buffer flusher에 flush를 요청하게 되는데, 이 때 BUFFER_FLUSH_THREADS가 데이터베이스에서 사용할 buffer flusher와 flush list의 수를 설정한다.

<a id="1c158820718e049f"></a>
## BUFFER_FLUSHING_INTERVAL

<a id="519c61c9561dabd5"></a>
### 기본 정보

<a id="463fe24b7143efe7"></a>
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

<a id="14ed733d53fbd4bb"></a>
### 설명

갱신된 디스크 테이블스페이스 페이지들을 디스크로 flush하는 버퍼 flusher가 처리할 job이 없을 때의 유휴 시간 (sec)을 설정한다.

<a id="b96275518efeb2cc"></a>
## BUFFER_FREE_LIST_COUNT

<a id="f58554e5929d9bad"></a>
### 기본 정보

<a id="073d8f190e3c72af"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_FREE_LIST_COUNT |
| 요약 | number of buffer free lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 64 |
| 기본값 | 16 |

<a id="433c86f16b2dab10"></a>
### 설명

버퍼 캐쉬에 즉시 사용 가능한 bch들을 연결하는 buffer free list의 수를 설정한다.

<a id="1bd792f53d5ba663"></a>
## BUFFER_HASH_BUCKETS

<a id="bd31c14cb7b534bc"></a>
### 기본 정보

<a id="dbb9fc980d9ed566"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_HASH_BUCKETS |
| 요약 | number of buffer hash buckets |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 0 |
| MAX | 1073741824 |
| 기본값 | 0 |

<a id="4539b5116dfa09e5"></a>
### 설명

버퍼에 caching 된 디스크 테이블스페이스 페이지를 위한 hash bucket의 개수를 설정한다. 0 부터 1073741824 까지 설정할 수 있으며 0은 BUFFER_CACHE_SIZE에 따라 설정된 버퍼에 caching 할 수 있는 페이지 수만큼의 hash bucket을 계산하여 설정한다. 만약 설정된 값보다 버퍼의 크기가 작으면 버퍼의 크기로 hash bucket 수를 조정한다.

<a id="d3646878a9120d28"></a>
## BUFFER_HOT_REGION_CRITERIA

<a id="3039e5ce2ede835d"></a>
### 기본 정보

<a id="c21997cf5a269aba"></a>
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

<a id="5f415abf4ad1bbd7"></a>
### 설명

버퍼 lru list에서 cold region에 존재하는 페이지를 hot region으로 옮기기 위한 touch count를 설정한다.

<a id="10e1956399f865fb"></a>
## BUFFER_HOT_REGION_PERCENT

<a id="27e6328729f5c7df"></a>
### 기본 정보

<a id="67ff65df3e535e37"></a>
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

<a id="c30cd312710ac829"></a>
### 설명

버퍼 lru list에 존재하는 전체 페이지 중에 hot region의 페이지의 비율 (백분율)을 설정한다.

<a id="13083c99a7903cf9"></a>
## BUFFER_LRU_LIST_COUNT

<a id="72a12f1dcea8e41d"></a>
### 기본 정보

<a id="f8ba818124d95a45"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | BUFFER_LRU_LIST_COUNT |
| 요약 | number of buffer LRU lists |
| Data type | BIGINT |
| 적용단계 | NONE |
| 변경가능 여부 | FALSE |
| ALTER SESSION 여부 | FALSE |
| ALTER SYSTEM 여부 | FALSE |
| MIN | 1 |
| MAX | 64 |
| 기본값 | 16 |

<a id="a2a22b83901cf887"></a>
### 설명

디스크 테이블스페이스 페이지를 caching 하기 위한 free buffer가 없을 때 caching하여 사용 중인 페이지들 중에 victim을 선정하기 위한 lru list의 수를 설정한다.

<a id="6a085d73f9b87018"></a>
## BUFFER_MULTIPAGE_READ_COUNT

<a id="9eff0634fe35a322"></a>
### 기본 정보

<a id="303357e2f8a77daa"></a>
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

<a id="af79db2dc7238cdb"></a>
### 설명

디스크 테이블을 full scan 할 때 한 번의 디스크 IO에 사용할 최대 페이지 수를 설정한다.

<a id="0e812b2c9e76b5d3"></a>
## BULK_IO_PAGE_COUNT

<a id="e6322bae72da6cd5"></a>
### 기본 정보

<a id="fe62466de331f762"></a>
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

<a id="844b792a55c6c12f"></a>
### 설명

서버를 재시작할 때 데이터 파일에 IO READ가 발생할 경우나 데이터 파일을 생성할 때 IO WRITE가 발생할 경우에 사용된다.

서버를 재시작하거나 데이터 파일을 생성할 때 BULK_IO_PAGE_COUNT * 8192 크기만큼 heap 메모리가 할당되며 세션의 PRIVATE_STATIC_AREA_SIZE가 그 크기보다 작을 경우 메모리 부족 에러가 발생할 수 있다. 이 경우에는 PRIVATE_STATIC_AREA_SIZE를 늘려주어야 한다.

<a id="1ed5d56cd36bdb73"></a>
## CDISPATCHER_HOT_POLICY_INTERVAL

<a id="21468cad1313f12c"></a>
### 기본 정보

<a id="39a652e762b0ac00"></a>
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

<a id="8262e13da3d070db"></a>
### 설명

cdispatcher에서 dequeue 할 때 busy waiting 하는 시간이다. Micro second 단위이며 이 값을 크게 하면 CPU를 많이 사용하는 대신 사용자 응답 시간 (latency)은 줄어든다.

<a id="671deffd2ab8337e"></a>
## CDISPATCHER_LOCKLESS_THREADS

<a id="d1ae80b2efd59cb3"></a>
### 기본 정보

<a id="2ff2aefcda23d95b"></a>
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
| MAX | 32 |
| 기본값 | 1 |

<a id="5a7607b1d6ac253d"></a>
### 설명

Lockless 데이터 송수신자의 cdispatcher thread 개수를 설정한다. Lockable 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_THREADS](#1ad390d544ffb7dd) 로 설정한다.

<a id="7d2b99f9893c4fdd"></a>
## CDISPATCHER_SOCKET_BUFFER_SIZE

<a id="831dba2ec7957ab3"></a>
### 기본 정보

<a id="a387892ced6fc99c"></a>
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

<a id="56a0714734930b50"></a>
### 설명

cdispatcher socket buffer (송신자, 수신자)의 크기이다.

<a id="db91e89095d8f8af"></a>
## CDISPATCHER_SYNC_THREADS

<a id="3450eceee2059164"></a>
### 기본 정보

<a id="c7c60df9483388be"></a>
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

<a id="1d361d9bb270de7f"></a>
### 설명

cdispatcher sync thread의 개수이다.

<a id="1ad390d544ffb7dd"></a>
## CDISPATCHER_THREADS

<a id="8c84ae3a128d9f77"></a>
### 기본 정보

<a id="c92e74967ce15327"></a>
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
| MAX | 32 |
| 기본값 | 1 |

<a id="854ec9d5ad460da0"></a>
### 설명

locable 데이터 송수신자의 cdispatcher thread 개수를 설정한다. lockless 데이터 송수신자의 cdispatcher thread 개수는 [CDISPATCHER_LOCKLESS_THREADS](#671deffd2ab8337e) 로 설정한다.

<a id="1dee2f55589adbef"></a>
## CHANGE_TRACKING

<a id="429f2353cb7a129e"></a>
### 기본 정보

<a id="995872010ae69b7c"></a>
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

<a id="be5fbd4329be2384"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 변경된 페이지들을 tracking 할지 여부를 설정한다.

- NO: disable change tracking
- YES: enable change tracking

데이터베이스가 archivelog로 운용 중인 경우에만 mount 이상 단계에서 ALTER DATABASE { ENABLE | DISABLE } CHANGE TRACKING 으로 change tracking을 enable 할 수 있다.

<a id="2c74cdeb62faf3ef"></a>
## CHANGE_TRACKING_EXTENT_SIZE

<a id="b1ea63e067ccab72"></a>
### 기본 정보

<a id="ae08d2edcebbe3b9"></a>
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

<a id="525642fb82179192"></a>
### 설명

Change tracking 할 때 하나의 dirty flag로 표시할 페이지 수를 설정한다. 예를 들어, 32로 설정하면 32 페이지당 하나의 dirty flag를 사용하고, 128로 설정하면 128 페이지당 하나의 dirty flag를 사용한다.

<a id="972bd916aa3076a6"></a>
## CHANGE_TRACKING_FILE

<a id="918a092c44cd43b6"></a>
### 기본 정보

<a id="6193ff12a61d63c4"></a>
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

<a id="50676362db280e3c"></a>
### 설명

Change tracking을 저장할 파일의 디렉토리와 파일 이름을 설정한다.

<a id="73c7d5ff63df2b12"></a>
## CHAR_LENGTH_UNITS

<a id="cf84e15f2569af82"></a>
### 기본 정보

<a id="fc9c518c9334b073"></a>
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

<a id="f776ca5d92add67c"></a>
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

<a id="c1ae35f4e3638d30"></a>
## CHARACTER_SET

<a id="2be75b5bc1205044"></a>
### 기본 정보

<a id="9bcefb43840e907b"></a>
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

<a id="02cfb87e389a4bf6"></a>
### 설명

Database의 character set이다.  
Database를 생성할 때 적용되는 속성으로써 다음 중 하나의 값을 설정할 수 있다.

<a id="0fd9cd92c7f4340e"></a>
| Character set | 설명 |
| --- | --- |
| SQL_ASCII | ASCII standard |
| UTF8 | Unicode, 8-bit |
| UHC | Unified Hangul code |
| GB18030 | Chinese government standard |

<a id="a565bab786e08132"></a>
## CHECK_DEDICATE_CONNECTION_INTERVAL

<a id="401ef19dcf0bd847"></a>
### 기본 정보

<a id="ab488509d51b3712"></a>
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

<a id="38f50aa3db49ba8e"></a>
### 설명

C/S dedicate 환경에서 client가 접속을 강제로 종료했을 경우, 이를 검사하는 주기이다. Dedicate server (gserver)가 socket을 확인하여 끊어졌으면 종료한다. 기본값은 1,000 millisecond (1초)이다.

<a id="00600d199f1da0b8"></a>
## CLIENT_MAX_COUNT

<a id="ee030b9f3aac8f80"></a>
### 기본 정보

<a id="3aa039b53941460d"></a>
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

<a id="5c60cf86cc21ff32"></a>
### 설명

접속할 수 있는 세션의 최대 개수를 설정한다.

<a id="565fbd7974a6c993"></a>
## CLIENT_NUMA_POLICY

<a id="12b74dcad7024a5b"></a>
### 기본 정보

<a id="edbe0ae1600560a4"></a>
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

<a id="94dfeb4d0b8d90a5"></a>
### 설명

Client 프로세스들을 NUMA 노드들에 분배하기 위한 정책을 결정한다. CLIENT_NUMA_POLICY 프로퍼티는 NUMA 프로퍼티가 on 되어있을 때 동작한다.

- 0: 세션 ID를 모듈러 (modular)해서 연결할 NUMA 노드를 결정한다.
- 1: 통계정보를 바탕으로 가장 조금 연결되어 있는 NUMA 노드에 우선적으로 연결한다.
- 2: C/S client는 TCP_CLIENT_NUMA_NODE 프로퍼티에 의해서 결정되고, D/A client는 DA_CLIENT_ NUMA_NODE 프로퍼티에 의해서 결정된다.

<a id="2e95adb58b7e3022"></a>
## CLOSE_PSM_CHILD_STMTS

<a id="68f19fadb908fad8"></a>
### 기본 정보

<a id="ac33c8c970a182a9"></a>
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

<a id="08b708fbeceb7cf4"></a>
### 설명

매 실행 마지막에 PSM의 child 구문을 close 한다.

<a id="c62c4f1868520953"></a>
## CLUSTER_ASYNC_COMMIT

<a id="1589340dc9a3785e"></a>
### 기본 정보

<a id="16f10a3508cfb0b9"></a>
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

<a id="99f4e8bd56c2351b"></a>
### 설명

Cluster system에서 내부적으로 commit protocol을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 commit을 비동기 처리하기 때문에 일시적으로 노드별 consistency가 깨어질 수 있다. 반면에 이 프로퍼티가 꺼져 있으면 commit 할 때마다 동기화하기 때문에 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="c54177ae2728d933"></a>
## CLUSTER_ASYNC_REPLICATION

<a id="5af0ce81e20b442c"></a>
### 기본 정보

<a id="836d246e16574227"></a>
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

<a id="e0861ece20af634b"></a>
### 설명

Cluster system에서 내부적으로 replication을 async 모드로 처리할 것인지 여부를 설정한다.

> 이 프로퍼티가 켜져 있으면 각 노드별로 데이터를 비동기적으로 반영하기 때문에 어떤 노드에 접속하여 작업을 수행하는지에 따라 응답시간이 차이난다. 반면에 이 프로퍼티가 꺼져 있으면 데이터를 변경할 때마다 동기화하기 때문에 전체 성능이 저하될 수 있다. 따라서 원하는 용도에 맞춰서 사용할 프로퍼티를 적절하게 설정해야 한다.

<a id="d4b27dd22f84f997"></a>
## CLUSTER_CM_BUFFER_COUNT

<a id="834cd5a4b878cf31"></a>
### 기본 정보

<a id="8b2ae4bccf62d74a"></a>
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

<a id="4b6356b9c54229e1"></a>
### 설명

Cluster의 communication buffer 개수이다.

<a id="bbb2d0495d335a8a"></a>
## CLUSTER_CM_BUFFER_SIZE

<a id="0521d22477426a58"></a>
### 기본 정보

<a id="13cf2f931db5af75"></a>
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

<a id="02286f908a096718"></a>
### 설명

Cluster의 communication buffer 크기이다.

<a id="7b24ef6f5a9151c8"></a>
## CLUSTER_CM_READ_BUFFER_SIZE

<a id="267e3798043a4ff2"></a>
### 기본 정보

<a id="6bcf46bac18ebbcd"></a>
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

<a id="9fb7f879a1cbb2f6"></a>
### 설명

Communication read block의 크기이다.

<a id="118fc6df92bb6769"></a>
## CLUSTER_COMMIT_SLAVES

<a id="ee941ab00311859b"></a>
### 기본 정보

<a id="b874e734d1d9b666"></a>
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

<a id="0c340cd8ae0de9d5"></a>
### 설명

Commit slave의 번호이다.

<a id="93a7a399dfd9eac1"></a>
## CLUSTER_COMMIT_STREAM_ISOLATION

<a id="a6abb032dd03003a"></a>
### 기본 정보

<a id="795cc6b31bba1698"></a>
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

<a id="d66d13995e0c70e0"></a>
### 설명

Cluster system에서 내부적으로 commit 처리 흐름을 다른 protocol 처리와 분리하여 수행할 것인지 여부를 설정한다. 시스템 환경에 따라 commit 처리를 분리할 경우 성능이 향상될 수 있다.

<a id="257af08a0d602972"></a>
## CLUSTER_CONNECTION

<a id="a4b284c30a9994b6"></a>
### 기본 정보

<a id="efed3fb1aa4825d6"></a>
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

<a id="b246271281d49f0f"></a>
### 설명

Cluster의 connection mode이다. (socket: 0, rdma:1)

<a id="de83e05081d5c6e3"></a>
## CLUSTER_CONNECTION_TIMEOUT_SEC

<a id="0a5b812d1dc8c412"></a>
### 기본 정보

<a id="c0cc8ecc1d54cf14"></a>
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

<a id="45bef4acf19373c5"></a>
### 설명

Cluster의 connection timeout 이다.

<a id="0531a63bae95ba79"></a>
## CLUSTER_DATA_SYNC_SERVERS

<a id="e4424589f3665a0c"></a>
### 기본 정보

<a id="5d1ac006f0a7a9c2"></a>
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

<a id="720988de40be4ef6"></a>
### 설명

Data synchronization server의 개수이다.

<a id="9368ee056984faf2"></a>
## CLUSTER_DEADLOCK_TIMEOUT

<a id="c2bb1514d29abae2"></a>
### 기본 정보

<a id="07c10c40e864379f"></a>
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

<a id="19979a9fc1bc78aa"></a>
### 설명

Lockable cluster server 부족 등으로 cluster server를 점유하려는 경합이 심해지는 경우 cluster deadlock이 발생할 수 있다. Cluster deadlock이 발생한 경우 이 프로퍼티에 설정된 시간만큼 deadlock이 해결되기를 기다리고, 해결되지 않으면 CLUSTER_DEADLOCK_TIMEOUT 에러가 발생한다.

<a id="27a7ce8e229dd498"></a>
## CLUSTER_DISPATCHER_IN_QUEUE_SIZE

<a id="e3bc5d2cbbacd1d4"></a>
### 기본 정보

<a id="5f9d48fc9757da8a"></a>
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

<a id="f28c5b45ab0ad829"></a>
### 설명

Cluster dispatcher in-queue의 크기이다.

<a id="c11c9d7d2c7ead78"></a>
## CLUSTER_DISPATCHER_NUMA_STREAM_MAP

<a id="bcc6f8e35254d6bc"></a>
### 기본 정보

<a id="d74adf6a9996063e"></a>
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

<a id="bc5452f727f7c56d"></a>
### 설명

Cluster 디스패처들이 연결될 NUMA 노드를 결정한다. CLUSTER_DISPATCHER_NUMA_STREAM_MAP 프로퍼티는 NUMA 프로퍼티가 on되어 있을 때 동작한다.

> 만약 CLUSTER_COMMIT_STREAM_ISOLATION 프로퍼티가 on 되어 있다면 0번 스트림은 commit stream의 NUMA 노드로 설정된다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고 1번 스트림은 NUMA 노드 1번에 연결하며 2번 스트림은 NUMA 노드 2번에 연결한다.

```
CLUSTER_DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="a193d50d13f53c54"></a>
## CLUSTER_DISPATCHER_OUT_QUEUE_SIZE

<a id="1edf29c15528cca5"></a>
### 기본 정보

<a id="6000dd850ce8d3ac"></a>
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

<a id="df119e0568a5cb77"></a>
### 설명

Cluster dispatcher의 out-queue 크기이다.

<a id="e8c823089b0c93f8"></a>
## CLUSTER_HEARTBEAT_INTERVAL

<a id="6794cea62733d2ce"></a>
### 기본 정보

<a id="718d9ab56bc069ab"></a>
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

<a id="5345222c86e5c106"></a>
### 설명

Cluster의 상태를 점검하는 주기 (초)이다. 0은 비활성화 상태를 의미한다.

<a id="c5d64d808ef66729"></a>
## CLUSTER_HEARTBEAT_RETRY_COUNT

<a id="be9da02ad0269cc7"></a>
### 기본 정보

<a id="4b2f7efa5e31eafa"></a>
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

<a id="c5e4603892e10c72"></a>
### 설명

Cluster 상태 점검을 다시 시도하는 횟수이다.

<a id="58d76894fd3d9b40"></a>
## CLUSTER_IGNORE_INACTIVE_MEMBER

<a id="fec383e0d621eda3"></a>
### 기본 정보

<a id="137fb0afb8c8b18a"></a>
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

<a id="dae81356cbad8db0"></a>
### 설명

Cluster의 in-active 멤버를 무시한다.

<a id="7e9c834d14b3c64d"></a>
## CLUSTER_MAX_PACKET_SIZE

<a id="23b5a9d63de4fd00"></a>
### 기본 정보

<a id="c7fc44a9523efee0"></a>
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

<a id="f4ab42ab1c46564e"></a>
### 설명

원격 프로토콜이 한 번에 전송할 수 있는 패킷의 최대 크기를 결정한다. 원격으로 전송해야 하는 column의 크기가 CLUSTER_MAX_PACKET_SIZE 프로퍼티 크기를 초과할 경우, 해당 프로퍼티를 column 크기보다 크게 설정해야 한다.

<a id="698e06b95042f1d0"></a>
## CLUSTER_MAX_PAYLOAD_SIZE

<a id="1b75c615b6c52e3f"></a>
### 기본 정보

<a id="2577326419d732ba"></a>
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

<a id="0e93d87bd46bec5c"></a>
### 설명

원격으로 전송되는 클러스터 패킷은 여러 개의 piece로 나뉘어 전달될 수 있는데 CLUSTER_MAX_PAYLOAD_SIZE 프로퍼티는 하나의 piece에 저장할 수 있는 데이터의 최대 크기를 설정한다.

<a id="c60cc652a63f812c"></a>
## CLUSTER_PACKET_ALLOCATION_TIMEOUT

<a id="35bafea00822aa5c"></a>
### 기본 정보

<a id="1a8799abd744cd38"></a>
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

<a id="6a743af5380fa7ff"></a>
### 설명

Cluster 패킷 구성에 필요한 메모리를 할당할 때 기다릴 수 있는 최대 시간 (초)을 설정한다.

<a id="0245afc925dbdd31"></a>
## CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT

<a id="c6e0086646f381c7"></a>
### 기본 정보

<a id="6f8de0678a74a477"></a>
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

<a id="7550854cc68a58ff"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Failover 시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, session을 종료시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT](#8aeb8ef4387e3c5f) property를 사용하여 제한 시간을 설정한다.

<a id="8aeb8ef4387e3c5f"></a>
## CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT

<a id="da7a092dc50ff436"></a>
### 기본 정보

<a id="1d560cec6cb9690d"></a>
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

<a id="378ae6385227182f"></a>
### 설명

Cluster에서 protocol을 전송한 후에 응답이 올 때까지 최대로 대기하는 시간이다. 제한된 시간 내에 응답이 없을 경우 GOLDILOCKS는 protocol에 따라 session을 종료시키거나, 응답이 없는 원격 cluster member를 failover 시킨다. Session을 종료시키는 정책을 사용하려면 *CLUSTER_PROTOCOL_SESSION_FATAL_POLICY_TIMEOUT* property를 사용하여 제한 시간을 설정하고, failover 시키는 정책을 사용하려면 [CLUSTER_PROTOCOL_FAILOVER_POLICY_TIMEOUT](#0245afc925dbdd31) property를 사용하여 제한 시간을 설정한다.

<a id="4067980b56607177"></a>
## CLUSTER_SERVER_RESPONSE_QUEUE_SIZE

<a id="0d649c9785bd9569"></a>
### 기본 정보

<a id="04d6995a23d57882"></a>
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

<a id="48cd014fc0f4d932"></a>
### 설명

원격 서버로부터 응답을 받기 위한 queue의 최대 크기를 설정한다.

<a id="7827552e29820f46"></a>
## CLUSTER_SESSION_HASH_BUCKETS

<a id="b4e597a273457583"></a>
### 기본 정보

<a id="907ea1035c36a820"></a>
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

<a id="44a3660a2b99245b"></a>
### 설명

Cluster session을 관리하기 위한 hash bucket의 개수를 설정한다.

<a id="e29c13f6b906efd3"></a>
## CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY

<a id="db518892eac649cf"></a>
### 기본 정보

<a id="10ab318eb418b881"></a>
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

<a id="256922af30f8cc6d"></a>
### 설명

Cluster system에서 split-brain 상황을 해결하기 위한 정책을 설정한다. 1 이상의 값으로 설정할 경우 해결 방안을 locator에게 질의한다.

> Locator에게 한 질의에 timeout이 발생하면 CLUSTER_SPLIT_BRAIN_RETRY_COUNT만큼 질의를 시도한다. 재시도에 실패하면 속성값이 1인 경우에는 failover를 강제로 진행하고 속성값이 2인 경우에는 fatal 종료한다.

<a id="8494f9beebc38bc1"></a>
## CLUSTER_SPLIT_BRAIN_RETRY_COUNT

<a id="ca9e4e56a9a3890d"></a>
### 기본 정보

<a id="00694362863655d6"></a>
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

<a id="6a1c431267f552dd"></a>
### 설명

Cluster system에서 CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY가 1 이상으로 설정되었을 경우에 사용된다. Locator에게 보낸 질의에 응답이 없을 경우, 질의를 다시 시도하는 횟수를 설정한다.

<a id="915ef3c179101a20"></a>
## COMMITTER_HOT_POLICY_INTERVAL

<a id="60e1a409938f0a6c"></a>
### 기본 정보

<a id="08c935afbcd932bb"></a>
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

<a id="a582d1834fc5d687"></a>
### 설명

Commit cserver가 commit protocol 메시지를 읽기 위해 deque 할 때 busy waiting의 기준 시간 간격을 설정한다. 만약 1000000 (1초)로 설정할 경우, 이전 deque에 성공한 이후 다시 deque를 시도할 때까지 1 초를 경과하지 않았다면 deque에서의 대기시간 (timeout)을 0으로 설정하여 busy waiting 한다.

<a id="8ca9279aea15e71a"></a>
## CONTROL_FILE_0 ~ CONTROL_FILE_7

<a id="e5d7d8931703eb57"></a>
### 기본 정보

<a id="9d3f4bfd91a4aa56"></a>
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

<a id="113a876a4e104bd0"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화해야 하는데 이 때 각 control file이 저장될 디렉토리와 파일 이름을 설정한다.

<a id="fbb88bf30587b3b7"></a>
## CONTROL_FILE_COUNT

<a id="6be486d705d7faa3"></a>
### 기본 정보

<a id="989121f083dab1ed"></a>
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

<a id="00e5b4a81d5fbc2c"></a>
### 설명

Control file이 훼손되면 database를 사용할 수 없기 때문에 안정성을 위해 control file을 다중화한다. CONTROL_FILE_COUNT는 control file의 다중화 개수를 설정하며 최소 두 개에서 최대 여덟 개까지 다중화할 수 있다.

<a id="72ac0375385a21df"></a>
## CONTROL_FILE_TEMP_NAME

<a id="4a8009fdc92d736e"></a>
### 기본 정보

<a id="a68856031ed36e14"></a>
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

<a id="3bdfb545b2e3339d"></a>
### 설명

Database를 운용하는 중에 control file은 수시로 변경되고 필요할 경우 임시로 복사본을 만들 수도 있다. CONTROL_FILE_TEMP_NAME은 control file이 임시로 저장되는 디렉토리와 파일 이름을 설정한다.

<a id="110d7d96a15c6633"></a>
## COORDINATOR_COMMIT_WRITE_MODE

<a id="43ece745ced0c48e"></a>
### 기본 정보

<a id="b03e740bd22314f1"></a>
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

<a id="a3542a972a30da3a"></a>
### 설명

조정자 (coordinator)에 적용되는 commit write mode 이다. 만약 TRANSACTION_COMMIT_WRITE_MODE가 "no wait"이고 해당 프로퍼티가 "wait" 인 경우라면 조정자 노드는 "wait"으로 동작하고 그 외 노드들은 "no wait"으로 동작한다.

<a id="7bcabacc6dd16b96"></a>
## CSERVERS

<a id="be558577f55a9646"></a>
### 기본 정보

<a id="5dbf9a24a67a3af7"></a>
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
| MAX | 512 |
| 기본값 | 10 |

<a id="91bc44c8a4e4f0d5"></a>
### 설명

lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수는 [LOCKLESS_CSERVERS](#08572d621976e4cf) 로 설정한다.

<a id="8263e4c9febb4e59"></a>
## DA_CLIENT_NUMA_NODE

<a id="423a3b8c3e17fb52"></a>
### 기본 정보

<a id="5cb5aa9153685285"></a>
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

<a id="61db9227cfa039d3"></a>
### 설명

Direct Access (D/A) 세션이 바인드 될 NUMA 노드 ID를 설정한다. DA_CLIENT_NUMA_NODE는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="864b0bea0ceb423f"></a>
## DATA_STORE_MODE

<a id="fe14adb15f10eb82"></a>
### 기본 정보

<a id="41165f7e106d32a2"></a>
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

<a id="8060f42cba298d48"></a>
### 설명

Database의 저장 방식을 설정한다.

- 1: CDS 모드는 다중 사용자에 대한 동시성은 지원하지만 영속성은 보장하지 않는다. 즉, data 삽입/ 삭제/ 갱신을 비롯하여 database를 변경하는 모든 연산에 대한 로그를 기록하지 않기 때문에 장애가 발생할 경우 복구할 수도 없다.
- 2: TDS 모드는 다중 사용자에 대한 동시성 및 로그를 이용한 영속성을 보장한다.

<a id="05f3a7f8610e7992"></a>
## DATABASE_ACCESS_MODE

<a id="30b0492718c76914"></a>
### 기본 정보

<a id="21eec76bd4592a93"></a>
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

<a id="bfe3b06d9cdf90df"></a>
### 설명

Database를 시작할 때 접근 모드를 설정한다.

- 0: Database 조회만 할 수 있고 삽입/ 갱신/ 삭제는 불가능하다.
- 1: Database를 조회/ 삽입/ 삭제/ 갱신할 수 있다.

<a id="3aef71218e1f0e74"></a>
## DATABASE_INSTANCE_NAME

<a id="a97a00b17c0448a2"></a>
### 기본 정보

<a id="3ab50e3cfdd98997"></a>
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

<a id="4179452bae3a74c1"></a>
### 설명

데이터베이스의 instance 이름이다.

<a id="d870c4f82263ee42"></a>
## DDL_AUTOCOMMIT

<a id="664c6c4724b6a73f"></a>
### 기본 정보

<a id="fedfddb144aeb7d1"></a>
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

<a id="5ac6ba213be1b13b"></a>
### 설명

Autocommit이 적용되지 않는 DDL에 대한 autocommit 여부를 설정한다. 예를 들어, table의 생성과 변경에는 autocommit이 적용되지 않기 때문에 DDL_AUTOCOMMIT이 '0'인 경우 rollback을 수행하여 table 생성과 변경을 철회할 수 있다. 이에 반해 DDL_AUTOCOMMIT을 '1'로 설정하면 autocommit이 적용되지 않는 DDL들이 즉시 commit 된다.

<a id="c74ed7c43d59727e"></a>
## DDL_LOCK_TIMEOUT

<a id="09c8f0e93dccf9dd"></a>
### 기본 정보

<a id="e51ea07b9949ad48"></a>
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

<a id="072f4ed761028267"></a>
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

<a id="c1c580cb41b0ba84"></a>
## DEADLOCK_PRIORITY

<a id="f1adbe753e89e2e2"></a>
### 기본 정보

<a id="98a68dea41235e07"></a>
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

<a id="95d1e2ef448295ad"></a>
### 설명

다수의 트랜잭션을 동시에 수행하다가 deadlock이 발생할 경우, deadlock을 유발한 트랜잭션들 중에서 weight 값이 낮은 트랜잭션을 victim으로 선택하여 deadlock을 해결한다. 이 속성값이 상대적으로 높은 세션에서 시작된 트랜잭션과, 이 속성값이 더 낮은 세션에서 시작된 트랜잭션 사이에서 deadlock이 발생하면, 이 속성값이 더 낮은쪽 트랜잭션이 deadlock victim으로 선택된다. Deadlock이 발생했을 때 어느 트랜잭션을 우선적으로 처리할 것인가에 따라 이 속성값을 설정해야 한다.

이 속성값을 설정한 후에 트랜잭션을 시작해야 이 값이 해당 트랜잭션의 weight으로 적용되며, 트랜잭션이 시작된 후에는 이 값을 변경하더라도 트랜잭션의 weight는 변경되지 않음에 유의해야 한다.

<a id="7f1c0835161cb0bd"></a>
## DEFAULT_GLOBAL_SECONDARY_INDEX_CREATION

<a id="ea0e3b3f5e3ef096"></a>
### 기본 정보

<a id="0a9510056a496012"></a>
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

<a id="4416415091a5427f"></a>
### 설명

Cluster system에서 테이블을 생성할 때 global secondary index를 생성할지 여부를 설정한다. Global secondary index를 생성하지 않은 테이블에 대한 non-deterministic 질의는 실패한다. NO로 설정한 상태에서 테이블을 생성한 후에 별도로 global secondary index를 생성할 수도 있다.

<a id="18af0467c7305800"></a>
## DEFAULT_INDEX_LOGGING

> 3.2 이후로 지원하지 않는다.

<a id="5d2f89a445688ba3"></a>
### 기본 정보

<a id="2b856a4befde500e"></a>
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

<a id="e498eed5bcf3ba9c"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 LOGGING 속성을 지정하지 않은 경우, LOGGING 속성은 DEFAULT_INDEX_LOGGING 프로퍼티 값으로 설정된다. 만약 인덱스가 LOGGING 테이블스페이스에 생성되면 반드시 LOGGING 속성이 설정되어야 한다.

<a id="634522b46caa996e"></a>
## DEFAULT_INDEX_PCTFREE

<a id="1a25aecd5fb77bf1"></a>
### 기본 정보

<a id="bbf7b6dbe0dfe7ed"></a>
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

<a id="86a3d998d2c47392"></a>
### 설명

인덱스를 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_INDEX_PCTFREE 프로퍼티 값으로 설정된다.

<a id="20a8b41202237971"></a>
## DEFAULT_INITRANS

<a id="5b5b42c7baa8dc1f"></a>
### 기본 정보

<a id="7505a061aa5c5dfb"></a>
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

<a id="2ff4823016d6ebe9"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 INITRANS 구문을 지정하지 않은 경우 INITRANS는 DEFAULT_INITRANS 프로퍼티 값으로 설정된다.

<a id="fe1c8130fa479435"></a>
## DEFAULT_MAXTRANS

<a id="788f0d643c8ada1e"></a>
### 기본 정보

<a id="e0513ba3305273a4"></a>
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

<a id="62ef035a5f49b841"></a>
### 설명

테이블이나 인덱스를 생성할 때 사용자가 명시적으로 MAXTRANS 구문을 지정하지 않은 경우 MAXTRANS는 DEFAULT_MAXTRANS 프로퍼티 값으로 설정된다.

<a id="3417c93aa0f18d18"></a>
## DEFAULT_PCTFREE

<a id="3bbea830c1326ea9"></a>
### 기본 정보

<a id="7dc404056ba9b8a3"></a>
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

<a id="904bfbc2c269dc01"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTFREE 구문을 지정하지 않은 경우 PCTFREE는 DEFAULT_PCTFREE 프로퍼티 값으로 설정된다.

<a id="bb31c38575b030b7"></a>
## DEFAULT_PCTUSED

<a id="a71d1b9cad151f23"></a>
### 기본 정보

<a id="19be2b64b1c25dc0"></a>
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

<a id="7f9f204fa616648d"></a>
### 설명

테이블을 생성할 때 사용자가 명시적으로 PCTUSED 구문을 지정하지 않은 경우 PCTUSED는 DEFAULT_PCTUSED 프로퍼티 값으로 설정된다.

<a id="162f9c1b8ca7923a"></a>
## DEFAULT_REMOVAL_BACKUP_FILE

<a id="455d65d7db3e6386"></a>
### 기본 정보

<a id="ab497912dd68bec3"></a>
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

<a id="e4ab29cb1b68d2e2"></a>
### 설명

백업 목록을 삭제할 때 백업 파일을 삭제할지 여부를 지정한다.

<a id="eb90dc396c899eab"></a>
## DEFAULT_REMOVAL_OBSOLETE_BACKUP_LIST

<a id="9c6b2a14527a1d8b"></a>
### 기본 정보

<a id="f678f46c26461bc5"></a>
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

<a id="7f202d924648e625"></a>
### 설명

INCREMENTAL BACKUP을 수행할 때 obsolete 된 이전 백업 목록의 삭제 여부를 설정한다.

<a id="e144387380cfccfa"></a>
## DEFAULT_SHARDING

<a id="952bb515d58e000c"></a>
### 기본 정보

<a id="1d0c8acffaa91d79"></a>
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

<a id="370845d4ac7eb936"></a>
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

<a id="70417d25a12eef45"></a>
## DISABLE_DDL_CDC_GIVEUP

<a id="dbb21b736ec94733"></a>
### 기본 정보

<a id="28ad5f5e3c23ea2e"></a>
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

<a id="dbf1b67343adae34"></a>
### 설명

CDC의 give up에 영향을 미치는 supplemental log 대상 테이블에 대한 DDL 수행을 금지한다.  
관련 DDL은 [DDL 구문에 따른 give-up 발생 및 절차에 따른 허용 여부](../part-07-replication/48-cyclone.md#9a83f84426f61a37)를 참조한다.

<a id="0ab93e6df7502ac6"></a>
## DISABLE_UPDATE_PK_CDC_GIVEUP

<a id="4f76f48be2603722"></a>
### 기본 정보

<a id="9b2cf5f478320a74"></a>
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

<a id="7d6dc72451b6d16a"></a>
### 설명

CDC give up을 유발한 UPDATE primary key를 비활성화 한다.

<a id="82be57d67c9fee84"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE

<a id="aa6a59cfc0a40f4b"></a>
### 기본 정보

<a id="5433ab554a1f1ad9"></a>
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

<a id="9affd6bc56d04eda"></a>
### 설명

TARGETTYPE protocol을 허용하지 않는다.

<a id="63bc1f48a538fc8f"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_ALL

<a id="89e6a39a0c819027"></a>
### 기본 정보

<a id="76131b0b1edd328e"></a>
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

<a id="e04a63eb43287309"></a>
### 설명

TARGETTYPE_WITH_ALL protocol을 허용하지 않는다.

<a id="94eb4663803b42c0"></a>
## DISALLOWED_PROTOCOL_TARGETTYPE_WITH_NAME

<a id="c89a0752ed8923cc"></a>
### 기본 정보

<a id="36bd089b1040bdde"></a>
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

<a id="796ba45aec936e74"></a>
### 설명

TARGETTYPE_WITH_NAME protocol을 허용하지 않는다.

<a id="c11b9c1292b1feaa"></a>
## DISPATCHER_CM_BUFFER_SIZE

<a id="0dde0d24909394d2"></a>
### 기본 정보

<a id="27a7464d493898f0"></a>
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

<a id="6e19ba14bc6eecb0"></a>
### 설명

Shared 모드에서 사용하는 전체 communication buffer 크기로써 Shared Static Area (SSA) 내에 할당되어 사용된다.

<a id="e30a74c34b59a5f9"></a>
## DISPATCHER_CM_UNIT_SIZE

<a id="3081336019ef6910"></a>
### 기본 정보

<a id="b7f7596f470f0b9d"></a>
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

<a id="19b8f67b67247ba5"></a>
### 설명

Shared 모드에서 dispatcher가 관리하는 unit의 크기이다. 이 크기가 크면 메모리가 낭비되고 이 크기가 작으면 성능이 저하될 수 있다.  
Shared 모드에서 통신 packet의 최대 크기로 설정된다.

<a id="7eb7bac1c571cf2c"></a>
## DISPATCHER_CONNECTIONS

<a id="36c5ed8f45e297fe"></a>
### 기본 정보

<a id="a78d8f8d2941b1b1"></a>
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

<a id="3e1107bdc7485865"></a>
### 설명

Shared 모드에서 하나의 dispatcher가 관리할 수 있는 최대 connection (client)의 개수이다.  
시스템에서 지원하는 최대값이 설정값보다 작으면 내부적으로 시스템 최대값으로 설정된다.

<a id="cbc04fe82db97f6f"></a>
## DISPATCHER_HOT_POLICY_INTERVAL

<a id="e8c8289caceb044f"></a>
### 기본 정보

<a id="2b49d78dc15a0767"></a>
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

<a id="b3784f24f48ddb9a"></a>
### 설명

Busy waiting에 대한 dispatcher dequeue 주기이다. (micro second)

<a id="87649d609d27df78"></a>
## DISPATCHER_LOAD_BALANCING

<a id="4f498b7270812c76"></a>
### 기본 정보

<a id="702e7cf6bd955cd5"></a>
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

<a id="2ab2a4eabb213818"></a>
### 설명

Shared 모드에서 client에 접속할 때 dispatcher를 할당하는 알고리즘이다.

- 0: 현재 연결된 client 수가 적은 dispatcher에 할당한다.
- 1: 순차적으로 dispatcher에 할당한다.

<a id="97047c314c3ecc6c"></a>
## DISPATCHER_NUMA_STREAM_MAP

<a id="edc27a8e06b66d9f"></a>
### 기본 정보

<a id="b8b49030df8bf6d9"></a>
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

<a id="bd680d8c8706a1e2"></a>
### 설명

디스패처들이 연결될 NUMA 노드를 결정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

다음은 디스패처가 세 개인 경우의 예이다. 0번 스트림은 NUMA 노드 0번에 연결하고, 1번 스트림은 NUMA 노드 1번에 연결하고, 2번 스트림은 NUMA 노드 2번에 연결한다.

```
DISPATCHER_NUMA_STREAM_MAP = '0:1:2'
```

<a id="fe966afda6b6ceda"></a>
## DISPATCHER_QUEUE_SIZE

<a id="d1a3f64cf4a81f1d"></a>
### 기본 정보

<a id="266ba67787d413a9"></a>
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

<a id="c040d4ff55273228"></a>
### 설명

Shared 모드에서 dispatcher와 shared-server 간의 통신을 위한 queue 크기를 설정한다.

<a id="6ce097ff0a412c47"></a>
## DISPATCHER_RESPONSE_MINI_QUEUE_COUNT

<a id="ccb83f8e19e319a6"></a>
### 기본 정보

<a id="ec6d5645638b2bd8"></a>
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

<a id="7d3c4d8980b09940"></a>
### 설명

각 response queue의 mini queue 개수이다.

<a id="9755b351f07db769"></a>
## DISPATCHER_REQUEST_MINI_QUEUE_COUNT

<a id="bd7f087b11a3d538"></a>
### 기본 정보

<a id="cc826005e9ec41d6"></a>
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

<a id="4fe5cc6a01b0cd17"></a>
### 설명

각 request queue의 mini queue 개수이다.

<a id="f72e5f95109928eb"></a>
## DISPATCHERS

<a id="0cd8687eb91a3769"></a>
### 기본 정보

<a id="cc7c58e1122c5b12"></a>
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

<a id="551db882ee78e89f"></a>
### 설명

Shared 모드를 사용할 때 dispatcher process 개수를 설정한다.  
Open 단계에서는 alter system을 사용하여 값을 줄일 수 없다.

<a id="19ca321be7fe8b1e"></a>
## FETCH_FAILOVER

<a id="59e48d41e4692df6"></a>
### 기본 정보

<a id="d6e1e9bd70e328cd"></a>
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

<a id="a576cdd452a73cbb"></a>
### 설명

Fetch failover를 활성화한다.

<a id="e1e07b2ed9848ec7"></a>
## GLOBAL_CONNECTION_ALLOW_SESSION_DEPENDENCY

<a id="c62c930254627e9d"></a>
### 기본 정보

<a id="253d9dda368e250d"></a>
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

<a id="caef50fe42a78ec1"></a>
### 설명

Global connection에서 session dependent한 정보를 포함한 질의 수행 지원 여부를 설정한다.

<a id="32c1554a4994ece0"></a>
## GLOBAL_JOURNAL_BUFFER_SIZE

<a id="cd96cb7f89f11b1b"></a>
### 기본 정보

<a id="c4f519a1f7f22ee4"></a>
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

<a id="cc4b2f13b9441e8b"></a>
### 설명

Global journal의 buffer 크기이다.

<a id="40217b2ef2b0c799"></a>
## GLOBAL_JOURNAL_BUFFER_TOTAL_MAX_SIZE

<a id="6c4454174bc85561"></a>
### 기본 정보

<a id="8edf63ff299fa362"></a>
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

<a id="4b3cd9762289e474"></a>
### 설명

Global journal buffer의 최대 사이즈의 합이다.

<a id="345b0b4b3875158a"></a>
## GLOBAL_PROPERTY_LOCK_TIMEOUT

<a id="b4754e06d42c9dc6"></a>
### 기본 정보

<a id="a5b7581542383cab"></a>
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

<a id="5e75851ccca2656d"></a>
### 설명

Global property를 변경할 때 동시성을 제어하기 위해 lock 하는데 이 때 해당 lock 하기 위해 대기하는 시간을 설정한다.

<a id="e4f03944a64c2a8c"></a>
## GLOBAL_TRANSACTION_COMMIT_WRITE_MODE

<a id="0945631e748ac3fd"></a>
### 기본 정보

<a id="df2c8e6e3d79ee35"></a>
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

<a id="7ae8463846498192"></a>
### 설명

Global transaction의 commit write mode를 변경하기 위한 프로퍼티이다. TRANSACTION_COMMIT_ WRITE_MODE는 모든 트랜잭션들에 적용되는 반면에 이 프로퍼티는 global transaction에만 적용된다. 만약 해당 프로퍼티가 2로 설정되면 TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

- 0: no wait
- 1: wait
- 2: TRANSACTION_COMMIT_WRITE_MODE 값을 따른다.

<a id="1d2e700b80482ed8"></a>
## GLOBAL_TRANSACTION_ISOLATION_SCOPE

<a id="8a90b10bc07672f8"></a>
### 기본 정보

<a id="d5349d979e8ea32d"></a>
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

<a id="0295a3aa2187663c"></a>
### 설명

Transaction이 두 개 이상의 cluster group에 걸쳐 데이터를 변경한 경우 이를 global transaction으로 처리할지 다수의 domain transaction으로 처리할지 결정하는 프로퍼티이다.

- 0: Global tranaction으로 처리
- 1: 다수의 domain transaction으로 처리

> 이 프로퍼티가 1인 경우에는 cluster group마다 독립적인 트랜잭션으로 commit하기 때문에 트랜잭션 원자성 (transaction atomicity)을 보장하지 않는다.

<a id="417a9c5834fbc351"></a>
## GLOBAL_TRANSACTION_LOG_DIR

<a id="4cf986f9b81d4ddf"></a>
### 기본 정보

<a id="f2fae4b59975e3f0"></a>
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

<a id="ee0000b0c05d7823"></a>
### 설명

Global transaction log의 기본 directory 이다.

<a id="b4ee77276a33afaa"></a>
## GLOBAL_TRANSACTION_LOG_FILE_SIZE

<a id="483e7462245c22e7"></a>
### 기본 정보

<a id="51496b8117b131a5"></a>
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

<a id="a0691e88862a04ba"></a>
### 설명

Global transaction log의 file 크기이다.

<a id="d151201da0fa1229"></a>
## GMASTER_NUMA_NODE

<a id="f63a825d93eb4f05"></a>
### 기본 정보

<a id="46bfb21f8f4676fa"></a>
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

<a id="1535736a2ab9503f"></a>
### 설명

gmaster 데몬이 사용할 NUMA node의 ID를 설정한다. GMASTER_NUMA_NODE 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="f93b1d8360927a8c"></a>
## GMON_AUTOSTART

<a id="268287d9ad0cd941"></a>
### 기본 정보

<a id="6b40abe5a270d52b"></a>
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

<a id="e0b798941839b268"></a>
### 설명

gmon 프로세스를 자동으로 시작시킬지 여부를 설정한다.

<a id="d0d6276280d2ca4e"></a>
## HINT_ERROR

<a id="e3022ee925264b38"></a>
### 기본 정보

<a id="5a48901df31d3b1f"></a>
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

<a id="df0a7705d59883be"></a>
### 설명

Hint 구문에 대한 syntax error 및 validation error 체크 여부를 설정한다.

<a id="47cc619f17bdffe8"></a>
## IDLE_TIMEOUT

<a id="3b030485241c4ea1"></a>
### 기본 정보

<a id="962645e4313ea6df"></a>
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

<a id="a35b56c5bcd41355"></a>
### 설명

C/S 세션에서 최대로 대기할 수 있는 IDLE 시간을 설정하며 해당 IDLE 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT이 발생하지 않는다.

<a id="2b6e6a158772c423"></a>
## IN_DOUBT_DECISION

<a id="54c7fd7edf770f3a"></a>
### 기본 정보

<a id="2110abf4590f0eaa"></a>
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

<a id="c87ffe7d42e3e8d9"></a>
### 설명

분산 트랜잭션의 in-doubt 트랜잭션을 commit 할지 rollback 할지 결정한다.

- 1: Commit
- 2: Rollback

<a id="174103a82ca33399"></a>
## IN_KEY_RANGE_ARRAY_COUNT

<a id="ebbe20e5e7ba0f70"></a>
### 기본 정보

<a id="3f72aacccd245180"></a>
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

<a id="71308d5e3f99aa12"></a>
### 설명

Array 기반의 in key range scan을 수행할 수 있는 in key range 대상 value들의 최대 개수이다.

- 다음과 같은 구문에 대해 array 기반 in key range scan을 수행하려면 IN_KEY_RANGE_ARRAY_COUNT가 3 이상이어야 한다.

```
gSQL> SELECT * FROM T1 WHERE C1 IN ( 1, 2, 3 )
```

IN_KEY_RANGE_ARRAY_COUNT 값보다 in key range 대상 value들의 최대 개수가 더 많은 경우에는 instant table 기반으로 in key range scan을 수행한다.

<a id="2f496b4892fdea11"></a>
## INCREMENTAL_BACKUP_SCAN_BUFFER_SIZE

<a id="5971cc9b4b8309d2"></a>
### 기본 정보

<a id="9f62568d180406d2"></a>
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

<a id="cdce49491422ca91"></a>
### 설명

디스크 테이블스페이스를 incremental backup 하기 위해 한 번의 디스크 IO로 읽어들일 페이지의 수를 설정한다.

<a id="b8c22df182ec0f9e"></a>
## INDEX_BUILD_PARALLEL_FACTOR

<a id="cb318620bdd06d3b"></a>
### 기본 정보

<a id="8ef6106a312c6a26"></a>
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

<a id="b288636e0716dbeb"></a>
### 설명

인덱스를 생성할 때 병렬화 개수 (parallel factor)를 지정한다.

- 0: 시스템의 코어 개수로 지정된다.

<a id="8b5b1341d8b17e96"></a>
## INDEX_REBUILD_BLOCK_READ_COUNT

<a id="c19530ffae2ca8f9"></a>
### 기본 정보

<a id="1ebc0deda356ea41"></a>
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

<a id="17a075d53e1936b0"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축 하는 도중에 DML이 수행되면 journal data가 저장된다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal data들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. INDEX_REBUILD_BLOCK_READ_COUNT는 이 과정에서 journal data를 얼마만큼 읽어들여 인덱스에 반영할지를 나타낸다.

<a id="88a23b500d88d3e3"></a>
## INDEX_TREE_MERGE_PARALLEL_FACTOR

<a id="5d2e24ca8ab72239"></a>
### 기본 정보

<a id="45973f479956ba40"></a>
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

<a id="5bba87948e9c8911"></a>
### 설명

인덱스를 생성할 때 sub-tree를 합병하기 위한 병렬화 개수 (parallel factor)를 지정한다. 만약 해당 값이 INDEX_BUILD_PARALLEL_FACTOR 보다 큰 경우에는 INDEX_BUILD_PARALLEL_FACTOR를 사용한다.

- 0: INDEX_BUILD_PARALLEL_FACTOR를 따른다.

<a id="4e18d54409856066"></a>
## INST_ALLOCATOR_COUNT

<a id="a4b16d198cb8b14a"></a>
### 기본 정보

<a id="a1e8f958b4c22e46"></a>
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

<a id="7e4eb2b9bd6637b9"></a>
### 설명

인스턴트 블록을 할당 또는 삭제하는 연산의 병렬성을 높이기 위한 프로퍼티이다.

<a id="3649ca841af8360e"></a>
## INST_TABLE_BLOCK_SIZE

<a id="3eb0014a1c1ac7db"></a>
### 기본 정보

<a id="10157325023fda91"></a>
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

<a id="390037fce37559f4"></a>
### 설명

인스턴트 블록의 크기를 결정한다. 만약 인스턴트 레코드의 고정영역 크기가 인스턴트 블록의 크기를 초과하는 경우 다음과 같은 에러가 발생한다.

```
gSQL> SELECT DISTINCT * FROM T1, T1, T1, T1, T1, T1, T1, T1, T1, T1;

ERR-HY000(14098): maximum record length(16360) exceeds
```

<a id="52ee92ad840f8546"></a>
## JOURNAL_TEMP_DIR

<a id="d73fd99ca547d57a"></a>
### 기본 정보

<a id="d964389b8c2a4ec2"></a>
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

<a id="40910d400cb1df08"></a>
### 설명

Journaling의 임시 디렉토리이다.

<a id="0dee846592785c66"></a>
## KEEPALIVE_IDLE_TIME

<a id="1451c831749963ab"></a>
### 기본 정보

<a id="a34d05e9b2a5aee5"></a>
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

<a id="878ee30a426c19f8"></a>
### 설명

Keep alive packet을 송신하기 전에 client와 server 간 TCP packet의 송수신없이 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP packet 교환이 이루어지지 않으면 server 측에서 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="84da28f89339e59a"></a>
## LOCAL_CLUSTER_MEMBER

<a id="b3ad43bb0bef625b"></a>
### 기본 정보

<a id="d75e672dd1fc4557"></a>
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

<a id="6ddd2d929c32e1f8"></a>
### 설명

Local cluster member의 이름이다.

<a id="25c7c7f27ef5c165"></a>
## LOCAL_CLUSTER_MEMBER_HOST

<a id="fd8f1db68e5a1660"></a>
### 기본 정보

<a id="37747f38f1cedd19"></a>
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

<a id="013aab7680283d82"></a>
### 설명

Local cluster member의 host 이름이다.

<a id="06d24809c0adc5fa"></a>
## LOCAL_CLUSTER_MEMBER_PORT

<a id="2c32fe60700d9109"></a>
### 기본 정보

<a id="3ca0fa4a30cc19c9"></a>
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

<a id="df805b143eb1ef04"></a>
### 설명

Local cluster member의 listen port 이다.

<a id="6a91028ba3b32786"></a>
## LOCAL_JOURNAL_BUFFER_SIZE

<a id="3be6deb1fa653708"></a>
### 기본 정보

<a id="312c3d08cc1b25dd"></a>
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

<a id="ada5aa84f8a5b3d1"></a>
### 설명

Local journal buffer의 크기이다.

<a id="7b87ed1cef1e2c3e"></a>
## LOCATION_FILE

<a id="520faf7e5d95b0de"></a>
### 기본 정보

<a id="9b9fd7509a653c52"></a>
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

<a id="972b6d40b1244ebf"></a>
### 설명

Location file의 이름이다.

<a id="f5adbf7d9d5267e4"></a>
## LOCATOR_QUERY_TIMEOUT

<a id="6912f3a2294ecbe7"></a>
### 기본 정보

<a id="f40a5a3b1fb1fea0"></a>
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

<a id="fa1a1798c320dcdd"></a>
### 설명

Cluster system이 split-brain 상황에 대한 해결 방안을 locator에게 질의한 후에 응답을 기다리는 시간 (초)을 설정한다. CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY를 1 이상으로 설정했을 때만 사용할 수 있는 프로퍼티이다.

<a id="7840ab6c9fa2a412"></a>
## LOCK_HASH_TABLE_SIZE

<a id="6d7735d36342be11"></a>
### 기본 정보

<a id="67cac98d7a6a0b00"></a>
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

<a id="b538689510ce40a7"></a>
### 설명

잠금 관리자 (lock manager)가 관리하는 hash table의 최대 크기를 설정한다.

<a id="08572d621976e4cf"></a>
## LOCKLESS_CSERVERS

<a id="1fd6701f8f51a139"></a>
### 기본 정보

<a id="0cb569bbc7db82d5"></a>
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

<a id="b2804c57553669f9"></a>
### 설명

Lock을 획득하지 않는 연산을 수행하는 cluster server 프로세스의 개수를 설정한다. Lock을 획득하는 연산을 수행하는 cluster server 프로세스의 개수는 [CSERVERS](#7bcabacc6dd16b96) 로 설정한다.

<a id="a4c6cf2715e108ce"></a>
## LOG_BLOCK_SIZE

<a id="232be1e880730997"></a>
### 기본 정보

<a id="8d7de48984f3edb0"></a>
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

<a id="0f9cd02b97a818c5"></a>
### 설명

LOG_BLOCK_SIZE는 log buffer가 disk의 log file로 flush 되는 최소 크기이고 512, 1024, 2048, 4096 중 하나의 값으로 설정되어야 한다.

<a id="605705c3a23516a5"></a>
## LOG_BUFFER_SIZE

<a id="7f4835db2f308def"></a>
### 기본 정보

<a id="ae6be2a77d868eba"></a>
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

<a id="4dbedf2c03153748"></a>
### 설명

Database에서 DML 및 DDL 연산을 수행하여 생성한 redo log들은 공유 메모리 공간인 log buffer에 저장되고, LOG_BUFFER_SIZE를 참조하여 log buffer의 메모리 크기를 설정한다.

<a id="3f467bde446bc52c"></a>
## LOG_DIR

<a id="1d65de0a576dfbc6"></a>
### 기본 정보

<a id="4b5460ec56c02cdb"></a>
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

<a id="26c6610cdda2abb9"></a>
### 설명

Log buffer에 기록된 log는 database의 영속성을 보장하기 위해 비휘발성 저장 장치에 존재하는 log file로 flush 되고, LOG_DIR은 log file의 경로를 설정한다.

<a id="4fad35c49f1b85bd"></a>
## LOG_FILE_SIZE

<a id="85ae47c0f4e90adb"></a>
### 기본 정보

<a id="b058cbc5755eccb3"></a>
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
| MAX | 120 Gbyte |
| 기본값 | 100 Mbyte |

<a id="b849650f55919702"></a>
### 설명

Database에서 사용되는 log file의 크기를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 log file size를 변경할 수 없다.

<a id="b1c16102a5256fba"></a>
## LOG_GROUP_COUNT

<a id="6116ea12ee1509e1"></a>
### 기본 정보

<a id="a02a7168e584962d"></a>
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

<a id="da061be8dbe5ec37"></a>
### 설명

Database에서 사용되는 log group의 개수를 설정한다. 이는 database를 생성할 때만 참조되며 이후에는 영향을 미치지 않는다. Database를 생성한 후에 log group을 추가하거나 제거하는 기능은 별도의 구문으로 지원한다.

<a id="ea15619cd1b25f20"></a>
## LOG_MIRROR_MODE

<a id="0ec9bc289c1b81a1"></a>
### 기본 정보

<a id="b5f2fba7028fd1d4"></a>
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

<a id="69dd43c24e9114bc"></a>
### 설명

데이터베이스를 시작할 때 redo log 복제 tool인 LogMirror를 운영할 때 필요한 shared memory를 구성하기 위한 프로퍼티이다.   
LogMirror를 수행하려면 반드시 enable 되어야 한다.  
Shared memory의 크기는 LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE 프로퍼티로 변경할 수 있다.

<a id="8fee690c6fe17776"></a>
## LOG_MIRROR_SHARED_MEMORY_STATIC_SIZE

<a id="516ed427c030c2d3"></a>
### 기본 정보

<a id="3587ffcec7d711d2"></a>
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

<a id="de5b3e003942c411"></a>
### 설명

Redo log 복제 tool인 LogMirror에 사용될 shared memory의 크기를 설정하는 프로퍼티이다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="2e8248b257dae213"></a>
## LOG_MIRROR_TIMEOUT

<a id="904d140da88cce7e"></a>
### 기본 정보

<a id="324fd4c276826350"></a>
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

<a id="a7b60607292d8a29"></a>
### 설명

LogMirror의 응답을 기다리는 시간이다.   
만약 0일 경우 무한정 대기하며 그렇지 않을 경우 설정한 값만큼 대기하다가 TIMEOUT이 발생하고 LogMirror service를 중단한다. 이 후 서버는 정상적으로 운영된다.  
LOG_MIRROR_MODE가 enable 된 상태에서만 적용된다.

<a id="b6f4fa984c8c0c91"></a>
## LOG_SYNC_INTERVAL

<a id="fc5eeaa995f37f26"></a>
### 기본 정보

<a id="f6e36876f8dc0048"></a>
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

<a id="12c3ccec8ec4973d"></a>
### 설명

GOLDILOCKS의 log flusher는 log buffer의 내용을 disk log file로 flush하는 system thread이다. Log flusher가 유휴상태에서 깨어나면 flush 해야 할 log가 있는지 확인하여 있을 경우 flush를 수행한다. 이 때 LOG_SYNC_INTERVAL에 설정된 시간 내에 flush를 하지 않았다면 현재 log buffer의 마지막 block까지 flush를 수행하여 log buffer와 log file을 동기화한다.

<a id="90de572612c47a9c"></a>
## LOG_SYNC_INTERVAL_MSEC

<a id="cda4ed7c7a394fdd"></a>
### 기본 정보

<a id="aca47a4876a404d4"></a>
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

<a id="7aaafaeb31149f38"></a>
### 설명

Log를 동기화하는 millisecond 단위의 주기이다.

<a id="b558eac27b3218ef"></a>
## MAX_GROUP_COUNT

<a id="9a5f19ccebfe736d"></a>
### 기본 정보

<a id="c876e61dc5bfa3e2"></a>
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

<a id="47ed89ea541f8046"></a>
### 설명

그룹의 최대 개수이다.

<a id="a7ba49348dc7d12e"></a>
## MAX_JOURNAL_FILE_SIZE

<a id="e54bd58b581423ab"></a>
### 기본 정보

<a id="fbcbc39eecca6694"></a>
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

<a id="ffb8e8bfe2c164d7"></a>
### 설명

Cluster system에서 journaling이 발생할 경우 내부적으로 journaling data를 저장할 global journaling file 의 최대 크기 (quota)를 설정한다.

<a id="cd84b8e2e58d1d21"></a>
## MAX_NODE_COUNT

<a id="a70b528acd58def4"></a>
### 기본 정보

<a id="e43c6c68543a26fc"></a>
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

<a id="4dec49737cbf0b13"></a>
### 설명

최대 노드 개수이다.

<a id="7d810dcb4bf37edd"></a>
## MAXIMUM_CONCURRENT_ACTIVITIES

<a id="6fc3c1efe4cedee3"></a>
### 기본 정보

<a id="d755c1468dece5e6"></a>
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

<a id="b80eab3e531f214b"></a>
### 설명

동시에 수행될 수 있는 statement 개수를 설정한다.

<a id="49c36ad9046ee5f6"></a>
## MAXIMUM_FLANGE_COUNT

<a id="33cfd9b7c2605342"></a>
### 기본 정보

<a id="689f222f5906cf01"></a>
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

<a id="62dae5e4a27859d1"></a>
### 설명

Plan clock에서 확장될 수 있는 flange의 최대 개수이다.

<a id="2d5ccbaf1fcca4be"></a>
## MAXIMUM_FLUSH_LOG_BLOCK_COUNT

<a id="f6aca9a0ca3b3ae8"></a>
### 기본 정보

<a id="e5d985703e735d79"></a>
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

<a id="135b8c34f4abc7dc"></a>
### 설명

Log buffer의 내용을 disk의 log file에 flush 할 때 한 번의 write 연산으로 flush 할 log block의 최대 개수를 설정한다.

<a id="d1118fe7aa94012f"></a>
## MAXIMUM_FLUSH_PAGE_COUNT

<a id="520fbc6b89a1c73e"></a>
### 기본 정보

<a id="13c4133aaad009fa"></a>
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

<a id="a24601d3e626037d"></a>
### 설명

GOLDILOCKS의 datafile은 checkpoint와 특정 DDL문에 의해 disk에 flush 된다. Datafile을 flush 하기 위해 한 번의 write 연산으로 flush 할 data page의 최대 개수를 설정한다.

<a id="49c2be390f2f5244"></a>
## MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT

<a id="d799b2db743d0dda"></a>
### 기본 정보

<a id="9d0dffa76f687a76"></a>
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

<a id="9f8a83743407eb0b"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하면 DML 수행과 병행하여 처리할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 재구축을 시작한 시점의 데이터를 바탕으로 인덱스를 재구축한 후, journal log들을 통해 재구축하는 동안 변경된 데이터들이 인덱스에 반영된다. Journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="e18d6bc4cfc763a9"></a>
## MAXIMUM_JOURNAL_REPLAY_COUNT

<a id="2348878662d7fbbe"></a>
### 기본 정보

<a id="884a5131bd9f67a4"></a>
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

<a id="480b68ed48f550b1"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스를 DML과 병행하여 수행할 수 있는데 이 때 DML은 변경된 내용을 journal log로 남긴다. 테이블 리밸런스는 테이블을 동기화하는 동안 발생한 journal log를 1차로 반영하고, 다시 journal log를 반영하는 동안 누적된 journal log를 2차로 반영하는데, 이런 방식으로 최대 몇차까지 journal log를 반영할 것인지를 설정한다.

<a id="da4da917bac2f56a"></a>
## MAXIMUM_NAMED_CURSOR_COUNT

<a id="288281788416a4c7"></a>
### 기본 정보

<a id="bfb719a4fad00fd4"></a>
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

<a id="1f15680719e5cea0"></a>
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

<a id="f3616d5addd712c3"></a>
## MAXIMUM_SESSION_CM_BUFFER_SIZE

<a id="81e842e625946311"></a>
### 기본 정보

<a id="bdfd6a2a5f00411f"></a>
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

<a id="2417f09a378cf87b"></a>
### 설명

Shared mode로 접속한 하나의 session에서 사용 가능한 최대 buffer size를 설정한다.  
자세한 내용은 [DISPATCHER_CM_BUFFER_SIZE](#c11b9c1292b1feaa)를 참조한다.

<a id="209210069742905d"></a>
## MEASURE_CLUSTER_LATENCY

<a id="c35f3a2347407f40"></a>
### 기본 정보

<a id="80a388a0e910d249"></a>
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

<a id="5d9b233bf12187da"></a>
### 설명

Measure cluster의 latency 이다.

<a id="3d4046655634428a"></a>
## MEMORY_MERGE_RUN_COUNT

<a id="8d7a3f95bbe027a3"></a>
### 기본 정보

<a id="c8daf43cafa0f8a0"></a>
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

<a id="f284c4577fa0e7fb"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_MERGE_RUN_COUNT는 한 번에 병합할 정렬된 block들의 개수를 설정한다.

<a id="cc1c182363900cdd"></a>
## MEMORY_SORT_RUN_SIZE

<a id="463fb82254d485a2"></a>
### 기본 정보

<a id="be920efb1d572cfd"></a>
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

<a id="45ace39ccfba9560"></a>
### 설명

Bottom-up 방식의 memory B-tree index는 테이블의 모든 key를 추출하여 특정 block size (MEMORY_SORT_RUN_SIZE) 단위로 정렬하고, 정렬된 block들을 병합한 후 internal node를 만드는 방식으로 생성된다. MEMORY_SORT_RUN_SIZE는 정렬할 block 한 개의 크기를 설정한다.

<a id="e85de78158d7e20a"></a>
## MIN_SAMPLE_ROW_COUNT

<a id="c02e3efa2bb5a060"></a>
### 기본 정보

<a id="1a7783783331b193"></a>
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

<a id="616f2776e53d12a4"></a>
### 설명

샘플링을 이용해서 [ANALYZE TABLE](../part-03-sql-manual/18-sql-references.md#d6e173b64ebe5b6c)을 수행할 때의 최소 샘플링 row 건수이다.

<a id="ab7066f7cb181053"></a>
## MINIMUM_UNDO_PAGE_COUNT

<a id="981b0699b36a5b1f"></a>
### 기본 정보

<a id="c356f28d2036708d"></a>
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

<a id="8eeb464c1b877d8f"></a>
### 설명

DML은 이전 image를 저장하기 위해 undo page를 사용한다. DML당 undo segment를 하나씩 사용하여 undo page를 소모하는데, 만약 할당받은 undo segment의 page를 모두 소진하였을 경우 다른 undo segment의 page를 가져와서 사용할 수 있다. MINIMUM_UNDO_PAGE_COUNT는 undo page가 부족할 때 page를 가져올 undo segment를 찾기 위한 최소 undo page 수이다. 즉, undo page가 부족할 때, MINIMUM_UNDO_PAGE_COUNT 보다 많은 page를 보유한 undo segment에서만 page를 가져올 수 있다.

<a id="8df7835c1d5d7479"></a>
## NET_BUFFER_SIZE

<a id="cdd67e4b8e324aae"></a>
### 기본 정보

<a id="080ab45a81c57e75"></a>
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

<a id="9edb30443a8d15c9"></a>
### 설명

TCP 통신 buffer size를 설정한다.  
Dedicated 모드에서는 통신 packet의 최대 크기로 설정된다.  
Shared 모드에서는 [DISPATCHER_CM_UNIT_SIZE](#e30a74c34b59a5f9)가 사용된다.

<a id="ec78df636da07fb6"></a>
## NLS_DATE_FORMAT

<a id="8bd19dd4fb6f6ba0"></a>
### 기본 정보

<a id="4461d302c960faf9"></a>
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

<a id="878127dd575b0308"></a>
### 설명

NLS_DATE_FORMAT은 TO_CHAR와 TO_DATE 함수의 default date format을 지정한다.

<a id="1793ce4c56053b95"></a>
## NLS_TIME_FORMAT

<a id="2477ee7ce46fce28"></a>
### 기본 정보

<a id="e4d971ea01dbcbd8"></a>
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

<a id="f830dfd413bd227b"></a>
### 설명

NLS_TIME_FORMAT은 TO_CHAR와 TO_TIME 함수의 default time format을 지정한다.

<a id="0a90eef2149e893a"></a>
## NLS_TIME_WITH_TIME_ZONE_FORMAT

<a id="4658599158f0df5d"></a>
### 기본 정보

<a id="1eea1b97e24171fe"></a>
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

<a id="6ea2ca80e85fcb94"></a>
### 설명

NLS_TIME_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIME_WITH_TIME_ZONE 함수의 default time with time zone format을 지정한다.

<a id="15c05b1b42192d13"></a>
## NLS_TIMESTAMP_FORMAT

<a id="584353c30dbe9891"></a>
### 기본 정보

<a id="491ad174a89f1150"></a>
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

<a id="f660ff39bc3a91a8"></a>
### 설명

NLS_TIMESTAMP_FORMAT은 TO_CHAR와 TO_TIMESTAMP 함수의 default timestamp format을 지정한다.

<a id="7dad2bb0bce4c28d"></a>
## NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT

<a id="279caf6448d85d21"></a>
### 기본 정보

<a id="f777d4caa0bfcf27"></a>
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

<a id="67a9ddaae28ca7c9"></a>
### 설명

NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT은 TO_CHAR와 TO_TIMESTAMP_WITH_TIME_ZONE 함수의 default timestamp with time zone format을 지정한다.

<a id="508c9f19d157a048"></a>
## NUMA

<a id="ad6f39042083413a"></a>
### 기본 정보

<a id="00179870f9d67f27"></a>
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

<a id="d3cb57eb77a583e8"></a>
### 설명

NUMA를 활성화/ 비활성화한다.

> AIX에서 NUMA 속성을 사용하기 위해서는 사용자 계정을 변경해야 한다. 다음 명령을 루트 사용자로 실행한다.  
>   
> `# chuser "capabilities=CAP_NUMA_ATTACH,CAP_PROPAGATE" <username>`  
>   
> 여기에서 &lt;username&gt;은 루트가 아닌 AIX 사용자 계정이다.  
> 변경 사항을 적용하려면 로그아웃한 후에 다시 로그인해야 한다.

<a id="8f583a5352cf735b"></a>
## NUMA_MAP

<a id="7a34146832ffa0e9"></a>
### 기본 정보

<a id="d216cbb6ae292263"></a>
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

<a id="02783f0f950399a6"></a>
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

<a id="298173672c43f821"></a>
## OFFLINE_MEMBER_AFTER_FAILOVER

<a id="bb5b28ac59698b9d"></a>
### 기본 정보

<a id="123df40a2289c749"></a>
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

<a id="d29314c77cad3eae"></a>
### 설명

시스템의 백그라운드 프로세스 (gmaster)는 노드 장애에 따른 failover를 완료한 후에 장애 멤버를 자동으로 오프라인 시킨다.

만약 NO로 설정되어서 장애 멤버가 오프라인되지 않았다면 장애 멤버를 시스템에 다시 조인시키기 전에 다음 구문을 실행해야 한다.

```
gSQL> ALTER DATABASE OFFLINE INACTIVE CLUSTER MEMBERS;

Database altered.
```

<a id="c2088ccfdfb0784e"></a>
## ONLINE_INDEX_REBUILD_JOURNAL_REPLAY_THRESHOLD

<a id="3cf3a1dded336910"></a>
### 기본 정보

<a id="c18cdbdbe6441b66"></a>
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

<a id="f60553eb206a9dac"></a>
### 설명

인덱스를 ONLINE 모드에서 재구축하는 동안 수행된 DML은 journal log를 남긴다. 인덱스 재구축이 마무리되는 단계에서 여러 차례에 걸쳐 journal이 인덱스에 반영되는데 이 때 journal log를 반영하는 최대 차수는 [MAXIMUM_INDEX_REBUILD_JOURNAL_REPLAY_COUNT](#49c2be390f2f5244)가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="1739aed6da751bf1"></a>
## ONLINE_JOURNAL_REPLAY_THRESHOLD

<a id="799f659e7cd7e212"></a>
### 기본 정보

<a id="f2230708b4fe0d05"></a>
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

<a id="f5d9b9b9804bcfdf"></a>
### 설명

클러스터 환경에서 온라인 테이블 리밸런스는 수행 중에 발생한 DML이 남긴 journal log를 여러 번에 걸쳐 반영한다. Journal log를 반영하는 최대 차수는 MAXIMUM_JOURNAL_REPLAY_COUNT가 결정하지만 journal log를 반영할 때 남은 journal log의 양이 많지 않을 경우에는 굳이 최대 차수만큼 반복하지 않고 즉시 테이블에 EXCLUSIVE lock 하여 마지막 journal log를 반영하기 위한 journal log의 threshold 값으로 사용한다.

<a id="8e58e7afb1544b8a"></a>
## OS_GROUP_ACCESS

<a id="6c0561f6b8d87543"></a>
### 기본 정보

<a id="d63821efee2c4528"></a>
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

<a id="881a54e53d63d3f4"></a>
### 설명

동일한 group의 다른 user가 D/A로 접속하려면 이 설정을 YES로 변경해야 한다. 또한 시스템 상의 umask도 0002로 변경해야 한다.

<a id="82bc8730ab818b23"></a>
## PACKET_COMPRESSION_THRESHOLD

<a id="0439bac70e954eff"></a>
### 기본 정보

<a id="de8fbc3b8ae6a9f6"></a>
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

<a id="ce5541c6011607ea"></a>
### 설명

클라이언트로 보낼 통신 데이터의 크기가 PACKET_COMPRESSION_THRESHOLD 보다 클 경우, 통신 데이터를 압축한다.

<a id="b6ea0cd5dd02fd7c"></a>
## PAGE_CHECKSUM_TYPE

<a id="b70dd0b9fbe77cec"></a>
### 기본 정보

<a id="6d10773eff05ae13"></a>
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

<a id="e0a8ea1c38fefd3c"></a>
### 설명

Datafile의 각 page들에 대한 물리적 정합성을 보장하기 위해 checksum을 사용한다. GOLDILOCKS는 LSN, CRC 방식의 page checksum을 지원한다.

- 0: LSN
- 1: CRC

<a id="cece8facc312d50c"></a>
## PARALLEL_IO_FACTOR

<a id="301d2841f7b0a882"></a>
### 기본 정보

<a id="c9acbda4da9ab317"></a>
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

<a id="79e301de3599057a"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일을 병렬 로딩하고 체크포인트 할 때 데이터 파일을 병렬 기록하기 위한 thread 개수를 설정한다.

<a id="4fb4149ba11dec2d"></a>
## PARALLEL_IO_GROUP_1 ~ PARALLEL_IO_GROUP_16

<a id="317959022b79eb9d"></a>
### 기본 정보

<a id="5f7b0646e1a08020"></a>
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

<a id="3c51ad118c2a3b74"></a>
### 설명

Datafile의 병렬 IO를 위한 group directory를 설정한다. 즉, PARALLEL_IO_FACTOR 수만큼 group을 설정하여 각 group에 속한 datafile 별로 병렬 IO를 수행한다.

<a id="a473667f17702c3f"></a>
## PARALLEL_LOAD_FACTOR

<a id="3062c15b801dd069"></a>
### 기본 정보

<a id="193f7de0c4f21481"></a>
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

<a id="7177884fbf63c4a0"></a>
### 설명

데이터베이스를 시작할 때 데이터 파일의 메모리를 적재한 후에 병렬 작업을 위한 thread 개수를 설정한다.

<a id="1bf3bb738cbdc63c"></a>
## PENDING_LOG_BUFFER_COUNT

<a id="91add8f4ba351cbf"></a>
### 기본 정보

<a id="2ac6924033c82b9d"></a>
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

<a id="c23853946919eac6"></a>
### 설명

여러 트랜잭션이 동시에 실행될 경우 log buffer에 대한 경쟁을 줄이기 위해 pending log buffer를 사용하며, PENDING_LOG_BUFFER_COUNT는 동시에 사용할 수 있는 pending log buffer 개수를 설정한다.

<a id="3020e80cb1f0661c"></a>
## PLAN_CACHE

<a id="c7f590908d916fed"></a>
### 기본 정보

<a id="7ca13ec250f2bd34"></a>
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

<a id="bdb246b8a1a4c6a3"></a>
### 설명

Plan cache 사용 여부를 설정한다.

<a id="1fe7a4d4b4aa3dc8"></a>
## PLAN_CACHE_SIZE

<a id="67183e33d5c42dbf"></a>
### 기본 정보

<a id="39f6cd90d7e3d07d"></a>
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

<a id="3777eb772f331960"></a>
### 설명

Plan cache에 사용할 메모리 크기를 설정한다.

<a id="4e0c24b0d97a8dbf"></a>
## PRIVATE_STATIC_AREA_INIT_SIZE

<a id="592546b99d539d1f"></a>
### 기본 정보

<a id="d4d36ff2d3fcb582"></a>
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

<a id="295c5dfa1702cfd6"></a>
### 설명

세션이 사용할 heap 메모리의 최초 크기를 설정한다. 세션에서 사용되지 않는 메모리가 생기더라도 이 메모리들이 운영체제로 반환되지는 않는다.

<a id="ef319c1454eda309"></a>
## PRIVATE_STATIC_AREA_NEXT_SIZE

<a id="38c24fd5565b074a"></a>
### 기본 정보

<a id="b1164c675a664fa0"></a>
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

<a id="495821518656e364"></a>
### 설명

세션에서 heap 메모리를 추가적으로 할당할 때, 확장될 메모리 크기를 설정한다.

<a id="0bd836a0e8e983be"></a>
## PRIVATE_STATIC_AREA_SHRINK_THRESHOLD

<a id="d0e831d548c92fba"></a>
### 기본 정보

<a id="971fc2e8954d76eb"></a>
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

<a id="b182412dd56383ef"></a>
### 설명

세션에서 사용하지 않는 heap 메모리가 생기더라도 이 크기만큼의 메모리를 유지하며 시스템에 반환하지 않고 세션 내에서 재사용한다.

PRIVATE_STATIC_AREA_INIT_SIZE보다 작게 설정하더라도 그 크기보다 작아지지 않는다.

<a id="aca98e8e7e220b62"></a>
## PRIVATE_STATIC_AREA_SIZE

<a id="db188cd0de77ca19"></a>
### 기본 정보

<a id="cb1b75314a706df0"></a>
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

<a id="2bc47cd9b54fc32f"></a>
### 설명

세션에서 할당할 수 있는 최대 heap 메모리 크기를 지정한다.

<a id="5ab3f3ff45962883"></a>
## PROCESS_MAX_COUNT

<a id="09fef03468d9b834"></a>
### 기본 정보

<a id="77fff03788381124"></a>
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

<a id="f25752c602f82d51"></a>
### 설명

시스템에서 사용할 수 있는 최대 프로세스 (thread) 개수를 지정한다.

시스템 프로세스 생성  
• D/A 또는 C/S dedicated 모드로 접속할 때마다 프로세스가 생성된다.  
• C/S shared 모드는 기본적인 balancer, dispatcher, shared-server가 프로세스이고 client에서 접속할   
&nbsp;&nbsp;때는 프로세스가 생성되지 않는다.

<a id="257e442bb175a1c9"></a>
## QUERY_TIMEOUT

<a id="ea7f0959422c07a8"></a>
### 기본 정보

<a id="eb1da1c807c9902c"></a>
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

<a id="8e94c9431f4213ea"></a>
### 설명

세션에서 받은 명령어를 처리할 수 있는 최대 시간을 지정하며 만약 해당 시간을 초과하면 TIMEOUT 에러가 발생한다.

- 0: 무한 대기를 의미하며 TIMEOUT 에러가 발생하지 않는다.

<a id="8c83bf9e4b20c615"></a>
## READABLE_ARCHIVELOG_DIR_COUNT

<a id="902fd88c097cc0e2"></a>
### 기본 정보

<a id="e7a3551845fe4da0"></a>
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

<a id="41a72d2a246613da"></a>
### 설명

미디어 복구 시 archive redo log가 존재하는 디렉토리의 개수를 설정한다.

<a id="17e76fcf5a378bb0"></a>
## READABLE_BACKUP_DIR_COUNT

<a id="2d4426ee3cafaff7"></a>
### 기본 정보

<a id="e7692f7faae62fec"></a>
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

<a id="d946a35cd1ae9736"></a>
### 설명

증분 백업을 이용하여 파일을 복원할 때 증분 백업이 존재하는 디렉토리의 개수를 설정한다.

<a id="4846d594c8f2f1c8"></a>
## REBALANCE_BLOCK_READ_COUNT

<a id="08173363f9127b3c"></a>
### 기본 정보

<a id="d00e21b7d1960d6a"></a>
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

<a id="651076e9ced5d1c9"></a>
### 설명

Rebalance 하기 위해 block을 읽어들이는 횟수이다.

<a id="f56b87ee49060e5d"></a>
## RECOMPILE_CHECK_MINIMUM_PAGE_COUNT

> 3.1 이후로 지원하지 않는다.

<a id="a9cbdf55a3f60657"></a>
### 기본 정보

<a id="66303a99d7cf95a0"></a>
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

<a id="1f96bec71069811e"></a>
### 설명

Page count 변경에 의해 plan이 recompile 되었는지 여부를 체크하기 위해 minimum page count를 설정한다.

<a id="26323f549ffae9be"></a>
## RECOMPILE_PAGE_PERCENT

> 3.1 이후로 지원하지 않는다.

<a id="25681535143f38d0"></a>
### 기본 정보

<a id="2ae7eaf2c334e1b7"></a>
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

<a id="b59eacffd60ecdf9"></a>
### 설명

Page count가 변경되어 plan을 recompile 할 때의 page percentage를 설정한다. 이 값이 0인 경우 page count 변경에 따른 recompile을 하지 않는다.

<a id="3835c7855612ddba"></a>
## RECOVERY_LOG_BUFFER_SIZE

<a id="1ca567accc88457a"></a>
### 기본 정보

<a id="23626cd9cf5227a5"></a>
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

<a id="34308516290fb3d6"></a>
### 설명

복구를 위한 기본 log buffer 크기이다.

<a id="304a84aea67996e1"></a>
## RECYCLEBIN

<a id="fe0e1b0c0acb38de"></a>
### 기본 정보

<a id="0b23e415dc4e1738"></a>
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

<a id="e0b13952343db18e"></a>
### 설명

휴지통 기능을 활성화할지 여부를 설정한다.

<a id="f84f432b4708656a"></a>
## REDO_LOG_COMPRESSION_THRESHOLD

<a id="71c93a95d9c4b208"></a>
### 기본 정보

<a id="cec5096bad1f17a4"></a>
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

<a id="f0e08447d18377c5"></a>
### 설명

생성된 REDO LOG의 크기가 REDO_LOG_COMPRESSION_THRESHOLD 값보다 클 경우, REDO LOG를 압축한다.

<a id="b35a8cc689672ad7"></a>
## REFINE_RELATION

<a id="105f3dd3de35406d"></a>
### 기본 정보

<a id="105641d67541d650"></a>
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

<a id="493bbe245461f452"></a>
### 설명

이 속성을 NO로 하면 서버를 재시작할 때 REFINE RELATION 과정을 수행하지 않는다.

해당 프로퍼티는 REFINE RELATION 도중에 문제가 발생한 경우에 사용할 수 있으며 삭제되었지만 REFINE 하지 못한 RELATION (테이블이나 인덱스)들의 공간은 재사용할 수 없다. 문제를 해결한 이후 해당 프로퍼티를 YES로 설정하고 재시작하면 삭제하지 못했던 RELATION들에 대해 REFINE을 시도한다.

<a id="27ca012b7c47898a"></a>
## SESSION_FATAL_BEHAVIOR

<a id="9a7fd3073c316133"></a>
### 기본 정보

<a id="48d7cc4c1cea1fa2"></a>
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

<a id="8027d463ddc81c83"></a>
### 설명

Session fatal이 발생할 때 fatal을 유발한 thread만 종료시킬지 아니면 프로세스 자체를 종료시킬지 결정한다.

- 0: Fatal을 유발한 thread만 종료한다.
- 1: 프로세스를 종료한다. 해당 프로세스 내에 다수의 세션이 동시에 수행되고 있다면 모든 세션들이 데이터베이스 사용을 끝낸 후에 프로세스를 종료한다.

<a id="98280028b8506176"></a>
## SESSION_MEMORY_INIT_SIZE

<a id="eba13bea0ecbe6c3"></a>
### 기본 정보

<a id="42c9ada73e462505"></a>
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

<a id="4166da873b693b71"></a>
### 설명

세션에서 사용할 공유 메모리를 미리 할당할 크기를 설정한다.

<a id="1bc9edddd6cc8938"></a>
## SESSION_MEMORY_SHRINK_THRESHOLD

<a id="580d38f362e762bb"></a>
### 기본 정보

<a id="4a2462a2274b0bba"></a>
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

<a id="0b483b71f9dcd9fc"></a>
### 설명

세션에서 사용한 동적 공유 메모리를 해제할 때 세션에서 사용하지 않는 동적 공유 메모리를 시스템에 반납할지 여부를 판단하기 위한 경계값을 설정한다. 즉, 사용하지 않는 메모리 중 설정된 값보다 큰 크기의 메모리 청크가 있으면 시스템에 반납한다.

<a id="d6d5d6d257ee942f"></a>
## SHARED_MEMORY_ADDRESS

<a id="003f56ad222675fa"></a>
### 기본 정보

<a id="9c2c914d0a9cdd28"></a>
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

<a id="6edf2cb3525a7747"></a>
### 설명

Shared Static Area (SSA)의 주소를 지정한다.

<a id="746000a2b592d37c"></a>
## SHARED_MEMORY_STATIC_KEY

<a id="c9b43f0ed8f43a9d"></a>
### 기본 정보

<a id="d0de60cd020794db"></a>
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

<a id="ebcb65fc6c70033d"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory key 값을 지정한다.

<a id="8d62e268cf1f99e6"></a>
## SHARED_MEMORY_STATIC_NAME

<a id="bd6459d57ea31074"></a>
### 기본 정보

<a id="42e56dc34bef9a93"></a>
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

<a id="f7ab996c666f2d60"></a>
### 설명

서버를 구동할 때 Shared Static Area (SSA) 공간을 할당하면서 사용되는 shared memory name을 지정한다.

<a id="7a7e11988a1247ab"></a>
## SHARED_MEMORY_STATIC_SIZE

<a id="edbe6555935f9af1"></a>
### 기본 정보

<a id="8c91ea8c6ca11a5e"></a>
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

<a id="8b151f63fa39f5c3"></a>
### 설명

Shared Static Area (SSA)의 크기를 지정한다.

<a id="41ecb867cf90587b"></a>
## SHARED_REQUEST_QUEUE_COUNT

<a id="4380eb9227fd8944"></a>
### 기본 정보

<a id="de2dc734780af8bd"></a>
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

<a id="fe4a60c4ddb0a298"></a>
### 설명

Shared 모드의 dispatcher에서 shared-server로 요청하는 queue 개수를 설정한다. 여러 dispatcher가 사용자의 작업 요청을 shared-server에 할당할 때 사용하는 queue로써 일반적으로 load-balance를 위해 하나를 사용한다. 그러나 dispatcher와 shared-server가 많아지면 queue에 경합이 발생하여 성능이 저하될 수 있으므로 이 값을 늘려서 사용한다. 이 값이 커지면 load-balance가 비효율적으로 될 수 있고 dead-lock이 발생할 가능성이 커진다.

<a id="5b6410a318162726"></a>
## SHARED_SERVERS

<a id="16678ab573387e74"></a>
### 기본 정보

<a id="b96bb69107c54597"></a>
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

<a id="43ccd158f0dcec00"></a>
### 설명

Shared 모드에서 shared-server process 개수를 설정한다.  
Open 단계에서는 alter system으로 값을 줄일 수 없다.

<a id="779f7497941bca6e"></a>
## SHARED_SESSION

<a id="0139ee4ba4822e8b"></a>
### 기본 정보

<a id="a301bf4913e4d711"></a>
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

<a id="fd3d236c373b065f"></a>
### 설명

Shared 모드를 활성화할지 여부를 설정한다. 이 값을 NO로 설정하면 load-balancer (gbalancer), dispatcher (gdispatcher), shared-server (gserver)가 실행되지 않는다.

<a id="3ed5e9c7c1c9d03b"></a>
## SNAPSHOT_STATEMENT_TIMEOUT

<a id="5d2e97572a55a16f"></a>
### 기본 정보

<a id="0bfb01fdb473ba10"></a>
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

<a id="91da8298081c66e1"></a>
### 설명

Snapshot read가 필요로 하는 statement의 최대 유지 시간을 설정한다. 설정된 시간을 초과한 snapshot statement들에는 TIMEOUT 에러가 발생한다.

<a id="abcd818cc9b01587"></a>
## SQL_HISTORY_SIZE

<a id="c32af25267f35f9b"></a>
### 기본 정보

<a id="21a4cfa04bfe794d"></a>
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

<a id="3ab01f01a81add51"></a>
### 설명

SQLs의 이력 (history) 크기이다.

<a id="9d5fb6ed39653793"></a>
## SQL_HISTORY_TYPE

<a id="9842ad49a22811c8"></a>
### 기본 정보

<a id="a208bfea9a2e93e4"></a>
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

<a id="431b412e4ac336e3"></a>
### 설명

SQLs의 이력 (history) 타입이다.

- 0: Direct-execute
- 1: Prepare-execute
- 2: All

<a id="f8bdd3e05bcc8de7"></a>
## SUPPLEMENTAL_LOG_DATA_PRIMARY_KEY

<a id="70fb0e5f7bbd8e44"></a>
### 기본 정보

<a id="648e97ae05f861a4"></a>
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

<a id="51a1b1ab5fa3983a"></a>
### 설명

Database 내의 모든 변경 내용에 대한 supplemental log를 기록한다.

<a id="9605699e2c1952d0"></a>
## SYSTEM_DISK_DATA_TABLESPACE_SIZE

<a id="7f621687ba045a25"></a>
### 기본 정보

<a id="de368f56990732f0"></a>
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

<a id="df66c6b4f53355d7"></a>
### 설명

데이터베이스를 생성할 때 초기 DISK_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="972f1ab2635a449c"></a>
## SYSTEM_FILE_IO

<a id="ccffac2afafe4088"></a>
### 기본 정보

<a id="8904897b7c39d1b3"></a>
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

<a id="a324ea01ad1eb731"></a>
### 설명

데이터 파일과 로그 파일을 제외한 데이터베이스 파일을 사용할 때 IO 타입을 설정한다.

<a id="6aafad5f176b6b42"></a>
## SYSTEM_LOGGER_DIR

<a id="819d7f2605a6b27b"></a>
### 기본 정보

<a id="352e63287ed2cbce"></a>
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

<a id="27d4240beed71052"></a>
### 설명

Trace 로그 메시지가 기록되는 디스크 경로를 지정한다.

<a id="6b168c18d9e8e274"></a>
## SYSTEM_MEMORY_AUX_TABLESPACE_SIZE

<a id="0b3f16a84be79fbc"></a>
### 기본 정보

<a id="b903846249d5a57d"></a>
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

<a id="0a9ec541ea2d536a"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_AUX_TBS 테이블스페이스 크기를 결정한다.

<a id="d5c5acff0e0cb493"></a>
## SYSTEM_MEMORY_DATA_TABLESPACE_SIZE

<a id="31fb4cc6a962c60e"></a>
### 기본 정보

<a id="19f2834a5ffa7533"></a>
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

<a id="7813816fb276bca1"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_DATA_TBS 테이블스페이스 크기를 결정한다.

<a id="7676b18fa1042993"></a>
## SYSTEM_MEMORY_DICT_TABLESPACE_SIZE

<a id="f2ffe2029fd3eab2"></a>
### 기본 정보

<a id="c796f2478ecbfae8"></a>
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

<a id="45ca7be0a3686adc"></a>
### 설명

데이터베이스를 생성할 때 초기 DICTIONARY_TBS 테이블스페이스의 크기를 결정한다.

<a id="c71574138874e68b"></a>
## SYSTEM_MEMORY_TEMP_TABLESPACE_SIZE

<a id="e61117a02e1010fc"></a>
### 기본 정보

<a id="2cc3fa4037aaf0cb"></a>
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

<a id="cf3b47a6d3df55c6"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_TEMP_TBS 테이블스페이스의 크기를 결정한다.

<a id="f94942d4541245fe"></a>
## SYSTEM_MEMORY_UNDO_TABLESPACE_SIZE

<a id="5ce711220235c9cd"></a>
### 기본 정보

<a id="5d9491d6adc3590a"></a>
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

<a id="db5b6cec3579af34"></a>
### 설명

데이터베이스를 생성할 때 초기 MEM_UNDO_TBS 테이블스페이스의 크기를 결정한다.

<a id="8b183148e850c2a6"></a>
## SYSTEM_TABLESPACE_DIR

<a id="370d4ba71f8beed6"></a>
### 기본 정보

<a id="7211ddaf700e1706"></a>
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

<a id="978ac074c8bebebb"></a>
### 설명

데이터베이스를 생성할 때 초기 시스템 테이블스페이스들이 저장되는 경로를 지정한다.

<a id="b05287f88b7f8827"></a>
## SYSTEM_UDS_DIR

<a id="fd617a343e30e61d"></a>
### 기본 정보

<a id="8369ab3dd1ed22c1"></a>
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

<a id="ff80f73cafc68f50"></a>
### 설명

Unix domain socket 파일이 생성되는 directory를 설정한다.  
DB system 이외에 glsnr 등과 같은 unix domain socket에 대한 디렉토리 설정은 별도의 configuration file에서 관리된다.  
최대 설정 크기는 60 byte이다. (Unix domain socket 파일의 절대 경로 (디렉토리 + 파일 이름)의 최대 크기는 OS마다 다르지만 보통 100 byte 내외이다.)

<a id="b358b149376ec805"></a>
## TCP_CLIENT_NUMA_NODE

<a id="79f55042f565472d"></a>
### 기본 정보

<a id="506f674081e0477d"></a>
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

<a id="974bb8389cefb7fb"></a>
### 설명

Client server 세션이 바인드 될 NUMA 노드 ID를 설정한다. 해당 프로퍼티는 NUMA 프로퍼티가 on으로 설정된 경우에 작동한다.

<a id="37946b333329004e"></a>
## TCP_NODELAY

<a id="93642291b0a5a3d3"></a>
### 기본 정보

<a id="b629dd0645ded169"></a>
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

<a id="0bd4a5ed9ed88f03"></a>
### 설명

C/S 방식 (TCP socket)으로 client에 data를 전송할 때의 socket TCP_NODELAY 옵션을 설정한다.  
빠른 latency가 필요하지 않고 network 부하를 줄이고 싶은 경우에는 NO로 설정한다.

<a id="7963d1d1b5e036c4"></a>
## TEMP_SEGMENT_CACHE_SIZE

<a id="bd35c09a280f2a3d"></a>
### 기본 정보

<a id="c025e2b407a6d1ff"></a>
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

<a id="02298feeab42143a"></a>
### 설명

Global temporary table이나 global temporary index segment가 drop 될 때 tablespace에 반납하지 않고 session에서 caching 할 segment 개수를 지정한다. Segment cache에 존재하는 segment는 향후 global temporary table이나 global temporary index에서 재사용된다.

- 0: Session에서 global temporary table이나 global temporary index의 segment cache를 사용하지 않는다.
- 1 ~ 4294967295: Session에서 global temporary table이나 global temporary index의 segment cache를 주어진 개수만큼 유지한다.

<a id="0d74812f0418d18a"></a>
## TEMP_UNDO_ENABLED

<a id="8795ca122593de5b"></a>
### 기본 정보

<a id="dd2641029d1e4ab8"></a>
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

<a id="5a952e8c2a7499c4"></a>
### 설명

Global temporary table에 대한 undo 레코드의 로깅 위치를 지정한다.

- 0 (FALSE): 데이터베이스의 기본 undo tablespace에 undo 레코드를 기록한다.
- 1 (TRUE): 데이터베이스의 기본 temporary tablespace에 undo 레코드를 기록한다.

<a id="225fcacce2a5fd43"></a>
## TIMED_STATISTICS

<a id="dca30ff967cfc0cd"></a>
### 기본 정보

<a id="cbfd6dd6b14ed50f"></a>
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

<a id="58613b17d2010407"></a>
### 설명

Wait event를 측정하는지 여부이다.  
v$system_event, v$session_event, v$session_wait table에 wait event와 관련된 통계 기록을 남기고 싶은 경우에 설정한다.

- 0: 통계 기록을 남기지 않는다.
- 1: 통계 기록을 남긴다.
- 2: High precision timer를 이용하여 통계 기록을 남긴다.

<a id="f4bfb7782bcbfef3"></a>
## TIMEZONE

<a id="7eeefe7c42b4bbf7"></a>
### 기본 정보

<a id="f6266fa939dbec0a"></a>
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

<a id="c82ee309c2adb5e7"></a>
### 설명

Database의 time zone 값이다.  
Database가 생성될 때 적용되는 속성으로써 -14:00 ~ +14:00 범위의 값을 사용할 수 있다.

<a id="e0801e1e08857da3"></a>
## TRACE_ALTER_SYSTEM

<a id="2d7b1f280872ba1e"></a>
### 기본 정보

<a id="0e217f2ec01addf1"></a>
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

<a id="8994465005fc8cde"></a>
### 설명

ALTER SYSTEM 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

시스템 변경에 대한 기록을 남기려면 TRACE_ALTER_SYSTEM 프로퍼티를 ON으로 설정한다.  

TRACE_ALTER_SYSTEM 프로퍼티는 SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="2977b3b5d2103ed1"></a>
## TRACE_DDL

<a id="ae545e290da62312"></a>
### 기본 정보

<a id="d404d168d6f9895c"></a>
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

<a id="f2e127498b092c6c"></a>
### 설명

Data Definition Language (DDL) 구문을 실행할 때 해당 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.  

테이블 생성, 삭제, 변경 등과 같은 SQL 문을 실행했을 때 이에 대한 기록을 남기려면 TRACE_DDL 프로퍼티를 ON으로 설정한다.  

TRACE_DDL 프로퍼티는 DDL 구문 수행에만 영향을 주며, SELECT 질의, INSERT, UPDATE, DELETE 등의 구문 수행과는 무관하므로 성능에 영향을 주지 않는다.

<a id="20650666e7a79521"></a>
## TRACE_LOG_ID

<a id="3abece5c5de07402"></a>
### 기본 정보

<a id="f36da3245a8b98bd"></a>
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

<a id="b452b28c0008b649"></a>
### 설명

질의를 수행할 때 해당 질의에 대한 실행 계획 정보와 기타 정보를 trace directory(&lt;GOLDILOCKS_DATA&gt;/trc/) 아래에 있는 trace file (opt_p[프로세스ID]_s[세션ID].trc)에 기록한다.

질의에 대한 SQL 구문과 실행 계획, 수행시간 등에 대한 기록을 남기려면 아래 표의 flag 정보를 조합하여 설정한다.

**TRACE_LOG_ID에 대한 flag 정보**

<a id="f62aac5d8d72598a"></a>
| 정보 | Flag(on) | Flag(off) |
| --- | --- | --- |
| 성공한 SQL 질의 출력 여부 | 100000 | 0 |
| 실패한 SQL 질의 출력 여부 | 10000 | 0 |
| 실행 계획 출력 여부 | 1000 | 0 |
| 실행 형태 (direct/prepare) 출력 여부 | 100 | 0 |
| Bind 값 출력 여부 | 10 | 0 |
| 구간별 수행시간 출력 여부 | 1 | 0 |

만약 "성공한 SQL 질의 출력" + "실행 계획 출력" + "Bind 값 출력" 하려면 TRACE_LOG_ID 값을 101010으로 설정한다.

<a id="738b436bd25feaf4"></a>
## TRACE_LOG_MSGBUF_SIZE

<a id="9dbc8e9af3eaa6f1"></a>
### 기본 정보

<a id="12418280aa8eb492"></a>
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

<a id="33aa46b589380dd3"></a>
### 설명

Trace logfile에 기록할 log message를 구성하는데 사용되는 heap memory buffer의 크기를 설정한다.

<a id="324e76497490eb47"></a>
## TRACE_LOG_TIME_DETAIL

<a id="b1270b68bcd1afe4"></a>
### 기본 정보

<a id="186610158dcedb7b"></a>
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

<a id="1ab4a04265e55a54"></a>
### 설명

Trace log를 기록할 때 시간 정확도를 높일지 여부를 설정한다.  
이 값이 OFF로 설정된 경우, 10 ms의 정확도를 가지며, ON으로 설정된 경우 1 us의 정확도를 가진다.

<a id="ea8acb763a825a70"></a>
## TRACE_LOGGER

<a id="6a23fef555506bab"></a>
### 기본 정보

<a id="232d1df40dba9fd3"></a>
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

<a id="c0359b36c1409c60"></a>
### 설명

Trace log를 기록할 대상을 설정한다.  
1이면 file에 기록하고 2이면 remote로 파일에 기록한다.  
Remote로 기록하면 gtrclogger에서 원격으로 trace log를 수집하여 파일에 기록한다.

<a id="42f5a242eed8733a"></a>
## TRACE_LOGGER_REMOTE_HOST

<a id="2ce3c3d51ca68e75"></a>
### 기본 정보

<a id="ca3e6dbc478d8f6b"></a>
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

<a id="526a2b26ad195234"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 host를 설정한다.

<a id="853742fab0399708"></a>
## TRACE_LOGGER_REMOTE_PORT

<a id="e4b63281c3eb7552"></a>
### 기본 정보

<a id="ec767d341ba97d66"></a>
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

<a id="c1ee9756de271a71"></a>
### 설명

TRACE_LOGGER를 2로 설정하여 remote로 trace log를 전송할 port를 설정한다.

<a id="198d90f5c5250db0"></a>
## TRACE_LOGIN

<a id="a023227d2d22c249"></a>
### 기본 정보

<a id="2d704a56c8f2c16e"></a>
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

<a id="6686347cef0c9090"></a>
### 설명

로그인 할 때 해당 접속 정보를 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/login.trc)에 기록한다.  
로그인 할 때 이에 대한 기록을 남기려면 TRACE_LOGIN 프로퍼티를 ON으로 설정한다.

<a id="1132cf1f05fbce81"></a>
## TRACE_LONG_RUN_CURSOR

<a id="e35ed391e5e6b98c"></a>
### 기본 정보

<a id="a8b89917019aa3bb"></a>
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

<a id="5d17f1af3d59270e"></a>
### 설명

Cursor의 lifetime이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 정확한 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#d616832efbabdbc3) 프로퍼티를 사용한다.

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

<a id="112960eef58f0ddc"></a>
## TRACE_LONG_RUN_SQL

<a id="0e0d30f69311d53d"></a>
### 기본 정보

<a id="1b480ca9f87852fa"></a>
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

<a id="a08030b10333e43e"></a>
### 설명

구문의 수행시간이 프로퍼티에 지정된 시간보다 긴 SQL 문장을 trace file (&lt;GOLDILOCKS_DATA&gt;/trc/system.trc)에 기록한다.

- 값의 의미
    - 단위: millisecond
    - 0 값: 정보를 기록하지 않는다.
    - 권장값: 20 (millisecond) 이상
    - 10 ms 주기의 time tic을 이용하여 수행시간을 측정하므로 20 이상의 값을 권장한다.
    - 보다 정확한 정밀도를 위해서는 [TRACE_LONG_RUN_TIMER](#d616832efbabdbc3) 프로퍼티를 사용한다.

- 수행시간이 1초 이상인 SQL 구문을 기록한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL = 1000;
```

- 기본값으로 복원한다.

```
gSQL> ALTER SYSTEM SET TRACE_LONG_RUN_SQL TO DEFAULT;
```

<a id="d616832efbabdbc3"></a>
## TRACE_LONG_RUN_TIMER

<a id="c5a11954a03894c5"></a>
### 기본 정보

<a id="fdaaa731dd522a66"></a>
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

<a id="7112d85b6c1a6f64"></a>
### 설명

다음 프로퍼티들을 이용하여 SQL 구문의 실행시간을 측정할 때 측정 정밀도를 제어한다.

- [TRACE_LONG_RUN_CURSOR](#1132cf1f05fbce81)
- [TRACE_LONG_RUN_SQL](#112960eef58f0ddc)

- 값의 의미
    - 0: 10 millisecond의 interval을 가지는 timer thread를 사용한다.
    - 1: gettimeofday() 함수를 이용하여 시간을 측정한다. 정밀도는 높지만 system call로 인한 부하가 있다.

<a id="ad61cb83e9ed0304"></a>
## TRACE_XA

<a id="928790978a9c8eec"></a>
### 기본 정보

<a id="ef42bce5638fe5d8"></a>
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

<a id="1b4e9839f6cdc510"></a>
### 설명

XA 인터페이스를 사용할 때 추적 메세지를 출력할지 여부를 지정한다. 메세지는 'SYSTEM_LOGGER_DIR/xa.trc'에 출력된다.

<a id="b56d7130e9cfff6e"></a>
## TRANSACTION_ALLOCATION_TIMEOUT

<a id="59ddcb9b0c6f09b3"></a>
### 기본 정보

<a id="5cb0db52e0ad3078"></a>
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

<a id="763ab493fb74d257"></a>
### 설명

Transaction slot을 할당할 때의 최대 대기 시간이다.

대기 시간이 TRANSACTION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14129): transaction allocation time exceeded
```

<a id="f199bfb9103ec010"></a>
## TRANSACTION_COMMIT_WRITE_MODE

<a id="7300ad910d4ee8cb"></a>
### 기본 정보

<a id="2376cb49c096999c"></a>
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

<a id="3b582d10151daaf4"></a>
### 설명

TRANSACTION_COMMIT_WRITE_MODE는 트랜잭션이 완료될 때 트랜잭션이 생성한 log를 disk log file에 flush할지 여부를 설정한다. 즉, TRANSACTION_COMMIT_WRITE_MODE가 '1'이면 log를 트랜잭션 완료 시점에 disk log file에 flush해야 하고, 그렇지 않은 경우 log flush 여부와 관계없이 트랜잭션을 완료한다.

만약 TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정하여 시스템을 운용하는 경우에 트랜잭션을 COMMIT 한 후 log flush가 되지 않은 상태에서 GOLDILOCKS가 비정상적으로 종료되면 기록되지 않은 log로 인해 최신 data를 잃어버리게 된다.

따라서 모든 트랜잭션이 완료되었을 때 반드시 database에 남아 있어야 하는 경우 TRANSACTION_COMMIT_WRITE_MODE를 '1'로 설정하여 시스템을 운용하거나, TRANSACTION_COMMIT_WRITE_MODE를 '0'으로 설정한 후 트랜잭션이 완료되는 시점에 명시적으로 'ALTER SYSTEM FLUSH LOGS' 문을 수행하여 log를 flush해야 한다.

- 0: no wait
- 1: wait

<a id="dd04aa210a6bf284"></a>
## TRANSACTION_MAXIMUM_UNDO_PAGE_COUNT

<a id="a1e8859ad4b5c25b"></a>
### 기본 정보

<a id="e050e3bfc2a9f975"></a>
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

<a id="bb488c7e316f78f2"></a>
### 설명

트랜잭션이 기록할 수 있는 최대 undo 페이지 개수를 의미한다. 최소값은 1로 8 Kbyte이며, 최대값은 13107200으로 100 Gbyte이다.

<a id="46588d3be98b8298"></a>
## TRANSACTION_TABLE_SIZE

<a id="269e662ebbdc8eab"></a>
### 기본 정보

<a id="eb8ca887a56e7741"></a>
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

<a id="ea37526a13009af5"></a>
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

<a id="a9ff18a9fb143835"></a>
## TRANSACTION_TIMEOUT

<a id="0b9a367bff9467e0"></a>
### 기본 정보

<a id="b0cf31aeb70c931f"></a>
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

<a id="b75a0e23e93dd6ad"></a>
### 설명

Transaction이 활성화되어 있는 시간을 설정한다. Transaction이 장시간 활성화되어 있을 때 발생할 수 있는 부작용을 예방하기 위해 사용된다. 정해진 시간을 초과한 transaction이 있을 경우, gmaster 데몬이 해당 transaction을 소유한 세션을 자동으로 종료시킨다.

<a id="3ac07853b4055a71"></a>
## UNDO_RELATION_ALLOCATION_TIMEOUT

<a id="b72f23fd00f9c3d0"></a>
### 기본 정보

<a id="f1785b9cff6cce00"></a>
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

<a id="038c0295b6bec531"></a>
### 설명

Undo relation을 할당할 때의 최대 대기 시간이다.

대기 시간이 UNDO_RELATION_ALLOCATION_TIMEOUT을 초과할 경우 다음과 같은 에러가 발생한다.

```
gSQL> insert into t1 values(1);

ERR-HYT00(14130): undo relation allocation time exceeded
```

<a id="0f92476ebbf61fbf"></a>
## UNDO_RELATION_COUNT

<a id="ff302c56627a8ac2"></a>
### 기본 정보

<a id="c4b9dcab801c4c9c"></a>
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

<a id="092052e50e824553"></a>
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

<a id="f050e2e01cd76441"></a>
## UNDO_SHRINK_THRESHOLD

<a id="5cba58da00800031"></a>
### 기본 정보

<a id="84d9db9596dac752"></a>
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

<a id="ab8bcab57372c0f9"></a>
### 설명

Ager thread는 주기적으로 (10초) undo segment의 공간을 검사하여 공간을 많이 차지하고 있을 경우, 일부분을 테이블스페이스로 반환한다. 이 프로퍼티는 한 번에 반환해야 할 바이트 단위의 크기를 의미한다.

<a id="0dc500429d1dfbc0"></a>
## USE_LARGE_PAGES

<a id="e0758e8e72fa32f2"></a>
### 기본 정보

<a id="8e2d5e2b0ac7ce96"></a>
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

<a id="0e78a24ce48597d6"></a>
### 설명

HugePage를 사용한다. USE_LARGE_PAGES를 사용하려면 먼저 장비에 HugePage를 설정해야 한다.

- 0: Large page를 사용하지 않는다.
- 1: Large page를 사용한다. 만약 공유 메모리 할당에 실패할 경우에는 에러가 발생한다.
- 2: Large page를 사용하여 할당을 시도한다. 만약 공유 메모리 할당에 실패할 경우에는 regular page를 사용하여 메모리를 할당한다.

> 리눅스 커널 2.6.32-573 이상에서만 사용할 수 있다.

<a id="ac6ec7fa9db4e073"></a>
## USER_DATA_TABLESPACE_MEDIA_TYPE

<a id="27eeb03be0318f19"></a>
### 기본 정보

<a id="a4d1340f7f9eeb43"></a>
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

<a id="da3b53f04031f84a"></a>
### 설명

사용자 데이터 테이블스페이스를 생성할 때 테이블스페이스의 media 타입이 생략된 경우, default media 타입을 지정한다. 0은 memory, 1은 disk를 의미한다.

<a id="d983d67a71231b74"></a>
## USER_DATA_TABLESPACE_SIZE

<a id="0b4de326eaf97a89"></a>
### 기본 정보

<a id="69c40db014f6073b"></a>
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

<a id="b09927617b3cf429"></a>
### 설명

사용자 데이터 테이블스페이스가 생성되거나 데이터 파일이 추가될 때 데이터 파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="de868894b7d8c5a5"></a>
## USER_DISK_DATA_TABLESPACE_NEXTSIZE

<a id="82e9ced817f5e6a7"></a>
### 기본 정보

<a id="1dee46e3c5afc977"></a>
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

<a id="744af2179e395384"></a>
### 설명

사용자 디스크 데이터 테이블스페이스의 데이터파일이 확장되어야 할 때 확장할 크기가 설정되지 않은 경우, default 크기를 지정한다.

<a id="dcf959182b502ba9"></a>
## USER_TEMP_TABLESPACE_SIZE

<a id="27b4192b7d602eea"></a>
### 기본 정보

<a id="69613cc08a164591"></a>
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

<a id="bd69438e0e1f33e0"></a>
### 설명

사용자 temp 테이블스페이스가 생성되거나 데이터파일이 추가될 때 데이터파일의 크기가 생략된 경우, default 크기를 지정한다.

<a id="988e5560c480f7c7"></a>
## XA_TRANSACTION_IDLE_TIMEOUT

<a id="e8fed93e031f5a0f"></a>
### 기본 정보

<a id="56953b1e298118c2"></a>
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

<a id="9bb876198d1f5e52"></a>
### 설명

Xa transaction이 idle 상태 (XA가 시작된 후 다음 처리가 발생할 때까지 시간)로 대기할 수 있는 최대 시간이다. Idle 상태로 대기하다가 이 시간을 초과하면 xa transaction은 rollback 된다.

0으로 설정하면 XA가 idle 상태로 있더라도 무한 대기한다.

---

[← 9. Database Information](9-database-information.md) · [전체 목차](../README.md) · [11. SQL Elements →](../part-03-sql-manual/11-sql-elements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
