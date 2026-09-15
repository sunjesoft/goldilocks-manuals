<a id="b27e2a16d2232e7d"></a>

# 41. gagent

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/b27e2a16d2232e7d)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 40. glocator](40-glocator.md) · [전체 목차](../README.md) · [42. gloctl →](42-gloctl.md)

<a id="73b33559e015280f"></a>
## gagent 소개

<a id="a336919b35b83f26"></a>
### 정의

gagent는 GOLDILOCKS cluster system에서 각 멤버 노드와 함께 실행되어 [glocator](40-glocator.md#8c29744666a187bf)와 communication 하는 유틸리티이다.

> gagent는 glocator에게 local 노드의 location 정보를 제공할 수 있다. Location 정보의 정합성을 위해 glocator가 gagent 보다 먼저 실행되어야 한다.

<a id="855af7f792f371d6"></a>
### 사용법

```
gagent [options]
```

<a id="c65760ffe5b44668"></a>
### Option

<a id="1c15b2d02a529dd6"></a>
#### help

<a id="cff8e92be2ced78e"></a>
##### 설명

Help 메시지를 출력한다.

<a id="a9fba28ddd6acbab"></a>
##### 사용 예

```
$ gagent --help

Usage:
 gagent [options]

Options:

-s  --start                        Start gagent
-t  --stop                         Stop gagent
-u  --status                       Get gagent status
-f  --conf                         Set configure file
-o  --home                         gmaster home path
-l  --silent                       Suppress display message
-r  --no-copyright                 Suppress display copy right and version
-h  --help                         Print help message
```

<a id="952285ebe19c0668"></a>
#### start

<a id="21308304f28eba00"></a>
##### 설명

gagent를 구동한다. 같은 home 디렉토리를 갖는 gagent가 이미 구동 중이라면 에러가 발생한다.

<a id="d4f7d4bafb611160"></a>
##### 사용 예

```
$ gagent --start

gagent is started.
```

<a id="6770358ad8174e01"></a>
#### stop

<a id="d31c52d41aed620f"></a>
##### 설명

구동 중인 gagent를 멈추게 한다. 구동 중인 gagent를 멈추려면 동일한 home 디렉토리가 설정되어야 한다.

<a id="98797653a318b88e"></a>
##### 사용 예

```
$ gagent --stop

gagent is stopped.
```

<a id="5bf393fe7f2e122f"></a>
#### status

<a id="cd05c96ac2925339"></a>
##### 설명

구동 중인 gagent의 상태 메시지를 출력한다. 구동 중인 gagent 상태를 확인하려면 동일한 home directory가 설정되어야 한다.

<a id="d6582ae553c82859"></a>
##### 사용 예

```
$ gagent --status

gagent(31938) is running.
```

<a id="6514f65f0473014e"></a>
#### conf

<a id="c107376ed612e2f4"></a>
##### 설명

gagent를 구동할 때 configure file을 설정한다.

<a id="029bc158204b8ed6"></a>
##### 사용 예

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="df85131334faef59"></a>
#### home

<a id="a3a0b6a25d64b7a5"></a>
##### 설명

gagent를 구동할 때 GOLDILOCKS의 서버 홈 디렉토리를 설정한다.  
상대 경로를 사용할 경우 &lt;GOLDILOCKS_DATA&gt;를 기준으로 홈 디렉토리를 찾는다. &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수의 값으로 대체된다.

<a id="b713ff0016be4196"></a>
##### 사용 예

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

위의 예에서 gagent는 &lt;GOLDILOCKS_DATA&gt;/g1n1_home을 홈으로 설정하여 구동된다.

<a id="a5562eb223374f85"></a>
#### silent

<a id="959181f194fdbd23"></a>
##### 설명

실행에 대한 gagent의 메시지를 출력하지 않는다.

<a id="0f35cad05d62a22f"></a>
##### 사용 예

```
$ gagent --start --silent

 Copyright (C) 2010 SUNJESOFT Inc. All rights reserved.
```

<a id="85cdb3d0f2b0b886"></a>
#### no-copyright

<a id="399be01742d6a280"></a>
##### 설명

실행에 대한 gagent의 copyright와 버전 메시지를 출력하지 않는다.

<a id="a9a9c4c85f4521c6"></a>
##### 사용 예

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="8e219e12e2d98e77"></a>
## gagent Configuration

<a id="a5b4336e5361bdad"></a>
### Configuration File 및 환경 변수

gagent는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'AGENT_' 를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $AGENT_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다.

gagent는 $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf 파일을 자신의 환경 파일로 가지고 있다. gagent의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 gagent를 구동하면 된다.

<a id="4e01d88d8537de5b"></a>
### Configuration Property

<a id="2362c009a69ef656"></a>
#### HOST

<a id="27df95e895a84646"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | gagent가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/범위 | 0.0.0.0 |

gagent가 UDP 통신을 위해 bind하는 IP address이다.  
IP v4 형식의 IP address를 사용한다.

<a id="2b1c8a5831281015"></a>
#### PORT

<a id="417e6ac72d69aebb"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gagent가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/범위 | 43581 / 1024~49151 |

gagent가 UDP 통신으로 packet을 받는 port이다.  
Port는 1024부터 49151까지 사용할 수 있다.

<a id="a419c78d39d5320e"></a>
#### LOCATOR_HOST

<a id="3b4d8d1c076a040a"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_HOST |
| 설명 | glocator의 IP address이다. |
| Data type | ip address(ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator의 IP address이다.

<a id="f95f84378796a430"></a>
#### LOCATOR_PORT

<a id="e7f1425b9378b043"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

gagent가 glocator에게 packet을 보낼 때 glocator의 port이다.  
Port는 1024부터 49151까지 사용할 수 있다.

<a id="198e8247e04469aa"></a>
#### COMMAND_QUEUE_SIZE

<a id="307a09659b7475e8"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | COMMAND_QUEUE_SIZE |
| 설명 | 수신한 packet을 처리하기 전까지 저장하는 queue size이다. |
| Data type | INT |
| 기본값/ 범위 | 1048576 / 1048576~2147483648 |

gagent가 glocator로부터 받은 packet을 처리하기 전에 저장하는 queue의 size이다.  
Queue에는 packet이 command 단위의 단일한 item으로 저장된다.

<a id="2a3ffe02b1e3f192"></a>
#### COMMAND_ALLOCATOR_SIZE

<a id="c3c2f8c410c9488f"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | COMMAND_ALLOCATOR+SIZE |
| 설명 | Command queue에 저장되는 item을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 1048576 / 1048576~2147483648 |

Command queue에 저장되는 item (command)을 할당할 때 사용되는 allocator의 size이다.

<a id="8a903492618cda7e"></a>
#### PACKET_ALLOCATOR_SIZE

<a id="4d66006389a913b0"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PACKET_ALLOCATOR+SIZE |
| 설명 | UDP 통신으로 packet을 받을 때 packet을 할당하는 allocator size이다. |
| Data type | INT |
| 기본값/ 범위 | 1048576 / 1048576~2147483648 |

gagent가 packet을 받기 위해 할당하는 buffer를 위한 allocator의 size이다.

<a id="db08a9f18ecaff5a"></a>
#### SYSTEM_LOGGER_DIR

<a id="237d439dfb9c9044"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | gagent의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | '&lt;GOLDILOCKS_DATA&gt;/trc' |

gagent의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="4986679a97310064"></a>
#### UPDATE_LOCATION_TIME

<a id="de8ad76d44429f3c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | UPDATE_LOCATION_TIME |
| 설명 | gagent가 glocator에 자신의 location 정보를 업데이트 하는 주기를 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 120 / 30~2147483648 (second 단위) |

gagent에서 glocator에게 자신의 노드 location 정보를 업데이트 하는 주기를 설정한다.

<a id="4d69c40fe879cd8e"></a>
#### SESSION_TIMEOUT

<a id="7986c1f02e6da0ff"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SESSION_TIMEOUT |
| 설명 | gagent가 packet을 수신하기 위해 최대로 대기하는 시간을 설정한다. |
| Data type | Int |
| 기본값/ 범위 | 60 / 0 ~2147483648 (second 단위) |

glocator가 packet을 수신하기 위해 최대로 대기하는 시간 (초)을 설정한다. 처리되지 못하고 시간 초과된 packet은 버려진다.

<a id="9471172b80ce27ec"></a>
#### ALTERNATE_LOCATORS

<a id="24f59a0b5141c873"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ALTERNATE_LOCATORS |
| 설명 | alternate locators를 설정한다. |
| Data type | String |
| 기본값/ 범위 | empty / 0 ~ 1024 |

gagent에 설정된 glocator로부터 응답을 받지 못하는 경우, alternate locator로 대체하여 작업을 진행한다.

다음은 ALTERNATE_LOCATOR를 사용한 configure 파일의 예이다.

```
[AGENT]
PORT=43581
LOCATOR_HOST=127.0.0.1
LOCATOR_PORT=42581
ALTERNATE_LOCATORS='LOCATOR1,LOCATOR2'

[LOCATOR1]
HOST=127.0.0.1
PORT=42582

[LOCATOR2]
HOST=127.0.0.1
PORT=42583
```

---

[← 40. glocator](40-glocator.md) · [전체 목차](../README.md) · [42. gloctl →](42-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
