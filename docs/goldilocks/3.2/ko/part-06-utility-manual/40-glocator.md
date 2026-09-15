<a id="8c29744666a187bf"></a>

# 40. glocator

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/8c29744666a187bf)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 39. gtrclogger](39-gtrclogger.md) · [전체 목차](../README.md) · [41. gagent →](41-gagent.md)

<a id="cf1f0650f8c33750"></a>
## glocator 소개

<a id="7e2c9ffa0b061473"></a>
### 정의

glocator는 GOLDILOCKS cluster system에서 client에게 location을 제공하고 관리하는 유틸리티이다.  
glocator 프로그램은 [gloctl](42-gloctl.md#21bac538710a7115)과 [gagent](41-gagent.md#b27e2a16d2232e7d)를 통해 cluster member 노드들의 location 정보를 제공받는다.  
glocator는 User Datagram Protocol (UDP)을 사용하여 client 및 내부 프로세스와 통신한다.

> glocator가 사용하는 location 정보는 cluster member 노드가 사용하는 location과 차이가 있다. glocator는 member 노드의 host, listener port, db home path, agent port를 필요로 한다.   
> glocator는 gagent 보다 먼저 실행되어 gagent로부터 이런 location 정보를 제공받거나 gloctl을 통해 제공받아야 한다.

<a id="b651c34f12300b7c"></a>
### 사용법

```
glocator [options]
```

<a id="b6190d007f82d8f0"></a>
### Option

<a id="f24cd3770bb03c9d"></a>
#### help

<a id="3b1b186209f00cea"></a>
##### 설명

Help 메시지를 출력한다.

<a id="e7ecc92dea6d2b5c"></a>
##### 사용 예

```
$ glocator --help

Usage:
 glocator [options]

Options:

-c  --create       Create glocator environment
-s  --start        Start glocator
-t  --stop         Stop glocator
-f  --conf         Set configure file
-u  --status       Get glocator status
-y  --sync         Synchronize with alternate glocator(BOTH, SOURCE)
-l  --silent       Suppress display message
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help message
```

<a id="0472dc2e91d56d9c"></a>
#### create

<a id="407dbd94dd18ffbe"></a>
##### 설명

glocator의 데이터 파일을 생성한다.

<a id="fb2e1f842c21dc6e"></a>
##### 사용 예

```
$ glocator --create

glocator is created.
```

> glocator 데이터 파일은 &lt;GOLDILOCKS_DATA&gt;/db 디렉토리에 생성된다.

```
$ ls
README  glocator.dat  system_data.dbf  system_dict.dbf  system_undo.dbf
```

<a id="ff3622455163ecfb"></a>
#### start

<a id="4e26ce02b62b6015"></a>
##### 설명

glocator를 구동한다. 같은 port를 갖는 glocator가 이미 구동 중이라면 에러가 발생한다.

<a id="937ee0390e7b3e7a"></a>
##### 사용 예

```
$ glocator --start

glocator is started.
```

<a id="c0260ed32c96b18f"></a>
#### stop

<a id="8b35c90ea28c8b27"></a>
##### 설명

구동 중인 glocator를 정지시킨다. 구동 중인 glocator를 멈추려면 같은 port가 설정되어야 한다.

<a id="b890dd2525e1de1f"></a>
##### 사용 예

```
$ glocator --stop

glocator is stopped.
```

<a id="7540147a8994068e"></a>
#### conf

<a id="7813e266f8a32798"></a>
##### 설명

glocator를 구동할 때 configure file을 설정한다.

<a id="958fe1258fb3c8db"></a>
##### 사용 예

```
$ glocator --start --conf goldilocks.glocator.conf

glocator is started.
```

<a id="46f88c3e9dc68638"></a>
#### status

<a id="55ec7d400863c0b9"></a>
##### 설명

구동 중인 glocator의 상태 메시지를 출력한다. 구동 중인 glocator 상태를 확인하려면 같은 port가 설정 되어야 한다.

<a id="cffc64d16ab06cae"></a>
##### 사용 예

```
$ glocator --status

Process ID: 26058
Configuration file: goldilocks.glocator.conf
Unix domain path: /tmp/unix-glocator.42581
Udp listen host: 0.0.0.0, Port: 42581
glocator is running.
```

<a id="fd3abd87e565d7f3"></a>
#### sync

<a id="6a41ef5d02c28031"></a>
##### 설명

glocator를 구동하기 전에 ALTERNATE_LOCATORS에 설정된 glocator의 데이터를 동기화를 한다.

데이터 동기화에는 ALTERNATE_LOCATORS에서 데이터를 가지고 오는 SOURCE 방식과 두 glocator를 병합하는 BOTH 방식이 있다.

<a id="92ac8a7fac7eb999"></a>
##### 사용 예

다음은 sync 옵션에 성공하는 예이다.

```
$ glocator --start --sync

glocator is started.
```

다음은 sync 옵션에 실패하는 예이다. ALTERNATE_LOCATORS 속성에 값이 설정되지 않았다.

```
$ glocator --start --sync

ERR-HY000(60016): Need more alternate locator host information.
```

다음은 sync 옵션에 실패하는 예이다. ALTERNATE_LOCATORS에 설정된 glocator로부터 응답을 받지 못한 상황이다.

```
$ glocator --start --sync

ERR-HY000(60016): Need more alternate locator host information.
```

<a id="104ab2cbe6c9e12d"></a>
#### silent

<a id="6a10821ad3aaa1cb"></a>
##### 설명

실행에 대한 glocator의 메시지를 출력하지 않는다.

<a id="e6f2ba06597ce9e8"></a>
##### 사용 예

```
$ glocator --start --silent
```

<a id="d039fae1344a5967"></a>
#### no-copyright

<a id="cd2222728fc3441a"></a>
##### 설명

실행에 대한 glocator의 copyright와 버전 메시지를 출력하지 않는다.

<a id="35b065f5decb6036"></a>
##### 사용 예

```
$ glocator --start --no-copyright

glocator is started.
```

<a id="92fd0967d39462a1"></a>
## glocator 사용

<a id="96e08ad8d4527917"></a>
### 데이터 파일

glocator를 구동하려면 시작하기 전에 glocator 데이터 파일을 먼저 생성해야 한다.

```
$ glocator --create

glocator is created.
```

glocator 데이터 파일이 저장되는 디렉토리는 configuration [LOCATION_FILE_DIR](#0d30fa472b181cc7)을 수정하여 변경할 수 있다. 기본값은 &lt;GOLDILOCKS_DATA&gt;/db에 생성된다. 데이터 파일은 [LOCATION_FILE_NAME](#cb3bef28cca60b49)을 수정하여 변경할 수 있다. 기본값은 glocator.dat이다.

glocator 데이터 파일의 최대 크기와 초기 크기는 configuration [LOCATION_FILE_MAX_SIZE](#effee8241e68bbf5)와 [LOCATION_FILE_SIZE](#8abb82cba1c16cc5)를 수정하여 변경할 수 있다.

<a id="729941785f7cedfc"></a>
### CSTARTUP과 CSHUTDOWN

glocator는 GOLDILOCKS 서버의 CSTARTUP과 CSHUTDOWN에 사용될 수 있다.  
이를 위해서는 glocator가 구동 중이고 gsqlnet을 통해 CSTARTUP 또는 CSHUTDOWN 명령을 실행해야 한다.  
단, gsqlnet을 실행하는 장비의 odbc.ini에 LOCATOR_DSN과 속성값이 설정되어 있어야 한다.   
자세한 내용은 [GOLDILOCKS UNIX ODBC driver 라이브러리](../part-05-developer-manual/25-odbc.md#aeaf0a37b43531ca)를 참조한다.

다음은 glocator를 사용하기 위해 odbc.ini에 설정한 내용이다.

```
[GOLDILOCKS]
HOST=127.0.0.1
PORT=20101
UID=sys
PWD=gliese
LOCATOR_DSN=GLOCATOR

[GLOCATOR]
HOST=127.0.0.1
PORT=42581
```

> DSN [GLOCATOR]에 FILE 속성이 있으면 glocator 대신 FILE 속성에 명시된 파일을 우선해서 사용하므로 FILE 속성을 제외해야 한다.

CSTARTUP과 CSHUTDOWN 명령을 실행하려면 glocator가 member 노드들에 대한 location 정보를 알고 있어야 한다.

<a id="3709567b19fdacc4"></a>
### 다중화

<a id="f223578073f8e290"></a>
#### 개요

glocator 다중화는 데이터를 일관성있게 유지하여 장애가 발생할 경우 원격 glocator를 사용한 지속적인 서비스를 가능하게 한다.

<a id="c5af35e48664b440"></a>
#### 설정

다중화를 사용하려면 각각의 glocator가 configure file에 ALTERNATE_LOCATORS 속성을 설정해야 한다. ALTERNATE_LOCATORS 속성에는 Locator_name이 설정되어야 하고 설정된 Locator_name은 HOST, PORT 속성과 함께 configure 파일에 기록되어야 한다.

ALTERNATE_LOCATORS 속성은 다음과 같이 설정할 수 있다.

```
[LOCATOR]
ALTERNATE_LOCATORS = (locator_name1,locator_name2)
[locator_name1]
HOST= ip_address
PORT = port_num
[locator_name2]
HOST= ip_address
PORT = port_num
```

다음은 ALTERNATE_LOCATORS 속성을 설정하는 configure 파일의 예이다.

```
[LOCATOR]
PORT=42581
SYNC_RESPONSE_TIMEOUT = 2
SYNC_RETRY_COUNT = 2
LOCATION_FILE_NAME='glocator_1.dat'
ALTERNATE_LOCATORS=(LOCATOR_2,LOCATOR_3)

[LOCATOR_2]
HOST=127.0.0.1
PORT=42582

[LOCATOR_3]
HOST=127.0.0.1
PORT=42583
```


> 
> - [LOCATOR]는 glocator가 기본값으로 읽어들이는 DSN이다.
> - glocator와 관련된 ODBC와 gagent 설정에 대한 자세한 내용은 [odbc.ini 파일](../part-05-developer-manual/25-odbc.md#78b0fc955ee2c6e5), [ALTERNATE_LOCATORS](41-gagent.md#9471172b80ce27ec)을 참조한다.
> 

<a id="dcf04f3267ddb55e"></a>
#### 데이터 동기화

다중화된 glocator를 서비스할 때 데이터는 일관되게 유지되어야 한다. 기존에 작동 중인 glocator가 없을 경우, 모든 glocator는 일반 시작을 하면 된다. 기존에 동작 중인 glocator가 있을 경우, [sync](#fd3abd87e565d7f3) 옵션을 사용하여 데이터를 동기화하는 방법으로 alternate glocator를 시작할 수 있다.

[sync](#fd3abd87e565d7f3) 옵션에는 glocator 자신의 데이터와 alternate glocator의 데이터를 병합하는 BOTH와 상대 glocator로부터 데이터를 가지고 오는 SOURCE가 있다. glocator의 sync 작업은 glocator와 alternate glocator 사이의 1 : 1 대응 작업이다. 따라서 A, B, C 세 개의 glocator를 다중화하려고 할 때 A와 B가 이미 구동 중이고 C를 BOTH 방식으로 sync하여 구동하면 A 또는 B glocator의 데이터가 서로 다를 수 있다.

서비스 중인 glocator는 변경된 내용만 동기화한다. 패킷 손실 등의 이유로 데이터 동기화에 실패하는 경우, 데이터가 서로 다를 수 있다. 이 경우, [gloctl](42-gloctl.md#21bac538710a7115) 프로그램을 사용하여 해당 glocator에서 직접 데이터를 수정하거나 glocator를 sync 옵션으로 다시 시작할 수 있다.

<a id="b8471eaf4ce3bcbe"></a>
## 기능

<a id="a88d7ba491121954"></a>
### Connection Service

Cluster 환경에서 특정 노드에 대한 location 정보를 알지 못해도 사용자가 정한 몇 개의 노드 중에 임의로 접속할 수 있도록 service 기능을 제공한다.

Service 기능은 glocator에서 관리하는 노드를 사용자가 임의의 그룹으로 지정하는 것이다. 이 service는 gloctl 프로그램을 사용하여 등록할 수 있다. glocator에서 관리하는 서비스 목록 역시 gloctl 프로그램을 사용하여 확인할 수 있다.

응용 프로그램은 ODBC 드라이버를 사용하여 접속해야 하며 [odbc.ini 파일](../part-05-developer-manual/25-odbc.md#78b0fc955ee2c6e5)에 LOCATOR_DSN과 LOCATOR_SERVICE 속성을 지정해야 한다.

<a id="8a9fbb5de4c8e90f"></a>
![locator_service](../assets/images/52f91fa4c9348582.png)

위 그림은 응용 프로그램 (application)이 service s3에 속한 g1n1에 접속한 내용이다. ODBC 드라이버가 service를 이용하여 연결하는 순서는 service에 등록된 노드 순서와 동일하다. 위의 예에서 ODBC 드라이버가 g1n1에 연결하는데 실패하면 다음 순서인 노드 g2n1에 연결을 시도할 것이다.

> Service 기능을 사용하려면 glocator에 노드의 유효한 location 정보가 먼저 입력되어야 한다.

<a id="a255eaa2449c605b"></a>
### Cluster Failover

glocator는 server가 failover를 진행할 때 도움이 된다.

Server 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#dfa017b50ad92f75) 값이 1 또는 2로 설정되고, cluster 환경에서 노드 간에 연결이 끊어져 failover가 발생하면 각 노드는 cluster failover를 진행하여 gagent를 통해 glocator에게 자신의 viability를 질의한다.

질의를 받은 glocator는 연결이 끊어진 두 노드의 viability를 판단하고 gagent를 통해 각 노드에 결과를 전달한다.

Viabilty 결과를 받은 노드는 종료되거나 failover를 진행한다.

<a id="0d0f77c4f0504b97"></a>
## glocator Configuration

<a id="410bea8d5be102b8"></a>
### Configuration File 및 환경 변수

glocator는 configuration을 설정하기 위해 file이나 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'LOCATOR_'를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $LOCATOR_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file 내용은 환경 변수 설정값보다 우선한다.

glocator는 DSN을 [LOCATOR] 기본값으로 하여 configuration file을 읽는다.

glocator는 $GOLDILOCKS_DATA/conf/goldilocks.glocator.conf 파일을 자신의 환경 파일로 가지고 있다. glocator의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 glocator를 구동하면 된다.

<a id="daa1bdab24874cb4"></a>
### Configuration Property

<a id="4ef17b76020ca645"></a>
#### HOST

<a id="fd70e2ec3bf286e7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | glocator가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator가 UDP 통신을 위해 bind하는 IP address이다.  
IP v4 형식의 IP address를 사용한다.

<a id="d752827e4a4df35f"></a>
#### PORT

<a id="ca5e5b8e0776072f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

glocator가 UDP 통신으로 packet을 받는 port이다.  
Port는 1024부터 49151까지 사용할 수 있다.

<a id="df35b2acdd72327a"></a>
#### WORKER_COUNT

<a id="c25fef3012051491"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | WORKER_COUNT |
| 설명 | Job을 처리하는 thread의 개수이다. |
| Data type | INT |
| 기본값/ 범위 | 1 / 1~8 |

glocator가 client나 내부 프로세스로부터 받은 packet을 처리하는 thread의 개수이다.

<a id="2bef059b3683d474"></a>
#### SESSION_QUEUE_SIZE

<a id="b7b0479184193c39"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_QUEUE_SIZE |
| 설명 | 수신한 packet을 처리하기 전까지 저장하는 queue size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

glocator가 client나 내부 프로세스로부터 받은 packet을 처리하기 전에 저장하는 queue의 size이다.  
Queue에는 packet이 session 단위의 단일 item으로 저장된다.

<a id="00d66e35d6e41197"></a>
#### SESSION_ALLOCATOR_SIZE

<a id="7b17900c43951ab8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_ALLOCATOR_SIZE |
| 설명 | Session queue에 저장되는 item을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

Session queue에 저장되는 item (session)을 할당할 때 사용되는 allocator의 size이다.

<a id="94496bd1bf23f96f"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="23bffc4007f927ef"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PACKET_ALLOCATOR_SIZE |
| 설명 | UDP 통신으로 packet을 받을 때 packet을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 33554432 / 10485760~2147483648 |

glocator가 packet을 받기 위해 할당하는 buffer를 위한 allocator의 size이다.

<a id="caf41ba06811228b"></a>
#### SYSTEM_LOGGER_DIR

<a id="c8df5883aa213f5a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | glocator trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | '&lt;GOLDILOCKS_DATA&gt;/trc' |

glocator의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="18819fd8a3d53481"></a>
#### SYSTEM_UDS_DIR

<a id="1cee10568b4bd408"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | glocator에서 사용되는 unix domain socket 파일이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | '/tmp' / 최대 60 byte |

glocator에서 사용되는 unix domain socket 파일이 저장되는 directory path를 설정한다. Directory 최대 길이는 60 byte 이내로 설정해야 한다.

<a id="0d30fa472b181cc7"></a>
#### LOCATION_FILE_DIR

<a id="c7f2869732aae995"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_DIR |
| 설명 | glocator에서 사용되는 location 파일이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | '&lt;GOLDILOCKS_DATA&gt;/db' |

glocator에서 사용되는 location 파일이 저장되는 directory path를 설정한다.

<a id="cb3bef28cca60b49"></a>
#### LOCATION_FILE_NAME

<a id="6f384b5dcf9f2818"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_NAME |
| 설명 | glocator에서 사용되는 location 파일 이름이다. |
| Data type | String |
| 기본값/ 범위 | 'glocator.dat' |

glocator에서 사용되는 location 파일 이름을 설정한다.   
기본값은 glocator.dat 이다.

<a id="8abb82cba1c16cc5"></a>
#### LOCATION_FILE_SIZE

<a id="5e609541edf20ebe"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_SIZE |
| 설명 | Location 파일의 초기 size이다. |
| Data type | Int |
| 기본값/ 범위 | 1048576 / 104576~2147483648 |

glocator에서 사용되는 location 파일의 초기 size를 설정한다.

<a id="effee8241e68bbf5"></a>
#### LOCATION_FILE_MAX_SIZE

<a id="fba29852519b9750"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATION_FILE_MAX_SIZE |
| 설명 | Location 파일의 최대 size이다. |
| Data type | Int |
| 기본값/ 범위 | 10485760 / 104576~2147483648 |

glocator에서 사용되는 location 파일의 최대 size를 설정한다.

<a id="305f66bf78c5f190"></a>
#### SESSION_TIMEOUT

<a id="9017978d8cfa4066"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_TIMEOUT |
| 설명 | glocator가 packet을 수신하기 위해 최대로 대기하는 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 100 / 0 ~2147483648 (second 단위) |

glocator가 packet을 수신하기 위해 최대로 대기하는 시간 (초)을 설정한다. 처리되지 못하고 시간 초과된 packet은 버려진다.

<a id="1c0e7f67b82a2403"></a>
#### FAILOVER_TIMEOUT

<a id="1c350b153c3d2b22"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | FAILOVER_TIMEOUT |
| 설명 | glocator가 failover 요청을 받고 작업할 때의 최대 대기 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 18 / 0 ~2147483648 |

glocator가 요청받은 failover 작업을 하는 중에 packet을 기다리는 최대 시간을 설정한다. 시간을 초과하면 요청한 gagent에 에러를 반환한다.

<a id="13cbee08541c5e65"></a>
#### ALTERNATE_LOCATORS

<a id="40817dabf42d6ffa"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ALTERNATE_LOCATORS |
| 설명 | glocator의 alternate locator, 다중화 설정을 한다. |
| Data type | String |
| 기본값/ 범위 | empty / 0 ~ 1024 bytes |

glocator의 [다중화](#3709567b19fdacc4)를 설정한다.

<a id="d69d72026d8d4c14"></a>
#### SYNC_RETRY_COUNT

<a id="fb5ee3d7218331f9"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYNC_RETRY_COUNT |
| 설명 | glocator가 alternate locator와의 동기화 작업에 실패할 경우 다시 시도하는 횟수를 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 1 / 0 ~ 5 |

glocator 동기화 작업의 재전달 횟수를 설정한다.

데이터가 변경되었을 때 glocator는 alternate locator에 변경된 데이터를 전달하는데, 데이터를 전달한 후에 응답을 받지 못하면 다시 전달한다.

<a id="9a302ab8569e252d"></a>
#### SYNC_RESPONSE_TIMEOUT

<a id="25fbb66bc051efb4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYNC_RESPONSE_TIMEOUT |
| 설명 | glocator 동기화 작업에 대한 응답 대기 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 5 / 1 ~ 20 |

glocator가 전달한 동기화 데이터에 대한 응답을 기다리는 시간을 설정한다.

---

[← 39. gtrclogger](39-gtrclogger.md) · [전체 목차](../README.md) · [41. gagent →](41-gagent.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
