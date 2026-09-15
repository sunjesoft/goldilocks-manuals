<a id="8891badaec80f9ff"></a>

# 8. GOLDILOCKS 데이터베이스 이중화

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/8891badaec80f9ff)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 7. GOLDILOCKS 데이터베이스의 백업과 복구](7-goldilocks-데이터베이스의-백업과-복구.md) · [전체 목차](../README.md) · [9. Database Information →](9-database-information.md)

<a id="f592397250ad8fce"></a>
## 이중화 소개

본 장에서는 CYCLONE과 LOGMIRROR에 대해 설명한다.

GOLDILOCKS의 이중화는 CDC 방식을 사용하여 transaction을 이중화하는 CYCLONE과 원본 데이터베이스의 redo log file을 이중화하는 LOGMIRROR를 지원한다.

**이중화 tool 소개**

<a id="28228a87ecfb9216"></a>
| 이름 | 이중화 대상 | 설명 |
| --- | --- | --- |
| CYCLONE | Transaction | CDC 방식을 사용하여 master에 반영된 transaction을 이중화하여 slave에 반영한다. |
| LOGMIRROR | Redo log file | Master 데이터베이스의 redo log file을 slave에 동일하게 이중화한다. |

- CYCLONE
    - Change Data Capture (CDC) 방식으로 원본 데이터베이스의 redo log file을 분석하고 가공하여 원격 데이터베이스에 적용한다.
    - 데이터베이스의 redo log file에 저장된 내용을 분석하기 때문에 비동기 (async) 방식만 지원한다.
- LOGMIRROR
    - 원본 데이터베이스에 저장되는 redo log file을 원격지에 이중화한다.
    - 비동기 방식으로 동작하는 CYCLONE의 데이터 손실을 방지하기 위해 수행된다.

<a id="7e9a9928b90e8770"></a>
## 운영 방법

<a id="45b8ed13a2c1926d"></a>
### CYCLONE

일반적인 운영 방법과 옵션에 대한 자세한 내용은 [CYCLONE](../part-07-replication/44-cyclone.md#6cfc1d93d791dbe7)을 참조한다.

<a id="6e948e7a827e2023"></a>
#### 노드 추가와 삭제

CYCLONE은 group 단위로 수행되며 이는 이중화 노드와 동일하다. 만약 노드를 추가할 경우에는 group을 추가하고 삭제할 경우에는 group을 삭제하도록 한다.

<a id="fabeab7ac19cad2d"></a>
##### 노드 추가 예

- 추가하려는 group 2를 master 환경 파일에 기록한다.
    - 그룹마다 고유의 PORT를 설정해야 한다.
    - 기본 master 환경 파일: $GOLDILOCKS_DATA/conf/cyclone.master.conf

    - 다음은 기존에 운영 중인 group 1 노드이다.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102
    CAPTURE_TABLE =
    (
        testTable1,
        testTable2
    )
}
```

    - 다음은 추가하려는 group 2 노드이다.

```
GROUP_NAME = Group2
{
    PORT = 21103
    CAPTURE_TABLE =
    (
        testTable5,
        testTable6
    )
}
```

- 추가하려는 group 2를 slave 환경 파일에 기록한다.
    - 기존에 master에 추가한 group 2의 PORT와 동일해야 한다.
    - 기본 slave 환경 파일: $GOLDILOCKS_DATA/conf/cyclone.slave.conf

    - 다음은 기존에 운영 중인 group 1 노드이다.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102    
    APPLY_TABLE = 
    (
        testTable1 To testTable3,
        testTable2 To testTable4
    )
}
```

    - 다음은 추가하려는 group 2 노드이다.

```
{
    PORT = 21103    
    APPLY_TABLE = 
    (
        testTable5 To testTable7,
        testTable6 To testTable8
    )
}
```

- 추가된 group 2 노드를 master 장비에서 실행하고 확인한다.

```
prompt> cyclone --master --start --group Group2
[GROUP2] Startup done as Master.

prompt> cyclone --master --status
======================================
|       CYCLONE STATUS - MASTER      |
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

- 추가된 group 2 노드를 slave 장비에서 실행하고 확인한다.

```
prompt> cyclone --slave --start --group Group2
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="5a416537b910df08"></a>
##### 노드 삭제 예

