<a id="ecd391ad5392033a"></a>

# 46. gloctl

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/ecd391ad5392033a)  
> 태그: `20c.1_30_tag`

[← 45. gagent](45-gagent.md) · [전체 목차](../README.md) · [47. 개요 →](../part-07-replication/47-개요.md)

<a id="b6ece812079eb266"></a>
## gloctl 소개

<a id="7a4297148066a183"></a>
### 정의

gloctl은 GOLDILOCKS에서 제공하는 대화형 유틸리티로써 [glocator](44-glocator.md#d00263d8ce9e1ce2)에 location을 제공하고 편집한다.  
gloctl은 User Datagram Protocol (UDP) 통신 프로토콜을 사용하여 glocator와 통신한다.

<a id="7be9ca3783338dec"></a>
### 사용법

```
gloctl [options]
```

<a id="3706500d7496f7ec"></a>
### Option

<a id="c80e29e323551068"></a>
#### help

<a id="81ea7edc4a7295fb"></a>
##### 설명

Help 메시지를 출력한다.

<a id="22e8168e93cec773"></a>
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

<a id="4dc6a7e8320f3e98"></a>
#### conf

<a id="4c510585da0127a2"></a>
##### 설명

glocator와 통신하기 위해 [Configuration](#31946b2faf3065a0) 설정 파일을 지정한다.  
지정하지 않을 경우, $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf가 사용된다.

<a id="92a72b641e106451"></a>
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

<a id="a60a72dd90d7d5e6"></a>
#### ip

<a id="f87ddb4d6299ec6a"></a>
##### 설명

gloctl를 구동할 때 glocator의 IP address를 설정한다. DSN과 함께 사용될 때는 IP 설정값이 우선한다.

<a id="8762ef983ff43d91"></a>
##### 사용 예

```
$ gloctl --ip 127.0.0.1

gLoctl>
```

위의 예에서 glocator의 port는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="3879f7a585e263a5"></a>
#### port

<a id="24de70509d955287"></a>
##### 설명

gloctl를 구동할 때 glocator의 port를 설정한다. DSN와 함께 사용될 때는 port 설정값이 우선한다.

<a id="7afe19f49eb38866"></a>
##### 사용 예

```
$ gloctl --port 42581

gLoctl>
```

위의 예에서 glocator의 IP는 odbc.ini에서 DSN 기본값 LOCATOR를 이용하여 얻는다.

<a id="3030f5a1f85bb52b"></a>
#### import

<a id="7d6ff1e948889fee"></a>
##### 설명

대화형 모드가 아닌 파일 내의 gloctl 명령을 batch로 수행한다.

<a id="13f3f979d1ea5ca7"></a>
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

<a id="72d8833fff109420"></a>
#### silent

<a id="88679f3c38f9c86c"></a>
##### 설명

실행에 대한 gloctl의 메시지를 출력하지 않는다.

<a id="e494f5e134701da0"></a>
##### 사용 예

```
$ gloctl --silent --import import.txt
```

<a id="18b441c48ca70099"></a>
#### no-copyright

<a id="014049fe9d87cf38"></a>
##### 설명

실행에 대한 gloctl의 copy right와 버전 메시지를 출력하지 않는다.

<a id="29a61e53646b6838"></a>
##### 사용 예

```
$ gloctl --no-copyright

gLoctl>
```

<a id="e77bfad34d66d62f"></a>
## Interactive Command Reference

<a id="dba9a19d9534b6fa"></a>
### ADD MEMBER

<a id="1d11d7007b03c24a"></a>
#### 구문

```
ADD MEMBER {DSN | member_name {'host; port; db_home;'}}
```

<a id="0db7cc5c7a94aea3"></a>
#### 설명

glocator에 member 하나를 추가한다. odbc.ini에 존재하는 DSN 또는 member name과 필요한 location 정보를 입력해야 한다.


> 
> - Port는 glsnr의 port이다.
> - ADD MEMBER는 기존 member의 정보를 갱신할 때 사용할 수 있다. 이 때 해당 member가 failover하는 중이라면 갱신에 실패한다.
> 

<a id="2a6e696ad65c64b0"></a>
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

<a id="96e217146c757a4d"></a>
### ADD SERVICE

<a id="a5243fda88a32b62"></a>
#### 구문

```
ADD SERVICE service_name {'member_name; ... '}
```

<a id="f9a1183520f31c71"></a>
#### 설명

glocator에 service 하나를 추가한다. Service에 속한 node는 [glocator](44-glocator.md#d00263d8ce9e1ce2)에서 관리되어야 하며 glocator에 동일한 node가 없으면 무시된다.

<a id="181ae6daa8148770"></a>
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

> [odbc.ini 파일](../part-05-developer-manual/29-odbc.md#f1a0bc8659eada10)에 glocator 속성을 기술하고 [glocator](44-glocator.md#d00263d8ce9e1ce2)를 사용하면 gsqlnet과 기타 응용 프로그램은 service 목록 중 하나의 서버에 접속할 수 있다.

<a id="18e813f1255e0a4d"></a>
### DROP MEMBER

<a id="f3693e46f394aede"></a>
#### 구문

```
DROP MEMBER member_name
```

<a id="ae15d0f8d95c503d"></a>
#### 설명

member_name에 해당하는 member를 glocator에서 삭제한다.

> 삭제하려는 member가 failover 과정 중에 있다면 삭제할 수 없다.

<a id="0102251ecdf962ee"></a>
#### 사용 예

```
gLoctl> DROP MEMBER G1N2

Drop member succeeded.

gLoctl>
```

<a id="0289e75aa77eb5b8"></a>
### DROP SERVICE

<a id="27e9887b823f5df7"></a>
#### 구문

```
DROP MEMBER service_name
```

<a id="899f09519133291e"></a>
#### 설명

service_name에 해당하는 service를 glocator에서 삭제한다.

<a id="6944ba1fc20ceb1e"></a>
#### 사용 예

```
gLoctl> DROP SERVICE S1

Drop service succeeded.

gLoctl>
```

<a id="2343c512cab91237"></a>
### EXPORT

<a id="4068aef88a662743"></a>
#### 구문

```
EXPORT {'FILE'}
```

<a id="7781d5485e9bf6ef"></a>
#### 설명

glocator로부터 location 정보를 받아 파일에 저장한다.

<a id="ac5598cd8c04d1d8"></a>
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

<a id="fb64ea6218f6ea99"></a>
### HELP

<a id="8d6ce04b92e8b3d6"></a>
#### 구문

```
HELP
```

<a id="941f0c6306bf610d"></a>
#### 설명

gloctl의 대화형 모드에서 명령어 목록을 보여준다.

<a id="c6b1bd98b991b05f"></a>
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

<a id="de3fbed5cef6ea0a"></a>
### IMPORT

<a id="39aa060a0ba845e7"></a>
#### 구문

```
IMPORT {'FILE'}
```

<a id="590b9d84ee620acb"></a>
#### 설명

ini 형식의 파일을 이용하여 glocator에 location을 전송한다.

<a id="ed01ed52fda22158"></a>
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

<a id="c53796d9b1effcfa"></a>
### QUIT

<a id="fd0faea1e1d1eca8"></a>
#### 설명

gloctl을 종료한다.

<a id="a915ef954b6bee1e"></a>
#### 구문

```
QUIT
```

<a id="45dab7e6c742c949"></a>
### SET TIMEOUT

<a id="939969d4cb3e4936"></a>
#### 설명

glocator의 TIMEOUT을 설정한다.

<a id="9b91d705ae535e57"></a>
#### 구문

```
SET TIMEOUT {second}
```

<a id="ef293e4501e0aa22"></a>
#### 사용 예

```
gLoctl> set timeout 120

Set timeout.

gLoctl>
```

<a id="a39f74e06c202330"></a>
## Location File

Location file은 gloctl에서 glocator로 노드의 location 정보를 업로드하거나 다운로드한다.

<a id="516f70458e103e3a"></a>
### 설명

Location file 형식은 [데이터 원본 스펙](../part-05-developer-manual/29-odbc.md#231e925fcf0f36c5) 파일의 형식과 유사하다.

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

<a id="f6e45cf97a97d759"></a>
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

<a id="31946b2faf3065a0"></a>
## Configuration

gloctl의 환경파일은 $GOLDILOCKS_DATA/conf/goldilocks.gloctl.conf이다. gloctl의 구동 환경을 변경하려면 해당 파일의 내용을 변경하거나 [conf](#4dc6a7e8320f3e98) 옵션으로 환경 파일을 지정하여 gloctl을 구동하면 된다.

gloctl이 실행 중인 상태에서 gloctl의 환경을 변경하여 적용하려면 gloctl을 멈춘 후에 구동 환경을 변경 하고 다시 시작해야 한다.

<a id="8eee4f0142902761"></a>
### PORT

<a id="bdcc7c119425efc1"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl이 사용하는 port이다. |
| Data type | INT |
| 기본값/ 범위 | 44581 / 1024 ~ 49151 |

gloctl이 사용하는 소켓의 port를 설정한다.

<a id="131f10b419b0778a"></a>
### LOCATOR_HOST

<a id="511412e2e88d88d4"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 host address이다. |
| Data type | STRING |
| 기본값/ 범위 | 127.0.0.1 |

glocator의 host address를 설정한다.

<a id="73de104b131fd565"></a>
### LOCATOR_PORT

<a id="90153cd0c81a2551"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | PORT |
| 설명 | gloctl과 통신하는 glocator의 port이다. |
| Data type | INT |
| 기본값/ 범위 | 42581 / 1024 ~ 49151 |

glocator의 port를 설정한다.

<a id="78bda91af6109f71"></a>
### MESSAGE_TIMEOUT

<a id="719b3628cb853ffd"></a>
| 항목 | 설명 |
| --- | --- |
| 이름 | MESSAGE_TIMEOUT |
| 설명 | gloctl이 glocator로부터 응답을 기다리는 시간을 설정한다. (second) |
| Data type | INT |
| 기본값/ 범위 | 10 / 0 ~ 2147483647 |

gloctl이 glocator로 패킷을 보낸 후에 응답을 기다리는 시간을 설정한다.

---

[← 45. gagent](45-gagent.md) · [전체 목차](../README.md) · [47. 개요 →](../part-07-replication/47-개요.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
