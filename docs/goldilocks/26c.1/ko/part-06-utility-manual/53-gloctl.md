<a id="a658035d7767fad3"></a>

# 53. gloctl

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/a658035d7767fad3)  
> 태그: `26c.1_0_tag`

[← 52. gagent](52-gagent.md) · [전체 목차](../README.md) · [54. 개요 →](../part-07-replication/54-개요.md)

<a id="46c88c3f586b1d6f"></a>
## gloctl 소개

<a id="45a75c6c0628d505"></a>
### 정의

gloctl은 GOLDILOCKS에서 제공하는 대화형 유틸리티로써 [glocator](51-glocator.md#ad25c1271ccf5dff)에 location을 제공하고 편집한다.  
gloctl은 User Datagram Protocol (UDP) 통신 프로토콜을 사용하여 glocator와 통신한다.

<a id="7b3b2f11a42ca078"></a>
### 사용법

```
gloctl [options]
```

<a id="eb28d3ce5f40f926"></a>
### Option

<a id="ac9676561f50a07e"></a>
#### help

<a id="eb459d79ae8308c5"></a>
##### 설명

Help 메시지를 출력한다.

<a id="e4f73aa2b7b4c5f8"></a>
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

<a id="a288e94d213ce0e0"></a>
#### conf

<a id="7a4f2d3f17886139"></a>
##### 설명

glocator와 통신하기 위해 [Configuration](#dcc445d54d569c6b) 설정 파일을 지정한다.  
지정하지 않을 경우, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf가 사용된다.

<a id="ac1e699a8e01b883"></a>
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

<a id="c47be5195bddaa9b"></a>
#### ip

<a id="d0b911693df1b44e"></a>
##### 설명

gloctl를 구동할 때 glocator의 IP address를 설정한다. DSN과 함께 사용될 때는 IP 설정값이 우선한다.

<a id="c190da5b170601d6"></a>
##### 사용 예

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

위의 예에서 glocator의 port는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="ec5c4131e2237c56"></a>
#### port

<a id="06939058e1dcb108"></a>
##### 설명

gloctl를 구동할 때 glocator의 port를 설정한다. DSN와 함께 사용될 때는 port 설정값이 우선한다.

<a id="05b805f96e7cee20"></a>
##### 사용 예

```
$ gloctl --port 42581

gLoctl>
```

위의 예에서 glocator의 IP는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="e62894009d69ad4e"></a>
#### import

<a id="c5e3901ecb94f2f8"></a>
##### 설명

대화형 모드가 아닌 파일 내의 gloctl 명령을 batch로 수행한다.

<a id="e65665c21d0af23c"></a>
##### 사용 예

```
$ gloctl --import import.txt

HELP                                                       
QUIT                                                       
IMPORT       {'FILE'}             Upload FILE to locations 
EXPORT       {'FILE'}             Download locations to FILE
ADD MEMBER   {DSN|{member_name {'host; port; db_home;'}}} Add member location      
DROP MEMBER  {member_name}        Drop member location     
SET TIMEOUT  {second}             Set time for session timeout

Add member succeeded.
```

- 위의 예에서 사용한 import.txt의 내용은 다음과 같다.

```
HELP
ADD MEMBER G1N3 'HOST=127.0.0.1;PORT=24581;DB_HOME=g1n3_home;'
```

<a id="e55f0a572dc2d259"></a>
#### silent

<a id="be15b59b0fb693e8"></a>
##### 설명

실행에 대한 gloctl의 메시지를 출력하지 않는다.

<a id="e61b1adf71eead01"></a>
##### 사용 예

```
$ gloctl --silent --import import.txt
```

<a id="314b9d73359fbf2f"></a>
#### no-copyright

<a id="9641841aca179ac4"></a>
##### 설명

실행에 대한 gloctl의 copy right와 버전 메시지를 출력하지 않는다.

<a id="7cdeb4536d79ccca"></a>
##### 사용 예

```
$ gloctl --no-copyright

gLoctl>
```

<a id="8b67447b2d702c12"></a>
## Interactive Command Reference

<a id="72e66e06fa0c45d7"></a>
### ADD MEMBER

<a id="5d9bfa9bfda74467"></a>
#### 구문

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="f03e838bebc8b8bc"></a>
#### 설명

glocator에 member 하나를 추가한다. odbc.ini에 존재하는 DSN 또는 member name과 필요한 location 정보를 입력해야 한다.


> 
> - Port는 glsnr의 port이다.
> - ADD MEMBER는 기존 member의 정보를 갱신할 때 사용할 수 있다. 이 때 해당 member가 failover하는 중이라면 갱신에 실패한다.
> 

<a id="880d7f021729aa52"></a>
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
LOCATOR_DSN=LOCATOR
```

- Member의 location을 서술하여 추가한다.

```
gLoctl> ADD MEMBER G1N2 'HOST=127.0.0.1; PORT=20201; DB_HOME=g1n2_home;'

Add member succeeded.

gLoctl>
```

<a id="f98645423b29bc40"></a>
### ADD SERVICE

<a id="a110f20dda575076"></a>
#### 구문

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="9b92ffef79862051"></a>
#### 설명

glocator에 service 하나를 추가한다. Service에 속한 node는 [glocator](51-glocator.md#ad25c1271ccf5dff)에서 관리되어야 하며 glocator에 동일한 node가 없으면 무시된다.

<a id="c5536a4c1c126751"></a>
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

> [odbc.ini 파일](../part-05-developer-manual/34-odbc.md#1edb504add88d834)에 glocator 속성을 기술하고 [glocator](51-glocator.md#ad25c1271ccf5dff)를 사용하면 gsqlnet과 기타 응용 프로그램은 service 목록 중 하나의 서버에 접속할 수 있다.

<a id="d60da71b362183b2"></a>
### DROP MEMBER

<a id="49840ff4d1a21bbc"></a>
#### 구문

```
DROP MEMBER member_name
```

<a id="d54c7dd684b0182c"></a>
#### 설명

member_name에 해당하는 member를 glocator에서 삭제한다.

> 삭제하려는 member가 failover 과정 중에 있다면 삭제할 수 없다.

<a id="28a04035b2fe0b20"></a>
#### 사용 예

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="354d32df9df26230"></a>
### DROP SERVICE

<a id="e388b6eb38f646e1"></a>
#### 구문

```
DROP MEMBER service_name
```

<a id="f05956a7df045595"></a>
#### 설명

service_name에 해당하는 service를 glocator에서 삭제한다.

<a id="2900375f9f63d8ac"></a>
#### 사용 예

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="9153d1198cdb1d99"></a>
### EXPORT

<a id="698e47f1328f4557"></a>
#### 구문

```
EXPORT {'FILE'}
```

<a id="0963ff7042b8bb1c"></a>
#### 설명

glocator로부터 location 정보를 받아 파일에 저장한다.

<a id="6d210b60519c6a9c"></a>
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
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="9674ed6aaafcb3b9"></a>
### HELP

<a id="0e3461b756fa9510"></a>
#### 구문

```
HELP
```

<a id="5c025d4fc7ac00c0"></a>
#### 설명

gloctl의 대화형 모드에서 명령어 목록을 보여준다.

<a id="3c0ae864993a6df8"></a>
#### 사용 예

```
gLoctl> HELP

HELP
QUIT
IMPORT {'FILE'} Upload FILE to locations
EXPORT {'FILE'} Download locations to FILE
ADD MEMBER {DSN|{member_name {'host; port; db_home;'}}} Add member location
DROP MEMBER {member_name} Drop member location
SET TIMEOUT {second} Set time for session timeout
ADD SERVICE  {service_name {'member_name; ... '} } Add service
DROP SERVICE {service_name}       Drop service 

gLoctl>
```

<a id="4a07964cfd54411a"></a>
### IMPORT

<a id="77519396f2ada73c"></a>
#### 구문

```
IMPORT {'FILE'}
```

<a id="a9fe5a25ef42bf3c"></a>
#### 설명

ini 형식의 파일을 이용하여 glocator에 location을 전송한다.

<a id="bf8afd0ca1c6a777"></a>
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
HOST = 127.0.0.1
DB_HOME = g1n1_home

[G1N3]
PORT = 24581
HOST = 127.0.0.1
DB_HOME = g1n3_home
```

<a id="185ba5371144dd29"></a>
### QUIT

<a id="fc1d022490020dcd"></a>
#### 설명

gloctl을 종료한다.

<a id="b08b8b4293249eae"></a>
#### 구문

```
QUIT
```

<a id="36e6ad1f4875ae58"></a>
### SET TIMEOUT

<a id="3cb90a6c89c04b77"></a>
#### 설명

glocator의 TIMEOUT을 설정한다.

<a id="400030c21428ff27"></a>
#### 구문

```
SET TIMEOUT {second}
```

<a id="105c232224c65d10"></a>
#### 사용 예

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="34970e85ba4a5a48"></a>
## Location File

Location file은 gloctl에서 glocator로 노드의 location 정보를 업로드하거나 다운로드한다.

<a id="11a2cb83235698a8"></a>
### 설명

Location file 형식은 [데이터 원본 스펙](../part-05-developer-manual/34-odbc.md#8016e190132bb886) 파일의 형식과 유사하다.

```
[node_name]
HOST = host_address
PORT = port_no
DB_HOME = db_home_path

[SERVICE]
service_name = node_name {, node_name}*
```

Location file의 location 키워드는 다음 표와 같다.

**Location infornation**

<a id="e933693300ad71ea"></a>
| 키워드 | 설명 |
| --- | --- |
| node_name | 노드 이름이다. |
| HOST | 노드의 IP 주소이다. |
| PORT | 노드에서 실행된 glsnr의 port 번호이다. |
| DB_HOME | 노드의 홈 디렉토리를 설정한다. |

[SERVICE]는 서비스 힌트 목록을 나열하는 고정 키워드이다. glocator에 등록되어 있거나 등록할 서비스 힌트 목록은 SERVICE 키워드 아래에 나열된다.

HOST와 PORT 키워드는 반드시 입력되어야 하며 누락할 경우 에러가 발생한다.

다음은 location file을 구성하는 예이다.

```
[G1N1]
HOST = 192.168.0.101
PORT = 20101
DB_HOME = g1n1_home

[G1N2]
HOST = 192.168.0.102
PORT = 20102
DB_HOME = g1n2_home

[G2N1]
HOST = 192.168.0.201
PORT = 20201
DB_HOME = g2n1_home

[G2N2]
HOST = 192.168.0.202
PORT = 20202
DB_HOME = g2n2_home

[SERVICE]
service_1 = G1N1,G2N1
service_2 = G1N1,G1N2
```

<a id="dcc445d54d569c6b"></a>
## Configuration

gloctl의 환경파일은 $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf이다. gloctl의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 [conf](#a288e94d213ce0e0) 옵션으로 환경 파일을 지정하여 gloctl을 구동하면 된다.

gloctl이 실행 중인 상태에서 gloctl의 환경을 변경하여 적용하려면 gloctl을 멈춘 후에 구동 환경을 변경 하고 다시 시작해야 한다.

<a id="e9fa649541f9f974"></a>
### PORT

<a id="b392b7d3f1de5c5c"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl이 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 44581 / 1024 ~ 49151 |

gloctl이 사용하는 소켓의 port를 설정한다.

<a id="fc16182aa2ba332e"></a>
### LOCATOR_HOST

<a id="131a5a6f27121099"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 host address이다. |
| Data type | STRING |
| 기본값/ 범위 | 127.0.0.1 |

glocator의 host address를 설정한다.

<a id="38d6d96fabd6e673"></a>
### LOCATOR_PORT

<a id="f2e22b504577f315"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024 ~ 49151 |

glocator의 port를 설정한다.

<a id="ba4ec271a80a3dec"></a>
### MESSAGE_TIMEOUT

<a id="efba946c578d2615"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_TIMEOUT |
| 설명 | gloctl이 glocator로부터 응답을 기다리는 시간을 설정한다. (second) |
| Data type | INT |
| 기본값/ 범위 | 10 / 0 ~ 2147483647 |

gloctl이 glocator로 패킷을 보낸 후에 응답을 기다리는 시간을 설정한다.

---

[← 52. gagent](52-gagent.md) · [전체 목차](../README.md) · [54. 개요 →](../part-07-replication/54-개요.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
