<a id="59e46eee9a8743ee"></a>

# 42. gmon

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/59e46eee9a8743ee)  
> 태그: `20c.1_30_tag`

[← 41. gsyncher](41-gsyncher.md) · [전체 목차](../README.md) · [43. gtrclogger →](43-gtrclogger.md)

<a id="6dfbe5666f4b26e1"></a>
## gmon 소개

<a id="a38018ec75bc61a3"></a>
### 정의

gmon은 GOLDILOCKS가 제공하는 데이터베이스 (gmaster) 프로세스 감지 유틸리티이다.

<a id="d7ac76214f315b72"></a>
### 기능

gmon은 데이터베이스 프로세스 (gmaster)의 동작 여부를 모니터링하다가 해당 프로세스가 관리자의 SHUTDOWN에 의해 종료되지 않고 비정상적으로 종료되면 [gsyncher](41-gsyncher.md#e9aca969f462313c)를 실행하고 종료한다. 이는 gsyncher를 실행하여 log 손실을 최대한 줄이기 위함이다.

gmon은 서버 프로퍼티 GMON_AUTOSTART를 1로 설정하여 자동 실행되도록 하거나 사용자가 직접 실행할 수 있다.

> 하나의 gmaster 프로세스는 하나의 gmon 프로세스만 감지할 수 있다.

<a id="afd25baa6cfc6234"></a>
### 사용법

```
gmon [options]
```

<a id="1d500159e3aaf7af"></a>
### Option

```
-s  --start        Start gmon
-t  --stop         Stop gmon
-u  --status       Get gmon status
-o  --home         gmaster home path
-d  --uds_dir      unix domain socket directory
-l  --silent       Suppress display message 
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help messages
```

<a id="5705d1d99ee9a29d"></a>
#### start

gmon을 시작한다.

<a id="39e8ef926b3fe43e"></a>
#### stop

gmon을 종료한다.

<a id="51e56856759462f4"></a>
#### status

gmon process의 상태를 확인한다.

<a id="c03114cb5e6471cd"></a>
#### home

Database home 디렉토리이다. 생략할 경우 GOLDILOCKS_DATA 환경 변수에 설정된 값을 사용한다.

<a id="772b65fdb3926a22"></a>
#### uds_dir

unix domain socket이 생성되는 디렉토리를 설정한다. 디렉토리의 최대 길이는 50 바이트이다. 기본값은 /tmp 이다.

<a id="8a25ea33d196640f"></a>
#### silent

결과 메시지를 출력하지 않는다.

<a id="d0c96b8c2474086a"></a>
#### no-copyright

Copyright와 version을 출력하지 않는다.

<a id="c6ba709cac999b46"></a>
#### help

도움말을 출력한다.

<a id="457ee679d0dbb427"></a>
## 사용 예

- 예제 1: 기본 경로 ($GOLDILOCKS_DATA)를 사용하여 gmon을 실행한다.

```
$ gmon --start

gmon is started.
```

- 예제 2: home 경로를 지정하여 gmon을 실행한다. 상대 경로를 사용할 경우 $GOLDILOCKS_DATA를 베이스로 하여 home 경로가 지정된다.

```
$ gmon --start --home g1n1_home

gmon is started.
```

- 예제 3: home 경로를 절대 경로로 지정하여 gmon을 실행한다. 절대 경로를 사용할 경우, 지정된 경로로 home 경로가 지정된다.

```
$ gmon --start --home /g1n1_home

gmon is started.
```

- 예제 4: gmon process의 상태를 확인한다.

```
$ gmon --status --home /g1n1_home

gmon is running(19119).
```

- 예제 5: gmon process를 종료한다.

```
$ gmon --stop --home /g1n1_home

gmon is stopped.
```

---

[← 41. gsyncher](41-gsyncher.md) · [전체 목차](../README.md) · [43. gtrclogger →](43-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