- 삭제하려는 group 2 노드를 slave 장비에서 종료한다.

```
prompt> cyclone --slave --stop --group Group2
stop done.

prompt> cyclone --slave --status
======================================
CYCLONE STATUS - SLAVE
======================================
GROUP1 Running...
--------------------------------------
```

- 삭제하려는 group 2 노드를 master 장비에서 종료한다.

```
prompt> cyclone --master --stop --group Group2
stop done.

prompt> cyclone --master --status
======================================
CYCLONE STATUS - MASTER
======================================
GROUP1 Running...
--------------------------------------
```

- 삭제하려는 노드인 group 2를 master 환경 파일에서 제거한다.
    - 기본 master 환경 파일: $GOLDILOCKS_DATA/conf/cyclone.master.conf

    - 다음은 기존에 운영 중인 group 1 노드이다.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102
    CAPTURE_TABLE =
    (
        testTable1,
        testTable2
    )
}
```

    - Group 2 노드를 삭제한다.

<pre><code><del>GROUP_NAME = Group2
{
    PORT = 21103
    CAPTURE_TABLE =
    (
        testTable5,
        testTable6
    )
}</del></code></pre>

- 삭제하려는 노드인 group 2를 slave 환경 파일에서 제거한다.
    - 기본 slave 환경 파일: $GOLDILOCKS_DATA/conf/cyclone.slave.conf

    - 다음은 기존에 운영 중인 group1 노드이다.

```
...
...
GROUP_NAME = Group1
{
    PORT = 21102    
    APPLY_TABLE = 
    (
        testTable1 To testTable3,
        testTable2 To testTable4
    )
}
```

    - Group 2 노드를 삭제한다.

<pre><code><del>GROUP_NAME = Group2
{
    PORT = 21103    
    APPLY_TABLE = 
    (
        testTable5 To testTable7,
        testTable6 To testTable8
    )
}</del></code></pre>

<a id="93b3b1c98a3e0df8"></a>
#### 이중화 초기화

기존에 이중화를 수행했던 노드나 그룹에 포함된 table이 DDL 수행 등의 이유로 수행을 give up 했을 경우 이중화를 초기화할 수 있다. 특정 노드 또는 전체 노드를 초기화할 수 있다.

이중화 초기화는 slave에서 수행하고 있는 이중화를 --reset 옵션을 사용하여 재시작하는 방식으로 수행한다. Master에서는 특별한 작업을 수행하지 않아도 된다.

<a id="3c62120aa02b54ee"></a>
##### 특정 노드의 이중화 초기화 예

- 초기화하려는 group 2 노드를 slave 장비에서 종료한다.

```
prompt> cyclone --slave --stop --group Group2
stop done.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
--------------------------------------
```

- --reset 옵션을 사용하여 group 2 노드를 slave 장비에서 재시작한다.
    - Master 장비에서는 특정 작업을 수행하지 않아도 된다.
    - 현재 시점부터 이중화가 재시작된다.

```
prompt> cyclone --slave --start --reset --group Group2
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="7a058696120276cc"></a>
##### 전체 노드의 이중화 초기화 예

- Slave 장비에서 운영 중인 cyclone을 모두 종료한다.

```
prompt> cyclone --slave --stop
```

- --reset 옵션을 사용하여 slave 장비에서 재시작한다.
    - Master 장비에서는 특정 작업을 수행하지 않아도 된다.
    - 현재 시점부터 이중화가 시작된다.

```
prompt> cyclone --slave --start --reset
[GROUP1] Startup done as Slave.
[GROUP2] Startup done as Slave.

prompt> cyclone --slave --status
======================================
        CYCLONE STATUS - SLAVE        
======================================
 GROUP1 Running...
 GROUP2 Running...
--------------------------------------
```

<a id="bbd0f79ad5f3141b"></a>
### LOGMIRROR

