<a id="6f159f148ead5a53"></a>

# 38. gmon

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/6f159f148ead5a53)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 37. gsyncher](37-gsyncher.md) · [전체 목차](../README.md) · [39. gtrclogger →](39-gtrclogger.md)

<a id="83c8d9947d023be2"></a>
## gmon 소개

<a id="6464ab2fb5b40e00"></a>
### 정의

gmon은 GOLDILOCKS가 제공하는 데이터베이스(gmaster) 프로세스 감지 유틸리티이다.

<a id="24dfd227d385c646"></a>
### 기능

gmon은 데이터베이스 프로세스 (gmaster)의 동작 여부를 모니터링하다가 해당 프로세스가 관리자의 SHUTDOWN에 의해 종료되지 않고 비정상적으로 종료되면 [gsyncher](37-gsyncher.md#d209d39e430501eb)를 실행하고 종료한다. 이는 gsyncher를 실행하여 log 손실을 최대한 줄이기 위함이다.

gmon은 서버 프로퍼티 GMON_AUTOSTART를 1로 설정하여 자동 실행되도록 하거나 사용자가 직접 실행할 수 있다.

> 하나의 gmaster 프로세스는 하나의 gmon 프로세스만 감지할 수 있다.

<a id="7cdd2933439eba5b"></a>
### 사용법

```
gmon [options]
```

<a id="214718dbd821271c"></a>
### Option

```
-s  --start        Start gmon
-t  --stop         Stop gmon
-u  --status       Get gmon status
-o  --home         gmaster home path
-l  --silent       Suppress display message 
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help messages
```

<a id="f1add33319498085"></a>
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

[← 37. gsyncher](37-gsyncher.md) · [전체 목차](../README.md) · [39. gtrclogger →](39-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
