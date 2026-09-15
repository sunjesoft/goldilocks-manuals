<a id="21bac538710a7115"></a>

# 42. gloctl

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/21bac538710a7115)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 41. gagent](41-gagent.md) · [전체 목차](../README.md) · [43. 개요 →](../part-07-replication/43-개요.md)

<a id="2c692a75c497c7d5"></a>
## gloctl 소개

<a id="2e322baf91646f80"></a>
### 정의

gloctl은 GOLDILOCKS에서 제공하는 대화형 유틸리티로써 [glocator](40-glocator.md#8c29744666a187bf)에 location을 제공하고 편집한다.  
gloctl은 User Datagram Protocol (UDP) 통신 프로토콜을 사용하여 glocator와 통신한다.

<a id="dd989f298bee8a0e"></a>
### 사용법

```
gloctl [options]
```

<a id="58fbde9a2d978dd9"></a>
### Option

<a id="a932798e066c2855"></a>
#### help

<a id="cf6aafe524022a9c"></a>
##### 설명

Help 메시지를 출력한다.

<a id="dc0a35022040d5cb"></a>
##### 사용 예

```
$ gloctl --help

Usage:
 gloctl [options]

Options:

-c  --conf         User configure file
-i  --ip           Locator host ip
-p  --port         Locator port number
-o  --import       Import control FILE
-l  --silent       Suppress the display of result message and echoing commands
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help message
```

<a id="976974a6e39954d8"></a>
#### conf

<a id="df420839ae80d7ea"></a>
##### 설명

glocator와 통신하기 위해 [Configuration](#56f751499f970703) 설정 파일을 지정한다.  
지정하지 않을 경우, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf가 사용된다.

<a id="764f20ce4ec42721"></a>
##### 사용 예

```
$ gloctl --conf gloctl.conf

gLoctl>
```

- 위의 예에서 사용한 gloctl.conf 파일의 내용은 다음과 같다.

```
[GLOCTL]
# Port number (1024 ~ 49151)
PORT = 44581

# Locator address
LOCATOR_HOST = 127.0.0.1

# Locator port number (1024 ~ 49151)
LOCATOR_PORT = 42581

# Time out to receive message from glocator (second)
# second ( 0 ~ 2147483647 )
MESSAGE_TIMEOUT = 10
```

<a id="6db9a83d3260319d"></a>
#### ip

<a id="1b3671fa85edb740"></a>
##### 설명

gloctl를 구동할 때 glocator의 IP address를 설정한다. DSN과 함께 사용될 때는 IP 설정값이 우선한다.

<a id="455fb94f75acebc7"></a>
##### 사용 예

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

위의 예에서 glocator의 port는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="c969cf45b894b812"></a>
#### port

<a id="5085f128e6c4c90e"></a>
##### 설명

gloctl를 구동할 때 glocator의 port를 설정한다. DSN과 함께 사용될 때는 port 설정값이 우선한다.

<a id="58e367210a497fe0"></a>
##### 사용 예

```
$ gloctl --port 42581

gLoctl>
```

위의 예에서 glocator의 IP는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="99cfeba3570bff17"></a>
#### import

<a id="1319b493dd785a11"></a>
##### 설명

대화형 모드가 아닌 파일 내의 gloctl 명령을 batch로 수행한다.

<a id="8041f397efc95bcf"></a>
##### 사용 예

```
$ gloctl --import import.txt

HELP                                                       
QUIT                                                       
IMPORT       {'FILE'}             Upload FILE to locations 
EXPORT       {'FILE'}             Download locations to FILE
ADD MEMBER   {DSN|{member_name {'host; port; db_home; agent_port;'}}} Add member location      
DROP MEMBER  {member_name}        Drop member location     
SET TIMEOUT  {second}             Set time for session timeout

Add member succeeded.
```

- 위의 예에서 사용한 import.txt의 내용은 다음과 같다.

```
HELP
ADD MEMBER G1N3 'HOST=127.0.0.1;PORT=24581;DB_HOME=g1n3_home;AGENT_PORT= 44581;'
```

<a id="ef780959adecb777"></a>
#### silent

<a id="08ec7e66120b2cc1"></a>
##### 설명

실행에 대한 gloctl의 메시지를 출력하지 않는다.

<a id="8632ccff2d6550f5"></a>
##### 사용 예

```
$ gloctl --silent --import import.txt
```

<a id="91753018df72d7f6"></a>
#### no-copyright

<a id="f4ea1264951ee5bc"></a>
##### 설명

실행에 대한 gloctl의 copyright과 버전 메시지를 출력하지 않는다.

<a id="b4d8e210045c9fe4"></a>
##### 사용 예

```
$ gloctl --no-copyright

gLoctl>
```

<a id="1a1a9cd2f2f233dc"></a>
## Interactive Command Reference

<a id="45bd4e3889031ad9"></a>
### ADD MEMBER

<a id="8a1ebc981832ce94"></a>
#### 구문

```
ADD MEMBER {DSN | member_name {'host; port; db_home; agent_port;'}}
```

<a id="e9de13aa856ffd20"></a>
#### 설명

glocator에 member 하나를 추가한다. odbc.ini에 존재하는 DSN 또는 member name과 필요한 location 정보를 입력해야 한다.


> 
> - Port는 glsnr의 port이다.
> - ADD MEMBER는 기존 member의 정보를 갱신할 때 사용할 수 있다. 이 때 해당 member가 failover하는 중이라면 갱신에 실패한다.
> 

<a id="9f2d65f0ba781b40"></a>
#### 사용 예

odbc.ini의 DSN을 이용하여 ADD MEMBER를 수행한다.

```
gLoctl> ADD MEMBER G1N1

Add member succeeded.

gLoctl>
```

- 다음은 odbc.ini의 내용이다.

```
[G1N1]
HOST=127.0.0.1
PORT=20101
DB_HOME= g1n1_home
AGENT_PORT=43581
LOCATOR_DSN=LOCATOR
```

- Member의 location을 서술하여 추가한다.

```
gLoctl> ADD MEMBER G1N2 'HOST=127.0.0.1; PORT=20201; DB_HOME=g1n2_home; AGENT_PORT= 43581'

Add member succeeded.

gLoctl>
```

<a id="6d8244ec8b476667"></a>
### ADD SERVICE

<a id="ea1fd797641ea250"></a>
#### 구문

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="fd17bde5afe04cb9"></a>
#### 설명

glocator에 service 하나를 추가한다. Service에 속한 node는 [glocator](40-glocator.md#8c29744666a187bf)에서 관리되어야 하며 glocator에 동일한 node가 없으면 무시된다.

<a id="764e82e7ed7dff6e"></a>
#### 사용 예

ADD SERVICE로 service s1을 추가한다.

```
gLoctl> ADD SERVICE S1 'G1N1;G1N2;G2N1'

Add service succeeded.

gLoctl>
```

- 다음은 odbc.ini의 내용이다.

```
[GOLDILOCKS]
HOST=127.0.0.1
PORT=22581
LOCATOR_DSN=LOCATOR
LOCATOR_SERVICE=S1
[LOCATOR]
HOST=127.0.0.1
PORT=42581
```

> [odbc.ini 파일](../part-05-developer-manual/25-odbc.md#78b0fc955ee2c6e5)에 glocator 속성을 기술하고 [glocator](40-glocator.md#8c29744666a187bf)를 사용하면 gsqlnet과 기타 응용 프로그램은 service 목록 중 하나의 서버에 접속할 수 있다.

<a id="99bcb6a504c645e4"></a>
### DROP MEMBER

<a id="0744eb82788f0632"></a>
#### 구문

```
DROP MEMBER member_name
```

<a id="9b03c42e5bfb443b"></a>
#### 설명

member_name에 해당하는 member를 glocator에서 삭제한다.

> 삭제하려는 member가 failover 과정 중에 있다면 삭제할 수 없다.

<a id="4e32a3eb3990967f"></a>
#### 사용 예

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="2fce60e5bd31de03"></a>
### DROP SERVICE

<a id="17c504208a335e67"></a>
#### 구문

```
DROP MEMBER service_name
```

<a id="e3fef84a51a0ad0c"></a>
#### 설명

service_name에 해당하는 service를 glocator에서 삭제한다.

<a id="9206465332a42517"></a>
#### 사용 예

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="e16b49016e614806"></a>
### EXPORT

<a id="ec97259186b3abd7"></a>
#### 구문

```
EXPORT {'FILE'}
```

<a id="2ce35d20d0fba333"></a>
#### 설명

glocator로부터 location 정보를 받아 파일에 저장한다.

<a id="978b0ee80e46231f"></a>
#### 사용 예

Location.txt라는 파일에 location 정보를 다운로드 한다.

```
gLoctl> EXPORT 'Location.txt'

Export file succeeded.

gLoctl>
```

- 위 예의 Location.txt 파일 내용은 다음과 같다.

```
[G1N1]
PORT = 20101
AGENT_PORT = 0
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
AGENT_PORT = 44581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="3e19884f463f937f"></a>
### HELP

<a id="7b6136ab510e7cf1"></a>
#### 구문

```
HELP
```

<a id="2ef1cb577d2a4e53"></a>
#### 설명

gloctl의 대화형 모드에서 명령어 목록을 보여준다.

<a id="7b59e3f879eccd37"></a>
#### 사용 예

```
gLoctl> HELP

HELP
QUIT
IMPORT {'FILE'} Upload FILE to locations
EXPORT {'FILE'} Download locations to FILE
ADD MEMBER {DSN|{member_name {'host; port; db_home; agent_port;'}}} Add member location
DROP MEMBER {member_name} Drop member location
SET TIMEOUT {second} Set time for session timeout
ADD SERVICE  {service_name {'member_name; ... '} } Add service
DROP SERVICE {service_name}       Drop service 

gLoctl>
```

<a id="1eead03d615019d8"></a>
### IMPORT

<a id="f5a37e20cdc62e91"></a>
#### 구문

```
IMPORT {'FILE'}
```

<a id="bb43cdc9c1f05b83"></a>
#### 설명

ini 형식의 파일을 이용하여 glocator에 location을 전송한다.

<a id="53bcf24375b86c48"></a>
#### 사용 예

Location.txt 파일에 있는 내용을 glocator로 보낸다.

```
gLoctl> IMPORT 'Location.txt'

Import file succeeded.

gLoctl>
```

- 위 예의 Location.txt 파일 내용은 다음과 같다.

```
[G1N1]
PORT = 20101
AGENT_PORT = 0
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
AGENT_PORT = 44581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="90cb13092f682559"></a>
### QUIT

<a id="e2d69c0456001337"></a>
#### 설명

gloctl을 종료한다.

<a id="fe76eda1e96947b7"></a>
#### 구문

```
QUIT
```

<a id="3ab813ee921789a9"></a>
### SET TIMEOUT

<a id="860cf0d22368a95c"></a>
#### 설명

glocator의 TIMEOUT을 설정한다.

<a id="1500db1b7059bc96"></a>
#### 구문

```
SET TIMEOUT {second}
```

<a id="f2d68425d8be4789"></a>
#### 사용 예

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="e85c8553b0240431"></a>
## Location File

Location file은 gloctl에서 glocator로 노드의 location 정보를 업로드하거나 다운로드한다.

<a id="5b86dfd336692aa9"></a>
### 설명

Location file 형식은 [데이터 원본 스펙](../part-05-developer-manual/25-odbc.md#0c487f04041812c5) 파일의 형식과 유사하다.

```
[node_name]
HOST = host_address
PORT = port_no
DB_HOME = db_home_path
AGENT_PORT = agent_port_no 

[SERVICE]
service_name = node_name {, node_name}*
```

Location file의 location 키워드는 다음 표와 같다.

**Location infornation**

<a id="da1acce0f5be39a3"></a>
| 키워드 | 설명 |
| --- | --- |
| node_name | 노드 이름이다. |
| HOST | 노드의 IP 주소이다. |
| PORT | 노드에서 실행된 glsnr의 port 번호이다. |
| DB_HOME | 노드의 홈 디렉토리를 설정한다. |
| AGENT_PORT | 노드에서 실행된 gagent의 port 번호이다. |

[SERVICE]는 서비스 힌트 목록을 나열하는 고정 키워드이다. glocator에 등록되어 있거나 등록할 서비스 힌트 목록은 SERVICE 키워드 아래에 나열된다.

HOST와 PORT 키워드는 반드시 입력해야 하고 누락할 경우 에러가 발생한다.

다음은 location file을 구성하는 예이다.

```
[G1N1]
HOST = 192.168.0.101
PORT = 20101
DB_HOME = g1n1_home
AGENT_PORT = 40101

[G1N2]
HOST = 192.168.0.102
PORT = 20102
DB_HOME = g1n2_home
AGENT_PORT = 40102

[G2N1]
HOST = 192.168.0.201
PORT = 20201
DB_HOME = g2n1_home
AGENT_PORT = 40201

[G1N2]
HOST = 192.168.0.202
PORT = 20202
DB_HOME = g2n1_home
AGENT_PORT = 40202


[SERVICE]
service_1 = G1N1,G2N1
service_2 = G1N1,G1N2
```

<a id="56f751499f970703"></a>
## Configuration

gloctl의 환경 파일은 $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf이다. gloctl의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 [conf](#976974a6e39954d8) 옵션으로 환경 파일을 지정하여 gloctl을 구동하면 된다.

gloctl이 실행 중인 상태에서 gloctl의 환경을 변경하여 적용하려면 gloctl을 멈춘 후에 구동 환경을 변경 하고 다시 시작해야 한다.

<a id="a13daad3bf87d158"></a>
### PORT

<a id="547178d4eb606a35"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl이 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 44581 / 1024 ~ 49151 |

gloctl이 사용하는 소켓의 port를 설정한다.

<a id="16b7b08794ef463f"></a>
### LOCATOR_HOST

<a id="3c3e68279efa7dc7"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 host address이다. |
| Data type | STRING |
| 기본값/ 범위 | 127.0.0.1 |

glocator의 host address를 설정한다.

<a id="88a84d4bf159a70c"></a>
### LOCATOR_PORT

<a id="a35878d2b7e72357"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024 ~ 49151 |

glocator의 port를 설정한다.

<a id="1b63565e115749d4"></a>
### MESSAGE_TIMEOUT

<a id="4dc413c17a527f7d"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_TIMEOUT |
| 설명 | gloctl이 glocator로부터 응답을 기다리는 시간을 설정한다. (second) |
| Data type | INT |
| 기본값/ 범위 | 10 / 0 ~ 2147483647 |

gloctl이 glocator로 패킷을 보낸 후에 응답을 기다리는 시간을 설정한다.

---

[← 41. gagent](41-gagent.md) · [전체 목차](../README.md) · [43. 개요 →](../part-07-replication/43-개요.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
