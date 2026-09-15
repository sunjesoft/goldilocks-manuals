<a id="e8affc47a256e259"></a>

# 47. gagent

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/e8affc47a256e259)  
> 태그: `22c.1_10_tag`

[← 46. glocator](46-glocator.md) · [전체 목차](../README.md) · [48. gloctl →](48-gloctl.md)

<a id="b2e997e0a00f3db4"></a>
## gagent 소개

<a id="f22d6a622eddcce8"></a>
### 정의

gagent는 GOLDILOCKS cluster system에서 각 멤버 노드와 함께 실행되어 [glocator](46-glocator.md#68298fc49624d83a)와 communication 하는 유틸리티이다.

gagent가 속한 노드의 서버 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#5952b20d977ac530) 값이 1 또는 2로 설정되고 노드 간에 연결이 끊어져서 cluster failover가 진행되면 gagent는 glocator에게 자신이 속한 노드의 viability를 질의한다.   
자세한 내용은 [Cluster Failover](46-glocator.md#e3cefd63f5e7f99c)를 참조한다.

<a id="ddc17c853931e3d3"></a>
### 사용법

```
gagent [options]
```

<a id="52dce6f294b82944"></a>
### Option

<a id="b9853df190853227"></a>
#### help

<a id="507f928f2492e753"></a>
##### 설명

Help 메시지를 출력한다.

<a id="ee96ce2715bd800a"></a>
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

<a id="e98d11ee7c441ada"></a>
#### start

<a id="43802de09483bb2e"></a>
##### 설명

gagent를 구동한다. 같은 home 디렉토리를 갖는 gagent가 이미 구동 중이라면 에러가 발생한다.

<a id="a4b60dcbaf806f84"></a>
##### 사용 예

```
$ gagent --start

gagent is started.
```

<a id="657ab0231d38932b"></a>
#### stop

<a id="b753f37f9f80d64e"></a>
##### 설명

구동 중인 gagent를 멈추게 한다. 구동 중인 gagent를 멈추려면 동일한 home 디렉토리가 설정되어야 한다.

<a id="37f9897e2dd106a3"></a>
##### 사용 예

```
$ gagent --stop

gagent is stopped.
```

<a id="bb5a3f14ddecf4dd"></a>
#### status

<a id="8ffd6b59a29f017e"></a>
##### 설명

구동 중인 gagent의 상태 메시지를 출력한다. 구동 중인 gagent 상태를 확인하려면 동일한 home directory가 설정되어야 한다.

<a id="2e866ad0f735638b"></a>
##### 사용 예

```
$ gagent --status

gagent(31938) is running.
```

<a id="78317c785ee7df9d"></a>
#### conf

<a id="96e5045fe123f090"></a>
##### 설명

gagent를 구동할 때 configure file을 설정한다.

<a id="18c4b4e0e861ca8d"></a>
##### 사용 예

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="9315578a235c5686"></a>
#### home

<a id="a10d2bf1515474ef"></a>
##### 설명

gagent를 구동할 때 GOLDILOCKS의 서버 홈 디렉토리를 설정한다.   
상대 경로를 사용할 경우 &lt;GOLDILOCKS_DATA&gt;를 기준으로 홈 디렉토리를 찾는다. &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수의 값으로 대체된다.

<a id="53f2b64d176dd005"></a>
##### 사용 예

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

위의 예에서 gagent는 &lt;GOLDILOCKS_DATA&gt;/g1n1_home을 홈으로 설정하여 구동된다.

<a id="4feb273b3bf21e50"></a>
#### silent

<a id="462460fbde8ec7e5"></a>
##### 설명

실행에 대한 gagent의 메시지를 출력하지 않는다.

<a id="8141acf0d6d3ee6a"></a>
##### 사용 예

```
$ gagent --start --silent

 Copyright (C) 2010 SUNJESOFT Inc. All rights reserved.
```

<a id="a818717f2323ab9d"></a>
#### no-copyright

<a id="10f670291d3898fe"></a>
##### 설명

실행에 대한 gagent의 copy right와 버전 메시지를 출력하지 않는다.

<a id="e964be014e852d56"></a>
##### 사용 예

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="b0453a90ed04f853"></a>
## gagent Configuration

<a id="16182d8d1c59d282"></a>
### Configuration File 및 환경 변수

gagent는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'AGENT_' 를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $AGENT_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다.

gagent는 $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf 파일을 자신의 환경 파일로 가지고 있다. gagent의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 gagent를 구동하면 된다.

<a id="9588178814d150c8"></a>
### Configuration Property

<a id="55d69e36c69192d4"></a>
#### HOST

<a id="b4e04ba2f6e08874"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | gagent가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

gagent가 UDP 통신을 위해 bind하는 IP address이다.   
IP v4 형식의 IP address를 사용한다.

<a id="6795377669bc3695"></a>
#### REQUEST_PORT

<a id="2f0c1a28f3cd9a38"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REQUEST_PORT |
| 설명 | gagent가 request에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43581 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator에게 request 하는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="2268552b83e05408"></a>
#### RESPONSE_PORT

<a id="64c82241a4ebf782"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RESPONSE_PORT |
| 설명 | gagent가 response에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43582 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator로부터 response 받는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="87f6f25fdfafff12"></a>
#### LOCATOR_HOST

<a id="55ccaf2ddd580712"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_HOST |
| 설명 | glocator의 IP address이다. |
| Data type | ip address(ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator의 IP address이다.

<a id="ae49441caa8b481b"></a>
#### LOCATOR_PORT

<a id="cb522874843d7c40"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

gagent가 glocator에게 packet을 보낼 때 glocator의 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="5f5f9671503b9ab3"></a>
#### SYSTEM_LOGGER_DIR

<a id="c704b456d6086855"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | gagent의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/trc |

gagent의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="b44b3ac28add0314"></a>
#### SYSTEM_UDS_DIR

<a id="61139a737e1c145c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | gagent의 Unix Domain Socket file이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | /tmp (최대 50 byte) |

gagent의 Unix Domain Socket file이 저장되는 directory path이다. 기본값은 /tmp 이다. Directory 길이는 최대 50 byte까지 설정할 수 있다.

<a id="def3656ca1d2c38d"></a>
#### ALTERNATE_LOCATORS

<a id="b58a779e948cbf06"></a>
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
ALTERNATE_LOCATORS=(LOCATOR1,LOCATOR2)

[LOCATOR1]
HOST=127.0.0.1
PORT=42582

[LOCATOR2]
HOST=127.0.0.1
PORT=42583
```

<a id="2106d13c3d5dc760"></a>
#### KEEPALIVE_IDLE_TIME

<a id="9841437a99a0c77e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 설명 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| 기본값/ 범위 | 1 / 1 ~ 16383 |

Keep alive packet을 송신하기 전에 TCP 패킷이 송수신 되지 않는 상태로 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP 패킷 교환이 이루어지지 않으면 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="294c5cb76017bf1a"></a>
#### KEEPALIVE_COUNT

<a id="da11f1087826d700"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_COUNT |
| 설명 | tcp keepalive check count |
| Data type | INT |
| 기본값/ 범위 | 5 / 1 ~ 10 |

Keep alive mechanism을 수행하는 횟수이다.

<a id="54d7ac301706c3e9"></a>
#### KEEPALIVE_INTERVAL

<a id="6f3f0210b23c67a1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_INTERVAL |
| 설명 | tcp keepalive packet interval (sec) |
| Data type | INT |
| 기본값/ 범위 | 5 |

Keep alive 패킷을 전송하는 시간 간격이다.

---

[← 46. glocator](46-glocator.md) · [전체 목차](../README.md) · [48. gloctl →](48-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
