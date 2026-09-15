<a id="e9aca969f462313c"></a>

# 41. gsyncher

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/e9aca969f462313c)  
> 태그: `20c.1_30_tag`

[← 40. tablediff](40-tablediff.md) · [전체 목차](../README.md) · [42. gmon →](42-gmon.md)

<a id="44beafe544021d08"></a>
## gsyncher 소개

<a id="1f2c847fc4981a5d"></a>
### 정의

gsyncher는 GOLDILOCKS에서 제공하는 shared memory 상의 log와 disk의 logfile을 동기화하는 유틸리티이다.   
gsyncher는 서버가 운영되는 중에 비정상적으로 종료되면 shared memory에 남겨진 최신 log를 동기화하여 logfile에 기록한다.

<a id="a2da5f552479e295"></a>
### 특징

- 서버가 운영되는 동안에는 gsyncher를 실행할 수 없다.
- gsyncher가 운영될 수 있는 서버의 STARTUP 단계는 OPEN 이다.
- gsyncher를 실행하면 shared memory에 결합된 다른 응용 프로그램들을 모두 종료시킨다.
- gsyncher를 실행하는 중에 logfile이 스위치 될 수 있고, 이 경우에는 controlfile을 작성한다.
- gsyncher는 controlfile과 log가 반영되는 logfile을 사전에 backup한다.
- 훼손된 controlfile이 복원되어야 gsyncher를 실행할 수 있다.

<a id="37365197b2fd3b63"></a>
### 사용법

```
gsyncher [options]
```

<a id="8ab85e34cc2ba054"></a>
### Option

```
-l  --log               Log trace msg
-s  --silent            Do not print message
-f  --home              home directory
-c  --copy-right        Do not print copy right
-b  --backup-path       Backup directory
-h  --help              Print help message
```

<a id="51577a6967b82a35"></a>
## 사용 예

- 예제 1: 서버가 정상적으로 운영되는 도중에 gsyncher를 실행하였다.

```
$ gsyncher -l

[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)

[SHARED MEM] Detached from shm.

ERR-HY000(53002): gmaster is active
```

- 예제 2: gsyncher가 실행될 수 있는 서버의 STARTUP 단계가 아니다.

```
$ gsyncher -l


[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)

[SHARED MEM] Detached from shm.

ERR-HY000(53000): invalid phase(MOUNT): executable phase is OPEN
```

- 예제 3: gsyncher를 실행하면 진행 과정이 출력된다. 실행 결과는 total buffer (0) bytes로써 모든 log가 logfile에 이미 flush 되어 동기화 할 log가 없다.

```
$ gsyncher --log


[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)
[CLEAR PROCESS] Process 'gbalancer' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.

[FLUSH] Log buffer flushed - Log group from id (0) to (0), lsn from (130784) to (130784), total buffer (0) bytes

[SHARED MEM] Detached from shm.

[FINI] Log sync complete.
```

    - --log 옵션을 사용하여 gsyncher 동작을 로그 파일에 기록한다.

```
$ cat $GOLDILOCKS_DATA/trc/gsyncher.trc 

=================================================
 gsyncher start
 TIME    : 2015-08-05 16:12:15.776633
=================================================


[2015-08-05 16:12:15.776763 THREAD(29199,139846497756928)] 
[INIT] Log started.

[2015-08-05 16:12:15.777113 THREAD(29199,139846497756928)] 
[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)

[2015-08-05 16:12:15.777208 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gbalancer' is cleared.

[2015-08-05 16:12:15.777297 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gdispatcher' is cleared.

[2015-08-05 16:12:15.777358 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gdispatcher' is cleared.

[2015-08-05 16:12:15.777416 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.777917 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.777993 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778051 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778107 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778577 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778652 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778710 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778766 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.778822 THREAD(29199,139846497756928)] 
[CLEAR PROCESS] Process 'gserver' is cleared.

[2015-08-05 16:12:15.818007 THREAD(29199,139846497756928)] 
[SHARED MEM] Detached from shm.

[2015-08-05 16:12:15.818100 THREAD(29199,139846497756928)] 
[FINI] Log sync complete.
```

- 예제 4: Lsn 130786부터 lsn 131012까지의 log가 log group 1에 flush 되었다.

```
$ gsyncher -l


[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)
[CLEAR PROCESS] Process 'gsql' is cleared.
[CLEAR PROCESS] Process 'gbalancer' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.

[FLUSH] Log buffer flushed - Log group from id (1) to (1), lsn from (130786) to (131012), total buffer (84480) bytes

[SHARED MEM] Detached from shm.

[FINI] Log sync complete.
```

- 예제 5: gsyncher가 동작하는 도중에 logfile switch가 발생하면 controlfile에 반영된다.

```
$ gsyncher -l

[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)
[CLEAR PROCESS] Process 'gsql' is cleared.
[CLEAR PROCESS] Process 'gbalancer' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gdispatcher' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gserver' is cleared.
[CLEAR PROCESS] Process 'gsql' is cleared.
[CLEAR PROCESS] Process 'gsql' is cleared.

[FLUSH] Log buffer flushed - Log group from id (2) to (3), lsn from (156412) to (178129), total buffer (16644096) bytes

[CONTROLFILE] Saving controlfile caused by logfile switching.

[CONTROLFILE] '/media/solid/ssd_home/work/product/Gliese/home/wal/control_0.ctl' control file is saved.

[CONTROLFILE] '/media/solid/ssd_home/work/product/Gliese/home/wal/control_1.ctl' control file is saved.

[SHARED MEM] Detached from shm.

[FINI] Log sync complete.
```

---

[← 40. tablediff](40-tablediff.md) · [전체 목차](../README.md) · [42. gmon →](42-gmon.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
