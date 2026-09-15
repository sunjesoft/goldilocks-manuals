<a id="ce500fe89c0ee9b6"></a>

# 52. gagent

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/ce500fe89c0ee9b6)  
> 태그: `26c.1_0_tag`

[← 51. glocator](51-glocator.md) · [전체 목차](../README.md) · [53. gloctl →](53-gloctl.md)

<a id="87cf1fc95914f010"></a>
## gagent 소개

<a id="ea46e11cf3cb84e9"></a>
### 정의

gagent는 GOLDILOCKS cluster system에서 각 멤버 노드와 함께 실행되어 [glocator](51-glocator.md#ad25c1271ccf5dff)와 communication 하는 유틸리티이다.

gagent가 속한 노드의 서버 프로퍼티 [CLUSTER_SPLIT_BRAIN_RESOLUTION_POLICY](../part-02-administration-manual/10-server-property.md#5165de282789b915) 값이 1 또는 2로 설정되고 노드 간에 연결이 끊어져서 cluster failover가 진행되면 gagent는 glocator에게 자신이 속한 노드의 viability를 질의한다.   
자세한 내용은 [Cluster Failover](51-glocator.md#027f7ef35b3a087b)를 참조한다.

<a id="8fc59023b999b6f0"></a>
### 사용법

```
gagent [options]
```

<a id="13f4079841bc8339"></a>
### Option

<a id="35050da83c781dd5"></a>
#### help

<a id="298f21a4b0264ada"></a>
##### 설명

Help 메시지를 출력한다.

<a id="130a66467d73ee33"></a>
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

<a id="11530d87b7ef5746"></a>
#### start

<a id="0d0246be457afd85"></a>
##### 설명

gagent를 구동한다. 같은 home 디렉토리를 갖는 gagent가 이미 구동 중이라면 에러가 발생한다.

<a id="473de5965ce1b613"></a>
##### 사용 예

```
$ gagent --start

gagent is started.
```

<a id="eb7fa41d1d7f4a47"></a>
#### stop

<a id="ca856a8c63df7bb1"></a>
##### 설명

구동 중인 gagent를 멈추게 한다. 구동 중인 gagent를 멈추려면 동일한 home 디렉토리가 설정되어야 한다.

<a id="ded2cebc376c3f85"></a>
##### 사용 예

```
$ gagent --stop

gagent is stopped.
```

<a id="42e7bf5b043cd715"></a>
#### status

<a id="a5e5247c3282627d"></a>
##### 설명

구동 중인 gagent의 상태 메시지를 출력한다. 구동 중인 gagent 상태를 확인하려면 동일한 home directory가 설정되어야 한다.

<a id="0a10092c1f8388d4"></a>
##### 사용 예

```
$ gagent --status

gagent(31938) is running.
```

<a id="0aa378c1c6f1b40a"></a>
#### conf

<a id="e24c49ee95870a94"></a>
##### 설명

gagent를 구동할 때 configure file을 설정한다.

<a id="8339fdb71ba07050"></a>
##### 사용 예

```
$ gagent --start --conf goldilocks.gagent.conf

gagent is started.
```

<a id="ec64cd5ca3b414f5"></a>
#### home

<a id="940be7004a3dbbea"></a>
##### 설명

gagent를 구동할 때 GOLDILOCKS의 서버 홈 디렉토리를 설정한다.   
상대 경로를 사용할 경우 &lt;GOLDILOCKS_DATA&gt;를 기준으로 홈 디렉토리를 찾는다. &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수의 값으로 대체된다.

<a id="1e61dfb5fef30d67"></a>
##### 사용 예

```
$ gagent --start --home g1n1_home --conf goldilocks.gagent.conf  

gagent is started.
```

위의 예에서 gagent는 &lt;GOLDILOCKS_DATA&gt;/g1n1_home을 홈으로 설정하여 구동된다.

<a id="3d8ce22522b7ae06"></a>
#### silent

<a id="e4c57c2347586d46"></a>
##### 설명

실행에 대한 gagent의 메시지를 출력하지 않는다.

<a id="cdb3f4a7f6e12759"></a>
##### 사용 예

```
$ gagent --start --silent

 Copyright (C) 2010 SUNJESOFT Inc. All rights reserved.
```

<a id="58d8c0bcace59900"></a>
#### no-copyright

<a id="1a63c925784a6e5f"></a>
##### 설명

실행에 대한 gagent의 copy right와 버전 메시지를 출력하지 않는다.

<a id="bf50d355fb1e5c31"></a>
##### 사용 예

```
$ gagent --start --no-copyright

gagent is started.
```

<a id="f3b37a5527e52eee"></a>
## gagent Configuration

<a id="1da4080e9c3aa122"></a>
### Configuration File 및 환경 변수

gagent는 configuration을 설정하기 위해 file 또는 환경 변수를 사용할 수 있다.

환경 변수는 configuration property name에 prefix로 'AGENT_' 를 추가한 name을 사용하여 지정할 수 있다. 예를 들어 configuration file에 HOST를 설정하면 $AGENT_HOST를 지정하는 것과 같은 효과가 있다.

Configuration file의 내용은 환경 변수 설정값보다 우선한다.

gagent는 $GOLDILOCKS_DATA/conf/goldilocks.gagent.conf 파일을 자신의 환경 파일로 가지고 있다. gagent의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 환경 변수를 설정하고 gagent를 구동하면 된다.

<a id="b42a36318ba513d5"></a>
### Configuration Property

<a id="495df273eee9dbdb"></a>
#### HOST

<a id="cfca91a425bddee5"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | HOST |
| 설명 | gagent가 bind 하는 IP address이다. |
| Data type | ip address (ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

gagent가 UDP 통신을 위해 bind하는 IP address이다.   
IP v4 형식의 IP address를 사용한다.

<a id="8d09cf19dc80cea3"></a>
#### REQUEST_PORT

<a id="72ba7a1ab7c63b86"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | REQUEST_PORT |
| 설명 | gagent가 request에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43581 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator에게 request 하는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="1fffb2136779bdac"></a>
#### RESPONSE_PORT

<a id="0618cc6be4014359"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | RESPONSE_PORT |
| 설명 | gagent가 response에 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 43582 / 1024~49151 |

gagent가 tcp 통신을 할 때 glocator로부터 response 받는 용도로 사용하는 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="d0a877603e910573"></a>
#### LOCATOR_HOST

<a id="c4e57426b878adb3"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_HOST |
| 설명 | glocator의 IP address이다. |
| Data type | ip address(ip v4) |
| 기본값/ 범위 | 0.0.0.0 |

glocator의 IP address이다.

<a id="8cd495847448f06b"></a>
#### LOCATOR_PORT

<a id="9564a5c1f341ebf6"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | LOCATOR_PORT |
| 설명 | glocator가 Recv를 기다리는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024~49151 |

gagent가 glocator에게 packet을 보낼 때 glocator의 port이다.   
Port는 1024부터 49151까지 사용할 수 있다.

<a id="2f2b6252650a889c"></a>
#### SYSTEM_LOGGER_DIR

<a id="17f7ffa8972c147e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_LOGGER_DIR |
| 설명 | gagent의 trace log file의 directory path이다. |
| Data type | String |
| 기본값/ 범위 | &lt;GOLDILOCKS_DATA&gt;/trc |

gagent의 system trace log file이 저장되는 directory path이다. 기본값의 &lt;GOLDILOCKS_DATA&gt;는 $GOLDILOCKS_DATA 환경 변수 값으로 대체된다.

<a id="604f0fa5c4825309"></a>
#### SYSTEM_UDS_DIR

<a id="aba79251fc978689"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | SYSTEM_UDS_DIR |
| 설명 | gagent의 Unix Domain Socket file이 저장되는 directory path이다. |
| Data type | String |
| 기본값/ 범위 | /tmp (최대 50 byte) |

gagent의 Unix Domain Socket file이 저장되는 directory path이다. 기본값은 /tmp 이다. Directory 길이는 최대 50 byte까지 설정할 수 있다.

<a id="6516869ff8ad95b4"></a>
#### ALTERNATE_LOCATOR

<a id="466f7c9069ead763"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | ALTERNATE_LOCATOR |
| 설명 | alternate locator를 설정한다. |
| Data type | String |
| 기본값/ 범위 | empty / 0 ~ 1024 |

gagent에 설정된 glocator와 연결이 끊어지는 경우 alternate locator와 연결하여 작업을 진행한다. glocator가 이중화 된 상태에서 gagent가 연결하려는 glocator가 sub일 경우, master로 조정되어 연결된다.

다음은 ALTERNATE_LOCATOR를 사용한 configure 파일의 예이다.

```
[AGENT]
REQUEST_PORT=43581
RESPONSE_PORT=43581
LOCATOR_HOST=127.0.0.1
LOCATOR_PORT=42581
ALTERNATE_LOCATOR=LOCATOR1

[LOCATOR1]
HOST=127.0.0.1
PORT=42582
```

<a id="f576b4577e04a88c"></a>
#### KEEPALIVE_IDLE_TIME

<a id="28b13ef793124e6c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_IDLE_TIME |
| 설명 | tcp keepalive idle time for checking dead client session (sec) |
| Data type | INT |
| 기본값/ 범위 | 1 / 1 ~ 16383 |

Keep alive packet을 송신하기 전에 TCP 패킷이 송수신 되지 않는 상태로 지속되는 시간 (idle) 이다. 즉, KEEPALIVE_IDLE_TIME에 설정된 초 동안 TCP 패킷 교환이 이루어지지 않으면 dead connection을 감지하기 위해 keep alive mechanism을 수행한다.

<a id="dcdea4d4e8ab822f"></a>
#### KEEPALIVE_COUNT

<a id="98870b9832e6368e"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_COUNT |
| 설명 | tcp keepalive check count |
| Data type | INT |
| 기본값/ 범위 | 5 / 1 ~ 10 |

Keep alive mechanism을 수행하는 횟수이다.

<a id="b0c1ec08e52d067e"></a>
#### KEEPALIVE_INTERVAL

<a id="0ab027f048fedb6d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | KEEPALIVE_INTERVAL |
| 설명 | tcp keepalive packet interval (sec) |
| Data type | INT |
| 기본값/ 범위 | 5 |

Keep alive 패킷을 전송하는 시간 간격이다.

---

[← 51. glocator](51-glocator.md) · [전체 목차](../README.md) · [53. gloctl →](53-gloctl.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
