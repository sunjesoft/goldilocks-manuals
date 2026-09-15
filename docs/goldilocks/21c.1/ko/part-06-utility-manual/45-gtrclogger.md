<a id="7fbd83537810826f"></a>

# 45. gtrclogger

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/7fbd83537810826f)  
> 태그: `21c.1_35_tag`

[← 44. gmon](44-gmon.md) · [전체 목차](../README.md) · [46. glocator →](46-glocator.md)

<a id="428a8a01c70cdc58"></a>
## gtrclogger 소개

<a id="8ce0cf851c8f90af"></a>
### 정의

gtrclogger는 GOLDILOCKS의 log를 원격으로 수집하는 유틸리티이다.

GOLDILOCKS는 기본적으로 프로퍼티의 SYSTEM_LOGGER_DIR에 지정된 디렉토리 (기본값은 $GOLDILOCKS_DATA/trc)의 system.trc 파일에 서버에서 발생하는 이벤트와 trace log를 기록한다.

만약 다수의 서로 다른 instance를 운영하고 있는 환경이라면 각각의 서버에 발생하는 trace log를 별도로 모니터링해야 하는데 이에 대한 편의를 제공하고자 서로 다른 GOLDILOCKS instance의 trace log를 한 곳에 집중하여 수집할 수 있게 해 준다. gtrclogger는 다른 장비에서 실행 중인 여러 GOLDILOCKS의 trace log를 udp로 받아 파일에 저장한다.

gtrclogger는 원격 GOLDILOCKS로부터 trace log를 받아서 파일에 기록하는데, 이를 위해 원격 GOLDILOCKS는 다음과 같은 전송 프로퍼티를 가져야 한다.

- TRACE_LOGGER
- TRACE_LOGGER_REMOTE_HOST
- TRACE_LOGGER_REMOTE_PORT

<a id="19417bb435bc40d2"></a>
### 특징

- gtrclogger는 서버의 운영과 관계없이 실행할 수 있다.
- 여러 서버로부터 trace log를 받는 경우에도 받는 순서대로 하나의 파일에 저장한다.
- Trace log는 기본적으로 $(GOLDILOCKS_DATA)/trc/system.rmt.trc로 저장된다.
- system.rmt.trc가 10 Mbyte 보다 클 경우, system.rmt.trc_날짜_Index로 백업된다.

<a id="b12fdff9fd0befac"></a>
### 사용법

```
gtrclogger [options]
```

<a id="9797151faa2c944e"></a>
### Option

```
-s  --start        start gtrclogger
-q  --stop         stop gtrclogger
-p  --port         udp port for receive log (1024 ~ 49151): default 21470
-d  --dir          write file directory: default $(GOLDILOCKS_DATA)/system.rmt.trc
-h  --help         show gtrclogger help messages
```

<a id="9f340506493ce75f"></a>
## 사용 예

- 예제 1: 기본 port (21470)와 기본 디렉토리 ($GOLDILOCKS_DATA/trc)를 사용하여 gtrclogger를 실행한다.

```
$ gtrclogger --start

gtrclogger is started successfully.
```

- 예제 2: port 21471, 21472 두 개로 trace log를 받고 디렉토리는 $GOLDILOCKS_DATA/rmt_trc로 설정하여 gtrclogger를 실행한다.

```
$ gtrclogger -s -p 21471 -p 21472 -d $GOLDILOCKS_HOME/rmt_trc


ERR-HY000(11040): No such object 
(/home/lym1/workspace/product/Gliese/home/rmt_trc/system.rmt.trc)

$ mkdir $GOLDILOCKS_HOME/rmt_trc

$ gtrclogger -s -p 21471 -p 21472 -d $GOLDILOCKS_HOME/rmt_trc

gtrclogger is started successfully.
```

- 예제 3: gtrclogger를 종료한다.

```
$ gtrclogger -q

Stop Done.
```

---

[← 44. gmon](44-gmon.md) · [전체 목차](../README.md) · [46. glocator →](46-glocator.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