일반적인 운영 방법과 옵션에 대한 자세한 내용은 [LOGMIRROR](../part-07-replication/45-logmirror.md#a3584d4f89237bdd)를 참조한다.

<a id="63a58d715965f803"></a>
#### LOGMIRROR 상태 확인

LOGMIRROR와 연동할 경우 GOLDILOCKS는 LOGMIRROR의 응답 대기 과정을 포함한다. 만약 LOGMIRROR가 응답을 기다리고 있다면 GOLDILOCKS 역시 blocked 된 상태로 대기한다. 이런 상태는 v$system_stat에서 확인할 수 있다.

```
gSQL> SELECT * FROM V$SYSTEM_STAT WHERE STAT_NAME='LOG_MIRROR_SYNC_STATE';

STAT_NAME             STAT_VALUE COMMENTS                                     
--------------------- ------ ---------------------------------------------
LOG_MIRROR_SYNC_STATE      0 logmirror sync state( 0 : sync, 1 : blocked )


1 row selected.
```

STAT_VALUE가 '0'이면 대기 상태가 아닌 일반적인 상황이고 '1'이면 응답을 기다리는 blocked 상태이다. 응답을 기다리는 상황에서 GOLDILOCKS의 서비스를 재개할 경우, LOG_MIRROR_TIMEOUT을 변경하여 LOGMIRROR 서비스를 중단할 수 있다.

```
gSQL> ALTER SYSTEM SET LOG_MIRROR_TIMEOUT = 20;

System altered.
```

<a id="bb6a839a91ca6350"></a>
#### 이중화 초기화

LogMirror의 이중화 초기화는 수동으로 수행해야 한다. 이는 사용자가 옵션을 잘못 사용하여 데이터가 삭제되거나 복구 불능 상태가 되지 않도록 하기 위함이다.

> LOGMIRROR의 slave에는 control 파일과 redo log file이 저장되고 control 파일에는 운영에 필요한 정보가 저장 및 갱신된다.

<a id="c6583e7a8481635d"></a>
##### 이중화 초기화 예

- Slave 장비에서 운영 중인 LOGMIRROR를 종료한다.

```
prompt> logmirror --slave --stop 
stop done.
```

- Master 장비에서 운영 중인 LOGMIRROR를 종료한다.

```
prompt> logmirror --master --stop 
stop done.
```

- Slave 장비에서 이중화된 컨트롤 파일과 redo log file을 삭제한다.
    - 경로는 slave 환경 파일에 기술된 'LOG_PATH' 옵션을 참조한다.
    - 기본 LOGMIRROR slave 환경 파일: $GOLDILOCKS_DATA/conf/logmirror.slave.conf

<a id="c50a11702fc1336f"></a>
## Trace Log

Trace log에 대한 자세한 정보는 다음과 같다.

<a id="cc59bbe07a30be0d"></a>
<table class="table column_count_3"><caption> </caption><thead><tr><th class="to_center"><div>이름</div></th><th class="to_center"><div>구분</div></th><th class="to_center"><div>파일 이름</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="2"><div>CYCLONE</div></td><td class="to_left to_middle"><div>Master</div></td><td class="to_left to_middle"><div>cyclone_master_GROUP_NAME.trc</div></td></tr><tr><td class="to_left to_middle"><div>Slave</div></td><td class="to_left to_middle"><div>cyclone_slave_GROUP_NAME.trc</div></td></tr><tr><td class="to_left to_middle" rowspan="2"><div>LOGMIRROR</div></td><td class="to_left to_middle"><div>Master</div></td><td class="to_left to_middle"><div>LogMirror_master.trc</div></td></tr><tr><td class="to_left to_middle"><div>Slave</div></td><td class="to_left to_middle"><div>LogMirror_slave.trc</div></td></tr></tbody></table>

<a id="dc5777a0e4bd241c"></a>
### CYCLONE 에러 메시지와 해결 방법

다음은 CYCLONE의 에러 메시지와 해결 방법이다.

<a id="f0f88a9f90dddb82"></a>
| 에러 메시지 | 해결 방법 |
| --- | --- |
| Service is not available | GOLDILOCKS가 정상적으로 실행되어 있는지 확인한다. |
| table does not exist | 환경 파일에 기술한 table 이름을 확인한다. |
| schema does not exist | 환경 파일에 기술한 schema 이름을 확인한다. |
| previously added. Maybe duplicated | 환경 파일에 기술한 table이 중복되었는지 확인한다. |
| table must have a primary key | 환경 파일에 기술한 table에 primary key가 있는지 확인한다. |
| internal error occurred. | 상세 에러를 확인한다. |
| table must set supplemental log | GOLDILOCKS가 supplemental logging 되어 있는지 확인한다. |
| group XXX is already running | 해당 group이 이미 실행되어 있는지 확인한다. |
| GOLDILOCKS_DATA system environment is invalid | GOLDILOCKS_DATA 환경 변수가 설정되어 있는지 확인한다. |
| log file reused or invalid. restart cyclone with '--reset' option | Redo log file이 재사용되었거나 아카이빙 되어있는 redo log file이 없다.  Cyclone을 초기화하여 재시작해야 한다. |
| fail to analyze flow | 비정상적인 redo log를 분석할 경우에 발생하는 에러이며 master와 slave의 GOLDILOCKS 릴리즈 버전이 동일한지 확인한다. |
| Communication link failure | 네트워크 상태를 확인한다. Cyclone을 재시작한다. |
| Master disconnect abnormally | 네트워크 상태를 확인한다. Cyclone을 재시작한다. |
| Protocol error occurred | 상세 에러를 확인한다. |
| Already slave connected | Slave가 이미 실행되어 있는지 확인한다. |
| Invalid group name | 시작/ 종료할 때 명세한 그룹 이름을 확인한다. 환경 파일에 기술한 그룹 이름과 동일해야 한다. |
| Invalid capture information | 기존의 운영 정보가 비정상적인 경우이며 cyclone을 초기화한 후에 재시작한다. |
| Redo log file read timeout | 아카이빙 된 redo log file이 정상적으로 존재하는지 확인한다. |
| Invalid archive log file | 아카이빙 된 해당 redo log file이 정상적이지 않은 경우이다. Cyclone을 초기화하고 재시작해야 한다. |
| Fail to write file | 디스크의 여유 용량을 확인한 후에 cyclone을 재시작한다. |
| Invalid Meta File | Cyclone에서 관리하는 메타파일이 손상되었을 때 발생하는 에러이며 cyclone을 초기화하고 재시작해야 한다. |
| Redo log file does not exist | Master로 동작하는 GOLDILOCKS가 정상적으로 운영되고 있는지 확인한다. |
| [APPLIER-INSERT] XXX | 해당 이유로 인하여 INSERT에 실패했다. |
| [APPLIER-DELETE] XXX | 해당 이유로 인하여 DELETE에 실패했다. |
| [APPLIER-UPDATE] XXX | 해당 이유로 인하여 UPDATE에 실패했다. |

<a id="f6e6af7f5aa7061c"></a>
### LOGMIRROR 에러 메시지와 해결 방법

다음은 LOGMIRROR의 에러 메시지와 해결 방법이다.

<a id="4022f993a3053b9a"></a>
| 에러 메시지 | 해결 방법 |
| --- | --- |
| Service is not available | GOLDILOCKS가 정상적으로 실행되어 있는지 확인한다. |
| Invalid Protocol value | 해당 상세 메시지를 확인한다. |
| file does not eixst | 해당 파일이 정상적으로 존재하는지 확인한다. |
| invalid Control file | 컨트롤 파일이 손상된 상태이다. LOGMIRROR를 초기화하고 재시작해야 한다. |
| Communication link failure | 네트워크 상태를 확인한다. LOGMIRROR를 재시작한다. |
| GOLDILOCKS_DATA system environment is invalid | GOLDILOCKS_DATA 환경 변수가 설정되어 있는지 확인한다. |
| There is no Shared Memory Area for LogMirror | Master로 운영 중인 GOLDILOCKS의 프로퍼티 중에 LOG_MIRROR_MODE가 정상적으로 enable 되었는지 확인한다. |
| Master disconnect abnormally | 네트워크 상태를 확인한다. LOGMIRROR를 재시작해야 한다. |
| Invalid Log File | 해당 파일이 정상적으로 존재하는지 확인한다. |
| Connection Information does not exist | 환경 파일에 있는 GOLDILOCKS 접속 정보가 정상적인지 확인한다. |
| Archive Log File does not exist | Master로 운영 중인 GOLDILOCKS의 ARCHIVELOG_MODE가 정상적으로 설정되어 있는지 확인한다. |

---

[← 7. GOLDILOCKS 데이터베이스의 백업과 복구](7-goldilocks-데이터베이스의-백업과-복구.md) · [전체 목차](../README.md) · [9. Database Information →](9-database-information.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
